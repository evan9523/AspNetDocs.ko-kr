---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 권한 부여 서버 | 마이크로 소프트 문서
author: hongyes
description: 이 자습서에서는 OWIN OAuth 미들웨어를 사용하여 OAuth 2.0 권한 부여 서버를 구현하는 방법을 안내합니다. 이것은 단지 outlin 고급 자습서입니다 ...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540414"
---
<a name="owin-oauth-20-authorization-server"></a>OWIN OAuth 2.0 권한 부여 서버
====================
[홍예선과](https://github.com/hongyes) [프라부라즈 티아가라잔](https://github.com/Praburaj)

> 이 자습서에서는 OWIN OAuth 미들웨어를 사용하여 OAuth 2.0 권한 부여 서버를 구현하는 방법을 안내합니다. OWIN OAuth 2.0 권한 부여 서버를 만드는 단계만 간략하게 설명하는 고급 자습서입니다. 이것은 단계별 튜토리얼이 아닙니다. [샘플 코드를 다운로드합니다.](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)
>
> > [!NOTE]
> > 이 개요는 보안 프로덕션 앱을 만드는 데 사용해서는 안 됩니다. 이 자습서에서는 OWIN OAuth 미들웨어를 사용하여 OAuth 2.0 권한 부여 서버를 구현하는 방법에 대한 개요만 제공하기 위한 것입니다.
>
>
> ## <a name="software-versions"></a>소프트웨어 버전
>
> | **튜토리얼에 표시** | **또한 와 함께 작동** |
> | --- | --- |
> | Windows 8.1 | 윈도우 8, 윈도우 7 |
> | [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | [비주얼 스튜디오 2013 데스크탑 익스프레스](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express). 최신 업데이트와 Visual Studio 2012 가 작동해야하지만, 튜토리얼은 그것으로 테스트되지 않은, 일부 메뉴 선택 및 대화 상자는 다르다. |
> | .NET 4.5 |  |
>
> ## <a name="questions-and-comments"></a>질문 및 의견
>
> 당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [GitHub에 카타나 프로젝트에서](https://github.com/aspnet/AspNetKatana/)게시 할 수 있습니다 . 자습서 자체에 대한 질문과 의견은 페이지 하단의 주석 섹션을 참조하십시오.


[OAuth 2.0 프레임워크를](http://tools.ietf.org/html/rfc6749) 사용하면 타사 앱에서 HTTP 서비스에 대한 제한된 액세스를 얻을 수 있습니다. 클라이언트는 리소스 소유자의 자격 증명을 사용하여 보호된 리소스에 액세스하는 대신 특정 범위, 수명 및 기타 액세스 특성을 나타내는 문자열인 액세스 토큰을 얻습니다. 액세스 토큰은 리소스 소유자의 승인을 받은 권한 부여 서버에서 타사 클라이언트에 발급됩니다.

이 자습서는 다음을 다룹니다.

- 네 가지 권한 부여 권한 부여 유형 및 새로 고침 토큰을 지원하기 위해 권한 부여 서버를 만드는 방법:
    - 권한 부여 코드 부여
    - 암시적 부여
    - 리소스 소유자 암호 자격 증명 부여
    - 클라이언트 자격 증명 부여
- 액세스 토큰으로 보호되는 리소스 서버 만들기
- OAuth 2.0 클라이언트 만들기.

<a id="prerequisites"></a>
## <a name="prerequisites"></a>사전 요구 사항

- [비주얼 스튜디오 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) 또는 무료 [비주얼 스튜디오 익스프레스 2013,](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)페이지 상단의 **소프트웨어 버전에** 표시된 대로.
- OWIN에 익숙합니다. [카타나 프로젝트 시작하기와](https://msdn.microsoft.com/magazine/dn451439.aspx) [OWIN 및 카타나에서](index.md)새로운 사항 확인
- [역할,](http://tools.ietf.org/html/rfc6749#section-1.1) [프로토콜 흐름](http://tools.ietf.org/html/rfc6749#section-1.2)및 [권한 부여 부여를](http://tools.ietf.org/html/rfc6749#section-1.3)포함한 [OAuth](http://tools.ietf.org/html/rfc6749) 용어에 대한 친숙도. [OAuth 2.0 소개는](http://tools.ietf.org/html/rfc6749#section-1) 좋은 소개를 제공합니다.

## <a name="create-an-authorization-server"></a>권한 부여 서버 만들기

이 자습서에서는 [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) 및 ASP.NET MVC를 사용하여 권한 부여 서버를 만드는 방법을 대략 스케치합니다. 이 자습서에는 각 단계가 포함되어 있지 않으므로 완료된 샘플에 대한 다운로드를 곧 제공할 수 있기를 바랍니다. 먼저 *AuthorizationServer라는* 빈 웹 앱을 만들고 다음 패키지를 설치합니다.

- 마이크로소프트.아스프넷.Mvc
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth
- Microsoft.Owin.Security.Cookies
- 마이크로 소프트.Owin.Security.Google (또는 마이크로 소프트.Owin.Security.Facebook과 같은 다른 소셜 로그인 패키지)

*시작이라는*프로젝트 루트 폴더 아래에 [OWIN 시작 클래스를](owin-startup-class-detection.md) 추가합니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

*앱\_시작* 폴더를 만듭니다. *앱\_시작* 폴더를 선택하고 Shift+Alt+A를 사용하여 권한 *부여 서버\앱\_시작\Startup.Auth.cs* 파일의 다운로드버전을 추가합니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

위의 코드는 계정 관리를 위해 권한 부여 서버 자체에서 사용되는 쿠키 및 Google 인증에 응용 프로그램 / 외부 로그인을 할 수 있습니다.

`UseOAuthAuthorizationServer` 확장 방법은 권한 부여 서버를 설정하는 것입니다. 설정 옵션은 다음과 같습니다.

- `AuthorizeEndpointPath`: 클라이언트 응용 프로그램이 사용자가 토큰 또는 코드를 발급하는 데 동의를 얻기 위해 사용자 에이전트를 리디렉션하는 요청 경로입니다. 예를 들어`/Authorize`선행 슬래시로 시작해야 합니다.
- `TokenEndpointPath`: 요청 경로 클라이언트 응용 프로그램이 액세스 토큰을 얻기 위해 직접 통신합니다. "/토큰"과 같은 선행 슬래시로 시작해야 합니다. 클라이언트가 [클라이언트\_보안](http://tools.ietf.org/html/rfc6749#appendix-A.2)을 발급하는 경우 이 끝점에 제공해야 합니다.
- `ApplicationCanDisplayErrors`: 웹 `true` 응용 프로그램이 엔드포인트에서 클라이언트 유효성 검사 오류에 `/Authorize` 대한 사용자 지정 오류 페이지를 생성하려는 경우로 설정합니다. 이는 브라우저가 클라이언트 응용 프로그램으로 다시 리디렉션되지 않는 경우(예: `client_id` 올바르지 `redirect_uri` 않은 경우에만)에만 필요합니다. 끝점은 `/Authorize` "oauth"를 볼 것으로 예상해야 합니다. 오류", "오스. 오류 설명", "oauth" ErrorUri" 속성이 OWIN 환경에 추가됩니다.

    > [!NOTE]
    > 그렇지 않은 경우 권한 부여 서버는 오류 세부 정보가 있는 기본 오류 페이지를 반환합니다.
- `AllowInsecureHttp`: TRUE는 HTTP URI 주소에 권한을 부여하고 토큰 요청이 `redirect_uri` HTTP URI 주소에 도착할 수 있도록 허용하고 들어오는 요청 매개 변수에 HTTP URI 주소를 가질 수 있도록 허용합니다.

    > [!WARNING]
    > 보안 - 개발 전용입니다.
- `Provider`: 권한 부여 서버 미들웨어에서 발생하는 이벤트를 처리하기 위해 응용 프로그램에서 제공하는 개체입니다. 응용 프로그램은 인터페이스를 완전히 구현하거나 이 서버가 지원하는 OAuth 흐름에 필요한 대리자를 `OAuthAuthorizationServerProvider` 인스턴스를 만들고 할당할 수 있습니다.
- `AuthorizationCodeProvider`: 클라이언트 응용 프로그램으로 돌아가는 일회용 권한 부여 코드를 생성합니다. OAuth 서버가 보안을 유지하려면 응용 프로그램이 `AuthorizationCodeProvider` `OnCreate/OnCreateAsync` 이벤트에서 생성된 토큰이 에 대한 호출 한 `OnReceive/OnReceiveAsync`번만 유효한 것으로 간주되는 인스턴스를 제공해야 **합니다.**
- `RefreshTokenProvider`: 필요할 때 새 액세스 토큰을 생성하는 데 사용할 수 있는 새로 고침 토큰을 생성합니다. 부여 서버가 제공되지 않으면 끝점에서 새로 `/Token` 고침 토큰이 반환되지 않습니다.

## <a name="account-management"></a>계정 관리

OAuth는 사용자 계정 정보를 관리하는 위치 나 방법을 신경 쓰지 않습니다. 그것은 ASP.NET 그것을 담당하는 [정체성입니다.](../../../identity/index.md) 이 자습서에서는 계정 관리 코드를 단순화 하 고 사용자가 OWIN 쿠키 미들웨어를 사용 하 여 로그인할 수 있는지 확인 합니다. 다음은 다음의 단순화된 샘플 `AccountController`코드입니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

`ValidateClientRedirectUri`은 등록된 리디렉션 URL을 사용하여 클라이언트의 유효성을 검사하는 데 사용됩니다. `ValidateClientAuthentication`기본 구성표 헤더와 폼 본문을 확인하여 클라이언트의 자격 증명을 가져옵니다.

로그인 페이지는 다음과 같습니다.

![](owin-oauth-20-authorization-server/_static/image1.png)

지금 IETF의 OAuth 2 [권한 부여 코드 부여](http://tools.ietf.org/html/rfc6749#section-4.1) 섹션을 검토하십시오.

**공급자(아래** 표)는 [OAuth권한 부여 서버옵션입니다.](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx) 모든 OAuth `OAuthAuthorizationServerProvider`서버 이벤트를 포함하는 형식의 공급자입니다.

| 권한 부여 코드 부여 섹션의 흐름 단계 | 샘플 다운로드는 다음 단계를 수행합니다. |
| --- | --- |
|  |  |
| (A) 클라이언트는 리소스 소유자의 사용자 에이전트를 권한 부여 끝점으로 지시하여 흐름을 시작합니다. 클라이언트에는 클라이언트 식별자, 요청된 범위, 로컬 상태 및 권한 부여 서버가 액세스가 부여되거나 거부되면 사용자 에이전트를 다시 보내는 리디렉션 URI가 포함됩니다. | 공급자.일치 엔드 포인트 공급자.유효성 검사클라이언트RedirectUri 공급자.유효성 검사승인 요청 공급자.권한 부여 Endpoint |
|  |  |
| (B) 권한 부여 서버는 사용자 에이전트를 통해 리소스 소유자를 인증하고 리소스 소유자가 클라이언트의 액세스 요청을 부여하거나 거부하는지 여부를 설정합니다. | **사용자에게 액세스&gt; 권한을 부여하는 경우 &lt;** 공급자.매치엔드포인트 공급자.유효성 검사클라이언트RedirectUri 공급자.유효성 검사승인 요청 공급자.권한 부여Endpoint 권한 코드 제공.CreateAsync |
|  |  |
| (C) 리소스 소유자가 액세스 권한을 부여한다고 가정하면 권한 부여 서버는 앞에서 제공한 리디렉션 URI(요청 또는 클라이언트 등록 중)를 사용하여 사용자 에이전트를 클라이언트로 리디렉션합니다. ... |  |
|  |  |
| (D) 클라이언트는 이전 단계에서 받은 권한 부여 코드를 포함하여 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청합니다. 요청을 할 때 클라이언트는 권한 부여 서버로 인증합니다. 클라이언트에는 확인을 위한 권한 부여 코드를 가져오는 데 사용되는 리디렉션 URI가 포함됩니다. | provider.MatchEndpoint 공급자.유효성 검사 클라이언트 인증 인증 코드코드.ReceiveAsync 공급자.ValidateTokenRequest 공급자.토큰엔드포인트 액세스 토큰 공급자.CreateAsync 새로 고침 토큰 공급자.CreateAsync |

권한 부여 `AuthorizationCodeProvider.CreateAsync` 코드의 생성 및 유효성 검사를 제어하기 `ReceiveAsync` 위한 샘플 구현은 다음과 같습니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

위의 코드는 메모리 내 동시 사전을 사용하여 코드 및 ID 티켓을 저장하고 코드를 받은 후 ID를 복원합니다. 실제 응용 프로그램에서는 영구 데이터 저장소로 대체됩니다. 권한 부여 끝점은 리소스 소유자가 클라이언트에 대한 액세스 권한을 부여하는 것입니다. 일반적으로 사용자가 단추를 클릭하고 권한 부여를 확인할 수 있도록 사용자 인터페이스가 필요합니다. OWIN OAuth 미들웨어를 사용하면 응용 프로그램 코드가 권한 부여 끝점을 처리할 수 있습니다. 샘플 앱에서는 이를 처리하기 위해 호출된 `OAuthController` MVC 컨트롤러를 사용합니다. 다음은 샘플 구현입니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

이 `Authorize` 작업은 사용자가 권한 부여 서버에 로그인했는지 먼저 확인합니다. 그렇지 않은 경우 인증 미들웨어는 호출자에게 "응용 프로그램" 쿠키를 사용하여 인증하도록 하고 로그인 페이지로 리디렉션합니다. (위의 강조 표시된 코드를 참조하십시오.) 사용자가 로그인한 경우 아래와 같이 권한 부여 보기가 렌더링됩니다.

![](owin-oauth-20-authorization-server/_static/image2.png)

권한 **부여** 단추를 선택하면 `Authorize` 작업이 새 "Bearer" ID를 만들고 로그인합니다. 권한 부여 서버가 베어러 토큰을 생성하고 JSON 페이로드를 사용하여 클라이언트로 다시 보냅니다.

### <a name="implicit-grant"></a>암시적 부여

지금 IETF의 OAuth 2 [암시적 부여](http://tools.ietf.org/html/rfc6749#section-4.2) 섹션을 참조하십시오.

 그림 4에 표시된 [암시적 부여](http://tools.ietf.org/html/rfc6749#section-4.2) 흐름은 OWIN OAuth 미들웨어가 따르는 흐름 및 매핑입니다.

| 암시적 부여 섹션의 흐름 단계 | 샘플 다운로드는 다음 단계를 수행합니다. |
| --- | --- |
|  |  |
| (A) 클라이언트는 리소스 소유자의 사용자 에이전트를 권한 부여 끝점으로 지시하여 흐름을 시작합니다. 클라이언트에는 클라이언트 식별자, 요청된 범위, 로컬 상태 및 권한 부여 서버가 액세스가 부여되거나 거부되면 사용자 에이전트를 다시 보내는 리디렉션 URI가 포함됩니다. | 공급자.일치 엔드 포인트 공급자.유효성 검사클라이언트RedirectUri 공급자.유효성 검사승인 요청 공급자.권한 부여 Endpoint |
|  |  |
| (B) 권한 부여 서버는 사용자 에이전트를 통해 리소스 소유자를 인증하고 리소스 소유자가 클라이언트의 액세스 요청을 부여하거나 거부하는지 여부를 설정합니다. | **사용자에게 액세스&gt; 권한을 부여하는 경우 &lt;** 공급자.매치엔드포인트 공급자.유효성 검사클라이언트RedirectUri 공급자.유효성 검사승인 요청 공급자.권한 부여Endpoint 권한 코드 제공.CreateAsync |
|  |  |
| (C) 리소스 소유자가 액세스 권한을 부여한다고 가정하면 권한 부여 서버는 앞에서 제공한 리디렉션 URI(요청 또는 클라이언트 등록 중)를 사용하여 사용자 에이전트를 클라이언트로 리디렉션합니다. ... |  |
|  |  |
| (D) 클라이언트는 이전 단계에서 받은 권한 부여 코드를 포함하여 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청합니다. 요청을 할 때 클라이언트는 권한 부여 서버로 인증합니다. 클라이언트에는 확인을 위한 권한 부여 코드를 가져오는 데 사용되는 리디렉션 URI가 포함됩니다. |  |

권한 부여 코드 부여에`OAuthController.Authorize` 대한 권한 부여 끝점(작업)을 이미 구현했기 때문에 암시적 흐름도 자동으로 활성화됩니다. 참고: `Provider.ValidateClientRedirectUri` 리디렉션 URL을 사용하여 클라이언트 ID의 유효성을 검사하는 데 사용되며, 이 URL은 암시적 권한 부여 흐름이 악의적인[클라이언트(중간자](https://www.owasp.org/index.php/Man-in-the-middle_attack)공격)에게 액세스 토큰을 보내지 않도록 보호합니다.

### <a name="resource-owner-password-credentials-grant"></a>리소스 소유자 암호 자격 증명 부여

지금 IETF의 OAuth 2 [리소스 소유자 암호 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.3) 섹션을 참조하십시오.

 그림 5에 표시된 [리소스 소유자 암호 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.3) 흐름은 OWIN OAuth 미들웨어가 따르는 흐름 및 매핑입니다.

| 리소스 소유자 암호 자격 증명 부여 섹션에서 단계 흐름 | 샘플 다운로드는 다음 단계를 수행합니다. |
| --- | --- |
|  |  |
| (A) 리소스 소유자는 클라이언트에 사용자 이름과 암호를 제공합니다. |  |
|  |  |
| (B) 클라이언트는 리소스 소유자로부터 받은 자격 증명을 포함하여 권한 부여 서버의 토큰 끝점에서 액세스 토큰을 요청합니다. 요청을 할 때 클라이언트는 권한 부여 서버로 인증합니다. | provider.MatchEndpoint 공급자.유효성 검사 클라이언트 인증 공급자.유효성 검사토큰 요청 공급자.GrantResource소유자 자격 증명 공급자.TokenEndpoint 액세스 토큰 공급자.CreateAsync 새로 고침 토큰 공급자.CreateAsync 새로 고침 토큰 공급자.CreateAsync |
|  |  |
| (C) 권한 부여 서버는 클라이언트를 인증하고 리소스 소유자 자격 증명의 유효성을 검사하며, 유효한 경우 액세스 토큰을 발급합니다. |  |

다음은 `Provider.GrantResourceOwnerCredentials`샘플 구현입니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> 위의 코드는 자습서의 이 섹션을 설명하기 위한 것이며 보안 또는 프로덕션 앱에서 사용해서는 안 됩니다. 리소스 소유자 자격 증명을 검사하지 않습니다. 모든 자격 증명이 유효하다고 가정하고 새 ID를 만듭니다. 새 ID는 액세스 토큰을 생성하고 토큰을 새로 고치는 데 사용됩니다. 코드를 사용자 고유의 보안 계정 관리 코드로 바꾸십시오.


### <a name="client-credentials-grant"></a>클라이언트 자격 증명 부여

지금 IETF의 OAuth 2 [클라이언트 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.4) 섹션을 참조하십시오.

 그림 6에 표시된 [클라이언트 자격 증명 부여](http://tools.ietf.org/html/rfc6749#section-4.4) 흐름은 OWIN OAuth 미들웨어가 따르는 흐름 및 매핑입니다.

| 클라이언트 자격 증명 부여 섹션의 흐름 단계 | 샘플 다운로드는 다음 단계를 수행합니다. |
| --- | --- |
|  |  |
| (A) 클라이언트는 권한 부여 서버로 인증하고 토큰 끝점에서 액세스 토큰을 요청합니다. | provider.MatchEndpoint 공급자.유효성 검사 클라이언트 인증 공급자.유효성 검사 토큰 요청 공급자.GrantClientcredentials 공급자.TokenEndpoint 액세스 토큰 공급자.CreateAsync 새로 고침 토큰 공급자.CreateAsync |
|  |  |
| (B) 권한 부여 서버는 클라이언트를 인증하고 유효한 경우 액세스 토큰을 발급합니다. |  |

다음은 `Provider.GrantClientCredentials`샘플 구현입니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> 위의 코드는 자습서의 이 섹션을 설명하기 위한 것이며 보안 또는 프로덕션 앱에서 사용해서는 안 됩니다. 코드를 사용자 고유의 보안 클라이언트 관리 코드로 바꾸십시오.


### <a name="refresh-token"></a>토큰 새로 고침

지금 IETF의 OAuth 2 [새로 고침 토큰](http://tools.ietf.org/html/rfc6749#section-1.5) 섹션을 참조하십시오.

 그림 2에 표시된 [새로 고침 토큰](http://tools.ietf.org/html/rfc6749#section-1.5) 흐름은 OWIN OAuth 미들웨어가 따르는 흐름 및 매핑입니다.

| 클라이언트 자격 증명 부여 섹션의 흐름 단계 | 샘플 다운로드는 다음 단계를 수행합니다. |
| --- | --- |
|  |  |
| (G) 클라이언트는 권한 부여 서버로 인증하고 새로 고침 토큰을 표시하여 새 액세스 토큰을 요청합니다. 클라이언트 인증 요구 사항은 클라이언트 유형 및 권한 부여 서버 정책을 기반으로 합니다. | provider.MatchEndpoint 공급자.유효성 검사 클라이언트 인증 새로 고침 토큰 공급자.ReceiveAsync 공급자.유효성 검사 토큰 공급자.GrantRefreshToken 공급자.TokenEndpoint 액세스 토큰 공급자.CreateAsync 새로 고침 토큰 공급자.CreateAsync |
|  |  |
| (H) 권한 부여 서버는 클라이언트를 인증하고 새로 고침 토큰의 유효성을 검사하며, 유효한 경우 새 액세스 토큰(및 선택적으로 새 새로 고침 토큰)을 발행합니다. |  |

다음은 `Provider.GrantRefreshToken`샘플 구현입니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a>액세스 토큰으로 보호되는 리소스 서버 만들기

빈 웹 앱 프로젝트를 만들고 프로젝트에 다음 패키지를 설치합니다.

- 마이크로소프트.아스프넷.웹Api.오윈
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth

시작 클래스를 만들고 인증 및 웹 API를 구성합니다. 샘플 다운로드에서 *권한 부여 서버\리소스 서버\Startup.cs를* 참조하십시오.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

샘플 다운로드에서 *권한 부여\_서버\리소스 서버\앱 시작\Startup.Auth.cs를* 참조하십시오.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

샘플 다운로드에서 *권한 부여\_서버\리소스 서버\앱 시작\Startup.WebApi.cs를* 참조하십시오.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- `UseCors`메서드를 사용하면 모든 도메인에 대한 CORS가 허용됩니다.
- `UseOAuthBearerAuthentication`메서드는 요청의 권한 부여 헤더에서 베어러 토큰을 수신하고 유효성을 검사하는 OAuth 베어러 토큰 인증 미들웨어를 활성화합니다.
- `Config.SuppressDefaultHostAuthenticaiton`앱에서 기본 호스트 인증 보안 주체를 표시하므로 이 호출 후 모든 요청이 익명으로 표시됩니다.
- `HostAuthenticationFilter`지정된 인증 유형에 대해서만 인증을 활성화합니다. 이 경우 베어러 인증 유형입니다.

인증된 ID를 보여 주기 위해 현재 사용자의 클레임을 출력하는 ApiController를 만듭니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

권한 부여 서버와 리소스 서버가 동일한 컴퓨터에 없는 경우 OAuth 미들웨어는 다른 컴퓨터 키를 사용하여 베어러 액세스 토큰을 암호화하고 해독합니다. 두 프로젝트 간에 동일한 개인 키를 공유하기 `machinekey` 위해 두 *web.config* 파일에 동일한 설정을 추가합니다.

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a>OAuth 2.0 클라이언트 만들기

 우리는 클라이언트 코드를 단순화하기 위해 [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet 패키지를 사용합니다.

### <a name="authorization-code-grant-client"></a>권한 부여 코드 부여 클라이언트

 이 클라이언트는 MVC 응용 프로그램입니다. 백 엔드에서 액세스 토큰을 얻기 위해 권한 부여 코드 부여 흐름을 트리거합니다. 아래와 같이 단일 페이지가 있습니다.

![](owin-oauth-20-authorization-server/_static/image3.png)

- **권한 부여** 단추는 브라우저를 권한 부여 서버로 리디렉션하여 리소스 소유자에게 이 클라이언트에 대한 액세스 권한을 부여하도록 알립니다.
- **새로 고침** 단추는 현재 새로 고침 토큰을 사용하여 새 액세스 토큰및 새로 고침 토큰을 가져옵니다.
- **보호된 리소스 API 액세스** 단추는 리소스 서버를 호출하여 현재 사용자의 클레임 데이터를 얻고 페이지에 표시합니다.

다음은 클라이언트의 `HomeController` 샘플 코드입니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

`DotNetOpenAuth`기본적으로 SSL이 필요합니다. 데모에서 HTTP를 사용하므로 구성 파일에 다음 설정을 추가해야 합니다.

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> 보안 - 프로덕션 앱에서 SSL을 사용하지 않도록 설정하지 마십시오. 이제 로그인 자격 증명이 유선에서 일반 텍스트로 전송됩니다. 위의 코드는 로컬 샘플 디버깅 및 탐색용입니다.


### <a name="implicit-grant-client"></a>암시적 부여 클라이언트

이 클라이언트는 자바 스크립트를 사용하여 다음을 수행합니다.

1. 새 창을 열고 권한 부여 서버의 권한 부여 끝점으로 리디렉션합니다.
2. URL 조각이 다시 리디렉션될 때 URL 조각에서 액세스 토큰을 가져옵니다.

다음 이미지는 이 프로세스를 보여 주며 다음과 같은 프로세스를 보여 주며 다음과 같은 프로세스를 보여 주며 다음과

![](owin-oauth-20-authorization-server/_static/image4.png)

클라이언트는 홈 페이지용 페이지와 콜백용 페이지의 두 페이지가 있어야 합니다. 다음은 *Index.cshtml* 파일에 있는 자바스크립트 샘플 코드입니다.

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

*SignIn.cshtml* 파일의 콜백 처리 코드는 다음과 같습니다.

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> 가장 좋은 방법은 자바스크립트를 외부 파일로 이동하고 Razor 태그와 함께 포함하지 않는 것입니다. 이 샘플을 단순하게 유지하기 위해 결합되었습니다.


### <a name="resource-owner-password-credentials-grant-client"></a>리소스 소유자 암호 자격 증명 부여 클라이언트

콘솔 앱을 사용하여 이 클라이언트를 데모합니다. 코드는 다음과 같습니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a>클라이언트 자격 증명 부여 클라이언트

리소스 소유자 암호 자격 증명 부여와 유사하게 콘솔 앱 코드는 다음과 같습니다.

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
