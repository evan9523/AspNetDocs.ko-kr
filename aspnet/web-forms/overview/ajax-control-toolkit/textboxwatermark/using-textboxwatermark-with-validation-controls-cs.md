---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: (C#) 유효성 검사 컨트롤에 TextBoxWatermark 사용 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 TextBoxWatermark 컨트롤은 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에 사용자가 클릭 하 고 있나요...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 6ed3777e72adbb1a648a6f5215820d597a13bc92
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124497"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a>유효성 검사 컨트롤에 TextBoxWatermark 사용(C#)

by [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)

> AJAX Control Toolkit에서 TextBoxWatermark 컨트롤은 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 사용자가 상자에는 클릭, 비워집니다. 사용자는 텍스트를 입력 하지 않고 상자를 퇴사, 하는 경우에 미리 채워진된 텍스트 다시 나타납니다. 이 동일한 페이지의 ASP.NET 유효성 검사 컨트롤 충돌할 수 있지만 이러한 문제를 해결할 수 있습니다.

## <a name="overview"></a>개요

`TextBoxWatermark` AJAX Control Toolkit의 컨트롤을 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 사용자가 상자에는 클릭, 비워집니다. 사용자는 텍스트를 입력 하지 않고 상자를 퇴사, 하는 경우에 미리 채워진된 텍스트 다시 나타납니다. 이 동일한 페이지의 ASP.NET 유효성 검사 컨트롤 충돌할 수 있지만 이러한 문제를 해결할 수 있습니다.

## <a name="steps"></a>단계

샘플의 기본 설치는 다음:는 `TextBox` 제어를 사용 하 여 워터 마크 지정 되는 `TextBoxWatermarkExtender` 컨트롤입니다. 단추 포스트백을 트리거하고 나중에 트리거하는 데 사용할 페이지의 유효성 검사 컨트롤입니다. 또한는 `ScriptManager` 컨트롤은 ASP.NET AJAX를 초기화 해야 합니다.

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

이제 추가 `RequiredFieldValidator` 있는지 텍스트 필드에는 양식이 제출 되 면 확인 하는 컨트롤입니다. 합니다 `InitialValue` 유효성 검사기의 속성에 사용 되는 동일한 값으로 설정 해야 합니다는 `TextBoxWatermarkExtender` 제어 합니다. 양식이 제출 되는 경우는 변경 되지 않은 텍스트 상자의 값에 워터 마크 값이입니다.

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

하지만이 이렇게 한 문제가 있습니다. 클라이언트 JavaScript를 비활성화 하면, 텍스트 필드는 되지 않습니다 미리 채워진 워터 마크 텍스트를 따라서는 `RequiredFieldValidator` 오류 메시지를 트리거하지 않습니다. 따라서 두 번째 `RequiredFieldValidator` 컨트롤입니다. 필요한 빈 텍스트 상자에 대 한 확인 (생략 된 `InitialValue` 특성).

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

모두 유효성 검사기를 사용 하므로 `Display` = `"Dynamic"`, 최종 사용자는 두 유효성 검사기가 발생 하는 시각적 모양을에서 구분할 수 없습니다; 대신 것 같습니다. 둘 중 하나만 했습니다.

마지막으로, 없습니다 유효성 검사기 오류 메시지를 발급 하는 경우 필드의 텍스트를 출력 하도록 일부 서버 쪽 코드를 추가 합니다.

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]

[![유효성 검사기에서 필드에 텍스트가 있는지](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)

유효성 검사기에서 필드에는 텍스트가 없습니다 있습니다 ([클릭 하 여 큰 이미지 보기](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](using-textboxwatermark-in-a-formview-cs.md)
> [다음](using-textboxwatermark-in-a-formview-vb.md)
