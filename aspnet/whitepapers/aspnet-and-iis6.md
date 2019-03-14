---
uid: whitepapers/aspnet-and-iis6
title: Iis 6.0에서 ASP.NET 1.1 실행 | Microsoft Docs
author: rick-anderson
description: Windows Server 2003에서 IIS 6.0 및 ASP.NET 1.1 모두를 포함 하는 동안 이러한 구성 요소는 기본적으로 비활성화 됩니다. 이 백서에서는 IIS 6.0을 사용 하도록 설정 하는 중...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 38cd0abc1e9133b9b86cff6dd2759ce98ac5a115
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036900"
---
<a name="running-aspnet-11-with-iis-60"></a>IIS 6.0에서 ASP.NET 1.1 실행
====================
> Windows Server 2003에서 IIS 6.0 및 ASP.NET 1.1 모두를 포함 하는 동안 이러한 구성 요소는 기본적으로 비활성화 됩니다. 이 백서는 IIS 6.0 및 ASP.NET 1.1을 사용 하도록 설정 하는 방법에 설명 하 고 IIS 및 ASP.NET에서 최적의 성능을 얻기 위해 다양 한 구성 설정을 권장 합니다.
> 
> IIS 6.0 및 ASP.NET 1.1에 적용 됩니다.


또한 인터넷 정보 서버 (IIS) 버전 6.0의 최신 버전을 포함 하는 Windows Server 2003을 사용 하 여 ASP.NET 1.1 제공 됩니다. IIS 6.0 및 ASP.NET 1.1 원활 하 게 통합 하도록 설계 되어 새 IIS 6.0 작업자 프로세스 모델 이제 기본적으로 ASP.NET을

## <a name="aspnet-11-is-not-installed-by-default"></a>ASP.NET 1.1은 기본적으로 설치 되지

Microsoft의 서버 운영 체제의 이전 버전과 달리 인터넷 정보 서버 (IIS) 기본적으로 사용 되지 않습니다. ASP.NET 1.1 것도 아닙니다. 두 가지 방법으로 IIS를 사용 하도록 설정:

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a>옵션 #1-IIS 서버 구성 마법사 사용

Windows Server 2003을 새 ' 서버 구성 마법사 '를 제대로 원하는 모드에서 서버를 구성 하기 위해 제공 됩니다.

마법사를 시작 하려면-관리자 권한으로 로그인 해야 하는 마법사를 실행 하려면 참고로 이동: 시작 | 프로그램 | 관리 도구 및 선택 ' 구성 서버 '입니다.

한 번 선택한 ' 서버 구성 마법사 ' 화면이 표시 됩니다.

![](aspnet-and-iis6/_static/image1.jpg)

클릭 ' 다음 &gt;'.

![](aspnet-and-iis6/_static/image2.jpg)

클릭 ' 다음 &gt;'

![](aspnet-and-iis6/_static/image3.jpg)

이 화면에서 선택 해야 합니다 ' 구성 옵션으로 응용 프로그램 서버 (IIS, ASP.NET).

클릭 ' 다음 &gt;'.

![](aspnet-and-iis6/_static/image4.jpg)

응용 프로그램 서버로 서버를 구성 하려면을 선택한 후 추가 기능을 설치할지 확인이 화면이 표시 됩니다. 두 옵션 모두 기본적으로 선택 됩니다. ASP.NET을 자동으로 사용 하려면 선택 ' ASP를 사용 하도록 설정 합니다. NET'.

클릭 ' 다음 &gt;'.

![](aspnet-and-iis6/_static/image5.jpg)

이 화면 설치 옵션은 표시 됩니다.

클릭 ' 다음 &gt;'.

![](aspnet-and-iis6/_static/image6.jpg)

선택한 옵션을 설치 하는 동안에이 화면이 나타납니다. 일반적으로 다른 대화 상자 표시 서비스를 설치 하는 경우 수 또한 묻는 Windows 2003 Server 설치 CD의 위치입니다.

클릭 ' 다음 &gt;' 완료 되 면 합니다.

![](aspnet-and-iis6/_static/image7.jpg)

[마침] 클릭-Windows Server 2003 이제 IIS 6.0 및 ASP.NET 1.1을 지원 하도록 구성 됩니다.

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a>IIS, ASP.NET 및 IIS를 수동으로 구성 하는 #2-옵션을 사용 하도록 설정

' 구성 서버 마법사 '를 사용 하 고 싶지 않은 경우 제어판에서 IIS 6.0 및 ASP.NET 1.1 '프로그램 추가 / 제거'를 사용 하 여을 설치할 필요에 따라 있습니다.

먼저 제어판을 엽니다.

![](aspnet-and-iis6/_static/image8.jpg)

그런 다음 ' 추가/제거 Windows 구성 요소에 ' ' Windows 구성 요소 마법사 '를 엽니다.

![](aspnet-and-iis6/_static/image9.jpg)

강조 표시 하 고 ' 응용 프로그램 서버 '를 확인 하는 'Details'?'를 클릭 한 다음 단추:

![](aspnet-and-iis6/_static/image10.jpg)

ASP.NET을 설치 하려면 ' ASP 합니다. NET'.

Windows 구성 요소 마법사 반환 하려면 ' 확인'을 클릭 합니다. 클릭 ' 다음 &gt;' 설치를 시작 하려면 Windows 구성 요소 마법사에서:

![](aspnet-and-iis6/_static/image11.jpg)

일반적으로 다른 대화 상자 표시 서비스를 설치 하는 경우 수 또한 묻는 Windows 2003 Server 설치 CD의 위치입니다.

설치가 완료 되 면 Windows 구성 요소 마법사의 마지막 화면을 표시 됩니다.

![](aspnet-and-iis6/_static/image12.jpg)

IIS 6.0 및 ASP.NET 1.1은 이제 구성 및 사용할 수 있습니다.

## <a name="recommended-settings"></a>권장된 설정

IIS 6.0과 ASP.NET 1.1을 실행 하는 경우에 ASP.NET에서 최적의 성능을 얻기 위해 권장 되는 여러 구성 설정이:

- 작업자 프로세스 메모리 한도 구성
- 작업자 프로세스 재활용 구성

### <a name="configuring-worker-process-memory-limits"></a>작업자 프로세스 메모리 한도 구성

기본적으로 IIS 6.0의 IIS에서 사용할 수 있는 메모리 양에 제한을 설정 하지 않습니다. ASP 합니다. NET의 캐시 기능은 캐시 메모리에서 사전에 사용 되지 않는 항목을 제거할 수 있도록 메모리의 제한 사항 의존 합니다.

IIS 6.0의 기능을 재활용 하는 메모리를 구성 하는 것이 좋습니다. 이 오픈 인터넷 정보 서비스 관리자를 구성 하려면 (시작 | 프로그램 | 관리 도구 | 인터넷 정보 서비스)입니다. 열기 되 면 ' 응용 프로그램 풀 ' 폴더를 확장 합니다.

각 응용 프로그램 풀:

![](aspnet-and-iis6/_static/image13.jpg)

1. 예를 들어 응용 프로그램 풀에서 마우스 오른쪽 단추로 'DefaultAppPool' 및 '속성'을 선택 합니다.

![](aspnet-and-iis6/_static/image14.jpg)

2. 그런 다음 중 하나를 클릭 하 여 메모리 재활용을 사용 하도록 설정 ' 사용 된 최대 메모리 (메가바이트 단위). '. 값은 서버의 실제 가상이 아닌 메모리의 양보다 많을 수 없습니다는 유사한 추정치 512MB 이상의 실제 메모리 선택 310 사용 하 여 서버에 대 한 예: 실제 메모리의 60%입니다. 또한 최대 초과 하지 않는지 800MB 2GB 주소 공간을 사용 하는 경우 것이 좋습니다. 서버의 메모리 주소 공간 3 GB 인 경우 작업자 프로세스에 대 한 최대 메모리 제한을 1, 800 MB으로 될 수 있습니다.

![](aspnet-and-iis6/_static/image15.jpg)

'적용' 및 'OK' 속성 대화 상자를 종료 하려면 클릭 합니다. 모든 사용 가능한 응용 프로그램 풀에 대해이 단계를 반복 합니다.

### <a name="configuring-worker-recycling"></a>재활용 작업자 구성

기본적으로 IIS 6.0은 29 시간 마다 작업자 프로세스를 재활용 하도록 구성 됩니다. ASP.NET을 실행 중인 응용 프로그램에 대 한 다소 공격적인 이며 자동 작업자 프로세스 재활용은 사용 하지 않도록 하는 것이 좋습니다.

자동 작업자 프로세스 재활용을 사용 하지 않으려면 인터넷 정보 서비스 관리자를 열려면 먼저 (시작 | 프로그램 | 관리 도구 | 인터넷 정보 서비스)입니다. 열기 되 면 ' 응용 프로그램 풀 ' 폴더를 확장 합니다.

![](aspnet-and-iis6/_static/image16.jpg)

각 응용 프로그램 풀:

1. 예를 들어 응용 프로그램 풀에서 마우스 오른쪽 단추로 'DefaultAppPool' 및 '속성'을 선택 합니다.

![](aspnet-and-iis6/_static/image17.jpg)

2. 선택 취소 ' 분 단위로 작업자 프로세스 재생:':

![](aspnet-and-iis6/_static/image18.jpg)

'적용' 및 'OK' 속성 대화 상자를 종료 하려면 클릭 합니다. 모든 사용 가능한 응용 프로그램 풀에 대해이 단계를 반복 합니다.

## <a name="granting-write-access-to-the-file-system"></a>파일 시스템에 대 한 쓰기 액세스를 부여합니다.

응용 프로그램에 파일 시스템에 대 한 쓰기 권한이 필요 하 고 NTFS를 사용 하는 경우는 목록 ACL (액세스 제어) 폴더 또는 파일의 ASP.NET 액세스 권한을 부여 하려면 수정 해야 합니다.

예를 들어, ASP.NET을 부여 하 여 c:\inetpub\wwwroot에 대 한 쓰기 액세스 먼저 탐색기를 열고 디렉터리로 이동:

![](aspnet-and-iis6/_static/image19.jpg)

다음 예를 들어 'wwwroot' 속성과 선택 디렉터리를 마우스 오른쪽 단추로 클릭 합니다. 속성 대화 상자를 연 후 '보안' 탭을 선택 합니다.

![](aspnet-and-iis6/_static/image20.jpg)

C:\inetpub\wwwroot\ 디렉터리가 특수 디렉터리에는 특별 한 IIS 6.0 그룹 ' IIS\_WPG' 읽기 이미 부여 되어 &amp; 실행, 폴더 내용 보기 및 읽기 권한. 그러나 쓰기 권한을 부여 하려면 해야 쓰기에 대 한 허용 확인란을 클릭 합니다.

![](aspnet-and-iis6/_static/image21.jpg)

IIS 6.0은 이제이 폴더에 쓰기 권한을 가집니다. 이전에 유의 하 다음 단계-다른 폴더에 대 한 쓰기 권한을 부여 하려면, IIS를 추가 해야 할 수도\_WPG 그룹 아직 존재 하지 않는 경우.

> [!CAUTION]
> IIS에 쓰기 권한이 부여\_WPG ASP.NET 응용 프로그램을이 디렉터리에 쓸 수 있습니다.

## <a name="supporting-integrated-authentication-with-sql-server"></a>SQL Server를 사용 하 여 통합된 인증을 지 원하는

통합된 인증은 Windows NT 인증을 활용 하 여 SQL Server에 대 한 SQL Server 로그온 계정 유효성 검사를 허용 합니다. 표준 SQL Server 로그온 프로세스를 사용 하지 않으려면이 있습니다. 이 방법을 사용 하 여 네트워크 사용자 SQL Server Windows NT 네트워크 보안 프로세스에서 사용자 및 암호 정보를 가져오는 때문에 별도 로그온 id 또는 암호를 제공 하지 않고 SQL Server 데이터베이스를 액세스할 수 있습니다.

자격 증명 없이 응용 프로그램에 대 한 연결 문자열 내의 어느 저장 되기 때문에 좋은 선택 하는 ASP.NET 응용 프로그램에 대 한 통합된 인증 선택입니다. 대신 SQL에 연결할 때 사용할 연결 문자열은 다음과 같이 표시 됩니다.

`"server=localhost; database=Northwind;Trusted_Connection=true"`

이 연결 문자열에는 SQL Server에 액세스 하는 응용 프로그램의 Windows 자격 증명을 사용 하도록 SQL Server 알려 줍니다. ASP.NET/IIS 6의 경우 IIS에서 계정이 것이\_WPG 그룹입니다.

SQL Server와 ASP.NET 간의 통합된 인증을 사용 하려면 먼저 SQL Server 통합된 인증 또는 혼합 모드 인증에 대 한 구성 되어 있는지를 확인 해야이 확인 하기 위해 DBA를 사용 하 여 확인 합니다. 이러한 두 가지 모드 중 하나에 SQL Server 인 경우에 통합된 인증을 사용할 수 있습니다.

SQL Server 엔터프라이즈 관리자를 열고 (시작 | 프로그램 | Microsoft SQL Server | 적절 한 서버를 선택 하 고 보안 폴더를 확장 하는 엔터프라이즈 관리자):

![](aspnet-and-iis6/_static/image22.jpg)

경우 ' BUILTINT\IIS\_WPG' 그룹 없는 로그인을 마우스 오른쪽 단추로 클릭 하 고 새 로그인을 선택 합니다.

![](aspnet-and-iis6/_static/image23.jpg)

에 ' 이름:' 텍스트 상자에 입력 하거나 붙여넣습니다 ' [Server/도메인 이름] \IIS\_WPG' Windows NT 사용자/그룹 선택 하 고 줄임표 단추 클릭 또는:

![](aspnet-and-iis6/_static/image24.jpg)

현재 컴퓨터의 IIS 선택\_WPG 그룹 하 고 'Add' 및 선택기를 닫으려면 확인 합니다.

그런 다음 기본 데이터베이스 및 데이터베이스에 액세스 권한을 설정 해야 합니다. 설정 하려면 기본 데이터베이스 예를 들어 아래 Northwind 선택 드롭다운 목록에서에서 선택 합니다.

![](aspnet-and-iis6/_static/image25.jpg)

다음으로, 데이터베이스 액세스 탭을 클릭 합니다.

![](aspnet-and-iis6/_static/image26.jpg)

에 대 한 액세스를 허용 하려는 모든 데이터베이스에 대 한 허용 확인란을 클릭 합니다. 또한 해야 데이터베이스 역할 선택 db 검사\_소유자 로그인에 관리 하 고 선택한 데이터베이스를 사용 하는 데 필요한 모든 권한이 확인 됩니다.

속성 대화 상자를 종료 하려면 확인을 클릭 합니다. ASP.NET 응용 프로그램은 이제 통합 된 SQL Server 인증을 지원 하도록 구성 됩니다.

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a>IIS 6.0 기본 모드로 ASP.NET 1.0을 실행 하지 마세요

IIS 5 호환 모드로 IIS 6.0에서 ASP.NET 1.0만 지원 됩니다.

IIS 5.0 호환성 모드에서 실행 되도록 ASP.NET 1.0을 구성 하려면 인터넷 서비스 관리자 및 웹 사이트를 마우스 오른쪽 단추로 클릭 열고 속성을 선택 합니다.

![](aspnet-and-iis6/_static/image27.jpg)

서비스 탭으로 전환 하 고 확인? IIS 5.0 격리 모드에서 WWW 서비스 실행 됨:

![](aspnet-and-iis6/_static/image28.jpg)
