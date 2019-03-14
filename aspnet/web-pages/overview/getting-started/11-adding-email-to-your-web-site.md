---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: (Razor) 사이트 페이지는 Asp.net에서 전자 메일 보내기 | Microsoft Docs
author: Rick-Anderson
description: 이 웹 사이트에서 자동화 된 전자 메일 메시지를 전송 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: f388ac1a97bde39cffe6b592b436d7af0d419a5f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038400"
---
<a name="sending-email-from-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="c107b-103">ASP.NET 웹 페이지 (Razor) 사이트에서 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="c107b-103">Sending Email from an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="c107b-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c107b-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c107b-105">이 문서에서는 ASP.NET Web Pages (Razor)를 사용 하는 경우 웹 사이트에서 전자 메일 메시지를 전송 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-105">This article explains how to send an email message from a website when you use ASP.NET Web Pages (Razor).</span></span>
> 
> <span data-ttu-id="c107b-106">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="c107b-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="c107b-107">웹 사이트에서 전자 메일 메시지를 보내는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-107">How to send an email message from your website.</span></span>
> - <span data-ttu-id="c107b-108">전자 메일 메시지에 파일을 첨부 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="c107b-108">How to attach a file to an email message.</span></span>
> 
> <span data-ttu-id="c107b-109">문서에 도입 된 ASP.NET 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-109">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="c107b-110">`WebMail` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-110">The `WebMail` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c107b-111">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="c107b-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c107b-112">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="c107b-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="c107b-113">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a><span data-ttu-id="c107b-114">웹 사이트에서 전자 메일 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="c107b-114">Sending Email Messages from Your Website</span></span>

<span data-ttu-id="c107b-115">모든 종류의 웹 사이트에서 전자 메일을 전송 해야 하는 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-115">There are all sorts of reasons why you might need to send email from your website.</span></span> <span data-ttu-id="c107b-116">사용자에 게 확인 메시지를 보낼 수 있습니다 (예를 들어 새 사용자를 등록 합니다.) 자신에 게 알림을 보낼 수 있습니다 또는 `WebMail` 도우미를 사용 하면 쉽게 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-116">You might send confirmation messages to users, or you might send notifications to yourself (for example, that a new user has registered.) The `WebMail` helper makes it easy for you to send email.</span></span>

<span data-ttu-id="c107b-117">사용 하는 `WebMail` 도우미, SMTP 서버에 액세스할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-117">To use the `WebMail` helper, you have to have access to an SMTP server.</span></span> <span data-ttu-id="c107b-118">(SMTP에 대 한 의미 *Simple Mail Transfer Protocol*.) SMTP 서버에만 받는 사람의 서버로 메시지를 전달 하는 전자 메일 서버는 &#8212; 전자 메일의 아웃 바운드 측 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-118">(SMTP stands for *Simple Mail Transfer Protocol*.) An SMTP server is an email server that only forwards messages to the recipient's server &#8212; it's the outbound side of email.</span></span> <span data-ttu-id="c107b-119">웹 사이트에 대 한 호스팅 공급자를 사용 하는 경우는 아마도 설정 전자 메일을 사용 하 여 및 SMTP 서버 이름 이란 알 수 있습니다 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-119">If you use a hosting provider for your website, they probably set you up with email and they can tell you what your SMTP server name is.</span></span> <span data-ttu-id="c107b-120">회사 네트워크 내에서 작업 하는 경우 관리자 또는 IT 부서 수 일반적으로 정보를 제공 사용할 수 있는 SMTP 서버에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-120">If you're working inside a corporate network, an administrator or your IT department can usually give you the information about an SMTP server that you can use.</span></span> <span data-ttu-id="c107b-121">집으로 작업 하는 경우 해당 SMTP 서버의 이름을 알 수 있는 일반 전자 메일 공급자를 사용 하 여 테스트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-121">If you're working at home, you might even be able to test using your ordinary email provider, who can tell you the name of their SMTP server.</span></span> <span data-ttu-id="c107b-122">일반적으로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-122">You typically need:</span></span>

- <span data-ttu-id="c107b-123">SMTP 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-123">The name of the SMTP server.</span></span>
- <span data-ttu-id="c107b-124">포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-124">The port number.</span></span> <span data-ttu-id="c107b-125">이 거의 항상 25입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-125">This is almost always 25.</span></span> <span data-ttu-id="c107b-126">그러나 ISP 포트 587을 사용 하 여 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-126">However, your ISP may require you to use port 587.</span></span> <span data-ttu-id="c107b-127">보안 소켓 레이어 (SSL) 전자 메일을 사용 하는 경우 다른 포트를 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-127">If you are using secure sockets layer (SSL) for email, you might need a different port.</span></span> <span data-ttu-id="c107b-128">전자 메일 공급자를 사용 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-128">Check with your email provider.</span></span>
- <span data-ttu-id="c107b-129">자격 증명 (사용자 이름, 암호)입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-129">Credentials (user name, password).</span></span>

<span data-ttu-id="c107b-130">이 절차에서는 두 개의 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-130">In this procedure, you create two pages.</span></span> <span data-ttu-id="c107b-131">첫 번째 페이지에 기술 지원 양식에 입력 된 것 처럼 설명을 입력 하는 사용자가 수 있는 양식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-131">The first page has a form that lets users enter a description, as if they were filling in a technical-support form.</span></span> <span data-ttu-id="c107b-132">첫 번째 페이지는 두 번째 페이지에 해당 정보를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-132">The first page submits its information to a second page.</span></span> <span data-ttu-id="c107b-133">두 번째 페이지에서 코드는 사용자의 정보를 추출 하 고 전자 메일 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-133">In the second page, code extracts the user's information and sends an email message.</span></span> <span data-ttu-id="c107b-134">또한 문제 보고서를 받았는지 확인 하는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-134">It also displays a message confirming that the problem report has been received.</span></span>

![[image]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> <span data-ttu-id="c107b-136">코드를 간단히 유지 하기 위해이 예제에서는 다음을 초기화 합니다.는 `WebMail` 사용할 위치 페이지에서 오른쪽 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-136">To keep this example simple, the code initializes the `WebMail` helper right in the page where you use it.</span></span> <span data-ttu-id="c107b-137">그러나 실제 웹 사이트에 대 한 것을 전역 파일에 다음과 같은 초기화 코드를 저장 하는 것이 좋습니다 초기화할 수 있도록는 `WebMail` 웹 사이트의 모든 파일에 대 한 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-137">However, for real websites, it's a better idea to put initialization code like this in a global file, so that you initialize the `WebMail` helper for all files in your website.</span></span> <span data-ttu-id="c107b-138">자세한 내용은 [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-138">For more information, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers).</span></span>


1. <span data-ttu-id="c107b-139">새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-139">Create a new website.</span></span>
2. <span data-ttu-id="c107b-140">명명 된 새 페이지 추가 *EmailRequest.cshtml* 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-140">Add a new page named *EmailRequest.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    <span data-ttu-id="c107b-141">다음에 유의 합니다 `action` 폼 요소의 특성으로 설정 되었습니다 *ProcessRequest.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-141">Notice that the `action` attribute of the form element has been set to *ProcessRequest.cshtml*.</span></span> <span data-ttu-id="c107b-142">이 폼 현재 페이지로 대신 해당 페이지로 제출할 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-142">This means that the form will be submitted to that page instead of back to the current page.</span></span>
3. <span data-ttu-id="c107b-143">라는 새 페이지 추가 *ProcessRequest.cshtml* 웹 사이트에 다음 코드와 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-143">Add a new page named *ProcessRequest.cshtml* to the website and add the following code and markup:</span></span>   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    <span data-ttu-id="c107b-144">코드 페이지에 제출 된 폼 필드의 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-144">In the code, you get the values of the form fields that were submitted to the page.</span></span> <span data-ttu-id="c107b-145">다음 호출을 `WebMail` 도우미의 `Send` 만들고 전자 메일 메시지를 전송 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="c107b-145">You then call the `WebMail` helper's `Send` method to create and send the email message.</span></span> <span data-ttu-id="c107b-146">이 경우 값을 사용 하 여 폼에서 전송 된 값을 사용 하 여 연결 하는 텍스트의 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-146">In this case, the values to use are made up of text that you concatenate with the values that were submitted from the form.</span></span>

    <span data-ttu-id="c107b-147">이 페이지에 대 한 코드 내에 `try/catch` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-147">The code for this page is inside a `try/catch` block.</span></span> <span data-ttu-id="c107b-148">전자 메일 보내기 위해 어떤 이유로 소용이 없으면 (예를 들어 설정을 오른쪽)가 아닌의 코드를 `catch` 블록이 실행 되 고 설정는 `errorMessage` 변수 발생 한 오류를 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-148">If for any reason the attempt to send an email doesn't work (for example, the settings aren't right), the code in the `catch` block runs and sets the `errorMessage` variable to the error that has occurred.</span></span> <span data-ttu-id="c107b-149">(에 대 한 자세한 내용은 `try/catch` 블록 또는 `<text>` 태그를 참조 하십시오 [ASP.NET 웹 페이지 Razor 구문으로 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)</span><span class="sxs-lookup"><span data-stu-id="c107b-149">(For more information about `try/catch` blocks or the `<text>` tag, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)</span></span>

    <span data-ttu-id="c107b-150">페이지 본문의 경우는 `errorMessage` 변수가 비어 (기본값), 사용자에 게 전자 메일 메시지가 전송 된 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-150">In the body of the page, if the `errorMessage` variable is empty (the default), the user sees a message that the email message has been sent.</span></span> <span data-ttu-id="c107b-151">경우는 `errorMessage` 변수 메시지를 보내는 문제가 되었는지 하는 메시지를 사용자에 게 표시 되는 true로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-151">If the `errorMessage` variable is set to true, the user sees a message that there's been a problem sending the message.</span></span>

    <span data-ttu-id="c107b-152">오류 메시지가 표시 된 페이지 부분에는 추가 테스트: `if(debuggingFlag)`합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-152">Notice that in the portion of the page that displays an error message, there's an additional test: `if(debuggingFlag)`.</span></span> <span data-ttu-id="c107b-153">이 전자 메일을 전송 하는 데 문제가 있는 경우 true로 설정할 수 있는 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-153">This is a variable that you can set to true if you're having trouble sending email.</span></span> <span data-ttu-id="c107b-154">때 `debuggingFlag` 가 true 이면 추가 오류 메시지를 ASP.NET에서 전자 메일 메시지를 전송 하려고 할 때 보고 항목을 보여 주는 표시는 전자 메일을 보내는 데 문제가 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-154">When `debuggingFlag` is true, and if there's a problem sending email, an additional error message is displayed that shows whatever ASP.NET has reported when it tried to send the email message.</span></span> <span data-ttu-id="c107b-155">그러나 상당한 경고,: 전자 메일 메시지를 보낼 수 없는 경우 ASP.NET에서 보고 하는 오류 메시지는 제네릭이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-155">Fair warning, though: the error messages that ASP.NET reports when it can't send an email message can be generic.</span></span> <span data-ttu-id="c107b-156">예를 들어 경우 (예를 들어 있으므로 오류가 서버 이름에 대 한) ASP.NET SMTP 서버에 연결할 수 없습니다, 오류는 `Failure sending mail`합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-156">For example, if ASP.NET can't contact the SMTP server (for example, because you made an error in the server name), the error is `Failure sending mail`.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="c107b-157">**중요** 예외 개체에서 오류 메시지를 가져올 때 (`ex` 코드에서)를 수행 *하지* 정기적으로 사용자를 통해 해당 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-157">**Important** When you get an error message from an exception object (`ex` in the code), do *not* routinely pass that message through to users.</span></span> <span data-ttu-id="c107b-158">예외 개체에는 사용자가 표시 되지 않습니다 하 고 보안 취약성도 될 수 있는 정보가 종종 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-158">Exception objects often include information that users should not see and that can even be a security vulnerability.</span></span> <span data-ttu-id="c107b-159">때문에 변수를 포함 하는이 코드 `debuggingFlag` 오류 메시지를 표시 하는 스위치와 사용 되는 및 기본적으로 변수가 false로 설정 하는 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-159">That's why this code includes the variable `debuggingFlag` that's used as a switch to display the error message, and why the variable by default is set to false.</span></span> <span data-ttu-id="c107b-160">변수를 true (및 따라서 오류 메시지 표시)로 설정 해야 *만* 메일을 보내는 중에 문제가 발생 하면 디버깅 해야 할 경우.</span><span class="sxs-lookup"><span data-stu-id="c107b-160">You should set that variable to true (and therefore display the error message) *only* if you're having a problem with sending email and you need to debug.</span></span> <span data-ttu-id="c107b-161">문제를 해결 한 후 설정 `debuggingFlag` false 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-161">Once you have fixed any problems, set `debuggingFlag` back to false.</span></span>

    <span data-ttu-id="c107b-162">수정 다음 코드에서 관련 된 설정 전자 메일:</span><span class="sxs-lookup"><span data-stu-id="c107b-162">Modify the following email related settings in the code:</span></span>

   - <span data-ttu-id="c107b-163">설정 `your-SMTP-host` 에 대 한 액세스를 해야 하는 SMTP 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-163">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
   - <span data-ttu-id="c107b-164">설정 `your-user-name-here` SMTP 서버 계정의 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-164">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
   - <span data-ttu-id="c107b-165">설정 `your-account-password` SMTP 서버 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-165">Set `your-account-password` to the password for your SMTP server account.</span></span>
   - <span data-ttu-id="c107b-166">설정 `your-email-address-here` 고유한 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-166">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="c107b-167">이 메시지에서 전송 되는 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-167">This is the email address that the message is sent from.</span></span> <span data-ttu-id="c107b-168">(일부 전자 메일 공급자를 사용 하면 다른 지정할 수 없습니다 `From` 해결 하 고 사용자 이름으로 사용 합니다 `From` 주소입니다.)</span><span class="sxs-lookup"><span data-stu-id="c107b-168">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a><span data-ttu-id="c107b-169">전자 메일 설정 구성</span><span class="sxs-lookup"><span data-stu-id="c107b-169">Configuring Email Settings</span></span>
     > 
     > <span data-ttu-id="c107b-170">SMTP 서버, 포트 번호 및 등의 올바른 설정을 했는지 확인 하는 경우에 따라 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-170">It can be a challenge sometimes to make sure you have the right settings for the SMTP server, port number, and so on.</span></span> <span data-ttu-id="c107b-171">다음은 이에 대한 몇 가지 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-171">Here are a few tips:</span></span>
     > 
     > - <span data-ttu-id="c107b-172">SMTP 서버 이름을 같습니다 종종 `smtp.provider.com` 또는 `smtp.provider.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-172">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="c107b-173">그러나 사이트를 호스팅 공급자에 게시할 경우 SMTP 서버 이름을 이때 않을 `localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-173">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="c107b-174">이것이 게시 한 후 사이트 공급자의 서버에서 실행 되는 전자 메일 서버 응용 프로그램의 관점에서 로컬 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-174">This is because after you've published and your site is running on the provider's server, the email server might be local from the perspective of your application.</span></span> <span data-ttu-id="c107b-175">서버 이름에서이 변경 내용을 게시 하는 과정의 일부로 SMTP 서버 이름을 변경 해야 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-175">This change in server names might mean you have to change the SMTP server name as part of your publishing process.</span></span>
     > - <span data-ttu-id="c107b-176">포트 번호는 일반적으로 25입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-176">The port number is usually 25.</span></span> <span data-ttu-id="c107b-177">그러나 일부 공급자 포트를 사용 하 여 587 또는 일부 다른 포트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-177">However, some providers require you to use port 587 or some other port.</span></span>
     > - <span data-ttu-id="c107b-178">올바른 자격 증명을 사용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-178">Make sure that you use the right credentials.</span></span> <span data-ttu-id="c107b-179">사이트를 호스팅 공급자을 게시 하는 경우 특별히 설정 된 공급자가 전자 메일에 대 한 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-179">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="c107b-180">이러한 게시할 사용 자격 증명과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-180">These might be different from the credentials you use to publish.</span></span>
     > - <span data-ttu-id="c107b-181">경우에 따라 전혀 자격 증명이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-181">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="c107b-182">개인 ISP를 사용 하 여 메일을 보내는 경우 전자 메일 공급자 자격 증명 이미 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-182">If you're sending email using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="c107b-183">를 게시 한 후에 로컬 컴퓨터에 테스트 하는 경우 다른 자격 증명을 사용 하는 것이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-183">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
     > - <span data-ttu-id="c107b-184">설정 해야 하는 전자 메일 공급자에서 암호화를 사용 하는 경우 `WebMail.EnableSsl` 에 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-184">If your email provider uses encryption, you have to set `WebMail.EnableSsl` to `true`.</span></span>
4. <span data-ttu-id="c107b-185">실행 합니다 *EmailRequest.cshtml* 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-185">Run the *EmailRequest.cshtml* page in a browser.</span></span> <span data-ttu-id="c107b-186">(페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.)</span><span class="sxs-lookup"><span data-stu-id="c107b-186">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
5. <span data-ttu-id="c107b-187">사용자 이름 및 문제 설명, 입력 한 다음 클릭 합니다 **제출** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-187">Enter your name and a problem description, and then click the **Submit** button.</span></span> <span data-ttu-id="c107b-188">로 리디렉션됩니다 합니다 *ProcessRequest.cshtml* 페이지에서 메시지를 확인 하 고 전자 메일 메시지를 보냅니다는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-188">You're redirected to the *ProcessRequest.cshtml* page, which confirms your message and which sends you an email message.</span></span> 

    ![[image]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a><span data-ttu-id="c107b-190">전자 메일을 사용 하 여 파일 전송</span><span class="sxs-lookup"><span data-stu-id="c107b-190">Sending a File Using Email</span></span>

<span data-ttu-id="c107b-191">또한 전자 메일 메시지에 연결 된 파일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-191">You can also send files that are attached to email messages.</span></span> <span data-ttu-id="c107b-192">이 절차에서는 텍스트 파일 및 두 개의 HTML 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-192">In this procedure, you create a text file and two HTML pages.</span></span> <span data-ttu-id="c107b-193">텍스트 파일을 메일 첨부 파일로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-193">You'll use the text file as an email attachment.</span></span>

1. <span data-ttu-id="c107b-194">웹 사이트에서 새 텍스트 파일을 추가 하 고 이름을 *MyFile.txt*합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-194">In the website, add a new text file and name it *MyFile.txt*.</span></span>
2. <span data-ttu-id="c107b-195">다음 텍스트를 복사 하 고 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-195">Copy the following text and paste it in the file:</span></span> 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. <span data-ttu-id="c107b-196">라는 페이지를 만듭니다 *SendFile.cshtml* 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-196">Create a page named *SendFile.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. <span data-ttu-id="c107b-197">라는 페이지를 만듭니다 *ProcessFile.cshtml* 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-197">Create a page named *ProcessFile.cshtml* and add the following markup:</span></span> 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. <span data-ttu-id="c107b-198">수정 다음 전자 메일의 예제에서 코드에서 관련된 설정:</span><span class="sxs-lookup"><span data-stu-id="c107b-198">Modify the following email related settings in the code from the example:</span></span>

    - <span data-ttu-id="c107b-199">설정 `your-SMTP-host` 에 대 한 액세스를 해야 하는 SMTP 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-199">Set `your-SMTP-host` to the name of an SMTP server that you have access to.</span></span>
    - <span data-ttu-id="c107b-200">설정 `your-user-name-here` SMTP 서버 계정의 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-200">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
    - <span data-ttu-id="c107b-201">설정 `your-email-address-here` 고유한 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-201">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="c107b-202">이 메시지에서 전송 되는 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-202">This is the email address that the message is sent from.</span></span>
    - <span data-ttu-id="c107b-203">설정 `your-account-password` SMTP 서버 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-203">Set `your-account-password` to the password for your SMTP server account.</span></span>
    - <span data-ttu-id="c107b-204">설정 `target-email-address-here` 고유한 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-204">Set `target-email-address-here` to your own email address.</span></span> <span data-ttu-id="c107b-205">(이전에 일반적으로 보내 처럼 전자 메일이 다른 사용자에 게 있지만 테스트용, 있습니다 수 자신에 게 보냅니다.)</span><span class="sxs-lookup"><span data-stu-id="c107b-205">(As before, you'd normally send an email to someone else, but for testing, you can send it to yourself.)</span></span>
6. <span data-ttu-id="c107b-206">실행 합니다 *SendFile.cshtml* 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-206">Run the *SendFile.cshtml* page in a browser.</span></span>
7. <span data-ttu-id="c107b-207">사용자 이름, 제목 줄, 및 연결할 텍스트 파일의 이름을 입력 (*MyFile.txt*).</span><span class="sxs-lookup"><span data-stu-id="c107b-207">Enter your name, a subject line, and the name of the text file to attach (*MyFile.txt*).</span></span>
8. <span data-ttu-id="c107b-208">`Submit` 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-208">Click the `Submit` button.</span></span> <span data-ttu-id="c107b-209">으로 리디렉션됩니다 앞으로 *ProcessFile.cshtml* 페이지에서 메시지를 확인 하 고는 보내는 전자 메일 메시지 첨부 파일을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c107b-209">As before, you're redirected to the *ProcessFile.cshtml* page, which confirms your message and which sends you an email message with the attached file.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="c107b-210">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c107b-210">Additional Resources</span></span>


- [<span data-ttu-id="c107b-211">ASP.NET 웹 페이지(Razor) 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="c107b-211">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)
- [<span data-ttu-id="c107b-212">Simple Mail Transfer Protocol</span><span class="sxs-lookup"><span data-stu-id="c107b-212">Simple Mail Transfer Protocol</span></span>](https://msdn.microsoft.com/library/aa480435.aspx)
- [<span data-ttu-id="c107b-213">ASP.NET 웹 페이지에 대 한 사이트 전체 동작을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="c107b-213">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)