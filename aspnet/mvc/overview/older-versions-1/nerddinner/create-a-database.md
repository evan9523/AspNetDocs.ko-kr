---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 데이터베이스 만들기 | Microsoft 문서
author: rick-anderson
description: 2단계는 NerdDinner 응용 프로그램에 대한 모든 저녁 식사 및 RSVP 데이터를 보유하는 데이터베이스를 만드는 단계를 보여 주며 있습니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541613"
---
# <a name="create-a-database"></a>데이터베이스 만들기

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 2단계입니다.
> 
> 2단계는 NerdDinner 응용 프로그램에 대한 모든 저녁 식사 및 RSVP 데이터를 보유하는 데이터베이스를 만드는 단계를 보여 주며 있습니다.
> 
> MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-2-creating-the-database"></a>얼간이 저녁 식사 2 단계: 데이터베이스 만들기

우리는 우리의 NerdDinner 응용 프로그램에 대한 모든 Dinner 및 RSVP 데이터를 저장하는 데이터베이스를 사용할 것입니다.

아래 단계는 무료 SQL Server Express [에디션(Microsoft 웹 플랫폼 설치 관리자의](https://www.microsoft.com/web/downloads/platform.aspx)V2를 사용하여 쉽게 설치할 수 있음)을 사용하여 데이터베이스를 만드는 것을 보여 준다. 작성할 모든 코드는 SQL Server Express 및 전체 SQL Server모두에서 작동합니다.

### <a name="creating-a-new-sql-server-express-database"></a>새 SQL Server 익스프레스 데이터베이스 만들기

먼저 웹 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **&gt;새 항목 추가** 메뉴 명령을 선택합니다.

![](create-a-database/_static/image1.png)

그러면 Visual Studio의 "새 항목 추가" 대화 상자가 나타납니다. "데이터" 범주로 필터링하고 "SQL Server 데이터베이스" 항목 템플릿을 선택합니다.

![](create-a-database/_static/image2.png)

"NerdDinner.mdf"를 만들고 자하는 SQL Server Express 데이터베이스의 이름을 지정하고 확인을 누르겠습니다. 그런 다음 Visual Studio에서 이 파일을 \App\_Data 디렉토리에 추가할지 묻습니다(이미 읽기 및 쓰기 보안 ACL이 있는 디렉토리 설정입니다).

![](create-a-database/_static/image3.png)

"예"를 클릭하고 새 데이터베이스가 만들어지고 솔루션 탐색기에 추가됩니다.

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>데이터베이스 내에서 테이블 만들기

이제 새 빈 데이터베이스가 생겼습니다. 테이블에 테이블을 추가해 보겠습니다.

이렇게 하려면 Visual Studio 내의 "서버 탐색기" 탭 창으로 이동하여 데이터베이스와 서버를 관리할 수 있습니다. 응용 프로그램의 \App\_Data 폴더에 저장된 SQL Server Express 데이터베이스는 서버 탐색기 내에 자동으로 표시됩니다. 선택적으로 "Server Explorer" 창 위에 있는 "데이터베이스에 연결" 아이콘을 사용하여 목록에 SQL Server 데이터베이스(로컬 및 원격 모두)를 추가할 수 있습니다.

![](create-a-database/_static/image5.png)

우리는 우리의 NerdDinner 데이터베이스에 두 개의 테이블을 추가합니다 - 하나는 우리의 저녁 식사를 저장하고, 다른 하나는 그들에게 RSVP 수락을 추적할 수 있습니다. 데이터베이스 내의 "테이블" 폴더를 마우스 오른쪽 단추로 클릭하고 "새 테이블 추가" 메뉴 명령을 선택하여 새 테이블을 만들 수 있습니다.

![](create-a-database/_static/image6.png)

이렇게 하면 테이블의 스키마를 구성할 수 있는 테이블 디자이너가 열립니다. "Dinners" 테이블에는 10개의 데이터 열을 추가합니다.

![](create-a-database/_static/image7.png)

"DinnerID" 열이 테이블의 고유한 기본 키가 되기를 원합니다. "DinnerID" 열을 마우스 오른쪽 단추로 클릭하고 "기본 키 설정" 메뉴 항목을 선택하여 이 항목을 구성할 수 있습니다.

![](create-a-database/_static/image8.png)

DinnerID를 기본 키로 만드는 것 외에도 새 데이터 행이 테이블에 추가될 때 값이 자동으로 증가하는 "ID" 열로 구성하려고 합니다(첫 번째 삽입된 Dinner 행에는 DinnerID가 1, 두 번째 삽입된 행에는 DinnerID가 2 등)됩니다.

"DinnerID" 열을 선택한 다음 "열 속성" 편집기를 사용하여 열의 "(Id)" 속성을 "예"로 설정하여 이 작업을 수행할 수 있습니다. 표준 ID 기본값(새 저녁 식사 행마다 1부터 1부터 1부터 증가)을 사용합니다.

![](create-a-database/_static/image9.png)

그런 다음 Ctrl-S를 입력하거나 **File-Save&gt;** 메뉴 명령을 사용하여 테이블을 저장합니다. 이렇게 하면 테이블 이름을 지정하라는 메시지가 표시됩니다. 우리는 그것을 "저녁 식사"라고 합니다.

![](create-a-database/_static/image10.png)

그러면 새 Dinners 테이블이 서버 탐색기의 데이터베이스 내에 표시됩니다.

그런 다음 위의 단계를 반복하고 "RSVP" 테이블을 만듭니다. 이 테이블에는 3개의 열이 있습니다. RsvpID 열을 기본 키로 설정하고 ID 열로 만듭니다.

![](create-a-database/_static/image11.png)

우리는 그것을 저장하고 이름을 "RSVP"를 줄 것이다.

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>테이블 간에 외래 키 관계 설정

이제 데이터베이스 내에 두 개의 테이블이 있습니다. 마지막 스키마 디자인 단계는 이 두 테이블 간에 "일대다" 관계를 설정하여 각 Dinner 행을 0개 이상의 RSVP 행과 연결할 수 있도록 하는 것입니다. RSVP 테이블의 "DinnerID" 열을 구성하여 "DinnerID" 테이블의 "DinnerID" 열과 외래 키 관계를 갖도록 합니다.

이렇게 하려면 서버 탐색기에서 두 번 클릭하여 테이블 디자이너 내에서 RSVP 테이블을 엽니다. 그런 다음 그 안에 있는 "DinnerID" 열을 선택하고 마우스 오른쪽 단추로 클릭하고 "관계..."를 선택합니다. 컨텍스트 메뉴 명령:

![](create-a-database/_static/image12.png)

이렇게 하면 테이블 간의 관계를 설정하는 데 사용할 수 있는 대화 상자가 나타납니다.

![](create-a-database/_static/image13.png)

"추가" 단추를 클릭하여 대화 상자에 새 관계를 추가합니다. 관계가 추가되면 속성 그리드 내의 "테이블 및 열 사양" 트리 뷰 노드를 대화 상자 의 오른쪽에 확장한 다음 "..."를 클릭합니다. 그것의 오른쪽에 있는 버튼:

![](create-a-database/_static/image14.png)

"..." 단추는 관계에 관련된 테이블과 열을 지정하고 관계의 이름을 지정할 수 있는 다른 대화 상자를 제공합니다.

기본 키 테이블을 "저녁 식사"로 변경하고 저녁 식사 테이블 내의 "DinnerID" 열을 기본 키로 선택합니다. 우리의 RSVP 테이블은 외래 키 테이블과 RSVP가 됩니다. DinnerID 열은 외래 키로 연결됩니다.

![](create-a-database/_static/image15.png)

이제 RSVP 테이블의 각 행이 Dinner 테이블의 행과 연결됩니다. SQL Server는 참조 무결성을 유지하고 유효한 Dinner 행을 가리키지 않으면 새 RSVP 행을 추가하지 못하게 합니다. 또한 참조하는 RSVP 행이 여전히 있는 경우 Dinner 행을 삭제하지 못하게 됩니다.

### <a name="adding-data-to-our-tables"></a>테이블에 데이터 추가

Dinners 테이블에 샘플 데이터를 추가하여 완료해 보겠습니다. 서버 탐색기 내에서 마우스 오른쪽 단추로 클릭하고 "테이블 데이터 표시" 명령을 선택하여 테이블에 데이터를 추가할 수 있습니다.

![](create-a-database/_static/image16.png)

나중에 응용 프로그램 구현을 시작할 때 사용할 수 있는 Dinner 데이터의 몇 행을 추가하겠습니다.

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>다음 단계

데이터베이스 만들기를 완료했습니다. 이제 쿼리하고 업데이트하는 데 사용할 수 있는 모델 클래스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](create-a-new-aspnet-mvc-project.md)
> [다음](build-a-model-with-business-rule-validations.md)
