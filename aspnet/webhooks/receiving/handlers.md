---
uid: webhooks/receiving/handlers
title: ASP.NET 웹 후크 처리기 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크 요청을 처리 하는 방법입니다.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: 01c9a283d105c4a0973ff88c8de646c5f49a34db
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030100"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="cdf50-103">ASP.NET 웹 후크 처리기</span><span class="sxs-lookup"><span data-stu-id="cdf50-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="cdf50-104">웹 후크 요청 WebHook 수신기가 검증 된 후에 사용자 코드에서 처리할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="cdf50-105">이 경우 *처리기* 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-105">This is where *handlers* come in.</span></span> <span data-ttu-id="cdf50-106">처리기에서 파생 되는 [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) 인터페이스 하지만 일반적으로 사용 하 여는 [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) 클래스 인터페이스에서 직접 파생 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="cdf50-107">하나 이상의 처리기에서 웹 후크 요청을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="cdf50-108">처리기는 각각에 기반한 순서 대로 호출 됩니다 *순서* 것에서 가장 낮은 값에서 가장 높은 순서 인 (1에서 100 사이 여야 하는 좋습니다) 단순 정수 속성:</span><span class="sxs-lookup"><span data-stu-id="cdf50-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![웹 후크 처리기 순서 속성 다이어그램](_static/Handlers.png)

<span data-ttu-id="cdf50-110">처리기를 선택적으로 설정할 수는 *응답* 를 중지 했다가 다시 WebHook에 대 한 HTTP 응답 메시지로 보내도록 응답 처리를 진행 되는 WebHookHandlerContext 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="cdf50-111">위의 예에서 B 및 B 집합 응답 보다 더 높은 순서 지정 되었기 때문에 처리기 C 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="cdf50-112">응답 설정은 일반적으로 웹 후크 응답 정보를 다시 원래 API 수행할 수 있는 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="cdf50-113">이 예를 들어 Slack 웹 후크 응답 채널 WebHook에서 발생 한 위치에 다시 게시 되는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="cdf50-114">웹 후크는 특정 수신기에서 수신 하고자 하는 경우 처리기는 받는 사람 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="cdf50-115">수신기 설정 없는 경우 함수를 모두 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="cdf50-116">다른 일반적인 용도 응답의 하나를 사용 하는 것을 *410* 대 한 응답으로 나타내고 웹 후크는 더 이상 활성 요청이 제출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="cdf50-117">기본적으로 모든 웹 후크 수신기가 처리기를 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="cdf50-118">그러나 경우 합니다 *받는 사람* 처리기의 이름으로 속성을 해당 처리기에만 해당 수신기에서 웹 후크 요청이 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="cdf50-119">웹 후크를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-119">Processing a WebHook</span></span>

<span data-ttu-id="cdf50-120">가져와서 처리기가 호출 되는 [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) 웹 후크 요청에 대 한 정보를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="cdf50-121">일반적으로 HTTP 요청 본문 데이터에서 사용할 수는 *데이터* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="cdf50-122">데이터의 형식을 JSON 또는 HTML 양식 데이터는 일반적으로 하지만 원하는 경우 보다 구체적인 형식으로 캐스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="cdf50-123">예를 들어, ASP.NET 웹 후크에 의해 생성 된 사용자 지정 웹 후크를 캐스팅할 수 형식 [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

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

  ## <a name="queued-processing"></a><span data-ttu-id="cdf50-124">지연된 처리</span><span class="sxs-lookup"><span data-stu-id="cdf50-124">Queued Processing</span></span>

<span data-ttu-id="cdf50-125">응답은 몇 초 내에서 생성 되지 않은 경우 대부분의 웹 후크 발신자는 웹 후크를 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="cdf50-126">즉, 처리기가 다시 호출 되어 하지 위해에서 해당 시간 프레임 내에서 처리를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="cdf50-127">처리 시간이 오래 걸리면, 또는 개별적으로 처리 되는 것이 더 잘 하는 경우 해당 [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) 예를 들어 큐에 웹 후크 요청을 제출 하려면 사용할 수 있습니다 [Azure Storage 큐](https://msdn.microsoft.com/library/azure/dd179353.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="cdf50-128">에 대 한 개요는 [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) 구현 여기에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf50-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

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
