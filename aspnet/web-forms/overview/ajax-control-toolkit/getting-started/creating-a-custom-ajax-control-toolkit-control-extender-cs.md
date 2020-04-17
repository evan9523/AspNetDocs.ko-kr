---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: 사용자 지정 AJAX 제어 툴킷 제어 익스텐더 만들기(C#) | 마이크로 소프트 문서
author: rick-anderson
description: 사용자 지정 Extenders를 사용하면 새 클래스를 만들지 않고도 ASP.NET 컨트롤의 기능을 사용자 지정하고 확장할 수 있습니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ac7bf71227459ab4b1e87489e1faab6dc41545b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543030"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a><span data-ttu-id="86982-103">사용자 지정 AJAX 컨트롤 도구 키트 컨트롤 Extender 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="86982-103">Creating a Custom AJAX Control Toolkit Control Extender (C#)</span></span>

<span data-ttu-id="86982-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="86982-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="86982-105">사용자 지정 Extenders를 사용하면 새 클래스를 만들지 않고도 ASP.NET 컨트롤의 기능을 사용자 지정하고 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-105">Custom Extenders enable you to customize and extend the capabilities of ASP.NET controls without having to create new classes.</span></span>

<span data-ttu-id="86982-106">이 자습서에서는 사용자 지정 AJAX 제어 도구 키트 컨트롤 익스텐더를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="86982-106">In this tutorial, you learn how to create a custom AJAX Control Toolkit control extender.</span></span> <span data-ttu-id="86982-107">텍스트 상자에 텍스트를 입력할 때 단추의 상태를 사용 하지 않는 것에서 활성화로 변경 하는 간단 하지만 유용한 새 extender를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86982-107">We create a simple, but useful, new extender that changes the state of a Button from disabled to enabled when you type text into a TextBox.</span></span> <span data-ttu-id="86982-108">이 자습서를 읽은 후, 당신은 당신의 자신의 컨트롤 익스텐더와 ASP.NET AJAX 툴킷을 확장 할 수있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="86982-108">After reading this tutorial, you will be able to extend the ASP.NET AJAX Toolkit with your own control extenders.</span></span>

<span data-ttu-id="86982-109">Visual Studio 또는 Visual 웹 개발자를 사용하여 사용자 지정 컨트롤 익스텐더를 만들 수 있습니다(최신 버전의 Visual Web Developer이 있는지 확인).</span><span class="sxs-lookup"><span data-stu-id="86982-109">You can create custom control extenders using either Visual Studio or Visual Web Developer (make sure that you have the latest version of Visual Web Developer).</span></span>

## <a name="overview-of-the-disabledbutton-extender"></a><span data-ttu-id="86982-110">사용 안 함 단추 익스텐더의 개요</span><span class="sxs-lookup"><span data-stu-id="86982-110">Overview of the DisabledButton Extender</span></span>

<span data-ttu-id="86982-111">우리의 새로운 컨트롤 익스텐더는 DisabledButton 익스텐더라는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="86982-111">Our new control extender is named the DisabledButton extender.</span></span> <span data-ttu-id="86982-112">이 익스텐더에는 세 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-112">This extender will have three properties:</span></span>

- <span data-ttu-id="86982-113">TargetControlID - 컨트롤이 확장되는 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="86982-113">TargetControlID - The TextBox that the control extends.</span></span>
- <span data-ttu-id="86982-114">TargetButtonIID - 비활성화되어 있거나 활성화된 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="86982-114">TargetButtonIID - The Button that is disabled or enabled.</span></span>
- <span data-ttu-id="86982-115">비활성화텍스트 - 처음에 버튼에 표시되는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="86982-115">DisabledText - The text that is initially displayed in the Button.</span></span> <span data-ttu-id="86982-116">입력을 시작하면 Button 텍스트 속성의 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-116">When you start typing, the Button displays the value of the Button Text property.</span></span>

<span data-ttu-id="86982-117">비활성화 단추 확장기를 텍스트 상자 및 단추 컨트롤에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-117">You hook the DisabledButton extender to a TextBox and Button control.</span></span> <span data-ttu-id="86982-118">텍스트를 입력하기 전에 단추를 사용하지 않도록 설정하면 텍스트 상자 와 버튼이 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-118">Before you type any text, the Button is disabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

<span data-ttu-id="86982-119">(전체[크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="86982-119">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))</span></span>

<span data-ttu-id="86982-120">텍스트 입력을 시작하면 Button이 활성화되고 텍스트 상자 및 단추는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-120">After you start typing text, the Button is enabled and the TextBox and Button look like this:</span></span>

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

<span data-ttu-id="86982-121">(전체[크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="86982-121">([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))</span></span>

<span data-ttu-id="86982-122">컨트롤 익스텐더를 만들려면 다음 세 개의 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-122">To create our control extender, we need to create the following three files:</span></span>

- <span data-ttu-id="86982-123">DisabledButtonExtender.cs - 이 파일은 익스텐더 만들기를 관리하고 디자인 타임에 속성을 설정할 수 있는 서버 측 제어 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="86982-123">DisabledButtonExtender.cs - This file is the server-side control class that will manage creating your extender and allow you to set the properties at design-time.</span></span> <span data-ttu-id="86982-124">또한 익스텐더에서 설정할 수 있는 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-124">It also defines the properties that can be set on your extender.</span></span> <span data-ttu-id="86982-125">이러한 속성은 코드 및 디자인 타임에 액세스할 수 있으며 DisableButtonBehavior.js 파일에 정의된 속성을 일치시입니다.</span><span class="sxs-lookup"><span data-stu-id="86982-125">These properties are accessible via code and at design time and match properties defined in the DisableButtonBehavior.js file.</span></span>
- <span data-ttu-id="86982-126">DisabledButtonBehavior.js -- 이 파일은 모든 클라이언트 스크립트 논리를 추가하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="86982-126">DisabledButtonBehavior.js -- This file is where you will add all of your client script logic.</span></span>
- <span data-ttu-id="86982-127">DisabledButtonDesigner.cs - 이 클래스는 디자인 타임 기능을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-127">DisabledButtonDesigner.cs - This class enables design-time functionality.</span></span> <span data-ttu-id="86982-128">컨트롤 익스텐더가 Visual Studio/Visual 웹 개발자 디자이너에서 올바르게 작동하려면 이 클래스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-128">You need this class if you want the control extender to work correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="86982-129">따라서 컨트롤 익스텐더는 서버 측 컨트롤, 클라이언트 측 동작 및 서버 측 디자이너 클래스로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-129">So a control extender consists of a server-side control, a client-side behavior, and a server-side designer class.</span></span> <span data-ttu-id="86982-130">다음 섹션에서 이러한 세 파일을 모두 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="86982-130">You learn how to create all three of these files in the following sections.</span></span>

## <a name="creating-the-custom-extender-website-and-project"></a><span data-ttu-id="86982-131">사용자 지정 익스텐더 웹 사이트 및 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="86982-131">Creating the Custom Extender Website and Project</span></span>

<span data-ttu-id="86982-132">첫 번째 단계는 Visual Studio/Visual 웹 개발자에서 클래스 라이브러리 프로젝트 및 웹 사이트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="86982-132">The first step is to create a class library project and website in Visual Studio/Visual Web Developer.</span></span> <span data-ttu-id="86982-133">클래스 라이브러리 프로젝트에서 사용자 지정 익스텐더를 만들고 웹 사이트에서 사용자 지정 익스텐더를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-133">We�ll create the custom extender in the class library project and test the custom extender in the website.</span></span>

<span data-ttu-id="86982-134">웹 사이트로 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-134">Let�s start with the website.</span></span> <span data-ttu-id="86982-135">다음 단계에 따라 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86982-135">Follow these steps to create the website:</span></span>

1. <span data-ttu-id="86982-136">메뉴 옵션 **파일, 새 웹 사이트를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-136">Select the menu option **File, New Web Site**.</span></span>
2. <span data-ttu-id="86982-137">ASP.NET **웹 사이트** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-137">Select the **ASP.NET Web Site** template.</span></span>
3. <span data-ttu-id="86982-138">새 웹 사이트 웹 *사이트 이름1*.</span><span class="sxs-lookup"><span data-stu-id="86982-138">Name the new website *Website1*.</span></span>
4. <span data-ttu-id="86982-139">**확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-139">Click the **OK** button.</span></span>

<span data-ttu-id="86982-140">다음으로 컨트롤 익스텐더에 대한 코드를 포함하는 클래스 라이브러리 프로젝트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-140">Next, we need to create the class library project that will contain the code for the control extender:</span></span>

1. <span data-ttu-id="86982-141">메뉴 옵션 **파일, 추가, 새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-141">Select the menu option **File, Add, New Project**.</span></span>
2. <span data-ttu-id="86982-142">클래스 **라이브러리** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-142">Select the **Class Library** template.</span></span>
3. <span data-ttu-id="86982-143">사용자 지정 Extenders 라는 이름으로 새 클래스 라이브러리의 이름을 **지정합니다.**</span><span class="sxs-lookup"><span data-stu-id="86982-143">Name the new class library with the name **CustomExtenders**.</span></span>
4. <span data-ttu-id="86982-144">**확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-144">Click the **OK** button.</span></span>

<span data-ttu-id="86982-145">이 단계를 완료하면 솔루션 탐색기 창이 그림 1과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-145">After you complete these steps, your Solution Explorer window should look like Figure 1.</span></span>

<span data-ttu-id="86982-146">[![웹 사이트 및 클래스 라이브러리 프로젝트와 솔루션](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="86982-146">[![Solution with website and class library project](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)</span></span>

<span data-ttu-id="86982-147">**그림 01**: 웹 사이트 및 클래스 라이브러리 프로젝트가 있는 솔루션[(전체 크기 이미지를 보려면 클릭하십시오)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="86982-147">**Figure 01**: Solution with website and class library project([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))</span></span>

<span data-ttu-id="86982-148">다음으로 클래스 라이브러리 프로젝트에 필요한 모든 어셈블리 참조를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-148">Next, you need to add all of the necessary assembly references to the class library project:</span></span>

1. <span data-ttu-id="86982-149">사용자 지정 확장자 프로젝트를 마우스 오른쪽 단추로 클릭하고 **참조 추가**옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-149">Right-click the CustomExtenders project and select the menu option **Add Reference**.</span></span>
2. <span data-ttu-id="86982-150">.NET 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-150">Select the .NET tab.</span></span>
3. <span data-ttu-id="86982-151">다음 어셈블리에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-151">Add references to the following assemblies:</span></span>

    1. <span data-ttu-id="86982-152">System.Web.dll</span><span class="sxs-lookup"><span data-stu-id="86982-152">System.Web.dll</span></span>
    2. <span data-ttu-id="86982-153">System.Web.Extensions.dll</span><span class="sxs-lookup"><span data-stu-id="86982-153">System.Web.Extensions.dll</span></span>
    3. <span data-ttu-id="86982-154">System.Design.dll</span><span class="sxs-lookup"><span data-stu-id="86982-154">System.Design.dll</span></span>
    4. <span data-ttu-id="86982-155">시스템.웹.확장.Design.dll</span><span class="sxs-lookup"><span data-stu-id="86982-155">System.Web.Extensions.Design.dll</span></span>
4. <span data-ttu-id="86982-156">찾아보기 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-156">Select the Browse tab.</span></span>
5. <span data-ttu-id="86982-157">AjaxControlToolkit.dll 어셈블리에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-157">Add a reference to the AjaxControlToolkit.dll assembly.</span></span> <span data-ttu-id="86982-158">이 어셈블리는 AJAX 제어 도구 키트를 다운로드한 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-158">This assembly is located in the folder where you downloaded the AJAX Control Toolkit.</span></span>

<span data-ttu-id="86982-159">이 단계를 완료하면 클래스 라이브러리 프로젝트 참조 폴더가 그림 2와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-159">After you complete these steps, your class library project References folder should look like Figure 2.</span></span>

<span data-ttu-id="86982-160">[![필수 참조가 있는 참조 폴더](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="86982-160">[![References folder with required references](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)</span></span>

<span data-ttu-id="86982-161">**그림 02**: 필요한 참조가 있는 참조[폴더(전체 크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="86982-161">**Figure 02**: References folder with required references([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))</span></span>

## <a name="creating-the-custom-control-extender"></a><span data-ttu-id="86982-162">사용자 지정 제어 익스텐더 만들기</span><span class="sxs-lookup"><span data-stu-id="86982-162">Creating the Custom Control Extender</span></span>

<span data-ttu-id="86982-163">이제 클래스 라이브러리를 통해 익스텐더 컨트롤을 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-163">Now that we have our class library, we can start building our extender control.</span></span> <span data-ttu-id="86982-164">사용자 지정 익스텐더 컨트롤 클래스의 베어 골격부터 시작하겠습니다(목록 1 참조).</span><span class="sxs-lookup"><span data-stu-id="86982-164">Let�s start with the bare bones of a custom extender control class (see Listing 1).</span></span>

<span data-ttu-id="86982-165">**리스팅 1 - MyCustomExtender.cs**</span><span class="sxs-lookup"><span data-stu-id="86982-165">**Listing 1 - MyCustomExtender.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

<span data-ttu-id="86982-166">목록 1의 컨트롤 익스텐더 클래스에 대해 알 수 있는 몇 가지 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-166">There are several things that you notice about the control extender class in Listing 1.</span></span> <span data-ttu-id="86982-167">먼저 클래스가 기본 ExtenderControlBase 클래스에서 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-167">First, notice that the class inherits from the base ExtenderControlBase class.</span></span> <span data-ttu-id="86982-168">모든 AJAX 제어 툴킷 익스텐더 컨트롤은 이 기본 클래스에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-168">All AJAX Control Toolkit extender controls derive from this base class.</span></span> <span data-ttu-id="86982-169">예를 들어 기본 클래스에는 모든 컨트롤 익스텐더의 필수 속성인 TargetID 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-169">For example, the base class includes the TargetID property that is a required property of every control extender.</span></span>

<span data-ttu-id="86982-170">다음으로 클래스에는 클라이언트 스크립트와 관련된 다음 두 가지 특성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-170">Next, notice that the class includes the following two attributes related to client script:</span></span>

- <span data-ttu-id="86982-171">WebResource - 파일을 어셈블리에 포함된 리소스로 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="86982-171">WebResource - Causes a file to be included as an embedded resource in an assembly.</span></span>
- <span data-ttu-id="86982-172">ClientScriptResource - 스크립트 리소스를 어셈블리에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-172">ClientScriptResource - Causes a script resource to be retrieved from an assembly.</span></span>

<span data-ttu-id="86982-173">WebResource 특성은 사용자 지정 익스텐더가 컴파일될 때 MyControlBehavior.js 자바스크립트 파일을 어셈블리에 포함하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-173">The WebResource attribute is used to embed the MyControlBehavior.js JavaScript file into the assembly when the custom extender is compiled.</span></span> <span data-ttu-id="86982-174">ClientScriptResource 특성은 사용자 지정 익스텐더가 웹 페이지에서 사용될 때 어셈블리에서 MyControlBehavior.js 스크립트를 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-174">The ClientScriptResource attribute is used to retrieve the MyControlBehavior.js script from the assembly when the custom extender is used in a web page.</span></span>

<span data-ttu-id="86982-175">WebResource 및 ClientScriptResource 특성이 작동하려면 JavaScript 파일을 포함된 리소스로 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-175">In order for the WebResource and ClientScriptResource attributes to work, you must compile the JavaScript file as an embedded resource.</span></span> <span data-ttu-id="86982-176">솔루션 탐색기 창에서 파일을 선택하고 속성 시트를 열고 *빌드* **작업** 속성에 포함된 리소스 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-176">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property.</span></span>

<span data-ttu-id="86982-177">컨트롤 익스텐더에는 TargetControlType 특성도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-177">Notice that the control extender also includes a TargetControlType attribute.</span></span> <span data-ttu-id="86982-178">이 특성은 컨트롤 익스텐더에서 확장되는 컨트롤 유형을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-178">This attribute is used to specify the type of control that is extended by the control extender.</span></span> <span data-ttu-id="86982-179">목록 1의 경우 컨트롤 익스텐더가 TextBox를 확장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-179">In the case of Listing 1, the control extender is used to extend a TextBox.</span></span>

<span data-ttu-id="86982-180">마지막으로 사용자 지정 익스텐더에 MyProperty라는 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-180">Finally, notice that the custom extender includes a property named MyProperty.</span></span> <span data-ttu-id="86982-181">속성은 ExtenderControlProperty 특성으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-181">The property is marked with the ExtenderControlProperty attribute.</span></span> <span data-ttu-id="86982-182">GetPropertyValue() 및 SetPropertyValue() 메서드는 서버 측 컨트롤 익스텐더에서 클라이언트 측 동작으로 속성 값을 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-182">The GetPropertyValue() and SetPropertyValue() methods are used to pass the property value from the server-side control extender to the client-side behavior.</span></span>

<span data-ttu-id="86982-183">의 가서 우리의 DisabledButton 익스텐더에 대한 코드를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-183">Let�s go ahead and implement the code for our DisabledButton extender.</span></span> <span data-ttu-id="86982-184">이 익스텐더에 대한 코드는 목록 2에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-184">The code for this extender can be found in Listing 2.</span></span>

<span data-ttu-id="86982-185">**리스팅 2 - DisabledButtonExtender.cs**</span><span class="sxs-lookup"><span data-stu-id="86982-185">**Listing 2 - DisabledButtonExtender.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

<span data-ttu-id="86982-186">목록 2의 비활성화 된 Button 익스텐더에는 TargetButtonID 및 DisabledText라는 두 개의 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-186">The DisabledButton extender in Listing 2 has two properties named TargetButtonID and DisabledText.</span></span> <span data-ttu-id="86982-187">TargetButtonID 속성에 적용된 IDReferenceProperty는 Button 컨트롤의 ID 이외의 다른 것을 이 속성에 할당하지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-187">The IDReferenceProperty applied to the TargetButtonID property prevents you from assigning anything other than the ID of a Button control to this property.</span></span>

<span data-ttu-id="86982-188">WebResource 및 ClientScriptResource 특성은 이 확장기와 DisabledButtonBehavior.js라는 파일에 있는 클라이언트 측 동작을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-188">The WebResource and ClientScriptResource attributes associate a client-side behavior located in a file named DisabledButtonBehavior.js with this extender.</span></span> <span data-ttu-id="86982-189">다음 섹션에서이 자바 스크립트 파일에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-189">We discuss this JavaScript file in the next section.</span></span>

## <a name="creating-the-custom-extender-behavior"></a><span data-ttu-id="86982-190">사용자 지정 확장기 동작 만들기</span><span class="sxs-lookup"><span data-stu-id="86982-190">Creating the Custom Extender Behavior</span></span>

<span data-ttu-id="86982-191">컨트롤 익스텐더의 클라이언트 쪽 구성 요소를 동작이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-191">The client-side component of a control extender is called a behavior.</span></span> <span data-ttu-id="86982-192">단추를 사용하지 않도록 설정 및 활성화하기 위한 실제 논리는 DisabledButton 동작에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-192">The actual logic for disabling and enabling the Button is contained in the DisabledButton behavior.</span></span> <span data-ttu-id="86982-193">동작에 대한 자바스크립트 코드는 목록 3에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-193">The JavaScript code for the behavior is included in Listing 3.</span></span>

<span data-ttu-id="86982-194">**목록 3 - 비활성화된 Button.js**</span><span class="sxs-lookup"><span data-stu-id="86982-194">**Listing 3 - DisabledButton.js**</span></span>

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

<span data-ttu-id="86982-195">목록 3의 자바 스크립트 파일에는 비활성화 된 ButtonBehavior라는 클라이언트 측 클래스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-195">The JavaScript file in Listing 3 contains a client-side class named DisabledButtonBehavior.</span></span> <span data-ttu-id="86982-196">이 클래스는 서버 측 트윈과 마찬가지로 TargetButtonID 및 DisabledText라는 두\_개의 속성을 포함하며 TargetButtonID/set TargetButtonID를\_얻고 DisabledText/set DisabledText를\_\_사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-196">This class, like its server-side twin, includes two properties named TargetButtonID and DisabledText which you can access using get\_TargetButtonID/set\_TargetButtonID and get\_DisabledText/set\_DisabledText.</span></span>

<span data-ttu-id="86982-197">initialize() 메서드는 키업 이벤트 처리기를 동작에 대한 대상 요소와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-197">The initialize() method associates a keyup event handler with the target element for the behavior.</span></span> <span data-ttu-id="86982-198">이 동작과 연결된 TextBox에 문자를 입력할 때마다 키업 처리기가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-198">Each time you type a letter into the TextBox associated with this behavior, the keyup handler executes.</span></span> <span data-ttu-id="86982-199">키업 처리기는 동작과 연결된 TextBox에 텍스트가 포함되어 있는지 여부에 따라 Button을 활성화하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-199">The keyup handler either enables or disables the Button depending on whether the TextBox associated with the behavior contains any text.</span></span>

<span data-ttu-id="86982-200">리스팅 3에서 자바스크립트 파일을 포함된 리소스로 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-200">Remember that you must compile the JavaScript file in Listing 3 as an embedded resource.</span></span> <span data-ttu-id="86982-201">솔루션 탐색기 창에서 파일을 선택하고 속성 시트를 열고 *빌드* **작업** 속성에 포함된 리소스 값을 할당합니다(그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="86982-201">Select the file in the Solution Explorer window, open the property sheet, and assign the value *Embedded Resource* to the **Build Action** property (see Figure 3).</span></span> <span data-ttu-id="86982-202">이 옵션은 비주얼 스튜디오와 비주얼 웹 개발자 모두에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-202">This option is available in both Visual Studio and Visual Web Developer.</span></span>

<span data-ttu-id="86982-203">[![포함된 리소스로 JavaScript 파일 추가](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="86982-203">[![Adding a JavaScript file as an embedded resource](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)</span></span>

<span data-ttu-id="86982-204">**그림 03**: 자바스크립트 파일을 임베디드 리소스로 추가[(전체 크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="86982-204">**Figure 03**: Adding a JavaScript file as an embedded resource([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))</span></span>

## <a name="creating-the-custom-extender-designer"></a><span data-ttu-id="86982-205">사용자 지정 익스텐더 디자이너 만들기</span><span class="sxs-lookup"><span data-stu-id="86982-205">Creating the Custom Extender Designer</span></span>

<span data-ttu-id="86982-206">Extender를 완료하기 위해 만들어야 하는 마지막 클래스가 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-206">There is one last class that we need to create to complete our extender.</span></span> <span data-ttu-id="86982-207">목록 4에서 디자이너 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-207">We need to create the designer class in Listing 4.</span></span> <span data-ttu-id="86982-208">이 클래스는 확장자가 Visual Studio/Visual 웹 개발자 디자이너와 올바르게 행동하도록 하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-208">This class is required to make the extender behave correctly with the Visual Studio/Visual Web Developer Designer.</span></span>

<span data-ttu-id="86982-209">**리스팅 4 - DisabledButtonDesigner.cs**</span><span class="sxs-lookup"><span data-stu-id="86982-209">**Listing 4 - DisabledButtonDesigner.cs**</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

<span data-ttu-id="86982-210">목록 4의 디자이너를 디자이너 특성과 DisabledButton 익스텐더와 연결합니다. 다음과 같이 디자이너 특성을 DisabledButtonExtender 클래스에 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-210">You associate the designer in Listing 4 with the DisabledButton extender with the Designer attribute.You need to apply the Designer attribute to the DisabledButtonExtender class like this:</span></span>

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a><span data-ttu-id="86982-211">사용자 지정 익스텐더 사용</span><span class="sxs-lookup"><span data-stu-id="86982-211">Using the Custom Extender</span></span>

<span data-ttu-id="86982-212">이제 비활성화 버튼 컨트롤 익스텐더 만들기를 마쳤으니 ASP.NET 웹 사이트에서 사용할 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="86982-212">Now that we have finished creating the DisabledButton control extender, it is time to use it in our ASP.NET website.</span></span> <span data-ttu-id="86982-213">먼저 도구 상자에 사용자 지정 익스텐더를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-213">First, we need to add the custom extender to the toolbox.</span></span> <span data-ttu-id="86982-214">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="86982-214">Follow these steps:</span></span>

1. <span data-ttu-id="86982-215">솔루션 탐색기 창에서 페이지를 두 번 클릭하여 ASP.NET 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="86982-215">Open an ASP.NET page by double-clicking the page in the Solution Explorer window.</span></span>
2. <span data-ttu-id="86982-216">도구 상자를 마우스 오른쪽 단추로 클릭하고 메뉴 선택 옵션 **항목 선택.**</span><span class="sxs-lookup"><span data-stu-id="86982-216">Right-click the toolbox and select the menu option **Choose Items**.</span></span>
3. <span data-ttu-id="86982-217">도구 상자 항목 선택 대화 상자에서 CustomExtenders.dll 어셈블리를 찾아봅습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-217">In the Choose Toolbox Items dialog, browse to the CustomExtenders.dll assembly.</span></span>
4. <span data-ttu-id="86982-218">**확인** 버튼을 클릭하여 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-218">Click the **OK** button to close the dialog.</span></span>

<span data-ttu-id="86982-219">이 단계를 완료하면 비활성화 단추 컨트롤 익스텐더가 도구 상자에 나타납니다(그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="86982-219">After you complete these steps, the DisabledButton control extender should appear in the toolbox (see Figure 4).</span></span>

<span data-ttu-id="86982-220">[![도구 상자의 비활성화 단추](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="86982-220">[![DisabledButton in the toolbox](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)</span></span>

<span data-ttu-id="86982-221">**그림 04**: 도구 상자의 비활성화 버튼[(전체 크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="86982-221">**Figure 04**: DisabledButton in the toolbox([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))</span></span>

<span data-ttu-id="86982-222">다음으로 새 ASP.NET 페이지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-222">Next, we need to create a new ASP.NET page.</span></span> <span data-ttu-id="86982-223">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="86982-223">Follow these steps:</span></span>

1. <span data-ttu-id="86982-224">ShowDisabledButton.aspx라는 새 ASP.NET 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86982-224">Create a new ASP.NET page named ShowDisabledButton.aspx.</span></span>
2. <span data-ttu-id="86982-225">스크립트 관리자를 페이지로 드래그합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-225">Drag a ScriptManager onto the page.</span></span>
3. <span data-ttu-id="86982-226">텍스트 상자 컨트롤을 페이지로 끕습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-226">Drag a TextBox control onto the page.</span></span>
4. <span data-ttu-id="86982-227">단추 컨트롤을 페이지로 끕습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-227">Drag a Button control onto the page.</span></span>
5. <span data-ttu-id="86982-228">속성 창에서 Button ID 속성을 <em>btnSave</em> 값으로 변경하고 Text 속성을 *\*Save*값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-228">In the Properties window, change the Button ID property to the value <em>btnSave</em> and the Text property to the value *Save\**.</span></span>

<span data-ttu-id="86982-229">우리는 표준 ASP.NET 텍스트 상자와 버튼 컨트롤과 페이지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-229">We created a page with a standard ASP.NET TextBox and Button control.</span></span>

<span data-ttu-id="86982-230">다음으로, 비활성화 된 단추 확장기를 사용 하 고 TextBox 컨트롤을 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-230">Next, we need to extend the TextBox control with the DisabledButton extender:</span></span>

1. <span data-ttu-id="86982-231">Extender 마법사 대화 상자를 열려면 **확장작업 추가** 옵션을 선택합니다(그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="86982-231">Select the **Add Extender** task option to open the Extender Wizard dialog (see Figure 5).</span></span> <span data-ttu-id="86982-232">대화 상자에는 사용자 지정 비활성화단추 익스텐더가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-232">Notice that the dialog includes our custom DisabledButton extender.</span></span>
2. <span data-ttu-id="86982-233">비활성화 단추 익스텐더를 선택하고 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-233">Select the DisabledButton extender and click the **OK** button.</span></span>

<span data-ttu-id="86982-234">[![익스텐더 마법사 대화 상자](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="86982-234">[![The Extender Wizard dialog](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)</span></span>

<span data-ttu-id="86982-235">**그림 05**: 확장기 마법사 대화 상자[(클릭하여 전체 크기 이미지 보기)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="86982-235">**Figure 05**: The Extender Wizard dialog([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))</span></span>

<span data-ttu-id="86982-236">마지막으로 DisabledButton 익스텐더의 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-236">Finally, we can set the properties of the DisabledButton extender.</span></span> <span data-ttu-id="86982-237">TextBox 컨트롤의 속성을 수정하여 DisabledButton 익스텐더의 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-237">You can modify the properties of the DisabledButton extender by modifying the properties of the TextBox control:</span></span>

1. <span data-ttu-id="86982-238">디자이너에서 텍스트 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-238">Select the TextBox in the Designer.</span></span>
2. <span data-ttu-id="86982-239">속성 창에서 Extenders 노드를 확장합니다(그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="86982-239">In the Properties window, expand the Extenders node (see Figure 6).</span></span>
3. <span data-ttu-id="86982-240">DisabledText 속성에 *저장* 값 과 *값 btnSave* TargetButtonID 속성에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="86982-240">Assign the value *Save* to the DisabledText property and the value *btnSave* to the TargetButtonID property.</span></span>

<span data-ttu-id="86982-241">[![익스텐더 속성 설정](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="86982-241">[![Setting extender properties](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)</span></span>

<span data-ttu-id="86982-242">**그림 06**: 확장 속성[설정(전체 크기 이미지를 보려면 클릭)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="86982-242">**Figure 06**: Setting extender properties([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))</span></span>

<span data-ttu-id="86982-243">페이지를 실행하면(F5를 누르면) 단추 컨트롤이 처음에 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="86982-243">When you run the page (by hitting F5), the Button control is initially disabled.</span></span> <span data-ttu-id="86982-244">텍스트 상자에 텍스트를 입력하기 시작하면 단추 컨트롤이 활성화됩니다(그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="86982-244">As soon as you start entering text into the TextBox, the Button control is enabled (see Figure 7).</span></span>

<span data-ttu-id="86982-245">[![비활성화된 단추 익스텐더가 실행 중](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="86982-245">[![The DisabledButton extender in action](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)</span></span>

<span data-ttu-id="86982-246">**그림 07**: 비활성화 단추 익스텐더 가 작동하는[경우(클릭하여 전체 크기 이미지 보기)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="86982-246">**Figure 07**: The DisabledButton extender in action([Click to view full-size image](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))</span></span>

## <a name="summary"></a><span data-ttu-id="86982-247">요약</span><span class="sxs-lookup"><span data-stu-id="86982-247">Summary</span></span>

<span data-ttu-id="86982-248">이 자습서의 목표는 사용자 지정 익스텐더 컨트롤을 사용하여 AJAX 제어 도구 키트를 확장하는 방법을 설명하는 것이었습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-248">The goal of this tutorial was to explain how you can extend the AJAX Control Toolkit with custom extender controls.</span></span> <span data-ttu-id="86982-249">이 자습서에서는 간단한 DisabledButton 컨트롤 익스텐더를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-249">In this tutorial, we created a simple DisabledButton control extender.</span></span> <span data-ttu-id="86982-250">비활성화된 Button Extender 클래스, DisabledButtonBehavior 자바 스크립트 동작 및 DisabledButtonDesigner 클래스를 만들어이 확장기를 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="86982-250">We implemented this extender by creating a DisabledButtonExtender class, a DisabledButtonBehavior JavaScript behavior, and a DisabledButtonDesigner class.</span></span> <span data-ttu-id="86982-251">사용자 지정 컨트롤 extender를 만들 때마다 비슷한 단계 집합을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="86982-251">You follow a similar set of steps whenever you create a custom control extender.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="86982-252">[이전](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [다음](get-started-with-the-ajax-control-toolkit-vb.md)</span><span class="sxs-lookup"><span data-stu-id="86982-252">[Previous](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
[Next](get-started-with-the-ajax-control-toolkit-vb.md)</span></span>
