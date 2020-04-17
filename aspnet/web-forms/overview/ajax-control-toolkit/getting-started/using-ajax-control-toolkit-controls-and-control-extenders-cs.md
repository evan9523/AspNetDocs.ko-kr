---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: AJAX 제어 툴킷 제어 및 제어 익스텐더 사용 (C#) | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 페이지에 AJAX 제어 툴킷 컨트롤 및 익스텐더를 추가하는 방법을 알아봅니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 5729db63f831b74ca37c573791c53c39265c1f39
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543719"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>Using AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 Extender 사용(C#)

[로 마이크로 소프트](https://github.com/microsoft)

> ASP.NET 페이지에 AJAX 제어 툴킷 컨트롤 및 익스텐더를 추가하는 방법을 알아봅니다.

AJAX 제어 툴킷에는 일련의 컨트롤 및 컨트롤 익스텐더가 포함되어 있습니다. 이 간단한 자습서에서는 컨트롤 및 컨트롤 extenders를 ASP.NET 페이지에 추가하는 방법을 배웁니다.

> [!NOTE] 
> 
> AJAX 제어 도구 키트를 설치하고 AJAX 제어 도구 키트를 시각적 스튜디오/비주얼 웹 개발자 도구 상자에 추가하는 방법에 대한 지침은 [AJAX 제어 도구 키트로 시작하기 자습서를](get-started-with-the-ajax-control-toolkit-cs.md)참조하십시오.

## <a name="using-ajax-control-toolkit-controls"></a>AJAX 제어 툴킷 컨트롤 사용

AJAX 제어 툴킷 컨트롤은 일반 ASP.NET 컨트롤처럼 작동합니다. 도구 상자에서 ASP.NET 페이지로 컨트롤을 드래그할 수 있습니다. 디자인 뷰 또는 소스 보기에서 페이지에 컨트롤을 추가할 수 있습니다.

AJAX 제어 도구 키트의 컨트롤을 사용할 때 는 한 가지 특별한 요구 사항이 있습니다. 페이지에ScriptManager 컨트롤이 포함되어야 합니다. ScriptManager 컨트롤은 AJAX 제어 도구 키트 컨트롤에 필요한 모든 자바스크립트를 포함해야 합니다.

예를 들어 AJAX 제어 도구 키트 탭에는 편집기 컨트롤이라는 컨트롤이 포함되어 있습니다. 이 컨트롤에는 풍부한 HTML 편집기가 표시됩니다. 다음 단계에 따라 페이지에 편집기 컨트롤을 추가합니다.

1. ShowEditor.aspx라는 이름의 새 ASP.NET 페이지 만들기
2. 도구 상자의 AJAX 확장 탭 아래에서 ScriptManager 컨트롤을 선택하고 컨트롤을 페이지로 드래그합니다.
3. 도구 상자의 AJAX 제어 도구 키트 탭 아래에서 편집기 컨트롤을 선택하고 컨트롤을 페이지로 드래그합니다(그림 1 참조). 디자이너는 그림 2와 같아야 합니다.
4. 메뉴 옵션 **디버그, 디버깅 시작** 또는 F5 키를 누르면 웹 사이트를 실행합니다.
5. 그림 3의 페이지가 표시됩니다.

[![HTML 편집기 컨트롤 선택](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**그림 01**: HTML 편집기 컨트롤 선택[(클릭하여 전체 크기 이미지 보기)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png)

[![스크립트 관리자 및 편집 컨트롤이 있는 비주얼 스튜디오 디자이너](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**그림 02**: 스크립트 관리자 및 편집 컨트롤이 있는 비주얼 스튜디오[디자이너(클릭하여 전체 크기 이미지 보기)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png)

[![디스플레이 에디터.aspx 페이지](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**그림 03**: DisplayEditor.aspx 페이지[(전체 크기 이미지를 보려면 클릭)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png)

## <a name="using-ajax-control-toolkit-control-extenders"></a>AJAX 제어 툴킷 제어 익스텐더 사용

AJAX 제어 툴킷에는 컨트롤 익스텐더도 포함되어 있습니다. 이름에서 알 수 있듯이 컨트롤 익스텐더는 기존 컨트롤의 기능을 확장합니다. 예를 들어 ConfirmButton 컨트롤 익스텐더는 표준 ASP.NET 버튼 컨트롤을 확장합니다. Extender는 단추를 클릭할 때 확인 대화 상자를 표시되도록 단추 컨트롤의 동작을 변경합니다.

AJAX 컨트롤 툴킷 컨트롤과 마찬가지로 컨트롤 익스텐더에는 ScriptManager 컨트롤이 필요합니다. 페이지에서 컨트롤 익스텐더를 사용하기 전에 페이지에 ScriptManager 컨트롤을 추가해야 합니다.

확인 단추 컨트롤 익스텐더를 사용 하려면 다음 단계를 수행 합니다.

1. ShowConfirmButton.aspx라는 이름의 새 ASP.NET 페이지 만들기
2. AJAX 확장 탭 아래에서 페이지로 컨트롤을 드래그하여 페이지에 ScriptManager 컨트롤을 추가합니다.
3. 도구 상자의 표준 탭 아래에서 디자이너 표면으로 단추를 드래그하여 페이지에 표준 단추 컨트롤을 추가합니다.
4. 확장 **작업 추가** 옵션을 클릭합니다(그림 4 참조).
5. 확장자 선택 대화 상자에서 확인단추 익스텐더(그림 5 참조)를 선택하고 확인 단추를 클릭합니다.
6. 디자이너에서 단추 컨트롤을 선택하고 속성 창에서\_Extender, Button1 ConfirmButtonExtender 노드를 확장합니다(그림 6 참조). 값을 *정말?* ConfirmText 속성에 할당합니다.
7. 메뉴 옵션 **디버그, 디버깅 시작 또는** F5 키를 선택하여 페이지를 실행합니다.

[![확장기 추가 작업 옵션](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**그림 04**: 확장 작업 추가 옵션[(클릭하여 전체 크기 이미지 보기)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png)

[![확인 단추 제어 익스텐더 선택](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**그림 05**: 확인 버튼 컨트롤 익스텐더 선택[(전체 크기 이미지를 보려면 클릭)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png)

[![ConfirmButton 속성 설정](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**그림 06**: ConfirmButton 속성 설정[(전체 크기 이미지를 보려면 클릭)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png)

페이지가 열리면 단추가 표시됩니다. 단추를 클릭하면 그림 7의 확인 대화 상자가 표시됩니다.

[![확인 대화 상자 표시](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**그림 07**: 확인 대화 상자 표시[(전체 크기 이미지를 보려면 클릭)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png)

일반적으로 컨트롤 익스텐더를 페이지로 드래그하지 않습니다. 대신 **Extender 추가** 작업 옵션을 사용하여 페이지에 이미 추가한 컨트롤에 extender를 추가합니다. 또한 확장되는 컨트롤에 대한 속성 시트를 열어 컨트롤 익스텐더 속성을 설정합니다.

단일 ASP.NET 컨트롤은 여러 컨트롤 익스텐더로 확장할 수 있습니다. 확장되는 컨트롤에 대한 속성 시트에는 컨트롤과 연결된 모든 컨트롤 익스텐더가 나열됩니다.

> [!div class="step-by-step"]
> [이전](get-started-with-the-ajax-control-toolkit-cs.md)
> [다음](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
