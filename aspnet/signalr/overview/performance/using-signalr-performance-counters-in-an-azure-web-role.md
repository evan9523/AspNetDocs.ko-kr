---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Azure 웹 역할에서 SignalR 성능 카운터 사용 | Microsoft Docs
author: guardrex
description: Azure 웹 역할에서 SignalR 성능 카운터를 설치 하 고 사용 하는 방법입니다.
keywords: ASP.NET, signalr, 성능 카운터, azure 웹 역할
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240641"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a><span data-ttu-id="b4c1e-104">Azure 웹 역할에서 SignalR 성능 카운터 사용</span><span class="sxs-lookup"><span data-stu-id="b4c1e-104">Using SignalR performance counters in an Azure Web Role</span></span>

<span data-ttu-id="b4c1e-105">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="b4c1e-105">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="b4c1e-106">SignalR 성능 카운터는 Azure 웹 역할에서 앱의 성능을 모니터링 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-106">SignalR performance counters are used to monitor your app's performance in an Azure Web Role.</span></span> <span data-ttu-id="b4c1e-107">카운터는 Microsoft Azure 진단에 의해 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-107">The counters are captured by Microsoft Azure Diagnostics.</span></span> <span data-ttu-id="b4c1e-108">독립 실행형 또는 온-프레미스 앱에 사용 되는 동일한 도구인 *signalr.exe*를 사용 하 여 Azure에 SignalR 성능 카운터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-108">You install SignalR performance counters on Azure with *signalr.exe*, the same tool used for standalone or on-premises apps.</span></span> <span data-ttu-id="b4c1e-109">Azure 역할은 일시적 이므로 시작 시 SignalR 성능 카운터를 설치 하 고 등록 하도록 앱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-109">Since Azure roles are transient, you configure an app to install and register SignalR performance counters upon startup.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4c1e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b4c1e-110">Prerequisites</span></span>

* <span data-ttu-id="b4c1e-111">Visual Studio 2015 또는 [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span><span class="sxs-lookup"><span data-stu-id="b4c1e-111">Visual Studio 2015 or [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span></span>
* <span data-ttu-id="b4c1e-112">[MICROSOFT AZURE sdk For Visual Studio](https://azure.microsoft.com/downloads/) **참고: sdk를 설치한 후 컴퓨터를 다시 시작 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b4c1e-112">[Microsoft Azure SDK for Visual Studio](https://azure.microsoft.com/downloads/) **Note: Restart your machine after installing the SDK.**</span></span>
* <span data-ttu-id="b4c1e-113">Microsoft Azure 구독: 무료 Azure 평가판 계정에 등록 하려면 [Azure 무료 평가판](https://azure.microsoft.com/free/dotnet/)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-113">Microsoft Azure subscription: To sign up for a free Azure trial account, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a><span data-ttu-id="b4c1e-114">SignalR 성능 카운터를 노출 하는 Azure 웹 역할 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b4c1e-114">Creating an Azure Web Role application that exposes SignalR performance counters</span></span>

1. <span data-ttu-id="b4c1e-115">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-115">Open Visual Studio.</span></span>

2. <span data-ttu-id="b4c1e-116">Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-116">In Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="b4c1e-117">**새 프로젝트** 대화 상자의 왼쪽에서 **Visual c #**  >  **클라우드** 범주를 선택 하 고 **Azure 클라우드 서비스** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-117">In the **New Project** dialog box, select the **Visual C#** > **Cloud** category on the left, and then select the **Azure Cloud Service** template.</span></span> <span data-ttu-id="b4c1e-118">앱 이름을 **SignalRPerfCounters** 로 선택 하 고 **확인을**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-118">Name the app **SignalRPerfCounters** and select **OK**.</span></span>

   ![새 클라우드 응용 프로그램](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > <span data-ttu-id="b4c1e-120">**클라우드** 템플릿 범주나 **azure 클라우드 서비스** 템플릿이 표시 되지 않는 경우 Visual Studio 2017에 대 한 **azure 개발** 워크 로드를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-120">If you don't see the **Cloud** template category or the **Azure Cloud Service** template, you need to install the **Azure development** workload for Visual Studio 2017.</span></span> <span data-ttu-id="b4c1e-121">**새 프로젝트** 대화 상자의 왼쪽 아래에 있는 **Visual Studio 설치 관리자 열기** 링크를 선택 하 여 Visual Studio 설치 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-121">Choose the **Open Visual Studio Installer** link on the bottom-left side of the **New Project** dialog to open Visual Studio Installer.</span></span> <span data-ttu-id="b4c1e-122">**Azure 개발** 워크 로드를 선택한 다음 **수정** 을 선택 하 여 워크 로드 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-122">Select the **Azure development** workload, and then choose **Modify** to start installing the workload.</span></span>
   >
   > ![Visual Studio 설치 관리자의 Azure 개발 워크 로드](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. <span data-ttu-id="b4c1e-124">**새 Microsoft Azure 클라우드 서비스** 대화 상자에서 **ASP.NET 웹 역할** 을 선택 하 고 > 단추를 선택 하 여 프로젝트에 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-124">In the **New Microsoft Azure Cloud Service** dialog, select **ASP.NET Web Role** and select the > button to add the role to the project.</span></span> <span data-ttu-id="b4c1e-125">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-125">Select **OK**.</span></span>

   ![ASP.NET 웹 역할 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. <span data-ttu-id="b4c1e-127">**New ASP.NET 웹 응용 프로그램-WebRole1** 대화 상자에서 **MVC** 템플릿을 선택 하 고 **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-127">In the **New ASP.NET Web Application - WebRole1** dialog, select the **MVC** template, and then select **OK**.</span></span>

   ![MVC 및 Web API 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. <span data-ttu-id="b4c1e-129">**솔루션 탐색기**에서 **WebRole1**아래에 있는 *diagnostics.wadcfgx* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-129">In **Solution Explorer**, open the *diagnostics.wadcfgx* file under **WebRole1**.</span></span>

   ![솔루션 탐색기 diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. <span data-ttu-id="b4c1e-131">파일의 내용을 다음 구성으로 바꾸고 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-131">Replace the contents of the file with the following configuration and save the file:</span></span>

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. <span data-ttu-id="b4c1e-132">**도구**NuGet 패키지 관리자에서 **패키지 관리자 콘솔** 을 엽니다  >  **NuGet Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-132">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="b4c1e-133">다음 명령을 입력 하 여 최신 버전의 SignalR 및 SignalR 유틸리티 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-133">Enter the following commands to install the latest version of SignalR and the SignalR utilities package:</span></span>

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. <span data-ttu-id="b4c1e-134">SignalR 성능 카운터를 시작 하거나 재생할 때 역할 인스턴스에 설치 하도록 앱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-134">Configure the app to install the SignalR performance counters into the role instance when it starts up or recycles.</span></span> <span data-ttu-id="b4c1e-135">**솔루션 탐색기**에서 **WebRole1** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**  >  **새 폴더**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-135">In **Solution Explorer**, right-click on the **WebRole1** project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="b4c1e-136">새 폴더의 이름을 *시작*으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-136">Name the new folder *Startup*.</span></span>

   ![시작 폴더 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. <span data-ttu-id="b4c1e-138">*signalr.exe* **Microsoft.AspNet.SignalR.Utils** \<project folder> /SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils. \<version> 에서signalr.exe파일 (유틸리티 패키지와 함께 추가 됨)을 복사 합니다. /도구는 이전 단계에서 만든 *시작* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-138">Copy the *signalr.exe* file (added with the **Microsoft.AspNet.SignalR.Utils** package) from \<project folder>/SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\<version>/tools to the *Startup* folder you created in the previous step.</span></span>

11. <span data-ttu-id="b4c1e-139">**솔루션 탐색기**에서 *시작* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **기존 항목**추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-139">In **Solution Explorer**, right-click the *Startup* folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="b4c1e-140">표시 되는 대화 상자에서 *signalr.exe* 를 선택 하 고 **추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-140">In the dialog that appears, select *signalr.exe* and select **Add**.</span></span>

    ![프로젝트에 signalr.exe 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. <span data-ttu-id="b4c1e-142">만든 *시작* 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-142">Right-click on the *Startup* folder you created.</span></span> <span data-ttu-id="b4c1e-143">**Add**  >  **새 항목**추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-143">Select **Add** > **New Item**.</span></span> <span data-ttu-id="b4c1e-144">**일반** 노드를 선택 하 고 **텍스트 파일**을 선택한 다음 새 항목의 이름을 SignalRPerfCounterInstall로 입력 합니다 *.*</span><span class="sxs-lookup"><span data-stu-id="b4c1e-144">Select the **General** node, select **Text File**, and name the new item *SignalRPerfCounterInstall.cmd*.</span></span> <span data-ttu-id="b4c1e-145">이 명령 파일은 SignalR 성능 카운터를 웹 역할에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-145">This command file will install the SignalR performance counters into the web role.</span></span>

    ![SignalR 성능 카운터 설치 배치 파일 만들기](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. <span data-ttu-id="b4c1e-147">Visual Studio에서 *SignalRPerfCounterInstall* 파일을 만들면 주 창에서 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-147">When Visual Studio creates the *SignalRPerfCounterInstall.cmd* file, it will automatically open in the main window.</span></span> <span data-ttu-id="b4c1e-148">파일의 내용을 다음 스크립트로 바꾼 다음 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-148">Replace the contents of the file with the following script, then save and close the file.</span></span> <span data-ttu-id="b4c1e-149">이 스크립트는 역할 인스턴스에 SignalR 성능 카운터를 추가 하는 *signalr.exe*를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-149">This script executes *signalr.exe*, which adds the SignalR performance counters to the role instance.</span></span>

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. <span data-ttu-id="b4c1e-150">**솔루션 탐색기**에서 *signalr.exe* 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-150">Select the *signalr.exe* file in **Solution Explorer**.</span></span> <span data-ttu-id="b4c1e-151">파일의 **속성**에서 **출력 디렉터리로 복사** 를 **항상 복사**로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-151">In the file's **Properties**, set **Copy to Output Directory** to **Copy Always**.</span></span>

    ![출력 디렉터리로 복사를 항상 복사로 설정](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. <span data-ttu-id="b4c1e-153">*SignalRPerfCounterInstall* 파일에 대해 이전 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-153">Repeat the previous step for the *SignalRPerfCounterInstall.cmd* file.</span></span>

16. <span data-ttu-id="b4c1e-154">*SignalRPerfCounterInstall* 파일을 마우스 오른쪽 단추로 클릭 하 고 **연결 프로그램**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-154">Right-click on the *SignalRPerfCounterInstall.cmd* file and select **Open With**.</span></span> <span data-ttu-id="b4c1e-155">표시 되는 대화 상자에서 **이진 편집기** 를 선택 하 고 **확인**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-155">In the dialog that appears, select **Binary Editor** and select **OK**.</span></span>

    ![이진 편집기를 사용 하 여 열기](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. <span data-ttu-id="b4c1e-157">이진 편집기에서 파일의 선행 바이트를 선택 하 고 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-157">In the binary editor, select any leading bytes in the file and delete them.</span></span> <span data-ttu-id="b4c1e-158">파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-158">Save and close the file.</span></span>

    ![선행 바이트 삭제](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. <span data-ttu-id="b4c1e-160">서비스를 시작할 때 *SignalrPerfCounterInstall* 파일을 실행 하는 시작 작업을 추가 *합니다.*</span><span class="sxs-lookup"><span data-stu-id="b4c1e-160">Open *ServiceDefinition.csdef* and add a startup task that executes the *SignalrPerfCounterInstall.cmd* file when the service starts up:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. <span data-ttu-id="b4c1e-161">`Views/Shared/_Layout.cshtml`파일의 끝에서 jQuery 번들 스크립트를 열고 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-161">Open `Views/Shared/_Layout.cshtml` and remove the jQuery bundle script from the end of the file.</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. <span data-ttu-id="b4c1e-162">서버에서 메서드를 계속 호출 하는 JavaScript 클라이언트를 추가 `increment` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-162">Add a JavaScript client that continuously calls the `increment` method on the server.</span></span> <span data-ttu-id="b4c1e-163">을 열고 `Views/Home/Index.cshtml` 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-163">Open `Views/Home/Index.cshtml` and replace the contents with the following code:</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. <span data-ttu-id="b4c1e-164">**WebRole1** 프로젝트에서 *허브*라는 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-164">Create a new folder in the **WebRole1** project named *Hubs*.</span></span> <span data-ttu-id="b4c1e-165">**솔루션 탐색기** 에서 *허브* 폴더를 마우스 오른쪽 단추로 클릭 하 **Add**고  >  **새 항목**추가를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-165">Right-click the *Hubs* folder in **Solution Explorer** and select **Add** > **New Item**.</span></span> <span data-ttu-id="b4c1e-166">**새 항목 추가** 대화 상자에서 **Web**  >  **SignalR** 범주를 선택 하 고 **SignalR Hub 클래스 (v2)** 항목 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-166">In the **Add New Item** dialog box, select the **Web** > **SignalR** category, and then select the **SignalR Hub Class (v2)** item template.</span></span> <span data-ttu-id="b4c1e-167">새 허브의 이름을 *MyHub.cs* 하 고 **추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-167">Name the new hub *MyHub.cs* and select **Add**.</span></span>

    ![새 항목 추가 대화 상자의 허브 폴더에 SignalR Hub 클래스 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. <span data-ttu-id="b4c1e-169">*MyHub.cs* 가 주 창에서 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-169">*MyHub.cs* will automatically open in the main window.</span></span> <span data-ttu-id="b4c1e-170">내용을 다음 코드로 바꾼 다음 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-170">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. <span data-ttu-id="b4c1e-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* 는 SignalR 코드 베이스와 함께 제공 되는 연결 밀도 테스트 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* is a connection density testing tool provided with the SignalR codebase.</span></span> <span data-ttu-id="b4c1e-172">크랭크에는 영구 연결이 필요 하므로 테스트할 때 사용할 사이트에 하나를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-172">Since Crank requires a persistent connection, you add one to your site for use when testing.</span></span> <span data-ttu-id="b4c1e-173">*PersistentConnections*라는 **WebRole1** 프로젝트에 새 폴더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-173">Add a new folder to the **WebRole1** project called *PersistentConnections*.</span></span> <span data-ttu-id="b4c1e-174">이 폴더를 마우스 오른쪽 단추로 클릭 하 고 클래스 **추가**를 선택  >  **Class**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-174">Right-click this folder and select **Add** > **Class**.</span></span> <span data-ttu-id="b4c1e-175">새 클래스 파일의 이름을 *MyPersistentConnections.cs* 로, **추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-175">Name the new class file *MyPersistentConnections.cs* and select **Add**.</span></span>

24. <span data-ttu-id="b4c1e-176">Visual Studio가 주 창에서 *MyPersistentConnections.cs* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-176">Visual Studio will open the *MyPersistentConnections.cs* file in the main window.</span></span> <span data-ttu-id="b4c1e-177">내용을 다음 코드로 바꾼 다음 파일을 저장 하 고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-177">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. <span data-ttu-id="b4c1e-178">클래스를 사용 하 여 `Startup` SignalR 개체는 OWIN 시작 될 때 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-178">Using the `Startup` class, the SignalR objects start when OWIN starts up.</span></span> <span data-ttu-id="b4c1e-179">*Startup.cs* 를 열거나 만들고 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-179">Open or create *Startup.cs* and replace the contents with the following code:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    <span data-ttu-id="b4c1e-180">위의 코드에서 `OwinStartup` 특성은이 클래스를 OWIN 시작으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-180">In the code above, the `OwinStartup` attribute marks this class to start OWIN.</span></span> <span data-ttu-id="b4c1e-181">`Configuration`메서드가 SignalR을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-181">The `Configuration` method starts SignalR.</span></span>

26. <span data-ttu-id="b4c1e-182">**F5**키를 눌러 Microsoft Azure 에뮬레이터에서 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-182">Test your application in the Microsoft Azure Emulator by pressing **F5**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b4c1e-183">**MapSignalR**에서 **FileLoadException** 이 발생 하는 경우 *web.config* 에서 바인딩 리디렉션을 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-183">If you encounter a **FileLoadException** at **MapSignalR**, change the binding redirects in *web.config* to the following:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. <span data-ttu-id="b4c1e-184">1 분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-184">Wait about one minute.</span></span> <span data-ttu-id="b4c1e-185">Visual Studio에서 클라우드 탐색기 도구 창을 열고 (클라우드 탐색기**보기**  >  **Cloud Explorer**) 경로를 확장 `(Local)/Storage Accounts/(Development)/Tables` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-185">Open the Cloud Explorer tool window in Visual Studio (**View** > **Cloud Explorer**) and expand the path `(Local)/Storage Accounts/(Development)/Tables`.</span></span> <span data-ttu-id="b4c1e-186">**WADPerformanceCountersTable**를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-186">Double-click **WADPerformanceCountersTable**.</span></span> <span data-ttu-id="b4c1e-187">테이블 데이터에 SignalR 카운터가 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-187">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="b4c1e-188">테이블이 표시 되지 않으면 Azure Storage 자격 증명을 다시 입력 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-188">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="b4c1e-189">**클라우드 탐색기** 에서 테이블을 확인 하거나 테이블 열기 창에서 **새로 고침** 단추를 선택 하 여 테이블의 데이터를 표시 하려면 **새로 고침** 단추를 선택 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-189">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

    ![Visual Studio 클라우드 탐색기에서 WAD 성능 카운터 표 선택](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD 성능 카운터 테이블에 수집 된 카운터 표시](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. <span data-ttu-id="b4c1e-192">클라우드에서 응용 프로그램을 테스트 하려면 **serviceconfiguration.cscfg** 파일을 업데이트 하 고를 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 유효한 Azure Storage 계정 연결 문자열로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-192">To test your application in the cloud, update the **ServiceConfiguration.Cloud.cscfg** file and set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` to a valid Azure Storage account connection string.</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. <span data-ttu-id="b4c1e-193">응용 프로그램을 Azure 구독에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-193">Deploy the application to your Azure subscription.</span></span> <span data-ttu-id="b4c1e-194">Azure에 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 [클라우드 서비스를 만들고 배포 하는 방법](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-194">For details on how to deploy an application to Azure, see [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span>

30. <span data-ttu-id="b4c1e-195">잠시 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-195">Wait a few minutes.</span></span> <span data-ttu-id="b4c1e-196">**클라우드 탐색기**에서 위에서 구성한 저장소 계정을 찾고 `WADPerformanceCountersTable` 여기에서 테이블을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-196">In **Cloud Explorer**, locate the storage account you configured above and find the `WADPerformanceCountersTable` table in it.</span></span> <span data-ttu-id="b4c1e-197">테이블 데이터에 SignalR 카운터가 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-197">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="b4c1e-198">테이블이 표시 되지 않으면 Azure Storage 자격 증명을 다시 입력 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-198">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="b4c1e-199">**클라우드 탐색기** 에서 테이블을 확인 하거나 테이블 열기 창에서 **새로 고침** 단추를 선택 하 여 테이블의 데이터를 표시 하려면 **새로 고침** 단추를 선택 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-199">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

<span data-ttu-id="b4c1e-200">이 자습서에서 사용 되는 원래 콘텐츠에 대해 [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c1e-200">Special thanks to [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) for the original content used in this tutorial.</span></span>
