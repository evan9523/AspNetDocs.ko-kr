---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: ASP.NET AJAX 웹 서비스 이해 | Microsoft Docs
author: scottcate
description: 웹 서비스는 분산 된 시스템 간에 데이터를 교환 하는 플랫폼 간 솔루션을 제공 하는 .NET framework의 필수적인 부분입니다. 웹 ...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: eac3d53fd871d0cb5a2870488ce752c057cc5b1a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162845"
---
# <a name="understanding-aspnet-ajax-web-services"></a>ASP.NET AJAX 웹 서비스 이해

[Scott cate cda (](https://github.com/scottcate)

[PDF 다운로드](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> 웹 서비스는 분산 된 시스템 간에 데이터를 교환 하는 플랫폼 간 솔루션을 제공 하는 .NET framework의 필수적인 부분입니다. 웹 서비스는 일반적으로 다양 한 운영 체제, 개체 모델 및 프로그래밍 언어에서 데이터를 보내고 받을 수 있도록 하는 데 사용 되지만 ASP.NET AJAX 페이지에 데이터를 동적으로 삽입 하거나 페이지에서 백 엔드 시스템으로 데이터를 전송 하는 데에도 사용할 수 있습니다. 이 모든 작업은 다시 게시 작업을 실행 하지 않고 수행할 수 있습니다.

## <a name="calling-web-services-with-aspnet-ajax"></a>ASP.NET AJAX를 사용 하 여 웹 서비스 호출

Dan Wahlin

웹 서비스는 분산 된 시스템 간에 데이터를 교환 하는 플랫폼 간 솔루션을 제공 하는 .NET framework의 필수적인 부분입니다. 웹 서비스는 일반적으로 다양 한 운영 체제, 개체 모델 및 프로그래밍 언어에서 데이터를 보내고 받을 수 있도록 하는 데 사용 되지만 ASP.NET AJAX 페이지에 데이터를 동적으로 삽입 하거나 페이지에서 백 엔드 시스템으로 데이터를 전송 하는 데에도 사용할 수 있습니다. 이 모든 작업은 다시 게시 작업을 실행 하지 않고 수행할 수 있습니다.

ASP.NET AJAX UpdatePanel 컨트롤은 AJAX를 사용 하도록 설정 하는 간단한 방법을 제공 하지만 UpdatePanel을 사용 하지 않고 서버에서 데이터에 동적으로 액세스 해야 하는 경우가 있을 수 있습니다. 이 문서에서는 ASP.NET AJAX 페이지 내에서 웹 서비스를 만들고 사용 하 여이를 수행 하는 방법을 알아봅니다.

이 문서에서는 AutoCompleteExtender 라는 ASP.NET AJAX Toolkit의 웹 서비스 사용 컨트롤 뿐만 아니라 핵심 ASP.NET AJAX 확장에서 사용할 수 있는 기능에 대해 집중적으로 설명 합니다. AJAX 사용 웹 서비스 정의, 클라이언트 프록시 생성 및 JavaScript를 사용 하 여 웹 서비스 호출 등의 항목을 다룹니다. 웹 서비스 호출을 ASP.NET page 메서드에 직접 적용 하는 방법도 확인할 수 있습니다.

## <a name="web-services-configuration"></a>웹 서비스 구성

Visual Studio 2008을 사용 하 여 새 웹 사이트 프로젝트를 만들 때 web.config 파일에는 이전 버전의 Visual Studio 사용자에 게 익숙하지 않을 수 있는 새로운 추가 항목이 새로 추가 되었습니다. 이러한 수정 사항 중 일부는 "asp" 접두사를 페이지에서 사용할 수 있도록 ASP.NET AJAX 컨트롤에 매핑하고 다른 사용자는 필수 HttpHandlers 및 HttpModules를 정의 합니다. 목록 1은 `<httpHandlers>` 웹 서비스 호출에 영향을 주는 web.config의 요소에 대 한 수정 사항을 보여 줍니다. .Asmx 호출을 처리 하는 데 사용 되는 기본 HttpHandler는 제거 되 고 System.Web.Extensions.dll 어셈블리에 있는 ScriptHandlerFactory 클래스로 대체 됩니다. System.Web.Extensions.dll는 ASP.NET AJAX에서 사용 되는 모든 핵심 기능을 포함 합니다.

**나열 1. ASP.NET AJAX 웹 서비스 처리기 구성**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

이 HttpHandler는 JavaScript 웹 서비스 프록시를 사용 하 여 ASP.NET AJAX 페이지에서 .NET 웹 서비스로 JavaScript Object Notation (JSON) 호출을 수행할 수 있도록 하기 위해 작성 되었습니다. ASP.NET AJAX는 일반적으로 웹 서비스와 연결 된 표준 SOAP (Simple Object Access Protocol) 호출이 아닌 웹 서비스로 JSON 메시지를 보냅니다. 이로 인해 전체 요청 및 응답 메시지가 더 적게 발생 합니다. ASP.NET AJAX JavaScript 라이브러리가 JSON 개체를 사용 하도록 최적화 되어 있기 때문에 클라이언트 쪽 데이터를 더 효율적으로 처리할 수도 있습니다. 목록 2 및 목록 3에서는 JSON 형식으로 직렬화 된 웹 서비스 요청 및 응답 메시지의 예를 보여 줍니다. 목록 2에 표시 된 요청 메시지는 값이 "벨기에" 인 country 매개 변수를 전달 하는 반면, 3 번의 응답 메시지는 고객 개체의 배열과 관련 속성을 전달 합니다.

**목록 2. JSON으로 직렬화 된 웹 서비스 요청 메시지**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *>[!NOTE]작업 이름은 웹 서비스에 대 한 URL의 일부로 정의 됩니다. 또한 요청 메시지는 항상 JSON을 통해 제출 되지 않습니다. 웹 서비스는 UseHttpGet 매개 변수를 true로 설정 하 여 ScriptMethod 특성을 활용할 수 있습니다. 그러면 쿼리 문자열 매개 변수를 통해 매개 변수가 전달 됩니다.*

**목록 3. JSON으로 직렬화 된 웹 서비스 응답 메시지**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

다음 섹션에서는 JSON 요청 메시지를 처리 하 고 단순 및 복합 유형 모두를 사용 하 여 응답할 수 있는 웹 서비스를 만드는 방법을 알아봅니다.

## <a name="creating-ajax-enabled-web-services"></a>AJAX 사용 웹 서비스 만들기

ASP.NET AJAX 프레임 워크는 웹 서비스를 호출 하는 여러 가지 방법을 제공 합니다. AutoCompleteExtender 컨트롤 (ASP.NET AJAX Toolkit에서 사용 가능) 또는 JavaScript를 사용할 수 있습니다. 그러나 서비스를 호출 하기 전에 클라이언트 스크립트 코드에서 호출할 수 있도록 AJAX를 사용 하도록 설정 해야 합니다.

ASP.NET 웹 서비스를 처음 사용 하 든 관계 없이 서비스를 쉽게 만들고 AJAX를 사용 하도록 설정할 수 있습니다. .NET framework는 2002의 초기 릴리스와 ASP.NET AJAX 확장이 .NET framework의 기본 기능 집합을 기반으로 하는 추가 AJAX 기능을 제공 하므로 ASP.NET 웹 서비스 생성을 지원 했습니다. Visual Studio .NET 2008 Beta 2에는 .asmx 웹 서비스 파일을 만들 수 있는 지원이 기본적으로 제공 되며, System.web. WebService 클래스의 클래스 옆에 연결 된 코드가 자동으로 파생 됩니다. 클래스에 메서드를 추가할 때 웹 서비스 소비자가 호출 하려면 WebMethod 특성을 적용 해야 합니다.

목록 4에서는 이름이 GetCustomersByCountry () 인 메서드에 WebMethod 특성을 적용 하는 예제를 보여 줍니다.

**목록 4. 웹 서비스에서 WebMethod 특성 사용**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

GetCustomersByCountry () 메서드는 country 매개 변수를 허용 하 고 Customer 개체 배열을 반환 합니다. 메서드로 전달 되는 국가 값은 비즈니스 계층 클래스로 전달 됩니다. 그러면 데이터 계층 클래스를 호출 하 여 데이터베이스에서 데이터를 검색 하 고, 고객 개체 속성을 데이터로 채우고, 배열을 반환 합니다.

## <a name="using-the-scriptservice-attribute"></a>ScriptService 특성 사용

WebMethod 특성을 추가 하면 표준 SOAP 메시지를 웹 서비스로 보내는 클라이언트에서 GetCustomersByCountry () 메서드를 호출할 수 있지만 ASP.NET AJAX 응용 프로그램에서 즉시 JSON 호출을 수행할 수 없습니다. JSON 호출을 수행할 수 있도록 하려면 ASP.NET AJAX 확장의 `ScriptService` 특성을 웹 서비스 클래스에 적용 해야 합니다. 이렇게 하면 웹 서비스에서 JSON을 사용 하 여 형식이 지정 된 응답 메시지를 보낼 수 있으며 클라이언트 쪽 스크립트에서 JSON 메시지를 보내 서비스를 호출할 수 있습니다.

목록 5에서는 CustomersService 이라는 웹 서비스 클래스에 ScriptService 특성을 적용 하는 예를 보여 줍니다.

**목록 5. ScriptService 특성을 사용 하 여 AJAX-웹 서비스 사용**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

ScriptService 특성은 AJAX 스크립트 코드에서 호출할 수 있음을 나타내는 표식 역할을 합니다. 실제로는 백그라운드에서 발생 하는 JSON serialization 또는 deserialization 작업을 실제로 처리 하지 않습니다. ScriptHandlerFactory (web.config에서 구성) 및 기타 관련 된 클래스는 대량의 JSON 처리를 수행 합니다.

## <a name="using-the-scriptmethod-attribute"></a>ScriptMethod 특성 사용

ScriptService 특성은 ASP.NET AJAX 페이지에서 사용할 수 있도록 .NET 웹 서비스에서 정의 해야 하는 유일한 ASP.NET AJAX 특성입니다. 그러나 ScriptMethod 라는 또 다른 특성은 서비스의 웹 메서드에 직접 적용 될 수도 있습니다. ScriptMethod는, 및를 포함 하 여 세 가지 속성 `UseHttpGet` 을 정의 `ResponseFormat` `XmlSerializeString` 합니다. 웹 메서드가 또는 개체의 형태로 원시 XML 데이터를 반환 해야 `XmlDocument` `XmlElement` 하거나 서비스에서 반환 된 데이터가 항상 JSON이 아닌 XML로 serialize 되어야 하는 경우 이러한 속성의 값을 변경 하면 웹 메서드에서 허용 하는 요청 형식을 가져오기 위해 변경 해야 하는 경우에 유용할 수 있습니다.

UseHttpGet 속성은 POST 요청과 달리 웹 메서드가 GET 요청을 허용 해야 하는 경우에 사용할 수 있습니다. 요청은 QueryString 매개 변수로 변환 된 웹 메서드 입력 매개 변수와 함께 URL을 사용 하 여 전송 됩니다. UseHttpGet 속성은 기본적으로 false로 설정 되며, `true` 작업이 안전 하다 고 알려진 경우와 중요 한 데이터가 웹 서비스로 전달 되지 않은 경우에만로 설정 해야 합니다. 목록 6에서는 UseHttpGet 속성과 함께 ScriptMethod 특성을 사용 하는 예를 보여 줍니다.

**목록 6. ScriptMethod 특성을 UseHttpGet 속성과 함께 사용 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

목록 6에 표시 된 HttpGetEcho 웹 메서드가 호출 될 때 전송 되는 헤더의 예는 다음과 같습니다.

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

웹 메서드가 HTTP GET 요청을 허용 하는 것 외에도 ScriptMethod 특성은 JSON이 아닌 서비스에서 XML 응답을 반환 해야 하는 경우에도 사용할 수 있습니다. 예를 들어 웹 서비스는 원격 사이트에서 RSS 피드를 검색 하 여 XmlDocument 또는 XmlElement 개체로 반환할 수 있습니다. 그러면 XML 데이터 처리가 클라이언트에서 발생할 수 있습니다.

목록 7에서는 ResponseFormat 속성을 사용 하 여 웹 메서드에서 XML 데이터를 반환 하도록 지정 하는 예를 보여 줍니다.

**목록 7. ScriptMethod 특성에 ResponseFormat 속성을 사용 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

ResponseFormat 속성은 XmlSerializeString 속성과 함께 사용할 수도 있습니다. XmlSerializeString 속성의 기본값은 false입니다 .이 값은 속성이로 설정 된 경우 웹 메서드에서 반환 된 문자열을 제외한 모든 반환 형식이 XML로 serialize 됨을 의미 `ResponseFormat` `ResponseFormat.Xml` 합니다. `XmlSerializeString`가로 설정 된 경우 `true` 웹 메서드에서 반환 되는 모든 형식은 문자열 형식을 포함 하는 XML로 serialize 됩니다. ResponseFormat 속성의 값이 XmlSerializeString 속성의 값을 포함 하는 경우에는 `ResponseFormat.Json` 무시 됩니다.

목록 8은 XmlSerializeString 속성을 사용 하 여 문자열이 XML로 serialize 되도록 하는 예를 보여 줍니다.

**목록 8. XmlSerializeString 속성과 함께 ScriptMethod 특성 사용**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

목록 8에 표시 된 GetXmlString 웹 메서드를 호출 하 여 반환 되는 값은 다음에 표시 됩니다.

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

기본 JSON 형식은 요청 및 응답 메시지의 전체 크기를 최소화 하 고 크로스 브라우저 방식으로 ASP.NET AJAX 클라이언트에서 더 쉽게 사용 되지만, Internet Explorer 5 이상의 클라이언트 응용 프로그램에서 웹 메서드를 통해 XML 데이터를 반환 해야 하는 경우 ResponseFormat 및 XmlSerializeString 속성을 활용할 수 있습니다.

## <a name="working-with-complex-types"></a>복합 형식 작업

목록 5는 웹 서비스에서 Customer 라는 복합 형식을 반환 하는 예제를 보여 주었습니다. Customer 클래스는 FirstName 및 LastName과 같은 여러 가지 간단한 형식을 내부적으로 속성으로 정의 합니다. AJAX 사용 웹 메서드에서 입력 매개 변수나 반환 형식으로 사용 되는 복합 형식은 클라이언트 쪽에 전송 되기 전에 JSON으로 자동으로 직렬화 됩니다. 그러나 중첩 된 복합 형식 (다른 형식 내에서 내부적으로 정의 된 복합 형식)은 기본적으로 클라이언트에서 독립 실행형 개체로 사용할 수 없습니다.

웹 서비스에서 사용 하는 중첩 된 복합 형식을 클라이언트 페이지 에서도 사용 해야 하는 경우 ASP.NET AJAX GenerateScriptType 특성을 웹 서비스에 추가할 수 있습니다. 예를 들어 목록 9에 표시 된 CustomerDetails 클래스에는 ***중첩 된 복합 유형을 나타내는*** Address 및 성별 속성이 포함 되어 있습니다.

**목록 9. 여기에 표시 된 CustomerDetails 클래스에는 두 개의 중첩 된 복합 형식이 포함 되어 있습니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

목록 9에 표시 된 CustomerDetails 클래스 내에 정의 된 Address 및 성별 개체는 중첩 된 형식 이므로 JavaScript를 통해 클라이언트 쪽에서 사용할 수 있도록 자동으로 설정 되지 않습니다 (Address는 클래스이 고 성별은 열거형). 웹 서비스 내에서 사용 되는 중첩 형식을 클라이언트 쪽에서 사용할 수 있어야 하는 경우 앞에서 언급 한 GenerateScriptType 특성을 사용할 수 있습니다 (목록 10 참조). 서비스에서 다른 중첩 된 복합 형식이 반환 되는 경우이 특성을 여러 번 추가할 수 있습니다. 웹 서비스 클래스 또는 특정 웹 메서드에 직접 적용할 수 있습니다.

**10. GenerateScriptService 특성을 사용 하 여 클라이언트에서 사용할 수 있어야 하는 중첩 된 형식을 정의 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

`GenerateScriptType`웹 서비스에 특성을 적용 하면 클라이언트 쪽 ASP.NET AJAX JavaScript 코드에서 주소 및 성별 형식을 자동으로 사용할 수 있게 됩니다. 웹 서비스에 GenerateScriptType 특성을 추가 하 여 자동으로 생성 되 고 클라이언트에 전송 되는 JavaScript의 예는 목록 11에 나와 있습니다. 이 문서의 뒷부분에서 중첩 된 복합 형식을 사용 하는 방법에 대해 알아봅니다.

**목록 11. 중첩 된 복합 형식을 ASP.NET AJAX 페이지에서 사용할 수 있습니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

웹 서비스를 만들고 ASP.NET AJAX 페이지에서 액세스할 수 있도록 하는 방법을 살펴보았으므로 이제 데이터를 검색 하거나 웹 서비스로 보낼 수 있도록 JavaScript 프록시를 만들고 사용 하는 방법을 살펴보겠습니다.

## <a name="creating-javascript-proxies"></a>JavaScript 프록시 만들기

표준 웹 서비스 (.NET 또는 다른 플랫폼)를 호출 하는 경우 일반적으로 SOAP 요청 및 응답 메시지를 전송 하는 복잡성을 보호 하는 프록시 개체를 만드는 과정이 포함 됩니다. ASP.NET AJAX 웹 서비스 호출을 사용 하면 JavaScript 프록시를 만들고 JSON 메시지의 직렬화 및 역직렬화에 대해 걱정 하지 않고 손쉽게 서비스를 호출할 수 있습니다. JavaScript 프록시는 ASP.NET AJAX ScriptManager 컨트롤을 사용 하 여 자동으로 생성할 수 있습니다.

웹 서비스를 호출할 수 있는 JavaScript 프록시를 만드는 것은 ScriptManager의 서비스 속성을 사용 하 여 수행 됩니다. 이 속성을 사용 하면 ASP.NET AJAX 페이지에서 포스트백 작업 없이 데이터를 보내거나 받기 위해 비동기적으로 호출할 수 있는 하나 이상의 서비스를 정의할 수 있습니다. ASP.NET AJAX 컨트롤을 사용 하 여 서비스를 정의 하 `ServiceReference` 고 컨트롤의 속성에 웹 서비스 URL을 할당 합니다 `Path` . 목록 12는 CustomersService 라는 서비스를 참조 하는 예제를 보여 줍니다.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**목록 12. ASP.NET AJAX 페이지에서 사용 되는 웹 서비스 정의.**

ScriptManager 컨트롤을 통해 CustomersService에 대 한 참조를 추가 하면 JavaScript 프록시가 동적으로 생성 되 고 페이지에서 참조 됩니다. 프록시는 스크립트 태그를 사용 하 여 포함 되 &lt; &gt; 고 CustomersService 파일을 호출 하 고/sjs를 끝에 추가 하 여 동적으로 로드 됩니다. 다음 예제에서는 web.config에서 디버깅을 사용 하지 않도록 설정할 때 JavaScript 프록시가 페이지에 포함 되는 방법을 보여 줍니다.

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *>[!NOTE]생성 되는 실제 JavaScript 프록시 코드를 확인 하려는 경우에는 원하는 .Net 웹 서비스의 URL을 Internet Explorer의 주소 상자에 입력 하 고/sjs를 끝에 추가할 수 있습니다.*

web.config에서 디버깅을 사용 하도록 설정 하는 경우 JavaScript 프록시의 디버그 버전이 다음 그림과 같이 페이지에 포함 됩니다.

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

ScriptManager가 만든 JavaScript 프록시는 &lt; 스크립트 &gt; 태그의 src 특성을 사용 하 여 참조 하는 대신 페이지에 직접 포함 될 수도 있습니다. ServiceReference 컨트롤의 InlineScript 속성을 true (기본값은 false)로 설정 하 여이 작업을 수행할 수 있습니다. 이는 프록시가 여러 페이지에서 공유 되지 않는 경우 및 서버에 대 한 네트워크 호출 수를 줄이려는 경우에 유용할 수 있습니다. InlineScript가 true로 설정 된 경우 프록시 스크립트는 브라우저에서 캐시 되지 않으므로 ASP.NET AJAX 응용 프로그램의 여러 페이지에서 프록시를 사용 하는 경우 기본값 false를 사용 하는 것이 좋습니다. InlineScript 속성을 사용 하는 예제는 다음에 나와 있습니다.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>JavaScript 프록시 사용

ScriptManager 컨트롤을 사용 하 여 ASP.NET AJAX 페이지에서 웹 서비스를 참조 하는 경우 웹 서비스에 대 한 호출을 수행할 수 있으며 콜백 함수를 사용 하 여 반환 된 데이터를 처리할 수 있습니다. 웹 서비스는 네임 스페이스 (있는 경우), 클래스 이름 및 웹 메서드 이름을 참조 하 여 호출 됩니다. 웹 서비스로 전달 되는 모든 매개 변수는 반환 된 데이터를 처리 하는 콜백 함수와 함께 정의할 수 있습니다.

JavaScript 프록시를 사용 하 여 GetCustomersByCountry () 라는 웹 메서드를 호출 하는 예제는 목록 13에 나와 있습니다. GetCustomersByCountry () 함수는 최종 사용자가 페이지의 단추를 클릭할 때 호출 됩니다.

**목록 13. JavaScript 프록시를 사용 하 여 웹 서비스 호출**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

이 호출은 서비스에 정의 된 InterfaceTraining namespace, CustomersService class 및 GetCustomersByCountry 웹 메서드를 참조 합니다. 텍스트 상자에서 가져온 국가 값 뿐만 아니라 비동기 웹 서비스 호출이 반환 될 때 호출 되어야 하는 OnWSRequestComplete 이라는 콜백 함수를 전달 합니다. OnWSRequestComplete는 서비스에서 반환 된 고객 개체의 배열을 처리 하 고 페이지에 표시 되는 테이블로 변환 합니다. 호출에서 생성 되는 출력은 그림 1에 나와 있습니다.

[![비동기 AJAX 호출을 통해 가져온 데이터를 웹 서비스에 바인딩합니다.](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**그림 1**: 웹 서비스에 대 한 비동기 AJAX 호출을 수행 하 여 가져온 데이터 바인딩.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-web-services/_static/image3.png))

JavaScript 프록시는 웹 메서드를 호출 해야 하지만 프록시가 응답을 기다릴 수 없는 경우 웹 서비스에 대 한 단방향 호출을 수행할 수도 있습니다. 예를 들어, 웹 서비스를 호출 하 여 워크플로와 같은 프로세스를 시작 하 고 서비스의 반환 값을 기다리지 않을 수 있습니다. 서비스에 대 한 단방향 호출을 수행 해야 하는 경우에는 목록 13에 표시 된 콜백 함수를 간단히 생략할 수 있습니다. 콜백 함수를 정의 하지 않았으므로 프록시 개체는 웹 서비스가 데이터를 반환할 때까지 기다리지 않습니다.

## <a name="handling-errors"></a>오류 처리

웹 서비스에 대 한 비동기 콜백은 네트워크 다운, 웹 서비스를 사용할 수 없거나 예외가 반환 되는 등의 다양 한 유형의 오류가 발생할 수 있습니다. 다행히 ScriptManager에 의해 생성 된 JavaScript 프록시 개체를 사용 하면 이전에 표시 된 성공 콜백과 함께 오류 및 오류를 처리 하는 여러 콜백을 정의할 수 있습니다. 목록 14와 같이 웹 메서드에 대 한 호출에서 표준 콜백 함수 바로 다음에 오류 콜백 함수를 정의할 수 있습니다.

**목록 14. 오류 콜백 함수를 정의 하 고 오류를 표시 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

웹 서비스가 호출 될 때 발생 하는 모든 오류는 오류를 나타내는 개체를 매개 변수로 허용 하는 호출 될 OnWSRequestFailed () 콜백 함수를 트리거합니다. Error 개체는 오류의 원인과 호출 시간이 초과 되었는지 여부를 확인 하기 위해 여러 가지 다른 함수를 노출 합니다. 목록 14는 다른 오류 함수를 사용 하는 예를 보여 주고 그림 2는 함수에 의해 생성 된 출력의 예를 보여 줍니다.

[![ASP.NET AJAX error 함수를 호출 하 여 생성 된 출력입니다.](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**그림 2**: ASP.NET AJAX error 함수를 호출 하 여 생성 된 출력입니다.  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-web-services/_static/image6.png))

## <a name="handling-xml-data-returned-from-a-web-service"></a>웹 서비스에서 반환 된 XML 데이터 처리

이전에는 웹 메서드가 ResponseFormat 속성과 함께 ScriptMethod 특성을 사용 하 여 원시 XML 데이터를 반환 하는 방법을 살펴보았습니다. ResponseFormat이 ResponseFormat.Xml로 설정 된 경우 웹 서비스에서 반환 된 데이터는 JSON이 아닌 XML로 serialize 됩니다. 이는 JavaScript 또는 XSLT를 사용 하 여 처리 하기 위해 XML 데이터를 클라이언트에 직접 전달 해야 하는 경우에 유용할 수 있습니다. 현재 Internet Explorer 5 이상은 MSXML에 대 한 기본 제공 지원으로 인해 XML 데이터를 구문 분석 하 고 필터링 하는 데 가장 적합 한 클라이언트 쪽 개체 모델을 제공 합니다.

웹 서비스에서 XML 데이터를 검색 하는 것은 다른 데이터 형식을 검색 하는 것과 다르지 않습니다. 먼저 JavaScript 프록시를 호출 하 여 적절 한 함수를 호출 하 고 콜백 함수를 정의 합니다. 호출이 반환 되 면 콜백 함수의 데이터를 처리할 수 있습니다.

목록 15에서는 XmlElement 개체를 반환 하는 GetRssFeed () 라는 웹 메서드를 호출 하는 예를 보여 줍니다. GetRssFeed ()는 검색할 RSS 피드에 대 한 URL을 나타내는 단일 매개 변수를 허용 합니다.

**목록 15. 웹 서비스에서 반환 된 XML 데이터 작업**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

이 예에서는 RSS 피드에 URL을 전달 하 고 OnWSRequestComplete () 함수에서 반환 된 XML 데이터를 처리 합니다. OnWSRequestComplete ()는 먼저 브라우저가 Internet Explorer 인지 확인 하 여 MSXML 파서를 사용할 수 있는지 여부를 확인 합니다. 이 경우 XPath 문을 사용 하 여 &lt; &gt; RSS 피드 내의 모든 항목 태그를 찾습니다. 그런 다음 각 항목은를 반복 하 여 &lt; &gt; &lt; &gt; 각 항목의 데이터를 표시 하기 위해 연결 된 제목 및 링크 태그를 찾아서 처리 합니다. 그림 3에서는 JavaScript 프록시를 통해 GetRssFeed () 웹 메서드에 ASP.NET AJAX 호출을 수행 하 여 생성 된 출력의 예를 보여 줍니다.

## <a name="handling-complex-types"></a>복합 형식 처리

웹 서비스에서 허용 하거나 반환 하는 복합 형식은 JavaScript 프록시를 통해 자동으로 노출 됩니다. 그러나 앞에서 설명한 대로 GenerateScriptType 특성을 서비스에 적용 하지 않는 한 중첩 된 복합 형식은 클라이언트 쪽에서 직접 액세스할 수 없습니다. 클라이언트 쪽에서 중첩 된 복합 형식을 사용 하는 이유는 무엇 인가요?

이 질문에 대답 하려면 ASP.NET AJAX 페이지가 고객 데이터를 표시 하 고 최종 사용자가 고객의 주소를 업데이트할 수 있다고 가정 합니다. 웹 서비스에서 주소 유형 (CustomerDetails 클래스 내에 정의 된 복합 형식)을 클라이언트에 보낼 수 있도록 지정 하는 경우 코드를 더 효율적으로 다시 사용 하기 위해 업데이트 프로세스를 별도의 함수로 나눌 수 있습니다.

[![RSS 데이터를 반환 하는 웹 서비스를 호출 하 여 생성 된 출력입니다.](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**그림 3**: RSS 데이터를 반환 하는 웹 서비스를 호출 하 여 생성 된 출력  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-web-services/_static/image9.png))

목록 16은 모델 네임 스페이스에 정의 된 주소 개체를 호출 하 고 업데이트 된 데이터로 채운 다음 CustomerDetails 개체의 Address 속성에 할당 하는 클라이언트 쪽 코드의 예를 보여 줍니다. 그런 다음 CustomerDetails 개체가 처리를 위해 웹 서비스로 전달 됩니다.

**목록 16. 중첩 된 복합 형식 사용**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>페이지 메서드 만들기 및 사용

웹 서비스는 ASP.NET AJAX 페이지를 비롯 한 다양 한 클라이언트에 다시 활용할 수 있는 서비스를 노출 하는 뛰어난 방법을 제공 합니다. 그러나 다른 페이지에서 사용 하거나 공유 하지 않는 데이터를 페이지에서 검색 해야 하는 경우가 있을 수 있습니다. 이 경우 서비스는 단일 페이지 에서만 사용 되기 때문에 페이지에서 데이터에 액세스할 수 있도록 하는 .asmx 파일이 과도 한 것 처럼 보일 수 있습니다.

ASP.NET AJAX는 독립 실행형 .asmx 파일을 만들지 않고 웹 서비스와 같은 호출을 수행 하기 위한 또 다른 메커니즘을 제공 합니다. 이 작업은 "페이지 메서드" 라고 하는 기술을 사용 하 여 수행 됩니다. 페이지 메서드는 WebMethod 특성이 적용 된 페이지 또는 코드 병행 파일에 직접 포함 된 정적 (VB.NET의 공유) 메서드입니다. WebMethod 특성을 적용 하 여 런타임에 동적으로 생성 되는 PageMethods 라는 특수 JavaScript 개체를 사용 하 여 호출할 수 있습니다. PageMethods 개체는 JSON serialization/deserialization 프로세스에서 사용자를 보호 하는 프록시로 작동 합니다. PageMethods 개체를 사용 하려면 ScriptManager의 EnablePageMethods 속성을 true로 설정 해야 합니다.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

목록 17은 ASP.NET 코드 병행 클래스에서 두 페이지 메서드를 정의 하는 예제를 보여 줍니다. 이러한 메서드는 웹 사이트의 앱 코드 폴더에 있는 비즈니스 계층 클래스에서 데이터를 검색 \_ 합니다.

**목록 17. 페이지 메서드 정의**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

ScriptManager가 페이지에 웹 메서드가 있음을 감지 하면 앞에서 언급 한 PageMethods 개체에 대 한 동적 참조를 생성 합니다. 웹 메서드 호출은 PageMethods 클래스, 메서드 이름 및 전달 해야 하는 모든 필수 매개 변수 데이터를 참조 하 여 수행 됩니다. 목록 18은 앞에 표시 된 두 페이지 메서드를 호출 하는 예제를 보여 줍니다.

**목록 18. PageMethods JavaScript 개체를 사용 하 여 페이지 메서드를 호출 합니다.**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

PageMethods 개체를 사용 하는 것은 JavaScript 프록시 개체를 사용 하는 것과 매우 비슷합니다. 먼저 페이지 메서드에 전달 해야 하는 모든 매개 변수 데이터를 지정한 다음 비동기 호출이 반환 될 때 호출 해야 하는 콜백 함수를 정의 합니다. 오류 콜백을 지정할 수도 있습니다 (오류를 처리 하는 예제는 목록 14 참조).

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>AutoCompleteExtender 및 ASP.NET AJAX Toolkit

ASP.NET AJAX Toolkit (에서 사용 가능 [http://ajax.asp.net](http://ajax.asp.net) )은 웹 서비스에 액세스 하는 데 사용할 수 있는 여러 컨트롤을 제공 합니다. 특히 도구 키트에는 `AutoCompleteExtender` JavaScript 코드를 전혀 작성 하지 않고도 웹 서비스를 호출 하 고 페이지에 데이터를 표시 하는 데 사용할 수 있는 이라는 유용한 컨트롤이 포함 되어 있습니다.

AutoCompleteExtender 컨트롤을 사용 하 여 텍스트 상자의 기존 기능을 확장 하 고 사용자가 원하는 데이터를 보다 쉽게 찾을 수 있습니다. 텍스트 상자에 입력 하면 컨트롤을 사용 하 여 웹 서비스를 쿼리하고 텍스트 상자 아래에 결과를 동적으로 표시할 수 있습니다. 그림 4에서는 AutoCompleteExtender 컨트롤을 사용 하 여 지원 응용 프로그램의 고객 id를 표시 하는 예제를 보여 줍니다. 사용자가 텍스트 상자에 다른 문자를 입력 하는 경우 입력에 따라 다른 항목이 아래에 표시 됩니다. 사용자는 원하는 고객 id를 선택할 수 있습니다.

ASP.NET AJAX 페이지 내에서 AutoCompleteExtender를 사용 하려면 웹 사이트의 bin 폴더에 AjaxControlToolkit.dll 어셈블리를 추가 해야 합니다. 도구 키트 어셈블리를 추가한 후에는 해당 어셈블리를 포함 하는 컨트롤을 응용 프로그램의 모든 페이지에서 사용할 수 있도록 web.config에서 참조 하는 것이 좋습니다. web.config의 controls 태그 내에 다음 태그를 추가 하 여이 작업을 수행할 수 있습니다 &lt; &gt; .

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

특정 페이지에서 컨트롤을 사용 해야 하는 경우 web.config를 업데이트 하지 않고 다음과 같이 페이지 맨 위에 참조 지시문을 추가 하 여 참조할 수 있습니다.

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]

[![AutoCompleteExtender 컨트롤을 사용 합니다.](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**그림 4**: AutoCompleteExtender 컨트롤 사용  ([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-web-services/_static/image12.png))

ASP.NET AJAX Toolkit을 사용 하도록 웹 사이트를 구성한 후에는 일반 ASP.NET 서버 컨트롤을 추가 하는 것과 마찬가지로 AutoCompleteExtender 컨트롤을 페이지에 추가할 수 있습니다. 목록 19는 컨트롤을 사용 하 여 웹 서비스를 호출 하는 예제를 보여 줍니다.

**목록 19. ASP.NET AJAX Toolkit AutoCompleteExtender 컨트롤을 사용 합니다.**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

AutoCompleteExtender에는 서버 컨트롤에 있는 표준 ID 및 runat 속성을 비롯 한 여러 가지 속성이 있습니다. 또한 이러한 기능을 사용 하면 웹 서비스에서 데이터에 대해 쿼리 하기 전에 최종 사용자가 입력할 수 있는 문자 수를 정의할 수 있습니다. 목록 19에 표시 된가 수 Prefixlength 속성은 문자를 텍스트 상자에 입력할 때마다 서비스를 호출 합니다. 사용자가 문자를 입력할 때마다 텍스트 상자의 문자와 일치 하는 값을 검색 하기 위해 웹 서비스가 호출 될 때마다이 값을 신중 하 게 설정 하는 것이 좋습니다. 호출 하는 웹 서비스 및 대상 웹 메서드는 각각 ServicePath 및 ServiceMethod 속성을 사용 하 여 정의 됩니다. 마지막으로 TargetControlID 속성은 AutoCompleteExtender 컨트롤을 후크 할 텍스트 상자를 식별 합니다.

호출 되는 웹 서비스는 앞에서 설명한 대로 ScriptService 특성을 적용 해야 하며 대상 웹 메서드는 prefixText 및 count 라는 두 개의 매개 변수를 허용 해야 합니다. PrefixText 매개 변수는 최종 사용자가 입력 한 문자를 나타내고 count 매개 변수는 반환할 항목의 수를 나타냅니다 (기본값은 10). 목록 20에는 앞에서 나열 19의 AutoCompleteExtender 컨트롤에 의해 호출 되는 GetCustomerIDs 웹 메서드의 예제가 나와 있습니다. 웹 메서드는 데이터 필터링을 처리 하 고 일치 하는 결과를 반환 하는 데이터 계층 메서드를 호출 하는 비즈니스 계층 메서드를 호출 합니다. 데이터 계층 메서드의 코드는 목록 21에 표시 되어 있습니다.

**목록 20. AutoCompleteExtender 컨트롤에서 보낸 데이터 필터링**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**목록 21. 최종 사용자 입력을 기준으로 결과를 필터링 합니다.**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>결론

ASP.NET AJAX는 요청 및 응답 메시지를 처리 하는 많은 사용자 지정 JavaScript 코드를 작성 하지 않고도 웹 서비스 호출에 대 한 뛰어난 지원을 제공 합니다. 이 문서에서는 AJAX를 사용 하 여 .NET 웹 서비스를 사용 하 여 JSON 메시지를 처리 하 고 ScriptManager 컨트롤을 사용 하 여 JavaScript 프록시를 정의 하는 방법을 살펴보았습니다. JavaScript 프록시를 사용 하 여 웹 서비스를 호출 하 고, 단순 및 복합 형식을 처리 하 고, 오류를 처리 하는 방법도 살펴보았습니다. 마지막으로, 페이지 메서드를 사용 하 여 웹 서비스 호출의 생성 및 작성 프로세스를 간소화 하는 방법과 AutoCompleteExtender 컨트롤이 입력 하는 최종 사용자에 게 도움을 제공 하는 방법을 살펴보았습니다. ASP.NET AJAX에서 사용할 수 있는 UpdatePanel은 단순성으로 인해 많은 AJAX 프로그래머 들에 게 선택할 수 있는 컨트롤이 될 수 있지만 JavaScript 프록시를 통해 웹 서비스를 호출 하는 방법을 알면 많은 응용 프로그램에서 유용할 수 있습니다.

## <a name="bio"></a>약력

Dan Wahlin (Microsoft에서 가장 중요 한 ASP.NET 및 XML Web Services)는 인터페이스 기술 교육 ()의 .NET 개발 강사 및 아키텍처 컨설턴트입니다 [http://www.interfacett.com](http://www.interfacett.com) . Dan은 ASP.NET 개발자 용 XML 웹 사이트 ([www.XMLforASP.NET](http://www.XMLforASP.NET))가 INETA 스피커의 기관에 있으며 여러 회의를 말합니다. Dan 공동 작성 Wrox (전문가 Windows DNA), ASP.NET: 팁, 자습서 및 코드 (Sams teach yourself), ASP.NET 1.1 Insider Solutions, ASP.NET (전문 Wrox 2.0 AJAX), ASP.NET 2.0 MVP 해킹 및 제작한 XML for ASP.NET 개발자 (sams teach yourself). 코드, 문서 또는 책을 작성 하지 않을 때 Dan은 음악을 작성 하 고 기록 하 고 아내 및 어린이와 함께 golf 및 농구를 재생 하는 것을 활용할.

Scott Cate cda (는 1997부터 Microsoft 웹 기술을 사용 하 고 있으며 기술 자료 소프트웨어 솔루션에 초점을 맞춘 ASP.NET 기반 응용 프로그램을 전문적으로 작성 하는[www.myKB.com](http://www.myKB.com)(myKB.com)의 부사장입니다. Scott은 전자 메일을 통해 [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 또는 [ScottCate.com](http://ScottCate.com) 의 블로그를 통해 연락할 수 있습니다.

> [!div class="step-by-step"]
> [이전](understanding-asp-net-ajax-localization.md)
> [다음](understanding-asp-net-ajax-debugging-capabilities.md)
