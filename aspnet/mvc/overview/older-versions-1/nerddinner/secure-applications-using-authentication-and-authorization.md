---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 인증 및 권한 부여를 사용한 안전한 응용 프로그램 | 마이크로 소프트 문서
author: rick-anderson
description: 9단계는 NerdDinner 응용 프로그램을 보호하기 위해 인증 및 인증을 추가하는 방법을 보여 주므로 사용자가 사이트에 등록하고 로그인하여 만들 수 있습니다...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: d96f2763f6e62f9dd599fdb7977a97993d218305
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542575"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>인증 및 권한 부여를 사용하여 애플리케이션 보호

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 9단계입니다.
> 
> 9단계는 사용자가 새 저녁 식사를 만들기 위해 사이트에 등록하고 로그인해야 하며 저녁 식사를 주최하는 사용자만 나중에 편집할 수 있도록 NerdDinner 응용 프로그램을 보호하기 위해 인증 및 권한 부여를 추가하는 방법을 보여 주며, 이 에 대해 설명합니다.
> 
> MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner 단계 9: 인증 및 권한 부여

지금 우리의 NerdDinner 응용 프로그램은 사이트를 방문하는 모든 사람에게 모든 저녁 식사의 세부 사항을 만들고 편집 할 수있는 기능을 부여합니다. 사용자가 새 저녁 식사를 만들기 위해 사이트에 등록하고 로그인해야 하고, 저녁 식사를 주최하는 사용자만 나중에 편집할 수 있도록 제한을 추가해야 하도록 이 변경을 해 보겠습니다.

이를 위해 인증 및 인증을 사용하여 응용 프로그램을 보호합니다.

### <a name="understanding-authentication-and-authorization"></a>인증 및 권한 부여 이해

*인증은* 응용 프로그램에 액세스하는 클라이언트의 ID를 식별하고 유효성을 검사하는 프로세스입니다. 간단히 말해서, 최종 사용자가 웹 사이트를 방문 할 때 "누가"를 식별하는 것입니다. ASP.NET 브라우저 사용자를 인증하는 여러 가지 방법을 지원합니다. 인터넷 웹 응용 프로그램의 경우 가장 일반적인 인증 방법을 "양식 인증"이라고 합니다. 양식 인증을 사용하면 개발자가 응용 프로그램 내에서 HTML 로그인 양식을 작성한 다음 최종 사용자가 데이터베이스 또는 다른 암호 자격 증명 저장소에 대해 제출하는 사용자 이름/암호의 유효성을 검사할 수 있습니다. 사용자 이름/암호 조합이 올바른 경우 개발자는 ASP.NET 암호화된 HTTP 쿠키를 발급하여 향후 요청에서 사용자를 식별하도록 요청할 수 있습니다. 우리는 우리의 NerdDinner 응용 프로그램과 양식 인증을 사용하여 합니다.

*권한 부여는* 인증된 사용자가 특정 URL/리소스에 액세스하거나 일부 작업을 수행할 수 있는 권한이 있는지 여부를 결정하는 프로세스입니다. 예를 들어 NerdDinner 응용 프로그램 내에서 로그인한 사용자만 */Dinners/Create* URL에 액세스하고 새 Dinners를 만들 수 있는 권한을 부여합니다. 또한 저녁 식사를 주최하는 사용자만 편집하고 다른 모든 사용자에 대한 편집 액세스를 거부할 수 있도록 권한 부여 논리를 추가하려고 합니다.

### <a name="forms-authentication-and-the-accountcontroller"></a>양식 인증 및 계정 컨트롤러

ASP.NET MVC에 대한 기본 Visual Studio 프로젝트 템플릿은 새 ASP.NET MVC 응용 프로그램을 만들 때 양식 인증을 자동으로 활성화합니다. 또한 미리 빌드된 계정 로그인 페이지 구현을 프로젝트에 자동으로 추가하여 사이트 내에서 보안을 쉽게 통합할 수 있습니다.

기본 Site.master 마스터 페이지에는 사용자가 인증되지 않을 때 사이트의 오른쪽 상단에 "로그온" 링크가 표시됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

"로그온" 링크를 클릭하면 사용자가 */계정/로그온* URL로 이동합니다.

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

등록하지 않은 방문자는 "등록" 링크를 클릭하여 */Account/Register* URL로 이동하여 계정 세부 정보를 입력할 수 있습니다.

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

"등록" 버튼을 클릭하면 ASP.NET 멤버십 시스템 내에서 새 사용자가 생성되고 양식 인증을 사용하여 사이트에 사용자를 인증합니다.

사용자가 로그인하면 Site.master가 페이지의 오른쪽 상단을 변경하여 "환영[사용자 이름]"을 출력합니다. "로그온" 링크 대신 "로그오프" 링크를 렌더링합니다. "로그 오프" 링크를 클릭하면 사용자가 로그아웃됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

위의 로그인, 로그아웃 및 등록 기능은 프로젝트를 만들 때 Visual Studio에서 프로젝트에 추가한 AccountController 클래스 내에서 구현됩니다. AccountController의 UI는 \Views\Account 디렉터리 내의 보기 템플릿을 사용하여 구현됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

AccountController 클래스는 ASP.NET 양식 인증 시스템을 사용하여 암호화된 인증 쿠키를 발급하고 ASP.NET 멤버 자격 API를 사용하여 사용자 이름/암호를 저장하고 유효성을 검사합니다. ASP.NET 멤버 자격 API는 확장 가능하며 모든 암호 자격 증명 저장소를 사용할 수 있습니다. ASP.NET SQL 데이터베이스 또는 Active Directory 내에서 사용자 이름/암호를 저장하는 기본 제공 멤버 자격 공급자 구현과 함께 제공됩니다.

NerdDinner 응용 프로그램이 프로젝트의 루트에서 "web.config" 파일을 열고 그 안에 있는 멤버십 섹션을 &lt;&gt; 찾아서 사용해야 하는 멤버십 공급자를 구성할 수 있습니다. 프로젝트를 만들 때 추가된 기본 web.config는 SQL 멤버 자격 공급자를 등록하고 데이터베이스 위치를 지정하기 위해 "ApplicationServices"라는 연결 문자열을 사용하도록 구성합니다.

기본 "ApplicationServices" 연결 &lt;문자열(web.config 파일의 연결 Strings&gt; 섹션 내에 지정됨)은 SQL Express를 사용하도록 구성됩니다. "ASPNETDB"라는 SQL Express 데이터베이스를 가리킵니다. 응용 프로그램의 "앱\_데이터" 디렉토리 아래에 있는 MDF"입니다. 이 데이터베이스가 응용 프로그램 내에서 처음으로 멤버 자격 API를 사용할 때 존재하지 않는 경우 ASP.NET 자동으로 데이터베이스를 만들고 해당 데이터베이스 내에 적절한 멤버 자격 데이터베이스 스키마를 프로비전합니다.

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

SQL Express를 사용하는 대신 전체 SQL Server 인스턴스를 사용하거나 원격 데이터베이스에 연결하려는 경우 web.config 파일 내의 "ApplicationServices" 연결 문자열을 업데이트하고 해당 구성 설정 스키마가 가리키는 데이터베이스에 추가되었는지 확인하는 것만하면 됩니다. \Windows\Microsoft.NET\Framework\v2.0.50727\ 디렉터리 내에서 "aspnet\_regsql.exe" 유틸리티를 실행하여 멤버 자격및 기타 ASP.NET 응용 프로그램 서비스에 적합한 스키마를 데이터베이스에 추가할 수 있습니다.

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>[권한 부여] 필터를 사용하여 /Dinners/URL 만들기 권한 부여

NerdDinner 응용 프로그램에 대한 보안 인증 및 계정 관리 구현을 활성화하기 위해 코드를 작성할 필요가 없었습니다. 사용자는 당사의 애플리케이션에 새 계정을 등록하고 사이트의 로그인/로그아웃을 할 수 있습니다.

이제 응용 프로그램에 권한 부여 논리를 추가하고 방문자의 인증 상태 및 사용자 이름을 사용하여 사이트 내에서 수행할 수 있는 것과 수행할 수 없는 작업을 제어할 수 있습니다. 먼저 DinnersController 클래스의 "만들기" 작업 메서드에 권한 부여 논리를 추가합니다. 특히 */Dinners/Create* URL에 액세스하는 사용자가 로그인해야 합니다. 로그인하지 않은 경우 로그인할 수 있도록 로그인 페이지로 리디렉션됩니다.

이 논리를 구현하는 것은 매우 쉽습니다. 우리가해야 할 일은 다음과 같은 작업 메서드 만들기에 [권한 부여] 필터 특성을 추가하는 것입니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC는 작업 메서드에 선언적으로 적용할 수 있는 재사용 가능한 논리를 구현하는 데 사용할 수 있는 "작업 필터"를 만드는 기능을 지원합니다. [권한 부여] 필터는 ASP.NET MVC에서 제공하는 기본 제공 작업 필터 중 하나이며 개발자가 작업 메서드 및 컨트롤러 클래스에 권한 부여 규칙을 선언적으로 적용할 수 있습니다.

[위와 같은) 매개 변수 없이 적용하면 [권한 부여] 필터는 작업 메서드 요청을 하는 사용자가 로그인해야 하며 그렇지 않은 경우 자동으로 로그인 URL로 브라우저를 리디렉션합니다. 이 작업을 수행 할 때 원래 요청된 URL은 쿼리 문자열 인수로 전달됩니다 (예 : /Account / LogOn? ReturnUrl =%2fDinners%2fCreate). 그러면 AccountController는 사용자가 로그인한 후 원래 요청한 URL로 다시 리디렉션됩니다.

[권한 부여] 필터는 선택적으로 사용자가 로그인하고 허용된 사용자 또는 허용된 보안 역할의 구성원 목록에 로그인하도록 요구하는 데 사용할 수 있는 "사용자" 또는 "역할" 속성을 지정하는 기능을 지원합니다. 예를 들어 아래 코드는 "scottgu" 및 "billg"이라는 두 명의 특정 사용자만 /Dinners/Create URL에 액세스할 수 있도록 허용합니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

코드 내에 특정 사용자 이름을 포함시키는 것은 유지 관리가 불가능한 경향이 있습니다. 더 나은 방법은 코드가 검사하는 상위 수준 "역할"을 정의한 다음 데이터베이스 또는 활성 디렉터리 시스템을 사용하여 사용자를 역할에 매핑하는 것입니다(실제 사용자 매핑 목록을 코드에서 외부로 저장할 수 있음). ASP.NET 기본 제공 역할 관리 API뿐만 아니라 이 사용자/역할 매핑을 수행하는 데 도움이 되는 기본 제공 역할 공급자(SQL 및 Active Directory용 역할 공급자 포함)가 포함되어 있습니다. 그런 다음 코드를 업데이트하여 특정 "관리자" 역할 내의 사용자가 /Dinners/Create URL에 액세스할 수 있도록 허용할 수 있습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>저녁 식사 만들기 시 User.Identity.Name 속성 사용

Controller 기본 클래스에 노출된 User.Identity.Name 속성을 사용하여 현재 로그인한 요청 사용자의 사용자 이름을 검색할 수 있습니다.

이전에 Create() 작업 메서드의 HTTP-POST 버전을 구현할 때 Dinner의 "HostedBy" 속성을 정적 문자열로 하드 코딩했습니다. 이제 이 코드를 업데이트하여 User.Identity.Name 속성을 사용하고 Dinner를 만드는 호스트에 대한 RSVP를 자동으로 추가할 수 있습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

Create() 메서드에 [권한 부여] 특성을 추가했기 때문에 mVC를 ASP.NET 사용자가 /Dinners/Create URL을 방문하는 사용자가 사이트에 로그인한 경우에만 작업 메서드가 실행되도록 합니다. 따라서 User.Identity.Name 속성 값에는 항상 유효한 사용자 이름이 포함됩니다.

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>저녁 식사 편집 시 User.Identity.Name 속성 사용

이제 사용자가 호스팅하는 저녁 식사의 속성만 편집할 수 있도록 사용자를 제한하는 권한 부여 논리를 추가해 보겠습니다.

이를 위해 먼저 Dinner 개체에 "IsHostedBy(사용자 이름)" 도우미 메서드를 추가합니다(이전에 빌드한 Dinner.cs 부분 클래스 내에서). 이 도우미 메서드는 제공된 사용자 이름이 Dinner HostedBy 속성과 일치하는지 여부에 따라 true 또는 false를 반환하고 대/소문자를 구분하지 않음 문자열 비교를 수행하는 데 필요한 논리를 캡슐화합니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

그런 다음 DinnersController 클래스 내에서 편집() 작업 메서드에 [권한 부여] 특성을 추가합니다. 이렇게 하면 *사용자가 /Dinners/편집/[id] URL을* 요청하기 위해 로그인해야 합니다.

그런 다음 Dinner.IsHostedBy(사용자 이름) 도우미 메서드를 사용하는 편집 메서드에 코드를 추가하여 로그인한 사용자가 Dinner 호스트와 일치하는지 확인할 수 있습니다. 사용자가 호스트가 아닌 경우 "잘못된 소유자" 보기가 표시되고 요청을 종료합니다. 이 작업을 수행하는 코드는 다음과 같습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

그런 다음 \View\Dinners 디렉토리를 마우스 오른쪽 단추로 클릭하고 추가&gt;보기 메뉴 명령을 선택하여 새 "잘못된 소유자" 보기를 만들 수 있습니다. 아래 오류 메시지로 채워집니다.

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

이제 사용자가 소유하지 않은 저녁 식사를 편집하려고 하면 다음과 같은 오류 메시지가 표시됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

컨트롤러 내에서 Delete() 작업 메서드에 대해 동일한 단계를 반복하여 Dinners를 삭제할 수 있는 권한도 잠그고 Dinner의 호스트만 삭제할 수 있도록 할 수 있습니다.

### <a name="showinghiding-edit-and-delete-links"></a>링크 표시/숨기기 편집 및 삭제

세부 정보 URL에서 DinnersController 클래스의 편집 및 삭제 작업 메서드에 연결됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

현재 세부 정보 URL에 대한 방문자가 저녁 식사의 호스트인지 여부에 관계없이 편집 및 삭제 작업 링크가 표시됩니다. 방문 하는 사용자가 dinner의 소유자 인 경우에 링크 표시 되도록이 변경 해 보겠습니다.

DinnersController 내의 Details() 작업 메서드는 Dinner 개체를 검색한 다음 뷰 템플릿에 모델 개체로 전달합니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

아래와 같은 Dinner.IsHostedBy() 도우미 방법을 사용하여 보기 템플릿을 업데이트하여 편집 및 삭제 링크를 조건부로 표시/숨길 수 있습니다.

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>다음 단계

이제 인증된 사용자가 AJAX를 사용하여 저녁 식사를 위해 RSVP로 사용할 수 있는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](implement-efficient-data-paging.md)
> [다음](use-ajax-to-deliver-dynamic-updates.md)
