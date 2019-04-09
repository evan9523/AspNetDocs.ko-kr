---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: 웹 서비스 백 엔드 (VB)를 사용 하 여 숫자 위로/아래로 컨트롤 만들기 | Microsoft Docs
author: wenz
description: 확인 상자에 값을 입력 하는 사용자를 대신 숫자 위로/아래로 컨트롤 (Windows 및 기타 운영 체제에 있는) 점점 더 많은 c 증명 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 0442b5e22e44e0767825026b26ad3da55777b962
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59384268"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a>웹 서비스 백 엔드를 사용하여 숫자 위로/아래로 컨트롤 만들기(VB)

by [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)

> 확인 상자에 값을 입력 하는 사용자를 대신 숫자 위로/아래로 컨트롤 (존재 하는 Windows 및 기타 운영 체제에서) 증명 하는 점점 더 많은 편리 하 게 합니다. 기본적으로 NumericUpDown 컨트롤 항상 만큼 늘어나거나 줄어들 값 1, 하지만 더 많은 유연성을 증명 하는 웹 서비스입니다.


## <a name="overview"></a>개요

확인 상자에 값을 입력 하는 사용자를 대신 숫자 위로/아래로 컨트롤 (존재 하는 Windows 및 기타 운영 체제에서) 증명 하는 점점 더 많은 편리 하 게 합니다. 기본적으로 `NumericUpDown` 컨트롤 항상 만큼 늘어나거나 줄어들 값 1, 하지만 더 많은 유연성을 증명 하는 웹 서비스입니다.

## <a name="steps"></a>단계

ASP.NET AJAX Control Toolkit에 포함 된 `NumericUpDown` 텍스트 상자에 두 개의 단추를 자동으로 추가 하는 extender: 감소에 대 한 해당 값을 높이기 위한 하나입니다. 그러나 컨트롤을 웹 서비스 호출 (또는 페이지 메서드 호출)도 지원합니다. 때마다를 위로 또는 아래로 단추를 클릭 하면 JavaScript 코드 웹 서버에 연결 하 고 있는 메서드를 실행 합니다. 메서드 서명은 다음과 같습니다.

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

`current` 인수는 텍스트 상자; 현재 값을 `tag` 특성은 속성으로 설정할 수 있는 추가 컨텍스트 데이터를 `NumericUpDown` extender (하지만 필요 하지 않습니다).

이 샘플에서는 숫자 위로/아래로 컨트롤은 2의 거듭제곱 값 허용: 1, 2, 4, 8, 16, 32, 64 및 등입니다. 따라서 사용자가 값을 늘려야 하는 경우 실행 해야 이전 값을 double; 또 다른 방법은 두 값을 나누려고 해야 합니다. 이것이 완전 한 웹 서비스:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

마지막으로 새로운 ASP.NET 페이지를 만듭니다. 해야 일반적으로 `ScriptManager` 컨트롤을 `TextBox` 컨트롤 및 `NumericUpDownExtender` 제어 합니다. 후자의 경우 웹 서비스 정보를 제공 해야 합니다.

- `ServiceDownMethod` 아래쪽의 이름을 웹 메서드 또는 메서드를 페이지
- `ServiceDownPath` 아래쪽 서비스 메서드를 사용 하 여 웹 서비스에 대 한 경로 페이지 메서드를 사용 하는 경우를 생략 합니다.
- `ServiceUpMethod` 위쪽의 이름을 웹 메서드 또는 메서드를 페이지
- `ServiceUpPath` 최신 서비스 메서드를 사용 하 여 웹 서비스에 대 한 경로 페이지 메서드를 사용 하는 경우를 생략 합니다.

페이지의 전체 태그는 다음과 같습니다.

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

페이지를 실행 하는 방법을 텍스트 상자에 값을 항상 두 배로 위쪽 단추를 클릭 하 고 아래쪽 단추를 클릭할 때 절반이 됩니다 알 수 있습니다.


[![O2의 제곱 된 있는 숫자 표시](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)

2의 제곱 된 번호만 표시 ([클릭 하 여 큰 이미지 보기](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
