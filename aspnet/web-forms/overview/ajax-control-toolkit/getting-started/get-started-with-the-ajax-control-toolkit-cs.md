---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: AJAX Control Toolkit (C#)를 사용 하 여 시작 | Microsoft Docs
author: microsoft
description: AJAX Control Toolkit를 사용 하 여 시작 하려면 알아야 할 모든에 대해 알아봅니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 7478b090ec52778572d70065983de6be8bdb4e6b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65128185"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a>AJAX 컨트롤 도구 키트 시작(C#)

by [Microsoft](https://github.com/microsoft)

> AJAX Control Toolkit를 사용 하 여 시작 하려면 알아야 할 모든에 대해 알아봅니다.

AJAX Control Toolkit에는 ASP.NET 응용 프로그램에서 사용할 수 있는 30 개 이상의 무료 컨트롤이 포함 됩니다. 이 자습서에서는 AJAX Control Toolkit을 다운로드 하 고 Visual Studio/Visual Web Developer Express 도구 상자에 도구 키트 컨트롤을 추가 하는 방법을 알아봅니다.

## <a name="downloading-the-ajax-control-toolkit"></a>AJAX Control Toolkit 다운로드

합니다 [AJAX Control Toolkit](http://devexpress.com/act) ASP.NET 커뮤니티 및 ASP.NET 팀 멤버에 의해 개발 된 오픈 소스 프로젝트입니다. 

[![AJAX Control Toolkit 다운로드](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

**그림 01**: AJAX Control Toolkit를 다운로드 ([클릭 하 여 큰 이미지 보기](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))

파일을 다운로드 한 후에 파일의 차단을 해제 해야 합니다. 파일, 속성을 선택 합니다. 마우스 오른쪽 단추로 클릭 합니다 **차단 해제** 단추 (그림 2 참조).

[![AJAX 컨트롤 도구 키트 ZIP 파일을 차단 해제](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

**그림 02**: AJAX 컨트롤 도구 키트 ZIP 파일을 차단 해제 ([클릭 하 여 큰 이미지 보기](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))

파일의 차단을 해제 한 후 파일 압축을 풀 수 있습니다. 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 합니다 **풀기** 메뉴 옵션입니다. 이제 Visual Studio/Visual Web Developer 도구 상자에 도구 키트를 추가할 준비가 되었습니다.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>AJAX Control Toolkit의 도구 상자에 추가

AJAX Control Toolkit을 사용 하는 가장 쉬운 방법은 Visual Studio/Visual Web Developer 도구 상자에 도구 키트를 추가 하는 것 (그림 3 참조). 이런 방식으로 수 단순히 끌면 도구 키트 컨트롤 페이지를 사용 하려는 경우.

[![AJAX Control Toolkit 도구 상자에 표시 됩니다.](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

**그림 03**: 도구 상자에 표시 되는 AJAX Control Toolkit ([클릭 하 여 큰 이미지 보기](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))

첫째, 도구 상자에는 AJAX Control Toolkit 탭 추가 해야 합니다. 다음이 단계를 수행 합니다.

1. 메뉴 옵션 파일을 새 웹 사이트를 선택 하 여 새 ASP.NET 웹 사이트를 만듭니다. 편집기에서 파일을 열려면 솔루션 탐색기 창에서 Default.aspx를 두 번 클릭 합니다.
2. 일반 탭 아래에 있는 도구 상자를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가 탭** (그림 4 참조).
3. AJAX Control Toolkit 이라는 새 탭을 입력 합니다.

[![새 탭 추가](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

**그림 04**: 새 탭 추가 ([클릭 하 여 큰 이미지 보기](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))

다음으로, 새 탭에는 AJAX Control Toolkit 컨트롤을 추가 해야 합니다. 아래 단계를 수행합니다.

- AJAX Control Toolkit 탭 아래에 있는 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **(그림 5 참조)는 선택 항목**합니다.
- 위치로 이동 하는 AJAX Control Toolkit 압축을 해제 하 고 AjaxControlToolkit.dll 어셈블리를 선택 합니다.

[![도구 상자에 추가할 항목 선택](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

**그림 05**: 도구 상자에 추가할 항목 선택 ([클릭 하 여 큰 이미지 보기](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))

다음이 단계를 완료 한 후 도구 상자에는 모든 도구 키트 컨트롤이 나타납니다.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>도구 키트의 새 버전으로 업그레이드

도구 키트의 이전 버전을 사용 하 고 이제 이동 해야 하는 경우 권장 되는 단계는 다음과 이상 버전.

- 이진 파일-웹 사이트 Bin 폴더에서 AjaxControlToolkit.dll 어셈블리의 이전 버전을 삭제 합니다.
- 도구 상자 항목-AJAX Control Toolkit 탭 삭제 및 다시 탭을 만드는 AjaxControlToolkit.dll 어셈블리의 새 버전을 사용 하 여 위의 단계를 수행 합니다.

> [!div class="step-by-step"]
> [다음](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
