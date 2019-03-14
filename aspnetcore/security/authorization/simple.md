---
title: ASP.NET Core의 단순 권한 부여
author: rick-anderson
description: Authorize 특성을 사용하여 ASP.NET Core의 컨트롤러 및 액션에 대한 접근을 제한하는 방법을 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/simple
ms.openlocfilehash: 6409def0508b855d3d2a4a1f4d3a3d15bfe5dd32
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050660"
---
# <a name="simple-authorization-in-aspnet-core"></a><span data-ttu-id="4d8a0-103">ASP.NET Core의 단순 권한 부여</span><span class="sxs-lookup"><span data-stu-id="4d8a0-103">Simple authorization in ASP.NET Core</span></span>

<a name="security-authorization-simple"></a>

<span data-ttu-id="4d8a0-104">MVC의 권한 부여는 `AuthorizeAttribute` 특성과 이 특성의 다양한 매개 변수를 통해서 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d8a0-104">Authorization in MVC is controlled through the `AuthorizeAttribute` attribute and its various parameters.</span></span> <span data-ttu-id="4d8a0-105">가장 간단한 방법으로, 컨트롤러나 액션에 `AuthorizeAttribute` 특성을 적용하면 인증된 사용자만 해당 컨트롤러나 액션에 접근할 수 있게 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d8a0-105">At its simplest, applying the `AuthorizeAttribute` attribute to a controller or action limits access to the controller or action to any authenticated user.</span></span>

<span data-ttu-id="4d8a0-106">예를 들어 다음 코드는 인증된 사용자만 `AccountController`에 접근할 수 있게 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="4d8a0-106">For example, the following code limits access to the `AccountController` to any authenticated user.</span></span>

```csharp
[Authorize]
public class AccountController : Controller
{
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

<span data-ttu-id="4d8a0-107">컨트롤러가 아닌 액션에 권한 부여를 적용하고 싶다면 `AuthorizeAttribute` 특성을 액션 자체에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d8a0-107">If you want to apply authorization to an action rather than the controller, apply the `AuthorizeAttribute` attribute to the action itself:</span></span>

```csharp
public class AccountController : Controller
{
   public ActionResult Login()
   {
   }

   [Authorize]
   public ActionResult Logout()
   {
   }
}
```

<span data-ttu-id="4d8a0-108">이제 인증된 사용자만 `Logout` 함수에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d8a0-108">Now only authenticated users can access the `Logout` function.</span></span>

<span data-ttu-id="4d8a0-109">또는 `AllowAnonymous` 특성을 사용하여 인증되지 않은 사용자가 개별 액션에 접근할 수 있게 허용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d8a0-109">You can also use the `AllowAnonymous` attribute to allow access by non-authenticated users to individual actions.</span></span> <span data-ttu-id="4d8a0-110">예:</span><span class="sxs-lookup"><span data-stu-id="4d8a0-110">For example:</span></span>

```csharp
[Authorize]
public class AccountController : Controller
{
    [AllowAnonymous]
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

<span data-ttu-id="4d8a0-111">이렇게 특성을 적용하면 인증 여부 및 익명 상태와 관계없이 모든 사용자가 접근할 수 있는 `Login` 액션을 제외하고, `AccountController`에는 인증된 사용자만 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d8a0-111">This would allow only authenticated users to the `AccountController`, except for the `Login` action, which is accessible by everyone, regardless of their authenticated or unauthenticated / anonymous status.</span></span>

> [!WARNING]
> <span data-ttu-id="4d8a0-112">`[AllowAnonymous]`는 모든 권한 부여 문을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="4d8a0-112">`[AllowAnonymous]` bypasses all authorization statements.</span></span> <span data-ttu-id="4d8a0-113">`[AllowAnonymous]` 및 `[Authorize]` 특성을 결합하면 `[Authorize]` 특성은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d8a0-113">If you combine `[AllowAnonymous]` and any `[Authorize]` attribute, the `[Authorize]` attributes are ignored.</span></span> <span data-ttu-id="4d8a0-114">예를 들어 컨트롤러 수준에 `[AllowAnonymous]`를 적용하면 해당 컨트롤러의 (또는 그 내부의 모든 액션의) `[Authorize]` 특성은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d8a0-114">For example if you apply `[AllowAnonymous]` at the controller level, any `[Authorize]` attributes on the same controller (or on any action within it) is ignored.</span></span>
