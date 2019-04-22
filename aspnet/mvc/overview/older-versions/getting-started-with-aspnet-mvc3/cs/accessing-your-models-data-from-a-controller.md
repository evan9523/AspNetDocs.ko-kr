---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
title: 컨트롤러 (C#)에서 모델의 데이터에 액세스 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 002ada5c-f114-47ab-a441-57dbdb728ea0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: a2e2957ffe766282f127b6fb537af00673aa440f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59389845"
---
# <a name="accessing-your-models-data-from-a-controller-c"></a>컨트롤러에서 모델의 데이터에 액세스(C#)

[Rick Anderson]((https://twitter.com/RickAndMSFT))

> > [!NOTE]
> > 이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다. 보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. 시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다. 다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.
> 
> C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다. [C# 버전 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic을 원한다 면으로 전환 합니다 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 이 자습서의 합니다.

이 섹션에서는 새 만듭니다 `MoviesController` 클래스 및 영화 데이터를 검색 하 고 뷰 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다. 계속 하기 전에 응용 프로그램을 작성 해야 합니다.

마우스 오른쪽 단추로 클릭 합니다 *컨트롤러* 폴더를 만들어 새 `MoviesController` 컨트롤러입니다. 다음 옵션을 선택합니다.

- 컨트롤러 이름: **MoviesController**. (기본값입니다. )
- 템플릿: **읽기/쓰기 동작 및 Entity Framework를 사용 하 여 뷰를 사용 하 여 컨트롤러**합니다.
- 모델 클래스: **Movie (MvcMovie.Models)** 합니다.
- 데이터 컨텍스트 클래스: **(MvcMovie.Models) MovieDBContext**합니다.
- 레이아웃: **Razor (CSHTML)** 합니다. (기본값입니다.)

[![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image2.png "AddScaffoldedMovieController")](accessing-your-models-data-from-a-controller/_static/image1.png)

**추가**를 클릭합니다. Visual Web Developer는 다음 파일 및 폴더를 만듭니다.

- *MoviesController.cs* 프로젝트의 파일 *컨트롤러* 폴더입니다.
- A *영화* 프로젝트의 폴더 *뷰* 폴더입니다.
- *Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, 및 *Index.cshtml* 새 *Views\Movies* 폴더입니다.

[![NewMovieControllerScreenShot](accessing-your-models-data-from-a-controller/_static/image4.png "NewMovieControllerScreenShot")](accessing-your-models-data-from-a-controller/_static/image3.png)

ASP.NET MVC 3 스 캐 폴딩 메커니즘을 자동으로 생성 됩니다는 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰를 합니다. 이제 모든 기능을 갖춘 웹 응용 프로그램을 만들기, 나열, 편집 및 동영상 항목을 삭제할 수 있습니다.

응용 프로그램을 실행 하 고 이동 합니다 `Movies` 컨트롤러를 추가 하 여 */Movies* 브라우저의 주소 표시줄에서 URL로 합니다. 응용 프로그램은 기본 라우팅을 의존 하기 때문에 (에 정의 된 합니다 *Global.asax* 파일), 브라우저 요청 `http://localhost:xxxxx/Movies` 기본값으로 라우팅됩니다 `Index` 의 동작 메서드는 `Movies` 컨트롤러입니다. 브라우저 요청 말해 `http://localhost:xxxxx/Movies` 같습니다 효과적으로 브라우저 요청 `http://localhost:xxxxx/Movies/Index`합니다. 결과 빈 목록을 영화, 이므로 아직 추가 하지 않았습니다.

![](accessing-your-models-data-from-a-controller/_static/image5.png)

### <a name="creating-a-movie"></a>영화를 만들기

**새로 만들기** 링크를 선택합니다. 영화에 대 한 일부 정보를 입력 한 다음 클릭 합니다 **만들기** 단추입니다.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

클릭 하는 **만들기** 단추 하면 폼이 데이터베이스에서 동영상 정보가 저장 된 서버에 게시할 수 있습니다. 다음으로 리디렉션됩니다 합니다 */Movies* URL을 목록에서 새로 만든된 동영상을 볼 수 있습니다.

[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png "IndexWhenHarryMet")](accessing-your-models-data-from-a-controller/_static/image7.png)

나머지 몇 개의 동영상 항목을 만듭니다. 모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.

## <a name="examining-the-generated-code"></a>생성된 된 코드 검사

엽니다는 *Controllers\MoviesController.cs* 파일을 생성 된 검사 `Index` 메서드. 영화 컨트롤러와의 일부를 `Index` 메서드는 다음과 같습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

다음 줄을 `MoviesController` 앞에서 설명한 대로 클래스는 영화 데이터베이스 컨텍스트를 인스턴스화합니다. 쿼리, 편집 및 삭제 영화에 영화 데이터베이스 컨텍스트를 사용할 수 있습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

요청을를 `Movies` 컨트롤러의 모든 항목을 반환 합니다 `Movies` 영화 데이터베이스의 테이블 다음 결과 전달는 `Index` 보기.

## <a name="strongly-typed-models-and-the-model-keyword"></a>강력한 형식의 모델 및 @model 키워드

이 자습서의 앞부분에서 컨트롤러를 전달 하는 방법 데이터 또는 개체를 사용 하 여 뷰 템플릿 본는 `ViewBag` 개체입니다. `ViewBag` 뷰 정보를 전달 하는 편리한 런타임에 바인딩된 방법을 제공 하는 동적 개체입니다.

ASP.NET MVC는 또한 형식화 된 데이터 또는 개체를 뷰 템플릿으로 강력 하 게 전달 하는 기능을 제공 합니다. 이 접근 방식을 사용 하면 컴파일 시간을 개선할 Visual Web Developer 편집기에서 더 다양 한 IntelliSense 및 코드 검사를 강력한 형식입니다. 이 방법을 사용 합니다 `MoviesController` 클래스 및 *Index.cshtml* 템플릿 보기.

코드를 만드는 방법을 확인할 수 있습니다는 [ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx) 호출할 때 개체를 `View` 의 도우미 메서드에 `Index` 작업 메서드. 그런 다음이 `Movies` 컨트롤러에서 보기로 목록:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

포함 하 여를 `@model` 보기 템플릿 파일의 맨 위에 있는 문을 뷰에서 필요로 하는 개체의 형식을 지정할 수 있습니다. 다음에 Visual Web Developer 영화 컨트롤러를 만들 때 자동으로 포함 `@model` 맨 위에 있는 문을 합니다 *Index.cshtml* 파일:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

이렇게 `@model` 지시문을 사용 하면 사용 하 여 컨트롤러에서 보기로 전달 하는 영화 목록에 액세스할 수 있습니다는 `Model` 개체는 강력한 형식입니다. 예를 들어 합니다 *Index.cshtml* 수행 하 여 영화를 통해 템플릿 코드를 루프를 `foreach` 는 강력한 형식의 문을 `Model` 개체:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml)]

때문에 `Model` 개체는 강력한 (으로 `IEnumerable<Movie>` 개체), 각 `item` 루프에 있는 개체 형식의 `Movie`합니다. 다른 이점과 함께이 의미는 코드의 컴파일 타임 검사을 얻고 완벽 하 게 코드 편집기에서 IntelliSense 지원 합니다.

[![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image10.png "ModelIntelliSense")](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>SQL Server Compact를 사용 하 여 작업

제공 된 데이터베이스 연결 문자열을 가리키는 entity Framework Code First 검색을 `Movies` Code First 데이터베이스 자동으로 생성 하므로 아직 존재 하지 않는 데이터베이스입니다. 확인 하 여 생성 된 것을 확인할 수 있습니다 합니다 *앱\_데이터* 폴더입니다. 표시 되지 않는 경우는 *Movies.sdf* 파일을 클릭 합니다 **모든 파일 표시** 단추를 **솔루션 탐색기** 도구 모음에서 클릭는 **새로 고침** 단추를 클릭 한 다음를 확장 합니다 *앱\_데이터* 폴더입니다.

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png "SDF_in_SolnExp")](accessing-your-models-data-from-a-controller/_static/image11.png)

두 번 클릭 *Movies.sdf* 열려는 **서버 탐색기**합니다. 다음를 확장 합니다 **테이블** 데이터베이스에서 생성 된 테이블을 표시 하는 폴더입니다.

> [!NOTE]
> 두 번 클릭 하면 오류가 발생 하는 경우 *Movies.sdf*를 설치한 다음 했는지 [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원). (소프트웨어에 대 한 링크,이 자습서 시리즈의 1 부에서는 필수 조건 목록 참조). 릴리스를 설치한 경우 해야 닫았다가 다시 Visual Web Developer를 엽니다.


[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png "DB_explorer")](accessing-your-models-data-from-a-controller/_static/image13.png)

에 대해 하나씩, 두 테이블이 합니다 `Movie` 엔터티 집합 및는 `EdmMetadata` 테이블입니다. `EdmMetadata` 테이블 엔터티 프레임 워크에서 모델 및 데이터베이스 동기화 되지 않은 경우 확인을 사용 합니다.

마우스 오른쪽 단추로 클릭 합니다 `Movies` 선택한 테이블 **테이블 데이터 표시** 만든 데이터를 볼 수 있습니다.

[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png "MoviesTable")](accessing-your-models-data-from-a-controller/_static/image15.png)

마우스 오른쪽 단추로 클릭 합니다 `Movies` 선택한 테이블 **테이블 스키마 편집**합니다.

[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png "EditTableSchema")](accessing-your-models-data-from-a-controller/_static/image17.png)

[![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image20.png "TableSchemaSM")](accessing-your-models-data-from-a-controller/_static/image19.png)

알림 방법의 스키마를 `Movies` 테이블에 매핑됩니다는 `Movie` 앞에서 만든 클래스입니다. Entity Framework Code First 자동으로 생성이 스키마에 따라 프로그램 `Movie` 클래스입니다.

이 과정을 완료 하는 경우 연결을 닫습니다. (연결을 닫으려면 없는 경우 하면 오류가 발생할 수 다음에 프로젝트를 실행할 때).

[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image22.png "CloseConnection")](accessing-your-models-data-from-a-controller/_static/image21.png)

이제 있고 데이터베이스는 단순 목록 페이지에서 콘텐츠를 표시 합니다. 다음 자습서에서에서는 스 캐 폴드 된 코드의 나머지 부분을 검사 하 고 추가 된 `SearchIndex` 메서드 및 `SearchIndex` 영화가이 데이터베이스에 대 한 검색할 수 있는 보기입니다.

> [!div class="step-by-step"]
> [이전](adding-a-model.md)
> [다음](examining-the-edit-methods-and-edit-view.md)
