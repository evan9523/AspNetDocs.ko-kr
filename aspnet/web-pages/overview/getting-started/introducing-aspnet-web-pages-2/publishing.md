---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: ASP.NET 웹 페이지 소개-WebMatrix를 사용 하 여 사이트 게시 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 ASP.NET 웹 페이지 및 Microsoft WebMatrix를 소개 하는 자습서 집합의 마지막 기사입니다. 사이트를 게시 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: a09339a833ea0b4a2d3c3a9323cce777577ea048
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240589"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>ASP.NET 웹 페이지 소개-WebMatrix를 사용 하 여 사이트 게시

[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서는 ASP.NET 웹 페이지 및 Microsoft WebMatrix를 소개 하는 자습서 집합의 마지막 기사입니다. 다른 사람이 사용할 수 있도록 사이트를 인터넷에 게시 하는 방법을 설명 합니다. [ASP.NET 웹 페이지 사이트에 대 한 일관 된 검색을 만들어](https://go.microsoft.com/fwlink/?LinkId=251585)시리즈를 완료 했다고 가정 합니다.
> 
> 다음을 사용 하 여 사이트를 게시 하는 방법을 알아봅니다.
> 
> - Microsoft Azure
> - 웹 호스팅 회사

## <a name="about-publishing-your-site"></a>사이트 게시 정보

지금까지 페이지 테스트를 포함 하 여 로컬 컴퓨터에서 모든 작업을 완료 했습니다. <em>Cshtml</em> 페이지를 실행 하려면 WebMatrix에 내장 된 웹 서버 (IIS Express)를 사용 했습니다. 그러나 사용자를 제외 하 고 만든 사이트는 아무도 볼 수 없습니다. 다른 사용자가 사이트를 사용할 수 있도록 하려면 인터넷에 게시 해야 합니다.

공용 웹 서버에 대 한 액세스 권한이 없는 경우 게시는 *클라우드 플랫폼* 또는 *호스팅 공급자*의 계정이 있어야 함을 의미 합니다. Microsoft Azure와 같은 클라우드 플랫폼은 응용 프로그램에 주문형 인프라를 제공 합니다. 호스팅 공급자는 공개적으로 액세스할 수 있는 웹 서버를 소유 하 고 있으며 사이트의 공간을 임대 하는 회사입니다. 호스팅 계획은 대용량 상용 웹 사이트를 위해 작은 사이트에 대해 몇 달러 (또는 무료)에서 수백 달러의 월로 실행 됩니다.

> [!NOTE]
> 집에서 인터넷 서비스를 가져오는 데 사용 하는 ISP (인터넷 서비스 공급자)를 통해 공용 웹 서버에 액세스할 수 있습니다. 그러나 호스팅 공급자는 ASP.NET 웹 페이지을 지원 해야 합니다. 대부분의 Isp는 그렇지 않지만 항상 확인 하는 것이 좋습니다.

이 자습서에서는 게시 하는 방법에 대 한 개요를 제공 합니다. 모든 호스팅 공급자에 대해 프로세스가 약간 다르므로 모든 항목에 대 한 정확한 세부 정보를 제공 하는 것은 실용적이 지 않습니다. 그러나 프로세스가 작동 하는 방식을 이해 하는 것이 좋습니다.

이 자습서에는 다음 4 개의 섹션이 포함 되어 있습니다.

1. [기본 페이지 설정](#defaultpage)
2. 게시 (다음 중 하나 선택)  
 a. [Microsoft Azure에 사이트 게시](#azure)  
 b. [웹 호스팅 회사에 사이트 게시](#host)
3. [라이브 사이트 업데이트: 다시 게시](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>기본 페이지 설정

사용자가 웹 사이트의 기본 주소로 이동 하면 사이트의 기본 페이지가 사용자에 게 표시 됩니다. 예를 들어 *Default.htm* 이 사이트에 대 한 기본 페이지로 설정 된 경우로 이동 하는 것 `www.contoso.com` `www.contoso.com` 은로 이동 하는 것과 같습니다 `www.contoso.com/Default.htm` .

현재 사이트에서 기본 페이지로 **기본값. cshtml** 을 사용 합니다. 이 페이지는 기본 페이지에는 적합 하지만이 자습서에서는 빈 페이지가 표시 되도록 해당 페이지에 콘텐츠를 추가 하지 않았습니다. 기본. cshtml를 열고 내용을 다음 코드로 바꿉니다.

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

이제 사이트를 게시할 준비가 되었습니다. 먼저 사이트를 Azure에 배포 하는 방법 및 웹 호스팅 회사에 배포 하는 방법을 확인 합니다. 두 옵션 중 하나는 웹 사이트에서 작동 하며, 배포 옵션 중 하나를 수행 하기만 하면 됩니다.

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>Microsoft Azure에 사이트 게시

이 자습서에서는 먼저 Microsoft Azure에 사이트를 배포 하는 방법을 보여 줍니다. Microsoft 계정를 사용 하 여 로그인 하면 Azure에서 최대 10 개의 무료 사이트를 만들 수 있습니다. 이러한 무료 사이트는 사이트를 테스트 하는 편리한 방법을 제공 합니다. 모든 무료 사이트를 사용 하지 않도록 하려면 나중에이 예제 사이트를 언제 든 지 삭제할 수 있습니다. 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/free/dotnet/)을 참조하세요.

WebMatrix 리본에서 **게시** 단추를 클릭 합니다.

![WebMatrix 리본의 ' 게시 ' 단추](publishing/_static/image1.png)

**사이트 게시** 대화 상자가 표시 됩니다. Microsoft 계정에 로그인 하지 않은 경우 대화 상자에 **Azure 시작** 링크가 포함 됩니다. 이 링크를 클릭 합니다.

![사이트 게시](publishing/_static/image2.png)

Microsoft 계정에 로그인 하지 않은 경우에는 다시 로그인 할 수 있는 기회가 제공 됩니다. Microsoft 계정에 로그인 하 여 Azure에서 사이트를 게시 해야 합니다.

![링크를](publishing/_static/image3.png)

Microsoft 계정에 로그인 한 후에는 Azure에서 새 사이트를 만들거나 Azure의 기존 사이트 중 하나에 연결할 수 있는 링크가 대화 상자에 포함 되어 있습니다.

![새 사이트 만들기](publishing/_static/image4.png)

**새 사이트 만들기를**선택 합니다.

프로젝트의 이름을 **Webpagesmovies**로 지정 하면 사이트의 기본 이름이 **webpagesmovies.azurewebsites.net**됩니다. 이 기본 이름은 빨간색 느낌표로 표시 된 것과 같이 사용 하지 않을 가능성이 높습니다.

![기본 웹 사이트 이름](publishing/_static/image5.png)

사이트 이름을 사용할 수 있는 항목으로 변경 하 고 위치에 가까운 위치를 선택 합니다.

![변경 된 사이트 이름](publishing/_static/image6.png)

**확인**을 클릭합니다.

WebMatrix performss 서버가 사이트와 호환 되는지 확인 하는 테스트를 시작 합니다.

![호환성 테스트](publishing/_static/image7.png)

**계속**을 선택합니다.

호환성 테스트 결과가 표시 됩니다.

![호환성 결과](publishing/_static/image8.png)

**계속**을 선택합니다.

WebMatrix 사이트에 게시 될 파일 및 데이터베이스를 표시 합니다. 처음으로 사이트를 게시 하는 중 이므로 모든 파일이 나열 됩니다. 게시할 준비가 되지 않은 파일은 선택 취소할 수 있습니다. 이후 게시에서는 변경 된 파일만 표시 됩니다. [라이브 사이트 업데이트: 다시 게시](#update)를 참조 하십시오.

![게시 미리 보기](publishing/_static/image9.png)

**계속**을 선택합니다.

사이트가 Azure에 배포 된 후 배포가 완료 되었음을 나타내는 메시지가 표시 됩니다.

![게시 완료](publishing/_static/image10.png)

사이트와 데이터베이스가 Azure에 게시 되었으며 이제 공용에서 사용할 수 있습니다. 게시가 완료 되었음을 나타내는 메시지의 링크를 클릭 하면 배포 된 사이트가 표시 됩니다. 사용자 또는 인터넷에 액세스할 수 있는 모든 사용자가 데이터베이스에서 레코드를 추가 하거나 수정할 수 있습니다.

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>웹 호스팅 회사에 사이트 게시

Azure에 게시 하지 않기로 결정 한 경우 웹 호스팅 회사에 사이트를 게시할 수 있습니다.

**웹 호스팅 검색** 링크를 클릭 합니다.

![게시 설정 대화 상자에서 ' 웹 호스팅 찾기 ' 단추](publishing/_static/image12.png)

ASP.NET를 지 원하는 호스팅 공급자가 나열 된 Microsoft 사이트 페이지로 이동 합니다.

![호스팅 공급자가 나열 된 Microsoft 사이트 페이지](publishing/_static/image13.png)

물론 장기적으로 필요한 호스팅 기능을 정확 하 게 파악 하기 어려울 수 있습니다. 다음은 고려해 야 할 몇 가지 사항입니다.

- WebPagesMovies 사이트의 목적에 따라 SQL Server에 대 한 별도의 추가 기능이 필요 하지 않으므로 비용이 많이 듭니다. 사이트에서 자체 포함 된 SQL Server Compact Edition을 사용 하 고 있습니다. 그러나 앞으로 수행 하는 몇 가지 웹 사이트 작업에 대 한 SQL Server 액세스 권한이 필요할 수 있습니다. 가능 하다 고 생각 되 면 나중에 SQL Server 기능을 추가할 수 있는지 확인 합니다.
- 호스팅 공급자가 웹 배포 게시 프로토콜을 지원 하는지 여부를 확인 합니다. FTP 프로토콜을 사용 하 여 게시할 수 있지만 웹 배포 사용 하는 것이 더 편리 합니다.

일부 사이트는 무료 평가판 기간을 제공 합니다. WebMatrix를 사용 하 여 계속 실험 하 고 ASP.NET 웹 페이지 하는 동안 무료 평가판은 게시 및 호스팅을 시도 하는 좋은 방법입니다.

원하는 항목을 선택 합니다. 이 자습서에서는 DiscountASP.NET를 선택 했습니다. 자습서를 만드는 동안 해당 회사에는 몇 달 동안 사이트를 무료로 호스트할 수 있는 판촉이 있습니다.

> [!NOTE]
> 이 자습서의 호스팅 공급자를 선택 하는 것은 다른 회사에 대 한 해당 회사의 보증으로 해석 되어서는 안 됩니다. 그러나 설명을 위해 하나를 선택 해야 하 고 DiscountASP.NET는 ASP.NET 웹 페이지을 지 원하는 여러 회사 중 하 나와 게시를 위한 웹 배포 프로토콜입니다.

일반적으로 호스팅 공급자에 등록 한 후 회사는 사용자 이름 및 암호, 웹 서버의 URL 등을 포함 하는 전자 메일을 보냅니다. 호스팅 회사에서 웹 배포 프로토콜을 지 원하는 경우 게시 설정을 포함 하는 파일을 보내거나 다운로드할 수 있습니다. 게시 설정 파일은 프로세스를 간소화 합니다.

등록 하 고 게시할 준비가 되 면 WebMatrix 리본에서 **게시** 단추를 클릭 합니다. **게시 설정** 대화 상자가 표시 됩니다.

호스팅 공급자가 게시 설정 파일을 보낸 경우 **게시 설정 가져오기** 링크를 클릭 하 고 파일을 가져옵니다. 게시 설정 파일이 없는 경우 호스팅 회사에서 전자 메일로 보낸 값을 사용 하 여 필드를 입력 합니다. 완료 되 면 **게시 설정** 대화 상자는 다음과 같습니다.

![' 게시 설정 ' 대화 상자에 채워진 게시 설정](publishing/_static/image14.png)

**연결 유효성 검사**를 클릭 합니다. 모든 항목이 양호 하면 대화 상자가 **성공적으로 연결**된 것입니다. 즉, 호스팅 공급자의 서버와 통신할 수 있습니다.

![게시 설정이 올바르면 성공 메시지](publishing/_static/image15.png)

문제가 발생 하는 경우 WebMatrix는 문제의 원인을 알려 주는 것이 가장 좋습니다.

![게시 설정에 문제가 있는 경우 오류 메시지](publishing/_static/image16.png)

**Save** 를 클릭하여 설정을 저장합니다. WebMatrix는 테스트를 수행 하 여 호스팅 사이트와 올바르게 통신할 수 있는지 확인 합니다.

![게시 프로세스의 테스트를 수행 하는 메시지 제공](publishing/_static/image17.png)

**예**를 클릭합니다. WebMatrix는 일부 샘플 파일을 호스팅 공급자에 업로드 합니다. 호환성 테스트가 완료 되 면 WebMatrix는 결과를 보고 합니다.

![게시 테스트의 결과](publishing/_static/image18.png)

준비가 되 면 계속 진행 하 고 **계속** 을 클릭 하 여 실제 게시 프로세스를 시작 합니다. WebMatrix는 사이트에 있으며 이미 호스트 서버에 있는 파일 (현재는 없음)을 파악 하 고 게시 프로세스의 미리 보기를 제공 합니다.

![게시 프로세스에서 업로드할 파일의 미리 보기](publishing/_static/image19.png)

게시할 파일 목록에는 *동영상과*같이 만든 웹 페이지가 포함 됩니다. 이 목록에는 사용자가 설치한 도우미에 대 한 파일, 데이터베이스의 SQL Server Compact Edition을 실행 하는 데 사용할 파일 등도 포함 되어 있습니다. 결과적으로 초기 게시 프로세스가 상당히 될 수 있습니다.

**Continue(계속)** 를 클릭합니다. WebMatrix는 호스팅 공급자의 서버에 파일을 복사 합니다. 작업이 완료 되 면 상태 표시줄에 결과가 보고 됩니다.

![게시 프로세스가 성공적으로 완료 된 경우의 상태 표시줄 메시지](publishing/_static/image20.png)

라이브 사이트를 보려면 상태 표시줄의 링크를 클릭 합니다. URL에 *영화* 를 추가 하면 사용자가 만든 *동영상과* 파일이 표시 됩니다.

![동영상 페이지를 표시 하는 라이브 사이트](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>라이브 사이트 업데이트: 다시 게시

Azure 또는 웹 호스팅 회사에 사이트를 게시 한 후에는 &mdash; 컴퓨터의 버전과 서비스 공급자의 버전 중 두 개의 복사본이 있습니다. 사이트를 계속 개발할 수 있습니다 (다른 작업을 수행 하는 경우 다음 자습서의 일부로). 이렇게 하면 컴퓨터의 변경 내용을 서비스 공급자로 복사 하기 위해 사이트를 다시 게시 해야 합니다. WebMatrix의 게시 프로세스는 사이트에서 변경 된 파일을 확인 하 고 해당 파일만 게시할 수 있습니다.

재게시가 어떻게 작동 하는지 확인 하려면 *동영상. cshtml* 사이트를 열고 약간 변경 하 고 파일을 저장 합니다. 예를 들어 제목을로 변경 합니다 `Movies - Updated` .

리본에서 **게시** 단추를 클릭 합니다. WebMatrix는 변경 된 내용을 확인 하 고 게시 되는 파일의 미리 보기를 표시 합니다.

![다시 게시할 준비가 된 변경 된 파일을 보여 주는 ' 게시 ' 대화 상자](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> 기본적으로 WebMatrix는 처음 사이트를 게시할 때만 데이터베이스 (*.sdf* 파일)를 게시 합니다. 사이트가 게시 되 고 사람들이 웹 사이트와 상호 작용 하는 경우 라이브 사이트의 데이터베이스에는 일반적으로 사이트의 실제 데이터가 포함 됩니다. 일반적으로 테스트 데이터만 포함 하는 컴퓨터에 있는 *.sdf* 파일로 라이브 데이터베이스를 덮어쓰지 않도록 주의 해야 합니다. 이러한 이유로 **인해 게시는 원격 데이터베이스를 덮어쓰고**webstels 확인란은 기본적으로 선택 취소 되어 *WebPagesMovies.sdf* 있습니다.

**Continue(계속)** 를 클릭합니다. WebMatrix는 처음 게시 했을 때와 같이 변경 된 파일을 게시 하 고 성공 메시지를 표시 합니다.

라이브 사이트로 이동 하 고 (계속 표시 되는 경우 성공 메시지의 링크를 클릭 하 여) 변경 내용이 게시 되었는지 확인 합니다.

> [!TIP] 
> 
> **원격으로 파일 편집**
> 
> 사이트를 변경 하 고 다시 게시 하는 대신 WebMatrix에서 직접 원격 파일을 편집할 수 있습니다. 이 시나리오에서는 서비스 공급자에 있는 파일을 열고 WebMatrix는 편집할 수 있도록 해당 파일의 복사본을 다운로드 합니다. WebMatrix는 파일을 저장할 때마다 변경 내용을 사이트로 보냅니다.
> 
> 원격 편집은 라이브 사이트를 변경 하는 쉬운 방법입니다. 그러나이 방법으로 변경한 내용은 로컬 사이트의 파일과 동기화 되지 않습니다. 로컬 파일을 원격 사이트와 동기화 하기 위해 원격 파일을 다운로드할 수 있습니다. 이 프로세스는 역방향을 제외 하 고 게시와 매우 유사 하 게 작동 합니다.
> 
> 여기에서는 WebMatrix의 원격 편집 및 원격 다운로드 기능에 대해 자세히 설명 하지 않습니다. 여러 사용자가 서로 다른 컴퓨터의 동일한 사이트에서 작업 해야 하는 경우에 매우 유용 합니다. 자세한 내용은 [WebMatrix 2 Beta를 사용 하 여 원격 사이트 게시 및 편집](https://go.microsoft.com/fwlink/?LinkId=251591)을 참조 하세요.

## <a name="additional-resources"></a>추가 리소스

- [ASP.NET WebMatrix ASP.NET 웹 페이지 포럼](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages)에서 질문을 게시 하 고 답변을 얻을 수 있는 좋은 장소입니다.

> [!div class="step-by-step"]
> [이전](layouts.md)
