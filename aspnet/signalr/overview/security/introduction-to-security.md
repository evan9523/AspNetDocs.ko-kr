---
uid: signalr/overview/security/introduction-to-security
title: 시그널R 시큐리티 소개 | 마이크로 소프트 문서
author: bradygaster
description: SignalR 응용 프로그램을 개발할 때 고려해야 할 보안 문제에 대해 설명합니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675810"
---
# <a name="introduction-to-signalr-security"></a>SignalR 보안 소개

[패트릭 플레처,](https://github.com/pfletcher) [톰 피츠매켄](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 SignalR 응용 프로그램을 개발할 때 고려해야 할 보안 문제에 대해 설명합니다.
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

## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [시그널R 보안 개념](#concepts)

    - [인증 및 권한 부여](#authentication)
    - [연결 토큰](#connectiontoken)
    - [다시 연결할 때 그룹 재가입](#rejoingroup)
- [SignalR이 사이트 간 요청 위조를 방지하는 방법](#csrf)
- [시그널R 보안 권장 사항](#recommendations)

    - [보안 소켓 레이어(SSL) 프로토콜](#ssl)
    - [그룹을 보안 메커니즘으로 사용하지 마십시오.](#groupsecurity)
    - [클라이언트의 입력을 안전하게 처리](#input)
    - [활성 연결로 사용자 상태 변경 조정](#reconcile)
    - [자동으로 생성된 자바스크립트 프록시 파일](#autogen)
    - [예외](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>시그널R 보안 개념

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>인증 및 권한 부여

SignalR은 사용자를 인증하기 위한 기능을 제공하지 않습니다. 대신 SignalR 기능을 응용 프로그램의 기존 인증 구조에 통합합니다. 응용 프로그램에서 평소와 같이 사용자를 인증하고 SignalR 코드에서 인증 결과를 사용합니다. 예를 들어 ASP.NET 양식 인증을 사용하여 사용자를 인증한 다음 허브에서 메서드를 호출할 권한이 있는 사용자 또는 역할을 적용하여 사용자를 인증할 수 있습니다. 허브에서 사용자 이름 또는 사용자가 역할에 속하는지 여부와 같은 인증 정보를 클라이언트에 전달할 수도 있습니다.

SignalR은 허브 또는 메서드에 액세스할 수 있는 사용자를 지정하는 [권한 부여](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 특성을 제공합니다. 허브의 허브 또는 특정 메서드에 권한 부여 특성을 적용합니다. Authorize 특성이 없으면 허브에 연결된 클라이언트에서 허브의 모든 공용 메서드를 사용할 수 있습니다. 허브에 대한 자세한 내용은 [SignalR 허브에 대한 인증 및 권한 부여를](hub-authorization.md)참조하십시오.

영구 연결은 `Authorize` 적용하지 않고 허브에 특성을 적용합니다. 권한 부여 규칙을 적용하려면 `PersistentConnection` 메서드를 `AuthorizeRequest` 재정의해야 합니다. 영구 연결에 대한 자세한 내용은 [SignalR 영구 연결에 대한 인증 및 권한 부여를](persistent-connection-authorization.md)참조하십시오.

<a id="connectiontoken"></a>

### <a name="connection-token"></a>연결 토큰

SignalR은 보낸 사람의 ID를 확인하여 악의적인 명령을 실행하는 위험을 완화합니다. 각 요청에 대해 클라이언트와 서버는 인증된 사용자에 대한 연결 ID와 사용자 이름을 포함하는 연결 토큰을 전달합니다. 연결 ID는 연결된 각 클라이언트를 고유하게 식별합니다. 서버는 새 연결을 만들 때 연결 ID를 임의로 생성하고 연결 기간 동안 해당 ID를 유지합니다. 웹 응용 프로그램에 대한 인증 메커니즘은 사용자 이름을 제공합니다. SignalR는 암호화 및 디지털 서명을 사용하여 연결 토큰을 보호합니다.

![](introduction-to-security/_static/image2.png)

각 요청에 대해 서버는 토큰의 내용의 유효성을 검사하여 요청이 지정된 사용자로부터 오는지 확인합니다. 사용자 이름은 연결 ID와 일치해야 합니다. SignalR은 연결 ID와 사용자 이름을 모두 검증하여 악의적인 사용자가 다른 사용자를 쉽게 가장하지 못하도록 합니다. 서버가 연결 토큰의 유효성을 검사할 수 없는 경우 요청이 실패합니다.

![](introduction-to-security/_static/image4.png)

연결 ID는 확인 프로세스의 일부이므로 한 사용자의 연결 ID를 다른 사용자에게 공개하거나 쿠키와 같이 클라이언트에 값을 저장해서는 안 됩니다.

#### <a name="connection-tokens-vs-other-token-types"></a>연결 토큰 과 다른 토큰 유형

연결 토큰은 세션 토큰 또는 인증 토큰으로 나타나므로 보안 도구에 의해 플래그가 지정되는 경우가 있습니다.

SignalR의 연결 토큰은 인증 토큰이 아닙니다. 이 요청을 하는 사용자가 연결을 만든 사용자와 동일한지 확인하는 데 사용됩니다. ASP.NET SignalR은 연결을 서버 간에 이동할 수 있기 때문에 연결 토큰이 필요합니다. 토큰은 특정 사용자와 연결을 연결하지만 요청을 하는 사용자의 ID를 어설션하지 않습니다. SignalR 요청을 제대로 인증하려면 쿠키 또는 베어러 토큰과 같이 사용자의 ID를 어설션하는 다른 토큰이 있어야 합니다. 그러나 연결 토큰 자체는 해당 사용자가 요청했다는 주장을 하지 않으며 토큰에 포함된 연결 ID가 해당 사용자와 연결되어 있다고 주장하지 않습니다.

연결 토큰은 자체 인증 클레임을 제공하지 않으므로 "세션" 또는 "인증" 토큰으로 간주되지 않습니다. 요청의 사용자 ID와 토큰에 저장된 ID가 일치하지 않기 때문에 지정된 사용자의 연결 토큰을 다른 사용자(또는 인증되지 않은 요청)로 인증된 요청에서 재생하면 실패합니다.

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>다시 연결할 때 그룹 재가입

기본적으로 SignalR 응용 프로그램은 연결이 끊어지고 연결이 시간 만료되기 전에 다시 설정되는 경우와 같이 일시적인 중단으로 다시 연결할 때 사용자를 해당 그룹에 자동으로 다시 할당합니다. 다시 연결하면 클라이언트는 연결 ID와 할당된 그룹을 포함하는 그룹 토큰을 전달합니다. 그룹 토큰은 디지털 서명되고 암호화됩니다. 클라이언트는 다시 연결한 후 동일한 연결 ID를 유지합니다. 따라서 다시 연결된 클라이언트에서 전달된 연결 ID는 클라이언트에서 사용한 이전 연결 ID와 일치해야 합니다. 이 확인은 악의적인 사용자가 다시 연결할 때 권한이 있는 그룹에 가입하라는 요청을 전달하지 못하도록 합니다.

그러나 그룹 토큰이 만료되지 않는다는 점에 유의해야 합니다. 사용자가 과거에 그룹에 속해 있지만 해당 그룹에서 금지된 경우 해당 사용자는 금지된 그룹을 포함하는 그룹 토큰을 모방할 수 있습니다. 어떤 그룹에 속한 사용자를 안전하게 관리해야 하는 경우 데이터베이스와 같이 서버에 해당 데이터를 저장해야 합니다. 그런 다음 사용자가 그룹에 속하는지 여부를 서버에서 확인하는 논리를 응용 프로그램에 추가합니다. 그룹 구성원 자격 확인의 예는 [그룹 작업](../guide-to-the-api/working-with-groups.md)참조

그룹이 자동으로 다시 연결되면 일시적으로 중단된 후 연결이 다시 연결된 경우에만 적용됩니다. 사용자가 응용 프로그램에서 멀리 이동하여 연결이 끊어지거나 응용 프로그램이 다시 시작되는 경우 응용 프로그램에서 해당 사용자를 올바른 그룹에 추가하는 방법을 처리해야 합니다. 자세한 내용은 [그룹 작업을](../guide-to-the-api/working-with-groups.md)참조하십시오.

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR이 사이트 간 요청 위조를 방지하는 방법

CSRF(교차 사이트 요청 위조)는 악의적인 사이트가 현재 로그인되어 있는 취약한 사이트에 요청을 보내는 공격입니다. SignalR은 악의적인 사이트가 SignalR 응용 프로그램에 대한 유효한 요청을 만들 가능성은 매우 낮아서 CSRF를 방지합니다.

### <a name="description-of-csrf-attack"></a>CSRF 공격에 대한 설명

CSRF 공격의 예는 다음과 같습니다.

1. 사용자는 양식 인증을 사용하여 www.example.com 로그인합니다.
2. 서버는 사용자를 인증합니다. 서버의 응답에는 인증 쿠키가 포함됩니다.
3. 로그아웃하지 않고 사용자는 악의적인 웹 사이트를 방문합니다. 이 악성 사이트에는 다음과 같은 HTML 양식이 포함되어 있습니다.

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   양식 작업은 악의적인 사이트가 아닌 취약한 사이트에 게시됩니다. CSRF의 "교차 사이트" 부분입니다.
4. 사용자가 제출 단추를 클릭합니다. 브라우저에는 요청이 포함된 인증 쿠키가 포함됩니다.
5. 요청은 사용자의 인증 컨텍스트를 사용하여 example.com 서버에서 실행되며 인증된 사용자가 수행할 수 있는 모든 작업을 수행할 수 있습니다.

이 예제에서는 사용자가 양식 단추를 클릭해야 하지만 악의적인 페이지는 SignalR 응용 프로그램에 AJAX 요청을 보내는 스크립트를 쉽게 실행할 수 있습니다. 또한 악의적인 사이트가 "https://" 요청을 보낼 수 있으므로 SSL을 사용하면 CSRF 공격을 방지할 수 없습니다.

일반적으로 CSRF 공격은 브라우저가 대상 웹 사이트에 모든 관련 쿠키를 보내기 때문에 인증을 위해 쿠키를 사용하는 웹 사이트에 대해 가능합니다. 그러나 CSRF 공격은 쿠키 를 악용하는 것에 국한되지 않습니다. 예를 들어 기본 및 다이제스트 인증도 취약합니다. 사용자가 Basic 또는 다이제스트 인증으로 로그인하면 브라우저는 세션이 끝날 때까지 자격 증명을 자동으로 보냅니다.

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR에서 취한 CSRF 완화

SignalR은 악의적인 사이트가 응용 프로그램에 유효한 요청을 만들지 못하도록 다음 단계를 수행합니다. SignalR은 기본적으로 이러한 단계를 수행하므로 코드에서 작업을 수행할 필요가 없습니다.

- **교차 도메인 요청 사용 안 함** SignalR은 교차 도메인 요청을 비활성화하여 사용자가 외부 도메인에서 SignalR 끝점을 호출하지 못하도록 합니다. SignalR은 외부 도메인의 모든 요청을 유효하지 않은 것으로 간주하고 요청을 차단합니다. 이 기본 동작을 유지하는 것이 좋습니다. 그렇지 않으면 악의적인 사이트가 사용자를 속여 사이트로 명령을 보낼 수 있습니다. 교차 도메인 요청을 사용해야 하는 경우 도메인 [간 연결을 설정하는 방법을 참조하세요.](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)
- **쿠키가 아닌 쿼리 문자열에 연결 토큰 전달** SignalR은 연결 토큰을 쿠키가 아닌 쿼리 문자열 값으로 전달합니다. 브라우저가 악성 코드가 발생할 때 연결 토큰을 실수로 전달할 수 있기 때문에 쿠키에 연결 토큰을 저장하는 것은 안전하지 않습니다. 또한 쿼리 문자열에서 연결 토큰을 전달하면 연결 토큰이 현재 연결을 넘어 계속 유지되지 않습니다. 따라서 악의적인 사용자는 다른 사용자의 인증 자격 증명으로 요청을 할 수 없습니다.
- **연결 토큰 확인** [연결 토큰](#connectiontoken) 섹션에 설명된 대로 서버는 인증된 각 사용자와 연결된 연결 ID를 알고 있습니다. 서버는 사용자 이름과 일치하지 않는 연결 ID의 요청을 처리하지 않습니다. 악의적인 사용자가 사용자 이름과 현재 임의로 생성된 연결 ID를 알아야 하기 때문에 악의적인 사용자가 유효한 요청을 추측할 가능성은 거의 없습니다. 연결이 종료되자마자 해당 연결 ID가 유효하지 않게 됩니다. 익명 사용자는 중요한 정보에 액세스할 수 없어야 합니다.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>시그널R 보안 권장 사항

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>보안 소켓 레이어(SSL) 프로토콜

SSL 프로토콜은 암호화를 사용하여 클라이언트와 서버 간에 데이터 전송을 보호합니다. SignalR 응용 프로그램이 클라이언트와 서버 간에 중요한 정보를 전송하는 경우 전송에 SSL을 사용합니다. SSL 설정에 대한 자세한 내용은 [IIS 7에서 SSL을 설정하는 방법을](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)참조하십시오.

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>그룹을 보안 메커니즘으로 사용하지 마십시오.

그룹은 관련 사용자를 수집하는 편리한 방법이지만 중요한 정보에 대한 액세스를 제한하는 안전한 메커니즘은 아닙니다. 사용자가 다시 연결하는 동안 자동으로 그룹에 다시 참여할 수 있는 경우에 특히 그렇습니다. 대신 권한 있는 사용자를 역할에 추가하고 허브 메서드에 대한 액세스를 해당 역할의 구성원으로만 제한하는 것이 좋습니다. 역할에 따라 액세스를 제한하는 예는 [SignalR Hubs에 대한 인증 및 권한 부여를](hub-authorization.md)참조하십시오. 다시 연결할 때 그룹에 대한 사용자 액세스를 확인하는 예는 [그룹 작업](../guide-to-the-api/working-with-groups.md)작업을 참조하십시오.

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>클라이언트의 입력을 안전하게 처리

악의적인 사용자가 다른 사용자에게 스크립트를 보내지 않도록 하려면 다른 클라이언트로 브로드캐스트하기 위한 클라이언트의 모든 입력을 인코딩해야 합니다. SignalR 응용 프로그램에는 다양한 유형의 클라이언트가 있을 수 있으므로 서버가 아닌 수신 클라이언트에서 메시지를 인코딩해야 합니다. 따라서 HTML 인코딩은 웹 클라이언트에서 작동하지만 다른 유형의 클라이언트에는 적용되지 않습니다. 예를 들어 채팅 메시지를 표시하는 웹 클라이언트 메서드는 함수를 호출하여 사용자 `html()` 이름과 메시지를 안전하게 처리합니다.

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>활성 연결로 사용자 상태 변경 조정

활성 연결이 있는 동안 사용자의 인증 상태가 변경되면 사용자는 "활성 SignalR 연결 중에 사용자 ID를 변경할 수 없습니다"라는 오류가 표시됩니다. 이 경우 응용 프로그램이 서버에 다시 연결하여 연결 ID와 사용자 이름이 조정되었는지 확인해야 합니다. 예를 들어 응용 프로그램에서 활성 연결이 있는 동안 사용자가 로그아웃할 수 있도록 허용하는 경우 연결의 사용자 이름은 더 이상 다음 요청에 대해 전달된 이름과 일치하지 않습니다. 사용자가 로그아웃하기 전에 연결을 중지한 다음 다시 시작해야 합니다.

그러나 대부분의 응용 프로그램은 수동으로 연결을 중지하고 시작할 필요가 없습니다. 응용 프로그램이 웹 폼 응용 프로그램 또는 MVC 응용 프로그램의 기본 동작과 같이 로그아웃한 후 사용자를 별도의 페이지로 리디렉션하거나 로그아웃 한 후 현재 페이지를 새로 고치는 경우 활성 연결이 자동으로 끊어지고 추가 작업이 필요하지 않습니다.

다음 예제에서는 사용자 상태가 변경된 경우 연결을 중지하고 시작하는 방법을 보여 주며 있습니다.

[!code-html[Main](introduction-to-security/samples/sample3.html)]

또는 사이트에서 양식 인증을 사용하여 슬라이딩 만료를 사용하고 인증 쿠키를 유효하게 유지하는 활동이 없는 경우 사용자의 인증 상태가 변경될 수 있습니다. 이 경우 사용자는 로그아웃되고 사용자 이름은 더 이상 연결 토큰의 사용자 이름과 일치하지 않습니다. 인증 쿠키를 유효하게 유지하기 위해 웹 서버의 리소스를 주기적으로 요청하는 스크립트를 추가하여 이 문제를 해결할 수 있습니다. 다음 예제에서는 30분마다 리소스를 요청하는 방법을 보여 주며, 이 예제에서는 리소스를 요청하는 방법을 보여 주어 있습니다.

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>자동으로 생성된 자바스크립트 프록시 파일

각 사용자에 대한 JavaScript 프록시 파일에 모든 허브와 메서드를 포함하지 않으려면 파일의 자동 생성을 비활성화할 수 있습니다. 허브와 메서드가 여러 개 있지만 모든 사용자가 모든 메서드를 인식하지 않도록 하려면 이 옵션을 선택할 수 있습니다. **인에이블자바스크립트프록시스를** **false로**설정하여 자동 생성을 비활성화합니다.

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

JavaScript 프록시 파일에 대한 자세한 내용은 [생성된 프록시 및 수행 되는 작업을](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)참조하십시오. <a id="exceptions"></a>

### <a name="exceptions"></a>예외

개체가 중요한 정보를 클라이언트에 노출시킬 수 있으므로 예외 개체를 클라이언트에 전달하지 않아야 합니다. 대신 관련 오류 메시지를 표시하는 클라이언트의 메서드를 호출합니다.

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
