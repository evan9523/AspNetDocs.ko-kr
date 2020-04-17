---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: IIS (VB)의 다른 버전과 ASP.NET MVC사용 | 마이크로 소프트 문서
author: rick-anderson
description: 이 자습서에서는 다른 버전의 인터넷 정보 서비스와 ASP.NET MVC 및 URL 라우팅을 사용하는 방법을 배웁니다. 당신은 다른 전략을 배울 ...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: 5e04ae14026e6d5dd1e603be6c52ff6876a468cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542003"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a>다양한 버전의 IIS에 ASP.NET MVC 사용(VB)

[로 마이크로 소프트](https://github.com/microsoft)

> 이 자습서에서는 다른 버전의 인터넷 정보 서비스와 ASP.NET MVC 및 URL 라우팅을 사용하는 방법을 배웁니다. IIS 7.0(클래식 모드), IIS 6.0 및 이전 버전의 IIS에서 ASP.NET MVC를 사용하기 위한 다양한 전략을 배웁니다.

ASP.NET MVC 프레임워크는 브라우저 요청을 컨트롤러 작업으로 라우팅하기 위해 ASP.NET 라우팅에 따라 달라집니다. ASP.NET 라우팅을 활용하려면 웹 서버에서 추가 구성 단계를 수행해야 할 수 있습니다. 모든 것은 IIS(인터넷 정보 서비스) 버전과 응용 프로그램에 대한 요청 처리 모드에 따라 달라집니다.

다음은 IIS의 다른 버전에 대한 요약입니다.

- IIS 7.0(통합 모드) - 라우팅을 ASP.NET 사용할 필요가 없는 특별한 구성입니다.
- IIS 7.0(클래식 모드) - ASP.NET 라우팅을 사용하려면 특수 구성을 수행해야 합니다.
- IIS 6.0 이상 - 라우팅을 ASP.NET 사용하려면 특별한 구성을 수행해야 합니다.

IIS의 최신 버전은 버전 7.5 (Win7)입니다. IIS의 IIS 7은 Windows 서버 2008 및 VISTA/SP1 이상에 포함되어 있습니다. 또한 홈 베이직(참조)을 [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)제외한 모든 버전의 Vista 운영 체제에 IIS 7.0을 설치할 수 있습니다.

IIS 7.0은 요청을 처리하기 위한 두 가지 모드를 지원합니다. 통합 모드 또는 클래식 모드를 사용할 수 있습니다. 통합 모드에서 IIS 7.0을 사용할 때는 특별한 구성 단계를 수행할 필요가 없습니다. 그러나 클래식 모드에서 IIS 7.0을 사용할 때는 추가 구성을 수행해야 합니다.

마이크로 소프트 윈도우 서버 2003 IIS 6.0을 포함한다. Windows Server 2003 운영 체제를 사용하는 경우 IIS 6.0을 IIS 7.0으로 업그레이드할 수 없습니다. IIS 6.0을 사용할 때추가 구성 단계를 수행해야 합니다.

마이크로 소프트 윈도우 XP 전문가는 IIS 5.1을 포함한다. IIS 5.1을 사용할 때 추가 구성 단계를 수행해야 합니다.

마지막으로, 마이크로 소프트 윈도우 2000 마이크로 소프트 윈도우 2000 프로페셔널은 IIS 5.0을 포함한다. IIS 5.0을 사용할 때추가 구성 단계를 수행해야 합니다.

## <a name="integrated-versus-classic-mode"></a>통합 대 클래식 모드

IIS 7.0은 통합 및 클래식이라는 두 가지 요청 처리 모드를 사용하여 요청을 처리할 수 있습니다. 통합 모드는 더 나은 성능과 더 많은 기능을 제공합니다. 이전 버전의 IIS와의 이전 버전과의 호환성을 위해 클래식 모드가 포함되어 있습니다.

요청 처리 모드는 응용 프로그램 풀에 의해 결정됩니다. 응용 프로그램과 연결된 응용 프로그램 풀을 확인하여 특정 웹 응용 프로그램에서 사용 중인 처리 모드를 확인할 수 있습니다. 다음 단계를 수행하세요.

1. 인터넷 정보 서비스 관리자 시작
2. 연결 창에서 응용 프로그램을 선택합니다.
3. 작업 창에서 기본 **설정** 링크를 클릭하여 응용 프로그램 편집 대화 상자를 엽니다(그림 1 참조).
4. 선택한 응용 프로그램 풀을 기록해 둡것입니다.

기본적으로 IIS는 두 개의 응용 프로그램 풀을 지원하도록 구성됩니다: **DefaultAppPool** 및 **Classic .NET AppPool**. DefaultAppPool을 선택하면 응용 프로그램이 통합 요청 처리 모드에서 실행되고 있습니다. 클래식 .NET AppPool을 선택한 경우 응용 프로그램이 클래식 요청 처리 모드에서 실행중입니다.

[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)

**그림 1**: 요청 처리 모드 감지[(전체 크기 이미지를 보려면 클릭)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png)

응용 프로그램 편집 대화 상자 내에서 요청 처리 모드를 수정할 수 있습니다. 선택 단추를 클릭하고 응용 프로그램과 연결된 응용 프로그램 풀을 변경합니다. ASP.NET 응용 프로그램을 클래식 모드에서 통합 모드로 변경할 때 호환성 문제가 있음을 알 수 있습니다. 자세한 내용은 다음 문서를 참조하세요.

- Windows Vista 및 Windows 서버 2008에서 ASP.NET IIS 7.0으로 업그레이드 --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)

- iIS 7.0과의 ASP.NET 통합 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

ASP.NET 응용 프로그램이 DefaultAppPool을 사용하는 경우 라우팅(ASP.NET 따라서 MVC)ASP.NET 작동하기 위해 추가 단계를 수행할 필요가 없습니다. 그러나 ASP.NET 응용 프로그램이 Classic .NET AppPool을 사용하도록 구성된 경우 계속 읽으면 더 많은 작업을 수행할 수 있습니다.

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>이전 버전의 IIS와 ASP.NET MVC 사용

IIS 7.0보다 이전 버전의 IIS와 ASP.NET MVC를 사용해야 하거나 클래식 모드에서 IIS 7.0을 사용해야 하는 경우 두 가지 옵션이 있습니다. 먼저 파일 확장프로그램을 사용하도록 경로 테이블을 수정할 수 있습니다. 예를 들어 /Store/Details와 같은 URL을 요청하는 대신 /Store.aspx/Details와 같은 URL을 요청합니다.

두 번째 옵션은 *와일드카드 스크립트 맵이라는*것을 만드는 것입니다. 와일드카드 스크립트 맵을 사용하면 모든 요청을 ASP.NET 프레임워크에 매핑할 수 있습니다.

웹 서버에 액세스할 수 없는 경우(예: ASP.NET MVC 응용 프로그램이 인터넷 서비스 공급자가 호스팅하는 경우) 첫 번째 옵션을 사용해야 합니다. URL의 모양을 수정하지 않고 웹 서버에 액세스할 수 있는 경우 두 번째 옵션을 사용할 수 있습니다.

다음 섹션에서 각 옵션을 자세히 살펴봅니다.

## <a name="adding-extensions-to-the-route-table"></a>배관 테이블에 확장 추가

이전 버전의 IIS에서 작동하도록 ASP.NET 라우팅을 얻는 가장 쉬운 방법은 Global.asax 파일에서 경로 테이블을 수정하는 것입니다. 목록 1의 기본 및 수정되지 않은 Global.asax 파일은 기본 경로라는 하나의 경로를 구성합니다.

**리스팅 1 - 글로벌.asax(수정되지 않은)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

목록 1에 구성된 기본 경로를 사용하면 다음과 같은 URL을 라우팅할 수 있습니다.

/홈/인덱스

/제품/세부 정보/3

/Product

안타깝게도 이전 버전의 IIS는 이러한 요청을 ASP.NET 프레임워크에 전달하지 않습니다. 따라서 이러한 요청은 컨트롤러로 라우팅되지 않습니다. 예를 들어 URL/홈/인덱스에 대한 브라우저 요청을 하면 그림 2의 오류 페이지가 표시됩니다.

[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)

**그림 2**: 404 찾을 수 없는 오류 수신[(전체 크기 이미지를 보려면 클릭)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png)

이전 버전의 IIS는 특정 요청을 ASP.NET 프레임워크에만 매핑합니다. 요청은 올바른 파일 확장이 있는 URL이어야 합니다. 예를 들어 /SomePage.aspx에 대한 요청은 ASP.NET 프레임워크에 매핑됩니다. 그러나 /SomePage.htm에 대한 요청은 그렇지 않습니다.

따라서 라우팅ASP.NET 작동하려면 ASP.NET 프레임워크에 매핑된 파일 확장자를 포함하도록 기본 경로를 수정해야 합니다.

이 작업은 . `registermvc.wsf` ASP.NET MVC 1 릴리스에 `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`포함되었지만 ASP.NET 2현재 이 스크립트는 에서 [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)사용할 수 있는 ASP.NET 선물로 이동되었습니다.

이 스크립트를 실행하면 IIS에 새 .mvc 확장이 등록됩니다. .mvc 확장을 등록한 후 경로가 .mvc 확장을 사용하도록 Global.asax 파일에서 경로를 수정할 수 있습니다.

리스팅 2의 수정된 Global.asax 파일은 이전 버전의 IIS에서 작동합니다.

**리스팅 2 - Global.asax(확장으로 수정)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

중요: Global.asax 파일을 변경한 후 ASP.NET MVC 응용 프로그램을 다시 빌드해야 합니다.

목록 2의 Global.asax 파일에는 두 가지 중요한 변경 사항이 있습니다. 이제 Global.asax에 정의된 두 개의 경로가 있습니다. 기본 경로의 URL 패턴인 첫 번째 경로는 다음과 같습니다.

{컨트롤러}.mvc/{작업}/{id}

.mvc 확장자를 추가하면 ASP.NET 라우팅 모듈이 가로채는 파일 의 형식이 변경됩니다. 이 변경으로 ASP.NET MVC 응용 프로그램은 이제 다음과 같은 요청을 라우팅합니다.

/Home.mvc/인덱스/

/Product.mvc/세부 정보/3

/Product.mvc/

두 번째 경로인 루트 경로는 새 경로입니다. 루트 경로에 대한 이 URL 패턴은 빈 문자열입니다. 이 경로는 응용 프로그램의 루트에 대해 만든 요청을 일치시키는 데 필요합니다. 예를 들어 루트 경로는 다음과 같은 요청과 일치합니다.

[http://www.YourApplication.com/](http://www.YourApplication.com/)

경로 테이블을 수정한 후에는 응용 프로그램의 모든 링크가 이러한 새 URL 패턴과 호환되는지 확인해야 합니다. 즉, 모든 링크에 .mvc 확장이 포함되어 있는지 확인합니다. Html.ActionLink() 도우미 메서드를 사용하여 링크를 생성하는 경우 변경할 필요가 없습니다.

registermvc.wcf 스크립트를 사용하는 대신 ASP.NET 프레임워크에 직접 매핑되는 IIS에 새 확장을 추가할 수 있습니다. 새 확장프로그램을 직접 추가할 때 **파일이 있는지 확인이라는** 확인란이 선택되어 있지 않은지 확인합니다.

## <a name="hosted-server"></a>호스팅 서버

웹 서버에 항상 액세스할 수 있는 것은 아닙니다. 예를 들어 인터넷 호스팅 공급자를 사용하여 ASP.NET MVC 응용 프로그램을 호스팅하는 경우 IIS에 반드시 액세스할 수 있는 것은 아닙니다.

이 경우 ASP.NET 프레임워크에 매핑된 기존 파일 확장명 중 하나를 사용해야 합니다. ASP.NET 매핑된 파일 확장자의 예로는 .aspx, .axd 및 .ashx 확장인이 있습니다.

예를 들어 목록 3의 수정된 Global.asax 파일은 .mvc 확장자 대신 .aspx 확장을 사용합니다.

**목록 3 - Global.asax(.aspx 확장으로 수정)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

목록 3의 Global.asax 파일은 .mvc 확장자 대신 .aspx 확장을 사용한다는 사실을 제외하고는 이전 Global.asax 파일과 정확히 동일합니다. .aspx 확장을 사용 하려면 원격 웹 서버에서 설정을 수행할 필요가 없습니다.

## <a name="creating-a-wildcard-script-map"></a>와일드카드 스크립트 맵 만들기

ASP.NET MVC 응용 프로그램에 대한 URL을 수정하지 않고 웹 서버에 액세스할 수 있는 경우 추가 옵션이 있습니다. 웹 서버에 대한 모든 요청을 ASP.NET 프레임워크에 매핑하는 와일드카드 스크립트 맵을 만들 수 있습니다. 이렇게 하면 IIS 7.0(클래식 모드) 또는 IIS 6.0에서 기본 ASP.NET MVC 경로 테이블을 사용할 수 있습니다.

이 옵션을 사용하면 IIS가 웹 서버에 대한 모든 요청을 가로챌 수 있습니다. 여기에는 이미지, 클래식 ASP 페이지 및 HTML 페이지에 대한 요청이 포함됩니다. 따라서 와일드카드 스크립트 맵을 ASP.NET 활성화하면 성능에 영향을 미칩니다.

IIS 7.0에 와일드카드 스크립트 맵을 사용하도록 설정하는 방법은 다음과 같습니다.

1. 연결 창에서 응용 프로그램 선택
2. **피처** 뷰가 선택되어 있는지 확인
3. **처리기 매핑 단추를** 두 번 클릭합니다.
4. 와일드카드 **스크립트 맵 추가** 링크를 클릭합니다(그림 3 참조)
5. aspnet\_isapi.dll 파일에 대한 경로를 입력합니다(PageHandlerFactory 스크립트 맵에서 이 경로를 복사할 수 있음)
6. MVC 이름 입력
7. **확인** 버튼을 클릭합니다.

[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)

**그림 3**: IIS 7.0으로 와일드카드 스크립트 맵 만들기(전체[크기 이미지를 보려면 클릭)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png)

다음 단계에 따라 IIS 6.0을 사용하여 와일드카드 스크립트 맵을 만듭니다.

1. 웹 사이트를 마우스 오른쪽 단추로 클릭하고 속성을 선택합니다.
2. 홈 **디렉토리** 탭 선택
3. **구성** 단추를 클릭합니다.
4. **매핑** 탭 선택
5. **삽입** 단추를 클릭합니다(그림 4 참조)
6. 실행 파일 필드에 aspnet\_isapi.dll에 대한 경로를 붙여 넣습니다(.aspx 파일의 스크립트 맵에서 이 경로를 복사할 수 있음).
7. 레이블이 붙은 확인란의 선택 취소 **파일이 있는지 확인합니다.**
8. **확인** 버튼을 클릭합니다.

[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)

**그림 4**: IIS 6.0으로 와일드카드 스크립트 맵 만들기(전체[크기 이미지를 보려면 클릭)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png)

와일드카드 스크립트 맵을 사용하도록 설정한 후에는 루트 경로를 포함하도록 Global.asax 파일의 경로 테이블을 수정해야 합니다. 그렇지 않으면 응용 프로그램의 루트 페이지를 요청할 때 그림 5의 오류 페이지가 표시됩니다. 리스팅 4에서 수정된 Global.asax 파일을 사용할 수 있습니다.

[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)

**그림 5**: 루트 경로 오류 누락[(전체 크기 이미지를 보려면 클릭)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png)

**리스팅 4 - Global.asax(루트 경로로 수정)**

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

IIS 7.0 또는 IIS 6.0에 와일드카드 스크립트 맵을 사용하도록 설정한 후 다음과 같은 기본 경로 테이블에서 작동하는 요청을 만들 수 있습니다.

/

/홈/인덱스

/제품/세부 정보/3

/Product

## <a name="summary"></a>요약

이 자습서의 목표는 이전 버전의 IIS(또는 클래식 모드에서 IIS 7.0)를 사용할 때 ASP.NET MVC를 사용하는 방법을 설명하는 것이었습니다. 이전 버전의 IIS에서 작동하도록 라우팅을 ASP.NET 두 가지 방법인 기본 경로 테이블을 수정하거나 와일드카드 스크립트 맵을 만드는 방법에 대해 설명했습니다.

첫 번째 옵션은 ASP.NET MVC 응용 프로그램에 사용되는 URL을 수정해야 합니다. 이 첫 번째 옵션의 가장 큰 장점 중 하나는 경로 테이블을 수정하기 위해 웹 서버에 액세스할 필요가 없다는 것입니다. 즉, 인터넷 호스팅 회사에서 ASP.NET MVC 응용 프로그램을 호스팅하는 경우에도 이 첫 번째 옵션을 사용할 수 있습니다.

두 번째 옵션은 와일드카드 스크립트 맵을 만드는 것입니다. 이 두 번째 옵션의 장점은 URL을 수정할 필요가 없다는 것입니다. 이 두 번째 옵션의 단점은 ASP.NET MVC 응용 프로그램의 성능에 영향을 미칠 수 있다는 것입니다.

> [!div class="step-by-step"]
> [이전](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
