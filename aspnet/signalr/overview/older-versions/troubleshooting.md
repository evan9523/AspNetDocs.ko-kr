---
uid: signalr/overview/older-versions/troubleshooting
title: 시그널R 트러블슈팅(시그널R 1.x) | 마이크로 소프트 문서
author: bradygaster
description: 이 문서에서는 SignalR 응용 프로그램 개발과 관련된 일반적인 문제에 대해 설명합니다.
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543095"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>SignalR 문제 해결(SignalR 1.x)

로 [패트릭 플레처](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 SignalR의 일반적인 문제 해결 문제에 대해 설명합니다.

이 문서에는 다음 섹션이 포함되어 있습니다.

- [클라이언트와 서버 간의 호출 메서드가 자동으로 실패합니다.](#connection)
- [기타 연결 문제](#other)
- [컴파일 및 서버 측 오류](#server)
- [비주얼 스튜디오 문제](#vs)
- [인터넷 정보 서비스 문제](#iis)
- [Azure 문제](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>클라이언트와 서버 간의 호출 메서드가 자동으로 실패합니다.

이 섹션에서는 의미 있는 오류 메시지 없이 클라이언트와 서버 간의 메서드 호출이 실패할 수 있는 원인을 설명합니다. SignalR 응용 프로그램에서 서버는 클라이언트가 구현하는 메서드에 대한 정보가 없습니다. 서버가 클라이언트 메서드를 호출하면 메서드 이름과 매개 변수 데이터가 클라이언트로 전송되고 메서드는 서버가 지정한 형식에 있는 경우에만 실행됩니다. 클라이언트에서 일치하는 메서드를 찾을 수 없는 경우 아무 일도 발생하지 않으며 서버에서 오류 메시지가 발생하지 않습니다.

호출되지 않는 클라이언트 메서드를 자세히 조사하려면 허브의 시작 메서드를 호출하기 전에 로깅을 켜서 서버에서 어떤 호출이 들어오는지 확인할 수 있습니다. JavaScript 응용 프로그램에서 로깅을 사용하려면 [클라이언트 측 로깅(JavaScript 클라이언트 버전)을 활성화하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)참조하세요. .NET 클라이언트 응용 프로그램에서 로깅을 사용하려면 [클라이언트 측 로깅(.NET 클라이언트 버전)을 활성화하는 방법을](../guide-to-the-api/hubs-api-guide-net-client.md#logging)참조하세요.

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>맞춤법이 잘못 지정된 메서드, 잘못된 메서드 서명 또는 잘못된 허브 이름

호출된 메서드의 이름이나 서명이 클라이언트의 적절한 메서드와 정확히 일치하지 않으면 호출이 실패합니다. 서버에서 호출한 메서드 이름이 클라이언트의 메서드 이름과 일치하는지 확인합니다. 또한 SignalR는 JavaScript에서 적절하 듯이 camel 대/소문자를 사용하는 허브 `SendMessage` 프록시를 생성하므로 `sendMessage` 서버에서 호출된 메서드가 클라이언트 프록시에서 호출됩니다. 서버 쪽 `HubName` 코드에서 특성을 사용하는 경우 사용된 이름이 클라이언트에서 허브를 만드는 데 사용된 이름과 일치하는지 확인합니다. 특성을 `HubName` 사용하지 않는 경우 JavaScript 클라이언트의 허브 이름이 ChatHub 대신 chatHub와 같은 낙타 대/소문자인지 확인합니다.

### <a name="duplicate-method-name-on-client"></a>클라이언트에서 메서드 이름 중복

대/소문자만 다른 클라이언트에 중복 메서드가 없는지 확인합니다. 클라이언트 응용 프로그램에 라는 `sendMessage`메서드가 있는 경우 는 메서드도 `SendMessage` 호출 되지 않습니다 확인 합니다.

### <a name="missing-json-parser-on-the-client"></a>클라이언트에서 누락된 JSON 파서

SignalR은 서버와 클라이언트 간의 호출을 직렬화하기 위해 JSON 파서가 있어야 합니다. 클라이언트에 기본 제공 JSON 파서(예: Internet Explorer 7)가 없는 경우 응용 프로그램에 하나를 포함해야 합니다. 여기에서 JSON 파서를 다운로드할 수 [있습니다.](http://nuget.org/packages/json2)

### <a name="mixing-hub-and-persistentconnection-syntax"></a>혼합 허브 및 영구 연결 구문

SignalR는 허브와 영구 연결이라는 두 가지 통신 모델을 사용합니다. 이러한 두 통신 모델을 호출하는 구문은 클라이언트 코드에서 다릅니다. 서버 코드에 허브를 추가한 경우 모든 클라이언트 코드가 적절한 허브 구문을 사용하는지 확인합니다.

**자바 스크립트 클라이언트에서 영구 연결을 만드는 자바 스크립트 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**자바 스크립트 클라이언트에서 허브 프록시를 만드는 자바 스크립트 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**영구 연결에 경로를 매핑하는 C# 서버 코드**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**여러 응용 프로그램이 있는 경우 허브 또는 여러 허브에 경로를 매핑하는 C# 서버 코드**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>구독을 추가하기 전에 연결이 시작되었습니다.

서버에서 호출할 수 있는 메서드가 프록시에 추가되기 전에 Hub연결이 시작되면 메시지가 수신되지 않습니다. 다음 JavaScript 코드는 허브를 제대로 시작하지 않습니다.

**허브 메시지를 수신할 수 없는 잘못된 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

대신 Start를 호출하기 전에 메서드 구독을 추가합니다.

**허브에 구독을 올바르게 추가하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>허브 프록시에서 메서드 이름이 누락되었습니다.

서버에 정의된 메서드가 클라이언트에 구독되어 있는지 확인합니다. 서버가 메서드를 정의하더라도 클라이언트 프록시에 계속 추가해야 합니다. 메서드는 다음과 같은 방법으로 클라이언트 프록시에 추가할 수 있습니다(메서드가 허브가 아닌 허브의 `client` 멤버에 직접 추가됨).

**허브 프록시에 메서드를 추가하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>공용으로 선언되지 않은 허브 또는 허브 메서드

클라이언트에서 표시하려면 허브 구현 및 메서드를 로 `public`선언해야 합니다.

### <a name="accessing-hub-from-a-different-application"></a>다른 응용 프로그램에서 허브 액세스

SignalR 허브는 SignalR 클라이언트를 구현하는 응용 프로그램을 통해서만 액세스할 수 있습니다. SignalR은 SOAP 또는 WCF 웹 서비스와 같은 다른 통신 라이브러리와 상호 운용할 수 없습니다. 대상 플랫폼에 사용할 수 있는 SignalR 클라이언트가 없는 경우 서버의 끝점에 직접 액세스할 수 없습니다.

### <a name="manually-serializing-data"></a>수동으로 데이터를 직렬화

SignalR은 자동으로 JSON을 사용하여 메서드 매개 변수를 직렬화합니다.

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>원격 허브 메서드가 연결 해제된 기능의 클라이언트에서 실행되지 않음

이 동작은 의도된 것입니다. 호출될 때 `OnDisconnected` 허브가 이미 `Disconnected` 상태에 들어갔으며 추가 허브 메서드를 호출할 수 없습니다.

**OnDisconnected 이벤트에서 코드를 올바르게 실행하는 C# 서버 코드**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>연결 한도에 도달했습니다.

Windows 7과 같은 클라이언트 운영 체제에서 전체 버전의 IIS를 사용하는 경우 10연결 제한이 부과됩니다. 클라이언트 OS를 사용하는 경우 이 제한을 피하기 위해 대신 IIS Express를 사용합니다.

### <a name="cross-domain-connection-not-set-up-properly"></a>도메인 간 연결이 제대로 설정되지 않음

도메인 간 연결(SignalR URL이 호스팅 페이지와 동일한 도메인에 없는 연결)이 올바르게 설정되지 않으면 오류 메시지 없이 연결이 실패할 수 있습니다. 도메인 간 통신을 활성화하는 방법에 대한 자세한 내용은 [도메인 간 연결을 설정하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)참조하세요.

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>.NET 클라이언트에서 작동하지 않는 NTLM(Active Directory)을 사용하는 연결

도메인 보안을 사용하는 .NET 클라이언트 응용 프로그램의 연결이 제대로 구성되지 않은 경우 연결이 실패할 수 있습니다. 도메인 환경에서 SignalR을 사용하려면 필수 연결 속성을 다음과 같이 설정합니다.

**연결 자격 증명을 구현하는 C# 클라이언트 코드**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>기타 연결 문제

이 섹션에서는 연결 중에 발생하는 특정 증상 또는 오류 메시지에 대한 원인과 해결 에 대해 설명합니다.

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>"데이터를 전송하려면 먼저 시작이 호출되어야 합니다." 오류

이 오류는 연결이 시작되기 전에 코드가 SignalR 개체를 참조하는 경우 일반적으로 나타납니다. 서버에서 정의된 메서드를 호출하는 처리기 등의 와이어업은 연결이 완료된 후 추가되어야 합니다. `Start` 호출은 비동기이므로 호출 후 코드가 완료되기 전에 실행될 수 있습니다. 연결이 완전히 시작된 후 처리기를 추가하는 가장 좋은 방법은 시작 메서드에 매개 변수로 전달되는 콜백 함수에 처리기를 넣는 것입니다.

**SignalR 개체를 참조하는 이벤트 처리기를 올바르게 추가하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

SignalR 개체가 계속 참조되는 동안 연결이 중지되는 경우에도 이 오류가 표시됩니다.

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>"301 영구적으로 이동" 또는 "302 일시적으로 이동" 오류

프로젝트에 SignalR이라는 폴더가 포함되어 있으면 자동으로 생성된 프록시가 방해가 될 수 있습니다. 이 오류를 방지하려면 응용 프로그램에서 `SignalR` 호출된 폴더를 사용하거나 자동 프록시 생성을 해제하지 마십시오. 자세한 내용은 [생성된 프록시 및 프록시가 수행하는 작업을](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) 참조하십시오.

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>.NET 또는 Silverlight 클라이언트에서 "403 금지됨" 오류

이 오류는 도메인 간 통신이 제대로 활성화되지 않은 도메인 간 환경에서 발생할 수 있습니다. 도메인 간 통신을 활성화하는 방법에 대한 자세한 내용은 [도메인 간 연결을 설정하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)참조하세요. Silverlight 클라이언트에서 도메인 간 연결을 설정하려면 [Silverlight 클라이언트의 도메인 간 연결을](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)참조하십시오.

### <a name="404-not-found-error"></a>"404 찾을 수 없습니다" 오류

이 문제에 대 한 몇 가지 원인이 있습니다. 다음 을 모두 확인합니다.

- **허브 프록시 주소 참조가 올바르게 포맷되지 않았습니다.** 이 오류는 생성된 허브 프록시 주소에 대한 참조가 올바르게 서식이 지정되지 않은 경우에 일반적으로 나타납니다. 허브 주소에 대한 참조가 제대로 만들어졌는지 확인합니다. 자세한 [내용은 동적으로 생성된 프록시를 참조하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) 참조하십시오.
- **허브 경로를 추가하기 전에 응용 프로그램에 경로 추가:** 응용 프로그램에서 다른 경로를 사용하는 경우 추가된 첫 `MapHubs`번째 경로가 에 대한 호출인지 확인합니다.

### <a name="500-internal-server-error"></a>"500 내부 서버 오류"

이것은 다양한 원인을 가질 수있는 매우 일반적인 오류입니다. 오류에 대한 세부 정보는 서버의 이벤트 로그에 표시되거나 서버 디버깅을 통해 찾을 수 있습니다. 서버에서 자세한 오류를 켜면 보다 자세한 오류 정보를 얻을 수 있습니다. 자세한 내용은 [Hub 클래스의 오류를 처리하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)참조하십시오.

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>"TypeError: &lt;hubType이&gt; 정의되지 않았습니다" 오류

호출이 제대로 이루어지지 않으면 `MapHubs` 이 오류가 발생합니다. [자세한 내용은 SignalR 경로를 등록하고 SignalR 옵션을 구성하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#route) 참조하십시오.

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>Json Serialization예외는 사용자 코드에 의해 처리되지 않았습니다.

메서드에 보내는 매개 변수에 직렬화할 수 없는 형식(예: 파일 핸들 또는 데이터베이스 연결)이 포함되어 있지 않은지 확인합니다. 보안 또는 직렬화의 이유로 클라이언트로 보내지 않으려는 서버 쪽 개체에서 멤버를 사용해야 하는 경우 특성을 `JSONIgnore` 사용합니다.

### <a name="protocol-error-unknown-transport-error"></a>"프로토콜 오류: 알 수 없는 전송" 오류

이 오류는 클라이언트가 SignalR에서 사용하는 전송을 지원하지 않는 경우에 발생할 수 있습니다. SignalR에서 사용할 수 있는 브라우저에 대한 정보는 [전송 및 대체를](../getting-started/introduction-to-signalr.md#transports) 참조하십시오.

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"자바 스크립트 허브 프록시 생성이 비활성화되었습니다."

에서 동적으로 `DisableJavaScriptProxies` 생성된 프록시에 대한 참조를 포함하면서 설정된 `signalr/hubs`경우 이 오류가 발생합니다. 수동으로 프록시를 만드는 방법에 대한 자세한 내용은 [생성된 프록시 및 프록시가 수행하는 작업을](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)참조하십시오.

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>"연결 ID가 잘못된 형식" 또는 "활성 SignalR 연결 중에 사용자 ID를 변경할 수 없습니다." 오류

이 오류는 인증을 사용 중인 경우 볼 수 있으며 연결이 중지되기 전에 클라이언트가 로그아웃된 경우 나타날 수 있습니다. 해결 방법은 클라이언트를 로그아웃하기 전에 SignalR 연결을 중지하는 것입니다.

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"잡히지 않은 오류: SignalR: jQuery를 찾을 수 없습니다. SignalR.js 파일" 오류 전에 jQuery가 참조되었는지 확인하십시오.

SignalR 자바 스크립트 클라이언트를 실행 하려면 jQuery가 필요 합니다. jQuery에 대한 참조가 올바른지, 사용된 경로가 유효한지, jQuery에 대한 참조가 SignalR에 대한 참조 앞에 있는지 확인합니다.

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>"잡히지 않은 TypeError:&lt;&gt;정의되지 않은 속성 '속성'을 읽을 수 없습니다" 오류

이 오류는 jQuery 또는 허브 프록시가 제대로 참조되지 않아 서 발생합니다. jQuery 및 허브 프록시에 대한 참조가 올바른지, 사용된 경로가 유효한지, jQuery에 대한 참조가 허브 프록시에 대한 참조 앞에 있는지 확인합니다. 허브 프록시에 대한 기본 참조는 다음과 같아야 합니다.

**Hubs 프록시를 올바르게 참조하는 HTML 클라이언트 쪽 코드**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>"런타임바인더예외가 사용자 코드에 의해 처리되지 않았습니다" 오류

이 `Hub.On` 오류는 잘못 된 오버 로드를 사용 하는 경우 발생할 수 있습니다. 메서드에 return 값이 있는 경우 반환 형식을 제네릭 형식 매개 변수로 지정해야 합니다.

**클라이언트에 정의된 메서드(생성된 프록시 제외)**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>연결 ID가 일치하지 않거나 페이지 로드 간에 연결이 끊어짐

이 동작은 의도된 것입니다. 허브 개체는 페이지 개체에서 호스팅되므로 페이지를 새로 고칠 때 허브가 소멸됩니다. 여러 페이지 응용 프로그램은 페이지 로드 간에 일관성을 유지하려면 사용자와 연결 아이디 간의 연결을 유지해야 합니다. 연결 아이디는 `ConcurrentDictionary` 개체 또는 데이터베이스의 서버에 저장할 수 있습니다.

### <a name="value-cannot-be-null-error"></a>"값이 null일 수 없습니다." 오류

선택적 매개 변수가 있는 서버 측 메서드는 현재 지원되지 않습니다. 선택적 매개 변수를 생략하면 메서드가 실패합니다. 자세한 내용은 [선택적 매개 변수 를](https://github.com/SignalR/SignalR/issues/324)참조하십시오.

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>"파이어 폭스 주소에서 &lt;서버에 대 한&gt;연결을 설정할 수 없습니다" 파이어 버그에서 오류

WebSocket 전송에 대한 협상이 실패하고 다른 전송이 대신 사용되는 경우 Firebug에서 이 오류 메시지를 볼 수 있습니다. 이 동작은 의도된 것입니다.

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>.NET 클라이언트 응용 프로그램에서 "유효성 검사 절차에 따라 원격 인증서가 잘못되었습니다." 오류

서버에 사용자 지정 클라이언트 인증서가 필요한 경우 요청하기 전에 x509인증서를 연결에 추가할 수 있습니다. 을 사용하여 `Connection.AddClientCertificate`연결에 인증서를 추가합니다.

### <a name="connection-drops-after-authentication-times-out"></a>인증 시간이 끝나면 연결이 끊어집니다.

이 동작은 의도된 것입니다. 연결이 활성화되어 있는 동안에는 인증 자격 증명을 수정할 수 없습니다. 자격 증명을 새로 고치려면 연결을 중지하고 다시 시작해야 합니다.

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>onConnected jQuery 모바일을 사용 하는 경우 두 번 호출 됩니다.

jQuery Mobile의 `initializePage` 함수는 각 페이지의 스크립트를 다시 실행하도록 강제하여 두 번째 연결을 만듭니다. 이 문제에 대한 해결 방법은 다음과 같습니다.

- 자바 스크립트 파일 전에 jQuery 모바일에 대한 참조를 포함합니다.
- `initializePage` 을 설정하여 `$.mobile.autoInitializePage = false`기능을 비활성화합니다.
- 연결을 시작하기 전에 페이지가 초기화가 완료될 때까지 기다립니다.

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>서버 전송 이벤트를 사용 하 여 Silverlight 응용 프로그램에서 메시지가 지연 됩니다.

실버라이트에서 서버 전송 이벤트를 사용할 때 메시지가 지연됩니다. 긴 폴링을 대신 사용하려면 연결을 시작할 때 다음을 사용하십시오.

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>포에버 프레임 프로토콜을 사용하여 "권한 거부"

이것은 [여기에](https://github.com/SignalR/SignalR/issues/1963)설명 된 알려진 된 문제입니다. 이 증상은 최신 JQuery 라이브러리를 사용하여 나타날 수 있습니다. 해결 방법은 응용 프로그램을 JQuery 1.8.2로 다운그레이드하는 것입니다.

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>컴파일 및 서버 측 오류

 다음 섹션에는 컴파일러 및 서버 측 런타임 오류에 대한 가능한 솔루션이 포함되어 있습니다. 

### <a name="reference-to-hub-instance-is-null"></a>허브 인스턴스에 대한 참조는 null입니다.

각 연결에 대해 허브 인스턴스가 만들어지므로 코드에서 허브 의 인스턴스를 직접 만들 수 없습니다. 허브 자체 외부에서 허브에서 메서드를 호출하려면 Hub 컨텍스트에 대한 참조를 가져오는 방법에 대해 [Hub 클래스 외부에서 클라이언트 메서드를 호출하고 그룹을 관리하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) 참조하세요.

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext.현재.세션은 null입니다.

이 동작은 의도된 것입니다. SignalR은 세션 상태를 사용하도록 설정하면 이중 메시징이 중단되므로 ASP.NET 세션 상태를 지원하지 않습니다.

### <a name="no-suitable-method-to-override"></a>재정의할 적절한 방법이 없습니다.

이전 문서 나 블로그의 코드를 사용하는 경우이 오류가 표시 될 수 있습니다. 변경되거나 더 이상 사용되지 않는 메서드의 이름을 참조하지 않았는지 확인합니다( 예: `OnConnectedAsync`).

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>호스트 컨텍스트 확장.웹 소켓 서버Url은 null입니다.

이 동작은 의도된 것입니다. 이 멤버는 더 이상 사용되지 않으며 사용해서는 안 됩니다.

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"'signalr.hubs'라는 경로가 이미 경로 컬렉션에 있습니다." 오류

응용 프로그램에서 두 `MapHubs` 번 호출되는 경우 이 오류가 표시됩니다. 일부 예제 응용 `MapHubs` 프로그램은 전역 응용 프로그램 파일에서 직접 호출합니다. 다른 사람은 래퍼 클래스에서 호출합니다. 응용 프로그램이 두 가지 를 모두 수행하지 않는지 확인합니다.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>비주얼 스튜디오 문제

이 섹션에서는 Visual Studio에서 발생한 문제에 대해 설명합니다.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>스크립트 문서 노드가 솔루션 탐색기에서 나타나지 않음

일부 자습서에서는 디버깅하는 동안 솔루션 탐색기의 "스크립트 문서" 노드로 안내합니다. 이 노드는 JavaScript 디버거에 의해 생성되며 Internet Explorer에서 브라우저 클라이언트를 디버깅하는 동안에만 나타납니다. 크롬이나 파이어 폭스를 사용하는 경우 노드가 표시되지 않습니다. Silverlight 디버거와 같은 다른 클라이언트 디버거가 실행 중인 경우에도 JavaScript 디버거가 실행되지 않습니다.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR은 Visual Studio 2008 이전 에서 작동하지 않습니다.

이 동작은 의도된 것입니다. SignalR에는 .NET 프레임워크 4 이상이 필요합니다. 이를 위해서는 VisualR 애플리케이션을 Visual Studio 2010 이상에서 개발해야 합니다.

<a id="iis"></a>

## <a name="iis-issues"></a>IIS 문제

이 섹션에는 인터넷 정보 서비스에 대한 문제가 포함되어 있습니다.

### <a name="web-site-crashes-after-maphubs-call"></a>MapHubs 호출 후 웹 사이트 충돌

이 문제는 SignalR의 최신 버전에서 해결되었습니다. NuGet을 사용하여 설치를 업데이트하여 최신 버전의 SignalR을 사용하고 있는지 확인합니다.

<a id="azure"></a>

## <a name="azure-issues"></a>Azure 문제

이 섹션에는 Microsoft Azure에 대한 문제가 포함되어 있습니다.

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>토픽 이름을 변경한 후 Azure 백플레인을 통해 메시지가 수신되지 않습니다.

Azure 백플레인에서 사용하는 항목은 사용자가 구성할 수 없습니다.
