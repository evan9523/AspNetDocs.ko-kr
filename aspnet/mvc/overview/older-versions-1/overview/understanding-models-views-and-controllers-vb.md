---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
title: 모델, 뷰 및 컨트롤러 이해 (VB) | Microsoft Docs
author: StephenWalther
description: 모델, 뷰 및 컨트롤러에 대해 혼란 스 러 울 까 요? 이 자습서에서 Stephen Walther는 ASP.NET MVC 응용 프로그램의 다양 한 부분을 소개 합니다.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: a106374a-5e74-4fd0-9ac0-1a32280e5d0d
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
msc.type: authoredcontent
ms.openlocfilehash: e11487cbb863bae230ccb9dfdaf7172c65ec4d43
ms.sourcegitcommit: ffd0f59ef9b7d221a5b2010c32aa61c89c14f406
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042094"
---
# <a name="understanding-models-views-and-controllers-vb"></a>모델, 보기 및 컨트롤러 이해(VB)

[Stephen Walther](https://github.com/StephenWalther)

> 모델, 뷰 및 컨트롤러에 대해 혼란 스 러 울 까 요? 이 자습서에서 Stephen Walther는 ASP.NET MVC 응용 프로그램의 다양 한 부분을 소개 합니다.

이 자습서에서는 ASP.NET MVC 모델, 뷰 및 컨트롤러에 대 한 개략적인 개요를 제공 합니다. 즉, ASP.NET MVC의 M ', V ' 및 C '에 대해 설명 합니다.

이 자습서를 읽은 후에는 ASP.NET MVC 응용 프로그램의 다양 한 부분이 어떻게 함께 작동 하는지 이해 해야 합니다. ASP.NET MVC 응용 프로그램의 아키텍처가 ASP.NET Web Forms 응용 프로그램 또는 Active Server Pages 응용 프로그램과 어떻게 다른 지도 이해 해야 합니다.

## <a name="the-sample-aspnet-mvc-application"></a>샘플 ASP.NET MVC 응용 프로그램

ASP.NET MVC 웹 응용 프로그램을 만들기 위한 기본 Visual Studio 템플릿에는 ASP.NET MVC 응용 프로그램의 다양 한 부분을 이해 하는 데 사용할 수 있는 매우 간단한 샘플 응용 프로그램이 포함 되어 있습니다. 이 자습서에서는이 간단한 응용 프로그램을 활용 합니다.

Visual Studio 2008을 시작 하 고 메뉴 옵션 파일, 새 프로젝트를 차례로 선택 하 여 MVC 템플릿을 사용 하 여 새 ASP.NET MVC 응용 프로그램을 만듭니다 (그림 1 참조). 새 프로젝트 대화 상자의 프로젝트 형식 (Visual Basic 또는 c #)에서 선호 하는 프로그래밍 언어를 선택 하 고 템플릿에서 **ASP.NET MVC 웹 응용 프로그램** 을 선택 합니다. 확인 단추를 클릭합니다.

[![새 프로젝트 대화 상자](understanding-models-views-and-controllers-vb/_static/image1.jpg)](understanding-models-views-and-controllers-vb/_static/image1.png)

**그림 01**: 새 프로젝트 대화 상자 ([전체 크기 이미지를 보려면 클릭](understanding-models-views-and-controllers-vb/_static/image2.png))

새 ASP.NET MVC 응용 프로그램을 만들 때 **단위 테스트 프로젝트 만들기** 대화 상자가 나타납니다 (그림 2 참조). 이 대화 상자를 사용 하 여 ASP.NET MVC 응용 프로그램 테스트를 위한 솔루션에 별도의 프로젝트를 만들 수 있습니다. 옵션 **아니요, 단위 테스트 프로젝트를 만들지 않음** 을 선택 하 고 **확인** 단추를 클릭 합니다.

[![단위 테스트 만들기 대화 상자](understanding-models-views-and-controllers-vb/_static/image2.jpg)](understanding-models-views-and-controllers-vb/_static/image3.png)

**그림 02**: 단위 테스트 만들기 대화 상자 ([전체 크기 이미지를 보려면 클릭](understanding-models-views-and-controllers-vb/_static/image4.png))

새 ASP.NET MVC 응용 프로그램을 만든 후 솔루션 탐색기 창에는 여러 폴더와 파일이 표시 됩니다. 특히 모델, 뷰 및 컨트롤러 라는 세 개의 폴더가 표시 됩니다. 폴더 이름에서 짐작할 수 있듯이 이러한 폴더에는 모델, 뷰 및 컨트롤러를 구현 하기 위한 파일이 포함 되어 있습니다.

Controllers 폴더를 확장 하면 이름이 AccountController .vb이 고 이름이 HomeController 인 파일이 표시 됩니다. Views 폴더를 확장 하면 계정, 홈 및 공유 라는 세 개의 하위 폴더가 표시 됩니다. 홈 폴더를 확장 하면 이름이 .aspx 및 node.js 인 두 개의 추가 파일이 표시 됩니다 (그림 3 참조). 이러한 파일은 기본 ASP.NET MVC 템플릿에 포함 된 샘플 응용 프로그램을 구성 합니다.

[![솔루션 탐색기 창](understanding-models-views-and-controllers-vb/_static/image3.jpg)](understanding-models-views-and-controllers-vb/_static/image5.png)

**그림 03**: 솔루션 탐색기 창 ([전체 크기 이미지를 보려면 클릭](understanding-models-views-and-controllers-vb/_static/image6.png))

**디버그, 디버깅 시작**메뉴 옵션을 선택 하 여 샘플 응용 프로그램을 실행할 수 있습니다. 또는 F5 키를 누를 수 있습니다.

ASP.NET 응용 프로그램을 처음 실행 하면 디버그 모드를 사용 하도록 설정 하는 것을 권장 하는 그림 4의 대화 상자가 나타납니다. 확인 단추를 클릭 하면 응용 프로그램이 실행 됩니다.

[![디버깅 사용 안 함 대화 상자](understanding-models-views-and-controllers-vb/_static/image4.jpg)](understanding-models-views-and-controllers-vb/_static/image7.png)

**그림 04**: 디버깅 사용 안 함 대화 상자 ([전체 크기 이미지를 보려면 클릭](understanding-models-views-and-controllers-vb/_static/image8.png))

ASP.NET MVC 응용 프로그램을 실행 하면 Visual Studio가 웹 브라우저에서 응용 프로그램을 시작 합니다. 샘플 응용 프로그램은 인덱스 페이지와 정보 페이지로 구성 됩니다. 응용 프로그램이 처음 시작 될 때 인덱스 페이지가 나타납니다 (그림 5 참조). 응용 프로그램의 오른쪽 위에 있는 메뉴 링크를 클릭 하 여 정보 페이지로 이동할 수 있습니다.

[![인덱스 페이지](understanding-models-views-and-controllers-vb/_static/image5.jpg)](understanding-models-views-and-controllers-vb/_static/image9.png)

**그림 05**: 인덱스 페이지 ([전체 크기 이미지를 보려면 클릭](understanding-models-views-and-controllers-vb/_static/image10.png))

브라우저의 주소 표시줄에서 Url을 확인 합니다. 예를 들어 정보 메뉴 링크를 클릭 하면 브라우저 주소 표시줄의 URL이 **/Home/About**로 변경 됩니다.

브라우저 창을 닫고 Visual Studio로 돌아가면 Home/About 경로를 사용 하 여 파일을 찾을 수 없습니다. 파일이 존재 하지 않습니다. 가능한 방법은 무엇 인가요?

## <a name="a-url-does-not-equal-a-page"></a>URL이 페이지와 같지 않음

기존 ASP.NET Web Forms 응용 프로그램 또는 Active Server Pages 응용 프로그램을 빌드하는 경우 URL과 페이지 사이에 일 대 일 대응 관계가 있습니다. 서버에서 SomePage 라는 페이지를 요청 하면 SomePage 라는 디스크에 페이지가 더 잘 표시 됩니다. SomePage 파일이 없는 경우 **404-페이지를 찾을** 수 없음 오류가 표시 됩니다.

ASP.NET MVC 응용 프로그램을 빌드할 때 브라우저의 주소 표시줄에 입력 하는 URL과 응용 프로그램에서 찾을 수 있는 파일 간에는 아무런 관계가 없습니다. ASP.NET MVC 응용 프로그램에서 URL은 디스크에 있는 페이지 대신 컨트롤러 작업에 해당 합니다.

기존 ASP.NET 또는 ASP 응용 프로그램에서 브라우저 요청은 페이지에 매핑됩니다. 반면 ASP.NET MVC 응용 프로그램에서 브라우저 요청은 컨트롤러 작업에 매핑됩니다. ASP.NET Web Forms 응용 프로그램은 콘텐츠 중심입니다. 이와 대조적으로 ASP.NET MVC 응용 프로그램은 응용 프로그램 논리 중심입니다.

## <a name="understanding-aspnet-routing"></a>ASP.NET 라우팅 이해

브라우저 요청은 *ASP.NET Routing*이라는 ASP.NET framework의 기능을 통해 컨트롤러 작업에 매핑됩니다. ASP.NET 라우팅은 ASP.NET MVC 프레임 워크에서 들어오는 요청을 컨트롤러 작업으로 *라우팅하* 는 데 사용 됩니다.

ASP.NET 라우팅은 경로 테이블을 사용 하 여 들어오는 요청을 처리 합니다. 이 경로 테이블은 웹 응용 프로그램이 처음 시작 될 때 생성 됩니다. 경로 테이블은 Global.asax 파일에 설치 됩니다. 기본 MVC global.asax 파일은 목록 1에 포함 되어 있습니다.

**목록 1-global.asax**

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample1.vb)]

ASP.NET 응용 프로그램이 처음 시작 될 때 응용 프로그램 \_ Start () 메서드가 호출 됩니다. 목록 1에서이 메서드는 RegisterRoutes () 메서드를 호출 하 고 RegisterRoutes () 메서드는 기본 경로 테이블을 만듭니다.

기본 경로 테이블은 하나의 경로로 구성 됩니다. 이 기본 경로는 들어오는 모든 요청을 세 개의 세그먼트로 나눕니다. URL 세그먼트는 슬래시 사이의 모든 항목입니다. 첫 번째 세그먼트는 컨트롤러 이름에 매핑되고 두 번째 세그먼트는 동작 이름에 매핑되고 최종 세그먼트는 action 이라는 액션에 전달 된 매개 변수에 매핑됩니다.

예를 들어 다음 URL을 가정해 봅니다.

/Product/Details/3

이 URL은 다음과 같은 세 개의 매개 변수로 구문 분석 됩니다.

Controller = Product

작업 = 세부 정보

Id = 3

Global.asax 파일에 정의 된 기본 경로에는 세 매개 변수 모두에 대 한 기본값이 포함 됩니다. 기본 컨트롤러는 Home이 고 기본 동작은 Index 이며 기본 Id는 빈 문자열입니다. 이러한 기본값을 염두에 두면 다음 URL을 구문 분석 하는 방법을 고려해 야 합니다.

/Employee

이 URL은 다음과 같은 세 개의 매개 변수로 구문 분석 됩니다.

Controller = 직원

작업 = 인덱스

Id =?

마지막으로, URL (예:)을 제공 하지 않고 ASP.NET MVC 응용 프로그램을 여는 경우 `http://localhost` url은 다음과 같이 구문 분석 됩니다.

컨트롤러 = 홈

작업 = 인덱스

Id =?

요청은 HomeController 클래스에서 Index () 동작으로 라우팅됩니다.

## <a name="understanding-controllers"></a>컨트롤러 이해

컨트롤러는 사용자가 MVC 응용 프로그램과 상호 작용 하는 방식을 제어 하는 일을 담당 합니다. 컨트롤러는 ASP.NET MVC 응용 프로그램에 대 한 흐름 제어 논리를 포함 합니다. 컨트롤러는 사용자가 브라우저 요청을 만들 때 사용자에 게 다시 보낼 응답을 결정 합니다.

컨트롤러는 단지 클래스 (예: Visual Basic 또는 c # 클래스)입니다. 샘플 ASP.NET MVC 응용 프로그램에는 Controllers 폴더에 있는 HomeController 라는 컨트롤러가 포함 되어 있습니다. HomeController 파일의 내용은 목록 2에서 재현 됩니다.

**목록 2-HomeController.cs**

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample2.vb)]

HomeController에는 Index ()와 About () 라는 두 개의 메서드가 있습니다. 이러한 두 메서드는 컨트롤러에서 노출 하는 두 작업에 해당 합니다. URL/Home/Index는 HomeController () 메서드를 호출 하 고, URL/Home/About는 HomeController () 메서드를 호출 합니다.

컨트롤러의 모든 공용 메서드는 컨트롤러 작업으로 노출 됩니다. 이에 대해 주의 해야 합니다. 즉, 브라우저에 올바른 URL을 입력 하 여 인터넷에 액세스할 수 있는 모든 사용자가 컨트롤러에 포함 된 공용 메서드를 호출할 수 있습니다.

## <a name="understanding-views"></a>뷰 이해

HomeController 클래스, Index () 및 About ()에서 노출 하는 두 개의 컨트롤러 작업은 모두 뷰를 반환 합니다. 보기에는 브라우저에 전송 된 HTML 태그 및 콘텐츠가 포함 됩니다. 뷰는 ASP.NET MVC 응용 프로그램으로 작업할 때 페이지에 해당 합니다.

올바른 위치에 보기를 만들어야 합니다. HomeController () 작업은 다음 경로에 있는 뷰를 반환 합니다.

\Views\Home\Index.aspx

HomeController () 작업은 다음 경로에 있는 뷰를 반환 합니다.

\Views\Home\About.aspx

일반적으로 컨트롤러 작업에 대 한 보기를 반환 하려는 경우에는 컨트롤러와 동일한 이름을 사용 하 여 Views 폴더에 하위 폴더를 만들어야 합니다. 하위 폴더 내에서 컨트롤러 작업과 동일한 이름을 사용 하 여 .aspx 파일을 만들어야 합니다.

목록 3의 파일에는 .aspx 뷰가 포함 되어 있습니다.

**목록 3-.aspx 정보**

[!code-aspx[Main](understanding-models-views-and-controllers-vb/samples/sample3.aspx)]

목록 3의 첫 번째 줄을 무시 하면 대부분의 나머지 뷰가 표준 HTML로 구성 됩니다. 여기에서 원하는 HTML을 입력 하 여 보기의 내용을 수정할 수 있습니다.

보기는 Active Server Pages 또는 ASP.NET Web Forms의 페이지와 매우 비슷합니다. 뷰에는 HTML 내용과 스크립트가 포함 될 수 있습니다. 스크립트를 선호 하는 .NET 프로그래밍 언어 (예: c # 또는 Visual Basic .NET)로 작성할 수 있습니다. 스크립트를 사용 하 여 데이터베이스 데이터와 같은 동적 콘텐츠를 표시 합니다.

## <a name="understanding-models"></a>모델 이해

여기서는 컨트롤러에 대해 설명 하 고 보기에 대해 설명 했습니다. 설명 해야 하는 마지막 항목은 모델입니다. MVC 모델 이란?

MVC 모델에는 뷰나 컨트롤러에 포함 되지 않은 모든 응용 프로그램 논리가 포함 됩니다. 모델에는 모든 응용 프로그램 비즈니스 논리, 유효성 검사 논리 및 데이터베이스 액세스 논리가 포함 되어야 합니다. 예를 들어 Microsoft Entity Framework를 사용 하 여 데이터베이스에 액세스 하는 경우 모델 폴더에 Entity Framework 클래스 (.edmx 파일)를 만듭니다.

뷰에는 사용자 인터페이스 생성과 관련 된 논리도 포함 되어야 합니다. 컨트롤러는 올바른 뷰를 반환 하거나 사용자를 다른 작업 (흐름 제어)으로 리디렉션하는 데 필요한 최소한의 논리를 포함 해야 합니다. 다른 모든 항목은 모델에 포함 되어야 합니다.

일반적으로는 fat 모델과 skinny 컨트롤러에 대해 노력 해야 합니다. 컨트롤러 메서드는 코드를 몇 줄만 포함 해야 합니다. 컨트롤러 작업에서 너무 많은 작업을 수행 하는 경우에는 모델 폴더에서 논리를 새 클래스로 이동 하는 것을 고려해 야 합니다.

## <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 웹 응용 프로그램의 다양 한 부분에 대 한 개략적인 개요를 제공 했습니다. ASP.NET 라우팅이 들어오는 브라우저 요청을 특정 컨트롤러 작업에 매핑하는 방법을 배웠습니다. 컨트롤러에서 뷰가 브라우저에 반환 되는 방식을 조정 하는 방법을 배웠습니다. 마지막으로 모델에서 응용 프로그램 비즈니스, 유효성 검사 및 데이터베이스 액세스 논리를 포함 하는 방법을 배웠습니다.
