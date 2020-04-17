---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
title: '반복 #2 – 응용 프로그램을 멋지게 보이게(C#) | 마이크로 소프트 문서'
author: rick-anderson
description: 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 계단식 스타일 시트를 수정하여 응용 프로그램의 모양을 개선합니다.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1173feb-11ee-4017-8f3f-86599ea6ae13
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
msc.type: authoredcontent
ms.openlocfilehash: ee1d7c92524f6cbdb0f2d7facf85b629e0d91318
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542445"
---
# <a name="iteration-2--make-the-application-look-nice-c"></a>반복 #2 – 애플리케이션 모양 꾸미기(C#)

[로 마이크로 소프트](https://github.com/microsoft)

[코드 다운로드](iteration-2-make-the-application-look-nice-cs/_static/contactmanager_2_cs1.zip)

> 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 계단식 스타일 시트를 수정하여 응용 프로그램의 모양을 개선합니다.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>연락처 관리 ASP.NET MVC 응용 프로그램(C#) 구축

이 자습서 시리즈에서는 처음부터 끝까지 전체 연락처 관리 응용 프로그램을 빌드합니다. 연락처 관리자 응용 프로그램을 사용하면 사람 목록에 대한 연락처 정보(이름, 전화 번호 및 이메일 주소)를 저장할 수 있습니다.

여러 반복을 통해 응용 프로그램을 빌드합니다. 반복할 때마다 응용 프로그램이 점차 개선됩니다. 이 여러 반복 접근 방식의 목표는 각 변경의 이유를 이해할 수 있도록 하는 것입니다.

- 반복 #1 - 응용 프로그램을 만듭니다. 첫 번째 반복에서는 가능한 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업에 대한 지원을 추가합니다: CRUD 만들기, 읽기, 업데이트 및 삭제.

- 반복 #2 - 응용 프로그램을 멋지게 만듭니다. 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 계단식 스타일 시트를 수정하여 응용 프로그램의 모양을 개선합니다.

- 반복 #3 - 양식 유효성 검사를 추가합니다. 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 필수 양식 필드를 작성하지 않고 양식을 제출하지 못하도록 합니다. 또한 이메일 주소와 전화 번호의 유효성을 검사합니다.

- 반복 #4 - 응용 프로그램을 느슨하게 결합합니다. 이 네 번째 반복에서는 여러 소프트웨어 디자인 패턴을 활용하여 Contact Manager 응용 프로그램을 보다 쉽게 유지 관리하고 수정할 수 있습니다. 예를 들어 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 합니다.

- 반복 #5 - 단위 테스트를 만듭니다. 다섯 번째 반복에서는 단위 테스트를 추가하여 응용 프로그램을 보다 쉽게 유지 관리하고 수정할 수 있도록 합니다. 데이터 모델 클래스를 모의하고 컨트롤러 및 유효성 검사 논리에 대한 단위 테스트를 빌드합니다.

- 반복 #6 - 테스트 기반 개발을 사용합니다. 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성하고 단위 테스트에 대한 코드를 작성하여 응용 프로그램에 새로운 기능을 추가합니다. 이 반복에서는 연락처 그룹을 추가합니다.

- 반복 #7 - Ajax 기능을 추가합니다. 일곱 번째 반복에서는 Ajax에 대한 지원을 추가하여 응용 프로그램의 응답성과 성능을 향상시킵니다.

## <a name="this-iteration"></a>이 반복

이 반복의 목표는 연락처 관리자 응용 프로그램의 모양을 개선하는 것입니다. 현재 연락처 관리자는 기본 ASP.NET MVC 뷰 마스터 페이지 및 계단식 스타일 시트를 사용합니다(그림 1 참조). 이러한 나쁜 보이지 않는다, 하지만 난 그냥 다른 모든 ASP.NET MVC 웹 사이트처럼 연락처 관리자를 보고 싶지 않아요. 이러한 파일을 사용자 지정 파일로 바꾸고 싶습니다.

[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)

**그림 01**: ASP.NET MVC 응용 프로그램의 기본 모양[(전체 크기 이미지를 보려면 클릭)](iteration-2-make-the-application-look-nice-cs/_static/image2.png)

이 반복에서는 응용 프로그램의 시각적 디자인을 개선하기 위한 두 가지 방법에 대해 설명합니다. 먼저 ASP.NET MVC 디자인 갤러리를 활용하여 무료 ASP.NET MVC 디자인 템플릿을 다운로드하는 방법을 보여 드리고자 합니다. ASP.NET MVC 디자인 갤러리를 사용하면 작업을 수행하지 않고도 전문 웹 응용 프로그램을 만들 수 있습니다.

연락처 관리자 응용 프로그램에 대 한 ASP.NET MVC 디자인 갤러리에서 서식 파일을 사용 하지 않기로 결정 했습니다. 대신, 나는 전문 디자인 회사에 의해 만들어진 사용자 정의 디자인을했다. 이 자습서의 두 번째 부분에서는 전문 디자인 회사와 협력하여 MVC 디자인을 최종 ASP.NET 방법을 설명합니다.

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC 디자인 갤러리

ASP.NET MVC 디자인 갤러리는 Microsoft에서 제공하는 무료 리소스입니다. ASP.NET MVC 갤러리는 다음 주소에 있습니다.

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC 디자인 갤러리는 ASP.NET MVC 프로젝트에서 사용하기 위해 특별히 만들어진 무료 웹 사이트 디자인 컬렉션을 호스팅합니다. 디자인은 커뮤니티 구성원이 업로드합니다. 갤러리 방문자는 좋아하는 디자인에 투표할 수 있습니다(그림 2 참조).

[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)

**그림 02**: mVC 디자인 갤러리의 ASP.NET[(전체 크기 이미지를 보려면 클릭)](iteration-2-make-the-application-look-nice-cs/_static/image4.png)

이 자습서를 작성할 때 갤러리에서 가장 인기있는 디자인은 데이비드 하우저 (David Hauser)가 10 월이라는 디자인입니다. 다음 단계를 완료하여 ASP.NET MVC 프로젝트에 이 설계를 사용할 수 있습니다.

1. **다운로드** 버튼을 클릭하여 컴퓨터에 10.zip 파일을 다운로드합니다.
2. 다운로드한 10.zip 파일을 마우스 오른쪽 단추를 클릭하고 **차단 해제** 버튼을 클릭합니다(그림 3 참조).
3. 파일의 압축을 10월이라는 폴더로 압축을 해제합니다.
4. 10월 폴더에 포함된 DesignTemplate 폴더에서 모든 파일을 선택하고 파일을 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **복사를**선택합니다.
5. 시각적 스튜디오 솔루션 탐색기 창에서 ContactManager 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **붙여넣기를 선택합니다(그림** 4 참조).
6. *[MyProjectName]을* *연락처 관리자로* **편집, 찾기 및 바꾸기, 빠른 바꾸기** 및 바꾸기 옵션을 선택합니다(그림 5 참조).

[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)

**그림 03**: 웹에서 다운로드한 파일 차단 해제[(전체 크기 이미지를 보려면 클릭)](iteration-2-make-the-application-look-nice-cs/_static/image6.png)

[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)

**그림 04**: 솔루션 탐색기에서 파일 덮어쓰기[(전체 크기 이미지를 보려면 클릭)](iteration-2-make-the-application-look-nice-cs/_static/image8.png)

[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)

**그림 05**: [프로젝트 이름]을 연락처 관리자로 바꾸기[(전체 크기 이미지를 보려면 클릭하십시오)](iteration-2-make-the-application-look-nice-cs/_static/image10.png)

이 단계를 완료하면 웹 응용 프로그램에서 새 디자인을 사용합니다. 그림 6의 페이지는 10월 디자인이 있는 연락처 관리자 응용 프로그램의 모양을 보여 줍니다.

[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)

**그림 06**: 10월 템플릿이 있는 연락처 관리자[(전체 크기 이미지를 보려면 클릭하십시오)](iteration-2-make-the-application-look-nice-cs/_static/image12.png)

## <a name="creating-a-custom-aspnet-mvc-design"></a>사용자 지정 ASP.NET MVC 설계 만들기

ASP.NET MVC 디자인 갤러리는 다양한 디자인 스타일을 다양화합니다. 갤러리는 ASP.NET MVC 응용 프로그램의 모양을 사용자 정의 할 수있는 고통없는 방법을 제공합니다. 그리고 물론 갤러리는 완전히 자유롭다는 큰 장점이 있습니다.

그러나 웹 사이트에 대해 완전히 고유한 디자인을 만들어야 할 수도 있습니다. 이 경우 웹 사이트 디자인 회사와 협력하는 것이 합리적입니다. 연락처 관리자 응용 프로그램에 대 한 디자인에 대 한이 방법을 사용 하기로 결정 했습니다.

반복 #1 연락처 관리자를 압축하여 프로젝트를 설계 회사에 보냈습니다. 그들은 비주얼 스튜디오를 소유하지 않았다 (그들에 수치!), 하지만 그 문제가 제시하지 않았다. [https://www.asp.net](https://www.asp.net) 웹 사이트에서 Microsoft 비주얼 웹 개발자를 무료로 다운로드하고 시각적 웹 개발자의 연락처 관리자 응용 프로그램을 열 수 있었습니다. 며칠 만에 그림 7에서 디자인을 제작했습니다.

[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)

**그림 07**: ASP.NET MVC 연락처 관리자 디자인[(전체 크기 이미지를 보려면 클릭)](iteration-2-make-the-application-look-nice-cs/_static/image14.png)

새로운 디자인은 두 개의 주요 파일로 구성: 새로운 계단식 스타일 시트 파일 및 새 보기 마스터 페이지 파일. 뷰 마스터 페이지에는 ASP.NET MVC 응용 프로그램의 보기에 대한 레이아웃 및 공유 콘텐츠가 포함되어 있습니다. 예를 들어 뷰 마스터 페이지에는 그림 7에 나타나는 헤더, 탐색 탭 및 바닥글이 포함됩니다. 뷰\공유 폴더에 있는 기존 Site.Master 뷰 마스터 페이지를 디자인 회사의 새 Site.Master 파일과 함께 덮어썼습니다.

디자인 회사는 또한 새로운 계단식 스타일 시트와 이미지 세트를 만들었습니다. 이러한 새 파일을 콘텐츠 폴더에 배치하고 기존 Site.css 파일을 덮어썼습니다. 콘텐츠 폴더에 모든 정적 콘텐츠를 배치해야 합니다.

연락처 관리자의 새 디자인에는 연락처를 편집하고 삭제하기 위한 이미지가 포함되어 있습니다. 편집 및 삭제 이미지는 연락처의 HTML 테이블의 각 연락처 옆에 나타납니다.

원래 HTML로 렌더링된 이러한 링크입니다. 다음과 같은 ActionLink() 도우미:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample1.aspx)]

Html.ActionLink() 메서드는 이미지를 지원하지 않습니다(HTML이 보안상의 이유로 링크 텍스트를 인코딩하는 메서드). 따라서 Html.ActionLink()에 대한 호출을 다음과 같이 Url.Action()에 대한 호출로 바꿔 했습니다.

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample2.aspx)]

Html.ActionLink() 메서드는 전체 HTML 하이퍼링크를 렌더링합니다. 반면 Url.Action() 메서드는 &lt;&gt; 태그 없이 URL만 렌더링합니다.

또한 새 디자인에 선택된 탭과 선택되지 않은 탭이 모두 포함되어 있습니다. 예를 들어 그림 8에서 **새 연락처 만들기** 탭이 선택되고 내 **연락처** 탭이 선택되지 않습니다.

[![새 프로젝트 대화 상자](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)

**그림 08**: 선택 및 선택되지 않은 탭[(클릭하여 전체 크기 이미지를 보려면)](iteration-2-make-the-application-look-nice-cs/_static/image16.png)

선택된 탭과 선택되지 않은 탭을 모두 렌더링할 수 있도록 MenuItemHelper라는 사용자 지정 HTML 도우미를 만들었습니다. 이 도우미 메서드는 현재 &lt;&gt; 컨트롤러 및 &lt;작업이 도우미에&gt; 전달된 컨트롤러 및 작업 이름에 해당하는지 여부에 따라 li 태그 또는 li class="선택된" 태그를 렌더링합니다. MenuItemHelper의 코드는 목록 1에 포함되어 있습니다.

**목록 1 - 도우미\메뉴항목도우미.cs**

[!code-csharp[Main](iteration-2-make-the-application-look-nice-cs/samples/sample3.cs)]

MenuItemHelper는 내부적으로 TagBuilder 클래스를 사용하여 &lt;&gt; li HTML 태그를 작성합니다. TagBuilder 클래스는 새 HTML 태그를 빌드해야 할 때마다 사용할 수 있는 매우 유용한 유틸리티 클래스입니다. 여기에는 특성 추가, CSS 클래스 추가, ID 생성 및 태그 내부 HTML 수정 방법이 포함되어 있습니다.

## <a name="summary"></a>요약

이 반복에서는 ASP.NET MVC 응용 프로그램의 시각적 디자인을 개선했습니다. 먼저 ASP.NET MVC 디자인 갤러리를 소개했습니다. ASP.NET MVC 응용 프로그램에서 사용할 수 있는 ASP.NET MVC 디자인 갤러리에서 무료 디자인 템플릿을 다운로드하는 방법을 배웠습니다.

다음으로, 기본 계단식 스타일 시트 파일 및 마스터 뷰 페이지 파일을 수정 하여 사용자 지정 디자인을 만드는 방법에 대해 설명했습니다. 새 디자인을 지원하기 위해 연락처 관리자 응용 프로그램을 약간 변경해야 했습니다. 예를 들어 선택된 탭과 선택되지 않은 탭을 표시하는 MenuItemHelper라는 새 HTML 도우미를 추가했습니다.

다음 반복에서는 유효성 검사의 매우 중요한 주제를 다룹니다. 사용자가 사람의 이름과 성과 같은 필수 값을 제공하지 않고는 새 연락처를 만들 수 없도록 응용 프로그램에 유효성 검사 코드를 추가합니다.

> [!div class="step-by-step"]
> [이전](iteration-1-create-the-application-cs.md)
> [다음](iteration-3-add-form-validation-cs.md)
