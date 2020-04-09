---
uid: webhooks/diagnostics/debugging
title: ASP.NET 웹후크 디버깅 | 마이크로 소프트 문서
author: rick-anderson
description: ASP.NET 웹후크를 디버깅하는 방법.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675377"
---
# <a name="aspnet-webhooks-debugging"></a>ASP.NET 웹후크 디버깅

## <a name="debugging-in-azure"></a>Azure에서 디버깅

Azure에서 실행 하는 동안 웹 응용 프로그램을 디버깅 하려면 [Visual Studio를 사용 하 여 Azure 앱 서비스에서 웹 앱 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)자습서를 참조 하십시오.

## <a name="debugging-with-source-and-symbols"></a>원본 및 기호로 디버깅

사용자 고유의 코드를 디버깅하는 것 외에도 Microsoft ASP.NET WebHooks및 실제로 모든 .NET으로 디버깅할 수 있습니다. 로컬또는 원격으로 디버깅하든 상관없이 작동합니다. 먼저, **디버그로** 이동한 다음 **옵션 및 설정으로**이동하여 소스와 기호를 찾으려면 Visual Studio를 구성합니다. 다음과 같은 옵션을 설정합니다.

![옵션 및 설정](_static/SourceSymbols.png)

그런 다음 소스 및 기호를 다운로드하기 위해 [symbolsource.org](http://symbolsource.org) 대한 링크를 추가합니다. 위의 메뉴의 **기호** 탭으로 이동하여 다음을 기호 위치로 추가합니다.

```
http://srv.symbolsource.org/pdb/Public
```

또한 캐시 디렉터리에 짧은 이름이 있는지 확인합니다. 그렇지 않으면 파일 이름이 너무 길어 기호가 로드되지 않을 수 있습니다. 샘플 경로는 다음과 같은 것입니다.

```
C:\SymCache
```

설정은 다음과 유사해야 합니다.

![옵션 기호 파일 위치 예제](_static/SymSource.png)
