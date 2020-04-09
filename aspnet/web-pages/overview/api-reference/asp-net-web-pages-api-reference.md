---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET 웹 페이지 (면도기) API 빠른 참조 | 마이크로 소프트 문서
author: Rick-Anderson
description: 이 페이지에는 Razor 구문을 사용하여 웹 페이지를 프로그래밍하기 위한 가장 일반적으로 사용되는 개체, 속성 및 메서드에 대한 간단한 예제가 포함된 목록이 ASP.NET.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675852"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET 웹 페이지(Razor) API 빠른 참조

[Tom FitzMacken](https://github.com/tfitzmac)

> 이 페이지에는 Razor 구문을 사용하여 웹 페이지를 프로그래밍하기 위한 가장 일반적으로 사용되는 개체, 속성 및 메서드에 대한 간단한 예제가 포함된 목록이 ASP.NET.
> 
> "(v2)"로 표시된 설명은 웹 페이지 버전 2에서 ASP.NET.
> 
> API 참조 설명서의 경우 MSDN의 [ASP.NET 웹 페이지 참조 문서를](https://go.microsoft.com/fwlink/?LinkId=208659) 참조하십시오.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (면도기) 3
>   
> 
> 이 자습서에서는 ASP.NET 웹 페이지 2 및 ASP.NET 웹 페이지 1.0에서도 작동합니다(v2로 표시된 기능은 제외).

이 페이지에는 다음에 대한 참조 정보가 포함되어 있습니다.

- [클래스](#Classes)
- [Data](#Data)
- [도우미](#Helpers)
- [유효성 검사](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>클래스

### `AppState[key], AppState[index],App`

응용 프로그램의 모든 페이지에서 공유할 수 있는 데이터를 포함합니다. 동적 `App` 속성을 사용하여 다음 예제와 같이 동일한 데이터에 액세스할 수 있습니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

문자열 값을 부울 값(true/false)으로 변환합니다. 문자열이 true/false를 나타내지 않는 경우 false 또는 지정된 값을 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

문자열 값을 날짜/시간으로 변환합니다. 문자열이 날짜/시간을 나타내지 않는 경우 또는 지정된 값을 반환합니다. `DateTime.MinValue`

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

문자열 값을 소수점 값으로 변환합니다. 문자열이 소수점 값을 나타내지 않는 경우 0.0 또는 지정된 값을 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

문자열 값을 float로 변환합니다. 문자열이 소수점 값을 나타내지 않는 경우 0.0 또는 지정된 값을 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

문자열 값을 정수로 변환합니다. 문자열이 정수를 나타내지 않는 경우 0 또는 지정된 값을 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

선택적 추가 경로 파트를 사용 하 여 로컬 파일 경로에서 브라우저 호환 URL을 만듭니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

*값을* HTML 인코딩된 출력으로 렌더링하는 대신 HTML 태그로 렌더링합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

값을 문자열에서 지정된 형식으로 변환할 수 있는 경우 true를 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

개체 또는 변수에 값이 없는 경우 true를 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

요청이 POST인 경우 true를 반환합니다. (초기 요청은 일반적으로 GET입니다.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

이 페이지에 적용할 레이아웃 페이지의 경로를 지정합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

현재 요청의 페이지, 레이아웃 페이지 및 부분 페이지 간에 공유되는 데이터를 포함합니다. 동적 `Page` 속성을 사용하여 다음 예제와 같이 동일한 데이터에 액세스할 수 있습니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(레이아웃 페이지) 명명된 섹션에 없는 콘텐츠 페이지의 콘텐츠를 렌더링합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

지정된 경로 및 선택적 추가 데이터를 사용하여 콘텐츠 페이지를 렌더링합니다. 위치(예 1) 또는 키(예 `PageData` 2)별로 추가 매개변수의 값을 얻을 수 있습니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(레이아웃 페이지) 이름이 있는 콘텐츠 섹션을 렌더링합니다. 섹션을 선택 사항으로 만들기 위해 false로 *설정합니다.*

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

HTTP 쿠키의 값을 얻거나 설정합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

현재 요청에 업로드된 파일을 가져옵니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

양식에 게시된 데이터를 문자열로 가져옵니다. `Request[key]``Request.Form` 컬렉션과 컬렉션을 모두 검사합니다. `Request.QueryString`

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

URL 쿼리 문자열에 지정된 데이터를 가져옵니다. `Request[key]``Request.Form` 컬렉션과 컬렉션을 모두 검사합니다. `Request.QueryString`

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

양식 요소, 쿼리 문자열 값, 쿠키 또는 헤더 값에 대한 요청 유효성 검사를 선택적으로 비활성화합니다. 요청 유효성 검사는 기본적으로 활성화되어 있으며 사용자가 태그 또는 기타 잠재적으로 위험한 콘텐츠를 게시하지 못하도록 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

응답에 HTTP 서버 헤더를 추가합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

지정된 시간 동안 페이지 출력을 캐시합니다. 선택적으로 *슬라이딩을* 설정하여 각 페이지 액세스의 시간 시간을 재설정하고 페이지 요청의 각 쿼리 문자열에 대해 페이지의 다른 버전을 캐시하도록 *ByParams를 변경합니다.*

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

브라우저 요청을 새 위치로 리디렉션합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

브라우저로 전송된 HTTP 상태 코드를 설정합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

선택적 MIME 형식을 사용하여 *응답에 데이터* 내용을 씁니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

파일의 내용을 응답에 씁니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(레이아웃 페이지) 이름이 있는 콘텐츠 섹션을 정의합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

HTML인코딩된 문자열을 디코딩합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

HTML 태그에서 렌더링할 문자열을 인코딩합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

지정된 가상 경로에 대한 서버 물리적 경로를 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

URL에서 텍스트를 디코딩합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

URL에 넣을 텍스트를 인코딩합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

사용자가 브라우저를 닫을 때까지 존재하는 값을 얻거나 설정합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

개체 값의 문자열 표현을 표시합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

URL에서 추가 데이터를 가져옵니다(예: */MyPage/ExtraData).*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

지정한 사용자의 암호를 변경합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

계정 확인 토큰을 사용하여 계정을 확인합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

지정된 사용자 이름과 암호를 가진 새 사용자 계정을 만듭니다. 확인 토큰을 요구하려면 *요구확인 토큰에* 대해 true를 전달합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

현재 로그인한 사용자의 정수 식별자를 가져옵니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

현재 로그인한 사용자의 이름을 가져옵니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

사용자가 암호를 재설정할 수 있도록 사용자에게 전자 메일로 보낼 수 있는 암호 재설정 토큰을 생성합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

사용자 이름에서 사용자 ID를 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

현재 사용자가 로그인한 경우 true를 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

사용자가 확인된 경우(예: 확인 전자 메일을 통해) true를 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

현재 사용자의 이름이 지정된 사용자 이름과 일치하는 경우 true를 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

쿠키에 인증 토큰을 설정하여 사용자를 로그인합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

인증 토큰 쿠키를 제거하여 사용자를 로그아웃합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

사용자가 인증되지 않은 경우 HTTP 상태를 401(권한 없음)로 설정합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

현재 사용자가 지정된 역할 중 하나의 구성원이 아닌 경우 HTTP 상태를 401(무단)으로 설정합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

현재 사용자가 *사용자 이름으로*지정한 사용자가 아닌 경우 HTTP 상태를 401(무단)으로 설정합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

암호 재설정 토큰이 유효한 경우 사용자의 암호를 새 암호로 변경합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>데이터

### `Database.Execute(SQLstatement [,parameters]`

INSERT, DELETE 또는 UPDATE와 같은 선택적 매개 변수를 사용 하 여 *SQLstatement을* 실행 하 고 영향을 받는 레코드의 수를 반환 합니다.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

가장 최근에 삽입한 행에서 ID 열을 반환합니다.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

*Web.config* 파일에서 명명된 연결 문자열을 사용하여 지정된 데이터베이스 또는 지정된 데이터베이스 파일을 엽니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

연결 문자열을 사용하여 데이터베이스를 엽니다. (이 연결 `Database.Open`문자열 이름을 사용 하는 와 대조됩니다.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

*SQLstatement(선택적으로* 매개 변수 를 전달하는)을 사용하여 데이터베이스를 쿼리하고 결과를 컬렉션으로 반환합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

선택적 매개 변수를 사용 하 고 *SQLstatement를* 실행 하 고 단일 레코드를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

선택적 매개 변수를 사용 하 고 *SQLstatement를* 실행 하 고 단일 값을 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>도우미

### `Analytics.GetGoogleHtml(webPropertyId)`

지정된 ID에 대한 Google 애널리틱스 자바스크립트 코드를 렌더링합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

지정된 프로젝트에 대한 StatCounter 분석 자바스크립트 코드를 렌더링합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

지정된 계정에 대한 야후 분석 자바 스크립트 코드를 렌더링합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Bing에 검색을 전달합니다. 검색할 사이트와 검색 상자의 제목을 지정하려면 `Bing.SiteUrl` 및 `Bing.SiteTitle` 속성을 설정할 수 있습니다. 일반적으로 * \_AppStart* 페이지에서 이러한 속성을 설정합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

차트를 초기화합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

차트에 범례를 추가합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

차트에 일련의 값을 추가합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

지정된 데이터에 대한 해시를 반환합니다. 기본 알고리즘은 `sha256`.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Facebook 사용자가 페이지에 연결할 수 있습니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

파일 업로드를 위한 UI를 렌더링합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

지정된 Xbox 게이머 태그를 렌더링합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

지정된 이메일 주소에 대한 Gravatar 이미지를 렌더링합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

데이터 개체를 JSON(JavaScript 개체 표기형) 형식의 문자열로 변환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

JSON 인코딩된 입력 문자열을 반복하거나 데이터베이스에 삽입할 수 있는 데이터 개체로 변환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

지정된 제목 및 선택적 URL을 사용하여 소셜 네트워킹 링크를 렌더링합니다.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

오류 메시지를 양식 필드와 연결합니다. 도우미를 `ModelState` 사용하여 이 멤버에 액세스합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

오류 메시지를 양식과 연결합니다. 도우미를 `ModelState` 사용하여 이 멤버에 액세스합니다.

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

유효성 검사 오류가 없는 경우 true를 반환합니다. 도우미를 `ModelState` 사용하여 이 멤버에 액세스합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

개체 및 자식 오브젝트의 속성 및 값을 렌더링합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

reCAPTCHA 확인 테스트를 렌더링합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

reCAPTCHA 서비스에 대한 공개 및 개인 키를 설정합니다. 일반적으로 * \_AppStart* 페이지에서 이러한 속성을 설정합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

reCAPTCHA 테스트의 결과를 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

ASP.NET 웹 페이지에 대한 상태 정보를 렌더링합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

지정된 사용자에 대한 트위터 스트림을 렌더링합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

지정된 검색 텍스트에 대한 트위터 스트림을 렌더링합니다.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

선택적 너비와 높이로 지정된 파일에 대해 Flash 비디오 플레이어를 렌더링합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

선택적 너비와 높이로 지정된 파일에 대해 Windows Media 플레이어를 렌더링합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

필요한 너비와 높이로 지정된 *.xap* 파일에 대해 Silverlight 플레이어를 렌더링합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

*개체를*찾을 수 없는 경우 key 또는 null에 의해 지정 된 개체를 반환 합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

캐시에서 *키로* 지정된 개체를 제거합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

*key로*지정된 이름 아래 *캐시에 값을* 넣습니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

쿼리의 `WebGrid` 데이터를 사용하여 새 개체를 만듭니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

HTML 테이블에 데이터를 표시하도록 태그를 렌더링합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

개체에 대한 호출기 `WebGrid` 렌더링합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

지정된 경로에서 이미지를 로드합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

지정된 이미지를 워터마크로 추가합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

지정된 텍스트를 이미지에 추가합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

이미지를 가로 또는 세로로 뒤집습니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

파일을 업로드하는 동안 이미지가 페이지에 게시될 때 이미지를 로드합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

이미지크기를 조정합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

이미지를 왼쪽 또는 오른쪽으로 회전합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

이미지를 지정된 경로에 저장합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

SMTP 서버의 암호를 설정합니다. 일반적으로 * \_AppStart* 페이지에서 이 속성을 설정합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

메일 메시지를 전송합니다.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

SMTP 서버 이름을 설정합니다. 일반적으로 * \_AppStart* 페이지에서 이 속성을 설정합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

SMTP 서버의 사용자 이름을 설정합니다. 일반적으로 * \_AppStart* 페이지에서 이 속성을 설정해야 합니다.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>유효성 검사

### `Html.ValidationMessage(field)`

(v2) 지정된 필드에 대한 유효성 검사 오류 메시지를 렌더링합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

(v2) 모든 유효성 검사 오류 목록을 표시합니다.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

(v2) 지정된 유형의 유효성 검사에 대한 사용자 입력 요소를 등록합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

(v2) 유효성 검사 오류 메시지의 서식을 지정할 수 있도록 클라이언트 측 유효성 검사에 대한 CSS 클래스 특성을 동적으로 렌더링합니다. (적절한 클라이언트 스크립트 라이브러리를 참조하고 CSS 클래스를 정의해야 합니다.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

(v2) 사용자 입력 필드에 대한 클라이언트 측 유효성 검사를 활성화합니다. (적절한 클라이언트 스크립트 라이브러리를 참조해야 합니다.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

(v2) 유효성 검사를 위해 레지스트리된 모든 사용자 입력 요소에 유효한 값이 포함된 경우 true를 반환합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

(v2) 사용자가 사용자 입력 요소에 대한 값을 제공해야 함을 지정합니다.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

(v2) 사용자가 각 사용자 입력 요소에 대한 값을 제공해야 함을 지정합니다. 이 메서드를 사용하면 사용자 지정 오류 메시지를 지정할 수 없습니다.

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

(v2) 메서드를 사용할 때 유효성 검사 `Validation.Add` 테스트를 지정합니다.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
