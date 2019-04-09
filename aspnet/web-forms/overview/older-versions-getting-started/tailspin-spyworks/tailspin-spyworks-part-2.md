---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: '2부: 데이터 계층에 액세스 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 2 부에서는 데이터 액세스 계층을 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 3fbc6fe4d94534a038a81532b3cd8ca30ddf9b11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59378392"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="538a1-104">2부: 데이터 액세스 계층</span><span class="sxs-lookup"><span data-stu-id="538a1-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="538a1-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="538a1-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="538a1-106">Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="538a1-107">해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="538a1-108">이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="538a1-109">2 부에서는 데이터 액세스 계층을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-109">Part 2 covers adding the data access layer.</span></span>


## <a id="_Toc260221668"></a>  <span data-ttu-id="538a1-110">데이터 액세스 계층 추가</span><span class="sxs-lookup"><span data-stu-id="538a1-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="538a1-111">전자 상거래 응용 프로그램은 두 개의 데이터베이스에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="538a1-112">고객 정보에 대 한 표준 ASP.NET 멤버 자격 데이터베이스를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="538a1-113">쇼핑 카트 및 제품 카탈로그에 대 한 SQL Express 데이터베이스를 다음과 같이 구현 됩니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="538a1-114">응용 프로그램의 앱에서 (Commerce.mdf) 데이터베이스를 만들었으므로\_데이터 폴더.NET Entity Framework를 사용 하 여 데이터 액세스 계층 만들기를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="538a1-115">라는 폴더를 만들겠습니다 "데이터\_액세스" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 항목 추가"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="538a1-116">"설치 된 템플릿" 항목을 선택한 후 "ADO.NET Entity Data Model" 입력 EDM\_Commerce.edmx 이름으로 "추가" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="538a1-117">"데이터베이스에서 생성"을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="538a1-118">저장 하 고 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="538a1-118">Save and build.</span></span>

<span data-ttu-id="538a1-119">이제 첫 번째 – 특집 제품 범주 메뉴를 추가할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="538a1-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="538a1-120">[이전](tailspin-spyworks-part-1.md)
> [다음](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="538a1-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
