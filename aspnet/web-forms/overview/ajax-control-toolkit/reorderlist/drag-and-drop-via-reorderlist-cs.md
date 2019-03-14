---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: ReorderList (C#)를 통해 끌어서 놓기 | Microsoft Docs
author: wenz
description: ReorderList 컨트롤이 AJAX Control Toolkit에서 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다. 현재 순서 목록에는...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 15ae6ae60381f3f656f667a97dac72dbb283c80e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035030"
---
<a name="drag-and-drop-via-reorderlist-c"></a>ReorderList를 통해 끌어서 놓기(C#)
====================
by [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)

> ReorderList 컨트롤이 AJAX Control Toolkit에서 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다. 현재 순서 목록에는 서버에서 유지 됩니다.


## <a name="overview"></a>개요

`ReorderList` AJAX Control Toolkit 컨트롤 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다. 현재 순서 목록에는 서버에서 유지 됩니다.

## <a name="steps"></a>단계

`ReorderList` 컨트롤 목록에는 데이터베이스에서 바인딩 데이터를 지원 합니다. 무엇 보다도, 데이터 저장소 목록 요소 순서 변경 내용 쓰기도 지원합니다.

이 샘플에서는 데이터 저장소로 Microsoft SQL Server 2005 Express Edition을 사용 합니다. Express edition을 포함 하는 Visual Studio 설치에서 선택적 (및 사용 가능한) 부분은 데이터베이스가 있습니다. 아래에서 개별 다운로드로 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. 이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ). 서버에 연결을 두 번 클릭 `Databases` 새 데이터베이스를 만듭니다 (마우스 오른쪽 단추로 `New Database`) 이라는 `Tutorials`합니다.

이 데이터베이스에서 라는 새 테이블을 만듭니다 `AJAX` 다음 4 개의 열을 포함 합니다.

- `id` (기본 키, 정수 id를 NULL이 아님)
- `char` (char(1), NULL)
- `description` (varchar(50), NULL)
- `position` (int, NULL)


[![AJAX 테이블의 레이아웃](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

AJAX 테이블의 레이아웃 ([클릭 하 여 큰 이미지 보기](drag-and-drop-via-reorderlist-cs/_static/image3.png))


다음으로 두 가지 값을 사용 하 여 테이블을 채웁니다. `position` 열 요소는 정렬 순서를 포함 합니다.


[![AJAX 테이블의 초기 데이터](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

AJAX 테이블의 초기 데이터 ([클릭 하 여 큰 이미지 보기](drag-and-drop-via-reorderlist-cs/_static/image6.png))


생성 하는 데 필요한 다음 단계는 `SqlDataSource` 새 데이터베이스 및 해당 테이블을 사용 하 여 통신을 제어 합니다. 데이터 원본 지원 해야 합니다 `SELECT` 및 `UPDATE` SQL 명령입니다. 목록 요소의 순서를 나중에 변경 하는 경우는 `ReorderList` 컨트롤 데이터 소스에 두 값을 자동으로 전송 `Update` 명령: 새 위치와 요소의 ID입니다. 따라서 데이터 원본 요구는 `<UpdateParameters>` 이 두 값에 대 한 섹션:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

`ReorderList` 제어는 다음 특성을 설정 해야 합니다.

- `AllowReorder`: 목록 항목을 다시 정렬할 수 있습니다
- `DataSourceID`: 데이터 원본 ID
- `DataKeyField`: 데이터 원본에 기본 키 열 이름
- `SortOrderField`: 목록 항목에 대 한 정렬 순서를 제공 하는 데이터 원본 열

에 `<DragHandleTemplate>` 고 `<ItemTemplate>` 섹션 목록의 레이아웃 세밀 하 게 조정할 수 있습니다. 데이터 바인딩 가능 또한를 사용 하 여는 `Eval()` 메서드를 다음과 같이 합니다.

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

다음 CSS 스타일 정보 (에서 참조 되는 `<DragHandleTemplate>` 섹션을 `ReorderList` 컨트롤) 끌기 핸들 위로 이동할 때 마우스 포인터를 적절 하 게 변경 하 게:

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

마지막으로 `ScriptManager` 컨트롤이 페이지에 대 한 ASP.NET AJAX를 초기화 합니다.

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

브라우저에서이 예제를 실행 하 고 잠시 목록 항목을 다시 정렬 합니다. 그런 다음 페이지를 다시 로드 하거나 데이터베이스를 확인 합니다. 변경된 위치를 유지 관리 되었는지 및 값을 기준으로 반영 됩니다는 `position` 데이터베이스에 열 태그를 사용 하 여 방금 모든 코드 없이 합니다.


[![데이터가 새 목록 항목 순서에 따라 데이터베이스 변경](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

새 목록에 따라 데이터베이스 변경에서의 데이터 항목 순서 ([클릭 하 여 큰 이미지 보기](drag-and-drop-via-reorderlist-cs/_static/image9.png))

> [!div class="step-by-step"]
> [이전](using-postbacks-with-reorderlist-cs.md)
> [다음](using-postbacks-with-reorderlist-vb.md)
