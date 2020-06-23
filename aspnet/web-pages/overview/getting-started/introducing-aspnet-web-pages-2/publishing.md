---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: ASP.NET 웹 페이지 소개-WebMatrix를 사용 하 여 사이트 게시 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 ASP.NET 웹 페이지 및 Microsoft WebMatrix를 소개 하는 자습서 집합의 마지막 기사입니다. 사이트를 게시 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: a09339a833ea0b4a2d3c3a9323cce777577ea048
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240589"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a><span data-ttu-id="230c5-104">ASP.NET 웹 페이지 소개-WebMatrix를 사용 하 여 사이트 게시</span><span class="sxs-lookup"><span data-stu-id="230c5-104">Introducing ASP.NET Web Pages - Publishing a Site by Using WebMatrix</span></span>

<span data-ttu-id="230c5-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="230c5-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="230c5-106">이 자습서는 ASP.NET 웹 페이지 및 Microsoft WebMatrix를 소개 하는 자습서 집합의 마지막 기사입니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-106">This tutorial is the final installment in the tutorial set that introduces ASP.NET Web Pages and Microsoft WebMatrix.</span></span> <span data-ttu-id="230c5-107">다른 사람이 사용할 수 있도록 사이트를 인터넷에 게시 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-107">It discusses how to publish your site to the Internet so that others can work with it.</span></span> <span data-ttu-id="230c5-108">[ASP.NET 웹 페이지 사이트에 대 한 일관 된 검색을 만들어](https://go.microsoft.com/fwlink/?LinkId=251585)시리즈를 완료 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-108">It assumes you have completed the series through [Creating a Consistent Look for ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=251585).</span></span>
> 
> <span data-ttu-id="230c5-109">다음을 사용 하 여 사이트를 게시 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-109">You'll learn how to publish your site using:</span></span>
> 
> - <span data-ttu-id="230c5-110">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="230c5-110">Microsoft Azure</span></span>
> - <span data-ttu-id="230c5-111">웹 호스팅 회사</span><span class="sxs-lookup"><span data-stu-id="230c5-111">Web Hosting Company</span></span>

## <a name="about-publishing-your-site"></a><span data-ttu-id="230c5-112">사이트 게시 정보</span><span class="sxs-lookup"><span data-stu-id="230c5-112">About Publishing Your Site</span></span>

<span data-ttu-id="230c5-113">지금까지 페이지 테스트를 포함 하 여 로컬 컴퓨터에서 모든 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-113">Up to now, you've done all your work on a local computer, including testing your pages.</span></span> <span data-ttu-id="230c5-114"><em>Cshtml</em> 페이지를 실행 하려면 WebMatrix에 내장 된 웹 서버 (IIS Express)를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-114">To run your<em>.cshtml</em> pages, you've used the web server that's built into WebMatrix, namely IIS Express.</span></span> <span data-ttu-id="230c5-115">그러나 사용자를 제외 하 고 만든 사이트는 아무도 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-115">But of course no one can see the site you've created except you.</span></span> <span data-ttu-id="230c5-116">다른 사용자가 사이트를 사용할 수 있도록 하려면 인터넷에 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-116">To let others work with your site, you have to publish it to the Internet.</span></span>

<span data-ttu-id="230c5-117">공용 웹 서버에 대 한 액세스 권한이 없는 경우 게시는 *클라우드 플랫폼* 또는 *호스팅 공급자*의 계정이 있어야 함을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-117">Unless you have access to a public web server already, publishing means that you have to have an account with a *cloud platform* or a *hosting provider*.</span></span> <span data-ttu-id="230c5-118">Microsoft Azure와 같은 클라우드 플랫폼은 응용 프로그램에 주문형 인프라를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-118">A cloud platform, such as Microsoft Azure, provides on-demand infrastructure for your applications.</span></span> <span data-ttu-id="230c5-119">호스팅 공급자는 공개적으로 액세스할 수 있는 웹 서버를 소유 하 고 있으며 사이트의 공간을 임대 하는 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-119">A hosting provider is a company that owns publicly accessible web servers and that will rent you space for your site.</span></span> <span data-ttu-id="230c5-120">호스팅 계획은 대용량 상용 웹 사이트를 위해 작은 사이트에 대해 몇 달러 (또는 무료)에서 수백 달러의 월로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-120">Hosting plans run from a few dollars a month (or even free) for small sites to many hundreds of dollars a month for high-volume commercial websites.</span></span>

> [!NOTE]
> <span data-ttu-id="230c5-121">집에서 인터넷 서비스를 가져오는 데 사용 하는 ISP (인터넷 서비스 공급자)를 통해 공용 웹 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-121">You might have access to a public web server via the internet service provider (ISP) that you use to get internet service at home.</span></span> <span data-ttu-id="230c5-122">그러나 호스팅 공급자는 ASP.NET 웹 페이지을 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-122">However, your hosting provider must support ASP.NET Web Pages.</span></span> <span data-ttu-id="230c5-123">대부분의 Isp는 그렇지 않지만 항상 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-123">Many ISPs don't, but it's always worth checking.</span></span>

<span data-ttu-id="230c5-124">이 자습서에서는 게시 하는 방법에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-124">In this tutorial, we'll give you an overview of how to publish.</span></span> <span data-ttu-id="230c5-125">모든 호스팅 공급자에 대해 프로세스가 약간 다르므로 모든 항목에 대 한 정확한 세부 정보를 제공 하는 것은 실용적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-125">It's not practical to provide exact details for everything, because the process differs a bit for every hosting provider.</span></span> <span data-ttu-id="230c5-126">그러나 프로세스가 작동 하는 방식을 이해 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-126">But you'll get a good idea of how the process works.</span></span>

<span data-ttu-id="230c5-127">이 자습서에는 다음 4 개의 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-127">This tutorial contains four sections:</span></span>

1. [<span data-ttu-id="230c5-128">기본 페이지 설정</span><span class="sxs-lookup"><span data-stu-id="230c5-128">Setting up the default page</span></span>](#defaultpage)
2. <span data-ttu-id="230c5-129">게시 (다음 중 하나 선택)</span><span class="sxs-lookup"><span data-stu-id="230c5-129">Publishing (choose one of the following)</span></span>  
 <span data-ttu-id="230c5-130">a.</span><span class="sxs-lookup"><span data-stu-id="230c5-130">a.</span></span> [<span data-ttu-id="230c5-131">Microsoft Azure에 사이트 게시</span><span class="sxs-lookup"><span data-stu-id="230c5-131">Publishing Your Site to Microsoft Azure</span></span>](#azure)  
 <span data-ttu-id="230c5-132">b.</span><span class="sxs-lookup"><span data-stu-id="230c5-132">b.</span></span> [<span data-ttu-id="230c5-133">웹 호스팅 회사에 사이트 게시</span><span class="sxs-lookup"><span data-stu-id="230c5-133">Publishing Your Site to a Web Hosting Company</span></span>](#host)
3. [<span data-ttu-id="230c5-134">라이브 사이트 업데이트: 다시 게시</span><span class="sxs-lookup"><span data-stu-id="230c5-134">Updating the Live Site: Republishing</span></span>](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a><span data-ttu-id="230c5-135">기본 페이지 설정</span><span class="sxs-lookup"><span data-stu-id="230c5-135">Setting up the default page</span></span>

<span data-ttu-id="230c5-136">사용자가 웹 사이트의 기본 주소로 이동 하면 사이트의 기본 페이지가 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-136">When a user navigates to the base address for your web site, the default page for your site is displayed to the user.</span></span> <span data-ttu-id="230c5-137">예를 들어 *Default.htm* 이 사이트에 대 한 기본 페이지로 설정 된 경우로 이동 하는 것 `www.contoso.com` `www.contoso.com` 은로 이동 하는 것과 같습니다 `www.contoso.com/Default.htm` .</span><span class="sxs-lookup"><span data-stu-id="230c5-137">For example, when *Default.htm* is set as the default page for the site at `www.contoso.com`, then navigating to `www.contoso.com` is the same as navigating to `www.contoso.com/Default.htm`.</span></span>

<span data-ttu-id="230c5-138">현재 사이트에서 기본 페이지로 **기본값. cshtml** 을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-138">Currently, your site uses **Default.cshtml** as the default page.</span></span> <span data-ttu-id="230c5-139">이 페이지는 기본 페이지에는 적합 하지만이 자습서에서는 빈 페이지가 표시 되도록 해당 페이지에 콘텐츠를 추가 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-139">This page is fine for your default page, but in this tutorial you have not added any content to that page so it would display a blank page.</span></span> <span data-ttu-id="230c5-140">기본. cshtml를 열고 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-140">Open Default.cshtml and replace the content with the following code.</span></span>

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

<span data-ttu-id="230c5-141">이제 사이트를 게시할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-141">Now your site is ready for publication.</span></span> <span data-ttu-id="230c5-142">먼저 사이트를 Azure에 배포 하는 방법 및 웹 호스팅 회사에 배포 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-142">First, you will see how to deploy the site to Azure, and then how to deploy it to a web hosting company.</span></span> <span data-ttu-id="230c5-143">두 옵션 중 하나는 웹 사이트에서 작동 하며, 배포 옵션 중 하나를 수행 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-143">Either option works for your web site, and you only need to follow one of the deployment options.</span></span>

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a><span data-ttu-id="230c5-144">Microsoft Azure에 사이트 게시</span><span class="sxs-lookup"><span data-stu-id="230c5-144">Publishing Your Site to Microsoft Azure</span></span>

<span data-ttu-id="230c5-145">이 자습서에서는 먼저 Microsoft Azure에 사이트를 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-145">This tutorial will first show you how to deploy your site to Microsoft Azure.</span></span> <span data-ttu-id="230c5-146">Microsoft 계정를 사용 하 여 로그인 하면 Azure에서 최대 10 개의 무료 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-146">By signing in with a Microsoft account, you can create up to 10 free sites on Azure.</span></span> <span data-ttu-id="230c5-147">이러한 무료 사이트는 사이트를 테스트 하는 편리한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-147">These free sites provide a convenient way to test your sites.</span></span> <span data-ttu-id="230c5-148">모든 무료 사이트를 사용 하지 않도록 하려면 나중에이 예제 사이트를 언제 든 지 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-148">You can always delete this example site later to avoid using all of your free sites.</span></span> <span data-ttu-id="230c5-149">몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-149">You can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="230c5-150">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/free/dotnet/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="230c5-150">For details, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

<span data-ttu-id="230c5-151">WebMatrix 리본에서 **게시** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-151">In the WebMatrix ribbon, click the **Publish** button.</span></span>

![WebMatrix 리본의 ' 게시 ' 단추](publishing/_static/image1.png)

<span data-ttu-id="230c5-153">**사이트 게시** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-153">The **Publish Your Site** dialog box is displayed.</span></span> <span data-ttu-id="230c5-154">Microsoft 계정에 로그인 하지 않은 경우 대화 상자에 **Azure 시작** 링크가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-154">If you have not signed in to your Microsoft account, the dialog box will contain a **Get started with Azure** link.</span></span> <span data-ttu-id="230c5-155">이 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-155">Click this link.</span></span>

![사이트 게시](publishing/_static/image2.png)

<span data-ttu-id="230c5-157">Microsoft 계정에 로그인 하지 않은 경우에는 다시 로그인 할 수 있는 기회가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-157">If you have not signed in to a Microsoft account, you are again given the opportunity to sign in.</span></span> <span data-ttu-id="230c5-158">Microsoft 계정에 로그인 하 여 Azure에서 사이트를 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-158">You must sign in to a Microsoft account to publish your site on Azure.</span></span>

![링크를](publishing/_static/image3.png)

<span data-ttu-id="230c5-160">Microsoft 계정에 로그인 한 후에는 Azure에서 새 사이트를 만들거나 Azure의 기존 사이트 중 하나에 연결할 수 있는 링크가 대화 상자에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-160">After signing in to your Microsoft account, the dialog box contains links to create a new site on Azure or connect to one of your existing sites on Azure.</span></span>

![새 사이트 만들기](publishing/_static/image4.png)

<span data-ttu-id="230c5-162">**새 사이트 만들기를**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-162">Select **Create a new site**.</span></span>

<span data-ttu-id="230c5-163">프로젝트의 이름을 **Webpagesmovies**로 지정 하면 사이트의 기본 이름이 **webpagesmovies.azurewebsites.net**됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-163">If you named your project **WebPagesMovies**, the default name for your site will be **webpagesmovies.azurewebsites.net**.</span></span> <span data-ttu-id="230c5-164">이 기본 이름은 빨간색 느낌표로 표시 된 것과 같이 사용 하지 않을 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-164">This default name is most likely not available, as indicated by the red exclamation mark.</span></span>

![기본 웹 사이트 이름](publishing/_static/image5.png)

<span data-ttu-id="230c5-166">사이트 이름을 사용할 수 있는 항목으로 변경 하 고 위치에 가까운 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-166">Change the site name to something that is available, and select a location that is close to your location.</span></span>

![변경 된 사이트 이름](publishing/_static/image6.png)

<span data-ttu-id="230c5-168">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-168">Click **OK**.</span></span>

<span data-ttu-id="230c5-169">WebMatrix performss 서버가 사이트와 호환 되는지 확인 하는 테스트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-169">WebMatrix performss a test to determine if the server is compatible with your site.</span></span>

![호환성 테스트](publishing/_static/image7.png)

<span data-ttu-id="230c5-171">**계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-171">Select **Continue**.</span></span>

<span data-ttu-id="230c5-172">호환성 테스트 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-172">The results of the compatibility test are displayed.</span></span>

![호환성 결과](publishing/_static/image8.png)

<span data-ttu-id="230c5-174">**계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-174">Select **Continue**.</span></span>

<span data-ttu-id="230c5-175">WebMatrix 사이트에 게시 될 파일 및 데이터베이스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-175">WebMatrix displays the files and databases that will be published to the site.</span></span> <span data-ttu-id="230c5-176">처음으로 사이트를 게시 하는 중 이므로 모든 파일이 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-176">Since this is the first time you are publishing the site, all of the files are listed.</span></span> <span data-ttu-id="230c5-177">게시할 준비가 되지 않은 파일은 선택 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-177">You can uncheck a file that is not ready to be published.</span></span> <span data-ttu-id="230c5-178">이후 게시에서는 변경 된 파일만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-178">In the subsequent publications, only the files that have changed will be displayed.</span></span> <span data-ttu-id="230c5-179">[라이브 사이트 업데이트: 다시 게시](#update)를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="230c5-179">See [Updating the Live Site: Republishing](#update).</span></span>

![게시 미리 보기](publishing/_static/image9.png)

<span data-ttu-id="230c5-181">**계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-181">Select **Continue**.</span></span>

<span data-ttu-id="230c5-182">사이트가 Azure에 배포 된 후 배포가 완료 되었음을 나타내는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-182">After the site has been deployed to Azure, a message is displayed that indicates the deployment has completed.</span></span>

![게시 완료](publishing/_static/image10.png)

<span data-ttu-id="230c5-184">사이트와 데이터베이스가 Azure에 게시 되었으며 이제 공용에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-184">Your site and database have been published to Azure, and are now available to the public.</span></span> <span data-ttu-id="230c5-185">게시가 완료 되었음을 나타내는 메시지의 링크를 클릭 하면 배포 된 사이트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-185">Click the link in the message indicating publishing has completed, and you will now see your deployed site.</span></span> <span data-ttu-id="230c5-186">사용자 또는 인터넷에 액세스할 수 있는 모든 사용자가 데이터베이스에서 레코드를 추가 하거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-186">You or anyone with Internet access can add or modify records in the database.</span></span>

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a><span data-ttu-id="230c5-187">웹 호스팅 회사에 사이트 게시</span><span class="sxs-lookup"><span data-stu-id="230c5-187">Publishing Your Site to a Web Hosting Company</span></span>

<span data-ttu-id="230c5-188">Azure에 게시 하지 않기로 결정 한 경우 웹 호스팅 회사에 사이트를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-188">If you decide to not publish to Azure, you can instead publish your site to a web hosting company.</span></span>

<span data-ttu-id="230c5-189">**웹 호스팅 검색** 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-189">Click the **Find web hosting** link.</span></span>

![게시 설정 대화 상자에서 ' 웹 호스팅 찾기 ' 단추](publishing/_static/image12.png)

<span data-ttu-id="230c5-191">ASP.NET를 지 원하는 호스팅 공급자가 나열 된 Microsoft 사이트 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-191">You go to a page on the Microsoft site that lists hosting providers that support ASP.NET.</span></span>

![호스팅 공급자가 나열 된 Microsoft 사이트 페이지](publishing/_static/image13.png)

<span data-ttu-id="230c5-193">물론 장기적으로 필요한 호스팅 기능을 정확 하 게 파악 하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-193">Obviously, it can be difficult to know now exactly what hosting features you might require over the long term.</span></span> <span data-ttu-id="230c5-194">다음은 고려해 야 할 몇 가지 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-194">Here are a couple of things to consider:</span></span>

- <span data-ttu-id="230c5-195">WebPagesMovies 사이트의 목적에 따라 SQL Server에 대 한 별도의 추가 기능이 필요 하지 않으므로 비용이 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-195">For purposes of the WebPagesMovies site, you don't have to have a separate add-on for SQL Server, which often costs extra.</span></span> <span data-ttu-id="230c5-196">사이트에서 자체 포함 된 SQL Server Compact Edition을 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-196">In your site, you're using SQL Server Compact Edition, which is self-contained.</span></span> <span data-ttu-id="230c5-197">그러나 앞으로 수행 하는 몇 가지 웹 사이트 작업에 대 한 SQL Server 액세스 권한이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-197">However, you might need SQL Server access for some future website work you do.</span></span> <span data-ttu-id="230c5-198">가능 하다 고 생각 되 면 나중에 SQL Server 기능을 추가할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-198">If you think you might, make sure that you can add SQL Server capability later.</span></span>
- <span data-ttu-id="230c5-199">호스팅 공급자가 웹 배포 게시 프로토콜을 지원 하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-199">Check whether the hosting provider supports the Web Deploy publishing protocol.</span></span> <span data-ttu-id="230c5-200">FTP 프로토콜을 사용 하 여 게시할 수 있지만 웹 배포 사용 하는 것이 더 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-200">You can publish by using FTP protocol, but it's more convenient to use Web Deploy.</span></span>

<span data-ttu-id="230c5-201">일부 사이트는 무료 평가판 기간을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-201">Some sites offer a free trial period.</span></span> <span data-ttu-id="230c5-202">WebMatrix를 사용 하 여 계속 실험 하 고 ASP.NET 웹 페이지 하는 동안 무료 평가판은 게시 및 호스팅을 시도 하는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-202">A free trial is a good way to try publishing and hosting while you're still experimenting with WebMatrix and ASP.NET Web Pages.</span></span>

<span data-ttu-id="230c5-203">원하는 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-203">Pick one that you like.</span></span> <span data-ttu-id="230c5-204">이 자습서에서는 DiscountASP.NET를 선택 했습니다. 자습서를 만드는 동안 해당 회사에는 몇 달 동안 사이트를 무료로 호스트할 수 있는 판촉이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-204">For this tutorial, we selected DiscountASP.NET, because while we were creating the tutorial, that company had a promotion that let people host a site free for a few months.</span></span>

> [!NOTE]
> <span data-ttu-id="230c5-205">이 자습서의 호스팅 공급자를 선택 하는 것은 다른 회사에 대 한 해당 회사의 보증으로 해석 되어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-205">Our choice of a hosting provider for this tutorial shouldn't be interpreted as an endorsement of that company over any other.</span></span> <span data-ttu-id="230c5-206">그러나 설명을 위해 하나를 선택 해야 하 고 DiscountASP.NET는 ASP.NET 웹 페이지을 지 원하는 여러 회사 중 하 나와 게시를 위한 웹 배포 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-206">But we had to pick one for illustration, and DiscountASP.NET is one of the many companies that supports ASP.NET Web Pages and the Web Deploy protocol for publishing.</span></span>

<span data-ttu-id="230c5-207">일반적으로 호스팅 공급자에 등록 한 후 회사는 사용자 이름 및 암호, 웹 서버의 URL 등을 포함 하는 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-207">Typically, after you've signed up with the hosting provider, the company sends you an email that contains a user name and password, the URL of the web server, and so on.</span></span> <span data-ttu-id="230c5-208">호스팅 회사에서 웹 배포 프로토콜을 지 원하는 경우 게시 설정을 포함 하는 파일을 보내거나 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-208">If the hosting company supports Web Deploy protocol, they might send you a file that contains publish settings, or let you download one.</span></span> <span data-ttu-id="230c5-209">게시 설정 파일은 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-209">A publish settings file simplifies the process for you.</span></span>

<span data-ttu-id="230c5-210">등록 하 고 게시할 준비가 되 면 WebMatrix 리본에서 **게시** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-210">When you've signed up and are ready to publish, click the **Publish** button in the WebMatrix ribbon.</span></span> <span data-ttu-id="230c5-211">**게시 설정** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-211">The **Publish Settings** dialog box is displayed.</span></span>

<span data-ttu-id="230c5-212">호스팅 공급자가 게시 설정 파일을 보낸 경우 **게시 설정 가져오기** 링크를 클릭 하 고 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-212">If the hosting provider sent you a publish settings file, click the **Import publish settings** link and import the file.</span></span> <span data-ttu-id="230c5-213">게시 설정 파일이 없는 경우 호스팅 회사에서 전자 메일로 보낸 값을 사용 하 여 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-213">If you don't have a publish settings file, fill in the fields by using the values that the hosting company sent you in email.</span></span> <span data-ttu-id="230c5-214">완료 되 면 **게시 설정** 대화 상자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-214">Here's what the **Publish Settings** dialog box might look like when you're done:</span></span>

![' 게시 설정 ' 대화 상자에 채워진 게시 설정](publishing/_static/image14.png)

<span data-ttu-id="230c5-216">**연결 유효성 검사**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-216">Click **Validate Connection**.</span></span> <span data-ttu-id="230c5-217">모든 항목이 양호 하면 대화 상자가 **성공적으로 연결**된 것입니다. 즉, 호스팅 공급자의 서버와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-217">If everything is ok, the dialog box reports **Connected successfully**, which means it can communicate with the hosting provider's server.</span></span>

![게시 설정이 올바르면 성공 메시지](publishing/_static/image15.png)

<span data-ttu-id="230c5-219">문제가 발생 하는 경우 WebMatrix는 문제의 원인을 알려 주는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-219">If there's a problem, WebMatrix does its best to tell you what the problem is:</span></span>

![게시 설정에 문제가 있는 경우 오류 메시지](publishing/_static/image16.png)

<span data-ttu-id="230c5-221">**Save** 를 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-221">Click **Save** to save your settings.</span></span> <span data-ttu-id="230c5-222">WebMatrix는 테스트를 수행 하 여 호스팅 사이트와 올바르게 통신할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-222">WebMatrix offers to perform a test to make sure that it can communicate correctly with the hosting site:</span></span>

![게시 프로세스의 테스트를 수행 하는 메시지 제공](publishing/_static/image17.png)

<span data-ttu-id="230c5-224">**예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-224">Click **Yes**.</span></span> <span data-ttu-id="230c5-225">WebMatrix는 일부 샘플 파일을 호스팅 공급자에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-225">WebMatrix uploads some sample files to the hosting provider.</span></span> <span data-ttu-id="230c5-226">호환성 테스트가 완료 되 면 WebMatrix는 결과를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-226">When the compatibility test is done, WebMatrix reports the results:</span></span>

![게시 테스트의 결과](publishing/_static/image18.png)

<span data-ttu-id="230c5-228">준비가 되 면 계속 진행 하 고 **계속** 을 클릭 하 여 실제 게시 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-228">If you're ready to go, go ahead and click **Continue** to start the publish process for real.</span></span> <span data-ttu-id="230c5-229">WebMatrix는 사이트에 있으며 이미 호스트 서버에 있는 파일 (현재는 없음)을 파악 하 고 게시 프로세스의 미리 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-229">WebMatrix figures out what files are in your site and are already on the host server (right now, none) and gives you a preview of the publish process:</span></span>

![게시 프로세스에서 업로드할 파일의 미리 보기](publishing/_static/image19.png)

<span data-ttu-id="230c5-231">게시할 파일 목록에는 *동영상과*같이 만든 웹 페이지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-231">The list of files to publish includes the web pages that you've created like *Movies.cshtml*.</span></span> <span data-ttu-id="230c5-232">이 목록에는 사용자가 설치한 도우미에 대 한 파일, 데이터베이스의 SQL Server Compact Edition을 실행 하는 데 사용할 파일 등도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-232">The list also includes files for helpers that you've installed, the files to run SQL Server Compact Edition for your database, and so on.</span></span> <span data-ttu-id="230c5-233">결과적으로 초기 게시 프로세스가 상당히 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-233">As a result, the initial publish process can be substantial.</span></span>

<span data-ttu-id="230c5-234">**Continue(계속)** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-234">Click **Continue**.</span></span> <span data-ttu-id="230c5-235">WebMatrix는 호스팅 공급자의 서버에 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-235">WebMatrix copies your files to the hosting provider's server.</span></span> <span data-ttu-id="230c5-236">작업이 완료 되 면 상태 표시줄에 결과가 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-236">When it's done, the results are reported in the status bar:</span></span>

![게시 프로세스가 성공적으로 완료 된 경우의 상태 표시줄 메시지](publishing/_static/image20.png)

<span data-ttu-id="230c5-238">라이브 사이트를 보려면 상태 표시줄의 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-238">To see your live site, click the link in the status bar.</span></span> <span data-ttu-id="230c5-239">URL에 *영화* 를 추가 하면 사용자가 만든 *동영상과* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-239">Add *Movies* to the URL, and you'll see the *Movies.cshtml* file that you created:</span></span>

![동영상 페이지를 표시 하는 라이브 사이트](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a><span data-ttu-id="230c5-241">라이브 사이트 업데이트: 다시 게시</span><span class="sxs-lookup"><span data-stu-id="230c5-241">Updating the Live Site: Republishing</span></span>

<span data-ttu-id="230c5-242">Azure 또는 웹 호스팅 회사에 사이트를 게시 한 후에는 &mdash; 컴퓨터의 버전과 서비스 공급자의 버전 중 두 개의 복사본이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-242">Once you've published your site (to either Azure or a web hosting company), there are two copies of it &mdash; the version on your computer and the version on the service provider.</span></span> <span data-ttu-id="230c5-243">사이트를 계속 개발할 수 있습니다 (다른 작업을 수행 하는 경우 다음 자습서의 일부로).</span><span class="sxs-lookup"><span data-stu-id="230c5-243">You'll probably want to continue developing the site (if nothing else, as part of the next tutorial set).</span></span> <span data-ttu-id="230c5-244">이렇게 하면 컴퓨터의 변경 내용을 서비스 공급자로 복사 하기 위해 사이트를 다시 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-244">When you do, you have to republish your site in order to copy changes from your computer to the service provider.</span></span> <span data-ttu-id="230c5-245">WebMatrix의 게시 프로세스는 사이트에서 변경 된 파일을 확인 하 고 해당 파일만 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-245">The publish process in WebMatrix can determine what files have changed on your site and publish just those files.</span></span>

<span data-ttu-id="230c5-246">재게시가 어떻게 작동 하는지 확인 하려면 *동영상. cshtml* 사이트를 열고 약간 변경 하 고 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-246">To see how republishing works, open the *Movies.cshtml* site, make some small change, and then save the file.</span></span> <span data-ttu-id="230c5-247">예를 들어 제목을로 변경 합니다 `Movies - Updated` .</span><span class="sxs-lookup"><span data-stu-id="230c5-247">For example, change the title to `Movies - Updated`.</span></span>

<span data-ttu-id="230c5-248">리본에서 **게시** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-248">Click the **Publish** button in the ribbon.</span></span> <span data-ttu-id="230c5-249">WebMatrix는 변경 된 내용을 확인 하 고 게시 되는 파일의 미리 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-249">WebMatrix determines what's changed and shows you a preview of the files it will publish.</span></span>

![다시 게시할 준비가 된 변경 된 파일을 보여 주는 ' 게시 ' 대화 상자](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> <span data-ttu-id="230c5-251">기본적으로 WebMatrix는 처음 사이트를 게시할 때만 데이터베이스 (*.sdf* 파일)를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-251">By default, WebMatrix publishes your database (*.sdf* file) only the first time you publish the site.</span></span> <span data-ttu-id="230c5-252">사이트가 게시 되 고 사람들이 웹 사이트와 상호 작용 하는 경우 라이브 사이트의 데이터베이스에는 일반적으로 사이트의 실제 데이터가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-252">Once your site is published and people are interacting with the website, the database on the live site typically has the site's real data.</span></span> <span data-ttu-id="230c5-253">일반적으로 테스트 데이터만 포함 하는 컴퓨터에 있는 *.sdf* 파일로 라이브 데이터베이스를 덮어쓰지 않도록 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-253">You have to be very careful not to overwrite the live database with the *.sdf* file that's on your computer, which usually contains only test data.</span></span> <span data-ttu-id="230c5-254">이러한 이유로 **인해 게시는 원격 데이터베이스를 덮어쓰고**webstels 확인란은 기본적으로 선택 취소 되어 *WebPagesMovies.sdf* 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-254">That's why you see the warning **Publishing will overwrite any remote databases**, and why the check box for *WebPagesMovies.sdf* is cleared by default.</span></span>

<span data-ttu-id="230c5-255">**Continue(계속)** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-255">Click **Continue**.</span></span> <span data-ttu-id="230c5-256">WebMatrix는 처음 게시 했을 때와 같이 변경 된 파일을 게시 하 고 성공 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-256">WebMatrix publishes the changed files and shows you a success message, like it did the first time you published.</span></span>

<span data-ttu-id="230c5-257">라이브 사이트로 이동 하 고 (계속 표시 되는 경우 성공 메시지의 링크를 클릭 하 여) 변경 내용이 게시 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-257">Go to the live site (you can click the link in the success message if it's still showing) and verify that your change has been published.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="230c5-258">**원격으로 파일 편집**</span><span class="sxs-lookup"><span data-stu-id="230c5-258">**Editing Files Remotely**</span></span>
> 
> <span data-ttu-id="230c5-259">사이트를 변경 하 고 다시 게시 하는 대신 WebMatrix에서 직접 원격 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-259">As an alternative to changing your site and then republishing, you can edit remote files directly in WebMatrix.</span></span> <span data-ttu-id="230c5-260">이 시나리오에서는 서비스 공급자에 있는 파일을 열고 WebMatrix는 편집할 수 있도록 해당 파일의 복사본을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-260">In this scenario, you open a file that's on the service provider, and WebMatrix downloads a copy of it for you to edit.</span></span> <span data-ttu-id="230c5-261">WebMatrix는 파일을 저장할 때마다 변경 내용을 사이트로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-261">Every time you save the file, WebMatrix sends the changes to the site.</span></span>
> 
> <span data-ttu-id="230c5-262">원격 편집은 라이브 사이트를 변경 하는 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-262">Remote editing is an easy way to make changes to your live site.</span></span> <span data-ttu-id="230c5-263">그러나이 방법으로 변경한 내용은 로컬 사이트의 파일과 동기화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-263">However, the changes you make this way aren't synchronized with the files in your local site.</span></span> <span data-ttu-id="230c5-264">로컬 파일을 원격 사이트와 동기화 하기 위해 원격 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-264">To synchronize the local files with the remote site, you can download the remote files.</span></span> <span data-ttu-id="230c5-265">이 프로세스는 역방향을 제외 하 고 게시와 매우 유사 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-265">This process works much like publishing, except in reverse.</span></span>
> 
> <span data-ttu-id="230c5-266">여기에서는 WebMatrix의 원격 편집 및 원격 다운로드 기능에 대해 자세히 설명 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-266">We won't describe more about the remote-editing and remote-download facilities of WebMatrix here.</span></span> <span data-ttu-id="230c5-267">여러 사용자가 서로 다른 컴퓨터의 동일한 사이트에서 작업 해야 하는 경우에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-267">They're quite useful if multiple people have to work on the same site on different computers.</span></span> <span data-ttu-id="230c5-268">자세한 내용은 [WebMatrix 2 Beta를 사용 하 여 원격 사이트 게시 및 편집](https://go.microsoft.com/fwlink/?LinkId=251591)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="230c5-268">For more information, see [Publish and Edit a Remote Site with WebMatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="230c5-269">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="230c5-269">Additional Resources</span></span>

- <span data-ttu-id="230c5-270">[ASP.NET WebMatrix ASP.NET 웹 페이지 포럼](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages)에서 질문을 게시 하 고 답변을 얻을 수 있는 좋은 장소입니다.</span><span class="sxs-lookup"><span data-stu-id="230c5-270">[ASP.NET WebMatrix ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), a great place to post questions and get answers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="230c5-271">이전</span><span class="sxs-lookup"><span data-stu-id="230c5-271">Previous</span></span>](layouts.md)
