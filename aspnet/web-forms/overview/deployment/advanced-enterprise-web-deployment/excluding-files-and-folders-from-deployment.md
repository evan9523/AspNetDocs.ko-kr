---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: 배포에서 파일 및 폴더 제외 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 응용 프로그램 프로젝트를 빌드하고 패키지할 때 웹 배포 패키지에서 파일 및 폴더를 제외할 수 있는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438419"
---
# <a name="excluding-files-and-folders-from-deployment"></a><span data-ttu-id="4c1a8-103">배포에서 파일 및 폴더 제외</span><span class="sxs-lookup"><span data-stu-id="4c1a8-103">Excluding Files and Folders from Deployment</span></span>

<span data-ttu-id="4c1a8-104">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="4c1a8-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="4c1a8-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="4c1a8-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="4c1a8-106">이 항목에서는 웹 응용 프로그램 프로젝트를 빌드하고 패키지할 때 웹 배포 패키지에서 파일 및 폴더를 제외할 수 있는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-106">This topic describes how you can exclude files and folders from a web deployment package when you build and package a web application project.</span></span>

<span data-ttu-id="4c1a8-107">이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="4c1a8-108">이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="4c1a8-109">빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="overview"></a><span data-ttu-id="4c1a8-110">개요</span><span class="sxs-lookup"><span data-stu-id="4c1a8-110">Overview</span></span>

<span data-ttu-id="4c1a8-111">Visual Studio 2010에서 웹 응용 프로그램 프로젝트를 빌드하면 WPP (웹 게시 파이프라인)를 사용 하 여 컴파일된 웹 응용 프로그램을 배포 가능한 웹 패키지에 패키징하 여이 빌드 프로세스를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-111">When you build a web application project in Visual Studio 2010, the Web Publishing Pipeline (WPP) lets you extend this build process by packaging your compiled web application into a deployable web package.</span></span> <span data-ttu-id="4c1a8-112">그런 다음 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여이 웹 패키지를 원격 IIS 웹 서버에 배포 하거나 IIS 관리자를 통해 수동으로 웹 패키지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-112">You can then use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy this web package to a remote IIS web server, or import the web package manually through IIS Manager.</span></span> <span data-ttu-id="4c1a8-113">이 패키징 프로세스는 [웹 응용 프로그램 프로젝트 빌드 및 패키징](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-113">This packaging process is explained in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>

<span data-ttu-id="4c1a8-114">웹 패키지에 포함 되는 항목을 제어 하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="4c1a8-114">So how do you control what gets included in your web package?</span></span> <span data-ttu-id="4c1a8-115">기본 프로젝트 파일을 통해 Visual Studio의 프로젝트 설정은 많은 시나리오에 대 한 충분 한 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-115">The project settings in Visual Studio, through the underlying project file, provide sufficient control for a lot of scenarios.</span></span> <span data-ttu-id="4c1a8-116">그러나 경우에 따라 특정 대상 환경에 맞게 웹 패키지의 콘텐츠를 조정 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-116">However, in some cases you may want to tailor the contents of your web package to specific destination environments.</span></span> <span data-ttu-id="4c1a8-117">예를 들어 응용 프로그램을 테스트 환경에 배포할 때 로그 파일에 대 한 폴더를 포함 하 고 스테이징 또는 프로덕션 환경에 응용 프로그램을 배포할 때 해당 폴더를 제외 하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-117">For example, you might want to include a folder for log files when you deploy your application to a test environment but exclude the folder when you deploy the application to a staging or production environment.</span></span> <span data-ttu-id="4c1a8-118">이 항목에서는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-118">This topic will show you how to do this.</span></span>

## <a name="what-gets-included-by-default"></a><span data-ttu-id="4c1a8-119">기본적으로 포함 되는 항목</span><span class="sxs-lookup"><span data-stu-id="4c1a8-119">What Gets Included by Default?</span></span>

<span data-ttu-id="4c1a8-120">Visual Studio에서 웹 응용 프로그램 프로젝트 속성을 구성 하는 경우 **패키지/게시 웹** 페이지의 **배포할 항목** 목록에서 웹 배포 패키지에 포함할 항목을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-120">When you configure your web application project properties in Visual Studio, the **Items to deploy** list on the **Package/Publish Web** page lets you specify what you want to include in your web deployment package.</span></span> <span data-ttu-id="4c1a8-121">기본적으로이 **응용 프로그램을 실행 하는 데 필요한 파일만**으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-121">By default, this is set to **Only files needed to run this application**.</span></span>

![](excluding-files-and-folders-from-deployment/_static/image1.png)

<span data-ttu-id="4c1a8-122">**이 응용 프로그램을 실행 하는 데 필요한 파일만**선택 하는 경우 WPP는 웹 패키지에 추가 해야 하는 파일을 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-122">When you choose **Only files needed to run this application**, the WPP will try to determine which files should be added to the web package.</span></span> <span data-ttu-id="4c1a8-123">다음 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-123">This includes:</span></span>

- <span data-ttu-id="4c1a8-124">프로젝트에 대 한 모든 빌드 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-124">All the build outputs for the project.</span></span>
- <span data-ttu-id="4c1a8-125">**콘텐츠**빌드 작업으로 표시 된 모든 파일</span><span class="sxs-lookup"><span data-stu-id="4c1a8-125">Any files marked with a build action of **Content**.</span></span>

> [!NOTE]
> <span data-ttu-id="4c1a8-126">포함할 파일을 결정 하는 논리는 다음 파일에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-126">The logic that determines which files to include is contained in this file:</span></span>   
> <span data-ttu-id="4c1a8-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\. OnlyFilesToRunTheApp.*</span><span class="sxs-lookup"><span data-stu-id="4c1a8-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft.Web.Publishing.OnlyFilesToRunTheApp.targets*</span></span>

## <a name="excluding-specific-files-and-folders"></a><span data-ttu-id="4c1a8-128">특정 파일 및 폴더 제외</span><span class="sxs-lookup"><span data-stu-id="4c1a8-128">Excluding Specific Files and Folders</span></span>

<span data-ttu-id="4c1a8-129">어떤 경우에는 배포 되는 파일 및 폴더에 대해 보다 세분화 된 제어를 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-129">In some cases, you'll want more fine-grained control over which files and folders are deployed.</span></span> <span data-ttu-id="4c1a8-130">미리 제외 하려는 파일을 확인 하 고 제외를 모든 대상 환경에 적용 하는 경우 각 파일의 **빌드 작업** 을 **None**으로 간단히 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-130">If you know which files you want to exclude ahead of time, and the exclusion applies to all destination environments, you can simply set the **Build Action** of each file to **None**.</span></span>

<span data-ttu-id="4c1a8-131">**배포에서 특정 파일을 제외 하려면**</span><span class="sxs-lookup"><span data-stu-id="4c1a8-131">**To exclude specific files from deployment**</span></span>

1. <span data-ttu-id="4c1a8-132">**솔루션 탐색기** 창에서 파일을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-132">In the **Solution Explorer** window, right-click the file, and then click **Properties**.</span></span>
2. <span data-ttu-id="4c1a8-133">**속성** 창의 **빌드 작업** 행에서 **없음**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-133">In the **Properties** window, in the **Build Action** row, select **None**.</span></span>

<span data-ttu-id="4c1a8-134">그러나이 방법은 항상 편리 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-134">However, this approach is not always convenient.</span></span> <span data-ttu-id="4c1a8-135">예를 들어 대상 환경에 따라 그리고 Visual Studio 외부에서 포함 되는 파일 및 폴더를 변경 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-135">For example, you may want to vary which files and folders are included according to your destination environment, and from outside Visual Studio.</span></span> <span data-ttu-id="4c1a8-136">예를 들어 Contact manager 샘플 솔루션에서 다음을 수행 합니다. Mvc 프로젝트의 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-136">For example, in the Contact Manager sample solution, take a look at the contents of the ContactManager.Mvc project:</span></span>

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- <span data-ttu-id="4c1a8-137">내부 폴더에는 개발자가 개발 목적으로 로컬 데이터베이스를 만들고, 삭제 하 고, 채우기 위해 사용 하는 몇 가지 SQL 스크립트가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-137">The Internal folder contains some SQL scripts that the developer uses to create, drop, and populate local databases for development purposes.</span></span> <span data-ttu-id="4c1a8-138">이 폴더에는 스테이징 또는 프로덕션 환경에 배포할 내용이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-138">Nothing in this folder should be deployed to a staging or production environment.</span></span>
- <span data-ttu-id="4c1a8-139">Scripts 폴더에는 여러 JavaScript 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-139">The Scripts folder contains several JavaScript files.</span></span> <span data-ttu-id="4c1a8-140">이러한 파일은 대부분 Visual Studio에서 디버깅을 지원 하거나 IntelliSense를 제공 하기 위해서만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-140">A lot of these files are included purely to support debugging or provide IntelliSense in Visual Studio.</span></span> <span data-ttu-id="4c1a8-141">이러한 파일 중 일부는 스테이징 또는 프로덕션 환경에 배포 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-141">Some of these files should not be deployed to staging or production environments.</span></span> <span data-ttu-id="4c1a8-142">그러나 문제 해결을 용이 하 게 하기 위해 개발자 테스트 환경에 배포 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-142">However, you may want to deploy them to a developer test environment to facilitate troubleshooting.</span></span>

<span data-ttu-id="4c1a8-143">프로젝트 파일을 조작 하 여 특정 파일 및 폴더를 제외할 수는 있지만 더 쉬운 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-143">Although you could manipulate your project files to exclude specific files and folders, there is an easier way.</span></span> <span data-ttu-id="4c1a8-144">WPP에는 **ExcludeFromPackageFolders** 및 **ExcludeFromPackageFiles**라는 항목 목록을 작성 하 여 파일과 폴더를 제외 하는 메커니즘이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-144">The WPP includes a mechanism to exclude files and folders by building item lists named **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles**.</span></span> <span data-ttu-id="4c1a8-145">이러한 목록에 사용자 고유의 항목을 추가 하 여이 메커니즘을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-145">You can extend this mechanism by adding your own items to these lists.</span></span> <span data-ttu-id="4c1a8-146">이렇게 하려면 다음과 같은 개략적인 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-146">To do this, you need to complete these high-level steps:</span></span>

1. <span data-ttu-id="4c1a8-147">프로젝트 파일과 동일한 폴더에 *[project name]. wpp. .targets* 라는 사용자 지정 프로젝트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-147">Create a custom project file named *[project name].wpp.targets* in the same folder as your project file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4c1a8-148">웹 응용 프로그램 프로젝트&#x2014;파일과 동일한 *폴더 (예*&#x2014;: 빌드 및 배포 프로세스를 제어 하는 데 사용 하는 사용자 지정 프로젝트 파일)와 동일한 폴더에 있어야 *합니다.*</span><span class="sxs-lookup"><span data-stu-id="4c1a8-148">The *.wpp.targets* file needs to go in the same folder as your web application project file&#x2014;for example, *ContactManager.Mvc.csproj*&#x2014;rather than in the same folder as any custom project files you use to control the build and deployment process.</span></span>
2. <span data-ttu-id="4c1a8-149">*Wpp* 파일에서 **ItemGroup** 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-149">In the *.wpp.targets* file, add an **ItemGroup** element.</span></span>
3. <span data-ttu-id="4c1a8-150">**ItemGroup** 요소에서 **ExcludeFromPackageFolders** 및 **ExcludeFromPackageFiles** 항목을 추가 하 여 필요에 따라 특정 파일 및 폴더를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-150">In the **ItemGroup** element, add **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles** items to exclude specific files and folders as required.</span></span>

<span data-ttu-id="4c1a8-151">*이 파일의* 기본 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-151">This is the basic structure of this *.wpp.targets* file:</span></span>

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

<span data-ttu-id="4c1a8-152">각 항목에는 **Fromtarget**이라는 항목 메타 데이터 요소가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-152">Note that each item includes an item metadata element named **FromTarget**.</span></span> <span data-ttu-id="4c1a8-153">이는 빌드 프로세스에 영향을 주지 않는 선택적 값입니다. 사용자가 빌드 로그를 검토 하는 경우 특정 파일이 나 폴더가 생략 된 이유를 나타내는 역할만 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-153">This is an optional value that doesn't affect the build process; it simply serves to indicate why particular files or folders were omitted if someone reviews the build logs.</span></span>

## <a name="excluding-files-and-folders-from-a-web-package"></a><span data-ttu-id="4c1a8-154">웹 패키지에서 파일 및 폴더 제외</span><span class="sxs-lookup"><span data-stu-id="4c1a8-154">Excluding Files and Folders from a Web Package</span></span>

<span data-ttu-id="4c1a8-155">다음 절차에서는 웹 응용 프로그램 프로젝트에. n e t *.targets* 파일을 추가 하는 방법 및 프로젝트를 빌드할 때 파일을 사용 하 여 웹 패키지에서 특정 파일 및 폴더를 제외 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-155">The next procedure shows you how to add a *.wpp.targets* file to a web application project and how to use the file to exclude specific files and folders from the web package when you build your project.</span></span>

<span data-ttu-id="4c1a8-156">**웹 배포 패키지에서 파일 및 폴더를 제외 하려면**</span><span class="sxs-lookup"><span data-stu-id="4c1a8-156">**To exclude files and folders from a web deployment package**</span></span>

1. <span data-ttu-id="4c1a8-157">Visual Studio 2010에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-157">Open your solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="4c1a8-158">**솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 (예 **:),** **추가**를 가리킨 다음 **새 항목**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-158">In the **Solution Explorer** window, right-click your web application project node (for example, **ContactManager.Mvc**), point to **Add**, and then click **New Item**.</span></span>
3. <span data-ttu-id="4c1a8-159">**새 항목 추가** 대화 상자에서 **XML 파일** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-159">In the **Add New Item** dialog box, select the **XML File** template.</span></span>
4. <span data-ttu-id="4c1a8-160">**이름** 상자에 \*[project Name] \* \* \* *..* t a g e \* (예: **의사**(...))를 입력 한 다음 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-160">In the **Name** box, type *[project name]\*\*\*.wpp.targets*\* (for example, **ContactManager.Mvc.wpp.targets**), and then click **Add**.</span></span>

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="4c1a8-161">프로젝트의 루트 노드에 새 항목을 추가 하는 경우 해당 파일은 프로젝트 파일과 동일한 폴더에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-161">If you add a new item to the root node of a project, the file is created in the same folder as the project file.</span></span> <span data-ttu-id="4c1a8-162">Windows 탐색기에서 폴더를 열어이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-162">You can verify this by opening the folder in Windows Explorer.</span></span>
5. <span data-ttu-id="4c1a8-163">파일에서 **프로젝트** 요소와 **ItemGroup** 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-163">In the file, add a **Project** element and an **ItemGroup** element:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. <span data-ttu-id="4c1a8-164">웹 패키지에서 폴더를 제외 하려면 **ItemGroup** 요소에 **ExcludeFromPackageFolders** 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-164">If you want to exclude folders from the web package, add an **ExcludeFromPackageFolders** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="4c1a8-165">**Include** 특성에서 제외 하려는 폴더를 세미콜론으로 구분한 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-165">In the **Include** attribute, provide a semicolon-separated list of the folders you want to exclude.</span></span>
   2. <span data-ttu-id="4c1a8-166">**Fromtarget** metadata 요소에서 폴더를 제외 하는 이유 (예: *wpp* 파일의 이름)를 나타내는 의미 있는 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-166">In the **FromTarget** metadata element, provide a meaningful value to indicate why the folders are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. <span data-ttu-id="4c1a8-167">웹 패키지에서 파일을 제외 하려면 **ExcludeFromPackageFiles** 요소를 **ItemGroup** 요소에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-167">If you want to exclude files from the web package, add an **ExcludeFromPackageFiles** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="4c1a8-168">**Include** 특성에서 제외 하려는 파일의 세미콜론으로 구분 된 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-168">In the **Include** attribute, provide a semicolon-separated list of the files you want to exclude.</span></span>
   2. <span data-ttu-id="4c1a8-169">**Fromtarget** metadata 요소에서 파일을 제외 하는 이유 (예: *wpp* 파일의 이름)를 나타내는 의미 있는 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-169">In the **FromTarget** metadata element, provide a meaningful value to indicate why the files are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. <span data-ttu-id="4c1a8-170">이제 *[project name]. wpp* 파일은 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-170">The *[project name].wpp.targets* file should now resemble this:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. <span data-ttu-id="4c1a8-171">*[Project name] .targets .targets* 파일을 저장 한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-171">Save and close the *[project name].wpp.targets* file.</span></span>

<span data-ttu-id="4c1a8-172">다음 번에 웹 응용 프로그램 프로젝트를 빌드하고 패키지할 때 WPP는 *wpp 파일을* 자동으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-172">The next time you build and package your web application project, the WPP will automatically detect the *.wpp.targets* file.</span></span> <span data-ttu-id="4c1a8-173">지정한 모든 파일 및 폴더는 웹 패키지에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-173">Any files and folders you specified will not be included in the web package.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4c1a8-174">결론</span><span class="sxs-lookup"><span data-stu-id="4c1a8-174">Conclusion</span></span>

<span data-ttu-id="4c1a8-175">이 항목에서는 웹 응용 프로그램 프로젝트 파일과 동일한 폴더에 사용자 지정. n e t *.targets* 파일을 만들어 웹 패키지를 빌드할 때 특정 파일 및 폴더를 제외 하는 방법에 대해 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-175">This topic described how to exclude specific files and folders when you build a web package, by creating a custom *.wpp.targets* file in the same folder as your web application project file.</span></span>

## <a name="further-reading"></a><span data-ttu-id="4c1a8-176">추가 참고 자료</span><span class="sxs-lookup"><span data-stu-id="4c1a8-176">Further Reading</span></span>

<span data-ttu-id="4c1a8-177">사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하는 방법에 대 한 자세한 내용은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-177">For more information on using custom Microsoft Build Engine (MSBuild) project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="4c1a8-178">패키징 및 배포 프로세스에 대 한 자세한 내용은 [웹 응용 프로그램 프로젝트 빌드 및 패키징](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [웹 패키지 배포에 대 한 매개 변수 구성](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)및 [웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4c1a8-178">For more information on the packaging and deployment process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Configuring Parameters for Web Package Deployment](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md), and [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4c1a8-179">[이전](deploying-membership-databases-to-enterprise-environments.md)
> [다음](taking-web-applications-offline-with-web-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="4c1a8-179">[Previous](deploying-membership-databases-to-enterprise-environments.md)
[Next](taking-web-applications-offline-with-web-deploy.md)</span></span>
