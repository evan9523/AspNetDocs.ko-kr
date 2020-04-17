---
uid: aspnet/overview/owin-and-katana/katana-samples
title: 카타나 샘플 | 마이크로 소프트 문서
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540443"
---
# <a name="katana-samples"></a>Katana 샘플

[로 마이크로 소프트](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana 샘플

**ASP.NET 경로 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
일부 응용 프로그램에서는 Asp.Net 경로 테이블에 OWIN 구성 요소를 OWIN이 아닌 구성 요소와 나란히 연결할 수 있습니다. 이 샘플에서는 Microsoft.Owin.Host.SystemWeb에서 제공하는 RouteCollection 확장 메서드 인 MapOwinPath 및 MapOwinRoute를 사용하는 방법을 보여 주며 있습니다.

**분기 파이프라인 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
OWIN 요청 처리 파이프라인은 선형일 필요는 없으며 다른 방식으로 요청을 처리하기 위해 분기될 수 있습니다. 이 샘플에서는 요청 경로 또는 헤더와 같은 다른 요청 데이터를 기반으로 분기 파이프라인을 구성하는 방법을 보여 주며 있습니다. 이러한 구성 요소는 Microsoft.Owin.Mapping 누젯 패키지에서 사용할 수 있습니다.

**사용자 지정 서버 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
OWIN을 자체 호스팅할 때 사용자 지정 OWIN 서버를 사용하는 방법을 보여 주며

**임베디드 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
일부 OWIN 서버는 자체 프로세스(자체&quot;호스팅)에서&quot;실행할 수 있습니다. 이 샘플에서는 Microsoft.Owin.Hosting nuget 패키지에서 제공하는 도구를 사용하여 OWIN 응용 프로그램을 시작하는 방법을 보여 주며 있습니다.

**헬로월드 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN은 다양한 서버에서 응용 프로그램 이식성을 가능하게 하는 HTTP 서버 API 추상화입니다. 이 샘플에서는 원시 OWIN 추상화 주위에 몇 가지 **간단한 래퍼를** 사용하여 Hello World 응용 프로그램을 작성하고 ASP.NET 같은 웹 서버에서 실행하는 방법을 보여 줍니다.

**안녕하세요 세계 원시 OWIN 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
이 샘플에서는 **원시** OWIN 추상화를 사용하여 Hello World 응용 프로그램을 작성하고 Asp.Net 같은 웹 서버에서 실행하는 방법을 보여 줍니다.

**시그널R 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
OWIN / 카타나를 사용하여 신호기를 자체 호스트하는 방법을 보여줍니다. 자체 호스팅 SignalR에 대한 자세한 내용은 [자습서: SignalR 자체 호스트](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)를 참조하십시오.

**정적 파일 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
OWIN / 카타나를 사용하여 정적 파일에 대한 HTTP 요청을 지원하는 방법을 보여줍니다.

**웹 API** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
이 샘플에서는 IIS에서 OWIN을 호스팅하고 OWIN 파이프라인에 웹 API를 추가하는 방법을 보여 주며, 이 샘플에서는 OWIN 파이프라인에 웹 API를 추가합니다.

**웹 소켓 샘플** | [소스 코드](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
[System.Net.WebSockets.WebSocket 클래스를](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) 사용하여 OWIN에서 웹 소켓을 지원하는 방법을 보여 주며
