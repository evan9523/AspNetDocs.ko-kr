---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: 데이터베이스 데이터 테이블 표시(C#) | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서에서는 데이터베이스 레코드 집합을 표시하는 두 가지 방법을 보여 줍니다. HTML ta에서 데이터베이스 레코드 집합을 포맷하는 두 가지 방법을 보여 드리겠습니다.
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3fca8ac9e9b4e549ca76ffa282cc03aa4cc50e88
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542056"
---
# <a name="displaying-a-table-of-database-data-c"></a><span data-ttu-id="0db87-104">데이터베이스 데이터의 테이블 표시(C#)</span><span class="sxs-lookup"><span data-stu-id="0db87-104">Displaying a Table of Database Data (C#)</span></span>

<span data-ttu-id="0db87-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0db87-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="0db87-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="0db87-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> <span data-ttu-id="0db87-107">이 자습서에서는 데이터베이스 레코드 집합을 표시하는 두 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="0db87-108">HTML 테이블에서 데이터베이스 레코드 집합을 서식지정하는 두 가지 방법을 보여 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="0db87-109">먼저 뷰 내에서 데이터베이스 레코드를 직접 포맷하는 방법을 보여 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="0db87-110">다음으로 데이터베이스 레코드를 서식 지정할 때 부분을 활용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="0db87-111">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 데이터베이스 데이터의 HTML 테이블을 표시하는 방법을 설명하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="0db87-112">먼저 Visual Studio에 포함된 스캐폴딩 도구를 사용하여 레코드 집합을 자동으로 표시하는 뷰를 생성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="0db87-113">다음으로 데이터베이스 레코드를 서식 지정할 때 일부를 템플릿으로 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="0db87-114">모델 클래스 작성</span><span class="sxs-lookup"><span data-stu-id="0db87-114">Create the Model Classes</span></span>

<span data-ttu-id="0db87-115">Movies 데이터베이스 테이블의 레코드 집합을 표시할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="0db87-116">Movies 데이터베이스 테이블에는 다음 열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-116">The Movies database table contains the following columns:</span></span>

<a id="0.3_table01"></a>

| <span data-ttu-id="0db87-117">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="0db87-117">**Column Name**</span></span> | <span data-ttu-id="0db87-118">**데이터 유형**</span><span class="sxs-lookup"><span data-stu-id="0db87-118">**Data Type**</span></span> | <span data-ttu-id="0db87-119">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="0db87-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0db87-120">Id</span><span class="sxs-lookup"><span data-stu-id="0db87-120">Id</span></span> | <span data-ttu-id="0db87-121">Int</span><span class="sxs-lookup"><span data-stu-id="0db87-121">Int</span></span> | <span data-ttu-id="0db87-122">False</span><span class="sxs-lookup"><span data-stu-id="0db87-122">False</span></span> |
| <span data-ttu-id="0db87-123">제목</span><span class="sxs-lookup"><span data-stu-id="0db87-123">Title</span></span> | <span data-ttu-id="0db87-124">은바르르 (200)</span><span class="sxs-lookup"><span data-stu-id="0db87-124">Nvarchar(200)</span></span> | <span data-ttu-id="0db87-125">False</span><span class="sxs-lookup"><span data-stu-id="0db87-125">False</span></span> |
| <span data-ttu-id="0db87-126">감독</span><span class="sxs-lookup"><span data-stu-id="0db87-126">Director</span></span> | <span data-ttu-id="0db87-127">응바르차르 (50)</span><span class="sxs-lookup"><span data-stu-id="0db87-127">NVarchar(50)</span></span> | <span data-ttu-id="0db87-128">False</span><span class="sxs-lookup"><span data-stu-id="0db87-128">False</span></span> |
| <span data-ttu-id="0db87-129">날짜 발표</span><span class="sxs-lookup"><span data-stu-id="0db87-129">DateReleased</span></span> | <span data-ttu-id="0db87-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="0db87-130">DateTime</span></span> | <span data-ttu-id="0db87-131">False</span><span class="sxs-lookup"><span data-stu-id="0db87-131">False</span></span> |

<span data-ttu-id="0db87-132">ASP.NET MVC 응용 프로그램에서 Movies 테이블을 나타내려면 모델 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="0db87-133">이 자습서에서는 Microsoft 엔터티 프레임워크를 사용하여 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="0db87-134">이 자습서에서는 Microsoft 엔터티 프레임워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="0db87-135">그러나 LINQ에서 SQL, NHibernate 또는 ADO.NET ASP.NET MVC 응용 프로그램에서 데이터베이스와 상호 작용하기 위해 다양한 기술을 사용할 수 있다는 점을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="0db87-136">다음 단계에 따라 엔터티 데이터 모델 마법사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="0db87-137">솔루션 탐색기 창에서 모델 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **추가, 새 항목**선택.</span><span class="sxs-lookup"><span data-stu-id="0db87-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="0db87-138">**데이터** 범주를 선택하고 **ADO.NET 엔터티 데이터 모델** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="0db87-139">데이터 모델에 *MoviesDBModel.edmx라는* 이름을 지정하고 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="0db87-140">추가 단추를 클릭하면 엔터티 데이터 모델 마법사가 나타납니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="0db87-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="0db87-141">다음 단계에 따라 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="0db87-142">모델 내용 선택 단계에서 **데이터베이스에서 생성** 옵션을 **선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="0db87-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="0db87-143">데이터 **연결 선택** 단계에서 는 *MoviesDB.mdf* 데이터 연결 및 연결 설정에 *대해 MoviesDBEntities라는* 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="0db87-144">**다음** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="0db87-145">데이터베이스 **개체 선택** 단계에서 테이블 노드를 확장하고 동영상 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="0db87-146">네임스페이스 *모델을* 입력하고 **완료** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="0db87-147">[![SQL 클래스에 LINQ 만들기](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="0db87-148">**그림 01**: SQL 클래스에 LINQ 만들기[(전체 크기 이미지를 보려면 클릭)](displaying-a-table-of-database-data-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image2.png))</span></span>

<span data-ttu-id="0db87-149">엔터티 데이터 모델 마법사를 완료하면 엔터티 데이터 모델 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="0db87-150">디자이너는 동영상 엔터티를 표시해야 합니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="0db87-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="0db87-151">[![엔터티 데이터 모델 디자이너](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span></span>

<span data-ttu-id="0db87-152">**그림 02**: 엔터티 데이터 모델 디자이너[(전체 크기 이미지를 보려면 클릭)](displaying-a-table-of-database-data-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image4.png))</span></span>

<span data-ttu-id="0db87-153">계속하기 전에 한 가지 변화를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-153">We need to make one change before we continue.</span></span> <span data-ttu-id="0db87-154">엔터티 데이터 마법사는 Movies 데이터베이스 테이블을 나타내는 *Movies라는* 모델 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="0db87-155">Movies 클래스를 사용하여 특정 영화를 나타내기 때문에 클래스의 이름을 *동영상* 대신 *Movie* 동영상(복수편이 아닌 단수)으로 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="0db87-156">디자이너 표면에서 클래스 이름을 두 번 클릭하고 클래스 이름을 동영상에서 동영상으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="0db87-157">이렇게 변경한 후 **저장** 단추(플로피 디스크의 아이콘)를 클릭하여 Movie 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="0db87-158">동영상 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="0db87-158">Create the Movies Controller</span></span>

<span data-ttu-id="0db87-159">이제 데이터베이스 레코드를 나타낼 수 있는 방법이 있으므로 영화 컬렉션을 반환하는 컨트롤러를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="0db87-160">시각적 스튜디오 솔루션 탐색기 창에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭하고 **컨트롤러 추가** 옵션(그림 3 참조)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="0db87-161">[![컨트롤러 추가 메뉴](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-161">[![The Add Controller Menu](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span></span>

<span data-ttu-id="0db87-162">**그림 03**: 컨트롤러 추가 메뉴[(전체 크기 이미지를 보려면 클릭)](displaying-a-table-of-database-data-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image6.png))</span></span>

<span data-ttu-id="0db87-163">컨트롤러 **추가** 대화 상자가 나타나면 컨트롤러 이름 MovieController를 입력합니다(그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="0db87-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="0db87-164">새 컨트롤러를 추가하려면 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="0db87-165">[![컨트롤러 추가 대화 상자](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-165">[![The Add Controller dialog](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span></span>

<span data-ttu-id="0db87-166">**그림 04**: 컨트롤러 추가 대화 상자[(클릭하여 전체 크기 이미지 보기)](displaying-a-table-of-database-data-cs/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image8.png))</span></span>

<span data-ttu-id="0db87-167">데이터베이스 레코드 집합을 반환하도록 동영상 컨트롤러에서 노출하는 Index() 작업을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="0db87-168">목록 1의 컨트롤러처럼 보이게 하여 컨트롤러를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="0db87-169">**목록 1 – 컨트롤러\MovieController.cs**</span><span class="sxs-lookup"><span data-stu-id="0db87-169">**Listing 1 – Controllers\MovieController.cs**</span></span>

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

<span data-ttu-id="0db87-170">목록 1에서 MoviesDBEntities 클래스는 MoviesDB 데이터베이스를 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="0db87-171">이 클래스를 사용하려면 다음과 같이 MvcApplication1.Models 네임스페이스를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-171">To use this class, you need to import the MvcApplication1.Models namespace like this:</span></span>

<span data-ttu-id="0db87-172">MvcApplication1.모델 사용;</span><span class="sxs-lookup"><span data-stu-id="0db87-172">using MvcApplication1.Models;</span></span>

<span data-ttu-id="0db87-173">식 *엔터티입니다. MovieSet.ToList()는* Movies 데이터베이스 테이블의 모든 동영상 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-173">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="0db87-174">뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="0db87-174">Create the View</span></span>

<span data-ttu-id="0db87-175">HTML 테이블에 데이터베이스 레코드 집합을 표시하는 가장 쉬운 방법은 Visual Studio에서 제공하는 스캐폴딩을 활용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-175">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="0db87-176">메뉴 옵션 **빌드, 빌드 솔루션을**선택하여 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-176">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="0db87-177">**보기 추가** 대화 상자를 열기 전에 응용 프로그램을 빌드해야 하거나 데이터 클래스가 대화 상자에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-177">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="0db87-178">Index() 작업을 마우스 오른쪽 단추로 클릭하고 **보기 추가** 옵션을 선택합니다(그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="0db87-178">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="0db87-179">[![뷰 추가](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-179">[![Adding a view](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span></span>

<span data-ttu-id="0db87-180">**그림 05**: 보기 추가[(전체 크기 이미지를 보려면 클릭)](displaying-a-table-of-database-data-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-180">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image10.png))</span></span>

<span data-ttu-id="0db87-181">뷰 **추가** 대화 상자에서 **강력한 형식의 뷰 만들기라는 레이블이**붙은 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-181">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="0db87-182">Movie 클래스를 **뷰 데이터 클래스로**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-182">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="0db87-183">*목록을* 뷰 **콘텐츠로** 선택합니다(그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="0db87-183">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="0db87-184">이러한 옵션을 선택하면 동영상 목록이 표시되는 강력한 형식의 뷰가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-184">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="0db87-185">[![보기 추가 대화 상자](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-185">[![The Add View dialog](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="0db87-186">**그림 06**: 추가 보기 대화[상자(클릭하여 전체 크기 이미지 보기)](displaying-a-table-of-database-data-cs/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-186">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image12.png))</span></span>

<span data-ttu-id="0db87-187">**추가** 단추를 클릭하면 목록 2의 보기가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-187">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="0db87-188">이 보기에는 동영상 컬렉션을 반복하고 동영상의 각 속성을 표시하는 데 필요한 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-188">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="0db87-189">**목록 2 – 보기\영화\인덱스.aspx**</span><span class="sxs-lookup"><span data-stu-id="0db87-189">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

<span data-ttu-id="0db87-190">메뉴 옵션 **디버그, 디버깅 시작(또는** F5 키 를 누르기)을 선택하여 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-190">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="0db87-191">응용 프로그램을 실행실행하여 인터넷 익스플로러를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-191">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="0db87-192">/동영상 URL로 이동하면 그림 7의 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-192">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="0db87-193">[![영화 테이블](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-193">[![A table of movies](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span></span>

<span data-ttu-id="0db87-194">**그림 07**: 동영상 표[(전체 크기 이미지를 보려면 클릭)](displaying-a-table-of-database-data-cs/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="0db87-194">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image14.png))</span></span>

<span data-ttu-id="0db87-195">그림 7에서 데이터베이스 레코드 그리드의 모양에 대해 아무것도 좋아하지 않는 경우 인덱스 보기를 수정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-195">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="0db87-196">예를 들어 인덱스 보기를 수정하여 *해제된* *날짜로* 날짜 해제 헤더를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-196">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="0db87-197">부분 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="0db87-197">Create a Template with a Partial</span></span>

<span data-ttu-id="0db87-198">뷰가 너무 복잡해지면 뷰를 부분적으로 나누는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-198">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="0db87-199">부분적인 부분 설정을 사용하면 뷰를 더 쉽게 이해하고 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-199">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="0db87-200">각 동영상 데이터베이스 레코드의 서식을 지정하기 위해 템플릿으로 사용할 수 있는 부분을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-200">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="0db87-201">다음 단계를 수행하여 일부를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-201">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="0db87-202">View\Movie 폴더를 마우스 오른쪽 단추로 클릭하고 **보기 추가**옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-202">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="0db87-203">레이블이 붙은 확인란을 *선택합니다.ascx 부분 뷰 만들기.*</span><span class="sxs-lookup"><span data-stu-id="0db87-203">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="0db87-204">부분 *동영상 템플릿의*이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-204">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="0db87-205">레이블이 붙은 확인란을 **선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="0db87-205">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="0db87-206">뷰 데이터 *클래스로*동영상 입니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-206">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="0db87-207">*보기 내용으로*비어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-207">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="0db87-208">**추가** 단추를 클릭하여 프로젝트에 일부를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-208">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="0db87-209">이 단계를 완료한 후 MovieTemplate 일부를 수정하여 목록 3처럼 보이게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-209">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="0db87-210">**목록 3 – 보기\영화\영화템플릿.ascx**</span><span class="sxs-lookup"><span data-stu-id="0db87-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

<span data-ttu-id="0db87-211">목록 3의 부분 레코드 행에 대한 템플릿이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-211">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="0db87-212">목록 4에서 수정된 인덱스 보기는 동영상 템플릿 일부를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-212">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="0db87-213">**목록 4 – 보기\영화\인덱스.aspx**</span><span class="sxs-lookup"><span data-stu-id="0db87-213">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

<span data-ttu-id="0db87-214">목록 4의 보기에는 모든 동영상을 반복하는 foreach 루프가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-214">The view in Listing 4 contains a foreach loop that iterates through all of the movies.</span></span> <span data-ttu-id="0db87-215">각 동영상에 대해 MovieTemplate 부분의 포맷을 사용하여 동영상의 서식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-215">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="0db87-216">MovieTemplate는 RenderPartial() 도우미 메서드를 호출하여 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-216">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="0db87-217">수정된 인덱스 보기는 데이터베이스 레코드의 동일한 HTML 테이블을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-217">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="0db87-218">그러나 보기가 크게 단순화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-218">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="0db87-219">RenderPartial() 메서드는 문자열을 반환하지 않으므로 대부분의 다른 도우미 메서드와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-219">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="0db87-220">따라서 % Html.RenderPartial()를 &lt;사용하여 RenderPartial() 메서드를 호출해야 합니다. %= Html.RenderPartial(대신 %);&gt; &lt; %&gt;.</span><span class="sxs-lookup"><span data-stu-id="0db87-220">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial(); %&gt; instead of &lt;%= Html.RenderPartial(); %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="0db87-221">요약</span><span class="sxs-lookup"><span data-stu-id="0db87-221">Summary</span></span>

<span data-ttu-id="0db87-222">이 자습서의 목표는 HTML 테이블에 데이터베이스 레코드 집합을 표시하는 방법을 설명하는 것이었습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-222">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="0db87-223">먼저 Microsoft 엔터티 프레임워크를 활용하여 컨트롤러 작업에서 데이터베이스 레코드 집합을 반환하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-223">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="0db87-224">다음으로 Visual Studio 스캐폴딩을 사용하여 항목 컬렉션을 자동으로 표시하는 뷰를 생성하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-224">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="0db87-225">마지막으로 일부를 활용하여 뷰를 단순화하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-225">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="0db87-226">각 데이터베이스 레코드의 서식을 지정할 수 있도록 일부를 템플릿으로 사용하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0db87-226">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0db87-227">[이전](creating-model-classes-with-linq-to-sql-cs.md)
> [다음](performing-simple-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="0db87-227">[Previous](creating-model-classes-with-linq-to-sql-cs.md)
[Next](performing-simple-validation-cs.md)</span></span>
