---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: 엔터티 프레임워크(VB)를 통해 모델 클래스 만들기 | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서에서는 Microsoft 엔터티 프레임워크에서 ASP.NET MVC를 사용하는 방법을 배웁니다. 엔터티 마법사를 사용하여 엔터티 다와 ADO.NET 만드는 방법을 배웁니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: cdba91969a6ed9c02965999bbc48d5c5cdea140d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542653"
---
# <a name="creating-model-classes-with-the-entity-framework-vb"></a><span data-ttu-id="db7e3-104">Entity Framework를 사용하여 모델 클래스 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="db7e3-104">Creating Model Classes with the Entity Framework (VB)</span></span>

<span data-ttu-id="db7e3-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="db7e3-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="db7e3-106">이 자습서에서는 Microsoft 엔터티 프레임워크에서 ASP.NET MVC를 사용하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="db7e3-107">엔터티 마법사를 사용하여 엔터티 데이터 모델을 ADO.NET 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="db7e3-108">이 자습서의 과정에서 Entity Framework를 사용 하 여 데이터베이스 데이터를 선택, 삽입, 업데이트 및 삭제 하는 방법을 보여 주는 웹 응용 프로그램을 빌드 합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>

<span data-ttu-id="db7e3-109">이 자습서의 목표는 ASP.NET MVC 응용 프로그램을 빌드할 때 Microsoft 엔터티 프레임워크를 사용하여 데이터 액세스 클래스를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="db7e3-110">이 자습서는 Microsoft 엔터티 프레임워크에 대한 이전의 지식이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="db7e3-111">이 자습서가 끝나면 Entity Framework를 사용하여 데이터베이스 레코드를 선택, 삽입, 업데이트 및 삭제하는 방법을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="db7e3-112">Microsoft 엔터티 프레임워크는 데이터베이스에서 데이터 액세스 계층을 자동으로 생성할 수 있는 O/RM(개체 관계 매핑) 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="db7e3-113">Entity Framework를 사용하면 직접 데이터 액세스 클래스를 빌드하는 지루한 작업을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="db7e3-114">ASP.NET MVC와 Microsoft 엔터티 프레임워크 사이에는 필수적인 연결이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-114">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="db7e3-115">ASP.NET MVC에서 사용할 수 있는 엔터티 프레임워크에는 몇 가지 대안이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-115">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="db7e3-116">예를 들어 Microsoft LINQ와 같은 다른 O/RM 도구를 사용하여 SQL, NHibernate 또는 SubSonic에 MVC 모델 클래스를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-116">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>

<span data-ttu-id="db7e3-117">ASP.NET MVC와 함께 Microsoft 엔터티 프레임워크를 사용하는 방법을 설명하기 위해 간단한 샘플 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-117">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="db7e3-118">영화 데이터베이스 레코드를 표시하고 편집할 수 있는 영화 데이터베이스 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-118">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="db7e3-119">이 자습서에서는 서비스 팩 1을 통해 Visual Studio 2008 또는 Visual Web Developer 2008이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-119">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="db7e3-120">엔터티 프레임워크를 사용하려면 서비스 팩 1이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-120">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="db7e3-121">다음 주소에서 Visual Studio 2008 서비스 팩 1 또는 서비스 팩 1을 이와 함께 Visual Web 개발자를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-121">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="db7e3-122">동영상 샘플 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="db7e3-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="db7e3-123">영화 데이터베이스 응용 프로그램은 다음 열을 포함하는 Movies라는 데이터베이스 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="db7e3-124">열 이름</span><span class="sxs-lookup"><span data-stu-id="db7e3-124">Column Name</span></span> | <span data-ttu-id="db7e3-125">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="db7e3-125">Data Type</span></span> | <span data-ttu-id="db7e3-126">널 허용?</span><span class="sxs-lookup"><span data-stu-id="db7e3-126">Allow Nulls?</span></span> | <span data-ttu-id="db7e3-127">기본 키는?</span><span class="sxs-lookup"><span data-stu-id="db7e3-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db7e3-128">Id</span><span class="sxs-lookup"><span data-stu-id="db7e3-128">Id</span></span> | <span data-ttu-id="db7e3-129">int</span><span class="sxs-lookup"><span data-stu-id="db7e3-129">int</span></span> | <span data-ttu-id="db7e3-130">False</span><span class="sxs-lookup"><span data-stu-id="db7e3-130">False</span></span> | <span data-ttu-id="db7e3-131">True</span><span class="sxs-lookup"><span data-stu-id="db7e3-131">True</span></span> |
| <span data-ttu-id="db7e3-132">제목</span><span class="sxs-lookup"><span data-stu-id="db7e3-132">Title</span></span> | <span data-ttu-id="db7e3-133">은바르차르 (100)</span><span class="sxs-lookup"><span data-stu-id="db7e3-133">nvarchar(100)</span></span> | <span data-ttu-id="db7e3-134">False</span><span class="sxs-lookup"><span data-stu-id="db7e3-134">False</span></span> | <span data-ttu-id="db7e3-135">False</span><span class="sxs-lookup"><span data-stu-id="db7e3-135">False</span></span> |
| <span data-ttu-id="db7e3-136">감독</span><span class="sxs-lookup"><span data-stu-id="db7e3-136">Director</span></span> | <span data-ttu-id="db7e3-137">은바르차르 (100)</span><span class="sxs-lookup"><span data-stu-id="db7e3-137">nvarchar(100)</span></span> | <span data-ttu-id="db7e3-138">False</span><span class="sxs-lookup"><span data-stu-id="db7e3-138">False</span></span> | <span data-ttu-id="db7e3-139">False</span><span class="sxs-lookup"><span data-stu-id="db7e3-139">False</span></span> |

<span data-ttu-id="db7e3-140">다음 단계를 수행하여 이 테이블을 ASP.NET MVC 프로젝트에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="db7e3-141">솔루션 탐색기\_창에서 앱 데이터 폴더를 마우스 오른쪽 단추로 클릭하고 새 항목 추가 메뉴 옵션을 선택합니다. **Add, New Item.**</span><span class="sxs-lookup"><span data-stu-id="db7e3-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="db7e3-142">새 **항목 추가** 대화 상자에서 **SQL Server 데이터베이스를**선택하고 데이터베이스에 MoviesDB.mdf라는 이름을 지정하고 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="db7e3-143">MoviesDB.mdf 파일을 두 번 클릭하여 서버 탐색기/데이터베이스 탐색기 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="db7e3-144">MoviesDB.mdf 데이터베이스 연결을 확장하고 테이블 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션을 **선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="db7e3-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="db7e3-145">테이블 디자이너에서 ID, 제목 및 디렉터 열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="db7e3-146">**저장** 버튼(플로피 아이콘이 있음)을 클릭하여 새 테이블을 영화 이름으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="db7e3-147">Movies 데이터베이스 테이블을 만든 후 테이블에 일부 샘플 데이터를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="db7e3-148">동영상 테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 데이터 표시**옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="db7e3-149">표시되는 그리드에 가짜 동영상 데이터를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="db7e3-150">ADO.NET 엔터티 데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="db7e3-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="db7e3-151">엔터티 프레임워크를 사용하려면 엔터티 데이터 모델을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="db7e3-152">Visual Studio 엔터티 데이터 *모델 마법사를* 사용하여 데이터베이스에서 엔터티 데이터 모델을 자동으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="db7e3-153">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="db7e3-153">Follow these steps:</span></span>

1. <span data-ttu-id="db7e3-154">솔루션 탐색기 창에서 모델 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **추가, 새 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="db7e3-155">새 **항목 추가** 대화 상자에서 데이터 범주를 선택합니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="db7e3-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="db7e3-156">엔터티 **데이터 모델** ADO.NET 선택하고 엔터티 데이터 모델에 MoviesDBModel.edmx라는 이름을 지정한 다음 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="db7e3-157">**추가** 단추를 클릭하면 데이터 모델 마법사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="db7e3-158">모델 **내용 선택** 단계에서 **데이터베이스에서 생성** 옵션을 선택하고 **다음** 단추를 클릭합니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="db7e3-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="db7e3-159">데이터 **연결 선택** 단계에서 MoviesDB.mdf 데이터베이스 연결을 선택하고 엔터티 연결 설정 이름 MoviesDBEntities를 입력한 다음 **단추를** 클릭합니다(그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="db7e3-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="db7e3-160">데이터베이스 개체 선택 단계에서 동영상 데이터베이스 테이블을 선택하고 **완료** 단추를 **클릭합니다(그림** 4 참조).</span><span class="sxs-lookup"><span data-stu-id="db7e3-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="db7e3-161">이 단계를 완료하면 ADO.NET 엔터티 데이터 모델 디자이너(엔터티 디자이너)가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="db7e3-162">**그림 1 – 새 엔터티 데이터 모델 만들기**</span><span class="sxs-lookup"><span data-stu-id="db7e3-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

<span data-ttu-id="db7e3-164">**그림 2 - 모델 내용 단계 선택**</span><span class="sxs-lookup"><span data-stu-id="db7e3-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

<span data-ttu-id="db7e3-166">**그림 3 - 데이터 연결 선택**</span><span class="sxs-lookup"><span data-stu-id="db7e3-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

<span data-ttu-id="db7e3-168">**그림 4 – 데이터베이스 개체 선택**</span><span class="sxs-lookup"><span data-stu-id="db7e3-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="db7e3-170">ADO.NET 엔터티 데이터 모델 수정</span><span class="sxs-lookup"><span data-stu-id="db7e3-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="db7e3-171">엔터티 데이터 모델을 만든 후 엔터티 디자이너를 활용하여 모델을 수정할 수 있습니다(그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="db7e3-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="db7e3-172">솔루션 탐색기 창 내의 모델 폴더에 포함된 MoviesDBModel.edmx 파일을 두 번 클릭하여 언제든지 엔터티 디자이너를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="db7e3-173">**그림 5 – ADO.NET 엔터티 데이터 모델 디자이너**</span><span class="sxs-lookup"><span data-stu-id="db7e3-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

<span data-ttu-id="db7e3-175">예를 들어 엔터티 디자이너를 사용하여 엔터티 모델 데이터 마법사가 생성하는 클래스의 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="db7e3-176">마법사는 Movies라는 새 데이터 액세스 클래스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="db7e3-177">즉, 마법사는 클래스에 데이터베이스 테이블과 동일한 이름을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="db7e3-178">이 클래스를 사용하여 특정 동영상 인스턴스를 나타내므로 클래스의 이름을 동영상에서 동영상으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="db7e3-179">엔터티 클래스의 이름을 바꾸려면 엔터티 디자이너에서 클래스 이름을 두 번 클릭하고 새 이름을 입력할 수 있습니다(그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="db7e3-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="db7e3-180">또는 엔터티 디자이너에서 엔터티를 선택한 후 속성 창에서 엔터티 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="db7e3-181">**그림 6 - 엔터티 이름 변경**</span><span class="sxs-lookup"><span data-stu-id="db7e3-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

<span data-ttu-id="db7e3-183">저장 단추(플로피 디스크의 아이콘)를 클릭하여 수정한 후 엔터티 데이터 모델을 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="db7e3-184">이면에 엔터티 디자이너는 Visual Basic .NET 클래스 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-184">Behind the scenes, the Entity Designer generates a set of Visual Basic .NET classes.</span></span> <span data-ttu-id="db7e3-185">솔루션 탐색기 창에서 MoviesDBModel.Designer.vb 파일을 열어 이러한 클래스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-185">You can view these classes by opening the MoviesDBModel.Designer.vb file from the Solution Explorer window.</span></span>

<span data-ttu-id="db7e3-186">다음에 엔터티 디자이너를 사용할 때 변경 내용을 덮어쓰므로 Designer.vb 파일의 코드를 수정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="db7e3-186">Don't modify the code in the Designer.vb file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="db7e3-187">Designer.vb 파일에 정의된 엔터티 클래스의 기능을 확장하려면 별도의 파일에서 *부분 클래스를* 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-187">If you want to extend the functionality of the entity classes defined in the Designer.vb file then you can create *partial classes* in separate files.</span></span>

#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="db7e3-188">엔터티 프레임워크를 사용하여 데이터베이스 레코드 선택</span><span class="sxs-lookup"><span data-stu-id="db7e3-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="db7e3-189">영화 레코드 목록을 표시하는 페이지를 만들어 동영상 데이터베이스 응용 프로그램 빌드를 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="db7e3-190">목록 1의 홈 컨트롤러는 Index()라는 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="db7e3-191">Index() 작업은 엔터티 프레임워크를 활용하여 Movie 데이터베이스 테이블의 모든 동영상 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="db7e3-192">**목록 1 – 컨트롤러\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="db7e3-192">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

<span data-ttu-id="db7e3-193">목록 1의 컨트롤러에는 생성자가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="db7e3-194">생성자는 db라는 \_클래스 수준 필드를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="db7e3-195">\_db 필드는 Microsoft 엔터티 프레임워크에서 생성된 데이터베이스 엔터티를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="db7e3-196">\_db 필드는 엔터티 디자이너에 의해 생성된 MoviesDBEntities 클래스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>

<span data-ttu-id="db7e3-197">\_db 필드는 Index() 작업 내에서 사용되어 Movies 데이터베이스 테이블에서 레코드를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-197">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="db7e3-198">식 \_db입니다. MovieSet은 Movies 데이터베이스 테이블의 모든 레코드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-198">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="db7e3-199">ToList() 메서드는 동영상 집합을 동영상 개체의 일반 컬렉션인 동영상 목록(동영상)으로 변환하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-199">The ToList() method is used to convert the set of movies into a generic collection of Movie objects: List( Of Movie).</span></span>

<span data-ttu-id="db7e3-200">영화 레코드는 LINQ에서 엔터티로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-200">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="db7e3-201">목록 1의 Index() 작업은 LINQ *메서드 구문을* 사용하여 데이터베이스 레코드 집합을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-201">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="db7e3-202">원하는 경우 대신 LINQ *쿼리 구문을* 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-202">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="db7e3-203">다음 두 문은 매우 동일한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-203">The following two statements do the very same thing:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

<span data-ttu-id="db7e3-204">가장 직관적인 LINQ 구문(메서드 구문 또는 쿼리 구문)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-204">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="db7e3-205">두 방법 간의 성능 차이는 없습니다 - 유일한 차이점은 스타일입니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-205">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="db7e3-206">목록 2의 보기는 동영상 레코드를 표시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-206">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="db7e3-207">**목록 2 – 보기\홈\인덱스.aspx**</span><span class="sxs-lookup"><span data-stu-id="db7e3-207">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

<span data-ttu-id="db7e3-208">목록 2의 보기에는 각 동영상 레코드를 반복하고 영화 레코드의 제목 및 디렉터 속성 값을 표시하는 **For Each** 루프가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-208">The view in Listing 2 contains a **For Each** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="db7e3-209">각 레코드 옆에 편집 및 삭제 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-209">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="db7e3-210">또한 뷰 하단에 동영상 추가 링크가 나타납니다(그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="db7e3-210">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="db7e3-211">**그림 7 - 색인 보기**</span><span class="sxs-lookup"><span data-stu-id="db7e3-211">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

<span data-ttu-id="db7e3-213">인덱스 보기는 *형식이 입력된 보기입니다.*</span><span class="sxs-lookup"><span data-stu-id="db7e3-213">The Index view is a *typed view*.</span></span> <span data-ttu-id="db7e3-214">인덱스 보기에는 &lt;Inherits 특성을 포함하는 %@ Page %&gt; 지시문이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-214">The Index view has a &lt;%@ Page %&gt; directive that includes an Inherits attribute.</span></span> <span data-ttu-id="db7e3-215">Inherits 특성은 ViewData.Model 속성을 영화 개체의 강력한 형식의 일반 목록 컬렉션(동영상의 목록)으로 캐스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-215">The Inherits attribute casts the ViewData.Model property to a strongly typed generic List collection of Movie objects – a List(Of Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="db7e3-216">엔터티 프레임워크를 사용하여 데이터베이스 레코드 삽입</span><span class="sxs-lookup"><span data-stu-id="db7e3-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="db7e3-217">엔터티 프레임워크를 사용하여 데이터베이스 테이블에 새 레코드를 쉽게 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="db7e3-218">목록 3에는 Movie 데이터베이스 테이블에 새 레코드를 삽입하는 데 사용할 수 있는 홈 컨트롤러 클래스에 추가된 두 가지 새 작업이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="db7e3-219">**목록 3 – 컨트롤러\HomeController.vb (메서드 추가)**</span><span class="sxs-lookup"><span data-stu-id="db7e3-219">**Listing 3 – Controllers\HomeController.vb (Add methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

<span data-ttu-id="db7e3-220">첫 번째 Add() 작업은 뷰를 반환하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="db7e3-221">뷰에는 새 동영상 데이터베이스 레코드를 추가하기 위한 양식이 포함되어 있습니다(그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="db7e3-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="db7e3-222">양식을 제출하면 두 번째 Add() 작업이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="db7e3-223">두 번째 Add() 작업은 AcceptVerbs 특성으로 장식되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="db7e3-224">이 작업은 HTTP POST 작업을 수행할 때만 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="db7e3-225">즉, 이 작업은 HTML 양식을 게시할 때만 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="db7e3-226">두 번째 Add() 작업은 ASP.NET MVC TryUpdateModel() 메서드의 도움을 받아 엔터티 프레임워크 동영상 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="db7e3-227">TryUpdateModel() 메서드는 Add() 메서드에 전달된 FormCollection의 필드를 가져와 이러한 HTML 양식 필드의 값을 Movie 클래스에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>

<span data-ttu-id="db7e3-228">엔터티 프레임 워크를 사용 하는 경우 엔터티 클래스의 속성을 업데이트 하려면 TryUpdateModel 또는 UpdateModel 메서드를 사용 하는 경우 속성의 "화이트 리스트"를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>

<span data-ttu-id="db7e3-229">다음으로 Add() 작업은 몇 가지 간단한 양식 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="db7e3-230">이 작업은 Title 및 Director 속성에 값이 모두 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="db7e3-231">유효성 검사 오류가 있는 경우 유효성 검사 오류 메시지가 ModelState에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="db7e3-232">유효성 검사 오류가 없는 경우 엔터티 프레임워크의 도움을 받아 새 동영상 레코드가 Movies 데이터베이스 테이블에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="db7e3-233">새 레코드는 다음과 같은 두 줄의 코드로 데이터베이스에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

<span data-ttu-id="db7e3-234">코드의 첫 번째 줄은 엔터티 프레임워크에서 추적되는 동영상 집합에 새 Movie 엔터티를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="db7e3-235">두 번째 코드 줄은 기본 데이터베이스로 다시 추적되는 동영상에 대한 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="db7e3-236">**그림 8 - 추가 보기**</span><span class="sxs-lookup"><span data-stu-id="db7e3-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="db7e3-238">엔터티 프레임워크로 데이터베이스 레코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="db7e3-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="db7e3-239">엔터티 Framework를 사용하여 데이터베이스 레코드를 새 데이터베이스 레코드를 삽입하기 위해 방금 수행한 접근 방식과 거의 동일한 접근 방식을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="db7e3-240">목록 4에는 Edit()이라는 두 개의 새 컨트롤러 작업이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="db7e3-241">첫 번째 Edit() 작업은 영화 레코드를 편집하기 위한 HTML 양식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="db7e3-242">두 번째 편집() 작업은 데이터베이스를 업데이트하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="db7e3-243">**목록 4 – 컨트롤러\HomeController.vb (방법 편집)**</span><span class="sxs-lookup"><span data-stu-id="db7e3-243">**Listing 4 – Controllers\HomeController.vb (Edit methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

<span data-ttu-id="db7e3-244">두 번째 Edit() 작업은 편집중인 동영상의 ID와 일치하는 데이터베이스에서 동영상 레코드를 검색하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="db7e3-245">다음 LINQ to Entities 문은 특정 ID와 일치하는 첫 번째 데이터베이스 레코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

<span data-ttu-id="db7e3-246">다음으로 TryUpdateModel() 메서드는 HTML 양식 필드의 값을 동영상 엔터티의 속성에 할당하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="db7e3-247">업데이트할 정확한 속성을 지정하는 화이트리스트가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="db7e3-248">다음으로 영화 제목 및 디렉터 속성에 값이 있는지 확인하기 위해 몇 가지 간단한 유효성 검사가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="db7e3-249">두 속성 중 하나에 값이 없는 경우 유효성 검사 오류 메시지가 ModelState 및 ModelState.IsValid에 추가되어 false 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="db7e3-250">마지막으로 유효성 검사 오류가 없는 경우 기본 Movies 데이터베이스 테이블은 SaveChanges() 메서드를 호출하여 변경 내용으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="db7e3-251">데이터베이스 레코드를 편집할 때 편집중인 레코드의 ID를 데이터베이스 업데이트를 수행하는 컨트롤러 작업에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="db7e3-252">그렇지 않으면 컨트롤러 작업은 기본 데이터베이스에서 업데이트할 레코드를 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="db7e3-253">목록 5에 포함된 편집 보기에는 편집중인 데이터베이스 레코드의 ID를 나타내는 숨겨진 양식 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="db7e3-254">**목록 5 – 보기\홈\편집.aspx**</span><span class="sxs-lookup"><span data-stu-id="db7e3-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="db7e3-255">엔터티 프레임워크를 사용하여 데이터베이스 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="db7e3-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="db7e3-256">이 자습서에서 해결해야 하는 최종 데이터베이스 작업은 데이터베이스 레코드를 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="db7e3-257">목록 6의 컨트롤러 작업을 사용하여 특정 데이터베이스 레코드를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="db7e3-258">**목록 6 -- \컨트롤러\HomeController.vb (작업 삭제)**</span><span class="sxs-lookup"><span data-stu-id="db7e3-258">**Listing 6 -- \Controllers\HomeController.vb (Delete action)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

<span data-ttu-id="db7e3-259">Delete() 작업은 먼저 작업에 전달된 Id와 일치하는 동영상 엔터티를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="db7e3-260">다음으로, 동영상은 DeleteObject() 메서드를 호출한 다음 SaveChanges() 메서드를 호출하여 데이터베이스에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="db7e3-261">마지막으로 사용자가 색인 보기로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="db7e3-262">요약</span><span class="sxs-lookup"><span data-stu-id="db7e3-262">Summary</span></span>

<span data-ttu-id="db7e3-263">이 자습서의 목적은 ASP.NET MVC 및 Microsoft 엔터티 프레임워크를 활용하여 데이터베이스 기반 웹 응용 프로그램을 빌드하는 방법을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="db7e3-264">데이터베이스 레코드를 선택, 삽입, 업데이트 및 삭제할 수 있는 응용 프로그램을 빌드하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="db7e3-265">먼저 엔터티 데이터 모델 마법사를 사용하여 Visual Studio 내에서 엔터티 데이터 모델을 생성하는 방법에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="db7e3-266">다음으로 LINQto 엔터티를 사용하여 데이터베이스 테이블에서 데이터베이스 레코드 집합을 검색하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="db7e3-267">마지막으로 엔터티 프레임워크를 사용하여 데이터베이스 레코드를 삽입, 업데이트 및 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="db7e3-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="db7e3-268">[이전](validation-with-the-data-annotation-validators-cs.md)
> [다음](creating-model-classes-with-linq-to-sql-vb.md)</span><span class="sxs-lookup"><span data-stu-id="db7e3-268">[Previous](validation-with-the-data-annotation-validators-cs.md)
[Next](creating-model-classes-with-linq-to-sql-vb.md)</span></span>
