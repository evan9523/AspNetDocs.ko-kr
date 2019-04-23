---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: HTML 도우미 (VB)를 빌드하는 TagBuilder 클래스를 사용 하 여 | Microsoft Docs
author: StephenWalther
description: Stephen walther가 ASP.NET MVC 프레임 워크는 TagBuilder 클래스 라는의 유용한 유틸리티 클래스를 소개 합니다. TagBuilder 클래스를 쉽게 사용할 수 있습니다...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 4fe34858aadb705ffb59e06ba805493d89aa4028
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59403209"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a><span data-ttu-id="35cba-104">HTML 도우미 (VB)를 빌드하는 TagBuilder 클래스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="35cba-104">Using the TagBuilder Class to Build HTML Helpers (VB)</span></span>

<span data-ttu-id="35cba-105">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="35cba-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="35cba-106">Stephen walther가 ASP.NET MVC 프레임 워크는 TagBuilder 클래스 라는의 유용한 유틸리티 클래스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="35cba-107">HTML 태그를 쉽게 빌드하는 TagBuilder 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-107">You can use the TagBuilder class to easily build HTML tags.</span></span>


<span data-ttu-id="35cba-108">ASP.NET MVC 프레임 워크는 TagBuilder 클래스 HTML 도우미를 작성할 때 사용할 수 있는 유용한 유틸리티 클래스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="35cba-109">TagBuilder 클래스는 클래스의 이름에서 알 수 있듯이, 빌드할 수 있도록 쉽게 HTML 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="35cba-110">이 간략 한 자습서는 TagBuilder 클래스의 개요가 제공 됩니다 및 HTML을 렌더링 하는 간단한 HTML 도우미를 작성 하는 경우이 클래스를 사용 하는 방법에 알아봅니다 &lt;img&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="35cba-111">TagBuilder 클래스 개요</span><span class="sxs-lookup"><span data-stu-id="35cba-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="35cba-112">TagBuilder 클래스 System.Web.Mvc 네임 스페이스에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="35cba-113">다섯 가지 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-113">It has five methods:</span></span>

- <span data-ttu-id="35cba-114">AddCssClass() – 새로 추가할 수 있습니다 *클래스 = ""* 태그에 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-114">AddCssClass() – Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="35cba-115">GenerateId()-를 사용 하면 태그 id 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-115">GenerateId() – Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="35cba-116">이 메서드는 id에서 마침표를 자동으로 대체 (기본적으로 기간 밑줄로 바뀝니다)</span><span class="sxs-lookup"><span data-stu-id="35cba-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="35cba-117">MergeAttribute()-를 사용 하는 태그에 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-117">MergeAttribute() – Enables you to add attributes to a tag.</span></span> <span data-ttu-id="35cba-118">이 메서드의 여러 오버 로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="35cba-119">SetInnerText()-를 사용 하면 태그의 내부 텍스트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-119">SetInnerText() – Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="35cba-120">내부 텍스트 HTML 인코딩 자동입니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="35cba-121">Tostring ()-를 사용 하면 태그를 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-121">ToString() – Enables you to render the tag.</span></span> <span data-ttu-id="35cba-122">일반 태그, 시작 태그, 끝 태그 또는 자체 닫음 태그를 만들 것인지 여부를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>
  

<span data-ttu-id="35cba-123">TagBuilder 클래스에는 네 가지 중요 한 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="35cba-124">특성-모든 태그의 특성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-124">Attributes – Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="35cba-125">IdAttributeDotReplacement – 기간 (기본값은 밑줄)를 바꾸는 데 GenerateId() 메서드에서 문자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-125">IdAttributeDotReplacement – Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="35cba-126">InnerHTML – 태그의 내부 콘텐츠를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-126">InnerHTML – Represents the inner contents of the tag.</span></span> <span data-ttu-id="35cba-127">이 속성에 문자열을 할당 *하지 않습니다* HTML 문자열을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="35cba-128">TagName – 태그의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-128">TagName – Represents the name of the tag.</span></span>

<span data-ttu-id="35cba-129">이러한 메서드 및 속성 사용 하면 모든 기본 메서드 및 HTML 태그를 작성 해야 하는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="35cba-130">실제로 TagBuilder 클래스를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="35cba-131">StringBuilder 클래스를 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="35cba-132">그러나는 TagBuilder 클래스를 사용 하면 업무를 더 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="35cba-133">이미지 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="35cba-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="35cba-134">TagBuilder 클래스의 인스턴스를 만들면 빌드하는 TagBuilder 생성자에 원하는 태그의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="35cba-135">다음으로 태그의 특성을 수정할 수 MergeAttribute() 메서드와 AddCssClass와 같은 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="35cba-136">마지막으로 태그를 렌더링 하는 tostring () 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="35cba-137">예를 들어 목록 1 이미지 HTML 도우미를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="35cba-138">이미지 도우미는 HTML을 나타내는 TagBuilder를 사용 하 여 내부적으로 구현 됩니다 &lt;img&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="35cba-139">**Listing 1 – Helpers\ImageHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="35cba-139">**Listing 1 – Helpers\ImageHelper.vb**</span></span>

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

<span data-ttu-id="35cba-140">목록 1에서 모듈 Image() 라는 두 개의 오버 로드 된 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-140">The module in Listing 1 contains two overloaded methods named Image().</span></span> <span data-ttu-id="35cba-141">Image() 메서드를 호출 하면 여부 HTML 특성의 집합을 나타내는 개체를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="35cba-142">TagBuilder.MergeAttribute() 메서드를 사용 하는 TagBuilder에 src 특성 등의 개별 특성을 추가 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="35cba-143">또한 확인 TagBuilder.MergeAttributes() 메서드를 사용 하는 TagBuilder 특성의 컬렉션을 추가 하는 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="35cba-144">MergeAttributes() 메서드에서 사전을&lt;문자열, 개체&gt; 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="35cba-145">RouteValueDictionary 클래스 사전에 특성의 컬렉션을 나타내는 개체를 변환 하는 데 사용 됩니다&lt;문자열, 개체&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="35cba-146">이미지 도우미를 만든 후에 모든 다른 표준 HTML 도우미와 마찬가지로 ASP.NET MVC 보기에서 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="35cba-147">목록 2 뷰 이미지 도우미를 사용 하 여 Xbox의 동일한 이미지를 두 번 표시할 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="35cba-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="35cba-148">포함 및 제외 HTML 특성 컬렉션을 모두 Image() 도우미 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="35cba-149">**Listing 2 – Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="35cba-149">**Listing 2 – Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]


<span data-ttu-id="35cba-150">[![새 프로젝트 대화 상자](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="35cba-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="35cba-151">**그림 01**: 이미지 도우미를 사용 하 여 ([클릭 하 여 큰 이미지 보기](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="35cba-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span></span>


<span data-ttu-id="35cba-152">알림 Index.aspx 뷰의 맨 위에 있는 이미지 도우미에 연결 된 네임 스페이스를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="35cba-153">도우미는 다음 지시문을 사용 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

<span data-ttu-id="35cba-154">Visual Basic 응용 프로그램을 기본 네임 스페이스는 응용 프로그램의 이름과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cba-154">In a Visual Basic application, the default namespace is the same as the name of the application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="35cba-155">[이전](creating-custom-html-helpers-vb.md)
> [다음](creating-page-layouts-with-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="35cba-155">[Previous](creating-custom-html-helpers-vb.md)
[Next](creating-page-layouts-with-view-master-pages-vb.md)</span></span>
