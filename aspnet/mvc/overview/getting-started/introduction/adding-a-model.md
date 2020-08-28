---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 모델 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045119"
---
# <a name="adding-a-model"></a><span data-ttu-id="6940b-102">모델 추가</span><span class="sxs-lookup"><span data-stu-id="6940b-102">Adding a Model</span></span>

<span data-ttu-id="6940b-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6940b-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="6940b-104">이 섹션에서는 데이터베이스에서 동영상을 관리 하기 위한 몇 가지 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="6940b-105">이러한 클래스는 &quot; &quot; ASP.NET MVC 앱의 모델 부분이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="6940b-106">이러한 모델 클래스를 정의 하 고 사용 하려면 [Entity Framework](https://docs.microsoft.com/ef/) 라는 .NET Framework 데이터 액세스 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="6940b-107">Entity Framework (EF 라고도 함)는 *Code First*라는 개발 패러다임을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="6940b-108">Code First를 사용 하면 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="6940b-109">&quot;일반-이전 CLR 개체의 POCO 클래스 라고도 합니다. &quot; 그런 다음 클래스에서 즉석에서 데이터베이스를 만들 수 있습니다. 이렇게 하면 매우 깔끔하고 빠른 개발 워크플로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="6940b-110">먼저 데이터베이스를 만들어야 하는 경우에도이 자습서에 따라 MVC 및 EF 앱 개발에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="6940b-111">그런 다음 데이터베이스의 첫 번째 접근 방식을 설명 하는 Tom Fizmakens [ASP.NET 스 캐 폴딩](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) 자습서를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="6940b-112">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="6940b-112">Adding Model Classes</span></span>

<span data-ttu-id="6940b-113">**솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **클래스**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="6940b-114">*클래스* 이름 영화를 입력 합니다 &quot; &quot; .</span><span class="sxs-lookup"><span data-stu-id="6940b-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="6940b-115">클래스에 다음 5 가지 속성을 추가 합니다 `Movie` .</span><span class="sxs-lookup"><span data-stu-id="6940b-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="6940b-116">클래스를 사용 `Movie` 하 여 데이터베이스의 영화를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="6940b-117">개체의 각 인스턴스는 `Movie` 데이터베이스 테이블의 행에 해당 하며 클래스의 각 속성은 `Movie` 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="6940b-118">참고: System.object 및 관련 클래스를 사용 하려면 [Entity Framework NuGet 패키지](https://www.nuget.org/packages/EntityFramework/)를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="6940b-119">추가 지침을 보려면 링크를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="6940b-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="6940b-120">동일한 파일에서 다음 클래스를 추가 합니다 `MovieDBContext` .</span><span class="sxs-lookup"><span data-stu-id="6940b-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="6940b-121">`MovieDBContext`클래스는 `Movie` 데이터베이스의 클래스 인스턴스 가져오기, 저장 및 업데이트를 처리 하는 Entity Framework movie 데이터베이스 컨텍스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="6940b-122">는 `MovieDBContext` Entity Framework에서 제공 하는 `DbContext` 기본 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="6940b-123">및를 참조할 수 있으려면 `DbContext` `DbSet` `using` 파일의 맨 위에 다음 문을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="6940b-124">Using 문을 수동으로 추가 하 여이 작업을 수행할 수 있습니다. 또는 빨간 물결 모양의 선을 마우스로 가리킨 다음 클릭 `Show potential fixes` 하 여 `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="6940b-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="6940b-125">참고: 사용 되지 않는 여러 `using` 문이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="6940b-126">Visual Studio는 사용 되지 않는 종속성을 회색으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="6940b-127">회색 종속성을 마우스로 가리켜 사용 하지 않는 종속성을 제거 하 `Show potential fixes` 고 **사용 하지 않는 using 제거** 를 클릭 하 여 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="6940b-128">마지막으로 모델 (MVC의 M)을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="6940b-129">다음 섹션에서는 데이터베이스 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6940b-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6940b-130">[이전](adding-a-view.md)
> [다음](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="6940b-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
