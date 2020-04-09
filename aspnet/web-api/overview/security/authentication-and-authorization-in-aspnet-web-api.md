---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET 웹 API의 인증 및 권한 부여 | 마이크로 소프트 문서
author: MikeWasson
description: ASP.NET 웹 API에서 인증 및 권한 부여에 대한 일반적인 개요를 제공합니다.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675864"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>ASP.NET Web API의 인증 및 권한 부여

로 [마이크 와슨](https://github.com/MikeWasson)

웹 API를 만들었지만 이제 웹 API에 대한 액세스를 제어하려고 합니다. 이 문서 시리즈에서는 권한이 있는 사용자로부터 웹 API를 보호하기 위한 몇 가지 옵션을 살펴보겠습니다. 이 시리즈에서는 인증 및 권한 부여를 모두 다룹니다.

- *인증은* 사용자의 ID를 알고 있습니다. 예를 들어 Alice는 사용자 이름과 암호를 사용하여 로그인하고 서버는 암호를 사용하여 Alice를 인증합니다.
- *권한 부여는* 사용자가 작업을 수행할 수 있는지 여부를 결정합니다. 예를 들어 Alice에는 리소스를 얻을 수 있지만 리소스를 만들 수 있는 권한이 있습니다.

시리즈의 첫 번째 문서에서는 ASP.NET 웹 API에서 인증 및 권한 부여에 대한 일반적인 개요를 제공합니다. 다른 항목에서는 Web API에 대한 일반적인 인증 시나리오를 설명합니다.

> [!NOTE]
> 릭 앤더슨, 레비 브로데릭, 배리 도란스, 톰 다이크스트라, 홍메이 게, 데이비드 맷슨, 다니엘 로스, 팀 티켄 등 이 시리즈를 검토하고 귀중한 피드백을 제공한 분들께 감사드립니다.

## <a name="authentication"></a>인증

Web API는 인증이 호스트에서 발생한다고 가정합니다. 웹 호스팅의 경우 호스트는 인증을 위해 HTTP 모듈을 사용하는 IIS입니다. IIS 또는 ASP.NET 내장된 인증 모듈을 사용하도록 프로젝트를 구성하거나 사용자 지정 인증을 수행하기 위해 자체 HTTP 모듈을 작성할 수 있습니다.

호스트가 사용자를 인증하면 코드가 실행 중인 보안 컨텍스트를 나타내는 [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) 개체인 *보안 주체를*만듭니다. 호스트는 **Thread.CurrentPrincipal을**설정하여 현재 스레드에 주체를 연결합니다. 보안 주체에는 사용자에 대한 정보가 포함된 연결된 **Identity** 개체가 포함되어 있습니다. 사용자가 인증된 경우 **Identity.Is인증** 속성은 **true를**반환합니다. 익명 요청의 경우 **Is인증은** **false를 반환합니다.** 보안 주체에 대한 자세한 내용은 [역할 기반 보안](https://msdn.microsoft.com/library/shz8h065.aspx)을 참조하십시오.

### <a name="http-message-handlers-for-authentication"></a>인증을 위한 HTTP 메시지 처리기

인증을 위해 호스트를 사용하는 대신 HTTP 메시지 [처리기에](../advanced/http-message-handlers.md)인증 논리를 넣을 수 있습니다. 이 경우 메시지 처리기는 HTTP 요청을 검사하고 보안 주체를 설정합니다.

인증에 메시지 처리기를 언제 사용해야 합니까? 다음은 몇 가지 장단점입니다.

- HTTP 모듈은 ASP.NET 파이프라인을 통과하는 모든 요청을 봅니다. 메시지 처리기는 웹 API로 라우팅되는 요청만 볼 수 있습니다.
- 특정 경로에 인증 체계를 적용할 수 있는 경로별 메시지 처리기를 설정할 수 있습니다.
- HTTP 모듈은 IIS에만 해당됩니다. 메시지 처리기는 호스트에 구애받지 않으므로 웹 호스팅과 자체 호스팅모두에서 사용할 수 있습니다.
- HTTP 모듈은 IIS 로깅, 감사 등에 참여합니다.
- HTTP 모듈은 파이프라인의 앞에서 실행됩니다. 메시지 처리기에서 인증을 처리하는 경우 처리기가 실행될 때까지 보안 주체가 설정되지 않습니다. 또한 응답이 메시지 처리기를 떠날 때 주 서버는 이전 주 서버로 되돌아갑니다.

일반적으로 자체 호스팅을 지원할 필요가 없는 경우 HTTP 모듈이 더 나은 옵션입니다. 자체 호스팅을 지원해야 하는 경우 메시지 처리기를 고려하십시오.

### <a name="setting-the-principal"></a>보안 주체 설정

응용 프로그램에서 사용자 지정 인증 논리를 수행하는 경우 다음 두 위치에 보안 주체를 설정해야 합니다.

- **스레드.현재 주체**. 이 속성은 .NET에서 스레드의 주체를 설정하는 표준 방법입니다.
- **HttpContext.현재.사용자**. 이 속성은 ASP.NET 한정입니다.

다음 코드는 보안 주체를 설정하는 방법을 보여 주며 있습니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

웹 호스팅의 경우 두 위치에서 보안 주체를 설정해야 합니다. 그렇지 않으면 보안 컨텍스트가 일치하지 않을 수 있습니다. 그러나 자체 호스팅의 경우 **HttpContext.Current는** null입니다. 따라서 코드가 호스트에 불가지않는지 확인하려면 그림과 같이 **HttpContext.Current에**할당하기 전에 null을 확인하십시오.

## <a name="authorization"></a>권한 부여

권한 부여는 파이프라인의 나중에 컨트롤러에 더 가깝게 수행됩니다. 이렇게 하면 리소스에 대한 액세스 권한을 부여할 때 보다 세부적인 선택을 할 수 있습니다.

- *권한 부여 필터는* 컨트롤러 작업 전에 실행됩니다. 요청이 승인되지 않은 경우 필터는 오류 응답을 반환하고 작업이 호출되지 않습니다.
- 컨트롤러 작업 내에서 **ApiController.User** 속성에서 현재 보안 주체를 얻을 수 있습니다. 예를 들어 사용자 이름을 기반으로 리소스 목록을 필터링하여 해당 사용자에 속한 리소스만 반환할 수 있습니다.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>[권한 부여] 특성 사용

웹 API는 기본 제공 권한 부여 필터인 [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)를 제공합니다. 이 필터는 사용자가 인증되었는지 여부를 확인합니다. 그렇지 않은 경우 작업을 호출하지 않고 HTTP 상태 코드 401(무단)을 반환합니다.

필터를 전역적으로, 컨트롤러 수준에서 또는 개별 작업 수준에서 적용할 수 있습니다.

**전역 :** 모든 웹 API 컨트롤러에 대한 액세스를 제한하려면 **AuthorizeAttribute** 필터를 전역 필터 목록에 추가합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**컨트롤러**: 특정 컨트롤러에 대한 액세스를 제한하려면 필터를 컨트롤러에 특성으로 추가합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**작업**: 특정 작업에 대한 액세스를 제한하려면 작업 메서드에 특성을 추가합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

또는 특성을 사용하여 컨트롤러를 제한한 다음 특정 작업에 대한 `[AllowAnonymous]` 익명 액세스를 허용할 수 있습니다. 다음 예제에서는 메서드가 `Post` 제한되지만 메서드는 `Get` 익명 액세스를 허용합니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

이전 예제에서는 필터를 사용하여 인증된 사용자가 제한된 메서드에 액세스할 수 있습니다. 익명 사용자만 유지됩니다. 특정 사용자 또는 특정 역할의 사용자에 대한 액세스를 제한할 수도 있습니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> 웹 API 컨트롤러에 대한 **권한 부여특성** 필터는 **System.Web.Http** 네임스페이스에 있습니다. Web API 컨트롤러와 호환되지 않는 **System.Web.Mvc** 네임스페이스에는 MVC 컨트롤러에 대한 유사한 필터가 있습니다.

### <a name="custom-authorization-filters"></a>사용자 지정 권한 부여 필터

사용자 지정 권한 부여 필터를 작성하려면 다음 형식 중 하나에서 파생합니다.

- **Attribute을 권한 부여합니다.** 현재 사용자 및 사용자의 역할에 따라 권한 부여 논리를 수행 하려면이 클래스를 확장 합니다.
- **권한 부여필터특성**. 이 클래스를 확장하여 현재 사용자 또는 역할에 반드시 기반하지 않는 동기 권한 부여 논리를 수행합니다.
- **I권한 부여 필터**. 비동기 권한 부여 논리를 수행 하려면이 인터페이스를 구현 합니다. 예를 들어 권한 부여 논리가 비동기 I/O 또는 네트워크 호출을 하는 경우입니다. 권한 부여 논리가 CPU 바인딩된 경우 비동기 메서드를 작성할 필요가 없으므로 **AUTHORIZATIONFilterAttribute에서**파생하는 것이 더 간단합니다.

다음 다이어그램은 **AuthorizeAttribute** 클래스에 대한 클래스 계층 구조를 보여 주며 있습니다.

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>컨트롤러 작업 내부 권한 부여

경우에 따라 요청을 계속하도록 허용하지만 보안 주체에 따라 동작을 변경할 수 있습니다. 예를 들어 반환하는 정보는 사용자의 역할에 따라 변경될 수 있습니다. 컨트롤러 메서드 내에서 **ApiController.User** 속성에서 현재 보안 주체를 얻을 수 있습니다.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
