---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: 양식 인증(C#)으로 사용자 인증 | 마이크로 소프트 문서
author: rick-anderson
description: MVC 응용 프로그램의 특정 페이지를 암호로 보호하는 [권한 부여] 특성을 사용하는 방법을 알아봅니다. 웹 사이트 관리도 사용하는 방법을 배웁니다...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: f14f996c0b3a438647b5d181675457735e473354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540976"
---
# <a name="authenticating-users-with-forms-authentication-c"></a>폼 인증으로 사용자 인증(C#)

[로 마이크로 소프트](https://github.com/microsoft)

> MVC 응용 프로그램의 특정 페이지를 암호로 보호하는 [권한 부여] 특성을 사용하는 방법을 알아봅니다. 웹 사이트 관리 도구를 사용하여 사용자 및 역할을 만들고 관리하는 방법을 알아봅니다. 또한 사용자 계정 및 역할 정보가 저장되는 위치를 구성하는 방법에 대해서도 알아봅니다.

이 자습서의 목표는 폼 인증을 사용하여 ASP.NET MVC 응용 프로그램의 보기를 암호로 보호하는 방법을 설명하는 것입니다. 웹 사이트 관리 도구를 사용하여 사용자 및 역할을 만드는 방법을 알아봅니다. 또한 권한이 있는 사용자가 컨트롤러 작업을 호출하지 못하도록 하는 방법에 대해서도 알아봅니다. 마지막으로 사용자 이름과 암호가 저장되는 위치를 구성하는 방법을 알아봅니다.

#### <a name="using-the-web-site-administration-tool"></a>웹 사이트 관리 도구 사용

다른 작업을 수행하기 전에 일부 사용자와 역할을 만드는 것부터 시작해야 합니다. 새 사용자와 역할을 만드는 가장 쉬운 방법은 Visual Studio 2008 웹 사이트 관리 도구를 활용하는 것입니다. 이 도구를 실행하려면 구성을 ASP.NET 메뉴 옵션 **프로젝트.를**선택할 수 있습니다. 또는 솔루션 탐색기 창 상단에 나타나는 세계를 치는 망치의 (다소 무서운) 아이콘을 클릭하여 웹 사이트 관리 도구를 시작할 수 있습니다(그림 1 참조).

**그림 1 – 웹 사이트 관리 도구 시작**

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

웹 사이트 관리 도구 내에서 보안 탭을 선택하여 새 사용자 **Create user** 및 역할을 만듭니다. Stephen 사용자에게 원하는 암호(예: *비밀)를*제공합니다.

**그림 2 - 새 사용자 만들기**

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

먼저 역할을 사용하도록 설정하고 하나 이상의 역할을 정의하여 새 역할을 만듭니다. 역할 활성화 링크를 클릭하여 **역할을 활성화합니다.** 다음으로 **역할 만들기 또는 관리** 링크를 클릭하여 *관리자라는* 역할을 만듭니다(그림 3 참조).

**그림 3 - 새 역할 만들기**

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

마지막으로, 샐리라는 새 사용자를 만들고 사용자 만들기 링크를 클릭하고 샐리를 만들 때 관리자를 선택하여 샐리역할을 연결합니다(그림 4 참조).

**그림 4 - 역할에 사용자 추가**

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

모든 말과 완료되면, 당신은 스티븐과 샐리라는 두 개의 새로운 사용자가 있어야합니다. 관리자라는 새 역할도 있어야 합니다. 샐리는 관리자 역할의 일원이며 스티븐은 그렇지 않습니다.

#### <a name="requiring-authorization"></a>승인 필요

사용자가 작업에 [권한 부여] 특성을 추가하여 컨트롤러 작업을 호출하기 전에 사용자를 인증하도록 요구할 수 있습니다. 개별 컨트롤러 작업에 [권한 부여] 특성을 적용하거나 이 특성을 전체 컨트롤러 클래스에 적용할 수 있습니다.

예를 들어 목록 1의 컨트롤러는 CompanySecrets()라는 작업을 노출합니다. 이 작업은 [권한 부여] 특성으로 장식되므로 사용자가 인증되지 않는 한 이 작업을 호출할 수 없습니다.

**목록 1 – 컨트롤러\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

브라우저의 주소 표시줄에 URL /Home/CompanySecrets를 입력하여 CompanySecrets() 작업을 호출하고 인증된 사용자가 아닌 경우 자동으로 로그인 보기로 리디렉션됩니다(그림 5 참조).

**그림 5 – 로그인 보기**

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

로그인 보기를 사용하여 사용자 이름과 암호를 입력할 수 있습니다. 등록된 사용자가 아닌 경우 **레지스터** 링크를 클릭하여 레지스터 보기로 이동할 수 있습니다(그림 6 참조). 등록 보기를 사용하여 새 사용자 계정을 만들 수 있습니다.

**그림 6 – 레지스터 보기**

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

성공적으로 로그인하면 CompanySecrets 보기를 볼 수 있습니다(그림 7 참조). 기본적으로 브라우저 창을 닫을 때까지 계속 로그인됩니다.

**그림 7 – 회사 비밀 보기**

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>사용자 이름 또는 사용자 역할에 의해 권한 부여

[권한 부여] 특성을 사용하여 컨트롤러 작업에 대한 액세스를 특정 사용자 집합 또는 특정 사용자 역할 집합으로 제한할 수 있습니다. 예를 들어 목록 2의 수정된 홈 컨트롤러에는 StephenSecrets() 및 AdministratorSecrets()라는 두 개의 새 작업이 포함되어 있습니다.

**목록 2 – 컨트롤러\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

사용자 이름 인 Stephen만 StephenSecrets() 작업을 호출할 수 있습니다. 다른 모든 사용자는 로그인 보기로 리디렉션됩니다. Users 속성은 사용자 계정 이름의 쉼표로 분리된 목록을 허용합니다.

관리자 역할의 사용자만 AdministratorSecrets() 작업을 호출할 수 있습니다. 예를 들어 Sally는 관리자 그룹의 구성원이므로 AdministratorSecrets() 작업을 호출할 수 있습니다. 다른 모든 사용자는 로그인 보기로 리디렉션됩니다. Roles 속성은 역할 이름의 쉼표로 구분된 목록을 허용합니다.

#### <a name="configuring-authentication"></a>인증 구성

이 시점에서 사용자 계정 및 역할 정보가 저장되는 위치가 궁금할 수 있습니다. 기본적으로 정보는 MVC 응용 프로그램의 앱\_데이터 폴더에 있는 ASPNETDB.mdf라는 (RANU) SQL Express 데이터베이스에 저장됩니다. 이 데이터베이스는 멤버 자격 사용을 시작할 때 ASP.NET 프레임워크에 의해 자동으로 생성됩니다.

솔루션 탐색기 창에서 ASPNETDB.mdf 데이터베이스를 보려면 먼저 메뉴 옵션 프로젝트, 모든 파일 표시를 선택해야 합니다.

응용 프로그램을 개발할 때 기본 SQL Express 데이터베이스를 사용하는 것은 좋습니다. 그러나 프로덕션 응용 프로그램에 는 기본 ASPNETDB.mdf 데이터베이스를 사용하지 않을 수 있습니다. 이 경우 다음 두 단계를 완료하여 사용자 계정 정보가 저장되는 위치를 변경할 수 있습니다.

1. 프로덕션 데이터베이스에 응용 프로그램 서비스 데이터베이스 개체 추가 - 프로덕션 데이터베이스를 가리키도록 응용 프로그램 연결 문자열 변경

첫 번째 단계는 프로덕션 데이터베이스에 필요한 모든 데이터베이스 개체(테이블 및 저장 프로시저)를 추가하는 것입니다. 이러한 개체를 새 데이터베이스에 추가하는 가장 쉬운 방법은 ASP.NET SQL Server 설치 마법사를 활용하는 것입니다(그림 8 참조). Microsoft Visual Studio 2008 프로그램 그룹에서 Visual Studio 2008 명령 프롬프트를 열고 명령 프롬프트에서 다음 명령을 실행하여 이 도구를 시작할 수 있습니다.

아스프넷\_레그SQL

**그림 8 - ASP.NET SQL 서버 설치 마법사**

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

ASP.NET SQL Server 설치 마법사를 사용하면 네트워크에서 SQL Server 데이터베이스를 선택하고 ASP.NET 응용 프로그램 서비스에 필요한 모든 데이터베이스 개체를 설치할 수 있습니다. 데이터베이스 서버가 로컬 컴퓨터에 있을 필요는 없습니다.

> [!NOTE] 
> 
> ASP.NET SQL Server 설치 마법사를 사용하지 않으려면 다음 폴더에 응용 프로그램 서비스 데이터베이스 개체를 추가하기 위한 SQL 스크립트를 찾을 수 있습니다.
> 
> > C:\윈도우\마이크로소프트.NET 프레임 워크\v2.0.50727

필요한 데이터베이스 개체를 만든 후 MVC 응용 프로그램에서 사용하는 데이터베이스 연결을 수정해야 합니다. 프로덕션 데이터베이스를 가리키도록 웹 구성(web.config) 파일에서 ApplicationServices 연결 문자열을 수정합니다. 예를 들어, MyProductionDB라는 데이터베이스에 3 점 나열에서 수정 된 연결 (원래 ApplicationServices 연결 문자열이 주석이 없습니다).

**목록 3 – Web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>데이터베이스 사용 권한 구성

통합 보안을 사용하여 데이터베이스에 연결하는 경우 데이터베이스에 로그인할 때 올바른 Windows 사용자 계정을 추가해야 합니다. 올바른 계정은 ASP.NET 개발 서버 또는 인터넷 정보 서비스를 웹 서버로 사용하는지 여부에 따라 달라집니다. 올바른 사용자 계정은 운영 체제에 따라 다릅니다.

ASP.NET 개발 서버(Visual Studio에서 사용하는 기본 웹 서버)를 사용하는 경우 응용 프로그램이 Windows 사용자 계정의 컨텍스트 내에서 실행됩니다. 이 경우 Windows 사용자 계정을 데이터베이스 서버 로그인으로 추가해야 합니다.

또는 인터넷 정보 서비스를 사용하는 경우 ASPNET 계정 또는 NT AUTHORITY/NETWORK SERVICE 계정을 데이터베이스 서버 로그인으로 추가해야 합니다. Windows XP를 사용하는 경우 데이터베이스에 ASPNET 계정을 로그인으로 추가합니다. Windows Vista 또는 Windows Server 2008과 같은 최신 운영 체제를 사용하는 경우 NT AUTHORITY/NETWORK SERVICE 계정을 데이터베이스 로그인으로 추가합니다.

Microsoft SQL Server 관리 스튜디오를 사용하여 데이터베이스에 새 사용자 계정을 추가할 수 있습니다(그림 9 참조).

**그림 9 – 새 Microsoft SQL Server 로그인 만들기**

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

필요한 로그인을 만든 후에는 올바른 데이터베이스 역할을 가진 데이터베이스 사용자에게 로그인을 매핑해야 합니다. 로그인을 두 번 클릭하고 사용자 매핑 탭을 선택합니다. 예를 들어 사용자를 인증하려면 aspnet\_멤버 자격\_BasicAccess 데이터베이스 역할을 사용하도록 설정해야 합니다. 새 사용자를 만들려면 aspnet\_멤버 자격\_FullAccess 데이터베이스 역할을 사용하도록 설정해야 합니다(그림 10 참조).

**그림 10 – 응용 프로그램 서비스 데이터베이스 역할 추가**

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 응용 프로그램을 빌드할 때 폼 인증을 사용하는 방법을 배웠습니다. 먼저 웹 사이트 관리 도구를 활용하여 새 사용자와 역할을 만드는 방법을 배웠습니다. 다음으로 권한이 없는 사용자가 컨트롤러 작업을 호출하지 못하도록 [권한 부여] 특성을 사용하는 방법을 배웠습니다. 마지막으로 프로덕션 데이터베이스에 사용자 및 역할 정보를 저장하도록 MVC 응용 프로그램을 구성하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [다음](authenticating-users-with-windows-authentication-cs.md)
