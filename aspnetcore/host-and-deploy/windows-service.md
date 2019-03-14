---
title: Windows 서비스에서 ASP.NET Core 호스트
author: guardrex
description: Windows 서비스에서 ASP.NET Core 앱을 호스트하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/13/2019
uid: host-and-deploy/windows-service
ms.openlocfilehash: 081a631c9c3e74c01e15f4b0b272d650c162bd20
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031290"
---
# <a name="host-aspnet-core-in-a-windows-service"></a>Windows 서비스에서 ASP.NET Core 호스트

작성자: [Luke Latham](https://github.com/guardrex) 및 [Tom Dykstra](https://github.com/tdykstra)

IIS를 사용하지 않고 Windows에서 ASP.NET Core 앱을 [Windows 서비스](/dotnet/framework/windows-services/introduction-to-windows-service-applications)로 호스트할 수 있습니다. Windows Service로 호스팅되는 앱은 재부팅 후 자동으로 시작됩니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="deployment-type"></a>배포 유형

프레임워크 종속 또는 자체 포함 Windows 서비스 배포를 만들 수 있습니다. 배포 시나리오에 대한 자세한 내용은 [.NET Core 애플리케이션 배포](/dotnet/core/deploying/)를 참조하세요.

### <a name="framework-dependent-deployment"></a>프레임워크 종속 배포

FDD(프레임워크 종속 배포)에서는 대상 시스템에 .NET Core의 공유 시스템 차원 버전이 있어야 합니다. ASP.NET Core Windows 서비스 앱과 함께 FDD 시나리오를 사용하는 경우 SDK에서 *프레임워크 종속 실행 파일*이라는 실행 파일(*\*.exe*)을 생성합니다.

### <a name="self-contained-deployment"></a>자체 포함 배포

SCD(자체 포함 배포)에서는 대상 시스템에 공유 구성 요소가 없어도 됩니다. 런타임 및 앱의 종속성이 앱과 함께 호스팅 시스템에 배포됩니다.

## <a name="convert-a-project-into-a-windows-service"></a>프로젝트를 Windows 서비스로 변환

기존 ASP.NET Core 프로젝트를 다음과 같이 변경하여 앱을 서비스로 실행합니다.

### <a name="project-file-updates"></a>프로젝트 파일 업데이트

선택한 [배포 유형](#deployment-type)에 따라 프로젝트 파일을 업데이트합니다.

#### <a name="framework-dependent-deployment-fdd"></a>FDD(프레임워크 종속 배포)

대상 프레임워크가 포함된 `<PropertyGroup>`에 Windows [RID(런타임 식별자)](/dotnet/core/rid-catalog)를 추가합니다. 다음 예제에서는 RID가 `win7-x64`로 설정됩니다. `<SelfContained>` 속성을 `false`로 설정하여 추가합니다. 이러한 속성은 SDK가 Windows용 실행 파일(*.exe*)을 생성하도록 지시합니다.

ASP.NET Core 앱을 게시할 때 일반적으로 생성되는 *web.config* 파일은 Windows 서비스 앱에 필요하지 않습니다. *web.config* 파일이 생성되지 않도록 하려면 `<IsTransformWebConfigDisabled>` 속성을 `true`로 설정합니다.

::: moniker range=">= aspnetcore-2.2"

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <SelfContained>false</SelfContained>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

::: moniker-end

::: moniker range="= aspnetcore-2.1"

`<UseAppHost>` 속성을 `true`로 설정하여 추가합니다. 이 속성은 서비스에 FDD의 활성화 경로(실행 파일, *.exe*)를 제공합니다.

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.1</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <UseAppHost>true</UseAppHost>
  <SelfContained>false</SelfContained>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

::: moniker-end

#### <a name="self-contained-deployment-scd"></a>SCD(자체 포함 배포)

Windows [RID(런타임 식별자)](/dotnet/core/rid-catalog)가 있는지 확인하거나, 대상 프레임워크가 포함된 `<PropertyGroup>`에 RID를 추가합니다. `<IsTransformWebConfigDisabled>` 속성을 `true`로 설정하여 추가하면 *web.config* 파일이 생성되지 않습니다.

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp2.2</TargetFramework>
  <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

여러 개의 RID를 게시하려면

* 세미콜론으로 구분된 목록으로 RID를 제공합니다.
* 속성 이름 `<RuntimeIdentifiers>`(복수)를 사용합니다.

  자세한 내용은 [.NET Core RID 카탈로그](/dotnet/core/rid-catalog)를 참조하세요.

[Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices)에 패키지 참조를 추가합니다.

Windows 이벤트 로그 로깅을 사용하도록 설정하려면 [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog)에 대한 패키지 참조를 추가합니다.

자세한 내용은 [시작 및 중지 이벤트 처리](#handle-starting-and-stopping-events) 섹션을 참조하세요.

### <a name="programmain-updates"></a>Program.Main 업데이트

`Program.Main`에서 다음과 같이 변경합니다.

* 서비스 외부에서 실행할 때 테스트 및 디버그하려면 앱이 서비스 또는 콘솔 앱으로 실행되고 있는지 확인하는 코드를 추가합니다. 디버거가 연결되었는지 또는 `--console` 명령줄 인수가 있는지 검사합니다.

  두 조건 중 하나라도 true이면(앱이 서비스로 실행되지 않음) 웹 호스트에 대해 <xref:Microsoft.AspNetCore.Hosting.WebHostExtensions.Run*>을 호출합니다.

  두 조건이 모두 false이면(앱이 서비스로 실행됨) 다음을 수행합니다.

  * <xref:System.IO.Directory.SetCurrentDirectory*>를 호출하고 앱의 게시 위치에 대한 경로를 사용합니다. <xref:System.IO.Directory.GetCurrentDirectory*>를 호출하는 경우 Windows 서비스 앱이 *C:\\WINDOWS\\system32* 폴더를 반환하므로 경로를 얻기 위해 <xref:System.IO.Directory.GetCurrentDirectory*>를 호출하지는 마세요. 자세한 내용은 [현재 디렉터리 및 콘텐츠 루트](#current-directory-and-content-root) 섹션을 참조하세요.
  * <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>를 호출하여 앱을 서비스로 실행합니다.

  [명령줄 구성 공급자](xref:fundamentals/configuration/index#command-line-configuration-provider)에는 명령줄 인수에 대한 이름-값 쌍이 필요하므로 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>가 수신하기 전에 `--console` 스위치가 인수에서 제거됩니다.

* Windows 이벤트 로그에 기록하려면 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder.ConfigureLogging*>에 EventLog 공급자를 추가합니다. *appsettings.Production.json* 파일에서 `Logging:LogLevel:Default` 키를 사용하여 로깅 수준을 설정합니다. 데모 및 테스트 목적으로, 샘플 앱의 프로덕션 설정 파일에서는 로깅 수준이 `Information`으로 설정됩니다. 프로덕션에서 이 값은 일반적으로 `Error`로 설정됩니다. 자세한 내용은 <xref:fundamentals/logging/index#windows-eventlog-provider>을 참조하세요.

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=snippet_Program)]

### <a name="publish-the-app"></a>앱 게시

[dotnet publish](/dotnet/articles/core/tools/dotnet-publish), [Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles) 또는 Visual Studio Code를 사용하여 앱을 게시합니다. Visual Studio를 사용하는 경우 **FolderProfile**을 선택하고 **대상 위치**를 구성한 후 **게시** 단추를 선택합니다.

CLI(명령줄 인터페이스) 도구를 사용하여 샘플 앱을 게시하려면 [-c|--configuration](/dotnet/core/tools/dotnet-publish#options) 옵션에 릴리스 구성을 전달하여 프로젝트 폴더의 명령 프롬프트에서 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령을 실행합니다. 앱 외부 폴더에 게시하려면 [-o|--output](/dotnet/core/tools/dotnet-publish#options) 옵션에 경로를 사용합니다.

#### <a name="publish-a-framework-dependent-deployment-fdd"></a>FDD(프레임워크 종속 배포) 게시

다음 예제에서는 앱이 *c:\\svc* 폴더에 게시됩니다.

```console
dotnet publish --configuration Release --output c:\svc
```

#### <a name="publish-a-self-contained-deployment-scd"></a>SCD(자체 포함 배포) 게시

프로젝트 파일의 `<RuntimeIdenfifier>`(또는 `<RuntimeIdentifiers>`) 속성에 RID를 지정해야 합니다. `dotnet publish` 명령의 [-r|--runtime](/dotnet/core/tools/dotnet-publish#options) 옵션에 런타임을 제공합니다.

다음 예제에서는 앱이 `win7-x64` 런타임의 *c:\\svc* 폴더에 게시됩니다.

```console
dotnet publish --configuration Release --runtime win7-x64 --output c:\svc
```

### <a name="create-a-user-account"></a>사용자 계정 만들기

관리 명령 셸에서 `net user` 명령을 사용하여 서비스에 대한 사용자 계정을 만듭니다.

```console
net user {USER ACCOUNT} {PASSWORD} /add
```

기본 암호 만료는 6주입니다.

샘플 앱의 경우, 이름이 `ServiceUser`인 사용자 계정과 암호를 만듭니다. 다음 명령에서 `{PASSWORD}`를 [강력한 암호](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements)로 바꿉니다.

```console
net user ServiceUser {PASSWORD} /add
```

그룹에 사용자를 추가해야 하는 경우 `net localgroup` 명령을 사용합니다. 여기서 `{GROUP}`은 그룹의 이름입니다.

```console
net localgroup {GROUP} {USER ACCOUNT} /add
```

자세한 내용은 [서비스 사용자 계정](/windows/desktop/services/service-user-accounts)을 참조하세요.

Active Directory를 사용할 때 사용자를 관리하는 대체 방법은 관리 서비스 계정을 사용하는 것입니다. 자세한 내용은 [그룹 관리 서비스 계정 개요](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview)를 참조하세요.

### <a name="set-permissions"></a>권한 설정

#### <a name="access-to-the-app-folder"></a>앱 폴더 액세스

관리 명령 셸에서 [icacls](/windows-server/administration/windows-commands/icacls) 명령을 사용하여 앱 폴더에 대한 쓰기/읽기/실행 액세스 권한을 부여합니다.

```console
icacls "{PATH}" /grant {USER ACCOUNT}:(OI)(CI){PERMISSION FLAGS} /t
```

* `{PATH}` &ndash; 앱의 폴더에 대한 경로입니다.
* `{USER ACCOUNT}` &ndash; 사용자 계정(SID)입니다.
* `(OI)` &ndash; 개체 상속 플래그는 권한을 하위 파일에 전파합니다.
* `(CI)` &ndash; 컨테이너 상속 플래그는 권한을 하위 폴더에 전파합니다.
* `{PERMISSION FLAGS}` &ndash; 앱의 액세스 권한을 설정합니다.
  * 쓰기(`W`)
  * 읽기(`R`)
  * 실행(`X`)
  * 전체(`F`)
  * 수정(`M`)
* `/t` &ndash; 기존 하위 폴더 및 파일에 재귀적으로 적용합니다.

*c:\\svc* 폴더에 게시된 샘플 앱과 쓰기/읽기/실행 권한이 있는 `ServiceUser` 계정의 경우 다음 명령을 사용합니다.

```console
icacls "c:\svc" /grant ServiceUser:(OI)(CI)WRX /t
```

자세한 내용은 [icacls](/windows-server/administration/windows-commands/icacls)를 참조하세요.

#### <a name="log-on-as-a-service"></a>서비스로 로그온

사용자 계정에 [서비스로 로그온](/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) 권한을 부여하려면 다음을 수행합니다.

1. 로컬 보안 정책 콘솔 또는 로컬 그룹 정책 편집기 콘솔에서 **사용자 권한 할당** 정책을 찾습니다. 자세한 지침은 다음을 참조하십시오. [보안 정책 설정을 구성](/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings)합니다.
1. `Log on as a service` 정책을 찾습니다. 정책을 두 번 클릭하여 엽니다.
1. **사용자 또는 그룹 추가**를 선택합니다.
1. **고급**을 선택하고 **지금 찾기**를 선택합니다.
1. 이전에 [사용자 계정 만들기](#create-a-user-account) 섹션에서 만든 사용자 계정을 선택합니다. **확인**을 선택하여 선택을 적용합니다.
1. 개체 이름이 올바른지 확인한 후 **확인**을 선택합니다.
1. **적용**을 선택합니다. **확인**을 선택하여 정책 창을 닫습니다.

## <a name="manage-the-service"></a>서비스 관리

### <a name="create-the-service"></a>서비스 만들기

[sc.exe](https://technet.microsoft.com/library/bb490995) 명령줄 도구를 사용하여 관리 명령줄 셸에서 서비스를 만듭니다. `binPath` 값은 실행 파일 이름을 포함하는 앱의 실행 파일 경로입니다. **각 매개 변수의 등호 및 인용 문자 값 사이에 공백이 필요합니다.**

```console
sc create {SERVICE NAME} binPath= "{PATH}" obj= "{DOMAIN}\{USER ACCOUNT}" password= "{PASSWORD}"
```

* `{SERVICE NAME}` &ndash; [서비스 제어 관리자](/windows/desktop/services/service-control-manager)의 서비스에 할당하는 이름입니다.
* `{PATH}` &ndash; 서비스 실행 파일의 경로입니다.
* `{DOMAIN}` &ndash; 도메인 가입 머신의 도메인입니다. 도메인에 가입되지 않은 머신의 경우 로컬 머신 이름을 사용합니다.
* `{USER ACCOUNT}` &ndash; 서비스 실행에 사용되는 사용자 계정입니다.
* `{PASSWORD}` &ndash; 사용자 계정 암호입니다.

> [!WARNING]
> `obj` 매개 변수를 생략하지 **마세요**. `obj`의 기본값은 [LocalSystem 계정](/windows/desktop/services/localsystem-account) 계정입니다. `LocalSystem` 계정으로 서비스를 실행하면 상당한 보안 위험이 발생합니다. 항상 제한된 권한을 가진 사용자 계정으로 서비스를 실행하세요.

샘플 앱에 대한 예제는 다음과 같습니다.

* 서비스의 이름은 **MyService**입니다.
* 게시된 서비스는 *c:\\svc* 폴더에 있습니다. 앱 실행 파일의 이름은 *SampleApp.exe*입니다. `binPath` 값을 큰따옴표(")로 묶습니다.
* 서비스는 `ServiceUser` 계정으로 실행됩니다. `{DOMAIN}`을 사용자 계정의 도메인 또는 로컬 머신 이름으로 바꿉니다. `obj` 값을 큰따옴표(")로 묶습니다. 예제: 호스팅 시스템이 `MairaPC`라는 로컬 머신인 경우 `obj`를 `"MairaPC\ServiceUser"`로 설정합니다.
* `{PASSWORD}`를 사용자 계정의 암호로 바꿉니다. `password` 값을 큰따옴표(")로 묶습니다.

```console
sc create MyService binPath= "c:\svc\sampleapp.exe" obj= "{DOMAIN}\ServiceUser" password= "{PASSWORD}"
```

> [!IMPORTANT]
> 매개 변수의 등호와 매개 변수의 값 사이에 공백이 있는지 확인합니다.

### <a name="start-the-service"></a>서비스 시작

`sc start {SERVICE NAME}` 명령을 사용하여 서비스를 시작합니다.

샘플 앱 서비스를 시작하려면 다음 명령을 사용합니다.

```console
sc start MyService
```

명령은 서비스를 시작하는 데 몇 초 정도 걸립니다.

### <a name="determine-the-service-status"></a>서비스 상태 확인

서비스 상태를 확인하려면 `sc query {SERVICE NAME}` 명령을 사용합니다. 상태는 다음 값 중 하나로 보고됩니다.

* `START_PENDING`
* `RUNNING`
* `STOP_PENDING`
* `STOPPED`

다음 명령을 사용하여 샘플 앱 서비스의 상태를 확인합니다.

```console
sc query MyService
```

### <a name="browse-a-web-app-service"></a>웹앱 서비스 찾아보기

이 서비스가 `RUNNING` 상태이며 서비스가 웹앱인 경우 해당 경로에서 앱을 찾습니다(기본적으로 `http://localhost:5000`이며 [HTTPS 리디렉션 미들웨어](xref:security/enforcing-ssl)를 사용하는 경우 `https://localhost:5001`로 리디렉션함).

샘플 앱 서비스의 경우 `http://localhost:5000`에서 앱을 찾아봅니다.

### <a name="stop-the-service"></a>서비스를 중지하여

`sc stop {SERVICE NAME}` 명령을 사용하여 서비스를 중지합니다.

다음 명령은 샘플 앱 서비스를 중지합니다.

```console
sc stop MyService
```

### <a name="delete-the-service"></a>서비스 삭제

서비스를 중지하는 짧은 지연 후에 `sc delete {SERVICE NAME}` 명령을 사용하여 서비스를 제거합니다.

샘플 앱 서비스의 상태를 확인합니다.

```console
sc query MyService
```

이 샘플 앱 서비스가 `STOPPED` 상태인 경우 다음 명령을 사용하여 샘플 앱 서비스를 제거합니다.

```console
sc delete MyService
```

## <a name="handle-starting-and-stopping-events"></a>시작 및 중지 이벤트 처리

<xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarting*>, <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStarted*> 및 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService.OnStopping*> 이벤트를 처리하려면 추가로 다음과 같이 변경합니다.

1. `OnStarting`, `OnStarted` 및 `OnStopping` 메서드를 사용하여 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostService>에서 파생되는 클래스를 만듭니다.

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=snippet_CustomWebHostService)]

2. `CustomWebHostService`를 <xref:System.ServiceProcess.ServiceBase.Run*>에 전달하는 <xref:Microsoft.AspNetCore.Hosting.IWebHost>에 대한 확장 메서드를 만듭니다.

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. `Program.Main`에서 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*> 대신 `RunAsCustomService` 확장 메서드를 호출합니다.

   ```csharp
   host.RunAsCustomService();
   ```

   `Program.Main`에서 <xref:Microsoft.AspNetCore.Hosting.WindowsServices.WebHostWindowsServiceExtensions.RunAsService*>의 위치를 확인하려면 [프로젝트를 Windows 서비스로 변환](#convert-a-project-into-a-windows-service) 섹션에 표시된 코드 샘플을 참조하세요.

## <a name="proxy-server-and-load-balancer-scenarios"></a>프록시 서버 및 부하 분산 장치 시나리오

인터넷 또는 회사 네트워크의 요청과 상호 작용하고 프록시 또는 부하 분산 장치 뒤에 있는 서비스에는 추가 구성이 필요합니다. 자세한 내용은 <xref:host-and-deploy/proxy-load-balancer>을 참조하세요.

## <a name="configure-https"></a>HTTPS 구성

보안 엔드포인트로 서비스를 구성하려면 다음을 수행합니다.

1. 플랫폼의 인증서 획득 및 배포 메커니즘을 사용하여 호스팅 시스템에 대한 X.509 인증서를 만듭니다.

1. [Kestrel 서버 HTTPS 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 지정하여 인증서를 사용합니다.

서비스 엔드포인트를 보호하기 위해 ASP.NET Core HTTPS 개발 인증서 사용은 지원되지 않습니다.

## <a name="current-directory-and-content-root"></a>현재 디렉터리 및 콘텐츠 루트

Windows 서비스에 대해 <xref:System.IO.Directory.GetCurrentDirectory*>를 호출하여 반환된 현재 작업 디렉터리는 *C:\\WINDOWS\\system32* 폴더입니다. *system32* 폴더는 서비스의 파일(예: 설정 파일)을 저장을 저장하는 데 적절한 위치가 아닙니다. 다음 방법 중 하나를 사용하여 서비스의 자산 및 설정 파일을 유지 관리하고 액세스합니다.

### <a name="set-the-content-root-path-to-the-apps-folder"></a>콘텐츠 루트 경로를 앱 폴더로 설정

<xref:Microsoft.Extensions.Hosting.IHostingEnvironment.ContentRootPath*>는 서비스가 만들어질 때 `binPath` 인수에 제공된 동일한 경로입니다. `GetCurrentDirectory`를 호출하여 설정 파일의 경로를 만드는 대신, 앱의 콘텐츠 루트 경로를 사용하여 <xref:System.IO.Directory.SetCurrentDirectory*>를 호출합니다.

`Program.Main`에서 서비스 실행 파일의 폴더 경로를 확인하고 이 경로를 사용하여 앱의 콘텐츠 루트를 설정합니다.

```csharp
var pathToExe = Process.GetCurrentProcess().MainModule.FileName;
var pathToContentRoot = Path.GetDirectoryName(pathToExe);
Directory.SetCurrentDirectory(pathToContentRoot);

CreateWebHostBuilder(args)
    .Build()
    .RunAsService();
```

### <a name="store-the-services-files-in-a-suitable-location-on-disk"></a>디스크의 적합한 위치에 서비스 파일을 저장합니다.

파일이 포함된 폴더로 <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder>를 사용하는 경우 <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*>를 통해 절대 경로를 지정합니다.

## <a name="additional-resources"></a>추가 자료

* [Kestrel 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)(HTTPS 구성 및 SNI 지원 포함)
* <xref:fundamentals/host/web-host>
* <xref:test/troubleshoot>
