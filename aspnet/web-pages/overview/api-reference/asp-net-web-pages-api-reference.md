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
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET 웹 페이지 (Razor) API 빠른 참조

[Tom FitzMacken](https://github.com/tfitzmac)

> 이 페이지에는 가장 일반적으로 사용 되는 개체, 속성 및 메서드를 Razor 구문 ASP.NET 웹 페이지 프로그래밍 하는 방법에 대 한 간단한 예가 포함 된 목록이 포함 되어 있습니다.
> 
> "(V2)"로 표시 된 설명은 ASP.NET 웹 페이지 버전 2에서 도입 되었습니다.
> 
> API 참조 설명서는 MSDN에서 [ASP.NET 웹 페이지 참조 설명서](https://go.microsoft.com/fwlink/?LinkId=208659) 를 참조 하세요.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서에서는 ASP.NET 웹 페이지 2 및 ASP.NET 웹 페이지 1.0 (v2로 표시 된 기능 제외) 에서도 작동 합니다.

이 페이지에는 다음에 대 한 참조 정보가 포함 되어 있습니다.

- [클래스](#Classes)
- [Data](#Data)
- [도우미](#Helpers)
- [유효성 검사](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>클래스

### `AppState[key], AppState[index],App`

응용 프로그램의 모든 페이지에서 공유할 수 있는 데이터를 포함 합니다. `App`다음 예제와 같이 동적 속성을 사용 하 여 동일한 데이터에 액세스할 수 있습니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

문자열 값을 부울 값 (true/false)으로 변환 합니다. 문자열이 true/false를 나타내지 않으면 false 또는 지정 된 값을 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

문자열 값을 날짜/시간으로 변환 합니다. `DateTime.MinValue`문자열이 날짜/시간을 나타내지 않는 경우 또는 지정 된 값을 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

문자열 값을 10 진수 값으로 변환 합니다. 문자열이 10 진수 값을 나타내지 않는 경우 0.0 또는 지정 된 값을 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

문자열 값을 float로 변환 합니다. 문자열이 10 진수 값을 나타내지 않는 경우 0.0 또는 지정 된 값을 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

문자열 값을 정수로 변환 합니다. 문자열이 정수를 나타내지 않는 경우 0을 반환 하거나 지정 된 값을 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

선택적 추가 경로 부분을 사용 하 여 로컬 파일 경로에서 브라우저 호환 URL을 만듭니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

*값* 을 html로 인코딩된 출력으로 렌더링 하는 대신 html 태그로 렌더링 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

값을 문자열에서 지정 된 형식으로 변환할 수 있으면 true를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

개체 또는 변수에 값이 없으면 true를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

요청이 POST 인 경우 true를 반환 합니다. 초기 요청은 일반적으로 GET입니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

이 페이지에 적용할 레이아웃 페이지의 경로를 지정 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

현재 요청의 페이지, 레이아웃 페이지 및 부분 페이지 간에 공유 되는 데이터를 포함 합니다. `Page`다음 예제와 같이 동적 속성을 사용 하 여 동일한 데이터에 액세스할 수 있습니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(레이아웃 페이지) 명명 된 섹션에 없는 콘텐츠 페이지의 콘텐츠를 렌더링 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

지정 된 경로와 선택적 추가 데이터를 사용 하 여 콘텐츠 페이지를 렌더링 합니다. `PageData`위치 (예 1) 또는 키 (예 2)로에서 추가 매개 변수 값을 가져올 수 있습니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(레이아웃 페이지) 이름이 인 콘텐츠 섹션을 렌더링 합니다. 섹션을 선택 사항으로 만들려면 *필수* 를 false로 설정 합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

HTTP 쿠키의 값을 가져오거나 설정 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

현재 요청에서 업로드 된 파일을 가져옵니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

형식 (문자열)으로 게시 된 데이터를 가져옵니다. `Request[key]``Request.Form`및 컬렉션을 모두 검사 `Request.QueryString` 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

URL 쿼리 문자열에 지정 된 데이터를 가져옵니다. `Request[key]``Request.Form`및 컬렉션을 모두 검사 `Request.QueryString` 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

Form 요소, 쿼리 문자열 값, 쿠키 또는 헤더 값에 대 한 요청 유효성 검사를 선택적으로 사용 하지 않도록 설정 합니다. 요청 유효성 검사는 기본적으로 사용 하도록 설정 되어 있으므로 사용자가 태그 또는 기타 잠재적으로 위험한 콘텐츠를 게시할 수 없습니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

응답에 HTTP 서버 헤더를 추가 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

지정 된 시간 동안 페이지 출력을 캐시 합니다. 필요에 따라 *슬라이딩* 를 설정 하 여 각 페이지 액세스의 제한 시간을 다시 설정 하 고 페이지 요청에서 각 쿼리 문자열에 대해 서로 다른 버전의 페이지를 *varyByParams* 합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

브라우저 요청을 새 위치로 리디렉션합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

브라우저에 전송 되는 HTTP 상태 코드를 설정 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

선택적 MIME 형식을 사용 하 여 *데이터* 의 콘텐츠를 응답에 씁니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

파일의 내용을 응답에 씁니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(레이아웃 페이지) 이름이 인 콘텐츠 섹션을 정의 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

HTML로 인코딩된 문자열을 디코딩합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

HTML 태그에서 렌더링 하기 위해 문자열을 인코딩합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

지정 된 가상 경로에 대 한 서버 실제 경로를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

URL에서 텍스트를 디코딩합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

URL에 넣을 텍스트를 인코딩합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

사용자가 브라우저를 닫을 때까지 존재 하는 값을 가져오거나 설정 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

개체의 값에 대 한 문자열 표현을 표시 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

URL (예: */MyPage/ExtraData*)에서 추가 데이터를 가져옵니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

지정한 사용자의 암호를 변경합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

계정 확인 토큰을 사용 하 여 계정을 확인 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

지정 된 사용자 이름 및 암호를 사용 하 여 새 사용자 계정을 만듭니다. 확인 토큰을 요구 하려면 RequireConfirmationToken에 대해 true를 전달 *합니다.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

현재 로그인 한 사용자의 정수 식별자를 가져옵니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

현재 로그인 한 사용자의 이름을 가져옵니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

사용자가 암호를 다시 설정할 수 있도록 사용자에 게 전자 메일로 보낼 수 있는 암호 다시 설정 토큰을 생성 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

사용자 이름에서 사용자 ID를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

현재 사용자가 로그인 한 경우 true를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

사용자가 확인 된 경우 true를 반환 합니다 (예: 확인 전자 메일을 통해).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

현재 사용자의 이름이 지정 된 사용자 이름과 일치 하면 true를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

쿠키에 인증 토큰을 설정 하 여 사용자를 로그인 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

인증 토큰 쿠키를 제거 하 여 사용자를 로그 아웃 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

사용자가 인증되지 않은 경우 HTTP 상태를 401(권한 없음)로 설정합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

현재 사용자가 지정 된 역할 중 하나의 멤버가 아닌 경우는 HTTP 상태를 401 (권한 없음)로 설정 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

현재 사용자가 사용자 *이름*으로 지정 된 사용자가 아닌 경우는 HTTP 상태를 401 (권한 없음)로 설정 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

암호 다시 설정 토큰이 유효한 경우에서 사용자의 암호를 새 암호로 변경 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>데이터

### `Database.Execute(SQLstatement [,parameters]`

INSERT, DELETE 또는 UPDATE와 같은 선택적 매개 변수를 사용 하 여 *SQLstatement* 를 실행 하 고 영향을 받는 레코드의 수를 반환 합니다.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

가장 최근에 삽입한 행에서 ID 열을 반환합니다.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

지정 된 데이터베이스 파일 또는 *Web.config* 파일의 명명 된 연결 문자열을 사용 하 여 지정 된 데이터베이스를 엽니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

연결 문자열을 사용 하 여 데이터베이스를 엽니다. 이 `Database.Open` 는 연결 문자열 이름을 사용 하는와 대조 됩니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

*SQLstatement* (필요에 따라 매개 변수를 전달)를 사용 하 여 데이터베이스를 쿼리하고 결과를 컬렉션으로 반환 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

선택적 매개 변수를 사용 하 여 *SQLstatement* 를 실행 하 고 단일 레코드를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

선택적 매개 변수를 사용 하 여 *SQLstatement* 를 실행 하 고 단일 값을 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>도우미

### `Analytics.GetGoogleHtml(webPropertyId)`

지정 된 ID에 대 한 Google 분석 JavaScript 코드를 렌더링 합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

지정 된 프로젝트에 대 한 StatCounter Analytics JavaScript 코드를 렌더링 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

지정 된 계정에 대 한 Yahoo Analytics JavaScript 코드를 렌더링 합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

검색을 Bing에 전달 합니다. 검색할 사이트와 검색 상자의 제목을 지정 하려면 및 속성을 설정할 수 있습니다 `Bing.SiteUrl` `Bing.SiteTitle` . 일반적으로 * \_ AppStart* 페이지에서 이러한 속성을 설정 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

차트를 초기화 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

차트에 범례를 추가 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

차트에 일련의 값을 추가 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

지정 된 데이터에 대 한 해시를 반환 합니다. 기본 알고리즘은 `sha256` 입니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Facebook 사용자가 페이지에 연결할 수 있습니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

파일 업로드를 위한 UI를 렌더링 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

지정 된 Xbox 게이머 태그를 렌더링 합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

지정 된 전자 메일 주소에 대 한 Gravatar 이미지를 렌더링 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

데이터 개체를 JSON (JavaScript Object Notation) 형식의 문자열로 변환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

JSON으로 인코딩된 입력 문자열을 반복 해 서 반복 하거나 데이터베이스에 삽입할 수 있는 데이터 개체로 변환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

지정 된 제목 및 선택적 URL을 사용 하 여 소셜 네트워킹 링크를 렌더링 합니다.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

오류 메시지를 양식 필드와 연결 합니다. 도우미를 사용 `ModelState` 하 여이 멤버에 액세스 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

오류 메시지를 폼과 연결 합니다. 도우미를 사용 `ModelState` 하 여이 멤버에 액세스 합니다.

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

유효성 검사 오류가 없으면 true를 반환 합니다. 도우미를 사용 `ModelState` 하 여이 멤버에 액세스 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

개체 및 모든 자식 개체의 속성 및 값을 렌더링 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

ReCAPTCHA 확인 테스트를 렌더링 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

ReCAPTCHA 서비스에 대 한 공개 키 및 개인 키를 설정 합니다. 일반적으로 * \_ AppStart* 페이지에서 이러한 속성을 설정 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

ReCAPTCHA 테스트의 결과를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

ASP.NET 웹 페이지에 대 한 상태 정보를 렌더링 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

지정 된 사용자에 대 한 Twitter 스트림을 렌더링 합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

지정 된 검색 텍스트에 대 한 Twitter 스트림을 렌더링 합니다.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

지정 된 파일에 대해 선택적 너비와 높이를 사용 하 여 Flash 비디오 플레이어를 렌더링 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

지정 된 파일에 대해 선택적 너비와 높이를 사용 하 여 Windows Media player를 렌더링 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

지정 된 *.xap* 파일에 대해 필요한 너비와 높이를 사용 하 여 Silverlight 플레이어를 렌더링 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

*키*로 지정 된 개체를 반환 하거나, 개체를 찾을 수 없는 경우 null을 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

*키* 로 지정 된 개체를 캐시에서 제거 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

*키*로 지정 된 이름으로 캐시에 *값* 을 넣습니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

`WebGrid`쿼리의 데이터를 사용 하 여 새 개체를 만듭니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

HTML 테이블에 데이터를 표시 하는 태그를 렌더링 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

개체에 대 한 pager를 렌더링 `WebGrid` 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

지정 된 경로에서 이미지를 로드 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

지정 된 이미지를 워터 마크로 추가 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

이미지에 지정 된 텍스트를 추가 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

이미지를 가로 또는 세로로 대칭 이동 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

파일을 업로드 하는 동안 이미지를 페이지에 게시할 때 이미지를 로드 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

이미지의 크기를 조정 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

이미지를 왼쪽 또는 오른쪽으로 회전 합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

이미지를 지정 된 경로에 저장 합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

SMTP 서버에 대 한 암호를 설정 합니다. 일반적으로 * \_ AppStart* 페이지에서이 속성을 설정 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

이메일 메시지를 보냅니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

SMTP 서버 이름을 설정 합니다. 일반적으로 * \_ AppStart* 페이지에서이 속성을 설정 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

SMTP 서버에 대 한 사용자 이름을 설정 합니다. 일반적으로 * \_ AppStart* 페이지에서이 속성을 설정 해야 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>유효성 검사

### `Html.ValidationMessage(field)`

[v2 지정 된 필드에 대 한 유효성 검사 오류 메시지를 렌더링 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

[v2 모든 유효성 검사 오류 목록을 표시 합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

[v2 지정 된 형식의 유효성 검사에 대 한 사용자 입력 요소를 등록 합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

[v2 유효성 검사 오류 메시지의 형식을 지정할 수 있도록 클라이언트 쪽 유효성 검사에 대 한 CSS 클래스 특성을 동적으로 렌더링 합니다. 를 사용 하려면 적절 한 클라이언트 스크립트 라이브러리를 참조 하 고 CSS 클래스를 정의 해야 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

[v2 사용자 입력 필드에 대 한 클라이언트 쪽 유효성 검사를 사용 하도록 설정 합니다. 적절 한 클라이언트 스크립트 라이브러리를 참조 해야 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

[v2 유효성 검사에 registred 된 모든 사용자 입력 요소에 유효한 값이 포함 된 경우 true를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

[v2 사용자가 사용자 입력 요소에 대 한 값을 제공 하도록 지정 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

[v2 사용자가 각 사용자 입력 요소에 대 한 값을 제공 하도록 지정 합니다. 이 방법을 사용 하면 사용자 지정 오류 메시지를 지정할 수 없습니다.

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

[v2 메서드를 사용할 때 유효성 검사 테스트를 지정 합니다 `Validation.Add` .

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
