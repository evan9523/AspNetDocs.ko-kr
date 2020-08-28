---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: '사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 Extender 만들기 (c #) | Microsoft Docs'
author: rick-anderson
description: 사용자 지정 Extender를 사용 하면 새 클래스를 만들지 않고도 ASP.NET 컨트롤의 기능을 사용자 지정 하 고 확장할 수 있습니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 2522f22c80ebd34cd5adbb0ada51fd7755029426
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044677"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a><span data-ttu-id="1ba26-103">사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 Extender 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="1ba26-103">Creating a Custom AJAX Control Toolkit Control Extender (C#)</span></span>

<span data-ttu-id="1ba26-104">[Microsoft](https://github.com/microsoft) 에서</span><span class="sxs-lookup"><span data-stu-id="1ba26-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1ba26-105">사용자 지정 Extender를 사용 하면 새 클래스를 만들지 않고도 ASP.NET 컨트롤의 기능을 사용자 지정 하 고 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>

<span data-ttu-id="1ba26-106">이 자습서에서는 사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 extender를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="1ba26-107">텍스트 상자에 텍스트를 입력 하는 경우 단추의 상태를 사용 안 함에서 사용으로 변경 하는 간단 하 고 유용한 새 extender를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="1ba26-108">이 자습서를 읽은 후에는 사용자 고유의 컨트롤 extender로 ASP.NET AJAX Toolkit를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="1ba26-109">Visual Studio 또는 Visual Web Developer를 사용 하 여 사용자 지정 컨트롤 extender를 만들 수 있습니다 (최신 버전의 Visual Web Developer가 있는지 확인).</span><span class="sxs-lookup"><span data-stu-id="1ba26-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="1ba26-110">DisabledButton Extender의 개요</span><span class="sxs-lookup"><span data-stu-id="1ba26-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="1ba26-111">새 컨트롤 extender의 이름은 DisabledButton extender로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="1ba26-112">이 extender에는 다음과 같은 세 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-112">This extender will have three properties:</span></span>

- <span data-ttu-id="1ba26-113">TargetControlID-컨트롤이 확장 하는 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="1ba26-114">TargetButtonIID-사용 하지 않거나 사용 하도록 설정 된 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="1ba26-115">DisabledText-처음에 단추에 표시 되는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="1ba26-116">입력을 시작 하면 단추 텍스트 속성의 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="1ba26-117">DisabledButton extender를 TextBox 및 Button 컨트롤에 후크 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="1ba26-118">텍스트를 입력 하기 전에 단추가 비활성화 되 고 텍스트 상자와 단추가 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

<span data-ttu-id="1ba26-119">([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1ba26-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))</span></span>

<span data-ttu-id="1ba26-120">텍스트 입력을 시작한 후 단추가 활성화 되 고 텍스트 상자와 단추가 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

<span data-ttu-id="1ba26-121">([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="1ba26-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))</span></span>

<span data-ttu-id="1ba26-122">컨트롤 extender를 만들려면 다음 세 개의 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="1ba26-123">DisabledButtonExtender.cs-이 파일은 extender 만들기를 관리 하 고 디자인 타임에 속성을 설정 하는 데 사용할 수 있는 서버측 컨트롤 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-123">DisabledButtonExtender.cs - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="1ba26-124">또한 extender에서 설정할 수 있는 속성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="1ba26-125">이러한 속성은 코드와 디자인 타임에 액세스할 수 있으며 DisableButtonBehavior.js 파일에 정의 된 속성과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="1ba26-126">DisabledButtonBehavior.js--이 파일을 통해 모든 클라이언트 스크립트 논리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="1ba26-127">DisabledButtonDesigner.cs-이 클래스는 디자인 타임 기능을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-127">DisabledButtonDesigner.cs - This class enables design-time functionality.</span></span> <span data-ttu-id="1ba26-128">Visual Studio/Visual Web Developer Designer에서 컨트롤 extender가 제대로 작동 하도록 하려면이 클래스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="1ba26-129">따라서 컨트롤 extender는 서버측 컨트롤, 클라이언트 쪽 동작 및 서버 쪽 디자이너 클래스로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="1ba26-130">다음 섹션에서 이러한 세 파일을 모두 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="1ba26-131">사용자 지정 Extender 웹 사이트 및 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="1ba26-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="1ba26-132">첫 번째 단계는 Visual Studio/Visual Web Developer에서 클래스 라이브러리 프로젝트 및 웹 사이트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="1ba26-133">클래스 라이브러리 프로젝트에서 사용자 지정 extender를 만들고 웹 사이트에서 사용자 지정 extender를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-133">We'll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="1ba26-134">웹 사이트부터 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-134">Let's start with the website.</span></span> <span data-ttu-id="1ba26-135">웹 사이트를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="1ba26-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="1ba26-136">메뉴 옵션 **파일, 새 웹 사이트를**선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="1ba26-137">**ASP.NET 웹 사이트** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="1ba26-138">새 웹 사이트의 이름을 *Website1*로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="1ba26-139">**확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-139">Click the **OK** button.</span></span>

<span data-ttu-id="1ba26-140">다음으로, 컨트롤 extender에 대 한 코드를 포함 하는 클래스 라이브러리 프로젝트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="1ba26-141">메뉴 옵션 **파일, 추가, 새 프로젝트**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="1ba26-142">**클래스 라이브러리** 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="1ba26-143">이름이 **Customextenders**인 새 클래스 라이브러리의 이름을로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="1ba26-144">**확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-144">Click the **OK** button.</span></span>

<span data-ttu-id="1ba26-145">이러한 단계를 완료 한 후 솔루션 탐색기 창은 그림 1과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>

<span data-ttu-id="1ba26-146">[![웹 사이트 및 클래스 라이브러리 프로젝트를 사용 하는 솔루션](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="1ba26-146">[![Solution with website and class library project](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)</span></span>

<span data-ttu-id="1ba26-147">**그림 01**: 웹 사이트 및 클래스 라이브러리 프로젝트를 사용 하는 솔루션 ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="1ba26-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))</span></span>

<span data-ttu-id="1ba26-148">다음으로 클래스 라이브러리 프로젝트에 필요한 모든 어셈블리 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="1ba26-149">CustomExtenders 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **참조 추가**를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="1ba26-150">.NET 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="1ba26-151">다음 어셈블리에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="1ba26-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="1ba26-152">System.Web.dll</span></span>
    2. <span data-ttu-id="1ba26-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="1ba26-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="1ba26-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="1ba26-154">System.Design.dll</span></span>
    4. <span data-ttu-id="1ba26-155">System.Web.Extensions.Design.dll</span><span class="sxs-lookup"><span data-stu-id="1ba26-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="1ba26-156">찾아보기 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="1ba26-157">AjaxControlToolkit.dll 어셈블리에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="1ba26-158">이 어셈블리는 AJAX 컨트롤 도구 키트를 다운로드 한 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="1ba26-159">이러한 단계를 완료 한 후에는 클래스 라이브러리 프로젝트 참조 폴더는 그림 2와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-159">After you complete these steps, your class library project References folder should look like Figure 2.</span></span>

<span data-ttu-id="1ba26-160">[![필요한 참조가 있는 폴더 참조](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="1ba26-160">[![References folder with required references](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)</span></span>

<span data-ttu-id="1ba26-161">**그림 02**: 필요한 참조가 있는 폴더 참조 ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="1ba26-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))</span></span>

## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="1ba26-162">사용자 지정 컨트롤 Extender 만들기</span><span class="sxs-lookup"><span data-stu-id="1ba26-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="1ba26-163">이제 클래스 라이브러리를 만들었으므로 extender 컨트롤 빌드를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="1ba26-164">사용자 지정 extender 컨트롤 클래스의 완전 한 뼈부터 살펴보겠습니다 (목록 1 참조).</span><span class="sxs-lookup"><span data-stu-id="1ba26-164">Let's start with the bare bones of a custom extender control class (see Listing 1).</span></span>

<span data-ttu-id="1ba26-165">**목록 1-MyCustomExtender.cs**</span><span class="sxs-lookup"><span data-stu-id="1ba26-165">**Listing 1 - MyCustomExtender.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

<span data-ttu-id="1ba26-166">목록 1에서 컨트롤 extender 클래스에 대 한 몇 가지 사항을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="1ba26-167">먼저 클래스가 기본 ExtenderControlBase 클래스에서 상속 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="1ba26-168">모든 AJAX Control Toolkit extender 컨트롤은이 기본 클래스에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="1ba26-169">예를 들어 기본 클래스는 모든 컨트롤 extender의 필수 속성인 TargetID 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="1ba26-170">다음으로 클래스에는 클라이언트 스크립트와 관련 된 다음 두 가지 특성이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="1ba26-171">Webresource.axd-파일이 어셈블리에 포함 리소스로 포함 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="1ba26-172">ClientScriptResource-어셈블리에서 스크립트 리소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="1ba26-173">Webresource.axd 특성은 사용자 지정 extender가 컴파일될 때 어셈블리에 MyControlBehavior.js JavaScript 파일을 포함 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="1ba26-174">ClientScriptResource 특성은 웹 페이지에서 사용자 지정 extender를 사용할 때 어셈블리에서 MyControlBehavior.js 스크립트를 검색 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>

<span data-ttu-id="1ba26-175">Webresource.axd 및 ClientScriptResource 특성이 작동 하려면 JavaScript 파일을 포함 리소스로 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="1ba26-176">솔루션 탐색기 창에서 파일을 선택 하 고 속성 시트를 연 후에 *포함 된 리소스* 값을 **빌드 작업** 속성에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>

<span data-ttu-id="1ba26-177">컨트롤 extender에는 TargetControlType 특성도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="1ba26-178">이 특성은 컨트롤 extender에 의해 확장 되는 컨트롤의 형식을 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="1ba26-179">목록 1의 경우 컨트롤 extender를 사용 하 여 텍스트 상자를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="1ba26-180">마지막으로, 사용자 지정 extender에 이름이 T.myproperty 인 속성이 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="1ba26-181">속성은 ExtenderControlProperty 특성으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="1ba26-182">GetPropertyValue () 및 SetPropertyValue () 메서드는 서버측 컨트롤 extender의 속성 값을 클라이언트 쪽 동작으로 전달 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="1ba26-183">계속 해 서 DisabledButton extender에 대 한 코드를 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-183">Let's go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="1ba26-184">이 extender에 대 한 코드는 목록 2에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-184">The code for this extender can be found in Listing 2.</span></span>

<span data-ttu-id="1ba26-185">**목록 2-DisabledButtonExtender.cs**</span><span class="sxs-lookup"><span data-stu-id="1ba26-185">**Listing 2 - DisabledButtonExtender.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

<span data-ttu-id="1ba26-186">목록 2의 DisabledButton extender에는 TargetButtonID 및 DisabledText 라는 두 개의 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="1ba26-187">TargetButtonID 속성에 적용 된 IDReferenceProperty는 단추 컨트롤의 ID 이외의 항목을이 속성에 할당 하는 것을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="1ba26-188">Webresource.axd 및 ClientScriptResource 특성은 DisabledButtonBehavior.js 라는 파일에 있는 클라이언트측 동작을이 extender와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="1ba26-189">이 JavaScript 파일에 대해서는 다음 섹션에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="1ba26-190">사용자 지정 Extender 동작 만들기</span><span class="sxs-lookup"><span data-stu-id="1ba26-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="1ba26-191">컨트롤 extender의 클라이언트 쪽 구성 요소를 동작 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="1ba26-192">단추를 사용 하지 않도록 설정 하 고 설정 하는 실제 논리는 DisabledButton 동작에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="1ba26-193">동작에 대 한 JavaScript 코드는 목록 3에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

<span data-ttu-id="1ba26-194">**목록 3-DisabledButton.js**</span><span class="sxs-lookup"><span data-stu-id="1ba26-194">**Listing 3 - DisabledButton.js**</span></span>

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

<span data-ttu-id="1ba26-195">목록 3의 JavaScript 파일에는 이름이 DisabledButtonBehavior 인 클라이언트 쪽 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="1ba26-196">TargetButtonID 및 DisabledText 라는 두 개의 속성을 포함 하는이 클래스에는 get TargetButtonID/set TargetButtonID를 사용 하 여 액세스할 수 있으며 \_ \_ get \_ DisabledText/set DisabledText \_ 를 사용 하 여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="1ba26-197">Initialize () 메서드는 keyup 이벤트 처리기를 동작의 대상 요소와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="1ba26-198">이 동작과 연결 된 텍스트 상자에 문자를 입력할 때마다 keyup 처리기가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="1ba26-199">Keyup 처리기는 동작과 연결 된 텍스트 상자에 텍스트가 포함 되어 있는지 여부에 따라 단추를 사용 하거나 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="1ba26-200">목록 3에서 JavaScript 파일을 포함 리소스로 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="1ba26-201">솔루션 탐색기 창에서 파일을 선택 하 고 속성 시트를 연 후에 *포함 된 리소스* 값을 **빌드 작업** 속성에 할당 합니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="1ba26-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="1ba26-202">이 옵션은 Visual Studio 및 Visual Web Developer에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>

<span data-ttu-id="1ba26-203">[![JavaScript 파일을 포함 리소스로 추가](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="1ba26-203">[![Adding a JavaScript file as an embedded resource](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)</span></span>

<span data-ttu-id="1ba26-204">**그림 03**: JavaScript 파일을 포함 리소스로 추가 ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="1ba26-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))</span></span>

## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="1ba26-205">사용자 지정 Extender 디자이너 만들기</span><span class="sxs-lookup"><span data-stu-id="1ba26-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="1ba26-206">Extender를 완료 하기 위해 만들어야 하는 마지막 클래스가 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="1ba26-207">목록 4에서 designer 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="1ba26-208">이 클래스는 Visual Studio/Visual Web Developer Designer에서 extender가 제대로 작동 하도록 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="1ba26-209">**목록 4-DisabledButtonDesigner.cs**</span><span class="sxs-lookup"><span data-stu-id="1ba26-209">**Listing 4 - DisabledButtonDesigner.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

<span data-ttu-id="1ba26-210">목록 4의 디자이너를 Designer 특성을 사용 하 여 DisabledButton extender와 연결 합니다. 다음과 같이 Designer 특성을 DisabledButtonExtender 클래스에 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="1ba26-211">사용자 지정 Extender 사용</span><span class="sxs-lookup"><span data-stu-id="1ba26-211">Using the Custom Extender</span></span>

<span data-ttu-id="1ba26-212">이제 DisabledButton 컨트롤 extender 만들기를 완료 했으므로 ASP.NET 웹 사이트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="1ba26-213">먼저 도구 상자에 사용자 지정 extender를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="1ba26-214">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-214">Follow these steps:</span></span>

1. <span data-ttu-id="1ba26-215">솔루션 탐색기 창에서 페이지를 두 번 클릭 하 여 ASP.NET 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="1ba26-216">도구 상자를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **항목 선택**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="1ba26-217">도구 상자 항목 선택 대화 상자에서 CustomExtenders.dll 어셈블리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="1ba26-218">**확인** 단추를 클릭 하 여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="1ba26-219">이러한 단계를 완료 한 후에는 DisabledButton 컨트롤 extender가 도구 상자에 표시 됩니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="1ba26-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>

<span data-ttu-id="1ba26-220">[![도구 상자의 DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="1ba26-220">[![DisabledButton in the toolbox](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)</span></span>

<span data-ttu-id="1ba26-221">**그림 04**: 도구 상자에 DisabledButton ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="1ba26-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))</span></span>

<span data-ttu-id="1ba26-222">다음으로 새 ASP.NET 페이지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="1ba26-223">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-223">Follow these steps:</span></span>

1. <span data-ttu-id="1ba26-224">ShowDisabledButton 라는 새 ASP.NET 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="1ba26-225">ScriptManager를 페이지로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="1ba26-226">TextBox 컨트롤을 페이지로 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="1ba26-227">단추 컨트롤을 페이지로 끌어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="1ba26-228">속성 창에서 단추 ID 속성을 <em>btnSave</em> 값으로 변경 하 고 Text 속성을 \*Save \* \*값으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>

<span data-ttu-id="1ba26-229">표준 ASP.NET 텍스트 상자 및 단추 컨트롤을 사용 하 여 페이지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="1ba26-230">다음으로, DisabledButton extender를 사용 하 여 TextBox 컨트롤을 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="1ba26-231">Extender 작업 **추가** 옵션을 선택 하 여 extender 마법사 대화 상자를 엽니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="1ba26-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="1ba26-232">대화 상자에 사용자 지정 DisabledButton extender가 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="1ba26-233">DisabledButton extender를 선택 하 고 **확인** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-233">Select the DisabledButton extender and click the **OK** button.</span></span>

<span data-ttu-id="1ba26-234">[![Extender 마법사 대화 상자](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="1ba26-234">[![The Extender Wizard dialog](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)</span></span>

<span data-ttu-id="1ba26-235">**그림 05**: Extender 마법사 대화 상자 ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="1ba26-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))</span></span>

<span data-ttu-id="1ba26-236">마지막으로 DisabledButton extender의 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="1ba26-237">TextBox 컨트롤의 속성을 수정 하 여 DisabledButton extender의 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="1ba26-238">디자이너에서 텍스트 상자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="1ba26-239">속성 창에서 Extender 노드를 확장 합니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="1ba26-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="1ba26-240">DisabledText 속성에 *Save* 값을 할당 하 고 TargetButtonID 속성에 *btnSave* 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>

<span data-ttu-id="1ba26-241">[![Extender 속성 설정](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="1ba26-241">[![Setting extender properties](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)</span></span>

<span data-ttu-id="1ba26-242">**그림 06**: extender 속성 설정 ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="1ba26-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))</span></span>

<span data-ttu-id="1ba26-243">F5 키를 눌러 페이지를 실행 하면 단추 컨트롤이 처음에 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="1ba26-244">텍스트 상자에 텍스트를 입력 하는 즉시 단추 컨트롤이 사용 됩니다 (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="1ba26-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>

<span data-ttu-id="1ba26-245">[![DisabledButton extender의 동작](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="1ba26-245">[![The DisabledButton extender in action](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)</span></span>

<span data-ttu-id="1ba26-246">**그림 07**: 실행 중인 DisabledButton extender ([전체 크기 이미지를 보려면 클릭](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="1ba26-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))</span></span>

## <a name="summary"></a><span data-ttu-id="1ba26-247">요약</span><span class="sxs-lookup"><span data-stu-id="1ba26-247">Summary</span></span>

<span data-ttu-id="1ba26-248">이 자습서의 목표는 사용자 지정 extender 컨트롤을 사용 하 여 AJAX 컨트롤 도구 키트를 확장 하는 방법을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="1ba26-249">이 자습서에서는 간단한 DisabledButton 컨트롤 extender를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="1ba26-250">DisabledButtonExtender 클래스, DisabledButtonBehavior JavaScript 동작 및 DisabledButtonDesigner 클래스를 만들어이 extender를 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="1ba26-251">사용자 지정 컨트롤 extender를 만들 때마다 비슷한 단계 집합을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1ba26-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1ba26-252">[이전](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [다음](get-started-with-the-ajax-control-toolkit-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1ba26-252">[Previous](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
[Next](get-started-with-the-ajax-control-toolkit-vb.md)</span></span>
