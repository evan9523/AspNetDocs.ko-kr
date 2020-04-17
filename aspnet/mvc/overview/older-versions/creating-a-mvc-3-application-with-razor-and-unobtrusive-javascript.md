---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 면도기와 눈에 거슬리지 자바 스크립트와 MVC 3 응용 프로그램 만들기 | 마이크로 소프트 문서
author: rick-anderson
description: 사용자 목록 샘플 웹 응용 프로그램은 Razor 보기 엔진을 사용하여 ASP.NET MVC 3 응용 프로그램을 만드는 것이 얼마나 간단한지 보여 줍니다. 샘플 응용 프로그램 ...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542458"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="e20a6-104">Razor 및 Unobtrusive JavaScript를 사용하여 MVC 3 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="e20a6-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="e20a6-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e20a6-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e20a6-106">사용자 목록 샘플 웹 응용 프로그램은 Razor 보기 엔진을 사용하여 ASP.NET MVC 3 응용 프로그램을 만드는 것이 얼마나 간단한지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="e20a6-107">샘플 응용 프로그램은 ASP.NET MVC 버전 3 및 Visual Studio 2010과 함께 새로운 Razor 뷰 엔진을 사용하여 사용자 만들기, 표시, 편집 및 삭제와 같은 기능을 포함하는 가상의 사용자 목록 웹 사이트를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="e20a6-108">이 자습서에서는 MVC 3 응용 프로그램에서 사용자 목록 샘플을 빌드하기 위해 수행된 단계를 ASP.NET 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="e20a6-109">C# 및 VB 소스 코드가 있는 Visual Studio 프로젝트를 이 [항목과](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="e20a6-110">이 튜토리얼에 대한 질문이있는 경우, [MVC 포럼에](https://forums.asp.net/1146.aspx)게시하시기 바랍니다 .</span><span class="sxs-lookup"><span data-stu-id="e20a6-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="e20a6-111">개요</span><span class="sxs-lookup"><span data-stu-id="e20a6-111">Overview</span></span>

<span data-ttu-id="e20a6-112">빌드할 응용 프로그램은 간단한 사용자 목록 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="e20a6-113">사용자는 사용자 정보를 입력, 보기 및 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-113">Users can enter, view, and update user information.</span></span>

![샘플 사이트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="e20a6-115">여기에서 VB 및 C# 완료된 프로젝트를 다운로드할 수 [있습니다.](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)</span><span class="sxs-lookup"><span data-stu-id="e20a6-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="e20a6-116">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e20a6-116">Creating the Web Application</span></span>

<span data-ttu-id="e20a6-117">자습서를 시작 하려면 Visual Studio 2010을 열고 *ASP.NET MVC 3 웹 응용 프로그램* 템플릿을 사용 하 여 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="e20a6-118">응용 프로그램 &quot;Mvc3Razor의&quot;이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="e20a6-119">[![새로운 MVC 3 프로젝트](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="e20a6-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="e20a6-120">새로운 **ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램을**선택하고 Razor 보기 엔진을 선택한 다음 **확인을**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![새로운 ASP.NET MVC 3 프로젝트 대화 상자](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="e20a6-122">이 자습서에서는 ASP.NET 멤버 자격 공급자를 사용 하지 않습니다., 그래서 로그온 및 멤버 자격과 관련 된 모든 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="e20a6-123">**솔루션 탐색기에서**다음 파일 및 디렉터리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="e20a6-124">*컨트롤러\계정 컨트롤러*</span><span class="sxs-lookup"><span data-stu-id="e20a6-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="e20a6-125">*모델\계정 모델*</span><span class="sxs-lookup"><span data-stu-id="e20a6-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="e20a6-126">*뷰\공유\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="e20a6-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="e20a6-127">*뷰\계정(이* 디렉터리에 있는 모든 파일)</span><span class="sxs-lookup"><span data-stu-id="e20a6-127">*Views\Account* (and all the files in this directory)</span></span>

![졸 익스피타](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="e20a6-129"><em>&quot;</em>&quot; <em> \_Layout.cshtml</em> 파일을 편집하고 로그인 사용 안 `<div>` 함이라는 요소 `logindisplay` 내부의 태그를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="e20a6-130">다음 예제에서는 새 태그를 보여 주며 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="e20a6-131">모델 추가</span><span class="sxs-lookup"><span data-stu-id="e20a6-131">Adding the Model</span></span>

<span data-ttu-id="e20a6-132">**솔루션 탐색기에서** *모델* 폴더를 마우스 오른쪽 단추로 클릭하고 **에 추가를**선택한 다음 **클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![새 사용자 Mdl 클래스](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="e20a6-134">클래스 `UserModel` 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-134">Name the class `UserModel`.</span></span> <span data-ttu-id="e20a6-135">*UserModel* 파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="e20a6-136">클래스는 `UserModel` 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="e20a6-137">클래스의 각 멤버는 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임스페이스의 [필수](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 특성으로 주석이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="e20a6-138">[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임스페이스의 특성은 웹 응용 프로그램에 대한 자동 클라이언트 및 서버 측 유효성 검사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="e20a6-139">클래스를 `HomeController` 열고 `using` `UserModel` 및 `Users` 클래스에 액세스할 수 있도록 지시문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="e20a6-140">`HomeController` 선언 직후 다음 주석과 참조를 클래스에 `Users` 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="e20a6-141">클래스는 `Users` 이 자습서에서 사용할 단순화된 메모리 내 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="e20a6-142">실제 응용 프로그램에서는 데이터베이스를 사용하여 사용자 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="e20a6-143">`HomeController` 파일의 처음 몇 줄은 다음 예제에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="e20a6-144">다음 단계에서 스캐폴딩 마법사에서 사용자 모델을 사용할 수 있도록 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="e20a6-145">기본 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="e20a6-145">Creating the Default View</span></span>

<span data-ttu-id="e20a6-146">다음 단계는 사용자를 표시할 작업 메서드 및 보기를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="e20a6-147">기존 *뷰\Home\Index 파일을 삭제합니다.*</span><span class="sxs-lookup"><span data-stu-id="e20a6-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="e20a6-148">사용자를 표시하는 새 *Index* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="e20a6-149">`HomeController` 클래스에서 `Index` 메서드의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="e20a6-150">메서드 내부를 `Index` 마우스 오른쪽 단추로 클릭한 다음 **보기 추가를**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="e20a6-152">강력한 **형식의 뷰 만들기 옵션을 선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="e20a6-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="e20a6-153">**데이터 클래스 보기의**경우 **Mvc3Razor.Models.UserModel**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="e20a6-154">(보기 **데이터 클래스** 상자에 **Mvc3Razor.Models.UserModel이** 표시되지 않으면 프로젝트를 빌드해야 합니다.) 뷰 엔진이 **Razor로**설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="e20a6-155">**콘텐츠 보기를** **목록으로** 설정한 다음 **추가를**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-155">Set **View content** to **List** and then click **Add**.</span></span>

![인덱스 뷰 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="e20a6-157">새 보기는 뷰에 전달된 사용자 데이터를 자동으로 스캐폴드합니다. `Index`</span><span class="sxs-lookup"><span data-stu-id="e20a6-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="e20a6-158">새로 생성된 *뷰\Home\Index 파일을 검사합니다.*</span><span class="sxs-lookup"><span data-stu-id="e20a6-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="e20a6-159">**새 만들기,** **편집,** **세부 정보**및 **삭제** 링크는 작동하지 않지만 페이지의 나머지 는 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="e20a6-160">페이지를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-160">Run the page.</span></span> <span data-ttu-id="e20a6-161">사용자 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-161">You see a list of users.</span></span>

![색인 페이지](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="e20a6-163">*Index.cshtml* 파일을 열고 **편집**, **세부 정보**및 **삭제에** `ActionLink` 대한 태그를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="e20a6-164">사용자 이름은 ID로 사용되어 **편집,** **세부 정보**및 **삭제** 링크에서 선택한 레코드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="e20a6-165">세부 정보 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="e20a6-165">Creating the Details View</span></span>

<span data-ttu-id="e20a6-166">다음 단계는 사용자 `Details` 세부 정보를 표시하기 위해 작업 메서드및 보기를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![세부 정보](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="e20a6-168">홈 컨트롤러에 다음 `Details` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="e20a6-169">메서드 내부를 `Details` 마우스 오른쪽 단추로 클릭한 다음 <strong>보기 추가를</strong>선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="e20a6-170"><strong>보기 데이터 클래스</strong> 상자에 <strong>Mvc3Razor.Models.UserModel</strong>이 포함되어 있는지 확인합니다.<em>.</em></span><span class="sxs-lookup"><span data-stu-id="e20a6-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="e20a6-171"><strong>콘텐츠 보기를</strong> <strong>세부 정보로</strong> 설정한 다음 <strong>을 클릭합니다.</strong></span><span class="sxs-lookup"><span data-stu-id="e20a6-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![세부 정보 보기 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="e20a6-173">응용 프로그램을 실행하고 세부 정보 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-173">Run the application and select a details link.</span></span> <span data-ttu-id="e20a6-174">자동 스캐폴딩은 모델의 각 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-174">The automatic scaffolding shows each property in the model.</span></span>

![세부 정보](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="e20a6-176">편집 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="e20a6-176">Creating the Edit View</span></span>

<span data-ttu-id="e20a6-177">홈 컨트롤러에 다음 `Edit` 방법을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="e20a6-178">이전 단계에서와 같이 뷰를 추가하지만 **View 콘텐츠를** **편집하도록**설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![편집 보기 추가](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="e20a6-180">응용 프로그램을 실행하고 사용자 중 하나의 이름과 성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="e20a6-181">`UserModel` 클래스에 적용된 `DataAnnotation` 제약 조건을 위반하는 경우 양식을 제출할 때 서버 코드에서 생성되는 유효성 검사 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="e20a6-182">&quot;예를 들어 양식을 제출할 때&quot; 이름 &quot;&quot;Ann을 A로 변경하면 양식에 다음 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="e20a6-183">이 자습서에서는 사용자 이름을 기본 키로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="e20a6-184">따라서 사용자 이름 속성을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="e20a6-185">*Edit.cshtml* 파일에서 `Html.BeginForm` 명령문 바로 다음에서 사용자 이름을 숨겨진 필드로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="e20a6-186">이렇게 하면 모델에서 속성이 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="e20a6-187">다음 코드 조각은 명령문의 `Hidden` 배치를 보여 주며,</span><span class="sxs-lookup"><span data-stu-id="e20a6-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="e20a6-188">사용자 `TextBoxFor` 이름에 `ValidationMessageFor` 대한 및 마크업을 `DisplayFor` 호출로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="e20a6-189">메서드는 `DisplayFor` 속성을 읽기 전용 요소로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="e20a6-190">다음 예제에서는 전체 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-190">The following example shows the completed markup.</span></span> <span data-ttu-id="e20a6-191">원본 `TextBoxFor` 및 `ValidationMessageFor` 호출은 Razor 시작 주석 및 최종 주석`@* *@`문자 () 로 주석처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="e20a6-192">클라이언트 측 유효성 검사 사용</span><span class="sxs-lookup"><span data-stu-id="e20a6-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="e20a6-193">ASP.NET MVC 3에서 클라이언트 측 유효성 검사를 사용하려면 두 개의 플래그를 설정해야 하며 세 개의 JavaScript 파일을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="e20a6-194">응용 프로그램의 *Web.config* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="e20a6-195">응용 `that ClientValidationEnabled` `UnobtrusiveJavaScriptEnabled` 프로그램 설정에서 확인 및 true로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="e20a6-196">루트 *Web.config* 파일의 다음 조각에는 올바른 설정이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="e20a6-197">true로 설정하면 `UnobtrusiveJavaScriptEnabled` 눈에 거슬리지 않는 Ajax 및 눈에 거슬리지 않는 클라이언트 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="e20a6-198">눈에 거슬리지 않는 유효성 검사를 사용하면 유효성 검사 규칙이 HTML5 특성으로 바뀌게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="e20a6-199">HTML5 특성 이름은 소문자, 숫자 및 대시로만 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="e20a6-200">true로 설정하면 `ClientValidationEnabled` 클라이언트 측 유효성 검사가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="e20a6-201">응용 프로그램 *Web.config* 파일에 이러한 키를 설정 하 여 클라이언트 유효성 검사 및 전체 응용 프로그램에 대 한 눈에 거슬리지 자바 스크립트를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="e20a6-202">다음 코드를 사용하여 개별 보기 또는 컨트롤러 메서드에서 이러한 설정을 활성화하거나 사용하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="e20a6-203">또한 렌더링된 보기에 여러 JavaScript 파일을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="e20a6-204">모든 보기에 자바스크립트를 포함하는 쉬운 방법은 *뷰\공유\\_Layout.cshtml* 파일에 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="e20a6-205">Layout.cshtml 파일의 `<head>` 요소를 다음 코드로 바꿉니다. \* \_\*</span><span class="sxs-lookup"><span data-stu-id="e20a6-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="e20a6-206">처음 두 개의 jQuery 스크립트는 Microsoft Ajax 콘텐츠 전송 네트워크(CDN)에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="e20a6-207">Microsoft Ajax CDN을 활용하면 응용 프로그램의 첫 번째 성능이 크게 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="e20a6-208">응용 프로그램을 실행하고 편집 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-208">Run the application and click an edit link.</span></span> <span data-ttu-id="e20a6-209">브라우저에서 페이지의 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-209">View the page's source in the browser.</span></span> <span data-ttu-id="e20a6-210">브라우저 원본에는 양식의 `data-val` 많은 특성이 표시됩니다(데이터 유효성 검사용).</span><span class="sxs-lookup"><span data-stu-id="e20a6-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="e20a6-211">클라이언트 유효성 검사와 눈에 거슬리지 않는 JavaScript를 사용하도록 설정하면 `data-val="true"` 클라이언트 유효성 검사 규칙이 있는 입력 필드에는 눈에 거슬리지 않는 클라이언트 유효성 검사를 트리거하는 특성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="e20a6-212">예를 들어 `City` 모델의 필드가 [필수](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 특성으로 장식되어 다음 예제에 표시된 HTML이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="e20a6-213">각 클라이언트 유효성 검사 규칙에 대해 폼이 `data-val-rulename="message"`있는 특성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="e20a6-214">앞서 `City` 보여 드신 필드 예제를 사용 하 `data-val-required` 여 필요한 &quot;클라이언트 유효성 검사&quot;규칙 특성을 생성 하 고 메시지 도시 필드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="e20a6-215">응용 프로그램을 실행하고 사용자 중 하나를 편집하고 `City` 필드를 지웁습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="e20a6-216">필드를 탭하면 클라이언트 측 유효성 검사 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![도시 필수](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="e20a6-218">마찬가지로 클라이언트 유효성 검사 규칙의 각 매개 변수에 대해 `data-val-rulename-paramname=paramvalue`폼이 있는 특성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="e20a6-219">예를 들어 `FirstName` 속성은 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 특성에 추가되고 최소 길이 3과 최대 길이 8을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="e20a6-220">명명된 `length` 데이터 유효성 검사 `max` 규칙에는 매개 변수 이름과 매개 변수 값 8이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="e20a6-221">다음은 사용자 중 하나를 편집할 `FirstName` 때 필드에 대해 생성되는 HTML을 보여 주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="e20a6-222">눈에 거슬리지 않는 클라이언트 유효성 검사에 대한 자세한 내용은 브래드 윌슨의 [블로그에서 ASP.NET MVC 3의 눈에 거슬리지 않는 클라이언트 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) 항목을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="e20a6-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="e20a6-223">ASP.NET MVC 3 베타에서는 클라이언트 측 유효성 검사를 시작하려면 양식을 제출해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="e20a6-224">최종 릴리스에 대해 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="e20a6-225">뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="e20a6-225">Creating the Create View</span></span>

<span data-ttu-id="e20a6-226">다음 단계는 사용자가 `Create` 새 사용자를 만들 수 있도록 작업 메서드 및 보기를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="e20a6-227">홈 컨트롤러에 다음 `Create` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="e20a6-228">이전 단계에서와 같이 뷰를 추가하지만 **뷰 콘텐츠를** **만들기로 설정합니다.**</span><span class="sxs-lookup"><span data-stu-id="e20a6-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![뷰 만들기](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="e20a6-230">응용 프로그램을 실행하고 링크 **만들기를** 선택하고 새 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="e20a6-231">메서드는 `Create` 자동으로 클라이언트 쪽 및 서버 쪽 유효성 검사를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="e20a6-232">Ben X와 &quot;&quot;같은 공백이 포함된 사용자 이름을 입력해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="e20a6-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="e20a6-233">사용자 이름 필드를 탭하면 클라이언트 측 유효성 검사`White space is not allowed`오류()가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="e20a6-234">삭제 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="e20a6-234">Add the Delete method</span></span>

<span data-ttu-id="e20a6-235">자습서를 완료하려면 홈 `Delete` 컨트롤러에 다음 방법을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="e20a6-236">이전 `Delete` 단계에서와 같이 보기를 추가하여 **콘텐츠** **보기를 삭제로**설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![보기 삭제](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="e20a6-238">이제 유효성 검사를 통해 간단하지만 완벽하게 작동하는 ASP.NET MVC 3 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e20a6-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
