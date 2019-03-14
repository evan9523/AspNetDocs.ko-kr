---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: 인증 및 ASP.NET Web API에서에서 권한 부여 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에 인증 및 권한 부여의 일반적인 개요를 제공합니다.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a78606a74b2149e68e3b01f4fe204f4a13edf4b5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039100"
---
<a name="authentication-and-authorization-in-aspnet-web-api"></a>인증 및 ASP.NET Web API에서에서 권한 부여
====================
[Mike Wasson](https://github.com/MikeWasson)

웹 API를 만들었지만 이제에 대 한 액세스를 제어 하려고 합니다. 이 연재 기사의 권한 없는 사용자 로부터 웹 API를 보호 하기 위한 몇 가지 옵션에 살펴보겠습니다. 이 시리즈에서는 인증 및 권한 부여를 모두 설명 합니다.

- *인증* 사용자의 id를 아는 것입니다. 예를 들어 alice가 자신의 사용자 이름과 암호를 로그인 및 서버 암호를 사용 하 여 Alice를 인증 하 합니다.
- *권한 부여* 사용자 작업을 수행할 수 있는지 여부를 결정 하는 것입니다. 예를 들어 Alice는 리소스를 가져오지만 리소스를 만들 권한이 있습니다.

시리즈의 첫 번째 기사는 ASP.NET Web API에서 인증 및 권한 부여의 일반적인 개요를 제공합니다. 다른 항목 웹 API에 대 한 일반적인 인증 시나리오를 설명합니다.

> [!NOTE]
> 이 시리즈를 검토 하 고 소중한 피드백을 제공 하는 사람들에 게 감사 드립니다. Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken 합니다.


## <a name="authentication"></a>인증

Web API 호스트에서 발생 하는 인증을 가정 합니다. 웹 호스팅에 대 한 호스트가 인증에 대 한 HTTP 모듈을 사용 하는 IIS입니다. IIS 또는 ASP.NET에 기본 제공 인증 모듈 중 하나를 사용 하도록 프로젝트를 구성할 수도 있고 사용자 지정 인증을 수행 하도록 사용자 고유의 HTTP 모듈을 작성할 수 있습니다.

호스트에서 사용자를 인증 하는 경우 생성을 *주체*, 되는 [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) 코드가 실행 되는 보안 컨텍스트를 나타내는 개체입니다. 호스트를 현재 스레드에서 보안 주체를 설정 하 여 연결 **Thread.CurrentPrincipal**합니다. 연결 된 보안 주체가 포함 **Identity** 사용자에 대 한 정보를 포함 하는 개체입니다. 사용자가 인증 하는 경우는 **Identity.IsAuthenticated** 속성이 반환 **true**합니다. 익명 요청에 대 한 **IsAuthenticated** 반환 **false**합니다. 보안 주체에 대 한 자세한 내용은 참조 하세요. [역할 기반 보안](https://msdn.microsoft.com/library/shz8h065.aspx)합니다.

### <a name="http-message-handlers-for-authentication"></a>인증에 대 한 HTTP 메시지 처리기

인증에 대 한 호스트를 사용 하는 대신 인증 논리를 넣을 수 있습니다는 [HTTP 메시지 처리기](../advanced/http-message-handlers.md)합니다. 이런 경우 메시지 처리기는 HTTP 요청을 검사 하 고 보안 주체를 설정 합니다.

인증에 대 한 메시지 처리기를 사용 해야는 경우 절충은 다음과 같습니다.

- HTTP 모듈은 ASP.NET 파이프라인을 통과 하는 모든 요청을 볼 수 있습니다. 메시지 처리기는 Web API 요청 에서만 볼 수 있습니다.
- 특정 경로 인증 체계를 적용할 수 있는 경로 당 메시지 처리기를 설정할 수 있습니다.
- HTTP 모듈 IIS와 관련이 있습니다. 메시지 처리기 호스트 중립적 되므로 웹 호스팅 및 자체 호스팅을 사용 하 여 사용할 수 있습니다.
- HTTP 모듈은 IIS 로깅, 감사 등에 참여 합니다.
- HTTP 모듈 파이프라인의 이전 실행합니다. 메시지 처리기에서 인증을 처리 하는 경우에 처리기가 실행 가져오기 주 설정지 않습니다. 또한 응답 메시지 처리기를 벗어나면에 이전 주 서버 보안 주체가 되돌립니다.

일반적으로 자체 호스팅을 지원 하기 위해 필요 하지 않으면, HTTP 모듈은 더 나은 옵션입니다. 자체 호스팅을 지원 해야 할 경우 메시지 처리기를 것이 좋습니다.

### <a name="setting-the-principal"></a>보안 주체를 설정합니다.

사용자 지정 인증 논리를 수행 하는 응용 프로그램을 두 위치에서 보안 주체가 설정 해야 합니다.

- **Thread.CurrentPrincipal**. 이 속성은.NET의 스레드 보안 주체를 설정 하는 표준 방법입니다.
- **HttpContext.Current.User**. 이 속성은 ASP.NET에 대 한 합니다.

다음 코드는 보안 주체를 설정 하는 방법을 보여 줍니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

웹 호스팅을 위한; 양쪽 모두에서 보안 주체를 설정 해야 합니다. 그렇지 않은 경우 보안 컨텍스트는 일관 되지 않은 될 수 있습니다. 그러나 자체 호스팅, **HttpContext.Current** null입니다. 코드는 호스트-알 수 있도록 따라서 null 확인을 할당 하기 전에 **HttpContext.Current**표시 된 것 처럼 합니다.

## <a name="authorization"></a>권한 부여

파이프라인에서 나중에 발생 하는 권한 부여 컨트롤러에 가까운 합니다. 기능을 사용 하면 리소스에 대 한 액세스 권한을 부여 하면 더 세분화 된 항목을 선택할 수 있습니다.

- *권한 부여 필터* 컨트롤러 작업 보다 먼저 실행 합니다. 요청 받지 않은 필터 오류 응답을 반환 하 고 작업 호출 되지 않습니다.
- 컨트롤러 작업 내에서 현재 주 서버를 가져올 수 있습니다 합니다 **ApiController.User** 속성입니다. 예를 들어, 해당 사용자에 게 속하는 리소스에만 반환 합니다. 사용자 이름을 기반으로 하는 리소스의 목록을 필터링 할 수 있습니다.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>사용 하 여 [권한 부여] 특성

기본 제공 권한 부여 필터를 제공 하는 web API [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)합니다. 이 필터는 사용자가 인증 되었는지 여부를 확인 합니다. 그렇지 않은 경우 다음 작업을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)를 반환 합니다.

컨트롤러 수준에서 전역으로 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.

**전역적으로**: 모든 Web API 컨트롤러에 대 한 액세스를 제한 하려면 추가 합니다 **AuthorizeAttribute** 필터를 전역 필터 목록:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**컨트롤러**: 특정 컨트롤러에 대 한 액세스를 제한 하려면 필터 특성으로 컨트롤러에 추가 합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**작업**: 특정 작업에 대 한 액세스를 제한 하려면 동작 메서드에 특성을 추가:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

컨트롤러를 제한 한 다음 사용 하 여 특정 작업에 대 한 익명 액세스를 허용 하는 또는 `[AllowAnonymous]` 특성입니다. 다음 예제에서는 `Post` 메서드는 제한 되지만 `Get` 익명 액세스를 허용 하는 메서드.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

이전 예제에서는 필터는 제한 된 메서드를 액세스 하려면 인증 된 모든 사용자를 수 있습니다. 익명 사용자만 유지 됩니다. 특정 역할에 사용자 또는 특정 사용자에 게 액세스를 제한할 수도 있습니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> 합니다 **AuthorizeAttribute** Web API 컨트롤러에 대 한 필터에는 **System.Web.Http** 네임 스페이스입니다. MVC 컨트롤러에 대 한 유사한 필터를 **System.Web.Mvc** 네임 스페이스에 Web API 컨트롤러와 호환 되지 않습니다.


### <a name="custom-authorization-filters"></a>사용자 지정 권한 부여 필터

사용자 지정 권한 부여 필터를 작성 하려면 이러한 형식 중 하나에서 파생 됩니다.

- **AuthorizeAttribute**. 현재 사용자 및 사용자의 역할 기반 권한 부여 논리를 수행 하려면이 클래스를 확장 합니다.
- **AuthorizationFilterAttribute**. 현재 사용자 또는 역할에 기반 하지 않는 동기 권한 부여 논리를 수행 하려면이 클래스를 확장 합니다.
- **IAuthorizationFilter**. 비동기 권한 부여 논리를 수행 하려면이 인터페이스를 구현 합니다. 예를 들어, 권한 부여 논리에 비동기 I/O 또는 네트워크 호출을 하는 경우. (사용자 권한 부여 논리 CPU 바인딩된 경우 것이 더 간단를 파생할 **AuthorizationFilterAttribute**이므로 다음 비동기 메서드를 작성할 필요가 없습니다.)

다음 다이어그램의 클래스 계층 구조를 표시 합니다 **AuthorizeAttribute** 클래스입니다.

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>내부 컨트롤러 작업 권한 부여

경우에 따라 계속 되지만 원칙을 기반으로 동작을 변경 하는 요청을 허용할 수도 있습니다. 예를 들어, 정보를 반환 하는 사용자의 역할에 따라 변경 될 수 있습니다. 컨트롤러 메서드 내에서 현재 주 서버를 가져올 수 있습니다 합니다 **ApiController.User** 속성입니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
