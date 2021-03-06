---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: UpdatePanel을 사용 하 여 Popup 컨트롤에서 포스트백 처리 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. 특별 한 주의를 기울여야 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: dd045ae56696c7944df98cf805ba812fde1bb4ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496637"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a>UpdatePanel을 사용하여 팝업 컨트롤의 포스트백 처리(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)

> AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. 이러한 팝업 내에서 포스트백이 발생 하는 경우 특별 한 주의를 기울여야 합니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. 이러한 팝업 내에서 포스트백이 발생 하는 경우 특별 한 주의를 기울여야 합니다.

## <a name="steps"></a>단계

포스트백을 사용 하 여 `PopupControl`를 사용 하는 경우 `UpdatePanel`는 포스트백으로 인 한 페이지 새로 고침을 방지할 수 있습니다. 다음 태그는 몇 가지 중요 한 요소를 정의 합니다.

- ASP.NET AJAX 컨트롤 Toolkit이 작동 하도록 하는 `ScriptManager` 컨트롤
- 둘 다 popup을 트리거하는 두 개의 `TextBox` 컨트롤
- Popup으로 사용할 `Panel` 컨트롤
- 패널 내에서 `Calendar` 컨트롤은 `UpdatePanel` 컨트롤 내에 포함 되어 있습니다.
- 텍스트 상자에 패널을 할당 하는 두 개의 `PopupControlExtender` 컨트롤

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

`Calendar` 컨트롤의 `OnSelectionChanged` 특성이 설정 되어 있는지 확인 합니다. 따라서 사용자가 일정 내에서 날짜를 선택 하면 포스트백이 발생 하 고 서버 쪽 메서드 `c1_SelectionChanged()`이 실행 됩니다. 이 메서드 내에서 현재 날짜를 검색 하 여 텍스트 상자에 다시 써야 합니다.

이에 대 한 구문은 다음과 같습니다. 즉, 먼저 페이지의 `PopupControlExtender`에 대 한 프록시 개체를 생성 해야 합니다. ASP.NET AJAX 컨트롤 도구 키트는 `GetProxyForCurrentPopup()` 메서드를 제공 합니다. 이 메서드가 반환 하는 개체는 메서드 호출을 트리거한 컨트롤이 아니라 popup을 트리거한 컨트롤로 값을 다시 보내는 `Commit()` 메서드를 지원 합니다. 다음 코드에서는 선택 된 날짜를 `Commit()` 메서드에 대 한 인수로 제공 하 여 코드에서 선택한 날짜를 텍스트 상자에 다시 씁니다.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

이제 달력 날짜를 클릭할 때마다 선택한 날짜가 연결 된 텍스트 상자에 표시 되어 현재 여러 웹 사이트에서 찾을 수 있는 날짜 선택 컨트롤을 만듭니다.

[사용자가 텍스트 상자를 클릭할 때 달력이 표시 되는 ![](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)

사용자가 텍스트 상자를 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png)).

[날짜를 클릭 ![텍스트 상자에 배치 됩니다.](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)

날짜를 클릭 하면 텍스트 상자에 배치 됩니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png)).

> [!div class="step-by-step"]
> [이전](using-multiple-popup-controls-vb.md)
> [다음](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)
