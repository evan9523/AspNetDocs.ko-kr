---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 와 비주얼 스튜디오 2012의 새로운 내용 | 마이크로 소프트 문서
author: rick-anderson
description: 이 문서에서는 ASP.NET 4.5에 도입되는 새로운 기능과 향상된 기능에 대해 설명합니다. 또한 웹 개발을 위해 개선된 사항에 대해서도 설명합니다...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675888"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 및 Visual Studio 2012의 새로운 기능

> 이 문서에서는 ASP.NET 4.5에 도입되는 새로운 기능과 향상된 기능에 대해 설명합니다. 또한 Visual Studio 2012의 웹 개발을 위해 개선된 사항에 대해서도 설명합니다. 이 문서는 원래 2012년 2월 29일에 게시되었습니다.

- [ASP.NET 코어 런타임 및 프레임워크](#_Toc318097372)

    - [비동기적으로 HTTP 요청 및 응답 읽기 및 쓰기](#_Toc318097373)
    - [HttpRequest 처리 개선 사항](#_Toc318097374)
    - [비동기적으로 응답 플러시](#_Toc318097375)
    - [*대기* 및 *작업*기반 비동기 모듈 및 처리기 지원](#_Toc318097376)
    - [비동기 HTTP 모듈](#_Toc318097377)
    - [비동기 HTTP 처리기](#_Toc318097378)
    - [새로운 ASP.NET 요청 유효성 검사 기능](#_Toc318097379)
    - [지연된("지연") 요청 유효성 검사](#_Toc318097380)
    - [검증되지 않은 요청에 대한 지원](#_Toc318097381)
    - [안티XSS 라이브러리](#_Toc318097382)
    - [웹 소켓 프로토콜 지원](#_Toc318097383)
    - [번들 및 미니화](#_Toc318097384)
    - [웹 호스팅을 위한 성능 향상](#_Toc_perf)

        - [주요 성능 요소](#_Toc_perf_1)
        - [새로운 성능 기능에 대한 요구 사항](#_Toc_perf_2)
        - [공통 어셈블리 공유](#_Toc_perf_3)
        - [더 빠른 시작을 위해 멀티 코어 JIT 컴파일 사용](#_Toc_perf_4)
        - [메모리에 최적화하기 위한 가비지 콜렉션 튜닝](#_Toc_perf_5)
        - [웹 응용 프로그램에 대한 프리페칭](#_Toc_perf_6)
- [ASP.NET 웹 양식](#_Toc318097385)

    - [강력한 형식의 데이터 컨트롤](#_Toc318097386)
    - [모델 바인딩](#_Toc318097387)

        - [데이터 선택](#_Toc318097388)
        - [가치 공급자](#_Toc318097389)
        - [컨트롤의 값으로 필터링](#_Toc318097390)
    - [HTML 인코딩된 데이터 바인딩 식](#_Toc318097391)
    - [눈에 거슬리지 않는 유효성 검사](#_Toc318097392)
    - [HTML5 업데이트](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET 웹 페이지 2](#_Toc318097395)
- [비주얼 스튜디오 2012 릴리스 후보](#_Toc318097396)

    - [비주얼 스튜디오 2010과 비주얼 스튜디오 2012 릴리스 후보 간의 프로젝트 공유(프로젝트 호환성)](#project-compatibility)
    - [ASP.NET 4.5 웹 사이트 템플릿의 구성 변경 사항](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [ASP.NET 라우팅을 위한 IIS 7의 기본 지원](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML 편집기](#_Toc318097397)

        - [스마트 작업](#_Toc318097398)
        - [와이 아리아 지원](#_Toc318097399)
        - [새로운 HTML5 스니펫](#_Toc318097400)
        - [사용자 제어로 추출](#_Toc318097401)
        - [속성의 코드 너겟에 대한 IntelliSense](#_Toc318097402)
        - [개폐 태그의 이름을 바꿀 때 일치하는 태그의 자동 이름 바꾸기](#_Toc318097403)
        - [이벤트 처리기 생성](#_Toc318097404)
        - [스마트 들여쓰기](#_Toc318097405)
        - [명령문 자동 축소 완료](#_Toc318097406)
    - [자바 스크립트 편집기](#_Toc318097407)

        - [코드 개요](#_Toc318097408)
        - [중괄호 일치](#_Toc318097409)
        - [정의로 이동](#_Toc318097410)
        - [ECMAScript5 지원](#_Toc318097411)
        - [돔 인텔리센스](#_Toc318097412)
        - [VSDOC 서명 오버로드](#_Toc318097413)
        - [암시적 참조](#_Toc318097414)
    - [CSS 편집기](#_Toc318097415)

        - [명령문 자동 축소 완료](#_Toc318097416)
        - [계층적 들여쓰기.](#_Toc318097417)
        - [CSS 해킹 지원](#_Toc318097418)
        - [공급업체 별 스키마(-moz-,-web킷)](#_Toc318097419)
        - [댓글 달기 및 댓글 달기 지원](#_Toc318097420)
        - [색 선택](#_Toc318097421)
        - [조각](#_Toc318097422)
        - [사용자 지정 지역](#_Toc318097423)
    - [페이지 검사기](#_Toc318097424)
    - [게시](#_Toc318097425)

        - [게시 프로필](#_Toc318097426)
        - [사전 컴파일 및 병합ASP.NET](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [고지 사항](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET 코어 런타임 및 프레임워크

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>비동기적으로 HTTP 요청 및 응답 읽기 및 쓰기

ASP.NET 4는 *HttpRequest.GetBufferlessInputStream* 메서드를 사용하여 HTTP 요청 엔터티를 스트림으로 읽는 기능을 도입했습니다. 이 메서드는 요청 엔터티에 대한 스트리밍 액세스를 제공했습니다. 그러나 요청 기간 동안 스레드를 묶는 동기적으로 실행되었습니다.

ASP.NET 4.5는 HTTP 요청 엔터티에서 비동기적으로 스트림을 읽는 기능과 비동기적으로 플러시하는 기능을 지원합니다. ASP.NET 4.5는 또한 .aspx 페이지 처리기 및 ASP.NET MVC 컨트롤러와 같은 다운스트림 HTTP 처리기와의 보다 쉽게 통합할 수 있는 HTTP 요청 엔터티를 두 번 버퍼링할 수 있는 기능을 제공합니다.

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HttpRequest 처리 개선 사항

*httpRequest.GetBufferlessInputStream에서* ASP.NET 4.5에 의해 반환 된 스트림 참조는 동기 및 비동기 읽기 메서드를 모두 지원합니다. *GetBufferlessInputStream에서* 반환된 *스트림* 개체는 이제 BeginRead 및 EndRead 메서드를 모두 구현합니다. 비동기 *Stream* 메서드를 사용하면 요청 엔터티를 청크로 비동기적으로 읽을 수 있으며 ASP.NET 비동기 읽기 루프의 각 반복 간에 현재 스레드를 해제합니다.

ASP.NET 4.5 또한 버퍼링 된 방법으로 요청 엔터티를 읽기 위한 컴패니언 *메서드를*추가 했습니다. 이 새 오버로드는 *GetBufferlessInputStream처럼*작동하여 동기 및 비동기 읽기를 모두 지원합니다. 그러나 *GetBufferedInputStream은* 엔터티 바이트를 ASP.NET 내부 버퍼로 복사하여 다운스트림 모듈과 처리기가 요청 엔터티에 계속 액세스할 수 있도록 합니다. 예를 들어 파이프라인의 일부 업스트림 코드가 *GetBufferedInputStream을*사용하여 요청 엔터티를 이미 읽은 경우에도 *HttpRequest.Form* 또는 *HttpRequest.Files*를 사용할 수 있습니다. 이렇게 하면 요청(예: 대용량 파일 업로드를 데이터베이스에 스트리밍)에서 비동기 처리를 수행할 수 있지만 나중에 .aspx 페이지 및 MVC ASP.NET 컨트롤러를 계속 실행할 수 있습니다.

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>비동기적으로 응답 플러시

클라이언트가 멀리 떨어져 있거나 대역폭이 낮은 연결이 있는 경우 HTTP 클라이언트에 응답을 보내는 데 상당한 시간이 걸릴 수 있습니다. 일반적으로 ASP.NET 응용 프로그램에서 만들 때 응답 바이트를 버퍼링합니다. 그런 다음 ASP.NET 요청 처리의 맨 끝에서 누적된 버퍼의 단일 송신 작업을 수행합니다.

버퍼링된 응답이 큰 경우(예: 대용량 파일을 클라이언트로 스트리밍) *주기적으로 HttpResponse.Flush를* 호출하여 버퍼링된 출력을 클라이언트에 보내고 메모리 사용량을 제어해야 합니다. 그러나 *Flush는* 동기 호출이므로 반복적으로 *플러시를* 호출하면 잠재적으로 장기 실행되는 요청 동안 스레드가 계속 사용됩니다.

ASP.NET 4.5는 HttpResponse 클래스의 *BeginFlush* 및 *EndFlush* 메서드를 사용하여 비동기적으로 플러시 수행에 대한 지원을 *추가합니다.* 이러한 메서드를 사용하면 운영 체제 스레드를 연결하지 않고 클라이언트에 데이터를 점진적으로 보내는 비동기 모듈 및 비동기 처리기를 만들 수 있습니다. *BeginFlush* 호출과 *EndFlush* 호출 사이에 ASP.NET 현재 스레드를 해제합니다. 이렇게 하면 장기 실행 HTTP 다운로드를 지원하기 위해 필요한 총 활성 스레드 수가 크게 줄어듭니다.

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>*대기* 및 *작업* 지원 - 기반 비동기 모듈 및 처리기

.NET Framework 4는 *작업이라고*하는 비동기 프로그래밍 개념을 도입했습니다. 작업은 *System.Threading.Task* 네임스페이스의 *작업* 유형 및 관련 유형으로 표시됩니다. .NET Framework 4.5는 *작업* 개체 작업을 간단하게 만드는 컴파일러 향상 기능을 통해 이를 기반으로 합니다. .NET Framework 4.5에서 컴파일러는 *await* 및 *async라는*두 가지 새 키워드를 지원합니다. *await* 키워드는 코드 조각이 다른 코드 에서 비동기적으로 기다려야 한다는 것을 나타내는 구문적 약어입니다. *비동기* 키워드는 메서드를 작업 기반 비동기 메서드로 표시하는 데 사용할 수 있는 힌트를 나타냅니다.

*await*, *비동기*및 *작업* 개체의 조합을 사용하면 .NET 4.5에서 비동기 코드를 훨씬 쉽게 작성할 수 있습니다. ASP.NET 4.5는 새로운 컴파일러 향상 을 사용하여 비동기 HTTP 모듈 및 비동기 HTTP 처리기를 작성할 수 있는 새 API를 사용하여 이러한 단순화를 지원합니다.

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>비동기 HTTP 모듈

*Task* 개체를 반환하는 메서드 내에서 비동기 작업을 수행한다고 가정합니다. 다음 코드 예제는 Microsoft 홈 페이지를 다운로드하기 위해 비동기 호출을 하는 비동기 메서드를 정의합니다. 메서드 시그니처에서 *비동기* 키워드를 사용하고 *다운로드StringTaskAsync에*대한 *대기* 호출을 확인합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

.NET Framework는 다운로드가 완료될 때까지 기다리는 동안 호출 스택 해제를 자동으로 처리하고 다운로드가 완료된 후 호출 스택을 자동으로 복원합니다.

이제 비동기 ASP.NET HTTP 모듈에서 이 비동기 메서드를 사용한다고 가정합니다. ASP.NET 4.5에는 ASP.NET HTTP 파이프라인에서 노출된 이전 비동기 프로그래밍 모델과 작업 기반 비동기 메서드를 통합하는 데 사용할 수 있는 도우미*메서드(EventHandlerTaskAsyncHelper)와*새 대리자*유형(TaskEventHandler)이*포함되어 있습니다. 이 예제에서는 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 이 예제

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>비동기 HTTP 처리기

ASP.NET 비동기 처리기를 작성하는 기존의 방법은 *IHttpAsyncHandler* 인터페이스를 구현하는 것입니다. ASP.NET 4.5에서 파생할 수 있는 *HttpTaskAsyncHandler* 비동기 기본 형식을 도입하므로 비동기 처리기를 훨씬 쉽게 작성할 수 있습니다.

*HttpTaskAsyncHandler* 형식은 추상적이며 *ProcessRequestAsync* 메서드를 재정의해야 합니다. 내부적으로 ASP.NET *ProcessRequestAsync의* 반환 *서명(작업* 개체)을 ASP.NET 파이프라인에서 사용하는 이전 비동기 프로그래밍 모델과 통합하는 작업을 처리합니다.

다음 예제에서는 비동기 HTTP 처리기 구현의 일부로 Task 및 *await를* 사용하는 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주시면 *됩니다.*

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>새로운 ASP.NET 요청 유효성 검사 기능

기본적으로 ASP.NET 요청 유효성 검사를 수행하며 필드, 헤더, 쿠키 등에서 태그 또는 스크립트를 찾는 요청을 검사합니다. 검색된 경우 ASP.NET 예외를 throw합니다. 이는 잠재적인 교차 사이트 스크립팅 공격에 대한 첫 번째 방어선 역할을 합니다.

ASP.NET 4.5를 사용하면 유효성이 검사되지 않은 요청 데이터를 쉽게 쉽게 읽을 수 있습니다. ASP.NET 4.5는 또한 이전에 외부 라이브러리였던 인기있는 AntiXSS 라이브러리를 통합합니다.

개발자는 응용 프로그램에 대한 요청 유효성 검사를 선택적으로 해제할 수 있는 기능을 자주 요청했습니다. 예를 들어 응용 프로그램이 포럼 소프트웨어인 경우 사용자가 HTML 형식의 포럼 게시물및 주석을 제출하도록 허용하지만 요청 유효성 검사가 다른 모든 것을 검사하고 있는지 확인할 수 있습니다.

ASP.NET 4.5에서는 지연된("지연") 요청 유효성 검사 및 유효성이 검사되지 않은 요청 데이터에 대한 액세스등 유효성이 검사되지 않은 입력으로 선택적으로 작업할 수 있는 두 가지 기능이 도입되었습니다.

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>지연된("지연") 요청 유효성 검사

ASP.NET 4.5에서는 기본적으로 모든 요청 데이터가 요청 유효성 검사의 대상이 됩니다. 그러나 실제로 요청 데이터에 액세스할 때까지 요청 유효성 검사를 연기하도록 응용 프로그램을 구성할 수 있습니다. (특정 데이터 시나리오에 대한 지연 로드와 같은 용어를 기반으로 지연 요청 유효성 검사라고도 합니다.) 다음 예제와 같이 *httpRUntime* 요소에서 *requestValidationMode* 특성을 4.5로 설정하여 Web.config 파일에서 지연된 유효성 검사를 사용하도록 응용 프로그램을 구성할 수 있습니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

요청 유효성 검사 모드가 4.5로 설정된 경우 요청 유효성 검사는 특정 요청 값에 대해서만 트리거되며 코드가 해당 값에 액세스하는 경우에만 트리거됩니다. 예를 들어 코드가 Request.Form["포럼\_게시물"]의 값을 얻는 경우 요청 유효성 검사는 양식 컬렉션의 해당 요소에 대해서만 호출됩니다. *양식* 컬렉션의 다른 요소는 유효성이 검사되지 않습니다. 이전 버전의 ASP.NET 컬렉션의 모든 요소에 액세스할 때 전체 요청 컬렉션에 대 한 요청 유효성 검사가 트리거 되었습니다. 새 동작을 사용하면 다른 응용 프로그램 구성 요소가 다른 부분에 대한 요청 유효성 검사를 트리거하지 않고도 다양한 요청 데이터를 쉽게 볼 수 있습니다.

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>검증되지 않은 요청에 대한 지원

지연된 요청 유효성 검사만으로는 요청 유효성 검사를 선택적으로 우회하는 문제를 해결할 수 없습니다. Request.Form["포럼\_게시물"]에 대한 호출은 여전히 특정 요청 값에 대한 요청 유효성 검사를 트리거합니다. 그러나 해당 필드에서 태그를 허용하려는 경우 유효성 검사를 트리거하지 않고 이 필드에 액세스할 수 있습니다.

이를 위해 ASP.NET 4.5는 이제 요청 데이터에 대한 유효성이 검사되지 않은 액세스를 지원합니다. ASP.NET 4.5는 *HttpRequest* 클래스에 새 *유효성이 검사되지 않은* 컬렉션 속성을 포함합니다. 이 컬렉션은 *양식,* *쿼리 문자열,* *쿠키*및 *URL*과 같은 요청 데이터의 모든 공통 값에 대한 액세스를 제공합니다.

유효성이 검사되지 않은 요청 데이터를 읽을 수 있도록 포럼 예제를 사용하면 먼저 새 요청 유효성 검사 모드를 사용하도록 응용 프로그램을 구성해야 합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

그런 다음 *HttpRequest.Unvalidated* 속성을 사용하여 유효성이 검사되지 않은 양식 값을 읽을 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> 보안 - *유효성이 검사되지 않은 요청 데이터를 주의하여 사용하십시오!* ASP.NET 4.5는 유효성이 검사되지 않은 요청 속성 및 컬렉션을 추가하여 매우 구체적인 유효성이 검사되지 않은 요청 데이터에 쉽게 액세스할 수 있도록 했습니다. 그러나 위험한 텍스트가 사용자에게 렌더링되지 않도록 원시 요청 데이터에 대한 사용자 지정 유효성 검사를 수행해야 합니다.

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>안티XSS 라이브러리

Microsoft AntiXSS 라이브러리의 인기로 인해 ASP.NET 4.5는 이제 해당 라이브러리의 버전 4.0의 핵심 인코딩 루틴을 통합합니다.

인코딩 루틴은 새로운 *System.Web.Security.AntiXss* 네임스페이스의 *AntiXssEncoder* 형식에 의해 구현됩니다. *AntiXssEncoder* 형식을 사용 하 여 형식에 구현 되는 정적 인코딩 메서드를 호출 하 여 직접 사용할 수 있습니다. 그러나 새 안티 XSS 루틴을 사용하는 가장 쉬운 방법은 기본적으로 *AntiXssEncoder* 클래스를 사용하도록 ASP.NET 응용 프로그램을 구성하는 것입니다. 이렇게 하려면 Web.config 파일에 다음 특성을 추가합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

*인코더Type* 특성이 *AntiXssEncoder* 형식을 사용하도록 설정되면 ASP.NET 모든 출력 인코딩이 새 인코딩 루틴을 자동으로 사용합니다.

다음은 ASP.NET 4.5에 통합 된 외부 AntiXSS 라이브러리의 일부입니다.

- *HtmlEncode,* *HtmlFormUrlEncode*및 *Html속성 Encode*
- *Xml속성 엔코드* 및 *XmlEncode*
- *UrlEncode* 및 *UrlPathEncode* (새)
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>웹 소켓 프로토콜 지원

WebSockets 프로토콜은 HTTP를 통해 클라이언트와 서버 간에 안전한 실시간 양방향 통신을 설정하는 방법을 정의하는 표준 기반 네트워크 프로토콜입니다. Microsoft는 프로토콜을 정의하는 데 도움을 주기 위해 IETF 및 W3C 표준 기관과 협력해 왔습니다. WebSockets 프로토콜은 브라우저뿐만 아니라 모든 클라이언트에서 지원되며 Microsoft는 클라이언트 및 모바일 운영 체제모두에 WebSockets 프로토콜을 지원하는 상당한 리소스를 투자합니다.

WebSockets 프로토콜을 사용하면 클라이언트와 서버 간에 장기 실행 데이터 전송을 훨씬 쉽게 만들 수 있습니다. 예를 들어 클라이언트와 서버 간에 진정한 장기 실행 연결을 설정할 수 있으므로 채팅 응용 프로그램을 작성하는 것이 훨씬 쉽습니다. 소켓의 동작을 시뮬레이션하기 위해 정기적인 폴링 또는 HTTP 긴 폴링과 같은 해결 방법을 사용할 필요가 없습니다.

ASP.NET 4.5 및 IIS 8에는 하위 수준의 WebSockets 지원이 포함되어 있으므로 ASP.NET 개발자가 WebSockets 개체에서 문자열 및 이진 데이터를 비동기적으로 읽고 쓰는 데 관리되는 API를 사용할 수 있습니다. ASP.NET 4.5의 경우 WebSockets 프로토콜작업에 대한 형식을 포함하는 새로운 *System.Web.WebSockets* 네임스페이스가 있습니다.

브라우저 클라이언트는 다음 예제와 같이 ASP.NET 응용 프로그램의 URL을 가리키는 DOM *WebSocket* 개체를 만들어 WebSockets 연결을 설정합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

모든 종류의 모듈 또는 처리기를 사용하여 ASP.NET WebSockets 끝점을 만들 수 있습니다. 이전 예제에서는 .ashx 파일이 처리기를 만드는 빠른 방법이기 때문에 .ashx 파일이 사용되었습니다.

WebSockets 프로토콜에 따라 ASP.NET 응용 프로그램은 HTTP GET 요청에서 WebSockets 요청으로 요청을 업그레이드해야 한다는 표시로 클라이언트의 WebSockets 요청을 수락합니다. 예를 들면 다음과 같습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest* 메서드는 ASP.NET 현재 HTTP 요청을 해제 한 다음 컨트롤을 함수 대리자로 전송하기 때문에 함수 대리자를 수락합니다. 개념적으로 이 방법은 백그라운드 작업이 수행되는 스레드 시작 대리자를 정의하는 *System.Threading.Thread를*사용하는 방법과 유사합니다.

ASP.NET 클라이언트가 WebSockets 핸드셰이크를 성공적으로 완료한 후 ASP.NET 대리인을 호출하고 WebSockets 응용 프로그램이 실행시작됩니다. 다음 코드 예제에서는 ASP.NET 기본 제공 WebSockets 지원을 사용하는 간단한 에코 응용 프로그램을 보여 주었습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

*await* 키워드 및 비동기 작업 기반 작업에 대한 .NET 4.5의 지원은 WebSockets 응용 프로그램을 작성하는 데 적합합니다. 코드 예제에서는 WebSockets 요청이 ASP.NET 내에서 완전히 비동기적으로 실행되는 것을 보여 주어집니다. 응용 프로그램은 await 소켓을 호출하여 클라이언트에서 메시지가 전송될 때까지 비동기적으로 *대기합니다. 수신Async*. 마찬가지로 await 소켓을 호출하여 클라이언트에 비동기 메시지를 보낼 수 *있습니다. 센드애싱크*.

브라우저에서 응용 프로그램은 *메시지 온 메시지* 기능을 통해 WebSockets 메시지를 수신합니다. 브라우저에서 메시지를 보내려면 이 예제와 같이 *WebSocket* DOM 형식의 *send* 메서드를 호출합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

나중에 WebSockets 응용 프로그램에 대해 이 릴리스에 필요한 하위 수준 코딩 중 일부를 추상화하는 이 기능에 대한 업데이트를 릴리스할 수 있습니다.

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>묶음 및 축소

번들을 사용하면 개별 JavaScript 및 CSS 파일을 단일 파일처럼 취급할 수 있는 번들로 결합할 수 있습니다. 축소는 필요하지 않은 공백 및 기타 문자를 제거하여 JavaScript 및 CSS 파일을 압축합니다. 이러한 기능은 웹 양식, ASP.NET MVC 및 웹 페이지에서 작동합니다.

번들은 번들 클래스 또는 자식 클래스 중 하나인 스크립트번들 및 스타일번들을 사용하여 생성됩니다. 번들의 인스턴스를 구성한 후, 번들은 단순히 전역 번들컬렉션 인스턴스에 추가하기만 하면 들어오는 요청에 사용할 수 있게 됩니다. 기본 템플릿에서 번들 구성은 번들구성 파일에서 수행됩니다. 이 기본 구성은 템플릿에서 사용하는 모든 핵심 스크립트 및 css 파일에 대한 번들을 만듭니다.

번들은 몇 가지 가능한 도우미 방법 중 하나를 사용하여 뷰 내에서 참조됩니다. 디버그 대 릴리스 모드에서 번들에 대해 다른 태그 렌더링을 지원하기 위해 ScriptBundle 및 StyleBundle 클래스에는 도우미 메서드인 Render가 있습니다. 디버그 모드에서 렌더는 번들의 각 리소스에 대한 태그를 생성합니다. 릴리스 모드에서 Render는 전체 번들에 대해 단일 태그 요소를 생성합니다. 아래와 같이 web.config에서 컴파일 요소의 디버그 특성을 수정하여 디버그 모드와 릴리스 모드 간의 전환작업을 수행할 수 있습니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

또한 번들Table.Enable최적화 속성을 통해 최적화를 활성화하거나 사용하지 않도록 설정할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

파일이 번들로 묶이면 먼저 사전순으로 정렬됩니다(솔루션 **탐색기에서**표시되는 방식). 그런 다음 알려진 라이브러리와 사용자 지정 확장(예: jQuery, MooTools 및 Dojo)이 먼저 로드되도록 구성됩니다. 예를 들어, 위에 표시된 스크립트 폴더의 번들의 최종 순서는 다음과 같습니다.

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

CSS 파일은 또한 사전순으로 정렬된 다음 reset.css 및 normalize.css가 다른 파일보다 앞서 오게 되도록 재구성됩니다. 위에 표시된 스타일 폴더의 번들의 최종 정렬은 다음과 같습니다.

1. 리셋.css
2. 콘텐츠.css
3. forms.css
4. 글로벌.css
5. 메뉴.css
6. 스타일.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>웹 호스팅을 위한 성능 향상

.NET Framework 4.5 및 Windows 8에는 웹 서버 워크로드에 대한 성능이 크게 향상되는 데 도움이 되는 기능이 소개되어 있습니다. 여기에는 감소(최대 35%) 시작 시간 및 ASP.NET 사용하는 웹 호스팅 사이트의 메모리 공간 모두에서

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>주요 성능 요소

이상적으로는 모든 웹 사이트가 언제든지 다음 요청에 대한 빠른 응답을 보장하기 위해 활성화되고 메모리에 있어야 합니다. 사이트 응답성에 영향을 줄 수 있는 요소는 다음과 같습니다.

- 앱 풀이 재활용된 후 사이트를 다시 시작하는 데 걸리는 시간입니다. 사이트 어셈블리가 더 이상 메모리에 없을 때 사이트에 대한 웹 서버 프로세스를 시작하는 데 걸리는 시간입니다. 플랫폼 어셈블리는 다른 사이트에서 사용되므로 여전히 메모리에 있습니다. 이러한 상황을 "콜드 사이트, 웜 프레임워크 시작" 또는 "콜드 사이트 시작"이라고 합니다.
- 사이트가 차지하는 메모리 양입니다. 이에 대한 용어는 "사이트당 메모리 사용량" 또는 "공유되지 않은 작업 집합"입니다.

새로운 성능 향상은 이 두 가지 요인모두에 중점을 둡니다.

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>새로운 성능 기능에 대한 요구 사항

새 기능에 대한 요구 사항은 다음 범주로 나눌 수 있습니다.

- .NET 프레임워크 4에서 실행되는 개선 사항입니다.
- .NET Framework 4.5가 필요하지만 모든 버전의 Windows에서 실행할 수 있는 개선 사항입니다.
- Windows 8에서 실행되는 .NET Framework 4.5에서만 사용할 수 있는 향상된 사항입니다.

활성화할 수 있는 각 개선 수준에 따라 성능이 향상됩니다.

.NET Framework 4.5 개선 사항 중 일부는 다른 시나리오에도 적용되는 광범위한 성능 기능을 활용합니다.

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>공통 어셈블리 공유

**요구 사항**: .NET 프레임 워크 4 및 비주얼 스튜디오 11 개발자 미리보기 SDK

서버의 다른 사이트는 종종 동일한 도우미 어셈블리(예: 시작 키트 또는 샘플 응용 프로그램의 어셈블리)를 사용합니다. 각 사이트에는 Bin 디렉터리에서 이러한 어셈블리의 고유한 복사본이 있습니다. 어셈블리의 개체 코드는 동일하지만 물리적으로 분리된 어셈블리이므로 콜드 사이트 시작 중에 각 어셈블리를 별도로 읽고 메모리에 별도로 보관해야 합니다.

새로운 인턴닝 기능은 이러한 비효율성을 해결하고 RAM 요구 사항과 로드 시간을 모두 줄입니다. 인턴링을 사용하면 Windows에서 파일 시스템에 각 어셈블리의 단일 복사본을 유지할 수 있으며 사이트 Bin 폴더의 개별 어셈블리는 단일 복사본에 대한 기호 링크로 대체됩니다. 개별 사이트에 고유한 버전의 어셈블리가 필요한 경우 기호 링크는 새 버전의 어셈블리로 대체되고 해당 사이트만 영향을 받습니다.

기호 링크를 사용하여 어셈블리를 공유하려면\_aspnet intern.exe라는 새 도구가 필요하므로 인턴어 의 저장소를 만들고 관리할 수 있습니다. 그것은 비주얼 스튜디오의 일부로 제공됩니다 11 개발자 미리보기 SDK. 그러나 최신 [업데이트를](https://support.microsoft.com/kb/2468871)설치했다고 가정할 때 .NET Framework 4만 설치된 시스템에서 작동합니다.

자격을 갖춘 모든 어셈블리가 인턴으로 등록되었는지\_확인하려면 aspnet intern.exe를 주기적으로 실행합니다(예: 예약된 작업으로 일주일에 한 번). 일반적인 용도는 다음과 같습니다.

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

모든 옵션을 보려면 인수 없이 도구를 실행합니다.

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>더 빠른 시작을 위해 멀티 코어 JIT 컴파일 사용

**요구 사항**: .NET 프레임 워크 4.5

콜드 사이트 시작의 경우 어셈블리를 디스크에서 읽어야 할 뿐만 아니라 사이트를 JIT 컴파일해야 합니다. 복잡한 사이트의 경우 이로 인해 상당한 지연이 추가될 수 있습니다. .NET Framework 4.5의 새로운 범용 기술은 사용 가능한 프로세서 코어 에 JIT 컴파일을 분산하여 이러한 지연을 줄입니다. 그것은 사이트의 이전 출시 중에 수집 된 정보를 사용하여 가능한 한 빨리이 작업을 수행합니다. [System.Runtime.Profile 최적화.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) 메서드에 의해 구현 된이 기능.

여러 코어를 사용하는 JIT 컴파일은 ASP.NET 기본적으로 활성화되므로 이 기능을 활용하기 위해 아무 작업도 수행할 필요가 없습니다. 이 기능을 사용하지 않도록 설정하려면 Web.config 파일에서 다음 설정을 수행합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>메모리에 최적화하기 위한 가비지 콜렉션 튜닝

**요구 사항**: .NET 프레임 워크 4.5

사이트가 실행되면 GC(가비지 수집기) 힙을 사용하는 것이 메모리 소비에 중요한 요소가 될 수 있습니다. 모든 가비지 수집기와 마찬가지로 .NET Framework GC는 CPU 시간(컬렉션의 빈도 및 중요성)과 메모리 소비(새 개체, 해제된 개체 또는 사용 가능한 개체에 사용되는 추가 공간) 간의 장단점을 만듭니다. 이전 릴리스의 경우 적절한 균형을 이루도록 GC를 구성하는 방법에 대한 지침을 제공했습니다(예: [ASP.NET 2.0/3.5 공유 호스팅 구성](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)참조).

.NET Framework 4.5의 경우 여러 독립 실행형 설정 대신 이전에 권장하는 모든 GC 설정을 사용할 수 있는 워크로드 정의 구성 설정을 사용할 수 있을 뿐만 아니라 사이트별 작업 집합에 대한 추가 성능을 제공하는 새 튜닝을 사용할 수 있습니다.

GC 메모리 튜닝을 사용하려면 다음 설정을 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 파일에 추가합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

aspnet.config에 대한 변경에 대한 이전 지침에 익숙한 경우 이 설정이 이전 설정을 대체합니다(예: gcServer, gcConcurrent 등을 설정할 필요가 없습니다). 이전 설정을 제거할 필요가 없습니다.

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>웹 응용 프로그램에 대한 프리페칭

**요구 사항**: .NET 프레임 워크 4.5 윈도우 8에서 실행

여러 릴리스의 경우 Windows에는 응용 프로그램 시작의 디스크 읽기 비용을 줄이는 [프리페처라는](http://en.wikipedia.org/wiki/Prefetcher) 기술이 포함되어 있습니다. 콜드 시작은 주로 클라이언트 응용 프로그램의 문제이므로 이 기술은 서버에 필수적인 구성 요소만 포함하는 Windows Server에 포함되지 않았습니다. 이제 개별 웹 사이트의 출시를 최적화할 수 있는 최신 버전의 Windows Server에서 프리페칭을 사용할 수 있습니다.

Windows 서버의 경우 프리페처는 기본적으로 활성화되어 있지 않습니다. 고밀도 웹 호스팅을 위해 프리페처를 활성화하고 구성하려면 명령줄에서 다음 명령 집합을 실행합니다.

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

그런 다음 prefetcher를 ASP.NET 응용 프로그램과 통합하려면 Web.config 파일에 다음을 추가합니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET 웹 양식

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>강력한 형식의 데이터 컨트롤

ASP.NET 4.5에서 Web Forms에는 데이터 작업에 대한 몇 가지 개선 사항이 포함되어 있습니다. 첫 번째 개선 사항은 강력하게 입력된 데이터 컨트롤입니다. 이전 버전의 ASP.NET Web Forms 컨트롤의 경우 *Eval* 및 데이터 바인딩 식을 사용하여 데이터 바인딩값을 표시합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

양방향 데이터 바인딩의 경우 *바인딩을*사용합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

런타임에 이러한 호출은 리플렉션을 사용하여 지정된 멤버의 값을 읽은 다음 결과를 태그에 표시합니다. 이 방법을 사용하면 모양이 없는 임의의 데이터에 대해 데이터를 쉽게 바인딩할 수 있습니다.

그러나 이와 같은 데이터 바인딩 식은 멤버 이름에 대한 IntelliSense, 탐색(예: 정의로 이동) 또는 이러한 이름을 확인하는 컴파일 타임 검사와 같은 기능을 지원하지 않습니다.

이 문제를 해결하기 위해 ASP.NET 4.5는 컨트롤이 바인딩된 데이터의 데이터 형식을 선언하는 기능을 추가합니다. 새 *ItemType* 속성을 사용하여 이 작업을 수행합니다. 이 속성을 설정하면 데이터 바인딩 식의 범위에서 두 개의 새 형식변수를 사용할 수 있습니다: *Item* 및 *BindItem*. 변수는 강력하게 입력되므로 Visual Studio 개발 환경의 모든 이점을 얻을 수 있습니다.

양방향 데이터 바인딩 식의 경우 *BindItem* 변수를 사용합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

데이터 바인딩을 지원하는 ASP.NET Web Forms 프레임워크의 대부분의 컨트롤이 *ItemType* 속성을 지원하도록 업데이트되었습니다.

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>모델 바인딩

모델 바인딩은 ASP.NET Web Forms 컨트롤에서 데이터 바인딩을 확장하여 코드 중심 데이터 액세스와 함께 작동합니다. *ObjectDataSource* 컨트롤과 ASP.NET MVC의 모델 바인딩의 개념을 통합합니다.

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>데이터 선택

모델 바인딩을 사용하여 데이터를 선택하도록 데이터 컨트롤을 구성하려면 컨트롤의 *SelectMethod* 속성을 페이지 코드의 메서드 이름으로 설정합니다. 데이터 컨트롤은 페이지 수명 주기에서 적절한 시간에 메서드를 호출하고 반환된 데이터를 자동으로 바인딩합니다. *DataBind* 메서드를 명시적으로 호출할 필요가 없습니다.

다음 예제에서 *GridView* 컨트롤은 *Get범주:* 라는 메서드를 사용 하도록 구성 됩니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

페이지 코드에서 *GetCategories* 메서드를 만듭니다. 간단한 선택 작업의 경우 메서드는 매개 변수가 필요하지 않으며 *IEnumerable* 또는 *IQueryable* 개체를 반환해야 합니다. 새 *ItemType* 속성이 설정된 경우(앞에서 설명한 대로 강력한 형식의 데이터 바인딩 식에서 설명한 대로 강력한 [형식의 데이터](#_Toc318097386) 바인딩 식을 사용 함) 이러한 인터페이스의 일반 버전(IEnumerable *&lt;T&gt; * 또는 *IQueryable&lt;T)&gt;* 및 *ItemType* 속성의 형식과 일치하는 *T* 매개 변수(예: *&lt;IQueryable&gt;범주)가*반환되어야 합니다.

다음 예제에서는 *GetCategories* 메서드에 대 한 코드를 보여 주다. 이 예제에서는 Northwind 샘플 데이터베이스와 함께 엔터티 프레임워크 코드 첫 번째 모델을 사용합니다. 코드는 쿼리가 *Include* 메서드를 통해 각 범주에 대한 관련 제품의 세부 정보를 반환하는지 확인합니다. 이렇게 하면 태그의 *TemplateField* 요소가 [n+1 선택을](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)요구하지 않고 각 범주의 제품 수를 표시합니다.)

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

페이지가 실행되면 *GridView* 컨트롤은 *GetCategories* 메서드를 자동으로 호출하고 구성된 필드를 사용하여 반환된 데이터를 렌더링합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

select 메서드는 *IQueryable* 개체를 반환하므로 *GridView* 컨트롤은 쿼리를 실행하기 전에 쿼리를 추가로 조작할 수 있습니다. 예를 들어 *GridView* 컨트롤은 실행되기 전에 반환된 *IQueryable* 개체를 정렬하고 페이징하기 위한 쿼리 식을 추가하여 기본 LINQ 공급자에 의해 이러한 작업을 수행할 수 있습니다. 이 경우 Entity Framework는 이러한 작업이 데이터베이스에서 수행되도록 합니다.

다음 예제에서는 정렬 및 페이징을 허용하도록 수정된 *GridView* 컨트롤을 보여 주며 다음과 같은 예제를 보여 주며 다음과 같은 방법을 보여 주며 다음과 같은 방법을 보여 주며 있습니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

이제 페이지가 실행되면 컨트롤은 데이터의 현재 페이지만 표시되고 선택한 열에서 정렬되었는지 확인할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

반환된 데이터를 필터링하려면 매개 변수를 select 메서드에 추가해야 합니다. 이러한 매개 변수는 런타임에 모델 바인딩에 의해 채워지며 데이터를 반환하기 전에 쿼리를 변경하는 데 사용할 수 있습니다.

예를 들어 쿼리 문자열에 키워드를 입력하여 사용자가 제품을 필터링하도록 할 것이라고 가정합니다. 메서드에 매개 변수를 추가하고 매개 변수 값을 사용하도록 코드를 업데이트할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

이 코드에는 *키워드에* 대한 값이 제공된 다음 쿼리 결과를 반환하는 경우 *Where* 식이 포함됩니다.

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>가치 공급자

이전 예제에서는 *키워드* 매개 변수의 값이 어디에서 왔는지에 대해 구체적으로 언급하지 않았습니다. 이 정보를 나타내려면 매개 변수 특성을 사용할 수 있습니다. 이 예제에서는 *System.Web.ModelBinding* 네임스페이스에 있는 *QueryStringAttribute* 클래스를 사용할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

이렇게 하면 모델 바인딩에서 쿼리 문자열에서 런타임에 *키워드* 매개 변수에 값을 바인딩하려고 합니다. 형식 변환을 수행해야 할 수 있지만 이 경우에는 변환하지 않습니다. 값을 제공할 수 없고 형식이 null이 아닌 경우 예외가 throw됩니다.

이러한 메서드의 값 소스를 값 공급자라고 하며 사용할 값 공급자를 나타내는 매개 변수 특성을 값 공급자 특성이라고 합니다. Web Forms에는 쿼리 문자열, 쿠키, 양식 값, 컨트롤, 보기 상태, 세션 상태 및 프로필 속성과 같은 Web Forms 응용 프로그램의 모든 일반적인 사용자 입력 소스에 대한 값 공급자 및 해당 특성이 포함됩니다. 사용자 지정 값 공급자를 작성할 수도 있습니다.

기본적으로 매개 변수 이름은 값 공급자 컬렉션에서 값을 찾기 위한 키로 사용됩니다. 이 예제에서 코드는 키워드라는 쿼리 문자열 값(예: ~/default.aspx?keyword=chef)을 찾습니다. 사용자 지정 키를 매개 변수 특성에 인수로 전달하여 지정할 수 있습니다. 예를 들어 q라는 쿼리 문자열 변수의 값을 사용하려면 다음을 수행할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

이 메서드가 페이지 코드에 있는 경우 사용자는 쿼리 문자열을 사용하여 키워드를 전달하여 결과를 필터링할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

모델 바인딩은 값 읽기, null 값 확인, 적절한 유형으로 변환 시도, 변환이 성공했는지 확인, 마지막으로 쿼리의 값을 사용하여 직접 코딩해야 하는 많은 작업을 수행합니다. 모델 바인딩으로 인해 코드가 훨씬 줄어들고 응용 프로그램 전체에서 기능을 재사용할 수 있습니다.

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>컨트롤의 값으로 필터링

사용자가 드롭다운 목록에서 필터 값을 선택할 수 있도록 예제를 확장한다고 가정합니다. 태그에 다음 드롭다운 목록을 추가하고 *SelectMethod* 속성을 사용하여 다른 메서드에서 데이터를 얻도록 구성합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

일반적으로 일치하는 제품이 없는 경우 컨트롤에 메시지가 표시되도록 *GridView* 컨트롤에 *EmptyDataTemplate* 요소를 추가합니다.

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

페이지 코드에서 드롭다운 목록에 대한 새 선택 메서드를 추가합니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

마지막으로 *GetProducts* select 메서드를 업데이트하여 드롭다운 목록에서 선택한 범주의 ID를 포함하는 새 매개 변수를 가져옵니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

이제 페이지가 실행되면 사용자는 드롭다운 목록에서 범주를 선택할 수 있으며 *GridView* 컨트롤이 자동으로 다시 바인딩되어 필터링된 데이터를 표시할 수 있습니다. 이는 모델 바인딩이 선택 메서드에 대한 매개 변수 값을 추적하고 포스트백 후 매개 변수 값이 변경되었는지 여부를 감지하기 때문에 가능합니다. 이 경우 모델 바인딩은 연결된 데이터 컨트롤을 강제로 데이터에 다시 바인딩합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML 인코딩된 데이터 바인딩 식

이제 데이터 바인딩 식의 결과를 HTML로 인코딩할 수 있습니다. 콜론 추가(:) 데이터 바인딩 식을 &lt;표시하는 %# 접두사 끝에 는

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>눈에 거슬리지 않는 유효성 검사

이제 클라이언트 측 유효성 검사 논리에 눈에 거슬리지 않는 JavaScript를 사용하도록 기본 제공 유효성 검사기 컨트롤을 구성할 수 있습니다. 이렇게 하면 페이지 태그에서 인라인으로 렌더링되는 JavaScript의 양이 크게 줄어들고 전체 페이지 크기가 줄어듭니다. 다음과 같은 방법으로 유효성 검사기 컨트롤에 대한 눈에 거슬리지 않는 JavaScript를 구성할 수 있습니다.

- Web.config 파일의 * &lt;appSettings&gt; * 요소에 다음 설정을 추가하여 전역적으로: 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- 전역적으로 정적 *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* 속성을 *눈에 띄지 않는 유효성 검사Mode.WebForms(일반적으로* Global.asax 파일의 *응용 프로그램\_시작* 메서드)로 설정합니다.
- 페이지 클래스의 새 눈에 *띄지 않는 유효성 검사 유효성 검사 모드* 속성을 눈에 띄지 않는 유효성 검사 유효성 검사 *모드.WebForms로*설정 하여 개별적으로 *페이지에* 대 한 .

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 업데이트

HTML5의 새로운 기능을 활용하기 위해 Web Forms 서버 컨트롤이 일부 개선되었습니다.

- *TextBox* 컨트롤의 *TextMode* 속성은 *전자 메일,* *datetime*등과 같은 새 HTML5 입력 형식을 지원하도록 업데이트되었습니다.
- *FileUpload* 컨트롤은 이제 이 HTML5 기능을 지원하는 브라우저의 여러 파일 업로드를 지원합니다.
- 유효성 검사기 컨트롤은 이제 HTML5 입력 요소의 유효성 을 검사하는 것을 지원합니다.
- URL을 나타내는 특성이 있는 새 HTML5 요소는 이제 runat="서버"를 지원합니다. 따라서 ~ 연산자처럼 URL 경로에서 ASP.NET 규칙을 사용하여 응용 프로그램 루트를 나타낼 &lt;수 있습니다(예: 비디오 runat="서버" src="~/myVideo.wmv" /&gt;).
- *UpdatePanel* 컨트롤은 HTML5 입력 필드 게시를 지원하도록 수정되었습니다.

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 베타는 이제 비주얼 스튜디오 11 베타에 포함되어 있습니다. ASP.NET MVC는 MVC(모델 뷰 컨트롤러) 패턴을 활용하여 테스트가 용이하고 유지 관리 가능한 웹 응용 프로그램을 개발하기 위한 프레임워크입니다. ASP.NET MVC 4를 사용하면 모바일 웹용 응용 프로그램을 쉽게 빌드할 수 있으며 모든 장치에 연결할 수 있는 HTTP 서비스를 빌드하는 데 도움이 되는 ASP.NET 웹 API가 포함되어 있습니다. 자세한 내용은 ASP.NET [MVC 4 릴리스 정보를](mvc4-release-notes.md)참조하십시오.

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET 웹 페이지 2

새로운 기능은 다음과 같습니다.

- 새 사이트 템플릿 및 업데이트된 사이트 템플릿입니다.
- *유효성 검사* 도우미를 사용하여 서버 측 및 클라이언트 측 유효성 검사를 추가합니다.
- 자산 관리자를 사용하여 스크립트를 등록하는 기능입니다.
- OAuth 및 OpenID를 사용하여 페이스 북과 다른 사이트에서 로그인을 활성화.
- *지도* 도우미를 사용하여 맵 추가
- 웹 페이지 응용 프로그램을 나란히 실행합니다.
- 모바일 장치의 페이지 렌더링.

이러한 기능 및 전체 페이지 코드 예제에 대한 자세한 내용은 [웹 페이지 2 베타의 주요 기능을](https://go.microsoft.com/fwlink/?LinkID=227824)참조하십시오.

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>비주얼 웹 개발자 11 베타

이 섹션에서는 Visual Web Developer 11 베타 및 Visual Studio 2012 릴리스 후보의 웹 개발 개선 사항에 대한 정보를 제공합니다.

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>비주얼 스튜디오 2010과 비주얼 스튜디오 2012 릴리스 후보 간의 프로젝트 공유(프로젝트 호환성)

Visual Studio 2012 릴리스 후보까지, 비주얼 스튜디오의 최신 버전에서 기존 프로젝트를 열고 변환 마법사를 시작했습니다. 이로 인해 프로젝트의 콘텐츠(자산)를 이전 버전과 호환되지 않는 새 형식으로 업그레이드해야 했습니다. 따라서 변환 후 이전 버전의 Visual Studio에서 프로젝트를 열 수 없습니다.

많은 고객이 이것이 올바른 접근 방식이 아니라고 말했습니다. Visual Studio 11 베타에서는 이제 Visual Studio 2010 SP1을 통해 프로젝트 및 솔루션 공유를 지원합니다. 즉, Visual Studio 2012 릴리스 후보에서 2010 프로젝트를 열더라도 Visual Studio 2010 SP1에서 프로젝트를 열 수 있습니다.

> [!NOTE]
> 몇 가지 유형의 프로젝트는 Visual Studio 2010 SP1과 Visual Studio 2012 릴리스 후보 간에 공유할 수 없습니다. 여기에는 일부 이전 프로젝트(예: ASP.NET MVC 2 프로젝트) 또는 특수 목적(예: 설치 프로젝트)을 위한 프로젝트가 포함됩니다.

Visual Studio 11 베타에서 처음으로 Visual Studio 2010 SP1 웹 프로젝트를 열면 다음 속성이 프로젝트 파일에 추가됩니다.

- 파일 업그레이드 플래그
- 업그레이드백업위치
- 올드툴스버전
- VisualStudioVersion
- VSToolsPath

파일 업그레이드플래그, 업그레이드백업위치 및 OldToolsVersion은 프로젝트 파일을 업그레이드하는 프로세스에서 사용됩니다. Visual Studio 2010에서 프로젝트 작업에 아무런 영향을 미치지 않습니다.

VisualStudioVersion은 MSBuild 4.5에서 현재 프로젝트에 대한 Visual Studio 버전을 나타내는 새 속성입니다. 이 속성은 MSBuild 4.0(Visual Studio 2010 SP1에서 사용하는 MSBuild 버전)에 존재하지 않았기 때문에 프로젝트 파일에 기본값을 삽입합니다.

VSToolsPath 속성은 MSBuildExtensionsPath32 설정으로 표시되는 경로에서 가져올 올바른 .targets 파일을 결정하는 데 사용됩니다.

가져오기 요소와 관련된 몇 가지 변경 내용도 있습니다. 두 버전의 Visual Studio 간의 호환성을 지원하려면 이러한 변경이 필요합니다.

> [!NOTE]
> 두 대의 서로 다른 컴퓨터에서 Visual Studio 2010 SP1과 Visual Studio 11 Beta 간에 프로젝트를 공유하는\_경우 프로젝트에 앱 데이터 폴더에 로컬 데이터베이스가 포함되어 있는 경우 데이터베이스에서 사용하는 SQL Server 버전이 두 컴퓨터에 설치되어 있는지 확인해야 합니다.

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 웹 사이트 템플릿의 구성 변경 사항

Visual Studio 2012 릴리스 후보의 웹 사이트 템플릿을 사용하여 만든 사이트의 기본 *Web.config* 파일에 대해 다음과 같은 변경 사항이 변경되었습니다.

- `<httpRuntime>` 요소에서 `encoderType` 특성은 이제 ASP.NET 추가된 AntiXSS 형식을 사용하도록 기본적으로 설정됩니다. 자세한 내용은 [AntiXSS 라이브러리를](#_Toc318097382)참조하십시오.
- 또한 `<httpRuntime>` 요소에서 `requestValidationMode` 특성은 "4.5"로 설정됩니다. 즉, 기본적으로 요청 유효성 검사는 지연된("지연") 유효성 검사를 사용하도록 구성됩니다. 자세한 내용은 [새 ASP.NET 요청 유효성 검사 기능을](#_Toc318097379)참조하십시오.
- 섹션의 `<modules>` 요소에는 특성이 `runAllManagedModulesForAllRequests` 포함되어 있지 않습니다. `<system.webServer>` (기본값은 false입니다.) 즉, SP1로 업데이트되지 않은 IIS 7 버전을 사용하는 경우 새 사이트에서 라우팅에 문제가 있을 수 있습니다. 자세한 내용은 [라우팅에 대한 IIS 7의 기본 지원을](#Native_Support_In_IIS7_For_ASPNET_Routine)ASP.NET.

이러한 변경 사항은 기존 응용 프로그램에 영향을 주지 않습니다. 그러나 새 템플릿을 사용하여 ASP.NET 4.5에 대해 만든 기존 웹 사이트와 새 웹 사이트 간의 동작 차이를 나타낼 수 있습니다.

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>ASP.NET 라우팅을 위한 IIS 7의 기본 지원

이 와 같은 ASP.NET 변경 되지 않습니다., 하지만 SP1 업데이트 적용 되지 않은 IIS 7의 버전을 작업 하는 경우 영향을 미칠 수 있는 새 웹 사이트 프로젝트에 대 한 템플릿변경.

ASP.NET 라우팅을 지원하기 위해 다음 구성 설정을 응용 프로그램에 추가할 수 있습니다.

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

**runAllManagedModulesForAllRequests가** true이면 `http://mysite/myapp/home` *URL에 .aspx,* *.mvc*또는 이와 유사한 확장이 없더라도 url과 같은 URL이 ASP.NET.

IIS 7에 대한 업데이트로 인해 **runAllManagedModulesForAllRequests가** 불필요하게 설정되고 기본적으로 라우팅ASP.NET 지원합니다. 업데이트에 대한 자세한 내용은 Microsoft 지원 문서 [특정 IIS 7.0 또는 IIS 7.5 처리기가 기간으로 종료되지 않는 요청을 처리할 수 있는 업데이트를 사용할 수](https://support.microsoft.com/kb/980368)있습니다.)

웹 사이트가 IIS 7에서 실행중이고 IIS가 업데이트된 경우 **runAllManagedModulesForAllRequests를** true로 설정할 필요가 없습니다. 실제로 요청에 불필요한 처리 오버헤드가 추가되므로 true로 설정하는 것은 권장되지 않습니다. 이 설정이 true이면 *.htm,* *.jpg*및 기타 정적 파일에 대한 요청및 기타 정적 파일을 포함한 모든 요청도 요청 ASP.NET 파이프라인을 거닐게 됩니다.

Visual Studio 2012 RC에서 제공되는 템플릿을 사용하여 새 ASP.NET 4.5 웹 사이트를 만드는 경우 웹 사이트의 구성에는 **runAllManagedModulesForAllRequests** 설정이 포함되지 않습니다. 즉, 기본적으로 설정이 false입니다.

그런 다음 SP1이 설치되지 않은 Windows 7에서 웹 사이트를 실행하는 경우 IIS 7에는 필요한 업데이트가 포함되지 않습니다. 결과적으로 라우팅이 작동하지 않으며 오류가 표시됩니다. 라우팅이 작동하지 않는 문제가 있는 경우 다음 중 하나를 수행할 수 있습니다.

- IIS 7에 업데이트를 추가하는 SP1로 Windows 7을 업데이트합니다.
- 이전에 나열된 Microsoft 지원 문서에 설명된 업데이트를 설치합니다.
- 해당 웹 사이트의 Web.config 파일에서 **runAllManagedModulesForAllRequests를** true로 설정합니다. 이렇게 하면 요청에 약간의 오버헤드가 추가됩니다.

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML 편집기

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>스마트 작업

디자인 보기에서 서버 컨트롤의 복잡한 속성에는 쉽게 설정할 수 있도록 대화 상자와 마법사가 연결된 경우가 많습니다. 예를 들어 특수 대화 상자를 사용하여 데이터 원본을 *Repeater* 컨트롤에 추가하거나 *GridView* 컨트롤에 열을 추가할 수 있습니다.

그러나 복잡한 속성에 대한 이러한 유형의 UI 도움말은 소스 보기에서 사용할 수 없습니다. 따라서 Visual Studio 11에서는 소스 보기를 위한 스마트 작업을 소개합니다. 스마트 태스크는 C# 및 Visual Basic 편집기에서 일반적으로 사용되는 기능에 대한 컨텍스트 인식 바로 가기입니다.

ASP.NET Web Forms 컨트롤의 경우 삽입 지점이 요소 내부에 있을 때 서버 태그에 작은 글리프로 스마트 작업이 나타납니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

글리프를 클릭하거나 CTRL+를 누르면 스마트 작업이 확장됩니다. (점)과 마찬가지로 코드 편집기에서도 사용됩니다. 그런 다음 디자인 보기의 스마트 작업과 유사한 바로 가기를 표시합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

예를 들어 이전 그림의 스마트 태스크에는 GridView 작업 옵션이 표시됩니다. 열 편집을 선택하면 다음 대화 상자가 표시됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

대화 상자에 채우기는 설계 보기에서 설정할 수 있는 것과 동일한 속성을 설정합니다. 확인을 클릭하면 컨트롤의 태그가 새 설정으로 업데이트됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>와이 아리아 지원

액세스 가능한 웹 사이트를 작성하는 것이 점점 더 중요해지고 있습니다. [WAI-ARIA 접근성 표준은](http://www.w3.org/WAI/intro/aria) 개발자가 액세스 가능한 웹 사이트를 작성하는 방법을 정의합니다. 이 표준은 이제 Visual Studio에서 완전히 지원됩니다.

예를 들어 *역할* 특성에 전체 IntelliSense가 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

또한 WAI-ARIA 표준은 HTML5 문서에 의미 체계를 추가할 수 있는 *aria가* 접두사에 붙어 있는 특성을 소개합니다. 비주얼 스튜디오는 또한 완전히 이러한 *aria-속성을* 지원합니다 :

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>새로운 HTML5 스니펫

Visual Studio는 일반적으로 사용되는 HTML5 태그를 더 빠르고 쉽게 작성할 수 있도록 여러 스니펫을 포함합니다. 예를 들어 비디오 스니펫은 다음과 같은 것입니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

스니펫을 호출하려면 IntelliSense에서 요소를 선택할 때 탭을 두 번 누릅니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

이렇게 하면 사용자 지정할 수 있는 코드 조각이 생성됩니다.

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>사용자 제어로 추출

큰 웹 페이지에서는 개별 조각을 사용자 컨트롤로 이동하는 것이 좋습니다. 이러한 리팩터링 양식은 페이지의 가독성을 높이고 페이지 구조를 단순화할 수 있습니다.

이를 쉽게 하기 위해 소스 보기에서 웹 양식 페이지를 편집할 때 이제 페이지에서 텍스트를 선택하고 마우스 오른쪽 단추로 클릭한 다음 사용자 컨트롤로 추출을 선택할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>속성의 코드 너겟에 대한 IntelliSense

Visual Studio는 항상 모든 페이지 또는 컨트롤에서 서버 측 코드 너겟에 대한 IntelliSense를 제공했습니다. 이제 비주얼 스튜디오뿐만 아니라 HTML 속성의 코드 너겟에 대한 IntelliSense를 포함한다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

이렇게 하면 데이터 바인딩 식을 더 쉽게 만들 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>개폐 태그의 이름을 바꿀 때 일치하는 태그의 자동 이름 바꾸기

HTML 요소의 이름을 바꾸면(예: *div* 태그를 *헤더* 태그로 변경) 해당 개폐 태그도 실시간으로 변경됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

이렇게 하면 닫는 태그를 변경하거나 잘못된 태그를 변경하는 것을 잊어버린 오류를 방지할 수 있습니다.

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>이벤트 처리기 생성

이제 Visual Studio에는 이벤트 처리기를 작성하고 수동으로 바인딩하는 데 도움이 되는 소스 보기의 기능이 포함되어 있습니다. 소스 보기에서 이벤트 이름을 편집하는 경우 IntelliSense는&gt;새 이벤트 만들기를 표시하여 &lt;올바른 서명이 있는 페이지 코드에서 이벤트 처리기를 만듭니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

기본적으로 이벤트 처리기는 이벤트 처리 메서드의 이름에 컨트롤의 ID를 사용합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

결과 이벤트 처리기는 다음과 같습니다(이 경우 C#).

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>스마트 들여쓰기

빈 HTML 요소 안에 있는 동안 Enter를 누르면 편집기에서 삽입 지점을 올바른 위치에 배치합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

이 위치에 Enter를 누르면 닫는 태그가 아래로 이동하고 개구 태그와 일치하도록 들여쓰기됩니다. 삽입 점도 들여쓰기됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>명령문 자동 축소 완료

이제 Visual Studio의 IntelliSense 목록은 입력한 내용에 따라 필터링되므로 관련 옵션만 표시됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense는 또한 IntelliSense 목록에서 개별 단어의 제목 대/소문자를 기반으로 필터링합니다. 예를 들어 "dl"을 입력하면 dl과 asp:DataList가 모두 표시됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

이 기능을 사용하면 알려진 요소에 대한 명령문 완성을 더 빠르게 얻을 수 있습니다.

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript 편집기

비주얼 스튜디오 2012 릴리스 후보의 자바 스크립트 편집기는 완전히 새로운 이며 크게 비주얼 스튜디오에서 자바 스크립트와 함께 작업의 경험을 향상.

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>코드 개요

이제 모든 함수에 대해 윤곽영역이 자동으로 생성되므로 현재 포커스와 관련이 없는 파일 의 일부를 축소할 수 있습니다.

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>중괄호 일치

삽입 점을 개구부 또는 닫는 중괄호에 놓으면 편집기가 일치하는 중괄호를 강조 표시됩니다.

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>정의로 이동

정의로 이동 명령을 사용하면 함수 또는 변수의 소스로 이동할 수 있습니다.

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 지원

편집기는 자바스크립트 언어를 설명하는 표준의 최신 버전인 ECMAScript5의 새 구문 및 API를 지원합니다.

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>돔 인텔리센스

DOM API에 대한 IntelliSense가 개선되었으며 *쿼리 선택기,* DOM 저장소, 문서 간 메시징 및 *캔버스를*비롯한 많은 새로운 HTML5 API를 지원합니다. DOM IntelliSense는 이제 네이티브 형식 라이브러리 정의가 아닌 단일 간단한 자바스크립트 파일에 의해 구동됩니다. 이렇게 하면 쉽게 확장하거나 교체할 수 있습니다.

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC 서명 오버로드

이 예제와 같이 새 * &lt;서명&gt; * 요소를 사용하여 JavaScript 함수의 별도의 오버로드에 대해 자세한 IntelliSense 주석을 선언할 수 있습니다.

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>암시적 참조

이제 자바스크립트 파일을 중앙 목록에 추가하여 자바스크립트 파일이나 블록 레퍼런스가 포함된 파일 목록에 암시적으로 포함될 수 있습니다. 예를 들어, 파일의 중앙 목록에 jQuery 파일을 추가할 수 있습니다., 그리고 당신은 얻을 거 야 질의 함수에 대 한 모든 자바 스크립트 블록파일, 명시적으로 참조 했 든 여부 (사용 하 여 /// &lt;참조/)&gt;.

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS 편집기

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>명령문 자동 축소 완료

CSS의 IntelliSense 목록은 이제 선택한 스키마에서 지원하는 CSS 속성 및 값을 기반으로 필터링됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense는 타이틀 케이스 검색도 지원합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>계층적 들여쓰기

CSS 편집기는 들여쓰기를 사용하여 계층 적 규칙을 표시하므로 계단식 규칙이 논리적으로 구성되는 방법에 대한 개요를 제공합니다. 다음 예제에서 선택기 #list 목록의 계단식 자식이므로 들여쓰기됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

다음 예제에서는 보다 복잡한 상속을 보여 주며 다음과 같은 보다 복잡한 상속을 보여 주며 다음과 같은 보다 복잡한 상속을 보여

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

규칙의 들여쓰기는 상위 규칙에 의해 결정됩니다. 계층 적 들여쓰기는 기본적으로 활성화되어 있지만 옵션 대화 상자 (도구, 메뉴 모음의 옵션)를 비활성화 할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS 해킹 지원

수백 개의 실제 CSS 파일을 분석하면 CSS 해킹이 매우 일반적이며 이제 Visual Studio가 가장 널리 사용되는 파일을 지원합니다. 이 지원에는 IntelliSense 및 별\*() 및\_밑줄 () 속성 해킹의 유효성 검사가 포함됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

일반적인 선택기 해킹도 지원되므로 계층적 들여쓰기가 적용될 때도 유지됩니다. 인터넷 익스플로러 7을 대상으로하는 데 사용되는 일반적인 선택기 해킹은 * \*:첫 번째 자식 + HTML로*선택기를 준비하는 것입니다. 이 규칙을 사용하면 계층적 들여쓰기가 유지됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>공급업체 별 스키마(-moz-, -웹킷)

CSS3는 서로 다른 시간에 다른 브라우저에서 구현된 많은 속성을 소개합니다. 이전에는 개발자가 공급업체별 구문을 사용하여 특정 브라우저에 대해 코딩해야 했습니다. 이러한 브라우저별 속성은 이제 IntelliSense에 포함됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>댓글 달기 및 댓글 달기 지원

이제 코드 편집기에서 사용하는 것과 동일한 바로 가기(Ctrl+K, C에 주석을 달고 Ctrl+K, 주석 을 해제할 수 있음)를 사용하여 CSS 규칙에 주석을 달고 주석을 달 수 있습니다.

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>색 선택

이전 버전의 Visual Studio에서는 색상 관련 특성에 대한 IntelliSense가 명명된 색상 값의 드롭다운 목록으로 구성되었습니다. 이 목록은 모든 기능을 갖춘 컬러 선택으로 대체되었습니다.

색상 값을 입력하면 색상 선택기가 자동으로 표시되고 이전에 사용한 색상 목록이 표시되고 기본 색상 팔레트가 표시됩니다. 마우스 나 키보드를 사용하여 색상을 선택할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

목록을 전체 색상 선택기로 확장할 수 있습니다. 불투명도 슬라이더를 이동할 때 모든 색상을 RGBA로 자동으로 변환하여 알파 채널을 제어할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>코드 조각

CSS 편집기의 스니펫을 통해 브라우저 간 스타일을 더 쉽고 빠르게 만들 수 있습니다. 브라우저별 설정이 필요한 많은 CSS3 속성이 이제 코드 조각으로 롤백되었습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS 스니펫은 IntelliSense 목록을 보여 주면 at-symbol(@를 입력하여 CSS3 미디어 쿼리와 같은 고급 시나리오를 지원합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

값을 선택하고 @media 탭을 누르면 CSS 편집기에서 다음 스니펫을 삽입합니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

코드용 코드 조각과 마찬가지로 사용자 고유의 CSS 스니펫을 만들 수 있습니다.

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>사용자 지정 지역

코드 편집기에서 이미 사용할 수 있는 명명된 코드 영역은 이제 CSS 편집에 사용할 수 있습니다. 이렇게 하면 관련 스타일 블록을 쉽게 그룹화할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

영역이 축소되면 영역 이름이 표시됩니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>페이지 검사기

페이지 검사기는 Visual Studio IDE에서 웹 페이지(HTML, 웹 양식, ASP.NET MVC 또는 웹 페이지)를 렌더링하고 소스 코드와 결과 출력을 모두 검사할 수 있는 도구입니다. ASP.NET 페이지의 경우 Page Inspector를 사용하면 브라우저에 렌더링되는 HTML 태그를 생성한 서버 측 코드를 확인할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

페이지 관리자에 대한 자세한 내용은 다음 자습서를 참조하십시오.

- [ASP.NET MVC에서](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md) 페이지 검사기 사용
- ASP.NET 웹 [양식에서](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md) 페이지 검사기 사용

<a id="_Toc318097425"></a>
### <a name="publishing"></a>게시

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>게시 프로필

Visual Studio 2010에서는 웹 응용 프로그램 프로젝트에 대한 게시 정보가 버전 제어에 저장되지 않으며 다른 사람과 공유하도록 설계되지 않았습니다. Visual Studio 2012 릴리스 후보에서 게시 프로필의 형식이 변경되었습니다. 팀 아티팩트가 만들어졌으며 이제 MSBuild를 기반으로 빌드에서 쉽게 활용할 수 있습니다. 빌드 구성 정보는 게시 대화 상자에 있으므로 게시하기 전에 빌드 구성을 쉽게 전환할 수 있습니다.

게시 프로필은 PublishProfiles 폴더에 저장됩니다. 폴더의 위치는 사용 중인 프로그래밍 언어에 따라 다릅니다.

- C#: 속성\게시 프로필
- 비주얼 기본: 내 프로젝트\게시프로필

각 프로필은 MSBuild 파일입니다. 게시하는 동안 이 파일은 프로젝트의 MSBuild 파일로 가져옵니다. Visual Studio 2010에서 게시 또는 패키지 프로세스를 변경하려면 **ProjectName**.wpp.targets라는 파일에 사용자 지정을 입력해야 합니다. 이 지원은 계속 지원되지만 이제 게시 프로필 자체에 사용자 지정을 넣을 수 있습니다. 이렇게 하면 사용자 지정은 해당 프로필에만 사용됩니다.

이제 MSBuild의 게시 프로필을 활용할 수도 있습니다. 이렇게 하려면 프로젝트를 빌드할 때 다음 명령을 사용합니다.

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

project.csproj 값은 프로젝트의 경로이며 ProfileName은 게시할 프로필의 이름입니다. 또는 *PublishProfile* 속성의 프로필 이름을 전달하는 대신 전체 경로를 게시 프로필에 전달할 수 있습니다.

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>사전 컴파일 및 병합ASP.NET

웹 응용 프로그램 프로젝트의 경우 Visual Studio 2012 릴리스 후보는 프로젝트를 게시하거나 패키지할 때 사이트의 콘텐츠를 미리 컴파일하고 병합할 수 있는 패키지/게시 웹 속성 페이지에 옵션을 추가합니다. 이러한 옵션을 보려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 속성을 선택한 다음 패키지/웹 속성 페이지를 선택합니다. 다음 그림에서는 옵션을 게시하기 전에 이 응용 프로그램을 미리 컴파일할 수 있습니다.

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

이 옵션을 선택하면 웹 응용 프로그램을 게시하거나 패키지할 때마다 Visual Studio에서 응용 프로그램을 미리 컴파일합니다. 사이트가 미리 컴파일되는 방법 또는 어셈블리병합 방법을 제어하려면 고급 단추를 클릭하여 해당 옵션을 구성합니다.

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

비주얼 스튜디오에서 웹 프로젝트를 테스트하기위한 기본 웹 서버는 이제 IIS 익스프레스입니다. Visual Studio 개발 서버는 개발 중에도 로컬 웹 서버의 옵션이지만 IIS Express는 이제 권장 서버가 되었습니다. 비주얼 스튜디오 11 베타에서 IIS Express를 사용하는 경험은 Visual Studio 2010 SP1에서 사용하는 것과 매우 유사합니다.

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>고지 사항

본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.

이 문서에 포함된 정보는 게시 날짜 당시 논의된 문제에 대한 Microsoft Corporation의 현재 관점을 나타냅니다. Microsoft는 변화하는 시장 상황에 대응해야 하므로 Microsoft의 약속으로 해석되지 않아야 하며, Microsoft는 게시 날짜 이후 제시된 정보의 정확성을 보증하지 않습니다.

이 백서는 정보 제공만을 목적으로 합니다. Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.

해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나 검색 시스템에 저장 또는 도입되거나 전송될 수 없습니다.

Microsoft는 이 설명서 본안에 관련된 특허권, 상표권, 저작권, 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 설명서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권 또는 기타 지적 재산권 등에 대한 어떠한 사용권도 허용하지 않습니다.

달리 명시되지 않는 한, 예를 들어 회사, 조직, 제품, 도메인 이름, 이메일 주소, 로고, 로고, 장소 또는 이벤트는 가상이며 실제 회사, 조직, 제품, 도메인 이름, 이메일 주소, 로고, 사람, 장소 또는 이벤트와 관련이 없습니다.

© 2012 Microsoft Corporation. All rights reserved.

Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.

여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.
