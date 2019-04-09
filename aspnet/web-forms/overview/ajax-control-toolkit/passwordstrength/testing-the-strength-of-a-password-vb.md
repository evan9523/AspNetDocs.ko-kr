---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: (VB) 암호 강도 테스트 | Microsoft Docs
author: wenz
description: 암호는 지연 사용자 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있습니다 있도록 거의 모든 곳에서 필요 합니다. ASP에서 PasswordStrength 컨트롤입니다. N....
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: fb185c4147d516ab28d632b3e874b6f1d46f6576
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59408422"
---
# <a name="testing-the-strength-of-a-password-vb"></a><span data-ttu-id="1e100-104">암호 강도 테스트(VB)</span><span class="sxs-lookup"><span data-stu-id="1e100-104">Testing the Strength of a Password (VB)</span></span>

<span data-ttu-id="1e100-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1e100-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1e100-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="1e100-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span></span>

> <span data-ttu-id="1e100-107">암호는 지연 사용자 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있습니다 있도록 거의 모든 곳에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e100-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="1e100-108">ASP.NET AJAX Control Toolkit에서 PasswordStrength 컨트롤 성이나 암호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e100-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>


## <a name="overview"></a><span data-ttu-id="1e100-109">개요</span><span class="sxs-lookup"><span data-stu-id="1e100-109">Overview</span></span>

<span data-ttu-id="1e100-110">암호는 지연 사용자 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있습니다 있도록 거의 모든 곳에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e100-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="1e100-111">`PasswordStrength` ASP.NET AJAX Control Toolkit 컨트롤 성이나 암호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e100-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="1e100-112">단계</span><span class="sxs-lookup"><span data-stu-id="1e100-112">Steps</span></span>

<span data-ttu-id="1e100-113">`PasswordStrength` 컨트롤 텍스트 상자를 확장 하 고 그 안에 암호 충분 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e100-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="1e100-114">다양 한 특성을 통해 옵션 제공 그 중 일부가 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e100-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- `MinimumNumericCharacters` <span data-ttu-id="1e100-115">암호에 필요한 숫자 문자의 최소 개수</span><span class="sxs-lookup"><span data-stu-id="1e100-115">minimum number of numeric characters required in the password</span></span>
- `MinimumSymbolCharacters` <span data-ttu-id="1e100-116">암호에 필요한 기호 문자 (없습니다 문자 및 숫자)의 최소 수</span><span class="sxs-lookup"><span data-stu-id="1e100-116">minimum number of symbol characters (not letters and digits) required in the password</span></span>
- `PreferredPasswordLength` <span data-ttu-id="1e100-117">암호의 최소 길이</span><span class="sxs-lookup"><span data-stu-id="1e100-117">minimum length of the password</span></span>
- `RequiresUpperAndLowerCaseCharacters` <span data-ttu-id="1e100-118">암호를 대 / 소문자를 사용 해야 하는 여부</span><span class="sxs-lookup"><span data-stu-id="1e100-118">whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="1e100-119">합니다 `StrengthIndicatorType` 텍스트로, 암호의 강도 표시 하는 방법을 설명 (값 `"Text"`) 또는 진행률 표시줄의 종류 (값 `"BarIndicator"`).</span><span class="sxs-lookup"><span data-stu-id="1e100-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="1e100-120">에 `DisplayPosition` 특성을 구성한 위치 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e100-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="1e100-121">ASP.NET AJAX를 포함 한 전체 예제를 다음과 같습니다 `ScriptManager` 컨트롤은 `PasswordStrength` 컨트롤과 물론 사용자 암호를 입력할 수 있는 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="1e100-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="1e100-122">데모를 위해 두 번째 폼 필드 입력 내용을 개발 하는 동안 볼 수 있도록 일반 텍스트 필드 및 암호 필드가 아닙니다입니다.</span><span class="sxs-lookup"><span data-stu-id="1e100-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

<span data-ttu-id="1e100-123">페이지 실행 한 번 입력 합니다. 소문자, 대문자, 숫자 및 기호를 입력 한 후에 암호 unbreakable으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e100-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>


[![N<span data-ttu-id="1e100-124">ow 암호 양호 (매우)]</span><span class="sxs-lookup"><span data-stu-id="1e100-124">ow the password is (quite) good]</span></span>(testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)

<span data-ttu-id="1e100-125">이제 암호 () 활동적 ([클릭 하 여 큰 이미지 보기](testing-the-strength-of-a-password-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1e100-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1e100-126">이전</span><span class="sxs-lookup"><span data-stu-id="1e100-126">Previous</span></span>](testing-the-strength-of-a-password-cs.md)
