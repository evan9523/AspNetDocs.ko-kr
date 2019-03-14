---
ms.openlocfilehash: 939231583679d469d01724cc1a405bd45e46d2c5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57175903"
---
```console
npm run release
```

이 명령은 앱을 실행할 때 제공되는 클라이언트 쪽 자산을 생성합니다. 자산은 *wwwroot* 폴더에 배치됩니다.

Webpack은 다음 작업을 완료했습니다.

* *wwwroot* 디렉터리의 콘텐츠를 제거했습니다.
* TypeScript를 JavaScript로 변환했습니다(*트랜스파일*&mdash;이라는 프로세스).
* 파일 크기를 줄이기 위해 생성된 JavaScript를 변환했습니다(*축소*&mdash;라는 프로세스).
* *src*에서 *wwwroot* 디렉터리로 처리된 JavaScript, CSS 및 HTML 파일을 복사했습니다.
* 다음 요소를 *wwwroot/index.html* 파일에 삽입했습니다.
    * *wwwroot/main.\<hash\>.css* 파일을 참조하는 `<link>` 태그입니다. 이 태그는 `</head>` 태그를 닫기 전에 즉시 배치합니다.
    * 축소된 *wwwroot/main.\<hash\>.js* 파일을 참조하는 `<script>` 태그입니다. 이 태그는 `</body>` 태그를 닫기 전에 즉시 배치합니다.
