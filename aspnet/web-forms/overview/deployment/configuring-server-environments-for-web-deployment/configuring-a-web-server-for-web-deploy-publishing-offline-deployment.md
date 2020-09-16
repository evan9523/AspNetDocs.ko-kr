---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
title: 웹 배포 게시용 웹 서버 구성 (오프 라인 배포) | Microsoft Docs
author: jrjlee
description: 이 항목에서는 오프 라인 웹 게시 및 배포를 지원 하도록 IIS 웹 서버를 구성 하는 방법에 대해 설명 합니다. 인터넷 정보 서비스 작업 하는 경우 (...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ba92788f-9f03-44b1-b6b2-af8413e6a35d
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
msc.type: authoredcontent
ms.openlocfilehash: ed11720e6ea00df22f58d9afd32ccce95a5d1a60
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609666"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-offline-deployment"></a><span data-ttu-id="85e98-104">웹 배포 게시용 웹 서버 구성(오프라인 배포)</span><span class="sxs-lookup"><span data-stu-id="85e98-104">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>

<span data-ttu-id="85e98-105">[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="85e98-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="85e98-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="85e98-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="85e98-107">이 항목에서는 오프 라인 웹 게시 및 배포를 지원 하도록 IIS 웹 서버를 구성 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-107">This topic describes how to configure an IIS web server to support offline web publishing and deployment.</span></span>
> 
> <span data-ttu-id="85e98-108">인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포) 2.0 이상으로 작업 하는 경우 응용 프로그램 또는 사이트를 웹 서버로 가져오는 데 사용할 수 있는 세 가지 주요 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-108">When you work with Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="85e98-109">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-109">You can:</span></span>
> 
> - <span data-ttu-id="85e98-110">*웹 배포 원격 에이전트 서비스*를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-110">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="85e98-111">이 방법을 사용 하려면 웹 서버를 구성 해야 하지만 서버에 모든 항목을 배포 하려면 로컬 서버 관리자의 자격 증명을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-111">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="85e98-112">*웹 배포 처리기*를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-112">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="85e98-113">이 방법은 훨씬 복잡 하며 웹 서버를 설정 하는 데 더 많은 초기 노력이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-113">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="85e98-114">그러나이 방법을 사용 하면 관리자가 아닌 사용자가 배포를 수행할 수 있도록 IIS를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-114">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="85e98-115">웹 배포 처리기는 IIS 버전 7 이상 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-115">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="85e98-116">*오프 라인 배포*를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-116">Use *offline deployment*.</span></span> <span data-ttu-id="85e98-117">이 방법을 사용 하려면 웹 서버를 최소한으로 구성 해야 하지만 서버 관리자는 웹 패키지를 서버에 수동으로 복사 하 여 IIS 관리자를 통해 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-117">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="85e98-118">이러한 접근 방식의 주요 기능, 장점 및 단점에 대 한 자세한 내용은 [웹 배포에 대 한 올바른 접근 방법 선택](choosing-the-right-approach-to-web-deployment.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="85e98-118">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

<span data-ttu-id="85e98-119">예, 네트워크 인프라 또는 보안 제한으로 인해 원격 배포가 허용 되지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="85e98-119">Yes, if your network infrastructure or security restrictions prevent remote deployment.</span></span> <span data-ttu-id="85e98-120">이는 인터넷 연결 환경에서 발생 하는 경우가 가장 많습니다 .이는 웹 서버가 물리적으로 또는 방화벽 및 서브넷을 통해 서버 인프라의 나머지 부분에서&#x2014;&#x2014;격리 되는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-120">This is most likely to be the case in Internet-facing production environments, where the web servers are isolated&#x2014;either physically or by firewalls and subnets&#x2014;from the rest of your server infrastructure.</span></span>

<span data-ttu-id="85e98-121">웹 응용 프로그램을 정기적으로 업데이트 하는 경우에는이 방법이 그다지 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-121">Obviously, this approach becomes less desirable if your web applications are updated on a regular basis.</span></span> <span data-ttu-id="85e98-122">인프라에서 허용 하는 경우 웹 배포 처리기 또는 웹 배포 원격 에이전트 서비스를 사용 하 여 원격 배포를 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-122">If your infrastructure allows it, you may want to consider enabling remote deployment, using either the Web Deploy Handler or the Web Deploy Remote Agent Service.</span></span>

## <a name="task-overview"></a><span data-ttu-id="85e98-123">작업 개요</span><span class="sxs-lookup"><span data-stu-id="85e98-123">Task Overview</span></span>

<span data-ttu-id="85e98-124">웹 패키지의 오프 라인 가져오기 및 배포를 지원 하도록 웹 서버를 구성 하려면 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-124">To configure the web server to support offline import and deployment of web packages, you'll need to:</span></span>

- <span data-ttu-id="85e98-125">IIS 7.5 및 IIS 7 권장 구성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-125">Install IIS 7.5 and the IIS 7 recommended configuration.</span></span>
- <span data-ttu-id="85e98-126">웹 배포 2.1 이상 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-126">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="85e98-127">배포 된 콘텐츠를 호스팅하는 IIS 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-127">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="85e98-128">웹 Deployment Agent 서비스를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-128">Disable the Web Deployment Agent Service.</span></span>

<span data-ttu-id="85e98-129">특히 샘플 솔루션을 호스트 하려면 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-129">To host the sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="85e98-130">.NET Framework 4.0을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-130">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="85e98-131">ASP.NET MVC 3을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-131">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="85e98-132">이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-132">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="85e98-133">이 항목의 작업 및 연습에서는 Windows Server 2008 r 2를 실행 하는 클린 서버 빌드를 시작 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-133">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="85e98-134">계속 하기 전에 다음을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="85e98-134">Before you continue, ensure that:</span></span>

- <span data-ttu-id="85e98-135">Windows Server 2008 R2 서비스 팩 1 및 사용 가능한 모든 업데이트가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-135">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="85e98-136">서버가 도메인에 가입 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-136">The server is domain-joined.</span></span>
- <span data-ttu-id="85e98-137">서버에 고정 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-137">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="85e98-138">컴퓨터를 도메인에 가입 하는 방법에 대 한 자세한 내용은 [도메인에 컴퓨터 가입 및 로그온](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="85e98-138">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="85e98-139">고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 [고정 Ip 주소 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="85e98-139">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="85e98-140">제품 및 구성 요소 설치</span><span class="sxs-lookup"><span data-stu-id="85e98-140">Install Products and Components</span></span>

<span data-ttu-id="85e98-141">이 섹션에서는 웹 서버에 필요한 제품 및 구성 요소를 설치 하는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-141">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="85e98-142">시작 하기 전에 Windows 업데이트를 실행 하 여 서버가 최신 상태 인지 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-142">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="85e98-143">이 경우 다음 항목을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-143">In this case, you need to install these things:</span></span>

- <span data-ttu-id="85e98-144">**IIS 7 권장 구성**.</span><span class="sxs-lookup"><span data-stu-id="85e98-144">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="85e98-145">웹 서버에서 **웹 서버 (iis)** 역할을 사용 하도록 설정 하 고 ASP.NET 응용 프로그램을 호스트 하기 위해 필요한 iis 모듈 및 구성 요소 집합을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-145">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="85e98-146">**.NET Framework 4.0**.</span><span class="sxs-lookup"><span data-stu-id="85e98-146">**.NET Framework 4.0**.</span></span> <span data-ttu-id="85e98-147">이는이 버전의 .NET Framework에서 빌드된 응용 프로그램을 실행 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-147">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="85e98-148">**웹 배포 도구 2.1**이상.</span><span class="sxs-lookup"><span data-stu-id="85e98-148">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="85e98-149">그러면 웹 배포 (및 해당 기본 실행 파일 MSDeploy.exe)가 서버에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-149">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="85e98-150">웹 배포은 IIS와 통합 되며 웹 패키지를 가져오고 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-150">Web Deploy integrates with IIS and lets you import and export web packages.</span></span>
- <span data-ttu-id="85e98-151">**ASP.NET MVC 3**.</span><span class="sxs-lookup"><span data-stu-id="85e98-151">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="85e98-152">그러면 MVC 3 응용 프로그램을 실행 하는 데 필요한 어셈블리가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-152">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="85e98-153">이 연습에서는 웹 플랫폼 설치 관리자를 사용 하 여 다양 한 구성 요소를 설치 하 고 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-153">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="85e98-154">웹 플랫폼 설치 관리자를 사용할 필요는 없지만 종속성을 자동으로 감지 하 고 항상 최신 제품 버전을 확보 하 여 설치 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-154">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="85e98-155">자세한 내용은 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/?linkid=9805118)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="85e98-155">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="85e98-156">**필요한 제품 및 구성 요소를 설치 하려면**</span><span class="sxs-lookup"><span data-stu-id="85e98-156">**To install the required products and components**</span></span>

1. <span data-ttu-id="85e98-157">[웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9805118)를 다운로드 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-157">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="85e98-158">설치가 완료 되 면 웹 플랫폼 설치 관리자가 자동으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-158">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="85e98-159">이제 언제 든 지 **시작** 메뉴에서 웹 플랫폼 설치 관리자를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-159">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="85e98-160">이렇게 하려면 **시작** 메뉴에서 **모든 프로그램**을 클릭 한 다음 **Microsoft 웹 플랫폼 설치 관리자**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-160">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="85e98-161">**웹 플랫폼 설치 관리자 3.0** 창의 위쪽에서 **제품**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-161">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="85e98-162">창의 왼쪽에 있는 탐색 창에서 **프레임 워크**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-162">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="85e98-163">**Microsoft .NET Framework 4** 행에서 .NET Framework이 아직 설치 되지 않은 경우 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-163">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="85e98-164">Windows 업데이트를 통해 .NET Framework 4.0를 이미 설치 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-164">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="85e98-165">제품 또는 구성 요소가 이미 설치 되어 있는 경우 웹 플랫폼 설치 관리자는 **추가** 단추를 **설치**된 텍스트로 바꿔이를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-165">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image1.png)
6. <span data-ttu-id="85e98-166">**ASP.NET MVC 3 (Visual Studio 2010)** 행에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-166">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="85e98-167">탐색 창에서 **서버**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-167">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="85e98-168">**IIS 7 권장 구성** 행에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-168">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="85e98-169">**웹 배포 도구 2.1** 행에서 **추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-169">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="85e98-170">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-170">Click **Install**.</span></span> <span data-ttu-id="85e98-171">웹 플랫폼 설치 관리자는 설치&#x2014;연결 된 종속성과 함께&#x2014;제품 목록과 사용 조건에 동의 하 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-171">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image2.png)
11. <span data-ttu-id="85e98-172">사용 약관을 검토 하 고 약관에 동의 하는 경우 동의 **함**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-172">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="85e98-173">설치가 완료 되 면 **마침**을 클릭 하 고 **웹 플랫폼 설치 관리자 3.0** 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-173">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="85e98-174">IIS를 설치 하기 전에 .NET Framework 4.0를 설치한 경우 ASP.NET의 최신 버전을 IIS에 등록 하려면 [ASP.NET IIS 등록 도구](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnetregiis.exe)를 실행 해야 합니다 \_ .</span><span class="sxs-lookup"><span data-stu-id="85e98-174">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="85e98-175">이렇게 하지 않으면 IIS에서 문제 없이 정적 콘텐츠 (HTML 파일)를 제공 하는 것을 알 수 있지만 ASP.NET 콘텐츠를 검색 하려고 할 때에는 **HTTP 오류 404.0 – 찾을** 수 없음이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-175">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="85e98-176">다음 절차를 사용 하 여 ASP.NET 4.0이 등록 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-176">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="85e98-177">**IIS에 ASP.NET 4.0를 등록 하려면**</span><span class="sxs-lookup"><span data-stu-id="85e98-177">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="85e98-178">**시작**을 클릭 한 다음 **명령 프롬프트**를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-178">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="85e98-179">검색 결과에서 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-179">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="85e98-180">명령 프롬프트 창에서 **\ v 4.0.30319** 디렉터리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-180">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="85e98-181">다음 명령을 입력 하 고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-181">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample1.cmd)]
5. <span data-ttu-id="85e98-182">어느 시점에서 든 64 비트 웹 응용 프로그램을 호스트 하려는 경우 ASP.NET의 64 비트 버전을 IIS에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-182">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="85e98-183">이렇게 하려면 명령 프롬프트 창에서 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 디렉터리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-183">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="85e98-184">다음 명령을 입력 하 고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-184">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample2.cmd)]

<span data-ttu-id="85e98-185">지금까지 Windows 업데이트를 사용 하 여 설치한 새 제품 및 구성 요소에 대 한 사용 가능한 업데이트를 다운로드 하 고 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-185">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-iis-website"></a><span data-ttu-id="85e98-186">IIS 웹 사이트 구성</span><span class="sxs-lookup"><span data-stu-id="85e98-186">Configure the IIS Website</span></span>

<span data-ttu-id="85e98-187">웹 콘텐츠를 서버에 배포 하려면 먼저 콘텐츠를 호스팅하는 IIS 웹 사이트를 만들고 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-187">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="85e98-188">웹 배포는 기존 IIS 웹 사이트에만 웹 패키지를 배포할 수 있습니다. 웹 사이트를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-188">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="85e98-189">개략적인 수준에서 다음 작업을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-189">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="85e98-190">콘텐츠를 호스트할 파일 시스템에 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-190">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="85e98-191">콘텐츠를 제공 하는 IIS 웹 사이트를 만들고 로컬 폴더에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-191">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="85e98-192">로컬 폴더의 응용 프로그램 풀 id에 대 한 읽기 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-192">Grant read permissions to the application pool identity on the local folder.</span></span>

<span data-ttu-id="85e98-193">IIS의 기본 웹 사이트에 콘텐츠를 배포 하는 것은 아무 작업도 수행 하지 않지만 테스트 또는 데모 시나리오 이외의 다른 항목에는이 방법을 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-193">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="85e98-194">프로덕션 환경을 시뮬레이트하려면 응용 프로그램의 요구 사항과 관련 된 설정을 사용 하 여 새 IIS 웹 사이트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-194">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="85e98-195">**IIS 웹 사이트를 만들고 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="85e98-195">**To create and configure an IIS website**</span></span>

1. <span data-ttu-id="85e98-196">로컬 파일 시스템에서 콘텐츠를 저장할 폴더를 만듭니다 (예: **C:\demosite**).</span><span class="sxs-lookup"><span data-stu-id="85e98-196">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="85e98-197">**시작** 메뉴에서 **관리 도구**를 가리킨 다음 **인터넷 정보 서비스 (IIS) 관리자**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-197">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="85e98-198">IIS 관리자의 **연결** 창에서 서버 노드를 확장 합니다 (예: **PROWEB1**).</span><span class="sxs-lookup"><span data-stu-id="85e98-198">In IIS Manager, in the **Connections** pane, expand the server node (for example, **PROWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image3.png)
4. <span data-ttu-id="85e98-199">**사이트** 노드를 마우스 오른쪽 단추로 클릭 한 다음 **웹 사이트 추가**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-199">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="85e98-200">**사이트 이름** 상자에 IIS 웹 사이트의 이름을 입력 합니다 (예: **demosite**).</span><span class="sxs-lookup"><span data-stu-id="85e98-200">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="85e98-201">**실제 경로** 상자에 로컬 폴더 경로 (예: **c:\demosite**)를 입력 하거나 해당 경로를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-201">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="85e98-202">**포트** 상자에 웹 사이트를 호스트 하려는 포트 번호 (예: **85**)를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-202">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="85e98-203">표준 포트 번호는 HTTP의 경우 80이 고 HTTPS의 경우 443입니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-203">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="85e98-204">그러나 포트 80에서이 웹 사이트를 호스팅하는 경우 사이트에 액세스 하려면 먼저 기본 웹 사이트를 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-204">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="85e98-205">웹 사이트에 대 한 DNS (Domain Name System) 레코드를 구성 하려는 경우가 아니면 **호스트 이름** 상자를 비워 둡니다. 그런 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-205">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="85e98-206">프로덕션 환경에서는 포트 80에서 웹 사이트를 호스트 하 고 일치 하는 DNS 레코드와 함께 호스트 헤더를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-206">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="85e98-207">IIS 7에서 호스트 헤더를 구성 하는 방법에 대 한 자세한 내용은 [웹 사이트의 호스트 헤더 구성 (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx)을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="85e98-207">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="85e98-208">Windows Server 2008 r 2의 DNS 서버 역할에 대 한 자세한 내용은 [Dns 서버 개요](https://technet.microsoft.com/library/cc770392.aspx) 및 [dns 서버](https://technet.microsoft.com/windowsserver/dd448607)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="85e98-208">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="85e98-209">**작업** 창의 **사이트 편집**에서 **바인딩**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-209">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="85e98-210">**사이트 바인딩** 대화 상자에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-210">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image5.png)
11. <span data-ttu-id="85e98-211">**사이트 바인딩 추가** 대화 상자에서 기존 사이트 구성과 일치 하는 **IP 주소** 및 **포트** 를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-211">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="85e98-212">**호스트 이름** 상자에 웹 서버의 이름 (예: **PROWEB1**)을 입력 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-212">In the **Host name** box, type the name of your web server (for example, **PROWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="85e98-213">첫 번째 사이트 바인딩을 사용 하면 IP 주소와 포트 또는를 사용 하 여 로컬에서 사이트에 액세스할 수 있습니다 `http://localhost:85` .</span><span class="sxs-lookup"><span data-stu-id="85e98-213">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="85e98-214">두 번째 사이트 바인딩을 사용 하면 컴퓨터 이름 (예:)을 사용 하 여 도메인에 있는 다른 컴퓨터에서 사이트에 액세스할 수 있습니다 http://proweb1:85) .</span><span class="sxs-lookup"><span data-stu-id="85e98-214">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://proweb1:85).</span></span>
13. <span data-ttu-id="85e98-215">**사이트 바인딩** 대화 상자에서 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-215">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="85e98-216">**연결** 창에서 **애플리케이션 풀**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-216">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="85e98-217">**응용 프로그램 풀** 창에서 응용 프로그램 풀의 이름을 마우스 오른쪽 단추로 클릭 한 다음 **기본 설정**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-217">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="85e98-218">기본적으로 응용 프로그램 풀의 이름은 웹 사이트의 이름 (예: **Demosite**)과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-218">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="85e98-219">**.NET Framework 버전** 목록에서 **.NET Framework v 4.0.30319**를 선택한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-219">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="85e98-220">샘플 솔루션에는 .NET Framework 4.0가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-220">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="85e98-221">이는 일반적으로 웹 배포 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-221">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="85e98-222">웹 사이트가 콘텐츠를 제공 하기 위해 응용 프로그램 풀 id에 콘텐츠를 저장 하는 로컬 폴더에 대 한 읽기 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-222">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="85e98-223">IIS 7.5에서 응용 프로그램 풀은 기본적으로 고유한 응용 프로그램 풀 id로 실행 됩니다 (응용 프로그램 풀은 일반적으로 Network Service 계정을 사용 하 여 실행 되는 이전 버전의 IIS와 대조).</span><span class="sxs-lookup"><span data-stu-id="85e98-223">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="85e98-224">응용 프로그램 풀 id는 실제 사용자 계정이 아니므로 대신 사용자 또는&#x2014;그룹 목록에 표시 되지 않습니다. 대신 응용 프로그램 풀이 시작 될 때 동적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-224">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="85e98-225">각 응용 프로그램 풀 id는 로컬 **IIS \_ iusrs** 보안 그룹에 숨겨진 항목으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-225">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="85e98-226">파일이 나 폴더에서 응용 프로그램 풀 id에 대 한 사용 권한을 부여 하려면 다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-226">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="85e98-227">Iis **AppPool \( 응용 프로그램 풀 이름을** 사용 하 여 응용 프로그램 풀 id에 직접 사용 권한을 할당 합니다 (예: **iis AppPool\DemoSite**).</span><span class="sxs-lookup"><span data-stu-id="85e98-227">Assign permissions to the application pool identity directly, using the format **IIS AppPool\(application pool name)** (for example, **IIS AppPool\DemoSite**).</span></span>
- <span data-ttu-id="85e98-228">**IIS \_ iusrs** 그룹에 사용 권한을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-228">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="85e98-229">가장 일반적인 방법은 로컬 **IIS \_ iusrs** 그룹에 사용 권한을 할당 하는 것입니다 .이 방법을 사용 하면 파일 시스템 권한을 다시 구성 하지 않고 응용 프로그램 풀을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-229">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="85e98-230">다음 절차에서는이 그룹 기반 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-230">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="85e98-231">IIS 7.5의 응용 프로그램 풀 id에 대 한 자세한 내용은 [응용 프로그램 풀 id](https://go.microsoft.com/?linkid=9805123)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="85e98-231">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="85e98-232">**IIS 웹 사이트에 대 한 폴더 사용 권한을 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="85e98-232">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="85e98-233">Windows 탐색기에서 로컬 폴더의 위치로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-233">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="85e98-234">폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-234">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="85e98-235">**Security** 탭에서 **Edit**을 클릭한 다음 **Add**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-235">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="85e98-236">**위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-236">Click **Locations**.</span></span> <span data-ttu-id="85e98-237">**위치** 대화 상자에서 로컬 서버를 선택 하 고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-237">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image8.png)
5. <span data-ttu-id="85e98-238">**사용자 또는 그룹 선택** 대화 상자에서 **IIS \_ iusrs**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-238">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="85e98-239">**에 대 한 사용 권한 (폴더 이름)** 대화 상자에서 새 그룹에 **읽기 & 실행**, **폴더 내용**보기 및 기본적으로 **읽기** 권한이 할당 된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-239">In the **Permissions for (folder name)** dialog box, notice that the new group has been assigned the **Read & execute**, **List folder contents**, and **Read** permissions by default.</span></span> <span data-ttu-id="85e98-240">이를 변경 되지 않은 상태로 두고 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-240">Leave this unchanged and click **OK**.</span></span>
7. <span data-ttu-id="85e98-241">**확인** 을 클릭 하 여 **(폴더 이름) 속성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-241">Click **OK** to close the **(folder name) Properties** dialog box.</span></span>

## <a name="disable-the-remote-agent-service"></a><span data-ttu-id="85e98-242">원격 에이전트 서비스를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="85e98-242">Disable the Remote Agent Service</span></span>

<span data-ttu-id="85e98-243">웹 배포를 설치 하는 경우 웹 Deployment Agent 서비스가 설치 되 고 자동으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-243">When you install Web Deploy, the Web Deployment Agent Service is installed and started automatically.</span></span> <span data-ttu-id="85e98-244">이 서비스를 사용 하면 원격 위치에서 웹 패키지를 배포 하 고 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-244">This service allows you to deploy and publish web packages from a remote location.</span></span> <span data-ttu-id="85e98-245">이 시나리오에서는 원격 배포 기능을 사용 하지 않으므로 서비스를 중지 하 고 사용 하지 않도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-245">You won't be using the remote deployment capability in this scenario, so you should stop and disable the service.</span></span>

> [!NOTE]
> <span data-ttu-id="85e98-246">웹 패키지를 수동으로 가져오고 배포 하기 위해 원격 에이전트 서비스를 중지할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-246">You don't need to stop the remote agent service in order to import and deploy a web package manually.</span></span> <span data-ttu-id="85e98-247">그러나 서비스를 사용 하지 않으려는 경우 서비스를 중지 하 고 사용 하지 않도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-247">However, it's a good practice to stop and disable the service if you don't plan to use it.</span></span>

<span data-ttu-id="85e98-248">다양 한 명령줄 유틸리티나 Windows PowerShell cmdlet을 사용 하 여 여러 가지 방법으로 서비스를 중지 하 고 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-248">You can stop and disable a service in multiple ways, using various command-line utilities or Windows PowerShell cmdlets.</span></span> <span data-ttu-id="85e98-249">이 절차에서는 간단한 UI 기반 접근 방식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-249">This procedure describes a straightforward UI-based approach.</span></span>

<span data-ttu-id="85e98-250">**원격 에이전트 서비스를 중지 하 고 사용 하지 않도록 설정 하려면**</span><span class="sxs-lookup"><span data-stu-id="85e98-250">**To stop and disable the remote agent service**</span></span>

1. <span data-ttu-id="85e98-251">**시작** 메뉴에서 **관리 도구**를 가리킨 다음 **서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-251">On the **Start** menu, point to **Administrative Tools**, and then click **Services**.</span></span>
2. <span data-ttu-id="85e98-252">서비스 콘솔에서 **웹 Deployment Agent 서비스** 행을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-252">In the Services console, locate the **Web Deployment Agent Service** row.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image9.png)
3. <span data-ttu-id="85e98-253">**웹 Deployment Agent Service**를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-253">Right-click **Web Deployment Agent Service**, and then click **Properties**.</span></span>
4. <span data-ttu-id="85e98-254">**웹 Deployment Agent 서비스 속성** 대화 상자에서 **중지**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-254">In the **Web Deployment Agent Service Properties** dialog box, click **Stop**.</span></span>
5. <span data-ttu-id="85e98-255">**시작 유형** 목록에서 **사용 안 함**을 선택한 다음 **확인**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-255">In the **Startup type** list, select **Disabled**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image10.png)

## <a name="conclusion"></a><span data-ttu-id="85e98-256">결론</span><span class="sxs-lookup"><span data-stu-id="85e98-256">Conclusion</span></span>

<span data-ttu-id="85e98-257">이 시점에서 웹 서버를 오프 라인 웹 패키지 배포에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-257">At this point, your web server is ready for offline web package deployment.</span></span> <span data-ttu-id="85e98-258">웹 패키지를 IIS 웹 사이트로 가져오기 전에 다음 핵심 사항을 확인 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e98-258">Before you attempt to import web packages to an IIS website, you may want to check these key points:</span></span>

- <span data-ttu-id="85e98-259">ASP.NET 4.0를 IIS에 등록 했습니까?</span><span class="sxs-lookup"><span data-stu-id="85e98-259">Have you registered ASP.NET 4.0 with IIS?</span></span>
- <span data-ttu-id="85e98-260">응용 프로그램 풀 id에 웹 사이트의 원본 폴더에 대 한 읽기 권한이 있나요?</span><span class="sxs-lookup"><span data-stu-id="85e98-260">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="85e98-261">웹 Deployment Agent 서비스를 중지 했습니까?</span><span class="sxs-lookup"><span data-stu-id="85e98-261">Have you stopped the Web Deployment Agent Service?</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="85e98-262">[이전](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
> [다음](configuring-a-database-server-for-web-deploy-publishing.md)</span><span class="sxs-lookup"><span data-stu-id="85e98-262">[Previous](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
[Next](configuring-a-database-server-for-web-deploy-publishing.md)</span></span>
