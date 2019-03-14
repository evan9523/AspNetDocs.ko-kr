---
ms.openlocfilehash: 83a958fe6a8d61becf9f9062e8ad0ff69108b435
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034990"
---
<a name="jquery-validation-pluginhttpjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="bd212-101">[jQuery 유효성 검사 플러그 인](http://jqueryvalidation.org/) - 유효성 검사를 쉽게 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-101">[jQuery Validation Plugin](http://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="bd212-102">[![빌드 상태](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency 상태](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="bd212-102">[![Build Status](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency Status](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="bd212-103">jQuery 유효성 검사 플러그 인은 애플리케이션에 맞는 모든 종류의 사용자 지정을 쉽게 만들도록 하면서 기존 폼에 대한 드롭인 유효성 검사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[<span data-ttu-id="bd212-104">프로젝트 지원</span><span class="sxs-lookup"><span data-stu-id="bd212-104">Help the project</span></span>](http://pledgie.com/campaigns/18159)

<span data-ttu-id="bd212-105">[![프로젝트 지원](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span><span class="sxs-lookup"><span data-stu-id="bd212-105">[![Help the project](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="bd212-106">이 프로젝트는 지원을 기다리고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-106">This project is looking for help!</span></span> <span data-ttu-id="bd212-107">[진행 중인 pledgie 캠페인에 기부하고](http://pledgie.com/campaigns/18159) 캠페인 의도를 전달하는 데 도움을 주세요.</span><span class="sxs-lookup"><span data-stu-id="bd212-107">[You can donate to the ongoing pledgie campaign](http://pledgie.com/campaigns/18159) and help spread the word.</span></span> <span data-ttu-id="bd212-108">이 플러그 인을 사용해본 적이 있거나 사용할 계획인 경우 도움을 주실 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-108">If you've used the plugin, or plan to use, consider a donation - any amount will help.</span></span>

<span data-ttu-id="bd212-109">[pledgie 페이지](http://pledgie.com/campaigns/18159)에서 기부하는 방법에 대한 계획을 찾으실 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-109">You can find the plan for how to spend the money on the [pledgie page](http://pledgie.com/campaigns/18159).</span></span>

## <a name="getting-started"></a><span data-ttu-id="bd212-110">시작</span><span class="sxs-lookup"><span data-stu-id="bd212-110">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="bd212-111">사전 빌드된 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="bd212-111">Downloading the prebuilt files</span></span>

<span data-ttu-id="bd212-112">사전 빌드된 파일은 http://jqueryvalidation.org/에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-112">Prebuilt files can be downloaded from http://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="bd212-113">최신 변경 내용 다운로드</span><span class="sxs-lookup"><span data-stu-id="bd212-113">Downloading the latest changes</span></span>

<span data-ttu-id="bd212-114">릴리스되지 않은 개발 파일은 다음에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-114">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="bd212-115">이 리포지토리 [다운로드](https://github.com/jzaefferer/jquery-validation/archive/master.zip) 또는 포크</span><span class="sxs-lookup"><span data-stu-id="bd212-115">[Downloading](https://github.com/jzaefferer/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="bd212-116">빌드 설치</span><span class="sxs-lookup"><span data-stu-id="bd212-116">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="bd212-117">`grunt`를 실행하여 “dist” 디렉터리에 빌드된 파일 생성</span><span class="sxs-lookup"><span data-stu-id="bd212-117">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="bd212-118">페이지에 포함</span><span class="sxs-lookup"><span data-stu-id="bd212-118">Including it on your page</span></span>

<span data-ttu-id="bd212-119">페이지에 jQuery 및 플러그 인을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-119">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="bd212-120">그런 다음 유효성을 검사할 폼을 선택하고 `validate` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-120">Then select a form to validate and call the `validate` method.</span></span>

```html
<form>
    <input required>
</form>
<script src="jquery.js"></script>
<script src="jquery.validate.js"></script>
<script>
$("form").validate();
</script>
```

<span data-ttu-id="bd212-121">또는 requirejs를 통해 모듈에 jQuery 및 플러그 인을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-121">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="bd212-122">규칙 및 사용자 지정을 설정하는 방법에 대한 자세한 내용은 [설명서를 확인](http://jqueryvalidation.org/documentation/)하세요.</span><span class="sxs-lookup"><span data-stu-id="bd212-122">For more information on how to setup a rules and customizations, [check the documentation](http://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="bd212-123">문제 보고 및 코드 참여</span><span class="sxs-lookup"><span data-stu-id="bd212-123">Reporting issues and contributing code</span></span>

<span data-ttu-id="bd212-124">자세한 내용은 [참여 지침](CONTRIBUTING.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd212-124">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="bd212-125">**메일 유효성 검사에 대한 중요 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="bd212-125">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="bd212-126">버전 1.12.0에서 이 플러그 인은 [HTML5 사양이 브라우저에 사용하도록 제안](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)하는 동일한 정규식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-126">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="bd212-127">지침을 따르고 동일한 검사를 사용할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-127">We will follow their lead and use the same check.</span></span> <span data-ttu-id="bd212-128">사양이 잘못되었다고 생각되면 문제를 보고하세요.</span><span class="sxs-lookup"><span data-stu-id="bd212-128">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="bd212-129">다른 요구 사항이 있는 경우 [사용자 지정 메서드를 사용](http://jqueryvalidation.org/jQuery.validator.addMethod/)하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-129">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="license"></a><span data-ttu-id="bd212-130">라이선스</span><span class="sxs-lookup"><span data-stu-id="bd212-130">License</span></span>
<span data-ttu-id="bd212-131">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="bd212-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="bd212-132">MIT 라이선스에 따라 사용이 허가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd212-132">Licensed under the MIT license.</span></span>