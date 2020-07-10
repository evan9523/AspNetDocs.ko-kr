---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: '자습서: MVC 5 웹 앱에 대 한 고급 EF 시나리오 알아보기'
description: 이 자습서에는 Entity Framework Code First를 사용 하는 ASP.NET 웹 응용 프로그램을 개발 하는 기본 사항을 벗어날 때 알아 두어야 하는 몇 가지 항목이 소개 되어 있습니다.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: d7cc83a5b78a60f575f5c3065079679189296a0c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "86188737"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a>자습서: MVC 5 웹 앱에 대 한 고급 EF 시나리오 알아보기

이전 자습서에서는 계층당 하나의 테이블 상속을 구현 했습니다. 이 자습서에는 Entity Framework Code First를 사용 하는 ASP.NET 웹 응용 프로그램을 개발 하는 기본 사항을 벗어날 때 알아 두어야 하는 몇 가지 항목이 소개 되어 있습니다. 첫 번째 섹션에는 코드를 안내 하 고 Visual Studio를 사용 하 여 작업을 완료 하는 단계별 지침이 나와 있습니다. 다음 섹션에서는 간략 한 소개와 함께 몇 가지 항목을 소개 하 고 자세한 내용을 보려면 리소스에 대 한 링크를 제공 합니다.

이러한 항목의 대부분은 이미 만든 페이지를 사용 하 여 작업 합니다. 원시 SQL을 사용 하 여 대량 업데이트를 수행 하려면 데이터베이스에 있는 모든 과정의 크레딧 수를 업데이트 하는 새 페이지를 만듭니다.

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

이 자습서에서는 다음과 같은 작업을 수행합니다.

> [!div class="checklist"]
> * 원시 SQL 쿼리 수행
> * 추적 안 함 쿼리 수행
> * 데이터베이스로 전송 되는 SQL 쿼리 검사

다음에 대해서도 알아봅니다.

> [!div class="checklist"]
> * 추상화 계층 만들기
> * 프록시 클래스
> * 자동 변경 내용 검색
> * 자동 유효성 검사
> * Entity Framework 파워 도구
> * 소스 코드 Entity Framework

## <a name="prerequisite"></a>필수 조건

* [상속 구현](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a>원시 SQL 쿼리 수행

Entity Framework Code First API에는 SQL 명령을 데이터베이스에 직접 전달할 수 있는 메서드가 포함 되어 있습니다. 다음과 같은 옵션이 있습니다.

- 엔터티 형식을 반환 하는 쿼리에 대해 [Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) 메서드를 사용 합니다. 반환 된 개체는 개체에 필요한 형식 이어야 `DbSet` 하며, 추적을 해제 하지 않는 한 데이터베이스 컨텍스트에 의해 자동으로 추적 됩니다. [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) 메서드에 대 한 다음 섹션을 참조 하십시오.
- 엔터티가 아닌 형식을 반환 하는 쿼리에는 [SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) 메서드를 사용 합니다. 이 메서드를 사용하여 엔터티 형식을 검색하더라도 반환된 데이터는 데이터베이스 컨텍스트에 의해 추적되지 않습니다.
- 쿼리가 아닌 명령에 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) 를 사용 합니다.

Entity Framework를 사용할 때 장점 중 하나는 코드가 데이터를 저장하는 특정 메서드에 너무 얽매이지 않아도 된다는 점입니다. 이것은 사용자를 위한 SQL 쿼리와 명령이 생성되므로 가능하며 사용자는 코드를 직접 작성할 필요가 없습니다. 그러나 수동으로 만든 특정 SQL 쿼리를 실행 해야 하는 경우에는 예외적인 시나리오가 있습니다. 이러한 방법을 사용 하면 이러한 예외를 처리할 수 있습니다.

웹 애플리케이션에서 SQL 명령을 실행할 때 항상 그렇듯이 SQL 삽입 공격으로부터 사이트를 보호하기 위한 예방 조치를 취해야 합니다. 이를 수행하는 한 가지 방법은 매개 변수가 있는 쿼리를 사용하여 웹 페이지에서 제출한 문자열을 SQL 명령으로 해석할 수 없도록 하는 것입니다. 이 자습서에서는 사용자 입력을 쿼리에 통합할 때 매개 변수가 있는 쿼리를 사용합니다.

### <a name="calling-a-query-that-returns-entities"></a>엔터티를 반환 하는 쿼리 호출

[Dbset &lt; &gt; ](https://msdn.microsoft.com/library/gg696460.aspx) 엔터티 클래스는 형식의 엔터티를 반환 하는 쿼리를 실행 하는 데 사용할 수 있는 메서드를 제공 합니다 `TEntity` . 이 기능이 어떻게 작동 하는지 확인 하려면 `Details` 컨트롤러의 메서드에서 코드를 변경 `Department` 합니다.

*DepartmentController.cs*의 `Details` 메서드에서 `db.Departments.FindAsync` `db.Departments.SqlQuery` 다음 강조 표시 된 코드에 표시 된 것 처럼 메서드 호출을 메서드 호출로 바꿉니다.

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

새 코드가 올바르게 작동하는지 확인하려면 **부서** 탭을 선택한 후 부서 중 하나에 대해 **세부 정보**를 선택합니다. 모든 데이터가 예상 대로 표시 되는지 확인 합니다.

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>다른 형식의 개체를 반환 하는 쿼리 호출

이전에 등록 날짜별로 학생 수를 보여주는 [정보] 페이지의 학생 통계 표를 만들었습니다. *HomeController.cs* 에서이 작업을 수행 하는 코드는 LINQ를 사용 합니다.

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

LINQ를 사용 하지 않고 SQL에서 직접이 데이터를 검색 하는 코드를 작성 한다고 가정 합니다. 이렇게 하려면 엔터티 개체가 아닌 다른 항목을 반환 하는 쿼리를 실행 해야 합니다. 즉, [SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) 메서드를 사용 해야 합니다.

*HomeController.cs*에서 `About` 다음 강조 표시 된 코드에 표시 된 것 처럼 메서드의 LINQ 문을 SQL 문으로 바꿉니다.

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

정보 페이지를 실행 합니다. 이전에 수행한 것과 동일한 데이터를 표시 하는지 확인 합니다.

### <a name="calling-an-update-query"></a>업데이트 쿼리 호출

Contoso 대학 관리자가 모든 과정에 대 한 크레딧 수를 변경 하는 등 데이터베이스에서 대량 변경을 수행할 수 있다고 가정 합니다. 대학에 과목이 많은 경우 엔터티로 모두 검색하여 개별적으로 변경하는 것은 비효율적입니다. 이 섹션에서는 사용자가 모든 과정에 대 한 크레딧 수를 변경 하는 인수를 지정할 수 있는 웹 페이지를 구현 하 고 SQL 문을 실행 하 여 변경 작업을 수행 합니다 `UPDATE` . 

*CourseController.cs*에서 `UpdateCourseCredits` 및에 대 한 메서드를 추가 합니다 `HttpGet` `HttpPost` .

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

컨트롤러에서 요청을 처리할 때 `HttpGet` 변수에 아무 것도 반환 되지 `ViewBag.RowsAffected` 않고, 뷰에 빈 텍스트 상자와 제출 단추가 표시 됩니다.

**업데이트** 단추를 클릭 하면 `HttpPost` 메서드가 호출 되 고 `multiplier` 텍스트 상자에 입력 된 값이 포함 됩니다. 그런 다음 코드는 과정을 업데이트 하는 SQL을 실행 하 고 영향을 받는 행 수를 변수의 뷰에 반환 합니다 `ViewBag.RowsAffected` . 뷰가 해당 변수에서 값을 가져오는 경우 텍스트 상자 및 제출 단추 대신 업데이트 된 행 수를 표시 합니다.

*CourseController.cs*에서 메서드 중 하나를 마우스 오른쪽 단추로 클릭 한 `UpdateCourseCredits` 다음 **뷰 추가**를 클릭 합니다. **뷰 추가** 대화 상자가 나타납니다. 기본값을 그대로 두고 **추가**를 선택 합니다.

*Views\Course\UpdateCourseCredits.cshtml*에서 템플릿 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

**Courses(과정)** 탭을 선택하여 `UpdateCourseCredits` 메서드를 실행한 후 브라우저의 주소 표시줄에서 URL 끝에 "/UpdateCourseCredits"를 추가합니다(예: `http://localhost:50205/Course/UpdateCourseCredits`). 텍스트 상자에 숫자를 입력합니다.

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

**업데이트**를 클릭합니다. 영향을 받는 행 수가 표시 됩니다.

학점 수가 수정된 과정 목록을 보려면 **목록으로 돌아가기**를 클릭합니다.

원시 SQL 쿼리에 대 한 자세한 내용은 MSDN의 [원시 Sql 쿼리](https://msdn.microsoft.com/data/jj592907) 를 참조 하세요.

## <a name="no-tracking-queries"></a>비 추적 쿼리

데이터베이스 컨텍스트가 테이블 행을 검색하고 해당 내용을 나타내는 엔터티 개체를 만드는 경우 기본적으로 메모리의 엔터티가 데이터베이스의 해당 내용과 동기화 상태인지 여부의 추적을 유지합니다. 메모리의 데이터는 캐시의 역할을 하고 엔터티를 업데이트할 때 사용됩니다. 컨텍스트 인스턴스는 일반적으로 수명이 짧으며(각 요청에 대해 새 것이 만들어지고 삭제됨) 엔터티를 읽는 컨텍스트는 일반적으로 해당 엔터티가 다시 사용되기 전에 삭제되므로 이 캐싱은 웹 애플리케이션에 종종 필요하지 않습니다.

[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 메서드를 사용 하 여 메모리에서 엔터티 개체 추적을 사용 하지 않도록 설정할 수 있습니다. 이러한 작업을 수행할 수 있는 일반적인 시나리오는 다음을 포함합니다.

- 쿼리는 추적 기능을 해제 하는 대량의 데이터를 검색 하 여 성능을 현저 하 게 향상 시킬 수 있습니다.
- 엔터티를 업데이트 하기 위해 연결 하려고 하지만 이전에 다른 용도로 동일한 엔터티를 검색 했습니다. 엔터티는 데이터베이스 컨텍스트에서 이미 추적 중이므로 변경하려는 엔터티를 연결할 수 없습니다. 이러한 상황을 처리 하는 한 가지 방법은 `AsNoTracking` 이전 쿼리와 함께 옵션을 사용 하는 것입니다.

[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 메서드를 사용 하는 방법을 보여 주는 예제는 [이 자습서의 이전 버전](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)을 참조 하세요. 이 자습서 버전은 Edit 메서드에서 모델 바인더에서 만든 엔터티에 수정 된 플래그를 설정 하지 않으므로 필요 하지 않습니다 `AsNoTracking` .

## <a name="examine-sql-sent-to-database"></a>데이터베이스로 전송 되는 SQL 검사

때로는 데이터베이스로 전송된 실제 SQL 쿼리를 볼 수 있는 것이 도움이 됩니다. 이전 자습서에서는 인터셉터 코드에서이 작업을 수행 하는 방법을 살펴보았습니다. 이제 인터셉터 코드를 작성 하지 않고이 작업을 수행 하는 몇 가지 방법이 나와 있습니다. 이 작업을 수행 하려면 간단한 쿼리를 살펴본 다음 즉시 로드, 필터링, 정렬 등의 옵션을 추가할 때 발생 하는 상황을 살펴보겠습니다.

*Controller/CourseController*에서 `Index` 메서드를 다음 코드로 바꾸어 즉시 로드를 일시적으로 중지 합니다.

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

이제 문에 중단점을 설정 `return` 합니다 (해당 줄에서 커서를 사용 하 여 F9). **F5** 키를 눌러 디버그 모드에서 프로젝트를 실행 하 고 과정 인덱스 페이지를 선택 합니다. 코드가 중단점에 도달 하면 변수를 검사 `sql` 합니다. SQL Server로 전송 된 쿼리가 표시 됩니다. 간단한 `Select` 문입니다.

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

**텍스트 시각화 도우미**에서 쿼리를 보려면 돋보기를 클릭 합니다.

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

이제 사용자가 특정 부서에 대해 필터링 할 수 있도록 강좌 인덱스 페이지에 드롭다운 목록을 추가 합니다. 코스를 제목별로 정렬 하 고 탐색 속성에 대해 즉시 로드를 지정 `Department` 합니다.

*CourseController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

문에 중단점을 복원 `return` 합니다.

메서드는 매개 변수의 드롭다운 목록에서 선택한 값을 받습니다 `SelectedDepartment` . 아무 것도 선택 하지 않으면이 매개 변수는 null이 됩니다.

`SelectList`모든 부서를 포함 하는 컬렉션은 드롭다운 목록에 대 한 보기로 전달 됩니다. 생성자에 전달 된 매개 변수는 `SelectList` 값 필드 이름, 텍스트 필드 이름 및 선택 된 항목을 지정 합니다.

`Get`리포지토리의 메서드에 대해 `Course` 코드는 탐색 속성에 대 한 필터 식, 정렬 순서 및 즉시 로드를 지정 합니다 `Department` . `true`드롭다운 목록에서 선택 된 항목이 없는 경우 (즉, null 임) 필터 식은 항상를 반환 합니다 `SelectedDepartment` .

*Views\Course\Index.cshtml*에서 여는 태그 바로 앞에 `table` 다음 코드를 추가 하 여 드롭다운 목록과 제출 단추를 만듭니다.

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

중단점이 여전히 설정 된 상태에서 과정 인덱스 페이지를 실행 합니다. 코드가 중단점에 처음으로 이동 하 여 페이지가 브라우저에 표시 되도록 합니다. 드롭다운 목록에서 부서를 선택 하 고 **필터**를 클릭 합니다.

이번에는 드롭다운 목록에 대 한 부서 쿼리의 첫 번째 중단점이 표시 됩니다. 이를 건너뛰고 다음에 `query` 코드가 중단점에 도달 했을 때 해당 변수가 어떻게 표시 되는지 확인 합니다 `Course` . 다음과 같은 내용이 표시 됩니다.

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

이제 쿼리는 `JOIN` `Department` 데이터와 함께 데이터를 로드 하는 쿼리 `Course` 이며 절이 포함 되어 있음을 알 수 있습니다 `WHERE` .

줄을 제거 `var sql = courses.ToString()` 합니다.

## <a name="create-an-abstraction-layer"></a>추상화 계층 만들기

대부분의 개발자는 리포지토리 및 작업 패턴 단위를 구현하기 위한 코드를 Entity Framework에서 작동하는 코드를 둘러싼 래퍼로 작성합니다. 이러한 패턴은 애플리케이션의 데이터 액세스 계층 및 비즈니스 논리 계층 간에 추상화 계층을 만드는 데 사용됩니다. 이러한 패턴을 구현하면 데이터 저장소의 변경 내용으로부터 애플리케이션을 격리할 수 있으며 자동화된 단위 테스트 또는 TDD(테스트 중심 개발)를 용이하게 수행할 수 있습니다. 그러나 이러한 패턴을 구현 하는 추가 코드를 작성 하는 것은 여러 가지 이유로 EF를 사용 하는 응용 프로그램에는 적합 한 선택이 아닐 수 있습니다.

- EF 컨텍스트 클래스 자체에서 데이터 저장소별 코드로부터 사용자 코드를 격리합니다.
- EF 컨텍스트 클래스는 EF를 사용하여 수행하는 데이터베이스 업데이트에 대해 작업 단위 클래스로 사용될 수 있습니다.
- Entity Framework 6에서 도입 된 기능을 사용 하면 리포지토리 코드를 작성 하지 않고도 TDD를 보다 쉽게 구현할 수 있습니다.

리포지토리 및 작업 단위 패턴을 구현 하는 방법에 대 한 자세한 내용은 [이 자습서 시리즈의 Entity Framework 5 버전](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)을 참조 하세요. Entity Framework 6에서 TDD를 구현 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [EF6에서 모의 DbSets를 보다 쉽게 사용할 수 있게 하는 방법](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [모의 프레임 워크를 사용 하 여 테스트](https://msdn.microsoft.com/data/dn314429)
- [사용자 고유의 테스트를 사용 하 여 테스트 두 배](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a>프록시 클래스

Entity Framework에서 엔터티 인스턴스를 만들 때 (예: 쿼리를 실행 하는 경우) 엔터티에 대 한 프록시 역할을 하는 동적으로 생성 된 파생 형식의 인스턴스로 만듭니다. 예를 들어 다음 두 개의 디버거 이미지를 참조 하세요. 첫 번째 이미지에서는 엔터티를 인스턴스화한 직후에 `student` 변수가 예상한 형식 인지 확인 합니다 `Student` . 두 번째 이미지에서는 EF를 사용 하 여 데이터베이스에서 학생 엔터티를 읽은 후 프록시 클래스를 볼 수 있습니다.

![프록시 클래스 이전](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![프록시 클래스 후](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

이 프록시 클래스는 엔터티의 일부 가상 속성을 재정의 하 여 속성에 액세스할 때 자동으로 작업을 수행 하기 위한 후크를 삽입 합니다. 이 메커니즘을 사용 하는 하나의 함수는 지연 로드입니다.

대부분의 경우 이러한 프록시 사용을 인식 하지 않아도 되지만 다음과 같은 예외가 있습니다.

- 일부 시나리오에서는 Entity Framework에서 프록시 인스턴스를 만들지 못하게 할 수 있습니다. 예를 들어 엔터티를 serialize 하는 경우 일반적으로 프록시 클래스가 아니라 POCO 클래스를 원합니다. Serialization 문제를 방지 하는 한 가지 방법은 [Entity Framework 웹 API 사용](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) 자습서에 표시 된 것 처럼 엔터티 개체 대신 dto (데이터 전송 개체)를 serialize 하는 것입니다. 또 다른 방법은 [프록시 생성을 사용 하지 않도록 설정](https://msdn.microsoft.com/data/jj592886.aspx)하는 것입니다.
- 연산자를 사용 하 여 엔터티 클래스 `new` 를 인스턴스화하면 프록시 인스턴스를 가져올 수 없습니다. 즉, 지연 로드 및 자동 변경 내용 추적과 같은 기능을 사용할 수 없습니다. 이는 일반적으로 정상입니다. 일반적으로는 데이터베이스에 없는 새 엔터티를 만들고 엔터티를로 명시적으로 표시 하는 경우 일반적으로 변경 내용 추적이 필요 하지 않으므로 지연 로드가 필요 하지 않습니다 `Added` . 그러나 지연 로드가 필요 하 고 변경 내용 추적이 필요한 경우 클래스의 [만들기](https://msdn.microsoft.com/library/gg679504.aspx) 메서드를 사용 하 여 프록시를 사용 하 여 새 엔터티 인스턴스를 만들 수 있습니다 `DbSet` .
- 프록시 형식에서 실제 엔터티 형식을 가져올 수 있습니다. 클래스의 [Getobjecttype](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) 메서드를 사용 하 여 `ObjectContext` 프록시 형식 인스턴스의 실제 엔터티 형식을 가져올 수 있습니다.

자세한 내용은 MSDN에서 [프록시 작업](https://msdn.microsoft.com/data/JJ592886.aspx) 을 참조 하세요.

## <a name="automatic-change-detection"></a>자동 변경 내용 검색

Entity Framework는 엔터티의 현재 값을 원래 값과 비교하여 엔터티가 변경된 방법(즉, 데이터베이스에 전송해야 하는 업데이트)을 결정합니다. 원래 값은 엔터티가 쿼리 또는 연결될 때 저장됩니다. 자동 변경 내용 검색을 발생시키는 일부 메서드는 다음과 같습니다.

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

많은 수의 엔터티를 추적 하 고 루프에서 이러한 메서드 중 하나를 여러 번 호출 하는 경우 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) 속성을 사용 하 여 자동 변경 검색 기능을 일시적으로 해제 하면 성능이 크게 향상 될 수 있습니다. 자세한 내용은 MSDN의 [변경 내용 자동 검색](https://msdn.microsoft.com/data/jj556205) 을 참조 하세요.

## <a name="automatic-validation"></a>자동 유효성 검사

메서드를 호출 하는 경우 `SaveChanges` 기본적으로 Entity Framework는 데이터베이스를 업데이트 하기 전에 변경 된 모든 엔터티의 모든 속성에 있는 데이터의 유효성을 검사 합니다. 많은 수의 엔터티를 업데이트 하 고 이미 데이터의 유효성을 검사 한 경우이 작업은 필요 하지 않으며, 유효성 검사를 일시적으로 해제 하 여 변경 내용을 저장 하는 프로세스에 시간이 더 오래 걸립니다. [Validateonsaveenabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) 속성을 사용 하 여이 작업을 수행할 수 있습니다. 자세한 내용은 MSDN의 [유효성 검사](https://msdn.microsoft.com/data/gg193959) 를 참조 하세요.

## <a name="entity-framework-power-tools"></a>Entity Framework 파워 도구

[Entity Framework 파워 도구](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) 는 이러한 자습서에 표시 된 데이터 모델 다이어그램을 만드는 데 사용 된 Visual Studio 추가 기능입니다. 또한 도구는 기존 데이터베이스의 테이블을 기반으로 엔터티 클래스 생성과 같은 다른 기능을 수행 하 여 Code First에서 데이터베이스를 사용할 수 있습니다. 도구를 설치한 후에는 상황에 맞는 메뉴에 몇 가지 추가 옵션이 표시 됩니다. 예를 들어 **솔루션 탐색기**에서 컨텍스트 클래스를 마우스 오른쪽 단추로 클릭 하면 및 **Entity Framework** 옵션이 표시 됩니다. 이렇게 하면 다이어그램을 생성 하는 기능을 제공 합니다. Code First를 사용 하는 경우 다이어그램에서 데이터 모델을 변경할 수 없지만 이해 하기 쉽도록 항목을 이동할 수 있습니다.

![EF 다이어그램](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a>소스 코드 Entity Framework

Entity Framework 6의 소스 코드는 [GitHub](https://github.com/aspnet/EntityFramework6)에서 사용할 수 있습니다. 버그를 파일에 제공할 수 있으며 EF 소스 코드에 대 한 향상 된 기능을 제공할 수 있습니다.

소스 코드는 열려 있지만 Entity Framework은 Microsoft 제품으로 완전히 지원 됩니다. Microsoft Entity Framework 팀이 어떤 참가자를 수락할지 관리하고 각 릴리스의 품질을 보장하기 위해 모든 코드 변경 내용을 테스트합니다.

## <a name="acknowledgments"></a>감사의 글

- Tom Dykstra는이 자습서의 원래 버전을 작성 하 고 EF 5 업데이트를 공동 작성 하 고 EF 6 업데이트를 작성 했습니다. Tom은 Microsoft 웹 플랫폼 및 도구 콘텐츠 팀의 선임 프로그래밍 기록기입니다.
- Twitter ( [Rick Anderson](https://blogs.msdn.com/b/rickandy/) )는 [@RickAndMSFT](http://twitter.com/RickAndMSFT) EF 5 및 MVC 4의 자습서를 업데이트 하 고 ef 6 업데이트를 공동 작성 하는 대부분의 작업을 수행 했습니다. Rick는 Azure 및 MVC를 중심으로 하는 Microsoft의 선임 프로그래밍 기록기입니다.
- [행](http://www.romiller.com) 하 고 Entity Framework 팀의 다른 구성원이 코드 검토를 사용 하 고 ef 5 및 ef 6에 대 한 자습서를 업데이트 하는 동안 발생 한 마이그레이션의 많은 문제를 디버그 하는 데 도움이 되었습니다.

## <a name="troubleshoot-common-errors"></a>일반적인 오류 문제 해결

### <a name="cannot-createshadow-copy"></a>복사본을 만들거나 섀도 복사할 수 없음

오류 메시지:

> ' &lt; Filename &gt; '이 이미 있는 경우 해당 파일을 만들거나 섀도 복사할 수 없습니다.

솔루션

몇 초 정도 기다렸다가 페이지를 새로 고칩니다.

### <a name="update-database-not-recognized"></a>업데이트-데이터베이스를 인식할 수 없습니다.

오류 메시지 ( `Update-Database` PMC의 명령에서):

> ' 업데이트-데이터베이스 ' 라는 용어는 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램의 이름으로 인식 되지 않습니다. 이름의 철자를 확인하거나 경로가 포함되어 있으면 경로가 올바른지 확인하고 다시 시도합니다.

솔루션

Visual Studio를 끝냅니다. 프로젝트를 다시 열고 다시 시도 하세요.

### <a name="validation-failed"></a>유효성 검사 실패

오류 메시지 ( `Update-Database` PMC의 명령에서):

> 하나 이상의 엔터티에 대 한 유효성 검사에 실패 했습니다. 자세한 내용은 ' EntityValidationErrors ' 속성을 참조 하세요.

솔루션

이 문제의 한 가지 원인은 메서드가 실행 될 때 유효성 검사 오류입니다 `Seed` . 메서드를 디버깅 하는 방법에 대 한 팁은 [EF (시드 및 디버깅 Entity Framework) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 를 참조 하세요 `Seed` .

### <a name="http-50019-error"></a>HTTP 500.19 오류

오류 메시지:

> HTTP 오류 500.19-내부 서버 오류 페이지에 대 한 관련 구성 데이터가 잘못 되어 요청 된 페이지에 액세스할 수 없습니다.

솔루션

이 오류를 발생 시킬 수 있는 한 가지 방법은 각각 동일한 포트 번호를 사용 하 여 솔루션의 복사본을 여러 개 포함 하는 것입니다. 일반적으로 Visual Studio의 모든 인스턴스를 종료 한 다음 작업 중인 프로젝트를 다시 시작 하 여이 문제를 해결할 수 있습니다. 작동 하지 않는 경우 포트 번호를 변경해 보세요. 프로젝트 파일을 마우스 오른쪽 단추로 클릭 한 다음 속성을 클릭 합니다. **웹** 탭을 선택한 다음 **프로젝트 Url** 텍스트 상자에서 포트 번호를 변경 합니다.

### <a name="error-locating-sql-server-instance"></a>SQL Server 인스턴스 찾기 오류

오류 메시지:

> SQL Server에 연결하는 중에 네트워크 관련 오류 또는 인스턴스별 오류가 발생했습니다. 서버를 찾을 수 없거나 액세스할 수 없습니다. 인스턴스 이름이 올바르고 SQL Server가 원격 연결을 허용하도록 구성되어 있는지 확인합니다. (공급자: SQL 네트워크 인터페이스, 오류: 26 - 지정된 서버/인스턴스 찾기 오류)

솔루션

연결 문자열을 확인합니다. 데이터베이스를 수동으로 삭제 한 경우 생성 문자열에서 데이터베이스 이름을 변경 합니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 리소스

 Entity Framework를 사용 하 여 데이터로 작업 하는 방법에 대 한 자세한 내용은 [MSDN의 EF 설명서 페이지](https://msdn.microsoft.com/data/ee712907) 및 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)를 참조 하세요.

웹 응용 프로그램을 빌드한 후 배포 하는 방법에 대 한 자세한 내용은 MSDN Library에서 [ASP.NET 웹 배포-권장 리소스](../../../../whitepapers/aspnet-web-deployment-content-map.md) 를 참조 하세요.

인증 및 권한 부여와 같은 MVC와 관련 된 다른 항목에 대 한 자세한 내용은 [ASP.NET Mvc 권장 리소스](../recommended-resources-for-mvc.md)를 참조 하세요.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음과 같은 작업을 수행합니다.

> [!div class="checklist"]
> * 원시 SQL 쿼리 수행
> * 추적 안 함 쿼리 수행
> * 데이터베이스로 전송 된 SQL 쿼리를 검사 합니다.

또한 다음에 대해 알아보았습니다.

> [!div class="checklist"]
> * 추상화 계층 만들기
> * 프록시 클래스
> * 자동 변경 내용 검색
> * 자동 유효성 검사
> * Entity Framework 파워 도구
> * 소스 코드 Entity Framework

ASP.NET MVC 응용 프로그램에서 Entity Framework 사용에 대 한이 일련의 자습서를 완료 했습니다. EF Database First에 대해 알아보려면 DB First tutorial 시리즈를 참조 하세요.
> [!div class="nextstepaction"]
> [Entity Framework Database First](../database-first-development/setting-up-database.md)