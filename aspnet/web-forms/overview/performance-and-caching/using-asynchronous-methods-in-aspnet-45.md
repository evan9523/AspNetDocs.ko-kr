---
uid: web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
title: ASP.NET 4.5 |에서 비동기 메서드 사용 Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 무료로 제공 되는 웹 Visual Studio Express 2012를 사용 하 여 비동기 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항에 대해 설명 합니다.
ms.author: riande
ms.date: 01/02/2019
ms.assetid: a585c9a2-7c8e-478b-9706-90f3739c50d1
msc.legacyurl: /web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: a0aed792c5a2e790eed10c1aecf84fe5e535cea4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045158"
---
# <a name="using-asynchronous-methods-in-aspnet-45"></a>ASP.NET 4.5에서 비동기 메서드 사용

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 [웹 Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11)를 사용 하 여 비동기 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)을 사용할 수도 있습니다. 이 자습서에는 다음 섹션이 포함 되어 있습니다.
> 
> - [스레드 풀에서 요청이 처리되는 방법](#HowRequestsProcessedByTP)
> - [동기 또는 비동기 메서드 선택](#ChoosingSyncVasync)
> - [응용 프로그램 예제](#SampleApp)
> - [Gizmo 그리려면 동기 페이지](#GizmosSynch)
> - [비동기 Gizmo 그리려면 페이지 만들기](#CreatingAsynchGizmos)
> - [여러 작업을 병렬로 수행](#Parallel)
> - [취소 토큰 사용](#CancelToken)
> - [높은 동시성/대기 시간이 긴 웹 서비스 호출을 위한 서버 구성](#ServerConfig)
> 
> 에서이 자습서에 대 한 전체 샘플이 제공 됩니다.  
> [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/)[GitHub](https://github.com/) 사이트에 있습니다.

ASP.NET 4.5 웹 페이지 ( [.net 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx) 조합)를 사용 하면 [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)형식의 개체를 반환 하는 비동기 메서드를 등록할 수 있습니다. .NET Framework 4에서는 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 이라고 하는 비동기 프로그래밍 개념을 도입 했으며 ASP.NET 4.5은 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)을 지원 합니다. 작업은 **작업** 형식 및 [system.object](https://msdn.microsoft.com/library/system.threading.tasks.aspx) 네임 스페이스의 관련 형식으로 표시 됩니다. .NET Framework 4.5는 이전 비동기 방법 보다 훨씬 더 복잡 한 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 개체 작업을 수행 하는 [wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드를 사용 하 여이 비동기 지원을 기반으로 합니다. [Wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드는 코드 조각이 다른 코드 부분에서 비동기적으로 대기 해야 함을 나타내는 구문상의 약어입니다. [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드는 메서드를 작업 기반 비동기 메서드로 표시 하는 데 사용할 수 있는 힌트를 나타냅니다. **Wait**, **async**및 **Task** 개체의 조합을 사용 하면 .net 4.5에서 비동기 코드를 훨씬 쉽게 작성할 수 있습니다. 비동기 메서드에 대 한 새 모델을 *작업 기반 비동기 패턴* (**탭**) 이라고 합니다. 이 자습서에서는 [wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드 및 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 네임 스페이스를 사용 하는 비동기 프로그래밍에 대해 잘 알고 있다고 가정 합니다.

[Wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드 및 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 네임 스페이스 사용에 대 한 자세한 내용은 다음 참조를 참조 하세요.

- [백서: .NET의 비동기](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Async/Wait FAQ](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio 비동기 프로그래밍](https://msdn.microsoft.com/vstudio/gg316360)

## <a name="how-requests-are-processed-by-the-thread-pool"></a><a id="HowRequestsProcessedByTP"></a>  스레드 풀에서 요청을 처리 하는 방법

웹 서버에서 .NET Framework는 ASP.NET 요청을 처리 하는 데 사용 되는 스레드 풀을 유지 관리 합니다. 요청이 도착하면 해당 요청을 처리하기 위해 풀에서 하나의 스레드가 디스패치됩니다. 요청이 동기적으로 처리 되는 경우 요청이 처리 되는 동안 요청을 처리 하는 스레드가 사용 중이 고 해당 스레드가 다른 요청을 처리할 수 없습니다.   
  
스레드 풀을 많은 사용량이 많은 스레드를 수용할 수 있을 만큼 충분히 크게 만들 수 있으므로이는 문제가 되지 않을 수 있습니다. 그러나 스레드 풀의 스레드 수는 제한 됩니다 (.NET 4.5의 기본 최대값은 5000 임). 장기 실행 요청의 동시성이 높은 대규모 응용 프로그램에서는 사용 가능한 모든 스레드가 사용 중일 수 있습니다. 이러한 상황을 스레드 고갈이라고 합니다. 이 조건에 도달 하면 웹 서버는 요청을 큐에 대기 시킵니다. 요청 큐가 가득 차면 웹 서버는 HTTP 503 상태 (서버 사용량이 많음)를 포함 하는 요청을 거부 합니다. CLR 스레드 풀에는 새 스레드 주입에 대 한 제한이 있습니다. 동시성이 버스 티 (즉, 웹 사이트에 갑자기 많은 수의 요청이 있을 수 있음), 대기 시간이 긴 백 엔드 호출로 인해 사용 가능한 모든 요청 스레드가 사용 중인 경우 제한 된 스레드 주입 속도로 인해 응용 프로그램의 응답 성능이 저하 될 수 있습니다. 또한 스레드 풀에 추가 된 각 새 스레드에는 오버 헤드 (예: 1mb 스택 메모리)가 있습니다. 스레드 풀이 .NET 4.5 기본 최대값인 5로 증가 하는 대기 시간 호출을 처리 하는 동기 메서드를 사용 하는 웹 응용 프로그램은 응용 프로그램에서 비동기 메서드를 사용 하 여 동일한 요청을 처리할 수 있는 것 보다 약 5gb의 메모리를 사용 하 고 50 스레드만 사용 합니다. 비동기 작업을 수행 하는 경우 항상 스레드를 사용 하는 것은 아닙니다. 예를 들어 비동기 웹 서비스 요청을 수행 하는 경우 ASP.NET는 **비동기** 메서드 호출과 대기 사이의 스레드를 사용 하지 **않습니다.** 대기 시간이 긴 서비스 요청에 스레드 풀을 사용 하면 메모리 사용 공간이 많고 서버 하드웨어 사용률이 저하 될 수 있습니다.

## <a name="processing-asynchronous-requests"></a>비동기 요청 처리

시작 시 많은 수의 동시 요청이 표시 되거나 버스 티 부하가 있는 웹 응용 프로그램 (동시성이 갑자기 증가 하는 경우), 웹 서비스 호출을 통해 응용 프로그램의 응답성이 향상 됩니다. 하나의 비동기 요청을 처리하는 시간은 하나의 동기 요청을 처리하는 시간과 동일합니다. 예를 들어 요청에서 완료 하는 데 2 초가 필요한 웹 서비스 호출을 수행 하는 경우이 요청은 동기적으로 수행 되는지 또는 비동기적으로 수행 될 때 2 초가 걸립니다. 그러나 비동기 호출 중에는 스레드가 다른 요청에 대 한 응답을 차단 하지 않고 첫 번째 요청이 완료 될 때까지 기다립니다. 따라서 비동기 요청은 장기 실행 작업을 호출 하는 동시 요청이 많은 경우 요청 큐 및 스레드 풀 증가를 방지 합니다.

## <a name="choosing-synchronous-or-asynchronous-methods"></a><a id="ChoosingSyncVasync"></a>  동기 또는 비동기 메서드 선택

이 섹션에서는 동기 또는 비동기 메서드를 사용 하는 경우에 대 한 지침을 제공 합니다. 단지 지침입니다. 각 응용 프로그램을 개별적으로 검사 하 여 비동기 메서드가 성능에 도움이 되는지 확인 합니다.

일반적으로 다음과 같은 경우에는 동기 메서드를 사용 합니다.

- 작업이 단순하거나 단기 실행 작업인 경우
- 단순성이 효율성보다 더 중요한 경우
- 작업이 광범위한 디스크 또는 네트워크 오버헤드를 유발하는 작업이 아닌 주로 CPU 작업인 경우. CPU 바인딩된 작업에 비동기 메서드를 사용 하면 어떠한 이점도 없으며 오버 헤드가 증가 합니다.

일반적으로 다음 조건에 대해 비동기 메서드를 사용 합니다.

- 비동기 메서드를 통해 사용할 수 있는 서비스를 호출 하 고 있으며 .NET 4.5 이상을 사용 하 고 있습니다.
- 작업이 CPU 관련 작업이 아닌 네트워크 또는 I/O 관련 작업인 경우
- 병렬 처리가 코드의 단순성보다 더 중요한 경우
- 사용자에게 장기 실행 요청을 취소할 수 있는 메커니즘을 제공하려는 경우
- 스레드 전환의 혜택이 컨텍스트 전환 비용을 능가 하는 경우 일반적으로 동기 메서드가 작업을 수행 하지 않고 ASP.NET request 스레드를 차단 하는 경우 메서드를 비동기적으로 설정 해야 합니다. 비동기 호출을 수행 하 여 ASP.NET request 스레드는 웹 서비스 요청이 완료 되기를 기다리는 동안 작업을 수행 하지 않도록 차단 되지 않습니다.
- 테스트를 통해 차단 작업은 사이트 성능의 병목 상태 이며 IIS는 이러한 차단 호출에 비동기 메서드를 사용 하 여 더 많은 요청을 수행할 수 있음을 보여 줍니다.

  다운로드 가능한 샘플에서는 비동기 메서드를 효과적으로 사용 하는 방법을 보여 줍니다. 제공 된 샘플은 ASP.NET 4.5의 비동기 프로그래밍에 대 한 간단한 데모를 제공 하도록 설계 되었습니다. 이 샘플은 ASP.NET의 비동기 프로그래밍에 대 한 참조 아키텍처로 작성 된 것이 아닙니다. 샘플 프로그램은 작업을 호출 하는 [ASP.NET Web API](../../../web-api/index.md) 메서드를 호출 합니다. 장기 실행 웹 서비스 호출을 시뮬레이션 하기 위해 [지연 됩니다.](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 대부분의 프로덕션 응용 프로그램에는 비동기 메서드를 사용 하는 경우 이러한 분명 한 이점이 표시 되지 않습니다.   
  
일부 응용 프로그램에는 모든 메서드가 비동기 방식으로 필요 합니다. 몇 가지 동기 메서드를 비동기 메서드로 변환 하는 것이 필요한 작업량에 대해 최상의 효율성을 제공 하는 경우가 많습니다.

## <a name="the-sample-application"></a><a id="SampleApp"></a>  응용 프로그램 예제

[https://github.com/RickAndMSFT/Async-ASP.NET](https://github.com/RickAndMSFT/Async-ASP.NET) [GitHub](https://github.com/) 사이트의에서 샘플 응용 프로그램을 다운로드할 수 있습니다. 리포지토리는 세 가지 프로젝트로 구성 됩니다.

- *WebAppAsync*: Web API **WebAPIpwg** 서비스를 사용 하는 ASP.NET Web Forms 프로젝트입니다. 이 자습서에 대 한 대부분의 코드는이 프로젝트에서 가져온 것입니다.
- *WebAPIpgw*: 컨트롤러를 구현 하는 ASP.NET MVC 4 Web API 프로젝트 `Products, Gizmos and Widgets` 입니다. *WebAppAsync* 프로젝트 및 *Mvc4Async* 프로젝트에 대 한 데이터를 제공 합니다.
- *Mvc4Async*: 다른 자습서에서 사용 되는 코드를 포함 하는 ASP.NET MVC 4 프로젝트입니다. **WebAPIpwg** 서비스에 대 한 Web API 호출을 수행 합니다.

## <a name="the-gizmos-synchronous-page"></a><a id="GizmosSynch"></a>  Gizmo 그리려면 동기 페이지

 다음 코드에서는 `Page_Load` gizmo 그리려면 목록을 표시 하는 데 사용 되는 동기 메서드를 보여 줍니다. 이 문서에서 gizmo는 가상 기계적 장치입니다. 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample1.cs)]

다음 코드에서는 `GetGizmos` gizmo 서비스의 메서드를 보여 줍니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample2.cs)]

`GizmoService GetGizmos`메서드는 gizmo 그리려면 데이터 목록을 반환 하는 ASP.NET WEB API HTTP 서비스에 URI를 전달 합니다. *WebAPIpgw* 프로젝트에는 Web API 및 컨트롤러의 구현이 포함 되어 있습니다 `gizmos, widget` `product` .  
다음 이미지는 샘플 프로젝트의 gizmo 그리려면 페이지를 보여 줍니다.

![Gizmo 그리려면](using-asynchronous-methods-in-aspnet-45/_static/image1.png)

## <a name="creating-an-asynchronous-gizmos-page"></a><a id="CreatingAsynchGizmos"></a>  비동기 Gizmo 그리려면 페이지 만들기

이 샘플에서는 새로운 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 및 [wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드 (.Net 4.5 및 Visual Studio 2012에서 사용 가능)를 사용 하 여 컴파일러가 비동기 프로그래밍에 필요한 복잡 한 변환을 유지 관리할 수 있도록 합니다. 컴파일러를 사용 하면 c #의 동기 제어 흐름 구문을 사용 하 여 코드를 작성할 수 있으며, 컴파일러는 스레드 차단을 방지 하기 위해 콜백을 사용 하는 데 필요한 변환을 자동으로 적용 합니다.

ASP.NET 비동기 페이지는 [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) `Async` 특성이 "true"로 설정 된 Page 지시어를 포함 해야 합니다. 다음 코드는 [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) `Async` *GizmosAsync* 페이지에 대해 특성이 "True"로 설정 된 페이지 지시문을 보여 줍니다.

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample3.aspx?highlight=1)]

다음 코드에서는 `Gizmos` 동기 `Page_Load` 메서드와 비동기 페이지를 보여 줍니다 `GizmosAsync` . 브라우저에서 [HTML 5 &lt; 표시 &gt; 요소](http://www.w3.org/wiki/HTML/Elements/mark)를 지 원하는 경우의 변경 내용이 노란색 강조 표시로 표시 됩니다 `GizmosAsync` .

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample4.cs)]

비동기 버전:

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample5.cs?highlight=3,6-7,9,11)]

 다음 변경 내용이 적용 되어 `GizmosAsync` 페이지를 비동기로 허용 합니다.

- [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) 지시문에는 `Async` 특성이 "true"로 설정 되어 있어야 합니다.
- `RegisterAsyncTask`메서드는 비동기적으로 실행 되는 코드를 포함 하는 비동기 작업을 등록 하는 데 사용 됩니다.
- 새 `GetGizmosSvcAsync` 메서드는 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드로 표시 됩니다 .이 키워드는 본문의 부분에 대 한 콜백을 생성 하 고 반환 되는을 자동으로 만들기 위해 컴파일러에 지시 합니다 `Task` .
- &quot;Async &quot; 가 비동기 메서드 이름에 추가 되었습니다. "Async"를 추가 하는 것은 필요 하지 않지만 비동기 메서드를 작성 하는 경우에는 규칙입니다.
- 새 메서드의 반환 형식은 `GetGizmosSvcAsync` `Task` 입니다. 의 반환 형식은 `Task` 진행 중인 작업을 나타내며는 비동기 작업의 완료를 대기 하는 핸들을 사용 하 여 메서드의 호출자에 게 제공 합니다.
- [Wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드가 웹 서비스 호출에 적용 되었습니다.
- 비동기 웹 서비스 API가 호출 된 `GetGizmosAsync` 경우 ()

`GetGizmosSvcAsync`메서드 본문 내에서 다른 비동기 메서드를 `GetGizmosAsync` 호출 합니다. `GetGizmosAsync``Task<List<Gizmo>>`데이터를 사용할 수 있을 때 최종적으로 완료 되는를 즉시 반환 합니다. Gizmo 데이터가 있을 때까지 다른 작업을 수행 하지 않으려는 경우 코드는 **wait** 키워드를 사용 하 여 작업을 기다립니다 합니다. **Wait** 키워드는 **async** 키워드로 주석이 지정 된 메서드에만 사용할 수 있습니다.

**Wait** 키워드는 태스크가 완료 될 때까지 스레드를 차단 하지 않습니다. 메서드의 나머지 부분을 작업의 콜백으로 등록 하 고를 즉시 반환 합니다. 대기 작업이 최종적으로 완료 되 면 해당 콜백을 호출 하 고, 중단 된 위치에서 즉시 메서드 실행을 다시 시작 합니다. [Wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 및 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드 및 [작업](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 네임 스페이스를 사용 하는 방법에 대 한 자세한 내용은 [비동기 참조](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async)를 참조 하세요.

다음 코드에서는 `GetGizmos` 및 `GetGizmosAsync` 메서드를 보여 줍니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample6.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample7.cs?highlight=1,4-8)]

 비동기 변경은 위의 **GizmosAsync** 와 비슷합니다. 

- 메서드 시그니처에 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 키워드로 주석이 추가 되었고, 반환 형식이로 변경 되 `Task<List<Gizmo>>` 고, *async* 가 메서드 이름에 추가 되었습니다.
- 비동기 [Httpclient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) 클래스는 동기 [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) 클래스 대신 사용 됩니다.
- [Wait](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 키워드가 [httpclient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)[getasync](https://msdn.microsoft.com/library/hh158944(VS.110).aspx) 비동기 메서드에 적용 되었습니다.

다음 이미지는 비동기 gizmo 뷰를 보여 줍니다.

![async](using-asynchronous-methods-in-aspnet-45/_static/image2.png)

Gizmo 그리려면 데이터의 브라우저 프레젠테이션은 동기 호출로 생성 된 뷰와 동일 합니다. 유일한 차이점은 비동기 버전이 부하가 많은 경우 성능이 더 높을 수 있다는 것입니다.

## <a name="registerasynctask-notes"></a>RegisterAsyncTask 참고 사항

로 연결 된 메서드 `RegisterAsyncTask` 는 [PreRender](https://msdn.microsoft.com/library/ms178472.aspx)후 즉시 실행 됩니다.

비동기 void 페이지 이벤트를 직접 사용 하는 경우 다음 코드와 같이 합니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample8.cs)]

더 이상 이벤트가 실행 되는 시기를 완전히 제어할 수 없습니다. 예를 들어 .aspx 및입니다. Master `Page_Load` 는 이벤트를 정의 하 고 둘 중 하나 또는 둘 다 비동기 이므로 실행 순서를 보장할 수 없습니다. 이벤트 처리기 (예:)에 대해 동일한 확정 되지 않은 순서가 `async void Button_Click` 적용 됩니다.

## <a name="performing-multiple-operations-in-parallel"></a><a id="Parallel"></a>  여러 작업을 병렬로 수행

비동기 메서드는 작업에서 여러 독립적인 작업을 수행 해야 하는 경우 동기 메서드에 비해 상당한 이점이 있습니다. 제공 된 샘플에서 동기 페이지 *PWG*(제품, 위젯 및 gizmo 그리려면)는 세 개의 웹 서비스 호출 결과를 표시 하 여 제품, 위젯 및 gizmo 그리려면 목록을 가져옵니다. 이러한 서비스를 제공 하는 [ASP.NET Web API](../../../web-api/index.md) 프로젝트는 작업을 사용 [합니다. 지연](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 시간을 시뮬레이션 하거나 네트워크 호출을 느리게 합니다. 지연이 500 밀리초로 설정 된 경우 동기 버전이 1500 밀리초를 초과 하는 동안 비동기 *PWGasync* 페이지를 완료 하는 데 약간의 500 밀리초가 소요 됩니다 `PWG` . 다음 코드에는 동기 *PWG* 페이지가 나와 있습니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample9.cs)]

아래에는 비동기 `PWGasync` 코드를 보여 줍니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample10.cs?highlight=5,11,21)]

다음 이미지는 비동기 *PWGasync* 페이지에서 반환 되는 뷰를 보여 줍니다.

![](using-asynchronous-methods-in-aspnet-45/_static/image3.png)

## <a name="using-a-cancellation-token"></a><a id="CancelToken"></a>  취소 토큰 사용

을 반환 하는 비동기 메서드는 `Task` 취소할 수 있으며 Page 지시어의 특성과 함께 제공 되는 경우 [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) 매개 변수를 사용 `AsyncTimeout` 합니다. [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) 다음 코드에서는 제한 시간 (초)이 있는 *Gizmoscancelasync .aspx* 페이지를 보여 줍니다.

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample11.aspx?highlight=1)]

다음 코드는 *GizmosCancelAsync.aspx.cs* 파일을 보여 줍니다.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample12.cs?highlight=6,9)]

제공 된 샘플 응용 프로그램에서 *gizmoscancelasync* 링크를 선택 하면 *gizmoscancelasync .aspx* 페이지가 호출 되 고 비동기 호출의 취소 (제한 시간)가 설명 됩니다. 지연 시간이 임의 범위 내에 있으므로 페이지를 몇 번 새로 고쳐 시간 초과 오류 메시지를 가져와야 할 수 있습니다.

## <a name="server-configuration-for-high-concurrencyhigh-latency-web-service-calls"></a><a id="ServerConfig"></a>  높은 동시성/대기 시간이 긴 웹 서비스 호출을 위한 서버 구성

비동기 웹 응용 프로그램의 이점을 실현 하려면 기본 서버 구성을 변경 해야 할 수 있습니다. 비동기 웹 응용 프로그램을 구성 하 고 스트레스 테스트할 때 다음 사항에 유의 하세요.

- Windows 7, Windows Vista, Window 8 및 모든 Windows 클라이언트 운영 체제에는 최대 10 개의 동시 요청이 있습니다. 높은 부하 상태에서 비동기 메서드의 이점을 확인 하려면 Windows Server 운영 체제가 필요 합니다.
- 다음 명령을 사용 하 여 관리자 권한 명령 프롬프트에서 IIS에 .NET 4.5을 등록 합니다.  
  %windir%\Microsoft.NET\Framework64 \v4.0.30319\aspnet \_ regiis-i  
  [ASP.NET IIS 등록 도구 (Aspnet \_regiis.exe)를](https://msdn.microsoft.com/library/k6h9cz8h.aspx) 참조 하세요.
- [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) 큐 제한을 기본값 1000에서 5000으로 늘려야 할 수 있습니다. 설정이 너무 낮으면 HTTP 503 상태를 포함 하는 [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) 거부 요청이 표시 될 수 있습니다. HTTP.sys 큐 제한을 변경 하려면 다음을 수행 합니다.

    - IIS 관리자를 열고 응용 프로그램 풀 창으로 이동 합니다.
    - 대상 응용 프로그램 풀을 마우스 오른쪽 단추로 클릭 하 고 **고급 설정**을 선택 합니다.  
        ![고급](using-asynchronous-methods-in-aspnet-45/_static/image4.png)
    - **고급 설정** 대화 상자에서 *큐 길이* 를 1000에서 5000로 변경 합니다.  
        ![큐 길이](using-asynchronous-methods-in-aspnet-45/_static/image5.png)  
  
  위의 이미지에서 응용 프로그램 풀이 .NET 4.5을 사용 하 고 있더라도 .NET framework는 v 4.0으로 표시 됩니다. 이러한 불일치를 이해 하려면 다음을 참조 하십시오.

- [.Net 버전 관리 및 다중 대상 지정-.net 4.5은 .NET 4.0로의 전체 업그레이드입니다.](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
- [2.0이 아닌 ASP.NET 3.5를 사용 하도록 IIS 응용 프로그램 또는 AppPool을 설정 하는 방법](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
- [.NET Framework 버전 및 종속성](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)

- 응용 프로그램에서 웹 서비스 또는 System.NET를 사용 하 여 HTTP를 통해 백 엔드와 통신 하는 경우 [Connectionmanagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) 요소를 늘려야 할 수 있습니다. ASP.NET 응용 프로그램의 경우 자동 구성 기능으로 Cpu 수의 12 배까지 제한 됩니다. 즉, 사중 프로세서에서 \* IP 끝점에 대 한 최대 12 4 = 48 동시 연결을 사용할 수 있습니다. 이는 자동 [구성에 연결](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)되어 있기 때문에 ASP.NET 응용 프로그램을 늘리는 가장 쉬운 방법은 `maxconnection` global.asax 파일의 from 메서드에서 프로그래밍 방식으로를 설정 하는 것 [입니다.](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) `Application_Start` *global.asax* 예제는 샘플 다운로드를 참조 하세요.
- .NET 4.5에서 [MaxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) 에 대 한 5000의 기본값은 적절 해야 합니다.

## <a name="contributors"></a>참가자

- [Levi Broderick](http://stackoverflow.com/users/59641/levi)
- [Tom Dykstra](http://www.bing.com/search?q=site%3Aasp.net+%22Tom+Dykstra%22+-forums.asp.net&amp;qs=n&amp;form=QBRE&amp;pq=site%3Aasp.net+%22tom+dykstra%22+-forums.asp.net&amp;sc=8-42&amp;sp=-1&amp;sk=)
- [Brad Wilson](http://bradwilson.typepad.com/)
- [HongMei Ge](https://blogs.msdn.com/b/hongmeig/)
