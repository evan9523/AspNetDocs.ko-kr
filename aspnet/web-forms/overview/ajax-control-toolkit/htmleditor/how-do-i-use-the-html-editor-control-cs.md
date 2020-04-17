---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: HTML 편집기 컨트롤을 사용하려면 어떻게 해야 합니까? (C#) | 마이크로 소프트 문서
author: rick-anderson
description: HTMLEditor는 도구 모음의 버튼을 통해 HTML 콘텐츠를 쉽게 만들고 편집 할 수있는 ASP.NET AJAX 컨트롤입니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: eb3a87f914c24ada52ebb5a315a7e242e96158f7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543121"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a><span data-ttu-id="470b6-104">HTML 편집기 컨트롤을 사용하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="470b6-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="470b6-105">(C#)</span><span class="sxs-lookup"><span data-stu-id="470b6-105">(C#)</span></span>

<span data-ttu-id="470b6-106">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="470b6-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="470b6-107">HTMLEditor는 도구 모음의 버튼을 통해 HTML 콘텐츠를 쉽게 만들고 편집 할 수있는 ASP.NET AJAX 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>

<span data-ttu-id="470b6-108">이 자습서의 목표는 AJAX 제어 도구 키트에 포함된 HTML 편집기 컨트롤에 대한 개요를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="470b6-109">HTML 편집기에는 글꼴 크기 변경, 글꼴 선택, 배경 색 변경, 전경 색상 수정, 링크 추가, 이미지 추가, 텍스트 정렬 변경, 잘라내기, 복사 및 붙여넣기 작업 수행(그림 1 참조)에 대한 옵션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>

<span data-ttu-id="470b6-110">[![HTML 편집기](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="470b6-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="470b6-111">**그림 01**: HTML 편집기[(클릭하여 전체 크기 이미지 보기)](how-do-i-use-the-html-editor-control-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="470b6-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image2.png))</span></span>

<span data-ttu-id="470b6-112">HTML 편집기를 사용하면 디자인 모드를 사용하여 콘텐츠를 입력하거나 HTML을 직접 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="470b6-113">HTML 콘텐츠를 미리 볼 수 있는 옵션도 제공됩니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="470b6-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>

<span data-ttu-id="470b6-114">[![디자인, HTML 및 미리 보기 버튼](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="470b6-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)</span></span>

<span data-ttu-id="470b6-115">**그림 02**: 디자인, HTML 및 미리보기 버튼[(클릭하여 전체 크기 이미지 보기)](how-do-i-use-the-html-editor-control-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="470b6-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image4.png))</span></span>

<span data-ttu-id="470b6-116">이 자습서에서는 HTML 편집기를 표시 하는 방법, HTML 편집기에 나타나는 도구 모음 단추를 사용자 지정 하는 방법 및 교차 사이트 스크립팅 공격을 방지 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="470b6-117">HTML 편집기 표시</span><span class="sxs-lookup"><span data-stu-id="470b6-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="470b6-118">ASP.NET 페이지에서 HTML 편집기를 사용하려면 먼저 페이지에 ScriptManager 컨트롤을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="470b6-119">ScriptManager 컨트롤은 Visual Studio/Visual 웹 개발자 익스프레스 도구 상자의 AJAX 확장 탭 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="470b6-120">페이지의 다른 컨트롤보다 앞에 ScriptManager 컨트롤을 페이지 상단에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="470b6-121">예를 들어, 열기 서버 측 &lt;양식&gt; 태그 바로 아래에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="470b6-122">HTML 편집기 컨트롤은 나머지 AJAX 제어 도구 키트 컨트롤과 함께 도구 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="470b6-123">편집기 컨트롤의 이름이 지정됩니다(그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="470b6-123">It is named the Editor control (see Figure 3).</span></span>

<span data-ttu-id="470b6-124">[![HTML 편집기 컨트롤](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="470b6-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)</span></span>

<span data-ttu-id="470b6-125">**그림 03**: HTML 편집기 컨트롤[(클릭으로 전체 크기 이미지 보기)](how-do-i-use-the-html-editor-control-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="470b6-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image6.png))</span></span>

<span data-ttu-id="470b6-126">HTML 편집기를 페이지로 드래그한 후 속성 시트에서 해당 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="470b6-127">예를 들어 일반적으로 폭 및 높이 속성을 설정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="470b6-128">목록 1에는 HTML 편집기가 포함된 ASP.NET 페이지의 소스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="470b6-129">**목록 1 - SimpleEditor.aspx**</span><span class="sxs-lookup"><span data-stu-id="470b6-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

<span data-ttu-id="470b6-130">목록 1의 페이지에는 HTML 편집기 컨트롤, 단추 컨트롤 및 리터럴 컨트롤이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="470b6-131">단추를 클릭하면 HTML 편집기의 내용이 리터럴 컨트롤에 나타납니다(그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="470b6-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>

<span data-ttu-id="470b6-132">[![HTML 편집기와 함께 양식 제출](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="470b6-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)</span></span>

<span data-ttu-id="470b6-133">**그림 04**: HTML 편집기로 양식 제출[(클릭하려면 전체 크기 이미지 보기)](how-do-i-use-the-html-editor-control-cs/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="470b6-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image8.png))</span></span>

<span data-ttu-id="470b6-134">HTML 편집기 콘텐츠 속성은 HTML 편집기에 입력된 HTML 콘텐츠를 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="470b6-135">이 HTML 콘텐츠에는 자바스크립트가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="470b6-136">다음 섹션에서는 JavaScript 주입 공격을 방지하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="470b6-137">HTML 편집기 도구 모음 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="470b6-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="470b6-138">편집기에서 나타나는 단추를 정확하게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="470b6-139">예를 들어 사용자가 HTML 편집기를 HTML 모드로 전환하지 못하도록 HTML 탭을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="470b6-140">또는 사용자가 포럼 메시지 게시물에서 지나치게 큰 텍스트를 만들지 못하도록 글꼴 크기 드롭다운 목록을 제거할 수 있습니다(그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="470b6-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>

<span data-ttu-id="470b6-141">[![사용자 정의 HTML 편집기](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="470b6-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)</span></span>

<span data-ttu-id="470b6-142">**그림 05**: 사용자 정의 HTML 편집기[(전체 크기 이미지를 보려면 클릭)](how-do-i-use-the-html-editor-control-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="470b6-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-cs/_static/image10.png))</span></span>

<span data-ttu-id="470b6-143">기본 편집기 클래스에서 새 HTML 편집기 파생 을 통해 도구 모음 단추를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="470b6-144">예를 들어 목록 2의 사용자 지정 편집기에는 굵게 및 기울임꼴에 대한 도구 모음 단추만 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="470b6-145">다른 모든 도구 모음 버튼이 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="470b6-146">또한 HTML 탭이 편집기 하단에서 제거되었습니다(하지만 디자인 및 미리 보기 탭은 여전히 있습니다).</span><span class="sxs-lookup"><span data-stu-id="470b6-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="470b6-147">**목록 2\_- 앱 코드\사용자 지정 편집기.cs**</span><span class="sxs-lookup"><span data-stu-id="470b6-147">**Listing 2 - App\_Code\CustomEditor.cs**</span></span>

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

<span data-ttu-id="470b6-148">클래스가 자동으로 컴파일되도록 앱\_코드 폴더에 목록 2의 클래스를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="470b6-149">앱\_코드 폴더가 웹 사이트에 없는 경우 폴더를 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="470b6-150">사용자 지정 편집기를 만든 후 일반 HTML 편집기를 추가하는 것과 동일한 방법으로 ASP.NET 페이지에 추가할 수 있습니다(목록 3 참조).</span><span class="sxs-lookup"><span data-stu-id="470b6-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="470b6-151">**목록 3 - 쇼 사용자 정의 편집기.aspx**</span><span class="sxs-lookup"><span data-stu-id="470b6-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="470b6-152">XSS(교차 사이트 스크립팅) 공격 방지</span><span class="sxs-lookup"><span data-stu-id="470b6-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="470b6-153">사용자의 입력을 수락하고 웹 사이트에 해당 입력을 다시 표시할 때마다 XSS(교차 사이트 스크립팅) 공격에 대한 웹 사이트를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="470b6-154">이론적으로 악의적인 해커는 입력이 다시 표시될 때 실행되는 JavaScript 코드를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="470b6-155">자바 스크립트는 사용자 암호 또는 기타 중요한 정보를 도용하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="470b6-156">일반적으로 웹 페이지에 표시하기 전에 사용자로부터 검색한 입력을 암호화하여 XSS 공격을 물리칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="470b6-157">그러나 HTML 편집기의 출력을 인코딩하면 스크립트 &lt;&gt; 태그를 인코딩할 뿐만 아니라 모든 HTML 태그도 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="470b6-158">즉, 글꼴 유형, 글꼴 크기 및 배경 색과 같은 모든 서식이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="470b6-159">암호, 신용 카드 번호 및 주민등록 번호와 같은 사용자로부터 중요한 정보를 수집하는 경우 HTML 편집기에서 사용자로부터 검색하는 인코딩되지 않은 콘텐츠를 표시해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="470b6-160">HTML 콘텐츠를 다시 표시하지 않거나 신뢰할 수 있는 당사자가 HTML 콘텐츠를 웹 사이트에 제출하는 경우에만 HTML 편집기를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="470b6-161">예를 들어 블로그 응용 프로그램을 만들고 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="470b6-162">이 경우 블로그 게시물을 작성할 때 HTML 편집기를 사용 하는 것이 합리적이다.</span><span class="sxs-lookup"><span data-stu-id="470b6-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="470b6-163">당신은 블로그 게시물을 제출하는 유일한 사람이고, 아마도, 당신은 악의적 인 자바 스크립트를 제출하지 자신을 신뢰할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="470b6-164">그러나 익명 사용자가 주석을 게시할 수 있도록 허용할 때 HTML 편집기를 사용하는 것은 의미가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="470b6-165">사용자가 암호와 같은 중요한 정보를 제출하는 경우 특히 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="470b6-166">악의적인 사용자가 암호를 도용하는 데 적합한 JavaScript가 포함된 댓글을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="470b6-167">요약</span><span class="sxs-lookup"><span data-stu-id="470b6-167">Summary</span></span>

<span data-ttu-id="470b6-168">이 자습서에서는 AJAX 제어 도구 키트에 포함된 HTML 편집기 컨트롤에 대한 간략한 개요를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="470b6-169">HTML 편집기를 사용하여 사용자의 풍부한 콘텐츠를 수락하고 콘텐츠를 서버에 제출하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="470b6-170">또한 HTML 편집기에서 표시되는 도구 모음 단추를 사용자 지정하는 방법에 대해서도 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="470b6-171">마지막으로 HTML 편집기를 사용하여 잠재적으로 악의적인 입력을 수락할 때 사이트 간 스크립팅 공격을 방지하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="470b6-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="470b6-172">다음</span><span class="sxs-lookup"><span data-stu-id="470b6-172">Next</span></span>](how-do-i-use-the-html-editor-control-vb.md)
