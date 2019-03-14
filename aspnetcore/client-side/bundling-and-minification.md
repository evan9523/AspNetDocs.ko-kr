---
title: ASP.NET Core에서 정적 자산 번들링 및 축소하기
author: scottaddie
description: 번들링 및 축소 기술을 적용하여 ASP.NET Core 웹 응용 프로그램에서 정적 리소스를 최적화하는 방법을 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 11/20/2018
uid: client-side/bundling-and-minification
ms.openlocfilehash: 5d5f0aadb7740c9b2b959d12a585cd8c91758ce8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031850"
---
# <a name="bundle-and-minify-static-assets-in-aspnet-core"></a><span data-ttu-id="af223-103">ASP.NET Core에서 정적 자산 번들링 및 축소하기</span><span class="sxs-lookup"><span data-stu-id="af223-103">Bundle and minify static assets in ASP.NET Core</span></span>

<span data-ttu-id="af223-104">작성자: [Scott Addie](https://twitter.com/Scott_Addie) 및 [David Pine](https://twitter.com/davidpine7)</span><span class="sxs-lookup"><span data-stu-id="af223-104">By [Scott Addie](https://twitter.com/Scott_Addie) and [David Pine](https://twitter.com/davidpine7)</span></span>

<span data-ttu-id="af223-105">이 문서에서는 ASP.NET Core 웹 응용 프로그램에서 번들링 및 축소를 사용하는 방법을 비롯해서 이러한 기능을 적용하여 얻을 수 있는 이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-105">This article explains the benefits of applying bundling and minification, including how these features can be used with ASP.NET Core web apps.</span></span>

## <a name="what-is-bundling-and-minification"></a><span data-ttu-id="af223-106">번들링 및 축소란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="af223-106">What is bundling and minification</span></span>

<span data-ttu-id="af223-107">번들링 및 축소는 웹 앱에 적용할 수 있는 두 가지 고유한 성능 최적화입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-107">Bundling and minification are two distinct performance optimizations you can apply in a web app.</span></span> <span data-ttu-id="af223-108">번들링 및 축소를 함께 사용하면 서버 요청 수를 줄이고 요청된 정적 자산의 크기를 줄여서 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-108">Used together, bundling and minification improve performance by reducing the number of server requests and reducing the size of the requested static assets.</span></span>

<span data-ttu-id="af223-109">번들링 및 축소는 주로 첫 번째 페이지의 요청 로드 시간을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-109">Bundling and minification primarily improve the first page request load time.</span></span> <span data-ttu-id="af223-110">브라우저는 웹 페이지가 요청되면 정적 자산(JavaScript, CSS 및 이미지)을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-110">Once a web page has been requested, the browser caches the static assets (JavaScript, CSS, and images).</span></span> <span data-ttu-id="af223-111">따라서 동일한 자산을 요구하는 동일한 사이트에서 동일한 페이지(들)을 요청하는 경우에는 번들링 및 축소로 성능을 개선하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-111">Consequently, bundling and minification don't improve performance when requesting the same page, or pages, on the same site requesting the same assets.</span></span> <span data-ttu-id="af223-112">자산에 대한 만료 헤더가 올바르게 설정되지 않고 번들링 및 축소를 사용하지 않는 경우에는 브라우저의 새로 고침 추론이 며칠 지난 후에 자산이 오래된 것으로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-112">If the expires header isn't set correctly on the assets and if bundling and minification isn't used, the browser's freshness heuristics mark the assets stale after a few days.</span></span> <span data-ttu-id="af223-113">게다가 브라우저는 각 자산에 대한 유효성 검사 요청을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-113">Additionally, the browser requires a validation request for each asset.</span></span> <span data-ttu-id="af223-114">이 경우 번들링 및 축소는 첫 번째 페이지 요청 이후라도 성능 개선을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-114">In this case, bundling and minification provide a performance improvement even after the first page request.</span></span>

### <a name="bundling"></a><span data-ttu-id="af223-115">번들링</span><span class="sxs-lookup"><span data-stu-id="af223-115">Bundling</span></span>

<span data-ttu-id="af223-116">번들링은 여러 개의 파일을 단일 파일로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-116">Bundling combines multiple files into a single file.</span></span> <span data-ttu-id="af223-117">번들링은 웹 페이지 같은 웹 자산을 렌더링하는데 필요한 서버 요청의 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-117">Bundling reduces the number of server requests that are necessary to render a web asset, such as a web page.</span></span> <span data-ttu-id="af223-118">CSS, JavaScript 등에 대한 여러 개의 개별 번들을 만들 수 있습니다. 파일 수가 적다는 말은 브라우저에서 서버로 보내는 HTTP 요청 수 또는 응용 프로그램을 제공하는 서비스의 HTTP 요청 수가 줄어든다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-118">You can create any number of individual bundles specifically for CSS, JavaScript, etc. Fewer files means fewer HTTP requests from the browser to the server or from the service providing your application.</span></span> <span data-ttu-id="af223-119">따라서 첫 번째 페이지 로드 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="af223-119">This results in improved first page load performance.</span></span>

### <a name="minification"></a><span data-ttu-id="af223-120">축소</span><span class="sxs-lookup"><span data-stu-id="af223-120">Minification</span></span>

<span data-ttu-id="af223-121">축소는 기능 변경 없이 코드에서 불필요한 문자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-121">Minification removes unnecessary characters from code without altering functionality.</span></span> <span data-ttu-id="af223-122">결과적으로 요청된 자산(CSS, 이미지 및 JavaScript 파일 같은)의 크기가 크게 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-122">The result is a significant size reduction in requested assets (such as CSS, images, and JavaScript files).</span></span> <span data-ttu-id="af223-123">일반적인 축소의 부수적인 작용은 변수 이름을 한 문자로 줄이고 주석과 불필요한 공백을 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-123">Common side effects of minification include shortening variable names to one character and removing comments and unnecessary whitespace.</span></span>

<span data-ttu-id="af223-124">다음 JavaScript 함수를 살펴보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="af223-124">Consider the following JavaScript function:</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.js)]

<span data-ttu-id="af223-125">축소는 이 함수를 다음과 같이 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-125">Minification reduces the function to the following:</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.min.js)]

<span data-ttu-id="af223-126">주석과 불필요한 공백을 제거하는 것 외에도 다음 매개 변수 및 변수 이름이 다음과 같이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-126">In addition to removing the comments and unnecessary whitespace, the following parameter and variable names were renamed as follows:</span></span>

<span data-ttu-id="af223-127">원래 이름</span><span class="sxs-lookup"><span data-stu-id="af223-127">Original</span></span> | <span data-ttu-id="af223-128">변경된 이름</span><span class="sxs-lookup"><span data-stu-id="af223-128">Renamed</span></span>
--- | :---:
`imageTagAndImageID` | `t`
`imageContext` | `a`
`imageElement` | `r`

## <a name="impact-of-bundling-and-minification"></a><span data-ttu-id="af223-129">번들링 및 축소의 영향</span><span class="sxs-lookup"><span data-stu-id="af223-129">Impact of bundling and minification</span></span>

<span data-ttu-id="af223-130">다음 표는 자산을 개별적으로 로드하는 경우와 번들링 및 축소를 사용하는 경우의 차이를 간략히 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="af223-130">The following table outlines differences between individually loading assets and using bundling and minification:</span></span>

<span data-ttu-id="af223-131">작업</span><span class="sxs-lookup"><span data-stu-id="af223-131">Action</span></span> | <span data-ttu-id="af223-132">B/M을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="af223-132">With B/M</span></span> | <span data-ttu-id="af223-133">B/M 없이</span><span class="sxs-lookup"><span data-stu-id="af223-133">Without B/M</span></span> | <span data-ttu-id="af223-134">변화</span><span class="sxs-lookup"><span data-stu-id="af223-134">Change</span></span>
--- | :---: | :---: | :---:
<span data-ttu-id="af223-135">파일 요청</span><span class="sxs-lookup"><span data-stu-id="af223-135">File Requests</span></span>  | <span data-ttu-id="af223-136">7</span><span class="sxs-lookup"><span data-stu-id="af223-136">7</span></span>   | <span data-ttu-id="af223-137">18</span><span class="sxs-lookup"><span data-stu-id="af223-137">18</span></span>     | <span data-ttu-id="af223-138">157%</span><span class="sxs-lookup"><span data-stu-id="af223-138">157%</span></span>
<span data-ttu-id="af223-139">전송(kb)</span><span class="sxs-lookup"><span data-stu-id="af223-139">KB Transferred</span></span> | <span data-ttu-id="af223-140">156</span><span class="sxs-lookup"><span data-stu-id="af223-140">156</span></span> | <span data-ttu-id="af223-141">264.68</span><span class="sxs-lookup"><span data-stu-id="af223-141">264.68</span></span> | <span data-ttu-id="af223-142">70%</span><span class="sxs-lookup"><span data-stu-id="af223-142">70%</span></span>
<span data-ttu-id="af223-143">로드 시간 (ms)</span><span class="sxs-lookup"><span data-stu-id="af223-143">Load Time (ms)</span></span> | <span data-ttu-id="af223-144">885</span><span class="sxs-lookup"><span data-stu-id="af223-144">885</span></span> | <span data-ttu-id="af223-145">2360</span><span class="sxs-lookup"><span data-stu-id="af223-145">2360</span></span>   | <span data-ttu-id="af223-146">167%</span><span class="sxs-lookup"><span data-stu-id="af223-146">167%</span></span>

<span data-ttu-id="af223-147">브라우저는 HTTP 요청 헤더에 관해 매우 장황합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-147">Browsers are fairly verbose with regard to HTTP request headers.</span></span> <span data-ttu-id="af223-148">번들링 시 전송되는 총 바이트가 상당히 감소하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-148">The total bytes sent metric saw a significant reduction when bundling.</span></span> <span data-ttu-id="af223-149">로드 시간이 크게 개선되었지만 이 예제는 로컬에서 실행된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-149">The load time shows a significant improvement, however this example ran locally.</span></span> <span data-ttu-id="af223-150">네트워크를 통해서 전송되는 자산에 대해 번들링 및 축소를 사용하면 큰 성능 향상을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-150">Greater performance gains are realized when using bundling and minification with assets transferred over a network.</span></span>

## <a name="choose-a-bundling-and-minification-strategy"></a><span data-ttu-id="af223-151">번들링 및 축소 전략 선택하기</span><span class="sxs-lookup"><span data-stu-id="af223-151">Choose a bundling and minification strategy</span></span>

<span data-ttu-id="af223-152">MVC 및 Razor 페이지 프로젝트 템플릿을 묶음 및 축소 JSON 구성 파일의 구성에 대 한 기본 제공 솔루션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-152">The MVC and Razor Pages project templates provide an out-of-the-box solution for bundling and minification consisting of a JSON configuration file.</span></span> <span data-ttu-id="af223-153">와 같은 타사 도구를 [Gulp](xref:client-side/using-gulp) 하 고 [Grunt](xref:client-side/using-grunt) 실행 기 작업을 좀 더 많은 복잡성을 사용 하 여 동일한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-153">Third-party tools, such as the [Gulp](xref:client-side/using-gulp) and [Grunt](xref:client-side/using-grunt) task runners, accomplish the same tasks with a bit more complexity.</span></span> <span data-ttu-id="af223-154">개발 워크플로에서 처리 묶음 및 축소 초과 해야 하는 경우 타사 도구는 최적의 선택&mdash;lint 및 이미지 최적화와 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-154">A third-party tool is a great fit when your development workflow requires processing beyond bundling and minification&mdash;such as linting and image optimization.</span></span> <span data-ttu-id="af223-155">디자인 타임 묶음 및 축소를 사용 하 여 앱의 배포 하기 전에 축소 된 파일이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af223-155">By using design-time bundling and minification, the minified files are created prior to the app's deployment.</span></span> <span data-ttu-id="af223-156">묶음 및 축소를 배포 하기 전에 서버 부하 감소의 이점이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-156">Bundling and minifying before deployment provides the advantage of reduced server load.</span></span> <span data-ttu-id="af223-157">그러나 해당 디자인 타임 묶음을 인식 해야 하 고 축소 빌드 복잡성 증가 정적 파일 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-157">However, it's important to recognize that design-time bundling and minification increases build complexity and only works with static files.</span></span>

## <a name="configure-bundling-and-minification"></a><span data-ttu-id="af223-158">번들링 및 축소 구성하기</span><span class="sxs-lookup"><span data-stu-id="af223-158">Configure bundling and minification</span></span>

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="af223-159">ASP.NET Core 2.0 이전에서는 MVC 및 Razor 페이지 프로젝트 템플릿에서 각 번들에 대한 옵션을 정의하는 *bundleconfig.json* 구성 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-159">In ASP.NET Core 2.0 or earlier, the MVC and Razor Pages project templates provide a *bundleconfig.json* configuration file that defines the options for each bundle:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="af223-160">ASP.NET Core 2.1 이상에서는 MVC 또는 Razor 페이지 프로젝트 루트에 *bundleconfig.json*이라는 새로운 JSON 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-160">In ASP.NET Core 2.1 or later, add a new JSON file, named *bundleconfig.json*, to the MVC or Razor Pages project root.</span></span> <span data-ttu-id="af223-161">다음 JSON을 이 파일의 시작점으로 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="af223-161">Include the following JSON in that file as a starting point:</span></span>

::: moniker-end

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig.json)]

<span data-ttu-id="af223-162">*bundleconfig.json* 파일은 각 번들에 대한 옵션을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-162">The *bundleconfig.json* file defines the options for each bundle.</span></span> <span data-ttu-id="af223-163">위의 예제에서는 사용자 지정 JavaScript(*wwwroot/js/site.js*) 및 스타일시트(*wwwroot/css/site.css*) 파일들에 대해 단일 번들 구성이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="af223-163">In the preceding example, a single bundle configuration is defined for the custom JavaScript (*wwwroot/js/site.js*) and stylesheet (*wwwroot/css/site.css*) files.</span></span>

<span data-ttu-id="af223-164">구성 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-164">Configuration options include:</span></span>

* <span data-ttu-id="af223-165">`outputFileName`: 출력 번들 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-165">`outputFileName`: The name of the bundle file to output.</span></span> <span data-ttu-id="af223-166">*bundleconfig.json* 파일로부터의 상대 경로를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-166">Can contain a relative path from the *bundleconfig.json* file.</span></span> <span data-ttu-id="af223-167">**필수**</span><span class="sxs-lookup"><span data-stu-id="af223-167">**required**</span></span>
* <span data-ttu-id="af223-168">`inputFiles`: 배열 함께 번들로 제공할 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-168">`inputFiles`: An array of files to bundle together.</span></span> <span data-ttu-id="af223-169">이 배열의 값은 구성 파일에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-169">These are relative paths to the configuration file.</span></span> <span data-ttu-id="af223-170">**선택적**, \*값이 비어 있으면 빈 출력 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="af223-170">**optional**, \*an empty value results in an empty output file.</span></span> <span data-ttu-id="af223-171">[와일드카드 사용](http://www.tldp.org/LDP/abs/html/globbingref.html) 패턴이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="af223-171">[globbing](http://www.tldp.org/LDP/abs/html/globbingref.html) patterns are supported.</span></span>
* <span data-ttu-id="af223-172">`minify`: 출력 형식에 대 한 축소 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-172">`minify`: The minification options for the output type.</span></span> <span data-ttu-id="af223-173">**선택적**, *기본값 - `minify: { enabled: true }`*</span><span class="sxs-lookup"><span data-stu-id="af223-173">**optional**, *default - `minify: { enabled: true }`*</span></span>
  * <span data-ttu-id="af223-174">이 구성 옵션은 출력 파일 형식마다 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="af223-174">Configuration options are available per output file type.</span></span>
    * [<span data-ttu-id="af223-175">CSS Minifier</span><span class="sxs-lookup"><span data-stu-id="af223-175">CSS Minifier</span></span>](https://github.com/madskristensen/BundlerMinifier/wiki/cssminifier)
    * [<span data-ttu-id="af223-176">JavaScript Minifier</span><span class="sxs-lookup"><span data-stu-id="af223-176">JavaScript Minifier</span></span>](https://github.com/madskristensen/BundlerMinifier/wiki/JavaScript-Minifier-settings)
    * [<span data-ttu-id="af223-177">HTML Minifier</span><span class="sxs-lookup"><span data-stu-id="af223-177">HTML Minifier</span></span>](https://github.com/madskristensen/BundlerMinifier/wiki)
* <span data-ttu-id="af223-178">`includeInProject`: 프로젝트 파일에 생성 된 파일을 추가할지 여부를 나타내는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-178">`includeInProject`: Flag indicating whether to add generated files to project file.</span></span> <span data-ttu-id="af223-179">**선택적**, *기본값 - false*</span><span class="sxs-lookup"><span data-stu-id="af223-179">**optional**, *default - false*</span></span>
* <span data-ttu-id="af223-180">`sourceMap`: 해당 번들된 파일에 대 한 소스 맵을 생성할지 여부를 나타내는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-180">`sourceMap`: Flag indicating whether to generate a source map for the bundled file.</span></span> <span data-ttu-id="af223-181">**선택적**, *기본값 - false*</span><span class="sxs-lookup"><span data-stu-id="af223-181">**optional**, *default - false*</span></span>
* <span data-ttu-id="af223-182">`sourceMapRootPath`: 생성 된 소스 맵 파일을 저장 하는 것에 대 한 루트 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="af223-182">`sourceMapRootPath`: The root path for storing the generated source map file.</span></span>

## <a name="build-time-execution-of-bundling-and-minification"></a><span data-ttu-id="af223-183">빌드 시 번들링 및 축소 실행하기</span><span class="sxs-lookup"><span data-stu-id="af223-183">Build-time execution of bundling and minification</span></span>

<span data-ttu-id="af223-184">[BuildBundlerMinifier](https://www.nuget.org/packages/BuildBundlerMinifier/) NuGet 패키지를 사용하면 빌드 시 번들링 및 축소를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-184">The [BuildBundlerMinifier](https://www.nuget.org/packages/BuildBundlerMinifier/) NuGet package enables the execution of bundling and minification at build time.</span></span> <span data-ttu-id="af223-185">이 패키지는 빌드 및 정리 시에 실행되는 [MSBuild 대상](/visualstudio/msbuild/msbuild-targets)을 주입합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-185">The package injects [MSBuild Targets](/visualstudio/msbuild/msbuild-targets) which run at build and clean time.</span></span> <span data-ttu-id="af223-186">빌드 프로세스는 *bundleconfig.json* 파일을 분석하여 정의된 구성을 기반으로 출력 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-186">The *bundleconfig.json* file is analyzed by the build process to produce the output files based on the defined configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="af223-187">BuildBundlerMinifier는 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-187">BuildBundlerMinifier belongs to a community-driven project on GitHub for which Microsoft provides no support.</span></span> <span data-ttu-id="af223-188">문제점은 [여기](https://github.com/madskristensen/BundlerMinifier/issues)에 제출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-188">Issues should be filed [here](https://github.com/madskristensen/BundlerMinifier/issues).</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="af223-189">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af223-189">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="af223-190">프로젝트에 *BuildBundlerMinifier* 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-190">Add the *BuildBundlerMinifier* package to your project.</span></span>

<span data-ttu-id="af223-191">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-191">Build the project.</span></span> <span data-ttu-id="af223-192">출력 창에 다음 내용이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af223-192">The following appears in the Output window:</span></span>

```console
1>------ Build started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>
1>Bundler: Begin processing bundleconfig.json
1>  Minified wwwroot/css/site.min.css
1>  Minified wwwroot/js/site.min.js
1>Bundler: Done processing bundleconfig.json
1>BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
```

<span data-ttu-id="af223-193">프로젝트를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-193">Clean the project.</span></span> <span data-ttu-id="af223-194">출력 창에 다음 내용이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af223-194">The following appears in the Output window:</span></span>

```console
1>------ Clean started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>
1>Bundler: Cleaning output from bundleconfig.json
1>Bundler: Done cleaning output file from bundleconfig.json
========== Clean: 1 succeeded, 0 failed, 0 skipped ==========
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="af223-195">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="af223-195">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="af223-196">프로젝트에 *BuildBundlerMinifier* 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-196">Add the *BuildBundlerMinifier* package to your project:</span></span>

```console
dotnet add package BuildBundlerMinifier
```

<span data-ttu-id="af223-197">ASP.NET을 사용 하는 경우 Core 1.x의 경우 새로 추가 된 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-197">If using ASP.NET Core 1.x, restore the newly added package:</span></span>

```console
dotnet restore
```

<span data-ttu-id="af223-198">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-198">Build the project:</span></span>

```console
dotnet build
```

<span data-ttu-id="af223-199">다음 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af223-199">The following appears:</span></span>

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


    Bundler: Begin processing bundleconfig.json
    Bundler: Done processing bundleconfig.json
    BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
```

<span data-ttu-id="af223-200">프로젝트를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-200">Clean the project:</span></span>

```console
dotnet clean
```

<span data-ttu-id="af223-201">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="af223-201">The following output appears:</span></span>

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


  Bundler: Cleaning output from bundleconfig.json
  Bundler: Done cleaning output file from bundleconfig.json
```

---

## <a name="ad-hoc-execution-of-bundling-and-minification"></a><span data-ttu-id="af223-202">번들링 및 축소의 애드혹 실행</span><span class="sxs-lookup"><span data-stu-id="af223-202">Ad hoc execution of bundling and minification</span></span>

<span data-ttu-id="af223-203">프로젝트를 빌드하지 않고도 필요할 때마다 번들링 및 축소 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-203">It's possible to run the bundling and minification tasks on an ad hoc basis, without building the project.</span></span> <span data-ttu-id="af223-204">[BundlerMinifier.Core](https://www.nuget.org/packages/BundlerMinifier.Core/) NuGet 패키지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-204">Add the [BundlerMinifier.Core](https://www.nuget.org/packages/BundlerMinifier.Core/) NuGet package to your project:</span></span>

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=10)]

> [!NOTE]
> <span data-ttu-id="af223-205">BundlerMinifier.Core는 Microsoft에서 지원을 제공하지 않는 GitHub의 커뮤니티 주도 프로젝트에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-205">BundlerMinifier.Core belongs to a community-driven project on GitHub for which Microsoft provides no support.</span></span> <span data-ttu-id="af223-206">문제점은 [여기](https://github.com/madskristensen/BundlerMinifier/issues)에 제출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-206">Issues should be filed [here](https://github.com/madskristensen/BundlerMinifier/issues).</span></span>

<span data-ttu-id="af223-207">이 패키지는 .NET Core CLI가 *dotnet-bundle* 도구를 포함하도록 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-207">This package extends the .NET Core CLI to include the *dotnet-bundle* tool.</span></span> <span data-ttu-id="af223-208">다음 명령을 패키지 관리자 콘솔(PMC) 창 또는 명령 셸에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-208">The following command can be executed in the Package Manager Console (PMC) window or in a command shell:</span></span>

```console
dotnet bundle
```

> [!IMPORTANT]
> <span data-ttu-id="af223-209">NuGet 패키지 관리자는 \*.csproj 파일에 `<PackageReference />` 노드로 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-209">NuGet Package Manager adds dependencies to the \*.csproj file as `<PackageReference />` nodes.</span></span> <span data-ttu-id="af223-210">`dotnet bundle` 명령은 `<DotNetCliToolReference />` 노드가 사용되는 경우에만 .NET Core CLI에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="af223-210">The `dotnet bundle` command is registered with the .NET Core CLI only when a `<DotNetCliToolReference />` node is used.</span></span> <span data-ttu-id="af223-211">그에 맞춰 \*.Csproj 파일을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-211">Modify the \*.csproj file accordingly.</span></span>

## <a name="add-files-to-workflow"></a><span data-ttu-id="af223-212">워크플로에 파일 추가하기</span><span class="sxs-lookup"><span data-stu-id="af223-212">Add files to workflow</span></span>

<span data-ttu-id="af223-213">다음과 비슷한 또 다른 *custom.css* 파일이 추가되는 예제를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="af223-213">Consider an example in which an additional *custom.css* file is added resembling the following:</span></span>

[!code-css[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/css/custom.css)]

<span data-ttu-id="af223-214">*custom.css*를 축소하고 이를 *site.css*와 함께 *site.min.css* 파일에 번들하려면 다음과 같이 상대 경로를 *bundleconfig.json*에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-214">To minify *custom.css* and bundle it with *site.css* into a *site.min.css* file, add the relative path to *bundleconfig.json*:</span></span>

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig2.json?highlight=6)]

> [!NOTE]
> <span data-ttu-id="af223-215">또는 다음과 같은 와일드 카드 사용 패턴을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-215">Alternatively, the following globbing pattern could be used:</span></span>
>
> ```json
> "inputFiles": ["wwwroot/**/*(*.css|!(*.min.css))"]
> ```
>
> <span data-ttu-id="af223-216">이 와일드 카드 사용 패턴은 축소된 파일 패턴을 제외한 모든 CSS 파일을 매칭합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-216">This globbing pattern matches all CSS files and excludes the minified file pattern.</span></span>

<span data-ttu-id="af223-217">애플리케이션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-217">Build the application.</span></span> <span data-ttu-id="af223-218">*site.min.css*를 열고 *custom.css*의 내용이 파일 끝에 추가되었음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-218">Open *site.min.css* and notice the content of *custom.css* is appended to the end of the file.</span></span>

## <a name="environment-based-bundling-and-minification"></a><span data-ttu-id="af223-219">환경 기반 번들링 및 축소</span><span class="sxs-lookup"><span data-stu-id="af223-219">Environment-based bundling and minification</span></span>

<span data-ttu-id="af223-220">프로덕션 환경에서는 번들링되고 축소된 앱의 파일을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-220">As a best practice, the bundled and minified files of your app should be used in a production environment.</span></span> <span data-ttu-id="af223-221">개발하는 중에는 원본 파일을 사용해야 앱을 손쉽게 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-221">During development, the original files make for easier debugging of the app.</span></span>

<span data-ttu-id="af223-222">뷰에서 [Environment 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)를 사용하여 페이지에 포함할 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-222">Specify which files to include in your pages by using the [Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) in your views.</span></span> <span data-ttu-id="af223-223">Environment 태그 도우미는 특정 [환경](xref:fundamentals/environments)에서 실행될 때만 자신의 내용을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-223">The Environment Tag Helper only renders its contents when running in specific [environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="af223-224">다음 `environment` 태그는 `Development` 환경에서 실행하는 경우에만 처리되지 않은 CSS 파일을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-224">The following `environment` tag renders the unprocessed CSS files when running in the `Development` environment:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=21-24)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=9-12)]

::: moniker-end

<span data-ttu-id="af223-225">다음 `environment` 태그는 `Development`가 아닌 환경에서 실행할 때 번들링되고 축소된 CSS 파일을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-225">The following `environment` tag renders the bundled and minified CSS files when running in an environment other than `Development`.</span></span> <span data-ttu-id="af223-226">예를 들어 `Production`이나 `Staging`에서 실행하면 다음 스타일시트의 렌더링이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="af223-226">For example, running in `Production` or `Staging` triggers the rendering of these stylesheets:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=5&range=25-30)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=13-18)]

::: moniker-end

## <a name="consume-bundleconfigjson-from-gulp"></a><span data-ttu-id="af223-227">Gulp에서 bundleconfig.json 사용하기</span><span class="sxs-lookup"><span data-stu-id="af223-227">Consume bundleconfig.json from Gulp</span></span>

<span data-ttu-id="af223-228">앱의 번들링 및 축소 워크플로에서 추가적인 처리를 필요로 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-228">There are cases in which an app's bundling and minification workflow requires additional processing.</span></span> <span data-ttu-id="af223-229">그 예로 이미지 최적화, 캐시 무효화 및 CDN 자산 처리를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-229">Examples include image optimization, cache busting, and CDN asset processing.</span></span> <span data-ttu-id="af223-230">이러한 요구 사항을 충족하려면 Gulp를 사용하도록 번들링 및 축소 워크플로를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-230">To satisfy these requirements, you can convert the bundling and minification workflow to use Gulp.</span></span>

### <a name="use-the-bundler--minifier-extension"></a><span data-ttu-id="af223-231">Bundler & Minifier 확장 사용</span><span class="sxs-lookup"><span data-stu-id="af223-231">Use the Bundler & Minifier extension</span></span>

<span data-ttu-id="af223-232">Visual Studio [Bundler & Minifier](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BundlerMinifier) 확장 처리 Gulp로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-232">The Visual Studio [Bundler & Minifier](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BundlerMinifier) extension handles the conversion to Gulp.</span></span>

> [!NOTE]
> <span data-ttu-id="af223-233">Bundler & Minifier 확장 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-233">The Bundler & Minifier extension belongs to a community-driven project on GitHub for which Microsoft provides no support.</span></span> <span data-ttu-id="af223-234">문제점은 [여기](https://github.com/madskristensen/BundlerMinifier/issues)에 제출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-234">Issues should be filed [here](https://github.com/madskristensen/BundlerMinifier/issues).</span></span>

<span data-ttu-id="af223-235">솔루션 탐색기에서 *bundleconfig.json* 파일을 마우스 오른쪽 버튼으로 클릭하고 **Bundler & Minifier**  >  **Convert To Gulp...** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-235">Right-click the *bundleconfig.json* file in Solution Explorer and select **Bundler & Minifier** > **Convert To Gulp...**:</span></span>

![Convert To Gulp 컨텍스트 메뉴](../client-side/bundling-and-minification/_static/convert-to-gulp.png)

<span data-ttu-id="af223-237">그러면 프로젝트에 *gulpfile.js* 및 *package.json* 파일이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="af223-237">The *gulpfile.js* and *package.json* files are added to the project.</span></span> <span data-ttu-id="af223-238">그리고 *package.json* 파일의 `devDependencies` 섹션에 나열된 지원 [npm](https://www.npmjs.com/) 패키지들이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="af223-238">The supporting [npm](https://www.npmjs.com/) packages listed in the *package.json* file's `devDependencies` section are installed.</span></span>

<span data-ttu-id="af223-239">PMC 창에서 다음 명령을 실행하여 Gulp CLI를 전역 종속성으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-239">Run the following command in the PMC window to install the Gulp CLI as a global dependency:</span></span>

```console
npm i -g gulp-cli
```

<span data-ttu-id="af223-240">입력, 출력 및 설정을 위해 *gulpfile.js* 파일에서 *bundleconfig.json* 파일을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-240">The *gulpfile.js* file reads the *bundleconfig.json* file for the inputs, outputs, and settings.</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-12&highlight=10)]

### <a name="convert-manually"></a><span data-ttu-id="af223-241">직접 변환하기</span><span class="sxs-lookup"><span data-stu-id="af223-241">Convert manually</span></span>

<span data-ttu-id="af223-242">Visual Studio나 Bundler & Minifier 확장을 사용할 수 없는 경우 직접 수작업으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-242">If Visual Studio and/or the Bundler & Minifier extension aren't available, convert manually.</span></span>

<span data-ttu-id="af223-243">프로젝트 루트에 다음 `devDependencies`가 지정된 *package.json* 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-243">Add a *package.json* file, with the following `devDependencies`, to the project root:</span></span>

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/package.json?range=5-13)]

<span data-ttu-id="af223-244">*package.json*과 동일한 수준에서 다음 명령을 실행하여 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-244">Install the dependencies by running the following command at the same level as *package.json*:</span></span>

```console
npm i
```

<span data-ttu-id="af223-245">전역 종속성으로 Gulp CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-245">Install the Gulp CLI as a global dependency:</span></span>

```console
npm i -g gulp-cli
```

<span data-ttu-id="af223-246">*gulpfile.js* 파일을 프로젝트 루트 아래에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-246">Copy the *gulpfile.js* file below to the project root:</span></span>

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-11,14-)]

### <a name="run-gulp-tasks"></a><span data-ttu-id="af223-247">Gulp 작업 실행하기</span><span class="sxs-lookup"><span data-stu-id="af223-247">Run Gulp tasks</span></span>

<span data-ttu-id="af223-248">Visual Studio에서 프로젝트를 빌드하기 전에 Gulp 축소 작업을 트리거하려면 \*.csproj 파일에 다음 [MSBuild 대상](/visualstudio/msbuild/msbuild-targets)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af223-248">To trigger the Gulp minification task before the project builds in Visual Studio, add the following [MSBuild Target](/visualstudio/msbuild/msbuild-targets) to the \*.csproj file:</span></span>

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=14-16)]

<span data-ttu-id="af223-249">이 예제에서 `MyPreCompileTarget` 대상 내에 정의된 모든 작업은 사전 정의된 `Build` 대상보다 먼저 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="af223-249">In this example, any tasks defined within the `MyPreCompileTarget` target run before the predefined `Build` target.</span></span> <span data-ttu-id="af223-250">Visual Studio의 출력 창에 다음과 비슷한 출력이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af223-250">Output similar to the following appears in Visual Studio's Output window:</span></span>

```console
1>------ Build started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
1>[14:17:49] Using gulpfile C:\BuildBundlerMinifierApp\gulpfile.js
1>[14:17:49] Starting 'min:js'...
1>[14:17:49] Starting 'min:css'...
1>[14:17:49] Starting 'min:html'...
1>[14:17:49] Finished 'min:js' after 83 ms
1>[14:17:49] Finished 'min:css' after 88 ms
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
```

<span data-ttu-id="af223-251">또는 Visual Studio의 작업 러너 탐색기를 사용하여 Gulp 작업을 특정 Visual Studio 이벤트에 바인딩 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af223-251">Alternatively, Visual Studio's Task Runner Explorer may be used to bind Gulp tasks to specific Visual Studio events.</span></span> <span data-ttu-id="af223-252">이에 대한 지침은 [기본 작업 실행하기](xref:client-side/using-gulp#running-default-tasks)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="af223-252">See [Running default tasks](xref:client-side/using-gulp#running-default-tasks) for instructions on doing that.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af223-253">추가 자료</span><span class="sxs-lookup"><span data-stu-id="af223-253">Additional resources</span></span>

* [<span data-ttu-id="af223-254">Gulp 사용하기</span><span class="sxs-lookup"><span data-stu-id="af223-254">Use Gulp</span></span>](xref:client-side/using-gulp)
* [<span data-ttu-id="af223-255">Grunt 사용하기</span><span class="sxs-lookup"><span data-stu-id="af223-255">Use Grunt</span></span>](xref:client-side/using-grunt)
* [<span data-ttu-id="af223-256">다양한 환경 사용하기</span><span class="sxs-lookup"><span data-stu-id="af223-256">Use multiple environments</span></span>](xref:fundamentals/environments)
* [<span data-ttu-id="af223-257">태그 도우미</span><span class="sxs-lookup"><span data-stu-id="af223-257">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
