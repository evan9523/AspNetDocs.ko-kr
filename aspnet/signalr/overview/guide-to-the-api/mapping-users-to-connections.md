---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: SignalR 사용자를 연결로 매핑 | 마이크로 소프트 문서
author: bradygaster
description: 이 항목에서는 사용자 및 해당 연결에 대한 정보를 유지하는 방법을 보여 주었습니다. 패트릭 플레처는이 주제를 작성하는 데 도움이. 이 항목에 사용된 소프트웨어 버전...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675780"
---
# <a name="mapping-signalr-users-to-connections"></a>SignalR 사용자를 연결에 매핑

[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 항목에서는 사용자 및 해당 연결에 대한 정보를 유지하는 방법을 보여 주었습니다.
>
> 패트릭 플레처는이 주제를 작성하는 데 도움이.
>
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에 사용된 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - 시그널R 버전 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
>
> 이전 버전의 SignalR에 대한 자세한 내용은 [SignalR 이전 버전을](../older-versions/index.md)참조하십시오.
>
> ## <a name="questions-and-comments"></a>질문 및 의견
>
> 이 자습서를 어떻게 좋아했는지, 그리고 페이지 하단의 댓글에서 개선할 수 있는 내용에 대한 피드백을 남겨주세요. 당신은 튜토리얼과 직접 관련이없는 질문이있는 경우, 당신은 [ASP.NET SignalR 포럼에](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 게시하거나 [StackOverflow.com](http://stackoverflow.com/).

## <a name="introduction"></a>소개

허브에 연결하는 각 클라이언트는 고유 연결 ID를 전달합니다. 허브 컨텍스트의 `Context.ConnectionId` 속성에서 이 값을 검색할 수 있습니다. 응용 프로그램에서 사용자를 연결 ID에 매핑하고 해당 매핑을 유지해야 하는 경우 다음 중 하나를 사용할 수 있습니다.

- [사용자 ID 공급자(SignalR 2)](#IUserIdProvider)
- 사전과 같은 [메모리 내 저장소](#inmemory)
- [각 사용자에 대한 신호 R 그룹](#groups)
- 데이터베이스 테이블 또는 Azure 테이블 [저장소와](#database)같은 영구 외부 저장소

이러한 각 구현은 이 항목에 나와 있습니다. 의 `OnConnected`에서 `OnDisconnected`및 `OnReconnected` 메서드를 `Hub` 사용하여 사용자 연결 상태를 추적합니다.

응용 프로그램에 가장 적합한 방법은 다음을 기반으로 합니다.

- 응용 프로그램을 호스팅하는 웹 서버 의 수입니다.
- 현재 연결된 사용자 목록을 받아야 하는지 여부입니다.
- 응용 프로그램 또는 서버가 다시 시작될 때 그룹 및 사용자 정보를 유지해야 하는지 여부입니다.
- 외부 서버 호출 대기 시간이 문제인지 여부입니다.

다음 표에서는 이러한 고려 사항에 적합한 방법을 보여 주며 있습니다.

|  | 두 개 이상의 서버 | 현재 연결된 사용자 목록 받기 | 다시 시작한 후 정보 유지 | 최적의 성능 |
| --- | --- | --- | --- | --- |
| 사용자 ID 공급자 | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| 메모리 내 |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| 단일 사용자 그룹 | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| 영구, 외부 | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID 공급자

이 기능을 사용하면 사용자가 새 인터페이스 IUserIdProvider를 통해 IRequest를 기반으로 하는 userId를 지정할 수 있습니다.

**The IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

기본적으로 사용자의 이름을 `IPrincipal.Identity.Name` 사용자 이름으로 사용하는 구현이 있습니다. 이를 변경하려면 응용 프로그램이 `IUserIdProvider` 시작될 때 전역 호스트에 구현을 등록하십시오.

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

허브 내에서 다음 API를 통해 이러한 사용자에게 메시지를 보낼 수 있습니다.

**특정 사용자에게 메시지 보내기**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>인메모리 스토리지

다음 예제에서는 메모리에 저장된 사전에서 연결 및 사용자 정보를 유지하는 방법을 보여 주며 있습니다. 사전은 연결 `HashSet` ID를 저장하는 데 a를 사용합니다. 사용자는 언제든지 SignalR 응용 프로그램에 두 개 이상의 연결을 가질 수 있습니다. 예를 들어 여러 장치를 통해 연결하거나 두 개 이상의 브라우저 탭을 통해 연결된 사용자에게는 두 개 이상의 연결 ID가 있습니다.

응용 프로그램이 종료되면 모든 정보가 손실되지만 사용자가 연결을 다시 설정하면 다시 채워집니다. 각 서버에 별도의 연결 컬렉션이 있기 때문에 환경에 두 개 이상의 웹 서버가 포함되어 있으면 메모리 내 저장소가 작동하지 않습니다.

첫 번째 예제에서는 사용자 연결을 연결하는 것을 관리하는 클래스를 보여 둡니다. HashSet의 키는 사용자 이름입니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

다음 예제에서는 허브에서 연결 매핑 클래스를 사용하는 방법을 보여 주며 있습니다. 클래스의 인스턴스는 변수 이름에 `_connections`저장됩니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>단일 사용자 그룹

각 사용자에 대한 그룹을 만든 다음 해당 사용자에게만 도달하려는 경우 해당 그룹에 메시지를 보낼 수 있습니다. 각 그룹의 이름은 사용자의 이름입니다. 사용자에게 두 개 이상의 연결이 있는 경우 각 연결 ID가 사용자의 그룹에 추가됩니다.

사용자가 연결을 끊을 때 그룹에서 사용자를 수동으로 제거해서는 안 됩니다. 이 작업은 SignalR 프레임워크에 의해 자동으로 수행됩니다.

다음 예제에서는 단일 사용자 그룹을 구현하는 방법을 보여 주며 있습니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>영구, 외부 스토리지

이 항목에서는 연결 정보를 저장하기 위해 데이터베이스 또는 Azure 테이블 저장소를 사용하는 방법을 보여 주며 있습니다. 이 방법은 각 웹 서버가 동일한 데이터 리포지토리와 상호 작용할 수 있기 때문에 여러 웹 서버가 있는 경우에 작동합니다. 웹 서버가 작동을 중지하거나 응용 프로그램이 `OnDisconnected` 다시 시작되면 메서드가 호출되지 않습니다. 따라서 데이터 리포지토리에 더 이상 유효하지 않은 연결 ID에 대한 레코드가 있을 수 있습니다. 이러한 분리된 레코드를 정리하려면 응용 프로그램과 관련된 기간 외부에서 만든 연결을 무효화할 수 있습니다. 이 섹션의 예제에는 연결이 만들어진 시기를 추적하는 값이 포함되어 있지만 백그라운드 프로세스로 수행하려고 할 수 있으므로 이전 레코드를 정리하는 방법을 표시하지 않습니다.

### <a name="database"></a>데이터베이스

다음 예제에서는 데이터베이스에서 연결 및 사용자 정보를 유지하는 방법을 보여 주며 있습니다. 모든 데이터 액세스 기술을 사용할 수 있습니다. 그러나 아래 예제에서는 엔터티 프레임 워크를 사용 하 여 모델을 정의 하는 방법을 보여 주어 있습니다. 이러한 엔터티 모델은 데이터베이스 테이블 및 필드에 해당합니다. 데이터 구조는 응용 프로그램의 요구 사항에 따라 크게 달라질 수 있습니다.

첫 번째 예제에서는 여러 연결 엔터티와 연결할 수 있는 사용자 엔터티를 정의하는 방법을 보여 주며 있습니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

그런 다음 허브에서 아래 표시된 코드로 각 연결 상태를 추적할 수 있습니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure 테이블 스토리지

다음 Azure 테이블 저장소 예제는 데이터베이스 예제와 유사합니다. Azure 테이블 저장소 서비스를 시작하는 데 필요한 모든 정보는 포함되지 않습니다. 자세한 내용은 [.NET 에서 테이블 저장소를 사용하는 방법을 참조하십시오.](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)

다음 예제에서는 연결 정보를 저장하기 위한 테이블 엔터티를 보여 주며 있습니다. 사용자 이름으로 데이터를 분할하고 연결 ID로 각 엔터티를 식별하므로 사용자는 언제든지 여러 연결을 가질 수 있습니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

허브에서 각 사용자의 연결 상태를 추적합니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
