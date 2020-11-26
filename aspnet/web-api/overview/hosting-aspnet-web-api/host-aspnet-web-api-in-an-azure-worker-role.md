---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Azure 작업자 역할의 호스트 ASP.NET Web API 2-ASP.NET 4.x
author: MikeWasson
description: '자습서: OWIN를 사용 하 여 Web API 프레임 워크를 자체 호스트 하는 Azure 작업자 역할의 ASP.NET Web API를 호스팅합니다.'
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 06bd33a7d30ab38d851d929d72ae8c539e16873c
ms.sourcegitcommit: 4b78855427f1397df0a7be3559e04ec94a78c308
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96151908"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="15532-103">Azure 작업자 역할의 호스트 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="15532-103">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>

<span data-ttu-id="15532-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="15532-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="15532-105">이 자습서에서는 OWIN를 사용 하 여 Web API 프레임 워크를 자체 호스트 하는 Azure 작업자 역할의 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15532-105">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="15532-106">OWIN ( [Open Web Interface for .net](http://owin.org/) )는 .net 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-106">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="15532-107">OWIN는 서버에서 웹 응용 프로그램을 분리 하 여 IIS 외부 (예: Azure 작업자 역할 내부)에서 웹 응용 프로그램을 자체 호스트 하는 데 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="15532-108">이 자습서에서는 OWIN 응용 프로그램을 자체 호스트 하는 데 사용 되는 HTTP 서버를 제공 하는 Owin HttpListener 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-108">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="15532-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="15532-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="15532-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="15532-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="15532-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="15532-111">Web API 2</span></span>
> - [<span data-ttu-id="15532-112">Azure SDK for .NET 2.3</span><span class="sxs-lookup"><span data-stu-id="15532-112">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="15532-113">Microsoft Azure 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="15532-113">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="15532-114">관리자 권한으로 Visual Studio를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-114">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="15532-115">Azure 계산 에뮬레이터를 사용 하 여 응용 프로그램을 로컬로 디버깅 하려면 관리자 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-115">Administrator privileges are needed to debug the application locally, using the Azure Compute Emulator.</span></span>

<span data-ttu-id="15532-116">**파일** 메뉴에서 **새로 만들기** 를 클릭 한 다음 **프로젝트** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-116">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="15532-117">**설치 된 템플릿** 의 Visual c # 아래에서 **클라우드** 를 클릭 한 다음 **Windows Azure 클라우드 서비스** 를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-117">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="15532-118">프로젝트 이름을 "AzureApp"으로 선택 하 고 **확인** 을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-118">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="15532-119">**새 Windows Azure 클라우드 서비스** 대화 상자에서 **작업자 역할** 을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-119">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="15532-120">기본 이름 ("WorkerRole1")을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="15532-120">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="15532-121">이 단계에서는 솔루션에 작업자 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-121">This step adds a worker role to the solution.</span></span> <span data-ttu-id="15532-122">**확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-122">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="15532-123">생성 되는 Visual Studio 솔루션에는 두 개의 프로젝트가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15532-123">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="15532-124">&quot;AzureApp은 &quot; Azure 응용 프로그램에 대 한 역할 및 구성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-124">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="15532-125">&quot;WorkerRole1에는 &quot; 작업자 역할에 대 한 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15532-125">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="15532-126">일반적으로이 자습서에서는 단일 역할을 사용 하지만 Azure 응용 프로그램에는 여러 역할이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15532-126">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="15532-127">Web API 및 OWIN 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="15532-127">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="15532-128">**도구** 메뉴에서 **NuGet 패키지 관리자** 를 클릭 한 다음 **패키지 관리자 콘솔** 을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-128">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="15532-129">패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-129">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="15532-130">HTTP 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="15532-130">Add an HTTP Endpoint</span></span>

<span data-ttu-id="15532-131">솔루션 탐색기에서 AzureApp 프로젝트를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-131">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="15532-132">역할 노드를 확장 하 고 WorkerRole1를 마우스 오른쪽 단추로 클릭 한 다음 **속성** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-132">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="15532-133">**엔드포인트** 를 클릭한 다음, **엔드포인트 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-133">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="15532-134">**프로토콜** 드롭다운 목록에서 "http"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-134">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="15532-135">**공용 포트** 및 **개인 포트** 에 80을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-135">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="15532-136">이러한 포트 번호는 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15532-136">These port numbers can be different.</span></span> <span data-ttu-id="15532-137">공용 포트는 역할에 요청을 보낼 때 클라이언트에서 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15532-137">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="15532-138">Self-Host 웹 API 구성</span><span class="sxs-lookup"><span data-stu-id="15532-138">Configure Web API for Self-Host</span></span>

<span data-ttu-id="15532-139">솔루션 탐색기에서 WorkerRole1 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**  /  **클래스** 를 선택 하 여 새 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-139">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="15532-140">클래스 `Startup` 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-140">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="15532-141">이 파일의 모든 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="15532-141">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="15532-142">Web API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="15532-142">Add a Web API Controller</span></span>

<span data-ttu-id="15532-143">그런 다음 웹 API 컨트롤러 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-143">Next, add a Web API controller class.</span></span> <span data-ttu-id="15532-144">WorkerRole1 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클래스 **추가** 를 선택  /  **Class** 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-144">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="15532-145">TestController 클래스의 이름을로 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-145">Name the class TestController.</span></span> <span data-ttu-id="15532-146">이 파일의 모든 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="15532-146">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="15532-147">편의상이 컨트롤러는 일반 텍스트를 반환 하는 두 개의 GET 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-147">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="15532-148">OWIN 호스트 시작</span><span class="sxs-lookup"><span data-stu-id="15532-148">Start the OWIN Host</span></span>

<span data-ttu-id="15532-149">WorkerRole.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15532-149">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="15532-150">이 클래스는 작업자 역할이 시작 및 중지 될 때 실행 되는 코드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-150">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="15532-151">다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-151">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="15532-152">클래스에 **IDisposable** 멤버를 추가 합니다 `WorkerRole` .</span><span class="sxs-lookup"><span data-stu-id="15532-152">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="15532-153">`OnStart`메서드에서 호스트를 시작 하는 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-153">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="15532-154">**WebApp** 메서드는 OWIN 호스트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-154">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="15532-155">클래스의 이름은 `Startup` 메서드의 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="15532-155">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="15532-156">규칙에 따라 호스트는 `Configure` 이 클래스의 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-156">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="15532-157">`OnStop` *\_ 앱* 인스턴스를 삭제 하려면를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-157">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="15532-158">WorkerRole.cs에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15532-158">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="15532-159">솔루션을 빌드하고 F5 키를 눌러 Azure 계산 에뮬레이터에서 응용 프로그램을 로컬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-159">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="15532-160">방화벽 설정에 따라 에뮬레이터를 방화벽을 통해 허용 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15532-160">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="15532-161">다음과 같은 예외가 발생 하는 경우 해결 방법은 [이 블로그 게시물](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="15532-161">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="15532-162">"파일 또는 어셈블리 ' Owin, Version = 2.0.2.0, Culture = 중립, PublicKeyToken = 31bf3856ad364e35 ' 또는 해당 종속성 중 하나를 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15532-162">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="15532-163">찾은 어셈블리의 매니페스트 정의가 어셈블리 참조와 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15532-163">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="15532-164">(HRESULT의 예외: 0x80131040) "</span><span class="sxs-lookup"><span data-stu-id="15532-164">(Exception from HRESULT: 0x80131040)"</span></span>

<span data-ttu-id="15532-165">계산 에뮬레이터는 끝점에 로컬 IP 주소를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-165">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="15532-166">계산 에뮬레이터 UI를 확인 하 여 IP 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15532-166">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="15532-167">작업 표시줄 알림 영역에서 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **계산 에뮬레이터 UI 표시** 를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-167">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="15532-168">서비스 배포, 배포 [id], 서비스 세부 정보에서 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="15532-168">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="15532-169">웹 브라우저를 열고 http://<em>address</em>/test/1로 이동 합니다. 여기서 <em>address</em> 는 계산 에뮬레이터에서 할당 한 IP 주소입니다. 예를 들면 `http://127.0.0.1:80/test/1` 입니다.</span><span class="sxs-lookup"><span data-stu-id="15532-169">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="15532-170">웹 API 컨트롤러에서 응답이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-170">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="15532-171">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="15532-171">Deploy to Azure</span></span>

<span data-ttu-id="15532-172">이 단계에서는 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-172">For this step, you must have an Azure account.</span></span> <span data-ttu-id="15532-173">아직 없는 경우 몇 분만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15532-173">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="15532-174">자세한 내용은 [Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="15532-174">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="15532-175">솔루션 탐색기에서 AzureApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-175">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="15532-176">**게시** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-176">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="15532-177">Azure 계정에 로그인 하지 않은 경우 **로그인** 을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-177">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="15532-178">로그인 한 후 구독을 선택 하 고 **다음** 을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-178">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="15532-179">클라우드 서비스의 이름을 입력 하 고 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-179">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="15532-180">**만들기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-180">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="15532-181">**게시** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-181">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="15532-182">Azure 활동 로그 창에는 배포 진행률이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15532-182">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="15532-183">앱이 배포 되 면로 이동 http://appname.cloudapp.net/test/1 합니다.</span><span class="sxs-lookup"><span data-stu-id="15532-183">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="15532-184">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="15532-184">Additional Resources</span></span>

- [<span data-ttu-id="15532-185">프로젝트 Katana 개요</span><span class="sxs-lookup"><span data-stu-id="15532-185">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="15532-186">GitHub의 Katana 프로젝트</span><span class="sxs-lookup"><span data-stu-id="15532-186">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
