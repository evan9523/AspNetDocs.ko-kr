---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 및 Visual Studio 2012의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 ASP.NET 4.5에 도입 된 새로운 기능 및 향상 된 기능에 대해 설명 합니다. 웹 개발을 위한 향상 된 기능에 대해서도 설명 합니다.
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345407"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 및 Visual Studio 2012의 새로운 기능

> 이 문서에서는 ASP.NET 4.5에 도입 된 새로운 기능 및 향상 된 기능에 대해 설명 합니다. Visual Studio 2012에서 웹 개발을 위한 향상 된 기능에 대해서도 설명 합니다. 이 문서는 원래 2012 년 2 월 29 일에 게시 되었습니다.

- [ASP.NET Core 런타임 및 프레임 워크](#_Toc318097372)

    - [HTTP 요청 및 응답을 비동기적으로 읽고 씁니다.](#_Toc318097373)
    - [HttpRequest 처리에 대 한 향상 된 기능](#_Toc318097374)
    - [비동기 응답 플러시](#_Toc318097375)
    - [*Wait* 및 *작업*기반 비동기 모듈 및 처리기 지원](#_Toc318097376)
    - [비동기 HTTP 모듈](#_Toc318097377)
    - [비동기 HTTP 처리기](#_Toc318097378)
    - [새 ASP.NET Request 유효성 검사 기능](#_Toc318097379)
    - [지연 된 ("지연") 요청 유효성 검사](#_Toc318097380)
    - [유효성 검사 요청에 대 한 지원](#_Toc318097381)
    - [Xss 라이브러리 방지](#_Toc318097382)
    - [Websocket 프로토콜에 대 한 지원](#_Toc318097383)
    - [묶음 및 축소](#_Toc318097384)
    - [웹 호스팅에 대 한 성능 향상](#_Toc_perf)

        - [주요 성능 요소](#_Toc_perf_1)
        - [새 성능 기능에 대 한 요구 사항](#_Toc_perf_2)
        - [공용 어셈블리 공유](#_Toc_perf_3)
        - [더 빠른 시작을 위해 멀티 코어 JIT 컴파일 사용](#_Toc_perf_4)
        - [메모리 최적화를 위한 가비지 수집 튜닝](#_Toc_perf_5)
        - [웹 응용 프로그램 프리페치](#_Toc_perf_6)
- [ASP.NET Web Forms](#_Toc318097385)

    - [강력한 형식의 데이터 컨트롤](#_Toc318097386)
    - [모델 바인딩](#_Toc318097387)

        - [데이터 선택](#_Toc318097388)
        - [값 공급자](#_Toc318097389)
        - [컨트롤에서 값으로 필터링](#_Toc318097390)
    - [HTML로 인코딩된 Data-Binding 식](#_Toc318097391)
    - [조심 스럽게 유효성 검사](#_Toc318097392)
    - [HTML5 업데이트](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET 웹 페이지 2](#_Toc318097395)
- [Visual Studio 2012 릴리스 후보](#_Toc318097396)

    - [Visual Studio 2010와 Visual Studio 2012 릴리스 후보 간의 프로젝트 공유 (프로젝트 호환성)](#project-compatibility)
    - [ASP.NET 4.5 웹 사이트 템플릿의 구성 변경 내용](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [IIS 7 for ASP.NET 라우팅의 기본 지원](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML 편집기](#_Toc318097397)

        - [스마트 작업](#_Toc318097398)
        - [WAI-ARIA 지원](#_Toc318097399)
        - [새 HTML5 코드 조각](#_Toc318097400)
        - [사용자 정의 컨트롤로 추출](#_Toc318097401)
        - [특성의 코드 너 깃 IntelliSense](#_Toc318097402)
        - [여는 태그 또는 닫는 태그의 이름을 바꿀 때 일치 하는 태그의 자동 이름 바꾸기](#_Toc318097403)
        - [이벤트 처리기 생성](#_Toc318097404)
        - [스마트 들여쓰기](#_Toc318097405)
        - [문 완성 자동 줄이기](#_Toc318097406)
    - [JavaScript 편집기](#_Toc318097407)

        - [코드 개요](#_Toc318097408)
        - [중괄호 일치](#_Toc318097409)
        - [정의로 이동](#_Toc318097410)
        - [ECMAScript5 지원](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [VSDOC 서명 오버 로드](#_Toc318097413)
        - [암시적 참조](#_Toc318097414)
    - [CSS 편집기](#_Toc318097415)

        - [문 완성 자동 줄이기](#_Toc318097416)
        - [계층적 들여쓰기.](#_Toc318097417)
        - [CSS 해킹 지원](#_Toc318097418)
        - [공급 업체별 스키마 (-moz-,-webkit)](#_Toc318097419)
        - [주석 달기 및 주석 처리 지원](#_Toc318097420)
        - [색 선택기](#_Toc318097421)
        - [조각](#_Toc318097422)
        - [사용자 지정 지역](#_Toc318097423)
    - [페이지 검사기](#_Toc318097424)
    - [게시](#_Toc318097425)

        - [게시 프로필](#_Toc318097426)
        - [ASP.NET 미리 컴파일 및 병합](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [고지 사항](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET Core 런타임 및 프레임 워크

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>HTTP 요청 및 응답을 비동기적으로 읽고 씁니다.

ASP.NET 4에서는 *HttpRequest GetBufferlessInputStream* 메서드를 사용 하 여 HTTP 요청 엔터티를 스트림으로 읽는 기능을 도입 했습니다. 이 메서드는 요청 엔터티에 대 한 스트리밍 액세스를 제공 합니다. 그러나 요청 기간 동안 스레드를 연결 하는 동기적으로 실행 됩니다.

ASP.NET 4.5는 HTTP 요청 엔터티에서 비동기적으로 스트림을 읽는 기능 및 비동기적으로 플러시하는 기능을 지원 합니다. ASP.NET 4.5는 또한 .aspx 페이지 처리기 및 ASP.NET MVC 컨트롤러와 같은 다운스트림 HTTP 처리기와 쉽게 통합할 수 있는 HTTP 요청 엔터티를 이중 버퍼링 할 수 있는 기능을 제공 합니다.

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HttpRequest 처리에 대 한 향상 된 기능

GetBufferlessInputStream에서 ASP.NET 4.5에 의해 반환 된 스트림 참조는 동기 및 비동기 읽기 메서드를 모두 지원 합니다 *.* 이제 *GetBufferlessInputStream* 에서 반환 된 *스트림* 개체가 system.io.stream.beginread 및 EndRead 메서드를 모두 구현 합니다. 비동기 *스트림* 메서드를 사용 하면 비동기적으로 요청 엔터티를 읽을 수 있으며, ASP.NET는 비동기 읽기 루프의 각 반복 사이에 현재 스레드를 해제 합니다.

또한 ASP.NET 4.5는 버퍼링 된 방식으로 요청 엔터티를 읽기 위한 도우미 메서드를 추가 했습니다. *HttpRequest. GetBufferedInputStream*. 이 새 오버 로드는 동기 및 비동기 읽기를 모두 지 원하는 *GetBufferlessInputStream*처럼 작동 합니다. 그러나 읽을 때 *GetBufferedInputStream* 는 또한 엔터티 바이트를 ASP.NET 내부 버퍼에 복사 하 여 다운스트림 모듈 및 처리기가 요청 엔터티에 계속 액세스할 수 있도록 합니다. 예를 들어 파이프라인의 일부 업스트림 코드가 이미 *GetBufferedInputStream*를 사용 하 여 요청 엔터티를 읽은 경우 *HttpRequest* 또는 *HttpRequest*를 계속 사용할 수 있습니다. 이를 통해 요청에 대 한 비동기 처리를 수행할 수 있습니다 (예: 데이터베이스에 대 한 대량 파일 업로드 스트리밍). 그러나 이후에 .aspx 페이지 및 MVC ASP.NET 컨트롤러를 실행 합니다.

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>비동기 응답 플러시

클라이언트가 멀리 떨어져 있거나 낮은 대역폭 연결을 사용 하는 경우 HTTP 클라이언트에 응답을 보내는 데 상당한 시간이 걸릴 수 있습니다. 일반적으로 ASP.NET는 응용 프로그램에 의해 생성 되는 응답 바이트를 버퍼링 합니다. 그런 다음 ASP.NET는 요청 처리의 끝에서 계산 된 버퍼의 단일 송신 작업을 수행 합니다.

버퍼링 된 응답이 크면 (예: 클라이언트에 대 한 대량 파일 스트리밍) *httpresponse.cache* 를 주기적으로 호출 하 여 버퍼링 된 출력을 클라이언트로 보내고 메모리 사용을 제어 합니다. 그러나 *플러시가* 동기 호출 이기 때문에 *플러시* 를 반복적으로 호출 하면 잠재적으로 장기 실행 되는 요청 기간 동안 스레드가 계속 사용 됩니다.

ASP.NET 4.5는 *httpresponse.cache* 클래스의 *Beginflush* 및 *endflush* 메서드를 사용 하 여 비동기적으로 플러시를 수행 하기 위한 지원을 추가 합니다. 이러한 메서드를 사용 하 여 운영 체제 스레드를 사용 하지 않고 클라이언트에 데이터를 증분 방식으로 보내는 비동기 모듈 및 비동기 처리기를 만들 수 있습니다. *Beginflush* 와 *endflush* 호출 사이에서 ASP.NET는 현재 스레드를 해제 합니다. 이렇게 하면 장기 실행 HTTP 다운로드를 지 원하는 데 필요한 총 활성 스레드 수가 크게 줄어듭니다.

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>*Wait* 및 *작업* 기반 비동기 모듈 및 처리기 지원

.NET Framework 4에서는 *작업*이라고 하는 비동기 프로그래밍 개념을 소개 했습니다. 작업은 *작업* 형식 및 *system.object* 네임 스페이스의 관련 형식으로 표시 됩니다. .NET Framework 4.5은 *작업* 개체 작업을 간단 하 게 하는 컴파일러 향상 기능을 통해이를 기반으로 합니다. .NET Framework 4.5에서 컴파일러는 *wait* 및 *async*라는 두 개의 새로운 키워드를 지원 합니다. *Wait* 키워드는 코드 조각이 다른 코드 부분에서 비동기적으로 대기 해야 함을 나타내는 구문상의 약어입니다. *Async* 키워드는 메서드를 작업 기반 비동기 메서드로 표시 하는 데 사용할 수 있는 힌트를 나타냅니다.

*Wait*, *async*및 *Task* 개체의 조합을 사용 하면 .net 4.5에서 비동기 코드를 훨씬 쉽게 작성할 수 있습니다. ASP.NET 4.5는 새로운 컴파일러의 향상 된 기능을 사용 하 여 비동기 HTTP 모듈과 비동기 HTTP 처리기를 작성할 수 있도록 하는 새로운 Api와 함께 이러한 단순화을 지원 합니다.

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>비동기 HTTP 모듈

*작업* 개체를 반환 하는 메서드 내에서 비동기 작업을 수행 하려는 경우를 가정해 보겠습니다. 다음 코드 예제에서는 Microsoft 홈 페이지를 다운로드 하는 비동기 호출을 수행 하는 비동기 메서드를 정의 합니다. 메서드 시그니처에서 *async* 키워드를 사용 하 고 *Downloadstringtaskasync*에 대 한 *wait* 호출을 확인 합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

이것은 모두 작성 해야 합니다. 다운로드가 완료 될 때까지 대기 하는 동안 자동으로 호출 스택 해제를 처리 하 고 다운로드를 완료 한 후에 호출 스택을 자동으로 복원 하는 .NET Framework.

이제 비동기 ASP.NET HTTP 모듈에서이 비동기 메서드를 사용 하려고 한다고 가정 합니다. ASP.NET 4.5에는 작업 기반 비동기 메서드를 ASP.NET HTTP 파이프라인에서 노출 하는 이전 비동기 프로그래밍 모델과 통합 하는 데 사용할 수 있는 도우미 메서드 (*EventHandlerTaskAsyncHelper*) 및 새로운 대리자 형식 (*TaskEventHandler*)이 포함 되어 있습니다. 이 예제에서는 다음 방법을 보여 줍니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>비동기 HTTP 처리기

ASP.NET에서 비동기 처리기를 작성 하는 일반적인 방법은 *IHttpAsyncHandler* 인터페이스를 구현 하는 것입니다. ASP.NET 4.5는에서 파생 될 수 있는 *HttpTaskAsyncHandler* 비동기 기본 형식을 도입 하 여 비동기 처리기를 훨씬 쉽게 작성할 수 있도록 합니다.

*HttpTaskAsyncHandler* 형식은 Abstract 이며 *processrequestasync* 메서드를 재정의 해야 합니다. 내부적으로 ASP.NET는 *Processrequestasync* 의 반환 서명 ( *작업* 개체)을 ASP.NET 파이프라인에서 사용 하는 이전 비동기 프로그래밍 모델과 통합 하는 작업을 처리 합니다.

다음 예제에서는 *작업* 을 사용 하 고 비동기 HTTP 처리기 구현의 일부로 *대기 하는* 방법을 보여 줍니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>새 ASP.NET Request 유효성 검사 기능

기본적으로 ASP.NET는 요청 유효성 검사를 수행 하며, 필드, 헤더, 쿠키 등에서 태그 또는 스크립트를 찾기 위한 요청을 검사 합니다. 검색 된 내용이 있으면 ASP.NET가 예외를 throw 합니다. 이는 잠재적인 사이트 간 스크립팅 공격에 대 한 첫 번째 방어선의 역할을 합니다.

ASP.NET 4.5를 사용 하면 유효성 검사 요청 데이터를 쉽게 선택적으로 읽을 수 있습니다. ASP.NET 4.5는 이전에는 외부 라이브러리인 널리 사용 되는 방지 Xss 라이브러리도 통합 합니다.

개발자는 응용 프로그램에 대 한 요청 유효성 검사를 선택적으로 해제할 수 있는 기능을 자주 요청 합니다. 예를 들어 응용 프로그램이 포럼 소프트웨어 인 경우 사용자가 HTML 형식의 포럼 게시 및 주석을 제출할 수 있지만 여전히 요청 유효성 검사에서 다른 모든 항목을 확인 하 고 있는지 확인 하는 것이 좋습니다.

ASP.NET 4.5에는 유효성 검사 입력을 쉽게 사용할 수 있도록 하는 두 가지 기능이 도입 되었습니다. 지연 된 ("지연") 요청 유효성 검사 및 유효성 검사 요청 데이터에 대 한 액세스입니다.

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>지연 된 ("지연") 요청 유효성 검사

ASP.NET 4.5에서는 기본적으로 모든 요청 데이터에 요청 유효성 검사가 적용 됩니다. 그러나 요청 데이터에 실제로 액세스할 때까지 요청 유효성 검사를 지연 하도록 응용 프로그램을 구성할 수 있습니다. (특정 데이터 시나리오에 대 한 지연 로드와 같은 용어를 기반으로 하는 지연 요청 유효성 검사 라고도 합니다.) 다음 예제와 같이 *httpRUntime* 요소에서 *requestvalidationmode* 특성을 4.5로 설정 하 여 Web.config 파일에서 지연 된 유효성 검사를 사용 하도록 응용 프로그램을 구성할 수 있습니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

요청 유효성 검사 모드를 4.5로 설정 하면 특정 요청 값에 대해서만 요청 유효성 검사가 트리거되고 코드에서 해당 값에 액세스 하는 경우에만 발생 합니다. 예를 들어 코드에서 Request. Form ["포럼 게시물"]의 값을 가져오는 경우 \_ 양식 컬렉션의 해당 요소에 대해서만 요청 유효성 검사가 호출 됩니다. *폼* 컬렉션의 다른 요소는 모두 유효성이 검사 되지 않습니다. 이전 버전의 ASP.NET에서는 컬렉션의 요소에 액세스할 때 전체 요청 컬렉션에 대해 요청 유효성 검사가 트리거 되었습니다. 새 동작을 사용 하면 다른 응용 프로그램 구성 요소에서 다른 부분에 대 한 요청 유효성 검사를 트리거하지 않고 다른 요청 데이터를 쉽게 볼 수 있습니다.

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>유효성 검사 요청에 대 한 지원

지연 된 요청 유효성 검사 만으로는 요청 유효성 검사를 선택적으로 바이패스 하는 문제를 해결 하지 않습니다. Request ["포럼 \_ 게시물"]에 대 한 호출은 해당 특정 요청 값에 대 한 요청 유효성 검사를 트리거합니다. 그러나 해당 필드에서 태그를 허용 하려고 하기 때문에 유효성 검사를 트리거하지 않고이 필드에 액세스할 수 있습니다.

이를 허용 하기 위해 ASP.NET 4.5는 이제 데이터를 요청 하는 유효성 검사 액세스를 지원 합니다. ASP.NET 4.5에는 *HttpRequest* 클래스에 새 *유효성 검사* collection 속성이 포함 되어 있습니다. 이 컬렉션은 *폼*, *QueryString*, *쿠키*및 *Url*과 같은 요청 데이터의 모든 일반 값에 대 한 액세스를 제공 합니다.

포럼 예제를 사용 하 여 유효성 검사 request 데이터를 읽을 수 있으려면 먼저 새 요청 유효성 검사 모드를 사용 하도록 응용 프로그램을 구성 해야 합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

그런 다음 *HttpRequest 유효성 검사* 속성을 사용 하 여 유효성 검사 form 값을 읽을 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> 보안- *유효성 검사 요청 데이터를 주의 해 서 사용 합니다.* ASP.NET 4.5은 매우 구체적인 유효성 검사 request 데이터에 쉽게 액세스할 수 있도록 유효성 검사 요청 속성 및 컬렉션을 추가 했습니다. 그러나 위험한 텍스트가 사용자에 게 렌더링 되지 않도록 원시 요청 데이터에 대 한 사용자 지정 유효성 검사를 수행 해야 합니다.

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>Xss 라이브러리 방지

Microsoft의 위조 방지 라이브러리의 인기도로 인해 ASP.NET 4.5은 이제 해당 라이브러리의 버전 4.0에서 핵심 인코딩 루틴을 통합 합니다.

인코딩 루틴은 새 *antixssencoder 사용할* 네임 스페이스의 형식으로 구현 됩니다 *.* 형식에서 구현 되는 정적 인코딩 메서드를 호출 하 여 *antixssencoder 사용할* 형식을 직접 사용할 수 있습니다. 그러나 새 XSS 루틴을 사용 하는 가장 쉬운 방법은 기본적으로 *antixssencoder 사용할* 클래스를 사용 하도록 ASP.NET 응용 프로그램을 구성 하는 것입니다. 이렇게 하려면 Web.config 파일에 다음 특성을 추가 합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

*EncoderType* 특성이 *antixssencoder 사용할* 유형을 사용 하도록 설정 된 경우 ASP.NET의 모든 출력 인코딩은 자동으로 새 인코딩 루틴을 사용 합니다.

ASP.NET 4.5에 통합 된 외부 방지 Xss 라이브러리의 일부입니다.

- *HtmlEncode*, *HtmlFormUrlEncode*및 *htmlattributeencode*
- *Xmlattributeencode* 및 *xmlencoding*
- *UrlEncode* 및 *UrlPathEncode* (신규)
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>Websocket 프로토콜에 대 한 지원

Websocket 프로토콜은 HTTP를 통해 클라이언트와 서버 간에 보안 실시간 양방향 통신을 설정 하는 방법을 정의 하는 표준 기반 네트워크 프로토콜입니다. Microsoft는 IETF 및 W3C 표준 본문을 모두 사용 하 여 프로토콜을 정의 하는 데 도움을 받았습니다. Websocket 프로토콜은 브라우저 뿐만 아니라 모든 클라이언트에서 지원 되며, Microsoft는 클라이언트와 모바일 운영 체제에서 Websocket 프로토콜을 지 원하는 상당한 리소스를 투자 합니다.

Websocket 프로토콜을 사용 하면 클라이언트와 서버 간에 장기 실행 데이터 전송을 훨씬 쉽게 만들 수 있습니다. 예를 들어, 클라이언트와 서버 간에 진정한 장기 실행 연결을 설정할 수 있으므로 채팅 응용 프로그램을 작성 하는 것이 훨씬 쉽습니다. 소켓의 동작을 시뮬레이션 하기 위해 주기적인 폴링 또는 HTTP 긴 폴링과 같은 해결 방법을 사용할 필요는 없습니다.

ASP.NET 4.5 및 IIS 8은 낮은 수준의 Websocket 지원을 포함 하 여 ASP.NET 개발자가 Websocket 개체의 문자열과 이진 데이터를 비동기적으로 읽고 쓰는 데 관리 되는 Api를 사용할 수 있도록 합니다. ASP.NET 4.5의 경우 Websocket 프로토콜을 사용 하기 위한 형식을 포함 하는 새 *system.web. websocket* 네임 스페이스가 있습니다.

브라우저 클라이언트는 다음 예제와 같이 ASP.NET 응용 프로그램의 URL을 가리키는 DOM *WebSocket* 개체를 만들어 websocket 연결을 설정 합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

모든 종류의 모듈 또는 처리기를 사용 하 여 ASP.NET에서 Websocket 끝점을 만들 수 있습니다. 이전 예제에서 .ashx 파일이 사용 되었습니다. .ashx 파일은 처리기를 만드는 빠른 방법입니다.

Websocket 프로토콜에 따라 ASP.NET 응용 프로그램은 요청을 HTTP GET 요청에서 Websocket 요청으로 업그레이드 해야 함을 지정 하 여 클라이언트의 Websocket 요청을 허용 합니다. 예는 다음과 같습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest* 메서드는 ASP.NET가 현재 HTTP 요청을 해제 한 다음 컨트롤을 함수 대리자로 전송 하기 때문에 함수 대리자를 허용 합니다. 이 접근 방식은 개념적 작업이 수행 되는 스레드 시작 대리자를 정의 하는 *system.object*를 사용 하는 방법과 비슷합니다.

ASP.NET 후 클라이언트는 Websocket 핸드셰이크를 성공적으로 완료 한 후 대리자를 호출 하 고 Websocket 응용 프로그램이 실행을 시작 합니다. 다음 코드 예제에서는 ASP.NET에서 기본 제공 Websocket 지원을 사용 하는 간단한 echo 응용 프로그램을 보여 줍니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

*Wait* 키워드 및 비동기 작업 기반 작업에 대해 .net 4.5의 지원은 websocket 응용 프로그램을 작성 하는 데 매우 적합 합니다. 코드 예제에서는 Websocket 요청이 ASP.NET 내에서 완전히 비동기적으로 실행 되는 것을 보여 줍니다. 응용 프로그램은 wait socket을 호출 하 여 클라이언트에서 메시지가 전송 될 때까지 비동기적으로 대기 *합니다. ReceiveAsync*. 마찬가지로 wait socket을 호출 하 여 클라이언트에 비동기 메시지를 보낼 수 있습니다 *. SendAsync*.

브라우저에서 응용 프로그램은 *onmessage* 함수를 통해 websocket 메시지를 수신 합니다. 브라우저에서 메시지를 보내려면 다음 예에 표시 된 것 처럼 *WebSocket* DOM 형식의 *send* 메서드를 호출 합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

나중에이 기능에 대 한 업데이트를 출시할 때이 릴리스에서 Websocket 응용 프로그램에 필요한 하위 수준 코딩 중 일부를 추상화할 수 있습니다.

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>묶음 및 축소

번들을 사용 하면 개별 JavaScript 및 CSS 파일을 단일 파일 처럼 처리할 수 있는 번들로 결합할 수 있습니다. 축소는 공백 및 필요 하지 않은 다른 문자를 제거 하 여 JavaScript 및 CSS 파일을 축소 합니다. 이러한 기능은 Web Forms, ASP.NET MVC 및 웹 페이지에서 작동 합니다.

번들은 번들 클래스 또는 해당 자식 클래스 (ScriptBundle 및 StyleBundle) 중 하나를 사용 하 여 만듭니다. 번들의 인스턴스를 구성한 후에는 글로벌 BundleCollection 인스턴스에 추가 하기만 하면 들어오는 요청에 번들을 사용할 수 있습니다. 기본 템플릿에서 번들 구성은 BundleConfig 파일에서 수행 됩니다. 이 기본 구성은 템플릿에서 사용 되는 모든 핵심 스크립트와 css 파일에 대 한 번들을 만듭니다.

번들은 가능한 몇 가지 도우미 메서드 중 하나를 사용 하 여 뷰 내에서 참조 됩니다. 디버그 모드와 릴리스 모드에서 번들에 대 한 다른 태그 렌더링을 지원 하기 위해 ScriptBundle 및 StyleBundle 클래스에는 렌더링의 도우미 메서드를 사용할 수 있습니다. 디버그 모드에서 Render는 번들의 각 리소스에 대 한 태그를 생성 합니다. 릴리스 모드에서 Render는 전체 번들에 대 한 단일 태그 요소를 생성 합니다. 디버그 모드와 릴리스 모드 사이를 전환 하려면 아래와 같이 web.config에서 컴파일 요소의 debug 특성을 수정 하면 됩니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

또한 최적화를 사용 하거나 사용 하지 않도록 설정 하는 것은 Bundletable.enableoptimization 속성을 통해 직접 설정할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

파일이 번들로 묶여 있으면 먼저 사전순으로 정렬 됩니다 ( **솔루션 탐색기**에 표시 되는 방식). 그런 다음 알려진 라이브러리와 해당 사용자 지정 확장 (예: jQuery, MooTools 및 Dojo)이 먼저 로드 되도록 구성 됩니다. 예를 들어 위에 표시 된 것 처럼 스크립트 폴더를 묶는 마지막 순서는 다음과 같습니다.

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

또한 CSS 파일을 사전순으로 정렬 한 다음 다시 구성 하 여 다시 설정 하 고 다른 모든 파일 앞에와 야 합니다. 위에 표시 된 스타일 폴더 묶음의 최종 정렬은 다음과 같습니다.

1. 다시 설정. css
2. 콘텐츠나
3. forms .css
4. globals
5. 메뉴 .css
6. styles. css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>웹 호스팅에 대 한 성능 향상

.NET Framework 4.5 및 Windows 8에는 웹 서버 워크 로드에 대해 상당한 성능 향상을 구현 하는 데 도움이 되는 기능이 소개 되어 있습니다. 여기에는 축소 (최대 35%)가 포함 됩니다. 시작 시간 및 ASP.NET를 사용 하는 웹 호스팅 사이트의 메모리 공간을 모두 사용 합니다.

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>주요 성능 요소

이상적으로 모든 웹 사이트는 다음 요청에 대 한 빠른 응답을 보장 하기 위해 활성 및 메모리에 있어야 합니다. 사이트 응답성에 영향을 줄 수 있는 요인은 다음과 같습니다.

- 응용 프로그램 풀이 재생 된 후 사이트를 다시 시작 하는 데 걸리는 시간입니다. 사이트 어셈블리가 더 이상 메모리에 없는 경우 사이트에 대 한 웹 서버 프로세스를 시작 하는 데 걸리는 시간입니다. 플랫폼 어셈블리는 다른 사이트에서 사용 되므로 아직 메모리에 있습니다. 이러한 상황을 "콜드 사이트, 웜 프레임 워크 시작" 또는 "콜드 사이트 시작" 이라고 합니다.
- 사이트가 차지 하는 메모리의 양입니다. 이에 대 한 용어는 "사이트별 메모리 소비량" 또는 "공유 되지 않은 작업 집합"입니다.

새 성능 향상은 이러한 두 요소에 중점을 둡니다.

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>새 성능 기능에 대 한 요구 사항

새 기능에 대 한 요구 사항은 다음과 같은 범주로 나눌 수 있습니다.

- .NET Framework 4에서 실행 되는 향상 된 기능
- .NET Framework 4.5를 요구 하지만 모든 버전의 Windows에서 실행할 수 있는 향상 된 기능입니다.
- Windows 8에서 실행 되는 .NET Framework 4.5 에서만 사용할 수 있는 향상 된 기능입니다.

사용할 수 있는 각 향상 수준으로 성능이 향상 됩니다.

.NET Framework 4.5 향상 된 기능 중 일부는 다른 시나리오에도 적용 되는 광범위 한 성능 기능을 활용 합니다.

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>공용 어셈블리 공유

**요구 사항**: .NET Framework 4 및 Visual Studio 11 DEVELOPER Preview SDK

서버에 있는 여러 사이트에서 동일한 도우미 어셈블리 (예: 시작 키트 또는 샘플 응용 프로그램의 어셈블리)를 사용 하는 경우가 많습니다. 각 사이트에는 Bin 디렉터리에 이러한 어셈블리의 자체 복사본이 있습니다. 어셈블리에 대 한 개체 코드는 동일 하더라도 물리적으로 별도의 어셈블리 이므로 콜드 사이트를 시작 하는 동안 각 어셈블리를 별도로 읽고 메모리에 별도로 보관 해야 합니다.

새로운 인턴 기능은 이러한 비효율성을 해결 하 고 RAM 요구 사항과 로드 시간을 모두 줄입니다. 인턴을 사용 하면 Windows에서 파일 시스템에 각 어셈블리의 단일 복사본을 유지 하 고 사이트 Bin 폴더의 개별 어셈블리가 단일 복사본에 대 한 바로 가기 링크로 바뀝니다. 개별 사이트에 고유한 버전의 어셈블리가 필요한 경우 기호화 된 링크는 새 버전의 어셈블리로 바뀌고 해당 사이트에만 영향을 줍니다.

기호화 된 링크를 사용 하 여 어셈블리를 공유 하려면 \_ 인턴 지정 된 어셈블리의 저장소를 만들고 관리할 수 있는 aspnetintern.exe 라는 새로운 도구가 필요 합니다. Visual Studio 11 Developer Preview SDK의 일부로 제공 됩니다. 그러나 최신 [업데이트](https://support.microsoft.com/kb/2468871)를 설치한 경우에만 .NET Framework 4만 설치 된 시스템에서 작동 합니다.

적격 한 모든 어셈블리가 인턴 지정 된 상태 인지 확인 하려면 정기적으로 \_ (예: 예약 된 작업으로 매주 한 번) aspnetintern.exe 실행 합니다. 일반적인 용도는 다음과 같습니다.

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

모든 옵션을 보려면 인수 없이 도구를 실행 합니다.

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>더 빠른 시작을 위해 멀티 코어 JIT 컴파일 사용

**요구 사항**: .NET Framework 4.5

콜드 사이트를 시작 하는 경우 디스크에서 어셈블리를 읽을 뿐만 아니라 사이트를 JIT로 컴파일해야 합니다. 복잡 한 사이트의 경우이로 인해 상당한 지연이 발생할 수 있습니다. .NET Framework 4.5의 새로운 범용 기술은 사용 가능한 프로세서 코어 간에 JIT 컴파일을 분산 하 여 이러한 지연을 줄입니다. 이전에 사이트를 시작 하는 동안 수집 된 정보를 사용 하 여이 작업을 최대한 빨리 수행 합니다. 이 기능은 System.object를 구현 하는 [startprofile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) 메서드에 의해 구현 됩니다.

ASP.NET에서는 여러 코어를 사용 하는 JIT 컴파일을 기본적으로 사용 하도록 설정 되어 있으므로이 기능을 활용 하기 위해 아무것도 수행할 필요가 없습니다. 이 기능을 사용 하지 않도록 설정 하려면 Web.config 파일에서 다음 설정을 지정 합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>메모리 최적화를 위한 가비지 수집 튜닝

**요구 사항**: .NET Framework 4.5

사이트를 실행 하 고 나면 GC (가비지 수집기) 힙을 사용 하는 것이 메모리 사용에 중요 한 요인이 될 수 있습니다. 모든 가비지 수집기와 마찬가지로 .NET Framework GC는 CPU 시간 (컬렉션의 빈도 및 중요도)과 메모리 사용 (새로운, 해제 또는 사용 가능한 개체에 사용 되는 추가 공간) 간의 균형을 만듭니다. 이전 릴리스의 경우 적절 한 균형을 이루기 위해 GC를 구성 하는 방법에 대 한 지침을 제공 합니다 (예: [ASP.NET 2.0/3.5 공유 호스팅 구성](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)참조).

.NET Framework 4.5의 경우 여러 독립 실행형 설정 대신 이전에 권장 되는 모든 GC 설정 및 사이트별 작업 집합에 대 한 추가 성능을 제공 하는 새로운 튜닝을 사용 하는 워크 로드 정의 구성 설정을 사용할 수 있습니다.

GC 메모리 튜닝을 사용 하도록 설정 하려면 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 파일에 다음 설정을 추가 합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

aspnet.config 변경에 대 한 이전 지침을 잘 알고 있는 경우에는이 설정이 이전 설정을 대체 합니다. 예를 들어 gcServer, gcConcurrent 등을 설정할 필요가 없습니다. 이전 설정은 제거할 필요가 없습니다.

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>웹 응용 프로그램 프리페치

**요구 사항**: Windows 8에서 실행 되는 .NET Framework 4.5

여러 릴리스의 경우 Windows에는 응용 프로그램 시작의 디스크 읽기 비용을 줄이는 [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) 이라는 기술이 포함 되어 있습니다. 콜드 시작은 클라이언트 응용 프로그램에서 주로 문제가 되기 때문에이 기술은 서버에 필수적인 구성 요소만 포함 하는 Windows Server에 포함 되어 있지 않습니다. 이제 최신 버전의 Windows Server에서 프리페치를 사용할 수 있으며,이 경우 개별 웹 사이트의 시작을 최적화할 수 있습니다.

Windows Server의 경우 prefetcher는 기본적으로 사용 하도록 설정 되어 있지 않습니다. 고밀도 웹 호스팅을 위한 prefetcher를 사용 하도록 설정 하 고 구성 하려면 명령줄에서 다음 명령 집합을 실행 합니다.

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

그런 다음 prefetcher을 ASP.NET 응용 프로그램과 통합 하려면 Web.config 파일에 다음을 추가 합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET 웹 양식

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>강력한 형식의 데이터 컨트롤

ASP.NET 4.5의 Web Forms에는 데이터 작업을 위한 몇 가지 향상 된 기능이 포함 되어 있습니다. 첫 번째 향상 된 기능은 강력한 형식의 데이터 컨트롤입니다. 이전 버전의 ASP.NET에서 Web Forms 컨트롤의 경우 *Eval* 및 데이터 바인딩 식을 사용 하 여 데이터 바인딩된 값을 표시 합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

양방향 데이터 바인딩의 경우 *Bind*를 사용 합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

런타임에는 이러한 호출에서 리플렉션을 사용 하 여 지정 된 멤버의 값을 읽은 다음 결과를 태그에 표시 합니다. 이 접근 방식을 사용 하면 데이터를 사용 하지 않는 임의의 데이터에 쉽게 바인딩할 수 있습니다.

그러나 이와 같은 데이터 바인딩 식은 멤버 이름, 탐색 (예: 정의로 이동) 또는 이러한 이름에 대 한 컴파일 타임 검사와 같은 기능을 지원 하지 않습니다.

이 문제를 해결 하기 위해 ASP.NET 4.5는 컨트롤이 바인딩된 데이터의 데이터 형식을 선언 하는 기능을 추가 합니다. 새 *ItemType* 속성을 사용 하 여이 작업을 수행 합니다. 이 속성을 설정 하면 데이터 바인딩 식의 범위에서 *item* 및 *binditem*이라는 두 가지 형식화 된 새 변수를 사용할 수 있습니다. 변수가 강력 하 게 형식화 되어 있기 때문에 Visual Studio 개발 환경을 최대한 활용할 수 있습니다.

양방향 데이터 바인딩 식의 경우 *Binditem* 변수를 사용 합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

ASP.NET Web Forms 프레임 워크에서 데이터 바인딩을 지 원하는 대부분의 컨트롤은 *ItemType* 속성을 지원 하도록 업데이트 되었습니다.

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>모델 바인딩

모델 바인딩은 코드 중심 데이터 액세스를 사용 하도록 ASP.NET Web Forms 컨트롤의 데이터 바인딩을 확장 합니다. ASP.NET MVC의 모델 바인딩과 *ObjectDataSource* 컨트롤의 개념을 통합 합니다.

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>데이터 선택

모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 컨트롤의 *SelectMethod* 속성을 페이지 코드의 메서드 이름으로 설정 합니다. 데이터 컨트롤은 페이지 수명 주기에서 적절 한 시간에 메서드를 호출 하 고 반환 된 데이터를 자동으로 바인딩합니다. *DataBind* 메서드를 명시적으로 호출할 필요가 없습니다.

다음 예제에서는 *GridView* 컨트롤이 *getcategories*라는 메서드를 사용 하도록 구성 되어 있습니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

페이지의 코드에서 *Getcategories* 메서드를 만듭니다. 간단한 select 작업의 경우에는 메서드에 매개 변수가 필요 하지 않으며 *IEnumerable* 또는 *IQueryable* 개체를 반환 해야 합니다. 이전에 [강력한 형식의 데이터 컨트롤](#_Toc318097386) 에 설명 된 것 처럼 강력한 형식의 데이터 바인딩 식을 사용할 수 있도록 하는 새 *ItemType* 속성이 설정 된 경우 이러한 인터페이스의 제네릭 버전을 반환 해야 합니다. * &lt; &gt; 즉* * &lt; &gt; *, *T* 매개 변수는 *ItemType* 속성의 형식과 일치 합니다 (예: *iqueryable &lt; 범주 &gt; *).

다음 예제에서는 *Getcategories* 메서드에 대 한 코드를 보여 줍니다. 이 예에서는 Northwind 샘플 데이터베이스와 Entity Framework Code First 모델을 사용 합니다. 이 코드는 쿼리가 *Include* 메서드를 사용 하 여 각 범주에 대 한 관련 제품의 세부 정보를 반환 하는지 확인 합니다. 이렇게 하면 태그의 *templatefield로 변환* 요소가 [n + 1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)를 요구 하지 않고 각 범주의 제품 수를 표시 합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

페이지가 실행 되 면 *GridView* 컨트롤이 *getcategories* 메서드를 자동으로 호출 하 고 구성 된 필드를 사용 하 여 반환 된 데이터를 렌더링 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

Select 메서드는 *IQueryable* 개체를 반환 하므로 *GridView* 컨트롤은 쿼리를 실행 하기 전에 쿼리를 추가로 조작할 수 있습니다. 예를 들어, *GridView* 컨트롤이 실행 되기 전에 반환 된 *IQueryable* 개체를 정렬 하 고 페이징 하기 위해 쿼리 식을 추가 하 여 해당 작업이 기본 LINQ 공급자에 의해 수행 되도록 할 수 있습니다. 이 경우 Entity Framework는 데이터베이스에서 해당 작업이 수행 되도록 합니다.

다음 예제에서는 정렬 및 페이징을 허용 하도록 수정 된 *GridView* 컨트롤을 보여 줍니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

이제 페이지가 실행 될 때 컨트롤은 데이터의 현재 페이지만 표시 되 고 선택한 열을 기준으로 정렬 되도록 할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

반환 된 데이터를 필터링 하려면 매개 변수를 select 메서드에 추가 해야 합니다. 이러한 매개 변수는 런타임에 모델 바인딩으로 채워지고, 데이터를 반환 하기 전에 쿼리를 변경 하는 데 사용할 수 있습니다.

예를 들어 사용자가 쿼리 문자열에 키워드를 입력 하 여 제품을 필터링 하려는 경우를 가정해 보겠습니다. 매개 변수를 메서드에 추가 하 고 매개 변수 값을 사용 하도록 코드를 업데이트할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

이 코드에는 *키워드* 에 대 한 값을 제공 하 고 쿼리 결과를 반환 하는 경우 *Where* 식이 포함 됩니다.

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>값 공급자

위의 예는 *키워드* 매개 변수의 값이 제공 된 위치에 대 한 구체적인 정보가 아닙니다. 이 정보를 나타내려면 매개 변수 특성을 사용할 수 있습니다. 이 예제에서는 *system.web. ModelBinding* 네임 스페이스에 있는 *querystringattribute* 클래스를 사용할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

이렇게 하면 런타임에 쿼리 문자열의 값을 *키워드* 매개 변수에 바인딩하기 위해 모델 바인딩이 수행 됩니다. (이 경우에는 형식 변환을 수행 하는 경우가 포함 될 수 있습니다.) 값을 제공할 수 없고 형식이 null을 허용 하지 않는 경우 예외가 throw 됩니다.

이러한 메서드에 대 한 값의 소스를 값 공급자 라고 하며 사용할 값 공급자를 나타내는 매개 변수 특성을 값 공급자 특성 이라고 합니다. Web Forms에는 쿼리 문자열, 쿠키, 폼 값, 컨트롤, 뷰 상태, 세션 상태 및 프로필 속성과 같이 Web Forms 응용 프로그램에서 사용자 입력의 일반적인 모든 원본에 대 한 값 공급자 및 해당 특성이 포함 됩니다. 사용자 지정 값 공급자를 작성할 수도 있습니다.

기본적으로 매개 변수 이름은 값 공급자 컬렉션에서 값을 찾기 위한 키로 사용 됩니다. 이 예제에서 코드는 키워드 (예: ~/default.aspx? keyword = chef) 라는 쿼리 문자열 값을 검색 합니다. 매개 변수 특성에 인수로 전달 하 여 사용자 지정 키를 지정할 수 있습니다. 예를 들어 q 라는 쿼리 문자열 변수 값을 사용 하려면 다음을 수행 합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

이 메서드가 페이지의 코드에 있는 경우 사용자는 쿼리 문자열을 사용 하 여 키워드를 전달 하 여 결과를 필터링 할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

모델 바인딩은 값을 읽고, null 값을 확인 하 고, 적절 한 형식으로 변환 하 고, 변환에 성공 했는지 여부를 확인 하 고, 마지막으로 쿼리의 값을 사용 하 여 코딩 해야 하는 많은 작업을 수행 합니다. 모델 바인딩은 응용 프로그램 전체에서 기능을 다시 사용 하는 기능과 훨씬 작은 코드를 생성 합니다.

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>컨트롤에서 값으로 필터링

예를 확장 하 여 사용자가 드롭다운 목록에서 필터 값을 선택할 수 있도록 하려는 경우를 가정해 보겠습니다. 다음 드롭다운 목록을 태그에 추가 하 고 *SelectMethod* 속성을 사용 하 여 다른 메서드에서 데이터를 가져오도록 구성 합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

일반적으로 일치 하는 제품이 없는 경우 컨트롤이 메시지를 표시 하도록 *GridView* 컨트롤에 *emptydatatemplate이* 요소를 추가 합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

페이지 코드에서 드롭다운 목록에 대 한 새 select 메서드를 추가 합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

마지막으로 *Getproducts* select 메서드를 업데이트 하 여 드롭다운 목록에서 선택한 범주의 ID를 포함 하는 새 매개 변수를 가져옵니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

이제 페이지가 실행 될 때 사용자는 드롭다운 목록에서 범주를 선택할 수 있으며, *GridView* 컨트롤이 자동으로 바인딩되어 필터링 된 데이터를 표시 합니다. 이는 모델 바인딩이 select 메서드의 매개 변수 값을 추적 하 고 다시 게시 후 매개 변수 값이 변경 되었는지 여부를 검색 하기 때문에 가능 합니다. 그렇다면 모델 바인딩에서는 연결 된 데이터 컨트롤이 데이터에 강제로 다시 바인딩됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML로 인코딩된 Data-Binding 식

이제 데이터 바인딩 식의 결과를 HTML로 인코딩할 수 있습니다. 콜론 추가 (:) &lt;데이터 바인딩 식을 표시 하 는% # 접두사의 끝에 다음을 수행 합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>조심 스럽게 유효성 검사

이제 클라이언트 쪽 유효성 검사 논리에 대해 적합 하지 않은 JavaScript를 사용 하도록 기본 제공 유효성 검사기 컨트롤을 구성할 수 있습니다. 이렇게 하면 페이지 태그에서 인라인으로 렌더링 된 JavaScript의 양이 크게 줄어들고 전체 페이지 크기가 줄어듭니다. 다음과 같은 방법으로 유효성 검사기 컨트롤에 대해 방해가 되지 않는 JavaScript를 구성할 수 있습니다.

- 전역적으로 Web.config 파일의 * &lt; appSettings &gt; * 요소에 다음 설정을 추가 합니다. 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- 전역적으로 *UnobtrusiveValidationMode* 속성을 *UnobtrusiveValidationMode* (일반적으로 Global.asax 파일의 *응용 프로그램 \_ 시작* 메서드)로 설정 하 여 전역적으로 설정 합니다.
- *페이지 클래스의* 새 *UnobtrusiveValidationMode* 속성을 *UnobtrusiveValidationMode*로 설정 하 여 페이지에 대해 개별적으로 설정 합니다.

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 업데이트

HTML5의 새 기능을 활용 하기 위해 Web Forms 서버 컨트롤에 대 한 몇 가지 기능이 향상 되었습니다.

- *TextBox* 컨트롤의 *TextMode* 속성은 *email*, *datetime*등의 새 HTML5 입력 형식을 지원 하도록 업데이트 되었습니다.
- 이제 *FileUpload* 컨트롤은이 HTML5 기능을 지 원하는 브라우저에서 여러 파일 업로드를 지원 합니다.
- 유효성 검사기 컨트롤은 이제 HTML5 입력 요소의 유효성 검사를 지원 합니다.
- URL을 나타내는 특성이 있는 새 HTML5 요소는 이제 runat = "server"를 지원 합니다. 그 결과, ~ 연산자와 같이 URL 경로에 ASP.NET 규칙을 사용 하 여 응용 프로그램 루트를 나타낼 수 있습니다 (예: &lt; video runat = "server" src = "~/Myvideo.rerereers"/ &gt; ).
- HTML5 입력 필드 게시를 지원 하도록 *UpdatePanel* 컨트롤이 수정 되었습니다.

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 Beta는 이제 Visual Studio 11 Beta에 포함 되어 있습니다. ASP.NET MVC는 MVC (모델-뷰-컨트롤러) 패턴을 활용 하 여 매우 테스트 가능 하 고 유지 가능한 웹 응용 프로그램을 개발 하기 위한 프레임 워크입니다. ASP.NET MVC 4를 사용 하면 모바일 웹 응용 프로그램을 쉽게 빌드할 수 있으며, 모든 장치에 연결할 수 있는 HTTP 서비스를 빌드하는 데 도움이 되는 ASP.NET Web API 포함 됩니다. 자세한 내용은 [ASP.NET MVC 4 릴리스 정보](mvc4-release-notes.md)를 참조 하세요.

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET 웹 페이지 2

새로운 기능은 다음과 같습니다.

- 새 사이트 템플릿 및 업데이트 된 사이트 템플릿.
- *유효성 검사* 도우미를 사용 하 여 서버 쪽 및 클라이언트 쪽 유효성 검사를 추가 합니다.
- 자산 관리자를 사용 하 여 스크립트를 등록할 수 있습니다.
- OAuth 및 Openid connect를 사용 하 여 Facebook 및 기타 사이트에서 로그인을 사용 하도록 설정 합니다.
- *맵* 도우미를 사용 하 여 맵 추가
- 웹 페이지 응용 프로그램을 나란히 실행 합니다.
- 모바일 장치에 대 한 렌더링 페이지

이러한 기능 및 전체 페이지 코드 예제에 대 한 자세한 내용은 [웹 페이지 2 Beta의 주요 기능](https://go.microsoft.com/fwlink/?LinkID=227824)을 참조 하세요.

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 베타

이 섹션에서는 Visual Web Developer 11 Beta 및 Visual Studio 2012 릴리스 후보의 웹 개발 개선 사항에 대 한 정보를 제공 합니다.

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010와 Visual Studio 2012 릴리스 후보 간의 프로젝트 공유 (프로젝트 호환성)

Visual Studio 2012 릴리스 후보가 될 때까지 최신 버전의 Visual Studio에서 기존 프로젝트를 열면 변환 마법사가 시작 됩니다. 이렇게 하면 이전 버전과 호환 되지 않는 새 형식으로 프로젝트 및 솔루션의 콘텐츠 (자산)를 강제로 업그레이드 했습니다. 따라서 변환 후 이전 버전의 Visual Studio에서 프로젝트를 열 수 없습니다.

많은 고객이 올바른 방법이 아니라는 것을 알게 되었습니다. Visual Studio 11 Beta에서는 이제 Visual Studio 2010 s p 1과의 프로젝트 및 솔루션 공유를 지원 합니다. 즉, Visual Studio 2012 릴리스 후보에서 2010 프로젝트를 열 경우 Visual Studio 2010 s p 1에서 프로젝트를 열 수 있습니다.

> [!NOTE]
> Visual Studio 2010 SP1 및 Visual Studio 2012 릴리스 후보 간에는 몇 가지 형식의 프로젝트를 공유할 수 없습니다. 여기에는 몇 가지 이전 프로젝트 (예: ASP.NET MVC 2 프로젝트) 또는 특별 한 용도로 사용 되는 프로젝트 (예: 설치 프로젝트)가 포함 됩니다.

Visual studio 11 Beta에서 처음으로 Visual Studio 2010 SP1 웹 프로젝트를 열면 다음 속성이 프로젝트 파일에 추가 됩니다.

- FileUpgradeFlags
- UpgradeBackupLocation
- OldToolsVersion
- VisualStudioVersion
- VSToolsPath

FileUpgradeFlags, UpgradeBackupLocation 및 OldToolsVersion은 프로젝트 파일을 업그레이드 하는 프로세스에서 사용 됩니다. Visual Studio 2010에서 프로젝트 작업에는 영향을 주지 않습니다.

VisualStudioVersion는 현재 프로젝트에 대 한 Visual Studio 버전을 나타내는 MSBuild 4.5에 사용 되는 새 속성입니다. 이 속성은 MSBuild 4.0 (Visual Studio 2010 s p 1에서 사용 하는 MSBuild 버전)에 존재 하지 않기 때문에 프로젝트 파일에 기본값을 삽입 합니다.

VSToolsPath 속성은 MSBuildExtensionsPath32 설정으로 표시 된 경로에서 가져올 올바른 .targets 파일을 결정 하는 데 사용 됩니다.

Import 요소와 관련 된 몇 가지 변경 내용도 있습니다. 이러한 변경 내용은 두 버전의 Visual Studio 간 호환성을 지원 하기 위해 필요 합니다.

> [!NOTE]
> 프로젝트를 서로 다른 두 컴퓨터의 Visual Studio 2010 s p 1과 Visual Studio 11 Beta 간에 공유 하는 경우, 프로젝트의 응용 프로그램 데이터 폴더에 로컬 데이터베이스가 포함 되어 있으면 \_ 데이터베이스에 사용 되는 SQL Server 버전이 두 컴퓨터에 모두 설치 되어 있는지 확인 해야 합니다.

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 웹 사이트 템플릿의 구성 변경 내용

Visual Studio 2012 릴리스 후보에서 웹 사이트 템플릿을 사용 하 여 만든 사이트의 기본 *Web.config* 파일이 다음과 같이 변경 되었습니다.

- `<httpRuntime>`이제 요소에서 특성은 `encoderType` ASP.NET에 추가 된 방지 xss 유형을 사용 하도록 기본적으로 설정 됩니다. 자세한 내용은 [Xss 라이브러리 방지](#_Toc318097382)를 참조 하세요.
- 또한 요소에서 `<httpRuntime>` `requestValidationMode` 특성은 "4.5"로 설정 됩니다. 즉, 기본적으로 요청 유효성 검사는 지연 된 ("지연") 유효성 검사를 사용 하도록 구성 됩니다. 자세한 내용은 [New ASP.NET Request Validation Features](#_Toc318097379)을 참조 하세요.
- `<modules>`섹션의 요소에 `<system.webServer>` 특성이 포함 되어 있지 않습니다 `runAllManagedModulesForAllRequests` . 기본값은 false입니다. 즉, s p 1로 업데이트 되지 않은 IIS 7의 버전을 사용 하는 경우 새 사이트에서 라우팅하는 데 문제가 있을 수 있습니다. 자세한 내용은 [ASP.NET 라우팅에 대 한 IIS 7의 기본 지원](#Native_Support_In_IIS7_For_ASPNET_Routine)을 참조 하세요.

이러한 변경 내용은 기존 응용 프로그램에 영향을 주지 않습니다. 그러나 새 템플릿을 사용 하 여 ASP.NET 4.5에 대해 만드는 새 웹 사이트와 기존 웹 사이트 간의 동작 차이를 나타낼 수 있습니다.

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>IIS 7 for ASP.NET 라우팅의 기본 지원

이는 ASP.NET 변경 되지 않지만 SP1 업데이트를 적용 하지 않은 IIS 7 버전을 작업 하는 경우 영향을 줄 수 있는 새 웹 사이트 프로젝트에 대 한 템플릿의 변경 내용입니다.

ASP.NET에서는 라우팅을 지원 하기 위해 응용 프로그램에 다음 구성 설정을 추가할 수 있습니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

**RunAllManagedModulesForAllRequests** 가 true 인 경우와 같은 URL은 `http://mysite/myapp/home` url에 *.aspx*, *mvc*또는 유사한 확장이 없더라도 ASP.NET로 이동 합니다.

IIS 7에 대 한 업데이트를 수행 하면 **runAllManagedModulesForAllRequests** 설정이 불필요 하 게 되며 ASP.NET 라우팅이 기본적으로 지원 됩니다. 업데이트에 대 한 자세한 내용은 [특정 iis 7.0 또는 iis 7.5 처리기에서 url이 마침표로 끝나지 않는 요청을 처리할 수 있도록 업데이트를 사용할 수 있는](https://support.microsoft.com/kb/980368)Microsoft 지원 문서를 참조 하세요.

웹 사이트가 IIS 7에서 실행 중이 고 IIS가 업데이트 된 경우 **runAllManagedModulesForAllRequests** 를 true로 설정할 필요가 없습니다. 실제로이를 true로 설정 하는 것은 요청에 불필요 한 처리 오버 헤드를 추가 하기 때문에 권장 되지 않습니다. 이 설정이 true 이면 *.htm*, *.jpg*및 기타 정적 파일에 대 한 요청을 비롯 한 모든 요청은 ASP.NET request 파이프라인을 거칩니다.

Visual Studio 2012 RC에 제공 된 템플릿을 사용 하 여 새 ASP.NET 4.5 웹 사이트를 만드는 경우 웹 사이트의 구성에는 **runAllManagedModulesForAllRequests** 설정이 포함 되지 않습니다. 즉, 기본적으로이 설정은 false입니다.

S p 1이 설치 되지 않은 Windows 7에서 웹 사이트를 실행 하는 경우에는 IIS 7에 필요한 업데이트가 포함 되지 않습니다. 결과적으로 라우팅이 작동 하지 않으며 오류가 표시 됩니다. 라우팅이 작동 하지 않는 문제가 발생 하는 경우 다음 중 하나를 수행할 수 있습니다.

- IIS 7에 업데이트를 추가 하는 Windows 7을 s p 1로 업데이트 합니다.
- 이전에 나열 된 Microsoft 지원 문서에 설명 된 업데이트를 설치 합니다.
- 해당 웹 사이트의 Web.config 파일에서 **runAllManagedModulesForAllRequests** 를 true로 설정 합니다. 이렇게 하면 요청에 약간의 오버 헤드가 추가 됩니다.

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML 편집기

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>스마트 작업

디자인 뷰 서버 컨트롤의 복잡 한 속성에는 일반적으로 대화 상자와 마법사를 연결 하 여 쉽게 설정할 수 있습니다. 예를 들어 특수 대화 상자를 사용 하 여 데이터 소스를 *Repeater* 컨트롤에 추가 하거나 *GridView* 컨트롤에 열을 추가할 수 있습니다.

그러나 복잡 한 속성에 대 한이 형식의 UI 도움말은 소스 뷰에서 사용할 수 없습니다. 따라서 Visual Studio 11에서는 소스 뷰에 대 한 스마트 작업을 소개 합니다. 스마트 작업은 c # 및 Visual Basic 편집기에서 일반적으로 사용 되는 기능에 대 한 상황에 맞는 바로 가기입니다.

ASP.NET Web Forms 컨트롤의 경우 삽입 지점이 요소 내부에 있을 때 스마트 작업이 서버 태그에 작은 문자 모양으로 나타납니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

문자 모양을 클릭 하거나 CTRL + .를 누르면 스마트 작업 확장 됩니다. (점), 코드 편집기에서와 동일 합니다. 그런 다음 디자인 뷰의 스마트 작업과 유사한 바로 가기를 표시 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

예를 들어 위의 그림에서 스마트 작업는 GridView 작업 옵션을 보여 줍니다. 열 편집을 선택 하면 다음 대화 상자가 표시 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

대화 상자를 채우면 디자인 뷰에서 설정할 수 있는 속성과 동일 하 게 설정 됩니다. 확인을 클릭 하면 컨트롤의 태그가 새 설정으로 업데이트 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAI-ARIA 지원

액세스 가능한 웹 사이트를 작성 하는 것은 점점 더 중요 해지고 있습니다. [Wai-ARIA 접근성 표준은](http://www.w3.org/WAI/intro/aria) 개발자가 액세스할 수 있는 웹 사이트를 작성 하는 방법을 정의 합니다. 이 표준은 이제 Visual Studio에서 완벽 하 게 지원 됩니다.

예를 들어 *role* 특성에는 이제 전체 IntelliSense가 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

WAI-ARIA 표준에는 HTML5 문서에 의미 체계를 추가할 수 있도록 하는 *aria* 접두사가 포함 된 특성도 도입 되었습니다. 또한 Visual Studio는 이러한 *aria 특성을* 완벽 하 게 지원 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>새 HTML5 코드 조각

일반적으로 사용 되는 HTML5 태그를 더 쉽고 빠르게 작성할 수 있도록 Visual Studio에는 여러 개의 코드 조각이 포함 되어 있습니다. 비디오 조각은 다음과 같습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

코드 조각을 호출 하려면 IntelliSense에서 요소를 선택할 때 Tab 키를 두 번 누릅니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

그러면 사용자 지정할 수 있는 코드 조각이 생성 됩니다.

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>사용자 정의 컨트롤로 추출

대형 웹 페이지에서는 개별 요소를 사용자 컨트롤로 이동 하는 것이 좋을 수 있습니다. 이러한 형태의 리팩터링을 통해 페이지의 가독성을 높이고 페이지 구조를 단순화할 수 있습니다.

이렇게 하려면 소스 뷰에서 Web Forms 페이지를 편집할 때 페이지에서 텍스트를 선택 하 고 마우스 오른쪽 단추로 클릭 한 다음 사용자 정의 컨트롤로 추출을 선택 하면 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>특성의 코드 너 깃 IntelliSense

Visual Studio는 항상 모든 페이지나 컨트롤에서 서버 쪽 코드 너 깃 IntelliSense를 제공 합니다. 이제 Visual Studio는 HTML 특성의 코드 너 깃 IntelliSense를 포함 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

이렇게 하면 데이터 바인딩 식을 보다 쉽게 만들 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>여는 태그 또는 닫는 태그의 이름을 바꿀 때 일치 하는 태그의 자동 이름 바꾸기

HTML 요소의 이름을 바꾸는 경우 (예: *div* 태그를 *헤더* 태그로 변경 하는 경우) 해당 하는 여는 태그와 닫는 태그는 실시간으로 변경 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

이렇게 하면 닫는 태그를 변경 하거나 잘못 된 태그를 변경 하는 것을 잊은 오류를 방지할 수 있습니다.

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>이벤트 처리기 생성

이제 Visual Studio에는 이벤트 처리기를 작성 하 고 수동으로 바인딩할 수 있도록 소스 뷰의 기능이 포함 되어 있습니다. 소스 뷰에서 이벤트 이름을 편집 하는 경우 IntelliSense는 &lt; 새 이벤트 만들기를 표시 하며 &gt; ,이 이벤트 처리기는 페이지의 코드에서 올바른 서명이 있는 이벤트 처리기를 만듭니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

기본적으로 이벤트 처리기는 이벤트 처리 메서드의 이름에 대해 컨트롤의 ID를 사용 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

결과 이벤트 처리기는 다음과 같습니다 (이 경우 c #의 경우).

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>스마트 들여쓰기

빈 HTML 요소 내에서 Enter 키를 누르면 편집기에서 적절 한 위치에 삽입 지점을 삽입 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

이 위치에서 Enter 키를 누르면 닫는 태그가 아래로 이동 하 여 여는 태그와 일치 하 게 들여씁니다. 또한 삽입 지점은 다음과 같이 들여쓰기 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>문 완성 자동 줄이기

이제 Visual Studio의 IntelliSense 목록에는 관련 옵션만 표시 되도록 입력 하는 내용에 따라 필터링 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

Intellisense는 IntelliSense 목록에 있는 개별 단어의 제목 대/소문자를 기준으로 필터링 됩니다. 예를 들어 "dl"을 입력 하면 dl과 asp: DataList가 모두 표시 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

이 기능을 사용 하면 알려진 요소에 대해 문 완성을 더 빠르게 수행할 수 있습니다.

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript 편집기

Visual Studio 2012 릴리스 후보의 JavaScript 편집기는 완전히 새로운 기능으로, Visual Studio에서 JavaScript 작업 환경을 크게 향상 시킵니다.

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>코드 개요

이제 모든 함수에 대해 개요 영역이 자동으로 만들어지므로 현재 포커스와 관련이 없는 파일의 일부를 축소할 수 있습니다.

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>중괄호 일치

여는 중괄호 또는 닫는 중괄호에 삽입 지점을 삽입 하면 편집기에서 일치 항목을 강조 표시 합니다.

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>정의로 이동

정의로 이동 명령을 사용 하면 함수 또는 변수의 원본으로 이동할 수 있습니다.

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 지원

편집기는 JavaScript 언어를 설명 하는 표준의 최신 버전인 ECMAScript5에서 새로운 구문과 Api를 지원 합니다.

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

IntelliSense 용 IntelliSense Api는 *Queryselector*, dom 저장소, 크로스 문서 메시징 및 *캔버스*를 비롯 한 다양 한 새 HTML5 api에 대 한 지원으로 향상 되었습니다. DOM IntelliSense는 이제 네이티브 형식 라이브러리 정의가 아니라 간단한 단일 JavaScript 파일에 의해 구동 됩니다. 이렇게 하면 쉽게 확장 하거나 바꿀 수 있습니다.

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC 서명 오버 로드

이제 다음 예제와 같이 새 * &lt; signature &gt; * 요소를 사용 하 여 JavaScript 함수의 개별 오버 로드에 대 한 자세한 IntelliSense 주석을 선언할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>암시적 참조

이제 지정 된 JavaScript 파일이 나 블록에서 참조 하는 파일 목록에 암시적으로 포함 될 JavaScript 파일을 중앙 목록에 추가할 수 있습니다. 즉, 해당 내용에 대 한 IntelliSense를 가져옵니다. 예를 들어 파일의 중앙 목록에 jQuery 파일을 추가할 수 있으며,이 파일을 명시적으로 참조 (///참조/사용) 할 수 있는지 여부에 관계 없이 파일의 JavaScript 블록에서 jQuery 함수에 대해 IntelliSense를 가져옵니다 &lt; &gt; .

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS 편집기

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>문 완성 자동 줄이기

이제 CSS에 대 한 IntelliSense 목록이 선택한 스키마에서 지 원하는 CSS 속성 및 값을 기준으로 필터링 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense는 제목 사례 검색도 지원 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>계층적 들여쓰기

CSS 편집기는 들여쓰기를 사용 하 여 계층 규칙을 표시 합니다 .이 규칙은 연계 규칙의 논리적 구성 방법에 대 한 개요를 제공 합니다. 다음 예제에서 선택기 #list는 목록의 계단식 자식인 것 이므로 들여씁니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

다음 예제에서는 좀 더 복잡 한 상속을 보여 줍니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

규칙의 들여쓰기는 부모 규칙에 따라 결정 됩니다. 계층적 들여쓰기는 기본적으로 사용 하도록 설정 되어 있지만 옵션 대화 상자 (도구, 메뉴 모음에서 옵션)를 사용 하지 않도록 설정할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS 해킹 지원

수백 개의 실제 CSS 파일을 분석 하면 CSS 해킹 매우 일반적으로 표시 되 고 Visual Studio에서는 가장 널리 사용 되는 항목을 지원 합니다. 이 지원에는 별표 ( \* ) 및 밑줄 ( \_ ) 속성 해킹에 대 한 IntelliSense 및 유효성 검사가 포함 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

표준 선택기 해킹도 지원 되므로 계층적 들여쓰기가 적용 되는 경우에도 유지 됩니다. Internet Explorer 7을 대상으로 하는 데 사용 되는 일반적인 선택기는 * \* 첫 번째-자식 + html*과 함께 선택기 앞에 추가 하는 것입니다. 해당 규칙을 사용 하 여 계층적 들여쓰기를 유지 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>공급 업체별 스키마 (-moz-,-webkit)

CSS3에는 다양 한 브라우저에서 다양 한 시간에 구현 된 많은 속성이 도입 되었습니다. 이전에는 개발자가 공급 업체별 구문을 사용 하 여 특정 브라우저에 대해 코딩 했습니다. 이러한 브라우저 관련 속성은 이제 IntelliSense에 포함 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>주석 달기 및 주석 처리 지원

이제 코드 편집기에서 사용 하는 것과 같은 바로 가기 키를 사용 하 여 CSS 규칙을 주석 처리 하 고 주석 처리를 제거할 수 있습니다 (Ctrl + K, C to comment 및 Ctrl + K, 주석 처리를 해제).

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>색 선택기

이전 버전의 Visual Studio에서 색 관련 특성의 IntelliSense는 명명 된 색 값의 드롭다운 목록으로 이루어져 있습니다. 이 목록은 전체 기능을 갖춘 색 선택으로 대체 되었습니다.

색 값을 입력 하면 색 선택이 자동으로 표시 되 고 이전에 사용 된 색의 목록과 기본 색상표가 표시 됩니다. 마우스나 키보드를 사용 하 여 색을 선택할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

목록을 전체 색 선택으로 확장할 수 있습니다. 선택 하면 불투명도 슬라이더를 이동할 때 모든 색을 자동으로 RGBA로 변환 하 여 알파 채널을 제어할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>코드 조각

CSS 편집기의 코드 조각을 사용 하면 브라우저 간 스타일을 쉽고 빠르게 만들 수 있습니다. 브라우저 관련 설정이 필요한 많은 CSS3 속성은 이제 조각으로 롤오버 되었습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS 코드 조각은 IntelliSense 목록을 표시 하는 기호 (@)를 입력 하 여 고급 시나리오 (예: CSS3 media queries)를 지원 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

값을 선택 하 @media 고 tab 키를 누르면 CSS 편집기는 다음 코드 조각을 삽입 합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

코드 조각과 마찬가지로 고유한 CSS 코드 조각을 만들 수 있습니다.

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>사용자 지정 지역

이제 코드 편집기에서 이미 사용할 수 있는 명명 된 코드 영역을 CSS 편집용으로 사용할 수 있습니다. 이렇게 하면 관련 스타일 블록을 쉽게 그룹화 할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

영역을 축소 하면 지역 이름이 표시 됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>페이지 검사기

페이지 검사기는 Visual Studio IDE에서 웹 페이지 (HTML, Web Forms, ASP.NET MVC 또는 웹 페이지)를 렌더링 하 고 소스 코드와 결과 출력을 모두 검사할 수 있도록 하는 도구입니다. ASP.NET 페이지의 경우 페이지 검사기를 통해 브라우저에 렌더링 되는 HTML 태그를 생성 한 서버측 코드를 확인할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

페이지 검사기에 대 한 자세한 내용은 다음 자습서를 참조 하세요.

- [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md) 에서 페이지 검사기 사용
- [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md) 에서 페이지 검사기 사용

<a id="_Toc318097425"></a>
### <a name="publishing"></a>게시

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>게시 프로필

Visual Studio 2010에서 웹 응용 프로그램 프로젝트에 대 한 게시 정보는 버전 제어에 저장 되지 않으며 다른 사용자와 공유 하도록 디자인 되지 않았습니다. Visual Studio 2012 릴리스 후보에서는 게시 프로필의 형식이 변경 되었습니다. 팀 아티팩트가 생성 되었으므로 이제 MSBuild를 기반으로 하는 빌드에서 쉽게 활용할 수 있습니다. 빌드 구성 정보는 게시 하기 전에 빌드 구성을 쉽게 전환할 수 있도록 게시 대화 상자에 있습니다.

게시 프로필은 게시 프로필 폴더에 저장 됩니다. 폴더의 위치는 사용 하는 프로그래밍 언어에 따라 달라 집니다.

- C #: Properties\PublishProfiles
- Visual Basic: 내 프로필 프로필

각 프로필은 MSBuild 파일입니다. 게시 하는 동안이 파일을 프로젝트의 MSBuild 파일로 가져옵니다. Visual Studio 2010에서 게시 또는 패키지 프로세스를 변경 하려는 경우에는 **ProjectName**이라는 파일에 사용자 지정을 저장 해야 합니다. 이는 계속 지원 되지만 이제는 사용자 지정을 게시 프로필 자체에 추가할 수 있습니다. 이렇게 하면 사용자 지정이 해당 프로필에만 사용 됩니다.

이제 MSBuild에서 게시 프로필을 활용할 수도 있습니다. 이렇게 하려면 프로젝트를 빌드할 때 다음 명령을 사용 합니다.

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

.Csproj 값은 프로젝트의 경로이 고 ProfileName는 게시할 프로필의 이름입니다. 또는 *PublishProfile* 속성에 대 한 프로필 이름을 전달 하는 대신 게시 프로필에 대 한 전체 경로를 전달할 수 있습니다.

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET 미리 컴파일 및 병합

웹 응용 프로그램 프로젝트의 경우 Visual Studio 2012 릴리스 후보는 프로젝트를 게시 하거나 패키지할 때 사이트의 콘텐츠를 미리 컴파일하고 병합할 수 있는 웹 속성 패키지/게시 페이지에 옵션을 추가 합니다. 이러한 옵션을 보려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택한 다음 패키지 및 웹 게시 속성 페이지를 선택 합니다. 다음 그림에서는 게시 하기 전에이 응용 프로그램 미리 컴파일 옵션을 보여 줍니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

이 옵션을 선택 하면 웹 응용 프로그램을 게시 하거나 패키지할 때마다 Visual Studio에서 응용 프로그램을 미리 컴파일합니다. 사이트를 미리 컴파일하는 방법 또는 어셈블리를 병합 하는 방법을 제어 하려는 경우 고급 단추를 클릭 하 여 해당 옵션을 구성 합니다.

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

이제 Visual Studio에서 웹 프로젝트를 테스트 하는 데 사용할 기본 웹 서버가 IIS Express. Visual Studio 개발 서버는 개발 중에도 로컬 웹 서버에 대 한 옵션 이지만 IIS Express 이제 권장 되는 서버입니다. Visual Studio 11 Beta에서 IIS Express를 사용 하는 환경은 Visual Studio 2010 s p 1에서 사용 하는 것과 매우 비슷합니다.

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>고지 사항

본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.

이 문서에 포함된 정보는 게시 날짜 당시 논의된 문제에 대한 Microsoft Corporation의 현재 관점을 나타냅니다. Microsoft는 변화하는 시장 상황에 대응해야 하므로 Microsoft의 약속으로 해석되지 않아야 하며, Microsoft는 게시 날짜 이후 제시된 정보의 정확성을 보증하지 않습니다.

이 백서는 정보 제공만을 목적으로 합니다. Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.

해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나 검색 시스템에 저장 또는 도입되거나 전송될 수 없습니다.

Microsoft는 이 설명서 본안에 관련된 특허권, 상표권, 저작권, 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 설명서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권 또는 기타 지적 재산권 등에 대한 어떠한 사용권도 허용하지 않습니다.

별도로 언급 하지 않는 한, 용례에 사용 된 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트는 실제 데이터가 아닙니다. 어떠한 실제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 또는 이벤트와도 연관 시킬 의도가 없으며 그렇게 유추 해서도 안 됩니다.

© 2012 Microsoft Corporation. All rights reserved.

Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.

여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.
