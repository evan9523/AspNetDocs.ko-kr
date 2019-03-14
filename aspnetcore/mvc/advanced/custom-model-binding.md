---
title: ASP.NET Core의 사용자 지정 모델 바인딩
author: ardalis
description: 모델 바인딩을 통해 컨트롤러 작업이 ASP.NET Core의 모델 형식과 함께 직접 작동할 수 있게 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 11/13/2018
uid: mvc/advanced/custom-model-binding
ms.openlocfilehash: 33551c9fc22561b992b4a09a4c7187ade136c09c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057080"
---
# <a name="custom-model-binding-in-aspnet-core"></a>ASP.NET Core의 사용자 지정 모델 바인딩

작성자: [Steve Smith](https://ardalis.com/)

모델 바인딩을 통해 컨트롤러 작업에서 HTTP 요청이 아닌 모델 형식(메서드 인수로 전달된)을 직접 작업할 수 있습니다. 들어오는 요청 데이터와 애플리케이션 모델 간의 매핑은 모델 바인더를 통해 처리됩니다. 개발자는 사용자 지정 모델 바인더를 구현하여 기본 모델 바인딩 기능을 확장할 수 있습니다(일반적으로 개발자가 고유의 공급자를 작성할 필요는 없음).

[GitHub에서 샘플 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/advanced/custom-model-binding/)

## <a name="default-model-binder-limitations"></a>기본 모델 바인더 제한 사항

기본 모델 바인더는 대부분의 공용 .NET Core 데이터 형식을 지원하며 대부분의 개발자 요구 사항을 충족해야 합니다. 요청의 텍스트 기반 입력을 모델 형식에 직접 바인딩할 것으로 예상됩니다. 바인딩하려면 입력을 변환해야 할 수도 있습니다. 예를 들어 모델 데이터를 조회하는 데 사용할 수 있는 키를 갖고 있는 경우 그 키를 기반으로 사용자 지정 모델 바인더를 사용하여 데이터를 가져올 수 있습니다.

## <a name="model-binding-review"></a>모델 바인딩 검토

모델 바인딩은 작업을 수행하는 형식에 대한 특정 정의를 사용합니다. *단순 형식*은 입력의 단일 문자열에서 변환됩니다. *복합 형식*은 여러 입력 값에서 변환됩니다. 프레임워크는 `TypeConverter`의 존재 여부에 따라 차이점을 확인합니다. 외부 리소스가 필요 없는 간단한 `string` -> `SomeType` 매핑이 있는 경우 형식 변환기를 만드는 것이 좋습니다.

개발자 고유의 사용자 지정 모델 바인더를 만들기 전에 기존 모델 바인더가 구현되는 방식을 검토하는 것이 좋습니다. base64로 인코딩된 문자열을 바이트 배열로 변환하는 데 사용할 수 있는 [ByteArrayModelBinder](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.binders.bytearraymodelbinder)를 고려해 보세요. 바이트 배열은 종종 파일 또는 데이터베이스 BLOB 필드로 저장됩니다.

### <a name="working-with-the-bytearraymodelbinder"></a>ByteArrayModelBinder 사용

Base64로 인코딩된 문자열은 이진 데이터를 나타내는 데 사용할 수 있습니다. 예를 들어 다음 이미지를 문자열로 인코딩할 수 있습니다.

![dotnet bot](custom-model-binding/images/bot.png "dotnet bot")

인코딩된 문자열의 일부가 다음 그림에 표시되어 있습니다.

![인코딩된 dotnet bot](custom-model-binding/images/encoded-bot.png "인코딩된 dotnet bot")

[샘플의 추가 정보](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/advanced/custom-model-binding/sample/CustomModelBindingSample/README.md)에 제공된 지침에 따라 base64로 인코딩된 문자열을 파일로 변환합니다.

ASP.NET Core MVC는 base64로 인코드된 문자열을 가져온 후 `ByteArrayModelBinder`를 사용하여 바이트 배열로 변환할 수 있습니다. [IModelBinderProvider](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.imodelbinderprovider)를 구현하는 [ByteArrayModelBinderProvider](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.binders.bytearraymodelbinderprovider)는 `byte[]` 인수를 `ByteArrayModelBinder`에 매핑합니다.

```csharp
public IModelBinder GetBinder(ModelBinderProviderContext context)
{
    if (context == null)
    {
        throw new ArgumentNullException(nameof(context));
    }

    if (context.Metadata.ModelType == typeof(byte[]))
    {
        return new ByteArrayModelBinder();
    }

    return null;
}
```

개발자 고유의 사용자 지정 모델 바인더를 만들 때 고유의 `IModelBinderProvider` 형식을 구현해도 되고 [ModelBinderAttribute](/dotnet/api/microsoft.aspnetcore.mvc.modelbinderattribute)를 사용해도 됩니다.

다음 예제에서는 `ByteArrayModelBinder`를 사용하여 base64로 인코딩된 문자열을 `byte[]`로 변환하고 그 결과를 파일에 저장하는 방법을 보여줍니다.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Controllers/ImageController.cs?name=post1&highlight=3)]

[Postman](https://www.getpostman.com/) 같은 도구를 사용하여 base64로 인코딩된 문자열을 이 api 메서드에 게시할 수 있습니다.

![postman](custom-model-binding/images/postman.png "postman")

바인더가 요청 데이터를 적절한 이름의 속성 또는 인수로 바인딩할 수 있는 한, 모델 바인딩은 성공합니다. 다음 예제에서는 보기 모델에 `ByteArrayModelBinder`를 사용하는 방법을 보여줍니다.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Controllers/ImageController.cs?name=post2&highlight=2)]

## <a name="custom-model-binder-sample"></a>사용자 지정 모델 바인더 샘플

이 섹션에서는 다음과 같은 사용자 지정 모델 바인더를 구현하겠습니다.

- 들어오는 요청 데이터를 강력한 형식의 키 인수로 변환합니다.
- Entity Framework Core를 사용하여 연결된 엔터티를 가져옵니다.
- 연결된 엔터티를 작업 메서드에 인수로 전달합니다.

다음 샘플은 `Author` 모델에서 `ModelBinder` 특성을 사용합니다.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Data/Author.cs?highlight=10)]

이전 코드에서 `ModelBinder` 특성은 `Author` 작업 매개 변수를 바인딩하는 데 사용할 `IModelBinder` 형식을 지정합니다.

다음 `AuthorEntityBinder` 클래스는 Entity Framework Core 및 `authorId`를 사용하여 데이터 원본에서 엔터티를 가져와 `Author` 매개 변수를 바인딩합니다.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Binders/AuthorEntityBinder.cs?name=demo)]

> [!NOTE]
> 앞의 `AuthorEntityBinder` 클래스는 사용자 지정 모델 바인더를 설명하기 위한 것입니다. 이 클래스는 조회 시나리오의 모범 사례를 설명하기 위한 것이 아닙니다. 조회의 경우 `authorId`를 바인딩하고 작업 메서드에서 데이터베이스를 쿼리합니다. 이 방식은 모델 바인딩 실패를 `NotFound` 사례와 구분합니다.

다음 코드는 작업 메서드에 `AuthorEntityBinder`를 사용하는 방법을 보여줍니다.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Controllers/BoundAuthorsController.cs?name=demo2&highlight=2)]

`ModelBinder` 특성은 기본 규칙을 사용하지 않는 매개 변수에 `AuthorEntityBinder`를 적용하는 데 사용할 수 있습니다.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Controllers/BoundAuthorsController.cs?name=demo1&highlight=2)]

이 예에서는 인수 이름이 기본 `authorId`가 아니기 때문에 `ModelBinder` 특성을 사용하여 매개 변수에 지정됩니다. 컨트롤러와 작업 메서드는 작업 메서드에서 엔터티를 조회하는 것에 비해 간단합니다. Entity Framework Core를 사용하여 작성자를 가져오는 논리는 모델 바인더로 이동되었습니다. `Author` 모델에 바인딩하는 메서드가 여러 개 있는 경우 상당히 간소화될 수 있습니다.

개별 모델 속성(viewmodel처럼) 또는 작업 메서드 매개 변수에 `ModelBinder` 특성을 적용하여 그 형식 또는 작업에만 해당하는 특정 모델 바인더 또는 모델을 지정할 수 있습니다.

### <a name="implementing-a-modelbinderprovider"></a>ModelBinderProvider 구현

특성을 적용하는 대신, `IModelBinderProvider`를 구현할 수도 있습니다. 기본 제공 프레임워크 바인더는 이 방식으로 구현됩니다. 바인더가 작동하는 형식을 지정할 때 바인더가 허용하는 입력이 **아니라** 바인더가 생성하는 인수 형식을 지정합니다. 다음 바인더 공급자는 `AuthorEntityBinder`를 작업합니다. 공급자의 MVC 컬렉션에 추가할 때 `Author` 또는 `Author`-형식 매개 변수에서 `ModelBinder` 특성을 사용할 필요가 없습니다.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Binders/AuthorEntityBinderProvider.cs?highlight=17-20)]

> 참고: 앞의 코드는 `BinderTypeModelBinder`를 반환합니다. `BinderTypeModelBinder`는 모델 바인더에 대한 팩터리 역할을 하며 DI(종속성 주입)를 제공합니다. `AuthorEntityBinder`는 EF Core에 액세스하려면 DI가 필요합니다. 모델 바인더에서 DI의 서비스를 요구하는 경우 `BinderTypeModelBinder`를 사용합니다.

사용자 지정 모델 바인더 공급자를 사용하려면 `ConfigureServices`에서 추가합니다.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Startup.cs?name=callout&highlight=5-9)]

모델 바인더를 평가할 때 공급자 컬렉션은 순서대로 검사됩니다. 바인더를 반환하는 첫 번째 공급자가 사용됩니다.

다음 이미지는 디버거의 기본 모델 바인더를 보여줍니다.

![기본 모델 바인더](custom-model-binding/images/default-model-binders.png "기본 모델 바인더")

컬렉션 끝에 공급자를 추가하면 사용자 지정 바인더가 기회를 얻기도 전에 기본 제공 모델 바인더가 호출될 수 있습니다. 이 예제에서는 `Author` 작업 인수에 사용되도록 사용자 지정 공급자를 컬렉션의 시작 부분에 추가합니다.

[!code-csharp[](custom-model-binding/sample/CustomModelBindingSample/Startup.cs?name=callout&highlight=5-9)]

## <a name="recommendations-and-best-practices"></a>권장 사항 및 모범 사례

사용자 지정 모델 바인더:

- 상태 코드를 설정하거나 결과를 반환하려고 시도하면 안 됩니다(예를 들어 404 찾을 수 없음). 모델 바인딩이 실패하면 [작업 필터](xref:mvc/controllers/filters) 또는 작업 메서드 자체의 논리에서 오류를 처리해야 합니다.
- 작업 메서드에서 반복 코드와 교차 편집 문제를 제거하는 데 가장 유용합니다.
- 일반적으로 문자열을 사용자 지정 형식으로 변환하는 데 사용되지 않습니다. [`TypeConverter`](/dotnet/api/system.componentmodel.typeconverter)가 더 좋은 옵션입니다.
