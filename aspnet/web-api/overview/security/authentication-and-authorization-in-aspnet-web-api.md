---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API의 인증 및 권한 부여 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API의 인증 및 권한 부여에 대 한 일반적인 개요를 제공 합니다.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345622"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>ASP.NET Web API의 인증 및 권한 부여

[Mike Wasson](https://github.com/MikeWasson)

Web API를 만들었지만 이제이에 대 한 액세스를 제어 하려고 합니다. 이 문서 시리즈에서는 권한이 없는 사용자 로부터 web API를 보호 하기 위한 몇 가지 옵션을 살펴보겠습니다. 이 시리즈는 인증 및 권한 부여를 모두 다룹니다.

- *인증* 에서 사용자의 id를 알고 있습니다. 예를 들어 Alice는 자신의 사용자 이름과 암호를 사용 하 여 로그인 하 고, 서버는 암호를 사용 하 여 Alice를 인증 합니다.
- *권한 부여* 는 사용자가 작업을 수행할 수 있는지 여부를 결정 합니다. 예를 들어 Alice에 게는 리소스를 가져올 수 있는 권한이 있지만 리소스를 만들 수는 없습니다.

시리즈의 첫 번째 문서에서는 ASP.NET Web API의 인증 및 권한 부여에 대 한 일반적인 개요를 제공 합니다. 다른 항목에서는 Web API에 대 한 일반적인 인증 시나리오에 대해 설명 합니다.

> [!NOTE]
> 이 시리즈를 검토 하 고 소중한 의견을 제공 해 주셔서 감사 합니다. Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.

## <a name="authentication"></a>인증

Web API는 호스트에서 인증이 발생 한다고 가정 합니다. 웹 호스팅의 경우 호스트는 인증을 위해 HTTP 모듈을 사용 하는 IIS입니다. IIS 또는 ASP.NET에 기본 제공 되는 인증 모듈을 사용 하도록 프로젝트를 구성 하거나 사용자 지정 인증을 수행 하는 사용자 고유의 HTTP 모듈을 작성할 수 있습니다.

호스트는 사용자를 인증할 때 코드가 실행 되는 보안 컨텍스트를 나타내는 [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) 개체인 보안 *주체*를 만듭니다. 호스트는 **system.threading.thread.currentprincipal**를 설정 하 여 현재 스레드에 보안 주체를 연결 합니다. 보안 주체는 사용자에 대 한 정보를 포함 하는 연결 된 **id** 개체를 포함 합니다. 사용자가 인증 되 면 **Identity. isauthenticated** 속성은 **true**를 반환 합니다. 익명 요청의 경우 **Isauthenticated** 는 **false**를 반환 합니다. 보안 주체에 대 한 자세한 내용은 [역할 기반 보안](https://msdn.microsoft.com/library/shz8h065.aspx)을 참조 하세요.

### <a name="http-message-handlers-for-authentication"></a>인증에 대 한 HTTP 메시지 처리기

인증을 위해 호스트를 사용 하는 대신 [HTTP 메시지 처리기](../advanced/http-message-handlers.md)에 인증 논리를 추가할 수 있습니다. 이 경우 메시지 처리기는 HTTP 요청을 검사 하 고 보안 주체를 설정 합니다.

인증에 메시지 처리기를 사용 해야 하는 경우는 언제 인가요? 몇 가지 장단점은 다음과 같습니다.

- HTTP 모듈은 ASP.NET 파이프라인을 통해 이동 하는 모든 요청을 확인 합니다. 메시지 처리기는 Web API로 라우팅되는 요청만 볼 수 있습니다.
- 특정 경로에 인증 체계를 적용할 수 있는 경로 단위 메시지 처리기를 설정할 수 있습니다.
- HTTP 모듈은 IIS에만 적용 됩니다. 메시지 처리기는 호스트에 독립적 이므로 웹 호스팅 및 자체 호스팅 모두에서 사용할 수 있습니다.
- HTTP 모듈은 IIS 로깅, 감사 등에 참여 합니다.
- HTTP 모듈은 파이프라인에서 이전에 실행 됩니다. 메시지 처리기에서 인증을 처리 하는 경우 처리기가 실행 될 때까지 보안 주체가 설정 되지 않습니다. 또한 보안 주체는 응답이 메시지 처리기를 벗어날 때 이전 주체로 돌아갑니다.

일반적으로 자체 호스팅을 지원 하지 않아도 되는 경우 HTTP 모듈이 더 나은 옵션입니다. 자체 호스팅을 지원 해야 하는 경우에는 메시지 처리기를 고려해 야 합니다.

### <a name="setting-the-principal"></a>보안 주체 설정

응용 프로그램에서 사용자 지정 인증 논리를 수행 하는 경우 다음 두 위치에서 보안 주체를 설정 해야 합니다.

- **System.threading.thread.currentprincipal**. 이 속성은 .NET에서 스레드의 보안 주체를 설정 하는 표준 방법입니다.
- **HttpContext. 사용자**. 이 속성은 ASP.NET에만 적용 됩니다.

다음 코드에서는 보안 주체를 설정 하는 방법을 보여 줍니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

웹 호스팅의 경우 두 위치 모두에서 보안 주체를 설정 해야 합니다. 그렇지 않으면 보안 컨텍스트가 일치 하지 않게 될 수 있습니다. 그러나 자체 호스팅을 위해 **httpcontext.current** 는 null입니다. 따라서 코드에 호스트를 독립적으로 사용할 수 있도록 하려면 표시 된 대로 **httpcontext.current**에를 할당 하기 전에 null 인지 확인 합니다.

## <a name="authorization"></a>권한 부여

권한 부여는 컨트롤러에 더 가깝게 파이프라인에서 나중에 수행 됩니다. 이를 통해 리소스에 대 한 액세스 권한을 부여할 때 더 세부적인 선택을 할 수 있습니다.

- *권한 부여 필터* 는 컨트롤러 작업 이전에 실행 됩니다. 요청이 인증 되지 않은 경우 필터는 오류 응답을 반환 하 고 동작은 호출 되지 않습니다.
- 컨트롤러 작업 내에서 **ApiController** 속성을 사용 하 여 현재 보안 주체를 가져올 수 있습니다. 예를 들어 사용자 이름에 따라 리소스 목록을 필터링 하 여 해당 사용자에 게 속하는 리소스만 반환할 수 있습니다.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>[권한 부여] 특성 사용

Web API는 기본 제공 권한 부여 필터 인 [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)을 제공 합니다. 이 필터는 사용자가 인증 되었는지 여부를 확인 합니다. 그렇지 않으면 동작을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)을 반환 합니다.

전역, 컨트롤러 수준 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.

**전역적**으로: 모든 Web API 컨트롤러에 대 한 액세스를 제한 하려면 전역 필터 목록에 **AuthorizeAttribute** 필터를 추가 합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**컨트롤러**: 특정 컨트롤러에 대 한 액세스를 제한 하려면 해당 필터를 컨트롤러에 특성으로 추가 합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**작업**: 특정 작업에 대 한 액세스를 제한 하려면 작업 메서드에 특성을 추가 합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

또는 컨트롤러를 제한 한 다음 특성을 사용 하 여 특정 작업에 대 한 익명 액세스를 허용할 수 있습니다 `[AllowAnonymous]` . 다음 예제에서 `Post` 메서드는 제한 되지만 `Get` 메서드는 익명 액세스를 허용 합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

이전 예제에서 필터는 인증 된 사용자가 제한 된 메서드에 액세스할 수 있도록 허용 합니다. 익명 사용자만 유지 됩니다. 특정 사용자 또는 특정 역할의 사용자에 대 한 액세스를 제한할 수도 있습니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Web API 컨트롤러에 대 한 **AuthorizeAttribute** 필터는 **system.web. Http** 네임 스페이스에 있습니다. Web API 컨트롤러와 호환 되지 않는 **system.web 네임 스페이스** 의 mvc 컨트롤러에 대 한 유사한 필터가 있습니다.

### <a name="custom-authorization-filters"></a>사용자 지정 권한 부여 필터

사용자 지정 권한 부여 필터를 작성 하려면 다음 형식 중 하나에서 파생 합니다.

- **AuthorizeAttribute**. 현재 사용자 및 사용자의 역할에 따라 권한 부여 논리를 수행 하려면이 클래스를 확장 합니다.
- **Authorizationfilterattribute**입니다. 이 클래스를 확장 하 여 현재 사용자 또는 역할을 기반으로 하지 않아도 되는 동기 권한 부여 논리를 수행 합니다.
- **IAuthorizationFilter**. 비동기 권한 부여 논리를 수행 하려면이 인터페이스를 구현 합니다. 예를 들어 권한 부여 논리가 비동기 i/o 또는 네트워크 호출을 수행 하는 경우입니다. 권한 부여 논리가 CPU 바인딩된 경우에는 비동기 메서드를 작성할 필요가 없기 때문에 **Authorizationfilterattribute**에서 파생 하는 것이 더 간단 합니다.

다음 다이어그램에서는 **AuthorizeAttribute** 클래스에 대 한 클래스 계층 구조를 보여 줍니다.

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>컨트롤러 작업 내부 권한 부여

경우에 따라 요청을 계속 진행 하지만 보안 주체에 따라 동작을 변경 하도록 허용할 수도 있습니다. 예를 들어 반환 하는 정보는 사용자의 역할에 따라 변경 될 수 있습니다. 컨트롤러 메서드 내에서 **ApiController** 속성을 사용 하 여 현재 보안 주체를 가져올 수 있습니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
