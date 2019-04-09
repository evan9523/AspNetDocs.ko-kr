---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 명령줄 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: c9aadec642837953dde4cf3e89ec9a7d484b380e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59401337"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="8315d-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 명령줄 배포</span><span class="sxs-lookup"><span data-stu-id="8315d-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>

<span data-ttu-id="8315d-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8315d-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="8315d-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="8315d-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="8315d-106">이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="8315d-107">시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="8315d-108">개요</span><span class="sxs-lookup"><span data-stu-id="8315d-108">Overview</span></span>

<span data-ttu-id="8315d-109">이 자습서는 Visual Studio 웹을 호출 하는 방법을 보여 줍니다. 명령줄에서 파이프라인을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="8315d-110">하려는 시나리오에 유용 [배포 프로세스를 자동화](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 것 수동으로 Visual Studio에서 작업을 수행 하는 대신 일반적으로 사용 하 여를 [소스 코드 버전 제어 시스템이](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="8315d-111">배포 변경</span><span class="sxs-lookup"><span data-stu-id="8315d-111">Make a change to deploy</span></span>

<span data-ttu-id="8315d-112">현재 정보 페이지 템플릿 코드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-112">Currently the About page displays the template code.</span></span>

![템플릿 코드를 사용 하 여 페이지에 대 한](command-line-deployment/_static/image1.png)

<span data-ttu-id="8315d-114">학생 등록의 요약을 표시 하는 코드를 사용 하 여는 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="8315d-115">열기는 *About.aspx* 페이지에서 모든 내부 태그를 삭제 합니다 `MainContent` `Content` 요소와 해당 위치에 다음 태그를 삽입:</span><span class="sxs-lookup"><span data-stu-id="8315d-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="8315d-116">프로젝트를 실행 하 고 선택 합니다 **에 대 한** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-116">Run the project and select the **About** page.</span></span>

![정보 페이지](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="8315d-118">명령줄을 사용 하 여 테스트 배포</span><span class="sxs-lookup"><span data-stu-id="8315d-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="8315d-119">다른 데이터베이스 변경, 따라서 사용 하지 않도록 설정 dbDacFx 데이터베이스 aspnet ContosoUniversity 데이터베이스 배포를 배포 하 고 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="8315d-120">열기는 **웹 게시** 마법사에 세 개의 각 게시 프로필을 선택 취소 합니다 **데이터베이스 업데이트** 확인란을 **설정** 탭.</span><span class="sxs-lookup"><span data-stu-id="8315d-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="8315d-121">Windows 8 시작 페이지에서 검색할 **VS2012 용 개발자 명령 프롬프트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="8315d-122">에 대 한 아이콘을 마우스 오른쪽 단추로 클릭 **VS2012 용 개발자 명령 프롬프트** 누릅니다 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="8315d-123">솔루션 파일의 경로 사용 하 여 솔루션 파일의 경로를 대체 명령 프롬프트에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="8315d-124">MSBuild는 솔루션을 빌드 및 테스트 환경에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![명령줄 출력](command-line-deployment/_static/image3.png)

<span data-ttu-id="8315d-126">브라우저를 열고 다음으로 이동 `http://localhost/ContosoUniversity`를 클릭 합니다 **에 대 한** 페이지 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="8315d-127">테스트에 학생이 있는지를 만들지를 보면 아래에서 빈 페이지는 **학생 본문 통계** 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="8315d-128">로 이동 합니다 **학생** 페이지에서 **학생 추가**, 학생이 몇 명 추가 및 돌아옵니다를 **에 대 한** 학생 통계를 보려면 페이지를 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![테스트 환경에서 페이지에 대 한](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="8315d-130">키 명령줄 옵션</span><span class="sxs-lookup"><span data-stu-id="8315d-130">Key command line options</span></span>

<span data-ttu-id="8315d-131">MSBuild에서 솔루션 파일 경로 및 두 개의 속성 전달할 입력 한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="8315d-132">개별 프로젝트를 배포 및 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="8315d-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="8315d-133">만들려는 솔루션에 하면 모든 프로젝트를 솔루션 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="8315d-134">여러 개의 웹 프로젝트가 솔루션에 있는 경우에 다음과 같은 MSBuild 동작이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="8315d-135">명령줄에서 지정 하는 속성은 모든 프로젝트에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="8315d-136">따라서 각 웹 프로젝트 게시 프로필을 지정 하는 이름이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="8315d-137">지정 하는 경우 `/p:PublishProfile=Test`, 각 웹 프로젝트 라는 게시 프로필이 있어야 *테스트*합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="8315d-138">다른 빌드되지도 하는 경우에 성공적으로 한 프로젝트를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="8315d-139">자세한 내용은 참조는 stackoverflow 스레드 [두 개의 패키지를 사용 하 여 MSBuild 실패](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="8315d-140">솔루션을 대신 개별 프로젝트를 지정 하는 경우 Visual Studio 버전을 지정 하는 매개 변수를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="8315d-141">Visual Studio 2012를 사용 하는 경우에 명령줄 다음 예제와 비슷한 것:</span><span class="sxs-lookup"><span data-stu-id="8315d-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="8315d-142">Visual Studio 2010에 대 한 버전 번호를은 10.0입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="8315d-143">자세한 내용은 [Visual Studio 프로젝트 호환성 및 VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) Sayed Hashimi의 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-143">For more information, see [Visual Studio project compatibility and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="8315d-144">게시 프로필을 지정</span><span class="sxs-lookup"><span data-stu-id="8315d-144">Specifying the publish profile</span></span>

<span data-ttu-id="8315d-145">이름 또는 전체 경로를 게시 프로필을 지정할 수 있습니다 합니다 *.pubxml* 다음 예제에서와 같이 파일:</span><span class="sxs-lookup"><span data-stu-id="8315d-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="8315d-146">웹 게시 명령줄 게시를 위해 지원 되는 메서드</span><span class="sxs-lookup"><span data-stu-id="8315d-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="8315d-147">메서드를 게시 하는 세 개의 명령줄 게시를 위해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-147">Three publish methods are supported for command line publishing:</span></span>

- `MSDeploy` <span data-ttu-id="8315d-148">웹 배포를 사용 하 여 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-148">- Publish by using Web Deploy.</span></span>
- `Package` <span data-ttu-id="8315d-149">웹 배포 패키지를 만들어 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-149">- Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="8315d-150">만든 MSBuild 명령에서 패키지를 별도로 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- `FileSystem` <span data-ttu-id="8315d-151">지정된 된 폴더에 파일을 복사 하 여 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-151">- Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="8315d-152">빌드 구성 및 플랫폼 지정</span><span class="sxs-lookup"><span data-stu-id="8315d-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="8315d-153">Visual Studio 또는 명령줄에서 빌드 구성 및 플랫폼 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="8315d-154">명명 된 속성을 포함 하는 게시 프로필 `LastUsedBuildConfiguration` 고 `LastUsedPlatform`, 있지만 프로젝트가 빌드되는 방식을 확인 하기 위해 이러한 속성을 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="8315d-155">자세한 내용은 [MSBuild: 구성 속성을 설정 하는 방법을](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) Sayed Hashimi의 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="8315d-156">스테이징에 배포</span><span class="sxs-lookup"><span data-stu-id="8315d-156">Deploy to staging</span></span>

<span data-ttu-id="8315d-157">Azure에 배포 하려면 명령줄에 암호를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="8315d-158">에 암호화 된 형태로 저장 된 Visual Studio에서 게시 프로필의 암호를 저장 하는 경우는 사용자 *. pubxml.user* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="8315d-159">해당 파일에서 명령줄 매개 변수에서 암호를 전달 해야 하므로 명령줄 배포를 수행할 때 MSBuild를 통해 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="8315d-160">필요한 암호를 복사 합니다 *.publishsettings* 스테이징 웹 사이트의 앞서 다운로드 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="8315d-161">암호는 값을 `userPWD` 웹 배포에 대 한 특성 `publishProfile` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![웹 배포 암호](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="8315d-163">Windows 8 시작 페이지에서 검색할 **VS2012 용 개발자 명령 프롬프트**, 명령 프롬프트를 열려면 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="8315d-164">(필요가 엽니다 관리자로이 이번 되므로 로컬 컴퓨터의 IIS에 배포 되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="8315d-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="8315d-165">솔루션 파일 및 암호를 사용 하 여 암호에 대 한 경로 사용 하 여 솔루션 파일의 경로를 대체 명령 프롬프트에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="8315d-166">이 명령줄에 추가 매개 변수를 포함 하는 알림: `/p:AllowUntrustedCertificate=true`합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="8315d-167">이 자습서가 작성 하는 대로 `AllowUntrustedCertificate` 명령줄에서 Azure에 게시할 때 속성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="8315d-168">이 버그에 대 한 수정이 릴리스되면 해당 매개 변수를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="8315d-169">브라우저를 열고 스테이징 사이트의 URL로 이동 하 고 클릭 합니다 **에 대 한** 페이지 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="8315d-170">테스트 환경에 대해 앞서 살펴본에서 통계를 보려면 학생이 몇 명 만들어야 할 수도 합니다 **에 대 한** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="8315d-171">프로덕션 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="8315d-171">Deploy to production</span></span>

<span data-ttu-id="8315d-172">프로덕션에 배포 하기 위한 프로세스는 스테이징에 대 한 프로세스와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="8315d-173">필요한 암호를 복사 합니다 *.publishsettings* 프로덕션 웹 사이트의 앞서 다운로드 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="8315d-174">오픈 **VS2012 용 개발자 명령 프롬프트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="8315d-175">솔루션 파일 및 암호를 사용 하 여 암호에 대 한 경로 사용 하 여 솔루션 파일의 경로를 대체 명령 프롬프트에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="8315d-176">실제 프로덕션 사이트에 대 한 데이터베이스 변경에도 발생 한 경우 일반적으로 복사 합니다 *앱\_offline.htm* 배포 하기 전에 사이트에 파일 및 성공적인 배포 후에 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="8315d-177">브라우저를 열고 스테이징 사이트의 URL로 이동 하 고 클릭 합니다 **에 대 한** 페이지 배포 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="8315d-178">요약</span><span class="sxs-lookup"><span data-stu-id="8315d-178">Summary</span></span>

<span data-ttu-id="8315d-179">이제 명령줄을 사용 하 여 응용 프로그램 업데이트를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-179">You have now deployed an application update by using the command line.</span></span>

![테스트 환경에서 페이지에 대 한](command-line-deployment/_static/image6.png)

<span data-ttu-id="8315d-181">다음 자습서에서는 웹을 확장 하는 방법의 예가 표시 됩니다 파이프라인을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="8315d-182">예제는 프로젝트에 포함 되지 않은 파일을 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8315d-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8315d-183">[이전](deploying-a-database-update.md)
> [다음](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="8315d-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
