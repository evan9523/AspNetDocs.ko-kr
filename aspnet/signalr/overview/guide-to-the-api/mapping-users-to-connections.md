---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: SignalR 사용자를 연결에 매핑 | Microsoft Docs
author: bradygaster
description: 이 항목에서는 사용자와 해당 연결에 대 한 정보를 유지 하는 방법을 보여 줍니다. Patrick Fletcher에서이 항목을 작성 하는 데 도움이 되었습니다. 이 항목에 사용 되는 소프트웨어 버전
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345419"
---
# <a name="mapping-signalr-users-to-connections"></a>SignalR 사용자를 연결에 매핑

[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 항목에서는 사용자와 해당 연결에 대 한 정보를 유지 하는 방법을 보여 줍니다.
>
> Patrick Fletcher에서이 항목을 작성 하는 데 도움이 되었습니다.
>
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 버전 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
>
> 이전 버전의 SignalR에 대 한 자세한 내용은 [SignalR 이전 버전](../older-versions/index.md)을 참조 하세요.
>
> ## <a name="questions-and-comments"></a>질문 및 설명
>
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.

## <a name="introduction"></a>소개

허브에 연결 하는 각 클라이언트는 고유한 연결 id를 전달 합니다. 허브 컨텍스트의 속성에서이 값을 검색할 수 있습니다 `Context.ConnectionId` . 응용 프로그램에서 사용자를 연결 id에 매핑하고 해당 매핑을 유지 해야 하는 경우 다음 중 하나를 사용할 수 있습니다.

- [사용자 ID 공급자 (SignalR 2)](#IUserIdProvider)
- 사전 같은 [메모리 내 저장소](#inmemory)
- [각 사용자에 대 한 SignalR 그룹](#groups)
- 데이터베이스 테이블 또는 Azure table storage와 같은 [영구 외부 저장소](#database)

이러한 각 구현은이 항목에 나와 있습니다. `OnConnected`클래스의, 및 메서드를 사용 하 여 `OnDisconnected` `OnReconnected` `Hub` 사용자 연결 상태를 추적 합니다.

응용 프로그램에 대 한 가장 좋은 방법은 다음에 따라 달라 집니다.

- 응용 프로그램을 호스팅하는 웹 서버의 수입니다.
- 현재 연결 된 사용자의 목록을 가져와야 하는지 여부입니다.
- 응용 프로그램 또는 서버를 다시 시작할 때 그룹 및 사용자 정보를 유지 해야 하는지 여부입니다.
- 외부 서버 호출의 대기 시간이 문제 인지 여부입니다.

다음 표에서는 이러한 고려 사항에 대해 작동 하는 방법을 보여 줍니다.

|  | 둘 이상의 서버 | 현재 연결 된 사용자 목록 가져오기 | 다시 시작한 후 정보 유지 | 최적의 성능 |
| --- | --- | --- | --- | --- |
| UserID 공급자 | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| 메모리 내 |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| 단일 사용자 그룹 | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| 영구, 외부 | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID 공급자

사용자는이 기능을 사용 하 여 새 interface IUserIdProvider를 통해 IRequest를 기반으로 하는 사용자 Id를 지정할 수 있습니다.

**IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

기본적으로 사용자의 사용자 이름으로 사용자를 사용 하는 구현이 있습니다 `IPrincipal.Identity.Name` . 이를 변경 하려면 `IUserIdProvider` 응용 프로그램이 시작 될 때의 구현을 전역 호스트에 등록 합니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

허브 내에서 다음 API를 통해 이러한 사용자에 게 메시지를 보낼 수 있습니다.

**특정 사용자에 게 메시지 보내기**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>메모리 내 저장소

다음 예에서는 메모리에 저장 된 사전에 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다. 사전은를 사용 하 여 `HashSet` 연결 id를 저장 합니다. 사용자는 언제 든 지 SignalR 응용 프로그램에 대 한 연결을 둘 이상 가질 수 있습니다. 예를 들어 여러 장치 또는 둘 이상의 브라우저 탭을 통해 연결 된 사용자에 게는 둘 이상의 연결 id가 있습니다.

응용 프로그램이 종료 되 면 모든 정보가 손실 되지만 사용자가 연결을 다시 설정 하면 다시 채워집니다. 각 서버에 별도의 연결 컬렉션이 있기 때문에 환경에 둘 이상의 웹 서버가 포함 된 경우에는 메모리 내 저장소가 작동 하지 않습니다.

첫 번째 예제에서는 연결에 대 한 사용자 매핑을 관리 하는 클래스를 보여 줍니다. HashSet의 키는 사용자의 이름이 됩니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

다음 예제에서는 허브에서 연결 매핑 클래스를 사용 하는 방법을 보여 줍니다. 클래스의 인스턴스는 변수 이름에 저장 됩니다 `_connections` .

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>단일 사용자 그룹

각 사용자에 대 한 그룹을 만든 다음 해당 사용자 에게만 도달 하려는 경우 해당 그룹에 메시지를 보낼 수 있습니다. 각 그룹의 이름은 사용자의 이름입니다. 사용자가 두 개 이상의 연결을 사용 하는 경우 각 연결 id는 사용자 그룹에 추가 됩니다.

사용자가 연결을 끊을 때 그룹에서 사용자를 수동으로 제거 하면 안 됩니다. 이 작업은 SignalR 프레임 워크에서 자동으로 수행 됩니다.

다음 예제에서는 단일 사용자 그룹을 구현 하는 방법을 보여 줍니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>영구, 외부 저장소

이 항목에서는 데이터베이스 또는 Azure table storage를 사용 하 여 연결 정보를 저장 하는 방법을 보여 줍니다. 이 방법은 각 웹 서버가 동일한 데이터 저장소와 상호 작용할 수 있기 때문에 여러 웹 서버를 사용 하는 경우 작동 합니다. 웹 서버의 작동이 중지 되거나 응용 프로그램이 다시 시작 `OnDisconnected` 되 면 메서드가 호출 되지 않습니다. 따라서 데이터 리포지토리에 더 이상 유효 하지 않은 연결 id 레코드가 있을 수 있습니다. 이러한 분리 된 레코드를 정리 하려면 응용 프로그램과 관련 된 시간 범위 밖에 서 만들어진 모든 연결을 무효화할 수 있습니다. 이 섹션의 예에는 연결을 만들 때 추적 하는 값이 포함 되어 있지만이를 백그라운드 프로세스로 수행 하려는 경우에는 오래 된 레코드를 정리 하는 방법은 표시 되지 않습니다.

### <a name="database"></a>데이터베이스

다음 예에서는 데이터베이스에서 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다. 모든 데이터 액세스 기술을 사용할 수 있습니다. 그러나 다음 예에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다. 이러한 엔터티 모델은 데이터베이스 테이블 및 필드에 해당 합니다. 데이터 구조는 응용 프로그램의 요구 사항에 따라 크게 다를 수 있습니다.

첫 번째 예제에서는 많은 연결 엔터티와 연결 될 수 있는 사용자 엔터티를 정의 하는 방법을 보여 줍니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

그런 다음 허브에서 아래와 같은 코드를 사용 하 여 각 연결의 상태를 추적할 수 있습니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure 테이블 스토리지

다음 Azure table storage 예는 데이터베이스 예제와 비슷합니다. Azure Table Storage 서비스를 시작 하는 데 필요한 일부 정보는 포함 되어 있지 않습니다. 자세한 내용은 [.net에서 테이블 저장소를 사용 하는 방법을](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)참조 하세요.

다음 예에서는 연결 정보를 저장 하기 위한 테이블 엔터티를 보여 줍니다. 사용자 이름으로 데이터를 분할 하 고 각 엔터티를 연결 id로 식별 하므로 사용자는 언제 든 지 여러 연결을 사용할 수 있습니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

허브에서 각 사용자의 연결 상태를 추적 합니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
