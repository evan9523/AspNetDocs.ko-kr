---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: '페이스 북, 트위터, 링크드 인과 구글 OAuth2 로그인 (C #)와 MVC 5 응용 프로그램을 만들기 | 마이크로 소프트 문서'
author: Rick-Anderson
description: 이 자습서에서는 사용자가 외부 authenti의 자격 증명으로 OAuth 2.0을 사용하여 로그인할 수 있는 ASP.NET MVC 5 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675918"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="8bc4a-103">Facebook, Twitter, LinkedIn 및 Google OAuth2 로그온을 제공하는 ASP.NET MVC 5 앱 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="8bc4a-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="8bc4a-104">로 [릭 앤더슨](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8bc4a-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="8bc4a-105">이 자습서에서는 사용자가 [OAuth 2.0을](http://oauth.net/2/) 사용하여 Facebook, Twitter, LinkedIn, Microsoft 또는 Google과 같은 외부 인증 공급자의 자격 증명을 사용하여 로그인할 수 있는 ASP.NET MVC 5 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="8bc4a-106">간단히 하기 위해 이 자습서에서는 Facebook 및 Google의 자격 증명 작업에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="8bc4a-107">수백만 명의 사용자가 이미 이러한 외부 공급자와 계정을 가지고 있기 때문에 웹 사이트에서 이러한 자격 증명을 사용하도록 설정하면 상당한 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="8bc4a-108">이러한 사용자는 새 자격 증명 집합을 만들고 기억할 필요가 없는 경우 사이트에 등록하는 경향이 더 높을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="8bc4a-109">또한 [ASP.NET SMS와 이메일 이중 인증과 MVC 5 응용 프로그램을](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="8bc4a-110">또한 이 자습서에서는 사용자에 대한 프로필 데이터를 추가하는 방법과 멤버 자격 API를 사용하여 역할을 추가하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="8bc4a-111">이 튜토리얼은 [릭 앤더슨에](https://blogs.msdn.com/rickAndy) 의해 작성되었습니다 [@RickAndMSFT](https://twitter.com/RickAndMSFT) (트위터에 저를 따르십시오 : ).</span><span class="sxs-lookup"><span data-stu-id="8bc4a-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="8bc4a-112">시작하기</span><span class="sxs-lookup"><span data-stu-id="8bc4a-112">Getting Started</span></span>

<span data-ttu-id="8bc4a-113">웹 또는 비주얼 [스튜디오 2013에 대한 Visual Studio Express](https://go.microsoft.com/fwlink/?LinkId=299058) [2013을](https://go.microsoft.com/fwlink/?LinkId=306566)설치하고 실행하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="8bc4a-114">비주얼 스튜디오 [2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390521) 이상 설치.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="8bc4a-115">드롭 박스, GitHub, 링크드 인, 인스 타 그램, 버퍼, 세일즈 포스, 스팀, 스택 교환, Tripit, 트위치, 트위터, 야후!에 대한 도움말, 이 [샘플 프로젝트를](https://github.com/matthewdunsdon/oauthforaspnet)참조하십시오 .</span><span class="sxs-lookup"><span data-stu-id="8bc4a-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="8bc4a-116">Google OAuth 2를 사용하고 SSL 경고 없이 로컬로 디버깅하려면 Visual Studio [2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390521) 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="8bc4a-117">**시작** 페이지에서 **새 프로젝트를** 클릭하거나 메뉴를 사용하여 **파일**을 선택한 다음 **새 프로젝트를**선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="8bc4a-118">첫 번째 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="8bc4a-118">Creating Your First Application</span></span>

<span data-ttu-id="8bc4a-119">**새 프로젝트를**클릭한 다음 왼쪽에서 **시각적 C#을** 선택한 다음 **웹을** 선택한 다음 **웹 응용 프로그램을 ASP.NET**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="8bc4a-120">프로젝트 이름을 "MvcAuth"로 지정한 다음 **확인을**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="8bc4a-121">새 **ASP.NET 프로젝트** 대화 상자에서 **MVC를**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="8bc4a-122">인증이 개별 **사용자 계정이**아닌 경우 **인증 변경** 단추를 클릭하고 개별 **사용자 계정을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="8bc4a-123">**클라우드에서 호스트를**선택하면 앱이 Azure에서 호스팅하기가 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="8bc4a-124">**클라우드에서 호스트를**선택한 경우 구성 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="8bc4a-125">NuGet을 사용하여 최신 OWIN 미들웨어로 업데이트</span><span class="sxs-lookup"><span data-stu-id="8bc4a-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="8bc4a-126">NuGet 패키지 관리자를 사용하여 [OWIN 미들웨어를](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="8bc4a-127">왼쪽 메뉴에서 **업데이트를** 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="8bc4a-128">**모든 업데이트** 단추를 클릭하거나 OWIN 패키지만 검색할 수 있습니다(다음 이미지에 표시됨).</span><span class="sxs-lookup"><span data-stu-id="8bc4a-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="8bc4a-129">아래 이미지에는 OWIN 패키지만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="8bc4a-130">PMC(패키지 관리자 콘솔)에서 모든 `Update-Package` 패키지를 업데이트하는 명령을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="8bc4a-131">응용 프로그램을 실행하려면 **F5** 또는 **Ctrl+F5를** 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="8bc4a-132">아래 이미지에서 포트 번호는 1234입니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="8bc4a-133">응용 프로그램을 실행하면 다른 포트 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="8bc4a-134">브라우저 창의 크기에 따라 탐색 아이콘을 클릭하여 **홈**, **정보**, **연락처,** **등록** 및 로그인 링크를 확인해야 **할** 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="8bc4a-135">프로젝트에서 SSL 설정</span><span class="sxs-lookup"><span data-stu-id="8bc4a-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="8bc4a-136">구글과 페이스 북과 같은 인증 공급자에 연결하려면, 당신은 SSL을 사용하기 위해 IIS-익스프레스를 설정해야합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="8bc4a-137">로그인 후 SSL을 계속 사용하고 HTTP로 다시 드롭하지 않는 것이 중요하며, 로그인 쿠키는 사용자 이름과 암호와 마찬가지로 비밀이며 SSL을 사용하지 않고는 와이어를 통해 일반 텍스트로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="8bc4a-138">게다가 MVC 파이프라인이 실행되기 전에 이미 핸드셰이크를 수행하고 채널을 보호하는 데 시간이 걸렸기 때문에 MVC 파이프라인이 실행되기 전에 HTTP로 리디렉션하면 현재 요청이나 향후 요청이 훨씬 빨라지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="8bc4a-139">**솔루션 탐색기에서** **MvcAuth** 프로젝트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="8bc4a-140">F4 키를 누르고 프로젝트 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="8bc4a-141">또는 **보기** 메뉴에서 **속성 창을**선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="8bc4a-142">**SSL을** True로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="8bc4a-143">SSL URL을 복사합니다(다른 SSL 프로젝트를 만들지 `https://localhost:44300/` 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="8bc4a-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="8bc4a-144">**솔루션 탐색기에서** **MvcAuth** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="8bc4a-145">**웹** 탭을 선택한 다음 SSL URL을 **프로젝트 URL** 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="8bc4a-146">파일(Ctl+S)을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="8bc4a-147">페이스 북과 구글 인증 애플 리 케이 션을 구성 하려면이 URL이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="8bc4a-148">모든 요청이 HTTPS를 `Home` 사용해야 하도록 컨트롤러에 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="8bc4a-149">보다 안전한 방법은 응용 프로그램에 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 필터를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="8bc4a-150">내 자습서에서 SSL으로 응용 프로그램 &quot;보호&quot; 및 내 자습서에서 특성 권한 부여 섹션을 참조 하 고 인증 및 SQL DB를 사용 하 고 [Azure 앱 서비스에 배포 하는 ASP.NET MVC 응용 프로그램을 만듭니다.](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)</span><span class="sxs-lookup"><span data-stu-id="8bc4a-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="8bc4a-151">홈 컨트롤러의 일부가 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="8bc4a-152">Ctrl+F5를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="8bc4a-153">이전에 인증서를 설치한 경우 이 섹션의 나머지 부분을 건너뛰고 [OAuth 2용 Google 앱 만들기로 이동하여 앱을 프로젝트에 연결한](#goog)다음 지침에 따라 IIS Express에서 생성한 자체 서명된 인증서를 신뢰할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="8bc4a-154">보안 **경고** 대화 상자를 읽은 다음 localhost를 나타내는 인증서를 설치하려면 **예를** 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="8bc4a-155">IE에 *홈* 페이지가 표시되며 SSL 경고가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="8bc4a-156">구글 크롬은 또한 인증서를 수락하고 경고없이 HTTPS 콘텐츠를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="8bc4a-157">Firefox는 자체 인증서 저장소를 사용하므로 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="8bc4a-158">우리의 응용 프로그램을 위해 당신은 안전하게 **내가 위험을 이해**클릭 할 수 있습니다 .</span><span class="sxs-lookup"><span data-stu-id="8bc4a-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="8bc4a-159">OAuth 2용 Google 앱 만들기 및 앱 연결</span><span class="sxs-lookup"><span data-stu-id="8bc4a-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="8bc4a-160">현재 Google OAuth 지침은 [ASP.NET 코어에서 Google 인증 구성을](/aspnet/core/security/authentication/social/google-logins)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="8bc4a-161">[Google Developers Console](https://console.developers.google.com/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="8bc4a-162">이전에 프로젝트를 만들지 않은 경우 왼쪽 탭에서 **자격 증명을** 선택한 다음 을 **선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="8bc4a-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="8bc4a-163">왼쪽 탭에서 자격 증명 을 **클릭합니다.**</span><span class="sxs-lookup"><span data-stu-id="8bc4a-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="8bc4a-164">**자격 증명 만들기를** 클릭한 다음 **OAuth 클라이언트 ID**.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="8bc4a-165">클라이언트 **ID 만들기** 대화 상자에서 응용 프로그램 유형에 대한 기본 **웹 응용 프로그램을** 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="8bc4a-166">위에서 사용한 SSL URL로 **인증된 자바스크립트** `https://localhost:44300/` 출처를 설정합니다(다른 SSL 프로젝트를 만들지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="8bc4a-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="8bc4a-167">권한 **있는 리디렉션 URI를** 다음으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="8bc4a-168">OAuth 동의 화면 메뉴 항목을 클릭한 다음 이메일 주소와 제품 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="8bc4a-169">양식을 완료하면 **저장을**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="8bc4a-170">라이브러리 메뉴 항목을 클릭하고 **Google+ API를**검색한 다음 활성화를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="8bc4a-171">아래 이미지는 활성화된 API를 보여 주며, 이 에 대해 보여 주시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="8bc4a-172">Google API 관리자에서 **자격 증명** 탭을 방문하여 **클라이언트 ID를**가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="8bc4a-173">응용 프로그램 암호와 JSON 파일을 저장하려면 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="8bc4a-174">**ClientId** 및 **ClientSecret를** 복사하여 `UseGoogleAuthentication` *App_Start* 폴더의 *Startup.Auth.cs* 파일에 있는 메서드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="8bc4a-175">아래에 표시된 **ClientId** 및 **ClientSecret** 값은 샘플이며 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="8bc4a-176">보안 - 소스 코드에 중요한 데이터를 저장하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="8bc4a-177">계정 과 자격 증명은 샘플을 단순하게 유지하기 위해 위의 코드에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="8bc4a-178">[ASP.NET 및 Azure 앱 서비스에 암호 및 기타 중요한 데이터를 배포하는 모범 사례를](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="8bc4a-179">**CTRL+F5를** 눌러 응용 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="8bc4a-180">**로그인** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="8bc4a-181">**다른 서비스 사용에서 로그인하려면** **Google**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="8bc4a-182">위의 단계를 놓치면 HTTP 401 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="8bc4a-183">위의 단계를 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-183">Recheck your steps above.</span></span> <span data-ttu-id="8bc4a-184">필수 설정(예: 제품 **이름)을**놓친 경우 누락된 항목을 추가하고 저장합니다. 인증이 작동하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="8bc4a-185">자격 증명을 입력할 Google 사이트로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="8bc4a-186">자격 증명을 입력하면 방금 만든 웹 응용 프로그램에 대한 권한을 부여하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="8bc4a-187">**Accept**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-187">Click **Accept**.</span></span> <span data-ttu-id="8bc4a-188">이제 Google 계정을 등록할 수 있는 MvcAuth 응용 프로그램의 **등록** 페이지로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="8bc4a-189">Gmail 계정에 사용되는 로컬 전자 메일 등록 이름을 변경할 수 있지만 일반적으로 기본 전자 메일 별칭(즉, 인증에 사용하는 별칭)을 그대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="8bc4a-190">**등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="8bc4a-191">Facebook에서 앱을 만들고 앱에 연결</span><span class="sxs-lookup"><span data-stu-id="8bc4a-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="8bc4a-192">현재 페이스 북 OAuth2 인증 지침에 대 한, [참조 페이스 북 인증 구성](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="8bc4a-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="8bc4a-193">멤버십 데이터 검토</span><span class="sxs-lookup"><span data-stu-id="8bc4a-193">Examine the Membership Data</span></span>

<span data-ttu-id="8bc4a-194">**보기** 메뉴에서 **서버 탐색기를**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="8bc4a-195">**기본 연결(MvcAuth)을**확장하고 **테이블을**확장하고 **AspNetUsers를** 마우스 오른쪽 단추로 클릭하고 **테이블 데이터 표시를**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers 테이블 데이터](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="8bc4a-197">사용자 클래스에 프로필 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="8bc4a-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="8bc4a-198">이 섹션에서는 다음 이미지와 같이 등록 하는 동안 사용자 데이터에 생년일과 홈 타운을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![고향과 Bday와 레그](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="8bc4a-200">*Model\IdentityModels.cs* 파일을 열고 생년월일 및 홈 타운 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="8bc4a-201">*모델\AccountViewModels.cs* 파일 및 설정된 생년월일 `ExternalLoginConfirmationViewModel`및 홈 타운 속성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="8bc4a-202">*컨트롤러\AccountController.cs* 파일을 열고 그림과 같이 작업 메서드에서 `ExternalLoginConfirmation` 생년월일 및 홈 타운에 대한 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="8bc4a-203">*뷰\계정\ExternalLoginConfirm.cshtml* 파일에 생년월일 및 홈 타운 추가:</span><span class="sxs-lookup"><span data-stu-id="8bc4a-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="8bc4a-204">멤버십 데이터베이스를 삭제하여 애플리케이션에 Facebook 계정을 다시 등록하고 새 생년월일 및 홈타운 프로필 정보를 추가할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="8bc4a-205">**솔루션 탐색기에서** **모든 파일 표시** 아이콘을 클릭한 다음 데이터 *추가\aspnet-MvcAuth-\_&lt;dateStamp&gt;.mdf를* 마우스 오른쪽 버튼으로 클릭하고 **삭제를 클릭합니다.**</span><span class="sxs-lookup"><span data-stu-id="8bc4a-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="8bc4a-206">**도구** 메뉴에서 **NuGet 패키지 관리자를**클릭한 다음 **패키지 관리자 콘솔(PMC)을** 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="8bc4a-207">PMC에 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="8bc4a-208">마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="8bc4a-208">Enable-Migrations</span></span>
2. <span data-ttu-id="8bc4a-209">마이그레이션 추가 기능</span><span class="sxs-lookup"><span data-stu-id="8bc4a-209">Add-Migration Init</span></span>
3. <span data-ttu-id="8bc4a-210">업데이트-데이터베이스</span><span class="sxs-lookup"><span data-stu-id="8bc4a-210">Update-Database</span></span>

<span data-ttu-id="8bc4a-211">응용 프로그램을 실행하고 페이스 북과 구글을 사용하여 로그인하고 일부 사용자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="8bc4a-212">멤버십 데이터 검토</span><span class="sxs-lookup"><span data-stu-id="8bc4a-212">Examine the Membership Data</span></span>

<span data-ttu-id="8bc4a-213">**보기** 메뉴에서 **서버 탐색기를**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="8bc4a-214">**AspNetUsers를** 마우스 오른쪽 단추로 클릭하고 **테이블 데이터 표시를**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="8bc4a-215">`HomeTown` 및 `BirthDate` 필드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="8bc4a-216">앱 로그오프 및 다른 계정으로 로그인</span><span class="sxs-lookup"><span data-stu-id="8bc4a-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="8bc4a-217">Facebook을 사용하여 앱에 로그온한 다음 로그아웃한 다음 다른 Facebook 계정(동일한 브라우저 사용)으로 다시 로그인하려고 하면 사용한 이전 Facebook 계정에 즉시 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="8bc4a-218">다른 계정을 사용하려면 Facebook으로 이동하여 Facebook에서 로그아웃해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="8bc4a-219">다른 제3자 인증 공급자에게도 동일한 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="8bc4a-220">또는 다른 브라우저를 사용하여 다른 계정으로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bc4a-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8bc4a-221">Next Steps</span></span>

<span data-ttu-id="8bc4a-222">야후와 링크드 인 지침에 대한 제리 펠저에 의해 [OWIN에 대한 야후와 링크드 인 OAuth 보안 제공 업체소개를](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="8bc4a-223">ASP.NET MVC 5에 대한 Jerrie의 예쁜 소셜 로그인 버튼을 참조하여 소셜 로그인 버튼을 활성화하십시오.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="8bc4a-224">내 자습서를 따르십시오 [인증 및 SQL DB를 사용하여 ASP.NET MVC 앱을 만들고](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)이 자습서를 계속하고 다음을 보여 주어 Azure App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="8bc4a-225">Azure에 앱을 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="8bc4a-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="8bc4a-226">역할로 앱을 보호하는 방법.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="8bc4a-227">[RequireHttps를](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) 사용하여 앱을 보호하고 필터를 [인증하는](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) 방법.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="8bc4a-228">멤버 자격 API를 사용하여 사용자 및 역할을 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="8bc4a-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="8bc4a-229">이 튜토리얼을 좋아하는 방법과 우리가 개선 할 수있는 것에 대한 피드백을 남겨주세요.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="8bc4a-230">코드로 [어떻게 보여줄](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)때 새 주제를 요청할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="8bc4a-231">ASP.NET 추가할 새로운 기능을 요청하고 투표할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="8bc4a-232">예를 들어 사용자 및 역할을 만들고 관리하는 도구에 투표할 수 [있습니다.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="8bc4a-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="8bc4a-233">ASP.NET 외부 인증 서비스가 작동하는 방법에 대한 자세한 설명은 로버트 맥머레이의 [외부 인증 서비스를](https://asp.net/web-api/overview/security/external-authentication-services)참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="8bc4a-234">로버트의 기사는 또한 마이크로 소프트와 트위터 인증을 가능하게에 자세히 간다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="8bc4a-235">Tom Dykstra의 우수한 [EF/MVC 자습서에서는](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 엔터티 프레임워크를 사용하여 작업하는 방법을 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
