---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET 데이터 액세스-권장 리소스 | Microsoft Docs
author: rick-anderson
description: 이 항목에서는 ASP.NET 웹 응용 프로그램의 데이터에 액세스 하는 방법에 대 한 설명서 리소스 링크를 제공 합니다 .이 링크는 주로 Entity Framework 및 SQL Se ...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345147"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET 데이터 액세스 - 권장 리소스

> 이 항목에서는 주로 Entity Framework 및 SQL Server를 사용 하 여 ASP.NET 웹 응용 프로그램의 데이터에 액세스 하는 방법에 대 한 설명서 리소스 링크를 제공 합니다.
> 
> 유용한 블로그 게시물, [stackoverflow](http://stackoverflow.com) 스레드 또는 유용한 다른 링크를 알고 있는 경우 링크가 포함 된 [전자 메일을 보내 주세요](mailto:aspnetue@microsoft.com?subject=Data Access Content Map) .
> 
> 마지막 업데이트 4/3/2014

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [ASP.NET에서 데이터 액세스 시작](#gettingstarted)
- [Entity Framework를 사용 하 여](#ef)

    - [Entity Framework Code First 사용](#cf)
    - [Entity Framework Code First 마이그레이션 사용](#efcfmigrations)
    - [Entity Framework Database First 또는 Model First 사용 (EF Designer)](#efdbf)
    - [Entity Framework에서 관련 데이터 로드 (지연 로드, 즉시 로드 및 명시적 로드)](#efrelateddata)
    - [Entity Framework 성능 최적화](#optimizingef)
    - [Entity Framework 응용 프로그램에서 동시성 처리](#efconcurrency)
    - [Entity Framework에 대 한 서적](#efbooks)
    - [추가 Entity Framework 리소스](#otherefresources)
- [ASP.NET Web Forms 응용 프로그램의 데이터 바인딩](#wfdatabinding)

    - [Web Forms 모델 바인딩 사용](#wfmodelbinding)
    - [Web Forms 데이터 소스 컨트롤 사용](#wfdsc)
    - [Web Forms Data-Bound 컨트롤 및 Data-Binding 식 사용](#wfdbc)
- [SQL Server 데이터베이스 작업](#sqlserver)

    - [SQL Server Express LocalDB 데이터베이스 작업](#sslocaldb)
    - [SQL Server Express 데이터베이스 작업](#sse)
    - [Windows Azure SQL Database 사용](#ssdb)
    - [SQL Server 및 Windows Azure SQL Database 중에서 선택](#ssdbchoosing)
- [NoSQL 데이터베이스 관리 시스템 작업](#nosql)
- [ASP.NET 응용 프로그램에서 LINQ 쿼리 사용](#linq)
- [Dynamic Data 스 캐 폴딩 사용](#dd)
- [데이터 액세스 보안](#securing)
- [데이터 액세스 성능 최적화](#optimizingdataaccess)
- [데이터베이스 배포](#deploying)
- [웹 서비스를 통해 데이터 액세스](#webservice)
- [추가 리소스](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>ASP.NET에서 데이터 액세스 시작

- [데이터 저장소 옵션 (Microsoft Azure를 사용 하 여 클라우드 앱 Real-World 빌드)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md). 클라우드의 개발에 대 한 전자 서적 장. 에서는 관계형 데이터베이스에 익숙한 많은 개발자 들이 간과 하기 쉬우므로 NoSQL 데이터베이스를 소개 합니다. 관계형 또는 NoSQL을 선택 하거나 특정 플랫폼을 선택할 때 고려할 사항에 대 한 지침을 제공 합니다.
- MSDN ( [ASP.NET Data Access Options](https://msdn.microsoft.com/library/ms178359.aspx) ). ASP.NET에 대 한 관계형 데이터베이스에 대 한 데이터 액세스 옵션을 소개 하 고, 시나리오에 적합 한 플랫폼 및 액세스 방법을 선택 하는 방법에 대 한 지침을 제공 합니다.
- [관계형 데이터베이스](http://en.wikipedia.org/wiki/Relational_database). 위키백과). 관계형 데이터베이스에 대 한 작업을 수행 하지 않은 경우 관계형 데이터베이스 용어 및 개념에 대 한 소개는이 페이지를 참조 하세요. 특히 SQL Server에 대 한 소개는이 항목의 뒷부분에 나오는 [SQL Server 데이터베이스 작업](#sqlserver) 을 참조 하세요.

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>Entity Framework를 사용 하 여

- [Entity Framework 개발 방법](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf) (MSDN) Entity Framework 개발 방법 Database First, Model First 또는 Code First를 선택 하는 방법에 대 한 지침입니다.

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>Entity Framework Code First 사용

다음 자습서에서는 다운로드 가능한 샘플 응용 프로그램을 제공 합니다.

- [MVC 5를 사용 하 여 EF 6 시작](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 연결 복원 력, 명령 가로채기, 비동기 등의 마이그레이션 및 EF 6 기능을 비롯 한 다양 한 Entity Framework Code First 시나리오를 다룹니다. [EF 5/MVC 4 시리즈](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)의 업데이트 된 버전입니다. 이전 시리즈는 리포지토리에 대 한 자습서와 새 계열에 포함 되지 않은 작업 단위 패턴을 포함 합니다.
- [ASP.NET MVC 5 소개](../mvc/overview/getting-started/introduction/getting-started.md). 보다 좁은 범위의 Entity Framework Code First 시나리오를 다루지만 MVC 기능을 보다 포괄적으로 소개 합니다.
- [모델 바인딩 및 Web Forms](https://go.microsoft.com/fwlink/?LinkId=286117) Web Forms 응용 프로그램에서 Code First를 사용 합니다.
- [ASP.NET 4.5 Web Forms를 시작](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)합니다. Code First의 일부 검사를 사용 하는 Web Forms에 대 한 소개입니다. 모델 바인딩을 사용 합니다.
- [MVC Music 저장소](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md). 는 멤버 자격과 권한 부여를 구현 하는 전자 상거래 MVC 3 응용 프로그램에서 Code First를 사용 합니다. 여기에 사용 된 MVC 버전 및 ASP.NET 멤버 자격 (인증 및 권한 부여) 시스템은 오래 된 버전입니다. ASP.NET 멤버 자격에 대 한 최신 정보는를 참조 [https://asp.net/identity](https://asp.net/identity) 하세요.

기타 리소스:

- [Entity Framework-기존 데이터베이스에 Code First](https://msdn.microsoft.com/data/jj200620)합니다. 알려면. 기존 데이터베이스에서 Code First를 사용 하는 방법을 보여 주는 비디오 및 연습입니다.
- [데이터 개발자 센터-Entity Framework](https://msdn.microsoft.com/data/ef). 알려면. Entity Framework 팀에서 만들고 유지 관리 하는 Entity Framework 설명서에 대 한 지침은 [시작](https://msdn.microsoft.com/data/ee712907) 링크를 참조 하세요.

이 항목의 뒷부분에 나오는 Entity Framework 및 [추가 Entity Framework 리소스](#otherefresources) [에 대 한 서적](#efbooks) 도 참조 하세요.

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>Entity Framework Code First 마이그레이션 사용

위에 나열 된 대부분의 Code First 자습서에서는 마이그레이션을 다룹니다. 또한 다음 리소스를 참조 하세요.

- [Visual Studio를 사용 하 여 웹 배포를 ASP.NET](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). Code First 마이그레이션를 사용 하 여 데이터베이스를 배포 하는 방법을 보여 주는 2 부 자습서 시리즈입니다.
- [멤버 자격, OAuth 및 SQL Database가 포함 된 보안 ASP.NET MVC 5 앱을 Windows Azure 웹 사이트에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. Microsoft Azure). 마이그레이션을 사용 하 여 멤버 자격 및 응용 프로그램 데이터를 Azure에 배포 하는 방법을 설명 합니다.
- [Visual Studio 및 ASP.NET의 웹 배포 개요](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment). Code First 마이그레이션 Visual studio 웹 배포 기능에 통합 되는 방법에 대 한 설명은 **Visual studio에서 데이터베이스 배포 구성** 섹션을 참조 하세요.
- [데이터 개발자 센터-Code First 마이그레이션](https://msdn.microsoft.com/data/jj591621) (MSDN). Entity Framework 팀의 마이그레이션 설명서입니다.
- [마이그레이션 동영상 가이드 시리즈](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx). EF 블로그). Code First 마이그레이션의 고급 항목에 대 한 세 가지 비디오
- [ASP.NET 웹 페이지 사이트를 사용 하 여 Code First 마이그레이션](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites)합니다. Mikesdotnetting 블로그). 데이터 컨텍스트를 Visual Studio 클래스 라이브러리 프로젝트에 배치 하 여 ASP.NET 웹 페이지 사이트에서 Code First 마이그레이션을 사용 하는 방법을 보여 줍니다.

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>Entity Framework Database First 또는 Model First 사용 (EF Designer)

- [MVC 5를 사용 하 여 Database First Entity Framework 6부터 시작](../mvc/overview/getting-started/database-first-development/setting-up-database.md)합니다. 서버 탐색기에서 스크립트를 실행 하 여 데이터베이스를 만든 다음 Entity Framework 디자이너를 사용 하 여 데이터 모델을 만듭니다. 간단한 CRUD 웹 페이지를 만드는 방법을 보여 줍니다. 다른 데이터 처리 함수에 대 한 모든 EF 워크플로는 동일한 DbContext API를 사용 하므로 Code First 자습서 중 하나를 따를 수 있습니다.

다음 리소스는 이전 버전입니다. Entity Framework 버전 4.0을 사용 하 고 Web Forms 응용 프로그램의 데이터 바인딩에 데이터 소스 컨트롤을 사용 하려는 경우에 유용 합니다.

- [Entity Framework 4.0를 시작](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)합니다. **EntityDataSource** 컨트롤을 사용 하는 방법을 보여 줍니다.
- [Entity Framework 계속](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)( **ObjectDataSource** 컨트롤을 사용 하는 방법을 보여 줍니다. 동시성 처리에 대 한 자습서, EF 성능에 대 한 자습서 및 EF 4.0의 새로운 기능에 대 한 자습서가 포함 되어 있습니다.

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>Entity Framework에서 관련 데이터 처리 (지연 로드, 즉시 로드 및 명시적 로드)

- [ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련 데이터를 읽습니다](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md). Code First MVC 샘플 응용 프로그램입니다. 표시 되는 메서드는 Web Forms 모델 바인딩과 Database First 워크플로에도 적용 됩니다.
- [데이터 개발자 센터-관련 엔터티 로드](https://msdn.microsoft.com/data/jj574232) (MSDN) 관련 데이터 로드에 대 한 Entity Framework 팀의 설명서입니다.

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>Entity Framework 성능 최적화

- [ASP.NET 응용 프로그램에 대 한 고급 Entity Framework 시나리오](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)입니다. 사용자 고유의 SQL 문을 실행 하거나 사용자 고유의 저장 프로시저를 호출 하는 방법, 변경 검색을 사용 하지 않도록 설정 하는 방법 및 변경 내용을 저장할 때 유효성 검사를 해제 하는 방법을 보여 줍니다.
- [Entity Framework 5에 대 한 성능 고려 사항](https://msdn.microsoft.com/data/hh949853) (MSDN)
- [성능 고려 사항 (Entity Framework)](https://msdn.microsoft.com/library/cc853327) (MSDN)
- [ASP.NET 웹 응용 프로그램에서 Entity Framework를 사용 하 여 성능을 최대화](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)합니다. Entity Framework 4.0에 적용 됩니다.
- 이 항목의 뒷부분에 있는 [ASP.NET 데이터 액세스 최적화](#optimizingdataaccess) 도 참조 하세요.

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>Entity Framework 응용 프로그램에서 동시성 처리

- [ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 동시성 처리](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md). MVC 샘플 응용 프로그램을 사용 하는 Code First DbContext API.
- [데이터 개발자 센터 – 낙관적 동시성 패턴](https://msdn.microsoft.com/data/jj592904) (MSDN). Entity Framework 팀의 동시성 설명서입니다.
- [ASP.NET 웹 응용 프로그램에서 Entity Framework를 사용 하 여 동시성 처리](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md). Entity Framework 4.0에 적용 됩니다. Web Forms 샘플 응용 프로그램을 사용 하는 Database First ObjectContext API.

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>Entity Framework에 대 한 서적

- [프로그래밍 Entity Framework:](http://shop.oreilly.com/product/0636920022237.do) Julie Lerman 및 Rowan DbContext by.
- [프로그래밍 Entity Framework:](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 및 rowan를 통해 Code First.

이러한 책은 모두 최신 권장 기법을 사용 하 여 최신 상태입니다. 인터넷에서 사용할 수 있는 것 보다 더 포괄적이 고 따르기 쉬운 Entity Framework 소개를 제공 합니다. Julie Lerman를 사용 하 여 [Entity Framework 프로그래밍](http://shop.oreilly.com/product/9780596807252.do) 하는 다른 책은 더 크고 포괄적 이지만 이전에는 더 이상 Entity Framework 사용 하지 않는 것이 좋습니다. MSDN 사이트의 [데이터 개발자 센터](https://msdn.microsoft.com/data/aa937716) 에서 Entity Framework 팀에 게 권장 되는 서적 목록도 참조 하세요.

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>기타 Entity Framework 리소스

- [Entity Framework (ADO.NET) 팀 블로그](https://blogs.msdn.com/b/adonet/). 최신 정보 및 새로운 개선 사항에 대 한 공지 사항에 대 한 최상의 리소스 중 하나입니다. 다른 EF 관련 블로그의 경우 [시작 Entity Framework](https://msdn.microsoft.com/data/ee712907)에서 Blogroll를 참조 하세요.
- [MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx). Entity Framework와 관련 된 항목에 대 한 유용한 **데이터 요소** 열을 참조 하세요.

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>ASP.NET Web Forms 응용 프로그램의 데이터 바인딩

- [ASP.NET Web Forms Data Access Options](https://msdn.microsoft.com/library/jj822927.aspx) (MSDN) <a id="wfmodelbinding"></a> .

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>Web Forms 모델 바인딩 사용

- [모델 바인딩 및 Web Forms](https://go.microsoft.com/fwlink/?LinkId=286117) EF Code First를 사용 하는 자습서 시리즈입니다.
- [Web Forms 모델 바인딩 파트 1: 데이터 선택](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx) (Scott Guthrie의 블로그) 이러한 이전 블로그 게시물에서 현재 이름이 ItemType 인 속성의 이름은 ModelType 이지만, 그렇지 않으면 포함 된 정보가 유효 합니다.
- [Web Forms 모델 바인딩 파트 2: 데이터 필터링](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx) (Scott Guthrie의 블로그)
- [Web Forms 모델 바인딩 파트 3: 업데이트 및 유효성 검사](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx) (Scott Guthrie의 블로그)
- [ASP.NET 4.5 Web Forms 모델 바인딩입니다](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md). (비디오).
- [모델 바인딩 파트 1-데이터 선택](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md) (비디오)
- [모델 바인딩 파트 2-필터링](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md) (비디오)
- [ASP.NET 4.5 Web Forms 시작-데이터 항목 및 세부 정보를 표시](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)합니다.

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>Web Forms 데이터 소스 컨트롤 사용

- [데이터 원본 웹 서버 컨트롤](https://msdn.microsoft.com/library/ms247258.aspx) (MSDN)
- Entity Framework 6 (Microsoft 웹 개발 블로그)의 [Dynamic Data 공급자 및 EntityDataSource 컨트롤 릴리스 발표](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>Web Forms Data-Bound 컨트롤 및 Data-Binding 식 사용

- [모델 바인딩 및 Web Forms](https://go.microsoft.com/fwlink/?LinkId=286117) EF Code First를 사용 하는 자습서 시리즈입니다.
- [ASP.NET 4.5 Web Forms 시작-데이터 항목 및 세부 정보를 표시](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)합니다.
- [강력한 형식의 데이터 컨트롤](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx) (Scott Guthrie의 블로그)
- [강력한 형식의 데이터 컨트롤](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (비디오)
- [ASP.NET 4.5 Web Forms 강력한 형식의 데이터 컨트롤](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md) (비디오).
- [데이터 바인딩된 웹 서버 컨트롤](https://msdn.microsoft.com/library/ms228214.aspx) (MSDN)
- [데이터 바인딩 식 개요](https://msdn.microsoft.com/library/ms178366.aspx) (MSDN). 이 페이지에는 **Eval** 및 **바인드**만 포함 됩니다. **항목** 및 **binditem**을 포함 하도록 업데이트 되지 않았습니다.

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>SQL Server 데이터베이스 작업

- [SQL Server Database 기능](https://msdn.microsoft.com/library/hh230827.aspx) (MSDN) 다양 한 SQL Server 항목에 대 한 일반적인 소개는 TOC에서이 항목 아래에 있는 항목을 참조 하세요.
- [SQL Server 버전](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver) (MSDN). 각 버전에 대 한 자세한 정보에 대 한 링크가 포함 된 사용 가능한 SQL Server 버전에 대 한 요약입니다.)
- [ASP.NET 웹 응용 프로그램 (MSDN)에 대 한 연결 문자열을 SQL Server](https://msdn.microsoft.com/library/jj653752.aspx) 합니다.
- [ASP.NET 웹 응용 프로그램 (MSDN)에 SQL Server Compact를 사용](https://msdn.microsoft.com/library/ms247257.aspx) 합니다.
- [Microsoft SQL Server: 데이터베이스 제품 샘플](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md). 예제 AdventureWorks 데이터베이스.
- [예제 데이터베이스를 설치](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)합니다. 여기에 표시 된 방법 외에도 샘플 .mdf 파일 중 하나를 \_ 웹 프로젝트의 응용 프로그램 데이터 폴더에 다운로드 하 고, 데이터베이스를 localdb로 변환 하 고, localdb 연결 문자열을 만들 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 [방법: LocalDB로 업그레이드](https://msdn.microsoft.com/library/hh873188.aspx)를 참조 하세요.

SQL Server Express 및 LocalDB를 사용 하 고 SQL Server와 SQL Database 중 하나를 선택 하는 방법에 대해서는 다음 섹션을 참조 하세요.

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>SQL Server Express LocalDB 데이터베이스 작업

- [SQL Server Express 2012 LocalDB](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx) (MSDN). LocalDB에 대 한 공식 MSDN 소개.
- [ASP.NET 웹 응용 프로그램 (MSDN)에 대 한 연결 문자열을 SQL Server](https://msdn.microsoft.com/library/jj653752.aspx) 합니다.
- [방법: LocalDB로 업그레이드](https://msdn.microsoft.com/library/hh873188.aspx) (MSDN) 이전 버전의 SQL Server Express에서 LocalDB로 .mdf 파일을 마이그레이션하는 방법입니다. [SQL Server 2012 샘플 데이터베이스](https://go.microsoft.com/fwlink/?linkid=117483)중 하나를 다운로드 하는 경우에도이 과정을 진행 해야 합니다.
- [향상 된 SQL Express](https://go.microsoft.com/fwlink/?LinkId=234375) (SQL Server Express 블로그) 인 LocalDB 소개. 는 MSDN에 포함 된 것 보다 더 많은 배경으로 LocalDB를 만들었습니다.
- [LocalDB: 내 데이터베이스는 어디에 있나요?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL Server Express 블로그). LocalDB 데이터베이스 파일이 생성 되는 위치에 대 한 정보입니다.
- [전체 IIS에서 LocalDB 사용, 1 부: 사용자 프로필](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx) (SQL Server Express 블로그). LocalDB는 IIS에서 작동 하도록 설계 되지 않았습니다. 이 일련의 블로그 게시물에서는 문제 및 몇 가지 해결 방법을 설명 합니다.

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>SQL Server Express 데이터베이스 작업

- [ASP.NET 웹 응용 프로그램 (MSDN)에 대 한 연결 문자열을 SQL Server](https://msdn.microsoft.com/library/jj653752.aspx) 합니다. SQL Server Express와 함께 AttachDBFileName 연결 문자열 설정을 사용 하는 경우에는이 페이지의 사용자 인스턴스 섹션을 참조 하십시오.
- [로컬 SQL Server Express 2008 (SQL Server Express 블로그)의 소유권을 가져오는 방법](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx) 입니다. SQL Server Express 인스턴스의 관리자가 아니기 때문에 SQL Server Express 데이터베이스에서 일반적인 문제를 해결할 수 없습니다. 기본적으로 SQL Server Express를 설치한 사람만이 관리자입니다. 이 블로그에서는 컴퓨터의 관리자 인 경우 관리자에 게 SQL Server Express 하는 방법을 설명 합니다.
- [ASP.NET 웹 응용 프로그램에서 프로덕션 환경에 SQL Server Express 데이터베이스를 사용할 수 있나요?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN).

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>Windows Azure SQL Database 사용

- [멤버 자격, OAuth 및 SQL Database이 있는 보안 ASP.NET MVC 앱을 Windows Azure 웹 사이트](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data) (Microsoft Azure 사이트)에 배포 합니다.
- [SQL 데이터베이스](https://docs.microsoft.com/azure/sql-database/) (Microsoft Azure 사이트) 자습서 및 방법 가이드를 시작 합니다.
- [Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx) (MSDN). MSDN의 SQL Database에 대 한 목차의 최상위 노드입니다.
- [Windows Azure SQL Database Technet Wiki 문서 인덱스](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx) (Microsoft technet 사이트)
- [일시적인 오류 처리 응용 프로그램 블록](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx)입니다. 제한으로 인해 발생 하는 일시적인 네트워크 오류 및 연결 오류를 처리할 수 있게 해 주는 프레임 워크입니다. NuGet 패키지에서 사용 가능: [Enterprise Library 5.0-일시적인 오류 처리 응용 프로그램 블록](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling)입니다.
- [SQL Database 및 Entity Framework 시작](https://msdn.microsoft.com/data/jj556244) (MSDN)
- Microsoft [Azure 교육 키트](https://www.microsoft.com/download/details.aspx?id=8396) (Microsoft 다운로드 센터). SQL Database에 대 한 실습 실습을 포함 합니다.
- [Windows Azure SQL Database 커뮤니티 포럼](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads).
- [Windows Azure SQL Database](https://msdn.microsoft.com/library/ff803375.aspx) (MSDN)로 이동 합니다. Microsoft 패턴 및 관행 팀에서 포괄적인 종단 간 시나리오의 한 장입니다. 마이그레이션할 수 있는 이유와 SQL Server에서 SQL Database로 마이그레이션하는 방법에 대해 설명 합니다.
- [SQL Server 데이터베이스를 Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN)로 마이그레이션합니다.
- [마이그레이션 마법사를 SQL Database](http://sqlazuremw.codeplex.com/)합니다. SQL Database에서 데이터베이스를 마이그레이션하는 데 사용할 수 있는 오픈 소스 도구입니다.

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>SQL Server 및 Windows Azure SQL Database 중에서 선택

- [Windows Azure SQL Database와 SQL Server 비교](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx) (Microsoft TechNet 사이트).
- [Windows Azure SQL Database로 데이터 마이그레이션: 도구 및 기술](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx) (MSDN) SQL Server를 SQL Database와 비교 하 고 SQL Server에서 SQL Database로 마이그레이션하는 시점에 대 한 지침을 제공 하는 섹션이 포함 되어 있습니다.
- [Windows Azure SQL Database 배달 가이드](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx) (Microsoft TechNet 사이트)
- [SQL Server 기능 제한 사항 (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx) (MSDN)
- [Windows Azure Table Storage 및 windows Azure SQL Database-비교 및 대조](https://msdn.microsoft.com/library/jj553018.aspx) (MSDN) Windows Azure에 배포 하는 응용 프로그램의 경우 windows Azure Table storage가 Windows Azure SQL Database에 대 한 대안이 될 수 있습니다. 이 항목은 이러한 대체 방법을 결정 하는 데 도움이 됩니다.
- [Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee336279) (MSDN).
- [지침 및 제한 사항(Microsoft Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>NoSQL 데이터베이스 관리 시스템 작업

- [Microsoft Azure Data Services](https://www.windowsazure.com/develop/net/data/) (Microsoft Azure 사이트). [테이블 서비스 기능 가이드](https://docs.microsoft.com/azure/) 및 페이지의 **빅 데이터** 섹션을 참조 하세요.
- [저장소 테이블, 큐 및 blob (Microsoft Azure 사이트)를 사용 하는 다중 계층 응용 프로그램을 ASP.NET](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) 합니다. Microsoft Azure storage NoSQL 테이블을 사용 하는 다운로드 가능한 샘플 응용 프로그램의 종단 간 자습서입니다.

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>ASP.NET 응용 프로그램에서 LINQ 쿼리 사용

- MSDN ( [ASP.NET Data Access Options](https://msdn.microsoft.com/library/ms178359.aspx#linq) ). LINQ에 대 한 소개를 포함 합니다.
- [LINQ 학습 비디오](http://www.misfitgeek.com/windows-client-linq-training-videos-20/) (Joe Stagner의 블로그)
- [동적 LINQ 리소스에 대 한 링크가 포함 된 ASP.NET 포럼 스레드](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>Dynamic Data 스 캐 폴딩 사용

- [프로젝트 템플릿](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata) (MSDN)을 Dynamic Data 합니다. Dynamic Data 프로젝트를 사용 하는 경우에 대 한 지침입니다.
- [ASP.NET Dynamic Data](https://msdn.microsoft.com/library/ee845452.aspx) (MSDN).

<a id="securing"></a>

## <a name="securing-data-access"></a>데이터 액세스 보안

- [ASP.NET에서 데이터 액세스 보호](https://msdn.microsoft.com/library/ms178375.aspx) (MSDN)를 사용 합니다.
- [보안 고려 사항 (Entity Framework)](https://msdn.microsoft.com/library/cc716760.aspx) (MSDN)
- [방법: 데이터 소스 컨트롤을 사용 하는 경우 연결 문자열 보호](https://msdn.microsoft.com/library/ms178372.aspx) (MSDN)

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>데이터 액세스 성능 최적화

- [ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225.aspx) (MSDN).
- [ASP.NET 캐싱](https://msdn.microsoft.com/library/xsbfdd8c.aspx) (MSDN).
- [ASP.NET 성능 향상](https://msdn.microsoft.com/library/ff647787) (MSDN) 이 페이지의 맨 위에 "사용 중지 된 콘텐츠" 경고가 있지만 대부분의 정보는 여전히 관련이 있으며, 비교할 수 있는 업데이트 된 리소스가 없습니다.
- [SQL Server 성능 향상](https://msdn.microsoft.com/library/ff647793) (MSDN) 이전 링크와 동일한 주석입니다.

이 항목의 앞부분에 나오는 [Entity Framework 성능 최적화](#optimizingef) 도 참조 하세요.

<a id="deploying"></a>

## <a name="deploying-a-database"></a>데이터베이스 배포

- [ASP.NET 웹 배포-권장 리소스](aspnet-web-deployment-content-map.md) (MSDN).

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>웹 서비스를 통해 데이터 액세스

- [웹 서비스 (MSDN)를 통해 데이터에 액세스](https://msdn.microsoft.com/library/ms178359.aspx#webservice) 합니다. Web API와 WCF를 사용 하는 경우에 대 한 지침입니다.
- [ASP.NET Web API 시작 하는 중](../web-api/index.md)입니다.
- [WCF Data Services](https://msdn.microsoft.com/data/bb931106) (MSDN)을 (를) 합니다.

<a id="additional"></a>

## <a name="additional-resources"></a>추가 리소스

- MSDN ( [ASP.NET Data ACCESS FAQ](https://msdn.microsoft.com/library/jj653753.aspx) ).
- [ASP.NET Web Forms 자습서-데이터](../web-forms/overview/data-access/index.md)입니다. 이러한 자습서 대부분은 상대적으로 이전입니다. [Microsoft Azure를 사용 하 여 클라우드 앱을 Real-World 빌드하](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) 는 [ASP.NET 데이터 액세스 옵션](https://msdn.microsoft.com/library/ms178359.aspx) 및 데이터 저장소 옵션을 먼저 읽어 보세요. 사용자의 시나리오에 적합 하지 않은 데이터 액세스 방법이 너무 크지 않도록 해야 합니다.
- [ASP.NET MVC 콘텐츠 맵](../mvc/overview/getting-started/recommended-resources-for-mvc.md)
- [자습서-데이터를 ASP.NET 웹 페이지](../web-pages/overview/data/index.md)합니다.
- [Visual Studio (MSDN)에서 데이터에 액세스](https://msdn.microsoft.com/library/wzabh8c4.aspx) 이 콘텐츠 맵과 유사한 링크 목록을 제공 하지만 ASP.NET 대신 Visual Studio에 포커스가 있습니다.
