---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 뷰를 생성'
description: 이 자습서는 컨트롤러 및 뷰를 생성 하려면 ASP.NET 스 캐 폴딩을 사용에 중점을 둡니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65121220"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 뷰를 생성

MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다. 생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.

이 자습서는 컨트롤러 및 뷰를 생성 하려면 ASP.NET 스 캐 폴딩을 사용에 중점을 둡니다.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 스 캐 폴드 추가
> * 새 보기에 대 한 링크 추가
> * 학생 뷰를 표시 합니다.
> * 등록 보기를 표시 합니다.

## <a name="prerequisite"></a>필수 조건

* [웹 응용 프로그램 및 데이터 모델 만들기](creating-the-web-application.md)

## <a name="add-scaffold"></a>스 캐 폴드 추가

모델 클래스에 대 한 표준 데이터 작업을 제공 하는 코드를 생성할 준비가 되었습니다. 스 캐 폴드 항목을 추가 하 여 코드를 추가 합니다. 다음을 추가할 수 있습니다; 스 캐 폴딩 유형에 대 한 여러 가지 이 자습서에서는 이전 섹션에서 만든 학생 및 등록 모델에 해당 하는 뷰와 컨트롤러 스 캐 폴드 포함 됩니다.

프로젝트에서 일관성을 유지 하려면 기존에 새 컨트롤러를 추가 합니다 **컨트롤러** 폴더입니다. 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 선택한 폴더 **추가** > **스 캐 폴드 된 새 항목**합니다.

선택 된 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 5 컨트롤러** 옵션입니다. 이 옵션은 컨트롤러 및 업데이트, 삭제, 만들기 및 모델의 데이터를 표시 하는 것에 대 한 뷰를 생성 됩니다.

![mvc 컨트롤러 추가](generating-views/_static/image2.png)

선택 **학생 (ContosoSite.Models)** 모델 클래스를 선택 합니다 **ContosoUniversityDataEntities (ContosoSite.Models)** 컨텍스트 클래스에 대 한 합니다. 컨트롤러 이름으로 유지할 **StudentsController**합니다.

**추가**를 클릭합니다.

오류가 발생 하는 경우 이전 섹션에서 프로젝트를 빌드하지 않은 때문에 수 있습니다. 그렇다면 프로젝트를 빌드하지 및 다음 스 캐 폴드 된 항목을 다시 추가 합니다.

새 컨트롤러와 보기를 프로젝트의 참조는 코드 생성 프로세스를 완료 한 후 **컨트롤러** 하 고 **뷰** > **학생** 폴더 .

동일한 단계를 다시 수행 하지만 대 한 스 캐 폴드를 추가 합니다 **등록** 클래스입니다. 가 완료 되 면를 **EnrollmentsController.cs** 파일 및 하위 폴더 **뷰** 이라는 **등록** 만들기, 삭제, 세부 정보, 편집 및 인덱스 보기를 사용 합니다.

## <a name="add-links-to-new-views"></a>새 보기에 대 한 링크 추가

새 보기를 탐색 하기 쉽게 학생 및 등록에 대 한 하이퍼링크의 몇 인덱스 뷰를 추가할 수 있습니다. 파일을 엽니다 **뷰** > **홈** > *Index.cshtml*는 사이트에 대 한 홈 페이지입니다. Jumbotron는 아래에 다음 코드를 추가 합니다.

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

ActionLink 메서드에 대 한 첫 번째 매개 변수 링크에 표시할 텍스트입니다. 두 번째 매개 변수는 작업 및 세 번째 매개 변수는 컨트롤러의 이름입니다. 예를 들어, 첫 번째 링크 StudentsController에서 인덱스 작업을 가리킵니다. 실제 하이퍼링크는 이러한 값에서 생성 됩니다. 궁극적으로 첫 번째 링크를 통해 사용자는 **Index.cshtml** 내에서 파일을 **뷰/학생** 폴더입니다.

## <a name="display-student-views"></a>학생 뷰를 표시 합니다.

프로젝트에 올바르게 추가 코드는 학생의 목록을 표시 하 고 편집, 생성 또는 데이터베이스의 학생 레코드를 삭제 하면을 확인 합니다.

마우스 오른쪽 단추로 클릭 합니다 **뷰** > **홈** > *Index.cshtml* 파일을 열고 선택 **브라우저에서 보기**합니다. 응용 프로그램 홈 페이지에서 선택 **학생의 목록을**합니다.

![](generating-views/_static/image6.png)

에 **인덱스** 페이지에서이 데이터를 수정 하는 학생과 링크 목록을 확인 합니다. 선택 된 **새로 만들기** 에 연결 하 고 새 학생에 대 한 일부 값을 제공 합니다. 클릭 **만들기**, 및 새 학생 목록에 추가 됩니다.

다시를 **인덱스** 페이지에서 선택 합니다 **편집** 링크를 선택한 학생에 대 한 일부 값을 변경 합니다. 클릭 **저장할**, 학생 레코드가 변경 되었는지 확인 합니다.

마지막으로 선택 합니다 **삭제** 에 연결 하 고 클릭 하 여 레코드를 삭제할 것인지 확인 합니다 **삭제** 단추입니다.

모든 코드를 작성 하지 않고도 Student 테이블에서 데이터에 대 한 일반적인 작업을 수행 하는 뷰를 추가 했습니다.

알 수 있습니다는 필드의 텍스트 레이블을 속성을 기반으로 데이터베이스 (같은 **LastName**) 없는 반드시 웹 페이지에 표시 하려는 합니다. 예를 들어 되도록 레이블 수도 **Last Name**합니다. 이 자습서의 뒷부분에 나오는이 디스플레이 문제를 해결 됩니다.

## <a name="display-enrollment-views"></a>등록 보기를 표시 합니다.

데이터베이스에는 학생 및 등록 테이블 사이의 강좌 및 등록 테이블 사이 일 대 다 관계에 일 대 다 관계를 포함합니다. 등록에 대 한 뷰는 이러한 관계를 올바르게 처리. 선택한 서버 사이트에 대 한 홈 페이지로 이동 합니다 **등록 목록** 링크 차례로 합니다 **새로 만들기** 링크.

보기에는 새 등록 레코드를 만드는 양식이 표시 됩니다. 특히, 폼에 포함 되어 있음을 알 수 있습니다는 **CourseID** 드롭 다운 목록 및 **StudentID** 드롭 다운 목록. 두 관련된 테이블의 값으로 채워집니다.

또한 필드의 데이터 형식에 제공된 된 값의 유효성 검사는 따라 적용 자동으로 됩니다. **등급** 호환 되지 않는 값을 제공 하려고 하면 오류 메시지가 표시 됩니다 있도록 숫자로 필요 합니다. *엔터프라이즈급 필드는 숫자 여야 합니다.*

자동으로 생성 된 뷰를 사용 하는 사용자가 데이터베이스의 데이터로 작업할 수 있도록 확인 했습니다. 이 시리즈의 다음 자습서에서는 데이터베이스를 업데이트 하 고 웹 응용 프로그램에서 해당 변경 됩니다 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 추가 스 캐 폴드
> * 새 보기에 대 한 추가 링크
> * 표시 된 학생 뷰
> * 표시 된 등록 보기

데이터베이스를 변경 하는 방법을 알아보려면 다음 자습서로 이동 합니다.
> [!div class="nextstepaction"]
> [데이터베이스 변경](changing-the-database.md)