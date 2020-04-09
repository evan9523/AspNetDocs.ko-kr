---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 페이팔로 결제 및 결제 | 마이크로 소프트 문서
author: Erikre
description: 이 튜토리얼 시리즈는 ASP.NET 4.5및 Microsoft Visual Studio Express 2013을 사용하여 ASP.NET 웹 폼 응용 프로그램을 빌드하는 기본 정보를 가르쳐 드립니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675690"
---
# <a name="checkout-and-payment-with-paypal"></a>PayPal로 체크 아웃 및 지불

로 [에릭 레이탄](https://github.com/Erikre)

[Wingtip 장난감 샘플 프로젝트 다운로드 (C #)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 책 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈에서는 웹용 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용하여 ASP.NET 웹 양식 응용 프로그램을 빌드하는 기본 정보를 강의합니다. [C# 소스 코드가 있는](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) Visual Studio 2013 프로젝트를 이 자습서 시리즈와 함께 사용할 수 있습니다.

이 자습서에서는 PayPal을 사용하여 사용자 권한 부여, 등록 및 지불을 포함하도록 Wingtip Toys 샘플 응용 프로그램을 수정하는 방법을 설명합니다. 로그인한 사용자만 제품을 구매할 수 있는 권한이 부여됩니다. ASP.NET 4.5 Web Forms 프로젝트 템플릿의 기본 제공 사용자 등록 기능에는 이미 필요한 것이 많이 포함되어 있습니다. 페이팔 익스프레스 체크아웃 기능을 추가합니다. 이 튜토리얼에서는 PayPal 개발자 테스트 환경을 사용하므로 실제 자금이 전송되지 않습니다. 자습서의 끝에서, 당신은 쇼핑 카트에 추가 할 제품을 선택하여 응용 프로그램을 테스트합니다, 체크 아웃 버튼을 클릭, PayPal 테스트 웹 사이트에 데이터를 전송. PayPal 테스트 웹 사이트에서 배송 및 결제 정보를 확인한 다음 현지 Wingtip Toys 샘플 응용 프로그램으로 돌아가 구매를 확인하고 완료합니다.

확장성과 보안을 다루는 온라인 쇼핑을 전문으로 하는 숙련된 타사 결제 프로세서가 몇 가지 있습니다. ASP.NET 개발자는 쇼핑 및 구매 솔루션을 구현하기 전에 타사 결제 솔루션을 활용하는 장점을 고려해야 합니다.

> [!NOTE] 
> 
> Wingtip Toys 샘플 응용 프로그램은 웹 개발자가 사용할 수 있는 특정 ASP.NET 개념 및 기능을 표시하도록 설계되었으며 ASP.NET. 이 샘플 응용 프로그램은 확장성 및 보안과 관련하여 가능한 모든 상황에 최적화되지 않았습니다.

## <a name="what-youll-learn"></a>학습할 내용:

- 폴더의 특정 페이지에 대한 액세스를 제한하는 방법.
- 익명 장바구니에서 알려진 장바구니를 만드는 방법.
- 프로젝트에 대 한 SSL을 사용 하는 방법.
- 프로젝트에 OAuth 공급자를 추가하는 방법.
- 페이팔을 사용하여 페이팔 테스트 환경을 사용하여 제품을 구입하는 방법.
- **세부 정보보기** 컨트롤에 페이팔의 세부 정보를 표시하는 방법.
- 페이팔에서 얻은 세부 사항으로 Wingtip 장난감 응용 프로그램의 데이터베이스를 업데이트하는 방법.

## <a name="adding-order-tracking"></a>주문 추적 추가

이 자습서에서는 사용자가 만든 순서의 데이터를 추적하기 위해 두 개의 새 클래스를 만듭니다. 수업은 배송 정보, 구매 합계 및 지불 확인에 관한 데이터를 추적합니다.

### <a name="add-the-order-and-orderdetail-model-classes"></a>순서 및 순서 세부 사항 모델 클래스 추가

이 `Category`자습서 시리즈의 앞에서 는 *모델* 폴더에서 에서 " `Product`및 `CartItem` 클래스를 만들어 범주, 제품 및 장바구니 항목에 대한 스키마를 정의했습니다. 이제 두 개의 새 클래스를 추가하여 제품 주문에 대한 스키마와 주문세부 정보를 정의합니다.

1. **모델** 폴더에 *Order.cs*라는 새 클래스를 추가합니다.   
   새 클래스 파일이 편집기에 표시됩니다.
2. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. *모델* 폴더에 *OrderDetail.cs* 클래스를 추가합니다.
4. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order` 및 `OrderDetail` 클래스에는 구매 및 배송에 사용되는 주문 정보를 정의하는 스키마가 포함되어 있습니다.

또한 엔터티 클래스를 관리하고 데이터베이스에 대한 데이터 액세스를 제공하는 데이터베이스 컨텍스트 클래스를 업데이트해야 합니다. 이렇게 하려면 새로 만든 순서 및 `OrderDetail` 모델 클래스를 클래스에 추가 합니다. `ProductContext`

1. **솔루션 탐색기에서** *ProductContext.cs* 파일을 찾아 엽니다.
2. 아래와 같이 강조 표시된 코드를 *ProductContext.cs* 파일에 추가합니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

이 자습서 시리즈에서 앞에서 설명한 것처럼 *ProductContext.cs* 파일의 코드는 엔터티 프레임워크의 `System.Data.Entity` 모든 핵심 기능에 액세스할 수 있도록 네임스페이스를 추가합니다. 이 기능에는 강력한 형식의 개체로 작업하여 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 기능이 포함됩니다. 클래스의 `ProductContext` 위의 코드는 새로 추가된 `Order` 클래스에 `OrderDetail` 엔터티 프레임워크 액세스를 추가합니다.

## <a name="adding-checkout-access"></a>체크 아웃 액세스 추가

Wingtip 장난감 샘플 응용 프로그램은 익명 사용자가 검토하고 장바구니에 제품을 추가 할 수 있습니다. 그러나 익명 사용자가 장바구니에 추가한 제품을 구매하기로 선택한 경우 사이트에 로그온해야 합니다. 로그온한 후에는 체크 아웃 및 구매 프로세스를 처리하는 웹 응용 프로그램의 제한된 페이지에 액세스할 수 있습니다. 이러한 제한된 페이지는 응용 프로그램의 *체크 아웃* 폴더에 포함되어 있습니다.

### <a name="add-a-checkout-folder-and-pages"></a>체크 아웃 폴더 및 페이지 추가

이제 체크 아웃 폴더와 *체크 아웃* 프로세스 중에 고객이 볼 수 있는 페이지를 만듭니다. 이 자습서의 나중에 이러한 페이지를 업데이트합니다.

1. **솔루션 탐색기에서** 프로젝트 이름(Wingtip**Toys)을**마우스 오른쪽 단추로 클릭하고 **새 폴더 추가를**선택합니다. 

    ![페이팔로 결제 및 결제 - 새 폴더](checkout-and-payment-with-paypal/_static/image1.png)
2. 새 폴더 의 이름을 *체크 아웃합니다.*
3. *체크 아웃* 폴더를 마우스 오른쪽 단추로 클릭한 다음**새 항목** **추가를**-&gt;선택합니다. 

    ![페이팔로 결제 및 결제 - 새로운 항목](checkout-and-payment-with-paypal/_static/image2.png)
4. **새 항목 추가** 대화 상자가 표시됩니다.
5. 왼쪽에 있는 **Visual C#**  - &gt; **웹** 템플릿 그룹을 선택합니다. 그런 다음 중간 창에서 **마스터 페이지가 있는 웹 양식을**선택하고 *CheckoutStart.aspx*. 

    ![페이팔로 결제 및 결제 - 새 항목 대화 상자 추가](checkout-and-payment-with-paypal/_static/image3.png)
6. 이전과 마찬가지로 *Site.Master* 파일을 마스터 페이지로 선택합니다.
7. 위의 동일한 단계를 사용하여 *체크 아웃* 폴더에 다음 페이지를 추가합니다.   

    - 체크 아웃리뷰.aspx
    - 체크 아웃완료.aspx
    - 체크 아웃취소.aspx
    - 체크 아웃오류.aspx

### <a name="add-a-webconfig-file"></a>Web.config 파일 추가

*체크 아웃* 폴더에 새 *Web.config* 파일을 추가하면 폴더에 포함된 모든 페이지에 대한 액세스를 제한할 수 있습니다.

1. *체크 아웃* 폴더를 마우스 오른쪽 단추로 클릭하고 **새 항목** **추가를**  - &gt; 선택합니다.  
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 왼쪽에 있는 **Visual C#**  - &gt; **웹** 템플릿 그룹을 선택합니다. 그런 다음 중간 창에서 **웹 구성 파일을**선택하고 *Web.config의*기본 이름을 수락한 다음 **에 추가를**선택합니다.
3. *Web.config* 파일의 기존 XML 콘텐츠를 다음으로 바꿉니다.  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. *Web.config* 파일을 저장합니다.

*Web.config* 파일은 웹 응용 프로그램의 알 수 없는 모든 사용자가 *체크 아웃* 폴더에 포함된 페이지에 대한 액세스를 거부해야 함을 지정합니다. 그러나 사용자가 계정을 등록하고 로그온한 경우 알려진 사용자가 되며 *체크 아웃* 폴더의 페이지에 액세스할 수 있습니다.

ASP.NET 구성은 계층 구조를 따르며, 각 *Web.config* 파일은 구성 설정을 폴더에 적용하고 그 아래에 있는 모든 자식 디렉터리에 적용합니다.

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>프로젝트에 SSL 사용

 SSL(Secure Sockets Layer)은 웹 서버 및 웹 클라이언트가 암호화를 사용하여 더욱 안전하게 통신할 수 있도록 정의된 프로토콜입니다. SSL을 사용하지 않으면 네트워크에 실제로 액세스하여 패킷을 스니핑하는 누군가에게 클라이언트와 서버 간에 전송된 데이터가 노출됩니다. 또한 몇 가지 일반적인 인증 체계는 일반 HTTP를 통해서는 보호되지 않습니다. 특히, 기본 인증 및 폼 인증은 암호화되지 않은 자격 증명을 보냅니다. 보안을 위해서 인증 체계는 SSL을 사용해야 합니다. 

1. **솔루션 탐색기에서** **WingtipToys** 프로젝트를 클릭한 다음 **F4를** 눌러 **속성** 창을 표시합니다.
2. **SSL 을** `true`로 변경합니다.
3. 나중에 사용할 수 있도록 **SSL URL** 을 복사합니다.   
 SSL URL은 `https://localhost:44300/` 이전에 SSL 웹 사이트를 만든 적이 없는 경우(아래 와 같이)입니다.   
    ![프로젝트 속성](checkout-and-payment-with-paypal/_static/image4.png)
4. **솔루션 탐색기에서** **WingtipToys** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성을**클릭합니다.
5. 왼쪽 탭에서 **웹**을 클릭합니다.
6. 이전에 저장한 **SSL URL을** 사용하도록 **프로젝트 URL을** 변경합니다.   
    ![프로젝트 웹 속성](checkout-and-payment-with-paypal/_static/image5.png)
7. **CTRL+S**키를 눌러 페이지를 저장합니다.
8. **Ctrl+F5를** 눌러 응용 프로그램을 실행합니다. Visual Studio에서 SSL 경고를 방지할 수 있도록 하는 옵션을 표시합니다.
9. **예** 를 클릭하여 IIS Express SSL 인증서를 신뢰하고 계속합니다.   
    ![IIS Express SSL 인증서 정보](checkout-and-payment-with-paypal/_static/image6.png)  
  보안 경고가 표시됩니다.
10. **예** 를 클릭하여 인증서를 localhost에 설치합니다.   
    ![보안 경고 대화 상자](checkout-and-payment-with-paypal/_static/image7.png)  
  브라우저 창이 표시됩니다.

이제 SSL을 사용하여 로컬에서 웹 응용 프로그램을 쉽게 테스트할 수 있습니다.

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>OAuth 2.0 공급자 추가

ASP.NET Web Forms는 멤버 자격 및 인증을 위해 개선된 옵션을 제공합니다. 이러한 개선 사항에는 OAuth가 포함됩니다. OAuth는 웹, 모바일 및 데스크톱 애플리케이션에서 간단한 표준 메서드로 보안 권한 부여를 허용하는 개방형 프로토콜입니다. ASP.NET 웹 폼 템플릿은 OAuth를 사용하여 페이스 북, 트위터, 구글 및 Microsoft를 인증 공급자로 노출시킵니다. 이 자습서에서는 인증 공급자로 Google만 사용하지만 다른 공급자를 사용하도록 코드를 쉽게 수정할 수 있습니다. 다른 공급자를 구현하는 단계도 이 자습서에 표시되는 단계와 매우 비슷합니다.

자습서에서는 인증 외에도 역할을 사용하여 권한 부여를 구현합니다. `canEdit` 역할에 추가한 사용자만 데이터를 변경할 수 있습니다(연락처 만들기, 편집 또는 삭제).

> [!NOTE] 
> 
> Windows Live 응용 프로그램은 작업 중인 웹 사이트에 대한 라이브 URL만 허용하므로 로그인 을 테스트하기 위해 로컬 웹 사이트 URL을 사용할 수 없습니다.

다음 단계를 통해 Google 인증 공급자를 추가할 수 있습니다.

1. *\_앱 시작\Startup.Auth.cs 파일을 엽니다.*
2. 메서드가 다음과 같이 나타나도록 `app.UseGoogleAuthentication()` 메서드에서 주석 문자를 제거합니다. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. [Google Developers Console](https://console.developers.google.com/)로 이동합니다. Google 개발자 메일 계정(gmail.com)으로 로그인해야 합니다. Google 계정이 없으면 **계정 만들기** 링크를 선택합니다.   
   다음으로, **Google 개발자 콘솔**이 표시됩니다.   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. 프로젝트 **만들기** 단추를 클릭하고 프로젝트 이름과 ID를 입력합니다(기본값을 사용할 수 있음). 그런 다음 **계약 확인란과** **만들기** 단추를 클릭합니다.  

    ![구글 - 새로운 프로젝트](checkout-and-payment-with-paypal/_static/image9.png)

    몇 초 내에 새 프로젝트가 만들어지고 브라우저에 새 프로젝트 페이지가 표시됩니다.
5. 왼쪽 탭에서 **API &amp; 인증을**클릭한 다음 자격 증명 을 **클릭합니다.**
6. **OAuth**에서 **새 클라이언트 ID 만들기를** 클릭합니다.   
   **Create Client ID** 대화 상자가 표시됩니다.   
    ![Google - 클라이언트 ID 만들기](checkout-and-payment-with-paypal/_static/image10.png)
7. 클라이언트 **ID 만들기** 대화 상자에서 응용 프로그램 유형에 대한 기본 **웹 응용 프로그램을** 유지합니다.
8. 이 자습서의 앞에서 사용한 **공인 자바스크립트 원본을** 설정합니다(다른`https://localhost:44300/` SSL 프로젝트를 만들지 않은 경우).   
   이 URL이 애플리케이션의 원점입니다. 이 샘플의 경우 localhost 테스트 URL만 입력합니다. 그러나 로컬 호스트 및 프로덕션을 고려하여 여러 URL을 입력할 수 있습니다.
9. **Authorized Redirect URI** 를 다음으로 설정합니다. 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   이 값은 ASP.NET OAuth 사용자가 Google OAuth 서버와 통신하는 데 사용하는 URI입니다. 위에서 사용한 SSL URL을 `https://localhost:44300/` 기억하십시오(다른 SSL 프로젝트를 만들지 않는 한).
10. 클라이언트 ID 만들기 단추를 **클릭합니다.**
11. Google 개발자 콘솔의 왼쪽 메뉴에서 **동의 화면** 메뉴 항목을 클릭한 다음 이메일 주소와 제품 이름을 설정합니다. 양식을 완료하면 **저장을**클릭합니다.
12. **API** 메뉴 항목을 클릭하고 아래로 스크롤한 다음 **Google+ API**옆의 **끄기** 버튼을 클릭합니다.   
    이 옵션을 수락하면 Google+ API가 활성화됩니다.
13. 또한 버전 3.0.0으로 **Microsoft.Owin** NuGet 패키지를 업데이트해야 합니다.   
    **도구** 메뉴에서 **NuGet 패키지 관리자를** 선택한 다음 **솔루션에 대한 NuGet 패키지 관리를 선택합니다.**  
    NuGet 패키지 관리 창에서 **Microsoft.Owin** 패키지를 버전 3.0.0으로 찾아 **업데이트합니다.**
14. Visual Studio에서 클라이언트 `UseGoogleAuthentication` **ID와 클라이언트** **시크릿을** 복사하여 *메서드에* 붙여넣은 Startup.Auth.cs 페이지의 메서드를 업데이트합니다. 아래에 표시된 **클라이언트 ID** 및 **클라이언트 보안** 값은 샘플이며 작동하지 않습니다. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. **CTRL+F5를** 눌러 응용 프로그램을 빌드하고 실행합니다. **로그인** 링크를 클릭합니다.
16. **다른 서비스 사용에서 로그인하려면** **Google**을 클릭합니다.  
    ![로그인](checkout-and-payment-with-paypal/_static/image11.png)
17. 자격 증명을 입력해야 하는 경우 자격 증명을 입력할 google 사이트로 리디렉션됩니다.  
    ![Google - 로그인](checkout-and-payment-with-paypal/_static/image12.png)
18. 자격 증명을 입력하면 방금 만든 웹 응용 프로그램에 대한 권한을 부여하라는 메시지가 표시됩니다.  
    ![프로젝트 기본 서비스 계정](checkout-and-payment-with-paypal/_static/image13.png)
19. **Accept**를 클릭합니다. 이제 Google 계정을 등록할 수 있는 **WingtipToys** 응용 프로그램의 **등록** 페이지로 다시 리디렉션됩니다.  
    ![Google 계정을 사용하여 등록](checkout-and-payment-with-paypal/_static/image14.png)
20. Gmail 계정에 사용되는 로컬 전자 메일 등록 이름을 변경할 수 있지만 일반적으로 기본 전자 메일 별칭(즉, 인증에 사용하는 별칭)을 그대로 사용합니다. 위에 표시된 대로 **로그인을** 클릭합니다.

### <a name="modifying-login-functionality"></a>로그인 기능 수정

이 자습서 시리즈에서 설명한 것처럼 대부분의 사용자 등록 기능은 기본적으로 ASP.NET 웹 폼 템플릿에 포함되어 있습니다. 이제 기본 *Login.aspx* 및 *Register.aspx* 페이지를 수정하여 메서드를 `MigrateCart` 호출합니다. 이 `MigrateCart` 메서드는 새로 로그인한 사용자를 익명 장바구니와 연결합니다. 사용자와 장바구니를 연결하여 Wingtip Toys 샘플 응용 프로그램은 방문 간에 사용자의 장바구니를 유지할 수 있습니다.

1. **솔루션 탐색기에서** *계정* 폴더를 찾아 엽니다.
2. *Login.aspx.cs* 라는 코드 뒤에 페이지를 수정 하려면 노란색으로 강조 표시된 코드를 포함 하 여 다음과 같이 표시 됩니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. *Login.aspx.cs* 파일을 저장합니다.

지금은 `MigrateCart` 메서드에 대한 정의가 없다는 경고를 무시할 수 있습니다. 이 자습서의 나중에 조금 추가 됩니다.

*Login.aspx.cs* 코드 뒤 파일은 LogIn 메서드를 지원합니다. Login.aspx 페이지를 검사하면 이 페이지에 클릭시 코드 숨결의 `LogIn` 처리기가 트리거되는 "로그인" 버튼이 포함되어 있음을 알 수 있습니다.

Login.aspx.cs `Login` 메서드가 *Login.aspx.cs* 호출되면 라는 `usersShoppingCart` 쇼핑 카트의 새 인스턴스가 만들어집니다. 장바구니(GUID)의 ID가 검색되어 `cartId` 변수로 설정됩니다. 그런 다음 `MigrateCart` 메서드를 호출하여 `cartId` 로그인한 사용자의 이름과 이름을 이 메서드에 전달합니다. 장바구니를 마이그레이션할 때 익명 장바구니를 식별하는 데 사용되는 GUID가 사용자 이름으로 바뀝니다.

사용자가 로그인할 때 장바구니를 마이그레이션하기 위해 *Login.aspx.cs* 코드 숨결 파일을 수정하는 것 외에도 *Register.aspx.cs 코드 숨은 파일을* 수정하여 사용자가 새 계정을 만들고 로그인할 때 장바구니를 마이그레이션해야 합니다.

1. *Account* 폴더에서 *Register.aspx.cs*라는 코드 숨결 파일을 엽니다.
2. 다음과 같이 표시되도록 코드를 노란색으로 표시하여 코드 숨결 파일을 수정합니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. *Register.aspx.cs* 파일을 저장합니다. 다시 한번 메서드에 `MigrateCart` 대한 경고를 무시합니다.

`CreateUser_Click` 이벤트 처리기에 사용된 코드는 `LogIn` 메서드에서 사용한 코드와 매우 유사합니다. 사용자가 사이트에 등록하거나 로그인하면 `MigrateCart` 메서드를 호출합니다.

## <a name="migrating-the-shopping-cart"></a>장바구니 마이그레이션

로그인 및 등록 프로세스가 업데이트되었으므로 코드를 추가하여 메서드를 `MigrateCart` 사용하여 장바구니를 마이그레이션할 수 있습니다.

1. **솔루션 탐색기에서** *논리* 폴더를 찾아 *ShoppingCartActions.cs* 클래스 파일을 엽니다.
2. *ShoppingCartActions.cs* 파일의 기존 코드에 노란색으로 강조 표시된 코드를 추가하여 *ShoppingCartActions.cs* 파일의 코드가 다음과 같이 표시됩니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

이 `MigrateCart` 메서드는 기존 cartId를 사용하여 사용자의 장바구니를 찾습니다. 다음으로 코드는 모든 장바구니 항목을 반복하고 스키마에서 `CartId` 지정한 `CartItem` 대로 속성을 로그인한 사용자 이름으로 바꿉니다.

### <a name="updating-the-database-connection"></a>데이터베이스 연결 업데이트

**미리 빌드된** Wingtip Toys 샘플 응용 프로그램을 사용하여 이 자습서를 따르는 경우 기본 멤버 자격 데이터베이스를 다시 만들어야 합니다. 기본 연결 문자열을 수정하면 다음에 응용 프로그램을 실행할 때 멤버 자격 데이터베이스가 만들어집니다.

1. 프로젝트의 루트에서 *Web.config* 파일을 엽니다.
2. 다음과 같이 표시되도록 기본 연결 문자열을 업데이트합니다.   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>페이팔 통합

PayPal은 온라인 판매자의 결제를 허용하는 웹 기반 결제 플랫폼입니다. 이 자습서는 다음에 페이팔의 익스프레스 체크 아웃 기능을 응용 프로그램에 통합 하는 방법을 설명 합니다. 익스프레스 체크아웃을 사용하면 고객이 PayPal을 사용하여 장바구니에 추가한 항목에 대한 비용을 지불할 수 있습니다.

### <a name="create-paypal-test-accounts"></a>페이팔 테스트 계정 만들기

PayPal 테스트 환경을 사용하려면 개발자 테스트 계정을 만들고 확인해야 합니다. 개발자 테스트 계정을 사용하여 구매자 테스트 계정과 판매자 테스트 계정을 만듭니다. 개발자 테스트 계정 자격 증명은 또한 Wingtip Toys 샘플 응용 프로그램이 PayPal 테스트 환경에 액세스할 수 있도록 합니다.

1. 브라우저에서 PayPal 개발자 테스트 사이트로 이동합니다.   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. PayPal 개발자 계정이 없는 경우 **등록을**클릭하고 등록 단계를 따라 새 계정을 만듭니다. 기존 PayPal 개발자 계정이 있는 경우 **로그인**을 클릭하여 로그인합니다. 이 자습서의 후반부에서 Wingtip Toys 샘플 응용 프로그램을 테스트하려면 PayPal 개발자 계정이 필요합니다.
3. PayPal 개발자 계정에 방금 가입한 경우 PayPal을 사용하여 PayPal 개발자 계정을 확인해야 할 수 있습니다. PayPal이 이메일 계정으로 전송한 단계에 따라 계정을 확인할 수 있습니다. PayPal 개발자 계정을 확인하면 PayPal 개발자 테스트 사이트에 다시 로그인합니다.
4. PayPal 개발자 계정으로 PayPal 개발자 사이트에 로그인한 후 아직 계정이 없는 경우 PayPal 구매자 테스트 계정을 만들어야 합니다. 구매자 테스트 계정을 만들려면 PayPal 사이트에서 **응용 프로그램 탭을** 클릭한 다음 **샌드박스 계정을**클릭합니다.   
 **샌드박스 테스트 계정** 페이지가 표시됩니다.   

    > [!NOTE] 
    > 
    > 페이팔 개발자 사이트는 이미 판매자 테스트 계정을 제공합니다.

    ![페이팔로 결제 및 결제 - 샌드박스 테스트 계정](checkout-and-payment-with-paypal/_static/image15.png)
5. 샌드박스 테스트 계정 페이지에서 **계정 만들기를**클릭합니다.
6. 테스트 **계정 만들기** 페이지에서 구매자 테스트 계정 이메일과 원하는 암호를 선택합니다.   

    > [!NOTE] 
    > 
    > 이 자습서의 끝에 있는 Wingtip Toys 샘플 응용 프로그램을 테스트하려면 구매자 이메일 주소와 암호가 필요합니다.

    ![페이팔로 결제 및 결제 - 샌드박스 테스트 계정](checkout-and-payment-with-paypal/_static/image16.png)
7. 계정 만들기 단추를 클릭하여 구매자 테스트 계정을 **만듭니다.**  
 **샌드박스 테스트 계정** 페이지가 표시됩니다. 

    ![페이팔 결제 및 결제 - 페이팔 계정](checkout-and-payment-with-paypal/_static/image17.png)
8. **샌드박스 테스트 계정** 페이지에서 진행자 이메일 계정을 **클릭합니다.**  
    **프로필** 및 **알림** 옵션이 나타납니다.
9. **프로필** 옵션을 선택한 다음 **API 자격 증명을** 클릭하여 판매자 테스트 계정에 대한 API 자격 증명을 봅니다.
10. 테스트 API 자격 증명을 메모장에 복사합니다.

Wingtip Toys 샘플 응용 프로그램에서 PayPal 테스트 환경으로 API를 호출하려면 표시된 클래식 TEST API 자격 증명(사용자 이름, 암호 및 서명)이 필요합니다. 다음 단계에서 자격 증명을 추가합니다.

### <a name="add-paypal-class-and-api-credentials"></a>페이팔 클래스 및 API 자격 증명 추가

페이팔 코드의 대부분을 단일 클래스에 배치합니다. 이 클래스에는 PayPal과 통신하는 데 사용되는 방법이 포함되어 있습니다. 또한 이 클래스에 PayPal 자격 증명을 추가합니다.

1. Visual Studio 내의 Wingtip Toys 샘플 응용 프로그램에서 **논리** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 항목** **추가를**  - &gt; 선택합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 왼쪽에 **설치된** 창에서 **시각적 C#** 아래에서 **코드를**선택합니다.
3. 가운데 창에서 **클래스를**선택합니다. 이 새 클래스의 이름을 **PayPalFunctions.cs.**
4. **추가**를 클릭합니다.  
   새 클래스 파일이 편집기에 표시됩니다.
5. 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. PayPal 테스트 환경에 함수 호출을 수행할 수 있도록 이 자습서의 앞에서 표시한 판매자 API 자격 증명(사용자 이름, 암호 및 서명)을 추가합니다.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> 이 샘플 응용 프로그램에서는 C# 파일(.cs)에 자격 증명을 추가하기만 하면 됩니다. 그러나 구현된 솔루션에서는 구성 파일에서 자격 증명을 암호화하는 것이 좋습니다.

NVPAPICaller 클래스는 페이팔 기능의 대부분을 포함. 클래스의 코드는 PayPal 테스트 환경에서 테스트 구매하는 데 필요한 방법을 제공합니다. 다음 세 가지 페이팔 기능은 구매를 위해 사용됩니다.

- `SetExpressCheckout` 함수
- `GetExpressCheckoutDetails` 함수
- `DoExpressCheckoutPayment` 함수

이 `ShortcutExpressCheckout` 방법은 장바구니에서 테스트 구매 정보 및 제품 `SetExpressCheckout` 세부 정보를 수집하고 PayPal 기능을 호출합니다. 이 `GetCheckoutDetails` 방법은 구매 세부 정보를 `GetExpressCheckoutDetails` 확인하고 테스트 구매를하기 전에 PayPal 기능을 호출합니다. 이 `DoCheckoutPayment` 방법은 `DoExpressCheckoutPayment` PayPal 함수를 호출하여 테스트 환경에서 테스트 구매를 완료합니다. 나머지 코드는 문자열 인코딩, 문자열 디코딩, 처리 배열 및 자격 증명 결정과 같은 PayPal 메서드 및 프로세스를 지원합니다.

> [!NOTE] 
> 
> PayPal을 사용하면 [PayPal의 API 사양에](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)따라 선택적 구매 세부 정보를 포함할 수 있습니다. Wingtip Toys 샘플 응용 프로그램에서 코드를 확장하여 지역화 세부 정보, 제품 설명, 세금, 고객 서비스 번호 및 기타 여러 선택적 필드를 포함할 수 있습니다.

**바로 가기익스프레스체크아웃** 메서드에 지정된 반환 및 취소 URL은 포트 번호를 사용합니다.

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

Visual Web 개발자가 SSL을 사용하여 웹 프로젝트를 실행하면 일반적으로 포트 44300이 웹 서버에 사용됩니다. 위와 같이 포트 번호는 44300입니다. 응용 프로그램을 실행하면 다른 포트 번호가 표시될 수 있습니다. 이 자습서의 끝에서 Wingtip Toys 샘플 응용 프로그램을 성공적으로 실행할 수 있도록 코드에서 포트 번호를 올바르게 설정해야 합니다. 이 자습서의 다음 섹션에서는 로컬 호스트 포트 번호를 검색하고 PayPal 클래스를 업데이트하는 방법을 설명합니다.

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>페이팔 클래스에서 로컬 호스트 포트 번호 업데이트

Wingtip Toys 샘플 응용 프로그램은 PayPal 테스트 사이트로 이동하여 Wingtip Toys 샘플 응용 프로그램의 로컬 인스턴스로 돌아가서 제품을 구입합니다. PayPal이 올바른 URL로 돌아가려면 위에서 언급한 PayPal 코드에서 로컬로 실행 중인 샘플 응용 프로그램의 포트 번호를 지정해야 합니다.

1. **솔루션 탐색기에서** 프로젝트 이름(WingtipToys)을 마우스 오른쪽 단추로 클릭하고**WingtipToys** **속성을**선택합니다.
2. 왼쪽 열에서 **웹** 탭을 선택합니다.
3. **프로젝트 URL** 상자에서 포트 번호를 검색합니다.
4. 필요한 경우 *PayPalFunctions.cs* `cancelURL` 파일의 PayPal`NVPAPICaller`클래스 ()를 업데이트하여 `returnURL` 웹 응용 프로그램의 포트 번호를 사용합니다.   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

이제 추가한 코드가 로컬 웹 응용 프로그램에 대한 예상 포트와 일치합니다. 페이팔은 로컬 컴퓨터에서 올바른 URL로 돌아갈 수 있습니다.

### <a name="add-the-paypal-checkout-button"></a>페이팔 체크아웃 버튼 추가

이제 기본 PayPal 함수가 샘플 응용 프로그램에 추가되었으므로 이러한 함수를 호출하는 데 필요한 태그 및 코드를 추가할 수 있습니다. 먼저 장바구니 페이지에 표시되는 체크아웃 버튼을 추가해야 합니다.

1. *쇼핑카트.aspx 파일을 엽니다.*
2. 파일 아래쪽으로 스크롤하여 주석을 `<!--Checkout Placeholder -->` 찾습니다.
3. 다음과 같이 마크업이 대체되도록 주석을 `ImageButton` 컨트롤로 바꿉습니다.  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. *ShoppingCart.aspx.cs* 파일에서 파일 `UpdateBtn_Click` 끝에 있는 이벤트 처리기 후 `CheckOutBtn_Click` 이벤트 처리기를 추가합니다.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. 또한 *ShoppingCart.aspx.cs* 파일에서 `CheckoutBtn`에 대한 참조를 추가하여 새 이미지 단추를 다음과 같이 참조합니다.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. 변경 내용을 *ShoppingCart.aspx* 파일과 *ShoppingCart.aspx.cs* 파일에 모두 저장합니다.
7. 메뉴에서 **디버그**-&gt;**빌드 WingtipToys를**선택합니다.  
   새로 추가된 **ImageButton** 컨트롤로 프로젝트가 다시 빌드됩니다.

### <a name="send-purchase-details-to-paypal"></a>페이팔로 구매 세부 정보 보내기

사용자가 장바구니*페이지(ShoppingCart.aspx)에서* **체크아웃** 버튼을 클릭하면 구매 프로세스가 시작됩니다. 다음 코드는 제품을 구입하는 데 필요한 첫 번째 PayPal 기능을 호출합니다.

1. 체크 *아웃* 폴더에서 *CheckoutStart.aspx.cs*라는 코드 뒤에 파일을 엽니다.   
   코드 숨결 파일을 열어야 합니다.
2. 기존 코드를 다음으로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

응용 프로그램의 사용자가 장바구니 페이지의 **체크 아웃** 단추를 클릭하면 브라우저는 *CheckoutStart.aspx* 페이지로 이동합니다. *CheckoutStart.aspx* 페이지가 로드되면 `ShortcutExpressCheckout` 메서드가 호출됩니다. 이 시점에서 사용자는 PayPal 테스트 웹 사이트로 전송됩니다. 페이팔 사이트에서 사용자는 PayPal 자격 증명을 입력하고 구매 세부 정보를 검토하고 PayPal 계약을 수락하고 메서드가 `ShortcutExpressCheckout` 완료되는 Wingtip Toys 샘플 응용 프로그램으로 돌아갑니다. 메서드가 `ShortcutExpressCheckout` 완료되면 `ShortcutExpressCheckout` 메서드에 지정된 *CheckoutReview.aspx* 페이지로 사용자를 리디렉션합니다. 이를 통해 사용자는 Wingtip Toys 샘플 응용 프로그램 내에서 주문 세부 정보를 검토할 수 있습니다.

### <a name="review-order-details"></a>주문 세부 정보 검토

페이팔에서 반환 한 후, Wingtip 장난감 샘플 응용 프로그램의 *체크 아웃검토.aspx* 페이지 주문 세부 사항을 표시 합니다. 이 페이지에서는 제품을 구입하기 전에 주문 세부 정보를 검토할 수 있습니다. *CheckoutReview.aspx* 페이지는 다음과 같이 만들어야 합니다.

1. 체크 *아웃* 폴더에서 *CheckoutReview.aspx*라는 페이지를 엽니다.
2. 기존 태그를 다음으로 바꿉꿉을 바꿉입니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. *CheckoutReview.aspx.cs* 라는 코드 뒤에 페이지를 열고 기존 코드를 다음과 같은 것으로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**DetailsView** 컨트롤은 PayPal에서 반환된 주문 세부 정보를 표시하는 데 사용됩니다. 또한 위의 코드는 주문 세부 정보를 Wingtip Toys `OrderDetail` 데이터베이스에 개체로 저장합니다. 사용자가 **주문 완료** 버튼을 클릭하면 *체크 아웃Complete.aspx* 페이지로 리디렉션됩니다.

> [!NOTE] 
> 
> **팁**
> 
> *CheckoutReview.aspx* 페이지의 태그에서 `<ItemStyle>` 태그는 페이지 하단 근처의 **DetailsView** 컨트롤 내의 항목 스타일을 변경하는 데 사용됩니다. **디자인 보기의** 페이지를 보고(Visual Studio의 왼쪽 아래 모서리에서 **디자인을** 선택한 다음 **DetailsView** 컨트롤을 선택하고 **스마트 태그(컨트롤** 의 오른쪽 상단에 있는 화살표 아이콘)를 선택하면 **DetailsView 작업을**볼 수 있습니다.
> 
> ![페이팔로 결제 및 결제 - 필드 편집](checkout-and-payment-with-paypal/_static/image18.png)
> 
> 필드 **편집을**선택하면 **필드** 대화 상자가 나타납니다. 이 대화 상자에서 **DetailsView** 컨트롤의 **ItemStyle**, 와 같은 시각적 속성을 쉽게 제어할 수 있습니다.
> 
> ![페이팔로 결제 및 결제 - 필드 대화 상자](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>전체 구매

*체크 아웃완료.aspx* 페이지는 페이팔에서 구입합니다. 위에서 언급했듯이 사용자는 응용 프로그램이 *CheckoutComplete.aspx* 페이지로 이동하기 전에 **주문 완료** 버튼을 클릭해야 합니다.

1. 체크 *아웃* 폴더에서 체크 아웃이라는 페이지를 엽니다.Complete.aspx . *CheckoutComplete.aspx*
2. 기존 태그를 다음으로 바꿉꿉을 바꿉입니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. *CheckoutComplete.aspx.cs* 라는 코드 뒤에 페이지를 열고 기존 코드를 다음과 같은 것으로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

체크 *아웃Complete.aspx* 페이지가 로드 `DoCheckoutPayment` 될 때 메서드가 호출 됩니다. 앞에서 설명한 `DoCheckoutPayment` 것처럼 이 방법은 PayPal 테스트 환경에서 구매를 완료합니다. PayPal이 주문 구매를 완료하면 *결제Complete.aspx* 페이지에 구매자에게 결제 `ID` 트랜잭션이 표시됩니다.

### <a name="handle-cancel-purchase"></a>구매 취소 처리

사용자가 구매를 취소하기로 결정한 경우 *CheckoutCancel.aspx* 페이지로 이동하여 주문이 취소되었음을 확인할 수 있습니다.

1. *체크 아웃* 폴더에서 *CheckoutCancel.aspx라는* 페이지를 엽니다.
2. 기존 태그를 다음으로 바꿉꿉을 바꿉입니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>구매 오류 처리

구매 프로세스 중 오류는 *CheckoutError.aspx* 페이지에서 처리합니다. *CheckoutStart.aspx* 페이지의 코드 뒤에, *CheckoutReview.aspx* 페이지, 그리고 *체크 아웃Complete.aspx* 페이지 각 리디렉션됩니다 *체크 아웃Error.aspx* 오류 발생 하는 경우 페이지.

1. *체크 아웃* 폴더에서 *CheckoutError.aspx라는* 페이지를 엽니다.
2. 기존 태그를 다음으로 바꿉꿉을 바꿉입니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

*체크 아웃Error.aspx* 페이지는 체크 아웃 프로세스 중에 오류가 발생할 때 오류 세부 정보와 함께 표시됩니다.

## <a name="running-the-application"></a>애플리케이션 실행

응용 프로그램을 실행하여 제품을 구입하는 방법을 확인합니다. 페이팔 테스트 환경에서 실행됩니다. 실제 돈은 교환되지 않습니다.

1. 모든 파일이 Visual Studio에 저장되어 있는지 확인합니다.
2. 웹 브라우저를 열고 [https://developer.paypal.com](https://developer.paypal.com/)로 이동합니다.
3. 이 자습서의 앞에서 만든 PayPal 개발자 계정으로 로그인합니다.  
   페이팔의 개발자 샌드 박스에 대 한, 익스프레스 [https://developer.paypal.com](https://developer.paypal.com/) 체크 아웃을 테스트 하려면 로그인 해야. 이는 페이팔의 샌드박스 테스트에만 적용되며 페이팔의 라이브 환경에는 적용되지 않습니다.
4. 비주얼 스튜디오에서 **F5를** 눌러 Wingtip Toys 샘플 응용 프로그램을 실행합니다.  
   데이터베이스가 다시 빌드되면 브라우저가 열리고 *Default.aspx* 페이지가 표시됩니다.
5. '자동차'와 같은 제품 카테고리를 선택한 다음 각 제품 옆에 **장바구니에 추가를** 클릭하여 장바구니에 세 가지 다른 제품을 추가합니다.  
   장바구니에 선택한 제품이 표시됩니다.
6. 결제하려면 **페이팔** 버튼을 클릭합니다. 

    ![페이팔로 결제 및 결제 - 카트](checkout-and-payment-with-paypal/_static/image20.png)

   체크 아웃하려면 Wingtip Toys 샘플 응용 프로그램에 대한 사용자 계정이 있어야 합니다.
7. 페이지 오른쪽에 있는 **Google** 링크를 클릭하여 기존 gmail.com 이메일 계정으로 로그인합니다.  
   gmail.com 계정이 없는 경우 [www.gmail.com](https://www.gmail.com/)에서 테스트 목적으로 계정을 만들 수 있습니다. "등록"을 클릭하여 표준 로컬 계정을 사용할 수도 있습니다. 

    ![페이팔로 결제 및 결제 - 로그인](checkout-and-payment-with-paypal/_static/image21.png)
8. Gmail 계정 및 비밀번호로 로그인합니다. 

    ![페이팔로 결제 및 결제 - Gmail 로그인](checkout-and-payment-with-paypal/_static/image22.png)
9. **로그인** 버튼을 클릭하여 Wingtip Toys 샘플 응용 프로그램 사용자 이름으로 Gmail 계정을 등록합니다. 

    ![페이팔로 결제 및 결제 - 계정 등록](checkout-and-payment-with-paypal/_static/image23.png)
10. PayPal 테스트 사이트에서 이 자습서의 앞부분에서 만든 **구매자** 이메일 주소와 암호를 추가한 다음 **로그인** 버튼을 클릭합니다. 

    ![페이팔로 결제 및 결제 - 페이팔 로그인](checkout-and-payment-with-paypal/_static/image24.png)
11. PayPal 정책에 동의하고 **동의 및 계속** 버튼을 클릭합니다.  
    이 페이지는 이 PayPal 계정을 처음 사용할 때만 표시됩니다. 다시이 테스트 계정입니다, 실제 돈이 교환되지 않습니다. 

    ![페이팔 결제 및 결제 - 페이팔 정책](checkout-and-payment-with-paypal/_static/image25.png)
12. PayPal 테스트 환경 검토 페이지에서 주문 정보를 검토하고 **계속을 클릭합니다.** 

    ![페이팔로 결제 및 결제 - 리뷰 정보](checkout-and-payment-with-paypal/_static/image26.png)
13. *CheckoutReview.aspx* 페이지에서 주문 금액을 확인하고 생성된 배송 주소를 확인합니다. 그런 다음 **주문 완료** 버튼을 클릭합니다. 

    ![페이팔결제 - 주문 검토](checkout-and-payment-with-paypal/_static/image27.png)
14. **결제완료.aspx** 페이지가 결제 거래 ID와 함께 표시됩니다. 

    ![페이팔로 결제 및 결제 - 결제 완료](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>데이터베이스 검토

응용 프로그램을 실행한 후 Wingtip Toys 샘플 응용 프로그램 데이터베이스에서 업데이트된 데이터를 검토하면 응용 프로그램이 제품 구매를 성공적으로 기록한 것을 확인할 수 있습니다.

이 자습서 시리즈의 이전과 마찬가지로 **데이터베이스 탐색기** 창(Visual Studio의**서버 탐색기** 창)을 사용하여 *Wingtiptoys.mdf* 데이터베이스 파일에 포함된 데이터를 검사할 수 있습니다.

1. 여전히 열려 있는 경우 브라우저 창을 닫습니다.
2. Visual Studio에서 **솔루션 탐색기** 상단의 **모든 파일 표시** 아이콘을 선택하여 앱 **\_데이터** 폴더를 확장할 수 있습니다.
3. **앱\_데이터** 폴더를 확장합니다.  
 폴더에 대한 **모든 파일 표시** 아이콘을 선택해야 할 수 있습니다.
4. *Wingtiptoys.mdf* 데이터베이스 파일을 마우스 오른쪽 단추로 클릭하고 **열기를**선택합니다.  
    **서버 탐색기가** 표시됩니다.
5. **테이블** 폴더를 확장합니다.
6. **주문**테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 데이터 표시를**선택합니다.  
 **Orders** 테이블이 표시됩니다.
7. **결제트랜잭션ID** 열을 검토하여 성공적인 트랜잭션을 확인합니다. 

    ![페이팔로 결제 및 결제 - 데이터베이스 검토](checkout-and-payment-with-paypal/_static/image29.png)
8. **주문** 테이블 창을 닫습니다.
9. 서버 탐색기에서 **OrderDetails** 테이블을 마우스 오른쪽 단추로 클릭하고 **테이블 데이터 표시를**선택합니다.
10. OrderDetails `OrderId` `Username` 테이블의 값과 값을 **검토합니다.** 이러한 값은 `OrderId` **Orders** `Username` 테이블에 포함된 값과 일치합니다.
11. **OrderDetails** 테이블 창을 닫습니다.
12. 윙팁 장난감 데이터베이스*파일(Wingtiptoys.mdf)을*마우스 오른쪽 버튼으로 클릭하고 **연결 닫기를**선택합니다.
13. **솔루션 탐색기** 창이 표시되지 않으면 **서버 탐색기** 창 하단의 **솔루션 탐색기를** 클릭하여 **솔루션 탐색기를** 다시 표시합니다.

## <a name="summary"></a>요약

이 자습서에서는 제품 구매를 추적하기 위해 주문 및 주문 세부 스키마를 추가했습니다. 또한 PayPal 기능을 Wingtip Toys 샘플 애플리케이션에 통합했습니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 구성 개요](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[Azure 앱 서비스에 멤버십, OAuth 및 SQL 데이터베이스를 사용하여 보안 ASP.NET 웹 양식 앱 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[마이크로소프트 Azure - 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>고지 사항

이 자습서에는 샘플 코드가 포함되어 있습니다. 이러한 샘플 코드는 어떤 종류의 보증없이 "있는 대로"제공됩니다. 따라서 Microsoft는 샘플 코드의 정확성, 무결성 또는 품질을 보장하지 않습니다. 당신은 당신의 자신의 위험에 샘플 코드를 사용하는 데 동의합니다. 어떠한 경우에도 Microsoft는 샘플 코드, 콘텐츠(이에 국한되지 않음)에 대해 어떠한 방식으로든 귀하에게 책임을 지지 않으며, 샘플 코드, 콘텐츠 또는 샘플 코드 사용으로 인해 발생한 모든 종류의 손실 또는 손상을 포함하되 이에 국한되지 않습니다. 귀하는 이에 대해 Microsoft가 게시, 전송, 사용 또는 이에 국한되지 않는 자료를 포함하되 이에 국한되지 않는 모든 종류의 손실, 손실, 상해 또는 손해에 대해 무해한 배상, 저장 및 보유하는 데 동의합니다.

> [!div class="step-by-step"]
> [이전](shopping-cart.md)
> [다음](membership-and-administration.md)
