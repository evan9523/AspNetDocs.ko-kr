---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: UpdatePanel (VB) 하지 않고 팝업 컨트롤에서 포스트백 처리 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. Su에서 포스트백을 발생 하면...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: 6dcb2b09279ec6400465f79fadc2a1b6c72f8f07
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064560"
---
<a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a>UpdatePanel을 사용하지 않고 팝업 컨트롤에서 포스트백 처리(VB)
====================
by [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)

> AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. 이러한 패널의 포스트백이 발생할 때 페이지에 여러 패널 패널 클릭 했는지 확인 하기 어렵습니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. 이러한 패널의 포스트백이 발생할 때 페이지에 여러 패널 패널 클릭 했는지 확인 하기 어렵습니다.

## <a name="steps"></a>단계

사용 하는 경우는 `PopupControl` 포스트백을 있지만 필요 없이 `UpdatePanel` 페이지의 컨트롤 도구 키트에서 포스트백을 발생 하는 팝업을 트리거 했습니다. 클라이언트 요소를 결정 하는 방법을 제공 하지 않습니다. 그러나 작은 트릭이이 시나리오에 대 한 해결 방법을 제공 합니다.

먼저, 기본 설정 같습니다.:는 모두 동일한 팝업 일정 트리거는 두 개의 텍스트 상자입니다. 두 `PopupControlExtenders` 텍스트 상자 및 팝업을 결합 합니다.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

기본 개념에는 숨겨진된 폼 필드를 추가 하는 것은 &lt; `form` &gt; 팝업을 시작 하는 입력란을 포함 하는 요소:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

페이지 로드 되 면 두 텍스트 상자에 이벤트 처리기를 추가 하는 JavaScript 코드: 사용자가 텍스트 상자에 때마다 이름과 숨겨진된 폼 필드에 기록 됩니다.

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

서버 쪽 코드에서 숨겨진된 필드의 값을 읽어야 합니다. 숨겨진된 양식 필드를 조작 하는 간단한 되므로 숨겨진된 값의 유효성을 검사 방법은 화이트 리스트 필요한 것입니다. 올바른 입력란을 식별 한 후 달력에서 날짜에 기록 됩니다.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]


[![텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다.](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)

텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다 ([클릭 하 여 큰 이미지 보기](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))


[![날짜를 클릭 하면 텍스트 상자에 전환](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)

날짜를 클릭 하면 텍스트 상자에 배치 ([클릭 하 여 큰 이미지 보기](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))

> [!div class="step-by-step"]
> [이전](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
