---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 사용자 지정 HTML 도우미 만들기(C#) | 마이크로 소프트 문서
author: microsoft
description: 이 자습서의 목표는 MVC 보기 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주는 것입니다. HTML 도우미를 활용 하 여...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a2e5a5b42aa5bf267a42fef2fcad7022001ce6f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675333"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="ffda7-104">사용자 지정 HTML 도우미 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="ffda7-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="ffda7-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ffda7-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ffda7-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="ffda7-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="ffda7-107">이 자습서의 목표는 MVC 보기 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="ffda7-108">HTML 도우미를 활용 하 여 표준 HTML 페이지를 만들 려면 수행 해야 하는 HTML 태그의 지루한 입력의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="ffda7-109">이 자습서의 목표는 MVC 보기 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="ffda7-110">HTML 도우미를 활용 하 여 표준 HTML 페이지를 만들 려면 수행 해야 하는 HTML 태그의 지루한 입력의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="ffda7-111">이 자습서의 첫 번째 부분에서는 ASP.NET MVC 프레임워크에 포함된 기존 HTML 도우미 중 일부를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="ffda7-112">다음으로 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="ffda7-113">HTML 도우미 이해</span><span class="sxs-lookup"><span data-stu-id="ffda7-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="ffda7-114">HTML 도우미는 문자열을 반환 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="ffda7-115">문자열은 원하는 모든 유형의 콘텐츠를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="ffda7-116">예를 들어 HTML 도우미를 사용하여 HTML `<input>` 및 태그와 `<img>` 같은 표준 HTML 태그를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="ffda7-117">또한 HTML 도우미를 사용하여 탭 스트립이나 데이터베이스 데이터의 HTML 테이블과 같은 보다 복잡한 콘텐츠를 렌더링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="ffda7-118">ASP.NET MVC 프레임워크에는 다음과 같은 표준 HTML 도우미 집합이 포함되어 있습니다(전체 목록은 아닙니다).</span><span class="sxs-lookup"><span data-stu-id="ffda7-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="ffda7-119">Html.액션링크()</span><span class="sxs-lookup"><span data-stu-id="ffda7-119">Html.ActionLink()</span></span>
- <span data-ttu-id="ffda7-120">Html.시작 양식()</span><span class="sxs-lookup"><span data-stu-id="ffda7-120">Html.BeginForm()</span></span>
- <span data-ttu-id="ffda7-121">Html.체크 박스()</span><span class="sxs-lookup"><span data-stu-id="ffda7-121">Html.CheckBox()</span></span>
- <span data-ttu-id="ffda7-122">Html.드롭다운리스트()</span><span class="sxs-lookup"><span data-stu-id="ffda7-122">Html.DropDownList()</span></span>
- <span data-ttu-id="ffda7-123">Html.엔드폼()</span><span class="sxs-lookup"><span data-stu-id="ffda7-123">Html.EndForm()</span></span>
- <span data-ttu-id="ffda7-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="ffda7-124">Html.Hidden()</span></span>
- <span data-ttu-id="ffda7-125">Html.리스트박스()</span><span class="sxs-lookup"><span data-stu-id="ffda7-125">Html.ListBox()</span></span>
- <span data-ttu-id="ffda7-126">Html.암호()</span><span class="sxs-lookup"><span data-stu-id="ffda7-126">Html.Password()</span></span>
- <span data-ttu-id="ffda7-127">Html.라디오 버튼()</span><span class="sxs-lookup"><span data-stu-id="ffda7-127">Html.RadioButton()</span></span>
- <span data-ttu-id="ffda7-128">Html.텍스트 영역()</span><span class="sxs-lookup"><span data-stu-id="ffda7-128">Html.TextArea()</span></span>
- <span data-ttu-id="ffda7-129">Html.텍스트 상자()</span><span class="sxs-lookup"><span data-stu-id="ffda7-129">Html.TextBox()</span></span>

<span data-ttu-id="ffda7-130">예를 들어 목록 1의 양식을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="ffda7-131">이 양식은 표준 HTML 도우미 두 대의 도움을 받아 렌더링됩니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="ffda7-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="ffda7-132">이 양식은 `Html.BeginForm()` `Html.TextBox()` 및 도우미 메서드를 사용하여 간단한 HTML 양식을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="ffda7-133">[![HTML 도우미로 렌더링된 페이지](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ffda7-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="ffda7-134">**그림 01**: HTML 도우미로 렌더링된[페이지(전체 크기 이미지를 보려면 클릭)](creating-custom-html-helpers-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ffda7-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="ffda7-135">**리스팅 1 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ffda7-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="ffda7-136">Html.BeginForm() 도우미 메서드는 HTML `<form>` 태그를 열고 닫는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="ffda7-137">메서드는 `Html.BeginForm()` using 문 내에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="ffda7-138">using 문은 사용 블록의 `<form>` 끝에서 태그가 닫히도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="ffda7-139">원하는 경우 사용 블록을 만드는 대신 Html.EndForm() 도우미 메서드를 호출하여 `<form>` 태그를 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="ffda7-140">가장 직관적인 것처럼 보이는 열기 `<form>` 및 닫기 태그를 만들 려면 어떤 접근 방식을 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="ffda7-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="ffda7-141">도우미 `Html.TextBox()` 메서드는 목록 1에서 HTML `<input>` 태그를 렌더링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="ffda7-142">브라우저에서 소스 보기를 선택하면 목록 2에 HTML 소스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="ffda7-143">원본에 표준 HTML 태그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffda7-144">`Html.TextBox()`-HTML 도우미는 `<% %>` 태그 대신 태그로 `<%= %>` 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="ffda7-145">동일한 기호를 포함하지 않으면 브라우저에 렌더링되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="ffda7-146">ASP.NET MVC 프레임워크에는 작은 도우미 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="ffda7-147">대부분의 경우 사용자 지정 HTML 도우미를 사용하여 MVC 프레임워크를 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="ffda7-148">이 자습서의 나머지 부분에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="ffda7-149">**리스팅 2 –`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="ffda7-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="ffda7-150">정적 메소드를 사용 하 고 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="ffda7-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="ffda7-151">새 HTML 도우미를 만드는 가장 쉬운 방법은 문자열을 반환 하는 정적 메서드를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="ffda7-152">예를 들어 HTML `<label>` 태그를 렌더링하는 새 HTML 도우미를 만들기로 결정한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="ffda7-153">목록 2의 클래스를 사용하여 `<label>` 을 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="ffda7-154">**리스팅 2 –`Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="ffda7-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="ffda7-155">목록 2의 클래스에 대해 특별한 것은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="ffda7-156">메서드는 `Label()` 단순히 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="ffda7-157">목록 3의 수정된 인덱스 `LabelHelper` 보기는 `<label>` HTML 태그를 렌더링하는 데 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="ffda7-158">`Application1.Helpers` 보기에는 네임스페이스를 `<%@ imports %>` 가져오는 지시문이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="ffda7-159">**리스팅 2 –`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ffda7-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="ffda7-160">확장 방법을 사용 하 고 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="ffda7-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="ffda7-161">ASP.NET MVC 프레임워크에 포함된 표준 HTML 도우미와 마찬가지로 작동하는 HTML 도우미를 만들려면 확장 메서드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="ffda7-162">확장 메서드를 사용하면 기존 클래스에 새 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="ffda7-163">HTML 도우미 메서드를 만들 때 뷰의 Html 속성으로 표시되는 HtmlHelper 클래스에 새 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="ffda7-164">목록 3의 클래스는 명명된 `HtmlHelper` `Label()`클래스에 확장 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="ffda7-165">이 클래스에 대해 알아두어야 할 몇 가지 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="ffda7-166">먼저 클래스가 정적 클래스임을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="ffda7-167">정적 클래스를 사용하여 확장 메서드를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="ffda7-168">둘째, `Label()` 메서드의 첫 번째 매개 변수 앞에 키워드가 `this`앞에 옵니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="ffda7-169">확장 메서드의 첫 번째 매개 변수는 확장 메서드가 확장되는 클래스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="ffda7-170">**리스팅 3 –`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="ffda7-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="ffda7-171">확장 메서드를 만들고 응용 프로그램을 성공적으로 빌드하면 확장 메서드가 클래스의 다른 모든 메서드와 마찬가지로 Visual Studio Intellisense에 나타납니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="ffda7-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="ffda7-172">유일한 차이점은 확장 메서드 옆에 특수 기호(아래쪽 화살표아이콘)가 표시된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="ffda7-173">[![Html.Label() 확장 메서드 사용](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ffda7-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="ffda7-174">**그림 02**: Html.Label() 확장 방법을 사용하여[(전체 크기 이미지를 보려면 클릭하십시오)](creating-custom-html-helpers-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="ffda7-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="ffda7-175">목록 4의 수정된 인덱스 보기는 Html.Label() 확장 `<label>` 메서드를 사용하여 모든 태그를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="ffda7-176">**리스팅 4 –`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ffda7-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="ffda7-177">요약</span><span class="sxs-lookup"><span data-stu-id="ffda7-177">Summary</span></span>

<span data-ttu-id="ffda7-178">이 자습서에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="ffda7-179">먼저 문자열을 반환하는 정적 `Label()` 메서드를 만들어 사용자 지정 HTML 도우미를 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="ffda7-180">다음으로 클래스에 확장 메서드를 `Label()` 만들어 사용자 지정 HTML 도우미 `HtmlHelper` 메서드를 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="ffda7-181">이 자습서에서는 매우 간단한 HTML 도우미 메서드를 빌드하는 데 중점을 두어 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="ffda7-182">HTML 도우미는 원하는 만큼 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="ffda7-183">트리 보기, 메뉴 또는 데이터베이스 데이터 테이블과 같은 풍부한 콘텐츠를 렌더링하는 HTML 도우미를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffda7-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ffda7-184">[이전](asp-net-mvc-views-overview-cs.md)
> [다음](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ffda7-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
