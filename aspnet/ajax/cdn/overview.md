---
uid: ajax/cdn/overview
title: 마이크로소프트 아약스 콘텐츠 전송 네트워크 | 마이크로 소프트 문서
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 8e7efa2f321976671be321c760e2b478fe6e9e99
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540209"
---
# <a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="48b35-102">Microsoft Ajax Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="48b35-102">Microsoft Ajax Content Delivery Network</span></span>

> [!WARNING]
> <span data-ttu-id="48b35-103">프로덕션 응용 프로그램은 CDN 자산에 대한 하드 의존성을 가져서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="48b35-104">응용 프로그램은 참조된 CDN 자산을 테스트하고 CDN을 사용할 수 없는 경우 대체 자산을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span>
>
> <span data-ttu-id="48b35-105">Microsoft Ajax CDN에는 Azure CDN을 사용하는 것 이상의 SLA가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="48b35-106">[이 GitHub 문제를](https://github.com/dotnet/AspNetDocs/issues/116) 사용하여 Microsoft Ajax CDN의 문제를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-106">Use [this GitHub issue](https://github.com/dotnet/AspNetDocs/issues/116) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="48b35-107">목차</span><span class="sxs-lookup"><span data-stu-id="48b35-107">Table of Contents</span></span>

<span data-ttu-id="48b35-108">**[ajax.microsoft.com 이름이 ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="48b35-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="48b35-109">**[비주얼 스튜디오 .vsdoc 지원](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="48b35-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="48b35-110">**[CDN에서 ASP.NET 아약스 사용](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="48b35-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="48b35-111">**[CDN에서 jQuery 사용](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="48b35-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="48b35-112">**[CDN에서 jQuery UI 사용](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="48b35-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="48b35-113">**[CDN의 타사 파일](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="48b35-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="48b35-114">cdN에서 jQuery 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="48b35-115">cdN에서 릴리스를 마이그레이션하는 jQuery</span><span class="sxs-lookup"><span data-stu-id="48b35-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="48b35-116">cdN에서 ui 를 릴리스하는 jQuery</span><span class="sxs-lookup"><span data-stu-id="48b35-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="48b35-117">cdN에서 j쿼리 유효성 검사 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="48b35-118">cdN에서 모바일 릴리스를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="48b35-119">cdN에서 j쿼리 템플릿 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="48b35-120">CDN에서 jQuery 주기 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="48b35-121">cdN에서 데이터 테이블 릴리스를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="48b35-122">모더니저, CDN에서 출시</span><span class="sxs-lookup"><span data-stu-id="48b35-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="48b35-123">JSHint, CDN에서 출시</span><span class="sxs-lookup"><span data-stu-id="48b35-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="48b35-124">CDN에서 녹아웃 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="48b35-125">CDN에서 릴리스 세계화</span><span class="sxs-lookup"><span data-stu-id="48b35-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="48b35-126">CDN에서 릴리스 응답</span><span class="sxs-lookup"><span data-stu-id="48b35-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="48b35-127">CDN에서 부트스트랩 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="48b35-128">부트스트랩 터치카로젤이 CDN에서 출시됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="48b35-129">CDN에서 해머.js 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="48b35-130">CDN에서 웹 양식 및 아약스 릴리스에 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="48b35-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="48b35-131">ASP.NET MVC 는 CDN에서 출시됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="48b35-132">CDN에서 ASP.NET 시그널R 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="48b35-133">Microsoft Ajax 콘텐츠 전송 네트워크(CDN)는 jQuery와 같은 인기 있는 타사 자바스크립트 라이브러리를 호스팅하며 웹 응용 프로그램에 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="48b35-134">예를 들어 이 CDN에서 호스팅되는 jQuery를 사용하여 페이지에 &lt;&gt; ajax.aspnetcdn.com 가리키는 스크립트 태그를 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="48b35-135">CDN을 활용하면 Ajax 응용 프로그램의 성능을 크게 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="48b35-136">CDN의 내용은 전 세계에 있는 서버에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="48b35-137">또한 CDN을 사용하면 브라우저가 다른 도메인에 있는 웹 사이트에 캐시된 타사 JavaScript 파일을 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="48b35-138">CDN은 보안 소켓 계층을 사용하여 웹 페이지를 제공해야 하는 경우 SSL(HTTPS)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="48b35-139">CDN은 해당 라이브러리의 소유자가 업로드하고 라이선스가 부여된 다음과 같은 타사 스크립트 라이브러리를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="48b35-140">j쿼리 (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="48b35-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="48b35-141">j쿼리 UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="48b35-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="48b35-142">jQuery 모바일 (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="48b35-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="48b35-143">j쿼리 유효성 검사 (https://jqueryvalidation.org/)</span><span class="sxs-lookup"><span data-stu-id="48b35-143">jQuery Validation (https://jqueryvalidation.org/)</span></span>
- <span data-ttu-id="48b35-144">j쿼리 주기(www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="48b35-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="48b35-145">j쿼리 데이터 테이블 (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="48b35-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="48b35-146">마이크로 소프트 아약스 CDN은 또한 마이크로 소프트에 의해 업로드 된 다음과 같은 라이브러리를 포함한다 :</span><span class="sxs-lookup"><span data-stu-id="48b35-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="48b35-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="48b35-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="48b35-148">ASP.NET MVC 자바 스크립트 파일</span><span class="sxs-lookup"><span data-stu-id="48b35-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="48b35-149">ASP.NET 시그널러 자바 스크립트 파일</span><span class="sxs-lookup"><span data-stu-id="48b35-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="48b35-150">Microsoft는 이 CDN에서 호스팅되는 타사 라이브러리의 소유권을 주장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="48b35-151">라이브러리의 저작권 소유자는 이러한 라이브러리에 라이선스를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="48b35-152">이러한 라이브러리를 다운로드하고 사용해야 할 모든 권리는 각 저작권 소유자에 의해서만 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="48b35-153">Microsoft는 Microsoft 라이브러리가 아니기 때문에 이 CDN에서 호스팅되는 타사 라이브러리에 대한 보증 또는 지적 재산권 라이선스(내재된 특허 권 없음 포함)를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="48b35-154">자바 스크립트 라이브러리를 제출하고자하고 라이브러리는 상위 자바 스크립트 라이브러리 중 http://trends.builtwith.com) 하나입니다 (에 나열된 또는 (a) 인기있는 이러한 라이브러리에 확장 / 플러그인; 또는 AjaxCDNSubmission@Microsoft.com(b) ASP.NET 사용하기에 도움이 다음 문의하시기 바랍니다 .</span><span class="sxs-lookup"><span data-stu-id="48b35-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="48b35-155">ajax.microsoft.com 이름이 ajax.aspnetcdn.com</span><span class="sxs-lookup"><span data-stu-id="48b35-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="48b35-156">cdN은 microsoft.com 도메인 이름을 사용하는 데 사용되었으며 aspnetcdn.com 도메인 이름을 사용하도록 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="48b35-157">브라우저가 microsoft.com 도메인을 참조할 때 각 요청과 함께 해당 도메인의 쿠키를 전송하기 때문에 이러한 변경은 성능을 높이기 위해 이루어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="48b35-158">microsoft.com 이외의 도메인 이름으로 이름을 변경하면 성능을 최대 25%까지 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="48b35-159">ajax.microsoft.com 계속 작동하지만 ajax.aspnetcdn.com 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="48b35-160">이전 형식:https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="48b35-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="48b35-161">새로운 형식:https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="48b35-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="48b35-162">비주얼 스튜디오 .vsdoc 지원</span><span class="sxs-lookup"><span data-stu-id="48b35-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="48b35-163">Visual Studio 2008에서 .vsdoc 파일을 올바르게 사용하려면 VS 2008 SP1이 설치되어 있는지 확인하고 vsdoc 파일에 대한 핫픽스가 설치되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="48b35-164">여기에서 다음을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-164">You can get these from here:</span></span>

- [<span data-ttu-id="48b35-165">비주얼 스튜디오 2008 SP1 다운로드</span><span class="sxs-lookup"><span data-stu-id="48b35-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "비주얼 스튜디오 2008 SP1 다운로드")
- [<span data-ttu-id="48b35-166">비주얼 스튜디오 2008 SP1에 대한 .vsdoc 핫픽스 다운로드</span><span class="sxs-lookup"><span data-stu-id="48b35-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "비주얼 스튜디오 2008 SP1에 대한 .vsdoc 핫픽스 다운로드")

<span data-ttu-id="48b35-167">Visual Studio 2010은 추가 패치 없이 .vsdoc 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="48b35-168">CDN에서 ASP.NET 아약스 사용</span><span class="sxs-lookup"><span data-stu-id="48b35-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="48b35-169">ASP.NET 4를 사용하는 경우 ASP.NET 프레임워크 스크립트에 대한 모든 요청을 CDN으로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="48b35-170">로컬 웹 서버 대신 CDN에서 스크립트를 검색하면 공용 ASP.NET 웹 사이트의 성능이 크게 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="48b35-171">스크립트 관리자 EnableCDN 속성을 사용하여 모든 ASP.NET 프레임워크 스크립트 요청을 Microsoft Ajax CDN으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="48b35-172">CDN에서 jQuery 사용</span><span class="sxs-lookup"><span data-stu-id="48b35-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="48b35-173">다음 스크립트 요소를 페이지에 추가하여 웹 응용 프로그램에서 CDN에서 호스팅되는 jQuery 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="48b35-174">CDN에는 다음 요소를 사용할 수 있는 jQuery 스크립트의 축소된 버전도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="48b35-175">CDN을 사용할 수 없는 경우 페이지가 자신의 웹 사이트의 로컬 경로에서 jQuery로 대체되도록 하려면 CDN을 참조하는 요소 바로 다음에 다음 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="48b35-176">다음 샘플 페이지에서는 jQuery 라이브러리의 CDN 버전을 사용하여 단추를 클릭할 때 div 요소의 내용을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="48b35-177">jQuery에 대해 자세히 알아보고 [jQuery](http://jquery.com/) 웹 사이트를 방문하여 jQuery의 로컬 복사본을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="48b35-178">CDN에서 jQuery UI 사용</span><span class="sxs-lookup"><span data-stu-id="48b35-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="48b35-179">또한 CDN은 jQuery UI 라이브러리를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="48b35-180">jQuery UI 라이브러리에는 ASP.NET 응용 프로그램에서 사용할 수 있는 다양한 위젯 및 효과 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="48b35-181">예를 들어 다음 페이지에서는 ASP.NET Web Forms 응용 프로그램의 컨텍스트에서 jQuery UI Datepicker를 사용하여 팝업 일정을 표시하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="48b35-182">키보드를 사용하여 TextBox로 포커스를 이동하면 캘린더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![날짜 선택기로 만든 팝업 달력](overview/_static/image1.png)

<span data-ttu-id="48b35-184">위의 코드에 CDN의 파일 세 파일을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="48b35-185">jQuery 라이브러리 &mdash; jQuery UI 라이브러리는 jQuery 라이브러리에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="48b35-186">jQuery UI 라이브러리를 추가하기 전에 페이지에 jQuery 라이브러리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="48b35-187">jQuery UI &mdash; 라이브러리 jQuery UI 라이브러리에는 위의 페이지에 사용된 Datepicker 위젯과 같은 모든 jQuery UI 효과 및 위젯이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="48b35-188">jQuery UI 테마 &mdash; jQuery UI는 서로 다른 테마를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="48b35-189">위의 페이지에는 Redmond 테마를 가져오는 CSS 파일에 대한 링크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="48b35-190">모든 표준 jQuery UI 테마는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="48b35-191">[각](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN의 jQuery UI 1.8.10") 테마에 대한 미리보기 이미지를 보려면 이 페이지를 방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="48b35-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="48b35-192">jQuery UI 라이브러리에 대한 자세한 내용은 공식 [jQuery UI 웹 사이트를](http://jQueryUI.com "jQuery UI 웹 사이트")방문하십시오.</span><span class="sxs-lookup"><span data-stu-id="48b35-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="48b35-193">CDN의 타사 파일</span><span class="sxs-lookup"><span data-stu-id="48b35-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="48b35-194">CDN은 가장 인기 있는 타사 자바스크립트 라이브러리를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="48b35-195">Microsoft는 이 CDN에서 호스팅되는 타사 라이브러리의 소유권을 주장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="48b35-196">라이브러리의 저작권 소유자는 이러한 라이브러리에 라이선스를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="48b35-197">이러한 라이브러리를 다운로드하고 사용해야 할 모든 권리는 각 저작권 소유자에 의해서만 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="48b35-198">Microsoft는 Microsoft 라이브러리가 아니기 때문에 이 CDN에서 호스팅되는 타사 라이브러리에 대한 보증 또는 지적 재산권 라이선스(내재된 특허 권 없음 포함)를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="48b35-199">cdN에서 jQuery 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="48b35-200">jQuery의 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-350"></a><span data-ttu-id="48b35-201">j쿼리 버전 3.5.0</span><span class="sxs-lookup"><span data-stu-id="48b35-201">jQuery version 3.5.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.5.0.slim.min.map

#### <a name="jquery-version-341"></a><span data-ttu-id="48b35-202">j쿼리 버전 3.4.1</span><span class="sxs-lookup"><span data-stu-id="48b35-202">jQuery version 3.4.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.slim.min.map

#### <a name="jquery-version-340"></a><span data-ttu-id="48b35-203">j쿼리 버전 3.4.0</span><span class="sxs-lookup"><span data-stu-id="48b35-203">jQuery version 3.4.0</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.0.slim.min.map

#### <a name="jquery-version-331"></a><span data-ttu-id="48b35-204">j쿼리 버전 3.3.1</span><span class="sxs-lookup"><span data-stu-id="48b35-204">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="48b35-205">j쿼리 버전 3.2.1</span><span class="sxs-lookup"><span data-stu-id="48b35-205">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="48b35-206">j쿼리 버전 3.2.0</span><span class="sxs-lookup"><span data-stu-id="48b35-206">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="48b35-207">j쿼리 버전 3.1.1</span><span class="sxs-lookup"><span data-stu-id="48b35-207">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="48b35-208">j쿼리 버전 3.1.0</span><span class="sxs-lookup"><span data-stu-id="48b35-208">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="48b35-209">j쿼리 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="48b35-209">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="48b35-210">j쿼리 버전 2.2.4</span><span class="sxs-lookup"><span data-stu-id="48b35-210">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="48b35-211">j쿼리 버전 2.2.3</span><span class="sxs-lookup"><span data-stu-id="48b35-211">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="48b35-212">j쿼리 버전 2.2.2</span><span class="sxs-lookup"><span data-stu-id="48b35-212">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="48b35-213">j쿼리 버전 2.2.1</span><span class="sxs-lookup"><span data-stu-id="48b35-213">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="48b35-214">j쿼리 버전 2.2.0</span><span class="sxs-lookup"><span data-stu-id="48b35-214">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="48b35-215">j쿼리 버전 2.1.4</span><span class="sxs-lookup"><span data-stu-id="48b35-215">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="48b35-216">j쿼리 버전 2.1.3</span><span class="sxs-lookup"><span data-stu-id="48b35-216">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="48b35-217">j쿼리 버전 2.1.2</span><span class="sxs-lookup"><span data-stu-id="48b35-217">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="48b35-218">j쿼리 버전 2.1.1</span><span class="sxs-lookup"><span data-stu-id="48b35-218">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="48b35-219">j쿼리 버전 2.1.0</span><span class="sxs-lookup"><span data-stu-id="48b35-219">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="48b35-220">j쿼리 버전 2.0.3</span><span class="sxs-lookup"><span data-stu-id="48b35-220">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="48b35-221">j쿼리 버전 2.0.2</span><span class="sxs-lookup"><span data-stu-id="48b35-221">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="48b35-222">j쿼리 버전 2.0.1</span><span class="sxs-lookup"><span data-stu-id="48b35-222">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="48b35-223">jQuery 버전 2.0.0</span><span class="sxs-lookup"><span data-stu-id="48b35-223">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="48b35-224">j쿼리 버전 1.12.4</span><span class="sxs-lookup"><span data-stu-id="48b35-224">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="48b35-225">j쿼리 버전 1.12.3</span><span class="sxs-lookup"><span data-stu-id="48b35-225">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="48b35-226">j쿼리 버전 1.12.2</span><span class="sxs-lookup"><span data-stu-id="48b35-226">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="48b35-227">j쿼리 버전 1.12.1</span><span class="sxs-lookup"><span data-stu-id="48b35-227">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="48b35-228">j쿼리 버전 1.12.0</span><span class="sxs-lookup"><span data-stu-id="48b35-228">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="48b35-229">j쿼리 버전 1.11.3</span><span class="sxs-lookup"><span data-stu-id="48b35-229">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="48b35-230">j쿼리 버전 1.11.2</span><span class="sxs-lookup"><span data-stu-id="48b35-230">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="48b35-231">j쿼리 버전 1.11.1</span><span class="sxs-lookup"><span data-stu-id="48b35-231">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="48b35-232">j쿼리 버전 1.11.0</span><span class="sxs-lookup"><span data-stu-id="48b35-232">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="48b35-233">j쿼리 버전 1.10.2</span><span class="sxs-lookup"><span data-stu-id="48b35-233">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="48b35-234">j쿼리 버전 1.10.1</span><span class="sxs-lookup"><span data-stu-id="48b35-234">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="48b35-235">j쿼리 버전 1.10.0</span><span class="sxs-lookup"><span data-stu-id="48b35-235">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="48b35-236">j쿼리 버전 1.9.1</span><span class="sxs-lookup"><span data-stu-id="48b35-236">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="48b35-237">j쿼리 버전 1.9.0</span><span class="sxs-lookup"><span data-stu-id="48b35-237">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="48b35-238">j쿼리 버전 1.8.3</span><span class="sxs-lookup"><span data-stu-id="48b35-238">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="48b35-239">j쿼리 버전 1.8.2</span><span class="sxs-lookup"><span data-stu-id="48b35-239">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="48b35-240">j쿼리 버전 1.8.1</span><span class="sxs-lookup"><span data-stu-id="48b35-240">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="48b35-241">j쿼리 버전 1.8.0</span><span class="sxs-lookup"><span data-stu-id="48b35-241">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="48b35-242">j쿼리 버전 1.7.2</span><span class="sxs-lookup"><span data-stu-id="48b35-242">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="48b35-243">j쿼리 버전 1.7.1</span><span class="sxs-lookup"><span data-stu-id="48b35-243">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="48b35-244">j쿼리 버전 1.7</span><span class="sxs-lookup"><span data-stu-id="48b35-244">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="48b35-245">j쿼리 버전 1.6.4</span><span class="sxs-lookup"><span data-stu-id="48b35-245">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="48b35-246">j쿼리 버전 1.6.3</span><span class="sxs-lookup"><span data-stu-id="48b35-246">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="48b35-247">j쿼리 버전 1.6.2</span><span class="sxs-lookup"><span data-stu-id="48b35-247">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="48b35-248">j쿼리 버전 1.6.1</span><span class="sxs-lookup"><span data-stu-id="48b35-248">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="48b35-249">j쿼리 버전 1.6</span><span class="sxs-lookup"><span data-stu-id="48b35-249">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="48b35-250">j쿼리 버전 1.5.2</span><span class="sxs-lookup"><span data-stu-id="48b35-250">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="48b35-251">j쿼리 버전 1.5.1</span><span class="sxs-lookup"><span data-stu-id="48b35-251">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="48b35-252">j쿼리 버전 1.5</span><span class="sxs-lookup"><span data-stu-id="48b35-252">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="48b35-253">j쿼리 버전 1.4.4</span><span class="sxs-lookup"><span data-stu-id="48b35-253">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="48b35-254">j쿼리 버전 1.4.3</span><span class="sxs-lookup"><span data-stu-id="48b35-254">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="48b35-255">j쿼리 버전 1.4.2</span><span class="sxs-lookup"><span data-stu-id="48b35-255">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="48b35-256">j쿼리 버전 1.4.1</span><span class="sxs-lookup"><span data-stu-id="48b35-256">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="48b35-257">j쿼리 버전 1.4</span><span class="sxs-lookup"><span data-stu-id="48b35-257">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="48b35-258">j쿼리 버전 1.3.2</span><span class="sxs-lookup"><span data-stu-id="48b35-258">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="48b35-259">cdN에서 릴리스를 마이그레이션하는 jQuery</span><span class="sxs-lookup"><span data-stu-id="48b35-259">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="48b35-260">jQuery 마이그레이션의 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-260">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="48b35-261">jQuery 버전 마이그레이션 3.0.0</span><span class="sxs-lookup"><span data-stu-id="48b35-261">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="48b35-262">jQuery 마이그레이션 버전 1.2.1</span><span class="sxs-lookup"><span data-stu-id="48b35-262">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="48b35-263">jQuery 마이그레이션 버전 1.2.0</span><span class="sxs-lookup"><span data-stu-id="48b35-263">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="48b35-264">jQuery 마이그레이션 버전 1.1.1</span><span class="sxs-lookup"><span data-stu-id="48b35-264">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="48b35-265">jQuery 마이그레이션 버전 1.1.0</span><span class="sxs-lookup"><span data-stu-id="48b35-265">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="48b35-266">jQuery 마이그레이션 버전 1.0.0</span><span class="sxs-lookup"><span data-stu-id="48b35-266">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="48b35-267">cdN에서 ui 를 릴리스하는 jQuery</span><span class="sxs-lookup"><span data-stu-id="48b35-267">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="48b35-268">jQuery UI 라이브러리의 다음 릴리스는 이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-268">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="48b35-269">각 링크를 클릭하여 파일의 실제 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-269">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="48b35-270">j쿼리 UI 1.12.1</span><span class="sxs-lookup"><span data-stu-id="48b35-270">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "Microsoft Ajax CDN의 jQuery UI 1.12.1")
- [<span data-ttu-id="48b35-271">j쿼리 UI 1.12.0</span><span class="sxs-lookup"><span data-stu-id="48b35-271">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "Microsoft Ajax CDN의 jQuery UI 1.12.0")
- [<span data-ttu-id="48b35-272">j쿼리 UI 1.11.4</span><span class="sxs-lookup"><span data-stu-id="48b35-272">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "Microsoft Ajax CDN의 jQuery UI 1.11.4")
- [<span data-ttu-id="48b35-273">j쿼리 UI 1.11.3</span><span class="sxs-lookup"><span data-stu-id="48b35-273">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "Microsoft Ajax CDN의 jQuery UI 1.11.3")
- [<span data-ttu-id="48b35-274">j쿼리 UI 1.11.2</span><span class="sxs-lookup"><span data-stu-id="48b35-274">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "Microsoft Ajax CDN의 jQuery UI 1.11.2")
- [<span data-ttu-id="48b35-275">j쿼리 UI 1.11.1</span><span class="sxs-lookup"><span data-stu-id="48b35-275">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "Microsoft Ajax CDN의 jQuery UI 1.11.1")
- [<span data-ttu-id="48b35-276">j쿼리 UI 1.11.0</span><span class="sxs-lookup"><span data-stu-id="48b35-276">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "Microsoft Ajax CDN의 jQuery UI 1.11.0")
- [<span data-ttu-id="48b35-277">j쿼리 UI 1.10.4</span><span class="sxs-lookup"><span data-stu-id="48b35-277">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "Microsoft Ajax CDN의 jQuery UI 1.10.4")
- [<span data-ttu-id="48b35-278">j쿼리 UI 1.10.3</span><span class="sxs-lookup"><span data-stu-id="48b35-278">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "Microsoft Ajax CDN의 jQuery UI 1.10.3")
- [<span data-ttu-id="48b35-279">j쿼리 UI 1.10.2</span><span class="sxs-lookup"><span data-stu-id="48b35-279">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "Microsoft Ajax CDN의 jQuery UI 1.10.2")
- [<span data-ttu-id="48b35-280">j쿼리 UI 1.10.1</span><span class="sxs-lookup"><span data-stu-id="48b35-280">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "Microsoft Ajax CDN의 jQuery UI 1.10.1")
- [<span data-ttu-id="48b35-281">j쿼리 UI 1.10.0</span><span class="sxs-lookup"><span data-stu-id="48b35-281">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "Microsoft Ajax CDN의 jQuery UI 1.10.0")
- [<span data-ttu-id="48b35-282">j쿼리 UI 1.9.2</span><span class="sxs-lookup"><span data-stu-id="48b35-282">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "Microsoft Ajax CDN의 jQuery UI 1.9.2")
- [<span data-ttu-id="48b35-283">j쿼리 UI 1.9.1</span><span class="sxs-lookup"><span data-stu-id="48b35-283">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "Microsoft Ajax CDN의 jQuery UI 1.9.1")
- [<span data-ttu-id="48b35-284">j쿼리 UI 1.9.0</span><span class="sxs-lookup"><span data-stu-id="48b35-284">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "Microsoft Ajax CDN의 jQuery UI 1.9.0")
- [<span data-ttu-id="48b35-285">j쿼리 UI 1.8.24</span><span class="sxs-lookup"><span data-stu-id="48b35-285">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "Microsoft Ajax CDN의 jQuery UI 1.8.24")
- [<span data-ttu-id="48b35-286">j쿼리 UI 1.8.23</span><span class="sxs-lookup"><span data-stu-id="48b35-286">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "Microsoft Ajax CDN의 jQuery UI 1.8.23")
- [<span data-ttu-id="48b35-287">j쿼리 UI 1.8.22</span><span class="sxs-lookup"><span data-stu-id="48b35-287">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "Microsoft Ajax CDN의 jQuery UI 1.8.22")
- [<span data-ttu-id="48b35-288">j쿼리 UI 1.8.21</span><span class="sxs-lookup"><span data-stu-id="48b35-288">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "Microsoft Ajax CDN의 jQuery UI 1.8.21")
- [<span data-ttu-id="48b35-289">j쿼리 UI 1.8.20</span><span class="sxs-lookup"><span data-stu-id="48b35-289">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "Microsoft Ajax CDN의 jQuery UI 1.8.20")
- [<span data-ttu-id="48b35-290">j쿼리 UI 1.8.19</span><span class="sxs-lookup"><span data-stu-id="48b35-290">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "Microsoft Ajax CDN의 jQuery UI 1.8.19")
- [<span data-ttu-id="48b35-291">j쿼리 UI 1.8.18</span><span class="sxs-lookup"><span data-stu-id="48b35-291">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "Microsoft Ajax CDN의 jQuery UI 1.8.18")
- [<span data-ttu-id="48b35-292">j쿼리 UI 1.8.17</span><span class="sxs-lookup"><span data-stu-id="48b35-292">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "Microsoft Ajax CDN의 jQuery UI 1.8.17")
- [<span data-ttu-id="48b35-293">j쿼리 UI 1.8.16</span><span class="sxs-lookup"><span data-stu-id="48b35-293">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "Microsoft Ajax CDN의 jQuery UI 1.8.16")
- [<span data-ttu-id="48b35-294">j쿼리 UI 1.8.15</span><span class="sxs-lookup"><span data-stu-id="48b35-294">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "Microsoft Ajax CDN의 jQuery UI 1.8.15")
- [<span data-ttu-id="48b35-295">j쿼리 UI 1.8.14</span><span class="sxs-lookup"><span data-stu-id="48b35-295">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "Microsoft Ajax CDN의 jQuery UI 1.8.14")
- [<span data-ttu-id="48b35-296">j쿼리 UI 1.8.13</span><span class="sxs-lookup"><span data-stu-id="48b35-296">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "Microsoft Ajax CDN의 jQuery UI 1.8.13")
- [<span data-ttu-id="48b35-297">j쿼리 UI 1.8.12</span><span class="sxs-lookup"><span data-stu-id="48b35-297">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "Microsoft Ajax CDN의 jQuery UI 1.8.12")
- [<span data-ttu-id="48b35-298">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="48b35-298">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "Microsoft Ajax CDN의 jQuery UI 1.8.11")
- [<span data-ttu-id="48b35-299">j쿼리 UI 1.8.10</span><span class="sxs-lookup"><span data-stu-id="48b35-299">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "Microsoft Ajax CDN의 jQuery UI 1.8.10")
- [<span data-ttu-id="48b35-300">j쿼리 UI 1.8.9</span><span class="sxs-lookup"><span data-stu-id="48b35-300">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "Microsoft Ajax CDN의 jQuery UI 1.8.9")
- [<span data-ttu-id="48b35-301">j쿼리 UI 1.8.8</span><span class="sxs-lookup"><span data-stu-id="48b35-301">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "Microsoft Ajax CDN의 jQuery UI 1.8.8")
- [<span data-ttu-id="48b35-302">j쿼리 UI 1.8.7</span><span class="sxs-lookup"><span data-stu-id="48b35-302">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "Microsoft Ajax CDN의 jQuery UI 1.8.7")
- [<span data-ttu-id="48b35-303">j쿼리 UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="48b35-303">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "Microsoft Ajax CDN의 jQuery UI 1.8.6")
- [<span data-ttu-id="48b35-304">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="48b35-304">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="48b35-305">cdN에서 j쿼리 유효성 검사 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-305">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="48b35-306">[jQuery 유효성 검사](https://jqueryvalidation.org/ "j쿼리 유효성 검사 플러그인") 플러그인의 다음 릴리스는 이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-306">The following releases of the [jQuery Validation](https://jqueryvalidation.org/ "jQuery Validation Plugin") plugin are hosted on this CDN.</span></span> <span data-ttu-id="48b35-307">각 링크를 클릭하여 파일의 실제 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-307">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="48b35-308">j쿼리 유효성 검사 1.19.1</span><span class="sxs-lookup"><span data-stu-id="48b35-308">jQuery Validate 1.19.1</span></span>](jquery-validate/cdnjqueryvalidate1191.md "j쿼리 유효성 검사 1.19.1")
- [<span data-ttu-id="48b35-309">j쿼리 유효성 검사 1.19.0</span><span class="sxs-lookup"><span data-stu-id="48b35-309">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "j쿼리 유효성 검사 1.19.0")
- [<span data-ttu-id="48b35-310">j쿼리 유효성 검사 1.17.0</span><span class="sxs-lookup"><span data-stu-id="48b35-310">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "j쿼리 유효성 검사 1.17.0")
- [<span data-ttu-id="48b35-311">j쿼리 유효성 검사 1.16.0</span><span class="sxs-lookup"><span data-stu-id="48b35-311">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery Validation 1.16.0")
- [<span data-ttu-id="48b35-312">j쿼리 유효성 검사 1.15.1</span><span class="sxs-lookup"><span data-stu-id="48b35-312">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Validation 1.15.1")
- [<span data-ttu-id="48b35-313">j쿼리 유효성 검사 1.15.0</span><span class="sxs-lookup"><span data-stu-id="48b35-313">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery Validation 1.15.0")
- [<span data-ttu-id="48b35-314">j쿼리 유효성 검사 1.14.0</span><span class="sxs-lookup"><span data-stu-id="48b35-314">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Validation 1.14.0")
- [<span data-ttu-id="48b35-315">j쿼리 유효성 검사 1.13.1</span><span class="sxs-lookup"><span data-stu-id="48b35-315">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Validation 1.13.1")
- [<span data-ttu-id="48b35-316">j쿼리 유효성 검사 1.13.0</span><span class="sxs-lookup"><span data-stu-id="48b35-316">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Validation 1.13.0")
- [<span data-ttu-id="48b35-317">j쿼리 유효성 검사 1.12.0</span><span class="sxs-lookup"><span data-stu-id="48b35-317">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Validation 1.12.0")
- [<span data-ttu-id="48b35-318">j쿼리 유효성 검사 1.11.1</span><span class="sxs-lookup"><span data-stu-id="48b35-318">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Validation 1.11.1")
- [<span data-ttu-id="48b35-319">j쿼리 유효성 검사 1.11.0</span><span class="sxs-lookup"><span data-stu-id="48b35-319">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery Validation 1.11.0")
- [<span data-ttu-id="48b35-320">j쿼리 유효성 검사 1.10.0</span><span class="sxs-lookup"><span data-stu-id="48b35-320">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery Validation 1.10.0")
- [<span data-ttu-id="48b35-321">j쿼리 유효성 검사 1.9</span><span class="sxs-lookup"><span data-stu-id="48b35-321">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate 버전 1.9")
- [<span data-ttu-id="48b35-322">j쿼리 유효성 검사 1.8.1</span><span class="sxs-lookup"><span data-stu-id="48b35-322">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate 버전 1.8.1")
- [<span data-ttu-id="48b35-323">j쿼리 유효성 검사 1.8</span><span class="sxs-lookup"><span data-stu-id="48b35-323">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate 버전 1.8")
- [<span data-ttu-id="48b35-324">j쿼리 유효성 검사 1.7</span><span class="sxs-lookup"><span data-stu-id="48b35-324">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate 버전 1.7")
- [<span data-ttu-id="48b35-325">jQuery Validate 1.6</span><span class="sxs-lookup"><span data-stu-id="48b35-325">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Validate 1.6")
- [<span data-ttu-id="48b35-326">jQuery Validate 1.5.5</span><span class="sxs-lookup"><span data-stu-id="48b35-326">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Validate 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="48b35-327">cdN에서 모바일 릴리스를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-327">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="48b35-328">jQuery Mobile 라이브러리의 다음 릴리스는 이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-328">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="48b35-329">각 링크를 클릭하여 파일의 실제 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-329">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="48b35-330">jQuery 모바일 1.4.5</span><span class="sxs-lookup"><span data-stu-id="48b35-330">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.5")
- [<span data-ttu-id="48b35-331">jQuery 모바일 1.4.2</span><span class="sxs-lookup"><span data-stu-id="48b35-331">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.2")
- [<span data-ttu-id="48b35-332">jQuery 모바일 1.4.1</span><span class="sxs-lookup"><span data-stu-id="48b35-332">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.1")
- [<span data-ttu-id="48b35-333">jQuery 모바일 1.4.0</span><span class="sxs-lookup"><span data-stu-id="48b35-333">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "Microsoft Ajax CDN의 jQuery Mobile 1.4.0")
- [<span data-ttu-id="48b35-334">jQuery 모바일 1.3.2</span><span class="sxs-lookup"><span data-stu-id="48b35-334">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.2")
- [<span data-ttu-id="48b35-335">jQuery 모바일 1.3.1</span><span class="sxs-lookup"><span data-stu-id="48b35-335">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.1")
- [<span data-ttu-id="48b35-336">jQuery 모바일 1.3.0</span><span class="sxs-lookup"><span data-stu-id="48b35-336">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "Microsoft Ajax CDN의 jQuery Mobile 1.3.0")
- [<span data-ttu-id="48b35-337">jQuery 모바일 1.2.0</span><span class="sxs-lookup"><span data-stu-id="48b35-337">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "Microsoft Ajax CDN의 jQuery Mobile 1.2.0")
- [<span data-ttu-id="48b35-338">jQuery 모바일 1.1.2</span><span class="sxs-lookup"><span data-stu-id="48b35-338">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.2")
- [<span data-ttu-id="48b35-339">jQuery 모바일 1.1.1</span><span class="sxs-lookup"><span data-stu-id="48b35-339">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.1")
- [<span data-ttu-id="48b35-340">jQuery 모바일 1.1.0</span><span class="sxs-lookup"><span data-stu-id="48b35-340">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.0")
- [<span data-ttu-id="48b35-341">jQuery 모바일 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="48b35-341">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "Microsoft Ajax CDN의 jQuery Mobile 1.1.0 RC2")
- [<span data-ttu-id="48b35-342">jQuery 모바일 1.0.1</span><span class="sxs-lookup"><span data-stu-id="48b35-342">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "Microsoft Ajax CDN의 jQuery Mobile 1.0.1")
- [<span data-ttu-id="48b35-343">jQuery 모바일 1.0</span><span class="sxs-lookup"><span data-stu-id="48b35-343">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "Microsoft Ajax CDN의 jQuery Mobile 1.0")
- [<span data-ttu-id="48b35-344">jQuery 모바일 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="48b35-344">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 RC2")
- [<span data-ttu-id="48b35-345">jQuery 모바일 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="48b35-345">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 RC1")
- [<span data-ttu-id="48b35-346">jQuery 모바일 1.0 베타 3</span><span class="sxs-lookup"><span data-stu-id="48b35-346">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "Microsoft Ajax CDN의 jQuery Mobile 1.0 베타 3")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="48b35-347">cdN에서 j쿼리 템플릿 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-347">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="48b35-348">jQuery 템플릿 플러그인의 다음 릴리스는 이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-348">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="48b35-349">각 링크를 클릭하여 파일의 실제 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-349">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="48b35-350">jQuery 템플릿 베타 1</span><span class="sxs-lookup"><span data-stu-id="48b35-350">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery 템플릿 베타 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="48b35-351">CDN에서 jQuery 주기 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-351">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="48b35-352">jQuery 주기 플러그인의 다음 릴리스는이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-352">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="48b35-353">각 링크를 클릭하여 파일의 실제 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-353">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="48b35-354">j쿼리 주기 2.99</span><span class="sxs-lookup"><span data-stu-id="48b35-354">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="48b35-355">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="48b35-355">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="48b35-356">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="48b35-356">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="48b35-357">cdN에서 데이터 테이블 릴리스를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-357">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="48b35-358">jQuery DataTables 플러그인의 다음 릴리스는 이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-358">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="48b35-359">각 링크를 클릭하여 파일의 실제 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-359">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="48b35-360">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="48b35-360">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="48b35-361">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="48b35-361">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="48b35-362">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="48b35-362">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="48b35-363">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="48b35-363">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="48b35-364">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="48b35-364">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="48b35-365">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="48b35-365">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="48b35-366">j쿼리 데이터 테이블 1.9.0</span><span class="sxs-lookup"><span data-stu-id="48b35-366">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="48b35-367">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="48b35-367">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="48b35-368">모더니저, CDN에서 출시</span><span class="sxs-lookup"><span data-stu-id="48b35-368">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="48b35-369">[모더니즈르의](http://www.modernizr.com "모더니즈르") 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-369">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="48b35-370">JSHint, CDN에서 출시</span><span class="sxs-lookup"><span data-stu-id="48b35-370">JSHint Releases on the CDN</span></span>

<span data-ttu-id="48b35-371">[JSHint의](http://www.jshint.com "JSHint") 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-371">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="48b35-372">CDN에서 녹아웃 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-372">Knockout Releases on the CDN</span></span>

<span data-ttu-id="48b35-373">[녹아웃의](http://www.knockoutjs.com "녹아웃") 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-373">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

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

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="48b35-374">CDN에서 릴리스 세계화</span><span class="sxs-lookup"><span data-stu-id="48b35-374">Globalize Releases on the CDN</span></span>

<span data-ttu-id="48b35-375">[글로벌화의](https://github.com/jquery/globalize "세계화") 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-375">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="48b35-376">버전 1.0.0 세계화</span><span class="sxs-lookup"><span data-stu-id="48b35-376">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="48b35-377">버전 세계화 0.1.1</span><span class="sxs-lookup"><span data-stu-id="48b35-377">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="48b35-378">모든 문화</span><span class="sxs-lookup"><span data-stu-id="48b35-378">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="48b35-379">"{문화권 코드}"를 원하는 문화권 코드로 바꿉니다(예: globalize.culture.en-GB.js== CDN의 Microsoft 파일 ==이러한 라이브러리는 Microsoft에서 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-379">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="48b35-380">CDN에서 릴리스 응답</span><span class="sxs-lookup"><span data-stu-id="48b35-380">Respond Releases on the CDN</span></span>

<span data-ttu-id="48b35-381">[응답의](https://github.com/scottjehl/Respond "대응") 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-381">The following releases of [Respond](https://github.com/scottjehl/Respond "Respond") are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="48b35-382">응답 버전 1.4.2</span><span class="sxs-lookup"><span data-stu-id="48b35-382">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="48b35-383">응답 버전 1.4.1</span><span class="sxs-lookup"><span data-stu-id="48b35-383">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="48b35-384">응답 버전 1.4.0</span><span class="sxs-lookup"><span data-stu-id="48b35-384">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="48b35-385">응답 버전 1.3.0</span><span class="sxs-lookup"><span data-stu-id="48b35-385">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="48b35-386">응답 버전 1.2.0</span><span class="sxs-lookup"><span data-stu-id="48b35-386">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="48b35-387">CDN에서 부트스트랩 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-387">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="48b35-388">[getbootstrap.com](http://getbootstrap.com "getbootstrap.com") 부트스트랩의 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-388">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-441"></a><span data-ttu-id="48b35-389">부트 스트랩 버전 4.4.1</span><span class="sxs-lookup"><span data-stu-id="48b35-389">Bootstrap version 4.4.1</span></span>

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

#### <a name="bootstrap-version-431"></a><span data-ttu-id="48b35-390">부트스트랩 버전 4.3.1</span><span class="sxs-lookup"><span data-stu-id="48b35-390">Bootstrap version 4.3.1</span></span>

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

#### <a name="bootstrap-version-421"></a><span data-ttu-id="48b35-391">부트스트랩 버전 4.2.1</span><span class="sxs-lookup"><span data-stu-id="48b35-391">Bootstrap version 4.2.1</span></span>

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

#### <a name="bootstrap-version-411"></a><span data-ttu-id="48b35-392">부트 스트랩 버전 4.1.1</span><span class="sxs-lookup"><span data-stu-id="48b35-392">Bootstrap version 4.1.1</span></span>

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

#### <a name="bootstrap-version-400"></a><span data-ttu-id="48b35-393">부트스트랩 버전 4.0.0</span><span class="sxs-lookup"><span data-stu-id="48b35-393">Bootstrap version 4.0.0</span></span>

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

#### <a name="bootstrap-version-341"></a><span data-ttu-id="48b35-394">부트스트랩 버전 3.4.1</span><span class="sxs-lookup"><span data-stu-id="48b35-394">Bootstrap version 3.4.1</span></span>

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

#### <a name="bootstrap-version-340"></a><span data-ttu-id="48b35-395">부트스트랩 버전 3.4.0</span><span class="sxs-lookup"><span data-stu-id="48b35-395">Bootstrap version 3.4.0</span></span>

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

#### <a name="bootstrap-version-337"></a><span data-ttu-id="48b35-396">부트스트랩 버전 3.3.7</span><span class="sxs-lookup"><span data-stu-id="48b35-396">Bootstrap version 3.3.7</span></span>

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

#### <a name="bootstrap-version-336"></a><span data-ttu-id="48b35-397">부트스트랩 버전 3.3.6</span><span class="sxs-lookup"><span data-stu-id="48b35-397">Bootstrap version 3.3.6</span></span>

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

#### <a name="bootstrap-version-335"></a><span data-ttu-id="48b35-398">부트스트랩 버전 3.3.5</span><span class="sxs-lookup"><span data-stu-id="48b35-398">Bootstrap version 3.3.5</span></span>

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

#### <a name="bootstrap-version-334"></a><span data-ttu-id="48b35-399">부트스트랩 버전 3.3.4</span><span class="sxs-lookup"><span data-stu-id="48b35-399">Bootstrap version 3.3.4</span></span>

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

#### <a name="bootstrap-version-332"></a><span data-ttu-id="48b35-400">부트스트랩 버전 3.3.2</span><span class="sxs-lookup"><span data-stu-id="48b35-400">Bootstrap version 3.3.2</span></span>

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

#### <a name="bootstrap-version-331"></a><span data-ttu-id="48b35-401">부트스트랩 버전 3.3.1</span><span class="sxs-lookup"><span data-stu-id="48b35-401">Bootstrap version 3.3.1</span></span>

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

#### <a name="bootstrap-version-330"></a><span data-ttu-id="48b35-402">부트스트랩 버전 3.3.0</span><span class="sxs-lookup"><span data-stu-id="48b35-402">Bootstrap version 3.3.0</span></span>

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

#### <a name="bootstrap-version-320"></a><span data-ttu-id="48b35-403">부트스트랩 버전 3.2.0</span><span class="sxs-lookup"><span data-stu-id="48b35-403">Bootstrap version 3.2.0</span></span>

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

#### <a name="bootstrap-version-311"></a><span data-ttu-id="48b35-404">부트스트랩 버전 3.1.1</span><span class="sxs-lookup"><span data-stu-id="48b35-404">Bootstrap version 3.1.1</span></span>

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

#### <a name="bootstrap-version-310"></a><span data-ttu-id="48b35-405">부트스트랩 버전 3.1.0</span><span class="sxs-lookup"><span data-stu-id="48b35-405">Bootstrap version 3.1.0</span></span>

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

#### <a name="bootstrap-version-303"></a><span data-ttu-id="48b35-406">부트스트랩 버전 3.0.3</span><span class="sxs-lookup"><span data-stu-id="48b35-406">Bootstrap version 3.0.3</span></span>

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

#### <a name="bootstrap-version-302"></a><span data-ttu-id="48b35-407">부트스트랩 버전 3.0.2</span><span class="sxs-lookup"><span data-stu-id="48b35-407">Bootstrap version 3.0.2</span></span>

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

#### <a name="bootstrap-version-301"></a><span data-ttu-id="48b35-408">부트스트랩 버전 3.0.1</span><span class="sxs-lookup"><span data-stu-id="48b35-408">Bootstrap version 3.0.1</span></span>

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

#### <a name="bootstrap-version-300"></a><span data-ttu-id="48b35-409">부트스트랩 버전 3.0.0</span><span class="sxs-lookup"><span data-stu-id="48b35-409">Bootstrap version 3.0.0</span></span>

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

#### <a name="bootstrap-version-232"></a><span data-ttu-id="48b35-410">부트스트랩 버전 2.3.2</span><span class="sxs-lookup"><span data-stu-id="48b35-410">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="48b35-411">부트스트랩 버전 2.3.1</span><span class="sxs-lookup"><span data-stu-id="48b35-411">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="48b35-412">부트스트랩 터치카로젤이 CDN에서 출시됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-412">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="48b35-413">부트 스트랩 [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") 터치 카루스엘 릴리스의 다음 릴리스는 CDN에서 호스팅됩니다 :</span><span class="sxs-lookup"><span data-stu-id="48b35-413">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="48b35-414">부트스트랩 터치카로젤 버전 0.8.0</span><span class="sxs-lookup"><span data-stu-id="48b35-414">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="48b35-415">CDN에서 해머.js 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-415">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="48b35-416">Hammer.js [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") 릴리스의 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-416">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="48b35-417">해머.js 버전 2.0.4</span><span class="sxs-lookup"><span data-stu-id="48b35-417">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="48b35-418">CDN에서 웹 양식 및 아약스 릴리스에 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="48b35-418">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="48b35-419">ASP.NET 아약스 라이브러리의 다음 릴리스는 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-419">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="48b35-420">각 링크를 클릭하여 파일의 실제 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-420">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="48b35-421">ASP.NET 웹 양식 및 아약스 버전 4.5.2</span><span class="sxs-lookup"><span data-stu-id="48b35-421">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "ASP.NET Web Forms 및 Ajax 4.5.2")
- [<span data-ttu-id="48b35-422">ASP.NET 웹 양식 및 아약스 버전 4</span><span class="sxs-lookup"><span data-stu-id="48b35-422">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "ASP.NET Web Forms and Ajax 4")
- [<span data-ttu-id="48b35-423">ASP.NET 아약스 버전 3.5</span><span class="sxs-lookup"><span data-stu-id="48b35-423">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "ASP.NET Ajax 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="48b35-424">ASP.NET MVC 는 CDN에서 출시됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-424">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="48b35-425">다음은 이 CDN에서 ASP.NET MVC 자바스크립트 파일이 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-425">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="48b35-426">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="48b35-426">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="48b35-427">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="48b35-427">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="48b35-428">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="48b35-428">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="48b35-429">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="48b35-429">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="48b35-430">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="48b35-430">ASP.NET MVC 3.0</span></span>

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

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="48b35-431">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="48b35-431">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="48b35-432">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="48b35-432">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="48b35-433">CDN에서 ASP.NET 시그널R 릴리스</span><span class="sxs-lookup"><span data-stu-id="48b35-433">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="48b35-434">다음 ASP.NET SignalR 자바 스크립트 파일은이 CDN에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="48b35-434">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="48b35-435">ASP.NET 시그널R 2.2.2</span><span class="sxs-lookup"><span data-stu-id="48b35-435">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="48b35-436">ASP.NET 시그널R 2.2.1</span><span class="sxs-lookup"><span data-stu-id="48b35-436">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="48b35-437">ASP.NET 시그널R 2.2.0</span><span class="sxs-lookup"><span data-stu-id="48b35-437">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="48b35-438">ASP.NET 시그널R 2.1.0</span><span class="sxs-lookup"><span data-stu-id="48b35-438">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="48b35-439">ASP.NET 시그널R 2.0.3</span><span class="sxs-lookup"><span data-stu-id="48b35-439">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="48b35-440">ASP.NET 시그널R 2.0.2</span><span class="sxs-lookup"><span data-stu-id="48b35-440">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="48b35-441">ASP.NET 시그널R 2.0.1</span><span class="sxs-lookup"><span data-stu-id="48b35-441">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="48b35-442">ASP.NET 시그널R 2.0.0</span><span class="sxs-lookup"><span data-stu-id="48b35-442">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="48b35-443">ASP.NET 시그널R 1.1.3</span><span class="sxs-lookup"><span data-stu-id="48b35-443">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="48b35-444">ASP.NET 시그널R 1.1.2</span><span class="sxs-lookup"><span data-stu-id="48b35-444">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="48b35-445">ASP.NET 시그널R 1.1.1</span><span class="sxs-lookup"><span data-stu-id="48b35-445">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="48b35-446">ASP.NET 시그널R 1.1.0</span><span class="sxs-lookup"><span data-stu-id="48b35-446">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="48b35-447">ASP.NET 시그널R 1.0.1</span><span class="sxs-lookup"><span data-stu-id="48b35-447">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="48b35-448">CDN의 사용 약관에 대한 자세한 내용은 [Microsoft Ajax CDN 사용 약관을](https://www.asp.net/terms-of-use "마이크로소프트 아약스 CDN 이용 약관")참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="48b35-448">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
