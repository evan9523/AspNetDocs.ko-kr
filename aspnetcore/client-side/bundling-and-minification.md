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
# <a name="bundle-and-minify-static-assets-in-aspnet-core"></a>ASP.NET Core에서 정적 자산 번들링 및 축소하기

작성자: [Scott Addie](https://twitter.com/Scott_Addie) 및 [David Pine](https://twitter.com/davidpine7)

이 문서에서는 ASP.NET Core 웹 응용 프로그램에서 번들링 및 축소를 사용하는 방법을 비롯해서 이러한 기능을 적용하여 얻을 수 있는 이점을 설명합니다.

## <a name="what-is-bundling-and-minification"></a>번들링 및 축소란 무엇입니까?

번들링 및 축소는 웹 앱에 적용할 수 있는 두 가지 고유한 성능 최적화입니다. 번들링 및 축소를 함께 사용하면 서버 요청 수를 줄이고 요청된 정적 자산의 크기를 줄여서 성능을 향상시킬 수 있습니다.

번들링 및 축소는 주로 첫 번째 페이지의 요청 로드 시간을 개선합니다. 브라우저는 웹 페이지가 요청되면 정적 자산(JavaScript, CSS 및 이미지)을 캐시합니다. 따라서 동일한 자산을 요구하는 동일한 사이트에서 동일한 페이지(들)을 요청하는 경우에는 번들링 및 축소로 성능을 개선하지 못합니다. 자산에 대한 만료 헤더가 올바르게 설정되지 않고 번들링 및 축소를 사용하지 않는 경우에는 브라우저의 새로 고침 추론이 며칠 지난 후에 자산이 오래된 것으로 간주합니다. 게다가 브라우저는 각 자산에 대한 유효성 검사 요청을 필요로 합니다. 이 경우 번들링 및 축소는 첫 번째 페이지 요청 이후라도 성능 개선을 제공합니다.

### <a name="bundling"></a>번들링

번들링은 여러 개의 파일을 단일 파일로 결합합니다. 번들링은 웹 페이지 같은 웹 자산을 렌더링하는데 필요한 서버 요청의 수를 줄입니다. CSS, JavaScript 등에 대한 여러 개의 개별 번들을 만들 수 있습니다. 파일 수가 적다는 말은 브라우저에서 서버로 보내는 HTTP 요청 수 또는 응용 프로그램을 제공하는 서비스의 HTTP 요청 수가 줄어든다는 뜻입니다. 따라서 첫 번째 페이지 로드 성능이 향상됩니다.

### <a name="minification"></a>축소

축소는 기능 변경 없이 코드에서 불필요한 문자를 제거합니다. 결과적으로 요청된 자산(CSS, 이미지 및 JavaScript 파일 같은)의 크기가 크게 감소합니다. 일반적인 축소의 부수적인 작용은 변수 이름을 한 문자로 줄이고 주석과 불필요한 공백을 제거하는 것입니다.

다음 JavaScript 함수를 살펴보시기 바랍니다.

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.js)]

축소는 이 함수를 다음과 같이 줄입니다.

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/js/site.min.js)]

주석과 불필요한 공백을 제거하는 것 외에도 다음 매개 변수 및 변수 이름이 다음과 같이 변경되었습니다.

원래 이름 | 변경된 이름
--- | :---:
`imageTagAndImageID` | `t`
`imageContext` | `a`
`imageElement` | `r`

## <a name="impact-of-bundling-and-minification"></a>번들링 및 축소의 영향

다음 표는 자산을 개별적으로 로드하는 경우와 번들링 및 축소를 사용하는 경우의 차이를 간략히 보여줍니다.

작업 | B/M을 사용 하 여 | B/M 없이 | 변화
--- | :---: | :---: | :---:
파일 요청  | 7   | 18     | 157%
전송(kb) | 156 | 264.68 | 70%
로드 시간 (ms) | 885 | 2360   | 167%

브라우저는 HTTP 요청 헤더에 관해 매우 장황합니다. 번들링 시 전송되는 총 바이트가 상당히 감소하는 것을 볼 수 있습니다. 로드 시간이 크게 개선되었지만 이 예제는 로컬에서 실행된 것입니다. 네트워크를 통해서 전송되는 자산에 대해 번들링 및 축소를 사용하면 큰 성능 향상을 얻을 수 있습니다.

## <a name="choose-a-bundling-and-minification-strategy"></a>번들링 및 축소 전략 선택하기

MVC 및 Razor 페이지 프로젝트 템플릿을 묶음 및 축소 JSON 구성 파일의 구성에 대 한 기본 제공 솔루션을 제공 합니다. 와 같은 타사 도구를 [Gulp](xref:client-side/using-gulp) 하 고 [Grunt](xref:client-side/using-grunt) 실행 기 작업을 좀 더 많은 복잡성을 사용 하 여 동일한 작업을 수행 합니다. 개발 워크플로에서 처리 묶음 및 축소 초과 해야 하는 경우 타사 도구는 최적의 선택&mdash;lint 및 이미지 최적화와 같은 합니다. 디자인 타임 묶음 및 축소를 사용 하 여 앱의 배포 하기 전에 축소 된 파일이 생성 됩니다. 묶음 및 축소를 배포 하기 전에 서버 부하 감소의 이점이 제공 합니다. 그러나 해당 디자인 타임 묶음을 인식 해야 하 고 축소 빌드 복잡성 증가 정적 파일 에서만 작동 합니다.

## <a name="configure-bundling-and-minification"></a>번들링 및 축소 구성하기

::: moniker range="<= aspnetcore-2.0"

ASP.NET Core 2.0 이전에서는 MVC 및 Razor 페이지 프로젝트 템플릿에서 각 번들에 대한 옵션을 정의하는 *bundleconfig.json* 구성 파일을 제공합니다.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

ASP.NET Core 2.1 이상에서는 MVC 또는 Razor 페이지 프로젝트 루트에 *bundleconfig.json*이라는 새로운 JSON 파일을 추가합니다. 다음 JSON을 이 파일의 시작점으로 포함시킵니다.

::: moniker-end

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig.json)]

*bundleconfig.json* 파일은 각 번들에 대한 옵션을 정의합니다. 위의 예제에서는 사용자 지정 JavaScript(*wwwroot/js/site.js*) 및 스타일시트(*wwwroot/css/site.css*) 파일들에 대해 단일 번들 구성이 정의됩니다.

구성 옵션은 다음과 같습니다.

* `outputFileName`: 출력 번들 파일의 이름입니다. *bundleconfig.json* 파일로부터의 상대 경로를 포함할 수 있습니다. **필수**
* `inputFiles`: 배열 함께 번들로 제공할 파일입니다. 이 배열의 값은 구성 파일에 대한 상대 경로입니다. **선택적**, *값이 비어 있으면 빈 출력 파일이 만들어집니다. [와일드카드 사용](http://www.tldp.org/LDP/abs/html/globbingref.html) 패턴이 지원됩니다.
* `minify`: 출력 형식에 대 한 축소 옵션입니다. **선택적**, *기본값 - `minify: { enabled: true }`*
  * 이 구성 옵션은 출력 파일 형식마다 달라집니다.
    * [CSS Minifier](https://github.com/madskristensen/BundlerMinifier/wiki/cssminifier)
    * [JavaScript Minifier](https://github.com/madskristensen/BundlerMinifier/wiki/JavaScript-Minifier-settings)
    * [HTML Minifier](https://github.com/madskristensen/BundlerMinifier/wiki)
* `includeInProject`: 프로젝트 파일에 생성 된 파일을 추가할지 여부를 나타내는 플래그입니다. **선택적**, *기본값 - false*
* `sourceMap`: 해당 번들된 파일에 대 한 소스 맵을 생성할지 여부를 나타내는 플래그입니다. **선택적**, *기본값 - false*
* `sourceMapRootPath`: 생성 된 소스 맵 파일을 저장 하는 것에 대 한 루트 경로입니다.

## <a name="build-time-execution-of-bundling-and-minification"></a>빌드 시 번들링 및 축소 실행하기

[BuildBundlerMinifier](https://www.nuget.org/packages/BuildBundlerMinifier/) NuGet 패키지를 사용하면 빌드 시 번들링 및 축소를 수행할 수 있습니다. 이 패키지는 빌드 및 정리 시에 실행되는 [MSBuild 대상](/visualstudio/msbuild/msbuild-targets)을 주입합니다. 빌드 프로세스는 *bundleconfig.json* 파일을 분석하여 정의된 구성을 기반으로 출력 파일을 생성합니다.

> [!NOTE]
> BuildBundlerMinifier는 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속합니다. 문제점은 [여기](https://github.com/madskristensen/BundlerMinifier/issues)에 제출해야 합니다.

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

프로젝트에 *BuildBundlerMinifier* 패키지를 추가합니다.

프로젝트를 빌드합니다. 출력 창에 다음 내용이 나타납니다.

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

프로젝트를 정리합니다. 출력 창에 다음 내용이 나타납니다.

```console
1>------ Clean started: Project: BuildBundlerMinifierApp, Configuration: Debug Any CPU ------
1>
1>Bundler: Cleaning output from bundleconfig.json
1>Bundler: Done cleaning output file from bundleconfig.json
========== Clean: 1 succeeded, 0 failed, 0 skipped ==========
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

프로젝트에 *BuildBundlerMinifier* 패키지를 추가합니다.

```console
dotnet add package BuildBundlerMinifier
```

ASP.NET을 사용 하는 경우 Core 1.x의 경우 새로 추가 된 패키지를 복원 합니다.

```console
dotnet restore
```

프로젝트를 빌드합니다.

```console
dotnet build
```

다음 메시지가 나타납니다.

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


    Bundler: Begin processing bundleconfig.json
    Bundler: Done processing bundleconfig.json
    BuildBundlerMinifierApp -> C:\BuildBundlerMinifierApp\bin\Debug\netcoreapp2.0\BuildBundlerMinifierApp.dll
```

프로젝트를 정리합니다.

```console
dotnet clean
```

다음 출력이 표시됩니다.

```console
Microsoft (R) Build Engine version 15.4.8.50001 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.


  Bundler: Cleaning output from bundleconfig.json
  Bundler: Done cleaning output file from bundleconfig.json
```

---

## <a name="ad-hoc-execution-of-bundling-and-minification"></a>번들링 및 축소의 애드혹 실행

프로젝트를 빌드하지 않고도 필요할 때마다 번들링 및 축소 작업을 실행할 수 있습니다. [BundlerMinifier.Core](https://www.nuget.org/packages/BundlerMinifier.Core/) NuGet 패키지를 프로젝트에 추가합니다.

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=10)]

> [!NOTE]
> BundlerMinifier.Core는 Microsoft에서 지원을 제공하지 않는 GitHub의 커뮤니티 주도 프로젝트에 속해 있습니다. 문제점은 [여기](https://github.com/madskristensen/BundlerMinifier/issues)에 제출해야 합니다.

이 패키지는 .NET Core CLI가 *dotnet-bundle* 도구를 포함하도록 확장합니다. 다음 명령을 패키지 관리자 콘솔(PMC) 창 또는 명령 셸에서 실행할 수 있습니다.

```console
dotnet bundle
```

> [!IMPORTANT]
> NuGet 패키지 관리자는 *.csproj 파일에 `<PackageReference />` 노드로 종속성을 추가합니다. `dotnet bundle` 명령은 `<DotNetCliToolReference />` 노드가 사용되는 경우에만 .NET Core CLI에 등록됩니다. 그에 맞춰 *.Csproj 파일을 수정해야 합니다.

## <a name="add-files-to-workflow"></a>워크플로에 파일 추가하기

다음과 비슷한 또 다른 *custom.css* 파일이 추가되는 예제를 가정해 봅니다.

[!code-css[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/wwwroot/css/custom.css)]

*custom.css*를 축소하고 이를 *site.css*와 함께 *site.min.css* 파일에 번들하려면 다음과 같이 상대 경로를 *bundleconfig.json*에 추가합니다.

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/bundleconfig2.json?highlight=6)]

> [!NOTE]
> 또는 다음과 같은 와일드 카드 사용 패턴을 사용할 수도 있습니다.
>
> ```json
> "inputFiles": ["wwwroot/**/*(*.css|!(*.min.css))"]
> ```
>
> 이 와일드 카드 사용 패턴은 축소된 파일 패턴을 제외한 모든 CSS 파일을 매칭합니다.

애플리케이션을 빌드합니다. *site.min.css*를 열고 *custom.css*의 내용이 파일 끝에 추가되었음을 확인합니다.

## <a name="environment-based-bundling-and-minification"></a>환경 기반 번들링 및 축소

프로덕션 환경에서는 번들링되고 축소된 앱의 파일을 사용하는 것이 가장 좋습니다. 개발하는 중에는 원본 파일을 사용해야 앱을 손쉽게 디버깅할 수 있습니다.

뷰에서 [Environment 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)를 사용하여 페이지에 포함할 파일을 지정합니다. Environment 태그 도우미는 특정 [환경](xref:fundamentals/environments)에서 실행될 때만 자신의 내용을 렌더링합니다.

다음 `environment` 태그는 `Development` 환경에서 실행하는 경우에만 처리되지 않은 CSS 파일을 렌더링합니다.

::: moniker range=">= aspnetcore-2.0"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=21-24)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=9-12)]

::: moniker-end

다음 `environment` 태그는 `Development`가 아닌 환경에서 실행할 때 번들링되고 축소된 CSS 파일을 렌더링합니다. 예를 들어 `Production`이나 `Staging`에서 실행하면 다음 스타일시트의 렌더링이 트리거됩니다.

::: moniker range=">= aspnetcore-2.0"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=5&range=25-30)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-cshtml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/Pages/_Layout.cshtml?highlight=3&range=13-18)]

::: moniker-end

## <a name="consume-bundleconfigjson-from-gulp"></a>Gulp에서 bundleconfig.json 사용하기

앱의 번들링 및 축소 워크플로에서 추가적인 처리를 필요로 하는 경우가 있습니다. 그 예로 이미지 최적화, 캐시 무효화 및 CDN 자산 처리를 들 수 있습니다. 이러한 요구 사항을 충족하려면 Gulp를 사용하도록 번들링 및 축소 워크플로를 변환할 수 있습니다.

### <a name="use-the-bundler--minifier-extension"></a>Bundler & Minifier 확장 사용

Visual Studio [Bundler & Minifier](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BundlerMinifier) 확장 처리 Gulp로 변환 합니다.

> [!NOTE]
> Bundler & Minifier 확장 Microsoft 지원 되지 않습니다 제공 하는 GitHub의 커뮤니티 기반 프로젝트에 속합니다. 문제점은 [여기](https://github.com/madskristensen/BundlerMinifier/issues)에 제출해야 합니다.

솔루션 탐색기에서 *bundleconfig.json* 파일을 마우스 오른쪽 버튼으로 클릭하고 **Bundler & Minifier**  >  **Convert To Gulp...** 를 선택합니다.

![Convert To Gulp 컨텍스트 메뉴](../client-side/bundling-and-minification/_static/convert-to-gulp.png)

그러면 프로젝트에 *gulpfile.js* 및 *package.json* 파일이 추가됩니다. 그리고 *package.json* 파일의 `devDependencies` 섹션에 나열된 지원 [npm](https://www.npmjs.com/) 패키지들이 설치됩니다.

PMC 창에서 다음 명령을 실행하여 Gulp CLI를 전역 종속성으로 설치합니다.

```console
npm i -g gulp-cli
```

입력, 출력 및 설정을 위해 *gulpfile.js* 파일에서 *bundleconfig.json* 파일을 읽습니다.

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-12&highlight=10)]

### <a name="convert-manually"></a>직접 변환하기

Visual Studio나 Bundler & Minifier 확장을 사용할 수 없는 경우 직접 수작업으로 변환합니다.

프로젝트 루트에 다음 `devDependencies`가 지정된 *package.json* 파일을 추가합니다.

[!code-json[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/package.json?range=5-13)]

*package.json*과 동일한 수준에서 다음 명령을 실행하여 종속성을 설치합니다.

```console
npm i
```

전역 종속성으로 Gulp CLI를 설치 합니다.

```console
npm i -g gulp-cli
```

*gulpfile.js* 파일을 프로젝트 루트 아래에 복사합니다.

[!code-javascript[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/gulpfile.js?range=1-11,14-)]

### <a name="run-gulp-tasks"></a>Gulp 작업 실행하기

Visual Studio에서 프로젝트를 빌드하기 전에 Gulp 축소 작업을 트리거하려면 *.csproj 파일에 다음 [MSBuild 대상](/visualstudio/msbuild/msbuild-targets)을 추가합니다.

[!code-xml[](../client-side/bundling-and-minification/samples/BuildBundlerMinifierApp/BuildBundlerMinifierApp.csproj?range=14-16)]

이 예제에서 `MyPreCompileTarget` 대상 내에 정의된 모든 작업은 사전 정의된 `Build` 대상보다 먼저 실행됩니다. Visual Studio의 출력 창에 다음과 비슷한 출력이 나타납니다.

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

또는 Visual Studio의 작업 러너 탐색기를 사용하여 Gulp 작업을 특정 Visual Studio 이벤트에 바인딩 할 수 있습니다. 이에 대한 지침은 [기본 작업 실행하기](xref:client-side/using-gulp#running-default-tasks)를 참고하시기 바랍니다.

## <a name="additional-resources"></a>추가 자료

* [Gulp 사용하기](xref:client-side/using-gulp)
* [Grunt 사용하기](xref:client-side/using-grunt)
* [다양한 환경 사용하기](xref:fundamentals/environments)
* [태그 도우미](xref:mvc/views/tag-helpers/intro)
