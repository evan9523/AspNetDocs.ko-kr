---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: 사용자 지정 경로 만들기 (VB) | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET MVC 응용 프로그램에 사용자 지정 경로를 추가하는 방법에 대해 알아봅니다. 이 자습서에서는 Global.asax 파일에서 기본 경로 테이블을 수정하는 방법을 배웁니다.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd12307f685fa064832bb4198df06df2c3f2d3be
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542744"
---
# <a name="creating-custom-routes-vb"></a>사용자 지정 경로 만들기(VB)

[로 마이크로 소프트](https://github.com/microsoft)

> ASP.NET MVC 응용 프로그램에 사용자 지정 경로를 추가하는 방법에 대해 알아봅니다. 이 자습서에서는 Global.asax 파일에서 기본 경로 테이블을 수정하는 방법을 배웁니다.

이 자습서에서는 ASP.NET MVC 응용 프로그램에 사용자 지정 경로를 추가 하는 방법을 배웁니다. 사용자 지정 경로를 사용하여 Global.asax 파일에서 기본 경로 테이블을 수정하는 방법을 알아봅니다.

ASP.NET MVC 응용 프로그램에서는 기본 경로 테이블이 정상적으로 작동합니다. 그러나 전문적인 라우팅 요구 사항이 있음을 발견할 수 있습니다. 이 경우 사용자 지정 경로를 만들 수 있습니다.

예를 들어 블로그 응용 프로그램을 빌드한다고 가정해 보겠습니다. 다음과 같은 들어오는 요청을 처리할 수 있습니다.

/아카이브/12-25-2009

사용자가 이 요청을 입력하면 날짜 12/25/2009에 해당하는 블로그 항목을 반환하려고 합니다. 이러한 유형의 요청을 처리하려면 사용자 지정 경로를 만들어야 합니다.

목록 1의 Global.asax 파일에는 /Archive/entry*date와*같은 요청을 처리하는 새 사용자 지정 경로인 Blog가 포함되어 있습니다.

**목록 1 - Global.asax(사용자 지정 경로)**

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

라우트 테이블에 추가하는 경로의 순서가 중요합니다. 새 사용자 지정 블로그 경로가 기존 기본 경로 앞에 추가됩니다. 순서를 반대로 하면 기본 경로는 항상 사용자 지정 경로 대신 호출됩니다.

사용자 지정 블로그 경로는 /Archive/로 시작하는 모든 요청과 일치합니다. 따라서 다음 URL과 모두 일치합니다.

- /아카이브/12-25-2009

- /아카이브/10-6-2004

- /아카이브/사과

사용자 지정 경로는 들어오는 요청을 Archive라는 컨트롤러에 매핑하고 Entry() 작업을 호출합니다. Entry() 메서드가 호출되면 entryDate라는 매개 변수로 항목 날짜가 전달됩니다.

목록 2의 컨트롤러와 함께 블로그 사용자 지정 경로를 사용할 수 있습니다.

**리스팅 2 - 아카이브컨트롤러.vb**

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

목록 2의 Entry() 메서드는 DateTime 형식의 매개 변수를 허용합니다. MVC 프레임워크는 URL에서 입력 날짜를 DateTime 값으로 자동으로 변환할 수 있을 만큼 스마트합니다. URL의 항목 날짜 매개 변수를 DateTime으로 변환할 수 없는 경우 오류가 발생합니다(그림 1 참조).

**그림 1 - 매개 변수 변환 오류**

[![새 프로젝트 대화 상자](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)

**그림 01**: 매개 변수 변환 오류[(전체 크기 이미지를 보려면 클릭)](creating-custom-routes-vb/_static/image2.png)

## <a name="summary"></a>요약

이 자습서의 목표는 사용자 지정 경로를 만드는 방법을 보여 주는 것이었습니다. 블로그 항목을 나타내는 Global.asax 파일의 경로 테이블에 사용자 지정 경로를 추가하는 방법을 배웠습니다. 블로그 항목에 대한 요청을 ArchiveController라는 컨트롤러와 Entry()라는 컨트롤러 작업에 매핑하는 방법에 대해 설명했습니다.

> [!div class="step-by-step"]
> [이전](asp-net-mvc-controller-overview-vb.md)
> [다음](creating-a-route-constraint-vb.md)
