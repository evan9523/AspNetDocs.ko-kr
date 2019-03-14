---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: ASP.NET Web API 2 Azure 작업자 역할에 호스트 | Microsoft Docs
author: MikeWasson
description: 이 자습서에 OWIN을 사용 하 여 Web API 프레임 워크 자체 호스트 하는 Azure 작업자 역할에서 ASP.NET Web API를 호스트 하는 방법을 보여줍니다. .NET (OWIN) 독일에 대 한 open Web Interface...
ms.author: riande
ms.date: 04/02/2014
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 40cb1a4514beaf81e7ed75bbd3e478f2ba146fe5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063920"
---
<a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="202dc-104">ASP.NET Web API 2 Azure 작업자 역할에서 호스트</span><span class="sxs-lookup"><span data-stu-id="202dc-104">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>
====================
<span data-ttu-id="202dc-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="202dc-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="202dc-106">이 자습서에 OWIN을 사용 하 여 Web API 프레임 워크 자체 호스트 하는 Azure 작업자 역할에서 ASP.NET Web API를 호스트 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-106">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="202dc-107">[Open Web Interface for.NET](http://owin.org/) (OWIN).NET 웹 서버 및 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="202dc-108">이상적인 OWIN 자체 IIS 외부에서 사용자 고유의 프로세스에서 웹 응용 프로그램을 호스팅하는 서버에서 웹 응용 프로그램을 분리 하는 OWIN – Azure 작업자 역할 내에서 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="202dc-109">이 자습서에서는 Microsoft.Owin.Host.HttpListener 패키지 자체 OWIN 응용 프로그램을 호스팅하는 데 사용 하는 HTTP 서버를 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-109">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="202dc-110">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="202dc-110">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="202dc-111">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="202dc-111">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="202dc-112">Web API 2</span><span class="sxs-lookup"><span data-stu-id="202dc-112">Web API 2</span></span>
> - [<span data-ttu-id="202dc-113">Azure SDK for.NET 2.3</span><span class="sxs-lookup"><span data-stu-id="202dc-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)


## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="202dc-114">Microsoft Azure 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="202dc-114">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="202dc-115">관리자 권한으로 Visual Studio를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-115">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="202dc-116">Azure 계산 에뮬레이터를 사용 하 여 응용 프로그램을 로컬로 디버깅 하려면 관리자 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-116">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="202dc-117">에 **파일** 메뉴에서 클릭 **새로 만들기**, 클릭 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-117">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="202dc-118">**설치 된 템플릿**, Visual C#에서 클릭 **클라우드** 을 클릭 한 다음 **Windows Azure 클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-118">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="202dc-119">"AzureApp" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-119">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="202dc-120">에 **새 Windows Azure 클라우드 서비스** 대화 상자에서 두 번 클릭 **작업자 역할**입니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-120">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="202dc-121">기본 이름 ("WorkerRole1")을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-121">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="202dc-122">이 단계에서는 솔루션에 작업자 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-122">This step adds a worker role to the solution.</span></span> <span data-ttu-id="202dc-123">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-123">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="202dc-124">만든 Visual Studio 솔루션에는 두 개의 프로젝트가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-124">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="202dc-125">&quot;AzureApp&quot; 역할 및 Azure 응용 프로그램에 대 한 구성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-125">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="202dc-126">&quot;WorkerRole1&quot; 작업자 역할에 대 한 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-126">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="202dc-127">일반적으로 Azure 응용 프로그램을이 자습서에서는 단일 역할을 사용 하 여 여러 역할을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-127">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="202dc-128">웹 API 및 OWIN 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-128">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="202dc-129">**도구** 메뉴에서 클릭 **NuGet 패키지 관리자**, 클릭 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-129">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="202dc-130">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-130">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="202dc-131">HTTP 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="202dc-131">Add an HTTP Endpoint</span></span>

<span data-ttu-id="202dc-132">솔루션 탐색기에서 AzureApp 프로젝트를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-132">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="202dc-133">역할 노드를 확장, WorkerRole1를 마우스 오른쪽 단추로 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-133">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="202dc-134">클릭 **끝점**를 클릭 하 고 **끝점 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-134">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="202dc-135">에 **프로토콜** 드롭다운 목록에서 "http"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-135">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="202dc-136">**공용 포트** 하 고 **개인 포트**, 80을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-136">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="202dc-137">이러한 포트 번호는 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-137">These port numbers can be different.</span></span> <span data-ttu-id="202dc-138">공용 포트는 클라이언트 역할에 요청을 보낼 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-138">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="202dc-139">웹 API에 대 한 구성 자체 호스트</span><span class="sxs-lookup"><span data-stu-id="202dc-139">Configure Web API for Self-Host</span></span>

<span data-ttu-id="202dc-140">솔루션 탐색기에서 WorkerRole1 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** / **클래스** 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-140">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="202dc-141">클래스 이름을 `Startup`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-141">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="202dc-142">모두이 파일의 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-142">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="202dc-143">웹 API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="202dc-143">Add a Web API Controller</span></span>

<span data-ttu-id="202dc-144">다음으로, Web API 컨트롤러 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-144">Next, add a Web API controller class.</span></span> <span data-ttu-id="202dc-145">WorkerRole1 프로젝트를 마우스 오른쪽 단추로 누르고 **추가** / **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-145">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="202dc-146">TestController 클래스를 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-146">Name the class TestController.</span></span> <span data-ttu-id="202dc-147">모두이 파일의 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-147">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="202dc-148">편의상이 컨트롤러 방금 일반 텍스트를 반환 하는 두 개의 GET 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-148">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="202dc-149">OWIN 호스트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-149">Start the OWIN Host</span></span>

<span data-ttu-id="202dc-150">WorkerRole.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-150">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="202dc-151">이 클래스는 작업자 역할은 시작 및 중지 될 때 실행 되는 코드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-151">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="202dc-152">다음 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="202dc-152">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="202dc-153">추가 된 **IDisposable** 멤버는 `WorkerRole` 클래스:</span><span class="sxs-lookup"><span data-stu-id="202dc-153">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="202dc-154">에 `OnStart` 메서드를 호스트 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-154">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="202dc-155">합니다 **WebApp.Start** 메서드 OWIN 호스트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-155">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="202dc-156">이름을 합니다 `Startup` 클래스는 메서드 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-156">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="202dc-157">호스트는 호출 규칙에 따라는 `Configure` 이 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="202dc-157">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="202dc-158">재정의 된 `OnStop` 삭제 하는  *\_앱* 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="202dc-158">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="202dc-159">WorkerRole.cs의 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-159">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="202dc-160">솔루션을 빌드하고 f5 키를 눌러 Azure Compute 에뮬레이터에서 응용 프로그램을 로컬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-160">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="202dc-161">방화벽 설정에 따라 방화벽을 통해 에뮬레이터를 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-161">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="202dc-162">다음과 같은 예외를 표시 하는 경우를 참조 하세요 [이 블로그 게시물](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) 해결 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-162">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="202dc-163">"파일이 나 어셈블리를 로드할 수 없습니다 ' Microsoft.Owin, 버전 2.0.2.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 =' 또는 해당 종속성 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-163">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="202dc-164">찾은 어셈블리의 매니페스트 정의가 어셈블리 참조를 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-164">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="202dc-165">(예외가 발생한 HRESULT: 0x80131040)"</span><span class="sxs-lookup"><span data-stu-id="202dc-165">(Exception from HRESULT: 0x80131040)"</span></span>


<span data-ttu-id="202dc-166">계산 에뮬레이터는 로컬 IP 주소를 끝점에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-166">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="202dc-167">Compute 에뮬레이터 UI를 확인 하 여 IP 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-167">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="202dc-168">작업 표시줄 알림 영역에서에서 에뮬레이터 아이콘을 마우스 오른쪽 단추로 누르고 **Compute 에뮬레이터 UI 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-168">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="202dc-169">배포 서비스 배포 [id], 서비스 세부 정보 아래에서 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-169">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="202dc-170">웹 브라우저를 열고 http:// 이동할<em>주소</em>/테스트/1, 여기서 <em>주소</em> 계산 에뮬레이터에서 할당 한 IP 주소는 예를 들어 `http://127.0.0.1:80/test/1`합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-170">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="202dc-171">Web API 컨트롤러에서 응답이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-171">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="202dc-172">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="202dc-172">Deploy to Azure</span></span>

<span data-ttu-id="202dc-173">이 단계에서는 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-173">For this step, you must have an Azure account.</span></span> <span data-ttu-id="202dc-174">아직 없다면, 몇 분만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-174">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="202dc-175">자세한 내용은 참조 하세요 [Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-175">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="202dc-176">솔루션 탐색기에서 AzureApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-176">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="202dc-177">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-177">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="202dc-178">Azure 계정에 로그인 하지 않은 경우 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-178">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="202dc-179">에 로그인 한 후 구독을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-179">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="202dc-180">클라우드 서비스에 대 한 이름을 입력 하 고 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-180">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="202dc-181">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-181">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="202dc-182">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-182">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="202dc-183">Azure 활동 로그 창에 배포 진행률이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-183">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="202dc-184">앱을 배포할 때 이동할 http://appname.cloudapp.net/test/1합니다.</span><span class="sxs-lookup"><span data-stu-id="202dc-184">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="202dc-185">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="202dc-185">Additional Resources</span></span>

- [<span data-ttu-id="202dc-186">프로젝트 Katana 개요</span><span class="sxs-lookup"><span data-stu-id="202dc-186">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="202dc-187">Katana Project on GitHub</span><span class="sxs-lookup"><span data-stu-id="202dc-187">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
