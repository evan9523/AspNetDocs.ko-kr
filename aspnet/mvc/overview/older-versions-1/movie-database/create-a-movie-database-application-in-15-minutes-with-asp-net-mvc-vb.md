---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: ASP.NET MVC (VB)를 사용 하 여 15 분만에 영화 데이터베이스 응용 프로그램 만들기 | Microsoft Docs
author: StephenWalther
description: Stephen walther가 전체 데이터베이스 기반의 ASP.NET MVC 응용 프로그램 시작부터 완료를 빌드합니다. 이 자습서는 새로운는 사람들에 대 한 훌륭한 소개 하는 중...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: f0a060bffc2e45f54d03571b6609a30876202e32
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044810"
---
<a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a>ASP.NET MVC를 사용하여 15분 만에 영화 데이터베이스 애플리케이션 만들기(VB)
====================
[Stephen walther가](https://github.com/StephenWalther)

[코드 다운로드](http://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> Stephen walther가 전체 데이터베이스 기반의 ASP.NET MVC 응용 프로그램 시작부터 완료를 빌드합니다. 이 자습서는 ASP.NET MVC Framework를 처음 접하는 및 ASP.NET MVC 응용 프로그램을 구축 하는 과정 이해 하려는 사용자에 대 한 훌륭한 소개 합니다.


이 자습서의 목적은 "는 것은 어떤지에"의 의미를 제공 하는 ASP.NET MVC 응용 프로그램을 빌드합니다. 이 자습서에서는 있습니까 무기를 발사 하는 전체 ASP.NET MVC 응용 프로그램 시작부터 완료를 구축 하는 과정입니다. 간단한 데이터베이스 중심 응용 프로그램을 작성 하는 방법을 나열, 만들기, 데이터베이스 레코드를 편집을 보여 주는 방법을 하겠습니다.

응용 프로그램을 빌드하는 프로세스를 간소화 하기 위해 Visual Studio 2008의 스 캐 폴딩 기능에 알아보겠습니다. 초기 코드 및 콘텐츠는 컨트롤러, 모델 및 뷰를 생성 하는 Visual Studio 알림이 제공 됩니다.

Active Server Pages와 ASP.NET 보았다면 다음 찾아야 ASP.NET MVC 매우 친숙 합니다. ASP.NET MVC 뷰는 Active Server Pages 응용 프로그램의 페이지과 매우 유사 합니다. 및 기존의 ASP.NET Web Forms 응용 프로그램과 마찬가지로 ASP.NET MVC 사용 하면 다양 한 언어 및.NET framework에서 제공 하는 클래스에 대 한 전체 액세스 합니다.

독자는이 자습서를 파악할 수 있도록 하는 방법을 ASP.NET MVC 응용 프로그램을 구축 하는 환경은 모두 유사한 것과 다르며 Active Server Pages 또는 ASP.NET Web Forms 응용 프로그램을 구축 하는 환경을의입니다.

## <a name="overview-of-the-movie-database-application"></a>영화 데이터베이스 응용 프로그램 개요

간단 하 게 목표 이기 때문에 매우 간단한 영화 데이터베이스 응용 프로그램을 빌드할 합니다. 간단한 영화 데이터베이스 응용 프로그램 수 있도록 세 가지를 수행 합니다.

1. 영화 데이터베이스 레코드 집합 나열
2. 새 영화 데이터베이스 레코드 만들기
3. 기존 영화 데이터베이스 레코드를 편집 합니다.

마찬가지로 간단 하 게 유지 하려는 것 이므로 알아보겠습니다 최소 수가 응용 프로그램을 빌드하는 데 필요한 ASP.NET MVC 프레임 워크의 기능 활용. 예를 들어에서는 없습니다 활용 Test-Driven Development 합니다.

응용 프로그램을 만들기 위해 각 단계를 완료 해야 합니다.

1. ASP.NET MVC 웹 응용 프로그램 프로젝트를 만들려면
2. 데이터베이스 만들기
3. 데이터베이스 모델 만들기
4. ASP.NET MVC 컨트롤러 만들기
5. ASP.NET MVC 뷰 만들기

## <a name="preliminaries"></a>준비 단계

Visual Studio 2008 또는 Visual Web Developer 2008 Express는 ASP.NET MVC 응용 프로그램 빌드에 필요 합니다. ASP.NET MVC 프레임 워크를 다운로드 해야 합니다.

Visual Studio 2008을 소유 하지 않은, Visual Studio 2008 90 일 평가판이 웹이 사이트에서 다운로드할 수 있습니다.

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

또는 만들면 ASP.NET MVC 응용 프로그램 Visual Web Developer Express 2008을 사용 하 여 됩니다. Visual Web Developer Express를 사용 하려는 경우 다음 해야 서비스 팩 1을 설치 합니다. Visual Web Developer 2008 Express 서비스 팩 1을 사용 하 여이 웹 사이트에서 다운로드할 수 있습니다.

[https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

Visual Studio 2008 또는 Visual Web Developer 2008을 설치한 후 ASP.NET MVC 프레임 워크를 설치 해야 합니다. 다음 웹 사이트에서 ASP.NET MVC 프레임 워크를 다운로드할 수 있습니다.

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> ASP.NET 프레임 워크 및 ASP.NET MVC 프레임 워크를 개별적으로 다운로드 하는 대신 웹 플랫폼 설치 관리자를 활용할 수 있습니다. 웹 플랫폼 설치 관리자는 설치 된 응용 프로그램을 쉽게 관리할 수 있도록 하는 응용 프로그램 컴퓨터:
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)


## <a name="creating-an-aspnet-mvc-web-application-project"></a>ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기

Visual Studio 2008에서 새 ASP.NET MVC 웹 응용 프로그램 프로젝트를 만들어 보겠습니다. 메뉴 옵션을 선택 **파일, 새 프로젝트** 그림 1의 새 프로젝트 대화 상자를 볼 수 있습니다. 프로그래밍 언어와 Visual Basic을 선택 하 고 ASP.NET MVC 웹 응용 프로그램 프로젝트 템플릿을 선택 합니다. 프로젝트 이름을 MovieApp 제공 하 고 확인 단추를 클릭 합니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)

**그림 01**: 새 프로젝트 대화 상자 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))


새 프로젝트 대화 상자의 맨 위에 있는 드롭다운 목록에서.NET Framework 3.5를 선택 하거나 ASP.NET MVC 웹 응용 프로그램 프로젝트 템플릿이 나타나지 않았는지 확인 합니다.


새 MVC 웹 응용 프로그램 프로젝트를 만들 때마다 Visual Studio는 별도 단위 테스트 프로젝트를 만들 것인지 묻는 메시지를 표시 합니다. 그림 2에서 대화 상자가 나타납니다. 서 우리가 않습니다 만들 테스트가이 자습서에서는 시간 제약 조건으로 인해 (, 예에서는 해야 죄 잠시이 대 한) 선택 합니다 **No** 옵션을 클릭 합니다 **확인** 단추.

> [!NOTE] 
> 
> Visual Web Developer는 테스트 프로젝트를 지원 하지 않습니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)

**그림 02**: 단위 테스트 프로젝트 만들기 대화 상자 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))


ASP.NET MVC 응용 프로그램 폴더의 표준 집합이: 모델, 뷰 및 컨트롤러 폴더입니다. 솔루션 탐색기 창에서 폴더의이 표준 집합을 볼 수 있습니다. 영화 데이터베이스 응용 프로그램을 구축 하기 위해 각 모델, 뷰 및 컨트롤러 폴더에 파일을 추가 해야 합니다.

Visual Studio를 사용 하 여 새 MVC 응용 프로그램을 만든 경우 샘플 응용 프로그램을 얻게 됩니다. 처음부터 새로 시작 하려는 것 이므로이 샘플 응용 프로그램에 대 한 콘텐츠를 삭제 해야 합니다. 다음 파일 및 폴더를 삭제 해야 합니다.

- Controllers\HomeController.vb
- Views\Home

## <a name="creating-the-database"></a>데이터베이스 만들기

이 영화 데이터베이스 레코드를 보관할 데이터베이스를 생성 해야 합니다. 다행히 Visual Studio는 SQL Server Express 라는 무료 데이터베이스를 포함 합니다. 데이터베이스를 만들려면 다음이 단계를 수행 합니다.

1. 앱을 마우스 오른쪽 단추로 클릭\_메뉴 옵션을 선택 하는 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목**합니다.
2. 선택 된 **데이터** 범주를 선택 합니다 **SQL Server 데이터베이스** 템플릿 (그림 3 참조).
3. 새 데이터베이스의 이름을 *MoviesDB.mdf* 을 클릭 합니다 **추가** 단추입니다.

앱에 있는 MoviesDB.mdf 파일을 두 번 클릭 하 여 데이터베이스에 연결할 수 데이터베이스를 만든 후\_데이터 폴더. 서버 탐색기 창을 엽니다 MoviesDB.mdf 파일을 두 번 클릭 합니다.

> [!NOTE] 
> 
> 서버 탐색기 창에는 Visual Web Developer의 경우 데이터베이스 탐색기 창을 이라고 합니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)

**그림 03**: Microsoft SQL Server 데이터베이스 만들기 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))


다음으로 새 데이터베이스 테이블을 만들고 해야 합니다. 서버 탐색기 창에서 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다. 이 메뉴 옵션을 선택 하면 데이터베이스 테이블 디자이너를 엽니다. 다음 데이터베이스 열을 만듭니다.

<a id="0.2_table01"></a>


| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | Int | False |
| 제목 | Nvarchar(100) | False |
| 책임자 | Nvarchar(100) | False |
| DateReleased | DateTime | False |


첫 번째 열, Id 열에 두 특수 속성이 있습니다. 첫째, Id 열을 기본 키 열으로 표시 해야 합니다. Id 열을 선택한 후 클릭 합니다 **기본 키 설정** 단추 (예: 키 보이는 아이콘을 임). 둘째, Id 열을 Id 열으로 표시 해야 합니다. 열 속성 창에서 Id 사양 섹션까지 아래로 스크롤하여 확장 합니다. 변경 된 **Id** 속성을 값 **예**합니다. 작업을 완료 하는 경우 테이블은 그림 4와 같습니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)

**그림 04**: 영화 데이터베이스 테이블 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))


새 테이블을 저장 하는 최종 단계가입니다. 저장 단추 (플로피 아이콘)를 클릭 하 고 새 테이블 이름을 영화를 지정 합니다.

테이블 만들기를 마친 후 테이블에 일부 영화 레코드를 추가 합니다. 서버 탐색기 창에서 동영상 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다. (그림 5 참조) 즐겨 찾는 영화 목록을 입력 합니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)

**그림 05**: 입력 동영상 레코드 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))


## <a name="creating-the-model"></a>모델 만들기

다음 데이터베이스를 표현 하는 클래스 집합을 만드는 해야 합니다. 데이터베이스 모델을 생성 해야 합니다. 데이터베이스 모델의 클래스를 자동으로 생성 하는 Microsoft Entity Framework의 이점은 알아보겠습니다.

> [!NOTE] 
> 
> ASP.NET MVC 프레임 워크는 Microsoft Entity Framework는 관련이 없습니다. 다양 한 개체 관계형 매핑을 사용 하 여 데이터베이스 모델 클래스를 만들 수 있습니다 (또는 / M) LINQ to SQL, Subsonic 및 NHibernate 포함 하는 도구입니다.


엔터티 데이터 모델 마법사를 시작 하려면 다음이 단계를 수행 합니다.

1. 메뉴 옵션을 선택 하 고 솔루션 탐색기 창에서 Models 폴더를 마우스 오른쪽 단추로 클릭 **추가, 새 항목**합니다.
2. 선택 된 **데이터** 범주를 선택 합니다 **ADO.NET 엔터티 데이터 모델** 템플릿.
3. 데이터 모델의 이름을 *MoviesDBModel.edmx* 을 클릭 합니다 **추가** 단추입니다.

추가 단추를 클릭 하면 엔터티 데이터 모델 마법사 나타납니다 (그림 6 참조). 마법사를 완료 하려면 다음이 단계를 수행 합니다.

1. 에 **Model 콘텐츠 선택** 단계를 선택 합니다 **데이터베이스에서 생성** 옵션입니다.
2. 에 **데이터 연결 선택** 단계를 사용 하 여 합니다 *MoviesDB.mdf* 데이터 연결 및 이름 *MoviesDBEntities* 연결 설정 합니다. 클릭 합니다 **다음** 단추입니다.
3. 에 **데이터베이스 개체 선택** 단계, 테이블 노드를 확장 한 다음 동영상 테이블을 선택 합니다. 네임 스페이스를 입력 *MovieApp.Models* 을 클릭 합니다 **마침** 단추입니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)

**그림 06**: 엔터티 데이터 모델 마법사를 사용 하 여 데이터베이스 모델 생성 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))


엔터티 데이터 모델 마법사를 완료 한 후 엔터티 데이터 모델 디자이너가 열립니다. 디자이너에 영화 데이터베이스 테이블에 표시 됩니다 (그림 7 참조).


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)

**그림 07**: 엔터티 데이터 모델 디자이너 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))


계속 하기 전에 하나의 변경 해야 합니다. 엔터티 데이터 마법사 영화 데이터베이스 테이블을 나타내는 이라는 영화 모델 클래스를 생성 합니다. 클래스의 이름을 수정 하려면 먼저 특정 영화를 나타내는 영화 클래스를 사용 해야, 하므로 *영화* of *영화* (단일 아니라 복수).

디자이너 화면의 클래스의 이름을 두 번 클릭 하 고 영화 Movies에서 클래스의 이름을 변경 하십시오. 이렇게 변경한 후 다음을 클릭 합니다 **저장** 단추 (플로피 디스크 아이콘) 동영상 클래스를 생성 합니다.

## <a name="creating-the-aspnet-mvc-controller"></a>ASP.NET MVC 컨트롤러 만들기

다음 단계는 ASP.NET MVC 컨트롤러를 만드는 것입니다. 컨트롤러는 ASP.NET MVC 응용 프로그램을 사용 하 여 사용자 상호 작용 하는 방법을 제어 하는 일을 담당 합니다.

아래 단계를 수행합니다.

1. 솔루션 탐색기 창에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 컨트롤러**합니다.
2. 컨트롤러 추가 대화 상자에서 이름을 입력 *HomeController* 레이블이 지정 된 확인란 **만들기, 업데이트 및 세부 정보 시나리오에 대 한 작업 메서드를 추가** (그림 8 참조).
3. 클릭 합니다 **추가** 프로젝트에 새 컨트롤러를 추가 하려면 단추입니다.

다음이 단계를 완료 한 후 목록 1에서 컨트롤러 생성 됩니다. 인덱스 세부 정보를 만들기, 명명 된 메서드에 포함 되어 있는지 확인할 수 있습니다 하 고 편집 합니다. 다음 섹션에서는 이러한 메서드가 작동 하기를 가져오려고 하는 데 필요한 코드를 추가 합니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)

**그림 08**: 새 ASP.NET MVC 컨트롤러 추가 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))


**Listing 1 – Controllers\HomeController.vb**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a>데이터베이스 레코드 목록

Home 컨트롤러의 index () 메서드는 ASP.NET MVC 응용 프로그램에 대 한 기본 메서드입니다. ASP.NET MVC 응용 프로그램을 실행 하는 경우 index () 메서드는 호출 되는 첫 번째 컨트롤러 메서드.

영화 데이터베이스 테이블에서 레코드 목록을 표시할 index () 메서드를 사용 하겠습니다. 알아보겠습니다 데이터베이스의 이점은 앞에서 만든 index () 메서드를 사용 하 여 영화 데이터베이스 레코드를 검색 하는 모델 클래스입니다.

HomeController 클래스 목록 2에서 라는 새 private 필드 포함 되도록 수정 했지만 \_db입니다. MoviesDBEntities 클래스가 나타내는 데이터베이스 모델 및이 클래스는 데이터베이스와 통신 하는 데 사용 했습니다.

또한 목록 2에서 index () 메서드를 수정 했습니다. Index () 메서드는 MoviesDBEntities 클래스를 사용 하 여 영화 데이터베이스 테이블에서 모든 영화 레코드를 검색 합니다. 식을  *\_db입니다. MovieSet.ToList()* 영화 데이터베이스 테이블에서 모든 영화 레코드 목록을 반환 합니다.

동영상 목록 보기에 전달 됩니다. 뷰 데이터와 뷰에 전달 가져옵니다 View() 메서드에 전달 되는 항목입니다.

**2 – Controllers/HomeController.vb (수정 된 인덱스 메서드)를 나열 합니다.**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

Index () 메서드 Index 라는 뷰를 반환 합니다. 영화 데이터베이스 레코드의 목록을 표시 하려면이 보기를 생성 해야 합니다. 아래 단계를 수행합니다.


프로젝트를 빌드하면 해야 (메뉴 옵션을 선택 **빌드, 솔루션 빌드**) 열기 전에 **뷰 추가** 대화 상자 또는 없는 클래스에 표시 됩니다는 **데이터 클래스 보기** 드롭다운 목록입니다.


1. 코드 편집기에서 index () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 9 참조).
2. 뷰 추가 대화 상자에서 레이블이 지정 된 확인란을 확인 하십시오 **강력한 형식의 뷰를 만들** 확인란이 선택 되어 있습니다.
3. **콘텐츠 보기** 드롭다운 목록에서 값을 선택 *목록*합니다.
4. **데이터 클래스를 보려면** 드롭다운 목록에서 값을 선택 *MovieApp.Movie*합니다.
5. 만들 새 추가 단추를 클릭 (그림 10 참조)를 확인 합니다.

다음이 단계를 완료 하면 Index.aspx 라는 새 뷰 Views\Home 폴더에 추가 됩니다. 인덱스 뷰의 내용은 목록 3에 포함 됩니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)

**그림 09**: 뷰 컨트롤러 작업에서 추가 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)

**그림 10**: 뷰 추가 대화 상자를 사용 하 여 새 보기 만들기 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))


[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

인덱스 보기에는 모든 HTML 표 내의 영화 데이터베이스 테이블에서 영화 레코드를 표시합니다. 뷰에 For ViewData.Model 속성으로 표현 하는 각 영화를 반복 하는 각 루프입니다. 그런 다음 F5 키를 눌러 응용 프로그램을 실행 하면 그림 11에서 웹 페이지를 볼 수 있습니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)

**그림 11**: 인덱스 보기 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))


## <a name="creating-new-database-records"></a>새 데이터베이스 레코드 만들기

이전 섹션에서 만든 인덱스 보기에 새 데이터베이스 레코드를 만들기 위한 링크가 포함 되어 있습니다. 보겠습니다 논리를 구현 하 고 새 영화 데이터베이스 레코드를 만드는 데 필요한 보기를 만듭니다.

Home 컨트롤러 create () 라는 두 개의 메서드도 포함 합니다. 첫 번째 create () 메서드 매개 변수가 없습니다. Create () 메서드의이 오버 로드는 새 영화 데이터베이스 레코드를 만들기 위한 HTML 폼을 표시 하는 데 사용 됩니다.

두 번째 create () 메서드가 FormCollection 매개 변수입니다. Create () 메서드의이 오버 로드는 서버에 새 영화를 만들기 위한 HTML 폼 게시 될 때 호출 됩니다. 이 두 번째 create () 메서드 메서드가 HTTP Post 작업을 수행 하지 않으면 호출 되는 것을 방지 하는 AcceptVerbs 특성에 있는지 확인 합니다.

이 두 번째 create () 메서드 4의 업데이트 된 HomeController 클래스에서 수정 되었습니다. 새 버전의 create () 메서드 영화 매개 변수를 허용 하 고 영화 데이터베이스 테이블에 새 영화를 삽입 하기 위한 논리가 포함 합니다.

> [!NOTE] 
> 
> 바인딩 특성을 확인 합니다. HTML 양식에서 영화 Id 속성을 업데이트 하려고 하지 때문에이 속성을 명시적으로 제외 해야 합니다.


**4-Controllers\HomeController.vb (수정 된 Create 메서드)를 나열 합니다.**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

Visual Studio를 사용 하면 쉽게 새 동영상 데이터베이스를 만들기 위한 양식 만들 (그림 12 참조)를 기록 합니다. 아래 단계를 수행합니다.

1. 코드 편집기에서 create () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가**합니다.
2. 레이블이 지정 된 확인란을 확인 하십시오 **강력한 형식의 뷰를 만들** 확인란이 선택 되어 있습니다.
3. **콘텐츠 보기** 드롭다운 목록에서 값을 선택 *만들기*합니다.
4. **데이터 클래스를 보려면** 드롭다운 목록에서 값을 선택 *MovieApp.Movie*합니다.
5. 클릭 합니다 **추가** 새 뷰를 만들려면 단추입니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)

**그림 12**: 만들기 뷰 추가 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))


Visual Studio에서 자동으로 목록 5에서 뷰를 생성 합니다. 이 뷰는 각 영화 클래스의 속성에 해당 하는 필드를 포함 하는 HTML 폼을 포함 합니다.

**Listing 5 – Views\Home\Create.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> 뷰 추가 대화 상자에서 생성 된 HTML 양식 Id 양식 필드를 생성 합니다. Id 열이 Id 열 이기 때문에이 양식 필드가 필요 하지 않습니다 하 고 안전 하 게 제거할 수 있습니다.


만들기 뷰를 추가한 후에 데이터베이스에 새 영화 레코드를 추가할 수 있습니다. F5 키를 눌러 응용 프로그램을 실행 하 고 그림 13에서 양식을 보려면 새로 만들기 링크를 클릭 합니다. 완료 하 고 양식을 제출 하는 경우 새 영화 데이터베이스 레코드가 만들어집니다.

표시 양식 유효성 검사를 자동으로 가져옵니다. 동영상, 릴리스 날짜를 입력 하는 것을 잊은 또는 잘못 된 릴리스 날짜를 입력할 경우 그런 다음 양식을 다시 표시 됩니다 하 고 릴리스 날짜 필드를 강조 표시 됩니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)

**그림 13**: 새 영화 데이터베이스 레코드를 만드는 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))


## <a name="editing-existing-database-records"></a>기존 데이터베이스 레코드를 편집합니다.

이전 섹션에서 나열 하 고 새 데이터베이스 레코드를 만들 수 있습니다 하는 방법을 설명 했습니다. 이 최종 섹션에서는 기존 데이터베이스 레코드를 편집할 수는 방법을 설명 합니다.

먼저 편집 양식 생성 해야 합니다. Visual Studio에서 편집 폼에 자동으로 생성 되므로이 단계는 쉽습니다. Visual Studio code 편집기에서 HomeController.vb 클래스를 열고이 단계를 수행 합니다.

1. 코드 편집기에서 되 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 14 참조).
2. 레이블이 지정 된 확인란 **강력한 형식의 뷰를 만들**합니다.
3. **콘텐츠 보기** 드롭다운 목록에서 값을 선택 *편집*합니다.
4. **데이터 클래스를 보려면** 드롭다운 목록에서 값을 선택 *MovieApp.Movie*합니다.
5. 클릭 합니다 **추가** 새 뷰를 만들려면 단추입니다.

Views\Home 폴더 Edit.aspx 라는 새 뷰를 추가이 단계를 완료 합니다. 이 뷰는 영화 레코드 편집에 대 한 HTML 폼을 포함 합니다.


[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)

**그림 14**: 편집 뷰 추가 ([클릭 하 여 큰 이미지 보기](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))


> [!NOTE] 
> 
> 편집 보기 영화 Id 속성에 해당 하는 HTML 폼 필드를 포함 합니다. Id 속성의 값을 편집 하는 사람들이 않으려고 하기 때문에이 양식 필드를 제거 해야 합니다.


마지막으로, 데이터베이스 레코드를 편집을 지원 하도록 해당 Home 컨트롤러를 수정 해야 합니다. 업데이트 된 HomeController 클래스 목록 6에 포함 됩니다.

**6-Controllers\HomeController.vb (편집 메서드)를 나열합니다.**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

6 목록에 추가 논리가 되 메서드의 두 오버 로드를 추가 했습니다. 첫 번째 되 메서드 메서드에 전달 된 Id 매개 변수에 해당 하는 영화 데이터베이스 레코드를 반환 합니다. 데이터베이스에서 동영상 레코드 업데이트를 수행 하는 두 번째 오버 로드 합니다.

알림 원본 동영상을 검색 하 고 데이터베이스의 기존 영화를 업데이트 하려면 ApplyPropertyChanges() 호출 해야 합니다.

## <a name="summary"></a>요약

이 자습서의 목적은 ASP.NET MVC 응용 프로그램을 구축 하는 환경을 파악할 수 있도록 하는 것 이었습니다. ASP.NET MVC 웹 응용 프로그램을 구축 하는 Active Server Pages 또는 ASP.NET 응용 프로그램을 구축 하는 환경을 매우 비슷합니다는 검색 하는 것이 좋겠습니다.

이 자습서에서는 ASP.NET MVC framework의 가장 기본적인 기능만 검사 했습니다. 이후 자습서에서에서는 심층 탐구 컨트롤러, 컨트롤러 작업, 보기, 데이터 보기 및 HTML 도우미와 같은 항목입니다.

> [!div class="step-by-step"]
> [이전](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)
