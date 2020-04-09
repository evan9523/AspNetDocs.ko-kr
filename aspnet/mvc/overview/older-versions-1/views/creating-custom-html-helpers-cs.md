---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 사용자 지정 HTML 도우미 만들기(C#) | 마이크로 소프트 문서
author: microsoft
description: 이 자습서의 목표는 MVC 보기 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주는 것입니다. HTML 도우미를 활용 하 여...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a2e5a5b42aa5bf267a42fef2fcad7022001ce6f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675333"
---
# <a name="creating-custom-html-helpers-c"></a>사용자 지정 HTML 도우미 만들기(C#)

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> 이 자습서의 목표는 MVC 보기 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주는 것입니다. HTML 도우미를 활용 하 여 표준 HTML 페이지를 만들 려면 수행 해야 하는 HTML 태그의 지루한 입력의 양을 줄일 수 있습니다.

이 자습서의 목표는 MVC 보기 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주는 것입니다. HTML 도우미를 활용 하 여 표준 HTML 페이지를 만들 려면 수행 해야 하는 HTML 태그의 지루한 입력의 양을 줄일 수 있습니다.

이 자습서의 첫 번째 부분에서는 ASP.NET MVC 프레임워크에 포함된 기존 HTML 도우미 중 일부를 설명합니다. 다음으로 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 설명합니다.

## <a name="understanding-html-helpers"></a>HTML 도우미 이해

HTML 도우미는 문자열을 반환 하는 메서드입니다. 문자열은 원하는 모든 유형의 콘텐츠를 나타낼 수 있습니다. 예를 들어 HTML 도우미를 사용하여 HTML `<input>` 및 태그와 `<img>` 같은 표준 HTML 태그를 렌더링할 수 있습니다. 또한 HTML 도우미를 사용하여 탭 스트립이나 데이터베이스 데이터의 HTML 테이블과 같은 보다 복잡한 콘텐츠를 렌더링할 수도 있습니다.

ASP.NET MVC 프레임워크에는 다음과 같은 표준 HTML 도우미 집합이 포함되어 있습니다(전체 목록은 아닙니다).

- Html.액션링크()
- Html.시작 양식()
- Html.체크 박스()
- Html.드롭다운리스트()
- Html.엔드폼()
- Html.Hidden()
- Html.리스트박스()
- Html.암호()
- Html.라디오 버튼()
- Html.텍스트 영역()
- Html.텍스트 상자()

예를 들어 목록 1의 양식을 고려합니다. 이 양식은 표준 HTML 도우미 두 대의 도움을 받아 렌더링됩니다(그림 1 참조). 이 양식은 `Html.BeginForm()` `Html.TextBox()` 및 도우미 메서드를 사용하여 간단한 HTML 양식을 렌더링합니다.

[![HTML 도우미로 렌더링된 페이지](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**그림 01**: HTML 도우미로 렌더링된[페이지(전체 크기 이미지를 보려면 클릭)](creating-custom-html-helpers-cs/_static/image3.png)

**리스팅 1 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

Html.BeginForm() 도우미 메서드는 HTML `<form>` 태그를 열고 닫는 데 사용됩니다. 메서드는 `Html.BeginForm()` using 문 내에서 호출 됩니다. using 문은 사용 블록의 `<form>` 끝에서 태그가 닫히도록 합니다.

원하는 경우 사용 블록을 만드는 대신 Html.EndForm() 도우미 메서드를 호출하여 `<form>` 태그를 닫을 수 있습니다. 가장 직관적인 것처럼 보이는 열기 `<form>` 및 닫기 태그를 만들 려면 어떤 접근 방식을 사용하십시오.

도우미 `Html.TextBox()` 메서드는 목록 1에서 HTML `<input>` 태그를 렌더링하는 데 사용됩니다. 브라우저에서 소스 보기를 선택하면 목록 2에 HTML 소스가 표시됩니다. 원본에 표준 HTML 태그가 포함되어 있습니다.

> [!IMPORTANT]
> `Html.TextBox()`-HTML 도우미는 `<% %>` 태그 대신 태그로 `<%= %>` 렌더링됩니다. 동일한 기호를 포함하지 않으면 브라우저에 렌더링되지 않습니다.

ASP.NET MVC 프레임워크에는 작은 도우미 집합이 포함되어 있습니다. 대부분의 경우 사용자 지정 HTML 도우미를 사용하여 MVC 프레임워크를 확장해야 합니다. 이 자습서의 나머지 부분에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 배웁니다.

**리스팅 2 –`Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>정적 메소드를 사용 하 고 HTML 도우미 만들기

새 HTML 도우미를 만드는 가장 쉬운 방법은 문자열을 반환 하는 정적 메서드를 만드는 것입니다. 예를 들어 HTML `<label>` 태그를 렌더링하는 새 HTML 도우미를 만들기로 결정한다고 가정해 보겠습니다. 목록 2의 클래스를 사용하여 `<label>` 을 렌더링할 수 있습니다.

**리스팅 2 –`Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

목록 2의 클래스에 대해 특별한 것은 없습니다. 메서드는 `Label()` 단순히 문자열을 반환합니다.

목록 3의 수정된 인덱스 `LabelHelper` 보기는 `<label>` HTML 태그를 렌더링하는 데 를 사용합니다. `Application1.Helpers` 보기에는 네임스페이스를 `<%@ imports %>` 가져오는 지시문이 포함되어 있습니다.

**리스팅 2 –`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>확장 방법을 사용 하 고 HTML 도우미 만들기

ASP.NET MVC 프레임워크에 포함된 표준 HTML 도우미와 마찬가지로 작동하는 HTML 도우미를 만들려면 확장 메서드를 만들어야 합니다. 확장 메서드를 사용하면 기존 클래스에 새 메서드를 추가할 수 있습니다. HTML 도우미 메서드를 만들 때 뷰의 Html 속성으로 표시되는 HtmlHelper 클래스에 새 메서드를 추가합니다.

목록 3의 클래스는 명명된 `HtmlHelper` `Label()`클래스에 확장 메서드를 추가합니다. 이 클래스에 대해 알아두어야 할 몇 가지 사항이 있습니다. 먼저 클래스가 정적 클래스임을 알 수 있습니다. 정적 클래스를 사용하여 확장 메서드를 정의해야 합니다.

둘째, `Label()` 메서드의 첫 번째 매개 변수 앞에 키워드가 `this`앞에 옵니다. 확장 메서드의 첫 번째 매개 변수는 확장 메서드가 확장되는 클래스를 나타냅니다.

**리스팅 3 –`Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

확장 메서드를 만들고 응용 프로그램을 성공적으로 빌드하면 확장 메서드가 클래스의 다른 모든 메서드와 마찬가지로 Visual Studio Intellisense에 나타납니다(그림 2 참조). 유일한 차이점은 확장 메서드 옆에 특수 기호(아래쪽 화살표아이콘)가 표시된다는 것입니다.

[![Html.Label() 확장 메서드 사용](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**그림 02**: Html.Label() 확장 방법을 사용하여[(전체 크기 이미지를 보려면 클릭하십시오)](creating-custom-html-helpers-cs/_static/image6.png)

목록 4의 수정된 인덱스 보기는 Html.Label() 확장 `<label>` 메서드를 사용하여 모든 태그를 렌더링합니다.

**리스팅 4 –`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>요약

이 자습서에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 배웠습니다. 먼저 문자열을 반환하는 정적 `Label()` 메서드를 만들어 사용자 지정 HTML 도우미를 만드는 방법을 배웠습니다. 다음으로 클래스에 확장 메서드를 `Label()` 만들어 사용자 지정 HTML 도우미 `HtmlHelper` 메서드를 만드는 방법을 배웠습니다.

이 자습서에서는 매우 간단한 HTML 도우미 메서드를 빌드하는 데 중점을 두어 사용했습니다. HTML 도우미는 원하는 만큼 복잡할 수 있습니다. 트리 보기, 메뉴 또는 데이터베이스 데이터 테이블과 같은 풍부한 콘텐츠를 렌더링하는 HTML 도우미를 빌드할 수 있습니다.

> [!div class="step-by-step"]
> [이전](asp-net-mvc-views-overview-cs.md)
> [다음](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
