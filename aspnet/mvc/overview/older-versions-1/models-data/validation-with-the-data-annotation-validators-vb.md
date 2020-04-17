---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 데이터 항법 유효성 검사기(VB)로 유효성 검사 | 마이크로 소프트 문서
author: rick-anderson
description: 데이터 부수 모델 바인더를 활용하여 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행합니다. 다양한 유형의 유효성 검사기를 사용하는 방법에 대해 알아봅니다...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: cabdf6dab9e5de53a45adcf126705533fca02de7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542640"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="67af7-104">데이터 주석 유효성 검사기를 사용한 유효성 검사(VB)</span><span class="sxs-lookup"><span data-stu-id="67af7-104">Validation with the Data Annotation Validators (VB)</span></span>

<span data-ttu-id="67af7-105">[로 마이크로 소프트](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="67af7-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="67af7-106">데이터 부수 모델 바인더를 활용하여 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="67af7-107">다양한 유형의 유효성 검사기 특성을 사용하고 Microsoft 엔터티 프레임워크에서 유효성 검사기 특성과 함께 작업하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="67af7-108">이 자습서에서는 데이터 별표 유효성 검사기를 사용하여 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="67af7-109">데이터 별표 유효성 검사기를 사용하면 필수 또는 StringLength 특성과 같은 하나 이상의 특성을 클래스 속성에 추가하여 유효성 검사를 수행할 수 있다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="67af7-110">데이터 주석 유효성 검사기를 사용하려면 먼저 데이터 주석 모델 바인더를 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="67af7-111">여기를 클릭하여 CodePlex 웹 사이트에서 데이터 주석 모델 바인더 샘플을 다운로드할 수 [있습니다.](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)</span><span class="sxs-lookup"><span data-stu-id="67af7-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="67af7-112">데이터 주석 모델 바인더는 Microsoft ASP.NET MVC 프레임워크의 공식 적인 부분이 아니라는 점을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="67af7-113">데이터 주석 모델 바인더는 Microsoft ASP.NET MVC 팀에 의해 만들어졌지만 Microsoft는 이 자습서에서 설명하고 사용하는 데이터 주석 모델 바인더에 대한 공식 제품 지원을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="67af7-114">데이터 추가 모델 바인더 사용</span><span class="sxs-lookup"><span data-stu-id="67af7-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="67af7-115">ASP.NET MVC 응용 프로그램에서 데이터 주석 모델 바인더를 사용하려면 먼저 Microsoft.Web.Mvc.DataAnnotations.dll 어셈블리 및 System.ComponentModel.DataAnnotations.dll 어셈블리에 대한 참조를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="67af7-116">메뉴 옵션 **프로젝트를 선택, 참조 추가.**</span><span class="sxs-lookup"><span data-stu-id="67af7-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="67af7-117">다음으로 **찾아보기** 탭을 클릭하고 데이터 주석 모델 바인더 샘플을 다운로드하고 압축을 풀었던 위치로 이동합니다(그림 **1**참조).</span><span class="sxs-lookup"><span data-stu-id="67af7-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="67af7-118">**그림 1**: 데이터 주석 모델 바인더에 대한 참조 추가[(전체 크기 이미지를 보려면 클릭)](validation-with-the-data-annotation-validators-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="67af7-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="67af7-119">Microsoft.Web.Mvc.DataAnnotations.dll 어셈블리와 System.ComponentModel.DataAnnotations.dll 어셈블리를 모두 선택하고 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="67af7-120">데이터 주석 모델 바인더가 있는 .NET 프레임워크 서비스 팩 1에 포함된 System.ComponentModel.DataAnnotations.dll 어셈블리는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="67af7-121">데이터 주석 모델 바인더 샘플 다운로드에 포함된 System.ComponentModel.DataAnnotations.dll 어셈블리 버전을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="67af7-122">마지막으로 Global.asax 파일에 데이터Annotations 모델 바인더를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="67af7-123">응용\_\_프로그램 Start() 메서드가 다음과 같이 보이도록 다음 코드 줄을 응용 프로그램 Start() 이벤트 처리기에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="67af7-124">이 코드 줄은 전체 ASP.NET MVC 응용 프로그램의 기본 모델 바인더로 DataAnnotationsModelBinder를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="67af7-125">데이터 추가 유효성 검사기 특성 사용</span><span class="sxs-lookup"><span data-stu-id="67af7-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="67af7-126">데이터 주석 모델 바인더를 사용하는 경우 유효성 검사기 특성을 사용하여 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="67af7-127">System.ComponentModel.DataAnotations 네임스페이스에는 다음 유효성 검사기 특성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="67af7-128">범위 - 속성 값이 지정된 값 범위 사이에 속하는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="67af7-129">정규 표현식 - 속성 값이 지정된 정규식 패턴과 일치하는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="67af7-130">필수 – 필요에 따라 속성을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="67af7-131">StringLength - 문자열 속성의 최대 길이를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="67af7-132">유효성 검사 - 모든 유효성 검사기 특성에 대한 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="67af7-133">유효성 검사 요구 사항이 표준 유효성 검사기에 의해 충족되지 않으면 항상 기본 유효성 검사기 특성에서 새 유효성 검사기 특성을 상속하여 사용자 지정 유효성 검사기 특성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="67af7-134">**목록 1의** 제품 클래스는 이러한 유효성 검사기 특성을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="67af7-135">이름, 설명 및 UnitPrice 속성은 필수로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="67af7-136">Name 속성의 문자열 길이는 10자 미만이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="67af7-137">마지막으로 UnitPrice 속성은 통화 금액을 나타내는 정규식 패턴과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="67af7-138">**목록 1**: 모델\Product.vb</span><span class="sxs-lookup"><span data-stu-id="67af7-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="67af7-139">Product 클래스는 하나의 추가 특성인 DisplayName 특성을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="67af7-140">DisplayName 특성을 사용하면 속성이 오류 메시지에 표시될 때 속성 이름을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="67af7-141">"UnitPrice 필드가 필요합니다"라는 오류 메시지를 표시하는 대신 "가격 필드가 필요합니다"라는 오류 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="67af7-142">유효성 검사기에서 표시되는 오류 메시지를 완전히 사용자 지정하려면 다음과 같이 유효성 검사기의 ErrorMessage 속성에 사용자 지정 오류 메시지를 할당할 수 있습니다.`<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="67af7-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="67af7-143">**목록 1의** 제품 클래스를 **목록 2의**Create() 컨트롤러 작업과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="67af7-144">이 컨트롤러 작업은 모델 상태에 오류가 있는 경우 뷰 만들기를 다시 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="67af7-145">**목록 2**: 컨트롤러\제품컨트롤러.vb</span><span class="sxs-lookup"><span data-stu-id="67af7-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="67af7-146">마지막으로 만들기() 작업을 마우스 오른쪽 단추로 클릭하고 **보기 추가**옵션을 선택하여 **목록 3에서** 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="67af7-147">제품 클래스를 모델 클래스로 사용하여 강력한 형식의 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="67af7-148">보기 콘텐츠 드롭다운 목록에서 **만들기를** 선택합니다(그림 **2**참조).</span><span class="sxs-lookup"><span data-stu-id="67af7-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="67af7-149">**그림 2**: 뷰 만들기 추가</span><span class="sxs-lookup"><span data-stu-id="67af7-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="67af7-150">**목록 3**: 보기\제품\만들기.aspx</span><span class="sxs-lookup"><span data-stu-id="67af7-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="67af7-151">**보기 추가** 메뉴 옵션에서 생성된 만들기 양식에서 ID 필드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="67af7-152">Id 필드는 ID 열에 해당하므로 사용자가 이 필드에 대한 값을 입력하도록 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="67af7-153">제품을 만들기 위한 양식을 제출하고 필요한 필드에 대한 값을 입력하지 않으면 그림 **3의** 유효성 검사 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="67af7-154">**그림 3**: 필수 필드 누락</span><span class="sxs-lookup"><span data-stu-id="67af7-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="67af7-155">잘못된 통화 금액을 입력하면 **그림 4의** 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="67af7-156">**그림 4**: 유효하지 않은 통화 금액</span><span class="sxs-lookup"><span data-stu-id="67af7-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="67af7-157">엔터티 프레임워크를 사용하여 데이터 어노미션 유효성 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="67af7-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="67af7-158">Microsoft 엔터티 프레임워크를 사용하여 데이터 모델 클래스를 생성하는 경우 클래스에 유효성 검사기 특성을 직접 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="67af7-159">Entity Framework 디자이너는 모델 클래스를 생성하므로 다음에 디자이너를 변경할 때 모델 클래스에 대한 모든 변경 내용이 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="67af7-160">Entity Framework에서 생성된 클래스와 함께 유효성 검사기를 사용하려면 메타 데이터 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="67af7-161">유효성 검사기를 실제 클래스에 적용하는 대신 메타 데이터 클래스에 유효성 검사기를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="67af7-162">예를 들어 엔터티 프레임워크를 사용하여 Movie 클래스를 만들었다고 가정합니다(그림 **5**참조).</span><span class="sxs-lookup"><span data-stu-id="67af7-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="67af7-163">또한 영화 제목 및 디렉터 속성을 필수 속성으로 만들려는 경우를 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="67af7-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="67af7-164">이 경우 **목록 4에서**부분 클래스 및 메타 데이터 클래스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="67af7-165">**그림 5**: 엔터티 프레임워크에서 생성된 동영상 클래스</span><span class="sxs-lookup"><span data-stu-id="67af7-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="67af7-166">**목록 4**: 모델\Movie.vb</span><span class="sxs-lookup"><span data-stu-id="67af7-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="67af7-167">**리스팅 4의** 파일에는 Movie 및 MovieMetaData라는 두 개의 클래스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="67af7-168">동영상 클래스는 부분 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-168">The Movie class is a partial class.</span></span> <span data-ttu-id="67af7-169">DataModel.Designer.vb 파일에 포함된 엔터티 프레임워크에서 생성된 부분 클래스에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="67af7-170">현재 .NET 프레임워크는 부분 속성을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="67af7-171">따라서 DataModel.Designer.vb 파일에 정의된 Movie 클래스의 속성에 유효성 검사기 특성을 적용하는 방법은 없습니다. **Listing 4**</span><span class="sxs-lookup"><span data-stu-id="67af7-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="67af7-172">동영상 부분 클래스는 MovieMetaData 클래스를 가리키는 MetadataType 특성으로 장식되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="67af7-173">MovieMetaData 클래스에는 Movie 클래스의 속성에 대한 프록시 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="67af7-174">유효성 검사기 특성은 MovieMetaData 클래스의 속성에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="67af7-175">제목, 디렉터 및 날짜 릴리스 속성은 모두 필수 속성으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="67af7-176">Director 속성은 5자 미만을 포함하는 문자열을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="67af7-177">마지막으로 DisplayName 특성은 DateReleased 속성에 적용되어 "해제된 날짜 필드가 필요합니다." 등의 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="67af7-178">오류 대신 "날짜 릴리스 필드가 필요합니다."</span><span class="sxs-lookup"><span data-stu-id="67af7-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="67af7-179">MovieMetaData 클래스의 프록시 속성은 Movie 클래스의 해당 속성과 동일한 형식을 나타낼 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="67af7-180">예를 들어 Director 속성은 Movie 클래스의 문자열 속성이며 MovieMetaData 클래스의 개체 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="67af7-181">**그림 6의** 페이지는 Movie 속성에 대해 잘못된 값을 입력할 때 반환되는 오류 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="67af7-182">**그림 6**: 엔터티 프레임워크가 있는 유효성 검사기 사용[(전체 크기 이미지를 보려면 클릭)](validation-with-the-data-annotation-validators-vb/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="67af7-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="67af7-183">요약</span><span class="sxs-lookup"><span data-stu-id="67af7-183">Summary</span></span>

<span data-ttu-id="67af7-184">이 자습서에서는 데이터 별표 모델 바인더를 활용하여 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="67af7-185">필수 및 StringLength 특성과 같은 다양한 유형의 유효성 검사기 특성을 사용하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="67af7-186">또한 Microsoft 엔터티 프레임워크로 작업할 때 이러한 특성을 사용하는 방법에 대해서도 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="67af7-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="67af7-187">이전</span><span class="sxs-lookup"><span data-stu-id="67af7-187">Previous</span></span>](validating-with-a-service-layer-vb.md)
