---
title: JavaScriptServices를 사용하여 ASP.NET Core에서 단일 페이지 응용 프로그램 만들기
author: scottaddie
description: JavaScriptServices를 사용하여 ASP.NET Core가 지원하는 단일 페이지 응용 프로그램(SPA)을 만드는 방식의 이점에 대해 알아봅니다.
ms.author: scaddie
ms.custom: H1Hack27Feb2017
ms.date: 08/02/2017
uid: client-side/spa-services
ms.openlocfilehash: ee772e67ef14608bcc6e3498ade00424ff6090e5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062080"
---
# <a name="use-javascriptservices-to-create-single-page-applications-in-aspnet-core"></a>JavaScriptServices를 사용하여 ASP.NET Core에서 단일 페이지 응용 프로그램 만들기

작성자: [Scott Addie](https://github.com/scottaddie) 및 [Fiyaz Hasan](http://fiyazhasan.me/)

단일 페이지 응용 프로그램(SPA)은 내재된 풍부한 사용자 경험으로 인해서 인기 있는 웹 응용 프로그램 형식입니다. [Angular](https://angular.io/) 및 [React](https://facebook.github.io/react/) 같은 클라이언트 측 SPA 프레임워크 또는 라이브러리를 ASP.NET Core 같은 서버 측 프레임워크와 통합하는 작업은 어려울 일일 수 있습니다. [JavaScriptServices](https://github.com/aspnet/JavaScriptServices)는 이런 통합 작업의 어려움을 줄이기 위해 개발되었습니다. 서로 다른 클라이언트 및 서버 기술 스택 간의 원활한 작업을 가능하게 해줍니다.

<a name="what-is-js-services"></a>

## <a name="what-is-javascriptservices"></a>JavaScriptServices란

JavaScriptServices는 ASP.NET Core를 위한 클라이언트 측 기술들의 모음입니다. 이 기술의 목표는 ASP.NET Core를 SPA 구축 시 개발자가 선호하는 서버 측 플랫폼으로 자리매김하는 것입니다.

JavaScriptServices는 개별적인 세 가지 NuGet 패키지로 이루어져 있습니다.

* [Microsoft.AspNetCore.NodeServices](https://www.nuget.org/packages/Microsoft.AspNetCore.NodeServices/) (NodeServices)
* [Microsoft.AspNetCore.SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) (SpaServices)
* [Microsoft.AspNetCore.SpaTemplates](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaTemplates/) (SpaTemplates)

이 패키지들은 다음과 같은 경우에 유용합니다.

* 서버에서 JavaScript를 실행하는 경우.
* SPA 프레임워크나 라이브러리를 사용하는 경우.
* Webpack을 사용하여 클라이언트 측 자산을 빌드하는 경우.

이 문서는 대부분의 초점을 SpaServices 패키지의 사용 방법에 두고 있습니다.

<a name="what-is-spa-services"></a>

## <a name="what-is-spaservices"></a>SpaServices란

SpaServices는 ASP.NET Core를 SPA 구축 시 개발자가 선호하는 서버 측 플랫폼으로 자리매김하기 위해서 개발되었습니다. ASP.NET Core로 SPA를 개발하기 위해서 SpaServices가 필수적인 것은 아니며 특정 클라이언트 프레임워크로 제한하지도 않습니다.

SpaServices는 다음과 같은 유용한 인프라를 제공합니다.

* [서버 측 사전 렌더링](#server-prerendering)
* [Webpack Dev 미들웨어](#webpack-dev-middleware)
* [실시간 모듈 교체](#hot-module-replacement)
* [라우팅 도우미](#routing-helpers)

종합적으로 이러한 인프라 구성 요소는 개발 워크플로와 런타임 환경 모두를 향상시킵니다. 이 구성 요소들은 개별적으로 사용할 수 있습니다.

<a name="spa-services-prereqs"></a>

## <a name="prerequisites-for-using-spaservices"></a>SpaServices 사용을 위한 전제 조건

SpaServices를 사용하려면 다음을 설치합니다.

* npm을 비롯한 [Node.js](https://nodejs.org/)(버전 6 이상)
  * 구성 요소가 설치되어 있으며 찾을 수 있는지 확인해보려면 명령줄에서 다음을 실행합니다.

    ```console
    node -v && npm -v
    ```

참고: Azure 웹 사이트에 배포 하는 경우 여기에서는 아무 작업도 수행할 필요가 없습니다 &mdash; Node.js 설치 되어 서버 환경에서 사용할 수 있습니다.

* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]

  * Windows에서 Visual Studio 2017을 사용하는 경우 **.NET Core 플랫폼 간 개발** 워크로드를 선택하여 SDK를 설치합니다.

* [Microsoft.AspNetCore.SpaServices](https://www.nuget.org/packages/Microsoft.AspNetCore.SpaServices/) NuGet 패키지

<a name="server-prerendering"></a>

## <a name="server-side-prerendering"></a>서버 측 사전 렌더링

유니버설(또는 동형) 응용 프로그램은 서버 및 클라이언트 양쪽 모두에서 실행할 수 있는 JavaScript 응용 프로그램입니다. Angular, React 및 기타 인기 있는 프레임워크는 이 응용 프로그램 개발 스타일을 위한 유니버설 플랫폼을 제공합니다. 그 개념은 우선 서버에서 Node.js를 통해서 프레임워크 구성 요소를 렌더링한 다음 이후의 실행은 클라이언트에 위임하는 것입니다.

SpaServices가 제공하는 ASP.NET Core [태그 도우미](xref:mvc/views/tag-helpers/intro)는 서버에서 JavaScript 함수를 호출하여 서버 측 사전 렌더링의 구현을 단순화합니다.

### <a name="prerequisites"></a>전제 조건

다음을 설치합니다.

* [aspnet-prerendering](https://www.npmjs.com/package/aspnet-prerendering) npm 패키지:

    ```console
    npm i -S aspnet-prerendering
    ```

### <a name="configuration"></a>구성하기

태그 도우미는 프로젝트의 *_ViewImports.cshtml* 파일에서 네임스페이스를 등록하여 검색 가능합니다.

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/_ViewImports.cshtml?highlight=3)]

태그 도우미는 Razor 뷰 내부에서 HTML과 유사한 구문을 활용하여 저수준 API와 직접 통신하는 복잡함을 추상화합니다.

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=5)]

### <a name="the-asp-prerender-module-tag-helper"></a>`asp-prerender-module` 태그 도우미

위의 코드 예제에 사용된 `asp-prerender-module` 태그 도우미는 서버에서 Node.js를 통해서 *ClientApp/dist/main-server.js*를 실행합니다. 명확히 말하자면 *main-server.js* 파일은 [Webpack](http://webpack.github.io/) 빌드 프로세스의 TypeScript-JavaScript 소스 간 변환 작업의 결과물입니다. Webpack은 `main-server`의 진입점 별칭과 *ClientApp/boot-server.ts* 파일에서 시작되는 이 별칭에 대한 종속성 그래프의 순회를 정의합니다.

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=53)]

다음 Angular 예제에서 *ClientApp/boot-server.ts* 파일은 `aspnet-prerendering` npm 패키지의 `createServerRenderer` 함수 및 `RenderResult` 형식을 사용하여 Node.js를 통한 서버 렌더링을 구성합니다. 서버 측 렌더링에 사용될 HTML 마크업은 강력한 형식의 JavaScript `Promise` 개체로 래핑된 resolve 함수 호출로 전달됩니다. 이 `Promise` 개체가 중요한 이유는 DOM의 자리 표시자 요소에 삽입하기 위해 비동기적으로 HTML의 마크업을 페이지에 제공하기 때문입니다.

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-34,79-)]

### <a name="the-asp-prerender-data-tag-helper"></a>`asp-prerender-data` 태그 도우미

`asp-prerender-module` 태그 도우미와 함께 `asp-prerender-data` 태그 도우미를 사용하면 Razor 뷰에서 서버 측 JavaScript로 컨텍스트 정보를 전달할 수 있습니다. 예를 들어 다음 태그는 사용자 데이터를 `main-server` 모듈로 전달합니다.

[!code-cshtml[](../client-side/spa-services/sample/SpaServicesSampleApp/Views/Home/Index.cshtml?range=9-12)]

지정한 `UserName` 인수는 기본 제공 JSON 직렬 변환기를 이용하여 직렬화되고 `params.data` 개체에 저장됩니다. 다음의 Angular 예제는 이 데이터를 사용하여 `h1` 요소 내에 개인화된 인사말을 생성합니다.

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,38-52,79-)]

참고: 태그 도우미에 전달 된 속성 이름으로 표시 됩니다 **PascalCase** 표기법입니다. 이와는 달리 JavaScript에서는 동일한 속성 이름이 **camelCase**로 표현됩니다. 이 차이는 기본 JSON 직렬화 구성으로 인한 것입니다.

위의 코드 예제를 확장하기 위해 `resolve` 함수에 제공되는 `globals` 속성을 추가하여 데이터를 서버에서 뷰로 전달할 수 있습니다.

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/boot-server.ts?range=6,10-21,57-77,79-)]

`globals` 개체 내에 정의된 `postList` 배열은 브라우저의 전역 `window` 개체에 연결됩니다. 이렇게 전역 범위로 변수를 끌어올리면 특히 동일한 데이터를 서버에서 한 번 그리고 클라이언트에서 다시 한 번 로딩하는 작업과 관련된 반복적인 노력을 줄일 수 있습니다.

![window 개체에 연결된 전역 postList 변수](spa-services/_static/global_variable.png)

<a name="webpack-dev-middleware"></a>

## <a name="webpack-dev-middleware"></a>Webpack Dev 미들웨어

[Webpack Dev 미들웨어](https://webpack.github.io/docs/webpack-dev-middleware.html)는 필요할 때마다 Webpack이 리소스를 빌드하는 간결한 개발 워크플로를 도입합니다. 이 미들웨어는 페이지가 브라우저에서 다시 로드될 때 클라이언트 측 리소스를 자동으로 컴파일하고 제공합니다. 다른 대안은 타사의 종속성이나 사용자 지정 코드가 변경될 때 프로젝트의 npm 빌드 스크립트를 사용해서 직접 Webpack을 호출하는 것입니다. 다음 예제는 *package.json* 파일의 npm 빌드 스크립트를 보여줍니다.

```json
"build": "npm run build:vendor && npm run build:custom",
```

### <a name="prerequisites"></a>전제 조건

다음을 설치합니다.

* [aspnet-webpack](https://www.npmjs.com/package/aspnet-webpack) npm 패키지:

    ```console
    npm i -D aspnet-webpack
    ```

### <a name="configuration"></a>구성하기

Webpack Dev 미들웨어는 *Startup.cs* 파일의 `Configure` 메서드에서 다음 코드를 통해서 HTTP 요청 파이프라인에 등록됩니다.

[!code-csharp[](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=snippet_WebpackMiddlewareRegistration&highlight=4)]

`UseWebpackDevMiddleware` 확장 메서드는 `UseStaticFiles` 확장 메서드를 통해서 [정적 파일 호스팅을 등록](xref:fundamentals/static-files)하기 전에 미리 호출해야 합니다. 보안 상의 이유로 앱이 개발 모드에서 실행될 때만 이 미들웨어를 등록해야 합니다.

*webpack.config.js* 파일의 `output.publicPath` 속성은 미들웨어에게 `dist` 폴더의 변경 사항을 모니터링하도록 지정합니다.

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,13-16)]

<a name="hot-module-replacement"></a>

## <a name="hot-module-replacement"></a>실시간 모듈 교체

Webpack의 [실시간 모듈 교체(HMR)](https://webpack.js.org/concepts/hot-module-replacement/) 기능은 [Webpack Dev 미들웨어](#webpack-dev-middleware)가 진화한 것으로 생각하면 됩니다. HMR은 모든 동일한 이점을 제공할 뿐만 아니라 변경 사항을 컴파일 한 뒤 페이지의 내용을 자동으로 갱신하여 개발 워크플로우를 더욱 간소화합니다. SPA의 현재 메모리 내 상태와 디버깅 세션을 방해하지 않도록 이 기능과 브라우저 새로 고침을 혼동하지 마십시오. Webpack Dev 미들웨어 서비스와 브라우저 간에는 실시간 링크가 존재하며, 이 얘기는 변경 사항이 브라우저로 푸시된다는 뜻입니다.

### <a name="prerequisites"></a>전제 조건

다음을 설치합니다.

* [webpack-hot-middleware](https://www.npmjs.com/package/webpack-hot-middleware) npm 패키지:

    ```console
    npm i -D webpack-hot-middleware
    ```

### <a name="configuration"></a>구성하기

`Configure` 메서드에서 MVC의 HTTP 요청 파이프라인에 HMR 구성 요소를 등록해야 합니다.

```csharp
app.UseWebpackDevMiddleware(new WebpackDevMiddlewareOptions {
    HotModuleReplacement = true
});
```

[Webpack Dev 미들웨어](#webpack-dev-middleware)의 경우와 마찬가지로`UseStaticFiles` 확장 메서드를 호출 하기 전에 `UseWebpackDevMiddleware` 확장 메서드를 먼저 호출해야 합니다. 보안 상의 이유로 앱이 개발 모드에서 실행될 때만 이 미들웨어를 등록해야 합니다.

*webpack.config.js* 파일에서는 `plugins` 배열이 비어 있더라도 이를 정의해야 합니다.

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/webpack.config.js?range=6,25)]

브라우저에서 앱을 로딩한 다음, 개발자 도구의 콘솔 탭에서 HMR의 활성화를 확인할 수 있습니다.

![실시간 모듈 교체 연결 메시지](spa-services/_static/hmr_connected.png)

<a name="routing-helpers"></a>

## <a name="routing-helpers"></a>라우팅 도우미

대부분의 ASP.NET Core 기반 SPA에서는 서버 측 라우팅뿐만 아니라 클라이언트 측 라우팅이 필요합니다. SPA 및 MVC 라우팅 시스템은 서로 간섭 없이 독립적으로 동작할 수 있습니다. 그러나 404 HTTP 응답 식별이라는 한 가지 까다로운 문제가 존재합니다.

확장자가 존재하지 않는 `/some/page`라는 경로가 사용되는 시나리오를 생각해보겠습니다. 요청이 서버 측 경로와는 패턴이 일치하지 않지만 클라이언트 측 경로와는 패턴이 일치한다고 가정합니다. 이제 일반적으로 서버에서 이미지 파일을 찾는 것으로 예상되는 `/images/user-512.png`에 대한 들어오는 요청을 생각해보겠습니다. 요청한 리소스 경로가 모든 서버 측 경로 또는 정적 파일과 일치하지 않으면 클라이언트 측 응용 프로그램이 처리하지 않을 가능성이 있으며, 일반적으로는 404 HTTP 상태 코드를 반환해야 합니다.

### <a name="prerequisites"></a>전제 조건

다음을 설치합니다.

* 클라이언트 측 라우팅 npm 패키지. 예를 들어 Angular를 사용하는 경우입니다.

    ```console
    npm i -S @angular/router
    ```

### <a name="configuration"></a>구성하기

`Configure` 메서드에서 `MapSpaFallbackRoute`라는 확장 메서드를 사용합니다.

[!code-csharp[](../client-side/spa-services/sample/SpaServicesSampleApp/Startup.cs?name=snippet_MvcRoutingTable&highlight=7-9)]

팁: 경로 구성 하는 순서 대로 평가 됩니다. 따라서 앞의 코드 예제에서는 `default` 경로가 가장 먼저 패턴 일치에 사용됩니다.

<a name="new-project-creation"></a>

## <a name="creating-a-new-project"></a>새 프로젝트 만들기

JavaScriptServices는 미리 구성된 응용 프로그램 템플릿을 제공합니다. SpaServices는 Angular, React, 및 Redux 같은 다양한 프레임워크 및 라이브러리와 함께 템플릿에서 사용됩니다.

이러한 템플릿들은 다음 명령을 실행하여 .NET Core CLI를 통해서 설치할 수 있습니다.

```console
dotnet new --install Microsoft.AspNetCore.SpaTemplates::*
```

사용 가능한 SPA 템플릿 목록은 다음과 같습니다.

| 템플릿                                 | 약식 이름 | 언어 | 태그        |
|:------------------------------------------|:-----------|:---------|:------------|
| MVC ASP.NET Core with Angular             | angular    | [C#]     | Web/MVC/SPA |
| MVC ASP.NET Core with React.js             | react      | [C#]     | Web/MVC/SPA |
| MVC ASP.NET Core with React.js and Redux  | reactredux | [C#]     | Web/MVC/SPA |

SPA 템플릿 중 하나를 사용하여 새로운 프로젝트를 만들려면 [dotnet new](/dotnet/core/tools/dotnet-new) 명령 뒤에 템플릿의 **약식 이름**을 추가합니다. 다음 명령은 서버 측에 ASP.NET Core MVC가 구성된 Angular 응용 프로그램을 생성합니다.

```console
dotnet new angular
```

<a name="runtime-config-mode"></a>

### <a name="set-the-runtime-configuration-mode"></a>런타임 구성 모드 설정

다음과 같은 두 가지 기본 런타임 구성 모드가 존재합니다.

* **Development**:
  * 손쉬운 디버깅을 위해 소스 맵이 포함되어 있습니다.
  * 성능을 위한 클라이언트 측 코드를 최적화하지 않습니다.
* **Production**:
  * 소스 맵을 제외합니다.
  * 번들링 및 축소를 통해서 클라이언트 측 코드를 최적화합니다.

ASP.NET Core는 `ASPNETCORE_ENVIRONMENT` 라는 환경 변수를 사용하여 구성 모드를 저장합니다. 자세한 내용은 **[환경 설정하기](xref:fundamentals/environments#set-the-environment)** 를 참고하시기 바랍니다.

### <a name="running-with-net-core-cli"></a>.NET Core CLI로 실행하기

다음 명령을 프로젝트 루트에서 실행하여 필요한 NuGet 및 npm 패키지를 복원합니다.

```console
dotnet restore && npm i
```

응용 프로그램을 빌드하고 실행합니다.

```console
dotnet run
```

응용 프로그램은 [런타임 구성 모드](#runtime-config-mode)에 따라 localhost에서 시작됩니다. 브라우저에서 `http://localhost:5000`로 이동하면 방문 페이지가 표시됩니다.

### <a name="running-with-visual-studio-2017"></a>Visual Studio 2017로 실행하기

[dotnet new](/dotnet/core/tools/dotnet-new) 명령으로 생성한 *.csproj* 파일을 엽니다. 필요한 NuGet 및 npm 패키지는 프로젝트가 열릴 때 자동으로 복원됩니다. 이 복원 프로세스는 최대 몇 분 정도 걸릴 수 있으며 완료되면 응용 프로그램을 실행할 준비가 완료됩니다. 녹색 실행 버튼을 클릭하거나 `Ctrl + F5` 키를 누르면 브라우저가 응용 프로그램의 방문 페이지를 엽니다. 응용 프로그램은 [런타임 구성 모드](#runtime-config-mode)에 따라 localhost에서 실행됩니다.

<a name="app-testing"></a>

## <a name="testing-the-app"></a>앱 테스트하기

SpaServices 템플릿은 [Karma](https://karma-runner.github.io/1.0/index.html)와 [Jasmine](https://jasmine.github.io/)을 사용하여 클라이언트 측 테스트를 실행하도록 미리 구성되어 있습니다. Jasmine은 인기 있는 JavaScript 용 단위 테스트 프레임워크인 반면, Karma는 해당 테스트에 대한 테스트 러너입니다. Karma는 [Webpack Dev 미들웨어](#webpack-dev-middleware)와 함께 동작하도록 구성되어 있으므로 개발자는 변경 사항이 있을 때마다 매번 중단하고 테스트를 실행할 필요가 없습니다. 테스트 케이스에 대해 실행 중인 코드든 테스트 케이스 자체든 상관없이 테스트가 자동으로 실행됩니다.

Angular 응용 프로그램을 예로 들면, *counter.component.spec.ts* 파일에 `CounterComponent`에 대한 두 가지 Jasmine 테스트 케이스가 미리 제공됩니다.

[!code-typescript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/app/components/counter/counter.component.spec.ts?range=15-28)]

*ClientApp* 디렉터리에서 명령 프롬프트를 엽니다. 다음 명령을 실행합니다.

```console
npm test
```

이 스크립트는 *karma.conf.js* 파일에 정의된 설정을 읽는 Karma 테스트 러너를 실행합니다. *karma.conf.js*는 다른 설정들 중에서 `files` 배열을 통해서 실행될 테스트 파일을 식별합니다.

[!code-javascript[](../client-side/spa-services/sample/SpaServicesSampleApp/ClientApp/test/karma.conf.js?range=4-5,8-11)]

<a name="app-publishing"></a>

## <a name="publishing-the-application"></a>응용 프로그램 게시하기

생성된 클라이언트 측 자산과 게시된 ASP.NET Core의 결과물을 배포 준비 패키지로 결합하는 일은 번거로운 작업일 수도 있습니다. 다행스럽게도 SpaServices는 `RunWebpack`이라는 이름의 사용자 지정 MSBuild 대상으로 전체 게시 프로세스를 조정합니다.

[!code-xml[](../client-side/spa-services/sample/SpaServicesSampleApp/SpaServicesSampleApp.csproj?range=31-45)]

이 MSBuild 대상은 다음과 같은 작업을 책임집니다.

1. Npm 패키지를 복원합니다.
1. 타사 클라이언트 측 자산의 프로덕션 수준 빌드를 생성합니다.
1. 사용자 지정 클라이언트 측 자산의 프로덕션 수준 빌드를 생성합니다.
1. Webpack이 생성한 자산을 게시 폴더에 복사합니다.

다음을 실행하면 MSBuild 대상이 호출됩니다.

```console
dotnet publish -c Release
```

## <a name="additional-resources"></a>추가 자료

* [Angular Docs](https://angular.io/docs)
