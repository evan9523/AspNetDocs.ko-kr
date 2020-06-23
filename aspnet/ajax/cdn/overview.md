---
uid: ajax/cdn/overview
title: Microsoft Ajax Content Delivery Network | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: b66e812f0324be95effdd8d232baa6a59302b9df
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240603"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="19ecf-102">Microsoft Ajax Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="19ecf-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="19ecf-103">프로덕션 응용 프로그램은 CDN 자산에 대 한 하드 종속성을 사용 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="19ecf-104">응용 프로그램은 참조 된 CDN 자산을 테스트 하 고 CDN을 사용할 수 없는 경우 대체 (fallback) 자산을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="19ecf-105">Microsoft Ajax CDN은 Azure CDN를 사용 하는 것 이상의 SLA를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="19ecf-106">Microsoft Ajax CDN 문제를 보고 하려면 [이 GitHub 문제](https://github.com/dotnet/AspNetDocs/issues/116) 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="19ecf-107">목차</span><span class="sxs-lookup"><span data-stu-id="19ecf-107">Table of Contents</span></span>

<span data-ttu-id="19ecf-108">**[ajax.microsoft.com 이름이 ajax.aspnetcdn.com로 바뀜](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="19ecf-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="19ecf-109">**[Visual Studio. vsdoc 지원](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="19ecf-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="19ecf-110">**[CDN에서 ASP.NET Ajax 사용](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="19ecf-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="19ecf-111">**[CDN에서 jQuery 사용](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="19ecf-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="19ecf-112">**[CDN에서 jQuery UI 사용](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="19ecf-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="19ecf-113">**[CDN의 타사 파일](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="19ecf-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="19ecf-114">CDN의 jQuery 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="19ecf-115">CDN에서 jQuery 마이그레이션 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="19ecf-116">CDN의 jQuery UI 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="19ecf-117">CDN의 jQuery 유효성 검사 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="19ecf-118">CDN의 jQuery Mobile 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="19ecf-119">CDN에서 jQuery 템플릿 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="19ecf-120">CDN의 jQuery 주기 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="19ecf-121">CDN의 jQuery Datatable 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="19ecf-122">CDN의 Modernizr 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="19ecf-123">CDN의 JSHint 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="19ecf-124">CDN의 릴리스 녹아웃</span><span class="sxs-lookup"><span data-stu-id="19ecf-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="19ecf-125">CDN의 세계화 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="19ecf-126">CDN에 대 한 응답 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="19ecf-127">CDN의 부트스트랩 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="19ecf-128">CDN의 부트스트랩 TouchCarousel 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="19ecf-129">CDN의Hammer.js 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="19ecf-130">ASP.NET Web Forms 및 CDN의 Ajax 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="19ecf-131">CDN의 ASP.NET MVC 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="19ecf-132">CDN의 ASP.NET SignalR 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="19ecf-133">Microsoft Ajax Content Delivery Network (CDN)는 jQuery와 같은 인기 있는 타사 JavaScript 라이브러리를 호스팅하고 웹 응용 프로그램에 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="19ecf-134">예를 들어 &lt; &gt; ajax.aspnetcdn.com를 가리키는 페이지에 스크립트 태그를 추가 하 여이 CDN에서 호스팅되는 jQuery를 사용 하 여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="19ecf-135">CDN을 활용 하 여 Ajax 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="19ecf-136">CDN의 콘텐츠는 전 세계에 있는 서버에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="19ecf-137">또한 CDN을 사용 하면 브라우저에서 다른 도메인에 있는 웹 사이트에 대해 캐시 된 타사 JavaScript 파일을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="19ecf-138">CDN은 SSL(Secure Sockets Layer)를 사용 하 여 웹 페이지를 제공 해야 하는 경우 SSL (HTTPS)을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="19ecf-139">CDN은 해당 라이브러리의 소유자가 업로드 하 고 사용이 허가 된 다음 타사 스크립트 라이브러리를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="19ecf-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="19ecf-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="19ecf-141">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="19ecf-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="19ecf-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="19ecf-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="19ecf-143">jQuery 유효성 검사 (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="19ecf-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="19ecf-144">jQuery 주기 (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="19ecf-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="19ecf-145">jQuery Datatable (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="19ecf-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="19ecf-146">Microsoft Ajax CDN에는 Microsoft에서 업로드 한 다음 라이브러리도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="19ecf-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="19ecf-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="19ecf-148">ASP.NET MVC JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="19ecf-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="19ecf-149">ASP.NET SignalR JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="19ecf-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="19ecf-150">Microsoft는이 CDN에서 호스트 되는 타사 라이브러리의 소유권을 주장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="19ecf-151">라이브러리의 저작권 소유자는 이러한 라이브러리에 대 한 라이선스를 사용자에 게 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="19ecf-152">이러한 라이브러리를 다운로드 하 여 사용 해야 하는 모든 권한은 해당 저작권 소유자에 의해서만 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="19ecf-153">Microsoft 라이브러리가 아니기 때문에 Microsoft는이 CDN에서 호스트 되는 타사 라이브러리에 대 한 보증 또는 지적 재산권 (묵시적 특허 권리 없음)을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="19ecf-154">JavaScript 라이브러리를 제출 하려는 경우 라이브러리는 http://trends.builtwith.com) (a) 인기 있는 이러한 라이브러리에 대 한 확장/플러그인 또는에 나열 된 최상위 javascript 라이브러리 중 하나 이며 (b) ASP.NET에서 사용 하는 데 도움이 AjaxCDNSubmission@Microsoft.com 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="19ecf-155">ajax.microsoft.com 이름이 ajax.aspnetcdn.com로 바뀜</span><span class="sxs-lookup"><span data-stu-id="19ecf-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="19ecf-156">CDN은 microsoft.com 도메인 이름을 사용 하는 데 사용 되며 aspnetcdn.com 도메인 이름을 사용 하도록 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="19ecf-157">브라우저에서 microsoft.com 도메인을 참조할 때 각 요청과 함께 네트워크를 통해 해당 도메인의 쿠키를 전송 하기 때문에 성능이 향상 되도록 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="19ecf-158">Microsoft.com가 아닌 도메인 이름으로 이름을 바꾸면 25%까지 늘어날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="19ecf-159">참고 ajax.microsoft.com는 계속 작동 하지만 ajax.aspnetcdn.com 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="19ecf-160">이전 형식:https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="19ecf-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="19ecf-161">새 형식:https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="19ecf-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="19ecf-162">Visual Studio. vsdoc 지원</span><span class="sxs-lookup"><span data-stu-id="19ecf-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="19ecf-163">Visual Studio 2008에서. vsdoc 파일을 제대로 사용 하려면 VS 2008 s p 1이 설치 되어 있고 vsdoc 파일용 핫픽스가 설치 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="19ecf-164">다음에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-164">You can get these from here:</span></span>

- [<span data-ttu-id="19ecf-165">Visual Studio 2008 SP1 다운로드</span><span class="sxs-lookup"><span data-stu-id="19ecf-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Visual Studio 2008 SP1 다운로드")
- [<span data-ttu-id="19ecf-166">Visual Studio 2008 s p 1 용. vsdoc 핫픽스를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "Visual Studio 2008 s p 1 용. vsdoc 핫픽스를 다운로드 합니다.")

<span data-ttu-id="19ecf-167">Visual Studio 2010는 추가 패치 없이. s a s doc 파일을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="19ecf-168">CDN에서 ASP.NET Ajax 사용</span><span class="sxs-lookup"><span data-stu-id="19ecf-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="19ecf-169">ASP.NET 4를 사용 하는 경우 ASP.NET 프레임 워크 스크립트에 대 한 모든 요청을 CDN으로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="19ecf-170">로컬 웹 서버 대신 CDN에서 스크립트를 검색 하면 공용 ASP.NET 웹 사이트의 성능을 크게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="19ecf-171">ScriptManager EnableCDN 속성을 사용 하 여 모든 ASP.NET framework 스크립트 요청을 Microsoft Ajax CDN으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="19ecf-172">CDN에서 jQuery 사용</span><span class="sxs-lookup"><span data-stu-id="19ecf-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="19ecf-173">페이지에 다음 스크립트 요소를 추가 하 여 웹 응용 프로그램에서 CDN에 호스팅된 jQuery 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="19ecf-174">CDN에는 다음 요소를 사용 하 여 가져올 수 있는 jQuery 스크립트의 버전이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="19ecf-175">CDN을 사용할 수 없는 경우 자체 웹 사이트의 로컬 경로에서 jQuery를 로드 하도록 페이지를 대체 하려면 CDN을 참조 하는 요소 바로 뒤에 다음 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="19ecf-176">다음 샘플 페이지에서는 로컬 복사본에 대 한 대체 (fallback)를 사용 하 여 단추를 클릭할 때 div 요소의 내용을 표시 하는 jQuery 라이브러리의 CDN 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="19ecf-177">[Jquery 웹 사이트](http://jquery.com/) 를 방문 하 여 jquery에 대 한 자세한 내용을 확인 하 고 jquery의 로컬 복사본을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="19ecf-178">CDN에서 jQuery UI 사용</span><span class="sxs-lookup"><span data-stu-id="19ecf-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="19ecf-179">CDN은 jQuery UI 라이브러리도 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="19ecf-180">JQuery UI 라이브러리에는 ASP.NET 응용 프로그램에서 사용할 수 있는 다양 한 위젯 및 효과 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="19ecf-181">예를 들어 다음 페이지에서는 ASP.NET Web Forms 응용 프로그램의 컨텍스트에서 jQuery UI Datepicker를 사용 하 여 팝업 달력을 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="19ecf-182">키보드를 사용 하 여 포커스를 TextBox로 이동 하면 달력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![Datepicker를 사용 하 여 만든 팝업 달력](overview/_static/image1.png)

<span data-ttu-id="19ecf-184">위의 코드에서 CDN의 파일 3 개를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="19ecf-185">Jquery 라이브러리는 jquery &mdash; UI 라이브러리에 종속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="19ecf-186">JQuery UI 라이브러리를 추가 하기 전에 jQuery 라이브러리를 페이지에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="19ecf-187">Jquery ui 라이브러리 jQuery ui 라이브러리에는 &mdash; 위의 페이지에서 사용 된 Datepicker widget과 같은 모든 JQUERY ui 효과 및 위젯이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="19ecf-188">Jquery ui 테마 &mdash; JQUERY ui는 다른 테마를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="19ecf-189">위의 페이지에는 Redmond 테마를 가져오는 CSS 파일에 대 한 링크가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="19ecf-190">모든 표준 jQuery UI 테마는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="19ecf-191">[이 페이지를 방문](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN의 jQuery UI 1.8.10") 하 여 각 테마의 미리 보기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="19ecf-192">JQuery UI 라이브러리에 대해 자세히 알아보려면 공식 [JQUERY ui 웹 사이트](http://jQueryUI.com "jQuery UI 웹 사이트")를 방문 하세요.</span><span class="sxs-lookup"><span data-stu-id="19ecf-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="19ecf-193">CDN의 타사 파일</span><span class="sxs-lookup"><span data-stu-id="19ecf-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="19ecf-194">CDN은 가장 인기 있는 타사 JavaScript 라이브러리 중 일부를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="19ecf-195">Microsoft는이 CDN에서 호스트 되는 타사 라이브러리의 소유권을 주장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="19ecf-196">라이브러리의 저작권 소유자는 이러한 라이브러리에 대 한 라이선스를 사용자에 게 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="19ecf-197">이러한 라이브러리를 다운로드 하 여 사용 해야 하는 모든 권한은 해당 저작권 소유자에 의해서만 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="19ecf-198">Microsoft 라이브러리가 아니기 때문에 Microsoft는이 CDN에서 호스트 되는 타사 라이브러리에 대 한 보증 또는 지적 재산권 (묵시적 특허 권리 없음)을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="19ecf-199">CDN의 jQuery 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="19ecf-200">다음 jQuery 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-350"></a><span data-ttu-id="19ecf-201">jQuery 버전 3.5.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-201">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="19ecf-202">jQuery 버전 3.4.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-202">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="19ecf-203">jQuery 버전 3.4.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-203">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="19ecf-204">jQuery 버전 3.3.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-204">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="19ecf-205">jQuery 버전 3.2.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-205">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="19ecf-206">jQuery 버전 3.2.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-206">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="19ecf-207">jQuery 버전 3.1.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-207">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="19ecf-208">jQuery 버전 3.1.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-208">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="19ecf-209">jQuery 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-209">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="19ecf-210">jQuery 버전 2.2.4</span><span class="sxs-lookup"><span data-stu-id="19ecf-210">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="19ecf-211">jQuery 버전 2.2.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-211">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="19ecf-212">jQuery 버전 2.2.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-212">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="19ecf-213">jQuery 버전 2.2.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-213">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="19ecf-214">jQuery 버전 2.2.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-214">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="19ecf-215">jQuery 버전 2.1.4</span><span class="sxs-lookup"><span data-stu-id="19ecf-215">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="19ecf-216">jQuery 버전 2.1.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-216">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="19ecf-217">jQuery 버전 2.1.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-217">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="19ecf-218">jQuery 버전 2.1.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-218">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="19ecf-219">jQuery 버전 2.1.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-219">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="19ecf-220">jQuery 버전 2.0.3 라이브러리가</span><span class="sxs-lookup"><span data-stu-id="19ecf-220">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="19ecf-221">jQuery 버전 2.0.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-221">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="19ecf-222">jQuery 버전 2.0.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-222">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="19ecf-223">jQuery 버전 2.0.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-223">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="19ecf-224">jQuery 버전 1.12.4</span><span class="sxs-lookup"><span data-stu-id="19ecf-224">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="19ecf-225">jQuery 버전 1.12.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-225">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="19ecf-226">jQuery 버전 1.12.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-226">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="19ecf-227">jQuery 버전 1.12.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-227">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="19ecf-228">jQuery 버전 1.12.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-228">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="19ecf-229">jQuery 버전 1.11.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-229">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="19ecf-230">jQuery 버전 1.11.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-230">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="19ecf-231">jQuery 버전 1.11.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-231">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="19ecf-232">jQuery 버전 1.11.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-232">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="19ecf-233">jQuery 버전 1.10.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-233">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="19ecf-234">jQuery 버전 1.10.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-234">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="19ecf-235">jQuery 버전 1.10.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-235">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="19ecf-236">jQuery 버전 1.9.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-236">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="19ecf-237">jQuery 버전 1.9.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-237">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="19ecf-238">jQuery 버전 1.8.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-238">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="19ecf-239">jQuery 버전 1.8.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-239">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="19ecf-240">jQuery 버전 1.8.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-240">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="19ecf-241">jQuery 버전 1.8.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-241">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="19ecf-242">jQuery 버전 1.7.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-242">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="19ecf-243">jQuery 버전 1.7.1 for</span><span class="sxs-lookup"><span data-stu-id="19ecf-243">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="19ecf-244">jQuery 버전 1.7</span><span class="sxs-lookup"><span data-stu-id="19ecf-244">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="19ecf-245">jQuery 버전 1.6.4</span><span class="sxs-lookup"><span data-stu-id="19ecf-245">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="19ecf-246">jQuery 버전 1.6.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-246">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="19ecf-247">jQuery 버전 1.6.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-247">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="19ecf-248">jQuery 버전 1.6.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-248">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="19ecf-249">jQuery 버전 1.6</span><span class="sxs-lookup"><span data-stu-id="19ecf-249">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="19ecf-250">jQuery 버전 1.5.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-250">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="19ecf-251">jQuery 버전 1.5.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-251">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="19ecf-252">jQuery 버전 1.5</span><span class="sxs-lookup"><span data-stu-id="19ecf-252">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="19ecf-253">jQuery 버전 1.4.4</span><span class="sxs-lookup"><span data-stu-id="19ecf-253">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="19ecf-254">jQuery 버전 1.4.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-254">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="19ecf-255">jQuery 버전 1.4.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-255">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="19ecf-256">jQuery 버전 1.4.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-256">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="19ecf-257">jQuery 버전 1.4</span><span class="sxs-lookup"><span data-stu-id="19ecf-257">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="19ecf-258">jQuery 버전 1.3.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-258">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="19ecf-259">CDN에서 jQuery 마이그레이션 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-259">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="19ecf-260">다음과 같은 jQuery 마이그레이션 릴리스가 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-260">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="19ecf-261">jQuery 마이그레이션 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-261">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="19ecf-262">jQuery 마이그레이션 버전 1.2.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-262">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="19ecf-263">jQuery 마이그레이션 버전 1.2.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-263">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="19ecf-264">jQuery 마이그레이션 버전 1.1.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-264">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="19ecf-265">jQuery 마이그레이션 버전 1.1.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-265">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="19ecf-266">jQuery 버전 1.0.0 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="19ecf-266">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="19ecf-267">CDN의 jQuery UI 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-267">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="19ecf-268">다음 버전의 jQuery UI 라이브러리는이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-268">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="19ecf-269">각 링크를 클릭 하 여 파일의 실제 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-269">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="19ecf-270">jQuery UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-270">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN의 jQuery UI 1.12.1")
- [<span data-ttu-id="19ecf-271">jQuery UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-271">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN의 jQuery UI 1.12.0")
- [<span data-ttu-id="19ecf-272">jQuery UI 1.11.4 이상을</span><span class="sxs-lookup"><span data-stu-id="19ecf-272">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN의 jQuery UI 1.11.4")
- [<span data-ttu-id="19ecf-273">jQuery UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-273">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN의 jQuery UI 1.11.3")
- [<span data-ttu-id="19ecf-274">jQuery UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-274">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN의 jQuery UI 1.11.2")
- [<span data-ttu-id="19ecf-275">jQuery UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-275">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN의 jQuery UI 1.11.1")
- [<span data-ttu-id="19ecf-276">jQuery UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-276">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN의 jQuery UI 1.11.0")
- [<span data-ttu-id="19ecf-277">jQuery UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="19ecf-277">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN의 jQuery UI 1.10.4")
- [<span data-ttu-id="19ecf-278">jQuery UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-278">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN의 jQuery UI 1.10.3")
- [<span data-ttu-id="19ecf-279">jQuery UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-279">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN의 jQuery UI 1.10.2")
- [<span data-ttu-id="19ecf-280">jQuery UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-280">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN의 jQuery UI 1.10.1")
- [<span data-ttu-id="19ecf-281">jQuery UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-281">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN의 jQuery UI 1.10.0")
- [<span data-ttu-id="19ecf-282">jQuery UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-282">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN의 jQuery UI 1.9.2")
- [<span data-ttu-id="19ecf-283">jQuery UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-283">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN의 jQuery UI 1.9.1")
- [<span data-ttu-id="19ecf-284">jQuery UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-284">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN의 jQuery UI 1.9.0")
- [<span data-ttu-id="19ecf-285">jQuery UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="19ecf-285">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN의 jQuery UI 1.8.24")
- [<span data-ttu-id="19ecf-286">jQuery UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="19ecf-286">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN의 jQuery UI 1.8.23")
- [<span data-ttu-id="19ecf-287">jQuery UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="19ecf-287">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN의 jQuery UI 1.8.22")
- [<span data-ttu-id="19ecf-288">jQuery UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="19ecf-288">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN의 jQuery UI 1.8.21")
- [<span data-ttu-id="19ecf-289">jQuery UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="19ecf-289">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN의 jQuery UI 1.8.20")
- [<span data-ttu-id="19ecf-290">jQuery UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="19ecf-290">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN의 jQuery UI 1.8.19")
- [<span data-ttu-id="19ecf-291">jQuery UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="19ecf-291">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN의 jQuery UI 1.8.18")
- [<span data-ttu-id="19ecf-292">jQuery UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="19ecf-292">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN의 jQuery UI 1.8.17")
- [<span data-ttu-id="19ecf-293">jQuery UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="19ecf-293">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN의 jQuery UI 1.8.16")
- [<span data-ttu-id="19ecf-294">jQuery UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="19ecf-294">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN의 jQuery UI 1.8.15")
- [<span data-ttu-id="19ecf-295">jQuery UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="19ecf-295">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN의 jQuery UI 1.8.14")
- [<span data-ttu-id="19ecf-296">jQuery UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="19ecf-296">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN의 jQuery UI 1.8.13")
- [<span data-ttu-id="19ecf-297">jQuery UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="19ecf-297">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN의 jQuery UI 1.8.12")
- [<span data-ttu-id="19ecf-298">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="19ecf-298">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN의 jQuery UI 1.8.11")
- [<span data-ttu-id="19ecf-299">jQuery UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="19ecf-299">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN의 jQuery UI 1.8.10")
- [<span data-ttu-id="19ecf-300">jQuery UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="19ecf-300">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN의 jQuery UI 1.8.9")
- [<span data-ttu-id="19ecf-301">jQuery UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="19ecf-301">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN의 jQuery UI 1.8.8")
- [<span data-ttu-id="19ecf-302">jQuery UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="19ecf-302">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN의 jQuery UI 1.8.7")
- [<span data-ttu-id="19ecf-303">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="19ecf-303">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN의 jQuery UI 1.8.6")
- [<span data-ttu-id="19ecf-304">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="19ecf-304">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="19ecf-305">CDN의 jQuery 유효성 검사 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-305">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="19ecf-306">[JQuery 유효성 검사](https://jqueryvalidation.org/ "jQuery 유효성 검사 플러그 인") 플러그 인의 다음 릴리스는이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-306">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="19ecf-307">각 링크를 클릭 하 여 파일의 실제 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-307">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="19ecf-308">jQuery Validate 1.19.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-308">jQuery Validate 1.19.2</span></span>](jquery-validate/cdnjqueryvalidate1192.md "jQuery 유효성 검사 1.19.2")
- [<span data-ttu-id="19ecf-309">jQuery Validate 1.19.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-309">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "jQuery 유효성 검사 1.19.1")
- [<span data-ttu-id="19ecf-310">jQuery Validate 1.19.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-310">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery 유효성 검사 1.19.0")
- [<span data-ttu-id="19ecf-311">jQuery Validate 1.17.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-311">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery 유효성 검사 1.17.0")
- [<span data-ttu-id="19ecf-312">jQuery Validate 1.16.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-312">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Validation 1.16.0")
- [<span data-ttu-id="19ecf-313">jQuery Validate 1.15.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-313">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Validation 1.15.1")
- [<span data-ttu-id="19ecf-314">jQuery Validate 1.15.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-314">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Validation 1.15.0")
- [<span data-ttu-id="19ecf-315">jQuery Validate 1.14.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-315">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Validation 1.14.0")
- [<span data-ttu-id="19ecf-316">jQuery Validate 1.13.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-316">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Validation 1.13.1")
- [<span data-ttu-id="19ecf-317">jQuery Validate 1.13.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-317">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Validation 1.13.0")
- [<span data-ttu-id="19ecf-318">jQuery Validate 1.12.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-318">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Validation 1.12.0")
- [<span data-ttu-id="19ecf-319">jQuery Validate 1.11.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-319">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Validation 1.11.1")
- [<span data-ttu-id="19ecf-320">jQuery Validate 1.11.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-320">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Validation 1.11.0")
- [<span data-ttu-id="19ecf-321">jQuery Validate 1.10.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-321">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Validation 1.10.0")
- [<span data-ttu-id="19ecf-322">jQuery 유효성 검사 1.9</span><span class="sxs-lookup"><span data-stu-id="19ecf-322">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 버전 1.9")
- [<span data-ttu-id="19ecf-323">jQuery Validate 1.8.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-323">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate 버전 1.8.1")
- [<span data-ttu-id="19ecf-324">jQuery 유효성 검사 1.8</span><span class="sxs-lookup"><span data-stu-id="19ecf-324">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 버전 1.8")
- [<span data-ttu-id="19ecf-325">jQuery 유효성 검사 1.7</span><span class="sxs-lookup"><span data-stu-id="19ecf-325">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 버전 1.7")
- [<span data-ttu-id="19ecf-326">jQuery Validate 1.6</span><span class="sxs-lookup"><span data-stu-id="19ecf-326">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Validate 1.6")
- [<span data-ttu-id="19ecf-327">jQuery Validate 1.5.5</span><span class="sxs-lookup"><span data-stu-id="19ecf-327">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Validate 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="19ecf-328">CDN의 jQuery Mobile 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-328">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="19ecf-329">JQuery Mobile library의 다음 릴리스는이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-329">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="19ecf-330">각 링크를 클릭 하 여 파일의 실제 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-330">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="19ecf-331">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="19ecf-331">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.5")
- [<span data-ttu-id="19ecf-332">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-332">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.2")
- [<span data-ttu-id="19ecf-333">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-333">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.1")
- [<span data-ttu-id="19ecf-334">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-334">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.0")
- [<span data-ttu-id="19ecf-335">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-335">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.2")
- [<span data-ttu-id="19ecf-336">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-336">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.1")
- [<span data-ttu-id="19ecf-337">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-337">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.0")
- [<span data-ttu-id="19ecf-338">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-338">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN의 jQuery Mobile 1.2.0")
- [<span data-ttu-id="19ecf-339">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-339">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.2")
- [<span data-ttu-id="19ecf-340">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-340">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.1")
- [<span data-ttu-id="19ecf-341">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-341">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.0")
- [<span data-ttu-id="19ecf-342">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="19ecf-342">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.0 RC2")
- [<span data-ttu-id="19ecf-343">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-343">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN의 jQuery Mobile 1.0.1")
- [<span data-ttu-id="19ecf-344">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-344">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN의 jQuery Mobile 1.0")
- [<span data-ttu-id="19ecf-345">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="19ecf-345">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="19ecf-346">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="19ecf-346">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="19ecf-347">jQuery Mobile 1.0 베타 3</span><span class="sxs-lookup"><span data-stu-id="19ecf-347">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 베타 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="19ecf-348">CDN에서 jQuery 템플릿 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-348">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="19ecf-349">다음 릴리스의 jQuery 템플릿 플러그 인이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-349">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="19ecf-350">각 링크를 클릭 하 여 파일의 실제 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-350">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="19ecf-351">jQuery 템플릿 베타 1</span><span class="sxs-lookup"><span data-stu-id="19ecf-351">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 템플릿 베타 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="19ecf-352">CDN의 jQuery 주기 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-352">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="19ecf-353">다음 릴리스의 jQuery Cycle 플러그 인이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-353">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="19ecf-354">각 링크를 클릭 하 여 파일의 실제 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-354">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="19ecf-355">jQuery 주기 2.99</span><span class="sxs-lookup"><span data-stu-id="19ecf-355">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="19ecf-356">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="19ecf-356">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="19ecf-357">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="19ecf-357">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="19ecf-358">CDN의 jQuery Datatable 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-358">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="19ecf-359">다음 릴리스의 jQuery Datatable 플러그 인이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-359">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="19ecf-360">각 링크를 클릭 하 여 파일의 실제 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-360">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="19ecf-361">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="19ecf-361">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="19ecf-362">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="19ecf-362">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="19ecf-363">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="19ecf-363">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="19ecf-364">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-364">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="19ecf-365">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-365">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="19ecf-366">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-366">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="19ecf-367">jQuery Datatable 1.9.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-367">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="19ecf-368">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-368">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="19ecf-369">CDN의 Modernizr 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-369">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="19ecf-370">CDN에서 호스트 되는 [Modernizr](http://www.modernizr.com "Modernizr") 의 릴리스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-370">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="19ecf-371">CDN의 JSHint 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-371">JSHint Releases on the CDN</span></span>

<span data-ttu-id="19ecf-372">다음 버전의 [Jshint](http://www.jshint.com "JSHint") 는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-372">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="19ecf-373">CDN의 릴리스 녹아웃</span><span class="sxs-lookup"><span data-stu-id="19ecf-373">Knockout Releases on the CDN</span></span>

<span data-ttu-id="19ecf-374">다음 [녹아웃](http://www.knockoutjs.com "Knockout") 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-374">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="19ecf-375">CDN의 세계화 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-375">Globalize Releases on the CDN</span></span>

<span data-ttu-id="19ecf-376">다음 [전역화](https://github.com/jquery/globalize "세계화") 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-376">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="19ecf-377">세계화 버전 1.0.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-377">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="19ecf-378">세계화 버전 0.1.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-378">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="19ecf-379">모든 문화권</span><span class="sxs-lookup"><span data-stu-id="19ecf-379">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="19ecf-380">"{Culture-코드}"를 원하는 문화권 코드로 바꿉니다. 예를 들어 CDN의 Microsoft 파일 = =이 라이브러리는 Microsoft에서 업로드 했습니다 globalize.culture.en-GB.js.</span><span class="sxs-lookup"><span data-stu-id="19ecf-380">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="19ecf-381">CDN에 대 한 응답 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-381">Respond Releases on the CDN</span></span>

<span data-ttu-id="19ecf-382">다음의 [응답](https://github.com/scottjehl/Respond "대응") 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-382">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="19ecf-383">응답 버전 1.4.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-383">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="19ecf-384">응답 버전 1.4.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-384">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="19ecf-385">응답 버전 1.4.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-385">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="19ecf-386">응답 버전 1.3.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-386">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="19ecf-387">응답 버전 1.2.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-387">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="19ecf-388">CDN의 부트스트랩 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-388">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="19ecf-389">CDN에서 호스트 되는 [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") 부트스트랩의 릴리스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-389">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-450"></a><span data-ttu-id="19ecf-390">부트스트랩 버전 4.5.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-390">Bootstrap version 4.5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.5.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-441"></a><span data-ttu-id="19ecf-391">부트스트랩 버전 4.4.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-391">Bootstrap version 4.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.4.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-431"></a><span data-ttu-id="19ecf-392">부트스트랩 버전 4.3.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-392">Bootstrap version 4.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.3.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-421"></a><span data-ttu-id="19ecf-393">부트스트랩 버전 4.2.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-393">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="19ecf-394">부트스트랩 버전 4.1.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-394">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="19ecf-395">부트스트랩 버전 4.0.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-395">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-341"></a><span data-ttu-id="19ecf-396">부트스트랩 버전 3.4.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-396">Bootstrap version 3.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.1/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-340"></a><span data-ttu-id="19ecf-397">부트스트랩 버전 3.4.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-397">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="19ecf-398">부트스트랩 버전 3.3.7</span><span class="sxs-lookup"><span data-stu-id="19ecf-398">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="19ecf-399">부트스트랩 버전 3.3.6</span><span class="sxs-lookup"><span data-stu-id="19ecf-399">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="19ecf-400">부트스트랩 버전 3.3.5</span><span class="sxs-lookup"><span data-stu-id="19ecf-400">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="19ecf-401">부트스트랩 버전 3.3.4</span><span class="sxs-lookup"><span data-stu-id="19ecf-401">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="19ecf-402">부트스트랩 버전 3.3.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-402">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="19ecf-403">부트스트랩 버전 3.3.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-403">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="19ecf-404">부트스트랩 버전 3.3.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-404">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="19ecf-405">부트스트랩 버전 3.2.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-405">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="19ecf-406">부트스트랩 버전 3.1.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-406">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="19ecf-407">부트스트랩 버전 3.1.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-407">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="19ecf-408">부트스트랩 버전 3.0.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-408">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="19ecf-409">부트스트랩 버전 3.0.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-409">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="19ecf-410">부트스트랩 버전 3.0.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-410">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="19ecf-411">부트스트랩 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-411">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="19ecf-412">부트스트랩 버전 2.3.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-412">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="19ecf-413">부트스트랩 버전 2.3.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-413">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="19ecf-414">CDN의 부트스트랩 TouchCarousel 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-414">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="19ecf-415">부트스트랩 TouchCarousel 릴리스의 다음 릴리스는 [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-415">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="19ecf-416">부트스트랩 TouchCarousel version 0.8.0부터</span><span class="sxs-lookup"><span data-stu-id="19ecf-416">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="19ecf-417">CDN의 Hammer.js 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-417">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="19ecf-418">[http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/")CDN에서 호스트 되는 Hammer.js 릴리스의 릴리스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-418">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="19ecf-419">Hammer.js 버전 2.0.4 이상을</span><span class="sxs-lookup"><span data-stu-id="19ecf-419">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="19ecf-420">ASP.NET Web Forms 및 CDN의 Ajax 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-420">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="19ecf-421">ASP.NET Ajax 라이브러리의 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-421">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="19ecf-422">각 링크를 클릭 하 여 파일의 실제 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-422">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="19ecf-423">ASP.NET Web Forms 및 Ajax 버전 4.5.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-423">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web Forms 및 Ajax 4.5.2")
- [<span data-ttu-id="19ecf-424">ASP.NET Web Forms 및 Ajax 버전 4</span><span class="sxs-lookup"><span data-stu-id="19ecf-424">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms and Ajax 4")
- [<span data-ttu-id="19ecf-425">ASP.NET Ajax 버전 3.5</span><span class="sxs-lookup"><span data-stu-id="19ecf-425">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="19ecf-426">CDN의 ASP.NET MVC 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-426">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="19ecf-427">다음 ASP.NET MVC JavaScript 파일은이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-427">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="19ecf-428">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-428">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="19ecf-429">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-429">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="19ecf-430">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-430">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="19ecf-431">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-431">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="19ecf-432">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-432">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="19ecf-433">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-433">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="19ecf-434">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-434">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="19ecf-435">CDN의 ASP.NET SignalR 릴리스</span><span class="sxs-lookup"><span data-stu-id="19ecf-435">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="19ecf-436">다음 ASP.NET SignalR JavaScript 파일은이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="19ecf-436">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="19ecf-437">ASP.NET SignalR 2.2.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-437">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="19ecf-438">ASP.NET SignalR 2.2.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-438">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="19ecf-439">ASP.NET SignalR 2.2.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-439">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="19ecf-440">ASP.NET SignalR 2.1.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-440">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="19ecf-441">ASP.NET SignalR 2.0.3 라이브러리가</span><span class="sxs-lookup"><span data-stu-id="19ecf-441">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="19ecf-442">ASP.NET SignalR 2.0.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-442">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="19ecf-443">ASP.NET SignalR 2.0.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-443">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="19ecf-444">ASP.NET SignalR 2.0.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-444">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="19ecf-445">ASP.NET SignalR 1.1.3</span><span class="sxs-lookup"><span data-stu-id="19ecf-445">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="19ecf-446">ASP.NET SignalR 1.1.2</span><span class="sxs-lookup"><span data-stu-id="19ecf-446">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="19ecf-447">ASP.NET SignalR 1.1.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-447">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="19ecf-448">ASP.NET SignalR 1.1.0</span><span class="sxs-lookup"><span data-stu-id="19ecf-448">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="19ecf-449">ASP.NET SignalR 1.0.1</span><span class="sxs-lookup"><span data-stu-id="19ecf-449">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="19ecf-450">CDN 사용 약관에 대 한 자세한 내용은 [Microsoft AJAX Cdn 사용 약관](https://www.asp.net/terms-of-use "Microsoft Ajax CDN 사용 약관")을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="19ecf-450">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
