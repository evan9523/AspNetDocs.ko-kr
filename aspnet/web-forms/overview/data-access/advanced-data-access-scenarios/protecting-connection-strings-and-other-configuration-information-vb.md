---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-vb
title: 연결 문자열 및 기타 구성 정보 보호 (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET 응용 프로그램은 일반적으로 Web.config 파일에 구성 정보를 저장 합니다. 이 정보 중 일부는 중요 하며 보호를 보증 합니다. Def ...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: cd17dbe1-c5e1-4be8-ad3d-57233d52cef1
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/protecting-connection-strings-and-other-configuration-information-vb
msc.type: authoredcontent
ms.openlocfilehash: 070e1dccb80ef9af21ea621357c5b23e2ada6f9f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421001"
---
# <a name="protecting-connection-strings-and-other-configuration-information-vb"></a>연결 문자열 및 기타 구성 정보 보호(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_73_VB.zip) 또는 [PDF 다운로드](protecting-connection-strings-and-other-configuration-information-vb/_static/datatutorial73vb1.pdf)

> ASP.NET 응용 프로그램은 일반적으로 Web.config 파일에 구성 정보를 저장 합니다. 이 정보 중 일부는 중요 하며 보호를 보증 합니다. 기본적으로이 파일은 웹 사이트 방문자에 게 제공 되지 않지만 관리자나 해커가 웹 서버의 파일 시스템에 액세스 하 여 파일의 내용을 볼 수 있습니다. 이 자습서에서는 ASP.NET 2.0에서 web.config 파일의 섹션을 암호화 하 여 중요 한 정보를 보호할 수 있는 방법을 알아봅니다.

## <a name="introduction"></a>소개

ASP.NET 응용 프로그램에 대 한 구성 정보는 일반적으로 `Web.config`이라는 XML 파일에 저장 됩니다. 이러한 자습서를 진행 하는 동안 `Web.config`를 몇 번 업데이트 했습니다. 예를 들어 [첫 번째 자습서](../introduction/creating-a-data-access-layer-vb.md)에서 `Northwind` 형식화 된 데이터 집합을 만들 때 연결 문자열 정보는 `<connectionStrings>` 섹션의 `Web.config`에 자동으로 추가 됩니다. 나중에 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서에서 `Web.config`를 수동으로 업데이트 하 여 프로젝트의 모든 ASP.NET 페이지가 `DataWebControls` 테마를 사용 해야 함을 나타내는 `<pages>` 요소를 추가 합니다.

`Web.config`에는 연결 문자열과 같은 중요 한 데이터가 포함 될 수 있기 때문에 `Web.config`의 콘텐츠를 안전 하 게 유지 하 고 권한이 없는 뷰어에 숨어 두어야 합니다. 기본적으로 `.config` 확장을 사용 하는 파일에 대 한 모든 HTTP 요청은 그림 1에 표시 된 *이 유형의 페이지를 제공 하지 않는* 메시지를 반환 하는 ASP.NET 엔진에 의해 처리 됩니다. 즉, 방문자는 브라우저의 주소 표시줄에 http://www.YourServer.com/Web.config를 입력 하기만 하면 `Web.config` 파일의 내용을 볼 수 없습니다.

[브라우저를 통해 web.config를 방문 하면이 형식의 페이지가 제공 되지 않습니다. 메시지를 반환 ![](protecting-connection-strings-and-other-configuration-information-vb/_static/image2.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image1.png)

**그림 1**: 브라우저를 통해 `Web.config`를 방문 하면이 형식의 페이지가 제공 되지 않습니다 ([전체 크기 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-vb/_static/image3.png)).

그러나 공격자가 `Web.config` 파일 s 내용을 볼 수 있는 다른 악용을 찾을 수 있는 경우는 어떻게 되나요? 공격자가이 정보를 사용 하 여 수행할 수 있는 작업 및 `Web.config`내에서 중요 한 정보를 추가로 보호 하기 위해 수행할 수 있는 단계는 무엇 인가요? 다행히 `Web.config`의 대부분 섹션에는 중요 한 정보가 포함 되어 있지 않습니다. 공격자가 ASP.NET 페이지에서 사용 하는 기본 테마의 이름을 알고 있는 경우 어떤 피해를 perpetrate?

그러나 특정 `Web.config` 섹션에는 연결 문자열, 사용자 이름, 암호, 서버 이름, 암호화 키 등을 포함할 수 있는 중요 한 정보가 포함 되어 있습니다. 이 정보는 일반적으로 다음 `Web.config` 섹션에서 찾을 수 있습니다.

- `<appSettings>`
- `<connectionStrings>`
- `<identity>`
- `<sessionState>`

이 자습서에서는 이러한 중요 한 구성 정보를 보호 하는 기술을 살펴봅니다. 여기에서 볼 수 있듯이 .NET Framework 버전 2.0에는 프로그래밍 방식으로 선택 된 구성 섹션을 암호화 하 고 암호 해독 하는 데 사용 되는 보호 된 구성 시스템이 포함 되어 있습니다.

> [!NOTE]
> 이 자습서에서는 ASP.NET 응용 프로그램에서 데이터베이스에 연결 하는 데 필요한 Microsoft s 권장 사항에 대해 살펴봅니다. 연결 문자열을 암호화 하는 것 외에도 안전 하 게 데이터베이스에 연결 하 여 시스템을 강화 하는 데 도움이 될 수 있습니다.

## <a name="step-1-exploring-aspnet-20-s-protected-configuration-options"></a>1 단계: ASP.NET 2.0 s 보호 된 구성 옵션 탐색

ASP.NET 2.0에는 구성 정보를 암호화 및 암호 해독 하기 위한 보호 된 구성 시스템이 포함 되어 있습니다. 여기에는 프로그래밍 방식으로 구성 정보를 암호화 하거나 암호 해독 하는 데 사용할 수 있는 .NET Framework 메서드가 포함 됩니다. 보호 된 구성 시스템은 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)을 사용 하 여 개발자가 어떤 암호화 구현을 사용할 것인지 선택할 수 있습니다.

.NET Framework는 두 개의 보호 된 구성 공급자와 함께 제공 됩니다.

- [`RSAProtectedConfigurationProvider`](https://msdn.microsoft.com/library/system.configuration.rsaprotectedconfigurationprovider.aspx) -암호화 및 암호 해독에 비대칭 [RSA 알고리즘](http://en.wikipedia.org/wiki/Rsa) 을 사용 합니다.
- [`DPAPIProtectedConfigurationProvider`](https://msdn.microsoft.com/system.configuration.dpapiprotectedconfigurationprovider.aspx) -암호화 및 암호 해독을 위해 Windows [DPAPI (데이터 보호 API)](https://msdn.microsoft.com/library/ms995355.aspx) 를 사용 합니다.

보호 된 구성 시스템은 공급자 디자인 패턴을 구현 하므로 사용자가 보호 하는 구성 공급자를 만들어 응용 프로그램에 연결할 수 있습니다. 이 프로세스에 대 한 자세한 내용은 [보호 된 구성 공급자 구현](https://msdn.microsoft.com/library/wfc2t3az(VS.80).aspx) 을 참조 하세요.

RSA 및 DPAPI 공급자는 암호화 및 암호 해독 루틴에 키를 사용 하며 이러한 키는 컴퓨터 또는 사용자 수준에서 저장할 수 있습니다. 컴퓨터 수준 키는 웹 응용 프로그램이 자체 전용 서버에서 실행 되거나 암호화 된 정보를 공유 해야 하는 서버에 여러 응용 프로그램이 있는 경우에 적합 합니다. 사용자 수준 키는 동일한 서버의 다른 응용 프로그램이 보호 된 응용 프로그램 구성 섹션의 암호를 해독할 수 없는 공유 호스팅 환경에서 보다 안전한 옵션입니다.

이 자습서에서는 DPAPI 공급자와 컴퓨터 수준 키를 사용 합니다. 특히 보호 된 구성 시스템을 사용 하 여 대부분의 `Web.config` 섹션을 암호화할 수 있지만 `Web.config`에서 `<connectionStrings>` 섹션을 암호화 하는 것을 확인할 수 있습니다. 사용자 수준 키를 사용 하거나 RSA 공급자를 사용 하는 방법에 대 한 자세한 내용은이 자습서의 끝부분에 있는 추가 판독값 섹션의 리소스를 참조 하세요.

> [!NOTE]
> `RSAProtectedConfigurationProvider` 및 `DPAPIProtectedConfigurationProvider` 공급자는 각각 공급자 이름 `RsaProtectedConfigurationProvider` 및 `DataProtectionConfigurationProvider`를 사용 하 여 `machine.config` 파일에 등록 됩니다. 구성 정보를 암호화 하거나 암호를 해독할 때 실제 형식 이름 (`RSAProtectedConfigurationProvider` 및 `DPAPIProtectedConfigurationProvider`) 대신 적절 한 공급자 이름 (`RsaProtectedConfigurationProvider` 또는 `DataProtectionConfigurationProvider`)을 제공 해야 합니다. `$WINDOWS$\Microsoft.NET\Framework\version\CONFIG` 폴더에서 `machine.config` 파일을 찾을 수 있습니다.

## <a name="step-2-programmatically-encrypting-and-decrypting-configuration-sections"></a>2 단계: 프로그래밍 방식으로 구성 섹션 암호화 및 암호 해독

몇 줄의 코드를 사용 하 여 지정 된 공급자를 사용 하 여 특정 구성 섹션을 암호화 하거나 암호 해독할 수 있습니다. 곧 확인할 수 있듯이 코드는 적절 한 구성 섹션을 프로그래밍 방식으로 참조 하 고 `ProtectSection` 또는 `UnprotectSection` 메서드를 호출한 다음 `Save` 메서드를 호출 하 여 변경 내용을 유지 하기만 하면 됩니다. 또한 .NET Framework에는 구성 정보를 암호화 하 고 해독할 수 있는 유용한 명령줄 유틸리티가 포함 되어 있습니다. 3 단계의이 명령줄 유틸리티를 살펴보겠습니다.

구성 정보를 프로그래밍 방식으로 보호 하는 방법을 설명 하기 위해 `Web.config`에서 `<connectionStrings>` 섹션을 암호화 하 고 암호를 해독 하는 단추를 포함 하는 ASP.NET 페이지를 만들어 보겠습니다.

먼저 `AdvancedDAL` 폴더에서 `EncryptingConfigSections.aspx` 페이지를 엽니다. TextBox 컨트롤을 도구 상자에서 디자이너로 끌어 `ID` 속성을 `WebConfigContents`, `TextMode` 속성을 `MultiLine`, `Width` 및 `Rows` 속성을 각각 95% 및 15로 설정 합니다. 이 TextBox 컨트롤은 콘텐츠가 암호화 되는지 여부를 신속 하 게 확인할 수 있도록 `Web.config`의 내용을 표시 합니다. 물론 실제 응용 프로그램에서는 `Web.config`의 내용을 표시 하지 않을 것입니다.

텍스트 상자 아래에 `EncryptConnStrings` 및 `DecryptConnStrings`라는 두 개의 Button 컨트롤을 추가 합니다. 텍스트 속성을 설정 하 여 연결 문자열을 암호화 하 고 연결 문자열의 암호를 해독 합니다.

이 시점에서 화면은 그림 2와 유사 하 게 표시 됩니다.

[텍스트 상자와 두 개의 단추 웹 컨트롤을 페이지에 추가 ![](protecting-connection-strings-and-other-configuration-information-vb/_static/image5.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image4.png)

**그림 2**: 텍스트 상자와 두 개의 단추 웹 컨트롤을 페이지에 추가 ([전체 크기 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-vb/_static/image6.png))

다음으로 페이지가 처음 로드 될 때 `WebConfigContents` 텍스트 상자에 `Web.config` 내용을 로드 하 고 표시 하는 코드를 작성 해야 합니다. 페이지의 코드 숨김이 클래스에 다음 코드를 추가 합니다. 이 코드는 `DisplayWebConfig` 라는 메서드를 추가 하 고 `Page.IsPostBack` `False`때 `Page_Load` 이벤트 처리기에서 호출 합니다.

[!code-vb[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample1.vb)]

`DisplayWebConfig` 메서드는 [`File` 클래스](https://msdn.microsoft.com/library/system.io.file.aspx) 를 사용 하 여 응용 프로그램 `Web.config` 파일을 열고 [`StreamReader` 클래스](https://msdn.microsoft.com/library/system.io.streamreader.aspx) 를 사용 하 여 콘텐츠를 문자열로 읽고 [`Path` 클래스](https://msdn.microsoft.com/library/system.io.path.aspx) 를 사용 하 여 `Web.config` 파일의 실제 경로를 생성 합니다. 이러한 세 클래스는 모두 [`System.IO` 네임 스페이스](https://msdn.microsoft.com/library/system.io.aspx)에 있습니다. 따라서 코드를 사용 하는 클래스의 맨 위에 `Imports``System.IO` 문을 추가 하거나 이러한 클래스 이름 앞에 `System.IO.`를 추가 해야 합니다.

그런 다음 이벤트 `Click` 두 단추 컨트롤에 대 한 이벤트 처리기를 추가 하 고 DPAPI 공급자를 사용 하 여 컴퓨터 수준 키를 사용 하 여 `<connectionStrings>` 섹션을 암호화 하 고 암호 해독 하는 데 필요한 코드를 추가 해야 합니다. 디자이너에서 각 단추를 두 번 클릭 하 여 코드 숨김으로 된 클래스에 `Click` 이벤트 처리기를 추가한 후 다음 코드를 추가 합니다.

[!code-vb[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample2.vb)]

두 이벤트 처리기에서 사용 되는 코드는 거의 동일 합니다. 둘 다 [`WebConfigurationManager` 클래스](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.aspx) 의 [`OpenWebConfiguration` 메서드](https://msdn.microsoft.com/library/system.web.configuration.webconfigurationmanager.openwebconfiguration.aspx)를 통해 현재 응용 프로그램 `Web.config` 파일에 대 한 정보를 가져오는 것으로 시작 합니다. 이 메서드는 지정 된 가상 경로에 대 한 웹 구성 파일을 반환 합니다. 그런 다음 `Web.config` 파일 s `<connectionStrings>` 섹션은 [`Configuration` 클래스](https://msdn.microsoft.com/library/system.configuration.configuration.aspx) s [`GetSection(sectionName)` 메서드](https://msdn.microsoft.com/library/system.configuration.configuration.getsection.aspx)를 통해 액세스 합니다 .이 메서드는 [`ConfigurationSection`](https://msdn.microsoft.com/library/system.configuration.configurationsection.aspx) 개체를 반환 합니다.

`ConfigurationSection` 개체는 구성 섹션과 관련 된 추가 정보 및 기능을 제공 하는 [`SectionInformation` 속성](https://msdn.microsoft.com/library/system.configuration.configurationsection.sectioninformation.aspx) 을 포함 합니다. 위의 코드에서 볼 수 있듯이 `SectionInformation` 속성 `IsProtected` 속성을 확인 하 여 구성 섹션이 암호화 되는지 여부를 확인할 수 있습니다. 또한 `SectionInformation` 속성 s `ProtectSection(provider)` 및 `UnprotectSection` 메서드를 통해 섹션을 암호화 하거나 암호를 해독할 수 있습니다.

`ProtectSection(provider)` 메서드는 암호화할 때 사용할 보호 된 구성 공급자의 이름을 지정 하는 문자열을 입력으로 받아들입니다. `EncryptConnString` 단추 s 이벤트 처리기에서 DPAPI 공급자가 사용 되도록 DataProtectionConfigurationProvider를 `ProtectSection(provider)` 메서드로 전달 합니다. `UnprotectSection` 메서드는 구성 섹션을 암호화 하는 데 사용 된 공급자를 확인할 수 있으므로 입력 매개 변수가 필요 하지 않습니다.

`ProtectSection(provider)` 또는 `UnprotectSection` 메서드를 호출한 후에는 `Configuration` 개체 s [`Save` 메서드](https://msdn.microsoft.com/library/system.configuration.configuration.save.aspx) 를 호출 하 여 변경 내용을 유지 해야 합니다. 구성 정보를 암호화 하거나 암호를 해독 하 고 변경 내용을 저장 한 후에는 `DisplayWebConfig`를 호출 하 여 텍스트 상자 컨트롤에 업데이트 된 `Web.config` 콘텐츠를 로드 합니다.

위의 코드를 입력 한 후 브라우저를 통해 `EncryptingConfigSections.aspx` 페이지를 방문 하 여 테스트 합니다. 처음에는 `<connectionStrings>` 섹션이 일반 텍스트로 표시 된 `Web.config`의 내용을 나열 하는 페이지가 표시 됩니다 (그림 3 참조).

[텍스트 상자와 두 개의 단추 웹 컨트롤을 페이지에 추가 ![](protecting-connection-strings-and-other-configuration-information-vb/_static/image8.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image7.png)

**그림 3**: 텍스트 상자와 두 개의 단추 웹 컨트롤을 페이지에 추가 ([전체 크기 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-vb/_static/image9.png))

이제 연결 문자열 암호화 단추를 클릭 합니다. 요청 유효성 검사를 사용 하도록 설정 하는 경우 `WebConfigContents` 텍스트 상자에서 다시 게시 된 태그는 메시지를 표시 하는 `HttpRequestValidationException`을 생성 하 고 잠재적으로 위험한 `Request.Form` 값이 클라이언트에서 검색 된 것입니다. ASP.NET 2.0에서 기본적으로 사용 하도록 설정 된 요청 유효성 검사는 인코딩되지 않은 HTML을 포함 하는 포스트백을 금지 하 고 스크립트 삽입 공격을 방지 하도록 디자인 되었습니다. 이 검사는 페이지 또는 응용 프로그램 수준에서 사용 하지 않도록 설정할 수 있습니다. 이 페이지에서이 기능을 해제 하려면 `@Page` 지시어에서 `ValidateRequest` 설정을 `False`로 설정 합니다. `@Page` 지시문은 페이지의 선언적 태그 맨 위에 있습니다.

[!code-aspx[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample3.aspx)]

요청 유효성 검사, 용도, 페이지 및 응용 프로그램 수준에서이 기능을 사용 하지 않도록 설정 하는 방법 및 태그를 HTML 인코딩하는 방법에 대 한 자세한 내용은 [요청 유효성 검사-스크립트 공격 방지](../../../../whitepapers/request-validation.md)를 참조 하세요.

페이지에 대 한 요청 유효성 검사를 사용 하지 않도록 설정한 후에는 연결 문자열 암호화 단추를 다시 클릭 합니다. 다시 게시 하는 경우 구성 파일에 액세스 하 고 DPAPI 공급자를 사용 하 여 `<connectionStrings>` 섹션을 암호화 합니다. 그러면 텍스트 상자가 업데이트 되어 새 `Web.config` 콘텐츠가 표시 됩니다. 그림 4에 표시 된 것 처럼 `<connectionStrings>` 정보가 암호화 됩니다.

[연결 문자열 암호화 단추를 클릭 하 ![&lt;connectionString&gt; 섹션을 암호화 합니다.](protecting-connection-strings-and-other-configuration-information-vb/_static/image11.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image10.png)

**그림 4**: 연결 문자열 암호화 단추를 클릭 하면 `<connectionString>` 섹션이 암호화 됩니다 ([전체 크기 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-vb/_static/image12.png)).

내 컴퓨터에서 생성 된 암호화 된 `<connectionStrings>` 섹션이 다음을 위해 `<CipherData>` 요소의 일부 콘텐츠가 제거 되었습니다.

[!code-xml[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample4.xml)]

> [!NOTE]
> `<connectionStrings>` 요소는 암호화 (`DataProtectionConfigurationProvider`)를 수행 하는 데 사용 되는 공급자를 지정 합니다. 이 정보는 연결 문자열 암호 해독 단추를 클릭할 때 `UnprotectSection` 메서드에서 사용 됩니다.

`Web.config`에서 연결 문자열 정보에 액세스 하는 경우, SqlDataSource 컨트롤 또는 형식화 된 데이터 집합의 Tableadapter에서 자동 생성 된 코드에서 코드를 작성 합니다. 그러면 자동으로 암호가 해독 됩니다. 간단히 말해서 암호화 된 `<connectionString>` 섹션의 암호를 해독 하는 추가 코드 또는 논리를 추가할 필요가 없습니다. 이를 보여 주기 위해 기본 보고 섹션 (`~/BasicReporting/SimpleDisplay.aspx`)의 간단한 표시 자습서와 같은 이전 자습서 중 하나를 방문해 보세요. 그림 5와 같이 자습서는 정상적으로 작동 하는 것과 동일 하 게 작동 하며,이는 암호화 된 연결 문자열 정보가 ASP.NET 페이지에 의해 자동으로 해독 됨을 나타냅니다.

[데이터 액세스 계층 ![자동으로 연결 문자열 정보를 해독 합니다.](protecting-connection-strings-and-other-configuration-information-vb/_static/image14.png)](protecting-connection-strings-and-other-configuration-information-vb/_static/image13.png)

**그림 5**: 데이터 액세스 계층이 자동으로 연결 문자열 정보를 해독 합니다 ([전체 크기 이미지를 보려면 클릭](protecting-connection-strings-and-other-configuration-information-vb/_static/image15.png)).

`<connectionStrings>` 섹션을 일반 텍스트 표현으로 되돌리려면 연결 문자열 암호 해독 단추를 클릭 합니다. 다시 게시 시 `Web.config`의 연결 문자열이 일반 텍스트로 표시 되어야 합니다. 이 시점에서 화면은이 페이지를 처음 방문할 때 처럼 보입니다 (그림 3 참조).

## <a name="step-3-encrypting-configuration-sections-usingaspnet_regiisexe"></a>3 단계:`aspnet_regiis.exe`를 사용 하 여 구성 섹션 암호화

.NET Framework은 `$WINDOWS$\Microsoft.NET\Framework\version\` 폴더에 다양 한 명령줄 도구를 포함 합니다. 예를 들어 [Sql 캐시 종속성 사용](../caching-data/using-sql-cache-dependencies-vb.md) 자습서에서는 `aspnet_regsql.exe` 명령줄 도구를 사용 하 여 SQL 캐시 종속성에 필요한 인프라를 추가 하는 방법을 살펴보았습니다. 이 폴더의 또 다른 유용한 명령줄 도구는 [ASP.NET IIS 등록 도구 (`aspnet_regiis.exe`)](https://msdn.microsoft.com/library/k6h9cz8h(VS.80).aspx)입니다. 이름에서 알 수 있듯이 ASP.NET IIS 등록 도구는 주로 Microsoft professional 웹 서버 (IIS)를 사용 하 여 ASP.NET 2.0 응용 프로그램을 등록 하는 데 사용 됩니다. IIS 관련 기능 외에도 ASP.NET IIS 등록 도구를 사용 하 여 `Web.config`에서 지정 된 구성 섹션을 암호화 하거나 암호를 해독할 수 있습니다.

다음 문은 `aspnet_regiis.exe` 명령줄 도구를 사용 하 여 구성 섹션을 암호화 하는 데 사용 되는 일반 구문을 보여 줍니다.

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample5.cmd)]

*섹션* 은 암호화할 구성 섹션입니다 (예: connectionStrings). *실제\_디렉터리* 는 웹 응용 프로그램의 루트 디렉터리에 대 한 전체 실제 경로이 고 *provider* 는 사용할 보호 된 구성 공급자의 이름 (예: DataProtectionConfigurationProvider)입니다. 또는 웹 응용 프로그램이 IIS에 등록 되어 있는 경우 다음 구문을 사용 하 여 실제 경로 대신 가상 경로를 입력할 수 있습니다.

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample6.cmd)]

다음 `aspnet_regiis.exe` 예제에서는 컴퓨터 수준 키로 DPAPI 공급자를 사용 하 여 `<connectionStrings>` 섹션을 암호화 합니다.

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample7.cmd)]

마찬가지로 `aspnet_regiis.exe` 명령줄 도구를 사용 하 여 구성 섹션의 암호를 해독할 수 있습니다. `-pef` 스위치를 사용 하는 대신 `-pdf` (또는 `-pe`대신 `-pd`)를 사용 합니다. 또한 암호를 해독 하는 경우에는 공급자 이름이 필요 하지 않습니다.

[!code-console[Main](protecting-connection-strings-and-other-configuration-information-vb/samples/sample8.cmd)]

> [!NOTE]
> 컴퓨터와 관련 된 키를 사용 하는 DPAPI 공급자를 사용 하 고 있으므로 웹 페이지를 제공 하는 컴퓨터와 동일한 컴퓨터에서 `aspnet_regiis.exe`를 실행 해야 합니다. 예를 들어 로컬 개발 컴퓨터에서이 명령줄 프로그램을 실행 한 후 암호화 된 web.config 파일을 프로덕션 서버에 업로드 하는 경우 프로덕션 서버는 암호화 된 후에 연결 문자열 정보를 해독할 수 없습니다. 개발 컴퓨터에 특정 한 키 사용 Rsa 공급자는 RSA 키를 다른 컴퓨터로 내보낼 수 있으므로이 제한이 없습니다.

## <a name="understanding-database-authentication-options"></a>데이터베이스 인증 옵션 이해

응용 프로그램에서 Microsoft SQL Server 데이터베이스에 대 한 `SELECT`, `INSERT`, `UPDATE`또는 `DELETE` 쿼리를 실행 하기 전에 먼저 데이터베이스에서 요청자를 식별 해야 합니다. 이 프로세스를 *인증* 이라고 하며 SQL Server는 두 가지 인증 방법을 제공 합니다.

- **Windows 인증** -응용 프로그램이 실행 되는 프로세스를 사용 하 여 데이터베이스와 통신 합니다. ASP.NET 개발 서버 Visual Studio 2005 s를 통해 ASP.NET 응용 프로그램을 실행 하는 경우 ASP.NET 응용 프로그램은 현재 로그온 한 사용자의 id를 가정 합니다. Microsoft IIS (Internet Information Server)에서 ASP.NET 응용 프로그램의 경우 ASP.NET 응용 프로그램은 일반적으로 사용자 지정할 수 있지만 `domainName``\MachineName` 또는 `domainName``\NETWORK SERVICE`id를 가정 합니다.
- **SQL 인증** -사용자 ID 및 암호 값은 인증을 위한 자격 증명으로 제공 됩니다. SQL 인증을 사용 하면 연결 문자열에 사용자 ID와 암호가 제공 됩니다.

Windows 인증은 더 안전 하기 때문에 SQL 인증 보다 우선 합니다. Windows 인증을 사용 하는 경우 연결 문자열은 사용자 이름 및 암호에서 무료로 제공 되며 웹 서버와 데이터베이스 서버가 서로 다른 두 컴퓨터에 있는 경우에는 자격 증명이 네트워크를 통해 일반 텍스트로 전송 되지 않습니다. 그러나 SQL 인증을 사용 하는 경우 인증 자격 증명이 연결 문자열에 하드 코딩 되며 웹 서버에서 일반 텍스트로 데이터베이스 서버로 전송 됩니다.

이러한 자습서에서는 Windows 인증을 사용 했습니다. 연결 문자열을 검사 하 여 어떤 인증 모드를 사용 중인지 알 수 있습니다. 이 자습서의 `Web.config` 연결 문자열은 다음과 같습니다.

`Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\NORTHWND.MDF; Integrated Security=True; User Instance=True`

Integrated Security = True 이며 사용자 이름 및 암호가 부족 하면 Windows 인증을 사용 하 고 있음을 알 수 있습니다. 일부 연결 문자열에서는 Integrated Security = True 대신 트러스트 된 연결 이라는 용어가 사용 되며 세 가지 모두 Windows 인증 사용을 의미 합니다.

다음 예에서는 SQL 인증을 사용 하는 연결 문자열을 보여 줍니다. 연결 문자열에 포함 된 자격 증명을 확인 합니다.

`Server=serverName; Database=Northwind; uid=userID; pwd=password`

공격자가 응용 프로그램 `Web.config` 파일을 볼 수 있다고 가정 합니다. SQL 인증을 사용 하 여 인터넷을 통해 액세스할 수 있는 데이터베이스에 연결 하는 경우 공격자가이 연결 문자열을 사용 하 여 SQL Management Studio 또는 자체 웹 사이트의 ASP.NET 페이지를 통해 데이터베이스에 연결할 수 있습니다. 이 위협을 완화 하기 위해 보호 된 구성 시스템을 사용 하 여 `Web.config`에서 연결 문자열 정보를 암호화 합니다.

> [!NOTE]
> SQL Server에서 사용할 수 있는 다양 한 인증 유형에 대 한 자세한 내용은 [보안 ASP.NET 응용 프로그램 빌드: 인증, 권한 부여 및 보안 통신](https://msdn.microsoft.com/library/aa302392.aspx)을 참조 하세요. Windows 및 SQL 인증 구문 간의 차이점을 보여 주는 추가 연결 문자열 예는 [ConnectionStrings.com](http://www.connectionstrings.com/)을 참조 하세요.

## <a name="summary"></a>요약

기본적으로 ASP.NET 응용 프로그램에서 `.config` 확장명을 가진 파일은 브라우저를 통해 액세스할 수 없습니다. 이러한 유형의 파일은 데이터베이스 연결 문자열, 사용자 이름 및 암호 등의 중요 한 정보를 포함할 수 있기 때문에 반환 되지 않습니다. .NET 2.0의 보호 된 구성 시스템은 지정 된 구성 섹션을 암호화할 수 있도록 하 여 중요 한 정보를 추가로 보호할 수 있습니다. 보호 된 구성 공급자에는 두 가지가 있습니다. 하나는 RSA 알고리즘을 사용 하 고 다른 하나는 Windows DPAPI (데이터 보호 API)를 사용 합니다.

이 자습서에서는 DPAPI 공급자를 사용 하 여 구성 설정을 암호화 하 고 해독 하는 방법을 살펴보았습니다. 이는 2 단계에서 살펴본 것 처럼 프로그래밍 방식으로 수행할 수 있으며, 3 단계에서 다룬 `aspnet_regiis.exe` 명령줄 도구를 통해 수행할 수 있습니다. 사용자 수준 키를 사용 하거나 RSA 공급자를 대신 사용 하는 방법에 대 한 자세한 내용은 추가 정보 섹션의 리소스를 참조 하세요.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [보안 ASP.NET 응용 프로그램 빌드: 인증, 권한 부여 및 보안 통신](https://msdn.microsoft.com/library/aa302392.aspx)
- [ASP.NET 2.0 응용 프로그램에서 구성 정보 암호화](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [ASP.NET 2.0에서 `Web.config` 값 암호화](https://weblogs.asp.net/scottgu/archive/2006/01/09/434893.aspx)
- [방법: DPAPI를 사용 하 여 ASP.NET 2.0의 구성 섹션 암호화](https://msdn.microsoft.com/library/ms998280.aspx)
- [방법: RSA를 사용 하 여 ASP.NET 2.0의 구성 섹션 암호화](https://msdn.microsoft.com/library/ms998283.aspx)
- [.NET 2.0의 구성 API](http://www.odetocode.com/Articles/418.aspx)
- [Windows 데이터 보호](https://msdn.microsoft.com/library/ms995355.aspx)

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 리드 검토자는 Teresa Murphy 및 Randy Schmidt입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb.md)
> [다음](debugging-stored-procedures-vb.md)
