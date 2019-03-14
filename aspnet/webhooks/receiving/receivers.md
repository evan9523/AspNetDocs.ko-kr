---
uid: webhooks/receiving/receivers
title: ASP.NET 웹 후크 수신기 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크 수신기
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038980"
---
# <a name="aspnet-webhooks-receivers"></a>ASP.NET 웹 후크 수신기

Webhook를 받는 발신자가 있는 사용자에 따라 달라 집니다. 경우에 따라 구독자는 실제로 수신 대기 하는지 확인 하는 웹 후크를 등록 하는 추가 단계가 있습니다. 일부 웹 후크 HTTP POST 요청을 독립적으로 검색 되는 이벤트 정보에 대 한 참조만 포함 되는 위치 밀어넣기-끌어오기 모델을 제공 합니다. 종종 보안 모델은 상당히 달라 집니다.

Microsoft ASP.NET 웹 후크의 목적은 간단 하 고 일관성 있게 Webhook의 특정 변형을 처리 하는 방법을 파악 하는 시간이 많이 소비 하지 않고 API를 연결 하도록 합니다.

웹 후크 수신기는 수락 하 고 특정 보낸에서 웹 후크를 확인 하는 일을 담당 합니다. 웹 후크 수신기는 임의 개수의 Webhook 각각 고유한 구성을 지원할 수 있습니다. 예를 들어 GitHub 웹 후크 수신기 GitHub 리포지토리에 있는 모든 수의 웹 후크를 사용할 수 있습니다.

## <a name="webhook-receiver-uris"></a>웹 후크 수신기 Uri

Microsoft ASP.NET 웹 후크를 설치 하 여 서비스는 개방형 수의 웹 후크 요청을 수락 하는 일반 웹 후크 컨트롤러를 가져올 수 있습니다. 요청이 도착 하면 특정 WebHook 발신자를 처리 하는 것에 대 한 설치 된 적절 한 수신기를 선택 합니다.

이 컨트롤러의 URI는 서비스를 사용 하 여 등록 하는 웹 후크 URI 이며 형식:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

보안상의 이유로 많은 WebHook 수신기를 사용 하려면 URI는 *https* URI 및 일부 경우에도 포함 해야는 의도 된 파티 위의 URI에 웹 후크를 보낼 수만 적용 하는 데 사용 되는 추가 쿼리 매개 변수 .

합니다 `<receiver>` 구성 요소는 수신기의 이름 예를 들어 `github` 또는 `slack`합니다.

합니다 *{id}* 특정 WebHook 수신기 구성을 식별 하는 선택적 식별자입니다. 이 특정 수신기를 사용 하 여 N 웹 후크를 등록 수 있습니다. 예를 들어, 세 가지 독립적인 웹 후크에 대 한 등록 하는 다음 세 가지 Uri는 사용할 수 있습니다.:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>웹 후크 수신기 설치

Microsoft ASP.NET 웹 후크를 사용 하 여 웹 후크를 수신 하려면 먼저 웹 후크 공급자 또는 공급자의 웹 후크를 받으려면 Nuget 패키지를 설치 합니다. Nuget 패키지 라고 [Microsoft.AspNet.WebHooks.Receivers.*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) 여기서 마지막 부분에 지원 되는 서비스를 나타냅니다. 예

[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) GitHub에서 웹 후크를 수신 하기 위한 지원을 제공 하 고 [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) ASP에서 생성 하는 웹 후크를 수신 하기 위한 지원을 제공 합니다. NET 웹 후크입니다.

Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, 스트라이프, Trello 및 WordPress에 대 한 지원을 기본적 있습니다 하지만 임의 개수의 다른 공급자를 지원 하기 위해 가능 합니다.

## <a name="configuring-a-webhook-receiver"></a>웹 후크 수신기 구성

WebHook 수신기를 통해 구성 되는 [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) 해당 인터페이스의 특정 구현 및 인터페이스에 모든 종속성 주입 모델을 사용 하 여 등록할 수 있습니다. 기본 구현에는 Web.config 파일에서 설정할 수 있습니다, Azure Web Apps를 사용 하는 경우를 통해 설정할 수 있는 응용 프로그램 설정을 사용 합니다 [Azure Portal](https://portal.azure.com/)합니다.

![Azure 앱 설정](_static/AzureAppSettings.png)

응용 프로그램 설정 키의 형식은 아래와 같습니다.

```
MS_WebHookReceiverSecret_<receiver>
```

값이 일치 하는 값의 쉼표로 구분 된 목록을 합니다 *{id}* 는 웹 후크 등록 된, 예를 들어 값:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>웹 후크 수신기를 초기화합니다.

웹 후크 수신기에, 일반적으로 등록 하 여 초기화 되는 *WebApiConfig* 예를 들어 정적 클래스:

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
