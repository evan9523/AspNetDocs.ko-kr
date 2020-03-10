---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: Entity Framework (C#)를 사용 하 여 모델 클래스 만들기 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 Microsoft Entity Framework에서 ASP.NET MVC를 사용 하는 방법에 대해 알아봅니다. 엔터티 마법사를 사용 하 여 ADO.NET 엔터티 Da를 만드는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 2e0e365c287fc455015d237ea466301335805d14
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469439"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a><span data-ttu-id="22f5e-104">Entity Framework를 사용하여 모델 클래스 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="22f5e-104">Creating Model Classes with the Entity Framework (C#)</span></span>

<span data-ttu-id="22f5e-105">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="22f5e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="22f5e-106">이 자습서에서는 Microsoft Entity Framework에서 ASP.NET MVC를 사용 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="22f5e-107">엔터티 마법사를 사용 하 여 ADO.NET 엔터티 데이터 모델을 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="22f5e-108">이 자습서에서는 Entity Framework를 사용 하 여 데이터베이스 데이터를 선택, 삽입, 업데이트 및 삭제 하는 방법을 보여 주는 웹 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>

<span data-ttu-id="22f5e-109">이 자습서의 목표는 ASP.NET MVC 응용 프로그램을 빌드할 때 Microsoft Entity Framework를 사용 하 여 데이터 액세스 클래스를 만드는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="22f5e-110">이 자습서에서는 Microsoft Entity Framework에 대해 이전에 알지 못하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="22f5e-111">이 자습서를 마치면 Entity Framework를 사용 하 여 데이터베이스 레코드를 선택, 삽입, 업데이트 및 삭제 하는 방법을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="22f5e-112">Microsoft Entity Framework는 데이터베이스에서 자동으로 데이터 액세스 계층을 생성할 수 있도록 하는 O/RM (개체 관계형 매핑) 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="22f5e-113">Entity Framework를 사용 하면 데이터 액세스 클래스를 직접 빌드하는 지루한 작업을 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

<span data-ttu-id="22f5e-114">ASP.NET MVC와 함께 Microsoft Entity Framework를 사용 하는 방법을 설명 하기 위해 간단한 샘플 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-114">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="22f5e-115">동영상 데이터베이스 레코드를 표시 하 고 편집할 수 있는 동영상 데이터베이스 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-115">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="22f5e-116">이 자습서에서는 Visual Studio 2008 또는 Visual Web Developer 2008 서비스 팩 1이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-116">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="22f5e-117">Entity Framework를 사용 하려면 서비스 팩 1이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-117">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="22f5e-118">다음 주소에서 Visual Studio 2008 서비스 팩 1 또는 Visual Web Developer 서비스 팩 1을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-118">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> <span data-ttu-id="22f5e-119">ASP.NET MVC와 Microsoft Entity Framework 사이에는 필수적으로 연결 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-119">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="22f5e-120">ASP.NET MVC에서 사용할 수 있는 Entity Framework에 대 한 몇 가지 대안이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-120">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="22f5e-121">예를 들어 Microsoft LINQ to SQL, NHibernate 절전 모드 또는 SubSonic 같은 다른 O/RM 도구를 사용 하 여 MVC 모델 클래스를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-121">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>

## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="22f5e-122">Movie 샘플 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="22f5e-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="22f5e-123">Movie 데이터베이스 응용 프로그램은 다음 열을 포함 하는 Movie 라는 데이터베이스 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="22f5e-124">열 이름</span><span class="sxs-lookup"><span data-stu-id="22f5e-124">Column Name</span></span> | <span data-ttu-id="22f5e-125">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="22f5e-125">Data Type</span></span> | <span data-ttu-id="22f5e-126">Null을 허용 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="22f5e-126">Allow Nulls?</span></span> | <span data-ttu-id="22f5e-127">기본 키 인가요?</span><span class="sxs-lookup"><span data-stu-id="22f5e-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="22f5e-128">Id</span><span class="sxs-lookup"><span data-stu-id="22f5e-128">Id</span></span> | <span data-ttu-id="22f5e-129">int</span><span class="sxs-lookup"><span data-stu-id="22f5e-129">int</span></span> | <span data-ttu-id="22f5e-130">False</span><span class="sxs-lookup"><span data-stu-id="22f5e-130">False</span></span> | <span data-ttu-id="22f5e-131">True</span><span class="sxs-lookup"><span data-stu-id="22f5e-131">True</span></span> |
| <span data-ttu-id="22f5e-132">제목</span><span class="sxs-lookup"><span data-stu-id="22f5e-132">Title</span></span> | <span data-ttu-id="22f5e-133">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="22f5e-133">nvarchar(100)</span></span> | <span data-ttu-id="22f5e-134">False</span><span class="sxs-lookup"><span data-stu-id="22f5e-134">False</span></span> | <span data-ttu-id="22f5e-135">False</span><span class="sxs-lookup"><span data-stu-id="22f5e-135">False</span></span> |
| <span data-ttu-id="22f5e-136">감독</span><span class="sxs-lookup"><span data-stu-id="22f5e-136">Director</span></span> | <span data-ttu-id="22f5e-137">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="22f5e-137">nvarchar(100)</span></span> | <span data-ttu-id="22f5e-138">False</span><span class="sxs-lookup"><span data-stu-id="22f5e-138">False</span></span> | <span data-ttu-id="22f5e-139">False</span><span class="sxs-lookup"><span data-stu-id="22f5e-139">False</span></span> |

<span data-ttu-id="22f5e-140">다음 단계를 수행 하 여이 테이블을 ASP.NET MVC 프로젝트에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="22f5e-141">솔루션 탐색기 창에서 App\_Data 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목을 차례로 선택 합니다.**</span><span class="sxs-lookup"><span data-stu-id="22f5e-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="22f5e-142">**새 항목 추가** 대화 상자에서 **SQL Server database**를 선택 하 고 데이터베이스 이름을 MoviesDB로 지정한 다음 **추가** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="22f5e-143">MoviesDB 파일을 두 번 클릭 하 여 서버 탐색기/데이터베이스 탐색기 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="22f5e-144">MoviesDB 데이터베이스 연결을 확장 하 고 Tables 폴더를 마우스 오른쪽 단추로 클릭 한 다음 메뉴 옵션 **새 테이블 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="22f5e-145">테이블 디자이너에서 Id, 제목 및 감독 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="22f5e-146">**저장** 단추 (플로피 아이콘이 있음)를 클릭 하 여 새 테이블을 이름으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="22f5e-147">동영상 데이터베이스 테이블을 만든 후에는 테이블에 몇 가지 샘플 데이터를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="22f5e-148">동영상 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **테이블 데이터 표시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="22f5e-149">표시 되는 표에 가짜 영화 데이터를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="22f5e-150">ADO.NET 엔터티 데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="22f5e-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="22f5e-151">Entity Framework을 사용 하려면 엔터티 데이터 모델를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="22f5e-152">Visual Studio *엔터티 데이터 모델 마법사* 를 사용 하 여 데이터베이스에서 엔터티 데이터 모델를 자동으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="22f5e-153">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="22f5e-153">Follow these steps:</span></span>

1. <span data-ttu-id="22f5e-154">솔루션 탐색기 창의 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목을**차례로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="22f5e-155">**새 항목 추가** 대화 상자에서 데이터 범주를 선택 합니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="22f5e-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="22f5e-156">**ADO.NET 엔터티 데이터 모델** 템플릿을 선택 하 고 이름을 MoviesDBModel에 엔터티 데이터 모델 지정 하 고 **추가** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="22f5e-157">**추가** 단추를 클릭 하면 데이터 모델 마법사가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="22f5e-158">**모델 콘텐츠 선택** 단계에서 **데이터베이스에서 생성** 옵션을 선택 하 고 **다음** 단추를 클릭 합니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="22f5e-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="22f5e-159">**데이터 연결 선택** 단계에서 MoviesDB 데이터베이스 연결을 선택 하 고, 엔터티 연결 설정 이름 MoviesDBEntities을 입력 하 고, **다음** 단추를 클릭 합니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="22f5e-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="22f5e-160">**데이터베이스 개체 선택** 단계에서 동영상 데이터베이스 테이블을 선택 하 고 **마침** 단추를 클릭 합니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="22f5e-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="22f5e-161">이러한 단계를 완료 한 후에는 Entity Designer (ADO.NET 엔터티 데이터 모델 Designer)가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="22f5e-162">**그림 1-새 엔터티 데이터 모델 만들기**</span><span class="sxs-lookup"><span data-stu-id="22f5e-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

<span data-ttu-id="22f5e-164">**그림 2-모델 콘텐츠 선택 단계**</span><span class="sxs-lookup"><span data-stu-id="22f5e-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

<span data-ttu-id="22f5e-166">**그림 3-데이터 연결 선택**</span><span class="sxs-lookup"><span data-stu-id="22f5e-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

<span data-ttu-id="22f5e-168">**그림 4-데이터베이스 개체 선택**</span><span class="sxs-lookup"><span data-stu-id="22f5e-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="22f5e-170">ADO.NET 엔터티 데이터 모델 수정</span><span class="sxs-lookup"><span data-stu-id="22f5e-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="22f5e-171">엔터티 데이터 모델를 만든 후 Entity Designer를 활용 하 여 모델을 수정할 수 있습니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="22f5e-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="22f5e-172">솔루션 탐색기 창 내의 모델 폴더에 포함 된 MoviesDBModel 파일을 두 번 클릭 하 여 언제 든 지 Entity Designer을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="22f5e-173">**그림 5-ADO.NET 엔터티 데이터 모델 디자이너**</span><span class="sxs-lookup"><span data-stu-id="22f5e-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

<span data-ttu-id="22f5e-175">예를 들어 Entity Designer를 사용 하 여 엔터티 모델 데이터 마법사에서 생성 하는 클래스의 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="22f5e-176">마법사에서 영화 라는 새 데이터 액세스 클래스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="22f5e-177">즉, 마법사에서 클래스에 데이터베이스 테이블과 동일한 이름을 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="22f5e-178">이 클래스를 사용 하 여 특정 영화 인스턴스를 나타내기 때문에 클래스의 이름을 영화에서 동영상으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="22f5e-179">엔터티 클래스의 이름을 바꾸려면 Entity Designer의 클래스 이름을 두 번 클릭 하 고 새 이름을 입력 합니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="22f5e-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="22f5e-180">또는 Entity Designer에서 엔터티를 선택한 후 속성 창의 엔터티 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="22f5e-181">**그림 6-엔터티 이름 변경**</span><span class="sxs-lookup"><span data-stu-id="22f5e-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

<span data-ttu-id="22f5e-183">저장 단추 (플로피 디스크 아이콘)를 클릭 하 여 수정한 후에 엔터티 데이터 모델을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="22f5e-184">Entity Designer는 내부적으로 C# 클래스 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-184">Behind the scenes, the Entity Designer generates a set of C# classes.</span></span> <span data-ttu-id="22f5e-185">솔루션 탐색기 창에서 MoviesDBModel.Designer.cs 파일을 열어 이러한 클래스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-185">You can view these classes by opening the MoviesDBModel.Designer.cs file from the Solution Explorer window.</span></span>

<span data-ttu-id="22f5e-186">Designer.cs 파일에서 코드를 수정 하지 마세요. 다음에 Entity Designer를 사용할 때 변경 내용을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-186">Don't modify the code in the Designer.cs file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="22f5e-187">Designer.cs 파일에 정의 된 엔터티 클래스의 기능을 확장 하려는 경우에는 개별 파일에 *partial 클래스* 를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-187">If you want to extend the functionality of the entity classes defined in the Designer.cs file then you can create *partial classes* in separate files.</span></span>

#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="22f5e-188">Entity Framework를 사용 하 여 데이터베이스 레코드 선택</span><span class="sxs-lookup"><span data-stu-id="22f5e-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="22f5e-189">영화 레코드 목록을 표시 하는 페이지를 만들어 영화 데이터베이스 응용 프로그램 빌드를 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="22f5e-190">목록 1의 홈 컨트롤러는 Index () 라는 동작을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="22f5e-191">Index () 작업은 Entity Framework를 활용 하 여 Movie 데이터베이스 테이블의 모든 동영상 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="22f5e-192">**목록 1 – Controllers\ homecontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="22f5e-192">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

<span data-ttu-id="22f5e-193">1을 나열 하는 컨트롤러에는 생성자가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="22f5e-194">생성자는 \_db 라는 클래스 수준 필드를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="22f5e-195">\_db 필드는 Microsoft Entity Framework에서 생성 된 데이터베이스 엔터티를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="22f5e-196">\_db 필드는 Entity Designer 생성 된 MoviesDBEntities 클래스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>

<span data-ttu-id="22f5e-197">Home 컨트롤러에서 theMoviesDBEntities 클래스를 사용 하려면 MovieEntityApp 네임 스페이스 (*Mvcprojectname*)를 가져와야 합니다. 모델).</span><span class="sxs-lookup"><span data-stu-id="22f5e-197">In order to use theMoviesDBEntities class in the Home controller, you must import the MovieEntityApp.Models namespace (*MVCProjectName*.Models).</span></span>

<span data-ttu-id="22f5e-198">\_db 필드는 Index () 작업 내에서 영화 데이터베이스 테이블의 레코드를 검색 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-198">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="22f5e-199">식 \_db입니다. MovieSet는 동영상 데이터베이스 테이블의 모든 레코드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-199">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="22f5e-200">ToList () 메서드를 사용 하 여 동영상 집합을 동영상 개체의 제네릭 컬렉션 (목록&lt;동영상&gt;)으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-200">The ToList() method is used to convert the set of movies into a generic collection of Movie objects (List&lt;Movie&gt;).</span></span>

<span data-ttu-id="22f5e-201">동영상 레코드는 LINQ to Entities의 도움을 통해 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-201">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="22f5e-202">목록 1의 Index () 동작은 LINQ *메서드 구문을* 사용 하 여 데이터베이스 레코드 집합을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-202">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="22f5e-203">원하는 경우 LINQ *쿼리 구문을* 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-203">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="22f5e-204">다음 두 문은 동일한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-204">The following two statements do the very same thing:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

<span data-ttu-id="22f5e-205">가장 직관적인 LINQ 구문 (메서드 구문 또는 쿼리 구문)을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-205">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="22f5e-206">두 방법의 성능 차이는 없습니다. 유일한 차이점은 스타일입니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-206">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="22f5e-207">목록 2의 뷰는 영화 레코드를 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-207">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="22f5e-208">**목록 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="22f5e-208">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

<span data-ttu-id="22f5e-209">목록 2의 뷰에는 각 영화 레코드를 반복 하 고 영화 레코드의 제목 및 감독 속성 값을 표시 하는 **foreach** 루프가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-209">The view in Listing 2 contains a **foreach** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="22f5e-210">그러면 각 레코드 옆에 편집 및 삭제 링크가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-210">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="22f5e-211">또한 보기의 아래쪽에 영화 추가 링크가 표시 됩니다 (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="22f5e-211">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="22f5e-212">**그림 7-인덱스 뷰**</span><span class="sxs-lookup"><span data-stu-id="22f5e-212">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

<span data-ttu-id="22f5e-214">인덱스 뷰는 형식화 된 *뷰입니다*.</span><span class="sxs-lookup"><span data-stu-id="22f5e-214">The Index view is a *typed view*.</span></span> <span data-ttu-id="22f5e-215">인덱스 뷰에는 모델 속성을 Movie 개체의 강력한 형식의 제네릭 목록 컬렉션 (목록&lt;Movie)로 캐스팅 하는 *Inherits* 특성이 있는 &lt;% @ Page%&gt; 지시어가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-215">The Index view includes a &lt;%@ Page %&gt; directive with an *Inherits* attribute that casts the Model property to a strongly typed generic List collection of Movie objects (List&lt;Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="22f5e-216">Entity Framework를 사용 하 여 데이터베이스 레코드 삽입</span><span class="sxs-lookup"><span data-stu-id="22f5e-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="22f5e-217">Entity Framework를 사용 하 여 데이터베이스 테이블에 새 레코드를 쉽게 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="22f5e-218">목록 3에는 새 레코드를 Movie 데이터베이스 테이블에 삽입 하는 데 사용할 수 있는 새 작업 두 개가 홈 컨트롤러 클래스에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="22f5e-219">**목록 3 – Controllers\ homecontroller.cs (메서드 추가)**</span><span class="sxs-lookup"><span data-stu-id="22f5e-219">**Listing 3 – Controllers\HomeController.cs (Add methods)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

<span data-ttu-id="22f5e-220">첫 번째 Add () 작업은 단순히 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="22f5e-221">이 보기에는 새 동영상 데이터베이스 레코드를 추가 하기 위한 양식이 포함 되어 있습니다 (그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="22f5e-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="22f5e-222">양식을 제출 하면 두 번째 Add () 동작이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="22f5e-223">두 번째 Add () 동작은 AcceptVerbs 특성으로 데코 레이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="22f5e-224">HTTP POST 작업을 수행 하는 경우에만이 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="22f5e-225">즉, HTML 폼을 게시할 때만이 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="22f5e-226">두 번째 Add () 작업은 ASP.NET MVC TryUpdateModel () 메서드를 사용 하 여 Entity Framework Movie 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="22f5e-227">TryUpdateModel () 메서드는 Add () 메서드에 전달 되는 FormCollection의 필드를 사용 하 고 이러한 HTML 양식 필드의 값을 Movie 클래스에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>

<span data-ttu-id="22f5e-228">Entity Framework 사용 하는 경우 TryUpdateModel 또는 UpdateModel 메서드를 사용 하 여 엔터티 클래스의 속성을 업데이트할 때 속성의 "백서"를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>

<span data-ttu-id="22f5e-229">그런 다음 추가 () 작업은 몇 가지 간단한 폼 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="22f5e-230">작업은 Title 및 Director 속성 모두에 값이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="22f5e-231">유효성 검사 오류가 있는 경우 유효성 검사 오류 메시지가 ModelState에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="22f5e-232">유효성 검사 오류가 없으면 Entity Framework의 도움을 사용 하 여 새 동영상 레코드가 동영상 데이터베이스 테이블에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="22f5e-233">새 레코드는 다음 두 줄의 코드를 사용 하 여 데이터베이스에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

<span data-ttu-id="22f5e-234">코드의 첫 번째 줄은 Entity Framework에서 추적 하는 동영상 집합에 새 동영상 엔터티를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="22f5e-235">코드의 두 번째 줄에는 다시 기본 데이터베이스로 추적 되는 동영상의 모든 변경 내용이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="22f5e-236">**그림 8-추가 뷰**</span><span class="sxs-lookup"><span data-stu-id="22f5e-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="22f5e-238">Entity Framework를 사용 하 여 데이터베이스 레코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="22f5e-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="22f5e-239">거의 동일한 방법으로 Entity Framework를 사용 하 여 데이터베이스 레코드를 편집 하 여 새 데이터베이스 레코드를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="22f5e-240">목록 4에는 Edit () 라는 두 개의 새로운 컨트롤러 작업이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="22f5e-241">첫 번째 Edit () 작업은 동영상 레코드를 편집 하기 위한 HTML 폼을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="22f5e-242">두 번째 Edit () 작업은 데이터베이스 업데이트를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="22f5e-243">**목록 4 – Controllers\ homecontroller.cs (Edit 메서드)**</span><span class="sxs-lookup"><span data-stu-id="22f5e-243">**Listing 4 – Controllers\HomeController.cs (Edit methods)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

<span data-ttu-id="22f5e-244">두 번째 Edit () 작업은 편집 중인 동영상의 Id와 일치 하는 데이터베이스에서 영화 레코드를 검색 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="22f5e-245">다음 LINQ to Entities 문은 특정 Id와 일치 하는 첫 번째 데이터베이스 레코드를 가져와 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

<span data-ttu-id="22f5e-246">그런 다음 TryUpdateModel () 메서드를 사용 하 여 HTML 양식 필드의 값을 movie 엔터티의 속성에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="22f5e-247">업데이트할 정확한 속성을 지정 하기 위해 흰색 목록이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="22f5e-248">그런 다음, 영화 제목 및 감독 속성 모두에 값이 있는지 확인 하기 위해 몇 가지 간단한 유효성 검사가 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="22f5e-249">속성 중 하나에 값이 없는 경우 유효성 검사 오류 메시지가 ModelState 및 ModelState에 추가 됩니다. IsValid는 false 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="22f5e-250">마지막으로 유효성 검사 오류가 없는 경우에는 SaveChanges () 메서드를 호출 하 여 기본 영화 데이터베이스 테이블이 변경 내용으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="22f5e-251">데이터베이스 레코드를 편집할 때 데이터베이스 업데이트를 수행 하는 컨트롤러 작업에 편집 중인 레코드의 Id를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="22f5e-252">그렇지 않으면 컨트롤러 작업은 기본 데이터베이스에서 업데이트할 레코드를 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="22f5e-253">목록 5에 포함 된 편집 뷰는 편집 중인 데이터베이스 레코드의 Id를 나타내는 숨겨진 양식 필드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="22f5e-254">**목록 5 – Views\Home\Edit.aspx**</span><span class="sxs-lookup"><span data-stu-id="22f5e-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="22f5e-255">Entity Framework를 사용 하 여 데이터베이스 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="22f5e-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="22f5e-256">이 자습서에서 작업 해야 하는 최종 데이터베이스 작업은 데이터베이스 레코드를 삭제 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="22f5e-257">목록 6의 컨트롤러 작업을 사용 하 여 특정 데이터베이스 레코드를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="22f5e-258">**목록 6--\Controllers\HomeController.cs (Delete 동작)**</span><span class="sxs-lookup"><span data-stu-id="22f5e-258">**Listing 6 -- \Controllers\HomeController.cs (Delete action)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

<span data-ttu-id="22f5e-259">Delete () 작업은 먼저 작업에 전달 된 Id와 일치 하는 영화 엔터티를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="22f5e-260">다음으로, DeleteObject () 메서드를 호출한 다음 SaveChanges () 메서드를 호출 하 여 데이터베이스에서 동영상이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="22f5e-261">마지막으로 사용자가 인덱스 뷰로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="22f5e-262">요약</span><span class="sxs-lookup"><span data-stu-id="22f5e-262">Summary</span></span>

<span data-ttu-id="22f5e-263">이 자습서의 목적은 ASP.NET MVC 및 Microsoft Entity Framework를 활용 하 여 데이터베이스 기반 웹 응용 프로그램을 빌드하는 방법을 보여 주는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="22f5e-264">데이터베이스 레코드를 선택, 삽입, 업데이트 및 삭제할 수 있는 응용 프로그램을 빌드하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="22f5e-265">먼저 엔터티 데이터 모델 마법사를 사용 하 여 Visual Studio 내에서 엔터티 데이터 모델을 생성 하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="22f5e-266">다음으로 LINQ to Entities를 사용 하 여 데이터베이스 테이블에서 데이터베이스 레코드 집합을 검색 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="22f5e-267">마지막으로, Entity Framework를 사용 하 여 데이터베이스 레코드를 삽입, 업데이트 및 삭제 했습니다.</span><span class="sxs-lookup"><span data-stu-id="22f5e-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="22f5e-268">다음</span><span class="sxs-lookup"><span data-stu-id="22f5e-268">Next</span></span>](creating-model-classes-with-linq-to-sql-cs.md)
