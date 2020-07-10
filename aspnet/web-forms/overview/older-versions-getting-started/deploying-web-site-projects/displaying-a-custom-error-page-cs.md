---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
title: '사용자 지정 오류 페이지 표시 (c #) | Microsoft Docs'
author: rick-anderson
description: ASP.NET 웹 응용 프로그램에서 런타임 오류가 발생할 때 사용자에 게 표시 되는 것은 무엇 인가요? 해답은 웹 사이트의 &lt; customErrors 구성 방법에 따라 달라 집니다. &gt;
ms.author: riande
ms.date: 06/09/2009
ms.assetid: cb061642-faf3-41b2-9372-69e13444d458
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/displaying-a-custom-error-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 777948732690443d63f1fb2afd6f72a33a496c44
ms.sourcegitcommit: 0d583ed9253103f3e50b6d729276e667591cdd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86211054"
---
# <a name="displaying-a-custom-error-page-c"></a>사용자 지정 오류 페이지 표시(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_11_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial11_CustomErrors_cs.pdf)

> ASP.NET 웹 응용 프로그램에서 런타임 오류가 발생할 때 사용자에 게 표시 되는 것은 무엇 인가요? 해답은 웹 사이트의 customErrors 구성 방법에 따라 달라 집니다 &lt; &gt; . 기본적으로 사용자는 런타임 오류가 발생 한 것으로 unsightly 노란색 화면 표시를 표시 합니다. 이 자습서에서는 사이트의 모양과 느낌에 맞는 멋지고-보기 편 사용자 지정 오류 페이지를 표시 하도록 이러한 설정을 사용자 지정 하는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

완벽 한 세계에서는 런타임 오류가 발생 하지 않습니다. 프로그래머는 nary a 버그와 강력한 사용자 입력 유효성 검사를 사용 하 여 코드를 작성 하 고, 데이터베이스 서버 및 전자 메일 서버와 같은 외부 리소스는 오프 라인 상태가 되지 않습니다. 물론 실제 오류는 피할 수 있습니다. .NET Framework의 클래스는 예외를 throw 하 여 오류를 신호로 알립니다. 예를 들어, SqlConnection 개체의 Open 메서드를 호출 하면 연결 문자열에 지정 된 데이터베이스에 대 한 연결이 설정 됩니다. 그러나 데이터베이스가 다운 되거나 연결 문자열의 자격 증명이 유효 하지 않은 경우 Open 메서드는을 throw `SqlException` 합니다. 블록을 사용 하 여 예외를 처리할 수 있습니다 `try/catch/finally` . 블록 내의 코드가 `try` 예외를 throw 하는 경우 개발자가 오류 로부터 복구를 시도할 수 있는 적절 한 catch 블록으로 제어가 전송 됩니다. 일치 하는 catch 블록이 없거나 예외를 throw 한 코드가 try 블록에 없는 경우 예외는 블록 검색에서 호출 스택을 처리 합니다 `try/catch/finally` .

예외가 처리 되지 않고 ASP.NET 런타임으로 모든 방식으로 버블링 되 면 [ `HttpApplication` 클래스](https://msdn.microsoft.com/library/system.web.httpapplication.aspx)의 [ `Error` 이벤트가](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx) 발생 하 고 구성 된 *오류 페이지가* 표시 됩니다. 기본적으로 ASP.NET는 affectionately [노랑 화면](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow) 으로 참조 되는 오류 페이지를 표시 합니다. YSOD는 두 가지 버전이 있습니다. 하나는 예외 정보, 스택 추적 및 응용 프로그램을 디버깅 하는 개발자에 게 유용한 기타 정보를 보여 줍니다 ( **그림 1**참조). 다른 것은 런타임 오류가 있음을 나타내는 것입니다 ( **그림 2**참조).

예외 세부 정보는 응용 프로그램을 디버깅 하는 개발자에 게 매우 유용 하지만 최종 사용자에 게는 tacky 및 전문적를 표시 합니다. 대신 최종 사용자는 상황을 설명 하는 보다 사용자에 게 친숙 한 prose 사이트의 모양과 느낌을 유지 관리 하는 오류 페이지로 이동 해야 합니다. 이러한 사용자 지정 오류 페이지를 만드는 것은 매우 간단 합니다. 이 자습서는 ASP를 살펴보세요. 네트워크의 다른 오류 페이지. 그런 다음 오류 발생 시 사용자 지정 오류 페이지를 표시 하도록 웹 응용 프로그램을 구성 하는 방법을 보여 줍니다.

### <a name="examining-the-three-types-of-error-pages"></a>세 가지 유형의 오류 페이지 검사

ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 하면 다음과 같은 세 가지 유형의 오류 페이지 중 하나가 표시 됩니다.

- 예외 세부 정보 화면에서 오류 발생 페이지,
- 오류 메시지 페이지의 런타임 오류 노란색 화면 또는
- 사용자 지정 오류 페이지

개발자가 가장 잘 알고 있는 오류 페이지는 예외 정보입니다. 기본적으로이 페이지는 로컬에서 방문 하는 사용자에 게 표시 되므로 개발 환경에서 사이트를 테스트할 때 오류가 발생할 때 표시 되는 페이지입니다. 이름에서 알 때 예외 정보는 예외에 대 한 세부 정보를 제공 합니다. 형식, 메시지 및 스택 추적입니다. ASP.NET 페이지의 코드 숨김 클래스에서 코드에 의해 예외가 발생 하 고 디버깅을 위해 응용 프로그램을 구성한 경우 예외 세부 정보에도이 코드 줄이 표시 됩니다 (위 및 아래에 몇 줄의 코드가 표시 됨).

**그림 1** 에서는 예외 세부 정보 페이지를 보여 줍니다. 브라우저의 주소 창에 있는 URL을 확인 `http://localhost:62275/Genre.aspx?ID=foo` 합니다. 이 페이지에는 `Genre.aspx` 특정 장르의 책 검토가 나열 됩니다. 이를 위해서는 `GenreId` 값 (a `uniqueidentifier` )을 querystring을 통해 전달 해야 합니다. 예를 들어 fiction 리뷰를 볼 수 있는 적절 한 URL은 `Genre.aspx?ID=7683ab5d-4589-4f03-a139-1c26044d0146` 입니다. `uniqueidentifier`값이 아닌 값이 querystring (예: "foo")을 통해 전달 되 면 예외가 throw 됩니다.

> [!NOTE]
> 데모 웹 응용 프로그램에서 다운로드할 수 있는이 오류를 재현 하려면 `Genre.aspx?ID=foo` 직접 방문 하거나에서 "런타임 오류 생성" 링크를 클릭 합니다 `Default.aspx` .

**그림 1**에 나와 있는 예외 정보를 확인 합니다. 페이지 맨 위에 "문자열을 uniqueidentifier로 변환 하지 못했습니다." 라는 예외 메시지가 표시 됩니다. 예외의 형식 `System.Data.SqlClient.SqlException` 도 나열 됩니다. 스택 추적도 있습니다.

[![](displaying-a-custom-error-page-cs/_static/image2.png)](displaying-a-custom-error-page-cs/_static/image1.png)

**그림 1**: 예외 정보에 예외에 대 한 정보가 포함 되어 있습니다.  
 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-cs/_static/image3.png))

다른 유형의 YSOD는 런타임 오류가 있습니다 .이는 **그림 2**에 나와 있습니다. 런타임 오류 메시지는 방문자에 게 런타임 오류가 발생 했음을 알려 주지만 throw 된 예외에 대 한 정보는 포함 하지 않습니다. 그러나이 파일을 수정 하 여 오류 세부 정보를 표시 하는 방법에 대 한 지침을 제공 합니다 .이는 해당 하는 `Web.config` ysod의 일부입니다.

기본적으로 런타임 오류 메시지는 사용자가 원격으로 방문 하는 사용자에 게 표시 됩니다 ( http://www.yoursite.com) **그림 2**:의 브라우저 주소 표시줄에서 URL로 복합적) `http://httpruntime.web703.discountasp.net/Genre.aspx?ID=foo` . 개발자는 오류 세부 정보를 확인 하는 데 관심이 있기 때문에 두 가지 다른 YSOD 화면이 존재 하지만 이러한 정보는 사이트를 방문 하는 모든 사용자에 게 잠재적인 보안 취약점 또는 기타 중요 한 정보를 노출 시킬 수 있으므로 라이브 사이트에 표시 해서는 안 됩니다.

> [!NOTE]
> DiscountASP.NET를 웹 호스트로 사용 하 고 있는 경우 라이브 사이트를 방문할 때 런타임 오류 메시지가 표시 되지 않는 것을 알 수 있습니다. DiscountASP.NET는 기본적으로 예외 정보를 표시 하도록 서버를 구성 했기 때문입니다. 좋은 소식은 파일에 섹션을 추가 하 여이 기본 동작을 재정의할 수 있다는 것입니다 `<customErrors>` `Web.config` . "표시 되는 오류 페이지 구성" 섹션에서 섹션을 `<customErrors>` 자세히 살펴봅니다.

[![](displaying-a-custom-error-page-cs/_static/image5.png)](displaying-a-custom-error-page-cs/_static/image4.png)

**그림 2**: 런타임 오류 메시지에 오류 정보가 포함 되어 있지 않음  
 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-cs/_static/image6.png))

세 번째 오류 페이지 유형은 사용자가 만드는 웹 페이지인 사용자 지정 오류 페이지입니다. 사용자 지정 오류 페이지의 장점으로는 페이지의 모양과 느낌을 함께 사용자에 게 표시 되는 정보를 완전히 제어할 수 있습니다. 사용자 지정 오류 페이지에서는 다른 페이지와 동일한 마스터 페이지 및 스타일을 사용할 수 있습니다. "사용자 지정 오류 페이지 사용" 섹션에서는 사용자 지정 오류 페이지를 만들고 처리 되지 않은 예외가 발생할 경우이를 표시 하도록 구성 하는 과정을 안내 합니다. **그림 3** 에서는이 사용자 지정 오류 페이지의 최대 사용량을 제공 합니다. 여기에서 볼 수 있듯이 오류 페이지의 모양과 느낌은 그림 1과 2에 표시 된 두 가지 죽음의 노랑 화면 중 하나를 훨씬 더 전문적으로 보입니다.

[![](displaying-a-custom-error-page-cs/_static/image8.png)](displaying-a-custom-error-page-cs/_static/image7.png)

**그림 3**: 사용자 지정 오류 페이지에서 보다 맞춤식 모양 및 느낌 제공  
 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-cs/_static/image9.png))

잠시 시간을 내 서 **그림 3**에서 브라우저의 주소 표시줄을 검사 합니다. 주소 표시줄에는 사용자 지정 오류 페이지의 URL ()이 표시 `/ErrorPages/Oops.aspx` 됩니다. 그림 1과 2에서는 오류가 발생 한 것과 동일한 페이지에 노란색의 주황색 화면이 표시 됩니다 ( `Genre.aspx` ). 사용자 지정 오류 페이지에 querystring 매개 변수를 통해 오류가 발생 한 페이지의 URL이 전달 됩니다 `aspxerrorpath` .

## <a name="configuring-which-error-page-is-displayed"></a>표시 되는 오류 페이지 구성

표시 되는 세 가지 오류 페이지는 두 가지 변수를 기반으로 합니다.

- 섹션의 구성 정보 `<customErrors>` 및
- 사용자가 로컬에서 또는 원격으로 사이트를 방문 하 고 있는지 여부입니다.

의 [ `<customErrors>` 섹션](https://msdn.microsoft.com/library/h0hfz6fc.aspx) 에는 `Web.config` `defaultRedirect` 및와 같은 오류 페이지에 영향을 주는 두 가지 특성이 있습니다. `mode` `defaultRedirect` 특성은 선택 사항입니다. 제공 되는 경우 사용자 지정 오류 페이지의 URL을 지정 하 고 런타임 오류 메시지 대신 사용자 지정 오류 페이지가 표시 되어야 함을 나타냅니다. `mode`특성은 필수 이며, 또는의 세 가지 값 중 하나 `On` 를 허용 `Off` `RemoteOnly` 합니다. 이러한 값에는 다음과 같은 동작이 있습니다.

- `On`-사용자 지정 오류 페이지 또는 런타임 오류 메시지는 로컬 또는 원격 인지에 관계 없이 모든 방문자에 게 표시 됨을 나타냅니다.
- `Off`-예외 정보는 로컬 또는 원격 인지에 관계 없이 모든 방문자에 게 표시 되도록 지정 합니다.
- `RemoteOnly`-사용자 지정 오류 페이지 또는 런타임 오류 YSOD 메시지가 원격 방문자에 게 표시 되는 반면, 예외 세부 정보는 로컬 방문자에 게 표시 됨을 나타냅니다.

달리 지정 하지 않는 한 ASP.NET는 mode 특성을로 설정 하 `RemoteOnly` 고 값을 지정 하지 않은 것 처럼 작동 `defaultRedirect` 합니다. 즉, 기본 동작은 런타임 오류 메시지가 원격 방문자에 게 표시 되는 반면 예외 정보는 로컬 방문자에 게 표시 되는 것입니다. 웹 응용 프로그램에 섹션을 추가 하 여이 기본 동작을 재정의할 수 있습니다. `<customErrors>``Web.config file.`

## <a name="using-a-custom-error-page"></a>사용자 지정 오류 페이지 사용

모든 웹 응용 프로그램에는 사용자 지정 오류 페이지가 있어야 합니다. 런타임 오류 메시지에 대 한 보다 전문적인 대안을 제공 하 고, 쉽게 만들 수 있으며, 사용자 지정 오류 페이지를 사용 하도록 응용 프로그램을 구성 하는 데 몇 분 밖에 걸리지 않습니다. 첫 번째 단계는 사용자 지정 오류 페이지를 만드는 것입니다. 이라는 새 폴더를 서적 검토 응용 프로그램에 추가 하 `ErrorPages` 고 라는 새 ASP.NET 페이지에 추가 했습니다 `Oops.aspx` . 페이지가 사이트의 나머지 페이지와 동일한 마스터 페이지를 사용 하도록 하 여 동일한 모양과 느낌을 자동으로 상속 하도록 합니다.

[![](displaying-a-custom-error-page-cs/_static/image11.png)](displaying-a-custom-error-page-cs/_static/image10.png)

**그림 4**: 사용자 지정 오류 페이지 만들기

다음으로 오류 페이지에 대 한 콘텐츠를 만드는 데 몇 분 정도 걸립니다. 예기치 않은 오류가 발생 했음을 나타내는 메시지와 사이트 홈페이지에 대 한 링크가 포함 된 간단한 사용자 지정 오류 페이지를 만들었습니다.

[![](displaying-a-custom-error-page-cs/_static/image13.png)](displaying-a-custom-error-page-cs/_static/image12.png)

**그림 5**: 사용자 지정 오류 페이지 디자인  
 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-cs/_static/image14.png))

오류 페이지가 완료 되 면 런타임 오류 메시지 대신 사용자 지정 오류 페이지를 사용 하도록 웹 응용 프로그램을 구성 합니다. 이를 위해서는 섹션의 특성에서 오류 페이지의 URL을 지정 `<customErrors>` `defaultRedirect` 합니다. 응용 프로그램의 파일에 다음 태그를 추가 합니다 `Web.config` .

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample1.xml)]

위의 태그는 응용 프로그램을 구성 하 여 사용자가 로컬로 방문한 사용자에 게 예외 정보를 표시 하 고, 사용자 지정 오류 페이지를 사용 하 여 사용자가 원격으로 방문 하는 사용자에 게 표시 합니다. 이 작업을 수행 하려면 프로덕션 환경에 웹 사이트를 배포 하 고 잘못 된 querystring 값을 사용 하 여 라이브 사이트의 장르 페이지를 방문 하세요. 사용자 지정 오류 페이지가 표시 됩니다 ( **그림 3**으로 다시 참조).

사용자 지정 오류 페이지가 원격 사용자 에게만 표시 되는지 확인 하려면 `Genre.aspx` 개발 환경에서 잘못 된 querystring이 있는 페이지를 방문 하세요. 예외 세부 정보는 여전히 표시 됩니다 ( **그림 1**참조). `RemoteOnly`이 설정은 프로덕션 환경에서 사이트를 방문 하는 사용자가 로컬로 작업 하는 개발자가 예외의 세부 정보를 계속 확인 하는 동안 사용자 지정 오류 페이지를 볼 수 있도록 합니다.

## <a name="notifying-developers-and-logging-error-details"></a>개발자에 게 알림 및 오류 정보 로깅

개발 환경에서 발생 하는 오류는 개발자가 자신의 컴퓨터에서 발생 한 것입니다. 그는 예외 정보에 예외 정보를 표시 하 고 오류가 발생 했을 때 수행 하는 단계를 알고 있습니다. 그러나 프로덕션에서 오류가 발생 하는 경우 개발자는 사이트를 방문 하는 최종 사용자가 오류를 보고 하는 데 시간이 걸리지 않는 한 오류가 발생 했음을 알지 못합니다. 또한 예외 유형, 메시지 및 스택 추적을 몰라도 사용자가 개발 팀에 오류가 발생 했음을 경고할 수 있는 경우에도 오류의 원인을 진단 하기 어려울 수 있습니다.

이러한 이유로 프로덕션 환경의 모든 오류는 일부 영구 저장소 (예: 데이터베이스)에 기록 되 고, 개발자가이 오류에 대 한 경고를 표시 하는 것이 가장 중요 합니다. 사용자 지정 오류 페이지는이 로깅 및 알림을 수행 하는 데 좋은 장소와 같이 보일 수 있습니다. 아쉽게도 사용자 지정 오류 페이지에는 오류 세부 정보에 대 한 액세스 권한이 없으므로이 정보를 기록 하는 데 사용할 수 없습니다. 몇 가지 방법으로 오류 세부 정보를 가로채서 기록할 수 있으며, 다음 세 가지 자습서에서이 항목을 자세히 살펴볼 수 있습니다.

## <a name="using-different-custom-error-pages-for-different-http-error-statuses"></a>다른 HTTP 오류 상태에 다른 사용자 지정 오류 페이지 사용

ASP.NET 페이지에서 예외가 throw 되 고 처리 되지 않는 경우 예외는 구성 된 오류 페이지를 표시 하는 ASP.NET 런타임으로 처리 합니다. 요청 된 파일을 찾을 수 없거나 파일에 대 한 읽기 권한이 사용 하지 않도록 설정 된 경우와 같은 이유로 ASP.NET 엔진에 요청을 처리할 수 없는 경우 ASP.NET 엔진은를 발생 시킵니다 `HttpException` . ASP.NET 페이지에서 발생 하는 예외와 같은이 예외는 런타임까지 버블링 되어 적절 한 오류 페이지가 표시 됩니다.

프로덕션 환경에서 웹 응용 프로그램을 사용 하면 사용자가 찾을 수 없는 페이지를 요청 하는 경우 사용자 지정 오류 페이지가 표시 됩니다. **그림 6** 에서는 이러한 예를 보여 줍니다. 이 요청은 존재 하지 않는 페이지 ()에 대 한 것 이므로 `NoSuchPage.aspx` `HttpException` 이 throw 되 고 사용자 지정 오류 페이지가 표시 됩니다 ( `NoSuchPage.aspx` `aspxerrorpath` querystring 매개 변수에 대 한 참조).

[![](displaying-a-custom-error-page-cs/_static/image16.png)](displaying-a-custom-error-page-cs/_static/image15.png)

**그림 6**: ASP.NET 런타임은 잘못 된 요청에 대 한 응답으로 구성 된 오류 페이지를 표시 합니다 ([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-cs/_static/image17.png)).

기본적으로 모든 유형의 오류는 동일한 사용자 지정 오류 페이지를 표시 합니다. 그러나 `<error>` 섹션 내의 자식 요소를 사용 하 여 특정 HTTP 상태 코드에 대해 다른 사용자 지정 오류 페이지를 지정할 수 있습니다 `<customErrors>` . 예를 들어 HTTP 상태 코드 404을 포함 하는 페이지를 찾을 수 없음 오류가 발생 하는 경우 다른 오류 페이지가 표시 되도록 하려면 섹션을 업데이트 하 여 `<customErrors>` 다음 태그를 포함 합니다.

[!code-xml[Main](displaying-a-custom-error-page-cs/samples/sample2.xml)]

이와 같이 변경 하면 사용자가 원격으로 방문 하는 사용자가 존재 하지 않는 ASP.NET 리소스를 요청 하는 경우 `404.aspx` 대신 사용자 지정 오류 페이지로 리디렉션됩니다 `Oops.aspx` . **그림 7** 에 설명 된 것 처럼 `404.aspx` 페이지는 일반 사용자 지정 오류 페이지 보다 더 구체적인 메시지를 포함할 수 있습니다.

> [!NOTE]
> [404 오류 페이지를 확인 하 고,](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/) 유효한 404 오류 페이지를 만드는 방법에 대 한 지침을 제공 합니다.

[![](displaying-a-custom-error-page-cs/_static/image19.png)](displaying-a-custom-error-page-cs/_static/image18.png)

**그림 7**: 사용자 지정 404 오류 페이지에 더 많은 대상 메시지가 표시 되는 경우`Oops.aspx`  
([전체 크기 이미지를 보려면 클릭](displaying-a-custom-error-page-cs/_static/image20.png)) 

`404.aspx`사용자가 찾을 수 없는 페이지를 요청 하는 경우에만 페이지에 도달할 수 있으므로 사용자가이 특정 유형의 오류를 해결 하는 데 도움이 되는 기능을 포함 하도록이 사용자 지정 오류 페이지를 향상 시킬 수 있습니다. 예를 들어 알려진 잘못 된 Url을 양호한 Url에 매핑한 다음 `404.aspx` 사용자 지정 오류 페이지에서 해당 테이블에 대해 쿼리를 실행 하 고 사용자가 연결 하려고 하는 페이지를 제안 하는 데이터베이스 테이블을 작성할 수 있습니다.

> [!NOTE]
> ASP.NET 엔진에서 처리 하는 리소스에 대 한 요청이 있는 경우에만 사용자 지정 오류 페이지가 표시 됩니다. [IIS와 ASP.NET 개발 서버 자습서의 핵심 차이점](core-differences-between-iis-and-the-asp-net-development-server-cs.md) 에 설명 된 대로 웹 서버는 특정 요청 자체를 처리할 수 있습니다. 기본적으로 IIS 웹 서버는 ASP.NET 엔진을 호출 하지 않고 이미지 및 HTML 파일과 같은 정적 콘텐츠에 대 한 요청을 처리 합니다. 따라서 사용자가 존재 하지 않는 이미지 파일을 요청 하는 경우 ASP 대신 IIS의 기본 404 오류 메시지를 다시 받게 됩니다. NET의 구성 된 오류 페이지입니다.

## <a name="summary"></a>요약

ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생 하면 사용자에 게 다음 세 가지 오류 페이지 중 하나가 표시 됩니다. 예외 세부 정보 노랑 화면 런타임 오류 노란색 화면 (죽음) 또는 사용자 지정 오류 페이지를 지정 합니다. 표시 되는 오류 페이지는 응용 프로그램의 `<customErrors>` 구성과 사용자가 로컬로 또는 원격으로 방문 하 고 있는지 여부에 따라 달라 집니다. 기본 동작은 로컬 방문자에 게 예외 정보를 표시 하 고, 원격 방문자에 게 런타임 오류를 표시 하는 것입니다.

런타임 오류는 사이트를 방문 하는 사용자 로부터 잠재적으로 중요 한 오류 정보를 숨기는 반면, 사이트의 모양과 느낌에서 중단 되 고 응용 프로그램을 버그가 있는 합니다. 사용자 지정 오류 페이지를 만들고 디자인 하 고 섹션의 특성에 해당 URL을 지정 하는 사용자 지정 오류 페이지를 사용 하는 것이 더 나은 방법입니다 `<customErrors>` `defaultRedirect` . 여러 HTTP 오류 상태에 대해 여러 사용자 지정 오류 페이지를 포함할 수도 있습니다.

사용자 지정 오류 페이지는 프로덕션 환경에서 웹 사이트에 대 한 포괄적인 오류 처리 전략의 첫 번째 단계입니다. 오류를 개발자에 게 경고 하 고 세부 정보를 기록 하는 것도 중요 한 단계입니다. 다음 세 가지 자습서에서는 오류 알림 및 로깅에 대 한 기술을 살펴봅니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [오류 페이지, 한 번 더](http://www.smashingmagazine.com/2009/01/29/404-error-pages-one-more-time/)
- [예외 디자인 지침](https://msdn.microsoft.com/library/ms229014.aspx)
- [사용자에 게 친숙 한 오류 페이지](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [예외 처리 및 Throw](https://msdn.microsoft.com/library/5b2yeyab.aspx)
- [ASP.NET에서 사용자 지정 오류 페이지를 사용 하 여 올바르게 사용](http://professionalaspnet.com/archive/2007/09/30/Properly-Using-Custom-Error-Pages-in-ASP.NET.aspx)
- [ASP.NET 추적 개요](/previous-versions/aspnet/bb386420(v%3Dvs.100))

> [!div class="step-by-step"]
> [이전](strategies-for-database-development-and-deployment-cs.md)
> [다음](processing-unhandled-exceptions-cs.md)
