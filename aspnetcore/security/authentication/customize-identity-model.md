---
title: ASP.NET core에서 identity 모델 사용자 지정 합니다.
author: ajcvickers
description: 이 문서에서는 ASP.NET Core Id에 대 한 기본 Entity Framework Core 데이터 모델을 사용자 지정 하는 방법을 설명 합니다.
ms.author: avickers
ms.date: 09/24/2018
uid: security/authentication/customize_identity_model
ms.openlocfilehash: 90c867eeac0e64bfe77cc7a829d61e831a2fb8e1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024780"
---
# <a name="identity-model-customization-in-aspnet-core"></a><span data-ttu-id="982a8-103">ASP.NET core에서 identity 모델 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-103">Identity model customization in ASP.NET Core</span></span>

<span data-ttu-id="982a8-104">[Arthur Vickers](https://github.com/ajcvickers)</span><span class="sxs-lookup"><span data-stu-id="982a8-104">By [Arthur Vickers](https://github.com/ajcvickers)</span></span>

<span data-ttu-id="982a8-105">ASP.NET Core Id 관리 및 ASP.NET Core 앱에서 사용자를 저장 하기 위한 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-105">ASP.NET Core Identity provides a framework for managing and storing user accounts in ASP.NET Core apps.</span></span> <span data-ttu-id="982a8-106">Id가 프로젝트에 추가 하면 **개별 사용자 계정** 인증 메커니즘으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-106">Identity is added to your project when **Individual User Accounts** is selected as the authentication mechanism.</span></span> <span data-ttu-id="982a8-107">기본적으로 Id를 사용 하므로 Entity Framework (EF)를 사용 하 여 핵심 데이터 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-107">By default, Identity makes use of an Entity Framework (EF) Core data model.</span></span> <span data-ttu-id="982a8-108">이 문서에서는 Id 모델을 사용자 지정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-108">This article describes how to customize the Identity model.</span></span>

## <a name="identity-and-ef-core-migrations"></a><span data-ttu-id="982a8-109">Id 및 EF Core 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="982a8-109">Identity and EF Core Migrations</span></span>

<span data-ttu-id="982a8-110">모델을 검사 하기 전에 Id를 사용 하 여 작동 하는 방법을 이해 하는 데 유용 것 [EF Core 마이그레이션](/ef/core/managing-schemas/migrations/) 를 만들고 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-110">Before examining the model, it's useful to understand how Identity works with [EF Core Migrations](/ef/core/managing-schemas/migrations/) to create and update a database.</span></span> <span data-ttu-id="982a8-111">최상위 수준에 프로세스는.</span><span class="sxs-lookup"><span data-stu-id="982a8-111">At the top level, the process is:</span></span>

1. <span data-ttu-id="982a8-112">정의 또는 업데이트를 [코드에서 데이터 모델](/ef/core/modeling/)합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-112">Define or update a [data model in code](/ef/core/modeling/).</span></span>
1. <span data-ttu-id="982a8-113">이 모델 데이터베이스에 적용할 수 있는 변경 내용을 변환할 마이그레이션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-113">Add a Migration to translate this model into changes that can be applied to the database.</span></span>
1. <span data-ttu-id="982a8-114">마이그레이션이 올바르게 나타내는 의도 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-114">Check that the Migration correctly represents your intentions.</span></span>
1. <span data-ttu-id="982a8-115">모델을 사용 하 여 동기화 할 데이터베이스를 업데이트 하려면 마이그레이션을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-115">Apply the Migration to update the database to be in sync with the model.</span></span>
1. <span data-ttu-id="982a8-116">추가 모델을 구체화 하 고 데이터베이스 동기화 상태를 유지 하는 1-4 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-116">Repeat steps 1 through 4 to further refine the model and keep the database in sync.</span></span>

<span data-ttu-id="982a8-117">다음 방법 중 하나를 사용 하 여 추가 하 고 마이그레이션을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-117">Use one of the following approaches to add and apply Migrations:</span></span>

* <span data-ttu-id="982a8-118">합니다 **패키지 관리자 콘솔** Visual Studio를 사용 하는 경우 (PMC) 창.</span><span class="sxs-lookup"><span data-stu-id="982a8-118">The **Package Manager Console** (PMC) window if using Visual Studio.</span></span> <span data-ttu-id="982a8-119">자세한 내용은 [EF Core PMC 도구](/ef/core/miscellaneous/cli/powershell)합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-119">For more information, see [EF Core PMC tools](/ef/core/miscellaneous/cli/powershell).</span></span>
* <span data-ttu-id="982a8-120">.NET Core CLI 명령줄을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="982a8-120">The .NET Core CLI if using the command line.</span></span> <span data-ttu-id="982a8-121">자세한 내용은 [EF Core.NET 명령줄 도구](/ef/core/miscellaneous/cli/dotnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-121">For more information, see [EF Core .NET command line tools](/ef/core/miscellaneous/cli/dotnet).</span></span>
* <span data-ttu-id="982a8-122">클릭 하는 **마이그레이션 적용** 앱이 실행 되 면 오류 페이지에는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-122">Clicking the **Apply Migrations** button on the error page when the app is run.</span></span>

<span data-ttu-id="982a8-123">ASP.NET Core 개발 시 오류 페이지 처리기를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-123">ASP.NET Core has a development-time error page handler.</span></span> <span data-ttu-id="982a8-124">처리기는 앱이 실행 되는 경우 마이그레이션을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-124">The handler can apply migrations when the app is run.</span></span> <span data-ttu-id="982a8-125">프로덕션 앱에 대 한 것이 마이그레이션이에서 SQL 스크립트를 생성 하 고 제어 되는 앱 및 데이터베이스 배포의 일환으로 데이터베이스 변경 내용을 배포에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-125">For production apps, it's often more appropriate to generate SQL scripts from the migrations and deploy database changes as part of a controlled app and database deployment.</span></span>

<span data-ttu-id="982a8-126">Id를 사용 하는 새 앱을 만든 경우 위의 1-2 단계 이미 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-126">When a new app using Identity is created, steps 1 and 2 above have already been completed.</span></span> <span data-ttu-id="982a8-127">즉, 초기 데이터 모델이 이미 있는 및 초기 마이그레이션 프로젝트에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-127">That is, the initial data model already exists, and the initial migration has been added to the project.</span></span> <span data-ttu-id="982a8-128">여전히 초기 마이그레이션을 데이터베이스에 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-128">The initial migration still needs to be applied to the database.</span></span> <span data-ttu-id="982a8-129">다음 방법 중 하나를 통해 초기 마이그레이션을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-129">The initial migration can be applied via one of the following approaches:</span></span>

* <span data-ttu-id="982a8-130">실행 `Update-Database` PMC에서.</span><span class="sxs-lookup"><span data-stu-id="982a8-130">Run `Update-Database` in PMC.</span></span>
* <span data-ttu-id="982a8-131">실행 `dotnet ef database update` 명령 셸에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-131">Run `dotnet ef database update` in a command shell.</span></span>
* <span data-ttu-id="982a8-132">클릭 합니다 **마이그레이션 적용** 앱이 실행 되 면 오류 페이지에는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-132">Click the **Apply Migrations** button on the error page when the app is run.</span></span>

<span data-ttu-id="982a8-133">모델에 변경 내용이 이전 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-133">Repeat the preceding steps as changes are made to the model.</span></span>

## <a name="the-identity-model"></a><span data-ttu-id="982a8-134">Id 모델</span><span class="sxs-lookup"><span data-stu-id="982a8-134">The Identity model</span></span>

### <a name="entity-types"></a><span data-ttu-id="982a8-135">엔터티 형식</span><span class="sxs-lookup"><span data-stu-id="982a8-135">Entity types</span></span>

<span data-ttu-id="982a8-136">Id 모델 엔터티 형식은 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-136">The Identity model consists of the following entity types.</span></span>

|<span data-ttu-id="982a8-137">엔터티 형식</span><span class="sxs-lookup"><span data-stu-id="982a8-137">Entity type</span></span>|<span data-ttu-id="982a8-138">설명</span><span class="sxs-lookup"><span data-stu-id="982a8-138">Description</span></span>                                                  |
|-----------|-------------------------------------------------------------|
|`User`     |<span data-ttu-id="982a8-139">사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-139">Represents the user.</span></span>                                         |
|`Role`     |<span data-ttu-id="982a8-140">역할을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-140">Represents a role.</span></span>                                           |
|`UserClaim`|<span data-ttu-id="982a8-141">사용자가 소유 하는 클레임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-141">Represents a claim that a user possesses.</span></span>                    |
|`UserToken`|<span data-ttu-id="982a8-142">사용자에 대 한 인증 토큰을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-142">Represents an authentication token for a user.</span></span>               |
|`UserLogin`|<span data-ttu-id="982a8-143">로그인을 사용 하 여 사용자를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-143">Associates a user with a login.</span></span>                              |
|`RoleClaim`|<span data-ttu-id="982a8-144">역할 내에서 모든 사용자에 게 부여 되는 클레임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-144">Represents a claim that's granted to all users within a role.</span></span>|
|`UserRole` |<span data-ttu-id="982a8-145">사용자 및 역할을 연결 하는 조인 엔터티를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-145">A join entity that associates users and roles.</span></span>               |

### <a name="entity-type-relationships"></a><span data-ttu-id="982a8-146">엔터티 형식 관계</span><span class="sxs-lookup"><span data-stu-id="982a8-146">Entity type relationships</span></span>

<span data-ttu-id="982a8-147">[엔터티 형식](#entity-types) 다음과 같은 방법으로 서로 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-147">The [entity types](#entity-types) are related to each other in the following ways:</span></span>

* <span data-ttu-id="982a8-148">각 `User` 많을 수 `UserClaims`입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-148">Each `User` can have many `UserClaims`.</span></span>
* <span data-ttu-id="982a8-149">각 `User` 많을 수 `UserLogins`입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-149">Each `User` can have many `UserLogins`.</span></span>
* <span data-ttu-id="982a8-150">각 `User` 많을 수 `UserTokens`입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-150">Each `User` can have many `UserTokens`.</span></span>
* <span data-ttu-id="982a8-151">각 `Role` 연결 된 여러 있습니다 `RoleClaims`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-151">Each `Role` can have many associated `RoleClaims`.</span></span>
* <span data-ttu-id="982a8-152">각 `User` 관련 된 많은 가질 수 있습니다 `Roles`, 및 각 `Role` 다를 사용 하 여 연결할 수 있습니다 `Users`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-152">Each `User` can have many associated `Roles`, and each `Role` can be associated with many `Users`.</span></span> <span data-ttu-id="982a8-153">이 데이터베이스의 조인 테이블이 필요는 다 대 다 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-153">This is a many-to-many relationship that requires a join table in the database.</span></span> <span data-ttu-id="982a8-154">조인 테이블은 표현 된 `UserRole` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="982a8-154">The join table is represented by the `UserRole` entity.</span></span>

### <a name="default-model-configuration"></a><span data-ttu-id="982a8-155">기본 모델 구성</span><span class="sxs-lookup"><span data-stu-id="982a8-155">Default model configuration</span></span>

<span data-ttu-id="982a8-156">대부분 identity 정의 *컨텍스트 클래스* 에서 상속 되는 <xref:Microsoft.EntityFrameworkCore.DbContext> 구성 하 고 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-156">Identity defines many *context classes* that inherit from <xref:Microsoft.EntityFrameworkCore.DbContext> to configure and use the model.</span></span> <span data-ttu-id="982a8-157">이 구성을 수행 해야를 사용 하는 [EF Core Code First Fluent API](/ef/core/modeling/) 에 <xref:Microsoft.EntityFrameworkCore.DbContext.OnModelCreating*> 컨텍스트 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="982a8-157">This configuration is done using the [EF Core Code First Fluent API](/ef/core/modeling/) in the <xref:Microsoft.EntityFrameworkCore.DbContext.OnModelCreating*> method of the context class.</span></span> <span data-ttu-id="982a8-158">기본 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-158">The default configuration is:</span></span>

```csharp
builder.Entity<TUser>(b =>
{
    // Primary key
    b.HasKey(u => u.Id);

    // Indexes for "normalized" username and email, to allow efficient lookups
    b.HasIndex(u => u.NormalizedUserName).HasName("UserNameIndex").IsUnique();
    b.HasIndex(u => u.NormalizedEmail).HasName("EmailIndex");

    // Maps to the AspNetUsers table
    b.ToTable("AspNetUsers");

    // A concurrency token for use with the optimistic concurrency checking
    b.Property(u => u.ConcurrencyStamp).IsConcurrencyToken();

    // Limit the size of columns to use efficient database types
    b.Property(u => u.UserName).HasMaxLength(256);
    b.Property(u => u.NormalizedUserName).HasMaxLength(256);
    b.Property(u => u.Email).HasMaxLength(256);
    b.Property(u => u.NormalizedEmail).HasMaxLength(256);

    // The relationships between User and other entity types
    // Note that these relationships are configured with no navigation properties

    // Each User can have many UserClaims
    b.HasMany<TUserClaim>().WithOne().HasForeignKey(uc => uc.UserId).IsRequired();

    // Each User can have many UserLogins
    b.HasMany<TUserLogin>().WithOne().HasForeignKey(ul => ul.UserId).IsRequired();

    // Each User can have many UserTokens
    b.HasMany<TUserToken>().WithOne().HasForeignKey(ut => ut.UserId).IsRequired();

    // Each User can have many entries in the UserRole join table
    b.HasMany<TUserRole>().WithOne().HasForeignKey(ur => ur.UserId).IsRequired();
});

builder.Entity<TUserClaim>(b =>
{
    // Primary key
    b.HasKey(uc => uc.Id);

    // Maps to the AspNetUserClaims table
    b.ToTable("AspNetUserClaims");
});

builder.Entity<TUserLogin>(b =>
{
    // Composite primary key consisting of the LoginProvider and the key to use
    // with that provider
    b.HasKey(l => new { l.LoginProvider, l.ProviderKey });

    // Limit the size of the composite key columns due to common DB restrictions
    b.Property(l => l.LoginProvider).HasMaxLength(128);
    b.Property(l => l.ProviderKey).HasMaxLength(128);

    // Maps to the AspNetUserLogins table
    b.ToTable("AspNetUserLogins");
});

builder.Entity<TUserToken>(b =>
{
    // Composite primary key consisting of the UserId, LoginProvider and Name
    b.HasKey(t => new { t.UserId, t.LoginProvider, t.Name });

    // Limit the size of the composite key columns due to common DB restrictions
    b.Property(t => t.LoginProvider).HasMaxLength(maxKeyLength);
    b.Property(t => t.Name).HasMaxLength(maxKeyLength);

    // Maps to the AspNetUserTokens table
    b.ToTable("AspNetUserTokens");
});

builder.Entity<TRole>(b =>
{
    // Primary key
    b.HasKey(r => r.Id);

    // Index for "normalized" role name to allow efficient lookups
    b.HasIndex(r => r.NormalizedName).HasName("RoleNameIndex").IsUnique();

    // Maps to the AspNetRoles table
    b.ToTable("AspNetRoles");

    // A concurrency token for use with the optimistic concurrency checking
    b.Property(r => r.ConcurrencyStamp).IsConcurrencyToken();

    // Limit the size of columns to use efficient database types
    b.Property(u => u.Name).HasMaxLength(256);
    b.Property(u => u.NormalizedName).HasMaxLength(256);

    // The relationships between Role and other entity types
    // Note that these relationships are configured with no navigation properties

    // Each Role can have many entries in the UserRole join table
    b.HasMany<TUserRole>().WithOne().HasForeignKey(ur => ur.RoleId).IsRequired();

    // Each Role can have many associated RoleClaims
    b.HasMany<TRoleClaim>().WithOne().HasForeignKey(rc => rc.RoleId).IsRequired();
});

builder.Entity<TRoleClaim>(b =>
{
    // Primary key
    b.HasKey(rc => rc.Id);

    // Maps to the AspNetRoleClaims table
    b.ToTable("AspNetRoleClaims");
});

builder.Entity<TUserRole>(b =>
{
    // Primary key
    b.HasKey(r => new { r.UserId, r.RoleId });

    // Maps to the AspNetUserRoles table
    b.ToTable("AspNetUserRoles");
});
```

### <a name="model-generic-types"></a><span data-ttu-id="982a8-159">모델 제네릭 형식</span><span class="sxs-lookup"><span data-stu-id="982a8-159">Model generic types</span></span>

<span data-ttu-id="982a8-160">기본값을 정의 하는 identity [공용 언어 런타임](/dotnet/standard/glossary#clr) 위에 나열 된 각 엔터티 형식에 대 한 (CLR) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-160">Identity defines default [Common Language Runtime](/dotnet/standard/glossary#clr) (CLR) types for each of the entity types listed above.</span></span> <span data-ttu-id="982a8-161">이러한 형식은 모두 사용 하 여 접두사가 *Identity*:</span><span class="sxs-lookup"><span data-stu-id="982a8-161">These types are all prefixed with *Identity*:</span></span>

* `IdentityUser`
* `IdentityRole`
* `IdentityUserClaim`
* `IdentityUserToken`
* `IdentityUserLogin`
* `IdentityRoleClaim`
* `IdentityUserRole`

<span data-ttu-id="982a8-162">직접 이러한 형식을 사용 하는 대신 앱 자체의 형식에 대 한 형식은 기본 클래스로 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-162">Rather than using these types directly, the types can be used as base classes for the app's own types.</span></span> <span data-ttu-id="982a8-163">`DbContext` Id로 정의 된 클래스는 일반, 같은 다른 CLR 형식은 하나 이상의 모델의 엔터티 형식에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-163">The `DbContext` classes defined by Identity are generic, such that different CLR types can be used for one or more of the entity types in the model.</span></span> <span data-ttu-id="982a8-164">이러한 제네릭 형식을 허용할는 `User` 기본 키 (PK) 데이터 형식을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-164">These generic types also allow the `User` primary key (PK) data type to be changed.</span></span>

<span data-ttu-id="982a8-165">Id를 사용 하 여 역할에 대 한 지원을 사용 하는 경우는 <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext> 클래스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-165">When using Identity with support for roles, an <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext> class should be used.</span></span> <span data-ttu-id="982a8-166">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="982a8-166">For example:</span></span>

```csharp
// Uses all the built-in Identity types
// Uses `string` as the key type
public class IdentityDbContext
    : IdentityDbContext<IdentityUser, IdentityRole, string>
{
}

// Uses the built-in Identity types except with a custom User type
// Uses `string` as the key type
public class IdentityDbContext<TUser>
    : IdentityDbContext<TUser, IdentityRole, string>
        where TUser : IdentityUser
{
}

// Uses the built-in Identity types except with custom User and Role types
// The key type is defined by TKey
public class IdentityDbContext<TUser, TRole, TKey> : IdentityDbContext<
    TUser, TRole, TKey, IdentityUserClaim<TKey>, IdentityUserRole<TKey>,
    IdentityUserLogin<TKey>, IdentityRoleClaim<TKey>, IdentityUserToken<TKey>>
        where TUser : IdentityUser<TKey>
        where TRole : IdentityRole<TKey>
        where TKey : IEquatable<TKey>
{
}

// No built-in Identity types are used; all are specified by generic arguments
// The key type is defined by TKey
public abstract class IdentityDbContext<
    TUser, TRole, TKey, TUserClaim, TUserRole, TUserLogin, TRoleClaim, TUserToken>
    : IdentityUserContext<TUser, TKey, TUserClaim, TUserLogin, TUserToken>
         where TUser : IdentityUser<TKey>
         where TRole : IdentityRole<TKey>
         where TKey : IEquatable<TKey>
         where TUserClaim : IdentityUserClaim<TKey>
         where TUserRole : IdentityUserRole<TKey>
         where TUserLogin : IdentityUserLogin<TKey>
         where TRoleClaim : IdentityRoleClaim<TKey>
         where TUserToken : IdentityUserToken<TKey>
```

<span data-ttu-id="982a8-167">것도 가능 역할 (클레임만),이 경우 Id를 사용 하는 <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUserContext`1> 클래스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-167">It's also possible to use Identity without roles (only claims), in which case an <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUserContext`1> class should be used:</span></span>

```csharp
// Uses the built-in non-role Identity types except with a custom User type
// Uses `string` as the key type
public class IdentityUserContext<TUser>
    : IdentityUserContext<TUser, string>
        where TUser : IdentityUser
{
}

// Uses the built-in non-role Identity types except with a custom User type
// The key type is defined by TKey
public class IdentityUserContext<TUser, TKey> : IdentityUserContext<
    TUser, TKey, IdentityUserClaim<TKey>, IdentityUserLogin<TKey>,
    IdentityUserToken<TKey>>
        where TUser : IdentityUser<TKey>
        where TKey : IEquatable<TKey>
{
}

// No built-in Identity types are used; all are specified by generic arguments, with no roles
// The key type is defined by TKey
public abstract class IdentityUserContext<
    TUser, TKey, TUserClaim, TUserLogin, TUserToken> : DbContext
        where TUser : IdentityUser<TKey>
        where TKey : IEquatable<TKey>
        where TUserClaim : IdentityUserClaim<TKey>
        where TUserLogin : IdentityUserLogin<TKey>
        where TUserToken : IdentityUserToken<TKey>
{
}
```

## <a name="customize-the-model"></a><span data-ttu-id="982a8-168">모델을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="982a8-168">Customize the model</span></span>

<span data-ttu-id="982a8-169">모델 사용자 지정에 대 한 시작 지점을 적절 한 상황에 맞는 형식에서 파생 시키는 경우</span><span class="sxs-lookup"><span data-stu-id="982a8-169">The starting point for model customization is to derive from the appropriate context type.</span></span> <span data-ttu-id="982a8-170">참조 된 [제네릭 형식을 모델링](#model-generic-types) 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-170">See the [Model generic types](#model-generic-types) section.</span></span> <span data-ttu-id="982a8-171">이 컨텍스트 형식 이라고 관례적으로 `ApplicationDbContext` ASP.NET Core 템플릿에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-171">This context type is customarily called `ApplicationDbContext` and is created by the ASP.NET Core templates.</span></span>

<span data-ttu-id="982a8-172">컨텍스트는 두 가지 방법으로 모델을 구성 하려면 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-172">The context is used to configure the model in two ways:</span></span>

* <span data-ttu-id="982a8-173">엔터티 및 제네릭 형식 매개 변수를 형식 키를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-173">Supplying entity and key types for the generic type parameters.</span></span>
* <span data-ttu-id="982a8-174">재정의 `OnModelCreating` 이러한 형식의 매핑을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-174">Overriding `OnModelCreating` to modify the mapping of these types.</span></span>

<span data-ttu-id="982a8-175">재정의 하는 경우 `OnModelCreating`, `base.OnModelCreating` 먼저 호출 되어야; 재정의 구성은 다음 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-175">When overriding `OnModelCreating`, `base.OnModelCreating` should be called first; the overriding configuration should be called next.</span></span> <span data-ttu-id="982a8-176">EF Core에는 일반적으로 마지막으로 한 업데이트 정책 구성에 대 한에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-176">EF Core generally has a last-one-wins policy for configuration.</span></span> <span data-ttu-id="982a8-177">예를 들어 경우는 `ToTable` 엔터티 형식에 대 한 메서드는 먼저 하나의 테이블 이름 및 다시 나중에 다른 테이블 이름으로 테이블 이름이 두 번째 호출에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-177">For example, if the `ToTable` method for an entity type is called first with one table name and then again later with a different table name, the table name in the second call is used.</span></span>

### <a name="custom-user-data"></a><span data-ttu-id="982a8-178">사용자 지정 사용자 데이터</span><span class="sxs-lookup"><span data-stu-id="982a8-178">Custom user data</span></span>

<span data-ttu-id="982a8-179">[사용자 지정 사용자 데이터](xref:security/authentication/add-user-data) 에서 상속 하 여 사용할 `IdentityUser`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-179">[Custom user data](xref:security/authentication/add-user-data) is supported by inheriting from `IdentityUser`.</span></span> <span data-ttu-id="982a8-180">이 형식의 이름에 `ApplicationUser`:</span><span class="sxs-lookup"><span data-stu-id="982a8-180">It's customary to name this type `ApplicationUser`:</span></span>


```csharp
public class ApplicationUser : IdentityUser
{
    public string CustomTag { get; set; }
}
```

<span data-ttu-id="982a8-181">사용 된 `ApplicationUser` 컨텍스트에 대 한 제네릭 인수 형식:</span><span class="sxs-lookup"><span data-stu-id="982a8-181">Use the `ApplicationUser` type as a generic argument for the context:</span></span>

```csharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }
}
```

<span data-ttu-id="982a8-182">재정의 하지 않아도 됩니다 `OnModelCreating` 에 `ApplicationDbContext` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-182">There's no need to override `OnModelCreating` in the `ApplicationDbContext` class.</span></span> <span data-ttu-id="982a8-183">EF Core 매핑하는 `CustomTag` 규칙에 따라 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-183">EF Core maps the `CustomTag` property by convention.</span></span> <span data-ttu-id="982a8-184">데이터베이스를 새 업데이트 해야 하는 반면 `CustomTag` 열입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-184">However, the database needs to be updated to create a new `CustomTag` column.</span></span> <span data-ttu-id="982a8-185">열을 만들려면 마이그레이션을 추가 하 고 다음에 설명 된 대로 데이터베이스를 업데이트할 [Id 및 EF Core 마이그레이션](#identity-and-ef-core-migrations)합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-185">To create the column, add a migration, and then update the database as described in [Identity and EF Core Migrations](#identity-and-ef-core-migrations).</span></span>

<span data-ttu-id="982a8-186">업데이트 `Startup.ConfigureServices` 를 사용 하도록 `ApplicationUser` 클래스:</span><span class="sxs-lookup"><span data-stu-id="982a8-186">Update `Startup.ConfigureServices` to use the new `ApplicationUser` class:</span></span>

::: moniker range=">= aspnetcore-2.1"

```csharp
services.AddDefaultIdentity<ApplicationUser>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultUI();
```

<span data-ttu-id="982a8-187">ASP.NET Core 2.1 이상 버전에서는 Identity Razor 클래스 라이브러리로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-187">In ASP.NET Core 2.1 or later, Identity is provided as a Razor Class Library.</span></span> <span data-ttu-id="982a8-188">자세한 내용은 <xref:security/authentication/scaffold-identity>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="982a8-188">For more information, see <xref:security/authentication/scaffold-identity>.</span></span> <span data-ttu-id="982a8-189">앞의 코드 호출을 해야 하는 결과적으로 <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-189">Consequently, the preceding code requires a call to <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span></span> <span data-ttu-id="982a8-190">Identity 스 캐 폴더는 프로젝트에 파일을 식별을 추가 하려면 사용 된 경우 호출을 제거 `AddDefaultUI`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-190">If the Identity scaffolder was used to add Identity files to the project, remove the call to `AddDefaultUI`.</span></span> <span data-ttu-id="982a8-191">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="982a8-191">For more information, see:</span></span>

* [<span data-ttu-id="982a8-192">스캐폴드 ID</span><span class="sxs-lookup"><span data-stu-id="982a8-192">Scaffold Identity</span></span>](xref:security/authentication/scaffold-identity)
* [<span data-ttu-id="982a8-193">추가, 다운로드 및 Id에 사용자 지정 사용자 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-193">Add, download, and delete custom user data to Identity</span></span>](xref:security/authentication/add-user-data)

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();
```

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext, Guid>()
        .AddDefaultTokenProviders();
```

::: moniker-end

### <a name="change-the-primary-key-type"></a><span data-ttu-id="982a8-194">기본 키 형식 변경</span><span class="sxs-lookup"><span data-stu-id="982a8-194">Change the primary key type</span></span>

<span data-ttu-id="982a8-195">데이터베이스가 만들어진 후 PK 열의 데이터 형식에 대 한 변경 많은 데이터베이스 시스템에서 문제가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-195">A change to the PK column's data type after the database has been created is problematic on many database systems.</span></span> <span data-ttu-id="982a8-196">PK를 일반적으로 변경 삭제 하 고 테이블을 다시 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-196">Changing the PK typically involves dropping and re-creating the table.</span></span> <span data-ttu-id="982a8-197">따라서, 키 유형 데이터베이스를 만들 때 초기 마이그레이션에 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-197">Therefore, key types should be specified in the initial migration when the database is created.</span></span>

<span data-ttu-id="982a8-198">PK 유형을 변경 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-198">Follow these steps to change the PK type:</span></span>

1. <span data-ttu-id="982a8-199">데이터베이스를 만든 경우 PK 변경 하기 전에 실행 `Drop-Database` (PMC) 또는 `dotnet ef database drop` (.NET Core CLI)를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-199">If the database was created before the PK change, run `Drop-Database` (PMC) or `dotnet ef database drop` (.NET Core CLI) to delete it.</span></span>
2. <span data-ttu-id="982a8-200">데이터베이스의 삭제를 확인 한 후 제거 된 초기 마이그레이션을 `Remove-Migration` (PMC) 또는 `dotnet ef migrations remove` (.NET Core CLI).</span><span class="sxs-lookup"><span data-stu-id="982a8-200">After confirming deletion of the database, remove the initial migration with `Remove-Migration` (PMC) or `dotnet ef migrations remove` (.NET Core CLI).</span></span>
3. <span data-ttu-id="982a8-201">업데이트를 `ApplicationDbContext` 에서 파생 된 클래스 <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext`3>합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-201">Update the `ApplicationDbContext` class to derive from <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityDbContext`3>.</span></span> <span data-ttu-id="982a8-202">새 키 유형을 지정 `TKey`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-202">Specify the new key type for `TKey`.</span></span> <span data-ttu-id="982a8-203">예를 들어 사용 하는 `Guid` 키 유형:</span><span class="sxs-lookup"><span data-stu-id="982a8-203">For example, to use a `Guid` key type:</span></span>

    ```csharp
    public class ApplicationDbContext
        : IdentityDbContext<IdentityUser<Guid>, IdentityRole<Guid>, Guid>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }
    }
    ```

    ::: moniker range=">= aspnetcore-2.0"

    <span data-ttu-id="982a8-204">위의 코드에서 제네릭 클래스 <xref:Microsoft.AspNetCore.Identity.IdentityUser`1> 고 <xref:Microsoft.AspNetCore.Identity.IdentityRole`1> 새 키 유형을 사용 하려면 반드시 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-204">In the preceding code, the generic classes <xref:Microsoft.AspNetCore.Identity.IdentityUser`1> and <xref:Microsoft.AspNetCore.Identity.IdentityRole`1> must be specified to use the new key type.</span></span>

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    <span data-ttu-id="982a8-205">위의 코드에서 제네릭 클래스 <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUser`1> 고 <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityRole`1> 새 키 유형을 사용 하려면 반드시 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-205">In the preceding code, the generic classes <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityUser`1> and <xref:Microsoft.AspNetCore.Identity.EntityFrameworkCore.IdentityRole`1> must be specified to use the new key type.</span></span>

    ::: moniker-end

    <span data-ttu-id="982a8-206">`Startup.ConfigureServices` 일반 사용자를 사용 하도록 업데이트 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-206">`Startup.ConfigureServices` must be updated to use the generic user:</span></span>

    ::: moniker range=">= aspnetcore-2.1"

    ```csharp
    services.AddDefaultIdentity<IdentityUser<Guid>>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();
    ```

    ::: moniker-end

    ::: moniker range="= aspnetcore-2.0"

    ```csharp
    services.AddIdentity<IdentityUser<Guid>, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();
    ```

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    ```csharp
    services.AddIdentity<IdentityUser<Guid>, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext, Guid>()
            .AddDefaultTokenProviders();
    ```

    ::: moniker-end

4. <span data-ttu-id="982a8-207">사용자 지정 하는 경우 `ApplicationUser` 클래스를 사용 하는, 클래스에서 상속 하도록 업데이트 `IdentityUser`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-207">If a custom `ApplicationUser` class is being used, update the class to inherit from `IdentityUser`.</span></span> <span data-ttu-id="982a8-208">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="982a8-208">For example:</span></span>

    ::: moniker range="<= aspnetcore-1.1"

    [!code-csharp[](customize-identity-model/samples/1.1/MvcSampleApp/Models/ApplicationUser.cs?name=snippet_ApplicationUser&highlight=4)]

    ::: moniker-end

    ::: moniker range=">= aspnetcore-2.0"

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Data/ApplicationUser.cs?name=snippet_ApplicationUser&highlight=4)]

    ::: moniker-end

    <span data-ttu-id="982a8-209">업데이트 `ApplicationDbContext` 사용자 지정을 참조 하려면 `ApplicationUser` 클래스:</span><span class="sxs-lookup"><span data-stu-id="982a8-209">Update `ApplicationDbContext` to reference the custom `ApplicationUser` class:</span></span>

    ```csharp
    public class ApplicationDbContext
        : IdentityDbContext<ApplicationUser, IdentityRole<Guid>, Guid>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }
    }
    ```

    <span data-ttu-id="982a8-210">사용자 지정 데이터베이스 컨텍스트 클래스의 Id 서비스를 추가 하는 경우 등록 `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="982a8-210">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    ::: moniker range=">= aspnetcore-2.1"

    ```csharp
    services.AddDefaultIdentity<ApplicationUser>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultUI()
            .AddDefaultTokenProviders();
    ```

    <span data-ttu-id="982a8-211">기본 키의 데이터 형식을 분석에서 유추 되는 <xref:Microsoft.EntityFrameworkCore.DbContext> 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-211">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    <span data-ttu-id="982a8-212">ASP.NET Core 2.1 이상 버전에서는 Identity Razor 클래스 라이브러리로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-212">In ASP.NET Core 2.1 or later, Identity is provided as a Razor Class Library.</span></span> <span data-ttu-id="982a8-213">자세한 내용은 <xref:security/authentication/scaffold-identity>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="982a8-213">For more information, see <xref:security/authentication/scaffold-identity>.</span></span> <span data-ttu-id="982a8-214">앞의 코드 호출을 해야 하는 결과적으로 <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-214">Consequently, the preceding code requires a call to <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span></span> <span data-ttu-id="982a8-215">Identity 스 캐 폴더는 프로젝트에 파일을 식별을 추가 하려면 사용 된 경우 호출을 제거 `AddDefaultUI`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-215">If the Identity scaffolder was used to add Identity files to the project, remove the call to `AddDefaultUI`.</span></span>

    ::: moniker-end

    ::: moniker range="= aspnetcore-2.0"

    ```csharp
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>()
            .AddDefaultTokenProviders();
    ```

    <span data-ttu-id="982a8-216">기본 키의 데이터 형식을 분석에서 유추 되는 <xref:Microsoft.EntityFrameworkCore.DbContext> 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-216">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    ```csharp
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext, Guid>()
            .AddDefaultTokenProviders();
    ```

    <span data-ttu-id="982a8-217">합니다 <xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> 메서드에서 `TKey` 기본 키의 데이터 형식을 나타내는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-217">The <xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> method accepts a `TKey` type indicating the primary key's data type.</span></span>

    ::: moniker-end

5. <span data-ttu-id="982a8-218">사용자 지정 하는 경우 `ApplicationRole` 클래스를 사용 하는, 클래스에서 상속 하도록 업데이트 `IdentityRole<TKey>`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-218">If a custom `ApplicationRole` class is being used, update the class to inherit from `IdentityRole<TKey>`.</span></span> <span data-ttu-id="982a8-219">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="982a8-219">For example:</span></span>

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Data/ApplicationRole.cs?name=snippet_ApplicationRole&highlight=4)]

    <span data-ttu-id="982a8-220">업데이트 `ApplicationDbContext` 사용자 지정을 참조 하려면 `ApplicationRole` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-220">Update `ApplicationDbContext` to reference the custom `ApplicationRole` class.</span></span> <span data-ttu-id="982a8-221">다음 클래스는 사용자 지정을 참조 하는 예를 들어 `ApplicationUser` 및 사용자 지정 `ApplicationRole`:</span><span class="sxs-lookup"><span data-stu-id="982a8-221">For example, the following class references a custom `ApplicationUser` and a custom `ApplicationRole`:</span></span>

    ::: moniker range=">= aspnetcore-2.1"

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Data/ApplicationDbContext.cs?name=snippet_ApplicationDbContext&highlight=5-6)]

    <span data-ttu-id="982a8-222">사용자 지정 데이터베이스 컨텍스트 클래스의 Id 서비스를 추가 하는 경우 등록 `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="982a8-222">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    [!code-csharp[](customize-identity-model/samples/2.1/RazorPagesSampleApp/Startup.cs?name=snippet_ConfigureServices&highlight=13-16)]

    <span data-ttu-id="982a8-223">기본 키의 데이터 형식을 분석에서 유추 되는 <xref:Microsoft.EntityFrameworkCore.DbContext> 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-223">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    <span data-ttu-id="982a8-224">ASP.NET Core 2.1 이상 버전에서는 Identity Razor 클래스 라이브러리로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-224">In ASP.NET Core 2.1 or later, Identity is provided as a Razor Class Library.</span></span> <span data-ttu-id="982a8-225">자세한 내용은 <xref:security/authentication/scaffold-identity>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="982a8-225">For more information, see <xref:security/authentication/scaffold-identity>.</span></span> <span data-ttu-id="982a8-226">앞의 코드 호출을 해야 하는 결과적으로 <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-226">Consequently, the preceding code requires a call to <xref:Microsoft.AspNetCore.Identity.IdentityBuilderUIExtensions.AddDefaultUI*>.</span></span> <span data-ttu-id="982a8-227">Identity 스 캐 폴더는 프로젝트에 파일을 식별을 추가 하려면 사용 된 경우 호출을 제거 `AddDefaultUI`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-227">If the Identity scaffolder was used to add Identity files to the project, remove the call to `AddDefaultUI`.</span></span>

    ::: moniker-end

    ::: moniker range="= aspnetcore-2.0"

    [!code-csharp[](customize-identity-model/samples/2.0/RazorPagesSampleApp/Data/ApplicationDbContext.cs?name=snippet_ApplicationDbContext&highlight=5-6)]

    <span data-ttu-id="982a8-228">사용자 지정 데이터베이스 컨텍스트 클래스의 Id 서비스를 추가 하는 경우 등록 `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="982a8-228">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    [!code-csharp[](customize-identity-model/samples/2.0/RazorPagesSampleApp/Startup.cs?name=snippet_ConfigureServices&highlight=7-9)]

    <span data-ttu-id="982a8-229">기본 키의 데이터 형식을 분석에서 유추 되는 <xref:Microsoft.EntityFrameworkCore.DbContext> 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-229">The primary key's data type is inferred by analyzing the <xref:Microsoft.EntityFrameworkCore.DbContext> object.</span></span>

    ::: moniker-end

    ::: moniker range="<= aspnetcore-1.1"

    [!code-csharp[](customize-identity-model/samples/1.1/MvcSampleApp/Data/ApplicationDbContext.cs?name=snippet_ApplicationDbContext&highlight=5-6)]

    <span data-ttu-id="982a8-230">사용자 지정 데이터베이스 컨텍스트 클래스의 Id 서비스를 추가 하는 경우 등록 `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="982a8-230">Register the custom database context class when adding the Identity service in `Startup.ConfigureServices`:</span></span>

    [!code-csharp[](customize-identity-model/samples/1.1/MvcSampleApp/Startup.cs?name=snippet_ConfigureServices&highlight=7-9)]

    <span data-ttu-id="982a8-231">합니다 <xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> 메서드에서 `TKey` 기본 키의 데이터 형식을 나타내는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-231">The <xref:Microsoft.Extensions.DependencyInjection.IdentityEntityFrameworkBuilderExtensions.AddEntityFrameworkStores*> method accepts a `TKey` type indicating the primary key's data type.</span></span>

    ::: moniker-end

### <a name="add-navigation-properties"></a><span data-ttu-id="982a8-232">탐색 속성 추가</span><span class="sxs-lookup"><span data-stu-id="982a8-232">Add navigation properties</span></span>

<span data-ttu-id="982a8-233">관계에 대 한 모델 구성을 변경 하는 것은 기타 변경을 보다 더 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-233">Changing the model configuration for relationships can be more difficult than making other changes.</span></span> <span data-ttu-id="982a8-234">새로 추가 관계를 만드는 대신 기존 관계를 대체 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-234">Care must be taken to replace the existing relationships rather than create new, additional relationships.</span></span> <span data-ttu-id="982a8-235">특히 변경 된 관계는 기존 관계와 같은 외래 키 (FK) 속성을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-235">In particular, the changed relationship must specify the same foreign key (FK) property as the existing relationship.</span></span> <span data-ttu-id="982a8-236">예를 들어, 간의 관계 `Users` 및 `UserClaims` 기본적으로 다음과 같이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-236">For example, the relationship between `Users` and `UserClaims` is, by default, specified as follows:</span></span>

```csharp
builder.Entity<TUser>(b =>
{
    // Each User can have many UserClaims
    b.HasMany<TUserClaim>()
     .WithOne()
     .HasForeignKey(uc => uc.UserId)
     .IsRequired();
});
```

<span data-ttu-id="982a8-237">이 관계에 대 한 외래 키로 지정 된 된 `UserClaim.UserId` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-237">The FK for this relationship is specified as the `UserClaim.UserId` property.</span></span> <span data-ttu-id="982a8-238">`HasMany` 및 `WithOne` 탐색 속성이 없는 관계를 인수 없이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-238">`HasMany` and `WithOne` are called without arguments to create the relationship without navigation properties.</span></span>

<span data-ttu-id="982a8-239">탐색 속성을 추가 `ApplicationUser` 연결 된 있도록 `UserClaims` 사용자에서 참조할 수:</span><span class="sxs-lookup"><span data-stu-id="982a8-239">Add a navigation property to `ApplicationUser` that allows associated `UserClaims` to be referenced from the user:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
}
```

<span data-ttu-id="982a8-240">합니다 `TKey` 에 대 한 `IdentityUserClaim<TKey>` 사용자의 PK에 대 한 지정 된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-240">The `TKey` for `IdentityUserClaim<TKey>` is the type specified for the PK of users.</span></span> <span data-ttu-id="982a8-241">이 예에서 `TKey` 는 `string` 기본값을 사용 중 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-241">In this case, `TKey` is `string` because the defaults are being used.</span></span> <span data-ttu-id="982a8-242">있기 **되지** PK 형식에 대 한는 `UserClaim` 엔터티 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-242">It's **not** the PK type for the `UserClaim` entity type.</span></span>

<span data-ttu-id="982a8-243">구성 되어야 합니다는 탐색 속성에 있으면 이제 `OnModelCreating`:</span><span class="sxs-lookup"><span data-stu-id="982a8-243">Now that the navigation property exists, it must be configured in `OnModelCreating`:</span></span>

```csharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();
        });
    }
}
```

<span data-ttu-id="982a8-244">관계와 똑같은 이전 호출에서 지정 된 탐색 속성을 사용 하 여만 구성 되어 있는지 확인 `HasMany`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-244">Notice that relationship is configured exactly as it was before, only with a navigation property specified in the call to `HasMany`.</span></span>

<span data-ttu-id="982a8-245">탐색 속성은 데이터베이스가 아니라 EF 모델에만 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-245">The navigation properties only exist in the EF model, not the database.</span></span> <span data-ttu-id="982a8-246">관계에 대 한 FK 변경 되지 않으므로 이러한 종류의 모델 변경에는 데이터베이스를 업데이트할 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-246">Because the FK for the relationship hasn't changed, this kind of model change doesn't require the database to be updated.</span></span> <span data-ttu-id="982a8-247">이 변경을 수행한 후 마이그레이션을 추가 하 여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-247">This can be checked by adding a migration after making the change.</span></span> <span data-ttu-id="982a8-248">합니다 `Up` 고 `Down` 메서드는 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-248">The `Up` and `Down` methods are empty.</span></span>

### <a name="add-all-user-navigation-properties"></a><span data-ttu-id="982a8-249">모든 사용자 탐색 속성 추가</span><span class="sxs-lookup"><span data-stu-id="982a8-249">Add all User navigation properties</span></span>

<span data-ttu-id="982a8-250">위의 섹션을 사용 하 여 지침으로, 다음 예제에서는 사용자의 모든 관계에 대 한 단방향 탐색 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-250">Using the section above as guidance, the following example configures unidirectional navigation properties for all relationships on User:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
    public virtual ICollection<IdentityUserLogin<string>> Logins { get; set; }
    public virtual ICollection<IdentityUserToken<string>> Tokens { get; set; }
    public virtual ICollection<IdentityUserRole<string>> UserRoles { get; set; }
}
```

```csharp
public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne()
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne()
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne()
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });
    }
}
```

### <a name="add-user-and-role-navigation-properties"></a><span data-ttu-id="982a8-251">사용자 및 역할 탐색 속성 추가</span><span class="sxs-lookup"><span data-stu-id="982a8-251">Add User and Role navigation properties</span></span>

<span data-ttu-id="982a8-252">위의 섹션을 사용 하 여 지침으로, 다음 예제에서는 사용자 및 역할에서 모든 관계에 대 한 탐색 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-252">Using the section above as guidance, the following example configures navigation properties for all relationships on User and Role:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<IdentityUserClaim<string>> Claims { get; set; }
    public virtual ICollection<IdentityUserLogin<string>> Logins { get; set; }
    public virtual ICollection<IdentityUserToken<string>> Tokens { get; set; }
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationRole : IdentityRole
{
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationUserRole : IdentityUserRole<string>
{
    public virtual ApplicationUser User { get; set; }
    public virtual ApplicationRole Role { get; set; }
}
```

```csharp
public class ApplicationDbContext
    : IdentityDbContext<
        ApplicationUser, ApplicationRole, string,
        IdentityUserClaim<string>, ApplicationUserRole, IdentityUserLogin<string>,
        IdentityRoleClaim<string>, IdentityUserToken<string>>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne()
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne()
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne()
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.User)
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });

        modelBuilder.Entity<ApplicationRole>(b =>
        {
            // Each Role can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.Role)
                .HasForeignKey(ur => ur.RoleId)
                .IsRequired();
        });

    }
}
```

<span data-ttu-id="982a8-253">메모:</span><span class="sxs-lookup"><span data-stu-id="982a8-253">Notes:</span></span>

* <span data-ttu-id="982a8-254">이 예제에서는 또한는 `UserRole` 역할에 사용자의 다 대 다 관계를 탐색 하는 데 필요한 엔터티를 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-254">This example also includes the `UserRole` join entity, which is needed to navigate the many-to-many relationship from Users to Roles.</span></span>
* <span data-ttu-id="982a8-255">반영 하도록 탐색 속성의 형식을 변경 해야 `ApplicationXxx` 형식 대신 지금 사용 중인 `IdentityXxx` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-255">Remember to change the types of the navigation properties to reflect that `ApplicationXxx` types are now being used instead of `IdentityXxx` types.</span></span>
* <span data-ttu-id="982a8-256">사용 해야 합니다 `ApplicationXxx` 제네릭에서 `ApplicationContext` 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-256">Remember to use the `ApplicationXxx` in the generic `ApplicationContext` definition.</span></span>

### <a name="add-all-navigation-properties"></a><span data-ttu-id="982a8-257">모든 탐색 속성 추가</span><span class="sxs-lookup"><span data-stu-id="982a8-257">Add all navigation properties</span></span>

<span data-ttu-id="982a8-258">위의 섹션을 사용 하 여 지침으로, 다음 예제에서는 모든 엔터티 형식에서 모든 관계에 대 한 탐색 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-258">Using the section above as guidance, the following example configures navigation properties for all relationships on all entity types:</span></span>

```csharp
public class ApplicationUser : IdentityUser
{
    public virtual ICollection<ApplicationUserClaim> Claims { get; set; }
    public virtual ICollection<ApplicationUserLogin> Logins { get; set; }
    public virtual ICollection<ApplicationUserToken> Tokens { get; set; }
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
}

public class ApplicationRole : IdentityRole
{
    public virtual ICollection<ApplicationUserRole> UserRoles { get; set; }
    public virtual ICollection<ApplicationRoleClaim> RoleClaims { get; set; }
}

public class ApplicationUserRole : IdentityUserRole<string>
{
    public virtual ApplicationUser User { get; set; }
    public virtual ApplicationRole Role { get; set; }
}

public class ApplicationUserClaim : IdentityUserClaim<string>
{
    public virtual ApplicationUser User { get; set; }
}

public class ApplicationUserLogin : IdentityUserLogin<string>
{
    public virtual ApplicationUser User { get; set; }
}

public class ApplicationRoleClaim : IdentityRoleClaim<string>
{
    public virtual ApplicationRole Role { get; set; }
}

public class ApplicationUserToken : IdentityUserToken<string>
{
    public virtual ApplicationUser User { get; set; }
}
```

```csharp
public class ApplicationDbContext
    : IdentityDbContext<
        ApplicationUser, ApplicationRole, string,
        ApplicationUserClaim, ApplicationUserRole, ApplicationUserLogin,
        ApplicationRoleClaim, ApplicationUserToken>
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {
    }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<ApplicationUser>(b =>
        {
            // Each User can have many UserClaims
            b.HasMany(e => e.Claims)
                .WithOne(e => e.User)
                .HasForeignKey(uc => uc.UserId)
                .IsRequired();

            // Each User can have many UserLogins
            b.HasMany(e => e.Logins)
                .WithOne(e => e.User)
                .HasForeignKey(ul => ul.UserId)
                .IsRequired();

            // Each User can have many UserTokens
            b.HasMany(e => e.Tokens)
                .WithOne(e => e.User)
                .HasForeignKey(ut => ut.UserId)
                .IsRequired();

            // Each User can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.User)
                .HasForeignKey(ur => ur.UserId)
                .IsRequired();
        });

        modelBuilder.Entity<ApplicationRole>(b =>
        {
            // Each Role can have many entries in the UserRole join table
            b.HasMany(e => e.UserRoles)
                .WithOne(e => e.Role)
                .HasForeignKey(ur => ur.RoleId)
                .IsRequired();

            // Each Role can have many associated RoleClaims
            b.HasMany(e => e.RoleClaims)
                .WithOne(e => e.Role)
                .HasForeignKey(rc => rc.RoleId)
                .IsRequired();
        });
    }
}
```

### <a name="use-composite-keys"></a><span data-ttu-id="982a8-259">복합 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-259">Use composite keys</span></span>

<span data-ttu-id="982a8-260">이전 섹션에서는 Id 모델에 사용 된 키의 형식을 변경 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-260">The preceding sections demonstrated changing the type of key used in the Identity model.</span></span> <span data-ttu-id="982a8-261">복합 키를 사용 하도록 Id 키 모델 변경 지원 또는 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-261">Changing the Identity key model to use composite keys isn't supported or recommended.</span></span> <span data-ttu-id="982a8-262">Identity를 사용 하 여 복합 키를 사용 하 여 Identity manager 코드 모델과 상호 작용 하는 방법을 변경 하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-262">Using a composite key with Identity involves changing how the Identity manager code interacts with the model.</span></span> <span data-ttu-id="982a8-263">이 사용자 지정이 문서의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-263">This customization is beyond the scope of this document.</span></span>

### <a name="change-tablecolumn-names-and-facets"></a><span data-ttu-id="982a8-264">테이블/열 이름 바꾸기 및 패싯</span><span class="sxs-lookup"><span data-stu-id="982a8-264">Change table/column names and facets</span></span>

<span data-ttu-id="982a8-265">테이블 및 열 이름을 변경 하려면 호출 `base.OnModelCreating`합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-265">To change the names of tables and columns, call `base.OnModelCreating`.</span></span> <span data-ttu-id="982a8-266">기본값을 재정의 하는 구성에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-266">Then, add configuration to override any of the defaults.</span></span> <span data-ttu-id="982a8-267">예를 들어, 모든 Identity 테이블의 이름을 변경 하려면:</span><span class="sxs-lookup"><span data-stu-id="982a8-267">For example, to change the name of all the Identity tables:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.ToTable("MyUsers");
    });

    modelBuilder.Entity<IdentityUserClaim<string>>(b =>
    {
        b.ToTable("MyUserClaims");
    });

    modelBuilder.Entity<IdentityUserLogin<string>>(b =>
    {
        b.ToTable("MyUserLogins");
    });

    modelBuilder.Entity<IdentityUserToken<string>>(b =>
    {
        b.ToTable("MyUserTokens");
    });

    modelBuilder.Entity<IdentityRole>(b =>
    {
        b.ToTable("MyRoles");
    });

    modelBuilder.Entity<IdentityRoleClaim<string>>(b =>
    {
        b.ToTable("MyRoleClaims");
    });

    modelBuilder.Entity<IdentityUserRole<string>>(b =>
    {
        b.ToTable("MyUserRoles");
    });
}
```

<span data-ttu-id="982a8-268">이러한 예제에는 기본 Id 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-268">These examples use the default Identity types.</span></span> <span data-ttu-id="982a8-269">와 같은 앱 유형을 사용 하는 경우 `ApplicationUser`, 기본 형식 대신 해당 형식을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-269">If using an app type such as `ApplicationUser`, configure that type instead of the default type.</span></span>

<span data-ttu-id="982a8-270">다음 예제에서는 일부 열 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-270">The following example changes some column names:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.Property(e => e.Email).HasColumnName("EMail");
    });

    modelBuilder.Entity<IdentityUserClaim<string>>(b =>
    {
        b.Property(e => e.ClaimType).HasColumnName("CType");
        b.Property(e => e.ClaimValue).HasColumnName("CValue");
    });
}
```

<span data-ttu-id="982a8-271">특정를 사용 하 여 일부 유형의 데이터베이스 열을 구성할 수 있습니다 *패싯* (예를 들어 최대 `string` 허용 되는 길이).</span><span class="sxs-lookup"><span data-stu-id="982a8-271">Some types of database columns can be configured with certain *facets* (for example, the maximum `string` length allowed).</span></span> <span data-ttu-id="982a8-272">여러 열의 최대 길이 설정 하는 다음 예제에서는 `string` 모델의 속성:</span><span class="sxs-lookup"><span data-stu-id="982a8-272">The following example sets column maximum lengths for several `string` properties in the model:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<IdentityUser>(b =>
    {
        b.Property(u => u.UserName).HasMaxLength(128);
        b.Property(u => u.NormalizedUserName).HasMaxLength(128);
        b.Property(u => u.Email).HasMaxLength(128);
        b.Property(u => u.NormalizedEmail).HasMaxLength(128);
    });

    modelBuilder.Entity<IdentityUserToken<string>>(b =>
    {
        b.Property(t => t.LoginProvider).HasMaxLength(128);
        b.Property(t => t.Name).HasMaxLength(128);
    });
}
```

### <a name="map-to-a-different-schema"></a><span data-ttu-id="982a8-273">다른 스키마에 매핑</span><span class="sxs-lookup"><span data-stu-id="982a8-273">Map to a different schema</span></span>

<span data-ttu-id="982a8-274">스키마는 데이터베이스 공급자에서 다르게 동작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-274">Schemas can behave differently across database providers.</span></span> <span data-ttu-id="982a8-275">SQL Server에 대 한 기본값의 모든 테이블을 만들 때 합니다 *dbo* 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-275">For SQL Server, the default is to create all tables in the *dbo* schema.</span></span> <span data-ttu-id="982a8-276">다른 스키마에서 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-276">The tables can be created in a different schema.</span></span> <span data-ttu-id="982a8-277">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="982a8-277">For example:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.HasDefaultSchema("notdbo");
}
```

::: moniker range=">= aspnetcore-2.1"

### <a name="lazy-loading"></a><span data-ttu-id="982a8-278">지연 로드</span><span class="sxs-lookup"><span data-stu-id="982a8-278">Lazy loading</span></span>

<span data-ttu-id="982a8-279">이 섹션에서는 지연 로드 프록시 Id 모델에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-279">In this section, support for lazy-loading proxies in the Identity model is added.</span></span> <span data-ttu-id="982a8-280">지연 로드는 탐색 속성을 로드 하는 첫 번째 확인 하지 않고 사용할 수 있으므로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-280">Lazy-loading is useful since it allows navigation properties to be used without first ensuring they're loaded.</span></span>

<span data-ttu-id="982a8-281">엔터티 형식 수에 대 한 적합 한 여러 가지 방법으로 지연 로드에 설명 된 대로 합니다 [EF Core 설명서](/ef/core/querying/related-data#lazy-loading)합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-281">Entity types can be made suitable for lazy-loading in several ways, as described in the [EF Core documentation](/ef/core/querying/related-data#lazy-loading).</span></span> <span data-ttu-id="982a8-282">간단히 하기 위해 요구 하는 지연 로드 프록시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-282">For simplicity, use lazy-loading proxies, which requires:</span></span>

* <span data-ttu-id="982a8-283">설치 합니다 [Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/) 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-283">Installation of the [Microsoft.EntityFrameworkCore.Proxies](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Proxies/) package.</span></span>
* <span data-ttu-id="982a8-284">에 대 한 호출 <xref:Microsoft.EntityFrameworkCore.ProxiesExtensions.UseLazyLoadingProxies*> 내부 <xref:Microsoft.Extensions.DependencyInjection.EntityFrameworkServiceCollectionExtensions.AddDbContext*>합니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-284">A call to <xref:Microsoft.EntityFrameworkCore.ProxiesExtensions.UseLazyLoadingProxies*> inside <xref:Microsoft.Extensions.DependencyInjection.EntityFrameworkServiceCollectionExtensions.AddDbContext*>.</span></span>
* <span data-ttu-id="982a8-285">공용 엔터티 형식을 사용 하 여 `public virtual` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="982a8-285">Public entity types with `public virtual` navigation properties.</span></span>

<span data-ttu-id="982a8-286">다음 예제에서는 호출 `UseLazyLoadingProxies` 에서 `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="982a8-286">The following example demonstrates calling `UseLazyLoadingProxies` in `Startup.ConfigureServices`:</span></span>

```csharp
services
    .AddDbContext<ApplicationDbContext>(
        b => b.UseSqlServer(connectionString)
              .UseLazyLoadingProxies())
    .AddDefaultIdentity<ApplicationUser>()
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

<span data-ttu-id="982a8-287">엔터티 형식에 탐색 속성을 추가 하는 지침은 앞의 예제를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="982a8-287">Refer to the preceding examples for guidance on adding navigation properties to the entity types.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="982a8-288">추가 자료</span><span class="sxs-lookup"><span data-stu-id="982a8-288">Additional resources</span></span>

* <xref:security/authentication/scaffold-identity>

::: moniker-end
