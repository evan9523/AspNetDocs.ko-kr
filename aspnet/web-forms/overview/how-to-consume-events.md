---
title: '방법: Web Forms 애플리케이션에서 이벤트 사용'
description: ASP.NET Web Forms apps에서 단추 클릭 이벤트를 처리 하는 방법을 알아봅니다.
author: rick-anderson
ms.author: riande
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- events [ASP.NET], Web Forms
- Web Forms controls, and events
- event handlers [ASP.NET], Web Forms
- events [ASP.NET], consuming
- Web Forms, event handling
ms.assetid: 73bf8638-c4ec-4069-b0bb-a1dc79b92e32
ms.openlocfilehash: 2e1807fed7d03db5893e1767a7a3a0de81862e7f
ms.sourcegitcommit: db13f9477981daabd57b99a410ec34e31e8d6aae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94674805"
---
# <a name="how-to-consume-events-in-a-web-forms-app"></a>방법: Web Forms 앱에서 이벤트 사용

ASP.NET Web Forms 애플리케이션의 주된 활용 방식은 웹 페이지에 컨트롤을 채운 다음 사용자가 클릭하는 컨트롤에 따라 특정 작업을 수행하는 것입니다. 예를 들어, <xref:System.Web.UI.WebControls.Button?displayProperty=nameWithType> 컨트롤은 사용자가 웹 페이지에서 해당 컨트롤을 클릭하면 이벤트를 발생시킵니다. 이벤트를 처리하면 애플리케이션이 해당 단추 클릭에 대해 적절한 애플리케이션 논리를 수행할 수 있습니다.  
  
## <a name="handle-a-button-click-event-on-a-webpage"></a>웹 페이지에서 단추 클릭 이벤트 처리  
  
1. 다음 단계에서 정의할 메서드의 이름으로 설정된 <xref:System.Web.UI.WebControls.Button> 값을 가진 `OnClick` 컨트롤이 있는 ASP.NET Web Forms 페이지(웹 페이지)를 만듭니다.  
  
    ```xml  
    <asp:Button ID="Button1" runat="server" Text="Click Me" OnClick="Button1_Click" />  
    ```  
  
2. <xref:System.Web.UI.WebControls.Button.Click> 이벤트 대리자 시그니처와 일치하고 `OnClick` 값에 대해 정의한 이름을 갖는 이벤트 처리기를 정의합니다.  
  
    ```csharp  
    protected void Button1_Click(object sender, EventArgs e)  
    {  
        // perform action  
    }  
    ```  
  
    ```vb  
    Protected Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' perform action  
    End Sub  
    ```  
  
     <xref:System.Web.UI.WebControls.Button.Click> 이벤트는 대리자 형식에 <xref:System.EventHandler> 클래스를 사용하고 이벤트 데이터에 <xref:System.EventArgs> 클래스를 사용합니다. ASP.NET 페이지 프레임워크에서는 <xref:System.EventHandler>의 인스턴스를 만드는 코드를 자동으로 생성하고 이 대리자 인스턴스를 <xref:System.Web.UI.WebControls.Button.Click> 인스턴스의 <xref:System.Web.UI.WebControls.Button> 이벤트에 추가합니다.  
  
3. 2단계에서 정의한 이벤트 처리기 메서드에서 코드를 추가하여 이벤트가 발생할 때 필요한 모든 작업을 수행합니다.  
  
## <a name="see-also"></a>참조

- [삽입, 업데이트 및 삭제와 연결 된 이벤트를 검사 합니다.](data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
- [.NET의 이벤트](/dotnet/standard/index.md)
