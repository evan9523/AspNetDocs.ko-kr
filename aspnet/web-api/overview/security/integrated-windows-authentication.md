---
uid: web-api/overview/security/integrated-windows-authentication
title: Windows 통합 인증 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 Windows 통합 인증을 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: c5fe57c4a20e28fa434659a75484e3a4c37195f8
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424781"
---
# <a name="integrated-windows-authentication"></a>Windows 통합 인증

[Mike Wasson](https://github.com/MikeWasson)

Windows 통합 인증을 사용 하면 사용자가 Kerberos 또는 NTLM을 사용 하 여 Windows 자격 증명으로 로그인 할 수 있습니다. 클라이언트는 인증 헤더에 자격 증명을 보냅니다. Windows 인증은 인트라넷 환경에 가장 적합합니다. 자세한 내용은 [Windows 인증](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)을 참조하세요.

| 장점 | 단점 |
| --- | --- |
| IIS에 기본 제공 됩니다. | 인터넷 응용 프로그램에는 권장 되지 않습니다. | 
| 는 요청에서 사용자 자격 증명을 보내지 않습니다. | 클라이언트에서 Kerberos 또는 NTLM 지원이 필요 합니다. |
| 클라이언트 컴퓨터가 도메인에 속해 있는 경우 (예: 인트라넷 응용 프로그램) 사용자가 자격 증명을 입력할 필요가 없습니다. | 클라이언트는 Active Directory 도메인에 있어야 합니다. |

> [!NOTE]
> 응용 프로그램이 Azure에서 호스트 되 고 온-프레미스 Active Directory 도메인을 사용 하는 경우 온-프레미스 AD를 Azure Active Directory와 페더레이션 하는 것이 좋습니다. 이렇게 하면 사용자가 온-프레미스 자격 증명을 사용 하 여 로그인 할 수 있지만 인증은 Azure AD에서 수행 됩니다. 자세한 내용은 [Azure 인증](../../../visual-studio/overview/2012/windows-azure-authentication.md)을 참조 하세요.

Windows 통합 인증을 사용 하는 응용 프로그램을 만들려면 MVC 4 프로젝트 마법사에서 "인트라넷 응용 프로그램" 템플릿을 선택 합니다. 이 프로젝트 템플릿은 Web.config 파일에 다음 설정을 저장 합니다.

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

클라이언트 쪽에서 Windows 통합 인증은 대부분의 주요 브라우저를 포함 하는 [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) 인증 체계를 지 원하는 모든 브라우저에서 작동 합니다. .NET 클라이언트 응용 프로그램의 경우 **Httpclient** 클래스는 Windows 인증을 지원 합니다.

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Windows 인증은 CSRF (교차 사이트 요청 위조) 공격에 취약 합니다. [CSRF (교차 사이트 요청 위조) 공격 방지를](preventing-cross-site-request-forgery-csrf-attacks.md)참조 하세요.
