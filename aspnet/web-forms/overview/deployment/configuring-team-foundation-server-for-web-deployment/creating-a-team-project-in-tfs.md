---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: TFS에서 팀 프로젝트 만들기 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 TFS (Team Foundation Server) 2010에서 새 팀 프로젝트를 만드는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519563"
---
# <a name="creating-a-team-project-in-tfs"></a><span data-ttu-id="95f65-103">TFS에서 팀 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="95f65-103">Creating a Team Project in TFS</span></span>

<span data-ttu-id="95f65-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="95f65-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="95f65-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="95f65-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="95f65-106">이 항목에서는 TFS (Team Foundation Server) 2010에서 새 팀 프로젝트를 만드는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-106">This topic describes how to create a new team project in Team Foundation Server (TFS) 2010.</span></span>

<span data-ttu-id="95f65-107">이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="95f65-108">작업 개요</span><span class="sxs-lookup"><span data-stu-id="95f65-108">Task Overview</span></span>

<span data-ttu-id="95f65-109">TFS에서 새 팀 프로젝트를 프로 비전 하 고 사용 하려면 다음과 같은 개략적인 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-109">To provision and use a new team project in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="95f65-110">새 팀 프로젝트를 만들 사용자에 게 사용 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-110">Grant permissions to the user who will create the new team project.</span></span>
- <span data-ttu-id="95f65-111">팀 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-111">Create the team project.</span></span>
- <span data-ttu-id="95f65-112">프로젝트에 대 한 작업을 수행할 팀 멤버에 게 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-112">Grant permissions to the team members who will work on the project.</span></span>
- <span data-ttu-id="95f65-113">일부 콘텐츠를 체크 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-113">Check in some content.</span></span>

<span data-ttu-id="95f65-114">이 항목에서는 이러한 절차를 수행 하는 방법을 보여 주고 각 절차를 담당 하 게 될 가능성이 높은 사용자 및 작업 역할을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-114">This topic will show you how to perform these procedures, and it will identify the users and job roles that are likely to be responsible for each procedure.</span></span> <span data-ttu-id="95f65-115">조직의 구조에 따라 이러한 각 작업은 다른 사용자의 책임 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-115">Be aware that, depending on the structure of your organization, each of these tasks may be the responsibility of a different person.</span></span>

<span data-ttu-id="95f65-116">이 항목의 작업 및 연습에서는 TFS를 설치 및 구성 하 고 구성 프로세스의 일부로 팀 프로젝트 컬렉션을 만들었다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-116">The tasks and walkthroughs in this topic assume that you've installed and configured TFS, and that you've created a team project collection as part of the configuration process.</span></span> <span data-ttu-id="95f65-117">이러한 가정에 대 한 자세한 내용 및 시나리오에 대 한 보다 일반적인 배경 정보는 [웹 배포용 TFS 빌드 서버 구성](configuring-a-tfs-build-server-for-web-deployment.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="95f65-117">For more information on these assumptions, and for more general background information on the scenario, see [Configure a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span>

## <a name="grant-permissions-to-the-team-project-creator"></a><span data-ttu-id="95f65-118">팀 프로젝트 작성자에 게 권한 부여</span><span class="sxs-lookup"><span data-stu-id="95f65-118">Grant Permissions to the Team Project Creator</span></span>

<span data-ttu-id="95f65-119">새 팀 프로젝트를 만들려면 다음 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-119">In order to create a new team project, you need these permissions:</span></span>

- <span data-ttu-id="95f65-120">TFS 응용 프로그램 계층에 대 한 **새 프로젝트 만들기** 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-120">You must have the **Create new projects** permission on the TFS application tier.</span></span> <span data-ttu-id="95f65-121">일반적으로 **Project Collection Administrators** TFS 그룹에 사용자를 추가 하 여이 사용 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-121">You typically grant this permission by adding users to the **Project Collection Administrators** TFS group.</span></span> <span data-ttu-id="95f65-122">**Team Foundation Administrators** 글로벌 그룹에도이 권한이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-122">The **Team Foundation Administrators** global group also includes this permission.</span></span>
- <span data-ttu-id="95f65-123">SharePoint 사이트 컬렉션 내에 TFS 팀 프로젝트 컬렉션에 해당 하는 새 팀 사이트를 만들 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-123">You must have permission to create new team sites within the SharePoint site collection that corresponds to the TFS team project collection.</span></span> <span data-ttu-id="95f65-124">일반적으로 SharePoint 사이트 모음에 대 한 **모든** 권한이 있는 sharepoint 그룹에 사용자를 추가 하 여이 사용 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-124">You typically grant this permission by adding the user to a SharePoint group with **Full Control** rights on the SharePoint site collection.</span></span>
- <span data-ttu-id="95f65-125">SQL Server Reporting Services 기능을 사용 하는 경우 Reporting Services에서 **Team Foundation Content Manager** 역할의 멤버 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-125">If you're using SQL Server Reporting Services features, you must be a member of the **Team Foundation Content Manager** role in Reporting Services.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="95f65-126">이러한 절차를 수행 하는 사람은 누구 인가요?</span><span class="sxs-lookup"><span data-stu-id="95f65-126">Who Performs These Procedures?</span></span>

<span data-ttu-id="95f65-127">일반적으로 TFS 배포를 관리 하는 개인 또는 그룹도 이러한 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-127">Typically, the person or group who administers the TFS deployment also performs these procedures.</span></span>

<span data-ttu-id="95f65-128">이는 권한이 높은 권한 집합 이기 때문에 일반적으로 TFS 배포 관리를 담당 하는 작은 사용자 하위 집합에서 새 팀 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-128">Because this is a highly privileged set of permissions, new team projects are typically created by a small subset of users with responsibility for administering a TFS deployment.</span></span> <span data-ttu-id="95f65-129">개발자에 게는 일반적으로 새 팀 프로젝트를 만드는 데 필요한 권한이 부여 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-129">Developers will not usually be granted the permissions required to create new team projects.</span></span>

### <a name="grant-permissions-in-tfs"></a><span data-ttu-id="95f65-130">TFS에서 권한 부여</span><span class="sxs-lookup"><span data-stu-id="95f65-130">Grant Permissions in TFS</span></span>

<span data-ttu-id="95f65-131">사용자가 새 팀 프로젝트를 만들 수 있도록 하려는 경우 가장 높은 수준의 작업은 팀 프로젝트 컬렉션에 대 한 **Project Collection Administrators** 그룹에 사용자를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-131">If you want to enable a user to create new team projects, the first high-level task is to add the user to the **Project Collection Administrators** group for the team project collection.</span></span>

<span data-ttu-id="95f65-132">**Project Collection Administrators 그룹에 사용자를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="95f65-132">**To add a user to the Project Collection Administrators group**</span></span>

1. <span data-ttu-id="95f65-133">TFS 서버의 **시작** 메뉴에서 **모든 프로그램**을 가리키고 **Microsoft Team Foundation Server 2010**를 클릭 한 다음 **Team Foundation 관리 콘솔**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-133">On the TFS server, on the **Start** menu, point to **All Programs**, click **Microsoft Team Foundation Server 2010**, and then click **Team Foundation Administration Console**.</span></span>
2. <span data-ttu-id="95f65-134">탐색 트리 보기에서 **응용 프로그램 계층**을 확장 한 다음 **팀 프로젝트 컬렉션**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-134">In the navigation tree view, expand **Application Tier**, and then click **Team Project Collections**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. <span data-ttu-id="95f65-135">**팀 프로젝트 컬렉션** 창에서 관리 하려는 팀 프로젝트 컬렉션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-135">In the **Team Project Collections** pane, select the team project collection you want to manage.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. <span data-ttu-id="95f65-136">**일반** 탭에서 **그룹 멤버 자격**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-136">On the **General** tab, click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. <span data-ttu-id="95f65-137">**전역 그룹** 대화 상자에서 **Project Collection Administrators** 그룹을 선택 하 고 **속성**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-137">In the **Global Groups** dialog box, select the **Project Collection Administrators** group, and then click **Properties**.</span></span>
6. <span data-ttu-id="95f65-138">**Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**을 선택 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-138">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. <span data-ttu-id="95f65-139">**사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 새 팀 프로젝트를 만들 사용자의 이름을 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-139">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to be able to create new team projects, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. <span data-ttu-id="95f65-140">**Team Foundation Server 그룹 속성** 대화 상자에서 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-140">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
9. <span data-ttu-id="95f65-141">**전역 그룹** 대화 상자에서 **닫기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-141">In the **Global Groups** dialog box, click **Close**.</span></span>

### <a name="grant-permissions-in-sharepoint-services"></a><span data-ttu-id="95f65-142">SharePoint Services에서 사용 권한 부여</span><span class="sxs-lookup"><span data-stu-id="95f65-142">Grant Permissions in SharePoint Services</span></span>

<span data-ttu-id="95f65-143">다음으로 사용자에 게 TFS 팀 프로젝트 컬렉션에 해당 하는 SharePoint 사이트 모음에 새 팀 사이트를 만들 수 있는 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-143">Next, you need to give the user permission to create new team sites in the SharePoint site collection that corresponds to your TFS team project collection.</span></span>

<span data-ttu-id="95f65-144">**SharePoint 사이트 모음에 대 한 모든 권한을 부여 하려면**</span><span class="sxs-lookup"><span data-stu-id="95f65-144">**To grant Full Control permissions on the SharePoint site collection**</span></span>

1. <span data-ttu-id="95f65-145">Team Foundation Server 관리 콘솔의 **팀 프로젝트 컬렉션** 페이지에서 관리 하려는 팀 프로젝트 컬렉션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-145">In the Team Foundation Server Administration Console, on the **Team Project Collections** page, select the team project collection you want to manage.</span></span>
2. <span data-ttu-id="95f65-146">**SharePoint 사이트** 탭에서 **현재 기본 사이트 위치** URL의 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-146">On the **SharePoint Site** tab, note the value of the **Current Default Site Location** URL.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. <span data-ttu-id="95f65-147">Internet Explorer를 열고 2 단계에서 적어둔 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-147">Open Internet Explorer, and then go to the URL you noted in step 2.</span></span>

    > [!NOTE]
    > <span data-ttu-id="95f65-148">팀 프로젝트 컬렉션을 만든 사용자로 Windows에 로그온 하지 않은 경우 계속 하려면 SharePoint에이 사용자로 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-148">If you're not logged on to Windows as the user who created the team project collection, you'll need to sign in to SharePoint as this user in order to continue.</span></span>
4. <span data-ttu-id="95f65-149">**사이트 동작** 메뉴에서 **사이트 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-149">On the **Site Actions** menu, click **Site Settings**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. <span data-ttu-id="95f65-150">**사이트 설정** 페이지의 **사용자 및 사용 권한**에서 **사용자 및 그룹**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-150">On the **Site Settings** page, under **Users and Permissions**, click **People and groups**.</span></span>
6. <span data-ttu-id="95f65-151">왼쪽 탐색 패널에서 **그룹**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-151">In the left navigation panel, click **Groups**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. <span data-ttu-id="95f65-152">**사용자 및 그룹: 모든 그룹** 페이지에서 **이 사이트에 대 한 그룹 설정**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-152">On the **People and Groups: All Groups** page, click **Set Up Groups for this Site**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > <span data-ttu-id="95f65-153">이중 HTTP 인코딩 버그로 인해 <strong>http 404 찾을</strong> 수 없음 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-153">You may receive an <strong>HTTP 404 Not Found</strong> error due to a double HTTP encoding bug.</span></span> <span data-ttu-id="95f65-154">이 경우 URL을 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-154">If this occurs, replace the URL with this:</span></span>   
   > <span data-ttu-id="95f65-155">`[site_collection_URL]/_layouts/permsetup.aspx` 예:</span><span class="sxs-lookup"><span data-stu-id="95f65-155">`[site_collection_URL]/_layouts/permsetup.aspx` For example:</span></span>  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. <span data-ttu-id="95f65-156">**이 사이트에 대 한 그룹 설정** 페이지에서 팀 프로젝트를 만들 사용자를 **소유자** 그룹에 추가한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-156">On the **Set Up Groups for this Site** page, add the user who will create team projects to the **Owners** group, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image10.png)

<span data-ttu-id="95f65-157">사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만들 수 있도록 설정 하는 방법에 대 한 자세한 내용은 [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/library/dd547204.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="95f65-157">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span>

## <a name="create-a-new-team-project-and-add-users"></a><span data-ttu-id="95f65-158">새 팀 프로젝트를 만들고 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="95f65-158">Create a New Team Project and Add Users</span></span>

<span data-ttu-id="95f65-159">필요한 권한이 있으면 Visual Studio 2010의 **팀 탐색기** 창을 사용 하 여 새 팀 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-159">Once you have the necessary permissions, you can use the **Team Explorer** window in Visual Studio 2010 to create a new team project.</span></span> <span data-ttu-id="95f65-160">이 방법은 필요한 모든 정보를 수집 하 고 TFS, SharePoint 및 SQL Server Reporting Services에서 필요한 작업을 수행 하는 마법사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-160">This approach provides a wizard that collects all the required information and performs the necessary tasks in TFS, SharePoint, and SQL Server Reporting Services.</span></span> <span data-ttu-id="95f65-161">또한 개발자 팀의 멤버에 게 새 팀 프로젝트에 대 한 권한을 부여 하 여 콘텐츠를 추가 하 고 수정할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-161">You'll also need to grant permissions on the new team project to members of the developer team, to enable them to add and modify content.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="95f65-162">이러한 절차를 수행 하는 사람은 누구 인가요?</span><span class="sxs-lookup"><span data-stu-id="95f65-162">Who Performs These Procedures?</span></span>

<span data-ttu-id="95f65-163">일반적으로 TFS 관리자 또는 개발자 팀 리더는 이러한 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-163">Usually either a TFS administrator or a developer team leader performs these procedures.</span></span>

### <a name="create-a-new-team-project"></a><span data-ttu-id="95f65-164">새 팀 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="95f65-164">Create a New Team Project</span></span>

<span data-ttu-id="95f65-165">다음 절차에서는 TFS 2010에서 새 팀 프로젝트를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-165">The next procedure describes how to create a new team project in TFS 2010.</span></span>

<span data-ttu-id="95f65-166">**새 팀 프로젝트를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="95f65-166">**To create a new team project**</span></span>

1. <span data-ttu-id="95f65-167">**시작** 메뉴에서 **모든 프로그램**을 가리키고 **Microsoft Visual Studio 2010**를 클릭 한 다음 **Microsoft Visual Studio 2010**을 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-167">On the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, right-click **Microsoft Visual Studio 2010**, and then click **Run as administrator**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="95f65-168">Visual Studio 2010을 관리자 권한으로 실행 하지 않으면 새 팀 프로젝트 마법사가 마지막 단계에서 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-168">If you don't run Visual Studio 2010 as an administrator, the New Team Project Wizard will fail on the last step.</span></span>
2. <span data-ttu-id="95f65-169">**사용자 계정 컨트롤** 대화 상자가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-169">If the **User Account Control** dialog box appears, click **Yes**.</span></span>
3. <span data-ttu-id="95f65-170">Visual Studio의 **팀** 메뉴에서 **Team Foundation Server에 연결**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-170">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="95f65-171">TFS 서버에 대 한 연결을 이미 구성한 경우에는 4-7 단계를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-171">If you have already configured a connection to a TFS server, you can omit steps 4-7.</span></span>
4. <span data-ttu-id="95f65-172">**팀 프로젝트에 연결** 대화 상자에서 **서버**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-172">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
5. <span data-ttu-id="95f65-173">**Team Foundation Server 추가/제거** 대화 상자에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-173">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
6. <span data-ttu-id="95f65-174">**Team Foundation Server 추가** 대화 상자에서 TFS 인스턴스의 세부 정보를 입력 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-174">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. <span data-ttu-id="95f65-175">**Team Foundation Server 추가/제거** 대화 상자에서 **닫기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-175">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
8. <span data-ttu-id="95f65-176">**팀 프로젝트에 연결** 대화 상자에서 연결할 TFS 인스턴스를 선택 하 고 추가 하려는 팀 프로젝트 컬렉션을 선택한 다음 **연결**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-176">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection you want to add to, and then click **Connect**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. <span data-ttu-id="95f65-177">**팀 탐색기** 창에서 팀 프로젝트 컬렉션을 마우스 오른쪽 단추로 클릭 한 다음 **새 팀 프로젝트**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-177">In the **Team Explorer** window, right-click the team project collection, and then click **New Team Project**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. <span data-ttu-id="95f65-178">**새 팀 프로젝트** 대화 상자에서 팀 프로젝트에 대 한 이름 및 설명을 입력 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-178">In the **New Team Project** dialog box, provide a name and a description for the team project, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="95f65-179">팀 프로젝트에 공백이 포함 된 경우 인터넷 정보 서비스 (IIS) 웹 배포 (웹 배포 도구)를 사용 하 여 출력 경로에서 패키지를 배포 하는 경우 몇 가지 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-179">If your team project includes spaces, you may face some issues when you come to use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy packages from the output path.</span></span> <span data-ttu-id="95f65-180">경로에 공백이 있으면 명령 웹 배포 실행 하기가 훨씬 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-180">Spaces in the path can make it a lot more difficult to run Web Deploy commands.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. <span data-ttu-id="95f65-181">**프로세스 템플릿 선택** 페이지에서 개발 프로세스를 관리 하는 데 사용할 프로세스 템플릿을 선택 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-181">On the **Select a Process Template** page, select the process template that you want to use to manage the development process, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="95f65-182">TFS의 프로세스 템플릿에 대 한 자세한 내용은 [프로세스 템플릿 및 도구](https://msdn.microsoft.com/vstudio/aa718795)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="95f65-182">For more information on process templates for TFS, see [Process Templates and Tools](https://msdn.microsoft.com/vstudio/aa718795).</span></span>
12. <span data-ttu-id="95f65-183">**팀 사이트 설정** 페이지에서 기본 설정을 변경 하지 않고 그대로 두고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-183">On the **Team Site Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
13. <span data-ttu-id="95f65-184">이 설정은 TFS 팀 프로젝트와 연결 된 SharePoint 팀 사이트를 만들거나 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-184">This setting creates, or identifies, a SharePoint team site that is associated with the TFS team project.</span></span> <span data-ttu-id="95f65-185">개발 팀은이 사이트를 사용 하 여 설명서를 관리 하 고, 토론 스레드에 참여 하 고, wiki 페이지를 만들고, 코드와 관련 되지 않은 다양 한 기타 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-185">Your development team can use this site to manage documentation, participate in discussion threads, create wiki pages, and perform various other tasks that are not related to code.</span></span> <span data-ttu-id="95f65-186">자세한 내용은 [SharePoint 제품 간의 상호 작용 및 Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="95f65-186">For more information, see [Interactions Between SharePoint Products and Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).</span></span>
14. <span data-ttu-id="95f65-187">**원본 제어 설정 지정** 페이지에서 기본 설정을 변경 하지 않고 그대로 **두고 다음을 클릭 합니다**.</span><span class="sxs-lookup"><span data-stu-id="95f65-187">On the **Specify Source Control Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
15. <span data-ttu-id="95f65-188">이 설정은 TFS 폴더 계층에서 콘텐츠에 대 한 루트 폴더 역할을 하는 위치를 식별 하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-188">This setting identifies or creates the location in the TFS folder hierarchy that will act as a root folder for your content.</span></span>
16. <span data-ttu-id="95f65-189">**팀 프로젝트 설정 확인** 페이지에서 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-189">On the **Confirm Team Project Settings** page, click **Finish**.</span></span>
17. <span data-ttu-id="95f65-190">새 팀 프로젝트가 성공적으로 만들어지면 **팀 프로젝트를 만든** 페이지에서 **닫기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-190">When the new team project is successfully created, on the **Team Project Created** page, click **Close**.</span></span>

### <a name="add-users-to-a-team-project"></a><span data-ttu-id="95f65-191">팀 프로젝트에 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="95f65-191">Add Users to a Team Project</span></span>

<span data-ttu-id="95f65-192">이제 새 팀 프로젝트를 만들었으므로 사용자에 게 콘텐츠를 추가 하 고 공동 작업을 시작할 수 있는 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-192">Now that you've created the new team project, you can grant permissions to users to enable them to start adding and collaborating on content.</span></span>

<span data-ttu-id="95f65-193">**팀 프로젝트에 사용자를 추가 하려면**</span><span class="sxs-lookup"><span data-stu-id="95f65-193">**To add users to a team project**</span></span>

1. <span data-ttu-id="95f65-194">Visual Studio 2010의 **팀 탐색기** 창에서 팀 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **팀 프로젝트 설정**을 가리킨 다음 **그룹 멤버 자격**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-194">In Visual Studio 2010, in the **Team Explorer** window, right-click the team project, point to **Team Project Settings**, and then click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. <span data-ttu-id="95f65-195">사용자가 소스 제어에서 코드를 추가, 수정 및 제거할 수 있도록 하려면 해당 사용자를 **Contributors** 그룹에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-195">To enable a user to add, modify, and remove code under source control, you need to add him or her to the **Contributors** group.</span></span>
3. <span data-ttu-id="95f65-196">**프로젝트 그룹** 대화 상자에서 **Contributors** 그룹을 선택 하 고 **속성**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-196">In the **Project Groups** dialog box, select the **Contributors** group, and then click **Properties**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. <span data-ttu-id="95f65-197">**Team Foundation Server 그룹 속성** 대화 상자에서 **Windows 사용자 또는 그룹**을 선택 하 고 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-197">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. <span data-ttu-id="95f65-198">**사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 팀 프로젝트에 추가 하려는 사용자의 이름을 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-198">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to add to the team project, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. <span data-ttu-id="95f65-199">**Team Foundation Server 그룹 속성** 대화 상자에서 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-199">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
7. <span data-ttu-id="95f65-200">**프로젝트 그룹** 대화 상자에서 **닫기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-200">In the **Project Groups** dialog box, click **Close**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="95f65-201">결론</span><span class="sxs-lookup"><span data-stu-id="95f65-201">Conclusion</span></span>

<span data-ttu-id="95f65-202">이 시점에서 새로운 팀 프로젝트를 사용할 준비가 되 고 개발자 팀이 개발 프로세스에서 콘텐츠를 추가 하 고 공동 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-202">At this point, your new team project is ready to use, and your developer team can start adding content and collaborating on the development process.</span></span>

<span data-ttu-id="95f65-203">다음 항목인 [소스 제어에](adding-content-to-source-control.md)콘텐츠 추가에서는 소스 제어에 콘텐츠를 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f65-203">The next topic, [Adding Content to Source Control](adding-content-to-source-control.md), describes how to add content to source control.</span></span>

## <a name="further-reading"></a><span data-ttu-id="95f65-204">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="95f65-204">Further Reading</span></span>

<span data-ttu-id="95f65-205">TFS에서 팀 프로젝트를 만드는 방법에 대 한 광범위 한 지침은 [팀 프로젝트 만들기](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="95f65-205">For broader guidance on creating team projects in TFS, see [Create a Team Project](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span></span> <span data-ttu-id="95f65-206">사용자가 팀 프로젝트 컬렉션 내에서 새 팀 프로젝트를 만들 수 있도록 설정 하는 방법에 대 한 자세한 내용은 [팀 프로젝트 컬렉션에 대 한 관리자 권한 설정](https://msdn.microsoft.com/library/dd547204.aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="95f65-206">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span> <span data-ttu-id="95f65-207">팀 프로젝트에 사용자를 추가 하는 방법에 대 한 자세한 내용은 [팀 프로젝트에 사용자 추가](https://msdn.microsoft.com/library/bb558971.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="95f65-207">For more information on adding users to team projects, see [Add Users to Team Projects](https://msdn.microsoft.com/library/bb558971.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="95f65-208">[이전](configuring-team-foundation-server-for-web-deployment.md)
> [다음](adding-content-to-source-control.md)</span><span class="sxs-lookup"><span data-stu-id="95f65-208">[Previous](configuring-team-foundation-server-for-web-deployment.md)
[Next](adding-content-to-source-control.md)</span></span>
