---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: 정렬, 필터링 및 ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 페이징 추가 | Microsoft Docs'
author: tdykstra
description: 이 자습서에서는 추가 정렬, 필터링 및 페이징 기능을 합니다 **학생** 인덱스 페이지입니다. 단순 그룹화 페이지를 만들 수도 있습니다.
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: b7b5d3d3931f752f2effc044ca8cc52eab22da0a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056420"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a>자습서: 정렬, 필터링 및 ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 페이징 추가

에 [이전 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)에 대 한 기본적인 CRUD 작업에 대 한 웹 페이지 집합을 구현 `Student` 엔터티. 이 자습서에서는 추가 정렬, 필터링 및 페이징 기능을 합니다 **학생** 인덱스 페이지입니다. 단순 그룹화 페이지를 만들 수도 있습니다.

다음 이미지는 페이지 모양을 완료 되 면 표시 합니다. 열 제목은 해당 열로 정렬하기 위해 사용자가 클릭할 수 있는 링크입니다. 열 제목을 반복해서 클릭하면 오름차순 및 내림차순으로 정렬 순서가 토글됩니다.

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 열 정렬 링크 추가
> * 검색 상자 추가
> * 페이징 추가
> * 정보 페이지 만들기

## <a name="prerequisites"></a>전제 조건

* [기본 CRUD 기능 구현](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a>열 정렬 링크 추가

학생 인덱스 페이지에 정렬를 추가 하려면 변경 합니다 `Index` 메서드의 `Student` 컨트롤러 코드를 추가 하는 `Student` 인덱스 뷰.

### <a name="add-sorting-functionality-to-the-index-method"></a>Index 메서드에 정렬 기능 추가

- *Controllers\StudentController.cs*을 대체 합니다 `Index` 메서드를 다음 코드로:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

이 코드는 URL의 쿼리 문자열에서 `sortOrder` 매개 변수를 받습니다. 쿼리 문자열 값은 작업 메서드에 매개 변수로 ASP.NET MVC에서 제공 됩니다. 필요에 따라 뒤에 밑줄과 내림차순을 지정 하려면 "desc" 문자열은 "Name" 또는 "Date" 하는 문자열입니다. 기본 정렬 순서는 오름차순입니다.

인덱스 페이지를 처음 요청하면 쿼리 문자열은 없습니다. 오름차순으로 학생 들에 게 표시 됩니다 `LastName`를 기본값인에서 제어 이동 사례에서 설정한는 `switch` 문입니다. 사용자가 열 제목 하이퍼링크를 클릭하면 쿼리 문자열에 해당 `sortOrder` 값이 제공됩니다.

두 `ViewBag` 변수 뷰 열 제목 하이퍼링크를 적절 한 쿼리 문자열 값을 사용 하 여 구성할 수 있도록 사용 됩니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

이것은 3개로 구성된 문입니다. 첫 번째 경우를 지정 합니다 `sortOrder` 매개 변수는 null 이거나 비어 있는 경우 `ViewBag.NameSortParm` 로 설정 해야 "이름\_desc" 고, 그렇지 않으면 빈 문자열로 설정 해야 합니다. 이러한 두 명령문을 사용하면 뷰에서 다음과 같이 열 제목 하이퍼링크를 설정할 수 있습니다.

| 현재 정렬 순서 | 성 하이퍼링크 | 날짜 하이퍼링크 |
| --- | --- | --- |
| 성 오름차순 | descending | ascending |
| 성 내림차순 | ascending | ascending |
| 날짜 오름차순 | ascending | descending |
| 날짜 내림차순 | ascending | ascending |

메서드를 사용 하 여 [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) 기준으로 정렬 하려면 열을 지정 합니다. 코드를 만듭니다는 <xref:System.Linq.IQueryable%601> 하기 전에 변수를 `switch` 문을 수정에 `switch` 문 및 호출 합니다 `ToList` 메서드를 `switch` 문을. `IQueryable` 변수를 작성하고 수정하면 데이터베이스에 쿼리가 보내지지 않습니다. 변환할 때까지 쿼리가 실행 되지 않습니다 합니다 `IQueryable` 와 같은 메서드를 호출 하 여 컬렉션 개체로 `ToList`합니다. 따라서이 코드 발생 될 때까지 실행 되지 않습니다 하는 단일 쿼리는 `return View` 문입니다.

각 정렬 순서에 대 한 다른 LINQ 문을 작성 하는 대신, LINQ 명령문을 동적으로 만들 수 있습니다. 동적 LINQ에 대 한 정보를 참조 하세요 [동적 LINQ](https://go.microsoft.com/fwlink/?LinkID=323957)합니다.

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>학생 인덱스 뷰에 열 제목 하이퍼링크 추가

1. *Views\Student\Index.cshtml*을 대체 합니다 `<tr>` 및 `<th>` 강조 표시 된 코드를 사용 하 여 머리글 행에 대 한 요소:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   이 코드에 정보를 사용 합니다 `ViewBag` 적절 한 쿼리를 사용 하 여 하이퍼링크를 설정 하는 속성 문자열 값입니다.

2. 페이지를 실행 하 고 클릭 합니다 **성을** 및 **등록 날짜** 정렬 되는지 확인 하려면 열 머리글 작동 합니다.

   클릭 한 후 합니다 **Last Name** 제목 학생 내림차순 마지막 이름 순서로 표시 됩니다.

## <a name="add-a-search-box"></a>검색 상자 추가

학생 인덱스 페이지에 필터링을 추가 하려면 뷰에 텍스트 상자와 제출 단추를 추가 및 해당 변경 됩니다는 `Index` 메서드. 텍스트 상자에는 첫 번째 이름과 마지막 이름 필드에서 검색할 문자열을 입력할 수 있습니다.

### <a name="add-filtering-functionality-to-the-index-method"></a>인덱스 메서드에 필터링 기능 추가

- *Controllers\StudentController.cs*을 대체 합니다 `Index` 메서드를 다음 코드로 (변경 내용을 강조 표시):

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

코드를 추가 하는 `searchString` 매개 변수를는 `Index` 메서드. 검색 문자열 값은 Index 뷰에 추가할 텍스트 상자에서 가져옵니다. 또한 추가 `where` 이름 또는 성을 검색 문자열이 포함 된 학생만 선택 하는 LINQ 문 절. 추가 하는 문에 <xref:System.Linq.Queryable.Where%2A> 절에 대 한 검색 값이 있는 경우에 실행 합니다.

> [!NOTE]
> 대부분의 메모리 내 컬렉션에 확장 메서드 또는 Entity Framework 엔터티 집합에 대해 동일한 메서드를 호출할 수 있습니다. 결과 일반적으로 동일 하지만 경우에 따라 다를 수 있습니다.
>
> 예를 들어,.NET Framework 구현의 `Contains` 메서드, 빈 문자열을 전달 하지만 SQL Server Compact 4.0에 대 한 Entity Framework 공급자를 빈 문자열에 대 한 0 개 행을 반환 하는 경우 모든 행을 반환 합니다. 따라서 예제에서 코드 (배치 합니다 `Where` 내에서 문을 `if` 문)는 모든 버전의 SQL Server에 대 한 동일한 결과 얻을 수 있는지. 또한.NET Framework 구현의 `Contains` 메서드는 기본적으로 대/소문자 구분 비교를 수행 하지만 Entity Framework SQL Server 공급자는 기본적으로 대/소문자 구분 비교를 수행 합니다. 따라서 호출을 `ToUpper` 테스트를 명시적으로 대/소문자 확인 메서드를 사용 하면 결과가 반환 하는 저장소를 사용 하 여 나중에 코드를 변경할 때 변경 되지 않습니다는 `IEnumerable` 컬렉션 대신는 `IQueryable` 개체. (`IEnumerable` 컬렉션에서 `Contains` 메서드를 호출하면 .NET Framework 구현을 가져오고 `IQueryable` 개체에서 호출하면 데이터베이스 공급자 구현을 가져옵니다.)
>
> Null 처리가 사용 하거나 다른 데이터베이스 공급자에 대 한 다른 수도 있습니다는 `IQueryable` 사용 하는 경우 개체 비교를 `IEnumerable` 컬렉션입니다. 예를 들어, 일부 시나리오에서는 `Where` 와 같은 조건 `table.Column != 0` 이 있는 열을 반환 하지 않을 수 `null` 값으로. 자세한 내용은 [잘못 된 'where' 절에 변수를 null 처리](https://data.uservoice.com/forums/72025-entity-framework-feature-suggestions/suggestions/1015361-incorrect-handling-of-null-variables-in-where-cl)합니다.

### <a name="add-a-search-box-to-the-student-index-view"></a>학생 인덱스 뷰에 검색 상자 추가

1. *Views\Student\Index.cshtml*를 열기 전에 즉시 강조 표시 된 코드를 추가 `table` 캡션, 텍스트 상자를 만들기 위해 태그와 **검색** 단추입니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. 페이지를 실행 하 고, 검색 문자열을 입력, 클릭 **검색** 필터링이 작동 하는지 확인 합니다.

   알림 URL "an" 검색 문자열, 즉,이 페이지에 책갈피 받지 않는 필터링된 된 목록 책갈피를 사용 하는 경우를 포함 하지 않습니다. 이 적용 됩니다도 열 정렬 링크에는 전체 목록이 정렬 됩니다. 변경 된 **검색** 자습서의 뒷부분에 나오는 필터 조건에 대 한 쿼리 문자열을 사용 하는 단추입니다.

## <a name="add-paging"></a>페이징 추가

학생 인덱스 페이지에 페이징을 추가 하려면 먼저 설치 합니다 **PagedList.Mvc** NuGet 패키지. 다음의 추가 변경 합니다 `Index` 메서드 페이징 링크를 추가 하 고는 `Index` 보기. **PagedList.Mvc** 많은 좋은 페이징 및 ASP.NET MVC에 대 한 패키지를 정렬 중 하나 이며 여기서 사용 예를 들어, 다른 옵션과 비교에 대 한 권장 사항 아니라로 제공 됩니다.

### <a name="install-the-pagedlistmvc-nuget-package"></a>PagedList.MVC NuGet 패키지를 설치 합니다.

NuGet **PagedList.Mvc** 패키지를 자동으로 설치 합니다 **PagedList** 패키지를 종속성으로 합니다. 합니다 **PagedList** 설치 패키지를 `PagedList` 에 대 한 컬렉션 형식 및 확장명 메서드 `IQueryable` 및 `IEnumerable` 컬렉션입니다. 확장 메서드는 데이터의 단일 페이지 만들기를 `PagedList` 의 컬렉션에 `IQueryable` 또는 `IEnumerable`, 및 `PagedList` 컬렉션 여러 속성 및 페이징에 도움이 되는 메서드를 제공 합니다. 합니다 **PagedList.Mvc** 패키지 페이징 단추를 표시 하는 페이징 도우미를 설치 합니다.

1. **도구** 메뉴에서 **NuGet 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.

2. 에 **패키지 관리자 콘솔** 창 있는지 확인 합니다 **패키지 원본** 는 **nuget.org** 및 **기본 프로젝트** 는**ContosoUniversity**, 다음 명령을 입력 합니다.

   ```text
   Install-Package PagedList.Mvc
   ```

3. 프로젝트를 빌드합니다.

### <a name="add-paging-functionality-to-the-index-method"></a>인덱스 메서드에 페이징 기능 추가

1. *Controllers\StudentController.cs*, 추가 `using` 문을 여 `PagedList` 네임 스페이스:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. `Index` 메서드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   이 코드는 추가 `page` 매개 변수, 현재 정렬 순서 매개 변수, 및 메서드 서명에 현재 필터 매개 변수:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   처음으로 페이지 표시 되거나, 사용자를 페이징 또는 정렬 링크를 누르면 하지 않은 경우 모든 매개 변수가 null입니다. 페이징 링크를 클릭 하는 경우는 `page` 변수에 표시할 페이지 번호를 포함 합니다.

   `ViewBag` 페이징 하는 동안 동일한 정렬 순서를 유지 하기 위해 페이징 링크에 포함 되어야 하므로 속성은 현재 정렬 순서를 사용 하 여 보기를 제공 합니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   다른 속성인 `ViewBag.CurrentFilter`, 현재 필터 문자열을 사용 하 여 뷰를 제공 합니다. 이 값은 페이징 중 필터 설정을 유지하기 위해 페이징 링크에 포함되어야 하며 페이지를 다시 표시할 때 텍스트 상자에 복원되어야 합니다. 페이징 중에 검색 문자열이 변경되면 새 필터로 인해 다른 데이터가 표시될 수 있으므로 페이지는 1로 재설정되어야 합니다. 검색 문자열은 텍스트 상자에 값을 입력 하 고 전송 단추를 누를 때 변경 됩니다. 이런 경우는 `searchString` 매개 변수가 null이 아닙니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   메서드의 끝에는 `ToPagedList` 확장 메서드를 학생 들에 게 `IQueryable` 개체는 학생 쿼리를 페이징을 지 원하는 컬렉션 형식의 학생의 단일 페이지를 변환 합니다. 해당 단일 학생 페이지가 뷰에 전달 됩니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   `ToPagedList` 메서드는 페이지 번호를 사용합니다. 두 개의 물음표는 나타내는 합니다 [null 병합 연산자로](/dotnet/csharp/language-reference/operators/null-coalescing-operator)합니다. Null 병합 연산자는 nullable 형식의 기본값을 정의합니다. `(page ?? 1)` 식은 값이 있는 경우 `page` 값을 반환하고 `page`가 Null이면 1일 반환합니다.

### <a name="add-paging-links-to-the-student-index-view"></a>학생 인덱스 뷰에 페이징 링크 추가

1. *Views\Student\Index.cshtml*, 기존 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   페이지 맨 위에 `@model` 문은 뷰가 `List` 개체 대신 `PagedList` 개체를 가져오는 것을 지정합니다.

   합니다 `using` 방침 `PagedList.Mvc` MVC 도우미 페이징 단추에 대 한 액세스를 제공 합니다.

   오버 로드를 사용 하는 코드 [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) 지정할 수 있도록 하는 [FormMethod.Get](/previous-versions/aspnet/dd460179(v=vs.100))합니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   기본값 [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) 즉, 매개 변수가 URL에 없는 HTTP 메시지 본문에 쿼리 문자열로 전달 하는 POST로 양식 데이터를 전송 합니다. HTTP GET을 지정하면 폼 데이터가 URL에 쿼리 문자열로 전달되고 이를 통해 사용자는 URL을 책갈피로 지정할 수 있습니다. 합니다 [HTTP GET 사용에 대 한 W3C 지침](http://www.w3.org/2001/tag/doc/whenToUseGet.html) 업데이트 작업이 발생 하지 않습니다 하는 경우에 GET을 사용 해야 하는 것이 좋습니다.

   입력란은 새 페이지를 클릭 하면 현재 검색 문자열을 볼 수 있습니다는 현재 검색 문자열을 사용 하 여 초기화 됩니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   열 머리글 링크는 쿼리 문자열을 사용하여 현재 검색 문자열을 컨트롤러에 전달하므로 사용자가 필터 결과 내에서 정렬할 수 있습니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   현재 페이지와 총 페이지 수가 표시 됩니다.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   표시할 페이지가 없는 경우 "0 0 페이지"가 표시 됩니다. (페이지 번호는 페이지 수보다 큰 경우 때문 `Model.PageNumber` 1 및 `Model.PageCount` 은 0입니다.)

   페이징 단추가 표시 됩니다는 `PagedListPager` 도우미:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   `PagedListPager` 도우미 다양 한 스타일 지정 및 Url을 포함 하 여 지정할 수 있는 옵션을 제공 합니다. 자세한 내용은 [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) GitHub 사이트에서.

2. 페이지를 실행 합니다.

   다른 정렬 순서의 페이징 링크를 클릭하여 페이징이 작동하는지 확인합니다. 그런 다음, 검색 문자열을 입력하고 페이징을 다시 시도하여 정렬 및 필터링을 통해 페이징이 제대로 작동하는지 확인합니다.

## <a name="create-an-about-page"></a>정보 페이지 만들기

Contoso University 웹 사이트의 페이지에 대 한 각 등록 날짜에 대해 등록 한 학생 수가 표시 됩니다. 여기에는 그룹화와 그룹에 대한 간단한 계산이 필요합니다. 이 작업을 수행하기 위해 다음을 수행합니다.

- 뷰에 전달해야 하는 데이터에 대해 뷰 모델 클래스를 만듭니다.
- 수정 된 `About` 의 메서드는 `Home` 컨트롤러.
- 수정 된 `About` 보기.

### <a name="create-the-view-model"></a>뷰 모델 만들기

만들기는 *Viewmodel* 프로젝트 폴더의 폴더입니다. 해당 폴더에 있는 클래스 파일을 추가 *EnrollmentDateGroup.cs* 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>홈 컨트롤러 수정

1. *HomeController.cs*, 다음 추가 `using` 파일의 맨 위에 있는 문을:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. 여는 중괄호를 클래스에 대 한 직후 데이터베이스 컨텍스트에 대 한 클래스 변수를 추가 합니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. `About` 메서드를 다음 코드로 바꿉니다.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   LINQ 문은 등록 날짜별로 학생 엔터티를 그룹화하고 각 그룹의 엔터티 수를 계산하며 결과를 `EnrollmentDateGroup` 뷰 모델 개체의 컬렉션에 저장합니다.

4. 추가 된 `Dispose` 메서드:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>정보 뷰 수정

1. 코드를 대체 합니다 *Views\Home\About.cshtml* 를 다음 코드로 파일:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. 앱을 실행 하 고 클릭 합니다 **에 대 한** 링크 합니다.

   각 등록 날짜에 대 한 학생 수가 테이블에 표시 됩니다.

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 자료

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 열 정렬 링크 추가
> * 검색 상자 추가
> * 페이징 추가
> * 정보 페이지 만들기

연결 복원 력 및 명령 인터 셉 션을 사용 하는 방법을 알아보려면 다음 문서로 계속 진행 하세요.
> [!div class="nextstepaction"]
> [연결 복원 력 및 명령 인터 셉 션](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)