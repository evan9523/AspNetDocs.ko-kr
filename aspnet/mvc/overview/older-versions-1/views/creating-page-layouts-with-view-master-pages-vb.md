---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: 마스터 페이지 보기(VB)를 사용할 수 있는 페이지 레이아웃 만들기 | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서에서는 보기 마스터 페이지를 활용하여 응용 프로그램의 여러 페이지에 대한 공통 페이지 레이아웃을 만드는 방법을 배웁니다. 당신은 사용할 수 있습니다 ...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 37b8d858c72357ebbe51458f76511a9672b01b4d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542497"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a><span data-ttu-id="1400d-104">보기 마스터 페이지를 사용하여 페이지 레이아웃 만들기(VB)</span><span class="sxs-lookup"><span data-stu-id="1400d-104">Creating Page Layouts with View Master Pages (VB)</span></span>

<span data-ttu-id="1400d-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1400d-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="1400d-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="1400d-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> <span data-ttu-id="1400d-107">이 자습서에서는 보기 마스터 페이지를 활용하여 응용 프로그램의 여러 페이지에 대한 공통 페이지 레이아웃을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="1400d-108">예를 들어 보기 마스터 페이지를 사용하여 두 열 페이지 레이아웃을 정의하고 웹 응용 프로그램의 모든 페이지에 대해 두 열 레이아웃을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="1400d-109">마스터 페이지 보기를 사용할 수 있는 페이지 레이아웃 만들기</span><span class="sxs-lookup"><span data-stu-id="1400d-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="1400d-110">이 자습서에서는 보기 마스터 페이지를 활용하여 응용 프로그램의 여러 페이지에 대한 공통 페이지 레이아웃을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="1400d-111">예를 들어 보기 마스터 페이지를 사용하여 두 열 페이지 레이아웃을 정의하고 웹 응용 프로그램의 모든 페이지에 대해 두 열 레이아웃을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="1400d-112">또한 보기 마스터 페이지를 활용하여 응용 프로그램의 여러 페이지에서 공통 콘텐츠를 공유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="1400d-113">예를 들어 보기 마스터 페이지에 웹 사이트 로고, 탐색 링크 및 배너 광고를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="1400d-114">이렇게 하면 응용 프로그램의 모든 페이지에 이 콘텐츠가 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="1400d-115">이 자습서에서는 새 보기 마스터 페이지를 만들고 마스터 페이지를 기반으로 새 보기 콘텐츠 페이지를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="1400d-116">뷰 마스터 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="1400d-116">Creating a View Master Page</span></span>

<span data-ttu-id="1400d-117">먼저 두 개의 열 레이아웃을 정의하는 뷰 마스터 페이지를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="1400d-118">View\Shared 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **추가, 새 항목**및 MVC 뷰 마스터 페이지 템플릿을 선택하여 MVC 프로젝트에 새 뷰 마스터 페이지를 추가합니다(그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="1400d-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the  MVC View Master Page template (see Figure 1).</span></span>

<span data-ttu-id="1400d-119">[![보기 마스터 페이지 추가](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)</span></span>

<span data-ttu-id="1400d-120">**그림 01**: 뷰 마스터 페이지 추가[(전체 크기 이미지를 보려면 클릭)](creating-page-layouts-with-view-master-pages-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))</span></span>

<span data-ttu-id="1400d-121">응용 프로그램에서 두 개 이상의 뷰 마스터 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="1400d-122">각 뷰 마스터 페이지는 다른 페이지 레이아웃을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="1400d-123">예를 들어 특정 페이지에 2열 레이아웃과 다른 페이지에 3열 레이아웃이 있어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="1400d-124">뷰 마스터 페이지는 표준 ASP.NET MVC 보기와 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="1400d-125">그러나 일반 보기와 달리 뷰 마스터 페이지에는 `<asp:ContentPlaceHolder>` 하나 이상의 태그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="1400d-126">태그는 `<contentplaceholder>` 개별 콘텐츠 페이지에서 재정의할 수 있는 마스터 페이지의 영역을 표시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="1400d-127">예를 들어 목록 1의 뷰 마스터 페이지는 두 개의 열 레이아웃을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="1400d-128">여기에는 `<contentplaceholder>` 두 개의 태그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="1400d-129">각 `<ContentPlaceHolder>` 열에 대해 하나씩.</span><span class="sxs-lookup"><span data-stu-id="1400d-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="1400d-130">**리스팅 1 –`Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="1400d-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

<span data-ttu-id="1400d-131">목록 1의 뷰 마스터 페이지의 본문에는 두 열에 해당하는 두 `<div>` 개의 태그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="1400d-132">계단식 스타일 시트 열 클래스는 `<div>` 두 태그에 모두 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="1400d-133">이 클래스는 마스터 페이지 의 맨 위에 선언된 스타일 시트에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="1400d-134">디자인 보기로 전환하여 뷰 마스터 페이지가 렌더링되는 방법을 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="1400d-135">소스 코드 편집기 왼쪽 하단에 있는 디자인 탭을 클릭합니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="1400d-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>

<span data-ttu-id="1400d-136">[![디자이너의 마스터 페이지 미리 보기](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)</span></span>

<span data-ttu-id="1400d-137">**그림 02**: 디자이너의 마스터 페이지 미리 보기[(전체 크기 이미지를 보려면 클릭)](creating-page-layouts-with-view-master-pages-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))</span></span>

### <a name="creating-a-view-content-page"></a><span data-ttu-id="1400d-138">보기 콘텐츠 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="1400d-138">Creating a View Content Page</span></span>

<span data-ttu-id="1400d-139">뷰 마스터 페이지를 만든 후 보기 마스터 페이지를 기반으로 하나 이상의 보기 콘텐츠 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="1400d-140">예를 들어 View\Home 폴더를 마우스 오른쪽 단추로 클릭하고, **추가, 새 항목**선택, **MVC 보기 콘텐츠 페이지** 템플릿 선택, Index.aspx 이름 입력 및 추가 단추를 클릭하여 홈 컨트롤러의 인덱스 보기 콘텐츠 페이지를 만들 수 있습니다(그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="1400d-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the Add button (see Figure 3).</span></span>

<span data-ttu-id="1400d-141">[![보기 콘텐츠 페이지 추가](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)</span></span>

<span data-ttu-id="1400d-142">**그림 03**: 보기 콘텐츠 페이지 추가[(전체 크기 이미지를 보려면 클릭)](creating-page-layouts-with-view-master-pages-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))</span></span>

<span data-ttu-id="1400d-143">추가 단추를 클릭하면 보기 콘텐츠 페이지와 연결할 보기 마스터 페이지를 선택할 수 있는 새 대화 상자가 나타납니다(그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="1400d-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="1400d-144">이전 섹션에서 만든 Site.master 보기 마스터 페이지로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>

<span data-ttu-id="1400d-145">[![마스터 페이지 선택](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)</span></span>

<span data-ttu-id="1400d-146">**그림 04**: 마스터 페이지 선택[(전체 크기 이미지를 보려면 클릭)](creating-page-layouts-with-view-master-pages-vb/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))</span></span>

<span data-ttu-id="1400d-147">Site.master 마스터 페이지를 기반으로 새 보기 콘텐츠 페이지를 만든 후 목록 2에서 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="1400d-148">**리스팅 2 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="1400d-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

<span data-ttu-id="1400d-149">이 보기에는 `<asp:Content>` 뷰 마스터 페이지의 각 `<asp:ContentPlaceHolder>` 태그에 해당하는 태그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="1400d-150">각 `<asp:Content>` 태그에는 재정의하는 특정 `<asp:ContentPlaceHolder>` 을 가리키는 ContentPlaceHolderID 특성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="1400d-151">또한 목록 2의 콘텐츠 보기 페이지에는 일반적인 HTML 태그가 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="1400d-152">예를 들어, 개폐 `<html>` 또는 `<head>` 태그를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="1400d-153">모든 일반 열기 및 닫는 태그는 뷰 마스터 페이지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="1400d-154">보기 콘텐츠 페이지에 표시하려는 모든 콘텐츠는 `<asp:Content>` 태그 내에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="1400d-155">이러한 태그 외부에 HTML 또는 기타 콘텐츠를 배치하면 페이지를 보려고 할 때 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="1400d-156">콘텐츠 보기 페이지의 마스터 페이지에서 `<asp:ContentPlaceHolder>` 모든 태그를 재정의할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="1400d-157">`<asp:ContentPlaceHolder>` 태그를 특정 콘텐츠로 바꾸려는 경우에만 태그를 재정의하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="1400d-158">예를 들어 목록 3의 수정된 인덱스 `<asp:Content>` 보기에는 두 개의 태그만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="1400d-159">각 태그에는 `<asp:Content>` 일부 텍스트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="1400d-160">**리스팅 3 –`Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="1400d-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

<span data-ttu-id="1400d-161">목록 3의 보기가 요청되면 그림 5의 페이지를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="1400d-162">뷰는 두 개의 열이 있는 페이지를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="1400d-163">또한 뷰 콘텐츠 페이지의 콘텐츠가 뷰 마스터 페이지의 콘텐츠와 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page.</span></span>

<span data-ttu-id="1400d-164">[![인덱스 보기 콘텐츠 페이지](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)</span></span>

<span data-ttu-id="1400d-165">**그림 05**: 색인 보기 콘텐츠 페이지[(전체 크기 이미지를 보려면 클릭)](creating-page-layouts-with-view-master-pages-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))</span></span>

### <a name="modifying-view-master-page-content"></a><span data-ttu-id="1400d-166">보기 마스터 페이지 콘텐츠 수정</span><span class="sxs-lookup"><span data-stu-id="1400d-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="1400d-167">뷰 마스터 페이지로 작업할 때 거의 즉시 발생하는 한 가지 문제는 다른 보기 콘텐츠 페이지가 요청될 때 뷰 마스터 페이지 콘텐츠를 수정하는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="1400d-168">예를 들어 웹 응용 프로그램의 각 페이지에 고유한 제목을 두도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="1400d-169">그러나 제목은 보기 콘텐츠 페이지가 아니라 뷰 마스터 페이지에 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="1400d-170">그렇다면 각 보기 콘텐츠 페이지의 페이지 제목을 어떻게 사용자 지정합니까?</span><span class="sxs-lookup"><span data-stu-id="1400d-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="1400d-171">보기 콘텐츠 페이지에 표시되는 제목을 수정하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="1400d-172">먼저 보기 콘텐츠 페이지 상단에 선언된 `<%@ page %>` 지시의 제목 특성에 페이지 제목을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="1400d-173">예를 들어 페이지 제목 "Super Great Website"를 색인 보기에 할당하려면 색인 보기 맨 위에 다음 지시문을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

<span data-ttu-id="1400d-174">색인 보기가 브라우저에 렌더링되면 원하는 제목이 브라우저 제목 표시줄에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>

<span data-ttu-id="1400d-175">[![브라우저 제목 표시줄](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="1400d-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)</span></span>

<span data-ttu-id="1400d-176">제목 특성이 작동하려면 마스터 보기 페이지가 충족해야 하는 중요한 요구 사항이 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="1400d-177">뷰 마스터 페이지에는 `<head runat="server">` 헤더에 대한 `<head>` 일반 태그 대신 태그가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="1400d-178">태그에 `<head>` runat="server" 특성이 포함되지 않으면 제목이 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="1400d-179">기본 보기 마스터 페이지에는 `<head runat="server">` 필수 태그가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="1400d-180">개별 보기 콘텐츠 페이지에서 마스터 페이지 콘텐츠를 수정하는 또 다른 방법은 `<asp:ContentPlaceHolder>` 태그에서 수정할 영역을 래핑하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="1400d-181">예를 들어 제목뿐만 아니라 마스터 뷰 페이지에서 렌더링되는 메타 태그도 변경하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="1400d-182">목록 4의 마스터 보기 `<asp:ContentPlaceHolder>` 페이지에는 `<head>` 태그 내에 태그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="1400d-183">**리스팅 4 –`Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="1400d-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

<span data-ttu-id="1400d-184">목록 4의 `<asp:ContentPlaceHolder>` 태그에는 기본 제목및 기본 메타 태그와 같은 기본 콘텐츠가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="1400d-185">개별 보기 콘텐츠 페이지에서 `<asp:ContentPlaceHolder>` 이 태그를 재정의하지 않으면 기본 콘텐츠가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="1400d-186">목록 5의 `<asp:ContentPlaceHolder>` 콘텐츠 보기 페이지는 사용자 지정 제목 및 사용자 지정 메타 태그를 표시하기 위해 태그를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="1400d-187">**리스팅 5 –`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="1400d-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="1400d-188">요약</span><span class="sxs-lookup"><span data-stu-id="1400d-188">Summary</span></span>

<span data-ttu-id="1400d-189">이 자습서에서는 마스터 페이지를 보고 콘텐츠 페이지를 볼 수 있는 기본 소개를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="1400d-190">새 보기 마스터 페이지를 만들고 이를 기반으로 보기 콘텐츠 페이지를 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="1400d-191">또한 특정 보기 콘텐츠 페이지에서 보기 마스터 페이지의 내용을 수정하는 방법도 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1400d-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1400d-192">[이전](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [다음](passing-data-to-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1400d-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
[Next](passing-data-to-view-master-pages-vb.md)</span></span>
