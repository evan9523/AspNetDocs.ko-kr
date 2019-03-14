---
title: '자습서: ASP.NET MVC 웹앱에서 EF Core 시작'
description: 이는 Contoso University 샘플 애플리케이션을 처음부터 빌드하는 방법을 설명하는 일련의 자습서 중 첫 번째입니다.
author: rick-anderson
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/06/2019
ms.topic: tutorial
uid: data/ef-mvc/intro
ms.openlocfilehash: f7b557c8e560393ae886c46fad95c48ccbcc65b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043470"
---
# <a name="tutorial-get-started-with-ef-core-in-an-aspnet-mvc-web-app"></a>자습서: ASP.NET MVC 웹앱에서 EF Core 시작

[!INCLUDE [RP better than MVC](~/includes/RP-EF/rp-over-mvc.md)]

Contoso University 샘플 웹 애플리케이션은 EF(Entity Framework) Core 2.0 및 Visual Studio 2017을 사용하여 ASP.NET Core 2.2 MVC 웹 애플리케이션을 만드는 방법을 보여 줍니다.

샘플 애플리케이션은 가상 Contoso University의 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다. 이는 Contoso University 샘플 애플리케이션을 처음부터 빌드하는 방법을 설명하는 일련의 자습서 중 첫 번째입니다.

EF Core 2.0은 최신 버전의 EF이지만 EF 6.x의 모든 기능을 가지고 있지 않습니다. EF 6.x 및 EF Core 중에 선택하는 방법에 대한 내용은 [EF Core와  EF6.x 비교](/ef/efcore-and-ef6/)를 참조합니다. EF 6.x를 선택하는 경우 [이 자습서 시리즈의 이전 버전](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)을 참조하세요.

> [!NOTE]
> 이 자습서의 ASP.NET Core 1.1 버전의 경우 [PDF 형식에서 이 자습서의 VS 2017 업데이트 2 버전](https://webpifeed.blob.core.windows.net/webpifeed/Partners/efmvc1.1.pdf)을 참조하세요.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * ASP.NET Core MVC 웹앱 만들기
> * 사이트 스타일 설정
> * EF Core NuGet 패키지에 대해 알아보기
> * 데이터 모델 만들기
> * 데이터베이스 컨텍스트 만들기
> * SchoolContext 등록
> * 테스트 데이터로 DB 초기화
> * 컨트롤러 및 뷰 만들기
> * 데이터베이스 보기

## <a name="prerequisites"></a>전제 조건

[!INCLUDE [](~/includes/net-core-prereqs.md)]

## <a name="troubleshooting"></a>문제 해결

해결할 수 없는 문제가 발생한 경우 일반적으로 [완료된 프로젝트](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)와 코드를 비교하여 해결책을 찾을 수 있습니다. 일반적인 오류 목록 및 해결 방법은 [시리즈에서 마지막 자습서의 문제 해결 섹션](advanced.md#common-errors)을 참조하세요. 필요한 내용을 찾지 못한 경우 질문을 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 또는 [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core)에 대한 StackOverflow.com에 게시할 수 있습니다.

> [!TIP]
> 10 자습서의 시리즈이며, 각각은 이전 자습서에서 수행된 작업을 기반으로 합니다. 각 자습서를 성공적으로 완료한 후에 프로젝트 복사본의 저장을 고려합니다. 그런 다음, 문제가 발생한 경우 전체 시리즈의 처음으로 다시 이동하는 대신 이전 자습서부터 시작할 수 있습니다.

## <a name="contoso-university-web-app"></a>Contoso University 웹앱

이 자습서에서 빌드하는 애플리케이션은 간단한 대학 웹 사이트입니다.

사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다. 다음은 만들 몇 가지 화면입니다.

![학생 인덱스 페이지](intro/_static/students-index.png)

![학생 편집 페이지](intro/_static/student-edit.png)

자습서가 Entity Framework를 사용하는 방법에 주로 초점을 맞출 수 있도록 이 사이트의 UI 스타일은 기본 제공 템플릿에서 생성된 내용에 가깝게 유지되었습니다.

## <a name="create-aspnet-core-mvc-web-app"></a>ASP.NET Core MVC 웹앱 만들기

Visual Studio를 열고 "ContosoUniversity"라는 새로운 ASP.NET Core C# 웹 프로젝트를 만듭니다.

* **파일** 메뉴에서 **새로 만들기 > 프로젝트**를 선택합니다.

* 왼쪽 창에서 **설치됨 > Visual C# > 웹**을 선택합니다.

* **ASP.NET Core 웹 애플리케이션** 프로젝트 템플릿을 선택합니다.

* 이름으로 **ContosoUniversity**를 입력하고 **확인**을 클릭합니다.

  ![새 프로젝트 대화 상자](intro/_static/new-project2.png)

* **새 ASP.NET Core 웹 애플리케이션(.NET Core)** 대화 상자가 표시될 때까지 기다립니다.

  ![새 ASP.NET Core 프로젝트 대화 상자](intro/_static/new-aspnet2.png)

* **ASP.NET Core 2.2** 및 **웹 애플리케이션(Model-View-Controller)** 템플릿을 선택합니다.

  **참고:** 이 자습서에는 ASP.NET Core 2.2 및 EF Core 2.0 이상이 필요합니다.

* **인증**이 **인증 없음**으로 설정되었는지 확인합니다.

*  **확인**을 클릭합니다.

## <a name="set-up-the-site-style"></a>사이트 스타일 설정

몇 가지 간단한 변경 내용으로 사이트 메뉴, 레이아웃 및 홈 페이지를 설정합니다.

*Views/Shared/_Layout.cshtml*을 열고 다음과 같이 변경합니다.

* 모든 “ContosoUniversity”를 “Contoso University”로 변경합니다. 세 번 나옵니다.

* **정보**, **학생**, **강좌**, **강사** 및 **부서** 메뉴 항목을 추가하고 **개인 정보** 메뉴 항목을 삭제합니다.

변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[](intro/samples/cu/Views/Shared/_Layout.cshtml?highlight=6,32-36,51)]

*Views/Home/Index.cshtml*에서 다음 코드로 파일의 콘텐츠를 텍스트를 대체하여 ASP.NET 및 MVC에 대한 텍스트를 이 애플리케이션에 대한 텍스트로 바꿉니다.

[!code-cshtml[](intro/samples/cu/Views/Home/Index.cshtml)]

CTRL+F5 키를 눌러 프로젝트를 실행하거나 메뉴 모음에서 **디버그 > 디버깅하지 않고 시작**을 선택합니다. 이 자습서에서 만드는 페이지에 대한 탭이 포함된 홈페이지가 표시됩니다.

![Contoso University 홈페이지](intro/_static/home-page.png)

## <a name="about-ef-core-nuget-packages"></a>EF Core NuGet 패키지 정보

프로젝트에 EF Core 지원을 추가하려면 대상으로 지정하려는 데이터베이스 공급자를 설치합니다. 이 자습서에서는 SQL Server를 사용하며 공급자 패키지는 [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/)입니다. 이 패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있으므로 앱에 `Microsoft.AspNetCore.App` 패키지에 대한 패키지 참조가 있는 경우 패키지를 참조할 필요가 없습니다.

이 패키지 및 해당 종속성(`Microsoft.EntityFrameworkCore` 및 `Microsoft.EntityFrameworkCore.Relational`)은 EF에 대한 런타임 지원을 제공합니다. [마이그레이션](migrations.md) 자습서에서 나중에 도구 패키지를 추가합니다.

Entity Framework Core에 사용할 수 있는 다른 데이터베이스 공급자에 대한 정보는 [데이터베이스 공급자](/ef/core/providers/)를 참조하세요.

## <a name="create-the-data-model"></a>데이터 모델 만들기

다음으로 Contoso University 애플리케이션에 대한 엔터티 클래스를 만듭니다. 다음과 같은 세 가지 엔터티로 시작합니다.

![강좌-등록-학생 데이터 모델 다이어그램](intro/_static/data-model-diagram.png)

`Student` 및 `Enrollment` 엔터티 간에 일대다 관계가 있으며 `Course` 및 `Enrollment` 엔터티 간에 일대다 관계가 있습니다. 즉, 학생은 개수에 관계 없이 강좌에 등록될 수 있으며 강좌는 등록된 학생이 여러 명일 수 있습니다.

다음 섹션에서 이러한 엔터티 각각에 대한 클래스를 만듭니다.

### <a name="the-student-entity"></a>학생 엔터티

![학생 엔터티 다이어그램](intro/_static/student-entity.png)

*Models* 폴더에서 *Student.cs*라는 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

`ID` 속성은 이 클래스에 해당하는 데이터베이스 테이블의 기본 키 열이 됩니다. 기본적으로 Entity Framework는 `ID` 또는 `classnameID`로 명명된 속성을 기본 키로 해석합니다.

`Enrollments` 속성은 [탐색 속성](/ef/core/modeling/relationships)입니다. 탐색 속성은 이 엔터티와 관련된 다른 엔터티를 포함합니다. 이 경우 `Student entity`의 `Enrollments` 속성은 해당 `Student` 엔터티에 관련된 모든 `Enrollment` 엔터티를 포함합니다. 즉, 데이터베이스의 지정된 학생 행에 두 개의 관련된 등록 행(해당 StudentID 외래 키 열에 해당 학생의 기본 키 값을 포함하는 행)이 있는 경우 해당 `Student` 엔터티의 `Enrollments` 탐색 속성은 두 개의 `Enrollment` 엔터티를 포함합니다.

탐색 속성이 여러 엔터티를 포함할 수 있는 경우(다대다 또는 일대다 관계로), 해당 형식은 `ICollection<T>`와 같이 항목이 추가, 삭제 및 업데이트될 수 있는 목록이어야 합니다. `List<T>` 또는 `HashSet<T>`와 같은 형식 또는 `ICollection<T>`를 지정할 수 있습니다. `ICollection<T>`를 지정하는 경우 EF는 기본적으로 `HashSet<T>` 컬렉션을 만듭니다.

### <a name="the-enrollment-entity"></a>등록 엔터티

![등록 엔터티 다이어그램](intro/_static/enrollment-entity.png)

*Models* 폴더에서*Enrollment.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

`EnrollmentID` 속성은 기본 키가 됩니다. 이 엔터티는 `Student` 엔터티에서 본 것과 같이 자체적으로 `ID` 대신 `classnameID` 패턴을 사용합니다. 일반적으로 하나의 패턴을 선택하고 이를 데이터 모델 전체에서 사용합니다. 여기에서 변형은 패턴 중 하나를 사용할 수 있음을 보여 줍니다. [자습서의 뒷부분](inheritance.md)에서는 클래스 이름 없이 ID를 사용하여 더 손쉽게 데이터 모델에서 상속을 구현하는 방법을 알아봅니다.

`Grade` 속성은 `enum`입니다. `Grade` 형식 선언 뒤에 있는 물음표는 `Grade` 속성이 nullable이라는 것을 나타냅니다. Null인 등급은 0 등급과는 다릅니다. Null은 알려지지 않거나 아직 등록되지 않은 등급을 의미합니다.

`StudentID` 속성은 외래 키로, 해당 탐색 속성은 `Student`입니다. `Enrollment` 엔터티는 하나의 `Student` 엔터티와 연결되어 있으므로 속성은 단일 `Student` 엔터티만 포함할 수 있습니다(이전에 살펴본 여러 `Enrollment` 엔터티를 포함할 수 있는 `Student.Enrollments` 탐색 속성과 달리).

`CourseID` 속성은 외래 키로, 해당 탐색 속성은 `Course`입니다. `Enrollment` 엔터티는 하나의 `Course` 엔터티와 연결됩니다.

Entity Framework는 속성 이름이 `<navigation property name><primary key property name>`인 경우 외래 키 속성으로는 해석합니다(예: `Student` 엔터티의 기본 키가 `ID`이므로 `Student` 탐색 속성의 경우 `StudentID`). 외래 키 속성의 이름을 단순히 `<primary key property name>`으로 지정할 수 있습니다(예: `Course` 엔터티의 기본 키가 `CourseID`이므로 `CourseID`).

### <a name="the-course-entity"></a>강좌 엔터티

![강좌 엔터티 다이어그램](intro/_static/course-entity.png)

*Models* 폴더에서*Course.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

`Enrollments` 속성은 탐색 속성입니다. `Course` 엔터티는 `Enrollment` 엔터티의 개수와 관련이 있을 수 있습니다.

이 시리즈의 [이후의 자습서](complex-data-model.md)에서 `DatabaseGenerated` 특성에 대해 자세히 설명합니다. 기본적으로 이 특성을 통해 생성하는 데이터베이스를 갖는 대신 강좌에 대한 기본 키를 입력할 수 있습니다.

## <a name="create-the-database-context"></a>데이터베이스 컨텍스트 만들기

특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스는 데이터베이스 컨텍스트 클래스입니다. `Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다. 코드에서 데이터 모델에 포함되는 엔터티를 지정합니다. 특정 Entity Framework 동작을 사용자 지정할 수도 있습니다. 이 프로젝트에서 클래스 이름은 `SchoolContext`로 지정됩니다.

프로젝트 폴더에서 *Data*라는 이름의 폴더를 만듭니다.

*Data* 폴더에서 *SchoolContext.cs*라는 새로운 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

이 코드는 각 엔터티 집합에 대한 `DbSet` 속성을 만듭니다. Entity Framework 용어에서 엔터티 집합은 일반적으로 데이터베이스 테이블에 해당하고 엔터티는 테이블의 행에 해당합니다.

`DbSet<Enrollment>` 및 `DbSet<Course>` 문을 생략할 수 있으며 이는 동일하게 작동합니다. `Student` 엔터티는 `Enrollment` 엔터티를 참조하고 `Enrollment` 엔터티는 `Course` 엔터티를 참조하기 때문에 Entity Framework는 이를 암시적으로 포함합니다.

데이터베이스가 만들어지면 EF는 `DbSet` 속성 이름과 동일한 이름을 갖는 테이블을 만듭니다. 컬렉션에 대한 속성 이름은 일반적으로 복수형이지만(Student보다는 Students) 개발자는 테이블 이름을 복수화할지 여부에 대해 동의하지 않습니다. 이러한 자습서의 경우 DbContext에서 단수 테이블 이름을 지정하여 기본 동작을 재정의합니다. 이렇게 하려면 마지막 DbSet 속성 뒤에 강조 표시된 다음 코드를 추가합니다.

[!code-csharp[](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-schoolcontext"></a>SchoolContext 등록

ASP.NET Core는 기본적으로 [종속성 주입](../../fundamentals/dependency-injection.md)을 구현합니다. 서비스(예: EF 데이터베이스 컨텍스트)는 애플리케이션 시작 중에 종속성 주입에 등록됩니다. 이러한 서비스(예: MVC 컨트롤러)가 필요한 구성 요소에는 생성자 매개 변수를 통해 이러한 서비스가 제공됩니다. 이 자습서의 뒷부분에서 컨텍스트 인스턴스를 가져오는 컨트롤러 생성자 코드를 볼 수 있습니다.

`SchoolContext`를 서비스로 등록하려면 *Startup.cs*를 열고 강조 표시된 줄을 `ConfigureServices` 메서드에 추가합니다.

[!code-csharp[](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

`DbContextOptionsBuilder` 개체에서 메서드를 호출하여 연결 문자열의 이름을 컨텍스트에 전달합니다. 로컬 개발의 경우 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index)은 *appsettings.json* 파일에서 연결 문자열을 읽습니다.

`ContosoUniversity.Data` 및 `Microsoft.EntityFrameworkCore` 네임스페이스에 대해 `using` 문을 추가한 다음, 프로젝트를 빌드합니다.

[!code-csharp[](intro/samples/cu/Startup.cs?name=snippet_Usings)]

*appsettings.json* 파일을 열고 다음 예제에 표시된 대로 연결 문자열을 추가합니다.

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

### <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

연결 문자열은 SQL Server LocalDB 데이터베이스를 지정합니다. LocalDB는 프로덕션 사용이 아닌 애플리케이션 개발용으로 고안된 SQL Server Express 데이터베이스 엔진의 경량 버전입니다. LocalDB는 요청 시 시작하고 사용자 모드에서 실행되므로 복잡한 구성이 없습니다. 기본적으로 LocalDB는 *.mdf* 데이터베이스 파일을 `C:/Users/<user>` 디렉터리에 만듭니다.

## <a name="initialize-db-with-test-data"></a>테스트 데이터로 DB 초기화

Entity Framework에서 빈 데이터베이스를 만듭니다. 이 섹션에서는 테스트 데이터로 채우기 위해 데이터베이스를 만든 후 호출되는 메서드를 작성합니다.

여기에서 `EnsureCreated` 메서드를 사용하여 자동으로 데이터베이스를 만듭니다. [이후의 자습서](migrations.md)에서는 데이터베이스를 삭제하고 다시 작성하는 대신 데이터베이스 스키마를 변경하도록 Code First 마이그레이션을 사용하여 모델 변경 내용을 처리하는 방법을 알아봅니다.

*Data* 폴더에서 *DbInitializer.cs*라는 새 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다. 이로 인해 필요할 때 데이터베이스가 만들어지며 테스트 데이터를 새 데이터베이스로 로드합니다.

[!code-csharp[](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

코드는 데이터베이스에 학생이 있는지를 확인하고 없는 경우 데이터베이스가 새 것이며 테스트 데이터로 시드되어야 한다고 가정합니다. `List<T>` 컬렉션이 아닌 배열에 테스트 데이터를 로드하여 성능을 최적화합니다.

*Program.cs*에서 애플리케이션 시작 시에 다음을 수행하는 `Main` 메서드를 수정합니다.

* 종속성 주입 컨테이너에서 데이터베이스 컨텍스트 인스턴스를 가져옵니다.
* 컨텍스트를 전달하는 시드 메서드를 호출합니다.
* 시드 메서드가 완료되면 컨텍스트를 삭제합니다.

[!code-csharp[](intro/samples/cu/Program.cs?name=snippet_Seed&highlight=3-20)]

`using` 문을 추가합니다.

[!code-csharp[](intro/samples/cu/Program.cs?name=snippet_Usings)]

이전 자습서에서는 *Startup.cs*의 `Configure` 메서드에서 유사한 코드를 볼 수 있습니다. 요청 파이프라인을 설정하는 데에만 `Configure` 메서드를 사용하는 것이 좋습니다. 애플리케이션 시작 코드는 `Main` 메서드에 속합니다.

이제 애플리케이션을 처음으로 실행하면 데이터베이스가 생성되고 테스트 데이터로 시드됩니다. 데이터 모델을 변경할 때마다 데이터베이스를 삭제하고, 시드 메서드를 업데이트하고, 동일한 방식으로 새 데이터베이스를 사용하여 새로 시작합니다. 이후의 자습서에서는 데이터 모델이 변경될 때 데이터베이스를 삭제하고 다시 작성하지 않고 데이터베이스를 수정하는 방법을 볼 수 있습니다.

## <a name="create-controller-and-views"></a>컨트롤러 및 뷰 만들기

다음으로 Visual Studio에서 스캐폴딩 엔진을 사용하여 EF에서 데이터를 쿼리하고 저장하는 데 사용하는 MVC 컨트롤러 및 보기를 추가합니다.

CRUD 작업 메서드와 보기를 자동으로 만드는 작업을 스캐폴딩이라고 합니다. 스캐폴딩은 사용자 고유의 요구 사항에 맞게 수정할 수 있는 스캐폴드된 코드가 시작 지점인 코드 생성과 다릅니다. 반면에 일반적으로 생성된 코드를 수정하지 않습니다. 생성된 코드를 사용자 지정해야 하는 경우 partial 클래스를 사용하거나 항목이 변경될 때 코드를 다시 생성합니다.

* **솔루션 탐색기**에서 **컨트롤러** 폴더를 마우스 오른쪽 단추로 클릭하고 **추가 -> 스캐폴드 항목 새로 만들기**를 선택합니다.

**MVC 종속성 추가** 대화 상자가 나타나는 경우:

* [Visual Studio를 최신 버전으로 업데이트합니다](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017). Visual Studio 15.5 이전 버전이 이 대화 상자를 표시합니다.
* 업데이트할 수 없는 경우 **추가**를 선택한 다음 컨트롤러 추가 단계를 다시 따릅니다.

* **스캐폴드 추가** 대화 상자에서:

  * **Entity Framework를 사용하며 뷰가 포함된 MVC 컨트롤러**를 선택합니다.

  * **추가**를 클릭합니다. **Entity Framework를 사용하여 뷰 포함 MVC 컨트롤러 추가** 대화 상자가 표시됩니다.

    ![학생 스캐폴드](intro/_static/scaffold-student2.png)

  * **모델 클래스**에서 **학생**을 선택합니다.

  * **데이터 컨텍스트 클래스**에서 **SchoolContext**를 선택합니다.

  * 기본값 **StudentsController**를 이름으로 허용합니다.

  * **추가**를 클릭합니다.

  **추가**를 클릭하면 Visual Studio 스캐폴딩 엔진은 *StudentsController.cs* 파일과 컨트롤러와 작동하는 뷰 집합(*.cshtml* 파일)을 만듭니다.

(스캐폴딩 엔진은 이 자습서의 앞에서 수행한 것과 같이 수동으로 먼저 만들지 않은 경우 데이터베이스 컨텍스트를 만들 수도 있습니다. **데이터 컨텍스트 클래스**의 오른쪽에 있는 더하기 기호를 클릭하여 **컨트롤러 추가** 상자에 새 컨텍스트 클래스를 지정할 수 있습니다.  그런 다음, Visual Studio는 `DbContext` 클래스 뿐만 아니라 컨트롤러와 뷰도 만듭니다.)

컨트롤러는 `SchoolContext`를 생성자 매개 변수로 사용합니다.

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Context&highlight=5,7,9)]

ASP.NET Core 종속성 주입은 `SchoolContext`의 인스턴스를 컨트롤러에 전달하는 것을 담당합니다. 이전에 *Startup.cs* 파일에서 구성했습니다.

컨트롤러는 데이터베이스에 모든 학생을 표시하는 `Index` 작업 메서드를 포함합니다. 메서드는 데이터베이스 컨텍스트 인스턴스의 `Students` 속성을 읽어 학생 엔터티 집합에서 학생의 목록을 가져옵니다.

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex&highlight=3)]

이 자습서의 뒷부분에 나오는 이 코드에서 비동기 프로그래밍 요소에 대해 알아봅니다.

*Views/Students/Index.cshtml* 보기가 테이블에 이 목록을 표시합니다.

[!code-cshtml[](intro/samples/cu/Views/Students/Index1.cshtml)]

CTRL+F5 키를 눌러 프로젝트를 실행하거나 메뉴 모음에서 **디버그 > 디버깅하지 않고 시작**을 선택합니다.

학생 탭을 클릭하여 `DbInitializer.Initialize` 메서드가 삽입된 테스트 데이터를 봅니다. 브라우저 창의 폭에 따라 페이지의 맨 위에 `Student` 탭 링크가 표시되거나 링크를 보기 위해 오른쪽 맨 위의 탐색 아이콘을 클릭해야 합니다.

![좁은 Contoso University 홈페이지](intro/_static/home-page-narrow.png)

![학생 인덱스 페이지](intro/_static/students-index.png)

## <a name="view-the-database"></a>데이터베이스 보기

애플리케이션을 시작했을 때 `DbInitializer.Initialize` 메서드는 `EnsureCreated`를 호출합니다. EF는 데이터베이스가 없는 것을 확인하고 하나를 만들었습니다. 그런 다음, `Initialize` 메서드 코드의 나머지 부분은 데이터베이스를 데이터로 채웠습니다. **SQL Server 개체 탐색기**(SSOX)를 사용하여 Visual Studio에서 데이터베이스를 볼 수 있습니다.

브라우저를 닫습니다.

SSOX 창이 열려 있지 않은 경우 Visual Studio의 **보기** 메뉴에서 선택합니다.

SSOX에서 **(localdb) \MSSQLLocalDB > 데이터베이스**를 클릭한 다음, *appsettings.json* 파일의 연결 문자열에 있는 데이터베이스 이름에 대한 항목을 클릭합니다.

**테이블** 노드를 확장하여 데이터베이스의 테이블을 봅니다.

![SSOX의 테이블](intro/_static/ssox-tables.png)

**학생** 테이블을 마우스 오른쪽 단추로 클릭하고, **데이터 보기**를 클릭하여 만들어진 열 및 테이블에 삽입된 행을 봅니다.

![SSOX의 학생 테이블](intro/_static/ssox-student-table.png)

<em>.mdf</em> 및 <em>.ldf</em> 데이터베이스 파일은 <em>C:\Users\\<yourusername></em> 폴더에 있습니다.

앱 시작 시 실행되는 이니셜라이저 메서드에서 `EnsureCreated`를 호출하기 때문에 이제 `Student` 클래스에 변경 내용을 만들고, 데이터베이스를 삭제하고, 애플리케이션을 다시 시작할 수 있으며, 데이터베이스는 변경 내용에 맞도록 자동으로 다시 생성됩니다. 예를 들어 `EmailAddress` 속성을 `Student` 클래스에 추가하는 경우 다시 만들어진 테이블에 새 `EmailAddress` 열이 표시됩니다.

## <a name="conventions"></a>규칙

Entity Framework에서 전체 데이터베이스를 만들 수 있도록 작성해야 했던 코드의 양은 규칙의 사용 또는 Entity Framework에서 만드는 가정으로 인해 최소입니다.

* `DbSet` 속성의 이름은 테이블 이름으로 사용됩니다. `DbSet` 속성에서 참조하지 않는 엔터티의 경우 엔터티 클래스 이름이 테이블 이름으로 사용됩니다.

* 엔터티 속성 이름은 열 이름에 사용됩니다.

* ID 또는 classnameID로 명명된 엔터티 속성은 기본 키 속성으로 인식됩니다.

* 속성 이름이 *<navigation property name><primary key property name>* 인 경우 외래 키 속성으로는 해석됩니다(예: `Student` 엔터티의 기본 키가 `ID`이므로 `Student` 탐색 속성의 경우 `StudentID`). 외래 키 속성의 이름을 단순히 *<primary key property name>* 으로 지정할 수 있습니다(예: `Enrollment` 엔터티의 기본 키가 `EnrollmentID`이므로 `EnrollmentID`).

기본 동작은 재정의될 수 있습니다. 예를 들어 이 자습서의 앞부분에서 본 것처럼 테이블 이름을 명시적으로 지정할 수 있습니다. 또한 이 시리즈의 [이후의 자습서](complex-data-model.md)에서 볼 수 있듯이 열 이름을 설정하고 기본 키 또는 외래 키로 속성을 설정할 수 있습니다.

## <a name="asynchronous-code"></a>비동기 코드

비동기 프로그래밍은 ASP.NET Core 및 EF Core에 대한 기본 모드입니다.

웹 서버에는 사용할 수 있는 스레드 수가 제한적이며, 로드 양이 많은 상황에서는 사용 가능한 모든 스레드가 사용될 수 있습니다. 이 경우 서버는 스레드가 해제될 때까지 새 요청을 처리할 수 없습니다. 동기 코드를 사용하면 I/O 완료를 대기하느라 작업을 실제로 수행하지 않는 동안에 많은 스레드가 정체될 수 있습니다. 비동기 코드를 사용하면 프로세스가 I/O 완료를 대기할 때 다른 요청을 처리하는 데 사용하도록 해당 스레드가 서버에서 해제됩니다. 따라서 비동기 코드를 사용하면 서버 리소스를 더 효율적으로 사용할 수 있으며 서버가 지연 없이 더 많은 트래픽을 처리할 수 있습니다.

비동기 코드는 런타임 시 약간의 오버헤드를 도입하지만 트래픽이 높은 상황에서는 잠재적 성능 향상이 상당한 반면, 트래픽이 낮은 상황의 경우 성능 저하는 미미합니다.

다음 코드에서 `async` 키워드, `Task<T>` 반환 값, `await` 키워드 및 `ToListAsync` 메서드는 비동기적으로 코드 실행을 수행합니다.

[!code-csharp[](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex)]

* `async` 키워드는 컴파일러에서 메서드 본문의 부분에 대한 콜백을 생성하고 반환되는 `Task<IActionResult>` 개체를 자동으로 만들도록 합니다.

* 반환 형식 `Task<IActionResult>`는 `IActionResult` 형식의 결과와 함께 진행 중인 작업을 나타냅니다.

* `await` 키워드로 인해 컴파일러는 메서드를 두 부분으로 분할합니다. 첫 번째 부분은 비동기적으로 시작되는 작업을 종료합니다. 두 번째 부분은 작업이 완료될 때 호출되는 콜백 메서드에 배치됩니다.

* `ToListAsync`는 `ToList` 확장 메서드의 비동기 버전입니다.

Entity Framework를 사용하는 비동기 코드를 작성할 때 고려해야 할 몇 가지 사항은 다음과 같습니다.

* 쿼리 또는 명령을 데이터베이스에 보내는 명령문만 비동기적으로 실행됩니다. 예를 들어 `ToListAsync`, `SingleOrDefaultAsync` 및 `SaveChangesAsync`를 포함합니다. 예를 들어 `var students = context.Students.Where(s => s.LastName == "Davolio")`와 같은 `IQueryable`을 변경하는 명령문은 포함되지 않습니다.

* EF 컨텍스트는 스레드로부터 안전하지 않습니다. 동시에 여러 작업을 수행하지 마십시오. 비동기 EF 메서드를 호출하는 경우 항상 `await` 키워드를 사용합니다.

* 비동기 코드의 성능 이점을 활용하려는 경우 사용 중인(예: 페이징) 라이브러리 패키지 또한 쿼리를 데이터베이스에 전송하도록 하는 Entity Framework 메서드를 호출하는 경우 비동기를 사용하는지 확인합니다.

.NET에서의 비동기 프로그래밍에 대한 자세한 내용은 [비동기 개요](/dotnet/articles/standard/async)를 참조하세요.

## <a name="get-the-code"></a>코드 가져오기

[완성된 애플리케이션을 다운로드하거나 확인합니다.](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * ASP.NET Core MVC 웹앱 만들기
> * 사이트 스타일 설정
> * EF Core NuGet 패키지에 대해 알아보기
> * 데이터 모델 만들기
> * 데이터베이스 컨텍스트 만들기
> * SchoolContext 등록
> * 테스트 데이터로 DB 초기화
> * 컨트롤러 및 뷰 만들기
> * 데이터베이스 보기

다음 자습서에서는 기본 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 수행하는 방법을 배웁니다.

기본 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 수행하는 방법을 알아보려면 다음 문서로 진행합니다.
> [!div class="nextstepaction"]
> [기본 CRUD 기능 구현](crud.md)
