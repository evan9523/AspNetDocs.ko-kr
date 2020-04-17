---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: IIS (VB)의 다른 버전과 ASP.NET MVC사용 | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서에서는 다른 버전의 인터넷 정보 서비스와 ASP.NET MVC 및 URL 라우팅을 사용하는 방법을 배웁니다. 당신은 다른 전략을 배울 ...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: 5e04ae14026e6d5dd1e603be6c52ff6876a468cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542003"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a><span data-ttu-id="ae5f8-104">다양한 버전의 IIS에 ASP.NET MVC 사용(VB)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-104">Using ASP.NET MVC with Different Versions of IIS (VB)</span></span>

<span data-ttu-id="ae5f8-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ae5f8-106">이 자습서에서는 다른 버전의 인터넷 정보 서비스와 ASP.NET MVC 및 URL 라우팅을 사용하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="ae5f8-107">IIS 7.0(클래식 모드), IIS 6.0 및 이전 버전의 IIS에서 ASP.NET MVC를 사용하기 위한 다양한 전략을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>

<span data-ttu-id="ae5f8-108">ASP.NET MVC 프레임워크는 브라우저 요청을 컨트롤러 작업으로 라우팅하기 위해 ASP.NET 라우팅에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="ae5f8-109">ASP.NET 라우팅을 활용하려면 웹 서버에서 추가 구성 단계를 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="ae5f8-110">모든 것은 IIS(인터넷 정보 서비스) 버전과 응용 프로그램에 대한 요청 처리 모드에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="ae5f8-111">다음은 IIS의 다른 버전에 대한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="ae5f8-112">IIS 7.0(통합 모드) - 라우팅을 ASP.NET 사용할 필요가 없는 특별한 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="ae5f8-113">IIS 7.0(클래식 모드) - ASP.NET 라우팅을 사용하려면 특수 구성을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="ae5f8-114">IIS 6.0 이상 - 라우팅을 ASP.NET 사용하려면 특별한 구성을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="ae5f8-115">IIS의 최신 버전은 버전 7.5 (Win7)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="ae5f8-116">IIS의 IIS 7은 Windows 서버 2008 및 VISTA/SP1 이상에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="ae5f8-117">또한 홈 베이직(참조)을 [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)제외한 모든 버전의 Vista 운영 체제에 IIS 7.0을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="ae5f8-118">IIS 7.0은 요청을 처리하기 위한 두 가지 모드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="ae5f8-119">통합 모드 또는 클래식 모드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="ae5f8-120">통합 모드에서 IIS 7.0을 사용할 때는 특별한 구성 단계를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="ae5f8-121">그러나 클래식 모드에서 IIS 7.0을 사용할 때는 추가 구성을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="ae5f8-122">마이크로 소프트 윈도우 서버 2003 IIS 6.0을 포함한다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="ae5f8-123">Windows Server 2003 운영 체제를 사용하는 경우 IIS 6.0을 IIS 7.0으로 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="ae5f8-124">IIS 6.0을 사용할 때추가 구성 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="ae5f8-125">마이크로 소프트 윈도우 XP 전문가는 IIS 5.1을 포함한다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="ae5f8-126">IIS 5.1을 사용할 때 추가 구성 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="ae5f8-127">마지막으로, 마이크로 소프트 윈도우 2000 마이크로 소프트 윈도우 2000 프로페셔널은 IIS 5.0을 포함한다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="ae5f8-128">IIS 5.0을 사용할 때추가 구성 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="ae5f8-129">통합 대 클래식 모드</span><span class="sxs-lookup"><span data-stu-id="ae5f8-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="ae5f8-130">IIS 7.0은 통합 및 클래식이라는 두 가지 요청 처리 모드를 사용하여 요청을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="ae5f8-131">통합 모드는 더 나은 성능과 더 많은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="ae5f8-132">이전 버전의 IIS와의 이전 버전과의 호환성을 위해 클래식 모드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="ae5f8-133">요청 처리 모드는 응용 프로그램 풀에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="ae5f8-134">응용 프로그램과 연결된 응용 프로그램 풀을 확인하여 특정 웹 응용 프로그램에서 사용 중인 처리 모드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="ae5f8-135">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-135">Follow these steps:</span></span>

1. <span data-ttu-id="ae5f8-136">인터넷 정보 서비스 관리자 시작</span><span class="sxs-lookup"><span data-stu-id="ae5f8-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="ae5f8-137">연결 창에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="ae5f8-138">작업 창에서 기본 **설정** 링크를 클릭하여 응용 프로그램 편집 대화 상자를 엽니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="ae5f8-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="ae5f8-139">선택한 응용 프로그램 풀을 기록해 둡것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="ae5f8-140">기본적으로 IIS는 두 개의 응용 프로그램 풀을 지원하도록 구성됩니다: **DefaultAppPool** 및 **Classic .NET AppPool**.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="ae5f8-141">DefaultAppPool을 선택하면 응용 프로그램이 통합 요청 처리 모드에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="ae5f8-142">클래식 .NET AppPool을 선택한 경우 응용 프로그램이 클래식 요청 처리 모드에서 실행중입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>

<span data-ttu-id="ae5f8-143">[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)</span></span>

<span data-ttu-id="ae5f8-144">**그림 1**: 요청 처리 모드 감지[(전체 크기 이미지를 보려면 클릭)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))</span></span>

<span data-ttu-id="ae5f8-145">응용 프로그램 편집 대화 상자 내에서 요청 처리 모드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="ae5f8-146">선택 단추를 클릭하고 응용 프로그램과 연결된 응용 프로그램 풀을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="ae5f8-147">ASP.NET 응용 프로그램을 클래식 모드에서 통합 모드로 변경할 때 호환성 문제가 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="ae5f8-148">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="ae5f8-149">Windows Vista 및 Windows 서버 2008에서 ASP.NET IIS 7.0으로 업그레이드 --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>

- <span data-ttu-id="ae5f8-150">iIS 7.0과의 ASP.NET 통합 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>

<span data-ttu-id="ae5f8-151">ASP.NET 응용 프로그램이 DefaultAppPool을 사용하는 경우 라우팅(ASP.NET 따라서 MVC)ASP.NET 작동하기 위해 추가 단계를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="ae5f8-152">그러나 ASP.NET 응용 프로그램이 Classic .NET AppPool을 사용하도록 구성된 경우 계속 읽으면 더 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="ae5f8-153">이전 버전의 IIS와 ASP.NET MVC 사용</span><span class="sxs-lookup"><span data-stu-id="ae5f8-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="ae5f8-154">IIS 7.0보다 이전 버전의 IIS와 ASP.NET MVC를 사용해야 하거나 클래식 모드에서 IIS 7.0을 사용해야 하는 경우 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="ae5f8-155">먼저 파일 확장프로그램을 사용하도록 경로 테이블을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="ae5f8-156">예를 들어 /Store/Details와 같은 URL을 요청하는 대신 /Store.aspx/Details와 같은 URL을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="ae5f8-157">두 번째 옵션은 *와일드카드 스크립트 맵이라는*것을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="ae5f8-158">와일드카드 스크립트 맵을 사용하면 모든 요청을 ASP.NET 프레임워크에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="ae5f8-159">웹 서버에 액세스할 수 없는 경우(예: ASP.NET MVC 응용 프로그램이 인터넷 서비스 공급자가 호스팅하는 경우) 첫 번째 옵션을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="ae5f8-160">URL의 모양을 수정하지 않고 웹 서버에 액세스할 수 있는 경우 두 번째 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="ae5f8-161">다음 섹션에서 각 옵션을 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="ae5f8-162">배관 테이블에 확장 추가</span><span class="sxs-lookup"><span data-stu-id="ae5f8-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="ae5f8-163">이전 버전의 IIS에서 작동하도록 ASP.NET 라우팅을 얻는 가장 쉬운 방법은 Global.asax 파일에서 경로 테이블을 수정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="ae5f8-164">목록 1의 기본 및 수정되지 않은 Global.asax 파일은 기본 경로라는 하나의 경로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="ae5f8-165">**리스팅 1 - 글로벌.asax(수정되지 않은)**</span><span class="sxs-lookup"><span data-stu-id="ae5f8-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

<span data-ttu-id="ae5f8-166">목록 1에 구성된 기본 경로를 사용하면 다음과 같은 URL을 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="ae5f8-167">/홈/인덱스</span><span class="sxs-lookup"><span data-stu-id="ae5f8-167">/Home/Index</span></span>

<span data-ttu-id="ae5f8-168">/제품/세부 정보/3</span><span class="sxs-lookup"><span data-stu-id="ae5f8-168">/Product/Details/3</span></span>

<span data-ttu-id="ae5f8-169">/Product</span><span class="sxs-lookup"><span data-stu-id="ae5f8-169">/Product</span></span>

<span data-ttu-id="ae5f8-170">안타깝게도 이전 버전의 IIS는 이러한 요청을 ASP.NET 프레임워크에 전달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="ae5f8-171">따라서 이러한 요청은 컨트롤러로 라우팅되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="ae5f8-172">예를 들어 URL/홈/인덱스에 대한 브라우저 요청을 하면 그림 2의 오류 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>

<span data-ttu-id="ae5f8-173">[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)</span></span>

<span data-ttu-id="ae5f8-174">**그림 2**: 404 찾을 수 없는 오류 수신[(전체 크기 이미지를 보려면 클릭)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))</span></span>

<span data-ttu-id="ae5f8-175">이전 버전의 IIS는 특정 요청을 ASP.NET 프레임워크에만 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="ae5f8-176">요청은 올바른 파일 확장이 있는 URL이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="ae5f8-177">예를 들어 /SomePage.aspx에 대한 요청은 ASP.NET 프레임워크에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="ae5f8-178">그러나 /SomePage.htm에 대한 요청은 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="ae5f8-179">따라서 라우팅ASP.NET 작동하려면 ASP.NET 프레임워크에 매핑된 파일 확장자를 포함하도록 기본 경로를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="ae5f8-180">이 작업은 . `registermvc.wsf`</span><span class="sxs-lookup"><span data-stu-id="ae5f8-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="ae5f8-181">ASP.NET MVC 1 릴리스에 `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`포함되었지만 ASP.NET 2현재 이 스크립트는 에서 [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)사용할 수 있는 ASP.NET 선물로 이동되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="ae5f8-182">이 스크립트를 실행하면 IIS에 새 .mvc 확장이 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="ae5f8-183">.mvc 확장을 등록한 후 경로가 .mvc 확장을 사용하도록 Global.asax 파일에서 경로를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="ae5f8-184">리스팅 2의 수정된 Global.asax 파일은 이전 버전의 IIS에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="ae5f8-185">**리스팅 2 - Global.asax(확장으로 수정)**</span><span class="sxs-lookup"><span data-stu-id="ae5f8-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

<span data-ttu-id="ae5f8-186">중요: Global.asax 파일을 변경한 후 ASP.NET MVC 응용 프로그램을 다시 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-186">Important: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>

<span data-ttu-id="ae5f8-187">목록 2의 Global.asax 파일에는 두 가지 중요한 변경 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="ae5f8-188">이제 Global.asax에 정의된 두 개의 경로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="ae5f8-189">기본 경로의 URL 패턴인 첫 번째 경로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="ae5f8-190">{컨트롤러}.mvc/{작업}/{id}</span><span class="sxs-lookup"><span data-stu-id="ae5f8-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="ae5f8-191">.mvc 확장자를 추가하면 ASP.NET 라우팅 모듈이 가로채는 파일 의 형식이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="ae5f8-192">이 변경으로 ASP.NET MVC 응용 프로그램은 이제 다음과 같은 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="ae5f8-193">/Home.mvc/인덱스/</span><span class="sxs-lookup"><span data-stu-id="ae5f8-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="ae5f8-194">/Product.mvc/세부 정보/3</span><span class="sxs-lookup"><span data-stu-id="ae5f8-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="ae5f8-195">/Product.mvc/</span><span class="sxs-lookup"><span data-stu-id="ae5f8-195">/Product.mvc/</span></span>

<span data-ttu-id="ae5f8-196">두 번째 경로인 루트 경로는 새 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="ae5f8-197">루트 경로에 대한 이 URL 패턴은 빈 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="ae5f8-198">이 경로는 응용 프로그램의 루트에 대해 만든 요청을 일치시키는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="ae5f8-199">예를 들어 루트 경로는 다음과 같은 요청과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-199">For example, the Root route will match a request that looks like this:</span></span>

[http://www.YourApplication.com/](http://www.YourApplication.com/)

<span data-ttu-id="ae5f8-200">경로 테이블을 수정한 후에는 응용 프로그램의 모든 링크가 이러한 새 URL 패턴과 호환되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-200">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="ae5f8-201">즉, 모든 링크에 .mvc 확장이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-201">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="ae5f8-202">Html.ActionLink() 도우미 메서드를 사용하여 링크를 생성하는 경우 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-202">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>

<span data-ttu-id="ae5f8-203">registermvc.wcf 스크립트를 사용하는 대신 ASP.NET 프레임워크에 직접 매핑되는 IIS에 새 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-203">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="ae5f8-204">새 확장프로그램을 직접 추가할 때 **파일이 있는지 확인이라는** 확인란이 선택되어 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-204">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>

## <a name="hosted-server"></a><span data-ttu-id="ae5f8-205">호스팅 서버</span><span class="sxs-lookup"><span data-stu-id="ae5f8-205">Hosted Server</span></span>

<span data-ttu-id="ae5f8-206">웹 서버에 항상 액세스할 수 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-206">You don't always have access to your web server.</span></span> <span data-ttu-id="ae5f8-207">예를 들어 인터넷 호스팅 공급자를 사용하여 ASP.NET MVC 응용 프로그램을 호스팅하는 경우 IIS에 반드시 액세스할 수 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-207">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="ae5f8-208">이 경우 ASP.NET 프레임워크에 매핑된 기존 파일 확장명 중 하나를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-208">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="ae5f8-209">ASP.NET 매핑된 파일 확장자의 예로는 .aspx, .axd 및 .ashx 확장인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-209">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="ae5f8-210">예를 들어 목록 3의 수정된 Global.asax 파일은 .mvc 확장자 대신 .aspx 확장을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-210">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="ae5f8-211">**목록 3 - Global.asax(.aspx 확장으로 수정)**</span><span class="sxs-lookup"><span data-stu-id="ae5f8-211">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

<span data-ttu-id="ae5f8-212">목록 3의 Global.asax 파일은 .mvc 확장자 대신 .aspx 확장을 사용한다는 사실을 제외하고는 이전 Global.asax 파일과 정확히 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-212">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="ae5f8-213">.aspx 확장을 사용 하려면 원격 웹 서버에서 설정을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-213">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="ae5f8-214">와일드카드 스크립트 맵 만들기</span><span class="sxs-lookup"><span data-stu-id="ae5f8-214">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="ae5f8-215">ASP.NET MVC 응용 프로그램에 대한 URL을 수정하지 않고 웹 서버에 액세스할 수 있는 경우 추가 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-215">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="ae5f8-216">웹 서버에 대한 모든 요청을 ASP.NET 프레임워크에 매핑하는 와일드카드 스크립트 맵을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-216">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="ae5f8-217">이렇게 하면 IIS 7.0(클래식 모드) 또는 IIS 6.0에서 기본 ASP.NET MVC 경로 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-217">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="ae5f8-218">이 옵션을 사용하면 IIS가 웹 서버에 대한 모든 요청을 가로챌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-218">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="ae5f8-219">여기에는 이미지, 클래식 ASP 페이지 및 HTML 페이지에 대한 요청이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-219">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="ae5f8-220">따라서 와일드카드 스크립트 맵을 ASP.NET 활성화하면 성능에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-220">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="ae5f8-221">IIS 7.0에 와일드카드 스크립트 맵을 사용하도록 설정하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-221">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="ae5f8-222">연결 창에서 응용 프로그램 선택</span><span class="sxs-lookup"><span data-stu-id="ae5f8-222">Select your application in the Connections window</span></span>
2. <span data-ttu-id="ae5f8-223">**피처** 뷰가 선택되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="ae5f8-223">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="ae5f8-224">**처리기 매핑 단추를** 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-224">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="ae5f8-225">와일드카드 **스크립트 맵 추가** 링크를 클릭합니다(그림 3 참조)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-225">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="ae5f8-226">aspnet\_isapi.dll 파일에 대한 경로를 입력합니다(PageHandlerFactory 스크립트 맵에서 이 경로를 복사할 수 있음)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-226">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="ae5f8-227">MVC 이름 입력</span><span class="sxs-lookup"><span data-stu-id="ae5f8-227">Enter the name MVC</span></span>
7. <span data-ttu-id="ae5f8-228">**확인** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-228">Click the **OK** button</span></span>

<span data-ttu-id="ae5f8-229">[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-229">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)</span></span>

<span data-ttu-id="ae5f8-230">**그림 3**: IIS 7.0으로 와일드카드 스크립트 맵 만들기(전체[크기 이미지를 보려면 클릭)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-230">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))</span></span>

<span data-ttu-id="ae5f8-231">다음 단계에 따라 IIS 6.0을 사용하여 와일드카드 스크립트 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-231">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="ae5f8-232">웹 사이트를 마우스 오른쪽 단추로 클릭하고 속성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-232">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="ae5f8-233">홈 **디렉토리** 탭 선택</span><span class="sxs-lookup"><span data-stu-id="ae5f8-233">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="ae5f8-234">**구성** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-234">Click the **Configuration** button</span></span>
4. <span data-ttu-id="ae5f8-235">**매핑** 탭 선택</span><span class="sxs-lookup"><span data-stu-id="ae5f8-235">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="ae5f8-236">**삽입** 단추를 클릭합니다(그림 4 참조)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-236">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="ae5f8-237">실행 파일 필드에 aspnet\_isapi.dll에 대한 경로를 붙여 넣습니다(.aspx 파일의 스크립트 맵에서 이 경로를 복사할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="ae5f8-237">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="ae5f8-238">레이블이 붙은 확인란의 선택 취소 **파일이 있는지 확인합니다.**</span><span class="sxs-lookup"><span data-stu-id="ae5f8-238">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="ae5f8-239">**확인** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-239">Click the **OK** button</span></span>

<span data-ttu-id="ae5f8-240">[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-240">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)</span></span>

<span data-ttu-id="ae5f8-241">**그림 4**: IIS 6.0으로 와일드카드 스크립트 맵 만들기(전체[크기 이미지를 보려면 클릭)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-241">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))</span></span>

<span data-ttu-id="ae5f8-242">와일드카드 스크립트 맵을 사용하도록 설정한 후에는 루트 경로를 포함하도록 Global.asax 파일의 경로 테이블을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-242">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="ae5f8-243">그렇지 않으면 응용 프로그램의 루트 페이지를 요청할 때 그림 5의 오류 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-243">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="ae5f8-244">리스팅 4에서 수정된 Global.asax 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-244">You can use the modified Global.asax file in Listing 4.</span></span>

<span data-ttu-id="ae5f8-245">[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-245">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)</span></span>

<span data-ttu-id="ae5f8-246">**그림 5**: 루트 경로 오류 누락[(전체 크기 이미지를 보려면 클릭)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="ae5f8-246">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))</span></span>

<span data-ttu-id="ae5f8-247">**리스팅 4 - Global.asax(루트 경로로 수정)**</span><span class="sxs-lookup"><span data-stu-id="ae5f8-247">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

<span data-ttu-id="ae5f8-248">IIS 7.0 또는 IIS 6.0에 와일드카드 스크립트 맵을 사용하도록 설정한 후 다음과 같은 기본 경로 테이블에서 작동하는 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-248">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="ae5f8-249">/홈/인덱스</span><span class="sxs-lookup"><span data-stu-id="ae5f8-249">/Home/Index</span></span>

<span data-ttu-id="ae5f8-250">/제품/세부 정보/3</span><span class="sxs-lookup"><span data-stu-id="ae5f8-250">/Product/Details/3</span></span>

<span data-ttu-id="ae5f8-251">/Product</span><span class="sxs-lookup"><span data-stu-id="ae5f8-251">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="ae5f8-252">요약</span><span class="sxs-lookup"><span data-stu-id="ae5f8-252">Summary</span></span>

<span data-ttu-id="ae5f8-253">이 자습서의 목표는 이전 버전의 IIS(또는 클래식 모드에서 IIS 7.0)를 사용할 때 ASP.NET MVC를 사용하는 방법을 설명하는 것이었습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-253">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="ae5f8-254">이전 버전의 IIS에서 작동하도록 라우팅을 ASP.NET 두 가지 방법인 기본 경로 테이블을 수정하거나 와일드카드 스크립트 맵을 만드는 방법에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-254">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="ae5f8-255">첫 번째 옵션은 ASP.NET MVC 응용 프로그램에 사용되는 URL을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-255">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="ae5f8-256">이 첫 번째 옵션의 가장 큰 장점 중 하나는 경로 테이블을 수정하기 위해 웹 서버에 액세스할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-256">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="ae5f8-257">즉, 인터넷 호스팅 회사에서 ASP.NET MVC 응용 프로그램을 호스팅하는 경우에도 이 첫 번째 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-257">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="ae5f8-258">두 번째 옵션은 와일드카드 스크립트 맵을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-258">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="ae5f8-259">이 두 번째 옵션의 장점은 URL을 수정할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-259">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="ae5f8-260">이 두 번째 옵션의 단점은 ASP.NET MVC 응용 프로그램의 성능에 영향을 미칠 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae5f8-260">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ae5f8-261">이전</span><span class="sxs-lookup"><span data-stu-id="ae5f8-261">Previous</span></span>](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
