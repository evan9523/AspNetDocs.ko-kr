---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: Azure Service Bus로 SignalR 규모 확장 (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: cab185ccb048a374a08f4b5d978b30675c30a60d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59383965"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a><span data-ttu-id="8c993-102">Azure Service Bus로 SignalR 규모 확장(SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="8c993-102">SignalR Scaleout with Azure Service Bus (SignalR 1.x)</span></span>

<span data-ttu-id="8c993-103">하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="8c993-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="8c993-104">이 자습서에서는 Service Bus 백플레인에서 사용 하 여 각 역할 인스턴스에 메시지를 분산 하는 Windows Azure 웹 역할에는 SignalR 응용 프로그램 배포.</span><span class="sxs-lookup"><span data-stu-id="8c993-104">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="8c993-105">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="8c993-105">Prerequisites:</span></span>

- <span data-ttu-id="8c993-106">Windows Azure 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-106">A Windows Azure account.</span></span>
- <span data-ttu-id="8c993-107">합니다 [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-107">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="8c993-108">Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="8c993-108">Visual Studio 2012.</span></span>

<span data-ttu-id="8c993-109">Service bus 백플레인에서 호환 이기도 [Windows Server 용 Service Bus](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), 버전 1.1입니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-109">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="8c993-110">그러나 Service Bus for Windows Server의 버전 1.0과 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-110">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="8c993-111">가격</span><span class="sxs-lookup"><span data-stu-id="8c993-111">Pricing</span></span>

<span data-ttu-id="8c993-112">Service Bus 백플레인에서 메시지를 보낼 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-112">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="8c993-113">최신 가격 정보 참조 [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-113">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="8c993-114">이 문서 작성 당시 1 달러 미만 매월 1,000,000 개의 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-114">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="8c993-115">백플레인에서는 SignalR 허브 메서드에 대 한 각 호출에 대 한 service bus 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-115">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="8c993-116">일부 제어 메시지 등에 대 한 연결, 연결 끊김, 조인 또는 그대로 유지 되어 그룹도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-116">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="8c993-117">대부분의 응용 프로그램에서 대부분의 메시지 트래픽 허브 메서드 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-117">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="8c993-118">개요</span><span class="sxs-lookup"><span data-stu-id="8c993-118">Overview</span></span>

<span data-ttu-id="8c993-119">자세한 자습서를 시작 하기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-119">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="8c993-120">새 Service Bus 네임 스페이스를 만들려면 Windows Azure 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-120">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="8c993-121">응용 프로그램에 이러한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-121">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="8c993-122">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="8c993-122">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="8c993-123">Microsoft.AspNet.SignalR.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="8c993-123">Microsoft.AspNet.SignalR.ServiceBus</span></span>](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. <span data-ttu-id="8c993-124">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-124">Create a SignalR application.</span></span>
4. <span data-ttu-id="8c993-125">Global.asax 백플레인에서 구성 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-125">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="8c993-126">각 응용 프로그램에 대 한 "응용 프로그램 이름"에 대 한 다른 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-126">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="8c993-127">여러 응용 프로그램에서 동일한 값을 사용 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8c993-127">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="8c993-128">Azure 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="8c993-128">Create the Azure Services</span></span>

<span data-ttu-id="8c993-129">에 설명 된 대로 클라우드 서비스를 만듭니다 [클라우드 서비스 만들기 및 배포 하는 방법을](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-129">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="8c993-130">섹션의 단계에 따라 "방법: 빠른 생성을 사용 하 여 클라우드 서비스를 만들기 "입니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-130">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="8c993-131">이 자습서에서는 인증서를 업로드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-131">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="8c993-132">에 설명 된 대로 새 Service Bus 네임 스페이스를 만듭니다 [방법을 사용 하 여 Service Bus 토픽/구독에](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)입니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-132">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="8c993-133">"서비스 Namespace 만들기" 섹션의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-133">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="8c993-134">클라우드 서비스 및 Service Bus 네임 스페이스에 대 한 동일한 지역을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-134">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>


## <a name="create-the-visual-studio-project"></a><span data-ttu-id="8c993-135">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="8c993-135">Create the Visual Studio Project</span></span>

<span data-ttu-id="8c993-136">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-136">Start Visual Studio.</span></span> <span data-ttu-id="8c993-137">**파일** 메뉴에서 클릭 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-137">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="8c993-138">에 **새 프로젝트** 대화 상자에서 **Visual C#** 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-138">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="8c993-139">아래 **설치 된 템플릿**를 선택 **클라우드** 선택한 후 **Windows Azure 클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-139">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="8c993-140">기본.NET Framework 4.5를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-140">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="8c993-141">ChatService 응용 프로그램 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-141">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="8c993-142">에 **새 Windows Azure 클라우드 서비스** 대화 상자에서 ASP.NET MVC 4 웹 역할 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-142">In the **New Windows Azure Cloud Service** dialog, select ASP.NET MVC 4 Web Role.</span></span> <span data-ttu-id="8c993-143">오른쪽 화살표 단추를 클릭 (**&gt;**) 솔루션에 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-143">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="8c993-144">따라서 새 역할 위로 마우스를 이동 연필 아이콘을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-144">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="8c993-145">역할 이름을 바꾸려면이 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-145">Click this icon to rename the role.</span></span> <span data-ttu-id="8c993-146">"SignalRChat" 역할 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-146">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="8c993-147">에 **새 ASP.NET MVC 4 프로젝트** 마법사 **인터넷 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-147">In the **New ASP.NET MVC 4 Project** wizard, select **Internet Application**.</span></span> <span data-ttu-id="8c993-148">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-148">Click **OK**.</span></span> <span data-ttu-id="8c993-149">프로젝트 마법사에서 두 개의 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-149">The project wizard creates two projects:</span></span>

- <span data-ttu-id="8c993-150">ChatService: 이 프로젝트는 Windows Azure 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-150">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="8c993-151">Azure 역할 및 기타 구성 옵션을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-151">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="8c993-152">SignalRChat: 이 프로젝트는 ASP.NET MVC 4 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-152">SignalRChat: This project is your ASP.NET MVC 4 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="8c993-153">SignalR 채팅 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="8c993-153">Create the SignalR Chat Application</span></span>

<span data-ttu-id="8c993-154">채팅 응용 프로그램을 만들려면이 자습서의 단계를 따라 [SignalR 및 MVC 4 시작](tutorial-getting-started-with-signalr-and-mvc-4.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-154">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="8c993-155">필요한 라이브러리를 설치 하려면 NuGet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-155">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="8c993-156">**도구** 메뉴에서 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-156">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="8c993-157">에 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-157">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="8c993-158">사용 된 `-ProjectName` Windows Azure 프로젝트 보다는 ASP.NET MVC 프로젝트에 패키지를 설치 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-158">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="8c993-159">백플레인에서 구성</span><span class="sxs-lookup"><span data-stu-id="8c993-159">Configure the Backplane</span></span>

<span data-ttu-id="8c993-160">응용 프로그램의 Global.asax 파일에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-160">In your application's Global.asax file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="8c993-161">이제 service bus 연결 문자열 가져오기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-161">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="8c993-162">Azure portal에서 만든 service bus 네임 스페이스를 선택 하 고 액세스 키 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-162">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="8c993-163">연결 문자열을 클립보드에 복사한 다음 붙여 넣습니다 합니다 *connectionString* 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-163">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="8c993-164">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="8c993-164">Deploy to Azure</span></span>

<span data-ttu-id="8c993-165">솔루션 탐색기에서 확장을 **역할** ChatService 프로젝트 내부 폴더.</span><span class="sxs-lookup"><span data-stu-id="8c993-165">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

<span data-ttu-id="8c993-166">SignalRChat 역할을 마우스 오른쪽 단추로 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-166">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="8c993-167">**구성** 탭을 선택합니다. 아래 **인스턴스** 2를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-167">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="8c993-168">VM 크기 설정할 수도 있습니다 **작음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-168">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="8c993-169">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-169">Save the changes.</span></span>

<span data-ttu-id="8c993-170">솔루션 탐색기에서 ChatService 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-170">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="8c993-171">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-171">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="8c993-172">Windows Azure에 첫 번째 시간 게시 인 경우 자격 증명을 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-172">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="8c993-173">에 **게시** 마법사 "자격 증명을 다운로드 하려면 로그인"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-173">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="8c993-174">Windows Azure 포털에 로그인 하 고 게시 설정 파일을 다운로드 하 라는 메시지가 나타납니다이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-174">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="8c993-175">클릭 **가져오기** 다운로드 한 게시 설정 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-175">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="8c993-176">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-176">Click **Next**.</span></span> <span data-ttu-id="8c993-177">에 **게시 설정** 대화 상자 아래에 있는 **클라우드 서비스**, 앞에서 만든 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-177">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="8c993-178">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-178">Click **Publish**.</span></span> <span data-ttu-id="8c993-179">응용 프로그램을 배포 하 고 Vm을 시작 하려면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-179">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="8c993-180">지금 채팅 응용 프로그램을 실행 하는 경우 역할 인스턴스가 Service Bus 토픽을 사용 하 여 Azure Service Bus를 통해 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-180">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="8c993-181">항목은 여러 구독자를 허용 하는 메시지 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-181">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="8c993-182">백플레인에서 항목 및 구독에 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-182">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="8c993-183">구독 및 메시지 작업을 보려면 Azure portal을 열고 Service Bus 네임 스페이스를 선택한 "항목"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-183">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="8c993-184">메시지 작업 대시보드에 표시 되는 데 몇 분 정도 걸릴 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-184">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="8c993-185">SignalR 항목 수명을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c993-185">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="8c993-186">응용 프로그램 배포는 수동으로 항목을 삭제 하거나 해당 항목에 대 한 설정을 변경 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8c993-186">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>
