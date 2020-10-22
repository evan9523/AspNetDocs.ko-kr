---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: 웹 개발 모범 사례 (Azure를 사용 하 여 클라우드 앱 Real-World 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345510"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>웹 개발 모범 사례 (Azure를 사용 하 여 클라우드 앱 Real-World 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

처음 세 가지 패턴은 agile 개발 프로세스를 설정 하는 것입니다. 나머지는 아키텍처 및 코드에 대 한 것입니다. 이 항목은 웹 개발 모범 사례 모음입니다.

- 스마트 부하 분산 장치 뒤에 있는 [상태 비저장 웹 서버](#stateless) .
- [세션 상태를 방지](#sessionstate) 합니다 .이 문제를 방지 하려면 데이터베이스 대신 분산 캐시를 사용 합니다.
- [CDN을 사용](#cdn) 하 여 정적 파일 자산 (이미지, 스크립트)을에 지 캐시 합니다.
- 호출을 차단 하지 않으려면 [.net 4.5의 비동기 지원을 사용](#async) 합니다.

이러한 방법은 클라우드 앱 뿐만 아니라 모든 웹 개발에 유효 하지만 클라우드 앱에서 특히 중요 합니다. 클라우드 환경에서 제공 하는 매우 유연한 크기 조정을 최적으로 사용 하는 데 도움이 되는 함께 작동 합니다. 이러한 방법을 따르지 않는 경우 응용 프로그램 크기를 조정 하려고 할 때 제한이 발생 합니다.

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>스마트 부하 분산 장치 뒤에 있는 상태 비저장 웹 계층

*상태 비저장 웹 계층* 은 웹 서버 메모리 나 파일 시스템에 응용 프로그램 데이터를 저장 하지 않음을 의미 합니다. 웹 계층 상태 비저장을 유지 하면 더 나은 고객 환경을 제공 하 고 비용을 절감할 수 있습니다.

- 웹 계층이 상태 비저장이 고 부하 분산 장치 뒤에 있는 경우 서버를 동적으로 추가 하거나 제거 하 여 응용 프로그램 트래픽의 변경 내용에 신속 하 게 대응할 수 있습니다. 실제로 사용 하는 동안에만 서버 리소스에 대 한 비용을 지불 하는 클라우드 환경에서는 수요 변화에 대응 하는 기능이 크게 단축 될 수 있습니다.
- 상태 비저장 웹 계층은 응용 프로그램을 확장 하는 것이 훨씬 더 간단 합니다. 이를 통해 크기 조정 요구에 더 빠르게 대응할 수 있으며 프로세스에서 개발 및 테스트에 드는 비용을 줄일 수 있습니다.
- 온-프레미스 서버와 같은 클라우드 서버를 패치 및 재부팅 해야 하는 경우가 있습니다. 웹 계층이 상태 비저장 인 경우 서버가 일시적으로 중단 될 때 트래픽을 다시 라우팅하는 것으로 인해 오류가 발생 하거나 예기치 않은 동작이 발생 하지 않습니다.

대부분의 실제 응용 프로그램은 웹 세션의 상태를 저장 해야 합니다. 여기서 기본 지점은 웹 서버에 저장 하지 않는 것입니다. 쿠키의 클라이언트 또는 캐시 공급자를 사용 하는 ASP.NET 세션 상태의 in-process 서버 쪽 등의 다른 방법으로 상태를 저장할 수 있습니다. 로컬 파일 시스템 대신 [Windows Azure Blob 저장소](unstructured-blob-storage.md) 에 파일을 저장할 수 있습니다.

웹 계층이 상태 비저장 인 경우 Microsoft Azure 웹 사이트에서 응용 프로그램의 크기를 조정 하는 것이 얼마나 쉬운지 보여 주는 예는 관리 포털에서 Windows Azure 웹 사이트에 대 한 **크기 조정** 탭을 참조 하세요.

![크기 조정 탭](web-development-best-practices/_static/image1.png)

웹 서버를 추가 하려는 경우 인스턴스 수 슬라이더를 오른쪽으로 끌어 놓기만 하면 됩니다. 5로 설정 하 고 **저장**을 클릭 한 다음, Windows Azure에서 웹 사이트의 트래픽을 처리 하는 5 개의 웹 서버가 있습니다.

![5 개 인스턴스](web-development-best-practices/_static/image2.png)

쉽게 인스턴스 수를 3으로 설정 하거나 다시 1로 설정 하는 것이 좋습니다. 크기를 다시 조정 하는 경우 Windows Azure는 시간을 기준으로 시간을 기준으로 요금이 청구 되므로 즉시 비용을 절약 하기 시작 합니다.

Microsoft Azure에서 CPU 사용량에 따라 웹 서버 수를 자동으로 늘리거나 줄이도록 지시할 수도 있습니다. 다음 예제에서 CPU 사용량이 60% 미만이 되 면 웹 서버 수가 최소 2로 줄어들고, CPU 사용량이 80%를 초과 하면 웹 서버 수가 최대 4 개까지 증가 하 게 됩니다.

![CPU 사용량에 따라 크기 조정](web-development-best-practices/_static/image3.png)

또는 근무 시간 동안만 사이트를 사용 하 고 있는 경우에는 어떻게 하나요? Microsoft Azure에서 주간에 여러 서버를 실행 하도록 지시 하 고 야간, 야간 및 주말의 단일 서버를 줄일 수 있습니다. 다음 일련의 스크린샷에서는 업무 시간 동안 오전 8 시부터 오후 5 시 사이에 한 서버를 실행 하도록 웹 사이트를 설정 하는 방법을 보여 줍니다.

![일정에 따라 크기 조정](web-development-best-practices/_static/image4.png)

![일정 시간 설정](web-development-best-practices/_static/image5.png)

![주간 일정](web-development-best-practices/_static/image6.png)

![Weeknight 일정](web-development-best-practices/_static/image7.png)

![주말 일정](web-development-best-practices/_static/image8.png)

물론이 모든 작업은 포털 뿐만 아니라 스크립트 에서도 수행할 수 있습니다.

응용 프로그램의 규모를 확장 하는 기능은 Windows Azure에서 거의 무제한 이므로, 웹 계층 상태 비저장을 유지 하 여 서버 Vm을 동적으로 추가 또는 제거 하는 장애를 방지 해야 합니다.

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>세션 상태 방지

종종 실제 클라우드 앱에서 사용자 세션에 대한 일종의 상태를 저장을 회피하는 데 실용적이지 않지만 일부 접근 방법은 다른 항목 보다 성능 및 확장성에 더 많은 영향을 줍니다. 상태를 저장해야 하는 경우 가장 좋은 해결법은 상태의 크기를 작게 유지하고 쿠키에 저장하는 것입니다. 가능 하지 않은 경우 다음으로 가장 좋은 해결 방법은 [분산 된 메모리 내 캐시](distributed-caching.md#sessionstate)에 대 한 공급자와 ASP.NET 세션 상태를 사용 하는 것입니다. 성능 및 확장성 측면에서 최악의 해결법은 데이터베이스 지원 세션 상태 제공자를 사용하는 것입니다.

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>CDN을 사용 하 여 정적 파일 자산 캐시

CDN은 Content Delivery Network의 머리글자어입니다. 이미지 및 스크립트 파일 등의 정적 파일 자산을 CDN 공급자에 게 제공 하면 공급자는 모든 사용자가 응용 프로그램에 액세스할 때마다 캐시 된 자산에 대해 상대적으로 빠른 응답 및 짧은 대기 시간을 얻을 수 있도록 전 세계의 데이터 센터에 이러한 파일을 캐시 합니다. 이렇게 하면 사이트의 전체 로드 시간이 단축 되 고 웹 서버에 대 한 부하가 줄어듭니다. CDNs는 지리적으로 광범위 하 게 분산 된 대상에 도달 하는 경우 특히 중요 합니다.

Microsoft Azure에는 CDN이 있으며, Windows Azure 또는 모든 웹 호스팅 환경에서 실행 되는 응용 프로그램에서 다른 CDNs를 사용할 수 있습니다.

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>호출을 차단 하지 않도록 .NET 4.5의 비동기 지원 사용

.NET 4.5는 비동기 작업을 훨씬 간단 하 게 처리 하기 위해 c # 및 VB 프로그래밍 언어를 개선 했습니다. 비동기 프로그래밍의 혜택은 여러 웹 서비스 호출을 동시에 시작 하려는 경우와 같은 병렬 처리 상황을 위한 것이 아닙니다. 또한 높은 부하 상태에서 웹 서버를 보다 효율적이 고 안정적으로 수행할 수 있습니다. 웹 서버에는 제한 된 수의 스레드만 사용할 수 있으며, 모든 스레드가 사용 중일 때 부하가 높은 상태에서 들어오는 요청은 스레드를 해제할 때까지 기다려야 합니다. 응용 프로그램 코드에서 데이터베이스 쿼리 및 웹 서비스 호출과 같은 작업을 비동기적으로 처리 하지 않는 경우 서버에서 i/o 응답을 기다리는 동안 많은 스레드를 불필요 하 게 연결 합니다. 이렇게 하면 부하가 높은 부하 상태에서 서버가 처리할 수 있는 트래픽 양이 제한 됩니다. 비동기 프로그래밍을 사용 하는 경우 데이터를 받을 때까지 웹 서비스나 데이터베이스에서 데이터를 반환 하도록 대기 하는 스레드가 새 요청을 처리 하기 위해 해제 됩니다. 사용량이 많은 웹 서버에서 수백 또는 수천 개의 요청을 즉시 처리할 수 있으며, 그렇지 않으면 스레드를 해제할 때까지 대기 하 게 됩니다.

앞서 살펴본 것 처럼 웹 사이트를 처리 하는 웹 서버의 수를 줄일 수 있습니다. 따라서 서버에서 더 많은 처리량을 달성할 수 있는 경우에는 대부분의 처리량이 필요 하지 않으며, 달리 지정 된 트래픽 볼륨에 대해 서버 수가 더 적기 때문에 비용을 절감할 수 있습니다.

.NET 4.5 비동기 프로그래밍 모델에 대 한 지원은 Web Forms, MVC 및 Web API 용 ASP.NET 4.5에 포함 되어 있습니다. Entity Framework 6에서 [Windows AZURE STORAGE API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)에 있습니다.

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4.5의 비동기 지원

ASP.NET 4.5에서는 비동기 프로그래밍에 대 한 지원이 언어 뿐만 아니라 MVC, Web Forms 및 Web API 프레임 워크에도 추가 되었습니다. 예를 들어 ASP.NET MVC controller 작업 메서드는 웹 요청에서 데이터를 수신 하 고이 데이터를 뷰에 전달한 다음 HTML을 만들어 브라우저로 보냅니다. 작업 메서드는 웹 페이지에 데이터를 표시 하거나 웹 페이지에 입력 된 데이터를 저장 하기 위해 데이터베이스 또는 웹 서비스에서 데이터를 가져와야 하는 경우가 많습니다. 이러한 시나리오에서는 작업 메서드를 비동기 방식으로 쉽게 만들 수 있습니다. *actionresult* 개체를 반환 하는 대신 *작업 &lt; &gt; actionresult* 를 반환 하 고 메서드를 *async* 키워드로 표시 합니다. 메서드 내에서 코드 줄이 대기 시간을 포함 하는 작업을 시작 하면 wait 키워드로 표시 됩니다.

데이터베이스 쿼리에 대 한 리포지토리 메서드를 호출 하는 간단한 동작 메서드는 다음과 같습니다.

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

다음은 데이터베이스 호출을 비동기적으로 처리 하는 방법과 동일 합니다.

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

내부적으로 컴파일러는 적절 한 비동기 코드를 생성 합니다. 응용 프로그램에서를 호출 하면 `FindTaskByIdAsync` ASP.NET가 `FindTask` 요청을 만든 다음 작업자 스레드를 해제 하 고 다른 요청을 처리할 수 있도록 합니다. `FindTask`요청이 완료 되 면 해당 호출 후에 오는 코드를 계속 처리 하기 위해 스레드가 다시 시작 됩니다. 요청이 시작 될 때와 데이터가 반환 될 때 사이에 중간 중에는 `FindTask` 응답을 대기 하는 데 연결 되는 유용한 작업을 수행할 수 있는 스레드가 있습니다.

비동기 코드에는 약간의 오버 헤드가 있지만 부하가 낮은 상태에서는 오버 헤드가 거의 발생 하지 않지만, 부하가 높은 상태에서는 사용 가능한 스레드를 대기 중인 요청을 처리할 수 있습니다.

ASP.NET 1.1 이후로 이러한 종류의 비동기 프로그래밍을 수행 하는 것이 가능 하지만,이를 작성 하 고, 오류가 발생 하기 쉬우며, 디버깅 하기 어렵습니다. ASP.NET 4.5에서이에 대 한 코딩을 간소화 했으므로 더 이상 그렇게 하지 않아도 됩니다.

### <a name="async-support-in-entity-framework-6"></a>Entity Framework 6의 비동기 지원

4.5의 비동기 지원의 일부로 웹 서비스 호출, 소켓 및 파일 시스템 i/o에 대 한 비동기 지원을 제공 했지만, 웹 응용 프로그램의 가장 일반적인 패턴은 데이터베이스를 적중 하는 것이 고 데이터 라이브러리는 async를 지원 하지 않습니다. 이제 Entity Framework 6은 데이터베이스 액세스에 대 한 비동기 지원을 추가 합니다.

Entity Framework 6에서는 쿼리 또는 명령을 데이터베이스에 전송 하는 모든 메서드에 비동기 버전이 있습니다. 다음 예제에서는 *Find* 메서드의 비동기 버전을 보여 줍니다.

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

이 비동기 지원은 삽입, 삭제, 업데이트 및 간단한 찾기 뿐만 아니라 LINQ 쿼리에서도 작동 합니다.

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

`Async` `ToList` 이 코드에서는 쿼리가 데이터베이스로 전송 되도록 하는 메서드 이기 때문에 메서드의 버전이 있습니다. `Where`및 `OrderByDescending` 메서드는 쿼리를 구성 하는 반면, `ToListAsync` 메서드는 쿼리를 실행 하 고 응답을 `result` 변수에 저장 합니다.

## <a name="summary"></a>요약

웹 프로그래밍 프레임 워크 및 클라우드 환경에서 여기에 설명 된 웹 개발 모범 사례를 구현할 수 있지만 ASP.NET 및 Windows Azure의 도구를 사용 하면 쉽게 만들 수 있습니다. 이러한 패턴을 따르는 경우 웹 계층을 쉽게 확장할 수 있으며 각 서버에서 더 많은 트래픽을 처리할 수 있으므로 비용을 최소화할 수 있습니다.

[다음 장에서](single-sign-on.md) 는 클라우드에서 Single Sign-On 시나리오를 사용 하는 방법을 살펴봅니다.

## <a name="resources"></a>리소스

자세한 내용은 다음 리소스를 참조 하세요.

상태 비저장 웹 서버:

- [Microsoft 패턴 및 사례-자동](https://msdn.microsoft.com/library/dn589774.aspx)크기 조정 지침
- [Microsoft Azure 웹 사이트에서 ARR의 인스턴스 선호도를 사용 하지 않도록 설정](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)합니다. Windows Azure 웹 사이트의 세션 선호도에 대해 설명 하는 Rez 용 Ari의 블로그 게시물입니다.

CDN

- [안전 하지 않음: 확장 가능 하 고 복원 가능한 Cloud Services 빌드](https://channel9.msdn.com/Series/FailSafe) 9 개 부분으로 구성 된 비디오 시리즈, Marc Mercuri 및 Mark Simm. 1:34:00에서 시작 하는 에피소드 3의 CDN 토론을 참조 하세요.
- [Microsoft 패턴 및 구현 정적 콘텐츠 호스팅 패턴](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN 검토](http://www.cdnreviews.com/). 많은 CDNs의 개요.

비동기 프로그래밍:

- [ASP.NET MVC 4에서 비동기 메서드 사용](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md) Rick Anderson의 자습서.
- [Async 및 wait를 사용한 비동기 프로그래밍 (c # 및 Visual Basic)](https://msdn.microsoft.com/library/vstudio/hh191443.aspx) MSDN 백서는 비동기 프로그래밍에 대 한 근거를 설명 하 고, ASP.NET 4.5에서 작동 하는 방법 및이를 구현 하는 코드를 작성 하는 방법을 설명 합니다.
- [비동기 쿼리 및 저장 Entity Framework](https://msdn.microsoft.com/data/jj819165)
- [Async를 사용 하 여 ASP.NET 웹 응용 프로그램을 빌드하는 방법](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7)입니다. 행 별 비디오 프레젠테이션. 높은 부하 상태에서 비동기 프로그래밍으로 웹 서버 처리량을 크게 향상 시킬 수 있는 방법을 보여 주는 그래픽 데모를 제공 합니다.
- [안전 하지 않음: 확장 가능 하 고 복원 가능한 Cloud Services 빌드](https://channel9.msdn.com/Series/FailSafe) 9 개 부분으로 구성 된 비디오 시리즈, Marc Mercuri 및 Mark Simm. 확장성에 대 한 비동기 프로그래밍의 영향에 대 한 논의는 에피소드 4 및 에피소드 8을 참조 하세요.
- [ASP.NET 4.5에는 비동기 메서드를 사용 하 고 중요 한 알려진 문제를 사용 하는 마법입니다](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx). ASP.NET Web Forms 응용 프로그램에서 기본적으로 async를 사용 하는 Scott Hanselman의 블로그 게시물입니다.

웹 개발 모범 사례에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Fix It 샘플 응용 프로그램-모범 사례를](the-fix-it-sample-application.md#bestpractices)소개 합니다. 이 설명서의 부록에서는 Fix It 응용 프로그램에서 구현 된 여러 가지 모범 사례를 보여 줍니다.
- [웹 개발자 검사 목록](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [이전](continuous-integration-and-continuous-delivery.md)
> [다음](single-sign-on.md)
