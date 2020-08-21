---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: '부록: Fix It 샘플 응용 프로그램 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs'
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 549d1513279190ae5abe87c59a48e1caa1cfa5f7
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702935"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="f958a-104">부록: Fix It 샘플 응용 프로그램 (Azure를 사용 하 여 실제 클라우드 앱 빌드)</span><span class="sxs-lookup"><span data-stu-id="f958a-104">Appendix: The Fix It Sample Application (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="f958a-105">사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f958a-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f958a-106">Fix It 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="f958a-106">Download The Fix It Project</span></span>](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> <span data-ttu-id="f958a-107">Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="f958a-108">클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="f958a-109">전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f958a-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="f958a-110">Azure를 사용 하 여 실제 클라우드 앱 빌드에 대 한이 부록에는 다운로드할 수 있는 Fix It 샘플 응용 프로그램에 대 한 추가 정보를 제공 하는 다음 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-110">This appendix to the Building Real World Cloud Apps with Azure e-book contains the following sections that provide additional information about the Fix It sample application that you can download:</span></span>

- [<span data-ttu-id="f958a-111">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="f958a-111">Known issues</span></span>](#knownissues)
- [<span data-ttu-id="f958a-112">모범 사례</span><span class="sxs-lookup"><span data-stu-id="f958a-112">Best practices</span></span>](#bestpractices)
- [<span data-ttu-id="f958a-113">로컬 컴퓨터의 Visual Studio에서 앱을 실행 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f958a-113">How to run the app from Visual Studio on your local computer</span></span>](#run-in-vs)
- [<span data-ttu-id="f958a-114">Windows PowerShell 스크립트를 사용 하 여 Azure App Service Web Apps에 기본 앱을 배포 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f958a-114">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>](#deploybase)
- [<span data-ttu-id="f958a-115">Windows PowerShell 스크립트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f958a-115">Troubleshooting the Windows PowerShell scripts</span></span>](#troubleshooting)
- [<span data-ttu-id="f958a-116">큐 처리를 사용 하 여 앱을 배포 하 여 Web Apps 및 Azure 클라우드 서비스를 Azure App Service 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f958a-116">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a><span data-ttu-id="f958a-117">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="f958a-117">Known issues</span></span>

<span data-ttu-id="f958a-118">이 설명서에 제공 된 패턴 중 일부를 가능한 한 간단 하 게 보여 주기 위해 Fix It 앱이 원래 개발 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-118">The Fix It app was originally developed in order to illustrate as simply as possible some of the patterns presented in this e-book.</span></span> <span data-ttu-id="f958a-119">그러나이 문서에서는 실제 앱을 빌드하는 데 대 한 정보를 제공 하기 때문에 릴리스 소프트웨어에 대해 수행 했던 것과 비슷한 검토 및 테스트 프로세스에 대 한 수정 It 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-119">However, since the e-book is about building real-world apps, we subjected the Fix It code to a review and testing process similar to what we'd do for released software.</span></span> <span data-ttu-id="f958a-120">모든 실제 응용 프로그램에서와 마찬가지로 몇 가지 문제가 발견 되었으며 일부는 수정 하 고 그 중 일부는 이후 릴리스로 연기 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-120">We found a number of issues, and as with any real-world application, some of them we fixed and some of them we deferred to a later release.</span></span>

<span data-ttu-id="f958a-121">다음 목록은 프로덕션 응용 프로그램에서 해결 해야 하는 문제를 포함 하지만, 한 가지 이유 또는 Fix It 샘플 응용 프로그램의 초기 릴리스에서 해결 하지 않기로 결정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-121">The following list includes issues that should be addressed in a production application, but for one reason or another we decided not to address in the initial release of the Fix It sample application.</span></span>

### <a name="security"></a><span data-ttu-id="f958a-122">보안</span><span class="sxs-lookup"><span data-stu-id="f958a-122">Security</span></span>

- <span data-ttu-id="f958a-123">존재 하지 않는 소유자에 게 작업을 할당할 수 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-123">Ensure that you can't assign a task to a non-existent owner.</span></span>
- <span data-ttu-id="f958a-124">사용자가 만들었거나 할당 한 작업만 보고 수정할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-124">Ensure that you can only view and modify tasks that you created or are assigned to you.</span></span>
- <span data-ttu-id="f958a-125">로그인 페이지 및 인증 쿠키에 HTTPS를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-125">Use HTTPS for sign-in pages and authentication cookies.</span></span>
- <span data-ttu-id="f958a-126">인증 쿠키에 대 한 시간 제한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-126">Specify a time limit for authentication cookies.</span></span>

### <a name="input-validation"></a><span data-ttu-id="f958a-127">입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="f958a-127">Input validation</span></span>

<span data-ttu-id="f958a-128">일반적으로 프로덕션 앱은 Fix It 앱 보다 더 많은 입력 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-128">In general, a production app would do more input validation than the Fix It app.</span></span> <span data-ttu-id="f958a-129">예를 들어 업로드에 허용 되는 이미지 크기/이미지 파일 크기를 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-129">For example, the image size / image file size allowed for upload should be limited.</span></span>

### <a name="administrator-functionality"></a><span data-ttu-id="f958a-130">관리자 기능</span><span class="sxs-lookup"><span data-stu-id="f958a-130">Administrator functionality</span></span>

<span data-ttu-id="f958a-131">관리자는 기존 태스크에 대 한 소유권을 변경할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-131">An administrator should be able to change ownership on existing tasks.</span></span> <span data-ttu-id="f958a-132">예를 들어 관리 액세스를 사용 하도록 설정 하지 않은 경우 작업을 유지 관리할 수 있는 권한이 없는 작업의 작성자는 회사를 떠날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-132">For example, the creator of a task might leave the company, leaving no one with authority to maintain the task unless administrative access is enabled.</span></span>

### <a name="queue-message-processing"></a><span data-ttu-id="f958a-133">큐 메시지 처리</span><span class="sxs-lookup"><span data-stu-id="f958a-133">Queue message processing</span></span>

<span data-ttu-id="f958a-134">Fix It 앱에서 큐 메시지 처리는 최소한의 코드를 사용 하 여 큐 중심 작업 패턴을 보여 주기 위해 간단 하 게 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-134">Queue message processing in the Fix It app was designed to be simple in order to illustrate the queue-centric work pattern with a minimum amount of code.</span></span> <span data-ttu-id="f958a-135">이 간단한 코드는 실제 프로덕션 응용 프로그램에는 적합 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-135">This simple code would not be adequate for an actual production application.</span></span>

- <span data-ttu-id="f958a-136">이 코드는 각 큐 메시지가 한 번만 처리 되는 것을 보장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-136">The code does not guarantee that each queue message will be processed at most once.</span></span> <span data-ttu-id="f958a-137">큐에서 메시지를 받는 경우 다른 큐 수신기에 메시지가 표시 되지 않는 시간 제한 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-137">When you get a message from the queue, there is a timeout period, during which the message is invisible to other queue listeners.</span></span> <span data-ttu-id="f958a-138">메시지를 삭제 하기 전에 제한 시간이 만료 되 면 메시지가 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-138">If the timeout expires before the message is deleted, the message becomes visible again.</span></span> <span data-ttu-id="f958a-139">따라서 작업자 역할 인스턴스에서 메시지를 처리 하는 데 시간이 오래 걸리는 경우에는 이론적으로 동일한 메시지를 두 번 처리 하 여 데이터베이스에서 중복 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-139">Therefore, if a worker role instance spends a long time processing a message, it is theoretically possible for the same message to get processed twice, resulting in a duplicate task in the database.</span></span> <span data-ttu-id="f958a-140">이 문제에 대 한 자세한 내용은 [Azure Storage 큐 사용](https://msdn.microsoft.com/library/ff803365.aspx#sec7)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f958a-140">For more information about this issue, see [Using Azure Storage Queues](https://msdn.microsoft.com/library/ff803365.aspx#sec7).</span></span>
- <span data-ttu-id="f958a-141">큐 폴링 논리는 메시지 검색을 일괄 처리 하 여 더 비용 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-141">The queue polling logic could be more cost-effective, by batching message retrieval.</span></span> <span data-ttu-id="f958a-142">[Cloudqueue. GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)을 호출할 때마다 트랜잭션 비용이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-142">Every time you call [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), there is a transaction cost.</span></span> <span data-ttu-id="f958a-143">대신, 단일 트랜잭션에서 여러 메시지를 가져오는 [GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (복수형의 ')를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-143">Instead, you can call [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (note the plural 's'), which gets multiple messages in a single transaction.</span></span> <span data-ttu-id="f958a-144">Azure Storage 큐에 대 한 트랜잭션 비용은 매우 낮으므로 대부분의 시나리오에서 비용에 미치는 영향은 그다지 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-144">The transaction costs for Azure Storage Queues are very low, so the impact on costs is not substantial in most scenarios.</span></span>
- <span data-ttu-id="f958a-145">큐 메시지 처리 코드에서 루프를 사용 하면 다중 코어 Vm을 효율적으로 활용 하지 않는 CPU 선호도가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-145">The tight loop in the queue message-processing code causes CPU affinity, which does not utilize multi-core VMs efficiently.</span></span> <span data-ttu-id="f958a-146">더 나은 디자인은 작업 병렬 처리를 사용 하 여 여러 비동기 작업을 병렬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-146">A better design would use task parallelism to run several async tasks in parallel.</span></span>
- <span data-ttu-id="f958a-147">큐 메시지 처리에는 기초적인 예외 처리만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-147">Queue message-processing has only rudimentary exception handling.</span></span> <span data-ttu-id="f958a-148">예를 들어 코드는 [포이즌 메시지](https://msdn.microsoft.com/library/ms789028.aspx)를 처리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-148">For example, the code doesn't handle [poison messages](https://msdn.microsoft.com/library/ms789028.aspx).</span></span> <span data-ttu-id="f958a-149">메시지 처리 시 예외가 발생 하는 경우 오류를 기록 하 고 메시지를 삭제 해야 합니다. 그렇지 않으면 작업자 역할은 다시 처리를 시도 하 고 루프가 무기한 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-149">(When message processing causes an exception, you have to log the error and delete the message, or the worker role will try to process it again, and the loop will continue indefinitely.)</span></span>

### <a name="sql-queries-are-unbounded"></a><span data-ttu-id="f958a-150">SQL 쿼리는 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-150">SQL queries are unbounded</span></span>

<span data-ttu-id="f958a-151">현재 수정 It 코드는 인덱스 페이지에 대 한 쿼리가 반환할 수 있는 행 수에 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-151">Current Fix It code places no limit on how many rows the queries for Index pages might return.</span></span> <span data-ttu-id="f958a-152">많은 양의 작업을 데이터베이스에 입력 하는 경우 수신 된 결과 목록의 크기가 성능 문제를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-152">If a large volume of tasks is entered into the database, the size of the resulting lists received could cause performance issues.</span></span> <span data-ttu-id="f958a-153">이 솔루션은 페이징을 구현 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-153">The solution is to implement paging.</span></span> <span data-ttu-id="f958a-154">예제를 보려면 [ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 정렬, 필터링 및 페이징](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f958a-154">For an example, see [Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span></span>

### <a name="view-models-recommended"></a><span data-ttu-id="f958a-155">모델 보기 권장</span><span class="sxs-lookup"><span data-stu-id="f958a-155">View models recommended</span></span>

<span data-ttu-id="f958a-156">Fix It 앱은 FixItTask 엔터티 클래스를 사용 하 여 컨트롤러와 뷰 간에 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-156">The Fix It app uses the FixItTask entity class to pass information between the controller and the view.</span></span> <span data-ttu-id="f958a-157">모범 사례는 보기 모델을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-157">A best practice is to use view models.</span></span> <span data-ttu-id="f958a-158">도메인 모델 (예: FixItTask 엔터티 클래스)은 데이터를 지 원하는 데 필요한 항목을 중심으로 디자인 되었으며, 데이터를 표시 하기 위해 뷰 모델을 디자인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-158">The domain model (e.g., the FixItTask entity class) is designed around what is needed for data persistence, while a view model can be designed for data presentation.</span></span> <span data-ttu-id="f958a-159">자세한 내용은 [12 ASP.NET MVC 모범 사례](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f958a-159">For more information, see [12 ASP.NET MVC Best Practices](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).</span></span>

### <a name="secure-image-blob-recommended"></a><span data-ttu-id="f958a-160">보안 이미지 blob 권장</span><span class="sxs-lookup"><span data-stu-id="f958a-160">Secure image blob recommended</span></span>

<span data-ttu-id="f958a-161">Fix It 앱은 업로드 된 이미지를 공개로 저장 합니다. 즉, URL을 찾는 사람이 이미지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-161">The Fix It app stores uploaded images as public, meaning that anyone who finds the URL can access the images.</span></span> <span data-ttu-id="f958a-162">이미지는 공용이 아닌 보안을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-162">The images could be secured instead of public.</span></span>

### <a name="no-powershell-automation-scripts-for-queues"></a><span data-ttu-id="f958a-163">큐에 대 한 PowerShell automation 스크립트가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-163">No PowerShell automation scripts for queues</span></span>

<span data-ttu-id="f958a-164">샘플 PowerShell 자동화 스크립트는 전체 Azure App Service Web Apps에서 실행 되는 Fix의 기본 버전용으로 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-164">Sample PowerShell automation scripts were written only for the base version of Fix It that runs entirely in Azure App Service Web Apps.</span></span> <span data-ttu-id="f958a-165">웹 앱을 설정 하 고 배포 하는 데 필요한 스크립트를 제공 하지 않았습니다. 큐 처리에 필요한 클라우드 서비스 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-165">We haven't provided scripts for setting up and deploying to the web app plus Cloud Service environment required for queue processing.</span></span>

### <a name="special-handling-for-html-codes-in-user-input"></a><span data-ttu-id="f958a-166">사용자 입력의 HTML 코드에 대 한 특수 처리</span><span class="sxs-lookup"><span data-stu-id="f958a-166">Special handling for HTML codes in user input</span></span>

<span data-ttu-id="f958a-167">ASP.NET는 악의적인 사용자가 사용자 입력 텍스트 상자에 스크립트를 입력 하 여 사이트 간 스크립팅 공격을 시도할 수 있는 여러 가지 방법을 자동으로 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-167">ASP.NET automatically prevents many ways in which malicious users might attempt cross-site scripting attacks by entering script in user input text boxes.</span></span> <span data-ttu-id="f958a-168">그리고 `DisplayFor` 작업 제목과 메모를 표시 하는 데 사용 되는 MVC 도우미는 브라우저에 보내는 값을 자동으로 HTML 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-168">And the MVC `DisplayFor` helper used to display task titles and notes automatically HTML-encodes values that it sends to the browser.</span></span> <span data-ttu-id="f958a-169">그러나 프로덕션 앱에서는 추가 측정을 수행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-169">But in a production app you might want to take additional measures.</span></span> <span data-ttu-id="f958a-170">자세한 내용은 [ASP.NET의 요청 유효성 검사](https://msdn.microsoft.com/library/hh882339.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f958a-170">For more information, see [Request Validation in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).</span></span>

<a id="bestpractices"></a>
## <a name="best-practices"></a><span data-ttu-id="f958a-171">모범 사례</span><span class="sxs-lookup"><span data-stu-id="f958a-171">Best practices</span></span>

<span data-ttu-id="f958a-172">다음은 코드 검토에서 검색 된 후 수정 된 문제 및 Fix It 앱의 원래 버전에 대 한 테스트입니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-172">Following are some issues that were fixed after being discovered in code review and testing of the original version of the Fix It app.</span></span> <span data-ttu-id="f958a-173">일부는 코드를 신속 하 게 작성 하 고 릴리스 소프트웨어를 사용 하기 위한 것이 아니라 원래 코드 작성자 있는지 특정 모범 사례를 인식 하지 못하기 때문에 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-173">Some were caused by the original coder not being aware of a particular best practice, some simply because the code was written quickly and wasn't intended for released software.</span></span> <span data-ttu-id="f958a-174">웹 앱을 개발 하는 다른 사용자에 게 도움이 될 수 있는이 검토 및 테스트에서 배운 내용이 있는 경우 여기에서 문제를 나열 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-174">We're listing the issues here in case there's something we learned from this review and testing that might be helpful to others who are also developing web apps.</span></span>

### <a name="dispose-the-database-repository"></a><span data-ttu-id="f958a-175">데이터베이스 리포지토리를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-175">Dispose the database repository</span></span>

<span data-ttu-id="f958a-176">`FixItTaskRepository`클래스는 Entity Framework 인스턴스를 삭제 해야 합니다 `DbContext` .</span><span class="sxs-lookup"><span data-stu-id="f958a-176">The `FixItTaskRepository` class must dispose the Entity Framework `DbContext` instance.</span></span> <span data-ttu-id="f958a-177">클래스에서를 구현 하 여이 작업을 수행 했습니다 `IDisposable` `FixItTaskRepository` .</span><span class="sxs-lookup"><span data-stu-id="f958a-177">We did this by implementing `IDisposable` in the `FixItTaskRepository` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

<span data-ttu-id="f958a-178">AutoFac는 인스턴스를 자동으로 삭제 `FixItTaskRepository` 하므로 명시적으로 삭제할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-178">Note that AutoFac will automatically dispose the `FixItTaskRepository` instance, so we don't need to explicitly dispose it.</span></span>

<span data-ttu-id="f958a-179">또 다른 옵션은 `DbContext` 에서 멤버 변수를 제거 하 `FixItTaskRepository` 고 대신 `DbContext` 문 내에서 각 리포지토리 메서드 내에 지역 변수를 만드는 `using` 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-179">Another option is to remove the `DbContext` member variable from `FixItTaskRepository`, and instead create a local `DbContext` variable within each repository method, inside a `using` statement.</span></span> <span data-ttu-id="f958a-180">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-180">For example:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a><span data-ttu-id="f958a-181">DI를 사용 하 여 단일 항목를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-181">Register singletons as such with DI</span></span>

<span data-ttu-id="f958a-182">클래스 및 클래스의 인스턴스는 하나만 `PhotoService` `Logger` 필요 하므로 이러한 클래스는 *DependenciesConfig.cs*의 [종속성 주입에 대 한 단일 인스턴스로 등록](https://code.google.com/p/autofac/wiki/InstanceScope) 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-182">Since only one instance of the `PhotoService` class and `Logger` class is needed, these classes should be [registered as single instances for dependency injection](https://code.google.com/p/autofac/wiki/InstanceScope) in *DependenciesConfig.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a><span data-ttu-id="f958a-183">보안: 사용자에 게 오류 정보를 표시 하지 않음</span><span class="sxs-lookup"><span data-stu-id="f958a-183">Security: Don't show error details to users</span></span>

<span data-ttu-id="f958a-184">원래 Fix It 앱에는 일반 오류 페이지가 없으며 모든 예외를 UI로 버블링 하므로 데이터베이스 연결 오류와 같은 일부 예외 때문에 브라우저에 전체 스택 추적이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-184">The original Fix It app didn't have a generic error page and just let all exceptions bubble up to the UI, so some exceptions such as database connection errors could result in a full stack trace being displayed to the browser.</span></span> <span data-ttu-id="f958a-185">자세한 오류 정보는 악의적인 사용자의 공격을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-185">Detailed error information can sometimes facilitate attacks by malicious users.</span></span> <span data-ttu-id="f958a-186">해결 방법은 예외 정보를 기록 하 고 오류 세부 정보를 포함 하지 않는 오류 페이지를 사용자에 게 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-186">The solution is to log the exception details and display an error page to the user that doesn't include error details.</span></span> <span data-ttu-id="f958a-187">Fix It 앱은 이미 로깅 되었으며 오류 페이지를 표시 하기 위해 `<customErrors mode=On>` Web.config 파일에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-187">The Fix It app was already logging, and in order to display an error page, we added `<customErrors mode=On>` in the Web.config file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

<span data-ttu-id="f958a-188">이 경우 기본적으로 오류에 대해 *Views\Shared\Error.cshtml* 가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-188">By default this causes *Views\Shared\Error.cshtml* to be displayed for errors.</span></span> <span data-ttu-id="f958a-189">오류를 사용자 지정할 수 있습니다 *. cshtml* 또는 고유한 오류 페이지 보기를 만들고 특성을 추가 `defaultRedirect` 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-189">You can customize *Error.cshtml* or create your own error page view and add a `defaultRedirect` attribute.</span></span> <span data-ttu-id="f958a-190">특정 오류에 대해 서로 다른 오류 페이지를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-190">You can also specify different error pages for specific errors.</span></span>

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a><span data-ttu-id="f958a-191">보안: 작성자만 작업을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-191">Security: only allow a task to be edited by its creator</span></span>

<span data-ttu-id="f958a-192">대시보드 인덱스 페이지에는 로그온 한 사용자가 만든 작업만 표시 되지만 악의적인 사용자가 다른 사용자의 작업에 대 한 ID를 사용 하 여 URL을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-192">The Dashboard Index page only shows tasks created by the logged-on user, but a malicious user could create a URL with an ID to another user's task.</span></span> <span data-ttu-id="f958a-193">이 경우 404을 반환 하는 코드를 *DashboardController.cs* 에 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-193">We added code in *DashboardController.cs* to return a 404 in that case:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a><span data-ttu-id="f958a-194">예외를 무시 안 함</span><span class="sxs-lookup"><span data-stu-id="f958a-194">Don't swallow exceptions</span></span>

<span data-ttu-id="f958a-195">원본 Fix It 앱은 SQL 쿼리에서 발생 한 예외를 기록한 후에만 null을 반환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-195">The original Fix It app just returned null after logging an exception that resulted from a SQL query:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

<span data-ttu-id="f958a-196">이렇게 하면 쿼리가 성공 했지만 행을 반환 하지 않은 것 처럼 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-196">This would make it look to the user as if the query succeeded but just didn't return any rows.</span></span> <span data-ttu-id="f958a-197">솔루션은 catch 및 로깅 후 예외를 다시 throw 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-197">Solution is to re-throw the exception after catching and logging:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a><span data-ttu-id="f958a-198">작업자 역할의 모든 예외 Catch</span><span class="sxs-lookup"><span data-stu-id="f958a-198">Catch all exceptions in worker roles</span></span>

<span data-ttu-id="f958a-199">작업자 역할에서 처리 되지 않은 예외가 발생 하면 VM이 재활용 되므로 try-catch 블록에서 수행 하는 모든 작업을 래핑하고 모든 예외를 처리 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-199">Any unhandled exceptions in a worker role will cause the VM to be recycled, so you want to wrap everything you do in a try-catch block and handle all exceptions.</span></span>

### <a name="specify-length-for-string-properties-in-entity-classes"></a><span data-ttu-id="f958a-200">엔터티 클래스에서 문자열 속성의 길이 지정</span><span class="sxs-lookup"><span data-stu-id="f958a-200">Specify length for string properties in entity classes</span></span>

<span data-ttu-id="f958a-201">간단한 코드를 표시 하기 위해 원래 버전의 Fix It 앱은 FixItTask 엔터티의 필드에 대해 길이를 지정 하지 않았기 때문에 데이터베이스에서 varchar (max)로 정의 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-201">In order to display simple code, the original version of the Fix It app didn't specify lengths for the fields of the FixItTask entity, and as a result they were defined as varchar(max) in the database.</span></span> <span data-ttu-id="f958a-202">결과적으로 UI에는 거의 모든 양의 입력이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-202">As a result, the UI would accept almost any amount of input.</span></span> <span data-ttu-id="f958a-203">Length를 지정 하면 웹 페이지의 사용자 입력과 데이터베이스의 열 크기에 모두 적용 되는 제한이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-203">Specifying lengths sets limits that apply both to user input in the web page and column size in the database:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a><span data-ttu-id="f958a-204">Private 멤버를 변경할 수 없는 경우 readonly로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-204">Mark private members as readonly when they aren't expected to change</span></span>

<span data-ttu-id="f958a-205">예를 들어 클래스에서 `DashboardController` 인스턴스는 `FixItTaskRepository` 생성 되며 변경 될 것으로 예상 되지 않으므로이를 [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)로 정의 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-205">For example, in the `DashboardController` class an instance of `FixItTaskRepository` is created and isn't expected to change, so we defined it as [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx).</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a><span data-ttu-id="f958a-206">List를 사용 합니다. 목록 대신 Any () Count () &gt; 0</span><span class="sxs-lookup"><span data-stu-id="f958a-206">Use list.Any() instead of list.Count() &gt; 0</span></span>

<span data-ttu-id="f958a-207">목록에 있는 항목 중 하나 이상이 지정 된 조건에 맞는지 확인 하는 것이 가장 중요 한 경우에는 [모든 메서드를](https://msdn.microsoft.com/library/bb534972.aspx) 사용 합니다 .이는 조건에 따라 항목이 발견 되는 즉시 반환 되는 반면, 메서드는 `Count` 항상 모든 항목을 반복 해야 하는 경우에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-207">If you all you care about is whether one or more items in a list fit the specified criteria, use the [Any](https://msdn.microsoft.com/library/bb534972.aspx) method, because it returns as soon as an item fitting the criteria is found, whereas the `Count` method always has to iterate through every item.</span></span> <span data-ttu-id="f958a-208">대시보드 *인덱스 cshtml* 파일에는 원래 다음 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-208">The Dashboard *Index.cshtml* file originally had this code:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

<span data-ttu-id="f958a-209">이를 다음과 같이 변경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-209">We changed it to this:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a><span data-ttu-id="f958a-210">MVC 도우미를 사용 하 여 MVC 뷰에서 Url 생성</span><span class="sxs-lookup"><span data-stu-id="f958a-210">Generate URLs in MVC views using MVC helpers</span></span>

<span data-ttu-id="f958a-211">홈 페이지의 **Fix It 만들기** 단추에 대해 fix it 앱은 앵커 요소를 하드 코딩 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-211">For the **Create a Fix It** button on the home page, the Fix It app hard coded an anchor element:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

<span data-ttu-id="f958a-212">이와 같은 보기/작업 링크의 경우 [Url. action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 도우미를 사용 하는 것이 좋습니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-212">For View/Action links like this it's better to use the [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper, for example:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a><span data-ttu-id="f958a-213">작업자 역할에서 Sleep 대신 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-213">Use Task.Delay instead of Thread.Sleep in worker role</span></span>

<span data-ttu-id="f958a-214">새 프로젝트 템플릿은 `Thread.Sleep` 작업자 역할에 대 한 샘플 코드를 만들지만 스레드를 절전 모드로 전환 하면 스레드 풀에서 불필요 한 추가 스레드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-214">The new-project template puts `Thread.Sleep` in the sample code for a worker role, but causing the thread to sleep can cause the thread pool to spawn additional unnecessary threads.</span></span> <span data-ttu-id="f958a-215">대신, [Delay](https://msdn.microsoft.com/library/hh139096.aspx) 를 사용 하 여이를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-215">You can avoid that by using [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) instead.</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a><span data-ttu-id="f958a-216">비동기 void 방지</span><span class="sxs-lookup"><span data-stu-id="f958a-216">Avoid async void</span></span>

<span data-ttu-id="f958a-217">비동기 메서드가 값을 반환 하지 않아도 되는 경우 대신 형식을 반환 `Task` `void` 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-217">If an async method doesn't need to return a value, return a `Task` type rather than `void`.</span></span>

<span data-ttu-id="f958a-218">이 예제는 클래스에서 가져온 것입니다 `FixItQueueManager` .</span><span class="sxs-lookup"><span data-stu-id="f958a-218">This example is from the `FixItQueueManager` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

<span data-ttu-id="f958a-219">`async void`최상위 이벤트 처리기에만를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-219">You should use `async void` only for top-level event handlers.</span></span> <span data-ttu-id="f958a-220">로 메서드를 정의 하는 경우 호출자는 메서드를 대기 `async void` 하거나 메서드에서 throw 하는 예외를 catch **할** 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-220">If you define a method as `async void`, the caller cannot **await** the method or catch any exceptions the method throws.</span></span> <span data-ttu-id="f958a-221">자세한 내용은 [비동기 프로그래밍의 모범 사례](https://msdn.microsoft.com/magazine/jj991977.aspx)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f958a-221">For more information, see [Best Practices in Asynchronous Programming](https://msdn.microsoft.com/magazine/jj991977.aspx).</span></span>

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a><span data-ttu-id="f958a-222">취소 토큰을 사용 하 여 작업자 역할 루프에서 중단</span><span class="sxs-lookup"><span data-stu-id="f958a-222">Use a cancellation token to break from worker role loop</span></span>

<span data-ttu-id="f958a-223">일반적으로 작업자 역할의 **Run** 메서드는 무한 루프를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-223">Typically, the **Run** method on a worker role contains an infinite loop.</span></span> <span data-ttu-id="f958a-224">작업자 역할을 중지 하면 [Roleentrypoint](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-224">When the worker role is stopping, the [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) method is called.</span></span> <span data-ttu-id="f958a-225">이 메서드를 사용 하 여 **실행** 메서드 내에서 수행 되는 작업을 취소 하 고 정상적으로 종료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-225">You should use this method to cancel the work that is being done inside the **Run** method and exit gracefully.</span></span> <span data-ttu-id="f958a-226">그렇지 않으면 작업이 작업 중간에 종료 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-226">Otherwise, the process might be terminated in the middle of an operation.</span></span>

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a><span data-ttu-id="f958a-227">자동 MIME 스니핑 프로시저 옵트아웃 (Opt out)</span><span class="sxs-lookup"><span data-stu-id="f958a-227">Opt out of Automatic MIME Sniffing Procedure</span></span>

<span data-ttu-id="f958a-228">Internet Explorer에서 웹 서버에 지정 된 형식과 다른 MIME 형식을 보고 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-228">In some cases, Internet Explorer reports a MIME type different than the type specified by the web server.</span></span> <span data-ttu-id="f958a-229">예를 들어, Internet Explorer에서 HTTP 응답 헤더 Content-type과 함께 배달 된 파일의 HTML 콘텐츠를 찾으면 (텍스트/일반) Internet Explorer는 콘텐츠를 HTML로 렌더링 해야 함을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-229">For instance, if Internet Explorer finds HTML content in a file delivered with the HTTP response header Content-Type: text/plain, Internet Explorer determines that the content should be rendered as HTML.</span></span> <span data-ttu-id="f958a-230">아쉽게도이 "MIME 스니핑"은 신뢰할 수 없는 콘텐츠를 호스트 하는 서버에 대 한 보안 문제를 일으킬 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-230">Unfortunately, this "MIME-sniffing" can also lead to security problems for servers hosting untrusted content.</span></span> <span data-ttu-id="f958a-231">Internet Explorer 8은이 문제를 해결 하기 위해 MIME 형식 확인 코드를 다양 하 게 변경 하 고 응용 프로그램 개발자에 게 MIME 검사를 [옵트아웃 (opt out)](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-231">To combat this problem, Internet Explorer 8 has made a number of changes to MIME-type determination code and allows application developers to [opt out of MIME-sniffing](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx).</span></span> <span data-ttu-id="f958a-232">다음 코드가 *Web.config* 파일에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-232">The following code was added to the *Web.config* file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a><span data-ttu-id="f958a-233">묶음 및 축소 사용</span><span class="sxs-lookup"><span data-stu-id="f958a-233">Enable bundling and minification</span></span>

<span data-ttu-id="f958a-234">Visual Studio에서 새 웹 프로젝트를 만들 때 JavaScript 파일의 묶음 및 축소는 기본적으로 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-234">When Visual Studio creates a new web project, bundling and minification of JavaScript files is not enabled by default.</span></span> <span data-ttu-id="f958a-235">BundleConfig.cs에 코드 줄을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-235">We added a line of code in BundleConfig.cs:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a><span data-ttu-id="f958a-236">인증 쿠키에 대 한 만료 시간 제한 설정</span><span class="sxs-lookup"><span data-stu-id="f958a-236">Set an expiration time-out for authentication cookies</span></span>

<span data-ttu-id="f958a-237">기본적으로 인증 쿠키는 2 주 후에 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-237">By default, authentication cookies expire in two weeks.</span></span> <span data-ttu-id="f958a-238">시간이 짧으면 더 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-238">A shorter time is more secure.</span></span> <span data-ttu-id="f958a-239">*StartupAuth.cs*에서이 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-239">You can change this setting in *StartupAuth.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a><span data-ttu-id="f958a-240">로컬 컴퓨터의 Visual Studio에서 앱을 실행 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f958a-240">How to run the app from Visual Studio on your local computer</span></span>

<span data-ttu-id="f958a-241">Fix It 앱을 실행 하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-241">There are two ways to run the Fix It app:</span></span>

- <span data-ttu-id="f958a-242">새 작업을 SQL 데이터베이스에 직접 기록 하는 기본 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-242">Run the base application that writes new tasks directly to the SQL database.</span></span>
- <span data-ttu-id="f958a-243">큐와 백 엔드 서비스를 사용 하 여 응용 프로그램을 실행 하 여 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-243">Run the application using a queue plus a backend service to create tasks.</span></span> <span data-ttu-id="f958a-244">큐 패턴은 [큐 중심 작업 패턴](queue-centric-work-pattern.md)장에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-244">The queue pattern is described in the chapter [Queue-Centric Work Pattern](queue-centric-work-pattern.md).</span></span>

<a id="runbase"></a>
### <a name="run-the-base-application"></a><span data-ttu-id="f958a-245">기본 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f958a-245">Run the base application</span></span>

1. <span data-ttu-id="f958a-246">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-246">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>
2. <span data-ttu-id="f958a-247">[Visual Studio 용 AZURE SDK for .net](https://azure.microsoft.com/downloads/)을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-247">Install the [Azure SDK for .NET for Visual Studio](https://azure.microsoft.com/downloads/).</span></span>
3. <span data-ttu-id="f958a-248">[MSDN 코드 갤러리](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)에서 .zip 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-248">Download the .zip file from the [MSDN Code Gallery](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).</span></span>
4. <span data-ttu-id="f958a-249">파일 탐색기에서 .zip 파일을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 한 다음 속성 창 차단 해제를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-249">In File Explorer, right-click the .zip file and click Properties, then in the Properties window click Unblock.</span></span>
5. <span data-ttu-id="f958a-250">파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-250">Unzip the file.</span></span>
6. <span data-ttu-id="f958a-251">.Sln 파일을 두 번 클릭 하 여 Visual Studio를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-251">Double-click the .sln file to launch Visual Studio.</span></span>
7. <span data-ttu-id="f958a-252">**도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 차례로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-252">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>
8. <span data-ttu-id="f958a-253">패키지 관리자 콘솔 (PMC)에서 복원을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-253">In the Package Manager Console (PMC), click Restore.</span></span>
9. <span data-ttu-id="f958a-254">Visual Studio를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-254">Exit Visual Studio.</span></span>
10. <span data-ttu-id="f958a-255">[Azure Storage 에뮬레이터](/azure/storage/common/storage-use-emulator)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-255">Start the [Azure Storage Emulator](/azure/storage/common/storage-use-emulator).</span></span>
11. <span data-ttu-id="f958a-256">Visual Studio를 다시 시작 하 고 이전 단계에서 닫은 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-256">Restart Visual Studio, opening the solution file you closed in the previous step.</span></span>
12. <span data-ttu-id="f958a-257">FixIt 프로젝트가 시작 프로젝트로 설정 되어 있는지 확인 한 다음 CTRL + F5 키를 눌러 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-257">Make sure the FixIt project is set as the startup project, and then press CTRL+F5 to run the project.</span></span>

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a><span data-ttu-id="f958a-258">큐 처리를 사용 하 여 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f958a-258">Run the application with queue processing</span></span>

1. <span data-ttu-id="f958a-259">[기본 응용 프로그램을 실행](#runbase)하는 지침에 따라 브라우저를 닫고 Visual Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-259">Follow the directions for [Run the base application](#runbase), and then close the browser and close Visual Studio.</span></span>
2. <span data-ttu-id="f958a-260">관리자 권한으로 Visual Studio를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-260">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="f958a-261">(Azure 계산 에뮬레이터를 사용 하 고 관리자 권한이 필요 합니다.)</span><span class="sxs-lookup"><span data-stu-id="f958a-261">(You'll be using the Azure compute emulator, and that requires administrator privileges.)</span></span>
3. <span data-ttu-id="f958a-262">*Myfixit* 프로젝트 (웹 프로젝트)의 응용 프로그램 *Web.config* 파일에서의 값을 `appSettings/UseQueues` "true"로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-262">In the application *Web.config* file in the *MyFixIt* project (the web project), change the value of `appSettings/UseQueues` to "true":</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. <span data-ttu-id="f958a-263">[Azure Storage 에뮬레이터가](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) 아직 실행 되 고 있지 않은 경우 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-263">If the [Azure Storage Emulator](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) isn't still running, start it again.</span></span>
5. <span data-ttu-id="f958a-264">FixIt 웹 프로젝트 및 MyFixItCloudService 프로젝트를 동시에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-264">Run the FixIt web project and the MyFixItCloudService project simultaneously.</span></span>

    <span data-ttu-id="f958a-265">Visual Studio 사용:</span><span class="sxs-lookup"><span data-stu-id="f958a-265">Using Visual Studio:</span></span>

   1. <span data-ttu-id="f958a-266">F 5 **를 눌러 FixIt 프로젝트를 실행** 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-266">Press **F5** to run the FixIt project.</span></span>
   2. <span data-ttu-id="f958a-267">**솔루션 탐색기**에서 MyFixItCloudService 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **디버그**  >  **새 인스턴스 시작**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-267">In **Solution Explorer**, right-click the MyFixItCloudService project, and then click **Debug** > **Start New Instance**.</span></span>

    <span data-ttu-id="f958a-268">웹에 Visual Studio 2013 Express 사용:</span><span class="sxs-lookup"><span data-stu-id="f958a-268">Using Visual Studio 2013 Express for Web:</span></span>

   3. <span data-ttu-id="f958a-269">솔루션 탐색기에서 FixIt 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-269">In Solution Explorer, right-click the FixIt solution and select **Properties**.</span></span>
   4. <span data-ttu-id="f958a-270">**여러 개의 시작 프로젝트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-270">Select **Multiple Startup Projects**.</span></span>
   5. <span data-ttu-id="f958a-271">MyFixIt 및 MyFixItCloudService의 **작업** 드롭다운 목록에서 **시작**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-271">In the **Action** dropdown list under MyFixIt and MyFixItCloudService, select **Start**.</span></span>
   6. <span data-ttu-id="f958a-272">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-272">Click **OK**.</span></span>
   7. <span data-ttu-id="f958a-273">**F5** 키를 눌러 두 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-273">Press **F5** to run both projects.</span></span>

      <span data-ttu-id="f958a-274">MyFixItCloudService 프로젝트를 실행 하면 Visual Studio에서 Azure 계산 에뮬레이터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-274">When you run the MyFixItCloudService project, Visual Studio starts the Azure compute emulator.</span></span> <span data-ttu-id="f958a-275">방화벽 구성에 따라 에뮬레이터를 방화벽을 통해 허용 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-275">Depending on your firewall configuration, you might need to allow the emulator through the firewall.</span></span>

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a><span data-ttu-id="f958a-276">Windows PowerShell 스크립트를 사용 하 여 Azure App Service Web Apps에 기본 앱을 배포 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f958a-276">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>

<span data-ttu-id="f958a-277">[모두 자동화](automate-everything.md) 패턴을 설명 하기 위해 Azure에서 환경을 설정 하 고 프로젝트를 새 환경에 배포 하는 스크립트를 사용 하 여 Fix It 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-277">To illustrate the [Automate Everything](automate-everything.md) pattern, the Fix It app is supplied with scripts that set up an environment in Azure and deploy the project to the new environment.</span></span> <span data-ttu-id="f958a-278">다음 지침에서는 스크립트를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-278">The following instructions explain how to use the scripts.</span></span>

<span data-ttu-id="f958a-279">큐를 사용 하지 않고 Azure에서 실행 하려는 경우 큐를 사용 하 여 로컬로 실행 하도록 변경 하려면 다음 지침을 수행 하기 전에 UseQueues appSetting 값을 다시 false로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-279">If you want to run in Azure without using queues, and you made the changes to run locally with queues, make sure you set the UseQueues appSetting value back to false before proceeding with the following instructions.</span></span>

<span data-ttu-id="f958a-280">이 지침에서는 수정 It 솔루션을 로컬로 다운로드 하 여 실행 한 것으로 가정 하 고 Azure 계정이 있거나 관리할 수 있는 Azure 구독이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-280">These instructions assume you have already downloaded and run the Fix It solution locally, and that you have an Azure account or have an Azure subscription that you are authorized to manage.</span></span>

1. <span data-ttu-id="f958a-281">**Azure PowerShell** 콘솔을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-281">Install the **Azure PowerShell** console.</span></span> <span data-ttu-id="f958a-282">자세한 내용은 [Azure PowerShell 설치 및 구성법](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f958a-282">For instructions, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span>

    <span data-ttu-id="f958a-283">이 사용자 지정 콘솔은 Azure 구독과 함께 작동 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-283">This customized console is configured to work with your Azure subscription.</span></span> <span data-ttu-id="f958a-284">Azure 모듈은 *Program Files* 디렉터리에 설치 되며 Azure PowerShell 콘솔을 사용할 때마다 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-284">The Azure module is installed in the *Program Files* directory and is automatically imported on every use of the Azure PowerShell console.</span></span>

    <span data-ttu-id="f958a-285">Windows PowerShell ISE와 같은 다른 호스트 프로그램에서 작업 하려면 [import-module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet을 사용 하 여 azure 모듈을 가져오거나 azure 모듈의 명령을 사용 하 여 모듈의 자동 가져오기를 트리거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-285">If you prefer to work in a different host program, such as Windows PowerShell ISE, be sure to use the [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet to import the Azure module or use a command in the Azure module to trigger automatic importing of the module.</span></span>
2. <span data-ttu-id="f958a-286">**관리자 권한으로 실행** 옵션을 사용 하 여 Azure PowerShell를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-286">Start Azure PowerShell with the **Run as administrator** option.</span></span>
3. <span data-ttu-id="f958a-287">[Set-executionpolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet을 실행 하 여 Azure PowerShell 실행 정책을로 설정 `RemoteSigned` 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-287">Run the [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet to set the Azure PowerShell execution policy to `RemoteSigned`.</span></span> <span data-ttu-id="f958a-288">**Y** (예의 경우)를 입력 하 여 정책 변경을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-288">Enter **Y** (for Yes) to complete the policy change.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    <span data-ttu-id="f958a-289">이 설정을 사용 하면 디지털 서명 되지 않은 로컬 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-289">This setting enables you to run local scripts that aren't digitally signed.</span></span> <span data-ttu-id="f958a-290">실행 정책을로 설정할 수도 있습니다. 이렇게 하면 `Unrestricted` 나중에 차단 해제 단계가 필요 하지 않습니다. 하지만 보안상의 이유로이 방법은 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-290">(You can also set the execution policy to `Unrestricted`, which would eliminate the need for the unblock step later, but this is not recommended for security reasons.)</span></span>
4. <span data-ttu-id="f958a-291">Cmdlet을 실행 `Add-AzureAccount` 하 여 계정에 대 한 자격 증명으로 PowerShell을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-291">Run the `Add-AzureAccount` cmdlet to set up PowerShell with credentials for your account.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    <span data-ttu-id="f958a-292">이러한 자격 증명은 일정 기간 후에 만료 되므로 cmdlet을 다시 실행 해야 합니다 `Add-AzureAccount` .</span><span class="sxs-lookup"><span data-stu-id="f958a-292">These credentials expire after a period of time and you have to re-run the `Add-AzureAccount` cmdlet.</span></span> <span data-ttu-id="f958a-293">이 e-learning을 작성 하는 동안 자격 증명의 만료 시간 제한은 12 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-293">As this e-book is being written, the time limit before credentials expire is 12 hours.</span></span>
5. <span data-ttu-id="f958a-294">구독이 여러 개인 경우 Get-azuresubscription cmdlet을 사용 하 여 테스트 환경을 만들려는 구독을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-294">If you have multiple subscriptions, use the Select-AzureSubscription cmdlet to specify the subscription you want to create the test environment in.</span></span>
6. <span data-ttu-id="f958a-295">및 cmdlet을 사용 하 여 동일한 Azure 구독에 대 한 관리 인증서를 가져옵니다 `Get-AzurePublishSettingsFile` `Import-AzurePublishSettingsFile` .</span><span class="sxs-lookup"><span data-stu-id="f958a-295">Import a management certificate for the same Azure subscription by using the `Get-AzurePublishSettingsFile` and `Import-AzurePublishSettingsFile` cmdlets.</span></span> <span data-ttu-id="f958a-296">이 cmdlet 중 첫 번째 cmdlet은 인증서 파일을 다운로드 하 고, 두 번째 cmdlet은 파일을 가져오기 위해 해당 파일의 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-296">The first of these cmdlets downloads a certificate file, and in the second one you specify the location of that file in order to import it.</span></span> > [!IMPORTANT]
   > <span data-ttu-id="f958a-297">다운로드 한 파일은 Azure 서비스를 관리 하는 데 사용할 수 있는 인증서를 포함 하므로 안전한 위치에 보관 하거나 작업을 수행 하는 경우 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-297">Keep the downloaded file in a safe location or delete it when you're done with it, because it contains a certificate that can be used to manage your Azure services.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    <span data-ttu-id="f958a-298">인증서는 SQL Database 서버에서 방화벽 규칙을 설정 하기 위해 개발 컴퓨터의 IP 주소를 검색 하는 REST API 호출에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-298">The certificate is used for a REST API call that detects the development machine's IP address in order to set a firewall rule on the SQL Database server.</span></span>
7. <span data-ttu-id="f958a-299">[집합 위치](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (별칭은 `cd` , `chdir` 및)을 실행 하 여 `sl` 스크립트가 포함 된 디렉터리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-299">Run the [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (aliases are `cd`, `chdir`, and `sl`) to navigate to the directory that contains the scripts.</span></span> <span data-ttu-id="f958a-300">(It 솔루션 수정 폴더의 *Automation* 폴더에 있습니다.) 디렉터리 이름에 공백이 포함 된 경우 경로를 따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-300">(They're located in the *Automation* folder in the Fix It solution folder.) Put the path in quotes if any of the directory names contain spaces.</span></span> <span data-ttu-id="f958a-301">예를 들어 디렉터리로 이동 하려면 `c:\Sample Apps\FixIt\Automation` 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-301">For example, to navigate to the `c:\Sample Apps\FixIt\Automation` directory you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. <span data-ttu-id="f958a-302">Windows PowerShell에서 이러한 스크립트를 실행할 수 있도록 하려면 [파일 차단 해제](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-302">To allow Windows PowerShell to run these scripts, use the [Unblock-File](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet.</span></span> <span data-ttu-id="f958a-303">스크립트는 인터넷에서 다운로드 되었으므로 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-303">(The scripts are blocked because they were downloaded from the Internet.)</span></span>

    > [!WARNING]
    > <span data-ttu-id="f958a-304">보안-스크립트나 실행 파일을 실행 하기 전에 `Unblock-File` 메모장에서 파일을 열고 명령을 검사 하 여 악성 코드가 포함 되지 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-304">Security - Before running `Unblock-File` on any script or executable file, open the file in Notepad, examine the commands, and verify that they do not contain any malicious code.</span></span>

    <span data-ttu-id="f958a-305">예를 들어 다음 명령은 `Unblock-File` 현재 디렉터리의 모든 스크립트에서 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-305">For example, the following command runs the `Unblock-File` cmdlet on all scripts in the current directory.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. <span data-ttu-id="f958a-306">기본 (큐 처리 없음)에 대 한 웹 앱을 만들려면 It 앱을 수정 하 고 환경 생성 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-306">To create the web app for the base (no queues processing) Fix It app, run the environment creation script.</span></span>

    <span data-ttu-id="f958a-307">필수 `Name` 매개 변수는 데이터베이스의 이름을 지정 하며 스크립트에서 만드는 저장소 계정에도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-307">The required `Name` parameter specifies the name of the database and is also used for the storage account that the script creates.</span></span> <span data-ttu-id="f958a-308">이름은 azurewebsites.net 도메인 내에서 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-308">The name must be globally unique within the azurewebsites.net domain.</span></span> <span data-ttu-id="f958a-309">Fixit 또는 Test와 같이 고유 하지 않은 이름을 지정 하거나 (예: fixitdemo) `New-AzureWebsite` cmdlet은 충돌을 보고 하는 내부 오류로 인해 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-309">If you specify a name that is not unique, like Fixit or Test (or even as in the example, fixitdemo), the `New-AzureWebsite` cmdlet fails with an Internal Error that reports a conflict.</span></span> <span data-ttu-id="f958a-310">이 스크립트는 이름을 모두 소문자로 변환 하 여 웹 앱, 저장소 계정 및 데이터베이스의 이름 요구 사항을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-310">The script converts the name to all lower-case to comply with name requirements for web apps, storage accounts, and databases.</span></span>

    <span data-ttu-id="f958a-311">필수 `SqlDatabasePassword` 매개 변수는 SQL Database에 대해 생성 되는 관리자 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-311">The required `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="f958a-312">암호에 특수 XML 문자를 포함 하지 않습니다 ( &amp; &lt; &gt; ;).</span><span class="sxs-lookup"><span data-stu-id="f958a-312">Don't include special XML characters in the password (&amp; &lt; &gt; ;).</span></span> <span data-ttu-id="f958a-313">이는 스크립트가 작성 된 방식에 대 한 제한 사항이 며 Azure의 제한이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-313">This is a limitation of the way the scripts were written, not a limitation of Azure.</span></span>

    <span data-ttu-id="f958a-314">예를 들어 "fixitdemo" 라는 웹 앱을 만들고 SQL Server 관리자 암호 "Passw0rd1"를 사용 하려는 경우 다음 명령을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-314">For example, if you want to create a web app named "fixitdemo" and use a SQL Server administrator password of "Passw0rd1", you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    <span data-ttu-id="f958a-315">이름은 azurewebsites.net 도메인에서 고유 해야 하며 암호 복잡성에 대 한 SQL Database 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-315">The name must be unique in the azurewebsites.net domain, and the password must meet SQL Database requirements for password complexity.</span></span> <span data-ttu-id="f958a-316">Passw0rd1 예제는 요구 사항을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-316">(The example Passw0rd1 does meet the requirements.)</span></span>

    <span data-ttu-id="f958a-317">명령은 ". .로 시작 합니다. \"</span><span class="sxs-lookup"><span data-stu-id="f958a-317">Note that the command begins with ".\".</span></span> <span data-ttu-id="f958a-318">악의적인 스크립트 실행을 방지 하기 위해 Windows PowerShell을 사용 하려면 스크립트를 실행할 때 스크립트 파일의 정규화 된 경로를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-318">To help prevent malicious execution of scripts, Windows PowerShell requires that you provide the fully qualified path to the script file when you run a script.</span></span> <span data-ttu-id="f958a-319">점을 사용 하 여 현재 디렉터리 (".)를 나타낼 수 있습니다. \" 또는 다음과 같이 정규화 된 경로를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-319">You can use a dot to indicate the current directory (".\") or provide the fully qualified path, such as:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    <span data-ttu-id="f958a-320">스크립트에 대 한 자세한 내용을 보려면 cmdlet을 사용 하십시오 `Get-Help` .</span><span class="sxs-lookup"><span data-stu-id="f958a-320">For more information about the script, use the `Get-Help` cmdlet.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    <span data-ttu-id="f958a-321">`Detailed` `Full` `Parameters` `Examples` Get-help cmdlet의,, 및 매개 변수를 사용 하 여 반환 되는 도움말을 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-321">You can use the `Detailed`, `Full`, `Parameters`, and `Examples` parameters of the Get-Help cmdlet to filter the help that is returned.</span></span>

    <span data-ttu-id="f958a-322">스크립트가 실패 하거나 오류를 생성 하는 경우 (예: "AzureWebsite: Call Get-azuresubscription and Get-azuresubscription first") Azure PowerShell의 구성을 완료 하지 않았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-322">If the script fails or generates errors, such as "New-AzureWebsite : Call Set-AzureSubscription and Select-AzureSubscription first," you might not have completed the configuration of Azure PowerShell.</span></span>

    <span data-ttu-id="f958a-323">스크립트가 완료 되 면 Azure 관리 포털를 사용 하 여 생성 된 리소스를 볼 수 있습니다 .이에 대해서는 [모두 자동화](automate-everything.md) 단원을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f958a-323">After the script finishes, you can use the Azure Management Portal to see the resources that were created, as shown in the [Automate Everything](automate-everything.md) chapter.</span></span>
10. <span data-ttu-id="f958a-324">새 Azure 환경에 FixIt 프로젝트를 배포 하려면 *AzureWebsite.ps1* 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-324">To deploy the FixIt project to the new Azure environment, use the *AzureWebsite.ps1* script.</span></span> <span data-ttu-id="f958a-325">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-325">For example:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    <span data-ttu-id="f958a-326">배포가 완료 되 면 브라우저가 Azure에서 실행 되는 수정 사항으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-326">When deployment is done, the browser opens with Fix It running in Azure.</span></span>

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a><span data-ttu-id="f958a-327">Windows PowerShell 스크립트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f958a-327">Troubleshooting the Windows PowerShell scripts</span></span>

<span data-ttu-id="f958a-328">이러한 스크립트를 실행할 때 발생 하는 가장 일반적인 오류는 사용 권한과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-328">The most common errors encountered when running these scripts are related to permissions.</span></span> <span data-ttu-id="f958a-329">및가 성공적으로 실행 되었으며 `Add-AzureAccount` `Import-AzurePublishSettingsFile` 동일한 Azure 구독에 사용 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-329">Make sure that `Add-AzureAccount` and `Import-AzurePublishSettingsFile` were successful and that you used them for the same Azure subscription.</span></span> <span data-ttu-id="f958a-330">`Add-AzureAccount`가 성공적으로 수행 된 경우에도 다시 실행 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-330">Even if `Add-AzureAccount` was successful you might have to run it again.</span></span> <span data-ttu-id="f958a-331">에 의해 추가 된 사용 권한은 `Add-AzureAccount` 12 시간 후에 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-331">The permissions added by `Add-AzureAccount` expire in 12 hours.</span></span>

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a><span data-ttu-id="f958a-332">개체 참조가 개체의 인스턴스로 설정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-332">Object reference not set to an instance of an object.</span></span>

<span data-ttu-id="f958a-333">스크립트에서 "개체 참조가 개체의 인스턴스로 설정 되지 않았습니다."와 같은 오류를 반환 하는 경우 Windows PowerShell에서 처리할 개체를 찾을 수 없음을 의미 합니다 .이는 null 참조 예외입니다 .이 경우에는 cmdlet을 실행 `Add-AzureAccount` 하 고 스크립트를 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-333">If the script returns errors, such as "Object reference not set to an instance of an object," which means that Windows PowerShell can't find an object to process (this is a null reference exception), run the `Add-AzureAccount` cmdlet and try the script again.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a><span data-ttu-id="f958a-334">InternalError: 서버에서 내부 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-334">InternalError: The server encountered an internal error.</span></span>

<span data-ttu-id="f958a-335">`New-AzureWebsite`Azurewebsites.net 도메인에서 이름이 고유 하지 않은 경우 cmdlet은 내부 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-335">The `New-AzureWebsite` cmdlet returns an internal error when the name is not unique in the azurewebsites.net domain.</span></span> <span data-ttu-id="f958a-336">오류를 해결 하려면 *New-AzureWebsiteEnv.ps1*의 name 매개 변수에 있는 이름에 대해 다른 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-336">To resolve the error, use a different value for the name, which is in the Name parameter of *New-AzureWebsiteEnv.ps1*.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a><span data-ttu-id="f958a-337">스크립트 다시 시작</span><span class="sxs-lookup"><span data-stu-id="f958a-337">Restarting the script</span></span>

<span data-ttu-id="f958a-338">*New-AzureWebsiteEnv.ps1* 스크립트가 "스크립트가 완료 되었습니다." 라는 메시지를 인쇄 하기 전에 실패 하 여 다시 시작 해야 하는 경우 스크립트가 중지 되기 전에 만든 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-338">If you need to restart the *New-AzureWebsiteEnv.ps1* script because it failed before it printed the "Script is complete" message, you might want to delete resources that the script created before it stopped.</span></span> <span data-ttu-id="f958a-339">예를 들어 스크립트가 ContosoFixItDemo 웹 앱을 이미 만들었고 동일한 이름으로 스크립트를 다시 실행 하는 경우에는 이름이 사용 중 이므로 스크립트가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-339">For example, if the script already created the ContosoFixItDemo web app and you run the script again with the same name, the script will fail because the name is in use.</span></span>

<span data-ttu-id="f958a-340">스크립트가 중지 되기 전에 만든 리소스를 확인 하려면 다음 cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-340">To determine which resources the script created before it stopped, use the following cmdlets:</span></span>

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- <span data-ttu-id="f958a-341">`Get-AzureSqlDatabase`:이 cmdlet을 실행 하려면 데이터베이스 서버 이름을 `Get-AzureSqlDatabase` 다음과 같이 파이프 합니다.   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span><span class="sxs-lookup"><span data-stu-id="f958a-341">`Get-AzureSqlDatabase`: To run this cmdlet, pipe the database server name to `Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span></span>

<span data-ttu-id="f958a-342">이러한 리소스를 삭제 하려면 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-342">To delete these resources, use the following commands.</span></span> <span data-ttu-id="f958a-343">데이터베이스 서버를 삭제 하면 해당 서버와 연결 된 데이터베이스가 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-343">Note that if you delete the database server, you automatically delete the databases associated with the server.</span></span>

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a><span data-ttu-id="f958a-344">큐 처리를 사용 하 여 앱을 배포 하 여 Web Apps 및 Azure 클라우드 서비스를 Azure App Service 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f958a-344">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>

<span data-ttu-id="f958a-345">큐를 사용 하도록 설정 하려면 MyFixIt\Web.config 파일에서 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-345">To enable queues, make the following change in the MyFixIt\Web.config file.</span></span> <span data-ttu-id="f958a-346">에서 `appSettings` 의 값을 `UseQueues` "true"로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-346">Under `appSettings`, change the value of `UseQueues` to "true":</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

<span data-ttu-id="f958a-347">그런 다음 [앞](#deploybase)에서 설명한 대로 AZURE APP SERVICE에서 MVC 응용 프로그램을 웹 앱에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-347">Then deploy the MVC application to an web app in Azure App Service, as described [earlier](#deploybase).</span></span>

<span data-ttu-id="f958a-348">다음으로 새 Azure 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-348">Next, create a new Azure cloud service.</span></span> <span data-ttu-id="f958a-349">Fix It 앱에 포함 된 스크립트는 클라우드 서비스를 만들거나 배포 하지 않으므로이를 위해 Azure Portal를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-349">The scripts included with the Fix It app do not create or deploy the cloud service, so you must use Azure portal for this.</span></span> <span data-ttu-id="f958a-350">포털에서 **새로 만들기**  --  **계산** – **클라우드 서비스**  --  **빠른 생성**을 클릭 하 고 URL 및 데이터 센터 위치를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-350">In the portal, click **New** -- **Compute** – **Cloud Service** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="f958a-351">웹 앱을 배포한 동일한 데이터 센터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-351">Use the same data center where you deployed the web app.</span></span>

![](the-fix-it-sample-application/_static/image1.png)

<span data-ttu-id="f958a-352">클라우드 서비스를 배포 하려면 먼저 일부 구성 파일을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-352">Before you can deploy the cloud service, you need to update some of the configuration files.</span></span>

<span data-ttu-id="f958a-353">MyFixIt.WorkerRole\app.config의에서 `connectionStrings` 연결 문자열의 값을 `appdb` SQL Database에 대 한 실제 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-353">In MyFixIt.WorkerRole\app.config, under `connectionStrings`, replace the value of the `appdb` connection string with the actual connection string for the SQL Database.</span></span> <span data-ttu-id="f958a-354">포털에서 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-354">You can get the connection string from the portal.</span></span> <span data-ttu-id="f958a-355">포털에서 **SQL 데이터베이스**  -  **appdb**  -  **뷰 SQL Database ADO .net, ODBC, PHP 및 JDBC에 대 한 연결 문자열**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-355">In the portal, click **SQL Databases** - **appdb** - **View SQL Database connection strings for ADO .Net, ODBC, PHP, and JDBC**.</span></span> <span data-ttu-id="f958a-356">ADO.NET 연결 문자열을 복사 하 고 값을 app.config 파일에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-356">Copy the ADO.NET connection string and paste the value into the app.config file.</span></span> <span data-ttu-id="f958a-357">"{Your \_ password \_ }"를 데이터베이스 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-357">Replace "{your\_password\_here}" with your database password.</span></span> <span data-ttu-id="f958a-358">(스크립트를 사용 하 여 MVC 앱을 배포 했다고 가정 하 고 스크립트 매개 변수에서 데이터베이스 암호를 지정 `SqlDatabasePassword` 했습니다.)</span><span class="sxs-lookup"><span data-stu-id="f958a-358">(Assuming you used the scripts to deploy the MVC app, you specified the database password in the `SqlDatabasePassword` script parameter.)</span></span>

<span data-ttu-id="f958a-359">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-359">The result should look like the following:</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

<span data-ttu-id="f958a-360">동일한 MyFixIt.WorkerRole\app.config 파일의에서 `appSettings` Azure storage 계정에 대 한 두 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-360">In the same MyFixIt.WorkerRole\app.config file, under `appSettings`, replace the two placeholder values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

<span data-ttu-id="f958a-361">포털에서 선택 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-361">You can get the access key from the portal.</span></span> <span data-ttu-id="f958a-362">[저장소 계정을 관리 하는 방법을](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f958a-362">See [How To Manage Storage Accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>

<span data-ttu-id="f958a-363">MyFixItCloudService\ServiceConfiguration.Cloud.cscfg에서 Azure storage 계정에 대해 동일한 두 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-363">In MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, replace the same two placeholders values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

<span data-ttu-id="f958a-364">이제 클라우드 서비스를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-364">Now you are ready to deploy the cloud service.</span></span> <span data-ttu-id="f958a-365">솔루션 탐색기에서 MyFixItCloudService 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f958a-365">In Solution Explore, right-click the MyFixItCloudService project and select **Publish**.</span></span> <span data-ttu-id="f958a-366">자세한 내용은 [이 자습서](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)의 2 부에 있는 "[Azure에 응용 프로그램 배포](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)"를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f958a-366">For more information, see "[Deploy the Application to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", which is in part 2 of [this tutorial](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f958a-367">이전</span><span class="sxs-lookup"><span data-stu-id="f958a-367">Previous</span></span>](more-patterns-and-guidance.md)
