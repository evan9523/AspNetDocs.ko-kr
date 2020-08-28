---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: 'AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 Extender 사용 (c #) | Microsoft Docs'
author: rick-anderson
description: ASP.NET 페이지에 AJAX 컨트롤 도구 키트 컨트롤과 extender를 추가 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 48c8479fce6d121b8a4f03d972ac4117ed974958
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044508"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>Using AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 Extender 사용(C#)

[Microsoft](https://github.com/microsoft) 에서

> ASP.NET 페이지에 AJAX 컨트롤 도구 키트 컨트롤과 extender를 추가 하는 방법에 대해 알아봅니다.

AJAX 컨트롤 도구 키트에는 컨트롤 및 컨트롤 extender 집합이 포함 되어 있습니다. 이 간략 한 자습서에서는 ASP.NET 페이지에 컨트롤과 컨트롤 extender를 추가 하는 방법에 대해 알아봅니다.

> [!NOTE] 
> 
> Ajax 컨트롤 도구 키트를 설치 하 고 Visual Studio/Visual Web Developer 도구 상자에 AJAX 컨트롤 도구 키트를 추가 하는 방법에 대 한 지침은 [Ajax 컨트롤 도구 키트 시작](get-started-with-the-ajax-control-toolkit-cs.md)자습서를 참조 하세요.

## <a name="using-ajax-control-toolkit-controls"></a>AJAX 컨트롤 도구 키트 컨트롤 사용

AJAX 컨트롤 도구 키트 컨트롤은 일반적인 ASP.NET 컨트롤과 마찬가지로 작동 합니다. 도구 상자에서 컨트롤을 ASP.NET 페이지로 끌 수 있습니다. 디자인 뷰 또는 소스 뷰에서 페이지에 컨트롤을 추가할 수 있습니다.

AJAX 컨트롤 도구 키트의 컨트롤을 사용 하는 경우 특별 한 요구 사항이 있습니다. 페이지는 ScriptManager 컨트롤을 포함 해야 합니다. ScriptManager 컨트롤은 AJAX 컨트롤 도구 키트 컨트롤에 필요한 모든 JavaScript를 포함 하는 일을 담당 합니다.

예를 들어 AJAX 컨트롤 도구 키트 탭은 편집기 컨트롤 이라는 컨트롤을 포함 합니다. 이 컨트롤은 리치 HTML 편집기를 표시 합니다. 페이지에 편집기 컨트롤을 추가 하려면 다음 단계를 따르세요.

1. ShowEditor 라는 새 ASP.NET 페이지를 만듭니다.
2. 도구 상자의 AJAX 확장 탭 아래에서 ScriptManager 컨트롤을 선택 하 고 컨트롤을 페이지로 끌어옵니다.
3. 도구 상자의 AJAX 컨트롤 도구 키트 탭 아래에서 편집기 컨트롤을 선택 하 고 컨트롤을 페이지로 끌어옵니다 (그림 1 참조). 디자이너는 그림 2와 같습니다.
4. **디버그, 디버깅 시작** 또는 F5 키로 메뉴 옵션을 선택 하 여 웹 사이트를 실행 합니다.
5. 그림 3에 페이지가 표시 되어야 합니다.

[![HTML 편집기 컨트롤 선택](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**그림 01**: HTML 편집기 컨트롤 선택 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))

[![ScriptManager 및 Edit 컨트롤이 포함 된 Visual Studio 디자이너](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**그림 02**: ScriptManager 및 Edit 컨트롤이 있는 Visual Studio 디자이너 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))

[![DisplayEditor .aspx 페이지](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**그림 03**: displayeditor .aspx 페이지 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>AJAX 컨트롤 도구 키트 컨트롤 Extender 사용

AJAX 컨트롤 도구 키트에는 컨트롤 extender도 포함 되어 있습니다. 이름에서 알 때 컨트롤 extender는 기존 컨트롤의 기능을 확장 합니다. 예를 들어, ASP.NET button 컨트롤 extender는 표준 Button 컨트롤을 확장 합니다. Extender는 단추 컨트롤의 동작을 변경 하 여 단추를 클릭 하면 확인 대화 상자가 표시 됩니다.

AJAX 컨트롤 도구 키트 컨트롤과 마찬가지로 컨트롤 extender에는 ScriptManager 컨트롤이 필요 합니다. 페이지에서 컨트롤 extender 사용을 시작 하기 전에 페이지에 ScriptManager 컨트롤을 추가 해야 합니다.

다음 단계를 수행 하 여 추가 단추 컨트롤 extender를 사용 합니다.

1. ShowASP.NET 라는 새 페이지를 만듭니다.
2. AJAX 확장 탭 아래에서 페이지로 컨트롤을 끌어서 ScriptManager 컨트롤을 페이지에 추가 합니다.
3. 도구 상자의 표준 탭 아래에서 단추를 디자이너 화면으로 끌어서 표준 단추 컨트롤을 페이지에 추가 합니다.
4. 확장 작업 **추가** 옵션을 클릭 합니다 (그림 4 참조).
5. Extender 선택 대화 상자에서를 선택 하 고 (그림 5 참조) 확인 단추를 클릭 합니다.
6. 디자이너에서 Button 컨트롤을 선택 하 고 속성 창에서 Extender, Button1을 \_ buttonbuttonextender 노드를 확장 합니다 (그림 6 참조). *' 정말로? '* 값을 할당 합니다. 를 텍스트 속성으로 변환할 수 있습니다.
7. **디버그, 디버깅 시작** 메뉴 옵션을 선택 하거나 F5 키를 눌러 페이지를 실행 합니다.

[![Extender 추가 작업 옵션](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**그림 04**: Extender 추가 작업 옵션 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))

[![[컨트롤] 확장](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**그림 05**: 확장[이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png)합니다.

[![로 설정 단추 속성 설정](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**그림 06**: 단일 기능 단추 속성 설정 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))

페이지가 열리면 단추가 표시 됩니다. 단추를 클릭 하면 그림 7에 확인 대화 상자가 표시 됩니다.

[![확인 대화 상자 표시](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**그림 07**: 확인 대화 상자 표시 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))

일반적으로 컨트롤 extender를 페이지로 끌어 오지 않습니다. 대신, 페이지에 이미 추가 된 컨트롤에 extender를 추가 하려면 **extender 작업 추가** 옵션을 사용 합니다. 또한 확장 중인 컨트롤의 속성 시트를 열어 컨트롤 extender 속성을 설정 하는 것을 볼 수 있습니다.

단일 ASP.NET 컨트롤은 여러 컨트롤 extender로 확장할 수 있습니다. 확장 되는 컨트롤의 속성 시트에는 컨트롤과 연결 된 모든 컨트롤 extender가 나열 됩니다.

> [!div class="step-by-step"]
> [이전](get-started-with-the-ajax-control-toolkit-cs.md)
> [다음](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
