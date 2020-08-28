---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
title: '멤버 자격 사용자 저장소에 대 한 사용자 자격 증명 유효성 검사 (c #) | Microsoft Docs'
author: rick-anderson
description: 이 자습서에서는 프로그래밍 방법 및 로그인 제어를 모두 사용 하 여 멤버 자격 사용자 저장소에 대해 사용자 자격 증명의 유효성을 검사 하는 방법을 살펴봅니다.
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 61aa4e08-aa81-4aeb-8ebe-19ba7a65e04c
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
msc.type: authoredcontent
ms.openlocfilehash: fd50f4e63c75cf77eb21629d0c11a859da6b357d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045236"
---
# <a name="validating-user-credentials-against-the-membership-user-store-c"></a>멤버 자격 사용자 저장소에 대해 사용자 자격 증명의 유효성 검사(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_cs.pdf)

> 이 자습서에서는 프로그래밍 방식 및 로그인 제어를 모두 사용 하 여 멤버 자격 사용자 저장소에 대해 사용자 자격 증명의 유효성을 검사 하는 방법을 설명 합니다. 로그인 컨트롤의 모양과 동작을 사용자 지정 하는 방법에 대해서도 살펴봅니다.

## <a name="introduction"></a>소개

<a id="Tutorial05"></a> [이전 자습서](creating-user-accounts-cs.md) 에서는 멤버 자격 프레임 워크에서 새로운 사용자 계정을 만드는 방법에 대해 살펴보았습니다. 먼저 `Membership` 클래스의 메서드를 통해 사용자 계정을 만든 `CreateUser` 다음 CreateUserWizard 웹 컨트롤을 사용 하 여 검사 하는 방법에 대해 살펴보았습니다. 그러나 로그인 페이지는 현재 하드 코드 된 사용자 이름 및 암호 쌍 목록에 대해 제공 된 자격 증명의 유효성을 검사 합니다. 멤버 프레임 워크의 사용자 저장소에 대 한 자격 증명의 유효성을 검사 하도록 로그인 페이지의 논리를 업데이트 해야 합니다.

사용자 계정을 만드는 것과 매우 유사 하 게 자격 증명을 프로그래밍 방식으로 또는 선언적으로 확인할 수 있습니다. 멤버 자격 API에는 사용자 저장소에 대해 사용자의 자격 증명을 프로그래밍 방식으로 확인 하는 메서드가 포함 되어 있습니다. 및 ASP.NET에는 사용자 이름 및 암호에 대 한 텍스트 상자와 로그인 단추를 사용 하 여 사용자 인터페이스를 렌더링 하는 로그인 웹 컨트롤이 함께 제공 됩니다.

이 자습서에서는 프로그래밍 방식 및 로그인 제어를 모두 사용 하 여 멤버 자격 사용자 저장소에 대해 사용자 자격 증명의 유효성을 검사 하는 방법을 설명 합니다. 로그인 컨트롤의 모양과 동작을 사용자 지정 하는 방법에 대해서도 살펴봅니다. 그럼 시작하겠습니다.

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>1 단계: 멤버 자격 사용자 저장소에 대 한 자격 증명 유효성 검사

폼 인증을 사용 하는 웹 사이트의 경우 사용자는 로그인 페이지를 방문 하 고 자격 증명을 입력 하 여 웹 사이트에 로그온 합니다. 그런 다음 이러한 자격 증명을 사용자 저장소와 비교 합니다. 유효한 경우 방문자의 id와 신뢰성을 나타내는 보안 토큰 인 폼 인증 티켓이 사용자에 게 부여 됩니다.

멤버 자격 프레임 워크에 대해 사용자의 유효성을 검사 하려면 `Membership` 클래스의 [ `ValidateUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)를 사용 합니다. `ValidateUser`메서드는 두 개의 입력 매개 변수 및을 사용 *`username`* *`password`* 하 고 자격 증명이 유효한 지 여부를 나타내는 부울 값을 반환 합니다. `CreateUser`이전 자습서에서 검사 한 메서드와 마찬가지로 `ValidateUser` 메서드는 실제 유효성 검사를 구성 된 멤버 자격 공급자에 게 위임 합니다.

는 `SqlMembershipProvider` 저장 프로시저를 통해 지정 된 사용자의 암호를 가져와서 제공 된 자격 증명의 유효성을 검사 합니다 `aspnet_Membership_GetPasswordWithFormat` . 는 `SqlMembershipProvider` 세 가지 형식 (clear, encrypted 또는 해시 됨) 중 하나를 사용 하 여 사용자의 암호를 저장 합니다. `aspnet_Membership_GetPasswordWithFormat`저장 프로시저는 원시 형식으로 암호를 반환 합니다. 암호화 되거나 해시 된 암호의 경우는 `SqlMembershipProvider` *`password`* 메서드에 전달 된 값을 해당 하는 `ValidateUser` 암호화 또는 해시 된 상태로 변환한 다음 데이터베이스에서 반환 된 것과 비교 합니다. 데이터베이스에 저장 된 암호가 사용자가 입력 한 형식이 지정 된 암호와 일치 하는 경우 자격 증명이 유효 합니다.

`Login.aspx`회원 프레임 워크 사용자 저장소에 대해 제공 된 자격 증명의 유효성을 검사 하도록 로그인 페이지 (~/)를 업데이트 해 보겠습니다. 이 로그인 페이지 <a id="Tutorial02"></a> 를 [*폼 인증 자습서 개요*](../introduction/an-overview-of-forms-authentication-cs.md) 로 돌아가, 사용자 이름 및 암호에 대해 두 개의 텍스트 상자를 사용 하 여 인터페이스를 만들고, 사용자 이름 및 로그인 단추를 선택 합니다 (그림 1 참조). 이 코드는 하드 코드 된 사용자 이름 및 암호 쌍의 하드 코드 된 목록에 대해 입력 한 자격 증명의 유효성을 검사 합니다 (Scott/password, Jisun/password 및 Sam/password). <a id="Tutorial03"></a> [*폼 인증 구성 및 고급 항목*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) 자습서에서는 폼 인증 티켓의 속성에 추가 정보를 저장 하도록 로그인 페이지의 코드를 업데이트 했습니다 `UserData` .

[![로그인 페이지의 인터페이스에는 두 개의 텍스트 상자, CheckBoxList 및 단추가 포함 됩니다.](validating-user-credentials-against-the-membership-user-store-cs/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image1.png)

**그림 1**: 로그인 페이지의 인터페이스에는 두 개의 텍스트 상자, CheckBoxList 및 단추가 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image3.png)).

로그인 페이지의 사용자 인터페이스는 변경 되지 않은 상태로 유지 될 수 있지만 `Click` 사용자의 유효성을 검사 하는 코드를 사용 하 여 사용자의 멤버 프레임 워크 사용자 저장소에 대해 로그인 단추의 이벤트 처리기를 바꾸어야 합니다. 해당 코드가 다음과 같이 표시 되도록 이벤트 처리기를 업데이트 합니다.

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample1.cs)]

이 코드는 매우 간단 합니다. 메서드를 호출 하 여 제공 된 사용자 이름과 암호를 전달 하는 것부터 시작 `Membership.ValidateUser` 합니다. 해당 메서드가 true를 반환 하는 경우 사용자는 `FormsAuthentication` 클래스의 RedirectFromLoginPage 메서드를 통해 사이트에 로그인 됩니다. (에서 <a id="Tutorial2"></a> 설명한 대로 [*폼 인증 자습서의 개요*](../introduction/an-overview-of-forms-authentication-cs.md) 에서는 `FormsAuthentication.RedirectFromLoginPage` 폼 인증 티켓을 만든 다음 사용자를 적절 한 페이지로 리디렉션합니다. 그러나 자격 증명이 유효 하지 않으면 `InvalidCredentialsMessage` 레이블이 표시 되어 사용자의 사용자 이름 또는 암호가 잘못 되었음을 사용자에 게 알립니다.

이것이 전부입니다!

로그인 페이지가 예상 대로 작동 하는지 테스트 하려면 이전 자습서에서 만든 사용자 계정 중 하나를 사용 하 여 로그인을 시도 합니다. 또는 계정을 아직 만들지 않은 경우 계속 진행 하 여 페이지에서 만듭니다 `~/Membership/CreatingUserAccounts.aspx` .

> [!NOTE]
> 사용자가 자신의 자격 증명을 입력 하 고 로그인 페이지 양식을 전송 하면 암호를 포함 한 자격 증명이 인터넷을 통해 웹 서버에 *일반 텍스트로*전송 됩니다. 즉, 네트워크 트래픽이 사용자 이름 및 암호를 볼 수 있음을 의미 합니다. 이를 방지 하기 위해서는 [SSL (Secure Socket 레이어)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)을 사용 하 여 네트워크 트래픽을 암호화 해야 합니다. 이렇게 하면 웹 서버에서 받을 때까지 브라우저를 떠날 때 자격 증명 (전체 페이지의 HTML 태그)이 암호화 됩니다.

### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>멤버 자격 프레임 워크에서 잘못 된 로그인 시도를 처리 하는 방법

방문자가 로그인 페이지에 도달 하 여 자격 증명을 전송 하면 브라우저에서 로그인 페이지에 대 한 HTTP 요청을 만듭니다. 자격 증명이 유효 하면 HTTP 응답은 쿠키에 인증 티켓을 포함 합니다. 따라서 사이트에 침입 하려는 해커는 유효한 사용자 이름 및 암호 추측을 사용 하 여 로그인 페이지에 HTTP 요청을 철저히 보내는 프로그램을 만들 수 있습니다. 암호 추측이 올바르면 로그인 페이지는 인증 티켓 쿠키를 반환 합니다 .이 쿠키는 프로그램에서 유효한 사용자 이름/암호 쌍에 대 한 stumbled 있음을 알고 있습니다. 무차별 암호 대입을 통해 이러한 프로그램은 사용자의 암호를 시 수 있습니다. 특히 암호가 취약 한 경우입니다.

이러한 무차별 암호 대입 공격을 방지 하기 위해 특정 기간 내에 로그인 시도가 실패 한 특정 횟수에 해당 하는 경우 멤버 자격 프레임 워크는 사용자를 잠급니다. 정확한 매개 변수는 다음 두 멤버 자격 공급자 구성 설정을 통해 구성할 수 있습니다.

- `maxInvalidPasswordAttempts` -계정을 잠그기 전 기간 내에 사용자에 게 허용 되는 잘못 된 암호 시도 횟수를 지정 합니다. 기본값은 5입니다.
- `passwordAttemptWindow` -지정 된 수의 잘못 된 로그인 시도로 인해 계정이 잠기는 시간 (분)을 나타냅니다. 기본값은 10입니다.

사용자가 잠긴 경우 관리자가 계정의 잠금을 해제할 때까지 로그인 할 수 없습니다. 사용자가 잠겨 있으면 `ValidateUser` *always* `false` 올바른 자격 증명이 제공 된 경우에도 메서드는 항상를 반환 합니다. 이 동작으로 인해 해커가 무차별 암호 대입 방법을 통해 사이트에 침입 하 게 될 가능성이 낮아집니다. 그러나 암호를 잊어버린 경우 나 실수로 실수로 Caps Lock을 사용 하거나 잘못 입력 한 요일이 있는 유효한 사용자를 잠글 수 있습니다.

아쉽게도 사용자 계정 잠금을 해제 하는 기본 제공 도구는 없습니다. 계정을 잠금 해제 하려면 데이터베이스를 수정할 수 있습니다 `IsLockedOut` `aspnet_Membership` . 적절 한 사용자 계정에 대 한 테이블의 필드를 직접 변경 하거나 잠금을 해제 하는 옵션을 사용 하 여 잠긴 계정을 나열 하는 웹 기반 인터페이스를 만들 수 있습니다. 이후 자습서에서 일반적인 사용자 계정 및 역할 관련 작업을 수행 하기 위한 관리 인터페이스 만들기를 살펴보겠습니다.

> [!NOTE]
> 메서드의 한 가지 단점은 `ValidateUser` 제공 된 자격 증명이 유효 하지 않은 경우 이유에 대 한 설명을 제공 하지 않는다는 것입니다. 사용자 저장소에 일치 하는 사용자 이름/암호 쌍이 없거나 사용자가 아직 승인 되지 않았거나 사용자가 잠겨 있어서 자격 증명이 유효 하지 않을 수 있습니다. 4 단계에서는 로그인 시도가 실패할 때 사용자에 게 더 자세한 메시지를 표시 하는 방법을 알아봅니다.

## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>2 단계: 로그인 웹 컨트롤을 통해 자격 증명 수집

[로그인 웹 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) 은 <a id="SKM5"></a> [*폼 인증 개요*](../introduction/an-overview-of-forms-authentication-cs.md) 자습서에서 만든 것과 매우 유사한 기본 사용자 인터페이스를 렌더링 합니다. 로그인 컨트롤을 사용 하면 방문자의 자격 증명을 수집 하는 인터페이스를 만드는 작업을 저장 합니다. 또한 로그인 컨트롤이 사용자에 게 자동으로 로그인 하 여 (제출 된 자격 증명이 유효 하다 고 가정) 코드를 작성 하지 않아도 됩니다.

`Login.aspx`수동으로 만든 인터페이스와 코드를 로그인 컨트롤로 바꿔서 업데이트 해 보겠습니다. 에서 기존 태그와 코드를 제거 하 여 시작 `Login.aspx` 합니다. 완전히 삭제 하거나 간단히 주석으로 처리할 수 있습니다. 선언적 태그를 주석으로 처리 하려면 `<%--` 및 구분 기호를 사용 하 여 묶습니다 `--%>` . 이러한 구분 기호를 수동으로 입력할 수도 있고, 그림 2에 표시 된 것 처럼 주석 처리할 텍스트를 선택한 다음 도구 모음에서 선택한 줄 주석 아이콘을 클릭할 수도 있습니다. 마찬가지로, 선택한 줄 주석 처리 아이콘을 사용 하 여 코드 숨김이 있는 클래스에서 선택한 코드를 주석으로 처리할 수 있습니다.

[![Login.aspx에서 기존 선언적 태그 및 소스 코드를 주석으로 처리 합니다.](validating-user-credentials-against-the-membership-user-store-cs/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image4.png)

**그림 2**:에서 기존 선언적 태그 및 소스 코드 주석 처리 `Login.aspx` ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image6.png))

> [!NOTE]
> Visual Studio 2005에서 선언 태그를 볼 때 선택한 줄 주석 주석 달기 아이콘을 사용할 수 없습니다. Visual Studio 2008을 사용 하지 않는 경우 `<%--` 및 구분 기호를 수동으로 추가 해야 합니다 `--%>` .

그런 다음 로그인 컨트롤을 도구 상자에서 페이지로 끌고 해당 `ID` 속성을로 설정 `myLogin` 합니다. 이 시점에서 화면은 그림 3과 유사 하 게 표시 됩니다. 로그인 컨트롤의 기본 인터페이스에는 사용자 이름 및 암호에 대 한 텍스트 상자 컨트롤, 나중에 암호 기억 확인란 및 로그인 단추가 포함 됩니다. 또한 `RequiredFieldValidator` 두 텍스트 상자에 대 한 컨트롤도 있습니다.

[![페이지에 로그인 컨트롤 추가](validating-user-credentials-against-the-membership-user-store-cs/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image7.png)

**그림 3**: 페이지에 로그인 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image9.png))

완료 되었습니다. 로그인 컨트롤의 로그인 단추를 클릭 하면 포스트백이 발생 하 고 로그인 컨트롤이 메서드를 호출 `Membership.ValidateUser` 하 여 입력 한 사용자 이름과 암호를 전달 합니다. 자격 증명이 유효 하지 않은 경우 로그인 컨트롤에 해당 메시지가 표시 됩니다. 그러나 자격 증명이 유효 하면 로그인 컨트롤이 폼 인증 티켓을 만들고 사용자를 적절 한 페이지로 리디렉션합니다.

로그인 컨트롤은 네 가지 요소를 사용 하 여 성공적으로 로그인 할 때 사용자를 리디렉션할 적절 한 페이지를 결정 합니다.

- 로그인 컨트롤이 폼 인증 구성에서 설정 하 여 정의 된 로그인 페이지에 있는지 여부 `loginUrl` 입니다 .이 설정의 기본값은입니다. `Login.aspx`
- `ReturnUrl`Querystring 매개 변수가 있는지 여부
- 로그인 컨트롤의 [ `DestinationUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx) 값입니다.
- `defaultUrl`폼 인증 구성 설정에 지정 된 값입니다 .이 설정의 기본값은입니다.`Default.aspx`

그림 4에서는 로그인 컨트롤에서 이러한 4 개의 매개 변수를 사용 하 여 적절 한 페이지 결정을 내리는 방법을 보여 줍니다.

[![페이지에 로그인 컨트롤 추가](validating-user-credentials-against-the-membership-user-store-cs/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image10.png)

**그림 4**: 페이지에 로그인 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image12.png))

잠시 시간을 내 서 브라우저를 통해 사이트를 방문 하 고 멤버 자격 프레임 워크에서 기존 사용자로 로그인 하 여 로그인 컨트롤을 테스트 합니다.

로그인 컨트롤의 렌더링 된 인터페이스는 매우 구성 가능 합니다. 모양에 영향을 주는 속성은 여러 가지가 있습니다. 자세히, 사용자 인터페이스 요소 레이아웃에 대 한 정확한 제어를 위해 로그인 컨트롤을 템플릿으로 변환할 수 있습니다. 이 단계의 나머지 부분에서는 모양 및 레이아웃을 사용자 지정 하는 방법을 살펴봅니다.

### <a name="customizing-the-login-controls-appearance"></a>로그인 컨트롤의 모양 사용자 지정

로그인 컨트롤의 기본 속성 설정은 제목 (로그인), 사용자 이름 및 암호 입력을 위한 텍스트 상자 및 레이블 컨트롤, 사용자 이름 및 암호 입력을 위한 레이블 컨트롤, 로그인 단추를 사용 하 여 사용자 인터페이스를 렌더링 합니다. 이러한 요소의 모양은 모두 로그인 컨트롤의 다양 한 속성을 통해 구성할 수 있습니다. 또한 새 사용자 계정을 만들기 위해 페이지에 대 한 링크와 같은 추가 사용자 인터페이스 요소를 추가 하 여 속성을 하나 또는 두 개 설정할 수 있습니다.

로그인 컨트롤의 모양을 gussy 하는 데 몇 분 정도 걸립니다. 페이지의 `Login.aspx` 페이지 맨 위에 login 이라는 텍스트가 이미 있으므로 로그인 컨트롤의 제목은 불필요 합니다. 따라서 로그인 컨트롤의 제목을 제거 하려면 [ `TitleText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx) 값을 지우십시오.

두 TextBox 컨트롤의 왼쪽에 있는 사용자 이름: 및 암호: 레이블은 [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) 각각 및 [ `PasswordLabelText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)을 통해 사용자 지정할 수 있습니다. 사용자 이름: Label을 변경 하 여 사용자 이름:을 읽습니다. 레이블 및 텍스트 상자 스타일은 [`LabelStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) 각각 및 [ `TextBoxStyle` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)을 통해 구성할 수 있습니다.

다음 시간 후 암호 확인란의 Text 속성은 로그인 컨트롤의를 통해 설정할 수 [`RememberMeText property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx) 있으며, 기본 선택 된 상태는 [`RememberMeSet property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx) (기본값은 False)을 통해 구성할 수 있습니다. 계속 해 서 속성을 True로 설정 하 여 나중에 나중에 `RememberMeSet` 암호 지정 확인란을 선택 합니다.

로그인 컨트롤은 사용자 인터페이스 컨트롤의 레이아웃을 조정 하기 위한 두 가지 속성을 제공 합니다. 는 [`TextLayout property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx) Username: 및 Password: 레이블이 해당 하는 텍스트 상자 (기본값)의 왼쪽에 표시 되는지 여부를 나타냅니다. 는 [`Orientation property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx) 사용자 이름 및 암호 입력이 세로 (다른 하나 위에 있는 경우) 또는 가로로 배치 되었는지 여부를 나타냅니다. 이러한 두 가지 속성을 기본값으로 설정 하지만 이러한 두 속성을 기본값이 아닌 값으로 설정 하 여 결과 효과를 확인 하는 것이 좋습니다.

> [!NOTE]
> 다음 섹션 로그인 컨트롤의 레이아웃 구성에서 템플릿 사용을 살펴보고 레이아웃 컨트롤의 사용자 인터페이스 요소에 대 한 정확한 레이아웃을 정의 합니다.

[`CreateUserText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx)및 [ `CreateUserUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx) 을 아직 등록 하지 않음으로 설정 하 여 로그인 컨트롤의 속성 설정을 래핑합니다. 계정 만들기 `~/Membership/CreatingUserAccounts.aspx`각각에 해당 합니다. 그러면 이전 자습서에서 만든 페이지를 가리키는 하이퍼링크가 로그인 컨트롤의 인터페이스에 추가 <a id="SKM6"></a> [preceding tutorial](creating-user-accounts-cs.md)됩니다. 로그인 컨트롤의 [`HelpPageText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx) 및 속성과 [ `HelpPageUrl` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx) [`PasswordRecoveryText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx) 및 [ `PasswordRecoveryUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx) 은 동일한 방식으로 작동 하며, 도움말 페이지 및 암호 복구 페이지에 대 한 링크를 렌더링 합니다.

이러한 속성을 변경한 후에는 로그인 컨트롤의 선언적 태그와 모양이 그림 5에 표시 된 것과 유사 하 게 표시 됩니다.

[![로그인 컨트롤의 속성 값이 모양을 지시 합니다.](validating-user-credentials-against-the-membership-user-store-cs/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image13.png)

**그림 5**: 로그인 컨트롤의 속성 값이 모양을 지시 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image15.png))

### <a name="configuring-the-login-controls-layout"></a>로그인 컨트롤의 레이아웃 구성

로그인 웹 컨트롤의 기본 사용자 인터페이스는 HTML에서 인터페이스를 배치 합니다 `<table>` . 그러나 렌더링 된 출력을 보다 세부적으로 제어 해야 하는 경우는 어떻게 되나요? 를 `<table>` 일련의 태그로 바꿀 수도 `<div>` 있습니다. 또는 응용 프로그램에 인증을 위해 추가 자격 증명이 필요한 경우 어떻게 하나요? 예를 들어 많은 금융 웹 사이트에서 사용자는 사용자 이름 및 암호 뿐만 아니라 개인 식별 번호 (PIN) 또는 기타 식별 정보를 제공 해야 합니다. 이유가 무엇이 든, 로그인 컨트롤을 템플릿으로 변환 하 여 인터페이스의 선언 태그를 명시적으로 정의할 수 있습니다.

추가 자격 증명을 수집 하도록 로그인 컨트롤을 업데이트 하기 위해 다음 두 가지 작업을 수행 해야 합니다.

1. 추가 자격 증명을 수집 하는 웹 컨트롤을 포함 하도록 로그인 컨트롤의 인터페이스를 업데이트 합니다.
2. 사용자의 사용자 이름과 암호가 올바르고 추가 자격 증명이 유효한 경우에만 사용자가 인증 되도록 로그인 컨트롤의 내부 인증 논리를 재정의 합니다.

첫 번째 작업을 수행 하려면 로그인 컨트롤을 템플릿으로 변환 하 고 필요한 웹 컨트롤을 추가 해야 합니다. 두 번째 작업의 경우, 컨트롤의 [ `Authenticate` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)에 대 한 이벤트 처리기를 만들어 로그인 컨트롤의 인증 논리를 대체 시킬 수 있습니다.

사용자의 사용자 이름, 암호 및 전자 메일 주소를 묻는 메시지를 표시 하 고 제공 된 전자 메일 주소가 파일의 전자 메일 주소와 일치 하는 경우에만 사용자를 인증 하도록 로그인 제어를 업데이트 해 보겠습니다. 먼저 로그인 컨트롤의 인터페이스를 템플릿으로 변환 해야 합니다. 로그인 컨트롤의 스마트 태그에서 템플릿으로 변환 옵션을 선택 합니다.

[![로그인 컨트롤을 템플릿으로 변환](validating-user-credentials-against-the-membership-user-store-cs/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image16.png)

**그림 6**: 로그인 컨트롤을 템플릿으로 변환 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image18.png))

> [!NOTE]
> 로그인 컨트롤을 템플릿 이전 버전으로 되돌리려면 컨트롤의 스마트 태그에서 다시 설정 링크를 클릭 합니다.

로그인 컨트롤을 템플릿으로 변환 하면 `LayoutTemplate` HTML 요소 및 사용자 인터페이스를 정의 하는 웹 컨트롤을 사용 하 여 컨트롤의 선언 태그에를 추가 합니다. 그림 7에 표시 된 것 처럼 컨트롤을 템플릿으로 변환 하면, 등의 다양 한 속성이 속성 창에서 제거 됩니다 `TitleText` `CreateUserUrl` . 이러한 속성 값은 템플릿을 사용할 때 무시 되기 때문입니다.

[![로그인 컨트롤이 템플릿으로 변환 될 때 사용할 수 있는 속성의 수를 줄입니다.](validating-user-credentials-against-the-membership-user-store-cs/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image19.png)

**그림 7**: 로그인 컨트롤이 템플릿으로 변환 될 때 사용할 수 있는 속성 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image21.png))

필요에 따라의 HTML 태그를 `LayoutTemplate` 수정할 수 있습니다. 마찬가지로 새 웹 컨트롤을 템플릿에 자유롭게 추가할 수 있습니다. 그러나 로그인 컨트롤의 핵심 웹 컨트롤은 템플릿에 유지 되 고 할당 된 값을 유지 하는 것이 중요 `ID` 합니다. 특히 `UserName` 또는 `Password` 텍스트 상자, `RememberMe` 확인란, `LoginButton` 단추, `FailureText` 레이블 또는 `RequiredFieldValidator` 컨트롤을 제거 하거나 이름을 변경 하지 마십시오.

방문자의 전자 메일 주소를 수집 하려면 템플릿에 텍스트 상자를 추가 해야 합니다. `<tr>`텍스트 상자를 포함 하는 테이블 행 () `Password` 과 다음 시간 후 저장 확인란을 포함 하는 테이블 행 사이에 다음 선언적 태그를 추가 합니다.

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample2.aspx)]

텍스트 상자를 추가한 후 `Email` 브라우저를 통해 페이지를 방문 합니다. 그림 8에 나와 있는 것 처럼 로그인 컨트롤의 사용자 인터페이스에는 이제 세 번째 텍스트 상자가 포함 되어 있습니다.

[![이제 로그인 컨트롤에 사용자 전자 메일 주소에 대 한 텍스트 상자가 포함 되어 있습니다.](validating-user-credentials-against-the-membership-user-store-cs/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image22.png)

**그림 8**: 이제 로그인 컨트롤에 사용자 전자 메일 주소에 대 한 텍스트 상자가 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image24.png)).

이 시점에서 로그인 컨트롤은 아직 메서드를 사용 하 여 `Membership.ValidateUser` 제공 된 자격 증명의 유효성을 검사 합니다. 마찬가지로 텍스트 상자에 입력 한 값은 `Email` 사용자가 로그인 할 수 있는지 여부에 관계 없이 사용 됩니다. 3 단계에서는 사용자 이름과 암호가 올바르고 제공 된 전자 메일 주소가 파일의 전자 메일 주소와 일치 하는 경우에만 자격 증명을 유효한 것으로 간주 하도록 로그인 컨트롤의 인증 논리를 재정의 하는 방법을 살펴보겠습니다.

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>3 단계: 로그인 컨트롤의 인증 논리 수정

방문자가 자격 증명을 제공 하 고 로그인 단추를 클릭 하면 다시 게시 ensues 및 로그인 제어가 인증 워크플로를 통해 진행 됩니다. [ `LoggingIn` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx)를 발생 시켜 워크플로를 시작 합니다. 이 이벤트와 연결 된 이벤트 처리기는 속성을로 설정 하 여 로그인 작업을 취소할 수 있습니다 `e.Cancel` `true` .

로그인 작업이 취소 되지 않으면 [ `Authenticate` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)를 발생 시켜 워크플로가 진행 됩니다. 이벤트에 대 한 이벤트 처리기가 있는 경우 `Authenticate` 제공 된 자격 증명이 유효한 지 여부를 확인 해야 합니다. 이벤트 처리기가 지정 되지 않은 경우 로그인 컨트롤은 메서드를 사용 하 여 `Membership.ValidateUser` 자격 증명의 유효성을 확인 합니다.

제공 된 자격 증명이 유효 하면 폼 인증 티켓이 만들어지고 [ `LoggedIn` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx) 발생 하며 사용자가 해당 페이지로 리디렉션됩니다. 그러나 자격 증명이 잘못 된 것으로 간주 되 면 [ `LoginError` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx) 발생 하 고 사용자에 게 자격 증명이 잘못 되었음을 알리는 메시지가 표시 됩니다. 기본적으로 실패 한 경우 로그인 컨트롤은 `FailureText` 레이블 컨트롤의 Text 속성을 오류 메시지로 설정 합니다. 로그인에 성공 하지 못했습니다. 다시 시도 하세요.) 그러나 Login 컨트롤의 [ `FailureAction` 속성이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx) 로 설정 된 경우에는 로그인 `RedirectToLoginPage` 컨트롤이 `Response.Redirect` querystring 매개 변수를 추가 하는 로그인 페이지에를 발급 합니다 `loginfailure=1` .이로 인해 로그인 컨트롤이 오류 메시지를 표시 합니다.

그림 9에서는 인증 워크플로의 순서도를 제공 합니다.

[![로그인 컨트롤의 인증 워크플로](validating-user-credentials-against-the-membership-user-store-cs/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image25.png)

**그림 9**: 로그인 컨트롤의 인증 워크플로 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image27.png))

> [!NOTE]
> `FailureAction`의 페이지 옵션을 사용 하는 경우 `RedirectToLogin` 다음 시나리오를 고려 하세요. `Site.master`현재 마스터 페이지에는 현재 익명 사용자가 방문 하는 경우 왼쪽 열에 표시 되는 텍스트, Hello, 낯선이 있지만 해당 텍스트를 로그인 컨트롤로 바꾸려고 한다고 가정 합니다. 이렇게 하면 익명 사용자가 로그인 페이지를 직접 방문 하도록 요구 하지 않고 사이트의 모든 페이지에서 로그인 할 수 있습니다. 그러나 사용자가 마스터 페이지에서 렌더링 된 로그인 컨트롤을 통해 로그인 할 수 없는 경우에는 해당 `Login.aspx` 페이지에 추가 지침, 링크 및 기타 도움말 (예: 새 계정 만들기 또는 분실 한 암호 검색에 대 한 링크)이 포함 될 수 있으므로이 페이지를 로그인 페이지 ()로 리디렉션하는 것이 좋을 수 있습니다.

### <a name="creating-theauthenticateevent-handler"></a>`Authenticate`이벤트 처리기 만들기

사용자 지정 인증 논리를 연결 하기 위해 로그인 컨트롤의 이벤트에 대 한 이벤트 처리기를 만들어야 `Authenticate` 합니다. 이벤트에 대 한 이벤트 처리기를 만들면 `Authenticate` 다음 이벤트 처리기 정의가 생성 됩니다.

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample3.cs)]

여기에서 볼 수 있듯이 `Authenticate` 이벤트 처리기는 형식의 개체를 [`AuthenticateEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx) 두 번째 입력 매개 변수로 전달 합니다. 클래스에는 `AuthenticateEventArgs` `Authenticated` 제공 된 자격 증명이 유효한 지 여부를 지정 하는 데 사용 되는 라는 부울 속성이 포함 되어 있습니다. 그런 다음 작업은 제공 된 자격 증명이 유효한 지 여부를 확인 하 고이에 따라 속성을 설정 하는 코드를 작성 하는 것입니다 `e.Authenticate` .

### <a name="determining-and-validating-the-supplied-credentials"></a>제공 된 자격 증명 확인 및 유효성 검사

로그인 컨트롤의 [`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx) 및 [ `Password` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx) 을 사용 하 여 사용자가 입력 한 사용자 이름 및 암호 자격 증명을 확인 합니다. 이전 단계에서 추가한 텍스트 상자와 같은 추가 웹 컨트롤에 입력 된 값을 확인 하려면 `Email` *`LoginControlID`* `.FindControl` ("")를 사용 하 여 속성이 인 *`controlID`* 템플릿의 웹 컨트롤에 대 한 프로그래밍 참조를 가져옵니다 `ID` *`controlID`* . 예를 들어 텍스트 상자에 대 한 참조를 가져오려면 `Email` 다음 코드를 사용 합니다.

`TextBox EmailTextBox = myLogin.FindControl("Email") as TextBox;`

사용자 자격 증명의 유효성을 검사 하기 위해 다음 두 가지 작업을 수행 해야 합니다.

1. 제공 된 사용자 이름 및 암호가 유효한 지 확인 합니다.
2. 입력 한 전자 메일 주소가 로그인을 시도 하는 사용자의 파일에 있는 전자 메일 주소와 일치 하는지 확인 합니다.

첫 번째 검사를 수행 하려면 `Membership.ValidateUser` 1 단계에서 본 것 처럼 메서드를 사용 하면 됩니다. 두 번째 확인의 경우 사용자의 전자 메일 주소를 확인 하 여 TextBox 컨트롤에 입력 한 전자 메일 주소와 비교할 수 있도록 해야 합니다. 특정 사용자에 대 한 정보를 가져오려면 `Membership` 클래스의 [ `GetUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)를 사용 합니다.

`GetUser`메서드에는 많은 오버 로드가 있습니다. 매개 변수를 전달 하지 않고 사용 하는 경우 현재 로그인 한 사용자에 대 한 정보를 반환 합니다. 특정 사용자에 대 한 정보를 가져오려면를 호출 하 여 사용자 `GetUser` 이름으로 전달 합니다. 어느 쪽이 든,,, `GetUser` 등과 같은 속성을 가진 [ `MembershipUser` 개체](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)를 반환 `UserName` `Email` `IsApproved` `IsOnline` 합니다.

다음 코드에서는 이러한 두 가지 검사를 구현 합니다. 둘 다 통과 하면 `e.Authenticate` 가로 설정 되 고, `true` 그렇지 않으면가 할당 됩니다 `false` .

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample4.cs)]

이 코드를 그대로 사용 하 고 올바른 사용자 이름, 암호 및 전자 메일 주소를 입력 하 여 유효한 사용자로 로그인 합니다. 다시 시도 하지만 이번에는 잘못 된 전자 메일 주소를 사용 합니다 (그림 10 참조). 마지막으로, 존재 하지 않는 사용자 이름을 사용 하 여 세 번째 시간을 시도 합니다. 첫 번째 경우에는 사이트에 성공적으로 로그온 해야 하지만 마지막 두 경우에는 로그인 컨트롤의 잘못 된 자격 증명 메시지가 표시 되어야 합니다.

[![잘못 된 전자 메일 주소를 제공 하면 tito에 로그인 할 수 없습니다.](validating-user-credentials-against-the-membership-user-store-cs/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image28.png)

**그림 10**: 잘못 된 전자 메일 주소를 제공 하는 경우 로그인 할 수 없음 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image30.png))

> [!NOTE]
> 1 단계의 잘못 된 로그인 시도를 처리 하는 방법 섹션에 설명 된 대로 `Membership.ValidateUser` 메서드를 호출 하 고 잘못 된 자격 증명을 전달 하면 잘못 된 로그인 시도를 추적 하 고 지정 된 기간 내에 잘못 된 시도의 특정 임계값을 초과 하는 경우 사용자를 잠급니다. 사용자 지정 인증 논리가 메서드를 호출 하기 때문에 `ValidateUser` 유효한 사용자 이름에 대해 잘못 된 암호를 입력 하면 잘못 된 로그인 시도 카운터가 증가 하지만 사용자 이름과 암호가 유효 하지만 전자 메일 주소가 잘못 된 경우에는이 카운터가 증가 하지 않습니다. 이 동작은 해커가 사용자 이름과 암호를 알고 있지만 무차별 암호 대입 기술을 사용 하 여 사용자의 이메일 주소를 확인 해야 하기 때문에 적합 합니다.

## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>4 단계: 로그인 컨트롤의 잘못 된 자격 증명 메시지 개선

사용자가 잘못 된 자격 증명을 사용 하 여 로그온을 시도 하는 경우 로그인 컨트롤은 로그인 시도가 실패 했음을 설명 하는 메시지를 표시 합니다. 특히 사용자의 로그인 시도에 대 한 기본값을 포함 하는 [ `FailureText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)으로 지정 된 메시지를 컨트롤에 표시 합니다. 다시 시도하세요.

사용자의 자격 증명이 유효 하지 않은 이유는 여러 가지가 있습니다.

- 사용자 이름이 없을 수 있습니다.
- 사용자 이름이 있지만 암호가 잘못 되었습니다.
- 사용자 이름 및 암호가 올바르지만 사용자가 아직 승인 되지 않은 경우
- 사용자 이름 및 암호가 올바르지만 사용자가 잠겨 있습니다 (지정 된 시간 프레임 내에 잘못 된 로그인 시도 횟수를 초과 했기 때문일 수 있음).

사용자 지정 인증 논리를 사용 하는 경우 다른 이유가 있을 수 있습니다. 예를 들어 3 단계에서 작성 한 코드를 사용 하는 경우 사용자 이름 및 암호는 유효 하지만 전자 메일 주소가 올바르지 않을 수 있습니다.

자격 증명이 유효 하지 않은 이유에 관계 없이 로그인 컨트롤은 같은 오류 메시지를 표시 합니다. 이러한 피드백이 아직 승인 되지 않았거나 잠긴 사용자의 경우 혼란 스 러 울 수 있습니다. 그러나 약간의 작업을 통해 로그인 컨트롤이 더 적절 한 메시지를 표시 하도록 할 수 있습니다.

사용자가 잘못 된 자격 증명으로 로그인을 시도할 때마다 로그인 컨트롤이 해당 이벤트를 발생 시킵니다 `LoginError` . 계속 해 서이 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample5.cs)]

위의 코드는 로그인 컨트롤의 속성을 기본값으로 설정 하 여 시작 됩니다 `FailureText` (로그인 시도가 실패 했습니다. 다시 시도 하세요.) 그런 다음 제공 된 사용자 이름이 기존 사용자 계정에 매핑되는지 여부를 확인 합니다. 그럴 경우 결과 `MembershipUser` 개체의 `IsLockedOut` 및 `IsApproved` 속성을 확인 하 여 계정이 잠겨 있거나 아직 승인 되지 않은 경우를 확인 합니다. 두 경우 모두 속성은 `FailureText` 해당 값으로 업데이트 됩니다.

이 코드를 테스트 하려면 의도적으로 기존 사용자로 로그인을 시도 하지만 잘못 된 암호를 사용 합니다. 10 분의 시간 프레임 내에 행에서이 작업을 5 번 수행 하면 계정이 잠깁니다. 그림 11에 표시 된 것 처럼 후속 로그인 시도는 항상 올바른 암호를 사용 하 여 실패 하지만 로그인 시도가 너무 많기 때문에 계정이 잠긴 것으로 표시 됩니다. 관리자에 게 문의 하 여 계정 잠금이 해제 된 메시지를 확인 하세요.

[![잘못 된 로그인 시도를 너무 많이 수행 하 여 잠 궜 습니다.](validating-user-credentials-against-the-membership-user-store-cs/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image31.png)

**그림 11**: 잘못 된 로그인 시도를 너무 많이 수행 하 여 잠금 ([전체 크기 이미지를 보려면 클릭](validating-user-credentials-against-the-membership-user-store-cs/_static/image33.png))

## <a name="summary"></a>요약

이 자습서 이전에는 로그인 페이지에서 하드 코드 된 사용자 이름/암호 쌍 목록에 대해 제공 된 자격 증명의 유효성을 검사 했습니다. 이 자습서에서는 멤버 자격 프레임 워크에 대 한 자격 증명의 유효성을 검사 하도록 페이지를 업데이트 했습니다. 1 단계에서는 `Membership.ValidateUser` 메서드를 프로그래밍 방식으로 사용 하는 방법을 살펴보았습니다. 2 단계에서 수동으로 만든 사용자 인터페이스와 코드를 로그인 컨트롤로 바꿨습니다.

로그인 컨트롤은 표준 로그인 사용자 인터페이스를 렌더링 하 고 멤버 자격 프레임 워크에 대해 사용자 자격 증명의 유효성을 자동으로 검사 합니다. 또한 유효한 자격 증명이 있는 경우 로그인 컨트롤은 폼 인증을 통해 사용자에 게 서명 합니다. 간단히 말해서, 로그인 컨트롤을 페이지에 끌어서 추가 선언적 태그나 코드를 추가 하지 않아도 완전 한 기능의 로그인 사용자 환경을 사용할 수 있습니다. 무엇 보다도 로그인 컨트롤은 사용자 지정이 가능 하므로 렌더링 된 사용자 인터페이스와 인증 논리를 세부적으로 제어할 수 있습니다.

이 시점에서 웹 사이트 방문자는 새 사용자 계정을 만들고 사이트에 로그인 할 수 있지만 인증 된 사용자를 기준으로 페이지에 대 한 액세스를 제한 하는 것을 확인 해야 합니다. 현재 인증 또는 익명의 모든 사용자는 사이트의 모든 페이지를 볼 수 있습니다. 사용자를 기준으로 사이트 페이지에 대 한 액세스를 제어 하는 것과 함께 해당 기능이 사용자에 따라 달라 지는 특정 페이지가 있을 수 있습니다. 다음 자습서에서는 로그인 한 사용자에 따라 액세스 및 페이지 내 기능을 제한 하는 방법을 보여 줍니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [잠긴 사용자 및 승인 되지 않은 사용자에 게 사용자 지정 메시지 표시](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [ASP.NET 2.0의 멤버 자격, 역할 및 프로필 검사](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [방법: ASP.NET 로그인 페이지 만들기](https://msdn.microsoft.com/library/ms178331.aspx)
- [로그인 컨트롤 기술 설명서](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [Login 컨트롤 사용](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>저자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은에서 또는의 블로그를 통해 연결할 수 있습니다 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) [http://ScottOnWriting.NET](http://scottonwriting.net/) .

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자는 Teresa Murphy 및 Michael Olivero입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 줄을에 놓습니다 [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com) .

> [!div class="step-by-step"]
> [이전](creating-user-accounts-cs.md)
> [다음](user-based-authorization-cs.md)
