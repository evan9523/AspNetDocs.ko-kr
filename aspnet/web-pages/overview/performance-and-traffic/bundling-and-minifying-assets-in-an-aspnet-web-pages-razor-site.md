---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: ASP.NET 웹 페이지(Razor) 사이트에서 에셋 묶기 및 축소 | 마이크로 소프트 문서
author: rick-anderson
description: 번들 및 축소는 사이트를 더 빠르게 만드는 방법입니다. 번들을 사용하면 여러 JavaScript (.js) 파일 또는 여러 개의 계단식 스타일 시트 (...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 2a877c1e1a06ea2357f96b37ec4ae72f9f9c9ff3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81539924"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지(Razor) 사이트에서 자산 묶음 및 축소

[로 마이크로 소프트](https://github.com/microsoft)

> 번들 및 축소는 사이트를 더 빠르게 만드는 방법입니다. 번들링을 사용하면 여러*JavaScript(.js)* 파일 또는 여러 개의 계단식 스타일*시트(.css)* 파일을 결합하여 한 번에 하나씩 다운로드할 수 있습니다. Minification은 공백을 짜내고 다운로드한 파일을 가능한 한 작게 만들기 위해 다른 유형의 압축을 수행합니다.
> 
> > [!NOTE]
> > 필요한 요소를 포함하는 패키지를 아직 Microsoft WebMatrix에서 사용할 수 없기 때문에 ASP.NET 웹 페이지 2의 RC 릴리스는 번들 및 축소를 지원하지 않습니다. 불편을 끼쳐드려 죄송합니다. 이 패키지는 ASP.NET 웹 페이지 2와 WebMatrix 2의 최종 릴리스에서 사용할 수 있을 것으로 예상됩니다.
