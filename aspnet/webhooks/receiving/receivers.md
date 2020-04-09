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
# <a name="aspnet-webhooks-receivers"></a>ASP.NET 웹후크 수신기

WebHook을 받는 것은 보낸 사람이 누구인지에 따라 다릅니다. 때로는 구독자가 실제로 듣고 있는지 확인하는 WebHook을 등록하는 추가 단계가 있습니다. 일부 WebHooks는 HTTP POST 요청에 이벤트 정보에 대한 참조만 포함하는 푸시 투 풀 모델을 제공하며, 이 경우 독립적으로 검색할 수 있습니다. 종종 보안 모델은 꽤 다양합니다.

Microsoft ASP.NET WebHooks의 목적은 WebHooks의 특정 변형을 처리하는 방법을 알아내는 데 많은 시간을 소비하지 않고 API를 더 간단하고 일관되게 연결하는 것입니다.

WebHook 수신기는 특정 발신자의 WebHook을 수락하고 검증할 책임이 있습니다. WebHook 수신기는 자체 구성을 통해 각 웹후크를 임의로 지원할 수 있습니다. 예를 들어 GitHub WebHook 수신기는 여러 GitHub 리포지토리에서 웹후크를 허용할 수 있습니다.

## <a name="webhook-receiver-uris"></a>웹후크 수신기 URI

Microsoft ASP.NET WebHooks를 설치하면 개방형 서비스 수의 WebHook 요청을 허용하는 일반 WebHook 컨트롤러를 얻을 수 있습니다. 요청이 도착하면 특정 WebHook 발신자를 처리하기 위해 설치한 적절한 수신기를 선택합니다.

이 컨트롤러의 URI는 서비스에 등록하고 양식의 WebHook URI입니다.

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

보안상의 이유로 많은 WebHook 수신기는 URI가 *https* URI여야 하며 경우에 따라 의도한 당사자만 위의 URI에 WebHook을 보낼 수 있도록 적용하는 데 사용되는 추가 쿼리 매개 변수도 포함되어야 합니다.

`<receiver>` 구성 요소는 수신기의 이름(예: `github` `slack`또는 .)입니다.

*{id}는* 특정 WebHook 수신기 구성을 식별하는 데 사용할 수 있는 선택적 식별자입니다. 특정 수신기에 N WebHook을 등록하는 데 사용할 수 있습니다. 예를 들어 다음 세 개의 URI를 사용하여 세 개의 독립적인 WebHook에 등록할 수 있습니다.

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>웹후크 수신기 설치

Microsoft ASP.NET WebHooks를 사용하여 웹후크를 받으려면 먼저 WebHook 공급자 또는 웹후크를 수신하려는 공급자를 위한 Nuget 패키지를 설치합니다. Nuget 패키지의 이름은 [Microsoft.AspNet.WebHooks.Receivers.*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) 마지막 부분에서 지원되는 서비스를 나타냅니다. 예를 들면 다음과 같습니다.

[Microsoft.AspNet.WebHooks.Receivers.GitHub는](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) GitHub및 [Microsoft.AspNet.WebHooks.Receivers.Custom에서](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) 웹후크수신을 지원하며, ASP.NET 웹후크에서 생성된 웹후크수신을 지원합니다.

상자 밖으로 당신은 드롭 박스에 대한 지원을 찾을 수 있습니다, GitHub, MailChimp, 페이팔, 푸셔, 세일즈 포스, 슬랙, 스트라이프, 트렐로, 워드 프레스하지만 다른 공급자의 수를 지원할 수 있습니다.

## <a name="configuring-a-webhook-receiver"></a>웹후크 수신기 구성

WebHook 수신기는 [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface를 통해 구성되며 해당 인터페이스의 특정 구현은 모든 종속성 주입 모델을 사용하여 등록할 수 있습니다. 기본 구현에서는 Web.config 파일에서 설정할 수 있는 응용 프로그램 설정을 사용하거나 Azure Web Apps를 사용하는 경우 [Azure Portal](https://portal.azure.com/)을 통해 설정할 수 있습니다.

![Azure 앱 설정](_static/AzureAppSettings.png)

응용 프로그램 설정 키의 형식은 다음과 같습니다.

```
MS_WebHookReceiverSecret_<receiver>
```

이 값은 다음과 같은 WebHooks가 등록된 *{id}* 값과 일치하는 쉼표로 구분된 값 목록입니다.

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>웹후크 수신기 초기화

WebHook 수신기는 일반적으로 *WebApiConfig* 정적 클래스에 등록하여 초기화됩니다.

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
