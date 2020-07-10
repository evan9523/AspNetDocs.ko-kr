---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: ASP.NET MVC 2의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 ASP.NET MVC 2에 도입 된 새로운 기능 및 향상 된 기능에 대해 설명 합니다. 이 문서도 다운로드할 수 있습니다.
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: 1a0a29241d8afecd295b11013b27621b21c9ed52
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162715"
---
# <a name="whats-new-in-aspnet-mvc-2"></a>ASP.NET MVC 2의 새로운 기능

> 이 문서에서는 ASP.NET MVC 2에 도입 된 새로운 기능 및 향상 된 기능에 대해 설명 합니다. 이 문서도 [다운로드할](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf) 수 있습니다.

[간략하게](#_TOC1)   
[ASP.NET MVC 1.0 프로젝트를 ASP.NET MVC 2로 업그레이드](#_TOC2)   
[새 기능](#_TOC3)   
[템플릿 기반 도우미](#_TOC3_1)   
[영역인](#_TOC3_2)   
[비동기 컨트롤러에 대 한 지원](#_TOC3_3)   
[작업 메서드 매개 변수에서 DefaultValueAttribute 지원](#_TOC3_4)   
[모델 바인더를 사용 하 여 이진 데이터 바인딩 지원](#_TOC3_5)   
[ModelMetadata 및 ModelMetadataProvider 클래스](#_TOC3_6)   
[DataAnnotations 특성에 대 한 지원](#_TOC3_7)   
[모델 유효성 검사기 공급자](#_TOC3_8)   
[클라이언트 쪽 유효성 검사](#_TOC3_9)   
[Visual Studio 2010에 대 한 새 코드 조각](#_TOC3_10)   
[새 RequireHttpsAttribute 작업 필터](#_TOC3_11)   
[HTTP 메서드 동사 재정의](#_TOC3_12)   
[템플릿 도우미에 대 한 새 HiddenInputAttribute 클래스](#_TOC3_13)   
[ValidationSummary 도우미 메서드는 모델 수준 오류를 표시할 수 있습니다.](#_TOC3_14)   
[Visual Studio의 T4 템플릿은 .NET Framework API 향상의 대상 버전과 관련 된 코드를 생성](#_TOC3_15)[API Improvements](#_TOC4) 합니다.  
[주요 변경 내용](#_TOC5)  
[고지 사항](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>간략하게

ASP.NET MVC 2는 ASP.NET MVC 1.0을 기반으로 하며 생산성 향상에 중점을 두는 다양 한 향상 된 기능 및 기능을 소개 합니다. 이 릴리스는 ASP.NET MVC 1.0와 호환 되므로 ASP.NET MVC 1.0의 모든 기술 자료, 기술, 코드 및 확장이 계속 적용 됩니다.

ASP.NET MVC에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [MSDN의 ASP.NET MVC 설명서](https://go.microsoft.com/fwlink/?LinkId=159758)
- [ASP.NET MVC 웹 사이트](https://asp.net/mvc/)
- [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>ASP.NET MVC 1.0 프로젝트를 ASP.NET MVC 2로 업그레이드

ASP.NET MVC 2는 동일한 서버에 ASP.NET MVC 1.0와 함께 설치할 수 있습니다. 그러면 응용 프로그램 개발자가 ASP.NET MVC 1.0 응용 프로그램을 ASP.NET MVC 2로 업그레이드할 시기를 유연 하 게 선택할 수 있습니다. 업그레이드 하는 방법에 대 한 자세한 내용은 [ASP.NET mvc 1.0 응용 프로그램을 ASP.NET mvc 2로 업그레이드](https://go.microsoft.com/fwlink/?LinkID=185459)문서를 참조 하세요.

## <a name="new-features"></a><a id="_TOC3"></a>새 기능

이 섹션에서는 MVC 2 릴리스에 도입 된 기능을 설명 합니다.

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>템플릿 기반 도우미

템플릿 기반 도우미를 사용 하면 편집 및 표시를 위해 HTML 요소를 데이터 형식과 자동으로 연결할 수 있습니다. 예를 들어 DateTime 형식의 데이터가 뷰에 표시 되는 경우에는 날짜 선택 UI 요소가 자동으로 렌더링 될 수 있습니다. 이는 ASP.NET Dynamic Data에서 필드 템플릿이 작동 하는 방법과 비슷합니다. 자세한 내용은 MSDN 웹 사이트에서 [템플릿 기반 도우미를 사용 하 여 데이터 표시](https://go.microsoft.com/fwlink/?LinkId=159062) 를 참조 하세요.

### <a name="areas"></a><a id="_TOC3_2"></a>영역인

영역을 사용 하면 많은 수의 작은 섹션으로 많은 프로젝트를 구성 하 여 규모가 많은 웹 응용 프로그램의 복잡성을 관리할 수 있습니다. 각 섹션 ("영역")은 일반적으로 규모가 많은 웹 사이트의 개별 섹션을 나타내며 관련 컨트롤러 및 뷰 집합을 그룹화 하는 데 사용 됩니다. 자세한 내용은 연습: MSDN 웹 사이트의 [영역별로 ASP.NET MVC 응용 프로그램 구성](https://go.microsoft.com/fwlink/?LinkId=158978) 을 참조 하세요.

새 영역을 만들려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 추가를 클릭 한 다음 영역을 클릭 합니다. 그러면 영역 이름을 입력 하 라는 대화 상자가 표시 됩니다. 영역 이름을 입력 하면 Visual Studio에서 프로젝트에 새 영역을 추가 합니다.

다음 그림은 두 개의 영역, 즉 관리자와 블로그를 포함 하는 프로젝트의 레이아웃 예를 보여 줍니다.

![](what-is-new-in-aspnet-mvc/_static/image1.png)

영역을 만들 때 Visual Studio는 AreaRegistration에서 파생 되는 클래스를 각 영역에 추가 합니다. 이 클래스는 다음 예제와 같이 영역과 해당 경로를 등록 하는 데 필요 합니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

ASP.NET MVC 2의 기본 프로젝트 템플릿에는 Global.asax 파일의 코드에 있는 RegisterAllAreas 메서드에 대 한 호출이 포함 되어 있습니다. 이 메서드는 AreaRegistration 클래스에서 파생 되는 모든 형식을 검색 하 여 형식의 인스턴스를 인스턴스화한 다음 인스턴스에서 RegisterArea 메서드를 호출 하 여 프로젝트의 각 영역을 등록 합니다. 다음 예제에서는이 작업을 수행 하는 방법을 보여 줍니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

컨텍스트를 호출 하 여 RegisterArea 메서드에 네임 스페이스를 지정 하지 않는 경우 네임 스페이스. Add 메서드, 등록 클래스의 네임 스페이스는 기본적으로 사용 됩니다.

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>비동기 컨트롤러에 대 한 지원

이제 ASP.NET MVC 2를 사용 하 여 컨트롤러에서 요청을 비동기적으로 처리할 수 있습니다. 이로 인해 차단 작업 (예: 네트워크 요청)을 자주 호출 하 여 차단 되지 않는 요소를 호출 하는 서버를 허용 하 여 성능이 향상 될 수 있습니다. 자세한 내용은 MSDN의 [ASP.NET MVC에서 비동기 컨트롤러 사용](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) 항목을 참조 하세요.

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>작업 메서드 매개 변수에서 DefaultValueAttribute 지원

System.componentmodel 클래스를 사용 하면 인수 매개 변수에 대 한 기본값을 동작 메서드에 제공할 수 있습니다. 예를 들어 다음 기본 경로가 정의 되어 있다고 가정 합니다.

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.json)]

또한 다음과 같은 컨트롤러 및 작업 메서드가 정의 되어 있다고 가정 합니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

다음 요청 Url은 앞의 예제에 정의 된 보기 작업 메서드를 호출 합니다.

- /Article/View/123
- /Article/View/123? page = 1 (이전 요청과 효과적으로 같음)
- /Article/View/123? page = 2

DefaultValueAttribute 특성이 없으면 페이지 인수가 값이 제공 되지 않은 null을 허용 하지 않는 값 형식 이므로 이전 목록의 첫 번째 URL이 작동 하지 않습니다.

코드가 Visual Basic 2010 또는 Visual c # 2010로 작성 된 경우 다음 예제와 같이 DefaultValueAttribute 특성 대신 선택적 매개 변수를 사용할 수 있습니다.

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>모델 바인더를 사용 하 여 이진 데이터 바인딩 지원

Base-64로 인코딩된 문자열로 이진 값을 인코딩하는 Html. 숨겨진 도우미의 새 오버 로드가 다음과 같이 두 가지 있습니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

일반적인 용도는 개체에 대 한 타임 스탬프를 뷰에 포함 하는 것입니다. 예를 들어 응용 프로그램에 다음 제품 개체가 포함 될 수 있습니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

편집 폼은 다음 예제와 같이 폼에서 타임 스탬프 속성을 렌더링할 수 있습니다.

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

이 태그는 타임 스탬프 값을 포함 하는 숨겨진 input 요소를 다음 예제와 유사한 base-64로 인코딩된 문자열로 렌더링 합니다.

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

이 폼은 다음 예제와 같이 Product 형식의 인수를 포함 하는 작업 메서드에 게시 될 수 있습니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

작업 메서드에서 게시 된 base-64로 인코딩된 문자열을 바이트 배열로 변환 하기 때문에 TimeStamp 속성이 올바르게 채워집니다.

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>ModelMetadata 및 ModelMetadataProvider 클래스

ModelMetadataProvider 클래스는 뷰 내에서 모델에 대 한 메타 데이터를 가져오기 위한 추상화를 제공 합니다. MVC 2에는 System.componentmodel 네임 스페이스의 특성에 의해 노출 되는 메타 데이터를 사용할 수 있도록 하는 기본 공급자가 포함 되어 있습니다. 데이터베이스 또는 XML 파일과 같은 다른 데이터 저장소에서 메타 데이터를 제공 하는 메타 데이터 공급자를 만들 수 있습니다.

ViewDataDictionary 클래스는 ModelMetadataProvider 클래스에 의해 모델에서 추출 된 메타 데이터를 포함 하는 ModelMetadata 개체를 노출 합니다. 이렇게 하면 템플릿 기반 도우미가이 메타 데이터를 사용 하 고 그에 따라 출력을 조정할 수 있습니다.

자세한 내용은 [Modelmetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) 및 [modelmetadataprovider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) 클래스에 대 한 설명서를 참조 하세요.

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>DataAnnotations 특성에 대 한 지원

ASP.NET MVC 2는 입력 유효성 검사를 제공 하기 위해 모델에 바인딩할 때 범위 특성, RequiredAttribute, StringLengthAttribute 및 RegexAttribute 유효성 검사 특성 (System.componentmodel 네임 스페이스에 정의 됨)을 사용할 수 있도록 지원 합니다.

자세한 내용은 MSDN 웹 사이트에서 [방법: Dataannotations을 사용 하 여 모델 데이터 유효성 검사 특성](https://go.microsoft.com/fwlink/?LinkId=159063) 을 참조 하세요. 이러한 특성의 사용을 보여 주는 샘플 프로젝트는에서 다운로드할 수 있습니다 [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) .

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>모델 유효성 검사기 공급자

모델 유효성 검사 공급자 클래스는 모델에 대 한 유효성 검사 논리를 제공 하는 추상화를 나타냅니다. ASP.NET MVC에는 System.componentmodel annotation 네임 스페이스에 포함 된 유효성 검사 특성을 기반으로 하는 기본 공급자가 포함 되어 있습니다. 모델에 대 한 유효성 검사 규칙의 사용자 지정 매핑과 사용자 지정 유효성 검사 규칙을 정의 하는 고유한 유효성 검사 공급자를 만들 수도 있습니다. 자세한 내용은 [ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) 클래스에 대 한 설명서를 참조 하세요.

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>클라이언트 쪽 유효성 검사

모델 유효성 검사기 공급자 클래스는 클라이언트 쪽 유효성 검사 라이브러리에서 사용할 수 있는 JSON 직렬화 된 데이터 형식으로 브라우저에 유효성 검사 메타 데이터를 노출 합니다. ASP.NET MVC 2에는 앞에서 설명한 DataAnnotations 네임 스페이스 유효성 검사 특성을 지 원하는 클라이언트 유효성 검사 라이브러리 및 어댑터가 포함 되어 있습니다. 공급자 클래스를 사용 하 여 JSON 데이터를 처리 하 고 대체 라이브러리로 호출 하는 어댑터를 작성 하 여 다른 클라이언트 유효성 검사 라이브러리를 사용할 수도 있습니다.

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>Visual Studio 2010에 대 한 새 코드 조각

ASP.NET MVC 2에 대 한 일련의 HTML 코드 조각이 Visual Studio 2010와 함께 설치 됩니다. 이러한 코드 조각의 목록을 보려면 도구 메뉴에서 코드 조각 관리자를 선택 합니다. 언어에 대해 HTML을 선택 하 고 위치에서 ASP.NET MVC 2를 선택 합니다. 코드 조각을 사용 하는 방법에 대 한 자세한 내용은 Visual Studio 설명서를 참조 하세요.

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>새 RequireHttpsAttribute 작업 필터

ASP.NET MVC 2에는 작업 메서드 및 컨트롤러에 적용할 수 있는 새 RequireHttpsAttribute 클래스가 포함 되어 있습니다. 기본적으로이 필터는 비 SSL (HTTP) 요청을 SSL 사용 (HTTPS)으로 리디렉션합니다.

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>HTTP 메서드 동사 재정의

REST 아키텍처 스타일을 사용 하 여 웹 사이트를 빌드할 때 HTTP 동사는 리소스에 대해 수행할 작업을 결정 하는 데 사용 됩니다. REST를 사용 하려면 응용 프로그램이 GET, PUT, POST 및 DELETE를 비롯 한 일반적인 HTTP 동사의 전체 범위를 지원 해야 합니다.

ASP.NET MVC 2에는 작업 메서드에 적용할 수 있는 새로운 특성과 해당 기능 compact 구문이 포함 되어 있습니다. 이러한 특성을 통해 ASP.NET MVC는 HTTP 동사를 기반으로 작업 메서드를 선택할 수 있습니다. 다음 예제에서 POST 요청은 첫 번째 작업 메서드를 호출 하 고 PUT 요청은 두 번째 작업 메서드를 호출 합니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

이전 버전의 ASP.NET MVC에서 이러한 작업 메서드는 다음 예제와 같이 더 자세한 구문이 필요 합니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

브라우저는 GET 및 POST HTTP 동사로 지원 하기 때문에 다른 동사가 필요한 작업에 게시할 수 없습니다. 따라서 기본적으로 모든 RESTful 요청을 지원할 수는 없습니다.

그러나 POST 작업 중에 RESTful 요청을 지원 하기 위해 ASP.NET MVC 2는 새로운 HttpMethodOverride HTML 도우미 메서드를 소개 합니다. 이 메서드는 폼에서 HTTP 메서드를 효과적으로 에뮬레이트하는 숨겨진 input 요소를 렌더링 합니다. 예를 들어 HttpMethodOverride HTML 도우미 메서드를 사용 하 여 양식 제출이 PUT 또는 DELETE 요청으로 표시 되도록 할 수 있습니다. HttpMethodOverride의 동작은 다음 특성에 영향을 줍니다.

- HttpPostAttribute
- HttpPutAttribute
- HttpGetAttribute
- HttpDeleteAttribute
- AcceptVerbsAttribute

숨겨진 input 요소는 해당 이름을 X-HTTP 메서드 재정의로 설정 하 고 해당 값을 에뮬레이션할 HTTP 동사로 설정 합니다. 재정의 값은 HTTP 헤더 또는 쿼리 문자열 값에서 이름/값 쌍으로 지정할 수도 있습니다.

이 재정의는 실제 요청이 POST 요청인 경우에만 사용할 수 있습니다. 다른 HTTP 동사를 사용 하는 요청에 대해서는 재정의 값이 무시 됩니다.

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>템플릿 도우미에 대 한 새 HiddenInputAttribute 클래스

모델 속성에 새 HiddenInputAttribute 특성을 적용 하 여 편집기 템플릿에 모델을 표시할 때 숨겨진 input 요소를 렌더링할지 여부를 지정할 수 있습니다. 특성은 HiddenInput의 암시적 UIHint 값을 설정 합니다. 특성의 DisplayValue 속성을 사용 하 여 편집기 및 디스플레이 모드에서 값을 표시할지 여부를 지정할 수 있습니다. DisplayValue를 false로 설정 하면 일반적으로 필드를 둘러싸는 HTML 태그 뿐만 아니라 아무것도 표시 되지 않습니다. DisplayValue의 기본값은 true입니다.

다음 시나리오에서 HiddenInputAttribute 특성을 사용할 수 있습니다.

- 뷰를 통해 사용자가 개체의 ID를 편집할 수 있으며, 값을 표시 하 고, 이전 ID를 포함 하는 숨겨진 input 요소를 제공 하 여 컨트롤러에 다시 전달할 수 있도록 해야 합니다.
- 뷰를 사용 하 여 timestamp 속성과 같이 사용자가 표시 되지 않아야 하는 이진 속성을 편집할 수 있습니다. 이 경우 값과 주변 HTML 태그 (예: 레이블 및 값)가 표시 되지 않습니다.

다음 예제에서는 HiddenInputAttribute 클래스를 사용 하는 방법을 보여 줍니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

특성을 true로 설정 하거나 매개 변수를 지정 하지 않은 경우 다음 작업이 수행 됩니다.

- 표시 템플릿에서 레이블이 렌더링 되 고 사용자에 게 값이 표시 됩니다.
- 편집기 템플릿에서 레이블이 렌더링 되 고 숨겨진 input 요소에서 값이 렌더링 됩니다.

특성을 false로 설정 하면 다음 작업이 수행 됩니다.

- 표시 템플릿에서는 해당 필드에 대해 아무것도 렌더링 되지 않습니다.
- 편집기 템플릿에서는 레이블이 렌더링 되지 않으며 값이 숨겨진 input 요소에 렌더링 됩니다.

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>ValidationSummary 도우미 메서드는 모델 수준 오류를 표시할 수 있습니다.

모든 유효성 검사 오류를 항상 표시 하는 대신 ValidationSummary 도우미 메서드에 모델 수준 오류만 표시 하는 새로운 옵션이 있습니다. 이렇게 하면 각 필드 옆에 표시 될 유효성 검사 요약 및 필드 관련 오류에 모델 수준 오류가 표시 됩니다.

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>Visual Studio의 T4 템플릿은 .NET Framework 대상 버전과 관련 된 코드를 생성 합니다.

응용 프로그램에서 사용 하는 .NET Framework 버전을 지정 하는 ASP.NET MVC T4 호스트의 T4 파일에 새 속성을 사용할 수 있습니다. 이렇게 하면 T4 템플릿이 .NET Framework 버전에 해당 하는 코드와 태그를 생성할 수 있습니다. Visual Studio 2008에서 값은 항상 .NET 3.5입니다. Visual Studio 2010에서 값은 .NET 3.5 또는 .NET 4입니다.

## <a name="api-improvements"></a><a id="_TOC4"></a>API 향상

이 섹션에서는 기존 ASP.NET MVC 형식 및 멤버의 변경 내용에 대해 설명 합니다.

- Controller 클래스에 보호 된 가상 CreateActionInvoker 메서드를 추가 했습니다. 이 메서드는 컨트롤러의 ActionInvoker 속성에 의해 호출 되며 호출자가 이미 설정 되지 않은 경우 호출자의 지연 인스턴스화를 허용 합니다.
- AuthorizeAttribute 클래스에 보호 된 가상 HandleUnauthorizedRequest 메서드를 추가 했습니다. 이렇게 하면 권한 부여가 실패할 때 AuthorizeAttribute에서 파생 되는 필터가 동작을 제어할 수 있습니다.
- ValueProviderDictionary 클래스에서 추가 (문자열 키, 개체 값) 메서드를 추가 했습니다. 이렇게 하면 다음 예제와 같이 ValueProviderDictionary에 대 한 사전 이니셜라이저 구문을 사용할 수 있습니다.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- \_AjaxContext 클래스에 get object 메서드를 추가 했습니다. Get data 메서드와 비슷한 JavaScript 메서드입니다. \_ 응답의 콘텐츠 형식이 application/json 인 경우 get \_ OBJECT는 json 개체를 반환 합니다.
- AuthorizationContext 클래스에서 ActionDescriptor 속성을 추가 했습니다.
- UrlParameter를 추가 했습니다. 폼 게시에 속성이 없을 때 ID 속성이 포함 된 모델에 바인딩할 때 문제를 해결 하는 데 사용할 수 있는 선택적 토큰입니다. 자세한 내용은 Phil Haack의 블로그에서 [ASP.NET MVC 2 선택적 URL 매개 변수](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) 항목을 참조 하세요.

## <a name="breaking-changes"></a><a id="_TOC5"></a>주요 변경 내용

다음 변경 내용으로 인해 기존 ASP.NET MVC 1.0 응용 프로그램에서 오류가 발생할 수 있습니다.

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>IDataErrorInfo을 구현 하는 클래스에 대 한 속성 유효성 검사 동작 변경

IDataErrorInfo를 사용 하 여 유효성 검사를 수행 하는 모델 개체의 경우 새 값이 설정 되었는지 여부에 관계 없이 모든 속성의 유효성이 검사 됩니다. ASP.NET MVC 1.0에서는 새 값 집합이 설정 된 속성만 확인 되었습니다. ASP.NET MVC 2에서 IDataErrorInfo의 Error 속성은 모든 속성 유효성 검사기가 성공한 경우에만 호출 됩니다.

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>IIS 스크립트 매핑 스크립트는 설치 관리자에서 더 이상 사용할 수 없습니다.

IIS 스크립트 매핑 스크립트는 클래식 모드에서 iis 6 및 iis 7에 대 한 스크립트 맵을 구성 하는 데 사용 되는 명령줄 스크립트입니다. Visual Studio 개발 서버를 사용 하거나 통합 모드에서 IIS 7을 사용 하는 경우 스크립트 매핑 스크립트가 필요 하지 않습니다. 스크립트는 [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)에서 별도의 지원 되지 않는 다운로드로 사용할 수 있습니다.

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>MVC 퓨처의 Html. 대체 도우미 메서드는 더 이상 사용할 수 없습니다.

MVC 뷰 엔진의 렌더링 동작 변경으로 인해 Html. 대체 도우미 메서드는 작동 하지 않고 제거 되었습니다.

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>IValueProvider 인터페이스는 IDictionary의 모든 용도를 대체 합니다.

MVC 1.0에서 IDictionary를 수락한 모든 속성 또는 메서드 인수는 이제 IValueProvider를 허용 합니다. 이 변경 내용은 사용자 지정 값 공급자 또는 사용자 지정 모델 바인더를 포함 하는 응용 프로그램에만 적용 됩니다. 이러한 변경의 영향을 받는 속성 및 메서드의 예는 다음과 같습니다.

- ControllerBase 및 ModelBindingContext 클래스의 ValueProvider 속성입니다.
- Controller 클래스의 TryUpdateModel 메서드

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>새 CSS 클래스가 사이트 .css 파일에 추가 되었습니다.

ASP.NET MVC 프로젝트 템플릿의 사이트 .css 파일은 유효성 검사 기능 및 템플릿 기반 도우미에서 사용 하는 새 스타일을 포함 하도록 업데이트 되었습니다.

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>이제 도우미가 MvcHtmlString 개체를 반환 합니다.

ASP.NET 4에서 새로운 HTML 인코딩 식 구문을 활용 하기 위해 이제는 HTML 도우미의 반환 형식이 문자열 대신 MvcHtmlString 됩니다. ASP.NET MVC 2를 사용 하 고 ASP.NET 3.5에서 새 도우미를 사용 하는 경우에는 HTML 인코딩 구문을 활용할 수 없습니다. 새 구문은 ASP.NET 4에서 ASP.NET MVC 2를 실행 하는 경우에만 사용할 수 있습니다.

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>이제 JsonResult는 HTTP POST 요청에만 응답 합니다.

정보 공개 가능성이 있는 JSON 하이재킹 공격을 완화 하기 위해 기본적으로 JsonResult 클래스는 이제 HTTP POST 요청에만 응답 합니다. JsonResult 개체를 반환 하는 작업 메서드에 대 한 Ajax GET 호출은 POST를 대신 사용 하도록 변경 해야 합니다. 필요한 경우 JsonResult의 새 JsonRequestBehavior 속성을 설정 하 여이 동작을 재정의할 수 있습니다. 잠재적 악용에 대 한 자세한 내용은 블로그 게시물 Phil Haack의 [블로그 게시물을](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) 참조 하세요.

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>ModelBindingContext의 모델 및 ModelType 속성 setter는 사용 되지 않습니다.

ModelBindingContext 클래스에 설정 가능한 새 ModelMetadata 속성이 추가 되었습니다. 새 속성은 모델과 ModelType 속성을 모두 캡슐화 합니다. Model 및 ModelType 속성은 더 이상 사용 되지 않지만 이전 버전과의 호환성을 위해 속성 getter가 여전히 작동 합니다. ModelMetadata 속성에 위임 하 여 값을 검색 합니다.

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>DefaultControllerFactory 클래스에 대 한 변경 내용에서 파생 된 사용자 지정 컨트롤러 팩터리가 중단 됩니다.

RequestContext 속성을 제거 하 여 DefaultControllerFactory 클래스를 수정 했습니다. 이 속성 대신 요청 컨텍스트 인스턴스가 보호 된 가상 GetControllerInstance 및 Getcontrollerinstance 메서드에 전달 됩니다. 이 변경 내용은 DefaultControllerFactory에서 파생 된 사용자 지정 컨트롤러 팩터리에 영향을 줍니다.

사용자 지정 컨트롤러 팩터리는 ASP.NET MVC 응용 프로그램에 대 한 종속성 주입을 제공 하는 데 주로 사용 됩니다. ASP.NET MVC 2를 지원 하도록 사용자 지정 컨트롤러 팩터리를 업데이트 하려면 새 서명과 일치 하도록 메서드 시그니처 또는 시그니처를 변경 하 고 속성 대신 요청 컨텍스트 매개 변수를 사용 합니다.

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>이제 "Area"는 예약 된 경로 값 키입니다.

이제 경로 값의 "영역" 문자열은 "controller" 및 "action"과 동일한 방식으로 ASP.NET MVC에서 특별 한 의미를 갖습니다. 한 가지 의미는 HTML 도우미가 "영역"을 포함 하는 경로 값 사전과 함께 제공 되는 경우 도우미는 더 이상 쿼리 문자열에 "영역"을 추가 하지 않습니다.

영역 기능을 사용 하는 경우 경로 URL의 일부로 {area}를 사용 하지 않도록 해야 합니다.

## <a name="disclaimer"></a><a id="_TOC6"></a>내용을

본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.

이 문서에 포함된 정보는 게시 날짜 당시 논의된 문제에 대한 Microsoft Corporation의 현재 관점을 나타냅니다. Microsoft는 변화하는 시장 상황에 대응해야 하므로 Microsoft의 약속으로 해석되지 않아야 하며, Microsoft는 게시 날짜 이후 제시된 정보의 정확성을 보증하지 않습니다.

이 백서는 정보 제공만을 목적으로 합니다. Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.

해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나 검색 시스템에 저장 또는 도입되거나 전송될 수 없습니다.

Microsoft는 이 설명서 본안에 관련된 특허권, 상표권, 저작권, 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 설명서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권 또는 기타 지적 재산권 등에 대한 어떠한 사용권도 허용하지 않습니다.

별도로 언급 하지 않는 한, 용례에 사용 된 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트는 실제 데이터가 아닙니다. 어떠한 실제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 또는 이벤트와도 연관 시킬 의도가 없으며 그렇게 유추 해서도 안 됩니다.

© 2010 Microsoft Corporation. All rights reserved.

Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.

여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.
