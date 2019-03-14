---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: 엔터프라이즈 배포에서에서 웹 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 많은 개발자에 엔터프라이즈급 웹 응용 프로그램 배포를 관리 하는 경우 접할 수 과제를 충족 하는 방법을 설명 하는 중...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: 735cc5ac37e369e6149c526174c3f74a08db9758
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026160"
---
<a name="web-deployment-in-the-enterprise"></a><span data-ttu-id="ba137-103">기업에서 웹 배포</span><span class="sxs-lookup"><span data-stu-id="ba137-103">Web Deployment in the Enterprise</span></span>
====================
<span data-ttu-id="ba137-104">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="ba137-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="ba137-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="ba137-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="ba137-106">이 자습서에는 많은 개발, 테스트, 스테이징 및 프로덕션 환경에 엔터프라이즈급 웹 응용 프로그램 배포를 관리할 때 발생 하는 과제를 충족 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-106">This tutorial describes how to meet lots of the challenges you'll encounter when you manage the deployment of enterprise-scale web applications to development, test, staging, and production environments.</span></span> <span data-ttu-id="ba137-107">자습서에는 다양 한 일반 작업 및 절차를 안내 하는 개념 및 작업 기반 콘텐츠 혼합 함께 참조 솔루션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-107">The tutorial includes a reference solution together with a mixture of conceptual and task-oriented content to guide you through various common tasks and procedures.</span></span>
> 
> <span data-ttu-id="ba137-108">이 자습서의 번역을 이탈리아어를 방문 [ http://www.lucamorelli.it ](http://www.lucamorelli.it)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-108">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


## <a name="enterprise-deployment-challenges"></a><span data-ttu-id="ba137-109">엔터프라이즈 배포 과제</span><span class="sxs-lookup"><span data-stu-id="ba137-109">Enterprise Deployment Challenges</span></span>

<span data-ttu-id="ba137-110">조직에서는 복잡 한 엔터프라이즈급 솔루션의 배포를 관리 하는 경우 이러한 문제를 자주 발견:</span><span class="sxs-lookup"><span data-stu-id="ba137-110">Organizations often encounter these challenges when they look to manage the deployment of complex, enterprise-scale solutions:</span></span>

- <span data-ttu-id="ba137-111">해야 있으려면 개발자와 같은 여러 환경에 프로젝트를 배포 또는 테스트 환경, 플랫폼 및 프로덕션 서버를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-111">You need to be able to deploy projects to multiple environments, like developer or test environments, staging platforms, and production servers.</span></span> <span data-ttu-id="ba137-112">각 환경에 대 한 다른 구성 설정을 사용 하 여 배포 해야 하는 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-112">The solution needs to be deployed with different configuration settings for each environment.</span></span>
- <span data-ttu-id="ba137-113">단일 단계 또는 자동화 된 빌드 및 배포 프로세스의 일환으로 동시에 여러 종속 프로젝트를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-113">You need to deploy multiple dependent projects simultaneously as part of a single-step or automated build and deployment process.</span></span>
- <span data-ttu-id="ba137-114">자동화 된 프로세스에서 드라이브 배포 수 있게 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-114">You need to be able to drive deployment from an automated process.</span></span> <span data-ttu-id="ba137-115">예를 들어, 새 코드를 체크 인할 때 웹 응용 프로그램 테스트 환경에 배포 하는 CI (지속적인 통합) 프로세스를 사용 하려면.</span><span class="sxs-lookup"><span data-stu-id="ba137-115">For example, you want to use a continuous integration (CI) process to deploy web applications to a test environment when new code is checked in.</span></span>
- <span data-ttu-id="ba137-116">모든 대상 환경에 필요한 자격 증명 또는 잘못 구성 설정이 않을 것으로 배포 프로세스를 제어 하 고 Visual Studio 외부에서 배포 변수를 설정 하는 일을 할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-116">You need to be able to control the deployment process and set deployment variables from outside Visual Studio, as developers are unlikely to have the correct configuration settings or the necessary credentials for every target environment.</span></span>
- <span data-ttu-id="ba137-117">데이터베이스 스키마 기반 프로젝트를 배포 하 고 후속 배포에서 기존 데이터를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-117">You need to deploy schema-based database projects and preserve existing data on subsequent deployments.</span></span>
- <span data-ttu-id="ba137-118">사용자 계정 데이터를 배포 하지 않고 임시 단위로 멤버 자격 데이터베이스를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-118">You need to deploy membership databases on an ad hoc basis without deploying user account data.</span></span> <span data-ttu-id="ba137-119">기존 사용자 계정 데이터 손실 없이 배포 된 멤버 자격 데이터베이스의 스키마를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-119">You may also need to update the schema of deployed membership databases without losing existing user account data.</span></span>
- <span data-ttu-id="ba137-120">다양 한 대상 환경에 콘텐츠를 배포할 때 특정 파일 또는 폴더를 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-120">You need to exclude certain files or folders when you deploy content to various target environments.</span></span>

## <a name="overview-of-approach"></a><span data-ttu-id="ba137-121">접근 방법의 개요</span><span class="sxs-lookup"><span data-stu-id="ba137-121">Overview of Approach</span></span>

<span data-ttu-id="ba137-122">이 시리즈의 다른 자습서와 함께이 자습서에서는이 고급 방법을 사용 하 여 위에 설명 된 과제를 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-122">This tutorial, together with the other tutorials in this series, uses this high-level approach to meet the challenges described above.</span></span>

- <span data-ttu-id="ba137-123">**전체 빌드 및 배포 프로세스를 제어 하려면 사용자 지정 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ba137-123">**Use custom Microsoft Build Engine (MSBuild) project files to control the overall build and deployment process.**</span></span>
- <span data-ttu-id="ba137-124">이렇게 하면 빌드 및 스크립트 가능한 단일 작업의 일부분으로 솔루션의 모든 프로젝트를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-124">This lets you build and deploy every project in the solution as part of a single, scriptable operation.</span></span>
- <span data-ttu-id="ba137-125">환경 관련 설정 간단한 환경별 프로젝트 파일을 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-125">Environment-specific settings are configured using simple environment-specific project files.</span></span> <span data-ttu-id="ba137-126">솔루션 구성을 사용 하 여 Visual Studio – 중심 방식을 달리 다른 환경에 대 한 배포를 구성 하기 위해 게시 프로필을이 이렇게 구성 하 고 Visual Studio 외부에서 배포 프로세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-126">In contrast to the Visual Studio–centric approach of using solution configurations and publish profiles to configure deployments for different environments, this approach lets you configure and manage the deployment process from outside Visual Studio.</span></span> <span data-ttu-id="ba137-127">즉, 개발자가 없는 연결 문자열, 서비스 끝점, 서버 자격 증명 및 기타 배포 변수에 대상 환경에 대 한 지식이 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-127">This means that developers don't need advance knowledge of connection strings, service endpoints, server credentials, and other deployment variables for destination environments.</span></span>
- <span data-ttu-id="ba137-128">Team Foundation Server (TFS) 워크플로의 일부로 팀 빌드에서 사용자 지정 프로젝트 파일을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-128">The custom project files can be invoked by Team Build as part of a Team Foundation Server (TFS) workflow.</span></span> <span data-ttu-id="ba137-129">이 CI 시나리오에 대 한 자동화 된 배포를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-129">This lets you configure automated deployment for CI scenarios.</span></span>

<span data-ttu-id="ba137-130">**인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 패키지 및 웹 응용 프로그램 프로젝트를 배포 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ba137-130">**Use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to package and deploy web application projects.**</span></span>

- <span data-ttu-id="ba137-131">웹 배포 패키지 및 종속성, 구성 설정, 보안 설정 및 기타 요구 사항 함께 대상 IIS 웹 서버에 웹 응용 프로그램 콘텐츠를 배포할 수 있는 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-131">Web Deploy provides a framework that lets you package and deploy your web application content to a destination IIS web server, together with dependencies, configuration settings, security settings, and any other requirements.</span></span>
- <span data-ttu-id="ba137-132">사용자 지정 MSBuild 프로젝트 파일 내에서 전체 패키징 및 배포 프로세스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-132">You can control the entire packaging and deployment process from within your custom MSBuild project files.</span></span> <span data-ttu-id="ba137-133">또한 IIS 대상 세부 정보, 연결 문자열 및 서비스 끝점 등 웹 배포 패키지와 함께 제공 되는 구성 파일을 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-133">You can also manipulate the configuration settings that accompany your web deployment package, like connection strings, service endpoints, and IIS destination details.</span></span>
- <span data-ttu-id="ba137-134">웹 게시 파이프라인을 함께 웹 배포는 다양 한 배포를 사용자 지정할 수 있는 확장성 지점 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-134">Web Deploy, together with the Web Publishing Pipeline, offers lots of extensibility points that let you customize your deployments.</span></span> <span data-ttu-id="ba137-135">예를 들어, 웹 배포 패키지에서 원하지 않는 파일 및 폴더를 제외 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-135">For example, it's easy to exclude unwanted files and folders from your web deployment packages.</span></span>

<span data-ttu-id="ba137-136">**VSDBCMD.exe 유틸리티를 사용 하 여 배포 하 여 데이터베이스 스키마를 업데이트 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ba137-136">**Use the VSDBCMD.exe utility to deploy and update database schemas.**</span></span>

- <span data-ttu-id="ba137-137">VSDBCMD을 사용 하면 Visual Studio 데이터베이스 프로젝트를 빌드할 때 생성 되는 데이터베이스 스키마 파일 (.dbschema)에서 데이터베이스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-137">VSDBCMD allows you to deploy databases from a database schema file (.dbschema), which is generated when you build a Visual Studio database project.</span></span> <span data-ttu-id="ba137-138">반면, 웹 배포에 포함 된 데이터베이스 배포 기능은 로컬 SQL Server 인스턴스에서 기존 데이터베이스를 배포 하는 데 더 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-138">In contrast, the database deployment functionality included in Web Deploy is more suited to deploying existing databases from a local SQL Server instance.</span></span>
- <span data-ttu-id="ba137-139">데이터베이스 프로젝트를 배포 하기 위한 Visual Studio의 기능을 달리 VSDBCMD 기존 대상 데이터베이스에 차등 업데이트를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-139">Unlike Visual Studio's functionality for deploying database projects, VSDBCMD lets you deploy differential updates to an existing target database.</span></span> <span data-ttu-id="ba137-140">이 옵션을 사용 하면 데이터베이스 스키마를 업그레이드 하는 동안 모든 기존 데이터를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-140">This allows you to preserve any existing data while you upgrade the database schema.</span></span>
- <span data-ttu-id="ba137-141">사용자 지정 MSBuild 프로젝트 파일 내에서 VSDBCMD 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-141">You can execute VSDBCMD commands from within your custom MSBuild project files.</span></span>

## <a name="content-map"></a><span data-ttu-id="ba137-142">콘텐츠 맵</span><span class="sxs-lookup"><span data-stu-id="ba137-142">Content Map</span></span>

<span data-ttu-id="ba137-143">이 자습서에는 네 가지 주요 영역에 부합 하는 항목이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-143">This tutorial includes topics that fall into four main areas.</span></span>

<span data-ttu-id="ba137-144">이러한 항목을 참조 솔루션 소개&#x2014;Contact Manager 솔루션&#x2014;다운로드 하 여 로컬 컴퓨터에 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-144">These topics introduce the reference solution&#x2014;the Contact Manager solution&#x2014;and describe how to download it and configure it on your local machine:</span></span>

- [<span data-ttu-id="ba137-145">Contact Manager 솔루션</span><span class="sxs-lookup"><span data-stu-id="ba137-145">The Contact Manager Solution</span></span>](the-contact-manager-solution.md)
- [<span data-ttu-id="ba137-146">Contact Manager 솔루션 설정</span><span class="sxs-lookup"><span data-stu-id="ba137-146">Setting Up the Contact Manager Solution</span></span>](setting-up-the-contact-manager-solution.md)

<span data-ttu-id="ba137-147">이러한 항목 MSBuild 프로젝트 파일을 소개, 만들기 및 사용자 지정 프로젝트 파일을 사용 하는 방법 Contact Manager 솔루션에 대 한 배포 프로세스를 단계별로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-147">These topics introduce MSBuild project files, describe how you can create and use custom project files, and walk through the deployment process for the Contact Manager solution:</span></span>

- [<span data-ttu-id="ba137-148">프로젝트 파일 이해</span><span class="sxs-lookup"><span data-stu-id="ba137-148">Understanding the Project File</span></span>](understanding-the-project-file.md)
- [<span data-ttu-id="ba137-149">빌드 프로세스 이해</span><span class="sxs-lookup"><span data-stu-id="ba137-149">Understanding the Build Process</span></span>](understanding-the-build-process.md)

<span data-ttu-id="ba137-150">빌드 및 패키징 프로세스 작동 방식, 웹 게시 파이프라인을 사용 하 여 빌드 프로세스를 통합 하는 방법, 배포 매개 변수를 수정 하는 방법 및 대상 웹 패키지를 배포 하는 방법을 포함 하 여 웹 응용 프로그램 배포에 설명 환경:</span><span class="sxs-lookup"><span data-stu-id="ba137-150">These topics describe web application deployment, including how the build and packaging process works, how the build process integrates with the Web Publishing Pipeline, how to modify deployment parameters, and how to deploy web packages to destination environments:</span></span>

- [<span data-ttu-id="ba137-151">웹 애플리케이션 프로젝트 빌드 및 패키징</span><span class="sxs-lookup"><span data-stu-id="ba137-151">Building and Packaging Web Application Projects</span></span>](building-and-packaging-web-application-projects.md)
- [<span data-ttu-id="ba137-152">웹 패키지 배포용 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="ba137-152">Configuring Parameters for Web Package Deployment</span></span>](configuring-parameters-for-web-package-deployment.md)
- [<span data-ttu-id="ba137-153">웹 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="ba137-153">Deploying Web Packages</span></span>](deploying-web-packages.md)

- <span data-ttu-id="ba137-154">[데이터베이스 프로젝트 배포](deploying-database-projects.md) 장점과 각 접근 방식의 단점와 함께 Visual Studio 데이터베이스 프로젝트를 배포 하 여 다양 한 기법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-154">[Deploying Database Projects](deploying-database-projects.md) describes the different techniques you can use to deploy Visual Studio database projects, together with the advantages and disadvantages of each approach.</span></span> <span data-ttu-id="ba137-155">[만들기 및 배포 명령 파일을 실행](creating-and-running-a-deployment-command-file.md) 배포 논리를 캡슐화 하 고 단일 단계 프로세스로 복잡 한 솔루션을 배포할 수 있습니다 하는 간단한 명령 파일을 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-155">[Creating and Running a Deployment Command File](creating-and-running-a-deployment-command-file.md) describes how to create a simple command file that encapsulates your deployment logic and lets you deploy complex solutions as a single-step process.</span></span>
- <span data-ttu-id="ba137-156">마지막으로, [수동으로 웹 패키지 설치](manually-installing-web-packages.md) 으로 IIS 웹 패키지를 가져올 수를 표시 하 여 자습서를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-156">Finally, [Manually Installing Web Packages](manually-installing-web-packages.md) concludes the tutorial by showing you to import web packages into IIS.</span></span>

## <a name="key-technologies"></a><span data-ttu-id="ba137-157">핵심 기술</span><span class="sxs-lookup"><span data-stu-id="ba137-157">Key Technologies</span></span>

<span data-ttu-id="ba137-158">이 자습서의 항목에서는 주로이 기술을 사용 하 여 이러한 빌드 및 배포를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-158">The topics in this tutorial primarily use these technologies to manage build and deployment:</span></span>

- <span data-ttu-id="ba137-159">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="ba137-159">Visual Studio 2010</span></span>
- <span data-ttu-id="ba137-160">MSBuild</span><span class="sxs-lookup"><span data-stu-id="ba137-160">MSBuild</span></span>
- <span data-ttu-id="ba137-161">IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="ba137-161">IIS 7.5</span></span>
- <span data-ttu-id="ba137-162">웹 배포 2.0</span><span class="sxs-lookup"><span data-stu-id="ba137-162">Web Deploy 2.0</span></span>
- <span data-ttu-id="ba137-163">VSDBCMD.exe 데이터베이스 배포 유틸리티</span><span class="sxs-lookup"><span data-stu-id="ba137-163">The VSDBCMD.exe database deployment utility</span></span>

## <a name="other-tutorials-in-this-series"></a><span data-ttu-id="ba137-164">이 시리즈의 다른 자습서</span><span class="sxs-lookup"><span data-stu-id="ba137-164">Other Tutorials in This Series</span></span>

<span data-ttu-id="ba137-165">이 엔터프라이즈급 웹 배포에서 다섯 개의 자습서 시리즈의 일부를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-165">This forms part of a series of five tutorials on enterprise-scale web deployment.</span></span> <span data-ttu-id="ba137-166">다른 자습서 시리즈의은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-166">These are the other tutorials in the series:</span></span>

- <span data-ttu-id="ba137-167">[엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-167">[Deploying Web Applications in Enterprise Scenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span> <span data-ttu-id="ba137-168">이 소개 콘텐츠 자습서 시리즈에 대 한 상황에 맞는 배경 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-168">This introductory content provides the contextual background for the tutorial series.</span></span> <span data-ttu-id="ba137-169">자습서 시나리오를 설명 하 고 작업 및 연습 시리즈 전반에 설명 되어 광범위 한 응용 프로그램 수명 주기 관리 (ALM) 프로세스에 적합 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-169">It describes the tutorial scenario, and it illustrates how the tasks and walkthroughs described throughout the series fit into a broader Application Lifecycle Management (ALM) process.</span></span>
- <span data-ttu-id="ba137-170">[웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-170">[Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span> <span data-ttu-id="ba137-171">이 자습서에는 웹 배포 에이전트 서비스 (원격 에이전트) 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 한 다양 한 배포 시나리오를 지원 하도록 Windows 서버를 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-171">This tutorial describes how to configure Windows servers to support various deployment scenarios, including remote web package deployment using the Web Deployment Agent Service (the remote agent) or the Web Deploy Handler and remote database deployment.</span></span> <span data-ttu-id="ba137-172">사용자 고유의 환경에 대 한 적절 한 배포 방법 선택에 지침을 제공 하 고 웹 팜 프레임 워크 (WFF)를 사용 하 여 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-172">It provides guidance on choosing the appropriate deployment method for your own environment, and it describes how to use the Web Farm Framework (WFF) to replicate deployed web applications across all the web servers in a server farm.</span></span>
- <span data-ttu-id="ba137-173">[웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-173">[Configuring Team Foundation Server for Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span> <span data-ttu-id="ba137-174">이 자습서에서는 수동으로 트리거된 배포 특정 빌드의 및 CI 프로세스의 일부로 자동화 된 배포를 포함 하 여 다양 한 배포 시나리오를 지원 하도록 TFS를 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-174">This tutorial describes how to configure TFS to support various deployment scenarios, including automated deployment as part of a CI process and manually triggered deployments of specific builds.</span></span>
- <span data-ttu-id="ba137-175">[고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba137-175">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="ba137-176">이 자습서에서는 사용자 지정 된 여러 환경에 대 한 데이터베이스 배포, 배포에서 파일 및 폴더 제외 하 고, 배포 프로세스 중 웹 응용 프로그램을 오프 라인 등 다양 한 고급 배포 작업을 수행 하는 방법 설명 .</span><span class="sxs-lookup"><span data-stu-id="ba137-176">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ba137-177">다음</span><span class="sxs-lookup"><span data-stu-id="ba137-177">Next</span></span>](the-contact-manager-solution.md)