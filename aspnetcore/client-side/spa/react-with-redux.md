---
title: ASP.NET Core와 함께 React-with-Redux 프로젝트 템플릿 사용
author: SteveSandersonMS
description: React with Redux 및 create-react-app에 대한 ASP.NET Core SPA(단일 페이지 애플리케이션) 프로젝트 템플릿을 시작하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/13/2019
uid: spa/react-with-redux
ms.openlocfilehash: ed2e9aea449ddb09fef049a391f40f57452786a8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028500"
---
# <a name="use-the-react-with-redux-project-template-with-aspnet-core"></a><span data-ttu-id="bcb51-103">ASP.NET Core와 함께 React-with-Redux 프로젝트 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="bcb51-103">Use the React-with-Redux project template with ASP.NET Core</span></span>

<span data-ttu-id="bcb51-104">업데이트된 React-with-Redux 프로젝트 템플릿은 React, Redux 및 CRA([create-react-app](https://github.com/facebookincubator/create-react-app)) 규칙을 사용하여 풍부한 클라이언트 쪽 UI(사용자 인터페이스)를 구현하는 ASP.NET Core 앱에 대한 편리한 시작점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb51-104">The updated React-with-Redux project template provides a convenient starting point for ASP.NET Core apps using React, Redux, and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="bcb51-105">프로젝트 만들기 명령을 제외하고 React-with-Redux 템플릿에 대한 모든 정보는 React 템플릿과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb51-105">With the exception of the project creation command, all information about the React-with-Redux template is the same as the React template.</span></span> <span data-ttu-id="bcb51-106">이 프로젝트 형식을 만들려면 `dotnet new react` 대신 `dotnet new reactredux`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb51-106">To create this project type, run `dotnet new reactredux` instead of `dotnet new react`.</span></span> <span data-ttu-id="bcb51-107">React 기반 템플릿에 공통적인 기능에 대한 자세한 내용은 [React 템플릿 설명서](xref:spa/react)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcb51-107">For more information about the functionality common to both React-based templates, see [React template documentation](xref:spa/react).</span></span>

<span data-ttu-id="bcb51-108">React와 Redux 하위 응용 프로그램을 IIS의 구성에 대 한 자세한 내용은 [ReactRedux 템플릿 2.1: IIS에서 SPA를 사용할 수 없습니다. (aspnet/Templating &num;555)](https://github.com/aspnet/Templating/issues/555)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb51-108">For information on configuring a React-with-Redux sub-application in IIS, see [ReactRedux Template 2.1: Unable to use SPA on IIS (aspnet/Templating &num;555)](https://github.com/aspnet/Templating/issues/555).</span></span>
