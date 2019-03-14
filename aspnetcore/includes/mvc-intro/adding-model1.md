---
ms.openlocfilehash: 72e33ea44976963193d2560427fc418875be450e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038870"
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="6e731-101">ASP.NET Core MVC 앱에 모델 추가</span><span class="sxs-lookup"><span data-stu-id="6e731-101">Add a model to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="6e731-102">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="6e731-102">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="6e731-103">이 섹션에서는 데이터베이스에서 동영상을 관리하기 위한 일부 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6e731-103">In this section, you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="6e731-104">이러한 클래스는 **M**VC 앱의 "**M**odel" 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="6e731-104">These classes will be the "**M**odel" part of the **M**VC app.</span></span>

<span data-ttu-id="6e731-105">이러한 클래스를 EF Core([Entity Framework Core](/ef/core))와 함께 사용하여 데이터베이스 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6e731-105">You use these classes with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="6e731-106">EF Core는 작성해야 하는 데이터 액세스 코드를 간소화하는 ORM(개체-관계형 매핑) 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="6e731-106">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span> <span data-ttu-id="6e731-107">[EF Core는 많은 데이터베이스 엔진을 지원합니다](/ef/core/providers/).</span><span class="sxs-lookup"><span data-stu-id="6e731-107">[EF Core supports many database engines](/ef/core/providers/).</span></span>

<span data-ttu-id="6e731-108">직접 만드는 모델 클래스는 EF Core에 대한 종속성이 없으므로 POCO(Plain Old CLR Object) 클래스로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e731-108">The model classes you'll create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="6e731-109">이 클래스는 데이터베이스에 저장되는 데이터의 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6e731-109">They just define the properties of the data that will be stored in the database.</span></span>

<span data-ttu-id="6e731-110">이 자습서에서는 먼저 모델 클래스를 작성하면 EF Core가 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e731-110">In this tutorial you'll write the model classes first, and EF Core will create the database.</span></span> <span data-ttu-id="6e731-111">이 문서에서 설명하지 않는 대체 방법은 기존 데이터베이스에서 모델 클래스를 생성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6e731-111">An alternate approach not covered here is to generate model classes from an already-existing database.</span></span> <span data-ttu-id="6e731-112">이 방법에 대한 정보는 [ASP.NET Core - 기존 데이터베이스](/ef/core/get-started/aspnetcore/existing-db)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e731-112">For information about that approach, see [ASP.NET Core - Existing Database](/ef/core/get-started/aspnetcore/existing-db).</span></span>

## <a name="add-a-data-model-class"></a><span data-ttu-id="6e731-113">데이터 모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="6e731-113">Add a data model class</span></span>
