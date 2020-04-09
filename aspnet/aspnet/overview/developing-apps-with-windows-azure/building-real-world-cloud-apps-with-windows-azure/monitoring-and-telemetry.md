---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 모니터링 및 원격 분석(Azure를 사용한 실제 클라우드 앱 빌드) | 마이크로 소프트 문서
author: MikeWasson
description: Azure 전자책을 사용한 실제 클라우드 앱 구축은 Scott Guthrie가 개발한 프레젠테이션을 기반으로 합니다. 그것은 그가 할 수있는 13 패턴과 관행을 설명합니다 ...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675672"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>모니터링 및 원격 분석(Azure를 사용한 실제 클라우드 앱 빌드)

[마이크 와슨,](https://github.com/MikeWasson) [릭 앤더슨,](https://twitter.com/RickAndMSFT) [톰 다이크스트라](https://github.com/tdykstra)

[프로젝트 수정](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure 전자책을 **사용한 실제 클라우드 앱 구축은** Scott Guthrie가 개발한 프레젠테이션을 기반으로 합니다. 클라우드용 웹 앱을 성공적으로 개발하는 데 도움이 되는 13가지 패턴과 사례에 대해 설명합니다. 전자책에 대한 자세한 내용은 [첫 번째 장을](introduction.md)참조하십시오.

많은 사람들이 고객이 응용 프로그램이 중단된 시기를 알리기 위해 고객에 의존합니다. 이는 클라우드에서 특히 모범 사례가 아닙니다. 빠른 알림을 보장할 수 없으며 알림을 받을 때 발생한 일에 대한 최소한의 데이터를 얻거나 오해의 소지가 있는 데이터를 얻을 수 있습니다. 좋은 원격 분석 및 로깅 시스템을 사용하면 앱에서 무슨 일이 일어나고 있는지 알 수 있으며 문제가 발생하면 즉시 알아내고 작업할 유용한 문제 해결 정보를 찾을 수 있습니다.

## <a name="buy-or-rent-a-telemetry-solution"></a>원격 분석 솔루션 구매 또는 대여

> [!NOTE]
> 이 문서는 [응용 프로그램 인사이트가](/azure/application-insights/app-insights-overview) 릴리스되기 전에 작성되었습니다. 응용 프로그램 인사이트는 Azure의 원격 분석 솔루션에 선호되는 방법입니다. 자세한 내용은 [ASP.NET 웹 사이트에 대한 응용 프로그램 인사이트 설정을](/azure/application-insights/app-insights-asp-net) 참조하십시오.

클라우드 환경의 장점은 승리를 위해 구매하거나 임대하는 것이 정말 쉽다는 것입니다. 원격 분석이 예입니다. 많은 노력없이 당신은 매우 비용 효율적으로, 정말 좋은 원격 분석 시스템을 얻을 수 있습니다. Azure와 통합되는 훌륭한 파트너가 많이 있으며, 그 중 일부는 프리 티어를 가지고 있으므로 기본 원격 분석을 아무 것도 얻을 수 없습니다. 다음은 Azure에서 현재 사용할 수 있는 몇 가지 사항입니다.

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft 시스템 센터에는](http://www.petri.co.il/microsoft-system-center-introduction.htm#) 모니터링 기능도 포함되어 있습니다.

새로운 유물 을 설정하여 원격 분석 시스템을 사용하는 것이 얼마나 쉬운지 보여 드리겠습니다.

Azure 관리 포털에서 서비스에 등록합니다. **새**를 클릭한 다음 **저장**을 클릭합니다. 추가 기능 대화 **상자 선택상자가** 나타납니다. 아래로 스크롤하여 **새 유물을**클릭합니다.

![추가 기능 선택](monitoring-and-telemetry/_static/image1.png)

오른쪽 화살표를 클릭하고 원하는 서비스 계층을 선택합니다. 이 데모에서는 프리 티어를 사용합니다.

![추가 기능 맞춤 설정](monitoring-and-telemetry/_static/image2.png)

오른쪽 화살표를 클릭하고 "구매"를 확인하고 새로운 유물이 포털에 추가 기능으로 표시됩니다.

![리뷰 구매](monitoring-and-telemetry/_static/image3.png)

![관리 포털의 새로운 유물 추가 기능](monitoring-and-telemetry/_static/image4.png)

**연결 정보를**클릭하고 라이센스 키를 복사합니다.

![연결 정보](monitoring-and-telemetry/_static/image5.png)

포털의 웹 **앱구성** 탭으로 이동하여 **성능 모니터링을** **추가 기능으로**설정하고 추가 기능 드롭다운 **선택** 목록을 **새 Relic으로**설정합니다. 그런 다음 **저장을**클릭합니다.

![구성 탭의 새 유물](monitoring-and-telemetry/_static/image6.png)

비주얼 스튜디오에서 앱에 새 유물 NuGet 패키지를 설치합니다.

![구성 탭의 개발자 분석](monitoring-and-telemetry/_static/image7.png)

Azure에 앱을 배포하고 사용을 시작합니다. 몇 가지 Fix It 작업을 만들어 새 유물이 모니터링할 수 있는 몇 가지 작업을 제공합니다.

그런 다음 포털의 **추가 기능** 탭에서 **새 유물** 페이지로 **돌아가서 관리를**클릭합니다. 포털은 인증을 위해 단일 사인온을 사용하여 새로운 유물 관리 포털로 전송되므로 자격 증명을 다시 입력할 필요가 없습니다. 개요 페이지에는 다양한 성능 통계가 표시됩니다. (이미지를 클릭하여 개요 페이지 전체 크기를 확인합니다.)

[![새로운 유물 모니터링 탭](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

다음은 볼 수 있는 몇 가지 통계입니다.

- 하루 중 다른 시간에 평균 응답 시간.

    ![응답 시간](monitoring-and-telemetry/_static/image10.png)
- 하루 중 다른 시간에 처리량 비율(분당 요청)

    ![처리량](monitoring-and-telemetry/_static/image11.png)
- 서버 CPU 시간은 다른 HTTP 요청을 처리하는 데 사용되었습니다.

    ![웹 트랜잭션 시간](monitoring-and-telemetry/_static/image12.png)
- 응용 프로그램 코드의 다른 부분에서 소비되는 CPU 시간:

    ![추적 세부 정보](monitoring-and-telemetry/_static/image13.png)
- 과거 성능 통계.

    ![역사적 성과](monitoring-and-telemetry/_static/image14.png)
- Blob 서비스와 같은 외부 서비스에 대한 호출 및 서비스가 얼마나 안정적이고 응답성이 있는지에 대한 통계입니다.

    ![외부 서비스](monitoring-and-telemetry/_static/image15.png)

    ![외부 서비스](monitoring-and-telemetry/_static/image16.png)

    ![외부 서비스](monitoring-and-telemetry/_static/image17.png)
- 전 세계 또는 미국 웹 앱 트래픽의 출처에 대한 정보입니다.

    ![Geography](monitoring-and-telemetry/_static/image18.png)

보고서 및 이벤트를 설정할 수도 있습니다. 예를 들어 오류가 표시되기 시작할 때마다 지원 담당자에게 문제를 알리는 이메일을 보낼 수 있습니다.

![보고서](monitoring-and-telemetry/_static/image19.png)

새 유물은 원격 분석 시스템의 한 예일 뿐입니다. 다른 서비스에서도 이 모든 것을 얻을 수 있습니다. 클라우드의 장점은 코드를 작성할 필요 없이 최소한의 비용없이 응용 프로그램이 사용되는 방식과 고객이 실제로 경험하는 것에 대한 더 많은 정보를 갑자기 얻을 수 있다는 것입니다.

<a id="log"></a>
## <a name="log-for-insight"></a>인사이트를 위한 로그

원격 분석 패키지는 좋은 첫 번째 단계이지만 여전히 사용자 고유의 코드를 계측해야 합니다. 원격 분석 서비스는 문제가 있을 때 알려주고 고객이 겪고 있는 일을 알려주지만 코드에서 무슨 일이 일어나고 있는지에 대한 많은 통찰력을 제공하지 못할 수도 있습니다.

앱이 수행하는 작업을 확인하기 위해 프로덕션 서버로 원격으로 이동하지 않아도 됩니다. 서버가 하나 있을 때 실용적일 수 있지만 수백 개의 서버로 확장하여 원격으로 전환해야 하는 서버를 모르는 경우 는 어떨까요? 로깅은 문제를 분석하고 디버깅하기 위해 프로덕션 서버로 원격할 필요가 없는 충분한 정보를 제공해야 합니다. 로그를 통해서만 문제를 격리할 수 있도록 충분한 정보를 로깅해야 합니다.

### <a name="log-in-production"></a>프로덕션 에 로그인

많은 사람들이 문제가 있고 디버깅을 원할 때만 프로덕션에서 추적을 켜고 있습니다. 이렇게 하면 문제를 알고 있는 시간과 문제를 인식하는 데 유용한 문제 해결 정보를 얻는 시간 사이에 상당한 지연이 발생할 수 있습니다. 그리고 당신이 얻을 정보는 간헐적 인 오류에 도움이되지 않을 수 있습니다.

스토리지가 저렴한 클라우드 환경에서 권장하는 것은 항상 프로덕션 환경에서 로그온을 유지한다는 것입니다. 이렇게 하면 오류가 이미 기록되어 있고 시간이 지남에 따라 발생하거나 다른 시간에 정기적으로 발생하는 문제를 분석하는 데 도움이 되는 기록 데이터가 있습니다. 제거 프로세스를 자동화하여 이전 로그를 삭제할 수 있지만 로그를 유지하는 것보다 이러한 프로세스를 설정하는 것이 더 비쌀 수 있습니다.

로깅의 추가 비용은 문제가 발생할 때 이미 사용할 수 있는 모든 정보를 저장하여 절약할 수 있는 문제 해결 시간과 비용에 비해 간단합니다. 그런 다음 누군가가 어젯밤 8:00 경에 임의의 오류가 있다고 말하지만 오류를 기억하지 못하면 문제가 무엇인지 쉽게 알 수 있습니다.

한 달에 4기가바이트 미만의 로그를 보관할 수 있으며 성능 병목 현상을 방지하기 위해 로깅 라이브러리가 비동기인지 확인하려면 로깅의 성능 영향이 간단합니다.

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>작업이 필요한 로그에서 알리는 로그 차별화

로그는 (당신이 뭔가를 알고 싶어요) 또는 ACT (나는 당신이 뭔가를 하고 싶어)를 알리기위한 것입니다. 사람이나 자동화된 프로세스가 진정으로 조치를 취해야 하는 문제에 대해서만 ACT 로그를 작성해야 합니다. 너무 많은 ACT 로그가 노이즈를 생성하므로 정품 문제를 찾기 위해 모든 것을 선별하는 데 너무 많은 작업이 필요합니다. ACT 로그가 지원 직원에게 이메일을 보내는 것과 같은 일부 작업을 자동으로 트리거하는 경우 단일 문제로 인해 수천 개의 작업이 트리거되지 않도록 합니다.

.NET System.Diagnostics 추적에서 로그에 오류, 경고, 정보 및 디버그/세부 정보 수준을 할당할 수 있습니다. ACT 로그에 대한 오류 수준을 예약하고 INFORM 로그에 대해 하위 수준을 사용하여 ACT를 INFORM 로그와 구분할 수 있습니다.

![로깅 수준](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>런타임에 로깅 수준 구성

프로덕션 환경에서 항상 로깅을 하는 것이 좋습니다. 예를 들어 추적 `System.Diagnostics` 기능을 사용하는 경우 오류, 경고, 정보 및 디버그/세부 정보를 만들 수 있습니다. 프로덕션 환경에서 오류, 경고 및 정보 로그를 항상 기록하는 것이 좋습니다.

Azure 앱 서비스의 웹 앱에는 파일 `System.Diagnostics` 시스템, 테이블 저장소 또는 Blob 저장소에 로그를 작성하기 위한 기본 제공 지원이 있습니다. 각 저장소 대상에 대해 서로 다른 로깅 수준을 선택할 수 있으며 응용 프로그램을 다시 시작하지 않고도 즉시 로깅 수준을 변경할 수 있습니다. BLOB 스토리지 지원을 사용하면 HDInsight가 Blob 스토리지에서 직접 작업하는 방법을 알고 있기 때문에 응용 프로그램 로그에서 [HDInsight](https://docs.microsoft.com/azure/hdinsight/) 분석 작업을 더 쉽게 실행할 수 있습니다.

### <a name="log-exceptions"></a>예외 기록

그냥 예외를 두지 *마십시오. 로깅 코드에서 ToString()을* 사용합니다. 컨텍스트 정보를 남깁니다. SQL 오류의 경우 SQL 오류 번호가 남습니다. 모든 예외에 대해 컨텍스트 정보, 예외 자체 및 내부 예외를 포함하여 문제 해결에 필요한 모든 것을 제공하고 있는지 확인합니다. 예를 들어 컨텍스트 정보에는 서버 이름, 트랜잭션 식별자 및 사용자 이름(암호 또는 비밀은 포함되지 않음)이 포함될 수 있습니다.

각 개발자가 예외 로깅을 사용하여 올바른 작업을 수행하는 경우 일부 개발자는 그렇지 않습니다. 매번 올바른 방식으로 수행되도록 하려면 예외 처리 처리를 로거 인터페이스에 바로 빌드합니다.

### <a name="log-calls-to-services"></a>서비스에 대한 통화 로그

앱이 서비스에 호출할 때마다 데이터베이스또는 REST API 또는 외부 서비스에 대한 로그를 작성하는 것이 좋습니다. 성공 또는 실패의 표시뿐만 아니라 각 요청이 걸린 시간도 로그에 포함합니다. 클라우드 환경에서는 전체 가동 중단이 아닌 속도 저하와 관련된 문제가 종종 발생합니다. 일반적으로 10밀리초가 걸리는 것이 갑자기 1초 를 복용하기 시작할 수 있습니다. 누군가가 앱이 느리다고 말하면 New Relic 또는 어떤 원격 분석 서비스를 보고 자신의 경험을 검증할 수 있어야 하며, 그 다음 에는 느린 이유에 대한 세부 정보를 자세히 살펴볼 수 있는 자신의 로그가 될 수 있기를 원합니다.

### <a name="use-an-ilogger-interface"></a>ILogger 인터페이스 사용

프로덕션 응용 프로그램을 만들 때 수행하는 것이 좋습니다. *ILogger* 이렇게 하면 나중에 로깅 구현을 쉽게 변경할 수 있으며 모든 코드를 통해 로깅을 수행할 필요가 없습니다. Fix It 앱 `System.Diagnostics.Trace` 전체에서 클래스를 사용할 수 있지만 대신 *ILogger를*구현하는 로깅 클래스의 표지 아래에 클래스를 사용하고 있으며 앱 전체에서 *ILogger* 메서드 호출을 수행합니다.

이렇게 하면 로깅을 더 풍부하게 만들려면 원하는 [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) 로깅 메커니즘으로 바꿀 수 있습니다. 예를 들어 앱이 성장함에 따라 [NLog](http://nlog-project.org/) 또는 [엔터프라이즈 라이브러리 로깅 응용 프로그램 블록과](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)같은 보다 포괄적인 로깅 패키지를 사용하도록 결정할 수 있습니다. [(Log4Net은](http://logging.apache.org/log4net/) 인기있는 또 다른 로깅 프레임 워크이지만 비동기 로깅을하지 않습니다.)

NLog와 같은 프레임워크를 사용하는 한 가지 가능한 이유는 로깅 출력을 별도의 대용량 및 고부가가치 데이터 저장소로 분할하기 위해서입니다. 이를 통해 ACT 데이터에 대한 빠른 액세스를 유지하면서 빠른 쿼리를 실행할 필요가 없는 대량의 INFORM 데이터를 효율적으로 저장할 수 있습니다.

### <a name="semantic-logging"></a>의미 체계 로깅

보다 유용한 진단 정보를 생성할 수 있는 비교적 새로운 로깅 방법은 [SLAB(엔터프라이즈 라이브러리 시맨틱 로깅 응용 프로그램 블록)을](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)참조하십시오. SLAB은 .NET 4.5에서 [WINDOWS용 이벤트 추적](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) 및 [이벤트 소스](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 지원을 사용하여 보다 구조화되고 쿼리 가능한 로그를 만들 수 있습니다. 기록하는 각 이벤트 유형에 대해 다른 메서드를 정의하여 작성하는 정보를 사용자 지정할 수 있습니다. 예를 들어 SQL Database 오류를 기록하려면 `LogSQLDatabaseError` 메서드를 호출할 수 있습니다. 이러한 종류의 예외에 대해 주요 정보 조각이 오류 번호라는 것을 알고 있으므로 메서드 서명에 오류 번호 매개 변수를 포함하고 오류 번호를 작성한 로그 레코드에 별도의 필드로 기록할 수 있습니다. 숫자는 별도의 필드에 있기 때문에 오류 번호를 메시지 문자열로 연결했을 때보다 SQL 오류 번호를 기반으로 보고서를 보다 쉽고 안정적으로 얻을 수 있습니다.

## <a name="logging-in-the-fix-it-app"></a>수정 앱에 로그인

### <a name="the-ilogger-interface"></a>ILogger 인터페이스

다음은 Fix It 앱의 *ILogger* 인터페이스입니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

이러한 방법을 사용하면 *System.Diagnostics*에서 지원하는 동일한 네 가지 수준에서 로그를 작성할 수 있습니다. TraceApi 메서드는 대기 시간에 대한 정보가 있는 외부 서비스 호출을 로깅하기 위한 것입니다. 디버그/세부 수준에 대한 메서드 집합을 추가할 수도 있습니다.

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger 인터페이스의 로거 구현

인터페이스의 구현은 정말 간단합니다. 기본적으로 표준 *System.Diagnostics* 메서드를 호출합니다. 다음 코드 조각에는 세 가지 정보 메서드와 각각 의 정보 메서드가 모두 표시됩니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>ILogger 메서드 호출

Fix It 앱의 코드가 예외를 잡을 때마다 *ILogger* 메서드를 호출하여 예외 세부 정보를 기록합니다. 또한 데이터베이스, Blob 서비스 또는 REST API를 호출할 때마다 호출 전에 스톱워치를 시작하고 서비스가 반환될 때 스톱워치를 중지하고 성공 또는 실패에 대한 정보와 함께 경과 시간을 기록합니다.

로그 메시지에는 클래스 이름과 메서드 이름이 포함됩니다. 로그 메시지가 응용 프로그램 코드의 어떤 부분을 작성했는지 확인하는 것이 좋습니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

따라서 Fix It 앱이 SQL Database를 호출할 때마다 호출, 호출한 메서드 및 정확히 걸리는 시간을 확인할 수 있습니다.

![로그에 있는 SQL 데이터베이스 쿼리](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

로그를 탐색하면 데이터베이스 호출에 걸리는 시간이 가변적인 것을 알 수 있습니다. 이 정보는 유용할 수 있습니다: 앱이 이 모든 것을 기록하기 때문에 데이터베이스 서비스가 시간이 지남에 따라 어떻게 수행되는지에 대한 기록 추세를 분석할 수 있습니다. 예를 들어 서비스는 대부분의 경우 빠를 수 있지만 요청이 실패하거나 응답이 하루 중 특정 시간에 느려질 수 있습니다.

Blob 서비스에 대해 동일한 작업을 수행할 수 있습니다.

![Blob 업로드 로그](monitoring-and-telemetry/_static/image23.png)

서비스를 호출할 때마다 작성하는 몇 줄의 코드에 불과하며, 이제 누군가가 문제가 발생했다고 말하면 문제가 무엇인지, 오류인지, 아니면 그냥 느리게 실행되는지 정확히 알 수 있습니다. 서버에 원격으로 연결하거나 오류가 발생한 후 로깅을 켜지 않고도 문제의 원인을 찾아내고 다시 만들 수 있습니다.

## <a name="dependency-injection-in-the-fix-it-app"></a>수정 앱에서 종속성 주입

위에 표시된 예제의 리포지토리 생성자가 로거 인터페이스 구현을 어떻게 가져옵니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

구현에 인터페이스를 연결하려면 응용 프로그램은 [AutoFac와](http://autofac.org/) [종속성 주입](http://en.wikipedia.org/wiki/Dependency_injection)(DI)를 사용합니다. DI를 사용하면 코드 전체의 여러 위치에서 인터페이스를 기반으로 하는 개체를 사용할 수 있으며 인터페이스가 인스턴스화될 때 사용되는 구현을 한 곳에서만 지정하면 됩니다. 이렇게 하면 구현을 쉽게 변경할 수 있습니다. 또는 자동화된 테스트를 위해 로거의 모의 버전을 대체할 수 있습니다.

Fix It 응용 프로그램은 모든 리포지토리와 모든 컨트롤러에서 DI를 사용합니다. 컨트롤러 클래스의 생성자는 리포지토리가 로거 인터페이스를 얻는 것과 동일한 방식으로 *ITaskRepository* 인터페이스를 가져옵니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

앱은 AutoFac DI 라이브러리를 사용하여 이러한 생성자에 대한 *TaskRepository* 및 *Logger* 인스턴스를 자동으로 제공합니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

이 코드는 기본적으로 생성자가 *ILogger* 인터페이스를 필요로 하는 곳, *로거* 클래스의 인스턴스를 전달하며, *IFixItTaskRepository* 인터페이스가 필요할 때마다 *FixItTaskRepository* 클래스의 인스턴스를 전달한다고 말합니다.

[AutoFac은](http://autofac.org/) 사용할 수 있는 많은 종속성 주입 프레임워크 중 하나입니다. 또 다른 인기있는 하나는 Microsoft 패턴 및 사례에서 권장하고 지원하는 [Unity입니다.](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)

## <a name="built-in-logging-support-in-azure"></a>Azure의 기본 제공 로깅 지원

Azure는 Azure 앱 [서비스에서 웹 앱에 대한](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)다음과 같은 종류의 로깅을 지원합니다.

- System.Diagnostics 추적(사이트를 다시 시작하지 않고도 즉석에서 레벨을 켜고 끌 수 있습니다).
- 윈도우 이벤트.
- IIS 로그 (HTTP / FREB).

Azure는 클라우드 서비스에서 다음과 같은 종류의 [로깅을](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)지원합니다.

- 시스템.진단 추적.
- 성능 카운터.
- 윈도우 이벤트.
- IIS 로그 (HTTP / FREB).
- 사용자 지정 디렉터리 모니터링.

Fix It 앱은 System.Diagnostics 추적을 사용합니다. 웹 앱에서 System.Diagnostics 로깅을 활성화하기 만하면 포털에서 스위치를 뒤집거나 REST API를 호출하기만 하면 됩니다. 포털에서 사이트의 **구성** 탭을 클릭하고 아래로 스크롤하여 응용 프로그램 진단 섹션을 **봅슬로** 합니다. 로깅을 켜거나 끄고 원하는 로깅 수준을 선택할 수 있습니다. Azure에서 파일 시스템 또는 저장소 계정에 로그를 작성하도록 할 수 있습니다.

![구성 탭의 앱 진단 및 사이트 진단](monitoring-and-telemetry/_static/image24.png)

Azure에서 로깅을 활성화하면 Visual Studio 출력 창에서 로그가 생성되는 대로 로그를 볼 수 있습니다.

![스트리밍 로그 메뉴](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![스트리밍 로그 메뉴](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

저장소 계정에 로그를 작성하고 Visual Studio또는 [Azure 저장소 탐색기의](https://azure.microsoft.com/features/storage-explorer/) **서버 탐색기와** 같은 Azure 저장소 테이블 서비스에 액세스할 수 있는 모든 도구를 사용하여 로그를 볼 수도 있습니다.

![서버 탐색기의 로그인](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>요약

즉시 사용 가능 원격 분석 시스템을 구현하고, 자체 코드에 계측기 로깅을 구현하고, Azure에서 로깅을 구성하는 것은 정말 간단합니다. 또한 프로덕션 문제가 있는 경우 원격 분석 시스템과 사용자 지정 로그를 조합하면 고객에게 주요 문제가 되기 전에 문제를 신속하게 해결하는 데 도움이 됩니다.

다음 [장에서는](transient-fault-handling.md) 일시적인 오류를 처리하는 방법을 살펴보고 조사해야 하는 프로덕션 문제가 되지 않도록 합니다.

## <a name="resources"></a>리소스

자세한 내용은 다음 리소스를 참조하세요.

주로 원격 분석에 대한 설명서:

- [마이크로 소프트 패턴 및 관행 - Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx). 계측 및 원격 분석 지침, 서비스 계량 지침, 상태 끝점 모니터링 패턴 및 런타임 재구성 패턴을 참조하십시오.
- [클라우드에서 페니 핀칭: Azure 웹 사이트에서 새 유물 성능 모니터링 을 활성화합니다.](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)
- [Azure 클라우드 서비스에서 대규모 서비스 설계를 위한 모범 사례입니다.](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx) 백서: 마크 심스와 마이클 토마시 원격 분석 및 진단 섹션을 참조하십시오.
- [응용 프로그램 통찰력을 갖춘 차세대 개발.](https://msdn.microsoft.com/magazine/dn683794.aspx) MSDN 매거진 기사.

주로 로깅에 대한 설명서:

- [시맨틱 로깅 응용 프로그램 블록(SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). 닐 매켄지는 SLAB을 통해 의미 론적 로깅의 사례를 제시합니다.
- [의미 체계 로깅을 통해 구조적이고 의미 있는 로그 만들기.](https://channel9.msdn.com/Events/Build/2013/3-336) (비디오) 줄리안 도밍게즈는 SLAB을 통해 의미 론적 로깅의 사례를 제시합니다.
- [EF6 SQL 로깅 - 1부: 간단한 로깅](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/). 아서 비커스는 EF 6의 엔티티 프레임워크에서 실행되는 쿼리를 기록하는 방법을 보여줍니다.
- [ASP.NET MVC 응용 프로그램에서 엔터티 프레임 워크와 연결 복원력 및 명령 차단](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md). 9부로 구성된 자습서 시리즈의 네 번째 는 EF 6 명령 차단 기능을 사용하여 Entity Framework에서 데이터베이스로 전송된 SQL 명령을 기록하는 방법을 보여 주십입니다.
- [C # 5.0 발신자 정보 특성을 사용하여 로깅을 개선합니다.](http://www.dotnetcurry.com/showarticle.aspx?ID=972) 리터럴에 하드 코딩하거나 수동으로 리플렉션을 사용하지 않고 calling 메서드의 이름을 쉽게 기록하는 방법.

주로 문제 해결에 대한 설명서:

- [Azure 문제 &amp; 해결 디버깅 블로그](https://blogs.msdn.com/b/kwill/).
- [AzureTools - Azure 개발자 지원 팀에서 사용하는 진단 유틸리티](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)입니다. Azure VM에서 다양한 진단 및 모니터링 도구를 다운로드하고 실행하는 데 사용할 수 있는 도구에 대한 다운로드 링크를 소개하고 제공합니다. 특정 VM에서 문제를 진단해야 하는 경우에 유용합니다.
- [Visual Studio를 사용하여 Azure 앱 서비스에서 웹 앱 문제 해결.](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) System.Diagnostics 추적 및 원격 디버깅을 시작하기 위한 단계별 자습서입니다.

비디오:

- [페일세이프: 확장 가능하고 탄력적인 클라우드 서비스 구축.](https://channel9.msdn.com/Series/FailSafe) 울리히 호만, 마크 머큐리, 마크 심스의 9부작 시리즈. MICROSOFT 고객 자문 팀(CAT) 경험이 실제 고객과 함께 작성한 스토리와 함께 매우 접근가능하고 흥미로운 방식으로 높은 수준의 개념과 아키텍처 원칙을 제시합니다. 에피소드 4와 9는 모니터링 및 원격 측정에 관한 것입니다. 에피소드 9에는 모니터링 서비스 메트릭스허브, 앱다이내믹스, 뉴 리릭 및 페이저듀티에 대한 개요가 포함되어 있습니다.
- [큰 건물: Azure 고객으로부터 얻은 교훈 - 파트 II](https://channel9.msdn.com/Events/Build/2012/3-030). Mark Simms는 실패를 위한 설계와 모든 계측에 대해 이야기합니다. Failsafe 시리즈와 유사하지만 자세한 방법 세부 정보로 이동합니다.

코드 샘플:

- [Azure의 클라우드 서비스 기본 사항.](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649) Microsoft Azure 고객 자문 팀에서 만든 샘플 응용 프로그램입니다. 다음 문서에서 설명한 대로 원격 분석 및 로깅 방법을 모두 보여 줍니다. 샘플은 [NLog](http://nlog-project.org/)를 사용하여 응용 프로그램 로깅을 구현합니다. 관련 설명서의 경우 [원격 분석 및 로깅에 대한 TechNet 위키 문서 4개 시리즈를](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)참조하십시오.

> [!div class="step-by-step"]
> [이전](design-to-survive-failures.md)
> [다음](transient-fault-handling.md)
