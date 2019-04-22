---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner 자습서 소개 | Microsoft Docs
author: shanselman
description: 새로운 프레임 워크는 가장 좋은 방법은 작업을 작성 하는 경우 이 자습서에서는 ASP.NE를 사용 하 여 완료 하지만 크기가 작은 응용 프로그램을 작성 하는 방법을 설명 하는 중...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: ebd49295ea165ba4ef1a25398cff7dddcfa54f11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59392198"
---
# <a name="introducing-the-nerddinner-tutorial"></a>NerdDinner 자습서 소개

[Scott Hanselman](https://github.com/shanselman)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 새로운 프레임 워크는 가장 좋은 방법은 작업을 작성 하는 경우 이 자습서는 작은 빌드만 ASP.NET MVC 1을 사용 하 여 응용 프로그램을 완료 하는 방법을 안내 하 고는 핵심 개념 중 일부를 소개 합니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-tutorial"></a>NerdDinner 자습서

새로운 프레임 워크는 가장 좋은 방법은 작업을 작성 하는 경우 이 자습서는 작은 빌드만 ASP.NET MVC를 사용 하 여 응용 프로그램을 완료 하는 방법을 안내 하 고는 핵심 개념 중 일부를 소개 합니다.

빌드 하려는 응용 프로그램 "NerdDinner" 라고 합니다. NerdDinner 쉽게를 찾고 dinners online을 구성 하는 사용자를 제공 합니다.

![](introducing-the-nerddinner-tutorial/_static/image1.png)

NerdDinner 등록 된 사용자를를 만들고, 편집 dinners를 삭제할 수 있습니다. 응용 프로그램 간에 일관 된 유효성 검사 및 비즈니스 규칙 집합을 적용 합니다.

![](introducing-the-nerddinner-tutorial/_static/image2.png)

방문자는 AJAX 기반 지도 사용 하 여 향후 dinners 가까이 보유 하 고 검색할 수 있습니다.

![](introducing-the-nerddinner-tutorial/_static/image3.png)

클릭 하면는 dinner 이동 해당 세부 정보 페이지를 어디서 알아볼 수 자세히:

![](introducing-the-nerddinner-tutorial/_static/image4.png)

Dinner 참여에 관심이 있는 경우 로그인 하거나 사이트에 등록 수 있습니다.

![](introducing-the-nerddinner-tutorial/_static/image5.png)

이벤트 참석 RSVP AJAX 기반 링크를 클릭할 수 있습니다.

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>NerdDinner 구현

파일-를 사용 하 여 NerdDinner 응용 프로그램을 시작 하겠습니다&gt;새로운 ASP.NET MVC 프로젝트를 만들려면 Visual Studio 내에서 새 프로젝트 명령입니다. 그런 다음 증분 방식으로 추가 기능 및 기능. 이 과정에서 설명 하겠습니다.

1. [새 ASP.NET MVC 프로젝트를 만드는 방법](create-a-new-aspnet-mvc-project.md)
2. [데이터베이스를 만드는 방법](create-a-database.md)
3. [비즈니스 규칙 유효성 검사를 사용 하 여 모델을 빌드하는 방법](build-a-model-with-business-rule-validations.md)
4. [목록/세부 정보 UI 구현 하려면 컨트롤러와 뷰를 사용 하는 방법](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [CRUD를 제공 하는 방법 (만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [ViewData 사용 및 ViewModel 클래스를 구현 하는 방법](use-viewdata-and-implement-viewmodel-classes.md)
7. [마스터 페이지 및 부분을 사용 하 여 UI를 다시 사용 하는 방법](re-use-ui-using-master-pages-and-partials.md)
8. [효율적인 데이터 페이징 구현 하는 방법](implement-efficient-data-paging.md)
9. [인증 및 권한 부여를 사용 하 여 응용 프로그램을 보호 하는 방법](secure-applications-using-authentication-and-authorization.md)
10. [AJAX를 사용 하 여 동적 업데이트를 제공 하는 방법](use-ajax-to-deliver-dynamic-updates.md)
11. [AJAX를 사용 하 여 매핑 시나리오를 구현 하는 방법](use-ajax-to-implement-mapping-scenarios.md)
12. [자동화 된 단위 테스트를 사용 하는 방법](enable-automated-unit-testing.md)

NerdDinner의 고유한 복사본을 빌드할 수 있습니다 각 완료 하 여 처음부터 단계에서는이 챕터에 연습입니다. 또는 여기에서 소스 코드의 전체 버전을 다운로드할 수 있습니다. [GitHub에서 NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner)합니다. 또한 필요에 따라 수도 있습니다 [이 자습서에서는 무료 PDF 버전을 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) 하려면 오프 라인 자습서를 읽어 보세요.

응용 프로그램을 빌드하려면 Visual Studio 2008 또는 무료 Visual Web Developer 2008 Express를 사용할 수 있습니다. 데이터베이스에 대 한 SQL Server 또는 무료 SQL Server Express를 사용할 수 있습니다.

ASP.NET MVC, Visual Web Developer 2008 Express 및 SQL Server Express (모든 사용 가능)의 V2를 사용 하 여 설치할 수는 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>이제 시작 해 보겠습니다...

NerdDinner 란 살펴보았습니다 했으므로 실제로 롤업 하 고 일부 코드를 작성 하겠습니다.

파일-를 사용 하 여 먼저&gt;NerdDinner 응용 프로그램을 만들려면 Visual Studio 내에서 새 프로젝트입니다.

> [!div class="step-by-step"]
> [다음](create-a-new-aspnet-mvc-project.md)
