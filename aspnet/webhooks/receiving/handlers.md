---
uid: webhooks/receiving/handlers
title: ASP.NET 웹후크 핸들러 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET WebHooks에서 요청을 처리하는 방법.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: ff12dd8df167eca17ecbd9f03a71807d44af2b30
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675211"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="729f7-103">ASP.NET 웹후크 처리기</span><span class="sxs-lookup"><span data-stu-id="729f7-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="729f7-104">WebHooks 요청이 WebHook 수신기에 의해 검증되면 사용자 코드에서 처리할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="729f7-105">여기서 *처리기가* 들어옵니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-105">This is where *handlers* come in.</span></span> <span data-ttu-id="729f7-106">처리기는 [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) 인터페이스에서 파생되지만 일반적으로 인터페이스에서 직접 파생되는 대신 [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="729f7-107">하나 이상의 처리기에서 WebHook 요청을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="729f7-108">처리기는 Order가 간단한 정수인 *가장* 낮은 값에서 가장 높은 순서로 호출됩니다(1에서 100 사이로 제안됨).</span><span class="sxs-lookup"><span data-stu-id="729f7-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook 처리기 주문 속성 다이어그램](_static/Handlers.png)

<span data-ttu-id="729f7-110">처리기는 선택적으로 WebHookHandlerContext에서 *응답* 속성을 설정할 수 있으며, 이 속성은 처리를 중지하고 응답이 WebHook에 대한 HTTP 응답으로 다시 전송하도록 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="729f7-111">위의 경우 처리기 C는 B보다 높은 순서를 가지며 B는 응답을 설정하기 때문에 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="729f7-112">응답 설정은 일반적으로 응답이 정보를 원래 API로 다시 전달할 수 있는 WebHooks에만 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="729f7-113">예를 들어 Slack WebHooks의 경우 응답이 WebHook에서 발생한 채널에 다시 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="729f7-114">처리기는 특정 수신기에서 WebHook만 수신하려는 경우 Receiver 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="729f7-115">수신기를 설정하지 않으면 모든 수신기가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="729f7-116">응답의 또 다른 일반적인 용도는 *410 Gone* 응답을 사용하여 WebHook이 더 이상 활성화되지 않고 더 이상 요청을 제출하지 않아야 함을 나타내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="729f7-117">기본적으로 처리기는 모든 WebHook 수신기에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="729f7-118">그러나 *Receiver* 속성이 처리기의 이름으로 설정된 경우 해당 처리기는 해당 수신기에서 WebHook 요청만 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="729f7-119">웹 후크 처리</span><span class="sxs-lookup"><span data-stu-id="729f7-119">Processing a WebHook</span></span>

<span data-ttu-id="729f7-120">처리기가 호출되면 WebHook 요청에 대한 정보가 포함된 [WebHookHandlerContext가](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="729f7-121">일반적으로 HTTP 요청 본문인 데이터는 *Data* 속성에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="729f7-122">데이터의 형식은 일반적으로 JSON 또는 HTML 양식 데이터이지만 원하는 경우 보다 구체적인 형식으로 캐스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="729f7-123">예를 들어 ASP.NET WebHook에서 생성된 사용자 지정 WebHooks는 다음과 같이 [사용자 지정 알림](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) 유형으로 캐스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="729f7-124">큐에 대기된 처리</span><span class="sxs-lookup"><span data-stu-id="729f7-124">Queued Processing</span></span>

<span data-ttu-id="729f7-125">응답이 몇 초 내에 생성되지 않으면 대부분의 WebHook 발신자는 WebHook을 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="729f7-126">즉, 처리기가 다시 호출되지 않도록 해당 기간 내에 처리를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="729f7-127">처리 시간이 더 오래 걸리거나 별도로 더 잘 처리되는 경우 [WebHookQueueHandler를](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) 사용하여 WebHook 요청을 큐에 제출하는 데 사용할 수 있습니다(예: [Azure 저장소 큐)](https://msdn.microsoft.com/library/azure/dd179353.aspx)</span><span class="sxs-lookup"><span data-stu-id="729f7-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="729f7-128">[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) 구현의 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="729f7-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
