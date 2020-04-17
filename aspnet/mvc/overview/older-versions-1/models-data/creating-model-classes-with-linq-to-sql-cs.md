---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: LINQ에서 SQL(C#)으로 모델 클래스 만들기 | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스를 만드는 한 가지 방법을 설명 하는 것입니다. 이 자습서에서는 모델 c를 빌드하는 방법을 배웁니다.
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: eac6fec3a4cfd833b810378d946874a246d9a2c3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542731"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a>LINQ to SQL을 사용하여 모델 클래스 만들기(C#)

[로 마이크로 소프트](https://github.com/microsoft)

[PDF 다운로드](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> 이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스를 만드는 한 가지 방법을 설명 하는 것입니다. 이 자습서에서는 Microsoft LINQ를 SQL로 활용하여 모델 클래스를 빌드하고 데이터베이스 액세스를 수행하는 방법을 알아봅니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스를 만드는 한 가지 방법을 설명 하는 것입니다. 이 자습서에서는 Microsoft LINQ를 SQL로 활용하여 모델 클래스를 빌드하고 데이터베이스 액세스를 수행하는 방법을 배웁니다.

이 자습서에서는 기본 Movie 데이터베이스 응용 프로그램을 빌드합니다. 먼저 Movie 데이터베이스 응용 프로그램을 가능한 가장 빠르고 쉬운 방법으로 만듭니다. 컨트롤러 작업에서 직접 모든 데이터 액세스를 수행합니다.

다음으로 저장소 패턴을 사용하는 방법을 배웁니다. 리포지토리 패턴을 사용하려면 좀 더 많은 작업이 필요합니다. 그러나 이 패턴을 채택하면 변경에 적응하고 쉽게 테스트할 수 있는 응용 프로그램을 빌드할 수 있다는 장점이 있습니다.

## <a name="what-is-a-model-class"></a>모델 클래스란 무엇입니까?

MVC 모델에는 MVC 뷰 또는 MVC 컨트롤러에 포함되지 않은 모든 응용 프로그램 논리가 포함되어 있습니다. 특히 MVC 모델에는 모든 응용 프로그램 비즈니스 및 데이터 액세스 논리가 포함되어 있습니다.

다양한 기술을 사용하여 데이터 액세스 논리를 구현할 수 있습니다. 예를 들어 Microsoft 엔터티 프레임워크, NHibernate, subsonic 또는 ADO.NET 클래스를 사용하여 데이터 액세스 클래스를 빌드할 수 있습니다.

이 자습서에서는 LINQ to SQL을 사용하여 데이터베이스를 쿼리하고 업데이트합니다. LINQ to SQL은 Microsoft SQL Server 데이터베이스와 상호 작용하는 매우 쉬운 방법을 제공합니다. 그러나 ASP.NET MVC 프레임워크는 LINQ에서 SQL에 연결되지 않는다는 점을 이해하는 것이 중요합니다. ASP.NET MVC는 모든 데이터 액세스 기술과 호환됩니다.

## <a name="create-a-movie-database"></a>동영상 데이터베이스 만들기

이 자습서에서는 모델 클래스를 빌드하는 방법을 설명하기 위해 간단한 Movie 데이터베이스 응용 프로그램을 빌드합니다. 첫 번째 단계는 새 데이터베이스를 만드는 것입니다. 솔루션 탐색기\_창에서 앱 데이터 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **추가, 새 항목**을 선택합니다. SQL **Server 데이터베이스** 템플릿을 선택하고 MoviesDB.mdf라는 이름을 지정한 다음 **추가** 단추를 클릭합니다(그림 1 참조).

[![새 SQL 서버 데이터베이스 추가](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**그림 01**: 새 SQL Server 데이터베이스 추가[(전체 크기 이미지를 보려면 클릭)](creating-model-classes-with-linq-to-sql-cs/_static/image3.png)

새 데이터베이스를 만든 후 앱\_데이터 폴더에서 MoviesDB.mdf 파일을 두 번 클릭하여 데이터베이스를 열 수 있습니다. MoviesDB.mdf 파일을 두 번 클릭하면 서버 탐색기 창이 열립니다(그림 2 참조).

서버 탐색기 창은 시각적 웹 개발자를 사용할 때 데이터베이스 탐색기 창이라고 합니다.

[![서버 탐색기 창 사용](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**그림 02**: 서버 탐색기 창 사용[(전체 크기 이미지를 보려면 클릭)](creating-model-classes-with-linq-to-sql-cs/_static/image6.png)

우리는 우리의 영화를 나타내는 우리의 데이터베이스에 하나의 테이블을 추가해야합니다. 테이블 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션을 **선택합니다.** 이 메뉴 옵션을 선택하면 테이블 디자이너가 열립니다(그림 3 참조).

[![서버 탐색기 창 사용](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**그림 03**: 테이블 디자이너[(전체 크기 이미지를 보려면 클릭)](creating-model-classes-with-linq-to-sql-cs/_static/image9.png)

데이터베이스 테이블에 다음 열을 추가해야 합니다.

| **열 이름** | **데이터 유형** | **Null 허용** |
| --- | --- | --- |
| Id | Int | False |
| 제목 | 은바르르 (200) | False |
| 감독 | 은바르르 (50) | False |

Id 열에 대해 두 가지 특별한 작업을 수행해야 합니다. 먼저 테이블 디자이너의 열을 선택하고 키 아이콘을 클릭하여 Id 열을 기본 키 열로 표시해야 합니다. LINQ to SQL에서는 데이터베이스에 대한 삽입 또는 업데이트를 수행할 때 기본 키 열을 지정해야 합니다.

그런 다음 Id 열에 예 값을 Id **속성에** 할당하여 ID 열을 Id 열로 표시해야 합니다(그림 3 참조). Identity 열은 테이블에 새 데이터 행을 추가할 때마다 자동으로 새 번호가 할당되는 열입니다.

## <a name="create-linq-to-sql-classes"></a>SQL 클래스에 LINQ 만들기

MVC 모델에는 tblMovie 데이터베이스 테이블을 나타내는 SQL 클래스에 대한 LINQ가 포함됩니다. 이러한 LINQ를 SQL 클래스로 만드는 가장 쉬운 방법은 모델 폴더를 마우스 오른쪽 단추로 클릭하고, **추가, 새 항목 추가를**선택하고, LINQ에서 SQL 클래스 템플릿을 선택하고, 클래스에 Movie.dbml 이름을 지정하고, **추가** 단추를 클릭하는 것입니다(그림 4 참조).

[![SQL 클래스에 LINQ 만들기](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**그림 04**: SQL 클래스에 LINQ 만들기[(전체 크기 이미지를 보려면 클릭)](creating-model-classes-with-linq-to-sql-cs/_static/image12.png)

MOVIE LINQ를 SQL 클래스로 만든 직후 개체 관계형 디자이너가 나타납니다. 서버 탐색기 창에서 개체 관계형 디자이너로 데이터베이스 테이블을 드래그하여 특정 데이터베이스 테이블을 나타내는 LINQ를 SQL 클래스로 만들 수 있습니다. tblMovie 데이터베이스 테이블을 개체 관계형 디자이너에 추가해야 합니다(그림 5 참조).

[![개체 관계형 디자이너 사용](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**그림 05**: 객체 관계형 디자이너 사용[(전체 크기 이미지를 보려면 클릭)](creating-model-classes-with-linq-to-sql-cs/_static/image15.png)

기본적으로 개체 관계 디자이너는 디자이너로 드래그하는 데이터베이스 테이블과 이름이 매우 같은 클래스를 만듭니다. 그러나 클래스를 호출하고 싶지는 `tblMovie`않습니다. 따라서 디자이너에서 클래스의 이름을 클릭 하 고 클래스의 이름을 Movie로 변경 합니다.

마지막으로 LINQ를 SQL 클래스에 저장하려면 **저장** 단추(플로피 그림)를 클릭해야 합니다. 그렇지 않으면 개체 관계형 디자이너에서 SQL 클래스로 LINQ를 생성하지 않습니다.

## <a name="using-linq-to-sql-in-a-controller-action"></a>컨트롤러 작업에서 LINQ에서 SQL로 사용

LINQ에서 SQL 클래스로 이동하므로 이러한 클래스를 사용하여 데이터베이스에서 데이터를 검색할 수 있습니다. 이 섹션에서는 컨트롤러 작업 내에서 직접 LINQ를 SQL 클래스에 사용하는 방법을 배웁니다. TblMovies 데이터베이스 테이블의 동영상 목록을 MVC 보기에 표시합니다.

먼저 HomeController 클래스를 수정해야 합니다. 이 클래스는 응용 프로그램의 컨트롤러 폴더에서 찾을 수 있습니다. 목록 1의 클래스처럼 보이면 클래스를 수정합니다.

**리스팅 1 –`Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

목록 `Index()` 1의 작업은 LINQ에서 SQL DataContext `MovieDataContext`클래스(the)를 사용하여 `MoviesDB` 데이터베이스를 나타냅니다. 클래스는 `MoveDataContext` Visual Studio 개체 관계형 디자이너에 의해 생성되었습니다.

LINQ 쿼리는 `tblMovies` 데이터베이스 테이블에서 모든 동영상을 검색하기 위해 DataContext에 대해 수행됩니다. 동영상 목록은 .라는 `movies`로컬 변수에 할당됩니다. 마지막으로 동영상 목록이 뷰 데이터를 통해 뷰에 전달됩니다.

동영상을 표시하려면 인덱스 보기를 수정해야 합니다. `Views\Home\` 폴더에서 인덱스 보기를 찾을 수 있습니다. 목록 2의 뷰처럼 보이게 되도록 인덱스 보기를 업데이트합니다.

**리스팅 2 –`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

수정된 인덱스 보기에는 `<%@ import namespace %>` 뷰 맨 위에 지시문이 포함되어 있습니다. 이 지시문은 `MvcApplication1.Models namespace`을 가져옵니다. 뷰에서 `model` 클래스( 특히 `Movie` 클래스)와 함께 작업하려면 이 네임스페이스가 필요합니다.

목록 2의 보기에는 `foreach` 속성으로 표시되는 모든 항목을 반복하는 `ViewData.Model` 루프가 포함되어 있습니다. 각 `movie`에 `Title` 대해 속성 값이 표시됩니다.

`ViewData.Model` 속성 값이 `IEnumerable`에 캐스팅됩니다. 이 내용은 `ViewData.Model`의 내용을 반복하기 위해 필요합니다. 여기서 또 다른 옵션은 강력한 형식의 `view`을 만드는 것입니다. 강력한 형식을 `view`만들 때 뷰의 코드 `ViewData.Model` 숨결 클래스에서 특정 형식에 속성을 캐스팅합니다.

`HomeController` 클래스 및 Index 보기를 수정한 후 응용 프로그램을 실행하면 빈 페이지가 표시됩니다. 데이터베이스 테이블에 동영상 레코드가 없기 때문에 빈 `tblMovies` 페이지가 표시됩니다.

데이터베이스 테이블에 레코드를 `tblMovies` 추가하려면 서버 탐색기 `tblMovies` 창(Visual Web 개발자의 데이터베이스 탐색기 창)에서 데이터베이스 테이블을 마우스 오른쪽 단추로 클릭하고 테이블 데이터 표시 옵션을 선택합니다. 나타나는 표를 `movie` 사용하여 레코드를 삽입할 수 있습니다(그림 6 참조).

[![동영상 삽입](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**그림 06**: 동영상 삽입[(클릭하여 전체 크기 이미지 보기)](creating-model-classes-with-linq-to-sql-cs/_static/image18.png)

테이블에 일부 데이터베이스 레코드를 `tblMovies` 추가하고 응용 프로그램을 실행하면 그림 7의 페이지가 표시됩니다. 모든 동영상 데이터베이스 레코드가 글머리 기호 목록에 표시됩니다.

[![인덱스 보기로 동영상 표시](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**그림 07**: 색인 보기로 동영상 표시[(전체 크기 이미지를 보려면 클릭)](creating-model-classes-with-linq-to-sql-cs/_static/image21.png)

## <a name="using-the-repository-pattern"></a>리포지토리 패턴 사용

이전 섹션에서는 컨트롤러 작업 내에서 직접 LINQ를 SQL 클래스에 사용했습니다. 컨트롤러 작업에서 직접 `MovieDataContext` `Index()` 클래스를 사용 했습니다. 간단한 응용 프로그램의 경우이 작업을 수행하는 데 아무런 문제가 없습니다. 그러나 컨트롤러 클래스에서 LINQ에서 SQL로 직접 작업하면 보다 복잡한 응용 프로그램을 빌드해야 하는 경우 문제가 발생합니다.

컨트롤러 클래스 내에서 LINQ를 SQL로 사용하면 나중에 데이터 액세스 기술을 전환하기가 어렵습니다. 예를 들어 Microsoft LINQ를 SQL로 사용하는 것에서 데이터 액세스 기술로 Microsoft 엔터티 프레임워크를 사용하는 것으로 전환할 수 있습니다. 이 경우 응용 프로그램 내에서 데이터베이스에 액세스하는 모든 컨트롤러를 다시 작성해야 합니다.

컨트롤러 클래스 내에서 LINQ에서 SQL로 LINQ를 사용하면 응용 프로그램에 대한 단위 테스트를 빌드하기가 어렵습니다. 일반적으로 단위 테스트를 수행할 때 데이터베이스와 상호 작용하지 않으려고 합니다. 단위 테스트를 사용하여 데이터베이스 서버가 아닌 응용 프로그램 논리를 테스트하려고 합니다.

향후 변경에 더 쉽게 적응할 수 있고 보다 쉽게 테스트할 수 있는 MVC 응용 프로그램을 빌드하려면 저장소 패턴을 사용하는 것이 좋습니다. 저장소 패턴을 사용하면 모든 데이터베이스 액세스 논리가 포함된 별도의 리포지토리 클래스를 만듭니다.

리포지토리 클래스를 만들 때 리포지토리 클래스에서 사용하는 모든 메서드를 나타내는 인터페이스를 만듭니다. 컨트롤러 내에서 저장소 대신 인터페이스에 대해 코드를 작성합니다. 이렇게 하면 나중에 다른 데이터 액세스 기술을 사용하여 리포지토리를 구현할 수 있습니다.

목록 3의 인터페이스는 `IMovieRepository` 이름이 지정되며 `ListAll()`.

**리스팅 3 –`Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

목록 4의 리포지토리 클래스는 `IMovieRepository` 인터페이스를 구현합니다. 인터페이스에 필요한 메서드에 `ListAll()` 해당하는 메서드가 `IMovieRepository` 포함되어 있습니다.

**리스팅 4 –`Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

마지막으로 목록 `MoviesController` 5의 클래스는 저장소 패턴을 사용합니다. 더 이상 LINQ를 SQL 클래스에 직접 사용하지 않습니다.

**리스팅 5 –`Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

목록 5의 `MoviesController` 클래스에는 두 개의 생성자가 있습니다. 첫 번째 생성자인 매개 변수 없는 생성자는 응용 프로그램이 실행될 때 호출됩니다. 이 생성자는 클래스의 `MovieRepository` 인스턴스를 만들고 두 번째 생성자에게 전달합니다.

두 번째 생성자는 단일 매개 `IMovieRepository` 변수인 매개 변수를 가있습니다. 이 생성자는 매개 변수값을 .라는 `_repository`클래스 수준 필드에 할당하기만 하면 됩니다.

`MoviesController` 클래스는 종속성 주입 패턴이라는 소프트웨어 디자인 패턴을 활용하고 있습니다. 특히 생성자 종속성 주입이라는 것을 사용하고 있습니다. 이 패턴에 대한 자세한 내용은 마틴 파울러의 다음 기사를 읽어보세요.

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

첫 번째 생성자(첫 `MoviesController` 번째 생성자 제외)의 모든 코드가 실제 `IMovieRepository` `MovieRepository` 클래스 대신 인터페이스와 상호 작용합니다. 코드는 인터페이스의 구체적인 구현 대신 추상 인터페이스와 상호 작용합니다.

응용 프로그램에서 사용하는 데이터 액세스 기술을 수정하려면 대체 데이터베이스 `IMovieRepository` 액세스 기술을 사용하는 클래스로 인터페이스를 구현하기만 하면 됩니다. 예를 들어 클래스 또는 `EntityFrameworkMovieRepository` 클래스를 `SubSonicMovieRepository` 만들 수 있습니다. 컨트롤러 클래스는 인터페이스에 대해 프로그래밍되므로 컨트롤러 클래스의 `IMovieRepository` 새 구현을 컨트롤러 클래스에 전달할 수 있으며 클래스는 계속 작동합니다.

또한 `MoviesController` 클래스를 테스트하려는 경우 가짜 영화 저장소 클래스를 `HomeController`에 전달할 수 있습니다. 실제로 데이터베이스에 `IMovieRepository` 액세스하지 않지만 인터페이스에 필요한 모든 메서드를 포함하는 클래스를 `IMovieRepository` 사용하여 클래스를 구현할 수 있습니다. 이렇게 하면 실제 데이터베이스에 `MoviesController` 실제로 액세스하지 않고 클래스를 단위 테스트할 수 있습니다.

## <a name="summary"></a>요약

이 자습서의 목표는 Microsoft LINQ를 SQL로 활용하여 MVC 모델 클래스를 만드는 방법을 보여 주는 것이었습니다. ASP.NET MVC 응용 프로그램에 데이터베이스 데이터를 표시하기 위한 두 가지 전략을 살펴보었습니다. 먼저 LINQ를 SQL 클래스에 만들고 컨트롤러 작업 내에서 직접 클래스를 사용했습니다. 컨트롤러 내에서 LINQ에서 SQL 클래스로 LINQ를 사용하면 MVC 응용 프로그램에서 데이터베이스 데이터를 빠르고 쉽게 표시할 수 있습니다.

다음으로, 데이터베이스 데이터를 표시하기 위한 약간 더 어렵지만 확실히 더 유덕한 경로를 탐색했습니다. 저장소 패턴을 활용하고 모든 데이터베이스 액세스 논리를 별도의 리포지토리 클래스에 배치했습니다. 컨트롤러에서 우리는 구체적인 클래스 대신 인터페이스에 대해 모든 코드를 작성했습니다. 리포지토리 패턴의 장점은 나중에 데이터베이스 액세스 기술을 쉽게 변경할 수 있고 컨트롤러 클래스를 쉽게 테스트할 수 있다는 것입니다.

> [!div class="step-by-step"]
> [이전](creating-model-classes-with-the-entity-framework-cs.md)
> [다음](displaying-a-table-of-database-data-cs.md)
