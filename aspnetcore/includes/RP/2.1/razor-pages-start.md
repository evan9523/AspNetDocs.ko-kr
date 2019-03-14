---
ms.openlocfilehash: 528dafa1ef39982fde2e11428a74c5c26f341554
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033660"
---
기본 템플릿은 **RazorPagesMovie**, **홈**, **정보** 및 **연락처** 링크와 페이지를 만듭니다. 브라우저 창 크기에 따라 탐색 아이콘을 클릭하여 링크를 표시해야 할 수 있습니다.

![홈 또는 인덱스 페이지](~/tutorials/razor-pages/razor-pages-start/_static/home2.png)

링크를 테스트합니다. **RazorPagesMovie** 및 **홈** 링크는 인덱스 페이지로 이동합니다. **정보** 및 **연락처** 링크는 각각 `About` 및 `Contact` 페이지로 이동합니다.

## <a name="project-files-and-folders"></a>프로젝트 파일 및 폴더

다음 표에는 프로젝트의 파일 및 폴더가 나와 있습니다. 이 자습서의 경우 *Startup.cs* 파일을 이해하는 것이 가장 중요합니다. 아래 제공된 각 링크를 검토할 필요는 없습니다. 프로젝트의 파일이나 폴더에 대한 자세한 정보가 필요할 경우 링크가 참조로 제공됩니다.

| 파일 또는 폴더 | 용도 |
| -------------- | ------- |
| *wwwroot* | 고정 자산을 포함합니다. [고정 파일](xref:fundamentals/static-files)을 참조하세요. |
| *페이지* | [Razor 페이지](xref:razor-pages/index)에 대한 폴더입니다. |
| *appsettings.json* | [구성](xref:fundamentals/configuration/index) |
| *Program.cs* | ASP.NET Core 앱의 [호스트](xref:fundamentals/index#host)를 구성합니다. |
| *Startup.cs* | 서비스 및 요청 파이프라인을 구성합니다. [시작](xref:fundamentals/startup)을 참조하세요. |

### <a name="the-pagesshared-folder"></a>Pages/Shared 폴더

*_Layout.cshtml* 파일은 공통적인 HTML 요소(스크립트 및 스타일시트 링크)를 포함하고 앱에 대한 레이아웃을 설정합니다. 예를 들어 **RazorPagesMovie**, **홈****정보** 또는 **연락처**를 선택하면 웹 페이지에서 공통 요소 집합이 표시됩니다. 공통적인 요소에는 창 위쪽의 탐색 메뉴 및 창 아래쪽의 헤더가 포함됩니다. 자세한 내용은 [레이아웃](xref:mvc/views/layout)을 참조하세요.

*_ValidationScriptsPartial.cshtml* 파일은 [jQuery](https://jquery.com/) 유효성 검사 스크립트에 대한 참조를 제공합니다. 자습서의 뒷부분에서 `Create` 및 `Edit` 페이지를 추가하면 *_ValidationScriptsPartial.cshtml* 파일이 사용됩니다.

*_CookieConsentPartial.cshtml* 파일은 개인 정보 및 쿠키 사용 정책을 요약하는 탐색 막대 및 콘텐츠를 제공합니다. 프로젝트에 포함된 GDPR 자산에 대한 자세한 내용은 [ASP.NET Core에서 EU GDPR(일반 데이터 보호 규정) 지원](xref:security/gdpr)을 참조하세요.

### <a name="the-pages-folder"></a>Pages 폴더

*_ViewStart.cshtml*은 Razor 페이지 `Layout` 속성을 설정하여 *_Layout.cshtml* 파일을 사용합니다. 자세한 내용은 [레이아웃](xref:mvc/views/layout)을 참조하세요.

*_ViewImports.cshtml* 파일에는 각 Razor 페이지로 가져온 Razor 지시문이 포함됩니다. 자세한 내용은 [공유된 지시문 가져오기](xref:mvc/views/layout#importing-shared-directives)를 참조하세요.

`About`, `Contact` 및 `Index` 페이지는 앱을 시작하는 데 사용할 수 있는 기본 페이지입니다. `Error` 페이지는 오류 정보를 표시하는 데 사용됩니다.
