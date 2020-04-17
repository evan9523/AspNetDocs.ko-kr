---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 페이지 모델 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 숨결 코드 모델 중에서 선택할 수 있었습니다. 코드 숨결은 Src attr을 사용하여 구현 할 수 있습니다 ...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 6c2435a06d04209db21fb8e075f68ff0b7a9ef7e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542861"
---
# <a name="the-aspnet-20-page-model"></a><span data-ttu-id="7ee41-104">ASP.NET 2.0 페이지 모델</span><span class="sxs-lookup"><span data-stu-id="7ee41-104">The ASP.NET 2.0 Page Model</span></span>

<span data-ttu-id="7ee41-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7ee41-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7ee41-106">ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 숨결 코드 모델 중에서 선택할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="7ee41-107">코드 숨는 Src 특성 또는 지시의 CodeBehind 특성을 사용 하 여 구현될 수 있습니다. @Page</span><span class="sxs-lookup"><span data-stu-id="7ee41-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="7ee41-108">ASP.NET 2.0에서 개발자는 여전히 인라인 코드와 코드 숨미기 중에서 선택할 수 있지만 코드 숨미는 모델에 대한 상당한 개선 사항이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

<span data-ttu-id="7ee41-109">ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 숨결 코드 모델 중에서 선택할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="7ee41-110">코드 숨는 Src 특성 또는 지시의 CodeBehind 특성을 사용 하 여 구현될 수 있습니다. @Page</span><span class="sxs-lookup"><span data-stu-id="7ee41-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="7ee41-111">ASP.NET 2.0에서 개발자는 여전히 인라인 코드와 코드 숨미기 중에서 선택할 수 있지만 코드 숨미는 모델에 대한 상당한 개선 사항이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="7ee41-112">코드 뒤 모델의 개선 사항</span><span class="sxs-lookup"><span data-stu-id="7ee41-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="7ee41-113">ASP.NET 2.0의 코드 뒤에 있는 모델의 변경 사항을 완전히 이해하려면 ASP.NET 1.x에 존재했던 모델을 신속하게 검토하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="7ee41-114">ASP.NET 1.x의 코드 뒤 모델</span><span class="sxs-lookup"><span data-stu-id="7ee41-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="7ee41-115">ASP.NET 1.x에서 코드 뒤 모델은 ASPX 파일(웹폼)과 프로그래밍 코드가 포함된 코드 숨결 파일로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="7ee41-116">두 파일은 ASPX 파일의 @Page 지시문을 사용하여 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="7ee41-117">ASPX 페이지의 각 컨트롤에는 코드 숨김 파일에 인스턴스 변수로 해당 선언이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="7ee41-118">코드 숨김 파일에는 이벤트 바인딩을 위한 코드와 Visual Studio 디자이너에 필요한 생성된 코드도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="7ee41-119">이 모델은 상당히 잘 작동했지만 ASPX 페이지의 모든 ASP.NET 요소는 코드 숨은 파일에서 해당 코드가 필요하기 때문에 코드와 콘텐츠의 진정한 분리가 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="7ee41-120">예를 들어 디자이너가 Visual Studio IDE 외부의 ASPX 파일에 새 서버 컨트롤을 추가한 경우 코드 숨김 파일에서 해당 컨트롤에 대한 선언이 없기 때문에 응용 프로그램이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="7ee41-121">ASP.NET 코드 뒤 모델 2.0</span><span class="sxs-lookup"><span data-stu-id="7ee41-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="7ee41-122">ASP.NET 2.0은 이 모델에서 크게 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="7ee41-123">ASP.NET 2.0에서는 ASP.NET 2.0에 제공된 새 *부분 클래스를* 사용하여 코드 숨미는 것이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="7ee41-124">ASP.NET 2.0의 코드 숨김 클래스는 클래스 정의의 일부만 포함한다는 것을 의미하는 부분 클래스로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-124">The code-behind class in ASP.NET 2.0 is defined as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="7ee41-125">클래스 정의의 나머지 부분은 런타임 시 또는 웹 사이트가 미리 컴파일될 때 ASPX 페이지를 사용하여 ASP.NET 2.0에 의해 동적으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="7ee41-126">@Page 지시문을 사용하여 코드 숨김 파일과 ASPX 페이지 간의 링크는 여전히 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="7ee41-127">그러나 CodeBehind 또는 Src 특성 대신 ASP.NET 2.0은 이제 CodeFile 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="7ee41-128">Inherits 특성은 페이지의 클래스 이름을 지정하는 데도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="7ee41-129">일반적인 @ 페이지 지시문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="7ee41-130">ASP.NET 2.0 코드 숨김 파일의 일반적인 클래스 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="7ee41-131">C# 및 Visual Basic은 현재 부분 클래스를 지원하는 유일한 관리언어입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="7ee41-132">따라서 J#을 사용하는 개발자는 ASP.NET 2.0에서 코드 뒤 모델을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>

<span data-ttu-id="7ee41-133">개발자는 이제 자신이 만든 코드만 포함하는 코드 파일을 갖게 되므로 새 모델은 코드 숨미기 모델을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="7ee41-134">또한 코드 숨김 파일에 인스턴스 변수 선언이 없기 때문에 코드와 콘텐츠를 진정한 분리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="7ee41-135">ASPX 페이지의 부분 클래스는 이벤트 바인딩이 이루어지는 위치이므로 Visual Basic 개발자는 코드 뒤에서 Handles 키워드를 사용하여 이벤트를 바인딩하여 약간의 성능 향상을 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="7ee41-136">C#에는 동등한 키워드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-136">C# has no equivalent keyword.</span></span>

## <a name="new--page-directive-attributes"></a><span data-ttu-id="7ee41-137">새 @ 페이지 지시문 특성</span><span class="sxs-lookup"><span data-stu-id="7ee41-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="7ee41-138">ASP.NET 2.0 @ 페이지 지시문에 많은 새 특성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="7ee41-139">ASP.NET 2.0의 새로운 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="7ee41-140">Async</span><span class="sxs-lookup"><span data-stu-id="7ee41-140">Async</span></span>

<span data-ttu-id="7ee41-141">비동기 특성을 사용하면 비동기적으로 실행되도록 페이지를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="7ee41-142">이 모듈의 후반부에서 비동기 페이지를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="7ee41-143">비동기 시간 시간</span><span class="sxs-lookup"><span data-stu-id="7ee41-143">AsyncTimeout</span></span>

<span data-ttu-id="7ee41-144">비동기 페이지에 대한 시간 지정을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="7ee41-145">기본값은 45초입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="7ee41-146">Codefile</span><span class="sxs-lookup"><span data-stu-id="7ee41-146">CodeFile</span></span>

<span data-ttu-id="7ee41-147">CodeFile 특성은 Visual Studio 2002/2003의 CodeBehind 특성을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="7ee41-148">코드 파일베이스 클래스</span><span class="sxs-lookup"><span data-stu-id="7ee41-148">CodeFileBaseClass</span></span>

<span data-ttu-id="7ee41-149">CodeFileBaseClass 특성은 여러 페이지가 단일 기본 클래스에서 파생되는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="7ee41-150">이 특성이 없는 ASP.NET 부분 클래스를 구현하기 때문에 ASP.NETs 컴파일 엔진이 페이지의 컨트롤을 기반으로 새 멤버를 자동으로 생성하기 때문에 ASPX 페이지에 선언된 참조 컨트롤에 공유 공통 필드를 사용하는 기본 클래스가 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="7ee41-151">따라서 ASP.NET 두 개 이상의 페이지에 대한 공통 기본 클래스를 원하는 경우 CodeFileBaseClass 특성에서 기본 클래스를 지정한 다음 해당 기본 클래스에서 각 페이지 클래스를 파생시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="7ee41-152">이 특성을 사용할 때도 CodeFile 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="7ee41-153">편집 모드</span><span class="sxs-lookup"><span data-stu-id="7ee41-153">CompilationMode</span></span>

<span data-ttu-id="7ee41-154">이 특성을 사용하면 ASPX 페이지의 컴파일레이션모드 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="7ee41-155">컴파일모드 속성은 **항상**, **자동**및 **안**함 값을 포함하는 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="7ee41-156">기본값은 **항상**입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-156">The default is **Always**.</span></span> <span data-ttu-id="7ee41-157">**자동** 설정을 사용하면 ASP.NET 가능하면 페이지를 동적으로 컴파일할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="7ee41-158">동적 컴파일에서 페이지를 제외하면 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="7ee41-159">그러나 제외된 페이지에 컴파일해야 하는 코드가 포함된 경우 페이지를 탐색할 때 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="7ee41-160">활성화이벤트유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7ee41-160">EnableEventValidation</span></span>

<span data-ttu-id="7ee41-161">이 특성은 포스트백 및 콜백 이벤트의 유효성을 검사할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="7ee41-162">이 옵션을 사용하면 포스트백 또는 콜백 이벤트에 대한 인수가 확인되어 원래 렌더링한 서버 컨트롤에서 시작되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="7ee41-163">Enabletheming</span><span class="sxs-lookup"><span data-stu-id="7ee41-163">EnableTheming</span></span>

<span data-ttu-id="7ee41-164">이 특성은 ASP.NET 테마가 페이지에서 사용되는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="7ee41-165">기본값은 **false입니다.**</span><span class="sxs-lookup"><span data-stu-id="7ee41-165">The default is **false**.</span></span> <span data-ttu-id="7ee41-166">ASP.NET 테마는 [모듈 10에서](profiles-themes-and-web-parts.md)다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="7ee41-167">라인프라그마스</span><span class="sxs-lookup"><span data-stu-id="7ee41-167">LinePragmas</span></span>

<span data-ttu-id="7ee41-168">이 특성은 컴파일 중에 라인 실용모를 추가해야 하는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="7ee41-169">라인 pragmas 코드의 특정 섹션을 표시 하는 디버거에 의해 사용 되는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="7ee41-170">유지 보수스크롤포지션포스트백</span><span class="sxs-lookup"><span data-stu-id="7ee41-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="7ee41-171">이 특성은 포스트백 간의 스크롤 위치를 유지하기 위해 JavaScript가 페이지에 삽입되는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="7ee41-172">이 특성은 기본적으로 **false입니다.**</span><span class="sxs-lookup"><span data-stu-id="7ee41-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="7ee41-173">이 특성이 **true이면**ASP.NET &lt;&gt; 다음과 같이 보이는 스크립트 블록을 포스트백에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="7ee41-174">이 스크립트 블록의 src는 WebResource.axd입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="7ee41-175">이 리소스는 물리적 경로가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-175">This resource is not a physical path.</span></span> <span data-ttu-id="7ee41-176">이 스크립트가 요청되면 ASP.NET 동적으로 스크립트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="7ee41-177">마스터페이지파일</span><span class="sxs-lookup"><span data-stu-id="7ee41-177">MasterPageFile</span></span>

<span data-ttu-id="7ee41-178">이 특성은 현재 페이지의 마스터 페이지 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="7ee41-179">경로는 상대적이거나 절대적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-179">The path can be relative or absolute.</span></span> <span data-ttu-id="7ee41-180">마스터 페이지는 [모듈 4에서](master-pages.md)다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="7ee41-181">Stylesheettheme</span><span class="sxs-lookup"><span data-stu-id="7ee41-181">StyleSheetTheme</span></span>

<span data-ttu-id="7ee41-182">이 특성을 사용하면 ASP.NET 2.0 테마로 정의된 사용자 인터페이스 모양 속성을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="7ee41-183">테마는 [모듈 10에서](profiles-themes-and-web-parts.md)다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="7ee41-184">테마</span><span class="sxs-lookup"><span data-stu-id="7ee41-184">Theme</span></span>

<span data-ttu-id="7ee41-185">페이지의 테마를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-185">Specifies the theme for the page.</span></span> <span data-ttu-id="7ee41-186">StyleSheetTheme 특성에 대한 값을 지정하지 않은 경우 테마 특성은 페이지의 컨트롤에 적용되는 모든 스타일을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="7ee41-187">제목</span><span class="sxs-lookup"><span data-stu-id="7ee41-187">Title</span></span>

<span data-ttu-id="7ee41-188">페이지의 제목을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-188">Sets the title for the page.</span></span> <span data-ttu-id="7ee41-189">여기에 지정된 값은 렌더링된 페이지의 &lt;제목&gt; 요소에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="7ee41-190">뷰상태 암호화 모드</span><span class="sxs-lookup"><span data-stu-id="7ee41-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="7ee41-191">ViewState암호화모드 열거형의 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="7ee41-192">사용 가능한 값은 **항상**, **자동**및 **없음**입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="7ee41-193">기본값은 **자동**입니다. 이 특성이 **자동**값으로 설정되면 viewstate가 암호화되어 **등록요구뷰스테이트암호화** 메서드를 호출하여 제어 요청을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="7ee41-194">@ 페이지 지시문을 통해 공용 속성 값 설정</span><span class="sxs-lookup"><span data-stu-id="7ee41-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="7ee41-195">ASP.NET 2.0에서 @Page 지시문의 또 다른 새로운 기능은 기본 클래스의 공용 속성의 초기 값을 설정하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="7ee41-196">예를 들어 기본 클래스에 **SomeText라는** 공용 속성이 있고 페이지가 로드될 때 **Hello로** 초기화하려고 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="7ee41-197">@Page 지시문에 다음과 같이 값을 설정하기만 하면 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="7ee41-198">@ 페이지 지시문의 **SomeText** 특성은 기본 클래스의 SomeText 속성의 초기 값을 *Hello로 설정합니다.*.</span><span class="sxs-lookup"><span data-stu-id="7ee41-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="7ee41-199">아래 비디오는 @ Page 지시문을 사용하여 기본 클래스에서 공용 속성의 초기 값을 설정하는 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>

![](the-asp-net-2-0-page-model/_static/image1.png)

[<span data-ttu-id="7ee41-200">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="7ee41-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="7ee41-201">페이지 클래스의 새 공용 속성</span><span class="sxs-lookup"><span data-stu-id="7ee41-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="7ee41-202">다음 공용 속성은 ASP.NET 2.0의 새 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="7ee41-203">앱상대템플릿소스디렉터리</span><span class="sxs-lookup"><span data-stu-id="7ee41-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="7ee41-204">응용 프로그램 상대 경로를 페이지 또는 컨트롤에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="7ee41-205">예를 들어 http://app/folder/page.aspx에 있는 페이지의 경우 속성은 ~/폴더/를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="7ee41-206">앱상대가상패스</span><span class="sxs-lookup"><span data-stu-id="7ee41-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="7ee41-207">상대 가상 디렉터리 경로를 페이지 또는 컨트롤에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="7ee41-208">예를 들어 에 http://app/folder/page.aspx있는 페이지의 경우 속성은 ~/폴더/page.aspx를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="7ee41-209">비동기 시간 시간</span><span class="sxs-lookup"><span data-stu-id="7ee41-209">AsyncTimeout</span></span>

<span data-ttu-id="7ee41-210">비동기 페이지 처리에 사용되는 시간 시간을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="7ee41-211">비동기 페이지는 이 모듈의 후반부에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="7ee41-212">클라이언트 쿼리 스트링</span><span class="sxs-lookup"><span data-stu-id="7ee41-212">ClientQueryString</span></span>

<span data-ttu-id="7ee41-213">요청된 URL의 쿼리 문자열 부분을 반환하는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="7ee41-214">이 값은 URL 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-214">This value is URL encoded.</span></span> <span data-ttu-id="7ee41-215">HttpServerUtility 클래스의 UrlDecode 메서드를 사용하여 디코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="7ee41-216">클라이언트 스크립트</span><span class="sxs-lookup"><span data-stu-id="7ee41-216">ClientScript</span></span>

<span data-ttu-id="7ee41-217">이 속성은 클라이언트 쪽 스크립트의 ASP.NETs 방출을 관리하는 데 사용할 수 있는 ClientScriptManager 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="7ee41-218">(ClientScriptManager 클래스는 이 모듈의 후반부에서 다룹니다.)</span><span class="sxs-lookup"><span data-stu-id="7ee41-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="7ee41-219">활성화이벤트유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7ee41-219">EnableEventValidation</span></span>

<span data-ttu-id="7ee41-220">이 속성은 포스트백 및 콜백 이벤트에 대해 이벤트 유효성 검사를 사용하도록 설정할지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="7ee41-221">이 옵션을 사용하면 포스트백 또는 콜백 이벤트에 대한 인수가 확인되어 원래 렌더링된 서버 컨트롤에서 시작되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="7ee41-222">Enabletheming</span><span class="sxs-lookup"><span data-stu-id="7ee41-222">EnableTheming</span></span>

<span data-ttu-id="7ee41-223">이 속성은 ASP.NET 2.0 테마가 페이지에 적용되는지 여부를 지정하는 부울을 얻거나 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="7ee41-224">Form</span><span class="sxs-lookup"><span data-stu-id="7ee41-224">Form</span></span>

<span data-ttu-id="7ee41-225">이 속성은 ASPX 페이지에서 HTML 양식을 HtmlForm 개체로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="7ee41-226">헤더</span><span class="sxs-lookup"><span data-stu-id="7ee41-226">Header</span></span>

<span data-ttu-id="7ee41-227">이 속성은 페이지 헤더를 포함하는 HtmlHead 개체에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="7ee41-228">반환된 HtmlHead 오브젝트를 사용하여 스타일 시트, 메타 태그 등을 얻음/설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="7ee41-229">IdSparator</span><span class="sxs-lookup"><span data-stu-id="7ee41-229">IdSeparator</span></span>

<span data-ttu-id="7ee41-230">이 읽기 전용 속성은 ASP.NET 페이지에서 컨트롤에 대 한 고유 ID를 빌드할 때 컨트롤 식별자를 분리 하는 데 사용 되는 문자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="7ee41-231">코드에서 직접 사용하기에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="7ee41-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="7ee41-232">IsAsync</span></span>

<span data-ttu-id="7ee41-233">이 속성은 비동기 페이지를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="7ee41-234">비동기 페이지는 이 모듈의 후반부에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="7ee41-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="7ee41-235">IsCallback</span></span>

<span data-ttu-id="7ee41-236">이 읽기 전용 속성은 페이지가 호출 백의 결과인 경우 **true를** 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="7ee41-237">콜백은 이 모듈의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="7ee41-238">이스크로스페이지포스트백</span><span class="sxs-lookup"><span data-stu-id="7ee41-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="7ee41-239">이 읽기 전용 속성은 페이지가 교차 페이지 포스트백의 일부인 경우 **true를** 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="7ee41-240">교차 페이지 포스트백은 이 모듈의 뒷부분에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="7ee41-241">Items</span><span class="sxs-lookup"><span data-stu-id="7ee41-241">Items</span></span>

<span data-ttu-id="7ee41-242">페이지 컨텍스트에 저장된 모든 개체를 포함하는 IDictionary 인스턴스에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="7ee41-243">이 IDictionary 개체에 항목을 추가할 수 있으며 컨텍스트의 수명 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="7ee41-244">유지 보수스크롤포지션포스트백</span><span class="sxs-lookup"><span data-stu-id="7ee41-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="7ee41-245">이 속성은 ASP.NET 포스트백이 발생한 후 브라우저에서 페이지 스크롤 위치를 유지하는 JavaScript를 내는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="7ee41-246">이 속성에 대한 자세한 내용은 이 모듈의 앞에서 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="7ee41-247">마스터</span><span class="sxs-lookup"><span data-stu-id="7ee41-247">Master</span></span>

<span data-ttu-id="7ee41-248">이 읽기 전용 속성은 마스터 페이지가 적용된 페이지에 대한 MasterPage 인스턴스에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="7ee41-249">마스터페이지파일</span><span class="sxs-lookup"><span data-stu-id="7ee41-249">MasterPageFile</span></span>

<span data-ttu-id="7ee41-250">페이지의 마스터 페이지 파일 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="7ee41-251">이 속성은 PreInit 메서드에서만 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="7ee41-252">맥스페이지스테이트필드길이</span><span class="sxs-lookup"><span data-stu-id="7ee41-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="7ee41-253">이 속성은 페이지 상태의 최대 길이를 바이트로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="7ee41-254">속성이 양수로 설정된 경우 페이지 보기 상태는 지정된 바이트 수를 초과하지 않도록 여러 숨겨진 필드로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="7ee41-255">속성이 음수인 경우 뷰 상태는 청크로 나눌 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="7ee41-256">페이지 어댑터</span><span class="sxs-lookup"><span data-stu-id="7ee41-256">PageAdapter</span></span>

<span data-ttu-id="7ee41-257">요청 브라우저에 대한 페이지를 수정하는 PageAdapter 개체에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="7ee41-258">Previouspage</span><span class="sxs-lookup"><span data-stu-id="7ee41-258">PreviousPage</span></span>

<span data-ttu-id="7ee41-259">Server.Transfer 또는 교차 페이지 포스트백의 경우 이전 페이지에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="7ee41-260">Skinid</span><span class="sxs-lookup"><span data-stu-id="7ee41-260">SkinID</span></span>

<span data-ttu-id="7ee41-261">페이지에 적용할 ASP.NET 2.0 스킨을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="7ee41-262">Stylesheettheme</span><span class="sxs-lookup"><span data-stu-id="7ee41-262">StyleSheetTheme</span></span>

<span data-ttu-id="7ee41-263">이 속성은 페이지에 적용되는 스타일 시트를 얻거나 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="7ee41-264">템플릿 제어</span><span class="sxs-lookup"><span data-stu-id="7ee41-264">TemplateControl</span></span>

<span data-ttu-id="7ee41-265">페이지에 대한 포함 컨트롤에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="7ee41-266">테마</span><span class="sxs-lookup"><span data-stu-id="7ee41-266">Theme</span></span>

<span data-ttu-id="7ee41-267">페이지에 적용된 ASP.NET 2.0 테마의 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="7ee41-268">이 값은 PreInit 메서드 앞에 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="7ee41-269">제목</span><span class="sxs-lookup"><span data-stu-id="7ee41-269">Title</span></span>

<span data-ttu-id="7ee41-270">이 속성은 페이지 헤더에서 가져온 대로 페이지의 제목을 가져오거나 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="7ee41-271">뷰상태 암호화 모드</span><span class="sxs-lookup"><span data-stu-id="7ee41-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="7ee41-272">페이지의 ViewState암호화 모드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="7ee41-273">이 단원의 앞에서 이 속성에 대한 자세한 설명은 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ee41-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="7ee41-274">페이지 클래스의 새 보호속성</span><span class="sxs-lookup"><span data-stu-id="7ee41-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="7ee41-275">다음은 ASP.NET 2.0에서 Page 클래스의 새 보호된 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="7ee41-276">어댑터</span><span class="sxs-lookup"><span data-stu-id="7ee41-276">Adapter</span></span>

<span data-ttu-id="7ee41-277">요청한 장치에서 페이지를 렌더링하는 ControlAdapter에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="7ee41-278">비동기 모드</span><span class="sxs-lookup"><span data-stu-id="7ee41-278">AsyncMode</span></span>

<span data-ttu-id="7ee41-279">이 속성은 페이지가 비동기적으로 처리되는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="7ee41-280">코드에서 직접 사용하지 않고 런타임에서 사용하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="7ee41-281">클라이언트ID세파레이터</span><span class="sxs-lookup"><span data-stu-id="7ee41-281">ClientIDSeparator</span></span>

<span data-ttu-id="7ee41-282">이 속성은 컨트롤에 대 한 고유한 클라이언트 아이디를 만들 때 구분 기호로 사용 되는 문자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="7ee41-283">코드에서 직접 사용하지 않고 런타임에서 사용하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="7ee41-284">페이지스테이트퍼시스터</span><span class="sxs-lookup"><span data-stu-id="7ee41-284">PageStatePersister</span></span>

<span data-ttu-id="7ee41-285">이 속성은 페이지에 대 한 PageStatePersister 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="7ee41-286">이 속성은 주로 ASP.NET 컨트롤 개발자가 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="7ee41-287">유니크파일패스서픽스</span><span class="sxs-lookup"><span data-stu-id="7ee41-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="7ee41-288">이 속성은 브라우저를 캐싱하기 위한 파일 경로에 추가된 고유한 접미사를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-288">This property returns a unique suffix that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="7ee41-289">기본값은 \_ \_ufps= 및 6자리 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="7ee41-290">페이지 클래스에 대한 새 공용 메서드</span><span class="sxs-lookup"><span data-stu-id="7ee41-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="7ee41-291">다음 공개 메서드는 ASP.NET 2.0의 Page 클래스에 새로 가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="7ee41-292">애드온프리렌더컴량</span><span class="sxs-lookup"><span data-stu-id="7ee41-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="7ee41-293">이 메서드는 비동기 페이지 실행을 위한 이벤트 처리기 대리자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="7ee41-294">비동기 페이지는 이 모듈의 후반부에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="7ee41-295">적용스타일시트스킨</span><span class="sxs-lookup"><span data-stu-id="7ee41-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="7ee41-296">페이지 스타일 시트의 속성을 페이지에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="7ee41-297">실행등록된 동기 작업</span><span class="sxs-lookup"><span data-stu-id="7ee41-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="7ee41-298">이 메서드는 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="7ee41-299">겟검증자</span><span class="sxs-lookup"><span data-stu-id="7ee41-299">GetValidators</span></span>

<span data-ttu-id="7ee41-300">지정되지 않은 유효성 검사 그룹이 없는 경우 지정된 유효성 검사 그룹 또는 기본 유효성 검사 그룹에 대한 유효성 검사기 컬렉션을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="7ee41-301">레지스터AsyncTask</span><span class="sxs-lookup"><span data-stu-id="7ee41-301">RegisterAsyncTask</span></span>

<span data-ttu-id="7ee41-302">이 메서드는 새 비동기 작업을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-302">This method registers a new async task.</span></span> <span data-ttu-id="7ee41-303">비동기 페이지는 이 모듈의 후반부에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="7ee41-304">레지스터필요컨트롤상태</span><span class="sxs-lookup"><span data-stu-id="7ee41-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="7ee41-305">이 메서드는 ASP.NET 페이지 제어 상태를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="7ee41-306">Register필요뷰상태암호화</span><span class="sxs-lookup"><span data-stu-id="7ee41-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="7ee41-307">이 메서드는 ASP.NET 페이지 viewstate 암호화가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="7ee41-308">해결 클라이언트Url</span><span class="sxs-lookup"><span data-stu-id="7ee41-308">ResolveClientUrl</span></span>

<span data-ttu-id="7ee41-309">이미지 등에 대한 클라이언트 요청에 사용할 수 있는 상대 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="7ee41-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="7ee41-310">SetFocus</span></span>

<span data-ttu-id="7ee41-311">이 메서드는 페이지를 처음 로드할 때 지정 된 컨트롤에 포커스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="7ee41-312">레지스터 해제컨트롤상태</span><span class="sxs-lookup"><span data-stu-id="7ee41-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="7ee41-313">이 메서드는 더 이상 제어 상태 지속성을 필요로 하지 않는 컨트롤으로 전달 되는 컨트롤을 등록 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="7ee41-314">페이지 수명 주기 변경</span><span class="sxs-lookup"><span data-stu-id="7ee41-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="7ee41-315">ASP.NET 2.0의 페이지 수명 주기는 크게 변경되지 않았지만 알아야 할 몇 가지 새로운 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-315">The page lifecycle in ASP.NET 2.0 hasn't changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="7ee41-316">ASP.NET 2.0 페이지 수명 주기는 아래에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="7ee41-317">프리이니트 (ASP.NET 2.0의 새로운 것)</span><span class="sxs-lookup"><span data-stu-id="7ee41-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="7ee41-318">PreInit 이벤트는 개발자가 액세스할 수 있는 수명 주기의 초기 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="7ee41-319">이 이벤트가 추가되면 2.0 테마, 마스터 페이지, ASP.NET 2.0 프로필에 대한 액세스 속성 등을 프로그래밍 방식으로 변경할 수 ASP.NET. 포스트백 상태에 있는 경우 Viewstate가 수명 주기의 이 시점에서 컨트롤에 아직 적용되지 않았다는 것을 깨닫는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="7ee41-320">따라서 이 단계에서 개발자가 컨트롤의 속성을 변경하는 경우 페이지 수명 주기의 나중에 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="7ee41-321">Init</span><span class="sxs-lookup"><span data-stu-id="7ee41-321">Init</span></span>

<span data-ttu-id="7ee41-322">Init 이벤트는 ASP.NET 1.x에서 변경되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="7ee41-323">페이지에서 컨트롤의 속성을 읽거나 초기화하려는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="7ee41-324">이 단계에서는 마스터 페이지, 테마 등이 이미 페이지에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="7ee41-325">InitComplete(2.0의 새로운 것)</span><span class="sxs-lookup"><span data-stu-id="7ee41-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="7ee41-326">InitComplete 이벤트는 페이지 초기화 단계의 끝에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="7ee41-327">수명 주기의 이 시점에서 페이지의 컨트롤에 액세스할 수 있지만 해당 상태는 아직 채워지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="7ee41-328">사전 로드(2.0의 새로운 것)</span><span class="sxs-lookup"><span data-stu-id="7ee41-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="7ee41-329">이 이벤트는 모든 포스트백 데이터가 적용된 후 페이지\_로드 직전에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="7ee41-330">로드</span><span class="sxs-lookup"><span data-stu-id="7ee41-330">Load</span></span>

<span data-ttu-id="7ee41-331">로드 이벤트는 ASP.NET 1.x에서 변경되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="7ee41-332">로드완료(2.0의 새로운 것)</span><span class="sxs-lookup"><span data-stu-id="7ee41-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="7ee41-333">LoadComplete 이벤트는 페이지 로드 단계의 마지막 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="7ee41-334">이 단계에서는 모든 포스트백 및 뷰상태 데이터가 페이지에 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="7ee41-335">Prerender</span><span class="sxs-lookup"><span data-stu-id="7ee41-335">PreRender</span></span>

<span data-ttu-id="7ee41-336">페이지에 동적으로 추가된 컨트롤에 대해 viewstate를 적절하게 유지 관리하려면 PreRender 이벤트가 마지막으로 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="7ee41-337">프리렌더완료(2.0의 새로운 것)</span><span class="sxs-lookup"><span data-stu-id="7ee41-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="7ee41-338">PreRenderComplete 단계에서 모든 컨트롤이 페이지에 추가되고 페이지를 렌더링할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="7ee41-339">PreRenderComplete 이벤트는 페이지 뷰상태가 저장되기 전에 발생한 마지막 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="7ee41-340">저장 상태완료(2.0의 새로운 것)</span><span class="sxs-lookup"><span data-stu-id="7ee41-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="7ee41-341">SaveStateComplete 이벤트는 모든 페이지 뷰상태 및 제어 상태가 저장된 직후에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="7ee41-342">이 이벤트는 페이지가 실제로 브라우저에 렌더링되기 전의 마지막 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="7ee41-343">렌더링</span><span class="sxs-lookup"><span data-stu-id="7ee41-343">Render</span></span>

<span data-ttu-id="7ee41-344">렌더링 메서드는 1.x ASP.NET 이후로 변경되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="7ee41-345">HtmlTextWriter가 초기화되고 페이지가 브라우저에 렌더링되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="7ee41-346">ASP.NET 2.0의 크로스 페이지 포스트백</span><span class="sxs-lookup"><span data-stu-id="7ee41-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="7ee41-347">ASP.NET 1.x에서는 포스트백이 같은 페이지에 게시해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="7ee41-348">교차 페이지 포스트백은 허용되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="7ee41-349">ASP.NET 2.0은 IButtonControl 인터페이스를 통해 다른 페이지에 다시 게시할 수 있는 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="7ee41-350">타사 사용자 지정 컨트롤 외에 새로운 IButtonControl 인터페이스(단추, LinkButton 및 ImageButton)를 구현하는 모든 컨트롤은 PostBackUrl 특성을 사용하여 이 새로운 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="7ee41-351">다음 코드는 두 번째 페이지로 다시 게시하는 Button 컨트롤을 보여 주며, 이 컨트롤은 두 번째 페이지로 다시 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="7ee41-352">페이지가 다시 게시되면 포스트백을 시작하는 페이지는 두 번째 페이지의 PreviousPage 속성을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="7ee41-353">이 기능은 컨트롤이 다른\_페이지로 다시 게시할 때 ASP.NET 2.0이 페이지에 렌더링되는 새로운 WebForm DoPostBackWithOptions 클라이언트 쪽 기능을 통해 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="7ee41-354">이 자바 스크립트 함수는 클라이언트에 스크립트를 내보하는 새로운 WebResource.axd 처리기에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="7ee41-355">아래 동영상은 교차 페이지 포스트백의 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-355">The video below is a walkthrough of a cross-page postback.</span></span>

![](the-asp-net-2-0-page-model/_static/image2.png)

[<span data-ttu-id="7ee41-356">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="7ee41-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="7ee41-357">교차 페이지 포스트백에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="7ee41-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="7ee41-358">Viewstate</span><span class="sxs-lookup"><span data-stu-id="7ee41-358">Viewstate</span></span>

<span data-ttu-id="7ee41-359">교차 페이지 포스트백 시나리오의 첫 번째 페이지에서 뷰 상태에 어떤 일이 발생하는지 이미 자문해 보았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="7ee41-360">결국 IPostBackDataHandler를 구현하지 않는 모든 컨트롤은 viewstate를 통해 해당 상태를 유지하므로 교차 페이지 포스트백의 두 번째 페이지에서 해당 컨트롤의 속성에 액세스하려면 페이지의 뷰상태에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="7ee41-361">ASP.NET 2.0은 이전 PAGE라는 \_ \_두 번째 페이지에서 새 숨겨진 필드를 사용하여 이 시나리오를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="7ee41-362">이전 \_ \_페이지 양식 필드에는 첫 번째 페이지의 뷰상태가 포함되어 있으므로 두 번째 페이지의 모든 컨트롤의 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="7ee41-363">찾기 제어 우회</span><span class="sxs-lookup"><span data-stu-id="7ee41-363">Circumventing FindControl</span></span>

<span data-ttu-id="7ee41-364">교차 페이지 포스트백의 비디오 연습에서 FindControl 메서드를 사용하여 첫 페이지의 TextBox 컨트롤에 대한 참조를 얻었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="7ee41-365">이 메서드는 이러한 용도로 는 잘 작동하지만 FindControl은 비용이 많이 들며 추가 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="7ee41-366">다행히 ASP.NET 2.0은 많은 시나리오에서 작동하는 이 목적을 위해 FindControl에 대한 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="7ee41-367">이전 PageType 지시문을 사용하면 TypeName 또는 VirtualPath 특성을 사용하여 이전 페이지에 대한 강력한 형식의 참조를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="7ee41-368">TypeName 특성을 사용하면 이전 페이지의 형식을 지정할 수 있으며 VirtualPath 특성을 사용하면 가상 경로를 사용하여 이전 페이지를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="7ee41-369">이전 PageType 지시문을 설정한 후 공용 속성을 사용하여 액세스를 허용하려는 컨트롤 등을 노출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="7ee41-370">랩 1 크로스 페이지 포스트백</span><span class="sxs-lookup"><span data-stu-id="7ee41-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="7ee41-371">이 실습에서는 ASP.NET 2.0의 새 교차 페이지 포스트백 기능을 사용하는 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="7ee41-372">Visual Studio 2005를 열고 새 ASP.NET 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="7ee41-373">page2.aspx라는 새 웹 양식을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="7ee41-374">디자인 뷰에서 Default.aspx를 열고 단추 컨트롤과 텍스트 상자 컨트롤을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="7ee41-375">단추 컨트롤에 **SubmitButton의** ID를 지정하고 TextBox에서 **사용자 이름의**ID를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="7ee41-376">단추의 PostBackUrl 속성을 page2.aspx로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="7ee41-377">소스 보기에서 페이지2.aspx를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="7ee41-378">아래와 같이 @ 이전 페이지 유형 지시문을 추가하십시오.</span><span class="sxs-lookup"><span data-stu-id="7ee41-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="7ee41-379">page2.aspx의\_코드 숨결의 페이지 로드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="7ee41-380">빌드 메뉴에서 빌드를 클릭하여 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="7ee41-381">Default.aspx에 대한 코드 숨결에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="7ee41-382">page2.aspx의 페이지\_로드를 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="7ee41-383">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-383">Build the project.</span></span>
11. <span data-ttu-id="7ee41-384">프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-384">Run the project.</span></span>
12. <span data-ttu-id="7ee41-385">TextBox에 이름을 입력하고 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="7ee41-386">결과는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7ee41-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="7ee41-387">ASP.NET 2.0의 비동기 페이지</span><span class="sxs-lookup"><span data-stu-id="7ee41-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="7ee41-388">ASP.NET 많은 경합 문제는 외부 호출(예: 웹 서비스 또는 데이터베이스 호출), 파일 IO 대기 시간 등의 대기 시간으로 인해 발생합니다. ASP.NET 응용 프로그램에 대해 요청이 이루어지면 ASP.NET 해당 작업자 스레드 중 하나를 사용하여 해당 요청을 서비스합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="7ee41-389">해당 요청은 요청이 완료되고 응답이 전송될 때까지 해당 스레드를 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="7ee41-390">ASP.NET 2.0은 페이지를 비동기적으로 실행하는 기능을 추가하여 이러한 유형의 문제와 함께 대기 시간 문제를 해결하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="7ee41-391">즉, 작업자 스레드는 요청을 시작한 다음 다른 스레드에 추가 실행을 전달하여 사용 가능한 스레드 풀로 빠르게 돌아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="7ee41-392">파일 IO, 데이터베이스 호출 등이 완료되면 스레드 풀에서 새 스레드를 가져와 요청을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="7ee41-393">페이지를 비동기적으로 실행하게 만드는 첫 번째 단계는 다음과 같이 페이지 지시문의 **Async** 특성을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="7ee41-394">이 특성은 ASP.NET 페이지에 대한 IHttpAsyncHandler를 구현하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="7ee41-395">다음 단계는 PreRender 이전 페이지의 수명 주기의 한 지점에서 AddOnPreRenderCompleteAsync 메서드를 호출하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="7ee41-396">이 메서드는 일반적으로 페이지\_로드에서 호출 됩니다. AddOnPreRenderCompleteAsync 메서드는 두 개의 매개 변수를 사용합니다. 시작 이벤트 처리기 및 끝 이벤트 처리기.</span><span class="sxs-lookup"><span data-stu-id="7ee41-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="7ee41-397">BeginEventHandler는 IAsyncResult를 반환한 다음 EndEventHandler에 매개 변수로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="7ee41-398">아래 비디오는 비동기 페이지 요청의 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-398">The video below is a walkthrough of an asynchronous page request.</span></span>

![](the-asp-net-2-0-page-model/_static/image3.png)

[<span data-ttu-id="7ee41-399">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="7ee41-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> <span data-ttu-id="7ee41-400">EndEventHandler가 완료될 때까지 비동기 페이지가 브라우저에 렌더링되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="7ee41-401">의심의 여지가 있지만 일부 개발자는 비동기 호출과 유사하다고 생각할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="7ee41-402">그렇지 않다는 것을 깨닫는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-402">It's important to realize that they are not.</span></span> <span data-ttu-id="7ee41-403">비동기 요청의 이점은 첫 번째 작업자 스레드를 스레드 풀로 반환하여 새 요청을 서비스할 수 있어 IO 바인딩 등으로 인한 경합이 줄어든다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>

## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="7ee41-404">ASP.NET 2.0의 스크립트 콜백</span><span class="sxs-lookup"><span data-stu-id="7ee41-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="7ee41-405">웹 개발자는 항상 콜백과 관련된 깜박임을 방지하는 방법을 모색해 왔으며,</span><span class="sxs-lookup"><span data-stu-id="7ee41-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="7ee41-406">ASP.NET 1.x에서 SmartNavigation은 깜박임을 방지하는 가장 일반적인 방법이었지만 SmartNavigation은 클라이언트에서 구현이 복잡하기 때문에 일부 개발자에게 문제를 일으켰습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="7ee41-407">ASP.NET 2.0은 스크립트 콜백으로 이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="7ee41-408">스크립트 콜백은 XMLHttp를 사용하여 JavaScript를 통해 웹 서버에 대한 요청을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="7ee41-409">XMLHttp 요청은 브라우저의 DOM을 통해 조작할 수 있는 XML 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="7ee41-410">XMLHttp 코드는 새 WebResource.axd 처리기에 의해 사용자에게 숨김이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="7ee41-411">ASP.NET 2.0에서 스크립트 콜백을 구성하는 데 필요한 몇 가지 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="7ee41-412">1단계 : ICallbackEventHandler 인터페이스 구현</span><span class="sxs-lookup"><span data-stu-id="7ee41-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="7ee41-413">ASP.NET 페이지를 스크립트 콜백에 참여하는 것으로 인식하려면 ICallbackEventHandler 인터페이스를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="7ee41-414">다음과 같이 코드 숨결 파일에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="7ee41-415">@Implements 지시문을 다음과 같이 사용하여 이 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="7ee41-416">일반적으로 인라인 ASP.NET 코드를 사용할 때 @Implements 지시문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="7ee41-417">2단계 : GetCallbackEvent참조 호출</span><span class="sxs-lookup"><span data-stu-id="7ee41-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="7ee41-418">앞에서 설명한 것처럼 XMLHttp 호출은 WebResource.axd 처리기에 캡슐화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="7ee41-419">페이지가 렌더링되면 ASP.NET WebResource.axd에서\_제공하는 클라이언트 스크립트인 WebForm DoCallback에 대한 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="7ee41-420">WebForm\_DoCallback 함수는 \_ \_콜백에 대한 doPostBack 함수를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="7ee41-421">doPostBack은 프로그래밍 방식으로 페이지에 양식을 제출한다는 것을 \_ \_기억하십시오.</span><span class="sxs-lookup"><span data-stu-id="7ee41-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="7ee41-422">콜백 시나리오에서는 포스트백을 방지하려고 하므로 \_ \_doPostBack으로는 충분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="7ee41-423">\_\_doPostBack은 여전히 클라이언트 스크립트 콜백 시나리오의 페이지에 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="7ee41-424">그러나 콜백에는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-424">However, it's not used for the callback.</span></span>

<span data-ttu-id="7ee41-425">WebForm\_DoCallback 클라이언트 측 함수에 대한 인수는 일반적으로 페이지\_로드에서 호출되는 서버 측 함수 GetCallbackEventReference를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="7ee41-426">GetCallbackEventReference에 대한 일반적인 호출은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="7ee41-427">이 경우 cm는 ClientScriptManager의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="7ee41-428">ClientScriptManager 클래스는 이 모듈의 후반부에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-428">The ClientScriptManager class will be covered later in this module.</span></span>

<span data-ttu-id="7ee41-429">GetCallbackEventReference에는 여러 오버로드된 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="7ee41-430">이 경우 인수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="7ee41-431">GetCallbackEventReference가 호출되는 컨트롤에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="7ee41-432">이 경우 페이지 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="7ee41-433">클라이언트 측 코드에서 서버 쪽 이벤트로 전달되는 문자열 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="7ee41-434">이 경우, 임 ddlCompany라는 드롭다운의 값을 전달한다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="7ee41-435">서버 쪽 콜백 이벤트에서 반환 값(문자열)을 수락하는 클라이언트 측 함수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="7ee41-436">이 함수는 서버 측 콜백이 성공한 경우에만 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="7ee41-437">따라서 견고성을 위해 일반적으로 오류 발생 시 실행할 클라이언트 측 함수의 이름을 지정하는 추가 문자열 인수를 사용하는 GetCallbackEventReference의 오버로드된 버전을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="7ee41-438">서버에 대한 콜백 전에 시작한 클라이언트 측 함수를 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="7ee41-439">이 경우 이러한 스크립트가 없으므로 인수는 null입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="7ee41-440">콜백을 비동기적으로 수행할지 여부를 지정하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="7ee41-441">클라이언트에서 WebForm\_DoCallback을 호출하면 이러한 인수가 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="7ee41-442">따라서 이 페이지가 클라이언트에서 렌더링되면 해당 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="7ee41-443">클라이언트에서 함수의 시그니처가 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="7ee41-444">클라이언트 측 함수는 5개의 문자열과 부울을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="7ee41-445">위의 예제에서 null인 추가 문자열에는 서버 측 콜백의 오류를 처리하는 클라이언트 측 함수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="7ee41-446">3단계 : 클라이언트 측 제어 이벤트 연결</span><span class="sxs-lookup"><span data-stu-id="7ee41-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="7ee41-447">위의 GetCallbackEventReference의 반환 값이 문자열 변수에 할당되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="7ee41-448">이 문자열은 콜백을 시작하는 컨트롤에 대한 클라이언트 쪽 이벤트를 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="7ee41-449">이 예제에서는 콜백이 페이지의 드롭다운에 의해 시작되므로 *OnChange* 이벤트를 연결하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="7ee41-450">클라이언트 쪽 이벤트를 연결하려면 다음과 같이 클라이언트 쪽 태그에 처리기를 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="7ee41-451">*cbRef는* GetCallbackEventReference에 대한 호출의 반환 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="7ee41-452">여기에는 위에 표시된\_WebForm DoCallback에 대한 호출이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="7ee41-453">4단계 : 클라이언트 측 스크립트 등록</span><span class="sxs-lookup"><span data-stu-id="7ee41-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="7ee41-454">GetCallbackEventReference 호출은 서버 측 콜백이 성공할 때 **ShowCompanyName이라는** 클라이언트 측 스크립트가 실행되도록 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="7ee41-455">해당 스크립트는 ClientScriptManager 인스턴스를 사용 하 여 페이지에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="7ee41-456">클라이언트스크립트관리자 클래스는 이 모듈의 후반부에서 설명합니다. 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-456">(The ClientScriptManager class will be discussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="7ee41-457">5 단계 : ICallbackEventHandler 인터페이스의 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="7ee41-458">ICallbackEventHandler코드에서 구현해야 하는 두 가지 방법이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="7ee41-459">그들은 **레이즈콜백 이벤트** 및 **겟콜백 이벤트입니다.**</span><span class="sxs-lookup"><span data-stu-id="7ee41-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="7ee41-460">**RaiseCallbackEvent** 인수로 문자열을 소요 하 고 아무것도 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="7ee41-461">문자열 인수는 클라이언트 측 호출에서 WebForm\_DoCallback으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="7ee41-462">이 경우 해당 값은 ddlCompany라는 드롭다운의 *값* 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="7ee41-463">서버 쪽 코드는 RaiseCallbackEvent 메서드에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="7ee41-464">예를 들어 콜백이 외부 리소스에 대해 WebRequest를 만드는 경우 해당 코드는 RaiseCallbackEvent에 배치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="7ee41-465">**GetCallbackEvent** 클라이언트에 콜백의 반환을 처리 하는 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="7ee41-466">인수를 수행하지 않고 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="7ee41-467">반환하는 문자열은 클라이언트 측 함수에 인수로 전달됩니다(이 경우 *ShowCompanyName*.</span><span class="sxs-lookup"><span data-stu-id="7ee41-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="7ee41-468">위의 단계를 완료하면 ASP.NET 2.0에서 스크립트 콜백을 수행할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>

![](the-asp-net-2-0-page-model/_static/image4.png)

[<span data-ttu-id="7ee41-469">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="7ee41-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)

<span data-ttu-id="7ee41-470">ASP.NET 스크립트 콜백은 XMLHttp 호출을 지원하는 모든 브라우저에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="7ee41-471">여기에는 현재 사용 되는 모든 최신 브라우저가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="7ee41-472">Internet Explorer는 XMLHttp ActiveX 개체를 사용하지만 다른 최신 브라우저(예정된 IE 7 포함)는 본질적인 XMLHttp 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="7ee41-473">브라우저가 콜백을 지원하는지 프로그래밍 방식으로 확인하려면 **Request.Browser.SupportCallback** 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="7ee41-474">요청 클라이언트가 스크립트 콜백을 지원하는 경우 이 속성은 **true를** 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="7ee41-475">ASP.NET 2.0에서 클라이언트 스크립트로 작업</span><span class="sxs-lookup"><span data-stu-id="7ee41-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="7ee41-476">ASP.NET 2.0의 클라이언트 스크립트는 ClientScriptManager 클래스를 사용하여 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="7ee41-477">ClientScriptManager 클래스는 형식과 이름을 사용하여 클라이언트 스크립트를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="7ee41-478">이렇게 하면 동일한 스크립트가 프로그래밍 방식으로 페이지에 두 번 이상 삽입되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="7ee41-479">스크립트가 페이지에 성공적으로 등록된 후 동일한 스크립트를 등록하려고 하면 스크립트가 두 번째로 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="7ee41-480">중복 스크립트가 추가되지 않으며 예외가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="7ee41-481">불필요한 계산을 방지하기 위해 스크립트가 이미 등록되어 있는지 확인하는 데 사용할 수 있으므로 두 번 이상 등록하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>

<span data-ttu-id="7ee41-482">ClientScriptManager의 메서드는 모든 현재 ASP.NET 개발자에게 익숙해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="7ee41-483">레지스터클라이언트스크립트블록</span><span class="sxs-lookup"><span data-stu-id="7ee41-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="7ee41-484">이 메서드는 렌더링된 페이지의 맨 위에 스크립트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="7ee41-485">이 기능은 클라이언트에서 명시적으로 호출되는 함수를 추가하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="7ee41-486">이 메서드에는 두 가지 오버로드된 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="7ee41-487">네 개의 인수 중 세 가지가 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="7ee41-488">아래에 이 계정과 키의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-488">They are:</span></span>

`type (string)`

<span data-ttu-id="7ee41-489">***형식*** 인수는 스크립트에 대한 형식을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="7ee41-490">일반적으로 페이지의 유형(이 형식)을 사용하는 것이 좋습니다. 형식에 대한 GetType())입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="7ee41-491">***키*** 인수는 스크립트에 대한 사용자 정의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="7ee41-492">각 스크립트에 대해 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-492">This should be unique for each script.</span></span> <span data-ttu-id="7ee41-493">동일한 키와 이미 추가된 스크립트 유형이 있는 스크립트를 추가하려고 하면 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="7ee41-494">***스크립트*** 인수는 추가할 실제 스크립트를 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="7ee41-495">StringBuilder를 사용하여 스크립트를 만든 다음 StringBuilder의 ToString() 메서드를 사용하여 ***스크립트*** 인수를 할당하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="7ee41-496">세 개의 인수만 사용하는 오버로드된 RegisterClientScriptBlock을 사용하는 경우&lt;스크립트&gt; &lt;요소에&gt;스크립트 요소(스크립트 및 /script)를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="7ee41-497">네 번째 인수를 사용하는 RegisterClientScriptBlock의 오버로드를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="7ee41-498">네 번째 인수는 ASP.NET 스크립트 요소를 추가해야 하는지 여부를 지정하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="7ee41-499">이 인수가 **true이면**스크립트에 스크립트 요소를 명시적으로 포함해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="7ee41-500">IsClientScriptBlock등록 메서드를 사용하여 스크립트가 이미 등록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="7ee41-501">이렇게 하면 이미 등록된 스크립트를 다시 등록하려는 시도를 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="7ee41-502">레지스터클라이언트스크립트포함(2.0의 새로운 것)</span><span class="sxs-lookup"><span data-stu-id="7ee41-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="7ee41-503">RegisterClientScriptInclude 태그는 외부 스크립트 파일에 연결되는 스크립트 블록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="7ee41-504">두 개의 오버로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-504">It has two overloads.</span></span> <span data-ttu-id="7ee41-505">하나는 키와 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-505">One takes a key and a URL.</span></span> <span data-ttu-id="7ee41-506">두 번째 인수는 형식을 지정하는 세 번째 인수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="7ee41-507">예를 들어 다음 코드는 응용 프로그램의 스크립트 폴더 루트에서 jsfunctions.js에 연결하는 스크립트 블록을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="7ee41-508">이 코드는 렌더링된 페이지에서 다음과 같은 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="7ee41-509">스크립트 블록은 페이지 하단에 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-509">The script block is rendered at the bottom of the page.</span></span>

<span data-ttu-id="7ee41-510">IsClientScriptInclude등록 된 방법을 사용하여 스크립트가 이미 등록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="7ee41-511">이렇게 하면 스크립트를 다시 등록하려는 시도를 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="7ee41-512">레지스터스타트업 스크립트</span><span class="sxs-lookup"><span data-stu-id="7ee41-512">RegisterStartupScript</span></span>

<span data-ttu-id="7ee41-513">RegisterStartupScript 메서드는 RegisterClientScriptBlock 메서드와 동일한 인수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="7ee41-514">RegisterStartupScript에 등록된 스크립트는 페이지로드 후하지만 OnLoad 클라이언트 측 이벤트 전에 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="7ee41-515">1.X에서 &lt;RegisterStartupScript에 등록된 스크립트는 닫기/양식&gt; 태그 바로 앞에 배치되었으며 RegisterClientScriptBlock에 등록된 &lt;&gt; 스크립트는 개구 양식 태그 바로 다음에 배치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="7ee41-516">ASP.NET 2.0에서는 둘 다 닫기 &lt;/form&gt; 태그 바로 앞에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="7ee41-517">RegisterStartupScript에 함수를 등록하면 클라이언트 쪽 코드에서 명시적으로 호출할 때까지 해당 함수가 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>

<span data-ttu-id="7ee41-518">IsStartupScript등록 메서드를 사용하여 스크립트가 이미 등록되었는지 확인하고 스크립트를 다시 등록하려는 시도를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="7ee41-519">기타 클라이언트스크립트관리자 방법</span><span class="sxs-lookup"><span data-stu-id="7ee41-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="7ee41-520">다음은 ClientScriptManager 클래스의 다른 유용한 방법 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>

|  <span data-ttu-id="7ee41-521"><strong>겟콜백이벤트</strong></span><span class="sxs-lookup"><span data-stu-id="7ee41-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="7ee41-522">이 모듈의 이전 스크립트 콜백을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7ee41-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="7ee41-523"><strong>겟포스트백클라이언트하이퍼링크</strong></span><span class="sxs-lookup"><span data-stu-id="7ee41-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="7ee41-524">클라이언트 측 이벤트에서 다시 게시하는 데 사용할 수 있는 JavaScript 참조(자바스크립트:&lt;호출)를&gt;가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="7ee41-525"><strong>겟포스트백이벤트참조</strong></span><span class="sxs-lookup"><span data-stu-id="7ee41-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="7ee41-526">클라이언트에서 다시 게시물을 시작하는 데 사용할 수 있는 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="7ee41-527"><strong>GetWebResourceUrl</strong></span><span class="sxs-lookup"><span data-stu-id="7ee41-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="7ee41-528">어셈블리에 포함된 리소스에 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="7ee41-529"><strong>RegisterClientScript리소스</strong>와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="7ee41-530"><strong>레지스터클라이언트스크립트리소스</strong></span><span class="sxs-lookup"><span data-stu-id="7ee41-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="7ee41-531">페이지에 웹 리소스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="7ee41-532">이러한 리소스는 어셈블리에 포함되고 새 WebResource.axd 처리기에서 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="7ee41-533"><strong>레지스터히든필드</strong></span><span class="sxs-lookup"><span data-stu-id="7ee41-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="7ee41-534">페이지에 숨겨진 양식 필드를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="7ee41-535"><strong>레지스터온제출서</strong></span><span class="sxs-lookup"><span data-stu-id="7ee41-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="7ee41-536">HTML 양식이 제출될 때 실행되는 클라이언트 쪽 코드를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7ee41-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |
