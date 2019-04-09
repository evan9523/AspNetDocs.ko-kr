---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: '8부: 최종 페이지, 예외 처리 및 결론 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 8 부 페이지 및 예외에 대 한 연락처 페이지를 추가 하는 중...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: db8db4e3bff8047b48a7528b5146873ab6d84714
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59398685"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a>8부: 최종 페이지, 예외 처리 및 결론

[Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다. 해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 8 부 페이지 및 예외 처리에 대 한 연락처 페이지를 추가합니다. 시리즈의 결론입니다.


## <a id="_Toc260221680"></a>  페이지 (ASP.NET에서 이메일 보내기)에 문의

ContactUs.aspx 라는 새 페이지 만들기

디자이너를 사용 하는 ToolkitScriptManager 등의 AjaxControlToolkit 편집기 컨트롤을 특수 기록 형식을 만듭니다. .

![](tailspin-spyworks-part-8/_static/image1.jpg)

코드 숨김 파일에서에서 클릭 이벤트 처리기를 생성 하 고 연락처 정보를 전자 메일로 보내기 위한 메서드를 구현 하 여 "제출" 단추를 두 번 클릭 합니다.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

이 코드는 web.config 파일을 메일을 보내는 데 사용할 SMTP 서버를 지정 하는 구성 섹션의 항목 포함 필요 합니다.

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>  페이지에 대 한

AboutUs.aspx 라는 페이지를 만들고 원하는 모든 콘텐츠를 추가 합니다.

## <a id="_Toc260221682"></a>  전역 예외 처리기

마지막으로, 응용 프로그램에 걸쳐 우리는 throw 된 예외 되며 예측할 수 없는 경우에는 콜드 또한 웹 응용 프로그램에서 처리 되지 않은 원인 예외입니다.

웹 사이트 방문자에 게 표시할 처리 되지 않은 예외가 없습니다 하려고 합니다.

![](tailspin-spyworks-part-8/_static/image2.jpg)

처리 되지 않은 예외는 끔찍한 사용자 경험 중 외에도 보안 문제가 될 수도 있습니다.

이 문제를 해결 하려면 전역 예외 처리기를 구현 합니다.

이렇게 하려면 Global.asax 파일을 열고 다음 미리 생성 된 이벤트 처리기를 확인 합니다.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

응용 프로그램을 구현 하는 코드를 추가\_다음과 같은 오류 처리기입니다.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

그런 다음 솔루션에 Error.aspx 라는 페이지를 추가 하 고이 마크업 코드 조각 추가.

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

페이지에서 이제\_Request 개체에서 이벤트 처리기 추출 오류 메시지를 로드 합니다.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>  결론

ASP.NET WebForms 쉽게 살펴본 등 데이터베이스 액세스, 멤버 자격, AJAX 사용 하 여 정교한 웹 사이트를 만들려고 합니다. 매우 신속 하 게 합니다.

다행히이 자습서가 제공한 고유한 ASP.NET WebForms 응용 프로그램 구축을 시작 하는 데 필요한 도구!

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-7.md)
