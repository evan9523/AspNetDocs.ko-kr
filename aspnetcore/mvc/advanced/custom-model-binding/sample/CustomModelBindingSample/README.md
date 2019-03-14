---
ms.openlocfilehash: 71a40fcab8f1d1005cbe9327d01a42484765a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059640"
---
# <a name="custom-model-binding-demo"></a><span data-ttu-id="41d8a-101">사용자 지정 모델 바인딩 데모</span><span class="sxs-lookup"><span data-stu-id="41d8a-101">Custom Model Binding Demo</span></span>

<span data-ttu-id="41d8a-102">앱을 실행하고 base64로 인코딩된 문자열을 `ImageController` 엔드포인트(`/api/image/`)에 게시하여 `ByteArrayModelBinder`를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="41d8a-102">Test `ByteArrayModelBinder` by running the app and POSTing a base64-encoded string to the `ImageController` endpoint (`/api/image/`).</span></span> <span data-ttu-id="41d8a-103">요청 본문에 파일 및 파일 이름 속성을 양식 데이터로 지정합니다([Postman](https://www.getpostman.com/) 또는 유사한 도구 사용).</span><span class="sxs-lookup"><span data-stu-id="41d8a-103">Specify the file and filename properties in the request body as form-data (using [Postman](https://www.getpostman.com/) or a similar tool).</span></span> <span data-ttu-id="41d8a-104">[이 샘플 문자열](Base64String.txt)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41d8a-104">You can use [this sample string](Base64String.txt).</span></span> <span data-ttu-id="41d8a-105">결과는 지정된 파일 이름으로 *wwwroot/images/upload* 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="41d8a-105">The result is saved in the *wwwroot/images/upload* folder with the filename specified.</span></span>

<span data-ttu-id="41d8a-106">사용자 지정 바인딩 예제를 테스트하려면 다음 엔드포인트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41d8a-106">To test the custom binding example, try the following endpoints:</span></span>

* <span data-ttu-id="41d8a-107">/api/authors/1</span><span class="sxs-lookup"><span data-stu-id="41d8a-107">/api/authors/1</span></span>
* <span data-ttu-id="41d8a-108">/api/authors/2(찾을 수 없음)</span><span class="sxs-lookup"><span data-stu-id="41d8a-108">/api/authors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="41d8a-109">/api/boundauthors/1</span><span class="sxs-lookup"><span data-stu-id="41d8a-109">/api/boundauthors/1</span></span>
* <span data-ttu-id="41d8a-110">/api/boundauthors/2(찾을 수 없음)</span><span class="sxs-lookup"><span data-stu-id="41d8a-110">/api/boundauthors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="41d8a-111">/api/boundauthors/get/1</span><span class="sxs-lookup"><span data-stu-id="41d8a-111">/api/boundauthors/get/1</span></span>
* <span data-ttu-id="41d8a-112">/api/boundauthors/get/2(콘텐츠 없음) &ndash; 이 작업은 null을 검사하지 않고 *404 찾을 수 없음*을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="41d8a-112">/api/boundauthors/get/2 (NO CONTENT) &ndash; This action doesn't check for null and returns a *404 Not Found*.</span></span>
