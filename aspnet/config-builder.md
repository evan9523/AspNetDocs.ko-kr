---
uid: config-builder
title: ASP.NET용 구성 빌더
author: rick-anderson
description: 외부 원본에서 web.config 값 이외의 원본에서 구성 데이터를 가져오는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 7/17/2020
msc.type: content
ms.openlocfilehash: 1f95efcceb2ecf33fece12174cecf65cd8b27675
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424795"
---
# <a name="configuration-builders-for-aspnet"></a>ASP.NET용 구성 빌더

[Stephen Molloy](https://github.com/StephenMolloy) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

구성 빌더는 ASP.NET apps가 외부 원본에서 구성 값을 가져올 수 있는 최신 및 agile 메커니즘을 제공 합니다.

구성 빌더:

* .NET Framework 4.7.1 이상에서 사용할 수 있습니다.
* 구성 값을 읽기 위한 유연한 메커니즘을 제공 합니다.
* 컨테이너 및 클라우드 중심 환경으로 이동 하는 앱의 기본 요구 사항 중 일부를 해결 합니다.
* 를 사용 하 여 .NET 구성 시스템에서 이전에 사용할 수 없는 소스 (예: Azure Key Vault 및 환경 변수)를 그려서 구성 데이터의 보호를 향상할 수 있습니다.

## <a name="keyvalue-configuration-builders"></a>키/값 구성 빌더

구성 작성기에서 처리할 수 있는 일반적인 시나리오는 키/값 패턴을 따르는 구성 섹션에 대 한 기본 키/값 대체 메커니즘을 제공 하는 것입니다. ConfigurationBuilders의 .NET Framework 개념은 특정 구성 섹션 또는 패턴으로 제한 되지 않습니다. 그러나 `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders))의 많은 구성 빌더가 키/값 패턴 내에서 작동 합니다.

## <a name="keyvalue-configuration-builders-settings"></a>키/값 구성 작성기 설정

다음 설정은의 모든 키/값 구성 작성기에 적용 `Microsoft.Configuration.ConfigurationBuilders` 됩니다.

### <a name="mode"></a>Mode

구성 작성기는 키/값 정보의 외부 소스를 사용 하 여 구성 시스템의 선택 된 키/값 요소를 채웁니다. 특히 `<appSettings/>` 및 섹션은 `<connectionStrings/>` 구성 빌더에서 특별 한 처리를 받습니다. 빌더는 다음과 같은 세 가지 모드에서 작동 합니다.

* `Strict`-기본 모드입니다. 이 모드에서 구성 빌더는 잘 알려진 키/값 중심 구성 섹션 에서만 작동 합니다. `Strict`모드 섹션의 각 키를 열거 합니다. 외부 원본에 일치 하는 키가 있는 경우:

   * 구성 빌더는 결과 구성 섹션의 값을 외부 원본의 값으로 바꿉니다.
* `Greedy`-이 모드는 모드와 밀접 하 게 관련 되어 `Strict` 있습니다. 원래 구성에 이미 있는 키로 제한 되지 않습니다.

  * 구성 빌더는 외부 소스의 모든 키/값 쌍을 결과 구성 섹션에 추가 합니다.

* `Expand`-구성 섹션 개체로 구문 분석 하기 전에 원시 XML에서 작동 합니다. 문자열에서 토큰을 확장 하는 것으로 간주할 수 있습니다. 패턴과 일치 하는 원시 XML 문자열의 모든 부분은 `${token}` 토큰 확장의 후보가 됩니다. 외부 원본에 해당 하는 값이 없으면 토큰이 변경 되지 않습니다. 이 모드의 빌더는 및 섹션으로 제한 되지 않습니다 `<appSettings/>` `<connectionStrings/>` .

*web.config* 에서 다음 태그를 사용 하면 환경 [configbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) 를 모드에서 사용할 수 있습니다 `Strict` .

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

다음 코드는 앞의 `<appSettings/>` `<connectionStrings/>` *web.config* 파일에 나와 있는을 읽습니다.

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

위의 코드에서는 속성 값을로 설정 합니다.

* 환경 변수에 키가 설정 되지 않은 경우 *web.config* 파일의 값입니다.
* 환경 변수의 값입니다 (설정 된 경우).

예를 `ServiceID` 들어에는 다음이 포함 됩니다.

* 환경 변수가 `ServiceID` 설정 되지 않은 경우 "ServiceID value from web.config"
* 환경 변수의 값입니다 `ServiceID` (설정 된 경우).

다음 이미지는 `<appSettings/>` 환경 편집기에 설정 된 이전 *web.config* 파일의 키/값을 보여 줍니다.

![환경 편집기](config-builder/static/env.png)

참고: 환경 변수의 변경 내용을 확인 하려면 Visual Studio를 종료 하 고 다시 시작 해야 할 수 있습니다.

### <a name="prefix-handling"></a>접두사 처리

키 접두사는 다음과 같은 경우 키 설정을 간소화할 수 있습니다.

* .NET Framework 구성은 복잡 하 고 중첩 됩니다.
* 외부 키/값 원본은 일반적으로 기본 이며 본질적으로 플랫입니다. 예를 들어 환경 변수는 중첩 되지 않습니다.

다음 방법 중 하나를 사용 하 여 `<appSettings/>` 환경 변수를 통해 및를 구성에 삽입할 수 `<connectionStrings/>` 있습니다.

* `EnvironmentConfigBuilder`기본 모드의와 `Strict` 구성 파일에 적절 한 키 이름을 사용 합니다. 위의 코드와 태그는이 방법을 사용 합니다. 이 방법을 사용 하면와 모두에 동일한 이름의 키를 사용할 수 **없습니다** `<appSettings/>` `<connectionStrings/>` .
* 모드에서는 두 개의를 `EnvironmentConfigBuilder` `Greedy` 고유 접두사와 함께 사용 `stripPrefix` 합니다. 이 접근 방식을 사용 하 여 앱은 `<appSettings/>` `<connectionStrings/>` 구성 파일을 업데이트할 필요 없이 읽을 수 있습니다. 다음 섹션인 [stripPrefix](#stripprefix)는이 작업을 수행 하는 방법을 보여 줍니다.
* `EnvironmentConfigBuilder` `Greedy` 서로 다른 접두사를 사용 하 여 모드에서 두 s를 사용 합니다. 이 방법에서는 키 이름이 접두사와 달라 야 하므로 중복 키 이름을 가질 수 없습니다.  예를 들어:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

위의 태그를 사용 하 여 동일한 플랫 키/값 소스를 사용 하 여 두 개의 다른 섹션에 대 한 구성을 채울 수 있습니다.

다음 이미지는 `<appSettings/>` `<connectionStrings/>` 환경 편집기에 설정 된 이전 *web.config* 파일의 및 키/값을 보여 줍니다.

![환경 편집기](config-builder/static/prefix.png)

다음 코드는 `<appSettings/>` `<connectionStrings/>` 이전 *web.config* 파일에 포함 된 및 키/값을 읽습니다.

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

위의 코드에서는 속성 값을로 설정 합니다.

* 환경 변수에 키가 설정 되지 않은 경우 *web.config* 파일의 값입니다.
* 환경 변수의 값입니다 (설정 된 경우).

예를 들어 이전 *web.config* 파일, 이전 환경 편집기 이미지의 키/값, 이전 코드를 사용 하는 경우 다음 값이 설정 됩니다.

|  키              | 값 |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | Env 변수에서 AppSetting_ServiceID|
|    AppSetting_default            | Env의 AppSetting_default 값 |
|       ConnStr_default         | Env에서 ConnStr_default val|

### <a name="stripprefix"></a>stripPrefix

`stripPrefix`: 부울, 기본값은 `false` 입니다. 

이전 XML 태그는 응용 프로그램 설정을 연결 문자열에서 분리 하지만 *web.config* 파일의 모든 키가 지정 된 접두사를 사용 해야 합니다. 예를 들어 접두사는 `AppSetting` `ServiceID` 키 ("AppSetting_ServiceID")에 추가 되어야 합니다. 에서 `stripPrefix` 접두사는 *web.config* 파일에서 사용 되지 않습니다. 구성 작성기 원본 (예: 환경)에는 접두사가 필요 합니다. 대부분의 개발자가를 사용 하 게 될 것으로 예상 `stripPrefix` 합니다.

응용 프로그램은 일반적으로 접두사를 제거 합니다. 다음 *web.config* 는 접두사를 제거 합니다.

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

위의 *web.config* 파일에서 `default` 키는 및에 모두 `<appSettings/>` `<connectionStrings/>` 있습니다.

다음 이미지는 `<appSettings/>` `<connectionStrings/>` 환경 편집기에 설정 된 이전 *web.config* 파일의 및 키/값을 보여 줍니다.

![환경 편집기](config-builder/static/prefix.png)

다음 코드는 `<appSettings/>` `<connectionStrings/>` 이전 *web.config* 파일에 포함 된 및 키/값을 읽습니다.

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

위의 코드에서는 속성 값을로 설정 합니다.

* 환경 변수에 키가 설정 되지 않은 경우 *web.config* 파일의 값입니다.
* 환경 변수의 값입니다 (설정 된 경우).

예를 들어 이전 *web.config* 파일, 이전 환경 편집기 이미지의 키/값, 이전 코드를 사용 하는 경우 다음 값이 설정 됩니다.

|  키              | 값 |
| ----------------- | ------------ |
|     ServiceID           | Env 변수에서 AppSetting_ServiceID|
|    기본값            | Env의 AppSetting_default 값 |
|    기본값         | Env에서 ConnStr_default val|

### <a name="tokenpattern"></a>tokenPattern

`tokenPattern`: 문자열, 기본값:`@"\$\{(\w+)\}"`

`Expand`작성기의 동작은 원시 XML에서 처럼 보이는 토큰을 검색 합니다 `${token}` . 검색은 기본 정규식을 사용 하 여 수행 됩니다 `@"\$\{(\w+)\}"` . 와 일치 하는 문자 집합은 `\w` XML 보다 엄격 하 고 많은 구성 소스에서 허용 됩니다. `tokenPattern`토큰 이름에 필요한 것 보다 많은 문자를 사용 `@"\$\{(\w+)\}"` 합니다.

`tokenPattern`문자열

* 개발자가 토큰 일치에 사용 되는 regex를 변경할 수 있습니다.
* 잘 구성 된 위험한 regex 인지 확인 하기 위해 유효성 검사가 수행 되지 않습니다.
* 캡처 그룹을 포함 해야 합니다. 전체 regex는 전체 토큰과 일치 해야 합니다. 첫 번째 캡처는 구성 소스에서 조회할 토큰 이름 이어야 합니다.

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>Microsoft.Configuration.ConfigurationBuilders의 구성 빌더

### <a name="environmentconfigbuilder"></a>환경 Configbuilder

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

환경 [Configbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):

* 는 가장 간단한 구성 빌더입니다.
* 환경에서 값을 읽습니다.
* 에는 추가 구성 옵션이 없습니다.
* `name`특성 값은 임의입니다.

**참고:** Windows 컨테이너 환경에서 런타임에 설정 된 변수는 EntryPoint 프로세스 환경에만 삽입 됩니다. 서비스 또는 비 EntryPoint 프로세스로 실행 되는 앱은 컨테이너의 메커니즘을 통해 다른 방식으로 삽입 되지 않는 한 이러한 변수를 선택 하지 않습니다. [IIS](https://github.com/Microsoft/iis-docker/pull/41) / [ASP.NET](https://github.com/Microsoft/aspnet-docker)기반 컨테이너의 경우 현재 버전의 [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) 는 *DefaultAppPool* 에서만이를 처리 합니다. 다른 Windows 기반 컨테이너 변형은 진입점이 아닌 프로세스에 대 한 자체 삽입 메커니즘을 개발 해야 할 수 있습니다.

### <a name="usersecretsconfigbuilder"></a>UserSecretsConfigBuilder

> [!WARNING]
> 소스 코드에는 암호, 중요 한 연결 문자열 또는 기타 중요 한 데이터를 저장 하지 마세요. 프로덕션 암호는 개발 또는 테스트에 사용 하면 안 됩니다.

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

이 구성 작성기는 [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets)와 유사한 기능을 제공 합니다.

.NET Framework 프로젝트에서 [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) 를 사용할 수 있지만 비밀 파일을 지정 해야 합니다. 또는 `UserSecretsId` 프로젝트 파일에서 속성을 정의 하 고 읽을 수 있도록 올바른 위치에 원시 비밀 파일을 만들 수 있습니다. 외부 종속성을 프로젝트 외부로 유지 하기 위해 비밀 파일은 XML 형식입니다. XML 서식 지정은 구현 세부 정보 이며,이 형식은에 의존해 서는 안 됩니다. .NET Core 프로젝트를 사용 하 여 파일 *에secrets.js* 를 공유 해야 하는 경우 [SimpleJsonConfigBuilder](#simplejsonconfigbuilder)를 사용 하는 것이 좋습니다. `SimpleJsonConfigBuilder`또한 .Net Core의 형식은 변경 될 수 있는 구현 세부 정보로 간주 되어야 합니다.

구성 특성 `UserSecretsConfigBuilder` :

* `userSecretsId`-XML 암호 파일을 식별 하는 데 선호 되는 방법입니다. 이는 프로젝트 속성을 사용 하 여이 식별자를 저장 하는 .NET Core와 유사 하 게 작동 `UserSecretsId` 합니다. 문자열은 고유 해야 하며 GUID가 아니어도 됩니다. 이 특성을 사용 하 여 `UserSecretsConfigBuilder` `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` 이 식별자에 속하는 비밀 파일에 대해 잘 알려진 로컬 위치 ()를 확인 합니다.
* `userSecretsFile`-암호를 포함 하는 파일을 지정 하는 선택적 특성입니다. `~`문자는 응용 프로그램 루트를 참조 하는 시작 부분에서 사용할 수 있습니다. 이 특성 또는 `userSecretsId` 특성이 필요 합니다. 둘 다 지정 하면가 `userSecretsFile` 우선적으로 적용 됩니다.
* `optional`: boolean, default value `true` -암호 파일을 찾을 수 없는 경우 예외를 방지 합니다. 
* `name`특성 값은 임의입니다.

비밀 파일의 형식은 다음과 같습니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>AzureKeyVaultConfigBuilder

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) 는 [Azure Key Vault](/azure/key-vault/key-vault-whatis)에 저장 된 값을 읽습니다.

`vaultName`필요 합니다 (자격 증명 모음의 이름 또는 자격 증명 모음에 대 한 URI). 다른 특성은 연결할 자격 증명 모음에 대 한 제어를 허용 하지만 응용 프로그램이에서 작동 하는 환경에서 실행 되 고 있지 않은 경우에만 필요 합니다 `Microsoft.Azure.Services.AppAuthentication` . Azure 서비스 인증 라이브러리는 가능 하면 실행 환경에서 연결 정보를 자동으로 선택 하는 데 사용 됩니다. 연결 문자열을 제공 하 여 자동으로 연결 정보를 선택할 수 있습니다.

* `vaultName`-이 `uri` 제공 되지 않은 경우 필요 합니다. 키/값 쌍을 읽을 Azure 구독의 자격 증명 모음 이름을 지정 합니다.
* `connectionString`- [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support) 에서 사용할 수 있는 연결 문자열
* `uri`-지정 된 값을 사용 하 여 다른 Key Vault 공급자에 연결 `uri` 합니다. 지정 하지 않으면 Azure ( `vaultName` )는 자격 증명 모음 공급자입니다.
* `version`-Azure Key Vault는 암호에 대 한 버전 관리 기능을 제공 합니다. 을 `version` 지정 하면 작성기는이 버전과 일치 하는 암호만 검색 합니다.
* `preloadSecretNames`-기본적으로이 빌더는 초기화 될 때 key vault의 **모든** 키 이름을 querys 합니다. 모든 키 값을 읽지 않으려면이 특성을로 설정 `false` 합니다. 이를로 설정 `false` 하면 한 번에 하나씩 비밀을 읽습니다. 자격 증명 모음에서 "Get" 액세스를 허용 하지만 "목록" 액세스를 허용 하지 않는 경우 암호를 한 번에 하나씩 읽는 것이 유용할 수 있습니다. **참고:** `Greedy`모드를 사용 하 `preloadSecretNames` 는 경우은 `true` (기본값) 여야 합니다.

### <a name="keyperfileconfigbuilder"></a>KeyPerFileConfigBuilder

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) 는 디렉터리의 파일을 값의 원본으로 사용 하는 기본 구성 작성기입니다. 파일 이름은 키 이며 콘텐츠는 값입니다. 이 구성 작성기는 오케스트레이션 컨테이너 환경에서 실행할 때 유용할 수 있습니다. Docker Swarm 및 Kubernetes와 같은 시스템 `secrets` 은이 파일을 기준으로이 키로 해당 오케스트레이션 windows 컨테이너를 제공 합니다.

특성 정보:

* `directoryPath` - 필수입니다. 값을 찾을 경로를 지정 합니다. Windows용 Docker 암호는 기본적으로 *C:\ProgramData\Docker\secrets* 디렉터리에 저장 됩니다.
* `ignorePrefix`-이 접두사로 시작 하는 파일은 제외 됩니다. 기본값은 “무시”입니다.
* `keyDelimiter`-기본값은 `null` 입니다. 지정 된 경우 구성 빌더는 디렉터리의 여러 수준을 트래버스하 고이 구분 기호를 사용 하 여 키 이름을 작성 합니다. 이 값이 이면 `null` 구성 빌더는 디렉터리의 최상위 수준만 확인 합니다.
* `optional`-기본값은 `false` 입니다. 원본 디렉터리가 없는 경우 구성 작성기에서 오류를 발생 시켜야 하는지 여부를 지정 합니다.

### <a name="simplejsonconfigbuilder"></a>SimpleJsonConfigBuilder

> [!WARNING]
> 소스 코드에는 암호, 중요 한 연결 문자열 또는 기타 중요 한 데이터를 저장 하지 마세요. 프로덕션 암호는 개발 또는 테스트에 사용 하면 안 됩니다.

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

.NET Core 프로젝트는 일반적으로 구성에 JSON 파일을 사용 합니다. [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder를 사용 하면 .NET Core JSON 파일을 .NET Framework에서 사용할 수 있습니다. 이 구성 작성기는 플랫 키/값 원본에서 .NET Framework 구성의 특정 키/값 영역으로의 기본 매핑을 제공 합니다. 이 구성 작성기는 계층적 구성을 제공 **하지** 않습니다. JSON 지원 파일은 복합 계층적 개체가 아닌 사전과 유사 합니다. 다중 수준 계층 파일을 사용할 수 있습니다. 이 공급자 `flatten` 는를 구분 기호로 사용 하 여 각 수준에 속성 이름을 추가 하 여 깊이 `:` 입니다.

특성 정보:

* `jsonFile` - 필수입니다. 읽을 JSON 파일을 지정 합니다. `~`문자는 앱 루트를 참조 하는 시작 부분에서 사용할 수 있습니다.
* `optional`-부울, 기본값은 `true` 입니다. JSON 파일을 찾을 수 없는 경우 예외를 throw 하지 않습니다.
* `jsonMode` - `[Flat|Sectional]`. 기본값은 `Flat`입니다. `jsonMode`가 이면 `Flat` JSON 파일은 단일 플랫 키/값 원본입니다. `EnvironmentConfigBuilder`및는 `AzureKeyVaultConfigBuilder` 단일 플랫 키/값 원본 이기도 합니다. `SimpleJsonConfigBuilder`가 모드로 구성 된 경우 `Sectional` :

  * JSON 파일은 개념적으로 최상위 수준 에서만 여러 사전으로 나뉩니다.
  * 각 사전은 연결 된 최상위 속성 이름과 일치 하는 구성 섹션에만 적용 됩니다. 예를 들어:

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="configuration-builders-order"></a>구성 작성기 순서

[Aspnet/MicrosoftConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub 리포지토리에서 [Configurationbuilders 실행 순서](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution) 를 확인 합니다.

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>사용자 지정 키/값 구성 작성기 구현

구성 빌더가 요구를 충족 하지 않는 경우 사용자 지정 항목을 작성할 수 있습니다. `KeyValueConfigBuilder`기본 클래스는 대체 모드와 대부분의 접두사 문제를 처리 합니다. 구현 프로젝트에는 다음만 필요 합니다.

* 기본 클래스에서 상속 하 고 및을 통해 키/값 쌍의 기본 소스를 구현 합니다 `GetValue` `GetAllValues` .
* 프로젝트에 [urationBuildersMicrosoft.Configuration.Config](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) 를 추가 합니다.

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

`KeyValueConfigBuilder`기본 클래스는 키/값 구성 작성기에서 많은 작업과 일관 된 동작을 제공 합니다.

## <a name="additional-resources"></a>추가 자료

* [구성 빌더 GitHub 리포지토리](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [.NET을 사용 하 여 Azure Key Vault에 대 한 서비스 간 인증](/azure/key-vault/service-to-service-authentication#connection-string-support)
