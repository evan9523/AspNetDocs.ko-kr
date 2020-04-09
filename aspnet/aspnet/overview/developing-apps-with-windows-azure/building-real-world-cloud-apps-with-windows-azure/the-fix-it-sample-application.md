---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: '부록: 수정 샘플 응용 프로그램 (Azure를 사용 하 고 실제 클라우드 애플 리 케이 션 빌드) | 마이크로 소프트 문서'
author: MikeWasson
description: Azure 전자책을 사용한 실제 클라우드 앱 구축은 Scott Guthrie가 개발한 프레젠테이션을 기반으로 합니다. 그것은 그가 할 수있는 13 패턴과 관행을 설명합니다 ...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675636"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="7f906-104">부록: 수정 샘플 응용 프로그램(Azure를 사용하여 실제 클라우드 앱 빌드)</span><span class="sxs-lookup"><span data-stu-id="7f906-104">Appendix: The Fix It Sample Application (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="7f906-105">[마이크 와슨,](https://github.com/MikeWasson) [릭 앤더슨,](https://twitter.com/RickAndMSFT) [톰 다이크스트라](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7f906-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="7f906-106">수정 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="7f906-106">Download The Fix It Project</span></span>](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> <span data-ttu-id="7f906-107">Azure 전자책을 **사용한 실제 클라우드 앱 구축은** Scott Guthrie가 개발한 프레젠테이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="7f906-108">클라우드용 웹 앱을 성공적으로 개발하는 데 도움이 되는 13가지 패턴과 사례에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="7f906-109">전자책에 대한 자세한 내용은 [첫 번째 장을](introduction.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f906-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="7f906-110">Azure 전자책이 있는 실제 클라우드 앱 빌드에 대한 이 부록에는 다운로드할 수 있는 Fix It 샘플 응용 프로그램에 대한 추가 정보를 제공하는 다음 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-110">This appendix to the Building Real World Cloud Apps with Azure e-book contains the following sections that provide additional information about the Fix It sample application that you can download:</span></span>

- [<span data-ttu-id="7f906-111">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="7f906-111">Known issues</span></span>](#knownissues)
- [<span data-ttu-id="7f906-112">모범 사례</span><span class="sxs-lookup"><span data-stu-id="7f906-112">Best practices</span></span>](#bestpractices)
- [<span data-ttu-id="7f906-113">로컬 컴퓨터에서 Visual Studio에서 앱을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="7f906-113">How to run the app from Visual Studio on your local computer</span></span>](#run-in-vs)
- [<span data-ttu-id="7f906-114">Windows PowerShell 스크립트를 사용하여 기본 앱을 Azure 앱 서비스 웹 앱에 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="7f906-114">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>](#deploybase)
- [<span data-ttu-id="7f906-115">Windows PowerShell 스크립트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7f906-115">Troubleshooting the Windows PowerShell scripts</span></span>](#troubleshooting)
- [<span data-ttu-id="7f906-116">Azure 앱 서비스 웹 앱 및 Azure 클라우드 서비스에 큐 처리를 사용하여 앱을 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="7f906-116">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a><span data-ttu-id="7f906-117">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="7f906-117">Known issues</span></span>

<span data-ttu-id="7f906-118">Fix It 앱은 원래 이 전자책에 제시된 패턴 중 일부를 가능한 한 간단하게 설명하기 위해 개발되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-118">The Fix It app was originally developed in order to illustrate as simply as possible some of the patterns presented in this e-book.</span></span> <span data-ttu-id="7f906-119">그러나 전자 책은 실제 앱을 빌드하는 것에 관한 것이므로 릴리스된 소프트웨어에 대해 수행하는 것과 유사한 검토 및 테스트 프로세스에 Fix It 코드를 적용했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-119">However, since the e-book is about building real-world apps, we subjected the Fix It code to a review and testing process similar to what we'd do for released software.</span></span> <span data-ttu-id="7f906-120">우리는 여러 가지 문제를 발견했으며 실제 응용 프로그램과 마찬가지로 일부 응용 프로그램은 수정했으며 일부는 나중에 릴리스로 연기했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-120">We found a number of issues, and as with any real-world application, some of them we fixed and some of them we deferred to a later release.</span></span>

<span data-ttu-id="7f906-121">다음 목록에는 프로덕션 응용 프로그램에서 해결해야 하는 문제가 포함되어 있지만 한 가지 이유 또는 다른 이유로 Fix It 샘플 응용 프로그램의 초기 릴리스에서 해결하지 않기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-121">The following list includes issues that should be addressed in a production application, but for one reason or another we decided not to address in the initial release of the Fix It sample application.</span></span>

### <a name="security"></a><span data-ttu-id="7f906-122">보안</span><span class="sxs-lookup"><span data-stu-id="7f906-122">Security</span></span>

- <span data-ttu-id="7f906-123">존재하지 않는 소유자에게 작업을 할당할 수 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-123">Ensure that you can't assign a task to a non-existent owner.</span></span>
- <span data-ttu-id="7f906-124">생성했거나 사용자에게 할당된 작업만 보고 수정할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-124">Ensure that you can only view and modify tasks that you created or are assigned to you.</span></span>
- <span data-ttu-id="7f906-125">로그인 페이지 및 인증 쿠키에 HTTPS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-125">Use HTTPS for sign-in pages and authentication cookies.</span></span>
- <span data-ttu-id="7f906-126">인증 쿠키에 대한 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-126">Specify a time limit for authentication cookies.</span></span>

### <a name="input-validation"></a><span data-ttu-id="7f906-127">입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7f906-127">Input validation</span></span>

<span data-ttu-id="7f906-128">일반적으로 프로덕션 앱은 Fix It 앱보다 더 많은 입력 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-128">In general, a production app would do more input validation than the Fix It app.</span></span> <span data-ttu-id="7f906-129">예를 들어 업로드가 허용되는 이미지 크기/이미지 파일 크기는 제한되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-129">For example, the image size / image file size allowed for upload should be limited.</span></span>

### <a name="administrator-functionality"></a><span data-ttu-id="7f906-130">관리자 기능</span><span class="sxs-lookup"><span data-stu-id="7f906-130">Administrator functionality</span></span>

<span data-ttu-id="7f906-131">관리자는 기존 작업의 소유권을 변경할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-131">An administrator should be able to change ownership on existing tasks.</span></span> <span data-ttu-id="7f906-132">예를 들어 작업 작성자는 관리 액세스가 활성화되지 않는 한 작업을 유지할 권한이 없는 회사를 떠날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-132">For example, the creator of a task might leave the company, leaving no one with authority to maintain the task unless administrative access is enabled.</span></span>

### <a name="queue-message-processing"></a><span data-ttu-id="7f906-133">큐 메시지 처리</span><span class="sxs-lookup"><span data-stu-id="7f906-133">Queue message processing</span></span>

<span data-ttu-id="7f906-134">Fix It 앱에서 큐 메시지 처리는 최소한의 코드로 큐 중심 작업 패턴을 설명하기 위해 간단하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-134">Queue message processing in the Fix It app was designed to be simple in order to illustrate the queue-centric work pattern with a minimum amount of code.</span></span> <span data-ttu-id="7f906-135">이 간단한 코드는 실제 프로덕션 응용 프로그램에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-135">This simple code would not be adequate for an actual production application.</span></span>

- <span data-ttu-id="7f906-136">코드는 각 큐 메시지가 한 번에 처리된다는 것을 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-136">The code does not guarantee that each queue message will be processed at most once.</span></span> <span data-ttu-id="7f906-137">큐에서 메시지를 받으면 다른 큐 수신기에 메시지가 표시되지 않는 시간 시간(시간) 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-137">When you get a message from the queue, there is a timeout period, during which the message is invisible to other queue listeners.</span></span> <span data-ttu-id="7f906-138">메시지가 삭제되기 전에 시간 시간이 만료되면 메시지가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-138">If the timeout expires before the message is deleted, the message becomes visible again.</span></span> <span data-ttu-id="7f906-139">따라서 작업자 역할 인스턴스가 메시지를 처리하는 데 오랜 시간을 소비하는 경우 이론적으로 동일한 메시지가 두 번 처리되어 데이터베이스에 중복 작업이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-139">Therefore, if a worker role instance spends a long time processing a message, it is theoretically possible for the same message to get processed twice, resulting in a duplicate task in the database.</span></span> <span data-ttu-id="7f906-140">이 문제에 대한 자세한 내용은 [Azure 저장소 큐 사용](https://msdn.microsoft.com/library/ff803365.aspx#sec7)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f906-140">For more information about this issue, see [Using Azure Storage Queues](https://msdn.microsoft.com/library/ff803365.aspx#sec7).</span></span>
- <span data-ttu-id="7f906-141">메시지 검색을 일괄 처리하여 큐 폴링 논리를 보다 비용 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-141">The queue polling logic could be more cost-effective, by batching message retrieval.</span></span> <span data-ttu-id="7f906-142">[CloudQueue.GetMessageAsync를](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)호출할 때마다 트랜잭션 비용이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-142">Every time you call [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), there is a transaction cost.</span></span> <span data-ttu-id="7f906-143">대신 단일 트랜잭션에서 여러 메시지를 받는 [CloudQueue.GetMessagesAsync(복수의](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) 's')를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-143">Instead, you can call [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (note the plural 's'), which gets multiple messages in a single transaction.</span></span> <span data-ttu-id="7f906-144">Azure 저장소 큐의 트랜잭션 비용은 매우 낮으므로 대부분의 시나리오에서는 비용에 미치는 영향이 그리 많지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-144">The transaction costs for Azure Storage Queues are very low, so the impact on costs is not substantial in most scenarios.</span></span>
- <span data-ttu-id="7f906-145">큐 메시지 처리 코드의 긴밀한 루프는 다중 코어 VM을 효율적으로 활용하지 않는 CPU 선호도를 유발합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-145">The tight loop in the queue message-processing code causes CPU affinity, which does not utilize multi-core VMs efficiently.</span></span> <span data-ttu-id="7f906-146">더 나은 디자인은 작업 병렬 처리를 사용하여 여러 비동기 작업을 병렬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-146">A better design would use task parallelism to run several async tasks in parallel.</span></span>
- <span data-ttu-id="7f906-147">큐 메시지 처리에는 기본적인 예외 처리만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-147">Queue message-processing has only rudimentary exception handling.</span></span> <span data-ttu-id="7f906-148">예를 들어 코드는 [포이즌 메시지를](https://msdn.microsoft.com/library/ms789028.aspx)처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-148">For example, the code doesn't handle [poison messages](https://msdn.microsoft.com/library/ms789028.aspx).</span></span> <span data-ttu-id="7f906-149">메시지 처리로 인해 예외가 발생하면 오류를 기록하고 메시지를 삭제해야 하거나 작업자 역할이 다시 처리하려고 시도하면 루프가 무기한 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-149">(When message processing causes an exception, you have to log the error and delete the message, or the worker role will try to process it again, and the loop will continue indefinitely.)</span></span>

### <a name="sql-queries-are-unbounded"></a><span data-ttu-id="7f906-150">SQL 쿼리는 무한합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-150">SQL queries are unbounded</span></span>

<span data-ttu-id="7f906-151">현재 Fix It 코드는 인덱스 페이지에 대한 쿼리가 반환할 수 있는 행 수에 제한을 두지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-151">Current Fix It code places no limit on how many rows the queries for Index pages might return.</span></span> <span data-ttu-id="7f906-152">데이터베이스에 많은 양의 작업을 입력하면 수신된 결과 목록의 크기로 인해 성능 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-152">If a large volume of tasks is entered into the database, the size of the resulting lists received could cause performance issues.</span></span> <span data-ttu-id="7f906-153">해결책은 페이징을 구현하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-153">The solution is to implement paging.</span></span> <span data-ttu-id="7f906-154">예를 들어 [ASP.NET MVC 응용 프로그램에서 엔터티 프레임워크를 사용 하 여 정렬, 필터링 및 페이징을](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-154">For an example, see [Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span></span>

### <a name="view-models-recommended"></a><span data-ttu-id="7f906-155">권장 모델 보기</span><span class="sxs-lookup"><span data-stu-id="7f906-155">View models recommended</span></span>

<span data-ttu-id="7f906-156">Fix It 앱은 FixItTask 엔터티 클래스를 사용하여 컨트롤러와 뷰 간에 정보를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-156">The Fix It app uses the FixItTask entity class to pass information between the controller and the view.</span></span> <span data-ttu-id="7f906-157">뷰 모델을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-157">A best practice is to use view models.</span></span> <span data-ttu-id="7f906-158">도메인 모델(예: FixItTask 엔터티 클래스)은 데이터 지속성에 필요한 것을 중심으로 설계되었으며 뷰 모델은 데이터 프레젠테이션용으로 설계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-158">The domain model (e.g., the FixItTask entity class) is designed around what is needed for data persistence, while a view model can be designed for data presentation.</span></span> <span data-ttu-id="7f906-159">자세한 내용은 [12ASP.NET MVC 모범 사례를](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f906-159">For more information, see [12 ASP.NET MVC Best Practices](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).</span></span>

### <a name="secure-image-blob-recommended"></a><span data-ttu-id="7f906-160">보안 이미지 Blob 권장</span><span class="sxs-lookup"><span data-stu-id="7f906-160">Secure image blob recommended</span></span>

<span data-ttu-id="7f906-161">Fix It 앱은 업로드된 이미지를 공개로 저장하므로 URL을 찾는 사람은 누구나 이미지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-161">The Fix It app stores uploaded images as public, meaning that anyone who finds the URL can access the images.</span></span> <span data-ttu-id="7f906-162">이미지는 공개가 아닌 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-162">The images could be secured instead of public.</span></span>

### <a name="no-powershell-automation-scripts-for-queues"></a><span data-ttu-id="7f906-163">큐에 대한 PowerShell 자동화 스크립트 없음</span><span class="sxs-lookup"><span data-stu-id="7f906-163">No PowerShell automation scripts for queues</span></span>

<span data-ttu-id="7f906-164">샘플 PowerShell 자동화 스크립트는 Azure App Service 웹 앱에서 전적으로 실행되는 Fix It의 기본 버전에 대해서만 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-164">Sample PowerShell automation scripts were written only for the base version of Fix It that runs entirely in Azure App Service Web Apps.</span></span> <span data-ttu-id="7f906-165">웹 앱에 설정하고 배포하기 위한 스크립트와 큐 처리에 필요한 클라우드 서비스 환경을 제공하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-165">We haven't provided scripts for setting up and deploying to the web app plus Cloud Service environment required for queue processing.</span></span>

### <a name="special-handling-for-html-codes-in-user-input"></a><span data-ttu-id="7f906-166">사용자 입력에서 HTML 코드에 대한 특수 처리</span><span class="sxs-lookup"><span data-stu-id="7f906-166">Special handling for HTML codes in user input</span></span>

<span data-ttu-id="7f906-167">ASP.NET 악의적인 사용자가 사용자 입력 텍스트 상자에 스크립트를 입력하여 사이트 간 스크립팅 공격을 시도할 수 있는 여러 가지 방법을 자동으로 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-167">ASP.NET automatically prevents many ways in which malicious users might attempt cross-site scripting attacks by entering script in user input text boxes.</span></span> <span data-ttu-id="7f906-168">그리고 작업 `DisplayFor` 제목및 메모를 표시하는 데 사용되는 MVC 도우미는 브라우저에 전송하는 값을 자동으로 HTML 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-168">And the MVC `DisplayFor` helper used to display task titles and notes automatically HTML-encodes values that it sends to the browser.</span></span> <span data-ttu-id="7f906-169">그러나 프로덕션 앱에서는 추가 조치를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-169">But in a production app you might want to take additional measures.</span></span> <span data-ttu-id="7f906-170">자세한 내용은 ASP.NET 유효성 [검사 요청을](https://msdn.microsoft.com/library/hh882339.aspx)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f906-170">For more information, see [Request Validation in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).</span></span>

<a id="bestpractices"></a>
## <a name="best-practices"></a><span data-ttu-id="7f906-171">모범 사례</span><span class="sxs-lookup"><span data-stu-id="7f906-171">Best practices</span></span>

<span data-ttu-id="7f906-172">다음은 Fix It 앱의 원래 버전의 코드 검토 및 테스트에서 발견된 후 수정된 몇 가지 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-172">Following are some issues that were fixed after being discovered in code review and testing of the original version of the Fix It app.</span></span> <span data-ttu-id="7f906-173">일부는 원래 코더가 특정 모범 사례를 인식하지 못하고 코드가 신속하게 작성되어 릴리스된 소프트웨어를 위한 것이 아니기 때문에 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-173">Some were caused by the original coder not being aware of a particular best practice, some simply because the code was written quickly and wasn't intended for released software.</span></span> <span data-ttu-id="7f906-174">이 리뷰와 테스트에서 배운 것이 웹 앱을 개발하는 다른 사람들에게 도움이 될 수 있는 문제가 있는 경우를 대비하여 여기에 문제를 나열하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-174">We're listing the issues here in case there's something we learned from this review and testing that might be helpful to others who are also developing web apps.</span></span>

### <a name="dispose-the-database-repository"></a><span data-ttu-id="7f906-175">데이터베이스 리포지토리 삭제</span><span class="sxs-lookup"><span data-stu-id="7f906-175">Dispose the database repository</span></span>

<span data-ttu-id="7f906-176">클래스는 `FixItTaskRepository` 엔터티 프레임워크 `DbContext` 인스턴스를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-176">The `FixItTaskRepository` class must dispose the Entity Framework `DbContext` instance.</span></span> <span data-ttu-id="7f906-177">클래스에서 구현하여 `IDisposable` 이 `FixItTaskRepository` 작업을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-177">We did this by implementing `IDisposable` in the `FixItTaskRepository` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

<span data-ttu-id="7f906-178">AutoFac은 인스턴스를 `FixItTaskRepository` 자동으로 삭제하므로 명시적으로 삭제할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-178">Note that AutoFac will automatically dispose the `FixItTaskRepository` instance, so we don't need to explicitly dispose it.</span></span>

<span data-ttu-id="7f906-179">또 다른 옵션은 `DbContext` 에서 `FixItTaskRepository`멤버 변수를 제거하고 `DbContext` 대신 문 내에서 각 리포지토리 메서드 내에서 로컬 변수를 만드는 것입니다. `using`</span><span class="sxs-lookup"><span data-stu-id="7f906-179">Another option is to remove the `DbContext` member variable from `FixItTaskRepository`, and instead create a local `DbContext` variable within each repository method, inside a `using` statement.</span></span> <span data-ttu-id="7f906-180">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="7f906-180">For example:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a><span data-ttu-id="7f906-181">DI와 같은 싱글톤 등록</span><span class="sxs-lookup"><span data-stu-id="7f906-181">Register singletons as such with DI</span></span>

<span data-ttu-id="7f906-182">`PhotoService` 클래스와 `Logger` 클래스의 인스턴스가 하나만 필요하므로 이러한 클래스는 *DependenciesConfig.cs* [종속성 주입을 위한 단일 인스턴스로 등록되어야](https://code.google.com/p/autofac/wiki/InstanceScope) 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-182">Since only one instance of the `PhotoService` class and `Logger` class is needed, these classes should be [registered as single instances for dependency injection](https://code.google.com/p/autofac/wiki/InstanceScope) in *DependenciesConfig.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a><span data-ttu-id="7f906-183">보안: 사용자에게 오류 세부 정보를 표시하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="7f906-183">Security: Don't show error details to users</span></span>

<span data-ttu-id="7f906-184">원래 Fix It 앱에는 일반 오류 페이지가 없으며 모든 예외가 UI에 버블링되도록 하여 데이터베이스 연결 오류와 같은 일부 예외로 인해 전체 스택 추적이 브라우저에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-184">The original Fix It app didn't have a generic error page and just let all exceptions bubble up to the UI, so some exceptions such as database connection errors could result in a full stack trace being displayed to the browser.</span></span> <span data-ttu-id="7f906-185">자세한 오류 정보는 악의적인 사용자의 공격을 용이하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-185">Detailed error information can sometimes facilitate attacks by malicious users.</span></span> <span data-ttu-id="7f906-186">해결 방법은 예외 세부 정보를 기록하고 오류 세부 정보가 포함되지 않은 사용자에게 오류 페이지를 표시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-186">The solution is to log the exception details and display an error page to the user that doesn't include error details.</span></span> <span data-ttu-id="7f906-187">Fix It 앱이 이미 로깅 중이었으며 오류 페이지를 `<customErrors mode=On>` 표시하기 위해 Web.config 파일에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-187">The Fix It app was already logging, and in order to display an error page, we added `<customErrors mode=On>` in the Web.config file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

<span data-ttu-id="7f906-188">기본적으로 이로 인해 *뷰\공유\Error.cshtml이* 오류에 대해 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-188">By default this causes *Views\Shared\Error.cshtml* to be displayed for errors.</span></span> <span data-ttu-id="7f906-189">*Error.cshtml을* 사용자 지정하거나 고유한 오류 페이지 보기를 `defaultRedirect` 만들고 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-189">You can customize *Error.cshtml* or create your own error page view and add a `defaultRedirect` attribute.</span></span> <span data-ttu-id="7f906-190">특정 오류에 대해 다른 오류 페이지를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-190">You can also specify different error pages for specific errors.</span></span>

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a><span data-ttu-id="7f906-191">보안: 작성자가 작업을 편집할 수 있도록 허용</span><span class="sxs-lookup"><span data-stu-id="7f906-191">Security: only allow a task to be edited by its creator</span></span>

<span data-ttu-id="7f906-192">대시보드 색인 페이지에는 로그온한 사용자가 만든 작업만 표시되지만 악의적인 사용자는 다른 사용자의 작업에 ID가 있는 URL을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-192">The Dashboard Index page only shows tasks created by the logged-on user, but a malicious user could create a URL with an ID to another user's task.</span></span> <span data-ttu-id="7f906-193">이 경우 404를 반환하기 위해 *DashboardController.cs* 코드를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-193">We added code in *DashboardController.cs* to return a 404 in that case:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a><span data-ttu-id="7f906-194">예외를 삼키지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="7f906-194">Don't swallow exceptions</span></span>

<span data-ttu-id="7f906-195">원래 Fix It 앱은 SQL 쿼리로 인해 발생한 예외를 로깅한 후 null을 반환했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-195">The original Fix It app just returned null after logging an exception that resulted from a SQL query:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

<span data-ttu-id="7f906-196">이렇게하면 쿼리가 성공했지만 행을 반환하지 않은 것처럼 사용자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-196">This would make it look to the user as if the query succeeded but just didn't return any rows.</span></span> <span data-ttu-id="7f906-197">해결 방법은 catch 및 로깅 후 예외를 다시 throw하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-197">Solution is to re-throw the exception after catching and logging:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a><span data-ttu-id="7f906-198">작업자 역할의 모든 예외 catch</span><span class="sxs-lookup"><span data-stu-id="7f906-198">Catch all exceptions in worker roles</span></span>

<span data-ttu-id="7f906-199">작업자 역할에서 처리되지 않은 예외는 VM을 재활용하게 되므로 try-catch 블록에서 수행하는 모든 작업을 래핑하고 모든 예외를 처리하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-199">Any unhandled exceptions in a worker role will cause the VM to be recycled, so you want to wrap everything you do in a try-catch block and handle all exceptions.</span></span>

### <a name="specify-length-for-string-properties-in-entity-classes"></a><span data-ttu-id="7f906-200">엔터티 클래스의 문자열 속성에 대한 길이 지정</span><span class="sxs-lookup"><span data-stu-id="7f906-200">Specify length for string properties in entity classes</span></span>

<span data-ttu-id="7f906-201">간단한 코드를 표시 하기 위해 Fix It 앱의 원래 버전 FixItTask 엔터티의 필드에 대 한 길이 지정 하지 않은, 그리고 결과적으로 그들은 varchar (최대)로 정의 된 데이터베이스에.</span><span class="sxs-lookup"><span data-stu-id="7f906-201">In order to display simple code, the original version of the Fix It app didn't specify lengths for the fields of the FixItTask entity, and as a result they were defined as varchar(max) in the database.</span></span> <span data-ttu-id="7f906-202">결과적으로 UI는 거의 모든 양의 입력을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-202">As a result, the UI would accept almost any amount of input.</span></span> <span data-ttu-id="7f906-203">길이를 지정하면 웹 페이지의 사용자 입력과 데이터베이스의 열 크기에 모두 적용되는 제한이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-203">Specifying lengths sets limits that apply both to user input in the web page and column size in the database:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a><span data-ttu-id="7f906-204">변경될 것으로 예상되지 않을 때 개인 멤버를 readonly로 표시</span><span class="sxs-lookup"><span data-stu-id="7f906-204">Mark private members as readonly when they aren't expected to change</span></span>

<span data-ttu-id="7f906-205">예를 들어 `DashboardController` 클래스에서 인스턴스가 `FixItTaskRepository` 만들어지고 변경될 것으로 예상되지 않으므로 [readonly로](https://msdn.microsoft.com/library/acdd6hb7.aspx)정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-205">For example, in the `DashboardController` class an instance of `FixItTaskRepository` is created and isn't expected to change, so we defined it as [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx).</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a><span data-ttu-id="7f906-206">목록을 사용합니다. 목록 대신 Any()입니다. 카운트() &gt; 0</span><span class="sxs-lookup"><span data-stu-id="7f906-206">Use list.Any() instead of list.Count() &gt; 0</span></span>

<span data-ttu-id="7f906-207">목록의 하나 이상의 항목이 지정된 기준에 맞는지 여부만 신경 [Any](https://msdn.microsoft.com/library/bb534972.aspx) 쓰는 경우 조건에 맞는 항목이 발견되는 즉시 반환되지만 `Count` 메서드는 항상 모든 항목을 반복해야 하므로 Any 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-207">If you all you care about is whether one or more items in a list fit the specified criteria, use the [Any](https://msdn.microsoft.com/library/bb534972.aspx) method, because it returns as soon as an item fitting the criteria is found, whereas the `Count` method always has to iterate through every item.</span></span> <span data-ttu-id="7f906-208">대시보드 *Index.cshtml* 파일에는 원래 이 코드가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-208">The Dashboard *Index.cshtml* file originally had this code:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

<span data-ttu-id="7f906-209">우리는 이것을 변경했습니다:</span><span class="sxs-lookup"><span data-stu-id="7f906-209">We changed it to this:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a><span data-ttu-id="7f906-210">MVC 도우미를 사용하여 MVC 보기에서 URL 생성</span><span class="sxs-lookup"><span data-stu-id="7f906-210">Generate URLs in MVC views using MVC helpers</span></span>

<span data-ttu-id="7f906-211">홈 페이지의 **수정** 만들기 단추의 경우 Fix It 앱이 앵커 요소를 하드 코딩했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-211">For the **Create a Fix It** button on the home page, the Fix It app hard coded an anchor element:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

<span data-ttu-id="7f906-212">이와 같은 보기/작업 링크의 경우 [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 도우미를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-212">For View/Action links like this it's better to use the [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper, for example:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a><span data-ttu-id="7f906-213">작업자 역할에서 Thread.Sleep 대신 Task.Delay 사용</span><span class="sxs-lookup"><span data-stu-id="7f906-213">Use Task.Delay instead of Thread.Sleep in worker role</span></span>

<span data-ttu-id="7f906-214">새 프로젝트 템플릿은 `Thread.Sleep` 작업자 역할에 대한 샘플 코드에 포함하지만 스레드가 절전 모드로 연결되면 스레드 풀이 추가 불필요한 스레드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-214">The new-project template puts `Thread.Sleep` in the sample code for a worker role, but causing the thread to sleep can cause the thread pool to spawn additional unnecessary threads.</span></span> <span data-ttu-id="7f906-215">대신 [Task.Delay를](https://msdn.microsoft.com/library/hh139096.aspx) 사용하여 이를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-215">You can avoid that by using [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) instead.</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a><span data-ttu-id="7f906-216">비동기 보이드 방지</span><span class="sxs-lookup"><span data-stu-id="7f906-216">Avoid async void</span></span>

<span data-ttu-id="7f906-217">비동기 메서드가 값을 `Task` 반환할 필요가 없는 경우 . `void`</span><span class="sxs-lookup"><span data-stu-id="7f906-217">If an async method doesn't need to return a value, return a `Task` type rather than `void`.</span></span>

<span data-ttu-id="7f906-218">이 예제는 `FixItQueueManager` 클래스에서 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-218">This example is from the `FixItQueueManager` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

<span data-ttu-id="7f906-219">최상위 이벤트 `async void` 처리기에만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-219">You should use `async void` only for top-level event handlers.</span></span> <span data-ttu-id="7f906-220">메서드를 `async void`로 정의하는 경우 호출자는 메서드를 **기다리거나** 메서드가 throw하는 예외를 catch할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-220">If you define a method as `async void`, the caller cannot **await** the method or catch any exceptions the method throws.</span></span> <span data-ttu-id="7f906-221">자세한 내용은 [비동기 프로그래밍의 모범 사례를](https://msdn.microsoft.com/magazine/jj991977.aspx)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f906-221">For more information, see [Best Practices in Asynchronous Programming](https://msdn.microsoft.com/magazine/jj991977.aspx).</span></span>

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a><span data-ttu-id="7f906-222">취소 토큰을 사용하여 작업자 역할 루프에서 분리</span><span class="sxs-lookup"><span data-stu-id="7f906-222">Use a cancellation token to break from worker role loop</span></span>

<span data-ttu-id="7f906-223">일반적으로 작업자 역할의 **Run** 메서드에는 무한 루프가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-223">Typically, the **Run** method on a worker role contains an infinite loop.</span></span> <span data-ttu-id="7f906-224">작업자 역할이 중지되면 [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-224">When the worker role is stopping, the [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) method is called.</span></span> <span data-ttu-id="7f906-225">이 메서드를 사용 하 여 **Run** 메서드 내에서 수행 되는 작업을 취소 하 고 정상적으로 종료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-225">You should use this method to cancel the work that is being done inside the **Run** method and exit gracefully.</span></span> <span data-ttu-id="7f906-226">그렇지 않으면 작업이 중간에 종료될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-226">Otherwise, the process might be terminated in the middle of an operation.</span></span>

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a><span data-ttu-id="7f906-227">자동 MIME 스니핑 절차 거부</span><span class="sxs-lookup"><span data-stu-id="7f906-227">Opt out of Automatic MIME Sniffing Procedure</span></span>

<span data-ttu-id="7f906-228">경우에 따라 Internet Explorer는 웹 서버에서 지정한 유형과 다른 MIME 유형을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-228">In some cases, Internet Explorer reports a MIME type different than the type specified by the web server.</span></span> <span data-ttu-id="7f906-229">예를 들어 Internet Explorer가 HTTP 응답 헤더 콘텐츠 유형: 텍스트/일반과 함께 전달된 파일에서 HTML 콘텐츠를 발견하면 Internet Explorer는 콘텐츠를 HTML로 렌더링해야 한다고 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-229">For instance, if Internet Explorer finds HTML content in a file delivered with the HTTP response header Content-Type: text/plain, Internet Explorer determines that the content should be rendered as HTML.</span></span> <span data-ttu-id="7f906-230">안타깝게도 이 "MIME 스니핑"은 신뢰할 수 없는 콘텐츠를 호스팅하는 서버의 보안 문제로 이어질 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-230">Unfortunately, this "MIME-sniffing" can also lead to security problems for servers hosting untrusted content.</span></span> <span data-ttu-id="7f906-231">이 문제를 방지하기 위해 Internet Explorer 8은 MIME 형식 결정 코드를 여러 번 변경했으며 응용 프로그램 개발자가 [MIME 스니핑을 옵트아웃할](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-231">To combat this problem, Internet Explorer 8 has made a number of changes to MIME-type determination code and allows application developers to [opt out of MIME-sniffing](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx).</span></span> <span data-ttu-id="7f906-232">다음 코드가 *Web.config* 파일에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-232">The following code was added to the *Web.config* file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a><span data-ttu-id="7f906-233">번들 및 축소 사용</span><span class="sxs-lookup"><span data-stu-id="7f906-233">Enable bundling and minification</span></span>

<span data-ttu-id="7f906-234">Visual Studio에서 새 웹 프로젝트를 만들 때 자바스크립트 파일의 번들 및 축소는 기본적으로 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-234">When Visual Studio creates a new web project, bundling and minification of JavaScript files is not enabled by default.</span></span> <span data-ttu-id="7f906-235">BundleConfig.cs 코드 줄을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-235">We added a line of code in BundleConfig.cs:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a><span data-ttu-id="7f906-236">인증 쿠키의 만료 시간 시간 설정</span><span class="sxs-lookup"><span data-stu-id="7f906-236">Set an expiration time-out for authentication cookies</span></span>

<span data-ttu-id="7f906-237">기본적으로 인증 쿠키는 2주 후 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-237">By default, authentication cookies expire in two weeks.</span></span> <span data-ttu-id="7f906-238">짧은 시간은 더 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-238">A shorter time is more secure.</span></span> <span data-ttu-id="7f906-239">*StartupAuth.cs*이 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-239">You can change this setting in *StartupAuth.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a><span data-ttu-id="7f906-240">로컬 컴퓨터에서 Visual Studio에서 앱을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="7f906-240">How to run the app from Visual Studio on your local computer</span></span>

<span data-ttu-id="7f906-241">Fix It 앱을 실행하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-241">There are two ways to run the Fix It app:</span></span>

- <span data-ttu-id="7f906-242">SQL 데이터베이스에 직접 새 작업을 기록하는 기본 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-242">Run the base application that writes new tasks directly to the SQL database.</span></span>
- <span data-ttu-id="7f906-243">큐와 백 엔드 서비스를 사용하여 응용 프로그램을 실행하여 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-243">Run the application using a queue plus a backend service to create tasks.</span></span> <span data-ttu-id="7f906-244">큐 패턴은 [큐 중심 작업 패턴](queue-centric-work-pattern.md)장에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-244">The queue pattern is described in the chapter [Queue-Centric Work Pattern](queue-centric-work-pattern.md).</span></span>

<a id="runbase"></a>
### <a name="run-the-base-application"></a><span data-ttu-id="7f906-245">기본 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7f906-245">Run the base application</span></span>

1. <span data-ttu-id="7f906-246">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-246">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>
2. <span data-ttu-id="7f906-247">Visual [Studio에 .NET에 대한 Azure SDK를 설치합니다.](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="7f906-247">Install the [Azure SDK for .NET for Visual Studio](https://azure.microsoft.com/downloads/).</span></span>
3. <span data-ttu-id="7f906-248">[MSDN 코드 갤러리에서](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).zip 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-248">Download the .zip file from the [MSDN Code Gallery](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).</span></span>
4. <span data-ttu-id="7f906-249">파일 탐색기에서 .zip 파일을 마우스 오른쪽 단추로 클릭하고 속성을 클릭한 다음 속성 창에서 차단 해제를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-249">In File Explorer, right-click the .zip file and click Properties, then in the Properties window click Unblock.</span></span>
5. <span data-ttu-id="7f906-250">파일 의 압축을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-250">Unzip the file.</span></span>
6. <span data-ttu-id="7f906-251">.sln 파일을 두 번 클릭하여 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-251">Double-click the .sln file to launch Visual Studio.</span></span>
7. <span data-ttu-id="7f906-252">**도구** 메뉴에서 **패키지 관리자 NuGet을**클릭한 다음 **패키지 관리자 콘솔을**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-252">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>
8. <span data-ttu-id="7f906-253">PMC(패키지 관리자 콘솔)에서 복원을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-253">In the Package Manager Console (PMC), click Restore.</span></span>
9. <span data-ttu-id="7f906-254">Visual Studio를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-254">Exit Visual Studio.</span></span>
10. <span data-ttu-id="7f906-255">Azure [저장소 에뮬레이터를](/azure/storage/common/storage-use-emulator)시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-255">Start the [Azure storage emulator](/azure/storage/common/storage-use-emulator).</span></span>
11. <span data-ttu-id="7f906-256">이전 단계에서 닫은 솔루션 파일을 열어 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-256">Restart Visual Studio, opening the solution file you closed in the previous step.</span></span>
12. <span data-ttu-id="7f906-257">FixIt 프로젝트가 시작 프로젝트로 설정되어 있는지 확인한 다음 CTRL+F5를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-257">Make sure the FixIt project is set as the startup project, and then press CTRL+F5 to run the project.</span></span>

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a><span data-ttu-id="7f906-258">큐 처리를 사용 하 고 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7f906-258">Run the application with queue processing</span></span>

1. <span data-ttu-id="7f906-259">기본 응용 [프로그램 실행의 지시에](#runbase)따라 브라우저를 닫고 Visual Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-259">Follow the directions for [Run the base application](#runbase), and then close the browser and close Visual Studio.</span></span>
2. <span data-ttu-id="7f906-260">관리자 권한으로 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-260">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="7f906-261">Azure 계산 에뮬레이터를 사용하며 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-261">(You'll be using the Azure compute emulator, and that requires administrator privileges.)</span></span>
3. <span data-ttu-id="7f906-262">*MyFixIt* 프로젝트(웹 프로젝트)의 `appSettings/UseQueues` 응용 프로그램 *Web.config* 파일에서 값을 "true"로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-262">In the application *Web.config* file in the *MyFixIt* project (the web project), change the value of `appSettings/UseQueues` to "true":</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. <span data-ttu-id="7f906-263">Azure [저장소 에뮬레이터가](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) 계속 실행되지 않으면 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-263">If the [Azure storage emulator](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) isn't still running, start it again.</span></span>
5. <span data-ttu-id="7f906-264">FixIt 웹 프로젝트와 MyFixItCloudService 프로젝트를 동시에 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-264">Run the FixIt web project and the MyFixItCloudService project simultaneously.</span></span>

    <span data-ttu-id="7f906-265">비주얼 스튜디오 사용:</span><span class="sxs-lookup"><span data-stu-id="7f906-265">Using Visual Studio:</span></span>

   1. <span data-ttu-id="7f906-266">**F5를** 눌러 FixIt 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-266">Press **F5** to run the FixIt project.</span></span>
   2. <span data-ttu-id="7f906-267">**솔루션 탐색기에서**MyFixItCloudService 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 새 인스턴스 시작 **디버그를** > **Start New Instance**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-267">In **Solution Explorer**, right-click the MyFixItCloudService project, and then click **Debug** > **Start New Instance**.</span></span>

    <span data-ttu-id="7f906-268">웹용 비주얼 스튜디오 2013 익스프레스 사용:</span><span class="sxs-lookup"><span data-stu-id="7f906-268">Using Visual Studio 2013 Express for Web:</span></span>

   3. <span data-ttu-id="7f906-269">솔루션 탐색기에서 FixIt 솔루션을 마우스 오른쪽 단추로 클릭하고 **속성을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-269">In Solution Explorer, right-click the FixIt solution and select **Properties**.</span></span>
   4. <span data-ttu-id="7f906-270">**여러 시작 프로젝트를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-270">Select **Multiple Startup Projects**.</span></span>
   5. <span data-ttu-id="7f906-271">MyFixIt 및 MyFixItCloudService 아래의 **작업** 드롭다운 목록에서 **시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-271">In the **Action** dropdown list under MyFixIt and MyFixItCloudService, select **Start**.</span></span>
   6. <span data-ttu-id="7f906-272">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-272">Click **OK**.</span></span>
   7. <span data-ttu-id="7f906-273">**F5** 키를 눌러 두 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-273">Press **F5** to run both projects.</span></span>

      <span data-ttu-id="7f906-274">MyFixItCloudService 프로젝트를 실행 하면 Visual Studio Azure 계산 에뮬레이터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-274">When you run the MyFixItCloudService project, Visual Studio starts the Azure compute emulator.</span></span> <span data-ttu-id="7f906-275">방화벽 구성에 따라 방화벽을 통해 에뮬레이터를 허용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-275">Depending on your firewall configuration, you might need to allow the emulator through the firewall.</span></span>

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a><span data-ttu-id="7f906-276">Windows PowerShell 스크립트를 사용하여 기본 앱을 Azure 앱 서비스 웹 앱에 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="7f906-276">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>

<span data-ttu-id="7f906-277">[모든 자동화](automate-everything.md) 패턴을 설명하기 위해 Fix It 앱은 Azure에서 환경을 설정하고 새 환경에 프로젝트를 배포하는 스크립트와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-277">To illustrate the [Automate Everything](automate-everything.md) pattern, the Fix It app is supplied with scripts that set up an environment in Azure and deploy the project to the new environment.</span></span> <span data-ttu-id="7f906-278">다음 지침은 스크립트를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-278">The following instructions explain how to use the scripts.</span></span>

<span data-ttu-id="7f906-279">큐를 사용하지 않고 Azure에서 실행하려는 경우 다음 지침을 진행하기 전에 UseQueues appSet 값을 false로 다시 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-279">If you want to run in Azure without using queues, and you made the changes to run locally with queues, make sure you set the UseQueues appSetting value back to false before proceeding with the following instructions.</span></span>

<span data-ttu-id="7f906-280">이러한 지침은 이미 다운로드하여 로컬에서 Fix It 솔루션을 실행하고 Azure 계정이 있거나 관리할 권한이 있는 Azure 구독이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-280">These instructions assume you have already downloaded and run the Fix It solution locally, and that you have an Azure account or have an Azure subscription that you are authorized to manage.</span></span>

1. <span data-ttu-id="7f906-281">Azure **PowerShell** 콘솔을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-281">Install the **Azure PowerShell** console.</span></span> <span data-ttu-id="7f906-282">자세한 내용은 [Azure PowerShell 설치 및 구성법](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f906-282">For instructions, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span>

    <span data-ttu-id="7f906-283">이 사용자 지정된 콘솔은 Azure 구독에서 작동하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-283">This customized console is configured to work with your Azure subscription.</span></span> <span data-ttu-id="7f906-284">Azure 모듈은 프로그램 *파일* 디렉터리에 설치되며 Azure PowerShell 콘솔을 사용할 때마다 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-284">The Azure module is installed in the *Program Files* directory and is automatically imported on every use of the Azure PowerShell console.</span></span>

    <span data-ttu-id="7f906-285">Windows PowerShell ISE와 같은 다른 호스트 프로그램에서 작업하려는 경우 가져오기 [모듈](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet을 사용하여 Azure 모듈을 가져오거나 Azure 모듈의 명령을 사용하여 모듈의 자동 가져오기를 트리거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-285">If you prefer to work in a different host program, such as Windows PowerShell ISE, be sure to use the [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet to import the Azure module or use a command in the Azure module to trigger automatic importing of the module.</span></span>
2. <span data-ttu-id="7f906-286">**관리자로 실행** 옵션을 사용 하 고 Azure PowerShell을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-286">Start Azure PowerShell with the **Run as administrator** option.</span></span>
3. <span data-ttu-id="7f906-287">Azure PowerShell 실행 정책을 로 설정하려면 [실행 정책](https://go.microsoft.com/fwlink/p/?linkid=293941) `RemoteSigned`설정 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-287">Run the [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet to set the Azure PowerShell execution policy to `RemoteSigned`.</span></span> <span data-ttu-id="7f906-288">정책 **Y** 변경을 완료하려면 Y(예)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-288">Enter **Y** (for Yes) to complete the policy change.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    <span data-ttu-id="7f906-289">이 설정을 사용하면 디지털 서명되지 않은 로컬 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-289">This setting enables you to run local scripts that aren't digitally signed.</span></span> <span data-ttu-id="7f906-290">(나중에 차단 해제 단계가 `Unrestricted`필요하지 않은 을 으로 실행 정책을 설정할 수도 있지만 보안상의 이유로는 권장되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="7f906-290">(You can also set the execution policy to `Unrestricted`, which would eliminate the need for the unblock step later, but this is not recommended for security reasons.)</span></span>
4. <span data-ttu-id="7f906-291">cmdlet을 `Add-AzureAccount` 실행하여 계정에 대한 자격 증명을 사용하여 PowerShell을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-291">Run the `Add-AzureAccount` cmdlet to set up PowerShell with credentials for your account.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    <span data-ttu-id="7f906-292">이러한 자격 증명은 시간이 지나면 만료되며 cmdlet을 `Add-AzureAccount` 다시 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-292">These credentials expire after a period of time and you have to re-run the `Add-AzureAccount` cmdlet.</span></span> <span data-ttu-id="7f906-293">이 전자책을 작성할 때 자격 증명이 만료되기 까지의 시간 제한은 12시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-293">As this e-book is being written, the time limit before credentials expire is 12 hours.</span></span>
5. <span data-ttu-id="7f906-294">구독이 여러 개인 경우 Select-AzureSubscription cmdlet을 사용하여 테스트 환경을 만들 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-294">If you have multiple subscriptions, use the Select-AzureSubscription cmdlet to specify the subscription you want to create the test environment in.</span></span>
6. <span data-ttu-id="7f906-295">및 `Import-AzurePublishSettingsFile` cmdlet을 사용하여 동일한 Azure `Get-AzurePublishSettingsFile` 구독에 대한 관리 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-295">Import a management certificate for the same Azure subscription by using the `Get-AzurePublishSettingsFile` and `Import-AzurePublishSettingsFile` cmdlets.</span></span> <span data-ttu-id="7f906-296">이러한 cmdlet 중 첫 번째는 인증서 파일을 다운로드하고 두 번째 cmdlet에서는 인증서 파일을 가져오기 위해 해당 파일의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-296">The first of these cmdlets downloads a certificate file, and in the second one you specify the location of that file in order to import it.</span></span> > [!IMPORTANT]
   > <span data-ttu-id="7f906-297">다운로드한 파일을 안전한 위치에 보관하거나 Azure 서비스를 관리하는 데 사용할 수 있는 인증서가 포함되어 있으므로 파일을 완료하면 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-297">Keep the downloaded file in a safe location or delete it when you're done with it, because it contains a certificate that can be used to manage your Azure services.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    <span data-ttu-id="7f906-298">이 인증서는 SQL Database 서버에서 방화벽 규칙을 설정하기 위해 개발 컴퓨터의 IP 주소를 검색하는 REST API 호출에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-298">The certificate is used for a REST API call that detects the development machine's IP address in order to set a firewall rule on the SQL Database server.</span></span>
7. <span data-ttu-id="7f906-299">설정 [위치](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet(별칭은 `cd`, `chdir`및)을 `sl`실행하여 스크립트가 포함된 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-299">Run the [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (aliases are `cd`, `chdir`, and `sl`) to navigate to the directory that contains the scripts.</span></span> <span data-ttu-id="7f906-300">수정 솔루션 폴더의 *자동화* 폴더에 있습니다. 디렉터리 이름에 공백이 있는 경우 경로를 따옴표로 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-300">(They're located in the *Automation* folder in the Fix It solution folder.) Put the path in quotes if any of the directory names contain spaces.</span></span> <span data-ttu-id="7f906-301">예를 들어 `c:\Sample Apps\FixIt\Automation` 디렉터리로 이동하려면 다음 명령을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-301">For example, to navigate to the `c:\Sample Apps\FixIt\Automation` directory you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. <span data-ttu-id="7f906-302">Windows PowerShell에서 이러한 스크립트를 실행할 수 있도록 하려면 [파일 차단 해제](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-302">To allow Windows PowerShell to run these scripts, use the [Unblock-File](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet.</span></span> <span data-ttu-id="7f906-303">스크립트는 인터넷에서 다운로드했기 때문에 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-303">(The scripts are blocked because they were downloaded from the Internet.)</span></span>

    > [!WARNING]
    > <span data-ttu-id="7f906-304">보안 - `Unblock-File` 스크립트 또는 실행 파일에서 실행하기 전에 메모장에서 파일을 열고 명령을 검사하고 악성 코드가 포함되어 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-304">Security - Before running `Unblock-File` on any script or executable file, open the file in Notepad, examine the commands, and verify that they do not contain any malicious code.</span></span>

    <span data-ttu-id="7f906-305">예를 들어 다음 명령은 `Unblock-File` 현재 디렉터리에서 모든 스크립트에서 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-305">For example, the following command runs the `Unblock-File` cmdlet on all scripts in the current directory.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. <span data-ttu-id="7f906-306">기본에 대한 웹 앱을 만들려면(큐 처리 없음) Fix It 앱은 환경 만들기 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-306">To create the web app for the base (no queues processing) Fix It app, run the environment creation script.</span></span>

    <span data-ttu-id="7f906-307">필수 `Name` 매개 변수는 데이터베이스 이름을 지정하고 스크립트가 만드는 저장소 계정에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-307">The required `Name` parameter specifies the name of the database and is also used for the storage account that the script creates.</span></span> <span data-ttu-id="7f906-308">이름은 azurewebsites.net 도메인 내에서 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-308">The name must be globally unique within the azurewebsites.net domain.</span></span> <span data-ttu-id="7f906-309">Fixit 또는 Test와 같이 고유하지 않은 이름을 지정하는 경우(또는 예제에서와 `New-AzureWebsite` 같이 fixitdemo) cmdlet은 충돌을 보고하는 내부 오류와 함께 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-309">If you specify a name that is not unique, like Fixit or Test (or even as in the example, fixitdemo), the `New-AzureWebsite` cmdlet fails with an Internal Error that reports a conflict.</span></span> <span data-ttu-id="7f906-310">스크립트는 웹 앱, 저장소 계정 및 데이터베이스에 대한 이름 요구 사항을 준수하도록 이름을 모든 소문자로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-310">The script converts the name to all lower-case to comply with name requirements for web apps, storage accounts, and databases.</span></span>

    <span data-ttu-id="7f906-311">필요한 `SqlDatabasePassword` 매개 변수는 SQL Database에 대해 만들어질 관리자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-311">The required `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="7f906-312">암호(;)특수&amp; &lt; &gt; XML 문자를 포함하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="7f906-312">Don't include special XML characters in the password (&amp; &lt; &gt; ;).</span></span> <span data-ttu-id="7f906-313">이는 Azure의 제한이 아니라 스크립트를 작성한 방식의 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-313">This is a limitation of the way the scripts were written, not a limitation of Azure.</span></span>

    <span data-ttu-id="7f906-314">예를 들어 "fixitdemo"라는 웹 앱을 만들고 "Passw0rd1"의 SQL Server 관리자 암호를 사용하려는 경우 다음 명령을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-314">For example, if you want to create a web app named "fixitdemo" and use a SQL Server administrator password of "Passw0rd1", you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    <span data-ttu-id="7f906-315">이름은 azurewebsites.net 도메인에서 고유해야 하며 암호가 암호 복잡성에 대한 SQL Database 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-315">The name must be unique in the azurewebsites.net domain, and the password must meet SQL Database requirements for password complexity.</span></span> <span data-ttu-id="7f906-316">(Passw0rd1 예제는 요구 사항을 충족합니다.)</span><span class="sxs-lookup"><span data-stu-id="7f906-316">(The example Passw0rd1 does meet the requirements.)</span></span>

    <span data-ttu-id="7f906-317">명령은 "로 시작합니다. \".</span><span class="sxs-lookup"><span data-stu-id="7f906-317">Note that the command begins with ".\".</span></span> <span data-ttu-id="7f906-318">스크립트의 악의적인 실행을 방지하려면 Windows PowerShell에서 스크립트를 실행할 때 스크립트 파일에 대한 정규화된 경로를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-318">To help prevent malicious execution of scripts, Windows PowerShell requires that you provide the fully qualified path to the script file when you run a script.</span></span> <span data-ttu-id="7f906-319">점을 사용하여 현재 디렉터리(")를 나타낼\"수 있습니다. 또는 다음과 같이 정규화된 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-319">You can use a dot to indicate the current directory (".\") or provide the fully qualified path, such as:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    <span data-ttu-id="7f906-320">스크립트에 대한 자세한 내용은 `Get-Help` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-320">For more information about the script, use the `Get-Help` cmdlet.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    <span data-ttu-id="7f906-321">[의 `Detailed`에서 `Full`, `Parameters` `Examples`</span><span class="sxs-lookup"><span data-stu-id="7f906-321">You can use the `Detailed`, `Full`, `Parameters`, and `Examples` parameters of the Get-Help cmdlet to filter the help that is returned.</span></span>

    <span data-ttu-id="7f906-322">스크립트가 실패하거나 "새-AzureWebsite : 호출 집합-AzureSubscription 및 Select-AzureSubscription 첫 번째"와 같은 오류를 생성하는 경우 Azure PowerShell의 구성을 완료하지 않았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-322">If the script fails or generates errors, such as "New-AzureWebsite : Call Set-AzureSubscription and Select-AzureSubscription first," you might not have completed the configuration of Azure PowerShell.</span></span>

    <span data-ttu-id="7f906-323">스크립트가 완료되면 Azure 관리 포털을 사용하여 [모든](automate-everything.md) 자동화 장과 같이 생성된 리소스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-323">After the script finishes, you can use the Azure Management Portal to see the resources that were created, as shown in the [Automate Everything](automate-everything.md) chapter.</span></span>
10. <span data-ttu-id="7f906-324">새 Azure 환경에 FixIt 프로젝트를 배포하려면 *AzureWebsite.ps1* 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-324">To deploy the FixIt project to the new Azure environment, use the *AzureWebsite.ps1* script.</span></span> <span data-ttu-id="7f906-325">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="7f906-325">For example:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    <span data-ttu-id="7f906-326">배포가 완료되면 브라우저가 Azure에서 실행되는 Fix It으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-326">When deployment is done, the browser opens with Fix It running in Azure.</span></span>

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a><span data-ttu-id="7f906-327">Windows PowerShell 스크립트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7f906-327">Troubleshooting the Windows PowerShell scripts</span></span>

<span data-ttu-id="7f906-328">이러한 스크립트를 실행할 때 발생하는 가장 일반적인 오류는 사용 권한과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-328">The most common errors encountered when running these scripts are related to permissions.</span></span> <span data-ttu-id="7f906-329">`Add-AzureAccount` 동일한 `Import-AzurePublishSettingsFile` Azure 구독에 사용했는지 확인하고 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-329">Make sure that `Add-AzureAccount` and `Import-AzurePublishSettingsFile` were successful and that you used them for the same Azure subscription.</span></span> <span data-ttu-id="7f906-330">성공한 `Add-AzureAccount` 경우에도 다시 실행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-330">Even if `Add-AzureAccount` was successful you might have to run it again.</span></span> <span data-ttu-id="7f906-331">추가된 `Add-AzureAccount` 권한은 12시간 만에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-331">The permissions added by `Add-AzureAccount` expire in 12 hours.</span></span>

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a><span data-ttu-id="7f906-332">개체 참조가 개체의 인스턴스로 설정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-332">Object reference not set to an instance of an object.</span></span>

<span data-ttu-id="7f906-333">스크립트가 "개체 참조가 개체의 인스턴스로 설정되지 않음"과 같은 오류를 반환하는 경우 Windows PowerShell은 처리할 개체를 찾을 `Add-AzureAccount` 수 없습니다(null 참조 예외)는 cmdlet을 실행하고 스크립트를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-333">If the script returns errors, such as "Object reference not set to an instance of an object," which means that Windows PowerShell can't find an object to process (this is a null reference exception), run the `Add-AzureAccount` cmdlet and try the script again.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a><span data-ttu-id="7f906-334">내부 오류: 서버에 내부 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-334">InternalError: The server encountered an internal error.</span></span>

<span data-ttu-id="7f906-335">cmdlet은 `New-AzureWebsite` azurewebsites.net 도메인에서 이름이 고유하지 않은 경우 내부 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-335">The `New-AzureWebsite` cmdlet returns an internal error when the name is not unique in the azurewebsites.net domain.</span></span> <span data-ttu-id="7f906-336">오류를 해결하려면 *New-AzureWebsiteEnv.ps1의*이름 매개 변수에 있는 이름에 대해 다른 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-336">To resolve the error, use a different value for the name, which is in the Name parameter of *New-AzureWebsiteEnv.ps1*.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a><span data-ttu-id="7f906-337">스크립트 다시 시작</span><span class="sxs-lookup"><span data-stu-id="7f906-337">Restarting the script</span></span>

<span data-ttu-id="7f906-338">"스크립트가 완료되었습니다" 메시지를 인쇄하기 전에 실패했기 때문에 *New-AzureWebsiteEnv.ps1* 스크립트를 다시 시작해야 하는 경우 스크립트가 중지되기 전에 만든 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-338">If you need to restart the *New-AzureWebsiteEnv.ps1* script because it failed before it printed the "Script is complete" message, you might want to delete resources that the script created before it stopped.</span></span> <span data-ttu-id="7f906-339">예를 들어 스크립트가 이미 ContosoFixItDemo 웹 앱을 만든 다음 동일한 이름으로 스크립트를 다시 실행하는 경우 이름이 사용 중이기 때문에 스크립트가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-339">For example, if the script already created the ContosoFixItDemo web app and you run the script again with the same name, the script will fail because the name is in use.</span></span>

<span data-ttu-id="7f906-340">스크립트가 중지되기 전에 만든 리소스를 확인하려면 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-340">To determine which resources the script created before it stopped, use the following cmdlets:</span></span>

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- <span data-ttu-id="7f906-341">`Get-AzureSqlDatabase`: 이 cmdlet을 실행하려면 데이터베이스 `Get-AzureSqlDatabase`서버 이름을 다음으로 파이프합니다.`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span><span class="sxs-lookup"><span data-stu-id="7f906-341">`Get-AzureSqlDatabase`: To run this cmdlet, pipe the database server name to `Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span></span>

<span data-ttu-id="7f906-342">이러한 리소스를 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-342">To delete these resources, use the following commands.</span></span> <span data-ttu-id="7f906-343">데이터베이스 서버를 삭제하면 서버와 연결된 데이터베이스가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-343">Note that if you delete the database server, you automatically delete the databases associated with the server.</span></span>

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a><span data-ttu-id="7f906-344">Azure 앱 서비스 웹 앱 및 Azure 클라우드 서비스에 큐 처리를 사용하여 앱을 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="7f906-344">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>

<span data-ttu-id="7f906-345">큐를 사용하려면 MyFixIt\Web.config 파일에서 다음을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-345">To enable queues, make the following change in the MyFixIt\Web.config file.</span></span> <span data-ttu-id="7f906-346">에서 `appSettings`값 `UseQueues` "true"로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-346">Under `appSettings`, change the value of `UseQueues` to "true":</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

<span data-ttu-id="7f906-347">그런 다음 [앞에서](#deploybase)설명한 대로 Azure 앱 서비스의 웹 앱에 MVC 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-347">Then deploy the MVC application to an web app in Azure App Service, as described [earlier](#deploybase).</span></span>

<span data-ttu-id="7f906-348">다음으로 새 Azure 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-348">Next, create a new Azure cloud service.</span></span> <span data-ttu-id="7f906-349">Fix It 앱에 포함된 스크립트는 클라우드 서비스를 만들거나 배포하지 않으므로 이를 위해 Azure 포털을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-349">The scripts included with the Fix It app do not create or deploy the cloud service, so you must use Azure portal for this.</span></span> <span data-ttu-id="7f906-350">포털에서 **새** -- **계산** - **클라우드 서비스** -- **빠른 만들기를**클릭한 다음 URL과 데이터 센터 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-350">In the portal, click **New** -- **Compute** – **Cloud Service** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="7f906-351">웹 앱을 배포한 것과 동일한 데이터 센터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-351">Use the same data center where you deployed the web app.</span></span>

![](the-fix-it-sample-application/_static/image1.png)

<span data-ttu-id="7f906-352">클라우드 서비스를 배포하려면 일부 구성 파일을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-352">Before you can deploy the cloud service, you need to update some of the configuration files.</span></span>

<span data-ttu-id="7f906-353">MyFixIt.WorkerRole\app.config에서 아래에서 `connectionStrings` `appdb` 연결 문자열의 값을 SQL Database의 실제 연결 문자열로 바꿉습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-353">In MyFixIt.WorkerRole\app.config, under `connectionStrings`, replace the value of the `appdb` connection string with the actual connection string for the SQL Database.</span></span> <span data-ttu-id="7f906-354">포털에서 연결 문자열을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-354">You can get the connection string from the portal.</span></span> <span data-ttu-id="7f906-355">포털에서 - **ADO .Net, ODBC, PHP 및 JDBC에 대한 SQL** - **Databaseappdb**보기 SQL 데이터베이스 연결 문자열을 클릭합니다. **SQL Databases**</span><span class="sxs-lookup"><span data-stu-id="7f906-355">In the portal, click **SQL Databases** - **appdb** - **View SQL Database connection strings for ADO .Net, ODBC, PHP, and JDBC**.</span></span> <span data-ttu-id="7f906-356">ADO.NET 연결 문자열을 복사하고 app.config 파일에 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-356">Copy the ADO.NET connection string and paste the value into the app.config file.</span></span> <span data-ttu-id="7f906-357">"여기에서\_암호{}"를\_데이터베이스 암호로 바꿉습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-357">Replace "{your\_password\_here}" with your database password.</span></span> <span data-ttu-id="7f906-358">스크립트를 사용하여 MVC 앱을 배포했다고 가정하면 `SqlDatabasePassword` 스크립트 매개 변수에 데이터베이스 암호를 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-358">(Assuming you used the scripts to deploy the MVC app, you specified the database password in the `SqlDatabasePassword` script parameter.)</span></span>

<span data-ttu-id="7f906-359">결과는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-359">The result should look like the following:</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

<span data-ttu-id="7f906-360">동일한 MyFixIt.WorkerRole\app.config 파일에서 `appSettings`Azure 저장소 계정에 대한 두 자리 표시자 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-360">In the same MyFixIt.WorkerRole\app.config file, under `appSettings`, replace the two placeholder values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

<span data-ttu-id="7f906-361">포털에서 액세스 키를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-361">You can get the access key from the portal.</span></span> <span data-ttu-id="7f906-362">[저장소 계정을 관리하는 방법을](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f906-362">See [How To Manage Storage Accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>

<span data-ttu-id="7f906-363">MyFixItCloudService\ServiceConfiguration.Cloud.cscfg에서 Azure 저장소 계정에 대해 동일한 두 자리 표시자 값을 바꿉습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-363">In MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, replace the same two placeholders values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

<span data-ttu-id="7f906-364">이제 클라우드 서비스를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-364">Now you are ready to deploy the cloud service.</span></span> <span data-ttu-id="7f906-365">솔루션 탐색에서 MyFixItCloudService 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f906-365">In Solution Explore, right-click the MyFixItCloudService project and select **Publish**.</span></span> <span data-ttu-id="7f906-366">자세한 내용은 [이 자습서의](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)2부에 있는["Azure에 응용 프로그램 배포"를](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f906-366">For more information, see "[Deploy the Application to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", which is in part 2 of [this tutorial](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7f906-367">이전</span><span class="sxs-lookup"><span data-stu-id="7f906-367">Previous</span></span>](more-patterns-and-guidance.md)
