---
title: Razor 구성 요소 호스트 및 배포
author: guardrex
description: 'ASP.NET Core, 콘텐츠 전송 네트워크(CDN), 파일 서버 및 GitHub 페이지를 사용하여 Razor 구성 요소 및 Blazor 앱을 호스트하고 배포하는 방법을 알아봅니다.'
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: host-and-deploy/razor-components/index
---
# <a name="host-and-deploy-razor-components"></a>Razor 구성 요소 호스트 및 배포

작성자: [Luke Latham](https://github.com/guardrex), [Rainer Stropek](https://www.timecockpit.com) 및 [Daniel Roth](https://github.com/danroth27)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

## <a name="publish-the-app"></a>앱 게시

앱은 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령을 사용하여 릴리스 구성으로 배포하기 위해 게시됩니다. IDE는 자체에 내장된 게시 기능을 사용하여 자동으로 `dotnet publish` 명령의 실행을 처리할 수 있으므로, 사용 중인 개발 도구에 따라 명령 프롬프트에서 수동으로 명령을 실행할 필요가 없을 수도 있습니다.

```console
dotnet publish -c Release
```

`dotnet publish`는 배포할 자산을 만들기 전에 프로젝트의 종속성을 [복원](/dotnet/core/tools/dotnet-restore)하고 프로젝트를 [빌드](/dotnet/core/tools/dotnet-build)합니다. 빌드 프로세스의 일부로 앱 다운로드 크기와 로드 시간을 줄이기 위해 사용하지 않는 메서드와 어셈블리를 제거합니다. 배포는 */bin/Release/&lt;target-framework&gt;/publish* 폴더에 생성됩니다.

*publish* 폴더의 자산은 웹 서버에 배포됩니다. 배포는 사용 중인 개발 도구에 따라 수동 프로세스일 수도 있고 자동 프로세스일 수도 있습니다.

## <a name="host-configuration-values"></a>호스트 구성 값

[서버 쪽 호스팅 모델](xref:razor-components/hosting-models#server-side-hosting-model)을 사용하는 Razpr 구성 요소 앱은 [웹 호스트 구성 값](xref:fundamentals/host/web-host#host-configuration-values)을 허용할 수 있습니다.

[클라이언트 쪽 호스팅 모델](xref:razor-components/hosting-models#client-side-hosting-model)을 사용하는 Blazor 앱은 개발 환경의 런타임에 다음 호스트 구성 값을 명령줄 인수로 허용할 수 있습니다.

### <a name="content-root"></a>콘텐츠 루트

`--contentroot` 인수는 앱의 콘텐츠 파일을 포함하는 디렉터리에 대한 절대 경로를 설정합니다.

* 명령 프롬프트에서 앱을 로컬로 실행할 때 인수를 전달합니다. 앱의 디렉터리에서 다음을 실행합니다.

  ```console
  dotnet run --contentroot=/<content-root>
  ```

* **IIS Express** 프로필의 *launchSettings.json* 파일에 항목을 추가합니다. 이 설정은 Visual Studio Debugger를 사용하여 앱을 실행하는 경우 및 `dotnet run`을 사용하여 명령 프롬프트에서 앱을 실행할 때 선택합니다.

  ```json
  "commandLineArgs": "--contentroot=/<content-root>"
  ```

* Visual Studio의 **속성** > **디버그** > **애플리케이션 인수**에서 인수를 지정합니다. Visual Studio 속성 페이지에서 인수를 설정하면 해당 인수를 *launchSettings.json* 파일에 추가합니다.

  ```console
  --contentroot=/<content-root>
  ```

### <a name="path-base"></a>경로 기준

`--pathbase` 인수는 루트가 아닌 가상 경로를 사용하여 로컬로 앱을 실행하기 위한 앱 기본 경로를 설정합니다. (준비 및 프로덕션의 경우 `<base>` 태그 `href`는 `/` 이외의 경로로 설정됩니다). 자세한 내용은 [앱 기본 경로](#app-base-path) 섹션을 참조하세요.

> [!IMPORTANT]
> `<base>` 태그의 `href`에 대해 제공되는 경로와 달리 `--pathbase` 인수 값을 전달할 때 뒤에 슬래시(`/`)를 포함하지 않습니다. 앱 기본 경로가 `<base>` 태그에 `<base href="/CoolApp/" />`로 제공되는 경우(뒤에 슬래시 포함) 명령줄 인수 값을 `--pathbase=/CoolApp`로 전달합니다(뒤에 슬래시 없음).

* 명령 프롬프트에서 앱을 로컬로 실행할 때 인수를 전달합니다. 앱의 디렉터리에서 다음을 실행합니다.

  ```console
  dotnet run --pathbase=/<virtual-path>
  ```

* **IIS Express** 프로필의 *launchSettings.json* 파일에 항목을 추가합니다. 이 설정은 Visual Studio Debugger를 사용하여 앱을 실행하는 경우 및 `dotnet run`을 사용하여 명령 프롬프트에서 앱을 실행할 때 선택합니다.

  ```json
  "commandLineArgs": "--pathbase=/<virtual-path>"
  ```

* Visual Studio의 **속성** > **디버그** > **애플리케이션 인수**에서 인수를 지정합니다. Visual Studio 속성 페이지에서 인수를 설정하면 해당 인수를 *launchSettings.json* 파일에 추가합니다.

  ```console
  --pathbase=/<virtual-path>
  ```

### <a name="urls"></a>URL

`--urls` 인수는 요청을 수신하기 위한 포트 및 프로토콜을 포함하는 IP 주소 또는 호스트 주소를 나타냅니다.

* 명령 프롬프트에서 앱을 로컬로 실행할 때 인수를 전달합니다. 앱의 디렉터리에서 다음을 실행합니다.

  ```console
  dotnet run --urls=http://127.0.0.1:0
  ```

* **IIS Express** 프로필의 *launchSettings.json* 파일에 항목을 추가합니다. 이 설정은 Visual Studio Debugger를 사용하여 앱을 실행하는 경우 및 `dotnet run`을 사용하여 명령 프롬프트에서 앱을 실행할 때 선택합니다.

  ```json
  "commandLineArgs": "--urls=http://127.0.0.1:0"
  ```

* Visual Studio의 **속성** > **디버그** > **애플리케이션 인수**에서 인수를 지정합니다. Visual Studio 속성 페이지에서 인수를 설정하면 해당 인수를 *launchSettings.json* 파일에 추가합니다.

  ```console
  --urls=http://127.0.0.1:0
  ```

## <a name="deploy-a-client-side-blazor-app"></a>클라이언트 쪽 Blazor 앱 배포

[클라이언트 쪽 호스팅 모델](xref:razor-components/hosting-models#client-side-hosting-model)을 사용하는 경우:

* Blazor 앱, 해당 앱의 종속성 및 .NET 런타임이 브라우저에 다운로드됩니다.
* 해당 앱은 브라우저 UI 스레드에서 직접 실행됩니다. 다음 방법 중 하나 이상을 사용할 수 있습니다.
  * Blazor 앱은 ASP.NET Core 앱에서 제공됩니다. [ASP.NET Core를 사용하여 클라이언트 쪽 Blazor가 호스트하는 배포](#client-side-blazor-hosted-deployment-with-aspnet-core) 섹션을 참조하세요.
  * Blazor 앱은 정적 호스팅 웹 서버 또는 서비스에 배치되며, 이 경우 Blazor 앱을 처리하기 위해 .NET을 사용하지 않습니다. [클라이언트 쪽 Blazor 독립 실행형 배포](#client-side-blazor-standalone-deployment) 섹션을 참조하세요.
  
### <a name="configure-the-linker"></a>링커 구성

Blazor는 각 빌드에 대해 IL(중간 언어) 연결을 수행하여 출력 어셈블리에서 불필요한 IL을 제거합니다. 빌드에 대한 어셈블리 연결을 제어할 수 있습니다. 자세한 내용은 <xref:host-and-deploy/razor-components/configure-linker>을 참조하세요.

### <a name="rewrite-urls-for-correct-routing"></a>올바른 라우팅을 위해 URL 다시 생성

클라이언트 쪽 앱의 페이지 구성 요소에 대한 요청 라우팅은 서버 쪽에서 호스트하는 앱에 대한 요청 라우팅처럼 간단하지 않습니다. 다음 두 페이지를 사용하여 클라이언트 쪽 앱을 생각해 보겠습니다.

* **_Main.cshtml_** &ndash; 앱의 루트에서 로드하며 정보 페이지(`href="About"`)에 대한 링크를 포함합니다.
* **_About.cshtml_** &ndash; 페이지 정보입니다.

브라우저의 주소 표시줄을 사용하여 앱의 기본 문서를 요청하는 경우(예: `https://www.contoso.com/`):

1. 브라우저가 요청을 합니다.
1. 기본 페이지(일반적으로 *index.html*)가 반환됩니다.
1. *index.html* 앱을 부트스트랩으로 처리합니다.
1. Blazor의 라우터가 로드되고 Razor 기본 페이지(*Main.cshtml*)가 표시됩니다.

기본 페이지에서 정보 페이지에 대한 링크를 선택하면 정보 페이지가 로드됩니다. Blazor 라우터는 브라우저가 인터넷상에서 `www.contoso.com`에 대해 `About`를 요청하는 것을 중단하므로 정보 페이지에 대한 링크 선택은 클라이언트에서 작동합니다. *클라이언트 쪽 앱 내의* 내부 페이지에 대한 모든 요청도 같은 방법으로 작동합니다. 요청은 인터넷상에서 서버가 호스트하는 리소스에 대한 브라우저 기반 요청을 트리거하지 않습니다. 라우터가 내부적으로 요청을 처리합니다.

브라우저의 주소 표시줄을 사용하여 `www.contoso.com/About`을 요청하면 해당 요청이 실패합니다. 앱의 인터넷 호스트에 해당 리소스가 없으므로 *찾을 수 없음 404* 응답이 반환됩니다.

브라우저는 인터넷 기반 호스트에 대해 클라이언트 쪽 페이지를 요청하므로, 웹 서버 및 호스팅 서비스는 서버에 실제로 존재하지 않는 리소스에 대한 모든 요청을 *index.html* 페이지에 씁니다. *index.html*이 반환되는 경우 앱의 클라이언트 쪽 라우터가 인수하여 올바른 리소스로 응답합니다.

### <a name="app-base-path"></a>앱 기본 경로

앱 기본 경로는 서버상의 가상 앱 루트 경로입니다. 예를 들어 Contoso 서버의 가상 폴더 `/CoolApp/`에 상주하는 앱은 `https://www.contoso.com/CoolApp`에 도달하며 `/CoolApp/`의 가상 기본 경로를 포함합니다. 앱 기본 경로를 `CoolApp/`로 설정하면 앱은 서버상에 가상으로 상주하는 위치를 인식하게 됩니다. 해당 앱은 앱 기본 경로를 사용하여 루트 디렉터리에 없는 구성 요소에서 앱 루트에 대한 상대 URL을 구성합니다. 이렇게 하면 디렉터리 구조의 다른 수준에 존재하는 구성 요소가 앱 전체의 위치에서 다른 리소스에 대한 링크를 만들 수 있습니다. 또한 링크의 `href` 대상이 앱 기본 경로 내에 있는 경우 &mdash; Blazor 라우터가 내부 탐색을 처리하는 경우 하이퍼링크 클릭을 가로채기 위해서도 앱 기본 경로를 사용합니다.

많은 호스팅 시나리오에서 앱에 대한 서버의 가상 경로는 앱의 루트입니다. 이러한 경우 앱 기본 경로는 앱에 대한 기본 구성인 슬래시(`<base href="/" />`)입니다. GitHub 페이지 및 IIS 가상 디렉터리 또는 하위 애플리케이션 등의 다른 호스팅 시나리오에서는 앱 기본 경로를 앱에 대한 서버의 가상 경로로 설정해야 합니다. 앱의 기본 경로를 설정하려면 `<head>` 태그 요소 내에서 찾은 *index.html*의 `<base>` 태그를 추가하거나 업데이트합니다. `href` 속성 값을 `<virtual-path>/`(뒤에 슬래시가 필요함)로 설정하며, 여기서 `<virtual-path>/`는 앱에 대한 서버의 전체 가상 앱 루트 경로입니다. 앞의 예에서 가상 경로는 `CoolApp/`: `<base href="CoolApp/" />`로 설정됩니다.

루트가 아닌 경로가 구성된 앱(예: `<base href="CoolApp/" />`)의 경우, 앱은 *로컬로 실행하면* 해당 리소스를 찾지 못합니다. 로컬 개발 및 시험 중에 이 문제를 해결하려면 런타임에 `<base>` 태그의 `href` 값과 일치하는 *기본 경로* 인수를 제공할 수 있습니다.

앱을 로컬로 실행하는 경우 경로 기본 인수를 루트 경로(`/`)와 함께 전달하려면 앱의 디렉터리에서 다음 명령을 실행합니다.

```console
dotnet run --pathbase=/CoolApp
```

앱이 `http://localhost:port/CoolApp`에서 로컬로 응답합니다.

자세한 내용은 [경로 기본 호스트 구성 값](#path-base) 섹션을 참조하세요.

> [!IMPORTANT]
> 앱이 [클라이언트 쪽 호스팅 모델](xref:razor-components/hosting-models#client-side-hosting-model)(**Blazor** 프로젝트 템플릿 기반)을 사용하고 ASP.NET Core 앱에서 IIS 하위 애플리케이션으로 호스트되는 경우, 상속된 ASP.NET Core 모듈 핸들러를 사용하지 않도록 설정하거나 *web.config* 파일에서 루트(상위) 앱의 `<handlers>` 섹션을 하위 앱에서 상속하지 않도록 해야 합니다.
>
> 파일에 `<handlers>` 섹션을 추가하여 앱의 게시된 *web.config* 파일에서 핸들러를 제거합니다.
>
> ```xml
> <handlers>
>   <remove name="aspNetCore" />
> </handlers>
> ```
>
> 또는 `inheritInChildApplications`를 `false`로 설정한 상태에서 `<location>` 요소를 사용하여 루트(상위) 앱의 `<system.webServer>` 섹션의 상속을 사용하지 않도록 설정합니다.
>
> ```xml
> <?xml version="1.0" encoding="utf-8"?>
> <configuration>
>  <location path="." inheritInChildApplications="false">
>    <system.webServer>
>      <handlers>
>        <add name="aspNetCore" ... />
>      </handlers>
>      <aspNetCore ... />
>    </system.webServer>
>  </location>
> </configuration>
> ```
>
> 핸들러 제거 또는 상속을 사용하지 않도록 설정은 이 섹션에서 설명하는 대로 앱의 기본 경로 구성에 더하여 수행됩니다. IIS에서 하위 앱을 구성할 때
앱의 *index.html* 파일에서 앱 기본 경로를 사용한 IIS 별칭으로 설정합니다.

### <a name="client-side-blazor-hosted-deployment-with-aspnet-core"></a>ASP.NET Core를 사용하여 클라이언트 쪽 Blazor가 호스트하는 배포

*호스트하는 배포*는 서버상에서 실행하는 [ASP.NET Core 앱](xref:index)에서 클라이언트 쪽 Blazor 앱을 브라우저에 제공하지 않습니다.

Blazor 앱은 ASP.NET Core 앱과 함께 배포되도록 게시된 출력의 후자 앱과 함께 포함됩니다. ASP.NET Core 앱을 호스트할 수 있는 웹 서버가 필요합니다. 호스트하는 배포의 경우, Visual Studio는 **Blazor(ASP.NET Core가 호스트하는)** 프로젝트 템플릿([dotnet new](/dotnet/core/tools/dotnet-new) 명령을 사용하는 경우 `blazorhosted` 템플릿)을 포함합니다.

ASP.NET Core 앱 호스팅 및 배포에 대한 자세한 내용은 <xref:host-and-deploy/index>를 참조하세요.

Azure App Service에 배포에 대한 자세한 내용은 다음 토픽을 참조하세요.

<xref:tutorials/publish-to-azure-webapp-using-vs>  
Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.

### <a name="client-side-blazor-standalone-deployment"></a>클라이언트 쪽 Blazor 독립 실행형 배포

*독립 실행형 배포*는 클라이언트 쪽 Blazor 앱을 클라이언트가 직접 요청하는 정적 파일 세트로 제공합니다. Blazor 앱을 제공하기 위해 웹 서버를 사용하지 않습니다.

#### <a name="client-side-blazor-standalone-hosting-with-iis"></a>IIS를 사용하여 클라이언트 쪽 Blazor 독립 실행형 호스팅

IIS는 Blazor 앱에 사용할 수 있는 정적 파일 서버입니다. Blazor를 호스트하도록 IIS를 구성하려면 [IIS에서 정적 웹 사이트 작성](/iis/manage/creating-websites/scenario-build-a-static-website-on-iis)을 참조하세요.

게시된 자산은 *\\bin\\Release\\&lt;target-framework&gt;\\publish* 폴더에 생성됩니다. 웹 서버 또는 호스팅 서비스에서 *publish* 폴더의 콘텐츠를 호스트합니다.

**web.config**

Blazor 프로젝트가 게시되면 다음 IIS 구성을 사용하여 *web.config* 파일이 생성됩니다.

* 다음 파일 확장명에 대해 MIME 형식을 설정합니다.
  * *\*.dll*: `application/octet-stream`
  * *\*.json*: `application/json`
  * *\*.wasm*: `application/wasm`
  * *\*.woff*: `application/font-woff`
  * *\*.woff2*: `application/font-woff`
* 다음 MIME 형식에 대해 HTTP 압축을 사용합니다.
  * `application/octet-stream`
  * `application/wasm`
* URL 재작성 모듈 규칙을 설정합니다.
  * 앱의 정적 자산이 상주하는 하위 디렉터리(*&lt;assembly_name&gt;\\dist\\&lt;path_requested&gt;*)를 제공합니다.
  * 파일이 아닌 자산에 대한 요청이 정적 자산 폴더에 있는 앱의 기본 문서(*&lt;assembly_name&gt;\\dist\\index.html*)로 리디렉션되도록 SPA 폴백 라우팅을 만듭니다.

**URL 다시 생성 모듈 설치**

URL을 다시 생성하려면 [URL 다시 생성 모듈](https://www.iis.net/downloads/microsoft/url-rewrite)이 필요합니다. 이 모듈은 기본적으로 설치되지 않으며 웹 서버(IIS) 역할 서비스 기능으로 설치하는 데 사용할 수 없습니다. 이 모듈은 IIS 웹 사이트에서 다운로드해야 합니다. 웹 플랫폼 설치 관리자를 사용하여 이 모듈을 설치합니다.

1. 로컬에서 [URL 다시 생성 모듈 다운로드 페이지](https://www.iis.net/downloads/microsoft/url-rewrite#additionalDownloads)로 이동합니다. 영어 버전의 경우 **WebPI**를 선택하여 WebPI 설치 관리자를 다운로드합니다. 다른 언어의 경우 서버에 맞는 아키텍처(x86 x64)를 선택하여 설치 관리자를 다운로드합니다.
1. 설치 관리자를 서버에 복사합니다. 설치 관리자를 실행합니다. **설치** 버튼을 선택하고 사용 조건에 동의합니다. 설치가 완료된 후 서버를 다시 시작하지 않아도 됩니다.

**웹 사이트 구성**

웹 사이트의 **실제 경로**를 앱의 폴더로 설정합니다. 이 폴더는 다음을 포함합니다.

* 필요한 리디렉션 규칙 및 파일 콘텐츠 형식 등 IIS가 웹 사이트를 구성하기 위해 사용하는 *web.config* 파일.
* 앱의 정적 자산 폴더입니다.

**문제 해결**

*500 내부 서버 오류*가 수신되고 웹 사이트의 구성에 액세스를 시도할 때 IIS 관리자가 오류를 표시하면 URL 다시 생성 모듈이 설치되었는지 확인합니다. 모듈이 설치되지 않은 경우 IIS가 *web.config* 파일을 구문 분석할 수 없습니다. 그러면 IIS 관리자가 웹 사이트의 구성을 로드할 수 없으며 웹 사이트가 Blazor의 정적 파일을 제공할 수 없습니다.

IIS 배포 문제 해결에 대한 자세한 내용은 <xref:host-and-deploy/iis/troubleshoot>를 참조하세요.

#### <a name="client-side-blazor-standalone-hosting-with-nginx"></a>Nginx를 사용하여 클라이언트 쪽 Blazor 독립 실행형 호스팅

다음 *nginx.conf* 파일은 Nginx가 디스크에서 *Index.html* 파일을 찾을 수 없을 때마다 해당 파일을 보내도록 구성하는 방법을 보여 주도록 단순화되었습니다.

```
events { }
http {
    server {
        listen 80;

        location / {
            root /usr/share/nginx/html;
            try_files $uri $uri/ /Index.html =404;
        }
    }
}
```

프로덕션 Nginx 웹 서버 구성에 대한 자세한 내용은 [NGINX Plus 및 NGINX 구성 파일 만들기](https://docs.nginx.com/nginx/admin-guide/basic-functionality/managing-configuration-files/)를 참조하세요.

#### <a name="client-side-blazor-standalone-hosting-with-nginx-in-docker"></a>Docker에서 Nginx를 사용하여 클라이언트 쪽 Blazor 독립 실행형 호스팅

Docker에서 Nginx를 사용하여 Blazor를 호스트하려면 Dockerfile을 Alpine 기반 Nginx 이미지를 사용하도록 구성합니다. Dockerfile을 업데이트하여 *nginx.config* 파일을 컨테이너에 복사합니다.

다음 예제와 같이 Dockerfile에 한 줄을 추가합니다.

```
FROM nginx:alpine
COPY ./bin/Release/netstandard2.0/publish /usr/share/nginx/html/
COPY nginx.conf /etc/nginx/nginx.conf
```

#### <a name="client-side-blazor-standalone-hosting-with-github-pages"></a>GitHub 페이지를 사용하여 클라이언트 쪽 Blazor 독립 실행형 호스팅

URL 다시 생성을 처리하려면 *index.html* 페이지로 요청 리디렉션을 처리하는 스크립트를 사용하여 *404.html* 파일을 추가합니다. 커뮤니티에서 제공하는 예제 구현은 [GitHub 페이지에 대한 단일 페이지 앱](http://spa-github-pages.rafrex.com/)([rafrex/spa-github-pages on GitHub](https://github.com/rafrex/spa-github-pages#readme))을 참조하세요. 커뮤니티 방식을 사용하는 예는 [blazor-demo/blazor-demo.github.io on GitHub](https://github.com/blazor-demo/blazor-demo.github.io)([실시간 사이트](https://blazor-demo.github.io/))를 참조하세요.

조직의 사이트 대신 프로젝트 사이트를 사용하는 경우 *index.html*의 `<base>` 태그를 추가하거나 업데이트합니다. `href` 속성 값을 `<repository-name>/`으로 설정하며, 여기서 `<repository-name>/`은 GitHub 리포지토리 이름입니다.

## <a name="deploy-a-server-side-razor-components-app"></a>서버 쪽 Razor 구성 요소 앱 배포

[서버 쪽 호스팅 모델](xref:razor-components/hosting-models#server-side-hosting-model)을 사용하는 경우 Razor 구성 요소는 서버의 ASP.NET Core 앱에서 실행됩니다. UI 업데이트, 이벤트 처리 및 JavaScript 호출은 SignalR 연결상에서 처리됩니다.

이 앱은 ASP.NET Core 앱과 함께 배포되도록 게시된 출력의 후자 앱과 함께 포함됩니다. ASP.NET Core 앱을 호스트할 수 있는 웹 서버가 필요합니다. 서버 쪽 배포의 경우, Visual Studio는 **Blazor(ASP.NET Core의 서버 쪽)** 프로젝트 템플릿([dotnet new](/dotnet/core/tools/dotnet-new) 명령을 사용하는 경우 `blazorserver` 템플릿)을 포함합니다.

<!--

**INSERT: Concerns are the same as publishing an ASP.NET Core SignalR app**

**INSERT: Content on the Azure SignalR Service**

**INSERT: Manually turn on WebSockets support**

-->

ASP.NET Core 앱이 게시된 경우 Razor 구성 요소는 ASP.NET Core 앱 및 Razor 구성 요소 앱을 함께 배포할 수 있도록 게시된 출력에 포함됩니다. ASP.NET Core 앱 호스팅 및 배포에 대한 자세한 내용은 <xref:host-and-deploy/index>를 참조하세요.

Azure App Service에 배포에 대한 자세한 내용은 다음 토픽을 참조하세요.

<xref:tutorials/publish-to-azure-webapp-using-vs>  
Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.
