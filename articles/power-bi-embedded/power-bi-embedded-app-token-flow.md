---
title: "aaaAuthenticating и авторизации с Power BI Embedded"
description: "Аутентификация и авторизация в Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="f8a14-103">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="f8a14-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="f8a14-104">использует службы Power BI Embedded Hello **ключей** и **токенов приложения** для проверки подлинности и авторизации, вместо явного конечным пользователем проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f8a14-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="f8a14-105">В этой модели ваше приложение управляет проверкой подлинности и авторизацией пользователей.</span><span class="sxs-lookup"><span data-stu-id="f8a14-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="f8a14-106">При необходимости, ваше приложение создает и отправляет токенов приложения hello, сообщает нашей службы toorender hello запрошенного отчета.</span><span class="sxs-lookup"><span data-stu-id="f8a14-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="f8a14-107">Такой подход не требует toouse вашего приложения Azure Active Directory для проверки подлинности пользователя и авторизации, несмотря на то, что вы по-прежнему можете.</span><span class="sxs-lookup"><span data-stu-id="f8a14-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="f8a14-108">Два способа tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="f8a14-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="f8a14-109">**Ключи** можно использовать для всех вызовов REST API в Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="f8a14-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="f8a14-110">можно найти в hello ключи Hello **портал Azure** , щелкнув **все параметры** и затем **ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="f8a14-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="f8a14-111">С ключом следует обращаться как с паролем.</span><span class="sxs-lookup"><span data-stu-id="f8a14-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="f8a14-112">В этих разделах содержится toomake разрешения вызова любого API REST с коллекцией определенную рабочую область.</span><span class="sxs-lookup"><span data-stu-id="f8a14-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="f8a14-113">toouse ключ во время вызова REST добавьте после заголовка авторизации hello:</span><span class="sxs-lookup"><span data-stu-id="f8a14-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="f8a14-114">**Маркеры приложений** используются для всех запросов внедрения.</span><span class="sxs-lookup"><span data-stu-id="f8a14-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="f8a14-115">Они клиентском спроектированный toobe запуска, они будут ограниченные tooa один лучший подход tooset отчета и его срок действия.</span><span class="sxs-lookup"><span data-stu-id="f8a14-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="f8a14-116">Маркеры приложения представляют собой веб-маркеры JWT, подписанные одним из ключей.</span><span class="sxs-lookup"><span data-stu-id="f8a14-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="f8a14-117">Срок действия токена приложение может содержать hello следующих утверждений:</span><span class="sxs-lookup"><span data-stu-id="f8a14-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="f8a14-118">Утверждение</span><span class="sxs-lookup"><span data-stu-id="f8a14-118">Claim</span></span> | <span data-ttu-id="f8a14-119">Описание</span><span class="sxs-lookup"><span data-stu-id="f8a14-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8a14-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="f8a14-120">**ver**</span></span> |<span data-ttu-id="f8a14-121">версия Hello токен приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f8a14-121">hello version of hello app token.</span></span> <span data-ttu-id="f8a14-122">0.2.0 — hello текущей версии.</span><span class="sxs-lookup"><span data-stu-id="f8a14-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="f8a14-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="f8a14-123">**aud**</span></span> |<span data-ttu-id="f8a14-124">Hello предназначен получателя токена hello.</span><span class="sxs-lookup"><span data-stu-id="f8a14-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="f8a14-125">Для Power BI Embedded используйте адрес https://analysis.windows.net/powerbi/api</span><span class="sxs-lookup"><span data-stu-id="f8a14-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="f8a14-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="f8a14-126">**iss**</span></span> |<span data-ttu-id="f8a14-127">Строка, указывающая приложения hello, выдавшего токен hello.</span><span class="sxs-lookup"><span data-stu-id="f8a14-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="f8a14-128">**type**</span><span class="sxs-lookup"><span data-stu-id="f8a14-128">**type**</span></span> |<span data-ttu-id="f8a14-129">Тип токена приложения, который находится в процессе создания Hello.</span><span class="sxs-lookup"><span data-stu-id="f8a14-129">hello type of app token which is being created.</span></span> <span data-ttu-id="f8a14-130">Текущий тип hello поддерживается только **внедрить**.</span><span class="sxs-lookup"><span data-stu-id="f8a14-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="f8a14-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="f8a14-131">**wcn**</span></span> |<span data-ttu-id="f8a14-132">Токен hello имени коллекции рабочей выдается для.</span><span class="sxs-lookup"><span data-stu-id="f8a14-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="f8a14-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="f8a14-133">**wid**</span></span> |<span data-ttu-id="f8a14-134">Токен hello идентификатор рабочей области выдается для.</span><span class="sxs-lookup"><span data-stu-id="f8a14-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="f8a14-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="f8a14-135">**rid**</span></span> |<span data-ttu-id="f8a14-136">Маркер идентификатора hello выдается для отчетов.</span><span class="sxs-lookup"><span data-stu-id="f8a14-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="f8a14-137">**username** (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f8a14-137">**username** (optional)</span></span> |<span data-ttu-id="f8a14-138">При использовании RLS, это строка, которая позволяет идентифицировать пользователя hello при применении правила RLS.</span><span class="sxs-lookup"><span data-stu-id="f8a14-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="f8a14-139">**roles** (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f8a14-139">**roles** (optional)</span></span> |<span data-ttu-id="f8a14-140">Строка, содержащая hello ролей tooselect при применении правил безопасности уровня строк.</span><span class="sxs-lookup"><span data-stu-id="f8a14-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="f8a14-141">При выборе нескольких ролей их нужно передавать в виде массива строк.</span><span class="sxs-lookup"><span data-stu-id="f8a14-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="f8a14-142">**scp** (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f8a14-142">**scp** (optional)</span></span> |<span data-ttu-id="f8a14-143">Строка, содержащая hello области разрешений.</span><span class="sxs-lookup"><span data-stu-id="f8a14-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="f8a14-144">При выборе нескольких ролей их нужно передавать в виде массива строк.</span><span class="sxs-lookup"><span data-stu-id="f8a14-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="f8a14-145">**exp** (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f8a14-145">**exp** (optional)</span></span> |<span data-ttu-id="f8a14-146">Указывает, в какой hello токена истечет время hello.</span><span class="sxs-lookup"><span data-stu-id="f8a14-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="f8a14-147">Его следует передавать в качестве метки времени Unix</span><span class="sxs-lookup"><span data-stu-id="f8a14-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="f8a14-148">**nbf** (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f8a14-148">**nbf** (optional)</span></span> |<span data-ttu-id="f8a14-149">Указывает hello запуске в какой hello токен являются допустимыми.</span><span class="sxs-lookup"><span data-stu-id="f8a14-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="f8a14-150">Его следует передавать в качестве метки времени Unix</span><span class="sxs-lookup"><span data-stu-id="f8a14-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="f8a14-151">Пример маркера приложения будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f8a14-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="f8a14-152">После декодирования он станет выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f8a14-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="f8a14-153">Методы доступны на пакеты SDK, которые упрощают создание apptokens hello.</span><span class="sxs-lookup"><span data-stu-id="f8a14-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="f8a14-154">Например, для .NET можно взглянуть на hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) класс и hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) методы.</span><span class="sxs-lookup"><span data-stu-id="f8a14-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="f8a14-155">Для hello .NET SDK, можно ссылаться по слишком[областей](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="f8a14-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="f8a14-156">Области действия</span><span class="sxs-lookup"><span data-stu-id="f8a14-156">Scopes</span></span>

<span data-ttu-id="f8a14-157">При использовании маркеров внедрения, вы можете toorestrict использование hello ресурсы, которые обеспечивают доступ к.</span><span class="sxs-lookup"><span data-stu-id="f8a14-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="f8a14-158">Для этого можно создать маркер с заданной областью разрешений.</span><span class="sxs-lookup"><span data-stu-id="f8a14-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="f8a14-159">Здесь представлены Hello hello доступные области для Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="f8a14-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="f8a14-160">Область</span><span class="sxs-lookup"><span data-stu-id="f8a14-160">Scope</span></span>|<span data-ttu-id="f8a14-161">Описание</span><span class="sxs-lookup"><span data-stu-id="f8a14-161">Description</span></span>|
|---|---|
|<span data-ttu-id="f8a14-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="f8a14-162">Dataset.Read</span></span>|<span data-ttu-id="f8a14-163">Предоставляет разрешение tooread hello указанного набора данных.</span><span class="sxs-lookup"><span data-stu-id="f8a14-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="f8a14-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="f8a14-164">Dataset.Write</span></span>|<span data-ttu-id="f8a14-165">Предоставляет разрешение toowrite toohello указанного набора данных.</span><span class="sxs-lookup"><span data-stu-id="f8a14-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="f8a14-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="f8a14-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="f8a14-167">Предоставляет разрешение tooread и записи toohello указанного набора данных.</span><span class="sxs-lookup"><span data-stu-id="f8a14-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="f8a14-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="f8a14-168">Report.Read</span></span>|<span data-ttu-id="f8a14-169">Предоставляет разрешение tooview hello указанного отчета.</span><span class="sxs-lookup"><span data-stu-id="f8a14-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="f8a14-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="f8a14-170">Report.ReadWrite</span></span>|<span data-ttu-id="f8a14-171">Предоставляет разрешение tooview и измените hello указанного отчета.</span><span class="sxs-lookup"><span data-stu-id="f8a14-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="f8a14-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="f8a14-172">Workspace.Report.Create</span></span>|<span data-ttu-id="f8a14-173">Предоставляет разрешение toocreate новый отчет в пределах указанного hello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="f8a14-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="f8a14-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="f8a14-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="f8a14-175">Предоставляет разрешение tooclone существующий отчет в пределах указанного hello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="f8a14-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="f8a14-176">Можно указать несколько областей с помощью пробел между областями hello hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f8a14-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="f8a14-177">**Обязательные утверждения — области**</span><span class="sxs-lookup"><span data-stu-id="f8a14-177">**Required claims - scopes**</span></span>

<span data-ttu-id="f8a14-178">точка подключения службы: {scopesClaim} scopesClaim может быть строку или массив строк, отметить hello допускается разрешения tooworkspace ресурсы (отчета, набора данных, и т. д.)</span><span class="sxs-lookup"><span data-stu-id="f8a14-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="f8a14-179">Декодированный маркер, с областями определен, будет выглядеть аналогично toohello следующее.</span><span class="sxs-lookup"><span data-stu-id="f8a14-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="f8a14-180">Операции и области</span><span class="sxs-lookup"><span data-stu-id="f8a14-180">Operations and scopes</span></span>

|<span data-ttu-id="f8a14-181">Операция</span><span class="sxs-lookup"><span data-stu-id="f8a14-181">Operation</span></span>|<span data-ttu-id="f8a14-182">Целевой ресурс</span><span class="sxs-lookup"><span data-stu-id="f8a14-182">Target resource</span></span>|<span data-ttu-id="f8a14-183">Разрешения для маркеров</span><span class="sxs-lookup"><span data-stu-id="f8a14-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="f8a14-184">Создайте (в памяти) новый отчет на основе набора данных.</span><span class="sxs-lookup"><span data-stu-id="f8a14-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="f8a14-185">Выборка</span><span class="sxs-lookup"><span data-stu-id="f8a14-185">Dataset</span></span>|<span data-ttu-id="f8a14-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="f8a14-186">Dataset.Read</span></span>|
|<span data-ttu-id="f8a14-187">Создание нового отчета, основанного на наборе данных (в памяти) и сохраните отчет hello.</span><span class="sxs-lookup"><span data-stu-id="f8a14-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="f8a14-188">Выборка</span><span class="sxs-lookup"><span data-stu-id="f8a14-188">Dataset</span></span>|<span data-ttu-id="f8a14-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="f8a14-189">* Dataset.Read</span></span><br><span data-ttu-id="f8a14-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="f8a14-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="f8a14-191">Просмотр и изменение (в памяти) существующего отчета.</span><span class="sxs-lookup"><span data-stu-id="f8a14-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="f8a14-192">Report.Read подразумевает наличие Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="f8a14-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="f8a14-193">Это не позволит toosave изменения разрешений.</span><span class="sxs-lookup"><span data-stu-id="f8a14-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="f8a14-194">Отчет</span><span class="sxs-lookup"><span data-stu-id="f8a14-194">Report</span></span>|<span data-ttu-id="f8a14-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="f8a14-195">Report.Read</span></span>|
|<span data-ttu-id="f8a14-196">Изменение и сохранение существующего отчета.</span><span class="sxs-lookup"><span data-stu-id="f8a14-196">Edit and save an existing report.</span></span>|<span data-ttu-id="f8a14-197">Отчет</span><span class="sxs-lookup"><span data-stu-id="f8a14-197">Report</span></span>|<span data-ttu-id="f8a14-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="f8a14-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="f8a14-199">Сохранение копии отчета ("Сохранить как").</span><span class="sxs-lookup"><span data-stu-id="f8a14-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="f8a14-200">Отчет</span><span class="sxs-lookup"><span data-stu-id="f8a14-200">Report</span></span>|<span data-ttu-id="f8a14-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="f8a14-201">* Report.Read</span></span><br><span data-ttu-id="f8a14-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="f8a14-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="f8a14-203">Вот как работает hello потока</span><span class="sxs-lookup"><span data-stu-id="f8a14-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="f8a14-204">Скопируйте ключи tooyour hello API приложения.</span><span class="sxs-lookup"><span data-stu-id="f8a14-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="f8a14-205">Можно получить ключи hello в **портала Azure**.</span><span class="sxs-lookup"><span data-stu-id="f8a14-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="f8a14-206">Маркер декларирует утверждение и имеет срок действия.</span><span class="sxs-lookup"><span data-stu-id="f8a14-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="f8a14-207">Маркер подписывается с помощью ключей доступа API.</span><span class="sxs-lookup"><span data-stu-id="f8a14-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="f8a14-208">Пользователь запрашивает tooview отчет.</span><span class="sxs-lookup"><span data-stu-id="f8a14-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="f8a14-209">Маркер проверяется с помощью ключей доступа API.</span><span class="sxs-lookup"><span data-stu-id="f8a14-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="f8a14-210">Power BI Embedded отправляет toouser отчета.</span><span class="sxs-lookup"><span data-stu-id="f8a14-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="f8a14-211">После **Power BI Embedded** пользователь toohello отчета, отправляет hello пользователь может просматривать отчет hello в пользовательские приложения.</span><span class="sxs-lookup"><span data-stu-id="f8a14-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="f8a14-212">Например, если вы импортировали hello [анализ PBIX данных продаж образец](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello образец веб-приложение будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f8a14-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="f8a14-213">См. также</span><span class="sxs-lookup"><span data-stu-id="f8a14-213">See Also</span></span>

[<span data-ttu-id="f8a14-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="f8a14-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="f8a14-215">Приступая к работе с примером Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="f8a14-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="f8a14-216">Типичные сценарии использования Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="f8a14-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="f8a14-217">Начало работы с Microsoft Power BI Embedded (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="f8a14-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="f8a14-218">Репозиторий PowerBI-CSharp на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="f8a14-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="f8a14-219">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="f8a14-219">More questions?</span></span> [<span data-ttu-id="f8a14-220">Повторите hello сообщества Power BI</span><span class="sxs-lookup"><span data-stu-id="f8a14-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

