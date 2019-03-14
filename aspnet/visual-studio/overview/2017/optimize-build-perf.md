---
uid: visual-studio/overview/2017/optimize-build-perf
title: 솔루션에 대한 빌드 성능 최적화
author: AngelosP
description: 솔루션에 대한 빌드 성능 최적화
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050510"
---
# <a name="optimize-build-performance-for-solution"></a>솔루션에 대한 빌드 성능 최적화

Visual Studio 2017 15.8 또는 나중에 메뉴 항목을 포함 합니다. **빌드할** > **ASP.NET 컴파일** > **솔루션에 대 한 빌드 성능을 최적화**합니다.

![새 메뉴 항목의 스크린샷](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET에서는 ASP.NET 프로젝트는 컴파일러의 복사본에 저마다 독특한 즉 런타임에 해당 뷰를 컴파일합니다. 그러나 개발자 컴퓨터에서 컴파일러의 복사본에는 Visual Studio의 복사본과 일치 하지 않습니다 하는 경우 빌드 성능이 저하 됩니다 증분 빌드 1 ~ 3 초 순서. 이 기능은 일반적으로 증분 빌드 속도의 Visual Studio와 일치 하도록 컴파일러에 프로젝트의 복사본을 업데이트 합니다.

**이 Asp.net 4.7.1 적용할 또는 나중에 프로젝트에 해당, ASP.NET Core에 적용 되지 않습니다.**
