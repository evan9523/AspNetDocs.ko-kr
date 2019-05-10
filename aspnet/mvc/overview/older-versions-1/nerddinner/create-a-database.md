---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 데이터베이스 만들기 | Microsoft Docs
author: microsoft
description: 2 단계 모두의 저녁 식사를 보유 하는 데이터베이스를 만들고 NerdDinner 응용 프로그램에 대 한 데이터를 회신 하는 단계를 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65117468"
---
# <a name="create-a-database"></a><span data-ttu-id="43214-103">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="43214-103">Create a Database</span></span>

<span data-ttu-id="43214-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="43214-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="43214-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="43214-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="43214-106">이 무료의 2 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="43214-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="43214-107">2 단계 모두의 저녁 식사를 보유 하는 데이터베이스를 만들고 NerdDinner 응용 프로그램에 대 한 데이터를 회신 하는 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43214-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="43214-108">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="43214-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="43214-109">NerdDinner Step 2: 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="43214-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="43214-110">사용 데이터베이스 NerdDinner 응용 프로그램에 대 한 Dinner 및 참석 여부 회신 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="43214-111">무료 SQL Server Express edition을 사용 하 여 데이터베이스를 만드는 다음 단계 표시 (의 V2를 사용 하 여 쉽게 설치할 수 있습니다 합니다 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span><span class="sxs-lookup"><span data-stu-id="43214-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="43214-112">SQL Server Express와 전체 SQL Server를 사용 하 여 작동 하는 모든 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="43214-113">새 SQL Server Express 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="43214-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="43214-114">에서는 웹 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 시작 하 고 다음을 선택 합니다 **추가-&gt;새 항목** 메뉴 명령:</span><span class="sxs-lookup"><span data-stu-id="43214-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="43214-115">Visual Studio의 "새 항목 추가" 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43214-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="43214-116">"데이터" 범주별으로 필터링 하 고 "SQL Server 데이터베이스" 항목 템플릿을 선택 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="43214-117">에서는 "NerdDinner.mdf" 만들고 적중 확인 하려는 SQL Server Express 데이터베이스를 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="43214-118">Visual Studio는 다음 문의 우리의 \App에이 파일을 추가 하고자 하는 경우\_데이터 디렉터리 (이미 디렉터리 읽기를 사용 하 여 설정 및 보안 Acl을 작성):</span><span class="sxs-lookup"><span data-stu-id="43214-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="43214-119">"예"를 클릭 하 고 새 데이터베이스 생성 되며이 솔루션 탐색기에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="43214-120">데이터베이스 내에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="43214-120">Creating Tables within our Database</span></span>

<span data-ttu-id="43214-121">이제 새 빈 데이터베이스를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-121">We now have a new empty database.</span></span> <span data-ttu-id="43214-122">일부 테이블을 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-122">Let's add some tables to it.</span></span>

<span data-ttu-id="43214-123">이렇게 하려면 데이터베이스 및 서버를 관리할 수 있게 하는 Visual Studio 내에서 "서버 탐색기" 탭 창으로 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43214-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="43214-124">SQL Server Express 데이터베이스를 \App에 저장 된\_응용 프로그램 데이터 폴더는 자동으로 내에 표시 서버 탐색기.</span><span class="sxs-lookup"><span data-stu-id="43214-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="43214-125">"서버 탐색기" 창 맨 위에 있는 "데이터베이스에 연결" 아이콘을를 사용 하 여 추가 SQL Server 데이터베이스 (로컬 및 원격 모두)도 목록에 추가 하려면 필요에 따라 했습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="43214-126">두 테이블에 RSVP도 추적 하는 Dinners 및 다른 저장 하나 NerdDinner 데이터베이스 –에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="43214-127">새 테이블 데이터베이스 내에서 "테이블" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 테이블 추가" 메뉴 명령을 선택 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="43214-128">테이블의 스키마를 구성할 수 있도록 하는 테이블 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="43214-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="43214-129">"Dinners" 테이블에 대 한 10 개 열의 데이터가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43214-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="43214-130">테이블에 대 한 고유 기본 키 여야 할 "DinnerID" 열을 표시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="43214-131">이 "DinnerID" 열을 마우스 오른쪽 단추로 클릭 하 고 "기본 키 설정" 메뉴 항목을 선택 하 여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="43214-132">DinnerID 기본 키 작업을 수행 하는 것 외에도 할 뿐 아니라이 값은 새 데이터 행을 테이블에 추가 됨에 따라 자동으로 증가 "id" 열으로 구성 (첫 번째 삽입된 Dinner 행 1의 DinnerID 해야 합니다. 즉, 두 번째 삽입 한 행 DinnerID 갖습니다 2 등).</span><span class="sxs-lookup"><span data-stu-id="43214-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="43214-133">"DinnerID" 열을 선택 하 여이 작업을 수행 하 고 "열 속성" 편집기를 사용 하 여 "Yes" 열에 "(Identity입니다)" 속성을 설정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="43214-134">표준 id 기본값을 사용 하 여 (1부터 시작 하 고 각 새 Dinner 행에 1을 증가).</span><span class="sxs-lookup"><span data-stu-id="43214-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="43214-135">Ctrl + S를 입력 하 여 또는 사용 하 여 테이블 저장 한 다음 됩니다 합니다 **파일-&gt;저장** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="43214-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="43214-136">이 테이블의 이름을 지정 하는 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="43214-136">This will prompt us to name the table.</span></span> <span data-ttu-id="43214-137">이름은 "Dinners":</span><span class="sxs-lookup"><span data-stu-id="43214-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="43214-138">새 Dinners 테이블은 서버 탐색기에서 데이터베이스 내에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43214-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="43214-139">에서는 그런 다음 위의 단계를 반복 하 고 "RSVP" 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43214-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="43214-140">사용 하 여이 테이블 3 열이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-140">This table with have 3 columns.</span></span> <span data-ttu-id="43214-141">기본 키로 RsvpID 열을 설정 하 고도 어렵게 id 열:</span><span class="sxs-lookup"><span data-stu-id="43214-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="43214-142">저장 하 고 이름을 "RSVP" 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43214-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="43214-143">테이블 간의 외래 키 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="43214-144">이제 데이터베이스 내에서 두 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-144">We now have two tables within our database.</span></span> <span data-ttu-id="43214-145">마지막 스키마 디자인 단계 각 Dinner 행 0 개 이상의 RSVP 행에 적용 되는 연결 수 있도록 이러한 두 테이블 간에 "일대다" 관계를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43214-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="43214-146">"Dinners" 테이블에서 "DinnerID" 열에 외래 키 관계에 RSVP 테이블의 "DinnerID" 열을 구성 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="43214-147">이렇게 하려면에서는 엽니다 참석 여부 회신은 테이블 디자이너에서는 서버 탐색기에서 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="43214-148">그 안의 "DinnerID" 열 선택 후 마우스 오른쪽 단추로 클릭 하 고 "관계..."를 선택 상황에 맞는 메뉴 명령:</span><span class="sxs-lookup"><span data-stu-id="43214-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="43214-149">테이블 간의 관계를 설정 하기 사용할 수 있는 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43214-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="43214-150">대화 상자에 새 관계를 추가 하려면 [추가] 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="43214-151">관계를 추가한 후 대화 상자의 오른쪽에 속성 표 내에서 "테이블 및 열 사양" 트리 뷰 노드를 확장 하 고 오른쪽의 "..." 단추를 클릭 하겠습니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="43214-152">"..." 단추를 클릭 하면 테이블 및 열을 관계와 관련 한 가지 뿐만 아니라 관계 이름 수를 지정할 수 있는 다른 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="43214-153">"Dinners" 되도록 기본 키 테이블을 변경 하 고 기본 키로 Dinners 테이블 내에서 "DinnerID" 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="43214-154">외래 키 테이블 및 RSVP RSVP 테이블이 됩니다. DinnerID 열이 외래 키와 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43214-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="43214-155">이제 RSVP 테이블의 각 행의를 저녁 테이블의 행과 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43214-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="43214-156">SQL Server는 미국 –에 대 한 참조 무결성을 유지 되며 올바른 Dinner 행을 가리키지 않을 경우 새 RSVP 행을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="43214-157">또한 수 없게 됩니다 미국에서 참조 하는 행을 여전히 RSVP 없으면 Dinner 행을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="43214-158">테이블에 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="43214-158">Adding Data to our Tables</span></span>

<span data-ttu-id="43214-159">보겠습니다 Dinners 테이블에 일부 샘플 데이터를 추가 하 여 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="43214-160">서버 탐색기 내에서 마우스 오른쪽 단추로 클릭 하 고 "테이블 데이터 표시" 명령을 선택 하 여 테이블에 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="43214-161">에서는 몇 가지 응용 프로그램을 구현 하는 대로 나중에 사용할 수는 Dinner 데이터 행 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="43214-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="43214-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43214-162">Next Step</span></span>

<span data-ttu-id="43214-163">데이터베이스 작성을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-163">We've finished creating our database.</span></span> <span data-ttu-id="43214-164">이제 쿼리 및 업데이트를 사용할 수 있는 모델 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="43214-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="43214-165">[이전](create-a-new-aspnet-mvc-project.md)
> [다음](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="43214-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
