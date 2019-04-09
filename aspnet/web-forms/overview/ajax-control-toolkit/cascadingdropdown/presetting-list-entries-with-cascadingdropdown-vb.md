---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: CascadingDropDown (VB)를 사용 하 여 목록 항목 미리 설정 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 6e685d599e3dbc095631e3c28a603ac9c38f799c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59385893"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a><span data-ttu-id="0691a-103">CascadingDropDown으로 목록 항목 미리 설정(VB)</span><span class="sxs-lookup"><span data-stu-id="0691a-103">Presetting List Entries with CascadingDropDown (VB)</span></span>

<span data-ttu-id="0691a-104">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="0691a-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="0691a-105">[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="0691a-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span></span>

> <span data-ttu-id="0691a-106">AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0691a-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="0691a-107">약간의 코드를 사용 하 여 데이터를 동적으로 로드 되 면 목록 요소는 미리 선택 가능한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0691a-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>


## <a name="overview"></a><span data-ttu-id="0691a-108">개요</span><span class="sxs-lookup"><span data-stu-id="0691a-108">Overview</span></span>

<span data-ttu-id="0691a-109">AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0691a-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="0691a-110">(예를 들어 미국 주 목록을 제공 하는 하나의 목록 및 해당 상태의 주요 도시를 사용 하 여 다음 목록에 다음 채워집니다.) 약간의 코드를 사용 하 여 데이터를 동적으로 로드 되 면 목록 요소는 미리 선택 가능한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0691a-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="0691a-111">단계</span><span class="sxs-lookup"><span data-stu-id="0691a-111">Steps</span></span>

<span data-ttu-id="0691a-112">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="0691a-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="0691a-113">DropDownList 컨트롤은 그런 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0691a-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="0691a-114">이 목록에 대 한 웹 서비스 URL 및 메서드 정보를 제공 하는 CascadingDropDown extender 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0691a-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="0691a-115">CascadingDropDown extender 비동기적으로 호출 된 다음 메서드 시그니처를 사용 하 여 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="0691a-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="0691a-116">메서드는 CascadingDropDown 값 형식의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0691a-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="0691a-117">목록 항목의 캡션 및 값 형식의 생성자에 먼저 인수가 (HTML `value` 특성).</span><span class="sxs-lookup"><span data-stu-id="0691a-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="0691a-118">세 번째 인수를 설정 하는 경우 true, 목록에 요소가 자동으로 선택 됩니다 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0691a-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="0691a-119">브라우저에서 페이지 로드 입력 3 개 공급 업체를 사용 하 여 드롭다운 목록 미리 선택 되 고 두 번째 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0691a-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>


[![T<span data-ttu-id="0691a-120">그 목록 채우기 및 자동으로 미리 선택]</span><span class="sxs-lookup"><span data-stu-id="0691a-120">he list is filled and preselected automatically]</span></span>(presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)

<span data-ttu-id="0691a-121">목록 채우기 및 자동으로 미리 선택 ([클릭 하 여 큰 이미지 보기](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="0691a-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0691a-122">[이전](using-cascadingdropdown-with-a-database-vb.md)
> [다음](using-auto-postback-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="0691a-122">[Previous](using-cascadingdropdown-with-a-database-vb.md)
[Next](using-auto-postback-with-cascadingdropdown-vb.md)</span></span>
