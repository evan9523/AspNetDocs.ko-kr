---
title: ASP.NET Core의 태그 도우미
author: rick-anderson
description: 태그 도우미란 무엇이며 ASP.NET Core에서 어떻게 사용하는지 알아봅니다.
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2018
uid: mvc/views/tag-helpers/intro
ms.openlocfilehash: 4b9bceb3ce0153af2d9a30c402febe09707145b7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041240"
---
# <a name="tag-helpers-in-aspnet-core"></a><span data-ttu-id="832d0-103">ASP.NET Core의 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="832d0-103">Tag Helpers in ASP.NET Core</span></span>

<span data-ttu-id="832d0-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="832d0-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="what-are-tag-helpers"></a><span data-ttu-id="832d0-105">태그 도우미란?</span><span class="sxs-lookup"><span data-stu-id="832d0-105">What are Tag Helpers?</span></span>

<span data-ttu-id="832d0-106">태그 도우미를 사용하면 서버 쪽 코드를 Razor 파일에서 HTML 요소를 만들고 렌더링하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-106">Tag Helpers enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span> <span data-ttu-id="832d0-107">예를 들어 기본 제공 `ImageTagHelper`는 이미지 이름에 버전 번호를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-107">For example, the built-in `ImageTagHelper` can append a version number to the image name.</span></span> <span data-ttu-id="832d0-108">이미지가 변경될 때마다 서버에서 이미지에 대한 고유 버전을 새로 생성하므로 클라이언트는 항상 최신 이미지를 가져옵니다(오래된 캐시된 이미지 대신).</span><span class="sxs-lookup"><span data-stu-id="832d0-108">Whenever the image changes, the server generates a new unique version for the image, so clients are guaranteed to get the current image (instead of a stale cached image).</span></span> <span data-ttu-id="832d0-109">양식 작성, 링크, 자산 로드 등의 일반적인 작업을 위한 여러 가지 기본 제공 태그 도우미가 있으며, 공용 GitHub 리포지토리 및 NuGet 패키지로도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-109">There are many built-in Tag Helpers for common tasks - such as creating forms, links, loading assets and more - and even more available in public GitHub repositories and as NuGet packages.</span></span> <span data-ttu-id="832d0-110">태그 도우미는 C#에서 작성되며 요소 이름, 특성 이름 또는 부모 태그 기반의 HTML 요소를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-110">Tag Helpers are authored in C#, and they target HTML elements based on element name, attribute name, or parent tag.</span></span> <span data-ttu-id="832d0-111">예를 들어 기본 제공 `LabelTagHelper`는 `LabelTagHelper` 특성이 적용될 때 HTML `<label>` 요소를 대상으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-111">For example, the built-in `LabelTagHelper` can target the HTML `<label>` element when the `LabelTagHelper` attributes are applied.</span></span> <span data-ttu-id="832d0-112">[HTML 도우미](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers)에 익숙한 경우 태그 도우미를 사용하면 Razor 보기에서 HTML과 C# 간의 명시적 전환이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-112">If you're familiar with [HTML Helpers](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers), Tag Helpers reduce the explicit transitions between HTML and C# in Razor views.</span></span> <span data-ttu-id="832d0-113">많은 경우 HTML 도우미는 특정 태그 도우미에 대한 대체 방법을 제공하지만, 태그 도우미는 HTML 도우미를 대체하지 않으며 각 HTML 도우미에 대한 태그 도우미가 없다는 사실을 인지하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-113">In many cases, HTML Helpers provide an alternative approach to a specific Tag Helper, but it's important to recognize that Tag Helpers don't replace HTML Helpers and there's not a Tag Helper for each HTML Helper.</span></span> <span data-ttu-id="832d0-114">[HTML 도우미와 비교한 태그 도우미](#tag-helpers-compared-to-html-helpers)를 보시면 차이점이 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-114">[Tag Helpers compared to HTML Helpers](#tag-helpers-compared-to-html-helpers) explains the differences in more detail.</span></span>

## <a name="what-tag-helpers-provide"></a><span data-ttu-id="832d0-115">태그 도우미가 제공하는 기능</span><span class="sxs-lookup"><span data-stu-id="832d0-115">What Tag Helpers provide</span></span>

<span data-ttu-id="832d0-116">**HTML에 적합한 개발 환경** 대부분 태그 도우미를 사용한 Razor 태그는 표준 HTML과 비슷하게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-116">**An HTML-friendly development experience** For the most part, Razor markup using Tag Helpers looks like standard HTML.</span></span> <span data-ttu-id="832d0-117">HTML/CSS/JavaScript에 익숙한 프런트 엔드 디자이너는 C# Razor 구문을 배우지 않아도 Razor를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-117">Front-end designers conversant with HTML/CSS/JavaScript can edit Razor without learning C# Razor syntax.</span></span>

<span data-ttu-id="832d0-118">**HTML 및 Razor 태그를 만드는 다양한 IntelliSense 환경** 이것이 바로 Razor 보기에서 서버 쪽 태그 생성에 대한 이전 접근 방식을 사용하는 HTML 도우미와 명확하게 다른 점입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-118">**A rich IntelliSense environment for creating HTML and Razor markup** This is in sharp contrast to HTML Helpers, the previous approach to server-side creation of markup in Razor views.</span></span> <span data-ttu-id="832d0-119">[HTML 도우미와 비교한 태그 도우미](#tag-helpers-compared-to-html-helpers)를 보시면 차이점이 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-119">[Tag Helpers compared to HTML Helpers](#tag-helpers-compared-to-html-helpers) explains the differences in more detail.</span></span> <span data-ttu-id="832d0-120">[태그 도우미에 IntelliSense 지원](#intellisense-support-for-tag-helpers)을 보시면 IntelliSense 환경에 대해 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-120">[IntelliSense support for Tag Helpers](#intellisense-support-for-tag-helpers) explains the IntelliSense environment.</span></span> <span data-ttu-id="832d0-121">심지어 Razor C# 구문에 익숙한 개발자는 태그 도우미를 사용하면 C# Razor 태그를 작성하는 것보다 생산성이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-121">Even developers experienced with Razor C# syntax are more productive using Tag Helpers than writing C# Razor markup.</span></span>

<span data-ttu-id="832d0-122">**생산성을 높이고 서버에만 제공되는 정보를 사용하여 보다 강력하고 안정적이고 유지 가능한 코드를 작성하는 방법** 예를 들어 지금까지는 이미지를 변경하면 이미지 이름도 변경하는 것이 이미지 업데이트의 원칙이었습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-122">**A way to make you more productive and able to produce more robust, reliable, and maintainable code using information only available on the server** For example, historically the mantra on updating images was to change the name of the image when you change the image.</span></span> <span data-ttu-id="832d0-123">성능상의 이유로 이미지를 적극적으로 캐시해야 하며, 이미지 이름을 변경하지 않는 한 클라이언트가 오래된 복사본으로 전락할 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-123">Images should be aggressively cached for performance reasons, and unless you change the name of an image, you risk clients getting a stale copy.</span></span> <span data-ttu-id="832d0-124">지금까지는 이미지가 편집되면 이름을 변경하고 웹앱의 이미지에 대한 각 참조를 업데이트해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-124">Historically, after an image was edited, the name had to be changed and each reference to the image in the web app needed to be updated.</span></span> <span data-ttu-id="832d0-125">이 작업은 매우 많은 인력이 필요할 뿐 아니라 오류 가능성이 높습니다(참조를 누락하거나 실수로 잘못된 문자열을 입력하는 등). 기본 제공 `ImageTagHelper`는 이 작업을 자동으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-125">Not only is this very labor intensive, it's also error prone (you could miss a reference, accidentally enter the wrong string, etc.) The built-in `ImageTagHelper` can do this for you automatically.</span></span> <span data-ttu-id="832d0-126">`ImageTagHelper`는 이미지 이름에 버전 번호를 추가할 수 있으며, 따라서 이미지가 변경될 때마다 서버에서 자동으로 이미지의 새 고유 버전을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-126">The `ImageTagHelper` can append a version number to the image name, so whenever the image changes, the server automatically generates a new unique version for the image.</span></span> <span data-ttu-id="832d0-127">클라이언트는 항상 최신 이미지를 가져오게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-127">Clients are guaranteed to get the current image.</span></span> <span data-ttu-id="832d0-128">`ImageTagHelper`를 사용하면 이와 같은 견고함과 노동력 절감 효과를 근본적으로 무료로 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-128">This robustness and labor savings comes essentially free by using the `ImageTagHelper`.</span></span>

<span data-ttu-id="832d0-129">대부분의 기본 제공 태그 도우미는 표준 HTML 요소를 대상으로 하며 요소에 대한 서버 쪽 특성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-129">Most built-in Tag Helpers target standard HTML elements and provide server-side attributes for the element.</span></span> <span data-ttu-id="832d0-130">예를 들어 *보기/계정* 폴더의 여러 보기에서 사용되는 `<input>` 요소에는 `asp-for` 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-130">For example, the `<input>` element used in many views in the *Views/Account* folder contains the `asp-for` attribute.</span></span> <span data-ttu-id="832d0-131">이 특성은 지정된 모델 속성의 이름을 렌더링된 HTML로 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-131">This attribute extracts the name of the specified model property into the rendered HTML.</span></span> <span data-ttu-id="832d0-132">다음 모델과 함께 Razor 보기를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-132">Consider a Razor view with the following model:</span></span>

```csharp
public class Movie
{
    public int ID { get; set; }
    public string Title { get; set; }
    public DateTime ReleaseDate { get; set; }
    public string Genre { get; set; }
    public decimal Price { get; set; }
}
```

<span data-ttu-id="832d0-133">다음 Razor 태그는 다음과 같은 일을 합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-133">The following Razor markup:</span></span>

```cshtml
<label asp-for="Movie.Title"></label>
```

<span data-ttu-id="832d0-134">다음 HTML을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-134">Generates the following HTML:</span></span>

```html
<label for="Movie_Title">Title</label>
```

<span data-ttu-id="832d0-135">`asp-for` 특성은 [LabelTagHelper](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.labeltaghelper?view=aspnetcore-2.0)의 `For` 속성에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-135">The `asp-for` attribute is made available by the `For` property in the [LabelTagHelper](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.labeltaghelper?view=aspnetcore-2.0).</span></span> <span data-ttu-id="832d0-136">자세한 내용은 [태그 도우미 작성](xref:mvc/views/tag-helpers/authoring)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="832d0-136">See [Author Tag Helpers](xref:mvc/views/tag-helpers/authoring) for more information.</span></span>

## <a name="managing-tag-helper-scope"></a><span data-ttu-id="832d0-137">태그 도우미 범위 관리</span><span class="sxs-lookup"><span data-stu-id="832d0-137">Managing Tag Helper scope</span></span>

<span data-ttu-id="832d0-138">태그 도우미 범위는 `@addTagHelper`, `@removeTagHelper` 및 "!" 옵트아웃 문자를 조합하여 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-138">Tag Helpers scope is controlled by a combination of `@addTagHelper`, `@removeTagHelper`, and the "!" opt-out character.</span></span>

<a name="add-helper-label"></a>

### <a name="addtaghelper-makes-tag-helpers-available"></a><span data-ttu-id="832d0-139">`@addTagHelper`는 태그 도우미를 사용할 수 있도록 설정</span><span class="sxs-lookup"><span data-stu-id="832d0-139">`@addTagHelper` makes Tag Helpers available</span></span>

<span data-ttu-id="832d0-140">*AuthoringTagHelpers*라는 새 ASP.NET Core 웹앱을 만들면 다음과 같은 *Views/_ViewImports.cshtml* 파일이 프로젝트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-140">If you create a new ASP.NET Core web app named *AuthoringTagHelpers*, the following *Views/_ViewImports.cshtml* file will be added to your project:</span></span>

[!code-cshtml[](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopy.cshtml?highlight=2&range=2-3)]

<span data-ttu-id="832d0-141">`@addTagHelper` 지시문은 태그 도우미를 보기에 사용할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-141">The `@addTagHelper` directive makes Tag Helpers available to the view.</span></span> <span data-ttu-id="832d0-142">이 예에서 보기 파일은 *Pages/_ViewImports.cshtml*이며, 기본적으로 *Pages* 폴더 및 하위 폴더에 있는 모든 파일에서 이 파일을 상속하므로 태그 도우미를 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-142">In this case, the view file is *Pages/_ViewImports.cshtml*, which by default is inherited by all files in the *Pages* folder and subfolders; making Tag Helpers available.</span></span> <span data-ttu-id="832d0-143">위의 코드에서는 와일드카드 구문("\*")을 사용하여 지정된 어셈블리의 모든 태그 도우미(*Microsoft.AspNetCore.Mvc.TagHelpers*)를 *보기* 디렉터리 또는 하위 디렉터리에 있는 모든 보기 파일에서 사용할 수 있도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-143">The code above uses the wildcard syntax ("\*") to specify that all Tag Helpers in the specified assembly (*Microsoft.AspNetCore.Mvc.TagHelpers*) will be available to every view file in the *Views* directory or subdirectory.</span></span> <span data-ttu-id="832d0-144">`@addTagHelper` 뒤에 나오는 첫 번째 매개 변수는 로드할 태그 도우미를 지정하고(여기서는 모든 태그 도우미에 "\*" 사용), 두 번째 매개 변수 "Microsoft.AspNetCore.Mvc.TagHelpers"는 태그 도우미를 포함하는 어셈블리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-144">The first parameter after `@addTagHelper` specifies the Tag Helpers to load (we are using "\*" for all Tag Helpers), and the second parameter "Microsoft.AspNetCore.Mvc.TagHelpers" specifies the assembly containing the Tag Helpers.</span></span> <span data-ttu-id="832d0-145">*Microsoft.AspNetCore.Mvc.TagHelpers*는 기본 제공 ASP.NET Core 태그 도우미에 대한 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-145">*Microsoft.AspNetCore.Mvc.TagHelpers* is the assembly for the built-in ASP.NET Core Tag Helpers.</span></span>

<span data-ttu-id="832d0-146">이 프로젝트의 모든 태그 도우미(*AuthoringTagHelpers*라는 어셈블리를 만드는)를 노출하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-146">To expose all of the Tag Helpers in this project (which creates an assembly named *AuthoringTagHelpers*), you would use the following:</span></span>

[!code-cshtml[](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopy.cshtml?highlight=3)]

<span data-ttu-id="832d0-147">기본 네임스페이스(`AuthoringTagHelpers.TagHelpers.EmailTagHelper`)가 있는 `EmailTagHelper`가 프로젝트에 포함된 경우 태그 도우미의 FQN(정규화된 이름)을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-147">If your project contains an `EmailTagHelper` with the default namespace (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), you can provide the fully qualified name (FQN) of the Tag Helper:</span></span>

```cshtml
@using AuthoringTagHelpers
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.EmailTagHelper, AuthoringTagHelpers
```

<span data-ttu-id="832d0-148">FQN을 사용하여 보기에 태그 도우미를 추가하려면 먼저 FQN(`AuthoringTagHelpers.TagHelpers.EmailTagHelper`)을 추가한 후 어셈블리 이름(*AuthoringTagHelpers*)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-148">To add a Tag Helper to a view using an FQN, you first add the FQN (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), and then the assembly name (*AuthoringTagHelpers*).</span></span> <span data-ttu-id="832d0-149">대부분의 개발자는 "\*" 와일드카드 구문을 사용하는 방법을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-149">Most developers prefer to use the  "\*" wildcard syntax.</span></span> <span data-ttu-id="832d0-150">와일드카드 구문을 사용하면 "\*" 와일드카드 문자를 FQN에 접미사로 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-150">The wildcard syntax allows you to insert the wildcard character "\*" as the suffix in an FQN.</span></span> <span data-ttu-id="832d0-151">예를 들어 다음 지시문은 `EmailTagHelper`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-151">For example, any of the following directives will bring in the `EmailTagHelper`:</span></span>

```cshtml
@addTagHelper AuthoringTagHelpers.TagHelpers.E*, AuthoringTagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.Email*, AuthoringTagHelpers
```

<span data-ttu-id="832d0-152">앞서 언급했듯이, *Views/_ViewImports.cshtml* 파일에 `@addTagHelper` 지시문을 추가하면 *보기* 디렉터리 및 하위 디렉터리에 있는 모든 보기 파일에서 태그 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-152">As mentioned previously, adding the `@addTagHelper` directive to the *Views/_ViewImports.cshtml* file makes the Tag Helper available to all view files in the *Views* directory and subdirectories.</span></span> <span data-ttu-id="832d0-153">특정 보기에만 태그 도우미를 노출하도록 옵트인하려면 특정 보기 파일에서 `@addTagHelper` 지시문을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-153">You can use the `@addTagHelper` directive in specific view files if you want to opt-in to exposing the Tag Helper to only those views.</span></span>

<a name="remove-razor-directives-label"></a>

### <a name="removetaghelper-removes-tag-helpers"></a><span data-ttu-id="832d0-154">`@removeTagHelper`로 태그 도우미 제거</span><span class="sxs-lookup"><span data-stu-id="832d0-154">`@removeTagHelper` removes Tag Helpers</span></span>

<span data-ttu-id="832d0-155">`@removeTagHelper`는 `@addTagHelper`와 동일한 두 개의 매개 변수를 갖고 있으며, 이전에 추가된 태그 도우미를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-155">The `@removeTagHelper` has the same two parameters as `@addTagHelper`, and it removes a Tag Helper that was previously added.</span></span> <span data-ttu-id="832d0-156">예를 들어 특정 보기에 적용된 `@removeTagHelper`는 보기에서 지정된 태그 도우미를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-156">For example, `@removeTagHelper` applied to a specific view removes the specified Tag Helper from the view.</span></span> <span data-ttu-id="832d0-157">*Views/Folder/_ViewImports.cshtml* 파일에 `@removeTagHelper`를 사용하면 *폴더*에 있는 모든 보기에서 지정된 태그 도우미가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-157">Using `@removeTagHelper` in a *Views/Folder/_ViewImports.cshtml* file removes the specified Tag Helper from all of the views in *Folder*.</span></span>

### <a name="controlling-tag-helper-scope-with-the-viewimportscshtml-file"></a><span data-ttu-id="832d0-158">*_ViewImports.cshtml* 파일을 사용하여 태그 도우미 범위 제어</span><span class="sxs-lookup"><span data-stu-id="832d0-158">Controlling Tag Helper scope with the *_ViewImports.cshtml* file</span></span>

<span data-ttu-id="832d0-159">보기 폴더에 *_ViewImports.cshtml*을 추가할 수 있습니다. 그러면 보기 엔진이 해당 파일과 *Views/_ViewImports.cshtml* 파일의 지시문을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-159">You can add a *_ViewImports.cshtml* to any view folder, and the view engine applies the directives from both that file and the *Views/_ViewImports.cshtml* file.</span></span> <span data-ttu-id="832d0-160">*홈* 보기에 대한 비어 있는 *Views/Home/_ViewImports.cshtml* 파일을 추가한 경우 변경되는 내용이 없습니다. *_ViewImports.cshtml* 파일은 추가 파일이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-160">If you added an empty *Views/Home/_ViewImports.cshtml* file for the *Home* views, there would be no change because the *_ViewImports.cshtml* file is additive.</span></span> <span data-ttu-id="832d0-161">*Views/Home/_ViewImports.cshtml* 파일(기본 *Views/_ViewImports.cshtml* 파일에 없음)에 추가되는 `@addTagHelper` 지시문은 *홈* 폴더에 있는 보기에만 태그 도우미를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-161">Any `@addTagHelper` directives you add to the *Views/Home/_ViewImports.cshtml* file (that are not in the default *Views/_ViewImports.cshtml* file) would expose those Tag Helpers to views only in the *Home* folder.</span></span>

<a name="opt-out"></a>

### <a name="opting-out-of-individual-elements"></a><span data-ttu-id="832d0-162">개별 요소 옵트아웃</span><span class="sxs-lookup"><span data-stu-id="832d0-162">Opting out of individual elements</span></span>

<span data-ttu-id="832d0-163">태그 도우미 옵트아웃 문자("!")를 사용하여 요소 수준에서 태그 도우미를 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-163">You can disable a Tag Helper at the element level with the Tag Helper opt-out character ("!").</span></span> <span data-ttu-id="832d0-164">예를 들어 다음과 같은 태그 도우미 옵트아웃 문자를 사용하여 `<span>`에서 `Email` 유효성 검사가 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-164">For example, `Email` validation is disabled in the `<span>` with the Tag Helper opt-out character:</span></span>

```cshtml
<!span asp-validation-for="Email" class="text-danger"></!span>
```

<span data-ttu-id="832d0-165">여는 태그와 닫는 태그에 태그 도우미 옵트아웃 문자를 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-165">You must apply the Tag Helper opt-out character to the opening and closing tag.</span></span> <span data-ttu-id="832d0-166">(여는 태그에 옵트아웃 문자를 추가하면 Visual Studio 편집기가 자동으로 닫는 태그에 옵트아웃 문자를 추가합니다).</span><span class="sxs-lookup"><span data-stu-id="832d0-166">(The Visual Studio editor automatically adds the opt-out character to the closing tag when you add one to the opening tag).</span></span> <span data-ttu-id="832d0-167">옵트아웃 문자를 추가하면 요소 및 태그 도우미 특성이 더 이상 구별되는 글꼴로 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-167">After you add the opt-out character, the element and Tag Helper attributes are no longer displayed in a distinctive font.</span></span>

<a name="prefix-razor-directives-label"></a>

### <a name="using-taghelperprefix-to-make-tag-helper-usage-explicit"></a><span data-ttu-id="832d0-168">`@tagHelperPrefix`를 사용하여 태그 도우미 사용을 명시적으로 만들기</span><span class="sxs-lookup"><span data-stu-id="832d0-168">Using `@tagHelperPrefix` to make Tag Helper usage explicit</span></span>

<span data-ttu-id="832d0-169">`@tagHelperPrefix` 지시문을 사용하면 태그 도우미를 지원하고 태그 도우미 사용을 명시적으로 만들도록 태그 접두사 문자열을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-169">The `@tagHelperPrefix` directive allows you to specify a tag prefix string to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> <span data-ttu-id="832d0-170">예를 들어 *Views/_ViewImports.cshtml* 파일에 다음 태그를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-170">For example, you could add the following markup to the *Views/_ViewImports.cshtml* file:</span></span>

```cshtml
@tagHelperPrefix th:
```
<span data-ttu-id="832d0-171">아래의 코드 이미지에서 태그 도우미 접두사가 `th:`로 지정되고, 따라서 `th:` 접두사를 사용하는 요소만 태그 도우미를 지원합니다(태그 도우미 지원 요소에는 고유한 글꼴이 있음).</span><span class="sxs-lookup"><span data-stu-id="832d0-171">In the code image below, the Tag Helper prefix is set to `th:`, so only those elements using the prefix `th:` support Tag Helpers (Tag Helper-enabled elements have a distinctive font).</span></span> <span data-ttu-id="832d0-172">`<label>` 및 `<input>` 요소는 태그 도우미 접두사가 있고 태그 도우미를 사용할 수 있지만 `<span>` 요소는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-172">The `<label>` and `<input>` elements have the Tag Helper prefix and are Tag Helper-enabled, while the `<span>` element doesn't.</span></span>

![이미지](intro/_static/thp.png)

<span data-ttu-id="832d0-174">`@addTagHelper`에 적용되는 동일한 계층 규칙이 `@tagHelperPrefix`에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-174">The same hierarchy rules that apply to `@addTagHelper` also apply to `@tagHelperPrefix`.</span></span>

## <a name="self-closing-tag-helpers"></a><span data-ttu-id="832d0-175">자체 닫는 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="832d0-175">Self-closing Tag Helpers</span></span>

<span data-ttu-id="832d0-176">여러 태그 도우미를 자체 닫는 태그로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-176">Many Tag Helpers can't be used as self-closing tags.</span></span> <span data-ttu-id="832d0-177">일부 태그 도우미는 자체 닫는 태그로 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-177">Some Tag Helpers are designed to be self-closing tags.</span></span> <span data-ttu-id="832d0-178">자체 닫는 태그로 설계되지 않은 태그 도우미를 사용하면 렌더링된 출력이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-178">Using a Tag Helper that was not designed to be self-closing suppresses the rendered output.</span></span> <span data-ttu-id="832d0-179">태그 도우미를 자체적으로 닫으면 렌더링된 출력에 자체 닫는 태그가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-179">Self-closing a Tag Helper results in a self-closing tag in the rendered output.</span></span> <span data-ttu-id="832d0-180">자세한 내용은 [태그 도우미 작성](xref:mvc/views/tag-helpers/authoring)에서 [이 메모](xref:mvc/views/tag-helpers/authoring#self-closing)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="832d0-180">For more information, see [this note](xref:mvc/views/tag-helpers/authoring#self-closing) in [Authoring Tag Helpers](xref:mvc/views/tag-helpers/authoring).</span></span>

## <a name="intellisense-support-for-tag-helpers"></a><span data-ttu-id="832d0-181">태그 도우미에 대한 IntelliSense 지원</span><span class="sxs-lookup"><span data-stu-id="832d0-181">IntelliSense support for Tag Helpers</span></span>

<span data-ttu-id="832d0-182">Visual Studio에서 새 ASP.NET Core 웹앱을 만들면 "Microsoft.AspNetCore.Razor.Tools" NuGet 패키지가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-182">When you create a new ASP.NET Core web app in Visual Studio, it adds the NuGet package "Microsoft.AspNetCore.Razor.Tools".</span></span> <span data-ttu-id="832d0-183">이 패키지는 태그 도우미 도구를 추가하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-183">This is the package that adds Tag Helper tooling.</span></span>

<span data-ttu-id="832d0-184">HTML `<label>` 요소를 작성하는 방안을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="832d0-184">Consider writing an HTML `<label>` element.</span></span> <span data-ttu-id="832d0-185">Visual Studio 편집기에서 `<l`를 입력하는 즉시 IntelliSense는 일치하는 요소를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-185">As soon as you enter `<l` in the Visual Studio editor, IntelliSense displays matching elements:</span></span>

![이미지](intro/_static/label.png)

<span data-ttu-id="832d0-187">HTML 도움말뿐 아니라 아이콘(그 아래에 있는 "@" symbol with "<>")도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-187">Not only do you get HTML help, but the icon (the "@" symbol with "<>" under it).</span></span>

![이미지](intro/_static/tagSym.png)

<span data-ttu-id="832d0-189">태그 도우미의 대상으로 요소를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-189">identifies the element as targeted by Tag Helpers.</span></span> <span data-ttu-id="832d0-190">순수 HTML 요소(예: `fieldset`)는 "<>" 아이콘을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-190">Pure HTML elements (such as the `fieldset`) display the "<>" icon.</span></span>

<span data-ttu-id="832d0-191">순수 HTML `<label>` 태그는 HTML 태그를(기본 Visual Studio 색 테마가 있는)를 갈색 글꼴로, 특성을 빨간색으로, 특성 값을 파란색으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-191">A pure HTML `<label>` tag displays the HTML tag (with the default Visual Studio color theme) in a brown font, the attributes in red, and the attribute values in blue.</span></span>

![이미지](intro/_static/LableHtmlTag.png)

<span data-ttu-id="832d0-193">`<label`을 입력하면 IntelliSense가 사용 가능한 HTML/CSS 특성 및 태그 도우미 대상 특성을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-193">After you enter `<label`, IntelliSense lists the available HTML/CSS attributes and the Tag Helper-targeted attributes:</span></span>

![이미지](intro/_static/labelattr.png)

<span data-ttu-id="832d0-195">IntelliSense 문을 완성하면 탭 키를 입력하여 선택한 값으로 문을 완성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-195">IntelliSense statement completion allows you to enter the tab key to complete the statement with the selected value:</span></span>

![이미지](intro/_static/stmtcomplete.png)

<span data-ttu-id="832d0-197">태그 도우미 특성을 입력하는 즉시 태그 및 특성 글꼴이 변합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-197">As soon as a Tag Helper attribute is entered, the tag and attribute fonts change.</span></span> <span data-ttu-id="832d0-198">기본 Visual Studio "파란색" 또는 "밝은" 색 테마를 사용하면 글꼴은 자주색 볼드입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-198">Using the default Visual Studio "Blue" or "Light" color theme, the font is bold purple.</span></span> <span data-ttu-id="832d0-199">"어두운" 테마를 사용하면 글꼴은 청록색 볼드입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-199">If you're using the "Dark" theme the font is bold teal.</span></span> <span data-ttu-id="832d0-200">이 문서의 이미지는 기본 테마를 사용하여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-200">The images in this document were taken using the default theme.</span></span>

![이미지](intro/_static/labelaspfor2.png)

<span data-ttu-id="832d0-202">Visual Studio *CompleteWord* 바로 가기를 입력할 수 있으며(큰따옴표 안에서는 Ctrl + 스페이스가 [기본](/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio)), 이제 C# 클래스와 마찬가지로 C#에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-202">You can enter the Visual Studio *CompleteWord* shortcut (Ctrl +spacebar is the [default](/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio) inside the double quotes (""), and you are now in C#, just like you would be in a C# class.</span></span> <span data-ttu-id="832d0-203">IntelliSense는 페이지 모델에 모든 메서드 및 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-203">IntelliSense displays all the methods and properties on the page model.</span></span> <span data-ttu-id="832d0-204">속성 형식이 `ModelExpression`이므로 메서드 및 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-204">The methods and properties are available because the property type is `ModelExpression`.</span></span> <span data-ttu-id="832d0-205">아래 이미지에서는 `RegisterViewModel`을 사용할 수 있도록 `Register` 보기를 편집하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-205">In the image below, I'm editing the `Register` view, so the `RegisterViewModel` is available.</span></span>

![이미지](intro/_static/intellemail.png)

<span data-ttu-id="832d0-207">IntelliSense는 페이지에서 모델에 사용할 수 있는 속성과 메서드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-207">IntelliSense lists the properties and methods available to the model on the page.</span></span> <span data-ttu-id="832d0-208">다양한 IntelliSense 환경에서 CSS 클래스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-208">The rich IntelliSense environment helps you select the CSS class:</span></span>

![이미지](intro/_static/iclass.png)

![이미지](intro/_static/intel3.png)

## <a name="tag-helpers-compared-to-html-helpers"></a><span data-ttu-id="832d0-211">HTML 도우미와 비교한 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="832d0-211">Tag Helpers compared to HTML Helpers</span></span>

<span data-ttu-id="832d0-212">태그 도우미는 Razor 보기의 HTML 요소에 연결되고, [HTML 도우미](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers)는 HTML을 사용하여 Razor 보기에 배치된 메서드로 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-212">Tag Helpers attach to HTML elements in Razor views, while [HTML Helpers](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers) are invoked as methods interspersed with HTML in Razor views.</span></span> <span data-ttu-id="832d0-213">CSS 클래스 "caption"을 사용하여 HTML 레이블을 만드는 다음 Razor 태그를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="832d0-213">Consider the following Razor markup, which creates an HTML label with the CSS class "caption":</span></span>

```cshtml
@Html.Label("FirstName", "First Name:", new {@class="caption"})
```

<span data-ttu-id="832d0-214">`@` 기호는 Razor에 여기가 코드의 시작임을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-214">The at (`@`) symbol tells Razor this is the start of code.</span></span> <span data-ttu-id="832d0-215">다음 두 매개 변수("FirstName" 및 "First Name:")는 문자열이므로 [IntelliSense](/visualstudio/ide/using-intellisense)가 도움이 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-215">The next two parameters ("FirstName" and "First Name:") are strings, so [IntelliSense](/visualstudio/ide/using-intellisense) can't help.</span></span> <span data-ttu-id="832d0-216">마지막 인수:</span><span class="sxs-lookup"><span data-stu-id="832d0-216">The last argument:</span></span>

```cshtml
new {@class="caption"}
```

<span data-ttu-id="832d0-217">특성을 표시하는 데 사용되는 익명 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-217">Is an anonymous object used to represent attributes.</span></span> <span data-ttu-id="832d0-218"><strong>클래스</strong>는 C#에서 예약된 키워드이므로 `@` 기호를 사용하여 C#이 "@class="를 기호(속성 이름)로 해석하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-218">Because <strong>class</strong> is a reserved keyword in C#, you use the `@` symbol to force C# to interpret "@class=" as a symbol (property name).</span></span> <span data-ttu-id="832d0-219">프런트 엔드 디자이너(HTML/CSS/JavaScript 및 기타 클라이언트에 익숙하지만 C# 및 Razor에는 익숙하지 않은 사람)에게는 대부분의 줄이 이질적입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-219">To a front-end designer (someone familiar with HTML/CSS/JavaScript and other client technologies but not familiar with C# and Razor), most of the line is foreign.</span></span> <span data-ttu-id="832d0-220">IntelliSense의 도움 없이 전체 줄을 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-220">The entire line must be authored with no help from IntelliSense.</span></span>

<span data-ttu-id="832d0-221">`LabelTagHelper`를 사용하면 동일한 태그를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-221">Using the `LabelTagHelper`, the same markup can be written as:</span></span>

![이미지](intro/_static/label2.png)

<span data-ttu-id="832d0-223">태그 도우미 버전을 사용하면 Visual Studio 편집기에서 `<l`를 입력하는 즉시 IntelliSense는 일치하는 요소를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-223">With the Tag Helper version, as soon as you enter `<l` in the Visual Studio editor, IntelliSense displays matching elements:</span></span>

![이미지](intro/_static/label.png)

<span data-ttu-id="832d0-225">IntelliSense의 도움을 받아 전체 줄을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-225">IntelliSense helps you write the entire line.</span></span> <span data-ttu-id="832d0-226">또한 `LabelTagHelper`는 기본적으로 `asp-for` 특성 값("FirstName")의 콘텐츠를 "First Name"으로 설정합니다. 카멜식 대/소문자 속성을 공백이 있는 속성 이름으로 구성된 문장으로 변환하며 여기서는 새로운 대문자 문자가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-226">The `LabelTagHelper` also defaults to setting the content of the `asp-for` attribute value ("FirstName") to "First Name"; It converts camel-cased properties to a sentence composed of the property name with a space where each new upper-case letter occurs.</span></span> <span data-ttu-id="832d0-227">다음 태그에서:</span><span class="sxs-lookup"><span data-stu-id="832d0-227">In the following markup:</span></span>

![이미지](intro/_static/label2.png)

<span data-ttu-id="832d0-229">생성:</span><span class="sxs-lookup"><span data-stu-id="832d0-229">generates:</span></span>

```cshtml
<label class="caption" for="FirstName">First Name</label>
```

<span data-ttu-id="832d0-230">`<label>`에 콘텐츠를 추가하면 카멜식 대/소문자-문장식 대/소문자 콘텐츠가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-230">The camel-cased to sentence-cased content isn't used if you add content to the `<label>`.</span></span> <span data-ttu-id="832d0-231">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="832d0-231">For example:</span></span>

![이미지](intro/_static/1stName.png)

<span data-ttu-id="832d0-233">생성:</span><span class="sxs-lookup"><span data-stu-id="832d0-233">generates:</span></span>

```cshtml
<label class="caption" for="FirstName">Name First</label>
```

<span data-ttu-id="832d0-234">다음 코드 이미지는 Visual Studio 2015에 포함된 기존 ASP.NET 4.5.x MVC 템플릿으로 생성한 *Views/Account/Register.cshtml* Razor 보기의 양식 부분을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-234">The following code image shows the Form portion of the *Views/Account/Register.cshtml* Razor view generated from the legacy ASP.NET 4.5.x MVC template included with Visual Studio 2015.</span></span>

![이미지](intro/_static/regCS.png)

<span data-ttu-id="832d0-236">Visual Studio 편집기는 회색 배경에 C# 코드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-236">The Visual Studio editor displays C# code with a grey background.</span></span> <span data-ttu-id="832d0-237">예를 들어 `AntiForgeryToken` HTML 도우미의 경우:</span><span class="sxs-lookup"><span data-stu-id="832d0-237">For example, the `AntiForgeryToken` HTML Helper:</span></span>

```cshtml
@Html.AntiForgeryToken()
```

<span data-ttu-id="832d0-238">회색 배경과 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-238">is displayed with a grey background.</span></span> <span data-ttu-id="832d0-239">레지스터 보기의 태그는 대부분 C#입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-239">Most of the markup in the Register view is C#.</span></span> <span data-ttu-id="832d0-240">태그 도우미를 사용하는 동급의 방법과 비교해 보세요.</span><span class="sxs-lookup"><span data-stu-id="832d0-240">Compare that to the equivalent approach using Tag Helpers:</span></span>

![이미지](intro/_static/regTH.png)

<span data-ttu-id="832d0-242">태그는 HTML 도우미 방식보다 훨씬 깔끔하며 읽기, 편집 및 유지 관리가 훨씬 용이합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-242">The markup is much cleaner and easier to read, edit, and maintain than the HTML Helpers approach.</span></span> <span data-ttu-id="832d0-243">C# 코드는 서버에서 알아야 하는 최소 수준으로 축소됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-243">The C# code is reduced to the minimum that the server needs to know about.</span></span> <span data-ttu-id="832d0-244">Visual Studio 편집기는 태그 도우미의 대상 태그를 고유의 글꼴로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-244">The Visual Studio editor displays markup targeted by a Tag Helper in a distinctive font.</span></span>

<span data-ttu-id="832d0-245">*이메일* 그룹을 떠올려 보세요.</span><span class="sxs-lookup"><span data-stu-id="832d0-245">Consider the *Email* group:</span></span>

[!code-csharp[](intro/sample/Register.cshtml?range=12-18)]

<span data-ttu-id="832d0-246">각 "asp-" 특성은 "Email" 값을 갖지만 "Email"은 문자열이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-246">Each of the "asp-" attributes has a value of "Email", but "Email" isn't a string.</span></span> <span data-ttu-id="832d0-247">이 컨텍스트에서 "Email"은 `RegisterViewModel`에 대한 C# 모델 식 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-247">In this context, "Email" is the C# model expression property for the `RegisterViewModel`.</span></span>

<span data-ttu-id="832d0-248">Visual Studio 편집기를 사용하면 레지스터 양식의 태그 도우미 접근 방식에서 사용되는 **모든** 태그를 작성할 수 있지만, Visual Studio는 HTML 도우미 접근 방식에서 대부분의 코드에 도움을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-248">The Visual Studio editor helps you write **all** of the markup in the Tag Helper approach of the register form, while Visual Studio provides no help for most of the code in the HTML Helpers approach.</span></span> <span data-ttu-id="832d0-249">[태그 도우미에 대한 IntelliSense 지원](#intellisense-support-for-tag-helpers)에서는 Visual Studio 편집기에서 태그 도우미를 사용하는 것에 대해 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-249">[IntelliSense support for Tag Helpers](#intellisense-support-for-tag-helpers) goes into detail on working with Tag Helpers in the Visual Studio editor.</span></span>

## <a name="tag-helpers-compared-to-web-server-controls"></a><span data-ttu-id="832d0-250">웹 서버 컨트롤과 비교한 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="832d0-250">Tag Helpers compared to Web Server Controls</span></span>

* <span data-ttu-id="832d0-251">태그 도우미는 연결된 요소가 없고, 단순히 요소 및 콘텐츠 렌더링에 참여할 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-251">Tag Helpers don't own the element they're associated with; they simply participate in the rendering of the element and content.</span></span> <span data-ttu-id="832d0-252">페이지에서 ASP.NET [웹 서버 컨트롤](https://msdn.microsoft.com/library/7698y1f0.aspx)이 선언 및 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-252">ASP.NET [Web Server controls](https://msdn.microsoft.com/library/7698y1f0.aspx) are declared and invoked on a page.</span></span>

* <span data-ttu-id="832d0-253">[웹 서버 컨트롤](https://msdn.microsoft.com/library/zsyt68f1.aspx)에는 개발 및 디버깅을 어렵게 만들 수 있는 중요한 수명 주기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-253">[Web Server controls](https://msdn.microsoft.com/library/zsyt68f1.aspx) have a non-trivial lifecycle that can make developing and debugging difficult.</span></span>

* <span data-ttu-id="832d0-254">웹 서버 컨트롤을 사용하면 클라이언트 컨트롤을 사용하여 클라이언트 DOM(문서 개체 모델) 요소에 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-254">Web Server controls allow you to add functionality to the client Document Object Model (DOM) elements by using a client control.</span></span> <span data-ttu-id="832d0-255">태그 도우미에는 DOM이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-255">Tag Helpers have no DOM.</span></span>

* <span data-ttu-id="832d0-256">웹 서버 컨트롤은 자동 브라우저 검색 기능을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-256">Web Server controls include automatic browser detection.</span></span> <span data-ttu-id="832d0-257">태그 도우미는 브라우저를 모릅니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-257">Tag Helpers have no knowledge of the browser.</span></span>

* <span data-ttu-id="832d0-258">여러 태그 도우미가 같은 요소에서 작동할 수 있으며([태그 도우미 충돌 방지](xref:mvc/views/tag-helpers/authoring#avoid-tag-helper-conflicts) 참조) 일반적으로 웹 서버 컨트롤을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-258">Multiple Tag Helpers can act on the same element (see [Avoiding Tag Helper conflicts](xref:mvc/views/tag-helpers/authoring#avoid-tag-helper-conflicts) ) while you typically can't compose Web Server controls.</span></span>

* <span data-ttu-id="832d0-259">태그 도우미는 범위가 지정된 HTML 요소의 태그와 콘텐츠를 수정할 수 있지만, 페이지에 있는 다른 항목은 직접 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-259">Tag Helpers can modify the tag and content of HTML elements that they're scoped to, but don't directly modify anything else on a page.</span></span> <span data-ttu-id="832d0-260">웹 서버 컨트롤은 범위가 덜 구체적이고 페이지의 다른 부분에 영향을 주는 작업을 수행할 수 있으며, 이로 인해 의도하지 않은 부작용이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-260">Web Server controls have a less specific scope and can perform actions that affect other parts of your page; enabling unintended side effects.</span></span>

* <span data-ttu-id="832d0-261">웹 서버 컨트롤은 형식 변환기를 사용하여 문자열을 개체로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-261">Web Server controls use type converters to convert strings into objects.</span></span> <span data-ttu-id="832d0-262">태그 도우미를 사용하면 기본적으로 C#에서 작업하게 되므로 형식을 변환할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-262">With Tag Helpers, you work natively in C#, so you don't need to do type conversion.</span></span>

* <span data-ttu-id="832d0-263">웹 서버 컨트롤은 [System.ComponentModel](/dotnet/api/system.componentmodel)을 사용하여 구성 요소와 컨트롤의 런타임 및 디자인 타임 동작을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-263">Web Server controls use [System.ComponentModel](/dotnet/api/system.componentmodel) to implement the run-time and design-time behavior of components and controls.</span></span> <span data-ttu-id="832d0-264">`System.ComponentModel`에는 특성 및 형식 변환기를 구현하고, 데이터 소스에 바인딩하고, 구성 요소 사용을 허가하기 위한 기본 클래스 및 인터페이스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-264">`System.ComponentModel` includes the base classes and interfaces for implementing attributes and type converters, binding to data sources, and licensing components.</span></span> <span data-ttu-id="832d0-265">태그 도우미와는 달리, 일반적으로 `TagHelper`에서 파생되고 `TagHelper` 기본 클래스가 `Process` 및 `ProcessAsync` 메서드만 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-265">Contrast that to Tag Helpers, which typically derive from `TagHelper`, and the `TagHelper` base class exposes only two methods, `Process` and `ProcessAsync`.</span></span>

## <a name="customizing-the-tag-helper-element-font"></a><span data-ttu-id="832d0-266">태그 도우미 요소 글꼴 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="832d0-266">Customizing the Tag Helper element font</span></span>

<span data-ttu-id="832d0-267">**도구** > **옵션** > **환경** > **글꼴 및 색**에서 글꼴 및 색을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-267">You can customize the font and colorization from **Tools** > **Options** > **Environment** > **Fonts and Colors**:</span></span>

![이미지](intro/_static/fontoptions2.png)

## <a name="additional-resources"></a><span data-ttu-id="832d0-269">추가 자료</span><span class="sxs-lookup"><span data-stu-id="832d0-269">Additional resources</span></span>

* [<span data-ttu-id="832d0-270">태그 도우미 작성</span><span class="sxs-lookup"><span data-stu-id="832d0-270">Author Tag Helpers</span></span>](xref:mvc/views/tag-helpers/authoring)
* [<span data-ttu-id="832d0-271">양식 사용</span><span class="sxs-lookup"><span data-stu-id="832d0-271">Working with Forms </span></span>](xref:mvc/views/working-with-forms)
* <span data-ttu-id="832d0-272">[GitHub의 TagHelperSamples](https://github.com/dpaquette/TagHelperSamples)에는 [부트스트랩](http://getbootstrap.com/)을 사용하기 위한 태그 도우미 샘플이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="832d0-272">[TagHelperSamples on GitHub](https://github.com/dpaquette/TagHelperSamples) contains Tag Helper samples for working with [Bootstrap](http://getbootstrap.com/).</span></span>
