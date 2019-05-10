---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
title: 큐 중심 작업 패턴 (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: cc1ad51b-40c3-4c68-8620-9aaa0fd1f6cf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
msc.type: authoredcontent
ms.openlocfilehash: 9081691207a1a8ccd58e1a93a0be06af15c0b2d0
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65118723"
---
# <a name="queue-centric-work-pattern-building-real-world-cloud-apps-with-azure"></a>큐 중심 작업 패턴 (실제 클라우드 앱 빌드 Azure 사용 하 여)

하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.

이전에 살펴본 여러 서비스를 사용 하 여 앱의 효과적인 SLA가 "복합" SLA를 발생할 수 있습니다 하는 *제품* 개별 Sla에 대 한 합니다. 예를 들어 Fix It 응용 프로그램 웹 사이트, 저장소 및 SQL Database를 사용합니다. 이러한 서비스 중 하나가 실패 하면 앱 사용자에 게 오류가 반환 됩니다.

캐싱이 읽기 전용 콘텐츠에 대 한 일시적인 오류를 처리 하는 것이 좋습니다. 하지만 응용 프로그램 작업 해야 하는 경우에 어떻게? 예를 들어 사용자가 새 수정 작업을 제출 하는 경우 앱은 캐시에 작업을 바로 넣을 수 없습니다. 앱을 처리할 수 있도록 영구 데이터 저장소에 수정 작업을 작성 해야 합니다.

큐 중심 작업 패턴 제공 되는 위치입니다. 이 패턴을 사용 하는 웹 계층 및 백 엔드 서비스 간의 느슨한 결합 합니다.

패턴의 작동 방식을 다음과 같습니다. 응용 프로그램 요청을 가져오면 작업 항목을 큐에 배치 하 고 즉시 응답을 반환 합니다. 그런 다음 별도 백 엔드 프로세스를 큐에서 작업 항목을 가져오는 하 고 작업을 수행 합니다.

큐 중심 작업 패턴에 유용합니다.

- 작업 시간이 오래 걸리는 (대기).
- 필요한 작업을 외부 서비스를 항상 사용할 수 없습니다.
- 작업이 리소스를 많이 사용 (CPU).
- 갑작스러운 부하 버스트) (적용 평준화 하는 속도 활용할 수 있는 작업입니다.

## <a name="reduced-latency"></a>대기 시간 단축된

큐는 시간이 오래 걸리는 작업을 수행 하는 언제 든 지 유용 합니다. 작업 변수를 사용할 경우 몇 초 이상 차단 하는 대신 최종 사용자 작업 항목 큐에 저장 합니다. "노력 하 고,"는 사용자에 게 알림 및 다음 큐 수신기를 사용 하 여 백그라운드에서 작업을 처리 합니다.

예를 들어 온라인 상점에서 무언가 구입 하면 웹 사이트 주문을 확인 즉시 합니다. 그렇다고 전자 메일이 배달 트럭에 이미 있습니다. 작업을 큐에 배치한 하 고 백그라운드에서 이러한 항목 전달에 대 한 준비 신용 검사를 수행 하는 등입니다.

짧은 대기 시간을 사용 하 여 시나리오에 대 한 총 엔드-투-엔드에 비해 작업을 동기적으로 수행 하는 큐를 사용 하 여 더 수 있습니다. 하지만 다른 이점도 해당 단점은 보다 클 수 있습니다 경우에 합니다.

## <a name="increased-reliability"></a>향상 된 안정성

Fix It 했습니다 되었습니다 지켜보는 것 지금의 버전에서는 SQL Database 백 엔드를 사용 하 여 웹 프런트 엔드는 밀접 하 게 결합 됩니다. SQL database 서비스를 사용할 수 없는 경우 사용자는 오류를 가져옵니다. 재시도 작동 하지 않는 경우 (즉, 오류를 일시적인 이상) 할 수 있는 유일한 항목은 오류를 표시 하 고 나중에 다시 시도를 사용자에 게 요청 합니다.

![SQL Database 백 엔드에 실패 한 경우 실패 한 프런트 엔드 다이어그램 보여 주는 웹](queue-centric-work-pattern/_static/image1.png)

앱은 사용자가 수정 작업을 제출 하는 경우에 큐를 사용 하 여, 큐에 메시지를 씁니다. 메시지 페이로드를 [JSON](http://json.org/) 태스크의 표현입니다. 메시지는 큐에 기록 되는 즉시 앱 반환 하 고 즉시 사용자에 게 성공 메시지를 보여 줍니다.

오프 라인으로 전환-와 같은 SQL 데이터베이스 또는 큐 수신기-백 엔드 서비스의 경우 사용자는 새 수정 작업 계속 제출할 수 있습니다. 백 엔드 서비스를 다시 사용할 수까지는 메시지 큐만 합니다. 이 시점에서 백 엔드 서비스는 백로그에서 catch 합니다.

![웹 프런트 엔드를 계속 하는 SQL Database 오류가 있을 때 함수를 보여 주는 다이어그램](queue-centric-work-pattern/_static/image2.png)

또한 이제 추가할 수 있습니다 백 엔드 논리를 더 프런트 엔드의 복원 력을 염려 하지 않고 있습니다. 예를 들어, 다음을 새 Fix It가 할당 될 때마다 소유자에 게 전자 메일 또는 SMS 메시지를 전송 하는 것이 좋습니다. 전자 메일 또는 SMS 서비스를 사용할 수 없는 경우에 다른 모든 작업을 처리할 수 있으며 전자 메일/SMS 메시지를 보내기 위한 별도 큐에 메시지를 입력 한 다음 수 있습니다.

이전에 효과적인 SLA가 Web Apps &times; 저장소 &times; SQL Database = 99.7%입니다. (참조 [디자인 장애를 견딜 수](design-to-survive-failures.md).)

큐를 사용 하도록 앱을 변경 하는 경우 복합 99.8%의 SLA에 대 한 웹 프런트 엔드 웹 앱 및 저장소에 대해서만 달라 집니다. (참고는 큐의 일부인 Azure 저장소 서비스에서 blob 저장소와 동일한 SLA를 포함 합니다.)

99.8% 보다 더 필요한 경우에 두 개의 다른 지역의 두 개의 큐를 만들 수 있습니다. 보조 복제본으로 주 고 다른 하나를 지정 합니다. 앱을 장애 조치할 보조 큐에 기본 큐를 사용할 수 없는 경우. 둘 다 사용할 수 없게 동시 가능성이 매우 낮습니다.

## <a name="rate-leveling-and-independent-scaling"></a>속도 평준화 하 고 독립적인 크기 조정

큐가 이라는 것에 유용 *평준화 속도* 하거나 *부하 평준화*합니다.

웹 앱에 트래픽이 갑자기 많은 취약 많습니다. 자동 크기 조정을 자동으로 증가 된 웹 트래픽을 처리 하도록 웹 서버를 추가 하려면를 사용 하는 동안 자동 크기 조정은 부하에 갑작스러운 스파이크를 처리할 만큼 신속 하 게 대응할 수 못할 수 있습니다. 웹 서버를 큐에 메시지를 작성 하 여 수행 해야 하는 작업의 일부는 오프 로드할 수, 하는 경우 더 많은 트래픽을 처리할 수 있도록 합니다. 그런 다음 백 엔드 서비스를 큐에서 메시지 읽기 하 고 처리할 수 있습니다. 큐의 깊이 늘리거나 수신 부하가 변경 됨.

대부분의 백 엔드 서비스에 오프 로드 시간이 오래 걸리는 작업을 사용 하 여 웹 계층의 트래픽이 갑자기 치 쉽게 응답할 수 있습니다. 및 모든 지정 된 양의 트래픽이 적은 웹 서버에서 처리할 수 있으므로 비용을 절약 합니다.

확장할 수 있습니다 웹 계층 및 백 엔드 서비스를 독립적으로 합니다. 예를 들어, 하나의 서버 큐 메시지 처리 되지만 웹 서버 3 해야 할 수 있습니다. 또는 백 엔드 서버를 더 계산 집약적 작업을 백그라운드에서 실행 중인 경우 해야 할 수 있습니다.

![](queue-centric-work-pattern/_static/image3.png)

자동 크기 조정 뿐만 아니라 웹 계층 백 엔드 서비스를 사용 하 여 작동합니다. 확장할 수도 있고 백 엔드 Vm의 CPU 사용량을 기준으로 큐에 작업을 처리 하는 Vm의 수를 축소할 수 있습니다. 또는 큐에 있는 항목 수에 따라 자동으로 조정할 수 있습니다. 예를 들어 10 개 항목을 큐에 유지 되도록 자동 크기 조정을 알려줄 수 있습니다. 큐 항목 수가 10 개 있으면 자동 크기 조정 Vm을 추가 합니다. 이러한 캐치 업 하는 방법, 자동 크기 조정은 추가 Vm을 해체입니다.

## <a name="adding-queues-to-the-fix-it-application"></a>추가 문제를 해결 하려면 큐에 대기 시키는 응용 프로그램

큐 패턴을 구현 하려면 Fix It 응용 프로그램에 두 가지 사항을 변경 해야 합니다.

- 사용자가 새 수정 작업을 제출 하면 데이터베이스에 작성 하는 대신 큐에서 작업을 배치 합니다.
- 큐의 메시지를 처리 하는 백 엔드 서비스를 만듭니다.

큐를 사용 합니다 [Azure Queue Storage 서비스](https://www.windowsazure.com/develop/net/how-to-guides/queue-service/)합니다. 사용 하는 다른 옵션도 [Azure Service Bus](https://docs.microsoft.com/azure/service-bus/)합니다.

큐 서비스를 사용 하 여 결정을 큐에 메시지를 받고 보내는 데 앱을 요구 하는 방법을 고려 합니다.

- 협동 생산자와 경쟁 소비자에 게 경우에 Azure Queue Storage 서비스를 사용 하 여 하는 것이 좋습니다. "협력 생산자" 큐를 여러 프로세스 메시지를 추가 하는 것을 의미 합니다. 여러 프로세스를 처리 하는 데 큐 메시지를 끌어오는 있지만 하나 "소비자입니다."만 지정 된 모든 메시지를 처리할 수 없음을 의미 하는 "경쟁 소비자" 단일 큐를 사용 하 여 가져올 수 있습니다 보다 더 많은 처리량을 할 경우 추가 큐 및/또는 추가 저장소 계정을 사용 합니다.
- 필요한 경우는 [게시/구독 모델](http://en.wikipedia.org/wiki/Publish/subscribe), Azure Service Bus 큐를 사용 하는 것이 좋습니다.

Fix It 응용 프로그램에 협동 생산자와 경쟁 소비자 모델을 맞춥니다.

다른 고려 사항은 응용 프로그램의 가용성입니다. Queue Storage 서비스를 사용 하면 SLA에 영향을 주지 사용 되므로 blob storage에 대해 사용 되는 동일한 서비스의 일부인 합니다. Azure Service Bus는 자체 SLA 사용 하 여 별도 서비스입니다. Service Bus 큐를 사용 하는 경우 추가 SLA 백분율을 고려할 필요가 및 복합 SLA는 작아야 합니다. 큐 서비스를 선택할 때 사용자가 선택한 응용 프로그램 가용성에 영향을 이해할 수 있는지 확인 합니다. 자세한 내용은 참조는 [리소스](#resources) 섹션입니다.

## <a name="creating-queue-messages"></a>큐 메시지 만들기

Fix It 작업을 큐에 삽입할 웹 프런트 엔드는 다음 단계를 수행 합니다.

1. 만들기는 [CloudQueueClient](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueueclient.aspx) 인스턴스. `CloudQueueClient` 큐 서비스에 대 한 요청을 실행 하려면 인스턴스가 사용 됩니다.
2. 아직 존재 하지 않는 경우에 큐를 만듭니다.
3. Fix It 작업을 serialize 합니다.
4. 호출 [CloudQueue.AddMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.addmessageasync.aspx) 큐 메시지를 배치 하 합니다.

생성자에서이 작업을 사용 하도록 하겠습니다 및 `SendMessageAsync` 메서드의 새 `FixItQueueManager` 클래스입니다.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample1.cs?highlight=11-12,16,18-25)]

여기에서는 사용 합니다 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 를 JSON 형식으로 fixit를 serialize 하는 라이브러리. 원하는 어떤 직렬화 방법을 사용할 수 있습니다. JSON을 사용 하면 XML 보다 정보가 덜 자세 되면서 사람이 인식할 수 있는 이점이 있습니다.

프로덕션 품질의 코드는 오류 처리 논리를 추가, 데이터베이스를 사용할 수 없게 하는 경우 일시 중지, 복구를 더욱 명확 하 게 처리, 응용 프로그램 시작 시 큐 만들기 및 관리 "[포이즌" 메시지](https://msdn.microsoft.com/library/ms789028(v=vs.110).aspx)합니다. (포이즌 메시지는 어떤 이유로 처리할 수 없는 메시지는 합니다. 원하지 포이즌 메시지는 처리, 실패, 다시 시도, 실패 및 등을 지속적으로 시도 하는 작업자 역할이 있는 큐에 저장 합니다.)

프런트 엔드 MVC 응용 프로그램에서 새 작업을 만드는 코드를 업데이트 해야 합니다. 작업 저장소에 배치 하는 대신 호출 된 `SendMessageAsync` 위에 표시 된 메서드.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample2.cs?highlight=10)]

## <a name="processing-queue-messages"></a>큐 메시지를 처리합니다.

큐의 메시지를 처리 하려면 백 엔드 서비스를 만들어 보겠습니다. 백 엔드 서비스에는 다음 단계를 수행 하는 무한 루프로 실행 됩니다.

1. 큐에서 다음 메시지를 가져옵니다.
2. Fix It 작업에 메시지를 deserialize 합니다.
3. 데이터베이스에 수정 작업을 작성 합니다.

백 엔드 서비스를 호스트 하려면 포함 하는 Azure 클라우드 서비스를 만듭니다는 *작업자 역할*입니다. 작업자 역할을 백 엔드 처리를 수행할 수 있는 하나 이상의 Vm으로 구성 됩니다. 이러한 Vm에서 실행 되는 코드는 사용 가능 해지면 큐에서 메시지를 끌어옵니다. 각 메시지에 대해에서는 JSON 페이로드를 deserialize 하 고 이전 웹 계층에서에서 사용 하는 동일한 저장소를 사용 하 여 데이터베이스에 수정이 작업 엔터티 인스턴스를 작성 합니다.

다음 단계를 작업자를 추가 하는 방법에는 표준 웹 프로젝트가 있는 솔루션에 역할 프로젝트를 보여 줍니다. Fix It 프로젝트에서 다운로드할 수 있는 다음이 단계를 아직 되었습니다.

먼저 클라우드 서비스 프로젝트를 Visual Studio 솔루션에 추가 합니다. 솔루션을 마우스 오른쪽 단추로 클릭 **추가**, 한 다음 **새 프로젝트**합니다. 왼쪽된 창에서 확장 **Visual C#** 선택한 **클라우드**합니다.

[![](queue-centric-work-pattern/_static/image5.png)](queue-centric-work-pattern/_static/image4.png)

에 **새 Azure 클라우드 서비스** 대화 상자에서 확장 된 **Visual C#** 왼쪽된 창에서 노드. 선택 **작업자 역할** 오른쪽 화살표 아이콘을 클릭 합니다.

![](queue-centric-work-pattern/_static/image6.png)

(추가할 수도 있습니다는 한 *웹 역할*입니다. 우리는 Fix It는 Azure 웹 사이트에서를 실행 하는 대신 동일한 클라우드 서비스에서 프런트 엔드는 실행할 수 있습니다. 프런트 엔드 및 백 엔드 간의 연결을 쉽게 조정할 수 있도록 몇 가지 장점이입니다. 그러나이 데모를 간단히 유지 하기는 Azure App Service 웹 앱에 프런트 엔드를 유지 하 고만 클라우드 서비스에서 백 엔드를 실행 합니다.)

작업자 역할에 기본 이름이 할당 됩니다. 이름을 변경 하 고 오른쪽 창에서 작업자 역할 위에 마우스를 가져가고 연필 아이콘을 클릭 합니다.

![](queue-centric-work-pattern/_static/image7.png)

클릭 **확인** 대화 상자를 완료 합니다. Visual Studio 솔루션에 프로젝트가 추가 됩니다.

- 구성 정보를 포함 하 여 클라우드 서비스를 정의 하는 Azure 프로젝트.
- 작업자 역할을 정의 하는 작업자 역할 프로젝트.

![](queue-centric-work-pattern/_static/image8.png)

자세한 내용은 참조 하세요. [Visual Studio를 사용 하 여 Azure 프로젝트 만들기.](https://msdn.microsoft.com/library/windowsazure/ee405487.aspx)

작업자 역할 내에서 폴링할 메시지에 대 한 호출 하 여 합니다 `ProcessMessageAsync` 메서드는 `FixItQueueManager` 살펴본는 클래스입니다.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample3.cs?highlight=25)]

`ProcessMessagesAsync` 메서드 메시지 대기 중이 있는지 확인 합니다. 메시지를 deserialize 할 경우 하나는 `FixItTask` 엔터티 데이터베이스에서 엔터티를 저장 합니다. 큐가 비어 있을 때까지 반복 합니다.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample4.cs)]

큐 메시지에는 작은 트랜잭션이 발생에 대 한 폴링이 부과할 처리 되도록 대기 중인 메시지가 없는 경우 작업자 역할의 `RunAsync` 메서드는 초 기다렸다가 폴링하기 전에 다시 호출 하 여 `Task.Delay(1000)`입니다.

웹 프로젝트에서 비동기 코드를 추가 합니다. 자동으로 성능을 향상 시킬 수 IIS에서 제한 된 스레드 풀을 관리 하기 때문입니다. 작업자 역할 프로젝트의 경우는 아닙니다. 작업자 역할의 확장성 향상을 위해 다중 스레드 코드를 작성 하거나 비동기 코드를 사용 하 여 구현할 수 있습니다 [병렬 프로그래밍](https://msdn.microsoft.com/library/ff963553.aspx)합니다. 샘플 병렬 프로그래밍을 구현 하지 않지만 병렬 프로그래밍을 구현할 수 있도록 비동기 코드를 만드는 방법을 보여 줍니다.

## <a name="summary"></a>요약

이 챕터에 큐 중심 작업 패턴을 구현 하 여 응용 프로그램 응답성, 안정성 및 확장성을 개선 하는 방법을 살펴보았습니다.

이 전자책에서 다룹니다 13 패턴의 마지막 하지만 물론 많은 패턴도 있습니다 이며 도움이 될 수 있는 사례 성공적인 클라우드 앱을 빌드합니다. 합니다 [마지막 챕터](more-patterns-and-guidance.md) 13 이러한 패턴에 포함 된 하지 않은 항목에 대 한 리소스에 대 한 링크를 제공 합니다.

<a id="resources"></a>
## <a name="resources"></a>자료

큐에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

설명서:

- [Microsoft Azure Storage 큐 1 부: Getting Started](http://justazure.com/microsoft-azure-storage-queues-part-1-getting-started/)합니다. 로마 Schacherl 문서.
- [백그라운드 작업 실행](https://msdn.microsoft.com/library/ff803365.aspx), 5 장을 [이동 응용 프로그램을 클라우드로 3rd Edition](https://msdn.microsoft.com/library/ff728592.aspx) Microsoft Patterns and Practices에서 합니다. (특히 섹션 ["를 사용 하 여 Azure Storage 큐"](https://msdn.microsoft.com/library/ff803365.aspx#sec7).)
- [확장성 및 Azure에서 큐 기반 메시징 솔루션의 비용된 효율성을 극대화 하기 위한 모범 사례](https://msdn.microsoft.com/library/windowsazure/hh697709.aspx)합니다. Valery Mizonov 여 백서입니다.
- [Azure 큐와 Service Bus 큐 비교](https://msdn.microsoft.com/magazine/jj159884.aspx)합니다. MSDN Magazine 기사를 사용 하는 큐 서비스를 선택 하는 데 도움이 되는 추가 정보를 제공 합니다. 문서에 Service Bus ACS를 사용할 수 없을 때 SB 큐를 사용할 수 없습니다 것을 의미 하는 인증에 대 한 ACS에 종속 되어 있는지 설명 합니다. 그러나 문서 작성 된 이후 SB 바뀌었습니다 사용할 수 있도록 [SAS 토큰](https://msdn.microsoft.com/library/windowsazure/dn170477.aspx) ACS 하는 대신 합니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx)합니다. 비동기 메시징 입문서, 파이프 및 필터 패턴, 보상 트랜잭션 패턴, 경쟁 소비자 패턴, CQRS 패턴을 참조 하세요.
- [CQRS Journey](https://msdn.microsoft.com/library/jj554200)합니다. Microsoft Patterns and Practices CQRS에 대 한 전자책을 참고 합니다.

비디오:

- [FailSafe: 확장성, 복원 력 있는 클라우드 서비스를 만드는 데](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms에서 비디오 시리즈를 9 개 부분으로 구성 합니다. 고급 개념 및 아키텍처 원칙으로 실제 고객의 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 스토리를 사용 하 여 액세스 가능 하 고 흥미로운 방식으로 표시 합니다. 소개 하 고 Azure Storage 서비스 큐에 대 한 에피소드 5 35:13부터 참조 하세요.

> [!div class="step-by-step"]
> [이전](distributed-caching.md)
> [다음](more-patterns-and-guidance.md)
