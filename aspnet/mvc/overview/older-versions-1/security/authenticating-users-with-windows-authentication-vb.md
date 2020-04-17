---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: Windows 인증(VB)으로 사용자 인증 | 마이크로 소프트 문서
author: rick-anderson
description: MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용하는 방법에 대해 알아봅니다. 응용 프로그램의 웹 에서 Windows 인증을 사용 하는 방법을 알아봅니다...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 446dcc338f61e1f76478c1085773e7ad089c73f4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540599"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a>Windows 인증으로 사용자 인증(VB)

[로 마이크로 소프트](https://github.com/microsoft)

> MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용하는 방법에 대해 알아봅니다. 응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용하도록 설정하는 방법과 IIS를 사용하여 인증을 구성하는 방법에 대해 알아봅니다. 마지막으로 [권한 부여] 특성을 사용하여 특정 Windows 사용자 또는 그룹에 대한 컨트롤러 작업에 대한 액세스를 제한하는 방법을 알아봅니다.

이 자습서의 목표는 인터넷 정보 서비스에 내장된 보안 기능을 활용하여 MVC 응용 프로그램의 보기를 암호로 보호하는 방법을 설명하는 것입니다. 컨트롤러 작업을 특정 Windows 사용자 또는 특정 Windows 그룹의 구성원인 사용자만 호출하도록 허용하는 방법을 알아봅니다.

Windows 인증을 사용하는 것은 내부 회사 웹 사이트(인트라넷 사이트)를 구축하고 사용자가 웹 사이트에 액세스할 때 표준 Windows 사용자 이름과 암호를 사용할 수 있도록 하려는 경우에 의미가 있습니다. 바깥쪽을 향한 웹 사이트(인터넷 웹 사이트)를 빌드하는 경우 폼 인증을 대신 사용하는 것이 좋습니다.

#### <a name="enabling-windows-authentication"></a>Windows 인증 사용

새 ASP.NET MVC 응용 프로그램을 만들 때 Windows 인증은 기본적으로 활성화되지 않습니다. 양식 인증은 MVC 응용 프로그램에 대해 사용할 수 있는 기본 인증 유형입니다. MVC 응용 프로그램의 웹 구성(web.config) 파일을 수정하여 Windows 인증을 사용하도록 설정해야 합니다. &lt;다음과 같이&gt; 인증 섹션을 찾아 서폼 인증 대신 Windows를 사용하도록 수정합니다.

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

Windows 인증을 사용하도록 설정하면 웹 서버에서 사용자 인증에 대한 책임이 있습니다. 일반적으로 ASP.NET MVC 응용 프로그램을 만들고 배포할 때 사용하는 웹 서버유형에는 두 가지 유형이 있습니다.

먼저 MVC 응용 프로그램을 개발하는 동안 Visual Studio에 포함된 ASP.NET 개발 웹 서버를 사용합니다. 기본적으로 ASP.NET 개발 웹 서버는 현재 Windows 계정의 컨텍스트에서 모든 페이지를 실행합니다(Windows에 로그인하는 데 사용한 계정).

ASP.NET 개발 웹 서버는 NTLM 인증도 지원합니다. 솔루션 탐색기 창에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 속성을 선택하여 NTLM 인증을 활성화할 수 있습니다. 그런 다음 웹 탭을 선택하고 NTLM 확인란을 선택합니다(그림 1 참조).

**그림 1 – ASP.NET 개발 웹 서버에 대한 NTLM 인증 사용**

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

프로덕션 웹 응용 프로그램의 경우 IIS를 웹 서버로 사용합니다. IIS는 다음과 같은 여러 유형의 인증을 지원합니다.

- 기본 인증 - HTTP 1.0 프로토콜의 일부로 정의됩니다. 사용자 이름과 암호를 인터넷을 통해 일반 텍스트(Base64 인코딩)로 보냅니다. - 다이제스트 인증 - 인터넷을 통해 암호 자체 대신 암호 해시를 보냅니다. - 통합 윈도우 (NTLM) 인증 - 창을 사용하여 인트라넷 환경에서 사용하는 인증의 가장 좋은 유형. - 인증서 인증 - 클라이언트 측 인증서를 사용하여 인증을 활성화합니다. 인증서는 Windows 사용자 계정에 매핑됩니다.

> [!NOTE] 
> 
> 이러한 다양한 유형의 인증에 대한 자세한 [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)개요는 을 참조하십시오.

인터넷 정보 서비스 관리자를 사용하여 특정 유형의 인증을 활성화할 수 있습니다. 모든 운영 체제의 경우 모든 유형의 인증을 사용할 수 없습니다. 또한 Windows Vista에서 IIS 7.0을 사용하는 경우 인터넷 정보 서비스 관리자에 나타나기 전에 다양한 유형의 Windows 인증을 사용하도록 설정해야 합니다. **제어판, 프로그램, 프로그램 및 기능을 열고 Windows 기능을 켜거나 끄고**인터넷 정보 서비스 노드를 확장합니다(그림 2 참조).

**그림 2 – Windows IIS 기능 활성화**

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

인터넷 정보 서비스를 사용하면 다양한 유형의 인증을 사용하거나 사용하지 않도록 설정할 수 있습니다. 예를 들어 그림 3에서는 IIS 7.0을 사용할 때 익명 인증을 사용하지 않도록 설정하고 NTLM(통합 Windows) 인증을 사용하도록 설정하는 것을 보여 줍니다.

**그림 3 – 통합 윈도우 인증 사용**

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Windows 사용자 및 그룹 권한 부여

Windows 인증을 사용하도록 설정하면 Authorize &lt;&gt; 특성을 사용하여 컨트롤러 또는 컨트롤러 작업에 대한 액세스를 제어할 수 있습니다. 이 특성은 전체 MVC 컨트롤러 또는 특정 컨트롤러 작업에 적용할 수 있습니다.

예를 들어 목록 1의 홈 컨트롤러는 Index(), CompanySecrets() 및 StephenSecrets()라는 세 가지 작업을 노출합니다. 누구나 Index() 작업을 호출할 수 있습니다. 그러나 Windows 로컬 관리자 그룹의 구성원만 CompanySecrets() 작업을 호출할 수 있습니다. 마지막으로, Redmond 도메인에서 Stephen이라는 Windows 도메인 사용자만 StephenSecrets() 작업을 호출할 수 있습니다.

**목록 1 – 컨트롤러\HomeController.vb**

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> UAC(Windows 사용자 계정 제어)로 인해 Windows Vista 또는 Windows Server 2008로 작업할 때 로컬 관리자 그룹은 다른 그룹과 다르게 동작합니다. &lt;컴퓨터의&gt; UAC 설정을 수정하지 않으면 권한 부여 특성이 로컬 관리자 그룹의 구성원을 올바르게 인식하지 못합니다.

올바른 사용 권한이 없는 컨트롤러 작업을 호출하려고 할 때 정확히 발생하는 작업은 사용 가능한 인증 유형에 따라 다릅니다. 기본적으로 ASP.NET 개발 서버를 사용할 때빈 페이지만 가져옵니다. 이 페이지는 **401 승인되지 않은** HTTP 응답 상태와 함께 제공됩니다.

반면에 익명 인증을 사용하지 않도록 설정하고 기본 인증을 사용하도록 설정한 경우 보호된 페이지를 요청할 때마다 로그인 대화 상자 메시지가 계속 표시됩니다(그림 4 참조).

**그림 4 - 기본 인증 로그인 대화 상자**

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용하는 방법을 설명했습니다. 응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용하도록 설정하는 방법과 IIS를 사용하여 인증을 구성하는 방법을 배웠습니다. 마지막으로 권한 부여 &lt;&gt; 특성을 사용하여 특정 Windows 사용자 또는 그룹에 대한 컨트롤러 작업에 대한 액세스를 제한하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](authenticating-users-with-forms-authentication-vb.md)
> [다음](preventing-javascript-injection-attacks-vb.md)
