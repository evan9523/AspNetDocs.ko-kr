---
title: ASP.NET Core의 부분 보기
author: ardalis
description: 부분 보기를 사용하여 큰 태그 파일을 나누고 ASP.NET Core 앱의 웹 페이지에서 공통 태그의 중복을 줄이는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 09/11/2018
uid: mvc/views/partial
ms.openlocfilehash: ff4b99580990edbd768128d77214e664a1e29e56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033300"
---
# <a name="partial-views-in-aspnet-core"></a><span data-ttu-id="39cad-103">ASP.NET Core의 부분 보기</span><span class="sxs-lookup"><span data-stu-id="39cad-103">Partial views in ASP.NET Core</span></span>

<span data-ttu-id="39cad-104">작성자: [Steve Smith](https://ardalis.com/), [Luke Latham](https://github.com/guardrex), [Maher JENDOUBI](https://twitter.com/maherjend), [Rick Anderson](https://twitter.com/RickAndMSFT), [Scott Sauber](https://twitter.com/scottsauber)</span><span class="sxs-lookup"><span data-stu-id="39cad-104">By [Steve Smith](https://ardalis.com/), [Luke Latham](https://github.com/guardrex), [Maher JENDOUBI](https://twitter.com/maherjend), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Scott Sauber](https://twitter.com/scottsauber)</span></span>

<span data-ttu-id="39cad-105">부분 보기는 다른 태그 파일의 렌더링된 출력  *내에서* HTML 출력을 렌더링하는 [Razor](xref:mvc/views/razor) 태그 파일(*.cshtml*)입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-105">A partial view is a [Razor](xref:mvc/views/razor) markup file (*.cshtml*) that renders HTML output *within* another markup file's rendered output.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="39cad-106">‘부분 보기’라는 용어는 MVC 앱(여기서 태그 파일을 ‘보기’라고 함) 또는 Razor Pages 앱(여기서 태그 파일을 ‘페이지’라고 함)을 개발하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-106">The term *partial view* is used when developing either an MVC app, where markup files are called *views*, or a Razor Pages app, where markup files are called *pages*.</span></span> <span data-ttu-id="39cad-107">이 주제에서는 일반적으로 MVC 보기 및 Razor Pages 페이지를 ‘태그 파일’로 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-107">This topic generically refers to MVC views and Razor Pages pages as *markup files*.</span></span>

::: moniker-end

<span data-ttu-id="39cad-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="39cad-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-partial-views"></a><span data-ttu-id="39cad-109">부분 보기를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="39cad-109">When to use partial views</span></span>

<span data-ttu-id="39cad-110">부분 보기는 다음을 수행하는 효과적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-110">Partial views are an effective way to:</span></span>

* <span data-ttu-id="39cad-111">큰 태그 파일을 작은 구성 요소로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-111">Break up large markup files into smaller components.</span></span>

  <span data-ttu-id="39cad-112">여러 논리적 조각으로 구성된 크고 복잡한 태그 파일에서는 부분 보기로 구분된 각 부분에 대해 작업하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-112">In a large, complex markup file composed of several logical pieces, there's an advantage to working with each piece isolated into a partial view.</span></span> <span data-ttu-id="39cad-113">태그에는 전체 페이지 구조와 부분 보기에 대한 참조만 포함되므로 태그 파일의 코드는 관리 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-113">The code in the markup file is manageable because the markup only contains the overall page structure and references to partial views.</span></span>
* <span data-ttu-id="39cad-114">태그 파일에서 공통 태그 콘텐츠의 중복을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-114">Reduce the duplication of common markup content across markup files.</span></span>

  <span data-ttu-id="39cad-115">태그 파일에서 동일한 태그 요소가 사용되면 부분 보기가 태그 콘텐츠의 중복을 하나의 부분 보기 파일로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-115">When the same markup elements are used across markup files, a partial view removes the duplication of markup content into one partial view file.</span></span> <span data-ttu-id="39cad-116">부분 보기에서 태그가 변경되면 부분 보기를 사용하는 태그 파일의 렌더링된 출력을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-116">When the markup is changed in the partial view, it updates the rendered output of the markup files that use the partial view.</span></span>

<span data-ttu-id="39cad-117">부분 보기는 일반 레이아웃 요소를 유지 관리하는 데 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-117">Partial views shouldn't be used to maintain common layout elements.</span></span> <span data-ttu-id="39cad-118">일반 레이아웃 요소는 [_Layout.cshtml](xref:mvc/views/layout) 파일에서 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-118">Common layout elements should be specified in [_Layout.cshtml](xref:mvc/views/layout) files.</span></span>

<span data-ttu-id="39cad-119">태그를 렌더링하려면 복잡한 렌더링 논리 또는 코드 실행이 필요한 부분 보기를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="39cad-119">Don't use a partial view where complex rendering logic or code execution is required to render the markup.</span></span> <span data-ttu-id="39cad-120">부분 보기 대신 [보기 구성 요소](xref:mvc/views/view-components)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-120">Instead of a partial view, use a [view component](xref:mvc/views/view-components).</span></span>

## <a name="declare-partial-views"></a><span data-ttu-id="39cad-121">부분 보기 선언</span><span class="sxs-lookup"><span data-stu-id="39cad-121">Declare partial views</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="39cad-122">부분 보기는 ‘보기’ 폴더(MVC) 또는 *Pages* 폴더(Razor Pages)에서 유지 관리되는 *.cshtml* 태그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-122">A partial view is a *.cshtml* markup file maintained within the *Views* folder (MVC) or *Pages* folder (Razor Pages).</span></span>

<span data-ttu-id="39cad-123">ASP.NET Core MVC에서 컨트롤러의 <xref:Microsoft.AspNetCore.Mvc.ViewResult>는 보기 또는 부분 보기를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-123">In ASP.NET Core MVC, a controller's <xref:Microsoft.AspNetCore.Mvc.ViewResult> is capable of returning either a view or a partial view.</span></span> <span data-ttu-id="39cad-124">비슷한 기능이 ASP.NET Core 2.2의 Razor Pages에 대해 계획되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-124">An analogous capability is planned for Razor Pages in ASP.NET Core 2.2.</span></span> <span data-ttu-id="39cad-125">Razor Pages에서 <xref:Microsoft.AspNetCore.Mvc.RazorPages.PageModel>은 <xref:Microsoft.AspNetCore.Mvc.PartialViewResult>를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-125">In Razor Pages, a <xref:Microsoft.AspNetCore.Mvc.RazorPages.PageModel> can return a <xref:Microsoft.AspNetCore.Mvc.PartialViewResult>.</span></span> <span data-ttu-id="39cad-126">부분 보기 참조 및 렌더링은 [부분 보기 참조](#reference-a-partial-view) 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-126">Referencing and rendering partial views is described in the [Reference a partial view](#reference-a-partial-view) section.</span></span>

<span data-ttu-id="39cad-127">MVC 보기 또는 페이지 렌더링과 달리 부분 보기는 *_ViewStart.cshtml*을 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-127">Unlike MVC view or page rendering, a partial view doesn't run *_ViewStart.cshtml*.</span></span> <span data-ttu-id="39cad-128">*_ViewStart.cshtml*에 대한 자세한 내용은 <xref:mvc/views/layout>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39cad-128">For more information on *_ViewStart.cshtml*, see <xref:mvc/views/layout>.</span></span>

<span data-ttu-id="39cad-129">부분 보기 파일 이름은 종종 밑줄(`_`)로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-129">Partial view file names often begin with an underscore (`_`).</span></span> <span data-ttu-id="39cad-130">이 명명 규칙은 필수는 아니지만 부분 보기를 보기 및 페이지와 시각적으로 구분하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-130">This naming convention isn't required, but it helps to visually differentiate partial views from views and pages.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="39cad-131">부분 보기는 ‘보기’ 폴더에서 유지 관리되는 *.cshtml* 태그 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-131">A partial view is a *.cshtml* markup file maintained within the *Views* folder.</span></span>

<span data-ttu-id="39cad-132">컨트롤러의 <xref:Microsoft.AspNetCore.Mvc.ViewResult>는 보기 또는 부분 보기를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-132">A controller's <xref:Microsoft.AspNetCore.Mvc.ViewResult> is capable of returning either a view or a partial view.</span></span>

<span data-ttu-id="39cad-133">MVC 보기 렌더링과 달리 부분 보기는 *_ViewStart.cshtml*을 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-133">Unlike MVC view rendering, a partial view doesn't run *_ViewStart.cshtml*.</span></span> <span data-ttu-id="39cad-134">*_ViewStart.cshtml*에 대한 자세한 내용은 <xref:mvc/views/layout>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39cad-134">For more information on *_ViewStart.cshtml*, see <xref:mvc/views/layout>.</span></span>

<span data-ttu-id="39cad-135">부분 보기 파일 이름은 종종 밑줄(`_`)로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-135">Partial view file names often begin with an underscore (`_`).</span></span> <span data-ttu-id="39cad-136">이 명명 규칙은 필수는 아니지만 부분 보기를 보기와 시각적으로 구분하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-136">This naming convention isn't required, but it helps to visually differentiate partial views from views.</span></span>

::: moniker-end

## <a name="reference-a-partial-view"></a><span data-ttu-id="39cad-137">부분 보기 참조</span><span class="sxs-lookup"><span data-stu-id="39cad-137">Reference a partial view</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="39cad-138">태그 파일 내에서 부분 보기를 참조할 수 있는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-138">Within a markup file, there are several ways to reference a partial view.</span></span> <span data-ttu-id="39cad-139">앱에서 다음과 같은 비동기 렌더링 방법 중 하나를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-139">We recommend that apps use one of the following asynchronous rendering approaches:</span></span>

* [<span data-ttu-id="39cad-140">부분 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="39cad-140">Partial Tag Helper</span></span>](#partial-tag-helper)
* [<span data-ttu-id="39cad-141">비동기 HTML 도우미</span><span class="sxs-lookup"><span data-stu-id="39cad-141">Asynchronous HTML Helper</span></span>](#asynchronous-html-helper)

::: moniker-end

::: moniker range="< aspnetcore-2.1"

<span data-ttu-id="39cad-142">태그 파일 내에서 부분 보기를 참조할 수 있는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-142">Within a markup file, there are two ways to reference a partial view:</span></span>

* [<span data-ttu-id="39cad-143">비동기 HTML 도우미</span><span class="sxs-lookup"><span data-stu-id="39cad-143">Asynchronous HTML Helper</span></span>](#asynchronous-html-helper)
* [<span data-ttu-id="39cad-144">동기 HTML 도우미</span><span class="sxs-lookup"><span data-stu-id="39cad-144">Synchronous HTML Helper</span></span>](#synchronous-html-helper)

<span data-ttu-id="39cad-145">앱에서 [비동기 HTML 도우미](#asynchronous-html-helper)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-145">We recommend that apps use the [Asynchronous HTML Helper](#asynchronous-html-helper).</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

### <a name="partial-tag-helper"></a><span data-ttu-id="39cad-146">부분 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="39cad-146">Partial Tag Helper</span></span>

<span data-ttu-id="39cad-147">[부분 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)에는 ASP.NET Core 2.1 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-147">The [Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper) requires ASP.NET Core 2.1 or later.</span></span>

<span data-ttu-id="39cad-148">부분 태그 도우미는 콘텐츠를 비동기식으로 렌더링하며 HTML 같은 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-148">The Partial Tag Helper renders content asynchronously and uses an HTML-like syntax:</span></span>

```cshtml
<partial name="_PartialName" />
```

<span data-ttu-id="39cad-149">파일 확장자가 있는 경우 태그 도우미는 부분 보기를 호출하는 태그 파일과 동일한 폴더에 있어야 하는 부분 보기를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-149">When a file extension is present, the Tag Helper references a partial view that must be in the same folder as the markup file calling the partial view:</span></span>

```cshtml
<partial name="_PartialName.cshtml" />
```

<span data-ttu-id="39cad-150">다음 예제에서는 앱 루트의 부분 보기를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-150">The following example references a partial view from the app root.</span></span> <span data-ttu-id="39cad-151">물결표-슬래시(`~/`) 또는 슬래시(`/`)로 시작되는 경로는 앱 루트를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-151">Paths that start with a tilde-slash (`~/`) or a slash (`/`) refer to the app root:</span></span>

<span data-ttu-id="39cad-152">**Razor 페이지**</span><span class="sxs-lookup"><span data-stu-id="39cad-152">**Razor Pages**</span></span>

```cshtml
<partial name="~/Pages/Folder/_PartialName.cshtml" />
<partial name="/Pages/Folder/_PartialName.cshtml" />
```

<span data-ttu-id="39cad-153">**MVC**</span><span class="sxs-lookup"><span data-stu-id="39cad-153">**MVC**</span></span>

```cshtml
<partial name="~/Views/Folder/_PartialName.cshtml" />
<partial name="/Views/Folder/_PartialName.cshtml" />
```

<span data-ttu-id="39cad-154">다음 예제는 상대 경로가 있는 부분 보기를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-154">The following example references a partial view with a relative path:</span></span>

```cshtml
<partial name="../Account/_PartialName.cshtml" />
```

<span data-ttu-id="39cad-155">자세한 내용은 <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39cad-155">For more information, see <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>.</span></span>

::: moniker-end

### <a name="asynchronous-html-helper"></a><span data-ttu-id="39cad-156">비동기 HTML 도우미</span><span class="sxs-lookup"><span data-stu-id="39cad-156">Asynchronous HTML Helper</span></span>

<span data-ttu-id="39cad-157">HTML 도우미를 사용할 때 가장 좋은 방법은 <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.PartialAsync*>를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-157">When using an HTML Helper, the best practice is to use <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.PartialAsync*>.</span></span> <span data-ttu-id="39cad-158">`PartialAsync`는 <xref:System.Threading.Tasks.Task`1>에 래핑된 <xref:Microsoft.AspNetCore.Html.IHtmlContent> 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-158">`PartialAsync` returns an <xref:Microsoft.AspNetCore.Html.IHtmlContent> type wrapped in a <xref:System.Threading.Tasks.Task`1>.</span></span> <span data-ttu-id="39cad-159">대기된 호출 접두사로 `@` 문자를 사용하여 메서드를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-159">The method is referenced by prefixing the awaited call with an `@` character:</span></span>

```cshtml
@await Html.PartialAsync("_PartialName")
```

<span data-ttu-id="39cad-160">파일 확장자가 있는 경우 HTML 도우미는 부분 보기를 호출하는 태그 파일과 동일한 폴더에 있어야 하는 부분 보기를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-160">When the file extension is present, the HTML Helper references a partial view that must be in the same folder as the markup file calling the partial view:</span></span>

```cshtml
@await Html.PartialAsync("_PartialName.cshtml")
```

<span data-ttu-id="39cad-161">다음 예제에서는 앱 루트의 부분 보기를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-161">The following example references a partial view from the app root.</span></span> <span data-ttu-id="39cad-162">물결표-슬래시(`~/`) 또는 슬래시(`/`)로 시작되는 경로는 앱 루트를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-162">Paths that start with a tilde-slash (`~/`) or a slash (`/`) refer to the app root:</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="39cad-163">**Razor 페이지**</span><span class="sxs-lookup"><span data-stu-id="39cad-163">**Razor Pages**</span></span>

```cshtml
@await Html.PartialAsync("~/Pages/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Pages/Folder/_PartialName.cshtml")
```

<span data-ttu-id="39cad-164">**MVC**</span><span class="sxs-lookup"><span data-stu-id="39cad-164">**MVC**</span></span>

::: moniker-end

```cshtml
@await Html.PartialAsync("~/Views/Folder/_PartialName.cshtml")
@await Html.PartialAsync("/Views/Folder/_PartialName.cshtml")
```

<span data-ttu-id="39cad-165">다음 예제는 상대 경로가 있는 부분 보기를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-165">The following example references a partial view with a relative path:</span></span>

```cshtml
@await Html.PartialAsync("../Account/_LoginPartial.cshtml")
```

<span data-ttu-id="39cad-166">또는 <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartialAsync*>를 사용하여 부분 보기를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-166">Alternatively, you can render a partial view with <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartialAsync*>.</span></span> <span data-ttu-id="39cad-167">이 메서드는 <xref:Microsoft.AspNetCore.Html.IHtmlContent>를 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-167">This method doesn't return an <xref:Microsoft.AspNetCore.Html.IHtmlContent>.</span></span> <span data-ttu-id="39cad-168">렌더링된 출력을 응답에 직접 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-168">It streams the rendered output directly to the response.</span></span> <span data-ttu-id="39cad-169">이 메서드는 결과를 반환하지 않기 때문에 Razor 코드 블록 내에서 호출되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-169">Because the method doesn't return a result, it must be called within a Razor code block:</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_RenderPartialAsync)]

<span data-ttu-id="39cad-170">`RenderPartialAsync` 스트림은 콘텐츠를 렌더링했으므로 일부 시나리오에서 더 나은 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-170">Since `RenderPartialAsync` streams rendered content, it provides better performance in some scenarios.</span></span> <span data-ttu-id="39cad-171">성능이 중요한 상황에서는 두 가지 방법을 모두 사용하여 페이지를 벤치마크하고 빠른 응답을 생성하는 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-171">In performance-critical situations, benchmark the page using both approaches and use the approach that generates a faster response.</span></span>

### <a name="synchronous-html-helper"></a><span data-ttu-id="39cad-172">동기 HTML 도우미</span><span class="sxs-lookup"><span data-stu-id="39cad-172">Synchronous HTML Helper</span></span>

<span data-ttu-id="39cad-173">`PartialAsync` 및 `RenderPartialAsync`의 해당하는 동기 항목은 각각 <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.Partial*> 및 <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartial*>입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-173"><xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.Partial*> and <xref:Microsoft.AspNetCore.Mvc.Rendering.HtmlHelperPartialExtensions.RenderPartial*> are the synchronous equivalents of `PartialAsync` and `RenderPartialAsync`, respectively.</span></span> <span data-ttu-id="39cad-174">교착 상태인 시나리오가 있으므로 동기 해당 항목을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-174">The synchronous equivalents aren't recommended because there are scenarios in which they deadlock.</span></span> <span data-ttu-id="39cad-175">동기 메서드는 이후 릴리스에서 제거 대상으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-175">The synchronous methods are targeted for removal in a future release.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39cad-176">코드를 실행해야 하는 경우 부분 보기 대신 [보기 구성 요소](xref:mvc/views/view-components)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-176">If you need to execute code, use a [view component](xref:mvc/views/view-components) instead of a partial view.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="39cad-177">`Partial` 또는 `RenderPartial` 호출 시 Visual Studio 분석기 경고가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-177">Calling `Partial` or `RenderPartial` results in a Visual Studio analyzer warning.</span></span> <span data-ttu-id="39cad-178">예를 들어 `Partial`의 존재는 다음 경고 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-178">For example, the presence of `Partial` yields the following warning message:</span></span>

> <span data-ttu-id="39cad-179">IHtmlHelper.Partial 사용 시 애플리케이션이 교착 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-179">Use of IHtmlHelper.Partial may result in application deadlocks.</span></span> <span data-ttu-id="39cad-180">&lt;부분&gt; 태그 도우미 또는 IHtmlHelper.PartialAsync를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="39cad-180">Consider using &lt;partial&gt; Tag Helper or IHtmlHelper.PartialAsync.</span></span>

<span data-ttu-id="39cad-181">`@Html.Partial` 호출을 `@await Html.PartialAsync` 또는 [부분 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-181">Replace calls to `@Html.Partial` with `@await Html.PartialAsync` or the [Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper).</span></span> <span data-ttu-id="39cad-182">부분 태그 도우미 마이그레이션에 대한 자세한 내용은 [HTML 도우미에서 마이그레이션](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper#migrate-from-an-html-helper)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-182">For more information on Partial Tag Helper migration, see [Migrate from an HTML Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper#migrate-from-an-html-helper).</span></span>

::: moniker-end

## <a name="partial-view-discovery"></a><span data-ttu-id="39cad-183">부분 보기 검색</span><span class="sxs-lookup"><span data-stu-id="39cad-183">Partial view discovery</span></span>

<span data-ttu-id="39cad-184">파일 확장자 없는 이름으로 부분 보기를 참조하는 경우, 다음 위치가 명시된 순서로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-184">When a partial view is referenced by name without a file extension, the following locations are searched in the stated order:</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="39cad-185">**Razor 페이지**</span><span class="sxs-lookup"><span data-stu-id="39cad-185">**Razor Pages**</span></span>

1. <span data-ttu-id="39cad-186">현재 페이지의 폴더를 실행 중</span><span class="sxs-lookup"><span data-stu-id="39cad-186">Currently executing page's folder</span></span>
1. <span data-ttu-id="39cad-187">페이지의 폴더 위에 있는 디렉터리 그래프</span><span class="sxs-lookup"><span data-stu-id="39cad-187">Directory graph above the page's folder</span></span>
1. `/Shared`
1. `/Pages/Shared`
1. `/Views/Shared`

<span data-ttu-id="39cad-188">**MVC**</span><span class="sxs-lookup"><span data-stu-id="39cad-188">**MVC**</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
1. `/Areas/<Area-Name>/Views/Shared`
1. `/Views/Shared`
1. `/Pages/Shared`

::: moniker-end

::: moniker range="< aspnetcore-2.0"

1. `/Areas/<Area-Name>/Views/<Controller-Name>`
1. `/Areas/<Area-Name>/Views/Shared`
1. `/Views/Shared`

::: moniker-end

<span data-ttu-id="39cad-189">다음 규칙이 부분 보기 검색에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-189">The following conventions apply to partial view discovery:</span></span>

* <span data-ttu-id="39cad-190">부분 보기가 다른 폴더에 있는 경우 파일 이름이 같은 다른 부분 보기가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-190">Different partial views with the same file name are allowed when the partial views are in different folders.</span></span>
* <span data-ttu-id="39cad-191">파일 확장명 없는 이름으로 부분 보기를 참조할 때 부분 보기가 호출자의 폴더와 ‘공유’ 폴더에 모두 있는 경우 호출자 폴더에 있는 부분 보기가 부분 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-191">When referencing a partial view by name without a file extension and the partial view is present in both the caller's folder and the *Shared* folder, the partial view in the caller's folder supplies the partial view.</span></span> <span data-ttu-id="39cad-192">호출자의 폴더에 부분 보기가 없는 경우 부분 보기는 ‘공유’ 폴더에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-192">If the partial view isn't present in the caller's folder, the partial view is provided from the *Shared* folder.</span></span> <span data-ttu-id="39cad-193">‘공유’ 폴더의 부분 보기를 ‘공유 부분 보기’ 또는 ‘기본 부분 보기’라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-193">Partial views in the *Shared* folder are called *shared partial views* or *default partial views*.</span></span>
* <span data-ttu-id="39cad-194">부분 보기는 ‘연결’ 가능하며, 순환 참조가 호출에 의해 형성되지 않는 경우 다른 부분 보기를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-194">Partial views can be *chained*&mdash;a partial view can call another partial view if a circular reference isn't formed by the calls.</span></span> <span data-ttu-id="39cad-195">상대 경로는 항상, 파일의 루트 또는 부모가 아닌 현재 파일에 상대적입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-195">Relative paths are always relative to the current file, not to the root or parent of the file.</span></span>

> [!NOTE]
> <span data-ttu-id="39cad-196">부분 보기에 정의된 [Razor](xref:mvc/views/razor) `section`은 부모 태그 파일에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-196">A [Razor](xref:mvc/views/razor) `section` defined in a partial view is invisible to parent markup files.</span></span> <span data-ttu-id="39cad-197">`section`만 정의되어 있는 부분 보기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-197">The `section` is only visible to the partial view in which it's defined.</span></span>

## <a name="access-data-from-partial-views"></a><span data-ttu-id="39cad-198">부분 보기에서 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="39cad-198">Access data from partial views</span></span>

<span data-ttu-id="39cad-199">부분 보기가 인스턴스화되면 부모의 `ViewData` 사전의 ‘사본’을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-199">When a partial view is instantiated, it receives a *copy* of the parent's `ViewData` dictionary.</span></span> <span data-ttu-id="39cad-200">부분 보기 내에서 데이터에 대한 업데이트는 부모 보기에 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-200">Updates made to the data within the partial view aren't persisted to the parent view.</span></span> <span data-ttu-id="39cad-201">부분 보기에서 변경된 `ViewData`는 부분 보기가 반환될 때 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-201">`ViewData` changes in a partial view are lost when the partial view returns.</span></span>

<span data-ttu-id="39cad-202">다음 예는 [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) 인스턴스를 부분 보기에 전달하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-202">The following example demonstrates how to pass an instance of [ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) to a partial view:</span></span>

```cshtml
@await Html.PartialAsync("_PartialName", customViewData)
```

<span data-ttu-id="39cad-203">모델을 부분 보기에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-203">You can pass a model into a partial view.</span></span> <span data-ttu-id="39cad-204">모델은 사용자 지정 개체일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-204">The model can be a custom object.</span></span> <span data-ttu-id="39cad-205">`PartialAsync`(콘텐츠 블록을 호출자에게 렌더링함) 또는 `RenderPartialAsync`(콘텐츠를 출력으로 스트리밍함)를 사용하여 모델을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-205">You can pass a model with `PartialAsync` (renders a block of content to the caller) or `RenderPartialAsync` (streams the content to the output):</span></span>

```cshtml
@await Html.PartialAsync("_PartialName", model)
```

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="39cad-206">**Razor 페이지**</span><span class="sxs-lookup"><span data-stu-id="39cad-206">**Razor Pages**</span></span>

<span data-ttu-id="39cad-207">샘플 앱의 다음 태그는 *Pages/ArticlesRP/ReadRP.cshtml* 페이지에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-207">The following markup in the sample app is from the *Pages/ArticlesRP/ReadRP.cshtml* page.</span></span> <span data-ttu-id="39cad-208">페이지에는 두 개의 부분 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-208">The page contains two partial views.</span></span> <span data-ttu-id="39cad-209">두 번째 부분 보기는 모델 및 `ViewData`를 부분 보기에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-209">The second partial view passes in a model and `ViewData` to the partial view.</span></span> <span data-ttu-id="39cad-210">`ViewDataDictionary` 생성자 오버로드를 사용하여 기존 `ViewData` 사전을 유지하면서 새로운 `ViewData` 사전을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-210">The `ViewDataDictionary` constructor overload is used to pass a new `ViewData` dictionary while retaining the existing `ViewData` dictionary.</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/ArticlesRP/ReadRP.cshtml?name=snippet_ReadPartialViewRP&highlight=5,15-19)]

<span data-ttu-id="39cad-211">*Pages/Shared/_AuthorPartialRP.cshtml*은 *ReadRP.cshtml* 태그 파일에서 참조하는 첫 번째 부분 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-211">*Pages/Shared/_AuthorPartialRP.cshtml* is the first partial view referenced by the *ReadRP.cshtml* markup file:</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/Shared/_AuthorPartialRP.cshtml)]

<span data-ttu-id="39cad-212">*Pages/ArticlesRP/_ArticleSectionRP.cshtml*은 *ReadRP.cshtml* 태그 파일에서 참조하는 두 번째 부분 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-212">*Pages/ArticlesRP/_ArticleSectionRP.cshtml* is the second partial view referenced by the *ReadRP.cshtml* markup file:</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Pages/ArticlesRP/_ArticleSectionRP.cshtml)]

<span data-ttu-id="39cad-213">**MVC**</span><span class="sxs-lookup"><span data-stu-id="39cad-213">**MVC**</span></span>

::: moniker-end

<span data-ttu-id="39cad-214">샘플 앱의 다음 태그는 *Views/Articles/Read.cshtml* 보기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-214">The following markup in the sample app shows the *Views/Articles/Read.cshtml* view.</span></span> <span data-ttu-id="39cad-215">보기에는 두 개의 부분 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-215">The view contains two partial views.</span></span> <span data-ttu-id="39cad-216">두 번째 부분 보기는 모델 및 `ViewData`를 부분 보기에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-216">The second partial view passes in a model and `ViewData` to the partial view.</span></span> <span data-ttu-id="39cad-217">`ViewDataDictionary` 생성자 오버로드를 사용하여 기존 `ViewData` 사전을 유지하면서 새로운 `ViewData` 사전을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-217">The `ViewDataDictionary` constructor overload is used to pass a new `ViewData` dictionary while retaining the existing `ViewData` dictionary.</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/Read.cshtml?name=snippet_ReadPartialView&highlight=5,15-19)]

<span data-ttu-id="39cad-218">*Views/Shared/_AuthorPartial.cshtml*은 *ReadRP.cshtml* 태그 파일에서 참조하는 첫 번째 부분 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-218">*Views/Shared/_AuthorPartial.cshtml* is the first partial view referenced by the *ReadRP.cshtml* markup file:</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Shared/_AuthorPartial.cshtml)]

<span data-ttu-id="39cad-219">*Views/Articles/_ArticleSection.cshtml*은 *Read.cshtml* 태그 파일에서 참조하는 두 번째 부분 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-219">*Views/Articles/_ArticleSection.cshtml* is the second partial view referenced by the *Read.cshtml* markup file:</span></span>

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/_ArticleSection.cshtml)]

<span data-ttu-id="39cad-220">런타임 시 부분은 부모 태그 파일의 렌더링된 출력에 렌더링됩니다. 여기서 자체는 공유 *_Layout.cshtml* 내에서 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-220">At runtime, the partials are rendered into the parent markup file's rendered output, which itself is rendered within the shared *_Layout.cshtml*.</span></span> <span data-ttu-id="39cad-221">첫 번째 부분 보기는 문서 작성자의 이름과 게시 날짜를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-221">The first partial view renders the article author's name and publication date:</span></span>

> <span data-ttu-id="39cad-222">Abraham Lincoln</span><span class="sxs-lookup"><span data-stu-id="39cad-222">Abraham Lincoln</span></span>
>
> <span data-ttu-id="39cad-223">&lt;공유 부분 보기 파일 경로&gt;의 부분 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-223">This partial view from &lt;shared partial view file path&gt;.</span></span>
> <span data-ttu-id="39cad-224">1863/11/19 12:00:00 AM</span><span class="sxs-lookup"><span data-stu-id="39cad-224">11/19/1863 12:00:00 AM</span></span>

<span data-ttu-id="39cad-225">두 번째 부분 보기는 문서의 섹션을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="39cad-225">The second partial view renders the article's sections:</span></span>

> <span data-ttu-id="39cad-226">섹션 1 인덱스: 0</span><span class="sxs-lookup"><span data-stu-id="39cad-226">Section One Index: 0</span></span>
>
> <span data-ttu-id="39cad-227">4개의 점수, 7년 전 ...</span><span class="sxs-lookup"><span data-stu-id="39cad-227">Four score and seven years ago ...</span></span>
>
> <span data-ttu-id="39cad-228">섹션 2 인덱스: 1</span><span class="sxs-lookup"><span data-stu-id="39cad-228">Section Two Index: 1</span></span>
>
> <span data-ttu-id="39cad-229">지금 멋진 전투에 참여하고 있습니다. 테스트 중...</span><span class="sxs-lookup"><span data-stu-id="39cad-229">Now we are engaged in a great civil war, testing ...</span></span>
>
> <span data-ttu-id="39cad-230">섹션 3 인덱스: 2</span><span class="sxs-lookup"><span data-stu-id="39cad-230">Section Three Index: 2</span></span>
>
> <span data-ttu-id="39cad-231">그러나 크게 볼 때 우리는 전념할 수 없습 ...</span><span class="sxs-lookup"><span data-stu-id="39cad-231">But, in a larger sense, we can not dedicate ...</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39cad-232">추가 자료</span><span class="sxs-lookup"><span data-stu-id="39cad-232">Additional resources</span></span>

::: moniker range=">= aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>
* <xref:mvc/views/view-components>
* <xref:mvc/controllers/areas>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/view-components>
* <xref:mvc/controllers/areas>

::: moniker-end
