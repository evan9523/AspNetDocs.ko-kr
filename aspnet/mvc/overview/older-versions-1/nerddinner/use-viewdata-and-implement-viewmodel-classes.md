---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 뷰데이터 사용 및 뷰모델 클래스 구현 | 마이크로 소프트 문서
author: rick-anderson
description: 6단계는 보다 풍부한 양식 편집 시나리오를 지원하도록 지원하는 방법을 보여 주며 컨트롤러에서 뷰로 데이터를 전달하는 데 사용할 수 있는 두 가지 방법에 대해서도 설명합니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541106"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>ViewData 사용 및 ViewModel 클래스 구현

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 6단계입니다.
> 
> 6단계는 보다 풍부한 양식 편집 시나리오를 지원하도록 설정하는 방법을 보여 주며 컨트롤러에서 뷰로 데이터를 전달하는 데 사용할 수 있는 두 가지 방법인 ViewData 및 ViewModel에 대해서도 설명합니다.
> 
> MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>얼간이 저녁 식사 6 단계 : 보기 데이터 및 보기 모델

여러 양식 게시물 시나리오를 다루었으며 CRUD(만들기, 업데이트 및 삭제) 지원을 구현하는 방법에 대해 설명했습니다. 이제 DinnersController 구현을 더 자세히 수행하 고 풍부한 형식 편집 시나리오에 대 한 지원을 사용 하 고 있습니다. 이 작업을 수행하는 동안 컨트롤러에서 뷰로 데이터를 전달하는 데 사용할 수 있는 두 가지 방법인 ViewData 및 ViewModel에 대해 설명합니다.

### <a name="passing-data-from-controllers-to-view-templates"></a>컨트롤러에서 뷰 템플릿으로 데이터 전달

MVC 패턴의 정의 특성 중 하나는 응용 프로그램의 다른 구성 요소 간에 적용하는 데 도움이 되는 엄격한 "우려 분리"입니다. 모델, 컨트롤러 및 뷰는 각각 잘 정의된 역할과 책임을 가지고 있으며 잘 정의된 방식으로 서로 통신합니다. 이렇게 하면 테스트 가능성 및 코드 재사용을 촉진하는 데 도움이 됩니다.

Controller 클래스가 클라이언트에 HTML 응답을 다시 렌더링하기로 결정하면 응답을 렌더링하는 데 필요한 모든 데이터를 뷰 템플릿에 명시적으로 전달해야 합니다. 뷰 템플릿은 데이터 검색 또는 응용 프로그램 논리를 수행해서는 안 되며 대신 컨트롤러에 의해 전달되는 모델/데이터에서 구동되는 렌더링 코드만 하도록 제한해야 합니다.

현재 DinnersController 클래스에서 뷰 템플릿으로 전달되는 모델 데이터는 간단하고 간단합니다 . 응용 프로그램에 더 많은 UI 기능을 추가하면 보기 템플릿 내에서 HTML 응답을 렌더링하기 위해 이 데이터 이상을 전달해야 하는 경우가 많습니다. 예를 들어 편집 및 만들기 내의 "국가" 필드를 HTML 텍스트 상자에서 드롭다운 목록으로 변경할 수 있습니다. 뷰 템플릿에서 국가 이름의 드롭다운 목록을 하드 코딩하는 대신 동적으로 채우는 지원되는 국가 목록에서 국가 이름을 생성할 수 있습니다. Dinner *개체와* 지원되는 국가 목록을 컨트롤러에서 뷰 템플릿으로 전달하는 방법이 필요합니다.

이 작업을 수행할 수 있는 두 가지 방법을 살펴보겠습니다.

### <a name="using-the-viewdata-dictionary"></a>뷰데이터 사전 사용

컨트롤러 기본 클래스는 컨트롤러에서 뷰로 추가 데이터 항목을 전달하는 데 사용할 수 있는 "ViewData" 사전 속성을 노출합니다.

예를 들어 편집 보기 내의 "국가" 텍스트 상자를 HTML 텍스트 상자에서 드롭다운 목록으로 변경하려는 시나리오를 지원하기 위해 국가 드롭다운 목록의 모델로 사용할 수 있는 SelectList 개체를 전달할 편집() 작업 메서드를 업데이트할 수 있습니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

위의 SelectList의 생성자는 현재 선택된 값뿐만 아니라 드롭다운 목록을 채울 카운티 목록을 수락합니다.

그런 다음 이전에 사용했던 Html.TextBox() 도우미 방법 대신 Edit.aspx 보기 템플릿을 업데이트하여 Html.DropDownList() 도우미 메서드를 사용할 수 있습니다.

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

위의 Html.DropDownList() 도우미 메서드에는 두 개의 매개 변수가 사용됩니다. 첫 번째는 출력할 HTML 양식 요소의 이름입니다. 두 번째는 ViewData 사전을 통해 전달한 "SelectList" 모델입니다. C# "as" 키워드를 사용하여 사전 내의 형식을 SelectList로 캐스팅합니다.

이제 응용 프로그램을 실행하고 브라우저 내에서 */Dinners/편집/1* URL에 액세스하면 편집 UI가 업데이트되어 텍스트 상자 대신 국가의 드롭다운 목록이 표시되도록 표시됩니다.

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

또한 HTTP-POST 편집 방법(오류가 발생할 경우 시나리오)에서 편집 보기 템플릿을 렌더링하므로 이 메서드를 업데이트하여 뷰 템플릿이 오류 시나리오에서 렌더링될 때 SelectList를 ViewData에 추가하도록 해야 합니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

이제 DinnersController 편집 시나리오는 드롭다운리스트를 지원합니다.

### <a name="using-a-viewmodel-pattern"></a>뷰모델 패턴 사용

ViewData 사전 접근 방식은 매우 빠르고 쉽게 구현할 수 있다는 이점이 있습니다. 그러나 일부 개발자는 오타가 컴파일 타임에 잡히지 않는 오류로 이어질 수 있기 때문에 문자열 기반 사전을 사용하는 것을 좋아하지 않습니다. 형식이 없는 ViewData 사전에서는 뷰 템플릿에서 C#과 같은 강력한 형식의 언어를 사용할 때 "as" 연산자 또는 캐스팅을 사용해야합니다.

사용할 수 있는 다른 방법은 종종 "ViewModel" 패턴이라고 합니다. 이 패턴을 사용할 때 특정 뷰 시나리오에 최적화된 강력한 형식의 클래스를 만들고 뷰 템플릿에 필요한 동적 값/콘텐츠에 대한 속성을 노출합니다. 그런 다음 컨트롤러 클래스는 이러한 뷰 최적화 클래스를 채우고 사용할 뷰 템플릿으로 전달할 수 있습니다. 이를 통해 뷰 템플릿 내에서 형식 안전, 컴파일 타임 검사 및 편집기 intellisense를 사용할 수 있습니다.

예를 들어 저녁 식사 양식 편집 시나리오를 활성화하려면 다음과 같은 "DinnerFormViewModel" 클래스를 만들 수 있습니다.이 클래스는 두 개의 강력한 형식속성을 노출합니다: Dinner 개체 및 국가 드롭다운 목록을 채우는 데 필요한 SelectList 모델:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

그런 다음 Edit() 작업 메서드를 업데이트하여 리포지토리에서 검색한 Dinner 개체를 사용하여 DinnerFormViewModel을 만든 다음 뷰 템플릿에 전달할 수 있습니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

그런 다음 view 템플릿을 업데이트하여 다음과 같이 edit.aspx 페이지 상단의 "상속" 특성을 변경하여 "DinnerFormViewModel" 대신 "DinnerFormViewModel"을 예상합니다.

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

이렇게 하면 뷰 템플릿 내의 "모델" 속성의 intellisense가 업데이트되어 전달하는 DinnerFormViewModel 형식의 개체 모델을 반영합니다.

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

그런 다음 뷰 코드를 업데이트하여 업데이트하여 작동할 수 있습니다. 우리가 만드는 입력 요소의 이름을 변경 하지 않는 방법 아래 공지 (양식 요소는 여전히 "제목", "국가") – 하지만 우리는 DinnerFormViewModel 클래스를 사용 하 여 값을 검색 하는 HTML 도우미 메서드를 업데이트 하 고:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

또한 오류를 렌더링할 때 DinnerFormViewModel 클래스를 사용하도록 편집 게시물 메서드를 업데이트합니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

또한 Create() 작업 메서드를 업데이트하여 동일한 *DinnerFormViewModel* 클래스를 다시 사용하여 해당 국가 내에 있는 DropDownList도 사용할 수 있습니다. 다음은 HTTP-GET 구현입니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

다음은 HTTP-POST 만들기 메서드의 구현입니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

이제 편집 및 만들기 화면 모두 국가 선택을 위한 드롭다운 목록을 지원합니다.

### <a name="custom-shaped-viewmodel-classes"></a>사용자 지정 모양의 뷰모델 클래스

위의 시나리오에서 DinnerFormViewModel 클래스는 지원 SelectList 모델 속성과 함께 Dinner 모델 개체를 속성으로 직접 노출합니다. 이 방법은 뷰 템플릿 내에서 만들려는 HTML UI가 도메인 모델 개체와 비교적 밀접하게 일치하는 시나리오에서 잘 작동합니다.

그렇지 않은 시나리오의 경우 개체 모델이 뷰에서 소비에 더 최적화되어 있고 기본 도메인 모델 개체와 완전히 다르게 보일 수 있는 사용자 지정 모양의 ViewModel 클래스를 만드는 것이 사용할 수 있습니다. 예를 들어 여러 모델 개체에서 수집된 다른 속성 이름 및/또는 집계 속성을 잠재적으로 노출할 수 있습니다.

사용자 정의 모양의 ViewModel 클래스는 컨트롤러에서 뷰로 데이터를 전달하고 컨트롤러의 작업 메서드에 다시 게시된 양식 데이터를 처리하는 데 모두 사용할 수 있습니다. 이 이후 시나리오에서는 작업 메서드가 양식 게시 데이터로 ViewModel 개체를 업데이트한 다음 ViewModel 인스턴스를 사용하여 실제 도메인 모델 개체를 매핑하거나 검색하도록 할 수 있습니다.

사용자 지정 모양의 ViewModel 클래스는 많은 유연성을 제공할 수 있으며 보기 템플릿 내에서 렌더링 코드를 찾거나 작업 메서드 내에서 양식 게시 코드가 너무 복잡해지기 시작할 때마다 조사할 수 있습니다. 이는 도메인 모델이 생성하는 UI와 깔끔하게 일치하지 않으며 중간 사용자 지정 모양의 ViewModel 클래스가 도움이 될 수 있다는 신호일 수 있습니다.

### <a name="next-step"></a>다음 단계

이제 부분 및 마스터 페이지를 사용하여 응용 프로그램 전체에서 UI를 다시 사용하고 공유하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [다음](re-use-ui-using-master-pages-and-partials.md)
