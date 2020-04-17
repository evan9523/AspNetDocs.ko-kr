---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: 컬러피커 컨트롤 익스텐더(VB) 사용 | 마이크로 소프트 문서
author: rick-anderson
description: ColorPicker는 팝업 컨트롤에서 UI와 클라이언트 측 색상 선택 기능을 제공하는 ASP.NET AJAX 익스텐더입니다. 그것은 어떤 ASP.NET 부착 할 수 있습니다 ...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: c373102665ac17020ca8d5f14d3488a874bb68de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542848"
---
# <a name="using-the-colorpicker-control-extender-vb"></a>컬러피커 컨트롤 익스텐더(VB) 사용

[로 마이크로 소프트](https://github.com/microsoft)

> ColorPicker는 팝업 컨트롤에서 UI와 클라이언트 측 색상 선택 기능을 제공하는 ASP.NET AJAX 익스텐더입니다. 모든 ASP.NET TextBox 컨트롤에 연결할 수 있습니다. 그것은.

이 자습서의 목표는 AJAX 제어 도구 키트 ColorPicker 컨트롤 익스텐더를 사용하는 방법을 설명하는 것입니다. ColorPicker 컨트롤 익스텐더에는 색상을 선택할 수 있는 팝업 대화 상자가 표시됩니다. ColorPicker는 사용자가 색상을 선택할 수 있도록 직관적인 사용자 인터페이스를 제공하려는 경우에 유용합니다.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>색상 선택기 컨트롤 확장기를 사용하여 텍스트 상자 컨트롤 확장

예를 들어 방문자가 사용자 지정된 명함을 만들 수 있는 웹 사이트를 만들려고 한다고 가정해 보겠습니다. 방문자는 명함의 텍스트를 입력하고 색상을 선택할 수 있습니다. 목록 1의 ASP.NET 페이지에는 txtCardText 및 txtCardColor라는 두 개의 텍스트 상자 컨트롤이 포함되어 있습니다. 양식을 제출하면 선택한 값이 표시됩니다(그림 1 참조).

[![명함을 만들기 위한 간단한 양식](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**그림 01**: 명함을 만들기위한 간단한 양식[(전체 크기 이미지를 보려면 클릭)](using-the-colorpicker-control-extender-vb/_static/image2.png)

**목록 1 - CreateCard.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

목록 1의 양식은 작동하지만 훌륭한 사용자 환경을 제공하지는 않습니다. 사용자는 텍스트 상자에 색상을 입력해야 합니다. 사용자가 완두콩 녹색의 올바른 음영과 같은 특수 한 색상을 원한다면 사용자는 도움없이 HTML 색상 코드를 파악해야합니다.

ColorPicker 컨트롤 익스텐더를 사용하여 더 나은 사용자 환경을 만들 수 있습니다. TextBox 컨트롤로 포커스를 이동할 때 ColorPicker에 색상 대화 상자가 표시됩니다(그림 2 참조).

[![컬러피커 컨트롤 익스텐더](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**그림 02**: 컬러 피커 컨트롤 익스텐더[(전체 크기 이미지를 보려면 클릭)](using-the-colorpicker-control-extender-vb/_static/image4.png)

목록 1의 양식과 함께 ColorPicker 컨트롤 익스텐더를 사용하려면 두 단계를 완료해야 합니다.

1. 페이지에 스크립트 관리자 컨트롤 추가
2. 페이지에 ColorPicker 컨트롤 익스텐더 추가

ColorPicker를 사용하려면 먼저 페이지에 ScriptManager를 추가해야 합니다. ScriptManager를 추가하는 좋은 장소는 열기 서버 측 &lt;&gt; 양식 태그 바로 아래에 있습니다. 도구 상자에서 페이지로 ScriptManager를 드래그할 수 있습니다(스크립트 관리자는 AJAX 확장 탭 아래에 있음). 또는 열기 서버 측 양식 태그 아래에 다음 태그를 소스 보기에 입력할 수 있습니다.

&lt;asp:스크립트관리자 ID="스크립트관리자1" 런나트="서버" /&gt;

페이지에 ColorPicker 컨트롤 익스텐더를 추가하는 가장 쉬운 방법은 디자인 뷰에 있습니다. txtCardColor 텍스트 상자 위에 마우스를 가져가면 확장기를 추가할 수 있는 스마트 작업 옵션이 나타납니다(그림 3 참조). 이 옵션을 선택하면 확장자 마법사가 나타납니다(그림 4 참조).

[![익스텐더 추가](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**그림 03**: 익스텐더 추가[(전체 크기 이미지를 보려면 클릭)](using-the-colorpicker-control-extender-vb/_static/image6.png)

[![익스텐더 마법사를 사용하여 컨트롤 익스텐더 선택](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**그림 04**: 익스텐더 마법사를 사용하여 컨트롤 익스텐더 선택[(전체 크기 이미지를 보려면 클릭)](using-the-colorpicker-control-extender-vb/_static/image8.png)

ColorPicker 익스텐더를 선택하여 colorPicker 익스텐더를 사용하여 txtCardColor 텍스트 상자를 확장할 수 있습니다. 확인을 클릭하여 대화 상자를 닫습니다.

이러한 변경을 하면 페이지의 소스가 목록 2처럼 보입니다.

**목록 2 - CreateCard.aspx(컬러선택기)**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

이제 페이지에 txtCardColor 텍스트 상자 컨트롤 바로 아래에 나타나는 ColorPickerExtender 컨트롤이 포함되어 있습니다. ColorPickerExtender 컨트롤은 txtCardColor 컨트롤을 확장하여 색상 선택기 대화 상자를 표시합니다.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>단추를 사용하여 색상 선택기 대화 상자 시작

ColorPicker 익스텐더는 다음 속성을 지원합니다.

- 팝업ButtonId - 색상 선택기 대화 상자가 나타나는 페이지의 단추 ID입니다.
- 팝업 위치 - 색상 선택 기 대화 상자의 대상 컨트롤을 기준으로 하는 위치입니다. 가능한 값은 절대, 가운데, 아래쪽 왼쪽, 아래쪽 오른쪽, 맨 위 왼쪽, 오른쪽, 왼쪽(기본값은 아래쪽 왼쪽)입니다.
- SampleControlId - 선택한 색상을 표시하는 컨트롤의 ID입니다.
- 선택색상 - ColorPicker가 선택한 초기 색상입니다.

이러한 속성을 사용하여 색상 선택 대화 상자가 표시되는 방법과 선택한 색상이 표시되는 방법을 사용자 지정할 수 있습니다. 목록 3의 페이지에서는 이러한 속성 중 몇 가지를 사용하는 방법을 보여 줍니다.

**목록 3 - 만들기CardButton.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

목록 3의 페이지에는 색상 선택 버튼이 포함되어 있습니다(그림 5 참조). 이 단추를 클릭하면 텍스트 상자 위에 색상 선택기 대화 상자가 나타납니다. 대화 상자에서 색상을 선택하면 선택한 색상이 lblSample 레이블 컨트롤의 배경색으로 나타납니다.

ColorPicker PopupButtonID 속성은 색상 선택 단추를 ColorPicker 익스텐더와 연결하는 데 사용됩니다. PopupButtonID 속성에 대 한 값을 제공 하는 경우 대상 컨트롤에 포커스가 있을 때 색상 선택 대화 상자가 더 이상 나타나지 않습니다. 대화 상자를 표시하려면 단추를 클릭해야 합니다.

SampleControlID 속성은 선택한 색상을 ColorPicker와 연결하는 데 사용됩니다. ColorPicker는 이 컨트롤의 배경색을 현재 선택한 색상으로 변경합니다.

[![단추로 색상 선택 대화 상자 표시](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**그림 05**: 버튼으로 색상 선택기 대화 상자 표시[(전체 크기 이미지를 보려면 클릭)](using-the-colorpicker-control-extender-vb/_static/image10.png)

## <a name="summary"></a>요약

이 자습서에서는 ColorPicker 컨트롤 익스텐더를 사용하여 팝업 색상 선택기 대화 상자를 표시하는 방법을 배웠습니다. 먼저 포커스가 TextBox 컨트롤로 이동될 때 대화 상자를 표시하는 방법을 살펴보습니다. 다음으로 단추를 클릭할 때 색상 선택 대화 상자를 표시하는 단추를 만드는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](using-the-colorpicker-control-extender-cs.md)
