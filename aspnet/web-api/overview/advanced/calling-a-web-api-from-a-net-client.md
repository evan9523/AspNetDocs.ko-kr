---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: '.NET 클라이언트에서 Web API 호출 (c #)-ASP.NET 4.x'
author: MikeWasson
description: 이 자습서에서는 .NET 4.x 응용 프로그램에서 web API를 호출 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 484d927eeb0ba49f5f00d476f4658ebc081d0a4a
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172941"
---
# <a name="call-a-web-api-from-a-net-client-c"></a>.NET 클라이언트에서 Web API 호출 (c #)

만든 사람 [Mike Wasson](https://github.com/MikeWasson) And [Rick Anderson](https://twitter.com/RickAndMSFT)

[완료 된 프로젝트를 다운로드](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)합니다. [지침을 다운로드하세요](/aspnet/core/tutorials/#how-to-download-a-sample). 

이 자습서에서는 .NET 응용 프로그램에서 웹 API를 호출 하는 방법을 보여 [줍니다.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)

이 자습서에서는 다음 web API를 사용 하는 클라이언트 앱이 작성 됩니다.

| 작업 | HTTP 메서드 | 상대 URI |
| --- | --- | --- |
| ID별 제품 가져오기 | GET | /api/products/*id* |
| 새 제품 만들기 | POST | /api/제품 |
| 제품 업데이트 | PUT | /api/products/*id* |
| 제품 삭제 | Delete | /api/products/*id* |

ASP.NET Web API를 사용 하 여이 API를 구현 하는 방법을 알아보려면 [CRUD 작업을 지 원하는 WEB API 만들기](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)를 참조 하세요.

간단히 하기 위해이 자습서의 클라이언트 응용 프로그램은 Windows 콘솔 응용 프로그램입니다. **Httpclient** 는 Windows Phone 및 Windows 스토어 앱 에서도 지원 됩니다. 자세한 내용은 [이식 가능한 라이브러리를 사용 하 여 여러 플랫폼에 대 한 WEB API 클라이언트 코드 작성](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx) 을 참조 하세요.

**참고:** 기본 Url과 상대 Uri를 하드 코드 된 값으로 전달 하는 경우 API를 활용 하는 규칙에 주의 해야 합니다 `HttpClient` . `HttpClient.BaseAddress`속성은 후행 슬래시 ()로 주소를 설정 해야 합니다 `/` . 예를 들어 하드 코드 된 리소스 Uri를 메서드에 전달할 때 `HttpClient.GetAsync` 선행 슬래시를 포함 하지 않습니다. `Product`ID로을 가져오려면 다음을 수행 합니다.

1. 설정`client.BaseAddress = new Uri("https://localhost:5001/");`
1. 을 요청 `Product` 합니다. 예: `client.GetAsync<Product>("api/products/4");`.

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a>콘솔 응용 프로그램 만들기

Visual Studio에서 **Httpclientsample** 이라는 새 Windows 콘솔 앱을 만들고 다음 코드를 붙여 넣습니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

위의 코드는 전체 클라이언트 앱입니다.

`RunAsync`는 완료 될 때까지 실행 되 고 차단 됩니다. 대부분의 **Httpclient** 메서드는 네트워크 i/o를 수행 하기 때문에 비동기입니다. 모든 비동기 작업은 내에서 수행 됩니다 `RunAsync` . 일반적으로 앱은 주 스레드를 차단 하지 않지만이 앱은 모든 상호 작용을 허용 하지 않습니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a>Web API 클라이언트 라이브러리를 설치 합니다.

NuGet 패키지 관리자를 사용 하 여 Web API 클라이언트 라이브러리 패키지를 설치 합니다.

**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다. 패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.

`Install-Package Microsoft.AspNet.WebApi.Client`

이전 명령은 다음 NuGet 패키지를 프로젝트에 추가 합니다.

* WebApi. 클라이언트
* Newtonsoft.Json

Netwonsoft (Json.NET 라고도 함)는 .NET 용으로 널리 사용 되는 고성능 JSON 프레임 워크입니다.

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a>모델 클래스 추가

`Product` 클래스를 확인합니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

이 클래스는 web API에서 사용 하는 데이터 모델과 일치 합니다. 앱은 **Httpclient** 를 사용 하 여 `Product` HTTP 응답에서 인스턴스를 읽을 수 있습니다. 앱은 deserialization 코드를 작성할 필요가 없습니다.

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a>HttpClient 만들기 및 초기화

정적 **Httpclient** 속성을 검사 합니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

**Httpclient** 는 한 번 인스턴스화되어 응용 프로그램의 수명 내내 다시 사용 됩니다. 다음 조건에 따라 **Socketexception** 오류가 발생할 수 있습니다.

* 요청당 새 **Httpclient** 인스턴스를 만듭니다.
* 부하가 높은 서버입니다.

요청당 새 **Httpclient** 인스턴스를 만들면 사용 가능한 소켓이 고갈 될 수 있습니다.

다음 코드는 **Httpclient** 인스턴스를 초기화 합니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

위의 코드는

* HTTP 요청에 대 한 기본 URI를 설정 합니다. 서버 앱에서 사용 되는 포트로 포트 번호를 변경 합니다. 서버 앱에 대 한 포트를 사용 하지 않으면 앱이 작동 하지 않습니다.
* Accept 헤더를 "application/json"으로 설정 합니다. 이 헤더를 설정 하면 서버에서 JSON 형식으로 데이터를 전송 합니다.

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a>리소스를 검색 하기 위해 GET 요청 보내기

다음 코드는 제품에 대 한 GET 요청을 보냅니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

**Getasync** 메서드는 HTTP GET 요청을 보냅니다. 메서드가 완료 되 면 HTTP 응답을 포함 하는 **HttpResponseMessage** 를 반환 합니다. 응답의 상태 코드가 성공 코드 이면 응답 본문은 제품의 JSON 표현을 포함 합니다. **Readasasync** 를 호출 하 여 JSON 페이로드를 `Product` 인스턴스로 deserialize 합니다. 응답 본문은 임의로 클 수 있으므로 **Readasasync** 메서드는 비동기입니다.

HTTP 응답에 오류 코드가 포함 되어 있으면 **Httpclient** 는 예외를 throw 하지 않습니다. 대신 **.issuccessstatuscode** 속성은 상태가 오류 코드 이면 **false** 입니다. HTTP 오류 코드를 예외로 처리 하는 것을 선호 하는 경우 응답 개체에서 [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) 를 호출 합니다. `EnsureSuccessStatusCode`상태 코드가 200 299 범위를 벗어나면 예외가 throw 됩니다 &ndash; . 요청 시간이 초과 되는 경우 **Httpclient** 는 다른 이유로 예외를 throw 할 수 있습니다 &mdash; .

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a>Deserialize 할 미디어 형식 포맷터

**Readasasync** 가 매개 변수 없이 호출 되는 경우 기본 *미디어 포맷터* 집합을 사용 하 여 응답 본문을 읽습니다. 기본 포맷터는 JSON, XML 및 폼 url로 인코딩된 데이터를 지원 합니다.

기본 포맷터를 사용 하는 대신, **Readasasync** 메서드에 포맷터 목록을 제공할 수 있습니다.  포맷터 목록을 사용 하면 사용자 지정 미디어 형식 포맷터가 있는 경우 유용 합니다.

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

자세한 내용은 [ASP.NET Web API 2의 미디어 포맷터](../formats-and-model-binding/media-formatters.md) (영문)를 참조 하세요.

## <a name="sending-a-post-request-to-create-a-resource"></a>리소스를 만들기 위한 POST 요청 보내기

다음 코드는 `Product` 인스턴스를 JSON 형식으로 포함 하는 POST 요청을 보냅니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

**PostAsJsonAsync** 메서드는 다음과 같습니다.

* 개체를 JSON으로 serialize 합니다.
* POST 요청에서 JSON 페이로드를 보냅니다.

요청이 성공 하면 다음을 수행 합니다.

* 201 (Created) 응답을 반환 해야 합니다.
* 응답에는 Location 헤더에 생성 된 리소스의 URL이 포함 되어야 합니다.

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a>리소스를 업데이트 하는 PUT 요청 보내기

다음 코드는 제품을 업데이트 하는 PUT 요청을 보냅니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

**PutAsJsonAsync** 메서드는 POST 대신 PUT 요청을 전송 한다는 점을 제외 하 고는 **PostAsJsonAsync**와 유사 하 게 작동 합니다.

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a>리소스를 삭제 하는 삭제 요청 보내기

다음 코드는 제품을 삭제 하는 삭제 요청을 보냅니다.

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

GET과 마찬가지로 DELETE 요청에는 요청 본문이 없습니다. DELETE를 사용 하 여 JSON 또는 XML 형식을 지정할 필요가 없습니다.

## <a name="test-the-sample"></a>샘플 테스트

클라이언트 앱을 테스트 하려면:

1. 서버 앱을 [다운로드](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) 하 고 실행 합니다. [지침을 다운로드하세요](/aspnet/core/#how-to-download-a-sample). 서버 앱이 작동 하는지 확인 합니다. 예를 들어는 `http://localhost:64195/api/products` 제품 목록을 반환 합니다.
2. HTTP 요청에 대 한 기본 URI를 설정 합니다. 서버 앱에서 사용 되는 포트로 포트 번호를 변경 합니다.
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. 클라이언트 앱을 실행합니다. 다음 출력이 생성됩니다.

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
