---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: ASP.NET MVC에서 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012의 페이지 검사기는 통합 브라우저를 사용 하는 웹 개발 도구입니다. 통합 브라우저에서 요소를 선택 하 고 페이지 검사기 합니다.
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 42d5683ce75467a159c9d13edf302bd6bf24a11d
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643695"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a>ASP.NET MVC에서 페이지 검사기 사용

사람, Tim Am마나트 n

> Visual Studio 2012의 페이지 검사기는 통합 브라우저를 사용 하는 웹 개발 도구입니다. 통합 브라우저에서 요소를 선택 하 고 페이지 검사기 요소의 원본 및 CSS를 즉시 강조 표시 합니다. MVC 뷰를 찾아보고, 렌더링 된 태그의 소스를 빠르게 찾고, Visual Studio 환경 내에서 브라우저 도구를 바로 사용할 수 있습니다.
> 
> [비디오 시청](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> 이 자습서에서는 검사 모드을 사용 하도록 설정한 다음 웹 프로젝트 내에서 태그 및 CSS를 빠르게 찾고 편집 하는 방법을 보여 줍니다. 이 자습서에서는 MVC 프로젝트를 사용 하지만 [Web Forms](https://go.microsoft.com/?linkid=9802001) 및 기타 ASP.NET 응용 프로그램에도 페이지 검사기을 사용할 수 있습니다.
> 
> 이 자습서에는 다음과 같은 섹션이 있습니다.
> 
> - [필수 구성 요소](#_1_prerequisites)
> - [웹 응용 프로그램 만들기](#_2_creating_a)
> - [페이지 검사기를 사용 하 여 뷰 찾아보기](#_3_using_page)
> - [검사 모드 사용](#_4_inspection_mode)
> - [페이지 검사기를 사용 하 여 태그 변경](#_5_using_page)
> - [검사 모드 및 HTML 창](#_6_inspection_mode)
> - [스타일 창에서 CSS 변경 내용 미리 보기](#_7_previewing_css)
> - [CSS 자동 동기화](#css_auto_sync)
> - [CSS 색 선택 사용](#css_color_picker)
> - [JavaScript에 동적 페이지 요소 매핑](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>필수 구성 요소

- 웹 용 [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) 또는 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/downloads#express-web)

> [!NOTE]
> 최신 버전의 페이지 검사기을 다운로드 하려면 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=255386) 를 사용 하 여 WINDOWS Azure SDK for .net 2.0을 설치 합니다.

페이지 검사기 Microsoft Web 개발자 도구와 함께 제공 됩니다. 최신 버전은 1.3입니다. 보유 한 버전을 확인 하려면 Visual Studio를 실행 하 고 **도움말** 메뉴에서 **정보 Microsoft Visual Studio** 를 선택 합니다.

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>웹 응용 프로그램 만들기

먼저 페이지 검사기 사용할 웹 응용 프로그램을 만듭니다. Visual Studio에서 **파일** &gt; **새 프로젝트**를 선택합니다. 왼쪽에서 **Visual c #** 을 확장 하 고 **웹**을 선택한 다음 **ASP.NET MVC4 웹 응용 프로그램**을 선택 합니다.

![새 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image2.png)

**확인**을 클릭합니다.

**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**을 선택 합니다. 기본 뷰 엔진으로 **Razor** 를 남겨 둡니다.

![새 ASP.NET MVC 프로젝트-인터넷 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image4.png)

응용 프로그램이 **소스** 뷰에서 열립니다.

![소스 뷰의 새 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image6.png)

이제 작업할 응용 프로그램이 있으므로 페이지 검사기를 사용 하 여 검사 하 고 수정할 수 있습니다.

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a>페이지 검사기를 사용 하 여 뷰 찾아보기

Visual Studio 2012에서 프로젝트의 뷰를 마우스 오른쪽 단추로 클릭 하 고 **페이지 검사기 보기**를 선택 하면 페이지 검사기 경로를 파악 하 고 페이지를 표시 합니다.

**솔루션 탐색기**에서 **Views** 폴더를 확장 한 다음 **Home** 폴더를 확장 합니다. Index cshtml 파일을 마우스 오른쪽 단추로 클릭 하 고 **페이지 검사기 보기**를 선택 합니다.

![View Index. cshtml in 페이지 검사기](using-page-inspector-in-aspnet-mvc/_static/image8.png)

기본적으로 페이지 검사기는 Visual Studio 환경의 왼쪽에 창으로 도킹 됩니다. 원하는 경우 다른 곳에 도킹 하거나 창의 도킹을 해제할 수 있습니다. [방법: 창 정렬 및 도킹을](https://msdn.microsoft.com/library/z4y0hsax.aspx)참조 하세요.

페이지 검사기 창의 위쪽 창에는 브라우저 창의 현재 페이지가 표시 됩니다. 아래쪽 창에는 페이지의 다양 한 측면을 검사할 수 있는 몇 가지 탭과 함께 HTML 태그의 페이지가 표시 됩니다. 아래쪽 창은 Internet Explorer의 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478) 와 비슷합니다.

![페이지 검사기 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image10.png)

이 자습서에서는 **HTML** 및 **스타일** 탭을 사용 하 여 신속 하 게 탐색 하 고 응용 프로그램을 변경 합니다.

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a>EnableInspection 모드

검사 모드에 페이지 검사기을 추가 하려면 **검사** 단추를 클릭 합니다. 검사 모드에서 렌더링 된 페이지의 일부에 마우스 포인터를 놓으면 해당 소스 태그나 코드가 강조 표시 됩니다.

![전환 검사 모드](using-page-inspector-in-aspnet-mvc/_static/image12.png)

이제 페이지 검사기 내에서 페이지의 서로 다른 부분으로 마우스를 이동 합니다. 이렇게 하면 마우스 포인터가 큼 더하기 기호로 바뀌고 아래 요소가 강조 표시 됩니다.

![Div를 마우스로 가리킵니다. 콘텐츠-래퍼](using-page-inspector-in-aspnet-mvc/_static/image14.png)

마우스 포인터를 이동 하면 Visual Studio는 소스 파일에서 해당 Razor 구문를 강조 표시 합니다. HTML 요소가 다른 소스 파일에서 제공 되는 경우 Visual Studio에서 자동으로 파일을 엽니다.

페이지 검사기에서 **html** 탭에는 Razor 구문에서 생성 된 html이 표시 됩니다. 마우스 포인터를 움직이면 HTML 요소가 강조 표시 됩니다. **스타일** 탭에는 요소에 대 한 CSS 규칙이 표시 됩니다.

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>페이지 검사기를 사용 하 여 태그 변경

페이지 검사기를 사용 하면 위치가 명확 하지 않을 수 있는 태그를 찾을 수 있습니다. 그런 다음 태그를 수정 하 고 결과 변경 내용을 볼 수 있습니다.

이를 확인 하려면 **검사** 를 클릭 한 다음 페이지 검사기 창에서 페이지 아래쪽으로 스크롤합니다.

마우스 포인터를 바닥글 영역으로 이동 하면 페이지 검사기 \_ layout 파일이 열리고 선택한 레이아웃 페이지의 섹션이 강조 표시 됩니다. 여기에서 볼 수 있듯이 바닥글 영역은 뷰 자체가 아니라 레이아웃 파일에 정의 됩니다.

![바닥글](using-page-inspector-in-aspnet-mvc/_static/image16.png)

이제 저작권 표시를 사용 하 여 줄 위로 마우스 포인터를 이동 <a id="a"></a> 합니다. \_Layout. cshtml 페이지에서 해당 줄이 강조 표시 됩니다.

![바닥글 저작권 선이 강조 표시 됨](using-page-inspector-in-aspnet-mvc/_static/image18.png)

레이아웃 cshtml 파일의 줄 끝에 일부 텍스트를 추가 \_ 합니다.

&lt;p &gt; &amp; copy; @DateTime.Now.Year -My ASP.NET MVC 응용 프로그램 바위! &lt; /p&gt;

이제 Ctrl + Alt + Enter를 누르거나 업데이트 표시줄을 클릭 하 여 페이지 검사기 브라우저 창에 결과를 표시 합니다.

![내 ASP.NET 응용 프로그램 돌!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

Index는 footer에 정의 되어 있지만 페이지 검사기 레이아웃에 포함 된 것으로 표시 된 것으로 간주 될 수 있습니다. \_

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>검사 모드 및 HTML 창

다음으로 HTML 창 및이 창에서 요소를 매핑하는 방법에 대해 간략히 살펴봅니다.

**검사** 를 클릭 하 여 검사 모드에 페이지 검사기을 배치 합니다.

"여기에 로고가 있습니다." 라는 페이지의 위쪽 부분을 클릭 합니다. 특정 요소를 자세히 검사 하 고 있으므로 마우스 포인터를 이동할 때 브라우저 창에 표시 되는 내용이 더 이상 표시 되지 않습니다.

이제 마우스 포인터를 **HTML** 창으로 이동 합니다. 마우스 포인터를 움직이면 페이지 검사기 **HTML** 창에서 요소를 윤곽선으로 표시 하 고 브라우저 창에서 해당 요소를 강조 표시 합니다.

![HTML 창](using-page-inspector-in-aspnet-mvc/_static/image22.png)

이전 처럼 페이지 검사기 \_ 임시 탭에서 layout. cshtml 파일을 엽니다. \_ layout. cshtml 임시 탭을 클릭 &lt; 하면 헤더 섹션에서 해당 태그가 강조 표시 됩니다. &gt;

![강조 표시 된 태그](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>스타일 창에서 CSS 변경 내용 미리 보기

다음으로 페이지 검사기 **스타일** 창을 사용 하 여 CSS에 대 한 변경 내용을 미리 봅니다.

**검사** 를 클릭 하 여 검사 모드에 페이지 검사기을 배치 합니다.

페이지 검사기 브라우저 창에서 **div. 콘텐츠-래퍼** 레이블이 나타날 때까지 마우스 포인터를 "홈 페이지" 섹션으로 이동 합니다.

![Div를 마우스로 가리킵니다. 콘텐츠-래퍼](using-page-inspector-in-aspnet-mvc/_static/image26.png)

Div. 콘텐츠-래퍼 섹션 내에서 한 번 클릭 한 다음 마우스 포인터를 **스타일** 창으로 이동 합니다. **스타일** 창에는이 요소에 대 한 모든 CSS 규칙이 표시 됩니다. 아래로 스크롤하여, 주요. 콘텐츠-래퍼 클래스 선택기를 찾습니다. 이제 배경 색 속성에 대 한 확인란의 선택을 취소 합니다.

![배경색 지우기](using-page-inspector-in-aspnet-mvc/_static/image28.png)

페이지 검사기 브라우저 창에서 변경 내용이 즉시 미리 보기를 확인 합니다.

확인란을 다시 선택 하 고 속성 값을 두 번 클릭 한 다음 빨강으로 변경 합니다. 변경 내용이 즉시 표시 됩니다.

![빨강 배경색](using-page-inspector-in-aspnet-mvc/_static/image30.png)

스타일 **창을 사용** 하면 스타일 시트 자체에 변경 내용을 커밋하기 전에 CSS 변경을 쉽게 테스트 하 고 미리 볼 수 있습니다.

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>CSS 자동 동기화

> [!NOTE]
> 이 기능을 사용 하려면 1.3 버전의 페이지 검사기 필요 합니다.

CSS 자동 동기화 기능을 사용 하면 CSS 파일을 직접 편집 하 고 페이지 검사기 브라우저에서 즉시 변경 내용을 볼 수 있습니다.

**검사** 를 클릭 하 여 검사 모드에 페이지 검사기을 배치 합니다.

페이지 검사기 브라우저에서 ' 홈 페이지 ' 섹션 위로 마우스 포인터를 이동 합니다. **콘텐츠-래퍼** 레이블이 나타날 때까지 이동 합니다. 한 번 클릭 하 여이 요소를 선택 합니다.

**스타일** 창에는이 요소에 대 한 모든 CSS 규칙이 표시 됩니다. 아래로 스크롤하여, 주요. 콘텐츠-래퍼 클래스 선택기를 찾습니다. "주요. 콘텐츠-래퍼"를 클릭 합니다. 페이지 검사기이 스타일 (.css)을 정의 하는 CSS 파일을 열고 해당 CSS 스타일을 강조 표시 합니다.

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

이제의 값을 `background-color` "red"로 변경 합니다. 변경 내용은 페이지 검사기 브라우저에 즉시 표시 됩니다.

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a>CSS 색 선택 사용

Visual Studio 2012의 CSS 편집기에는 색을 쉽게 선택 하 고 삽입할 수 있는 색 선택이 있습니다. 색 선택기는 색의 표준 색상표를 포함 하 고, 표준 색 이름, 해시 코드, RGB, RGBA, HSL 및 HSLA 색을 지원 하며, 문서에서 가장 최근에 사용한 색의 목록을 유지 관리 합니다.

이전 섹션에서는 속성의 값을 변경 했습니다 `background-color` . 색 선택기를 호출 하려면 속성 이름 뒤에 삽입 지점을 놓고 **#** 또는 **rgb (**.

![CSS 색 선택 막대입니다.](using-page-inspector-in-aspnet-mvc/_static/image36.png)

색을 클릭 하 여 선택 하거나 아래쪽 화살표 키를 누른 다음 왼쪽 및 오른쪽 화살표 키를 사용 하 여 색을 트래버스 합니다. 색을 방문할 때 해당 16 진수 값을 미리 봅니다.

![배경 색 속성 값 미리 보기](using-page-inspector-in-aspnet-mvc/_static/image38.png)

색 막대에 원하는 정확한 색이 없으면 색 선택 팝업을 사용할 수 있습니다. 이를 열려면 색 막대의 오른쪽 끝에 있는 이중 갈매기형 펼침 단추를 클릭 하거나 키보드에서 아래쪽 화살표를 한 번 또는 두 번 누릅니다.

![CSS 색 선택 팝업](using-page-inspector-in-aspnet-mvc/_static/image40.png)

오른쪽의 세로 막대에서 색을 클릭 합니다. 이렇게 하면 주 창에 해당 색의 그라데이션이 표시 됩니다. Enter 키를 눌러 세로 막대에서 색을 직접 선택 하거나 주 창에서 아무 점이 나 클릭 하 여 더 높은 정밀도로 선택 합니다.

사용 하려는 컴퓨터 화면에 색이 있는 경우 (Visual Studio 사용자 인터페이스 내부에 있을 필요가 없음) 오른쪽 아래에 있는 스 포 이트 도구를 사용 하 여 해당 값을 캡처할 수 있습니다.

색 선택 아래쪽의 슬라이더를 움직여 색의 불투명도를 변경할 수도 있습니다. 이렇게 하면 RGBA 형식이 불투명을 나타낼 수 있기 때문에 색 값이 RGBA 값으로 변경 됩니다.

색을 선택한 후 Enter 키를 누른 후 세미콜론을 입력 하 여 *사이트 .css* 파일의 배경색 항목을 완성 합니다.

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>페이지 검사기 업데이트 표시줄

페이지 검사기는 *사이트 .css* 파일의 변경 내용을 즉시 검색 하 고 업데이트 표시줄에 경고를 표시 합니다.

![업데이트 표시줄](using-page-inspector-in-aspnet-mvc/_static/image42.png)

모든 파일을 저장 하 고 페이지 검사기 브라우저를 새로 고치려면 Ctrl + Alt + Enter를 누르거나 업데이트 표시줄을 클릭 합니다. 강조 표시 색의 변경 내용이 브라우저에 나타납니다.

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a>JavaScript에 동적 페이지 요소 매핑

최신 웹 응용 프로그램에서는 페이지의 요소가 JavaScript를 사용 하 여 동적으로 생성 되는 경우가 많습니다. 이는 이러한 페이지 요소에 해당 하는 정적 태그 (HTML 또는 Razor)가 없음을 의미 합니다.

1.3 버전을 사용 하면 페이지에 동적으로 추가 된 항목을 해당 JavaScript 코드로 다시 매핑할 수 페이지 검사기. 이 기능을 설명 하기 위해 [SPA (단일 페이지 응용 프로그램) 템플릿을](../../../single-page-application/overview/introduction/knockoutjs-template.md)사용 합니다.

> [!NOTE]
> SPA 템플릿에 [ASP.NET 및 Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) 업데이트가 필요 합니다.

Visual Studio에서 **파일** &gt; **새 프로젝트**를 선택합니다. 왼쪽에서 **Visual c #** 을 확장 하 고 **웹**을 선택한 다음 **ASP.NET MVC4 웹 응용 프로그램**을 선택 합니다. **확인**을 클릭합니다.

**새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **단일 페이지 응용 프로그램**을 선택 합니다.

솔루션 탐색기에서 **Views** 폴더를 확장 한 다음 **Home** 폴더를 확장 합니다. Index cshtml 파일을 마우스 오른쪽 단추로 클릭 하 고 **페이지 검사기 보기**를 선택 합니다.

페이지 검사기 브라우저에 표시 되는 첫 번째 작업은 로그인 페이지입니다. "등록"을 클릭 하 고 사용자 이름 및 암호를 만듭니다. 등록 하면 응용 프로그램은 사용자를 로그인 하 고 몇 가지 샘플 항목을 사용 하 여 할 일 목록을 만듭니다.

**검사** 를 클릭 하 여 검사 모드에 페이지 검사기을 배치 합니다. 페이지 검사기 브라우저에서 할 일 항목 중 하나를 클릭 합니다. 파란색으로 강조 표시 되는 대신 요소가 주황색으로 강조 표시 되 고 요소 이름 옆에 "JS"가 표시 됩니다. 이는 요소가 스크립트를 통해 동적으로 생성 되었음을 나타냅니다.

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

또한 **호출 스택** 탭에 주황색 밑줄이 표시 됩니다. 이는 **호출 스택** 창에 요소에 대 한 추가 정보가 있음을 나타냅니다.

**호출 스택** 탭을 클릭 합니다. **호출 스택** 창에는 요소를 만든 JavaScript 호출에 대 한 호출 스택이 표시 됩니다. JQuery와 같은 외부 라이브러리 호출이 축소 되어 응용 프로그램 스크립트에 대 한 호출을 쉽게 볼 수 있습니다.

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

외부 라이브러리 호출을 포함 하 여 전체 스택을 보려면 "External library" 라는 레이블이 지정 된 노드를 확장 하면 됩니다.

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

호출 스택의 항목을 클릭 하면 Visual Studio에서 코드 파일을 열고 해당 스크립트를 강조 표시 합니다.

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a>참고 항목

[Visual Studio를 사용 하 여 ASP.NET MVC 4 소개](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net 웹 사이트)

[페이지 검사기 소개](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 비디오)

[페이지 검사기 오류 메시지](https://go.microsoft.com/?linkid=9813062) (MSDN)
