---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다. 테스트 환경-12 5로 IIS에 배포 | Microsoft Docs
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: 191d194d4aaad15ac6c5187105d49a03a2f06bf2
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59413349"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a><span data-ttu-id="f1493-103">SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다. IIS 5 12-테스트 환경으로 배포</span><span class="sxs-lookup"><span data-stu-id="f1493-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying to IIS as a Test Environment - 5 of 12</span></span>

<span data-ttu-id="f1493-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f1493-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f1493-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="f1493-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="f1493-106">이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="f1493-107">Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="f1493-108">계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="f1493-109">Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="f1493-110">개요</span><span class="sxs-lookup"><span data-stu-id="f1493-110">Overview</span></span>

<span data-ttu-id="f1493-111">이 자습서에서는 로컬 컴퓨터의 IIS에 ASP.NET 웹 응용 프로그램을 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-111">This tutorial shows how to deploy an ASP.NET web application to IIS on the local computer.</span></span>

<span data-ttu-id="f1493-112">응용 프로그램을 개발할 때 일반적으로 Visual Studio에서 실행 하 여 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-112">When you develop an application, you generally test by running it in Visual Studio.</span></span> <span data-ttu-id="f1493-113">기본적으로 Visual Studio 개발 서버 (Cassini 라고도 함)를 사용 하는이 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-113">By default, this means you're using the Visual Studio Development Server (also known as Cassini).</span></span> <span data-ttu-id="f1493-114">Visual Studio 개발 서버를 쉽게 Visual Studio에서 개발 중 테스트 하지만 IIS와 동일 하 게 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-114">The Visual Studio Development Server makes it easy to test during development in Visual Studio, but it doesn't work exactly like IIS.</span></span> <span data-ttu-id="f1493-115">결과적으로, Visual Studio에서 테스트 해도 호스팅 환경에서 IIS에 배포 될 때 실패 하는 경우 응용 프로그램은 제대로 실행 가능한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-115">As a result, it's possible that an application will run correctly when you test it in Visual Studio, but fail when it's deployed to IIS in a hosting environment.</span></span>

<span data-ttu-id="f1493-116">다음과 같은이 방법으로 응용 프로그램을 안정적으로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-116">You can test your application more reliably in these ways:</span></span>

1. <span data-ttu-id="f1493-117">개발 하는 동안 Visual Studio에서 테스트 하는 경우 Visual Studio 개발 서버 대신 IIS Express 또는 전체 IIS를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-117">Use IIS Express or full IIS instead of the Visual Studio Development Server when you test in Visual Studio during development.</span></span> <span data-ttu-id="f1493-118">이 방법을 일반적으로 에뮬레이트하 보다 정확 하 게 IIS에서 사이트를 실행 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-118">This method generally emulates more accurately how your site will run under IIS.</span></span> <span data-ttu-id="f1493-119">그러나이 메서드는 없습니다 배포 프로세스를 테스트 하거나 배포 프로세스의 결과 올바르게 실행 되는 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-119">However, this method does not test your deployment process or validate that the result of the deployment process will run correctly.</span></span>
2. <span data-ttu-id="f1493-120">프로덕션 환경으로 배포 하려면 나중에 사용할 것과 동일한 프로세스를 사용 하 여 개발 컴퓨터에서 IIS 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-120">Deploy the application to IIS on your development computer by using the same process that you'll use later to deploy it to your production environment.</span></span> <span data-ttu-id="f1493-121">이 메서드는 IIS에서 응용 프로그램이 올바르게 실행 되는 유효성을 검사 하는 것 외에도 배포 프로세스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-121">This method validates your deployment process in addition to validating that your application will run correctly under IIS.</span></span>
3. <span data-ttu-id="f1493-122">가까이 있는 최대한 프로덕션 환경과 테스트 환경에 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-122">Deploy the application to a test environment that is as close as possible to your production environment.</span></span> <span data-ttu-id="f1493-123">이 자습서에 대 한 프로덕션 환경에서 타사 호스팅 공급자 이므로 이상적인 테스트 환경 호스팅 공급자를 사용 하 여 두 번째 계정을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-123">Since the production environment for these tutorials is a third-party hosting provider, the ideal test environment would be a second account with the hosting provider.</span></span> <span data-ttu-id="f1493-124">테스트에 대해서만이 두 번째 계정을 사용 하지만 프로덕션 계정으로는 동일한 방식으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-124">You would use this second account only for testing, but it would be set up the same way as the production account.</span></span>

<span data-ttu-id="f1493-125">이 자습서에는 옵션 2 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-125">This tutorial shows the steps for option 2.</span></span> <span data-ttu-id="f1493-126">옵션 3에 대 한 지침의 끝에 제공 되는 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에서는이 자습서의 끝은 옵션 1에 대 한 리소스에 대 한 링크 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-126">Guidance for option 3 is provided at the end of the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial, and at the end of this tutorial there are links to resources for option 1.</span></span>

<span data-ttu-id="f1493-127">미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-127">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="configuring-the-application-to-run-in-medium-trust"></a><span data-ttu-id="f1493-128">보통 신뢰 수준에서 실행 하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="f1493-128">Configuring the Application to Run in Medium Trust</span></span>

<span data-ttu-id="f1493-129">IIS를 설치 하 고을 배포 하기 전에 Web.config 파일 설정 수 있도록 사이트 실행 보다 일반적인 공유 호스팅 환경에서 것 처럼 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-129">Before installing IIS and deploying to it, you'll change a Web.config file setting in order to make the site run more like it will in a typical shared hosting environment.</span></span>

<span data-ttu-id="f1493-130">호스팅 공급자는 일반적으로 웹 사이트에서 실행 *보통 신뢰*, 즉, 몇 가지 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-130">Hosting providers typically run your web site in *medium trust*, which means there are some things it is not allowed to do.</span></span> <span data-ttu-id="f1493-131">예를 들어, 응용 프로그램 코드 없습니다 Windows 레지스트리에 액세스 및 없습니다 읽기 또는 쓰기 응용 프로그램의 폴더 계층 구조 외부에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-131">For example, application code can't access the Windows registry and can't read or write files that are outside of your application's folder hierarchy.</span></span> <span data-ttu-id="f1493-132">기본적으로 응용 프로그램에서 실행 *높은 신뢰* 로컬 컴퓨터에서 의미 하는 응용 프로그램이 프로덕션에 배포할 때 오류가 발생 하는 작업을 수행 하는 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-132">By default your application runs in *high trust* on your local computer, which means that the application might be able to do things that would fail when you deploy it to production.</span></span> <span data-ttu-id="f1493-133">따라서 되도록 더 정확 하 게 반영 테스트 환경을 프로덕션 환경, 보통 신뢰 수준에서 실행할 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-133">Therefore, to make the test environment more accurately reflect the production environment, you'll configure the application to run in medium trust.</span></span>

<span data-ttu-id="f1493-134">응용 프로그램 Web.config 파일에서 추가 **트러스트** 요소에는 **system.web** 요소를이 예와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-134">In the application Web.config file, add a **trust** element in the **system.web** element, as shown in this example.</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

<span data-ttu-id="f1493-135">응용 프로그램이 이제 로컬 컴퓨터에도 IIS에서 보통 신뢰에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-135">The application will now run in medium trust in IIS even on your local computer.</span></span> <span data-ttu-id="f1493-136">이 설정을 사용 하면 작업을 수행 하는 프로덕션 환경에서 실패 하는 응용 프로그램 코드에서 최대한 일찍 시도 catch 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-136">This setting enables you to catch as early as possible any attempts by application code to do something that would fail in production.</span></span>

> [!NOTE]
> <span data-ttu-id="f1493-137">Entity Framework Code First 마이그레이션을 사용 하는 경우 버전 5.0 했는지 또는 나중에 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-137">If you are using Entity Framework Code First Migrations, make sure that you have version 5.0 or later installed.</span></span> <span data-ttu-id="f1493-138">Entity framework 버전 4.3, 마이그레이션 데이터베이스 스키마를 업데이트 하려면 완전 신뢰가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-138">In Entity Framework version 4.3, Migrations requires full trust in order to update the database schema.</span></span>


## <a name="installing-iis-and-web-deploy"></a><span data-ttu-id="f1493-139">설치할 IIS 및 웹 배포</span><span class="sxs-lookup"><span data-stu-id="f1493-139">Installing IIS and Web Deploy</span></span>

<span data-ttu-id="f1493-140">IIS를 개발 컴퓨터에서 IIS에 배포 해야 하 고 웹 배포 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-140">To deploy to IIS on your development computer, you must have IIS and Web Deploy installed.</span></span> <span data-ttu-id="f1493-141">이러한 기본 Windows 7 구성에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-141">These are not included in the default Windows 7 configuration.</span></span> <span data-ttu-id="f1493-142">IIS 및 웹 배포를 설치한 경우 다음 섹션으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-142">If you have already installed both IIS and Web Deploy, skip to the next section.</span></span>

<span data-ttu-id="f1493-143">사용 하 여 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 웹 플랫폼 설치 관리자를 IIS에 대 한 권장된 구성이 설치 하 고 자동으로 IIS 및 웹에 대 한 필수 구성 요소를 설치 하기 때문에 IIS 및 웹 배포를 설치 하는 기본 방법은 필요한 경우 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-143">Using the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) is the preferred way to install IIS and Web Deploy, because the Web Platform Installer installs a recommended configuration for IIS and it automatically installs the prerequisites for IIS and Web Deploy if necessary.</span></span>

<span data-ttu-id="f1493-144">IIS 및 웹 배포를 설치 하려면 웹 플랫폼 설치 관리자를 실행 하려면 다음 링크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-144">To run Web Platform Installer to install IIS and Web Deploy, use the following link.</span></span> <span data-ttu-id="f1493-145">이미 설치한 경우 IIS, 웹 배포 또는 관련 필수 구성 요소 중 하나를 웹 플랫폼 설치 관리자는 누락 된 것만 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-145">If you already have installed IIS, Web Deploy or any of their required components, the Web Platform Installer installs only what is missing.</span></span>

- [<span data-ttu-id="f1493-146">IIS 및 WebPI를 사용 하 여 웹 배포 설치</span><span class="sxs-lookup"><span data-stu-id="f1493-146">Install IIS and Web Deploy using WebPI</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a><span data-ttu-id="f1493-147">.NET 4에 기본 응용 프로그램 풀 설정</span><span class="sxs-lookup"><span data-stu-id="f1493-147">Setting the Default Application Pool to .NET 4</span></span>

<span data-ttu-id="f1493-148">IIS를 설치한 후 실행 **IIS 관리자** .NET Framework 버전 4에 기본 응용 프로그램 풀에 할당 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-148">After installing IIS, run **IIS Manager** to make sure that the .NET Framework version 4 is assigned to the default application pool.</span></span>

<span data-ttu-id="f1493-149">Windows에서 **시작** 메뉴에서 **실행**에서 "inetmgr"을 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-149">From the Windows **Start** menu, select **Run**, enter "inetmgr", and then click **OK**.</span></span> <span data-ttu-id="f1493-150">(경우 합니다 **실행** 명령에 없는 경우에 **시작** 메뉴를 열고 Windows 키와 R을 눌러 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-150">(If the **Run** command is not in your **Start** menu, you can press the Windows Key and R to open it.</span></span> <span data-ttu-id="f1493-151">또는 작업 표시줄을 마우스 오른쪽 단추로 클릭 합니다 **속성**를 선택 합니다 **시작 메뉴** 탭을 클릭 **사용자 지정**를 선택한 **명령을 실행**.)</span><span class="sxs-lookup"><span data-stu-id="f1493-151">Or right-click the taskbar, click **Properties**, select the **Start Menu** tab, click **Customize**, and select **Run command**.)</span></span>

<span data-ttu-id="f1493-152">에 **연결** 창에서 서버 노드를 확장 하 고 선택 **응용 프로그램 풀**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-152">In the **Connections** pane, expand the server node and select **Application Pools**.</span></span> <span data-ttu-id="f1493-153">에 **응용 프로그램 풀** 창 경우 **DefaultAppPool** 는 다음 섹션으로 건너뛸.NET framework 버전 4 다음 그림과 같이 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-153">In the **Application Pools** pane, if **DefaultAppPool** is assigned to the .NET framework version 4 as in the following illustration, skip to the next section.</span></span>

[![I<span data-ttu-id="f1493-154">netmgr_showing_4.0_app_pools]</span><span class="sxs-lookup"><span data-stu-id="f1493-154">netmgr_showing_4.0_app_pools]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)

<span data-ttu-id="f1493-155">두 개의 응용 프로그램 풀을 표시 하 고 둘 다.NET Framework 2.0으로 설정 됩니다 하는 경우 IIS에서 ASP.NET 4를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-155">If you see only two application pools and both of them are set to the .NET Framework 2.0, you have to install ASP.NET 4 in IIS:</span></span>

- <span data-ttu-id="f1493-156">마우스 오른쪽 단추로 클릭 하 여 명령 프롬프트 창을 엽니다 **명령 프롬프트** 는 Windows에서 **시작** 메뉴에서 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-156">Open a command prompt window by right-clicking **Command Prompt** in the Windows **Start** menu and selecting **Run as Administrator**.</span></span> <span data-ttu-id="f1493-157">그런 다음 실행 [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) 다음 명령을 사용 하 여 IIS에서 ASP.NET 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-157">Then run [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) to install ASP.NET 4 in IIS, using the following commands.</span></span> <span data-ttu-id="f1493-158">(64 비트 시스템에서는 "Framework64"를 사용 하 여 "Framework를"를 바꿉니다.)</span><span class="sxs-lookup"><span data-stu-id="f1493-158">(In 64-bit systems, replace "Framework" with "Framework64".)</span></span>

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    [![a<span data-ttu-id="f1493-159">spnet_regiis_installing_ASP.NET_4]</span><span class="sxs-lookup"><span data-stu-id="f1493-159">spnet_regiis_installing_ASP.NET_4]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)

    <span data-ttu-id="f1493-160">이 명령은.NET Framework 4에 대 한 새 응용 프로그램 풀 만들지만 기본 응용 프로그램 풀은 계속 2.0으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-160">This command creates new application pools for the .NET Framework 4, but the default application pool will still be set to 2.0.</span></span> <span data-ttu-id="f1493-161">배포 하는 응용 프로그램.NET 4를 대상으로 하는 해당 응용 프로그램 풀에.NET 4 응용 프로그램 풀을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-161">You'll be deploying an application that targets .NET 4 to that application pool, so you have to change the application pool to .NET 4.</span></span>

<span data-ttu-id="f1493-162">닫은 경우 **IIS 관리자**, 다시 실행, 해당 서버 노드를 확장 하 고 클릭 **응용 프로그램 풀** 표시 하는 **응용 프로그램 풀** 창으로 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-162">If you closed **IIS Manager**, run it again, expand the server node, and click **Application Pools** to display the **Application Pools** pane again.</span></span>

<span data-ttu-id="f1493-163">에 **응용 프로그램 풀** 창 클릭 **DefaultAppPool**를 선택한 다음를 **작업** 창 **기본 설정**.</span><span class="sxs-lookup"><span data-stu-id="f1493-163">In the **Application Pools** pane, click **DefaultAppPool**, and then in the **Actions** pane click **Basic Settings**.</span></span>

[![I<span data-ttu-id="f1493-164">netmgr_selecting_Basic_Settings_for_app_pool]</span><span class="sxs-lookup"><span data-stu-id="f1493-164">netmgr_selecting_Basic_Settings_for_app_pool]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)

<span data-ttu-id="f1493-165">에 **응용 프로그램 풀 편집** 대화 상자에서 변경 **.NET Framework 버전** 하 **.NET Framework v4.0.30319** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-165">In the **Edit Application Pool** dialog box, change **.NET Framework version** to **.NET Framework v4.0.30319** and click **OK**.</span></span>

[![S<span data-ttu-id="f1493-166">electing_.NET_4_for_DefaultAppPool]</span><span class="sxs-lookup"><span data-stu-id="f1493-166">electing_.NET_4_for_DefaultAppPool]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)

<span data-ttu-id="f1493-167">이제 IIS에 게시할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-167">You are now ready to publish to IIS.</span></span>

## <a name="publishing-to-iis"></a><span data-ttu-id="f1493-168">IIS에 게시</span><span class="sxs-lookup"><span data-stu-id="f1493-168">Publishing to IIS</span></span>

<span data-ttu-id="f1493-169">여러 가지 방법으로 Visual Studio 2010 및 웹 배포를 사용 하 여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-169">There are several ways you can deploy using Visual Studio 2010 and Web Deploy:</span></span>

- <span data-ttu-id="f1493-170">One-click 게시 하는 Visual Studio를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-170">Use Visual Studio one-click publish.</span></span>
- <span data-ttu-id="f1493-171">만들기는 *배포 패키지* IIS 관리자 UI를 사용 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-171">Create a *deployment package* and install it using the IIS Manager UI.</span></span> <span data-ttu-id="f1493-172">배포 패키지를 구성 하는 *.zip* 모든 파일과 IIS에서 사이트를 설치 하는 데 필요한 메타 데이터를 포함 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-172">The deployment package consists of a *.zip* file that contains all the files and metadata needed to install a site in IIS.</span></span>
- <span data-ttu-id="f1493-173">배포 패키지를 만들고 명령줄을 사용 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-173">Create a deployment package and install it using the command line.</span></span>

<span data-ttu-id="f1493-174">수행한 프로세스를 통해 자동화 하도록 Visual Studio를 설정 하려면 이전 자습서에서 배포 작업의 이러한 세 가지 방법을 모두에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-174">The process you went through in the previous tutorials to set up Visual Studio to automate deployment tasks applies to all of these three methods.</span></span> <span data-ttu-id="f1493-175">이 자습서에서는 이러한 메서드의 첫 번째를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-175">In these tutorials you'll use the first of these methods.</span></span> <span data-ttu-id="f1493-176">배포 패키지 사용에 대 한 자세한 내용은 [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/library/bb386521.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-176">For information about using deployment packages, see [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx).</span></span>

<span data-ttu-id="f1493-177">게시 하기 전에 Visual Studio를 관리자 모드에서 실행 되 고 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-177">Before publishing, make sure that you are running Visual Studio in administrator mode.</span></span> <span data-ttu-id="f1493-178">(Windows 7에서 **시작** 메뉴를 사용 하는 Visual Studio 버전에 대 한 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**.) 관리자 모드는만 경우 게시 하는 IIS에 로컬 컴퓨터의 게시에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-178">(In the Windows 7 **Start** menu, right-click the icon for the version of Visual Studio you're using and select **Run as Administrator**.) Administrator mode is required for publishing only when you are publishing to IIS on the local computer.</span></span>

<span data-ttu-id="f1493-179">**솔루션 탐색기**ContosoUniversity 프로젝트 (ContosoUniversity.DAL 프로젝트 아님)를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-179">In **Solution Explorer**, right-click the ContosoUniversity project (not the ContosoUniversity.DAL project) and select **Publish**.</span></span>

<span data-ttu-id="f1493-180">합니다 **웹 게시** 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-180">The **Publish Web** wizard appears.</span></span>

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

<span data-ttu-id="f1493-182">드롭다운 목록에서 선택  **&lt;새로 만들기... &gt;**.</span><span class="sxs-lookup"><span data-stu-id="f1493-182">In the drop-down list, select **&lt;New...&gt;**.</span></span>

<span data-ttu-id="f1493-183">에 **새 프로필** 대화 상자에서 "Test"를 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-183">In the **New Profile** dialog box, enter "Test", and then click **OK**.</span></span>

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

<span data-ttu-id="f1493-185">이 이름은 이전에 만든 파일을 변환 합니다 Web.Test.config의 중간 노드와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-185">This name is the same as the middle node of the Web.Test.config transform file that you created earlier.</span></span> <span data-ttu-id="f1493-186">이 관계 이며이 프로필을 사용 하 여 게시할 때 적용할 Web.Test.config 변환 원인</span><span class="sxs-lookup"><span data-stu-id="f1493-186">This correspondence is what causes the Web.Test.config transformations to be applied when you publish by using this profile.</span></span>

<span data-ttu-id="f1493-187">마법사를 자동으로 이동 합니다 **연결** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-187">The wizard automatically advances to the **Connection** tab.</span></span>

<span data-ttu-id="f1493-188">에 **서비스 URL** 상자에 입력 합니다 *localhost*합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-188">In the **Service URL** box, enter *localhost*.</span></span>

<span data-ttu-id="f1493-189">에 **사이트 및 응용 프로그램** 상자에 입력 합니다 *기본 웹 사이트/ContosoUniversity*합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-189">In the **Site/application** box, enter *Default Web Site/ContosoUniversity*.</span></span>

<span data-ttu-id="f1493-190">에 **대상 URL** 상자에 입력 `http://localhost/ContosoUniversity`합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-190">In the **Destination URL** box, enter `http://localhost/ContosoUniversity`.</span></span>

<span data-ttu-id="f1493-191">합니다 **대상 URL** 설정이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-191">The **Destination URL** setting isn't required.</span></span> <span data-ttu-id="f1493-192">Visual Studio 응용 프로그램 배포 완료 되 면 기본 브라우저가이 URL로 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-192">When Visual Studio finishes deploying the application, it automatically opens your default browser to this URL.</span></span> <span data-ttu-id="f1493-193">배포 후 자동으로 열려면 브라우저를 사용 하지 않으려는 경우에이 상자를 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-193">If you don't want the browser to open automatically after deployment, leave this box blank.</span></span>

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

<span data-ttu-id="f1493-195">클릭 **연결 유효성 검사** 설정이 올바른지 고 로컬 컴퓨터의 IIS에 연결할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-195">Click **Validate Connection** to verify that the settings are correct and you can connect to IIS on the local computer.</span></span>

<span data-ttu-id="f1493-196">녹색 확인 표시가 성공적으로 연결 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-196">A green check mark verifies that the connection is successful.</span></span>

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

<span data-ttu-id="f1493-198">클릭 **다음** 이동 합니다 **설정** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-198">Click **Next** to advance to the **Settings** tab.</span></span>

<span data-ttu-id="f1493-199">합니다 **구성** 드롭다운 목록 상자에 배포 하도록 빌드 구성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-199">The **Configuration** drop-down box specifies the build configuration to deploy.</span></span> <span data-ttu-id="f1493-200">기본값은 릴리스 원한다 면 말 이죠.</span><span class="sxs-lookup"><span data-stu-id="f1493-200">The default value is Release, which is what you want.</span></span>

<span data-ttu-id="f1493-201">유지 된 **대상에서 추가 파일 제거** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-201">Leave the **Remove additional files at destination** check box cleared.</span></span> <span data-ttu-id="f1493-202">첫 번째 배포 이므로 없습니다 모든 파일이 대상 폴더에 아직.</span><span class="sxs-lookup"><span data-stu-id="f1493-202">Since this is your first deployment, there won't be any files in the destination folder yet.</span></span>

<span data-ttu-id="f1493-203">에 **데이터베이스** 섹션에 대 한 연결 문자열 상자에서 다음 값을 입력 합니다 **SchoolContext**:</span><span class="sxs-lookup"><span data-stu-id="f1493-203">In the **Databases** section, enter the following value in the connection string box for **SchoolContext**:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

<span data-ttu-id="f1493-204">때문에 배포 프로세스 배포 된 Web.config 파일에서이 연결 문자열 저장 됩니다 **런타임에이 연결 문자열을 사용 하 여** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-204">The deployment process will put this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

<span data-ttu-id="f1493-205">또한 아래 **SchoolContext**를 선택 **Code First 마이그레이션을 적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-205">Also under **SchoolContext**, select **Apply Code First Migrations**.</span></span> <span data-ttu-id="f1493-206">이 옵션을 지정 하려면 배포 된 Web.config 파일을 구성 하는 배포 프로세스 사용 하면는 `MigrateDatabaseToLatestVersion` 이니셜라이저입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-206">This option causes the deployment process to configure the deployed Web.config file to specify the `MigrateDatabaseToLatestVersion` initializer.</span></span> <span data-ttu-id="f1493-207">자동으로이 이니셜라이저 응용 프로그램 배포 후 처음으로 데이터베이스에 액세스 하는 경우 데이터베이스를 최신 버전에 게 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-207">This initializer automatically updates the database to the latest version when the application accesses the database for the first time after deployment.</span></span>

<span data-ttu-id="f1493-208">에 대 한 연결 문자열 상자에 **DefaultConnection**, 다음 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-208">In the connection string box for **DefaultConnection**, enter the following value:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

<span data-ttu-id="f1493-209">둡니다 **데이터베이스 업데이트** 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-209">Leave **Update database** cleared.</span></span> <span data-ttu-id="f1493-210">앱에서.sdf 파일을 복사 하 여 멤버 자격 데이터베이스가 배포 될\_데이터를 숨기려면이 데이터베이스를 사용 하 여 다른 작업을 수행 하는 배포 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-210">The membership database will be deployed by copying the .sdf file in App\_Data, and you don't want the deployment process to do anything else with this database.</span></span>

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

<span data-ttu-id="f1493-212">클릭 **다음** 이동 하 여 **미리 보기** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-212">Click **Next** to advance to the **Preview** tab.</span></span>

<span data-ttu-id="f1493-213">에 **미리 보기** 탭을 클릭 **미리 보기 시작** 복사 될 파일의 목록을 보려면.</span><span class="sxs-lookup"><span data-stu-id="f1493-213">In the **Preview** tab, click **Start Preview** to see a list of the files that will be copied.</span></span>

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

<span data-ttu-id="f1493-216">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-216">Click **Publish**.</span></span>

<span data-ttu-id="f1493-217">Visual Studio 관리자 모드에 없는 경우 사용 권한 오류를 나타내는 오류 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-217">If Visual Studio is not in administrator mode, you might get an error message that indicates a permissions error.</span></span> <span data-ttu-id="f1493-218">이 경우 Visual Studio를 닫습니다, 그리고 관리자 모드에서 엽니다 및 다시 게시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-218">In that case, close Visual Studio, open it in administrator mode, and try to publish again.</span></span>

<span data-ttu-id="f1493-219">Visual Studio 관리자 모드에 있으면 합니다 **출력** 창 보고서를 성공적으로 빌드 및 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-219">If Visual Studio is in administrator mode, the **Output** window reports successful build and publish.</span></span>

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

<span data-ttu-id="f1493-221">브라우저는 자동으로 로컬 컴퓨터의 IIS에서 실행 되는 Contoso University 홈 페이지로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-221">The browser automatically opens to the Contoso University Home page running in IIS on the local computer.</span></span>

[![H<span data-ttu-id="f1493-222">ome_page_Test]</span><span class="sxs-lookup"><span data-stu-id="f1493-222">ome_page_Test]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)

## <a name="testing-in-the-test-environment"></a><span data-ttu-id="f1493-223">테스트 환경에서 테스트</span><span class="sxs-lookup"><span data-stu-id="f1493-223">Testing in the Test Environment</span></span>

<span data-ttu-id="f1493-224">환경 표시기 표시 "(테스트)" 대신 "(Dev)"는 것을 보여 줍니다 합니다 *Web.config* 환경 표시기에 대 한 변환의 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-224">Notice that the environment indicator shows "(Test)" instead of "(Dev)", which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

[![H<span data-ttu-id="f1493-225">ome_page_Test]</span><span class="sxs-lookup"><span data-stu-id="f1493-225">ome_page_Test]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)

<span data-ttu-id="f1493-226">실행 된 **학생** 페이지 배포 된 데이터베이스에 학생이 없는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-226">Run the **Students** page to verify that the deployed database has no students.</span></span> <span data-ttu-id="f1493-227">이 페이지를 선택 하면 Code First는 데이터베이스를 만듭니다 및 다음을 실행 하기 때문에 로드 하려면 몇 분 정도 걸릴 수 있습니다는 `Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f1493-227">When you select this page it may take a few minutes to load because Code First creates the database and then runs the `Seed` method.</span></span> <span data-ttu-id="f1493-228">(수행 되지 않은 것을 응용 프로그램 데이터베이스에 아직 액세스 하지 않은 시도 하기 때문에 홈 페이지에서 했을 때.)</span><span class="sxs-lookup"><span data-stu-id="f1493-228">(It didn't do that when you were on the home page because the application didn't try to access the database yet.)</span></span>

[![S<span data-ttu-id="f1493-229">tudents_page_Test]</span><span class="sxs-lookup"><span data-stu-id="f1493-229">tudents_page_Test]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)

<span data-ttu-id="f1493-230">실행 된 **강사** 페이지는 Code First 시드 강사 데이터를 사용 하 여 데이터베이스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-230">Run the **Instructors** page to verify that Code First seeded the database with instructor data:</span></span>

[![I<span data-ttu-id="f1493-231">nstructors_page_Test]</span><span class="sxs-lookup"><span data-stu-id="f1493-231">nstructors_page_Test]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)

<span data-ttu-id="f1493-232">선택 **추가 학생** 에서 **학생** 메뉴에서 학생을 추가 하 고 다음에 새 학생을 봅니다 합니다 **학생** 성공적으로 데이터베이스에 쓸 수를 확인 하려면 페이지 :</span><span class="sxs-lookup"><span data-stu-id="f1493-232">Select **Add Students** from the **Students** menu, add a student, and then view the new student in the **Students** page to verify that you can successfully write to the database:</span></span>

[![A<span data-ttu-id="f1493-233">dd_Students_page_Test]</span><span class="sxs-lookup"><span data-stu-id="f1493-233">dd_Students_page_Test]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)

[![S<span data-ttu-id="f1493-234">tudents_page_with_new_student_Test]</span><span class="sxs-lookup"><span data-stu-id="f1493-234">tudents_page_with_new_student_Test]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)

<span data-ttu-id="f1493-235">**과정** 메뉴에서 **업데이트 크레딧**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-235">From the **Courses** menu, select **Update Credits**.</span></span> <span data-ttu-id="f1493-236">합니다 **업데이트 크레딧** 페이지에는 관리자 권한이 필요 하므로 **로그인** 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-236">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="f1493-237">이전 버전 ("admin" 및 "$w0rd Pa") 만든 관리자 계정 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-237">Enter the administrator account credentials that you created earlier ("admin" and "Pas$w0rd").</span></span> <span data-ttu-id="f1493-238">합니다 **업데이트 크레딧** 이전 자습서에서 만든 관리자 계정을 테스트 환경에 배포한 올바르게 확인 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-238">The **Update Credits** page is displayed, which verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

[![L<span data-ttu-id="f1493-239">og_In_page_Test]</span><span class="sxs-lookup"><span data-stu-id="f1493-239">og_In_page_Test]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)

[![U<span data-ttu-id="f1493-240">pdate_Credits_page_Test]</span><span class="sxs-lookup"><span data-stu-id="f1493-240">pdate_Credits_page_Test]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)

<span data-ttu-id="f1493-241">확인을 *Elmah* 폴더가 자리 표시자 파일을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-241">Verify that an *Elmah* folder exists with only the placeholder file in it.</span></span>

[![E<span data-ttu-id="f1493-242">lmah_folder_Test]</span><span class="sxs-lookup"><span data-stu-id="f1493-242">lmah_folder_Test]</span></span>(deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a><span data-ttu-id="f1493-243">Code First 마이그레이션에 대 한 자동 Web.config 변경 내용 검토</span><span class="sxs-lookup"><span data-stu-id="f1493-243">Reviewing the Automatic Web.config Changes for Code First Migrations</span></span>

<span data-ttu-id="f1493-244">엽니다는 *Web.config* 배포 된 응용 프로그램에서 파일 *C:\inetpub\wwwroot\ContosoUniversity* 여기서 배포 프로세스를 구성 하도록 Code First 마이그레이션을 자동으로 확인할 수 있습니다 최신 버전으로 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-244">Open the *Web.config* file in the deployed application at *C:\inetpub\wwwroot\ContosoUniversity* and you can see where the deployment process configured Code First Migrations to automatically update the database to the latest version.</span></span>

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

<span data-ttu-id="f1493-245">배포 프로세스는 데이터베이스 스키마 업데이트에 대 한 단독으로 사용 하도록 Code First 마이그레이션에 대 한 새 연결 문자열도 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-245">The deployment process also created a new connection string for Code First Migrations to use exclusively for updating the database schema:</span></span>

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

<span data-ttu-id="f1493-247">이 추가 연결 문자열을 사용 하면 데이터베이스 스키마 업데이트에 대 한 하나의 사용자 계정 및 응용 프로그램 데이터 액세스에 대 한 다른 사용자 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-247">This additional connection string enables you to specify one user account for database schema updates, and a different user account for application data access.</span></span> <span data-ttu-id="f1493-248">예를 들어 db를 할당할 수 있습니다\_소유자 역할의 Code First 마이그레이션 및 db\_datareader 및 db\_응용 프로그램에 datawriter 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-248">For example, you could assign the db\_owner role to Code First Migrations, and db\_datareader and db\_datawriter roles to the application.</span></span> <span data-ttu-id="f1493-249">데이터베이스 스키마 변경에서 응용 프로그램의 잠재적 악성 코드 방지 하는 일반적인 심층 방어 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-249">This is a common defense-in-depth pattern that prevents potentially malicious code in the application from changing the database schema.</span></span> <span data-ttu-id="f1493-250">(예를 들어이 발생할 수 있습니다 SQL 주입 공격에.) 이 패턴은이 자습서에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-250">(For example, this might happen in a successful SQL injection attack.) This pattern is not used by these tutorials.</span></span> <span data-ttu-id="f1493-251">SQL Server Compact에 적용 되지 않습니다 및이 시리즈의 자습서의 뒷부분에서 SQL Server로 마이그레이션하는 경우 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-251">It does not apply to SQL Server Compact, and it does not apply when you migrate to SQL Server in a later tutorial in this series.</span></span> <span data-ttu-id="f1493-252">Cytanium 사이트 Cytanium에서 만든 SQL Server 데이터베이스에 액세스 하기 위한 하나의 사용자 계정만을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-252">The Cytanium site offers just one user account for accessing the SQL Server database that you create at Cytanium.</span></span> <span data-ttu-id="f1493-253">시나리오에서이 패턴을 구현할 수 인 경우에 다음 단계를 수행 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-253">If you are able to implement this pattern in your scenario, you can do it by performing the following steps:</span></span>

1. <span data-ttu-id="f1493-254">에 **설정** 탭을 **웹 게시** 마법사는 전체 데이터베이스 스키마 업데이트 권한이 있는 사용자를 지정 하는 연결 문자열을 입력 하 고 선택을 취소는 **이 연결 문자열을 사용 하 여 런타임 시** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-254">In the **Settings** tab of the **Publish Web** wizard, enter the connection string that specifies a user with full database schema update permissions, and clear the **Use this connection string at runtime** check box.</span></span> <span data-ttu-id="f1493-255">이것이 배포 된 Web.config 파일에는 `DatabasePublish` 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-255">In the deployed Web.config file, this becomes the `DatabasePublish` connection string.</span></span>
2. <span data-ttu-id="f1493-256">응용 프로그램에서 런타임 시 사용 하는 연결 문자열에 대 한 Web.config 파일 변환을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-256">Create a Web.config file transformation for the connection string that you want the application to use at run time.</span></span>

<span data-ttu-id="f1493-257">개발 컴퓨터에서 IIS에 응용 프로그램을 배포 하 고 있는 테스트 했으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-257">You have now deployed your application to IIS on your development computer and tested it there.</span></span> <span data-ttu-id="f1493-258">배포 프로세스 (배포 되지 않은 하려는 파일 제외) 오른쪽 위치에 응용 프로그램의 콘텐츠를 복사 하 고 또한 웹 배포는 IIS 구성 올바르게 배포 하는 동안 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-258">This verifies that the deployment process copied the application's content to the right location (excluding the files that you did not want to deploy), and also that Web Deploy configured IIS correctly during deployment.</span></span> <span data-ttu-id="f1493-259">다음 자습서에서는 아직 수행 하지 않은 배포 작업을 발견 하는 하나 이상의 테스트 실행:에 대해 폴더 사용 권한을 설정 합니다 *Elmah* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-259">In the next tutorial, you'll run one more test that finds a deployment task that has not yet been done: setting folder permissions on the *Elmah* folder.</span></span>

## <a name="more-information"></a><span data-ttu-id="f1493-260">추가 정보</span><span class="sxs-lookup"><span data-stu-id="f1493-260">More Information</span></span>

<span data-ttu-id="f1493-261">Visual Studio에서 IIS 또는 IIS Express를 실행 하는 방법에 대 한 내용은 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-261">For information about running IIS or IIS Express in Visual Studio, see the following resources:</span></span>

- <span data-ttu-id="f1493-262">[IIS Express 개요](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) IIS.net 사이트의.</span><span class="sxs-lookup"><span data-stu-id="f1493-262">[IIS Express Overview](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) on the IIS.net site.</span></span>
- <span data-ttu-id="f1493-263">[IIS Express 소개](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie의 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-263">[Introducing IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) on Scott Guthrie's blog.</span></span>
- <span data-ttu-id="f1493-264">[방법: Visual Studio에서 웹 프로젝트에 대 한 웹 서버를 지정](https://msdn.microsoft.com/library/ms178108.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-264">[How to: Specify the Web Server for Web Projects in Visual Studio](https://msdn.microsoft.com/library/ms178108.aspx).</span></span>
- <span data-ttu-id="f1493-265">[코어 IIS 간의 차이점 및 ASP.NET Development Server](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) ASP.NET 사이트의.</span><span class="sxs-lookup"><span data-stu-id="f1493-265">[Core Differences Between IIS and the ASP.NET Development Server](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) on the ASP.NET site.</span></span>
- <span data-ttu-id="f1493-266">[30 초 내에서에 ASP.NET MVC 또는 Web Forms 응용 프로그램 IIS 7에서 테스트](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx) Rick Anderson의 블로그에서입니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-266">[Test your ASP.NET MVC or Web Forms Application on IIS 7 in 30 seconds](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx) on Rick Anderson's blog.</span></span> <span data-ttu-id="f1493-267">이 항목의 Visual Studio 개발 서버 (Cassini)를 사용 하 여 테스트 수 없는 이유 IIS Express에서 테스트 하는 것 만큼 신뢰성이 이며 왜 IIS Express에서 테스트 하지 IIS에서 테스트 하는 것 만큼 신뢰성이 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-267">This entry provides examples of why testing with the Visual Studio Development Server (Cassini) is not as reliable as testing in IIS Express, and why testing in IIS Express is not as reliable as testing in IIS.</span></span>

<span data-ttu-id="f1493-268">어떤 문제에 대 한 정보는 보통 신뢰 수준에서 응용 프로그램을 실행 하는 경우에 발생할 수, 참조 [보통 신뢰에서 ASP.NET 응용 프로그램 호스팅](http://www.4guysfromrolla.com/articles/100307-1.aspx) Rolla 사이트에서 4 Guys에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1493-268">For information about what issues might arise when your application runs in medium trust, see [Hosting ASP.NET Applications in Medium Trust](http://www.4guysfromrolla.com/articles/100307-1.aspx) on the 4 Guys from Rolla site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f1493-269">[이전](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
> [다음](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="f1493-269">[Previous](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
[Next](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)</span></span>
