---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Microsoft Azure 인증 | Microsoft Docs
author: Rick-Anderson
description: Windows Azure Active Directory에 대 한 Microsoft ASP.NET 도구를 사용 하면 Windows Azure 웹 사이트에 호스트 된 웹 응용 프로그램에 대 한 인증을 간단히 수행할 수 있습니다.
ms.author: riande
ms.date: 02/20/2013
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: ab75218cbe3817c14a064e9816388aebc7e431f7
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240560"
---
# <a name="windows-azure-authentication"></a>Microsoft Azure 인증

[Rick Anderson](https://twitter.com/RickAndMSFT)

> Windows Azure Active Directory에 대 한 Microsoft ASP.NET 도구를 사용 하면 [Windows Azure 웹 사이트](https://www.windowsazure.com/home/features/web-sites/)에 호스트 된 웹 응용 프로그램에 대 한 인증을 간편 하 게 수행할 수 있습니다 Microsoft Azure 인증을 사용 하 여 조직의 Office 365 사용자를 인증 하 고, 온-프레미스 Active Directory에서 동기화 된 회사 계정 또는 사용자 지정 Windows Azure Active Directory 도메인에서 만든 사용자를 인증할 수 있습니다. Windows Azure 인증을 사용 하도록 설정 하면 단일 [Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) 테 넌 트를 사용 하 여 사용자를 인증 하도록 응용 프로그램이 구성 됩니다.
>
> ASP.NET Windows Azure 인증 도구는 클라우드 서비스의 웹 역할에 대해 지원 되지 않지만 향후 릴리스에서는 수행할 계획입니다. Windows Azure 웹 역할에서 WIF ( [Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) )가 지원 됩니다.
>
> 온-프레미스 Active Directory와 Windows Azure Active Directory 테 넌 트 간의 동기화를 설정 하는 방법에 대 한 자세한 내용은 [AD FS 2.0를 사용 하 여 Single Sign-On 구현 및 관리를](https://technet.microsoft.com/library/jj205462.aspx)참조 하세요.
>
> Windows Azure Active Directory는 현재 [무료 미리 보기 서비스로](https://azure.microsoft.com/free/dotnet/)제공 됩니다.

## <a name="requirements"></a>요구 사항:

- Visual Studio 2012 또는 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)
- [Visual Studio 2012 용 웹 도구 확장](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409) 또는 [Visual Studio Express 2012 용 웹 도구 확장](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)
- [Windows Azure Active Directory Microsoft ASP.NET tools – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306) 또는 [Microsoft ASP.NET tools for windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a>Visual Studio 2012을 사용 하 여 ASP.NET 웹 응용 프로그램 만들기

Visual Studio 2012을 사용 하 여 모든 웹 응용 프로그램을 만들 수 있습니다 .이 자습서에서는 ASP.NET MVC 인트라넷 템플릿을 사용 합니다.

1. 새 ASP.NET MVC 4 인트라넷 응용 프로그램을 만들고 모든 기본값을 적용 합니다. ( **Tra** net의 여야 하 고 **ter** net 프로젝트가 아닌).
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a>Window Azure 인증 사용 (개념의 전역 관리자 인 경우)

기존 Office 365 계정을 통해 기존 Windows Azure Active Directory 테 넌 트가 없는 경우 [새 windows Azure Active Directory 계정](https://g.microsoftonline.com/0AX00en/5)에 등록 하 여 새 테 넌 트를 만들 수 있습니다.

1. 프로젝트 메뉴에서 **Windows Azure 인증 사용**을 선택 합니다.

   ![](windows-azure-authentication/_static/image2.png)

2. Windows Azure Active Directory 테 넌 트의 도메인 (예: contoso.onmicrosoft.com)을 입력 하 고 **사용**을 클릭 합니다.

![](windows-azure-authentication/_static/image3.png)

3. 웹 인증 대화 상자에서 Windows Azure Active Directory 테 넌 트의 관리자로 로그인 합니다.

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a>개념의 비관리자가 Windows Azure를 사용 하도록 설정

Windows Azure Active Directory 테 넌 트에 대 한 전역 관리자 권한이 없는 경우 응용 프로그램을 프로 비전 하는 확인란의 선택을 취소할 수 있습니다.

![](windows-azure-authentication/_static/image6.png)

이 대화 상자에는 Azure Active Directory 개념를 사용 하 여 응용 프로그램을 프로 비전 하는 데 필요한 **도메인**, **응용 프로그램 보안 주체 ID** 및 **회신 URL** 이 표시 됩니다. 응용 프로그램을 프로 비전 하는 데 충분 한 권한이 있는 사용자에 게이 정보를 제공 해야 합니다. Cmdlet을 사용 하 여 서비스 주체를 수동으로 만드는 방법에 대 한 자세한 내용은[Windows Azure Active Directory-ASP.NET 응용 프로그램을 사용 하 여 Single Sign-On를 구현 하는 방법](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) 을 참조 하세요.
응용 프로그램을 성공적으로 프로 비전 한 후에는 **계속을 클릭 하 여 선택한 설정으로 web.config를 업데이트할**수 있습니다. 프로 비전이 발생 하기를 기다리는 동안 응용 프로그램을 계속 개발 하려는 경우 **닫기를 클릭 하 여 프로젝트 파일의 설정을 기억할**수 있습니다. 다음에 Windows Azure 인증 사용을 호출 하 고 프로 비전 확인란의 선택을 취소 하면 동일한 설정이 표시 되 고 **계속**을 클릭 한 다음 **web.config에서 이러한 설정 적용 **을 클릭 합니다.

1. 응용 프로그램을 Windows Azure 인증에 대해 구성 하 고 Windows Azure Active Directory로 프로 비전 하는 동안 기다립니다.
2. 응용 프로그램에 대해 Windows Azure 인증을 사용 하도록 설정한 후 **닫기** 를 클릭 합니다.

    ![](windows-azure-authentication/_static/image7.png)
3. F5 키를 눌러 응용 프로그램을 실행 합니다. 로그인 페이지로 자동으로 리디렉션됩니다. 디렉터리 개념 사용자 자격 증명을 사용 하 여 응용 프로그램에 로그인 합니다.

    ![](windows-azure-authentication/_static/image1.jpg)
4. 응용 프로그램에서 현재 자체 서명 된 테스트 인증서를 사용 하 고 있기 때문에 신뢰할 수 있는 인증 기관에서 인증서를 발급 하지 않았기 때문에 브라우저에서 경고를 받게 됩니다.

    이 경고는 **이 웹 사이트를 계속 탐색을** 클릭 하 여 로컬 개발 중에 무시 해도 됩니다.

    ![](windows-azure-authentication/_static/image8.png)
5. 이제 Windows Azure 인증을 사용 하 여 응용 프로그램에 성공적으로 로그인 했습니다.

    ![](windows-azure-authentication/_static/image2.jpg)

Windows Azure 인증을 사용 하도록 설정 하면 응용 프로그램이 다음과 같이 변경 됩니다.

- [Csrf](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))(사이트 간 요청 위조) 클래스 ( *앱 \_ Start\AntiXsrfConfig.cs* )가 프로젝트에 추가 됩니다.
- NuGet 패키지는 `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` 프로젝트에 추가 됩니다.
- 응용 프로그램의 windows Identity Foundation 설정은 Windows Azure Active Directory 테 넌 트의 보안 토큰을 허용 하도록 구성 됩니다. *Web.config* 파일의 변경 내용에 대 한 확장 된 보기를 보려면 아래 이미지를 클릭 하세요.

     ![](windows-azure-authentication/_static/image9.png)
- Windows Azure Active Directory 테 넌 트의 응용 프로그램에 대 한 서비스 주체가 프로 비전 됩니다.
- HTTPS를 사용할 수 있습니다.

## <a name="deploy-the-application-to-windows-azure"></a>Windows Azure에 응용 프로그램 배포

전체 지침은 [ASP.NET 웹 응용 프로그램을 Windows Azure 웹 사이트에 배포](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)를 참조 하세요.

Microsoft Azure 인증을 사용 하 여 응용 프로그램을 Azure 웹 사이트에 게시 하려면 다음을 수행 합니다.

1. 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 게시를 선택 합니다 **.**

    ![](windows-azure-authentication/_static/image3.jpg)
2. 웹 게시 대화 상자에서 Azure 웹 사이트에 대 한 게시 프로필을 다운로드 하 고 가져옵니다.

    ![](windows-azure-authentication/_static/image4.jpg)
3. **연결** 탭에는 **대상 url** (응용 프로그램의 공개 url)이 표시 됩니다. 연결 **유효성 검사** 를 클릭 하 여 연결을 테스트 합니다.

    ![](windows-azure-authentication/_static/image5.jpg)
4. 이 Azure 웹 사이트에 게시 한 경우 이전에 **대상에서 추가 파일 제거** 설정을 선택 하 여 응용 프로그램이 완전히 게시 되도록 하는 것이 좋습니다. **Windows Azure 인증 사용** 확인란이 선택 되어 있는지 확인 합니다.

    ![](windows-azure-authentication/_static/image10.png)
5. 선택 사항: **미리** 보기 탭에서 **미리 보기 시작** 을 클릭 하 여 배포 된 파일을 확인 합니다.

    ![](windows-azure-authentication/_static/image6.jpg)
6. **게시를 클릭 합니다.**

    대상 호스트에 대해 Windows Azure 인증을 사용 하도록 설정 하 라는 메시지가 표시 됩니다. 계속 하려면 **사용** 을 클릭 합니다.

    ![](windows-azure-authentication/_static/image11.png)
7. Windows Azure Active Directory 테 넌 트에 대 한 관리자 자격 증명을 입력 합니다.

    ![](windows-azure-authentication/_static/image7.jpg)
8. 응용 프로그램을 성공적으로 게시 하면 게시 된 웹 사이트에 브라우저가 열립니다.

    > [!NOTE]
    > 대상 호스트에 대해 Windows Azure 인증을 사용 하도록 설정한 후 응용 프로그램이 Windows Azure Active Directory와 완전히 프로 비전 되는 데 최대 5 분 정도 걸릴 수 있습니다 (일반적으로 더 작아야 함). ACS50001 오류를 수신 하는 경우 응용 프로그램을 처음 실행할 때 이름 ' [영역] '을 사용 하는 신뢰 당사자를 찾을 수 없습니다. 몇 분 정도 기다린 후 응용 프로그램을 다시 실행 해 보십시오.
9. 메시지가 표시 되 면 디렉터리에서 사용자로 로그인 합니다.

    ![](windows-azure-authentication/_static/image8.jpg)
10. 이제 Microsoft Azure 인증을 사용 하 여 Azure 호스팅된 응용 프로그램에 성공적으로 로그인 했습니다.

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a>알려진 문제

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a>Windows Azure 인증을 사용 하는 경우 역할 기반 권한 부여가 실패 함

현재는 역할 기반 권한 부여를 수행할 수 있도록 Windows Azure 인증에서 필요한 역할 클레임을 제공 하지 않습니다. 인증 된 사용자의 역할은 Windows Azure Active Directory에서 수동으로 검색 해야 합니다.

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a>Windows Azure 인증을 사용 하 여 응용 프로그램을 검색 하면 "ACS20016가 로그인 한 사용자의 도메인 (live.com)이이 STS의 허용 된 도메인과 일치 하지 않습니다." 오류가 발생 합니다.

Microsoft 계정 (예: hotmail.com, live.com, outlook.com)에 이미 로그인 한 상태에서 Windows Azure 인증을 사용 하도록 설정 된 응용 프로그램에 액세스 하려고 하면 Windows Azure Active Directory에서 Microsoft 계정의 도메인이 인식 되지 않기 때문에 400 오류 메시지가 표시 될 수 있습니다. 응용 프로그램에 로그인 하려면 먼저 Microsoft 계정에서 로그 아웃 합니다.

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a>Microsoft Azure 인증을 사용 하도록 설정 된 응용 프로그램에 로그인 하 고 없음 이외의 X509CertificateValidationMode는 accounts.accesscontrol.windows.net 인증서에 대 한 인증서 유효성 검사 오류가 발생 합니다.

인증서 유효성 검사는 필요 하지 않으며 사용 하지 않도록 설정 해야 합니다. WSFederationAuthenticationModule가 발급자 인증서의 지문을 확인 합니다.

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a>Windows Azure 인증을 사용 하도록 설정 하는 경우 웹 인증 대화 상자에 "ACS20016: 로그인 한 사용자의 도메인 (contoso.onmicrosoft.com)이이 STS의 허용 된 도메인과 일치 하지 않습니다." 라는 오류가 표시 됩니다.

이전에 동일한 Visual Studio 프로세스 내에서 다른 Windows Azure Active Directory 계정을 사용 하 여 로그인 한 경우이 오류가 표시 될 수 있습니다. 지정 된 계정에서 로그 아웃 하거나 Visual Studio를 다시 시작 합니다. 이전에 로그인 하 고 "로그인 유지" 옵션을 선택한 경우 브라우저 쿠키를 지워야 할 수 있습니다.

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a>ACS20012: 요청이 유효한 WS-FEDERATION 프로토콜 메시지가 아닙니다.

이 문제는 Azure 서비스 중 하나에 다른 Microsoft ID를 사용 하 여 이미 로그인 한 경우에 발생할 수 있습니다. IE의 InPrivate 또는 Chrome에서 Incognito와 같은 개인 브라우저 창을 사용 하거나 모든 쿠키를 지웁니다.

## <a name="additional-resources"></a>추가 리소스

- [Microsoft ASP.NET Tools For Windows Azure Active Directory – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci
- [Windows Azure 기능: Id](https://docs.microsoft.com/azure/active-directory/)
- [TechNet: Windows Azure Active Directory](https://technet.microsoft.com/library/hh967619.aspx)
- [Windows Azure Active Directory: 조직을 위한 앱 개발](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [Windows Azure Active Directory: 여러 조직을 위한 앱 개발](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [Windows Azure Active Directory를 사용 하 여 Single Sign-On를 구현 하는 방법](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- [Windows Azure Active Directory에서 Single sign-on: 심층](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) 살펴보기 – Vittorio Bertocci
- [AD FS 2.0를 사용 하 여 Single Sign-On 구현 및 관리](https://technet.microsoft.com/library/jj205462.aspx)
