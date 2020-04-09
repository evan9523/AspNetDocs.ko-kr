---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET 데이터 액세스 - 권장 리소스 | 마이크로 소프트 문서
author: rick-anderson
description: 이 항목에서는 주로 Entity Framework 및 SQL Se를 사용하여 ASP.NET 웹 응용 프로그램의 데이터에 액세스하는 방법에 대한 설명서 리소스에 대한 링크를 제공합니다.
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675786"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET 데이터 액세스 - 권장 리소스

> 이 항목에서는 주로 Entity Framework 및 SQL Server를 사용하여 ASP.NET 웹 응용 프로그램의 데이터에 액세스하는 방법에 대한 설명서 리소스에 대한 링크를 제공합니다.
> 
> 훌륭한 블로그 게시물, [stackoverflow](http://stackoverflow.com) 스레드 또는 유용 할 다른 링크를 알고 있다면 링크가있는 [이메일을 보내주십시오.](mailto:aspnetue@microsoft.com?subject=Data Access Content Map)
> 
> 최종 업데이트 2014년 4월 3일

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [ASP.NET 데이터 액세스 시작](#gettingstarted)
- [Entity Framework를 사용 하 여](#ef)

    - [엔터티 프레임워크 코드 를 먼저 사용](#cf)
    - [엔터티 프레임워크 코드 첫 번째 마이그레이션 사용](#efcfmigrations)
    - [엔터티 프레임워크 데이터베이스 를 먼저 사용하거나 먼저 모델(EF 디자이너) 사용](#efdbf)
    - [엔터티 프레임워크에서 관련 데이터 로드(지연 로드, 기지 로드 및 명시적 로드)](#efrelateddata)
    - [엔터티 프레임워크 성능 최적화](#optimizingef)
    - [엔터티 프레임워크 응용 프로그램에서 동시성 처리](#efconcurrency)
    - [엔터티 프레임워크에 대한 책](#efbooks)
    - [추가 엔터티 프레임워크 리소스](#otherefresources)
- [ASP.NET 웹 양식 응용 프로그램의 데이터 바인딩](#wfdatabinding)

    - [웹 양식 모델 바인딩 사용](#wfmodelbinding)
    - [웹 양식 데이터 원본 컨트롤 사용](#wfdsc)
    - [웹 양식 데이터 바인딩 컨트롤 및 데이터 바인딩 식 사용](#wfdbc)
- [SQL 서버 데이터베이스 작업](#sqlserver)

    - [SQL 서버 익스프레스 LocalDB 데이터베이스로 작업](#sslocaldb)
    - [SQL 서버 익스프레스 데이터베이스 작업](#sse)
    - [Windows Azure SQL 데이터베이스 작업](#ssdb)
    - [SQL 서버와 Windows Azure SQL 데이터베이스 중 선택](#ssdbchoosing)
- [NoSQL 데이터베이스 관리 시스템 작업](#nosql)
- [ASP.NET 응용 프로그램에서 LINQ 쿼리 사용](#linq)
- [동적 데이터 스캐폴딩 사용](#dd)
- [데이터 액세스 보안](#securing)
- [데이터 액세스 성능 최적화](#optimizingdataaccess)
- [데이터베이스 배포](#deploying)
- [웹 서비스를 통해 데이터에 액세스](#webservice)
- [추가 리소스](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>ASP.NET 데이터 액세스 시작

- [데이터 저장소 옵션(Windows Azure를 사용하여 실제 클라우드 앱 빌드)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md). 클라우드를 위한 개발에 관한 전자책의 장. 관계형 데이터베이스에 익숙한 많은 개발자가 간과하는 경향이 있는 대안으로 NoSQL 데이터베이스를 소개합니다. 관계형 또는 NoSQL을 선택하거나 특정 플랫폼을 선택할 때 고려해야 할 사항에 대한 지침을 제공합니다.
- [ASP.NET 데이터 액세스](https://msdn.microsoft.com/library/ms178359.aspx) 옵션(MSDN)을 참조하십시오. ASP.NET 관계형 데이터베이스에 대한 데이터 액세스 옵션 소개 및 시나리오에 적합한 플랫폼 및 액세스 방법을 선택하는 방법에 대한 지침입니다.
- [관계형 데이터베이스](http://en.wikipedia.org/wiki/Relational_database). 위키백과). 관계형 데이터베이스로 작업하지 않은 경우 관계형 데이터베이스 용어 및 개념에 대한 소개는 이 페이지를 참조하십시오. 특히 SQL Server에 대한 소개는 이 항목의 후반부에서 [SQL Server 데이터베이스로 작업하는](#sqlserver) 것을 참조하십시오.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Entity Framework를 사용 하 여

- [엔터티 프레임워크 개발 접근](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) 방식(MSDN). 엔터티 프레임워크 개발 접근 방식을 선택하는 방법에 대한 지침은 데이터베이스 우선, 모델 우선 또는 코드 우선입니다.

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>엔터티 프레임워크 코드 를 먼저 사용

다음 자습서에서는 다운로드 가능한 샘플 응용 프로그램을 제공합니다.

- [MVC 5를 사용하여 EF 6을 시작하기](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). 연결 복원력, 명령 차단 및 비동기와 같은 마이그레이션 및 EF 6 기능을 비롯한 다양한 엔터티 프레임워크 코드 코드 First 시나리오를 다룹니다. EF [5 / MVC 4 시리즈의](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)업데이트 된 버전입니다. 이전 시리즈에는 새 시리즈에 포함되지 않은 리포지토리 및 작업 단위 패턴에 대한 자습서가 포함되어 있습니다.
- [ASP.NET MVC 5 소개](../mvc/overview/getting-started/introduction/getting-started.md). 엔터티 프레임워크 코드 첫 번째 시나리오의 범위를 좁히지만 MVC 기능을 도입하는 보다 포괄적인 작업을 수행합니다.
- [모델 바인딩 및 웹 양식](https://go.microsoft.com/fwlink/?LinkId=286117). 웹 양식 응용 프로그램에서 코드 우선을 사용합니다.
- [ASP.NET 4.5 웹 양식을 시작 .](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md) 코드 First의 일부 적용 범위가 있는 웹 양식 소개. 모델 바인딩을 사용합니다.
- [MVC 뮤직 스토어](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md). 또한 회원 및 권한 부여를 구현하는 전자 상거래 MVC 3 응용 프로그램에서 코드 우선을 사용합니다. 여기에 사용되는 MVC 버전 및 ASP.NET 멤버십(인증 및 권한 부여) 시스템은 오래되었습니다. ASP.NET 멤버십에 대한 최신 정보는 을 [https://asp.net/identity](https://asp.net/identity)참조하십시오.

기타 리소스:

- [엔터티 프레임워크 - 기존 데이터베이스에 대한 코드 우선](https://msdn.microsoft.com/data/jj200620). Msdn. 기존 데이터베이스에서 Code First를 사용하는 방법을 보여 주는 비디오 및 연습입니다.
- [데이터 개발자 센터 - 엔터티 프레임 워크](https://msdn.microsoft.com/data/ef). Msdn. 엔터티 프레임워크 팀에서 만들고 유지 관리하는 엔터티 프레임워크 설명서에 대한 가이드는 [시작 하기](https://msdn.microsoft.com/data/ee712907) 링크를 참조하십시오.

이 항목의 후반부에 있는 엔터티 프레임워크 및 [추가 엔터티 프레임워크 리소스에](#otherefresources) [대한 책도](#efbooks) 참조하십시오.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>엔터티 프레임워크 코드 첫 번째 마이그레이션 사용

위에 나열된 코드 First 자습서의 대부분은 마이그레이션을 다룹니다. 다음 리소스도 참조하십시오.

- [Visual Studio를 사용한 ASP.NET 웹 배포](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)(영문). 코드 First 마이그레이션을 사용하여 데이터베이스를 배포하는 방법을 보여 주는 2부작 자습서 시리즈입니다.
- [Windows Azure 웹 사이트에 멤버 자격, OAuth 및 SQL 데이터베이스를 사용하여 보안 ASP.NET MVC 5 앱을 배포합니다.](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) 마이크로소프트 Azure). 마이그레이션을 사용하여 멤버 자격 및 응용 프로그램 데이터를 Azure에 배포하는 방법
- [비주얼 스튜디오 및 ASP.NET 대한 웹 배포 개요.](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment) 코드 첫 번째 마이그레이션이 Visual Studio 웹 배포 기능에 통합되는 방법에 대한 설명은 **Visual Studio의 데이터베이스 배포 구성** 섹션을 참조하십시오.
- [데이터 개발자 센터 - 코드 첫 번째](https://msdn.microsoft.com/data/jj591621) 마이그레이션(MSDN). 엔터티 프레임워크 팀의 마이그레이션 설명서입니다.
- [마이그레이션 스크린캐스트 시리즈](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). EF 블로그). 코드 첫 번째 마이그레이션의 고급 주제에 대한 세 가지 비디오입니다.
- [ASP.NET 웹 페이지 사이트와 코드 첫 번째 마이그레이션](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites). 마이크도팅 블로그). Visual Studio 클래스 라이브러리 프로젝트에 데이터 컨텍스트를 배치하여 ASP.NET 웹 페이지 사이트에서 Code First 마이그레이션을 사용하는 방법을 보여 주시면 됩니다.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>엔터티 프레임워크 데이터베이스 를 먼저 사용하거나 먼저 모델(EF 디자이너) 사용

- [MVC 5를 사용하여 엔터티 프레임워크 6 데이터베이스를 먼저 시작하기](../mvc/overview/getting-started/database-first-development/setting-up-database.md). 서버 탐색기에서 스크립트를 실행하여 데이터베이스를 만든 다음 Entity Framework 디자이너를 사용하여 데이터 모델을 만듭니다. 간단한 CRUD 웹 페이지를 만드는 방법을 보여 주며, 다른 데이터 처리 함수의 경우 모든 EF 워크플로가 동일한 DbContext API를 사용하기 때문에 Code First 자습서 중 하나를 따를 수 있습니다.

다음 리소스는 더 오래되었습니다. 엔터티 프레임워크의 버전 4.0을 사용하고 Web Forms 응용 프로그램에서 데이터 바인딩에 데이터 원본 컨트롤을 사용하려는 경우에 유용합니다.

- [엔터티 프레임워크 4.0을 시작하기](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). **EntityDataSource** 컨트롤을 사용하는 방법을 보여 주실 수 있습니다.
- [엔터티 프레임워크를 계속(개체](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)데이터 **소스** 컨트롤을 사용하는 방법을 보여 주어 도있습니다. 동시성 처리에 대한 자습서, EF 성능에 대한 자습서 및 EF 4.0의 새로운 내용에 대한 자습서가 포함되어 있습니다.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>엔터티 프레임워크에서 관련 데이터 처리(지연 로드, 즉시 로드 및 명시적 로드)

- [ASP.NET MVC 응용 프로그램에서 엔터티 프레임워크를 사용하여 관련 데이터 읽기.](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 코드 첫째, MVC 샘플 응용 프로그램입니다. 표시된 메서드는 Web Forms 모델 바인딩 및 데이터베이스 첫 번째 워크플로에도 적용됩니다.
- [데이터 개발자 센터 - 관련 엔터티](https://msdn.microsoft.com/data/jj574232) 로드(MSDN) 관련 데이터 로드에 대한 엔터티 프레임워크 팀의 설명서입니다.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>엔터티 프레임워크 성능 최적화

- [ASP.NET 응용 프로그램에 대한 고급 엔터티 프레임워크 시나리오.](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md) 사용자 고유의 SQL 문을 실행하거나 자신의 저장 프로시저를 호출하는 방법, 변경 내용 검색을 사용하지 않도록 설정하는 방법 및 변경 내용을 저장할 때 유효성 검사를 사용하지 않도록 설정하는 방법을 보여 줍니다.
- [엔터티 프레임워크 5(MSDN)에 대한 성능 고려 사항입니다.](https://msdn.microsoft.com/data/hh949853)
- [성능 고려 사항(엔터티 프레임워크)](https://msdn.microsoft.com/library/cc853327) (MSDN)
- [ASP.NET 웹 응용 프로그램에서 엔터티 프레임워크로 성능 극대화.](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md) 엔터티 프레임워크 4.0에 적용됩니다.
- 이 항목의 ASP.NET [데이터 액세스 최적화를](#optimizingdataaccess) 참조하십시오.

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>엔터티 프레임워크 응용 프로그램에서 동시성 처리

- [ASP.NET MVC 응용 프로그램에서 엔터티 프레임워크와 동시성 처리.](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 코드 첫째, MVC 샘플 응용 프로그램을 사용 하 여 DbContext API입니다.
- [데이터 개발자 센터 – 낙관적 동시성](https://msdn.microsoft.com/data/jj592904) 패턴(MSDN). 엔터티 프레임워크 팀의 동시성 설명서입니다.
- [ASP.NET 웹 응용 프로그램에서 엔터티 프레임 워크와 동시성 처리](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md). 엔터티 프레임워크 4.0에 적용됩니다. 데이터베이스 첫째, ObjectContext API, 웹 양식 샘플 응용 프로그램을 사용 하 여.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>엔터티 프레임워크에 대한 책

- [프로그래밍 엔티티 프레임워크: 줄리](http://shop.oreilly.com/product/0636920022237.do) 러먼과 로완 밀러의 DbContext.
- [프로그래밍 엔티티 프레임 워크: 줄리](http://shop.oreilly.com/product/0636920022220.do) 러먼과 로완 밀러에 의해 코드 먼저.

이 두 책은 모두 현재 권장 되는 기술과 최신. 인터넷에서 사용할 수 있는 것보다 엔터티 프레임워크에 대한 보다 포괄적이면서도 따라하기 쉬운 소개를 제공합니다. 줄리 Lerman에 의해 또 다른 책, [프로그래밍 엔터티 프레임 워크,](http://shop.oreilly.com/product/9780596807252.do) 더 크고 더 포괄적인 하지만 그것은 오래 되 고 그것은 다루는 기술의 많은 더 이상 엔터티 프레임 워크를 사용 하는 권장된 방법. [데이터 개발자 센터의](https://msdn.microsoft.com/data/aa937716) 엔터티 프레임워크 팀에서 권장하는 책 목록 - MSDN 사이트의 책 목록을 참조하십시오.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>기타 엔티티 프레임워크 리소스

- [엔터티 프레임워크(ADO.NET) 팀 블로그](https://blogs.msdn.com/b/adonet/). 최신 정보 및 새로운 개선 사항 발표를 위한 최고의 리소스 중 하나입니다. 다른 EF 관련 블로그의 경우 엔터티 [프레임워크시작의](https://msdn.microsoft.com/data/ee712907)블로그 롤을 참조하십시오.
- [MSDN 매거진](https://msdn.microsoft.com/magazine/default.aspx). 엔터티 프레임워크와 관련된 항목에 대해 자주 다루는 **데이터 요소** 열을 참조하십시오.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>ASP.NET 웹 양식 응용 프로그램의 데이터 바인딩

- [ASP.NET 웹 양식 데이터 액세스](https://msdn.microsoft.com/library/jj822927.aspx) 옵션(MSDN)<a id="wfmodelbinding"></a>.

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>웹 양식 모델 바인딩 사용

- [모델 바인딩 및 웹 양식](https://go.microsoft.com/fwlink/?LinkId=286117). EF 코드 를 먼저 사용하는 자습서 시리즈.
- [웹 양식 모델 바인딩 1부: 데이터 선택(Scott](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) Guthrie의 블로그). 이러한 이전 블로그 게시물에서 현재 ItemType이라는 이름의 속성은 ModelType으로 명명되었지만 그렇지 않으면 포함된 정보가 유효합니다.
- [웹 양식 모델 바인딩 2부: 데이터 필터링(Scott](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) Guthrie의 블로그).
- [웹 양식 모델 바인딩 3 부: 업데이트 및 유효성 검사](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (Scott Guthrie의 블로그).
- [ASP.NET 4.5 웹 양식 모델 바인딩.](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md) (비디오)를 참조하십시오.
- [모델 바인딩 파트 1 - 데이터](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) 선택(비디오)
- [모델 바인딩 파트 2 -](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) 필터링(비디오)
- [ASP.NET 4.5 웹 양식 시작 - 데이터 항목 및 세부 정보를 표시합니다.](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>웹 양식 데이터 원본 컨트롤 사용

- [데이터 원본 웹 서버](https://msdn.microsoft.com/library/ms247258.aspx) 컨트롤(MSDN).
- 엔터티 프레임워크 6(Microsoft 웹 개발 [블로그)에 대한 동적 데이터 공급자 및 EntityDataSource 제어의 릴리스를 발표합니다.](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>웹 양식 데이터 바인딩 컨트롤 및 데이터 바인딩 식 사용

- [모델 바인딩 및 웹 양식](https://go.microsoft.com/fwlink/?LinkId=286117). EF 코드 를 먼저 사용하는 자습서 시리즈입니다.
- [ASP.NET 4.5 웹 양식 시작 - 데이터 항목 및 세부 정보를 표시합니다.](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)
- [강력하게 입력 된 데이터 컨트롤](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (스콧 거스리의 블로그).
- [강력하게 입력된 데이터](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) 컨트롤(비디오)
- [ASP.NET 4.5 웹 양식 강력한 형식의 데이터 컨트롤](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (비디오).
- [데이터 바인딩된 웹 서버](https://msdn.microsoft.com/library/ms228214.aspx) 컨트롤(MSDN).
- [데이터 바인딩 식](https://msdn.microsoft.com/library/ms178366.aspx) 개요(MSDN). 이 페이지는 **Eval** 및 **Bind에만 다룹니다.** **항목** 및 **BindItem**을 포함하도록 업데이트되지 않았습니다.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>SQL 서버 데이터베이스 작업

- [SQL 서버 데이터베이스](https://msdn.microsoft.com/library/hh230827.aspx) 기능(MSDN)입니다. 다양한 SQL Server 항목에 대한 일반적인 소개는 TOC의 항목 아래에 있는 항목을 참조하십시오.
- [SQL 서버](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) 에디션(MSDN)입니다. 사용 가능한 SQL Server 버전에 대한 요약으로 각 버전에 대한 자세한 정보에 대한 링크가 있습니다.
- [ASP.NET 웹 응용 프로그램(MSDN)에 대한 SQL 서버 연결 문자열입니다.](https://msdn.microsoft.com/library/jj653752.aspx)
- [ASP.NET 웹 응용 프로그램(MSDN)에 SQL 서버 컴팩트를 사용합니다.](https://msdn.microsoft.com/library/ms247257.aspx)
- [Microsoft SQL 서버: 데이터베이스 제품 샘플.](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md) 어드벤처웍스 데이터베이스 샘플.
- [샘플 데이터베이스 설치](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). 여기에 표시된 방법 외에도 샘플 .mdf 파일 중 하나를 웹 프로젝트의\_앱 데이터 폴더에 다운로드하고 데이터베이스를 LocalDB로 변환하고 LocalDB 연결 문자열을 만들 수도 있습니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 [방법을 참조하십시오: LocalDB로 업그레이드.](https://msdn.microsoft.com/library/hh873188.aspx)

SQL Server Express 및 LocalDB로 작업하고 SQL Server와 SQL 데이터베이스 중에서 선택하는 방법에 대한 다음 섹션도 참조하십시오.

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>SQL 서버 익스프레스 LocalDB 데이터베이스로 작업

- [SQL 서버 익스프레스 2012 로컬DB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). 로컬DB에 대한 공식 MSDN 소개.
- [ASP.NET 웹 응용 프로그램(MSDN)에 대한 SQL 서버 연결 문자열입니다.](https://msdn.microsoft.com/library/jj653752.aspx)
- [방법: 로컬DB(MSDN)로 업그레이드합니다.](https://msdn.microsoft.com/library/hh873188.aspx) 이전 버전의 SQL Server Express에서 LocalDB로 .mdf 파일을 마이그레이션하는 방법. [SQL Server 2012 샘플 데이터베이스](https://go.microsoft.com/fwlink/?linkid=117483)중 하나를 다운로드하는 경우에도 이 프로세스를 거쳐야 합니다.
- 향상된 SQL 익스프레스(SQL Server Express [블로그)인 LocalDB를 소개합니다.](https://go.microsoft.com/fwlink/?LinkId=234375) 로컬DB가 MSDN에 포함된 것보다 생성된 이유에 대한 배경 지식이 더 있습니다.
- [LocalDB: 내 데이터베이스는 어디에 있습니까?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL Server 익스프레스 블로그)를 참조하십시오. LocalDB 데이터베이스 파일이 생성되는 위치에 대한 정보입니다.
- [전체 IIS를 사용하는 LocalDB, 파트 1: 사용자 프로필(SQL](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) Server Express 블로그). LocalDB는 IIS와 함께 작동하도록 설계되지 않았습니다. 이 일련의 블로그 게시물은 문제와 몇 가지 해결 방법을 설명합니다.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>SQL 서버 익스프레스 데이터베이스 작업

- [ASP.NET 웹 응용 프로그램(MSDN)에 대한 SQL 서버 연결 문자열입니다.](https://msdn.microsoft.com/library/jj653752.aspx) SQL Server Express에서 AttachDBFileName 연결 문자열 설정을 사용하는 경우 특히 이 페이지의 사용자 인스턴스 섹션을 참조하십시오.
- [로컬 SQL Server Express 2008(SQL Server Express 블로그)의 소유권을 가져가는 방법](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) SQL Server Express 인스턴스의 관리자가 아니므로 SQL Server Express 데이터베이스에서 작업할 수 없는 일반적인 문제입니다. 기본적으로 SQL Server Express를 설치한 사람만 관리자입니다. 이 블로그에서는 컴퓨터의 관리자인 경우 SQL Server Express 관리자를 직접 만드는 방법에 대해 설명합니다.
- [ASP.NET 웹 응용 프로그램이 프로덕션 환경에서 SQL Server Express 데이터베이스를 사용할 수 있습니까?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN)을 입력합니다.

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Windows Azure SQL 데이터베이스 작업

- Windows Azure 웹 사이트(Microsoft Azure [사이트)에 멤버십, OAuth 및 SQL 데이터베이스를 사용하여 보안 ASP.NET MVC 앱을 배포합니다.](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
- [SQL 데이터베이스(마이크로소프트](https://docs.microsoft.com/azure/sql-database/) Azure 사이트). 튜토리얼 및 방법 가이드를 시작하기.
- [윈도우 Azure SQL](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) 데이터베이스(MSDN). MSDN의 SQL 데이터베이스에 대한 목차 테이블의 최상위 노드입니다.
- [윈도우 Azure SQL 데이터베이스 테크넷 위키 기사 인덱스](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (마이크로 소프트 테크넷 사이트).
- [일시적인 오류 처리 애플리케이션 블록](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx). 제한으로 인한 일시적인 네트워크 오류 및 연결 오류를 처리할 수 있는 프레임워크입니다. NuGet 패키지에서 사용 가능: [엔터프라이즈 라이브러리 5.0 - 일시적인 오류 처리 응용 프로그램 블록](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling).
- [SQL 데이터베이스 및 엔터티 프레임워크(MSDN)를 시작했습니다.](https://msdn.microsoft.com/data/jj556244)
- [윈도우 Azure 교육 키트](https://www.microsoft.com/download/details.aspx?id=8396) (마이크로 소프트 다운로드 센터). SQL 데이터베이스에 대한 실습 랩이 포함되어 있습니다.
- [윈도우 Azure SQL 데이터베이스 커뮤니티 포럼](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [Windows Azure SQL 데이터베이스(MSDN)로 이동합니다.](https://msdn.microsoft.com/library/ff803375.aspx) Microsoft 패턴 및 사례 팀의 포괄적인 종단 간 시나리오의 한 장입니다. 마이그레이션하려는 이유와 SQL Server에서 SQL Database로 마이그레이션하는 방법을 다룹니다.
- [SQL 서버 데이터베이스를 MSDN(Windows Azure SQL 데이터베이스)으로 마이그레이션합니다.](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx)
- [SQL 데이터베이스 마이그레이션 마법사](http://sqlazuremw.codeplex.com/). SQL Database에서 데이터베이스를 마이그레이션하기 위한 오픈 소스 도구입니다.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>SQL 서버와 Windows Azure SQL 데이터베이스 중 선택

- [SQL 서버를 Windows Azure SQL 데이터베이스(Microsoft](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) TechNet 사이트)와 비교합니다.
- [Windows Azure SQL 데이터베이스로의 데이터 마이그레이션: 도구 및](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) 기술(MSDN). SQL Server와 SQL Database를 비교하고 SQL Server에서 SQL 데이터베이스로 마이그레이션할 시기에 대한 지침을 제공하는 섹션을 포함합니다.
- [윈도우 Azure SQL 데이터베이스 배달 가이드](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (마이크로 소프트 테크넷 사이트).
- [SQL 서버 기능 제한(Windows Azure SQL 데이터베이스)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN)
- [Windows Azure 테이블 저장소 및 Windows Azure SQL 데이터베이스 - 비교 및](https://msdn.microsoft.com/library/jj553018.aspx) 대조(MSDN). Windows Azure에 배포하는 응용 프로그램의 경우 Windows Azure 테이블 저장소가 Windows Azure SQL Database의 대안일 수 있습니다. 이 항목에서는 이러한 대안 중에서 결정하는 데 도움이 됩니다.
- [윈도우 Azure SQL](https://msdn.microsoft.com/library/windowsazure/ee336279) 데이터베이스(MSDN).
- [지침 및 제한 사항(Microsoft Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>NoSQL 데이터베이스 관리 시스템 작업

- [윈도우 Azure 데이터 서비스](https://www.windowsazure.com/develop/net/data/) (마이크로 소프트 Azure 사이트). 테이블 [서비스 기능 가이드와](https://docs.microsoft.com/azure/) 페이지의 **빅 데이터** 섹션을 참조하십시오.
- [저장소 테이블, 큐 및 Blob(Microsoft Azure 사이트)을 사용하는 ASP.NET 다중 계층 응용 프로그램입니다.](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) Windows Azure 저장소 NoSQL 테이블을 사용하는 다운로드 가능한 샘플 응용 프로그램이 있는 종단 간 자습서입니다.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>ASP.NET 응용 프로그램에서 LINQ 쿼리 사용

- [ASP.NET 데이터 액세스](https://msdn.microsoft.com/library/ms178359.aspx#linq) 옵션(MSDN)을 참조하십시오. LINQ에 대한 소개가 포함되어 있습니다.
- [LINQ 교육 비디오](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (조 스태그너의 블로그).
- [ASP.NET 동적 LINQ 리소스에 대한 링크가 있는 포럼 스레드.](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>동적 데이터 스캐폴딩 사용

- [동적 데이터 프로젝트](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) 템플릿(MSDN). 동적 데이터 프로젝트를 사용할 시기에 대한 지침입니다.
- ASP.NET 동적 데이터(MSDN)를 [사용합니다.](https://msdn.microsoft.com/library/ee845452.aspx)

<a id="securing"></a>

## <a name="securing-data-access"></a>데이터 액세스 보안

- [ASP.NET(MSDN)에서 데이터 액세스 보안.](https://msdn.microsoft.com/library/ms178375.aspx)
- [보안 고려 사항(엔터티 프레임워크)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN)
- [방법: MSDN(데이터 원본 컨트롤)을 사용할 때 연결 문자열을 보호합니다.](https://msdn.microsoft.com/library/ms178372.aspx)

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>데이터 액세스 성능 최적화

- [ASP.NET 성능](https://msdn.microsoft.com/library/cc668225.aspx) 개요(MSDN).
- [ASP.NET](https://msdn.microsoft.com/library/xsbfdd8c.aspx) 캐싱(MSDN)입니다.
- [ASP.NET 성능](https://msdn.microsoft.com/library/ff647787) 향상(MSDN) 이 페이지 상단에 "사용 중지된 콘텐츠" 경고가 있지만 대부분의 정보는 여전히 관련이 있으며 유사한 업데이트된 리소스가 없습니다.
- [MSDN(SQL 서버 성능 향상)](https://msdn.microsoft.com/library/ff647793) 이전 링크와 동일한 주석입니다.

이 항목의 앞에서 [엔터티 프레임워크 성능 최적화도](#optimizingef) 참조하십시오.

<a id="deploying"></a>

## <a name="deploying-a-database"></a>데이터베이스 배포

- [ASP.NET 웹 배포 - 권장](aspnet-web-deployment-content-map.md) 리소스(MSDN)입니다.

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>웹 서비스를 통해 데이터에 액세스

- [MSDN(웹 서비스)을 통해 데이터에 액세스합니다.](https://msdn.microsoft.com/library/ms178359.aspx#webservice) 웹 API와 WCF를 사용하는 시기에 대한 지침입니다.
- [ASP.NET 웹 API를 시작하십시오.](../web-api/index.md)
- [WCF 데이터](https://msdn.microsoft.com/data/bb931106) 서비스(MSDN).

<a id="additional"></a>

## <a name="additional-resources"></a>추가 리소스

- [ASP.NET 데이터 액세스 FAQ](https://msdn.microsoft.com/library/jj653753.aspx) (MSDN).
- [ASP.NET 웹 양식 자습서 - 데이터](../web-forms/overview/data-access/index.md). 이러한 자습서의 대부분은 비교적 오래 되었습니다. 먼저 ASP.NET [데이터 액세스 옵션](https://msdn.microsoft.com/library/ms178359.aspx) 및 [데이터 저장소 옵션(Windows Azure를 사용하여 실제 클라우드 앱 빌드)을](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) 읽어서 시나리오에 적합하지 않은 데이터 액세스 방법을 너무 멀리 하지 않도록 하십시오.
- [ASP.NET MVC 콘텐츠 맵.](../mvc/overview/getting-started/recommended-resources-for-mvc.md)
- [ASP.NET 웹 페이지 자습서 - 데이터](../web-pages/overview/data/index.md).
- [MSDN(비주얼 스튜디오)의 데이터에 액세스합니다.](https://msdn.microsoft.com/library/wzabh8c4.aspx) 이 콘텐츠 맵과 유사하지만 ASP.NET 아닌 Visual Studio에 중점을 둔 링크 목록을 제공합니다.
