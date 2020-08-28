---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 컨트롤러에서 모델의 데이터에 액세스 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045171"
---
# <a name="accessing-your-models-data-from-a-controller"></a>컨트롤러에서 모델의 데이터에 액세스

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

이 섹션에서는 새 클래스를 만들고 `MoviesController` 영화 데이터를 검색 하 고 보기 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다.

다음 단계로 이동 하기 전에 **응용 프로그램을 빌드합니다** . 응용 프로그램을 빌드하지 않으면 컨트롤러를 추가 하는 동안 오류가 발생 합니다.

솔루션 탐색기에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가**, **컨트롤러**를 차례로 클릭 합니다.

![](accessing-your-models-data-from-a-controller/_static/image1.png)

**스 캐 폴드 추가** 대화 상자에서 **Entity Framework를 사용 하 여 MVC 5 컨트롤러 (뷰 포함**)를 클릭 한 다음 **추가**를 클릭 합니다.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- 모델 클래스에 대해 **동영상 (MvcMovie. 모델)** 을 선택 합니다.
- 데이터 컨텍스트 클래스에 대해 **MovieDBContext (MvcMovie. 모델)** 를 선택 합니다.
- 컨트롤러 이름에 **moviescontroller.cs**을 입력 합니다.

  아래 이미지는 완료 된 대화 상자를 보여 줍니다.  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

**추가**를 클릭합니다. 오류가 발생 하면 컨트롤러 추가를 시작 하기 전에 응용 프로그램을 빌드하지 않았을 수 있습니다. Visual Studio에서 다음과 같은 파일 및 폴더를 만듭니다.

- *Controllers* 폴더에 있는 *MoviesController.cs* 파일입니다.
- *Views\Movies* 폴더입니다.
- 새 *Views\Movies* 폴더에서 *. cshtml, Delete cshtml, Details, Edit. cshtml*및 *인덱스* 를 만듭니다.

Visual Studio에서 자동으로 [crud](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (만들기, 읽기, 업데이트 및 삭제) 작업 메서드 및 보기를 만들었습니다 (crud 작업 메서드 및 보기의 자동 생성을 스 캐 폴딩 이라고 함). 이제 동영상 항목을 만들고, 나열 하 고, 편집 하 고, 삭제할 수 있는 완전히 작동 하는 웹 응용 프로그램이 있습니다.

응용 프로그램을 실행 하 고 **MVC 영화** 링크를 클릭 하거나, `Movies` 브라우저의 주소 표시줄에 있는 URL에 */da* 를 추가 하 여 컨트롤러를 찾습니다. 응용 프로그램은 기본 라우팅 ( *App \_ Start\RouteConfig.cs* 파일에 정의 됨)을 기반으로 하기 때문에 브라우저 요청은 `http://localhost:xxxxx/Movies` `Index` 컨트롤러의 기본 작업 메서드로 라우팅됩니다 `Movies` . 즉, 브라우저 요청은 `http://localhost:xxxxx/Movies` 실제로 브라우저 요청과 동일 합니다 `http://localhost:xxxxx/Movies/Index` . 아직 추가 하지 않았기 때문에 빈 영화 목록이 생성 됩니다.

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>동영상 만들기

**새로 만들기** 링크를 선택합니다. 동영상에 대 한 세부 정보를 입력 한 다음 **만들기** 단추를 클릭 합니다.

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> Price 필드에는 소수점 또는 쉼표를 입력할 수 없습니다. 소수점에 쉼표 (,)를 사용 하는 영어가 아닌 로캘 및 미국 영어가 아닌 날짜 형식에 대해 jQuery 유효성 검사를 지원 하려면 &quot; &quot; 사용할 *globalize.js* 및 특정 *문화/globalize.cultures.js* 파일 (부터 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) 및 JavaScript를 포함 해야 합니다 `Globalize.parseFloat` . 다음 자습서에서이 작업을 수행 하는 방법을 보여 드리겠습니다. 이제 10 같은 정수를 입력하면 됩니다.

[ **만들기** ] 단추를 클릭 하면 양식이 서버에 게시 되 고,이 경우 동영상 정보가 데이터베이스에 저장 됩니다. 그런 다음 목록에서 새로 만든 동영상을 볼 수 있는 */Clurl* 로 리디렉션됩니다.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

나머지 몇 개의 동영상 항목을 만듭니다. 모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.

## <a name="examining-the-generated-code"></a>생성 된 코드 검사

*Controllers\MoviesController.cs* 파일을 열고 생성 된 메서드를 검사 합니다 `Index` . 메서드를 사용 하는 동영상 컨트롤러의 일부는 `Index` 다음과 같습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

컨트롤러에 대 한 요청은 `Movies` 테이블의 모든 항목을 반환 `Movies` 하 고 결과를 뷰에 전달 합니다 `Index` . 클래스의 다음 줄은 `MoviesController` 앞에서 설명한 대로 영화 데이터베이스 컨텍스트를 인스턴스화합니다. 동영상 데이터베이스 컨텍스트를 사용 하 여 영화를 쿼리, 편집 및 삭제할 수 있습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>강력한 형식의 모델 및 @model 키워드

이 자습서의 앞부분에서 볼 때 컨트롤러에서 개체를 사용 하 여 데이터 또는 개체를 뷰 템플릿에 전달 하는 방법을 살펴보았습니다 `ViewBag` . 는 `ViewBag` 뷰에 정보를 전달 하는 데 편리한 런타임에 바인딩되는 방법을 제공 하는 동적 개체입니다.

또한 MVC는 *강력한* 형식의 개체를 뷰 템플릿에 전달 하는 기능을 제공 합니다. 강력 하 게 형식화 된이 방법은 Visual Studio 편집기에서 코드 및 더 다양 한 [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) 의 컴파일 시간 검사를 향상 시킬 수 있습니다. Visual Studio의 스 캐 폴딩 메커니즘은 *strongly* `MoviesController` 메서드 및 뷰를 만들 때 클래스 및 뷰 템플릿을 사용 하 여 강력한 형식의 모델을 전달 하는이 방법을 사용 했습니다.

*Controllers\MoviesController.cs* 파일에서 생성 된 메서드를 검사 합니다 `Details` . `Details`메서드는 다음과 같습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id`매개 변수는 일반적으로 경로 데이터로 전달 됩니다. 예를 들어는 `http://localhost:1234/movies/details/1` 컨트롤러를 movie controller로 설정 하 고 작업을 `details` 및 `id` 로 설정 합니다. 다음과 같이 쿼리 문자열을 사용 하 여 id를 전달할 수도 있습니다.

`http://localhost:1234/movies/details?id=1`

이 있으면 `Movie` 모델의 인스턴스가 `Movie` 뷰에 전달 됩니다 `Details` .

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

*Views\Movies\Details.cshtml* 파일의 내용을 검사 합니다.

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

`@model`뷰 템플릿 파일의 맨 위에 문을 포함 하 여 뷰가 예상 하는 개체 유형을 지정할 수 있습니다. 영화 컨트롤러를 만들 때 Visual Studio에서는 *Details.cshtml* 파일의 맨 위에 다음 `@model` 문을 자동으로 포함했습니다.

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

이 `@model` 지시문을 사용하면 강력한 형식인 `Model` 개체를 사용하여 컨트롤러가 뷰에 전달된 영화에 액세스할 수 있습니다. 예를 들어, *Details* 템플릿에서는 코드는 각 동영상 필드를 강력한 형식의 개체를 사용 하 여 `DisplayNameFor` HTML 도우미 [에 전달](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) 합니다 `Model` . `Create`및 `Edit` 메서드 및 뷰 템플릿은 또한 동영상 모델 개체를 전달 합니다.

MoviesController.cs 파일에서 *Index. cshtml* 뷰 템플릿 및 메서드를 검토 합니다 `Index` *MoviesController.cs* . [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)작업 메서드에서 도우미 메서드를 호출할 때 코드에서 개체를 만드는 방법을 확인 `View` `Index` 합니다. 그런 다음 코드는이 `Movies` 목록을 `Index` 동작 메서드에서 뷰로 전달 합니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

동영상 컨트롤러를 만들 때 Visual Studio는 다음 문을 자동으로 `@model` *Index. cshtml* 파일의 맨 위에 포함 합니다.

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

이 `@model` 지시문을 사용 하면 강력한 형식의 개체를 사용 하 여 컨트롤러에서 뷰로 전달 된 동영상 목록에 액세스할 수 있습니다 `Model` . 예를 들어, *인덱스인* 템플릿에서 코드는 강력한 형식의 개체에 대해 문을 수행 하 여 동영상을 반복 합니다 `foreach` `Model` .

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

개체는 강력한 형식의 개체 이기 때문에 `Model` `IEnumerable<Movie>` `item` 루프의 각 개체는로 형식화 됩니다 `Movie` . 다른 이점 중 하나는 코드 편집기에서 코드 및 전체 IntelliSense 지원에 대 한 컴파일 시간 검사를 가져오는 것입니다.

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>SQL Server LocalDB 사용

Entity Framework Code First 제공 된 데이터베이스 연결 문자열이 `Movies` 아직 존재 하지 않은 데이터베이스를 가리키고 있으므로 데이터베이스를 자동으로 만들 Code First. *앱 \_ 데이터* 폴더를 살펴보면이를 만들었는지 확인할 수 있습니다. *동영상 .mdf* 파일이 표시 되지 않으면 **솔루션 탐색기** 도구 모음에서 **모든 파일 표시** 단추를 클릭 하 고 **새로 고침** 단추를 클릭 한 다음 *앱 \_ 데이터* 폴더를 확장 합니다.

![](accessing-your-models-data-from-a-controller/_static/image9.png)

*동영상과* 를 두 번 클릭 하 여 **서버 탐색기**를 연 다음 **Tables** 폴더를 확장 하 여 영화 테이블을 표시 합니다. ID 옆의 키 아이콘을 확인 합니다. 기본적으로 EF는 ID가 기본 키 인 속성을 만듭니다. EF 및 MVC에 대 한 자세한 내용은 Tom Dykstra 's의 우수한 자습서 [mvc 및 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조 하세요.

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

테이블을 마우스 오른쪽 단추로 클릭 `Movies` 하 고 **테이블 데이터 표시** 를 선택 하 여 만든 데이터를 확인 합니다.

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

테이블을 마우스 오른쪽 단추로 클릭 하 `Movies` 고 **테이블 정의 열기** 를 선택 하 여 Entity Framework Code First 생성 된 테이블 구조를 확인 합니다.

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

테이블의 스키마가 앞에서 `Movies` 만든 클래스에 매핑되는 방식을 확인 `Movie` 합니다. Entity Framework Code First는 클래스를 기반으로이 스키마를 자동으로 만들었습니다 `Movie` .

완료 되 면 *MovieDBContext* 를 마우스 오른쪽 단추로 클릭 하 고 **연결 닫기**를 선택 하 여 연결을 닫습니다. 연결을 닫지 않은 경우 다음에 프로젝트를 실행할 때 오류가 발생할 수 있습니다.

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

이제 데이터를 표시, 편집, 업데이트 및 삭제할 데이터베이스 및 페이지가 제공됩니다. 다음 자습서에서는 스 캐 폴드 코드의 나머지 부분을 검토 하 고 `SearchIndex` `SearchIndex` 이 데이터베이스에서 영화를 검색할 수 있는 메서드 및 뷰를 추가 합니다. MVC와 함께 Entity Framework를 사용 하는 방법에 대 한 자세한 내용은 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델 만들기](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](creating-a-connection-string.md)
> [다음](examining-the-edit-methods-and-edit-view.md)
