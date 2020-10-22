---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: PayPal으로 체크 아웃 및 지불 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345649"
---
# <a name="checkout-and-payment-with-paypal"></a>PayPal로 체크 아웃 및 지불

[Erik Reitan](https://github.com/Erikre)

[정문 장난감 샘플 프로젝트 다운로드 (c #)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. 이 자습서 시리즈와 함께 사용할 수 있는 [c # 소스 코드를 사용](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트입니다.

이 자습서에서는 PayPal을 사용 하 여 사용자 권한 부여, 등록 및 지불을 포함 하도록 정문 장난감 샘플 응용 프로그램을 수정 하는 방법을 설명 합니다. 로그인 한 사용자 에게만 제품을 구매할 수 있는 권한이 부여 됩니다. ASP.NET 4.5 Web Forms 프로젝트 템플릿의 기본 제공 사용자 등록 기능에는 이미 필요한 많은 항목이 포함 되어 있습니다. PayPal Express 체크 아웃 기능을 추가 합니다. 이 자습서에서는 PayPal 개발자 테스트 환경을 사용 하므로 실제 자금은 전송 되지 않습니다. 이 자습서의 끝 부분에서는 쇼핑 카트에 추가할 제품을 선택 하 고, 체크 아웃 단추를 클릭 하 고, 데이터를 PayPal 테스트 웹 사이트로 전송 하 여 응용 프로그램을 테스트 합니다. PayPal 테스트 웹 사이트에서 배송 및 지불 정보를 확인 한 다음 로컬 정문 장난감 샘플 응용 프로그램으로 돌아가 구매를 확인 하 고 완료 합니다.

확장성 및 보안을 해결 하는 온라인 쇼핑을 전문적으로 하는 여러 가지 숙련 된 타사 지불 프로세서가 있습니다. ASP.NET 개발자는 쇼핑 및 구매 솔루션을 구현 하기 전에 타사 지불 솔루션을 활용 하는 이점을 고려해 야 합니다.

> [!NOTE] 
> 
> 정문 장난감 샘플 응용 프로그램은 ASP.NET 웹 개발자가 사용할 수 있는 특정 ASP.NET 개념 및 기능을 보여 주도록 설계 되었습니다. 이 샘플 응용 프로그램은 확장성 및 보안과 관련 하 여 가능한 모든 상황에 대해 최적화 되지 않았습니다.

## <a name="what-youll-learn"></a>학습할 내용:

- 폴더의 특정 페이지에 대 한 액세스를 제한 하는 방법
- 익명 쇼핑 카트에서 알려진 장바구니를 만드는 방법
- 프로젝트에 대해 SSL을 사용 하도록 설정 하는 방법
- 프로젝트에 OAuth 공급자를 추가 하는 방법
- Paypal 테스트 환경을 사용 하 여 제품을 구매 하는 데 PayPal을 사용 하는 방법입니다.
- **DetailsView** 컨트롤에서 PayPal의 세부 정보를 표시 하는 방법입니다.
- PayPal에서 얻은 세부 정보를 사용 하 여 정문 장난감 응용 프로그램의 데이터베이스를 업데이트 하는 방법입니다.

## <a name="adding-order-tracking"></a>주문 추적 추가

이 자습서에서는 사용자가 만든 순서에서 데이터를 추적 하는 두 개의 새 클래스를 만듭니다. 이 클래스는 배송 정보, 구매 총액 및 지불 확인에 대 한 데이터를 추적 합니다.

### <a name="add-the-order-and-orderdetail-model-classes"></a>Order 및 OrderDetail 모델 클래스 추가

이 자습서 시리즈의 앞부분에서는 `Category` `Product` `CartItem` *모델* 폴더에서, 및 클래스를 만들어 범주, 제품 및 쇼핑 카트 항목에 대 한 스키마를 정의 했습니다. 이제 두 개의 새 클래스를 추가 하 여 제품 주문 및 주문 세부 정보에 대 한 스키마를 정의 합니다.

1. **모델** 폴더에서 이름이 *Order.cs*인 새 클래스를 추가 합니다.   
   새 클래스 파일이 편집기에 표시 됩니다.
2. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. *모델* 폴더에 *OrderDetail.cs* 클래스를 추가 합니다.
4. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order`및 클래스에는 `OrderDetail` 구매 및 배송에 사용 되는 주문 정보를 정의 하는 스키마가 포함 되어 있습니다.

또한 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 데이터베이스 컨텍스트 클래스를 업데이트 해야 합니다. 이렇게 하려면 새로 만든 주문 및 `OrderDetail` 모델 클래스를 클래스에 추가 합니다 `ProductContext` .

1. **솔루션 탐색기**에서 *ProductContext.cs* 파일을 찾아 엽니다.
2. 아래와 같이 강조 표시 된 코드를 *ProductContext.cs* 파일에 추가 합니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

이 자습서 시리즈의 앞에서 설명한 것 처럼 *ProductContext.cs* 파일의 코드는 `System.Data.Entity` 네임 스페이스를 추가 하므로 Entity Framework의 모든 핵심 기능에 액세스할 수 있습니다. 이 기능에는 강력한 형식의 개체를 사용 하 여 데이터를 쿼리, 삽입, 업데이트 및 삭제 하는 기능이 포함 됩니다. 클래스의 위 코드는 `ProductContext` 새로 추가 된 및 클래스에 대 한 Entity Framework 액세스 권한을 추가 합니다 `Order` `OrderDetail` .

## <a name="adding-checkout-access"></a>체크 아웃 액세스 추가

정문 장난감 샘플 응용 프로그램은 익명 사용자가 쇼핑 카트에 제품을 검토 하 고 추가할 수 있도록 허용 합니다. 그러나 익명 사용자가 쇼핑 카트에 추가 하는 제품을 구매 하도록 선택 하는 경우 사이트에 로그온 해야 합니다. 로그온 하면 체크 아웃 및 구매 프로세스를 처리 하는 웹 응용 프로그램의 제한 된 페이지에 액세스할 수 있습니다. 이러한 제한 된 페이지는 응용 프로그램의 *체크 아웃* 폴더에 포함 되어 있습니다.

### <a name="add-a-checkout-folder-and-pages"></a>체크 아웃 폴더 및 페이지 추가

이제 체크 아웃 하는 동안 고객에 게 표시 되는 *체크 아웃* 폴더와 해당 폴더의 페이지를 만들게 됩니다. 이 자습서의 뒷부분에서 이러한 페이지를 업데이트 합니다.

1. **솔루션 탐색기** 에서 프로젝트 이름 (**정문 장난감**)을 마우스 오른쪽 단추로 클릭 하 고 **새 폴더 추가를**선택 합니다. 

    ![PayPal으로 체크 아웃 및 지불-새 폴더](checkout-and-payment-with-paypal/_static/image1.png)
2. 새 폴더의 이름을 *Checkout*로 합니다.
3. *체크 아웃* 폴더를 마우스 오른쪽 단추로 클릭 한 **Add**다음 - &gt; **새 항목**추가를 선택 합니다. 

    ![PayPal 체크 아웃 및 지불-새 항목](checkout-and-payment-with-paypal/_static/image2.png)
4. **새 항목 추가** 대화 상자가 표시됩니다.
5. 왼쪽의 **Visual c #**  - &gt; **웹** 템플릿 그룹을 선택 합니다. 그런 다음 가운데 창에서 **마스터 페이지로 웹 폼**을 선택 하 고 이름을 *CheckoutStart*로 바꿉니다. 

    ![PayPal 체크 아웃 및 지불-새 항목 추가 대화 상자](checkout-and-payment-with-paypal/_static/image3.png)
6. 이전과 마찬가지로 *사이트 .master* 파일을 마스터 페이지로 선택 합니다.
7. 위의 동일한 단계를 사용 하 여 다음과 같은 추가 페이지를 *체크 아웃* 폴더에 추가 합니다.   

    - CheckoutReview
    - CheckoutComplete
    - CheckoutCancel
    - CheckoutError

### <a name="add-a-webconfig-file"></a>Web.config 파일 추가

*체크 아웃* 폴더에 새 *Web.config* 파일을 추가 하면 폴더에 포함 된 모든 페이지에 대 한 액세스를 제한할 수 있습니다.

1. *체크 아웃* 폴더를 마우스 오른쪽 단추로 클릭 **Add** 하 고  - &gt; **새 항목**추가를 선택 합니다.  
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 왼쪽의 **Visual c #**  - &gt; **웹** 템플릿 그룹을 선택 합니다. 그런 다음 가운데 창에서 **웹 구성 파일**을 선택 하 고 *Web.config*기본 이름을 적용 한 다음 **추가**를 선택 합니다.
3. *Web.config* 파일의 기존 XML 콘텐츠를 다음으로 바꿉니다.  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. *Web.config* 파일을 저장합니다.

*Web.config* 파일은 웹 응용 프로그램의 모든 알 수 없는 사용자가 *체크 아웃* 폴더에 포함 된 페이지에 대 한 액세스를 거부 하도록 지정 합니다. 그러나 사용자가 계정을 등록 하 고 로그온 한 경우에는 알려진 사용자가 되며 *Checkout* 폴더의 페이지에 액세스할 수 있습니다.

ASP.NET 구성은 계층 구조를 따르며, 각 *Web.config* 파일에는 구성 설정이 있는 폴더와 그 아래에 있는 모든 하위 디렉터리에 대 한 구성 설정이 적용 됩니다.

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>프로젝트에 SSL 사용

 SSL(Secure Sockets Layer)은 웹 서버 및 웹 클라이언트가 암호화를 사용하여 더욱 안전하게 통신할 수 있도록 정의된 프로토콜입니다. SSL을 사용하지 않으면 네트워크에 실제로 액세스하여 패킷을 스니핑하는 누군가에게 클라이언트와 서버 간에 전송된 데이터가 노출됩니다. 또한 몇 가지 일반적인 인증 체계는 일반 HTTP를 통해서는 보호되지 않습니다. 특히, 기본 인증 및 폼 인증은 암호화되지 않은 자격 증명을 보냅니다. 보안을 위해서 인증 체계는 SSL을 사용해야 합니다. 

1. **솔루션 탐색기**에서 **WingtipToys** 프로젝트를 클릭 한 다음 **F4** 키를 눌러 **속성** 창을 표시 합니다.
2. **SSL 사용** 을로 변경 `true` 합니다.
3. 나중에 사용할 수 있도록 **SSL URL** 을 복사합니다.   
 `https://localhost:44300/`이전에 Ssl 웹 사이트를 만들지 않은 경우 SSL URL은 다음과 같이 표시 됩니다.   
    ![프로젝트 속성](checkout-and-payment-with-paypal/_static/image4.png)
4. **솔루션 탐색기**에서 **WingtipToys** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다.
5. 왼쪽 탭에서 **웹**을 클릭합니다.
6. 이전에 저장 한 **SSL url** 을 사용 하도록 **프로젝트 url** 을 변경 합니다.   
    ![프로젝트 웹 속성](checkout-and-payment-with-paypal/_static/image5.png)
7. **CTRL+S**키를 눌러 페이지를 저장합니다.
8. **Ctrl+F5**를 눌러 애플리케이션을 실행합니다. Visual Studio에서 SSL 경고를 방지할 수 있도록 하는 옵션을 표시합니다.
9. **예** 를 클릭하여 IIS Express SSL 인증서를 신뢰하고 계속합니다.   
    ![IIS Express SSL 인증서 정보](checkout-and-payment-with-paypal/_static/image6.png)  
  보안 경고가 표시됩니다.
10. **예** 를 클릭하여 인증서를 localhost에 설치합니다.   
    ![보안 경고 대화 상자](checkout-and-payment-with-paypal/_static/image7.png)  
  브라우저 창이 표시됩니다.

이제 SSL을 사용 하 여 웹 응용 프로그램을 로컬로 쉽게 테스트할 수 있습니다.

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>OAuth 2.0 공급자 추가

ASP.NET Web Forms는 멤버 자격 및 인증을 위해 개선된 옵션을 제공합니다. 이러한 개선 사항에는 OAuth가 포함됩니다. OAuth는 웹, 모바일 및 데스크톱 애플리케이션에서 간단한 표준 메서드로 보안 권한 부여를 허용하는 개방형 프로토콜입니다. ASP.NET Web Forms 템플릿에서는 OAuth를 사용 하 여 Facebook, Twitter, Google 및 Microsoft를 인증 공급자로 노출 합니다. 이 자습서에서는 인증 공급자로 Google만 사용하지만 다른 공급자를 사용하도록 코드를 쉽게 수정할 수 있습니다. 다른 공급자를 구현하는 단계도 이 자습서에 표시되는 단계와 매우 비슷합니다.

자습서에서는 인증 외에도 역할을 사용하여 권한 부여를 구현합니다. `canEdit` 역할에 추가한 사용자만 데이터를 변경할 수 있습니다(연락처 만들기, 편집 또는 삭제).

> [!NOTE] 
> 
> Windows Live 응용 프로그램은 작업 중인 웹 사이트의 라이브 URL만 허용 하므로 로그인 테스트에는 로컬 웹 사이트 URL을 사용할 수 없습니다.

다음 단계를 통해 Google 인증 공급자를 추가할 수 있습니다.

1. *앱 \_ Start\Startup.Auth.cs* 파일을 엽니다.
2. 메서드가 다음과 같이 나타나도록 `app.UseGoogleAuthentication()` 메서드에서 주석 문자를 제거합니다. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. [Google Developers Console](https://console.developers.google.com/)로 이동합니다. Google 개발자 메일 계정(gmail.com)으로 로그인해야 합니다. Google 계정이 없으면 **계정 만들기** 링크를 선택합니다.   
   다음으로, **Google 개발자 콘솔**이 표시됩니다.   
    ![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)
4. **프로젝트 만들기** 단추를 클릭 하 고 프로젝트 이름 및 ID (기본값을 사용할 수 있음)를 입력 합니다. 그런 다음 **규약 확인란** 을 클릭 하 고 **만들기** 단추를 클릭 합니다.  

    ![Google-새 프로젝트](checkout-and-payment-with-paypal/_static/image9.png)

    몇 초 내에 새 프로젝트가 만들어지고 브라우저에 새 프로젝트 페이지가 표시됩니다.
5. 왼쪽 탭에서 **api &amp; 인증**을 클릭 한 다음 **자격 증명**을 클릭 합니다.
6. **OAuth**에서 **새 클라이언트 ID 만들기** 를 클릭 합니다.   
   **Create Client ID** 대화 상자가 표시됩니다.   
    ![Google - 클라이언트 ID 만들기](checkout-and-payment-with-paypal/_static/image10.png)
7. **클라이언트 ID 만들기** 대화 상자에서 응용 프로그램 유형에 대 한 기본 **웹 응용 프로그램** 을 유지 합니다.
8. 다른 SSL 프로젝트를 만든 경우를 제외 하 고이 자습서의 앞부분에서 사용한 SSL URL에 **권한이 부여 된 JavaScript 원본을** 설정 `https://localhost:44300/` 합니다.   
   이 URL이 애플리케이션의 원점입니다. 이 샘플의 경우 localhost 테스트 URL만 입력합니다. 그러나 localhost 및 production를 고려 하 여 여러 Url을 입력할 수 있습니다.
9. **Authorized Redirect URI** 를 다음으로 설정합니다. 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   이 값은 ASP.NET OAuth 사용자가 Google OAuth 서버와 통신하는 데 사용하는 URI입니다. 다른 SSL 프로젝트를 만든 경우를 제외 하 고 위에서 사용한 SSL URL을 기억할 수 있습니다    `https://localhost:44300/` .
10. **클라이언트 ID 만들기** 단추를 클릭 합니다.
11. Google 개발자 콘솔의 왼쪽 메뉴에서 **동의 화면** 메뉴 항목을 클릭 한 다음 전자 메일 주소 및 제품 이름을 설정 합니다. 양식을 완료 했으면 **저장**을 클릭 합니다.
12. **Api** 메뉴 항목을 클릭 하 고 아래로 스크롤하여 **Google + API**옆의 **끄기** 단추를 클릭 합니다.   
    이 옵션을 적용 하면 Google + API를 사용할 수 있습니다.
13. 또한 **Owin** NuGet 패키지를 버전 3.0.0로 업데이트 해야 합니다.   
    **도구** 메뉴에서 **nuget 패키지 관리자** 를 선택한 다음, **솔루션용 nuget 패키지 관리**를 선택 합니다.  
    **NuGet 패키지 관리** 창에서 **Owin** 패키지를 찾아 버전 3.0.0로 업데이트 합니다.
14. Visual Studio에서 `UseGoogleAuthentication` **클라이언트 ID** 및 **클라이언트 암호** 를 복사 하 여 메서드에 붙여넣어 *Startup.Auth.cs* 페이지의 메서드를 업데이트 합니다. 아래 표시 된 **클라이언트 ID** 및 **클라이언트 암호** 값은 샘플 이며 작동 하지 않습니다. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. **Ctrl + F5** 키를 눌러 응용 프로그램을 빌드하고 실행 합니다. **로그인** 링크를 클릭합니다.
16. **다른 서비스를 사용 하 여 로그인**에서 **Google**을 클릭 합니다.  
    ![로그인](checkout-and-payment-with-paypal/_static/image11.png)
17. 자격 증명을 입력해야 하는 경우 자격 증명을 입력할 google 사이트로 리디렉션됩니다.  
    ![Google - 로그인](checkout-and-payment-with-paypal/_static/image12.png)
18. 자격 증명을 입력 하면 방금 만든 웹 응용 프로그램에 대 한 권한을 부여 하 라는 메시지가 표시 됩니다.  
    ![프로젝트 기본 서비스 계정](checkout-and-payment-with-paypal/_static/image13.png)
19. **Accept**를 클릭합니다. 이제 Google 계정을 등록할 수 있는 **WingtipToys** 응용 프로그램의 **등록** 페이지로 다시 리디렉션됩니다.  
    ![Google 계정을 사용하여 등록](checkout-and-payment-with-paypal/_static/image14.png)
20. Gmail 계정에 사용되는 로컬 전자 메일 등록 이름을 변경할 수 있지만 일반적으로 기본 전자 메일 별칭(즉, 인증에 사용하는 별칭)을 그대로 사용합니다. 위와 같이 **로그인을** 클릭 합니다.

### <a name="modifying-login-functionality"></a>로그인 기능 수정

앞에서 설명한 것 처럼이 자습서 시리즈에서는 대부분의 사용자 등록 기능이 기본적으로 ASP.NET Web Forms 템플릿에 포함 되었습니다. 이제 기본 *login.aspx* 를 수정 하 고 메서드를 호출 하는 .aspx 페이지를 *등록 합니다* . `MigrateCart` `MigrateCart`메서드는 새로 로그인 한 사용자를 익명 쇼핑 카트에 연결 합니다. 사용자와 쇼핑 카트를 연결 하 여 정문 장난감 샘플 응용 프로그램은 방문 간에 사용자의 쇼핑 카트를 유지 관리할 수 있습니다.

1. **솔루션 탐색기**에서 *계정* 폴더를 찾아서 엽니다.
2. *Login.aspx.cs* 라는 코드를 포함 하는 코드를 수정 하 여 다음과 같이 표시 되도록 코드를 노란색으로 표시 합니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. *Login.aspx.cs* 파일을 저장 합니다.

지금은 메서드에 대 한 정의가 없다는 경고를 무시 해도 됩니다 `MigrateCart` . 이 자습서의 뒷부분에서 조금 더 추가 될 것입니다.

*Login.aspx.cs* 코드 숨김이 로그인 메서드를 지원 합니다. Login.aspx 페이지를 검사 하면이 페이지에 "로그인" 단추가 표시 됩니다. 클릭 하면 코드 숨김으로 처리기가 트리거될 수 있습니다 `LogIn` .

`Login` *Login.aspx.cs* 에 대 한 메서드가 호출 되 면 라는 장바구니의 새 인스턴스가 `usersShoppingCart` 만들어집니다. 쇼핑 카트 ID (GUID)를 검색 하 여 `cartId` 변수로 설정 합니다. 그런 다음 메서드를 호출 하 여 `MigrateCart` `cartId` 로그인 한 사용자의 및 이름을 모두이 메서드에 전달 합니다. 쇼핑 카트를 마이그레이션하면 익명 쇼핑 카트를 식별 하는 데 사용 되는 GUID가 사용자 이름으로 바뀝니다.

사용자가 로그인 할 때 장바구니를 마이그레이션하도록 *Login.aspx.cs* 코드를 수정 하는 것 외에도, 사용자가 새 계정을 만들고 로그인 할 때 쇼핑 카트를 마이그레이션하도록 *Register.aspx.cs 코드 숨김으로 파일* 을 수정 해야 합니다.

1. *계정* 폴더에서 이름이 *Register.aspx.cs*인 코드 숨겨진 파일을 엽니다.
2. 다음과 같이 표시 되도록 코드를 노란색으로 포함 하 여 코드 숨김으로 파일을 수정 합니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. *Register.aspx.cs* 파일을 저장 합니다. 다시 한 번, 메서드에 대 한 경고를 무시 합니다 `MigrateCart` .

이벤트 처리기에서 사용한 코드는 `CreateUser_Click` 메서드에서 사용한 코드와 매우 비슷합니다 `LogIn` . 사용자가 사이트에 등록 하거나 로그인 하면 `MigrateCart` 메서드 호출이 수행 됩니다.

## <a name="migrating-the-shopping-cart"></a>쇼핑 카트 마이그레이션

로그인 및 등록 프로세스를 업데이트 했으므로 이제 메서드를 사용 하 여 쇼핑 카트를 마이그레이션하는 코드를 추가할 수 있습니다 `MigrateCart` .

1. **솔루션 탐색기**에서 *논리* 폴더를 찾아 *ShoppingCartActions.cs* 클래스 파일을 엽니다.
2. *ShoppingCartActions.cs* 파일의 기존 코드에 노란색으로 강조 표시 된 코드를 추가 하 여 *ShoppingCartActions.cs* 파일의 코드가 다음과 같이 표시 되도록 합니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

`MigrateCart`메서드는 기존 cartId를 사용 하 여 사용자의 쇼핑 카트를 찾습니다. 그런 다음 코드는 모든 쇼핑 카트 항목을 반복 하 고 스키마에 `CartId` 지정 된 대로 속성을 `CartItem` 로그인 한 사용자 이름으로 바꿉니다.

### <a name="updating-the-database-connection"></a>데이터베이스 연결을 업데이트 하는 중

**미리 빌드된** 정문 장난감 샘플 응용 프로그램을 사용 하 여이 자습서를 수행 하는 경우 기본 멤버 자격 데이터베이스를 다시 만들어야 합니다. 기본 연결 문자열을 수정 하 여 다음에 응용 프로그램을 실행할 때 멤버 자격 데이터베이스가 생성 됩니다.

1. 프로젝트의 루트에서 *Web.config* 파일을 엽니다.
2. 기본 연결 문자열을 업데이트 하 여 다음과 같이 표시 되도록 합니다.   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>PayPal 통합

PayPal은 온라인 상인의 지불을 허용 하는 웹 기반 청구 플랫폼입니다. 다음 자습서에서는 PayPal의 빠른 체크 아웃 기능을 응용 프로그램에 통합 하는 방법을 설명 합니다. 빠른 체크 아웃을 사용 하면 고객이 PayPal에 추가한 항목에 대해 PayPal을 사용 하 여 지불할 수 있습니다.

### <a name="create-paypal-test-accounts"></a>PayPal 테스트 계정 만들기

PayPal 테스트 환경을 사용 하려면 개발자 테스트 계정을 만들고 확인 해야 합니다. 개발자 테스트 계정을 사용 하 여 구매자 테스트 계정과 판매자 테스트 계정을 만듭니다. 또한 개발자 테스트 계정 자격 증명을 사용 하 여 정문 장난감 샘플 응용 프로그램에서 PayPal 테스트 환경에 액세스할 수 있습니다.

1. 브라우저에서 PayPal 개발자 테스트 사이트로 이동 합니다.   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. PayPal 개발자 계정이 없으면 **등록**을 클릭 하 고 등록 단계를 수행 하 여 새 계정을 만듭니다. 기존 PayPal 개발자 계정이 있는 **경우 로그인을 클릭 하**여 로그인 합니다. 이 자습서의 뒷부분에서 정문 장난감 샘플 응용 프로그램을 테스트 하려면 PayPal 개발자 계정이 필요 합니다.
3. 방금 PayPal 개발자 계정에 등록 한 경우 paypal 개발자 계정을 PayPal에 확인 해야 할 수 있습니다. 전자 메일 계정에 전송 된 단계를 수행 하 여 계정을 확인할 수 있습니다. PayPal 개발자 계정을 확인 했으면 PayPal 개발자 테스트 사이트에 다시 로그인 합니다.
4. Paypal 개발자 계정으로 PayPal 개발자 사이트에 로그인 한 후에는 PayPal 구매자 테스트 계정을 만들어야 합니다 (아직 없는 경우). 구매자 테스트 계정을 만들려면 PayPal 사이트에서 **응용 프로그램** 탭을 클릭 한 다음 **Sandbox 계정**을 클릭 합니다.   
 **Sandbox 테스트 계정** 페이지가 표시 됩니다.   

    > [!NOTE] 
    > 
    > PayPal 개발자 사이트는 이미 판매자 테스트 계정을 제공 합니다.

    ![PayPal-Sandbox 테스트 계정으로 체크 아웃 및 지불](checkout-and-payment-with-paypal/_static/image15.png)
5. Sandbox 테스트 계정 페이지에서 **계정 만들기**를 클릭 합니다.
6. **테스트 계정 만들기** 페이지에서 선택한 구매자 테스트 계정 전자 메일 및 암호를 선택 합니다.   

    > [!NOTE] 
    > 
    > 이 자습서의 끝 부분에서 정문 장난감 샘플 응용 프로그램을 테스트 하려면 구매자 전자 메일 주소 및 암호가 필요 합니다.

    ![PayPal-Sandbox 테스트 계정으로 체크 아웃 및 지불](checkout-and-payment-with-paypal/_static/image16.png)
7. **계정 만들기** 단추를 클릭 하 여 구매자 테스트 계정을 만듭니다.  
 **Sandbox 테스트 계정** 페이지가 표시 됩니다. 

    ![PayPal-PayPal 계정으로 체크 아웃 및 지불](checkout-and-payment-with-paypal/_static/image17.png)
8. **Sandbox 테스트 계정** 페이지에서 **촉진** 메일 계정을 클릭 합니다.  
    **프로필** 및 **알림** 옵션이 표시 됩니다.
9. **프로필** 옵션을 선택 하 고 **api 자격 증명** 을 클릭 하 여 판매자 테스트 계정에 대 한 api 자격 증명을 확인 합니다.
10. 테스트 API 자격 증명을 메모장에 복사 합니다.

정문 장난감 샘플 응용 프로그램에서 PayPal 테스트 환경으로 API 호출을 수행 하려면 표시 된 클래식 테스트 API 자격 증명 (사용자 이름, 암호 및 서명)이 필요 합니다. 다음 단계에서 자격 증명을 추가 합니다.

### <a name="add-paypal-class-and-api-credentials"></a>PayPal 클래스 및 API 자격 증명 추가

대부분의 PayPal 코드를 단일 클래스에 저장 합니다. 이 클래스는 PayPal과 통신 하는 데 사용 되는 메서드를 포함 합니다. 또한이 클래스에는 PayPal 자격 증명을 추가 합니다.

1. Visual Studio 내의 정문 장난감 샘플 응용 프로그램에서 **논리** 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **Add**  - &gt; **새 항목**추가를 선택 합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 왼쪽의 **설치 됨** 창에서 **Visual c #** 아래에 있는 **코드**를 선택 합니다.
3. 가운데 창에서 **클래스**를 선택 합니다. 새 클래스의 이름을 **PayPalFunctions.cs**로 합니다.
4. **추가**를 클릭합니다.  
   새 클래스 파일이 편집기에 표시 됩니다.
5. 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. 이 자습서의 앞부분에서 표시 한 판매자 API 자격 증명 (사용자 이름, 암호 및 서명)을 추가 하 여 PayPal 테스트 환경에 대 한 함수 호출을 수행할 수 있습니다.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> 이 샘플 응용 프로그램에서는 단순히 c # 파일 (.cs)에 자격 증명을 추가 합니다. 그러나 구현 된 솔루션에서는 구성 파일에서 자격 증명을 암호화 하는 것을 고려해 야 합니다.

NVPAPICaller 클래스에는 대부분의 PayPal 기능이 포함 되어 있습니다. 클래스의 코드는 PayPal 테스트 환경에서 테스트를 구매 하는 데 필요한 메서드를 제공 합니다. 다음 세 개의 PayPal 함수를 사용 하 여 구매를 수행 합니다.

- `SetExpressCheckout` 함수
- `GetExpressCheckoutDetails` 함수
- `DoExpressCheckoutPayment` 함수

`ShortcutExpressCheckout`메서드는 쇼핑 카트에 테스트 구매 정보 및 제품 정보를 수집 하 고 PayPal 함수를 호출 합니다 `SetExpressCheckout` . `GetCheckoutDetails`메서드는 구매 정보를 확인 하 고 `GetExpressCheckoutDetails` 테스트 구매를 수행 하기 전에 PayPal 함수를 호출 합니다. `DoCheckoutPayment`메서드는 PayPal 함수를 호출 하 여 테스트 환경에서 테스트 구매를 완료 합니다 `DoExpressCheckoutPayment` . 나머지 코드는 문자열 인코딩, 문자열 디코딩, 배열 처리 및 자격 증명 확인과 같은 PayPal 메서드 및 프로세스를 지원 합니다.

> [!NOTE] 
> 
> PayPal을 사용 하면 [paypal의 API 사양](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)에 따라 선택적 구매 세부 정보를 포함할 수 있습니다. 정문 장난감 샘플 응용 프로그램의 코드를 확장 하 여 지역화 세부 정보, 제품 설명, 세금, 고객 서비스 번호 및 기타 여러 옵션 필드를 포함할 수 있습니다.

**ShortcutExpressCheckout** 메서드에 지정 된 return 및 cancel url은 포트 번호를 사용 합니다.

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

Visual Web Developer는 SSL을 사용 하 여 웹 프로젝트를 실행 하는 경우 일반적으로 44300 포트를 웹 서버에 사용 합니다. 위와 같이 포트 번호는 44300입니다. 응용 프로그램을 실행 하면 다른 포트 번호가 표시 될 수 있습니다. 이 자습서의 끝 부분에서 정문 장난감 샘플 응용 프로그램을 성공적으로 실행할 수 있도록 코드에서 포트 번호를 올바르게 설정 해야 합니다. 이 자습서의 다음 섹션에서는 로컬 호스트 포트 번호를 검색 하 고 PayPal 클래스를 업데이트 하는 방법을 설명 합니다.

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>PayPal 클래스에서 LocalHost 포트 번호 업데이트

정문 장난감 샘플 응용 프로그램은 PayPal 테스트 사이트로 이동 하 여 정문 장난감 샘플 응용 프로그램의 로컬 인스턴스로 되돌아가는 방법으로 제품을 구입 합니다. PayPal에서 올바른 URL로 돌아가려면 위에서 언급 한 PayPal 코드에서 로컬로 실행 되는 샘플 응용 프로그램의 포트 번호를 지정 해야 합니다.

1. **솔루션 탐색기** 에서 프로젝트 이름 (**WingtipToys**)을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.
2. 왼쪽 열에서 **웹** 탭을 선택 합니다.
3. **프로젝트 Url** 상자에서 포트 번호를 검색 합니다.
4. 필요한 경우 `returnURL` `cancelURL` PayPalFunctions.cs 파일의 PayPal 클래스 ()에서 및를 업데이트 `NVPAPICaller` 하 *PayPalFunctions.cs* 여 웹 응용 프로그램의 포트 번호를 사용 합니다.   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

이제 추가한 코드는 로컬 웹 응용 프로그램에 대해 예상 되는 포트와 일치 합니다. PayPal은 로컬 컴퓨터에서 올바른 URL로 돌아올 수 있습니다.

### <a name="add-the-paypal-checkout-button"></a>PayPal 체크 아웃 단추를 추가 합니다.

이제 샘플 응용 프로그램에 기본 PayPal 함수를 추가 했으므로 이러한 함수를 호출 하는 데 필요한 태그와 코드를 추가 하기 시작할 수 있습니다. 먼저 쇼핑 카트 페이지에서 사용자에 게 표시 되는 체크 아웃 단추를 추가 해야 합니다.

1. *ShoppingCart* 파일을 엽니다.
2. 파일의 아래쪽으로 스크롤하고 `<!--Checkout Placeholder -->` 주석을 찾습니다.
3. 주석이 `ImageButton` 다음과 같이 표시 되도록 주석을 컨트롤로 바꿉니다.  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. *ShoppingCart.aspx.cs* 파일에서 `UpdateBtn_Click` 파일의 끝 부분에 있는 이벤트 처리기 뒤에 이벤트 처리기를 추가 합니다 `CheckOutBtn_Click` .  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. 또한 *ShoppingCart.aspx.cs* 파일에서에 대 한 참조를 추가 합니다 `CheckoutBtn` . 그러면 새 이미지 단추가 다음과 같이 참조 됩니다.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. *ShoppingCart* 파일과 *ShoppingCart.aspx.cs* 파일 모두에 대 한 변경 내용을 저장 합니다.
7. 메뉴에서 **디버그** - &gt; **빌드 WingtipToys**를 선택 합니다.  
   새로 추가 된 **ImageButton** 컨트롤을 사용 하 여 프로젝트를 다시 작성 합니다.

### <a name="send-purchase-details-to-paypal"></a>PayPal에 구매 정보 보내기

사용자가 쇼핑 카트 페이지 (*ShoppingCart*)의 **체크 아웃** 단추를 클릭 하면 구매 프로세스가 시작 됩니다. 다음 코드는 제품을 구매 하는 데 필요한 첫 번째 PayPal 함수를 호출 합니다.

1. *Checkout* 폴더에서 *CheckoutStart.aspx.cs*이라는 코드 숨김으로 파일을 엽니다.   
   코드 숨겨진 파일을 열어야 합니다.
2. 기존 코드를 다음으로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

응용 프로그램의 사용자가 쇼핑 카트 페이지에서 **체크 아웃** 단추를 클릭 하면 브라우저에서 *CheckoutStart* 페이지로 이동 합니다. *CheckoutStart* 페이지가 로드 되 면 `ShortcutExpressCheckout` 메서드가 호출 됩니다. 이 시점에서 사용자는 PayPal 테스트 웹 사이트로 전송 됩니다. PayPal 사이트에서 사용자는 PayPal 자격 증명을 입력 하 고, 구매 세부 정보를 검토 하 고, PayPal 계약을 수락 하 고, 메서드가 완료 된 정문 장난감 샘플 응용 프로그램으로 돌아갑니다 `ShortcutExpressCheckout` . `ShortcutExpressCheckout`메서드가 완료 되 면 사용자를 메서드에 지정 된 *CheckoutReview* 페이지로 리디렉션합니다 `ShortcutExpressCheckout` . 이를 통해 사용자는 정문 장난감 샘플 응용 프로그램 내에서 주문 정보를 검토할 수 있습니다.

### <a name="review-order-details"></a>주문 정보 검토

PayPal에서 반환 된 후에는 정문 장난감 샘플 응용 프로그램의 *CheckoutReview* 페이지에 주문 정보가 표시 됩니다. 이 페이지에서는 제품을 구입 하기 전에 주문 세부 정보를 검토할 수 있습니다. 다음과 같이 *CheckoutReview* 페이지를 만들어야 합니다.

1. *Checkout* 폴더에서 *CheckoutReview*라는 페이지를 엽니다.
2. 기존 태그를 다음으로 바꿉니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. *CheckoutReview.aspx.cs* 라는 코드 숨김으로 페이지를 열고 기존 코드를 다음으로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**DetailsView** 컨트롤은 PayPal에서 반환 된 주문 정보를 표시 하는 데 사용 됩니다. 또한 위의 코드는 주문 정보를 정문 장난감 데이터베이스에 개체로 저장 합니다 `OrderDetail` . 사용자가 **전체 주문** 단추를 클릭 하면 *CheckoutComplete* 페이지로 리디렉션됩니다.

> [!NOTE] 
> 
> **팁**
> 
> *CheckoutReview* 페이지의 태그에서 `<ItemStyle>` 태그는 페이지 아래쪽의 **DetailsView** 컨트롤 내에 있는 항목의 스타일을 변경 하는 데 사용 됩니다. Visual Studio의 왼쪽 아래에 있는 **디자인** 을 선택 하 여 **디자인 뷰에서** 페이지를 본 다음, **detailsview** 컨트롤을 선택 하 고 **스마트 태그** (컨트롤의 오른쪽 위에 있는 화살표 아이콘)를 선택 하면 **DetailsView 작업**을 볼 수 있습니다.
> 
> ![PayPal 체크 아웃 및 지불-필드 편집](checkout-and-payment-with-paypal/_static/image18.png)
> 
> **필드 편집**을 선택 하면 **필드** 대화 상자가 표시 됩니다. 이 대화 상자에서는 **DetailsView** 컨트롤의 시각적 속성 (예: **ItemStyle**)을 쉽게 제어할 수 있습니다.
> 
> ![PayPal-필드 대화 상자를 사용 하 여 체크 아웃 및 지불](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>구매 완료

*CheckoutComplete* 페이지를 사용 하 여 PayPal에서 구매할 수 있습니다. 위에서 설명한 것 처럼 사용자는 응용 프로그램에서 *CheckoutComplete* 페이지로 이동 하기 전에 **전체 순서** 단추를 클릭 해야 합니다.

1. *Checkout* 폴더에서 *CheckoutComplete*라는 페이지를 엽니다.
2. 기존 태그를 다음으로 바꿉니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. *CheckoutComplete.aspx.cs* 라는 코드 숨김으로 페이지를 열고 기존 코드를 다음으로 바꿉니다.   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

*CheckoutComplete* 페이지가 로드 되 면 `DoCheckoutPayment` 메서드가 호출 됩니다. 앞에서 설명한 것 처럼 `DoCheckoutPayment` 메서드는 PayPal 테스트 환경에서 구매를 완료 합니다. PayPal이 주문의 구매를 완료 한 후에는 *CheckoutComplete* 페이지에 구매 지불 트랜잭션이 표시 됩니다 `ID` .

### <a name="handle-cancel-purchase"></a>구매 취소 처리

사용자가 구매를 취소 하기로 결정 하면 해당 주문이 취소 된 것을 확인 하는 *CheckoutCancel* 페이지로 이동 합니다.

1. *Checkout* 폴더에서 *CheckoutCancel* 라는 페이지를 엽니다.
2. 기존 태그를 다음으로 바꿉니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>구매 오류 처리

구매 과정에서 발생 하는 오류는 *CheckoutError* 페이지에서 처리 됩니다. 오류가 발생 하는 경우 *CheckoutStart* 페이지, *CheckoutReview* 페이지 및 *CheckoutComplete* 페이지의 코드 숨김이 각각 *CheckoutError* 로 리디렉션됩니다 (.aspx 페이지).

1. *Checkout* 폴더에서 *CheckoutError* 라는 페이지를 엽니다.
2. 기존 태그를 다음으로 바꿉니다.   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

체크 아웃 프로세스 중에 오류가 발생 하면 *CheckoutError* 페이지가 표시 되 고 오류 정보가 표시 됩니다.

## <a name="running-the-application"></a>애플리케이션 실행

응용 프로그램을 실행 하 여 제품을 구매 하는 방법을 확인 합니다. PayPal 테스트 환경에서 실행 됩니다. 실제 돈을 교환 하지 않습니다.

1. 모든 파일이 Visual Studio에 저장 되었는지 확인 합니다.
2. 웹 브라우저를 열고로 이동 [https://developer.paypal.com](https://developer.paypal.com/) 합니다.
3. 이 자습서의 앞부분에서 만든 PayPal 개발자 계정으로 로그인 합니다.  
   PayPal의 개발자 샌드박스에서 [https://developer.paypal.com](https://developer.paypal.com/) express 체크 아웃을 테스트 하려면에 로그인 해야 합니다. 이는 paypal의 활성 환경에만 적용 되는 PayPal의 샌드박스 테스트에만 적용 됩니다.
4. Visual Studio에서 **F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.  
   데이터베이스를 다시 작성 한 후 브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*
5. 제품 범주를 선택 하 고 (예: "자동차") 각 제품 옆에 있는 **카트에 추가를** 클릭 하 여 쇼핑 카트에 세 가지 제품을 추가 합니다.  
   쇼핑 카트에 선택한 제품이 표시 됩니다.
6. **PayPal** 단추를 클릭 하 여 체크 아웃 합니다. 

    ![PayPal으로 체크 아웃 및 지불-카트](checkout-and-payment-with-paypal/_static/image20.png)

   체크 아웃 하면 정문 장난감 샘플 응용 프로그램에 대 한 사용자 계정이 필요 합니다.
7. 페이지 오른쪽의 **Google** 링크를 클릭 하 여 기존 gmail.com 전자 메일 계정으로 로그인 합니다.  
   Gmail.com 계정이 없는 경우 테스트 목적으로 [www.gmail.com](https://www.gmail.com/)에서 계정을 만들 수 있습니다. "등록"을 클릭 하 여 표준 로컬 계정을 사용할 수도 있습니다. 

    ![PayPal으로 체크 아웃 및 지불-로그인](checkout-and-payment-with-paypal/_static/image21.png)
8. Gmail 계정 및 암호를 사용 하 여 로그인 합니다. 

    ![PayPal 구매 및 결제-Gmail 로그인](checkout-and-payment-with-paypal/_static/image22.png)
9. **로그인** 단추를 클릭 하 여 정문 장난감 샘플 응용 프로그램 사용자 이름으로 gmail 계정을 등록 합니다. 

    ![PayPal을 사용한 체크 아웃 및 지불-계정 등록](checkout-and-payment-with-paypal/_static/image23.png)
10. PayPal 테스트 사이트에서이 자습서의 앞부분에서 만든 **구매자** 전자 메일 주소와 암호를 추가 하 고 **로그인** 단추를 클릭 합니다. 

    ![PayPal-PayPal 로그인을 사용 하 여 Checkout 및 결제](checkout-and-payment-with-paypal/_static/image24.png)
11. PayPal 정책에 동의 하 고 **동의 및 계속** 단추를 클릭 합니다.  
    이 페이지는이 PayPal 계정을 처음 사용할 때만 표시 됩니다. 이는 테스트 계정이 며 실제 돈을 교환 하지 않습니다. 

    ![PayPal-PayPal 정책으로 체크 아웃 및 지불](checkout-and-payment-with-paypal/_static/image25.png)
12. PayPal 테스트 환경 검토 페이지에서 주문 정보를 검토 하 고 **계속**을 클릭 합니다. 

    ![PayPal 체크 아웃 및 지불-정보 검토](checkout-and-payment-with-paypal/_static/image26.png)
13. *CheckoutReview* 페이지에서 주문 금액을 확인 하 고 생성 된 배송 주소를 확인 합니다. 그런 다음 **전체 주문** 단추를 클릭 합니다. 

    ![PayPal 주문 검토를 사용 하 여 체크아웃 및 지불](checkout-and-payment-with-paypal/_static/image27.png)
14. **CheckoutComplete** 페이지가 지불 트랜잭션 ID와 함께 표시 됩니다. 

    ![PayPal 체크 아웃 및 지불-체크 아웃 완료](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>데이터베이스 검토

응용 프로그램을 실행 한 후에는 정문 장난감 샘플 응용 프로그램 데이터베이스의 업데이트 된 데이터를 검토 하 여 응용 프로그램이 제품 구매를 성공적으로 기록 했는지 확인할 수 있습니다.

이 자습서 시리즈의 앞부분에서 했던 것 처럼 **데이터베이스 탐색기** 창 (Visual Studio의**서버 탐색기** 창)을 사용 하 여 *Wingtiptoys* 데이터베이스 파일에 포함 된 데이터를 검사할 수 있습니다.

1. 브라우저 창이 열려 있으면 닫습니다.
2. Visual Studio에서 **솔루션 탐색기** 위쪽의 **모든 파일 표시** 아이콘을 선택 하 여 **앱 \_ 데이터** 폴더를 확장할 수 있습니다.
3. **응용 프로그램 \_ 데이터** 폴더를 확장 합니다.  
 폴더에 대 한 **모든 파일 표시** 아이콘을 선택 해야 할 수도 있습니다.
4. *Wingtiptoys* 데이터베이스 파일을 마우스 오른쪽 단추로 클릭 하 고 **열기**를 선택 합니다.  
    **서버 탐색기** 표시 됩니다.
5. **테이블** 폴더를 확장합니다.
6. **Orders**테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시**를 선택 합니다.  
 **Orders** 테이블이 표시 됩니다.
7. **PaymentTransactionID** 열을 검토 하 여 성공한 트랜잭션을 확인 합니다. 

    ![PayPal 체크 아웃 및 지불-데이터베이스 검토](checkout-and-payment-with-paypal/_static/image29.png)
8. **Orders** 테이블 창을 닫습니다.
9. 서버 탐색기에서 **OrderDetails** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시**를 선택 합니다.
10. `OrderId` `Username` **OrderDetails** 테이블에서 및 값을 검토 합니다. 이러한 값은 `OrderId` `Username` **Orders** 테이블에 포함 된 및 값과 일치 합니다.
11. **OrderDetails** 테이블 창을 닫습니다.
12. 정문 장난감 데이터베이스 파일 (*Wingtiptoys*)을 마우스 오른쪽 단추로 클릭 하 고 **연결 닫기**를 선택 합니다.
13. **솔루션 탐색기** 창이 표시 되지 않으면 **서버 탐색기** 창 맨 아래에 있는 **솔루션 탐색기** 를 클릭 하 여 **솔루션 탐색기** 를 다시 표시 합니다.

## <a name="summary"></a>요약

이 자습서에서는 주문 및 주문 세부 정보 스키마를 추가 하 여 제품 구매를 추적 했습니다. 또한 PayPal 기능을 정문 장난감 샘플 응용 프로그램에 통합 했습니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 구성 개요](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET Web Forms 앱을 배포 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure-무료 평가판](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>고지 사항

이 자습서에는 샘플 코드가 포함 되어 있습니다. 이러한 샘플 코드는 어떠한 종류의 보증도 없이 "있는 그대로" 제공 됩니다. 따라서 Microsoft는 샘플 코드의 정확도, 무결성 또는 품질을 보장 하지 않습니다. 사용자의 위험에 따라 샘플 코드를 사용 하는 것에 동의 하는 것입니다. 어떤 경우에도 Microsoft는 모든 샘플 코드에 대 한 코드, 콘텐츠, 모든 샘플 코드의 오류 또는 누락, 콘텐츠 또는 샘플 코드 사용으로 인해 발생 하는 모든 종류의 손실 또는 손상에 대 한 사용자에 게 책임을 지지 않습니다. 이에 대 한 통지를 받고, 면책에 동의 하 고,이를 비롯 한 모든 손실, 손실을 초래 하거나,이를 비롯 한 모든 종류의 손해에 대 한 손해, 부상 또는 손해에 대 한 동의를 제공 합니다 .이는 여기에 표시 되 고 포함 된 보기를 포함 하지만이에 제한 되지 않습니다.

> [!div class="step-by-step"]
> [이전](shopping-cart.md)
> [다음](membership-and-administration.md)
