---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET 오류 처리 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: af5e5a9c8d211b07b57aa50238b02cabe249aef8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041630"
---
<a name="aspnet-error-handling"></a><span data-ttu-id="f4a35-103">ASP.NET 오류 처리</span><span class="sxs-lookup"><span data-stu-id="f4a35-103">ASP.NET Error Handling</span></span>
====================
<span data-ttu-id="f4a35-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="f4a35-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="f4a35-105">[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="f4a35-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="f4a35-106">이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="f4a35-107">Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="f4a35-108">이 자습서에서는 Wingtip Toys 샘플 응용 프로그램 오류 처리 및 오류 로그를 포함 하도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-108">In this tutorial, you will modify the Wingtip Toys sample application to include error handling and error logging.</span></span> <span data-ttu-id="f4a35-109">오류 처리 응용 프로그램이 정상적으로 오류를 처리 하 고 오류 메시지를 적절 하 게 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-109">Error handling will allow the application to gracefully handle errors and display error messages accordingly.</span></span> <span data-ttu-id="f4a35-110">오류 로그를 사용 하면을 찾고 발생 한 오류를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-110">Error logging will allow you to find and fix errors that have occurred.</span></span> <span data-ttu-id="f4a35-111">이 자습서는 "URL 라우팅" 이전 자습서에서 작성 하 고 Wingtip Toys 자습서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-111">This tutorial builds on the previous tutorial "URL Routing" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="f4a35-112">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="f4a35-112">What you'll learn:</span></span>

- <span data-ttu-id="f4a35-113">전역 오류 처리 응용 프로그램의 구성에 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-113">How to add global error handling to the application's configuration.</span></span>
- <span data-ttu-id="f4a35-114">응용 프로그램, 페이지 및 코드 수준에서 처리 하는 오류를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-114">How to add error handling at the application, page, and code levels.</span></span>
- <span data-ttu-id="f4a35-115">나중에 검토할 수에 대 한 오류를 기록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-115">How to log errors for later review.</span></span>
- <span data-ttu-id="f4a35-116">보안이 손상 되지 않는 오류 메시지를 표시 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="f4a35-116">How to display error messages that do not compromise security.</span></span>
- <span data-ttu-id="f4a35-117">오류 로깅 모듈 및 처리기의 ELMAH () 오류 로깅을 구현 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="f4a35-117">How to implement Error Logging Modules and Handlers (ELMAH) error logging.</span></span>

## <a name="overview"></a><span data-ttu-id="f4a35-118">개요</span><span class="sxs-lookup"><span data-stu-id="f4a35-118">Overview</span></span>

<span data-ttu-id="f4a35-119">ASP.NET 응용 프로그램은 일관 된 방식으로 실행 하는 동안 발생 하는 오류를 처리할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-119">ASP.NET applications must be able to handle errors that occur during execution in a consistent manner.</span></span> <span data-ttu-id="f4a35-120">ASP.NET 일관 된 방식으로 응용 프로그램에 오류를 알리는 방법을 제공 하는 공용 언어 런타임 (CLR)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-120">ASP.NET uses the common language runtime (CLR), which provides a way of notifying applications of errors in a uniform way.</span></span> <span data-ttu-id="f4a35-121">오류가 발생 하면 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-121">When an error occurs, an exception is thrown.</span></span> <span data-ttu-id="f4a35-122">예외는 오류, 조건 또는 응용 프로그램에서 발생 하는 예기치 않은 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-122">An exception is any error, condition, or unexpected behavior that an application encounters.</span></span>

<span data-ttu-id="f4a35-123">.NET Framework에서 예외는 `System.Exception`에서 상속받은 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-123">In the .NET Framework, an exception is an object that inherits from the `System.Exception` class.</span></span> <span data-ttu-id="f4a35-124">예외는 문제가 발생한 코드 영역에서 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-124">An exception is thrown from an area of code where a problem has occurred.</span></span> <span data-ttu-id="f4a35-125">예외는 응용 프로그램에서 예외를 처리 하는 코드를 제공 하는 위치로 호출 스택 위로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-125">The exception is passed up the call stack to a place where the application provides code to handle the exception.</span></span> <span data-ttu-id="f4a35-126">응용 프로그램 예외를 처리 하지 않는 브라우저 오류 세부 정보를 표시 하도록 강제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-126">If the application does not handle the exception, the browser is forced to display the error details.</span></span>

<span data-ttu-id="f4a35-127">모범 사례로, 코드 수준에서 오류 처리 `Try` / `Catch` / `Finally` 코드 내에서 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-127">As a best practice, handle errors in at the code level in `Try`/`Catch`/`Finally` blocks within your code.</span></span> <span data-ttu-id="f4a35-128">사용자 컨텍스트에서 발생 하는 문제를 해결할 수 있도록 이러한 블록을 배치 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-128">Try to place these blocks so that the user can correct problems in the context in which they occur.</span></span> <span data-ttu-id="f4a35-129">오류 처리 블록 오류가 발생 한 위치에서 너무 멀리 떨어진 경우 문제를 해결 하는 데 필요한 정보를 제공 하기 위해 더 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-129">If the error handling blocks are too far away from where the error occurred, it becomes more difficult to provide users with the information they need to fix the problem.</span></span>

### <a name="exception-class"></a><span data-ttu-id="f4a35-130">예외 클래스</span><span class="sxs-lookup"><span data-stu-id="f4a35-130">Exception Class</span></span>

<span data-ttu-id="f4a35-131">예외 클래스에는 예외가 상속 하는 기본 클래스가입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-131">The Exception class is the base class from which exceptions inherit.</span></span> <span data-ttu-id="f4a35-132">와 같은 대부분의 예외 개체는 예외 클래스의 몇 가지 파생된 클래스의 인스턴스를 `SystemException` 클래스를 `IndexOutOfRangeException` 클래스 또는 `ArgumentNullException` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-132">Most exception objects are instances of some derived class of the Exception class, such as the `SystemException` class, the `IndexOutOfRangeException` class, or the `ArgumentNullException` class.</span></span> <span data-ttu-id="f4a35-133">예외 클래스에 속성이 같은 `StackTrace` 속성을 `InnerException` 속성 및 `Message` 발생 한 오류에 대 한 특정 정보를 제공 하는 속성.</span><span class="sxs-lookup"><span data-stu-id="f4a35-133">The Exception class has properties, such as the `StackTrace` property, the `InnerException` property, and the `Message` property, that provide specific information about the error that has occurred.</span></span>

### <a name="exception-inheritance-hierarchy"></a><span data-ttu-id="f4a35-134">예외가 상속 계층 구조</span><span class="sxs-lookup"><span data-stu-id="f4a35-134">Exception Inheritance Hierarchy</span></span>

<span data-ttu-id="f4a35-135">런타임 예외에서 파생의 기본 집합이 `SystemException` 런타임 예외가 발생할 때 throw 되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-135">The runtime has a base set of exceptions deriving from the `SystemException` class that the runtime throws when an exception is encountered.</span></span> <span data-ttu-id="f4a35-136">대부분의 클래스와 같은 예외 클래스에서 상속 되는 `IndexOutOfRangeException` 클래스 및 `ArgumentNullException` 클래스, 추가 멤버를 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-136">Most of the classes that inherit from the Exception class, such as the `IndexOutOfRangeException` class and the `ArgumentNullException` class, do not implement additional members.</span></span> <span data-ttu-id="f4a35-137">따라서 가장 중요 한 정보는 예외에 대 한 예외, 예외 이름 및 예외에 포함 된 정보 계층 구조에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-137">Therefore, the most important information for an exception can be found in the hierarchy of exceptions, the exception name, and the information contained in the exception.</span></span>

### <a name="exception-handling-hierarchy"></a><span data-ttu-id="f4a35-138">예외 처리 계층</span><span class="sxs-lookup"><span data-stu-id="f4a35-138">Exception Handling Hierarchy</span></span>

<span data-ttu-id="f4a35-139">ASP.NET Web Forms 응용 프로그램에서는 특정 처리 계층에 따라 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-139">In an ASP.NET Web Forms application, exceptions can be handled based on a specific handling hierarchy.</span></span> <span data-ttu-id="f4a35-140">다음 수준에서 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-140">An exception can be handled at the following levels:</span></span>

- <span data-ttu-id="f4a35-141">응용 프로그램 수준</span><span class="sxs-lookup"><span data-stu-id="f4a35-141">Application level</span></span>
- <span data-ttu-id="f4a35-142">페이지 수준</span><span class="sxs-lookup"><span data-stu-id="f4a35-142">Page level</span></span>
- <span data-ttu-id="f4a35-143">코드 수준</span><span class="sxs-lookup"><span data-stu-id="f4a35-143">Code level</span></span>

<span data-ttu-id="f4a35-144">응용 프로그램에서 예외를 처리할 때 예외 클래스에서 상속 되는 예외에 대 한 추가 정보 검색 및 사용자에 게 표시 종종 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-144">When an application handles exceptions, additional information about the exception that is inherited from the Exception class can often be retrieved and displayed to the user.</span></span> <span data-ttu-id="f4a35-145">응용 프로그램, 페이지 및 코드 수준, 하는 것 외에도 HTTP 모듈 수준에서 IIS 사용자 지정 처리기를 사용 하 여 예외를 처리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-145">In addition to application, page, and code level, you can also handle exceptions at the HTTP module level and by using an IIS custom handler.</span></span>

### <a name="application-level-error-handling"></a><span data-ttu-id="f4a35-146">응용 프로그램 수준 오류 처리</span><span class="sxs-lookup"><span data-stu-id="f4a35-146">Application Level Error Handling</span></span>

<span data-ttu-id="f4a35-147">응용 프로그램의 구성을 수정 하거나 추가 하 여 응용 프로그램 수준에서 기본 오류를 처리할 수 있습니다는 `Application_Error` 처리기에는 *Global.asax* 응용 프로그램의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-147">You can handle default errors at the application level either by modifying your application's configuration or by adding an `Application_Error` handler in the *Global.asax* file of your application.</span></span>

<span data-ttu-id="f4a35-148">추가 하 여 기본 오류 및 HTTP 오류를 처리할 수 있습니다는 `customErrors` 섹션을 합니다 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-148">You can handle default errors and HTTP errors by adding a `customErrors` section to the *Web.config* file.</span></span> <span data-ttu-id="f4a35-149">`customErrors` 섹션을 사용 하면 사용자가 리디렉션됩니다 오류가 발생 하는 기본 페이지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-149">The `customErrors` section allows you to specify a default page that users will be redirected to when an error occurs.</span></span> <span data-ttu-id="f4a35-150">또한 특정 상태 코드 오류에 대 한 개별 페이지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-150">It also allows you to specify individual pages for specific status code errors.</span></span>

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

<span data-ttu-id="f4a35-151">그러나 다른 페이지로 사용자를 리디렉션할 구성을 사용 하는 경우에 발생 한 오류의 세부 정보 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-151">Unfortunately, when you use the configuration to redirect the user to a different page, you do not have the details of the error that occurred.</span></span>

<span data-ttu-id="f4a35-152">코드를 추가 하 여 응용 프로그램에서 발생 하는 오류를 트래핑할 수는 있지만 합니다 `Application_Error` 처리기에는 *Global.asax* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-152">However, you can trap errors that occur anywhere in your application by adding code to the `Application_Error` handler in the *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a><span data-ttu-id="f4a35-153">페이지 수준 오류 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="f4a35-153">Page Level Error Event Handling</span></span>

<span data-ttu-id="f4a35-154">없습니다 더 이상 아무 것도 페이지를 페이지 수준 처리기를 오류가 발생 하지만 컨트롤의 인스턴스는 유지 되지 않으므로 페이지로 사용자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-154">A page-level handler returns the user to the page where the error occurred, but because instances of controls are not maintained, there will no longer be anything on the page.</span></span> <span data-ttu-id="f4a35-155">응용 프로그램의 사용자에 게 오류 세부 정보를 제공, 특히 페이지로 오류 세부 정보를 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-155">To provide the error details to the user of the application, you must specifically write the error details to the page.</span></span>

<span data-ttu-id="f4a35-156">일반적으로 유용한 정보를 표시할 수 있는 페이지로 사용자 이동 또는 처리 되지 않은 오류를 기록 하는 페이지 수준 오류 처리기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-156">You would typically use a page-level error handler to log unhandled errors or to take the user to a page that can display helpful information.</span></span>

<span data-ttu-id="f4a35-157">이 코드 예제에는 ASP.NET 웹 페이지에서 오류 이벤트에 대 한 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-157">This code example shows a handler for the Error event in an ASP.NET Web page.</span></span> <span data-ttu-id="f4a35-158">이 처리기 내에서 이미 처리 되지 않은 모든 예외를 포착 `try` / `catch` 페이지에서 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-158">This handler catches all exceptions that are not already handled within `try`/`catch` blocks in the page.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

<span data-ttu-id="f4a35-159">오류를 처리 한 후 호출 하 여 해제 해야 하는 `ClearError` 서버 개체의 메서드 (`HttpServerUtility` 클래스), 그렇지 않으면 이전에 발생 한 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-159">After you handle an error, you must clear it by calling the `ClearError` method of the Server object (`HttpServerUtility` class), otherwise you will see an error that has previously occurred.</span></span>

### <a name="code-level-error-handling"></a><span data-ttu-id="f4a35-160">수준 오류 처리 코드</span><span class="sxs-lookup"><span data-stu-id="f4a35-160">Code Level Error Handling</span></span>

<span data-ttu-id="f4a35-161">하나가 오는 try 블록의 try / catch 문을 구성 또는 이상의 서로 다른 예외에 대 한 처리기를 지정 하는 절을 catch 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-161">The try-catch statement consists of a try block followed by one or more catch clauses, which specify handlers for different exceptions.</span></span> <span data-ttu-id="f4a35-162">예외가 throw 되 면는 CLR (공용 언어 런타임)이이 예외를 처리 하는 catch 문을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-162">When an exception is thrown, the common language runtime (CLR) looks for the catch statement that handles this exception.</span></span> <span data-ttu-id="f4a35-163">현재 실행 중인 메서드 catch 블록이 없으면 CLR은 등과 호출 스택을 확인 하 고 현재 메서드를 호출 하는 메서드를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-163">If the currently executing method does not contain a catch block, the CLR looks at the method that called the current method, and so on, up the call stack.</span></span> <span data-ttu-id="f4a35-164">Catch 블록이 없는 있으면 CLR 처리 되지 않은 예외 메시지가 사용자에 게 표시 및 프로그램의 실행을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-164">If no catch block is found, then the CLR displays an unhandled exception message to the user and stops execution of the program.</span></span>

<span data-ttu-id="f4a35-165">다음 코드 예제를 사용 하 여 일반적인 방법을 보여 줍니다 `try` / `catch` / `finally` 오류를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-165">The following code example shows a common way of using `try`/`catch`/`finally` to handle errors.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

<span data-ttu-id="f4a35-166">위의 코드에서 try 블록이 발생 가능한 예외를 방지 해야 하는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-166">In the above code, the try block contains the code that needs to be guarded against a possible exception.</span></span> <span data-ttu-id="f4a35-167">블록은 예외가 있거나 블록을 완료 될 때까지 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-167">The block is executed until either an exception is thrown or the block is completed successfully.</span></span> <span data-ttu-id="f4a35-168">경우는 `FileNotFoundException` 예외 또는 `IOException` 예외가 발생 하면 실행이 다른 페이지로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-168">If either a `FileNotFoundException` exception or an `IOException` exception occurs, the execution is transferred to a different page.</span></span> <span data-ttu-id="f4a35-169">그런 다음에 포함 된 코드는 finally 블록이 실행 된 오류가 발생 하는지 여부를 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-169">Then, the code contained in the finally block is executed, whether an error occurred or not.</span></span>

## <a name="adding-error-logging-support"></a><span data-ttu-id="f4a35-170">오류 로깅 지원 추가</span><span class="sxs-lookup"><span data-stu-id="f4a35-170">Adding Error Logging Support</span></span>

<span data-ttu-id="f4a35-171">Wingtip Toys 샘플 응용 프로그램에 오류 처리에 추가 하기 전에 추가 하 여 오류 로깅 지원을 추가 합니다는 `ExceptionUtility` 클래스를 *논리* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-171">Before adding error handling to the Wingtip Toys sample application, you will add error logging support by adding an `ExceptionUtility` class to the *Logic* folder.</span></span> <span data-ttu-id="f4a35-172">이 응용 프로그램 오류를 처리할 때마다 작업을 수행 하면 오류 세부 정보를 오류 로그 파일을 추가할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-172">By doing this, each time the application handles an error, the error details will be added to the error log file.</span></span>

1. <span data-ttu-id="f4a35-173">마우스 오른쪽 단추로 클릭 합니다 *논리* 한 다음 선택한 폴더 **추가**  - &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-173">Right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="f4a35-174">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-174">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="f4a35-175">선택 된 **Visual C#**  - &gt; **코드** 왼쪽의 템플릿 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-175">Select the **Visual C#** -&gt; **Code** templates group on the left.</span></span> <span data-ttu-id="f4a35-176">그런 다음 선택 **클래스**가운데에서 나열 하 고 이름을 **ExceptionUtility.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-176">Then, select **Class**from the middle list and name it **ExceptionUtility.cs**.</span></span>
3. <span data-ttu-id="f4a35-177">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-177">Choose **Add**.</span></span> <span data-ttu-id="f4a35-178">새 클래스 파일에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-178">The new class file is displayed.</span></span>
4. <span data-ttu-id="f4a35-179">기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-179">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

<span data-ttu-id="f4a35-180">예외를 호출 하 여는 예외 로그 파일에 기록 수 예외가 발생 하는 경우는 `LogException` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f4a35-180">When an exception occurs, the exception can be written to an exception log file by calling the `LogException` method.</span></span> <span data-ttu-id="f4a35-181">이 메서드는 두 개의 매개 변수, 예외 개체 및 예외의 원본에 대 한 세부 정보를 포함 하는 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-181">This method takes two parameters, the exception object and a string containing details about the source of the exception.</span></span> <span data-ttu-id="f4a35-182">예외 로그에 기록 됩니다 합니다 *ErrorLog.txt* 파일을 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-182">The exception log is written to the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>

### <a name="adding-an-error-page"></a><span data-ttu-id="f4a35-183">오류 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="f4a35-183">Adding an Error Page</span></span>

<span data-ttu-id="f4a35-184">Wingtip Toys 샘플 응용 프로그램에서 한 페이지 오류를 표시 하려면 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-184">In the Wingtip Toys sample application, one page will be used to display errors.</span></span> <span data-ttu-id="f4a35-185">오류 페이지는 사이트의 사용자에 게 보안 오류 메시지를 표시 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-185">The error page is designed to show a secure error message to users of the site.</span></span> <span data-ttu-id="f4a35-186">그러나 사용자가 코드의 현재 위치에 컴퓨터에 로컬로 제공 하는 HTTP 요청을 수행 하는 개발자가 추가 오류 세부 정보 오류 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-186">However, if the user is a developer making an HTTP request that is being served locally on the machine where the code lives, additional error details will be displayed on the error page.</span></span>

1. <span data-ttu-id="f4a35-187">프로젝트 이름을 마우스 오른쪽 단추로 클릭 (**Wingtip Toys**)에서 **솔루션 탐색기** 선택한 **추가**  - &gt; **새 항목**.</span><span class="sxs-lookup"><span data-stu-id="f4a35-187">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="f4a35-188">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-188">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="f4a35-189">선택 된 **Visual C#**  - &gt; **웹** 왼쪽의 템플릿 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-189">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="f4a35-190">가운데 목록에서 선택 **마스터 페이지를 사용 하 여 Web Form**, 하 고 이름을 **ErrorPage.aspx**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-190">From the middle list, select **Web Form with Master Page**,and name it **ErrorPage.aspx**.</span></span>
3. <span data-ttu-id="f4a35-191">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-191">Click **Add**.</span></span>
4. <span data-ttu-id="f4a35-192">선택 된 *Site.Master* 마스터 페이지 파일 및 선택한 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-192">Select the *Site.Master* file as the master page, and then choose **OK**.</span></span>
5. <span data-ttu-id="f4a35-193">기존 태그를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-193">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. <span data-ttu-id="f4a35-194">코드 숨김의 기존 코드를 바꿉니다 (*ErrorPage.aspx.cs*) 다음과 같이 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-194">Replace the existing code of the code-behind (*ErrorPage.aspx.cs*) so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

<span data-ttu-id="f4a35-195">오류 페이지 표시 되 면는 `Page_Load` 이벤트 처리기가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-195">When the error page is displayed, the `Page_Load` event handler is executed.</span></span> <span data-ttu-id="f4a35-196">에 `Page_Load` 처리기의 오류가 처리 먼저 될 위치에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-196">In the `Page_Load` handler, the location of where the error was first handled is determined.</span></span> <span data-ttu-id="f4a35-197">발생 한 마지막 오류를 호출 하 여 결정 됩니다 차례로 `GetLastError` 서버 개체의 메서드.</span><span class="sxs-lookup"><span data-stu-id="f4a35-197">Then, the last error that occurred is determined by call the `GetLastError` method of the Server object.</span></span> <span data-ttu-id="f4a35-198">예외를 더 이상 존재 하는 경우에 일반 예외를 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-198">If the exception no longer exists, a generic exception is created.</span></span> <span data-ttu-id="f4a35-199">그런 다음 HTTP 요청을 로컬로 수행한, 모든 오류 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-199">Then, if the HTTP request was made locally, all error details are shown.</span></span> <span data-ttu-id="f4a35-200">이 경우 웹 응용 프로그램을 실행 하는 로컬 컴퓨터만 이러한 오류 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-200">In this case, only the local machine running the web application will see these error details.</span></span> <span data-ttu-id="f4a35-201">오류 정보를 표시 된 후 로그 파일에 추가 하는 오류 및 서버에서 오류가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-201">After the error information has been displayed, the error is added to the log file and the error is cleared from the server.</span></span>

### <a name="displaying-unhandled-error-messages-for-the-application"></a><span data-ttu-id="f4a35-202">응용 프로그램에 대 한 처리 되지 않은 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-202">Displaying Unhandled Error Messages for the Application</span></span>

<span data-ttu-id="f4a35-203">추가 하 여는 `customErrors` 섹션을 합니다 *Web.config* 파일을 처리할 수 있습니다 신속 하 게 응용 프로그램 전체에서 발생 하는 간단한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-203">By adding a `customErrors` section to the *Web.config* file, you can quickly handle simple errors that occur throughout the application.</span></span> <span data-ttu-id="f4a35-204">또한 404-찾을 수 없는 파일 등 해당 상태 코드 값을 기반으로 하는 오류를 처리 하는 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-204">You can also specify how to handle errors based on their status code value, such as 404 - File not found.</span></span>

#### <a name="update-the-configuration"></a><span data-ttu-id="f4a35-205">구성 업데이트 하 고</span><span class="sxs-lookup"><span data-stu-id="f4a35-205">Update the Configuration</span></span>

<span data-ttu-id="f4a35-206">구성을 추가 하 여 업데이트를 `customErrors` 섹션을 합니다 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-206">Update the configuration by adding a `customErrors` section to the *Web.config* file.</span></span>

1. <span data-ttu-id="f4a35-207">**솔루션 탐색기**찾기 및 열기, 합니다 *Web.config* Wingtip Toys 샘플 응용 프로그램의 루트에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-207">In **Solution Explorer**, find and open the *Web.config* file at the root of the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="f4a35-208">추가 합니다 `customErrors` 섹션을 *Web.config* 내에서 파일을 `<system.web>` 다음과 같은 노드:</span><span class="sxs-lookup"><span data-stu-id="f4a35-208">Add the `customErrors` section to the *Web.config* file within the `<system.web>` node as follows:</span></span>   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. <span data-ttu-id="f4a35-209">저장 된 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-209">Save the *Web.config* file.</span></span>

<span data-ttu-id="f4a35-210">`customErrors` 섹션 "켜기"로 설정 되는 모드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-210">The `customErrors` section specifies the mode, which is set to "On".</span></span> <span data-ttu-id="f4a35-211">또한 지정 된 `defaultRedirect`, 지시 하는 응용 프로그램 오류가 발생할 때 탐색할 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-211">It also specifies the `defaultRedirect`, which tells the application which page to navigate to when an error occurs.</span></span> <span data-ttu-id="f4a35-212">또한 페이지를 찾을 수 없으면 404 오류를 처리 하는 방법을 지정 하는 특정 오류 요소를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-212">In addition, you have added a specific error element that specifies how to handle a 404 error when a page is not found.</span></span> <span data-ttu-id="f4a35-213">이 자습서의 뒷부분에서 추가 오류 처리 응용 프로그램 수준 오류의 세부 정보 캡처를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-213">Later in this tutorial, you will add additional error handling that will capture the details of an error at the application level.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="f4a35-214">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f4a35-214">Running the Application</span></span>

<span data-ttu-id="f4a35-215">업데이트 된 경로 확인 하려면 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-215">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="f4a35-216">키를 눌러 **F5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-216">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="f4a35-217">브라우저가 열리고 표시 합니다 *Default.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-217">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="f4a35-218">브라우저에 다음 URL을 입력 합니다. (사용 해야 **여** 포트 번호):</span><span class="sxs-lookup"><span data-stu-id="f4a35-218">Enter the following URL into the browser (be sure to use **your** port number):</span></span>  
    `https://localhost:44300/NoPage.aspx`
3. <span data-ttu-id="f4a35-219">검토 합니다 *ErrorPage.aspx* 브라우저에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-219">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 오류 처리-페이지 찾을 수 없음 오류](aspnet-error-handling/_static/image1.png)

<span data-ttu-id="f4a35-221">요청 하는 경우는 *NoPage.aspx* 존재 하지 않는 페이지 오류 페이지에는 표시 간단한 오류 메시지와 자세한 오류 정보를 추가 세부 정보를 사용할 수 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="f4a35-221">When you request the *NoPage.aspx* page, which does not exist, the error page will show the simple error message and the detailed error information if additional details are available.</span></span> <span data-ttu-id="f4a35-222">그러나 사용자는 원격 위치에서 존재 하지 않는 페이지를 요청 하는 경우 오류 페이지는 빨간색에서 오류 메시지를만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-222">However, if the user requested a non-existent page from a remote location, the error page would only show the error message in red.</span></span>

### <a name="including-an-exception-for-testing-purposes"></a><span data-ttu-id="f4a35-223">테스트 목적에 대 한 예외를 포함 하 여</span><span class="sxs-lookup"><span data-stu-id="f4a35-223">Including an Exception for Testing Purposes</span></span>

<span data-ttu-id="f4a35-224">발생 시 응용 프로그램이 어떻게 작동 하는지 확인 하려면, ASP.NET에서 오류 조건을 의도적으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-224">To verify how your application will function when an error occurs, you can deliberately create error conditions in ASP.NET.</span></span> <span data-ttu-id="f4a35-225">Wingtip Toys 샘플 응용 프로그램을 현상을 보려면 기본 페이지가 로드 하는 경우 테스트 예외를 throw 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-225">In the Wingtip Toys sample application, you will throw a test exception when the default page loads to see what happens.</span></span>

1. <span data-ttu-id="f4a35-226">코드 숨김을 엽니다는 *Default.aspx* Visual Studio의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-226">Open the code-behind of the *Default.aspx* page in Visual Studio.</span></span>   
   <span data-ttu-id="f4a35-227">합니다 *Default.aspx.cs* 코드 숨김 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-227">The *Default.aspx.cs* code-behind page will be displayed.</span></span>
2. <span data-ttu-id="f4a35-228">에 `Page_Load` 처리기를 처리기는 다음과 같이 표시 되도록 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-228">In the `Page_Load` handler, add code so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="f4a35-229">다양 한 유형의 예외를 만들 수는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-229">It is possible to create various different types of exceptions.</span></span> <span data-ttu-id="f4a35-230">위의 코드에서 만드는 `InvalidOperationException` 때 합니다 *Default.aspx* 페이지가 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-230">In the above code, you are creating an `InvalidOperationException` when the *Default.aspx* page is loaded.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="f4a35-231">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f4a35-231">Running the Application</span></span>

<span data-ttu-id="f4a35-232">응용 프로그램에서 예외를 처리 하는 방법을 확인 하려면 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-232">You can run the application to see how the application handles the exception.</span></span>

1. <span data-ttu-id="f4a35-233">키를 눌러 **ctrl+f5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-233">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="f4a35-234">응용 프로그램 InvalidOperationException을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-234">The application throws the InvalidOperationException.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="f4a35-235">눌러야 **ctrl+f5** 소스를 보려면 오류 Visual Studio에서 코드를 중단 하지 않고 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-235">You must press **CTRL+F5** to display the page without breaking into the code to view the source of the error in Visual Studio.</span></span>
2. <span data-ttu-id="f4a35-236">검토 합니다 *ErrorPage.aspx* 브라우저에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-236">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 오류 처리-오류 페이지](aspnet-error-handling/_static/image2.png)

<span data-ttu-id="f4a35-238">예외에 의해 포착 되 된 오류 정보를 보면 합니다 `customError` 섹션의 *Web.config* 파일.</span><span class="sxs-lookup"><span data-stu-id="f4a35-238">As you can see in the error details, the exception was trapped by the `customError` section in the *Web.config* file.</span></span>

### <a name="adding-application-level-error-handling"></a><span data-ttu-id="f4a35-239">응용 프로그램 수준 오류 처리 추가</span><span class="sxs-lookup"><span data-stu-id="f4a35-239">Adding Application-Level Error Handling</span></span>

<span data-ttu-id="f4a35-240">사용 하 여 예외를 트래핑 하는 대신 합니다 `customErrors` 섹션의 *Web.config* 파일, 예외에 대 한 정보만 확보 하는 경우 응용 프로그램 수준에서 오류를 트래핑 하 고 오류 세부 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-240">Rather than trap the exception using the `customErrors` section in the *Web.config* file, where you gain little information about the exception, you can trap the error at the application level and retrieve error details.</span></span>

1. <span data-ttu-id="f4a35-241">**솔루션 탐색기**찾기 및 열기, 합니다 *Global.asax.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-241">In **Solution Explorer**, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="f4a35-242">추가 **응용 프로그램\_오류** 처리기 다음과 같이 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-242">Add an **Application\_Error** handler so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

<span data-ttu-id="f4a35-243">응용 프로그램에서 오류가 발생 하는 경우는 `Application_Error` 처리기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-243">When an error occurs in the application, the `Application_Error` handler is called.</span></span> <span data-ttu-id="f4a35-244">이 처리기에서 마지막으로 예외를 검색 하 고 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-244">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="f4a35-245">예외 처리 되어 예외는 내부 예외 세부 정보를 포함 하는 경우 (즉, `InnerException` null이 아님), 응용 프로그램 실행을 이동 오류 페이지에는 예외 세부 정보에 표시 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-245">If the exception was unhandled and the exception contains inner-exception details (that is, `InnerException` is not null), the application transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="f4a35-246">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f4a35-246">Running the Application</span></span>

<span data-ttu-id="f4a35-247">응용 프로그램 수준에서 예외를 처리 하 여 제공 된 추가 오류 세부 정보를 보려면 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-247">You can run the application to see the additional error details provided by handling the exception at the application level.</span></span>

1. <span data-ttu-id="f4a35-248">키를 눌러 **ctrl+f5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-248">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="f4a35-249">응용 프로그램에서 throw 된 `InvalidOperationException` 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-249">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="f4a35-250">검토 합니다 *ErrorPage.aspx* 브라우저에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-250">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 오류 처리-응용 프로그램 수준 오류](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a><span data-ttu-id="f4a35-252">페이지 수준 오류 처리 추가</span><span class="sxs-lookup"><span data-stu-id="f4a35-252">Adding Page-Level Error Handling</span></span>

<span data-ttu-id="f4a35-253">에 추가할 수 있습니다 페이지 수준 오류 처리 페이지 추가 사용 하 여는 `ErrorPage` 특성을 `@Page` 페이지 또는 추가 하 여 지시문을 `Page_Error` 페이지의 코드 숨김에 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-253">You can add page-level error handling to a page either by using adding an `ErrorPage` attribute to the `@Page` directive of the page, or by adding a `Page_Error` event handler to the code-behind of a page.</span></span> <span data-ttu-id="f4a35-254">이 섹션에서는 추가 된 `Page_Error` 실행을 전송 하는 이벤트 처리기를 *ErrorPage.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="f4a35-254">In this section, you will add a `Page_Error` event handler that will transfer execution to the *ErrorPage.aspx* page.</span></span>

1. <span data-ttu-id="f4a35-255">**솔루션 탐색기**찾기 및 열기, 합니다 *Default.aspx.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-255">In **Solution Explorer**, find and open the *Default.aspx.cs* file.</span></span>
2. <span data-ttu-id="f4a35-256">추가 `Page_Error` 처리기로 코드 숨김 표시 되도록 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-256">Add a `Page_Error` handler so that the code-behind appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

<span data-ttu-id="f4a35-257">페이지에서 오류가 발생 하는 경우는 `Page_Error` 이벤트 처리기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-257">When an error occurs on the page, the `Page_Error` event handler is called.</span></span> <span data-ttu-id="f4a35-258">이 처리기에서 마지막으로 예외를 검색 하 고 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-258">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="f4a35-259">경우는 `InvalidOperationException` 발생을 `Page_Error` 이벤트 처리기 실행을 이동 오류 페이지에는 예외 세부 정보에 표시 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-259">If an `InvalidOperationException` occurs, the `Page_Error` event handler transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="f4a35-260">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f4a35-260">Running the Application</span></span>

<span data-ttu-id="f4a35-261">업데이트 된 경로 확인 하려면 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-261">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="f4a35-262">키를 눌러 **ctrl+f5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-262">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="f4a35-263">응용 프로그램에서 throw 된 `InvalidOperationException` 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-263">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="f4a35-264">검토 합니다 *ErrorPage.aspx* 브라우저에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-264">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 오류 처리-페이지 수준 오류](aspnet-error-handling/_static/image4.png)
3. <span data-ttu-id="f4a35-266">브라우저 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-266">Close your browser window.</span></span>

### <a name="removing-the-exception-used-for-testing"></a><span data-ttu-id="f4a35-267">테스트에 사용 되는 예외를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-267">Removing the Exception Used for Testing</span></span>

<span data-ttu-id="f4a35-268">이 자습서의 앞부분에서 추가한 예외를 throw 하지 않고 함수 Wingtip Toys 샘플 응용 프로그램을 허용 하려면 예외를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-268">To allow the Wingtip Toys sample application to function without throwing the exception you added earlier in this tutorial, remove the exception.</span></span>

1. <span data-ttu-id="f4a35-269">코드 숨김을 엽니다는 *Default.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-269">Open the code-behind of the *Default.aspx* page.</span></span>
2. <span data-ttu-id="f4a35-270">에 `Page_Load` 처리기를 처리기는 다음과 같이 표시 되도록 예외를 throw 하는 코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-270">In the `Page_Load` handler, remove the code that throws the exception so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a><span data-ttu-id="f4a35-271">코드 수준 오류 로깅 추가</span><span class="sxs-lookup"><span data-stu-id="f4a35-271">Adding Code-Level Error Logging</span></span>

<span data-ttu-id="f4a35-272">이 자습서의 앞부분에서 설명 했 듯이 코드 부분을 실행 하 고 발생 하는 첫 번째 오류를 처리 하려고 try/catch 문을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-272">As mentioned earlier in this tutorial, you can add try/catch statements to attempt to run a section of code and handle the first error that occurs.</span></span> <span data-ttu-id="f4a35-273">이 예제에서는 오류 세부 정보를 기록 오류 로그 파일의 오류를 나중에 검토할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-273">In this example, you will only write the error details to the error log file so that the error can be reviewed later.</span></span>

1. <span data-ttu-id="f4a35-274">**솔루션 탐색기**를 *논리* 폴더, 찾기 및 열기를 *PayPalFunctions.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-274">In **Solution Explorer**, in the *Logic* folder, find and open the *PayPalFunctions.cs* file.</span></span>
2. <span data-ttu-id="f4a35-275">업데이트 된 `HttpCall` 메서드 코드 요소로 다음과 같이 나타나도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-275">Update the `HttpCall` method so that the code appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

<span data-ttu-id="f4a35-276">위의 코드 호출을 `LogException` 에 포함 된 메서드는 `ExceptionUtility` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-276">The above code calls the `LogException` method that is contained in the `ExceptionUtility` class.</span></span> <span data-ttu-id="f4a35-277">추가한 합니다 *ExceptionUtility.cs* 클래스 파일을 합니다 *논리* 이 자습서의 앞부분에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-277">You added the *ExceptionUtility.cs* class file to the *Logic* folder earlier in this tutorial.</span></span> <span data-ttu-id="f4a35-278">`LogException` 메서드는 두 개의 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-278">The `LogException` method takes two parameters.</span></span> <span data-ttu-id="f4a35-279">첫 번째 매개 변수는 예외 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-279">The first parameter is the exception object.</span></span> <span data-ttu-id="f4a35-280">두 번째는 오류의 소스를 인식 하는 데 사용 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-280">The second parameter is a string used to recognize the source of the error.</span></span>

### <a name="inspecting-the-error-logging-information"></a><span data-ttu-id="f4a35-281">오류 로깅 정보를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-281">Inspecting the Error Logging Information</span></span>

<span data-ttu-id="f4a35-282">이전에 설명한 대로 응용 프로그램에서 오류를 먼저 수정 해야 확인 하려면 오류 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-282">As mentioned previously, you can use the error log to determine which errors in your application should be fixed first.</span></span> <span data-ttu-id="f4a35-283">물론, 트랩 및 오류 로그에 기록 된 오류만 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-283">Of course, only errors that have been trapped and written to the error log will be recorded.</span></span>

1. <span data-ttu-id="f4a35-284">**솔루션 탐색기**, 찾기 및 열기를 *ErrorLog.txt* 파일을 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-284">In **Solution Explorer**, find and open the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>   
 <span data-ttu-id="f4a35-285">선택 해야 할 수도 있습니다는 "**모든 파일 표시**" 옵션 또는 "**새로 고침**" 옵션의 맨 위에서 **솔루션 탐색기** 보려는 *ErrorLog.txt*파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-285">You may need to select the "**Show All Files**" option or the "**Refresh**" option from the top of **Solution Explorer** to see the *ErrorLog.txt* file.</span></span>
2. <span data-ttu-id="f4a35-286">Visual Studio에 표시 된 오류 로그를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-286">Review the error log displayed in Visual Studio:</span></span> 

    ![ASP.NET 오류 처리-ErrorLog.txt](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a><span data-ttu-id="f4a35-288">안전한 오류 메시지</span><span class="sxs-lookup"><span data-stu-id="f4a35-288">Safe Error Messages</span></span>

<span data-ttu-id="f4a35-289">것 **알아야** 는 응용 프로그램 오류 메시지를 표시 하는 경우이 해야 하지 포기할 악의적인 사용자는 응용 프로그램을 공격에 유용할 수 있는 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-289">It is **important to note** that when your application displays error messages, it should not give away information that a malicious user might find helpful in attacking your application.</span></span> <span data-ttu-id="f4a35-290">예를 들어, 응용 프로그램 데이터베이스 쓸 실패 시도 사용 하는 사용자 이름을 포함 하는 오류 메시지가 표시 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-290">For example, if your application unsuccessfully tries to write in to a database, it should not display an error message that includes the user name it is using.</span></span> <span data-ttu-id="f4a35-291">이러한 이유로 빨간색에서 일반 오류 메시지를 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-291">For this reason, a generic error message in red is displayed to the user.</span></span> <span data-ttu-id="f4a35-292">모든 추가 오류 세부 정보는 로컬 컴퓨터의 개발자에 게만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-292">All additional error details are only displayed to the developer on the local machine.</span></span>

## <a name="using-elmah"></a><span data-ttu-id="f4a35-293">ELMAH를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f4a35-293">Using ELMAH</span></span>

<span data-ttu-id="f4a35-294">ELMAH (오류 로깅 모듈 및 처리기)는 NuGet 패키지로 ASP.NET 응용 프로그램에 연결 하는 오류 로깅 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-294">ELMAH (Error Logging Modules and Handlers) is an error logging facility that you plug into your ASP.NET application as a NuGet package.</span></span> <span data-ttu-id="f4a35-295">ELMAH는 다음과 같은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-295">ELMAH provides the following capabilities:</span></span>

- <span data-ttu-id="f4a35-296">처리 되지 않은 예외의 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-296">Logging of unhandled exceptions.</span></span>
- <span data-ttu-id="f4a35-297">처리 되지 않은 예외를 기록된의 전체 로그를 보려면 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-297">A web page to view the entire log of recoded unhandled exceptions.</span></span>
- <span data-ttu-id="f4a35-298">각각의 전체 세부 정보를 보려면 웹 페이지 예외를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-298">A web page to view the full details of each logged exception.</span></span>
- <span data-ttu-id="f4a35-299">발생 시점에 각 오류의 전자 메일 알림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-299">An email notification of each error at the time it occurs.</span></span>
- <span data-ttu-id="f4a35-300">마지막 15 개의 오류 로그에서의 RSS 피드입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-300">An RSS feed of the last 15 errors from the log.</span></span>

<span data-ttu-id="f4a35-301">ELMAH를 사용 하 여 작업 하려면, 먼저 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-301">Before you can work with the ELMAH, you must install it.</span></span> <span data-ttu-id="f4a35-302">이 작업은 사용 하 여는 *NuGet* 설치 관리자를 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-302">This is easy using the *NuGet* package installer.</span></span> <span data-ttu-id="f4a35-303">이 자습서 시리즈의 앞부분에서 설명 했 듯이 NuGet은 쉽게 설치 하 고 Visual Studio에서 오픈 소스 라이브러리와 도구를 업데이트 하는 Visual Studio 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-303">As mentioned earlier in this tutorial series, NuGet is a Visual Studio extension that makes it easy to install and update open source libraries and tools in Visual Studio.</span></span>

1. <span data-ttu-id="f4a35-304">Visual Studio 내에서 **도구** 메뉴에서 **NuGet 패키지 관리자** > **솔루션용 NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-304">Within Visual Studio, from the **Tools** menu, select **NuGet Package Manager** > **Manage NuGet Packages for Solution**.</span></span> 

    ![ASP.NET 오류 처리-솔루션용 NuGet 패키지 관리](aspnet-error-handling/_static/image6.png)
2. <span data-ttu-id="f4a35-306">합니다 **NuGet 패키지 관리** Visual Studio 내에서 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-306">The **Manage NuGet Packages** dialog box is displayed within Visual Studio.</span></span>
3. <span data-ttu-id="f4a35-307">에 **NuGet 패키지 관리** 대화 상자에서 **Online** 왼쪽에서 선택한 후 **nuget.org**합니다. 그런 다음 찾아서 설치 합니다 **ELMAH** 온라인에서 사용 가능한 패키지의 목록에서 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-307">In the **Manage NuGet Packages** dialog box, expand **Online** on the left, and then select **nuget.org**. Then, find and install the **ELMAH** package from the list of available packages online.</span></span> 

    ![ASP.NET 오류 처리-ELMA NuGet 패키지](aspnet-error-handling/_static/image7.png)
4. <span data-ttu-id="f4a35-309">패키지를 다운로드 하려면 인터넷에 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-309">You will need to have an internet connection to download the package.</span></span>
5. <span data-ttu-id="f4a35-310">에 **프로젝트 선택** 대화 상자를 **WingtipToys** 선택을 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-310">In the **Select Projects** dialog box, make sure the **WingtipToys** selection is selected, and then click **OK**.</span></span> 

    ![ASP.NET 오류 처리-프로젝트 대화 상자를 선택 합니다.](aspnet-error-handling/_static/image8.png)
6. <span data-ttu-id="f4a35-312">클릭 **닫습니다** 에 **NuGet 패키지 관리** 필요한 경우 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f4a35-312">Click **Close** in the **Manage NuGet Packages** dialog box if needed.</span></span>
7. <span data-ttu-id="f4a35-313">Visual Studio에서 열려 있는 모든 파일을 다시 로드를 요청 하는 경우 선택 "**모두 예**"입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-313">If Visual Studio requests that you reload any open files, select "**Yes to All**".</span></span>
8. <span data-ttu-id="f4a35-314">ELMAH 패키지 자체에 대 한 항목을 추가 합니다 *Web.config* 프로젝트의 루트에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-314">The ELMAH package adds entries for itself in the *Web.config* file at the root of your project.</span></span> <span data-ttu-id="f4a35-315">Visual Studio 묻는 메시지가 수정 된 다시 로드 하려는 경우 *Web.config* 파일에서 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-315">If Visual Studio asks you if you want to reload the modified *Web.config* file, click **Yes**.</span></span>

<span data-ttu-id="f4a35-316">ELMAH 발생 하는 처리 되지 않은 오류를 저장할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-316">ELMAH is now ready to store any unhandled errors that occur.</span></span>

### <a name="viewing-the-elmah-log"></a><span data-ttu-id="f4a35-317">ELMAH 로그 보기</span><span class="sxs-lookup"><span data-stu-id="f4a35-317">Viewing the ELMAH Log</span></span>

<span data-ttu-id="f4a35-318">ELMAH 로그를 확인 하는 것은 쉽지만 있지만 ELMAH 로그에 기록 될 예외가 먼저 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-318">Viewing the ELMAH log is easy, but first you will create an unhandled exception that will be recorded in the ELMAH log.</span></span>

1. <span data-ttu-id="f4a35-319">키를 눌러 **ctrl+f5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-319">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="f4a35-320">처리 되지 않은 예외가 ELMAH 로그에 쓰려면 (포트 번호로 사용) 다음 URL로 브라우저에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-320">To write an unhandled exception to the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    <span data-ttu-id="f4a35-321">`https://localhost:44300/NoPage.aspx` 오류 페이지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-321">`https://localhost:44300/NoPage.aspx` The error page will be displayed.</span></span>
3. <span data-ttu-id="f4a35-322">ELMAH 로그를 표시 하려면 (포트 번호로 사용) 다음 URL로 브라우저에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-322">To display the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 오류 처리-ELMAH 오류 로그](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="f4a35-324">요약</span><span class="sxs-lookup"><span data-stu-id="f4a35-324">Summary</span></span>

<span data-ttu-id="f4a35-325">이 자습서에서는 응용 프로그램 수준, 페이지 수준 및 코드 수준에서 오류를 처리 하는 방법에 대 한 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-325">In this tutorial, you have learned about handling errors at the application level, the page level, and the code level.</span></span> <span data-ttu-id="f4a35-326">또한 나중에 검토할 수에 대 한 처리 및 처리 되지 않은 오류를 기록 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-326">You have also learned how to log handled and unhandled errors for later review.</span></span> <span data-ttu-id="f4a35-327">예외 로깅 및 NuGet을 사용 하 여 응용 프로그램에 대 한 알림을 제공 ELMAH 유틸리티를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-327">You added the ELMAH utility to provide exception logging and notification to your application using NuGet.</span></span> <span data-ttu-id="f4a35-328">또한 안전한 오류 메시지의 중요성에 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-328">Additionally, you have learned about the importance of safe error messages.</span></span>

## <a name="tutorial-series-conclusion"></a><span data-ttu-id="f4a35-329">자습서 시리즈 결론</span><span class="sxs-lookup"><span data-stu-id="f4a35-329">Tutorial Series Conclusion</span></span>

<span data-ttu-id="f4a35-330">*에 따라 다음에 참여해 주셔서 감사 합니다. 이 자습서 집합을 통해 ASP.NET Web Forms에 더 익숙해질 수 있기를 기대 합니다. ASP.NET 4.5와 Visual Studio 2013에서 사용 가능한 Web Forms 기능에 대 한 자세한 내용은 참조 하세요* [ *ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보* ](../../../../visual-studio/overview/2013/release-notes.md)  *. 또한에 언급 된 자습서를 살펴보려면 해야 합니다* \***다음 단계 \* \* \* 섹션과 defintely 사용해 합니다* [ *무료 Azure 평가판* ](https://azure.microsoft.com/pricing/free-trial/)*.\*</span><span class="sxs-lookup"><span data-stu-id="f4a35-330">*Thanks for following along. I hope this set of tutorials helped you become more familiar with ASP.NET Web Forms. If you need more information about Web Forms features available in ASP.NET 4.5 and Visual Studio 2013, see* [*ASP.NET and Web Tools for Visual Studio 2013 Release Notes*](../../../../visual-studio/overview/2013/release-notes.md)*. Also, be sure to take a look at the tutorial mentioned in the* \***Next Steps\*\*\*\*section and defintely try out the* [*free Azure trial*](https://azure.microsoft.com/pricing/free-trial/)*.\*</span></span>

![감사-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a><span data-ttu-id="f4a35-332">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4a35-332">Next Steps</span></span>

<span data-ttu-id="f4a35-333">Microsoft Azure에 웹 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 [보안 ASP.NET Web Forms 앱을 멤버 자격, OAuth 및 SQL Database를 사용 하 여 Azure 웹 사이트로 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-333">Learn more about deploying your web application to Microsoft Azure, see [Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to an Azure Web Site](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/).</span></span>

## <a name="free-trial"></a><span data-ttu-id="f4a35-334">무료 평가판</span><span class="sxs-lookup"><span data-stu-id="f4a35-334">Free Trial</span></span>

[<span data-ttu-id="f4a35-335">Microsoft Azure 무료 평가판</span><span class="sxs-lookup"><span data-stu-id="f4a35-335">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)  
 <span data-ttu-id="f4a35-336">Microsoft Azure에 웹 사이트를 게시할는 수 고를 덜, 유지 관리 비용.</span><span class="sxs-lookup"><span data-stu-id="f4a35-336">Publishing your website to Microsoft Azure will save you time, maintenance and expense.</span></span> <span data-ttu-id="f4a35-337">Azure에 웹 앱을 배포 하는 빠른 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-337">It's a quick process to deploying your web app to Azure.</span></span> <span data-ttu-id="f4a35-338">유지 관리 하 고 웹 앱을 모니터링 해야 할 때 Azure는 다양 한 도구 및 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-338">When you need to maintain and monitor your web app, Azure offers a variety of tools and services.</span></span> <span data-ttu-id="f4a35-339">데이터, 트래픽, id, 백업, 메시징, 미디어 및 Azure에서 성능을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-339">Manage data, traffic, identity, backups, messaging, media and performance in Azure.</span></span> <span data-ttu-id="f4a35-340">및이 모두 매우 경제적인 방식으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-340">And, all of this is provided in a very cost effective approach.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f4a35-341">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f4a35-341">Additional Resources</span></span>

<span data-ttu-id="f4a35-342">[ASP.NET 상태 모니터링을 사용 하 여 오류 세부 정보 로깅](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span><span class="sxs-lookup"><span data-stu-id="f4a35-342">[Logging Error Details with ASP.NET Health Monitoring](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span></span>  
[<span data-ttu-id="f4a35-343">ELMAH</span><span class="sxs-lookup"><span data-stu-id="f4a35-343">ELMAH</span></span>](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a><span data-ttu-id="f4a35-344">감사의 글</span><span class="sxs-lookup"><span data-stu-id="f4a35-344">Acknowledgements</span></span>

<span data-ttu-id="f4a35-345">이 자습서 시리즈의 콘텐츠에 중요 한 기여를 수행한 다음 사용자를 감사 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a35-345">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="f4a35-346">Alberto Poblacion, MVP &amp; MCT, 스페인</span><span class="sxs-lookup"><span data-stu-id="f4a35-346">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="f4a35-347">[Alex Thissen, 네덜란드](http://blog.alexthissen.nl/) (twitter: [ @alexthissen ](http://twitter.com/alexthissen))</span><span class="sxs-lookup"><span data-stu-id="f4a35-347">[Alex Thissen, Netherlands](http://blog.alexthissen.nl/) (twitter: [@alexthissen](http://twitter.com/alexthissen))</span></span>
- [<span data-ttu-id="f4a35-348">Andre Tournier, 미국</span><span class="sxs-lookup"><span data-stu-id="f4a35-348">Andre Tournier, USA</span></span>](http://andret503.wordpress.com/)
- <span data-ttu-id="f4a35-349">Apurva Joshi, Microsoft</span><span class="sxs-lookup"><span data-stu-id="f4a35-349">Apurva Joshi, Microsoft</span></span>
- [<span data-ttu-id="f4a35-350">Bojan Vrhovnik, 슬로베니아</span><span class="sxs-lookup"><span data-stu-id="f4a35-350">Bojan Vrhovnik, Slovenia</span></span>](http://twitter.com/bvrhovnik)
- <span data-ttu-id="f4a35-351">[Bruno Sonnino, 브라질](http://msmvps.com/blogs/bsonnino) (twitter: [ @bsonnino ](http://twitter.com/bsonnino))</span><span class="sxs-lookup"><span data-stu-id="f4a35-351">[Bruno Sonnino, Brazil](http://msmvps.com/blogs/bsonnino) (twitter: [@bsonnino](http://twitter.com/bsonnino))</span></span>
- [<span data-ttu-id="f4a35-352">Carlos dos Santos, 브라질</span><span class="sxs-lookup"><span data-stu-id="f4a35-352">Carlos dos Santos, Brazil</span></span>](http://www.carloscds.net/)
- <span data-ttu-id="f4a35-353">[Dave Campbell, 미국](http://www.wynapse.com/) (twitter: [ @windowsdevnews ](http://twitter.com/windowsdevnews))</span><span class="sxs-lookup"><span data-stu-id="f4a35-353">[Dave Campbell, USA](http://www.wynapse.com/) (twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))</span></span>
- <span data-ttu-id="f4a35-354">[Microsoft, Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="f4a35-354">[Jon Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- <span data-ttu-id="f4a35-355">[Michael 정자, USA](http://www.930solutions.com/) (twitter: [ @mrsharps ](http://twitter.com/mrsharps))</span><span class="sxs-lookup"><span data-stu-id="f4a35-355">[Michael Sharps, USA](http://www.930solutions.com/) (twitter: [@mrsharps](http://twitter.com/mrsharps))</span></span>
- <span data-ttu-id="f4a35-356">Mike 되</span><span class="sxs-lookup"><span data-stu-id="f4a35-356">Mike Pope</span></span>
- <span data-ttu-id="f4a35-357">[Mitchel 판매자, USA](http://www.mitchelsellers.com/) (twitter: [ @MitchelSellers ](http://twitter.com/MitchelSellers))</span><span class="sxs-lookup"><span data-stu-id="f4a35-357">[Mitchel Sellers, USA](http://www.mitchelsellers.com/) (twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))</span></span>
- [<span data-ttu-id="f4a35-358">Paul Cociuba, Microsoft</span><span class="sxs-lookup"><span data-stu-id="f4a35-358">Paul Cociuba, Microsoft</span></span>](http://linqto.me/Links/pcociuba)
- [<span data-ttu-id="f4a35-359">Paulo Morgado, Portugal</span><span class="sxs-lookup"><span data-stu-id="f4a35-359">Paulo Morgado, Portugal</span></span>](http://paulomorgado.net/)
- [<span data-ttu-id="f4a35-360">Pranav Rastogi, Microsoft</span><span class="sxs-lookup"><span data-stu-id="f4a35-360">Pranav Rastogi, Microsoft</span></span>](https://blogs.msdn.com/b/pranav_rastogi)
- [<span data-ttu-id="f4a35-361">Tim Ammann, Microsoft</span><span class="sxs-lookup"><span data-stu-id="f4a35-361">Tim Ammann, Microsoft</span></span>](https://blogs.iis.net/timamm/default.aspx)
- [<span data-ttu-id="f4a35-362">Microsoft, Tom Dykstra</span><span class="sxs-lookup"><span data-stu-id="f4a35-362">Tom Dykstra, Microsoft</span></span>](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a><span data-ttu-id="f4a35-363">커뮤니티 기여</span><span class="sxs-lookup"><span data-stu-id="f4a35-363">Community Contributions</span></span>

- <span data-ttu-id="f4a35-364">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span><span class="sxs-lookup"><span data-stu-id="f4a35-364">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span></span>  
  <span data-ttu-id="f4a35-365">MSDN의 visual Studio 2012 관련된 코드 샘플: [탐색: Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span><span class="sxs-lookup"><span data-stu-id="f4a35-365">Visual Studio 2012 related code sample on MSDN: [Navigation Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span></span>
- <span data-ttu-id="f4a35-366">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span><span class="sxs-lookup"><span data-stu-id="f4a35-366">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span></span>  
  <span data-ttu-id="f4a35-367">MSDN의 visual Studio 2012 관련된 코드 샘플: [Visual Basic에서는 ASP.NET 4.5 Web Forms 자습서 시리즈](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span><span class="sxs-lookup"><span data-stu-id="f4a35-367">Visual Studio 2012 related code sample on MSDN: [ASP.NET 4.5 Web Forms Tutorial Series in Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span></span>
- <span data-ttu-id="f4a35-368">Andrielle Azevedo-Microsoft 기술 대상 참가자 (twitter: @driazevedo)</span><span class="sxs-lookup"><span data-stu-id="f4a35-368">Andrielle Azevedo - Microsoft Technical Audience Contributor (twitter: @driazevedo)</span></span>  
  <span data-ttu-id="f4a35-369">Visual Studio 2012 translation: [Iniciando com ASP.NET Web Forms 4.5-Parte 1-e Visão Introdução 템플릿 Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span><span class="sxs-lookup"><span data-stu-id="f4a35-369">Visual Studio 2012 translation: [Iniciando com ASP.NET Web Forms 4.5 - Parte 1 - Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f4a35-370">이전</span><span class="sxs-lookup"><span data-stu-id="f4a35-370">Previous</span></span>](url-routing.md)
