---
ms.openlocfilehash: 4a4ad30846d1993b3e561c96c00fbf9a0c7f3929
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040810"
---
# <a name="aspnet-core-url-rewriting-sample-aspnet-core-2x"></a><span data-ttu-id="63b28-101">ASP.NET Core URL 다시 작성 샘플(ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="63b28-101">ASP.NET Core URL Rewriting Sample (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="63b28-102">이 샘플은 ASP.NET Core 2.x URL 다시 작성 미들웨어의 사용법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="63b28-102">This sample illustrates usage of ASP.NET Core 2.x URL Rewriting Middleware.</span></span> <span data-ttu-id="63b28-103">앱은 URL 리디렉션 및 URL 다시 작성 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="63b28-103">The app demonstrates URL redirect and URL rewriting options.</span></span>

<span data-ttu-id="63b28-104">샘플을 실행하면, 규칙 중 하나가 요청 URL에 적용될 때 파일 외 응답이 다시 작성되거나 리디렉션된 URL로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="63b28-104">When running the sample, non-file responses return the rewritten or redirected URL when one of the rules is applied to a request URL.</span></span> <span data-ttu-id="63b28-105">XML 및 텍스트 파일 예제에서, 정적 파일 미들웨어는 미들웨어에서 요청 URL을 다시 작성한 후 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63b28-105">For the XML and text file examples, Static File Middleware serves the file after the request URL is rewritten by the middleware.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="63b28-106">이 샘플의 예제</span><span class="sxs-lookup"><span data-stu-id="63b28-106">Examples in this sample</span></span>

* `AddRedirect("redirect-rule/(.*)", "redirected/$1")`
  - <span data-ttu-id="63b28-107">성공 상태 코드: 302 (있음)</span><span class="sxs-lookup"><span data-stu-id="63b28-107">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="63b28-108">예(리디렉션): **/redirect-rule/{capture_group}** 을 **/redirected/{capture_group}** 으로</span><span class="sxs-lookup"><span data-stu-id="63b28-108">Example (redirect): **/redirect-rule/{capture_group}** to **/redirected/{capture_group}**</span></span>
* `AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", skipRemainingRules: true)`
  - <span data-ttu-id="63b28-109">성공 상태 코드: 200 (정상)</span><span class="sxs-lookup"><span data-stu-id="63b28-109">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="63b28-110">예(다시 작성): **/rewrite-rule/{capture_group_1}/{capture_group_2}** 를 **/rewrtten?var1={capture_group_1}&var2={capture_group_2}** 로</span><span class="sxs-lookup"><span data-stu-id="63b28-110">Example (rewrite): **/rewrite-rule/{capture_group_1}/{capture_group_2}** to **/rewritten?var1={capture_group_1}&var2={capture_group_2}**</span></span>
* `AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")`
  - <span data-ttu-id="63b28-111">성공 상태 코드: 302 (있음)</span><span class="sxs-lookup"><span data-stu-id="63b28-111">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="63b28-112">예(리디렉션): **/apache-mod-rules-redirect/{capture_group}** 을 **/redirected?id={capture_group}** 으로</span><span class="sxs-lookup"><span data-stu-id="63b28-112">Example (redirect): **/apache-mod-rules-redirect/{capture_group}** to **/redirected?id={capture_group}**</span></span>
* `AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")`
  - <span data-ttu-id="63b28-113">성공 상태 코드: 200 (정상)</span><span class="sxs-lookup"><span data-stu-id="63b28-113">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="63b28-114">예(다시 작성): **/iis-rules-rewrite/{capture_group}** 을 **/rewritten?id={capture_group}** 으로</span><span class="sxs-lookup"><span data-stu-id="63b28-114">Example (rewrite): **/iis-rules-rewrite/{capture_group}** to **/rewritten?id={capture_group}**</span></span>
* `Add(RedirectXmlFileRequests)`
  - <span data-ttu-id="63b28-115">성공 상태 코드: 301 (영구적 이동)</span><span class="sxs-lookup"><span data-stu-id="63b28-115">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="63b28-116">예(리디렉션): **/file.xml**을 **/xmlfiles/file.xml**로</span><span class="sxs-lookup"><span data-stu-id="63b28-116">Example (redirect): **/file.xml** to **/xmlfiles/file.xml**</span></span>
* `Add(RewriteTextFileRequests)`
  - <span data-ttu-id="63b28-117">성공 상태 코드: 200 (정상)</span><span class="sxs-lookup"><span data-stu-id="63b28-117">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="63b28-118">예(다시 작성): **/some_file.txt**를 **/file.txt**로</span><span class="sxs-lookup"><span data-stu-id="63b28-118">Example (rewrite): **/some_file.txt** to **/file.txt**</span></span>
* `Add(new RedirectImageRequests(".png", "/png-images")))`<br>`Add(new RedirectImageRequests(".jpg", "/jpg-images")))`
  - <span data-ttu-id="63b28-119">성공 상태 코드: 301 (영구적 이동)</span><span class="sxs-lookup"><span data-stu-id="63b28-119">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="63b28-120">예(리디렉션): **/image.png**를 **/png-images/image.png**로</span><span class="sxs-lookup"><span data-stu-id="63b28-120">Example (redirect): **/image.png** to **/png-images/image.png**</span></span>
  - <span data-ttu-id="63b28-121">예(리디렉션): **/image.jpg**를 **/jpg-images/image.jpg**로</span><span class="sxs-lookup"><span data-stu-id="63b28-121">Example (redirect): **/image.jpg** to **/jpg-images/image.jpg**</span></span>

## <a name="use-a-physicalfileprovider"></a><span data-ttu-id="63b28-122">PhysicalFileProvider 사용</span><span class="sxs-lookup"><span data-stu-id="63b28-122">Use a PhysicalFileProvider</span></span>

<span data-ttu-id="63b28-123">또한 `PhysicalFileProvider`를 만들어 `IFileProvider`를 얻은 후 `AddApacheModRewrite()` 및 `AddIISUrlRewrite()` 메서드로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b28-123">You can also obtain an `IFileProvider` by creating a `PhysicalFileProvider` to pass into the `AddApacheModRewrite()` and `AddIISUrlRewrite()` methods:</span></span>

```csharp
using Microsoft.Extensions.FileProviders;
PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
```

## <a name="secure-redirection-extensions"></a><span data-ttu-id="63b28-124">보안 리디렉션 확장</span><span class="sxs-lookup"><span data-stu-id="63b28-124">Secure redirection extensions</span></span>

<span data-ttu-id="63b28-125">이 샘플은 URL(`https://localhost:5001`, `https://localhost`)을 사용하는 데 필요한 앱에 대한 `WebHostBuilder`구성 및 보안 리디렉션 메서드를 살펴보는 데 도움이 되는 테스트 인증서(*testCert.pfx*)를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b28-125">This sample includes `WebHostBuilder` configuration for the app to use URLs (`https://localhost:5001`, `https://localhost`) and a test certificate (*testCert.pfx*) to assist in exploring the secure redirect methods.</span></span> <span data-ttu-id="63b28-126">서버가 이미 포트 443을 할당하거나 사용중인 경우, `https://localhost`예제는 작동하지 않습니다. &mdash; *Program.cs* 파일의 `CreateWebHostBuilder`메서드에서 포트 443용 `ListenOptions`를 제거하거나 서버에서 포트 443을 바인딩 해제하여 Kestrel이 포트를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="63b28-126">If the server already has port 443 assigned or in use, the `https://localhost` example doesn't work&mdash;remove the `ListenOptions` for port 443 in the `CreateWebHostBuilder` method of the *Program.cs* file or unbind port 443 on the server so that Kestrel can use the port.</span></span>

| <span data-ttu-id="63b28-127">메서드</span><span class="sxs-lookup"><span data-stu-id="63b28-127">Method</span></span>                           | <span data-ttu-id="63b28-128">상태 코드</span><span class="sxs-lookup"><span data-stu-id="63b28-128">Status Code</span></span> |    <span data-ttu-id="63b28-129">포트</span><span class="sxs-lookup"><span data-stu-id="63b28-129">Port</span></span>    |
| -------------------------------- | :---------: | :--------: |
| `.AddRedirectToHttpsPermanent()` |     <span data-ttu-id="63b28-130">301</span><span class="sxs-lookup"><span data-stu-id="63b28-130">301</span></span>     | <span data-ttu-id="63b28-131">NULL(465)</span><span class="sxs-lookup"><span data-stu-id="63b28-131">null (465)</span></span> |
| `.AddRedirectToHttps()`          |     <span data-ttu-id="63b28-132">302</span><span class="sxs-lookup"><span data-stu-id="63b28-132">302</span></span>     | <span data-ttu-id="63b28-133">NULL(465)</span><span class="sxs-lookup"><span data-stu-id="63b28-133">null (465)</span></span> |
| `.AddRedirectToHttps(301)`       |     <span data-ttu-id="63b28-134">301</span><span class="sxs-lookup"><span data-stu-id="63b28-134">301</span></span>     | <span data-ttu-id="63b28-135">NULL(465)</span><span class="sxs-lookup"><span data-stu-id="63b28-135">null (465)</span></span> |
| `.AddRedirectToHttps(301, 5001)` |     <span data-ttu-id="63b28-136">301</span><span class="sxs-lookup"><span data-stu-id="63b28-136">301</span></span>     |    <span data-ttu-id="63b28-137">5001</span><span class="sxs-lookup"><span data-stu-id="63b28-137">5001</span></span>    |
