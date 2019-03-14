---
title: ASP.NET Core의 웹 서버 구현
author: guardrex
description: ASP.NET Core의 웹 서버 Kestrel 및 HTTP.sys를 검색합니다. 서버를 선택하는 방법 및 역방향 프록시 서버를 사용하는 시기에 대해 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/14/2019
uid: fundamentals/servers/index
---
# <a name="web-server-implementations-in-aspnet-core"></a>ASP.NET Core의 웹 서버 구현

작성자: [Tom Dykstra](https://github.com/tdykstra), [Steve Smith](https://ardalis.com/), [Stephen Halter](https://twitter.com/halter73) 및 [Chris Ross](https://github.com/Tratcher)

ASP.NET Core 앱은 In-process HTTP 서버 구현을 사용하여 실행됩니다. 서버 구현은 HTTP 요청을 수신하고 <xref:Microsoft.AspNetCore.Http.HttpContext>에 구성된 일련의 [요청 기능](xref:fundamentals/request-features)으로 앱에 표시합니다.

::: moniker range=">= aspnetcore-2.2"

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

ASP.NET Core는 다음과 함께 제공됩니다.

* [Kestrel 서버](xref:fundamentals/servers/kestrel)는 플랫폼 간 기본 HTTP 서버를 구현한 것입니다.
* IIS HTTP 서버는 IIS의 [In-process 서버](#in-process-hosting-model)입니다.
* [HTTP.sys 서버](xref:fundamentals/servers/httpsys)는 [Http.Sys 커널 드라이버 및 HTTP Server API](/windows/desktop/Http/http-api-start-page)를 기반으로 하는 Windows 전용 HTTP 서버입니다.

[IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 사용하는 경우 앱은 다음 중 하나를 실행합니다.

* [IIS HTTP 서버](#iis-http-server)를 사용하는 IIS 작업자 프로세스([In-process 호스팅 모델](#in-process-hosting-model))와 동일한 프로세스에서 권장되는 구성은 *In process*입니다.
* [Kestrel 서버](#kestrel)를 사용하는 IIS 작업자 프로세스([out-of-process 호스팅 모델](#out-of-process-hosting-model))와 다른 별도의 프로세스에서

[ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)은 IIS와 In-process IIS HTTP 서버 또는 Kestrel 간의 네이티브 IIS 요청을 처리하는 네이티브 IIS 모듈입니다. 자세한 내용은 <xref:host-and-deploy/aspnet-core-module>을 참조하세요.

## <a name="hosting-models"></a>호스팅 모델

### <a name="in-process-hosting-model"></a>In-Process 호스팅 모델

In-Process 호스팅을 사용하면 ASP.NET Core 앱은 IIS 작업자 프로세스와 동일한 프로세스에서 실행됩니다. 나가는 네트워크 트래픽을 동일한 머신에 다시 반환하는 네트워크 인터페이스인 루프백 어댑터를 통해 요청이 프록시되지 않기 때문에 In Process 호스팅에서는 Out-of-process 호스팅을 통해 성능을 개선합니다. IIS는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)를 사용하여 프로세스 관리를 처리합니다.

ASP.NET Core 모듈:

* 앱 초기화를 수행합니다.
  * [CoreCLR](/dotnet/standard/glossary#coreclr)을 로드합니다.
  * `Program.Main`.
* IIS 네이티브 요청의 수명을 처리합니다.

In-process 호스팅 모델은 .NET Framework를 대상으로 하는 ASP.NET Core 앱을 지원하지 않습니다.

다음 다이어그램은 IIS, ASP.NET Core 모듈 및 In-Process에 호스트된 앱 간의 관계를 보여 줍니다.

![ASP.NET Core 모듈](_static/ancm-inprocess.png)

요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다. 드라이버는 웹 사이트의 구성된 포트[일반적으로 80(HTTP) 또는 443(HTTPS)]에서 IIS로 네이티브 요청을 라우팅합니다. 모듈에서는 기본 요청을 수신하고 IIS HTTP Server(`IISHttpServer`)에 전달합니다. IIS HTTP 서버는 네이티브 요청을 관리형 요청으로 변환하는 IIS의 In-process 서버를 구현한 것입니다.

IIS HTTP Server가 요청을 처리하면 해당 요청이 ASP.NET Core 미들웨어 파이프라인에 푸시됩니다. 미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다. 앱의 응답은 IIS HTTP 서버를 통해 IIS로 다시 전달됩니다. IIS는 요청을 시작한 클라이언트에 응답을 보냅니다.

In-process 호스팅은 기존 앱에 대한 옵트인(opt-in) 기능이지만 [dotnet new](/dotnet/core/tools/dotnet-new) 템플릿은 기본적으로 모든 IIS 및 IIS Express 시나리오에 대해 In-Process 호스팅 모델로 설정됩니다.

### <a name="out-of-process-hosting-model"></a>Out-of-Process 호스팅 모델

ASP.NET Core 앱은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 이 모듈은 프로세스 관리를 수행합니다. 이 모듈은 첫 번째 요청이 들어올 때 ASP.NET Core 앱용 프로세스를 시작하고 종료되거나 충돌이 발생하면 앱을 다시 시작합니다. 이는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)로 관리되는 In-Process로 실행되는 앱에서 볼 수 있는 동작과 기본적으로 동일합니다.

다음 다이어그램은 IIS, ASP.NET Core 모듈 및 Out-of-Process에 호스트된 앱 간의 관계를 보여 줍니다.

![ASP.NET Core 모듈](_static/ancm-outofprocess.png)

요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다. 드라이버는 웹 사이트의 구성된 포트(일반적으로 80(HTTP) 또는 443(HTTPS))에서 IIS로 요청을 라우팅합니다. 모듈은 포트 80 또는 443이 아닌 앱의 임의의 포트에서 Kestrel로 요청을 전달합니다.

모듈은 시작 시 환경 변수를 통해 포트를 지정하고 IIS 통합 미들웨어는 `http://localhost:{PORT}`에서 수신 대기하도록 서버를 구성합니다. 추가 검사가 수행되고 모듈에서 시작되지 않은 요청은 거부됩니다. 모듈은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신된 경우에도 HTTP를 통해 요청이 전달됩니다.

Kestrel이 모듈에서 요청을 선택한 후, 요청은 ASP.NET Core 미들웨어 파이프라인으로 푸시됩니다. 미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다. IIS 통합에 의해 추가된 미들웨어는 체계, 원격 IP 및 경로 기준을 Kestrel에 요청을 전달하기 위한 계정으로 업데이트합니다. 앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.

IIS 및 ASP.NET Core 모듈 구성 지침은 다음 토픽을 참조하세요.

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/aspnet-core-module>

# <a name="macostabmacos"></a>[macOS](#tab/macos)

ASP.NET Core는 기본 플랫폼 간 HTTP 서버인 [Kestrel 서버](xref:fundamentals/servers/kestrel)와 함께 제공됩니다.

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

ASP.NET Core는 기본 플랫폼 간 HTTP 서버인 [Kestrel 서버](xref:fundamentals/servers/kestrel)와 함께 제공됩니다.

---

::: moniker-end

::: moniker range="< aspnetcore-2.2"

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

ASP.NET Core는 다음과 함께 제공됩니다.

* [Kestrel](xref:fundamentals/servers/kestrel) 서버는 기본 플랫폼 간 HTTP 서버입니다.
* [HTTP.sys 서버](xref:fundamentals/servers/httpsys)는 [Http.Sys 커널 드라이버 및 HTTP Server API](/windows/desktop/Http/http-api-start-page)를 기반으로 하는 Windows 전용 HTTP 서버입니다.

[IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 사용하면 앱이 [Kestrel 서버](#kestrel)를 사용하는 IIS 작업자 프로세스(*out-of-process*)와 다른 별도의 프로세스에서 실행됩니다.

ASP.NET Core 앱은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 이 모듈은 프로세스 관리를 수행합니다. 이 모듈은 첫 번째 요청이 들어올 때 ASP.NET Core 앱용 프로세스를 시작하고 종료되거나 충돌이 발생하면 앱을 다시 시작합니다. 이는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)로 관리되는 In-Process로 실행되는 앱에서 볼 수 있는 동작과 기본적으로 동일합니다.

다음 다이어그램은 IIS, ASP.NET Core 모듈 및 Out-of-Process에 호스트된 앱 간의 관계를 보여 줍니다.

![ASP.NET Core 모듈](_static/ancm-outofprocess.png)

요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다. 드라이버는 웹 사이트의 구성된 포트(일반적으로 80(HTTP) 또는 443(HTTPS))에서 IIS로 요청을 라우팅합니다. 모듈은 포트 80 또는 443이 아닌 앱의 임의의 포트에서 Kestrel로 요청을 전달합니다.

모듈은 시작 시 환경 변수를 통해 포트를 지정하고 IIS 통합 미들웨어는 `http://localhost:{port}`에서 수신 대기하도록 서버를 구성합니다. 추가 검사가 수행되고 모듈에서 시작되지 않은 요청은 거부됩니다. 모듈은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신된 경우에도 HTTP를 통해 요청이 전달됩니다.

Kestrel이 모듈에서 요청을 선택한 후, 요청은 ASP.NET Core 미들웨어 파이프라인으로 푸시됩니다. 미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다. IIS 통합에 의해 추가된 미들웨어는 체계, 원격 IP 및 경로 기준을 Kestrel에 요청을 전달하기 위한 계정으로 업데이트합니다. 앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.

IIS 및 ASP.NET Core 모듈 구성 지침은 다음 토픽을 참조하세요.

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/aspnet-core-module>

# <a name="macostabmacos"></a>[macOS](#tab/macos)

ASP.NET Core는 기본 플랫폼 간 HTTP 서버인 [Kestrel 서버](xref:fundamentals/servers/kestrel)와 함께 제공됩니다.

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

ASP.NET Core는 기본 플랫폼 간 HTTP 서버인 [Kestrel 서버](xref:fundamentals/servers/kestrel)와 함께 제공됩니다.

---

::: moniker-end

## <a name="kestrel"></a>Kestrel

Kestrel은 ASP.NET Core 프로젝트 템플릿에 포함된 기본 웹 서버입니다.

::: moniker range=">= aspnetcore-2.0"

Kestrel은 다음과 같이 사용할 수 있습니다.

* 인터넷을 포함한 네트워크로부터 직접 요청을 처리하는 에지 서버로서 단독으로 사용

  ![Kestrel은 역방향 프록시 서버 없이 직접 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet2.png)

* [IIS(인터넷 정보 서비스)](https://www.iis.net/), [Nginx](http://nginx.org) 또는 [Apache](https://httpd.apache.org/)와 같은 *역방향 프록시 서버*와 함께 사용 역방향 프록시 서버는 인터넷에서 HTTP 요청을 받아서 Kestrel에 전달합니다.

  ![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

&mdash;역방향 프록시 서버가 있는 호스팅 구성과 없는 호스팅 구성 모두&mdash; ASP.NET Core 2.1 이상 앱에 대해 지원됩니다.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

앱이 내부 네트워크의 요청만을 수락하는 경우 Kestrel을 단독으로 사용할 수 있습니다.

![Kestrel은 내부 네트워크와 직접 통신합니다.](kestrel/_static/kestrel-to-internal.png)

앱이 인터넷에 노출된 경우, Kestrel은 [IIS(인터넷 정보 서비스)](https://www.iis.net/), [Nginx](http://nginx.org) 또는 [Apache](https://httpd.apache.org/)와 같은 *역방향 프록시 서버*를 사용해야 합니다. 역방향 프록시 서버는 인터넷에서 HTTP 요청을 받아서 Kestrel에 전달합니다.

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

인터넷에 직접 노출되는 공용 에지 서버 배포에 역방향 프록시를 사용하는 가장 중요한 이유는 보안입니다. 1.x 버전의 Kestrel에는 인터넷의 공격으로부터 보호하기 위한 중요한 보안 기능이 없습니다. 여기에는 적절한 시간 제한, 요청 크기 제한, 동시 연결 제한을 비롯한 다양한 기능이 포함됩니다.

::: moniker-end

Kestrel을 역방향 프록시 구성에서 사용하는 경우에 대한 Kestrel 구성 지침 및 정보는 <xref:fundamentals/servers/kestrel>을 참조하세요.

### <a name="nginx-with-kestrel"></a>Nginx 및 Kestrel

Linux에서 Kestrel에 대한 역방향 프록시 서버로 Nginx를 사용하는 방법은 <xref:host-and-deploy/linux-nginx>를 참조하세요.

### <a name="apache-with-kestrel"></a>Apache 및 Kestrel

Linux에서 Kestrel에 대한 역방향 프록시 서버로 Apache를 사용하는 방법은 <xref:host-and-deploy/linux-apache>를 참조하세요.

::: moniker range=">= aspnetcore-2.2"

## <a name="iis-http-server"></a>IIS HTTP 서버

IIS HTTP 서버는 IIS의 [In-process 서버](#in-process-hosting-model)이고 In Process 배포에 필요합니다. [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)은 IIS와 IIS HTTP 서버 간에 네이티브 IIS 요청을 처리합니다. 자세한 내용은 <xref:host-and-deploy/aspnet-core-module>을 참조하세요.

::: moniker-end

## <a name="httpsys"></a>HTTP.sys

Windows에서 ASP.NET Core 앱을 실행할 경우 Kestrel 대신 HTTP.sys를 사용할 수 있습니다. 최상의 성능을 위해 일반적으로 Kestrel을 사용하는 것이 좋습니다. 앱이 인터넷에 노출되고 필수 기능이 Kestrel이 아닌 HTTP.sys에서 지원되는 경우 시나리오에서 HTTP.sys를 사용할 수 있습니다. 자세한 내용은 <xref:fundamentals/servers/httpsys>을 참조하세요.

![HTTP.sys는 인터넷과 직접 통신합니다.](httpsys/_static/httpsys-to-internet.png)

HTTP.sys는 내부 네트워크에만 노출되는 앱에도 사용할 수 있습니다.

![HTTP.sys는 내부 네트워크와 직접 통신합니다.](httpsys/_static/httpsys-to-internal.png)

HTTP.sys 구성 지침은 <xref:fundamentals/servers/httpsys>를 참조하세요.

## <a name="aspnet-core-server-infrastructure"></a>ASP.NET Core 서버 인프라

`Startup.Configure` 메서드에서 사용 가능한 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder>는 <xref:Microsoft.AspNetCore.Http.Features.IFeatureCollection> 형식의 <xref:Microsoft.AspNetCore.Builder.IApplicationBuilder.ServerFeatures> 속성을 노출합니다. Kestrel 및 HTTP.sys는 각각 단일 기능인 <xref:Microsoft.AspNetCore.Hosting.Server.Features.IServerAddressesFeature>만을 노출하지만 다른 서버 구현은 추가 기능을 노출할 수 있습니다.

`IServerAddressesFeature`를 사용하여 런타임 시 서버 구현이 바인딩된 포트를 확인할 수 있습니다.

## <a name="custom-servers"></a>사용자 지정 서버

기본 제공 서버가 앱의 요구 사항을 충족하지 않으면 사용자 지정 서버 구현을 만들 수 있습니다. [OWIN(Open Web Interface for .NET) 가이드](xref:fundamentals/owin)에서는 [Nowin](https://github.com/Bobris/Nowin) 기반 <xref:Microsoft.AspNetCore.Hosting.Server.IServer> 구현을 작성하는 방법을 보여 줍니다. 앱이 사용하는 기능 인터페이스에만 구현이 필요합니다. 최소한 <xref:Microsoft.AspNetCore.Http.Features.IHttpRequestFeature> 및 <xref:Microsoft.AspNetCore.Http.Features.IHttpResponseFeature>가 지원되어야 합니다.

## <a name="server-startup"></a>서버 시작

IDE(통합 개발 환경)이나 편집기가 앱을 시작하는 경우 서버가 실행됩니다.

* [Visual Studio](https://www.visualstudio.com/vs/) &ndash; 실행 프로필을 사용하여 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)/[ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module) 또는 콘솔에서 앱 및 서버를 시작할 수 있습니다.
* [Visual Studio Code](https://code.visualstudio.com/) &ndash; [Omnisharp](https://github.com/OmniSharp/omnisharp-vscode)로 앱 및 서버를 시작합니다. 그러면 CoreCLR 디버거를 활성화합니다.
* [Mac용 Visual Studio](https://www.visualstudio.com/vs/mac/) &ndash; [Mono Soft-Mode 디버거](https://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/)로 앱 및 서버를 시작합니다.

프로젝트의 폴더에 있는 명령 프롬프트에서 앱을 시작할 때 [dotnet run](/dotnet/core/tools/dotnet-run)은 서버 및 앱을 시작합니다(Kestrel 및 HTTP.sys만 해당). `Debug`(기본값) 또는 `Release`로 설정되어 있는 `-c|--configuration` 옵션으로 구성을 지정합니다. 실행 프로필이 *launchSettings.json* 파일에 있는 경우 `--launch-profile <NAME>` 옵션을 사용하여 실행 프로필(예: `Development` 또는 `Production`)을 설정합니다. 자세한 내용은 [dotnet run](/dotnet/core/tools/dotnet-run) 및 [.NET Core 배포 패키징](/dotnet/core/build/distribution-packaging)을 참조하세요.

## <a name="http2-support"></a>HTTP/2 지원

[HTTP/2](https://httpwg.org/specs/rfc7540.html)는 다음과 같은 배포 시나리오에서 ASP.NET Core를 통해 지원됩니다.

::: moniker range=">= aspnetcore-2.2"

* [Kestrel](xref:fundamentals/servers/kestrel#http2-support)
  * 운영 체제
    * Windows Server 2016/Windows 10 이상&dagger;
    * Linux 및 OpenSSL 1.0.2 이상(예: Ubuntu 16.04 이상)
    * 이후 릴리스에서는 macOS에서 HTTP/2가 지원됩니다.
  * 대상 프레임워크: .NET Core 2.2 이상
* [HTTP.sys](xref:fundamentals/servers/httpsys#http2-support)
  * Windows Server 2016/Windows 10 이상
  * 대상 프레임워크: HTTP.sys 배포에는 적용할 수 없습니다.
* [IIS(In-Process)](xref:host-and-deploy/iis/index#http2-support)
  * Windows Server 2016/Windows 10 이상, IIS 10 이상
  * 대상 프레임워크: .NET Core 2.2 이상
* [IIS(Out-of-process)](xref:host-and-deploy/iis/index#http2-support)
  * Windows Server 2016/Windows 10 이상, IIS 10 이상
  * 공용 에지 서버 연결은 HTTP/2를 사용하지만 Kestrel에 대한 역방향 프록시 연결은 HTTP/1.1을 사용합니다.
  * 대상 프레임워크: IIS Out-of-process 배포에는 적용할 수 없습니다.

&dagger;Kestrel은 Windows Server 2012 R2와 Windows 8.1에서의 HTTP/2 지원을 제한했습니다. 이러한 운영 체제에서 사용할 수 있는 지원 가능 TLS 암호 그룹 목록이 제한되므로 지원이 제한됩니다. TLS 연결을 보호하는 데 ECDSA(타원 곡선 디지털 서명 알고리즘)를 사용하여 생성된 인증서가 필요할 수 있습니다.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* [HTTP.sys](xref:fundamentals/servers/httpsys#http2-support)
  * Windows Server 2016/Windows 10 이상
  * 대상 프레임워크: HTTP.sys 배포에는 적용할 수 없습니다.
* [IIS(Out-of-process)](xref:host-and-deploy/iis/index#http2-support)
  * Windows Server 2016/Windows 10 이상, IIS 10 이상
  * 공용 에지 서버 연결은 HTTP/2를 사용하지만 Kestrel에 대한 역방향 프록시 연결은 HTTP/1.1을 사용합니다.
  * 대상 프레임워크: IIS Out-of-process 배포에는 적용할 수 없습니다.

::: moniker-end

HTTP/2 연결은 [ALPN(Application-Layer Protocol Negotiation)](https://tools.ietf.org/html/rfc7301#section-3) 및 TLS 1.2 이상을 사용해야 합니다. 자세한 정보는 서버 배포 시나리오와 관련된 항목을 참조하세요.

## <a name="additional-resources"></a>추가 자료

* <xref:fundamentals/servers/kestrel>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/azure-apps/index>
* <xref:host-and-deploy/linux-nginx>
* <xref:host-and-deploy/linux-apache>
* <xref:fundamentals/servers/httpsys>
