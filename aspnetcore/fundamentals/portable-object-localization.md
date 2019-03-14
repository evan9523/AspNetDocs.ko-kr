---
title: ASP.NET Core에서 이식 가능 개체 지역화 구성
author: sebastienros
description: 이 문서는 이식 가능 개체 파일을 소개하고 ASP.NET Core 애플리케이션에서 Orchard Core 프레임워크와 사용하는 단계를 간략하게 설명합니다.
ms.author: scaddie
ms.date: 09/26/2017
uid: fundamentals/portable-object-localization
ms.openlocfilehash: c9f892f5a886d7167b4705595ed2277279495201
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57053220"
---
# <a name="configure-portable-object-localization-in-aspnet-core"></a><span data-ttu-id="8058f-103">ASP.NET Core에서 이식 가능 개체 지역화 구성</span><span class="sxs-lookup"><span data-stu-id="8058f-103">Configure portable object localization in ASP.NET Core</span></span>

<span data-ttu-id="8058f-104">작성자: [Sébastien Ros](https://github.com/sebastienros) 및 [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="8058f-104">By [Sébastien Ros](https://github.com/sebastienros) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="8058f-105">이 문서는 ASP.NET Core 애플리케이션에서 PO(이식 가능 개체) 파일을 [Orchard Core](https://github.com/OrchardCMS/OrchardCore) 프레임워크와 함께 사용하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-105">This article walks through the steps for using Portable Object (PO) files in an ASP.NET Core application with the [Orchard Core](https://github.com/OrchardCMS/OrchardCore) framework.</span></span>

<span data-ttu-id="8058f-106">**참고:** Orchard Core는 Microsoft 제품이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-106">**Note:** Orchard Core isn't a Microsoft product.</span></span> <span data-ttu-id="8058f-107">따라서 Microsoft는 이 기능에 대한 지원을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-107">Consequently, Microsoft provides no support for this feature.</span></span>

<span data-ttu-id="8058f-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/localization/sample/POLocalization) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="8058f-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/localization/sample/POLocalization) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="what-is-a-po-file"></a><span data-ttu-id="8058f-109">PO 파일이란?</span><span class="sxs-lookup"><span data-stu-id="8058f-109">What is a PO file?</span></span>

<span data-ttu-id="8058f-110">PO 파일은 지정된 언어에 대한 번역된 문자열을 포함하는 텍스트 파일로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-110">PO files are distributed as text files containing the translated strings for a given language.</span></span> <span data-ttu-id="8058f-111">*.resx* 파일 대신 PO 파일을 사용하는 몇 가지 이점은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-111">Some advantages of using PO files instead *.resx* files include:</span></span>
- <span data-ttu-id="8058f-112">PO 파일은 복수화를 지원합니다. *.resx* 파일은 복수화를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-112">PO files support pluralization; *.resx* files don't support pluralization.</span></span>
- <span data-ttu-id="8058f-113">PO 파일은 *.resx* 파일처럼 컴파일되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-113">PO files aren't compiled like *.resx* files.</span></span> <span data-ttu-id="8058f-114">이와 같이 특수화된 도구 및 빌드 단계는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-114">As such, specialized tooling and build steps aren't required.</span></span>
- <span data-ttu-id="8058f-115">PO 파일은 공동 온라인 편집 도구와 함께 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-115">PO files work well with collaborative online editing tools.</span></span>

### <a name="example"></a><span data-ttu-id="8058f-116">예제</span><span class="sxs-lookup"><span data-stu-id="8058f-116">Example</span></span>

<span data-ttu-id="8058f-117">복수 형태로 하나를 포함하여 프랑스어로 두 개의 문자열에 대한 번역을 포함하는 샘플 PO 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-117">Here is a sample PO file containing the translation for two strings in French, including one with its plural form:</span></span>

<span data-ttu-id="8058f-118">*fr.po*</span><span class="sxs-lookup"><span data-stu-id="8058f-118">*fr.po*</span></span>

```text
#: Services/EmailService.cs:29
msgid "Enter a comma separated list of email addresses."
msgstr "Entrez une liste d'emails séparés par une virgule."

#: Views/Email.cshtml:112
msgid "The email address is \"{0}\"."
msgid_plural "The email addresses are \"{0}\"."
msgstr[0] "L'adresse email est \"{0}\"."
msgstr[1] "Les adresses email sont \"{0}\""
```

<span data-ttu-id="8058f-119">이 예제에서는 다음 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-119">This example uses the following syntax:</span></span>

- <span data-ttu-id="8058f-120">`#:`: 변환할 문자열의 컨텍스트를 나타내는 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-120">`#:`: A comment indicating the context of the string to be translated.</span></span> <span data-ttu-id="8058f-121">동일한 문자열은 사용되는 위치에 따라 다르게 변환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-121">The same string might be translated differently depending on where it's being used.</span></span>
- <span data-ttu-id="8058f-122">`msgid`: 번역 되지 않은 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-122">`msgid`: The untranslated string.</span></span>
- <span data-ttu-id="8058f-123">`msgstr`: 번역 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-123">`msgstr`: The translated string.</span></span>

<span data-ttu-id="8058f-124">복수화 지원의 경우 더 많은 항목을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-124">In the case of pluralization support, more entries can be defined.</span></span>

- <span data-ttu-id="8058f-125">`msgid_plural`: 번역 되지 않은 복수형 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-125">`msgid_plural`: The untranslated plural string.</span></span>
- <span data-ttu-id="8058f-126">`msgstr[0]`: 사례 0에 대 한 번역 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-126">`msgstr[0]`: The translated string for the case 0.</span></span>
- <span data-ttu-id="8058f-127">`msgstr[N]`: 사례 N에 대 한 번역 된 문자열</span><span class="sxs-lookup"><span data-stu-id="8058f-127">`msgstr[N]`: The translated string for the case N.</span></span>

<span data-ttu-id="8058f-128">PO 파일 사양은 [여기](https://www.gnu.org/savannah-checkouts/gnu/gettext/manual/html_node/PO-Files.html)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-128">The PO file specification can be found [here](https://www.gnu.org/savannah-checkouts/gnu/gettext/manual/html_node/PO-Files.html).</span></span>

## <a name="configuring-po-file-support-in-aspnet-core"></a><span data-ttu-id="8058f-129">ASP.NET Core에서 PO 파일 구성 지원</span><span class="sxs-lookup"><span data-stu-id="8058f-129">Configuring PO file support in ASP.NET Core</span></span>

<span data-ttu-id="8058f-130">이 예제는 Visual Studio 2017 프로젝트 템플릿에서 생성된 ASP.NET Core MVC 애플리케이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-130">This example is based on an ASP.NET Core MVC application generated from a Visual Studio 2017 project template.</span></span>

### <a name="referencing-the-package"></a><span data-ttu-id="8058f-131">패키지 참조</span><span class="sxs-lookup"><span data-stu-id="8058f-131">Referencing the package</span></span>

<span data-ttu-id="8058f-132">`OrchardCore.Localization.Core` NuGet 패키지에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-132">Add a reference to the `OrchardCore.Localization.Core` NuGet package.</span></span> <span data-ttu-id="8058f-133">패키지 소스 https://www.myget.org/F/orchardcore-preview/api/v3/index.json의 [MyGet](https://www.myget.org/)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-133">It's available on [MyGet](https://www.myget.org/) at the following package source: https://www.myget.org/F/orchardcore-preview/api/v3/index.json</span></span>

<span data-ttu-id="8058f-134">이제 *.csproj* 파일은 다음과 비슷한 줄을 포함합니다(버전 번호가 달라질 수 있음).</span><span class="sxs-lookup"><span data-stu-id="8058f-134">The *.csproj* file now contains a line similar to the following (version number may vary):</span></span>

[!code-xml[](localization/sample/POLocalization/POLocalization.csproj?range=9)]

### <a name="registering-the-service"></a><span data-ttu-id="8058f-135">서비스 등록</span><span class="sxs-lookup"><span data-stu-id="8058f-135">Registering the service</span></span>

<span data-ttu-id="8058f-136">*Startup.cs*의 `ConfigureServices` 메서드에 필요한 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-136">Add the required services to the `ConfigureServices` method of *Startup.cs*:</span></span>

[!code-csharp[](localization/sample/POLocalization/Startup.cs?name=snippet_ConfigureServices&highlight=4-21)]

<span data-ttu-id="8058f-137">*Startup.cs*의 `Configure` 메서드에 필요한 미들웨어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-137">Add the required middleware to the `Configure` method of *Startup.cs*:</span></span>

[!code-csharp[](localization/sample/POLocalization/Startup.cs?name=snippet_Configure&highlight=15)]

<span data-ttu-id="8058f-138">선택한 Razor 뷰에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-138">Add the following code to your Razor view of choice.</span></span> <span data-ttu-id="8058f-139">이 예제에서는 *About.cshtml*이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-139">*About.cshtml* is used in this example.</span></span>

[!code-cshtml[](localization/sample/POLocalization/Views/Home/About.cshtml)]

<span data-ttu-id="8058f-140">`IViewLocalizer` 인스턴스가 삽입되고 "Hello world!" 텍스트를 번역하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-140">An `IViewLocalizer` instance is injected and used to translate the text "Hello world!".</span></span>

### <a name="creating-a-po-file"></a><span data-ttu-id="8058f-141">PO 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="8058f-141">Creating a PO file</span></span>

<span data-ttu-id="8058f-142">애플리케이션 루트 폴더에 *<culture code>.po*라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-142">Create a file named *<culture code>.po* in your application root folder.</span></span> <span data-ttu-id="8058f-143">이 예제에서는 프랑스어가 사용되므로 파일 이름은 *fr.po*입니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-143">In this example, the file name is *fr.po* because the French language is used:</span></span>

[!code-text[](localization/sample/POLocalization/fr.po)]

<span data-ttu-id="8058f-144">이 파일은 번역할 문자열 및 프랑스어로 번역된 문자열 모두를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-144">This file stores both the string to translate and the French-translated string.</span></span> <span data-ttu-id="8058f-145">필요한 경우 번역은 해당 부모 문화권으로 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-145">Translations revert to their parent culture, if necessary.</span></span> <span data-ttu-id="8058f-146">이 예제에서 요청된 문화권이 `fr-FR` 또는 `fr-CA`인 경우 *fr.po* 파일이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-146">In this example, the *fr.po* file is used if the requested culture is `fr-FR` or `fr-CA`.</span></span>

### <a name="testing-the-application"></a><span data-ttu-id="8058f-147">애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="8058f-147">Testing the application</span></span>

<span data-ttu-id="8058f-148">애플리케이션을 실행하고 `/Home/About` URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-148">Run your application, and navigate to the URL `/Home/About`.</span></span> <span data-ttu-id="8058f-149">텍스트 **Hello world!**</span><span class="sxs-lookup"><span data-stu-id="8058f-149">The text **Hello world!**</span></span> <span data-ttu-id="8058f-150">가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-150">is displayed.</span></span>

<span data-ttu-id="8058f-151">`/Home/About?culture=fr-FR` URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-151">Navigate to the URL `/Home/About?culture=fr-FR`.</span></span> <span data-ttu-id="8058f-152">텍스트 **Bonjour le monde!**</span><span class="sxs-lookup"><span data-stu-id="8058f-152">The text **Bonjour le monde!**</span></span> <span data-ttu-id="8058f-153">가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-153">is displayed.</span></span>

## <a name="pluralization"></a><span data-ttu-id="8058f-154">복수화</span><span class="sxs-lookup"><span data-stu-id="8058f-154">Pluralization</span></span>

<span data-ttu-id="8058f-155">PO 파일은 동일한 문자열이 카디널리티에 따라 다르게 번역되어야 하는 경우 유용한 복수화 양식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-155">PO files support pluralization forms, which is useful when the same string needs to be translated differently based on a cardinality.</span></span> <span data-ttu-id="8058f-156">이 작업은 각 언어가 카디널리티에 따라 사용할 문자열을 선택하도록 사용자 지정 규칙을 정의한다는 점에서 복잡하게 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-156">This task is made complicated by the fact that each language defines custom rules to select which string to use based on the cardinality.</span></span>

<span data-ttu-id="8058f-157">Orchard 지역화 패키지는 이러한 다른 복수 양식을 자동으로 호출하는 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-157">The Orchard Localization package provides an API to invoke these different plural forms automatically.</span></span>

### <a name="creating-pluralization-po-files"></a><span data-ttu-id="8058f-158">복수화 PO 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="8058f-158">Creating pluralization PO files</span></span>

<span data-ttu-id="8058f-159">앞에서 언급한 *fr.po* 파일에 다음 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-159">Add the following content to the previously mentioned *fr.po* file:</span></span>

```text
msgid "There is one item."
msgid_plural "There are {0} items."
msgstr[0] "Il y a un élément."
msgstr[1] "Il y a {0} éléments."
```

<span data-ttu-id="8058f-160">이 예제의 각 항목이 나타내는 것의 설명은 [PO 파일이란?](#what-is-a-po-file)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8058f-160">See [What is a PO file?](#what-is-a-po-file) for an explanation of what each entry in this example represents.</span></span>

### <a name="adding-a-language-using-different-pluralization-forms"></a><span data-ttu-id="8058f-161">다른 복수화 양식을 사용하여 언어 추가</span><span class="sxs-lookup"><span data-stu-id="8058f-161">Adding a language using different pluralization forms</span></span>

<span data-ttu-id="8058f-162">이전 예제에서는 영어와 프랑스어 문자열이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-162">English and French strings were used in the previous example.</span></span> <span data-ttu-id="8058f-163">영어와 프랑스어에는 두 개의 복수화 양식만이 있으며 하나의 카디널리티가 첫 번째 복수 양식에 매핑되는 동일한 양식 규칙을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-163">English and French have only two pluralization forms and share the same form rules, which is that a cardinality of one is mapped to the first plural form.</span></span> <span data-ttu-id="8058f-164">다른 카디널리티는 두 번째 복수 양식에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-164">Any other cardinality is mapped to the second plural form.</span></span>

<span data-ttu-id="8058f-165">모든 언어는 동일한 규칙을 공유하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-165">Not all languages share the same rules.</span></span> <span data-ttu-id="8058f-166">세 가지 복수 양식을 가진 체코어로 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-166">This is illustrated with the Czech language, which has three plural forms.</span></span>

<span data-ttu-id="8058f-167">다음과 같이 `cs.po` 파일을 만들고 복수화에서 세 가지 다른 번역을 요구하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-167">Create the `cs.po` file as follows, and note how the pluralization needs three different translations:</span></span>

[!code-text[](localization/sample/POLocalization/cs.po)]

<span data-ttu-id="8058f-168">체코어 지역화를 허용하려면 `ConfigureServices` 메서드의 지원되는 문화권 목록에 `"cs"`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-168">To accept Czech localizations, add `"cs"` to the list of supported cultures in the `ConfigureServices` method:</span></span>

```csharp
var supportedCultures = new List<CultureInfo>
{
    new CultureInfo("en-US"),
    new CultureInfo("en"),
    new CultureInfo("fr-FR"),
    new CultureInfo("fr"),
    new CultureInfo("cs")
};
```

<span data-ttu-id="8058f-169">*Views/Home/About.cshtml* 파일을 편집하여 여러 카디널리티에 대한 지역화된 복수 문자열을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-169">Edit the *Views/Home/About.cshtml* file to render localized, plural strings for several cardinalities:</span></span>

```cshtml
<p>@Localizer.Plural(1, "There is one item.", "There are {0} items.")</p>
<p>@Localizer.Plural(2, "There is one item.", "There are {0} items.")</p>
<p>@Localizer.Plural(5, "There is one item.", "There are {0} items.")</p>
```

<span data-ttu-id="8058f-170">**참고:** 실제 시나리오에서는 변수는 나타내는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-170">**Note:** In a real world scenario, a variable would be used to represent the count.</span></span> <span data-ttu-id="8058f-171">여기에서 세 가지 다른 값으로 동일한 코드를 반복하여 매우 특정한 사례를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-171">Here, we repeat the same code with three different values to expose a very specific case.</span></span>

<span data-ttu-id="8058f-172">문화권이 전환되면 다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-172">Upon switching cultures, you see the following:</span></span>

<span data-ttu-id="8058f-173">`/Home/About`의 경우:</span><span class="sxs-lookup"><span data-stu-id="8058f-173">For `/Home/About`:</span></span>

```html
There is one item.
There are 2 items.
There are 5 items.
```

<span data-ttu-id="8058f-174">`/Home/About?culture=fr`의 경우:</span><span class="sxs-lookup"><span data-stu-id="8058f-174">For `/Home/About?culture=fr`:</span></span>

```html
Il y a un élément.
Il y a 2 éléments.
Il y a 5 éléments.
```

<span data-ttu-id="8058f-175">`/Home/About?culture=cs`의 경우:</span><span class="sxs-lookup"><span data-stu-id="8058f-175">For `/Home/About?culture=cs`:</span></span>

```html
Existuje jedna položka.
Existují 2 položky.
Existuje 5 položek.
```

<span data-ttu-id="8058f-176">체코어 문화권의 경우 세 가지 번역은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-176">Note that for the Czech culture, the three translations are different.</span></span> <span data-ttu-id="8058f-177">프랑스어 및 영어 문화권은 마지막 두 개의 번역된 문자열에 대해 동일한 구조를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-177">The French and English cultures share the same construction for the two last translated strings.</span></span>

## <a name="advanced-tasks"></a><span data-ttu-id="8058f-178">고급 작업</span><span class="sxs-lookup"><span data-stu-id="8058f-178">Advanced tasks</span></span>

### <a name="contextualizing-strings"></a><span data-ttu-id="8058f-179">문자열 맥락화</span><span class="sxs-lookup"><span data-stu-id="8058f-179">Contextualizing strings</span></span>

<span data-ttu-id="8058f-180">애플리케이션은 종종 여러 위치에서 번역되는 문자열을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-180">Applications often contain the strings to be translated in several places.</span></span> <span data-ttu-id="8058f-181">동일한 문자열은 앱 내의 특정 위치에서 다른 번역을 가질 수 있습니다(Razor 뷰 또는 클래스 파일).</span><span class="sxs-lookup"><span data-stu-id="8058f-181">The same string may have a different translation in certain locations within an app (Razor views or class files).</span></span> <span data-ttu-id="8058f-182">PO 파일은 표시되는 문자열을 분류하는 데 사용될 수 있는 파일 컨텍스트의 개념을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-182">A PO file supports the notion of a file context, which can be used to categorize the string being represented.</span></span> <span data-ttu-id="8058f-183">파일 컨텍스트를 사용하여 문자열은 파일 컨텍스트(또는 파일 컨텍스트 부족)에 따라 다르게 번역될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-183">Using a file context, a string can be translated differently, depending on the file context (or lack of a file context).</span></span>

<span data-ttu-id="8058f-184">PO 지역화 서비스는 전체 클래스 또는 문자열을 변역할 때 사용되는 뷰의 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-184">The PO localization services use the name of the full class or the view that's used when translating a string.</span></span> <span data-ttu-id="8058f-185">`msgctxt` 항목의 값을 설정하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-185">This is accomplished by setting the value on the `msgctxt` entry.</span></span>

<span data-ttu-id="8058f-186">이전 *fr.po* 예제에 대한 최소 추가를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-186">Consider a minor addition to the previous *fr.po* example.</span></span> <span data-ttu-id="8058f-187">*Views/Home/About.cshtml*에 있는 Razor 뷰는 예약된 `msgctxt` 항목의 값을 설정하여 파일 컨텍스트로 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-187">A Razor view located at *Views/Home/About.cshtml* can be defined as the file context by setting the reserved `msgctxt` entry's value:</span></span>

```text
msgctxt "Views.Home.About"
msgid "Hello world!"
msgstr "Bonjour le monde!"
```

<span data-ttu-id="8058f-188">`msgctxt`를 이와 같이 설정하면 텍스트 번역은 `/Home/About?culture=fr-FR`로 이동할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-188">With the `msgctxt` set as such, text translation occurs when navigating to `/Home/About?culture=fr-FR`.</span></span> <span data-ttu-id="8058f-189">번역은 `/Home/Contact?culture=fr-FR`로 이동할 때 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-189">The translation won't occur when navigating to `/Home/Contact?culture=fr-FR`.</span></span>

<span data-ttu-id="8058f-190">특정 항목이 지정된 파일 컨텍스트와 일치하지 않는 경우 Orchard Core의 대체 메커니즘은 컨텍스트 없이 적절한 PO 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-190">When no specific entry is matched with a given file context, Orchard Core's fallback mechanism looks for an appropriate PO file without a context.</span></span> <span data-ttu-id="8058f-191">*Views/Home/Contact.cshtml*에 대해 정의된 특정 파일 컨텍스트가 없다고 가정하는 경우 `/Home/Contact?culture=fr-FR`로 이동하면 다음과 같은 PO 파일이 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-191">Assuming there's no specific file context defined for *Views/Home/Contact.cshtml*, navigating to `/Home/Contact?culture=fr-FR` loads a PO file such as:</span></span>

[!code-text[](localization/sample/POLocalization/fr.po)]

### <a name="changing-the-location-of-po-files"></a><span data-ttu-id="8058f-192">PO 파일의 위치 변경</span><span class="sxs-lookup"><span data-stu-id="8058f-192">Changing the location of PO files</span></span>

<span data-ttu-id="8058f-193">PO 파일의 기본 위치는 `ConfigureServices`에서 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-193">The default location of PO files can be changed in `ConfigureServices`:</span></span>

```csharp
services.AddPortableObjectLocalization(options => options.ResourcesPath = "Localization");
```

<span data-ttu-id="8058f-194">이 예제에서 PO 파일은 *지역화* 폴더에서 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-194">In this example, the PO files are loaded from the *Localization* folder.</span></span>

### <a name="implementing-a-custom-logic-for-finding-localization-files"></a><span data-ttu-id="8058f-195">지역화 파일을 찾기 위한 사용자 지정 논리 구현</span><span class="sxs-lookup"><span data-stu-id="8058f-195">Implementing a custom logic for finding localization files</span></span>

<span data-ttu-id="8058f-196">PO 파일을 배치하는 데 더 복잡한 논리가 필요한 경우 서비스로 `OrchardCore.Localization.PortableObject.ILocalizationFileLocationProvider` 인터페이스를 구현하고 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-196">When more complex logic is needed to locate PO files, the `OrchardCore.Localization.PortableObject.ILocalizationFileLocationProvider` interface can be implemented and registered as a service.</span></span> <span data-ttu-id="8058f-197">PO 파일을 다양한 위치에 저장할 수 있는 경우 또는 폴더의 계층 구조 내에서 파일을 찾아야 하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-197">This is useful when PO files can be stored in varying locations or when the files have to be found within a hierarchy of folders.</span></span>

### <a name="using-a-different-default-pluralized-language"></a><span data-ttu-id="8058f-198">복수화된 다른 기본 언어 사용</span><span class="sxs-lookup"><span data-stu-id="8058f-198">Using a different default pluralized language</span></span>

<span data-ttu-id="8058f-199">패키지는 두 개의 복수 양식과 관련된 `Plural` 확장 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-199">The package includes a `Plural` extension method that's specific to two plural forms.</span></span> <span data-ttu-id="8058f-200">더 많은 복수 양식을 요구하는 언어의 경우 확장 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-200">For languages requiring more plural forms, create an extension method.</span></span> <span data-ttu-id="8058f-201">확장 메서드를 사용하면 기본 언어 &mdash;에 대해 지역화 파일을 제공할 필요가 없습니다. 원본 문자열을 코드에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-201">With an extension method, you won't need to provide any localization file for the default language &mdash; the original strings are already available directly in the code.</span></span>

<span data-ttu-id="8058f-202">번역의 문자열 배열을 허용하는 보다 일반적인 `Plural(int count, string[] pluralForms, params object[] arguments)` 오버로드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8058f-202">You can use the more generic `Plural(int count, string[] pluralForms, params object[] arguments)` overload which accepts a string array of translations.</span></span>
