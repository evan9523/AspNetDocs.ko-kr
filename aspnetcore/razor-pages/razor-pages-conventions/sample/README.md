---
ms.openlocfilehash: 68a77fffb9e2ed0eba05cceb2bff041f159501c6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046590"
---
# <a name="aspnet-core-model-providers-sample"></a><span data-ttu-id="8659c-101">ASP.NET Core 모델 공급자 샘플</span><span class="sxs-lookup"><span data-stu-id="8659c-101">ASP.NET Core Model Providers Sample</span></span>

<span data-ttu-id="8659c-102">이 샘플은 Razor 페이지 사용자 지정 경로 및 페이지 모델 공급자의 사용법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8659c-102">This sample illustrates use of Razor Pages custom route and page model providers.</span></span> <span data-ttu-id="8659c-103">이 샘플은 [Razor 페이지 경로 및 앱 규칙](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-convention-features) 항목에서 설명된 기능을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8659c-103">This sample demonstrates the features described in the [Razor Pages route and app conventions](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-convention-features) topic.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="8659c-104">이 샘플의 예제</span><span class="sxs-lookup"><span data-stu-id="8659c-104">Examples in this sample</span></span>

| <span data-ttu-id="8659c-105">시나리오</span><span class="sxs-lookup"><span data-stu-id="8659c-105">Scenario</span></span> | <span data-ttu-id="8659c-106">샘플 데모</span><span class="sxs-lookup"><span data-stu-id="8659c-106">Sample demo</span></span> |
| -------- | ----------- |
| [<span data-ttu-id="8659c-107">모델 규칙</span><span class="sxs-lookup"><span data-stu-id="8659c-107">Model conventions</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#model-conventions) | <span data-ttu-id="8659c-108">앱의 페이지에 경로 특성 및 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8659c-108">Add a route attribute and header to the app's pages.</span></span> |
| [<span data-ttu-id="8659c-109">AddPageRoute를 사용하여 페이지 경로 추가</span><span class="sxs-lookup"><span data-stu-id="8659c-109">Use AddPageRoute to add a page route</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#configure-a-page-route) | <span data-ttu-id="8659c-110">지정된 경로의 페이지를 지정된 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8659c-110">Adds the specified route to the page at the specified page.</span></span> |
| [<span data-ttu-id="8659c-111">페이지 모델 작업 규칙</span><span class="sxs-lookup"><span data-stu-id="8659c-111">Page model action conventions</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#page-model-action-conventions) | <span data-ttu-id="8659c-112">폴더의 페이지에 헤더를 추가하고, 단일 페이지에 헤더를 추가하고, 필터 팩토리를 구성하여 헤더를 앱의 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8659c-112">Add a header to pages in a folder, add a header to a single page, and configure a filter factory to add a header to the app's pages.</span></span> |
| [<span data-ttu-id="8659c-113">기본값 페이지 앱 모델 공급자 바꾸기</span><span class="sxs-lookup"><span data-stu-id="8659c-113">Replace the default page app model provider</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#replace-the-default-page-app-model-provider) | <span data-ttu-id="8659c-114">처리기 이름 지정 규칙을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8659c-114">Change the conventions for handler naming.</span></span> |
