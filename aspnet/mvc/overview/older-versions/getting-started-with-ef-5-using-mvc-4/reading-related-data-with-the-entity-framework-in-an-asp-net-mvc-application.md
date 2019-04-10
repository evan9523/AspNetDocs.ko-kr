---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: (5 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 관련된 데이터 읽기 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: f86212c1cb559c164342997fb0e4208339b5e3cc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59421123"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a>관련 (5 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 데이터 읽기

[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장이에 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완성 된 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드의 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


이전 자습서에서 School 데이터 모델을 완료 했습니다. 이 자습서에서는 읽기 및 관련된 데이터 표시 됩니다-즉, Entity Framework는 탐색 속성으로 로드 하는 데이터입니다.

다음 그림에서는 사용할 페이지를 보여 줍니다.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a>관련된 데이터의 지연 로딩과 명시적 로드

Entity Framework 관련된 데이터를 엔터티의 탐색 속성으로 로드할 수는 여러 가지가 있습니다.

- *지연 로드*. 엔터티를 처음 읽을 때 관련된 데이터가 검색되지 않습니다. 그러나 탐색 속성에 처음으로 액세스하려고 할 때 해당 탐색 속성에 필요한 데이터가 자동으로 검색됩니다. 이 인해 여러 쿼리가 데이터베이스로 전송-엔터티 자체 및 각 시간 관련 엔터티에 대 한 데이터를 검색 해야 합니다. 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *즉시 로드*. 엔터티를 읽을 때 관련된 데이터가 함께 검색됩니다. 이는 일반적으로 필요한 데이터를 모두 검색하는 단일 조인 쿼리를 발생시킵니다. 즉시 로드를 사용 하 여 지정 된 `Include` 메서드.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *명시적 로드*. 이 지연 로드를 제외 하 코드에서 관련된 데이터를 명시적으로 검색 탐색 속성에 액세스할 때 자동으로 발생 하지 않습니다. 관련된 데이터를 수동으로 로드 하는 엔터티 및 호출에 대 한 개체 상태 관리자 항목을 가져와서 합니다 `Collection.Load` 컬렉션에 대 한 메서드 또는 `Reference.Load` 단일 엔터티를 포함 하는 속성에 대 한 메서드. (다음 예제에서는 관리자 탐색 속성을 로드 하려는 경우 바꿔서 `Collection(x => x.Courses)` 사용 하 여 `Reference(x => x.Administrator)`.)

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

속성 값을 즉시 검색 하지 않으므로 지연 로드 및 명시적 로딩은 둘 다 라고도 *지연 된 로드*합니다.

일반적으로 알고 있는 경우 해야 관련된 데이터 검색을 즉시 로드는 최상의 성능을 제공 하는 모든 엔터티에 대 한 데이터베이스에 전송 된 단일 쿼리 검색 된 각 엔터티에 대 한 별도 쿼리보다 일반적으로 더 효율적 이므로 합니다. 예를 들어, 위의 예에서 각 부서에 10 개의 관련 된 강좌가 가정 합니다. 즉시 로드 예제는 데이터베이스에 왕복만 단일 (조인) 쿼리 및 단일으로 반환 됩니다. 지연 로드 하 고 명시적 로드 예제는 둘 다 11 개의 쿼리 및 11 개 왕복으로 인해 데이터베이스. 데이터베이스에 대한 추가 왕복은 대기 시간이 길 때 성능에 특히 악영향을 줍니다.

반면에 일부 시나리오에서는 지연 로딩을 더 효율적입니다. 즉시 로드는 SQL Server를 효율적으로 처리할 수 없습니다는 매우 복잡 한 조인이 생성 될 발생할 수 있습니다. 또는 처리 하는 엔터티 집합의 하위 집합에 대해서만 엔터티의 탐색 속성에 액세스 해야 할 경우, 지연 로드는 즉시 로드는 필요한 것 보다 더 많은 데이터를 검색 하므로 더 잘 수행할 수 있습니다. 성능이 중요한 경우 최상의 선택을 위해 두 가지 방식으로 성능을 테스트하는 것이 가장 좋습니다.

일반적으로 지연 오프 로드를 설정한 경우에 명시적 로드를 사용할 수 있습니다. Serialization 중 지연 오프 로드 설정 해야 하는 경우 시나리오 중 하나 이며 지연 로드 하 고 직렬화도 혼합 하지 마세요 및 지연 하는 경우 의도 한 것 보다 훨씬 더 많은 데이터를 쿼리 하 게 주의 하지 않으면 로드가 사용 됩니다. 직렬화 된 형식의 인스턴스에서 각 속성에 액세스 하 여 일반적으로 작동 합니다. 속성 액세스는 지연 로드를 트리거하고 지연 로드 된 엔터티 serialize 됩니다. Serialization 프로세스에는 다음 지연 로드 하는 엔터티를 잠재적으로 더 많은 지연 로드 및 serialization을 일으키는의 각 속성에 액세스 합니다. 런어웨이 연쇄 반응을이 방지 하려면 지연 엔터티를 serialize 하기 전에 오프 로드를 설정 합니다.

데이터베이스 컨텍스트 클래스는 기본적으로 지연 로드를 수행합니다. 두 가지 방법으로 지연 로드를 사용 하지 않도록 설정 합니다.

- 특정 탐색 속성에 대 한 생략 된 `virtual` 키워드는 속성을 선언 하는 경우.
- 모든 탐색 속성에 설정할 `LazyLoadingEnabled` 에 `false`입니다. 예를 들어 컨텍스트 클래스의 생성자에서 다음 코드를 넣을 수 있습니다. 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

지연 로드 성능 문제를 일으키는 코드를 숨길 수 있습니다. 예를 들어, 즉시 또는 명시적 로드를 지정 하지 않으면 하지만 대량의 엔터티를 처리 하 고, 각 반복에서 여러 탐색 속성을 사용 하는 코드 않을 매우 효율적인 (때문에 데이터베이스에 여러 번 왕복). 온-프레미스 SQL server를 사용 하 여 개발에서 효율적으로 작동 하는 응용 프로그램 대기 시간이 증가 및 지연 로드로 인해 Azure SQL Database를 이동할 때 성능 문제가 있을 수 있습니다. 현실적인 테스트 부하를 사용 하 여 데이터베이스 쿼리를 프로 파일링 지연 로딩은 적절 한 경우를 결정 하는 데 도움이 됩니다. 자세한 내용은 참조 하세요. [Entity Framework 전략 익히기: 관련된 데이터 로드](https://msdn.microsoft.com/magazine/hh205756.aspx) 하 고 [SQL Azure 네트워크 대기 시간을 줄이기 위해 Entity Framework를 사용 하 여](https://msdn.microsoft.com/magazine/gg309181.aspx)입니다.

## <a name="create-a-courses-index-page-that-displays-department-name"></a>과정 인덱스 페이지는 표시 부서 이름 만들기

합니다 `Course` 엔터티를 포함 하는 탐색 속성을 포함 합니다 `Department` 강좌에 할당 된 부서 엔터티. 가져오기 과정의 목록에 할당 된 부서의 이름을 표시할 해야는 `Name` 속성을를 `Department` 에 있는 엔터티는 `Course.Department` 탐색 속성.

라는 컨트롤러를 만듭니다 `CourseController` 에 대 한는 `Course` 엔터티 형식에는 이전에 수행한 동일한 옵션을 사용 하는 `Student` 다음 그림에 나와 있는 것 처럼 컨트롤러 (DAL 네임 스페이스에 컨텍스트 클래스 이미지와 달리 제외 모델 네임 스페이스가 아니라):

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

오픈 *Controllers\CourseController.cs* 확인을 `Index` 메서드:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

자동 스캐폴딩은 `Include` 메서드를 사용하여 `Department` 탐색 속성에 대해 즉시 로드를 지정했습니다.

오픈 *Views\Course\Index.cshtml* 기존 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

스캐폴드 코드에 다음 변경 내용을 만들었습니다.

- 제목을 변경 **인덱스** 하 **과정**합니다.
- 행 파일에 대 한 링크를 왼쪽으로 이동 합니다.
- 제목 아래에서 열을 추가 했습니다 **수** 보여주는 `CourseID` 속성 값입니다. (기본적으로 기본 키 되지 스 캐 폴드 된 되므로 일반적으로 최종 사용자에 게 의미가 없습니다. 그러나이 경우 기본 키가 의미 있는 및 대화 상자를 표시 하려는.)
- 마지막 열 머리글을 변경 **DepartmentID** (외래 키의 이름을 합니다 `Department` 엔터티)에 **부서**합니다.

마지막 열에 대 한 스 캐 폴드 된 코드를 표시 하는 `Name` 의 속성을 `Department` 로드 되는 엔터티는 `Department` 탐색 속성:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

페이지를 실행 합니다 (선택 된 **과정** Contoso University 홈페이지 탭) 부서 이름의 목록을 보려면.

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a>과정 및 등록을 보여 주는 강사 인덱스 페이지 만들기

이 섹션의 컨트롤러를 만들고에 대 한 보기를 `Instructor` 강사 인덱스 페이지를 표시 하기 위해 엔터티:

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

이 페이지는 다음과 같은 방법으로 관련된 데이터를 읽고 표시합니다.

- 강사 목록은의 관련된 데이터를 표시 합니다 `OfficeAssignment` 엔터티. `Instructor` 및 `OfficeAssignment` 엔터티는 일대영 또는 일 관계에 있습니다. 에 대 한 즉시 로드를 사용 하 여 `OfficeAssignment` 엔터티. 이전에 설명한 대로 기본 테이블의 검색된 모든 행에 관련된 데이터가 필요한 경우 즉시 로드는 일반적으로 더 효율적입니다. 이 경우 표시된 모든 강사에 대한 사무실 할당을 표시하길 원합니다.
- 사용자가 관련 강사를 선택 하는 경우 `Course` 엔터티가 표시 됩니다. `Instructor` 및 `Course` 엔터티는 다대다 관계에 있습니다. 에 대 한 즉시 로드를 사용 하 여 `Course` 엔터티 및 해당 관련 `Department` 엔터티. 이 경우 선택한 강사에 대해서만 강좌가 필요 하기 때문에 지연 로드 더 효율적일 수 있습니다. 그러나 이 예제에서는 탐색 속성에 있는 엔터티 내에서 탐색 속성에 대한 즉시 로드를 사용하는 방법을 보여 줍니다.
- 사용자가 강좌를 선택 하면 관련 된 데이터가 `Enrollments` 엔터티 집합에 표시 됩니다. `Course` 및 `Enrollment` 엔터티는 일대다 관계에 있습니다. 에 대 한 명시적 로드를 추가할 `Enrollment` 엔터티 및 해당 관련 `Student` 엔터티. (명시적 로드 필요는 없습니다 지연 로딩을 사용 하지만 명시적 로드를 수행 하는 방법을 보여 줍니다.)

### <a name="create-a-view-model-for-the-instructor-index-view"></a>강사 인덱스 뷰에 대 한 뷰 모델 만들기

강사 인덱스 페이지의 서로 다른 세 테이블을 보여 줍니다. 따라서 각각이 테이블 중 하나에 대한 데이터를 보유하는 세 가지 속성을 포함하는 보기 모델을 만듭니다.

에 *Viewmodel* 폴더를 만들기 *InstructorIndexData.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a>선택한 행에 대 한 스타일을 추가합니다.

선택한 행을 표시 하려면 다른 배경색을 해야 합니다. 스타일이이 UI를 제공 하려면 다음 강조 표시 된 코드 섹션에 추가 `/* info and errors */` 에 *Content\Site.css*다음과 같이 합니다.

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a>강사 컨트롤러 및 뷰 만들기

만들기는 `InstructorController` 다음 그림에 나와 있는 것 처럼 컨트롤러:

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

오픈 *Controllers\InstructorController.cs* 추가한를 `using` 방침을 `ViewModels` 네임 스페이스:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

스 캐 폴드 된 코드를 `Index` 동안만 즉시 로드를 지정 하는 메서드는 `OfficeAssignment` 탐색 속성:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

대체는 `Index` 메서드를 다음 코드로 추가 로드 관련 데이터 및 보기 모델에 넣습니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

메서드에서 선택적 경로 데이터 (`id`) 및 쿼리 문자열 매개 변수 (`courseID`)는 선택한 강사 및 선택한 과정의 ID 값을 제공 하 고 뷰에 모든 필요한 데이터를 전달 합니다. 매개 변수는 페이지의 **선택** 하이퍼링크에서 제공됩니다.

> [!TIP]
> 
> **경로 데이터**
> 
> 경로 데이터는 모델 바인더는 라우팅 테이블에 지정 된 URL 세그먼트에 있는 데이터입니다. 기본 경로 지정 하는 예를 들어 `controller`하십시오 `action`, 및 `id` 세그먼트:
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> 다음 URL에서 기본 경로 매핑합니다 `Instructor` 으로 `controller`를 `Index` 으로 `action` 1을 `id`; 이들은 경로 데이터 값입니다.
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> "? courseID 2021 =" 쿼리 문자열 값입니다. 전달 하는 경우에 모델 바인더가 작동을 `id` 쿼리 문자열 값으로:
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> Url에 의해 만들어집니다 `ActionLink` Razor 보기의 문입니다. 다음 코드에서를 `id` 하므로 일치 하는 기본 경로 매개 변수 `id` 경로 데이터에 추가 됩니다.
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> 다음 코드에서 `courseID` 쿼리 문자열로 추가 기본 경로 매개 변수와 일치 하지 않습니다.
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]


코드는 보기 모델의 인스턴스를 만들고 강사 목록에 배치하여 시작합니다. 코드에 대 한 즉시 로드를 지정 합니다 `Instructor.OfficeAssignment` 하며 `Instructor.Courses` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

두 번째 `Include` 메서드는 교육 코스를 로드 및 로드 되는 각 과정에 적용 되는 즉시 로드는 `Course.Department` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

이전에 설명한 대로 선행 로딩은 필요 하지 않지만 성능 향상을 위해 수행 됩니다. 뷰를 항상 필요 하므로 `OfficeAssignment` 효율적으로 동일한 쿼리에서 인출 하는 것이 엔터티를 합니다. `Course` 엔터티는 선행 로딩과 지연 로드 페이지가 없이 선택 된 강좌를 사용 하 여 더 자주 표시 되는 경우에 보다 이므로 웹 페이지에는 강사가 선택 된 경우에 필요 합니다.

강사의 ID를 선택한 경우 선택한 강사는 뷰 모델의 강사 목록에서 검색 됩니다. 보기 모델의 `Courses` 속성으로 로드 합니다 `Course` 해당 강사 엔터티 `Courses` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

합니다 `Where` 메서드는 컬렉션을 반환 하지만 조건 하나만 발생 하는 메서드를 전달 하는 예제의 `Instructor` 반환 되는 엔터티. 합니다 `Single` 메서드는 단일 컬렉션 변환 `Instructor` 해당 엔터티에 액세스할 수 있는 엔터티 `Courses` 속성입니다.

사용 된 [단일](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) 메서드 컬렉션을 아는 경우 컬렉션에서 항목을 하나만 갖습니다. `Single` 메서드에서 전달 된 컬렉션이 비어 있거나 둘 이상의 항목 경우 예외가 throw 됩니다. 대안은 [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), 기본 값을 반환 하는 (`null` 여기서) 컬렉션이 비어 있는 경우. 그러나이 경우 여전히 결과적으로 예외 (찾으려는 시도에서 `Courses` 속성을 `null` 참조), 예외 메시지에서 문제의 원인을 덜 명확 하 게 477860 및 합니다. 호출 하는 경우는 `Single` 메서드를 전달할 수도 있습니다에 `Where` 호출 하는 대신 조건은 `Where` 메서드 개별적으로:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

위 코드를 아래 코드 대신 사용합니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

다음으로 강좌를 선택한 경우 선택한 강좌가 보기 모델의 강좌 목록에서 검색됩니다. 보기 모델의 `Enrollments` 속성으로 로드 되는 `Enrollment` 해당 과정에서 엔터티 `Enrollments` 탐색 속성입니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a>강사 인덱스 뷰 수정

*Views\Instructor\Index.cshtml*, 기존 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

기존 코드에 다음 변경 내용을 만들었습니다.

- 모델 클래스를 `InstructorIndexData`로 변경했습니다.
- 페이지 제목을 **인덱스**에서 **강사**로 변경했습니다.
- 행 링크 열을 왼쪽으로 이동 합니다.
- 제거 된 **FullName** 열입니다.
- 추가 된 **Office** 표시 하는 열 `item.OfficeAssignment.Location` 경우에만 `item.OfficeAssignment` null이 아닙니다. (--0-또는-일대일 관계 이기 때문에 있을 수 없습니다 관련 `OfficeAssignment` 엔터티.) 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- 동적으로 추가 하는 추가 코드 `class="selectedrow"` 에 `tr` 선택한 강사의 요소입니다. 이 이전에 만든는 CSS 클래스를 사용 하 여 선택한 행의 배경색을 설정 합니다. (의 `valign` 특성 지정할 때 도움이 되며 다음 자습서에서 테이블에 다중 행 열을 추가 합니다.) 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- 새로 추가 `ActionLink` 레이블이 지정 된 **선택** 보낼 선택한 강사의 ID에 이르게 각 행에 있는 다른 링크를 바로 앞의 `Index` 메서드.

응용 프로그램을 실행 하 고 선택 합니다 **강사** 탭 합니다. 페이지에 표시 됩니다는 `Location` 관련 된 속성 `OfficeAssignment` 엔터티와 빈 테이블 셀 있을 때 관련 없는 `OfficeAssignment` 엔터티.

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

에 *Views\Instructor\Index.cshtml* 파일을 닫은 후 `table` (끝에 있는 요소 파일의)을 다음 강조 표시 된 코드를 추가 합니다. 이 강사가 선택 된 경우 강사와 관련 된 강좌의 목록을 표시 합니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

이 코드는 보기 모델의 `Courses` 속성을 읽어 강좌의 목록을 표시합니다. 또한 제공을 `Select` 의 선택된 된 강좌의 ID를 전송 하는 하이퍼링크를 `Index` 작업 메서드.

> [!NOTE]
> 합니다 *.css* 파일은 브라우저에서 캐시 됩니다. 응용 프로그램을 실행 하는 경우 변경 내용이 표시 되지 않으면, 하드 새로 고침을 수행 (CTRL 키를 누른 채 클릭 하는 **새로 고침** 단추 또는 ctrl+f5).


페이지를 실행 하 고 강사를 선택 합니다. 이제 선택된 강사에 할당된 강좌를 표시하는 표가 표시되고 각 강좌에 대해 할당된 부서의 이름이 표시됩니다.

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

방금 추가한 코드 블록 뒤에 다음 코드를 추가합니다. 해당 강좌가 선택된 경우에 강좌에 등록된 학생의 목록을 표시합니다.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

이 코드를 읽기는 `Enrollments` 과정에 등록 된 학생의 목록을 표시 하기 위해 보기 모델의 속성입니다.

페이지를 실행 하 고 강사를 선택 합니다. 그런 다음, 강좌를 선택하여 등록된 학생 및 해당 등급의 목록을 봅니다.

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a>명시적 로드를 추가합니다.

오픈 *InstructorController.cs* 하는 방법을 확인 `Index` 메서드는 선택한 과정에 대 한 등록의 목록을 가져옵니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

에 대 한 즉시 로드를 지정 하는 강사 목록을 검색할 때 합니다 `Courses` 탐색 속성 및는 `Department` 각 코스의 속성입니다. 추가한 다음 합니다 `Courses` 컬렉션 뷰 모델에 액세스 하려면 이제는 `Enrollments` 해당 컬렉션에 하나의 엔터티에서 탐색 속성입니다. 에 대해 즉시 로드를 지정 하지 않으므로 `Course.Enrollments` 탐색 속성이 해당 속성의 데이터를 지연 로드의 결과로 페이지에 표시 되 합니다.

다른 방법으로 코드를 변경 하지 않고 지연 로드를 사용 하지 않도록 설정한 경우는 `Enrollments` 속성 개수 등록 과정 없었습니다에 관계 없이 null이 될 것입니다. 로드 하는 경우에는 `Enrollments` 즉시 로드 또는 명시적 로드를 지정 해야 속성입니다. 즉시 로드를 수행 하는 방법을 이미 살펴보았습니다. 명시적 로드의 예를 보려면 대체 합니다 `Index` 명시적으로 로드 되는 다음 코드를 사용 하 여 메서드를 `Enrollments` 속성입니다. 변경 된 코드를 강조 표시 됩니다.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

선택한 후 `Course` 엔터티를 새 코드는 과정을 명시적으로 로드 `Enrollments` 탐색 속성:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

다음 사용자가 명시적으로 각 로드 하기 `Enrollment` 엔터티 관련 `Student` 엔터티:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

사용 하는 `Collection` 컬렉션 속성을 로드 하는 방법 엔터티 하나만 포함 하는 속성을 사용 하지만 `Reference` 메서드. 이제 강사 인덱스 페이지를 실행할 수 있습니다 하 고 데이터를 검색 하는 방법을 변경 했더라도 페이지에 표시 되는 항목의 차이가 표시 됩니다.

## <a name="summary"></a>요약

이제 모든 세 가지 방법 (지연, 즉시, 및 명시적) 탐색 속성에서 관련된 데이터 로드를 사용 했습니다. 다음 자습서에서는 관련된 데이터를 업데이트하는 방법을 설명합니다.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [다음](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
