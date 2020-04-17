---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: ASP.NET MVC 실행 프로세스 이해 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET MVC 프레임워크가 브라우저 요청을 단계별로 처리하는 방법을 알아봅니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541028"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>ASP.NET MVC 실행 프로세스 이해

[로 마이크로 소프트](https://github.com/microsoft)

> ASP.NET MVC 프레임워크가 브라우저 요청을 단계별로 처리하는 방법을 알아봅니다.

ASP.NET MVC 기반 웹 응용 프로그램에 대한 요청은 먼저 HTTP 모듈인 **UrlRoutingModule** 개체를 통과합니다. 이 모듈에서는 요청을 구문 분석하고 경로 선택을 수행합니다. **Url라우팅모듈** 개체는 현재 요청과 일치하는 첫 번째 경로 개체를 선택합니다. 경로 개체는 **RouteBase를**구현하는 클래스이며 일반적으로 **Route** 클래스의 인스턴스입니다. 일치하는 경로가 없는 경우 **UrlRoutingModule** 개체는 아무 작업도 수행하지 않으며 요청을 일반 ASP.NET 또는 IIS 요청 처리로 되돌릴 수 있습니다.

선택한 **경로** 개체에서 **Url라우팅모듈** 개체는 **라우트** 오브젝트와 연결된 **IRouteHandler** 개체를 가져옵니다. 일반적으로 MVC 응용 프로그램에서 는 **MvcRouteHandler**의 인스턴스가 됩니다. **IRouteHandler** 인스턴스는 **IHttpHandler** 개체를 만들고 **IHttpContext** 개체를 전달합니다. 기본적으로 MVC에 대한 **IHttpHandler** 인스턴스는 **MvcHandler** 개체입니다. 그런 다음 **MvcHandler** 개체는 궁극적으로 요청을 처리할 컨트롤러를 선택합니다.

> [!NOTE]
> ASP.NET MVC 웹 응용 프로그램이 IIS 7.0에서 실행될 경우 MVC 프로젝트의 파일 확장명은 필요하지 않습니다. 그러나 IIS 6.0에서는 처리기의 요청에 따라 .mvc 파일 확장명을 ASP.NET ISAPI DLL에 매핑해야 합니다.

모듈과 처리기는 ASP.NET MVC 프레임워크의 진입점입니다. 두 클래스에서는 다음 작업을 수행합니다.

- MVC 웹 응용 프로그램에서 적절한 컨트롤러를 선택합니다.
- 특정 컨트롤러 인스턴스를 가져옵니다.
- 컨트롤러의 **Execute** 메서드를 호출합니다.

다음은 MVC 웹 프로젝트의 실행 단계를 나열합니다.

- 응용 프로그램에 대한 첫 번째 요청 받기 

    - Global.asax 파일에서 **배관** 오브젝트가 **RouteTable** 오브젝트에 추가됩니다.
- 라우팅 수행 

    - **Url라우팅 모듈** 모듈은 **RouteTable** 컬렉션에서 첫 번째 일치 **하는 경로** 개체를 사용 하 여 **RouteData** 개체를 만든 다음 **요청 컨텍스트** **(IHttpContext)** 개체를 만드는 데 사용 합니다.
- MVC 요청 처리기 만들기 

    - **MvcRouteHandler** 개체는 **MvcHandler** 클래스의 인스턴스를 만들고 **RequestContext** 인스턴스를 전달합니다.
- 컨트롤러 만들기 

    - **MvcHandler** 개체는 **RequestContext** 인스턴스를 사용하여 **IControllerFactory** 개체(일반적으로 **DefaultControllerFactory** 클래스의 인스턴스)를 식별하여 컨트롤러 인스턴스를 만듭니다.
- 컨트롤러 실행 - **MvcHandler** 인스턴스는 컨트롤러의 **Execute** 메서드를 호출합니다. |
- 작업 호출 

    - 대부분의 컨트롤러는 컨트롤러 기본 클래스에서 **상속됩니다.** 이렇게 하는 컨트롤러의 경우 컨트롤러와 연결된 **ControllerActionInvoker** 개체는 호출할 컨트롤러 클래스의 작업 메서드를 결정한 다음 해당 메서드를 호출합니다.
- 결과 실행 

    - 일반적인 작업 메서드는 사용자 입력을 수신하고 적절한 응답 데이터를 준비한 다음 결과 형식을 반환하여 결과를 실행할 수 있습니다. 실행할 수 있는 기본 제공 결과 형식은 **ViewResult(뷰를** 렌더링하고 가장 자주 사용되는 결과 형식), **리디렉션ToRouteResult,** **리디렉션결과,** **ContentResult,** **JsonResult**및 **EmptyResult**입니다.
