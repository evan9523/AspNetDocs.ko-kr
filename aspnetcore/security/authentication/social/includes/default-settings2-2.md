---
ms.openlocfilehash: 733a41a76e289f8aed6ec2d246ed720e44808fec
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57182763"
---
에 대 한 호출 [AddIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.addidentity) 기본 체계 설정을 구성 합니다. 합니다 [AddAuthentication(String)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_String_) 집합 오버 로드는 [DefaultScheme](/dotnet/api/microsoft.aspnetcore.authentication.authenticationoptions.defaultscheme) 속성입니다. 합니다 [AddAuthentication (동작&lt;AuthenticationOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Authentication_AuthenticationOptions__) 오버 로드를 통해 다양 한 용도 대 한 기본 인증 체계를 설정 하려면 사용할 수 있는 인증 옵션을 구성 합니다. 에 대 한 후속 호출 `AddAuthentication` 이전에 구성 재정의 [AuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions) 속성입니다.

[AuthenticationBuilder](/dotnet/api/microsoft.aspnetcore.authentication.authenticationbuilder) 인증 처리기를 등록 하는 확장 메서드 수만 수 마다 한 번씩 호출 인증 체계입니다. 오버 로드를 사용 하 여 스키마 속성, 스키마 이름, 구성을 허용 하 고 표시 이름 수 있는 합니다.
