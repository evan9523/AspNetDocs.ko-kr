---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: 데이터베이스 역할 멤버 자격 테스트 환경에 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 테스트 환경에 솔루션 배포의 일부로 데이터베이스 역할에 사용자 계정을 추가 하는 방법을 설명 합니다. 포함 된 솔루션을 배포할 때 사용 하는 중...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: a15f5bf5f659d151e91ef9e53c5ad55bcd8e2b01
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130402"
---
# <a name="deploying-database-role-memberships-to-test-environments"></a><span data-ttu-id="0c4f1-104">테스트 환경에 데이터베이스 역할 멤버 자격 배포</span><span class="sxs-lookup"><span data-stu-id="0c4f1-104">Deploying Database Role Memberships to Test Environments</span></span>

<span data-ttu-id="0c4f1-105">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="0c4f1-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="0c4f1-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="0c4f1-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="0c4f1-107">이 항목에서는 테스트 환경에 솔루션 배포의 일부로 데이터베이스 역할에 사용자 계정을 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-107">This topic describes how to add user accounts to database roles as part of a solution deployment to a test environment.</span></span>
> 
> <span data-ttu-id="0c4f1-108">스테이징 또는 프로덕션 환경에 데이터베이스 프로젝트를 포함 하는 솔루션을 배포할 때는 일반적으로 원하지 개발자가 데이터베이스 역할에 사용자 계정을 추가 자동화할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-108">When you deploy a solution containing a database project to a staging or production environment, you typically don't want the developer to automate the addition of user accounts to database roles.</span></span> <span data-ttu-id="0c4f1-109">대부분의 경우에서 개발자는 데이터베이스 역할에 추가 해야 하는 사용자 계정을 알 수 없습니다 하 고 언제 든 지 이러한 요구 사항을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-109">In most cases, the developer won't know which user accounts need to be added to which database roles, and these requirements could change at any time.</span></span> <span data-ttu-id="0c4f1-110">그러나을 개발 하는 데이터베이스 프로젝트를 포함 하는 솔루션을 배포 하거나 테스트 환경을 상황은 일반적으로 다른:</span><span class="sxs-lookup"><span data-stu-id="0c4f1-110">However, when you deploy a solution containing a database project to a development or test environment, the situation is usually rather different:</span></span>
> 
> - <span data-ttu-id="0c4f1-111">개발자는 일반적으로 다시 솔루션도 배포 합니다는 정기적으로 하루에 여러 번 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-111">The developer typically re-deploys the solution on a regular basis, often several times a day.</span></span>
> - <span data-ttu-id="0c4f1-112">일반적으로 데이터베이스는 데이터베이스 사용자를 생성 및 모든 배포 후 역할에 추가 해야 하는 모든 배포에서 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-112">The database is typically re-created on every deployment, which means that database users must be created and added to roles after every deployment.</span></span>
> - <span data-ttu-id="0c4f1-113">일반적으로 개발자가 대상 개발 또는 테스트 환경 전체 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-113">The developer typically has full control over the target development or test environment.</span></span>
> 
> <span data-ttu-id="0c4f1-114">이 시나리오에서는 자동으로 데이터베이스 사용자를 만들고 배포 프로세스의 일부로 데이터베이스 역할 멤버 자격을 할당 하는 데 유용한 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-114">In this scenario, it's often beneficial to automatically create database users and assign database role memberships as part of the deployment process.</span></span>
> 
> <span data-ttu-id="0c4f1-115">주요 요인은이 작업 해야 함을 조건부 대상 환경에 따라입니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-115">The key factor is that this operation needs to be conditional based on the target environment.</span></span> <span data-ttu-id="0c4f1-116">스테이징 또는 프로덕션 환경에 배포 하는 경우 작업을 건너 뛰 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-116">If you're deploying to a staging or a production environment, you want to skip the operation.</span></span> <span data-ttu-id="0c4f1-117">개발자에 게 배포 하는 환경 테스트 하거나, 추가 개입 없이 역할 멤버 자격을 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-117">If you're deploying to a developer or test environment, you want to deploy role memberships without further intervention.</span></span> <span data-ttu-id="0c4f1-118">이 항목에서는 한 가지 방법은이 문제를 해결 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-118">This topic describes one approach you can use to address this challenge.</span></span>

<span data-ttu-id="0c4f1-119">이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="0c4f1-120">이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="0c4f1-121">빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="0c4f1-122">작업 개요</span><span class="sxs-lookup"><span data-stu-id="0c4f1-122">Task Overview</span></span>

<span data-ttu-id="0c4f1-123">이 항목을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-123">This topic assumes that:</span></span>

- <span data-ttu-id="0c4f1-124">분할 프로젝트 파일 방법은 솔루션 배포를 사용 하 여에 설명 된 대로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-124">You use the split project file approach to solution deployment, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span>
- <span data-ttu-id="0c4f1-125">에 설명 된 대로 VSDBCMD 데이터베이스 프로젝트를 배포 하려면 프로젝트 파일에서 호출할 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-125">You call VSDBCMD from the project file to deploy your database project, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

<span data-ttu-id="0c4f1-126">데이터베이스 사용자를 만들고 테스트 환경에 데이터베이스 프로젝트를 배포할 때 역할 멤버 자격을 할당 하려면를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-126">To create database users and assign role memberships when you deploy a database project to a test environment, you'll need to:</span></span>

- <span data-ttu-id="0c4f1-127">필요한 데이터베이스 변경을 수행 하는 Transact 구조적 쿼리 언어 (TRANSACT-SQL) 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-127">Create a Transact Structured Query Language (Transact-SQL) script that makes the necessary database changes.</span></span>
- <span data-ttu-id="0c4f1-128">Sqlcmd.exe 유틸리티를 사용 하 여 SQL 스크립트를 실행 하는 Microsoft Build Engine (MSBuild) 대상을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-128">Create a Microsoft Build Engine (MSBuild) target that uses the sqlcmd.exe utility to run the SQL script.</span></span>
- <span data-ttu-id="0c4f1-129">테스트 환경에 솔루션을 배포 하는 경우 대상을 호출 하 여 프로젝트 파일을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-129">Configure your project files to invoke the target when you're deploying your solution to a test environment.</span></span>

<span data-ttu-id="0c4f1-130">이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-130">This topic will show you how to perform each of these procedures.</span></span>

## <a name="scripting-the-database-role-memberships"></a><span data-ttu-id="0c4f1-131">데이터베이스 역할 멤버 자격을 스크립팅</span><span class="sxs-lookup"><span data-stu-id="0c4f1-131">Scripting the Database Role Memberships</span></span>

<span data-ttu-id="0c4f1-132">다른 방법으로 많은 Transact SQL 스크립트를 만들고 원하는 위치에.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-132">You can create a Transact-SQL script in a lot of different ways, and in any location you choose.</span></span> <span data-ttu-id="0c4f1-133">가장 쉬운 방법은 Visual Studio 2010의 솔루션 내에서 스크립트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-133">The easiest approach is to create the script within your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="0c4f1-134">**SQL 스크립트를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="0c4f1-134">**To create a SQL script**</span></span>

1. <span data-ttu-id="0c4f1-135">에 **솔루션 탐색기** 창에서 데이터베이스 프로젝트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-135">In the **Solution Explorer** window, expand your database project node.</span></span>
2. <span data-ttu-id="0c4f1-136">마우스 오른쪽 단추로 클릭 합니다 **스크립트** 폴더를 가리킵니다 **추가**를 클릭 하 고 **새 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-136">Right-click the **Scripts** folder, point to **Add**, and then click **New Folder**.</span></span>
3. <span data-ttu-id="0c4f1-137">형식 **테스트** 폴더 이름과 한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-137">Type **Test** as the folder name, and then press Enter.</span></span>
4. <span data-ttu-id="0c4f1-138">마우스 오른쪽 단추로 클릭 합니다 **테스트** 폴더를 가리킵니다 **추가**를 클릭 하 고 **스크립트**합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-138">Right-click the **Test** folder, point to **Add**, and then click **Script**.</span></span>
5. <span data-ttu-id="0c4f1-139">에 **새 항목 추가** 대화 상자에서 스크립트에 의미 있는 이름을 (예를 들어 **AddRoleMemberships.sql**)를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-139">In the **Add New Item** dialog box, give your script a meaningful name (for example, **AddRoleMemberships.sql**), and then click **Add**.</span></span>

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. <span data-ttu-id="0c4f1-140">에 *AddRoleMemberships.sql* 파일, TRANSACT-SQL 문을 추가 하는:</span><span class="sxs-lookup"><span data-stu-id="0c4f1-140">In the *AddRoleMemberships.sql* file, add Transact-SQL statements that:</span></span>

    1. <span data-ttu-id="0c4f1-141">데이터베이스를 액세스 하는 SQL Server 로그인에 대 한 데이터베이스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-141">Create a database user for the SQL Server login that will access your database.</span></span>
    2. <span data-ttu-id="0c4f1-142">필요한 데이터베이스 역할에 데이터베이스 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-142">Add the database user to any required database roles.</span></span>
7. <span data-ttu-id="0c4f1-143">파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-143">The file should resemble this:</span></span>

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. <span data-ttu-id="0c4f1-144">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-144">Save the file.</span></span>

## <a name="executing-the-script-on-the-target-database"></a><span data-ttu-id="0c4f1-145">대상 데이터베이스에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-145">Executing the Script on the Target Database</span></span>

<span data-ttu-id="0c4f1-146">이상적으로 데이터베이스 프로젝트를 배포할 때 배포 후 스크립트의 일부로 모든 필요한 TRANSACT-SQL 스크립트를 실행할 것 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-146">Ideally, you'd run any required Transact-SQL scripts as part of a post-deployment script when you deploy your database project.</span></span> <span data-ttu-id="0c4f1-147">그러나 배포 후 스크립트 솔루션 구성 또는 빌드 속성에 따라 조건부 논리를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-147">However, post-deployment scripts don't allow you to execute logic conditionally based on solution configurations or build properties.</span></span> <span data-ttu-id="0c4f1-148">대안은 만들어 MSBuild 프로젝트 파일에서 직접 SQL 스크립트를 실행 하는 **대상** sqlcmd.exe 명령을 실행 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-148">The alternative is to run your SQL scripts directly from the MSBuild project file, by creating a **Target** element that executes a sqlcmd.exe command.</span></span> <span data-ttu-id="0c4f1-149">대상 데이터베이스에서 스크립트를 실행 하려면이 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-149">You can use this command to run your script on the target database:</span></span>

[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]

> [!NOTE]
> <span data-ttu-id="0c4f1-150">Sqlcmd 명령줄 옵션에 대 한 자세한 내용은 참조 하세요. [sqlcmd 유틸리티](https://msdn.microsoft.com/library/ms162773.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-150">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>

<span data-ttu-id="0c4f1-151">이 명령은 MSBuild 대상에 포함 하면 전에 고려해 야 어떤 조건에서 스크립트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-151">Before you embed this command in an MSBuild target, you need to consider under what conditions you want the script to run:</span></span>

- <span data-ttu-id="0c4f1-152">대상 데이터베이스의 역할 멤버 자격을 변경 하기 전에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-152">The target database must exist before you change its role memberships.</span></span> <span data-ttu-id="0c4f1-153">이 스크립트를 실행 해야 하는 이와 같이 *후* 데이터베이스 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-153">As such, you need to run this script *after* the database deployment.</span></span>
- <span data-ttu-id="0c4f1-154">스크립트를 테스트 환경에만 실행 되도록 조건을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-154">You need to include a condition so that the script is only executed for test environments.</span></span>
- <span data-ttu-id="0c4f1-155">"What if" 배포를 실행 하는 경우&#x2014;즉, 배포 스크립트를 생성 하지만 실제로 실행 하는 경우&#x2014;SQL 스크립트를 실행 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-155">If you're running a "what if" deployment&#x2014;in other words, if you're generating deployment scripts but not actually running them&#x2014;you shouldn't run the SQL script.</span></span>

<span data-ttu-id="0c4f1-156">에 설명 된 분할 프로젝트 파일 방법을 사용 하는 경우 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), Contact Manager 샘플 솔루션에서 볼 수 있듯이, 다음과 같은 SQL 스크립트에 대 한 빌드 지침을 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-156">If you're using the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), as demonstrated by the Contact Manager sample solution, you can split the build instructions for your SQL script like this:</span></span>

- <span data-ttu-id="0c4f1-157">환경 관련 프로젝트 파일의 권한을 배포할지 여부를 결정 하는 속성과 함께 환경 관련 속성을 이동 해야 필요한 (예를 들어 *Env Dev.proj*).</span><span class="sxs-lookup"><span data-stu-id="0c4f1-157">Any required environment-specific properties, together with the property that determines whether to deploy permissions, should go in the environment-specific project file (for example, *Env-Dev.proj*).</span></span>
- <span data-ttu-id="0c4f1-158">대상 환경 간에 변경 되지 않는 모든 속성과 함께 MSBuild 대상 자체 유니버설 프로젝트 파일에서 이동 해야 합니다 (예를 들어 *Publish.proj*).</span><span class="sxs-lookup"><span data-stu-id="0c4f1-158">The MSBuild target itself, together with any properties that will not change between destination environments, should go in the universal project file (for example, *Publish.proj*).</span></span>

<span data-ttu-id="0c4f1-159">환경 관련 프로젝트 파일에서 데이터베이스 서버 이름, 대상 데이터베이스 이름 및 역할 멤버 자격을 배포할지 여부를 지정할 수 있도록 하는 부울 속성을 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-159">In the environment-specific project file, you need to define the database server name, the target database name, and a Boolean property that lets the user specify whether to deploy role memberships.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]

<span data-ttu-id="0c4f1-160">유니버설 프로젝트 파일에서 sqlcmd 실행 파일의 위치 및를 실행 하려는 SQL 스크립트의 위치를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-160">In the universal project file, you need to provide the location of the sqlcmd executable and the location of the SQL script you want to run.</span></span> <span data-ttu-id="0c4f1-161">이러한 속성 대상 환경에 관계 없이 동일 하 게 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-161">These properties will remain the same regardless of the destination environment.</span></span> <span data-ttu-id="0c4f1-162">Sqlcmd 명령을 실행 하는 MSBuild 대상을 만드는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-162">You also need to create an MSBuild target to execute the sqlcmd command.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]

<span data-ttu-id="0c4f1-163">다른 대상에 유용할 수 있습니다이으로 정적 속성으로 sqlcmd 실행 파일의 위치를 추가 하는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-163">Notice that you add the location of the sqlcmd executable as a static property, as this could be useful to other targets.</span></span> <span data-ttu-id="0c4f1-164">반면, SQL 스크립트의 위치 및 sqlcmd 명령의 구문을 대상 속성을 동적으로으로 정의한 되지 않으므로 필요한 대상이 실행 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-164">In contrast, you define the location of your SQL script and the syntax of the sqlcmd command as dynamic properties within the target, as they will not be required before the target is executed.</span></span> <span data-ttu-id="0c4f1-165">이 경우에 **DeployTestDBPermissions** 대상 이러한 조건이 충족 될 경우에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-165">In this case, the **DeployTestDBPermissions** target will only be executed if these conditions are met:</span></span>

- <span data-ttu-id="0c4f1-166">합니다 **DeployTestDBRoleMemberships** 속성이 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-166">The **DeployTestDBRoleMemberships** property is set to **true**.</span></span>
- <span data-ttu-id="0c4f1-167">사용자 지정 되지 않은 한 **WhatIf = true** 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-167">The user hasn't specified a **WhatIf=true** flag.</span></span>

<span data-ttu-id="0c4f1-168">마지막으로 반드시 대상을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-168">Finally, don't forget to invoke the target.</span></span> <span data-ttu-id="0c4f1-169">에 *Publish.proj* 파일을 할 수 있는이 대상 기본값에 대 한 종속성 목록에 추가 하 여 **FullPublish** 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-169">In the *Publish.proj* file, you can do this by adding the target to the dependency list for the default **FullPublish** target.</span></span> <span data-ttu-id="0c4f1-170">되도록 해야 합니다 **DeployTestDBPermissions** 대상 될 때까지 실행 되지 않습니다는 **PublishDbPackages** 대상이 실행 되었는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-170">You need to ensure that the **DeployTestDBPermissions** target is not executed until the **PublishDbPackages** target has been executed.</span></span>

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]

## <a name="conclusion"></a><span data-ttu-id="0c4f1-171">결론</span><span class="sxs-lookup"><span data-stu-id="0c4f1-171">Conclusion</span></span>

<span data-ttu-id="0c4f1-172">이 항목에서는 단방향은 추가할 수 있습니다 데이터베이스 사용자 및 역할 멤버 자격 배포 후 작업으로 데이터베이스 프로젝트를 배포 하는 경우를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-172">This topic described one way in which you can add database users and role memberships as a post-deployment action when you deploy a database project.</span></span> <span data-ttu-id="0c4f1-173">정기적으로 테스트 환경에서 데이터베이스를 다시 만들 경우 일반적으로를 피해 야 스테이징 또는 프로덕션 환경에 데이터베이스를 배포할 때 일반적으로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-173">This is typically useful when you regularly re-create a database in a test environment, but it should usually be avoided when you deploy databases to staging or production environments.</span></span> <span data-ttu-id="0c4f1-174">따라서 이렇게 하려면 적절 한 경우 데이터베이스 사용자 및 역할 멤버 자격만 생성 됩니다 있도록 필요한 조건부 논리를 사용 하는 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-174">As such, you should ensure that you use the necessary conditional logic so that database users and role memberships are only created when it's appropriate to do so.</span></span>

## <a name="further-reading"></a><span data-ttu-id="0c4f1-175">추가 정보</span><span class="sxs-lookup"><span data-stu-id="0c4f1-175">Further Reading</span></span>

<span data-ttu-id="0c4f1-176">VSDBCMD를 사용 하 여 데이터베이스 프로젝트를 배포 하는 방법은 참조 하세요 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-176">For more information on using VSDBCMD to deploy database projects, see [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="0c4f1-177">사용자 지정 된 다른 대상 환경에 대 한 데이터베이스 배포에 대 한 지침을 참조 하세요 [여러 환경에 대 한 데이터베이스 배포 사용자 지정](customizing-database-deployments-for-multiple-environments.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-177">For guidance on customizing database deployments for different target environments, see [Customizing Database Deployments for Multiple Environments](customizing-database-deployments-for-multiple-environments.md).</span></span> <span data-ttu-id="0c4f1-178">사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하에 대 한 자세한 내용은 참조 하세요. [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 하 고 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-178">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="0c4f1-179">Sqlcmd 명령줄 옵션에 대 한 자세한 내용은 참조 하세요. [sqlcmd 유틸리티](https://msdn.microsoft.com/library/ms162773.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c4f1-179">For more information on sqlcmd command-line options, see [sqlcmd Utility](https://msdn.microsoft.com/library/ms162773.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0c4f1-180">[이전](customizing-database-deployments-for-multiple-environments.md)
> [다음](deploying-membership-databases-to-enterprise-environments.md)</span><span class="sxs-lookup"><span data-stu-id="0c4f1-180">[Previous](customizing-database-deployments-for-multiple-environments.md)
[Next](deploying-membership-databases-to-enterprise-environments.md)</span></span>
