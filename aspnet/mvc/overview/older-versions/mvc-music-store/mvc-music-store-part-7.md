---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: '7 부: 멤버 자격 및 권한 부여 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 7 부에서는 멤버 자격 및 권한 부여에 대해 설명 합니다.
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433469"
---
# <a name="part-7-membership-and-authorization"></a><span data-ttu-id="012d8-104">7 부: 멤버 자격 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="012d8-104">Part 7: Membership and Authorization</span></span>

<span data-ttu-id="012d8-105">받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )</span><span class="sxs-lookup"><span data-stu-id="012d8-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="012d8-106">MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="012d8-107">MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="012d8-108">이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="012d8-109">7 부에서는 멤버 자격 및 권한 부여에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-109">Part 7 covers Membership and Authorization.</span></span>

<span data-ttu-id="012d8-110">현재 스토어 관리자 컨트롤러는 사이트를 방문 하는 누구나 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="012d8-111">사이트 관리자에 대 한 사용 권한을 제한 하려면이를 변경해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="012d8-112">AccountController 및 Views 추가</span><span class="sxs-lookup"><span data-stu-id="012d8-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="012d8-113">전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿과 ASP.NET MVC 3 빈 웹 응용 프로그램 템플릿의 차이점 중 하나는 빈 템플릿에 계정 컨트롤러가 포함 되지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="012d8-114">전체 ASP.NET MVC 3 웹 응용 프로그램 템플릿에서 만든 새 ASP.NET MVC 응용 프로그램에서 몇 개의 파일을 복사 하 여 계정 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="012d8-115">Full ASP.NET MVC 3 웹 응용 프로그램 템플릿을 사용 하 여 새 ASP.NET MVC 응용 프로그램을 만들고 프로젝트의 동일한 디렉터리에 다음 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="012d8-116">Controller 디렉터리에 AccountController.cs 복사</span><span class="sxs-lookup"><span data-stu-id="012d8-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="012d8-117">모델 디렉터리에서 AccountModels 복사</span><span class="sxs-lookup"><span data-stu-id="012d8-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="012d8-118">Views 디렉터리 내에 계정 디렉터리를 만들고 다음 네 가지 보기를 모두 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="012d8-119">MvcMusicStore로 시작 되도록 컨트롤러 및 모델 클래스의 네임 스페이스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="012d8-120">AccountController 클래스는 MvcMusicStore 네임 스페이스를 사용 해야 하 고 Accountcontroller 클래스는 MvcMusicStore 네임 스페이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="012d8-121">*참고: 이러한 파일은 자습서의 시작 부분에서 사이트 디자인 파일을 복사한 MvcMusicStore-Assets 다운로드 에서도 사용할 수 있습니다. 멤버 자격 파일은 코드 디렉터리에 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="012d8-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="012d8-122">업데이트 된 솔루션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="012d8-123">ASP.NET 구성 사이트를 사용 하 여 관리자 추가</span><span class="sxs-lookup"><span data-stu-id="012d8-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="012d8-124">웹 사이트에서 권한 부여를 요구 하기 전에 액세스 권한이 있는 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="012d8-125">사용자를 만드는 가장 쉬운 방법은 기본 제공 ASP.NET 구성 웹 사이트를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="012d8-126">솔루션 탐색기 아이콘을 클릭 하 여 ASP.NET 구성 웹 사이트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="012d8-127">그러면 구성 웹 사이트가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-127">This launches a configuration website.</span></span> <span data-ttu-id="012d8-128">홈 화면에서 보안 탭을 클릭 한 다음 화면 가운데에 있는 "역할 사용" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="012d8-129">"역할 만들기 또는 관리" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="012d8-130">역할 이름으로 "관리자"를 입력 하 고 역할 추가 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="012d8-131">뒤로 단추를 클릭 한 다음 왼쪽의 사용자 만들기 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="012d8-132">다음 정보를 사용 하 여 왼쪽에 있는 사용자 정보 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="012d8-133">**필드**</span><span class="sxs-lookup"><span data-stu-id="012d8-133">**Field**</span></span> | <span data-ttu-id="012d8-134">**값**</span><span class="sxs-lookup"><span data-stu-id="012d8-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="012d8-135">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="012d8-135">**User Name**</span></span> | <span data-ttu-id="012d8-136">관리자</span><span class="sxs-lookup"><span data-stu-id="012d8-136">Administrator</span></span> |
| <span data-ttu-id="012d8-137">**암호**</span><span class="sxs-lookup"><span data-stu-id="012d8-137">**Password**</span></span> | <span data-ttu-id="012d8-138">password123!</span><span class="sxs-lookup"><span data-stu-id="012d8-138">password123!</span></span> |
| <span data-ttu-id="012d8-139">**암호 확인**</span><span class="sxs-lookup"><span data-stu-id="012d8-139">**Confirm Password**</span></span> | <span data-ttu-id="012d8-140">password123!</span><span class="sxs-lookup"><span data-stu-id="012d8-140">password123!</span></span> |
| <span data-ttu-id="012d8-141">**전자 메일**</span><span class="sxs-lookup"><span data-stu-id="012d8-141">**E-mail**</span></span> | <span data-ttu-id="012d8-142">(모든 전자 메일 주소를 사용할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="012d8-142">(any email address will work)</span></span> |
| <span data-ttu-id="012d8-143">**보안 질문**</span><span class="sxs-lookup"><span data-stu-id="012d8-143">**Security Question**</span></span> | <span data-ttu-id="012d8-144">(원하는 모든 항목)</span><span class="sxs-lookup"><span data-stu-id="012d8-144">(whatever you like)</span></span> |
| <span data-ttu-id="012d8-145">**보안 대답**</span><span class="sxs-lookup"><span data-stu-id="012d8-145">**Security Answer**</span></span> | <span data-ttu-id="012d8-146">(원하는 모든 항목)</span><span class="sxs-lookup"><span data-stu-id="012d8-146">(whatever you like)</span></span> |

<span data-ttu-id="012d8-147">*참고: 물론 원하는 암호를 사용할 수 있습니다. 기본 암호 보안 설정에는 7 자 길이의 암호와 영숫자가 아닌 문자를 포함 하는 암호가 필요 합니다.*</span><span class="sxs-lookup"><span data-stu-id="012d8-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="012d8-148">이 사용자에 대 한 관리자 역할을 선택 하 고 사용자 만들기 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="012d8-149">이 시점에서 사용자가 성공적으로 생성 되었음을 나타내는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="012d8-150">이제 브라우저 창을 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="012d8-151">역할 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="012d8-151">Role-based Authorization</span></span>

<span data-ttu-id="012d8-152">이제 [권한 부여] 특성을 사용 하 여 StoreManagerController에 대 한 액세스를 제한할 수 있습니다 .이 특성을 사용 하 여 클래스의 컨트롤러 작업에 액세스 하려면 사용자가 관리자 역할에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="012d8-153">*참고: [권한 부여] 특성은 특정 작업 메서드 뿐만 아니라 컨트롤러 클래스 수준에도 배치할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="012d8-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="012d8-154">이제/Sstemanager로 이동 하면 다음과 같은 로그온 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="012d8-155">새 관리자 계정으로 로그온 한 후에는 이전과 마찬가지로 앨범 편집 화면으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="012d8-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="012d8-156">[이전](mvc-music-store-part-6.md)
> [다음](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="012d8-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>
