---
title: ASP.NET Core MVC에 대한 호환성 버전
author: rick-anderson
description: ASP.NET Core의 시작 클래스에서 서비스 및 앱의 요청 파이프라인을 구성하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2019
uid: mvc/compatibility-version
ms.openlocfilehash: b360da105799a1dccb1902e167e50e78864b76a9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048020"
---
# <a name="compatibility-version-for-aspnet-core-mvc"></a><span data-ttu-id="57929-103">ASP.NET Core MVC에 대한 호환성 버전</span><span class="sxs-lookup"><span data-stu-id="57929-103">Compatibility version for ASP.NET Core MVC</span></span>

<span data-ttu-id="57929-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="57929-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="57929-105"><xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> 메서드를 사용하면 ASP.NET Core MVC 2.1 이상에서 도입된 주요 동작 변경 내용을 앱이 옵트인(opt-in) 또는 옵트아웃(opt-out)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57929-105">The <xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> method allows an app to opt-in or opt-out of potentially breaking behavior changes introduced in ASP.NET Core MVC 2.1 or later.</span></span> <span data-ttu-id="57929-106">이 주요 동작 변경 내용은 일반적으로 MVC 하위 시스템의 작동 방식과 런타임에서 **코드**를 호출하는 방법과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57929-106">These potentially breaking behavior changes are generally in how the MVC subsystem behaves and how **your code** is called by the runtime.</span></span> <span data-ttu-id="57929-107">옵트인을 하면 ASP.NET Core의 최신 동작과 장기 동작을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57929-107">By opting in, you get the latest behavior, and the long-term behavior of ASP.NET Core.</span></span>

<span data-ttu-id="57929-108">다음 코드는 호환성 모드를 ASP.NET Core 2.2로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="57929-108">The following code sets the compatibility mode to ASP.NET Core 2.2:</span></span>

[!code-csharp[Main](compatibility-version/samples/2.x/CompatibilityVersionSample/Startup.cs?name=snippet1)]

<span data-ttu-id="57929-109">최신 버전(`CompatibilityVersion.Version_2_2`)을 사용하여 앱을 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="57929-109">We recommend you test your app using the latest version (`CompatibilityVersion.Version_2_2`).</span></span> <span data-ttu-id="57929-110">대부분의 앱은 최신 버전을 사용하여 주요 동작을 변경하지 않을 것으로 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="57929-110">We anticipate that most apps won't have breaking behavior changes using the latest version.</span></span>

<span data-ttu-id="57929-111">`SetCompatibilityVersion(CompatibilityVersion.Version_2_0)`을 호출하는 앱은 ASP.NET Core 2.1 MVC 및 이후의 2.x 버전에서 도입된 주요 동작 변경으로부터 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="57929-111">Apps that call `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)` are protected from potentially breaking behavior changes introduced in the ASP.NET Core 2.1 MVC and later 2.x versions.</span></span> <span data-ttu-id="57929-112">이 보호:</span><span class="sxs-lookup"><span data-stu-id="57929-112">This protection:</span></span>

* <span data-ttu-id="57929-113">2.1 이상의 모든 변경 내용에 적용되지는 않으며, MVC 하위 시스템의 주요 ASP.NET Core 런타임 동작 변경을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="57929-113">Does not apply to all 2.1 and later changes, it's targeted to potentially breaking ASP.NET Core runtime behavior changes in the MVC subsystem.</span></span>
* <span data-ttu-id="57929-114">다음의 주 버전으로 확장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57929-114">Does not extend to the next major version.</span></span>

<span data-ttu-id="57929-115">`SetCompatibilityVersion`을 호출하지 **않는** ASP.NET Core 2.1 및 이후 2.x 앱의 기본 호환성은 2.0 호환성입니다.</span><span class="sxs-lookup"><span data-stu-id="57929-115">The default compatibility for ASP.NET Core 2.1 and later 2.x apps that do **not** call `SetCompatibilityVersion` is 2.0 compatibility.</span></span> <span data-ttu-id="57929-116">즉, `SetCompatibilityVersion`을 호출하지 않는 것은 `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)`을 호출하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57929-116">That is, not calling `SetCompatibilityVersion` is the same as calling `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)`.</span></span>

<span data-ttu-id="57929-117">다음 코드는 다음 동작을 제외하고, 호환성 모드를 ASP.NET Core 2.2로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="57929-117">The following code sets the compatibility mode to ASP.NET Core 2.2, except for the following behaviors:</span></span>

* <xref:Microsoft.AspNetCore.Mvc.MvcOptions.AllowCombiningAuthorizeFilters>
* <xref:Microsoft.AspNetCore.Mvc.MvcOptions.InputFormatterExceptionPolicy>

[!code-csharp[Main](compatibility-version/samples/2.x/CompatibilityVersionSample/Startup2.cs?name=snippet1)]

<span data-ttu-id="57929-118">적절한 호환성 스위치를 사용하여 주요 동작 변경 내용이 발생하는 앱의 경우:</span><span class="sxs-lookup"><span data-stu-id="57929-118">For apps that encounter breaking behavior changes, using the appropriate compatibility switches:</span></span>

* <span data-ttu-id="57929-119">최신 릴리스를 사용하고 특정 주요 동작 변경 내용을 옵트아웃(opt out)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57929-119">Allows you to use the latest release and opt out of specific breaking behavior changes.</span></span>
* <span data-ttu-id="57929-120">최신 변경 내용과 함께 작동하도록 앱을 업데이트할 시간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57929-120">Gives you time to update your app so it works with the latest changes.</span></span>

<span data-ttu-id="57929-121"><xref:Microsoft.AspNetCore.Mvc.MvcOptions> 설명서에는 변경된 내용과 변경 내용이 대부분의 사용자에게 향상된 기능인 이유가 잘 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57929-121">The <xref:Microsoft.AspNetCore.Mvc.MvcOptions> documentation has a good explanation of what changed and why the changes are an improvement for most users.</span></span>

<span data-ttu-id="57929-122">이후에 [ASP.NET Core 3.0 버전](https://github.com/aspnet/Home/wiki/Roadmap)이 나올 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="57929-122">At some future date, there will be an [ASP.NET Core 3.0 version](https://github.com/aspnet/Home/wiki/Roadmap).</span></span> <span data-ttu-id="57929-123">호환성 스위치가 지원하는 이전 동작은 3.0 버전에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="57929-123">Old behaviors supported by compatibility switches will be removed in the 3.0 version.</span></span> <span data-ttu-id="57929-124">거의 모든 사용자에게 혜택을 주는 긍정적인 변화라고 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="57929-124">We feel these are positive changes benefitting nearly all users.</span></span> <span data-ttu-id="57929-125">이제 이러한 변경 내용을 도입함으로써 대부분의 앱이 혜택을 받을 수 있으며, 다른 사람은 앱을 업데이트할 시간을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57929-125">By introducing these changes now, most apps can benefit now, and the others will have time to update their apps.</span></span>
