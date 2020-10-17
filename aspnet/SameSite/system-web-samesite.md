---
title: ASP.NET에서 SameSite 쿠키 사용
author: rick-anderson
description: 를 사용 하 여 ASP.NET에서 쿠키를 SameSite 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: d50f157c6d92cb56cb6c59381af9139d1d3d1d3d
ms.sourcegitcommit: a309ca7af61e59195beb745b501a1a9f06fcd493
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92119365"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="ad0df-103">ASP.NET에서 SameSite 쿠키 사용</span><span class="sxs-lookup"><span data-stu-id="ad0df-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="ad0df-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ad0df-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="ad0df-105">SameSite은 CSRF (교차 사이트 요청 위조) 공격에 대 한 보호를 제공 하도록 설계 된 [IETF](https://ietf.org/about/) 초안 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-105">SameSite is an [IETF](https://ietf.org/about/) draft standard designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="ad0df-106">원래 [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)에서는 초안 표준이 [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)에서 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-106">Originally drafted in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), the draft standard was updated in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span></span> <span data-ttu-id="ad0df-107">업데이트 된 표준은 이전 표준과 호환 되지 않으며 다음과 같은 가장 눈에 띄는 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-107">The updated standard is not backward compatible with the previous standard, with the following being the most noticeable differences:</span></span>

* <span data-ttu-id="ad0df-108">SameSite 헤더가 없는 쿠키는 기본적으로로 처리 됩니다 `SameSite=Lax` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-108">Cookies without SameSite header are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="ad0df-109">`SameSite=None` 사이트 간 쿠키 사용을 허용 하려면를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-109">`SameSite=None` must be used to allow cross-site cookie use.</span></span>
* <span data-ttu-id="ad0df-110">어설션 되는 쿠키 `SameSite=None` 도로 표시 되어야 `Secure` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-110">Cookies that assert `SameSite=None` must also be marked as `Secure`.</span></span>
* <span data-ttu-id="ad0df-111">[`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) `sameSite=Lax` `sameSite=Strict` `<iframe>` 가 사이트 간 시나리오로 처리 되기 때문에를 사용 하는 응용 프로그램은 또는 쿠키와 관련 된 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-111">Applications that use [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) may experience issues with `sameSite=Lax` or `sameSite=Strict` cookies because `<iframe>` is treated as cross-site scenarios.</span></span>
* <span data-ttu-id="ad0df-112">값은 `SameSite=None` [2016 표준](https://tools.ietf.org/html/draft-west-first-party-cookies-07) 에서 허용 되지 않으며 일부 구현에서 이러한 쿠키를로 처리 `SameSite=Strict` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-112">The value `SameSite=None` is not allowed by the [2016 standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) and causes some implementations to treat such cookies as `SameSite=Strict`.</span></span> <span data-ttu-id="ad0df-113">이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-113">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="ad0df-114">이 `SameSite=Lax` 설정은 대부분의 응용 프로그램 쿠키에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-114">The `SameSite=Lax` setting works for most application cookies.</span></span> <span data-ttu-id="ad0df-115">Oidc ( [Openid connect Connect](https://openid.net/connect/) )와 같은 일부 형태의 인증 및 [ws-federation](https://auth0.com/docs/protocols/ws-fed) 은 게시 기반 리디렉션에 대해 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-115">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="ad0df-116">사후 기반 리디렉션은 SameSite 브라우저 보호를 트리거하고 이러한 구성 요소에 대해 SameSite을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-116">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="ad0df-117">대부분의 [OAuth](https://oauth.net/) 로그인은 요청 흐름의 차이로 인해 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-117">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="ad0df-118">쿠키를 내보내는 각 ASP.NET 구성 요소는 SameSite가 적절 한지 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-118">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

<span data-ttu-id="ad0df-119">2019 .Net SameSite 업데이트를 설치한 후 응용 프로그램 문제에 대 한 [알려진 문제](#known) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-119">See [Known Issues](#known) for problems with applications after installing the 2019 .Net SameSite updates.</span></span>

## <a name="using-samesite-in-aspnet-472-and-48"></a><span data-ttu-id="ad0df-120">ASP.NET 4.7.2 및 4.8에서 SameSite 사용</span><span class="sxs-lookup"><span data-stu-id="ad0df-120">Using SameSite in ASP.NET 4.7.2 and 4.8</span></span>

<span data-ttu-id="ad0df-121">.Net 4.7.2 및 4.8는 12 월 2019의 업데이트 출시 이후 SameSite에 대 한 [2019 초안 표준을](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-121">.Net 4.7.2 and 4.8 supports the [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite since the release of updates in December 2019.</span></span> <span data-ttu-id="ad0df-122">개발자는 [SameSite 속성](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)을 사용 하 여 SameSite 헤더의 값을 프로그래밍 방식으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-122">Developers are able to programmatically control the value of the SameSite header using the [HttpCookie.SameSite property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span></span> <span data-ttu-id="ad0df-123">속성을 `SameSite` , 또는로 설정 하면 `Strict` `Lax` `None` 해당 값이 쿠키를 사용 하 여 네트워크에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-123">Setting the `SameSite` property to `Strict`, `Lax`, or `None` results in those values being written on the network with the cookie.</span></span> <span data-ttu-id="ad0df-124">이 값을로 설정 하면 쿠키를 사용 하 여 `(SameSiteMode)(-1)` 네트워크에 SameSite 헤더를 포함 하지 않아야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-124">Setting it equal to `(SameSiteMode)(-1)` indicates that no SameSite header should be included on the network with the cookie.</span></span> <span data-ttu-id="ad0df-125">구성 파일의 [되어 속성](/dotnet/api/system.web.httpcookie.secure)또는 ' requireSSL '은 쿠키를로 표시 하는 데 사용할 수 있습니다 `Secure` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-125">The [HttpCookie.Secure Property](/dotnet/api/system.web.httpcookie.secure), or 'requireSSL' in config files, can be used to mark the cookie as `Secure` or not.</span></span>

<span data-ttu-id="ad0df-126">새 `HttpCookie` 인스턴스는 기본적으로 `SameSite=(SameSiteMode)(-1)` 및로 바뀝니다 `Secure=false` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-126">New `HttpCookie` instances will default to `SameSite=(SameSiteMode)(-1)` and `Secure=false`.</span></span> <span data-ttu-id="ad0df-127">이러한 기본값은 구성 섹션에서 재정의할 수 있습니다 `system.web/httpCookies` . 여기서 문자열은 `"Unspecified"` 에 대 한 간단한 구성 전용 구문입니다 `(SameSiteMode)(-1)` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-127">These defaults can be overridden in the `system.web/httpCookies` configuration section, where the string `"Unspecified"` is a friendly configuration-only syntax for `(SameSiteMode)(-1)`:</span></span>

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

<span data-ttu-id="ad0df-128">또한 ASP.Net는 이러한 기능에 대해 익명 인증, 폼 인증, 세션 상태 및 역할 관리와 같은 4 가지 특정 쿠키를 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-128">ASP.Net also issues four specific cookies of its own for these features: Anonymous Authentication, Forms Authentication, Session State, and Role Management.</span></span> <span data-ttu-id="ad0df-129">런타임에 가져온 이러한 쿠키의 인스턴스는 `SameSite` 다른 되어 인스턴스와 마찬가지로 및 속성을 사용 하 여 조작할 수 있습니다 `Secure` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-129">Instances of these cookies obtained in runtime can be manipulated using the `SameSite` and `Secure` properties just like any other HttpCookie instance.</span></span> <span data-ttu-id="ad0df-130">그러나 SameSite 표준의 패치워크 등장 때문에 이러한 4 가지 기능 쿠키에 대 한 구성 옵션은 일관 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-130">However, due to the patchwork emergence of the SameSite standard, configuration options for these four features cookies is inconsistent.</span></span> <span data-ttu-id="ad0df-131">다음은 관련 구성 섹션 및 특성입니다. 기본값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-131">The relevant configuration sections and attributes, with defaults, are shown below.</span></span> <span data-ttu-id="ad0df-132">`SameSite` `Secure` 기능에 대 한 또는 관련 특성이 없는 경우이 기능은 위에 설명 된 섹션에 구성 된 기본값으로 대체 됩니다 `system.web/httpCookies` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-132">If there is no `SameSite` or `Secure` related attribute for a feature, then the feature will fall back on the defaults configured in the `system.web/httpCookies` section discussed above.</span></span>

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

<span data-ttu-id="ad0df-133">**참고**: ' 지정 되지 않음 '은 현재에만 사용할 수 있습니다 `system.web/httpCookies@sameSite` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-133">**Note**: 'Unspecified' is only available to `system.web/httpCookies@sameSite` at the moment.</span></span> <span data-ttu-id="ad0df-134">이후 업데이트에서 이전에 표시 된 cookieSameSite 특성에 비슷한 구문을 추가 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-134">We hope to add similar syntax to the previously shown cookieSameSite attributes in future updates.</span></span> <span data-ttu-id="ad0df-135">`(SameSiteMode)(-1)`코드의 설정은 여전히 이러한 쿠키의 인스턴스에서 작동 합니다. \*</span><span class="sxs-lookup"><span data-stu-id="ad0df-135">Setting `(SameSiteMode)(-1)` in code still works on instances of these cookies.\*</span></span>

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a><span data-ttu-id="ad0df-136">.NET 앱 대상을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-136">Retarget .NET apps</span></span>

<span data-ttu-id="ad0df-137">.NET 4.7.2 이상을 대상으로 하려면:</span><span class="sxs-lookup"><span data-stu-id="ad0df-137">To target .NET 4.7.2 or later:</span></span>

* <span data-ttu-id="ad0df-138">*web.config* 다음을 포함 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-138">Ensure *web.config* contains the following:</span></span>  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  <span data-ttu-id="ad0df-139">자세한 내용은 [.Net 마이그레이션 가이드](/dotnet/framework/migration-guide/) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-139">The [.NET Migration Guide](/dotnet/framework/migration-guide/) has more details.</span></span>

* <span data-ttu-id="ad0df-140">프로젝트의 NuGet 패키지가 올바른 프레임 워크 버전을 대상으로 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-140">Verify NuGet packages in the project are targeted at the correct framework version.</span></span> <span data-ttu-id="ad0df-141">*packages.config* 파일을 검사 하 여 올바른 프레임 워크 버전을 확인할 수 있습니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-141">You can verify the correct framework version by examining the *packages.config* file, for example:</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  <span data-ttu-id="ad0df-142">위의 *packages.config* 파일에서 `Microsoft.ApplicationInsights` 패키지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-142">In the preceding *packages.config* file, the `Microsoft.ApplicationInsights` package:</span></span>
    * <span data-ttu-id="ad0df-143">는 .NET 4.5.1을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-143">Is  targeted against .NET 4.5.1.</span></span>
    * <span data-ttu-id="ad0df-144">`targetFramework` `net472` 프레임 워크 대상을 대상으로 하는 업데이트 된 패키지가 있는 경우 해당 특성이로 업데이트 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-144">Should have its `targetFramework` attribute updated to `net472` if an updated package targeting your framework target exists.</span></span>

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a><span data-ttu-id="ad0df-145">4.7.2 보다 이전 버전의 .NET</span><span class="sxs-lookup"><span data-stu-id="ad0df-145">.NET versions earlier than 4.7.2</span></span>

<span data-ttu-id="ad0df-146">Microsoft는 동일한 사이트 쿠키 특성을 4.7.2 하는 .NET 버전을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-146">Microsoft does not support .NET versions lower that 4.7.2 for writing the same-site cookie attribute.</span></span> <span data-ttu-id="ad0df-147">다음을 수행 하는 신뢰할 수 있는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-147">We have not found a reliable way to:</span></span>

* <span data-ttu-id="ad0df-148">브라우저 버전에 따라 특성이 올바르게 작성 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-148">Ensure the attribute is written correctly based on browser version.</span></span>
* <span data-ttu-id="ad0df-149">이전 프레임 워크 버전에서 인증 및 세션 쿠키를 가로채 고 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-149">Intercept and adjust authentication and session cookies on older framework versions.</span></span>

### <a name="december-patch-behavior-changes"></a><span data-ttu-id="ad0df-150">12 월 패치 동작 변경 내용</span><span class="sxs-lookup"><span data-stu-id="ad0df-150">December patch behavior changes</span></span>

<span data-ttu-id="ad0df-151">.NET Framework에 대 한 특정 동작 변경 내용은 `SameSite` 속성에서 값을 해석 하는 방법입니다 `None` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-151">The specific behavior change for .NET Framework is how the `SameSite` property interprets the `None` value:</span></span>

* <span data-ttu-id="ad0df-152">패치 값 이전에는 `None` 다음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-152">Before the patch a value of `None` meant:</span></span>
  * <span data-ttu-id="ad0df-153">특성을 전혀 내보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-153">Do not emit the attribute at all.</span></span>
* <span data-ttu-id="ad0df-154">패치 후:</span><span class="sxs-lookup"><span data-stu-id="ad0df-154">After the patch:</span></span>
  * <span data-ttu-id="ad0df-155">값은 `None` "값을 사용 하 여 특성을 내보냅니다 `None` ."를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-155">A value of `None` means "Emit the attribute with a value of `None`".</span></span>
  * <span data-ttu-id="ad0df-156">`SameSite`값이 `(SameSiteMode)(-1)` 이면 특성을 내보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-156">A `SameSite` value of `(SameSiteMode)(-1)` causes the attribute not to be emitted.</span></span>

<span data-ttu-id="ad0df-157">폼 인증 및 세션 상태 쿠키의 기본 SameSite 값이에서로 변경 `None` 되었습니다 `Lax` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-157">The default SameSite value for forms authentication and session state cookies was changed from `None` to `Lax`.</span></span>

### <a name="summary-of-change-impact-on-browsers"></a><span data-ttu-id="ad0df-158">브라우저에 대 한 변경 내용 영향 요약</span><span class="sxs-lookup"><span data-stu-id="ad0df-158">Summary of change impact on browsers</span></span>

<span data-ttu-id="ad0df-159">패치를 설치 하 고를 사용 하 여 쿠키를 발급 하는 경우 `SameSite.None` 다음 두 가지 중 하나가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-159">If you install the patch and issue a cookie with `SameSite.None`, one of two things will happen:</span></span>
* <span data-ttu-id="ad0df-160">Chrome v80는 새 구현에 따라이 쿠키를 처리 하며 쿠키에 대해 동일한 사이트 제한을 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-160">Chrome v80 will treat this cookie according to the new implementation, and not enforce same site restrictions on the cookie.</span></span>
* <span data-ttu-id="ad0df-161">새 구현을 지원 하도록 업데이트 되지 않은 브라우저는 이전 구현을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-161">Any browser that has not been updated to support the new implementation will follow the old implementation.</span></span> <span data-ttu-id="ad0df-162">이전 구현에는 다음이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-162">The old implementation says:</span></span>
  * <span data-ttu-id="ad0df-163">이해할 수 없는 값이 표시 되 면이를 무시 하 고 엄격한 동일한 사이트 제한으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-163">If you see a value you don't understand, ignore it and switch to strict same site restrictions.</span></span>

<span data-ttu-id="ad0df-164">따라서 앱이 Chrome에서 중단 되거나 다른 많은 위치에서 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-164">So either the app breaks in Chrome, or you break in numerous other places.</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="ad0df-165">기록 및 변경 내용</span><span class="sxs-lookup"><span data-stu-id="ad0df-165">History and changes</span></span>

<span data-ttu-id="ad0df-166">SameSite 지원은 [2016 초안 표준을](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)사용 하 여 .net 4.7.2에서 처음 구현 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-166">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="ad0df-167">2019 년 11 월 19 일 업데이트는 2016 표준에서 2019 standard로 업데이트 된 .NET 4.7.2 +입니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-167">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="ad0df-168">다른 버전의 Windows에 대 한 추가 업데이트가 곧 출시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-168">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="ad0df-169">자세한 내용은 <xref:samesite/kbs-samesite>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-169">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="ad0df-170">SameSite 사양의 2019 초안:</span><span class="sxs-lookup"><span data-stu-id="ad0df-170">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="ad0df-171">는 이전 버전과 호환 **되지 않습니다** . 2016 초안.</span><span class="sxs-lookup"><span data-stu-id="ad0df-171">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="ad0df-172">자세한 내용은이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-172">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="ad0df-173">쿠키를 기본적으로 처리 하도록 지정 합니다 `SameSite=Lax` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-173">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="ad0df-174">`SameSite=None`교차 사이트 배달을 사용 하도록 설정 하기 위해 명시적으로 어설션하는 쿠키를 지정 합니다 `Secure` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-174">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should also be marked as `Secure`.</span></span>
* <span data-ttu-id="ad0df-175">는 위에 나열 된 KB에 설명 된 대로 발급 된 패치에 의해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-175">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="ad0df-176">는 기본적으로 [2 월 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)에 [Chrome](https://chromestatus.com/feature/5088147346030592) 에서 사용 하도록 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-176">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="ad0df-177">브라우저에서 2019의이 표준으로 이동 하기 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-177">Browsers started moving to this standard in 2019.</span></span>

<a name="known"></a>

## <a name="known-issues"></a><span data-ttu-id="ad0df-178">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="ad0df-178">Known Issues</span></span>

<span data-ttu-id="ad0df-179">2016 및 2019 draft 사양이 호환 되지 않기 때문에 11 월 2019 .Net Framework 업데이트에서 일부 변경 내용이 적용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-179">Because the 2016 and 2019 draft specifications are not compatible, the November 2019 .Net Framework update introduces some changes that may be breaking.</span></span>

* <span data-ttu-id="ad0df-180">이제 세션 상태와 폼 인증 쿠키가 지정 되지 않은 것 처럼 네트워크에 기록 됩니다 `Lax` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-180">Session State and Forms Authentication cookies are now written to the network as `Lax` instead of unspecified.</span></span>
  * <span data-ttu-id="ad0df-181">대부분의 앱은 `SameSite=Lax` 쿠키를 사용 하지만을 사용 하는 사이트 또는 응용 프로그램에 게시 된 앱은 `iframe` 세션 상태나 폼 권한 부여 쿠키가 예상 대로 사용 되지 않는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-181">While most apps work with `SameSite=Lax` cookies, apps that POST across sites or applications that make use of `iframe` may find that their session state or forms authorization cookies aren't being used as expected.</span></span> <span data-ttu-id="ad0df-182">이를 해결 하려면 앞에서 `cookieSameSite` 설명한 대로 적절 한 구성 섹션의 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-182">To remedy this, change the `cookieSameSite` value in the appropriate configuration section as discussed previously.</span></span>
* <span data-ttu-id="ad0df-183">코드 또는 구성에서 명시적으로 설정 된 HttpCookies `SameSite=None` 는 이제 쿠키를 사용 하 여 값을 작성 했지만 이전에는 생략 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-183">HttpCookies that explicitly set `SameSite=None` in code or configuration now have that value written with the cookie, whereas it was previously omitted.</span></span> <span data-ttu-id="ad0df-184">이로 인해 2016 초안 표준만 지 원하는 이전 브라우저에서 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-184">This may cause issues with older browsers that only support the 2016 draft standard.</span></span>
  * <span data-ttu-id="ad0df-185">쿠키를 사용 하 여 2019 초안 표준을 지 원하는 브라우저를 대상으로 지정 하는 경우 `SameSite=None` 이를 표시 `Secure` 하거나 인식 하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-185">When targeting browsers supporting the 2019 draft standard with `SameSite=None` cookies, remember to also mark them `Secure` or they may not be recognized.</span></span>
  * <span data-ttu-id="ad0df-186">작성 하지 않는 2016 동작으로 되돌리려면 `SameSite=None` 앱 설정을 사용 `aspnet:SupressSameSiteNone=true` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-186">To revert to the 2016 behavior of not writing `SameSite=None`, use the app setting `aspnet:SupressSameSiteNone=true`.</span></span> <span data-ttu-id="ad0df-187">이는 앱의 모든 HttpCookies에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-187">Note that this will apply to all HttpCookies in the app.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="ad0df-188">Azure App Service-SameSite 쿠키 처리</span><span class="sxs-lookup"><span data-stu-id="ad0df-188">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="ad0df-189">Azure App Service .Net 4.7.2 앱에서 SameSite 동작을 구성 하는 방법에 대 한 자세한 내용은 [Azure App Service-SameSite 쿠키 처리 및 .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-189">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for information about how Azure App Service is configuring SameSite behaviors in .Net 4.7.2 apps.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="ad0df-190">이전 브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="ad0df-190">Supporting older browsers</span></span>

<span data-ttu-id="ad0df-191">2016 SameSite 표준에서는 알 수 없는 값을 값으로 처리 해야 합니다 `SameSite=Strict` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-191">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="ad0df-192">2016 SameSite 표준을 지 원하는 이전 브라우저에서 액세스 된 앱은 값이 인 SameSite 속성을 가져올 때 손상 될 수 있습니다 `None` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-192">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="ad0df-193">웹 앱은 이전 브라우저를 지원 하려는 경우 브라우저 검색을 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-193">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="ad0df-194">User-Agents 값이 매우 휘발성 이며 자주 변경 되기 때문에 ASP.NET는 브라우저 검색을 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-194">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span>

<span data-ttu-id="ad0df-195">문제를 해결 하는 Microsoft의 접근 방식은 브라우저가 `sameSite=None` 지원 하지 않는 것으로 알려진 경우 쿠키에서 특성을 제거 하는 브라우저 검색 구성 요소를 구현할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-195">Microsoft's approach to fixing the problem is to help you implement browser detection components to strip the `sameSite=None` attribute from cookies if a browser is known to not support it.</span></span> <span data-ttu-id="ad0df-196">Google의 충고는 두 쿠키를 발급 하는 것으로, 하나는 새 특성을, 하나는 특성이 없는 쿠키를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-196">Google's advice was to issue double cookies, one with the new attribute, and one without the attribute at all.</span></span> <span data-ttu-id="ad0df-197">하지만 Google의 조언을 제한적으로 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-197">However we consider Google's advice limited.</span></span> <span data-ttu-id="ad0df-198">일부 브라우저, 특히 모바일 브라우저는 한 사이트의 쿠키 수에 대 한 제한이 매우 적거나 도메인 이름이 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-198">Some browsers, especially mobile browsers have very small limits on the number of cookies a site, or a domain name can send.</span></span> <span data-ttu-id="ad0df-199">여러 쿠키를 전송 하는 경우, 특히 인증 쿠키와 같은 큰 쿠키는 모바일 브라우저 제한에 신속 하 게 도달 하 여 진단 하 고 수정 하기 어려운 앱 오류를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-199">Sending multiple cookies, especially large cookies like authentication cookies can reach the mobile browser limit very quickly, causing app failures that are hard to diagnose and fix.</span></span> <span data-ttu-id="ad0df-200">또한 두 번째 쿠키 방식을 사용 하도록 업데이트 되지 않은 타사 코드 및 구성 요소에 대 한 많은 에코 시스템이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-200">Furthermore as a framework there is a large ecosystem of third party code and components that may not be updated to use a double cookie approach.</span></span>

<span data-ttu-id="ad0df-201">[이 GitHub 리포지토리의]() 샘플 프로젝트에 사용 되는 브라우저 검색 코드는 두 개의 파일에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-201">The browser detection code used in the sample projects in [this GitHub repository]() is contained in two files</span></span>

* [<span data-ttu-id="ad0df-202">C # SameSiteSupport.cs</span><span class="sxs-lookup"><span data-stu-id="ad0df-202">C# SameSiteSupport.cs</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [<span data-ttu-id="ad0df-203">VB SameSiteSupport</span><span class="sxs-lookup"><span data-stu-id="ad0df-203">VB SameSiteSupport.vb</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

<span data-ttu-id="ad0df-204">이러한 검색은 가장 일반적인 브라우저 에이전트로, 2016 표준을 지원 하 고 특성을 완전히 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-204">These detections are the most common browser agents we have seen that support the 2016 standard and for which the attribute needs to be completely removed.</span></span> <span data-ttu-id="ad0df-205">완전 한 구현이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-205">It isn't meant as a complete implementation:</span></span>

* <span data-ttu-id="ad0df-206">앱에서 테스트 사이트가 아닌 브라우저를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-206">Your app may see browsers that our test sites do not.</span></span>
* <span data-ttu-id="ad0df-207">사용자 환경에 필요한 경우 검색을 추가할 준비를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-207">You should be prepared to add detections as necessary for your environment.</span></span>

<span data-ttu-id="ad0df-208">검색을 연결 하는 방법은 사용 중인 .NET 및 웹 프레임 워크의 버전에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-208">How you wire up the detection varies according the version of .NET and the web framework that you are using.</span></span> <span data-ttu-id="ad0df-209">[되어](/dotnet/api/system.web.httpcookie) 호출 사이트에서 다음 코드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-209">The following code can be called at the [HttpCookie](/dotnet/api/system.web.httpcookie) call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="ad0df-210">다음 ASP.NET 4.7.2 SameSite cookie 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-210">See the following ASP.NET 4.7.2 SameSite cookie topics:</span></span>

* [<span data-ttu-id="ad0df-211">C# MVC</span><span class="sxs-lookup"><span data-stu-id="ad0df-211">C# MVC</span></span>](xref:samesite/csMVC)
* [<span data-ttu-id="ad0df-212">C# WebForms</span><span class="sxs-lookup"><span data-stu-id="ad0df-212">C# WebForms</span></span>](xref:samesite/CSharpWebForms)
* [<span data-ttu-id="ad0df-213">VB WebForms</span><span class="sxs-lookup"><span data-stu-id="ad0df-213">VB WebForms</span></span>](xref:samesite/vbWF)
* [<span data-ttu-id="ad0df-214">VB MVC</span><span class="sxs-lookup"><span data-stu-id="ad0df-214">VB MVC</span></span>](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a><span data-ttu-id="ad0df-215">사이트가 HTTPS로 리디렉션 되는지 확인</span><span class="sxs-lookup"><span data-stu-id="ad0df-215">Ensuring your site redirects to HTTPS</span></span>

<span data-ttu-id="ad0df-216">ASP.NET 4. x, WebForms 및 MVC의 경우 [IIS의 URL 재작성](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) 기능을 사용 하 여 모든 요청을 HTTPS로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-216">For ASP.NET 4.x, WebForms and MVC, [IIS's URL Rewrite](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) feature can be used to redirect all requests to HTTPS.</span></span> <span data-ttu-id="ad0df-217">다음 XML에서는 샘플 규칙을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-217">The following XML shows a sample rule:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="ad0df-218">[IIS URL 재작성](https://www.iis.net/downloads/microsoft/url-rewrite) 의 온-프레미스 설치는 설치 해야 할 수 있는 선택적 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-218">In on-premises installations of [IIS URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) is an optional feature that may need installing.</span></span>

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="ad0df-219">SameSite 문제에 대 한 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="ad0df-219">Test apps for SameSite problems</span></span>

<span data-ttu-id="ad0df-220">지원 되는 브라우저를 사용 하 여 앱을 테스트 하 고 쿠키를 포함 하는 시나리오를 진행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-220">You must test your app with the browsers you support and go through your scenarios that involve cookies.</span></span> <span data-ttu-id="ad0df-221">쿠키 시나리오는 일반적으로 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-221">Cookie scenarios typically involve</span></span>

* <span data-ttu-id="ad0df-222">로그인 양식</span><span class="sxs-lookup"><span data-stu-id="ad0df-222">Login forms</span></span>
* <span data-ttu-id="ad0df-223">Facebook, Azure AD, OAuth 및 OIDC와 같은 외부 로그인 메커니즘</span><span class="sxs-lookup"><span data-stu-id="ad0df-223">External login mechanisms such as Facebook, Azure AD, OAuth and OIDC</span></span>
* <span data-ttu-id="ad0df-224">다른 사이트의 요청을 수락 하는 페이지</span><span class="sxs-lookup"><span data-stu-id="ad0df-224">Pages that accept requests from other sites</span></span>
* <span data-ttu-id="ad0df-225">Iframe에 포함 되도록 설계 된 앱의 페이지</span><span class="sxs-lookup"><span data-stu-id="ad0df-225">Pages in your app designed to be embedded in iframes</span></span>

<span data-ttu-id="ad0df-226">앱에서 쿠키가 올바르게 생성, 유지 및 삭제 되었는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-226">You should check that cookies are created, persisted and deleted correctly in your app.</span></span>

<span data-ttu-id="ad0df-227">타사 로그인을 통해와 같은 원격 사이트와 상호 작용 하는 앱은 다음 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-227">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="ad0df-228">여러 브라우저에서 상호 작용을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-228">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="ad0df-229">이 문서에서 설명 [하는 브라우저 검색 및 완화](#sob) 를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-229">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="ad0df-230">새 SameSite 동작을 옵트인 (opt in) 할 수 있는 클라이언트 버전을 사용 하 여 웹 앱을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-230">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="ad0df-231">Chrome, Firefox 및 Chromium Edge 모두에는 테스트에 사용할 수 있는 새로운 옵트인 기능 플래그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-231">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="ad0df-232">앱이 SameSite 패치를 적용 한 후 이전 클라이언트 버전, 특히 Safari를 사용 하 여 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-232">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="ad0df-233">자세한 내용은이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-233">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="ad0df-234">Chrome으로 테스트</span><span class="sxs-lookup"><span data-stu-id="ad0df-234">Test with Chrome</span></span>

<span data-ttu-id="ad0df-235">Chrome 78 +는 일시적인 완화를 제공 하기 때문에 잘못 된 결과를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-235">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="ad0df-236">Chrome 78 + 임시 완화를 사용 하면 쿠키가 2 분 이내에 이전 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-236">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="ad0df-237">적절 한 테스트 플래그가 설정 된 Chrome 76 또는 77은 보다 정확한 결과를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-237">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="ad0df-238">새 SameSite 동작을 테스트 하려면 `chrome://flags/#same-site-by-default-cookies` **사용**으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-238">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="ad0df-239">이전 버전의 Chrome (75 및 아래)은 새 설정으로 인해 실패 하는 것으로 보고 됩니다 `None` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-239">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="ad0df-240">이 문서의 [이전 브라우저 지원](#sob) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-240">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="ad0df-241">Google은 이전 chrome 버전을 사용할 수 없도록 설정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-241">Google does not make older chrome versions available.</span></span> <span data-ttu-id="ad0df-242">[Chromium 다운로드](https://www.chromium.org/getting-involved/download-chromium) 의 지침에 따라 이전 버전의 Chrome을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-242">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="ad0df-243">이전 버전의 chrome을 검색 하 여 제공 된 링크에서 Chrome을 다운로드 **하지** 마세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-243">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="ad0df-244">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="ad0df-244">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="ad0df-245">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="ad0df-245">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* <span data-ttu-id="ad0df-246">64 비트 버전의 Windows를 사용 하지 않는 경우 [OmahaProxy viewer](https://omahaproxy.appspot.com/) 를 사용 하 여 [Chromium에서 제공](https://www.chromium.org/getting-involved/download-chromium)하는 지침을 사용 하 여 Chrome 74 (v 74.0.3729.108)에 해당 하는 Chromium 분기를 조회할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-246">If you're not using a 64bit version of Windows you can use the [OmahaProxy viewer](https://omahaproxy.appspot.com/) to look up which Chromium branch corresponds to Chrome 74 (v74.0.3729.108) using the [instructions provided by Chromium](https://www.chromium.org/getting-involved/download-chromium).</span></span>

<span data-ttu-id="ad0df-247">카나리아 버전부터 `80.0.3975.0` 완화 된 + 사후 임시 완화는 새 플래그를 사용 하 여 테스트 목적으로 사용 하지 않도록 설정 하 여 `--enable-features=SameSiteDefaultChecksMethodRigorously` 완화가 제거 된 기능의 최종 종료 상태에서 사이트 및 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-247">Starting in Canary version `80.0.3975.0`, the Lax+POST temporary mitigation can be disabled for testing purposes using the new flag `--enable-features=SameSiteDefaultChecksMethodRigorously` to allow testing of sites and services in the eventual end state of the feature where the mitigation has been removed.</span></span> <span data-ttu-id="ad0df-248">자세한 내용은 Chromium Projects [SameSite Updates](https://www.chromium.org/updates/same-site) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-248">For more information, see The Chromium Projects [SameSite Updates](https://www.chromium.org/updates/same-site)</span></span>

#### <a name="test-with-chrome-80"></a><span data-ttu-id="ad0df-249">Chrome 80 이상으로 테스트</span><span class="sxs-lookup"><span data-stu-id="ad0df-249">Test with Chrome 80+</span></span>

<span data-ttu-id="ad0df-250">새 특성을 지 원하는 Chrome 버전을 [다운로드](https://www.google.com/chrome/) 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-250">[Download](https://www.google.com/chrome/) a version of Chrome that supports their new attribute.</span></span> <span data-ttu-id="ad0df-251">작성 시점에 현재 버전은 Chrome 80입니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-251">At the time of writing, the current version is Chrome 80.</span></span> <span data-ttu-id="ad0df-252">Chrome 80 `chrome://flags/#same-site-by-default-cookies` 에는 새 동작을 사용 하기 위해 플래그를 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-252">Chrome 80 needs the flag `chrome://flags/#same-site-by-default-cookies` enabled to use the new behavior.</span></span> <span data-ttu-id="ad0df-253">또한 ()을 사용 하도록 설정 `chrome://flags/#cookies-without-same-site-must-be-secure` 하 여 sameSite 특성이 활성화 되지 않은 쿠키의 예정 된 동작을 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-253">You should also enable (`chrome://flags/#cookies-without-same-site-must-be-secure`) to test the upcoming behavior for cookies which have no sameSite attribute enabled.</span></span> <span data-ttu-id="ad0df-254">Chrome 80는 `SameSite=Lax` 특정 요청에 대 한 유예 기간이 정해진 경우를 제외 하 고는 특성이 없는 쿠키를로 처리 하는 스위치를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-254">Chrome 80 is on target to make the switch to treat cookies without the attribute as `SameSite=Lax`, albeit with a timed grace period for certain requests.</span></span> <span data-ttu-id="ad0df-255">시간이 지정 된 유예 기간을 사용 하지 않도록 설정 하려면 다음 명령줄 인수를 사용 하 여 Chrome 80을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-255">To disable the timed grace period Chrome 80 can be launched with the following command line argument:</span></span>

`--enable-features=SameSiteDefaultChecksMethodRigorously`

<span data-ttu-id="ad0df-256">Chrome 80에는 브라우저 콘솔에 누락 된 sameSite 특성에 대 한 경고 메시지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-256">Chrome 80 has warning messages in the browser console about missing sameSite attributes.</span></span> <span data-ttu-id="ad0df-257">F12 키를 사용 하 여 브라우저 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-257">Use F12 to open the browser console.</span></span>

### <a name="test-with-safari"></a><span data-ttu-id="ad0df-258">Safari를 사용 하 여 테스트</span><span class="sxs-lookup"><span data-stu-id="ad0df-258">Test with Safari</span></span>

<span data-ttu-id="ad0df-259">Safari 12는 이전 초안을 엄격 하 게 구현 했으며 새 `None` 값이 쿠키에 있는 경우 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-259">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="ad0df-260">`None` 이 문서에서 [이전 브라우저를 지 원하는](#sob) 브라우저 검색 코드를 통해가 방지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-260">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="ad0df-261">MSAL, ADAL 또는 사용 중인 라이브러리를 사용 하 여 Safari 12, Safari 13 및 WebKit 기반 OS 스타일 로그인을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-261">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="ad0df-262">문제는 기본 OS 버전에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-262">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="ad0df-263">OSX Mojave (10.14) 및 iOS 12는 새로운 SameSite 동작의 호환성 문제를 해결 하는 것으로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-263">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="ad0df-264">OS를 OSX Catalina.properties (10.15) 또는 iOS 13로 업그레이드 하면 문제가 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-264">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="ad0df-265">Safari에는 현재 새 사양 동작 테스트를 위한 옵트인 플래그가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-265">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="ad0df-266">Firefox로 테스트</span><span class="sxs-lookup"><span data-stu-id="ad0df-266">Test with Firefox</span></span>

<span data-ttu-id="ad0df-267">새 표준에 대 한 Firefox 지원은 기능 플래그를 사용 하 여 페이지에서 옵트인 하 여 버전 68 이상에서 테스트할 수 있습니다 `about:config` `network.cookie.sameSite.laxByDefault` .</span><span class="sxs-lookup"><span data-stu-id="ad0df-267">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="ad0df-268">이전 버전의 Firefox와의 호환성 문제에 대 한 보고서가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-268">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-legacy-browser"></a><span data-ttu-id="ad0df-269">Edge (레거시) 브라우저를 사용 하 여 테스트</span><span class="sxs-lookup"><span data-stu-id="ad0df-269">Test with Edge (Legacy) browser</span></span>

<span data-ttu-id="ad0df-270">Edge는 이전 SameSite 표준을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-270">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="ad0df-271">Edge 버전 44 이상에는 새 표준에 대 한 알려진 호환성 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-271">Edge version 44+ doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="ad0df-272">Edge를 사용 하 여 테스트 (Chromium)</span><span class="sxs-lookup"><span data-stu-id="ad0df-272">Test with Edge (Chromium)</span></span>

<span data-ttu-id="ad0df-273">SameSite 플래그는 페이지에 설정 되어 `edge://flags/#same-site-by-default-cookies` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-273">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="ad0df-274">Edge Chromium에서 호환성 문제가 검색 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-274">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="ad0df-275">전자로 테스트</span><span class="sxs-lookup"><span data-stu-id="ad0df-275">Test with Electron</span></span>

<span data-ttu-id="ad0df-276">Electron 버전에는 이전 버전의 Chromium이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-276">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="ad0df-277">예를 들어 팀에서 사용 하는 전자의 버전은 Chromium 66 이며,이는 이전 동작을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-277">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="ad0df-278">제품에서 사용 하는 전자 제품 버전으로 고유한 호환성 테스트를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-278">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="ad0df-279">[이전 브라우저 지원](#sob)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0df-279">See [Supporting older browsers](#sob).</span></span>

## <a name="reverting-samesite-patches"></a><span data-ttu-id="ad0df-280">SameSite 패치 되돌리기</span><span class="sxs-lookup"><span data-stu-id="ad0df-280">Reverting SameSite patches</span></span>

<span data-ttu-id="ad0df-281">.NET Framework 앱의 업데이트 된 sameSite 동작을의 값에 대 한 sameSite 특성을 내보내지 않는 이전 동작으로 되돌릴 수 있으며 `None` ,이 값을 내보내지 않도록 인증 및 세션 쿠키를 되돌릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-281">You can revert the updated sameSite behavior in .NET Framework apps to its previous behavior where the sameSite attribute is not emitted for a value of `None`, and revert the authentication and session cookies to not emit the value.</span></span> <span data-ttu-id="ad0df-282">이는 표준에 대 한 변경 내용을 지 원하는 브라우저를 사용 하 여 사용자에 대 한 외부 POST 요청 또는 인증을 중단 하기 때문에 *매우 임시 수정*으로 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-282">This should be viewed as an *extremely temporary fix*, as the Chrome changes will break any external POST requests or authentication for users using browsers which support the changes to the standard.</span></span>

### <a name="reverting-net-472-behavior"></a><span data-ttu-id="ad0df-283">.NET 4.7.2 동작 되돌리기</span><span class="sxs-lookup"><span data-stu-id="ad0df-283">Reverting .NET 4.7.2 behavior</span></span>

<span data-ttu-id="ad0df-284">다음 구성 설정을 포함 하도록 *web.config* 를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0df-284">Update *web.config* to include the following configuration settings:</span></span>

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a><span data-ttu-id="ad0df-285">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ad0df-285">Additional resources</span></span>

* [<span data-ttu-id="ad0df-286">ASP.NET 및 ASP.NET Core의 예정 된 SameSite 쿠키 변경 내용</span><span class="sxs-lookup"><span data-stu-id="ad0df-286">Upcoming SameSite Cookie Changes in ASP.NET and ASP.NET Core</span></span>](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [<span data-ttu-id="ad0df-287">SameSite 및 "SameSite = None; 테스트 및 디버깅에 대 한 팁 보안 "쿠키</span><span class="sxs-lookup"><span data-stu-id="ad0df-287">Tips for testing and debugging SameSite-by-default and “SameSite=None; Secure” cookies</span></span>](https://www.chromium.org/updates/same-site/test-debug)
* [<span data-ttu-id="ad0df-288">Chromium 블로그: 개발자: 새 SameSite를 사용할 준비가 되었습니다. 보안 쿠키 설정</span><span class="sxs-lookup"><span data-stu-id="ad0df-288">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="ad0df-289">SameSite 쿠키 설명</span><span class="sxs-lookup"><span data-stu-id="ad0df-289">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="ad0df-290">Chrome 업데이트</span><span class="sxs-lookup"><span data-stu-id="ad0df-290">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)
* [<span data-ttu-id="ad0df-291">.NET SameSite 패치</span><span class="sxs-lookup"><span data-stu-id="ad0df-291">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)
* [<span data-ttu-id="ad0df-292">Azure 웹 응용 프로그램 동일한 사이트 정보</span><span class="sxs-lookup"><span data-stu-id="ad0df-292">Azure Web Applications Same Site Information</span></span>](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [<span data-ttu-id="ad0df-293">Azure ActiveDirectory 동일한 사이트 정보</span><span class="sxs-lookup"><span data-stu-id="ad0df-293">Azure ActiveDirectory Same Site Information</span></span>](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
