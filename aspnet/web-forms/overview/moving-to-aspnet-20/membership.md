---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 멤버십 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 멤버십은 ASP.NET 1.x의 양식 인증 모델의 성공을 기반으로 합니다. ASP.NET Forms 인증은 인코프에 편리한 방법을 제공합니다...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: ed48c11cbd483de088239bad7c2452b7fc60a1cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543771"
---
# <a name="membership"></a>멤버 자격

[로 마이크로 소프트](https://github.com/microsoft)

> ASP.NET 멤버십은 ASP.NET 1.x의 양식 인증 모델의 성공을 기반으로 합니다. ASP.NET Forms 인증은 로그인 양식을 ASP.NET 응용 프로그램에 통합하고 데이터베이스 또는 기타 데이터 저장소에 대해 사용자의 유효성을 검사하는 편리한 방법을 제공합니다.

ASP.NET 멤버십은 ASP.NET 1.x의 양식 인증 모델의 성공을 기반으로 합니다. ASP.NET Forms 인증은 로그인 양식을 ASP.NET 응용 프로그램에 통합하고 데이터베이스 또는 기타 데이터 저장소에 대해 사용자의 유효성을 검사하는 편리한 방법을 제공합니다. FormsAuthentication 클래스의 구성원은 인증을 위해 쿠키를 처리하고, 유효한 로그인을 확인하고, 사용자를 로그아웃하는 등 가능합니다. 그러나 ASP.NET 1.x 응용 프로그램에서 양식 인증을 구현하려면 상당한 양의 코드가 필요할 수 있습니다.

ASP.NET 2.0의 멤버십은 Forms 인증만사용하는 데 큰 발전을 이없습니다. (멤버 자격은 Forms 인증과 결합될 때 가장 강력하지만 양식 인증을 사용하는 것은 필수 사항은 아닙니다.) 곧 볼 수 있듯이 ASP.NET 2.0의 ASP.NET 멤버십 및 로그인 컨트롤을 사용하여 많은 코드를 전혀 작성하지 않고도 강력한 멤버십 시스템을 구현할 수 있습니다.

## <a name="implementing-membership-in-aspnet-20"></a>ASP.NET 2.0에서 멤버십 구현

멤버십은 네 단계에 따라 구현됩니다. 관련된 많은 하위 단계와 구현할 수 있는 선택적 구성이 있습니다. 이 단계는 멤버십 구성의 큰 그림을 설명하기 위한 것입니다.

1. 멤버 자격 데이터베이스 만들기(SQL Server가 멤버 자격 저장소로 사용되는 경우).
2. 응용 프로그램 구성 파일에 멤버 자격 옵션을 지정합니다. (멤버십은 기본적으로 활성화되어 있습니다.)
3. 사용할 멤버 자격 저장소의 유형을 결정합니다. 사용할 수 있는 옵션은 다음과 같습니다. 

    - 마이크로소프트 SQL 서버(버전 7.0 이상)
    - Active 디렉토리 스토어
    - 사용자 지정 멤버십 공급자
4. ASP.NET 양식 인증에 대한 응용 프로그램을 구성합니다. 다시 한 번 멤버 자격은 양식 인증을 활용하도록 설계되었지만 양식 인증을 사용하는 것은 필수 사항은 아닙니다.
5. 구성원 자격에 대한 사용자 계정을 정의하고 원하는 경우 역할을 구성합니다.

## <a name="creating-the-membership-database"></a>멤버 자격 데이터베이스 만들기

SQL Server 7.0 이상을 멤버십 저장소로 사용하는 경우 aspnet\_regsql 유틸리티(Visual Studio .NET 2005 명령 프롬프트에서 가장 쉽게 사용 가능)를 사용하여 데이터베이스를 구성할 수 있습니다. aspnet\_regsql 유틸리티는 명령 프롬프트 도구 또는 GUI 마법사를 통해 사용할 수 있습니다. 마법사 방법은 데이터베이스를 구성하는 가장 쉬운 방법입니다. 마법사에 액세스하려면 다음 명령을 실행하기만 하면 됩니다.

`aspnet_regsql W`

이 명령을 실행하면 아래와 같이 ASP.NET SQL Server 설치 마법사가 표시됩니다.

![](membership/_static/image1.jpg)

**그림 1**

ASP.NET SQL Server 설치 마법사는 마법사에서 지정한 인스턴스에서 웹 사이트를 만듭니다. 그러나 ASP.NET machine.config 파일의 연결 문자열을 사용하여 데이터베이스에 연결합니다. 기본적으로 이 연결 문자열은 SQL Server 2005 인스턴스를 가리키므로 SQL Server 2000 또는 SQL Server 7.0 인스턴스를 사용하는 경우 machine.config 파일에서 연결 문자열을 수정해야 합니다. 해당 연결 문자열은 여기에 위치할 수 있습니다.

[!code-xml[Main](membership/samples/sample1.xml)]

안타깝게도 연결 문자열을 수정하지 않으면 ASP.NET 설명오류가 없습니다. 데이터베이스를 만들지 않았다고 불평하는 것은 계속됩니다. 위의 경우 로컬 SQL Server 2000 인스턴스를 가리키도록 연결 문자열을 수정했습니다.

## <a name="specifying-configuration-and-adding-users-and-roles"></a>구성 지정 및 사용자 및 역할 추가

멤버 자격을 구성하는 다음 단계는 응용 프로그램의 web.config 파일에 필요한 정보를 추가하는 것입니다. ASP.NET 1.x에서, web.config 파일을 수정하는 것은 낮은 CamelCase의 사용과 Intellisense의 부족으로 인해 때로는 어려웠다. Visual Studio .NET 2005를 사용하면 구성 파일에 대한 Intellisense를 사용하면 작업이 훨씬 쉬워지지만 ASP.NET 2.0은 구성 파일을 편집하기 위한 웹 인터페이스를 제공하여 한 단계 더 발전합니다.

아래와 같이 솔루션 탐색기 도구 모음에서 ASP.NET 구성 단추를 클릭하여 웹 인터페이스를 시작할 수 있습니다. 로그인 컨트롤을 삽입할 때 표시되는 팝업을 통해 웹 인터페이스를 시작할 수도 있습니다.

![](membership/_static/image2.jpg)

**그림 2**

이렇게 하면 아래 표시된 ASP.NET 웹 사이트 관리 도구가 시작됩니다. ASP.NET 웹 사이트 관리는 응용 프로그램 설정을 쉽게 관리할 수 있는 4탭 인터페이스입니다. 다음 탭을 사용할 수 있습니다.

- **홈**
- **보안 및 보안** 사용자, 역할 및 액세스를 구성합니다.
- **응용 프로그램** 응용 프로그램 설정을 구성합니다.
- **공급자** 응용 프로그램 멤버 자격 공급자를 구성하고 테스트합니다.

웹 사이트 관리 도구를 사용하면 새 사용자를 쉽게 만들고, 새 역할을 만들고, 사용자 및 역할을 관리할 수 있습니다. 이 기능은 Windows 인터페이스에서 사용할 수 없습니다. Windows 인터페이스를 사용하면 권한 부여 설정을 쉽게 정의하고 웹 사이트 관리 도구에 없는 공급자 기능을 추가, 삭제 및 관리할 수 있습니다.

Windows 인터페이스를 실행하려면 인터넷 정보 서비스 스냅인을 열고 응용 프로그램을 마우스 오른쪽 단추로 클릭하고 속성을 선택합니다. ASP.NET 탭을 클릭한 다음 구성 편집 단추를 클릭합니다. (구성 편집 단추를 사용하려면 응용 프로그램이 ASP.NET 2.0 에서 실행되어야 합니다. ASP.NET 대화 상자에서도 ASP.NET 버전을 구성할 수 있습니다. ASP.NET 구성 설정 대화 상자가 아래와 같이 표시됩니다.

![](membership/_static/image3.jpg)

**그림 3**

일반 탭에는 연결 문자열 및 응용 프로그램 설정이 나열됩니다. 기울임꼴의 모든 설정은 상위 구성 파일(machine.config 또는 상위 수준의 web.config)에 정의되며 기울임꼴이 아닌 설정은 응용 프로그램 구성 파일에서 가져옵니다. 응용 프로그램 수준에서 설정을 추가, 제거 또는 편집하는 경우 ASP.NET 응용 프로그램 수준에서 설정을 추가, 제거 또는 수정합니다.

인증 탭은 다음과 같습니다. 여기서 멤버십 설정을 구성합니다. 양식 인증 설정, 멤버 자격 공급자 및 역할 공급자는 여기에서 구성할 수 있습니다.

![](membership/_static/image4.jpg)

**그림 4**

## <a name="implementing-membership-in-your-application"></a>응용 프로그램에서 멤버십 구현

응용 프로그램에서 ASP.NET 2.0 멤버 자격을 구현하는 가장 쉬운 방법은 제공된 Logon 컨트롤을 사용하는 것입니다. 이 방법을 사용하면 코드를 전혀 작성하지 않고 ASP.NET 2.0 멤버 자격의 기본 사항을 구현할 수 있습니다.

다음 로그온 컨트롤은 ASP.NET 2.0에서 사용할 수 있습니다.

## <a name="login-control"></a>로그인 제어

로그인 컨트롤은 다른 사용자가 회원 시스템에 로그인할 수 있는 인터페이스를 제공합니다. 그것은 사용자 이름과 암호 텍스트 상자와 로그인 버튼을 제공합니다. 아직 등록하지 않은 사용자를 위해 등록할 수 있는 링크, 사용자가 후속 방문시 자동으로 로그인할 수 있는 확인란, 암호 미리 알림 링크 등과 같은 다른 많은 일반적인 기능. 로그인 컨트롤의 모든 기능은 컨트롤의 속성을 통해 사용자 지정할 수 있습니다.

ASP.NET 1.x에서 개발자는 Forms 인증을 사용할 때 조회를 수행하기 위해 상당한 양의 코드를 작성해야 했습니다. ASP.NET 2.0 멤버십을 사용하면 코드를 전혀 작성하지 않고도 사용자의 유효성을 검사할 수 있습니다. ASP.NET 자동으로 사용자의 조회를 수행합니다. ASP.NET 멤버 자격을 사용하지 않고 로그인 컨트롤을 사용하는 경우 **OnAuthenticate** 메서드를 사용하여 사용자의 유효성을 검사할 수 있습니다.

## <a name="loginview-control"></a>LoginView 컨트롤

LoginView 컨트롤은 기본적으로 두 개의 템플릿을 제공하는 템플릿 컨트롤입니다. 익명 템플릿 및 로그인 템플릿입니다. 표시되는 템플릿은 사용자가 멤버십 시스템에 로그인되었는지 여부에 따라 결정됩니다. 이 컨트롤은 일반적으로 사용자가 아직 로그인하지 않은 경우 로그인 컨트롤과 사용자가 로그인할 때 LoginStatus 컨트롤 및/또는 기타 로그인 컨트롤을 표시하는 데 사용됩니다. ASP.NET 응용 프로그램에서 역할 관리를 사용하는 경우 LoginView 컨트롤은 사용자 역할에 따라 특정 템플릿을 표시할 수 있습니다. (ASP.NET 역할 관리에 대한 자세한 내용은 나중에 다룹니다.)

## <a name="passwordrecovery-control"></a>암호 복구 제어

PasswordRecovery 컨트롤을 사용하면 사용자가 현재 암호로 이메일을 받거나 암호를 재설정할 수 있습니다. 일반 텍스트 및 암호화된 암호를 복구하여 사용자에게 이메일로 전송할 수 있습니다. 암호를 해시하면 복구할 수 없습니다. 대신 사용자가 암호 재설정을 수행해야 합니다.

## <a name="loginstatus-control"></a>로그인 상태 제어

로그인 상태 컨트롤은 로그인하지 않은 사용자에게 로그인 표시기와 현재 로그인한 사용자에게 로그아웃 표시기를 표시하는 데 사용됩니다. Request.Is인증 속성은 표시할 표시기를 결정하는 데 사용됩니다. LoginStatus 컨트롤에 의해 표시되는 표시기는 **텍스트(LoginText** 및 **LogoutText** 속성을 통해 구현됨) 또는 이미지(LoginImageUrl 및 **LogoutImageUrl** 속성을 통해 구현됨)일 수 있습니다. **LoginImageUrl**

사용자가 LoginStatus 컨트롤을 통해 로그아웃하면 **LogoutPageUrl** 속성에서 지정한 URL로 리디렉션됩니다. 해당 속성이 설정되지 않으면 현재 페이지가 새로 고쳐집니다. 사이트가 Forms 인증으로 보호될 가능성이 높므로 현재 페이지를 새로 고치면 사용자가 사이트의 로그인 페이지로 리디렉션됩니다.

## <a name="loginname-control"></a>로그인 이름 제어

LoginName 컨트롤은 현재 사이트에 로그인한 사용자의 사용자 이름을 표시합니다.

## <a name="createuserwizard-control"></a>사용자 마법사 컨트롤 만들기

CreateUserWizard 컨트롤은 사용자에게 멤버십 시스템에 등록할 수 있는 편리한 방법을 제공합니다. 아래 표시된 인터페이스를 통해 단계(WizardSteps의 컬렉션으로 구현)를 추가할 수 있습니다.

![](membership/_static/image5.jpg)

**그림 5**

CreateUserWizard는 마법사 클래스에서 파생된 템플릿 컨트롤이며 다음 템플릿을 제공합니다.

- **헤더 템플릿** 이 템플릿은 마법사의 헤더 모양을 제어합니다.
- **사이드바 템플릿** 이 템플릿은 마법사의 사이드바 모양을 제어합니다.
- **시작 탐색 템플릿** 이 템플릿은 시작 단계에서 마법사의 탐색 모양을 제어합니다.
- **스텝 내비게이션 템플릿** 이 템플릿은 시작 또는 완료 단계에 있지 않을 때 탐색 영역의 모양을 제어합니다.
- **완료 탐색 템플릿** 이 템플릿은 완료 단계에 있을 때 탐색 영역의 모양을 제어합니다.

또한 마법사에 추가하는 각 단계에 대해 ASP.NET 해당 단계에 대한 ContentTemplate 및 사용자 지정 탐색 템플릿을 모두 포함하는 사용자 지정 템플릿을 만듭니다. CreateUserWizard 사용자 지정에 대한 자세한 내용은 VS.NET 2005 설명서를 참조하십시오.

## <a name="changepassword-control"></a>변경 암호 제어

ChangePassword 컨트롤을 사용하면 사용자가 자신의 암호를 변경할 수 있습니다. DisplayUserName 속성이 true인 경우(기본적으로 false임) 사용자는 로그인하지 않은 경우 자신의 암호를 변경할 수 있습니다. *사용자가* 이미 로그인되어 있고 DisplayUserName 속성이 true인 경우 사용자는 해당 사용자의 사용자 ID를 알고 있는 경우 로그인되지 않은 다른 사용자의 암호를 변경할 수 있습니다.

사용자가 로그인하지 않고도 암호를 변경할 수 있도록 하려면 ChangePassword 컨트롤이 표시되는 페이지에서 익명 액세스를 허용하는지 확인해야 합니다. 분명히, 사용자는 자신의 암호를 변경하기 위해 자신의 이전 암호를 제공해야합니다.

## <a name="role-management"></a>역할 관리

역할 관리를 사용하면 특정 역할에 사용자를 할당한 다음 해당 역할에 따라 특정 파일 또는 폴더에 대한 액세스를 제한할 수 있습니다. 역할 관리는 또한 프로그래밍 방식으로 누군가 역할을 결정하거나 특정 역할의 모든 사용자를 결정하고 그에 따라 응답할 수 있도록 API를 제공합니다.

역할 관리는 ASP.NET 멤버 자격의 요구 사항이 아니며 역할 관리를 사용하기 위한 멤버 자격 요건도 아닙니다. 그러나, 두 잘 서로 보충 하 고 그것은 개발자가 서로 함께에서 그들을 사용 하는 가능성이 높습니다.

응용 프로그램에서 역할 관리를 활성화하려면 web.config 파일을 다음과 같은 변경합니다.

[!code-xml[Main](membership/samples/sample2.xml)]

**cacheRolesInCookie** 특성이 true로 설정되면 ASP.NET 클라이언트의 쿠키에서 사용자 역할 멤버 자격을 캐시합니다. 이렇게 하면 역할 공급자에 대 한 호출 없이 역할 조회를 수행할 수 있습니다. 이 특성을 사용하는 경우 개발자는 **cookieProtection** 특성이 모두로 설정되어 있는지 확인하는 것이 좋습니다. (기본 설정입니다.) 이렇게 하면 쿠키 데이터가 암호화되고 쿠키 내용이 변경되지 않았는지 확인하는 데 도움이 됩니다. 웹 사이트 관리 도구를 사용하여 역할을 추가할 수 있습니다. 이를 통해 역할을 쉽게 정의하고, 해당 역할에 따라 사이트의 일부에 대한 액세스를 구성하고, 사용자를 역할에 할당할 수 있습니다.

![](membership/_static/image6.jpg)

**그림 6**

위와 같이 역할 이름을 입력한 다음 역할 추가를 클릭하여 새 역할을 추가할 수 있습니다. 기존 역할 목록에서 적절한 링크를 클릭하여 기존 역할을 관리하거나 삭제할 수 있습니다.

역할을 관리할 때 아래와 같이 사용자를 추가하거나 제거할 수 있습니다.

![](membership/_static/image7.jpg)

**그림 7**

사용자가 역할에 있는 경우 확인란을 선택하면 특정 역할에 사용자를 쉽게 추가할 수 있습니다. ASP.NET 자동으로 적절한 항목으로 멤버 자격 데이터베이스를 업데이트합니다. 또한 응용 프로그램에 대한 액세스 규칙을 구성할 수도 있습니다. ASP.NET 1.x 개발자는 web.config &lt;&gt; 파일의 권한 부여 요소를 통해 이 작업을 수행하는 데 익숙하며 이 옵션은 ASP.NET 2.0에서 계속 사용할 수 있습니다. 그러나 아래와 같이 웹 사이트 관리 도구를 사용하여 액세스 규칙을 쉽게 관리할 수 있습니다.

![](membership/_static/image8.jpg)

**그림 8**

이 경우 관리 폴더가 강조 표시되고(도구가 밝은 회색으로 강조 표시되어 보기 어렵기 때문에 보기 어렵고) 관리자 역할에 액세스 권한이 부여되었습니다. 다른 모든 사용자는 거부됩니다. 머리 아이콘을 클릭하여 규칙을 선택한 다음 위로 이동 및 아래로 이동 단추를 사용하여 규칙을 정렬할 수 있습니다. ASP.NET &lt;권한 부여&gt; 요소와 마찬가지로 규칙은 표시되는 순서대로 처리됩니다. 즉, 위의 샷에서 규칙의 순서가 반대로 되면 ASP.NET 발생할 첫 번째 규칙은 모든 사람을 폴더에 거부하는 규칙이기 때문에 아무도 관리 폴더에 액세스할 수 없습니다.

ASP.NET 2.0은 액세스 규칙을 지정하는 폴더에 web.config 파일을 추가합니다. 액세스 규칙은 구성 파일을 통해 또는 웹 사이트 관리 도구를 통해 편집할 수 있습니다. 즉, 웹 사이트 관리 도구는 단순히 구성 파일을 사용자 친화적인 환경에서 편집할 수 있는 인터페이스입니다.

## <a name="using-roles-in-code"></a>코드에서 역할 사용

역할 관리를 위한 API는 버전 1.x 이후로 변경되지 않았습니다. **IsInRole** 메서드는 사용자가 특정 역할에 있는지 확인 하는 데 사용 됩니다.

[!code-csharp[Main](membership/samples/sample3.cs)]

ASP.NET 현재 컨텍스트의 구성원으로 RolePrincipal 인스턴스를 만듭니다. RolePrincipal 개체는 다음과 같이 사용자가 속한 모든 역할을 가져오는 데 사용할 수 있습니다.

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>로그인뷰 컨트롤에서 역할 그룹 사용

이제 역할 관리 및 구성원 자격에 대한 이해를 얻었으니 ASP.NET 2.0에서 LoginView 컨트롤이 이 기능을 활용하는 방법에 대해 간략하게 논의할 수 있습니다. 앞에서 설명한 것처럼 LoginView 컨트롤은 기본적으로 두 개의 템플릿을 포함하는 템플릿 컨트롤입니다. 익명 템플릿 및 로그인 템플릿입니다. LoginView 작업 대화 상자에는 역할 그룹을 편집할 수 있는 링크(아래 표시)가 있습니다.

![](membership/_static/image9.jpg)

**그림 9**

각 RoleGroup 개체에는 RoleGroup에 적용되는 역할을 정의하는 문자열 배열이 포함되어 있습니다. 로그인뷰 컨트롤에 새 역할 그룹을 추가하려면 역할 그룹 편집 링크를 클릭합니다. 위의 이미지에서 관리자를 위한 새 역할 그룹을 추가한 것을 볼 수 있습니다. 보기 드롭다운에서 역할 그룹(역할 그룹[0])을 선택하면 관리자 역할의 구성원에게만 표시되는 템플릿을 구성할 수 있습니다. 아래 이미지에서 영업 역할 및 배포 역할의 구성원에 적용되는 새 역할 그룹을 추가했습니다. 이렇게 하면 LoginView 작업 대화 상자의 보기 드롭다운에 두 번째 역할 그룹이 추가되고 해당 템플릿에 추가된 모든 항목이 판매 또는 배포 역할의 모든 사용자가 볼 수 있습니다.

![](membership/_static/image10.jpg)

**그림 10**

## <a name="overriding-the-existing-membership-provider"></a>기존 멤버십 공급자 재정의

ASP.NET 멤버십의 기능을 확장할 수 있는 방법에는 여러 가지가 있습니다. 우선, SqlMembershipProvider 클래스의 기존 기능을 상속 하 고 메서드를 재정의 하 여 분명히 변경할 수 있습니다. 예를 들어 사용자를 만들 때 사용자 고유의 기능을 구현하려는 경우 다음과 같이 SqlMembershipProvider에서 상속하는 고유한 클래스를 만들 수 있습니다.

[!code-csharp[Main](membership/samples/sample5.cs)]

반면에 Access 데이터베이스에 멤버십 정보를 저장하기 위해 사용자 고유의 공급자를 만들려면 사용자 고유의 공급자를 만들 수 있습니다.

## <a name="creating-your-own-membership-provider"></a>나만의 멤버십 공급자 만들기

고유한 멤버 자격 공급자를 만들려면 먼저 멤버 자격 공급자 클래스에서 상속하는 클래스를 만들어야 합니다. VB.NET 사용하는 경우 Visual Studio 2005는 재정의해야 하는 모든 메서드에 대한 스텁을 추가합니다. C#을 사용하는 경우 스텁을 추가하는 데 사용됩니다.

다음을 재정의해야 합니다.

- 응용 프로그램 이름 속성
- 변경암호 기능
- 변경암호질문및답변기능
- 사용자 만들기 기능 만들기
- 삭제사용자 기능
- 사용 암호 다시 설정 속성
- 사용암호 복구 속성
- 찾기사용자비이메일 기능
- FindUsersByName 기능
- GetAllUsers 기능
- 겟넘사용자온라인 기능
- GetPassword 기능
- GetUser 기능
- GetuserNameBy이메일 기능
- 맥스유효암호시도 속성
- MinRequiredNonAlphanumeric문자 속성
- MinRequired암호길이 속성
- 암호 시도창 속성
- 암호 형식 속성
- 암호강도 정규표현식 속성
- 요구질문앤답변 속성
- 요구고유 이메일 속성
- 암호 재설정 기능
- 사용자 기능 잠금 해제
- 업데이트사용자 기능
- 유효성 검사사용자 기능

C# 개발자로 구현할 목록은 꽤 큽입니다. 구현 없이 VB.NET 클래스를 만든 다음 .NET 리플렉터 또는 유사한 도구를 사용하여 코드를 C#으로 변환하는 것이 더 쉬울 수 있습니다.

연결 문자열 및 기타 속성은 Initialize 메서드에서 기본값으로 설정해야 합니다. 초기화 메서드는 공급자가 런타임에 로드될 때 발생합니다. Initialize 메서드에 대 한 두 번째 매개 변수는 유형 System.Collections.Specialized.NameValueCollection 이며 web.config 파일에서 사용자 지정 공급자와 연결 된 &lt;추가&gt; 요소에 대 한 참조입니다. 해당 항목은 다음과 같습니다.

[!code-xml[Main](membership/samples/sample6.xml)]

다음은 초기화 방법의 예입니다.

[!code-csharp[Main](membership/samples/sample7.cs)]

사용자가 로그인 양식을 제출할 때 유효성을 검사하려면 ValidateUser 메서드를 사용해야 합니다. 이 메서드는 사용자가 로그인 컨트롤에서 로그인 단추를 클릭하면 발생합니다. 이 메서드에서 사용자 조회를 수행하는 코드를 배치합니다.

보시다시피, 자신의 멤버십 공급자를 작성하는 것은 어렵지 않으며 ASP.NET 2.0의 이 강력한 기능을 확장할 수 있습니다.
