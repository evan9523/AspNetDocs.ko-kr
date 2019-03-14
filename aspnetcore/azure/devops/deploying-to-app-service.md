---
title: App Service-ASP.NET Core 및 Azure를 사용 하 여 DevOps에 앱 배포
author: CamSoper
description: Azure App service에 ASP.NET Core 및 Azure를 사용 하 여 DevOps에 대 한 첫 번째 단계는 ASP.NET Core 앱을 배포 합니다.
ms.author: casoper
ms.custom: mvc, seodec18
ms.date: 10/24/2018
uid: azure/devops/deploy-to-app-service
ms.openlocfilehash: 9fe17c9e210d4dda9b74818104fc52a60d4f0077
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056560"
---
# <a name="deploy-an-app-to-app-service"></a>App Service에 앱 배포

[Azure App Service](/azure/app-service/) 는 Azure의 웹 호스팅 플랫폼입니다. 수동으로 또는 자동화 된 프로세스를 통해 Azure App Service에 웹 앱 배포를 수행할 수 있습니다. 이 가이드의이 섹션에서는 명령줄을 사용 하 여 스크립트 하거나 수동으로 트리거할 수 있습니다 또는 Visual Studio를 사용 하 여 수동으로 트리거되는 배포 방법을 설명 합니다.

이 섹션에서는 다음 작업을 수행할 수 있습니다.

* 다운로드 하 고 샘플 앱을 빌드하십시오.
* Azure Cloud Shell을 사용 하 여 Azure App Service 웹 앱을 만듭니다.
* Git를 사용 하 여 Azure에 샘플 앱을 배포 합니다.
* Visual Studio를 사용 하 여 앱에는 변경 내용을 배포 합니다.
* 웹 앱에 스테이징 슬롯을 추가 합니다.
* 스테이징 슬롯에 업데이트를 배포 합니다.
* 스테이징 및 프로덕션 슬롯을 교환 합니다.

## <a name="download-and-test-the-app"></a>다운로드 하 여 앱 테스트

이 가이드에 사용 되는 앱은 ASP.NET Core 앱을 미리 빌드된 [간단한 피드 판독기](https://github.com/Azure-Samples/simple-feed-reader/)합니다. Razor 페이지 앱을 사용 하는 것은 `Microsoft.SyndicationFeed.ReaderWriter` API RSS/Atom 피드를 검색 하 고 목록에서 뉴스 항목을 표시 합니다.

코드 검토를 자유롭게 이지만이 앱에 대 한 특별 임을 이해 해야 합니다. 설명을 위해 간단한 ASP.NET Core 앱만 됩니다.

명령 셸에서 코드를 다운로드할 프로젝트를 빌드하고 다음과 같이 실행 합니다.

> *참고: Linux/macOS 사용자는 적절 하 게 변경 경로 대 한 예를 들어, 앞에 슬래시를 사용 하 여 (`/`) 대신 백슬래시 (`\`).*

1. 로컬 컴퓨터의 폴더로 코드를 복제 합니다.

    ```console
    git clone https://github.com/Azure-Samples/simple-feed-reader/
    ```

2. 작업 폴더를 변경 합니다 *단순 피드 판독기* 만들어진 폴더입니다.

    ```console
    cd .\simple-feed-reader\SimpleFeedReader
    ```

3. 패키지를 복원 하 고 솔루션을 빌드하십시오.

    ```console
    dotnet build
    ```

4. 앱을 실행합니다.

    ```console
    dotnet run
    ```

    ![Dotnet run 명령에 성공](./media/deploying-to-app-service/dotnet-run.png)

5. 브라우저를 열고 이동할 `http://localhost:5000`합니다. 앱 입력 하거나 배포 피드 URL을 붙여 넣을 수 있으며 뉴스 항목 목록을 봅니다.

     ![RSS 피드의 내용을 표시 하는 앱](./media/deploying-to-app-service/app-in-browser.png)

6. 앱이 올바르게 작동 만족 했으면, 눌러 종료할 **Ctrl**+**C** 명령 셸에서 합니다.

## <a name="create-the-azure-app-service-web-app"></a>Azure App Service 웹 앱 만들기

앱을 배포 하려면 App Service 만들기 해야 [웹 앱](/azure/app-service/app-service-web-overview)합니다. 웹 앱을 만든 후 Git를 사용 하 여 로컬 컴퓨터에서를 배포할 수 있습니다.

1. 에 로그인 합니다 [Azure Cloud Shell](https://shell.azure.com/bash)합니다. 참고: 처음으로 로그인 할 때 Cloud Shell은 구성 파일에 대 한 저장소 계정을 만들려면 요구 합니다. 기본값을 사용 하거나 고유 이름을 제공 합니다.

2. 다음 단계에서 Cloud Shell을 사용 합니다.

    a. 웹 앱의 이름을 저장할 변수를 선언 합니다. 이름을 기본 URL에 사용할 고유 해야 합니다. 사용 하는 `$RANDOM` Bash 함수 이름을 생성 하는 고유성을 보장 및 형식으로 결과 `webappname99999`합니다.

    ```console
    webappname=mywebapp$RANDOM
    ```

    b. 리소스 그룹을 만듭니다. 리소스 그룹을 그룹으로 관리 하는 Azure 리소스를 집계 하는 수단을 제공 합니다.

    ```azure-cli
    az group create --location centralus --name AzureTutorial
    ```

    합니다 `az` 명령을 호출 합니다 [Azure CLI](/cli/azure/)합니다. CLI를 로컬로 실행할 수 있지만 시간 및 구성 저장 사용 하 여 Cloud Shell에서.

    다. S1 계층에서 App Service 계획을 만듭니다. App Service 계획은 동일한 가격 책정 계층을 공유 하는 웹 앱의 그룹입니다. S1 계층을 무료로 사용할 수 있는 없지만 스테이징 슬롯 기능 필요 합니다.

    ```azure-cli
    az appservice plan create --name $webappname --resource-group AzureTutorial --sku S1
    ```

    d. App Service 계획을 사용 하 여 동일한 리소스 그룹에서 웹 앱 리소스를 만듭니다.

    ```azure-cli
    az webapp create --name $webappname --resource-group AzureTutorial --plan $webappname
    ```

    e. 배포 자격 증명을 설정 합니다. 이러한 배포 자격 증명은 구독에서 모든 웹 앱에 적용 됩니다. 사용자 이름에 특수 문자를 사용 하지 마세요.

    ```azure-cli
    az webapp deployment user set --user-name REPLACE_WITH_USER_NAME --password REPLACE_WITH_PASSWORD
    ```

    f. 로컬 Git에서 표시 하는 배포를 허용 하도록 웹 앱을 구성 합니다 *Git 배포 URL*합니다. **나중에 참조에 대 한 url이**합니다.

    ```azure-cli
    echo Git deployment URL: $(az webapp deployment source config-local-git --name $webappname --resource-group AzureTutorial --query url --output tsv)
    ```

    g. 표시 된 *웹 앱 URL*합니다. 빈 웹 앱을 보려면이 URL로 이동 합니다. **나중에 참조에 대 한 url이**합니다.

    ```console
    echo Web app URL: http://$webappname.azurewebsites.net
    ```

3. 명령 셸에서 사용 하 여 로컬 컴퓨터에 웹 앱의 프로젝트 폴더를 이동 (예를 들어 `.\simple-feed-reader\SimpleFeedReader`). Git 배포 URL을 푸시 하도록 설정 하려면 다음 명령을 실행 합니다.

    a. 로컬 리포지토리에 원격 URL을 추가 합니다.

    ```console
    git remote add azure-prod GIT_DEPLOYMENT_URL
    ```

    b. 로컬 푸시 *마스터* 분기를 *azure prod* 원격의 *마스터* 분기 합니다.

    ```console
    git push azure-prod master
    ```

    이전에 만든 배포 자격 증명에 대 한 라는 메시지가 표시 됩니다. 명령 셸에서 출력을 관찰 합니다. Azure는 원격으로 ASP.NET Core 앱을 빌드합니다.

4. 브라우저에서로 이동 합니다 *웹 앱 URL* 앱이 빌드 및 배포를 확인 합니다. 추가 변경 내용을 사용 하 여 로컬 Git 리포지토리에 커밋할 수 `git commit`입니다. 앞으로 이러한 변경 내용을 Azure로 푸시할 `git push` 명령입니다.

## <a name="deployment-with-visual-studio"></a>Visual Studio 사용 하 여 배포

> *참고: 이 섹션에서는 Windows에만 적용 됩니다. Linux 및 macOS 사용자는 2 단계 아래에 설명 된 변경 내용을 확인 해야 합니다. 파일을 저장 하 고 사용 하 여 로컬 리포지토리에 변경 내용을 커밋하기 `git commit`합니다. 마지막으로 사용 하 여 변경 내용을 푸시 `git push`첫 번째 섹션 에서처럼 합니다.*

앱 명령 셸에서 이미 배포 되었습니다. 앱에 업데이트를 배포 하려면 Visual Studio의 통합된 도구를 사용해 보겠습니다. 배후에서 Visual Studio 도구, 명령줄 같지만 Visual Studio의 친숙 한 UI 내에서 동일한 작업을 수행 합니다.

1. 오픈 *SimpleFeedReader.sln* Visual Studio에서.
2. 솔루션 탐색기에서 엽니다 *Pages\Index.cshtml*합니다. 변경 `<h2>Simple Feed Reader</h2>` 에 `<h2>Simple Feed Reader - V2</h2>`입니다.
3. 키를 눌러 **Ctrl**+**Shift**+**B** 앱을 빌드할 수 있습니다.
4. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.

    ![마우스 오른쪽 단추로 클릭, 게시를 보여 주는 스크린샷](./media/deploying-to-app-service/publish.png)
5. Visual Studio에서 새 App Service 리소스를 만들 수 있지만이 업데이트는 기존 배포를 통해 게시 될 예정입니다. 에 **게시 대상 선택** 대화 상자에서 **App Service** 왼쪽에 있는 목록에서 선택한 후 **기존 선택**합니다. **게시**를 클릭합니다.
6. 에 **App Service** 대화 상자에서 Microsoft 또는 조직 계정을 Azure 구독을 만드는 데 오른쪽 위에 표시 되는지 확인 합니다. 없는 경우 드롭다운을 클릭 하 고 추가 합니다.
7. 확인 하는 올바른 Azure **구독** 을 선택 합니다. 에 대 한 **뷰**를 선택 **리소스 그룹**합니다. 확장 된 **AzureTutorial** 리소스 그룹 및 기존 웹 앱을 선택 합니다. **확인**을 클릭합니다.

    ![App Service 게시 대화 상자 보여 주는 스크린샷](./media/deploying-to-app-service/publish-dialog.png)

Visual Studio 빌드하고 Azure에 앱을 배포 합니다. 웹 앱 URL로 이동 합니다. 확인 된 `<h2>` 요소를 수정 하는 라이브입니다.

![변경 된 제목이 있는 앱](./media/deploying-to-app-service/app-v2.png)

## <a name="deployment-slots"></a>배포 슬롯

배포 슬롯 프로덕션 환경에서 실행 되는 앱에 영향을 주지 않고 변경 내용 스테이징을 지원 합니다. 준비 된 버전의 앱 품질 보증 팀에서 유효성이 검사 되 면 프로덕션 및 스테이징 슬롯을 교환할 수 있습니다. 준비 단계에서 앱이 방식으로 프로덕션으로 승격 됩니다. 스테이징 슬롯을 만들고, 일부 변경 내용을 배포 확인 후 프로덕션과 스테이징 슬롯을 교환 하는 다음 단계를 합니다.

1. 에 로그인 합니다 [Azure Cloud Shell](https://shell.azure.com/bash)아직 로그인 하지 않은 경우.
2. 스테이징 슬롯을 만듭니다.

    a. 이름의 배포 슬롯을 만듭니다 *준비*합니다.

    ```azure-cli
    az webapp deployment slot create --name $webappname --resource-group AzureTutorial --slot staging
    ```

    b. 로컬 Git 및 get에서 배포를 사용 하려면 스테이징 슬롯을 구성 합니다 **준비** 배포 URL입니다. **나중에 참조에 대 한 url이**합니다.

    ```azure-cli
    echo Git deployment URL for staging: $(az webapp deployment source config-local-git --name $webappname --resource-group AzureTutorial --slot staging --query url --output tsv)
    ```

    다. 스테이징 슬롯의 URL을 표시 합니다. 빈 스테이징 슬롯을 확인 하려면 URL로 이동 합니다. **나중에 참조에 대 한 url이**합니다.

    ```console
    echo Staging web app URL: http://$webappname-staging.azurewebsites.net
    ```

3. 텍스트 편집기 또는 Visual Studio에서 수정할 *pages/Index.cshtml* 다시 되도록 합니다 `<h2>` 요소를 읽습니다 `<h2>Simple Feed Reader - V3</h2>` 파일을 저장 합니다.

4. 파일 중 하나를 사용 하 여 로컬 Git 리포지토리에 커밋 합니다 **변경 내용을** Visual studio의 페이지 *팀 탐색기* 탭을 입력 하 여 다음 셸을 사용 하 여 로컬 컴퓨터의 명령 또는:

    ```console
    git commit -a -m "upgraded to V3"
    ```
5. 로컬 컴퓨터의 명령 셸 사용, Git 원격으로 스테이징 배포 URL을 추가 하 고 커밋된 변경 내용을 푸시하십시오.

    a. 로컬 Git 리포지토리를 스테이징에 대 한 원격 URL을 추가 합니다.

    ```console
    git remote add azure-staging <Git_staging_deployment_URL>
    ```

    b. 로컬 푸시 *마스터* 분기를 *azure 스테이징* 원격의 *마스터* 분기 합니다.

    ```console
    git push azure-staging master
    ```

    Azure를 빌드하고 앱을 배포 하는 동안 기다립니다.

6. V3 스테이징 슬롯에 배포한 있는지를 확인 하려면 두 개의 브라우저 창을 엽니다. 하나의 창에서 원본 웹 앱 URL로 이동 합니다. 다른 창에서 스테이징 웹 앱 URL로 이동 합니다. 프로덕션 URL은 앱의 V2에 사용 됩니다. 스테이징 URL에는 앱의 V3 사용 됩니다.

    ![브라우저 창을 비교 스크린 샷](./media/deploying-to-app-service/ready-to-swap.png)

7. Cloud Shell에서 확인/준비 접속 스테이징 슬롯을 프로덕션으로 교환 합니다.

    ```azure-cli
    az webapp deployment slot swap --name $webappname --resource-group AzureTutorial --slot staging
    ```

8. 두 개의 브라우저 창을 새로 고쳐서 교환 발생 했음을 확인 합니다.

    ![교환 후 브라우저 창을 비교](./media/deploying-to-app-service/swapped.png)

## <a name="summary"></a>요약

이 섹션에서는 다음 작업을 완료 했습니다.

* 다운로드 하 고 샘플 앱을 작성 합니다.
* Azure Cloud Shell을 사용 하 여 Azure App Service 웹 앱을 생성 합니다.
* Git를 사용 하 여 Azure에 샘플 앱을 배포 합니다.
* Visual Studio를 사용 하 여 앱에 변경 내용을 배포 합니다.
* 웹 앱에 스테이징 슬롯을 추가 합니다.
* 스테이징 슬롯에 대 한 업데이트를 배포합니다.
* 스테이징 및 프로덕션 슬롯을 교환 합니다.

다음 섹션에서는 Azure 파이프라인을 사용 하 여 DevOps 파이프라인을 빌드하는 방법에 알아봅니다.

## <a name="additional-reading"></a>추가 참조 항목

* [Web Apps 개요](/azure/app-service/app-service-web-overview)
* [Azure App Service에서.NET Core 및 SQL Database 웹 앱 빌드](/azure/app-service/app-service-web-tutorial-dotnetcore-sqldb)
* [Azure App Service에 대 한 배포 자격 증명을 구성 합니다.](/azure/app-service/app-service-deployment-credentials)
* [Azure App Service에서 스테이징 환경 설정](/azure/app-service/web-sites-staged-publishing)
