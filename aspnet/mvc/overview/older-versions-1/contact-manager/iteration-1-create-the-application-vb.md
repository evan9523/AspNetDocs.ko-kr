---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: '반복 #1 – 응용 프로그램 만들기(VB) | 마이크로 소프트 문서'
author: rick-anderson
description: '첫 번째 반복에서는 가능한 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업에 대한 지원을 추가합니다: 만들기, 읽기, 업데이트 및 D...'
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: 235f6f8812a2f584de8e07dcf97d5c1712c51776
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542536"
---
# <a name="iteration-1--create-the-application-vb"></a>반복 #1 – 애플리케이션 만들기(VB)

[로 마이크로 소프트](https://github.com/microsoft)

[코드 다운로드](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> 첫 번째 반복에서는 가능한 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업에 대한 지원을 추가합니다: CRUD 만들기, 읽기, 업데이트 및 삭제.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>연락처 관리 ASP.NET MVC 응용 프로그램(VB) 구축

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

이 첫 번째 반복에서는 기본 응용 프로그램을 빌드합니다. 목표는 가능한 한 가장 빠르고 간단한 방법으로 연락처 관리자를 구축하는 것입니다. 이후 반복에서는 응용 프로그램의 디자인을 개선합니다.

연락처 관리자 응용 프로그램은 기본 데이터베이스 기반 응용 프로그램입니다. 응용 프로그램을 사용하여 새 연락처를 만들고, 기존 연락처를 편집하고, 연락처를 삭제할 수 있습니다.

이 반복에서는 다음 단계를 완료합니다.

1. ASP.NET MVC 응용 프로그램
2. 연락처를 저장할 데이터베이스 만들기
3. Microsoft 엔터티 프레임워크를 사용하여 데이터베이스에 대한 모델 클래스 생성
4. 데이터베이스에 있는 모든 연락처를 나열할 수 있는 컨트롤러 작업 및 보기 만들기
5. 컨트롤러 작업 및 데이터베이스에서 새 연락처를 만들 수 있는 뷰 만들기
6. 컨트롤러 작업 및 데이터베이스의 기존 연락처를 편집할 수 있는 뷰 만들기
7. 컨트롤러 작업 및 데이터베이스의 기존 연락처를 삭제할 수 있는 뷰 만들기

## <a name="software-prerequisites"></a>소프트웨어 필수 구성 요소

ASP.NET MVC 응용 프로그램에서는 컴퓨터에 Visual Studio 2008 또는 Visual Web Developer 2008이 설치되어 있어야 합니다(Visual Web Developer은 Visual Studio의 모든 고급 기능을 포함하지 않는 Visual Studio의 무료 버전입니다). 다음 주소에서 Visual Studio 2008의 평가판 또는 Visual Web 개발자를 다운로드할 수 있습니다.

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> 비주얼 웹 개발자가 있는 ASP.NET MVC 응용 프로그램의 경우 Visual Web 개발자 서비스 팩 1이 설치되어 있어야 합니다. 서비스 팩 1이 없으면 웹 응용 프로그램 프로젝트를 만들 수 없습니다.

ASP.NET MVC 프레임워크입니다. 다음 주소에서 ASP.NET MVC 프레임워크를 다운로드할 수 있습니다.

[https://www.asp.net/mvc](../../../index.md)

이 자습서에서는 Microsoft 엔터티 프레임워크를 사용하여 데이터베이스에 액세스합니다. 엔터티 프레임워크는 .NET 프레임워크 3.5 서비스 팩 1에 포함되어 있습니다. 다음 위치에서 이 서비스 팩을 다운로드할 수 있습니다.

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

이러한 각 다운로드를 하나씩 수행하는 대신 웹 플랫폼 설치 관리자(웹 PI)를 활용할 수 있습니다. 다음 주소에서 웹 PI를 다운로드할 수 있습니다.

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC 프로젝트

ASP.NET MVC 웹 응용 프로그램 프로젝트입니다. 비주얼 스튜디오를 실행하고 메뉴 옵션 **파일을 선택, 새 프로젝트**. **새 프로젝트** 대화 상자가 나타납니다(그림 1 참조). **웹** 프로젝트 유형과 **ASP.NET MVC 웹 응용 프로그램** 템플릿을 선택합니다. 새 프로젝트 *연락처 관리자의* 이름을 지정하고 확인 단추를 클릭합니다.

**새 프로젝트** 대화 상자의 오른쪽 상단에 있는 드롭다운 목록에서 .NET Framework 3.5를 선택했는지 확인합니다. 그렇지 않으면 ASP.NET MVC 웹 응용 프로그램 템플릿이 나타나지 않습니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)

**그림 01**: 새 프로젝트 대화 상자[(클릭하여 전체 크기 이미지 보기)](iteration-1-create-the-application-vb/_static/image2.png)

MVC 응용 프로그램에서 ASP.NET **단위 테스트 프로젝트 만들기** 대화 상자가 나타납니다. 이 대화 상자를 사용하여 ASP.NET MVC 응용 프로그램을 만들 때 솔루션에 단위 테스트 프로젝트를 만들고 추가하려는 것을 나타낼 수 있습니다. 이 반복에서는 단위 테스트를 빌드하지 는 않지만 나중에 단위 테스트를 추가할 계획이기 때문에 예 옵션을 선택하고 **단위 테스트 프로젝트를 만들어야** 합니다. ASP.NET MVC 프로젝트를 만든 후 테스트 프로젝트를 추가하는 것보다 새로운 ASP.NET MVC 프로젝트를 처음 만들 때 테스트 프로젝트를 추가하는 것이 훨씬 쉽습니다.

> [!NOTE] 
> 
> Visual Web 개발자는 테스트 프로젝트를 지원하지 않으므로 Visual Web 개발자를 사용할 때 단위 테스트 프로젝트 만들기 대화 상자가 없습니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)

**그림 02**: 단위 테스트 프로젝트 만들기 대화 상자[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image4.png)

ASP.NET MVC 응용 프로그램이 시각적 스튜디오 솔루션 탐색기 창에 나타납니다(그림 3 참조). 솔루션 탐색기 창이 표시되지 않으면 메뉴 옵션 **보기, 솔루션 탐색기를**선택하여 이 창을 열 수 있습니다. 솔루션에는 ASP.NET MVC 프로젝트와 테스트 프로젝트의 두 프로젝트가 포함되어 있습니다. ASP.NET MVC 프로젝트는 ContactManager로 명명되고 테스트 프로젝트는 ContactManager.Test로 명명됩니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)

**그림 03**: 솔루션 탐색기 창[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image6.png)

## <a name="deleting-the-project-sample-files"></a>프로젝트 샘플 파일 삭제

ASP.NET MVC 프로젝트 템플릿에는 컨트롤러 및 뷰에 대한 샘플 파일이 포함되어 있습니다. 새 ASP.NET MVC 응용 프로그램을 만들기 전에 이러한 파일을 삭제해야 합니다. 솔루션 탐색기 창에서 파일 또는 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 삭제를 선택하여 파일 및 폴더를 삭제할 수 **있습니다.**

ASP.NET MVC 프로젝트에서 다음 파일을 삭제해야 합니다.

- \컨트롤러\홈 컨트롤러.vb

- \뷰\홈\약.aspx

- \뷰\홈\인덱스.aspx

또한 테스트 프로젝트에서 다음 파일을 삭제해야 합니다.

\컨트롤러\홈 컨트롤러테스트.vb

## <a name="creating-the-database"></a>데이터베이스 만들기

연락처 관리자 응용 프로그램은 데이터베이스 기반 웹 응용 프로그램입니다. 우리는 연락처 정보를 저장하는 데이터베이스를 사용합니다.

Microsoft SQL Server, 오라클, MySQL 및 IBM DB2 데이터베이스를 포함한 모든 최신 데이터베이스가 있는 ASP.NET MVC 프레임워크입니다. 이 자습서에서는 Microsoft SQL Server 데이터베이스를 사용합니다. Visual Studio를 설치하면 Microsoft SQL Server 데이터베이스의 무료 버전인 Microsoft SQL Server Express를 설치하는 옵션이 제공됩니다.

솔루션 탐색기 창에서 앱\_데이터 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **추가, 새 항목**을 선택하여 새 데이터베이스를 만듭니다. 새 **항목 추가** 대화 상자에서 **데이터** 범주 및 SQL **Server 데이터베이스** 템플릿을 선택합니다(그림 4 참조). 새 데이터베이스 ContactManagerDB.mdf의 이름을 지정하고 확인 버튼을 클릭합니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)

**그림 04**: 새 Microsoft SQL Server Express 데이터베이스 만들기[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image8.png)

새 데이터베이스를 만든 후 데이터베이스는 솔루션\_탐색기 창의 앱 데이터 폴더에 나타납니다. ContactManager.mdf 파일을 두 번 클릭하여 서버 탐색기 창을 열고 데이터베이스에 연결합니다.

> [!NOTE] 
> 
> Microsoft 비주얼 웹 개발자의 경우 서버 탐색기 창을 데이터베이스 탐색기 창이라고 합니다.

서버 탐색기 창을 사용하여 데이터베이스 테이블, 뷰, 트리거 및 저장 프로시저와 같은 새 데이터베이스 개체를 만들 수 있습니다. 테이블 폴더를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션을 **선택합니다.** 데이터베이스 테이블 디자이너가 나타납니다(그림 5 참조).

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)

**그림 05**: 데이터베이스 테이블 디자이너[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image10.png)

다음 열이 포함된 테이블을 만들어야 합니다.

<a id="0.2_table01"></a>

| **열 이름** | **데이터 유형** | **Null 허용** |
| --- | --- | --- |
| Id | int | false |
| FirstName | nvarchar(50) | false |
| LastName | nvarchar(50) | false |
| Phone | nvarchar(50) | false |
| Email | nvarchar(255) | false |

첫 번째 열인 Id 열은 특별합니다. Id 열을 ID 열과 기본 키 열로 표시해야 합니다. 열 속성을 확장하고(그림 6의 아래쪽을 확인) ID 사양 속성으로 아래로 스크롤하여 열이 ID 열임을 나타냅니다. **(Id)** 속성을 값 예로 **설정합니다.**

열을 선택하고 키 아이콘이 있는 단추를 클릭하여 열을 기본 키 열로 표시합니다. 열이 기본 키 열로 표시되면 키 아이콘이 열 옆에 나타납니다(그림 6 참조).

테이블 만들기를 마친 후 저장 단추(플로피 아이콘이 있는 단추)를 클릭하여 새 테이블을 저장합니다. 새 테이블에 연락처 이름을 *지정합니다.*

연락처 데이터베이스 테이블 만들기를 완료한 후 테이블에 일부 레코드를 추가해야 합니다. 서버 탐색기 창에서 연락처 테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 데이터 표시**옵션을 선택합니다. 나타나는 표에 하나 이상의 연락처를 입력합니다.

## <a name="creating-the-data-model"></a>데이터 모델 만들기

ASP.NET MVC 응용 프로그램은 모델, 뷰 및 컨트롤러로 구성됩니다. 먼저 이전 섹션에서 만든 연락처 테이블을 나타내는 모델 클래스를 만듭니다.

이 자습서에서는 Microsoft 엔터티 프레임워크를 사용하여 데이터베이스에서 모델 클래스를 자동으로 생성합니다.

> [!NOTE] 
> 
> ASP.NET MVC 프레임워크는 어떤 식으로든 Microsoft 엔터티 프레임워크에 연결되지 않습니다. NHibernate, LINQ에서 SQL 또는 ADO.NET 같은 대체 데이터베이스 액세스 기술과 ASP.NET MVC를 사용할 수 있습니다.

다음 단계에 따라 데이터 모델 클래스를 만듭니다.

1. 솔루션 탐색기 창에서 모델 폴더를 마우스 오른쪽 단추로 클릭하고 **새 항목 추가를**선택합니다. **새 항목 추가** 대화 상자가 나타납니다(그림 6 참조).
2. **데이터** 범주 및 **ADO.NET 엔터티 데이터 모델** 템플릿을 선택합니다. 데이터 *모델의* 이름을 지정하고 **추가** 단추를 클릭합니다. 엔터티 데이터 모델 마법사가 나타납니다(그림 7 참조).
3. 모델 내용 선택 단계에서 **데이터베이스에서 생성을** **선택합니다(그림** 7 참조).
4. 데이터 **연결 선택** 단계에서 ContactManagerDB.mdf 데이터베이스를 선택하고 엔터티 연결 설정에 대한 *ContactManagerDBEntity라는* 이름을 입력합니다(그림 8 참조).
5. 데이터베이스 개체 선택 단계에서 테이블레이블이 지정된 확인란을 **선택합니다(그림** 9 참조). 데이터 모델에는 데이터베이스에 포함된 모든 테이블이 포함됩니다(연락처 테이블이 하나뿐입니다). 네임스페이스 *모델을 입력합니다.* 완료 버튼을 클릭하여 마법사를 완료합니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)

**그림 06**: 새 항목 추가 대화 상자[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image12.png)

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)

**그림 07**: 모델 내용 선택[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image14.png)

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)

**그림 08**: 데이터 연결을 선택[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image16.png)

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)

**그림 09**: 데이터베이스 객체 선택[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image18.png)

엔터티 데이터 모델 마법사를 완료하면 엔터티 데이터 모델 디자이너가 나타납니다. 디자이너는 모델링되는 각 테이블에 해당하는 클래스를 표시합니다. 연락처라는 클래스가 하나 표시됩니다.

엔터티 데이터 모델 마법사는 데이터베이스 테이블 이름을 기반으로 클래스 이름을 생성합니다. 마법사에서 생성된 클래스의 이름을 거의 항상 변경해야 합니다. 디자이너에서 연락처 클래스를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **이름을 선택합니다.** 클래스 이름을 연락처(복수)에서 연락처(단수)로 변경합니다. 클래스 이름을 변경하면 클래스가 그림 10과 같이 나타납니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)

**그림 10**: 연락처 클래스[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image20.png)

이 시점에서 데이터베이스 모델을 만들었습니다. 연락처 클래스를 사용하여 데이터베이스의 특정 연락처 레코드를 나타낼 수 있습니다.

## <a name="creating-the-home-controller"></a>홈 컨트롤러 만들기

다음 단계는 홈 컨트롤러를 만드는 것입니다. 홈 컨트롤러는 ASP.NET MVC 응용 프로그램에서 호출되는 기본 컨트롤러입니다.

솔루션 탐색기 창에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭하고 **컨트롤러 추가** 옵션을 선택하여 홈 컨트롤러 클래스를 만듭니다(그림 11 참조). **만들기, 업데이트 및 세부 정보 시나리오에 대한 작업 메서드 추가라는**확인란에 알 수 있습니다. **추가** 단추를 클릭하기 전에 이 확인란을 선택했는지 확인합니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)

**그림 11**: 홈 컨트롤러 추가[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image22.png)

홈 컨트롤러를 만들 면 목록 1에서 클래스를 가져옵니다.

**목록 1 - 컨트롤러\홈컨트롤러.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a>연락처 목록

연락처 데이터베이스 테이블에 레코드를 표시 하려면 Index() 작업 및 인덱스 보기를 만들어야 합니다.

홈 컨트롤러에는 이미 Index() 작업이 포함되어 있습니다. 목록 2처럼 보이도록이 메서드를 수정해야 합니다.

**리스팅 2 - 컨트롤러\홈컨트롤러.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

목록 2의 홈 컨트롤러 클래스에는 엔터티라는 \_개인 필드가 포함되어 있습니다. \_엔터티 필드는 데이터 모델의 엔터티를 나타냅니다. \_엔터티 필드를 사용하여 데이터베이스와 통신합니다.

Index() 메서드는 연락처 데이터베이스 테이블의 모든 연락처를 나타내는 뷰를 반환합니다. 식 \_엔터티입니다. ContactSet.ToList()는 연락처 목록을 제네릭 목록으로 반환합니다.

이제 인덱스 컨트롤러를 만들었으니 다음으로 인덱스 뷰를 만들어야 합니다. 인덱스 뷰를 만들기 전에 메뉴 옵션 **빌드 솔루션**빌드를 선택하여 응용 프로그램을 컴파일합니다. 모델 클래스 목록이 **추가** 대화 상자에 표시되려면 뷰를 추가하기 전에 항상 프로젝트를 컴파일해야 합니다.

Index() 메서드를 마우스 오른쪽 단추로 클릭하고 메뉴 **추가** 옵션을 선택하여 인덱스 뷰를 만듭니다(그림 12 참조). 이 메뉴를 선택하면 **추가 보기** 대화 상자가 열립니다(그림 13 참조).

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)

**그림 12**: 색인 보기 추가[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image24.png)

뷰 **추가** 대화 상자에서 **강력한 형식의 뷰 만들기라는 레이블이**붙은 확인란을 선택합니다. 데이터 클래스 연락처 관리자.연락처 및 보기 콘텐츠 목록을 선택합니다. 이러한 옵션을 선택하면 연락처 레코드 목록을 표시하는 뷰가 생성됩니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)

**그림 13**: 추가 보기 대화 상자[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image26.png)

**추가** 단추를 클릭하면 목록 3의 인덱스 보기가 생성됩니다. 파일 &lt;맨 위에&gt; 표시되는 %@ 페이지 % 지시문을 확인합니다. 인덱스&lt;보기는 ViewPage IEnumerable&lt;ContactManager.Models.Contact&gt; &gt; 클래스에서 상속됩니다. 즉, 뷰의 모델 클래스는 연락처 엔터티 목록을 나타냅니다.

인덱스 뷰의 본문에는 Model 클래스로 표시되는 각 연락처를 반복하는 foreach 루프가 포함되어 있습니다. Contact 클래스의 각 속성 값이 HTML 테이블 내에 표시됩니다.

**목록 3 - 보기\홈\인덱스.aspx(수정되지 않은)**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

인덱스 보기를 한 번 수정해야 합니다. 세부 정보 보기를 만들지 않으므로 세부 정보 링크를 제거할 수 있습니다. 인덱스 보기에서 다음 코드를 찾아 제거합니다.

{.id = 항목입니다. ID})%%&gt;

색인 보기를 수정한 후 연락처 관리자 응용 프로그램을 실행할 수 있습니다. 메뉴 옵션 디버그를 선택하거나 디버깅을 시작하거나 F5를 누르기만 하면 됩니다. 응용 프로그램을 처음 실행할 때 그림 14의 대화 상자를 얻을 수 있습니다. **Web.config 파일 수정 옵션을 선택하여 디버깅을 활성화하고** 확인 단추를 클릭합니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)

**그림 14**: 디버깅 활성화[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image28.png)

인덱스 보기는 기본적으로 반환됩니다. 이 보기는 연락처 데이터베이스 테이블의 모든 데이터를 나열합니다(그림 15 참조).

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)

**그림 15**: 색인 보기[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image30.png)

색인 보기에는 뷰 맨 아래에 새 만들기라는 레이블이 붙은 링크가 포함되어 있습니다. 다음 섹션에서는 새 연락처를 만드는 방법을 배웁니다.

## <a name="creating-new-contacts"></a>새 연락처 만들기

사용자가 새 연락처를 만들 수 있도록 하려면 홈 컨트롤러에 두 개의 Create() 작업을 추가해야 합니다. 새 연락처를 만들기 위한 HTML 양식을 반환 하는 Create() 작업을 하나 만들어야 합니다. 새 연락처의 실제 데이터베이스 삽입을 수행하는 두 번째 Create() 작업을 만들어야 합니다.

홈 컨트롤러에 추가해야 하는 새 Create() 메서드는 목록 4에 포함되어 있습니다.

**목록 4 - 컨트롤러\HomeController.vb (메서드 만들기 사용)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

첫 번째 Create() 메서드는 HTTP GET으로 호출할 수 있으며 두 번째 Create() 메서드는 HTTP POST에서만 호출할 수 있습니다. 즉, 두 번째 Create() 메서드는 HTML 양식을 게시할 때만 호출할 수 있습니다. 첫 번째 Create() 메서드는 새 연락처를 만들기 위한 HTML 양식이 포함된 뷰를 반환합니다. 두 번째 Create() 메서드는 데이터베이스에 새 연락처를 추가합니다.

두 번째 Create() 메서드가 Contact 클래스의 인스턴스를 수락하도록 수정되었습니다. HTML 양식에서 게시된 양식 값은 ASP.NET MVC 프레임워크에 의해 이 Contact 클래스에 자동으로 바인딩됩니다. HTML 만들기 양식의 각 양식 필드는 Contact 매개 변수의 속성에 할당됩니다.

Contact 매개 변수는 [바인딩] 특성으로 장식되어 있습니다. [바인딩] 특성은 연락처 Id 속성을 바인딩에서 제외하는 데 사용됩니다. Id 속성은 Id 속성을 나타내므로 Id 속성을 설정하지 않으려고 합니다.

Create() 메서드의 본문에서 엔터티 프레임워크는 데이터베이스에 새 연락처를 삽입하는 데 사용됩니다. 새 연락처는 기존 연락처 집합에 추가되고 SaveChanges() 메서드가 호출되어 이러한 변경 내용을 기본 데이터베이스로 다시 푸시합니다.

두 만들기() 메서드 중 하나를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 추가 **보기(그림** 16 참조)를 선택하여 새 연락처를 만들기 위한 HTML 양식을 생성할 수 있습니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)

**그림 16**: 만들기 보기 추가[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image32.png)

보기 **추가** 대화 상자에서 **ContactManager.Contact** 클래스및 보기 내용에 대한 **만들기** 옵션을 선택합니다(그림 17 참조). **추가** 단추를 클릭하면 뷰 만들기가 자동으로 생성됩니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)

**그림 17**: 페이지 폭발 보기[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image34.png)

만들기 뷰에는 연락처 클래스의 각 속성에 대한 양식 필드가 포함되어 있습니다. 만들기 보기에 대한 코드는 목록 5에 포함되어 있습니다.

**리스팅 5 - 뷰\홈\만들기.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

만들기() 메서드를 수정하고 만들기 뷰를 추가한 후 담당자 응용 프로그램을 실행하고 새 연락처를 만들 수 있습니다. 색인 보기에 표시되는 **새 만들기** 링크를 클릭하여 만들기 보기로 이동합니다. 그림 18의 뷰가 표시됩니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)

**그림 18**: 뷰 만들기[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image36.png)

## <a name="editing-contacts"></a>연락처 편집

연락처 레코드를 편집하는 기능을 추가하는 것은 새 연락처 레코드를 만드는 기능을 추가하는 것과 매우 유사합니다. 먼저 홈 컨트롤러 클래스에 두 개의 새 편집 메서드를 추가해야 합니다. 이러한 새 편집() 메서드는 목록 6에 포함되어 있습니다.

**목록 6 - 컨트롤러\HomeController.vb (편집 방법 사용)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

첫 번째 편집() 메서드는 HTTP GET 작업에 의해 호출됩니다. Id 매개 변수는 편집 중인 연락처 레코드의 ID를 나타내는 이 메서드에 전달됩니다. 엔터티 프레임워크는 Id와 일치하는 연락처를 검색하는 데 사용됩니다. 레코드를 편집하기 위한 HTML 양식이 포함된 뷰가 반환됩니다.

두 번째 편집() 메서드는 데이터베이스에 대한 실제 업데이트를 수행합니다. 이 메서드는 Contact 클래스의 인스턴스를 매개 변수로 허용합니다. ASP.NET MVC 프레임워크는 편집 양식에서 이 클래스에 양식 필드를 자동으로 바인딩합니다. 연락처를 편집할 때 [Bind] 특성을 포함하지 않습니다(Id 속성값이 필요합니다).

엔터티 프레임워크는 수정된 연락처를 데이터베이스에 저장하는 데 사용됩니다. 원래 연락처는 먼저 데이터베이스에서 검색해야 합니다. 다음으로 엔터티 프레임워크 ApplyPropertyChanges() 메서드가 호출되어 연락처에 대한 변경 내용을 기록합니다. 마지막으로 엔터티 프레임 워크 SaveChanges() 메서드는 기본 데이터베이스에 대 한 변경 내용을 유지 하도록 호출 됩니다.

편집() 메서드를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 보기 추가 옵션을 선택하여 편집 양식이 포함된 뷰를 생성할 수 있습니다. 뷰 추가 대화 상자에서 **ContactManager.Models.Contact** 클래스 및 **편집** 뷰 콘텐츠를 선택합니다(그림 19 참조).

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)

**그림 19**: 편집 뷰 추가[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image38.png)

추가 단추를 클릭하면 새 편집 보기가 자동으로 생성됩니다. 생성되는 HTML 양식에는 연락처 클래스의 각 속성에 해당하는 필드가 포함되어 있습니다(목록 7 참조).

**리스팅 7 - 보기\홈\편집.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>연락처 삭제

연락처를 삭제하려면 홈 컨트롤러 클래스에 두 개의 Delete() 작업을 추가해야 합니다. 첫 번째 Delete() 작업에는 삭제 확인 양식이 표시됩니다. 두 번째 Delete() 작업은 실제 삭제를 수행합니다.

> [!NOTE] 
> 
> 나중에 반복 #7 Ajax 삭제 를 지원 하므로 연락처 관리자를 수정합니다.

두 개의 새 Delete() 메서드가 목록 8에 포함되어 있습니다.

**목록 8 - 컨트롤러\HomeController.vb (방법 삭제)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

첫 번째 Delete() 메서드는 데이터베이스에서 연락처 레코드를 삭제하기 위한 확인 양식을 반환합니다(그림 20 참조). 두 번째 Delete() 메서드는 데이터베이스에 대해 실제 삭제 작업을 수행합니다. 데이터베이스에서 원래 연락처를 검색한 후 엔터티 프레임워크 DeleteObject() 및 SaveChanges() 메서드를 호출하여 데이터베이스 삭제를 수행합니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)

**그림 20**: 삭제 확인 보기[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image40.png)

연락처 레코드를 삭제하기 위한 링크가 포함되도록 인덱스 뷰를 수정해야 합니다(그림 21 참조). 편집 링크가 포함된 동일한 테이블 셀에 다음 코드를 추가해야 합니다.

{.id = 항목입니다. ID})%%&gt;

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)

**그림 21**: 편집 링크가 있는 색인[보기(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image42.png)

다음으로 삭제 확인 보기를 만들어야 합니다. 홈 컨트롤러 클래스에서 Delete() 메서드를 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 보기 추가옵션을 선택합니다. 뷰 추가 대화 상자가 나타납니다(그림 22 참조).

목록, 만들기 및 편집 보기의 경우와 달리 뷰 추가 대화 상자에는 삭제 뷰를 만드는 옵션이 포함되어 있지 않습니다. 대신 연락처 **관리자.Models.Contact** 데이터 클래스 및 **빈** 보기 콘텐츠를 선택합니다. 빈 보기 콘텐츠 옵션을 선택하면 뷰를 스스로 만들어야 합니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)

**그림 22**: 삭제 확인 보기 추가[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image44.png)

삭제 보기의 내용은 목록 9에 포함되어 있습니다. 이 보기에는 특정 연락처를 삭제할지 여부를 확인하는 양식이 포함되어 있습니다(그림 21 참조).

**리스팅 9 - 보기\홈\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>기본 컨트롤러 이름 변경

연락처작업을 위한 컨트롤러 클래스의 이름이 HomeController 클래스라는 것이 귀찮을 수 있습니다. 컨트롤러의 이름을 ContactController로 지정해야 하지 않습니까?

이 문제는 쉽게 해결할 수 있습니다. 먼저 홈 컨트롤러의 이름을 리팩터링해야 합니다. Visual Studio 코드 편집기에서 HomeController 클래스를 열고 클래스 이름을 마우스 오른쪽 단추로 클릭하고 메뉴 옵션 **이름을 선택합니다.** 이 메뉴 옵션을 선택하면 이름 바꾸기 대화 상자가 열립니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)

**그림 23**: 컨트롤러 이름 리팩터링[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image46.png)

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)

**그림 24**: 이름 바꾸기 대화 상자 사용[(전체 크기 이미지를 보려면 클릭)](iteration-1-create-the-application-vb/_static/image48.png)

컨트롤러 클래스의 이름을 바꾸면 Visual Studio에서 View 폴더의 폴더 이름도 업데이트됩니다. Visual Studio는 \View\Home 폴더의 이름을 \View\Contact 폴더로 바꿉니다.

이 변경 한 후 응용 프로그램에 더 이상 홈 컨트롤러가 없습니다. 응용 프로그램을 실행하면 그림 25의 오류 페이지가 표시됩니다.

[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)

**그림 25**: 기본 컨트롤러 없음[(전체 크기 이미지를 보려면 클릭하십시오)](iteration-1-create-the-application-vb/_static/image50.png)

홈 컨트롤러 대신 연락처 컨트롤러를 사용하려면 Global.asax 파일의 기본 경로를 업데이트해야 합니다. Global.asax 파일을 열고 기본 경로에서 사용하는 기본 컨트롤러를 수정합니다(목록 10 참조).

**리스팅 10 - 글로벌.asax.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

이러한 변경이 끝나면 연락처 관리자가 올바르게 실행됩니다. 이제 연락처 컨트롤러 클래스를 기본 컨트롤러로 사용합니다.

## <a name="summary"></a>요약

이 첫 번째 반복에서는 가능한 가장 빠른 방법으로 기본 연락처 관리자 응용 프로그램을 만들었습니다. Visual Studio를 활용하여 컨트롤러와 뷰에 대한 초기 코드를 자동으로 생성했습니다. 또한 Entity Framework를 활용하여 데이터베이스 모델 클래스를 자동으로 생성했습니다.

현재 연락처 관리자 응용 프로그램을 사용하여 연락처 레코드를 나열, 생성, 편집 및 삭제할 수 있습니다. 즉, 데이터베이스 기반 웹 응용 프로그램에 필요한 모든 기본 데이터베이스 작업을 수행할 수 있습니다.

불행하게도, 우리의 응용 프로그램은 몇 가지 문제가 있습니다. 먼저 나는 이것을 인정하기를 주저, 연락처 관리자 응용 프로그램은 가장 매력적인 응용 프로그램이 아닙니다. 그것은 몇 가지 디자인 작업이 필요합니다. 다음 반복에서는 기본 보기 마스터 페이지와 계단식 스타일 시트를 변경하여 응용 프로그램의 모양을 개선하는 방법을 살펴보겠습니다.

둘째, 양식 유효성 검사를 구현하지 않았습니다. 예를 들어 양식 필드에 대한 값을 입력하지 않고 연락처 만들기 양식을 제출하는 것을 막을 수 있는 방법은 없습니다. 또한 잘못된 전화 번호와 이메일 주소를 입력할 수 있습니다. #3 반복에서 양식 유효성 검사 문제를 해결하기 시작합니다.

마지막으로, 가장 중요한 것은 연락처 관리자 응용 프로그램의 현재 이터레이션을 쉽게 수정하거나 유지 관리할 수 없다는 것입니다. 예를 들어 데이터베이스 액세스 논리는 컨트롤러 작업에 바로 적용됩니다. 즉, 컨트롤러를 수정하지 않으면 데이터 액세스 코드를 수정할 수 없습니다. 이후 반복에서는 연락처 관리자의 변경 복원력을 높이기 위해 구현할 수 있는 소프트웨어 디자인 패턴을 살펴봅니다.

> [!div class="step-by-step"]
> [이전](iteration-7-add-ajax-functionality-cs.md)
> [다음](iteration-2-make-the-application-look-nice-vb.md)
