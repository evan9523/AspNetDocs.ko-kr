---
title: ASP.NET Core에 대한 Razor 구문 참조
author: rick-anderson
description: 웹 페이지에 서버 기반 코드를 포함하는 Razor 태그 구문에 대해 알아봅니다.
ms.author: riande
ms.date: 10/26/2018
uid: mvc/views/razor
ms.openlocfilehash: 8e9ec3c5040e5a24cd5f773b1232897338741c0c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57052500"
---
# <a name="razor-syntax-reference-for-aspnet-core"></a><span data-ttu-id="1ebe5-103">ASP.NET Core에 대한 Razor 구문 참조</span><span class="sxs-lookup"><span data-stu-id="1ebe5-103">Razor syntax reference for ASP.NET Core</span></span>

<span data-ttu-id="1ebe5-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex), [Taylor Mullen](https://twitter.com/ntaylormullen) 및 [Dan Vicarel](https://github.com/Rabadash8820)</span><span class="sxs-lookup"><span data-stu-id="1ebe5-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex), [Taylor Mullen](https://twitter.com/ntaylormullen), and [Dan Vicarel](https://github.com/Rabadash8820)</span></span>

<span data-ttu-id="1ebe5-105">Razor는 웹 페이지에 서버 기반 코드를 포함하는 태그 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-105">Razor is a markup syntax for embedding server-based code into webpages.</span></span> <span data-ttu-id="1ebe5-106">Razor 구문은 Razor 태그, C# 및 HTML로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-106">The Razor syntax consists of Razor markup, C#, and HTML.</span></span> <span data-ttu-id="1ebe5-107">Razor를 포함하는 파일의 확장명은 일반적으로 *.cshtml*입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-107">Files containing Razor generally have a *.cshtml* file extension.</span></span>

## <a name="rendering-html"></a><span data-ttu-id="1ebe5-108">HTML 렌더링</span><span class="sxs-lookup"><span data-stu-id="1ebe5-108">Rendering HTML</span></span>

<span data-ttu-id="1ebe5-109">기본 Razor 언어는 HTML입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-109">The default Razor language is HTML.</span></span> <span data-ttu-id="1ebe5-110">Razor 태그에서 HTML을 렌더링하는 방법은 HTML 파일에서 HTML을 렌더링하는 방법과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-110">Rendering HTML from Razor markup is no different than rendering HTML from an HTML file.</span></span> <span data-ttu-id="1ebe5-111">*.cshtml* Razor 파일의 HTML 태그는 변경되지 않은 서버에서 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-111">HTML markup in *.cshtml* Razor files is rendered by the server unchanged.</span></span>

## <a name="razor-syntax"></a><span data-ttu-id="1ebe5-112">Razor 구문</span><span class="sxs-lookup"><span data-stu-id="1ebe5-112">Razor syntax</span></span>

<span data-ttu-id="1ebe5-113">Razor는 C#을 지원하며 `@` 기호를 사용하여 HTML에서 C#으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-113">Razor supports C# and uses the `@` symbol to transition from HTML to C#.</span></span> <span data-ttu-id="1ebe5-114">Razor는 C# 식을 평가하여 HTML 출력에서 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-114">Razor evaluates C# expressions and renders them in the HTML output.</span></span>

<span data-ttu-id="1ebe5-115">`@` 기호 뒤에 [Razor 예약 키워드](#razor-reserved-keywords)가 사용되면 이 기호는 Razor 관련 태그로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-115">When an `@` symbol is followed by a [Razor reserved keyword](#razor-reserved-keywords), it transitions into Razor-specific markup.</span></span> <span data-ttu-id="1ebe5-116">그렇지 않으면 C#으로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-116">Otherwise, it transitions into plain C#.</span></span>

<span data-ttu-id="1ebe5-117">Razor 태그에서 `@` 기호를 이스케이프하려면 두 번째 `@` 기호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-117">To escape an `@` symbol in Razor markup, use a second `@` symbol:</span></span>

```cshtml
<p>@@Username</p>
```

<span data-ttu-id="1ebe5-118">코드는 단일 `@` 기호를 사용하여 HTML로 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-118">The code is rendered in HTML with a single `@` symbol:</span></span>

```html
<p>@Username</p>
```

<span data-ttu-id="1ebe5-119">이메일 주소를 포함하는 HTML 특성 및 콘텐츠는 `@` 기호를 전환 문자로 취급하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-119">HTML attributes and content containing email addresses don't treat the `@` symbol as a transition character.</span></span> <span data-ttu-id="1ebe5-120">다음 예제의 이메일 주소는 Razor 구문 분석에 의해 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-120">The email addresses in the following example are untouched by Razor parsing:</span></span>

```cshtml
<a href="mailto:Support@contoso.com">Support@contoso.com</a>
```

## <a name="implicit-razor-expressions"></a><span data-ttu-id="1ebe5-121">암시적 Razor 식</span><span class="sxs-lookup"><span data-stu-id="1ebe5-121">Implicit Razor expressions</span></span>

<span data-ttu-id="1ebe5-122">암시적 Razor 식은 `@`으로 시작하고 그 뒤에 C# 코드가 옵니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-122">Implicit Razor expressions start with `@` followed by C# code:</span></span>

```cshtml
<p>@DateTime.Now</p>
<p>@DateTime.IsLeapYear(2016)</p>
```

<span data-ttu-id="1ebe5-123">C# `await` 키워드를 제외하고, 암시적 식에 공백이 있으면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-123">With the exception of the C# `await` keyword, implicit expressions must not contain spaces.</span></span> <span data-ttu-id="1ebe5-124">C# 문에 명확한 끝이 있으면 공백을 혼합 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-124">If the C# statement has a clear ending, spaces can be intermingled:</span></span>

```cshtml
<p>@await DoSomething("hello", "world")</p>
```

<span data-ttu-id="1ebe5-125">암시적 식은 C# 제네릭을 포함할 수 **없습니다**. 대괄호(`<>`) 안에 있는 문자가 HTML 태그로 해석되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-125">Implicit expressions **cannot** contain C# generics, as the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="1ebe5-126">다음 코드는 유효하지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-126">The following code is **not** valid:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="1ebe5-127">위의 코드는 다음 중 하나와 비슷한 컴파일러 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-127">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="1ebe5-128">"Int" 요소가 종료되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-128">The "int" element wasn't closed.</span></span> <span data-ttu-id="1ebe5-129">모든 요소는 하나 있어야 자체적으로 닫히거나 일치하는 끝 태그가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-129">All elements must be either self-closing or have a matching end tag.</span></span>
 *  <span data-ttu-id="1ebe5-130">'GenericMethod' 메서드 그룹을 비대리자 형식 '개체'로 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-130">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="1ebe5-131">메서드를 호출할 생각이었나요?</span><span class="sxs-lookup"><span data-stu-id="1ebe5-131">Did you intend to invoke the method?\`</span></span> 
 
<span data-ttu-id="1ebe5-132">제네릭 메서드 호출은 [명시적 Razor 식](#explicit-razor-expressions) 또는 [Razor 코드 블록](#razor-code-blocks)에 래핑되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-132">Generic method calls must be wrapped in an [explicit Razor expression](#explicit-razor-expressions) or a [Razor code block](#razor-code-blocks).</span></span>

## <a name="explicit-razor-expressions"></a><span data-ttu-id="1ebe5-133">명시적 Razor 식</span><span class="sxs-lookup"><span data-stu-id="1ebe5-133">Explicit Razor expressions</span></span>

<span data-ttu-id="1ebe5-134">명시적 Razor 식은 `@` 기호와 균형 잡힌 괄호로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-134">Explicit Razor expressions consist of an `@` symbol with balanced parenthesis.</span></span> <span data-ttu-id="1ebe5-135">지난 주의 시간을 렌더링하기 위해 다음 Razor 태그가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-135">To render last week's time, the following Razor markup is used:</span></span>

```cshtml
<p>Last week this time: @(DateTime.Now - TimeSpan.FromDays(7))</p>
```

<span data-ttu-id="1ebe5-136">`@()` 괄호 안의 모든 콘텐츠가 평가되고 출력에 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-136">Any content within the `@()` parenthesis is evaluated and rendered to the output.</span></span>

<span data-ttu-id="1ebe5-137">이전 섹션에서 설명한 암시적 식은 일반적으로 공백을 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-137">Implicit expressions, described in the previous section, generally can't contain spaces.</span></span> <span data-ttu-id="1ebe5-138">다음 코드에서 일주일은 현재 시간에서 차감되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-138">In the following code, one week isn't subtracted from the current time:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact.cshtml?range=17)]

<span data-ttu-id="1ebe5-139">이 코드는 다음 HTML을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-139">The code renders the following HTML:</span></span>

```html
<p>Last week: 7/7/2016 4:39:52 PM - TimeSpan.FromDays(7)</p>
```

<span data-ttu-id="1ebe5-140">명시적 식은 텍스트를 식 결과와 연결하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-140">Explicit expressions can be used to concatenate text with an expression result:</span></span>

```cshtml
@{
    var joe = new Person("Joe", 33);
}

<p>Age@(joe.Age)</p>
```

<span data-ttu-id="1ebe5-141">명시적 식이 없으면 `<p>Age@joe.Age</p>`는 이메일 주소로 처리되고 `<p>Age@joe.Age</p>`가 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-141">Without the explicit expression, `<p>Age@joe.Age</p>` is treated as an email address, and `<p>Age@joe.Age</p>` is rendered.</span></span> <span data-ttu-id="1ebe5-142">명시적 식으로 작성되면 `<p>Age33</p>`이 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-142">When written as an explicit expression, `<p>Age33</p>` is rendered.</span></span>

<span data-ttu-id="1ebe5-143">명시적 식은 *.cshtml* 파일에 있는 제네릭 메서드의 출력을 렌더링하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-143">Explicit expressions can be used to render output from generic methods in *.cshtml* files.</span></span> <span data-ttu-id="1ebe5-144">다음 표시는 앞에서 C# 제네릭의 대괄호로 인해 발생한 오류를 해결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-144">The following markup shows how to correct the error shown earlier caused by the brackets of a C# generic.</span></span> <span data-ttu-id="1ebe5-145">이 코드는 명시적 식으로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-145">The code is written as an explicit expression:</span></span>

```cshtml
<p>@(GenericMethod<int>())</p>
```

## <a name="expression-encoding"></a><span data-ttu-id="1ebe5-146">식 인코딩</span><span class="sxs-lookup"><span data-stu-id="1ebe5-146">Expression encoding</span></span>

<span data-ttu-id="1ebe5-147">문자열로 확인되는 C# 식은 인코딩된 HTML입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-147">C# expressions that evaluate to a string are HTML encoded.</span></span> <span data-ttu-id="1ebe5-148">`IHtmlContent`로 확인되는 C# 식은 `IHtmlContent.WriteTo`를 통해 직접 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-148">C# expressions that evaluate to `IHtmlContent` are rendered directly through `IHtmlContent.WriteTo`.</span></span> <span data-ttu-id="1ebe5-149">`IHtmlContent`로 확인되지 않는 C# 식은 `ToString`을 통해 문자열로 변환되고 인코딩된 후 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-149">C# expressions that don't evaluate to `IHtmlContent` are converted to a string by `ToString` and encoded before they're rendered.</span></span>

```cshtml
@("<span>Hello World</span>")
```

<span data-ttu-id="1ebe5-150">이 코드는 다음 HTML을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-150">The code renders the following HTML:</span></span>

```html
&lt;span&gt;Hello World&lt;/span&gt;
```

<span data-ttu-id="1ebe5-151">다음과 같은 이유로 HTML은 브라우저에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-151">The HTML is shown in the browser as:</span></span>

```
<span>Hello World</span>
```

<span data-ttu-id="1ebe5-152">`HtmlHelper.Raw` 출력은 인코딩되지 않지만 HTML 태그로 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-152">`HtmlHelper.Raw` output isn't encoded but rendered as HTML markup.</span></span>

> [!WARNING]
> <span data-ttu-id="1ebe5-153">삭제되지 않은 사용자 입력에서 `HtmlHelper.Raw`를 사용하는 것은 보안상 위험합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-153">Using `HtmlHelper.Raw` on unsanitized user input is a security risk.</span></span> <span data-ttu-id="1ebe5-154">사용자 입력에 악의적인 JavaScript 또는 다른 악용 기법이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-154">User input might contain malicious JavaScript or other exploits.</span></span> <span data-ttu-id="1ebe5-155">사용자 입력을 제거하기는 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-155">Sanitizing user input is difficult.</span></span> <span data-ttu-id="1ebe5-156">사용자 입력에 `HtmlHelper.Raw`를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-156">Avoid using `HtmlHelper.Raw` with user input.</span></span>

```cshtml
@Html.Raw("<span>Hello World</span>")
```

<span data-ttu-id="1ebe5-157">이 코드는 다음 HTML을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-157">The code renders the following HTML:</span></span>

```html
<span>Hello World</span>
```

## <a name="razor-code-blocks"></a><span data-ttu-id="1ebe5-158">Razor 코드 블록</span><span class="sxs-lookup"><span data-stu-id="1ebe5-158">Razor code blocks</span></span>

<span data-ttu-id="1ebe5-159">Razor 코드 블록은 `@`으로 시작하고 `{}`로 묶입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-159">Razor code blocks start with `@` and are enclosed by `{}`.</span></span> <span data-ttu-id="1ebe5-160">식과는 달리, 코드 블록 내부의 C# 코드는 렌더링되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-160">Unlike expressions, C# code inside code blocks isn't rendered.</span></span> <span data-ttu-id="1ebe5-161">보기의 코드 블록과 식은 같은 범위를 공유하고 순서대로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-161">Code blocks and expressions in a view share the same scope and are defined in order:</span></span>

```cshtml
@{
    var quote = "The future depends on what you do today. - Mahatma Gandhi";
}

<p>@quote</p>

@{
    quote = "Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.";
}

<p>@quote</p>
```

<span data-ttu-id="1ebe5-162">이 코드는 다음 HTML을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-162">The code renders the following HTML:</span></span>

```html
<p>The future depends on what you do today. - Mahatma Gandhi</p>
<p>Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.</p>
```

### <a name="implicit-transitions"></a><span data-ttu-id="1ebe5-163">암시적 전환</span><span class="sxs-lookup"><span data-stu-id="1ebe5-163">Implicit transitions</span></span>

<span data-ttu-id="1ebe5-164">코드 블록의 기본 언어는 C#이지만, Razor 페이지를 다시 HTML로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-164">The default language in a code block is C#, but the Razor Page can transition back to HTML:</span></span>

```cshtml
@{
    var inCSharp = true;
    <p>Now in HTML, was in C# @inCSharp</p>
}
```

### <a name="explicit-delimited-transition"></a><span data-ttu-id="1ebe5-165">구분 기호로 분리된 명시적 전환</span><span class="sxs-lookup"><span data-stu-id="1ebe5-165">Explicit delimited transition</span></span>

<span data-ttu-id="1ebe5-166">HTML을 렌더링해야 하는 코드 블록의 하위 섹션을 정의하려면 렌더링할 문자를 Razor **\<text>** 태그로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-166">To define a subsection of a code block that should render HTML, surround the characters for rendering with the Razor **\<text>** tag:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <text>Name: @person.Name</text>
}
```

<span data-ttu-id="1ebe5-167">HTML 태그로 묶이지 않은 HTML을 렌더링하려면 이 방법을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-167">Use this approach to render HTML that isn't surrounded by an HTML tag.</span></span> <span data-ttu-id="1ebe5-168">HTML 또는 Razor 태그가 없으면 Razor 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-168">Without an HTML or Razor tag, a Razor runtime error occurs.</span></span>

<span data-ttu-id="1ebe5-169">**\<text>** 태그는 콘텐츠를 렌더링할 때 공백을 제어하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-169">The **\<text>** tag is useful to control whitespace when rendering content:</span></span>

* <span data-ttu-id="1ebe5-170">**\<text>** 태그 사이의 콘텐츠만 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-170">Only the content between the **\<text>** tag is rendered.</span></span> 
* <span data-ttu-id="1ebe5-171">**\<text>** 태그 앞 또는 뒤에 있는 공백은 HTML 출력에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-171">No whitespace before or after the **\<text>** tag appears in the HTML output.</span></span>

### <a name="explicit-line-transition-with-"></a><span data-ttu-id="1ebe5-172">@을 사용하여 명시적 줄 전환:</span><span class="sxs-lookup"><span data-stu-id="1ebe5-172">Explicit Line Transition with @:</span></span>

<span data-ttu-id="1ebe5-173">코드 블록 내부의 나머지 전체 줄을 HTML로 렌더링하려면 `@:` 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-173">To render the rest of an entire line as HTML inside a code block, use the `@:` syntax:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    @:Name: @person.Name
}
```

<span data-ttu-id="1ebe5-174">코드에 `@:`이 없으면 Razor 런타임 오류가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-174">Without the `@:` in the code, a Razor runtime error is generated.</span></span>

<span data-ttu-id="1ebe5-175">경고: Razor 파일의 추가 `@` 문자는 블록의 뒷부분에 나오는 명령문에서 컴파일러 오류를 유발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-175">Warning: Extra `@` characters in a Razor file can cause compiler errors at statements later in the block.</span></span> <span data-ttu-id="1ebe5-176">실제 오류가 보고된 오류보다 먼저 발생하기 때문에 이러한 컴파일러 오류를 이해하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-176">These compiler errors can be difficult to understand because the actual error occurs before the reported error.</span></span> <span data-ttu-id="1ebe5-177">이 오류는 여러 암시적/명시적 식을 단일 코드 블록에 결합한 이후에 자주 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-177">This error is common after combining multiple implicit/explicit expressions into a single code block.</span></span>

## <a name="control-structures"></a><span data-ttu-id="1ebe5-178">제어 구조</span><span class="sxs-lookup"><span data-stu-id="1ebe5-178">Control structures</span></span>

<span data-ttu-id="1ebe5-179">제어 구조는 코드 블록의 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-179">Control structures are an extension of code blocks.</span></span> <span data-ttu-id="1ebe5-180">코드 블록의 모든 측면(태그로 전환, 인라인 C#)은 다음 구조에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-180">All aspects of code blocks (transitioning to markup, inline C#) also apply to the following structures:</span></span>

### <a name="conditionals-if-else-if-else-and-switch"></a><span data-ttu-id="1ebe5-181">조건부 @if, else if, else 및 @switch</span><span class="sxs-lookup"><span data-stu-id="1ebe5-181">Conditionals @if, else if, else, and @switch</span></span>

<span data-ttu-id="1ebe5-182">`@if`는 코드가 실행되는 시기를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-182">`@if` controls when code runs:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
```

<span data-ttu-id="1ebe5-183">`else` 및 `else if`는 `@` 기호가 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-183">`else` and `else if` don't require the `@` symbol:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
else if (value >= 1337)
{
    <p>The value is large.</p>
}
else
{
    <p>The value is odd and small.</p>
}
```

<span data-ttu-id="1ebe5-184">다음 태그는 switch 문 사용 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-184">The following markup shows how to use a switch statement:</span></span>

```cshtml
@switch (value)
{
    case 1:
        <p>The value is 1!</p>
        break;
    case 1337:
        <p>Your number is 1337!</p>
        break;
    default:
        <p>Your number wasn't 1 or 1337.</p>
        break;
}
```

### <a name="looping-for-foreach-while-and-do-while"></a><span data-ttu-id="1ebe5-185">Looping @for, @foreach, @while 및 @do while</span><span class="sxs-lookup"><span data-stu-id="1ebe5-185">Looping @for, @foreach, @while, and @do while</span></span>

<span data-ttu-id="1ebe5-186">템플릿 기반 HTML은 반복 제어 문으로 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-186">Templated HTML can be rendered with looping control statements.</span></span> <span data-ttu-id="1ebe5-187">사람 목록을 렌더링하려면:</span><span class="sxs-lookup"><span data-stu-id="1ebe5-187">To render a list of people:</span></span>

```cshtml
@{
    var people = new Person[]
    {
          new Person("Weston", 33),
          new Person("Johnathon", 41),
          ...
    };
}
```

<span data-ttu-id="1ebe5-188">다음 반복 문이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-188">The following looping statements are supported:</span></span>

`@for`

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@foreach`

```cshtml
@foreach (var person in people)
{
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@while`

```cshtml
@{ var i = 0; }
@while (i < people.Length)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
}
```

`@do while`

```cshtml
@{ var i = 0; }
@do
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
} while (i < people.Length);
```

### <a name="compound-using"></a><span data-ttu-id="1ebe5-189">복합 @using</span><span class="sxs-lookup"><span data-stu-id="1ebe5-189">Compound @using</span></span>

<span data-ttu-id="1ebe5-190">C#에서 `using` 문은 개체가 삭제되도록 보장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-190">In C#, a `using` statement is used to ensure an object is disposed.</span></span> <span data-ttu-id="1ebe5-191">Razor에서는 동일한 메커니즘을 사용하여 추가 콘텐츠를 포함하는 HTML 도우미를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-191">In Razor, the same mechanism is used to create HTML Helpers that contain additional content.</span></span> <span data-ttu-id="1ebe5-192">다음 코드에서 HTML 도우미는 `@using` 문을 사용하여 form 태그를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-192">In the following code, HTML Helpers render a form tag with the `@using` statement:</span></span>


```cshtml
@using (Html.BeginForm())
{
    <div>
        email:
        <input type="email" id="Email" value="">
        <button>Register</button>
    </div>
}
```

<span data-ttu-id="1ebe5-193">범위 수준 작업은 [태그 도우미](xref:mvc/views/tag-helpers/intro)를 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-193">Scope-level actions can be performed with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

### <a name="try-catch-finally"></a><span data-ttu-id="1ebe5-194">@try, catch, finally</span><span class="sxs-lookup"><span data-stu-id="1ebe5-194">@try, catch, finally</span></span>

<span data-ttu-id="1ebe5-195">예외 처리는 C#과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-195">Exception handling is similar to C#:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact7.cshtml)]

### <a name="lock"></a>@lock

<span data-ttu-id="1ebe5-196">Razor는 lock 문을 사용하여 중요한 섹션을 보호하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-196">Razor has the capability to protect critical sections with lock statements:</span></span>

```cshtml
@lock (SomeLock)
{
    // Do critical section work
}
```

### <a name="comments"></a><span data-ttu-id="1ebe5-197">설명</span><span class="sxs-lookup"><span data-stu-id="1ebe5-197">Comments</span></span>

<span data-ttu-id="1ebe5-198">Razor는 C# 및 HTML 주석을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-198">Razor supports C# and HTML comments:</span></span>

```cshtml
@{
    /* C# comment */
    // Another C# comment
}
<!-- HTML comment -->
```

<span data-ttu-id="1ebe5-199">이 코드는 다음 HTML을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-199">The code renders the following HTML:</span></span>

```html
<!-- HTML comment -->
```

<span data-ttu-id="1ebe5-200">Razor 주석은 웹 페이지가 렌더링되기 전에 서버에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-200">Razor comments are removed by the server before the webpage is rendered.</span></span> <span data-ttu-id="1ebe5-201">Razor는 `@*  *@`을 사용하여 주석을 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-201">Razor uses `@*  *@` to delimit comments.</span></span> <span data-ttu-id="1ebe5-202">다음 코드는 주석 처리되며, 따라서 서버에서 어떤 태그도 렌더링하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-202">The following code is commented out, so the server doesn't render any markup:</span></span>

```cshtml
@*
    @{
        /* C# comment */
        // Another C# comment
    }
    <!-- HTML comment -->
*@
```

## <a name="directives"></a><span data-ttu-id="1ebe5-203">지시문</span><span class="sxs-lookup"><span data-stu-id="1ebe5-203">Directives</span></span>

<span data-ttu-id="1ebe5-204">Razor 지시문은 `@` 기호 뒤에 예약된 키워드를 사용하여 암시적 식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-204">Razor directives are represented by implicit expressions with reserved keywords following the `@` symbol.</span></span> <span data-ttu-id="1ebe5-205">지시문은 일반적으로 보기를 구문 분석하는 방식을 변경하거나 다른 기능을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-205">A directive typically changes the way a view is parsed or enables different functionality.</span></span>

<span data-ttu-id="1ebe5-206">Razor가 보기에 대한 코드를 생성하는 원리를 이해하면 지시문의 작동 원리를 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-206">Understanding how Razor generates code for a view makes it easier to understand how directives work.</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact8.cshtml)]

<span data-ttu-id="1ebe5-207">이 코드는 다음과 비슷한 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-207">The code generates a class similar to the following:</span></span>

```csharp
public class _Views_Something_cshtml : RazorPage<dynamic>
{
    public override async Task ExecuteAsync()
    {
        var output = "Getting old ain't for wimps! - Anonymous";

        WriteLiteral("/r/n<div>Quote of the Day: ");
        Write(output);
        WriteLiteral("</div>");
    }
}
```

<span data-ttu-id="1ebe5-208">이 문서의 뒷부분에 나오는 [보기용으로 생성된 Razor C# 클래스 검사](#inspect-the-razor-c-class-generated-for-a-view) 섹션에서는 생성된 이 클래스를 보는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-208">Later in this article, the section [Inspect the Razor C# class generated for a view](#inspect-the-razor-c-class-generated-for-a-view) explains how to view this generated class.</span></span>

<a name="using"></a>
### <a name="using"></a>@using

<span data-ttu-id="1ebe5-209">`@using` 지시문은 C# `using` 지시문을 생성된 보기에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-209">The `@using` directive adds the C# `using` directive to the generated view:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact9.cshtml)]

### <a name="model"></a>@model

<span data-ttu-id="1ebe5-210">`@model` 지시문은 보기에 전달되는 모델 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-210">The `@model` directive specifies the type of the model passed to a view:</span></span>

```cshtml
@model TypeNameOfModel
```

<span data-ttu-id="1ebe5-211">개별 사용자 계정을 사용하여 만든 ASP.NET Core MVC 앱에서, *Views/Account/Login.cshtml* 보기는 다음과 같은 모델 선언을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-211">In an ASP.NET Core MVC app created with individual user accounts, the *Views/Account/Login.cshtml* view contains the following model declaration:</span></span>

```cshtml
@model LoginViewModel
```

<span data-ttu-id="1ebe5-212">생성된 클래스는 `RazorPage<dynamic>`에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-212">The class generated inherits from `RazorPage<dynamic>`:</span></span>

```csharp
public class _Views_Account_Login_cshtml : RazorPage<LoginViewModel>
```

<span data-ttu-id="1ebe5-213">Razor는 보기에 전달된 모델에 액세스할 수 있는 `Model` 속성을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-213">Razor exposes a `Model` property for accessing the model passed to the view:</span></span>

```cshtml
<div>The Login Email: @Model.Email</div>
```

<span data-ttu-id="1ebe5-214">`@model` 지시문은 이 속성의 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-214">The `@model` directive specifies the type of this property.</span></span> <span data-ttu-id="1ebe5-215">이 지시문은 보기가 파생되는 클래스를 생성한 `RazorPage<T>`의 `T`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-215">The directive specifies the `T` in `RazorPage<T>` that the generated class that the view derives from.</span></span> <span data-ttu-id="1ebe5-216">`@model` 지시문이 지정되지 않을 경우 `Model` 속성은 `dynamic` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-216">If the `@model` directive isn't specified, the `Model` property is of type `dynamic`.</span></span> <span data-ttu-id="1ebe5-217">모델의 값은 컨트롤러에서 보기로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-217">The value of the model is passed from the controller to the view.</span></span> <span data-ttu-id="1ebe5-218">자세한 내용은 [강력한 형식의 모델 및 &commat;모델 키워드](xref:tutorials/first-mvc-app/adding-model#strongly-typed-models-and-the--keyword)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-218">For more information, see [Strongly typed models and the &commat;model keyword](xref:tutorials/first-mvc-app/adding-model#strongly-typed-models-and-the--keyword).</span></span>

### <a name="inherits"></a>@inherits

<span data-ttu-id="1ebe5-219">`@inherits` 지시문은 보기에서 상속하는 클래스에 대한 완전한 제어권을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-219">The `@inherits` directive provides full control of the class the view inherits:</span></span>

```cshtml
@inherits TypeNameOfClassToInheritFrom
```

<span data-ttu-id="1ebe5-220">다음 코드는 사용자 지정 Razor 페이지 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-220">The following code is a custom Razor page type:</span></span>

[!code-csharp[](razor/sample/Classes/CustomRazorPage.cs)]

<span data-ttu-id="1ebe5-221">`CustomText`는 보기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-221">The `CustomText` is displayed in a view:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact10.cshtml)]

<span data-ttu-id="1ebe5-222">이 코드는 다음 HTML을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-222">The code renders the following HTML:</span></span>

```html
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

 <span data-ttu-id="1ebe5-223">`@model` 및 `@inherits`는 동일한 보기에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-223">`@model` and `@inherits` can be used in the same view.</span></span> <span data-ttu-id="1ebe5-224">`@inherits`는 보기에서 가져오는 *_ViewImports.cshtml* 파일에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-224">`@inherits` can be in a *_ViewImports.cshtml* file that the view imports:</span></span>

[!code-cshtml[](razor/sample/Views/_ViewImportsModel.cshtml)]

<span data-ttu-id="1ebe5-225">다음 코드는 강력한 형식의 보기 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-225">The following code is an example of a strongly-typed view:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Login1.cshtml)]

<span data-ttu-id="1ebe5-226">"rick@contoso.com"이 모델에 전달되면 보기에서 다음과 같은 HTML 태그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-226">If "rick@contoso.com" is passed in the model, the view generates the following HTML markup:</span></span>

```html
<div>The Login Email: rick@contoso.com</div>
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

### <a name="inject"></a>@inject

<span data-ttu-id="1ebe5-227">`@inject` 지시문을 사용하면 Razor 페이지에서 [서비스 컨테이너](xref:fundamentals/dependency-injection)의 서비스를 보기에 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-227">The `@inject` directive enables the Razor Page to inject a service from the [service container](xref:fundamentals/dependency-injection) into a view.</span></span> <span data-ttu-id="1ebe5-228">자세한 내용은 [보기에 종속성 주입](xref:mvc/views/dependency-injection)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-228">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span>

### <a name="functions"></a>@functions

<span data-ttu-id="1ebe5-229">`@functions` 지시문을 사용하면 Razor 페이지에서 C# 코드 블록을 보기에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-229">The `@functions` directive enables a Razor Page to add a C# code block to a view:</span></span>

```cshtml
@functions { // C# Code }
```

<span data-ttu-id="1ebe5-230">예:</span><span class="sxs-lookup"><span data-stu-id="1ebe5-230">For example:</span></span>

[!code-cshtml[](razor/sample/Views/Home/Contact6.cshtml)]

<span data-ttu-id="1ebe5-231">이 코드는 다음과 같은 HTML 태그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-231">The code generates the following HTML markup:</span></span>

```html
<div>From method: Hello</div>
```

<span data-ttu-id="1ebe5-232">다음 코드는 생성된 Razor C# 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-232">The following code is the generated Razor C# class:</span></span>

[!code-csharp[](razor/sample/Classes/Views_Home_Test_cshtml.cs?range=1-19)]

### <a name="section"></a>@section

<span data-ttu-id="1ebe5-233">`@section` 지시문은 [layout](xref:mvc/views/layout)과 함께 사용되어 HTML 페이지의 여러 부분에 있는 콘텐츠를 렌더링할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-233">The `@section` directive is used in conjunction with the [layout](xref:mvc/views/layout) to enable views to render content in different parts of the HTML page.</span></span> <span data-ttu-id="1ebe5-234">자세한 내용은 [섹션](xref:mvc/views/layout#layout-sections-label)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-234">For more information, see [Sections](xref:mvc/views/layout#layout-sections-label).</span></span>

## <a name="templated-razor-delegates"></a><span data-ttu-id="1ebe5-235">템플릿에 작성된 Razor 대리자</span><span class="sxs-lookup"><span data-stu-id="1ebe5-235">Templated Razor delegates</span></span>

<span data-ttu-id="1ebe5-236">Razor 템플릿을 사용하면 UI 코드 조각을 다음 형식으로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-236">Razor templates allow you to define a UI snippet with the following format:</span></span>

```cshtml
@<tag>...</tag>
```

<span data-ttu-id="1ebe5-237">다음 예제에서는 템플릿에 작성된 Razor 대리자를 <xref:System.Func`2>로 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-237">The following example illustrates how to specify a templated Razor delegate as a <xref:System.Func`2>.</span></span> <span data-ttu-id="1ebe5-238">[dynamic 형식](/dotnet/csharp/programming-guide/types/using-type-dynamic)은 대리자에서 캡슐화하는 메서드의 매개 변수로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-238">The [dynamic type](/dotnet/csharp/programming-guide/types/using-type-dynamic) is specified for the parameter of the method that the delegate encapsulates.</span></span> <span data-ttu-id="1ebe5-239">[object 형식](/dotnet/csharp/language-reference/keywords/object)은 대리자의 반환 값으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-239">An [object type](/dotnet/csharp/language-reference/keywords/object) is specified as the return value of the delegate.</span></span> <span data-ttu-id="1ebe5-240">템플릿은 `Name` 속성이 있는 `Pet`의 <xref:System.Collections.Generic.List`1>에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-240">The template is used with a <xref:System.Collections.Generic.List`1> of `Pet` that has a `Name` property.</span></span>

```csharp
public class Pet
{
    public string Name { get; set; }
}
```

```cshtml
@{
    Func<dynamic, object> petTemplate = @<p>You have a pet named <strong>@item.Name</strong>.</p>;

    var pets = new List<Pet>
    {
        new Pet { Name = "Rin Tin Tin" },
        new Pet { Name = "Mr. Bigglesworth" },
        new Pet { Name = "K-9" }
    };
}
```

<span data-ttu-id="1ebe5-241">템플릿은 `foreach` 문에서 제공하는 `pets`에서 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-241">The template is rendered with `pets` supplied by a `foreach` statement:</span></span>

```cshtml
@foreach (var pet in pets)
{
    @petTemplate(pet)
}
```

<span data-ttu-id="1ebe5-242">렌더링된 출력:</span><span class="sxs-lookup"><span data-stu-id="1ebe5-242">Rendered output:</span></span>

```html
<p>You have a pet named <strong>Rin Tin Tin</strong>.</p>
<p>You have a pet named <strong>Mr. Bigglesworth</strong>.</p>
<p>You have a pet named <strong>K-9</strong>.</p>
```

<span data-ttu-id="1ebe5-243">또한 인라인 Razor 템플릿은 메서드에 대한 인수로 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-243">You can also supply an inline Razor template as an argument to a method.</span></span> <span data-ttu-id="1ebe5-244">다음 예제에서는 `Repeat` 메서드에서 Razor 템플릿을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-244">In the following example, the `Repeat` method receives a Razor template.</span></span> <span data-ttu-id="1ebe5-245">이 메서드는 템플릿을 사용하여 목록에서 제공된 항목의 반복이 포함된 HTML 콘텐츠를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-245">The method uses the template to produce HTML content with repeats of items supplied from a list:</span></span>

```cshtml
@using Microsoft.AspNetCore.Html

@functions {
    public static IHtmlContent Repeat(IEnumerable<dynamic> items, int times, 
        Func<dynamic, IHtmlContent> template)
    {
        var html = new HtmlContentBuilder();

        foreach (var item in items)
        {
            for (var i = 0; i < times; i++)
            {
                html.AppendHtml(template(item));
            }
        }

        return html;
    }
}
```

<span data-ttu-id="1ebe5-246">이전 예제의 애완 동물 목록을 사용하여 `Repeat` 메서드는 다음 항목과 함께 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-246">Using the list of pets from the prior example, the `Repeat` method is called with:</span></span>

* <span data-ttu-id="1ebe5-247"><xref:System.Collections.Generic.List`1>의 `Pet`입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-247"><xref:System.Collections.Generic.List`1> of `Pet`.</span></span>
* <span data-ttu-id="1ebe5-248">각 애완 동물에 대한 반복 횟수</span><span class="sxs-lookup"><span data-stu-id="1ebe5-248">Number of times to repeat each pet.</span></span>
* <span data-ttu-id="1ebe5-249">순서가 지정되지 않은 목록의 목록 항목에 사용할 인라인 템플릿</span><span class="sxs-lookup"><span data-stu-id="1ebe5-249">Inline template to use for the list items of an unordered list.</span></span>

```cshtml
<ul>
    @Repeat(pets, 3, @<li>@item.Name</li>)
</ul>
```

<span data-ttu-id="1ebe5-250">렌더링된 출력:</span><span class="sxs-lookup"><span data-stu-id="1ebe5-250">Rendered output:</span></span>

```html
<ul>
    <li>Rin Tin Tin</li>
    <li>Rin Tin Tin</li>
    <li>Rin Tin Tin</li>
    <li>Mr. Bigglesworth</li>
    <li>Mr. Bigglesworth</li>
    <li>Mr. Bigglesworth</li>
    <li>K-9</li>
    <li>K-9</li>
    <li>K-9</li>
</ul>
```

## <a name="tag-helpers"></a><span data-ttu-id="1ebe5-251">태그 도우미</span><span class="sxs-lookup"><span data-stu-id="1ebe5-251">Tag Helpers</span></span>

<span data-ttu-id="1ebe5-252">[태그 도우미](xref:mvc/views/tag-helpers/intro)와 관련된 세 가지 지시문이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-252">There are three directives that pertain to [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

| <span data-ttu-id="1ebe5-253">지시문</span><span class="sxs-lookup"><span data-stu-id="1ebe5-253">Directive</span></span> | <span data-ttu-id="1ebe5-254">함수</span><span class="sxs-lookup"><span data-stu-id="1ebe5-254">Function</span></span> |
| --------- | -------- |
| [<span data-ttu-id="1ebe5-255">&commat;addTagHelper</span><span class="sxs-lookup"><span data-stu-id="1ebe5-255">&commat;addTagHelper</span></span>](xref:mvc/views/tag-helpers/intro#add-helper-label) | <span data-ttu-id="1ebe5-256">보기에 태그 도우미를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-256">Makes Tag Helpers available to a view.</span></span> |
| [<span data-ttu-id="1ebe5-257">&commat;removeTagHelper</span><span class="sxs-lookup"><span data-stu-id="1ebe5-257">&commat;removeTagHelper</span></span>](xref:mvc/views/tag-helpers/intro#remove-razor-directives-label) | <span data-ttu-id="1ebe5-258">보기에서 이전에 추가된 태그 도우미를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-258">Removes Tag Helpers previously added from a view.</span></span> |
| [<span data-ttu-id="1ebe5-259">&commat;tagHelperPrefix</span><span class="sxs-lookup"><span data-stu-id="1ebe5-259">&commat;tagHelperPrefix</span></span>](xref:mvc/views/tag-helpers/intro#prefix-razor-directives-label) | <span data-ttu-id="1ebe5-260">태그 도우미를 지원하고 태그 도우미 사용을 명시적으로 만들어주는 태그 접두사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-260">Specifies a tag prefix to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> |

## <a name="razor-reserved-keywords"></a><span data-ttu-id="1ebe5-261">Razor 예약 키워드</span><span class="sxs-lookup"><span data-stu-id="1ebe5-261">Razor reserved keywords</span></span>

### <a name="razor-keywords"></a><span data-ttu-id="1ebe5-262">Razor 키워드</span><span class="sxs-lookup"><span data-stu-id="1ebe5-262">Razor keywords</span></span>

* <span data-ttu-id="1ebe5-263">페이지(ASP.NET Core 2.0 이상 필요)</span><span class="sxs-lookup"><span data-stu-id="1ebe5-263">page (Requires ASP.NET Core 2.0 and later)</span></span>
* <span data-ttu-id="1ebe5-264">네임스페이스(namespace)</span><span class="sxs-lookup"><span data-stu-id="1ebe5-264">namespace</span></span>
* <span data-ttu-id="1ebe5-265">함수</span><span class="sxs-lookup"><span data-stu-id="1ebe5-265">functions</span></span>
* <span data-ttu-id="1ebe5-266">상속</span><span class="sxs-lookup"><span data-stu-id="1ebe5-266">inherits</span></span>
* <span data-ttu-id="1ebe5-267">model</span><span class="sxs-lookup"><span data-stu-id="1ebe5-267">model</span></span>
* <span data-ttu-id="1ebe5-268">section</span><span class="sxs-lookup"><span data-stu-id="1ebe5-268">section</span></span>
* <span data-ttu-id="1ebe5-269">도우미(현재 ASP.NET Core에서 지원되지 않음)</span><span class="sxs-lookup"><span data-stu-id="1ebe5-269">helper (Not currently supported by ASP.NET Core)</span></span>

<span data-ttu-id="1ebe5-270">Razor 키워드는 `@(Razor Keyword)`으로 이스케이프됩니다(예: `@(functions)`).</span><span class="sxs-lookup"><span data-stu-id="1ebe5-270">Razor keywords are escaped with `@(Razor Keyword)` (for example, `@(functions)`).</span></span>

### <a name="c-razor-keywords"></a><span data-ttu-id="1ebe5-271">C# Razor 키워드</span><span class="sxs-lookup"><span data-stu-id="1ebe5-271">C# Razor keywords</span></span>

* <span data-ttu-id="1ebe5-272">case</span><span class="sxs-lookup"><span data-stu-id="1ebe5-272">case</span></span>
* <span data-ttu-id="1ebe5-273">do</span><span class="sxs-lookup"><span data-stu-id="1ebe5-273">do</span></span>
* <span data-ttu-id="1ebe5-274">default</span><span class="sxs-lookup"><span data-stu-id="1ebe5-274">default</span></span>
* <span data-ttu-id="1ebe5-275">for</span><span class="sxs-lookup"><span data-stu-id="1ebe5-275">for</span></span>
* <span data-ttu-id="1ebe5-276">foreach</span><span class="sxs-lookup"><span data-stu-id="1ebe5-276">foreach</span></span>
* <span data-ttu-id="1ebe5-277">if</span><span class="sxs-lookup"><span data-stu-id="1ebe5-277">if</span></span>
* <span data-ttu-id="1ebe5-278">else</span><span class="sxs-lookup"><span data-stu-id="1ebe5-278">else</span></span>
* <span data-ttu-id="1ebe5-279">lock</span><span class="sxs-lookup"><span data-stu-id="1ebe5-279">lock</span></span>
* <span data-ttu-id="1ebe5-280">switch</span><span class="sxs-lookup"><span data-stu-id="1ebe5-280">switch</span></span>
* <span data-ttu-id="1ebe5-281">try</span><span class="sxs-lookup"><span data-stu-id="1ebe5-281">try</span></span>
* <span data-ttu-id="1ebe5-282">catch</span><span class="sxs-lookup"><span data-stu-id="1ebe5-282">catch</span></span>
* <span data-ttu-id="1ebe5-283">finally</span><span class="sxs-lookup"><span data-stu-id="1ebe5-283">finally</span></span>
* <span data-ttu-id="1ebe5-284">using</span><span class="sxs-lookup"><span data-stu-id="1ebe5-284">using</span></span>
* <span data-ttu-id="1ebe5-285">while</span><span class="sxs-lookup"><span data-stu-id="1ebe5-285">while</span></span>

<span data-ttu-id="1ebe5-286">C# Razor 키워드는 `@(@C# Razor Keyword)`으로 이중 이스케이프되어야 합니다(예: `@(@case)`).</span><span class="sxs-lookup"><span data-stu-id="1ebe5-286">C# Razor keywords must be double-escaped with `@(@C# Razor Keyword)` (for example, `@(@case)`).</span></span> <span data-ttu-id="1ebe5-287">첫 번째 `@`은 Razor 파서를 이스케이프합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-287">The first `@` escapes the Razor parser.</span></span> <span data-ttu-id="1ebe5-288">두 번째 `@`은 C# 파서를 이스케이프합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-288">The second `@` escapes the C# parser.</span></span>

### <a name="reserved-keywords-not-used-by-razor"></a><span data-ttu-id="1ebe5-289">Razor에서 사용하지 않는 예약된 키워드</span><span class="sxs-lookup"><span data-stu-id="1ebe5-289">Reserved keywords not used by Razor</span></span>

* <span data-ttu-id="1ebe5-290">클래스</span><span class="sxs-lookup"><span data-stu-id="1ebe5-290">class</span></span>

## <a name="inspect-the-razor-c-class-generated-for-a-view"></a><span data-ttu-id="1ebe5-291">보기용으로 생성된 Razor C# 클래스 검사</span><span class="sxs-lookup"><span data-stu-id="1ebe5-291">Inspect the Razor C# class generated for a view</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="1ebe5-292">.NET Core SDK 2.1 이상에서는 [Razor SDK](xref:razor-pages/sdk)가 Razor 파일의 컴파일을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-292">With .NET Core SDK 2.1 or later, the [Razor SDK](xref:razor-pages/sdk) handles compilation of Razor files.</span></span> <span data-ttu-id="1ebe5-293">프로젝트를 빌드할 때 Razor SDK는 프로젝트 루트에 *obj/<build_configuration>/<target_framework_moniker>/Razor* 디렉터리를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-293">When building a project, the Razor SDK generates an *obj/<build_configuration>/<target_framework_moniker>/Razor* directory in the project root.</span></span> <span data-ttu-id="1ebe5-294">*Razor* 디렉터리 내의 디렉터리 구조는 프로젝트의 디렉터리 구조를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-294">The directory structure within the *Razor* directory mirrors the project's directory structure.</span></span>

<span data-ttu-id="1ebe5-295">.NET Core 2.1을 대상으로 하는 ASP.NET Core 2.1 Razor Pages 프로젝트에서 다음 디렉터리 구조를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-295">Consider the following directory structure in an ASP.NET Core 2.1 Razor Pages project targeting .NET Core 2.1:</span></span>

* <span data-ttu-id="1ebe5-296">**Areas/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-296">**Areas/**</span></span>
  * <span data-ttu-id="1ebe5-297">**Admin/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-297">**Admin/**</span></span>
    * <span data-ttu-id="1ebe5-298">**Pages/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-298">**Pages/**</span></span>
      * <span data-ttu-id="1ebe5-299">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-299">*Index.cshtml*</span></span>
      * <span data-ttu-id="1ebe5-300">*Index.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-300">*Index.cshtml.cs*</span></span>
* <span data-ttu-id="1ebe5-301">**Pages/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-301">**Pages/**</span></span>
  * <span data-ttu-id="1ebe5-302">**Shared/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-302">**Shared/**</span></span>
    * <span data-ttu-id="1ebe5-303">*_Layout.cshtml*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-303">*_Layout.cshtml*</span></span>
  * <span data-ttu-id="1ebe5-304">*_ViewImports.cshtml*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-304">*_ViewImports.cshtml*</span></span>
  * <span data-ttu-id="1ebe5-305">*_ViewStart.cshtml*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-305">*_ViewStart.cshtml*</span></span>
  * <span data-ttu-id="1ebe5-306">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-306">*Index.cshtml*</span></span>
  * <span data-ttu-id="1ebe5-307">*Index.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-307">*Index.cshtml.cs*</span></span>

<span data-ttu-id="1ebe5-308">*Debug* 구성에 프로젝트를 빌드하면 다음 *obj* 디렉터리가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-308">Building the project in *Debug* configuration yields the following *obj* directory:</span></span>

* <span data-ttu-id="1ebe5-309">**obj/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-309">**obj/**</span></span>
  * <span data-ttu-id="1ebe5-310">**Debug/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-310">**Debug/**</span></span>
    * <span data-ttu-id="1ebe5-311">**netcoreapp2.1/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-311">**netcoreapp2.1/**</span></span>
      * <span data-ttu-id="1ebe5-312">**Razor/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-312">**Razor/**</span></span>
        * <span data-ttu-id="1ebe5-313">**Areas/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-313">**Areas/**</span></span>
          * <span data-ttu-id="1ebe5-314">**Admin/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-314">**Admin/**</span></span>
            * <span data-ttu-id="1ebe5-315">**Pages/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-315">**Pages/**</span></span>
              * <span data-ttu-id="1ebe5-316">*Index.g.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-316">*Index.g.cshtml.cs*</span></span>
        * <span data-ttu-id="1ebe5-317">**Pages/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-317">**Pages/**</span></span>
          * <span data-ttu-id="1ebe5-318">**Shared/**</span><span class="sxs-lookup"><span data-stu-id="1ebe5-318">**Shared/**</span></span>
            * <span data-ttu-id="1ebe5-319">*_Layout.g.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-319">*_Layout.g.cshtml.cs*</span></span>
          * <span data-ttu-id="1ebe5-320">*_ViewImports.g.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-320">*_ViewImports.g.cshtml.cs*</span></span>
          * <span data-ttu-id="1ebe5-321">*_ViewStart.g.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-321">*_ViewStart.g.cshtml.cs*</span></span>
          * <span data-ttu-id="1ebe5-322">*Index.g.cshtml.cs*</span><span class="sxs-lookup"><span data-stu-id="1ebe5-322">*Index.g.cshtml.cs*</span></span>

<span data-ttu-id="1ebe5-323">*pages/Index.cshtml*에 대해 생성된 클래스를 보려면 *obj/Debug/netcoreapp2.1/Razor/Pages/Index.g.cshtml.cs*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-323">To view the generated class for *Pages/Index.cshtml*, open *obj/Debug/netcoreapp2.1/Razor/Pages/Index.g.cshtml.cs*.</span></span>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="1ebe5-324">ASP.NET Core MVC 프로젝트에 다음 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-324">Add the following class to the ASP.NET Core MVC project:</span></span>

[!code-csharp[](razor/sample/Utilities/CustomTemplateEngine.cs)]

<span data-ttu-id="1ebe5-325">`Startup.ConfigureServices`에서 MVC가 추가한 `RazorTemplateEngine`을 `CustomTemplateEngine` 클래스로 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-325">In `Startup.ConfigureServices`, override the `RazorTemplateEngine` added by MVC with the `CustomTemplateEngine` class:</span></span>

[!code-csharp[](razor/sample/Startup.cs?highlight=4&range=10-14)]

<span data-ttu-id="1ebe5-326">`CustomTemplateEngine`의 `return csharpDocument;` 문에서 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-326">Set a breakpoint on the `return csharpDocument;` statement of `CustomTemplateEngine`.</span></span> <span data-ttu-id="1ebe5-327">중단점에서 프로그램 실행이 중지되면 `generatedCode`의 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-327">When program execution stops at the breakpoint, view the value of `generatedCode`.</span></span>

![generatedCode의 텍스트 시각화 도우미 보기](razor/_static/tvr.png)

::: moniker-end

## <a name="view-lookups-and-case-sensitivity"></a><span data-ttu-id="1ebe5-329">보기 조회 및 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="1ebe5-329">View lookups and case sensitivity</span></span>

<span data-ttu-id="1ebe5-330">Razor 보기 엔진은 보기에 대한 대/소문자 구분 조회를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-330">The Razor view engine performs case-sensitive lookups for views.</span></span> <span data-ttu-id="1ebe5-331">그러나 실제 조회는 기본 파일 시스템에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-331">However, the actual lookup is determined by the underlying file system:</span></span>

* <span data-ttu-id="1ebe5-332">파일 기반 원본:</span><span class="sxs-lookup"><span data-stu-id="1ebe5-332">File based source:</span></span>
  * <span data-ttu-id="1ebe5-333">파일 시스템이 대/소문자를 구문하지 않은 운영 체제(예: Windows)에서는 실제 파일 공급자 조회에서 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-333">On operating systems with case insensitive file systems (for example, Windows), physical file provider lookups are case insensitive.</span></span> <span data-ttu-id="1ebe5-334">예를 들어 `return View("Test")`는 */Views/Home/Test.cshtml*, */Views/home/test.cshtml* 및 기타 대/소문자 구분 변형과 일치하는 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-334">For example, `return View("Test")` results in matches for */Views/Home/Test.cshtml*, */Views/home/test.cshtml*, and any other casing variant.</span></span>
  * <span data-ttu-id="1ebe5-335">대/소문자를 구분하는 파일 시스템(예: Linux, OSX 및 `EmbeddedFileProvider`를 사용하는 파일 시스템)에서는 조회 시 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-335">On case-sensitive file systems (for example, Linux, OSX, and with `EmbeddedFileProvider`), lookups are case-sensitive.</span></span> <span data-ttu-id="1ebe5-336">예를 들어 `return View("Test")`는 */Views/Home/Test.cshtml*과 정확히 일치하는 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-336">For example, `return View("Test")` specifically matches */Views/Home/Test.cshtml*.</span></span>
* <span data-ttu-id="1ebe5-337">미리 컴파일된 보기: ASP.NET 2.0 이상을 사용하는 경우 모든 운영 체제에서 미리 컴파일된 보기 조회 시 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-337">Precompiled views: With ASP.NET Core 2.0 and later, looking up precompiled views is case insensitive on all operating systems.</span></span> <span data-ttu-id="1ebe5-338">이 동작은 Windows의 물리적 파일 공급자 동작과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-338">The behavior is identical to physical file provider's behavior on Windows.</span></span> <span data-ttu-id="1ebe5-339">미리 컴파일된 두 보기의 대소문자만 다른 경우 조회 결과가 불명확합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-339">If two precompiled views differ only in case, the result of lookup is non-deterministic.</span></span>

<span data-ttu-id="1ebe5-340">개발자는 파일 및 디렉터리 이름의 대/소문자를 다음의 대/소문자와 매칭하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-340">Developers are encouraged to match the casing of file and directory names to the casing of:</span></span>

* <span data-ttu-id="1ebe5-341">영역, 컨트롤러 및 작업 이름.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-341">Area, controller, and action names.</span></span>
* <span data-ttu-id="1ebe5-342">Razor 페이지.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-342">Razor Pages.</span></span>

<span data-ttu-id="1ebe5-343">대/소문자를 일치시키면 배포 시 기본 파일 시스템에 관계 없이 해당 보기를 잘 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe5-343">Matching case ensures the deployments find their views regardless of the underlying file system.</span></span>
