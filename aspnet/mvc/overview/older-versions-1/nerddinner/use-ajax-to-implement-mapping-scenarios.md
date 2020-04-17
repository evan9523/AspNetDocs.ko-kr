---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: AJAX를 사용하여 매핑 시나리오 구현 | 마이크로 소프트 문서
author: rick-anderson
description: 11단계는 AJAX 매핑 지원을 NerdDinner 애플리케이션에 통합하는 방법을 보여 주며, 저녁 식사를 만들거나 편집하거나 보는 사용자가 저녁 식사를 볼 수 있도록 합니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f2e2640eb421d5ee8006915f46cbe1090b8d21ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542588"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a><span data-ttu-id="6b562-103">AJAX를 사용하여 매핑 시나리오 구현</span><span class="sxs-lookup"><span data-stu-id="6b562-103">Use AJAX to Implement Mapping Scenarios</span></span>

<span data-ttu-id="6b562-104">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6b562-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="6b562-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="6b562-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="6b562-106">이것은 MVC 1을 ASP.NET 사용하여 작지만 완전한 웹 응용 프로그램을 빌드하는 방법을 안내하는 무료 ["NerdDinner" 응용 프로그램 자습서의](introducing-the-nerddinner-tutorial.md) 11단계입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-106">This is step 11 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="6b562-107">11단계는 AJAX 매핑 지원을 NerdDinner 응용 프로그램에 통합하는 방법을 보여 주며, 저녁 식사를 만들거나 편집하거나 보는 사용자가 저녁 식사의 위치를 그래픽으로 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-107">Step 11 shows how to integrate AJAX mapping support into our NerdDinner application, enabling users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>
> 
> <span data-ttu-id="6b562-108">MVC 3을 ASP.NET 사용하는 경우 [MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC 뮤직 스토어](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a><span data-ttu-id="6b562-109">얼간이 디너 단계 11: AJAX 맵 통합</span><span class="sxs-lookup"><span data-stu-id="6b562-109">NerdDinner Step 11: Integrating an AJAX Map</span></span>

<span data-ttu-id="6b562-110">이제 AJAX 매핑 지원을 통합하여 응용 프로그램을 좀 더 시각적으로 흥미롭게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-110">We'll now make our application a little more visually exciting by integrating AJAX mapping support.</span></span> <span data-ttu-id="6b562-111">이렇게 하면 저녁 식사를 만들거나 편집하거나 보는 사용자가 저녁 식사 의 위치를 그래픽으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-111">This will enable users who are creating, editing or viewing dinners to see the location of the dinner graphically.</span></span>

### <a name="creating-a-map-partial-view"></a><span data-ttu-id="6b562-112">맵 부분 뷰 작성</span><span class="sxs-lookup"><span data-stu-id="6b562-112">Creating a Map Partial View</span></span>

<span data-ttu-id="6b562-113">응용 프로그램 내의 여러 위치에서 매핑 기능을 사용할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-113">We are going to use mapping functionality in several places within our application.</span></span> <span data-ttu-id="6b562-114">코드를 DRY로 유지하기 위해 여러 컨트롤러 작업 및 뷰에서 다시 사용할 수 있는 단일 부분 템플릿 내에서 공통 맵 기능을 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-114">To keep our code DRY we'll encapsulate the common map functionality within a single partial template that we can re-use across multiple controller actions and views.</span></span> <span data-ttu-id="6b562-115">이 부분 뷰의 이름을 "map.ascx"로 지정하고 \View\Dinners 디렉토리 내에서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-115">We'll name this partial view "map.ascx" and create it within the \Views\Dinners directory.</span></span>

<span data-ttu-id="6b562-116">\View\Dinners 디렉토리를 마우스 오른쪽 단추로 클릭하고 추가&gt;보기 메뉴 명령을 선택하여 map.ascx 부분작성을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-116">We can create the map.ascx partial by right-clicking on the \Views\Dinners directory and choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="6b562-117">"Map.ascx" 뷰의 이름을 지정하고 부분 보기로 확인하고 강력한 형식의 "Dinner" 모델 클래스를 전달할 것임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-117">We'll name the view "Map.ascx", check it as a partial view, and indicate that we are going to pass it a strongly-typed "Dinner" model class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

<span data-ttu-id="6b562-118">"추가" 버튼을 클릭하면 부분 템플릿이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-118">When we click the "Add" button our partial template will be created.</span></span> <span data-ttu-id="6b562-119">그런 다음 Map.ascx 파일을 업데이트하여 다음 내용을 갖도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-119">We'll then update the Map.ascx file to have the following content:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

<span data-ttu-id="6b562-120">첫 &lt;번째&gt; 스크립트 참조는 Microsoft 가상 어스 6.2 매핑 라이브러리를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-120">The first &lt;script&gt; reference points to the Microsoft Virtual Earth 6.2 mapping library.</span></span> <span data-ttu-id="6b562-121">두 &lt;번째&gt; 스크립트 참조는 곧 만들 것입니다 map.js 파일을 가리키며 일반적인 자바 스크립트 매핑 논리를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-121">The second &lt;script&gt; reference points to a map.js file that we will shortly create which will encapsulate our common Javascript mapping logic.</span></span> <span data-ttu-id="6b562-122">&lt;div id="theMap"&gt; 요소는 가상 지구가 맵을 호스트하는 데 사용하는 HTML 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-122">The &lt;div id="theMap"&gt; element is the HTML container that Virtual Earth will use to host the map.</span></span>

<span data-ttu-id="6b562-123">그런 다음 이 &lt;&gt; 보기와 관련된 두 개의 JavaScript 함수를 포함하는 포함된 스크립트 블록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-123">We then have an embedded &lt;script&gt; block that contains two JavaScript functions specific to this view.</span></span> <span data-ttu-id="6b562-124">첫 번째 함수는 jQuery를 사용하여 페이지가 클라이언트 측 스크립트를 실행할 준비가 되면 실행되는 함수를 와이어업합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-124">The first function uses jQuery to wire-up a function that executes when the page is ready to run client-side script.</span></span> <span data-ttu-id="6b562-125">Map.js 스크립트 파일 내에서 가상 토지 맵 컨트롤을 로드하기 위해 정의할 LoadMap() 도우미 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-125">It calls a LoadMap() helper function that we'll define within our Map.js script file to load the virtual earth map control.</span></span> <span data-ttu-id="6b562-126">두 번째 함수는 위치를 식별하는 맵에 핀을 추가하는 콜백 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-126">The second function is a callback event handler that adds a pin to the map that identifies a location.</span></span>

<span data-ttu-id="6b562-127">클라이언트 측 스크립트 블록 내에서 &lt;서버&gt; 측 %= % 블록을 사용하여 JavaScript에 매핑하려는 Dinner의 위도와 경도를 포함하려는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-127">Notice how we are using a server-side &lt;%= %&gt; block within the client-side script block to embed the latitude and longitude of the Dinner we want to map into the JavaScript.</span></span> <span data-ttu-id="6b562-128">이 방법은 클라이언트 측 스크립트에서 사용할 수 있는 동적 값을 출력하는 데 유용한 기술입니다(값을 검색하기 위해 서버에 별도의 AJAX 호출을 요구하지 않고) 더 빠르게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-128">This is a useful technique to output dynamic values that can be used by client-side script (without requiring a separate AJAX call back to the server to retrieve the values – which makes it faster).</span></span> <span data-ttu-id="6b562-129">뷰가 &lt;서버에서 렌더링될 때 %= %&gt; 블록이 실행되므로 HTML의 출력은 포함된 JavaScript 값(예: var 위도 = 47.64312;)으로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-129">The &lt;%= %&gt; blocks will execute when the view is rendering on the server – and so the output of the HTML will just end up with embedded JavaScript values (for example: var latitude = 47.64312;).</span></span>

### <a name="creating-a-mapjs-utility-library"></a><span data-ttu-id="6b562-130">Map.js 유틸리티 라이브러리 만들기</span><span class="sxs-lookup"><span data-stu-id="6b562-130">Creating a Map.js utility library</span></span>

<span data-ttu-id="6b562-131">이제 맵에 대한 JavaScript 기능을 캡슐화하는 데 사용할 수 있는 Map.js 파일을 만들고 위의 LoadMap 및 LoadPin 메서드를 구현해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-131">Let's now create the Map.js file that we can use to encapsulate the JavaScript functionality for our map (and implement the LoadMap and LoadPin methods above).</span></span> <span data-ttu-id="6b562-132">프로젝트 내의 \Scripts 디렉터리를 마우스 오른쪽 단추로 클릭하여&gt;"새 항목 추가" 메뉴 명령을 선택하고 JScript 항목을 선택하고 이름을 "Map.js"로 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-132">We can do this by right-clicking on the \Scripts directory within our project, and then choose the "Add-&gt;New Item" menu command, select the JScript item, and name it "Map.js".</span></span>

<span data-ttu-id="6b562-133">다음은 가상 지구와 상호 작용하는 Map.js 파일에 추가할 JavaScript 코드로, 맵을 표시하고 저녁 식사를 위해 위치 핀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-133">Below is the JavaScript code we'll add to the Map.js file that will interact with Virtual Earth to display our map and add locations pins to it for our dinners:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a><span data-ttu-id="6b562-134">양식 작성 및 편집과 맵 통합</span><span class="sxs-lookup"><span data-stu-id="6b562-134">Integrating the Map with Create and Edit Forms</span></span>

<span data-ttu-id="6b562-135">이제 맵 지원을 기존 만들기 및 편집 시나리오와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-135">We'll now integrate the Map support with our existing Create and Edit scenarios.</span></span> <span data-ttu-id="6b562-136">좋은 소식은 이것이 매우 쉽게 할 수 있으며 컨트롤러 코드를 변경할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-136">The good news is that this is pretty easy to-do, and doesn't require us to change any of our Controller code.</span></span> <span data-ttu-id="6b562-137">만들기 및 편집 보기는 공통 "DinnerForm" 부분 보기를 공유하여 dinner 양식 UI를 구현하기 때문에 맵을 한 곳에 추가하고 만들기 및 편집 시나리오를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-137">Because our Create and Edit views share a common "DinnerForm" partial view to implement the dinner form UI, we can add the map in one place and have both our Create and Edit scenarios use it.</span></span>

<span data-ttu-id="6b562-138">우리가해야 할 일은 \View\Dinners\DinnerForm.ascx 부분 보기를 열고 새 맵을 부분적으로 포함하도록 업데이트하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-138">All we need to-do is to open the \Views\Dinners\DinnerForm.ascx partial view and update it to include our new map partial.</span></span> <span data-ttu-id="6b562-139">다음은 맵이 추가되면 업데이트된 DinnerForm의 모양입니다(참고: HTML 양식 요소는 간결하게 하기 위해 아래 코드 조각에서 생략됨).</span><span class="sxs-lookup"><span data-stu-id="6b562-139">Below is what the updated DinnerForm will look like once the map is added (note: the HTML form elements are omitted from the code snippet below for brevity):</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

<span data-ttu-id="6b562-140">위의 DinnerForm 부분 형식은 "DinnerFormViewModel" 형식의 개체를 모델 유형으로 사용합니다(국가 드롭다운 목록을 채우기 위해 Dinner 개체와 SelectList가 모두 필요하기 때문입니다).</span><span class="sxs-lookup"><span data-stu-id="6b562-140">The DinnerForm partial above takes an object of type "DinnerFormViewModel" as its model type (because it needs both a Dinner object, as well as a SelectList to populate the dropdownlist of countries).</span></span> <span data-ttu-id="6b562-141">우리의지도 부분 단지 의 객체를 필요로 "Dinner" 그 모델 유형으로, 그래서 우리는 맵 부분을 렌더링 할 때 우리는 DinnerFormViewModel의 저녁 식사 하위 속성을 전달합니다 :</span><span class="sxs-lookup"><span data-stu-id="6b562-141">Our Map partial just needs an object of type "Dinner" as its model type, and so when we render the map partial we are passing just the Dinner sub-property of DinnerFormViewModel to it:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

<span data-ttu-id="6b562-142">부분적으로 추가된 JavaScript 함수는 jQuery를 사용하여 "주소" HTML 텍스트 상자에 "흐림" 이벤트를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-142">The JavaScript function we've added to the partial uses jQuery to attach a "blur" event to the "Address" HTML textbox.</span></span> <span data-ttu-id="6b562-143">사용자가 텍스트 상자를 클릭하거나 탭할 때 발생되는 "포커스" 이벤트에 대해 들어본 적이 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-143">You've probably heard of "focus" events that fire when a user clicks or tabs into a textbox.</span></span> <span data-ttu-id="6b562-144">반대는 사용자가 텍스트 상자를 종료할 때 발생 하는 "흐림" 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-144">The opposite is a "blur" event that fires when a user exits a textbox.</span></span> <span data-ttu-id="6b562-145">위의 이벤트 처리기는 위도 및 경도 텍스트 상자 값을 지우고 맵에 새 주소 위치를 플로팅합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-145">The above event handler clears the latitude and longitude textbox values when this happens, and then plots the new address location on our map.</span></span> <span data-ttu-id="6b562-146">map.js 파일 내에서 정의한 콜백 이벤트 처리기는 우리가 제공한 주소에 따라 가상 지구에서 반환되는 값을 사용하여 양식의 경도 및 위도 텍스트 상자를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-146">A callback event handler that we defined within the map.js file will then update the longitude and latitude textboxes on our form using values returned by virtual earth based on the address we gave it.</span></span>

<span data-ttu-id="6b562-147">이제 응용 프로그램을 다시 실행하고 "호스트 저녁 식사" 탭을 클릭하면 표준 Dinner 양식 요소와 함께 표시되는 기본 맵이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-147">And now when we run our application again and click the "Host Dinner" tab we'll see a default map displayed along with our standard Dinner form elements:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

<span data-ttu-id="6b562-148">주소를 입력한 다음 탭을 멀리 하면 맵이 동적으로 업데이트되어 위치를 표시하고 이벤트 처리기가 위도/경도 텍스트 상자를 위치 값으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-148">When we type in an address, and then tab away, the map will dynamically update to display the location, and our event handler will populate the latitude/longitude textboxes with the location values:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

<span data-ttu-id="6b562-149">새 저녁 식사를 저장한 다음 편집을 위해 다시 열면 페이지가 로드될 때 맵 위치가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-149">If we save the new dinner and then open it again for editing, we'll find that the map location is displayed when the page loads:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

<span data-ttu-id="6b562-150">주소 필드가 변경될 때마다 맵과 위도/경도 좌표가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-150">Every time the address field is changed, the map and the latitude/longitude coordinates will update.</span></span>

<span data-ttu-id="6b562-151">이제 맵에 Dinner 위치가 표시되므로 위도 및 경도 양식 필드를 표시되는 텍스트 상자에서 대신 숨겨진 요소로 변경할 수 있습니다(맵이 주소를 입력할 때마다 자동으로 업데이트되므로).</span><span class="sxs-lookup"><span data-stu-id="6b562-151">Now that the map displays the Dinner location, we can also change the Latitude and Longitude form fields from being visible textboxes to instead be hidden elements (since the map is automatically updating them each time an address is entered).</span></span> <span data-ttu-id="6b562-152">이 작업을 수행하려면 Html.TextBox() HTML 도우미를 사용하여 Html.Hidden() 도우미 메서드를 사용하는 것으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-152">To-do this we'll switch from using the Html.TextBox() HTML helper to using the Html.Hidden() helper method:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

<span data-ttu-id="6b562-153">그리고 이제 우리의 양식은 좀 더 사용자 친화적이며 원시 위도 / 경도를 표시하지 마십시오 (데이터베이스에있는 각 Dinner와 함께 저장하는 동안).</span><span class="sxs-lookup"><span data-stu-id="6b562-153">And now our forms are a little more user-friendly and avoid displaying the raw latitude/longitude (while still storing them with each Dinner in the database):</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a><span data-ttu-id="6b562-154">세부 정보 뷰와 맵 통합</span><span class="sxs-lookup"><span data-stu-id="6b562-154">Integrating the Map with the Details View</span></span>

<span data-ttu-id="6b562-155">이제 맵을 만들기 및 편집 시나리오와 통합되었으므로 세부 정보 시나리오와 통합해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-155">Now that we have the map integrated with our Create and Edit scenarios, let's also integrate it with our Details scenario.</span></span> <span data-ttu-id="6b562-156">우리가해야 할 일은 % &lt;Html.RenderPartial ("지도")를 호출하는 것입니다. 세부&gt; 정보 보기 내에서 %.</span><span class="sxs-lookup"><span data-stu-id="6b562-156">All we need to-do is to call &lt;% Html.RenderPartial("map"); %&gt; within the Details view.</span></span>

<span data-ttu-id="6b562-157">다음은 전체 세부 정보 보기(맵 통합)의 소스 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-157">Below is what the source code to the complete Details view (with map integration) looks like:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

<span data-ttu-id="6b562-158">그리고 이제 사용자가 /Dinners/Details/[id] URL로 이동하면 저녁 식사에 대한 세부 정보, 지도에서 저녁 식사 위치(마우스를 가져가면 저녁 식사 제목과 주소가 표시되는 푸시 핀이 있음)가 표시되고 RSVP에 대한 AJAX 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-158">And now when a user navigates to a /Dinners/Details/[id] URL they'll see details about the dinner, the location of the dinner on the map (complete with a push-pin that when hovered over displays the title of the dinner and the address of it), and have an AJAX link to RSVP for it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a><span data-ttu-id="6b562-159">데이터베이스 및 리포지토리에서 위치 검색 구현</span><span class="sxs-lookup"><span data-stu-id="6b562-159">Implementing Location Search in our Database and Repository</span></span>

<span data-ttu-id="6b562-160">AJAX 구현을 완료하려면 사용자가 근처의 저녁 식사를 그래픽으로 검색할 수 있는 응용 프로그램의 홈 페이지에 맵을 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-160">To finish off our AJAX implementation, let's add a Map to the home page of the application that allows users to graphically search for dinners near them.</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

<span data-ttu-id="6b562-161">먼저 데이터베이스 및 데이터 리포지토리 계층 내에서 지원을 구현하여 Dinners에 대한 위치 기반 반경 검색을 효율적으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-161">We'll begin by implementing support within our database and data repository layer to efficiently perform a location-based radius search for Dinners.</span></span> <span data-ttu-id="6b562-162">[SQL 2008의](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) 새로운 지리 공간 기능을 사용하여 이를 구현하거나, 게리 드라이든이 여기에서 설명한 SQL 함수 [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) 접근 방식을 사용할 수도 있습니다.[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span><span class="sxs-lookup"><span data-stu-id="6b562-162">We could use the new [geospatial features of SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) to implement this, or alternatively we can use a SQL function approach that Gary Dryden discussed in article here: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) and Rob Conery blogged about using with LINQ to SQL here: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)</span></span>

<span data-ttu-id="6b562-163">이 기술을 구현하려면 Visual Studio 내에서 "서버 탐색기"를 열고 NerdDinner 데이터베이스를 선택한 다음 그 아래에 있는 "함수" 하위 노드를 마우스 오른쪽 단추로 클릭하고 새 "스칼라 값 함수"를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-163">To implement this technique, we will open the "Server Explorer" within Visual Studio, select the NerdDinner database, and then right-click on the "functions" sub-node under it and choose to create a new "Scalar-valued function":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

<span data-ttu-id="6b562-164">그런 다음 다음 DistanceBetween 함수에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-164">We'll then paste in the following DistanceBetween function:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

<span data-ttu-id="6b562-165">그런 다음 SQL Server에서 "가장 가까운 Dinners"라고 하는 새 테이블 값 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-165">We'll then create a new table-valued function in SQL Server that we'll call "NearestDinners":</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

<span data-ttu-id="6b562-166">이 "가장 가까운 Dinners" 테이블 함수는 DistanceBetween 도우미 기능을 사용하여 위도와 경도에서 100마일 이내에 있는 모든 Dinners를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-166">This "NearestDinners" table function uses the DistanceBetween helper function to return all Dinners within 100 miles of the latitude and longitude we supply it:</span></span>

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

<span data-ttu-id="6b562-167">이 함수를 호출하려면 먼저 \Model 디렉토리 에서 NerdDinner.dbml 파일을 두 번 클릭하여 LINQ를 SQL 디자이너에 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-167">To call this function, we'll first open up the LINQ to SQL designer by double-clicking on the NerdDinner.dbml file within our \Models directory:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

<span data-ttu-id="6b562-168">그런 다음 가장 가까운 Dinners 및 DistanceBetween 함수를 LINQ에서 SQL 디자이너로 끌어 이동하여 LINQ에서 SQL NerdDinnerDataContext 클래스에 대한 메서드로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-168">We'll then drag the NearestDinners and DistanceBetween functions onto the LINQ to SQL designer, which will cause them to be added as methods on our LINQ to SQL NerdDinnerDataContext class:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

<span data-ttu-id="6b562-169">그런 다음 가장 가까운 Dinner 함수를 사용하여 지정된 위치에서 100 마일 이내에있는 예정된 Dinners를 반환하는 DinnerRepository 클래스에 "FindByLocation" 쿼리 메서드를 노출 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-169">We can then expose a "FindByLocation" query method on our DinnerRepository class that uses the NearestDinner function to return upcoming Dinners that are within 100 miles of the specified location:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a><span data-ttu-id="6b562-170">JSON 기반 AJAX 검색 작업 방법 구현</span><span class="sxs-lookup"><span data-stu-id="6b562-170">Implementing a JSON-based AJAX Search Action Method</span></span>

<span data-ttu-id="6b562-171">이제 새로운 FindByLocation() 리포지토리 메서드를 활용하여 맵을 채우는 데 사용할 수 있는 Dinner 데이터 목록을 반환하는 컨트롤러 작업 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-171">We'll now implement a controller action method that takes advantage of the new FindByLocation() repository method to return back a list of Dinner data that can be used to populate a map.</span></span> <span data-ttu-id="6b562-172">이 작업 메서드는 클라이언트에서 자바 스크립트를 사용하여 쉽게 조작 할 수 있도록 JSON (자바 스크립트 개체 표기법) 형식으로 Dinner 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-172">We'll have this action method return back the Dinner data in a JSON (JavaScript Object Notation) format so that it can be easily manipulated using JavaScript on the client.</span></span>

<span data-ttu-id="6b562-173">이를 구현하기 위해 \Controllers 디렉터리를 마우스 오른쪽 단추로 클릭하고 컨트롤러 추가&gt;메뉴 명령을 선택하여 새 "SearchController" 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-173">To implement this, we'll create a new "SearchController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span> <span data-ttu-id="6b562-174">그런 다음 다음과 같은 새 SearchController 클래스 내에서 "SearchByLocation" 작업 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-174">We'll then implement a "SearchByLocation" action method within the new SearchController class like below:</span></span>

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

<span data-ttu-id="6b562-175">SearchController의 SearchByLocation 작업 메서드는 내부적으로 DinnerRepository에서 FindByLocation 메서드를 호출하여 근처 저녁 식사 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-175">The SearchController's SearchByLocation action method internally calls the FindByLocation method on DinnerRepository to get a list of nearby dinners.</span></span> <span data-ttu-id="6b562-176">그러나 Dinner 개체를 클라이언트에 직접 반환하는 대신 JsonDinner 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-176">Rather than return the Dinner objects directly to the client, though, it instead returns JsonDinner objects.</span></span> <span data-ttu-id="6b562-177">JsonDinner 클래스는 Dinner 속성의 하위 집합을 노출합니다(예: 보안상의 이유로 저녁 식사에 RSVP가 있는 사람의 이름은 공개하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="6b562-177">The JsonDinner class exposes a subset of Dinner properties (for example: for security reasons it doesn't disclose the names of the people who have RSVP'd for a dinner).</span></span> <span data-ttu-id="6b562-178">또한 Dinner에 존재하지 않는 RSVPCount 속성이 포함되어 있으며 특정 저녁 식사와 관련된 RSVP 개체 수를 계산하여 동적으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-178">It also includes an RSVPCount property that doesn't exist on Dinner– and which is dynamically calculated by counting the number of RSVP objects associated with a particular dinner.</span></span>

<span data-ttu-id="6b562-179">그런 다음 컨트롤러 기본 클래스의 Json() 도우미 메서드를 사용하여 JSON 기반 와이어 형식을 사용하여 저녁 식사 시퀀스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-179">We are then using the Json() helper method on the Controller base class to return the sequence of dinners using a JSON-based wire format.</span></span> <span data-ttu-id="6b562-180">JSON은 간단한 데이터 구조를 나타내는 표준 텍스트 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-180">JSON is a standard text format for representing simple data-structures.</span></span> <span data-ttu-id="6b562-181">다음은 두 JsonDinner 개체의 JSON 형식 목록이 작업 메서드에서 반환될 때 어떻게 보이는지 에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-181">Below is an example of what a JSON-formatted list of two JsonDinner objects looks like when returned from our action method:</span></span>

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a><span data-ttu-id="6b562-182">jQuery를 사용하여 JSON 기반 AJAX 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="6b562-182">Calling the JSON-based AJAX method using jQuery</span></span>

<span data-ttu-id="6b562-183">이제 SearchController의 SearchByLocation 작업 방법을 사용 하 여 NerdDinner 응용 프로그램의 홈 페이지를 업데이트할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-183">We are now ready to update the home page of the NerdDinner application to use the SearchController's SearchByLocation action method.</span></span> <span data-ttu-id="6b562-184">이렇게하려면 / 보기 / 홈 / Index.aspx보기 템플릿을 열고 텍스트 상자, 검색 버튼, 지도 및 &lt;dinnerList라는 div 요소를 갖도록 업데이트합니다.&gt;</span><span class="sxs-lookup"><span data-stu-id="6b562-184">To-do this, we'll open the /Views/Home/Index.aspx view template and update it to have a textbox, search button, our map, and a &lt;div&gt; element named dinnerList:</span></span>

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

<span data-ttu-id="6b562-185">그런 다음 페이지에 두 개의 JavaScript 함수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-185">We can then add two JavaScript functions to the page:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

<span data-ttu-id="6b562-186">첫 번째 JavaScript 함수는 페이지가 처음 로드될 때 맵을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-186">The first JavaScript function loads the map when the page first loads.</span></span> <span data-ttu-id="6b562-187">두 번째 JavaScript 함수는 검색 버튼에서 JavaScript 클릭 이벤트 처리기를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-187">The second JavaScript function wires up a JavaScript click event handler on the search button.</span></span> <span data-ttu-id="6b562-188">버튼을 누르면 FindDinnersGivenLocation() 자바 스크립트 함수를 호출하여 Map.js 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-188">When the button is pressed it calls the FindDinnersGivenLocation() JavaScript function which we'll add to our Map.js file:</span></span>

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

<span data-ttu-id="6b562-189">이 FindDinners주어진위치() 함수는 맵을 호출합니다. () 가상 지구 제어에서 입력한 위치에 중앙을 위치하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-189">This FindDinnersGivenLocation() function calls map.Find() on the Virtual Earth Control to center it on the entered location.</span></span> <span data-ttu-id="6b562-190">가상 지구 맵 서비스가 반환되면 맵이 반환됩니다. Find() 메서드는 콜백UpdateMapDinners 콜백 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-190">When the virtual earth map service returns, the map.Find() method invokes the callbackUpdateMapDinners callback method we passed it as the final argument.</span></span>

<span data-ttu-id="6b562-191">콜백UpdateMapDinners() 메서드는 실제 작업이 수행되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-191">The callbackUpdateMapDinners() method is where the real work is done.</span></span> <span data-ttu-id="6b562-192">그것은 jQuery의 $.post() 도우미 메서드를 사용 하 여 우리의 SearchController의 SearchByLocation() 작업 메서드에 AJAX 호출을 수행-그것을 전달 하 고 새로 중심된 지도의 경도.</span><span class="sxs-lookup"><span data-stu-id="6b562-192">It uses jQuery's $.post() helper method to perform an AJAX call to our SearchController's SearchByLocation() action method – passing it the latitude and longitude of the newly centered map.</span></span> <span data-ttu-id="6b562-193">$.post() 도우미 메서드가 완료될 때 호출되는 인라인 함수를 정의하고 SearchByLocation() 작업 메서드에서 반환된 JSON 형식의 저녁 식사 결과는 "dinners"라는 변수를 사용하여 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-193">It defines an inline function that will be called when the $.post() helper method completes, and the JSON-formatted dinner results returned from the SearchByLocation() action method will be passed it using a variable called "dinners".</span></span> <span data-ttu-id="6b562-194">그런 다음 반환된 각 저녁 식사에 대해 foreach를 수행하고 저녁 식사의 위도와 경도 및 기타 속성을 사용하여 지도에 새 핀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-194">It then does a foreach over each returned dinner, and uses the dinner's latitude and longitude and other properties to add a new pin on the map.</span></span> <span data-ttu-id="6b562-195">또한 지도 오른쪽에 있는 저녁 식사의 HTML 목록에 저녁 식사 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-195">It also adds a dinner entry to the HTML list of dinners to the right of the map.</span></span> <span data-ttu-id="6b562-196">그런 다음 푸시핀과 HTML 목록에 대해 호버 이벤트를 연결하여 사용자가 마우스를 가져가면 저녁 식사에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-196">It then wires-up a hover event for both the pushpins and the HTML list so that details about the dinner are displayed when a user hovers over them:</span></span>

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

<span data-ttu-id="6b562-197">그리고 지금 우리가 응용 프로그램을 실행하고 홈 페이지를 방문 할 때 우리는지도가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-197">And now when we run the application and visit the home-page we'll be presented with a map.</span></span> <span data-ttu-id="6b562-198">도시의 이름을 입력하면 지도에 다가오는 저녁 식사가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-198">When we enter the name of a city the map will display the upcoming dinners near it:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

<span data-ttu-id="6b562-199">저녁 식사 위에 마우스를 가져가면 자세한 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-199">Hovering over a dinner will display details about it.</span></span>

<span data-ttu-id="6b562-200">거품이나 HTML 목록의 오른쪽에 있는 Dinner 제목을 클릭하면 저녁 식사로 이동하여 선택적으로 RSVP를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-200">Clicking the Dinner title either in the bubble or on the right-hand side in the HTML list will navigate us to the dinner – which we can then optionally RSVP for:</span></span>

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a><span data-ttu-id="6b562-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b562-201">Next Step</span></span>

<span data-ttu-id="6b562-202">이제 NerdDinner 응용 프로그램의 모든 응용 프로그램 기능을 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-202">We've now implemented all the application functionality of our NerdDinner application.</span></span> <span data-ttu-id="6b562-203">이제 자동화된 단위 테스트를 활성화하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b562-203">Let's now look at how we can enable automated unit testing of it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6b562-204">[이전](use-ajax-to-deliver-dynamic-updates.md)
> [다음](enable-automated-unit-testing.md)</span><span class="sxs-lookup"><span data-stu-id="6b562-204">[Previous](use-ajax-to-deliver-dynamic-updates.md)
[Next](enable-automated-unit-testing.md)</span></span>
