---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
title: 서버 코드 (VB)에서 모달 팝업 창 시작 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 일부 시나리오는 t 해야 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 36ca81d7-906d-4db2-952b-add18a4ff421
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 55ee67150d1567a0334988a06ff0fcca8a89bbd4
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404054"
---
# <a name="launching-a-modal-popup-window-from-server-code-vb"></a>서버 코드에서 모달 팝업 창 시작(VB)

by [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)

> AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 일부 시나리오는 서버 쪽에서 모달 팝업의 열기를 트리거한 필요 합니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 일부 시나리오는 서버 쪽에서 모달 팝업의 열기를 트리거한 필요 합니다.

## <a name="steps"></a>단계

먼저, ASP.NET Button 웹 컨트롤 ModalPopup 컨트롤의 작동 방식을 보여 주기 위해 필요 합니다. 이러한 단추를 추가 합니다 &lt;폼&gt; 새 페이지에는 요소:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample1.aspx)]

그런 다음 태그를 만들려는 팝업 필요 합니다. 정의는 `<asp:Panel>` 컨트롤과 Button 컨트롤을 포함 하는지 확인 합니다. 또한 ModalPopup 컨트롤은 단추를 만들려면 이러한 닫기 팝업; 기능을 제공 합니다. 그렇지 않으면 사라집니다 수 있도록 쉽게 없습니다 있습니다.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample2.aspx)]

다음 페이지에 ASP.NET AJAX Toolkit의 ModalPopup 컨트롤을 추가 합니다. 컨트롤을 로드 하는 단추, 사라지는 수 있도록 하는 단추와 실제 팝업의 ID에 대 한 속성을 설정 합니다.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample3.aspx)]

ASP.NET AJAX를을 기준으로 모든 웹 페이지와 마찬가지로 스크립트 관리자는 다른 대상 브라우저에 대 한 필요한 JavaScript 라이브러리를 로드 해야 합니다.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample4.aspx)]

브라우저에서 예제를 실행 합니다. 단추를 클릭할 때 모달 팝업이 나타납니다. 서버 쪽 코드를 사용 하 여 동일한 효과 달성 하기 위해 새 단추는 필요 합니다.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample5.aspx)]

알 수 있듯이 단추 클릭 포스트백을 생성 하 고 실행 된 `ServerButton_Click()` 서버의 메서드. 이 메서드는 JavaScript 함수 호출 `launchModal()` 실행을 정확 하 게 하려면 JavaScript 함수 실행 됩니다 페이지가 로드 되 면:

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample6.aspx)]

작업을 `launchModal()` 는 ModalPopup 표시 하는 것입니다. `launchModal()` 함수는 전체 HTML 페이지가 로드 된 후 실행 됩니다. 그러나 그 순간 ASP.NET AJAX 프레임 워크 로드 되지 않았습니다 완전히 아직 있습니다. 따라서는 `launchModal()` 함수 ModalPopup 컨트롤을 나중에 표시 되어야 합니다는 변수로 설정 합니다.

[!code-html[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample7.html)]

`pageLoad()` JavaScript 함수는 ASP.NET AJAX 완전히 로드 되 면 실행 되는 특수 함수입니다. 따라서 코드 ModalPopup 컨트롤 이지만 경우에만 표시 하려면이 함수를 추가 했습니다 `launchModal()` 가 하기 전에 호출 되었습니다.

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample8.js)]

`$find()` 함수 페이지에서 명명된 된 요소를 찾고 및 서버 쪽 ID를 매개 변수로 필요 합니다. 따라서 `$find("mpe")` ModalPopup 컨트롤의 클라이언트 표시를 반환 합니다. 해당 `show()` 메서드를 표시 하는 팝업을 사용 합니다.


[![T모달 팝업 그 때 나타나는 단추 중 하나를 클릭](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)

모달 팝업이 표시 되는 경우 단추 중 하나를 클릭 하 고 ([클릭 하 여 큰 이미지 보기](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](positioning-a-modalpopup-cs.md)
> [다음](using-modalpopup-with-a-repeater-control-vb.md)
