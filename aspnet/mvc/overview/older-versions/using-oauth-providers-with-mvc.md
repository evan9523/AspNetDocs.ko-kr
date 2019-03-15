---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: MVC 4와 함께 OAuth 공급자 사용 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Facebo 같은 외부 공급자가 자격 증명으로 로그인 할 수 있는 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다...
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: d0203b62c911056fc56ed103c1c42f67816cbbf0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065730"
---
<a name="using-oauth-providers-with-mvc-4"></a>MVC 4와 함께 OAuth 공급자 사용
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 사용자가 외부 공급자, Facebook, Twitter, Microsoft, Google 등의 자격 증명으로 로그인 하 고 다음에 해당 공급자의 기능 중 일부를 통합할 수 있는 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 방법에 웹 응용 프로그램입니다. 간단히 하기 위해이 자습서에서 Facebook 자격 증명을 사용 하 여 작업에 중점을 둡니다.
> 
> ASP.NET MVC 5 웹 응용 프로그램에서 외부 자격 증명을 사용 하려면 참조 [Facebook 및 Google OAuth2 및 OpenID Sign on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.
> 
> 수백만 명의 사용자는 이러한 외부 공급자를 사용 하 여 계정을 이미 있기 때문에 중요 한 장점을 제공 웹 사이트에서 이러한 자격 증명을 사용 하도록 설정 합니다. 이러한 사용자를 만들고 새 자격 증명 집합을 기억 없는 경우 사이트에 대 한 등록 싶다는 더욱 수 있습니다. 또한 사용자가 이러한 공급자 중 하나를 통해 로그인 한 후 공급자에서 소셜 작업을 통합할 수 있습니다.


## <a name="what-youll-build"></a>만들 내용

이 자습서에서는 두 가지 주요 목표는

1. OAuth 공급자에서 자격 증명으로 로그인 할 사용자를 사용 하도록 설정 합니다.
2. 공급자에서 계정 정보를 검색 하 고 사이트에 대 한 계정 등록을 사용 하 여 해당 정보를 통합 합니다.

이 자습서의 예제에서 Facebook 인증 공급자로 사용 하 여에 집중 하지만 공급자 중 하나를 사용 하는 코드를 수정할 수 있습니다. 모든 공급자를 구현 하는 단계는이 자습서에서 단계와 매우 비슷합니다. 만 중요 한 차이점은 공급자의 API 직접 호출 시 설정으로 바뀝니다.

## <a name="prerequisites"></a>전제 조건

- [Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) 또는 [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)

Or

- Microsoft Visual Studio 2010 SP1 또는 [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)
- [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)

또한이 항목에서는 ASP.NET MVC 및 Visual Studio에 대 한 기본 지식이 있다고 가정 합니다. ASP.NET MVC 4 소개를 참조 하세요 [ASP.NET MVC 4 소개](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)합니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

Visual Studio에는 새 ASP.NET MVC 4 웹 응용 프로그램을 만들고 이름을 &quot;OAuthMVC&quot;합니다. .NET Framework 4.5 또는 4를 대상 수 있습니다.

![프로젝트 만들기](using-oauth-providers-with-mvc/_static/image1.png)

새 ASP.NET MVC 4 프로젝트 창에서 선택 **인터넷 응용 프로그램** 두고 **Razor** 를 뷰 엔진입니다.

![인터넷 응용 프로그램 선택](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a>공급자를 사용 하도록 설정

앱에서 AuthConfig.cs 라는 파일을 사용 하 여 프로젝트가 생성 되는 인터넷 응용 프로그램 템플릿을 사용 하 여 MVC 4 웹 응용 프로그램을 만들 때\_시작 폴더입니다.

![AuthConfig 파일](using-oauth-providers-with-mvc/_static/image3.png)

AuthConfig 파일은 외부 인증 공급자에 대 한 클라이언트를 등록 하는 코드를 포함 합니다. 기본적으로이 코드는 주석에서 어떤 외부 공급자를 사용할 수 있도록 합니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

외부 인증 클라이언트를 사용 하도록이 코드 주석 처리를 제거 해야 합니다. 사이트에서 포함 하려는 공급자만 주석 처리 합니다. 이 자습서에서는 Facebook 자격 증명을 사용할가 있습니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

메서드는 등록 매개 변수에 대 한 빈 문자열에 위의 예제에서 확인할 수 있습니다. 이제 응용 프로그램을 실행 하려고 하면 응용 프로그램 매개 변수에 대해 빈 문자열이 없으므로 인수 예외를 throw 합니다. 유효한 값을 제공 하려면 다음 섹션에 나와 있는 것 처럼 외부 공급자를 사용 하 여 웹 사이트 등록 해야 합니다.

## <a name="registering-with-an-external-provider"></a>외부 공급자를 사용 하 여 등록

외부 공급자의 자격 증명을 사용 하 여 사용자를 인증 하려면 공급자를 사용 하 여 웹 사이트를 등록 해야 합니다. 사이트를 등록 하면을 받게 됩니다 (예: 키 또는 id 및 암호) 매개 변수를 클라이언트를 등록 하는 경우를 포함 합니다. 계정을 사용 하려면 공급자가 있어야 합니다.

이 자습서에서는 이러한 공급자를 등록 하기 위해 필요한 단계를 모두 표시 되지 않습니다. 단계는 일반적으로 어렵습니다 없습니다. 사이트를 성공적으로 등록 하려면 해당 사이트에 제공 된 지침을 따릅니다. 등록 사이트 사용을 시작 하는 개발자 사이트를 참조:

- [Facebook](https://developers.facebook.com/)
- [Google](https://developers.google.com/)
- [Microsoft](http://manage.dev.live.com/)
- [Twitter](https://dev.twitter.com/)

Facebook을 사용 하 여 사이트를 등록할 때 제공할 수 있습니다 &quot;localhost&quot; 사이트 도메인 및 `&quot; http://localhost/&quot;` 아래 이미지에 표시 된 것과 같이 URL에 대 한 합니다. Localhost를 사용 하 여 대부분의 공급자를 사용 하 여 작동 하지만 현재 Microsoft 공급자와 함께 작동 하지 않습니다. Microsoft 공급자에 대 한 유효한 웹 사이트 URL을 포함 해야 합니다.

![사이트를 등록 합니다.](using-oauth-providers-with-mvc/_static/image4.png)

이전 이미지에서 앱 id, 앱 암호 및 연락처 전자 메일에 대 한 값을 제거 되었습니다. 실제로 사이트를 등록 하면 해당 값이 표시 됩니다. 응용 프로그램에 추가할 것 이므로 앱 id 및 앱 암호에 대 한 값을 확인 하려고 합니다.

## <a name="creating-test-users"></a>테스트 사용자 만들기

사이트를 테스트 하도록 기존 Facebook 계정을 사용 하 여를 고려해 하지 않습니다, 경우에이 섹션을 건너뛸 수 있습니다.

Facebook 앱 관리 페이지 내에서 응용 프로그램에 대 한 테스트 사용자를 쉽게 만들 수 있습니다. 사용할 수 있습니다 사이트에 로그인 할 계정을 테스트 합니다. 클릭 하 여 테스트 사용자를 만듭니다는 **역할** 링크를 클릭 하 고 왼쪽된 탐색 창에는 **만들기** 링크 합니다.

![테스트 사용자 만들기](using-oauth-providers-with-mvc/_static/image5.png)

Facebook 사이트를 요청 하는 테스트 계정 수를 자동으로 만듭니다.

## <a name="adding-application-id-and-secret-from-the-provider"></a>공급자에서 응용 프로그램 id 및 암호 추가

Facebook에서 id 및 암호를 수신 했으므로 AuthConfig 파일로 돌아가서 매개 변수 값으로 추가 합니다. 아래 표시 된 값은 실제 값이 없습니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a>외부 자격 증명으로 로그인

사이트의 외부 자격 증명을 사용 하도록 설정 하기 위해 수행 해야 합니다. 응용 프로그램을 실행 하 고 오른쪽 위 모서리의 로그인 링크를 클릭 합니다. 템플릿을 공급자로 Facebook을 등록 한 공급자의 단추를 포함 하에 자동으로 인식 합니다. 여러 공급자를 등록 하는 경우 각각에 대 한 단추를 자동으로 포함 됩니다.

![외부 로그인](using-oauth-providers-with-mvc/_static/image6.png)

이 자습서 외부 공급자에 대 한 로그인 단추를 사용자 지정 하는 방법을 다루지 않습니다. 해당 정보를 참조 하세요 [OAuth/OpenID를 사용 하는 경우에 로그인 UI를 사용자 지정](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)합니다.

Facebook 자격 증명으로 로그인 하려면 Facebook 단추를 클릭 합니다. 외부 공급자 중 하나를 선택 하면 해당 사이트에 리디렉션 되며 해당 서비스에 로그인 하 라는 메시지가 표시 합니다.

다음 이미지는 facebook 로그인 화면을 보여줍니다. 이 정보 oauthmvcexample 이라는 사이트에 로그인 하려면 Facebook 계정을 사용 한다고 합니다.

![facebook 인증](using-oauth-providers-with-mvc/_static/image7.png)

Facebook 자격 증명으로 로그인 한 후 페이지를 사용자 사이트 기본 정보에 액세스할 수 있는지 알립니다.

![권한을 요청](using-oauth-providers-with-mvc/_static/image8.png)

선택한 후 **앱으로 이동**, 사용자는 사이트에 등록 해야 합니다. 다음 이미지는 사용자가 Facebook 자격 증명을 사용 하 여 로그온 한 후 등록 페이지를 보여줍니다. 사용자 이름은 일반적으로 공급자의 이름으로 미리 채워집니다.

![register](using-oauth-providers-with-mvc/_static/image9.png)

클릭 **등록** 등록을 완료 합니다. 브라우저를 닫습니다.

새 계정 데이터베이스에 추가한는 볼 수 있습니다. 서버 탐색기에서 엽니다는 **DefaultConnection** 연 데이터베이스 합니다 **테이블** 폴더입니다.

![데이터베이스 테이블](using-oauth-providers-with-mvc/_static/image10.png)

마우스 오른쪽 단추로 클릭 합니다 **UserProfile** 선택한 테이블 **테이블 데이터 표시**합니다.

![데이터를 표시 합니다.](using-oauth-providers-with-mvc/_static/image11.png)

추가한 새 계정이 표시 됩니다. 데이터를 살펴봅니다 **웹 페이지\_OAuthMembership** 테이블입니다. 방금 추가한 계정에 대 한 외부 공급자와 관련 된 자세한 데이터를 표시 됩니다.

외부 인증을 사용 하도록 설정 하려는 경우 수행 됩니다. 다음 섹션에 표시 된 대로 새 사용자 등록 프로세스에 공급자의에서 정보를, 통합할 더 있습니다.

## <a name="create-models-for-additional-user-information"></a>추가 사용자 정보에 대 한 모델 만들기

이전 섹션에서 설명한 것 처럼 작동 하도록 기본 제공 계정 등록에 대 한 추가 정보를 검색할 필요가 없습니다. 그러나 대부분의 외부 공급자를 사용자에 대 한 다시 추가 정보를 전달 합니다. 다음 섹션에서는 해당 정보를 유지 하 고 데이터베이스에 저장 하는 방법을 보여 줍니다. 특히, 사용자의 전체 이름, 사용자의 개인 웹 페이지의 URI에 대 한 값 및 Facebook 계정을 확인 여부를 나타내는 값을 유지 합니다.

사용할지 [Code First 마이그레이션을](https://msdn.microsoft.com/data/jj591621) 추가 사용자 정보를 저장 하는 것에 대 한 테이블을 추가 합니다. 현재 데이터베이스의 스냅숏을 만들려면 먼저 해야 하므로 기존 데이터베이스에 테이블을 추가 됩니다. 현재 데이터베이스의 스냅숏을 만들어 나중에 새 테이블을 포함 하는 마이그레이션을 만들 수 있습니다. 현재 데이터베이스의 스냅숏을 만들려면:

1. 열기는 **패키지 관리자 콘솔**
2. 명령을 실행 하 여 **마이그레이션을 사용 하도록 설정**
3. 명령을 실행 하 여 **IgnoreChanges 추가 마이그레이션 초기 –**
4. 명령을 실행 하 여 **데이터베이스 업데이트**

이제 새 속성을 추가 합니다. Models 폴더에서 AccountModels.cs 파일을 열고 하 고 RegisterExternalLoginModel 클래스를 찾습니다. RegisterExternalLoginModel 클래스는 인증 공급자에서 반환 되는 값을 포함 합니다. FullName 및 링크를 아래 강조 표시 된 대로 라는 속성을 추가 합니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

또한 AccountModels.cs, ExtraUserInformation 라는 새 클래스를 추가 합니다. 이 클래스는 데이터베이스에 만들어지는 새 테이블을 나타냅니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

UsersContext 클래스의 새 클래스에 대 한 DbSet 속성을 만들려면 아래 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

이제 새 테이블을 만들 준비가 되었습니다. 다시 패키지 관리자 콘솔을 엽니다.

1. 명령을 실행 하 여 **추가 마이그레이션 AddExtraUserInformation**
2. 명령을 실행 하 여 **데이터베이스 업데이트**

이제 새 테이블 데이터베이스에 존재 합니다.

## <a name="retrieve-the-additional-data"></a>추가 데이터를 검색 합니다.

추가 사용자 데이터를 검색 하는 방법은 두 가지가 있습니다. 첫 번째 방법은 인증 요청 하는 동안 기본적으로 다시 전달 되는 사용자 데이터를 유지 하는 것입니다. 두 번째 방법은 특히 공급자 API를 호출 하 고 추가 정보를 요청 하는 것입니다. FullName 및 링크에 대 한 값은 자동으로 Facebook로 다시 전달 됩니다. Facebook 계정 확인에 있는지 여부를 나타내는 값을 Facebook API 호출을 통해 검색 됩니다. 첫째, FullName 및 링크에 대 한 값을 채웁니다 수 있으며 다음 나중에 확인 된 값입니다.

추가 사용자 데이터를 검색 하려면 엽니다는 **AccountController.cs** 파일을 **컨트롤러** 폴더.

이 파일에는 로깅, 등록 및 계정 관리에 대 한 논리를 포함 합니다. 특히, 호출 된 메서드를 확인할 수 있습니다 **ExternalLoginCallback** 하 고 **ExternalLoginConfirmation**합니다. 이러한 메서드 내에서 응용 프로그램에 대 한 외부 로그인 작업을 사용자 지정 코드를 추가할 수 있습니다. 첫 번째 줄을 **ExternalLoginCallback** 메서드에 포함 되어 있습니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

추가 사용자 데이터에 다시 전달 됩니다는 **ExtraData** 의 속성을 **AuthenticationResult** 에서 반환 되는 개체를 **VerifyAuthentication** 메서드. Facebook 클라이언트에서 다음 값이 포함 된 **ExtraData** 속성:

- ID
- name
- 선택합니다.
- 성별
- accesstoken

다른 공급자 ExtraData 속성에서 유사 하지만 약간 다른 데이터를 사용 해야 합니다.

사이트에 새 사용자 인 경우 일부 추가 데이터를 검색 및 확인 보기로 데이터를 전달 합니다. 메서드에서 코드의 마지막 블록은 사용자가 사이트에 새 하는 경우에 실행 됩니다. 다음 줄을 바꿉니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

이 줄:

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

이 변경은 단순히 FullName 및 링크 속성 값을 포함합니다.

에 **ExternalLoginConfirmation** 메서드를 코드 강조 표시 된 대로 추가 사용자 정보를 저장 하려면 아래를 수정 합니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a>뷰를 조정합니다.

공급자에서 검색 하는 추가 사용자 데이터를 등록 페이지에 표시 됩니다.

에 **뷰**/**계정** 폴더를 열고 **ExternalLoginConfirmation.cshtml**합니다. 사용자 이름에 대 한 기존 필드를 아래 FullName, 링크 및 PictureLink에 대 한 필드를 추가 합니다.

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

준비가 이제 거의 응용 프로그램을 실행 하 고 저장 하는 추가 정보를 사용 하 여 새 사용자를 등록 합니다. 사이트를 사용 하 여 이미 등록 되지 않은 계정이 있어야 합니다. 다른 테스트 계정을 사용 하거나의 행을 삭제 합니다 **UserProfile** 및 **웹 페이지\_OAuthMembership** 다시 사용 하려는 계정에 대 한 테이블입니다. 이러한 행을 삭제 하 여 계정을 다시 등록 해야 합니다.

응용 프로그램을 실행 하 고 새 사용자를 등록 합니다. 이 시간 확인 페이지에는 더 많은 값을 확인 합니다.

![register](using-oauth-providers-with-mvc/_static/image12.png)

등록을 완료 한 후 브라우저를 닫습니다. 데이터베이스에서 새 값이 표시를 확인 합니다 **ExtraUserInformation** 테이블입니다.

## <a name="install-nuget-package-for-facebook-api"></a>Facebook API에 대 한 NuGet 패키지를 설치 합니다.

Facebook은는 [API](https://developers.facebook.com/docs/reference/apis/) 작업을 수행 하려면 호출할 수 있습니다. 보내는 HTTP 요청을 전달 하거나 해당 요청을 보내는 용이 하 게 하는 NuGet 패키지 설치를 사용 하 여 Facebook API를 호출할 수 있습니다. 이 자습서의 예제는 NuGet 패키지를 사용 하 여 아닌 NuGet을 설치 패키지 중요 합니다. 이 자습서에서는 Facebook C# SDK 패키지를 사용 하는 방법을 보여 줍니다. Facebook API 호출에 도움이 되는 다른 NuGet 패키지 있습니다.

**NuGet 패키지 관리** windows Facebook C# SDK 패키지를 선택 합니다.

![패키지 설치](using-oauth-providers-with-mvc/_static/image13.png)

사용자에 대 한 액세스 토큰이 필요한 작업을 호출 하는 Facebook C# SDK를 사용 합니다. 다음 섹션에는 액세스 토큰을 가져오는 방법을 보여 줍니다.

## <a name="retrieve-access-token"></a>액세스 토큰을 가져옵니다.

대부분의 외부 공급자 사용자의 자격 증명이 확인 된 후에 액세스 토큰을 다시 전달 합니다. 이 액세스 토큰은 인증 된 사용자만 사용할 수 있는 작업을 호출할 수 있기 때문에 매우 중요 합니다. 따라서 검색 하 고 액세스 토큰을 저장 반드시 더 많은 기능을 제공 하려는 경우.

외부 공급자에 따라 제한 된 기간 동안에 대 한 액세스 토큰 유효할 수 있습니다. 유효한 액세스 토큰을 갖도록를 검색 합니다 것 될 때마다 사용자, 로그인 및 세션 값으로 저장 하지 않고 데이터베이스에 저장 합니다.

에 **ExternalLoginCallback** 메서드를 액세스 토큰은에 다시 전달도 **ExtraData** 의 속성을 **AuthenticationResult** 개체. 강조 표시 된 코드를 추가 합니다 **ExternalLoginCallback** 액세스 토큰을 저장 하는 **세션** 개체입니다. 이 코드는 사용자가 Facebook 계정에 로그인 할 때마다 실행 됩니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

하지만 Facebook에서 액세스 토큰을 검색 하는이 예제를 통해 검색할 수 있는 액세스 토큰 외부 공급자에서 명명 된 동일한 키 &quot;accesstoken&quot;합니다.

## <a name="logging-off"></a>로그오프

기본값 **로그 오프** 메서드가 응용 프로그램에서 사용자를 로그 했지만 사용자를 외부 공급자 로그 아웃을 기록 하지 않습니다. Facebook에서 사용자를 로그 사용자가 로그온 한 후 유지 토큰을 방지를 다음 강조 표시 된 코드를 추가할 수 있습니다 합니다 **로그 오프** 메서드는 AccountController에서.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

제공한 값을 `next` 매개 변수는 Facebook에서 사용자가 로그온 한 후 사용할 URL입니다. 로컬 컴퓨터에 테스트 하는 경우 로컬 사이트에 대 한 올바른 포트 번호를 제공 합니다. 프로덕션 환경에서 contoso.com과 같은 기본 페이지를 제공 합니다.

## <a name="retrieve-user-information-that-requires-the-access-token"></a>액세스 토큰이 필요한 사용자 정보를 검색 합니다.

액세스 토큰을 저장 하 고 Facebook C# SDK 패키지를 설치 했으므로 Facebook에서 추가 사용자 정보를 요청 함께 사용할 수 있습니다. 에 **ExternalLoginConfirmation** 메서드를의 인스턴스를 만들 합니다 **FacebookClient** 액세스 토큰의 값을 전달 하 여 클래스. 값을 요청 합니다 **확인할** 현재 인증 된 사용자에 대 한 속성입니다. 합니다 **확인할** 속성 Facebook에 휴대 전화에 메시지를 보내는 등의 다른 수단을 통해 계정 유효성 검사가 수행 되는지를 나타냅니다. 데이터베이스에서이 값을 저장 합니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

다시 사용자에 대 한 데이터베이스의 레코드를 삭제 하거나 다른 Facebook 계정을 사용 해야 합니다.

응용 프로그램을 실행 하 고 새 사용자를 등록 합니다. 확인 합니다 **ExtraUserInformation** 테이블을 참조 하는 확인 된 속성의 값입니다.

## <a name="conclusion"></a>결론

이 자습서에서는 Facebook을 사용 하 여 사용자 인증 및 등록 데이터에 대 한 통합 된 사이트를 만들었습니다. MVC 4 웹 응용 프로그램 및 해당 기본 동작을 사용자 지정 하는 방법에 대 한 설정 된 기본 동작에 대해 알아보았습니다.

## <a name="related-topics"></a>관련 항목

- [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
