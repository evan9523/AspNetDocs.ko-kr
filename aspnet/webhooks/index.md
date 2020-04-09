---
uid: webhooks/index
title: ASP.NET 웹후크 개요 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 웹후크소개.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa5fa190386ec803a6801de2d815c948677fe1f5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675436"
---
# <a name="aspnet-webhooks-overview"></a>ASP.NET 웹후크 개요

WebHook는 Web API와 SaaS 서비스를 연결하는 간단한 pub/sub 모델을 제공하는 가벼운 HTTP 패턴입니다. 서비스에서 이벤트가 발생하면 등록된 구독자에게 HTTP POST 요청의 형태로 알림이 전송됩니다. POST 요청에는 수신자가 적절하게 대처할 수 있도록 이벤트에 대한 정보를 포함되어 있습니다.

때문에 그들의 단순함, WebHooks는 이미 [드롭 박스,](http://dropbox.com/) [GitHub,](https://www.github.com/) [비트 버킷,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [페이팔,](http://www.paypal.com/) [슬랙,](http://www.slack.com) [스트라이프,](http://www.stripe.com) [트렐로,](http://www.trello.com/)그리고 더 많은 등의 서비스의 큰 숫자에 의해 노출되어 있습니다. 예를 들어 WebHook은 [파일이 Dropbox에서](http://dropbox.com/)변경되었거나 GitHub에서 코드 변경이 커밋되었거나 [PayPal에서](http://www.paypal.com/)결제가 시작되었거나 [Trello에서](http://www.trello.com/)카드가 생성되었음을 나타낼 수 있습니다. 가능성은 무한합니다!

Microsoft ASP.NET WebHooks를 사용하면 ASP.NET 응용 프로그램의 일부로 WebHook을 쉽게 보내고 받을 수 있습니다.

* 수신 측에서는 여러 WebHook 공급자로부터 WebHook을 수신하고 처리하기 위한 공통 모델을 제공합니다. 그것은 [드롭 박스,](http://dropbox.com/) [GitHub,](https://www.github.com/) [비트 버킷,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [페이팔,](http://www.paypal.com/) [푸셔,](http://www.pusher.com) [세일즈 포스,](http://www.salesforce.com) [슬랙,](http://www.slack.com) [스트라이프,](http://www.stripe.com) [트렐로,](http://www.trello.com/)[워드 프레스와](http://www.wordpress.com) [젠 데스크에](https://www.zendesk.com/) 대한 지원과 함께 상자에서 나온다하지만 더 많은 지원을 추가하기 쉽습니다.

* 전송 측에서는 구독관리 및 저장뿐만 아니라 올바른 구독자 집합에 이벤트 알림을 보내는 지원을 제공합니다. 이렇게 하면 구독자가 구독할 수 있는 고유한 이벤트 집합을 정의하고 상황이 발생하면 이를 알릴 수 있습니다.

시나리오에 따라 두 부분을 함께 사용하거나 따로 사용할 수 있습니다. 다른 서비스에서 WebHooks만 수신해야하는 경우 수신기 부분만 사용할 수 있습니다. 다른 사용자가 사용할 수 있도록 WebHooks만 노출하려는 경우 그렇게 할 수 있습니다.

코드는 웹 API 2 와 ASP.NET MVC 5ASP.NET 대상으로 하며 [GitHub에서 OSS로](https://github.com/aspnet/WebHooks)사용할 수 있습니다.

## <a name="webhooks-overview"></a>웹후크 개요

WebHooks는 서비스에서 서비스로 사용되는 방식이 다르지만 기본 개념은 동일하다는 것을 의미하는 패턴입니다. WebHooks는 사용자가 다른 곳에서 발생하는 이벤트를 구독할 수 있는 간단한 펍/하위 모델로 생각할 수 있습니다. 이벤트 알림은 이벤트 자체에 대한 정보를 포함하는 HTTP POST 요청으로 전파됩니다.

일반적으로 HTTP POST 요청에는 WebHook이 트리거되는 이벤트에 대한 정보를 포함하여 WebHook 보낸 사람에게 결정된 JSON 개체 또는 HTML 양식 데이터가 포함됩니다. 예를 들어 [GitHub의](https://www.github.com/) WebHook POST 요청 본문은 특정 리포지토리에서 새 문제가 열리면 다음과 같습니다.

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

WebHook이 실제로 의도된 보낸 사람으로부터 확인되도록 POST 요청은 어떤 식으로든 보호된 다음 수신자가 확인합니다. 예를 들어 [GitHub WebHooks에는](https://developer.github.com/webhooks/) 요청 본체의 해시가 있는 *X-Hub-Signature* HTTP 헤더가 포함되어 있으므로 걱정할 필요가 없습니다.

WebHook 흐름은 일반적으로 다음과 같습니다.

* WebHook 보낸 사람은 클라이언트가 구독할 수 있는 이벤트를 노출합니다. 이벤트는 새 데이터 항목이 삽입되었거나 프로세스가 완료되었거나 다른 항목과 같은 시스템의 관찰 가능한 변경 내용을 설명합니다.

* WebHook 수신기는 다음 네 가지로 구성된 WebHook을 등록하여 구독합니다.

     1. HTTP POST 요청의 형태로 이벤트 알림을 게시해야 하는 URI;

     2. WebHook이 발생해야 하는 특정 이벤트를 설명하는 필터 집합입니다.

     3. HTTP POST 요청에 서명하는 데 사용되는 비밀 키입니다.

     4. HTTP POST 요청에 포함될 추가 데이터입니다. 예를 들어 HTTP POST 요청 본문에 포함된 추가 HTTP 헤더 필드 또는 속성일 수 있습니다.

* 이벤트가 발생하면 일치하는 WebHook 등록이 발견되고 HTTP POST 요청이 제출됩니다. 일반적으로 어떤 이유로 받는 사람이 응답하지 않거나 HTTP POST 요청으로 인해 오류 응답이 발생하는 경우 HTTP POST 요청생성이 여러 번 다시 시도됩니다.

## <a name="webhooks-processing-pipeline"></a>웹후크 처리 파이프라인

들어오는 WebHooks에 대 한 Microsoft ASP.NET WebHooks 처리 파이프라인 다음과 같습니다.

![ASP.NET 웹후크 처리 파이프라인](_static/WebHookReceivers.png)

여기서 두 가지 주요 개념은 *수신기와* *처리기입니다.*

* *수신기는* 지정된 보낸 사람의 WebHook의 특정 맛을 처리하고 WebHook 요청이 실제로 의도된 보낸 사람에게서 온 것인지 확인하기 위해 보안 검사를 적용해야 합니다.

* *처리기는* 일반적으로 사용자 코드가 특정 WebHook을 처리하는 실행되는 곳입니다.

다음 노드에서 이러한 개념은 자세한 내용으로 설명되어 있습니다.
