---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: 사용자 지정 HTML 도우미 (VB) 만들기 | Microsoft Docs
author: microsoft
description: MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위해이 자습서의 목표가입니다. HTML 도우미를 활용 하는 중...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: e62e47bceddc516af7aa18fc66ed4ca4d704d277
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034950"
---
<a name="creating-custom-html-helpers-vb"></a>사용자 지정 HTML 도우미 만들기(VB)
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위해이 자습서의 목표가입니다. HTML 도우미를 활용 하 여 표준 HTML 페이지 만들기를 수행 해야 하는 HTML 태그의 지루한 작업 입력의 크기를 줄일 수 있습니다.


MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위해이 자습서의 목표가입니다. HTML 도우미를 활용 하 여 표준 HTML 페이지 만들기를 수행 해야 하는 HTML 태그의 지루한 작업 입력의 크기를 줄일 수 있습니다.

이 자습서의 첫 번째 부분에서는 설명 ASP.NET MVC framework에 포함 된 기존 HTML 도우미 중 일부입니다. 다음으로, 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 설명 합니다. 공유 메서드를 만들어 및 확장 메서드를 만들어 사용자 지정 HTML 도우미를 만드는 방법을 설명 하겠습니다.

## <a name="understanding-html-helpers"></a>HTML 도우미 이해

HTML 도우미는 문자열을 반환 하는 메서드입니다. 문자열에는 모든 유형의 콘텐츠를 나타낼 수 있습니다. 예를 들어 HTML과 같은 표준 HTML 태그를 렌더링할 HTML 도우미를 사용할 수 있습니다 `<input>` 고 `<img>` 태그입니다. 탭 스트립 또는 데이터베이스 데이터의 HTML 테이블을 같은 더 복잡 한 콘텐츠를 렌더링 HTML 도우미를 사용할 수도 있습니다.

ASP.NET MVC 프레임 워크에 (이 전체 목록은 아님)는 표준 HTML 도우미의 다음 집합에 포함 됩니다.

- Html.ActionLink()
- Html.BeginForm()
- Html.CheckBox()
- Html.DropDownList()
- Html.EndForm()
- Html.Hidden()
- Html.ListBox()
- Html.Password()
- Html.RadioButton()
- Html.TextArea()
- Html.TextBox()

예를 들어 목록 1에서 폼을 고려 합니다. 이 폼은 두 표준 HTML 도우미 (그림 1 참조)를 사용 하 여 렌더링 됩니다. 이 폼에서 사용 하 여 `Html.BeginForm()` 및 `Html.TextBox()` 도우미 메서드.


[![HTML 도우미를 사용 하 여 페이지 렌더링](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)

**그림 01**: HTML 도우미를 사용 하 여 페이지 렌더링 ([클릭 하 여 큰 이미지 보기](creating-custom-html-helpers-vb/_static/image3.png))


**목록 1 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

합니다 `Html.BeginForm()` 도우미 메서드를 사용 하는 중괄호 및 닫는 HTML 만드는 `<form>` 태그입니다. `Html.BeginForm()` 메서드를 사용 하 여 내는 문입니다. 문을 사용 하 여는 `<form>` 사용 하 여 끝 태그가 닫혀 가져옵니다 블록입니다.

사용 하 여 만드는 대신 선호 하는 경우 블록을 닫는 Html.EndForm() 도우미 메서드를 호출할 수 있습니다는 `<form>` 태그입니다. 어떤 방식을 선택 하 여 만들기 및 닫기 사용 `<form>` 가장 직관적인 보이는 태그입니다.

합니다 `Html.TextBox()` 도우미 메서드는 목록 1에서 HTML을 렌더링 하는 데 사용 됩니다 `<input>` 태그입니다. 브라우저에서 소스 보기를 선택 하는 경우의 HTML 소스 목록 2에 표시 됩니다. 소스 표준 HTML 태그가 포함 되어 있는지 확인 합니다.

> [!IMPORTANT]
> 다음에 유의 합니다 `Html.TextBox()`HTML 도우미와 함께 렌더링 된 `<%= %>` 대신 태그 `<% %>` 태그. 등호 기호를 포함 하지 않으면 브라우저에 렌더링 가져옵니다 아무 작업도 수행 합니다.

ASP.NET MVC 프레임 워크는 작은 도우미 집합이 포함 되어 있습니다. 대부분의 경우 사용자 지정 HTML 도우미를 사용 하 여 MVC 프레임 워크를 확장 해야 합니다. 이 자습서의 나머지 부분에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 알아봅니다.

**2 – 나열 `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a>공유 메서드를 사용 하 여 HTML 도우미 만들기

새 HTML 도우미를 만드는 가장 쉬운 방법은 문자열을 반환 하는 공유 메서드를 만드는 경우 Imagine, 예를 들어, HTML을 렌더링 하는 새 HTML 도우미 만들려는 `<label>` 태그입니다. 목록 2 클래스를 사용 하 여 렌더링 하는 수는 `<label>`합니다.

**2 – 나열 `Helpers\LabelHelper.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

목록 2에서 클래스에 대 한 특별 합니다. `Label()` 메서드는 단순히 문자열을 반환 합니다.

목록 3에서 수정 된 인덱스 뷰를 사용 하 여 `LabelHelper` HTML을 렌더링 하 `<label>` 태그입니다. 뷰를 포함 한 `<%@ imports %>` Application1.Helpers 네임 스페이스를 가져오는 지시문입니다.

**2 – 나열 `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>확장 메서드를 사용 하 여 HTML 도우미 만들기

만들려는 작동 하는 HTML 도우미와 같은 경우 확장 메서드를 만들려면 ASP.NET MVC 프레임 워크에 포함 하는 표준 HTML 도우미입니다. 확장 메서드를 사용 하면 기존 클래스에 새 메서드를 추가할 수 있습니다. 새 메서드를 추가 하는 HTML 도우미 메서드를 만들 때의 `HtmlHelper` 뷰의 Html 속성을 나타내는 클래스입니다.

라는 확장 메서드를 추가 하는 목록 3에 있는 Visual Basic 모듈 `Label()` 에 `HtmlHelper` 클래스입니다. 이 모듈에 대 한 유의 해야 하는 것 중 몇 가지 있습니다. 먼저 모듈으로 데코 레이트 된 있는지를 확인 합니다 `<Extension()>` 특성입니다. 이 특성을 사용 하려면 가져와야는 `System.Runtime.CompilerServices` 네임 스페이스

둘째, 있음을의 첫 번째 매개 변수를 `Label()` 메서드를 나타냅니다는 `HtmlHelper` 클래스입니다. 확장 메서드의 첫 번째 매개 변수는 확장 메서드를 확장 하는 클래스를 나타냅니다.

**3 – 나열 `Helpers\LabelExtensions.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

확장 메서드는 모든 클래스의 다른 메서드 같은 Visual Studio Intellisense 확장 메서드를 만들고 응용 프로그램을 성공적으로 빌드 후 나타나는 (그림 2 참조). 유일한 차이점은 해당 확장명 메서드 (아래쪽 화살표 아이콘) 옆에 있는 특수 기호를 사용 하 여 표시 합니다.


[![Html.Label() 확장 메서드를 사용 하 여](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)

**그림 02**: Html.Label() 확장 메서드를 사용 하 여 ([클릭 하 여 큰 이미지 보기](creating-custom-html-helpers-vb/_static/image6.png))


목록 4에서 수정 된 인덱스 뷰 Html.Label() 확장 메서드를 사용 하 여 모든 렌더링 하는 &lt;레이블&gt; 태그입니다.

**4-목록 `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a>요약

이 자습서에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 살펴보았습니다. 사용자 지정 하는 방법과 먼저 `Label()` HTML 도우미를 만들어 공유 메서드는 문자열을 반환 합니다. 사용자 지정 하는 방법과 어 `Label()` 에 확장 메서드를 만들어 HTML 도우미 메서드는 `HtmlHelper` 클래스입니다.

이 자습서에서는 매우 간단한 HTML 도우미 메서드를 작성에 집중 합니다. 실현 하는 HTML 도우미는 원하는 만큼 복잡 해질 수 있습니다. 트리 뷰, 메뉴 또는 데이터베이스 데이터의 테이블과 같은 다양 한 콘텐츠를 렌더링 하는 HTML 도우미를 작성할 수 있습니다.

> [!div class="step-by-step"]
> [이전](asp-net-mvc-views-overview-vb.md)
> [다음](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
