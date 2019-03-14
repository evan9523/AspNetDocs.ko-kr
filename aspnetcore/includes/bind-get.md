---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051960"
---
> [!WARNING]
> <span data-ttu-id="5cbd6-101">보안상의 이유로 페이지 모델 속성에 `GET` 요청 데이터를 바인딩하기 위해 옵트인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbd6-101">For security reasons, you must opt in to binding `GET` request data to page model properties.</span></span> <span data-ttu-id="5cbd6-102">속성에 매핑하기 전에 사용자 입력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbd6-102">Verify user input before mapping it to properties.</span></span> <span data-ttu-id="5cbd6-103">쿼리 문자열이나 경로 값을 사용하는 시나리오를 해결할 때 `GET` 바인딩을 옵트인하면 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5cbd6-103">Opting in to `GET` binding is useful when addressing scenarios which rely on query string or route values.</span></span>
>
> <span data-ttu-id="5cbd6-104">`GET` 요청에 속성을 바인딩하려면 [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) 특성의 `SupportsGet` 속성을 `true`로 설정합니다. `[BindProperty(SupportsGet = true)]`</span><span class="sxs-lookup"><span data-stu-id="5cbd6-104">To bind a property on `GET` requests, set the [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) attribute's `SupportsGet` property to `true`: `[BindProperty(SupportsGet = true)]`</span></span>
