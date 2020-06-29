---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework 정렬, 필터링 및 페이징 (3/10) | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 48938b378a741a0f1c351c2cb1d33b5140c6cf93
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484611"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a>ASP.NET MVC 응용 프로그램에서 Entity Framework 정렬, 필터링 및 페이징 (3/10)

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 5 Code First 및 Visual Studio 2012을 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. [이 챕터의](building-the-ef5-mvc4-chapter-downloads.md) 시작 또는 시작 프로젝트 다운로드에서 자습서 시리즈를 시작 하 고 여기에서 시작할 수 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완료 된 챕터를 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 하 여 문제를 재현해 보세요. 일반적으로 코드를 완성 된 코드와 비교 하 여 문제에 대 한 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 방법에 대 한 자세한 내용은 [오류 및 해결](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors) 방법을 참조 하세요.

이전 자습서에서는 엔터티에 대 한 기본 CRUD 작업을 위한 일련의 웹 페이지를 구현 `Student` 했습니다. 이 자습서에서는 **학생** 인덱스 페이지에 정렬, 필터링 및 페이징 기능을 추가 합니다. 단순 그룹화를 수행하는 페이지도 만듭니다.

다음 그림에서는 작업이 완료되었을 때 페이지 모양을 보여 줍니다. 열 제목은 해당 열로 정렬하기 위해 사용자가 클릭할 수 있는 링크입니다. 열 제목을 반복해서 클릭하면 오름차순 및 내림차순으로 정렬 순서가 토글됩니다.

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>학생 인덱스 페이지에 열 정렬 링크 추가

학생 인덱스 페이지에 정렬을 추가 하려면 컨트롤러의 메서드를 변경 하 `Index` `Student` 고 인덱스 뷰에 코드를 추가 `Student` 합니다.

### <a name="add-sorting-functionality-to-the-index-method"></a>인덱스 메서드에 정렬 기능 추가

*Controllers\StudentController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

이 코드는 URL의 쿼리 문자열에서 `sortOrder` 매개 변수를 받습니다. 쿼리 문자열 값은 ASP.NET MVC에서 작업 메서드에 대 한 매개 변수로 제공 됩니다. 매개 변수는 "Name" 또는 "Date" 문자열이며 필요에 따라 밑줄과 내림차순을 지정하는 문자열 "desc"가 옵니다. 기본 정렬 순서는 오름차순입니다.

인덱스 페이지를 처음 요청하면 쿼리 문자열은 없습니다. 학습자는 문에 대 한 제어에 의해 설정 된 기본값 인 오름차순으로 표시 됩니다 `LastName` `switch` . 사용자가 열 제목 하이퍼링크를 클릭하면 쿼리 문자열에 해당 `sortOrder` 값이 제공됩니다.

`ViewBag`뷰가 적절 한 쿼리 문자열 값을 사용 하 여 열 머리글 하이퍼링크를 구성할 수 있도록 두 개의 변수가 사용 됩니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

이것은 3개로 구성된 문입니다. 첫 번째 `sortOrder` 매개 변수는 매개 변수가 null 이거나 비어 있는 경우 `ViewBag.NameSortParm` "이름 desc"로 설정 해야 함을 지정 하 고, 그렇지 않은 경우에는 \_ 빈 문자열로 설정 해야 합니다. 이러한 두 문을 사용하면 뷰에서 다음과 같이 열 제목 하이퍼링크를 설정할 수 있습니다.

| 현재 정렬 순서 | 성 하이퍼링크 | 날짜 하이퍼링크 |
| --- | --- | --- |
| 성 오름차순 | descending | ascending |
| 성 내림차순 | ascending | ascending |
| 날짜 오름차순 | ascending | descending |
| 날짜 내림차순 | ascending | ascending |

메서드는 [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) 을 사용 하 여 정렬 기준으로 사용할 열을 지정 합니다. 이 코드는 문 앞에 [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) 변수 `switch` 를 만들고, 문에서이 변수를 수정 하 `switch` 고, `ToList` 문 다음에 메서드를 호출 합니다 `switch` . `IQueryable` 변수를 작성하고 수정하면 데이터베이스에 쿼리가 보내지지 않습니다. `IQueryable`와 같은 메서드를 호출 하 여 개체를 컬렉션으로 변환할 때까지 쿼리가 실행 되지 않습니다 `ToList` . 따라서이 코드는 문까지 실행 되지 않는 단일 쿼리를 생성 합니다 `return View` .

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>학생 인덱스 뷰에 열 제목 하이퍼링크 추가

*Views\Student\Index.cshtml*에서 `<tr>` `<th>` 제목 행의 및 요소를 강조 표시 된 코드로 바꿉니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

이 코드는 속성의 정보를 사용 하 여 `ViewBag` 적절 한 쿼리 문자열 값으로 하이퍼링크를 설정 합니다.

페이지를 실행 하 고 **Last Name** 및 **등록 날짜** 열 제목을 클릭 하 여 정렬이 작동 하는지 확인 합니다.

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

**성** 머리글을 클릭 하면 학생이 내림차순 성 순서로 표시 됩니다.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>학생 인덱스 페이지에 검색 상자 추가

학생 인덱스 페이지에 필터링을 추가하려면 뷰에 텍스트 상자와 [제출] 단추를 추가하고 `Index` 메서드에 해당 변경 내용을 적용합니다. 텍스트 상자를 통해 이름 및 성 필드에서 검색할 문자열을 입력할 수 있습니다.

### <a name="add-filtering-functionality-to-the-index-method"></a>인덱스 메서드에 필터링 기능 추가

*Controllers\StudentController.cs*에서 `Index` 메서드를 다음 코드로 바꿉니다 (변경 내용이 강조 표시 됨).

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

`searchString` 매개 변수를 `Index` 메서드에 추가했습니다. 또한 `where` 이름 또는 성이 검색 문자열을 포함 하 고 있는 학생만 선택 하는 절을 LINQ statement에 추가 했습니다. 인덱스 뷰에 추가할 텍스트 상자에서 검색 문자열 값이 수신 됩니다. [Where](https://msdn.microsoft.com/library/bb535040.aspx) 절을 추가 하는 문은 검색할 값이 있는 경우에만 실행 됩니다.

> [!NOTE]
> 대부분의 경우 Entity Framework 엔터티 집합에 대해 동일한 메서드를 호출 하거나 메모리 내 컬렉션에서 확장 메서드로 호출할 수 있습니다. 결과는 일반적으로 동일 하지만 경우에 따라 다를 수 있습니다. 예를 들어 메서드의 .NET Framework 구현은 `Contains` 빈 문자열을 전달할 때 모든 행을 반환 하지만 SQL Server Compact 4.0에 대 한 Entity Framework 공급자는 빈 문자열에 대해 0 개의 행을 반환 합니다. 따라서이 예제의 코드 (문 `Where` 내에 문을 배치)는 `if` 모든 버전의 SQL Server에 대해 동일한 결과를 얻을 수 있도록 합니다. 또한 메서드의 .NET Framework 구현은 `Contains` 기본적으로 대/소문자를 구분 하는 비교를 수행 하지만 Entity Framework SQL Server 공급자는 기본적으로 대/소문자를 구분 하지 않는 비교를 수행 합니다. 따라서 메서드를 호출 `ToUpper` 하 여 테스트를 명시적으로 대/소문자를 구분 하지 않도록 설정 하면 나중에 리포지토리를 사용 하도록 코드를 변경할 때 결과가 변경 되지 않습니다 `IEnumerable` . 그러면 개체가 아닌 컬렉션이 반환 됩니다 `IQueryable` . (`IEnumerable` 컬렉션에서 `Contains` 메서드를 호출하면 .NET Framework 구현을 가져오고 `IQueryable` 개체에서 호출하면 데이터베이스 공급자 구현을 가져옵니다.)

### <a name="add-a-search-box-to-the-student-index-view"></a>Students 인덱스 뷰에 검색 상자 추가

*Views\Student\Index.cshtml*에서 `table` 캡션, 텍스트 상자 및 **검색** 단추를 만들기 위해 강조 표시 된 코드를 여는 태그 바로 앞에 추가 합니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

페이지를 실행 하 고 검색 문자열을 입력 한 다음 **검색** 을 클릭 하 여 필터링이 작동 하는지 확인 합니다.

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

URL에 "a" 검색 문자열이 포함 되어 있지 않습니다. 즉,이 페이지를 책갈피로 만들면 책갈피를 사용할 때 필터링 된 목록을 가져올 수 없습니다. **검색** 단추를 변경 하 여 자습서의 뒷부분에서 필터 조건에 대 한 쿼리 문자열을 사용 합니다.

## <a name="add-paging-to-the-students-index-page"></a>학생 인덱스 페이지에 페이징 추가

학생 인덱스 페이지에 페이징을 추가 하려면 **PagedList** NuGet 패키지를 설치 하는 것으로 시작 합니다. 그런 다음 메서드를 추가로 변경 하 `Index` 고 뷰에 페이징 링크를 추가 `Index` 합니다. **PagedList** 는 ASP.NET Mvc에 대 한 다양 한 페이징 및 정렬 패키지 중 하나 이며, 여기에서 사용 하는 것은 다른 옵션에 대 한 권장 사항이 아닌 예제로만 사용 됩니다. 다음 그림에서는 페이징 링크를 보여 줍니다.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>PagedList NuGet 패키지를 설치 합니다.

NuGet **PagedList** 패키지는 자동으로 **PagedList** 패키지를 종속성으로 설치 합니다. **PagedList** 패키지는 및 컬렉션 `PagedList` 에 대 한 컬렉션 형식 및 확장 메서드를 설치 합니다 `IQueryable` `IEnumerable` . 확장 메서드는 또는에서 컬렉션에 데이터의 단일 페이지를 만들며 `PagedList` `IQueryable` `IEnumerable` , `PagedList` 컬렉션은 페이징을 용이 하 게 하는 여러 속성과 메서드를 제공 합니다. **PagedList** 패키지는 페이징 단추를 표시 하는 페이징 도우미를 설치 합니다.

**도구** 메뉴에서 **nuget 패키지 관리자** 를 선택한 다음 **솔루션에 대 한 nuget 패키지 관리**를 선택 합니다.

**NuGet 패키지 관리** 대화 상자에서 왼쪽의 **온라인** 탭을 클릭 한 다음 검색 상자에 "페이징"을 입력 합니다. **PagedList** 패키지가 표시 되 면 **설치**를 클릭 합니다.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

**프로젝트 선택** 상자에서 **확인**을 클릭 합니다.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a>인덱스 메서드에 페이징 기능 추가

*Controllers\StudentController.cs*에서 `using` 네임 스페이스에 대 한 문을 추가 합니다 `PagedList` .

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`Index` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

이 코드는 다음과 같이 `page` 매개 변수, 현재 정렬 순서 매개 변수 및 현재 필터 매개 변수를 메서드 시그니처에 추가 합니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

페이지가 처음 표시되거나 사용자가 페이징 또는 정렬 링크를 클릭하지 않으면 모든 매개 변수가 Null이 됩니다. 페이징 링크를 클릭 하면 `page` 표시할 페이지 번호가 변수에 포함 됩니다.

`A ViewBag`속성은 현재 정렬 순서를 사용 하 여 뷰를 제공 합니다 .이는 페이징 링크에 정렬 순서를 유지 하기 위해 페이징 링크에 포함 되어야 하기 때문입니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

또 다른 속성인는 `ViewBag.CurrentFilter` 현재 필터 문자열을 사용 하 여 뷰를 제공 합니다. 이 값은 페이징 중 필터 설정을 유지하기 위해 페이징 링크에 포함되어야 하며 페이지를 다시 표시할 때 텍스트 상자에 복원되어야 합니다. 페이징 중에 검색 문자열이 변경되면 새 필터로 인해 다른 데이터가 표시될 수 있으므로 페이지는 1로 재설정되어야 합니다. 텍스트 상자에 값을 입력 하 고 제출 단추를 누르면 검색 문자열이 변경 됩니다. 이 경우 `searchString` 매개 변수는 null이 아닙니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

메서드 끝에서 `ToPagedList` 학생 개체의 확장 메서드는 `IQueryable` 학생 쿼리를 페이징을 지 원하는 컬렉션 형식으로 학생의 단일 페이지로 변환 합니다. 그런 다음 학생의 단일 페이지가 보기에 전달 됩니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`ToPagedList` 메서드는 페이지 번호를 사용합니다. 두 물음표는 [null 병합 연산자](https://msdn.microsoft.com/library/ms173224.aspx)를 나타냅니다. Null 병합 연산자는 nullable 형식의 기본값을 정의합니다. `(page ?? 1)` 식은 값이 있는 경우 `page` 값을 반환하고 `page`가 Null이면 1일 반환합니다.

### <a name="add-paging-links-to-the-student-index-view"></a>학생 인덱스 뷰에 페이징 링크 추가

*Views\Student\Index.cshtml*에서 기존 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

페이지 맨 위에 `@model` 문은 뷰가 `List` 개체 대신 `PagedList` 개체를 가져오는 것을 지정합니다.

`using`에 대 한 문은 `PagedList.Mvc` 페이징 단추의 MVC 도우미에 대 한 액세스를 제공 합니다.

코드는 [Formmethod. Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)을 지정할 수 있는 [html.beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 의 오버 로드를 사용 합니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

기본 [HTML.BEGINFORM](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) POST를 사용 하 여 폼 데이터를 전송 합니다. 즉, 매개 변수가 HTTP 메시지 본문에 전달 되 고 URL에 쿼리 문자열로 전달 되지 않습니다. HTTP GET을 지정하면 폼 데이터가 URL에 쿼리 문자열로 전달되고 이를 통해 사용자는 URL을 책갈피로 지정할 수 있습니다. [HTTP get 사용에 대 한 W3C 지침](http://www.w3.org/2001/tag/doc/whenToUseGet.html) 에서는 작업으로 인해 업데이트가 발생 하지 않을 때 get을 사용 해야 합니다.

텍스트 상자는 현재 검색 문자열로 초기화 되므로 새 페이지를 클릭 하면 현재 검색 문자열을 볼 수 있습니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

열 머리글 링크는 쿼리 문자열을 사용하여 현재 검색 문자열을 컨트롤러에 전달하므로 사용자가 필터 결과 내에서 정렬할 수 있습니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

현재 페이지와 총 페이지 수가 표시 됩니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

표시할 페이지가 없으면 "0/0 페이지"가 표시 됩니다. 이 경우 페이지 번호는 `Model.PageNumber` 가 1이 고가 0 이므로 페이지 수는 페이지 수보다 큽니다 `Model.PageCount` .

도우미는 페이징 단추를 표시 합니다 `PagedListPager` .

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`PagedListPager`도우미는 url 및 스타일을 포함 하 여 사용자 지정할 수 있는 다양 한 옵션을 제공 합니다. 자세한 내용은 GitHub 사이트에서 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 를 참조 하세요.

페이지를 실행 합니다.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

다른 정렬 순서의 페이징 링크를 클릭하여 페이징이 작동하는지 확인합니다. 그런 다음, 검색 문자열을 입력하고 페이징을 다시 시도하여 정렬 및 필터링을 통해 페이징이 제대로 작동하는지 확인합니다.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>학생 통계를 표시 하는 정보 페이지 만들기

Contoso University 웹 사이트의 정보 페이지에는 각 등록 날짜에 등록된 학생 수가 표시됩니다. 여기에는 그룹화와 그룹에 대한 간단한 계산이 필요합니다. 이 작업을 수행하기 위해 다음을 수행합니다.

- 뷰에 전달해야 하는 데이터에 대해 뷰 모델 클래스를 만듭니다.
- `About`컨트롤러에서 메서드를 수정 `Home` 합니다.
- 뷰를 수정 `About` 합니다.

### <a name="create-the-view-model"></a>뷰 모델 만들기

*Viewmodels* 폴더를 만듭니다. 해당 폴더에서 *EnrollmentDateGroup.cs* 클래스를 추가 하 고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>홈 컨트롤러 수정

*HomeController.cs*에서 `using` 파일 맨 위에 다음 문을 추가 합니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

클래스에 대 한 여는 중괄호 바로 뒤에 데이터베이스 컨텍스트에 대 한 클래스 변수를 추가 합니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

`About` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

LINQ 문은 등록 날짜별로 학생 엔터티를 그룹화하고 각 그룹의 엔터티 수를 계산하며 결과를 `EnrollmentDateGroup` 뷰 모델 개체의 컬렉션에 저장합니다.

메서드를 추가 합니다 `Dispose` .

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>정보 뷰 수정

*Views\Home\About.cshtml* 파일의 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

앱을 실행 하 고 **정보** 링크를 클릭 합니다. 각 등록 날짜에 대한 학생 수가 테이블에 표시됩니다.

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a>선택 사항: Windows Azure에 앱 배포

지금까지 응용 프로그램은 개발 컴퓨터의 IIS Express에서 로컬로 실행 되었습니다. 다른 사용자가 인터넷을 통해 사용할 수 있도록 하려면 웹 호스팅 공급자에 배포 해야 합니다. 자습서의이 섹션에서는 Windows Azure 웹 사이트에 배포 합니다.

### <a name="using-code-first-migrations-to-deploy-the-database"></a>Code First 마이그레이션를 사용 하 여 데이터베이스 배포

데이터베이스를 배포 하려면 Code First 마이그레이션을 사용 합니다. Visual Studio에서 배포에 대 한 설정을 구성 하는 데 사용 하는 게시 프로필을 만들 때 **Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행)** 이라는 레이블이 지정 된 확인란을 선택 합니다. 이 설정을 사용 하면 Code First 이니셜라이저 클래스를 사용 하도록 배포 프로세스에서 대상 서버의 응용 프로그램 *Web.config* 파일을 자동으로 구성 합니다 `MigrateDatabaseToLatestVersion` .

Visual Studio는 배포 프로세스 중에 데이터베이스에서 어떤 작업도 수행 하지 않습니다. 배포 된 응용 프로그램이 배포 후 처음으로 데이터베이스에 액세스 하는 경우 Code First에서 자동으로 데이터베이스를 만들거나 데이터베이스 스키마를 최신 버전으로 업데이트 합니다. 응용 프로그램이 마이그레이션 방법을 구현 하는 경우이 `Seed` 메서드는 데이터베이스가 만들어지거나 스키마가 업데이트 된 후에 실행 됩니다.

마이그레이션 `Seed` 방법은 테스트 데이터를 삽입 합니다. 프로덕션 환경에 배포 하는 경우 `Seed` 프로덕션 데이터베이스에 삽입 하려는 데이터만 삽입 하도록 메서드를 변경 해야 합니다. 예를 들어 현재 데이터 모델에서는 개발 데이터베이스에 실제 강의를 포함 하 고 가상 학생이 있을 수 있습니다. 개발 중에를 `Seed` 로드 하는 메서드를 작성 한 다음 프로덕션에 배포 하기 전에 가상 학생을 주석으로 처리할 수 있습니다. 또는 `Seed` 단지 강좌를 로드 하는 메서드를 작성 하 고 응용 프로그램의 UI를 사용 하 여 테스트 데이터베이스에 가상 학생을 수동으로 입력할 수 있습니다.

### <a name="get-a-windows-azure-account"></a>Microsoft Azure 계정 가져오기

Microsoft Azure 계정이 필요 합니다. 아직 없는 경우 몇 분만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Windows Azure 무료 평가판](https://azure.microsoft.com/free/dotnet/)을 참조 하세요.

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a>Microsoft Azure에서 웹 사이트 및 SQL 데이터베이스 만들기

Microsoft Azure 웹 사이트는 공유 호스팅 환경에서 실행 됩니다. 즉, 다른 Windows Azure 클라이언트와 공유 되는 Vm (가상 컴퓨터)에서 실행 됩니다. 공유 호스팅 환경은 클라우드를 시작하는 저비용 방법입니다. 나중에 웹 트래픽이 증가하면 애플리케이션이 전용 VM에서 실행되어 요구에 맞게 확장될 수 있습니다. 더 복잡 한 아키텍처가 필요한 경우 Windows Azure 클라우드 서비스로 마이그레이션할 수 있습니다. 클라우드 서비스는 요구에 따라 구성할 수 있는 전용 VM에서 실행됩니다.

Windows Azure SQL Database은 SQL Server 기술을 기반으로 구축 된 클라우드 기반의 관계형 데이터베이스 서비스입니다. SQL Server와 함께 작동 하는 도구 및 응용 프로그램은 SQL Database 에서도 작동 합니다.

1. [Windows Azure 관리 포털](https://manage.windowsazure.com/)의 왼쪽 탭에서 **웹 사이트** 를 클릭 한 다음 **새로 만들기**를 클릭 합니다.

    ![관리 포털의 새 단추](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. **사용자 지정 만들기**를 클릭 합니다.

    ![관리 포털에서 데이터베이스 링크를 사용 하 여 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   **새 웹 사이트-사용자 지정 만들기** 마법사가 열립니다.
3. 마법사의 **새 웹 사이트** 단계에서 **url** 상자에 문자열을 입력 하 여 응용 프로그램에 대 한 고유 url로 사용 합니다. 전체 URL은 여기에 입력한 문자열과 텍스트 상자 옆에 표시되는 접미사로 구성됩니다. 이 그림에는 "ConU"가 표시 되지만 해당 URL을 선택 해야 합니다.

    ![관리 포털에서 데이터베이스 링크를 사용 하 여 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. **지역** 드롭다운 목록에서 가까운 지역을 선택 합니다. 이 설정은 웹 사이트를 실행 하는 데이터 센터를 지정 합니다.
5. **데이터베이스** 드롭다운 목록에서 **무료 20Mb SQL 데이터베이스 만들기**를 선택 합니다.

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. **DB 연결 문자열 이름**에 *schoolcontext.cs*를 입력 합니다.

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. 상자 아래쪽의 오른쪽을 가리키는 화살표를 클릭 합니다. 마법사에서 **데이터베이스 설정** 단계로 이동 합니다.
8. **이름** 상자에 다음 *을 입력 합니다*.
9. **서버** 상자에서 **새로 만들기 SQL Database 서버**를 선택 합니다. 또는 이전에 서버를 만든 경우 드롭다운 목록에서 해당 서버를 선택할 수 있습니다.
10. 관리자 **로그인 이름** 및 **암호**를 입력 합니다. **New SQL Database 서버**를 선택한 경우 여기서 기존 이름과 암호를 입력하지 않고 나중에 데이터베이스에 액세스할 때 사용하기 위해 지금 정의하는 새 이름과 암호를 입력합니다. 이전에 만든 서버를 선택한 경우 해당 서버에 대 한 자격 증명을 입력 합니다. 이 자습서에서는 ***고급*** 확인란을 선택 하지 않습니다. ***고급*** 옵션을 사용 하 여 데이터베이스 [데이터 정렬을](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)설정할 수 있습니다.
11. 웹 사이트에 대해 선택한 것과 동일한 **지역을** 선택 합니다.
12. 상자 오른쪽 아래에 있는 확인 표시를 클릭 하 여 완료 되었음을 표시 합니다.   
  
    ![새 웹 사이트의 데이터베이스 설정 단계-데이터베이스 마법사를 사용 하 여 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    다음 이미지는 기존 SQL Server 및 로그인을 사용 하는 방법을 보여 줍니다.   
  
    ![새 웹 사이트의 데이터베이스 설정 단계-데이터베이스 마법사를 사용 하 여 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    관리 포털은 웹 사이트 페이지로 반환 되 고 **상태** 열에는 사이트가 만들어지고 있는 것으로 표시 됩니다. 잠시 후 (일반적으로 1 분 미만) **상태** 열에는 사이트가 성공적으로 생성 된 것으로 표시 됩니다. 왼쪽의 탐색 모음에서 계정에 있는 사이트 수가 **웹 사이트** 아이콘 옆에 나타나고 데이터베이스 수가 **SQL 데이터베이스** 아이콘 옆에 표시 됩니다.

## <a name="deploy-the-application-to-windows-azure"></a>Windows Azure에 응용 프로그램 배포

1. Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **게시**를 선택합니다.  
  
    ![프로젝트 상황에 맞는 메뉴의 게시](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. **웹 게시** 마법사의 **프로필** 탭에서 **가져오기**를 클릭 합니다.  
  
    ![게시 설정 가져오기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. 이전에 Visual Studio에서 Windows Azure 구독을 추가 하지 않은 경우 다음 단계를 수행 합니다. 이러한 단계에서는 **Windows Azure 웹 사이트에서 가져오기** 아래의 드롭다운 목록에 웹 사이트가 포함 되도록 구독을 추가 합니다.

    a. **게시 프로필 가져오기** 대화 상자에서 **windows azure 웹 사이트에서 가져오기**를 클릭 한 다음 **windows azure 구독 추가**를 클릭 합니다.

    ![Windows Azure 구독 추가](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    b. **Windows Azure 구독 가져오기** 대화 상자에서 **구독 파일 다운로드**를 클릭 합니다.

    ![구독 파일 다운로드](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    c. 브라우저 창에서 *publishsettings* 파일을 저장 합니다.

    ![publishsettings 파일 다운로드](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > 보안- *publishsettings* 파일에는 microsoft Azure 구독 및 서비스를 관리 하는 데 사용 되는 자격 증명 (인코딩되지 않음)이 포함 되어 있습니다. 이 파일에 대 한 보안 모범 사례는 원본 디렉터리 외부 (예: *: libraries\documents* 폴더)에 임시로 저장 한 다음 가져오기가 완료 되 면 삭제 하는 것입니다. 파일에 대 한 액세스 권한을 획득 하는 악의적인 사용자는 `.publishsettings` Microsoft Azure 서비스를 편집, 생성 및 삭제할 수 있습니다.

    d. **Windows Azure 구독 가져오기** 대화 상자에서 **찾아보기** 를 클릭 하 고 *publishsettings* 파일로 이동 합니다.

    ![하위 다운로드](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    e. **가져오기**를 클릭합니다.

    ![import](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. **게시 프로필 가져오기** 대화 상자에서 **Windows Azure 웹 사이트에서 가져오기**를 선택 하 고 드롭다운 목록에서 웹 사이트를 선택한 다음 **확인**을 클릭 합니다.  
  
    ![게시 프로필 가져오기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. **연결** 탭에서 **연결 유효성 검사** 를 클릭 하 여 설정이 올바른지 확인 합니다.  
  
    ![연결 유효성 검사](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. 연결의 유효성을 검사 한 경우 **연결 유효성 검사** 단추 옆에 녹색 확인 표시가 표시 됩니다. **다음**을 클릭합니다.  
  
    ![연결의 유효성을 검사 했습니다.](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. **Schoolcontext.cs** 아래에 있는 **원격 연결 문자열** 드롭다운 목록을 열고 사용자가 만든 데이터베이스에 대 한 연결 문자열을 선택 합니다.
8. **Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행)** 을 선택 합니다.
9. 이 응용 프로그램에서 멤버 자격 데이터베이스를 사용 하지 않으므로 **Usercontext (defaultconnection)** 에 대해 **런타임에이 연결 문자열 사용** 을 선택 취소 합니다.   
  
    ![설정 탭](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. **다음**을 클릭합니다.
11. **미리 보기** 탭에서 **미리 보기 시작**을 클릭 합니다.  
  
    ![미리 보기 탭의 StartPreview 단추](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    이 탭에는 서버에 복사 되는 파일의 목록이 표시 됩니다. 미리 보기를 표시 하는 것은 응용 프로그램을 게시 하는 데 필요 하지 않지만 인식 하기 위한 유용한 기능입니다. 이 경우 표시 되는 파일 목록을 사용 하 여 아무런 작업을 수행할 필요가 없습니다. 다음에이 응용 프로그램을 배포할 때 변경 된 파일만이 목록에 표시 됩니다.  
  
    ![StartPreview 파일 출력](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. **게시**를 클릭합니다.  
    Visual Studio에서 Windows Azure 서버에 파일을 복사 하는 프로세스를 시작 합니다.
13. **출력** 창에 수행된 배포 작업이 표시되고 성공적인 배포 완료가 보고됩니다.  
  
    ![성공적인 배포를 보고 하는 출력 창](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. 성공적으로 배포 되 면 배포 된 웹 사이트의 URL에 대 한 기본 브라우저가 자동으로 열립니다.  
    만든 애플리케이션이 이제 클라우드에서 실행되고 있습니다. 학생 탭을 클릭 합니다.  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

이제 **Code First 마이그레이션 실행 (앱 시작 시 실행)** 을 선택 했기 때문에 *schoolcontext.cs* 데이터베이스가 Windows Azure SQL Database에서 생성 되었습니다. 배포 된 웹 사이트의 *Web.config* 파일이 변경 되어 코드가 처음으로 데이터베이스에서 데이터를 읽거나 쓸 때 ( **학생** 탭을 선택 했을 때 발생) [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저가 실행 됩니다.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

또한 배포 프로세스에서는 데이터베이스 스키마를 업데이트 하 고 데이터베이스를 시드 하는 데 사용할 Code First 마이그레이션에 대 한 새 연결 문자열 *(Schoolcontext.cs \_ databasepublish*)을 만들었습니다.

![연결 문자열 Database_Publish](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

*Defaultconnection* 연결 문자열은 멤버 자격 데이터베이스 (이 자습서에서는 사용 하지 않음)에 대 한 연결 문자열입니다. *Schoolcontext.cs* 연결 문자열은 ContosoUniversity 데이터베이스에 대 한 것입니다.

*ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*의 사용자 컴퓨터에서 Web.config 파일의 배포 된 버전을 찾을 수 있습니다. FTP를 사용 하 여 배포 된 *Web.config* 파일 자체에 액세스할 수 있습니다. 지침은 [Visual Studio를 사용 하 여 웹 배포 ASP.NET: 코드 업데이트 배포](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)를 참조 하세요. "FTP 도구를 사용 하려면 FTP URL, 사용자 이름 및 암호를 사용 해야 합니다."로 시작 하는 지침을 따르세요.

> [!NOTE]
> 웹 앱은 보안을 구현 하지 않으므로 URL을 검색 하는 모든 사용자가 데이터를 변경할 수 있습니다. 웹 사이트를 보호 하는 방법에 대 한 자세한 내용은 [Windows Azure 웹 사이트에 멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 앱 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)를 참조 하십시오. 다른 사용자가 Visual Studio에서 Windows Azure 관리 포털 또는 **서버 탐색기** 를 사용 하 여 사이트를 사용 하지 못하도록 하 여 사이트를 중지할 수 있습니다.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a>Code First 이니셜라이저

배포 섹션에서 사용 되는 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저를 살펴보았습니다. [Createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (기본값), [Dropcreatedatabaseifmodelchanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) 및 [dropcreatedatabasealways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)를 포함 하 여 사용할 수 있는 다른 이니셜라이저가 Code First 제공 됩니다. `DropCreateAlways`이니셜라이저는 단위 테스트에 대 한 조건을 설정 하는 데 유용할 수 있습니다. 사용자 고유의 이니셜라이저를 작성 하 고 응용 프로그램이 데이터베이스에서 읽거나 데이터베이스에 쓸 때까지 기다리지 않으려는 경우 이니셜라이저를 명시적으로 호출할 수도 있습니다. 이니셜라이저에 대 한 자세한 설명은 Julie Lerman 및 Rowan에서 Code First 하는 책 [프로그래밍 Entity Framework](http://shop.oreilly.com/product/0636920022220.do) 의 6 장을 참조 하세요.

## <a name="summary"></a>요약

이 자습서에서는 데이터 모델을 만들고 기본 CRUD, 정렬, 필터링, 페이징 및 그룹화 기능을 구현 하는 방법을 살펴보았습니다. 다음 자습서에서는 데이터 모델을 확장 하 여 고급 항목을 확인 하기 시작 합니다.

[ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
> [다음](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
