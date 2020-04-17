---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 데이터베이스 만들기 | Microsoft 문서
author: rick-anderson
description: 2단계는 NerdDinner 응용 프로그램에 대한 모든 저녁 식사 및 RSVP 데이터를 보유하는 데이터베이스를 만드는 단계를 보여 주며 있습니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541613"
---
# <a name="create-a-database"></a><span data-ttu-id="dfdb8-103">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="dfdb8-103">Create a Database</span></span>

<span data-ttu-id="dfdb8-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="dfdb8-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="dfdb8-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="dfdb8-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="dfdb8-106">이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 2단계입니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="dfdb8-107">2단계는 NerdDinner 응용 프로그램에 대한 모든 저녁 식사 및 RSVP 데이터를 보유하는 데이터베이스를 만드는 단계를 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="dfdb8-108">MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="dfdb8-109">얼간이 저녁 식사 2 단계: 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="dfdb8-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="dfdb8-110">우리는 우리의 NerdDinner 응용 프로그램에 대한 모든 Dinner 및 RSVP 데이터를 저장하는 데이터베이스를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="dfdb8-111">아래 단계는 무료 SQL Server Express [에디션(Microsoft 웹 플랫폼 설치 관리자의](https://www.microsoft.com/web/downloads/platform.aspx)V2를 사용하여 쉽게 설치할 수 있음)을 사용하여 데이터베이스를 만드는 것을 보여 준다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="dfdb8-112">작성할 모든 코드는 SQL Server Express 및 전체 SQL Server모두에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="dfdb8-113">새 SQL Server 익스프레스 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="dfdb8-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="dfdb8-114">먼저 웹 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **&gt;새 항목 추가** 메뉴 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="dfdb8-115">그러면 Visual Studio의 "새 항목 추가" 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="dfdb8-116">"데이터" 범주로 필터링하고 "SQL Server 데이터베이스" 항목 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="dfdb8-117">"NerdDinner.mdf"를 만들고 자하는 SQL Server Express 데이터베이스의 이름을 지정하고 확인을 누르겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="dfdb8-118">그런 다음 Visual Studio에서 이 파일을 \App\_Data 디렉토리에 추가할지 묻습니다(이미 읽기 및 쓰기 보안 ACL이 있는 디렉토리 설정입니다).</span><span class="sxs-lookup"><span data-stu-id="dfdb8-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="dfdb8-119">"예"를 클릭하고 새 데이터베이스가 만들어지고 솔루션 탐색기에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="dfdb8-120">데이터베이스 내에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="dfdb8-120">Creating Tables within our Database</span></span>

<span data-ttu-id="dfdb8-121">이제 새 빈 데이터베이스가 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-121">We now have a new empty database.</span></span> <span data-ttu-id="dfdb8-122">테이블에 테이블을 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-122">Let's add some tables to it.</span></span>

<span data-ttu-id="dfdb8-123">이렇게 하려면 Visual Studio 내의 "서버 탐색기" 탭 창으로 이동하여 데이터베이스와 서버를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="dfdb8-124">응용 프로그램의 \App\_Data 폴더에 저장된 SQL Server Express 데이터베이스는 서버 탐색기 내에 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="dfdb8-125">선택적으로 "Server Explorer" 창 위에 있는 "데이터베이스에 연결" 아이콘을 사용하여 목록에 SQL Server 데이터베이스(로컬 및 원격 모두)를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="dfdb8-126">우리는 우리의 NerdDinner 데이터베이스에 두 개의 테이블을 추가합니다 - 하나는 우리의 저녁 식사를 저장하고, 다른 하나는 그들에게 RSVP 수락을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="dfdb8-127">데이터베이스 내의 "테이블" 폴더를 마우스 오른쪽 단추로 클릭하고 "새 테이블 추가" 메뉴 명령을 선택하여 새 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="dfdb8-128">이렇게 하면 테이블의 스키마를 구성할 수 있는 테이블 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="dfdb8-129">"Dinners" 테이블에는 10개의 데이터 열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="dfdb8-130">"DinnerID" 열이 테이블의 고유한 기본 키가 되기를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="dfdb8-131">"DinnerID" 열을 마우스 오른쪽 단추로 클릭하고 "기본 키 설정" 메뉴 항목을 선택하여 이 항목을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="dfdb8-132">DinnerID를 기본 키로 만드는 것 외에도 새 데이터 행이 테이블에 추가될 때 값이 자동으로 증가하는 "ID" 열로 구성하려고 합니다(첫 번째 삽입된 Dinner 행에는 DinnerID가 1, 두 번째 삽입된 행에는 DinnerID가 2 등)됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="dfdb8-133">"DinnerID" 열을 선택한 다음 "열 속성" 편집기를 사용하여 열의 "(Id)" 속성을 "예"로 설정하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="dfdb8-134">표준 ID 기본값(새 저녁 식사 행마다 1부터 1부터 1부터 증가)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="dfdb8-135">그런 다음 Ctrl-S를 입력하거나 **File-Save&gt;** 메뉴 명령을 사용하여 테이블을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="dfdb8-136">이렇게 하면 테이블 이름을 지정하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-136">This will prompt us to name the table.</span></span> <span data-ttu-id="dfdb8-137">우리는 그것을 "저녁 식사"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="dfdb8-138">그러면 새 Dinners 테이블이 서버 탐색기의 데이터베이스 내에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="dfdb8-139">그런 다음 위의 단계를 반복하고 "RSVP" 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="dfdb8-140">이 테이블에는 3개의 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-140">This table with have 3 columns.</span></span> <span data-ttu-id="dfdb8-141">RsvpID 열을 기본 키로 설정하고 ID 열로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="dfdb8-142">우리는 그것을 저장하고 이름을 "RSVP"를 줄 것이다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="dfdb8-143">테이블 간에 외래 키 관계 설정</span><span class="sxs-lookup"><span data-stu-id="dfdb8-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="dfdb8-144">이제 데이터베이스 내에 두 개의 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-144">We now have two tables within our database.</span></span> <span data-ttu-id="dfdb8-145">마지막 스키마 디자인 단계는 이 두 테이블 간에 "일대다" 관계를 설정하여 각 Dinner 행을 0개 이상의 RSVP 행과 연결할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="dfdb8-146">RSVP 테이블의 "DinnerID" 열을 구성하여 "DinnerID" 테이블의 "DinnerID" 열과 외래 키 관계를 갖도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="dfdb8-147">이렇게 하려면 서버 탐색기에서 두 번 클릭하여 테이블 디자이너 내에서 RSVP 테이블을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="dfdb8-148">그런 다음 그 안에 있는 "DinnerID" 열을 선택하고 마우스 오른쪽 단추로 클릭하고 "관계..."를 선택합니다. 컨텍스트 메뉴 명령:</span><span class="sxs-lookup"><span data-stu-id="dfdb8-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="dfdb8-149">이렇게 하면 테이블 간의 관계를 설정하는 데 사용할 수 있는 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="dfdb8-150">"추가" 단추를 클릭하여 대화 상자에 새 관계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="dfdb8-151">관계가 추가되면 속성 그리드 내의 "테이블 및 열 사양" 트리 뷰 노드를 대화 상자 의 오른쪽에 확장한 다음 "..."를 클릭합니다. 그것의 오른쪽에 있는 버튼:</span><span class="sxs-lookup"><span data-stu-id="dfdb8-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="dfdb8-152">"..." 단추는 관계에 관련된 테이블과 열을 지정하고 관계의 이름을 지정할 수 있는 다른 대화 상자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="dfdb8-153">기본 키 테이블을 "저녁 식사"로 변경하고 저녁 식사 테이블 내의 "DinnerID" 열을 기본 키로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="dfdb8-154">우리의 RSVP 테이블은 외래 키 테이블과 RSVP가 됩니다. DinnerID 열은 외래 키로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="dfdb8-155">이제 RSVP 테이블의 각 행이 Dinner 테이블의 행과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="dfdb8-156">SQL Server는 참조 무결성을 유지하고 유효한 Dinner 행을 가리키지 않으면 새 RSVP 행을 추가하지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="dfdb8-157">또한 참조하는 RSVP 행이 여전히 있는 경우 Dinner 행을 삭제하지 못하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="dfdb8-158">테이블에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="dfdb8-158">Adding Data to our Tables</span></span>

<span data-ttu-id="dfdb8-159">Dinners 테이블에 샘플 데이터를 추가하여 완료해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="dfdb8-160">서버 탐색기 내에서 마우스 오른쪽 단추로 클릭하고 "테이블 데이터 표시" 명령을 선택하여 테이블에 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="dfdb8-161">나중에 응용 프로그램 구현을 시작할 때 사용할 수 있는 Dinner 데이터의 몇 행을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="dfdb8-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfdb8-162">Next Step</span></span>

<span data-ttu-id="dfdb8-163">데이터베이스 만들기를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-163">We've finished creating our database.</span></span> <span data-ttu-id="dfdb8-164">이제 쿼리하고 업데이트하는 데 사용할 수 있는 모델 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dfdb8-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dfdb8-165">[이전](create-a-new-aspnet-mvc-project.md)
> [다음](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="dfdb8-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
