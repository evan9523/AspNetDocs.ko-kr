---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: '튜토리얼: SignalR 2로 서버 브로드캐스트 | 마이크로 소프트 문서'
author: tdykstra
description: 이 자습서에서는 ASP.NET SignalR 2를 사용하여 서버 브로드캐스트 기능을 제공하는 웹 응용 프로그램을 만드는 방법을 보여 주며 있습니다.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675726"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>자습서: SignalR 2를 통해 서버 브로드캐스트

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

이 자습서에서는 ASP.NET SignalR 2를 사용하여 서버 브로드캐스트 기능을 제공하는 웹 응용 프로그램을 만드는 방법을 보여 주며 있습니다. 서버 브로드캐스트는 서버가 클라이언트에 전송된 통신을 시작한다는 것을 의미합니다.

이 자습서에서 만드는 응용 프로그램은 서버 브로드캐스트 기능에 대한 일반적인 시나리오인 주식 시세를 시뮬레이션합니다. 주기적으로 서버는 주가를 임의로 업데이트하고 연결된 모든 클라이언트에 업데이트를 브로드캐스트합니다. 브라우저에서 **변경** 및 **%** 열의 숫자와 기호는 서버의 알림에 대한 응답으로 동적으로 변경됩니다. 동일한 URL에 추가 브라우저를 열면 모두 동일한 데이터와 동일한 데이터 변경 내용이 동시에 표시됩니다.

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
> 응용 프로그램을 빌드하는 단계를 거치지 않으려면 새 빈 ASP.NET 웹 응용 프로그램 프로젝트에 SignalR.Sample 패키지를 설치할 수 있습니다. 이 자습서의 단계를 수행하지 않고 NuGet 패키지를 설치하는 경우 *readme.txt* 파일의 지침을 따라야 합니다. 패키지를 실행하려면 설치된 패키지에서 `ConfigureSignalR` 메서드를 호출하는 OWIN 시작 클래스를 추가해야 합니다. OWIN 시작 클래스를 추가 하지 않으면 오류가 발생 합니다. 이 문서의 [StockTicker 설치 샘플](#install-the-stockticker-sample) 섹션을 참조하십시오.

## <a name="prerequisites"></a>사전 요구 사항

* **ASP.NET 및 웹 개발** 워크로드가 있는 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="create-the-project"></a>프로젝트 만들기

이 섹션에서는 Visual Studio 2017을 사용하여 빈 ASP.NET 웹 응용 프로그램을 만드는 방법을 보여 주며 있습니다.

1. Visual Studio에서 ASP.NET 웹 응용 프로그램을 만듭니다.

    ![웹 만들기](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. 새 **ASP.NET 웹 응용 프로그램 - SignalR.StockTicker** 창에서 **빈 을** 선택하고 **확인을**선택합니다.

## <a name="set-up-the-server-code"></a>서버 코드 설정

이 섹션에서는 서버에서 실행되는 코드를 설정합니다.

### <a name="create-the-stock-class"></a>주식 클래스 만들기

먼저 *주식에* 대한 정보를 저장하고 전송하는 데 사용할 Stock 모델 클래스를 만듭니다.

1. **솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**클래스** **추가를** > 선택합니다.

1. 클래스 스톡의 이름을 지정하고 프로젝트에 *추가합니다.*

1. *Stock.cs* 파일의 코드를 이 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    주식을 만들 때 설정하는 두 속성은 `Symbol` (예 : Microsoft의 MSFT) 및 `Price`. 다른 속성은 설정 `Price`하는 방법 및 시기에 따라 달라 집니다. 처음 설정하면 `Price`값이 `DayOpen`에 전파됩니다. 그런 다음 설정하면 `Price` `Change` 앱에서 및 의 `PercentChange` 차이를 기준으로 속성 `Price` 값과 `DayOpen`을 계산합니다.

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>스톡티커허브 및 스톡티커 클래스 만들기

SignalR 허브 API를 사용하여 서버 간 상호 작용을 처리합니다. SignalR `StockTickerHub` `Hub` 클래스에서 파생 된 클래스는 클라이언트에서 받는 연결 및 메서드 호출을 처리 합니다. 또한 스톡 데이터를 유지하고 개체를 `Timer` 실행해야 합니다. 개체는 `Timer` 클라이언트 연결과 관계없이 가격 업데이트를 주기적으로 트리거합니다. 허브는 일시적이기 때문에 이러한 `Hub` 함수를 클래스에 넣을 수 없습니다. 앱은 클라이언트에서 서버로의 `Hub` 연결 및 호출과 같은 허브의 각 작업에 대한 클래스 인스턴스를 만듭니다. 따라서 재고 데이터를 유지하고 가격을 업데이트하며 가격 업데이트를 브로드캐스트하는 메커니즘은 별도의 클래스에서 실행해야 합니다. 클래스의 `StockTicker`이름을 지정합니다.

![스톡티커에서 방송](tutorial-server-broadcast-with-signalr/_static/image3.png)

`StockTicker` 서버에서 클래스의 인스턴스가 하나만 실행되도록 하려면 각 `StockTickerHub` 인스턴스에서 단일 `StockTicker` 인스턴스에 대한 참조를 설정해야 합니다. 클래스는 `StockTicker` 스톡 데이터를 가지고 있고 업데이트를 트리거하기 때문에 클라이언트에 브로드캐스트해야 하지만 `StockTicker` 클래스는 `Hub` 아닙니다. 클래스는 `StockTicker` SignalR 허브 연결 컨텍스트 개체에 대한 참조를 얻어야 합니다. 그런 다음 SignalR 연결 컨텍스트 개체를 사용하여 클라이언트에 브로드캐스트할 수 있습니다.

#### <a name="create-stocktickerhubcs"></a>StockTickerHub.cs 만들기

1. **솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**새 항목** **추가를** > 선택합니다.

1. **새 항목 추가 - SignalR.StockTicker에서** **설치된** > **시각적 C#** > **웹** > **신호기를** 선택한 다음 **SignalR 허브 클래스(v2)를**선택합니다.

1. *클래스 StockTickerHub의* 이름을 지정하고 프로젝트에 추가합니다.

    이 단계는 *StockTickerHub.cs* 클래스 파일을 만듭니다. 동시에 SignalR을 지원하는 스크립트 파일 및 어셈블리 참조 집합을 프로젝트에 추가합니다.

1. *StockTickerHub.cs* 파일의 코드를 이 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. 파일을 저장합니다.

앱은 [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 클래스를 사용하여 클라이언트가 서버에서 호출할 수 있는 메서드를 정의합니다. 한 가지 방법을 정의하고 `GetAllStocks()`있습니다. 클라이언트가 처음에 서버에 연결하면 이 메서드를 호출하여 현재 가격으로 모든 주식 목록을 가져옵니다. 메서드는 메모리에서 데이터를 반환하기 `IEnumerable<Stock>` 때문에 동기적으로 실행되고 반환될 수 있습니다.

데이터베이스 조회 또는 웹 서비스 호출과 같이 대기가 필요한 작업을 수행하여 메서드가 데이터를 `Task<IEnumerable<Stock>>` 얻어야 하는 경우 비동기 처리를 활성화하기 위해 반환 값으로 지정합니다. 자세한 내용은 [ASP.NET SignalR 허브 API 가이드 - 서버 - 비동기적으로 실행되는 경우를](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)참조하십시오.

속성은 `HubName` 앱이 클라이언트의 JavaScript 코드에서 허브를 참조하는 방법을 지정합니다. 이 특성을 사용하지 않는 경우 클라이언트의 기본 이름은 클래스 이름의 camelCase 버전이며 이 경우 `stockTickerHub`는 .입니다.

클래스를 만들 `StockTicker` 때 나중에 볼 수 있듯이 앱은 정적 `Instance` 속성에서 해당 클래스의 단일 인스턴스를 만듭니다. 그 단일 `StockTicker` 인스턴스는 얼마나 많은 클라이언트가 연결되거나 연결을 끊는지에 관계없이 메모리에 있습니다. 이 인스턴스는 `GetAllStocks()` 메서드가 현재 주식 정보를 반환하는 데 사용하는 것입니다.

#### <a name="create-stocktickercs"></a>StockTicker.cs 만들기

1. **솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**클래스** **추가를** > 선택합니다.

1. *클래스 StockTicker의* 이름을 지정하고 프로젝트에 추가합니다.

1. *StockTicker.cs* 파일의 코드를 이 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

모든 스레드는 StockTicker 코드의 동일한 인스턴스를 실행하므로 StockTicker 클래스는 스레드가 안전해야 합니다.

### <a name="examine-the-server-code"></a>서버 코드 검사

서버 코드를 검사하면 앱의 작동 방식을 이해하는 데 도움이 됩니다.

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>정적 필드에 싱글톤 인스턴스 저장

코드는 클래스의 인스턴스를 통해 `_instance` `Instance` 속성을 백업하는 정적 필드를 초기화합니다. 생성자는 비공개이므로 앱에서 만들 수 있는 클래스의 유일한 인스턴스입니다. 앱은 `_instance` 필드에 대해 [지연 초기화를](/dotnet/framework/performance/lazy-initialization) 사용합니다. 성능상의 이유가 아닙니다. 인스턴스 생성이 스레드에서 안전한지 확인하는 것입니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

클라이언트가 서버에 연결할 때마다 별도의 스레드에서 실행되는 StockTickerHub 클래스의 새 인스턴스는 클래스의 앞에서 보았듯이 `StockTicker.Instance` 정적 속성에서 StockTicker 싱글톤 인스턴스를 `StockTickerHub` 가져옵니다.

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>주식 데이터를 동시 사전에 저장

생성자는 일부 샘플 `_stocks` 스톡 데이터로 컬렉션을 초기화하고 `GetAllStocks` 주식을 반환합니다. 앞에서 보았듯이 이 stocks 컬렉션은 `StockTickerHub.GetAllStocks`클라이언트가 호출할 수 `Hub` 있는 클래스의 서버 메서드인 에 의해 반환됩니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

stocks 컬렉션은 스레드 안전을 위한 [동시사전](https://msdn.microsoft.com/library/dd287191.aspx) 유형으로 정의됩니다. 또는 [사전](https://msdn.microsoft.com/library/xfhwa508.aspx) 개체를 사용하고 변경할 때 사전을 명시적으로 잠글 수 있습니다.

이 샘플 응용 프로그램의 경우 응용 프로그램 데이터를 메모리에 저장하고 앱이 `StockTicker` 인스턴스를 삭제할 때 데이터를 손실해도 됩니다. 실제 응용 프로그램에서는 데이터베이스와 같은 백 엔드 데이터 저장소를 사용하여 작업합니다.

#### <a name="periodically-updating-stock-prices"></a>주기적으로 주가 업데이트

생성자는 주기적으로 `Timer` 주가를 임의로 업데이트하는 메서드를 호출하는 개체를 시작합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer`을 `UpdateStockPrices`호출합니다. 가격을 업데이트하기 전에 앱은 개체에 `_updateStockPricesLock` 대한 잠금을 수행합니다. 코드는 다른 스레드가 이미 가격을 업데이트하고 있는지 `TryUpdateStockPrice` 확인한 다음 목록의 각 주식을 호출합니다. 이 `TryUpdateStockPrice` 방법은 주가를 변경할지 여부와 변경 정도를 결정합니다. 주가가 변경되면 앱은 `BroadcastStockPrice` 연결된 모든 클라이언트에게 주가 변동을 브로드캐스트하기 위해 호출합니다.

플래그는 `_updatingStockPrices` [스레드가](https://msdn.microsoft.com/library/x13ttww7.aspx) 안전한지 확인하기 위해 휘발성으로 지정되었습니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

실제 응용 프로그램에서 `TryUpdateStockPrice` 메서드는 가격을 조회하기 위해 웹 서비스를 호출합니다. 이 코드에서 앱은 난수 생성기를 사용하여 임의로 변경합니다.

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>StockTicker 클래스가 고객에게 브로드캐스트할 수 있도록 SignalR 컨텍스트 를 가져오는 것

가격 변경은 `StockTicker` 개체에서 여기에서 시작되므로 연결된 모든 클라이언트에서 메서드를 `updateStockPrice` 호출해야 하는 개체입니다. `Hub` 클래스에서 클라이언트 메서드를 호출하는 API가 `StockTicker` 있지만 `Hub` 클래스에서 파생되지 않으며 `Hub` 개체에 대한 참조가 없습니다. 연결된 클라이언트로 브로드캐스트하려면 `StockTicker` 클래스에서 클래스에 대한 SignalR 컨텍스트 인스턴스를 `StockTickerHub` 얻고 이를 사용하여 클라이언트에서 메서드를 호출해야 합니다.

코드는 싱글톤 클래스 인스턴스를 만들고 생성자를 참조하는 암호를 전달하고 생성자가 속성에 넣을 때 SignalR `Clients` 컨텍스트에 대한 참조를 가져옵니다.

컨텍스트를 한 번만 가져오는 데는 두 가지 이유가 있습니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

컨텍스트의 `Clients` 속성을 가져오는 다음 `StockTickerClient` 속성에 넣으면 클래스와 동일하게 보이는 클라이언트 메서드를 호출하는 `Hub` 코드를 작성할 수 있습니다. 예를 들어 모든 클라이언트에 브로드캐스트하려면 을 작성할 `Clients.All.updateStockPrice(stock)`수 있습니다.

호출하는 메서드는 `updateStockPrice` 아직 `BroadcastStockPrice` 존재하지 않습니다. 클라이언트에서 실행되는 코드를 작성할 때 나중에 추가합니다. 앱이 런타임시 식을 `updateStockPrice` 평가한다는 의미동적이기 때문에 `Clients.All` 여기에서 참조할 수 있습니다. 이 메서드 호출이 실행되면 SignalR은 메서드 이름과 매개 변수 값을 클라이언트에 보내고 클라이언트에 라는 `updateStockPrice`메서드가 있는 경우 앱은 해당 메서드를 호출하고 매개 변수 값을 전달합니다.

`Clients.All`즉, 모든 클라이언트에 전송됩니다. SignalR은 보낼 클라이언트 또는 클라이언트 그룹을 지정하는 다른 옵션을 제공합니다. 자세한 내용은 [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)을 참조하십시오.

### <a name="register-the-signalr-route"></a>SignalR 경로 등록

서버는 어떤 URL을 가로채서 SignalR로 전달할지 알아야 합니다. 이렇게 하려면 OWIN 시작 클래스를 추가합니다.

1. **솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**새 항목** **추가를** > 선택합니다.

1. **새 항목 추가 - SignalR.StockTicker** **설치된** > **시각적 C#** > **웹을** 선택한 다음 **OWIN 시작 클래스를**선택합니다.

1. *클래스* 시작 이름을 지정하고 **확인을**선택합니다.

1. *Startup.cs* 파일의 기본 코드를 이 코드로 바꿉니다.

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

이제 서버 코드 설정이 완료되었습니다. 다음 섹션에서는 클라이언트를 설정합니다.

## <a name="set-up-the-client-code"></a>클라이언트 코드 설정

이 섹션에서는 클라이언트에서 실행되는 코드를 설정합니다.

### <a name="create-the-html-page-and-javascript-file"></a>HTML 페이지 및 자바스크립트 파일 만들기

HTML 페이지에 데이터가 표시되고 JavaScript 파일이 데이터를 구성합니다.

#### <a name="create-stocktickerhtml"></a>스톡티커 만들기.html

먼저 HTML 클라이언트를 추가합니다.

1. **솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**HTML 페이지** **추가를** > 선택합니다.

1. 파일 *스톡티커의* 이름을 지정하고 **확인을**선택합니다.

1. *StockTicker.html* 파일의 기본 코드를 이 코드로 바꿉니다.

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML은 5개의 열, 헤더 행 및 5개의 열모두에 걸쳐 있는 단일 셀이 있는 데이터 행이 있는 테이블을 만듭니다. 데이터 행에 "로드..."가 표시됩니다. 앱이 시작될 때 순간적으로 JavaScript 코드는 해당 행을 제거하고 서버에서 검색된 스톡 데이터가 있는 해당 자리 행에 추가됩니다.

    스크립트 태그는 다음을 지정합니다.

    * jQuery 스크립트 파일입니다.

    * SignalR 코어 스크립트 파일입니다.

    * SignalR 프록시 스크립트 파일입니다.

    * 나중에 만들 스톡티커 스크립트 파일입니다.

    앱은 SignalR 프록시 스크립트 파일을 동적으로 생성합니다. "/signalr/hubs" URL을 지정 하 고 Hub 클래스의 메서드에 대 한 프록시 `StockTickerHub.GetAllStocks`메서드를 정의 합니다.이 경우 에 대 한 입니다. 원하는 경우 [SignalR 유틸리티를](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)사용하여 이 JavaScript 파일을 수동으로 생성할 수 있습니다. 메서드 호출에서 동적 파일 생성을 `MapHubs` 사용하지 않도록 설정하는 것을 잊지 마십시오.

1. **솔루션 탐색기에서** **스크립트를 확장합니다.**

    jQuery 및 SignalR에 대한 스크립트 라이브러리는 프로젝트에 표시됩니다.

    > [!IMPORTANT]
    > 패키지 관리자는 SignalR 스크립트의 이후 버전을 설치합니다.

1. 프로젝트의 스크립트 파일 버전에 해당하도록 코드 블록의 스크립트 참조를 업데이트합니다.

1. **솔루션 탐색기에서** *StockTicker.html을*마우스 오른쪽 단추로 클릭한 다음 **시작 페이지로 설정을**선택합니다.

#### <a name="create-stocktickerjs"></a>스톡티커 만들기

이제 자바 스크립트 파일을 만듭니다.

1. **솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고**JavaScript 파일** **추가를** > 선택합니다.

1. 파일 *스톡티커의* 이름을 지정하고 **확인을**선택합니다.

1. 이 코드를 *StockTicker.js* 파일에 추가합니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>클라이언트 코드 검사

클라이언트 코드를 검사하면 클라이언트 코드가 서버 코드와 상호 작용하여 앱이 작동하는 방법을 알아보는 데 도움이 됩니다.

#### <a name="starting-the-connection"></a>연결 시작

`$.connection`는 SignalR 프록시를 나타냅니다. 코드는 클래스의 프록시에 대한 `StockTickerHub` 참조를 얻고 `ticker` 변수에 넣습니다. 프록시 이름은 `HubName` 특성에 의해 설정된 이름입니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

모든 변수와 함수를 정의한 후 파일의 마지막 코드 줄은 SignalR 함수를 호출하여 `start` SignalR 연결을 초기화합니다. 함수는 `start` 비동기적으로 실행되고 [jQuery 지연 된 개체를](http://api.jquery.com/category/deferred-object/)반환합니다. done 함수를 호출하여 앱이 비동기 작업을 완료할 때 호출할 함수를 지정할 수 있습니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>모든 주식 얻기

이 `init` 함수는 `getAllStocks` 서버의 함수를 호출하고 서버가 반환하는 정보를 사용하여 스톡 테이블을 업데이트합니다. 기본적으로 메서드 이름이 서버에서 파스칼 대/소문자인 경우에도 클라이언트에서 camelCasing을 사용해야 합니다. 낙타 선 규칙은 개체가 아닌 메서드에만 적용됩니다. 예를 들어, `stock.Symbol` 및 `stock.Price`을 `stock.symbol` 참조합니다. `stock.price`

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

메서드에서 `init` 앱은 개체의 형식 속성을 호출한 다음 변수의 자리 `formatStock` 표시자를 `stock` 개체 `stock` 속성 값으로 `supplant` 바꾸기 위해 호출하여 `rowTemplate` 서버에서 받은 각 stock 개체에 대한 테이블 행에 대한 HTML을 만듭니다. 그런 다음 결과 HTML이 주식 테이블에 추가됩니다.

> [!NOTE]
> 비동기 `init` `callback` `start` 함수가 완료된 후 실행되는 함수로 전달하여 호출합니다. 호출 `start`후 `init` 별도의 JavaScript 문으로 호출하면 시작 함수가 연결 설정이 완료될 때까지 기다리지 않고 즉시 실행되므로 함수가 실패합니다. 이 경우 함수는 앱이 `init` `getAllStocks` 서버 연결을 설정하기 전에 함수를 호출하려고 시도합니다.

#### <a name="getting-updated-stock-prices"></a>주가 업데이트

서버가 주식 가격을 변경하면 연결된 클라이언트를 호출합니다. `updateStockPrice` 앱은 `stockTicker` 프록시의 클라이언트 속성에 함수를 추가하여 서버에서 호출할 수 있도록 합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

함수는 `updateStockPrice` 서버에서 받은 스톡 개체를 `init` 함수와 동일한 방식으로 테이블 행에 포맷합니다. 테이블에 행을 넣는 대신 테이블에서 주식의 현재 행을 찾아 해당 행을 새 행으로 바꿉습니다.

## <a name="test-the-application"></a>애플리케이션 테스트

앱이 작동하는지 테스트할 수 있습니다. 모든 브라우저 창이 주가 변동과 함께 라이브 주식 테이블을 표시 볼 수 있습니다.

1. 도구 모음에서 스크립트 **디버깅을** 켜고 재생 버튼을 선택하여 디버그 모드에서 앱을 실행합니다.

    ![사용자가 디버깅 모드를 켜고 재생을 선택하는 스크린샷입니다.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    **라이브 스톡 테이블을**표시하는 브라우저 창이 열립니다. 주식 테이블에는 처음에 "로드..."가 표시됩니다. 그런 다음 짧은 시간 후에 앱에 초기 주식 데이터가 표시되고 주가가 변경되기 시작합니다.

1. 브라우저에서 URL을 복사하고 다른 두 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.

    초기 재고 표시는 첫 번째 브라우저와 동일하며 변경 사항이 동시에 발생합니다.

1. 모든 브라우저를 닫고 새 브라우저를 열고 동일한 URL로 이동합니다.

    StockTicker 싱글톤 개체는 서버에서 계속 실행되었습니다. **라이브 주식 테이블은** 주식이 계속 변화하고 있음을 보여줍니다. 변경 수치가 0인 초기 테이블이 표시되지 않습니다.

1. 브라우저를 닫습니다.

## <a name="enable-logging"></a>로깅 사용

SignalR에는 클라이언트에서 문제 해결을 돕기 위해 활성화할 수 있는 기본 제공 로깅 기능이 있습니다. 이 섹션에서는 로깅을 사용하도록 설정하고 로그가 SignalR에서 사용하는 다음 전송 방법을 알려주는 방법을 보여 주는 예제를 볼 수 있습니다.

* [웹 소켓](http://en.wikipedia.org/wiki/WebSocket), IIS 8 및 현재 브라우저에서 지원됩니다.

* [서버 전송 이벤트](http://en.wikipedia.org/wiki/Server-sent_events), 인터넷 익스플로러 이외의 브라우저에서 지원됩니다.

* [영원히 프레임,](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)인터넷 익스플로러에 의해 지원.

* 모든 브라우저에서 지원하는 [Ajax 긴 폴링.](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)

지정된 연결에 대해 SignalR은 서버와 클라이언트가 지원하는 최상의 전송 방법을 선택합니다.

1. 오픈 *스톡티커.js*.

1. 이 강조 표시된 코드 줄을 추가하면 파일 끝에 연결을 초기화하는 코드 바로 앞에서 로깅을 활성화할 수 있습니다.

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. **F5를** 눌러 프로젝트를 실행합니다.

1. 브라우저의 개발자 도구 창을 열고 콘솔을 선택하여 로그를 확인합니다. 새 연결에 대 한 전송 메서드를 협상 하는 SignalR의 로그를 보려면 페이지를 새로 고쳐야 할 수 있습니다.

    * Windows 8(IIS 8)에서 Internet Explorer 10을 실행하는 경우 전송 방법은 **WebSockets**입니다.

    * Windows 7(IIS 7.5)에서 인터넷 익스플로러 10을 실행하는 경우 전송 방법은 **iframe**입니다.

    * Windows 8(IIS 8)에서 Firefox 19를 실행하는 경우 전송 방법은 **WebSockets**입니다.

        > [!TIP]
        > 파이어 폭스에서, 콘솔 창을 얻기 위해 파이어 버그 추가 기능을 설치합니다.

    * Windows 7(IIS 7.5)에서 Firefox 19를 실행하는 경우 전송 방법은 **서버에서 전송하는** 이벤트입니다.

## <a name="install-the-stockticker-sample"></a>스톡티커 샘플 설치

[Microsoft.AspNet.SignalR.샘플은](http://nuget.org/packages/microsoft.aspnet.signalr.sample) StockTicker 응용 프로그램을 설치합니다. NuGet 패키지에는 처음부터 만든 단순화된 버전보다 더 많은 기능이 포함되어 있습니다. 자습서의 이 섹션에서는 NuGet 패키지를 설치하고 새 기능과 이를 구현하는 코드를 검토합니다.

> [!IMPORTANT]
> 이 자습서의 이전 단계를 수행하지 않고 패키지를 설치하는 경우 프로젝트에 OWIN 시작 클래스를 추가해야 합니다. NuGet 패키지에 대한 이 readme.txt 파일은 이 단계를 설명합니다.

### <a name="install-the-signalrsample-nuget-package"></a>SignalR.샘플 NuGet 패키지 설치

1. **솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리를 선택합니다.**

1. **NuGet 패키지 관리자: SignalR.StockTicker,** 찾아보기 를 **선택합니다.**

1. **패키지 소스에서** **nuget.org**을 선택합니다.

1. 검색 상자에 *SignalR.Sample을* 입력하고 **Microsoft.AspNet.SignalR.샘플** > **설치를**선택합니다.

1. **솔루션 탐색기에서** *SignalR.Sample* 폴더를 확장합니다.

    SignalR.Sample 패키지를 설치하면 폴더와 해당 내용이 생성되었습니다.

1. *SignalR.Sample* 폴더에서 *StockTicker.html을*마우스 오른쪽 단추로 클릭한 다음 **시작 페이지로 설정 옵션을**선택합니다.

    > [!NOTE]
    > SignalR.Sample NuGet 패키지를 설치하면 스크립트 폴더에 있는 jQuery 버전이 변경될 수 *있습니다.* 패키지가 *SignalR.Sample* 폴더에 설치하는 새 *StockTicker.html* 파일은 패키지가 설치하는 jQuery 버전과 동기화되지만 원래 *StockTicker.html* 파일을 다시 실행하려면 먼저 스크립트 태그에서 jQuery 참조를 업데이트해야 할 수 있습니다.

### <a name="run-the-application"></a>애플리케이션 실행

 첫 번째 앱에서 본 테이블에는 유용한 기능이 있었습니다. 전체 주식 시세 응용 프로그램은 새로운 기능을 보여줍니다: 주식 데이터와 상승 및 하락으로 색상을 변경 하는 주식을 표시 하는 가로 스크롤 창.

1. **F5를** 눌러 앱을 실행합니다.

     앱을 처음 실행하면 "시장"이 "닫혀"되고 정적 테이블과 스크롤되지 않는 티커 창이 표시됩니다.

1. **오픈 마켓을**선택합니다.

    ![라이브 시세의 스크린 샷.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * **라이브 주식 시세** 상자는 가로로 스크롤하기 시작하고 서버는 주기적으로 무작위로 주가 변동을 방송하기 시작합니다.

    * 주가가 매번 변경될 때마다 앱은 **라이브 스톡 테이블과** **라이브 스톡 시세를**모두 업데이트합니다.

    * 주식의 가격 변화가 긍정적이면 앱은 녹색 배경의 주식을 표시합니다.

    * 변경이 음수이면 앱에 빨간색 배경이 있는 주식이 표시됩니다.

1. **시장 닫기**선택.

    * 테이블 업데이트가 중지됩니다.

    * 시세 차면 스크롤이 중지됩니다.

1. **재설정**을 선택합니다.

    * 모든 재고 데이터가 재설정됩니다.

    * 가격 변경이 시작되기 전에 앱이 초기 상태를 복원합니다.

1. 브라우저에서 URL을 복사하고 다른 두 브라우저를 열고 URL을 주소 표시줄에 붙여넣습니다.

1. 각 브라우저에서 동일한 데이터가 동시에 동적으로 업데이트됩니다.

1. 컨트롤을 선택하면 모든 브라우저가 동시에 동일한 방식으로 응답합니다.

### <a name="live-stock-ticker-display"></a>라이브 스톡 티커 디스플레이

**라이브 스톡 티커** 디스플레이는 CSS `<div>` 스타일에 의해 한 줄로 포맷된 요소의 정렬되지 않은 목록입니다. 앱은 `<li>` 템플릿 문자열의 자리 표시자를 대체하고 `<li>` `<ul>` 요소를 동적으로 추가하여 테이블과 동일한 방식으로 티커를 초기화하고 업데이트합니다. 응용 프로그램은 에서 정렬되지 않은 `animate` 목록의 여백 왼쪽을 변경하려면 jQuery 함수를 사용하여 스크롤을 포함합니다. `<div>`

#### <a name="signalrsample-stocktickerhtml"></a>시그널R.샘플 스톡티커.html

주식 시세 HTML 코드 :

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>시그널R.샘플 스톡티커.css

주식 시세 CSS 코드 :

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>시그널R.샘플 시그널R.스톡티커.js

스크롤할 수 있는 jQuery 코드는 다음과 같은 것입니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>클라이언트가 호출할 수 있는 서버의 추가 메서드

앱에 유연성을 추가하려면 앱에서 호출할 수 있는 추가 방법이 있습니다.

#### <a name="signalrsample-stocktickerhubcs"></a>시그널R.샘플 StockTickerHub.cs

클래스는 `StockTickerHub` 클라이언트가 호출할 수 있는 네 가지 추가 메서드를 정의합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

앱은 `OpenMarket`페이지 `CloseMarket`상단의 단추에 대한 응답으로 를 `Reset` 호출합니다. 한 클라이언트가 모든 클라이언트에 즉시 전파되는 상태의 변경을 트리거하는 패턴을 보여 줍니다. 이러한 각 메서드는 시장 `StockTicker` 상태 변경을 일으키는 클래스의 메서드를 호출한 다음 새 상태를 브로드캐스트합니다.

#### <a name="signalrsample-stocktickercs"></a>시그널R.샘플 StockTicker.cs

`StockTicker` 클래스에서 앱은 `MarketState` 열거형 값을 반환하는 `MarketState` 속성으로 시장 상태를 유지관리합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

`StockTicker` 시장 상태를 변경하는 각 메서드는 클래스가 스레드로 안전해야 하기 때문에 잠금 블록 내에서 수행합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

이 코드가 스레드에서 안전한지 확인하려면 지정된 `_marketState` `MarketState` `volatile`속성을 백업하는 필드:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

`BroadcastMarketStateChange` 및 `BroadcastMarketReset` 메서드는 클라이언트에서 정의된 다른 메서드를 호출하는 것을 제외하고 이미 본 BroadcastStockPrice 메서드와 유사합니다.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>서버가 호출할 수 있는 클라이언트의 추가 기능

이제 `updateStockPrice` 이 함수는 테이블과 티커 디스플레이를 모두 `jQuery.Color` 처리하며 빨간색과 녹색으로 깜박이는 데 사용합니다.

*SignalR.StockTicker.js의* 새로운 기능은 시장 상태에 따라 버튼을 활성화하고 비활성화합니다. 또한 라이브 스톡 **시세** 수평 스크롤을 중지하거나 시작합니다. 많은 함수가 추가되고 `ticker.client`있기 때문에 앱은 [jQuery 확장 함수를](http://api.jquery.com/jQuery.extend/) 사용하여 함수를 추가합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>연결을 설정한 후 추가 클라이언트 설정

클라이언트가 연결을 설정한 후 수행할 몇 가지 추가 작업이 있습니다.

* 시장이 열려 있거나 닫혀 있는지 확인하여 `marketOpened` `marketClosed` 적절한 기능을 호출합니다.

* 서버 메서드 호출을 단추에 연결합니다.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

앱이 연결을 설정할 때까지 서버 메서드는 단추에 연결되지 않습니다. 따라서 코드에서 서버 메서드를 사용할 수 있게 되기 전에 서버 메서드를 호출할 수 없습니다.

## <a name="additional-resources"></a>추가 리소스

이 자습서에서는 서버에서 연결된 모든 클라이언트로 메시지를 브로드캐스트하는 SignalR 응용 프로그램을 프로그래밍하는 방법을 배웠습니다. 이제 모든 클라이언트의 알림에 대한 응답으로 정기적으로 메시지를 브로드캐스트할 수 있습니다. 다중 스레드 싱글톤 인스턴스의 개념을 사용하여 다중 플레이어 온라인 게임 시나리오에서 서버 상태를 유지할 수 있습니다. 예를 들어 [SignalR을 기반으로 하는 ShootR 게임을](https://github.com/NTaylorMullen/ShootR)참조하십시오.

피어 투 피어 통신 시나리오를 보여 주는 자습서의 경우 SignalR 및 [SignalR로 실시간](tutorial-high-frequency-realtime-with-signalr.md) [업데이트시작](introduction-to-signalr.md) 을 참조하십시오.

SignalR에 대한 자세한 내용은 다음 리소스를 참조하십시오.

* [ASP.NET SignalR](../../index.md)
* [시그널R 프로젝트](http://signalr.net/)
* [시그널R GitHub 및 샘플](https://github.com/SignalR/SignalR)
* [시그널러 위키](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 프로젝트 생성
> * 서버 코드 설정
> * 서버 코드 검사
> * 클라이언트 코드 설정
> * 클라이언트 코드 검사
> * 애플리케이션 테스트
> * 사용 가능한 로깅

다음 문서로 이동하여 ASP.NET SignalR 2를 사용하는 실시간 웹 응용 프로그램을 만드는 방법을 알아봅니다.
> [!div class="nextstepaction"]
> [SignalR로 실시간 웹 앱 만들기](real-time-web-applications-with-signalr.md)
