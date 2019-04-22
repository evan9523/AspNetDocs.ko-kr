---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: CAPTCHA를 사용 하 여 Asp.net Razor를 사용 하 여 봇을 방지 하기 위해) 사이트 | Microsoft Docs
author: microsoft
description: 이 문서에서는 자동화 프로그램 (봇)에 ASP.NET Web Pages (Razor) 작업을 수행 하지 못하도록 ReCaptcha (보안을 위해) 사용 하는 방법에 설명 했습니다...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: e7baafda8c5b6de4ab0de46948f969a6f0cc21ad
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59390911"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>CAPTCHA를 사용 하 여 Asp.net Razor를 사용 하 여 봇을 방지 하기 위해) 사이트

by [Microsoft](https://github.com/microsoft)

> 이 문서에서는 자동화 프로그램 (봇)는 ASP.NET Web Pages (Razor) 웹 사이트에서 작업을 수행 하지 못하도록 ReCaptcha (보안을 위해) 사용 하는 방법에 설명 합니다.
> 
> **학습할 내용:** 
> 
> - CAPTCHA 테스트 사이트를 추가 하는 방법.
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `ReCaptcha` 도우미입니다.
> 
> > [!NOTE]
> > 이 문서의 정보는 ASP.NET 웹 페이지 1.0 및 웹 페이지 2에 적용 됩니다.


## <a name="about-captchas"></a>CAPTCHAs에 대 한

사이트에 또는 만으로도 사용자를 등록 하면 언제 든 지 이름과 URL (블로그 주석에 대 한 유사한)를 입력, 많은 양의 가짜 이름과 표시 될 수 있습니다. 이러한 Url을 찾을 수 있으며 모든 웹 사이트를 유지 하려고 하는 자동화 프로그램 (봇)에서 종종 남아 있습니다. (일반적인 동기는 제품 판매에 대 한 Url을 게시 합니다.)

사용자는 실제 사용자 및 컴퓨터 프로그램이 아니라 사용 하 여 만들 수 있습니다는 *CAPTCHA* 를 등록 하거나 그렇지 않은 경우 해당 이름 및 사이트를 입력 하는 경우 사용자의 유효성을 검사 합니다. 컴퓨터 및 사람이 분리 하기가 공용 Turing 완전히 자동화 된 테스트는 CAPTCHA를 나타냅니다. CAPTCHA를은 *challenge-response 방식의* 는 사용자 작업을 수행 하 라는 메시지가 표시 된 테스트를 위해 사용자에 대 한 간단 하지만 작업을 수행 하는 자동화 된 프로그램에 대 한 하드 합니다. CAPTCHA의 가장 일반적인 종류는 일부 왜곡 된 문자를 참조 하 고를 입력 하 라는 메시지가 표시 됩니다. (왜곡 할 문자를 해독 하는 봇 어렵게 합니다.)

## <a name="adding-a-recaptcha-test"></a>ReCaptcha 테스트 추가

ASP.NET 페이지에서 사용할 수 있습니다 합니다 `ReCaptcha` ReCaptcha 서비스를 기반으로 하는 CAPTCHA 테스트를 렌더링 하는 도우미 ([http://recaptcha.net](http://recaptcha.net)). `ReCaptcha` 도우미 사용자 페이지의 유효성을 검사 하기 전에 정확 하 게 입력 해야 하는 두 개의 왜곡 된 단어의 이미지를 표시 합니다. 사용자 응답 ReCaptcha.Net 서비스에 의해 유효성이 검사 됩니다.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. ReCaptcha.Net에서 웹 사이트 등록 ([http://recaptcha.net](http://recaptcha.net)). 등록을 완료 하는 경우에 공개 키와 개인 키를 얻게 됩니다.
2. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372), 아직 없는 경우.
3. 아직 없는 경우는  *\_AppStart.cshtml* 파일, 웹 사이트의 루트 폴더에 라는 파일을 만듭니다  *\_AppStart.cshtml*합니다.
4. 다음을 추가 합니다 `Recaptcha` 에서 설정 도우미를  *\_AppStart.cshtml* 파일: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. 설정 된 `PublicKey` 및 `PrivateKey` 사용자 고유의 공용 및 개인 키를 사용 하 여 속성입니다.
6. 저장 된  *\_AppStart.cshtml* 파일을 닫습니다.
7. 웹 사이트의 루트 폴더에서 명명 된 새 페이지를 만듭니다 *Recaptcha.cshtml*합니다.
8. 기존 콘텐츠를 다음으로 바꿉니다. 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. 실행 합니다 *Recaptcha.cshtml* 브라우저에서 페이지입니다. 경우는 `PrivateKey` 값이 올바른지, ReCaptcha 컨트롤과 단추가 페이지에 표시 됩니다. 키에 전역적으로 설정 하지 했습니다  *\_AppStart.html*, 페이지에 오류가 표시 됩니다. 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. 테스트에 대 한 단어를 입력 합니다. ReCaptcha 테스트를 통과 하는 경우 그 결과는 메시지가 표시 됩니다. 그렇지 않으면 오류 메시지가 표시 되 고 ReCaptcha 컨트롤이 다시 표시 됩니다.

> [!NOTE]
> 컴퓨터가 프록시 서버를 사용 하는 도메인의 경우 구성 해야 할 수도 있습니다는 `defaultproxy` 의 요소를 *Web.config* 파일입니다. 다음 예제와 *Web.config* 파일을 `defaultproxy` ReCaptcha 서비스가 작동할 수 있도록 구성 요소입니다.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


- [ASP.NET 웹 페이지 사이트에 대 한 사이트 전체 동작을 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha site](https://www.google.com/recaptcha)
