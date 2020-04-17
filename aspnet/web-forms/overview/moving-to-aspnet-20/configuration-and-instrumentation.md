---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: 구성 및 계측 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 2.0의 구성 및 계측에는 큰 변화가 있습니다. 새로운 ASP.NET 구성 API를 사용하면 구성을 변경할 수 있습니다.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: 30ea2ffd3d055c5373a33615bc19a8f68fb568ab
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543056"
---
# <a name="configuration-and-instrumentation"></a>구성 및 계측

[로 마이크로 소프트](https://github.com/microsoft)

> ASP.NET 2.0의 구성 및 계측에는 큰 변화가 있습니다. 새로운 ASP.NET 구성 API를 사용하면 프로그래밍 방식으로 구성을 변경할 수 있습니다. 또한 많은 새로운 구성 설정이 존재하여 새로운 구성및 계측이 가능합니다.

ASP.NET 2.0의 구성 및 계측에는 큰 변화가 있습니다. 새로운 ASP.NET 구성 API를 사용하면 프로그래밍 방식으로 구성을 변경할 수 있습니다. 또한 많은 새로운 구성 설정이 존재하여 새로운 구성및 계측이 가능합니다.

이 단원에서는 구성 파일을 읽고 쓰는 것과 관련하여 구성 API를 ASP.NET ASP.NET 구성 파일에 대해서도 설명하며 ASP.NET 계측에 대해서도 다룹니다. 또한 ASP.NET 추적에서 사용할 수 있는 새로운 기능도 다룹니다.

## <a name="aspnet-configuration-api"></a>ASP.NET 구성 API

ASP.NET 구성 API를 사용하면 단일 프로그래밍 인터페이스를 사용하여 응용 프로그램 구성 데이터를 개발, 배포 및 관리할 수 있습니다. 구성 API를 사용하여 구성 파일에서 XML을 직접 편집하지 않고도 전체 ASP.NET 구성을 프로그래밍 방식으로 개발하고 수정할 수 있습니다. 또한 개발하는 콘솔 응용 프로그램 및 스크립트, 웹 기반 관리 도구 및 MMC(Microsoft 관리 콘솔) 스냅인에서 구성 API를 사용할 수 있습니다.

다음 두 구성 관리 도구는 구성 API를 사용하며 .NET Framework 버전 2.0에 포함됩니다.

- ASP.NET MMC 스냅인은 구성 API를 사용하여 관리 작업을 단순화하여 구성 계층구조의 모든 수준에서 로컬 구성 데이터의 통합보기를 제공합니다.
- 호스팅된 사이트를 포함하여 로컬 및 원격 응용 프로그램의 구성 설정을 관리할 수 있는 웹 사이트 관리 도구입니다.

ASP.NET 구성 API는 프로그래밍 방식으로 웹 사이트 및 응용 프로그램을 구성하는 데 사용할 수 있는 ASP.NET 관리 개체 집합으로 구성됩니다. 관리 개체는 .NET Framework 클래스 라이브러리로 구현됩니다. 구성 API 프로그래밍 모델은 컴파일 타임에 데이터 형식을 적용하여 코드 일관성과 안정성을 보장하는 데 도움이 됩니다. 응용 프로그램 구성을 보다 쉽게 관리할 수 있도록 구성 API를 사용하면 데이터를 다른 구성 파일에서 별도의 컬렉션으로 보는 대신 구성 계층 구조의 모든 지점에서 병합된 데이터를 단일 컬렉션으로 볼 수 있습니다. 또한 구성 API를 사용하면 구성 파일에서 XML을 직접 편집하지 않고도 전체 응용 프로그램 구성을 조작할 수 있습니다. 마지막으로 API는 웹 사이트 관리 도구와 같은 관리 도구를 지원하여 구성 작업을 단순화합니다. 구성 API는 컴퓨터에서 구성 파일 생성을 지원하고 여러 컴퓨터에서 구성 스크립트를 실행하여 배포를 단순화합니다.

> [!NOTE]
> 구성 API는 IIS 응용 프로그램 만들기를 지원하지 않습니다.

## <a name="working-with-local-and-remote-configuration-settings"></a>로컬 및 원격 구성 설정 작업

구성 개체는 컴퓨터와 같은 특정 물리적 엔터티 또는 응용 프로그램이나 웹 사이트와 같은 논리적 엔터티에 적용되는 구성 설정의 병합된 보기를 나타냅니다. 지정된 논리 엔터티는 로컬 컴퓨터 또는 원격 서버에 존재할 수 있습니다. 지정된 엔터티에 대한 구성 파일이 없는 경우 Configuration 개체는 Machine.config 파일에 정의된 기본 구성 설정을 나타냅니다.

다음 클래스에서 열린 구성 메서드 중 하나를 사용하여 Configuration 개체를 얻을 수 있습니다.

1. 엔터티가 클라이언트 응용 프로그램인 경우 ConfigurationManager 클래스입니다.
2. 엔터티가 웹 응용 프로그램인 경우 WebConfigurationManager 클래스입니다.

이러한 메서드는 Configuration 개체를 반환하며, 이 개체는 기본 구성 파일을 처리하는 데 필요한 메서드와 속성을 제공합니다. 당신은 읽거나 쓰기 위해 이러한 파일에 액세스 할 수 있습니다.

### <a name="reading"></a>읽기

GetSection 또는 GetSectionGroup 메서드를 사용하여 구성 정보를 읽습니다. 읽는 사용자 또는 프로세스에는 계층 구조의 모든 구성 파일에 대한 Read 권한이 있어야 합니다.

> [!NOTE]
> 경로 매개 변수를 사용하는 정적 GetSection 메서드를 사용하는 경우 경로 매개 변수는 코드가 실행 중인 응용 프로그램을 참조해야 합니다. 그렇지 않으면 매개 변수가 무시되고 현재 실행 중인 응용 프로그램의 구성 정보가 반환됩니다.

### <a name="writing"></a>쓰기

저장 방법 중 하나를 사용하여 구성 정보를 작성합니다. 작성하는 사용자 또는 프로세스에는 현재 구성 계층 수준에서 구성 파일 및 디렉터리에 대한 쓰기 권한과 계층 구조의 모든 구성 파일에 대한 읽기 사용 권한이 있어야 합니다.

지정된 엔터티에 대한 상속된 구성 설정을 나타내는 구성 파일을 생성하려면 다음 구성 메서드 중 하나를 사용합니다.

1. 저장 메서드를 사용하여 새 구성 파일을 만듭니다.
2. SaveAs 메서드는 다른 위치에서 새 구성 파일을 생성합니다.

## <a name="configuration-classes-and-namespaces"></a>구성 클래스 및 네임스페이스

많은 구성 클래스와 메서드는 서로 비슷합니다. 다음 표는 가장 일반적으로 사용되는 구성 클래스 및 네임스페이스에 대해 설명합니다.

| **구성 클래스 또는 네임스페이스** | **설명** |
| --- | --- |
| [시스템.구성](https://msdn.microsoft.com/library/system.configuration.aspx) 네임스페이스 | 모든 .NET Framework 응용 프로그램에 대한 기본 구성 클래스가 포함되어 있습니다. 섹션 처리기 클래스는 GetSection 및 GetSectionGroup과 같은 메서드에서 섹션에 대한 구성 데이터를 가져오는 데 사용됩니다. 이 두 메서드는 비정적입니다. |
| 시스템.구성.구성 클래스 | 컴퓨터, 응용 프로그램, 웹 디렉터리 또는 기타 리소스에 대한 구성 데이터 집합을 나타냅니다. 이 클래스에는 구성 설정을 업데이트하고 섹션 및 단면 그룹에 대한 참조를 얻기 위한 GetSection 및 GetSectionGroup과 같은 유용한 메서드가 포함되어 있습니다. 이 클래스는 WebConfigurationManager 및 ConfigurationManager 클래스의 메서드와 같은 디자인 시간 구성 데이터를 가져오는 메서드에 대 한 반환 형식으로 사용 됩니다. |
| System.Web.Configuration 네임스페이스 | [ASP.NET 구성 설정에서](https://msdn.microsoft.com/library/b5ysx397.aspx)정의된 ASP.NET 구성 섹션에 대한 섹션 처리기 클래스가 포함됩니다. 섹션 처리기 클래스는 GetSection 및 GetSectionGroup과 같은 메서드에서 섹션에 대한 구성 데이터를 가져오는 데 사용됩니다. |
| System.Web.Configuration.Web.WebConfigurationManager 클래스 | 런타임 및 디자인 타임 구성 설정에 대한 참조를 얻는 데 유용한 방법을 제공합니다. 이러한 메서드는 System.Configuration.Configuration 클래스를 반환 유형으로 사용합니다. 이 클래스의 정적 GetSection 메서드 또는 System.Configuration.ConfigurationManager 클래스의 비정적 GetSection 메서드를 상호 교환할 수 있습니다. 웹 응용 프로그램 구성의 경우 System.Configuration.Configuration.ConfigurationManager 클래스 대신 System.Web.Configuration.WebConfigurationManager 클래스를 권장합니다. |
| [시스템.구성.공급자](https://msdn.microsoft.com/library/system.configuration.provider.aspx) 네임스페이스 | 구성 공급자를 사용자 지정하고 확장하는 방법을 제공합니다. 구성 시스템의 모든 공급자 클래스에 대한 기본 클래스입니다. |
| [시스템.웹.관리](https://msdn.microsoft.com/library/system.web.management.aspx) 네임스페이스 | 웹 응용 프로그램의 상태를 관리하고 모니터링하기 위한 클래스와 인터페이스가 포함되어 있습니다. 엄밀히 말하면 이 네임스페이스는 구성 API의 일부로 간주되지 않습니다. 예를 들어 추적 및 이벤트 발생은 이 네임스페이스의 클래스에 의해 수행됩니다. |
| [시스템.관리.계측](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) 네임스페이스 | WMI(Windows 관리 계측)를 통해 관리 정보 및 이벤트를 잠재 소비자에게 노출하는 데 응용 프로그램의 계측에 필요한 클래스를 제공합니다. ASP.NET 상태 모니터링은 WMI를 사용하여 이벤트를 전달합니다. 엄밀히 말하면 이 네임스페이스는 구성 API의 일부로 간주되지 않습니다. |

## <a name="reading-from-aspnet-configuration-files"></a>ASP.NET 구성 파일에서 읽기

WebConfigurationManager 클래스는 ASP.NET 구성 파일에서 읽기 위한 핵심 클래스입니다. 기본적으로 구성 파일을 읽는 ASP.NET 세 단계가 있습니다.

1. OpenWebConfiguration 메서드를 사용하여 구성 개체를 가져옵니다.
2. 구성 파일에서 원하는 섹션에 대한 참조를 가져옵니다.
3. 구성 파일에서 원하는 정보를 읽습니다.

나타내는 구성 개체는 특정 구성 파일을 나타내지 않습니다. 대신 컴퓨터, 응용 프로그램 또는 웹 사이트의 구성에 대한 병합된 보기를 나타냅니다. 다음 코드 샘플은 *ProductInfo*라는 웹 응용 프로그램의 구성을 나타내는 Configuration 개체를 인스턴스화 합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> /ProductInfo 경로가 없는 경우 위의 코드는 machine.config 파일에 지정된 대로 기본 구성을 반환합니다.

구성 개체가 있으면 GetSection 또는 GetSectionGroup 메서드를 사용하여 구성 설정을 드릴다운할 수 있습니다. 다음 예제는 위의 ProductInfo 응용 프로그램에 대 한 가장 설정에 대 한 참조를 가져옵니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>ASP.NET 구성 파일에 쓰기

구성 파일에서 읽는 것과 마찬가지로 WebConfigurationManager 클래스는 구성 파일에 Asp.NET 작성하기 위한 핵심입니다. 구성 파일에 ASP.NET 작성하는 세 단계도 있습니다.

1. OpenWebConfiguration 메서드를 사용하여 구성 개체를 가져옵니다.
2. 구성 파일에서 원하는 섹션에 대한 참조를 가져옵니다.
3. 저장 또는 SaveAs 메서드를 사용하여 구성 파일에서 원하는 정보를 작성합니다.

다음 코드는 컴파일&gt; 요소의 &lt; **디버그** 특성을 false로 변경합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

이 코드가 실행되면 &lt;컴파일&gt; 요소의 **디버그** 특성이 *webApp* 응용 프로그램의 web.config 파일에 대해 false로 설정됩니다.

## <a name="systemwebmanagement-namespace"></a>시스템.웹.관리 네임스페이스

System.Web.Management 네임스페이스는 ASP.NET 응용 프로그램의 상태를 관리하고 모니터링하기 위한 클래스와 인터페이스를 제공합니다.

로깅은 이벤트를 공급자와 연결하는 규칙을 정의하여 수행됩니다. 이 규칙은 공급자에게 전송되는 이벤트 유형을 정의합니다. 로그할 수 있는 다음 기본 이벤트를 사용할 수 있습니다.

| **웹베이스 이벤트** | 모든 이벤트의 기본 이벤트 클래스입니다. 이벤트 코드, 이벤트 세부 정보 코드, 이벤트가 발생한 날짜 및 시간, 시퀀스 번호, 이벤트 메시지 및 이벤트 세부 정보와 같은 모든 이벤트에 필요한 속성을 포함합니다. |
| --- | --- |
| **웹 매니지먼트 이벤트** | 응용 프로그램 수명, 요청, 오류 및 감사 이벤트와 같은 관리 이벤트에 대한 기본 이벤트 클래스입니다. |
| **웹하트비트이벤트** | 응용 프로그램에서 정기적으로 생성되는 이벤트는 유용한 런타임 상태 정보를 캡처합니다. |
| **웹 감사 이벤트** | 권한 부여 실패, 암호 해독 실패 *등과* 같은 조건을 표시하는 데 사용되는 보안 감사 이벤트의 기본 클래스입니다. |
| **웹 요청 이벤트** | 모든 정보 요청 이벤트의 기본 클래스입니다. |
| **웹베이스오류이벤트** | 오류 조건을 나타내는 모든 이벤트의 기본 클래스입니다. |

사용 가능한 공급자 유형을 사용하면 이벤트 뷰어, SQL Server, WMI(Windows 관리 계측) 및 전자 메일에 이벤트 출력을 보낼 수 있습니다. 미리 구성된 공급자 및 이벤트 매핑은 이벤트 출력을 기록하는 데 필요한 작업량을 줄입니다.

ASP.NET 2.0은 즉시 이벤트 로그 공급자를 사용하여 응용 프로그램 도메인시작 및 중지를 기반으로 이벤트를 기록하고 처리되지 않은 예외를 기록합니다. 이렇게 하면 몇 가지 기본 시나리오를 다룰 수 있습니다. 예를 들어 응용 프로그램에서 예외를 throw하지만 사용자가 오류를 저장하지 않고 재현할 수 없다고 가정해 보겠습니다. 기본 이벤트 로그 규칙을 사용하면 예외 및 스택 정보를 수집하여 어떤 종류의 오류가 발생했는지 더 잘 알 수 있습니다. 또 다른 예는 응용 프로그램이 세션 상태를 잃고 있는 경우에 적용됩니다. 이 경우 이벤트 로그를 통해 응용 프로그램 도메인이 재활용되고 있는지 여부와 응용 프로그램 도메인이 처음에 중지된 이유를 확인할 수 있습니다.

또한 상태 모니터링 시스템은 확장 가능합니다. 예를 들어 사용자 지정 웹 이벤트를 정의하고 응용 프로그램 내에서 이벤트를 발생한 다음 전자 메일과 같은 공급자에게 이벤트 정보를 보내는 규칙을 정의할 수 있습니다. 이를 통해 계측기를 건강 모니터링 제공업체에 쉽게 연결할 수 있습니다. 또 다른 예로, 주문이 처리될 때마다 이벤트를 발생시키고 각 이벤트를 SQL Server 데이터베이스로 보내는 규칙을 설정할 수 있습니다. 사용자가 연속으로 여러 번 로그온하지 않을 때 이벤트를 발생시키고 전자 메일 기반 공급자를 사용하도록 이벤트를 설정할 수도 있습니다.

기본 공급자 및 이벤트에 대한 구성은 전역 Web.config 파일에 저장됩니다. 전역 Web.config 파일은 Machine.config 파일에 저장된 모든 웹 기반 설정을 ASP.NET 1x로 저장합니다. 전역 Web.config 파일은 다음 디렉터리에 있습니다.

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

전역 &lt;Web.config 파일의 상태 모니터링&gt; 섹션에서는 기본 구성 설정을 제공합니다. 응용 프로그램에 대한 Web.config 파일의 &lt;healthMonitoring&gt; 섹션을 구현하여 이러한 설정을 재정의하거나 사용자 고유의 설정을 구성할 수 있습니다.

전역 &lt;Web.config 파일의 상태 모니터링&gt; 섹션에는 다음 항목이 포함되어 있습니다.

| **공급자** | 이벤트 뷰어, WMI 및 SQL Server에 대해 설정된 공급자를 포함합니다. |
| --- | --- |
| **이벤트 매핑** | 다양한 WebBase 클래스에 대한 매핑이 포함되어 있습니다. 고유한 이벤트 클래스를 생성하는 경우 이 목록을 확장할 수 있습니다. 고유한 이벤트 클래스를 생성하면 정보를 보내는 공급자보다 세밀하게 세분화됩니다. 예를 들어 SQL Server로 전송되는 처리되지 않은 예외를 전자 메일로 보내는 동안 구성할 수 있습니다. |
| **규칙** | 이벤트매핑을 공급자에 연결합니다. |
| **버퍼링** | SQL Server 및 전자 메일 공급자와 함께 이벤트를 공급자에게 플러시하는 빈도를 결정하는 데 사용됩니다. |

다음은 전역 Web.config 파일의 코드 예제입니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>이벤트 뷰어에 이벤트를 저장하는 방법

앞에서 설명한 것처럼 이벤트 뷰어에서 이벤트를 로깅하는 공급자는 전역 Web.config 파일에서 구성됩니다. 기본적으로 **WebBaseErrorEvent** 및 **WebFailureAuditEvent를** 기반으로 하는 모든 이벤트가 기록됩니다. 추가 규칙을 추가하여 이벤트 로그에 추가 정보를 기록할 수 있습니다. 예를 들어 모든*이벤트(예:* **WebBaseEvent를**기반으로 하는 모든 이벤트)를 기록하려는 경우 Web.config 파일에 다음 규칙을 추가할 수 있습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

이 규칙은 **모든 이벤트** 이벤트 맵을 이벤트 로그 공급자에 연결합니다. eventMapping 및 공급자는 모두 전역 Web.config 파일에 포함됩니다.

## <a name="how-to-store-events-to-sql-server"></a>SQL Server에 이벤트를 저장하는 방법

이 메서드는 Aspnet\_regsql.exe 도구에 의해 생성 되는 **ASPNETDB** 데이터베이스를 사용 합니다. 기본 공급자는 App\_데이터 폴더의 파일 기반 데이터베이스 또는 SQL Server의 로컬 SQLExpress 인스턴스를 사용하는 LocalSqlServer 연결 문자열을 사용합니다. LocalSqlServer 연결 문자열과 SqlProvider는 모두 전역 Web.config 파일에 구성됩니다.

전역 Web.config 파일의 LocalSqlServer 연결 문자열은 다음과 같습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

다른 SQL Server 인스턴스를 사용하려면 %windir%\Microsoft.Net\Framework\v2.0에서 찾을 수 있는 Aspnet\_regsql.exe 도구를 사용해야 합니다. \* 폴더에 저장합니다. Aspnet\_regsql.exe 도구를 사용하여 SQL Server 인스턴스에서 사용자 지정 **ASPNETDB** 데이터베이스를 생성한 다음 응용 프로그램 구성 파일에 연결 문자열을 추가한 다음 새 연결 문자열을 사용하여 공급자를 추가합니다. **ASPNETDB** 데이터베이스를 만든 후에는 eventMapping을 sqlProvider에 연결하는 규칙을 설정해야 합니다.

기본 SqlProvider를 사용하든 자체 공급자를 구성하든 공급자를 이벤트 맵과 연결하는 규칙을 추가해야 합니다. 다음 규칙은 위에서 만든 새 공급자를 **모든 이벤트** 이벤트 맵에 연결합니다. 이 규칙은 **WebBaseEvent를** 기반으로 하는 모든 이벤트를 기록하고 MYASPNETDB 연결 문자열을 사용하는 MySqlWebEventProvider로 보냅니다. 다음 코드는 공급자를 이벤트 맵과 연결하는 규칙을 추가합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

SQL Server에만 오류를 보내려면 다음 규칙을 추가할 수 있습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>WMI로 이벤트를 전달하는 방법

이벤트를 WMI로 전달할 수도 있습니다. WMI 공급자는 기본적으로 전역 Web.config 파일에서 구성됩니다.

다음 코드 예제는 WMI에 이벤트를 전달하는 규칙을 추가합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

이벤트를 연결하는 규칙을 추가해야 합니다.예 공급자에 매핑 및 이벤트를 수신하는 WMI 수신기 응용 프로그램도 추가해야 합니다. 다음 코드 예제는 WMI 공급자를 모든 **이벤트** 이벤트 맵에 연결하는 규칙을 추가합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>이벤트를 이메일로 전달하는 방법

이벤트를 이메일로 전달할 수도 있습니다. SQL Server 또는 이벤트 로그에 더 적합한 많은 정보를 실수로 자신에게 보낼 수 있으므로 전자 메일 공급자에 매핑하는 이벤트 규칙에 주의해야 합니다. 두 개의 이메일 공급자가 있습니다. SimpleMailWebEvent공급자 및 템플릿메일웹이벤트제공자. 각각은 "템플릿" 및 "detailedTemplateErrors" 특성을 제외하고 동일한 구성 특성을 가지며, 둘 다 TemplatedMailWebEventProvider에서만 사용할 수 있습니다.

> [!NOTE]
> 이러한 이메일 공급자는 모두 구성되지 않습니다. Web.config 파일에 추가해야 합니다.

이 두 이메일 공급자 사이의 주요 차이점은 SimpleMailWebEventProvider 수정할 수 없는 일반 템플릿에서 전자 메일을 보냅니다. sample Web.config 파일은 다음 규칙을 사용하여 구성된 공급자 목록에 이 전자 메일 공급자를 추가합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

이메일 공급자를 **모든 이벤트** 이벤트 맵에 연결하기 위해 다음 규칙도 추가됩니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 추적

ASP.NET 2.0에서 추적에 세 가지 주요 개선 사항이 있습니다.

1. 통합 추적 기능
2. 추적 메시지에 대한 프로그래밍 방식 액세스
3. 향상된 애플리케이션 수준 추적

## <a name="integrated-tracing-functionality"></a>통합 추적 기능

이제 System.Diagnostics.Trace 클래스에서 내보낸 메시지를 추적 ASP.NET 및 ASP.NET 추적에서 내보낸 메시지를 System.Diagnostics.Trace로 라우팅할 수 있습니다. 계측 이벤트를 system.Diagnostics.Trace로 ASP.NET 전달할 수도 있습니다. 이 기능은 추적&gt; 요소의 새 **writeToDiagnosticsTrace** 특성에 &lt;의해 제공됩니다. 이 부울 값이 true이면 추적 메시지를 표시하기 위해 등록된 모든 리스너가 사용할 ASP.NET 추적 메시지가 System.Diagnostics 추적 인프라로 전달됩니다.

## <a name="programmatic-access-to-trace-messages"></a>추적 메시지에 대한 프로그래밍 방식 액세스

ASP.NET 2.0은 **TraceContextRecord** 클래스 및 TraceRecords 컬렉션을 통해 모든 추적 메시지에 프로그래밍 방식으로 액세스할 수 **있습니다.** 추적 메시지에 액세스하는 가장 효율적인 방법은 **TraceContextEventHandler** 대리자(ASP.NET 2.0의 새로운)를 등록하여 새 **TraceFinished** 이벤트를 처리하는 것입니다. 그런 다음 원하는 대로 추적 메시지를 반복할 수 있습니다.

다음 코드 샘플은 다음을 보여 줍니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

위의 예제에서는 TraceRecords 컬렉션을 반복한 다음 각 메시지를 응답 스트림에 씁니다.

## <a name="improved-application-level-tracing"></a>향상된 애플리케이션 수준 추적

응용 프로그램 수준 추적은&gt; 추적 요소의 **mostRecent** 최신 특성의 &lt;최신 도입을 통해 향상됩니다. 이 특성은 가장 최근의 응용 프로그램 수준 추적 출력이 표시되고 requestLimit에 의해 표시된 제한을 초과하는 이전 추적 데이터가 삭제되는지 여부를 지정합니다. false이면 requestLimit 특성에 도달할 때까지 요청에 대한 추적 데이터가 표시됩니다.

## <a name="aspnet-command-line-tools"></a>ASP.NET 명령줄 도구

ASP.NET 구성에 도움이 되는 몇 가지 명령줄 도구가 있습니다. ASP.NET 개발자는 aspnet\_regiis.exe 도구에 익숙해야 합니다. ASP.NET 2.0은 구성에 도움이 될 세 가지 다른 명령줄 도구를 제공합니다.

다음 명령줄 도구를 사용할 수 있습니다.

| **도구** | **사용** |
| --- | --- |
| **아스프넷\_레지스.exe** | IIS에 ASP.NET 등록할 수 있습니다. 이 도구에는 ASP.NET 2.0과 함께 제공되는 두 가지 버전이 있으며, 하나는 32비트 시스템(프레임워크 폴더)용이고 하나는 64비트 시스템용(Framework64 폴더)입니다. 64비트 버전은 32비트 OS에 설치되지 않습니다. |
| **아스프넷\_regsql.exe** | ASP.NET SQL Server 등록 도구는 ASP.NET SQL Server 공급자가 사용할 Microsoft SQL Server 데이터베이스를 만들거나 기존 데이터베이스에서 옵션을 추가하거나 제거하는 데 사용됩니다. Aspnet\_regsql.exe 파일은 [드라이브:]\WINDOWS\Microsoft.NET\Framework\version\버전웹 서버의 폴더에 있습니다. |
| **아스프넷\_regbrowsers.exe** | ASP.NET 브라우저 등록 도구는 모든 시스템 전체 브라우저 정의를 구문 분석 및 컴파일하여 어셈블리에 설치하고 어셈블리를 전역 어셈블리 캐시에 설치합니다. 이 도구는 브라우저 정의 파일을 사용합니다( 브라우저 파일)에서 .NET 프레임 워크 브라우저 하위 디렉토리. 이 도구는 %SystemRoot%\Microsoft.NET\Framework\버전\ 디렉토리에서 찾을 수 있습니다. |
| **aspnet\_컴파일러.exe** | ASP.NET 컴파일 도구를 사용하면 프로덕션 서버와 같은 대상 위치에 배포할 때 ASP.NET 웹 응용 프로그램을 컴파일할 수 있습니다. 내부 컴파일은 최종 사용자가 응용 프로그램을 컴파일하는 동안 응용 프로그램에 대한 첫 번째 요청에 지연이 발생하지 않기 때문에 응용 프로그램 성능에 도움이 됩니다. |

aspnet\_regiis.exe 도구는 ASP.NET 2.0에 새로운 것이 아니기 때문에 여기에서 논의하지 않습니다.

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET SQL 서버 등록 도구\_- aspnet regsql.exe

ASP.NET SQL Server 등록 도구를 사용하여 여러 유형의 옵션을 설정할 수 있습니다. SQL 연결을 지정하고, SQL Server를 사용하여 정보를 관리하는 ASP.NET 응용 프로그램 서비스를 지정하고, SQL 캐시 종속성에 사용되는 데이터베이스 또는 테이블을 나타내고, SQL Server를 사용하여 프로시저 및 세션 상태를 저장하는 지원을 추가하거나 제거할 수 있습니다.

여러 ASP.NET 응용 프로그램 서비스는 공급자를 사용하여 데이터 원본에서 데이터를 저장하고 검색하는 것을 관리합니다. 각 공급자는 데이터 원본에 따라 다릅니다. ASP.NET 다음과 같은 ASP.NET 기능에 대한 SQL Server 공급자가 포함되어 있습니다.

- 멤버 [자격(SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) 클래스).
- 역할 [관리(SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) 클래스).
- [프로필(SqlProfileProvider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx) 클래스).
- 웹 파트 개인 [정보화(SqlPersonalizationProvider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx) 클래스).
- 웹 [이벤트(SqlWebEventProvider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx) 클래스).

ASP.NET 설치할 때 서버의 Machine.config 파일에는 공급자를 의존하는 각 ASP.NET 기능에 대해 SQL Server 공급자를 지정하는 구성 요소가 포함됩니다. 이러한 공급자는 기본적으로 SQL Server Express 2005의 로컬 사용자 인스턴스에 연결하도록 구성됩니다. 공급자가 사용하는 기본 연결 문자열을 변경한 다음 컴퓨터 구성에서 구성된 ASP.NET 기능을 사용하려면 먼저 Aspnet\_regsql.exe를 사용하여 선택한 기능에 대해 SQL Server 데이터베이스 와 데이터베이스 요소를 설치해야 합니다. SQL 등록 도구를 사용하여 지정한 데이터베이스가 아직 존재하지 않는 경우(명령줄에 지정되지 않은 경우 aspnetdb가 기본 데이터베이스가 됨) 현재 사용자는 SQL Server에서 데이터베이스를 만들고 데이터베이스 내에서 스키마 요소를 만들 수 있는 권한이 있어야 합니다.

### <a name="sql-cache-dependency"></a>SQL 캐시 종속성

ASP.NET 출력 캐싱의 고급 기능은 SQL 캐시 종속성입니다. SQL 캐시 종속성은 테이블 폴링의 ASP.NET 구현을 사용하는 작업 모드와 SQL Server 2005의 쿼리 알림 기능을 사용하는 두 번째 모드의 두 가지 작업 모드를 지원합니다. SQL 등록 도구를 사용하여 테이블 폴링 작업 모드를 구성할 수 있습니다.

### <a name="session-state"></a>세션 상태

기본적으로 세션 상태 값과 정보는 ASP.NET 프로세스 내의 메모리에 저장됩니다. 또는 여러 웹 서버에서 공유할 수 있는 SQL Server 데이터베이스에 세션 데이터를 저장할 수 있습니다. SQL 등록 도구를 사용하여 세션 상태에 대해 지정한 데이터베이스가 아직 존재하지 않는 경우 현재 사용자는 SQL Server에서 데이터베이스를 만들고 데이터베이스 내에서 스키마 요소를 만들 수 있는 권한이 있어야 합니다. 데이터베이스가 있는 경우 현재 사용자는 기존 데이터베이스에 스키마 요소를 만들 수 있는 권한이 있어야 합니다.

SQL Server에 세션 상태 데이터베이스를 설치하려면 Aspnet\_regsql.exe 도구를 실행하고 다음 정보를 명령과 함께 제공하십시오.

- **-S** 옵션을 사용하는 SQL Server 인스턴스의 이름입니다.
- SQL Server를 실행하는 컴퓨터에서 데이터베이스를 만들 수 있는 권한이 있는 계정에 대한 로그온 자격 증명입니다. **-E** 옵션을 사용하여 현재 로그온한 사용자를 사용하거나 **-U** 옵션을 사용하여 **-P** 옵션과 함께 사용자 ID를 지정하여 암호를 지정합니다.
- **-ssadd** 명령줄 옵션을 사용하여 세션 상태 데이터베이스를 추가합니다.

기본적으로 Aspnet\_regsql.exe 도구를 사용하여 SQL Server 2005 익스프레스 에디션을 실행하는 컴퓨터에 세션 상태 데이터베이스를 설치할 수 없습니다.

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>ASP.NET 브라우저 등록 도구 -\_aspnet regbrowsers.exe

ASP.NET 버전 1.1에서 Machine.config 파일에는 &lt;browserCaps&gt;. 이 섹션에는 정규식을 기반으로 다양한 브라우저의 구성을 정의하는 일련의 XML 항목이 포함되어 있습니다. ASP.NET 버전 2.0의 경우 새 . BROWSER 파일은 XML 항목을 사용하여 특정 브라우저의 매개 변수를 정의합니다. 새 을 추가하여 새 브라우저에 정보를 추가합니다. 브라우저 파일은 %SystemRoot%\Microsoft.NET Framework\버전\CONFIG\브라우저에 있는 폴더에 있습니다.

응용 프로그램이 브라우저 정보가 필요한 때마다 .config 파일을 읽지 않으므로 새 을 만들 수 있습니다. 브라우저 파일을 실행하고 Aspnet\_regbrowsers.exe를 실행하여 어셈블리에 필요한 변경 내용을 추가합니다. 이렇게 하면 서버가 새 브라우저 정보에 즉시 액세스할 수 있으므로 정보를 수집하기 위해 응용 프로그램을 종료할 필요가 없습니다. 응용 프로그램은 현재 HttpRequest의 브라우저 속성을 통해 브라우저 기능에 액세스할 수 있습니다.

aspnet\_regbrowser.exe를 실행할 때 다음 옵션을 사용할 수 있습니다.

| **옵션** | **설명** |
| --- | --- |
| **-?** | 명령 창에\_Aspnet regbbrowsers.exe 도움말 텍스트를 표시합니다. |
| **-i** | 런타임 브라우저 기능 어셈블리를 만들고 전역 어셈블리 캐시에 설치합니다. |
| **-u** | 전역 어셈블리 캐시에서 런타임 브라우저 기능 어셈블리를 제거합니다. |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>ASP.NET 컴파일 도구 - aspnet\_컴파일러.exe

ASP.NET 컴파일 도구는 두 가지 일반적인 방법으로 사용할 수 있습니다: 대상 출력 디렉토리를 지정 하는 배포에 대 한 장소 컴파일 및 컴파일.

### <a name="compiling-an-application-in-place"></a>[응용 프로그램 제자리에 컴파일](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET 컴파일 도구는 응용 프로그램을 컴파일할 수 있습니다. 미리 컴파일된 사이트의 사용자는 첫 번째 요청시 페이지를 컴파일하여 지연이 발생하지 않습니다.

사이트를 미리 컴파일할 때 다음 항목이 적용됩니다.

- 사이트는 파일 및 디렉터리 구조를 유지합니다.
- 서버의 사이트에서 사용하는 모든 프로그래밍 언어에 대한 컴파일러가 있어야 합니다.
- 파일컴파일에 실패하면 전체 사이트가 컴파일에 실패합니다.

새 원본 파일을 추가한 후 응용 프로그램을 다시 컴파일할 수도 있습니다. 이 도구는 **-c** 옵션을 포함하지 않는 한 새 파일이나 변경된 파일만 컴파일합니다.

> [!NOTE]
> 중첩된 응용 프로그램을 포함하는 응용 프로그램의 컴파일은 중첩된 응용 프로그램을 컴파일하지 않습니다. 중첩된 응용 프로그램은 별도로 컴파일해야 합니다.

### <a name="compiling-an-application-for-deployment"></a>[배포를 위한 응용 프로그램 컴파일](https://msdn.microsoft.com/library/ms229863.aspx)

targetDir 매개 변수를 지정하여 배포(대상 위치로 컴파일)를 위한 응용 프로그램을 컴파일합니다. targetDir은 웹 응용 프로그램의 최종 위치이거나 컴파일된 응용 프로그램을 추가로 배포할 수 있습니다. **-u** 옵션을 사용하면 컴파일된 응용 프로그램의 특정 파일을 다시 컴파일하지 않고 변경할 수 있는 방식으로 응용 프로그램을 컴파일합니다. Aspnet\_컴파일러.exe는 정적 파일 형식과 동적 파일 형식을 구분하고 결과 응용 프로그램을 만들 때 다르게 처리합니다.

- 정적 파일 형식은 .css, .gif, .htm, .html, .jpg, .js 등과 같은 확장명이 있는 파일과 같이 연결된 컴파일러 또는 빌드 공급자가 없는 파일입니다. 이러한 파일은 단순히 대상 위치로 복사되며 디렉터리 구조의 상대 적인 위치는 유지됩니다.
- 동적 파일 형식은 .asax, .ascx, .ashx, .aspx, .aspx, .browser, .master 등과 같은 ASP.NET 특정 파일 이름 확장자가 있는 파일을 포함하여 연결된 컴파일러 또는 빌드 공급자가 있는 파일입니다. ASP.NET 컴파일 도구는 이러한 파일에서 어셈블리를 생성합니다. **-u** 옵션을 생략하면 도구는 파일 이름 확장자가 있는 파일도 만듭니다. 원본 소스 파일을 어셈블리에 매핑하는 컴파일된 파일입니다. 응용 프로그램 원본의 디렉터리 구조를 보존하기 위해 도구는 대상 응용 프로그램의 해당 위치에 자리 표시자 파일을 생성합니다.

컴파일된 응용 프로그램의 내용을 수정할 수 있음을 나타내려면 **-u** 옵션을 사용해야 합니다. 그렇지 않으면 후속 수정이 무시되거나 런타임 오류가 발생합니다.

다음 표는 ASP.NET 컴파일 도구가 **-u** 옵션이 포함되어 있을 때 다양한 파일 형식을 처리하는 방법을 설명합니다.

| **파일 형식** | **컴파일러 작업** |
| --- | --- |
| .ascx, .aspx, .master | 이러한 파일은 코드 숨는 파일과 스크립트 runat="server" &lt;&gt; 요소에 동봉된 모든 코드를 모두 포함하는 태그 및 소스 코드로 분할됩니다. 소스 코드는 해시 알고리즘에서 파생된 이름으로 어셈블리로 컴파일되고 어셈블리는 Bin 디렉터리에 배치됩니다. ** &lt; ** 인라인 코드, 즉 대괄호 ** % ** 사이에 둘러싸인 코드는 태그에 포함되며 컴파일되지 않습니다. 원본 파일과 이름이 같은 새 파일이 만들어지면 마크업이 포함되고 해당 출력 디렉터리에 배치됩니다. |
| .ashx, .asmx | 이러한 파일은 컴파일되지 않으며 컴파일되지 않은 출력 디렉터리로 이동됩니다. 처리기 코드를 컴파일하려면 App\_Code 디렉터리에서 코드를 소스 코드 파일에 배치합니다. |
| .cs, .vb, .jsl, .cpp(이전에 나열된 파일 형식에 대한 코드 숨결 파일 은 포함되지 않음) | 이러한 파일은 컴파일되어 참조하는 어셈블리의 리소스로 포함됩니다. 원본 파일은 출력 디렉토리에 복사되지 않습니다. 코드 파일이 참조되지 않으면 컴파일되지 않습니다. |
| 사용자 지정 파일 형식 | 이러한 파일은 컴파일되지 않습니다. 이러한 파일은 해당 출력 디렉토리에 복사됩니다. |
| 앱\_코드 하위 디렉터리에서 소스 코드 파일 | 이러한 파일은 어셈블리로 컴파일되어 Bin 디렉터리에 배치됩니다. |
| 앱\_GlobalResources 하위 디렉터리에서 .resx 및 .resource 파일 | 이러한 파일은 어셈블리로 컴파일되어 Bin 디렉터리에 배치됩니다. 기본\_출력 디렉터리 아래에 앱 GlobalResources 하위 디렉터리가 만들어지지 않으며 소스 디렉터리에 있는 .resx 또는 .resources 파일은 출력 디렉터리로 복사되지 않습니다. |
| 앱\_LocalResources 하위 디렉터리에서 .resx 및 .resource 파일 | 이러한 파일은 컴파일되지 않으며 해당 출력 디렉토리에 복사됩니다. |
| 앱\_테마 하위 디렉토리의 .skin 파일 | .skin 파일과 정적 테마 파일은 컴파일되지 않으며 해당 출력 디렉토리에 복사됩니다. |
| .browser Web.config 정적 파일 형식 어셈블리는 이미 Bin 디렉토리에 있습니다. | 이러한 파일은 출력 디렉토리에 있는 것처럼 복사됩니다. |

다음 표는 ASP.NET 컴파일 도구가 **-u** 옵션을 생략할 때 다른 파일 형식을 처리하는 방법을 설명합니다.

| **파일 형식** | **컴파일러 작업** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | 이러한 파일은 코드 숨는 파일과 스크립트 runat="server" &lt;&gt; 요소에 동봉된 모든 코드를 모두 포함하는 태그 및 소스 코드로 분할됩니다. 소스 코드는 해싱 알고리즘에서 파생된 이름으로 어셈블리로 컴파일됩니다. 결과 어셈블리는 Bin 디렉터리에 배치됩니다. ** &lt; ** 인라인 코드, 즉 대괄호 ** % ** 사이에 둘러싸인 코드는 태그에 포함되며 컴파일되지 않습니다. 컴파일러는 원본 파일과 이름이 같은 태그를 포함하도록 새 파일을 만듭니다. 이러한 결과 파일은 Bin 디렉토리에 배치됩니다. 또한 컴파일러는 원본 파일과 이름이 같지만 확장자를 가진 파일을 만듭니다. 매핑 정보가 포함된 컴파일된 정보입니다. Tthe. 컴파일된 파일은 원본 파일의 원래 위치에 해당하는 출력 디렉토리에 배치됩니다. |
| .ascx | 이러한 파일은 태그 와 소스 코드로 분할됩니다. 소스 코드는 어셈블리로 컴파일되고 해시 알고리즘에서 파생된 이름으로 Bin 디렉터리에 배치됩니다. 태그 파일이 생성되지 않습니다. |
| .cs, .vb, .jsl, .cpp(이전에 나열된 파일 형식에 대한 코드 숨결 파일 은 포함되지 않음) | .ascx, .ashx 또는 .aspx 파일에서 생성된 어셈블리에서 참조되는 소스 코드는 어셈블리로 컴파일되어 Bin 디렉터리에 배치됩니다. 원본 파일이 복사되지 않습니다. |
| 사용자 지정 파일 형식 | 이러한 파일은 동적 파일처럼 컴파일됩니다. 이를 기반으로 하는 파일의 유형에 따라 컴파일러는 매핑 파일을 출력 디렉터리에 배치할 수 있습니다. |
| 앱\_코드 하위 디렉터리에 있는 파일 | 이 하위 디렉터리에서 소스 코드 파일은 어셈블리로 컴파일되어 Bin 디렉터리에 배치됩니다. |
| 앱\_글로벌 리소스 하위 디렉터리에 있는 파일 | 이러한 파일은 어셈블리로 컴파일되어 Bin 디렉터리에 배치됩니다. 앱\_GlobalResources 하위 디렉터리없음 주 출력 디렉토리 아래에 생성되지 않습니다. 구성 파일이 적용을 지정하는 경우To="All", .resx 및 .resources 파일이 출력 디렉토리에 복사됩니다. [빌드 공급자](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)에 의해 참조 되는 경우 복사 되지 않습니다. |
| 앱\_LocalResources 하위 디렉터리에서 .resx 및 .resource 파일 | 이러한 파일은 고유한 이름을 가진 어셈블리로 컴파일되어 Bin 디렉터리에 배치됩니다. .resx 또는 .resource 파일은 출력 디렉토리에 복사되지 않습니다. |
| 앱\_테마 하위 디렉토리의 .skin 파일 | 테마는 어셈블리로 컴파일되고 Bin 디렉토리에 배치됩니다. 스텁 파일은 .skin 파일을 위해 만들어지고 해당 출력 디렉토리에 배치됩니다. 정적 파일(예: .css)은 출력 디렉토리에 복사됩니다. |
| .browser Web.config 정적 파일 형식 어셈블리는 이미 Bin 디렉토리에 있습니다. | 이러한 파일은 출력 디렉토리에 있는 것처럼 복사됩니다. |

### <a name="fixed-assembly-names"></a>[고정 어셈블리 이름](https://msdn.microsoft.com/library/ms229863.aspx##)

MSI Windows Installer를 사용하여 웹 응용 프로그램을 배포하는 것과 같은 일부 시나리오에서는 일관된 파일 이름과 내용뿐만 아니라 업데이트에 대한 어셈블리 또는 구성 설정을 식별하기 위해 일관된 디렉터리 구조를 사용해야 합니다. 이러한 경우 **-fixednames** 옵션을 사용하여 ASP.NET 컴파일 도구가 여러 페이지가 어셈블리로 컴파일되는 위치를 사용하는 대신 각 소스 파일에 대한 어셈블리를 컴파일하도록 지정할 수 있습니다. 이로 인해 많은 수의 어셈블리가 발생할 수 있으므로 확장성에 관심이 있는 경우 이 옵션을 주의해서 사용해야 합니다.

### <a name="strong-name-compilation"></a>[강력한 이름 편집](https://msdn.microsoft.com/library/ms229863.aspx##)

**-aptca**, **-delaysign,** **-keycontainer** 및 **-keyfile** 옵션은 Aspnet\_compiler.exe를 사용하여 강력한 이름 도구 [(Sn.exe)를](https://msdn.microsoft.com/library/k5b5tt23.aspx) 별도로 사용하지 않고 강력한 명명 된 어셈블리를 만들 수 있도록 제공됩니다. 이러한 옵션은 각각 **허용에 해당합니다., 부분적으로 신뢰할 수 있는 호출자속성,** **assemblyDelaySignAttribute,** **assemblyKeyNameAttribute**및 **assemblyKeyFile**속성 .

이러한 특성에 대한 설명은 이 코스의 범위를 벗어납니다.

## <a name="labs"></a>랩

다음 각 랩은 이전 랩을 기반으로 합니다. 순서대로 수행해야 합니다.

## <a name="lab-1-using-the-configuration-api"></a>랩 1: 구성 API 사용

1. *mod9lab이라는*새 웹 사이트를 만듭니다.
2. 사이트에 새 웹 구성 파일을 추가합니다.
3. web.config 파일에 다음을 추가합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

이렇게 하면 web.config 파일에 변경 내용을 저장할 수 있는 권한이 있습니다.

1. Default.aspx에 새 레이블 컨트롤을 추가하고 ID를 **lblDebugStatus로**변경합니다.
2. Default.aspx에 새 단추 컨트롤을 추가합니다.
3. 단추 컨트롤의 ID를 **btnToggleDebug로** 변경하고 텍스트를 **디버그 상태를 전환합니다.**
4. Default.aspx의 코드 숨결 파일에 대한 코드 보기를 열고 다음과 같이 **System.Web.Configuration에** 대한 **using** 문을 추가합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. 아래와 같이 클래스와 페이지\_Init 메서드에 두 개의 개인 변수를 추가합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. 페이지\_로드에 다음 코드를 추가합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. 기본값.aspx를 저장하고 찾아봅습니다. Label 컨트롤에 현재 디버그 상태가 표시됩니다.
2. 디자이너의 단추 컨트롤을 두 번 클릭하고 단추 컨트롤의 Click 이벤트에 다음 코드를 추가합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. 기본값.aspx를 저장하고 찾아보고 버튼을 클릭합니다.
2. 각 단추를 클릭한 후 web.config 파일을 열고 &lt;컴파일&gt; 섹션에서 **디버그** 특성을 관찰합니다.

## <a name="lab-2-logging-application-restarts"></a>랩 2: 로깅 응용 프로그램 다시 시작

이 실습에서는 이벤트 뷰어에서 응용 프로그램 종료, 시작 및 재컴파일의 로깅을 전환할 수 있는 코드를 만듭니다.

1. DropDownList를 default.aspx에 추가하고 ID를 ddlLogAppEvents로 변경합니다.
2. 드롭다운목록에 대한 **자동 포스트백** 속성을 **true로**설정합니다.
3. 드롭다운리스트의 항목 컬렉션에 세 개의 항목을 추가합니다. 첫 번째 항목의 **텍스트를** *선택 값* 및 값 -1을 만듭니다. 두 번째 항목의 **텍스트** 및 **값을** **True로** 만들고 세 번째 항목의 **텍스트** 및 **값을** **False로**만듭니다.
4. default.aspx에 새 레이블을 추가합니다. **id를 lblLogAppEvents로**변경합니다.
5. default.aspx에 대한 코드 숨김 보기를 열고 아래와 같이 HealthMonitoringSection 형식의 변수에 대한 새 선언을 추가합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. 페이지\_Init의 기존 코드에 다음 코드를 추가합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. 드롭다운 리스트를 두 번 클릭하고 선택된IndexChanged 이벤트에 다음 코드를 추가합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. 기본값.aspx를 찾아봅습니다.
2. 드롭다운을 **False로**설정합니다.
3. 이벤트 뷰어에서 응용 프로그램 로그를 지웁니다.
4. 단추를 클릭하여 응용 프로그램의 디버그 특성을 변경합니다.
5. 이벤트 뷰어에서 응용 프로그램 로그를 새로 고칩니다. 

    1. 이벤트가 기록되나요?
    2. 왜 또는 왜?
6. 드롭다운을 **True로 설정합니다.**
7. 단추를 클릭하여 응용 프로그램의 디버그 특성을 전환합니다.
8. 이벤트 뷰어에 응용 프로그램 로그인을 새로 고칩니다. 

    1. 이벤트가 기록되나요?
    2. 앱 종료의 이유는 무엇입니까?
9. 로깅 을 켜고 끄는 실험을 하고 web.config 파일의 변경 내용을 살펴봅니다.

## <a name="more-information"></a>추가 정보:

ASP.NET 2.0의 공급자 모델을 사용하면 응용 프로그램 계측뿐만 아니라 멤버십, 프로필 등과 같은 많은 다른 용도에 대해 사용자 고유의 공급자를 만들 수 있습니다. 응용 프로그램 이벤트를 텍스트 파일에 기록하는 사용자 지정 공급자 작성에 대한 자세한 내용은 [이 링크를](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)방문하십시오.
