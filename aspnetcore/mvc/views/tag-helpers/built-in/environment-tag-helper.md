---
title: ASP.NET Core의 Environment 태그 도우미
author: pkellner
description: 모든 속성을 포함하여 정의된 ASP.NET Core Environment 태그 도우미
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/environment-tag-helper
ms.openlocfilehash: 379f58ed37329f047d53adf1dcfdfd2ad6a6ca4e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028630"
---
# <a name="environment-tag-helper-in-aspnet-core"></a><span data-ttu-id="66bd8-103">ASP.NET Core의 Environment 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="66bd8-103">Environment Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="66bd8-104">작성자: [Peter Kellner](http://peterkellner.net), [Hisham Bin Ateya](https://twitter.com/hishambinateya) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="66bd8-104">By [Peter Kellner](http://peterkellner.net), [Hisham Bin Ateya](https://twitter.com/hishambinateya), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="66bd8-105">Environment 태그 도우미는 현재 [호스팅 환경](xref:fundamentals/environments)에 기반하여 포함된 콘텐츠를 조건부로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-105">The Environment Tag Helper conditionally renders its enclosed content based on the current [hosting environment](xref:fundamentals/environments).</span></span> <span data-ttu-id="66bd8-106">환경 태그 도우미의 단일 특성 `names`는 쉼표로 구분된 환경 이름 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-106">The Environment Tag Helper's single attribute, `names`, is a comma-separated list of environment names.</span></span> <span data-ttu-id="66bd8-107">제공된 환경 이름 중에 현재 환경과 일치하는 이름이 하나라도 있으면 포함된 콘텐츠가 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-107">If any of the provided environment names match the current environment, the enclosed content is rendered.</span></span>

<span data-ttu-id="66bd8-108">태그 도우미에 대한 개요는 <xref:mvc/views/tag-helpers/intro>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66bd8-108">For an overview of Tag Helpers, see <xref:mvc/views/tag-helpers/intro>.</span></span>

## <a name="environment-tag-helper-attributes"></a><span data-ttu-id="66bd8-109">Environment 태그 도우미의 특성</span><span class="sxs-lookup"><span data-stu-id="66bd8-109">Environment Tag Helper Attributes</span></span>

### <a name="names"></a><span data-ttu-id="66bd8-110">names</span><span class="sxs-lookup"><span data-stu-id="66bd8-110">names</span></span>

<span data-ttu-id="66bd8-111">`names`는 포함된 콘텐츠를 렌더링하도록 트리거하는 단일 호스팅 환경 이름 또는 쉼표로 구분된 호스팅 환경 이름의 목록을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-111">`names` accepts a single hosting environment name or a comma-separated list of hosting environment names that trigger the rendering of the enclosed content.</span></span>

<span data-ttu-id="66bd8-112">환경 값은 [IHostingEnvironment.EnvironmentName](xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName*)에서 반환한 현재 값과 비교됩니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-112">Environment values are compared to the current value returned by [IHostingEnvironment.EnvironmentName](xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName*).</span></span> <span data-ttu-id="66bd8-113">이 비교에서 대/소문자는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-113">The comparison ignores case.</span></span>

<span data-ttu-id="66bd8-114">다음 예에서는 환경 태그 도우미를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-114">The following example uses an Environment Tag Helper.</span></span> <span data-ttu-id="66bd8-115">호스팅 환경이 스테이징 또는 프로덕션일 경우 콘텐츠가 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-115">The content is rendered if the hosting environment is Staging or Production:</span></span>

```cshtml
<environment names="Staging,Production">
    <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

::: moniker range=">= aspnetcore-2.0"

## <a name="include-and-exclude-attributes"></a><span data-ttu-id="66bd8-116">include 및 exclude 특성</span><span class="sxs-lookup"><span data-stu-id="66bd8-116">include and exclude attributes</span></span>

<span data-ttu-id="66bd8-117">`include` & `exclude` 특성은 포함되거나 제외된 호스팅 환경 이름을 기반으로 포함된 콘텐츠의 렌더링 작업을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-117">`include` & `exclude` attributes control rendering the enclosed content based on the included or excluded hosting environment names.</span></span>

### <a name="include"></a><span data-ttu-id="66bd8-118">include</span><span class="sxs-lookup"><span data-stu-id="66bd8-118">include</span></span>

<span data-ttu-id="66bd8-119">`include` 속성은 `names` 특성과 유사한 동작을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-119">The `include` property exhibits similar behavior to the `names` attribute.</span></span> <span data-ttu-id="66bd8-120">`include` 특성 값에 나열된 환경은 앱의 호스팅 환경([IHostingEnvironment.EnvironmentName](xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName*))과 일치해야 `<environment>` 태그의 콘텐츠를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-120">An environment listed in the `include` attribute value must match the app's hosting environment ([IHostingEnvironment.EnvironmentName](xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName*)) to render the content of the `<environment>` tag.</span></span>

```cshtml
<environment include="Staging,Production">
    <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

### <a name="exclude"></a><span data-ttu-id="66bd8-121">Exclude</span><span class="sxs-lookup"><span data-stu-id="66bd8-121">exclude</span></span>

<span data-ttu-id="66bd8-122">`include` 특성과 달리, `<environment>` 태그의 콘텐츠는 호스팅 환경이 `exclude` 특성 값에 나열된 환경과 일치하지 않을 경우 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="66bd8-122">In contrast to the `include` attribute, the content of the `<environment>` tag is rendered when the hosting environment doesn't match an environment listed in the `exclude` attribute value.</span></span>

```cshtml
<environment exclude="Development">
    <strong>HostingEnvironment.EnvironmentName is not Development</strong>
</environment>
```

::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="66bd8-123">추가 자료</span><span class="sxs-lookup"><span data-stu-id="66bd8-123">Additional resources</span></span>

* <xref:fundamentals/environments>
