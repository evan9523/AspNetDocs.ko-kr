---
title: ASP.NET Core에 대 한 클라이언트 IP 수신
author: damienbod
description: 승인 된 IP 주소의 목록에 대해 원격 IP 주소의 유효성을 검사 하려면 미들웨어 또는 작업 필터를 작성 하는 방법에 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/31/2018
uid: security/ip-safelist
ms.openlocfilehash: 286f199c0d9164fa70d511aba523210c85c2fdfd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036840"
---
# <a name="client-ip-safelist-for-aspnet-core"></a><span data-ttu-id="bc933-103">ASP.NET Core에 대 한 클라이언트 IP 수신</span><span class="sxs-lookup"><span data-stu-id="bc933-103">Client IP safelist for ASP.NET Core</span></span>

<span data-ttu-id="bc933-104">하 여 [Damien Bowden](https://twitter.com/damien_bod) 고 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="bc933-104">By [Damien Bowden](https://twitter.com/damien_bod) and [Tom Dykstra](https://github.com/tdykstra)</span></span>
 
<span data-ttu-id="bc933-105">이 아티클에서 IP 수신 (라고도: 화이트 리스트) ASP.NET Core 앱을 구현 하는 세 가지 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-105">This article shows three ways to implement an IP safelist (also known as a whitelist) in an ASP.NET Core app.</span></span> <span data-ttu-id="bc933-106">사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-106">You can use:</span></span>

* <span data-ttu-id="bc933-107">모든 요청 원격 IP 주소를 확인 하는 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-107">Middleware to check the remote IP address of every request.</span></span>
* <span data-ttu-id="bc933-108">특정 컨트롤러 또는 작업 메서드에 대 한 요청 된 원격 IP 주소를 확인 하려면 작업 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-108">Action filters to check the remote IP address of requests for specific controllers or action methods.</span></span>
* <span data-ttu-id="bc933-109">Razor 페이지 필터를 Razor 페이지에 대 한 요청 된 원격 IP 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-109">Razor Pages filters to check the remote IP address of requests for Razor pages.</span></span>

<span data-ttu-id="bc933-110">샘플 앱은 두 가지 방법을 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-110">The sample app illustrates both approaches.</span></span> <span data-ttu-id="bc933-111">각 경우에서는 승인 된 클라이언트 IP 주소를 포함 하는 문자열을 앱 설정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-111">In each case, a string containing approved client IP addresses is stored in an app setting.</span></span> <span data-ttu-id="bc933-112">미들웨어 또는 필터를 목록으로 문자열을 구문 분석 하 고 원격 IP 목록 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-112">The middleware or filter parses the string into a list and  checks if the remote IP is in the list.</span></span> <span data-ttu-id="bc933-113">그렇지 않은 경우는 HTTP 403 사용 권한 없음 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-113">If not, an HTTP 403 Forbidden status code is returned.</span></span>

<span data-ttu-id="bc933-114">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/ip-safelist/samples/2.x/ClientIpAspNetCore) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="bc933-114">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/ip-safelist/samples/2.x/ClientIpAspNetCore) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="the-safelist"></a><span data-ttu-id="bc933-115">수신</span><span class="sxs-lookup"><span data-stu-id="bc933-115">The safelist</span></span>

<span data-ttu-id="bc933-116">목록에 구성 된 *appsettings.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-116">The list is configured in the *appsettings.json* file.</span></span> <span data-ttu-id="bc933-117">세미콜론으로 구분 된 목록 이므로 IPv4 및 IPv6 주소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-117">It's a semicolon-delimited list and can contain IPv4 and IPv6 addresses.</span></span>

[!code-json[](ip-safelist/samples/2.x/ClientIpAspNetCore/appsettings.json?highlight=2)]

## <a name="middleware"></a><span data-ttu-id="bc933-118">미들웨어</span><span class="sxs-lookup"><span data-stu-id="bc933-118">Middleware</span></span>

<span data-ttu-id="bc933-119">`Configure` 메서드는 미들웨어를 추가 하 고 수신 문자열을 생성자 매개 변수에서를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-119">The `Configure` method adds the middleware and passes the safelist string to it in a constructor parameter.</span></span>

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Startup.cs?name=snippet_Configure&highlight=7)]

<span data-ttu-id="bc933-120">미들웨어를 배열에 문자열을 구문 분석 및 배열에 있는 원격 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-120">The middleware parses the string into an array and looks for the remote IP address in the array.</span></span> <span data-ttu-id="bc933-121">원격 IP 주소가 없는 경우 미들웨어는 HTTP 401 사용할 수 없음 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-121">If the remote IP address is not found, the middleware returns HTTP 401 Forbidden.</span></span> <span data-ttu-id="bc933-122">이 유효성 검사 프로세스는 HTTP Get 요청에 대해 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-122">This validation process is bypassed for HTTP Get requests.</span></span>

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/AdminSafeListMiddleware.cs?name=snippet_ClassOnly)]

## <a name="action-filter"></a><span data-ttu-id="bc933-123">작업 필터</span><span class="sxs-lookup"><span data-stu-id="bc933-123">Action filter</span></span>

<span data-ttu-id="bc933-124">특정 컨트롤러 또는 작업 메서드에서 동안만 수신 하려는 경우에 작업 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-124">If you want a safelist only for specific controllers or action methods, use an action filter.</span></span> <span data-ttu-id="bc933-125">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-125">Here's an example:</span></span> 

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Filters/ClientIdCheckFilter.cs)]

<span data-ttu-id="bc933-126">작업 필터는 서비스 컨테이너에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-126">The action filter is added to the services container.</span></span>

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Startup.cs?name=snippet_ConfigureServices&highlight=3)]

<span data-ttu-id="bc933-127">필터 컨트롤러나 작업 메서드에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-127">The filter can then be used on a controller or action method.</span></span>

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Controllers/ValuesController.cs?name=snippet_Filter&highlight=1)]

<span data-ttu-id="bc933-128">샘플 앱에서 필터에 적용 되는 `Get` 메서드.</span><span class="sxs-lookup"><span data-stu-id="bc933-128">In the sample app, the filter is applied to the `Get` method.</span></span> <span data-ttu-id="bc933-129">전송 하 여 앱을 테스트 하면를 `Get` 특성 클라이언트 IP 주소 유효성을 검사 하는 API를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-129">So when you test the app by sending a `Get` API request, the attribute is validating the client IP address.</span></span> <span data-ttu-id="bc933-130">다른 HTTP 메서드를 사용 하 여 API를 호출 하 여 테스트할 때 미들웨어 클라이언트 IP의 유효성 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-130">When you test by calling the API with any other HTTP method, the middleware is validating the client IP.</span></span>

## <a name="razor-pages-filter"></a><span data-ttu-id="bc933-131">Razor 페이지 필터링</span><span class="sxs-lookup"><span data-stu-id="bc933-131">Razor Pages filter</span></span> 

<span data-ttu-id="bc933-132">Razor 페이지 앱에 대 한를 수신 하려는 경우에 Razor 페이지 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-132">If you want a safelist for a Razor Pages app, use a Razor Pages filter.</span></span> <span data-ttu-id="bc933-133">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-133">Here's an example:</span></span> 

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Filters/ClientIdCheckPageFilter.cs)]

<span data-ttu-id="bc933-134">이 필터는 MVC 필터 컬렉션에 추가 하 여 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-134">This filter is enabled by adding it to the MVC Filters collection.</span></span>

[!code-csharp[](ip-safelist/samples/2.x/ClientIpAspNetCore/Startup.cs?name=snippet_ConfigureServices&highlight=7-9)]

<span data-ttu-id="bc933-135">앱을 실행 하는 Razor 페이지를 요청 하는 경우 Razor 페이지 필터 클라이언트 IP의 유효성 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-135">When you run the app and request a Razor page, the Razor Pages filter is validating the client IP.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc933-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bc933-136">Next steps</span></span>

<span data-ttu-id="bc933-137">[ASP.NET Core 미들웨어에 자세히 알아보려면](xref:fundamentals/middleware/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc933-137">[Learn more about ASP.NET Core Middleware](xref:fundamentals/middleware/index).</span></span>
