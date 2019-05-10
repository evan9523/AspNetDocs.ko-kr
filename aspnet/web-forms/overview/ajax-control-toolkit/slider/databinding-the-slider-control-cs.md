---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
title: 데이터 바인딩 슬라이더 컨트롤 (C#) | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 슬라이더 컨트롤에 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 현재 positio 바인딩하는 것이 불가능 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7f77869-aa1d-4025-924f-622c57112db6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 9613b96612c2799c17bd5633083bb439913b4dc9
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124857"
---
# <a name="databinding-the-slider-control-c"></a>슬라이더 컨트롤 데이터 바인딩(C#)

by [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)

> AJAX Control Toolkit의 슬라이더 컨트롤에 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 다른 ASP.NET 컨트롤에 슬라이더의 현재 위치를 바인딩하는 것이 가능 합니다.

## <a name="overview"></a>개요

AJAX Control Toolkit의 슬라이더 컨트롤에 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 다른 ASP.NET 컨트롤에 슬라이더의 현재 위치를 바인딩하는 것이 가능 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample1.aspx)]

다음으로 두 개의 추가 `TextBox` 페이지로 컨트롤입니다. 하나는 그래픽 슬라이더도 변환 됩니다 및 다른 슬라이더의 위치에 저장 됩니다.

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample2.aspx)]

다음 단계는 이미 마지막 단계가입니다. `SliderExtender` ASP.NET AJAX Control Toolkit에서 첫 번째 텍스트 상자에서 슬라이더를 사용 하면 컨트롤과 슬라이더 위치를 변경 하는 경우 두 번째 텍스트 상자를 자동으로 업데이트 합니다. 작업을 위해서는 순서로 합니다 `SliderExtender`의 `TargetControlID` 첫 번째 텍스트 상자의 id 특성을 설정 해야 합니다는 `BoundControlID` 특성의 두 번째 텍스트 상자 ID로 설정 해야 합니다.

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample3.aspx)]

양방향에서 데이터 바인딩이 작동 브라우저에서 보듯이: 슬라이더의 위치를 업데이트 하 고 텍스트 상자에 새 값을 입력 합니다. 읽기 전용 두 번째 텍스트 상자를 설정 하면 여기에 값을 수동으로 업데이트 하려면 사용자에 대 한 어렵습니다 있도록 텍스트 필드에 약한 보호를 추가할 수 있습니다.

[![슬라이더 및 텍스트 상자에 동기화 됩니다.](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)

슬라이더 및 텍스트 상자에 동기화 됩니다 ([클릭 하 여 큰 이미지 보기](databinding-the-slider-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](using-the-slider-control-with-auto-postback-cs.md)
> [다음](using-the-slider-control-with-auto-postback-vb.md)
