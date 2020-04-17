---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET 웹 페이지 (면도기) 자주 묻는 질문 | 마이크로 소프트 문서
author: Rick-Anderson
description: 이 문서에서는 ASP.NET 웹 페이지(Razor) 및 WebMatrix에 대해 자주 묻는 몇 가지 질문을 나열합니다. 웹 페이지 (R) ASP.NET 튜토리얼에 사용되는 소프트웨어 버전
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: a312d1327bc88e721bf7fc7459e420e3f582c88d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543706"
---
# <a name="aspnet-web-pages-razor-faq"></a>ASP.NET 웹 페이지(Razor) FAQ

[Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > 웹매트릭스는 더 이상 ASP.NET 웹 페이지의 통합 개발 환경으로 권장되지 않습니다. [비주얼 스튜디오](xref:web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) 또는 비주얼 [스튜디오 코드를](https://code.visualstudio.com/)사용합니다.
>
> 이 문서에서는 ASP.NET 웹 페이지(Razor) 및 WebMatrix에 대해 자주 묻는 몇 가지 질문을 나열합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>튜토리얼에 사용되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (면도기) 3
> - Visual Studio 2013
> - 웹 매트릭스 3
>   
> 
> 이 자습서에서는 웹 페이지 2, WebMatrix 2 및 Visual Studio 2012에서 ASP.NET 작동합니다.

- [ASP.NET 웹 페이지, ASP.NET 웹 양식 및 ASP.NET MVC의 차이점은 무엇입니까?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [웹 페이지를 사용하여 작업하려면 WebMatrix가 필요합니까?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [웹 페이지 페이지에서 ASP.NET 웹 양식 컨트롤을 사용할 수 있습니까?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [WebMatrix를 사용하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [로그인을 지원하기 위해 WebSecurity 도우미를 사용해야 합니까?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [ASP.NET 웹 페이지는 HTML5를 지원합니까?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [웹 페이지에서 자바 스크립트 및 jQuery를 사용할 수 있습니까?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [추가 리소스](#AdditionalResources)

오류 및 기타 문제에 대한 질문은 [ASP.NET 웹 페이지(Razor) 문제 해결 가이드를](https://go.microsoft.com/fwlink/?LinkId=253001)참조하십시오.

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>ASP.NET 웹 페이지, ASP.NET 웹 양식 및 ASP.NET MVC의 차이점은 무엇입니까?

세 가지 모두 동적 웹 응용 프로그램을 만들기 위한 ASP.NET 기술입니다.

- ASP.NET 웹 페이지는 HTML 페이지에 동적(서버 측) 코드 및 데이터베이스 액세스를 추가하는 데 중점을 두고 있으며 간단하고 가벼운 구문을 제공합니다.
- ASP.NET 웹 폼은 페이지 개체 모델과 기존 창 유형 컨트롤(단추, 목록 등)을 기반으로 합니다. Web Forms는 클라이언트 기반(Windows 양식) 개발에 익숙한 이벤트 기반 모델을 사용합니다.
- ASP.NET MVC는 ASP.NET 대한 모델 뷰 컨트롤러 패턴을 구현합니다. "문제의 분리"(처리, 데이터 및 UI 계층)에 중점을 둡니다.

세 가지 프레임워크는 모두 완벽하게 지원되며 ASP.NET 팀에서 계속 개발됩니다. 일반적으로 사용할 프레임워크의 선택은 ASP.NET 대한 배경 과 경험에 따라 달라집니다.

특히 ASP.NET 웹 페이지는 HTML을 이미 알고 있는 사람들이 페이지에 서버 처리를 쉽게 추가할 수 있도록 설계되었습니다. 그것은 학생, 취미, 프로그래밍에 익숙하지 않은 일반 사람들에게 좋은 선택입니다. 또한 non-ASP.NET 웹 기술에 대한 경험이있는 개발자에게 좋은 선택이 될 수 있습니다.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>웹 페이지를 사용하여 작업하려면 WebMatrix가 필요합니까?

아니요. 웹매트릭스는 더 이상 ASP.NET 웹 페이지의 통합 개발 환경으로 권장되지 않습니다. [비주얼 스튜디오](program-asp-net-web-pages-in-visual-studio.md) 또는 비주얼 [스튜디오 코드를](https://code.visualstudio.com/)사용합니다.

Visual Studio 또는 Visual Studio 코드를 사용하지 않으려면 Microsoft 웹 플랫폼 설치 [관리자를](https://www.microsoft.com/web/downloads/platform.aspx)사용하여 구성 요소 제품을 개별적으로 설치할 수 있습니다. 다음 제품이 필요합니다.

- Microsoft .NET Framework 4.5도 필요합니다
- ASP.NET MVC 5 (ASP.NET 웹 페이지 프레임 워크도 설치)
- IIS 익스프레스 (웹 서버)
- 마이크로소프트 SQL 서버 컴팩트 4.0 (데이터베이스)

텍스트 편집기를 사용하여 *.cshtml(또는* *.vbhtml)* 페이지를 편집할 수 있습니다.

도구 없이 SQL Server 컴팩트*데이터베이스(.sdf* 파일)를 관리하는 것은 조금 더 어렵습니다. Visual Studio에는 *.sdf* 데이터베이스를 관리하기 위한 도구가 포함되어 있습니다. 코드에서 SQL 명령을 실행하여 많은 SQL Server 관리 작업을 수행할 수도 있습니다.

IDE(통합 개발 환경)를 사용하지 않고 *.cshtml* 페이지를 테스트하려면 라이브 서버에 배포할 수 있습니다. [(WebMatrix를 사용하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)

### <a name="running-iis-express-without-using-an-ide"></a>IDE를 사용하지 않고 IIS 익스프레스 실행

컴퓨터에 IIS Express를 웹 서버로 설치하는 경우 이 것을 사용하여 페이지를 테스트할 수 있습니다. 명령줄에서 IIS Express를 실행하고 특정 포트 번호와 연결할 수 있습니다. 그런 다음 브라우저에서 *.cshtml* 파일을 요청할 때 해당 포트를 지정합니다.

Windows에서 관리자 권한이 있는 명령 프롬프트를 열고 *C:\프로그램 파일\IIS Express로 변경합니다.* (64비트 시스템의 경우 *C:\프로그램 파일(x86)\IIS Express 폴더를 사용합니다.* 그런 다음 사이트에 대한 실제 경로를 사용하여 다음 명령을 입력합니다.

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

다른 프로세스에서 아직 예약하지 않은 포트 번호를 사용할 수 있습니다. (1024를 초과하는 포트 번호는 일반적으로 무료입니다.) 값의 `path` 경우 *.cshtml* 파일이 있는 웹 사이트 폴더의 경로를 사용합니다.

이 명령을 실행하여 IIS Express가 페이지를 서비스하도록 설정한 후 브라우저를 열고 *.cshtml* 파일로 검색할 수 있습니다. 다음과 같은 URL을 사용합니다.

`http://localhost:35896/default.cshtml`

IIS Express 명령줄 옵션에 `iisexpress.exe /?` 대한 도움말을 보려면 명령줄을 입력합니다.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>웹 페이지 페이지에서 ASP.NET 웹 양식 컨트롤을 사용할 수 있습니까?

아니요. 웹 양식은 [확인란](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) 컨트롤, [유효성 검사 컨트롤](https://msdn.microsoft.com/library/bwd43d0x)및 [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) 컨트롤과 같은 컨트롤은 웹 양식 페이지(.aspx 파일)에서만 작동합니다.*.aspx* 이러한 컨트롤에는 Web Forms 페이지 프레임워크가 필요합니다.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>WebMatrix를 사용하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?

예. 일반적으로 FTP를 사용하여 웹 사이트 파일을 서버에 수동으로 복사할 수 있습니다. 수동 복사본을 수행하는 경우 SQL Server Compact(데이터베이스)를 지원하는 파일도 복사해야 합니다. 자세한 내용은 [도구 없이 웹 페이지 배포 응용 프로그램](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)블로그 항목을 참조합니다.

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>로그인을 지원하기 위해 WebSecurity 도우미를 사용해야 합니까?

아니요. ASP.NET `SimpleMembership` 웹 페이지의 일부인 공급자는 하나의 옵션입니다. ASP.NET 일부인 보안 공급자(웹 양식에서 작업하는 데 사용할 수 있음)도 사용할 수 있습니다. 예를 들어 웹 양식에서와 마찬가지로 ASP.NET 웹 페이지에서 양식 인증을 사용할 수 있습니다. 양식 인증을 사용하는 방법의 한 예는 [C#.NET을 사용하여 ASP.NET 응용 프로그램에서 양식 기반 인증을 구현하는 방법](https://support.microsoft.com/kb/301240)Microsoft 지원 문서를 참조하십시오. 간단한 예제를 다운로드하려면 [ASP.NET 버전의 &amp; "로그인 암호](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm).

Windows 인증을 사용하는 방법에 대한 자세한 내용은 [ASP.NET 웹 페이지에서 Windows 인증 사용](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)블로그 게시물을 참조하십시오.

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>ASP.NET 웹 페이지는 HTML5를 지원합니까?

예. ASP.NET 웹*페이지(.cshtml* 또는 *.vbhtml* 페이지)로 만드는 페이지는 기본적으로 페이지가 렌더링되기 전에 서버에서 실행되는 코드를 포함하는 HTML 페이지입니다. 사용자의 브라우저가 HTML5를 지원하는 한 *.cshtml* 또는 *.vbhtml* 페이지에서 HTML5 요소를 사용할 수 있습니다.

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>웹 페이지에서 자바 스크립트 및 jQuery를 사용할 수 있습니까?

그렇습니다. ASP.NET 웹*페이지(.cshtml* 또는 *.vbhtml* 페이지)로 만드는 페이지는 서버 코드가 있는 HTML 페이지일 뿐입니다. 따라서 자바 스크립트 또는 jQuery를 사용하여 일반 HTML 페이지에서 할 수있는 모든 작업을 *.cshtml* 또는 *.vbhtml* 페이지에서 수행 할 수 있습니다.

WebMatrix의 **시작 사이트** 템플릿에는 여러 jQuery 라이브러리가 포함되어 있습니다. 해당 템플릿을 사용하여 사이트를 만드는 경우 *스크립트* 폴더에는 jQuery 코어*라이브러리(jquery-1.6.2.js)와* jQuery 유효성 검사용*라이브러리(jquery.validate.js*등)가 포함됩니다.

다음은 ASP.NET 웹 페이지에서 jQuery를 사용하는 방법을 보여 주는 몇 가지 블로그 게시물입니다.

- 레이첼 Appel에 의해 [웹 매트릭스를 사용하여 웹 페이지를 ASP.NET jQuery 선함 추가](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)
- [5 분: 웹 매트릭스 + jQuery UI + json + jQuery 템플릿](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) 조나스 에릭슨
- [마이크 브린드에 의해 웹 매트릭스 및 j쿼리 양식](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지(Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)

ASP.NET 웹 사이트의 [웹 매트릭스 및 ASP.NET 웹 페이지 포럼](https://forums.asp.net/1224.aspx/1?WebMatrix)
