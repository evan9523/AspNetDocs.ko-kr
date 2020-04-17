---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: AJAX 제어 툴킷(C#) | 마이크로 소프트 문서
author: rick-anderson
description: AJAX 제어 툴킷을 사용하기 위해 알아야 할 모든 것을 알아보십시오.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: b5954019ec3312f06f38012e4d3f9b1f71573f76
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543589"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="74104-103">AJAX 컨트롤 도구 키트 시작(C#)</span><span class="sxs-lookup"><span data-stu-id="74104-103">Get Started with the AJAX Control Toolkit (C#)</span></span>

<span data-ttu-id="74104-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="74104-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="74104-105">AJAX 제어 툴킷을 사용하기 위해 알아야 할 모든 것을 알아보십시오.</span><span class="sxs-lookup"><span data-stu-id="74104-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="74104-106">AJAX 제어 툴킷에는 ASP.NET 응용 프로그램에서 사용할 수 있는 30개 이상의 무료 컨트롤이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74104-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="74104-107">이 자습서에서는 AJAX 제어 도구 키트를 다운로드하고 도구 키트 컨트롤을 Visual Studio/Visual 웹 개발자 익스프레스 도구 상자에 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="74104-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="74104-108">AJAX 제어 툴킷 다운로드</span><span class="sxs-lookup"><span data-stu-id="74104-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="74104-109">[AJAX 제어 툴킷은](http://devexpress.com/act) ASP.NET 커뮤니티의 구성원과 ASP.NET 팀에 의해 개발 된 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="74104-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 

<span data-ttu-id="74104-110">[![AJAX 제어 툴킷 다운로드](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="74104-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="74104-111">**그림 01**: AJAX 제어 도구 키트 다운로드[(클릭하여 전체 크기 이미지 보기)](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="74104-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>

<span data-ttu-id="74104-112">파일을 다운로드한 후 파일 차단을 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74104-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="74104-113">파일을 마우스 오른쪽 단추로 클릭하고 속성을 선택하고 **차단 해제** 단추를 클릭합니다(그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="74104-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="74104-114">[![AJAX 제어 툴킷 ZIP 파일 차단 해제](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="74104-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="74104-115">**그림 02**: AJAX 제어 도구 키트 ZIP 파일 차단 해제[(클릭하여 전체 크기 이미지 보기)](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="74104-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>

<span data-ttu-id="74104-116">파일 차단을 해제한 후 파일의 압축을 풀 수 있습니다: 파일 마우스 오른쪽 단추를 클릭하고 **모든 메뉴 추출** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74104-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="74104-117">이제 도구 키트를 Visual Studio/Visual 웹 개발자 도구 상자에 추가할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="74104-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="74104-118">도구 상자에 AJAX 제어 도구 키트 추가</span><span class="sxs-lookup"><span data-stu-id="74104-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="74104-119">AJAX 제어 도구 키트를 사용하는 가장 쉬운 방법은 도구 키트를 Visual Studio/Visual 웹 개발자 도구 상자에 추가하는 것입니다(그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="74104-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="74104-120">이렇게 하면 도구 키트 컨트롤을 사용할 때 페이지로 드래그하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74104-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="74104-121">[![도구 상자에 AJAX 제어 도구 키트가 나타납니다.](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="74104-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="74104-122">**그림 03**: AJAX 제어 도구 키트가 도구 상자에 나타납니다[(전체 크기 이미지를 보려면 클릭하십시오)](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="74104-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>

<span data-ttu-id="74104-123">먼저 도구 상자에 AJAX 제어 도구 키트 탭을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74104-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="74104-124">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="74104-124">Follow these steps.</span></span>

1. <span data-ttu-id="74104-125">메뉴 옵션 파일을 선택하여 웹 사이트를 ASP.NET 새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74104-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="74104-126">솔루션 탐색기 창에서 Default.aspx를 두 번 클릭하여 편집기에서 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="74104-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="74104-127">일반 탭 아래에 있는 도구 상자를 마우스 오른쪽 단추로 클릭하고 **탭 추가** 옵션(그림 4 참조)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74104-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="74104-128">AJAX 제어 도구 키트라는 새 탭을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74104-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="74104-129">[![새 탭 추가](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="74104-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="74104-130">**그림 04**: 새 탭 추가[(클릭하여 전체 크기 이미지 보기)](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="74104-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>

<span data-ttu-id="74104-131">다음으로 AJAX 제어 도구 키트 컨트롤을 새 탭에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74104-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="74104-132">AJAX 제어 도구 키트 탭 아래를 마우스 오른쪽 단추로 클릭하고 메뉴 선택 **옵션(그림 5 참조)을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74104-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="74104-133">AJAX 제어 툴킷의 압축을 풀었던 위치를 찾아보고 AjaxControlToolkit.dll 어셈블리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74104-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="74104-134">[![도구 상자에 추가할 항목을 선택합니다.](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="74104-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="74104-135">**그림 05**: 도구 상자에 추가할 항목을 선택합니다(전체[크기 이미지를 보려면 클릭)](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="74104-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>

<span data-ttu-id="74104-136">이 단계를 완료하면 모든 도구 키트 컨트롤이 도구 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="74104-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="74104-137">새 버전의 툴킷으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="74104-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="74104-138">도구 키트의 이전 릴리스를 사용 하 고 지금 이후 버전으로 이동 해야 하는 경우 여기 권장된 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="74104-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="74104-139">바이너리 - 웹 사이트 빈 폴더에서 AjaxControlToolkit.dll 어셈블리의 이전 버전을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="74104-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="74104-140">도구 상자 항목 - AJAX 제어 도구 키트 탭을 삭제하고 위의 단계를 수행하여 AjaxControlToolkit.dll 어셈블리의 새 버전으로 탭을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74104-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="74104-141">다음</span><span class="sxs-lookup"><span data-stu-id="74104-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
