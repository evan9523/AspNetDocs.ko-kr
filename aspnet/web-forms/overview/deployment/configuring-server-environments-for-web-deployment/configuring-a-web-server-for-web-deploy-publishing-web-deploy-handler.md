---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: 웹 배포 게시용 웹 서버 구성(웹 배포 처리기)
author: jrjlee
description: 이 항목에서는 iis 웹 배포를 사용 하 여 웹 게시 및 배포를 지원 하도록 인터넷 정보 서비스 (IIS) 웹 서버를 구성 하는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: af46b5a74309fbae4b5db072363e71d965445f9a
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609687"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a><span data-ttu-id="ee975-103">웹 배포 게시용 웹 서버 구성(웹 배포 처리기)</span><span class="sxs-lookup"><span data-stu-id="ee975-103">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>

[<span data-ttu-id="ee975-104">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="ee975-104">PDF Download</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="ee975-105">이 항목에서는 iis 웹 배포 처리기를 사용 하 여 웹 게시 및 배포를 지원 하도록 인터넷 정보 서비스 (IIS) 웹 서버를 구성 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-105">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deploy Handler.</span></span>
> 
> <span data-ttu-id="ee975-106">웹 배포 2.0 이상에서 작업 하는 경우 응용 프로그램 또는 사이트를 웹 서버로 가져오는 데 사용할 수 있는 세 가지 주요 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-106">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="ee975-107">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-107">You can:</span></span>
> 
> - <span data-ttu-id="ee975-108">*웹 배포 원격 에이전트 서비스*를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-108">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="ee975-109">이 방법을 사용 하려면 웹 서버를 구성 해야 하지만 서버에 모든 항목을 배포 하려면 로컬 서버 관리자의 자격 증명을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-109">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="ee975-110">*웹 배포 처리기*를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-110">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="ee975-111">이 방법은 훨씬 복잡 하며 웹 서버를 설정 하는 데 더 많은 초기 노력이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-111">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="ee975-112">그러나이 방법을 사용 하면 관리자가 아닌 사용자가 배포를 수행할 수 있도록 IIS를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-112">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="ee975-113">웹 배포 처리기는 IIS 버전 7 이상 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-113">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="ee975-114">*오프 라인 배포*를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-114">Use *offline deployment*.</span></span> <span data-ttu-id="ee975-115">이 방법을 사용 하려면 웹 서버를 최소한으로 구성 해야 하지만 서버 관리자는 웹 패키지를 서버에 수동으로 복사 하 여 IIS 관리자를 통해 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-115">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="ee975-116">이러한 접근 방식의 주요 기능, 장점 및 단점에 대 한 자세한 내용은 [웹 배포에 대 한 올바른 접근 방법 선택](choosing-the-right-approach-to-web-deployment.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ee975-116">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

<span data-ttu-id="ee975-117">예, 관리자가 아닌 사용자가 특정 IIS 웹 사이트에 콘텐츠를 배포할 수 있도록 허용 하려면 예를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-117">Yes, if you want to allow non-administrator users to deploy content to specific IIS websites.</span></span> <span data-ttu-id="ee975-118">이 방법은 다음과 같은 시나리오에서 유용한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-118">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="ee975-119">스테이징 또는 프로덕션 환경-원격 배포를 트리거하는 개인 또는 서비스 계정이 서버 관리자의 자격 증명에 액세스할 가능성이 거의 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-119">Staging or production environments, where the person or service account that triggers the remote deployment is unlikely to have access to the credentials of a server administrator.</span></span>
- <span data-ttu-id="ee975-120">호스팅된 환경-원격 사용자에 게 웹 서버에 대 한 모든 권한을 부여 하지 않고 웹 사이트를 업데이트 하는 기능을 제공 하려고 합니다 (또는 다른 사용자의 웹 사이트에 대 한 액세스).</span><span class="sxs-lookup"><span data-stu-id="ee975-120">Hosted environments, where you want to give remote users the ability to update their websites without giving them full control of your web servers (or access to anyone else's websites).</span></span>

<span data-ttu-id="ee975-121">개발 또는 테스트 시나리오에서 또는 소규모 조직에서 서버 관리자 자격 증명을 사용 하 여 콘텐츠를 배포 하는 것은 contentious 적습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-121">In development or test scenarios, or in smaller organizations, deploying content using server administrator credentials is often less contentious.</span></span> <span data-ttu-id="ee975-122">이러한 시나리오에서는 [웹 배포 원격 에이전트 서비스](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) 를 사용 하 여 배포를 지원 하도록 웹 서버를 구성 하는 것이 더 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-122">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Remote Agent Service](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) offers a more straightforward approach.</span></span>

## <a name="task-overview"></a><span data-ttu-id="ee975-123">작업 개요</span><span class="sxs-lookup"><span data-stu-id="ee975-123">Task Overview</span></span>

<span data-ttu-id="ee975-124">웹 배포 처리기 방법을 사용 하 여 원격 컴퓨터에서 웹 패키지를 수락 하 고 배포 하도록 웹 서버를 구성 하려면 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-124">To configure the web server to accept and deploy web packages from a remote computer using the Web Deploy Handler approach, you'll need to:</span></span>

- <span data-ttu-id="ee975-125">배포를 수행 하는 데 사용할 자격 증명을 가진 도메인 사용자 계정 (관리자가 아닌 사용자)을 만들거나 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-125">Create, or choose, a domain user account (the "non-administrator user") whose credentials you'll use to perform deployments.</span></span>
- <span data-ttu-id="ee975-126">웹 관리 서비스 및 기본 인증 모듈을 포함 하 여 IIS 7.5를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-126">Install IIS 7.5, including the Web Management Service and the Basic Authentication module.</span></span>
- <span data-ttu-id="ee975-127">웹 배포 2.1 이상 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-127">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="ee975-128">원격 연결을 허용 하도록 웹 관리 서비스를 구성 하 고 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-128">Configure the Web Management Service to allow remote connections, and start the service.</span></span>
- <span data-ttu-id="ee975-129">배포 된 콘텐츠를 호스팅하는 IIS 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-129">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="ee975-130">IIS 관리자에서 웹 사이트에 대 한 관리자가 아닌 사용자 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-130">Grant your non-administrator user permissions on your website in IIS Manager.</span></span>
- <span data-ttu-id="ee975-131">웹 관리 서비스 위임 규칙에서 관리자가 아닌 사용자 계정을 사용 하 여 웹 사이트 콘텐츠를 추가 및 변경 하도록 서비스를 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-131">Ensure that the Web Management Service delegation rules permit the service to add and change website content using your non-administrator user account.</span></span>
- <span data-ttu-id="ee975-132">포트 8172에서 들어오는 연결을 허용 하도록 방화벽을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-132">Configure any firewalls to allow incoming connections on port 8172.</span></span>

<span data-ttu-id="ee975-133">이러한 솔루션을 특별히 호스트 하려면 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-133">To host the ContactManager sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="ee975-134">.NET Framework 4.0을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-134">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="ee975-135">ASP.NET MVC 3을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-135">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="ee975-136">이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-136">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="ee975-137">이 항목의 작업 및 연습에서는 Windows Server 2016를 실행 하는 클린 서버 빌드를 시작 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-137">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2016.</span></span> <span data-ttu-id="ee975-138">계속 하기 전에 다음을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ee975-138">Before you continue, ensure that:</span></span>

- <span data-ttu-id="ee975-139">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ee975-139">Windows Server 2016</span></span>
- <span data-ttu-id="ee975-140">서버가 도메인에 가입 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-140">The server is domain-joined.</span></span>
- <span data-ttu-id="ee975-141">서버에 고정 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-141">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="ee975-142">컴퓨터를 도메인에 가입 하는 방법에 대 한 자세한 내용은 [도메인에 컴퓨터 가입 및 로그온](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ee975-142">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="ee975-143">고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 [고정 Ip 주소 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ee975-143">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="ee975-144">제품 및 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="ee975-144">Install Products and Components</span></span>

<span data-ttu-id="ee975-145">이 섹션에서는 웹 서버에 필요한 제품 및 구성 요소를 설치 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-145">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="ee975-146">시작 하기 전에 Windows 업데이트를 실행 하 여 서버가 최신 상태 인지 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-146">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="ee975-147">이 경우 다음 항목을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-147">In this case, you need to install these things:</span></span>

- <span data-ttu-id="ee975-148">**IIS 7 권장 구성**.</span><span class="sxs-lookup"><span data-stu-id="ee975-148">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="ee975-149">웹 서버에서 **웹 서버 (iis)** 역할을 사용 하도록 설정 하 고 ASP.NET 응용 프로그램을 호스트 하기 위해 필요한 iis 모듈 및 구성 요소 집합을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-149">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="ee975-150">**IIS: 관리 서비스**입니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-150">**IIS: Management Service**.</span></span> <span data-ttu-id="ee975-151">이렇게 하면 IIS의 WMSvc (웹 관리 서비스)가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-151">This installs the Web Management Service (WMSvc) in IIS.</span></span> <span data-ttu-id="ee975-152">이 서비스는 IIS 웹 사이트의 원격 관리를 사용 하도록 설정 하 고 웹 배포 처리기 끝점을 클라이언트에 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-152">This service enables remote management of IIS websites and exposes the Web Deploy Handler endpoint to clients.</span></span>
- <span data-ttu-id="ee975-153">**IIS: 기본 인증**.</span><span class="sxs-lookup"><span data-stu-id="ee975-153">**IIS: Basic Authentication**.</span></span> <span data-ttu-id="ee975-154">이렇게 하면 IIS 기본 인증 모듈이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-154">This installs the IIS Basic Authentication module.</span></span> <span data-ttu-id="ee975-155">그러면 WMSvc (웹 관리 서비스)가 제공 하는 자격 증명을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-155">This lets the Web Management Service (WMSvc) authenticate the credentials you provide.</span></span>
- <span data-ttu-id="ee975-156">**웹 배포 도구 2.1**이상.</span><span class="sxs-lookup"><span data-stu-id="ee975-156">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="ee975-157">그러면 웹 배포 (및 해당 기본 실행 파일 MSDeploy.exe)가 서버에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-157">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="ee975-158">이 프로세스의 일부로 웹 배포 처리기를 설치 하 고 웹 관리 서비스와 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-158">As part of this process, it installs the Web Deploy Handler and integrates it with the Web Management Service.</span></span>
- <span data-ttu-id="ee975-159">**.NET Framework 4.0**.</span><span class="sxs-lookup"><span data-stu-id="ee975-159">**.NET Framework 4.0**.</span></span> <span data-ttu-id="ee975-160">이는이 버전의 .NET Framework에서 빌드된 응용 프로그램을 실행 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-160">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="ee975-161">**ASP.NET MVC 3**.</span><span class="sxs-lookup"><span data-stu-id="ee975-161">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="ee975-162">그러면 MVC 3 응용 프로그램을 실행 하는 데 필요한 어셈블리가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-162">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="ee975-163">이 연습에서는 웹 플랫폼 설치 관리자를 사용 하 여 다양 한 구성 요소를 설치 하 고 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-163">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="ee975-164">웹 플랫폼 설치 관리자를 사용할 필요는 없지만 종속성을 자동으로 감지 하 고 항상 최신 제품 버전을 확보 하 여 설치 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-164">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="ee975-165">자세한 내용은 [Microsoft 웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ee975-165">For more information, see [Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="ee975-166">**필요한 제품 및 구성 요소를 설치 하려면**</span><span class="sxs-lookup"><span data-stu-id="ee975-166">**To install the required products and components**</span></span>

1. <span data-ttu-id="ee975-167">[웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)를 다운로드 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-167">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="ee975-168">설치가 완료 되 면 웹 플랫폼 설치 관리자가 자동으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-168">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ee975-169">이제 언제 든 지 **시작** 메뉴에서 웹 플랫폼 설치 관리자를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-169">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="ee975-170">이렇게 하려면 **시작** 메뉴에서 **모든 프로그램**을 클릭 한 다음 **Microsoft 웹 플랫폼 설치 관리자**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-170">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="ee975-171">**웹 플랫폼 설치 관리자** 창의 위쪽에서 **제품**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-171">At the top of the **Web Platform Installer** window, click **Products**.</span></span>
4. <span data-ttu-id="ee975-172">창의 왼쪽에 있는 탐색 창에서 **프레임 워크**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-172">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="ee975-173">**Microsoft .NET Framework 4** 행에서 .NET Framework이 아직 설치 되지 않은 경우 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-173">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ee975-174">Windows 업데이트를 통해 .NET Framework 4.0를 이미 설치 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-174">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="ee975-175">제품 또는 구성 요소가 이미 설치 되어 있는 경우 웹 플랫폼 설치 관리자는 **추가** 단추를 **설치**된 텍스트로 바꿔이를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-175">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. <span data-ttu-id="ee975-176">**ASP.NET MVC 3 (Visual Studio 2010)** 행에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-176">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="ee975-177">탐색 창에서 **서버**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-177">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="ee975-178">**IIS 7 권장 구성** 행에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-178">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="ee975-179">**웹 배포 도구 2.1** 행에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-179">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="ee975-180">**IIS: 기본 인증** 행에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-180">In the **IIS: Basic Authentication** row, click **Add**.</span></span>
11. <span data-ttu-id="ee975-181">**IIS: Management Service** 행에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-181">In the **IIS: Management Service** row, click **Add**.</span></span>
12. <span data-ttu-id="ee975-182">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-182">Click **Install**.</span></span> <span data-ttu-id="ee975-183">웹 플랫폼 설치 관리자는 설치&#x2014;연결 된 종속성과 함께&#x2014;제품 목록과 사용 조건에 동의 하 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-183">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. <span data-ttu-id="ee975-184">사용 약관을 검토 하 고 약관에 동의 하는 경우 동의 **함**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-184">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
14. <span data-ttu-id="ee975-185">설치가 완료 되 면 **마침**을 클릭 하 고 **웹 플랫폼 설치 관리자** 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-185">When the installation is complete, click **Finish**, and then close the **Web Platform Installer** window.</span></span>

<span data-ttu-id="ee975-186">IIS를 설치 하기 전에 .NET Framework 4.0를 설치한 경우 ASP.NET의 최신 버전을 IIS에 등록 하려면 [ASP.NET IIS 등록 도구](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnetregiis.exe)를 실행 해야 합니다 \_ .</span><span class="sxs-lookup"><span data-stu-id="ee975-186">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="ee975-187">이렇게 하지 않으면 IIS에서 문제 없이 정적 콘텐츠 (HTML 파일)를 제공 하는 것을 알 수 있지만 ASP.NET 콘텐츠를 검색 하려고 할 때에는 **HTTP 오류 404.0 – 찾을** 수 없음이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-187">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="ee975-188">다음 절차를 사용 하 여 ASP.NET 4.0이 등록 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-188">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="ee975-189">**IIS에 ASP.NET 4.0를 등록 하려면**</span><span class="sxs-lookup"><span data-stu-id="ee975-189">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="ee975-190">**시작**을 클릭 한 다음 **명령 프롬프트**를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-190">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="ee975-191">검색 결과에서 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-191">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="ee975-192">명령 프롬프트 창에서 **\ v 4.0.30319** 디렉터리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-192">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="ee975-193">다음 명령을 입력 하 고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-193">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. <span data-ttu-id="ee975-194">어느 시점에서 든 64 비트 웹 응용 프로그램을 호스트 하려는 경우 ASP.NET의 64 비트 버전을 IIS에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-194">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="ee975-195">이렇게 하려면 명령 프롬프트 창에서 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 디렉터리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-195">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="ee975-196">다음 명령을 입력 하 고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-196">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

<span data-ttu-id="ee975-197">지금까지 Windows 업데이트를 사용 하 여 설치한 새 제품 및 구성 요소에 대 한 사용 가능한 업데이트를 다운로드 하 고 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-197">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-web-management-service"></a><span data-ttu-id="ee975-198">웹 관리 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="ee975-198">Configure the Web Management Service</span></span>

<span data-ttu-id="ee975-199">필요한 모든 항목을 설치 했으므로 다음 단계는 IIS에서 웹 관리 서비스를 구성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-199">Now that you've installed everything you need, the next step is to configure the Web Management Service in IIS.</span></span> <span data-ttu-id="ee975-200">개략적인 수준에서 다음 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-200">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="ee975-201">서버 수준에서 기본 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-201">Enable basic authentication at the server level.</span></span>
- <span data-ttu-id="ee975-202">원격 연결을 허용 하도록 웹 관리 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-202">Configure the Web Management Service to accept remote connections.</span></span>
- <span data-ttu-id="ee975-203">웹 관리 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-203">Start the Web Management Service.</span></span>
- <span data-ttu-id="ee975-204">필요한 웹 관리 서비스 위임 규칙이 준비 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-204">Check that the required Web Management Service delegation rules are in place.</span></span>

<span data-ttu-id="ee975-205">**웹 관리 서비스를 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="ee975-205">**To configure the Web Management Service**</span></span>

1. <span data-ttu-id="ee975-206">**시작** 메뉴에서 **관리 도구**를 가리킨 다음 **인터넷 정보 서비스 (IIS) 관리자**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-206">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="ee975-207">IIS 관리자의 **연결** 창에서 서버 노드 (예: **STAGEWEB1**)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-207">In IIS Manager, in the **Connections** pane, click the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. <span data-ttu-id="ee975-208">가운데 창의 **IIS**에서 **인증**을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-208">In the center pane, under **IIS**, double-click **Authentication**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. <span data-ttu-id="ee975-209">**기본 인증**을 마우스 오른쪽 단추로 클릭 한 다음 **사용**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-209">Right-click **Basic Authentication**, and then click **Enable**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. <span data-ttu-id="ee975-210">**연결** 창에서 서버 노드를 다시 클릭 하 여 최상위 수준 설정으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-210">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
6. <span data-ttu-id="ee975-211">가운데 창의 **관리**에서 **관리 서비스**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-211">In the center pane, under **Management**, double-click **Management Service**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. <span data-ttu-id="ee975-212">가운데 창에서 **원격 연결 사용**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-212">In the center pane, select **Enable remote connections**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ee975-213">웹 관리 서비스가 이미 실행 중인 경우에는 먼저 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-213">If the Web Management Service is already running, you'll need to stop it first.</span></span>
8. <span data-ttu-id="ee975-214">**작업** 창에서 **시작** 을 클릭 하 여 웹 관리 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-214">In the **Actions** pane, click **Start** to start the Web Management Service.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. <span data-ttu-id="ee975-215">설정을 저장할 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-215">If you're prompted to save your settings, click **Yes**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ee975-216">서비스가 자동으로 시작 되도록 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-216">You may also want to configure the service to start automatically.</span></span> <span data-ttu-id="ee975-217">이렇게 하려면 서비스 콘솔을 열고 **웹 관리 서비스**를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-217">To do this, open the Services console, right-click **Web Management Service**, and then click **Properties**.</span></span> <span data-ttu-id="ee975-218">**시작 유형** 드롭다운 목록에서 **자동**을 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-218">In the **Startup type** dropdown list, select **Automatic**, and then click **OK**.</span></span>
10. <span data-ttu-id="ee975-219">**연결** 창에서 서버 노드를 다시 클릭 하 여 최상위 수준 설정으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-219">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
11. <span data-ttu-id="ee975-220">가운데 창의 **관리**에서 **관리 서비스 위임**을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-220">In the center pane, under **Management**, double-click **Management Service Delegation**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. <span data-ttu-id="ee975-221">가운데 창에 규칙 집합이 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-221">Verify that the center pane contains a set of rules.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    <span data-ttu-id="ee975-222">이러한 규칙을 통해 권한 있는 웹 관리 서비스 사용자는 다양 한 웹 배포 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-222">These rules allow authorized Web Management Service users to use various Web Deploy providers.</span></span> <span data-ttu-id="ee975-223">예를 들어 웹 배포 처리기를 통해 IIS에 웹 응용 프로그램 및 콘텐츠를 배포 하려면 모든 인증 된 웹 관리 서비스 사용자가 **Contentpath** 및 **iisApp** 공급자 (스크린샷에서 볼 수 있는 마지막 규칙)를 사용 하도록 허용 하는 위임 규칙이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-223">For example, to deploy web applications and content to IIS through the Web Deploy Handler, there must be a delegation rule that allows all authenticated Web Management Service users to use the **contentPath** and **iisApp** providers (the last rule that you can see in the screenshot).</span></span>

    <span data-ttu-id="ee975-224">이 항목에 설명 된 순서 대로 제품 및 구성 요소를 설치한 경우 최신 버전의 웹 배포은 웹 관리 서비스에 필요한 모든 위임 규칙을 자동으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-224">If you installed products and components in the order described in this topic, the latest version of Web Deploy should automatically add all the required delegation rules to the Web Management Service.</span></span> <span data-ttu-id="ee975-225">관리 서비스 위임 페이지에 규칙이 표시 되지 않는 경우 직접 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-225">If the Management Service Delegation page does not show any rules, you'll need to create them yourself.</span></span> <span data-ttu-id="ee975-226">이 작업을 수행 하는 방법에 대 한 지침은 [웹 배포 처리기 구성](https://go.microsoft.com/?linkid=9805124)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ee975-226">For instructions on how to do this, see [Configure the Web Deployment Handler](https://go.microsoft.com/?linkid=9805124).</span></span>
13. <span data-ttu-id="ee975-227">**연결** 창에서 서버 노드를 다시 클릭 하 여 최상위 수준 설정으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-227">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>

## <a name="create-and-configure-an-iis-website"></a><span data-ttu-id="ee975-228">IIS 웹 사이트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="ee975-228">Create and Configure an IIS Website</span></span>

<span data-ttu-id="ee975-229">웹 콘텐츠를 서버에 배포 하려면 먼저 콘텐츠를 호스팅하는 IIS 웹 사이트를 만들고 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-229">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="ee975-230">웹 배포는 기존 IIS 웹 사이트에만 웹 패키지를 배포할 수 있습니다. 웹 사이트를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-230">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="ee975-231">또한 관리자가 아닌 계정이 원격으로 콘텐츠를 배포 하도록 허용 하려면 약간의 추가 구성을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-231">You also need to do a little extra configuration to allow your non-administrator account to deploy content remotely.</span></span> <span data-ttu-id="ee975-232">개략적인 수준에서 다음 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-232">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="ee975-233">콘텐츠를 호스트할 파일 시스템에 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-233">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="ee975-234">콘텐츠를 제공 하는 IIS 웹 사이트를 만들고 로컬 폴더에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-234">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="ee975-235">로컬 폴더의 응용 프로그램 풀 id에 대 한 읽기 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-235">Grant read permissions to the application pool identity on the local folder.</span></span>
- <span data-ttu-id="ee975-236">웹 응용 프로그램을 배포 하는 도메인 계정에 필요한 IIS 사용 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-236">Grant the necessary IIS permissions to the domain account that will deploy your web application.</span></span>

<span data-ttu-id="ee975-237">IIS의 기본 웹 사이트에 콘텐츠를 배포 하는 것은 아무 작업도 수행 하지 않지만 테스트 또는 데모 시나리오 이외의 다른 항목에는이 방법을 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-237">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="ee975-238">프로덕션 환경을 시뮬레이트하려면 응용 프로그램의 요구 사항과 관련 된 설정을 사용 하 여 새 IIS 웹 사이트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-238">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="ee975-239">**IIS 웹 사이트를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="ee975-239">**To create an IIS website**</span></span>

1. <span data-ttu-id="ee975-240">로컬 파일 시스템에서 콘텐츠를 저장할 폴더를 만듭니다 (예: **C:\demosite**).</span><span class="sxs-lookup"><span data-stu-id="ee975-240">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="ee975-241">**시작** 메뉴에서 **관리 도구**를 가리킨 다음 **인터넷 정보 서비스 (IIS) 관리자**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-241">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="ee975-242">IIS 관리자의 **연결** 창에서 서버 노드를 확장 합니다 (예: **STAGEWEB1**).</span><span class="sxs-lookup"><span data-stu-id="ee975-242">In IIS Manager, in the **Connections** pane, expand the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. <span data-ttu-id="ee975-243">**사이트** 노드를 마우스 오른쪽 단추로 클릭 한 다음 **웹 사이트 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-243">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="ee975-244">**사이트 이름** 상자에 IIS 웹 사이트의 이름을 입력 합니다 (예: **demosite**).</span><span class="sxs-lookup"><span data-stu-id="ee975-244">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="ee975-245">**실제 경로** 상자에 로컬 폴더 경로 (예: **c:\demosite**)를 입력 하거나 해당 경로를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-245">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="ee975-246">**포트** 상자에 웹 사이트를 호스트 하려는 포트 번호 (예: **85**)를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-246">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ee975-247">표준 포트 번호는 HTTP의 경우 80이 고 HTTPS의 경우 443입니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-247">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="ee975-248">그러나 포트 80에서이 웹 사이트를 호스팅하는 경우 사이트에 액세스 하려면 먼저 기본 웹 사이트를 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-248">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="ee975-249">웹 사이트에 대 한 DNS (Domain Name System) 레코드를 구성 하려는 경우가 아니면 **호스트 이름** 상자를 비워 둡니다. 그런 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-249">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > <span data-ttu-id="ee975-250">프로덕션 환경에서는 포트 80에서 웹 사이트를 호스트 하 고 일치 하는 DNS 레코드와 함께 호스트 헤더를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-250">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="ee975-251">IIS 7에서 호스트 헤더를 구성 하는 방법에 대 한 자세한 내용은 [웹 사이트의 호스트 헤더 구성 (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx)을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ee975-251">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="ee975-252">Windows Server의 DNS 서버 역할에 대 한 자세한 내용은 [Dns 서버 개요](https://technet.microsoft.com/library/cc770392.aspx) 및 [dns 서버](https://technet.microsoft.com/windowsserver/dd448607)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ee975-252">For more information on the DNS Server role in Windows Server, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="ee975-253">**작업** 창의 **사이트 편집**에서 **바인딩**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-253">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="ee975-254">**사이트 바인딩** 대화 상자에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-254">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. <span data-ttu-id="ee975-255">**사이트 바인딩 추가** 대화 상자에서 기존 사이트 구성과 일치 하는 **IP 주소** 및 **포트** 를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-255">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="ee975-256">**호스트 이름** 상자에 웹 서버의 이름 (예: **STAGEWEB1**)을 입력 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-256">In the **Host name** box, type the name of your web server (for example, **STAGEWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > <span data-ttu-id="ee975-257">첫 번째 사이트 바인딩을 사용 하면 IP 주소와 포트 또는를 사용 하 여 로컬에서 사이트에 액세스할 수 있습니다 `http://localhost:85` .</span><span class="sxs-lookup"><span data-stu-id="ee975-257">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="ee975-258">두 번째 사이트 바인딩을 사용 하면 컴퓨터 이름 (예:)을 사용 하 여 도메인에 있는 다른 컴퓨터에서 사이트에 액세스할 수 있습니다 http://stageweb1:85) .</span><span class="sxs-lookup"><span data-stu-id="ee975-258">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://stageweb1:85).</span></span>
13. <span data-ttu-id="ee975-259">**사이트 바인딩** 대화 상자에서 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-259">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="ee975-260">**연결** 창에서 **애플리케이션 풀**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-260">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="ee975-261">**응용 프로그램 풀** 창에서 응용 프로그램 풀의 이름을 마우스 오른쪽 단추로 클릭 한 다음 **기본 설정**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-261">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="ee975-262">기본적으로 응용 프로그램 풀의 이름은 웹 사이트의 이름 (예: **Demosite**)과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-262">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="ee975-263">**.NET clr 버전** 목록에서 **.net clr v 4.0.30319**를 선택한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-263">In the **.NET CLR version** list, select **.NET CLR v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

    > [!NOTE]
    > <span data-ttu-id="ee975-264">샘플 솔루션에는 .NET Framework 4.0가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-264">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="ee975-265">이는 일반적으로 웹 배포 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-265">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="ee975-266">웹 사이트가 콘텐츠를 제공 하기 위해 응용 프로그램 풀 id에 콘텐츠를 저장 하는 로컬 폴더에 대 한 읽기 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-266">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="ee975-267">IIS 7.5에서 응용 프로그램 풀은 기본적으로 고유한 응용 프로그램 풀 id로 실행 됩니다 (응용 프로그램 풀은 일반적으로 Network Service 계정을 사용 하 여 실행 되는 이전 버전의 IIS와 대조).</span><span class="sxs-lookup"><span data-stu-id="ee975-267">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="ee975-268">응용 프로그램 풀 id는 실제 사용자 계정이 아니므로 대신 사용자 또는&#x2014;그룹 목록에 표시 되지 않습니다. 대신 응용 프로그램 풀이 시작 될 때 동적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-268">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="ee975-269">각 응용 프로그램 풀 id는 로컬 **IIS \_ iusrs** 보안 그룹에 숨겨진 항목으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-269">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="ee975-270">파일이 나 폴더에서 응용 프로그램 풀 id에 대 한 사용 권한을 부여 하려면 다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-270">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="ee975-271">Iis **AppPool \( 응용 프로그램 풀 이름을** 사용 하 여 응용 프로그램 풀 id에 직접 사용 권한을 할당 합니다 (예: **iis AppPool\DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="ee975-271">Assign permissions to the application pool identity directly, using the format **IIS AppPool\(application pool name)** (for example, **IIS AppPool\DemoSite**).</span></span>
- <span data-ttu-id="ee975-272">**IIS \_ iusrs** 그룹에 사용 권한을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-272">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="ee975-273">가장 일반적인 방법은 로컬 **IIS \_ iusrs** 그룹에 사용 권한을 할당 하는 것입니다 .이 방법을 사용 하면 파일 시스템 권한을 다시 구성 하지 않고 응용 프로그램 풀을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-273">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="ee975-274">다음 절차에서는이 그룹 기반 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-274">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="ee975-275">IIS 7.5의 응용 프로그램 풀 id에 대 한 자세한 내용은 [응용 프로그램 풀 id](https://go.microsoft.com/?linkid=9805123)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ee975-275">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="ee975-276">**IIS 웹 사이트에 대 한 폴더 사용 권한을 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="ee975-276">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="ee975-277">Windows 탐색기에서 로컬 폴더의 위치로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-277">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="ee975-278">폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-278">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="ee975-279">**Security** 탭에서 **Edit**을 클릭한 다음 **Add**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-279">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="ee975-280">**위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-280">Click **Locations**.</span></span> <span data-ttu-id="ee975-281">**위치** 대화 상자에서 로컬 서버를 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-281">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. <span data-ttu-id="ee975-282">**사용자 또는 그룹 선택** 대화 상자에서 **IIS \_ iusrs**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-282">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="ee975-283">**에 대 한 사용 권한 (폴더 이름)** 대화 상자에서 새 그룹에 **읽기 &amp; 실행**, **폴더 내용**보기 및 기본적으로 **읽기** 권한이 할당 된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-283">In the **Permissions for (folder name)** dialog box, notice that the new group has been assigned the **Read &amp; execute**, **List folder contents**, and **Read** permissions by default.</span></span> <span data-ttu-id="ee975-284">이를 변경 되지 않은 상태로 두고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-284">Leave this unchanged and click **OK**.</span></span>
7. <span data-ttu-id="ee975-285">**확인** 을 클릭 하 여 **(폴더 이름) 속성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-285">Click **OK** to close the **(folder name) Properties** dialog box.</span></span>

<span data-ttu-id="ee975-286">최종 작업으로, 콘텐츠를 배포 하는 데 사용할 자격 증명을 가진 비관리자 사용자에 게 적절 한 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-286">As a final task, you must grant the appropriate permissions to the non-administrator user whose credentials you'll use to deploy content.</span></span> <span data-ttu-id="ee975-287">이 사용자는 웹 사이트에 원격으로 콘텐츠를 배포 하기 위한 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-287">This user requires the permissions to deploy content remotely to your website.</span></span>

<span data-ttu-id="ee975-288">**비관리자 도메인 사용자에 대 한 IIS 웹 사이트 권한을 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="ee975-288">**To configure IIS website permissions for a non-administrator domain user**</span></span>

1. <span data-ttu-id="ee975-289">IIS 관리자의 **연결** 창에서 웹 사이트 노드 (예: **demosite**)를 마우스 오른쪽 단추로 클릭 하 고 **배포**를 가리킨 다음 **웹 배포 게시 구성**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-289">In IIS Manager, in the **Connections** pane, right-click your website node (for example, **DemoSite**), point to **Deploy**, and then click **Configure Web Deploy Publishing**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. <span data-ttu-id="ee975-290">**웹 배포 게시 구성** 대화 상자에서 **게시 권한을 부여할 사용자 선택** 목록 오른쪽에 있는 줄임표 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-290">In the **Configure Web Deploy Publishing** dialog box, to the right of the **Select a user to give publishing permissions** list, click the ellipsis button.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. <span data-ttu-id="ee975-291">**사용자 허용** 대화 상자에서 콘텐츠를 배포 하는 데 사용할 계정의 도메인 및 사용자 이름을 입력 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-291">In the **Allow User** dialog box, type the domain and user name of the account you want to use to deploy content, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. <span data-ttu-id="ee975-292">**웹 배포 게시 구성** 대화 상자에서 **설치**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-292">In the **Configure Web Deploy Publishing** dialog box, click **Setup**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > <span data-ttu-id="ee975-293">이 작업을 수행 하면 두 가지 키 함수가 한 단계로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-293">This operation performs two key functions in one step.</span></span> <span data-ttu-id="ee975-294">먼저 이전 섹션에서 검사 한 위임 규칙에 따라 웹 관리 서비스를 통해 원격으로 웹 사이트를 수정할 수 있는 권한을 사용자에 게 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-294">First, it grants the user permission to modify the website remotely through the Web Management Service, according to the delegation rules you examined in the previous section.</span></span> <span data-ttu-id="ee975-295">둘째, 사용자에 게 웹 사이트의 원본 폴더에 대 한 모든 권한을 부여 하 여 사용자가 웹 사이트 콘텐츠에 대 한 권한을 추가, 수정 및 설정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-295">Second, it grants the user full control of the source folder for the website, which allows the user to add, modify, and set permissions on the website content.</span></span>
5. <span data-ttu-id="ee975-296">**웹 배포 게시 구성** 대화 상자에서 **닫기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-296">In the **Configure Web Deploy Publishing** dialog box, click **Close**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="ee975-297">방화벽 예외 구성</span><span class="sxs-lookup"><span data-stu-id="ee975-297">Configure Firewall Exceptions</span></span>

<span data-ttu-id="ee975-298">기본적으로 IIS 웹 관리 서비스는 TCP 포트 8172에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-298">By default, the IIS Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="ee975-299">웹 서버에서 Windows 방화벽을 사용 하는 경우 포트 8172에서 TCP 트래픽을 허용 하는 새 인바운드 규칙을 만들어야 합니다. 모든 아웃 바운드 트래픽은 기본적으로 Windows 방화벽에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-299">If Windows Firewall is enabled on your web server, you'll need to create a new inbound rule to allow TCP traffic on port 8172 (all outbound traffic is permitted by default in Windows Firewall).</span></span> <span data-ttu-id="ee975-300">타사 방화벽을 사용 하는 경우 트래픽을 허용 하는 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-300">If you use a third-party firewall, you'll need to create rules to allow traffic.</span></span>

| <span data-ttu-id="ee975-301">Direction</span><span class="sxs-lookup"><span data-stu-id="ee975-301">Direction</span></span> | <span data-ttu-id="ee975-302">보낸 포트</span><span class="sxs-lookup"><span data-stu-id="ee975-302">From Port</span></span> | <span data-ttu-id="ee975-303">포트에</span><span class="sxs-lookup"><span data-stu-id="ee975-303">To Port</span></span> | <span data-ttu-id="ee975-304">포트 유형</span><span class="sxs-lookup"><span data-stu-id="ee975-304">Port Type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ee975-305">인바운드</span><span class="sxs-lookup"><span data-stu-id="ee975-305">Inbound</span></span> | <span data-ttu-id="ee975-306">모두</span><span class="sxs-lookup"><span data-stu-id="ee975-306">Any</span></span> | <span data-ttu-id="ee975-307">8172</span><span class="sxs-lookup"><span data-stu-id="ee975-307">8172</span></span> | <span data-ttu-id="ee975-308">TCP</span><span class="sxs-lookup"><span data-stu-id="ee975-308">TCP</span></span> |
| <span data-ttu-id="ee975-309">아웃바운드</span><span class="sxs-lookup"><span data-stu-id="ee975-309">Outbound</span></span> | <span data-ttu-id="ee975-310">8172</span><span class="sxs-lookup"><span data-stu-id="ee975-310">8172</span></span> | <span data-ttu-id="ee975-311">모두</span><span class="sxs-lookup"><span data-stu-id="ee975-311">Any</span></span> | <span data-ttu-id="ee975-312">TCP</span><span class="sxs-lookup"><span data-stu-id="ee975-312">TCP</span></span> |

<span data-ttu-id="ee975-313">Windows 방화벽에서 규칙을 구성 하는 방법에 대 한 자세한 내용은 [방화벽 규칙 구성](https://technet.microsoft.com/library/dd448559(WS.10).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ee975-313">For more information on configuring rules in Windows Firewall, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="ee975-314">타사 방화벽의 경우 제품 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ee975-314">For third-party firewalls, please consult your product documentation.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ee975-315">결론</span><span class="sxs-lookup"><span data-stu-id="ee975-315">Conclusion</span></span>

<span data-ttu-id="ee975-316">이제 웹 서버에서 웹 관리 서비스를 통해 웹 배포 처리기에 대 한 원격 배포를 받아들일 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-316">Your web server should now be ready to accept remote deployments to the Web Deploy Handler through the Web Management Service.</span></span> <span data-ttu-id="ee975-317">서버에 웹 응용 프로그램을 배포 하기 전에 다음과 같은 주요 사항을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ee975-317">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="ee975-318">IIS의 서버 수준에서 기본 인증을 사용 하도록 설정 했습니까?</span><span class="sxs-lookup"><span data-stu-id="ee975-318">Have you enabled basic authentication at the server level in IIS?</span></span>
- <span data-ttu-id="ee975-319">웹 관리 서비스에 대 한 원격 연결을 사용 하도록 설정 했습니까?</span><span class="sxs-lookup"><span data-stu-id="ee975-319">Have you enabled remote connections to the Web Management Service?</span></span>
- <span data-ttu-id="ee975-320">웹 관리 서비스를 시작 했습니까?</span><span class="sxs-lookup"><span data-stu-id="ee975-320">Have you started the Web Management Service?</span></span>
- <span data-ttu-id="ee975-321">관리 서비스 위임 규칙이 준비 되어 있나요?</span><span class="sxs-lookup"><span data-stu-id="ee975-321">Are there management service delegation rules in place?</span></span>
- <span data-ttu-id="ee975-322">응용 프로그램 풀 id에 웹 사이트의 원본 폴더에 대 한 읽기 권한이 있나요?</span><span class="sxs-lookup"><span data-stu-id="ee975-322">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="ee975-323">비관리자 사용자 계정에 IIS의 사이트 수준 권한이 있나요?</span><span class="sxs-lookup"><span data-stu-id="ee975-323">Does the non-administrator user account have site-level permissions in IIS?</span></span>
- <span data-ttu-id="ee975-324">방화벽이 TCP 포트 8172의 서버에 대 한 들어오는 연결을 허용 하나요?</span><span class="sxs-lookup"><span data-stu-id="ee975-324">Does your firewall allow incoming connections to the server on TCP port 8172?</span></span>

## <a name="further-reading"></a><span data-ttu-id="ee975-325">추가 정보</span><span class="sxs-lookup"><span data-stu-id="ee975-325">Further Reading</span></span>

<span data-ttu-id="ee975-326">웹 배포 처리기에 웹 패키지를 배포 하기 위해 MSBuild (사용자 지정 Microsoft Build Engine) 프로젝트 파일을 구성 하는 방법에 대 한 지침은 [대상 환경의 배포 속성 구성](configuring-deployment-properties-for-a-target-environment.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ee975-326">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Web Deploy Handler, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ee975-327">[이전](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
> [다음](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="ee975-327">[Previous](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span></span>
