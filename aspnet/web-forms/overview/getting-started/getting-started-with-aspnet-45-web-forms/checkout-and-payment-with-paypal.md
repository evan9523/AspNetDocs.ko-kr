---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 체크 아웃 및 PayPal 사용 하 여 지불 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 0fc4e85a86289667566a76537dd1573f4d9b2bf0
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131736"
---
# <a name="checkout-and-payment-with-paypal"></a><span data-ttu-id="f5f52-103">PayPal로 체크 아웃 및 지불</span><span class="sxs-lookup"><span data-stu-id="f5f52-103">Checkout and Payment with PayPal</span></span>

<span data-ttu-id="f5f52-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="f5f52-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="f5f52-105">[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="f5f52-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="f5f52-106">이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="f5f52-107">Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="f5f52-108">이 자습서에서는 Wingtip Toys 샘플 응용 프로그램 사용자 권한 부여, 등록 및 PayPal을 사용 하 여 결제를 포함 하도록 수정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-108">This tutorial describes how to modify the Wingtip Toys sample application to include user authorization, registration, and payment using PayPal.</span></span> <span data-ttu-id="f5f52-109">에 로그인 한 사용자만 제품을 구매 하려면 권한 부여를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-109">Only users who are logged in will have authorization to purchase products.</span></span> <span data-ttu-id="f5f52-110">이미 ASP.NET 4.5 Web Forms 프로젝트 템플릿의 기본 제공 사용자 등록 기능을 포함 해야 하는 작업의 대부분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-110">The ASP.NET 4.5 Web Forms project template's built-in user registration functionality already includes much of what you need.</span></span> <span data-ttu-id="f5f52-111">PayPal Express 체크 아웃 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-111">You will add PayPal Express Checkout functionality.</span></span> <span data-ttu-id="f5f52-112">이 자습서에서는 테스트 환경에 없는 실제 금액 전송 될 있도록 PayPal 개발자를 사용할입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-112">In this tutorial you be using the PayPal developer testing environment, so no actual funds will be transferred.</span></span> <span data-ttu-id="f5f52-113">이 자습서의 끝 쇼핑 카트, 체크 아웃 단추를 클릭 하 고 PayPal 테스트 웹 사이트에 데이터를 전송에 추가할 제품을 선택 하 여 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-113">At the end of the tutorial, you will test the application by selecting products to add to the shopping cart, clicking the checkout button, and transferring data to the PayPal testing web site.</span></span> <span data-ttu-id="f5f52-114">PayPal 테스트 웹 사이트에서 전달 하 고 결제 정보를 확인 하 고 로컬 Wingtip Toys 샘플 응용 프로그램을 확인 하 고 구매를 완료로 돌아와서는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-114">On the PayPal testing web site, you will confirm your shipping and payment information and then return to the local Wingtip Toys sample application to confirm and complete the purchase.</span></span>

<span data-ttu-id="f5f52-115">해당 주소 확장성 및 보안에는 온라인 쇼핑에 전문화 된 여러 숙련 된 타사 지급 처리 프로세서를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-115">There are several experienced third-party payment processors that specialize in online shopping that address scalability and security.</span></span> <span data-ttu-id="f5f52-116">ASP.NET 개발자는 이점은 하나의 쇼핑을 구현 하 고 솔루션을 구매 하기 전에 타사 지불 솔루션을 활용 하 여 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-116">ASP.NET developers should consider the advantages of utilizing a third party payment solution before implementing a shopping and purchasing solution.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f5f52-117">Wingtip Toys 샘플 응용 프로그램은 ASP.NET 웹 개발자에 게 특정 ASP.NET 개념 및 사용할 수 있는 기능을 표시 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-117">The Wingtip Toys sample application was designed to shown specific ASP.NET concepts and features available to ASP.NET web developers.</span></span> <span data-ttu-id="f5f52-118">이 샘플 응용 프로그램 확장성 및 보안 관련 하 여 가능한 모든 상황에 최적화 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-118">This sample application was not optimized for all possible circumstances in regard to scalability and security.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="f5f52-119">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="f5f52-119">What you'll learn:</span></span>

- <span data-ttu-id="f5f52-120">폴더의 특정 페이지에 대 한 액세스를 제한 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="f5f52-120">How to restrict access to specific pages in a folder.</span></span>
- <span data-ttu-id="f5f52-121">익명 쇼핑 카트에서 알려진된 쇼핑 카트를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-121">How to create a known shopping cart from an anonymous shopping cart.</span></span>
- <span data-ttu-id="f5f52-122">프로젝트에 대 한 SSL을 사용 하도록 설정 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="f5f52-122">How to enable SSL for the project.</span></span>
- <span data-ttu-id="f5f52-123">OAuth 공급자 프로젝트에 추가 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="f5f52-123">How to add an OAuth provider to the project.</span></span>
- <span data-ttu-id="f5f52-124">PayPal을 사용 하 여 PayPal 테스트 환경을 사용 하 여 제품을 구매 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="f5f52-124">How to use PayPal to purchase products using the PayPal testing environment.</span></span>
- <span data-ttu-id="f5f52-125">PayPal에서 세부 정보를 표시 하는 방법에 **DetailsView** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-125">How to display details from PayPal in a **DetailsView** control.</span></span>
- <span data-ttu-id="f5f52-126">PayPal에서 가져온 정보를 사용 하 여 Wingtip Toys 응용 프로그램의 데이터베이스를 업데이트 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-126">How to update the database of the Wingtip Toys application with details obtained from PayPal.</span></span>

## <a name="adding-order-tracking"></a><span data-ttu-id="f5f52-127">주문 추적 추가</span><span class="sxs-lookup"><span data-stu-id="f5f52-127">Adding Order Tracking</span></span>

<span data-ttu-id="f5f52-128">이 자습서에서는 사용자가 만든 순서에서 데이터를 추적 하는 두 개의 새 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-128">In this tutorial, you'll create two new classes to track data from the order a user has created.</span></span> <span data-ttu-id="f5f52-129">클래스에서 배송 정보, 구매 합계 및 지불 확인에 대 한 데이터를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-129">The classes will track data regarding shipping information, purchase total, and payment confirmation.</span></span>

### <a name="add-the-order-and-orderdetail-model-classes"></a><span data-ttu-id="f5f52-130">Order 및 OrderDetail 모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="f5f52-130">Add the Order and OrderDetail Model Classes</span></span>

<span data-ttu-id="f5f52-131">이 자습서 시리즈의 앞부분에 나오는 범주, 제품에 대 한 스키마를 정의 하 고 쇼핑 카트에 항목을 만들어 합니다 `Category`, `Product`, 및 `CartItem` 클래스에 *모델* 폴더.</span><span class="sxs-lookup"><span data-stu-id="f5f52-131">Earlier in this tutorial series, you defined the schema for categories, products, and shopping cart items by creating the `Category`, `Product`, and `CartItem` classes in the *Models* folder.</span></span> <span data-ttu-id="f5f52-132">이제 제품 주문 및 주문 세부 정보에 대 한 스키마를 정의 하는 두 개의 새 클래스가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-132">Now you will add two new classes to define the schema for the product order and the details of the order.</span></span>

1. <span data-ttu-id="f5f52-133">에 **모델** 폴더를 라는 새 클래스 추가 *Order.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-133">In the **Models** folder, add a new class named *Order.cs*.</span></span>   
   <span data-ttu-id="f5f52-134">새 클래스 파일을 편집기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-134">The new class file is displayed in the editor.</span></span>
2. <span data-ttu-id="f5f52-135">기본 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-135">Replace the default code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. <span data-ttu-id="f5f52-136">추가 *OrderDetail.cs* 클래스는 *모델* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-136">Add an *OrderDetail.cs* class to the *Models* folder.</span></span>
4. <span data-ttu-id="f5f52-137">기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-137">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

<span data-ttu-id="f5f52-138">합니다 `Order` 및 `OrderDetail` 클래스 구매 및 전달에 사용 되는 주문 정보를 정의 하는 스키마를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-138">The `Order` and `OrderDetail` classes contain the schema to define the order information used for purchasing and shipping.</span></span>

<span data-ttu-id="f5f52-139">또한 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 데이터베이스 컨텍스트 클래스를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-139">In addition, you will need to update the database context class that manages the entity classes and that provides data access to the database.</span></span> <span data-ttu-id="f5f52-140">이렇게 하려면 새로 생성된 된 주문을 추가 하 고 `OrderDetail` 모델 클래스를 `ProductContext` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-140">To do this, you will add the newly created Order and `OrderDetail` model classes to `ProductContext` class.</span></span>

1. <span data-ttu-id="f5f52-141">**솔루션 탐색기**찾기 및 열기, 합니다 *ProductContext.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-141">In **Solution Explorer**, find and open the *ProductContext.cs* file.</span></span>
2. <span data-ttu-id="f5f52-142">강조 표시 된 코드를 추가 합니다 *ProductContext.cs* 아래와 같이 파일:</span><span class="sxs-lookup"><span data-stu-id="f5f52-142">Add the highlighted code to the *ProductContext.cs* file as shown below:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

<span data-ttu-id="f5f52-143">이 자습서 시리즈의 코드에서 이전에 설명한 것 처럼 합니다 *ProductContext.cs* 파일 추가 `System.Data.Entity` 네임 스페이스 Entity Framework의 모든 핵심 기능에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-143">As mentioned previously in this tutorial series, the code in the *ProductContext.cs* file adds the `System.Data.Entity` namespace so that you have access to all the core functionality of the Entity Framework.</span></span> <span data-ttu-id="f5f52-144">이 기능은 쿼리, 삽입, 업데이트 및 강력한 형식의 개체를 사용 하 여 데이터를 삭제 하는 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-144">This functionality includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span> <span data-ttu-id="f5f52-145">위의 코드는 `ProductContext` 하 고 새로 추가한 Entity Framework 액세스를 추가 하는 클래스 `Order` 및 `OrderDetail` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-145">The above code in the `ProductContext` class adds Entity Framework access to the newly added `Order` and `OrderDetail` classes.</span></span>

## <a name="adding-checkout-access"></a><span data-ttu-id="f5f52-146">체크 아웃 액세스 추가</span><span class="sxs-lookup"><span data-stu-id="f5f52-146">Adding Checkout Access</span></span>

<span data-ttu-id="f5f52-147">Wingtip Toys 샘플 응용 프로그램에서는 익명 사용자가 검토 하 고 쇼핑 카트에 제품을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-147">The Wingtip Toys sample application allows anonymous users to review and add products to a shopping cart.</span></span> <span data-ttu-id="f5f52-148">그러나 익명 사용자 들이 하 고 쇼핑 카트에 추가 제품 구매를 선택 해야에 로그온 할 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-148">However, when anonymous users choose to purchase the products they added to the shopping cart, they must log on to the site.</span></span> <span data-ttu-id="f5f52-149">이러한 로그온 한 후 체크 아웃을 처리 하 고 프로세스를 구입 하는 웹 응용 프로그램의 제한 된 페이지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-149">Once they have logged on, they can access the restricted pages of the Web application that handle the checkout and purchase process.</span></span> <span data-ttu-id="f5f52-150">이러한 제한 된 페이지에 포함 된 합니다 *체크 아웃* 응용 프로그램의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-150">These restricted pages are contained in the *Checkout* folder of the application.</span></span>

### <a name="add-a-checkout-folder-and-pages"></a><span data-ttu-id="f5f52-151">체크 아웃 폴더 및 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="f5f52-151">Add a Checkout Folder and Pages</span></span>

<span data-ttu-id="f5f52-152">이제 만들려는 합니다 *체크 아웃* 폴더 및 체크 아웃 프로세스 중에 고객에 게 표시 되는 것의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-152">You will now create the *Checkout* folder and the pages in it that the customer will see during the checkout process.</span></span> <span data-ttu-id="f5f52-153">이 자습서의 뒷부분에서 이러한 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-153">You will update these pages later in this tutorial.</span></span>

1. <span data-ttu-id="f5f52-154">프로젝트 이름을 마우스 오른쪽 단추로 클릭 (**Wingtip Toys**)에서 **솔루션 탐색기** 선택한 **에 새 폴더 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-154">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add a New Folder**.</span></span> 

    ![체크 아웃 및 PayPal-새 폴더를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image1.png)
2. <span data-ttu-id="f5f52-156">새 폴더의 이름을 *체크 아웃*합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-156">Name the new folder *Checkout*.</span></span>
3. <span data-ttu-id="f5f52-157">마우스 오른쪽 단추로 클릭 합니다 *체크 아웃* 한 다음 선택한 폴더 **추가**-&gt;**새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-157">Right-click the *Checkout* folder and then select **Add**-&gt;**New Item**.</span></span> 

    ![체크 아웃 및 PayPal-새 항목을 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image2.png)
4. <span data-ttu-id="f5f52-159">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-159">The **Add New Item** dialog box is displayed.</span></span>
5. <span data-ttu-id="f5f52-160">선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-160">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="f5f52-161">그런 다음, 가운데 창에서 선택 **마스터 페이지를 사용 하 여 Web Form**하 고 이름을 *CheckoutStart.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-161">Then, from the middle pane, select **Web Form with Master Page**and name it *CheckoutStart.aspx*.</span></span> 

    ![체크 아웃 및 지불 PayPal-를 사용 하 여 새 항목 추가 대화 상자](checkout-and-payment-with-paypal/_static/image3.png)
6. <span data-ttu-id="f5f52-163">이전과 마찬가지로 선택 합니다 *Site.Master* 마스터 페이지 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-163">As before, select the *Site.Master* file as the master page.</span></span>
7. <span data-ttu-id="f5f52-164">다음 추가 페이지를 추가 합니다 *체크 아웃* 위와 동일한 단계를 사용 하 여 폴더:</span><span class="sxs-lookup"><span data-stu-id="f5f52-164">Add the following additional pages to the *Checkout* folder using the same steps above:</span></span>   

    - <span data-ttu-id="f5f52-165">CheckoutReview.aspx</span><span class="sxs-lookup"><span data-stu-id="f5f52-165">CheckoutReview.aspx</span></span>
    - <span data-ttu-id="f5f52-166">CheckoutComplete.aspx</span><span class="sxs-lookup"><span data-stu-id="f5f52-166">CheckoutComplete.aspx</span></span>
    - <span data-ttu-id="f5f52-167">CheckoutCancel.aspx</span><span class="sxs-lookup"><span data-stu-id="f5f52-167">CheckoutCancel.aspx</span></span>
    - <span data-ttu-id="f5f52-168">CheckoutError.aspx</span><span class="sxs-lookup"><span data-stu-id="f5f52-168">CheckoutError.aspx</span></span>

### <a name="add-a-webconfig-file"></a><span data-ttu-id="f5f52-169">Web.config 파일 추가</span><span class="sxs-lookup"><span data-stu-id="f5f52-169">Add a Web.config File</span></span>

<span data-ttu-id="f5f52-170">새로 추가 하 여 *Web.config* 파일을 합니다 *체크 아웃* 폴더에 포함 된 모든 페이지에 액세스를 제한할 수 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-170">By adding a new *Web.config* file to the *Checkout* folder, you will be able to restrict access to all the pages contained in the folder.</span></span>

1. <span data-ttu-id="f5f52-171">마우스 오른쪽 단추로 클릭 합니다 *체크 아웃* 선택한 폴더 **추가**  - &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-171">Right-click the *Checkout* folder and select **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="f5f52-172">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-172">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="f5f52-173">선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-173">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="f5f52-174">그런 다음, 가운데 창에서 선택 **웹 구성 파일**의 기본 이름을 그대로 *Web.config*를 선택한 후 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-174">Then, from the middle pane, select **Web Configuration File**, accept the default name of *Web.config*, and then select **Add**.</span></span>
3. <span data-ttu-id="f5f52-175">기존 XML 콘텐츠를 대체 합니다 *Web.config* 다음 파일:</span><span class="sxs-lookup"><span data-stu-id="f5f52-175">Replace the existing XML content in the *Web.config* file with the following:</span></span>  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. <span data-ttu-id="f5f52-176">저장 된 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-176">Save the *Web.config* file.</span></span>

<span data-ttu-id="f5f52-177">*Web.config* 파일에는 웹 응용 프로그램의 모든 알 수 없는 사용자에 포함 된 페이지에 대 한 액세스를 거부 해야 지정 합니다 *체크 아웃* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-177">The *Web.config* file specifies that all unknown users of the Web application must be denied access to the pages contained in the *Checkout* folder.</span></span> <span data-ttu-id="f5f52-178">그러나 사용자가 계정을 등록 하 고 로그온을 하는 경우 이러한 알려진된 사용자 되며 페이지에 액세스 해야 합니다 *체크 아웃* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-178">However, if the user has registered an account and is logged on, they will be a known user and will have access to the pages in the *Checkout* folder.</span></span>

<span data-ttu-id="f5f52-179">ASP.NET 구성 계층 구조를 따르는지 확인 해야 여기서 각 *Web.config* 파일이 있는 폴더와 그 아래 자식 디렉터리의 모든 구성 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-179">It's important to note that ASP.NET configuration follows a hierarchy, where each *Web.config* file applies configuration settings to the folder that it is in and to all of the child directories below it.</span></span>

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a><span data-ttu-id="f5f52-180">프로젝트에 대 한 SSL을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f5f52-180">Enable SSL for the Project</span></span>

 <span data-ttu-id="f5f52-181">Secure Sockets Layer (SSL)는 웹 서버 및 웹 클라이언트가 암호화를 사용 하 여 더 안전 하 게 통신할 수 있도록 정의 된 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-181">Secure Sockets Layer (SSL) is a protocol defined to allow Web servers and Web clients to communicate more securely through the use of encryption.</span></span> <span data-ttu-id="f5f52-182">SSL을 사용 하지 않으면 클라이언트와 서버 간에 전송 되는 데이터 패킷 스니핑 네트워크에 대 한 물리적 액세스를 사용 하 여 모든 사용자에 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-182">When SSL is not used, data sent between the client and server is open to packet sniffing by anyone with physical access to the network.</span></span> <span data-ttu-id="f5f52-183">또한 몇 가지 일반적인 인증 체계 보호 되지 않습니다 일반 HTTP를 통해.</span><span class="sxs-lookup"><span data-stu-id="f5f52-183">Additionally, several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="f5f52-184">특히 기본 인증 및 폼 인증은 암호화 되지 않은 자격 증명을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-184">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="f5f52-185">보안 되도록 이러한 인증 체계는 SSL을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-185">To be secure, these authentication schemes must use SSL.</span></span> 

1. <span data-ttu-id="f5f52-186">**솔루션 탐색기**를 클릭 합니다 **WingtipToys** 프로젝트를 선택한 다음 키를 누릅니다 **F4** 표시할를 **속성** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-186">In **Solution Explorer**, click the **WingtipToys** project, then press **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="f5f52-187">변경 **SSL 사용** 에 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-187">Change **SSL Enabled** to `true`.</span></span>
3. <span data-ttu-id="f5f52-188">복사 합니다 **SSL URL** 나중에 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-188">Copy the **SSL URL** so you can use it later.</span></span>   
 <span data-ttu-id="f5f52-189">SSL url `https://localhost:44300/` 않으면 이전에 만든 SSL 웹 사이트 (아래와 같이).</span><span class="sxs-lookup"><span data-stu-id="f5f52-189">The SSL URL will be `https://localhost:44300/` unless you've previously created SSL Web Sites (as shown below).</span></span>   
    <span data-ttu-id="f5f52-190">![프로젝트 속성](checkout-and-payment-with-paypal/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="f5f52-190">![Project Properties](checkout-and-payment-with-paypal/_static/image4.png)</span></span>
4. <span data-ttu-id="f5f52-191">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **WingtipToys** 프로젝트 및 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-191">In **Solution Explorer**, right click the **WingtipToys** project and click **Properties**.</span></span>
5. <span data-ttu-id="f5f52-192">왼쪽된 탭에서 클릭 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-192">In the left tab, click **Web**.</span></span>
6. <span data-ttu-id="f5f52-193">변경 된 **프로젝트 Url** 사용 하는 **SSL URL** 이전에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-193">Change the **Project Url** to use the **SSL URL** that you saved earlier.</span></span>   
    <span data-ttu-id="f5f52-194">![프로젝트 웹 속성](checkout-and-payment-with-paypal/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f5f52-194">![Project Web Properties](checkout-and-payment-with-paypal/_static/image5.png)</span></span>
7. <span data-ttu-id="f5f52-195">키를 눌러 페이지를 저장할 **CTRL + S**입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-195">Save the page by pressing **CTRL+S**.</span></span>
8. <span data-ttu-id="f5f52-196">**Ctrl+F5**를 눌러 애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-196">Press **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="f5f52-197">Visual Studio에서 SSL 경고를 방지할 수 있도록 하는 옵션을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-197">Visual Studio will display an option to allow you to avoid SSL warnings.</span></span>
9. <span data-ttu-id="f5f52-198">클릭 **예** IIS Express SSL 인증서를 신뢰 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-198">Click **Yes** to trust the IIS Express SSL certificate and continue.</span></span>   
    <span data-ttu-id="f5f52-199">![IIS Express SSL 인증서 세부 정보](checkout-and-payment-with-paypal/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="f5f52-199">![IIS Express SSL certificate details](checkout-and-payment-with-paypal/_static/image6.png)</span></span>  
 <span data-ttu-id="f5f52-200">보안 경고가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-200">A Security Warning is displayed.</span></span>
10. <span data-ttu-id="f5f52-201">클릭 **예** 에 localhost 인증서를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-201">Click **Yes** to install the certificate to your localhost.</span></span>   
    <span data-ttu-id="f5f52-202">![보안 경고 대화 상자](checkout-and-payment-with-paypal/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f5f52-202">![Security Warning dialog box](checkout-and-payment-with-paypal/_static/image7.png)</span></span>  
 <span data-ttu-id="f5f52-203">브라우저 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-203">The browser window will be displayed.</span></span>

<span data-ttu-id="f5f52-204">이제 로컬로 SSL을 사용 하 여 웹 응용 프로그램 쉽게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-204">You can now easily test your Web application locally using SSL.</span></span>

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a><span data-ttu-id="f5f52-205">OAuth 2.0 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="f5f52-205">Add an OAuth 2.0 Provider</span></span>

<span data-ttu-id="f5f52-206">ASP.NET Web Forms는 멤버 자격 및 인증에 대 한 향상 된 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-206">ASP.NET Web Forms provides enhanced options for membership and authentication.</span></span> <span data-ttu-id="f5f52-207">이러한 향상 된이 기능 OAuth가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-207">These enhancements include OAuth.</span></span> <span data-ttu-id="f5f52-208">OAuth는 웹, 모바일 및 데스크톱 응용 프로그램에서 간단한 표준 메서드로 보안 권한 부여를 허용 하는 개방형 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-208">OAuth is an open protocol that allows secure authorization in a simple and standard method from web, mobile, and desktop applications.</span></span> <span data-ttu-id="f5f52-209">ASP.NET Web Forms 템플릿을 OAuth를 사용 하 여 Facebook, Twitter, Google 및 Microsoft를 인증 공급자로 표시.</span><span class="sxs-lookup"><span data-stu-id="f5f52-209">The ASP.NET Web Forms template uses OAuth to expose Facebook, Twitter, Google and Microsoft as authentication providers.</span></span> <span data-ttu-id="f5f52-210">이 자습서에서는 인증 공급자로 Google만 사용, 있지만 공급자 중 하나를 사용 하는 코드를 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-210">Although this tutorial uses only Google as the authentication provider, you can easily modify the code to use any of the providers.</span></span> <span data-ttu-id="f5f52-211">다른 공급자를 구현 하는 단계는이 자습서에서 단계와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-211">The steps to implement other providers are very similar to the steps you will see in this tutorial.</span></span>

<span data-ttu-id="f5f52-212">인증을 하는 것 외에도 자습서 권한 부여를 구현 하려면 역할도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-212">In addition to authentication, the tutorial will also use roles to implement authorization.</span></span> <span data-ttu-id="f5f52-213">에 추가한 사용자만의 `canEdit` 역할 데이터를 변경할 수 있게 됩니다 (만들기, 편집 또는 연락처 삭제).</span><span class="sxs-lookup"><span data-stu-id="f5f52-213">Only those users you add to the `canEdit` role will be able to change data (create, edit, or delete contacts).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f5f52-214">Windows Live 응용 프로그램 작업 웹 사이트에 대 한 라이브 URL에만 동의 로그인 테스트를 위해 로컬 웹 사이트 URL을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-214">Windows Live applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>

<span data-ttu-id="f5f52-215">다음 단계를 사용 하면 Google 인증 공급자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-215">The following steps will allow you to add a Google authentication provider.</span></span>

1. <span data-ttu-id="f5f52-216">엽니다는 *앱\_Start\Startup.Auth.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-216">Open the *App\_Start\Startup.Auth.cs* file.</span></span>
2. <span data-ttu-id="f5f52-217">주석 문자를 제거 합니다 `app.UseGoogleAuthentication()` 메서드도 표시 되는 메서드를 다음과 같이 나타나도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-217">Remove the comment characters from the `app.UseGoogleAuthentication()` method so that the method appears as follows:</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. <span data-ttu-id="f5f52-218">로 이동 합니다 [Google 개발자 콘솔](https://console.developers.google.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-218">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span> <span data-ttu-id="f5f52-219">Google 개발자 메일 계정 (gmail.com)으로 로그인을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-219">You will also need to sign-in with your Google developer email account (gmail.com).</span></span> <span data-ttu-id="f5f52-220">Google 계정이 없으면 선택 합니다 **계정을 만들** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-220">If you do not have a Google account, select the **Create an account** link.</span></span>   
   <span data-ttu-id="f5f52-221">다음으로 보면 합니다 **Google 개발자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-221">Next, you'll see the **Google Developers Console**.</span></span>   
    <span data-ttu-id="f5f52-222">![Google 개발자 콘솔](checkout-and-payment-with-paypal/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="f5f52-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span></span>
4. <span data-ttu-id="f5f52-223">클릭 합니다 **프로젝트 만들기** 단추 및 프로젝트 이름 및 ID (기본 값을 사용할 수 있음)를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-223">Click the **Create Project** button and enter a project name and ID (you can use the default values).</span></span> <span data-ttu-id="f5f52-224">클릭 합니다 **계약 확인란** 및 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-224">Then, click the **agreement checkbox** and the **Create** button.</span></span>  

    ![Google-새 프로젝트](checkout-and-payment-with-paypal/_static/image9.png)

   <span data-ttu-id="f5f52-226">몇 초 안에 새 프로젝트 생성 및 브라우저에 새 프로젝트 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-226">In a few seconds the new project will be created and your browser will display the new projects page.</span></span>
5. <span data-ttu-id="f5f52-227">왼쪽된 탭에서 클릭 **Api &amp; auth**를 클릭 하 고 **자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-227">In the left tab, click **APIs &amp; auth**, and then click **Credentials**.</span></span>
6. <span data-ttu-id="f5f52-228">클릭 합니다 **새 클라이언트 ID 만들기** 아래에서 **OAuth**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-228">Click the **Create New Client ID** under **OAuth**.</span></span>   
   <span data-ttu-id="f5f52-229">합니다 **클라이언트 ID 만들기** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-229">The **Create Client ID** dialog will be displayed.</span></span>   
    <span data-ttu-id="f5f52-230">![Google-클라이언트 ID 만들기](checkout-and-payment-with-paypal/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="f5f52-230">![Google - Create Client ID](checkout-and-payment-with-paypal/_static/image10.png)</span></span>
7. <span data-ttu-id="f5f52-231">에 **클라이언트 ID 만들기** 대화 상자에서 기본값을 그대로 **웹 응용 프로그램** 응용 프로그램 형식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-231">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
8. <span data-ttu-id="f5f52-232">설정 합니다 **권한이 부여 된 JavaScript 원본** 이 자습서의 앞부분에서 사용한 SSL URL로 (`https://localhost:44300/` 다른 SSL 프로젝트를 만든 하지 않는 한).</span><span class="sxs-lookup"><span data-stu-id="f5f52-232">Set the **Authorized JavaScript Origins** to the SSL URL you used earlier in this tutorial (`https://localhost:44300/` unless you've created other SSL projects).</span></span>   
   <span data-ttu-id="f5f52-233">이 URL은 응용 프로그램에 대 한 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-233">This URL is the origin for your application.</span></span> <span data-ttu-id="f5f52-234">이 샘플의 경우 localhost 테스트 URL만 입력할가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-234">For this sample, you will only enter the localhost test URL.</span></span> <span data-ttu-id="f5f52-235">그러나 실제로 localhost 및 프로덕션 계정에 여러 개의 Url을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-235">However, you can enter multiple URLs to account for localhost and production.</span></span>
9. <span data-ttu-id="f5f52-236">설정 된 **Authorized Redirect URI** 다음과:</span><span class="sxs-lookup"><span data-stu-id="f5f52-236">Set the **Authorized Redirect URI** to the following:</span></span> 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   <span data-ttu-id="f5f52-237">이 값은 URI는 ASP.NET OAuth 사용자가 google OAuth 서버와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-237">This value is the URI that ASP.NET OAuth users to communicate with the google OAuth server.</span></span> <span data-ttu-id="f5f52-238">위에서 사용 된 SSL URL을 기억 ( `https://localhost:44300/` 다른 SSL 프로젝트를 만든 하지 않는 한).</span><span class="sxs-lookup"><span data-stu-id="f5f52-238">Remember the SSL URL you used above (    `https://localhost:44300/` unless you've created other SSL projects).</span></span>
10. <span data-ttu-id="f5f52-239">클릭 합니다 **클라이언트 ID 만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-239">Click the **Create Client ID** button.</span></span>
11. <span data-ttu-id="f5f52-240">Google 개발자 콘솔의 왼쪽된 메뉴에서를 클릭 합니다 **동의 화면** 메뉴 항목에 설정한 전자 메일 주소 및 제품 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-240">On the left menu of the Google Developers Console, click the **Consent screen** menu item, then set your email address and product name.</span></span> <span data-ttu-id="f5f52-241">양식을 완료 하면, 클릭 **저장할**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-241">When you have completed the form, click **Save**.</span></span>
12. <span data-ttu-id="f5f52-242">클릭 합니다 **Api** 메뉴 항목, 아래로 스크롤하여를 클릭 합니다 **해제** 단추 옆에 **Google + API**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-242">Click the **APIs** menu item, scroll down and click the **off** button next to **Google+ API**.</span></span>   
    <span data-ttu-id="f5f52-243">이 옵션을 수락 Google + API를 사용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-243">Accepting this option will enable the Google+ API.</span></span>
13. <span data-ttu-id="f5f52-244">업데이트 해야 합니다 **Microsoft.Owin** 버전 3.0.0으로 NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="f5f52-244">You must also update the **Microsoft.Owin** NuGet package to version 3.0.0.</span></span>   
    <span data-ttu-id="f5f52-245">**도구** 메뉴에서 **NuGet 패키지 관리자** 선택한 후 **솔루션용 NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-245">From the **Tools** menu, select **NuGet Package Manager** and then select **Manage NuGet Packages for Solution**.</span></span>  
    <span data-ttu-id="f5f52-246">**NuGet 패키지 관리** 창, 찾기 및 업데이트 합니다 **Microsoft.Owin** 버전 3.0.0으로 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-246">From the **Manage NuGet Packages** window, find and update the **Microsoft.Owin** package to version 3.0.0.</span></span>
14. <span data-ttu-id="f5f52-247">Visual Studio에서 업데이트를 `UseGoogleAuthentication` 메서드를 *Startup.Auth.cs* 복사 및 붙여넣기 하 여 페이지를 **클라이언트 ID** 및 **클라이언트 암호** 메서드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-247">In Visual Studio, update the `UseGoogleAuthentication` method of the *Startup.Auth.cs* page by copying and pasting the **Client ID** and **Client Secret** into the method.</span></span> <span data-ttu-id="f5f52-248">합니다 **클라이언트 ID** 하 고 **클라이언트 비밀** 아래 표시 된 값은 샘플 및 작동 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-248">The **Client ID** and **Client Secret** values shown below are samples and will not work.</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. <span data-ttu-id="f5f52-249">키를 눌러 **ctrl+f5** 를 빌드하고 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-249">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="f5f52-250">클릭 합니다 **로그인** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-250">Click the **Log in** link.</span></span>
16. <span data-ttu-id="f5f52-251">아래 **다른 서비스를 사용 하 여 로그인 할**, 클릭 **Google**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-251">Under **Use another service to log in**, click **Google**.</span></span>  
    <span data-ttu-id="f5f52-252">![로그인](checkout-and-payment-with-paypal/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="f5f52-252">![Log in](checkout-and-payment-with-paypal/_static/image11.png)</span></span>
17. <span data-ttu-id="f5f52-253">자격 증명을 입력 해야 할 경우 자격 증명을 입력할 google 사이트로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-253">If you need to enter your credentials, you will be redirected to the google site where you will enter your credentials.</span></span>  
    ![Google-로그인](checkout-and-payment-with-paypal/_static/image12.png)
18. <span data-ttu-id="f5f52-255">자격 증명을 입력 한 후 방금 만든 웹 응용 프로그램에 권한을 부여 하려면 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-255">After you enter your credentials, you will be prompted to give permissions to the web application you just created.</span></span>  
    ![프로젝트 기본 서비스 계정](checkout-and-payment-with-paypal/_static/image13.png)
19. <span data-ttu-id="f5f52-257">클릭 **수락**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-257">Click **Accept**.</span></span> <span data-ttu-id="f5f52-258">이제 다시 이동 합니다는 **등록** 페이지의 **WingtipToys** Google 계정을 등록할 수 있는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-258">You will now be redirected back to the **Register** page of the **WingtipToys** application where you can register your Google account.</span></span>  
    <span data-ttu-id="f5f52-259">![Google 계정으로 등록](checkout-and-payment-with-paypal/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="f5f52-259">![Register with your Google Account](checkout-and-payment-with-paypal/_static/image14.png)</span></span>
20. <span data-ttu-id="f5f52-260">Gmail 계정에 사용 되는 로컬 전자 메일 등록 이름을 변경할 수 있지만 일반적으로 기본 전자 메일 별칭 (즉, 인증에 사용할 하나)를 유지 하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-260">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="f5f52-261">클릭 **로그인** 위와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-261">Click **Log in** as shown above.</span></span>

### <a name="modifying-login-functionality"></a><span data-ttu-id="f5f52-262">로그인 기능 수정</span><span class="sxs-lookup"><span data-stu-id="f5f52-262">Modifying Login Functionality</span></span>

<span data-ttu-id="f5f52-263">이전에 설명한 것 처럼이 자습서 시리즈에서 대부분의 사용자 등록 기능에 포함 되어 ASP.NET Web Forms 템플릿에 기본적으로.</span><span class="sxs-lookup"><span data-stu-id="f5f52-263">As previously mentioned in this tutorial series, much of the user registration functionality has been included in the ASP.NET Web Forms template by default.</span></span> <span data-ttu-id="f5f52-264">기본값을 수정 하는 이제 *Login.aspx* 하 고 *Register.aspx* 호출 하는 페이지는 `MigrateCart` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f5f52-264">Now you will modify the default *Login.aspx* and *Register.aspx* pages to call the `MigrateCart` method.</span></span> <span data-ttu-id="f5f52-265">`MigrateCart` 메서드는 익명 쇼핑 카트를 사용 하 여 새로 로그인된 한 사용자를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-265">The `MigrateCart` method associates a newly logged in user with an anonymous shopping cart.</span></span> <span data-ttu-id="f5f52-266">사용자를 연결 하 고 쇼핑 카트, Wingtip Toys 샘플 응용 프로그램을 방문 하는 사용자의 쇼핑 카트를 유지할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-266">By associating the user and shopping cart, the Wingtip Toys sample application will be able to maintain the shopping cart of the user between visits.</span></span>

1. <span data-ttu-id="f5f52-267">**솔루션 탐색기**찾기 및 열기, 합니다 *계정* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-267">In **Solution Explorer**, find and open the *Account* folder.</span></span>
2. <span data-ttu-id="f5f52-268">라는 코드 숨김 페이지를 수정 *Login.aspx.cs* 다음과 같이 표시 되도록 노란색으로 강조 표시 된 코드를 포함 하려면:</span><span class="sxs-lookup"><span data-stu-id="f5f52-268">Modify the code-behind page named *Login.aspx.cs* to include the code highlighted in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. <span data-ttu-id="f5f52-269">저장 된 *Login.aspx.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-269">Save the *Login.aspx.cs* file.</span></span>

<span data-ttu-id="f5f52-270">이제 경고에 대 한 정의가 없는 무시할 수 있습니다는 `MigrateCart` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f5f52-270">For now, you can ignore the warning that there is no definition for the `MigrateCart` method.</span></span> <span data-ttu-id="f5f52-271">추가할 것이 자습서의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-271">You will be adding it a bit later in this tutorial.</span></span>

<span data-ttu-id="f5f52-272">합니다 *Login.aspx.cs* 코드 숨김 파일은 로그인 메서드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-272">The *Login.aspx.cs* code-behind file supports a LogIn method.</span></span> <span data-ttu-id="f5f52-273">이 페이지에 "로그인" 단추가 표시 됩니다 Login.aspx 페이지를 검사 하 여 때 트리거를 클릭 합니다 `LogIn` 코드 숨김에 대 한 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-273">By inspecting the Login.aspx page, you'll see that this page includes a "Log in" button that when click triggers the `LogIn` handler on the code-behind.</span></span>

<span data-ttu-id="f5f52-274">경우는 `Login` 메서드를 *Login.aspx.cs* 라고, 명명 된 장바구니의 새 인스턴스 `usersShoppingCart` 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-274">When the `Login` method on the *Login.aspx.cs* is called, a new instance of the shopping cart named `usersShoppingCart` is created.</span></span> <span data-ttu-id="f5f52-275">쇼핑 카트 (GUID)의 ID를 검색 하 고로 설정 된 `cartId` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-275">The ID of the shopping cart (a GUID) is retrieved and set to the `cartId` variable.</span></span> <span data-ttu-id="f5f52-276">그런 다음, `MigrateCart` 모두 전달 메서드가 호출 되는 `cartId` 및이 방법에 로그인 한 사용자의 이름.</span><span class="sxs-lookup"><span data-stu-id="f5f52-276">Then, the `MigrateCart` method is called, passing both the `cartId` and the name of the logged-in user to this method.</span></span> <span data-ttu-id="f5f52-277">쇼핑 카트를 마이그레이션하면 익명 쇼핑 카트를 식별 하는 데 GUID 사용자 이름으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-277">When the shopping cart is migrated, the GUID used to identify the anonymous shopping cart is replaced with the user name.</span></span>

<span data-ttu-id="f5f52-278">수정 하는 것 외에도 *Login.aspx.cs* 사용자가 로그인 할 때 쇼핑 카트를 마이그레이션하도록 코드 숨김 파일 수정 해야 합니다 *Register.aspx.cs 코드 숨김 파일* 쇼핑 카트를 마이그레이션하도록 때 사용자는 새 계정을 만듭니다 하 고 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-278">In addition to modifying the *Login.aspx.cs* code-behind file to migrate the shopping cart when the user logs in, you must also modify the *Register.aspx.cs code-behind file* to migrate the shopping cart when the user creates a new account and logs in.</span></span>

1. <span data-ttu-id="f5f52-279">에 *계정* 폴더를 열고 코드 숨김 파일의 이름은 *Register.aspx.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-279">In the *Account* folder, open the code-behind file named *Register.aspx.cs*.</span></span>
2. <span data-ttu-id="f5f52-280">다음과 같이 표시 되도록 노란색으로 코드를 포함 하 여 코드 숨김 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-280">Modify the code-behind file by including the code in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. <span data-ttu-id="f5f52-281">저장 된 *Register.aspx.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-281">Save the *Register.aspx.cs* file.</span></span> <span data-ttu-id="f5f52-282">다시 한 번에 대 한 경고를 무시 합니다 `MigrateCart` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f5f52-282">Once again, ignore the warning about the `MigrateCart` method.</span></span>

<span data-ttu-id="f5f52-283">사용한 코드를 확인 합니다 `CreateUser_Click` 이벤트 처리기는에서 사용 되는 코드와 매우 비슷합니다는 `LogIn` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f5f52-283">Notice that the code you used in the `CreateUser_Click` event handler is very similar to the code you used in the `LogIn` method.</span></span> <span data-ttu-id="f5f52-284">사용자를 등록 하거나 사이트에 대 한 호출에서 로그를 `MigrateCart` 메서드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-284">When the user registers or logs in to the site, a call to the `MigrateCart` method will be made.</span></span>

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="f5f52-285">장바구니 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="f5f52-285">Migrating the Shopping Cart</span></span>

<span data-ttu-id="f5f52-286">사용 하 여 쇼핑 카트를 마이그레이션하도록 코드를 추가할 수는 로그인 및 등록 프로세스를 업데이트 했으므로 `MigrateCart` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f5f52-286">Now that you have the log-in and registration process updated, you can add the code to migrate the shopping cart using the `MigrateCart` method.</span></span>

1. <span data-ttu-id="f5f52-287">**솔루션 탐색기**, 찾을 합니다 *논리* 폴더를 *ShoppingCartActions.cs* 클래스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-287">In **Solution Explorer**, find the *Logic* folder and open the *ShoppingCartActions.cs* class file.</span></span>
2. <span data-ttu-id="f5f52-288">기존 코드에 노란색으로 강조 표시 하는 코드를 추가 합니다 *ShoppingCartActions.cs* 파일인 있도록의 코드를 *ShoppingCartActions.cs* 파일이 다음과 같이 표시 됩니다:</span><span class="sxs-lookup"><span data-stu-id="f5f52-288">Add the code highlighted in yellow to the existing code in the *ShoppingCartActions.cs* file, so that the code in the *ShoppingCartActions.cs* file appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

<span data-ttu-id="f5f52-289">`MigrateCart` 메서드 기존 cartId를 사용 하 여 사용자의 쇼핑 카트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-289">The `MigrateCart` method uses the existing cartId to find the shopping cart of the user.</span></span> <span data-ttu-id="f5f52-290">코드 쇼핑 카트에 항목을 모두 반복 하 고 대체 하는 다음으로 `CartId` 속성 (지정 된 대로 `CartItem` 스키마)에서 로그인 한 사용자 이름을 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="f5f52-290">Next, the code loops through all the shopping cart items and replaces the `CartId` property (as specified by the `CartItem` schema) with the logged-in user name.</span></span>

### <a name="updating-the-database-connection"></a><span data-ttu-id="f5f52-291">데이터베이스 연결 업데이트</span><span class="sxs-lookup"><span data-stu-id="f5f52-291">Updating the Database Connection</span></span>

<span data-ttu-id="f5f52-292">이 자습서를 사용 하 여 수행 하는 경우는 **미리 빌드된** Wingtip Toys 샘플 응용 프로그램을 기본 멤버 자격 데이터베이스를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-292">If you are following this tutorial using the **prebuilt** Wingtip Toys sample application, you must recreate the default membership database.</span></span> <span data-ttu-id="f5f52-293">기본 연결 문자열을 수정 하 여 멤버 자격 데이터베이스 응용 프로그램을 실행한 다음에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-293">By modifying the default connection string, the membership database will be created the next time the application runs.</span></span>

1. <span data-ttu-id="f5f52-294">엽니다는 *Web.config* 프로젝트의 루트에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-294">Open the *Web.config* file at the root of the project.</span></span>
2. <span data-ttu-id="f5f52-295">다음과 같이 표시 되도록 기본 연결 문자열을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-295">Update the default connection string so that it appears as follows:</span></span>   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a><span data-ttu-id="f5f52-296">PayPal 통합</span><span class="sxs-lookup"><span data-stu-id="f5f52-296">Integrating PayPal</span></span>

<span data-ttu-id="f5f52-297">PayPal는 온라인 merchants에서 지불을 수락 하는 웹 기반 청구 플랫폼.</span><span class="sxs-lookup"><span data-stu-id="f5f52-297">PayPal is a web-based billing platform that accepts payments by online merchants.</span></span> <span data-ttu-id="f5f52-298">이 자습서에는 다음 PayPal의 체크 아웃 Express 기능을 응용 프로그램에 통합 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-298">This tutorial next explains how to integrate PayPal's Express Checkout functionality into your application.</span></span> <span data-ttu-id="f5f52-299">빠른 체크 아웃 PayPal 해당 쇼핑 카트에 추가한 항목에 대 한 요금을 지불 하는 데 사용할 수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-299">Express Checkout allows your customers to use PayPal to pay for the items they have added to their shopping cart.</span></span>

### <a name="create-paypal-test-accounts"></a><span data-ttu-id="f5f52-300">PayPal 테스트 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f5f52-300">Create PayPal Test Accounts</span></span>

<span data-ttu-id="f5f52-301">테스트 환경 PayPal을 사용 하려면 만들고 해야 개발자 테스트 계정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-301">To use the PayPal testing environment, you must create and verify a developer test account.</span></span> <span data-ttu-id="f5f52-302">테스트 실행 계정 및 판매자 테스트 구매자를 만들려면 개발자 테스트 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-302">You will use the developer test account to create a buyer test account and a seller test account.</span></span> <span data-ttu-id="f5f52-303">또한 개발자 테스트 계정 자격 증명을 Wingtip Toys 샘플 응용 프로그램을 PayPal 테스트 환경에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-303">The developer test account credentials also will allow the Wingtip Toys sample application to access the PayPal testing environment.</span></span>

1. <span data-ttu-id="f5f52-304">브라우저에서 사이트를 테스트 하는 PayPal 개발자로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-304">In a browser, navigate to the PayPal developer testing site:</span></span>   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. <span data-ttu-id="f5f52-305">PayPal 개발자 계정이 없다면 새 계정을 클릭 하 여 만들 **등록**등록 단계를 수행 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-305">If you don't have a PayPal developer account, create a new account by clicking **Sign Up**and following the sign up steps.</span></span> <span data-ttu-id="f5f52-306">기존 PayPal 개발자 계정이 있는 경우 클릭 하 여 로그인 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-306">If you have an existing PayPal developer account, sign in by clicking **Log In**.</span></span> <span data-ttu-id="f5f52-307">PayPal 개발자 계정의이 자습서의 뒷부분에 나오는 Wingtip Toys 샘플 응용 프로그램을 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-307">You will need your PayPal developer account to test the Wingtip Toys sample application later in this tutorial.</span></span>
3. <span data-ttu-id="f5f52-308">PayPal 개발자 계정에 대 한 등록만, PayPal 사용 하 여 PayPal 개발자 계정을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-308">If you have just signed up for your PayPal developer account, you may need to verify your PayPal developer account with PayPal.</span></span> <span data-ttu-id="f5f52-309">PayPal 전자 메일 계정으로 전송 하는 단계를 수행 하 여 계정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-309">You can verify your account by following the steps that PayPal sent to your email account.</span></span> <span data-ttu-id="f5f52-310">PayPal 개발자 계정에 확인 한 후 다시 로그인 PayPal 개발자 사이트를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-310">Once you have verified your PayPal developer account, log back into the PayPal developer testing site.</span></span>
4. <span data-ttu-id="f5f52-311">이미 없다면 PayPal buyer 테스트 계정을 만들 필요가 PayPal 개발자 계정을 사용 하 여 PayPal 개발자 사이트에 로그인 후 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-311">After you are logged in to the PayPal developer site with your PayPal developer account you need to create a PayPal buyer test account if you don't already have one.</span></span> <span data-ttu-id="f5f52-312">PayPal 사이트 클릭 buyer 테스트 계정을 만들려면 합니다 **응용 프로그램** 탭을 클릭 한 다음 **샌드박스 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-312">To create a buyer test account, on the PayPal site click the **Applications** tab and then click **Sandbox accounts**.</span></span>   
 <span data-ttu-id="f5f52-313">합니다 **샌드박스 테스트 계정** 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-313">The **Sandbox test accounts** page is shown.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="f5f52-314">PayPal 개발자 사이트에는 이미 판매자 테스트 계정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-314">The PayPal Developer site already provides a merchant test account.</span></span>

    ![체크 아웃 및 PayPal-샌드박스 테스트 계정 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image15.png)
5. <span data-ttu-id="f5f52-316">샌드박스 테스트 계정 페이지에서 클릭 **계정 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-316">On the Sandbox test accounts page, click **Create Account**.</span></span>
6. <span data-ttu-id="f5f52-317">에 **테스트 계정 만들기** 페이지 테스트 계정 전자 메일 및 암호를 구매자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-317">On the **Create test account** page choose a buyer test account email and password of your choice.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="f5f52-318">Buyer 전자 메일 주소 및 암호를이 자습서의 끝에 Wingtip Toys 샘플 응용 프로그램을 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-318">You will need the buyer email addresses and password to test the Wingtip Toys sample application at the end of this tutorial.</span></span>

    ![체크 아웃 및 PayPal-샌드박스 테스트 계정 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image16.png)
7. <span data-ttu-id="f5f52-320">클릭 하 여 buyer 테스트 계정을 만들 합니다 **계정 만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-320">Create the buyer test account by clicking the **Create Account** button.</span></span>  
 <span data-ttu-id="f5f52-321">합니다 **샌드박스 테스트 계정** 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-321">The **Sandbox Test accounts** page is displayed.</span></span> 

    ![체크 아웃 및 PayPal-PayPal 계정으로 지불](checkout-and-payment-with-paypal/_static/image17.png)
8. <span data-ttu-id="f5f52-323">에 **샌드박스 테스트 계정** 페이지를 클릭 합니다 **진행자** 전자 메일 계정.</span><span class="sxs-lookup"><span data-stu-id="f5f52-323">On the **Sandbox test accounts** page, click the **facilitator** email account.</span></span>  
    <span data-ttu-id="f5f52-324">**프로필** 하 고 **알림** 옵션이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-324">**Profile** and **Notification** options appear.</span></span>
9. <span data-ttu-id="f5f52-325">선택 된 **프로필** 옵션을 선택한 다음 클릭 **API 자격 증명이** 판매자 테스트 계정에 대 한 API 자격 증명을 보려면.</span><span class="sxs-lookup"><span data-stu-id="f5f52-325">Select the **Profile** option, then click **API credentials** to view your API credentials for the merchant test account.</span></span>
10. <span data-ttu-id="f5f52-326">테스트 API 자격 증명이 메모장에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-326">Copy the TEST API credentials to notepad.</span></span>

<span data-ttu-id="f5f52-327">테스트 환경 PayPal 표시 클래식 API 테스트 자격 증명 (사용자 이름, 암호 및 서명) Wingtip Toys 샘플 응용 프로그램에서 API 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-327">You will need your displayed Classic TEST API credentials (Username, Password, and Signature) to make API calls from the Wingtip Toys sample application to the PayPal testing environment.</span></span> <span data-ttu-id="f5f52-328">다음 단계에서는 자격 증명을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-328">You will add the credentials in the next step.</span></span>

### <a name="add-paypal-class-and-api-credentials"></a><span data-ttu-id="f5f52-329">PayPal 클래스 및 API 자격 증명 추가</span><span class="sxs-lookup"><span data-stu-id="f5f52-329">Add PayPal Class and API Credentials</span></span>

<span data-ttu-id="f5f52-330">PayPal 코드의 대부분 단일 클래스에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-330">You will place the majority of the PayPal code into a single class.</span></span> <span data-ttu-id="f5f52-331">이 클래스는 PayPal을 사용 하 여 통신에 사용 된 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-331">This class contains the methods used to communicate with PayPal.</span></span> <span data-ttu-id="f5f52-332">또한이 클래스는 PayPal 자격 증명을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-332">Also, you will add your PayPal credentials to this class.</span></span>

1. <span data-ttu-id="f5f52-333">Visual Studio 내에서 Wingtip Toys 샘플 응용 프로그램을 마우스 오른쪽 단추로 클릭 합니다 **논리** 한 다음 선택한 폴더 **추가**  - &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-333">In the Wingtip Toys sample application within Visual Studio, right-click the **Logic** folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="f5f52-334">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-334">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="f5f52-335">아래 **Visual C#** 에서 합니다 **설치 됨** 창 왼쪽에서 선택 **코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-335">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span>
3. <span data-ttu-id="f5f52-336">가운데 창에서 선택 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-336">From the middle pane, select **Class**.</span></span> <span data-ttu-id="f5f52-337">이 새 클래스 이름을 **PayPalFunctions.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-337">Name this new class **PayPalFunctions.cs**.</span></span>
4. <span data-ttu-id="f5f52-338">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-338">Click **Add**.</span></span>  
   <span data-ttu-id="f5f52-339">새 클래스 파일을 편집기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-339">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="f5f52-340">기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-340">Replace the default code with the following code:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. <span data-ttu-id="f5f52-341">가맹점 API는 자격 증명 (사용자 이름, 암호 및 서명) PayPal 테스트 환경에 함수 호출을 만들 수 있도록이 자습서의 앞부분에서 표시를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-341">Add the Merchant API credentials (Username, Password, and Signature) that you displayed earlier in this tutorial so that you can make function calls to the PayPal testing environment.</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="f5f52-342">이 샘플 응용 프로그램에서 C# 파일 (.cs)를 자격 증명을 간단히 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-342">In this sample application you are simply adding credentials to a C# file (.cs).</span></span> <span data-ttu-id="f5f52-343">그러나 구현 된 솔루션에서는 구성 파일에서 자격 증명을 암호화 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-343">However, in a implemented solution, you should consider encrypting your credentials in a configuration file.</span></span>

<span data-ttu-id="f5f52-344">NVPAPICaller 클래스 PayPal 기능의 대부분을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-344">The NVPAPICaller class contains the majority of the PayPal functionality.</span></span> <span data-ttu-id="f5f52-345">클래스의 코드는 테스트 PayPal 테스트 환경에서 구매를 확인 하는 데 필요한 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-345">The code in the class provides the methods needed to make a test purchase from the PayPal testing environment.</span></span> <span data-ttu-id="f5f52-346">다음 세 가지 PayPal 함수를 구매 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-346">The following three PayPal functions are used to make purchases:</span></span>

- <span data-ttu-id="f5f52-347">`SetExpressCheckout` 함수</span><span class="sxs-lookup"><span data-stu-id="f5f52-347">`SetExpressCheckout` function</span></span>
- <span data-ttu-id="f5f52-348">`GetExpressCheckoutDetails` 함수</span><span class="sxs-lookup"><span data-stu-id="f5f52-348">`GetExpressCheckoutDetails` function</span></span>
- <span data-ttu-id="f5f52-349">`DoExpressCheckoutPayment` 함수</span><span class="sxs-lookup"><span data-stu-id="f5f52-349">`DoExpressCheckoutPayment` function</span></span>

<span data-ttu-id="f5f52-350">합니다 `ShortcutExpressCheckout` 장바구니와 호출 테스트 구매 정보 및 제품 세부 정보를 수집 하는 메서드는 `SetExpressCheckout` PayPal 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-350">The `ShortcutExpressCheckout` method collects the test purchase information and product details from the shopping cart and calls the `SetExpressCheckout` PayPal function.</span></span> <span data-ttu-id="f5f52-351">합니다 `GetCheckoutDetails` 메서드 호출 및 구매 정보를 확인 합니다 `GetExpressCheckoutDetails` 테스트 구매 하기 전에 PayPal 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-351">The `GetCheckoutDetails` method confirms purchase details and calls the `GetExpressCheckoutDetails` PayPal function before making the test purchase.</span></span> <span data-ttu-id="f5f52-352">합니다 `DoCheckoutPayment` 메서드를 호출 하 여 테스트 환경에서 테스트 구매를 완료 합니다 `DoExpressCheckoutPayment` PayPal 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-352">The `DoCheckoutPayment` method completes the test purchase from the testing environment by calling the `DoExpressCheckoutPayment` PayPal function.</span></span> <span data-ttu-id="f5f52-353">나머지 코드는 PayPal 메서드와 같은 문자열 인코딩, 디코딩 문자열, 배열 처리 및 자격 증명 확인 프로세스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-353">The remaining code supports the PayPal methods and process, such as encoding strings, decoding strings, processing arrays, and determining credentials.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f5f52-354">PayPal을 사용 하면 기준으로 선택적 구매 세부 정보를 포함할 수 있습니다 [PayPal의 API 사양](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-354">PayPal allows you to include optional purchase details based on [PayPal's API specification](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout).</span></span> <span data-ttu-id="f5f52-355">Wingtip Toys 샘플 응용 프로그램의 코드를 확장 하 여 다른 많은 선택적 필드 뿐만 아니라 지역화 세부 정보, 제품 설명, 세금, 고객 서비스 숫자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-355">By extending the code in the Wingtip Toys sample application, you can include localization details, product descriptions, tax, a customer service number, as well as many other optional fields.</span></span>

<span data-ttu-id="f5f52-356">반환 하 고 취소 Url에 지정 된 된 **ShortcutExpressCheckout** 메서드 포트 번호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-356">Notice that the return and cancel URLs that are specified in the **ShortcutExpressCheckout** method use a port number.</span></span>

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

<span data-ttu-id="f5f52-357">일반적으로 Visual Web Developer에서 SSL을 사용 하 여 웹 프로젝트를 실행 하는 경우 포트 44300 웹 서버에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-357">When Visual Web Developer runs a web project using SSL, commonly the port 44300 is used for the web server.</span></span> <span data-ttu-id="f5f52-358">위에 표시 된 것과 같이 포트 번호가 44300입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-358">As shown above, the port number is 44300.</span></span> <span data-ttu-id="f5f52-359">응용 프로그램을 실행 하는 경우 다른 포트 번호를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-359">When you run the application, you could see a different port number.</span></span> <span data-ttu-id="f5f52-360">올바르게 설정할 코드에서 수행할 수 있도록 성공 하기 위해 포트 번호 요구 사항이이 자습서의 끝에 Wingtip Toys 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-360">Your port number needs to be correctly set in the code so that you can successful run the Wingtip Toys sample application at the end of this tutorial.</span></span> <span data-ttu-id="f5f52-361">이 자습서의 다음 섹션에는 로컬 호스트 포트 번호를 검색 하 여 PayPal 클래스를 업데이트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-361">The next section of this tutorial explains how to retrieve the local host port number and update the PayPal class.</span></span>

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a><span data-ttu-id="f5f52-362">PayPal 클래스에 LocalHost 포트 번호를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-362">Update the LocalHost Port Number in the PayPal Class</span></span>

<span data-ttu-id="f5f52-363">Wingtip Toys 샘플 응용 프로그램 PayPal 테스트 사이트로 이동 하 고 Wingtip Toys 샘플 응용 프로그램의 로컬 인스턴스를 반환 하 여 제품을 구입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-363">The Wingtip Toys sample application purchases products by navigating to the PayPal testing site and returning to your local instance of the Wingtip Toys sample application.</span></span> <span data-ttu-id="f5f52-364">로컬로 실행 하는 포트 번호를 지정 해야 올바른 URL을 반환 하는 PayPal을 가지려면 위에서 언급 한 PayPal 코드에서 응용 프로그램 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-364">In order to have PayPal return to the correct URL, you need to specify the port number of the locally running sample application in the PayPal code mentioned above.</span></span>

1. <span data-ttu-id="f5f52-365">프로젝트 이름을 마우스 오른쪽 단추로 클릭 (**WingtipToys**)에서 **솔루션 탐색기** 선택한 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-365">Right-click the project name (**WingtipToys**) in **Solution Explorer** and select **Properties**.</span></span>
2. <span data-ttu-id="f5f52-366">왼쪽된 열에서 선택 합니다 **웹** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-366">In the left column, select the **Web** tab.</span></span>
3. <span data-ttu-id="f5f52-367">포트 번호를 검색 합니다 **프로젝트 Url** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-367">Retrieve the port number from the **Project Url** box.</span></span>
4. <span data-ttu-id="f5f52-368">필요한 경우 업데이트를 `returnURL` 하 고 `cancelURL` PayPal 클래스에서 (`NVPAPICaller`)에 *PayPalFunctions.cs* 웹 응용 프로그램의 포트 번호를 사용 하는 파일:</span><span class="sxs-lookup"><span data-stu-id="f5f52-368">If needed, update the `returnURL` and `cancelURL` in the PayPal class (`NVPAPICaller`) in the *PayPalFunctions.cs* file to use the port number of your web application:</span></span>   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

<span data-ttu-id="f5f52-369">이제 추가한 코드는 로컬 웹 응용 프로그램에 대 한 예상 된 포트를 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-369">Now the code that you added will match the expected port for your local Web application.</span></span> <span data-ttu-id="f5f52-370">PayPal 로컬 컴퓨터에 올바른 URL을 반환 하는 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-370">PayPal will be able to return to the correct URL on your local machine.</span></span>

### <a name="add-the-paypal-checkout-button"></a><span data-ttu-id="f5f52-371">PayPal 체크 아웃 단추를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-371">Add the PayPal Checkout Button</span></span>

<span data-ttu-id="f5f52-372">샘플 응용 프로그램에 추가 된 기본 PayPal 함수는 했으므로 이러한 함수를 호출 하는 데 필요한 코드 및 태그 추가 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-372">Now that the primary PayPal functions have been added to the sample application, you can begin adding the markup and code needed to call these functions.</span></span> <span data-ttu-id="f5f52-373">첫째, 사용자는 쇼핑 카트 페이지에 표시 되는 체크 아웃 단추를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-373">First, you must add the checkout button that the user will see on the shopping cart page.</span></span>

1. <span data-ttu-id="f5f52-374">엽니다는 *ShoppingCart.aspx* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-374">Open the *ShoppingCart.aspx* file.</span></span>
2. <span data-ttu-id="f5f52-375">파일의 아래쪽으로 스크롤하여 찾을 `<!--Checkout Placeholder -->` 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-375">Scroll to the bottom of the file and find the `<!--Checkout Placeholder -->` comment.</span></span>
3. <span data-ttu-id="f5f52-376">주석을 사용 하 여는 `ImageButton` 마크업은 다음과 같은 대체를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-376">Replace the comment with an `ImageButton` control so that the mark up is replaced as follows:</span></span>  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. <span data-ttu-id="f5f52-377">에 *ShoppingCart.aspx.cs* 파일을 후 합니다 `UpdateBtn_Click` 파일의 끝 부분에 대 한 이벤트 처리기 추가 `CheckOutBtn_Click` 이벤트 처리기:</span><span class="sxs-lookup"><span data-stu-id="f5f52-377">In the *ShoppingCart.aspx.cs* file, after the `UpdateBtn_Click` event handler near the end of the file, add the `CheckOutBtn_Click` event handler:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. <span data-ttu-id="f5f52-378">또한를 *ShoppingCart.aspx.cs* 파일에 대 한 참조를 추가 합니다는 `CheckoutBtn`새 이미지 단추는 다음과 같이 참조 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-378">Also in the *ShoppingCart.aspx.cs* file, add a reference to the `CheckoutBtn`, so that the new image button is referenced as follows:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. <span data-ttu-id="f5f52-379">변경 내용을 모두 저장 합니다 *ShoppingCart.aspx* 파일 및 *ShoppingCart.aspx.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-379">Save your changes to both the *ShoppingCart.aspx* file and the *ShoppingCart.aspx.cs* file.</span></span>
7. <span data-ttu-id="f5f52-380">메뉴에서 선택 **디버깅할**-&gt;**빌드 WingtipToys**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-380">From the menu, select **Debug**-&gt;**Build WingtipToys**.</span></span>  
   <span data-ttu-id="f5f52-381">프로젝트를 다시 작성 됩니다 새로 추가 된 **ImageButton** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-381">The project will be rebuilt with the newly added **ImageButton** control.</span></span>

### <a name="send-purchase-details-to-paypal"></a><span data-ttu-id="f5f52-382">PayPal 구매 정보 보내기</span><span class="sxs-lookup"><span data-stu-id="f5f52-382">Send Purchase Details to PayPal</span></span>

<span data-ttu-id="f5f52-383">클릭할 때 합니다 **체크 아웃** 쇼핑 카트 페이지에서 단추 (*ShoppingCart.aspx*), 구매 프로세스 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-383">When the user clicks the **Checkout** button on the shopping cart page (*ShoppingCart.aspx*), they'll begin the purchase process.</span></span> <span data-ttu-id="f5f52-384">다음 코드는 제품을 구매 하는 데 필요한 첫 번째 PayPal 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-384">The following code calls the first PayPal function needed to purchase products.</span></span>

1. <span data-ttu-id="f5f52-385">*체크 아웃* 폴더를 열고 코드 숨김 파일의 이름은 *CheckoutStart.aspx.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-385">From the *Checkout* folder, open the code-behind file named *CheckoutStart.aspx.cs*.</span></span>   
   <span data-ttu-id="f5f52-386">코드 숨김 파일을 열고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-386">Be sure to open the code-behind file.</span></span>
2. <span data-ttu-id="f5f52-387">기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-387">Replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

<span data-ttu-id="f5f52-388">응용 프로그램의 사용자가 클릭할 때 합니다 **체크 아웃** 쇼핑 카트 페이지 브라우저에서 단추 이동 합니다 *CheckoutStart.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="f5f52-388">When the user of the application clicks the **Checkout** button on the shopping cart page, the browser will navigate to the *CheckoutStart.aspx* page.</span></span> <span data-ttu-id="f5f52-389">경우는 *CheckoutStart.aspx* 로드 페이지는 `ShortcutExpressCheckout` 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-389">When the *CheckoutStart.aspx* page loads, the `ShortcutExpressCheckout` method is called.</span></span> <span data-ttu-id="f5f52-390">이 시점에서 사용자는 PayPal 테스트 웹 사이트로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-390">At this point, the user is transferred to the PayPal testing web site.</span></span> <span data-ttu-id="f5f52-391">PayPal 사이트에서 사용자 PayPal 자격 증명을 입력, 구매 정보를 검토, PayPal 계약에 동의 및 Wingtip Toys 샘플 응용 프로그램에 반환 합니다. 여기서는 `ShortcutExpressCheckout` 메서드가 완료 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-391">On the PayPal site, the user enters their PayPal credentials, reviews the purchase details, accepts the PayPal agreement and returns to the Wingtip Toys sample application where the `ShortcutExpressCheckout` method completes.</span></span> <span data-ttu-id="f5f52-392">경우는 `ShortcutExpressCheckout` 메서드가 완료 되 면 사용자를 리디렉션할 수는 *CheckoutReview.aspx* 에 지정 된 페이지는 `ShortcutExpressCheckout` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f5f52-392">When the `ShortcutExpressCheckout` method is complete, it will redirect the user to the *CheckoutReview.aspx* page specified in the `ShortcutExpressCheckout` method.</span></span> <span data-ttu-id="f5f52-393">이 Wingtip Toys 샘플 응용 프로그램 내에서 주문 세부 정보를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-393">This allows the user to review the order details from within the Wingtip Toys sample application.</span></span>

### <a name="review-order-details"></a><span data-ttu-id="f5f52-394">주문 세부 정보 검토</span><span class="sxs-lookup"><span data-stu-id="f5f52-394">Review Order Details</span></span>

<span data-ttu-id="f5f52-395">PayPal에서 반환 된 후의 *CheckoutReview.aspx* Wingtip Toys 샘플 응용 프로그램의 페이지에 주문 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-395">After returning from PayPal, the *CheckoutReview.aspx* page of the Wingtip Toys sample application displays the order details.</span></span> <span data-ttu-id="f5f52-396">이 페이지에서는 사용자가 제품을 구입 하기 전에 주문 세부 정보를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-396">This page allows the user to review the order details before purchasing the products.</span></span> <span data-ttu-id="f5f52-397">합니다 *CheckoutReview.aspx* 페이지를 다음과 같이 만들 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-397">The *CheckoutReview.aspx* page must be created as follows:</span></span>

1. <span data-ttu-id="f5f52-398">에 *체크 아웃* 폴더를 열고 페이지 라는 *CheckoutReview.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-398">In the *Checkout* folder, open the page named *CheckoutReview.aspx*.</span></span>
2. <span data-ttu-id="f5f52-399">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-399">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. <span data-ttu-id="f5f52-400">라는 코드 숨김 페이지를 엽니다 *CheckoutReview.aspx.cs* 기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-400">Open the code-behind page named *CheckoutReview.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

<span data-ttu-id="f5f52-401">합니다 **DetailsView** PayPal에서 반환 된 주문 세부 정보를 표시할 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-401">The **DetailsView** control is used to display the order details that have been returned from PayPal.</span></span> <span data-ttu-id="f5f52-402">위의 코드도 Wingtip Toys 데이터베이스에 주문 세부 정보를 저장 하는 또한는 `OrderDetail` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-402">Also, the above code saves the order details to the Wingtip Toys database as an `OrderDetail` object.</span></span> <span data-ttu-id="f5f52-403">사용자가 클릭할 때 합니다 **Complete Order** 리디렉션됩니다 단추를 *CheckoutComplete.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="f5f52-403">When the user clicks on the **Complete Order** button, they are redirected to the *CheckoutComplete.aspx* page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="f5f52-404">**팁**</span><span class="sxs-lookup"><span data-stu-id="f5f52-404">**Tip**</span></span>
> 
> <span data-ttu-id="f5f52-405">태그에는 *CheckoutReview.aspx* 페이지에서 `<ItemStyle>` 태그에서 항목의 스타일을 변경 하는 합니다 **DetailsView** 페이지 하단에 있는 컨트롤.</span><span class="sxs-lookup"><span data-stu-id="f5f52-405">In the markup of the *CheckoutReview.aspx* page, notice that the `<ItemStyle>` tag is used to change the style of the items within the **DetailsView** control near the bottom of the page.</span></span> <span data-ttu-id="f5f52-406">페이지를 확인 하 여 **디자인 뷰** (선택 하 여 **디자인** Visual Studio의 왼쪽된 아래 모서리에), 다음을 선택 하는 **DetailsView** 컨트롤을 선택 합니다  **스마트 태그** (맨 위에 있는 화살표 아이콘 컨트롤의 오른쪽)를 볼 수는 **DetailsView 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-406">By viewing the page in **Design View** (by selecting **Design** at the lower left corner of Visual Studio), then selecting the **DetailsView** control, and selecting the **Smart Tag** (the arrow icon at the top right of the control), you will be able to see the **DetailsView Tasks**.</span></span>
> 
> ![체크 아웃 및 지불 PayPal-를 사용 하 여 필드를 편집](checkout-and-payment-with-paypal/_static/image18.png)
> 
> <span data-ttu-id="f5f52-408">선택 하 여 **필드 편집**서 **필드** 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-408">By selecting **Edit Fields**, the **Fields** dialog box will appear.</span></span> <span data-ttu-id="f5f52-409">이 대화 상자에서 쉽게 제어할 수 있습니다 시각적 속성을 같은 **ItemStyle**의 합니다 **DetailsView** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-409">In this dialog box you can easily control the visual properties, such as **ItemStyle**, of the **DetailsView** control.</span></span>
> 
> ![체크 아웃 및 PayPal-필드 대화 상자를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a><span data-ttu-id="f5f52-411">구매를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-411">Complete Purchase</span></span>

<span data-ttu-id="f5f52-412">*CheckoutComplete.aspx* 페이지 PayPal에서 구매를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-412">*CheckoutComplete.aspx* page makes the purchase from PayPal.</span></span> <span data-ttu-id="f5f52-413">사용자 클릭 해야 위에서 설명 했 듯이 합니다 **Complete Order** 응용 프로그램으로 이동 하기 전에 단추를 *CheckoutComplete.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-413">As mentioned above, the user must click on the **Complete Order** button before the application will navigate to the *CheckoutComplete.aspx* page.</span></span>

1. <span data-ttu-id="f5f52-414">에 *체크 아웃* 폴더를 열고 페이지 라는 *CheckoutComplete.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-414">In the *Checkout* folder, open the page named *CheckoutComplete.aspx*.</span></span>
2. <span data-ttu-id="f5f52-415">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-415">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. <span data-ttu-id="f5f52-416">라는 코드 숨김 페이지를 엽니다 *CheckoutComplete.aspx.cs* 기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-416">Open the code-behind page named *CheckoutComplete.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

<span data-ttu-id="f5f52-417">경우는 *CheckoutComplete.aspx* 페이지가 로드 되는 `DoCheckoutPayment` 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-417">When the *CheckoutComplete.aspx* page is loaded, the `DoCheckoutPayment` method is called.</span></span> <span data-ttu-id="f5f52-418">앞서 언급 했 듯이 `DoCheckoutPayment` 메서드 PayPal 테스트 환경에서 구매를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-418">As mentioned earlier, the `DoCheckoutPayment` method completes the purchase from the PayPal testing environment.</span></span> <span data-ttu-id="f5f52-419">PayPal 구매 주문을 완료 되 면 합니다 *CheckoutComplete.aspx* 지불 트랜잭션을 표시 하는 페이지 `ID` 구매자 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-419">Once PayPal has completed the purchase of the order, the *CheckoutComplete.aspx* page displays a payment transaction `ID` to the purchaser.</span></span>

### <a name="handle-cancel-purchase"></a><span data-ttu-id="f5f52-420">구매 취소를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-420">Handle Cancel Purchase</span></span>

<span data-ttu-id="f5f52-421">사용자를 구매를 취소 하기로 한 경우 리디렉션됩니다에 *CheckoutCancel.aspx* 페이지는 표시 순서 취소 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-421">If the user decides to cancel the purchase, they will be directed to the *CheckoutCancel.aspx* page where they will see that their order has been cancelled.</span></span>

1. <span data-ttu-id="f5f52-422">라는 페이지를 엽니다 *CheckoutCancel.aspx* 에 *체크 아웃* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-422">Open the page named *CheckoutCancel.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="f5f52-423">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-423">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a><span data-ttu-id="f5f52-424">구매 오류 처리</span><span class="sxs-lookup"><span data-stu-id="f5f52-424">Handle Purchase Errors</span></span>

<span data-ttu-id="f5f52-425">오류 구매 과정에서 처리 되는 합니다 *CheckoutError.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-425">Errors during the purchase process will be handled by the *CheckoutError.aspx* page.</span></span> <span data-ttu-id="f5f52-426">코드 숨김 합니다 *CheckoutStart.aspx* 페이지를 *CheckoutReview.aspx* 페이지 및 *CheckoutComplete.aspx* 페이지 각 리디렉션됩니다는  *CheckoutError.aspx* 페이지 오류가 발생 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="f5f52-426">The code-behind of the *CheckoutStart.aspx* page, the *CheckoutReview.aspx* page, and the *CheckoutComplete.aspx* page will each redirect to the *CheckoutError.aspx* page if an error occurs.</span></span>

1. <span data-ttu-id="f5f52-427">라는 페이지를 엽니다 *CheckoutError.aspx* 에 *체크 아웃* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-427">Open the page named *CheckoutError.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="f5f52-428">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-428">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

<span data-ttu-id="f5f52-429">합니다 *CheckoutError.aspx* 체크 아웃 프로세스 중에 오류가 발생 하는 경우 오류 세부 정보를 사용 하 여 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-429">The *CheckoutError.aspx* page is displayed with the error details when an error occurs during the checkout process.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="f5f52-430">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="f5f52-430">Running the Application</span></span>

<span data-ttu-id="f5f52-431">제품을 구매 하는 방법은 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-431">Run the application to see how to purchase products.</span></span> <span data-ttu-id="f5f52-432">실행 된 PayPal에서 테스트 환경 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-432">Note that you will be running in the PayPal testing environment.</span></span> <span data-ttu-id="f5f52-433">실제 미지불 교환 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-433">No actual money is being exchanged.</span></span>

1. <span data-ttu-id="f5f52-434">Visual Studio에서 파일은 모든 했는지 확인.</span><span class="sxs-lookup"><span data-stu-id="f5f52-434">Make sure all your files are saved in Visual Studio.</span></span>
2. <span data-ttu-id="f5f52-435">웹 브라우저를 열고 이동할 [ https://developer.paypal.com ](https://developer.paypal.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-435">Open a Web browser and navigate to [https://developer.paypal.com](https://developer.paypal.com/).</span></span>
3. <span data-ttu-id="f5f52-436">이 자습서의 앞부분에서 만든 PayPal 개발자 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-436">Login with your PayPal developer account that you created earlier in this tutorial.</span></span>  
   <span data-ttu-id="f5f52-437">PayPal의 개발자 sandbox에 로그인 할 필요가 [ https://developer.paypal.com ](https://developer.paypal.com/) express 체크 아웃을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-437">For PayPal's developer sandbox, you need to be logged in at [https://developer.paypal.com](https://developer.paypal.com/) to test express checkout.</span></span> <span data-ttu-id="f5f52-438">이 테스트, PayPal의 라이브 환경 필요가 PayPal의 샌드박스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-438">This only applies to PayPal's sandbox testing, not to PayPal's live environment.</span></span>
4. <span data-ttu-id="f5f52-439">Visual Studio에서 눌러 **F5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-439">In Visual Studio, press **F5** to run the Wingtip Toys sample application.</span></span>  
   <span data-ttu-id="f5f52-440">브라우저를 열고 표시 데이터베이스 다시 작성 후 합니다 *Default.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-440">After the database rebuilds, the browser will open and show the *Default.aspx* page.</span></span>
5. <span data-ttu-id="f5f52-441">"자동차"와 같은 제품 범주를 선택한 다음 클릭 하 여 다양 한 제품이 쇼핑 카트에 추가 **카트에 추가** 각 제품 옆에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-441">Add three different products to the shopping cart by selecting the product category, such as "Cars" and then clicking **Add to Cart** next to each product.</span></span>  
   <span data-ttu-id="f5f52-442">쇼핑 카트는 선택한 제품을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-442">The shopping cart will display the product you have selected.</span></span>
6. <span data-ttu-id="f5f52-443">클릭 합니다 **PayPal** 체크 아웃 하는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-443">Click the **PayPal** button to checkout.</span></span> 

    ![체크 아웃 및 PayPal-카트를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image20.png)

   <span data-ttu-id="f5f52-445">체크 아웃 해야 Wingtip Toys 샘플 응용 프로그램에 대 한 사용자 계정이 있다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-445">Checking out will require that you have a user account for the Wingtip Toys sample application.</span></span>
7. <span data-ttu-id="f5f52-446">클릭 합니다 **Google** 기존 gmail.com 전자 메일 계정으로 로그인 페이지의 오른쪽에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-446">Click the **Google** link on the right of the page to log in with an existing gmail.com email account.</span></span>  
   <span data-ttu-id="f5f52-447">Gmail.com 계정이 없는 경우에 테스트용 하나를 만들 수 있습니다 [www.gmail.com](https://www.gmail.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-447">If you do not have a gmail.com account, you can create one for testing purposes at [www.gmail.com](https://www.gmail.com/).</span></span> <span data-ttu-id="f5f52-448">또한 "등록"을 클릭 하 여 표준 로컬 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-448">You can also use a standard local account by clicking "Register".</span></span> 

    ![체크 아웃 및 지불 PayPal-를 사용 하 여 로그인](checkout-and-payment-with-paypal/_static/image21.png)
8. <span data-ttu-id="f5f52-450">Gmail 계정 및 암호를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-450">Sign in with your gmail account and password.</span></span> 

    ![체크 아웃 및 PayPal-Gmail 로그인을 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image22.png)
9. <span data-ttu-id="f5f52-452">클릭 합니다 **로그인** Wingtip Toys 샘플 응용 프로그램 사용자 이름에 gmail 계정을 등록 하는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-452">Click the **Log in** button to register your gmail account with your Wingtip Toys sample application user name.</span></span> 

    ![체크 아웃 및 PayPal-등록 계정 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image23.png)
10. <span data-ttu-id="f5f52-454">PayPal 테스트 사이트에서 추가 프로그램 **buyer** 전자 메일 주소 및이 자습서의 앞부분에서 만든 암호를 클릭 합니다 **로그인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-454">On the PayPal test site, add your **buyer** email address and password that you created earlier in this tutorial, then click the **Log In** button.</span></span> 

    ![체크 아웃 및 PayPal-PayPal 로그인을 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image24.png)
11. <span data-ttu-id="f5f52-456">PayPal 정책에 동의 하 고 클릭 합니다 **동의 함 및 계속** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-456">Agree to the PayPal policy and click the **Agree and Continue** button.</span></span>  
    <span data-ttu-id="f5f52-457">이 페이지는만 보면이 PayPal 계정을 사용 하 여 처음으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-457">Note that this page is only displayed the first time you use this PayPal account.</span></span> <span data-ttu-id="f5f52-458">이것은 테스트 계정에 실제 미지불 교환 note 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-458">Again note that this is a test account, no real money is exchanged.</span></span> 

    ![체크 아웃 및 PayPal-PayPal 정책을 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image25.png)
12. <span data-ttu-id="f5f52-460">테스트 환경 검토 페이지 및 클릭 PayPal에서 주문 정보를 검토할 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-460">Review the order information on the PayPal testing environment review page and click **Continue**.</span></span> 

    ![체크 아웃 및 PayPal-검토 정보를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image26.png)
13. <span data-ttu-id="f5f52-462">에 *CheckoutReview.aspx* 페이지에서 주문 금액을 확인 하 고 생성 된 배송 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-462">On the *CheckoutReview.aspx* page, verify the order amount and view the generated shipping address.</span></span> <span data-ttu-id="f5f52-463">클릭 합니다 **Complete Order** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-463">Then, click the **Complete Order** button.</span></span> 

    ![체크 아웃 및 PayPal-순서 검토를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image27.png)
14. <span data-ttu-id="f5f52-465">합니다 **CheckoutComplete.aspx** 페이지는 지불 트랜잭션 id</span><span class="sxs-lookup"><span data-stu-id="f5f52-465">The **CheckoutComplete.aspx** page is displayed with a payment transaction ID.</span></span> 

    ![체크 아웃 및 PayPal-전체 체크 아웃을 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a><span data-ttu-id="f5f52-467">데이터베이스를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-467">Reviewing the Database</span></span>

<span data-ttu-id="f5f52-468">응용 프로그램을 실행 한 후 Wingtip Toys 샘플 응용 프로그램 데이터베이스의 업데이트 된 데이터를 검토 하 여 응용 프로그램에 성공적으로 제품의 구매 기록 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-468">By reviewing the updated data in the Wingtip Toys sample application database after running the application, you can see that the application successfully recorded the purchase of the products.</span></span>

<span data-ttu-id="f5f52-469">포함 된 데이터를 검사할 수 있습니다 합니다 *Wingtiptoys.mdf* 사용 하 여 데이터베이스 파일을 **데이터베이스 탐색기** 창 (**서버 탐색기** Visual Studio의 창) 수행한 것 처럼 이 자습서 시리즈의 앞부분에 나오는.</span><span class="sxs-lookup"><span data-stu-id="f5f52-469">You can inspect the data contained in the *Wingtiptoys.mdf* database file by using the **Database Explorer** window (**Server Explorer** window in Visual Studio) as you did earlier in this tutorial series.</span></span>

1. <span data-ttu-id="f5f52-470">열려 있는 경우 브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-470">Close the browser window if it is still open.</span></span>
2. <span data-ttu-id="f5f52-471">Visual Studio에서 선택 합니다 **모든 파일 표시** 맨 위에 있는 아이콘 **솔루션 탐색기** 확장할 수 있도록 합니다 **앱\_데이터** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-471">In Visual Studio, select the **Show All Files** icon at the top of **Solution Explorer** to allow you to expand the **App\_Data** folder.</span></span>
3. <span data-ttu-id="f5f52-472">확장 된 **앱\_데이터** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-472">Expand the **App\_Data** folder.</span></span>  
 <span data-ttu-id="f5f52-473">선택 해야 합니다 **모든 파일 표시** 폴더에 대 한 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-473">You may need to select the **Show All Files** icon for the folder.</span></span>
4. <span data-ttu-id="f5f52-474">마우스 오른쪽 단추로 클릭 합니다 *Wingtiptoys.mdf* 데이터베이스 파일 및 선택 **오픈**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-474">Right-click the *Wingtiptoys.mdf* database file and select **Open**.</span></span>  
    <span data-ttu-id="f5f52-475">**서버 탐색기** 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-475">**Server Explorer** is displayed.</span></span>
5. <span data-ttu-id="f5f52-476">**테이블** 폴더를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-476">Expand the **Tables** folder.</span></span>
6. <span data-ttu-id="f5f52-477">마우스 오른쪽 단추로 클릭 합니다 **주문을**선택한 테이블 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-477">Right-click the **Orders**table and select **Show Table Data**.</span></span>  
 <span data-ttu-id="f5f52-478">합니다 **주문** 테이블이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-478">The **Orders** table is displayed.</span></span>
7. <span data-ttu-id="f5f52-479">검토 합니다 **PaymentTransactionID** 성공적인 트랜잭션을 확인 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-479">Review the **PaymentTransactionID** column to confirm successful transactions.</span></span> 

    ![체크 아웃 및 PayPal-검토 데이터베이스를 사용 하 여 지불](checkout-and-payment-with-paypal/_static/image29.png)
8. <span data-ttu-id="f5f52-481">닫기 합니다 **주문** 테이블 창입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-481">Close the **Orders** table window.</span></span>
9. <span data-ttu-id="f5f52-482">서버 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 **OrderDetails** 선택한 테이블 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-482">In the Server Explorer, right-click the **OrderDetails** table and select **Show Table Data**.</span></span>
10. <span data-ttu-id="f5f52-483">검토를 `OrderId` 하 고 `Username` 값을 **OrderDetails** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-483">Review the `OrderId` and `Username` values in the **OrderDetails** table.</span></span> <span data-ttu-id="f5f52-484">이러한 값과 일치 하는 참고 합니다 `OrderId` 및 `Username` 에 포함 된 값을 **주문** 테이블.</span><span class="sxs-lookup"><span data-stu-id="f5f52-484">Note that these values match the `OrderId` and `Username` values included in the **Orders** table.</span></span>
11. <span data-ttu-id="f5f52-485">닫기 합니다 **OrderDetails** 테이블 창입니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-485">Close the **OrderDetails** table window.</span></span>
12. <span data-ttu-id="f5f52-486">Wingtip Toys 데이터베이스 파일을 마우스 오른쪽 단추로 클릭 (*Wingtiptoys.mdf*)을 선택 하 고 **근접 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-486">Right-click the Wingtip Toys database file (*Wingtiptoys.mdf*) and select **Close Connection**.</span></span>
13. <span data-ttu-id="f5f52-487">표시 되지 않으면 합니다 **솔루션 탐색기** 창 클릭 **솔루션 탐색기** 맨 아래에 **서버 탐색기** 표시할 창은 **솔루션 탐색기**  다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-487">If you do not see the **Solution Explorer** window, click **Solution Explorer** at the bottom of the **Server Explorer** window to show the **Solution Explorer** again.</span></span>

## <a name="summary"></a><span data-ttu-id="f5f52-488">요약</span><span class="sxs-lookup"><span data-stu-id="f5f52-488">Summary</span></span>

<span data-ttu-id="f5f52-489">이 자습서에서는 제품 구매를 추적 하는 주문과 주문 세부 정보 스키마를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-489">In this tutorial you added order and order detail schemas to track the purchase of products.</span></span> <span data-ttu-id="f5f52-490">또한 Wingtip Toys 샘플 응용 프로그램에 PayPal 기능을 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-490">You also integrated PayPal functionality into the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5f52-491">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f5f52-491">Additional Resources</span></span>

<span data-ttu-id="f5f52-492">[ASP.NET 구성 개요](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="f5f52-492">[ASP.NET Configuration Overview](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span></span>  
[<span data-ttu-id="f5f52-493">멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET Web Forms 앱을 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="f5f52-493">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="f5f52-494">Microsoft Azure 무료 평가판</span><span class="sxs-lookup"><span data-stu-id="f5f52-494">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a><span data-ttu-id="f5f52-495">고지 사항</span><span class="sxs-lookup"><span data-stu-id="f5f52-495">Disclaimer</span></span>

<span data-ttu-id="f5f52-496">이 자습서는 샘플 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-496">This tutorial contains sample code.</span></span> <span data-ttu-id="f5f52-497">이러한 샘플 코드는 어떤 종류의 보증 없이 "있는 그대로" 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-497">Such sample code is provided "as is" without warranty of any kind.</span></span> <span data-ttu-id="f5f52-498">따라서 Microsoft는 정확도, 무결성 또는 샘플 코드의 품질을 보장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-498">Accordingly, Microsoft does not guarantee the accuracy, integrity, or quality of the sample code.</span></span> <span data-ttu-id="f5f52-499">샘플 코드를 사용 하 여 사용자의 책임에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-499">You agree to use the sample code at your own risk.</span></span> <span data-ttu-id="f5f52-500">어떠한 상황는 Microsoft 지지를 어떤 방식으로 모든 샘플 코드의 경우 콘텐츠를 포함 하지만 여기에 오류나 누락 모든 샘플 코드, 콘텐츠, 손실 또는 모든 샘플 코드 사용으로 인해 발생 한 모든 종류의 손해에 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-500">Under no circumstances will Microsoft be liable to you in any way for any sample code, content, including but not limited to, any errors or omissions in any sample code, content, or any loss or damage of any kind incurred as a result of the use of any sample code.</span></span> <span data-ttu-id="f5f52-501">이로써 알림이 표시 됩니다 및 배상, 저장 하며 Microsoft에서 모든 손실, 손실, 부상 또는 손상 종류 비롯, 제한 없이 여 occasioned 또는 자료를 게시 하면는에서 발생 하는 클레임에 대 한 동의 통지가 수행 전송에서 사용 하거나 여기 견해에 국한 되지 않음 등을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5f52-501">You are hereby notified and do hereby agree to indemnify, save and hold Microsoft harmless from and against any and all loss, claims of loss, injury or damage of any kind including, without limitation, those occasioned by or arising from material that you post, transmit, use or rely on including, but not limited to, the views expressed therein.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f5f52-502">[이전](shopping-cart.md)
> [다음](membership-and-administration.md)</span><span class="sxs-lookup"><span data-stu-id="f5f52-502">[Previous](shopping-cart.md)
[Next](membership-and-administration.md)</span></span>
