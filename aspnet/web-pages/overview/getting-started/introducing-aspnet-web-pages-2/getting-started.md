---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: 시작 | Microsoft Docs
author: Rick-Anderson
description: WebMatrix는 ASP.NET 웹 페이지을 위한 통합 개발 환경으로 더 이상 권장 되지 않습니다. Visual Studio 또는 Visual Studio Code를 사용 합니다. 이 지침
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ac2111980e6393388a0530375fb9ef78dbbfaff6
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240762"
---
# <a name="getting-started"></a>시작

[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > WebMatrix는 ASP.NET 웹 페이지을 위한 통합 개발 환경으로 더 이상 권장 되지 않습니다. [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) 또는 [Visual Studio Code](https://code.visualstudio.com/)를 사용 합니다.
> 
> 
> 이 지침 및 응용 프로그램은 동적 웹 사이트를 만들기 위한 간단한 프레임 워크로 ASP.NET 웹 페이지 (버전 2 이상) 및 Razor 구문에 대 한 개요를 제공 합니다. 또한 페이지 및 사이트를 만들기 위한 도구인 WebMatrix를 소개 합니다.
> 
> **수준**: ASP.NET 웹 페이지를 새로 만들기 위한 것입니다.  
> **가정**하는 기술: HTML, 기본 css 스타일 시트 (css).
> 
> 집합의 첫 번째 자습서에서 학습할 내용:
> 
> - ASP.NET 웹 페이지 기술의 정의와 용도입니다.
> - WebMatrix는 무엇 인가요?
> - 모든 항목을 설치 하는 방법
> - WebMatrix를 사용 하 여 웹 사이트를 만드는 방법
>   
> 
> 설명 하는 기능/기술:
> 
> - Microsoft 웹 플랫폼 설치 관리자.
> - WebMatrix.
> - *. cshtml* 페이지
>   
> 
> Mike Pope는 원래이 자습서를 작성 했습니다. Microsoft WebMatrix 3 용으로 업데이트 되었습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 3

## <a name="what-should-you-know"></a>무엇을 알아야 하나요?

다음에 대해 잘 알고 있다고 가정 합니다.

- **HTML**. 심층적인 전문 지식이 필요 하지 않습니다. HTML에 대해서는 설명 하지 않지만 복잡 한 항목은 사용 하지 않습니다. 유용 하다 고 생각 되는 HTML 자습서에 대 한 링크를 제공 합니다.
- **Css 스타일 시트**입니다. HTML과 동일 합니다.
- **기본 데이터베이스 아이디어**. 데이터에 스프레드시트를 사용 하 여 데이터를 정렬 하 고 필터링 한 경우이 자습서를 일반적으로이 자습서로 가정 하는 전문 지식 수준입니다.

또한 기본적인 프로그래밍을 배우는 데 관심이 있다고 가정 합니다. C # 이라는 프로그래밍 언어를 사용 ASP.NET 웹 페이지 합니다. 프로그래밍에 대 한 배경 지식이 없어도 됩니다. 이전에 웹 페이지에서 JavaScript를 작성 한 적이 있다면 많은 배경을가지고 있습니다.

프로그래밍에 대해 잘 알고 있는 경우에는이 자습서 집합을 처음부터 빠르게 이동 하는 동안 새 프로그래머가 빠르게 이동 하는 것을 알 수 있습니다. 처음에는 몇 가지 자습서를 수행 하는 것 처럼 간단 하 게 설명할 수 있으며 더 빠른 클립으로 이동 하는 것도 있습니다.

## <a name="what-do-you-need"></a>무엇이 필요 한가요?

다음 항목이 필요합니다.

- Windows 8, Windows 7, Windows Server 2008 또는 Windows Server 2012를 실행 하는 컴퓨터
- 라이브 인터넷 연결.
- 관리자 권한 (설치 프로세스에 필요)

## <a name="what-is-aspnet-web-pages"></a>ASP.NET 웹 페이지 이란?

ASP.NET 웹 페이지는 동적 웹 페이지를 만드는 데 사용할 수 있는 프레임 워크입니다. 간단한 HTML 웹 페이지는 정적입니다. 해당 콘텐츠는 페이지에 있는 고정 HTML 태그에 의해 결정 됩니다. ASP.NET 웹 페이지를 사용 하 여 만든 것과 같은 동적 페이지를 통해 코드를 사용 하 여 즉시 페이지 콘텐츠를 만들 수 있습니다.

동적 페이지를 사용 하면 모든 종류의 작업을 수행할 수 있습니다. 양식을 사용 하 여 사용자에 게 입력 하 라는 메시지를 표시 한 다음 페이지가 표시 되는 내용과 표시 되는 모양을 변경할 수 있습니다. 사용자의 정보를 가져와서 데이터베이스에 저장 한 다음 나중에 나열할 수 있습니다. 사이트에서 전자 메일을 보낼 수 있습니다. 웹의 다른 서비스 (예: 매핑 서비스)와 상호 작용 하 고 이러한 원본의 정보를 통합 하는 페이지를 생성할 수 있습니다.

## <a name="what-is-webmatrix"></a>WebMatrix 란?

WebMatrix는 웹 페이지 편집기, 데이터베이스 유틸리티, 테스트 페이지에 대 한 웹 서버 및 웹 사이트를 인터넷에 게시 하기 위한 기능을 통합 하는 도구입니다. WebMatrix는 무료 이며 쉽게 설치 하 고 사용할 수 있습니다. (PHP와 같은 기타 기술 뿐만 아니라 일반 HTML 페이지에도 적용 됩니다.)

실제로 *는* WebMatrix를 사용 하 여 ASP.NET 웹 페이지 작업을 수행할 필요가 없습니다. 텍스트 편집기 (예:)를 사용 하 여 페이지를 만들고, 액세스 권한이 있는 웹 서버를 사용 하 여 페이지를 테스트할 수 있습니다. 그러나 WebMatrix를 사용 하면 모든 것이 매우 쉽지만 이러한 자습서에서는 전체에서 WebMatrix를 사용 합니다.

## <a name="about-these-tutorials"></a>이러한 자습서 정보

이 자습서 집합은 ASP.NET 웹 페이지를 사용 하는 방법에 대 한 소개입니다. 이 소개 자습서 집합에는 9 개의 자습서 합계가 있습니다. ASP.NET 웹 페이지 초보자가 전문적이 고 전문적인 웹 사이트를 만드는 과정을 안내 하는 일련의 자습서 집합의 일부입니다.

이 첫 번째 자습서에서는 ASP.NET 웹 페이지 작업 하는 방법에 대 한 기본 사항을 보여 줍니다. 완료 되 면이를 선택 하 고 웹 페이지를 더 자세히 탐색 하는 추가 자습서 집합을 사용할 수 있습니다.

이에 대 한 자세한 설명은 의도적으로 쉽게 설명 합니다. 무엇을 보여줄 때마다이 자습서를 설정 하는 것이 가장 쉽게 이해 하는 방법을 선택 합니다. 이후 자습서에서는 더 깊이 있게 전환 하 고 더 효율적이 고 유연한 접근 방식을 보여 줍니다. 그러나 이러한 자습서에서는 먼저 기본 사항을 이해 해야 합니다.

방금 시작한 자습서 집합은 다음과 같은 ASP.NET 웹 페이지 기능을 다룹니다.

- 설치를 소개 하 고 모든 항목을 가져옵니다. (여기서는 읽고 있는 자습서에 있습니다.)
- ASP.NET 웹 페이지 프로그래밍에 대 한 기본 사항입니다.
- 데이터베이스 만들기
- 사용자 입력 폼 만들기 및 처리
- 데이터베이스에서 데이터를 추가, 업데이트 및 삭제 합니다.

## <a name="what-will-you-create"></a>무엇을 만드시겠습니까?

이 자습서를 설정 하 고 이후에 원하는 영화를 나열할 수 있는 웹 사이트를 중심으로 합니다. 영화를 입력 하 고, 편집 하 고, 표시할 수 있습니다. 이 자습서 집합에서 만들 두 페이지는 다음과 같습니다. 첫 번째는 만들 동영상 목록 페이지를 보여 줍니다.

![영화 목록을 보여 주는 finshed 영화 앱](getting-started/_static/image1.png)

사이트에 새 영화 정보를 추가할 수 있는 페이지는 다음과 같습니다.

![동영상 추가 페이지를 표시 하는 완료 된 동영상 앱](getting-started/_static/image2.png)

이후 자습서에서는이 집합에 빌드를 설정 하 고 그림 업로드, 사용자의 로그인, 전자 메일 보내기, 소셜 미디어와의 통합 등의 추가 기능을 추가 합니다.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 앱 확인

완료 된 사이트가 라이브 웹 앱으로 실행 되 고 있는지 확인 하 시겠습니까? 다음 단추를 클릭 하기만 하면 Azure 계정에 전체 버전의 앱을 배포할 수 있습니다.

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음과 같은 옵션을 사용할 수 있습니다.

- [무료로 azure 계정 열기](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -유료 azure 서비스를 사용 하는 데 사용할 수 있는 크레딧을 확보 하 고, 사용한 후에도 계정을 유지 하 고 무료 Azure 서비스를 사용할 수 있습니다.
- [Msdn 구독자 혜택 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -msdn 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공 합니다.

## <a name="installing-everything"></a>모든 항목 설치

Microsoft에서 웹 플랫폼 설치 관리자를 사용 하 여 모든 항목을 설치할 수 있습니다. 실제로 설치 관리자를 설치 하 고이를 사용 하 여 다른 모든 항목을 설치 합니다.

웹 페이지를 사용 하려면 Windows XP SP3 이상이 설치 되어 있거나 Windows Server 2008 이상이 있어야 합니다.

ASP.NET 웹 사이트의 [웹 페이지 페이지](../../../index.md) 에서 **설치**를 클릭 합니다.

![&quot;WebMatrix 설치 단추를 표시 하는 ASP.NET 웹 사이트 &quot;](getting-started/_static/image3.png)

WebMatrix를 설치 하기 전에 사용 조건 및 개인정보 처리 방침에 동의 하 라는 메시지가 표시 됩니다.

![약관에 동의 하 여 설치 시작](getting-started/_static/image4.png)

**실행** 을 클릭 하 여 설치를 시작 합니다. 설치 관리자를 저장 하려면 **저장** 을 클릭 한 다음 저장 한 폴더에서 설치 관리자를 실행 합니다.

![](getting-started/_static/image5.png)

웹 플랫폼 설치 관리자가 WebMatrix를 설치할 준비가 되었습니다. **Install**을 클릭합니다.

![](getting-started/_static/image6.png)

설치 과정에서 컴퓨터에 설치 해야 하는 사항을 파악 하 고 프로세스를 시작 합니다. 설치 해야 하는 항목에 따라 프로세스는 몇 분에서 몇 분 정도 걸릴 수 있습니다. **동의** 함을 선택 하 여 사용 조건에 동의 합니다.

## <a name="hello-webmatrix"></a>Hello, WebMatrix

설치가 완료 되 면 설치 프로세스에서 WebMatrix를 자동으로 시작할 수 있습니다. 그렇지 않으면 Windows의 **시작** 메뉴에서 **Microsoft WebMatrix**를 시작 합니다.

WebMatrix를 처음 시작 하는 경우 Microsoft 계정 Microsoft Azure에 로그인 할 수 있는 기회가 제공 됩니다. 로그인 하면 Azure를 통해 10 개의 무료 웹 앱을 받게 됩니다. 이러한 무료 웹 앱은 앱을 테스트 하는 편리한 방법을 제공 합니다. Azure 계정이 아직 없지만 MSDN 구독이 있는 경우 [msdn subscription 혜택을 활성화할](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)수 있습니다. 그렇지 않으면 몇 분만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/free/dotnet/)을 참조하세요.

이 자습서를 계속 진행 하기 위해 지금 로그인 할 필요는 없습니다. 지금 로그인 하지 않으면 나중에 로그인 할 수 있는 옵션이 표시 됩니다. 이 자습서 시리즈의 마지막 [항목](publishing.md) 에서는 Azure에 웹 사이트를 배포 하는 방법을 설명 합니다. 따라서이 항목을 완료 하려면 로그인 해야 합니다.

**이제** Microsoft 계정를 사용 하 여 로그인 하거나, 오른쪽 아래 모서리에서 아니요를 선택 합니다.

![링크를](getting-started/_static/image7.png)

시작 하려면 빈 웹 사이트를 만들고 페이지를 추가 합니다. 이 집합의 이후 자습서에서는 기본 제공 웹 사이트 템플릿 중 하나를 사용 하 여 재생 합니다.

시작 창에서 **새로 만들기**를 클릭 합니다.

![WebMatrix 시작 화면](getting-started/_static/image8.png)

템플릿은 다양 한 유형의 웹 사이트에 대해 미리 작성 된 파일 및 페이지입니다. 기본적으로 사용할 수 있는 모든 템플릿을 보려면 템플릿 갤러리 옵션을 선택 합니다.

![템플릿 갤러리 선택](getting-started/_static/image9.png)

**빠른 시작** 창의 **ASP.NET** 그룹에서 **빈 사이트** 를 선택 하 고 새 사이트의 이름을 "webpagesmovies"로 선택 합니다.

![빈 사이트 템플릿이 선택 된 WebMatrix 빠른 시작 창](getting-started/_static/image10.png)

**다음**을 클릭합니다.

Microsoft 계정에 로그인 한 경우 Azure에서 사이트를 만들 수 있는 기회가 제공 됩니다. 사이트 이름에 따라 **WebPagesMovies.azurewebsites.net** 의 기본 이름이 제안 됩니다. 그러나 느낌표는이 이름을 Windows Azure에서 사용할 수 없음을 나타냅니다. 간단히 하기 위해 **건너뛰기** 를 선택 하 여 지금 Azure에서 웹 사이트 만들기를 무시 합니다. 이 시리즈의 뒷부분에서 Azure에 사이트를 게시 합니다.

![azure 사이트 만들기](getting-started/_static/image11.png)

WebMatrix에서 사이트를 만들고 엽니다.

![WebMatrix에서 새 웹 사이트 동영상 사이트 열기](getting-started/_static/image12.png)

위쪽에는 빠른 액세스 도구 모음과 리본 메뉴가 있습니다. 왼쪽 아래에서 작업 (**사이트**, **파일**, **데이터베이스**, **보고서**) 사이를 전환 하는 작업 영역 선택 기가 표시 됩니다. 오른쪽에는 편집기 및 보고서에 대 한 내용 창이 있습니다. 아래쪽에서 메시지에 대 한 알림 표시줄을 가끔 볼 수 있습니다.

WebMatrix 및 해당 기능에 대 한 자세한 내용은이 자습서를 참조 하세요.

## <a name="creating-a-web-page"></a>웹 페이지 만들기

WebMatrix 및 ASP.NET 웹 페이지에 익숙해질 수 있도록 간단한 페이지를 만듭니다.

작업 영역 선택기에서 **파일** 작업 영역을 선택 합니다. 이 작업 영역에서는 파일 및 폴더 작업을 수행할 수 있습니다. 왼쪽 창에는 사이트의 파일 구조가 표시 됩니다. 리본은 파일 관련 작업을 표시 하도록 변경 됩니다.

![WebMatrix의 파일 작업 영역](getting-started/_static/image13.png)

리본 메뉴에서 **새로 만들기** 아래에 있는 화살표를 클릭 한 다음 **새 파일**을 클릭 합니다.

![&quot;리본에서 새 명령을 사용 하 여 &quot; 새 파일 만들기](getting-started/_static/image14.png)

WebMatrix 파일 형식 목록을 표시 합니다. **CSHTML**를 선택 하 고 **이름** 상자에 "HelloWorld"를 입력 합니다. CSHTML 페이지는 ASP.NET 웹 페이지 페이지입니다.

![HelloWorld. cshtml 라는 새 CSHTML 페이지를 만듭니다.](getting-started/_static/image15.png)

**확인**을 클릭합니다.

WebMatrix가 페이지를 만들고 편집기에서 엽니다.

![WebMatrix 편집기의 새 HelloWorld 페이지](getting-started/_static/image16.png)

여기에서 볼 수 있듯이 페이지는 위쪽에 있는 블록을 제외 하 고 다음과 같은 일반적인 HTML 태그를 포함 합니다.

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

잠시 후에 코드를 추가 하기 위한 것입니다.

페이지의 &mdash; 요소 이름, 특성, 텍스트 및 위쪽의 블록은 모두 다른 색으로 되어 있습니다. 이를 *구문 강조 표시*라고 하며 모든 것을 명확 하 게 유지할 수 있습니다. WebMatrix에서 웹 페이지를 쉽게 사용할 수 있도록 하는 기능 중 하나입니다.

`<head>`다음 예제와 같이 및 요소에 대 한 콘텐츠를 추가 `<body>` 합니다. (원하는 경우 다음 블록을 복사 하 고 기존 전체 페이지를이 코드로 바꿀 수 있습니다.)

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

빠른 실행 도구 모음 또는 **파일** 메뉴에서 **저장**을 클릭 합니다.

![WebMatrix 빠른 실행 도구 모음의 저장 단추](getting-started/_static/image17.png)

## <a name="testing-the-page"></a>페이지 테스트

**파일** 작업 영역에서 *HelloWorld. cshtml* 페이지를 마우스 오른쪽 단추로 클릭 한 다음 **브라우저에서 시작**을 클릭 합니다.

![WebMatrix 리본에서 실행 단추를 사용 하 여 페이지 실행](getting-started/_static/image18.png)

WebMatrix는 컴퓨터에서 페이지를 테스트 하는 데 사용할 수 있는 기본 제공 웹 서버 (IIS Express)를 시작 합니다. (WebMatrix에서 IIS Express 하지 않고 웹 서버를 테스트 하기 전에 웹 서버에 페이지를 게시 해야 합니다.) 페이지가 기본 브라우저에 표시 됩니다.

![&quot;&quot;브라우저에서 실행 중인 Hello World 페이지](getting-started/_static/image19.png)

WebMatrix에서 페이지를 테스트 하는 경우 브라우저의 URL은 `http://localhost:33651/HelloWorld.cshtml.` 로컬 서버를 참조 하는 이름입니다 *localhost* . 즉, 사용자 컴퓨터에 있는 웹 서버에서 페이지를 제공 하는 것입니다. 앞서 설명한 것 처럼 WebMatrix에는 페이지를 시작할 때 실행 되는 IIS Express 이라는 웹 서버 프로그램이 포함 되어 있습니다.

*Localhost* (예 *: localhost: 33651*) 다음의 번호는 컴퓨터의 *포트 번호* 를 나타냅니다. 이 특정 웹 사이트에 IIS Express 사용 하는 "채널"의 번호입니다. 포트 번호는 사이트를 만들 때 1024 ~ 65536 범위의 임의로 선택 되며, 사용자가 만드는 모든 사이트 마다 다릅니다. 사용자 고유의 사이트를 테스트 하는 경우 포트 번호는 거의 33561 보다 다른 숫자입니다. 각 웹 사이트에 대해 서로 다른 포트를 사용 하 여 통신 하 고 있는 사이트를 바로 IIS Express 수 있습니다.

나중에 사이트를 공용 웹 서버에 게시할 때 URL에 *localhost* 가 더 이상 표시 되지 않습니다. 이 시점에서 또는 페이지와 같은 일반적인 URL을 볼 수 있습니다 `http://myhostingsite/mywebsite/HelloWorld.cshtml` . 이 자습서 시리즈의 뒷부분에서 사이트를 게시 하는 방법에 대해 자세히 알아봅니다.

## <a name="adding-some-server-side-code"></a>서버 쪽 코드 추가

브라우저를 닫고 WebMatrix의 페이지로 돌아갑니다.

코드 블록에 다음 코드와 같이 줄을 추가 합니다.

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

약간 약간의 Razor 코드입니다. 현재 날짜와 시간을 가져오고 해당 값을 라는 *변수에* 배치 한다는 것을 분명 하 게 알 수 있습니다 `currentDateTime` . 다음 자습서의 Razor 구문에 대 한 자세한 내용을 참조 하세요.

페이지의 본문에서 요소 뒤에 `<p>Hello World!</p>` 다음을 추가 합니다.

[!code-html[Main](getting-started/samples/sample4.html)]

이 코드는 `currentDateTime` 위쪽의 변수에 입력 한 값을 가져와 페이지의 태그에 삽입 합니다. `@`문자는 페이지의 ASP.NET 웹 페이지 코드를 표시 합니다.

페이지를 다시 실행 합니다. WebMatrix는 페이지를 실행 하기 전에 변경 내용을 저장 합니다. 이번에는 페이지에 날짜 및 시간이 표시 됩니다.

![&quot;&quot;동적으로 생성 된 시간 표시를 사용 하 여 브라우저에서 실행 중인 Hello World 페이지](getting-started/_static/image20.png)

잠시 기다렸다가 브라우저에서 페이지를 새로 고칩니다. 날짜 및 시간 표시가 업데이트 됩니다.

브라우저에서 페이지 소스를 확인 합니다. 이 태그는 다음과 같습니다.

[!code-html[Main](getting-started/samples/sample5.html)]

위쪽에 있는 `@{ }` 블록은 표시 되지 않습니다. 또한 날짜 및 시간 표시에는의 실제 문자열 (또는 모든 항목)이 표시 됩니다. `1/18/2012 2:49:50 PM` `@currentDateTime` *.cshtml* 여기서는 페이지를 실행 했을 때 ASP.NET로 표시 된 모든 코드 (이 경우에는 거의 없음)를 처리 했음을 의미 `@` 합니다. 코드가 출력을 생성 하 고 해당 출력이 페이지에 삽입 되었습니다.

## <a name="this-is-what-aspnet-web-pages-are-about"></a>이 ASP.NET 웹 페이지에 대 한 정보입니다.

ASP.NET 웹 페이지에서 동적 웹 콘텐츠를 생성 하는 것을 읽을 때 여기에 표시 되는 내용은 다음과 같습니다. 방금 만든 페이지에는 앞서 살펴본 것과 동일한 HTML 태그가 포함 됩니다. 또한 모든 종류의 작업을 수행할 수 있는 코드를 포함할 수 있습니다. 이 예에서는 현재 날짜 및 시간을 가져오는 간단한 작업을 수행 했습니다. 앞서 살펴본 것 처럼 HTML로 코드를 섞어서 하 여 페이지에서 출력을 생성할 수 있습니다. 사용자가 브라우저에서 *cshtml* 페이지를 요청 하면 ASP.NET는 웹 서버를 계속 사용할 때 페이지를 처리 합니다. ASP.NET 코드의 출력 (있는 경우)을 HTML로 페이지에 삽입 합니다. 코드 처리가 완료 되 면 ASP.NET는 결과 페이지를 브라우저로 보냅니다. 모든 브라우저는 HTML입니다. 다이어그램은 다음과 같습니다.

![ASP.NET에서 HTML을 동적으로 생성 하는 방법의 개념적 흐름](getting-started/_static/image21.png)

개념은 간단 하지만, 코드에서 수행할 수 있는 많은 흥미로운 작업이 있으며, 페이지에 HTML 콘텐츠를 동적으로 추가할 수 있는 여러 가지 흥미로운 방법이 있습니다. 또한 HTML 페이지와 *같은 ASP.NET 페이지* 에는 브라우저 자체에서 실행 되는 코드 (JavaScript 및 jQuery 코드)가 포함 될 수 있습니다. 이 자습서 집합과 이후의 모든 항목을 탐색 합니다.

## <a name="coming-up-next"></a>다음에서 시작

이 시리즈의 다음 자습서에서는 ASP.NET 웹 페이지 프로그래밍에 대해 좀 더 살펴보겠습니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 사이트를 처음부터 새로 만듭니다](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch). WebMatrix를 사용 하는 방법에 대 한 자습서입니다 (ASP.NET 웹 페이지는 아님). 이 자습서 집합에 포함 되지 않는 WebMatrix의 일부 추가 기능에 대 한 자세한 정보를 제공 합니다.

> [!div class="step-by-step"]
> [다음](intro-to-web-pages-programming.md)
