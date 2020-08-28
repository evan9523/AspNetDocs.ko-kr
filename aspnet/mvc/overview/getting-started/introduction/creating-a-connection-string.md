---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 연결 문자열 만들기 및 SQL Server LocalDB 작업 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 4400cb8c6a5d57da60d164220f929d69d7f4d2f7
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044261"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="aa0c5-102">연결 문자열 만들기 및 SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="aa0c5-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="aa0c5-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="aa0c5-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="aa0c5-104">연결 문자열 만들기 및 SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="aa0c5-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="aa0c5-105">`MovieDBContext`만든 클래스는 데이터베이스에 연결 하 고 `Movie` 개체를 데이터베이스 레코드에 매핑하는 태스크를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="aa0c5-106">한 가지 질문은 연결할 데이터베이스를 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="aa0c5-107">실제로는 사용할 데이터베이스를 지정할 필요가 없으며, 기본적으로 [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)를 사용 하 여 Entity Framework 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="aa0c5-108">이 섹션에서는 응용 프로그램의 *Web.config* 파일에 연결 문자열을 명시적으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="aa0c5-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="aa0c5-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="aa0c5-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) 는 요청 시 시작 하 고 사용자 모드에서 실행 되는 SQL Server Express 데이터베이스 엔진의 경량 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="aa0c5-111">LocalDB는 데이터베이스를 *.mdf* 파일로 사용할 수 있도록 하는 SQL Server Express의 특수 실행 모드로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="aa0c5-112">일반적으로 LocalDB 데이터베이스 파일은 웹 프로젝트의 *App \_ Data* 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="aa0c5-113">프로덕션 웹 응용 프로그램에서는 SQL Server Express을 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="aa0c5-114">특히 LocalDB는 IIS에서 작동 하도록 설계 되지 않았기 때문에 웹 응용 프로그램을 사용 하는 프로덕션에 사용 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="aa0c5-115">그러나 SQL Server 또는 SQL Azure으로 LocalDB 데이터베이스를 쉽게 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="aa0c5-116">Visual Studio 2017에서 LocalDB는 기본적으로 Visual Studio와 함께 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="aa0c5-117">기본적으로 Entity Framework는 `MovieDBContext` 이 프로젝트에 대 한 개체 컨텍스트 클래스와 동일한 이라는 연결 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="aa0c5-118">자세한 내용은 [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="aa0c5-119">아래에 표시 된 응용 프로그램 루트 *Web.config* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="aa0c5-120">( *Views* 폴더의 *Web.config* 파일이 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="aa0c5-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="aa0c5-121">요소를 찾습니다 `<connectionStrings>` .</span><span class="sxs-lookup"><span data-stu-id="aa0c5-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="aa0c5-122">`<connectionStrings>` *Web.config* 파일의 요소에 다음 연결 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="aa0c5-123">다음 예에서는 새 연결 문자열이 추가 된 *Web.config* 파일의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="aa0c5-124">두 연결 문자열은 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-124">The two connection strings are very similar.</span></span> <span data-ttu-id="aa0c5-125">첫 번째 연결 문자열의 이름은로 지정 되며 `DefaultConnection` 멤버 자격 데이터베이스에서 응용 프로그램에 액세스할 수 있는 사용자를 제어 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="aa0c5-126">추가 된 연결 문자열은 *App \_ Data* 폴더에 있는 *Movie. .mdf* 라는 LocalDB 데이터베이스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="aa0c5-127">이 자습서에서는 멤버 자격 데이터베이스를 사용 하지 않습니다. 멤버 자격, 인증 및 보안에 대 한 자세한 내용은 내 자습서에서 [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱 만들기 및 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="aa0c5-128">연결 문자열의 이름은 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 클래스의 이름과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="aa0c5-129">실제로 연결 문자열을 추가할 필요는 없습니다 `MovieDBContext` .</span><span class="sxs-lookup"><span data-stu-id="aa0c5-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="aa0c5-130">연결 문자열을 지정 하지 않으면 Entity Framework는 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 클래스의 정규화 된 이름 (이 경우)을 사용 하 여 사용자 디렉터리에 LocalDB 데이터베이스를 만듭니다 `MvcMovie.Models.MovieDBContext` .</span><span class="sxs-lookup"><span data-stu-id="aa0c5-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="aa0c5-131">을 포함 하는 경우 데이터베이스 이름을 원하는 대로 지정할 수 있습니다 *. MDF* 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="aa0c5-132">예를 들어, 데이터베이스 이름을 *Myfilms*로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="aa0c5-133">다음으로는 `MoviesController` 영화 데이터를 표시 하 고 사용자가 새 영화 목록을 만들 수 있도록 하는 새 클래스를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa0c5-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="aa0c5-134">[이전](adding-a-model.md)
> [다음](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="aa0c5-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
