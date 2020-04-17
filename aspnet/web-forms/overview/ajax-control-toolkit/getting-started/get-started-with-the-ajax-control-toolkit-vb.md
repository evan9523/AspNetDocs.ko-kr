---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: AJAX 제어 툴킷(VB) | 마이크로 소프트 문서
author: rick-anderson
description: AJAX 제어 툴킷을 사용하기 위해 알아야 할 모든 것을 알아보십시오.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: 6af5e293a35ce3e3ba35a0f7abfd2d92d538c84c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543563"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>AJAX 컨트롤 도구 키트 시작(VB)

[로 마이크로 소프트](https://github.com/microsoft)

> AJAX 제어 툴킷을 사용하기 위해 알아야 할 모든 것을 알아보십시오.

AJAX 제어 툴킷에는 ASP.NET 응용 프로그램에서 사용할 수 있는 30개 이상의 무료 컨트롤이 포함되어 있습니다. 이 자습서에서는 AJAX 제어 도구 키트를 다운로드하고 도구 키트 컨트롤을 Visual Studio/Visual 웹 개발자 익스프레스 도구 상자에 추가하는 방법을 알아봅니다.

## <a name="downloading-the-ajax-control-toolkit"></a>AJAX 제어 툴킷 다운로드

[AJAX 제어 툴킷은](http://devexpress.com/act) ASP.NET 커뮤니티의 구성원과 ASP.NET 팀에 의해 개발 된 오픈 소스 프로젝트입니다.

[![AJAX 제어 툴킷 다운로드](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**그림 01**: AJAX 제어 도구 키트 다운로드[(클릭하여 전체 크기 이미지 보기)](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png)

파일을 다운로드한 후 파일 차단을 해제해야 합니다. 파일을 마우스 오른쪽 단추로 클릭하고 속성을 선택하고 **차단 해제** 단추를 클릭합니다(그림 2 참조).

[![AJAX 제어 툴킷 ZIP 파일 차단 해제](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**그림 02**: AJAX 제어 도구 키트 ZIP 파일 차단 해제[(클릭하여 전체 크기 이미지 보기)](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png)

파일 차단을 해제한 후 파일의 압축을 풀 수 있습니다: 파일 마우스 오른쪽 단추를 클릭하고 **모든 메뉴 추출** 옵션을 선택합니다. 이제 도구 키트를 Visual Studio/Visual 웹 개발자 도구 상자에 추가할 준비가 되었습니다.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>도구 상자에 AJAX 제어 도구 키트 추가

AJAX 제어 도구 키트를 사용하는 가장 쉬운 방법은 도구 키트를 Visual Studio/Visual 웹 개발자 도구 상자에 추가하는 것입니다(그림 3 참조). 이렇게 하면 도구 키트 컨트롤을 사용할 때 페이지로 드래그하기만 하면 됩니다.

[![도구 상자에 AJAX 제어 도구 키트가 나타납니다.](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**그림 03**: AJAX 제어 도구 키트가 도구 상자에 나타납니다[(전체 크기 이미지를 보려면 클릭하십시오)](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)

먼저 도구 상자에 AJAX 제어 도구 키트 탭을 추가해야 합니다. 다음 단계를 수행합니다.

1. 메뉴 옵션 파일을 선택하여 웹 사이트를 ASP.NET 새 웹 사이트를 만듭니다. 솔루션 탐색기 창에서 Default.aspx를 두 번 클릭하여 편집기에서 파일을 엽니다.
2. 일반 탭 아래에 있는 도구 상자를 마우스 오른쪽 단추로 클릭하고 **탭 추가** 옵션(그림 4 참조)을 선택합니다.
3. AJAX 제어 도구 키트라는 새 탭을 입력합니다.

[![새 탭 추가](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**그림 04**: 새 탭 추가[(클릭하여 전체 크기 이미지 보기)](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png)

다음으로 AJAX 제어 도구 키트 컨트롤을 새 탭에 추가해야 합니다.

- AJAX 제어 도구 키트 탭 아래를 마우스 오른쪽 단추로 클릭하고 메뉴 선택 **옵션(그림 5 참조)을**선택합니다.
- AJAX 제어 툴킷의 압축을 풀었던 위치를 찾아보고 AjaxControlToolkit.dll 어셈블리를 선택합니다.

[![도구 상자에 추가할 항목을 선택합니다.](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**그림 05**: 도구 상자에 추가할 항목을 선택합니다(전체[크기 이미지를 보려면 클릭)](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png)

이 단계를 완료하면 모든 도구 키트 컨트롤이 도구 상자에 표시됩니다.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>새 버전의 툴킷으로 업그레이드

도구 키트의 이전 릴리스를 사용 하 고 지금 이후 버전으로 이동 해야 하는 경우 여기 권장된 단계는 다음과 같습니다.

- 바이너리 - 웹 사이트 빈 폴더에서 AjaxControlToolkit.dll 어셈블리의 이전 버전을 삭제합니다.
- 도구 상자 항목 - AJAX 제어 도구 키트 탭을 삭제하고 위의 단계를 수행하여 AjaxControlToolkit.dll 어셈블리의 새 버전으로 탭을 다시 만듭니다.

> [!div class="step-by-step"]
> [이전](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [다음](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
