---
title: ASP.NET Core 2.0용 Microsoft.AspNetCore.All 메타패키지
author: Rick-Anderson
description: ASP.NET Core 2.1 이상은 Microsoft.AspNetCore.All 메타패키지를 사용하는 것이 좋습니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 10/25/2018
uid: fundamentals/metapackage
ms.openlocfilehash: d95bafd412969bb8db38499bd2ff01af510d872c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064860"
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-20"></a>ASP.NET Core 2.0용 Microsoft.AspNetCore.All 메타패키지

> [!NOTE]
> ASP.NET Core 2.1 이상을 대상으로 하는 애플리케이션은 이 패키지가 아닌 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)를 사용하는 것이 좋습니다. 이 문서의 [Microsoft.AspNetCore.All에서 Microsoft.AspNetCore.App으로 마이그레이션](#migrate)을 참조하세요.

이 기능을 사용하려면 .NET Core 2.x를 대상으로 하는 ASP.NET Core 2.x가 필요합니다.

ASP.NET Core에 대한 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 메타패키지에는 다음 패키지들이 포함되어 있습니다.

* ASP.NET Core 팀에서 지원되는 모든 패키지
* Entity Framework Core에서 지원되는 모든 패키지
* ASP.NET Core 및 Entity Framework Core에서 사용되는 내부 및 타사 종속성

ASP.NET Core 2.x 및 Entity Framework Core 2.x의 모든 기능은 `Microsoft.AspNetCore.All` 패키지에 포함됩니다. ASP.NET Core 2.0을 대상으로 하는 기본 프로젝트 템플릿에는 이 패키지를 사용합니다.

`Microsoft.AspNetCore.All` 메타패키지의 버전 번호는 ASP.NET Core 버전 및 Entity Framework Core 버전을 나타냅니다.

`Microsoft.AspNetCore.All` 메타패키지를 사용하는 애플리케이션은 [.NET Core 런타임 저장소](/dotnet/core/deploying/runtime-store)를 자동으로 활용합니다. 런타임 저장소에는 ASP.NET Core 2.x 애플리케이션을 실행하는 데 필요한 모든 런타임 자산이 포함됩니다. `Microsoft.AspNetCore.All` 메타패키지를 사용할 경우, 참조되는 ASP.NET Core NuGet 패키지의 자산이 애플리케이션을 사용하여 배포되지 **않습니다**. 이러한 자산은 &mdash; .NET Core 런타임 저장소에 포함됩니다. 런타임 저장소의 자산은 애플리케이션 시작 시간 단축을 위해 미리 컴파일됩니다.

패키지 트리밍 프로세스를 이용하여 사용하지 않는 패키지를 제거할 수 있습니다. 트리밍된 패키지는 게시된 애플리케이션 출력에서 제외됩니다.

다음 *.csproj* 파일은 ASP.NET Core용 `Microsoft.AspNetCore.All` 메타패키지를 참조합니다.

[!code-xml[](metapackage/samples/Metapackage.All.Example.csproj?highlight=8)]

::: moniker range=">= aspnetcore-2.1"

## <a name="implicit-versioning"></a>암시적 버전 관리

ASP.NET Core 2.1 이상에서는 버전 없이 `Microsoft.AspNetCore.All` 패키지 참조를 지정할 수 있습니다. 버전이 지정되지 않은 경우 SDK(`Microsoft.NET.Sdk.Web`)에 의해 암시적 버전이 지정됩니다. SDK에서 지정하는 암시적 버전을 사용하고, 패키지 참조에 버전 번호를 명시적으로 설정하지 않는 것이 좋습니다. 이 방법에 대한 질문이 있는 경우 GitHub의 [Microsoft.AspNetCore.App 암시적 버전에 대한 토론](https://github.com/aspnet/Docs/issues/6430)에 의견을 남겨 주세요.

휴대용 앱의 암시적 버전은 `major.minor.0`으로 설정됩니다. 공유 프레임워크 롤포워드 메커니즘은 설치된 공유 프레임워크 중 최신 호환 버전에서 앱을 실행합니다. 개발, 테스트 및 프로덕션에서 동일한 버전이 사용되도록 하려면 모든 환경에 동일한 버전의 공유 프레임워크를 설치하도록 하세요. 자체 포함 앱의 경우 암시적 버전 번호가 설치된 SDK에 포함된 공유 프레임워크의 `major.minor.patch`로 설정됩니다.

`Microsoft.AspNetCore.All` 패키지 참조에 버전 번호를 지정해도 해당 버전의 고유 프레임워크가 선택된다고 보장할 수 **없습니다**. 예를 들어 "2.1.1" 버전을 지정했는데 "2.1.3"이 설치되는 경우가 있습니다. 이 경우 앱은 "2.1.3"을 사용합니다. 권장되는 방법은 아니지만 롤포워드를 비활성화할 수 있습니다(패치 및/또는 부 버전). DotNet 호스트 롤포워드 및 이 동작을 구성하는 방법에 대한 자세한 내용은 [DotNet 호스트 롤포워드](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md)를 참조하세요.

`Microsoft.AspNetCore.All`의 암시적 버전을 사용하려면 프로젝트의 SDK를 프로젝트 파일의 `Microsoft.NET.Sdk.Web`으로 설정해야 합니다. `Microsoft.NET.Sdk` SDK를 지정하면(프로젝트 파일의 맨 위에 있는 `<Project Sdk="Microsoft.NET.Sdk">`) 다음 경고가 생성됩니다.

*경고 NU1604: 프로젝트 종속성 Microsoft.AspNetCore.All는 경계값을 포함 하지 않습니다. 일관된 복원 결과를 얻으려면 종속 버전의 하한을 포함하세요.*

이는 .NET Core 2.1 SDK의 알려진 문제이며 .NET Core 2.2 SDK에서 수정될 예정입니다.

::: moniker-end

<a name="migrate"></a>

## <a name="migrating-from-microsoftaspnetcoreall-to-microsoftaspnetcoreapp"></a>Microsoft.AspNetCore.All에서 Microsoft.AspNetCore.App으로 마이그레이션

`Microsoft.AspNetCore.All`에는 다음 패키지가 포함되어 있지만 `Microsoft.AspNetCore.App` 패키지는 포함되어 있지 않습니다.

* `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServices.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServicesIntegration`
* `Microsoft.AspNetCore.DataProtection.AzureKeyVault`
* `Microsoft.AspNetCore.DataProtection.AzureStorage`
* `Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv`
* `Microsoft.AspNetCore.SignalR.Redis`
* `Microsoft.Data.Sqlite`
* `Microsoft.Data.Sqlite.Core`
* `Microsoft.EntityFrameworkCore.Sqlite`
* `Microsoft.EntityFrameworkCore.Sqlite.Core`
* `Microsoft.Extensions.Caching.Redis`
* `Microsoft.Extensions.Configuration.AzureKeyVault`
* `Microsoft.Extensions.Logging.AzureAppServices`
* `Microsoft.VisualStudio.Web.BrowserLink`

앱이 이전 패키지 또는 이러한 패키지에서 가져온 패키지의 API를 사용하는 경우 `Microsoft.AspNetCore.All`에서 `Microsoft.AspNetCore.App`으로 전환하려면 프로젝트에 이러한 패키지에 대한 참조를 추가합니다.

`Microsoft.AspNetCore.App`의 종속성이 아닌 이전 패키지의 종속성은 암시적으로 포함되지 않습니다. 예를 들어:

* `Microsoft.Extensions.Caching.Redis`의 종속성 `StackExchange.Redis`
* `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`의 종속성 `Microsoft.ApplicationInsights`

## <a name="update-aspnet-core-21"></a>ASP.NET Core 2.1 업데이트

2.1 이상의 경우 `Microsoft.AspNetCore.App` 메타패키지로 마이그레이션하는 것이 좋습니다. `Microsoft.AspNetCore.All` 메타패키지를 계속 사용하고 최신 패치 버전이 배포되었는지 확인하려면:

* 개발 컴퓨터 및 빌드 서버: 최신 설치 [.NET Core SDK](https://www.microsoft.com/net/download)합니다.
* 배포 서버: 최신 설치 [.NET Core 런타임](https://www.microsoft.com/net/download)합니다.
 애플리케이션을 다시 시작하면 앱이 최신 설치 버전으로 롤포워드됩니다.
