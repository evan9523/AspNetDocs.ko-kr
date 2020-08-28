---
uid: mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
title: 세부 정보 및 삭제 메서드 검사 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 03/26/2015
ms.assetid: f1d2a916-626c-4a54-8df4-77e6b9fff355
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 9c4e66454d6995bd750b62ef8b461bcfbdfb4b4f
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045093"
---
# <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="20395-102">세부 정보 및 삭제 메서드 검사</span><span class="sxs-lookup"><span data-stu-id="20395-102">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="20395-103">[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="20395-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="20395-104">자습서의이 부분에서는 자동으로 생성 된 및 메서드를 검사 `Details` 합니다 `Delete` .</span><span class="sxs-lookup"><span data-stu-id="20395-104">In this part of the tutorial, you'll examine the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="20395-105">세부 정보 및 삭제 메서드 검사</span><span class="sxs-lookup"><span data-stu-id="20395-105">Examining the Details and Delete Methods</span></span>

<span data-ttu-id="20395-106">컨트롤러를 열고 `Movie` 메서드를 검사 `Details` 합니다.</span><span class="sxs-lookup"><span data-stu-id="20395-106">Open the `Movie` controller and examine the `Details` method.</span></span>

![](examining-the-details-and-delete-methods/_static/image1.png)

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="20395-107">이 작업 메서드를 만든 MVC 스 캐 폴딩 엔진은 메서드를 호출 하는 HTTP 요청을 보여 주는 주석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="20395-107">The MVC scaffolding engine that created this action method adds a comment showing a HTTP request that invokes the method.</span></span> <span data-ttu-id="20395-108">이 경우 `GET` 세 개의 URL 세그먼트 ( `Movies` 컨트롤러, 메서드 및 값)가 포함 된 요청 `Details` `ID` 입니다.</span><span class="sxs-lookup"><span data-stu-id="20395-108">In this case it's a `GET` request with three URL segments, the `Movies` controller, the `Details` method and a `ID` value.</span></span>

<span data-ttu-id="20395-109">Code First를 사용 하면 메서드를 사용 하 여 데이터를 쉽게 검색할 수 `Find` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20395-109">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="20395-110">메서드에 기본 제공 되는 중요 한 보안 기능은 코드가 `Find` 코드에서 작업을 수행 하려고 시도 하기 전에 메서드가 영화를 발견 했는지 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="20395-110">An important security feature built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="20395-111">예를 들어 해커는 링크로 만든 URL을에서 `http://localhost:xxxx/Movies/Details/1` `http://localhost:xxxx/Movies/Details/12345` (또는 실제 영화를 나타내지 않는 다른 값)로 변경 하 여 사이트에 오류를 발생 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20395-111">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="20395-112">Null 동영상을 검사 하지 않은 경우에는 null 영화에서 데이터베이스 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="20395-112">If you did not check for a null movie, a null movie would result in a database error.</span></span>

<span data-ttu-id="20395-113">`Delete` 및 `DeleteConfirmed` 메서드를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="20395-113">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample2.cs?highlight=17)]

<span data-ttu-id="20395-114">HTTP GET `Delete` 메서드는 지정 된 동영상을 삭제 하지 않으며 삭제를 제출 () 할 수 있는 동영상 뷰를 반환 합니다 `HttpPost` .</span><span class="sxs-lookup"><span data-stu-id="20395-114">Note that the HTTP GET `Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (`HttpPost`) the deletion.</span></span> <span data-ttu-id="20395-115">GET 요청에 대한 응답에서 삭제 작업을 수행하는 것은(또는 해당 문제에 대한 편집 작업, 만들기 작업 또는 데이터를 변경하는 기타 작업을 수행하는 것은) 보안 허점을 야기합니다.</span><span class="sxs-lookup"><span data-stu-id="20395-115">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="20395-116">이에 대 한 자세한 내용은 Stephen Walther의 블로그 항목 [ASP.NET MVC 팁 #46를 참조 하세요. 보안 허점을 만들기 때문에 Delete 링크를 사용 하지 마세요](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span><span class="sxs-lookup"><span data-stu-id="20395-116">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="20395-117">데이터를 삭제하는 `HttpPost` 메서드의 이름은 HTTP POST 메서드에 고유한 서명 또는 이름을 부여하기 위해 `DeleteConfirmed`로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="20395-117">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="20395-118">두 메서드의 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="20395-118">The two method signatures are shown below:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="20395-119">CLR(공용 언어 런타임)은 고유한 매개 변수 서명을 갖기 위해 오버로드된 메서드가 필요합니다(동일한 메서드 이름이지만 다른 매개 변수의 목록).</span><span class="sxs-lookup"><span data-stu-id="20395-119">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="20395-120">그러나 여기에서 두 개의 Delete 메서드 (GET의 경우 하나, POST의 경우 one)는 동일한 매개 변수 시그니처를 갖고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20395-120">However, here you need two Delete methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="20395-121">(모두 매개 변수로 단일 정수를 허용해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="20395-121">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="20395-122">이를 정렬 하기 위해 몇 가지 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20395-122">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="20395-123">하나는 메서드에 다른 이름을 지정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="20395-123">One is to give the methods different names.</span></span> <span data-ttu-id="20395-124">앞의 예에서 스캐폴딩 메커니즘이 수행한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="20395-124">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="20395-125">그러나 이는 작은 문제를 야기합니다. ASP.NET은 URL의 세그먼트를 이름으로 작업 메서드에 매핑하고 메서드의 이름을 바꾸면 정상적으로 라우팅하여 해당 메서드를 찾을 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20395-125">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="20395-126">솔루션은 예제에서 확인한 것으로, `ActionName("Delete")` 특성을 `DeleteConfirmed` 메서드에 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="20395-126">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="20395-127">이렇게 하면 POST 요청에 대 한 */Delete/* 포함 된 URL에서 메서드를 찾을 수 있도록 라우팅 시스템에 대 한 매핑이 효과적으로 수행 됩니다 `DeleteConfirmed` .</span><span class="sxs-lookup"><span data-stu-id="20395-127">This effectively performs mapping for the routing system so that a URL that includes */Delete/* for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="20395-128">동일한 이름 및 서명을 가진 메서드의 문제를 방지 하는 또 다른 일반적인 방법은 사용 하지 않는 매개 변수를 포함 하도록 POST 메서드의 서명을 인위적으로 변경 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="20395-128">Another common way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="20395-129">예를 들어, 일부 개발자는 POST 메서드로 전달 되는 매개 변수 형식을 추가한 `FormCollection` 다음 매개 변수를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20395-129">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](examining-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="20395-130">요약</span><span class="sxs-lookup"><span data-stu-id="20395-130">Summary</span></span>

<span data-ttu-id="20395-131">이제 로컬 DB 데이터베이스에 데이터를 저장 하는 완전 한 ASP.NET MVC 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20395-131">You now have a complete ASP.NET MVC application that stores data in a local DB database.</span></span> <span data-ttu-id="20395-132">영화를 만들고, 읽고, 업데이트 하 고, 삭제 하 고, 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20395-132">You can create, read, update, delete, and search for movies.</span></span>

![](examining-the-details-and-delete-methods/_static/image2.png)

## <a name="next-steps"></a><span data-ttu-id="20395-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="20395-133">Next Steps</span></span>

<span data-ttu-id="20395-134">웹 응용 프로그램을 빌드 및 테스트 한 후에는 다른 사용자가 인터넷을 통해 사용할 수 있도록 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="20395-134">After you have built and tested a web application, the next step is to make it available to other people to use over the Internet.</span></span> <span data-ttu-id="20395-135">이렇게 하려면 웹 호스팅 공급자에 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20395-135">To do that, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="20395-136">Microsoft는 [무료 Azure 평가판 계정](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)에 최대 10 개의 웹 사이트를 제공 하는 무료 웹 호스팅을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="20395-136">Microsoft offers free web hosting for up to 10 web sites in a [free Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="20395-137">다음에 나오는 자습서에 따라 [멤버 자격, OAuth 및 SQL Database를 사용 하 여 Azure에 보안 ASP.NET MVC 앱을 배포 하는 것이](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)좋습니다.</span><span class="sxs-lookup"><span data-stu-id="20395-137">I suggest you next follow my tutorial [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="20395-138">뛰어난 자습서는 [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)Tom Dykstra의 중간 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="20395-138">An excellent tutorial is Tom Dykstra's intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="20395-139">[Stackoverflow](http://stackoverflow.com/help) 및 [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx) 은 질문을 할 수 있는 좋은 장소입니다.</span><span class="sxs-lookup"><span data-stu-id="20395-139">[Stackoverflow](http://stackoverflow.com/help) and the [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great places to ask questions.</span></span> <span data-ttu-id="20395-140">twitter에서 [저](https://twitter.com/RickAndMSFT)를 팔로우하시면 최신 자습서 업데이트를 받으실 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20395-140">Follow [me](https://twitter.com/RickAndMSFT) on twitter so you can get updates on my latest tutorials.</span></span>

<span data-ttu-id="20395-141">사용자 의견을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="20395-141">Feedback is welcome.</span></span>

<span data-ttu-id="20395-142">- [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="20395-142">— [Rick Anderson](https://blogs.msdn.com/rickAndy) twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT)</span></span>  
<span data-ttu-id="20395-143">- [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="20395-143">— [Scott Hanselman](http://www.hanselman.com/blog/) twitter: [@shanselman](https://twitter.com/shanselman)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="20395-144">이전</span><span class="sxs-lookup"><span data-stu-id="20395-144">Previous</span></span>](adding-validation.md)
