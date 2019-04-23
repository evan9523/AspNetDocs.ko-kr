---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Razor 구문 (C#)를 사용 하 여 ASP.NET 웹 프로그래밍 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 장의 개요를 제공 프로그래밍의 ASP.NET 웹 페이지를 사용 하 여 Razor 구문을 사용 합니다. ASP.NET은 동적 웹 pa를 실행 하기 위한 Microsoft의 기술 하는 중...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: 8237dc6b925ccefc5b411aebc8e7c399dcdc6746
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59407356"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="15080-104">Razor 구문 (C#)를 사용 하 여 ASP.NET 웹 프로그래밍 소개</span><span class="sxs-lookup"><span data-stu-id="15080-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>

<span data-ttu-id="15080-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="15080-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="15080-106">이 문서에서는 프로그래밍 개요 ASP.NET 웹 페이지 Razor 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="15080-107">ASP.NET은 웹 서버에서 동적 웹 페이지를 실행 하기 위한 Microsoft의 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="15080-108">이 문서는 C# 프로그래밍 언어를 사용 하 여 포커스입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="15080-109">**학습할**:</span><span class="sxs-lookup"><span data-stu-id="15080-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="15080-110">프로그래밍 팁 Razor 구문을 사용 하 여 ASP.NET 웹 페이지 프로그래밍 시작 하기 위한 상위 8입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="15080-111">기본 프로그래밍 개념을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="15080-112">어떤 ASP.NET 서버 코드 및 Razor 구문에 대 한 all입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="15080-113">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="15080-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="15080-114">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="15080-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="15080-115">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="the-top-8-programming-tips"></a><span data-ttu-id="15080-116">상위 8 프로그래밍 팁</span><span class="sxs-lookup"><span data-stu-id="15080-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="15080-117">이 섹션에서는 반드시 알아야 할 Razor 구문을 사용 하 여 ASP.NET 서버 코드 작성을 시작 하는 몇 가지 팁을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="15080-118">Razor 구문을 C# 프로그래밍 언어를 기준으로 하며는 ASP.NET 웹 페이지를 사용 하 여 가장 자주 사용 되는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="15080-119">그러나 Razor 구문을 Visual Basic 언어 및 Visual Basic에서도 수행할 수 있는 모든 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="15080-120">자세한 내용은 부록을 참조 하세요 [Visual Basic 언어와 구문이](https://go.microsoft.com/fwlink/?LinkId=202908)합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>


<span data-ttu-id="15080-121">대부분의 이러한 프로그래밍 기법에 대 한 자세한 내용은 문서의 뒷부분에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="15080-122">1. 코드를 사용 하 여 페이지를 추가 하 여 @ 문자</span><span class="sxs-lookup"><span data-stu-id="15080-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="15080-123">`@` 문자 인라인 식, 단일 문 블록 및 다중 문 블록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="15080-124">다음은 이러한 문이 페이지를 브라우저에서 실행할 때 모양을입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="15080-126">**HTML 인코딩**</span><span class="sxs-lookup"><span data-stu-id="15080-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="15080-127">사용 하 여 페이지의 콘텐츠를 표시 하는 `@` 문자를 앞의 예에서 같이 ASP.NET을 HTML로 인코딩하고 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="15080-128">이 예약 된 HTML 문자를 대체 (같은 `<` 하 고 `>` 및 `&`) 문자가 HTML 태그 또는 엔터티로 해석 되지 않고 웹 페이지에 표시할 문자를 사용 하도록 설정 하는 코드를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="15080-129">HTML 인코딩하지 않고 서버 코드의 출력을 올바르게 표시 되지 않 및 페이지 보안 위험에 노출 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="15080-130">목표는 태그로 태그를 렌더링 하는 HTML 태그를 출력 하는 경우 (예를 들어 `<p></p>` 단락 또는 `<em></em>` 텍스트를 강조 하기 위해), 섹션을 참조 하세요 [결합 텍스트, 태그 및 코드 블록의 코드](#BM_CombiningTextMarkupAndCode) 이 문서의 뒷부분에 나오는.</span><span class="sxs-lookup"><span data-stu-id="15080-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="15080-131">읽어보세요에서 HTML 인코딩에 대 한 [양식 작업](https://go.microsoft.com/fwlink/?LinkId=202892)합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>


### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="15080-132">2. 코드 블록을 중괄호로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="15080-133">A *코드 블록* 하나 이상의 코드 문을 포함 하 고 중괄호로 묶입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="15080-134">브라우저에 표시 된 결과:</span><span class="sxs-lookup"><span data-stu-id="15080-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="15080-136">3. 세미콜론을 사용 하 여 각 코드 문 블록 내 종료</span><span class="sxs-lookup"><span data-stu-id="15080-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="15080-137">코드 블록 내 각 전체 코드 문은 세미콜론으로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="15080-138">인라인 식 세미콜론으로 끝나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="15080-139">4. 변수를 사용 하 여 값을 저장 하려면</span><span class="sxs-lookup"><span data-stu-id="15080-139">4. You use variables to store values</span></span>

<span data-ttu-id="15080-140">값을 저장할 수 있습니다는 *변수*, 문자열, 숫자 및 날짜 등을 포함 합니다. 사용 하 여 새 변수를 만든를 `var` 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="15080-141">사용 하 여 페이지에서 직접 변수 값을 삽입할 수는 있지만 `@`합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="15080-142">브라우저에 표시 된 결과:</span><span class="sxs-lookup"><span data-stu-id="15080-142">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="15080-144">5. 리터럴 문자열 값 큰따옴표로 묶어야</span><span class="sxs-lookup"><span data-stu-id="15080-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="15080-145">A *문자열* 텍스트로 처리 되는 문자 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="15080-146">문자열을 지정 하려면 묶습니다 큰따옴표:</span><span class="sxs-lookup"><span data-stu-id="15080-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="15080-147">표시 하려는 문자열 백슬래시 문자를 포함 하는 경우 ( `\` ) 큰따옴표 또는 ( `"` )를 사용 하 여를 *축 자 문자열 리터럴은* 접두사로 하는 `@` 연산자.</span><span class="sxs-lookup"><span data-stu-id="15080-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="15080-148">(C#의 경우에 \ 축 자 문자열 리터럴을 사용 하지 않는 한 문자에 특별 한 의미가 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="15080-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="15080-149">큰따옴표를 포함 하려면 축 자 문자열 리터럴을 사용 하 여 및 따옴표를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="15080-150">두이 예제 모두를 사용 하 여 페이지에서 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-150">Here's the result of using both of these examples in a page:</span></span>

![Razor Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="15080-152">에 `@` 문자는 C#에서 축 자 문자열 리터럴은 표시 하 고 ASP.NET 페이지에서 코드를 표시 하기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>


### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="15080-153">6. 코드는 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="15080-153">6. Code is case sensitive</span></span>

<span data-ttu-id="15080-154">C#에서는 키워드 (같은 `var`, `true`, 및 `if`) 변수 이름은 대/소문자 구분 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="15080-155">코드의 다음 줄은 두 개의 다른 변수를 만듭니다 `lastName` 및 `LastName.`</span><span class="sxs-lookup"><span data-stu-id="15080-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="15080-156">변수를 선언 하는 경우 `var lastName = "Smith";` 페이지에서 해당 변수를 참조 하려는 경우 `@LastName`, 오류가 발생 하기 때문에 `LastName` 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-156">If you declare a variable as `var lastName = "Smith";` and if you try to reference that variable in your page as `@LastName`, an error results because `LastName` won't be recognized.</span></span>

> [!NOTE]
> <span data-ttu-id="15080-157">키워드 및 변수는 Visual basic에서는 *되지* 대 소문자를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>


### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="15080-158">7. 개체를 포함 하는 대부분의 코딩</span><span class="sxs-lookup"><span data-stu-id="15080-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="15080-159">*개체* 사용 하 여 프로그래밍할 수 있는 것을 나타내는 &#8212; 페이지, 텍스트 상자, 파일, 이미지, 웹 요청, 전자 메일 메시지, 고객 레코드 (데이터베이스 행) 등입니다. 개체 특징을 설명 하는 속성이 있고 읽기 또는 변경할 수 있습니다 &#8212; 텍스트 상자 개체의를 `Text` 등 속성인 요청 개체에는 `Url` 속성인 전자 메일 메시지에는 `From` 속성 고객 개체에는 `FirstName` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="15080-160">개체 수도 있는 메서드를 &quot;동사&quot; 을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="15080-161">파일 개체의 예로 `Save` 메서드를 이미지 개체의 `Rotate` 메서드 및 전자 메일 개체의 `Send` 메서드.</span><span class="sxs-lookup"><span data-stu-id="15080-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="15080-162">자주 사용 하는 `Request` 개체를 텍스트 상자 (폼 필드)의 값과 같은 정보를 제공 하는 브라우저 종류 요청, 페이지, 사용자 id 등의 URL을 한 페이지에서. 다음 예제에서는 속성에 액세스 하는 방법을 보여 줍니다는 `Request` 개체와 호출 하는 방법을 합니다 `MapPath` 메서드의 `Request` 서버의 페이지의 절대 경로 제공 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="15080-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="15080-163">브라우저에 표시 된 결과:</span><span class="sxs-lookup"><span data-stu-id="15080-163">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="15080-165">8. 의사 결정 하는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="15080-166">동적 웹 페이지의 핵심 기능은 조건에 따라 수행할 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="15080-167">이 작업을 수행 하는 가장 일반적인 방법은 된 합니다 `if` 문 (및 선택적 `else` 문).</span><span class="sxs-lookup"><span data-stu-id="15080-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="15080-168">문이 `if(IsPost)` 작성 하는 약식 방법 `if(IsPost == true)`합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="15080-169">와 함께 `if` 문 다양 한 조건에서 반복 코드 블록을 테스트 하는 방법 및 등과이 문서의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="15080-170">브라우저에 표시 된 결과 (클릭 한 후 **제출**):</span><span class="sxs-lookup"><span data-stu-id="15080-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="15080-172">HTTP GET 및 POST 메서드는 IsPost 속성</span><span class="sxs-lookup"><span data-stu-id="15080-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="15080-173">웹 페이지 (HTTP)에 사용 된 프로토콜 매우 제한 된 수의 서버에 요청을 확인 하는 데 사용 되는 메서드 (동사)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="15080-174">두 가지 자주 사용 되는 가져오기에 사용 되는 페이지를 읽으려는 및 페이지를 제출 하는 데 사용 되는 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="15080-175">일반적으로 사용자가 페이지를 요청할 처음 페이지가 요청 될 GET을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="15080-176">사용자 양식을 채우고 다음 제출 단추를 클릭을 하는 경우 브라우저는 서버에는 POST 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15080-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="15080-177">웹 프로그래밍에서 유용 여부는 페이지 요청 POST 또는 GET으로 페이지를 처리 하는 방법을 알 수 있도록 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="15080-178">ASP.NET 웹 페이지에서 사용할 수는 `IsPost` 속성 GET 또는 POST 요청 인지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="15080-179">요청을 POST 이면는 `IsPost` 속성은 true를 반환 하 고 폼의 입력란의 값 등 읽기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="15080-180">표시 되는 많은 예제 값에 따라 다르게 페이지를 처리 하는 방법을 보여 줍니다. `IsPost`합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>


## <a name="a-simple-code-example"></a><span data-ttu-id="15080-181">간단한 코드 예제</span><span class="sxs-lookup"><span data-stu-id="15080-181">A Simple Code Example</span></span>

<span data-ttu-id="15080-182">이 절차에서는 기본적인 프로그래밍 기술을 설명 하는 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15080-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="15080-183">예제에서는 입력 하 고 두 숫자를 추가 하 고 결과 표시 하는 사용자가 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15080-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="15080-184">편집기에서 새 파일을 만들고 이름을 *AddNumbers.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="15080-185">페이지에 이미 아무 것도 대체 페이지에 다음 코드와 태그를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="15080-186">알아두어야 할 몇 가지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="15080-187">합니다 `@` 문자 페이지에서 첫 번째 코드 블록을 시작 하 고 뒤에 나오는 `totalMessage` 페이지 하단에 있는 포함 된 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="15080-188">페이지의 맨 위에 있는 블록은 중괄호로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="15080-189">맨 위에 있는 블록의 모든 줄은 세미콜론으로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="15080-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="15080-190">변수 `total`, `num1`를 `num2`, 및 `totalMessage` 여러 숫자 및 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="15080-191">에 할당 된 리터럴 문자열 값을 `totalMessage` 큰따옴표로 변수가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="15080-192">코드는 경우 대/소문자를 구분 하기 때문에 `totalMessage` 변수를 사용 하 여 페이지 아래쪽에 있는, 이름과 맨 위에 있는 변수를 정확 하 게 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="15080-193">식 `num1.AsInt() + num2.AsInt()` 개체 및 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15080-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="15080-194">`AsInt` 메서드 각 변수에 대해에서 산술을 수행할 수 있도록 수 (정수)는 사용자가 입력 한 문자열을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="15080-195">`<form>` 태그를 포함 한 `method="post"` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="15080-196">사용자가 지정 하는 **추가**, 페이지 HTTP POST 메서드를 사용 하 여 서버에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="15080-197">페이지가 제출 되 면는 `if(IsPost)` true 및 조건부 테스트로 코드 실행, 숫자를 더한 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="15080-198">페이지를 저장 하 고 브라우저에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="15080-199">(페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.) 두 정수를 입력 한 다음 클릭 합니다 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="15080-201">기본 프로그래밍 개념</span><span class="sxs-lookup"><span data-stu-id="15080-201">Basic Programming Concepts</span></span>

<span data-ttu-id="15080-202">이 문서에서는 ASP.NET 웹 프로그래밍 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="15080-203">철저 한 검사를 자주 사용 됩니다 프로그래밍 개념을 통해 둘러보기 방금 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="15080-204">이 경우에 설명 거의 모든 ASP.NET Web Pages 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="15080-205">첫 번째 하지만 거의 기술적 배경입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="15080-206">Razor 구문, 서버 코드 및 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="15080-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="15080-207">Razor 구문은 웹 페이지에서 서버 기반 코드를 포함 하기 위한 단순 프로그래밍 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="15080-208">Razor 구문을 사용 하 여 웹 페이지에는 두 종류의 콘텐츠: 클라이언트가 콘텐츠 및 서버 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="15080-209">클라이언트 콘텐츠는 웹 페이지에는 항목: HTML 태그 (요소), CSS, JavaScript 및 일반 텍스트와 같은 일부 클라이언트 스크립트 아마도 등 스타일 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="15080-210">Razor 구문에는이 클라이언트 콘텐츠 서버 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="15080-211">서버는 페이지를 브라우저로 보내기 전에 페이지에서 서버 코드를 코드 먼저 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="15080-212">서버를 실행 하 여 코드를 단독으로 서버 기반 데이터베이스 액세스와 같은 클라이언트 콘텐츠를 사용 하 여 작업을 수행 하는 훨씬 더 복잡 해질 수 있는 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="15080-213">가장 중요 한 점은 서버 코드가 동적으로 만들 수 클라이언트 콘텐츠 &#8212; 수 HTML 태그나 기타 콘텐츠를 즉석에서 생성 하 고 다음 페이지를 포함할 수 있는 정적 HTML과 함께 브라우저에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="15080-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="15080-214">브라우저의 관점에서 서버 코드에 의해 생성 되는 콘텐츠를 클라이언트가 콘텐츠를 다른 모든 클라이언트가 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="15080-215">이미 살펴보았듯이, 필요한 서버 코드는 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="15080-216">ASP.NET 웹 페이지 Razor 구문을 포함 하는 특수 한 파일 확장명이 (*.cshtml* 하거나 *.vbhtml*).</span><span class="sxs-lookup"><span data-stu-id="15080-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="15080-217">서버는 이러한 확장을 인식, Razor 구문을 사용 하 여 표시 되 고 페이지에서 브라우저로 보내는 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="15080-218">ASP.NET 적합 하는 위치</span><span class="sxs-lookup"><span data-stu-id="15080-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="15080-219">Razor 구문은 ASP.NET에 기반으로 하는 Microsoft.NET Framework를 호출 하는 Microsoft 기술을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="15080-220">.NET Framework는 모든 유형의 응용 프로그램 컴퓨터 거의 개발 하기 위한 Microsoft의 빅, 포괄적인 프로그래밍 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="15080-221">ASP.NET은 웹 응용 프로그램을 만들기 위한 특별히 설계 된.NET Framework의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="15080-222">개발자가 전 세계의 다양 한 가장 크고 가장 트래픽이 많은 웹 사이트를 만드는 ASP.NET을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="15080-223">(언제 든 지 표시 파일 이름 확장명 *.aspx* 사이트에서 URL의 일부로, 알 수 있습니다 사이트 ASP.NET을 사용 하 여 작성 되었습니다.)</span><span class="sxs-lookup"><span data-stu-id="15080-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="15080-224">Razor 구문에도 쉽게 배울 초보자 생산성가 있는 경우 본인이 전문가일 경우는 간소화 된 구문을 사용 하는 ASP.NET의 모든 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="15080-225">이 구문은 간단 하 게 사용 하는 경우에 ASP.NET 및.NET Framework 제품군의 관계가 웹 사이트 보다 정교 해지면 있다고 할 수 있는 더 큰 프레임 워크의 기능을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="15080-227">**클래스 및 인스턴스**</span><span class="sxs-lookup"><span data-stu-id="15080-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="15080-228">ASP.NET 서버 코드 클래스의 개념을 이해에 기본 제공 되는 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="15080-229">클래스 정의 또는 템플릿 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="15080-230">예를 들어, 응용 프로그램에 포함 될 수 있습니다는 `Customer` 속성 및 메서드는 모든 customer 개체를 정의 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="15080-231">인스턴스를 만들고 응용 프로그램을 실제 고객 정보를 사용 하 여 작동 해야 하는 경우 (또는 *인스턴스화합니다*) customer 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="15080-232">각 개별 고객은 별도의 인스턴스는 `Customer` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="15080-233">모든 인스턴스가 동일한 속성 및 메서드를 지원 하지만 각 customer 개체가 고유 하므로 각 인스턴스에 대 한 속성 값은 일반적으로 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="15080-234">한 고객 개체에는 `LastName` 속성에는 "Smith" 수 있습니다 다른 고객 개체에서는 `LastName` 속성 "Jones." 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="15080-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="15080-235">마찬가지로 모든 개별 웹 페이지 사이트에서이 `Page` 의 인스턴스인 개체를 `Page` 클래스.</span><span class="sxs-lookup"><span data-stu-id="15080-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="15080-236">페이지의 단추를 `Button` 개체의 인스턴스를는 `Button` 클래스 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="15080-237">각 인스턴스는 고유한 특징이 있지만 모든 기반으로 하는 개체의 클래스 정의에 지정 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>


## <a name="basic-syntax"></a><span data-ttu-id="15080-238">기본 구문</span><span class="sxs-lookup"><span data-stu-id="15080-238">Basic Syntax</span></span>

<span data-ttu-id="15080-239">이전 기본 예제는 ASP.NET 웹 페이지의 페이지를 만드는 방법 및 서버 코드는 HTML 태그를 추가 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="15080-240">다음 Razor 구문을 사용 하 여 ASP.NET 서버 코드를 작성 하는 기본 사항을 알아봅니다 &#8212; , 프로그래밍 언어 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="15080-241">프로그래밍 경험이 있는 경우 (C를 사용한 경우에 특히 C++, C#, Visual Basic 또는 JavaScript)를 읽는 여기의 대부분에 게 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="15080-242">기능을 살펴보고 서버 코드가 태그에 추가 하는 방법을 익히는 필요할 것 *.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="15080-243">텍스트, 태그 및 코드 블록의 코드를 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="15080-244">서버 코드 블록에서 하려는 경우가 많습니다 출력 텍스트 또는 태그 (또는 둘 다) 페이지.</span><span class="sxs-lookup"><span data-stu-id="15080-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="15080-245">서버 코드 블록을 텍스트 코드 없는 하는 대신 렌더링할지 그대로 있으면 ASP.NET 코드에서 해당 텍스트를 구분할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="15080-246">다음과 같은 여러 가지 방법으로 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-246">There are several ways to do this.</span></span>

- <span data-ttu-id="15080-247">와 같은 HTML 요소에 텍스트를 묶으십시오 `<p></p>` 또는 `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="15080-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="15080-248">HTML 요소는 텍스트, HTML 요소 추가 및 서버 코드 식에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="15080-249">ASP.NET에서 여는 HTML 태그를 표시 하는 경우 (예를 들어 `<p>`), 요소를 포함 한 모든 렌더링 및으로 해당 콘텐츠 브라우저 네요 서버 코드 식을 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="15080-250">사용 된 `@:` 연산자 또는 `<text>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="15080-251">합니다 `@:` 일반 텍스트 또는 일치 하지 않는 HTML 태그를 포함 하는 콘텐츠의 단일 줄을 출력 합니다 `<text>` 요소 출력에 여러 줄을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="15080-252">이러한 옵션은 출력의 일부로 HTML 요소를 렌더링 하지 않을 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="15080-253">여러 줄 텍스트 또는 일치 하지 않는 HTML 태그를 출력 하려는 경우 사용 하 여 각 줄 앞 `@:`에서 줄을 묶을 수 있습니다 또는 `<text>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="15080-254">같은 합니다 `@:` 연산자를`<text>` 태그는 텍스트 콘텐츠를 ASP.NET에 사용 되며 페이지 출력에는 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="15080-255">첫 번째 예제에서는 앞의 예제를 반복 하지만 단일 쌍을 사용 하 여 `<text>` 태그를 렌더링할 텍스트를 묶으십시오.</span><span class="sxs-lookup"><span data-stu-id="15080-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="15080-256">두 번째 예제에서는 합니다 `<text>` 하 고 `</text>` 태그는 모두 일부 포함 되지 않은 텍스트와 일치 하지 않는 HTML 태그 세 줄을 묶습니다 (`<br />`), 서버 코드와 일치 하는 HTML 태그와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="15080-257">마찬가지로 수도 앞에 개별적으로 각 줄은 `@:` 연산자; 둘 다 방식으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="15080-258">이 섹션에 표시 된 대로 텍스트를 출력할 때 &#8212; HTML 요소를 사용 하는 `@:` 연산자와 `<text>` 요소 &#8212; ASP.NET 하지 HTML 인코딩 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="15080-259">(ASP.NET 서버 코드 식 및 서버 코드 블록 뒤에 나오는의 출력을 인코딩하는 앞에서 설명한 대로 `@`를 제외 하 고이 섹션에서 설명 하는 특수 한 현상.)</span><span class="sxs-lookup"><span data-stu-id="15080-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="15080-260">Whitespace</span><span class="sxs-lookup"><span data-stu-id="15080-260">Whitespace</span></span>

<span data-ttu-id="15080-261">문에서 (및 문자열 리터럴 외부에서) 공백이 문이 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="15080-262">문의 줄 바꿈을 문에서 영향을 주지 않습니다 개이고 가독성을 위해 문을 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="15080-263">다음 문은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="15080-264">그러나 문자열 리터럴로 중간 줄을 둘러쌀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="15080-265">다음 예제에서는 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="15080-266">위의 코드와 같이 여러 줄으로 줄 바꿈되는 긴 문자열을 결합 하려면 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="15080-267">연결 연산자를 사용할 수 있습니다 (`+`),이 문서의 뒷부분에서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="15080-268">사용할 수도 있습니다는 `@` 만들려면 축 자 문자열 리터럴,이 문서의 앞부분에서 본 것 처럼 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="15080-269">여러 줄 축 자 문자열 리터럴은 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="15080-270">코드 (및 태그) 주석</span><span class="sxs-lookup"><span data-stu-id="15080-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="15080-271">주석 자신 또는 다른 사용자에 대 한 정보를 그대로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="15080-272">사용 하지 않도록 할 수 있습니다 (*주석*) 코드 또는 태그를 시간에 대 한 페이지에 유지 하려고 하지만 실행 하지 않으려는의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="15080-273">다양 한 구문 및 HTML 태그에 대 한 Razor 코드의 주석 처리 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="15080-274">모든 Razor 코드에서와 마찬가지로 Razor 주석은 처리 (및 제거) 페이지를 브라우저로 전송 되기 전에 서버에서.</span><span class="sxs-lookup"><span data-stu-id="15080-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="15080-275">따라서 Razor 주석 구문을 파일을 편집 하지만 페이지의 소스에도 사용자가 표시 되지 경우 볼 수 있는 주석을 코드에 (또는 태그에도)를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="15080-276">ASP.NET Razor 주석에 대 한로 주석을 시작 하기 `@*` 사용 하 여 종료 및 `*@`합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="15080-277">주석 줄 또는 여러 줄에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="15080-278">다음은 코드 블록 내에서 주석이입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="15080-279">다음 코드 줄을 사용 하 여 코드의 동일한 블록 주석 처리 되어 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="15080-280">Razor 주석 구문을 사용 하는 대신 코드 블록 내부의 C#과 같은 사용 중인 프로그래밍 언어의 주석 구문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="15080-281">C#에서는 단일 줄 주석 앞에 `//` 로 시작 하는 문자 및 여러 줄 주석 `/*` 하 고 끝나야 `*/`합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="15080-282">(Razor 주석은와 마찬가지로 C# 주석 렌더링 되지 않습니다 브라우저로.)</span><span class="sxs-lookup"><span data-stu-id="15080-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="15080-283">이미 알고 계시 겠지만, 태그에 대 한 HTML 주석을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="15080-284">HTML 주석 시작 `<!--` 문자와 끝나는 `-->`합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="15080-285">HTML 주석 텍스트 뿐 아니라도 페이지에 유지 하려고 하지만 렌더링 하지 않으려는 모든 HTML 태그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="15080-286">이 HTML 주석 태그와 포함 된 텍스트의 전체 내용을 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="15080-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="15080-287">Razor 주석, HTML 주석 달리 *는* 페이지로 렌더링 사용자 페이지의 소스를 확인 하 여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="15080-288">Razor C#의 중첩 된 블록에 제약이 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="15080-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="15080-289">자세한 내용은 참조 하세요. [라는 C# 변수와 중첩 블록 손상 코드 생성](http://aspnetwebstack.codeplex.com/workitem/1914)</span><span class="sxs-lookup"><span data-stu-id="15080-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="15080-290">변수</span><span class="sxs-lookup"><span data-stu-id="15080-290">Variables</span></span>

<span data-ttu-id="15080-291">변수는 데이터를 저장 하는 데 사용 하는 명명 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="15080-292">변수를 아무 것도 이름을 지정할 수 있습니다 하지만 이름은 영문자로 시작 해야 하 고 공백 또는 예약 된 문자를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="15080-293">변수 및 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="15080-293">Variables and Data Types</span></span>

<span data-ttu-id="15080-294">변수는 어떤 종류의 데이터를 변수에 저장 됨을 나타내는 특정 데이터 형식에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="15080-295">문자열 값을 저장 하는 문자열 변수를 할 수 있습니다 (같은 &quot;Hello world&quot;), 다양 한 형식 (예: 2012/4/12 또는 2009 년 3 월의에서 날짜 값을 저장 하는 정수 값 (예: 3 또는 79)를 저장 하는 정수 변수 및 날짜 ).</span><span class="sxs-lookup"><span data-stu-id="15080-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="15080-296">및 다른 여러 데이터 형식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="15080-297">그러나 일반적으로 필요가 변수의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="15080-298">대부분의 경우 ASP.NET의 변수 데이터를 어떻게 사용 되 고 있는지에 따라 형식을 알아낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="15080-299">(형식을 지정 해야 하는 경우에 따라,이 참 이어야 하는 예제 표시 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="15080-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="15080-300">사용 하는 변수를 선언 합니다 `var` 키워드 (형식 지정 않으려는) 하는 경우 또는 형식의 이름을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="15080-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="15080-301">다음 예제에서는 웹 페이지에서 변수의 몇 가지 일반적인 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15080-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="15080-302">페이지에서 이전 예제와 결합 하면 브라우저에 표시 된이 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="15080-304">변환 및 데이터 형식 테스트</span><span class="sxs-lookup"><span data-stu-id="15080-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="15080-305">일반적으로 ASP.NET 데이터 형식을 자동으로 확인할 수 있습니다, 있지만 경우에 따라 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="15080-306">따라서 명시적 변환을 수행 하 여 ASP.NET을 도와줄 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="15080-307">형식을 변환 하는 것이 없는, 하는 경우에 때때로 것이 좋습니다 테스트 하려는 어떤 유형의 데이터를 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="15080-308">가장 일반적인 경우는 정수 또는 날짜와 같은 다른 형식으로 문자열을 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="15080-309">다음 예제에서는 문자열을 숫자로 변환 해야 여기서는 일반적인 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15080-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="15080-310">일반적으로 사용자 입력을 문자열로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="15080-311">사용자 번호를 입력 하 라는 메시지가 표시 한 경우에을 때 사용자 입력을 제출 하 고 코드에서 읽을 때 숫자를 입력 한 경우에 데이터를 문자열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="15080-312">따라서 문자열을 숫자로 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="15080-313">예에서를 변환 하지 않고 값에 산술 연산을 수행 하려는 경우 다음 오류가 발생을 ASP.NET 두 문자열을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="15080-314">*'Int' ' string '를 암시적으로 변환할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="15080-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="15080-315">정수 값으로 변환 하려면 호출을 `AsInt` 메서드.</span><span class="sxs-lookup"><span data-stu-id="15080-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="15080-316">변환이 성공한 경우에 다음 숫자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="15080-317">다음 표에서 변수에 대 한 몇 가지 일반적인 변환 및 테스트 메서드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="15080-318"><strong>메서드</strong></span><span class="sxs-lookup"><span data-stu-id="15080-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-319"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="15080-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-320"><strong>예제</strong></span><span class="sxs-lookup"><span data-stu-id="15080-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-321">정수 (예: "593") 정수를 나타내는 문자열을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-322">와 같은 문자열 변환 &quot;true&quot; 또는 &quot;false&quot; 부울 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-323">와 같은 10 진수 값이 있는 문자열로 변환 &quot;1.3&quot; 또는 &quot;7.439&quot; 부동 소수점 수입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-324">와 같은 10 진수 값이 있는 문자열로 변환 &quot;1.3&quot; 하거나 &quot;7.439&quot; 소수입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="15080-325">(ASP.NET, 10 진수는 부동 소수점 숫자를 보다 정확 합니다.)</span><span class="sxs-lookup"><span data-stu-id="15080-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-326">Asp.net은 날짜 및 시간 값을 나타내는 문자열을 변환 `DateTime` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-327">다른 데이터 형식 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="15080-328">연산자</span><span class="sxs-lookup"><span data-stu-id="15080-328">Operators</span></span>

<span data-ttu-id="15080-329">연산자는 키워드 또는 식에서 수행할 수 있는 명령의 종류를 ASP.NET에 지시 하는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="15080-330">C# 언어 (및 Razor 구문을 기반으로 하는) 다양 한 연산자를 지원 하지만 시작 하려면 몇 가지를 인식 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="15080-331">다음 표에서 가장 일반적인 연산자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15080-331">The following table summarizes the most common operators.</span></span>


:::row:::
    :::column:::
    <span data-ttu-id="15080-332"><strong>Operator</strong></span><span class="sxs-lookup"><span data-stu-id="15080-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-333"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="15080-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-334"><strong>예제</strong></span><span class="sxs-lookup"><span data-stu-id="15080-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-335">숫자 식에 사용 되는 수학 연산자.</span><span class="sxs-lookup"><span data-stu-id="15080-335">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-336">할당.</span><span class="sxs-lookup"><span data-stu-id="15080-336">Assignment.</span></span> <span data-ttu-id="15080-337">왼쪽에 있는 개체 문의 오른쪽에 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-337">Assigns the value on the right side of a statement to the object on the left side.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-338">같음</span><span class="sxs-lookup"><span data-stu-id="15080-338">Equality.</span></span> <span data-ttu-id="15080-339">반환 `true` 값이 같으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-339">Returns `true` if the values are equal.</span></span> <span data-ttu-id="15080-340">(의 차이 확인 합니다 `=` 연산자 및 `==` 연산자입니다.)</span><span class="sxs-lookup"><span data-stu-id="15080-340">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-341">같지 않음</span><span class="sxs-lookup"><span data-stu-id="15080-341">Inequality.</span></span> <span data-ttu-id="15080-342">반환 `true` 값 같지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="15080-342">Returns `true` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-343">작은-큰 보다-보다 작음-보다-또는-같음 및 크거나 같음.</span><span class="sxs-lookup"><span data-stu-id="15080-343">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-344">연결 문자열을 조인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-344">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="15080-345">ASP.NET이이 연산자는 식의 데이터 형식을 기반으로 하는 더하기 연산자 간의 차이점을 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-345">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+=` `-=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-346">증가 및 감소 연산자의 추가 하 고 변수에서 각각 1을 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="15080-346">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-347">점입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-347">Dot.</span></span> <span data-ttu-id="15080-348">개체 및 해당 속성 및 메서드를 구분 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-348">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-349">괄호입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-349">Parentheses.</span></span> <span data-ttu-id="15080-350">그룹 식 및 매개 변수를 전달할 메서드를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-350">Used to group expressions and to pass parameters to methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-351">대괄호입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-351">Brackets.</span></span> <span data-ttu-id="15080-352">배열 또는 컬렉션의 값에 액세스 하기 위해 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-352">Used for accessing values in arrays or collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-353">되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-353">Not.</span></span> <span data-ttu-id="15080-354">반대로 `true` 값을 `false` 그 반대로 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-354">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="15080-355">일반적으로 테스트 하는 약식 방법으로 사용 `false` (즉,에 대 한 없습니다 `true`).</span><span class="sxs-lookup"><span data-stu-id="15080-355">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&&` `||`
    :::column-end:::
    :::column:::
    <span data-ttu-id="15080-356">논리적 AND 또는 및 연결 하는 데 사용 되는 조건 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-356">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="15080-357">파일 및 코드의 폴더 경로 사용 하 여 작업</span><span class="sxs-lookup"><span data-stu-id="15080-357">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="15080-358">종종 코드에서 파일 및 폴더 경로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-358">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="15080-359">개발 컴퓨터에 나타나는 웹 사이트에 대 한 실제 폴더 구조의 예 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-359">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="15080-360">Url 및 경로 대 한 몇 가지 필수 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-360">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="15080-361">도메인 이름을 사용 하 여 시작 URL (`http://www.example.com`) 또는 서버 이름 (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="15080-361">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="15080-362">URL은 호스트 컴퓨터의 실제 경로에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-362">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="15080-363">예를 들어 `http://myserver` 폴더에 해당할 수 있습니다 *C:\websites\mywebsite* 서버의 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-363">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="15080-364">가상 경로 전체 경로 지정 하지 않고도 코드에서 경로 나타내는 축약형입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-364">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="15080-365">도메인 또는 서버 이름 다음에 나오는 URL 부분을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-365">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="15080-366">가상 경로 사용 하는 경우에 경로 업데이트 하지 않고도 다른 도메인 또는 서버에 코드를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-366">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="15080-367">차이점을 이해 하는 데 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-367">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="15080-368">전체 URL</span><span class="sxs-lookup"><span data-stu-id="15080-368">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="15080-369">서버 이름</span><span class="sxs-lookup"><span data-stu-id="15080-369">Server name</span></span> | <span data-ttu-id="15080-370">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="15080-370">*mycompanyserver*</span></span> |
| <span data-ttu-id="15080-371">가상 경로</span><span class="sxs-lookup"><span data-stu-id="15080-371">Virtual path</span></span> | <span data-ttu-id="15080-372">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="15080-372">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="15080-373">실제 경로</span><span class="sxs-lookup"><span data-stu-id="15080-373">Physical path</span></span> | <span data-ttu-id="15080-374">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="15080-374">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="15080-375">가상 루트가 / 드라이브는 c:의 루트와 마찬가지로 \입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-375">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="15080-376">(가상 폴더 경로 항상 슬래시를 사용 합니다.) 폴더의 가상 경로 실제 폴더 이름이 같은 필요가 없습니다. 별칭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-376">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="15080-377">(프로덕션 서버에서 가상 경로 거의 일치 하는 실제 경로 정확 하 게 합니다.)</span><span class="sxs-lookup"><span data-stu-id="15080-377">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="15080-378">코드에서 파일 및 폴더를 사용 하 여 작업할 때의 실제 경로 및 경우에 따라 사용 하는 개체에 따라 가상 경로 참조 해야 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-378">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="15080-379">ASP.NET이 도구를 제공 하면 이러한 코드에서 파일 및 폴더 경로 사용 하 여 작업에 대 한: 합니다 `Server.MapPath` 메서드 및 `~` 연산자 및 `Href` 메서드.</span><span class="sxs-lookup"><span data-stu-id="15080-379">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="15080-380">실제 가상 경로로 변환: Server.MapPath 메서드</span><span class="sxs-lookup"><span data-stu-id="15080-380">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="15080-381">합니다 `Server.MapPath` 메서드는 가상 경로 변환 (같은 */default.cshtml*) 절대 실제 경로에 (같은 *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="15080-381">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="15080-382">전체 실제 경로 필요할 때 언제 든이이 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-382">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="15080-383">일반적인 예로 읽거나 텍스트 파일 또는 웹 서버의 이미지 파일을 작성 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-383">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="15080-384">일반적으로 알 수 없는 호스팅 사이트 서버의 사이트의 절대 실제 경로 알고이 메서드는 경로 변환할 수 있도록-가상 경로-를 서버에 해당 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-384">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="15080-385">파일 또는 폴더 메서드에 가상 경로 전달 하 고 실제 경로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-385">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="15080-386">가상 루트 참조:는 ~ 연산자 및 Href 메서드</span><span class="sxs-lookup"><span data-stu-id="15080-386">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="15080-387">에 *.cshtml* 또는 *.vbhtml* 파일을 사용 하 여 가상 루트 경로 참조할 수 있습니다는 `~` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-387">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="15080-388">사이트에서 페이지를 이동할 수 있으며 다른 페이지에 포함 된 모든 링크는 손상 되지 때문에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-388">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="15080-389">그 어느 때 다른 위치로 웹 사이트를 이동 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-389">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="15080-390">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-390">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="15080-391">웹 사이트가 `http://myserver/myapp`, 이러한 경로 페이지가 실행 될 때 ASP.NET에서 어떻게 처리 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-391">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="15080-392">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="15080-392">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="15080-393">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="15080-393">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="15080-394">(실제로 이러한 경로 변수 값으로 표시 되지 않습니다 하지만 어떤는 처럼 ASP.NET 경로 처리 합니다.)</span><span class="sxs-lookup"><span data-stu-id="15080-394">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="15080-395">사용할 수는 `~` 연산자 위와 같이 서버 코드와 같이 태그에서:</span><span class="sxs-lookup"><span data-stu-id="15080-395">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="15080-396">태그를 사용 하 여는 `~` 연산자를 이미지 파일, 다른 웹 페이지 및 CSS 파일 같은 리소스에 대 한 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15080-396">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="15080-397">ASP.NET 페이지 (코드 및 태그)를 통해 찾아 해결 하는 모든 페이지를 실행 하는 경우는 `~` 적절 한 경로에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-397">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="15080-398">조건부 논리 및 루프</span><span class="sxs-lookup"><span data-stu-id="15080-398">Conditional Logic and Loops</span></span>

<span data-ttu-id="15080-399">ASP.NET 서버 코드를 사용 하면 조건에 따라 작업을 수행 하 고 특정 횟수 만큼 명령문을 반복 하는 코드를 작성할 수 있습니다 (즉, 루프를 실행 하는 코드).</span><span class="sxs-lookup"><span data-stu-id="15080-399">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="15080-400">테스트 조건</span><span class="sxs-lookup"><span data-stu-id="15080-400">Testing Conditions</span></span>

<span data-ttu-id="15080-401">사용할 간단한 조건을 테스트 하는 `if` 지정한 테스트를 기반으로 true 또는 false를 반환 하는 문:</span><span class="sxs-lookup"><span data-stu-id="15080-401">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="15080-402">`if` 키워드는 블록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-402">The `if` keyword starts a block.</span></span> <span data-ttu-id="15080-403">실제 테스트 (조건) 괄호로 이며 true 또는 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-403">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="15080-404">테스트가 true 인 경우를 실행 하는 문은 중괄호로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-404">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="15080-405">`if` 문을 포함할 수는 `else` 조건이 false 인 경우 실행할 문을 지정 하는 블록:</span><span class="sxs-lookup"><span data-stu-id="15080-405">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="15080-406">사용 하 여 여러 조건을 추가할 수 있습니다는 `else if` 블록:</span><span class="sxs-lookup"><span data-stu-id="15080-406">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="15080-407">이 예제에서는 첫 번째 조건이 if 블록이 true가 아니면는 `else if` 조건이 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-407">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="15080-408">조건이 충족 될 경우의 문에서 `else if` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-408">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="15080-409">어떤 조건 충족 되 면의 문에서 `else` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-409">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="15080-410">다른 경우 원하는 만큼 추가할 수 있습니다 블록 및를 사용 하 여 닫습니다는 `else` 으로 차단 합니다 &quot;등등&quot; 조건.</span><span class="sxs-lookup"><span data-stu-id="15080-410">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="15080-411">많은 수의 조건 테스트 하려면 사용을 `switch` 블록:</span><span class="sxs-lookup"><span data-stu-id="15080-411">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="15080-412">괄호 안에 테스트할 값입니다 (예에서는 `weekday` 변수).</span><span class="sxs-lookup"><span data-stu-id="15080-412">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="15080-413">각 개별 테스트를 사용 하는 `case` 콜론 (:)로 끝나는 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-413">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="15080-414">하는 경우의 값을 `case` 테스트 값과 일치 하는 문, 해당 case 블록의 코드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-414">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="15080-415">각 case 문을 사용 하 여 닫을 `break` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-415">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="15080-416">(각 나누기를 포함 해야 하는 경우 `case` 블록에서 다음 코드를 `case` 문을 에서도 실행 됩니다.) A `switch` 블록 같으며를 `default` 에 대 한 마지막 경우로 문은 &quot;등등&quot; 다른 경우에 없는 경우 실행 되는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-416">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="15080-417">브라우저에 표시 된 마지막 두 조건부 블록의 결과:</span><span class="sxs-lookup"><span data-stu-id="15080-417">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="15080-419">코드를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-419">Looping Code</span></span>

<span data-ttu-id="15080-420">자주 반복적으로 동일한 문을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-420">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="15080-421">반복 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-421">You do this by looping.</span></span> <span data-ttu-id="15080-422">예를 들어, 종종 문을 실행 하면 동일한 각 항목에 대 한 데이터의 컬렉션에서입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-422">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="15080-423">사용할 수 있습니다 정확 하 게 하는 횟수를 반복 하려면를 알고 있는 경우는 `for` 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-423">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="15080-424">이러한 종류의 루프까지 셈 카운트다운에 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-424">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="15080-425">로 시작 하는 루프를 `for` 세미콜론으로 종료 각 키워드 뒤에 괄호로 세 문입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-425">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="15080-426">첫 번째 문은 괄호 안에 (`var i=10;`) 카운터를 만들고 10으로 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-426">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="15080-427">카운터 이름 필요가 `i` &#8212; 모든 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-427">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="15080-428">경우는 `for` 루프가 실행, 카운터가 자동으로 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-428">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="15080-429">두 번째 문은 (`i < 21;`) 개수를 계산 하려면 정도 대 한 조건을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-429">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="15080-430">최대 20으로 이동 하려는 경우 (즉, 계속 해 서이 카운터는 21 보다 작거나 동안).</span><span class="sxs-lookup"><span data-stu-id="15080-430">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="15080-431">세 번째 문은 (`i++` ) 카운터는 루프가 실행 될 때마다 추가 1 있어야 함을 지정 하는 증분 연산자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-431">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="15080-432">중괄호 안의 루프의 각 반복에 대해 실행 되는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-432">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="15080-433">태그 새 단락을 만듭니다 (`<p>` 요소) 각 시간 및의 값을 표시할 출력에 줄을 추가 `i` (카운터).</span><span class="sxs-lookup"><span data-stu-id="15080-433">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="15080-434">이 페이지를 실행 하면 항목 수를 나타내는 각 줄의 텍스트를 사용 하 여 출력을 표시 하는 11 줄을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15080-434">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="15080-436">컬렉션 또는 배열을 사용 하 여 작업할 경우 자주 사용 하는 `foreach` 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-436">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="15080-437">컬렉션은 유사한 개체의 그룹 및 `foreach` 루프는 컬렉션의 각 항목에서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-437">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="15080-438">이 유형의 루프는 컬렉션에 대 한 편리한 있으므로 달리는 `for` 루프 필요가 카운터를 증가 시키거나 제한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-438">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="15080-439">대신는 `foreach` 루프 코드 컬렉션을 통해 완료 될 때까지 간단히 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-439">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="15080-440">다음 코드의 항목을 반환 하는 예를 들어를 `Request.ServerVariables` 은 웹 서버에 대 한 정보를 포함 하는 개체 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-440">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="15080-441">사용 하 여는 `foreac` 각 항목의 이름을 새 표시할 h 루프 `<li>` HTML 글머리 기호 목록의 요소에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-441">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="15080-442">`foreach` 키워드 뒤에 괄호가 컬렉션의 단일 항목을 나타내는 변수를 선언 하는 위치가 (예에서 `var item`) 뒤를 `in` 키워드를 반복 하려는 컬렉션에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-442">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="15080-443">본문에는 `foreach` 루프 앞에서 선언한 변수를 사용 하 여 현재 항목에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-443">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="15080-445">보다 일반적인 루프를 만들려면 사용 합니다 `while` 문:</span><span class="sxs-lookup"><span data-stu-id="15080-445">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="15080-446">`while` 루프 시작 합니다 `while` 키워드 뒤에 괄호 루프가 계속 되는 기간을 지정 하는 (여기에 대 한으로 `countNum` 경우 50 미만), then 블록을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-446">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="15080-447">루프는 일반적으로 증가 (추가) 또는 감소 (에서 빼기) 변수 또는 계산에 사용 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-447">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="15080-448">예에서는 `+=` 연산자에는 1을 더하여 `countNum` 루프가 실행 될 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-448">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="15080-449">(카운트다운 되는 루프에서 변수를 감소 시키기 위해 감소 연산자를 사용 하는 `-=`).</span><span class="sxs-lookup"><span data-stu-id="15080-449">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="15080-450">개체 및 컬렉션</span><span class="sxs-lookup"><span data-stu-id="15080-450">Objects and Collections</span></span>

<span data-ttu-id="15080-451">ASP.NET 웹 사이트의 거의 모든 항목은 웹 페이지 자체를 포함 하 여 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-451">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="15080-452">이 섹션에서는 자주 사용 하 여 코드에서 몇 가지 중요 한 개체를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-452">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="15080-453">Page 개체</span><span class="sxs-lookup"><span data-stu-id="15080-453">Page Objects</span></span>

<span data-ttu-id="15080-454">ASP.NET에서 가장 기본적인 개체는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-454">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="15080-455">조건에 맞는 개체 없이 직접 page 개체의 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-455">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="15080-456">다음 코드는 페이지의 파일 경로 가져오고 사용 하는 `Request` 페이지의 개체:</span><span class="sxs-lookup"><span data-stu-id="15080-456">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="15080-457">있도록 명확 현재 페이지 개체에 메서드와 속성을 참조 하는 선택적으로 사용할 수 키워드 `this` 코드에서 페이지 개체를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-457">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="15080-458">사용 하 여 이전 코드 예제와 같습니다 `this` 추가 페이지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="15080-458">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="15080-459">속성을 사용할 수는 `Page` 와 같은 많은 정보를 가져올 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-459">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="15080-460">`Request`.</span><span class="sxs-lookup"><span data-stu-id="15080-460">`Request`.</span></span> <span data-ttu-id="15080-461">이미 살펴보았듯이, 요청, 페이지, 사용자 id 등의 URL을 수행 하는 브라우저 종류를 포함 하 여 현재 요청에 대 한 정보 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-461">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="15080-462">`Response`.</span><span class="sxs-lookup"><span data-stu-id="15080-462">`Response`.</span></span> <span data-ttu-id="15080-463">서버 코드 실행이 완료 된 경우 브라우저에 보낼 응답 (페이지)에 대 한 정보 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-463">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="15080-464">예를 들어이 속성을 사용 하 여 응답에 정보를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-464">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="15080-465">컬렉션 개체 (배열 및 사전을)</span><span class="sxs-lookup"><span data-stu-id="15080-465">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="15080-466">A *컬렉션* 컬렉션과 같은 동일한 유형의 개체의 그룹인 `Customer` 데이터베이스에서 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-466">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="15080-467">ASP.NET와 같은 많은 기본 제공 컬렉션을 포함 합니다 `Request.Files` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-467">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="15080-468">컬렉션의 데이터를 자주 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-468">You'll often work with data in collections.</span></span> <span data-ttu-id="15080-469">두 가지 일반적인 컬렉션 형식은 합니다 *배열* 하며 *사전*합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-469">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="15080-470">배열 유사 항목 컬렉션을 저장 하 고 싶지만를 각 항목을 보유 하는 별도 변수를 만들지 않으려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-470">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="15080-471">배열에서 특정 데이터 형식을 선언와 같은 `string`, `int`, 또는 `DateTime`합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-471">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="15080-472">변수 배열을 포함할 수 있습니다, 선언에 대괄호를 추가 하 (같은 `string[]` 또는 `int[]`).</span><span class="sxs-lookup"><span data-stu-id="15080-472">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="15080-473">항목의 위치 (인덱스)를 사용 하는 배열 또는 사용 하 여 액세스할 수 있습니다는 `foreach` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-473">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="15080-474">배열 인덱스는 0부터 시작 &#8212; 즉, 첫 번째 항목은에서 위치 0, 두 번째 항목은 위치 1입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-474">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="15080-475">시작 하 여 배열에 있는 항목의 수를 확인할 수 있습니다 해당 `Length` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-475">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="15080-476">배열 검색) (배열에서 특정 항목의 위치를 가져오려면는 `Array.IndexOf` 메서드.</span><span class="sxs-lookup"><span data-stu-id="15080-476">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="15080-477">수행할 수도 있습니다 역방향 등 배열의 내용을 (합니다 `Array.Reverse` 메서드) 또는 콘텐츠를 정렬 (합니다 `Array.Sort` 메서드).</span><span class="sxs-lookup"><span data-stu-id="15080-477">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="15080-478">브라우저에 표시 하는 문자열 배열 코드의 출력:</span><span class="sxs-lookup"><span data-stu-id="15080-478">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="15080-480">사전이 같습니다 키/값 쌍의 컬렉션을 설정 하거나 해당 값을 검색 키 (또는 이름)을 제공 하는 위치</span><span class="sxs-lookup"><span data-stu-id="15080-480">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="15080-481">사용할 사전을 만들려면는 `new` 키워드를 새 사전 개체를 만드는 동안 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-481">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="15080-482">사용 하 여 변수를 사전에 할당할 수 있습니다는 `var` 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-482">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="15080-483">꺾쇠 괄호를 사용 하 여 사전에 있는 항목의 데이터 형식을 ( `< >` ).</span><span class="sxs-lookup"><span data-stu-id="15080-483">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="15080-484">선언의 끝 실제로 새 사전을 만듭니다 하는 방법 이기 때문에 괄호의 쌍을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-484">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="15080-485">사전에 항목을 추가 하려면 호출할 수 있습니다 합니다 `Add` 사전 변수의 메서드 (`myScores` 이 경우), 키 및 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-485">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="15080-486">또는 키를 나타내고 다음 예제와 같이 단순한 할당을 수행 하려면 대괄호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-486">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="15080-487">사전에서 값을 가져오려면 대괄호로 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-487">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="15080-488">매개 변수를 사용 하 여 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-488">Calling Methods with Parameters</span></span>

<span data-ttu-id="15080-489">이 문서의 앞부분에서 읽은 것 처럼 개체를 사용 하 여 프로그래밍 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-489">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="15080-490">예를 들어, 한 `Database` 개체에 있을 `Database.Connect` 메서드.</span><span class="sxs-lookup"><span data-stu-id="15080-490">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="15080-491">여러 방법에는 하나 이상의 매개 변수 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-491">Many methods also have one or more parameters.</span></span> <span data-ttu-id="15080-492">A *매개 변수* 메서드에 전달 하는 값은 해당 작업을 완료 하는 메서드를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-492">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="15080-493">예를 들어,에 대 한 선언을 확인 된 `Request.MapPath` 세 개의 매개 변수를 사용 하는 메서드:</span><span class="sxs-lookup"><span data-stu-id="15080-493">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="15080-494">(줄 읽기 쉽게 표시 하였습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-494">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="15080-495">기억 하는 내부 문자열 제외 하 고 배치 하는 거의 모든 줄 바꿈을 넣을 수 있습니다 따옴표에 포함 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="15080-495">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="15080-496">이 메서드는 지정된 된 가상 경로에 해당 하는 서버의 실제 경로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-496">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="15080-497">메서드에 대 한 세 가지 매개 변수는 `virtualPath`하십시오 `baseVirtualDir`, 및 `allowCrossAppMapping`합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-497">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="15080-498">(알 수 있습니다 선언 매개 변수를 수락 하 게 하는 데이터의 데이터 형식으로 나열 됩니다.) 이 메서드를 호출 하는 경우 모든 세 매개 변수에 대 한 값을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-498">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="15080-499">Razor 구문을 메서드에 매개 변수를 전달 하기 위한 두 가지 옵션을 제공 합니다. *위치 매개 변수* 하 고 *명명 된 매개 변수*합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-499">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="15080-500">위치 매개 변수를 사용 하 여 메서드를 호출 하는 엄격한 순서를 메서드 선언에 지정 된 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-500">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="15080-501">(일반적으로 알 수이 순서 메서드에 대 한 설명서를 참조 하 여.) 순서를 따라야 하며 매개 변수를 건너뛸 수 없습니다 &#8212; 하는 경우 필요한 전달 하면 빈 문자열 (`""`) 또는 `null` 에 대 한 값이 없는 위치 매개 변수에 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-501">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="15080-502">다음 예제에서는 라는 폴더가 있다고 가정 *스크립트* 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-502">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="15080-503">호출 된 `Request.MapPath` 메서드와 전달 올바른 순서로 세 가지 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-503">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="15080-504">다음의 결과 매핑된 경로가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-504">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="15080-505">경우는 메서드가 여러 매개 변수를 유지할 수 있습니다 코드 보다 읽기 쉬운 명명 된 매개 변수를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-505">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="15080-506">명명 된 매개 변수를 사용 하 여 메서드를 호출 하려면 매개 변수 이름 뒤에 콜론 (:) 및 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-506">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="15080-507">명명 된 매개 변수의 장점은 원하는 순서에 관계 없이 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-507">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="15080-508">(단점은 메서드 호출으로 compact 아닙니다.)</span><span class="sxs-lookup"><span data-stu-id="15080-508">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="15080-509">다음 예제에서는 위와 같은 메서드를 호출 하지만 명명 된 값을 제공 하는 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-509">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="15080-510">알 수 있듯이 다른 순서로 매개 변수 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-510">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="15080-511">그러나 앞의 예제 및이 예제를 실행 하는 경우 동일한 값을 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-511">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="15080-512">오류 처리</span><span class="sxs-lookup"><span data-stu-id="15080-512">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="15080-513">Try / Catch 문</span><span class="sxs-lookup"><span data-stu-id="15080-513">Try-Catch Statements</span></span>

<span data-ttu-id="15080-514">종종 컨트롤 외부 이유로 실패할 수 있는 코드에 문의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-514">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="15080-515">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="15080-515">For example:</span></span>

- <span data-ttu-id="15080-516">코드를 만들거나 파일에 액세스 하려고 하면, 모든 종류의 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-516">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="15080-517">원하는 파일이 존재 하지 않을, 잠긴 상태일 수 있습니다, 그리고 코드 수 하지 권한이 등.</span><span class="sxs-lookup"><span data-stu-id="15080-517">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="15080-518">마찬가지로 코드에는 데이터베이스의 레코드를 업데이트 하려고 하는 경우 사용 권한 문제가 발생할 수, 데이터베이스에 연결이 삭제 될 수 있습니다, 그리고 잘못 된 경우 등에 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15080-518">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="15080-519">프로그래밍 측면에서 이러한 상황 이라고 *예외*합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-519">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="15080-520">코드에서 예외가 발생 (throw)를 생성 오류 메시지, 사용자에 게 기껏해야 성가 시 거:</span><span class="sxs-lookup"><span data-stu-id="15080-520">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="15080-522">사용할 수 있는 코드 예외가 발생할 수 있는 경우에서 및이 유형의 오류 메시지를 방지 하기 위해 `try/catch` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="15080-522">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="15080-523">에 `try` 문을 체크 인하는 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-523">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="15080-524">하나 이상의 `catch` 문을 찾을 수 있습니다 특정 발생 했을 수 있는 오류 (특정 유형의 예외).</span><span class="sxs-lookup"><span data-stu-id="15080-524">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="15080-525">만큼 포함할 수 있습니다 `catch` 문을 때 예상 하는 오류에 대 한 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-525">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="15080-526">사용 하지 않는 것이 좋습니다 합니다 `Response.Redirect` 의 메서드 `try/catch` 문을 페이지에서 예외가 발생할 수 있기 때문에 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-526">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>


<span data-ttu-id="15080-527">다음 예제에서는 첫 번째 요청에서 텍스트 파일을 만들고 다음 사용자가 파일을 열 수 있는 단추를 표시 하는 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15080-527">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="15080-528">이 예제에서는 예외가 하면 있도록 의도적으로 잘못 된 파일 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-528">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="15080-529">코드에 포함 되어 `catch` 두 가지 가능한 예외에 대 한 문을: `FileNotFoundException`, 파일 이름에 잘못 된 경우 발생 하는 및 `DirectoryNotFoundException`, ASP.NET 폴더를도 찾을 수 없는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-529">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="15080-530">(모든 항목이 제대로 작동 하는 경우 실행 방식을 확인 하기 위해이 예에서 문은 주석 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="15080-530">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="15080-531">코드에서 예외를 처리 하지 않은 경우 이전 스크린 샷에서 처럼 오류 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15080-531">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="15080-532">그러나는 `try/catch` 섹션은 사용자가 이러한 종류의 오류를 표시 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="15080-532">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="15080-533">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="15080-533">Additional Resources</span></span>

<span data-ttu-id="15080-534">**Visual Basic을 사용한 프로그래밍**</span><span class="sxs-lookup"><span data-stu-id="15080-534">**Programming with Visual Basic**</span></span>


[<span data-ttu-id="15080-535">부록: Visual Basic 언어 및 구문</span><span class="sxs-lookup"><span data-stu-id="15080-535">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)


<span data-ttu-id="15080-536">**참조 설명서**</span><span class="sxs-lookup"><span data-stu-id="15080-536">**Reference Documentation**</span></span>


[<span data-ttu-id="15080-537">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="15080-537">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="15080-538">C# 언어</span><span class="sxs-lookup"><span data-stu-id="15080-538">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)
