---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 프로덕션에 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자 (usin ...)에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: ec025e757d00cbfbfbcda9408739d2593908bc07
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240624"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 프로덕션 환경에 배포

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈에서는 Visual Studio 2012 또는 Visual Studio 2010를 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다. 계열에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)를 참조 하십시오.

## <a name="overview"></a>개요

이 자습서에서는 Visual Studio one 클릭 게시 기능을 사용 하 여 Microsoft Azure 계정을 설정 하 고, 스테이징 및 프로덕션 환경을 만들고, 스테이징 및 프로덕션 환경에 ASP.NET 웹 응용 프로그램을 배포 합니다.

선호 하는 경우 타사 호스팅 공급자에 배포할 수 있습니다. 이 자습서에서 설명 하는 대부분의 절차는 각 공급자에 게 계정 및 웹 사이트 관리를 위한 자체 사용자 인터페이스가 있는 경우를 제외 하 고는 호스팅 공급자 또는 Azure에 대해 동일 합니다. Microsoft.com 웹 사이트의 [공급자 갤러리](https://www.microsoft.com/web/hosting) 에서 호스팅 공급자를 찾을 수 있습니다.

미리 알림: 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면이 자습서 시리즈의 문제 해결 페이지를 확인 해야 합니다.

## <a name="get-a-microsoft-azure-account"></a>Microsoft Azure 계정 가져오기

아직 Azure 계정이 없는 경우 몇 분만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/free/dotnet/)을 참조하세요.

## <a name="create-a-staging-environment"></a>스테이징 환경 만들기

> [!NOTE]
> 이 자습서는 작성 되었으므로 스테이징 및 프로덕션 환경을 만들기 위한 많은 프로세스를 자동화 하는 새로운 기능을 추가 Azure App Service. [Azure App Service에서 웹 앱에 대 한 스테이징 환경 설정](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/)을 참조 하세요.

[테스트 환경에 배포 자습서](deploying-to-iis.md)에 설명 된 것 처럼 가장 안정적인 테스트 환경은 프로덕션 웹 사이트와 동일한 호스팅 공급자의 웹 사이트입니다. 많은 호스팅 공급자에서이의 이점은 상당한 추가 비용을 기준으로 평가 해야 하지만, Azure에서 추가 무료 웹 앱을 준비 앱으로 만들 수 있습니다. 또한 데이터베이스가 필요 하 고, 프로덕션 데이터베이스의 비용에 대 한 추가 비용이 없음 또는 최소가 됩니다. Azure에서 각 데이터베이스에 대해 사용 하는 대신 사용 하는 데이터베이스 저장소의 양에 대 한 비용을 지불 하 고 준비에 사용할 추가 저장소의 양은 최소화 됩니다.

[테스트 환경에 배포 자습서](deploying-to-iis.md)에 설명 된 대로 스테이징 및 프로덕션 환경에서는 두 개의 데이터베이스를 하나의 데이터베이스로 배포 합니다. 각 환경에 대 한 추가 데이터베이스를 만들고 게시 프로필을 만들 때 각 데이터베이스에 대해 올바른 대상 문자열을 선택 하는 경우를 제외 하 고는 프로세스는 동일 하 게 유지 됩니다.

자습서의이 섹션에서는 스테이징 환경에 사용할 웹 앱 및 데이터베이스를 만들고 프로덕션 환경에 배포 하 고 배포 하기 전에 스테이징 및 테스트에 배포 합니다.

> [!NOTE]
> 다음 단계에서는 Azure 관리 포털을 사용 하 여 Azure App Service에서 웹 앱을 만드는 방법을 보여 줍니다. 최신 버전의 Azure SDK에서는 서버 탐색기를 사용 하 여 Visual Studio를 종료 하지 않고이 작업을 수행할 수도 있습니다. Visual Studio 2013에서는 게시 대화 상자에서 직접 웹 앱을 만들 수도 있습니다. 자세한 내용은 [Azure App Service에서 ASP.NET 웹 앱 만들기를 참조 하세요.](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)

1. [Azure 관리 포털](https://manage.windowsazure.com/)에서 **웹 사이트**를 클릭 한 다음 **새로 만들기**를 클릭 합니다.
2. **웹 사이트**를 클릭 한 다음 **사용자 지정 만들기**를 클릭 합니다.

    **새 웹 사이트-사용자 지정 만들기** 마법사가 열립니다. **사용자 지정 만들기** 마법사를 사용 하면 웹 사이트와 데이터베이스를 동시에 만들 수 있습니다.
3. 마법사의 **웹 사이트 만들기** 단계에서 **URL** 상자에 문자열을 입력 하 여 응용 프로그램의 스테이징 환경에 대 한 고유 url로 사용 합니다. 예를 들어 ContosoUniversity를 사용 하는 경우 ContosoUniversity-staging123 (끝에 난수 포함)를 입력 합니다.

    전체 URL은 여기에 입력한 문자열과 텍스트 상자 옆에 표시되는 접미사로 구성됩니다.
4. **지역** 드롭다운 목록에서 가장 가까운 지역을 선택 합니다.

    이 설정은 웹 앱이 실행 되는 데이터 센터를 지정 합니다.
5. **데이터베이스** 드롭다운 목록에서 **새 SQL 데이터베이스 만들기**를 선택 합니다.
6. **DB 연결 문자열 이름** 상자에서 기본값인 *defaultconnection*을 그대로 둡니다.
7. 상자 아래쪽의 오른쪽을 가리키는 화살표를 클릭 합니다.

    다음 그림에서는 예제 값을 포함 하는 **웹 사이트 만들기** 대화 상자를 보여 줍니다. 입력 한 URL과 지역은 다릅니다.

    ![웹 사이트 단계 만들기](deploying-to-production/_static/image1.png)

    마법사가 **Specify database settings** 단계로 진행합니다.
8. **이름** 상자에 *ContosoUniversity* 를 입력 하 여 고유 하 게 만듭니다 (예: *ContosoUniversity123*).
9. **서버** 상자에서 **새로 만들기 SQL Database 서버**를 선택 합니다.
10. 관리자 이름 및 암호를 입력 합니다.

    여기에 기존 이름과 암호를 입력 하지 않습니다. 나중에 데이터베이스에 액세스할 때 사용할 새 이름과 암호를 입력해야 합니다.
11. **지역** 상자에서 웹 앱에 대해 선택한 것과 동일한 지역을 선택 합니다.

    웹 서버와 데이터베이스 서버를 동일한 지역에 유지 하면 최상의 성능을 제공 하 고 비용을 최소화할 수 있습니다.
12. 상자 맨 아래에 있는 확인 표시를 클릭 하 여 완료 되었음을 표시 합니다.

    다음 그림에서는 예제 값을 포함 하는 **데이터베이스 설정 지정** 대화 상자를 보여 줍니다. 입력 한 값은 다를 수 있습니다.

    ![새 웹 사이트의 데이터베이스 설정 단계-데이터베이스 마법사로 만들기](deploying-to-production/_static/image2.png)

    관리 포털 웹 사이트 페이지로 반환 되 고 **상태** 열에는 웹 앱이 생성 되 고 있는 것으로 표시 됩니다. 잠시 후 (일반적으로 1 분 미만) **상태** 열에는 웹 앱이 성공적으로 생성 된 것으로 표시 됩니다. 왼쪽의 탐색 모음에서 계정에 있는 웹 앱 수가 웹 **사이트** 아이콘 옆에 나타나고 데이터베이스 수가 **SQL 데이터베이스** 아이콘 옆에 표시 됩니다.

    ![웹 사이트 페이지 관리 포털의 웹 사이트 페이지를 만들었습니다.](deploying-to-production/_static/image3.png)

    웹 앱 이름은 그림의 예제 앱과 다를 수 있습니다.

## <a name="deploy-the-application-to-staging"></a>스테이징에 응용 프로그램 배포

이제 스테이징 환경에 대 한 웹 앱 및 데이터베이스를 만들었으므로 프로젝트를 배포할 수 있습니다.

> [!NOTE]
> 이 지침에서는 publishsettings 파일을 다운로드 하 여 게시 프로필을 만드는 방법을 보여 줍니다 *.* 이 파일은 Azure 뿐만 아니라 타사 호스팅 공급자에 대해서도 작동 합니다. 최신 Azure SDK를 사용 하 여 Visual Studio에서 Azure에 직접 연결 하 고 Azure 계정에 있는 웹 앱 목록에서 선택할 수도 있습니다. Visual Studio 2013에서 **웹 게시** 대화 상자 또는 **서버 탐색기** 창에서 Azure에 로그인 할 수 있습니다. 자세한 내용은 [Azure App Service에서 ASP.NET 웹 앱 만들기](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)를 참조 하세요.

### <a name="download-the-publishsettings-file"></a>Publishsettings 파일을 다운로드 합니다.

1. 방금 만든 웹 앱의 이름을 클릭 합니다.

    ![사이트를 클릭 하 여 대시보드로 이동 합니다.](deploying-to-production/_static/image4.png)
2. **대시보드** 탭의 **빠른** 보기에서 **게시 프로필 다운로드**를 클릭 합니다.

    ![게시 프로필 링크 다운로드](deploying-to-production/_static/image5.png)

    이 단계에서는 웹 앱에 응용 프로그램을 배포 하기 위해 필요한 모든 설정이 포함 된 파일을 다운로드 합니다. 이 파일을 Visual Studio로 가져오면이 정보를 수동으로 입력할 필요가 없습니다.
3. Visual Studio에서 액세스할 수 있는 폴더에 *publishsettings* 파일을 저장 합니다.

    ![publishsettings 파일을 저장 하는 중](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > 보안- *publishsettings* 파일에는 Azure 구독 및 서비스를 관리 하는 데 사용 되는 자격 증명 (인코딩되지 않음)이 포함 되어 있습니다. 이 파일의 보안을 유지하는 가장 좋은 방법은 소스 디렉터리 밖(예: 라이브러리\문서 폴더)에 임시로 파일을 저장한 다음 일단 가져오기가 완료되면 삭제하는 것입니다. *Publishsettings* 파일에 대 한 액세스 권한을 획득 하는 악의적인 사용자는 Azure 서비스를 편집, 생성 및 삭제할 수 있습니다.

### <a name="create-a-publish-profile"></a>게시 프로필 만들기

1. Visual Studio의 **솔루션 탐색기** 에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 **게시** 를 선택 합니다.

    **웹 게시** 마법사가 열립니다.
2. **프로필** 탭을 클릭 합니다.
3. **가져오기**를 클릭합니다.
4. 이전에 다운로드 한 *publishsettings* 파일로 이동한 다음 **열기**를 클릭 합니다.

    ![게시 설정 가져오기 대화 상자](deploying-to-production/_static/image7.png)
5. **연결** 탭에서 **연결 유효성 검사** 를 클릭 하 여 설정이 올바른지 확인 합니다.

    연결의 유효성을 검사 한 경우 **연결 유효성 검사** 단추 옆에 녹색 확인 표시가 표시 됩니다.

    일부 호스팅 공급자의 경우 **연결 유효성 검사**를 클릭 하면 **인증서 오류** 대화 상자가 표시 될 수 있습니다. 이 경우 서버 이름이 필요한 지 확인 합니다. 서버 이름이 올바르면 **나중에 Visual Studio의 세션에 대해이 인증서 저장** 을 선택 하 고 **동의**를 클릭 합니다. (이 오류는 배포 하는 URL에 대 한 SSL 인증서 구매 비용을 방지 하기 위해 호스팅 공급자가 선택 했음을 의미 합니다. 유효한 인증서를 사용 하 여 보안 연결을 설정 하는 것을 선호 하는 경우 호스팅 공급자에 게 문의 하세요.)
6. **다음**을 클릭합니다.

    ![연결 성공 아이콘 및 연결 탭의 다음 단추](deploying-to-production/_static/image8.png)
7. **설정** 탭에서 **파일 게시 옵션**을 확장 하 고 **앱 \_ 데이터 폴더에서 파일 제외**를 선택 합니다.

    **파일 게시 옵션**의 기타 옵션에 대 한 자세한 내용은 [IIS에 배포](deploying-to-iis.md) 자습서를 참조 하십시오. 이 단계의 결과와 다음 데이터베이스 구성 단계를 보여 주는 스크린샷은 데이터베이스 구성 단계의 끝에 있습니다.
8. **데이터베이스** 섹션의 **defaultconnection** 에서 멤버 자격 데이터베이스에 대 한 데이터베이스 배포를 구성 합니다.
9. 1. **데이터베이스 업데이트**를 선택 합니다.

        **Defaultconnection** 바로 아래에 있는 **원격 연결 문자열** 상자는 publishsettings 파일의 연결 문자열로 채워집니다. 연결 문자열에는 *. pubxml* 파일에 일반 텍스트로 저장 된 SQL Server 자격 증명이 포함 되어 있습니다. 이러한 항목을 영구적으로 저장 하지 않으려는 경우에는 데이터베이스를 배포한 후 게시 프로필에서 제거 하 고, 대신 Azure에 저장 하면 됩니다. 자세한 내용은 Scott Hanselman의 블로그에서 [원본에서 Azure에 배포할 때 ASP.NET 데이터베이스 연결 문자열을 안전 하 게 유지 하는 방법](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx) 을 참조 하세요.
      2. **데이터베이스 업데이트 구성**을 클릭 합니다.
      3. **데이터베이스 업데이트 구성** 대화 상자에서 **SQL 스크립트 추가**를 클릭 합니다.
      4. **Sql 스크립트 추가** 상자에서 이전에 솔루션 폴더에 저장 한 *aspnet-data-prod* 스크립트로 이동한 다음 **열기**를 클릭 합니다.
      5. **데이터베이스 업데이트 구성** 대화 상자를 닫습니다.
10. **데이터베이스** 섹션의 **schoolcontext.cs** 에서 **실행 Code First 마이그레이션 (응용 프로그램 시작 시 실행)** 를 선택 합니다.

    Visual Studio에는 클래스에 대 한 **업데이트 데이터베이스** 대신 **Execute Code First 마이그레이션** 이 표시 됩니다 `DbContext` . 클래스를 사용 하 여 액세스 하는 데이터베이스를 배포 하기 위해 마이그레이션 대신 dbDacFx 공급자를 사용 하려는 경우 `DbContext` Visual Studio 및 ASP.NET FOR MSDN의 웹 배포 FAQ에서 [마이그레이션을 사용 하지 않고 Code First 데이터베이스 배포를 어떻게 할까요?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) 참조 하세요.

    **설정** 탭은 이제 다음 예제와 같습니다.

    ![준비에 대 한 설정 탭](deploying-to-production/_static/image9.png)
11. 다음 단계를 수행 하 여 프로필을 저장 하 고 *준비*로 이름을 바꿉니다.

    1. **프로필** 탭을 클릭 한 다음 **프로필 관리**를 클릭 합니다.
    2. 가져오기에서는 두 개의 새 프로필을 만들었습니다. 하나는 FTP 용 하나이 고 다른 하나는 웹 배포입니다. 웹 배포 프로필을 구성 했습니다 .이 프로필의 이름을 *준비*로 바꾸세요.

        ![프로필 이름을 준비로 바꾸기](deploying-to-production/_static/image10.png)
    3. **웹 게시 프로필 편집** 대화 상자를 닫습니다.
    4. **웹 게시** 마법사를 닫습니다.

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a>환경 표시기의 게시 프로필 변환 구성

> [!NOTE]
> 이 섹션에서는 환경 표시기에 대해 Web.config 변환을 설정 하는 방법을 보여 줍니다. 표시기가 요소에 있기 때문 `<appSettings>` 에 Azure App Service 배포 하는 경우 변환을 지정 하는 또 다른 대안이 있습니다. 자세한 내용은 [Azure에서 Web.config 설정 지정](web-config-transformations.md#watransforms)을 참조 하세요.

1. **솔루션 탐색기**에서 **속성**을 확장 한 다음, **프로필 프로필**을 확장 합니다.
2. *스테이징. pubxml*을 마우스 오른쪽 단추로 클릭 한 다음 **구성 변환 추가**를 클릭 합니다.

    ![준비에 대 한 구성 변환 추가](deploying-to-production/_static/image11.png)

    Visual Studio에서 *Web.Staging.config* 변환 파일을 만들고 엽니다.
3. *Web.Staging.config* 변환 파일에서 다음 코드를 여는 태그 바로 뒤에 삽입 `configuration` 합니다.

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    준비 게시 프로필을 사용 하는 경우이 변환은 환경 표시기를 "Prod"로 설정 합니다. 배포 된 웹 앱에서 "Contoso 대학" H1 제목 뒤에 "(Dev)" 또는 "(Test)"와 같은 접미사가 표시 되지 않습니다.
4. *Web.Staging.config* 파일을 마우스 오른쪽 단추로 클릭 하 고 **변환 미리 보기** 를 클릭 하 여 코딩 된 변환이 필요한 변경 내용을 생성 하는지 확인 합니다.

    **Web.config 미리 보기** 창에는 *Web.Release.config* 변환과 *Web.Staging.config* 변환을 모두 적용 한 결과가 표시 됩니다.

### <a name="prevent-public-use-of-the-test-app"></a>테스트 앱의 공개 사용 방지

스테이징 앱에 대 한 중요 한 고려 사항은 인터넷에 살고 있지만 공용으로 사용 하지 않으려는 것입니다. 사용자가 찾아서 사용할 가능성을 최소화 하기 위해 다음 방법 중 하나 이상을 사용할 수 있습니다.

- 스테이징을 테스트 하는 데 사용 하는 IP 주소 에서만 준비 앱에 대 한 액세스를 허용 하는 방화벽 규칙을 설정 합니다.
- 추측 하기에 불가능 한 난독 처리 된 URL을 사용 합니다.
- 검색 엔진이 테스트 앱 및 검색 결과에 대 한 보고서 링크를 탐색 하지 않도록 *robots.txt* 파일을 만듭니다.

이러한 메서드 중 첫 번째 메서드는 가장 효과적 이지만이 자습서에서는 Azure App Service 대신 Azure 클라우드 서비스에 배포 해야 하기 때문에 다루지 않습니다. Azure의 Cloud Services 및 IP 제한에 대 한 자세한 내용은 Azure에서 제공 하는 [계산 호스팅 옵션](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) 을 참조 하 고 [특정 IP 주소가 웹 역할에 액세스 하지 못하도록 차단](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx)합니다. 타사 호스팅 공급자에 배포 하는 경우 공급자에 게 문의 하 여 IP 제한을 구현 하는 방법을 알아보세요.

이 자습서에서는 *robots.txt* 파일을 만듭니다.

1. **솔루션 탐색기**에서 ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **새 항목 추가**를 클릭 합니다.
2. *robots.txt*이라는 새 **텍스트 파일** 을 만들고 다음 텍스트를 입력 합니다.

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    `User-agent`이 줄은 파일의 규칙이 모든 검색 엔진 웹 크롤러 (로봇)에 적용 된다는 것을 검색 엔진에 알려 주며, `Disallow` 줄은 사이트의 페이지를 크롤링하지 않도록 지정 합니다.

    검색 엔진에서 프로덕션 앱을 카탈로그로 작성 하 여 프로덕션 배포에서이 파일을 제외 해야 합니다. 이렇게 하려면 프로덕션 게시 프로필을 만들 때이 프로필의 설정을 구성 합니다.

### <a name="deploy-to-staging"></a>스테이징에 배포

1. Contoso 대학 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 클릭 하 여 **웹 게시** 마법사를 엽니다.
2. **준비** 프로필을 선택 했는지 확인 합니다.
3. **게시**를 클릭합니다.

    **출력** 창에 수행된 배포 작업이 표시되고 성공적인 배포 완료가 보고됩니다. 기본 브라우저가 자동으로 열리고 배포 된 웹 앱의 URL이 열립니다.

## <a name="test-in-the-staging-environment"></a>스테이징 환경에서 테스트

환경 표시기가 없다는 것을 확인할 수 있습니다. H1 제목 뒤에는 "(테스트)" 또는 "(Dev)"가 없습니다. 여기에는 환경 표시기의 *Web.config* 변환이 성공 했음을 보여 줍니다.

![홈 페이지 준비](deploying-to-production/_static/image12.png)

**학생** 페이지를 실행 하 여 배포 된 데이터베이스에 학생이 없는 경우를 확인 합니다.

**강사 페이지를** 실행 하 여 Code First가 강사 데이터로 데이터베이스를 시드 하는지 확인 합니다.

**학생 메뉴에서** **학생 추가** 를 선택 하 고 학생을 추가한 다음 **학생** 페이지에서 새 학생을 보고 데이터베이스에 성공적으로 쓸 수 있는지 확인 합니다.

**과정** 페이지에서 **크레딧 업데이트**를 클릭 합니다. [ **크레딧 업데이트** ] 페이지에는 관리자 권한이 필요 하므로 **로그인** 페이지가 표시 됩니다. 이전에 만든 관리자 계정 자격 증명 ("admin" 및 "prodpwd")을 입력 합니다. 이전 자습서에서 만든 관리자 계정이 테스트 환경에 올바르게 배포 되었는지 확인 하는 **크레딧 업데이트** 페이지가 표시 됩니다.

ELMAH에서 추적 되는 오류를 발생 시키는 잘못 된 URL을 요청 하 고 ELMAH 오류 보고서를 요청 합니다. 타사 호스팅 공급자에 배포 하는 경우 이전 자습서에서 비어 있던 것과 동일한 이유로 보고서가 비어 있을 수 있습니다. ELMAH가 로그 폴더에 쓸 수 있도록 호스팅 공급자의 계정 관리 도구를 사용 하 여 폴더 사용 권한을 구성 해야 합니다.

만든 응용 프로그램은 이제 프로덕션에 사용 하는 것과 동일한 웹 앱의 클라우드에서 실행 됩니다. 모든 것이 올바르게 작동 하므로 다음 단계는 프로덕션 환경에 배포 하는 것입니다.

## <a name="deploy-to-production"></a>프로덕션 환경에 배포

프로덕션 웹 앱을 만들고 프로덕션에 배포 하는 프로세스는 스테이징의 경우와 동일 하지만 배포에서 *robots.txt* 제외 해야 한다는 점이 다릅니다. 이렇게 하려면 게시 프로필 파일을 편집 합니다.

### <a name="create-the-production-environment-and-the-production-publish-profile"></a>프로덕션 환경 및 프로덕션 게시 프로필 만들기

1. 스테이징에 사용한 것과 동일한 절차에 따라 Azure에서 프로덕션 웹 앱 및 데이터베이스를 만듭니다.

    데이터베이스를 만들 때 이전에 만든 것과 동일한 서버에 데이터베이스를 배치 하거나 새 서버를 만들 수 있습니다.
2. *Publishsettings* 파일을 다운로드 합니다.
3. 준비에 사용한 것과 동일한 절차에 따라 *publishsettings* 파일을 가져와서 게시 프로필을 만듭니다.

    **설정** 탭의 **데이터베이스** 섹션에서 **defaultconnection** 아래의 데이터 배포 스크립트를 구성 하는 것을 잊지 마세요.
4. 게시 프로필의 이름을 *Production*로 바꿉니다.
5. 준비에 사용한 것과 동일한 절차에 따라 환경 표시기의 게시 프로필 변환을 구성 합니다.

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a>robots.txt를 제외 하도록 pubxml 파일을 편집 합니다.

게시 프로필 파일의 이름은 &lt; profilename &gt; *.xml* 이 고, *게시 프로필* 폴더에 있습니다. *Proprofiles* 폴더는 c # 웹 응용 프로그램 프로젝트의 *Properties* 폴더 아래, VB 웹 응용 프로그램 프로젝트의 *My project* 폴더 아래 또는 웹 앱 프로젝트의 *응용 프로그램 \_ 데이터* 폴더 아래에 있습니다. 각 *. pubxml* 파일에는 하나의 게시 프로필에 적용 되는 설정이 포함 되어 있습니다. 웹 게시 마법사에서 입력 하는 값은 이러한 파일에 저장 되며,이를 편집 하 여 Visual Studio UI에서 사용할 수 없는 설정을 만들거나 변경할 수 있습니다.

기본적으로 *. pubxml* 파일은 게시 프로필을 만들 때 프로젝트에 포함 되지만 프로젝트에서 제외할 수 있으며 Visual Studio에서 해당 파일을 계속 사용 합니다. Visual Studio는 프로젝트에 포함 되어 있는지 여부에 관계 없이 *pubxml* 파일에 대 한 파일 *프로필* 폴더를 찾습니다.

각 *. pubxml* 파일에는 *pubxml 사용자* 파일이 있습니다. *사용자가* **암호 저장** 옵션을 선택한 경우이 파일에는 암호화 된 암호가 포함 되며, 기본적으로 프로젝트에서 제외 됩니다.

*Pubxml* 파일에는 특정 게시 프로필과 관련 된 설정이 포함 되어 있습니다. 모든 프로필에 적용 되는 설정을 구성 하려는 경우에는 *wpp .targets* 파일을 만들 수 있습니다. 빌드 프로세스는 이러한 파일을 *.csproj* 또는 *.vbproj* 프로젝트 파일로 가져오므로 프로젝트 파일에서 구성할 수 있는 대부분의 설정은 이러한 파일에서 구성할 수 있습니다. *Pubxml* 파일 및 *.* n e t 파일에 대 한 자세한 내용은 [방법: Visual Studio 웹 프로젝트의 게시 프로필 (pubxml) 파일 및 .Targets .Targets 파일에서 배포 설정 편집](https://msdn.microsoft.com/library/ff398069.aspx)을 참조 하세요.

1. **솔루션 탐색기**에서 **속성** 을 확장 하 고, **프로필 프로필**을 확장 합니다.
2. *Production pubxml* 을 마우스 오른쪽 단추로 클릭 하 고 **열기**를 클릭 합니다.

    ![Pubxml 파일을 엽니다.](deploying-to-production/_static/image13.png)
3. *Production pubxml* 을 마우스 오른쪽 단추로 클릭 하 고 **열기**를 클릭 합니다.
4. 닫는 요소 바로 앞에 다음 줄을 추가 합니다 `PropertyGroup` .

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    이제 pubxml 파일은 다음 예제와 같습니다.

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    파일 및 폴더를 제외 하는 방법에 대 한 자세한 내용은 MSDN의 **Visual Studio 및 ASP.NET에 대 한 웹 배포 FAQ** 의 [배포에서 특정 파일 또는 폴더를 제외할 수 있나요?](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) 를 참조 하세요.

### <a name="deploy-to-production"></a>프로덕션 환경에 배포

1. **웹 게시** 마법사를 열고 **프로덕션** 게시 프로필을 선택 했는지 확인 한 다음 **미리** 보기 탭에서 **미리 보기 시작** 을 클릭 하 여 *robots.txt* 파일이 프로덕션 앱에 복사 되지 않는지 확인 합니다.

    ![프로덕션에 게시할 파일 미리 보기](deploying-to-production/_static/image14.png)

    복사할 파일의 목록을 검토 합니다. *Aspx.cs*, *aspx.designer.cs*, *Master.cs*및 *Master.designer.cs* 파일을 비롯 한 모든 *.cs* 파일이 생략 된 것을 볼 수 있습니다. 이 코드는 모두 *bin* 폴더에서 찾을 *ContosoUniversity.dll* 및 *ContosoUniversity* 파일로 컴파일 되었습니다. 응용 프로그램을 실행 하는 데는 *.dll* 만 필요 하 고, 이전에는 응용 프로그램을 실행 하는 데 필요한 파일만 배포 하도록 지정 했으므로 *.cs* 파일은 대상 환경에 복사 되지 않습니다. *Obj* 폴더와 *ContosoUniversity* 및 *.csproj* 파일은 동일한 이유로 생략 됩니다.

    **게시** 를 클릭 하 여 프로덕션 환경에 배포 합니다.
2. 스테이징에 사용한 것과 동일한 절차에 따라 프로덕션에서 테스트 합니다.

    URL 및 *robots.txt* 파일의 부재를 제외 하 고는 모두 준비와 동일 합니다.

## <a name="summary"></a>요약

이제 웹 앱을 성공적으로 배포 하 고 테스트 했으며 인터넷을 통해 공개적으로 사용할 수 있습니다.

![홈 페이지 프로덕션](deploying-to-production/_static/image15.png)

다음 자습서에서는 응용 프로그램 코드를 업데이트 하 고 변경 내용을 테스트, 스테이징 및 프로덕션 환경에 배포 합니다.

> [!NOTE]
> 프로덕션 환경에서 응용 프로그램을 사용 하는 동안에는 복구 계획을 구현 해야 합니다. 즉, 프로덕션 앱에서 안전한 저장소 위치로 데이터베이스를 정기적으로 백업 해야 하며 이러한 백업에 대 한 여러 세대를 유지 해야 합니다. 데이터베이스를 업데이트 하는 경우 변경 직전에 백업 복사본을 만들어야 합니다. 그런 다음, 실수를 하 고 프로덕션 환경에 배포한 후에도이를 검색 하지 않으면 데이터베이스가 손상 되기 전의 상태로 복구 될 수 있습니다. 자세한 내용은 [Azure SQL Database Backup 및 복원](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx)을 참조하세요.
> 
> 
> [!NOTE]
> 이 자습서에서 배포 하는 SQL Server 버전은 Azure SQL Database 됩니다. 배포 프로세스는 다른 버전의 SQL Server와 유사 하지만, 일부 시나리오에서 실제 프로덕션 응용 프로그램에는 Azure SQL Database에 대 한 특수 코드가 필요할 수 있습니다. 자세한 내용은 [Azure SQL Database 작업](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb) 및 [SQL Server 및 Azure SQL Database 중에서 선택](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing)을 참조 하세요.
> 
> [!div class="step-by-step"]
> [이전](setting-folder-permissions.md)
> [다음](deploying-a-code-update.md)
