---
uid: web-forms/overview/deployment/visual-studio-web-deployment/introduction
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 소개 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자에서 ASP.NET (게시) V를 사용 하는 중...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 24ad086d-865e-433c-9ac9-05f1a553da16
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/introduction
msc.type: authoredcontent
ms.openlocfilehash: 0edab77cd973af129e54c7867265f86b47c349a6
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59410138"
---
# <a name="aspnet-web-deployment-using-visual-studio-introduction"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 소개

[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자에서 ASP.NET (게시).NET 용 Azure SDK를 사용 하 여 Visual Studio 2012를 사용 합니다. 대부분의 절차는 Visual Studio 2013 용 비슷합니다.
> 
> 인터넷을 통해 사용자를 사용할 수 있도록 웹 응용 프로그램을 개발 합니다. 하지만 개발 컴퓨터에서 작업 결과 얻게 하는 방법을 설명 했으므로 이러한 직후에 일반적으로 웹 프로그래밍 자습서 중지 합니다. 이 자습서 시리즈에서는 해제할 다른 여기서 시작: 웹 앱을 작성, 테스트, 했습니다 준비가 되 고 합니다. 새로운 기능 이 자습서는 테스트를 위해 로컬 개발 컴퓨터에 IIS 이동한 다음 스테이징 및 프로덕션에 대 한 타사 호스팅 공급자 또는 Azure에 먼저 배포 하는 방법을 보여줍니다. 샘플 응용 프로그램을 배포 하는 경우 Entity Framework, SQL Server 및 ASP.NET 멤버 자격 시스템을 사용 하는 웹 응용 프로그램 프로젝트 샘플 응용 프로그램에 ASP.NET Web Forms를 사용 하 여 있지만 표시 된 절차는 ASP.NET MVC 및 Web API에도 적용 합니다.
> 
> 이 자습서는 Visual Studio에서 ASP.NET을 사용 하는 방법을 알고 있다고 가정 합니다. 시작 하는 것이 좋습니다는 이렇게 하지 않으면를 [기본 ASP.NET Web Forms 자습서](../../older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1.md) 또는 [기본 ASP.NET MVC 자습서](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)합니다.
> 
> 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET 배포 포럼](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) 또는 [StackOverflow](http://stackoverflow.com)합니다.
> 
> 이 콘텐츠는 무료 전자책 제공 이기도 [TechNet 전자책 갤러리](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#ASPNETWebDeploymentusingVisualStudio)합니다.


## <a name="overview"></a>개요

이 자습서는 SQL Server 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 배포를 안내 합니다. 테스트를 위해 로컬 개발 컴퓨터에 IIS 이동한 다음 Azure App Service에서 스테이징 및 프로덕션을 위해 Azure SQL Database에 웹 앱에 먼저 배포. One-click 게시 하는 Visual Studio를 사용 하 여 배포 하는 방법을 표시 하 고 명령줄을 사용 하 여 배포 하는 방법을 배웁니다.

다양 한 자습서는 까다롭게 보일 배포 프로세스를 만들 수 있습니다. 사실, 기본 절차는 간단 합니다. 그러나 실제 상황에서 종종 해야 할 추가 배포 작업-예를 들어 대상 서버의 폴더 사용 권한을 설정 합니다. 에서는 일부의 자습서를 성공적으로 실제 응용 프로그램 배포를 방해할 수 있는 정보 둬서는 안 기대에서 이러한 추가 작업을에 대해 설명 했습니다.

자습서는 순서 대로 실행 되도록 설계 하 고 이전 부분을 기반으로 하는 각 부분입니다. 상황에 관련이 없는 일부를 건너뛸 수 있지만 다음 나중에 자습서에서 절차를 조정 해야 할 수 있습니다.

## <a name="intended-audience"></a>대상 독자

이 자습서는 ASP.NET 개발자 환경에서 작업 하는 것을 목표로 위치:

- 프로덕션 환경은 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다.
- 배포는 지속적인 통합 프로세스 제한 되지 않지만 Visual Studio에서 직접 수행할 수 있습니다.

배포 [소스 제어](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md) 사용 하는 [지속적인](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 프로세스 명령줄에서 배포 하는 방법을 보여 주는 한 자습서를 제외 하 고이 자습서에서 다루지 않습니다. 지속적인 업데이트에 대 한 내용은 다음 리소스를 참조 합니다.

- [연속 통합 및 지속적인 업데이트 (Windows Azure 사용 하 여 빌드 실제 클라우드 앱)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)
- [Azure App Service에서 웹 앱 배포](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)
- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md) (엔터프라이즈 환경에 대 한 유용한 정보에 여전히 있는 Visual Studio 2010 용으로 작성 하는 자습서의 이전 집합입니다.)

## <a name="using-a-third-party-hosting-provider"></a>타사 호스팅 공급자를 사용 하 여

이 자습서에서는 Azure 계정을 설정 하 고 스테이징 및 프로덕션을 위해 Azure App Service에서 Web Apps에 응용 프로그램 배포 과정을 안내 합니다. 그러나 사용자가 선택한 타사 호스팅 공급자를 배포 하기 위한 동일한 기본 절차를 사용할 수 있습니다. 자습서 고유 프로세스를 통해 Azure로 이동 하는 경우를 설명 하며 타사 호스팅 공급자에서 예상할 수 있는 어떤 차이 것이 좋습니다.

## <a name="deploying-web-app-projects"></a>웹 앱 프로젝트를 배포합니다.

샘플 응용 프로그램을 다운로드 하 고이 자습서에 대 한 배포에 Visual Studio 웹 응용 프로그램 프로젝트입니다. 그러나 최신 설치 하는 경우 [Visual Studio 웹 게시 업데이트](https://msdn.microsoft.com/tr-tr/library/jj161045.aspx), 웹 앱 프로젝트에 대 한 동일한 배포 방법 및 도구를 사용할 수 있습니다.

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC 프로젝트를 배포합니다.

샘플 응용 프로그램 ASP.NET Web Forms 프로젝트를 이지만 모든 작업을 수행 하는 방법을 알아봅니다도 ASP.NET MVC에 적용 됩니다. Visual Studio MVC 프로젝트는 다른 형태의 웹 응용 프로그램 프로젝트입니다. 유일한 차이점은는 ASP.NET MVC 또는의 대상 버전을 지원 하지 않는 호스팅 공급자에 배포 하는 경우 해야 적절 한 설치 ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0)하십시오 [MVC 4](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/4.0.30506.0) 또는 [MVC 5](http://www.nuget.org/packages/Microsoft.AspNet.Mvc)) 프로젝트에 NuGet 패키지.

## <a name="programming-language"></a>프로그래밍 언어

샘플 응용 프로그램을 사용 하 여 C# 자습서는 C#에 대 한 지식이 필요 하지 않습니다 있고 자습서에 설명 된 배포 방법 언어별 없는 합니다.

## <a name="database-deployment-methods"></a>데이터베이스 배포 방법

세 가지 방법으로 Visual Studio에서 웹 배포와 함께 SQL Server 데이터베이스를 배포할 수 있습니다.

- Entity Framework Code First 마이그레이션
- DbDacFx 웹 배포 공급자
- DbFullSql 웹 배포 공급자

이 자습서에서는 이러한 메서드의 처음 두 개를 사용 합니다. DbFullSql Web Deploy 공급자는 더 이상 SQL Server Compact에서 SQL Server로 마이그레이션와 같은 일부 특정 시나리오를 제외 하 고 권장 되는 레거시 메서드입니다.

이 자습서에 나와 있는 방법이 없습니다 SQL Server Compact, SQL Server 데이터베이스에 대 한 합니다. SQL Server Compact 데이터베이스를 배포 하는 방법에 대 한 정보를 참조 하세요 [Visual Studio 웹 배포 사용 하 여 SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.

이 자습서에 표시 된 메서드를 필요한 웹 배포를 사용 하는 메서드를 게시 합니다. 다른 게시 FPSE, FTP, 파일 시스템 등의 메서드를 선호 하는 경우 참조 [웹 응용 프로그램 배포와 별도로 데이터베이스 배포](https://go.microsoft.com/fwlink/p/?LinkId=282413#databaseseparate) 에서 Visual Studio 및 ASP.NET 웹 배포 콘텐츠 맵.

### <a name="entity-framework-code-first-migrations"></a>Entity Framework Code First 마이그레이션

Entity Framework 버전 4.3, Microsoft Code First 마이그레이션을 도입 했습니다. Code First 마이그레이션을 데이터베이스에 변경 내용을 전파 하 고 데이터 모델에 대 한 증분 변경 프로세스를 자동화 합니다. Code First의 이전 버전에서는 일반적으로 Entity Framework를 삭제 하 고 데이터 모델을 변경할 때마다 데이터베이스를 다시 만들지를 사용 합니다. 테스트 데이터를 쉽게 다시 만들 하지만 프로덕션 환경에서 일반적으로 데이터베이스를 삭제 하지 않고 데이터베이스 스키마를 업데이트 하기 때문에 개발에서 문제가 아닙니다. 삭제 하 고 다시 작성 하지 않고 데이터베이스를 업데이트 하려면 Code First 마이그레이션 기능 사용 하도록 설정 합니다. Code First 자동으로 필요한 스키마 변경을 수행 하는 방법을 결정 하거나 변경 내용을 사용자 지정 하는 코드를 작성할 수 있습니다. Code First 마이그레이션을 소개를 참조 하세요 [Code First 마이그레이션을](https://msdn.microsoft.com/library/hh770484.aspx)합니다.

웹 프로젝트를 배포 하는 경우 Visual Studio에서 Code First 마이그레이션을 관리 하는 데이터베이스를 배포 하는 프로세스를 자동화할 수 있습니다. 게시 프로필을 만들면 Execute Code First Migrations (응용 프로그램 시작 시 실행) 이라는 레이블이 있는 확인란을 선택 합니다. 이렇게이 설정 하면 Code First 사용 되도록 자동으로 대상 서버에서 응용 프로그램 Web.config 파일을 구성 하는 배포 프로세스는 `MigrateDatabaseToLatestVersion` 이니셜라이저 클래스입니다.

Visual Studio 배포 프로세스 중 데이터베이스를 사용 하 여 작업을 수행 하지 않습니다. 배포 된 응용 프로그램 배포 후 처음으로 데이터베이스에 액세스할 때 Code First 자동으로 데이터베이스 만들거나 데이터베이스 스키마를 최신 버전으로 업데이트 합니다. 응용 프로그램 마이그레이션을 Seed 메서드를 구현 하는 경우 데이터베이스를 만들거나 스키마가 업데이트 한 후 메서드를 실행 합니다.

이 자습서에서는 응용 프로그램 데이터베이스를 배포 하려면 Code First 마이그레이션을 사용할 수 있습니다.

### <a name="the-dbdacfx-web-deploy-provider"></a>DbDacFx 웹 배포 공급자

Entity Framework Code First에서 관리 하지 않는 SQL Server 데이터베이스에 대 한 게시 프로필을 구성 하는 경우 데이터베이스 업데이트 이라는 레이블이 있는 확인란을 선택할 수 있습니다. 초기 배포 동안 dbDacFx 공급자 원본 데이터베이스와 일치 하도록 대상 데이터베이스의 테이블과 다른 데이터베이스 개체를 만듭니다. 후속 배포에서 공급자 원본 및 대상 데이터베이스 간의 차이점을 결정 하 고 원본 데이터베이스와 일치 하도록 대상 데이터베이스의 스키마를 업데이트 합니다. 기본적으로 공급자 테이블 또는 열을 삭제할 때와 같은 데이터 손실이 발생 내용을 변경 하지 않습니다.

이 메서드는 데이터베이스 테이블에서 데이터의 배포를 자동화 되지 않습니다 하지만 작업을 수행 하 고 배포 하는 동안 실행 하는 Visual Studio를 구성 하는 스크립트를 만들 수 있습니다. 배포 하는 동안 스크립트를 실행 하려면 다른 이유는 데이터 손실이 발생 하기 때문에 자동으로 수행할 수 없는 스키마 변경을 수행 하기 위해서입니다.

이 자습서에서는 ASP.NET 멤버 자격 데이터베이스를 배포 하려면 dbDacFx 공급자를 사용할 수 있습니다.

## <a name="troubleshooting-during-this-tutorial"></a>이 자습서에서 문제 해결

배포 하는 동안 오류가 발생 하거나 배포 된 사이트 올바르게 실행 되지 않은 경우 오류 메시지는 확실 한 솔루션을 항상 제공 하지 않습니다. 몇 가지 일반적인 문제 시나리오를 사용 하 여 도움이 [문제 해결 참조 페이지](troubleshooting.md) 를 사용할 수 있습니다. 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 문제 해결 페이지를 확인 해야 합니다.

## <a name="comments-welcome"></a>시작 설명

자습서에 대 한 의견을 기다리겠습니다를 하 고 자습서가 업데이트 되 면 노력 됩니다 계정 수정 또는 제안 자습서 주석에서 제공 되는 향상 된 기능에 대 한 야 합니다.

<a id="prerequisites"></a>

## <a name="prerequisites"></a>전제 조건

이 자습서는 다음 제품에 대 한 작성 했습니다.

- Windows 8 또는 Windows 7입니다.
- Visual Studio 2012 또는 Visual Studio 2012 Express for Web [최신 업데이트](https://go.microsoft.com/fwlink/?LinkId=272486)합니다.
- [Azure SDK for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=254364)

Visual Studio 2010 SP1 또는 Visual Studio 2013을 사용 하 여 자습서를 따를 수 있습니다 하지만 일부 스크린 샷은 달라질 수 있으며 일부 기능은 달라 집니다.

Visual Studio 2013을 사용 하는 경우 설치 [Visual Studio 2013 용 Azure SDK](https://go.microsoft.com/fwlink/?LinkID=324322)합니다.

Visual Studio 2010 SP1을 사용 하는 경우에 다음 소프트웨어를 설치 합니다.

- [Azure SDK for Visual Studio 2010](https://go.microsoft.com/fwlink/?LinkID=254269)
- [SQL Server Express LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=SQLLocalDBOnly_11_0)
- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh500335.aspx)합니다.

SDK 종속성 수에 이미 있는 컴퓨터에 따라 Azure SDK를 설치 하면 몇 분 30 분 이상에서 시간이 오래 걸릴 수 있습니다. Azure로 대신 타사 호스팅 공급자에 게시 SDK에는 Visual Studio 웹의 최신 업데이트가 포함 되어 있으므로 게시 기능을 계획 하는 경우에 Azure SDK가 필요 합니다.

> [!NOTE]
> 이 자습서는 Azure SDK의 버전 1.8.1 사용 하 여 작성 되었습니다. 그 후 추가 기능을 사용 하 여 최신 버전 출시 되었습니다. 이러한 기능 및 리소스에 대 한 자세한 정보가 있는 링크를 언급 하는 자습서 업데이트 되었습니다.


지침과 스크린샷은 Windows 8 기반으로 하지만 Windows 7에 대 한 차이점을 설명 하는 자습서입니다.

자습서를 완료 하는 데 필요한 다른 소프트웨어도 하지만 아직 설치를 할 필요가 없습니다. 이 자습서는 필요할 때 설치에 대 한 단계를 안내 합니다.

## <a name="download-the-sample-application"></a>샘플 응용 프로그램 다운로드

배포할 응용 프로그램은 Contoso University,를 이미 만들었습니다. 에 설명 된 Contoso University 응용 프로그램을 느슨하게 기반 대학 웹 사이트의 단순화 된 버전의 [ASP.NET 사이트의 Entity Framework 자습서](https://asp.net/entity-framework/tutorials)합니다.

설치 필수 구성 요소에 있는 경우 다운로드 합니다 [Contoso University 웹 응용 프로그램](https://go.microsoft.com/fwlink/p/?LinkId=282627)합니다. 합니다 *.zip* 파일 프로젝트의 여러 버전을 포함 합니다. 자습서의 단계를 진행 하려면 C# 폴더에 있는 프로젝트를 시작 합니다. 프로젝트의 모양은 자습서의 끝을 확인 하려면 ContosoUniversity 엔드 폴더에 프로젝트를 엽니다.

자습서 단계를 통해 작업에 대 한 프로젝트를 준비 하려면 다음 단계를 수행 합니다.

1. Visual Studio 프로젝트를 사용 하 여 작업에 대 한 사용 중인 모든 폴더에서 ContosoUniversity 라는 폴더에 C# 폴더에서 ContosoUniversity 솔루션 파일을 저장 합니다.

    기본적으로이 Visual Studio 2012에 대 한 다음 폴더입니다.

    `C:\Users\<username>\Documents\Visual Studio 2012\Projects`

    (이 자습서에서 스크린샷, 프로젝트 폴더는 루트 디렉터리에서에 있습니다는 `C`: 드라이브입니다.)
2. Visual Studio를 시작 하 고 프로젝트를 엽니다.
3. **솔루션 탐색기**솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **EnableNuGet 패키지 복원**합니다.
4. 솔루션을 빌드합니다.
5. 컴파일 오류를 받게 되 면 NuGet 패키지를 수동으로 복원 합니다.

    1. **솔루션 탐색기**솔루션을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **솔루션용 NuGet 패키지 관리**합니다.
    2. 맨 위에 있는 **NuGet 패키지 관리** 대화 상자 표시 **일부 NuGet 패키지는이 솔루션에 없습니다. 복원 하려면 클릭 합니다.** 클릭 합니다 **복원** 단추입니다.
    3. 솔루션을 다시 빌드합니다.
6. CTRL-F5 키를 눌러 응용 프로그램을 실행 합니다.

    응용 프로그램이 Contoso University 홈페이지를 엽니다.

    ![홈 페이지 개발](introduction/_static/image1.png)

    (Visual Studio SQL Server Express LocalDB 인스턴스를 시작 하는 동안 대기 시간을 수 있으며 오류가 발생할 수 있습니다는 제한 시간 경우 너무 오래 걸리는 프로세스입니다. 만 경우에서 프로젝트를 다시 시작합니다.)

웹 사이트 페이지의 메뉴 모음에서 액세스할 수 있으며 다음 기능을 수행할 수 있습니다.

- 학생 통계 (About 페이지)를 표시 합니다.
- 표시, 편집, 삭제 및 학생을 추가 합니다.
- 표시 및 편집 과정입니다.
- 표시 및 편집 강사입니다.
- 표시 하 고 부서를 편집 합니다.

다음은 몇 가지 대표적인 페이지의 스크린샷.

![학생 개발자 페이지](introduction/_static/image2.png)

![학생 페이지 개발자 추가](introduction/_static/image3.png)

## <a name="review-application-features-that-affect-deployment"></a>배포에 영향을 주는 응용 프로그램 기능 검토

응용 프로그램의 다음 기능 배포 하기 위해 수행 해야 하거나 배포 하는 방법에 영향을 줍니다. 이러한 각 시리즈의 다음 자습서에서 자세히 설명 되어 있습니다.

- Contoso University student 및 instructor 이름과 같은 응용 프로그램 데이터를 저장 하는 SQL Server 데이터베이스를 사용 합니다. 데이터베이스 테스트 데이터와 프로덕션 데이터의 조합에 포함 하 고 테스트 데이터를 제외 해야 하는 프로덕션에 배포할 때.
- SQL Server 데이터베이스에서 사용자 계정 정보를 저장 하는 ASP.NET 멤버 자격 시스템을 사용 하는 응용 프로그램입니다. 응용 프로그램 몇 가지 제한 된 정보에 대 한 액세스 권한이 있는 사용자는 관리자 사용자를 정의 합니다. 관리자 계정으로 테스트 계정이 없지만 멤버 자격 데이터베이스를 배포 해야 합니다.
- 응용 프로그램을 타사 오류 로깅 및 보고 유틸리티를 사용 합니다. 이 유틸리티는 응용 프로그램과 함께 배포 해야 하는 어셈블리에서 제공 됩니다.
- 오류 로깅 유틸리티 파일 폴더에 XML 파일에서 오류 정보를 씁니다. 배포에서이 폴더를 제외 해야 하에 배포 된 사이트의 ASP.NET에서 실행 되는 계정이이 폴더에 대 한 쓰기 권한이 있는지 확인 해야 합니다. (그렇지 않으면 테스트 환경에서 오류 로그 데이터를 프로덕션에 배포할 수 있습니다 및/또는 프로덕션 오류 로그 파일을 삭제 될 수 있습니다.)
- 응용 프로그램에 일부 설정을 변경 해야 하는 배포에 *Web.config* 대상 환경 (테스트, 준비 또는 프로덕션) 및 빌드에 따라 변경 해야 하는 다른 설정에 따라 파일 (디버그 또는 릴리스)를 구성 합니다.
- Visual Studio 솔루션에 클래스 라이브러리 프로젝트를 포함합니다. 이 프로젝트를 생성 하는 어셈블리에만 배포 프로젝트 자체입니다.

## <a name="summary"></a>요약

이 시리즈의 첫 번째 자습서에서는 샘플 Visual Studio 프로젝트를 다운로드 하 고 응용 프로그램을 배포 하는 방법에 영향을 주는 사이트 기능을 검토 합니다. 다음 자습서에서는 자동으로 처리할 이들 중 일부를 설정 하 여 배포를 위해 준비할 수 있습니다. 다른 수동으로 처리 있습니다.

> [!div class="step-by-step"]
> [다음](preparing-databases.md)
