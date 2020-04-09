---
uid: webhooks/receiving/receivers
title: ASP.NET 웹후크 수신기 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 웹후크 수신기
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: 60f46141b59fc3888a6480d8201160420469d1a7
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675162"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="cccff-103">ASP.NET 웹후크 수신기</span><span class="sxs-lookup"><span data-stu-id="cccff-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="cccff-104">WebHook을 받는 것은 보낸 사람이 누구인지에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="cccff-105">때로는 구독자가 실제로 듣고 있는지 확인하는 WebHook을 등록하는 추가 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="cccff-106">일부 WebHooks는 HTTP POST 요청에 이벤트 정보에 대한 참조만 포함하는 푸시 투 풀 모델을 제공하며, 이 경우 독립적으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="cccff-107">종종 보안 모델은 꽤 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="cccff-108">Microsoft ASP.NET WebHooks의 목적은 WebHooks의 특정 변형을 처리하는 방법을 알아내는 데 많은 시간을 소비하지 않고 API를 더 간단하고 일관되게 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="cccff-109">WebHook 수신기는 특정 발신자의 WebHook을 수락하고 검증할 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="cccff-110">WebHook 수신기는 자체 구성을 통해 각 웹후크를 임의로 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="cccff-111">예를 들어 GitHub WebHook 수신기는 여러 GitHub 리포지토리에서 웹후크를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="cccff-112">웹후크 수신기 URI</span><span class="sxs-lookup"><span data-stu-id="cccff-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="cccff-113">Microsoft ASP.NET WebHooks를 설치하면 개방형 서비스 수의 WebHook 요청을 허용하는 일반 WebHook 컨트롤러를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="cccff-114">요청이 도착하면 특정 WebHook 발신자를 처리하기 위해 설치한 적절한 수신기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="cccff-115">이 컨트롤러의 URI는 서비스에 등록하고 양식의 WebHook URI입니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="cccff-116">보안상의 이유로 많은 WebHook 수신기는 URI가 *https* URI여야 하며 경우에 따라 의도한 당사자만 위의 URI에 WebHook을 보낼 수 있도록 적용하는 데 사용되는 추가 쿼리 매개 변수도 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="cccff-117">`<receiver>` 구성 요소는 수신기의 이름(예: `github` `slack`또는 .)입니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="cccff-118">*{id}는* 특정 WebHook 수신기 구성을 식별하는 데 사용할 수 있는 선택적 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="cccff-119">특정 수신기에 N WebHook을 등록하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="cccff-120">예를 들어 다음 세 개의 URI를 사용하여 세 개의 독립적인 WebHook에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="cccff-121">웹후크 수신기 설치</span><span class="sxs-lookup"><span data-stu-id="cccff-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="cccff-122">Microsoft ASP.NET WebHooks를 사용하여 웹후크를 받으려면 먼저 WebHook 공급자 또는 웹후크를 수신하려는 공급자를 위한 Nuget 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="cccff-123">Nuget 패키지의 이름은 [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) 마지막 부분에서 지원되는 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="cccff-124">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-124">For example</span></span>

<span data-ttu-id="cccff-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub는](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) GitHub및 [Microsoft.AspNet.WebHooks.Receivers.Custom에서](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) 웹후크수신을 지원하며, ASP.NET 웹후크에서 생성된 웹후크수신을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="cccff-126">상자 밖으로 당신은 드롭 박스에 대한 지원을 찾을 수 있습니다, GitHub, MailChimp, 페이팔, 푸셔, 세일즈 포스, 슬랙, 스트라이프, 트렐로, 워드 프레스하지만 다른 공급자의 수를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="cccff-127">웹후크 수신기 구성</span><span class="sxs-lookup"><span data-stu-id="cccff-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="cccff-128">WebHook 수신기는 [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface를 통해 구성되며 해당 인터페이스의 특정 구현은 모든 종속성 주입 모델을 사용하여 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="cccff-129">기본 구현에서는 Web.config 파일에서 설정할 수 있는 응용 프로그램 설정을 사용하거나 Azure Web Apps를 사용하는 경우 [Azure Portal](https://portal.azure.com/)을 통해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure 앱 설정](_static/AzureAppSettings.png)

<span data-ttu-id="cccff-131">응용 프로그램 설정 키의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="cccff-132">이 값은 다음과 같은 WebHooks가 등록된 *{id}* 값과 일치하는 쉼표로 구분된 값 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="cccff-133">웹후크 수신기 초기화</span><span class="sxs-lookup"><span data-stu-id="cccff-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="cccff-134">WebHook 수신기는 일반적으로 *WebApiConfig* 정적 클래스에 등록하여 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="cccff-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
