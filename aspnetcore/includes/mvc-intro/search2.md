---
ms.openlocfilehash: d5d902a2a6fcae3155c23d0040a8026ed5808dff
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047960"
---
<!--
[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Shared/_Layout.cshtml?highlight=7,31)]


[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull)]

![Index view](~/tutorials/first-mvc-app/search/_static/ghost.png)


[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]

--> 

<span data-ttu-id="dfb4a-101">위의 `Index` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-101">The previous `Index` method:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,8&name=snippet_1stSearch)]

<span data-ttu-id="dfb4a-102">`id` 매개 변수를 포함한 업데이트된 `Index` 메서드:</span><span class="sxs-lookup"><span data-stu-id="dfb4a-102">The updated `Index` method with `id` parameter:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,8&name=snippet_SearchID)]

<span data-ttu-id="dfb4a-103">이제 쿼리 문자열 값이 아닌 경로 데이터(URL 세그먼트)로 검색 제목을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-103">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![URL에 추가된 단어 ghost와 Ghostbusters 및 Ghostbusters 2라는 두 개의 반환된 영화 목록이 있는 인덱스 보기](~/tutorials/first-mvc-app/search/_static/g2.png)

<span data-ttu-id="dfb4a-105">그러나 사용자가 영화를 검색하려고 할 때마다 URL을 수정하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-105">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="dfb4a-106">따라서 이제 영화를 필터링하는 데 도움이 되는 UI 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-106">So now you'll add UI elements to help them filter movies.</span></span> <span data-ttu-id="dfb4a-107">`Index` 메서드의 서명을 변경하여 경로 바인딩 `ID` 매개 변수 전달 방법을 테스트하는 경우 `searchString`이라는 매개 변수를 사용하도록 다시 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-107">If you changed the signature of the `Index` method to test how to pass the route-bound `ID` parameter, change it back so that it takes a parameter named `searchString`:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_1stSearch)]

<span data-ttu-id="dfb4a-108">*Views/Movies/Index.cshtml* 파일을 열고 아래에서 강조 표시된 `<form>` 표시를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-108">Open the *Views/Movies/Index.cshtml* file, and add the `<form>` markup highlighted below:</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexForm1.cshtml?highlight=10-16&range=4-21)]

<span data-ttu-id="dfb4a-109">HTML `<form>` 태그는 [양식 태그 도우미](xref:mvc/views/working-with-forms)를 사용하므로 양식을 제출하는 경우 필터 문자열은 영화 컨트롤러의 `Index` 작업에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-109">The HTML `<form>` tag uses the [Form Tag Helper](xref:mvc/views/working-with-forms), so when you submit the form, the filter string is posted to the `Index` action of the movies controller.</span></span> <span data-ttu-id="dfb4a-110">변경 내용을 저장하고 필터를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-110">Save your changes and then test the filter.</span></span>

![제목 필터 텍스트 상자에 단어 ghost를 입력하여 인덱스 보기](~/tutorials/first-mvc-app/search/_static/filter.png)

<span data-ttu-id="dfb4a-112">예상할 수 있는 대로 `Index` 메서드의 `[HttpPost]` 오버로드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-112">There's no `[HttpPost]` overload of the `Index` method as you might expect.</span></span> <span data-ttu-id="dfb4a-113">메서드가 앱의 상태를 변경하지 않고 데이터를 필터링하기 때문에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-113">You don't need it, because the method isn't changing the state of the app, just filtering data.</span></span>

<span data-ttu-id="dfb4a-114">다음 `[HttpPost] Index` 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-114">You could add the following `[HttpPost] Index` method.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_SearchPost)]

<span data-ttu-id="dfb4a-115">`notUsed` 매개 변수는 `Index` 메서드의 오버로드를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-115">The `notUsed` parameter is used to create an overload for the `Index` method.</span></span> <span data-ttu-id="dfb4a-116">자습서의 뒷부분에서 이에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-116">We'll talk about that later in the tutorial.</span></span>

<span data-ttu-id="dfb4a-117">이 메서드를 추가하는 경우 작업 호출자는 `[HttpPost] Index` 메서드와 일치하고 `[HttpPost] Index` 메서드는 아래 이미지에 나와 있는 대로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-117">If you add this method, the action invoker would match the `[HttpPost] Index` method, and the `[HttpPost] Index` method would run as shown in the image below.</span></span>

![HttpPost 인덱스에서의 애플리케이션 응답을 포함한 브라우저 창: ghost에 대한 필터](~/tutorials/first-mvc-app/search/_static/fo.png)

<span data-ttu-id="dfb4a-119">그러나 이 `[HttpPost]` 버전의 `Index` 메서드를 추가하는 경우에도 이를 모두 구현하는 방법은 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-119">However, even if you add this `[HttpPost]` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="dfb4a-120">특정 검색을 책갈피로 설정하거나 동일하게 필터링된 영화 목록을 보기 위해 클릭할 수 있는 링크를 친구에게 보내려고 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-120">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="dfb4a-121">HTTP POST 요청의 URL은 GET 요청의 URL(localhost:xxxxx/Movies/Index)과 동일합니다. URL에는 검색 정보가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-121">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL.</span></span> <span data-ttu-id="dfb4a-122">검색 문자열 정보는 [양식 필드 값](https://developer.mozilla.org/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data)으로 서버에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-122">The search string information is sent to the server as a [form field value](https://developer.mozilla.org/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data).</span></span> <span data-ttu-id="dfb4a-123">브라우저 개발자 도구 또는 뛰어난 [Fiddler 도구](http://www.telerik.com/fiddler)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-123">You can verify that with the browser Developer tools or the excellent [Fiddler tool](http://www.telerik.com/fiddler).</span></span> <span data-ttu-id="dfb4a-124">아래 이미지에서는 Chrome 브라우저 개발자 도구를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-124">The image below shows the Chrome browser Developer tools:</span></span>

![Microsoft Edge에 있는 개발자 도구의 네트워크 탭은 ghost의 searchString 값을 가진 요청 본문을 보여줍니다.](~/tutorials/first-mvc-app/search/_static/f12_rb.png)

<span data-ttu-id="dfb4a-126">요청 본문에서 검색 매개 변수 및 [XSRF](xref:security/anti-request-forgery) 토큰을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-126">You can see the search parameter and [XSRF](xref:security/anti-request-forgery) token in the request body.</span></span> <span data-ttu-id="dfb4a-127">이전 자습서에서 설명했듯이 [양식 태그 도우미](xref:mvc/views/working-with-forms)는 [XSRF](xref:security/anti-request-forgery) 위조 방지 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-127">Note, as mentioned in the previous tutorial, the [Form Tag Helper](xref:mvc/views/working-with-forms) generates an [XSRF](xref:security/anti-request-forgery) anti-forgery token.</span></span> <span data-ttu-id="dfb4a-128">컨트롤러 메서드에서 토큰 유효성을 검사할 필요가 없도록 데이터를 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-128">We're not modifying data, so we don't need to validate the token in the controller method.</span></span>

<span data-ttu-id="dfb4a-129">검색 매개 변수가 URL이 아닌 요청 본문에 있기 때문에 책갈피에 해당 검색 정보를 캡처하거나 다른 사용자와 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-129">Because the search parameter is in the request body and not the URL, you can't capture that search information to bookmark or share with others.</span></span> <span data-ttu-id="dfb4a-130">요청을 `HTTP GET`로 지정하여 이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="dfb4a-130">We'll fix this by specifying the request should be `HTTP GET`.</span></span>
