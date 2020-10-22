---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: '자습서: SignalR 2를 사용 하 여 서버 브로드캐스트 | Microsoft Docs'
author: tdykstra
description: 이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345600"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>자습서: SignalR 2를 사용 하 여 서버 브로드캐스트

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

이 자습서에서는 ASP.NET SignalR 2를 사용 하 여 서버 브로드캐스트 기능을 제공 하는 웹 응용 프로그램을 만드는 방법을 보여 줍니다. 서버 브로드캐스트는 서버에서 클라이언트로 전송 되는 통신을 시작 하는 것을 의미 합니다.

이 자습서에서 만들 응용 프로그램은 서버 브로드캐스트 기능을 위한 일반적인 시나리오인 주식 시세 표시기를 시뮬레이션 합니다. 정기적으로 서버는 주식 가격을 임의로 업데이트 하 고 연결 된 모든 클라이언트에 업데이트를 브로드캐스트합니다. 브라우저에서 **변경** 및 열의 숫자 및 기호는 **%** 서버의 알림에 대 한 응답으로 동적으로 변경 됩니다. 동일한 URL에 대 한 추가 브라우저를 열 경우 모두 동일한 데이터 및 동일한 데이터 변경 내용을 동시에 표시 합니다.

![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image1.png)

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 프로젝트 만들기
> * 서버 코드 설정
> * 서버 코드 검사
> * 클라이언트 코드 설정
> * 클라이언트 코드 검사
> * 애플리케이션 테스트
> * 로깅 사용

> [!IMPORTANT]
> 응용 프로그램을 빌드하는 단계를 수행 하지 않으려면 비어 있는 새 ASP.NET 웹 응용 프로그램 프로젝트에 SignalR 패키지를 설치 하면 됩니다. 이 자습서의 단계를 수행 하지 않고 NuGet 패키지를 설치 하는 경우 *readme.txt* 파일의 지침을 따라야 합니다. 패키지를 실행 하려면 설치 된 패키지에서 메서드를 호출 하는 OWIN startup 클래스를 추가 해야 `ConfigureSignalR` 합니다. OWIN startup 클래스를 추가 하지 않으면 오류가 표시 됩니다. 이 문서의 [StockTicker 샘플 설치](#install-the-stockticker-sample) 섹션을 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

* **ASP.NET 및 웹 개발** 워크로드가 있는 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="create-the-project"></a>프로젝트 만들기

이 섹션에서는 Visual Studio 2017을 사용 하 여 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 줍니다.

1. Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.

    ![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. **새 ASP.NET 웹 응용 프로그램-SignalR. StockTicker** 창에서 선택 된 **상태로 두고** **확인**을 선택 합니다.

## <a name="set-up-the-server-code"></a>서버 코드 설정

이 섹션에서는 서버에서 실행 되는 코드를 설정 합니다.

### <a name="create-the-stock-class"></a>스톡 클래스 만들기

먼저 주식 정보를 저장 하 고 전송 하는 데 사용할 *스톡* 모델 클래스를 만듭니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **클래스**추가를 선택 합니다.

1. 클래스 이름을 *스톡* 으로 만들고 프로젝트에 추가 합니다.

1. *Stock.cs* 파일의 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    주식을 만들 때 설정 하는 두 가지 속성은 `Symbol` (예: MSFT For Microsoft) 및 `Price` 입니다. 다른 속성은 설정 하는 방법과 시기에 따라 달라 집니다 `Price` . 처음 설정 하는 경우 `Price` 값이로 전파 `DayOpen` 됩니다. 그런 다음를 설정 하면 `Price` 앱에서 `Change` 와의 `PercentChange` 차이에 따라 및 속성 값을 계산 합니다 `Price` `DayOpen` .

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>StockTickerHub 및 StockTicker 클래스 만들기

SignalR Hub API를 사용 하 여 서버와 클라이언트 간의 상호 작용을 처리 합니다. `StockTickerHub`SignalR 클래스에서 파생 되는 클래스는 `Hub` 클라이언트의 수신 연결 및 메서드 호출을 처리 합니다. 또한 주식 데이터를 유지 관리 하 고 개체를 실행 해야 `Timer` 합니다. `Timer`개체는 클라이언트 연결과 무관 하 게 가격 업데이트를 주기적으로 트리거합니다. 허브가 일시적 이기 때문에 클래스에 이러한 함수를 배치할 수 없습니다 `Hub` . 앱은 `Hub` 클라이언트에서 서버로의 연결과 같은 허브의 각 태스크에 대 한 클래스 인스턴스를 만듭니다. 따라서 주식 데이터를 유지 하 고, 가격을 업데이트 하 고, 가격 업데이트를 브로드캐스팅하는 메커니즘이 별도의 클래스에서 실행 되어야 합니다. 클래스의 이름을로 `StockTicker` 합니다.

![StockTicker에서 브로드캐스팅](tutorial-server-broadcast-with-signalr/_static/image3.png)

클래스의 인스턴스 하나를 서버에서 실행 하려는 경우에만 `StockTicker` 각 인스턴스에서 singleton 인스턴스로 참조를 설정 해야 `StockTickerHub` `StockTicker` 합니다. `StockTicker`클래스는 스톡 데이터를 포함 하 고 업데이트를 트리거 하지만 클래스가 아니라 클라이언트에 브로드캐스트합니다 `StockTicker` `Hub` . `StockTicker`클래스는 SignalR Hub 연결 컨텍스트 개체에 대 한 참조를 가져와야 합니다. 그런 다음 SignalR 연결 컨텍스트 개체를 사용 하 여 클라이언트에 브로드캐스트할 수 있습니다.

#### <a name="create-stocktickerhubcs"></a>StockTickerHub.cs 만들기

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **새 항목**추가를 선택 합니다.

1. **새 항목 추가-SignalR. StockTicker**에서 **설치 됨**  >  **Visual c #**  >  **웹**  >  **SignalR** 를 선택한 다음 **SignalR Hub 클래스 (v2)** 를 선택 합니다.

1. 클래스 이름을 *StockTickerHub* 로 추가 하 고 프로젝트에 추가 합니다.

    이 단계에서는 *StockTickerHub.cs* 클래스 파일을 만듭니다. 동시에 SignalR를 지 원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가 합니다.

1. *StockTickerHub.cs* 파일의 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. 파일을 저장합니다.

앱은 [허브](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클래스를 사용 하 여 클라이언트가 서버에서 호출할 수 있는 메서드를 정의 합니다. 메서드 하나를 정의 하 고 있습니다 `GetAllStocks()` . 클라이언트는 처음 서버에 연결할 때이 메서드를 호출 하 여 현재 가격으로 모든 주식의 목록을 가져옵니다. 메서드는 `IEnumerable<Stock>` 메모리에서 데이터를 반환 하기 때문에 동기적으로 실행 하 고 반환할 수 있습니다.

데이터베이스 조회 나 웹 서비스 호출과 같이 대기와 관련 된 작업을 수행 하 여 메서드가 데이터를 가져와야 하는 경우 `Task<IEnumerable<Stock>>` 에는를 반환 값으로 지정 하 여 비동기 처리를 사용 하도록 설정 합니다. 자세한 내용은 [ASP.NET SignalR HUBS API 가이드-서버-비동기적으로 실행 하는 경우](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)를 참조 하세요.

`HubName`특성은 앱이 클라이언트의 JavaScript 코드에서 허브를 참조 하는 방법을 지정 합니다. 클라이언트의 기본 이름은이 특성을 사용 하지 않는 경우 클래스 이름의 camelCase 버전입니다 .이 경우에는 `stockTickerHub` 입니다.

나중에 클래스를 만들 때 `StockTicker` 앱은 정적 속성에 해당 클래스의 단일 인스턴스를 만듭니다 `Instance` . 의 singleton 인스턴스는 `StockTicker` 연결 하거나 연결을 끊는 클라이언트 수에 관계 없이 메모리에 있습니다. 이 인스턴스는 `GetAllStocks()` 메서드가 현재 주식 정보를 반환 하는 데 사용 하는 것입니다.

#### <a name="create-stocktickercs"></a>StockTicker.cs 만들기

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **클래스**추가를 선택 합니다.

1. 클래스 이름을 *StockTicker* 로 추가 하 고 프로젝트에 추가 합니다.

1. *StockTicker.cs* 파일의 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

모든 스레드가 동일한 StockTicker 코드 인스턴스를 실행 하므로 StockTicker 클래스는 스레드로부터 안전 해야 합니다.

### <a name="examine-the-server-code"></a>서버 코드 검사

서버 코드를 살펴보면 앱이 작동 하는 방식을 이해 하는 데 도움이 됩니다.

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>단일 인스턴스를 정적 필드에 저장

코드는 `_instance` `Instance` 클래스의 인스턴스를 사용 하 여 속성을 백업 하는 정적 필드를 초기화 합니다. 생성자는 전용 이므로 앱에서 만들 수 있는 클래스의 유일한 인스턴스입니다. 앱은 필드에 [초기화 지연을](/dotnet/framework/performance/lazy-initialization) 사용 합니다 `_instance` . 성능상의 이유로는 그렇지 않습니다. 인스턴스를 만드는 것은 스레드로부터 안전한 지 확인 하는 것입니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

클라이언트가 서버에 연결할 때마다 별도의 스레드에서 실행 되는 StockTickerHub 클래스의 새 인스턴스는 `StockTicker.Instance` 이전에 클래스에서 살펴본 것 처럼 정적 속성에서 StockTicker singleton 인스턴스를 가져옵니다 `StockTickerHub` .

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>ConcurrentDictionary에 주식 데이터 저장

생성자는 `_stocks` 일부 샘플 재고 데이터를 사용 하 여 컬렉션을 초기화 하 고 `GetAllStocks` 주식을 반환 합니다. 앞에서 살펴본 것 처럼이 주식 컬렉션은 `StockTickerHub.GetAllStocks` `Hub` 클라이언트가 호출할 수 있는 클래스의 서버 메서드인에 의해 반환 됩니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

스톡 컬렉션은 스레드 보안을 위해 [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) 형식으로 정의 됩니다. 또는 [사전](https://msdn.microsoft.com/library/xfhwa508.aspx) 개체를 사용 하 고 변경할 때 사전을 명시적으로 잠글 수 있습니다.

이 샘플 응용 프로그램의 경우 응용 프로그램 데이터를 메모리에 저장 하 고 앱이 인스턴스를 삭제할 때 데이터를 잃지는 것이 좋습니다  `StockTicker` . 실제 응용 프로그램에서는 데이터베이스와 같은 백 엔드 데이터 저장소를 사용 합니다.

#### <a name="periodically-updating-stock-prices"></a>정기적으로 주식 가격 업데이트

생성자는 `Timer` 임의 기준으로 주식 가격을 업데이트 하는 메서드를 주기적으로 호출 하는 개체를 시작 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer``UpdateStockPrices`상태 매개 변수에 null을 전달 하는를 호출 합니다. 앱은 가격을 업데이트 하기 전에 개체에 대 한 잠금을 사용 `_updateStockPricesLock` 합니다. 코드는 다른 스레드가 이미 가격을 업데이트 하 고 있는지 확인 한 다음 `TryUpdateStockPrice` 목록의 각 재고에 대해를 호출 합니다. `TryUpdateStockPrice`메서드는 주식 가격을 변경할 것인지 여부와 변경 되는 정도를 결정 합니다. 주가 변경 되 면 앱은 `BroadcastStockPrice` 를 호출 하 여 주식 가격 변경을 모든 연결 된 클라이언트에 브로드캐스트합니다.

`_updatingStockPrices` [일시적](https://msdn.microsoft.com/library/x13ttww7.aspx) 으로 지정 된 플래그는 스레드로부터 안전 하 게 보호 되도록 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

실제 응용 프로그램에서 메서드는 `TryUpdateStockPrice` 웹 서비스를 호출 하 여 가격을 조회 합니다. 이 코드에서 앱은 난수 생성기를 사용 하 여 임의로 변경을 수행 합니다.

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>StockTicker 클래스가 클라이언트에 브로드캐스트할 수 있도록 SignalR 컨텍스트 가져오기

여기서는 가격 변경이 개체에서 발생 하기 때문에 `StockTicker` `updateStockPrice` 연결 된 모든 클라이언트에서 메서드를 호출 해야 하는 개체입니다. 클래스에는 `Hub` 클라이언트 메서드를 호출 하기 위한 API가 있지만 `StockTicker` 클래스에서 파생 되지 않고 개체에 대 한 `Hub` 참조가 없습니다 `Hub` . 연결 된 클라이언트에 브로드캐스트하려면 클래스는 `StockTicker` 클래스에 대 한 SignalR context 인스턴스를 가져온 `StockTickerHub` 다음이를 사용 하 여 클라이언트에서 메서드를 호출 해야 합니다.

이 코드는 singleton 클래스 인스턴스를 만들고 해당 참조를 생성자에 전달 하 고 생성자가이를 속성에 배치 하는 경우 SignalR 컨텍스트에 대 한 참조를 가져옵니다 `Clients` .

컨텍스트를 한 번만 가져오려고 하는 두 가지 이유는 다음과 같습니다. 컨텍스트 가져오기 작업은 비용이 많이 들고, 한 번 가져오면 앱이 클라이언트에 전송 되는 메시지의 순서를 유지 하도록 할 수 있습니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

`Clients`컨텍스트의 속성을 가져와서 속성에 배치 `StockTickerClient` 하면 클래스에서와 동일 하 게 보이는 클라이언트 메서드를 호출 하는 코드를 작성할 수 있습니다 `Hub` . 예를 들어, 작성할 수 있는 모든 클라이언트에 브로드캐스트할 수 있습니다 `Clients.All.updateStockPrice(stock)` .

`updateStockPrice`에서 호출 하는 메서드가 `BroadcastStockPrice` 아직 존재 하지 않습니다. 나중에 클라이언트에서 실행 되는 코드를 작성할 때 추가 합니다. `updateStockPrice`가 동적 이므로이를 참조할 수 있습니다 `Clients.All` . 즉, 앱이 런타임에 식을 평가 합니다. 이 메서드 호출이 실행 되 면 SignalR는 메서드 이름과 매개 변수 값을 클라이언트에 보내고, 클라이언트에 라는 메서드가 있으면 `updateStockPrice` 앱은 해당 메서드를 호출 하 고 매개 변수 값을 전달 합니다.

`Clients.All` 모든 클라이언트에 보내기를 의미 합니다. SignalR는 보낼 클라이언트 또는 클라이언트 그룹을 지정 하는 다른 옵션을 제공 합니다. 자세한 내용은 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)를 참조 하세요.

### <a name="register-the-signalr-route"></a>SignalR 경로 등록

서버에서 가로채서 SignalR에 지시할 URL을 알고 있어야 합니다. 이렇게 하려면 OWIN startup 클래스를 추가 합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **새 항목**추가를 선택 합니다.

1. **새 항목 추가-SignalR. StockTicker** 에서 **설치 된**  >  **Visual c #**  >  **웹** 을 선택 하 고 **OWIN 시작 클래스**를 선택 합니다.

1. 클래스 이름을 *시작* 으로 하 고 **확인**을 선택 합니다.

1. *Startup.cs* 파일의 기본 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

이제 서버 코드를 설정 했습니다. 다음 섹션에서는 클라이언트를 설정 합니다.

## <a name="set-up-the-client-code"></a>클라이언트 코드 설정

이 섹션에서는 클라이언트에서 실행 되는 코드를 설정 합니다.

### <a name="create-the-html-page-and-javascript-file"></a>HTML 페이지 및 JavaScript 파일 만들기

HTML 페이지에 데이터가 표시 되 고 JavaScript 파일이 데이터를 구성 합니다.

#### <a name="create-stocktickerhtml"></a>StockTicker.html 만들기

먼저 HTML 클라이언트를 추가 합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **HTML 페이지**추가를 선택 합니다.

1. 파일 이름을 *StockTicker* 로 선택 하 고 **확인을**선택 합니다.

1. *StockTicker.html* 파일의 기본 코드를 다음 코드로 바꿉니다.

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML은 5 개의 열, 머리글 행 및 5 개 열 전체에 걸쳐 있는 단일 셀을 포함 하는 데이터 행을 포함 하는 테이블을 만듭니다. 데이터 행에 "로드 중 ..."이 표시 됩니다. 앱이 시작 되는 일시적입니다. JavaScript 코드는 해당 행을 제거 하 고 서버에서 검색 된 주식 데이터를 사용 하 여 해당 행을 추가 합니다.

    스크립트 태그는 다음을 지정 합니다.

    * JQuery 스크립트 파일입니다.

    * SignalR core 스크립트 파일입니다.

    * SignalR 프록시 스크립트 파일입니다.

    * 나중에 만들 StockTicker 스크립트 파일입니다.

    앱은 SignalR 프록시 스크립트 파일을 동적으로 생성 합니다. "/Signalr/hubs" URL을 지정 하 고 허브 클래스 (이 경우)의 메서드에 대 한 프록시 메서드를 정의 `StockTickerHub.GetAllStocks` 합니다. 원한다 면 [SignalR 유틸리티](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)를 사용 하 여이 JavaScript 파일을 수동으로 생성할 수 있습니다. 메서드 호출에서 동적 파일 생성을 사용 하지 않도록 설정 하는 것을 잊지 마세요 `MapHubs` .

1. **솔루션 탐색기**에서 **스크립트**를 확장 합니다.

    JQuery 및 SignalR에 대 한 스크립트 라이브러리는 프로젝트에 표시 됩니다.

    > [!IMPORTANT]
    > 패키지 관리자가 SignalR 스크립트의 최신 버전을 설치 합니다.

1. 프로젝트의 스크립트 파일 버전에 해당 하는 코드 블록의 스크립트 참조를 업데이트 합니다.

1. **솔루션 탐색기**에서 *StockTicker.html*을 마우스 오른쪽 단추로 클릭 한 다음 **시작 페이지로 설정**을 선택 합니다.

#### <a name="create-stocktickerjs"></a>StockTicker.js 만들기

이제 JavaScript 파일을 만듭니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **Add**  >  **JavaScript 파일**추가를 선택 합니다.

1. 파일 이름을 *StockTicker* 로 선택 하 고 **확인을**선택 합니다.

1. *StockTicker.js* 파일에 다음 코드를 추가 합니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>클라이언트 코드 검사

클라이언트 코드를 살펴보면 클라이언트 코드가 서버 코드와 상호 작용 하 여 앱이 작동 하도록 하는 방법을 배우는 데 도움이 됩니다.

#### <a name="starting-the-connection"></a>연결 시작

`$.connection` SignalR 프록시를 참조 합니다. 이 코드는 클래스의 프록시에 대 한 참조를 가져와 `StockTickerHub` `ticker` 변수에 넣습니다. 프록시 이름은 특성에 의해 설정 된 이름입니다 `HubName` .

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

모든 변수 및 함수를 정의한 후 파일의 마지막 코드 줄은 SignalR 함수를 호출 하 여 SignalR 연결을 초기화 합니다 `start` . `start`함수는 비동기적으로 실행 되 고 [jQuery 지연 된 개체](http://api.jquery.com/category/deferred-object/)를 반환 합니다. Done 함수를 호출 하 여 앱이 비동기 작업을 완료할 때 호출할 함수를 지정할 수 있습니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>모든 주식 가져오기

`init`함수는 `getAllStocks` 서버에서 함수를 호출 하 고 서버에서 반환 하는 정보를 사용 하 여 스톡 테이블을 업데이트 합니다. 서버에서 메서드 이름이 파스칼식 대/소문자를 사용 하는 경우에도 기본적으로 클라이언트에서 camelCasing를 사용 해야 합니다. CamelCasing 규칙은 개체가 아닌 메서드에만 적용 됩니다. 예를 들어, 또는가 `stock.Symbol` 아닌 and를 참조 `stock.Price` `stock.symbol` `stock.price` 합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

`init`메서드에서 응용 프로그램은를 호출 하 여 `formatStock` 개체의 속성 형식을 지정 하 `stock` 고,를 호출 하 여 `supplant` 변수의 자리 표시자를 `rowTemplate` `stock` 개체 속성 값으로 대체 하는 방식으로 서버에서 받은 각 스톡 개체의 테이블 행에 대 한 HTML을 만듭니다. 그러면 결과 HTML이 스톡 테이블에 추가 됩니다.

> [!NOTE]
> `init` `callback` 비동기 함수가 완료 된 후 실행 되는 함수로에 전달 하 여를 호출 `start` 합니다. `init`를 호출한 후 별도의 JavaScript 문으로 호출한 경우 `start` 함수는 시작 함수가 연결 설정을 완료할 때까지 기다리지 않고 즉시 실행 되기 때문에 실패 합니다. 이 경우 `init` 함수는 `getAllStocks` 앱이 서버 연결을 설정 하기 전에 함수를 호출 하려고 시도 합니다.

#### <a name="getting-updated-stock-prices"></a>업데이트 된 주식 가격

서버에서 주식 시세를 변경 하면 연결 된 클라이언트에서를 호출 합니다 `updateStockPrice` . 앱은 `stockTicker` 서버에서 호출할 수 있도록 프록시의 client 속성에 함수를 추가 합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

`updateStockPrice`함수는 함수에서와 동일한 방법으로 서버에서 받은 스톡 개체의 형식을 테이블 행으로 지정 합니다 `init` . 테이블에 행을 추가 하는 대신 테이블에서 주식의 현재 행을 찾아 해당 행을 새 행으로 바꿉니다.

## <a name="test-the-application"></a>애플리케이션 테스트

앱이 작동 하는지 테스트할 수 있습니다. 모든 브라우저 창에서 주식 가격이 변동 인 라이브 재고 테이블이 표시 됩니다.

1. 도구 모음에서 **스크립트 디버깅** 을 사용 하도록 설정 하 고 재생 단추를 선택 하 여 디버그 모드에서 앱을 실행 합니다.

    ![디버깅 모드를 켜고 재생을 선택 하는 사용자의 스크린샷](tutorial-server-broadcast-with-signalr/_static/image4.png)

    **라이브 재고 테이블**을 표시 하는 브라우저 창이 열립니다. Stock 테이블에는 처음에 "로드 중 ..."이 표시 됩니다. 그런 다음, 짧은 시간 후에 앱은 초기 주식 데이터를 표시 한 다음 주가 변경 되기 시작 합니다.

1. 브라우저에서 URL을 복사 하 여 다른 두 브라우저를 열고 Url을 주소 표시줄에 붙여넣습니다.

    초기 주식 표시는 첫 번째 브라우저와 동일 하며 변경 내용이 동시에 발생 합니다.

1. 모든 브라우저를 닫고 새 브라우저를 연 다음 동일한 URL로 이동 합니다.

    StockTicker singleton 개체가 서버에서 계속 실행 됩니다. **라이브 스톡 테이블** 은 주가 계속 변경 된 것을 보여 줍니다. 변경 수치가 0 인 초기 테이블은 표시 되지 않습니다.

1. 브라우저를 닫습니다.

## <a name="enable-logging"></a>로깅 사용

SignalR에는 문제 해결을 지원 하기 위해 클라이언트에서 사용할 수 있는 기본 제공 로깅 함수가 있습니다. 이 섹션에서는 로깅을 사용 하도록 설정 하 고 SignalR에서 사용 하는 전송 방법에 대 한 로그를 표시 하는 예제를 표시 합니다.

* [Websocket](http://en.wikipedia.org/wiki/WebSocket)-IIS 8 및 현재 브라우저에서 지원 됩니다.

* Internet Explorer 이외의 브라우저에서 지원 되는 [서버에서 보낸 이벤트](http://en.wikipedia.org/wiki/Server-sent_events)

* [영구적 프레임](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)으로, Internet Explorer에서 지원 됩니다.

* 모든 브라우저에서 지원 되는 [Ajax 긴 폴링](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling).

SignalR는 지정 된 모든 연결에 대해 서버와 클라이언트가 지 원하는 최상의 전송 방법을 선택 합니다.

1. *StockTicker.js*를 엽니다.

1. 이 강조 표시 된 코드 줄을 추가 하 여 파일 끝에서 연결을 초기화 하는 코드 바로 앞에서 로깅을 사용 하도록 설정 합니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. **F5** 키를 눌러 프로젝트를 실행 합니다.

1. 브라우저의 개발자 도구 창을 열고 콘솔을 선택 하 여 로그를 확인 합니다. 새 연결에 대 한 전송 방법을 협상 하는 SignalR의 로그를 확인 하려면 페이지를 새로 고쳐야 할 수도 있습니다.

    * Windows 8 (IIS 8)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 **websocket**입니다.

    * Windows 7 (IIS 7.5)에서 Internet Explorer 10을 실행 하는 경우 전송 방법은 **iframe**입니다.

    * Windows 8 (IIS 8)에서 Firefox 19를 실행 하는 경우 전송 방법은 **websocket**입니다.

        > [!TIP]
        > Firefox에서 Firebug 추가 기능을 설치 하 여 콘솔 창을 가져옵니다.

    * Windows 7 (IIS 7.5)에서 Firefox 19를 실행 하는 경우 전송 방법은 서버에서 **보낸** 이벤트입니다.

## <a name="install-the-stockticker-sample"></a>StockTicker 샘플 설치

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) 는 StockTicker 응용 프로그램을 설치 합니다. NuGet 패키지에는 처음부터 만든 단순화 된 버전 보다 더 많은 기능이 포함 되어 있습니다. 자습서의이 섹션에서는 NuGet 패키지를 설치 하 고 새 기능 및이를 구현 하는 코드를 검토 합니다.

> [!IMPORTANT]
> 이 자습서의 이전 단계를 수행 하지 않고 패키지를 설치 하는 경우 프로젝트에 OWIN startup 클래스를 추가 해야 합니다. NuGet 패키지에 대 한이 readme.txt 파일에서는이 단계에 대해 설명 합니다.

### <a name="install-the-signalrsample-nuget-package"></a>SignalR NuGet 패키지를 설치 합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.

1. **NuGet 패키지 관리자: SignalR. StockTicker**에서 **찾아보기**를 선택 합니다.

1. **패키지 원본**에서 **nuget.org**를 선택 합니다.

1. 검색 상자에 *SignalR* 를 입력 하 고 **SignalR**  >  **설치**를 선택 합니다.

1. **솔루션 탐색기**에서 *SignalR* 폴더를 확장 합니다.

    SignalR 패키지를 설치 하면 폴더와 해당 내용이 생성 됩니다.

1. *SignalR* 폴더에서 *StockTicker.html*을 마우스 오른쪽 단추로 클릭 한 다음 **시작 페이지로 설정**을 선택 합니다.

    > [!NOTE]
    > SignalR NuGet 패키지를 설치 하면 *Scripts* 폴더에 있는 jQuery 버전이 변경 될 수 있습니다. 패키지가 *SignalR* 폴더에 설치 하는 새 *StockTicker.html* 파일은 패키지가 설치 하는 jQuery 버전과 동기화 되지만 원래 *StockTicker.html* 파일을 다시 실행 하려는 경우 먼저 스크립트 태그에서 jquery 참조를 업데이트 해야 할 수 있습니다.

### <a name="run-the-application"></a>애플리케이션 실행

 첫 번째 앱에서 살펴본 테이블에는 유용한 기능이 있습니다. 전체 주식 시세 응용 프로그램에는 새 기능이 표시 됩니다. 가로 스크롤 창에서는 주식 데이터 및 주식으로 색을 변경 하는 주가 표시 됩니다.

1. **F5** 키를 눌러 앱을 실행 합니다.

     앱을 처음으로 실행 하는 경우 "market"은 "닫힘" 이며, 스크롤하지 않는 정적 테이블과 표시기 창이 표시 됩니다.

1. **시장 열기**를 선택 합니다.

    ![라이브 표시기의 스크린샷](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * **라이브 주식 시세 표시기** 상자를 가로로 스크롤하면 서버에서 정기적으로 주식 시세 변경을 정기적으로 브로드캐스트 하기 시작 합니다.

    * 주가 변경 될 때마다 앱은 **Live Stock 테이블과** **라이브 주식 시세 표시기**를 모두 업데이트 합니다.

    * 주가 변화 하는 경우 앱은 녹색 배경의 재고를 표시 합니다.

    * 변경이 음수 이면 앱은 빨간색 배경의 재고를 표시 합니다.

1. **시장 종결**을 선택 합니다.

    * 테이블 업데이트가 중지 됩니다.

    * 표시기가 스크롤을 중지 합니다.

1. **재설정**을 선택합니다.

    * 모든 재고 데이터를 다시 설정 합니다.

    * 앱은 가격 변경이 시작 되기 전에 초기 상태를 복원 합니다.

1. 브라우저에서 URL을 복사 하 여 다른 두 브라우저를 열고 Url을 주소 표시줄에 붙여넣습니다.

1. 각 브라우저에서 동시에 동일한 데이터를 동적으로 업데이트 하는 것을 볼 수 있습니다.

1. 컨트롤 중 하나를 선택 하면 모든 브라우저가 동시에 동일한 방식으로 응답 합니다.

### <a name="live-stock-ticker-display"></a>라이브 주식 종목 표시

**라이브 주식 시세** 표시는 `<div>` CSS 스타일로 한 줄로 서식 지정 된 요소에서 순서가 지정 되지 않은 목록입니다. 앱은 템플릿 문자열에서 자리 표시자를 대체 `<li>` 하 고 요소를 `<li>` 요소에 동적으로 추가 하 여 테이블과 동일한 방식으로 종목을 초기화 하 고 업데이트 합니다. `<ul>` 앱은 jQuery 함수를 사용 하 여에서 순서가 지정 되지 않은 `animate` 목록의 왼쪽 여백을 변경 하는 스크롤을 포함 합니다 `<div>` .

#### <a name="signalrsample-stocktickerhtml"></a>SignalR StockTicker.html

주식 시세 HTML 코드:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR StockTicker

주식 시세 CSS 코드:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR SignalR.StockTicker.js

스크롤할 수 있도록 하는 jQuery 코드:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>클라이언트에서 호출할 수 있는 서버에 대 한 추가 메서드

앱에 유연성을 추가 하기 위해 앱에서 호출할 수 있는 추가 방법이 있습니다.

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR StockTickerHub.cs

`StockTickerHub`클래스는 클라이언트에서 호출할 수 있는 다음 네 가지 메서드를 추가로 정의 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

앱은 `OpenMarket` `CloseMarket` `Reset` 페이지 맨 위에 있는 단추에 대 한 응답으로, 및를 호출 합니다. 모든 클라이언트에 즉시 전파 되는 상태 변경을 트리거하는 한 클라이언트의 패턴을 보여 줍니다. 이러한 각 메서드는 `StockTicker` 시장 상태를 변경 하 고 새 상태를 브로드캐스팅하는 클래스의 메서드를 호출 합니다.

#### <a name="signalrsample-stocktickercs"></a>SignalR StockTicker.cs

클래스에서 `StockTicker` 앱은 `MarketState` 열거형 값을 반환 하는 속성을 사용 하 여 시장의 상태를 유지 관리 합니다 `MarketState` .

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

`StockTicker`클래스를 스레드로부터 안전 하 게 보호 해야 하므로 시장 상태를 변경 하는 각 메서드는 잠금 블록 내에서이 작업을 수행 합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

이 코드가 스레드로부터 안전 하 게 보호 되도록 하기 위해 `_marketState` 지정 된 속성을 지 원하는 필드는 `MarketState` `volatile` 다음과 같습니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

`BroadcastMarketStateChange`및 `BroadcastMarketReset` 메서드는 클라이언트에 정의 된 다른 메서드를 호출 하는 것을 제외 하 고 이미 보았던 BroadcastStockPrice 메서드와 비슷합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>서버에서 호출할 수 있는 클라이언트의 추가 함수

`updateStockPrice`이제 함수는 테이블 및 표시기 표시를 모두 처리 하 고를 사용 하 여 `jQuery.Color` 빨강 및 녹색 색을 표시 합니다.

의 새 함수는 시장 상태에 따라 단추를 사용 하거나 사용 하지 않도록 설정 *SignalR.StockTicker.js* 합니다. 또한 **라이브 주식 시세 표시기** 가로 스크롤을 중지 하거나 시작 합니다. 많은 함수가에 추가 되기 때문에 `ticker.client` 앱은 [jQuery extend 함수](http://api.jquery.com/jQuery.extend/) 를 사용 하 여 추가 합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>연결을 설정한 후 추가 클라이언트 설정

클라이언트에서 연결을 설정한 후에는 다음과 같은 몇 가지 추가 작업을 수행 해야 합니다.

* 적절 한 or 함수를 호출 하기 위해 시장이 열려 있는지 또는 닫혀 있는지 확인 `marketOpened` `marketClosed` 합니다.

* 서버 메서드 호출을 단추에 연결 합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

서버 메서드는 앱이 연결을 설정할 때까지 단추에 연결 되지 않습니다. 코드를 사용 하기 전에 서버 메서드를 호출할 수 없기 때문입니다.

## <a name="additional-resources"></a>추가 리소스

이 자습서에서는 서버에서 연결 된 모든 클라이언트로 메시지를 브로드캐스팅하는 SignalR 응용 프로그램을 프로그래밍 하는 방법에 대해 알아보았습니다. 이제 모든 클라이언트의 알림에 대 한 응답으로 메시지를 정기적으로 브로드캐스트할 수 있습니다. 다중 스레드 singleton 인스턴스의 개념을 사용 하 여 다중 플레이어 온라인 게임 시나리오에서 서버 상태를 유지 관리할 수 있습니다. 예를 들어 SignalR을 [기반으로 하는 Sho이상 r 게임](https://github.com/NTaylorMullen/ShootR)을 참조 하세요.

피어 투 피어 통신 시나리오를 보여 주는 자습서는 [SignalR 시작](introduction-to-signalr.md) 하기 및 [SignalR를 사용 하 여 실시간 업데이트](tutorial-high-frequency-realtime-with-signalr.md)를 참조 하세요.

SignalR에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

* [ASP.NET SignalR](../../index.md)
* [SignalR 프로젝트](http://signalr.net/)
* [SignalR GitHub 및 샘플](https://github.com/SignalR/SignalR)
* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 프로젝트를 만듦
> * 서버 코드 설정
> * 서버 코드를 검사 합니다.
> * 클라이언트 코드 설정
> * 클라이언트 코드를 검사 합니다.
> * 애플리케이션 테스트
> * 로깅 사용

ASP.NET SignalR 2를 사용 하는 실시간 웹 응용 프로그램을 만드는 방법에 대해 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [SignalR를 사용 하 여 실시간 웹 앱 만들기](real-time-web-applications-with-signalr.md)
