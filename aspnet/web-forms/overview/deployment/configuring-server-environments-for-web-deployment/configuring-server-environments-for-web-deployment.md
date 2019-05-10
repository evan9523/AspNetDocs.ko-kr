---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: 웹 배포용 서버 환경 구성 | Microsoft Docs
author: jrjlee
description: 이 자습서에서는 한 번의 클릭 또는 자동화 된 지원, 웹 사이트 배포 및 다양 한 다른 시나리오에는 게시 서버 환경을 설정 하는 방법을 보여 줍니다...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 073161ce4faa3b7ba6749d7dfbaa5309eeca4f74
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130691"
---
# <a name="configuring-server-environments-for-web-deployment"></a>웹 배포용 서버 환경 구성

[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서에서는 한 번의 클릭 또는 자동화 된 지원, 웹 사이트 배포 및 다양 한 다른 시나리오에서 게시 서버 환경을 설정 하는 방법을 보여줍니다. 자습서에는 특정 방법 wff (웹 팜 프레임 워크) 서버 팜에 제공 하는 시나리오 기반 개요와 함께 설정 및 배포를 지원 하도록 웹 서버를 구성 하는 등 다양 한 작업을 완료 하는 과정을 안내 하는 항목이 포함 되어 있습니다. 더 높은 수준의 엔드-투-엔드 지침입니다.
> 
> 자습서에 설명 된 Fabrikam, Inc. 배포 시나리오를 사용 하 여 [엔터프라이즈 웹 배포: 시나리오 개요](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) 예제 및 네트워크 인프라에 대 한 참조 지점으로 합니다.
> 
> 이 자습서의 번역을 이탈리아어를 방문 [ http://www.lucamorelli.it ](http://www.lucamorelli.it)합니다.

이 자습서는 이러한 항목이 포함 되어 있습니다.

- [웹 배포에 적합한 접근 방식 선택](choosing-the-right-approach-to-web-deployment.md)
- [시나리오: 웹 배포용 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)
- [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)
- [웹 배포 게시용 웹 서버 구성(원격 에이전트)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [웹 배포 게시용 웹 서버 구성(웹 배포 처리기)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [웹 배포 게시용 웹 서버 구성(오프라인 배포)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [웹 배포 게시용 데이터베이스 서버 구성](configuring-a-database-server-for-web-deploy-publishing.md)
- [웹 팜 프레임워크를 사용하여 서버 팜 만들기](creating-a-server-farm-with-the-web-farm-framework.md)
- [대상 환경의 배포 속성 구성](configuring-deployment-properties-for-a-target-environment.md)

첫 번째 항목인 [웹 배포에 오른쪽 접근 방식을 선택](choosing-the-right-approach-to-web-deployment.md), 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 웹 응용 프로그램을 게시 하 여 기본 방법에 설명 2.0. 또한 각 접근 방식에 매핑되는 시나리오를 식별 합니다. 여기에서 각 시나리오 항목을 완료 하는 데 필요한 작업의 대략적인 개요를 제공 하 고 이러한 작업을 완료할 수 있도록 진행 해야 하는 항목을 식별 합니다.

에 설명 된 분할 프로젝트 파일 방법을 사용 하는 경우 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md) 를 최종 항목에 솔루션을 빌드하여 배포 [대상환경에대한배포속성구성](configuring-deployment-properties-for-a-target-environment.md), 다른 대상 환경에 배포에 대 한 환경 관련 프로젝트 파일을 구성 하는 방법에 설명 합니다.

## <a name="key-technologies"></a>핵심 기술

이 자습서는 웹 배포를 지원 하기 위해 이러한 제품과 기술을 사용 하는 방법에 중점을 둡니다.

- IIS 7.5
- 웹 배포 2.x
- WFF 2.x
- IIS 웹 관리 서비스 (WMSvc)

Windows Server 2008 R2, SQL Server 2008 R2, ASP.NET 4.0 및 ASP.NET MVC 3의 사용에 관한 자습서도 살펴봅니다.

## <a name="other-tutorials-in-this-series"></a>이 시리즈의 다른 자습서

이 엔터프라이즈급 웹 배포에서 다섯 개의 자습서 시리즈의 일부를 형성합니다. 다른 자습서 시리즈의은 다음과 같습니다.

- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)합니다. 이 소개 콘텐츠 자습서 시리즈에 대 한 상황에 맞는 배경 정보를 제공 합니다. 자습서 시나리오를 설명 하 고 작업 및 연습 시리즈 전반에 설명 되어 광범위 한 응용 프로그램 수명 주기 관리 (ALM) 프로세스에 적합 하는 방법을 보여 줍니다.
- [엔터프라이즈 배포에서에서 웹](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다. 이 자습서는 Microsoft Build Engine (MSBuild) 프로젝트 파일에 대 한 개념 소개, 웹 게시 파이프라인, 웹 배포 및 기타 관련된 기술을 제공합니다. 사용 하는 방법을 이러한 도구 함께 복잡 한 배포 프로세스를 관리 하려면 설명 합니다.
- [웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다. 이 자습서에서는 Team Foundation Server (TFS) 배포 특정 빌드의 수동 트리거 및 CI (지속적인 통합) 프로세스의 일부로 자동화 된 배포를 포함 하 여 다양 한 배포 시나리오를 지원 하도록 구성 하는 방법을 설명 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)합니다. 이 자습서에서는 사용자 지정 된 여러 환경에 대 한 데이터베이스 배포, 배포에서 파일 및 폴더 제외 하 고, 배포 프로세스 중 웹 응용 프로그램을 오프 라인 등 다양 한 고급 배포 작업을 수행 하는 방법 설명 .

> [!div class="step-by-step"]
> [다음](choosing-the-right-approach-to-web-deployment.md)
