---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: 봇이 ASP.NET 웹 면도기) 사이트를 사용하지 못하도록 CAPTCHA를 사용하는 경우 | 마이크로 소프트 문서
author: rick-anderson
description: 이 문서에서는 ReCaptcha (보안 조치)를 사용하여 자동화 된 프로그램 (봇)이 ASP.NET 웹 페이지 (Razor)에서 작업을 수행하지 못하도록하는 방법에 대해 설명합니다...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543758"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>CAPTCHA를 사용하여 봇이 ASP.NET 웹 면도기) 사이트를 사용하지 못하도록 방지

[로 마이크로 소프트](https://github.com/microsoft)

> 이 문서에서는 ReCaptcha(보안 조치)를 사용하여 자동화된 프로그램(봇)이 ASP.NET 웹 페이지(Razor) 웹 사이트에서 작업을 수행하지 못하도록 하는 방법을 설명합니다.
> 
> **학습할 내용:** 
> 
> - 사이트에 CAPTCHA 테스트를 추가하는 방법.
> 
> 다음은 이 문서에 소개된 ASP.NET 기능입니다.
> 
> - `ReCaptcha` 도우미입니다.
> 
> > [!NOTE]
> > 이 문서의 정보는 웹 페이지 1.0 및 웹 페이지 2ASP.NET 에 적용됩니다.

## <a name="about-captchas"></a>캡카에 대해

사람들이 사이트에 등록하도록 허용하거나 이름과 URL(예: 블로그 댓글)을 입력하면 가짜 이름이 넘쳐나실 수 있습니다. 이러한 URL은 종종 그들이 찾을 수 있는 모든 웹사이트에 URL을 남기려는 자동화된 프로그램(봇)에 의해 남습니다. (일반적인 동기는 판매용 제품의 URL을 게시하는 것입니다.)

사용자가 등록할 때 사용자의 유효성을 검사하기 위해 *CAPTCHA를* 사용하거나 이름과 사이트를 입력할 때 컴퓨터 프로그램이 아닌 실제 사용자인지 확인할 수 있습니다. CAPTCHA는 컴퓨터와 인간을 구분하기 위해 완전히 자동화 된 공공 튜링 테스트를 의미합니다. CAPTCHA는 사용자가 쉽게 할 수 있지만 자동화된 프로그램이 수행하는 데 어려운 작업을 수행하도록 요청하는 *챌린지 응답* 테스트입니다. CAPTCHA의 가장 일반적인 유형은 일부 왜곡된 문자를 보고 입력하라는 메시지가 표시되는 문자입니다. (왜곡은 봇이 문자를 해독하기 어렵게 만들어야 합니다.)

## <a name="adding-a-recaptcha-test"></a>ReCaptcha 테스트 추가

ASP.NET 페이지에서 는 도우미를 `ReCaptcha` 사용하여 ReCaptcha 서비스()를[http://recaptcha.net](http://recaptcha.net)기반으로 하는 CAPTCHA 테스트를 렌더링할 수 있습니다. 도우미는 `ReCaptcha` 페이지의 유효성을 검사하기 전에 사용자가 올바르게 입력해야 하는 왜곡된 두 단어의 이미지를 표시합니다. 사용자 응답은 ReCaptcha.Net 서비스에 의해 유효성을 검사합니다.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. ReCaptcha.Net ()에[http://recaptcha.net](http://recaptcha.net)웹 사이트를 등록합니다. 등록을 완료하면 공개 키와 개인 키를 받게 됩니다.
2. [ASP.NET 웹 페이지 사이트에 도우미 설치에](https://go.microsoft.com/fwlink/?LinkId=252372)설명된 대로 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가합니다.
3. * \_아직 AppStart.cshtml* 파일이 없는 경우 웹 사이트의 루트 폴더에 * \_AppStart.cshtml이라는*파일을 만듭니다.
4. AppStart.cshtml 파일에 다음 `Recaptcha` 도우미 설정을 추가합니다. * \_* 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. 사용자 `PublicKey` 고유의 공개 및 개인 키를 사용하여 및 `PrivateKey` 속성을 설정합니다.
6. AppStart.cshtml 파일을 저장하고 닫습니다. * \_*
7. 웹 사이트의 루트 폴더에서 *Recaptcha.cshtml이라는*새 페이지를 만듭니다.
8. 기존 콘텐츠를 다음 내용으로 바꿉꿉입니다. 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. 브라우저에서 *Recaptcha.cshtml* 페이지를 실행합니다. `PrivateKey` 값이 유효한 경우 페이지에 ReCaptcha 컨트롤과 버튼이 표시됩니다. * \_AppStart.html에서*키를 전역적으로 설정하지 않은 경우 페이지에 오류가 표시됩니다. 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. 테스트에 대한 단어를 입력합니다. ReCaptcha 테스트를 통과하면 해당 효과에 대한 메시지가 표시됩니다. 그렇지 않으면 오류 메시지가 표시되고 ReCaptcha 컨트롤이 다시 표시됩니다.

> [!NOTE]
> 컴퓨터가 프록시 서버를 사용하는 도메인에 있는 경우 `defaultproxy` *Web.config* 파일의 요소를 구성해야 할 수 있습니다. 다음 예제에서는 ReCaptcha 서비스가 작동하도록 구성된 `defaultproxy` 요소가 있는 *Web.config* 파일을 보여 주며 있습니다.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [ASP.NET 웹 페이지 사이트에 대한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
- [리캡차 사이트](https://www.google.com/recaptcha)
