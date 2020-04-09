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
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="063af-103">ASP.NET 웹후크 개요</span><span class="sxs-lookup"><span data-stu-id="063af-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="063af-104">WebHook는 Web API와 SaaS 서비스를 연결하는 간단한 pub/sub 모델을 제공하는 가벼운 HTTP 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="063af-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="063af-105">서비스에서 이벤트가 발생하면 등록된 구독자에게 HTTP POST 요청의 형태로 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="063af-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="063af-106">POST 요청에는 수신자가 적절하게 대처할 수 있도록 이벤트에 대한 정보를 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="063af-107">때문에 그들의 단순함, WebHooks는 이미 [드롭 박스,](http://dropbox.com/) [GitHub,](https://www.github.com/) [비트 버킷,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [페이팔,](http://www.paypal.com/) [슬랙,](http://www.slack.com) [스트라이프,](http://www.stripe.com) [트렐로,](http://www.trello.com/)그리고 더 많은 등의 서비스의 큰 숫자에 의해 노출되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="063af-108">예를 들어 WebHook은 [파일이 Dropbox에서](http://dropbox.com/)변경되었거나 GitHub에서 코드 변경이 커밋되었거나 [PayPal에서](http://www.paypal.com/)결제가 시작되었거나 [Trello에서](http://www.trello.com/)카드가 생성되었음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="063af-109">가능성은 무한합니다!</span><span class="sxs-lookup"><span data-stu-id="063af-109">The possibilities are endless!</span></span>

<span data-ttu-id="063af-110">Microsoft ASP.NET WebHooks를 사용하면 ASP.NET 응용 프로그램의 일부로 WebHook을 쉽게 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="063af-111">수신 측에서는 여러 WebHook 공급자로부터 WebHook을 수신하고 처리하기 위한 공통 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="063af-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="063af-112">그것은 [드롭 박스,](http://dropbox.com/) [GitHub,](https://www.github.com/) [비트 버킷,](https://bitbucket.org/) [MailChimp,](http://www.mailchimp.com/) [페이팔,](http://www.paypal.com/) [푸셔,](http://www.pusher.com) [세일즈 포스,](http://www.salesforce.com) [슬랙,](http://www.slack.com) [스트라이프,](http://www.stripe.com) [트렐로,](http://www.trello.com/)[워드 프레스와](http://www.wordpress.com) [젠 데스크에](https://www.zendesk.com/) 대한 지원과 함께 상자에서 나온다하지만 더 많은 지원을 추가하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="063af-113">전송 측에서는 구독관리 및 저장뿐만 아니라 올바른 구독자 집합에 이벤트 알림을 보내는 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="063af-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="063af-114">이렇게 하면 구독자가 구독할 수 있는 고유한 이벤트 집합을 정의하고 상황이 발생하면 이를 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="063af-115">시나리오에 따라 두 부분을 함께 사용하거나 따로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="063af-116">다른 서비스에서 WebHooks만 수신해야하는 경우 수신기 부분만 사용할 수 있습니다. 다른 사용자가 사용할 수 있도록 WebHooks만 노출하려는 경우 그렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="063af-117">코드는 웹 API 2 와 ASP.NET MVC 5ASP.NET 대상으로 하며 [GitHub에서 OSS로](https://github.com/aspnet/WebHooks)사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="063af-118">웹후크 개요</span><span class="sxs-lookup"><span data-stu-id="063af-118">WebHooks Overview</span></span>

<span data-ttu-id="063af-119">WebHooks는 서비스에서 서비스로 사용되는 방식이 다르지만 기본 개념은 동일하다는 것을 의미하는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="063af-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="063af-120">WebHooks는 사용자가 다른 곳에서 발생하는 이벤트를 구독할 수 있는 간단한 펍/하위 모델로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="063af-121">이벤트 알림은 이벤트 자체에 대한 정보를 포함하는 HTTP POST 요청으로 전파됩니다.</span><span class="sxs-lookup"><span data-stu-id="063af-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="063af-122">일반적으로 HTTP POST 요청에는 WebHook이 트리거되는 이벤트에 대한 정보를 포함하여 WebHook 보낸 사람에게 결정된 JSON 개체 또는 HTML 양식 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="063af-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="063af-123">예를 들어 [GitHub의](https://www.github.com/) WebHook POST 요청 본문은 특정 리포지토리에서 새 문제가 열리면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

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

<span data-ttu-id="063af-124">WebHook이 실제로 의도된 보낸 사람으로부터 확인되도록 POST 요청은 어떤 식으로든 보호된 다음 수신자가 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="063af-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="063af-125">예를 들어 [GitHub WebHooks에는](https://developer.github.com/webhooks/) 요청 본체의 해시가 있는 *X-Hub-Signature* HTTP 헤더가 포함되어 있으므로 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="063af-126">WebHook 흐름은 일반적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="063af-127">WebHook 보낸 사람은 클라이언트가 구독할 수 있는 이벤트를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="063af-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="063af-128">이벤트는 새 데이터 항목이 삽입되었거나 프로세스가 완료되었거나 다른 항목과 같은 시스템의 관찰 가능한 변경 내용을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="063af-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="063af-129">WebHook 수신기는 다음 네 가지로 구성된 WebHook을 등록하여 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="063af-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="063af-130">HTTP POST 요청의 형태로 이벤트 알림을 게시해야 하는 URI;</span><span class="sxs-lookup"><span data-stu-id="063af-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="063af-131">WebHook이 발생해야 하는 특정 이벤트를 설명하는 필터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="063af-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="063af-132">HTTP POST 요청에 서명하는 데 사용되는 비밀 키입니다.</span><span class="sxs-lookup"><span data-stu-id="063af-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="063af-133">HTTP POST 요청에 포함될 추가 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="063af-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="063af-134">예를 들어 HTTP POST 요청 본문에 포함된 추가 HTTP 헤더 필드 또는 속성일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="063af-135">이벤트가 발생하면 일치하는 WebHook 등록이 발견되고 HTTP POST 요청이 제출됩니다.</span><span class="sxs-lookup"><span data-stu-id="063af-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="063af-136">일반적으로 어떤 이유로 받는 사람이 응답하지 않거나 HTTP POST 요청으로 인해 오류 응답이 발생하는 경우 HTTP POST 요청생성이 여러 번 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="063af-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="063af-137">웹후크 처리 파이프라인</span><span class="sxs-lookup"><span data-stu-id="063af-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="063af-138">들어오는 WebHooks에 대 한 Microsoft ASP.NET WebHooks 처리 파이프라인 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET 웹후크 처리 파이프라인](_static/WebHookReceivers.png)

<span data-ttu-id="063af-140">여기서 두 가지 주요 개념은 *수신기와* *처리기입니다.*</span><span class="sxs-lookup"><span data-stu-id="063af-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="063af-141">*수신기는* 지정된 보낸 사람의 WebHook의 특정 맛을 처리하고 WebHook 요청이 실제로 의도된 보낸 사람에게서 온 것인지 확인하기 위해 보안 검사를 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="063af-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="063af-142">*처리기는* 일반적으로 사용자 코드가 특정 WebHook을 처리하는 실행되는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="063af-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="063af-143">다음 노드에서 이러한 개념은 자세한 내용으로 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="063af-143">In the following nodes these concepts are described in more details.</span></span>
