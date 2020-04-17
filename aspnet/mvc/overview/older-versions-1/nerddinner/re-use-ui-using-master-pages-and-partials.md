---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 마스터 페이지 및 부분 페이지를 사용하여 UI 재사용 | 마이크로 소프트 문서
author: rick-anderson
description: 7단계에서는 부분 보기 템플릿과 마스터 페이지를 사용하여 코드 중복을 제거하기 위해 뷰 템플릿 내에서 'DRY 원칙'을 적용할 수 있는 방법을 살펴봅니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542601"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>마스터 페이지 및 부분을 사용하여 UI 재사용

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 7단계입니다.
> 
> 7단계는 부분 보기 템플릿 및 마스터 페이지를 사용하여 코드 중복을 제거하기 위해 뷰 템플릿 내에서 "DRY 원칙"을 적용할 수 있는 방법을 살펴봅니다.
> 
> MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-7-partials-and-master-pages"></a>얼간이 저녁 식사 단계 7: 부분 및 마스터 페이지

MVC가 ASP.NET 디자인 철학 중 하나는 "자신을 반복하지 마십시오" 원칙(일반적으로 "DRY"라고 함)입니다. DRY 디자인은 코드와 논리의 중복을 제거하는 데 도움이 되며, 궁극적으로 응용 프로그램을 더 빠르게 빌드하고 유지 관리가 쉬워집니다.

우리는 이미 우리의 NerdDinner 시나리오의 몇 가지에 적용 된 DRY 원리를 보았다. 몇 가지 예: 유효성 검사 논리는 모델 계층 내에서 구현되므로 컨트롤러에서 편집 및 생성 시나리오 모두에서 적용할 수 있습니다. 편집, 세부 정보 및 삭제 작업 메서드에서 "NotFound" 보기 템플릿을 다시 사용하고 있습니다. 뷰 템플릿을 사용하여 규칙-명명 패턴을 사용하고 있으므로 View() 도우미 메서드를 호출할 때 이름을 명시적으로 지정할 필요가 없습니다. 편집 및 만들기 작업 시나리오모두에 DinnerFormViewModel 클래스를 다시 사용하고 있습니다.

이제 뷰 템플릿 내에서 "DRY 원칙"을 적용하여 코드 중복을 제거할 수 있는 방법을 살펴보겠습니다.

### <a name="re-visiting-our-edit-and-create-view-templates"></a>편집 및 뷰 템플릿 만들기 다시 방문

현재 우리는 두 개의 서로 다른 보기 템플릿을 사용 하 여- "Edit.aspx" 그리고 "Create.aspx" - 우리의 저녁 식사 양식 UI를 표시 하려면. 빠른 시각적 비교는 그들이 얼마나 비슷한지 강조합니다. 다음은 만들기 양식의 모양입니다.

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

그리고 여기에 우리의 "편집"양식의 모습은 다음과 같습니다 :

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

큰 차이는 없는가요? 제목 및 헤더 텍스트 이외에 양식 레이아웃과 입력 컨트롤은 동일합니다.

"Edit.aspx" 및 "Create.aspx" 보기 템플릿을 열면 동일한 양식 레이아웃 및 입력 제어 코드가 포함되어 있음을 알 수 있습니다. 이 중복은 우리가 소개하거나 새로운 Dinner 속성을 변경할 때마다 두 번 변경해야 한다는 것을 의미합니다.

### <a name="using-partial-view-templates"></a>부분 뷰 템플릿 사용

ASP.NET MVC는 페이지의 하위 부분에 대한 뷰 렌더링 논리를 캡슐화하는 데 사용할 수 있는 "부분 보기" 템플릿을 정의하는 기능을 지원합니다. "Partials"는 뷰 렌더링 논리를 한 번 정의한 다음 응용 프로그램 전체의 여러 위치에서 다시 사용할 수 있는 유용한 방법을 제공합니다.

Edit.aspx 및 Create.aspx 뷰 템플릿 중복을 "DRY-up"하는 데 도움이 되도록 폼 레이아웃 과 두 가지 모두에 공통적인 입력 요소를 캡슐화하는 "DinnerForm.ascx"라는 부분 뷰 템플릿을 만들 수 있습니다. 우리는 우리의 / 보기 / 저녁 식사 디렉토리를 마우스 오른쪽 버튼으로 클릭하고 "추가 보기"메뉴&gt;명령을 선택하여이 작업을 수행 할 수 있습니다 :

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

그러면 "보기 추가" 대화 상자가 표시됩니다. "DinnerForm"을 만들 새 뷰의 이름을 지정하고 대화 상자 내에서 "부분 보기 만들기" 확인란을 선택하고 DinnerFormViewModel 클래스를 전달할 것임을 나타냅니다.

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

"추가" 단추를 클릭하면 Visual Studio에서 "\View\Dinners" 디렉토리 내에서 새 "DinnerForm.ascx" 보기 템플릿을 만듭니다.

그런 다음 Edit.aspx/ Create.aspx 보기 템플릿에서 중복 양식 레이아웃/입력 제어 코드를 새 "DinnerForm.ascx" 부분 보기 템플릿에 복사/붙여넣을 수 있습니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

그런 다음 편집 및 뷰 만들기 템플릿을 업데이트하여 DinnerForm 부분 템플릿을 호출하고 양식 중복을 제거할 수 있습니다. 뷰 템플릿 내에서 Html.RenderPartial("DinnerForm")를 호출하여 이 작업을 수행할 수 있습니다.

##### <a name="createaspx"></a>만들기.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>편집.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

Html.RenderPartial(예: ~보기/Dinners/DinnerForm.ascx)를 호출할 때 원하는 부분 템플릿의 경로를 명시적으로 한정할 수 있습니다. 그러나 위의 코드에서는 ASP.NET MVC 내에서 규칙 기반 명명 패턴을 활용하고 렌더링할 부분의 이름으로 "DinnerForm"을 지정합니다. 이 작업을 수행할 때 MVC는 컨벤션 기반 뷰 디렉토리에서 먼저 살펴볼 ASP.NET.이 컨트롤러의 경우 /View/Dinners가 됩니다. 부분 템플릿을 찾지 못하면 /View /Shared 디렉터리에서 해당 템플릿을 찾습니다.

Html.RenderPartial()가 부분 뷰의 이름만으로 호출되면 ASP.NET mVC가 호출 뷰 템플릿에서 사용하는 것과 동일한 모델 및 ViewData 사전 개체를 부분 뷰로 전달합니다. 또는 부분 뷰를 사용할 대체 모델 개체 및/또는 ViewData 사전을 전달할 수 있는 Html.RenderPartial()의 오버로드된 버전이 있습니다. 이 기능은 전체 모델/뷰모델의 하위 집합만 전달하려는 시나리오에 유용합니다.

| **측면 주제: &lt;&gt; &lt;왜 % 대신&gt;%= % ?** |
| --- |
| 위의 코드에서 발견 할 수있는 미묘한 것 중 하나는 &lt;Html.RenderPartial ()를 호출 할 때&gt; &lt;%= % 블록 대신 % %&gt; 블록을 사용하고 있다는 것입니다. &lt;ASP.NET %= %&gt; 블록은 개발자가 지정된 값을 렌더링하려고 &lt;함을 나타냅니다(예:&gt; %= "Hello" %는 "Hello"를 렌더링합니다). &lt;%&gt; 블록대신 개발자가 코드를 실행하려고 함을 나타내며, 그 안에 렌더링된 출력은 &lt;명시적으로 수행되어야 함을 나타냅니다(예: % Response.Write("Hello") %&gt; 위의 Html.RenderPartial &lt;코드에서 % 블록을&gt; 사용하는 이유는 Html.RenderPartial() 메서드가 문자열을 반환하지 않고 대신 콘텐츠를 호출 뷰 템플릿의 출력 스트림으로 직접 출력하기 때문입니다. 성능 효율성을 위해 이 작업을 수행하므로 (잠재적으로 매우 큰) 임시 문자열 개체를 만들 필요가 없습니다. 이렇게 하면 메모리 사용량이 줄어들고 전체 응용 프로그램 처리량이 향상됩니다. Html.RenderPartial()를 사용할 때 의 한 가지 일반적인 실수는 % &lt;&gt; 블록 내에 있을 때 호출이 끝날 때 세미 콜론을 추가하는 것을 잊어버리는 것입니다. 예를 들어, 이 코드는 컴파일러 &lt;오류를 발생 합니다: % Html.RenderPartial ("DinnerForm") 대신&gt; 작성 해야: &lt;% Html.RenderPartial ("DinnerForm"); %&gt; &gt; 블록은 &lt;자체 포함된 코드 문이며 C# 코드 문을 사용하는 경우 세미 콜론으로 종료해야 하기 때문입니다. |

### <a name="using-partial-view-templates-to-clarify-code"></a>부분 보기 템플릿을 사용하여 코드 명확성

여러 위치에서 뷰 렌더링 논리가 중복되지 않도록 "DinnerForm" 부분 뷰 템플릿을 만들었습니다. 이것이 부분 보기 템플릿을 만드는 가장 일반적인 이유입니다.

때로는 한 곳에서만 호출되는 경우에도 부분 뷰를 만드는 것이 합리적입니다. 뷰 렌더링 논리를 추출하고 하나 이상의 잘 명명된 부분 템플릿으로 분할할 때 매우 복잡한 뷰 템플릿을 읽기가 훨씬 쉬워질 수 있습니다.

예를 들어 프로젝트의 Site.master 파일에서 아래 코드 조각을 살펴보겠습니다(곧 살펴보겠습니다). 코드는 비교적 간단하게 읽을 수 있습니다 - 부분적으로 화면 오른쪽 상단에 로그인 /로그 아웃 링크를 표시하는 논리가 "LogOnUserControl"부분 내에 캡슐화되어 있기 때문에:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

뷰 템플릿 내에서 html/코드 태그를 이해하려고 애쓰는 것이 혼란스러울 때마다 일부 가 추출되어 잘 명명된 부분 뷰로 리팩터링된 경우 더 명확하지 않은지 고려하십시오.

### <a name="master-pages"></a>마스터 페이지

ASP.NET MVC는 부분 보기를 지원하는 것 외에도 사이트의 공통 레이아웃 및 최상위 HTML을 정의하는 데 사용할 수 있는 "마스터 페이지" 템플릿을 만드는 기능도 지원합니다. 그런 다음 콘텐츠 자리 표시자 컨트롤을 마스터 페이지에 추가하여 뷰별로 재정의하거나 "채우기"할 수 있는 대체 가능한 영역을 식별할 수 있습니다. 이렇게 하면 응용 프로그램 전체에 공통 레이아웃을 적용하는 매우 효과적인(및 DRY) 방법을 제공합니다.

기본적으로 새 ASP.NET MVC 프로젝트에는 마스터 페이지 템플릿이 자동으로 추가됩니다. 이 마스터 페이지의 이름은 "Site.master"이며 \View\Shared\ 폴더 내에 있습니다.

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

기본 Site.master 파일은 다음과 같습니다. 사이트의 외부 html과 상단탐색 메뉴를 정의합니다. 여기에는 두 개의 대체 가능한 콘텐츠 자리 표시자 컨트롤(하나는 제목용이고 다른 하나는 페이지의 기본 콘텐츠를 대체해야 하는 컨트롤)이 포함되어 있습니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

NerdDinner 응용 프로그램("목록", "세부 정보", "편집", "만들기", "NotFound" 등)을 위해 만든 모든 보기 템플릿은 이 Site.master 템플릿을 기반으로 합니다. 이것은 "추가보기" 대화 상자를 사용하여 뷰를 만들 때 &lt;기본적으로 상위&gt; % @ 페이지 % 지시문에 추가 된 "MasterPageFile"특성을 통해 표시됩니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

즉, Site.master 콘텐츠를 변경하고 뷰 템플릿을 렌더링할 때 변경 내용을 자동으로 적용하고 사용할 수 있습니다.

우리의 응용 프로그램의 헤더가 "내 MVC 응용 프로그램"대신 "NerdDinner"되도록 Site.master의 헤더 섹션을 업데이트 해 보겠습니다. 또한 첫 번째 탭이 "Dinner찾기"(HomeController의 Index() 작업 메서드에서 처리되도록 탐색 메뉴를 업데이트하고 "DinnersController의 Create() 작업 메서드에서 처리됨"이라는 새 탭을 추가해 보겠습니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Site.master 파일을 저장하고 브라우저를 새로 고치면 응용 프로그램 내의 모든 보기에서 헤더 변경 내용이 표시됩니다. 예를 들어:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

그리고 */Dinners/편집/[id]* URL:

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>다음 단계

부분 및 마스터 페이지는 뷰를 깔끔하게 구성할 수 있는 매우 유연한 옵션을 제공합니다. 뷰 콘텐츠/코드가 중복되는 것을 방지하고 보기 템플릿을 더 쉽게 읽고 유지 관리할 수 있습니다.

이제 이전에 빌드한 목록 시나리오를 다시 방문하여 확장 가능한 페이징 지원을 사용하도록 설정해 보겠습니다.

> [!div class="step-by-step"]
> [이전](use-viewdata-and-implement-viewmodel-classes.md)
> [다음](implement-efficient-data-paging.md)
