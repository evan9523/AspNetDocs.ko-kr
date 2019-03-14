---
title: ASP.NET Core의 이미지 태그 도우미
author: pkellner
description: 이미지 태그 도우미의 사용 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/image-tag-helper
ms.openlocfilehash: 5eb74a6698911a1c594d11573192cb1b9ed53b49
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030110"
---
# <a name="image-tag-helper-in-aspnet-core"></a>ASP.NET Core의 이미지 태그 도우미

작성자: [Peter Kellner](http://peterkellner.net)

이미지 태그 도우미는 정적 이미지 파일에 캐시 버스팅 동작을 제공하도록 `<img>` 태그를 개선합니다.

캐시 버스팅 문자열은 자산의 URL에 추가된 정적 이미지 파일의 해시를 나타내는 고유한 값입니다. 고유한 문자열은 클라이언트(및 일부 프록시)에게 클라이언트의 캐시가 아닌 호스트 웹 서버에서 이미지를 다시 로드할지 묻습니다.

이미지 원본(`src`)은 호스트 웹 서버의 정적 파일입니다.

* 고유한 캐시 버스팅 문자열이 이미지 원본에 쿼리 매개 변수로 추가됩니다.
* 호스트 웹 서버에 위치한 파일이 변경될 경우 갱신된 요청 매개 변수를 포함하는 고유한 요청 URL이 생성됩니다.

태그 도우미에 대한 개요는 <xref:mvc/views/tag-helpers/intro>를 참조하세요.

## <a name="image-tag-helper-attributes"></a>이미지 태그 도우미 특성

### <a name="src"></a>src

이미지 태그 도우미를 활성화하려면 `<img>` 요소에 `src` 특성이 필요합니다.

이미지 원본(`src`)은 서버의 물리적 정적 파일을 가리켜야 합니다. `src`가 원격 URI일 경우 캐시 버스팅 쿼리 문자열 매개 변수가 생성되지 않습니다.

### <a name="asp-append-version"></a>asp-append-version

`asp-append-version`에 `src` 특성과 `true` 값이 지정되면 이미지 태그 도우미가 호출됩니다.

다음 예에서는 이미지 태그 도우미를 사용합니다.

```cshtml
<img src="~/images/asplogo.png" asp-append-version="true" />
```

정적 파일이 */wwwroot/images/* 디렉터리에 있을 경우, 생성되는 HTML은 다음과 비슷합니다(해시는 다름).

```html
<img src="/images/asplogo.png?v=Kl_dqr9NVtnMdsM2MUg4qthUnWZm5T1fCEimBPWDNgM" />
```

매개 변수 `v`에 할당된 값은 디스크에 존재하는 *asplogo.png* 파일의 해시 값입니다. 웹 서버가 정적 파일에 대한 읽기 액세스 권한을 얻을 수 없으면 렌더링된 태그의 `src` 특성에 `v` 매개 변수가 추가되지 않습니다.

## <a name="hash-caching-behavior"></a>해시 캐싱 동작

이미지 태그 도우미는 로컬 웹 서버에서 캐시 공급자를 사용해서 해당 파일의 계산된 `Sha512` 해시를 저장합니다. 파일이 여러 번 요청되면 해시가 다시 계산되지 않습니다. 캐시는 파일의 `Sha512` 해시가 계산될 때 파일에 첨부된 파일 감시자에 의해 무효화됩니다. 디스크에서 파일이 변경되면 새 해시가 계산되고 캐시됩니다.

## <a name="additional-resources"></a>추가 자료

* <xref:performance/caching/memory>
