---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: 웹 개발 모범 사례(Azure를 사용한 실제 클라우드 앱 빌드) | 마이크로 소프트 문서
author: MikeWasson
description: Azure 전자책을 사용한 실제 클라우드 앱 구축은 Scott Guthrie가 개발한 프레젠테이션을 기반으로 합니다. 그것은 그가 할 수있는 13 패턴과 관행을 설명합니다 ...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675642"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>웹 개발 모범 사례(Azure를 사용한 실제 클라우드 앱 빌드)

[마이크 와슨,](https://github.com/MikeWasson) [릭 앤더슨,](https://twitter.com/RickAndMSFT) [톰 다이크스트라](https://github.com/tdykstra)

[프로젝트 수정](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure 전자책을 **사용한 실제 클라우드 앱 구축은** Scott Guthrie가 개발한 프레젠테이션을 기반으로 합니다. 클라우드용 웹 앱을 성공적으로 개발하는 데 도움이 되는 13가지 패턴과 사례에 대해 설명합니다. 전자책에 대한 자세한 내용은 [첫 번째 장을](introduction.md)참조하십시오.

처음 세 가지 패턴은 민첩한 개발 프로세스를 설정하는 것입니다. 나머지는 아키텍처와 코드에 관한 것입니다. 다음은 웹 개발 모범 사례모음입니다.

- 스마트 로드 밸러블러 뒤에 [있는 상태 비관리 웹 서버.](#stateless)
- [세션 상태를 피하십시오(또는](#sessionstate) 이를 피할 수 없는 경우 데이터베이스가 아닌 분산 캐시를 사용하십시오).
- [CDN을 사용하여](#cdn) 정적 파일 자산(이미지, 스크립트)을 에지 캐시합니다.
- [.NET 4.5의 비동기 지원을 사용하여](#async) 통화 차단을 방지합니다.

이러한 방법은 클라우드 앱뿐만 아니라 모든 웹 개발에 유효하지만 클라우드 앱에 특히 중요합니다. 클라우드 환경에서 제공하는 매우 유연한 확장을 최적 으로 활용할 수 있도록 함께 작동합니다. 이러한 방법을 따르지 않으면 응용 프로그램의 크기를 조정하려고 할 때 제한이 적용됩니다.

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>스마트 로드 밸러블러 뒤에 있는 상태 비수기 웹 계층

*상태 비저장 웹 계층은* 웹 서버 메모리 또는 파일 시스템에 응용 프로그램 데이터를 저장하지 않는다는 것을 의미합니다. 웹 계층을 상태 비저장 상태로 유지하면 더 나은 고객 경험을 제공하고 비용을 절감할 수 있습니다.

- 웹 계층이 상태 비활성 상태이고 로드 밸러터 뒤에 있는 경우 서버를 동적으로 추가하거나 제거하여 응용 프로그램 트래픽의 변경 사항에 신속하게 대응할 수 있습니다. 실제로 서버 리소스를 사용하는 한 서버 리소스에 대해서만 비용을 지불하는 클라우드 환경에서는 수요 변화에 대응하는 기능이 막대한 절감 효과를 낼 수 있습니다.
- 상태 비수기 웹 계층은 응용 프로그램을 확장하는 것이 훨씬 간단합니다. 이를 통해 확장 요구 사항에 보다 신속하게 대응하고 프로세스의 개발 및 테스트에 더 적은 비용을 지출할 수 있습니다.
- 온-프레미스 서버와 같은 클라우드 서버는 가끔 패치를 적용하고 재부팅해야 합니다. 웹 계층이 상태 비저장인 경우 서버가 일시적으로 다운될 때 트래픽을 다시 라우팅해도 오류나 예기치 않은 동작이 발생하지 않습니다.

대부분의 실제 응용 프로그램은 웹 세션에 대한 상태를 저장해야 합니다. 여기서 중요한 점은 웹 서버에 저장하지 않는 것입니다. 캐시 공급자를 사용하여 클라이언트에서 쿠키 또는 프로세스 서버 측의 상태와 같은 다른 방법으로 상태를 저장할 수 ASP.NET 세션 상태입니다. 로컬 파일 시스템 대신 [Windows Azure Blob 저장소에](unstructured-blob-storage.md) 파일을 저장할 수 있습니다.

웹 계층이 상태 비저장인 경우 Windows Azure 웹 사이트에서 응용 프로그램을 확장하는 것이 얼마나 쉬운지 에 대한 예로 관리 포털에서 Windows Azure 웹 사이트의 **확장** 탭을 참조하십시오.

![크기 조정 탭](web-development-best-practices/_static/image1.png)

웹 서버를 추가하려는 경우 인스턴스 개수 슬라이더를 오른쪽으로 드래그하면 됩니다. 5로 설정하고 **저장을**클릭하고 몇 초 내에 Windows Azure에서 웹 사이트의 트래픽을 처리하는 5개의 웹 서버가 있습니다.

![5개의 인스턴스](web-development-best-practices/_static/image2.png)

인스턴스 카운트다운을 3으로 쉽게 설정하거나 다시 1로 되돌릴 수 있습니다. 규모를 축소하면 Windows Azure가 시간단위가 아닌 분 단위로 요금을 청구하기 때문에 즉시 비용을 절감하기 시작합니다.

또한 Windows Azure에 CPU 사용량에 따라 웹 서버 수를 자동으로 늘리거나 줄이도록 지시할 수도 있습니다. 다음 예제에서는 CPU 사용량이 60% 미만이면 웹 서버 수가 최소 2개로 줄어들고 CPU 사용량이 80%를 초과하면 웹 서버 수가 최대 4개까지 증가합니다.

![CPU 사용량에 따라 확장](web-development-best-practices/_static/image3.png)

또는 귀하의 사이트가 근무 시간 동안에만 바쁘다는 것을 알고 있다면 어떨까요? Windows Azure는 낮 동안 여러 서버를 실행하고 단일 서버 저녁, 야간 및 주말로 줄이도록 지시할 수 있습니다. 다음 화면 촬영 시리즈는 오전 8시부터 오후 5시까지 근무 시간 동안 한 서버와 4개의 서버를 운영하도록 웹 사이트를 설정하는 방법을 보여 주며, 이 방법은 다음과 같은 것입니다.

![일정에 따라 배율 조정](web-development-best-practices/_static/image4.png)

![일정 시간 설정](web-development-best-practices/_static/image5.png)

![주간 일정](web-development-best-practices/_static/image6.png)

![평일 일정](web-development-best-practices/_static/image7.png)

![주말 일정](web-development-best-practices/_static/image8.png)

물론 이 모든 작업은 포털뿐만 아니라 스크립트에서도 가능합니다.

웹 계층을 상태 비저장 상태로 유지하여 서버 VM을 동적으로 추가하거나 제거하는 데 방해가 되지 않는 한 Windows Azure에서는 응용 프로그램의 확장 기능은 거의 무제한입니다.

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>세션 상태 방지

종종 실제 클라우드 앱에서 사용자 세션에 대한 일종의 상태를 저장을 회피하는 데 실용적이지 않지만 일부 접근 방법은 다른 항목 보다 성능 및 확장성에 더 많은 영향을 줍니다. 상태를 저장해야 하는 경우 가장 좋은 해결법은 상태의 크기를 작게 유지하고 쿠키에 저장하는 것입니다. 이것이 가능하지 않은 경우, 다음 가장 좋은 해결책은 분산 [된 메모리 내 캐시에](distributed-caching.md#sessionstate)대한 공급자와 ASP.NET 세션 상태를 사용하는 것입니다. 성능 및 확장성 측면에서 최악의 해결법은 데이터베이스 지원 세션 상태 제공자를 사용하는 것입니다.

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>CDN을 사용하여 정적 파일 자산 캐시

CDN은 콘텐츠 전송 네트워크의 약자입니다. 이미지 및 스크립트 파일과 같은 정적 파일 에셋을 CDN 공급자에게 제공하고 공급자는 전 세계 데이터 센터에 이러한 파일을 캐시하므로 사용자가 응용 프로그램에 액세스할 때마다 캐시된 자산에 대해 비교적 빠른 응답과 낮은 대기 시간을 얻을 수 있습니다. 이렇게 하면 사이트의 전체 로드 시간이 빨라지고 웹 서버의 로드가 줄어듭니다. 지리적으로 널리 분산되어 있는 잠재고객에게 도달하는 경우 CDN은 특히 중요합니다.

Windows Azure에는 CDN이 있으며 Windows Azure 또는 웹 호스팅 환경에서 실행되는 응용 프로그램에서 다른 CDN을 사용할 수 있습니다.

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>.NET 4.5의 비동기 지원을 사용하여 통화 차단 방지

.NET 4.5는 작업을 비동기적으로 처리하는 것이 훨씬 간단하도록 C# 및 VB 프로그래밍 언어를 향상시켰습니다. 비동기 프로그래밍의 이점은 여러 웹 서비스 호출을 동시에 시작하려는 경우와 같은 병렬 처리 상황에서만 이점이 아닙니다. 또한 웹 서버가 높은 부하 조건에서 보다 효율적이고 신뢰할 수 있는 성능을 발휘할 수 있습니다. 웹 서버는 사용 가능한 스레드 수가 제한되어 있으며 로드 조건이 높은 조건에서 모든 스레드가 사용 중인 경우 들어오는 요청은 스레드가 해제될 때까지 기다려야 합니다. 응용 프로그램 코드가 데이터베이스 쿼리 및 웹 서비스 호출과 같은 작업을 비동기적으로 처리하지 않는 경우 서버가 I/O 응답을 기다리는 동안 많은 스레드가 불필요하게 묶여 있습니다. 이렇게 하면 부하가 많은 조건에서 서버가 처리할 수 있는 트래픽의 양이 제한됩니다. 비동기 프로그래밍을 사용하면 웹 서비스 또는 데이터베이스가 데이터를 반환하기를 기다리는 스레드가 수신된 데이터가 수신될 때까지 새 요청을 서비스하기 위해 해제됩니다. 바쁜 웹 서버에서는 수백 또는 수천 개의 요청을 즉시 처리할 수 있으며, 그렇지 않으면 스레드가 해제되기를 기다리고 있습니다.

앞에서 보았듯이 웹 사이트를 처리하는 웹 서버수를 늘리는 것만큼 쉽게 줄일 수 있습니다. 따라서 서버가 더 큰 처리량을 달성할 수 있는 경우 처리량이 많지 않으며 지정된 트래픽 볼륨에 대해 서버수가 더 적기 때문에 비용을 절감할 수 있습니다.

.NET 4.5 비동기 프로그래밍 모델에 대한 지원은 웹 폼, MVC 및 웹 API에 대한 ASP.NET 4.5에 포함되어 있습니다. 엔터티 프레임워크 6 및 [Windows Azure 저장소 API에서](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx).

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4.5의 비동기 지원

ASP.NET 4.5에서는 언어뿐만 아니라 MVC, 웹 양식 및 웹 API 프레임워크에도 비동기 프로그래밍에 대한 지원이 추가되었습니다. 예를 들어 ASP.NET MVC 컨트롤러 작업 메서드는 웹 요청에서 데이터를 수신 하 고 브라우저에 보낼 HTML을 만드는 뷰에 데이터를 전달 합니다. 작업 메서드는 웹 페이지에 표시하거나 웹 페이지에 입력된 데이터를 저장하기 위해 데이터베이스 또는 웹 서비스에서 데이터를 얻어야 하는 경우가 종종 있습니다. 이러한 시나리오에서는 *ActionResult* 개체를 반환 하는 대신 *작업&lt;ActionResult를&gt; * 반환 하 고 *비동기* 키워드로 메서드를 표시 하는 작업 메서드를 비동기로 쉽게 만들 수 있습니다. 메서드 내에서 코드 줄이 대기 시간이 포함된 작업을 시작하면 await 키워드로 표시합니다.

다음은 데이터베이스 쿼리에 대한 리포지토리 메서드를 호출하는 간단한 작업 메서드입니다.

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

다음은 데이터베이스 호출을 비동기적으로 처리하는 동일한 메서드입니다.

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

표지 에서 컴파일러는 적절한 비동기 코드를 생성합니다. 응용 프로그램이 에 대해 `FindTaskByIdAsync`호출할 `FindTask` 때 ASP.NET 요청을 한 다음 작업자 스레드를 해제하고 다른 요청을 처리할 수 있도록 합니다. 요청이 `FindTask` 완료되면 스레드가 다시 시작되어 해당 호출 이후에 제공되는 코드를 계속 처리합니다. `FindTask` 요청이 시작되는 시점과 데이터가 반환되는 동안 응답을 기다리는 데 도움이 되는 유용한 작업을 수행할 수 있는 스레드가 있습니다.

비동기 코드에는 약간의 오버헤드가 있지만 부하가 낮은 조건에서는 오버헤드가 무시할 수 있지만, 부하가 많은 조건에서는 사용 가능한 스레드를 기다리는 요청을 처리할 수 있습니다.

ASP.NET 1.1부터 이러한 종류의 비동기 프로그래밍을 수행할 수 있었지만 쓰기가 어렵고 오류가 발생하기 쉽고 디버깅하기가 어려웠습니다. 이제 ASP.NET 4.5에서 코딩을 단순화되었으므로 더 이상 코딩을 하지 않을 이유가 없습니다.

### <a name="async-support-in-entity-framework-6"></a>엔터티 프레임워크 6의 비동기 지원

4.5의 비동기 지원의 일환으로 웹 서비스 호출, 소켓 및 파일 시스템 I/O에 대한 비동기 지원을 제공했지만 웹 응용 프로그램의 가장 일반적인 패턴은 데이터베이스를 공격하는 것이고 데이터 라이브러리는 비동기를 지원하지 않았습니다. 이제 엔터티 프레임워크 6은 데이터베이스 액세스에 대한 비동기 지원을 추가합니다.

Entity Framework 6에서 쿼리 또는 명령을 데이터베이스로 전송하는 모든 메서드에는 비동기 버전이 있습니다. 이 예제에서는 *Find* 메서드의 비동기 버전을 보여 주실 수 있습니다.

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

이 비동기 지원은 삽입, 삭제, 업데이트 및 간단한 검색뿐만 아니라 LINQ 쿼리에서도 작동합니다.

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

이 코드에는 `Async` 쿼리를 `ToList` 데이터베이스로 전송하는 메서드이기 때문에 메서드 버전이 있습니다. `Where` 및 `OrderByDescending` 메서드는 쿼리만 구성하고 `ToListAsync` 메서드는 쿼리를 실행하고 `result` 변수에 응답을 저장합니다.

## <a name="summary"></a>요약

모든 웹 프로그래밍 프레임워크 및 클라우드 환경에서 여기에 설명된 웹 개발 모범 사례를 구현할 수 있지만 ASP.NET 및 Windows Azure에서 쉽게 사용할 수 있는 도구가 있습니다. 이러한 패턴을 따르는 경우 웹 계층을 쉽게 확장할 수 있으며 각 서버가 더 많은 트래픽을 처리할 수 있으므로 비용을 최소화할 수 있습니다.

[다음 장에서는](single-sign-on.md) 클라우드를 통해 단일 사인온 시나리오를 활성화하는 방법을 살펴봅니다.

## <a name="resources"></a>리소스

자세한 내용은 다음 리소스를 참조하십시오.

상태 비수기 웹 서버:

- [마이크로 소프트 패턴 및 관행 - 자동 크기 조정 지침](https://msdn.microsoft.com/library/dn589774.aspx).
- [Windows Azure 웹 사이트에서 ARR의 인스턴스 선호도 를 사용하지 않도록 설정합니다.](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/) Erez Benari의 블로그 게시물에서 Windows Azure 웹 사이트의 세션 선호도에 대해 설명합니다.

Cdn:

- [페일세이프: 확장 가능하고 탄력적인 클라우드 서비스 구축.](https://channel9.msdn.com/Series/FailSafe) 울리히 호만, 마크 머큐리, 마크 심스의 9부작 비디오 시리즈. 1:34:00부터 시작되는 에피소드 3의 CDN 토론을 참조하십시오.
- [Microsoft 패턴 및 사례 정적 콘텐츠 호스팅 패턴](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN 리뷰](http://www.cdnreviews.com/). 많은 CDN의 개요입니다.

비동기 프로그래밍:

- [ASP.NET MVC 4에서 비동기 메서드사용](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md). 릭 앤더슨에 의해 튜토리얼.
- [비동기 프로그래밍 비동기 및 Await (C# 및 시각적 기본)](https://msdn.microsoft.com/library/vstudio/hh191443.aspx). 비동기 프로그래밍에 대한 근거, ASP.NET 4.5에서 작동하는 방법 및 이를 구현하기 위한 코드를 작성하는 방법을 설명하는 MSDN 백서입니다.
- [엔터티 프레임워크 비동기 쿼리 및 저장](https://msdn.microsoft.com/data/jj819165)
- [async를 사용하여 ASP.NET 웹 응용 프로그램을 빌드하는 방법](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7). 로완 밀러의 비디오 프리젠 테이션. 비동기 프로그래밍이 높은 부하 조건에서 웹 서버 처리량을 크게 증가시킬 수 있는 방법에 대한 그래픽 데모가 포함되어 있습니다.
- [페일세이프: 확장 가능하고 탄력적인 클라우드 서비스 구축.](https://channel9.msdn.com/Series/FailSafe) 울리히 호만, 마크 머큐리, 마크 심스의 9부작 비디오 시리즈. 비동기 프로그래밍이 확장성에 미치는 영향에 대한 토론은 에피소드 4 및 에피소드 8을 참조하십시오.
- [ASP.NET 4.5 플러스 중요한 gotcha에서 비동기 메서드를 사용하는 마법](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx). Scott Hanselman의 블로그 게시물은 주로 웹 양식 응용 프로그램에서 비동기를 사용하는 ASP.NET.

추가 웹 개발 모범 사례는 다음 리소스를 참조하십시오.

- [수정 샘플 응용 프로그램 - 모범 사례](the-fix-it-sample-application.md#bestpractices). 이 전자책의 부록에는 Fix It 응용 프로그램에서 구현된 여러 가지 모범 사례가 나열되어 있습니다.
- [웹 개발자 체크리스트](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [이전](continuous-integration-and-continuous-delivery.md)
> [다음](single-sign-on.md)
