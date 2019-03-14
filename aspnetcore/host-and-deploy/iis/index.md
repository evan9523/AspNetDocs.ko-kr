---
title: IIS가 있는 Windows에서 ASP.NET Core 호스팅
author: guardrex
description: Windows Server IIS(인터넷 정보 서비스)에서 ASP.NET Core 앱을 호스팅하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/19/2019
uid: host-and-deploy/iis/index
---
# <a name="host-aspnet-core-on-windows-with-iis"></a>IIS가 있는 Windows에서 ASP.NET Core 호스팅

[Luke Latham](https://github.com/guardrex)으로

[.NET Core 호스팅 번들 설치](#install-the-net-core-hosting-bundle)

## <a name="supported-operating-systems"></a>지원되는 운영 체제

지원되는 운영 체제는 다음과 같습니다.

* Windows 7 이상
* Windows Server 2008 R2 이상

[HTTP.sys 서버](xref:fundamentals/servers/httpsys)(이전의 WebListener)는 IIS를 사용하는 역방향 프록시 구성에서 작동하지 않습니다. [Kestrel 서버](xref:fundamentals/servers/kestrel)를 사용합니다.

Azure에서 호스트하는 방법에 대한 자세한 내용은 <xref:host-and-deploy/azure-apps/index>를 참조하세요.

## <a name="supported-platforms"></a>지원되는 플랫폼

32비트(x86) 및 64비트(x64) 배포용으로 게시된 앱이 지원됩니다. 앱이 다음과 같지 않은 경우 32비트 앱을 배포하세요.

* 64비트 앱에 사용할 수 있는 더 큰 가상 메모리 주소 공간이 필요합니다.
* 더 큰 IIS 스택 크기가 필요합니다.
* 64비트 네이티브 종속성이 있습니다.

## <a name="application-configuration"></a>애플리케이션 구성

### <a name="enable-the-iisintegration-components"></a>IISIntegration 구성 요소 사용

::: moniker range=">= aspnetcore-2.1"

일반적인 *Program.cs*는 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>를 호출하여 호스트 설정을 시작합니다.

```csharp
public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

일반적인 *Program.cs*는 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>를 호출하여 호스트 설정을 시작합니다.

```csharp
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

**In-process 호스팅 모델**

`CreateDefaultBuilder`는 `UseIIS` 메서드를 호출하여 [CoreCLR](/dotnet/standard/glossary#coreclr)을 부팅하고 IIS 작업자 프로세스(*w3wp.exe* 또는 *iisexpress.exe*) 내에서 앱을 호스트합니다. 성능 테스트의 결과 .NET Core 앱을 in-process로 호스트하는 것이 앱을 out-of-process로 호스트하고 [Kestrel](xref:fundamentals/servers/kestrel) 서버에 대한 요청을 프록시하는 것보다 훨씬 높은 요청 처리량을 제공함을 나타냅니다.

In-process 호스팅 모델은 .NET Framework를 대상으로 하는 ASP.NET Core 앱을 지원하지 않습니다.

**Out-of-process 호스팅 모델**

IIS를 사용한 out-of-process 호스팅의 경우 `CreateDefaultBuilder`는 [Kestrel](xref:fundamentals/servers/kestrel) 서버를 웹 서버로 구성하고 [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)의 기본 경로 및 포트를 구성하여 IIS 통합을 구현합니다.

ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다. `CreateDefaultBuilder`는 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 메서드를 호출합니다. `UseIISIntegration`은 localhost IP 주소(`127.0.0.1`)의 동적 포트에서 수신 대기하도록 Kestrel을 구성합니다. 동적 포트가 1234인 경우 Kestrel은 `127.0.0.1:1234`에서 수신 대기합니다. 이 구성은 다음에서 제공된 다른 URL 구성을 바꿉니다.

* `UseUrls`
* [Kestrel의 수신 대기 API](xref:fundamentals/servers/kestrel#endpoint-configuration)
* [구성](xref:fundamentals/configuration/index)(또는 [명령줄 --urls 옵션](xref:fundamentals/host/web-host#override-configuration))

모듈을 사용하는 경우 `UseUrls` 호출 또는 Kestrel의 `Listen` API가 필요하지 않습니다. `UseUrls` 또는 `Listen`을 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때만 지정된 포트에서 수신 대기합니다.

In-process 및 out-of-process 호스팅 모델에 대한 자세한 내용은 [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module) 및 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.

::: moniker-end

::: moniker range="= aspnetcore-2.1"

`CreateDefaultBuilder`는 [Kestrel](xref:fundamentals/servers/kestrel) 서버를 웹 서버로 구성하고 [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)의 기본 경로 및 포트를 구성하여 IIS 통합을 구현합니다.

ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다. `CreateDefaultBuilder`는 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 메서드를 호출합니다. `UseIISIntegration`은 localhost IP 주소(`127.0.0.1`)의 동적 포트에서 수신 대기하도록 Kestrel을 구성합니다. 동적 포트가 1234인 경우 Kestrel은 `127.0.0.1:1234`에서 수신 대기합니다. 이 구성은 다음에서 제공된 다른 URL 구성을 바꿉니다.

* `UseUrls`
* [Kestrel의 수신 대기 API](xref:fundamentals/servers/kestrel#endpoint-configuration)
* [구성](xref:fundamentals/configuration/index)(또는 [명령줄 --urls 옵션](xref:fundamentals/host/web-host#override-configuration))

모듈을 사용하는 경우 `UseUrls` 호출 또는 Kestrel의 `Listen` API가 필요하지 않습니다. `UseUrls` 또는 `Listen`을 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때만 지정된 포트에서 수신 대기합니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

`CreateDefaultBuilder`는 [Kestrel](xref:fundamentals/servers/kestrel) 서버를 웹 서버로 구성하고 [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)의 기본 경로 및 포트를 구성하여 IIS 통합을 구현합니다.

ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다. `CreateDefaultBuilder`는 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 메서드를 호출합니다. `UseIISIntegration`은 localhost IP 주소(`localhost`)의 동적 포트에서 수신 대기하도록 Kestrel을 구성합니다. 동적 포트가 1234인 경우 Kestrel은 `localhost:1234`에서 수신 대기합니다. 이 구성은 다음에서 제공된 다른 URL 구성을 바꿉니다.

* `UseUrls`
* [Kestrel의 수신 대기 API](xref:fundamentals/servers/kestrel#endpoint-configuration)
* [구성](xref:fundamentals/configuration/index)(또는 [명령줄 --urls 옵션](xref:fundamentals/host/web-host#override-configuration))

모듈을 사용하는 경우 `UseUrls` 호출 또는 Kestrel의 `Listen` API가 필요하지 않습니다. `UseUrls` 또는 `Listen`을 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때만 지정된 포트에서 수신 대기합니다.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) 패키지에 대한 종속성을 앱의 종속성에 포함합니다. <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 확장 메서드를 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>에 추가하여 IIS 통합 미들웨어를 사용합니다.

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .UseIISIntegration()
    ...
```

<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*> 및 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*>이 둘 다 필요합니다. `UseIISIntegration`을 호출하는 코드는 코드 이식성에 영향을 주지 않습니다. 앱이 IIS 배후에서 실행되지 않는 경우(예를 들어 앱이 Kestrel에서 바로 실행되는 경우)에는 `UseIISIntegration`이 작동하지 않습니다.

ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다. `UseIISIntegration`은 localhost IP 주소(`localhost`)의 동적 포트에서 수신 대기하도록 Kestrel을 구성합니다. 동적 포트가 1234인 경우 Kestrel은 `localhost:1234`에서 수신 대기합니다. 이 구성은 다음에서 제공된 다른 URL 구성을 바꿉니다.

* `UseUrls`
* [구성](xref:fundamentals/configuration/index)(또는 [명령줄 --urls 옵션](xref:fundamentals/host/web-host#override-configuration))

모듈을 사용하는 경우 `UseUrls` 호출이 필요하지 않습니다. `UseUrls`를 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때만 지정된 포트에서 수신 대기합니다.

`UseUrls`를 ASP.NET Core 1.0 앱에서 호출하는 경우 모듈 구성 포트를 덮어 쓰지 않도록 `UseIISIntegration`을 호출하기 **전에** 호출합니다. 모듈 설정이 `UseUrls`를 재정의하기 때문에 이 호출 순서는 ASP.NET Core 1.1에서 필요하지 않습니다.

::: moniker-end

호스팅에 대한 자세한 내용은 [ASP.NET Core의 호스트](xref:fundamentals/index#host)를 참조하세요.

### <a name="iis-options"></a>IIS 옵션

::: moniker range=">= aspnetcore-2.2"

**In-process 호스팅 모델**

IIS 서버 옵션을 구성하려면 <xref:Microsoft.AspNetCore.Builder.IISServerOptions>에 대한 서비스 구성을 <xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*>에 포함합니다. 다음 예제에서는 AutomaticAuthentication을 사용하지 않도록 설정합니다.

```csharp
services.Configure<IISServerOptions>(options => 
{
    options.AutomaticAuthentication = false;
});
```

| 옵션                         | 기본 | 설정 |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | `true`인 경우 IIS 서버는 [Windows 인증](xref:security/authentication/windowsauth)에 의해 인증된 `HttpContext.User`를 설정합니다. `false`인 경우 서버는 `HttpContext.User`에 대한 ID만 제공하고, `AuthenticationScheme`에서 명시적으로 요청될 때 챌린지에 응답합니다. IIS에서 Windows 인증은 `AutomaticAuthentication`이 작동하기 위해 사용하도록 설정되어야 합니다. 자세한 내용은 [Windows 인증](xref:security/authentication/windowsauth)을 참조하세요. |
| `AuthenticationDisplayName`    | `null`  | 로그인 페이지에서 사용자에게 나타나는 표시 이름을 설정합니다. |

**Out-of-process 호스팅 모델**

::: moniker-end

IIS 옵션을 구성하려면 <xref:Microsoft.AspNetCore.Builder.IISOptions>에 대한 서비스 구성을 <xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*>에 포함합니다. 다음 예에서는 앱이 `HttpContext.Connection.ClientCertificate`를 채우는 것을 방지합니다.

```csharp
services.Configure<IISOptions>(options => 
{
    options.ForwardClientCertificate = false;
});
```

| 옵션                         | 기본 | 설정 |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | `true`이면 IIS 통합 미들웨어가 [Windows 인증](xref:security/authentication/windowsauth)에 의해 인증된 `HttpContext.User`를 설정합니다. `false`이면 미들웨어가 `HttpContext.User`에게 ID만 제공하고, `AuthenticationScheme`에서 명시적으로 요청될 때 챌린지에 응답합니다. IIS에서 Windows 인증은 `AutomaticAuthentication`이 작동하기 위해 사용하도록 설정되어야 합니다. 자세한 내용은 [Windows 인증](xref:security/authentication/windowsauth) 항목을 참조하세요. |
| `AuthenticationDisplayName`    | `null`  | 로그인 페이지에서 사용자에게 나타나는 표시 이름을 설정합니다. |
| `ForwardClientCertificate`     | `true`  | `true`면서 `MS-ASPNETCORE-CLIENTCERT` 요청 헤더가 있는 경우 `HttpContext.Connection.ClientCertificate`가 채워집니다. |

### <a name="proxy-server-and-load-balancer-scenarios"></a>프록시 서버 및 부하 분산 장치 시나리오

체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소를 전달하도록 전달된 헤더 미들웨어를 구성하는 IIS 통합 미들웨어 및 ASP.NET Core 모듈을 구성합니다. 추가 프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다. 자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.

### <a name="webconfig-file"></a>web.config 파일

*web.config* 파일은 [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)을 구성합니다. *web.config* 파일을 만들고, 변하고, 게시하는 작업은 프로젝트를 게시할 때 MSBuild 대상(`_TransformWebConfig`)에 의해 처리됩니다. 이 대상은 웹 SDK 대상(`Microsoft.NET.Sdk.Web`)에 나타납니다. SDK는 프로젝트 파일을 기반으로 해서 설정됩니다.

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
```

프로젝트에 *web.config* 파일이 없는 경우, [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)을 구성하기 위해 올바른 *processPath* 및 *인수*로 파일이 생성되어 [게시된 출력](xref:host-and-deploy/directory-structure)으로 이동됩니다.

프로젝트에 *web.config* 파일이 있는 경우, ASP.NET Core 모듈을 구성하기 위해 올바른 *processPath* 및 *인수*로 파일이 변환되어 게시된 출력으로 이동됩니다. 변환은 이 파일의 IIS 구성 설정을 수정하지 않습니다.

*web.config* 파일은 활성 IIS 모듈을 제어하는 추가 IIS 구성 설정을 제공할 수 있습니다. ASP.NET Core 앱을 사용하여 요청을 처리할 수 있는 IIS 모듈에 대한 자세한 내용은 [IIS 모듈](xref:host-and-deploy/iis/modules) 항목을 참조하세요.

웹 SDK가 *web.config* 파일을 변환하지 못하게 하려면 프로젝트 파일의 **\<IsTransformWebConfigDisabled>** 속성을 사용합니다.

```xml
<PropertyGroup>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

웹 SDK가 파일을 변환하지 않도록 설정하는 경우 개발자가 *processPath* 및 *인수*를 수동으로 설정해야 합니다. 자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.

### <a name="webconfig-file-location"></a>web.config 파일 위치

[ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)을 올바르게 설정하려면 배포된 앱의 콘텐츠 루트 경로(일반적으로 앱 기본 경로)에 *web.config* 파일이 있어야 합니다. IIS에 제공되는 웹 사이트 실제 경로와 동일한 위치입니다. 웹 배포를 사용하여 여러 앱을 게시하도록 설정하려면 앱의 루트에 *web.config* 파일이 있어야 합니다.

중요한 파일은 *\<assembly>.runtimeconfig.json*, *\<assembly>.xml*(XML 문서 주석) 및 *\<assembly>.deps.json*과 같은 앱의 실제 경로에 있습니다. *web.config* 파일이 있고 사이트가 정상적으로 시작되면 IIS는 이러한 중요한 파일이 요청되어도 제공하지 않습니다. *web.config* 파일이 없거나, 이름이 잘못 지정되었거나, 정상적으로 시작되도록 사이트를 구성할 수 없는 경우 IIS에서 중요한 파일을 공개적으로 제공할 수도 있습니다.

***web.config* 파일이 항상 배포에 있어야 하며, 올바르게 이름이 지정되고, 정상적으로 시작되도록 사이트를 구성할 수 있어야 합니다. 프로덕션 배포에서 *web.config* 파일을 제거하지 마세요.**

### <a name="transform-webconfig"></a>web.config 변환

게시할 때 *web.config*를 변환해야 하는 경우(예: 구성, 프로필 또는 환경을 기반으로 환경 변수 설정) <xref:host-and-deploy/iis/transform-webconfig>를 참조하세요.

## <a name="iis-configuration"></a>IIS 구성

**Windows Server 운영 체제**

**웹 서버(IIS)** 서버 역할을 사용하도록 설정하고 역할 서비스를 설정합니다.

1. **관리** 메뉴 또는 **서버 관리자**의 링크를 통해 **역할 및 기능 추가** 마법사를 사용합니다. **서버 역할** 단계에서 **웹 서버(IIS)** 확인란을 선택합니다.

   ![서버 역할 선택 단계에서 선택된 웹 서버 IIS 역할](index/_static/server-roles-ws2016.png)

1. **기능** 단계 후에는 웹 서버(IIS)에 대한 **역할 서비스** 단계가 로드됩니다. 원하는 IIS 역할 서비스를 선택하거나 제공된 기본 역할 서비스를 적용합니다.

   ![역할 서비스 선택 단계에서 선택된 기본 역할 서비스](index/_static/role-services-ws2016.png)

   **Windows 인증(선택 사항)**  
   Windows 인증을 사용하도록 설정하려면 **웹 서버** > **보안** 노드를 확장합니다. **Windows 인증** 기능을 선택합니다. 자세한 내용은 [Windows 인증 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 및 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.

   **WebSockets(선택 사항)**  
   WebSockets는 ASP.NET Core 1.1 이상에서 지원됩니다. WebSocket을 사용하도록 설정하려면 **웹 서버** > **애플리케이션 개발** 노드를 확장합니다. **WebSocket 프로토콜** 기능을 선택합니다. 자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참고하시기 바랍니다.

1. **확인** 단계를 진행하여 웹 서버 역할 및 서비스를 설치합니다. **웹 서버(IIS)** 역할을 설치한 후에 서버/IIS를 다시 시작할 필요는 없습니다.

**Windows 데스크톱 운영 체제**

**IIS 관리 콘솔** 및 **World Wide Web 서비스**를 사용하도록 설정합니다.

1. **제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.

1. **인터넷 정보 서비스** 노드를 엽니다. **웹 관리 도구** 노드를 엽니다.

1. **IIS 관리 콘솔** 확인란을 선택합니다.

1. **World Wide Web 서비스** 확인란을 선택합니다.

1. **World Wide Web 서비스**의 기본 기능을 그대로 사용하거나 IIS 기능을 사용자 지정합니다.

   **Windows 인증(선택 사항)**  
   Windows 인증을 사용하도록 설정하려면 **World Wide Web 서비스** > **보안** 노드를 확장합니다. **Windows 인증** 기능을 선택합니다. 자세한 내용은 [Windows 인증 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 및 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.

   **WebSockets(선택 사항)**  
   WebSockets는 ASP.NET Core 1.1 이상에서 지원됩니다. WebSocket을 사용하도록 설정하려면 **World Wide Web 서비스** > **애플리케이션 개발 기능** 노드를 확장합니다. **WebSocket 프로토콜** 기능을 선택합니다. 자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참고하시기 바랍니다.

1. IIS 설치 시 다시 시작해야 하는 경우 시스템을 다시 시작합니다.

![Windows 기능에서 선택된 IIS 관리 콘솔 및 World Wide Web 서비스](index/_static/windows-features-win10.png)

## <a name="install-the-net-core-hosting-bundle"></a>.NET Core 호스팅 번들 설치

호스팅 시스템에 *.NET Core 호스팅 번들*을 설치합니다. 번들은 .NET Core 런타임, .NET Core 라이브러리 및 [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)을 설치합니다. 이 모듈을 통해 ASP.NET Core 앱을 IIS 배후에서 실행할 수 있습니다. 시스템이 인터넷에 연결되지 않은 경우 [Microsoft Visual C++ 2015 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=53840)를 설치한 후에 .NET Core 호스팅 번들을 설치합니다.

> [!IMPORTANT]
> IIS 이전에 호스팅 번들이 설치된 경우 번들 설치를 복구해야 합니다. IIS를 설치한 후 호스팅 번들 설치 프로그램을 다시 실행합니다.

### <a name="direct-download-current-version"></a>직접 다운로드(현재 버전)

다음 링크를 사용하여 설치 관리자를 다운로드합니다.

[현재 .NET Core 호스팅 번들 설치 관리자(직접 다운로드)](https://www.microsoft.com/net/permalink/dotnetcore-current-windows-runtime-bundle-installer)

### <a name="earlier-versions-of-the-installer"></a>이전 버전의 설치 관리자

이전 버전의 설치 관리자를 가져오려면:

1. [.NET 다운로드 보관](https://www.microsoft.com/net/download/archives)으로 이동합니다.
1. **.NET Core**에서 .NET Core 버전을 선택합니다.
1. **앱 실행 - 런타임** 열에서 원하는 .NET Core 런타임 버전의 행을 찾습니다.
1. **런타임 및 호스팅 번들** 링크를 사용하여 설치 관리자를 다운로드합니다.

> [!WARNING]
> 일부 설치 관리자는 EOL(수명 종료)에 도달한 릴리스 버전을 포함하고 Microsoft에서 더 이상 지원되지 않습니다. 자세한 내용은 [지원 정책](https://www.microsoft.com/net/download/dotnet-core/2.0)을 참조하세요.

### <a name="install-the-hosting-bundle"></a>호스팅 번들 설치

1. 서버에서 설치 관리자를 실행합니다. 관리자 명령 셸에서 설치 관리자를 실행할 때 다음 매개 변수를 사용할 수 있습니다.

   * `OPT_NO_ANCM=1` &ndash; ASP.NET Core 모듈 설치를 건너뜁니다.
   * `OPT_NO_RUNTIME=1` &ndash; .NET Core 런타임 설치를 건너뜁니다.
   * `OPT_NO_SHAREDFX=1` &ndash; ASP.NET 공유 프레임워크(ASP.NET 런타임) 설치를 건너뜁니다.
   * `OPT_NO_X86=1` &ndash; x86 런타임 설치를 건너뜁니다. 32비트 앱을 호스팅하지 않음을 아는 경우 이 매개 변수를 사용합니다. 향후 32비트와 64비트 앱을 모두 호스트할 수 있는 기회가 있는 경우 이 매개 변수를 사용하지 않고 두 런타임을 모두 설치합니다.
   * `OPT_NO_SHARED_CONFIG_CHECK=1` &ndash; 공유 구성(*applicationHost.config*)이 IIS 설치와 동일한 머신에 있는 경우 IIS 공유 구성 사용 선택을 해제합니다. *ASP.NET Core 2.2 이상 호스팅 번들러 설치 관리자에 대해서만 사용할 수 있습니다.* 자세한 내용은 <xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration>을 참조하세요.
1. 시스템을 다시 시작하거나 명령 셸에서 **net stop was /y**, **net start w3svc**를 차례로 실행합니다. IIS를 다시 시작하면 설치 관리자에서 변경된 시스템 PATH(환경 변수)의 내용이 수집됩니다.

Windows 호스팅 번들 설치 관리자는 설치를 완료하기 위해 IIS를 다시 설정해야 함을 발견하면 IIS를 다시 설정합니다. 설치 관리자가 IIS 다시 설정을 트리거하면 모든 IIS 앱 풀 및 웹 사이트가 다시 시작됩니다.

> [!NOTE]
> IIS 공유 구성에 대한 자세한 내용은 [IIS 공유 구성을 사용하는 ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration)을 참조하세요.

## <a name="install-web-deploy-when-publishing-with-visual-studio"></a>Visual Studio을 사용하여 게시할 때 웹 배포 설치

[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하여 앱을 서버에 배포하는 경우 최신 버전의 웹 배포를 서버에 설치합니다. 웹 배포를 설치하려면 [WebPI(웹 플랫폼 설치 관리자)](https://www.microsoft.com/web/downloads/platform.aspx)를 사용하거나 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=43717)에서 직접 설치 관리자를 가져옵니다. WebPI를 사용하는 것이 좋습니다. WebPI는 호스팅 공급자에 대한 독립 실행형 설치 및 구성을 제공합니다.

## <a name="create-the-iis-site"></a>IIS 사이트 만들기

1. 호스팅 시스템에서 앱의 게시된 폴더 및 파일을 포함할 폴더를 만듭니다. 앱의 배포 레이아웃은 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목에서 설명합니다.

1. IIS 관리자의 **연결** 패널에서 서버 노드를 엽니다. **사이트** 폴더를 마우스 오른쪽 단추로 클릭합니다. 상황에 맞는 메뉴에서 **웹 사이트 추가**를 선택합니다.

1. **사이트 이름**을 제공하고 **실제 경로**를 앱의 배포 폴더로 설정합니다. **바인딩** 구성을 제공하고 **확인**을 선택하여 웹 사이트를 만듭니다.

   ![[웹 사이트 추가] 단계에서 사이트 이름, 실제 경로 및 호스트 이름을 제공합니다.](index/_static/add-website-ws2016.png)

   > [!WARNING]
   > 최상위 와일드카드 바인딩(`http://*:80/` 및 `http://+:80`)을 사용하지 **않아야** 합니다. 최상위 와일드카드 바인딩은 보안 취약점에 앱을 노출시킬 수 있습니다. 강력한 와일드카드와 약한 와일드카드 모두에 적용됩니다. 와일드카드보다는 명시적 호스트 이름을 사용합니다. 전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.mysub.com`)에는 이러한 보안 위험이 없습니다(취약한 `*.com`과 반대임). 자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.

1. 서버 노드에서 **애플리케이션 풀**을 선택합니다.

1. 사이트의 앱 풀을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **기본 설정**을 선택합니다.

1. **애플리케이션 풀 편집** 창에서 **.NET CLR 버전**을 **관리 코드 없음**으로 설정합니다.

   ![.NET CLR 버전에 대해 관리 코드 없음 설정](index/_static/edit-apppool-ws2016.png)

    ASP.NET Core는 별도의 프로세스에서 실행되며 런타임을 관리합니다. ASP.NET Core에서는 데스크톱 CLR을 로드할 필요가 없습니다. **.NET CLR 버전**을 **관리 코드 없음**으로 설정하는 것은 선택 사항입니다.

1. *ASP.NET Core 2.2 이상*: [In-process 호스팅 모델](xref:fundamentals/servers/index#in-process-hosting-model)을 사용하는 64비트(x64) [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd)의 경우 32비트(x86) 프로세스에 대해 앱 풀을 사용하지 않도록 설정합니다.

   IIS 관리자의 **애플리케이션 풀**에 있는 **작업** 사이드바에서 **애플리케이션 풀 기본값 설정** 또는 **고급 설정**을 선택합니다. **32비트 애플리케이션 사용**을 찾아 값을 `False`로 설정합니다. 이 설정은 [독립 프로세스 호스팅](xref:host-and-deploy/aspnet-core-module#out-of-process-hosting-model)에 배포된 앱에 영향을 주지 않습니다.

1. 프로세스 모델 ID에 적절한 권한이 있는지 확인합니다.

   애플리케이션 풀의 기본 ID(**프로세스 모델** > **ID**)가 **ApplicationPoolIdentity**에서 다른 ID로 변경되면, 새 ID에 앱의 폴더, 데이터베이스 및 기타 필요한 리소스에 액세스하는 데 필요한 권한이 있는지 확인합니다. 예를 들어 앱 풀에는 앱이 파일을 읽고 쓰는 폴더에 대한 읽기 및 쓰기 권한이 필요합니다.

**Windows 인증 구성(선택 사항)**  
자세한 내용은 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.

## <a name="deploy-the-app"></a>앱 배포

호스팅 시스템에 만든 폴더에 앱을 배포합니다. [웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)는 배포에 권장되는 메커니즘입니다.

### <a name="web-deploy-with-visual-studio"></a>Visual Studio를 사용한 웹 배포

웹 배포에서 사용할 게시 프로필을 만드는 방법은 [ASP.NET Core 앱 배포용 Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles) 항목을 참조하세요. 호스팅 공급자가 게시 프로필을 제공하거나 게시 프로필을 만들 수 있도록 지원하는 경우 해당 프로필을 다운로드하고 Visual Studio **게시** 대화 상자를 사용하여 가져옵니다.

![게시 대화 상자 페이지](index/_static/pub-dialog.png)

### <a name="web-deploy-outside-of-visual-studio"></a>Visual Studio 외부에서 웹 배포

[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)는 Visual Studio 외부에서 명령줄을 통해 사용할 수도 있습니다. 자세한 내용은 [웹 배포 도구](/iis/publish/using-web-deploy/use-the-web-deployment-tool)를 참조하세요.

### <a name="alternatives-to-web-deploy"></a>웹 배포에 대한 대안

수동 복사, Xcopy, Robocopy, PowerShell 등의 여러 방법 중 하나를 사용하여 앱을 호스팅 시스템으로 이동합니다.

IIS에 ASP.NET Core 배포에 대한 자세한 내용은 [IIS 관리자를 위한 배포 리소스](#deployment-resources-for-iis-administrators) 섹션을 참조하세요.

## <a name="browse-the-website"></a>웹 사이트 찾아보기

![IIS 시작 페이지가 로드된 Microsoft Edge 브라우저](index/_static/browsewebsite.png)

## <a name="locked-deployment-files"></a>배포 파일이 잠겨 있음

앱이 실행 중이면 배포 폴더의 파일이 잠겨 있습니다. 잠긴 파일은 배포 중에 덮어쓸 수 없습니다. 배포에서 잠긴 파일을 해제하려면 다음 방법 중 **하나**를 사용하여 앱 풀을 중지합니다.

* 웹 배포를 사용하고 프로젝트 파일에서 `Microsoft.NET.Sdk.Web`을 참조합니다. *app_offline.htm* 파일은 웹앱 디렉터리의 루트에 배치됩니다. 파일이 있는 경우 ASP.NET Core 모듈은 앱을 정상적으로 종료하고, 배포하는 동안 *app_offline.htm* 파일을 제공합니다. 자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)를 참조하세요.
* 서버의 IIS 관리자에서 앱 풀을 수동으로 중지합니다.
* PowerShell을 사용하여 *app_offline.html*을 삭제합니다(PowerShell 5 이상 필요).

  ```PowerShell
  $pathToApp = 'PATH_TO_APP'

  # Stop the AppPool
  New-Item -Path $pathToApp app_offline.htm

  # Provide script commands here to deploy the app

  # Restart the AppPool
  Remove-Item -Path $pathToApp app_offline.htm

  ```

## <a name="data-protection"></a>데이터 보호

[ASP.NET Core 데이터 보호 스택](xref:security/data-protection/introduction)은 인증에 사용되는 미들웨어를 포함하여 여러 ASP.NET Core [미들웨어](xref:fundamentals/middleware/index)에서 사용됩니다. 사용자 코드에서 데이터 보호 API가 호출되지 않더라도 배포 스크립트 또는 사용자 코드를 통해 영구적 암호화 [키 저장소](xref:security/data-protection/implementation/key-management)를 만들도록 데이터 보호를 구성해야 합니다. 데이터 보호를 구성하지 않으면 키는 메모리에 보관되고 앱이 다시 시작되면 삭제됩니다.

키 링이 메모리에 저장된 경우 앱을 다시 시작하면 다음과 같이 됩니다.

* 모든 쿠키 기반 인증 토큰이 무효화됩니다. 
* 사용자는 다음 요청에서 다시 로그인해야 합니다. 
* 키 링으로 보호된 데이터의 암호를 더 이상 해독할 수 없습니다. 여기에는 [CSRF 토큰](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) 및 [ASP.NET Core MVC TempData 쿠키](xref:fundamentals/app-state#tempdata)가 포함될 수 있습니다.

IIS에서 키 링을 저장하도록 데이터 보호를 구성하려면 다음 방법 중 **하나**를 사용합니다.

* **데이터 보호 레지스트리키 만들기**

  ASP.NET 앱에서 사용되는 데이터 보호 키는 앱 외부의 레지스트리에 저장됩니다. 지정된 앱의 키를 저장하려면 앱 풀에 대한 레지스트리 키를 만듭니다.

  WebFarm이 아닌 독립 실행형 IIS 설치의 경우 [Data Protection Provision-AutoGenKeys.ps1 PowerShell 스크립트](https://github.com/aspnet/AspNetCore/blob/master/src/DataProtection/Provision-AutoGenKeys.ps1)를 ASP.NET Core 앱과 함께 사용되는 각 응용 프로그램 풀에 사용할 수 있습니다. 이 스크립트는 앱의 앱 풀 작업자 프로세스 계정만 액세스할 수 있는 HKLM 레지스트리에 레지스트리 키를 만듭니다. 미사용 키는 컴퓨터 전체 키가 있는 DPAPI를 사용하여 암호화됩니다.

  웹 팜 시나리오에서는 UNC 경로를 사용하여 데이터 보호 키 링을 저장하도록 앱을 구성할 수 있습니다. 기본적으로 데이터 보호 키는 암호화되지 않습니다. 네트워크 공유에 대한 파일 권한은 앱 실행에 사용되는 Windows 계정으로 제한되어야 합니다. X509 인증서를 사용하여 미사용 키를 보호할 수도 있습니다. 사용자가 인증서를 업로드할 수 있는 메커니즘을 사용하는 것이 좋습니다. 즉, 사용자의 신뢰할 수 있는 인증서 저장소에 인증서를 배치하고, 사용자의 앱이 실행되는 모든 머신에서 이 인증서를 사용할 수 있도록 합니다. 자세한 내용은 [ASP.NET Core 데이터 보호 구성](xref:security/data-protection/configuration/overview)을 참조하세요.

* **사용자 프로필을 로드하도록 IIS 애플리케이션 풀 구성**

  이 설정은 앱 풀에 대한 **고급 설정** 아래의 **프로세스 모델** 섹션에 있습니다. **사용자 프로필**을 `True`로 설정합니다. `True`로 설정하면 키가 사용자 프로필 디렉터리에 저장되고, 사용자 계정에 관련된 키가 있는 DPAPI를 사용하여 보호됩니다. 키는 *%LOCALAPPDATA%/ASP.NET/DataProtection-Keys* 폴더에 저장됩니다.

  앱 풀의 [setProfileEnvironment 특성](/iis/configuration/system.applicationhost/applicationpools/add/processmodel#configuration)도 사용하도록 설정해야 합니다. `setProfileEnvironment` 의 기본값은 `true`입니다. Windows OS와 같은 일부 시나리오에서는 `setProfileEnvironment`가 `false`로 설정됩니다. 키가 예상대로 사용자 프로필 디렉터리에 저장되지 않는 경우 다음을 수행합니다.

  1. *%windir%/system32/inetsrv/config* 폴더로 이동합니다.
  1. *applicationHost.config* 파일을 엽니다.
  1. `<system.applicationHost><applicationPools><applicationPoolDefaults><processModel>` 요소를 찾습니다.
  1. `setProfileEnvironment` 특성이 존재하지 않는지 확인합니다. 존재하지 않을 경우 기본값이 `true`로 설정됩니다. 또는 특성 값을 명시적으로 `true`로 설정합니다.

* **파일 시스템을 키 링 저장소로 사용**

  [파일 시스템을 키 링 저장소로 사용](xref:security/data-protection/configuration/overview)하도록 앱 코드를 조정합니다. X509 인증서를 사용하여 키 링을 보호하고 신뢰할 수 있는 인증서인지 확인합니다. 자체 서명된 인증서인 경우 신뢰할 수 있는 루트 저장소에 배치합니다.

  웹 팜에서 IIS를 사용하는 경우 다음을 수행합니다.

  * 모든 컴퓨터에서 액세스할 수 있는 파일 공유를 사용합니다.
  * 각 시스템에 X509 인증서를 배포합니다. [코드에 데이터 보호](xref:security/data-protection/configuration/overview)를 구성합니다.

* **데이터 보호에 대한 컴퓨터 수준 정책 설정**

  데이터 보호 시스템은 데이터 보호 API를 사용하는 모든 앱에 대한 기본 [컴퓨터 수준 정책](xref:security/data-protection/configuration/machine-wide-policy) 설정을 제한적으로 지원합니다. 자세한 내용은 <xref:security/data-protection/introduction>을 참조하세요.

## <a name="virtual-directories"></a>가상 디렉터리

[IIS 가상 디렉터리](/iis/get-started/planning-your-iis-architecture/understanding-sites-applications-and-virtual-directories-on-iis#virtual-directories)는 ASP.NET Core 앱에서 지원되지 않습니다. 앱은 [하위 애플리케이션](#sub-applications)으로 호스팅될 수 있습니다.

## <a name="sub-applications"></a>하위 애플리케이션

ASP.NET Core 앱은 [IIS 하위 애플리케이션(하위 앱)](/iis/get-started/planning-your-iis-architecture/understanding-sites-applications-and-virtual-directories-on-iis#applications)으로 호스팅될 수 있습니다. 하위 앱의 경로는 루트 앱 URL의 일부가 됩니다.

::: moniker range="< aspnetcore-2.2"

하위 앱에는 ASP.NET Core 모듈이 처리기로 포함되지 않아야 합니다. 하위 앱의 *web.config* 파일에 모듈이 처리기로 추가되면, 하위 앱을 찾으려고 할 때 잘못된 구성 파일을 참조하는 *500.19 내부 서버 오류*가 표시됩니다.

다음 예제에서는 ASP.NET Core 하위 앱에 대해 게시된 *web.config* 파일을 보여 줍니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <aspNetCore processPath="dotnet" 
      arguments=".\MyApp.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

ASP.NET Core 앱 아래에 비ASP .NET Core 하위 앱을 호스팅하는 경우, 하위 앱의 *web.config* 파일에서 상속된 처리기를 명시적으로 제거합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <remove name="aspNetCore" />
    </handlers>
    <aspNetCore processPath="dotnet" 
      arguments=".\MyApp.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

하위 앱 내의 정적 자산 링크는 물결표-슬래시(`~/`) 표기법을 사용해야 합니다. 물결표-슬래시 표기법은 [태그 도우미](xref:mvc/views/tag-helpers/intro)를 트리거하여 하위 앱의 PathBase를 렌더링된 상대 링크 앞에 추가합니다. `/subapp_path`에서 하위 앱의 경우, `src="~/image.png"`와 연결된 이미지가 `src="/subapp_path/image.png"`으로 렌더링됩니다. 루트 앱의 정적 파일 미들웨어는 정적 파일 요청을 처리하지 않습니다. 요청은 하위 앱의 정적 파일 미들웨어에서 처리됩니다.

정적 자산의 `src` 특성이 절대 경로(예: `src="/image.png"`)로 설정된 경우 링크는 하위 앱의 PathBase 없이 렌더링됩니다. 루트 앱의 정적 파일 미들웨어는 루트 앱의 [웹 루트](xref:fundamentals/index#web-root)에서 자산을 제공하려고 시도하며, 그 결과 루트 앱에서 정적 자산을 사용할 수 있지 않으면 ‘404 - 찾을 수 없음’이 발생합니다.

ASP.NET Core 앱을 다른 ASP.NET Core 앱에서 하위 앱으로 호스팅하려면 다음을 수행합니다.

1. 하위 앱에 대한 앱 풀을 설정합니다. **.NET CLR 버전**을 **관리 코드 없음**으로 설정합니다.

1. 루트 사이트 아래의 폴더에 하위 앱을 사용하여 IIS 관리자에 루트 사이트를 추가합니다.

1. IIS 관리자에서 하위 앱 폴더를 마우스 오른쪽 단추로 클릭하고 **Convert to Application**(애플리케이션으로 변환)을 선택합니다.

1. **Add Application**(애플리케이션 추가) 대화 상자에서 **애플리케이션 풀**에 대한 **선택** 단추를 사용하여 하위 앱에 대해 만든 앱 풀을 할당합니다. **확인**을 선택합니다.

하위 앱에 대한 별도의 앱 풀 할당은 In-process 호스팅 모델을 사용할 때 필요합니다.

In-process 호스팅 모델 및 ASP.NET Core 모듈 구성에 대한 자세한 내용은 <xref:host-and-deploy/aspnet-core-module> 및 <xref:host-and-deploy/aspnet-core-module>을 참조하세요.

## <a name="configuration-of-iis-with-webconfig"></a>web.config를 사용하여 IIS 구성

IIS 구성은 ASP.NET Core 모듈을 사용하여 ASP.NET Core 앱에 대해 작동하는 IIS 시나리오에서 *web.config*에 포함된 `<system.webServer>` 섹션의 영향을 받습니다. 예를 들어, IIS 구성은 동적 압축에 대해 작동합니다. IIS가 동적 압축을 사용하도록 서버 수준에서 구성된 경우, 앱의 *web.config* 파일에 포함된 `<urlCompression>` 요소가 ASP.NET Core 앱에 대해 이를 비활성화할 수 있습니다.

자세한 내용은 [\<system.webServer>에 대한 구성 참조](/iis/configuration/system.webServer/), [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module) 및 [ASP.NET Core와 IIS 모듈](xref:host-and-deploy/iis/modules)을 참조하세요. 격리된 앱 풀에서 실행되는 개별 앱에 대해 환경 변수를 설정하려면(IIS 10.0 이상에서 지원됨), IIS 참조 문서에서 [환경 변수 \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목의 *AppCmd.exe 명령* 섹션을 참조하세요.

## <a name="configuration-sections-of-webconfig"></a>web.config 구성 섹션

*web.config*에 있는 ASP.NET 4.x 앱의 구성 섹션은 ASP.NET Core 앱의 구성에 사용되지 않습니다.

* `<system.web>`
* `<appSettings>`
* `<connectionStrings>`
* `<location>`

ASP.NET Core 앱은 다른 구성 공급자를 사용하여 구성됩니다. 자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참고하시기 바랍니다.

## <a name="application-pools"></a>애플리케이션 풀

::: moniker range=">= aspnetcore-2.2"

앱 풀 격리는 호스팅 모델에 따라 결정됩니다.

* In-process 호스팅 &ndash; 앱은 별도의 앱 풀에서 실행해야 합니다.
* Out-of-process 호스팅 &ndash; 각 앱을 자체 앱 풀에서 실행하여 앱을 서로 격리하는 것이 좋습니다.

IIS **웹 사이트 추가** 대화 상자는 기본적으로 앱당 단일 앱 풀로 구성됩니다. **사이트 이름**을 제공하면 텍스트가 자동으로 **애플리케이션 풀** 텍스트 상자로 전송됩니다. 사이트를 추가할 때 이 사이트 이름을 사용하여 새로운 앱 풀이 생성됩니다.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

서버에서 여러 웹 사이트를 호스트하는 경우 각 앱을 해당 앱 풀에서 실행하여 서로 격리하는 것이 좋습니다. 이 구성은 IIS **웹 사이트 추가** 대화 상자의 기본값입니다. **사이트 이름**을 제공하면 텍스트가 자동으로 **애플리케이션 풀** 텍스트 상자로 전송됩니다. 사이트를 추가할 때 이 사이트 이름을 사용하여 새로운 앱 풀이 생성됩니다.

::: moniker-end

## <a name="application-pool-identity"></a>애플리케이션 풀 ID

응용 프로그램 풀 ID 계정을 사용하면 도메인 또는 로컬 계정을 만들고 관리할 필요 없이 고유한 계정으로 앱을 실행할 수 있습니다. IIS 8.0 이상에서 IIS WAS(관리 작업자 프로세스)는 새로운 앱 풀의 이름으로 가상 계정을 만들고, 기본적으로 이 계정으로 앱 풀의 작업자 프로세스를 실행합니다. IIS 관리 콘솔의 애플리케이션 풀에 대한 **고급 설정** 아래에서 **ID**가 **ApplicationPoolIdentity**를 사용하도록 설정되어 있는지 확인합니다.

![애플리케이션 풀 고급 설정 대화 상자](index/_static/apppool-identity.png)

IIS 관리 프로세스는 Windows 보안 시스템에 앱 풀 이름이 포함된 보안 식별자를 만듭니다. 리소스는 이 ID를 사용하여 보호할 수 있습니다. 그러나 이 ID는 실제 사용자 계정이 아니며 Windows 사용자 관리 콘솔에 표시되지 않습니다.

IIS 작업자 프로세스에서 앱에 대한 높은 액세스 권한이 필요한 경우 앱이 포함된 디렉터리에 대한 ACL(액세스 제어 목록)을 수정합니다.

1. [Windows 탐색기]를 열고 해당 하위 디렉터리로 이동합니다.

1. 디렉터리를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.

1. **보안** 탭 아래에서 **편집** 단추, **추가** 단추를 차례로 선택합니다.

1. **위치** 단추를 선택하고 시스템이 선택되어 있는지 확인합니다.

1. **선택할 개체 이름 입력** 영역에 **IIS AppPool\\<app_pool_name>** 을 입력합니다. **이름 확인** 단추를 선택합니다. *DefaultAppPool*의 경우 **IIS AppPool\DefaultAppPool**을 사용하는 이름을 확인합니다. **이름 확인** 단추를 선택하면 개체 이름 영역에 **DefaultAppPool** 값이 표시됩니다. 개체 이름 영역에 앱 풀 이름을 직접 입력할 수는 없습니다. 개체 이름을 확인할 때는 **IIS AppPool\\<app_pool_name>** 형식을 사용합니다.

   ![앱 폴더에 대한 사용자 또는 그룹 선택 대화 상자: “이름 확인”을 선택하기 전에 개체 이름 영역의 “IIS AppPool\"에 앱 풀 이름 “DefaultAppPool”이 추가됩니다.](index/_static/select-users-or-groups-1.png)

1. **확인**을 선택합니다.

   ![앱 폴더에 대한 사용자 또는 그룹 선택 대화 상자: “이름 확인”을 선택하면 개체 이름 영역에 개체 이름 “DefaultAppPool”이 표시됩니다.](index/_static/select-users-or-groups-2.png)

1. 읽기 및 실행 권한은 기본적으로 부여됩니다. 필요에 따라 추가 권한을 제공합니다.

**ICACLS** 도구를 사용하여 명령 프롬프트에서 액세스 권한을 부여할 수도 있습니다. *DefaultAppPool*을 예로 들면, 다음 명령이 사용됩니다.

```console
ICACLS C:\sites\MyWebApp /grant "IIS AppPool\DefaultAppPool":F
```

자세한 내용은 [icacls](/windows-server/administration/windows-commands/icacls) 항목을 참조하세요.

## <a name="http2-support"></a>HTTP/2 지원

::: moniker range=">= aspnetcore-2.2"

[HTTP/2](https://httpwg.org/specs/rfc7540.html)는 다음과 같은 IIS 배포 시나리오에서 ASP.NET Core를 통해 지원됩니다.

* In-Process
  * Windows Server 2016/Windows 10 이상, IIS 10 이상
  * TLS 1.2 이상 연결
* Out of Process
  * Windows Server 2016/Windows 10 이상, IIS 10 이상
  * 공용 에지 서버 연결은 HTTP/2를 사용하지만 [Kestrel 서버](xref:fundamentals/servers/kestrel)에 대한 역방향 프록시 연결은 HTTP/1.1을 사용합니다.
  * TLS 1.2 이상 연결

In-Process 배포에서 HTTP/2 연결이 설정된 경우 [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*)에서 `HTTP/2`를 보고합니다. Out of Process 배포에서 HTTP/2 연결이 설정된 경우 [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*)에서 `HTTP/1.1`을 보고합니다.

In-process 및 out-of-process 호스팅 모델에 대한 자세한 내용은 <xref:host-and-deploy/aspnet-core-module> 항목 및 <xref:host-and-deploy/aspnet-core-module> 항목을 참조하세요.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

[HTTP/2](https://httpwg.org/specs/rfc7540.html)는 다음 기본 요구 사항을 충족하는 Out of Process 배포에 대해 지원됩니다.

* Windows Server 2016/Windows 10 이상, IIS 10 이상
* 공용 에지 서버 연결은 HTTP/2를 사용하지만 [Kestrel 서버](xref:fundamentals/servers/kestrel)에 대한 역방향 프록시 연결은 HTTP/1.1을 사용합니다.
* 대상 프레임워크: HTTP/2 연결은 IIS에 의해 완전히 처리되므로 Out of Process 배포에는 해당하지 않습니다.
* TLS 1.2 이상 연결

HTTP/2 연결이 설정된 경우 [HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*)에서 `HTTP/1.1`을 보고합니다.

::: moniker-end

HTTP/2는 기본적으로 사용됩니다. HTTP/2 연결이 설정되지 않은 경우 연결이 HTTP/1.1로 대체됩니다. IIS 배포가 포함된 HTTP/2 구성에 대한 자세한 내용은 [IIS의 HTTP/2](/iis/get-started/whats-new-in-iis-10/http2-on-iis)를 참조하세요.

## <a name="cors-preflight-requests"></a>CORS 실행 전 요청

이 섹션은 .NET Framework를 대상으로 하는 ASP.NET Core 앱에만 적용됩니다.

.NET Framework를 대상으로 하는 ASP.NET Core 앱의 경우 OPTIONS 요청은 IIS에서 기본적으로 앱에 전달되지 않습니다. OPTIONS 요청을 전달하도록 *web.config*에서 앱의 IIS 처리기를 구성하는 방법을 알아보려면 [ASP.NET Web API 2에서 원본 간 요청을 사용하도록 설정: CORS 작동 방식](/aspnet/web-api/overview/security/enabling-cross-origin-requests-in-web-api#how-cors-works)을 참조하세요.

## <a name="deployment-resources-for-iis-administrators"></a>IIS 관리자를 위한 배포 리소스

IIS 설명서에서 IIS에 대해 자세히 알아보세요.  
[IIS 설명서](/iis)

.NET Core 앱 배포 모델에 자세히 알아보세요.  
[.NET Core 애플리케이션 배포](/dotnet/core/deploying/)

ASP.NET Core 모듈이 Kestrel 웹 서버에서 역방향 프록시 서버로 IIS 또는 IIS Express를 어떻게 사용하도록 허용하는지 알아봅니다.  
[ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)

ASP.NET Core 앱을 호스팅하기 위해 ASP.NET Core 모듈을 구성하는 방법을 알아봅니다.  
[ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)

게시된 ASP.NET Core 앱의 디렉터리 구조에 대해 알아봅니다.  
[디렉터리 구조](xref:host-and-deploy/directory-structure)

ASP.NET Core 앱용 활성 및 비활성 IIS 모듈과 IIS 모듈을 관리하는 방법을 살펴봅니다.  
[IIS 모듈](xref:host-and-deploy/iis/troubleshoot)

ASP.NET Core 앱의 IIS 배포에 대한 문제 진단 방법을 알아봅니다.  
[문제 해결](xref:host-and-deploy/iis/troubleshoot)

IIS에서 ASP.NET Core 앱을 호스팅할 때 일반적인 오류를 구분합니다.  
[Azure App Service 및 IIS에 대한 일반적인 오류 참조](xref:host-and-deploy/azure-iis-errors-reference)

## <a name="additional-resources"></a>추가 자료

* <xref:test/troubleshoot>
* [ASP.NET Core 소개](xref:index)
* [공식 Microsoft IIS 사이트](https://www.iis.net/)
* [Windows Server 기술 콘텐츠 라이브러리](/windows-server/windows-server)
* [IIS의 HTTP/2](/iis/get-started/whats-new-in-iis-10/http2-on-iis)
* <xref:host-and-deploy/iis/transform-webconfig>
