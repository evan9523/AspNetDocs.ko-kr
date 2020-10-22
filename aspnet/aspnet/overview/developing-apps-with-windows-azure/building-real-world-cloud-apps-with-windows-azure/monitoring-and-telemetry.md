---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 모니터링 및 원격 분석 (Azure를 사용 하 여 클라우드 앱 빌드 Real-World) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345579"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>모니터링 및 원격 분석 (Azure를 사용 하 여 클라우드 앱 빌드) (Real-World)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

많은 사람들은 고객이 응용 프로그램의 작동 중단 시간을 알려 주는 데 사용 됩니다. 어디에서 나 특히 클라우드에서는 바람직하지 않습니다. 빠른 알림은 보장 되지 않으며, 알림을 받을 때 발생 하는 상황에 대 한 데이터를 최소한으로 또는 잘못 이해 하는 경우가 많습니다. 좋은 원격 분석 및 로깅 시스템을 사용 하 여 앱에서 발생 하는 작업을 파악 하 고, 문제를 해결 하 고 유용한 문제 해결 정보를 얻을 수 있습니다.

## <a name="buy-or-rent-a-telemetry-solution"></a>원격 분석 솔루션 구입 또는 임대

> [!NOTE]
> 이 문서는 [Application Insights](/azure/application-insights/app-insights-overview) 출시 되기 전에 작성 되었습니다. Azure에서 원격 분석 솔루션에 대 한 기본 방법은 Application Insights입니다. 자세한 내용은 [ASP.NET 웹 사이트에 대 한 Application Insights 설정](/azure/application-insights/app-insights-asp-net) 을 참조 하세요.

클라우드 환경에 대 한 유용한 사항 중 하나는 정말로 구매 하거나 승리 하는 방법에 대 한 것입니다. 원격 분석은 예입니다. 많은 노력이 없으면 매우 좋은 원격 분석 시스템을 가동 하 고 실행 하는 것은 매우 경제적입니다. Azure와 통합 되는 다양 한 파트너가 있으며, 그 중 일부는 무료 계층 이므로 아무 것도 기본 원격 분석을 얻을 수 있습니다. 다음은 현재 Azure에서 사용할 수 있는 몇 가지 방법입니다.

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) 에는 모니터링 기능도 포함 되어 있습니다.

원격 분석 시스템을 쉽게 사용할 수 있는 방법을 보여 주기 위해 새 유물을 설정 하는 과정을 빠르게 안내 합니다.

Azure 관리 포털에서 서비스에 등록 합니다. **새로 만들기**를 클릭 한 다음 **저장**을 클릭 합니다. **추가 기능 선택** 대화 상자가 나타납니다. 아래로 스크롤하여 **새 유물**을 클릭 합니다.

![추가 기능 선택](monitoring-and-telemetry/_static/image1.png)

오른쪽 화살표를 클릭 하 고 원하는 서비스 계층을 선택 합니다. 이 데모에서는 무료 계층을 사용 합니다.

![추가 기능 개인 설정](monitoring-and-telemetry/_static/image2.png)

오른쪽 화살표를 클릭 하 고, "구매"를 확인 하 고, 이제 새 유물을 포털의 추가 기능으로 표시 합니다.

![구매 검토](monitoring-and-telemetry/_static/image3.png)

![관리 포털의 새 유물 추가 기능](monitoring-and-telemetry/_static/image4.png)

**연결 정보**를 클릭 하 고 라이선스 키를 복사 합니다.

![연결 정보](monitoring-and-telemetry/_static/image5.png)

포털에서 웹 앱에 대 한 **구성** 탭으로 이동 하 여 **성능 모니터링** 을 **추가 기능**으로 설정 하 고 **추가 기능 선택** 드롭다운 목록을 **새 유물**으로 설정 합니다. 그런 다음 **Save**를 클릭합니다.

![구성 탭의 새 유물](monitoring-and-telemetry/_static/image6.png)

Visual Studio에서 앱에 새 유물 NuGet 패키지를 설치 합니다.

![구성 탭의 개발자 분석](monitoring-and-telemetry/_static/image7.png)

앱을 Azure에 배포 하 고 사용을 시작 합니다. 몇 가지 수정 It 작업을 만들어 새 유물을 모니터링 하기 위한 몇 가지 작업을 제공 합니다.

그런 다음 포털의 **추가** 기능 탭에 있는 **새 유물** 페이지로 돌아가 **관리**를 클릭 합니다. 포털은 인증을 위해 Single Sign-On를 사용 하 여 새 유물 관리 포털로 사용자를 전송 하므로 자격 증명을 다시 입력할 필요가 없습니다. 개요 페이지는 다양 한 성능 통계를 제공 합니다. (이미지를 클릭 하 여 개요 페이지 전체 크기를 표시 합니다.)

[![새 유물 모니터링 탭](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

다음은 몇 가지 통계를 볼 수 있습니다.

- 하루에 여러 번의 평균 응답 시간입니다.

    ![응답 시간](monitoring-and-telemetry/_static/image10.png)
- 하루 중 서로 다른 시간에 처리량 속도 (분당 요청 수)입니다.

    ![처리량](monitoring-and-telemetry/_static/image11.png)
- 다른 HTTP 요청을 처리 하는 데 걸린 서버 CPU 시간입니다.

    ![웹 트랜잭션 시간](monitoring-and-telemetry/_static/image12.png)
- 응용 프로그램 코드의 여러 부분에서 소요 된 CPU 시간:

    ![추적 정보](monitoring-and-telemetry/_static/image13.png)
- 성능 통계를 기록 합니다.

    ![기록 성능](monitoring-and-telemetry/_static/image14.png)
- Blob service와 같은 외부 서비스에 대 한 호출과 서비스의 안정적이 고 응답 하는 방법에 대 한 통계입니다.

    ![외부 서비스](monitoring-and-telemetry/_static/image15.png)

    ![외부 서비스](monitoring-and-telemetry/_static/image16.png)

    ![외부 서비스](monitoring-and-telemetry/_static/image17.png)
- 전 세계 또는 미국 웹 앱 트래픽 내의 위치에 대 한 정보를 제공 합니다.

    ![Geography](monitoring-and-telemetry/_static/image18.png)

보고서 및 이벤트를 설정할 수도 있습니다. 예를 들어, 오류를 볼 수 있는 경우 언제 든 지 경고 지원 담당자에 게 문제에 대 한 전자 메일을 보낼 수 있습니다.

![보고서](monitoring-and-telemetry/_static/image19.png)

새 유물은 원격 분석 시스템의 한 가지 예에 불과합니다. 이 모든 것을 다른 서비스 에서도 가져올 수 있습니다. 클라우드의 장점은 코드를 작성할 필요 없이 최소한의 비용을 들이지 않고도 응용 프로그램이 어떻게 사용 되 고 있는지에 대 한 훨씬 더 많은 정보를 얻을 수 있다는 것입니다.

<a id="log"></a>
## <a name="log-for-insight"></a>정보에 대 한 로그

원격 분석 패키지는 좋은 첫 번째 단계 이지만 사용자가 직접 코드를 계측 해야 합니다. 원격 분석 서비스는 문제가 발생 하는 경우 사용자에 게 알려 주며, 사용자의 코드에서 발생 하는 상황에 대 한 통찰력을 제공 하지 않을 수 있습니다.

앱에서 수행 하는 작업을 확인 하기 위해 프로덕션 서버에 원격으로 로그인 하지 않으려고 합니다. 서버 한 대를가지고 있는 경우에는이 작업을 수행 하는 것이 좋습니다. 그러나 수백 대의 서버에 대 한 크기를 조정 하는 경우에는 어떻게 해야 하나요? 로깅에서는 문제를 분석 하 고 디버그 하기 위해 프로덕션 서버에 원격으로 연결할 필요가 없는 충분 한 정보를 제공 해야 합니다. 로그를 통해서만 문제를 격리할 수 있도록 충분 한 정보를 기록 해야 합니다.

### <a name="log-in-production"></a>프로덕션 로그인

많은 사람들은 문제가 발생 하 고 디버그 하려는 경우에만 프로덕션에서 추적을 설정 합니다. 이 경우 문제를 인식 하는 시간과이에 대 한 유용한 문제 해결 정보를 얻는 시간 사이에 상당한 지연이 발생할 수 있습니다. 그리고 사용자가 제공 하는 정보는 일시적인 오류에 도움이 되지 않을 수 있습니다.

저장소를 저렴 하 게 하는 클라우드 환경에서 권장 되는 사항은 항상 프로덕션에서 로그온을 유지 하는 것입니다. 이러한 방식으로 오류가 발생 하는 경우에는 이미 로그 되어 있으며 시간이 지남에 따라 개발 되거나 정기적으로 발생 하는 문제를 분석 하는 데 도움이 되는 기록 데이터를 사용할 수 있습니다. 제거 프로세스를 자동화 하 여 오래 된 로그를 삭제할 수 있지만 로그를 유지 하는 것 보다 프로세스를 설정 하는 것이 더 부담이 될 수 있습니다.

추가 된 로깅 비용은 문제가 발생할 때 이미 사용 가능한 모든 정보를 사용 하 여 비용을 절감할 수 있는 문제 해결 시간과 비용에 비해 간단 합니다. 그런 다음 사용자에 게 마지막 밤 8:00에 대 한 임의 오류가 발생 했지만 오류를 기억할 수 없는 경우 문제를 쉽게 파악할 수 있습니다.

한 달에 $4 보다 작은 경우에는 50 기가바이트의 로그를 유지할 수 있습니다. 따라서 성능 병목 현상을 방지 하려면 로깅 라이브러리가 비동기 인지 확인 하는 것이 중요 합니다.

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>조치가 필요한 로그를 알려 주는 로그 구분

로그는 정보를 알려 주거나 (무엇을 알고 싶습니다.) 작업을 수행 하려고 합니다. 작업을 수행 하는 데 완전히 또는 자동화 된 프로세스가 필요한 문제에 대 한 작업 로그를 작성 해야 합니다. 작업 로그가 너무 많으면 노이즈를 만들어 자세히 살펴볼 하 여 모든 작업을 수행 하는 데 충분 한 작업을 수행 해야 합니다. 그리고 작업 로그가 지원 담당자에 게 전자 메일을 보내는 등의 일부 작업을 자동으로 트리거하는 경우 단일 문제로 인해 수천 개의 이러한 작업을 트리거할 수 없도록 합니다.

.NET 시스템 진단 추적에서 로그에는 오류, 경고, 정보 및 디버그/자세한 정보 표시 수준이 할당 될 수 있습니다. ACT 로그에 대 한 오류 수준을 예약 하 고 로그에 더 낮은 수준을 사용 하 여 로그를 알리는 행위를 구분할 수 있습니다.

![로깅 수준](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>런타임에 로깅 수준 구성

프로덕션 환경에서 로깅 기능을 사용 하는 것이 좋지만 응용 프로그램을 다시 시작 하거나 다시 시작 하지 않고도 런타임에 기록 하는 세부 수준에 맞게 조정할 수 있는 로깅 프레임 워크를 구현 하는 것도 좋은 방법입니다. 예를 들어에서 추적 기능을 사용 하는 경우 `System.Diagnostics` 오류, 경고, 정보 및 디버그/자세한 정보 표시 로그를 만들 수 있습니다. 항상 프로덕션에서 오류, 경고 및 정보 로그를 기록 하는 것이 좋으며, 경우에 따라 문제 해결을 위해 디버그/자세한 정보 로깅을 동적으로 추가할 수 있습니다.

Azure App Service의 Web Apps에는 `System.Diagnostics` 파일 시스템, 테이블 저장소 또는 Blob 저장소에 로그를 작성 하는 기능이 기본적으로 제공 됩니다. 각 저장소 대상에 대해 서로 다른 로깅 수준을 선택할 수 있으며, 응용 프로그램을 다시 시작 하지 않고 즉시 로깅 수준을 변경할 수 있습니다. HDInsight는 blob 저장소를 직접 사용 하는 방법을 알고 있으므로 Blob 저장소 지원을 통해 응용 프로그램 로그에서 [hdinsight](https://docs.microsoft.com/azure/hdinsight/) 분석 작업을 보다 쉽게 실행할 수 있습니다.

### <a name="log-exceptions"></a>예외 기록

예외를 그냥 넣지 마세요 *. 로깅 코드의 ToString ()* 컨텍스트 정보를 남깁니다. SQL 오류의 경우 SQL 오류 번호가 남습니다. 모든 예외에 대해 문제 해결에 필요한 모든 항목을 제공 하는지 확인 하기 위해 컨텍스트 정보, 예외 자체 및 내부 예외를 포함 합니다. 예를 들어 컨텍스트 정보에는 서버 이름, 트랜잭션 식별자 및 사용자 이름 (암호 또는 비밀)이 포함 될 수 있습니다.

각 개발자에 게 예외 로깅을 사용 하 여 적절 한 작업을 수행 하는 경우 그 중 일부는 그렇지 않습니다. 매번 적절 한 방식으로 수행 되도록 하려면로 거 인터페이스에 예외 처리를 직접 작성 합니다. 예외 개체 자체를로 거 클래스에 전달 하 고로 거 클래스에서 예외 데이터를 제대로 기록 합니다.

### <a name="log-calls-to-services"></a>서비스에 대 한 로그 호출

응용 프로그램이 서비스를 호출할 때마다 데이터베이스 또는 REST API 또는 외부 서비스에 있든 관계 없이 로그를 작성 하는 것이 좋습니다. 성공 또는 실패를 표시 하는 것은 아니지만 각 요청이 걸린 시간은 로그에 포함 합니다. 클라우드 환경에서 중단을 완료 하는 대신 속도가 느려지는 것과 관련 된 문제가 종종 표시 됩니다. 일반적으로 10 밀리초가 소요 되는 항목은 갑자기 시작 될 수 있습니다. 사용자가 앱을 느리게 표시 하는 경우, 사용자가 보유 한 새 유물 또는 원격 분석 서비스를 살펴보고 경험을 확인할 수 있도록 하 고, 속도가 느려지는 이유에 대 한 세부 정보를 확인 하기 위해 고유한 로그를 확인 하는 것이 좋습니다.

### <a name="use-an-ilogger-interface"></a>ILogger 인터페이스 사용

프로덕션 응용 프로그램을 만들 때 수행 하는 권장 사항은 간단한 *ILogger* 인터페이스를 만들고 일부 메서드를 적용 하는 것입니다. 이렇게 하면 나중에 로깅 구현을 쉽게 변경할 수 있으며,이를 위해 모든 코드를 사용할 필요가 없습니다. `System.Diagnostics.Trace`Fix it 앱 전체에서 클래스를 사용할 수 있지만, 대신 *ILogger*를 구현 하는 로깅 클래스의 내부적으로 사용 하 고 앱 전체에서 *ILogger* 메서드 호출을 수행 합니다.

이렇게 하면 로깅을 더 풍부 하 게 만들려는 경우 [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) 원하는 로깅 메커니즘으로 바꿀 수 있습니다. 예를 들어 앱이 커지면 [Nlog](http://nlog-project.org/) 또는 [Enterprise Library Logging 응용 프로그램 블록과](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)같은 보다 포괄적인 로깅 패키지를 사용 하도록 결정할 수 있습니다. [Log4Net](http://logging.apache.org/log4net/) 는 다른 인기 있는 로깅 프레임 워크 이지만 비동기 로깅은 수행 하지 않습니다.

NLog와 같은 프레임 워크를 사용 하는 한 가지 이유는 로깅 출력을 별도의 고용량 및 높은 값 데이터 저장소로 분할 하는 것입니다. 이를 통해 고속 쿼리를 실행할 필요가 없는 많은 양의 알림 데이터를 효율적으로 저장 하는 동시에 ACT 데이터에 빠르게 액세스할 수 있습니다.

### <a name="semantic-logging"></a>의미 체계 로깅

보다 유용한 진단 정보를 생성할 수 있는 로깅을 비교적 새로운 방식으로 수행 하려면 [Enterprise Library 의미 체계 로깅 응용 프로그램 블록 (슬 래 브)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)을 참조 하세요. 슬 래 브는 .NET 4.5에서 ETW ( [ETW(Windows용 이벤트 추적)](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) ) 및 [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 지원 기능을 사용 하 여 더 구조적인 및 쿼리 가능한 로그를 만들 수 있도록 합니다. 기록 하는 각 이벤트 형식에 대해 다른 방법을 정의 하 여 작성 한 정보를 사용자 지정할 수 있습니다. 예를 들어 SQL Database 오류를 기록 하려면 메서드를 호출할 수 있습니다 `LogSQLDatabaseError` . 이러한 종류의 예외에 대 한 중요 한 정보는 오류 번호를 알고 있으므로 메서드 서명에 오류 번호 매개 변수를 포함 하 고 기록 하는 로그 레코드의 개별 필드로 오류 번호를 기록할 수 있습니다. 이 번호는 별도의 필드에 있으므로 오류 번호를 메시지 문자열에 연결 하는 경우와 같이 SQL 오류 번호를 기반으로 하는 보고서를 보다 쉽고 안정적으로 가져올 수 있습니다.

## <a name="logging-in-the-fix-it-app"></a>Fix It 앱에서 로깅

### <a name="the-ilogger-interface"></a>ILogger 인터페이스

Fix It 앱의 *ILogger* 인터페이스는 다음과 같습니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

이러한 메서드를 사용 하 여 *시스템 진단*에서 지 원하는 것과 동일한 4 가지 수준에서 로그를 작성할 수 있습니다. TraceApi 메서드는 대기 시간에 대 한 정보를 사용 하 여 외부 서비스 호출을 로깅하는 데 사용 됩니다. 디버그/자세한 정보 표시 수준에 대 한 메서드 집합을 추가할 수도 있습니다.

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger 인터페이스의로 거 구현

인터페이스 구현은 정말 간단 합니다. 기본적으로 표준 *system.web* 메서드를 호출 하기만 하면 됩니다. 다음 코드 조각에서는 세 가지 정보 메서드와 각각 다른 메서드를 보여 줍니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>ILogger 메서드 호출

Fix It 앱에서 코드는 예외를 catch 할 때마다 *ILogger* 메서드를 호출 하 여 예외 정보를 기록 합니다. 또한 데이터베이스, Blob service 또는 REST API에 대 한 호출을 할 때마다 호출 전에 초시계를 시작 하 고, 서비스가 반환 될 때 초시계를 중지 하 고, 성공 또는 실패에 대 한 정보와 함께 경과 된 시간을 기록 합니다.

로그 메시지에는 클래스 이름과 메서드 이름이 포함 됩니다. 로그 메시지에서 응용 프로그램 코드를 작성 하는 부분을 확인 하는 것이 좋습니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

따라서 Fix It 앱이 SQL Database에 대 한 호출을 수행할 때마다 호출, 호출 하는 메서드 및 소요 시간을 정확 하 게 확인할 수 있습니다.

![로그의 SQL Database 쿼리](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

로그를 탐색 하는 경우 데이터베이스 호출 시간이 가변적 임을 알 수 있습니다. 이 정보가 유용할 수 있습니다. 앱이 모든 작업을 기록 하기 때문에 시간이 지남에 따라 데이터베이스 서비스의 수행 방식에 대 한 기록 추세를 분석할 수 있습니다. 예를 들어 서비스는 대부분 시간을 빠르게 할 수 있지만 요청이 실패 하거나 특정 시간에 응답 속도가 느려질 수 있습니다.

Blob service에 대해 동일한 작업을 수행할 수 있습니다. 앱이 새 파일을 업로드 하 고, 로그가 있으며, 각 파일을 업로드 하는 데 걸린 시간을 정확 하 게 확인할 수 있습니다.

![Blob 업로드 로그](monitoring-and-telemetry/_static/image23.png)

서비스를 호출할 때마다 작성 되는 코드의 추가 코드 줄 뿐 이며, 이제 누군가가 문제를 발생 시킬 때마다 문제가 무엇 인지, 오류 인지, 아니면 느리게 실행 되 었는 지를 정확히 알 수 있습니다. 서버에 원격으로 로그인 하지 않고도 문제의 원인을 파악 하 고 오류가 발생 한 후에도 로깅을 설정 하 여 다시 만들 수 있습니다.

## <a name="dependency-injection-in-the-fix-it-app"></a>Fix It 앱의 종속성 주입

위에 표시 된 예제의 리포지토리 생성자가로 거 인터페이스 구현을 가져오는 방법을 궁금할 수 있습니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

인터페이스를 구현에 연결 하기 위해 앱은 [Autofac](http://autofac.org/)와 함께 DI ( [종속성 주입](http://en.wikipedia.org/wiki/Dependency_injection))를 사용 합니다. DI를 사용 하면 코드 전체의 여러 위치에서 인터페이스를 기반으로 하는 개체를 사용할 수 있으며, 인터페이스를 인스턴스화할 때 사용 되는 구현을 한 곳 에서만 지정할 수 있습니다. 이렇게 하면 구현을 보다 쉽게 변경할 수 있습니다. 예를 들어 시스템 진단로 거를 NLog로 거로 바꿀 수 있습니다. 또는 자동화 된 테스트의 경우 모의 버전의로 거를 대체 하는 것이 좋습니다.

Fix It 응용 프로그램은 모든 리포지토리 및 모든 컨트롤러에서 DI를 사용 합니다. 컨트롤러 클래스의 생성자는 리포지토리가로 거 인터페이스를 가져오는 것과 동일한 방식으로 *Itaskrepository* 인터페이스를 가져옵니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

앱은 AutoFac DI 라이브러리를 사용 하 여 이러한 생성자에 대 한 *Taskrepository* 및 *로 거* 인스턴스를 자동으로 제공 합니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

이 코드는 기본적으로 생성자에 *ILogger* 인터페이스가 필요 하 고, *로 거* 클래스의 인스턴스를 전달 하 고, *ifixittaskrepository* 인터페이스가 필요할 때마다 *fixittaskrepository* 클래스의 인스턴스를 전달 한다는 것을 의미 합니다.

[Autofac](http://autofac.org/) 는 사용할 수 있는 많은 종속성 주입 프레임 워크 중 하나입니다. 또 다른 인기 있는 것은 Microsoft 패턴 및 관행에서 권장 되 고 지원 되는 [Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)입니다.

## <a name="built-in-logging-support-in-azure"></a>Azure의 기본 제공 로깅 지원

Azure는 [Azure App Service의 Web Apps에 대해](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)다음과 같은 종류의 로깅을 지원 합니다.

- 시스템 진단 추적 (사이트를 다시 시작 하지 않고 신속 하 게 수준을 켜고 설정할 수 있음)
- Windows 이벤트.
- IIS 로그 (HTTP/FREB).

Azure는 [Cloud Services에서](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)다음과 같은 종류의 로깅을 지원 합니다.

- 시스템 진단 추적.
- 성능 카운터.
- Windows 이벤트.
- IIS 로그 (HTTP/FREB).
- 사용자 지정 디렉터리 모니터링.

Fix It 앱은 시스템 진단 추적을 사용 합니다. 웹 앱에서 진단 로깅을 사용 하도록 설정 하려면 포털에서 스위치를 대칭 이동 하거나 REST API를 호출 해야 합니다. 포털에서 사이트에 대 한 **구성** 탭을 클릭 하 고 아래로 스크롤하여 **애플리케이션 진단** 섹션을 확인 합니다. 로깅을 설정 하거나 해제 하 고 원하는 로깅 수준을 선택할 수 있습니다. Azure에서 파일 시스템 또는 저장소 계정에 로그를 쓸 수 있습니다.

![구성 탭의 앱 진단 및 사이트 진단](monitoring-and-telemetry/_static/image24.png)

Azure에서 로깅을 사용 하도록 설정 하면 생성 될 때 Visual Studio 출력 창에서 로그를 볼 수 있습니다.

![스트리밍 로그 메뉴](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![스트리밍 로그 메뉴](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

로그를 저장소 계정에 기록 하 고 Visual Studio 또는 [Azure Storage 탐색기](https://azure.microsoft.com/features/storage-explorer/)의 **서버 탐색기** 와 같은 Azure Storage Table service에 액세스할 수 있는 도구를 사용 하 여 로그를 볼 수도 있습니다.

![서버 탐색기 로그인](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>요약

매우 간단 하 게 기본 원격 분석 시스템을 구현 하 고, 고유한 코드에서 로깅을 계측 하 고, Azure에서 로깅을 구성할 수 있습니다. 또한 프로덕션 문제가 있는 경우 원격 분석 시스템 및 사용자 지정 로그를 조합 하면 문제를 신속 하 게 해결 하는 데 도움이 됩니다.

[다음 장에서](transient-fault-handling.md) 조사 해야 하는 프로덕션 문제가 되지 않도록 일시적인 오류를 처리 하는 방법을 살펴보겠습니다.

## <a name="resources"></a>리소스

자세한 내용은 다음 리소스를 참조하세요.

설명서는 주로 원격 분석에 대 한 것입니다.

- [Microsoft 패턴 및 사례-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx) 계측 및 원격 분석 지침, 서비스 계량 지침, 상태 끝점 모니터링 패턴 및 런타임 재구성 패턴을 참조 하세요.
- [클라우드의 Penny 집기: Azure Websites에서 새로운 유물 성능 모니터링을 사용 하도록 설정](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)합니다.
- [Azure Cloud Services에서 Large-Scale 서비스를 디자인 하는 방법에 대 한 모범 사례](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)입니다. 이 백서에서는 Simm 및 Michael Thomassy을 표시 합니다. 원격 분석 및 진단 섹션을 참조 하세요.
- [Application Insights를 사용한 차세대 개발](https://msdn.microsoft.com/magazine/dn683794.aspx) MSDN Magazine 문서입니다.

설명서는 주로 로깅에 대해 설명 합니다.

- [의미 체계 로깅 응용 프로그램 블록 (슬 래 브)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). Neil Mackenzie는 슬 래 브를 포함 하는 의미 체계 로깅 사례를 제공 합니다.
- [의미 체계 로깅을 사용 하 여 구조적 및 의미 있는 로그 만들기](https://channel9.msdn.com/Events/Build/2013/3-336) 화면이 율리우스 Dominguez은 슬 래 브의 의미 체계 로깅 사례를 제공 합니다.
- [EF6 SQL 로깅 – 1 부: 간단한 로깅](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/) Arthur Vickers는 EF 6에서 Entity Framework에 의해 실행 된 쿼리를 기록 하는 방법을 보여 줍니다.
- [ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 연결 복원 력 및 명령 가로채기](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md) 네 부분으로 구성 된 자습서 시리즈의 네 번째 자습서 시리즈에서는 EF 6 명령 가로채기 기능을 사용 하 여 Entity Framework 하 여 데이터베이스로 전송 된 SQL 명령을 기록 하는 방법을 보여 줍니다.
- [C # 5.0 호출자 정보 특성을 사용 하 여 로깅을 개선](http://www.dotnetcurry.com/showarticle.aspx?ID=972)합니다. 리터럴을 하드 코딩 하거나 리플렉션을 사용 하 여 직접 호출 하는 메서드의 이름을 쉽게 기록 하는 방법입니다.

설명서는 주로 문제 해결에 대 한 것입니다.

- [Azure 문제 해결 &amp; 디버깅 블로그](https://blogs.msdn.com/b/kwill/).
- [Azuretools – Azure 개발자 지원 팀에서 사용 하는 진단 유틸리티](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)입니다. Azure VM에서 다양 한 진단 및 모니터링 도구를 다운로드 하 고 실행 하는 데 사용할 수 있는 도구에 대 한 다운로드 링크를 소개 하 고 제공 합니다. 특정 VM에서 문제를 진단 해야 하는 경우에 유용 합니다.
- [Visual Studio를 사용 하 여 Azure App Service에서 웹 앱 문제를 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)합니다. 시스템 진단 추적 및 원격 디버깅을 시작 하기 위한 단계별 자습서입니다.

비디오:

- [안전 하지 않음: 확장 가능 하 고 복원 가능한 Cloud Services 빌드](https://channel9.msdn.com/Series/FailSafe) Ulrich HoMarc Mercuri 및 Mark Simm에서 9 부분으로 된 시리즈. Microsoft의 Microsoft CAT (고객 자문 팀) 경험을 통해 실제 고객과 함께 제공 되는 스토리를 통해 매우 편리 하 게 액세스할 수 있고 흥미로운 방식으로 높은 수준의 개념 및 아키텍처 원칙을 제공 합니다. 에피소드 4와 9는 모니터링 및 원격 분석에 대 한 것입니다. 에피소드 9에는 MetricsHub, AppDynamics, 새 유물 및 PagerDuty 모니터링 서비스에 대 한 개요가 포함 되어 있습니다.
- [대규모 빌드: Azure 고객 으로부터 얻은 교훈-2 부](https://channel9.msdn.com/Events/Build/2012/3-030). Simm 표시는 오류 설계 및 모든 항목 계측에 대 한 것입니다. 안전 계열과 유사 하지만 자세한 방법에 대해 자세히 설명 합니다.

코드 샘플:

- [Azure의 클라우드 서비스 기본 사항](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)입니다. Microsoft Azure 고객 자문 팀에서 만든 샘플 응용 프로그램입니다. 다음 문서에 설명 된 대로 원격 분석 및 로깅 사례를 모두 보여 줍니다. 이 샘플에서는 [Nlog](http://nlog-project.org/)를 사용 하 여 응용 프로그램 로깅을 구현 합니다. 관련 설명서는 [원격 분석 및 로깅에 대 한 네 가지 TechNet wiki 문서 시리즈](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](design-to-survive-failures.md)
> [다음](transient-fault-handling.md)
