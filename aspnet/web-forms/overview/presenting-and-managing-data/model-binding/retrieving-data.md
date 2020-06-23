---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 상호 작용이 더 간편 하 게-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: d5f1982196c5985b001ca42c2711174e036bb1ec
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240750"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a>모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시

> 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource)를 처리 하는 것 보다 데이터 상호 작용이 보다 간단 하 게 진행 됩니다. 이 시리즈는 소개 자료로 시작 하 고 이후 자습서에서 보다 고급 개념으로 이동 합니다.
> 
> 모델 바인딩 패턴은 모든 데이터 액세스 기술에 적용 됩니다. 이 자습서에서는 Entity Framework를 사용 하지만 가장 친숙 한 데이터 액세스 기술을 사용할 수 있습니다. GridView, ListView, DetailsView 또는 FormView 컨트롤과 같은 데이터 바인딩된 서버 컨트롤에서 데이터를 선택, 업데이트, 삭제 및 만드는 데 사용할 메서드의 이름을 지정 합니다. 이 자습서에서는 SelectMethod의 값을 지정 합니다. 
> 
> 이 메서드 내에서 데이터를 검색 하는 논리를 제공 합니다. 다음 자습서에서는 UpdateMethod, DeleteMethod 및 InsertMethod에 대 한 값을 설정 합니다.
>
> 전체 프로젝트는 c # 또는 Visual Basic에서 [다운로드할](https://go.microsoft.com/fwlink/?LinkId=286116) 수 있습니다. 다운로드 가능한 코드는 Visual Studio 2012 이상에서 작동 합니다. 이 자습서에 표시 된 visual studio 2017 템플릿과 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.
> 
> 이 자습서에서는 Visual Studio에서 응용 프로그램을 실행 합니다. 또한 호스팅 공급자에 응용 프로그램을 배포 하 고 인터넷을 통해 사용할 수 있도록 설정할 수 있습니다. Microsoft는에서 최대 10 개의 웹 사이트에 대 한 무료 웹 호스팅을 제공 합니다.  
> [무료 Azure 평가판 계정](https://azure.microsoft.com/free/dotnet/). Visual Studio 웹 프로젝트를 Azure App Service Web Apps에 배포 하는 방법에 대 한 자세한 내용은 [Visual studio 시리즈를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md) 를 참조 하세요. 또한이 자습서에서는 Entity Framework Code First 마이그레이션 사용 하 여 SQL Server 데이터베이스를 Azure SQL Database에 배포 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> - Microsoft Visual Studio 2017 또는 Microsoft Visual Studio Community 2017
>   
> 이 자습서는 Visual Studio 2012 및 Visual Studio 2013 에서도 작동 하지만 사용자 인터페이스와 프로젝트 템플릿에는 약간의 차이가 있습니다.

## <a name="what-youll-build"></a>빌드할 내용

이 자습서에서는 다음을 수행합니다.

* 강좌에 등록 된 학생 들과 대학을 반영 하는 데이터 개체 작성
* 개체에서 데이터베이스 테이블 작성
* 테스트 데이터로 데이터베이스 채우기
* 웹 폼에 데이터 표시

## <a name="create-the-project"></a>프로젝트 만들기

1. Visual Studio 2017에서 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 프로젝트를 **만듭니다.**

   ![프로젝트 만들기](retrieving-data/_static/image19.png)

2. **확인**을 선택합니다. 템플릿을 선택 하는 대화 상자가 나타납니다.

   ![web forms 선택](retrieving-data/_static/image3.png)

3. **Web Forms** 템플릿을 선택 합니다. 

4. 필요한 경우 **개별 사용자 계정**에 대 한 인증을 변경 합니다. 

5. **확인**을 선택하여 프로젝트를 만듭니다.

## <a name="modify-site-appearance"></a>사이트 모양 수정

   사이트 모양을 사용자 지정 하려면 몇 가지 사항을 변경 해야 합니다. 
   
   1. Site.master 파일을 엽니다.
   
   2. 제목을 변경 하 여 **내 ASP.NET 응용 프로그램이**아닌 **Contoso 대학** 을 표시 합니다.

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. 헤더 텍스트를 **응용 프로그램 이름** 에서 **Contoso 대학**으로 변경 합니다.

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. 탐색 헤더 링크를 적절 한 사이트에 대 한 링크를 변경 합니다. 
   
      **및에 대 한** 링크를 제거 **하 고 대신** 만들 **학생** 페이지에 연결 합니다.

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. Site.master를 저장 합니다.

## <a name="add-a-web-form-to-display-student-data"></a>학생 데이터를 표시 하는 web form 추가

   1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** , **새 항목**을 차례로 선택 합니다. 
   
   2. **새 항목 추가** 대화 상자에서 **마스터 페이지 템플릿을 사용 하 여 웹 양식을** 선택 하 고 이름을 **학생과 .aspx**로 바꿉니다.

      ![페이지 만들기](retrieving-data/_static/image5.png)

   3. **추가**를 선택합니다.
   
   4. 웹 양식의 마스터 페이지에서 **site.master**를 선택 합니다.
   
   5. **확인**을 선택합니다.

## <a name="add-the-data-model"></a>데이터 모델 추가

**모델** 폴더에서 이름이 **UniversityModels.cs**인 클래스를 추가 합니다.

   1. **모델**을 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**을 차례로 선택 합니다. **새 항목 추가** 대화 상자가 나타납니다.

   2. 왼쪽 탐색 메뉴에서 **코드**, **클래스**를 차례로 선택 합니다.

      ![모델 클래스 만들기](retrieving-data/_static/image20.png)

   3. 클래스 이름을 **UniversityModels.cs** 로 하 고 **추가**를 선택 합니다.

      이 파일에서 `SchoolContext` ,, `Student` `Enrollment` 및 클래스를 다음과 `Course` 같이 정의 합니다.

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      `SchoolContext`클래스는 `DbContext` 데이터베이스 연결 및 데이터 변경 내용을 관리 하는에서 파생 됩니다.

      클래스에서 `Student` , 및 속성에 적용 되는 특성을 확인 `FirstName` `LastName` `Year` 합니다. 이 자습서에서는 이러한 특성을 사용 하 여 데이터 유효성 검사를 수행 합니다. 코드를 단순화 하기 위해 이러한 속성만 데이터 유효성 검사 특성으로 표시 됩니다. 실제 프로젝트에서는 유효성 검사가 필요한 모든 속성에 유효성 검사 특성을 적용 합니다.

   4. UniversityModels.cs을 저장 합니다.

## <a name="set-up-the-database-based-on-classes"></a>클래스를 기반으로 데이터베이스를 설정 합니다.

이 자습서에서는 [Code First 마이그레이션](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) 를 사용 하 여 개체와 데이터베이스 테이블을 만듭니다. 이러한 테이블에는 학생 및 해당 과정에 대 한 정보가 저장 됩니다.

   1. **도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.

   2. **패키지 관리자 콘솔**에서 다음 명령을 실행 합니다.  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      명령이 성공적으로 완료 되 면 마이그레이션 사용 이라는 메시지가 나타납니다.

      ![마이그레이션 사용](retrieving-data/_static/image8.png)

      *Configuration.cs* 라는 파일이 생성 된 것을 확인할 수 있습니다. 클래스에는 `Configuration` `Seed` 데이터베이스 테이블을 테스트 데이터로 미리 채울 수 있는 메서드가 있습니다.

## <a name="pre-populate-the-database"></a>데이터베이스 미리 채우기

   1. Configuration.cs를 엽니다.
   
   2. `Seed` 메서드에 다음 코드를 추가합니다. 또한 `using` 네임 스페이스에 대 한 문을 추가 `ContosoUniversityModelBinding. Models` 합니다.

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. Configuration.cs을 저장 합니다.

   4. 패키지 관리자 콘솔에서 명령 **추가-마이그레이션 초기**를 실행 합니다.

   5. **업데이트-데이터베이스**명령을 실행 합니다.

      이 명령을 실행할 때 예외가 발생 하면 `StudentID` 및 `CourseID` 값이 메서드 값과 다를 수 있습니다 `Seed` . 이러한 데이터베이스 테이블을 열고 및에 대 한 기존 값을 찾습니다 `StudentID` `CourseID` . 테이블 시드를 위해 코드에 해당 값을 추가 `Enrollments` 합니다.

## <a name="add-a-gridview-control"></a>GridView 컨트롤 추가

채워진 데이터베이스 데이터를 사용 하 여 이제 해당 데이터를 검색 하 고 표시할 수 있습니다. 

1. 학생과 .aspx를 엽니다.

2. `MainContent`자리 표시자를 찾습니다. 해당 자리 표시자 내에서이 코드를 포함 하는 **GridView** 컨트롤을 추가 합니다.

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   참고 사항:
   * GridView 요소의 속성에 설정 된 값을 확인 합니다 `SelectMethod` . 이 값은 다음 단계에서 만드는 GridView 데이터를 검색 하는 데 사용 되는 메서드를 지정 합니다. 
   
   * `ItemType`속성은 `Student` 앞에서 만든 클래스로 설정 됩니다. 이 설정을 사용 하면 태그의 클래스 속성을 참조할 수 있습니다. 예를 들어 클래스에는 `Student` 라는 컬렉션이 있습니다 `Enrollments` . 를 사용 하 여 `Item.Enrollments` 해당 컬렉션을 검색 한 다음 [LINQ 구문을](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) 사용 하 여 각 학생의 등록 크레딧 합계를 검색할 수 있습니다.
   
3. 학생 .aspx를 저장 합니다.

## <a name="add-code-to-retrieve-data"></a>데이터를 검색 하는 코드 추가

   학생 코드 숨김이 파일에서 값에 대해 지정 된 메서드를 추가 합니다 `SelectMethod` . 
   
   1. Students.aspx.cs를 엽니다.
   
   2. `using`및 네임 스페이스에 대 한 문을 추가 `ContosoUniversityModelBinding. Models` `System.Data.Entity` 합니다.

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. 에 대해 지정한 메서드를 추가 합니다 `SelectMethod` .

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      `Include`절은 쿼리 성능을 향상 시키지만 반드시 필요한 것은 아닙니다. 절이 없으면 `Include` 데이터는 [*지연 로드*](https://en.wikipedia.org/wiki/Lazy_loading)를 사용 하 여 검색 되며,이는 관련 데이터가 검색 될 때마다 데이터베이스에 별도의 쿼리를 전송 하는 작업을 포함 합니다. 절을 사용 하면 `Include` *즉시 로드*를 사용 하 여 데이터를 검색 합니다. 즉, 단일 데이터베이스 쿼리에서 모든 관련 데이터를 검색 합니다. 관련 데이터가 사용 되지 않는 경우 더 많은 데이터가 검색 되기 때문에 즉시 로드 효율성이 떨어집니다. 그러나이 경우에는 각 레코드에 대해 관련 데이터가 표시 되기 때문에 즉시 로드는 최상의 성능을 제공 합니다.

      관련 데이터를 로드할 때의 성능 고려 사항에 대 한 자세한 내용은 [ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련 데이터 읽기](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 문서의 **지연, 즉시 및 명시적 로드** 섹션을 참조 하세요.

      기본적으로 데이터는 키로 표시 된 속성의 값을 기준으로 정렬 됩니다. `OrderBy`다른 정렬 값을 지정 하는 절을 추가할 수 있습니다. 이 예제에서는 기본 속성을 `StudentID` 정렬에 사용 합니다. [데이터 정렬, 페이징 및 필터링](sorting-paging-and-filtering-data.md) 아티클에서 사용자가 정렬할 열을 선택할 수 있습니다.
 
   4. Students.aspx.cs을 저장 합니다.

## <a name="run-your-application"></a>애플리케이션 실행 

웹 응용 프로그램 (**F5**)을 실행 하 고 **학생** 페이지로 이동 하 여 다음을 표시 합니다.

   ![데이터 표시](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a>모델 바인딩 메서드 자동 생성

이 자습서 시리즈를 통해 작업할 때 자습서의 코드를 프로젝트에 간단 하 게 복사할 수 있습니다. 그러나이 방법의 한 가지 단점은 Visual Studio에서 제공 하는 기능을 인식 하 여 모델 바인딩 메서드에 대 한 코드를 자동으로 생성 하는 것이 아니라는 것입니다. 사용자 고유의 프로젝트에서 작업 하는 경우 자동 코드 생성을 통해 시간을 절약 하 고 작업을 구현 하는 방법을 파악할 수 있습니다. 이 단원에서는 자동 코드 생성 기능에 대해 설명 합니다. 이 섹션은 참고용 으로만 제공 되며 프로젝트에서 구현 해야 하는 코드는 포함 하지 않습니다. 

`SelectMethod`태그 코드에서,, 또는 속성에 대 한 값을 설정할 때 `UpdateMethod` `InsertMethod` `DeleteMethod` **새 메서드 만들기** 옵션을 선택할 수 있습니다.

![메서드 만들기](retrieving-data/_static/image18.png)

Visual Studio는 적절 한 시그니처를 사용 하 여 코드 숨김으로 메서드를 만들 뿐만 아니라 작업을 수행 하기 위한 구현 코드도 생성 합니다. `ItemType`자동 코드 생성 기능을 사용 하기 전에 먼저 속성을 설정 하는 경우 생성 된 코드는 해당 형식을 작업에 사용 합니다. 예를 들어 속성을 설정할 때 `UpdateMethod` 다음 코드가 자동으로 생성 됩니다.

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

이 코드는 프로젝트에 추가할 필요가 없습니다. 다음 자습서에서는 새 데이터를 업데이트, 삭제 및 추가 하기 위한 메서드를 구현 합니다.

## <a name="summary"></a>요약

이 자습서에서는 데이터 모델 클래스를 만들고 해당 클래스에서 데이터베이스를 생성 했습니다. 데이터베이스 테이블을 테스트 데이터로 채웠습니다. 모델 바인딩을 사용 하 여 데이터베이스에서 데이터를 검색 한 다음 GridView에 데이터를 표시 했습니다.

이 시리즈의 다음 [자습서](updating-deleting-and-creating-data.md) 에서는 데이터 업데이트, 삭제 및 만들기를 사용 하도록 설정 합니다.

> [!div class="step-by-step"]
> [다음](updating-deleting-and-creating-data.md)
