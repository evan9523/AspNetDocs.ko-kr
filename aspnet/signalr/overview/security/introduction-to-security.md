---
uid: signalr/overview/security/introduction-to-security
title: SignalR 보안 소개 | Microsoft Docs
author: bradygaster
description: SignalR 응용 프로그램을 개발할 때 고려해 야 하는 보안 문제에 대해 설명 합니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345450"
---
# <a name="introduction-to-signalr-security"></a>SignalR 보안 소개

[Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 SignalR 응용 프로그램을 개발할 때 고려해 야 하는 보안 문제에 대해 설명 합니다.
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

## <a name="overview"></a>개요

이 문서는 다음 섹션으로 구성됩니다.

- [SignalR 보안 개념](#concepts)

    - [인증 및 권한 부여](#authentication)
    - [연결 토큰](#connectiontoken)
    - [다시 연결할 때 다시 가입 하기 그룹](#rejoingroup)
- [SignalR에서 교차 사이트 요청 위조를 방지 하는 방법](#csrf)
- [SignalR 보안 권장 사항](#recommendations)

    - [SSL (Secure Socket Layers) 프로토콜](#ssl)
    - [그룹을 보안 메커니즘으로 사용 하지 마십시오.](#groupsecurity)
    - [클라이언트에서 입력을 안전 하 게 처리](#input)
    - [활성 연결을 사용 하 여 사용자 상태 변경 조정](#reconcile)
    - [자동으로 생성 된 JavaScript 프록시 파일](#autogen)
    - [예외](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR 보안 개념

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>인증 및 권한 부여

SignalR는 사용자를 인증 하는 기능을 제공 하지 않습니다. 대신 응용 프로그램의 기존 인증 구조에 SignalR 기능을 통합 합니다. 응용 프로그램에서 평소와 같이 사용자를 인증 하 고 SignalR 코드에서 인증 결과를 사용할 수 있습니다. 예를 들어 ASP.NET forms 인증을 사용 하 여 사용자를 인증 한 다음 허브에서 메서드를 호출할 수 있는 권한이 있는 사용자 또는 역할을 강제로 적용할 수 있습니다. 허브에서 사용자 이름 또는 사용자가 역할에 속하는지 여부와 같은 인증 정보를 클라이언트에 전달할 수도 있습니다.

SignalR는 허브 또는 메서드에 대 한 액세스 권한이 있는 사용자를 지정 하는 [권한 부여](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 특성을 제공 합니다. 허브 또는 허브의 특정 메서드에 권한 부여 특성을 적용 합니다. 권한 부여 특성이 없으면 허브에 연결 된 클라이언트에서 허브의 모든 공용 메서드를 사용할 수 있습니다. 허브에 대 한 자세한 내용은 [SignalR hubs에 대 한 인증 및 권한 부여](hub-authorization.md)를 참조 하세요.

`Authorize`특성을 허브에는 적용 하지만 영구 연결은 적용 하지 않습니다. 를 사용할 때 권한 부여 규칙을 적용 하려면 `PersistentConnection` 메서드를 재정의 해야 합니다 `AuthorizeRequest` . 영구 연결에 대 한 자세한 내용은 [SignalR 영구 연결에 대 한 인증 및 권한 부여](persistent-connection-authorization.md)를 참조 하세요.

<a id="connectiontoken"></a>

### <a name="connection-token"></a>연결 토큰

SignalR는 보낸 사람 id의 유효성을 검사 하 여 악의적인 명령이 실행 되는 위험을 완화 합니다. 각 요청에 대해 클라이언트와 서버는 인증 된 사용자에 대 한 연결 id와 사용자 이름을 포함 하는 연결 토큰을 전달 합니다. 연결 id는 연결 된 각 클라이언트를 고유 하 게 식별 합니다. 서버는 새 연결을 만들 때 연결 id를 임의로 생성 하 고 연결 기간 동안 해당 id를 유지 합니다. 웹 응용 프로그램에 대 한 인증 메커니즘은 사용자 이름을 제공 합니다. SignalR는 암호화 및 디지털 서명을 사용 하 여 연결 토큰을 보호 합니다.

![](introduction-to-security/_static/image2.png)

각 요청에 대해 서버는 토큰 내용의 유효성을 검사 하 여 요청이 지정 된 사용자에 게 제공 되는지 확인 합니다. 사용자 이름은 연결 id와 일치 해야 합니다. SignalR는 연결 id와 사용자 이름의 유효성을 모두 검사 하 여 악의적인 사용자가 다른 사용자를 쉽게 가장할 수 없도록 합니다. 서버에서 연결 토큰의 유효성을 검사할 수 없는 경우 요청이 실패 합니다.

![](introduction-to-security/_static/image4.png)

연결 id가 확인 프로세스의 일부 이기 때문에 다른 사용자에 게 한 사용자의 연결 id를 표시 하거나 쿠키와 같은 클라이언트에 값을 저장 해서는 안 됩니다.

#### <a name="connection-tokens-vs-other-token-types"></a>연결 토큰과 기타 토큰 유형 비교

연결 토큰은 세션 토큰 또는 인증 토큰으로 나타나므로 노출 되는 경우 위험을 초래 하는 보안 도구에 의해 플래그가 지정 되는 경우도 있습니다.

SignalR의 연결 토큰이 인증 토큰이 아닙니다. 이 요청은이 요청을 수행 하는 사용자가 연결을 만든 사용자와 동일한 지 확인 하는 데 사용 됩니다. ASP.NET SignalR에서 연결을 서버 간에 이동할 수 있으므로 연결 토큰이 필요 합니다. 토큰은 연결을 특정 사용자와 연결 하지만 요청 하는 사용자의 id를 어설션 하지 않습니다. SignalR 요청을 제대로 인증 하려면 쿠키 또는 전달자 토큰과 같은 사용자의 id를 어설션하는 다른 토큰이 있어야 합니다. 그러나 연결 토큰 자체는 해당 사용자가 요청을 수행 하는 클레임을 요구 하지 않으며 토큰 내에 포함 된 연결 ID만 해당 사용자와 연결 됩니다.

연결 토큰은 자체의 인증 클레임을 제공 하지 않으므로 "세션" 또는 "인증" 토큰으로 간주 되지 않습니다. 요청의 사용자 id와 토큰에 저장 된 id가 일치 하지 않기 때문에 지정 된 사용자의 연결 토큰을 사용 하 고 다른 사용자 (또는 인증 되지 않은 요청)로 인증 된 요청에서이를 재생 하면 실패 합니다.

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>다시 연결할 때 다시 가입 하기 그룹

기본적으로 SignalR 응용 프로그램은 연결 시간이 초과 되기 전에 연결을 삭제 하 고 다시 설정 하는 경우와 같이 일시적인 중단에서 다시 연결 하는 경우 사용자를 적절 한 그룹에 자동으로 다시 할당 합니다. 다시 연결 하는 경우 클라이언트는 연결 id 및 할당 된 그룹을 포함 하는 그룹 토큰을 전달 합니다. 그룹 토큰은 디지털 서명 되 고 암호화 됩니다. 다시 연결한 후 클라이언트는 동일한 연결 id를 유지 합니다. 따라서 다시 연결 된 클라이언트에서 전달 된 연결 id는 클라이언트에서 사용 하는 이전 연결 id와 일치 해야 합니다. 이렇게 확인 하면 악의적인 사용자가 다시 연결할 때 권한이 없는 그룹에 참가 하도록 요청을 전달할 수 없습니다.

그러나 그룹 토큰이 만료 되지 않는다는 점에 유의 해야 합니다. 사용자가 이전에 그룹에 속해 있지만 해당 그룹에서 금지 된 경우 해당 사용자는 금지 된 그룹을 포함 하는 그룹 토큰을 모방할 수 있습니다. 어떤 그룹에 속한 사용자를 안전 하 게 관리 해야 하는 경우에는 데이터베이스와 같은 해당 데이터를 서버에 저장 해야 합니다. 그런 다음 사용자가 그룹에 속하는지 여부를 서버에서 확인 하는 논리를 응용 프로그램에 추가 합니다. 그룹 멤버 자격을 확인 하는 예제는 [그룹 작업](../guide-to-the-api/working-with-groups.md)을 참조 하세요.

자동 다시 가입 하기 그룹은 일시적으로 중단 된 후 연결이 다시 연결 될 때만 적용 됩니다. 응용 프로그램에서 다른 위치로 이동 하거나 응용 프로그램을 다시 시작 하 여 사용자의 연결을 끊으면 응용 프로그램에서 해당 사용자를 올바른 그룹에 추가 하는 방법을 처리 해야 합니다. 자세한 내용은 [그룹 작업](../guide-to-the-api/working-with-groups.md)을 참조 하세요.

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR에서 교차 사이트 요청 위조를 방지 하는 방법

CSRF (교차 사이트 요청 위조)는 악의적인 사이트에서 사용자가 현재 로그인 한 취약 한 사이트로 요청을 보내는 공격입니다. SignalR는 악의적인 사이트가 SignalR 응용 프로그램에 대 한 유효한 요청을 만들 가능성이 거의 없도록 하 여 CSRF를 방지 합니다.

### <a name="description-of-csrf-attack"></a>CSRF 공격에 대 한 설명

CSRF 공격의 예는 다음과 같습니다.

1. 사용자는 폼 인증을 사용 하 여 www.example.com에 로그인 합니다.
2. 서버에서 사용자를 인증 합니다. 서버 응답에는 인증 쿠키가 포함 되어 있습니다.
3. 로그 아웃 하지 않으면 사용자가 악성 웹 사이트를 방문 합니다. 이 악의적인 사이트는 다음과 같은 HTML 양식을 포함 합니다.

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   양식 작업은 악의적인 사이트가 아닌 취약 한 사이트로 게시 됩니다. CSRF의 "교차 사이트" 부분입니다.
4. 사용자가 제출 단추를 클릭 합니다. 브라우저에는 요청과 함께 인증 쿠키가 포함 되어 있습니다.
5. 이 요청은 사용자의 인증 컨텍스트로 example.com 서버에서 실행 되며 인증 된 사용자가 수행할 수 있는 모든 작업을 수행할 수 있습니다.

이 예에서는 사용자가 양식 단추를 클릭 해야 하지만, 악의적인 페이지가 SignalR 응용 프로그램에 AJAX 요청을 보내는 스크립트를 쉽게 실행할 수 있습니다. 또한 SSL을 사용 하더라도 악의적인 사이트에서 "https://" 요청을 보낼 수 있으므로 CSRF 공격을 방지 하지 않습니다.

일반적으로 브라우저는 대상 웹 사이트에 관련 된 모든 쿠키를 보내기 때문에 인증에 쿠키를 사용 하는 웹 사이트에 대해 CSRF 공격을 수행할 수 있습니다. 그러나 CSRF 공격은 쿠키를 악용 하는 것으로 제한 되지 않습니다. 예를 들어, 기본 및 다이제스트 인증에도 취약 합니다. 사용자가 기본 또는 다이제스트 인증을 사용 하 여 로그인 한 후에는 세션이 종료 될 때까지 브라우저에서 자동으로 자격 증명을 보냅니다.

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR에서 가져온 CSRF 완화

SignalR는 악의적인 사이트에서 응용 프로그램에 대 한 올바른 요청을 만들지 못하도록 다음 단계를 수행 합니다. SignalR는 기본적으로 이러한 단계를 수행 하므로 코드에서 작업을 수행할 필요가 없습니다.

- **도메인 간 요청 사용 안 함** SignalR는 도메인 간 요청을 사용 하지 않도록 설정 하 여 사용자가 외부 도메인에서 SignalR 끝점을 호출 하지 못하도록 합니다. SignalR는 외부 도메인의 모든 요청을 유효 하지 않은 것으로 간주 하 고 요청을 차단 합니다. 이 기본 동작을 유지 하는 것이 좋습니다. 그렇지 않으면 악의적인 사이트에서 사용자가 사이트에 명령을 전송 하도록 유도할 수 있습니다. 도메인 간 요청을 사용 해야 하     [는 경우 도메인 간 연결을 설정 하는 방법](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) 을 참조 하세요.
- **쿠키가 아닌 쿼리 문자열의 연결 토큰을 전달 합니다** . SignalR는 쿠키 대신 쿼리 문자열 값으로 연결 토큰을 전달 합니다. 악의적인 코드가 발견 되 면 브라우저에서 실수로 연결 토큰을 전달할 수 있으므로 연결 토큰을 쿠키에 저장 하는 것은 안전 하지 않습니다. 또한 쿼리 문자열에 연결 토큰을 전달 하면 연결 토큰이 현재 연결을 넘어 지속 되지 않습니다. 따라서 악의적인 사용자가 다른 사용자의 인증 자격 증명을 사용 하 여 요청을 수행할 수 없습니다.
- **연결 토큰 확인**     [연결 토큰](#connectiontoken) 섹션에 설명 된 대로 서버는 인증 된 각 사용자와 연결 된 연결 id를 알고 있습니다. 서버는 사용자 이름과 일치 하지 않는 연결 id에서 요청을 처리 하지 않습니다. 악의적인 사용자가 사용자 이름과 현재 임의로 생성 된 연결 id를 알고 있어야 하기 때문에 악의적인 사용자가 유효한 요청을 추측할 가능성이 거의 없습니다. 연결이 종료 되는 즉시 해당 연결 id는 유효 하지 않게 됩니다. 익명 사용자는 중요 한 정보에 액세스할 수 없습니다.

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR 보안 권장 사항

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>SSL (Secure Socket Layers) 프로토콜

SSL 프로토콜은 암호화를 사용 하 여 클라이언트와 서버 간의 데이터 전송을 보호 합니다. SignalR 응용 프로그램이 클라이언트와 서버 간에 중요 한 정보를 전송 하는 경우 전송에 SSL을 사용 합니다. SSL을 설정 하는 방법에 대 한 자세한 내용은 [IIS 7에서 ssl을 설정 하는 방법](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)을 참조 하십시오.

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>그룹을 보안 메커니즘으로 사용 하지 마십시오.

그룹은 관련 사용자를 수집 하는 편리한 방법 이지만 중요 한 정보에 대 한 액세스를 제한 하는 보안 메커니즘은 아닙니다. 이는 사용자가 다시 연결 하는 동안 그룹을 자동으로 다시 조인할 수 있는 경우에 특히 그렇습니다. 대신 권한 있는 사용자를 역할에 추가 하 고 허브 메서드에 대 한 액세스를 해당 역할의 멤버로 제한 하는 것이 좋습니다. 역할에 따라 액세스를 제한 하는 예제는 [SignalR Hubs에 대 한 인증 및 권한 부여](hub-authorization.md)를 참조 하세요. 다시 연결할 때 그룹에 대 한 사용자 액세스를 확인 하는 예제는 [그룹 작업](../guide-to-the-api/working-with-groups.md)을 참조 하세요.

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>클라이언트에서 입력을 안전 하 게 처리

악의적인 사용자가 다른 사용자에 게 스크립트를 전송 하지 않도록 하려면 브로드캐스트할 클라이언트의 모든 입력을 다른 클라이언트로 인코딩해야 합니다. SignalR 응용 프로그램에는 다양 한 유형의 클라이언트가 있을 수 있으므로 서버 대신 수신 클라이언트에서 메시지를 인코딩해야 합니다. 따라서 HTML 인코딩은 웹 클라이언트에 대해서는 작동 하지만 다른 유형의 클라이언트에 대해서는 작동 하지 않습니다. 예를 들어 채팅 메시지를 표시 하는 웹 클라이언트 메서드는 함수를 호출 하 여 사용자 이름과 메시지를 안전 하 게 처리 `html()` 합니다.

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>활성 연결을 사용 하 여 사용자 상태 변경 조정

활성 연결이 존재 하는 동안 사용자의 인증 상태가 변경 되는 경우 사용자에 게 "활성 SignalR 연결 중에 사용자 id가 변경 될 수 없습니다." 라는 오류가 표시 됩니다. 이 경우 응용 프로그램은 연결 id와 사용자 이름이 조정 되도록 서버에 다시 연결 해야 합니다. 예를 들어, 활성 연결이 존재 하는 동안 사용자가 로그 아웃할 수 있도록 허용 하는 경우, 연결의 사용자 이름은 다음 요청에 대해 전달 된 이름과 더 이상 일치 하지 않습니다. 사용자가 로그 아웃 하기 전에 연결을 중지 하 고 다시 시작 하는 것이 좋습니다.

그러나 대부분의 응용 프로그램은 연결을 수동으로 중지 하 고 시작할 필요가 없다는 점에 유의 해야 합니다. 응용 프로그램이 Web Forms 응용 프로그램 또는 MVC 응용 프로그램의 기본 동작과 같이 로그 아웃 한 후 개별 페이지로 사용자를 리디렉션하거나, 로그 아웃 후 현재 페이지를 새로 고치면 활성 연결이 자동으로 끊어지고 추가 작업이 필요 하지 않습니다.

다음 예에서는 사용자 상태가 변경 된 경우 연결을 중지 하 고 시작 하는 방법을 보여 줍니다.

[!code-html[Main](introduction-to-security/samples/sample3.html)]

또는 사이트에서 폼 인증을 사용 하 여 상대 (sliding) 만료를 사용 하 고 인증 쿠키를 유효 하 게 유지 하는 작업이 없는 경우 사용자의 인증 상태가 변경 될 수 있습니다. 이 경우 사용자는 로그 아웃 되며 사용자 이름은 더 이상 연결 토큰의 사용자 이름과 일치 하지 않습니다. 웹 서버에서 리소스를 주기적으로 요청 하 여 인증 쿠키를 유효 하 게 유지 하는 스크립트를 추가 하면이 문제를 해결할 수 있습니다. 다음 예에서는 30 분 마다 리소스를 요청 하는 방법을 보여 줍니다.

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>자동으로 생성 된 JavaScript 프록시 파일

각 사용자에 대해 JavaScript 프록시 파일에 모든 허브 및 메서드를 포함 하지 않으려면 파일의 자동 생성을 사용 하지 않도록 설정할 수 있습니다. 여러 허브 및 방법이 있지만 모든 사용자가 모든 방법을 인식 하지 않으려는 경우이 옵션을 선택할 수 있습니다. 자동 생성을 사용 하지 않도록 설정 하려면 **EnableJavaScriptProxies** 을 **false**로 설정 합니다.

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

JavaScript 프록시 파일에 대 한 자세한 내용은 생성 된 [프록시와이를 수행](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)하는 작업을 참조 하세요. <a id="exceptions"></a>

### <a name="exceptions"></a>예외

개체가 중요 한 정보를 클라이언트에 노출할 수 있으므로 예외 개체를 클라이언트에 전달 하지 않아야 합니다. 대신 관련 오류 메시지를 표시 하는 메서드를 클라이언트에서 호출 합니다.

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
