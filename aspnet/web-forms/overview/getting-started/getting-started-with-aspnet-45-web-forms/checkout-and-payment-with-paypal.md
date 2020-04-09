---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 페이팔로 결제 및 결제 | 마이크로 소프트 문서
author: Erikre
description: 이 튜토리얼 시리즈는 ASP.NET 4.5및 Microsoft Visual Studio Express 2013을 사용하여 ASP.NET 웹 폼 응용 프로그램을 빌드하는 기본 정보를 가르쳐 드립니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675690"
---
# <a name="checkout-and-payment-with-paypal"></a><span data-ttu-id="897d9-103">PayPal로 체크 아웃 및 지불</span><span class="sxs-lookup"><span data-stu-id="897d9-103">Checkout and Payment with PayPal</span></span>

<span data-ttu-id="897d9-104">로 [에릭 레이탄](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="897d9-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="897d9-105">[Wingtip 장난감 샘플 프로젝트 다운로드 (C #)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 책 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="897d9-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="897d9-106">이 자습서 시리즈에서는 웹용 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용하여 ASP.NET 웹 양식 응용 프로그램을 빌드하는 기본 정보를 강의합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="897d9-107">[C# 소스 코드가 있는](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) Visual Studio 2013 프로젝트를 이 자습서 시리즈와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="897d9-108">이 자습서에서는 PayPal을 사용하여 사용자 권한 부여, 등록 및 지불을 포함하도록 Wingtip Toys 샘플 응용 프로그램을 수정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-108">This tutorial describes how to modify the Wingtip Toys sample application to include user authorization, registration, and payment using PayPal.</span></span> <span data-ttu-id="897d9-109">로그인한 사용자만 제품을 구매할 수 있는 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-109">Only users who are logged in will have authorization to purchase products.</span></span> <span data-ttu-id="897d9-110">ASP.NET 4.5 Web Forms 프로젝트 템플릿의 기본 제공 사용자 등록 기능에는 이미 필요한 것이 많이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-110">The ASP.NET 4.5 Web Forms project template's built-in user registration functionality already includes much of what you need.</span></span> <span data-ttu-id="897d9-111">페이팔 익스프레스 체크아웃 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-111">You will add PayPal Express Checkout functionality.</span></span> <span data-ttu-id="897d9-112">이 튜토리얼에서는 PayPal 개발자 테스트 환경을 사용하므로 실제 자금이 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-112">In this tutorial you be using the PayPal developer testing environment, so no actual funds will be transferred.</span></span> <span data-ttu-id="897d9-113">자습서의 끝에서, 당신은 쇼핑 카트에 추가 할 제품을 선택하여 응용 프로그램을 테스트합니다, 체크 아웃 버튼을 클릭, PayPal 테스트 웹 사이트에 데이터를 전송.</span><span class="sxs-lookup"><span data-stu-id="897d9-113">At the end of the tutorial, you will test the application by selecting products to add to the shopping cart, clicking the checkout button, and transferring data to the PayPal testing web site.</span></span> <span data-ttu-id="897d9-114">PayPal 테스트 웹 사이트에서 배송 및 결제 정보를 확인한 다음 현지 Wingtip Toys 샘플 응용 프로그램으로 돌아가 구매를 확인하고 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-114">On the PayPal testing web site, you will confirm your shipping and payment information and then return to the local Wingtip Toys sample application to confirm and complete the purchase.</span></span>

<span data-ttu-id="897d9-115">확장성과 보안을 다루는 온라인 쇼핑을 전문으로 하는 숙련된 타사 결제 프로세서가 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-115">There are several experienced third-party payment processors that specialize in online shopping that address scalability and security.</span></span> <span data-ttu-id="897d9-116">ASP.NET 개발자는 쇼핑 및 구매 솔루션을 구현하기 전에 타사 결제 솔루션을 활용하는 장점을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-116">ASP.NET developers should consider the advantages of utilizing a third party payment solution before implementing a shopping and purchasing solution.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="897d9-117">Wingtip Toys 샘플 응용 프로그램은 웹 개발자가 사용할 수 있는 특정 ASP.NET 개념 및 기능을 표시하도록 설계되었으며 ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="897d9-117">The Wingtip Toys sample application was designed to shown specific ASP.NET concepts and features available to ASP.NET web developers.</span></span> <span data-ttu-id="897d9-118">이 샘플 응용 프로그램은 확장성 및 보안과 관련하여 가능한 모든 상황에 최적화되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-118">This sample application was not optimized for all possible circumstances in regard to scalability and security.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="897d9-119">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="897d9-119">What you'll learn:</span></span>

- <span data-ttu-id="897d9-120">폴더의 특정 페이지에 대한 액세스를 제한하는 방법.</span><span class="sxs-lookup"><span data-stu-id="897d9-120">How to restrict access to specific pages in a folder.</span></span>
- <span data-ttu-id="897d9-121">익명 장바구니에서 알려진 장바구니를 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="897d9-121">How to create a known shopping cart from an anonymous shopping cart.</span></span>
- <span data-ttu-id="897d9-122">프로젝트에 대 한 SSL을 사용 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="897d9-122">How to enable SSL for the project.</span></span>
- <span data-ttu-id="897d9-123">프로젝트에 OAuth 공급자를 추가하는 방법.</span><span class="sxs-lookup"><span data-stu-id="897d9-123">How to add an OAuth provider to the project.</span></span>
- <span data-ttu-id="897d9-124">페이팔을 사용하여 페이팔 테스트 환경을 사용하여 제품을 구입하는 방법.</span><span class="sxs-lookup"><span data-stu-id="897d9-124">How to use PayPal to purchase products using the PayPal testing environment.</span></span>
- <span data-ttu-id="897d9-125">**세부 정보보기** 컨트롤에 페이팔의 세부 정보를 표시하는 방법.</span><span class="sxs-lookup"><span data-stu-id="897d9-125">How to display details from PayPal in a **DetailsView** control.</span></span>
- <span data-ttu-id="897d9-126">페이팔에서 얻은 세부 사항으로 Wingtip 장난감 응용 프로그램의 데이터베이스를 업데이트하는 방법.</span><span class="sxs-lookup"><span data-stu-id="897d9-126">How to update the database of the Wingtip Toys application with details obtained from PayPal.</span></span>

## <a name="adding-order-tracking"></a><span data-ttu-id="897d9-127">주문 추적 추가</span><span class="sxs-lookup"><span data-stu-id="897d9-127">Adding Order Tracking</span></span>

<span data-ttu-id="897d9-128">이 자습서에서는 사용자가 만든 순서의 데이터를 추적하기 위해 두 개의 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-128">In this tutorial, you'll create two new classes to track data from the order a user has created.</span></span> <span data-ttu-id="897d9-129">수업은 배송 정보, 구매 합계 및 지불 확인에 관한 데이터를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-129">The classes will track data regarding shipping information, purchase total, and payment confirmation.</span></span>

### <a name="add-the-order-and-orderdetail-model-classes"></a><span data-ttu-id="897d9-130">순서 및 순서 세부 사항 모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="897d9-130">Add the Order and OrderDetail Model Classes</span></span>

<span data-ttu-id="897d9-131">이 `Category`자습서 시리즈의 앞에서 는 *모델* 폴더에서 에서 " `Product`및 `CartItem` 클래스를 만들어 범주, 제품 및 장바구니 항목에 대한 스키마를 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-131">Earlier in this tutorial series, you defined the schema for categories, products, and shopping cart items by creating the `Category`, `Product`, and `CartItem` classes in the *Models* folder.</span></span> <span data-ttu-id="897d9-132">이제 두 개의 새 클래스를 추가하여 제품 주문에 대한 스키마와 주문세부 정보를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-132">Now you will add two new classes to define the schema for the product order and the details of the order.</span></span>

1. <span data-ttu-id="897d9-133">**모델** 폴더에 *Order.cs*라는 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-133">In the **Models** folder, add a new class named *Order.cs*.</span></span>   
   <span data-ttu-id="897d9-134">새 클래스 파일이 편집기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-134">The new class file is displayed in the editor.</span></span>
2. <span data-ttu-id="897d9-135">기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-135">Replace the default code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. <span data-ttu-id="897d9-136">*모델* 폴더에 *OrderDetail.cs* 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-136">Add an *OrderDetail.cs* class to the *Models* folder.</span></span>
4. <span data-ttu-id="897d9-137">기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-137">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

<span data-ttu-id="897d9-138">`Order` 및 `OrderDetail` 클래스에는 구매 및 배송에 사용되는 주문 정보를 정의하는 스키마가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-138">The `Order` and `OrderDetail` classes contain the schema to define the order information used for purchasing and shipping.</span></span>

<span data-ttu-id="897d9-139">또한 엔터티 클래스를 관리하고 데이터베이스에 대한 데이터 액세스를 제공하는 데이터베이스 컨텍스트 클래스를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-139">In addition, you will need to update the database context class that manages the entity classes and that provides data access to the database.</span></span> <span data-ttu-id="897d9-140">이렇게 하려면 새로 만든 순서 및 `OrderDetail` 모델 클래스를 클래스에 추가 합니다. `ProductContext`</span><span class="sxs-lookup"><span data-stu-id="897d9-140">To do this, you will add the newly created Order and `OrderDetail` model classes to `ProductContext` class.</span></span>

1. <span data-ttu-id="897d9-141">**솔루션 탐색기에서** *ProductContext.cs* 파일을 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-141">In **Solution Explorer**, find and open the *ProductContext.cs* file.</span></span>
2. <span data-ttu-id="897d9-142">아래와 같이 강조 표시된 코드를 *ProductContext.cs* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-142">Add the highlighted code to the *ProductContext.cs* file as shown below:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

<span data-ttu-id="897d9-143">이 자습서 시리즈에서 앞에서 설명한 것처럼 *ProductContext.cs* 파일의 코드는 엔터티 프레임워크의 `System.Data.Entity` 모든 핵심 기능에 액세스할 수 있도록 네임스페이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-143">As mentioned previously in this tutorial series, the code in the *ProductContext.cs* file adds the `System.Data.Entity` namespace so that you have access to all the core functionality of the Entity Framework.</span></span> <span data-ttu-id="897d9-144">이 기능에는 강력한 형식의 개체로 작업하여 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-144">This functionality includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span> <span data-ttu-id="897d9-145">클래스의 `ProductContext` 위의 코드는 새로 추가된 `Order` 클래스에 `OrderDetail` 엔터티 프레임워크 액세스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-145">The above code in the `ProductContext` class adds Entity Framework access to the newly added `Order` and `OrderDetail` classes.</span></span>

## <a name="adding-checkout-access"></a><span data-ttu-id="897d9-146">체크 아웃 액세스 추가</span><span class="sxs-lookup"><span data-stu-id="897d9-146">Adding Checkout Access</span></span>

<span data-ttu-id="897d9-147">Wingtip 장난감 샘플 응용 프로그램은 익명 사용자가 검토하고 장바구니에 제품을 추가 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-147">The Wingtip Toys sample application allows anonymous users to review and add products to a shopping cart.</span></span> <span data-ttu-id="897d9-148">그러나 익명 사용자가 장바구니에 추가한 제품을 구매하기로 선택한 경우 사이트에 로그온해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-148">However, when anonymous users choose to purchase the products they added to the shopping cart, they must log on to the site.</span></span> <span data-ttu-id="897d9-149">로그온한 후에는 체크 아웃 및 구매 프로세스를 처리하는 웹 응용 프로그램의 제한된 페이지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-149">Once they have logged on, they can access the restricted pages of the Web application that handle the checkout and purchase process.</span></span> <span data-ttu-id="897d9-150">이러한 제한된 페이지는 응용 프로그램의 *체크 아웃* 폴더에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-150">These restricted pages are contained in the *Checkout* folder of the application.</span></span>

### <a name="add-a-checkout-folder-and-pages"></a><span data-ttu-id="897d9-151">체크 아웃 폴더 및 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="897d9-151">Add a Checkout Folder and Pages</span></span>

<span data-ttu-id="897d9-152">이제 체크 아웃 폴더와 *체크 아웃* 프로세스 중에 고객이 볼 수 있는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-152">You will now create the *Checkout* folder and the pages in it that the customer will see during the checkout process.</span></span> <span data-ttu-id="897d9-153">이 자습서의 나중에 이러한 페이지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-153">You will update these pages later in this tutorial.</span></span>

1. <span data-ttu-id="897d9-154">**솔루션 탐색기에서** 프로젝트 이름(Wingtip**Toys)을**마우스 오른쪽 단추로 클릭하고 **새 폴더 추가를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-154">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add a New Folder**.</span></span> 

    ![페이팔로 결제 및 결제 - 새 폴더](checkout-and-payment-with-paypal/_static/image1.png)
2. <span data-ttu-id="897d9-156">새 폴더 의 이름을 *체크 아웃합니다.*</span><span class="sxs-lookup"><span data-stu-id="897d9-156">Name the new folder *Checkout*.</span></span>
3. <span data-ttu-id="897d9-157">*체크 아웃* 폴더를 마우스 오른쪽 단추로 클릭한 다음**새 항목** **추가를**-&gt;선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-157">Right-click the *Checkout* folder and then select **Add**-&gt;**New Item**.</span></span> 

    ![페이팔로 결제 및 결제 - 새로운 항목](checkout-and-payment-with-paypal/_static/image2.png)
4. <span data-ttu-id="897d9-159">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-159">The **Add New Item** dialog box is displayed.</span></span>
5. <span data-ttu-id="897d9-160">왼쪽에 있는 **Visual C#**  - &gt; **웹** 템플릿 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-160">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="897d9-161">그런 다음 중간 창에서 **마스터 페이지가 있는 웹 양식을**선택하고 *CheckoutStart.aspx*.</span><span class="sxs-lookup"><span data-stu-id="897d9-161">Then, from the middle pane, select **Web Form with Master Page**and name it *CheckoutStart.aspx*.</span></span> 

    ![페이팔로 결제 및 결제 - 새 항목 대화 상자 추가](checkout-and-payment-with-paypal/_static/image3.png)
6. <span data-ttu-id="897d9-163">이전과 마찬가지로 *Site.Master* 파일을 마스터 페이지로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-163">As before, select the *Site.Master* file as the master page.</span></span>
7. <span data-ttu-id="897d9-164">위의 동일한 단계를 사용하여 *체크 아웃* 폴더에 다음 페이지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-164">Add the following additional pages to the *Checkout* folder using the same steps above:</span></span>   

    - <span data-ttu-id="897d9-165">체크 아웃리뷰.aspx</span><span class="sxs-lookup"><span data-stu-id="897d9-165">CheckoutReview.aspx</span></span>
    - <span data-ttu-id="897d9-166">체크 아웃완료.aspx</span><span class="sxs-lookup"><span data-stu-id="897d9-166">CheckoutComplete.aspx</span></span>
    - <span data-ttu-id="897d9-167">체크 아웃취소.aspx</span><span class="sxs-lookup"><span data-stu-id="897d9-167">CheckoutCancel.aspx</span></span>
    - <span data-ttu-id="897d9-168">체크 아웃오류.aspx</span><span class="sxs-lookup"><span data-stu-id="897d9-168">CheckoutError.aspx</span></span>

### <a name="add-a-webconfig-file"></a><span data-ttu-id="897d9-169">Web.config 파일 추가</span><span class="sxs-lookup"><span data-stu-id="897d9-169">Add a Web.config File</span></span>

<span data-ttu-id="897d9-170">*체크 아웃* 폴더에 새 *Web.config* 파일을 추가하면 폴더에 포함된 모든 페이지에 대한 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-170">By adding a new *Web.config* file to the *Checkout* folder, you will be able to restrict access to all the pages contained in the folder.</span></span>

1. <span data-ttu-id="897d9-171">*체크 아웃* 폴더를 마우스 오른쪽 단추로 클릭하고 **새 항목** **추가를**  - &gt; 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-171">Right-click the *Checkout* folder and select **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="897d9-172">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-172">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="897d9-173">왼쪽에 있는 **Visual C#**  - &gt; **웹** 템플릿 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-173">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="897d9-174">그런 다음 중간 창에서 **웹 구성 파일을**선택하고 *Web.config의*기본 이름을 수락한 다음 **에 추가를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-174">Then, from the middle pane, select **Web Configuration File**, accept the default name of *Web.config*, and then select **Add**.</span></span>
3. <span data-ttu-id="897d9-175">*Web.config* 파일의 기존 XML 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-175">Replace the existing XML content in the *Web.config* file with the following:</span></span>  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. <span data-ttu-id="897d9-176">*Web.config* 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-176">Save the *Web.config* file.</span></span>

<span data-ttu-id="897d9-177">*Web.config* 파일은 웹 응용 프로그램의 알 수 없는 모든 사용자가 *체크 아웃* 폴더에 포함된 페이지에 대한 액세스를 거부해야 함을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-177">The *Web.config* file specifies that all unknown users of the Web application must be denied access to the pages contained in the *Checkout* folder.</span></span> <span data-ttu-id="897d9-178">그러나 사용자가 계정을 등록하고 로그온한 경우 알려진 사용자가 되며 *체크 아웃* 폴더의 페이지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-178">However, if the user has registered an account and is logged on, they will be a known user and will have access to the pages in the *Checkout* folder.</span></span>

<span data-ttu-id="897d9-179">ASP.NET 구성은 계층 구조를 따르며, 각 *Web.config* 파일은 구성 설정을 폴더에 적용하고 그 아래에 있는 모든 자식 디렉터리에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-179">It's important to note that ASP.NET configuration follows a hierarchy, where each *Web.config* file applies configuration settings to the folder that it is in and to all of the child directories below it.</span></span>

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a><span data-ttu-id="897d9-180">프로젝트에 SSL 사용</span><span class="sxs-lookup"><span data-stu-id="897d9-180">Enable SSL for the Project</span></span>

 <span data-ttu-id="897d9-181">SSL(Secure Sockets Layer)은 웹 서버 및 웹 클라이언트가 암호화를 사용하여 더욱 안전하게 통신할 수 있도록 정의된 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-181">Secure Sockets Layer (SSL) is a protocol defined to allow Web servers and Web clients to communicate more securely through the use of encryption.</span></span> <span data-ttu-id="897d9-182">SSL을 사용하지 않으면 네트워크에 실제로 액세스하여 패킷을 스니핑하는 누군가에게 클라이언트와 서버 간에 전송된 데이터가 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-182">When SSL is not used, data sent between the client and server is open to packet sniffing by anyone with physical access to the network.</span></span> <span data-ttu-id="897d9-183">또한 몇 가지 일반적인 인증 체계는 일반 HTTP를 통해서는 보호되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-183">Additionally, several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="897d9-184">특히, 기본 인증 및 폼 인증은 암호화되지 않은 자격 증명을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-184">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="897d9-185">보안을 위해서 인증 체계는 SSL을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-185">To be secure, these authentication schemes must use SSL.</span></span> 

1. <span data-ttu-id="897d9-186">**솔루션 탐색기에서** **WingtipToys** 프로젝트를 클릭한 다음 **F4를** 눌러 **속성** 창을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-186">In **Solution Explorer**, click the **WingtipToys** project, then press **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="897d9-187">**SSL 을** `true`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-187">Change **SSL Enabled** to `true`.</span></span>
3. <span data-ttu-id="897d9-188">나중에 사용할 수 있도록 **SSL URL** 을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-188">Copy the **SSL URL** so you can use it later.</span></span>   
 <span data-ttu-id="897d9-189">SSL URL은 `https://localhost:44300/` 이전에 SSL 웹 사이트를 만든 적이 없는 경우(아래 와 같이)입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-189">The SSL URL will be `https://localhost:44300/` unless you've previously created SSL Web Sites (as shown below).</span></span>   
    <span data-ttu-id="897d9-190">![프로젝트 속성](checkout-and-payment-with-paypal/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="897d9-190">![Project Properties](checkout-and-payment-with-paypal/_static/image4.png)</span></span>
4. <span data-ttu-id="897d9-191">**솔루션 탐색기에서** **WingtipToys** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성을**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-191">In **Solution Explorer**, right click the **WingtipToys** project and click **Properties**.</span></span>
5. <span data-ttu-id="897d9-192">왼쪽 탭에서 **웹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-192">In the left tab, click **Web**.</span></span>
6. <span data-ttu-id="897d9-193">이전에 저장한 **SSL URL을** 사용하도록 **프로젝트 URL을** 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-193">Change the **Project Url** to use the **SSL URL** that you saved earlier.</span></span>   
    <span data-ttu-id="897d9-194">![프로젝트 웹 속성](checkout-and-payment-with-paypal/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="897d9-194">![Project Web Properties](checkout-and-payment-with-paypal/_static/image5.png)</span></span>
7. <span data-ttu-id="897d9-195">**CTRL+S**키를 눌러 페이지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-195">Save the page by pressing **CTRL+S**.</span></span>
8. <span data-ttu-id="897d9-196">**Ctrl+F5를** 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-196">Press **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="897d9-197">Visual Studio에서 SSL 경고를 방지할 수 있도록 하는 옵션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-197">Visual Studio will display an option to allow you to avoid SSL warnings.</span></span>
9. <span data-ttu-id="897d9-198">**예** 를 클릭하여 IIS Express SSL 인증서를 신뢰하고 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-198">Click **Yes** to trust the IIS Express SSL certificate and continue.</span></span>   
    <span data-ttu-id="897d9-199">![IIS Express SSL 인증서 정보](checkout-and-payment-with-paypal/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="897d9-199">![IIS Express SSL certificate details](checkout-and-payment-with-paypal/_static/image6.png)</span></span>  
 <span data-ttu-id="897d9-200"> 보안 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-200">A Security Warning is displayed.</span></span>
10. <span data-ttu-id="897d9-201">**예** 를 클릭하여 인증서를 localhost에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-201">Click **Yes** to install the certificate to your localhost.</span></span>   
    <span data-ttu-id="897d9-202">![보안 경고 대화 상자](checkout-and-payment-with-paypal/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="897d9-202">![Security Warning dialog box](checkout-and-payment-with-paypal/_static/image7.png)</span></span>  
 <span data-ttu-id="897d9-203"> 브라우저 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-203">The browser window will be displayed.</span></span>

<span data-ttu-id="897d9-204">이제 SSL을 사용하여 로컬에서 웹 응용 프로그램을 쉽게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-204">You can now easily test your Web application locally using SSL.</span></span>

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a><span data-ttu-id="897d9-205">OAuth 2.0 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="897d9-205">Add an OAuth 2.0 Provider</span></span>

<span data-ttu-id="897d9-206">ASP.NET Web Forms는 멤버 자격 및 인증을 위해 개선된 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-206">ASP.NET Web Forms provides enhanced options for membership and authentication.</span></span> <span data-ttu-id="897d9-207">이러한 개선 사항에는 OAuth가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-207">These enhancements include OAuth.</span></span> <span data-ttu-id="897d9-208">OAuth는 웹, 모바일 및 데스크톱 애플리케이션에서 간단한 표준 메서드로 보안 권한 부여를 허용하는 개방형 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-208">OAuth is an open protocol that allows secure authorization in a simple and standard method from web, mobile, and desktop applications.</span></span> <span data-ttu-id="897d9-209">ASP.NET 웹 폼 템플릿은 OAuth를 사용하여 페이스 북, 트위터, 구글 및 Microsoft를 인증 공급자로 노출시킵니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-209">The ASP.NET Web Forms template uses OAuth to expose Facebook, Twitter, Google and Microsoft as authentication providers.</span></span> <span data-ttu-id="897d9-210">이 자습서에서는 인증 공급자로 Google만 사용하지만 다른 공급자를 사용하도록 코드를 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-210">Although this tutorial uses only Google as the authentication provider, you can easily modify the code to use any of the providers.</span></span> <span data-ttu-id="897d9-211">다른 공급자를 구현하는 단계도 이 자습서에 표시되는 단계와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-211">The steps to implement other providers are very similar to the steps you will see in this tutorial.</span></span>

<span data-ttu-id="897d9-212">자습서에서는 인증 외에도 역할을 사용하여 권한 부여를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-212">In addition to authentication, the tutorial will also use roles to implement authorization.</span></span> <span data-ttu-id="897d9-213">`canEdit` 역할에 추가한 사용자만 데이터를 변경할 수 있습니다(연락처 만들기, 편집 또는 삭제).</span><span class="sxs-lookup"><span data-stu-id="897d9-213">Only those users you add to the `canEdit` role will be able to change data (create, edit, or delete contacts).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="897d9-214">Windows Live 응용 프로그램은 작업 중인 웹 사이트에 대한 라이브 URL만 허용하므로 로그인 을 테스트하기 위해 로컬 웹 사이트 URL을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-214">Windows Live applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>

<span data-ttu-id="897d9-215">다음 단계를 통해 Google 인증 공급자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-215">The following steps will allow you to add a Google authentication provider.</span></span>

1. <span data-ttu-id="897d9-216">*\_앱 시작\Startup.Auth.cs 파일을 엽니다.*</span><span class="sxs-lookup"><span data-stu-id="897d9-216">Open the *App\_Start\Startup.Auth.cs* file.</span></span>
2. <span data-ttu-id="897d9-217">메서드가 다음과 같이 나타나도록 `app.UseGoogleAuthentication()` 메서드에서 주석 문자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-217">Remove the comment characters from the `app.UseGoogleAuthentication()` method so that the method appears as follows:</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. <span data-ttu-id="897d9-218">[Google Developers Console](https://console.developers.google.com/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-218">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span> <span data-ttu-id="897d9-219">Google 개발자 메일 계정(gmail.com)으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-219">You will also need to sign-in with your Google developer email account (gmail.com).</span></span> <span data-ttu-id="897d9-220">Google 계정이 없으면 **계정 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-220">If you do not have a Google account, select the **Create an account** link.</span></span>   
   <span data-ttu-id="897d9-221">다음으로, **Google 개발자 콘솔**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-221">Next, you'll see the **Google Developers Console**.</span></span>   
    <span data-ttu-id="897d9-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="897d9-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span></span>
4. <span data-ttu-id="897d9-223">프로젝트 **만들기** 단추를 클릭하고 프로젝트 이름과 ID를 입력합니다(기본값을 사용할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="897d9-223">Click the **Create Project** button and enter a project name and ID (you can use the default values).</span></span> <span data-ttu-id="897d9-224">그런 다음 **계약 확인란과** **만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-224">Then, click the **agreement checkbox** and the **Create** button.</span></span>  

    ![구글 - 새로운 프로젝트](checkout-and-payment-with-paypal/_static/image9.png)

   <span data-ttu-id="897d9-226"> 몇 초 내에 새 프로젝트가 만들어지고 브라우저에 새 프로젝트 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-226">In a few seconds the new project will be created and your browser will display the new projects page.</span></span>
5. <span data-ttu-id="897d9-227">왼쪽 탭에서 **API &amp; 인증을**클릭한 다음 자격 증명 을 **클릭합니다.**</span><span class="sxs-lookup"><span data-stu-id="897d9-227">In the left tab, click **APIs &amp; auth**, and then click **Credentials**.</span></span>
6. <span data-ttu-id="897d9-228">**OAuth**에서 **새 클라이언트 ID 만들기를** 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-228">Click the **Create New Client ID** under **OAuth**.</span></span>   
   <span data-ttu-id="897d9-229">**Create Client ID** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-229">The **Create Client ID** dialog will be displayed.</span></span>   
    <span data-ttu-id="897d9-230">![Google - 클라이언트 ID 만들기](checkout-and-payment-with-paypal/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="897d9-230">![Google - Create Client ID](checkout-and-payment-with-paypal/_static/image10.png)</span></span>
7. <span data-ttu-id="897d9-231">클라이언트 **ID 만들기** 대화 상자에서 응용 프로그램 유형에 대한 기본 **웹 응용 프로그램을** 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-231">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
8. <span data-ttu-id="897d9-232">이 자습서의 앞에서 사용한 **공인 자바스크립트 원본을** 설정합니다(다른`https://localhost:44300/` SSL 프로젝트를 만들지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="897d9-232">Set the **Authorized JavaScript Origins** to the SSL URL you used earlier in this tutorial (`https://localhost:44300/` unless you've created other SSL projects).</span></span>   
   <span data-ttu-id="897d9-233">이 URL이 애플리케이션의 원점입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-233">This URL is the origin for your application.</span></span> <span data-ttu-id="897d9-234">이 샘플의 경우 localhost 테스트 URL만 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-234">For this sample, you will only enter the localhost test URL.</span></span> <span data-ttu-id="897d9-235">그러나 로컬 호스트 및 프로덕션을 고려하여 여러 URL을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-235">However, you can enter multiple URLs to account for localhost and production.</span></span>
9. <span data-ttu-id="897d9-236">**Authorized Redirect URI** 를 다음으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-236">Set the **Authorized Redirect URI** to the following:</span></span> 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   <span data-ttu-id="897d9-237">이 값은 ASP.NET OAuth 사용자가 Google OAuth 서버와 통신하는 데 사용하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-237">This value is the URI that ASP.NET OAuth users to communicate with the google OAuth server.</span></span> <span data-ttu-id="897d9-238">위에서 사용한 SSL URL을 `https://localhost:44300/` 기억하십시오(다른 SSL 프로젝트를 만들지 않는 한).</span><span class="sxs-lookup"><span data-stu-id="897d9-238">Remember the SSL URL you used above (    `https://localhost:44300/` unless you've created other SSL projects).</span></span>
10. <span data-ttu-id="897d9-239">클라이언트 ID 만들기 단추를 **클릭합니다.**</span><span class="sxs-lookup"><span data-stu-id="897d9-239">Click the **Create Client ID** button.</span></span>
11. <span data-ttu-id="897d9-240">Google 개발자 콘솔의 왼쪽 메뉴에서 **동의 화면** 메뉴 항목을 클릭한 다음 이메일 주소와 제품 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-240">On the left menu of the Google Developers Console, click the **Consent screen** menu item, then set your email address and product name.</span></span> <span data-ttu-id="897d9-241">양식을 완료하면 **저장을**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-241">When you have completed the form, click **Save**.</span></span>
12. <span data-ttu-id="897d9-242">**API** 메뉴 항목을 클릭하고 아래로 스크롤한 다음 **Google+ API**옆의 **끄기** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-242">Click the **APIs** menu item, scroll down and click the **off** button next to **Google+ API**.</span></span>   
    <span data-ttu-id="897d9-243">이 옵션을 수락하면 Google+ API가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-243">Accepting this option will enable the Google+ API.</span></span>
13. <span data-ttu-id="897d9-244">또한 버전 3.0.0으로 **Microsoft.Owin** NuGet 패키지를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-244">You must also update the **Microsoft.Owin** NuGet package to version 3.0.0.</span></span>   
    <span data-ttu-id="897d9-245">**도구** 메뉴에서 **NuGet 패키지 관리자를** 선택한 다음 **솔루션에 대한 NuGet 패키지 관리를 선택합니다.**</span><span class="sxs-lookup"><span data-stu-id="897d9-245">From the **Tools** menu, select **NuGet Package Manager** and then select **Manage NuGet Packages for Solution**.</span></span>  
    <span data-ttu-id="897d9-246">NuGet 패키지 관리 창에서 **Microsoft.Owin** 패키지를 버전 3.0.0으로 찾아 **업데이트합니다.**</span><span class="sxs-lookup"><span data-stu-id="897d9-246">From the **Manage NuGet Packages** window, find and update the **Microsoft.Owin** package to version 3.0.0.</span></span>
14. <span data-ttu-id="897d9-247">Visual Studio에서 클라이언트 `UseGoogleAuthentication` **ID와 클라이언트** **시크릿을** 복사하여 *메서드에* 붙여넣은 Startup.Auth.cs 페이지의 메서드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-247">In Visual Studio, update the `UseGoogleAuthentication` method of the *Startup.Auth.cs* page by copying and pasting the **Client ID** and **Client Secret** into the method.</span></span> <span data-ttu-id="897d9-248">아래에 표시된 **클라이언트 ID** 및 **클라이언트 보안** 값은 샘플이며 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-248">The **Client ID** and **Client Secret** values shown below are samples and will not work.</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. <span data-ttu-id="897d9-249">**CTRL+F5를** 눌러 응용 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-249">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="897d9-250">**로그인** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-250">Click the **Log in** link.</span></span>
16. <span data-ttu-id="897d9-251">**다른 서비스 사용에서 로그인하려면** **Google**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-251">Under **Use another service to log in**, click **Google**.</span></span>  
    <span data-ttu-id="897d9-252">![로그인](checkout-and-payment-with-paypal/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="897d9-252">![Log in](checkout-and-payment-with-paypal/_static/image11.png)</span></span>
17. <span data-ttu-id="897d9-253">자격 증명을 입력해야 하는 경우 자격 증명을 입력할 google 사이트로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-253">If you need to enter your credentials, you will be redirected to the google site where you will enter your credentials.</span></span>  
    ![Google - 로그인](checkout-and-payment-with-paypal/_static/image12.png)
18. <span data-ttu-id="897d9-255">자격 증명을 입력하면 방금 만든 웹 응용 프로그램에 대한 권한을 부여하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-255">After you enter your credentials, you will be prompted to give permissions to the web application you just created.</span></span>  
    ![프로젝트 기본 서비스 계정](checkout-and-payment-with-paypal/_static/image13.png)
19. <span data-ttu-id="897d9-257">**Accept**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-257">Click **Accept**.</span></span> <span data-ttu-id="897d9-258">이제 Google 계정을 등록할 수 있는 **WingtipToys** 응용 프로그램의 **등록** 페이지로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-258">You will now be redirected back to the **Register** page of the **WingtipToys** application where you can register your Google account.</span></span>  
    <span data-ttu-id="897d9-259">![Google 계정을 사용하여 등록](checkout-and-payment-with-paypal/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="897d9-259">![Register with your Google Account](checkout-and-payment-with-paypal/_static/image14.png)</span></span>
20. <span data-ttu-id="897d9-260">Gmail 계정에 사용되는 로컬 전자 메일 등록 이름을 변경할 수 있지만 일반적으로 기본 전자 메일 별칭(즉, 인증에 사용하는 별칭)을 그대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-260">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="897d9-261">위에 표시된 대로 **로그인을** 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-261">Click **Log in** as shown above.</span></span>

### <a name="modifying-login-functionality"></a><span data-ttu-id="897d9-262">로그인 기능 수정</span><span class="sxs-lookup"><span data-stu-id="897d9-262">Modifying Login Functionality</span></span>

<span data-ttu-id="897d9-263">이 자습서 시리즈에서 설명한 것처럼 대부분의 사용자 등록 기능은 기본적으로 ASP.NET 웹 폼 템플릿에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-263">As previously mentioned in this tutorial series, much of the user registration functionality has been included in the ASP.NET Web Forms template by default.</span></span> <span data-ttu-id="897d9-264">이제 기본 *Login.aspx* 및 *Register.aspx* 페이지를 수정하여 메서드를 `MigrateCart` 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-264">Now you will modify the default *Login.aspx* and *Register.aspx* pages to call the `MigrateCart` method.</span></span> <span data-ttu-id="897d9-265">이 `MigrateCart` 메서드는 새로 로그인한 사용자를 익명 장바구니와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-265">The `MigrateCart` method associates a newly logged in user with an anonymous shopping cart.</span></span> <span data-ttu-id="897d9-266">사용자와 장바구니를 연결하여 Wingtip Toys 샘플 응용 프로그램은 방문 간에 사용자의 장바구니를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-266">By associating the user and shopping cart, the Wingtip Toys sample application will be able to maintain the shopping cart of the user between visits.</span></span>

1. <span data-ttu-id="897d9-267">**솔루션 탐색기에서** *계정* 폴더를 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-267">In **Solution Explorer**, find and open the *Account* folder.</span></span>
2. <span data-ttu-id="897d9-268">*Login.aspx.cs* 라는 코드 뒤에 페이지를 수정 하려면 노란색으로 강조 표시된 코드를 포함 하 여 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-268">Modify the code-behind page named *Login.aspx.cs* to include the code highlighted in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. <span data-ttu-id="897d9-269">*Login.aspx.cs* 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-269">Save the *Login.aspx.cs* file.</span></span>

<span data-ttu-id="897d9-270">지금은 `MigrateCart` 메서드에 대한 정의가 없다는 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-270">For now, you can ignore the warning that there is no definition for the `MigrateCart` method.</span></span> <span data-ttu-id="897d9-271">이 자습서의 나중에 조금 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-271">You will be adding it a bit later in this tutorial.</span></span>

<span data-ttu-id="897d9-272">*Login.aspx.cs* 코드 뒤 파일은 LogIn 메서드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-272">The *Login.aspx.cs* code-behind file supports a LogIn method.</span></span> <span data-ttu-id="897d9-273">Login.aspx 페이지를 검사하면 이 페이지에 클릭시 코드 숨결의 `LogIn` 처리기가 트리거되는 "로그인" 버튼이 포함되어 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-273">By inspecting the Login.aspx page, you'll see that this page includes a "Log in" button that when click triggers the `LogIn` handler on the code-behind.</span></span>

<span data-ttu-id="897d9-274">Login.aspx.cs `Login` 메서드가 *Login.aspx.cs* 호출되면 라는 `usersShoppingCart` 쇼핑 카트의 새 인스턴스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-274">When the `Login` method on the *Login.aspx.cs* is called, a new instance of the shopping cart named `usersShoppingCart` is created.</span></span> <span data-ttu-id="897d9-275">장바구니(GUID)의 ID가 검색되어 `cartId` 변수로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-275">The ID of the shopping cart (a GUID) is retrieved and set to the `cartId` variable.</span></span> <span data-ttu-id="897d9-276">그런 다음 `MigrateCart` 메서드를 호출하여 `cartId` 로그인한 사용자의 이름과 이름을 이 메서드에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-276">Then, the `MigrateCart` method is called, passing both the `cartId` and the name of the logged-in user to this method.</span></span> <span data-ttu-id="897d9-277">장바구니를 마이그레이션할 때 익명 장바구니를 식별하는 데 사용되는 GUID가 사용자 이름으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-277">When the shopping cart is migrated, the GUID used to identify the anonymous shopping cart is replaced with the user name.</span></span>

<span data-ttu-id="897d9-278">사용자가 로그인할 때 장바구니를 마이그레이션하기 위해 *Login.aspx.cs* 코드 숨결 파일을 수정하는 것 외에도 *Register.aspx.cs 코드 숨은 파일을* 수정하여 사용자가 새 계정을 만들고 로그인할 때 장바구니를 마이그레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-278">In addition to modifying the *Login.aspx.cs* code-behind file to migrate the shopping cart when the user logs in, you must also modify the *Register.aspx.cs code-behind file* to migrate the shopping cart when the user creates a new account and logs in.</span></span>

1. <span data-ttu-id="897d9-279">*Account* 폴더에서 *Register.aspx.cs*라는 코드 숨결 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-279">In the *Account* folder, open the code-behind file named *Register.aspx.cs*.</span></span>
2. <span data-ttu-id="897d9-280">다음과 같이 표시되도록 코드를 노란색으로 표시하여 코드 숨결 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-280">Modify the code-behind file by including the code in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. <span data-ttu-id="897d9-281">*Register.aspx.cs* 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-281">Save the *Register.aspx.cs* file.</span></span> <span data-ttu-id="897d9-282">다시 한번 메서드에 `MigrateCart` 대한 경고를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-282">Once again, ignore the warning about the `MigrateCart` method.</span></span>

<span data-ttu-id="897d9-283">`CreateUser_Click` 이벤트 처리기에 사용된 코드는 `LogIn` 메서드에서 사용한 코드와 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-283">Notice that the code you used in the `CreateUser_Click` event handler is very similar to the code you used in the `LogIn` method.</span></span> <span data-ttu-id="897d9-284">사용자가 사이트에 등록하거나 로그인하면 `MigrateCart` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-284">When the user registers or logs in to the site, a call to the `MigrateCart` method will be made.</span></span>

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="897d9-285">장바구니 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="897d9-285">Migrating the Shopping Cart</span></span>

<span data-ttu-id="897d9-286">로그인 및 등록 프로세스가 업데이트되었으므로 코드를 추가하여 메서드를 `MigrateCart` 사용하여 장바구니를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-286">Now that you have the log-in and registration process updated, you can add the code to migrate the shopping cart using the `MigrateCart` method.</span></span>

1. <span data-ttu-id="897d9-287">**솔루션 탐색기에서** *논리* 폴더를 찾아 *ShoppingCartActions.cs* 클래스 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-287">In **Solution Explorer**, find the *Logic* folder and open the *ShoppingCartActions.cs* class file.</span></span>
2. <span data-ttu-id="897d9-288">*ShoppingCartActions.cs* 파일의 기존 코드에 노란색으로 강조 표시된 코드를 추가하여 *ShoppingCartActions.cs* 파일의 코드가 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-288">Add the code highlighted in yellow to the existing code in the *ShoppingCartActions.cs* file, so that the code in the *ShoppingCartActions.cs* file appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

<span data-ttu-id="897d9-289">이 `MigrateCart` 메서드는 기존 cartId를 사용하여 사용자의 장바구니를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-289">The `MigrateCart` method uses the existing cartId to find the shopping cart of the user.</span></span> <span data-ttu-id="897d9-290">다음으로 코드는 모든 장바구니 항목을 반복하고 스키마에서 `CartId` 지정한 `CartItem` 대로 속성을 로그인한 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-290">Next, the code loops through all the shopping cart items and replaces the `CartId` property (as specified by the `CartItem` schema) with the logged-in user name.</span></span>

### <a name="updating-the-database-connection"></a><span data-ttu-id="897d9-291">데이터베이스 연결 업데이트</span><span class="sxs-lookup"><span data-stu-id="897d9-291">Updating the Database Connection</span></span>

<span data-ttu-id="897d9-292">**미리 빌드된** Wingtip Toys 샘플 응용 프로그램을 사용하여 이 자습서를 따르는 경우 기본 멤버 자격 데이터베이스를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-292">If you are following this tutorial using the **prebuilt** Wingtip Toys sample application, you must recreate the default membership database.</span></span> <span data-ttu-id="897d9-293">기본 연결 문자열을 수정하면 다음에 응용 프로그램을 실행할 때 멤버 자격 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-293">By modifying the default connection string, the membership database will be created the next time the application runs.</span></span>

1. <span data-ttu-id="897d9-294">프로젝트의 루트에서 *Web.config* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-294">Open the *Web.config* file at the root of the project.</span></span>
2. <span data-ttu-id="897d9-295">다음과 같이 표시되도록 기본 연결 문자열을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-295">Update the default connection string so that it appears as follows:</span></span>   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a><span data-ttu-id="897d9-296">페이팔 통합</span><span class="sxs-lookup"><span data-stu-id="897d9-296">Integrating PayPal</span></span>

<span data-ttu-id="897d9-297">PayPal은 온라인 판매자의 결제를 허용하는 웹 기반 결제 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-297">PayPal is a web-based billing platform that accepts payments by online merchants.</span></span> <span data-ttu-id="897d9-298">이 자습서는 다음에 페이팔의 익스프레스 체크 아웃 기능을 응용 프로그램에 통합 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-298">This tutorial next explains how to integrate PayPal's Express Checkout functionality into your application.</span></span> <span data-ttu-id="897d9-299">익스프레스 체크아웃을 사용하면 고객이 PayPal을 사용하여 장바구니에 추가한 항목에 대한 비용을 지불할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-299">Express Checkout allows your customers to use PayPal to pay for the items they have added to their shopping cart.</span></span>

### <a name="create-paypal-test-accounts"></a><span data-ttu-id="897d9-300">페이팔 테스트 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="897d9-300">Create PayPal Test Accounts</span></span>

<span data-ttu-id="897d9-301">PayPal 테스트 환경을 사용하려면 개발자 테스트 계정을 만들고 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-301">To use the PayPal testing environment, you must create and verify a developer test account.</span></span> <span data-ttu-id="897d9-302">개발자 테스트 계정을 사용하여 구매자 테스트 계정과 판매자 테스트 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-302">You will use the developer test account to create a buyer test account and a seller test account.</span></span> <span data-ttu-id="897d9-303">개발자 테스트 계정 자격 증명은 또한 Wingtip Toys 샘플 응용 프로그램이 PayPal 테스트 환경에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-303">The developer test account credentials also will allow the Wingtip Toys sample application to access the PayPal testing environment.</span></span>

1. <span data-ttu-id="897d9-304">브라우저에서 PayPal 개발자 테스트 사이트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-304">In a browser, navigate to the PayPal developer testing site:</span></span>   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. <span data-ttu-id="897d9-305">PayPal 개발자 계정이 없는 경우 **등록을**클릭하고 등록 단계를 따라 새 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-305">If you don't have a PayPal developer account, create a new account by clicking **Sign Up**and following the sign up steps.</span></span> <span data-ttu-id="897d9-306">기존 PayPal 개발자 계정이 있는 경우 **로그인**을 클릭하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-306">If you have an existing PayPal developer account, sign in by clicking **Log In**.</span></span> <span data-ttu-id="897d9-307">이 자습서의 후반부에서 Wingtip Toys 샘플 응용 프로그램을 테스트하려면 PayPal 개발자 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-307">You will need your PayPal developer account to test the Wingtip Toys sample application later in this tutorial.</span></span>
3. <span data-ttu-id="897d9-308">PayPal 개발자 계정에 방금 가입한 경우 PayPal을 사용하여 PayPal 개발자 계정을 확인해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-308">If you have just signed up for your PayPal developer account, you may need to verify your PayPal developer account with PayPal.</span></span> <span data-ttu-id="897d9-309">PayPal이 이메일 계정으로 전송한 단계에 따라 계정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-309">You can verify your account by following the steps that PayPal sent to your email account.</span></span> <span data-ttu-id="897d9-310">PayPal 개발자 계정을 확인하면 PayPal 개발자 테스트 사이트에 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-310">Once you have verified your PayPal developer account, log back into the PayPal developer testing site.</span></span>
4. <span data-ttu-id="897d9-311">PayPal 개발자 계정으로 PayPal 개발자 사이트에 로그인한 후 아직 계정이 없는 경우 PayPal 구매자 테스트 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-311">After you are logged in to the PayPal developer site with your PayPal developer account you need to create a PayPal buyer test account if you don't already have one.</span></span> <span data-ttu-id="897d9-312">구매자 테스트 계정을 만들려면 PayPal 사이트에서 **응용 프로그램 탭을** 클릭한 다음 **샌드박스 계정을**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-312">To create a buyer test account, on the PayPal site click the **Applications** tab and then click **Sandbox accounts**.</span></span>   
 <span data-ttu-id="897d9-313">**샌드박스 테스트 계정** 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-313">The **Sandbox test accounts** page is shown.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="897d9-314">페이팔 개발자 사이트는 이미 판매자 테스트 계정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-314">The PayPal Developer site already provides a merchant test account.</span></span>

    ![페이팔로 결제 및 결제 - 샌드박스 테스트 계정](checkout-and-payment-with-paypal/_static/image15.png)
5. <span data-ttu-id="897d9-316">샌드박스 테스트 계정 페이지에서 **계정 만들기를**클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-316">On the Sandbox test accounts page, click **Create Account**.</span></span>
6. <span data-ttu-id="897d9-317">테스트 **계정 만들기** 페이지에서 구매자 테스트 계정 이메일과 원하는 암호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-317">On the **Create test account** page choose a buyer test account email and password of your choice.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="897d9-318">이 자습서의 끝에 있는 Wingtip Toys 샘플 응용 프로그램을 테스트하려면 구매자 이메일 주소와 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-318">You will need the buyer email addresses and password to test the Wingtip Toys sample application at the end of this tutorial.</span></span>

    ![페이팔로 결제 및 결제 - 샌드박스 테스트 계정](checkout-and-payment-with-paypal/_static/image16.png)
7. <span data-ttu-id="897d9-320">계정 만들기 단추를 클릭하여 구매자 테스트 계정을 **만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="897d9-320">Create the buyer test account by clicking the **Create Account** button.</span></span>  
 <span data-ttu-id="897d9-321">**샌드박스 테스트 계정** 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-321">The **Sandbox Test accounts** page is displayed.</span></span> 

    ![페이팔 결제 및 결제 - 페이팔 계정](checkout-and-payment-with-paypal/_static/image17.png)
8. <span data-ttu-id="897d9-323">**샌드박스 테스트 계정** 페이지에서 진행자 이메일 계정을 **클릭합니다.**</span><span class="sxs-lookup"><span data-stu-id="897d9-323">On the **Sandbox test accounts** page, click the **facilitator** email account.</span></span>  
    <span data-ttu-id="897d9-324">**프로필** 및 **알림** 옵션이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-324">**Profile** and **Notification** options appear.</span></span>
9. <span data-ttu-id="897d9-325">**프로필** 옵션을 선택한 다음 **API 자격 증명을** 클릭하여 판매자 테스트 계정에 대한 API 자격 증명을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-325">Select the **Profile** option, then click **API credentials** to view your API credentials for the merchant test account.</span></span>
10. <span data-ttu-id="897d9-326">테스트 API 자격 증명을 메모장에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-326">Copy the TEST API credentials to notepad.</span></span>

<span data-ttu-id="897d9-327">Wingtip Toys 샘플 응용 프로그램에서 PayPal 테스트 환경으로 API를 호출하려면 표시된 클래식 TEST API 자격 증명(사용자 이름, 암호 및 서명)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-327">You will need your displayed Classic TEST API credentials (Username, Password, and Signature) to make API calls from the Wingtip Toys sample application to the PayPal testing environment.</span></span> <span data-ttu-id="897d9-328">다음 단계에서 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-328">You will add the credentials in the next step.</span></span>

### <a name="add-paypal-class-and-api-credentials"></a><span data-ttu-id="897d9-329">페이팔 클래스 및 API 자격 증명 추가</span><span class="sxs-lookup"><span data-stu-id="897d9-329">Add PayPal Class and API Credentials</span></span>

<span data-ttu-id="897d9-330">페이팔 코드의 대부분을 단일 클래스에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-330">You will place the majority of the PayPal code into a single class.</span></span> <span data-ttu-id="897d9-331">이 클래스에는 PayPal과 통신하는 데 사용되는 방법이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-331">This class contains the methods used to communicate with PayPal.</span></span> <span data-ttu-id="897d9-332">또한 이 클래스에 PayPal 자격 증명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-332">Also, you will add your PayPal credentials to this class.</span></span>

1. <span data-ttu-id="897d9-333">Visual Studio 내의 Wingtip Toys 샘플 응용 프로그램에서 **논리** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 항목** **추가를**  - &gt; 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-333">In the Wingtip Toys sample application within Visual Studio, right-click the **Logic** folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="897d9-334">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-334">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="897d9-335">왼쪽에 **설치된** 창에서 **시각적 C#** 아래에서 **코드를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-335">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span>
3. <span data-ttu-id="897d9-336">가운데 창에서 **클래스를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-336">From the middle pane, select **Class**.</span></span> <span data-ttu-id="897d9-337">이 새 클래스의 이름을 **PayPalFunctions.cs.**</span><span class="sxs-lookup"><span data-stu-id="897d9-337">Name this new class **PayPalFunctions.cs**.</span></span>
4. <span data-ttu-id="897d9-338">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-338">Click **Add**.</span></span>  
   <span data-ttu-id="897d9-339">새 클래스 파일이 편집기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-339">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="897d9-340">기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-340">Replace the default code with the following code:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. <span data-ttu-id="897d9-341">PayPal 테스트 환경에 함수 호출을 수행할 수 있도록 이 자습서의 앞에서 표시한 판매자 API 자격 증명(사용자 이름, 암호 및 서명)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-341">Add the Merchant API credentials (Username, Password, and Signature) that you displayed earlier in this tutorial so that you can make function calls to the PayPal testing environment.</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="897d9-342">이 샘플 응용 프로그램에서는 C# 파일(.cs)에 자격 증명을 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-342">In this sample application you are simply adding credentials to a C# file (.cs).</span></span> <span data-ttu-id="897d9-343">그러나 구현된 솔루션에서는 구성 파일에서 자격 증명을 암호화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-343">However, in a implemented solution, you should consider encrypting your credentials in a configuration file.</span></span>

<span data-ttu-id="897d9-344">NVPAPICaller 클래스는 페이팔 기능의 대부분을 포함.</span><span class="sxs-lookup"><span data-stu-id="897d9-344">The NVPAPICaller class contains the majority of the PayPal functionality.</span></span> <span data-ttu-id="897d9-345">클래스의 코드는 PayPal 테스트 환경에서 테스트 구매하는 데 필요한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-345">The code in the class provides the methods needed to make a test purchase from the PayPal testing environment.</span></span> <span data-ttu-id="897d9-346">다음 세 가지 페이팔 기능은 구매를 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-346">The following three PayPal functions are used to make purchases:</span></span>

- <span data-ttu-id="897d9-347">`SetExpressCheckout` 함수</span><span class="sxs-lookup"><span data-stu-id="897d9-347">`SetExpressCheckout` function</span></span>
- <span data-ttu-id="897d9-348">`GetExpressCheckoutDetails` 함수</span><span class="sxs-lookup"><span data-stu-id="897d9-348">`GetExpressCheckoutDetails` function</span></span>
- <span data-ttu-id="897d9-349">`DoExpressCheckoutPayment` 함수</span><span class="sxs-lookup"><span data-stu-id="897d9-349">`DoExpressCheckoutPayment` function</span></span>

<span data-ttu-id="897d9-350">이 `ShortcutExpressCheckout` 방법은 장바구니에서 테스트 구매 정보 및 제품 `SetExpressCheckout` 세부 정보를 수집하고 PayPal 기능을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-350">The `ShortcutExpressCheckout` method collects the test purchase information and product details from the shopping cart and calls the `SetExpressCheckout` PayPal function.</span></span> <span data-ttu-id="897d9-351">이 `GetCheckoutDetails` 방법은 구매 세부 정보를 `GetExpressCheckoutDetails` 확인하고 테스트 구매를하기 전에 PayPal 기능을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-351">The `GetCheckoutDetails` method confirms purchase details and calls the `GetExpressCheckoutDetails` PayPal function before making the test purchase.</span></span> <span data-ttu-id="897d9-352">이 `DoCheckoutPayment` 방법은 `DoExpressCheckoutPayment` PayPal 함수를 호출하여 테스트 환경에서 테스트 구매를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-352">The `DoCheckoutPayment` method completes the test purchase from the testing environment by calling the `DoExpressCheckoutPayment` PayPal function.</span></span> <span data-ttu-id="897d9-353">나머지 코드는 문자열 인코딩, 문자열 디코딩, 처리 배열 및 자격 증명 결정과 같은 PayPal 메서드 및 프로세스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-353">The remaining code supports the PayPal methods and process, such as encoding strings, decoding strings, processing arrays, and determining credentials.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="897d9-354">PayPal을 사용하면 [PayPal의 API 사양에](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)따라 선택적 구매 세부 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-354">PayPal allows you to include optional purchase details based on [PayPal's API specification](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout).</span></span> <span data-ttu-id="897d9-355">Wingtip Toys 샘플 응용 프로그램에서 코드를 확장하여 지역화 세부 정보, 제품 설명, 세금, 고객 서비스 번호 및 기타 여러 선택적 필드를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-355">By extending the code in the Wingtip Toys sample application, you can include localization details, product descriptions, tax, a customer service number, as well as many other optional fields.</span></span>

<span data-ttu-id="897d9-356">**바로 가기익스프레스체크아웃** 메서드에 지정된 반환 및 취소 URL은 포트 번호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-356">Notice that the return and cancel URLs that are specified in the **ShortcutExpressCheckout** method use a port number.</span></span>

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

<span data-ttu-id="897d9-357">Visual Web 개발자가 SSL을 사용하여 웹 프로젝트를 실행하면 일반적으로 포트 44300이 웹 서버에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-357">When Visual Web Developer runs a web project using SSL, commonly the port 44300 is used for the web server.</span></span> <span data-ttu-id="897d9-358">위와 같이 포트 번호는 44300입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-358">As shown above, the port number is 44300.</span></span> <span data-ttu-id="897d9-359">응용 프로그램을 실행하면 다른 포트 번호가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-359">When you run the application, you could see a different port number.</span></span> <span data-ttu-id="897d9-360">이 자습서의 끝에서 Wingtip Toys 샘플 응용 프로그램을 성공적으로 실행할 수 있도록 코드에서 포트 번호를 올바르게 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-360">Your port number needs to be correctly set in the code so that you can successful run the Wingtip Toys sample application at the end of this tutorial.</span></span> <span data-ttu-id="897d9-361">이 자습서의 다음 섹션에서는 로컬 호스트 포트 번호를 검색하고 PayPal 클래스를 업데이트하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-361">The next section of this tutorial explains how to retrieve the local host port number and update the PayPal class.</span></span>

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a><span data-ttu-id="897d9-362">페이팔 클래스에서 로컬 호스트 포트 번호 업데이트</span><span class="sxs-lookup"><span data-stu-id="897d9-362">Update the LocalHost Port Number in the PayPal Class</span></span>

<span data-ttu-id="897d9-363">Wingtip Toys 샘플 응용 프로그램은 PayPal 테스트 사이트로 이동하여 Wingtip Toys 샘플 응용 프로그램의 로컬 인스턴스로 돌아가서 제품을 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-363">The Wingtip Toys sample application purchases products by navigating to the PayPal testing site and returning to your local instance of the Wingtip Toys sample application.</span></span> <span data-ttu-id="897d9-364">PayPal이 올바른 URL로 돌아가려면 위에서 언급한 PayPal 코드에서 로컬로 실행 중인 샘플 응용 프로그램의 포트 번호를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-364">In order to have PayPal return to the correct URL, you need to specify the port number of the locally running sample application in the PayPal code mentioned above.</span></span>

1. <span data-ttu-id="897d9-365">**솔루션 탐색기에서** 프로젝트 이름(WingtipToys)을 마우스 오른쪽 단추로 클릭하고**WingtipToys** **속성을**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-365">Right-click the project name (**WingtipToys**) in **Solution Explorer** and select **Properties**.</span></span>
2. <span data-ttu-id="897d9-366">왼쪽 열에서 **웹** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-366">In the left column, select the **Web** tab.</span></span>
3. <span data-ttu-id="897d9-367">**프로젝트 URL** 상자에서 포트 번호를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-367">Retrieve the port number from the **Project Url** box.</span></span>
4. <span data-ttu-id="897d9-368">필요한 경우 *PayPalFunctions.cs* `cancelURL` 파일의 PayPal`NVPAPICaller`클래스 ()를 업데이트하여 `returnURL` 웹 응용 프로그램의 포트 번호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-368">If needed, update the `returnURL` and `cancelURL` in the PayPal class (`NVPAPICaller`) in the *PayPalFunctions.cs* file to use the port number of your web application:</span></span>   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

<span data-ttu-id="897d9-369">이제 추가한 코드가 로컬 웹 응용 프로그램에 대한 예상 포트와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-369">Now the code that you added will match the expected port for your local Web application.</span></span> <span data-ttu-id="897d9-370">페이팔은 로컬 컴퓨터에서 올바른 URL로 돌아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-370">PayPal will be able to return to the correct URL on your local machine.</span></span>

### <a name="add-the-paypal-checkout-button"></a><span data-ttu-id="897d9-371">페이팔 체크아웃 버튼 추가</span><span class="sxs-lookup"><span data-stu-id="897d9-371">Add the PayPal Checkout Button</span></span>

<span data-ttu-id="897d9-372">이제 기본 PayPal 함수가 샘플 응용 프로그램에 추가되었으므로 이러한 함수를 호출하는 데 필요한 태그 및 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-372">Now that the primary PayPal functions have been added to the sample application, you can begin adding the markup and code needed to call these functions.</span></span> <span data-ttu-id="897d9-373">먼저 장바구니 페이지에 표시되는 체크아웃 버튼을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-373">First, you must add the checkout button that the user will see on the shopping cart page.</span></span>

1. <span data-ttu-id="897d9-374">*쇼핑카트.aspx 파일을 엽니다.*</span><span class="sxs-lookup"><span data-stu-id="897d9-374">Open the *ShoppingCart.aspx* file.</span></span>
2. <span data-ttu-id="897d9-375">파일 아래쪽으로 스크롤하여 주석을 `<!--Checkout Placeholder -->` 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-375">Scroll to the bottom of the file and find the `<!--Checkout Placeholder -->` comment.</span></span>
3. <span data-ttu-id="897d9-376">다음과 같이 마크업이 대체되도록 주석을 `ImageButton` 컨트롤로 바꿉습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-376">Replace the comment with an `ImageButton` control so that the mark up is replaced as follows:</span></span>  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. <span data-ttu-id="897d9-377">*ShoppingCart.aspx.cs* 파일에서 파일 `UpdateBtn_Click` 끝에 있는 이벤트 처리기 후 `CheckOutBtn_Click` 이벤트 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-377">In the *ShoppingCart.aspx.cs* file, after the `UpdateBtn_Click` event handler near the end of the file, add the `CheckOutBtn_Click` event handler:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. <span data-ttu-id="897d9-378">또한 *ShoppingCart.aspx.cs* 파일에서 `CheckoutBtn`에 대한 참조를 추가하여 새 이미지 단추를 다음과 같이 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-378">Also in the *ShoppingCart.aspx.cs* file, add a reference to the `CheckoutBtn`, so that the new image button is referenced as follows:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. <span data-ttu-id="897d9-379">변경 내용을 *ShoppingCart.aspx* 파일과 *ShoppingCart.aspx.cs* 파일에 모두 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-379">Save your changes to both the *ShoppingCart.aspx* file and the *ShoppingCart.aspx.cs* file.</span></span>
7. <span data-ttu-id="897d9-380">메뉴에서 **디버그**-&gt;**빌드 WingtipToys를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-380">From the menu, select **Debug**-&gt;**Build WingtipToys**.</span></span>  
   <span data-ttu-id="897d9-381">새로 추가된 **ImageButton** 컨트롤로 프로젝트가 다시 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-381">The project will be rebuilt with the newly added **ImageButton** control.</span></span>

### <a name="send-purchase-details-to-paypal"></a><span data-ttu-id="897d9-382">페이팔로 구매 세부 정보 보내기</span><span class="sxs-lookup"><span data-stu-id="897d9-382">Send Purchase Details to PayPal</span></span>

<span data-ttu-id="897d9-383">사용자가 장바구니*페이지(ShoppingCart.aspx)에서* **체크아웃** 버튼을 클릭하면 구매 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-383">When the user clicks the **Checkout** button on the shopping cart page (*ShoppingCart.aspx*), they'll begin the purchase process.</span></span> <span data-ttu-id="897d9-384">다음 코드는 제품을 구입하는 데 필요한 첫 번째 PayPal 기능을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-384">The following code calls the first PayPal function needed to purchase products.</span></span>

1. <span data-ttu-id="897d9-385">체크 *아웃* 폴더에서 *CheckoutStart.aspx.cs*라는 코드 뒤에 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-385">From the *Checkout* folder, open the code-behind file named *CheckoutStart.aspx.cs*.</span></span>   
   <span data-ttu-id="897d9-386">코드 숨결 파일을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-386">Be sure to open the code-behind file.</span></span>
2. <span data-ttu-id="897d9-387">기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-387">Replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

<span data-ttu-id="897d9-388">응용 프로그램의 사용자가 장바구니 페이지의 **체크 아웃** 단추를 클릭하면 브라우저는 *CheckoutStart.aspx* 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-388">When the user of the application clicks the **Checkout** button on the shopping cart page, the browser will navigate to the *CheckoutStart.aspx* page.</span></span> <span data-ttu-id="897d9-389">*CheckoutStart.aspx* 페이지가 로드되면 `ShortcutExpressCheckout` 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-389">When the *CheckoutStart.aspx* page loads, the `ShortcutExpressCheckout` method is called.</span></span> <span data-ttu-id="897d9-390">이 시점에서 사용자는 PayPal 테스트 웹 사이트로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-390">At this point, the user is transferred to the PayPal testing web site.</span></span> <span data-ttu-id="897d9-391">페이팔 사이트에서 사용자는 PayPal 자격 증명을 입력하고 구매 세부 정보를 검토하고 PayPal 계약을 수락하고 메서드가 `ShortcutExpressCheckout` 완료되는 Wingtip Toys 샘플 응용 프로그램으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-391">On the PayPal site, the user enters their PayPal credentials, reviews the purchase details, accepts the PayPal agreement and returns to the Wingtip Toys sample application where the `ShortcutExpressCheckout` method completes.</span></span> <span data-ttu-id="897d9-392">메서드가 `ShortcutExpressCheckout` 완료되면 `ShortcutExpressCheckout` 메서드에 지정된 *CheckoutReview.aspx* 페이지로 사용자를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-392">When the `ShortcutExpressCheckout` method is complete, it will redirect the user to the *CheckoutReview.aspx* page specified in the `ShortcutExpressCheckout` method.</span></span> <span data-ttu-id="897d9-393">이를 통해 사용자는 Wingtip Toys 샘플 응용 프로그램 내에서 주문 세부 정보를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-393">This allows the user to review the order details from within the Wingtip Toys sample application.</span></span>

### <a name="review-order-details"></a><span data-ttu-id="897d9-394">주문 세부 정보 검토</span><span class="sxs-lookup"><span data-stu-id="897d9-394">Review Order Details</span></span>

<span data-ttu-id="897d9-395">페이팔에서 반환 한 후, Wingtip 장난감 샘플 응용 프로그램의 *체크 아웃검토.aspx* 페이지 주문 세부 사항을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-395">After returning from PayPal, the *CheckoutReview.aspx* page of the Wingtip Toys sample application displays the order details.</span></span> <span data-ttu-id="897d9-396">이 페이지에서는 제품을 구입하기 전에 주문 세부 정보를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-396">This page allows the user to review the order details before purchasing the products.</span></span> <span data-ttu-id="897d9-397">*CheckoutReview.aspx* 페이지는 다음과 같이 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-397">The *CheckoutReview.aspx* page must be created as follows:</span></span>

1. <span data-ttu-id="897d9-398">체크 *아웃* 폴더에서 *CheckoutReview.aspx*라는 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-398">In the *Checkout* folder, open the page named *CheckoutReview.aspx*.</span></span>
2. <span data-ttu-id="897d9-399">기존 태그를 다음으로 바꿉꿉을 바꿉입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-399">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. <span data-ttu-id="897d9-400">*CheckoutReview.aspx.cs* 라는 코드 뒤에 페이지를 열고 기존 코드를 다음과 같은 것으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-400">Open the code-behind page named *CheckoutReview.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

<span data-ttu-id="897d9-401">**DetailsView** 컨트롤은 PayPal에서 반환된 주문 세부 정보를 표시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-401">The **DetailsView** control is used to display the order details that have been returned from PayPal.</span></span> <span data-ttu-id="897d9-402">또한 위의 코드는 주문 세부 정보를 Wingtip Toys `OrderDetail` 데이터베이스에 개체로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-402">Also, the above code saves the order details to the Wingtip Toys database as an `OrderDetail` object.</span></span> <span data-ttu-id="897d9-403">사용자가 **주문 완료** 버튼을 클릭하면 *체크 아웃Complete.aspx* 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-403">When the user clicks on the **Complete Order** button, they are redirected to the *CheckoutComplete.aspx* page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="897d9-404">**팁**</span><span class="sxs-lookup"><span data-stu-id="897d9-404">**Tip**</span></span>
> 
> <span data-ttu-id="897d9-405">*CheckoutReview.aspx* 페이지의 태그에서 `<ItemStyle>` 태그는 페이지 하단 근처의 **DetailsView** 컨트롤 내의 항목 스타일을 변경하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-405">In the markup of the *CheckoutReview.aspx* page, notice that the `<ItemStyle>` tag is used to change the style of the items within the **DetailsView** control near the bottom of the page.</span></span> <span data-ttu-id="897d9-406">**디자인 보기의** 페이지를 보고(Visual Studio의 왼쪽 아래 모서리에서 **디자인을** 선택한 다음 **DetailsView** 컨트롤을 선택하고 **스마트 태그(컨트롤** 의 오른쪽 상단에 있는 화살표 아이콘)를 선택하면 **DetailsView 작업을**볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-406">By viewing the page in **Design View** (by selecting **Design** at the lower left corner of Visual Studio), then selecting the **DetailsView** control, and selecting the **Smart Tag** (the arrow icon at the top right of the control), you will be able to see the **DetailsView Tasks**.</span></span>
> 
> ![페이팔로 결제 및 결제 - 필드 편집](checkout-and-payment-with-paypal/_static/image18.png)
> 
> <span data-ttu-id="897d9-408">필드 **편집을**선택하면 **필드** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-408">By selecting **Edit Fields**, the **Fields** dialog box will appear.</span></span> <span data-ttu-id="897d9-409">이 대화 상자에서 **DetailsView** 컨트롤의 **ItemStyle**, 와 같은 시각적 속성을 쉽게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-409">In this dialog box you can easily control the visual properties, such as **ItemStyle**, of the **DetailsView** control.</span></span>
> 
> ![페이팔로 결제 및 결제 - 필드 대화 상자](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a><span data-ttu-id="897d9-411">전체 구매</span><span class="sxs-lookup"><span data-stu-id="897d9-411">Complete Purchase</span></span>

<span data-ttu-id="897d9-412">*체크 아웃완료.aspx* 페이지는 페이팔에서 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-412">*CheckoutComplete.aspx* page makes the purchase from PayPal.</span></span> <span data-ttu-id="897d9-413">위에서 언급했듯이 사용자는 응용 프로그램이 *CheckoutComplete.aspx* 페이지로 이동하기 전에 **주문 완료** 버튼을 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-413">As mentioned above, the user must click on the **Complete Order** button before the application will navigate to the *CheckoutComplete.aspx* page.</span></span>

1. <span data-ttu-id="897d9-414">체크 *아웃* 폴더에서 체크 아웃이라는 페이지를 엽니다.Complete.aspx . *CheckoutComplete.aspx*</span><span class="sxs-lookup"><span data-stu-id="897d9-414">In the *Checkout* folder, open the page named *CheckoutComplete.aspx*.</span></span>
2. <span data-ttu-id="897d9-415">기존 태그를 다음으로 바꿉꿉을 바꿉입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-415">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. <span data-ttu-id="897d9-416">*CheckoutComplete.aspx.cs* 라는 코드 뒤에 페이지를 열고 기존 코드를 다음과 같은 것으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-416">Open the code-behind page named *CheckoutComplete.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

<span data-ttu-id="897d9-417">체크 *아웃Complete.aspx* 페이지가 로드 `DoCheckoutPayment` 될 때 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-417">When the *CheckoutComplete.aspx* page is loaded, the `DoCheckoutPayment` method is called.</span></span> <span data-ttu-id="897d9-418">앞에서 설명한 `DoCheckoutPayment` 것처럼 이 방법은 PayPal 테스트 환경에서 구매를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-418">As mentioned earlier, the `DoCheckoutPayment` method completes the purchase from the PayPal testing environment.</span></span> <span data-ttu-id="897d9-419">PayPal이 주문 구매를 완료하면 *결제Complete.aspx* 페이지에 구매자에게 결제 `ID` 트랜잭션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-419">Once PayPal has completed the purchase of the order, the *CheckoutComplete.aspx* page displays a payment transaction `ID` to the purchaser.</span></span>

### <a name="handle-cancel-purchase"></a><span data-ttu-id="897d9-420">구매 취소 처리</span><span class="sxs-lookup"><span data-stu-id="897d9-420">Handle Cancel Purchase</span></span>

<span data-ttu-id="897d9-421">사용자가 구매를 취소하기로 결정한 경우 *CheckoutCancel.aspx* 페이지로 이동하여 주문이 취소되었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-421">If the user decides to cancel the purchase, they will be directed to the *CheckoutCancel.aspx* page where they will see that their order has been cancelled.</span></span>

1. <span data-ttu-id="897d9-422">*체크 아웃* 폴더에서 *CheckoutCancel.aspx라는* 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-422">Open the page named *CheckoutCancel.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="897d9-423">기존 태그를 다음으로 바꿉꿉을 바꿉입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-423">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a><span data-ttu-id="897d9-424">구매 오류 처리</span><span class="sxs-lookup"><span data-stu-id="897d9-424">Handle Purchase Errors</span></span>

<span data-ttu-id="897d9-425">구매 프로세스 중 오류는 *CheckoutError.aspx* 페이지에서 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-425">Errors during the purchase process will be handled by the *CheckoutError.aspx* page.</span></span> <span data-ttu-id="897d9-426">*CheckoutStart.aspx* 페이지의 코드 뒤에, *CheckoutReview.aspx* 페이지, 그리고 *체크 아웃Complete.aspx* 페이지 각 리디렉션됩니다 *체크 아웃Error.aspx* 오류 발생 하는 경우 페이지.</span><span class="sxs-lookup"><span data-stu-id="897d9-426">The code-behind of the *CheckoutStart.aspx* page, the *CheckoutReview.aspx* page, and the *CheckoutComplete.aspx* page will each redirect to the *CheckoutError.aspx* page if an error occurs.</span></span>

1. <span data-ttu-id="897d9-427">*체크 아웃* 폴더에서 *CheckoutError.aspx라는* 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-427">Open the page named *CheckoutError.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="897d9-428">기존 태그를 다음으로 바꿉꿉을 바꿉입니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-428">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

<span data-ttu-id="897d9-429">*체크 아웃Error.aspx* 페이지는 체크 아웃 프로세스 중에 오류가 발생할 때 오류 세부 정보와 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-429">The *CheckoutError.aspx* page is displayed with the error details when an error occurs during the checkout process.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="897d9-430">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="897d9-430">Running the Application</span></span>

<span data-ttu-id="897d9-431">응용 프로그램을 실행하여 제품을 구입하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-431">Run the application to see how to purchase products.</span></span> <span data-ttu-id="897d9-432">페이팔 테스트 환경에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-432">Note that you will be running in the PayPal testing environment.</span></span> <span data-ttu-id="897d9-433">실제 돈은 교환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-433">No actual money is being exchanged.</span></span>

1. <span data-ttu-id="897d9-434">모든 파일이 Visual Studio에 저장되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-434">Make sure all your files are saved in Visual Studio.</span></span>
2. <span data-ttu-id="897d9-435">웹 브라우저를 열고 [https://developer.paypal.com](https://developer.paypal.com/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-435">Open a Web browser and navigate to [https://developer.paypal.com](https://developer.paypal.com/).</span></span>
3. <span data-ttu-id="897d9-436">이 자습서의 앞에서 만든 PayPal 개발자 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-436">Login with your PayPal developer account that you created earlier in this tutorial.</span></span>  
   <span data-ttu-id="897d9-437">페이팔의 개발자 샌드 박스에 대 한, 익스프레스 [https://developer.paypal.com](https://developer.paypal.com/) 체크 아웃을 테스트 하려면 로그인 해야.</span><span class="sxs-lookup"><span data-stu-id="897d9-437">For PayPal's developer sandbox, you need to be logged in at [https://developer.paypal.com](https://developer.paypal.com/) to test express checkout.</span></span> <span data-ttu-id="897d9-438">이는 페이팔의 샌드박스 테스트에만 적용되며 페이팔의 라이브 환경에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-438">This only applies to PayPal's sandbox testing, not to PayPal's live environment.</span></span>
4. <span data-ttu-id="897d9-439">비주얼 스튜디오에서 **F5를** 눌러 Wingtip Toys 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-439">In Visual Studio, press **F5** to run the Wingtip Toys sample application.</span></span>  
   <span data-ttu-id="897d9-440">데이터베이스가 다시 빌드되면 브라우저가 열리고 *Default.aspx* 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-440">After the database rebuilds, the browser will open and show the *Default.aspx* page.</span></span>
5. <span data-ttu-id="897d9-441">'자동차'와 같은 제품 카테고리를 선택한 다음 각 제품 옆에 **장바구니에 추가를** 클릭하여 장바구니에 세 가지 다른 제품을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-441">Add three different products to the shopping cart by selecting the product category, such as "Cars" and then clicking **Add to Cart** next to each product.</span></span>  
   <span data-ttu-id="897d9-442">장바구니에 선택한 제품이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-442">The shopping cart will display the product you have selected.</span></span>
6. <span data-ttu-id="897d9-443">결제하려면 **페이팔** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-443">Click the **PayPal** button to checkout.</span></span> 

    ![페이팔로 결제 및 결제 - 카트](checkout-and-payment-with-paypal/_static/image20.png)

   <span data-ttu-id="897d9-445">체크 아웃하려면 Wingtip Toys 샘플 응용 프로그램에 대한 사용자 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-445">Checking out will require that you have a user account for the Wingtip Toys sample application.</span></span>
7. <span data-ttu-id="897d9-446">페이지 오른쪽에 있는 **Google** 링크를 클릭하여 기존 gmail.com 이메일 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-446">Click the **Google** link on the right of the page to log in with an existing gmail.com email account.</span></span>  
   <span data-ttu-id="897d9-447">gmail.com 계정이 없는 경우 [www.gmail.com](https://www.gmail.com/)에서 테스트 목적으로 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-447">If you do not have a gmail.com account, you can create one for testing purposes at [www.gmail.com](https://www.gmail.com/).</span></span> <span data-ttu-id="897d9-448">"등록"을 클릭하여 표준 로컬 계정을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-448">You can also use a standard local account by clicking "Register".</span></span> 

    ![페이팔로 결제 및 결제 - 로그인](checkout-and-payment-with-paypal/_static/image21.png)
8. <span data-ttu-id="897d9-450">Gmail 계정 및 비밀번호로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-450">Sign in with your gmail account and password.</span></span> 

    ![페이팔로 결제 및 결제 - Gmail 로그인](checkout-and-payment-with-paypal/_static/image22.png)
9. <span data-ttu-id="897d9-452">**로그인** 버튼을 클릭하여 Wingtip Toys 샘플 응용 프로그램 사용자 이름으로 Gmail 계정을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-452">Click the **Log in** button to register your gmail account with your Wingtip Toys sample application user name.</span></span> 

    ![페이팔로 결제 및 결제 - 계정 등록](checkout-and-payment-with-paypal/_static/image23.png)
10. <span data-ttu-id="897d9-454">PayPal 테스트 사이트에서 이 자습서의 앞부분에서 만든 **구매자** 이메일 주소와 암호를 추가한 다음 **로그인** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-454">On the PayPal test site, add your **buyer** email address and password that you created earlier in this tutorial, then click the **Log In** button.</span></span> 

    ![페이팔로 결제 및 결제 - 페이팔 로그인](checkout-and-payment-with-paypal/_static/image24.png)
11. <span data-ttu-id="897d9-456">PayPal 정책에 동의하고 **동의 및 계속** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-456">Agree to the PayPal policy and click the **Agree and Continue** button.</span></span>  
    <span data-ttu-id="897d9-457">이 페이지는 이 PayPal 계정을 처음 사용할 때만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-457">Note that this page is only displayed the first time you use this PayPal account.</span></span> <span data-ttu-id="897d9-458">다시이 테스트 계정입니다, 실제 돈이 교환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-458">Again note that this is a test account, no real money is exchanged.</span></span> 

    ![페이팔 결제 및 결제 - 페이팔 정책](checkout-and-payment-with-paypal/_static/image25.png)
12. <span data-ttu-id="897d9-460">PayPal 테스트 환경 검토 페이지에서 주문 정보를 검토하고 **계속을 클릭합니다.**</span><span class="sxs-lookup"><span data-stu-id="897d9-460">Review the order information on the PayPal testing environment review page and click **Continue**.</span></span> 

    ![페이팔로 결제 및 결제 - 리뷰 정보](checkout-and-payment-with-paypal/_static/image26.png)
13. <span data-ttu-id="897d9-462">*CheckoutReview.aspx* 페이지에서 주문 금액을 확인하고 생성된 배송 주소를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-462">On the *CheckoutReview.aspx* page, verify the order amount and view the generated shipping address.</span></span> <span data-ttu-id="897d9-463">그런 다음 **주문 완료** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-463">Then, click the **Complete Order** button.</span></span> 

    ![페이팔결제 - 주문 검토](checkout-and-payment-with-paypal/_static/image27.png)
14. <span data-ttu-id="897d9-465">**결제완료.aspx** 페이지가 결제 거래 ID와 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-465">The **CheckoutComplete.aspx** page is displayed with a payment transaction ID.</span></span> 

    ![페이팔로 결제 및 결제 - 결제 완료](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a><span data-ttu-id="897d9-467">데이터베이스 검토</span><span class="sxs-lookup"><span data-stu-id="897d9-467">Reviewing the Database</span></span>

<span data-ttu-id="897d9-468">응용 프로그램을 실행한 후 Wingtip Toys 샘플 응용 프로그램 데이터베이스에서 업데이트된 데이터를 검토하면 응용 프로그램이 제품 구매를 성공적으로 기록한 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-468">By reviewing the updated data in the Wingtip Toys sample application database after running the application, you can see that the application successfully recorded the purchase of the products.</span></span>

<span data-ttu-id="897d9-469">이 자습서 시리즈의 이전과 마찬가지로 **데이터베이스 탐색기** 창(Visual Studio의**서버 탐색기** 창)을 사용하여 *Wingtiptoys.mdf* 데이터베이스 파일에 포함된 데이터를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-469">You can inspect the data contained in the *Wingtiptoys.mdf* database file by using the **Database Explorer** window (**Server Explorer** window in Visual Studio) as you did earlier in this tutorial series.</span></span>

1. <span data-ttu-id="897d9-470">여전히 열려 있는 경우 브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-470">Close the browser window if it is still open.</span></span>
2. <span data-ttu-id="897d9-471">Visual Studio에서 **솔루션 탐색기** 상단의 **모든 파일 표시** 아이콘을 선택하여 앱 **\_데이터** 폴더를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-471">In Visual Studio, select the **Show All Files** icon at the top of **Solution Explorer** to allow you to expand the **App\_Data** folder.</span></span>
3. <span data-ttu-id="897d9-472">**앱\_데이터** 폴더를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-472">Expand the **App\_Data** folder.</span></span>  
 <span data-ttu-id="897d9-473">폴더에 대한 **모든 파일 표시** 아이콘을 선택해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-473">You may need to select the **Show All Files** icon for the folder.</span></span>
4. <span data-ttu-id="897d9-474">*Wingtiptoys.mdf* 데이터베이스 파일을 마우스 오른쪽 단추로 클릭하고 **열기를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-474">Right-click the *Wingtiptoys.mdf* database file and select **Open**.</span></span>  
    <span data-ttu-id="897d9-475">**서버 탐색기가** 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-475">**Server Explorer** is displayed.</span></span>
5. <span data-ttu-id="897d9-476">**테이블** 폴더를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-476">Expand the **Tables** folder.</span></span>
6. <span data-ttu-id="897d9-477">**주문**테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 데이터 표시를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-477">Right-click the **Orders**table and select **Show Table Data**.</span></span>  
 <span data-ttu-id="897d9-478">**Orders** 테이블이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-478">The **Orders** table is displayed.</span></span>
7. <span data-ttu-id="897d9-479">**결제트랜잭션ID** 열을 검토하여 성공적인 트랜잭션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-479">Review the **PaymentTransactionID** column to confirm successful transactions.</span></span> 

    ![페이팔로 결제 및 결제 - 데이터베이스 검토](checkout-and-payment-with-paypal/_static/image29.png)
8. <span data-ttu-id="897d9-481">**주문** 테이블 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-481">Close the **Orders** table window.</span></span>
9. <span data-ttu-id="897d9-482">서버 탐색기에서 **OrderDetails** 테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 데이터 표시를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-482">In the Server Explorer, right-click the **OrderDetails** table and select **Show Table Data**.</span></span>
10. <span data-ttu-id="897d9-483">OrderDetails `OrderId` `Username` 테이블의 값과 값을 **검토합니다.**</span><span class="sxs-lookup"><span data-stu-id="897d9-483">Review the `OrderId` and `Username` values in the **OrderDetails** table.</span></span> <span data-ttu-id="897d9-484">이러한 값은 `OrderId` **Orders** `Username` 테이블에 포함된 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-484">Note that these values match the `OrderId` and `Username` values included in the **Orders** table.</span></span>
11. <span data-ttu-id="897d9-485">**OrderDetails** 테이블 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-485">Close the **OrderDetails** table window.</span></span>
12. <span data-ttu-id="897d9-486">윙팁 장난감 데이터베이스*파일(Wingtiptoys.mdf)을*마우스 오른쪽 버튼으로 클릭하고 **연결 닫기를**선택합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-486">Right-click the Wingtip Toys database file (*Wingtiptoys.mdf*) and select **Close Connection**.</span></span>
13. <span data-ttu-id="897d9-487">**솔루션 탐색기** 창이 표시되지 않으면 **서버 탐색기** 창 하단의 **솔루션 탐색기를** 클릭하여 **솔루션 탐색기를** 다시 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-487">If you do not see the **Solution Explorer** window, click **Solution Explorer** at the bottom of the **Server Explorer** window to show the **Solution Explorer** again.</span></span>

## <a name="summary"></a><span data-ttu-id="897d9-488">요약</span><span class="sxs-lookup"><span data-stu-id="897d9-488">Summary</span></span>

<span data-ttu-id="897d9-489">이 자습서에서는 제품 구매를 추적하기 위해 주문 및 주문 세부 스키마를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-489">In this tutorial you added order and order detail schemas to track the purchase of products.</span></span> <span data-ttu-id="897d9-490">또한 PayPal 기능을 Wingtip Toys 샘플 애플리케이션에 통합했습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-490">You also integrated PayPal functionality into the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="897d9-491">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="897d9-491">Additional Resources</span></span>

<span data-ttu-id="897d9-492">[ASP.NET 구성 개요](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="897d9-492">[ASP.NET Configuration Overview](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span></span>  
[<span data-ttu-id="897d9-493">Azure 앱 서비스에 멤버십, OAuth 및 SQL 데이터베이스를 사용하여 보안 ASP.NET 웹 양식 앱 배포</span><span class="sxs-lookup"><span data-stu-id="897d9-493">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="897d9-494">마이크로소프트 Azure - 무료 평가판</span><span class="sxs-lookup"><span data-stu-id="897d9-494">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a><span data-ttu-id="897d9-495">고지 사항</span><span class="sxs-lookup"><span data-stu-id="897d9-495">Disclaimer</span></span>

<span data-ttu-id="897d9-496">이 자습서에는 샘플 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-496">This tutorial contains sample code.</span></span> <span data-ttu-id="897d9-497">이러한 샘플 코드는 어떤 종류의 보증없이 "있는 대로"제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-497">Such sample code is provided "as is" without warranty of any kind.</span></span> <span data-ttu-id="897d9-498">따라서 Microsoft는 샘플 코드의 정확성, 무결성 또는 품질을 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-498">Accordingly, Microsoft does not guarantee the accuracy, integrity, or quality of the sample code.</span></span> <span data-ttu-id="897d9-499">당신은 당신의 자신의 위험에 샘플 코드를 사용하는 데 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-499">You agree to use the sample code at your own risk.</span></span> <span data-ttu-id="897d9-500">어떠한 경우에도 Microsoft는 샘플 코드, 콘텐츠(이에 국한되지 않음)에 대해 어떠한 방식으로든 귀하에게 책임을 지지 않으며, 샘플 코드, 콘텐츠 또는 샘플 코드 사용으로 인해 발생한 모든 종류의 손실 또는 손상을 포함하되 이에 국한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-500">Under no circumstances will Microsoft be liable to you in any way for any sample code, content, including but not limited to, any errors or omissions in any sample code, content, or any loss or damage of any kind incurred as a result of the use of any sample code.</span></span> <span data-ttu-id="897d9-501">귀하는 이에 대해 Microsoft가 게시, 전송, 사용 또는 이에 국한되지 않는 자료를 포함하되 이에 국한되지 않는 모든 종류의 손실, 손실, 상해 또는 손해에 대해 무해한 배상, 저장 및 보유하는 데 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="897d9-501">You are hereby notified and do hereby agree to indemnify, save and hold Microsoft harmless from and against any and all loss, claims of loss, injury or damage of any kind including, without limitation, those occasioned by or arising from material that you post, transmit, use or rely on including, but not limited to, the views expressed therein.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="897d9-502">[이전](shopping-cart.md)
> [다음](membership-and-administration.md)</span><span class="sxs-lookup"><span data-stu-id="897d9-502">[Previous](shopping-cart.md)
[Next](membership-and-administration.md)</span></span>
