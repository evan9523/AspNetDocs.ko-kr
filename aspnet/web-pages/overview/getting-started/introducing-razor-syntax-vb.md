---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Razor 구문 (Visual Basic)를 사용 하 여 ASP.NET 웹 프로그래밍 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 부록 개요를 제공 ASP.NET 웹 페이지를 사용 하 여 프로그래밍의 Visual basic에서는 Razor 구문을 사용 합니다.
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: e6b63afb9492e810e19999c7c7ffe074ad510bda
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59406771"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="390c3-103">Razor 구문 (Visual Basic)를 사용 하 여 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="390c3-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="390c3-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="390c3-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="390c3-105">이 문서에서는 프로그래밍 개요 ASP.NET 웹 페이지 Razor 구문 및 Visual Basic을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="390c3-106">ASP.NET은 웹 서버에서 동적 웹 페이지를 실행 하기 위한 Microsoft의 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="390c3-107">**학습할**:</span><span class="sxs-lookup"><span data-stu-id="390c3-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="390c3-108">프로그래밍 팁 Razor 구문을 사용 하 여 ASP.NET 웹 페이지 프로그래밍 시작 하기 위한 상위 8입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="390c3-109">기본 프로그래밍 개념을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="390c3-110">어떤 ASP.NET 서버 코드 및 Razor 구문에 대 한 all입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="390c3-111">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="390c3-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="390c3-112">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="390c3-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="390c3-113">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="390c3-114">Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하 여 대부분의 예제 C#을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="390c3-115">하지만 Razor 구문을 Visual Basic을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="390c3-116">사용 하 여 웹 페이지를 만들면 Visual Basic의 ASP.NET 웹 페이지를 프로그래밍 하는 *.vbhtml* 파일 이름 확장명, Visual Basic 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="390c3-117">이 문서에서는 Visual Basic 언어 및 ASP.NET 웹 페이지를 만드는 구문을 사용 하 여 작업의 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="390c3-118">Microsoft WebMatrix에 대 한 기본 웹 사이트 템플릿 (**빵집**를 **사진 갤러리**, 및 **시작 사이트**등) C# 및 Visual Basic 버전에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="390c3-119">Visual Basic 템플릿을 NuGet 패키지로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="390c3-120">라는 폴더에 사이트의 루트 폴더에 설치 된 웹 사이트 템플릿을 *Microsoft 템플릿*합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>


## <a name="the-top-8-programming-tips"></a><span data-ttu-id="390c3-121">상위 8 프로그래밍 팁</span><span class="sxs-lookup"><span data-stu-id="390c3-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="390c3-122">이 섹션에서는 반드시 알아야 할 Razor 구문을 사용 하 여 ASP.NET 서버 코드 작성을 시작 하는 몇 가지 팁을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="390c3-123">1. 코드를 사용 하 여 페이지를 추가 하 여 @ 문자</span><span class="sxs-lookup"><span data-stu-id="390c3-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="390c3-124">`@` 문자 인라인 식, 단일 문 블록 및 다중 문 블록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="390c3-125">브라우저에 표시 된 결과:</span><span class="sxs-lookup"><span data-stu-id="390c3-125">The result displayed in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **<span data-ttu-id="390c3-127">HTML 인코딩</span><span class="sxs-lookup"><span data-stu-id="390c3-127">HTML Encoding</span></span>**
> 
> <span data-ttu-id="390c3-128">사용 하 여 페이지의 콘텐츠를 표시 하는 `@` 문자를 앞의 예에서 같이 ASP.NET을 HTML로 인코딩하고 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="390c3-129">이 예약 된 HTML 문자를 대체 (같은 `<` 하 고 `>` 및 `&`) 문자가 HTML 태그 또는 엔터티로 해석 되지 않고 웹 페이지에 표시할 문자를 사용 하도록 설정 하는 코드를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="390c3-130">HTML 인코딩하지 않고 서버 코드의 출력을 올바르게 표시 되지 않 및 페이지 보안 위험에 노출 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="390c3-131">목표는 태그로 태그를 렌더링 하는 HTML 태그를 출력 하는 경우 (예를 들어 `<p></p>` 단락 또는 `<em></em>` 텍스트를 강조 하기 위해), 섹션을 참조 하세요 [결합 텍스트, 태그 및 코드 블록의 코드](#BM_CombiningTextMarkupAndCode) 이 문서의 뒷부분에 나오는.</span><span class="sxs-lookup"><span data-stu-id="390c3-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="390c3-132">알아볼 수 있습니다에 HTML 인코딩에 대 한 [ASP.NET Web Pages 사이트에서 HTML 양식 작업](https://go.microsoft.com/fwlink/?LinkId=202892)합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>


### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="390c3-133">2. 코드를 사용 하 여 코드 블록 안에 포함 하는 중... 종료 코드</span><span class="sxs-lookup"><span data-stu-id="390c3-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="390c3-134">코드 블록을 하나 이상의 코드 문을 포함 및 키워드와 함께 묶입니다 `Code` 고 `End Code`입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="390c3-135">열기를 배치할 `Code` 키워드 바로 뒤를 `@` 문자 &#8212; 간의 공백 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="390c3-136">브라우저에 표시 된 결과:</span><span class="sxs-lookup"><span data-stu-id="390c3-136">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="390c3-138">3. 줄 바꿈 사용 하 여 각 코드 문 블록 내 종료</span><span class="sxs-lookup"><span data-stu-id="390c3-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="390c3-139">Visual Basic 코드 블록을 각 문은 줄 바꿈을 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="390c3-140">(이 문서의 뒷부분 표시 필요한 경우 긴 코드 문을 여러 줄으로 줄 바꿈 하는 방법입니다.)</span><span class="sxs-lookup"><span data-stu-id="390c3-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="390c3-141">4. 변수를 사용 하 여 값을 저장 하려면</span><span class="sxs-lookup"><span data-stu-id="390c3-141">4. You use variables to store values</span></span>

<span data-ttu-id="390c3-142">값을 저장할 수 있습니다는 *변수*, 문자열, 숫자 및 날짜 등을 포함 합니다. 사용 하 여 새 변수를 만든를 `Dim` 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="390c3-143">사용 하 여 페이지에서 직접 변수 값을 삽입할 수는 있지만 `@`합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="390c3-144">브라우저에 표시 된 결과:</span><span class="sxs-lookup"><span data-stu-id="390c3-144">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="390c3-146">5. 리터럴 문자열 값 큰따옴표로 묶어야</span><span class="sxs-lookup"><span data-stu-id="390c3-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="390c3-147">A *문자열* 텍스트로 처리 되는 문자 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="390c3-148">문자열을 지정 하려면 묶습니다 큰따옴표:</span><span class="sxs-lookup"><span data-stu-id="390c3-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="390c3-149">문자열 값 안에 큰따옴표를 포함 하려면 두 개의 큰따옴표 문자를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="390c3-150">페이지 출력에 1 번 나타나야 큰따옴표 문자를 하려는 경우 입력으로 `""` 내의 따옴표 붙은 문자열을 두 번 표시 하려는 경우 입력으로 `""""` 따옴표 붙은 문자열 내에서.</span><span class="sxs-lookup"><span data-stu-id="390c3-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="390c3-151">브라우저에 표시 된 결과:</span><span class="sxs-lookup"><span data-stu-id="390c3-151">The result displayed in a browser:</span></span>

![Razor Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="390c3-153">6. Visual Basic 코드 대/소문자 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="390c3-154">Visual Basic 언어는 대/소문자 구분 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="390c3-155">프로그래밍 키워드 (같은 `Dim`, `If`, 및 `True`) 및 변수 이름 (같은 `myString`, 또는 `subTotal`) 어떤 경우 든 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="390c3-156">변수에 값을 할당 하는 코드의 다음 줄 `lastname` 소문자를 사용 하 여 이름을 지정 하 고 다음 대문자로 된 이름을 사용 하 여 변수 값을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="390c3-157">브라우저에 표시 된 결과:</span><span class="sxs-lookup"><span data-stu-id="390c3-157">The result displayed in a browser:</span></span>

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="390c3-159">7. 개체를 사용 하 여 코딩의 대부분의 작업이</span><span class="sxs-lookup"><span data-stu-id="390c3-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="390c3-160">개체로 사용 하 여 프로그래밍할 수 있는 것을 나타내는 &#8212; 페이지, 텍스트 상자, 파일, 이미지, 웹 요청, 전자 메일 메시지, 고객 레코드 (데이터베이스 행) 등입니다. 개체 특징을 설명 하는 속성이 있습니다 &#8212; 텍스트 상자 개체의를 `Text` 속성인 요청 개체에는 `Url` 속성에는 전자 메일 메시지에는 `From` 속성을 고객 개체에는 `FirstName` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="390c3-161">개체 수도 있는 메서드를 &quot;동사&quot; 을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="390c3-162">파일 개체의 예로 `Save` 메서드를 이미지 개체의 `Rotate` 메서드 및 전자 메일 개체의 `Send` 메서드.</span><span class="sxs-lookup"><span data-stu-id="390c3-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="390c3-163">자주 사용 하는 `Request` 양식의 값 같은 정보를 제공 하는 개체를 요청, 페이지, 사용자 id 등의 URL을 수행 하는 브라우저 종류 (텍스트 상자, 등) 페이지에서 필드입니다. 속성에 액세스 하는 방법을 보여주는이 예제는 `Request` 개체 및 호출 하는 방법을 합니다 `MapPath` 메서드의 `Request` 서버의 페이지의 절대 경로 제공 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="390c3-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="390c3-164">브라우저에 표시 된 결과:</span><span class="sxs-lookup"><span data-stu-id="390c3-164">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="390c3-166">8. 의사 결정 하는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="390c3-167">동적 웹 페이지의 핵심 기능은 조건에 따라 수행할 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="390c3-168">이 작업을 수행 하는 가장 일반적인 방법은 된 합니다 `If` 문 (및 선택적 `Else` 문).</span><span class="sxs-lookup"><span data-stu-id="390c3-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="390c3-169">문이 `If IsPost` 작성 하는 약식 방법 `If IsPost = True`합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="390c3-170">와 함께 `If` 문 다양 한 조건에서 반복 코드 블록을 테스트 하는 방법 및 등과이 문서의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="390c3-171">브라우저에 표시 된 결과 (클릭 한 후 **제출**):</span><span class="sxs-lookup"><span data-stu-id="390c3-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **<span data-ttu-id="390c3-173">HTTP GET 및 POST 메서드는 IsPost 속성</span><span class="sxs-lookup"><span data-stu-id="390c3-173">HTTP GET and POST Methods and the IsPost Property</span></span>**
> 
> <span data-ttu-id="390c3-174">웹 페이지 (HTTP)에 사용 되는 프로토콜은 매우 제한 된 몇 가지 지원 (&quot;동사&quot;) 서버에 요청을 확인 하는 데 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="390c3-175">두 가지 자주 사용 되는 가져오기에 사용 되는 페이지를 읽으려는 및 페이지를 제출 하는 데 사용 되는 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="390c3-176">일반적으로 사용자가 페이지를 요청할 처음 페이지가 요청 될 GET을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="390c3-177">사용자 양식을 채웁니다을 클릭 하는 경우 **제출**, 브라우저는 서버에는 POST 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="390c3-178">웹 프로그래밍에서 유용 여부는 페이지 요청 POST 또는 GET으로 페이지를 처리 하는 방법을 알 수 있도록 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="390c3-179">ASP.NET 웹 페이지에서 사용할 수는 `IsPost` 속성 GET 또는 POST 요청 인지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="390c3-180">요청을 POST 이면는 `IsPost` 속성은 true를 반환 하 고 폼의 입력란의 값 등 읽기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="390c3-181">표시 되는 많은 예제 값에 따라 다르게 페이지를 처리 하는 방법을 보여 줍니다. `IsPost`합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>


## <a name="a-simple-code-example"></a><span data-ttu-id="390c3-182">간단한 코드 예제</span><span class="sxs-lookup"><span data-stu-id="390c3-182">A Simple Code Example</span></span>

<span data-ttu-id="390c3-183">이 절차에서는 기본적인 프로그래밍 기술을 설명 하는 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="390c3-184">예제에서는 입력 하 고 두 숫자를 추가 하 고 결과 표시 하는 사용자가 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="390c3-185">편집기에서 새 파일을 만들고 이름을 *AddNumbers.vbhtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="390c3-186">페이지에 이미 아무 것도 대체 페이지에 다음 코드와 태그를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="390c3-187">알아두어야 할 몇 가지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="390c3-188">합니다 `@` 문자 페이지에서 첫 번째 코드 블록을 시작 하 고 뒤에 나오는 `totalMessage` 아래쪽에 있는 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="390c3-189">페이지의 맨 위에 있는 블록으로 묶여 `Code...End Code`합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="390c3-190">변수 `total`, `num1`를 `num2`, 및 `totalMessage` 여러 숫자 및 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="390c3-191">에 할당 된 리터럴 문자열 값을 `totalMessage` 큰따옴표로 변수가 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="390c3-192">Visual Basic 코드 때 대/소문자를 구분 하지 않으므로 `totalMessage` 페이지 하단에 있는 변수를 사용 하는, 해당 이름을 페이지의 맨 위에 있는 변수 선언의 표기와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="390c3-193">대/소문자는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="390c3-194">식을 `num1.AsInt()`  +  `num2.AsInt()` 개체 및 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="390c3-195">`AsInt` 메서드 각 변수를 추가할 수 있는 전체 숫자 (정수)는 사용자가 입력 한 문자열을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="390c3-196">`<form>` 태그를 포함 한 `method="post"` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="390c3-197">사용자가 지정 하는 **추가**, 페이지 HTTP POST 메서드를 사용 하 여 서버에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="390c3-198">페이지가 제출 되는 경우, 코드 `If IsPost` true 나 조건부 코드를 실행, 숫자를 더한 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="390c3-199">페이지를 저장 하 고 브라우저에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="390c3-200">(페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.) 두 정수를 입력 한 다음 클릭 합니다 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="390c3-202">Visual Basic 언어 및 구문</span><span class="sxs-lookup"><span data-stu-id="390c3-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="390c3-203">이전 기본 예제 ASP.NET 웹 페이지를 만드는 방법 및 서버 코드는 HTML 태그를 추가 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="390c3-204">여기 Visual Basic을 사용 하 여 Razor 구문을 사용 하 여 ASP.NET 서버 코드를 작성 하는 기본적인 알아봅니다 &#8212; , 프로그래밍 언어 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="390c3-205">프로그래밍 경험이 있는 경우 (C를 사용한 경우에 특히 C++, C#, Visual Basic 또는 JavaScript)를 읽는 여기의 대부분에 게 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="390c3-206">기능을 살펴보고 WebMatrix 코드가 태그에 추가 하는 방법을 익히는 필요할 것 *.vbhtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a>  <span data-ttu-id="390c3-207">텍스트, 태그 및 코드 블록의 코드를 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="390c3-208">서버 코드 블록에서에서는 하려는 경우가 많습니다 텍스트와 태그 페이지를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="390c3-209">서버 코드 블록을 텍스트 코드 없는 하는 대신 렌더링할지 그대로 있으면 ASP.NET 코드에서 해당 텍스트를 구분할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="390c3-210">다음과 같은 여러 가지 방법으로 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-210">There are several ways to do this.</span></span>

- <span data-ttu-id="390c3-211">와 같은 HTML 블록 요소에서 텍스트를 묶으십시오 `<p></p>` 또는 `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="390c3-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="390c3-212">HTML 요소는 텍스트, HTML 요소 추가 및 서버 코드 식에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="390c3-213">ASP.NET에서 여는 HTML 태그를 표시 하는 경우 (예를 들어 `<p>`), 모든 요소 렌더링 및 해당 콘텐츠를 브라우저 (및 서버 코드 식 확인) 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="390c3-214">사용 된 `@:` 연산자 또는 `<text>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="390c3-215">합니다 `@:` 일반 텍스트 또는 일치 하지 않는 HTML 태그를 포함 하는 콘텐츠의 단일 줄을 출력 합니다 `<text>` 요소 출력에 여러 줄을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="390c3-216">이러한 옵션은 출력의 일부로 HTML 요소를 렌더링 하지 않을 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="390c3-217">다음 예제에서는 앞의 예제를 반복 하지만 단일 쌍을 사용 하 여 `<text>` 태그를 렌더링할 텍스트를 묶으십시오.</span><span class="sxs-lookup"><span data-stu-id="390c3-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="390c3-218">다음 예제에서는 `<text>` 및 `</text>` 태그는 모두 일부 포함 되지 않은 텍스트와 일치 하지 않는 HTML 태그 세 줄을 묶습니다 (`<br />`), 서버 코드와 일치 하는 HTML 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="390c3-219">마찬가지로 수도 앞에 개별적으로 각 줄은 `@:` 연산자; 둘 다 방식으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="390c3-220">이 섹션에 표시 된 대로 텍스트를 출력할 때 &#8212; HTML 요소를 사용 하는 `@:` 연산자와 `<text>` 요소 &#8212; ASP.NET 하지 HTML 인코딩 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="390c3-221">(ASP.NET 서버 코드 식 및 서버 코드 블록 뒤에 나오는의 출력을 인코딩하는 앞에서 설명한 대로 `@`를 제외 하 고이 섹션에서 설명 하는 특수 한 현상.)</span><span class="sxs-lookup"><span data-stu-id="390c3-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="390c3-222">Whitespace</span><span class="sxs-lookup"><span data-stu-id="390c3-222">Whitespace</span></span>

<span data-ttu-id="390c3-223">문에서 (및 문자열 리터럴 외부에서) 공백이 문이 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="390c3-224">긴 문을 여러 줄으로 분리</span><span class="sxs-lookup"><span data-stu-id="390c3-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="390c3-225">밑줄 문자를 사용 하 여 여러 줄 긴 코드 문의 중단할 수 있습니다 `_` (Visual Basic에서 호출 되는 *연속 문자*) 코드의 각 줄 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="390c3-226">다음 줄으로 문 중단 하려면 줄의 끝에 공백을 차례로 연속 문자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="390c3-227">다음 줄에서 문을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-227">Continue the statement on the next line.</span></span> <span data-ttu-id="390c3-228">문을 가독성을 개선 하기 위해 알아야 하는 만큼의 줄으로 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="390c3-229">다음 문은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="390c3-230">그러나 문자열 리터럴로 중간 줄을 둘러쌀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="390c3-231">다음 예제에서는 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="390c3-232">위의 코드와 같이 여러 줄으로 줄 바꿈되는 긴 문자열을 결합 하려면 사용 해야 합니다 *concatenation 연산자* (`&`),이 문서의 뒷부분에서 볼 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="390c3-233">코드 주석</span><span class="sxs-lookup"><span data-stu-id="390c3-233">Code comments</span></span>

<span data-ttu-id="390c3-234">주석 자신 또는 다른 사용자에 대 한 정보를 그대로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="390c3-235">Razor 구문 주석은 붙습니다 `@*` 하 고 끝나야 `*@`합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="390c3-236">Razor 구문 주석은 코드 블록 내에서 사용 하거나 작은따옴표는 일반적인 Visual Basic 주석 문자를 사용할 수 있습니다 (`'`) 각 줄에 접두사로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="390c3-237">변수</span><span class="sxs-lookup"><span data-stu-id="390c3-237">Variables</span></span>

<span data-ttu-id="390c3-238">변수는 데이터를 저장 하는 데 사용 하는 명명 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="390c3-239">변수를 아무 것도 이름을 지정할 수 있습니다 하지만 이름은 영문자로 시작 해야 하 고 공백 또는 예약 된 문자를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="390c3-240">Visual Basic의 경우 앞에서 본 것 처럼 변수 이름에 소문자 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="390c3-241">변수 및 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="390c3-241">Variables and data types</span></span>

<span data-ttu-id="390c3-242">변수는 어떤 종류의 데이터를 변수에 저장 됨을 나타내는 특정 데이터 형식에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="390c3-243">문자열 값을 저장 하는 문자열 변수를 할 수 있습니다 (같은 &quot;Hello world&quot;), 다양 한 형식 (예: 2012/4/12 또는 2009 년 3 월의에서 날짜 값을 저장 하는 정수 값 (예: 3 또는 79)를 저장 하는 정수 변수 및 날짜 ).</span><span class="sxs-lookup"><span data-stu-id="390c3-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="390c3-244">및 다른 여러 데이터 형식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="390c3-245">그러나 변수 형식을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="390c3-246">대부분의 경우에서 ASP.NET 데이터 변수를 어떻게 사용 되 고 있는지에 따라 형식을 알아낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="390c3-247">(형식을 지정 해야 하는 경우에 따라,이 참 이어야 하는 예제 표시 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="390c3-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="390c3-248">변수를 선언 된 형식을 지정 하지 않고, 사용 하 여 `Dim` 및 변수 이름 (예를 들어 `Dim myVar`).</span><span class="sxs-lookup"><span data-stu-id="390c3-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="390c3-249">를 형식으로 변수를 선언 하려면 `Dim` 변수 이름 뒤에 더하기 `As` 유형 이름 다음에 (예를 들어 `Dim myVar As String`).</span><span class="sxs-lookup"><span data-stu-id="390c3-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="390c3-250">다음 예에서는 변수를 사용 하 여 웹 페이지에는 몇 가지 인라인 식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="390c3-251">브라우저에 표시 된 결과:</span><span class="sxs-lookup"><span data-stu-id="390c3-251">The result displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="390c3-253">변환 및 데이터 형식 테스트</span><span class="sxs-lookup"><span data-stu-id="390c3-253">Converting and testing data types</span></span>

<span data-ttu-id="390c3-254">일반적으로 ASP.NET 데이터 형식을 자동으로 확인할 수 있습니다, 있지만 경우에 따라 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="390c3-255">따라서 명시적 변환을 수행 하 여 ASP.NET을 도와줄 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="390c3-256">형식을 변환 하는 것이 없는, 하는 경우에 때때로 것이 좋습니다 테스트 하려는 어떤 유형의 데이터를 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="390c3-257">가장 일반적인 경우는 정수 또는 날짜와 같은 다른 형식으로 문자열을 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="390c3-258">다음 예제에서는 문자열을 숫자로 변환 해야 여기서는 일반적인 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="390c3-259">일반적으로 사용자 입력을 문자열로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="390c3-260">숫자를 입력 하 라는 메시지가 표시 한 경우에을 때 사용자 입력을 제출 하 고 코드에서 읽을 때 숫자를 입력 한 경우에 데이터를 문자열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="390c3-261">따라서 문자열을 숫자로 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="390c3-262">예에서를 변환 하지 않고 값에 산술 연산을 수행 하려는 경우 다음 오류가 발생을 ASP.NET 두 문자열을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="390c3-263">정수 값으로 변환 하려면 호출을 `AsInt` 메서드.</span><span class="sxs-lookup"><span data-stu-id="390c3-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="390c3-264">변환이 성공한 경우에 다음 숫자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="390c3-265">다음 표에서 변수에 대 한 몇 가지 일반적인 변환 및 테스트 메서드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-265">The following table lists some common conversion and test methods for variables.</span></span>


:::row:::
    :::column:::
        <strong>Method</strong>
    :::column-end:::
    :::column:::
        <strong>Description</strong>
    :::column-end:::
    :::column:::
        <strong>Example</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        Converts a string that represents a whole number (like &quot;593&quot;) to an integer.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number. (In ASP.NET, a decimal number is more precise than a floating-point number.)
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        Converts a string that represents a date and time value to the ASP.NET `DateTime` type.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        Converts any other data type to a string.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::


## <a name="operators"></a><span data-ttu-id="390c3-266">연산자</span><span class="sxs-lookup"><span data-stu-id="390c3-266">Operators</span></span>

<span data-ttu-id="390c3-267">연산자는 키워드 또는 식에서 수행할 수 있는 명령의 종류를 ASP.NET에 지시 하는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-267">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="390c3-268">Visual Basic에서는 다양 한 연산자를 지원 하지만 ASP.NET 웹 페이지 개발을 시작 하려면 몇 가지를 인식 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-268">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="390c3-269">다음 표에서 가장 일반적인 연산자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-269">The following table summarizes the most common operators.</span></span>


:::row:::
    :::column:::
        <strong>Operator</strong>
    :::column-end:::
    :::column:::
        <strong>Description</strong>
    :::column-end:::
    :::column:::
        <strong>Examples</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        Math operators used in numerical expressions.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        Assignment and equality. Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        Inequality. Returns `True` if the values are not equal.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        Less than, greater than, less than or equal, and greater than or equal.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        Concatenation, which is used to join strings.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        The increment and decrement operators, which add and subtract 1 (respectively) from a variable.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        Dot. Used to distinguish objects and their properties and methods.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        Parentheses. Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        Not. Reverses a true value to false and vice versa. Typically used as a shorthand way to test for `False` (that is, for not `True`).
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        Logical AND and OR, which are used to link conditions together.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="390c3-270">파일 및 코드의 폴더 경로 사용 하 여 작업</span><span class="sxs-lookup"><span data-stu-id="390c3-270">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="390c3-271">종종 코드에서 파일 및 폴더 경로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-271">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="390c3-272">개발 컴퓨터에 나타나는 웹 사이트에 대 한 실제 폴더 구조의 예 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-272">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="390c3-273">Url 및 경로 대 한 몇 가지 필수 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-273">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="390c3-274">도메인 이름을 사용 하 여 시작 URL (`http://www.example.com`) 또는 서버 이름 (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="390c3-274">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="390c3-275">URL은 호스트 컴퓨터의 실제 경로에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-275">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="390c3-276">예를 들어 `http://myserver` 폴더에 해당할 수 있습니다 *C:\websites\mywebsite* 서버의 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-276">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="390c3-277">가상 경로 전체 경로 지정 하지 않고도 코드에서 경로 나타내는 축약형입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-277">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="390c3-278">도메인 또는 서버 이름 다음에 나오는 URL 부분을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-278">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="390c3-279">가상 경로 사용 하는 경우에 경로 업데이트 하지 않고도 다른 도메인 또는 서버에 코드를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-279">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="390c3-280">차이점을 이해 하는 데 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-280">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="390c3-281">전체 URL</span><span class="sxs-lookup"><span data-stu-id="390c3-281">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="390c3-282">서버 이름</span><span class="sxs-lookup"><span data-stu-id="390c3-282">Server name</span></span> | *<span data-ttu-id="390c3-283">mycompanyserver</span><span class="sxs-lookup"><span data-stu-id="390c3-283">mycompanyserver</span></span>* |
| <span data-ttu-id="390c3-284">가상 경로</span><span class="sxs-lookup"><span data-stu-id="390c3-284">Virtual path</span></span> | *<span data-ttu-id="390c3-285">/humanresources/CompanyPolicy.htm</span><span class="sxs-lookup"><span data-stu-id="390c3-285">/humanresources/CompanyPolicy.htm</span></span>* |
| <span data-ttu-id="390c3-286">실제 경로</span><span class="sxs-lookup"><span data-stu-id="390c3-286">Physical path</span></span> | *<span data-ttu-id="390c3-287">C:\mywebsites\humanresources\CompanyPolicy.htm</span><span class="sxs-lookup"><span data-stu-id="390c3-287">C:\mywebsites\humanresources\CompanyPolicy.htm</span></span>* |

<span data-ttu-id="390c3-288">가상 루트가 / 드라이브는 c:의 루트와 마찬가지로 \입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-288">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="390c3-289">(가상 폴더 경로 항상 슬래시를 사용 합니다.) 폴더의 가상 경로 실제 폴더 이름이 같은 필요가 없습니다. 별칭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-289">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="390c3-290">(프로덕션 서버에서 가상 경로 거의 일치 하는 실제 경로 정확 하 게 합니다.)</span><span class="sxs-lookup"><span data-stu-id="390c3-290">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="390c3-291">코드에서 파일 및 폴더를 사용 하 여 작업할 때의 실제 경로 및 경우에 따라 사용 하는 개체에 따라 가상 경로 참조 해야 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-291">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="390c3-292">ASP.NET이 도구를 제공 하면 이러한 코드에서 파일 및 폴더 경로 사용 하 여 작업에 대 한: 합니다 `Server.MapPath` 메서드 및 `~` 연산자 및 `Href` 메서드.</span><span class="sxs-lookup"><span data-stu-id="390c3-292">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="390c3-293">실제 가상 경로로 변환: Server.MapPath 메서드</span><span class="sxs-lookup"><span data-stu-id="390c3-293">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="390c3-294">합니다 `Server.MapPath` 메서드는 가상 경로 변환 (같은 */default.cshtml*) 절대 실제 경로에 (같은 *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="390c3-294">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="390c3-295">전체 실제 경로 필요할 때 언제 든이이 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-295">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="390c3-296">일반적인 예로 읽거나 텍스트 파일 또는 웹 서버의 이미지 파일을 작성 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-296">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="390c3-297">일반적으로 알 수 없는 호스팅 사이트 서버의 사이트의 절대 실제 경로 알고이 메서드는 경로 변환할 수 있도록-가상 경로-를 서버에 해당 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-297">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="390c3-298">파일 또는 폴더 메서드에 가상 경로 전달 하 고 실제 경로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-298">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="390c3-299">가상 루트 참조:는 ~ 연산자 및 Href 메서드</span><span class="sxs-lookup"><span data-stu-id="390c3-299">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="390c3-300">에 *.cshtml* 또는 *.vbhtml* 파일을 사용 하 여 가상 루트 경로 참조할 수 있습니다는 `~` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-300">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="390c3-301">사이트에서 페이지를 이동할 수 있으며 다른 페이지에 포함 된 모든 링크는 손상 되지 때문에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-301">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="390c3-302">그 어느 때 다른 위치로 웹 사이트를 이동 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-302">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="390c3-303">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-303">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="390c3-304">웹 사이트가 `http://myserver/myapp`, 이러한 경로 페이지가 실행 될 때 ASP.NET에서 어떻게 처리 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-304">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- `myImagesFolder`<span data-ttu-id="390c3-305">:</span><span class="sxs-lookup"><span data-stu-id="390c3-305">:</span></span> `http://myserver/myapp/images`
- `myStyleSheet` <span data-ttu-id="390c3-306">:</span><span class="sxs-lookup"><span data-stu-id="390c3-306">:</span></span> `http://myserver/myapp/styles/Stylesheet.css`

<span data-ttu-id="390c3-307">(실제로 이러한 경로 변수 값으로 표시 되지 않습니다 하지만 어떤는 처럼 ASP.NET 경로 처리 합니다.)</span><span class="sxs-lookup"><span data-stu-id="390c3-307">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="390c3-308">사용할 수는 `~` 연산자 위와 같이 서버 코드와 같이 태그에서:</span><span class="sxs-lookup"><span data-stu-id="390c3-308">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="390c3-309">태그를 사용 하 여는 `~` 연산자를 이미지 파일, 다른 웹 페이지 및 CSS 파일 같은 리소스에 대 한 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-309">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="390c3-310">ASP.NET 페이지 (코드 및 태그)를 통해 찾아 해결 하는 모든 페이지를 실행 하는 경우는 `~` 적절 한 경로에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-310">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="390c3-311">조건부 논리 및 루프</span><span class="sxs-lookup"><span data-stu-id="390c3-311">Conditional Logic and Loops</span></span>

<span data-ttu-id="390c3-312">ASP.NET 서버 코드 하면 조건 및 루프를 실행 하는 문이 지정한 횟수 만큼 즉, 코드를 반복 하는 쓰기 코드에 따라 작업을 수행).</span><span class="sxs-lookup"><span data-stu-id="390c3-312">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="390c3-313">테스트 조건</span><span class="sxs-lookup"><span data-stu-id="390c3-313">Testing conditions</span></span>

<span data-ttu-id="390c3-314">사용할 간단한 조건을 테스트 하는 `If...Then` 문이 반환 하는 `True` 또는 `False` 지정할 테스트 기준:</span><span class="sxs-lookup"><span data-stu-id="390c3-314">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="390c3-315">`If` 키워드는 블록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-315">The `If` keyword starts a block.</span></span> <span data-ttu-id="390c3-316">실제 테스트 (조건) 뒤의 `If` 키워드 및 true 또는 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-316">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="390c3-317">합니다 `If` 문이 끝나는 `Then`합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-317">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="390c3-318">테스트가 참일 경우 실행할 문을 묶여 `If` 고 `End If`입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-318">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="390c3-319">`If` 문을 포함할 수는 `Else` 조건이 false 인 경우 실행할 문을 지정 하는 블록:</span><span class="sxs-lookup"><span data-stu-id="390c3-319">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="390c3-320">경우는 `If` 문이 코드 블록을 시작, 법선을 사용 하 여 필요가 `Code...End Code` 블록을 포함 하도록 문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-320">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="390c3-321">추가 하기만 하면 `@` 블록에 있으며 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-321">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="390c3-322">이 방법은 사용 하 여 `If` 프로그래밍 키워드 뒤에 코드 블록을 포함 하는 다른 Visual Basic 뿐만 아니라 `For`를 `For Each`, `Do While`등입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-322">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="390c3-323">하나를 사용 하 여 여러 조건을 추가할 수 있습니다 `ElseIf` 블록:</span><span class="sxs-lookup"><span data-stu-id="390c3-323">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="390c3-324">이 예제에서는 첫 번째 조건이 합니다 `If` 블록이 true가 아니면는 `ElseIf` 조건이 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-324">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="390c3-325">조건이 충족 될 경우의 문에서 `ElseIf` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-325">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="390c3-326">어떤 조건 충족 되 면의 문에서 `Else` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-326">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="390c3-327">개수에 관계 없이 추가할 수 있습니다 `ElseIf` 블록을 닫고 사용 하 여는 `Else` 으로 차단 합니다 &quot;등등&quot; 조건.</span><span class="sxs-lookup"><span data-stu-id="390c3-327">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="390c3-328">많은 수의 조건 테스트 하려면 사용을 `Select Case` 블록:</span><span class="sxs-lookup"><span data-stu-id="390c3-328">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="390c3-329">테스트할 값입니다 (예제에서는 요일 변수)의 괄호 안에 있는 경우</span><span class="sxs-lookup"><span data-stu-id="390c3-329">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="390c3-330">각 개별 테스트를 사용 하는 `Case` 값을 나열 하는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-330">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="390c3-331">하는 경우의 값을 `Case` 문이 일치 하는 코드를 테스트 값을 `Case` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-331">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="390c3-332">브라우저에 표시 된 마지막 두 조건부 블록의 결과:</span><span class="sxs-lookup"><span data-stu-id="390c3-332">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="390c3-334">코드를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-334">Looping code</span></span>

<span data-ttu-id="390c3-335">자주 반복적으로 동일한 문을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-335">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="390c3-336">반복 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-336">You do this by looping.</span></span> <span data-ttu-id="390c3-337">예를 들어, 종종 문을 실행 하면 동일한 각 항목에 대 한 데이터의 컬렉션에서입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-337">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="390c3-338">사용할 수 있습니다 정확 하 게 하는 횟수를 반복 하려면를 알고 있는 경우는 `For` 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-338">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="390c3-339">이러한 종류의 루프까지 셈 카운트다운에 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-339">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="390c3-340">로 시작 하는 루프를 `For` 키워드 뒤에 세 개의 요소:</span><span class="sxs-lookup"><span data-stu-id="390c3-340">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="390c3-341">바로 뒤를 `For` 카운터 변수 선언 문을 (사용할 필요가 없습니다 `Dim`)에서 같이 범위, 표시 및 `i = 10 to 20`합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-341">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="390c3-342">즉, 변수의 `i` 10부터 계산을 시작 하 고 20 (포함)에 도달할 때까지 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-342">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="390c3-343">간의 합니다 `For` 및 `Next` 문 블록의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-343">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="390c3-344">하나 이상의 코드 문을 실행 하는 각 루프를 사용 하 여 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-344">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="390c3-345">`Next i` 문 루프를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-345">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="390c3-346">카운터를 증가 하 고 루프의 다음 반복을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-346">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="390c3-347">사이 코드 줄을 `For` 및 `Next` 줄 루프의 각 반복에 대해 실행 되는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-347">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="390c3-348">태그를 만들고 새 단락 (`<p>` 요소) 각 시간 및의 값을 표시할 출력에 줄을 추가 i (카운터).</span><span class="sxs-lookup"><span data-stu-id="390c3-348">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="390c3-349">이 페이지를 실행 하면 항목 수를 나타내는 각 줄의 텍스트를 사용 하 여 출력을 표시 하는 11 줄을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-349">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="390c3-351">컬렉션 또는 배열을 사용 하 여 작업할 경우 자주 사용 하는 `For Each` 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-351">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="390c3-352">컬렉션은 유사한 개체의 그룹 및 `For Each` 루프는 컬렉션의 각 항목에서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-352">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="390c3-353">이 유형의 루프는 컬렉션에 대 한 편리한 있으므로 달리는 `For` 루프 필요가 카운터를 증가 시키거나 제한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-353">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="390c3-354">대신는 `For Each` 루프 코드 컬렉션을 통해 완료 될 때까지 간단히 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-354">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="390c3-355">항목을 반환 하는이 예제는 `Request.ServerVariables` 컬렉션 (웹 서버에 대 한 정보 포함).</span><span class="sxs-lookup"><span data-stu-id="390c3-355">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="390c3-356">사용 하 여는 `For Each` 새 각 항목의 이름을 표시 하려면 루프 `<li>` HTML 글머리 기호 목록의 요소에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-356">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="390c3-357">`For Each` 키워드 뒤에 컬렉션의 단일 항목을 나타내는 변수 (예에서 `myItem`) 뒤를 `In` 키워드를 반복 하려는 컬렉션에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-357">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="390c3-358">본문에는 `For Each` 루프 앞에서 선언한 변수를 사용 하 여 현재 항목에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-358">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="390c3-360">보다 일반적인 루프를 만들려면 사용 합니다 `Do While` 문:</span><span class="sxs-lookup"><span data-stu-id="390c3-360">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="390c3-361">이 루프 시작의 `Do While` 반복 블록 뒤에 키워드, 조건을 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-361">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="390c3-362">루프는 일반적으로 증가 (추가) 또는 감소 (에서 빼기) 변수 또는 계산에 사용 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-362">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="390c3-363">예에서를 `+=` 연산자 1 값을 추가 변수는 루프가 실행 될 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-363">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="390c3-364">(카운트다운 되는 루프에서 변수를 감소 시키기 위해 감소 연산자를 사용 하는 `-=`.)</span><span class="sxs-lookup"><span data-stu-id="390c3-364">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="390c3-365">개체 및 컬렉션</span><span class="sxs-lookup"><span data-stu-id="390c3-365">Objects and Collections</span></span>

<span data-ttu-id="390c3-366">ASP.NET 웹 사이트의 거의 모든 항목은 웹 페이지 자체를 포함 하 여 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-366">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="390c3-367">이 섹션에서는 자주 사용 하 여 코드에서 몇 가지 중요 한 개체를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-367">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="390c3-368">Page 개체</span><span class="sxs-lookup"><span data-stu-id="390c3-368">Page objects</span></span>

<span data-ttu-id="390c3-369">ASP.NET에서 가장 기본적인 개체는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-369">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="390c3-370">조건에 맞는 개체 없이 직접 page 개체의 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-370">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="390c3-371">다음 코드는 페이지의 파일 경로 가져오고 사용 하는 `Request` 페이지의 개체:</span><span class="sxs-lookup"><span data-stu-id="390c3-371">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="390c3-372">속성을 사용할 수는 `Page` 와 같은 많은 정보를 가져올 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-372">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- `Request`<span data-ttu-id="390c3-373">.</span><span class="sxs-lookup"><span data-stu-id="390c3-373">.</span></span> <span data-ttu-id="390c3-374">이미 살펴보았듯이, 요청, 페이지, 사용자 id 등의 URL을 수행 하는 브라우저 종류를 포함 하 여 현재 요청에 대 한 정보 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-374">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- `Response`<span data-ttu-id="390c3-375">.</span><span class="sxs-lookup"><span data-stu-id="390c3-375">.</span></span> <span data-ttu-id="390c3-376">서버 코드 실행이 완료 된 경우 브라우저에 보낼 응답 (페이지)에 대 한 정보 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-376">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="390c3-377">예를 들어이 속성을 사용 하 여 응답에 정보를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-377">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="390c3-378">컬렉션 개체 (배열 및 사전을)</span><span class="sxs-lookup"><span data-stu-id="390c3-378">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="390c3-379">컬렉션은 개체의 컬렉션과 같은 동일한 유형의 그룹 `Customer` 데이터베이스에서 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-379">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="390c3-380">ASP.NET와 같은 많은 기본 제공 컬렉션을 포함 합니다 `Request.Files` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-380">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="390c3-381">컬렉션의 데이터를 자주 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-381">You'll often work with data in collections.</span></span> <span data-ttu-id="390c3-382">두 가지 일반적인 컬렉션 형식은 합니다 *배열* 하며 *사전*합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-382">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="390c3-383">배열 유사 항목 컬렉션을 저장 하 고 싶지만를 각 항목을 보유 하는 별도 변수를 만들지 않으려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-383">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="390c3-384">배열에서 특정 데이터 형식을 선언와 같은 `String`, `Integer`, 또는 `DateTime`합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-384">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="390c3-385">변수 배열을 포함할 수 있습니다, 선언에서 변수 이름에 괄호를 추가 하 (같은 `Dim myVar() As String`).</span><span class="sxs-lookup"><span data-stu-id="390c3-385">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="390c3-386">항목의 위치 (인덱스)를 사용 하는 배열 또는 사용 하 여 액세스할 수 있습니다는 `For Each` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-386">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="390c3-387">배열 인덱스는 0부터 시작 &#8212; 즉, 첫 번째 항목은에서 위치 0, 두 번째 항목은 위치 1입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-387">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="390c3-388">시작 하 여 배열에 있는 항목의 수를 확인할 수 있습니다 해당 `Length` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-388">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="390c3-389">배열에서 특정 항목의 위치를 가져올 수 (즉, 배열을 검색)를 사용 하 여를 `Array.IndexOf` 메서드.</span><span class="sxs-lookup"><span data-stu-id="390c3-389">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="390c3-390">수행할 수도 있습니다 역방향 등 배열의 내용을 (합니다 `Array.Reverse` 메서드) 또는 콘텐츠를 정렬 (합니다 `Array.Sort` 메서드).</span><span class="sxs-lookup"><span data-stu-id="390c3-390">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="390c3-391">브라우저에 표시 하는 문자열 배열 코드의 출력:</span><span class="sxs-lookup"><span data-stu-id="390c3-391">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="390c3-393">사전이 같습니다 키/값 쌍의 컬렉션을 설정 하거나 해당 값을 검색 키 (또는 이름)을 제공 하는 위치</span><span class="sxs-lookup"><span data-stu-id="390c3-393">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="390c3-394">사전을 만들려면를 사용 합니다 `New` 키워드는 만드는 새를 `Dictionary` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-394">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="390c3-395">사용 하 여 변수를 사전에 할당할 수 있습니다는 `Dim` 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-395">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="390c3-396">괄호를 사용 하 여 사전에 있는 항목의 데이터 형식을 ( `( )` ).</span><span class="sxs-lookup"><span data-stu-id="390c3-396">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="390c3-397">선언의 끝 실제로 새 사전을 만듭니다 하는 방법 이기 때문에 다른 괄호 쌍을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-397">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="390c3-398">사전에 항목을 추가 하려면 호출할 수 있습니다 합니다 `Add` 사전 변수의 메서드 (`myScores` 이 경우), 키 및 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-398">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="390c3-399">또는 키를 나타내고 다음 예제와 같이 단순한 할당을 수행 하려면 괄호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-399">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="390c3-400">사전에서 값을 가져오려면 괄호로 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-400">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="390c3-401">매개 변수를 사용 하 여 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-401">Calling Methods with Parameters</span></span>

<span data-ttu-id="390c3-402">이 문서의 앞부분에서 살펴본 것 처럼 개체를 프로그래밍 하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-402">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="390c3-403">예를 들어, 한 `Database` 개체에 있을 `Database.Connect` 메서드.</span><span class="sxs-lookup"><span data-stu-id="390c3-403">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="390c3-404">여러 방법에는 하나 이상의 매개 변수 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-404">Many methods also have one or more parameters.</span></span> <span data-ttu-id="390c3-405">A *매개 변수* 메서드에 전달 하는 값은 해당 작업을 완료 하는 메서드를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-405">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="390c3-406">예를 들어,에 대 한 선언을 확인 된 `Request.MapPath` 세 개의 매개 변수를 사용 하는 메서드:</span><span class="sxs-lookup"><span data-stu-id="390c3-406">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="390c3-407">이 메서드는 지정된 된 가상 경로에 해당 하는 서버의 실제 경로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-407">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="390c3-408">메서드에 대 한 세 가지 매개 변수는 `virtualPath`하십시오 `baseVirtualDir`, 및 `allowCrossAppMapping`합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-408">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="390c3-409">(알 수 있습니다 선언 매개 변수를 수락 하 게 하는 데이터의 데이터 형식으로 나열 됩니다.) 이 메서드를 호출 하는 경우 모든 세 매개 변수에 대 한 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-409">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="390c3-410">메서드에 매개 변수를 전달 하기 위한 두 가지 옵션이 Razor 구문을 사용 하 여 Visual Basic을 사용 하는 경우: *위치 매개 변수* 하거나 *명명 된 매개 변수*합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-410">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="390c3-411">위치 매개 변수를 사용 하 여 메서드를 호출 하는 엄격한 순서를 메서드 선언에 지정 된 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-411">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="390c3-412">(일반적으로 알 수이 순서 메서드에 대 한 설명서를 참조 하 여.) 순서를 따라야 하며 매개 변수를 건너뛸 수 없습니다 &#8212; 하는 경우 필요한 전달 하면 빈 문자열 (`""`)에 대 한 값이 없는 위치 매개 변수에 대해 null입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-412">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="390c3-413">다음 예제에서는 라는 폴더가 있다고 가정 *스크립트* 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-413">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="390c3-414">호출 된 `Request.MapPath` 메서드와 전달 올바른 순서로 세 가지 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-414">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="390c3-415">다음의 결과 매핑된 경로가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-415">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="390c3-416">메서드에 대 한 여러 매개 변수가 있는 경우 유지할 수 있습니다 코드 깔끔하고 더 읽을 수 있는 명명 된 매개 변수를 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="390c3-416">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="390c3-417">명명 된 매개 변수를 사용 하 여 메서드를 호출 하려면 뒤에 매개 변수 이름을 지정 `:=` 고 다음 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-417">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="390c3-418">명명 된 매개 변수의 장점은는 원하는 순서에 관계 없이 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-418">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="390c3-419">(단점은 메서드 호출으로 compact 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="390c3-419">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="390c3-420">다음 예제에서는 위와 같은 메서드를 호출 하지만 명명 된 값을 제공 하는 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-420">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="390c3-421">알 수 있듯이 다른 순서로 매개 변수 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-421">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="390c3-422">그러나 앞의 예제 및이 예제를 실행 하는 경우 동일한 값을 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-422">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="390c3-423">오류 처리</span><span class="sxs-lookup"><span data-stu-id="390c3-423">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="390c3-424">Try / Catch 문</span><span class="sxs-lookup"><span data-stu-id="390c3-424">Try-Catch statements</span></span>

<span data-ttu-id="390c3-425">종종 컨트롤 외부 이유로 실패할 수 있는 코드에 문의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-425">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="390c3-426">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="390c3-426">For example:</span></span>

- <span data-ttu-id="390c3-427">코드를 열기, 만들기, 읽기, 또는 파일을 작성 하 려 하면 모든 종류의 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-427">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="390c3-428">원하는 파일이 존재 하지 않을, 잠긴 상태일 수 있습니다, 그리고 코드 수 하지 권한이 등.</span><span class="sxs-lookup"><span data-stu-id="390c3-428">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="390c3-429">마찬가지로 코드에는 데이터베이스의 레코드를 업데이트 하려고 하는 경우 사용 권한 문제가 발생할 수, 데이터베이스에 연결이 삭제 될 수 있습니다, 그리고 잘못 된 경우 등에 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-429">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="390c3-430">프로그래밍 측면에서 이러한 상황 이라고 *예외*합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-430">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="390c3-431">코드에서 예외가 발생 (throw)를 생성 오류 메시지, 최적 시 사용자에 게 성가신 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-431">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="390c3-433">사용할 수 있는 코드 예외가 발생할 수 있는 경우에서 및이 유형의 오류 메시지를 방지 하기 위해 `Try/Catch` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-433">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="390c3-434">에 `Try` 문을 체크 인하는 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-434">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="390c3-435">하나 이상의 `Catch` 문을 찾을 수 있습니다 특정 발생 했을 수 있는 오류 (특정 유형의 예외).</span><span class="sxs-lookup"><span data-stu-id="390c3-435">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="390c3-436">만큼 포함할 수 있습니다 `Catch` 때 문이 예상 되는 오류에 대 한 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-436">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="390c3-437">사용 하지 않는 것이 좋습니다 합니다 `Response.Redirect` 의 메서드 `Try/Catch` 문을 페이지에서 예외가 발생할 수 있기 때문에 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-437">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>


<span data-ttu-id="390c3-438">다음 예제에서는 첫 번째 요청에서 텍스트 파일을 만들고 다음 사용자가 파일을 열 수 있는 단추를 표시 하는 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-438">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="390c3-439">이 예제에서는 예외가 하면 있도록 의도적으로 잘못 된 파일 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-439">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="390c3-440">코드에 포함 되어 `Catch` 두 가지 가능한 예외에 대 한 문을: `FileNotFoundException`, 파일 이름에 잘못 된 경우 발생 하는 및 `DirectoryNotFoundException`, ASP.NET 폴더를도 찾을 수 없는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-440">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="390c3-441">(모든 항목이 제대로 작동 하는 경우 실행 방식을 확인 하기 위해이 예에서 문은 주석 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="390c3-441">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="390c3-442">코드에서 예외를 처리 하지 않은 경우 이전 스크린 샷에서 처럼 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-442">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="390c3-443">그러나는 `Try/Catch` 섹션은 사용자가 이러한 종류의 오류를 표시 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="390c3-443">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="390c3-444">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="390c3-444">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="390c3-445">참조 설명서</span><span class="sxs-lookup"><span data-stu-id="390c3-445">Reference Documentation</span></span>

- [<span data-ttu-id="390c3-446">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="390c3-446">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="390c3-447">Visual Basic Language</span><span class="sxs-lookup"><span data-stu-id="390c3-447">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
