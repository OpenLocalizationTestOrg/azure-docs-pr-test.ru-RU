---
title: "Сквозная проверка подлинности в Azure AD Connect — смарт-блокировка | Документы Майкрософт"
description: "В этой статье описывается, как сквозная проверка подлинности Azure Active Directory (Azure AD) защищает учетные записи локальных от атак методом подбора пароля в облаке hello."
services: active-directory
keywords: "сквозная проверка подлинности azure ad connect, установка active directory, необходимые компоненты для azure ad, единый вход"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="69b54-104">Сквозная проверка подлинности Azure Active Directory: смарт-блокировка</span><span class="sxs-lookup"><span data-stu-id="69b54-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="69b54-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="69b54-105">Overview</span></span>

<span data-ttu-id="69b54-106">Azure AD обеспечивает защиту от атак методом подбора пароля и позволяет предотвратить потерю доступа пользователей к приложениям Office 365 и SaaS.</span><span class="sxs-lookup"><span data-stu-id="69b54-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="69b54-107">Эта функция, которая называется **смарт-блокировкой**, поддерживается при входе с помощью сквозной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="69b54-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="69b54-108">Смарт-блокировки по умолчанию включена для всех клиентов и защиты своей учетной записи пользователя все время hello; Нет tooturn без необходимости его на.</span><span class="sxs-lookup"><span data-stu-id="69b54-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all hello time; there is no need tooturn it on.</span></span>

<span data-ttu-id="69b54-109">Смарт-блокировка отслеживает неудачные попытки входа в систему и по достижении определенного **порогового значения блокировки** включает блокировку в течение заданного **периода блокировки**.</span><span class="sxs-lookup"><span data-stu-id="69b54-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="69b54-110">Отклоняются все учетное попытки злоумышленника hello во время длительности блокировки hello.</span><span class="sxs-lookup"><span data-stu-id="69b54-110">Any sign-in attempts from hello attacker during hello Lockout Duration are rejected.</span></span> <span data-ttu-id="69b54-111">Если по-прежнему hello атаки, hello последующих Сбой попытки входа окончании hello продолжительность блокировки приведет к более длительности блокировки.</span><span class="sxs-lookup"><span data-stu-id="69b54-111">If hello attack continues, hello subsequent failed sign-in attempts after hello Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="69b54-112">по умолчанию Hello пороговое значение блокировки — 10 неудачных попыток входа, а также по умолчанию hello, длительность блокировки, составляет 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="69b54-112">hello default Lockout Threshold is 10 failed attempts, and hello default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="69b54-113">Смарт-блокировки также различаются входы подлинность пользователей и от злоумышленников и только блокируются злоумышленники hello в большинстве случаев.</span><span class="sxs-lookup"><span data-stu-id="69b54-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out hello attackers in most cases.</span></span> <span data-ttu-id="69b54-114">Это не позволяет злоумышленникам намеренно заблокировать вход для настоящих пользователей.</span><span class="sxs-lookup"><span data-stu-id="69b54-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="69b54-115">Мы используем за вход поведение, устройства пользователей & браузеры и другие сигналы toodistinguish между подлинность пользователей и злоумышленники.</span><span class="sxs-lookup"><span data-stu-id="69b54-115">We use past sign-in behavior, users’ devices & browsers and other signals toodistinguish between genuine users and attackers.</span></span> <span data-ttu-id="69b54-116">Мы постоянно улучшаем наши алгоритмы.</span><span class="sxs-lookup"><span data-stu-id="69b54-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="69b54-117">Поскольку сквозная проверка подлинности перенаправляет запросы на проверку пароля на вашей локальной Active Directory (AD), вам потребуется tooprevent злоумышленниками, блокировку учетных записей пользователей AD.</span><span class="sxs-lookup"><span data-stu-id="69b54-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need tooprevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="69b54-118">Так как у вас есть собственные политики блокировки учетных записей AD (в частности, [ **пороговое значение блокировки** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) и [ **Сброс счетчика блокировки учетной записи после политики** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), необходимо пороговое значение блокировки tooconfigure Azure AD и длительность блокировки соответствующим образом значения toofilter out атак в облаке hello, прежде чем они достигнут локальной AD.</span><span class="sxs-lookup"><span data-stu-id="69b54-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need tooconfigure Azure AD’s Lockout Threshold and Lockout Duration values appropriately toofilter out attacks in hello cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="69b54-119">возможность смарт-блокировки Hello предоставляется бесплатно и является _на_ по умолчанию для всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="69b54-119">hello Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="69b54-120">Однако изменение порогового значения блокировки и блокировка значений с помощью Graph API Azure AD должна вашу лицензию клиента toohave по крайней мере один Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="69b54-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant toohave at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="69b54-121">Не требуется лицензия Azure AD Premium P2 _каждого пользователя_ tooget hello смарт-блокировку с проверкой подлинности к серверу.</span><span class="sxs-lookup"><span data-stu-id="69b54-121">You don't need an Azure AD Premium P2 license _per user_ tooget hello Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="69b54-122">tooensure что пользователей локальных учетных записей AD также защищены, требуется tooensure:</span><span class="sxs-lookup"><span data-stu-id="69b54-122">tooensure that your users’ on-premises AD accounts are well protected, you need tooensure that:</span></span>

1.  <span data-ttu-id="69b54-123">Пороговое значение блокировки Azure AD _меньше_, чем пороговое значение блокировки учетных записей AD.</span><span class="sxs-lookup"><span data-stu-id="69b54-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="69b54-124">Рекомендуется устанавливать значения hello таким образом, что пороговое значение блокировки учетной записи AD имеет по крайней мере два или три раза пороговое значение блокировки Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69b54-124">We recommend that you set hello values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="69b54-125">Продолжительность блокировки Azure AD (в секундах) _больше_, чем период сброса счетчика блокировки учетных записей AD (в минутах).</span><span class="sxs-lookup"><span data-stu-id="69b54-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="69b54-126">Проверка политик блокировки учетных записей AD</span><span class="sxs-lookup"><span data-stu-id="69b54-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="69b54-127">Используйте следующие инструкции tooverify hello политик блокировки учетных записей AD:</span><span class="sxs-lookup"><span data-stu-id="69b54-127">Use hello following instructions tooverify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="69b54-128">Откройте средство управления групповой политикой hello.</span><span class="sxs-lookup"><span data-stu-id="69b54-128">Open hello Group Policy Management tool.</span></span>
2.  <span data-ttu-id="69b54-129">Изменение hello групповой политики, примененные tooall пользователей, например, политика домена по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="69b54-129">Edit hello group policy that is applied tooall users, for example, hello Default Domain Policy.</span></span>
3.  <span data-ttu-id="69b54-130">Перейдите tooComputer Конфигурация компьютера\Политики\Параметры Windows\Параметры безопасности\Политики записей\Политика блокировки политика.</span><span class="sxs-lookup"><span data-stu-id="69b54-130">Navigate tooComputer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="69b54-131">Проверьте пороговое значение блокировки учетных записей и период сброса счетчика блокировки учетных записей.</span><span class="sxs-lookup"><span data-stu-id="69b54-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Политики блокировки учетных записей AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a><span data-ttu-id="69b54-133">Использовать Graph API toomanage hello значения блокировки смарт-клиента</span><span class="sxs-lookup"><span data-stu-id="69b54-133">Use hello Graph API toomanage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="69b54-134">Изменение порогового значения блокировки и периода блокировки с помощью API Graph Azure AD — это функция Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="69b54-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="69b54-135">Он также должен toobe глобального администратора для клиента.</span><span class="sxs-lookup"><span data-stu-id="69b54-135">It also needs you toobe a Global Administrator on your tenant.</span></span>

<span data-ttu-id="69b54-136">Можно использовать [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, задания и обновления значений смарт-блокировки Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69b54-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="69b54-137">Однако эти операции можно также выполнить программными средствами.</span><span class="sxs-lookup"><span data-stu-id="69b54-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="69b54-138">Считывание параметров смарт-блокировки</span><span class="sxs-lookup"><span data-stu-id="69b54-138">Read Smart Lockout values</span></span>

<span data-ttu-id="69b54-139">Выполните эти шаги tooread значения смарт-блокировки вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="69b54-139">Follow these steps tooread your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="69b54-140">Войдите в Graph Explorer как глобальный администратор клиента.</span><span class="sxs-lookup"><span data-stu-id="69b54-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="69b54-141">Если будет предложено, предоставление доступа для hello запрашиваемые разрешения на доступ.</span><span class="sxs-lookup"><span data-stu-id="69b54-141">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="69b54-142">Щелкните «Изменить разрешения» и выберите разрешение «Directory.ReadWrite.All» hello.</span><span class="sxs-lookup"><span data-stu-id="69b54-142">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="69b54-143">Настройте запрос Graph API hello следующим образом: версия набора слишком «Бета» тип запроса слишком «GET» и URL-адрес слишком`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="69b54-143">Configure hello Graph API request as follows: Set version too“BETA”, request type too“GET” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="69b54-144">Щелкните «Выполнить запрос» toosee значения смарт-блокировки вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="69b54-144">Click "Run Query" toosee your tenant's Smart Lockout values.</span></span> <span data-ttu-id="69b54-145">Если вы не устанавливали значений параметров клиента, вы увидите пустой набор параметров.</span><span class="sxs-lookup"><span data-stu-id="69b54-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="69b54-146">Установка параметров смарт-блокировки</span><span class="sxs-lookup"><span data-stu-id="69b54-146">Set Smart Lockout values</span></span>

<span data-ttu-id="69b54-147">Выполните эти шаги tooset значения смарт-блокировки вашего клиента (для hello только в первый раз).</span><span class="sxs-lookup"><span data-stu-id="69b54-147">Follow these steps tooset your tenant’s Smart Lockout values (for hello first time only):</span></span>

1. <span data-ttu-id="69b54-148">Войдите в Graph Explorer как глобальный администратор клиента.</span><span class="sxs-lookup"><span data-stu-id="69b54-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="69b54-149">Если будет предложено, предоставление доступа для hello запрашиваемые разрешения на доступ.</span><span class="sxs-lookup"><span data-stu-id="69b54-149">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="69b54-150">Щелкните «Изменить разрешения» и выберите разрешение «Directory.ReadWrite.All» hello.</span><span class="sxs-lookup"><span data-stu-id="69b54-150">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="69b54-151">Настройте запрос Graph API hello следующим образом: версия набора слишком «Бета» тип запроса слишком «POST» и URL-адрес слишком`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="69b54-151">Configure hello Graph API request as follows: Set version too“BETA”, request type too“POST” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="69b54-152">Скопируйте и вставьте после запроса JSON в поле «Текст запроса» hello hello.</span><span class="sxs-lookup"><span data-stu-id="69b54-152">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="69b54-153">Изменить соответствующим образом значения hello смарт-блокировки и использовать случайный идентификатор GUID для `templateId`.</span><span class="sxs-lookup"><span data-stu-id="69b54-153">Change hello Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="69b54-154">Щелкните «Выполнить запрос» tooset значения смарт-блокировки вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="69b54-154">Click "Run Query" tooset your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="69b54-155">Если вы не используете их, можно оставить hello **BannedPasswordList** и **EnableBannedPasswordCheck** как пустые значения ("») и «false» соответственно.</span><span class="sxs-lookup"><span data-stu-id="69b54-155">If you are not using them, you can leave hello **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="69b54-156">Убедитесь, что параметры смарт-блокировки клиента установлены, выполнив [следующие действия](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="69b54-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="69b54-157">Обновление параметров смарт-блокировки</span><span class="sxs-lookup"><span data-stu-id="69b54-157">Update Smart Lockout values</span></span>

<span data-ttu-id="69b54-158">Выполните эти шаги tooupdate значения смарт-блокировки вашего клиента (Если вы уже задали их перед).</span><span class="sxs-lookup"><span data-stu-id="69b54-158">Follow these steps tooupdate your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="69b54-159">Войдите в Graph Explorer как глобальный администратор клиента.</span><span class="sxs-lookup"><span data-stu-id="69b54-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="69b54-160">Если будет предложено, предоставление доступа для hello запрашиваемые разрешения на доступ.</span><span class="sxs-lookup"><span data-stu-id="69b54-160">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="69b54-161">Щелкните «Изменить разрешения» и выберите разрешение «Directory.ReadWrite.All» hello.</span><span class="sxs-lookup"><span data-stu-id="69b54-161">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="69b54-162">[Выполните эти шаги tooread значения смарт-блокировки вашего клиента](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="69b54-162">[Follow these steps tooread your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="69b54-163">Копировать hello `id` значение (GUID) для элемента hello с «displayName» как «PasswordRuleSettings».</span><span class="sxs-lookup"><span data-stu-id="69b54-163">Copy hello `id` value (a GUID) of hello item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="69b54-164">Настройте запрос Graph API hello следующим образом: установить версию слишком «Бета» тип запроса слишком «Исправление» и URL-адрес слишком`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -использовать hello GUID с шага 3 для `<id>`.</span><span class="sxs-lookup"><span data-stu-id="69b54-164">Configure hello Graph API request as follows: Set version too“BETA”, request type too“PATCH” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use hello GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="69b54-165">Скопируйте и вставьте после запроса JSON в поле «Текст запроса» hello hello.</span><span class="sxs-lookup"><span data-stu-id="69b54-165">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="69b54-166">Измените значения смарт-блокировки hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="69b54-166">Change hello Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="69b54-167">Щелкните «Выполнить запрос» tooupdate значения смарт-блокировки вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="69b54-167">Click "Run Query" tooupdate your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="69b54-168">Убедитесь, что параметры смарт-блокировки клиента были обновлены, выполнив [следующие действия](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="69b54-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="69b54-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69b54-169">Next steps</span></span>
- <span data-ttu-id="69b54-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.</span><span class="sxs-lookup"><span data-stu-id="69b54-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
