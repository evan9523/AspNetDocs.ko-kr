---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET 웹 페이지 (Razor) API 빠른 참조 | Microsoft Docs
author: Rick-Anderson
description: 이 페이지에는 가장 일반적으로 사용 되는 개체, 속성 및 메서드를 Razor 구문 ASP.NET 웹 페이지 프로그래밍 하는 방법에 대 한 간단한 예가 포함 된 목록이 포함 되어 있습니다.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345252"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="97f0b-103">ASP.NET 웹 페이지 (Razor) API 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="97f0b-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>

<span data-ttu-id="97f0b-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="97f0b-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="97f0b-105">이 페이지에는 가장 일반적으로 사용 되는 개체, 속성 및 메서드를 Razor 구문 ASP.NET 웹 페이지 프로그래밍 하는 방법에 대 한 간단한 예가 포함 된 목록이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="97f0b-106">"(V2)"로 표시 된 설명은 ASP.NET 웹 페이지 버전 2에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="97f0b-107">API 참조 설명서는 MSDN에서 [ASP.NET 웹 페이지 참조 설명서](https://go.microsoft.com/fwlink/?LinkId=208659) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="97f0b-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="97f0b-108">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="97f0b-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="97f0b-109">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="97f0b-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="97f0b-110">이 자습서에서는 ASP.NET 웹 페이지 2 및 ASP.NET 웹 페이지 1.0 (v2로 표시 된 기능 제외) 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>

<span data-ttu-id="97f0b-111">이 페이지에는 다음에 대 한 참조 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="97f0b-112">클래스</span><span class="sxs-lookup"><span data-stu-id="97f0b-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="97f0b-113">Data</span><span class="sxs-lookup"><span data-stu-id="97f0b-113">Data</span></span>](#Data)
- [<span data-ttu-id="97f0b-114">도우미</span><span class="sxs-lookup"><span data-stu-id="97f0b-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="97f0b-115">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="97f0b-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="97f0b-116">클래스</span><span class="sxs-lookup"><span data-stu-id="97f0b-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="97f0b-117">응용 프로그램의 모든 페이지에서 공유할 수 있는 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="97f0b-118">`App`다음 예제와 같이 동적 속성을 사용 하 여 동일한 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="97f0b-119">문자열 값을 부울 값 (true/false)으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="97f0b-120">문자열이 true/false를 나타내지 않으면 false 또는 지정 된 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="97f0b-121">문자열 값을 날짜/시간으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-121">Converts a string value to date/time.</span></span> <span data-ttu-id="97f0b-122">`DateTime.MinValue`문자열이 날짜/시간을 나타내지 않는 경우 또는 지정 된 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="97f0b-123">문자열 값을 10 진수 값으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="97f0b-124">문자열이 10 진수 값을 나타내지 않는 경우 0.0 또는 지정 된 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="97f0b-125">문자열 값을 float로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-125">Converts a string value to a float.</span></span> <span data-ttu-id="97f0b-126">문자열이 10 진수 값을 나타내지 않는 경우 0.0 또는 지정 된 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="97f0b-127">문자열 값을 정수로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-127">Converts a string value to an integer.</span></span> <span data-ttu-id="97f0b-128">문자열이 정수를 나타내지 않는 경우 0을 반환 하거나 지정 된 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="97f0b-129">선택적 추가 경로 부분을 사용 하 여 로컬 파일 경로에서 브라우저 호환 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="97f0b-130">*값* 을 html로 인코딩된 출력으로 렌더링 하는 대신 html 태그로 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="97f0b-131">값을 문자열에서 지정 된 형식으로 변환할 수 있으면 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="97f0b-132">개체 또는 변수에 값이 없으면 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="97f0b-133">요청이 POST 인 경우 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="97f0b-134">초기 요청은 일반적으로 GET입니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="97f0b-135">이 페이지에 적용할 레이아웃 페이지의 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="97f0b-136">현재 요청의 페이지, 레이아웃 페이지 및 부분 페이지 간에 공유 되는 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="97f0b-137">`Page`다음 예제와 같이 동적 속성을 사용 하 여 동일한 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="97f0b-138">(레이아웃 페이지) 명명 된 섹션에 없는 콘텐츠 페이지의 콘텐츠를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="97f0b-139">지정 된 경로와 선택적 추가 데이터를 사용 하 여 콘텐츠 페이지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="97f0b-140">`PageData`위치 (예 1) 또는 키 (예 2)로에서 추가 매개 변수 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="97f0b-141">(레이아웃 페이지) 이름이 인 콘텐츠 섹션을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="97f0b-142">섹션을 선택 사항으로 만들려면 *필수* 를 false로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="97f0b-143">HTTP 쿠키의 값을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="97f0b-144">현재 요청에서 업로드 된 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="97f0b-145">형식 (문자열)으로 게시 된 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="97f0b-146">`Request[key]``Request.Form`및 컬렉션을 모두 검사 `Request.QueryString` 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="97f0b-147">URL 쿼리 문자열에 지정 된 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="97f0b-148">`Request[key]``Request.Form`및 컬렉션을 모두 검사 `Request.QueryString` 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="97f0b-149">Form 요소, 쿼리 문자열 값, 쿠키 또는 헤더 값에 대 한 요청 유효성 검사를 선택적으로 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="97f0b-150">요청 유효성 검사는 기본적으로 사용 하도록 설정 되어 있으므로 사용자가 태그 또는 기타 잠재적으로 위험한 콘텐츠를 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="97f0b-151">응답에 HTTP 서버 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="97f0b-152">지정 된 시간 동안 페이지 출력을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="97f0b-153">필요에 따라 *슬라이딩* 를 설정 하 여 각 페이지 액세스의 제한 시간을 다시 설정 하 고 페이지 요청에서 각 쿼리 문자열에 대해 서로 다른 버전의 페이지를 *varyByParams* 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="97f0b-154">브라우저 요청을 새 위치로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="97f0b-155">브라우저에 전송 되는 HTTP 상태 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="97f0b-156">선택적 MIME 형식을 사용 하 여 *데이터* 의 콘텐츠를 응답에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="97f0b-157">파일의 내용을 응답에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="97f0b-158">(레이아웃 페이지) 이름이 인 콘텐츠 섹션을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="97f0b-159">HTML로 인코딩된 문자열을 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="97f0b-160">HTML 태그에서 렌더링 하기 위해 문자열을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="97f0b-161">지정 된 가상 경로에 대 한 서버 실제 경로를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="97f0b-162">URL에서 텍스트를 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="97f0b-163">URL에 넣을 텍스트를 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="97f0b-164">사용자가 브라우저를 닫을 때까지 존재 하는 값을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="97f0b-165">개체의 값에 대 한 문자열 표현을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="97f0b-166">URL (예: */MyPage/ExtraData*)에서 추가 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="97f0b-167">지정한 사용자의 암호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="97f0b-168">계정 확인 토큰을 사용 하 여 계정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="97f0b-169">지정 된 사용자 이름 및 암호를 사용 하 여 새 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="97f0b-170">확인 토큰을 요구 하려면 RequireConfirmationToken에 대해 true를 전달 *합니다.*</span><span class="sxs-lookup"><span data-stu-id="97f0b-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="97f0b-171">현재 로그인 한 사용자의 정수 식별자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="97f0b-172">현재 로그인 한 사용자의 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="97f0b-173">사용자가 암호를 다시 설정할 수 있도록 사용자에 게 전자 메일로 보낼 수 있는 암호 다시 설정 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="97f0b-174">사용자 이름에서 사용자 ID를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="97f0b-175">현재 사용자가 로그인 한 경우 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="97f0b-176">사용자가 확인 된 경우 true를 반환 합니다 (예: 확인 전자 메일을 통해).</span><span class="sxs-lookup"><span data-stu-id="97f0b-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="97f0b-177">현재 사용자의 이름이 지정 된 사용자 이름과 일치 하면 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="97f0b-178">쿠키에 인증 토큰을 설정 하 여 사용자를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="97f0b-179">인증 토큰 쿠키를 제거 하 여 사용자를 로그 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="97f0b-180">사용자가 인증되지 않은 경우 HTTP 상태를 401(권한 없음)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="97f0b-181">현재 사용자가 지정 된 역할 중 하나의 멤버가 아닌 경우는 HTTP 상태를 401 (권한 없음)로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="97f0b-182">현재 사용자가 사용자 *이름*으로 지정 된 사용자가 아닌 경우는 HTTP 상태를 401 (권한 없음)로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="97f0b-183">암호 다시 설정 토큰이 유효한 경우에서 사용자의 암호를 새 암호로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="97f0b-184">데이터</span><span class="sxs-lookup"><span data-stu-id="97f0b-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="97f0b-185">INSERT, DELETE 또는 UPDATE와 같은 선택적 매개 변수를 사용 하 여 *SQLstatement* 를 실행 하 고 영향을 받는 레코드의 수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="97f0b-186">가장 최근에 삽입한 행에서 ID 열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="97f0b-187">지정 된 데이터베이스 파일 또는 *Web.config* 파일의 명명 된 연결 문자열을 사용 하 여 지정 된 데이터베이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="97f0b-188">연결 문자열을 사용 하 여 데이터베이스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-188">Opens a database using the connection string.</span></span> <span data-ttu-id="97f0b-189">이 `Database.Open` 는 연결 문자열 이름을 사용 하는와 대조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="97f0b-190">*SQLstatement* (필요에 따라 매개 변수를 전달)를 사용 하 여 데이터베이스를 쿼리하고 결과를 컬렉션으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="97f0b-191">선택적 매개 변수를 사용 하 여 *SQLstatement* 를 실행 하 고 단일 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="97f0b-192">선택적 매개 변수를 사용 하 여 *SQLstatement* 를 실행 하 고 단일 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="97f0b-193">도우미</span><span class="sxs-lookup"><span data-stu-id="97f0b-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="97f0b-194">지정 된 ID에 대 한 Google 분석 JavaScript 코드를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="97f0b-195">지정 된 프로젝트에 대 한 StatCounter Analytics JavaScript 코드를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="97f0b-196">지정 된 계정에 대 한 Yahoo Analytics JavaScript 코드를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="97f0b-197">검색을 Bing에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-197">Passes a search to Bing.</span></span> <span data-ttu-id="97f0b-198">검색할 사이트와 검색 상자의 제목을 지정 하려면 및 속성을 설정할 수 있습니다 `Bing.SiteUrl` `Bing.SiteTitle` .</span><span class="sxs-lookup"><span data-stu-id="97f0b-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="97f0b-199">일반적으로 \* \_ AppStart\* 페이지에서 이러한 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="97f0b-200">차트를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="97f0b-201">차트에 범례를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="97f0b-202">차트에 일련의 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="97f0b-203">지정 된 데이터에 대 한 해시를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="97f0b-204">기본 알고리즘은 `sha256` 입니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="97f0b-205">Facebook 사용자가 페이지에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="97f0b-206">파일 업로드를 위한 UI를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="97f0b-207">지정 된 Xbox 게이머 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="97f0b-208">지정 된 전자 메일 주소에 대 한 Gravatar 이미지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="97f0b-209">데이터 개체를 JSON (JavaScript Object Notation) 형식의 문자열로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="97f0b-210">JSON으로 인코딩된 입력 문자열을 반복 해 서 반복 하거나 데이터베이스에 삽입할 수 있는 데이터 개체로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="97f0b-211">지정 된 제목 및 선택적 URL을 사용 하 여 소셜 네트워킹 링크를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="97f0b-212">오류 메시지를 양식 필드와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-212">Associates an error message with a form field.</span></span> <span data-ttu-id="97f0b-213">도우미를 사용 `ModelState` 하 여이 멤버에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="97f0b-214">오류 메시지를 폼과 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-214">Associates an error message with a form.</span></span> <span data-ttu-id="97f0b-215">도우미를 사용 `ModelState` 하 여이 멤버에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="97f0b-216">유효성 검사 오류가 없으면 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="97f0b-217">도우미를 사용 `ModelState` 하 여이 멤버에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="97f0b-218">개체 및 모든 자식 개체의 속성 및 값을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="97f0b-219">ReCAPTCHA 확인 테스트를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="97f0b-220">ReCAPTCHA 서비스에 대 한 공개 키 및 개인 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="97f0b-221">일반적으로 \* \_ AppStart\* 페이지에서 이러한 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="97f0b-222">ReCAPTCHA 테스트의 결과를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="97f0b-223">ASP.NET 웹 페이지에 대 한 상태 정보를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="97f0b-224">지정 된 사용자에 대 한 Twitter 스트림을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="97f0b-225">지정 된 검색 텍스트에 대 한 Twitter 스트림을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="97f0b-226">지정 된 파일에 대해 선택적 너비와 높이를 사용 하 여 Flash 비디오 플레이어를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="97f0b-227">지정 된 파일에 대해 선택적 너비와 높이를 사용 하 여 Windows Media player를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="97f0b-228">지정 된 *.xap* 파일에 대해 필요한 너비와 높이를 사용 하 여 Silverlight 플레이어를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="97f0b-229">*키*로 지정 된 개체를 반환 하거나, 개체를 찾을 수 없는 경우 null을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="97f0b-230">*키* 로 지정 된 개체를 캐시에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="97f0b-231">*키*로 지정 된 이름으로 캐시에 *값* 을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="97f0b-232">`WebGrid`쿼리의 데이터를 사용 하 여 새 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="97f0b-233">HTML 테이블에 데이터를 표시 하는 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="97f0b-234">개체에 대 한 pager를 렌더링 `WebGrid` 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="97f0b-235">지정 된 경로에서 이미지를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="97f0b-236">지정 된 이미지를 워터 마크로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="97f0b-237">이미지에 지정 된 텍스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="97f0b-238">이미지를 가로 또는 세로로 대칭 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="97f0b-239">파일을 업로드 하는 동안 이미지를 페이지에 게시할 때 이미지를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="97f0b-240">이미지의 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="97f0b-241">이미지를 왼쪽 또는 오른쪽으로 회전 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="97f0b-242">이미지를 지정 된 경로에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="97f0b-243">SMTP 서버에 대 한 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="97f0b-244">일반적으로 \* \_ AppStart\* 페이지에서이 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="97f0b-245">이메일 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="97f0b-246">SMTP 서버 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-246">Sets the SMTP server name.</span></span> <span data-ttu-id="97f0b-247">일반적으로 \* \_ AppStart\* 페이지에서이 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-247">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="97f0b-248">SMTP 서버에 대 한 사용자 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="97f0b-249">일반적으로 \* \_ AppStart\* 페이지에서이 속성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="97f0b-250">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="97f0b-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="97f0b-251">[v2 지정 된 필드에 대 한 유효성 검사 오류 메시지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="97f0b-252">[v2 모든 유효성 검사 오류 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="97f0b-253">[v2 지정 된 형식의 유효성 검사에 대 한 사용자 입력 요소를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="97f0b-254">[v2 유효성 검사 오류 메시지의 형식을 지정할 수 있도록 클라이언트 쪽 유효성 검사에 대 한 CSS 클래스 특성을 동적으로 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="97f0b-255">를 사용 하려면 적절 한 클라이언트 스크립트 라이브러리를 참조 하 고 CSS 클래스를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="97f0b-256">[v2 사용자 입력 필드에 대 한 클라이언트 쪽 유효성 검사를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="97f0b-257">적절 한 클라이언트 스크립트 라이브러리를 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="97f0b-258">[v2 유효성 검사에 registred 된 모든 사용자 입력 요소에 유효한 값이 포함 된 경우 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="97f0b-259">[v2 사용자가 사용자 입력 요소에 대 한 값을 제공 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="97f0b-260">[v2 사용자가 각 사용자 입력 요소에 대 한 값을 제공 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="97f0b-261">이 방법을 사용 하면 사용자 지정 오류 메시지를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="97f0b-261">This method does not let you specify a custom error message.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

<span data-ttu-id="97f0b-262">[v2 메서드를 사용할 때 유효성 검사 테스트를 지정 합니다 `Validation.Add` .</span><span class="sxs-lookup"><span data-stu-id="97f0b-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
