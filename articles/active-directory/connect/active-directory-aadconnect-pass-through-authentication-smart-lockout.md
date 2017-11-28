---
title: "Сквозная проверка подлинности в Azure AD Connect — смарт-блокировка | Документы Майкрософт"
description: "В этой статье описано, как сквозная проверка подлинности Azure Active Directory (Azure AD) позволяет защитить локальные учетные записи от атак методом подбора пароля в облаке."
services: active-directory
keywords: "Сквозная аутентификация Azure AD Connect, установка Active Directory, необходимые компоненты для Azure AD, единый вход"
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
ms.openlocfilehash: c84b2406e6373701c83c509342129bd6d7d4034b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="70aac-104">Сквозная проверка подлинности Azure Active Directory: смарт-блокировка</span><span class="sxs-lookup"><span data-stu-id="70aac-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="70aac-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="70aac-105">Overview</span></span>

<span data-ttu-id="70aac-106">Azure AD обеспечивает защиту от атак методом подбора пароля и позволяет предотвратить потерю доступа пользователей к приложениям Office 365 и SaaS.</span><span class="sxs-lookup"><span data-stu-id="70aac-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="70aac-107">Эта функция, которая называется **смарт-блокировкой**, поддерживается при входе с помощью сквозной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="70aac-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="70aac-108">По умолчанию смарт-блокировка включена для всех клиентов и постоянно защищает учетные записи пользователей; включать ее отдельно не требуется.</span><span class="sxs-lookup"><span data-stu-id="70aac-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all the time; there is no need to turn it on.</span></span>

<span data-ttu-id="70aac-109">Смарт-блокировка отслеживает неудачные попытки входа в систему и по достижении определенного **порогового значения блокировки** включает блокировку в течение заданного **периода блокировки**.</span><span class="sxs-lookup"><span data-stu-id="70aac-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="70aac-110">Все попытки входа злоумышленника в течение периода блокировки отклоняются.</span><span class="sxs-lookup"><span data-stu-id="70aac-110">Any sign-in attempts from the attacker during the Lockout Duration are rejected.</span></span> <span data-ttu-id="70aac-111">Если атака продолжается, то последующие неудачные попытки входа приводят к увеличению периода блокировки.</span><span class="sxs-lookup"><span data-stu-id="70aac-111">If the attack continues, the subsequent failed sign-in attempts after the Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="70aac-112">Пороговое значение блокировки по умолчанию — 10 неудачных попыток входа, а период блокировки по умолчанию — 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="70aac-112">The default Lockout Threshold is 10 failed attempts, and the default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="70aac-113">Смарт-блокировка также различает попытки входа настоящих пользователей и попытки входа злоумышленников и в большинстве случаев блокирует только попытки входа злоумышленников.</span><span class="sxs-lookup"><span data-stu-id="70aac-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out the attackers in most cases.</span></span> <span data-ttu-id="70aac-114">Это не позволяет злоумышленникам намеренно заблокировать вход для настоящих пользователей.</span><span class="sxs-lookup"><span data-stu-id="70aac-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="70aac-115">Чтобы различить настоящих пользователей и злоумышленников, мы используем данные о поведении в предыдущих попытках входа, сведения об устройствах и браузерах пользователей и другие сигналы.</span><span class="sxs-lookup"><span data-stu-id="70aac-115">We use past sign-in behavior, users’ devices & browsers and other signals to distinguish between genuine users and attackers.</span></span> <span data-ttu-id="70aac-116">Мы постоянно улучшаем наши алгоритмы.</span><span class="sxs-lookup"><span data-stu-id="70aac-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="70aac-117">Поскольку сквозная проверка подлинности перенаправляет запросы на проверку пароля в локальный каталог Active Directory (AD), необходимо предотвратить блокировку учетных записей пользователей AD злоумышленниками.</span><span class="sxs-lookup"><span data-stu-id="70aac-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need to prevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="70aac-118">Так как у вас есть собственные политики блокировки учетных записей AD (в частности, [**пороговое значение блокировки**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) и [**политики сброса счетчика блокировки учетных записей**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), необходимо настроить пороговое значение блокировки Azure AD и период блокировки, так чтобы отфильтровать атаки в облаке, прежде чем они достигнут локального каталога AD.</span><span class="sxs-lookup"><span data-stu-id="70aac-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need to configure Azure AD’s Lockout Threshold and Lockout Duration values appropriately to filter out attacks in the cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="70aac-119">Функция смарт-блокировки предоставляется бесплатно. Она _включена_ по умолчанию для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="70aac-119">The Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="70aac-120">Однако для изменения порогового значения блокировки и периода блокировки с помощью API Graph Azure AD клиенту требуется как минимум одна лицензия Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="70aac-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant to have at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="70aac-121">Чтобы получить возможность смарт-блокировки с помощью сквозной аутентификации, не требуется лицензия Azure AD Premium P2 для _каждого пользователя_.</span><span class="sxs-lookup"><span data-stu-id="70aac-121">You don't need an Azure AD Premium P2 license _per user_ to get the Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="70aac-122">Чтобы убедиться, что локальные учетные записи пользователей AD защищены, необходимо убедиться в следующем:</span><span class="sxs-lookup"><span data-stu-id="70aac-122">To ensure that your users’ on-premises AD accounts are well protected, you need to ensure that:</span></span>

1.  <span data-ttu-id="70aac-123">Пороговое значение блокировки Azure AD _меньше_, чем пороговое значение блокировки учетных записей AD.</span><span class="sxs-lookup"><span data-stu-id="70aac-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="70aac-124">Рекомендуется устанавливать значения таким образом, чтобы пороговое значение блокировки учетных записей AD как минимум в два-три раза превышало пороговое значение блокировки Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70aac-124">We recommend that you set the values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="70aac-125">Продолжительность блокировки Azure AD (в секундах) _больше_, чем период сброса счетчика блокировки учетных записей AD (в минутах).</span><span class="sxs-lookup"><span data-stu-id="70aac-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="70aac-126">Проверка политик блокировки учетных записей AD</span><span class="sxs-lookup"><span data-stu-id="70aac-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="70aac-127">Чтобы проверить политики блокировки учетных записей AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="70aac-127">Use the following instructions to verify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="70aac-128">Откройте средства управления групповыми политиками.</span><span class="sxs-lookup"><span data-stu-id="70aac-128">Open the Group Policy Management tool.</span></span>
2.  <span data-ttu-id="70aac-129">Измените групповую политику, которая применяется ко всем пользователям, например политику домена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="70aac-129">Edit the group policy that is applied to all users, for example, the Default Domain Policy.</span></span>
3.  <span data-ttu-id="70aac-130">Перейдите в раздел "Конфигурация компьютера\Политики\Параметры Windows\Параметры безопасности\Политики учетных записей\Политика блокировки учетных записей".</span><span class="sxs-lookup"><span data-stu-id="70aac-130">Navigate to Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="70aac-131">Проверьте пороговое значение блокировки учетных записей и период сброса счетчика блокировки учетных записей.</span><span class="sxs-lookup"><span data-stu-id="70aac-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Политики блокировки учетных записей AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-the-graph-api-to-manage-your-tenants-smart-lockout-values"></a><span data-ttu-id="70aac-133">Управление параметрами смарт-блокировки значения вашего клиента с помощью API Graph</span><span class="sxs-lookup"><span data-stu-id="70aac-133">Use the Graph API to manage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="70aac-134">Изменение порогового значения блокировки и периода блокировки с помощью API Graph Azure AD — это функция Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="70aac-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="70aac-135">Для использования этой функции вы также должны быть глобальным администратором клиента.</span><span class="sxs-lookup"><span data-stu-id="70aac-135">It also needs you to be a Global Administrator on your tenant.</span></span>

<span data-ttu-id="70aac-136">Для просмотра, установки и обновления параметров смарт-блокировки Azure AD можно использовать [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).</span><span class="sxs-lookup"><span data-stu-id="70aac-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to read, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="70aac-137">Однако эти операции можно также выполнить программными средствами.</span><span class="sxs-lookup"><span data-stu-id="70aac-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="70aac-138">Считывание параметров смарт-блокировки</span><span class="sxs-lookup"><span data-stu-id="70aac-138">Read Smart Lockout values</span></span>

<span data-ttu-id="70aac-139">Для считывания параметров смарт-блокировки вашего клиента выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="70aac-139">Follow these steps to read your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="70aac-140">Войдите в Graph Explorer как глобальный администратор клиента.</span><span class="sxs-lookup"><span data-stu-id="70aac-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="70aac-141">При необходимости предоставьте доступ для запрошенных разрешений.</span><span class="sxs-lookup"><span data-stu-id="70aac-141">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="70aac-142">Нажмите кнопку "Изменить разрешения" и выберите разрешение "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="70aac-142">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="70aac-143">Настройте запрос к API Graph следующим образом: установите версию в "BETA", тип запроса — в "GET" и URL-адрес в `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="70aac-143">Configure the Graph API request as follows: Set version to “BETA”, request type to “GET” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="70aac-144">Нажмите кнопку "Выполнить запрос" для просмотра параметров смарт-блокировки вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="70aac-144">Click "Run Query" to see your tenant's Smart Lockout values.</span></span> <span data-ttu-id="70aac-145">Если вы не устанавливали значений параметров клиента, вы увидите пустой набор параметров.</span><span class="sxs-lookup"><span data-stu-id="70aac-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="70aac-146">Установка параметров смарт-блокировки</span><span class="sxs-lookup"><span data-stu-id="70aac-146">Set Smart Lockout values</span></span>

<span data-ttu-id="70aac-147">Для установки параметров смарт-блокировки клиента (только в первый раз) выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="70aac-147">Follow these steps to set your tenant’s Smart Lockout values (for the first time only):</span></span>

1. <span data-ttu-id="70aac-148">Войдите в Graph Explorer как глобальный администратор клиента.</span><span class="sxs-lookup"><span data-stu-id="70aac-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="70aac-149">При необходимости предоставьте доступ для запрошенных разрешений.</span><span class="sxs-lookup"><span data-stu-id="70aac-149">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="70aac-150">Нажмите кнопку "Изменить разрешения" и выберите разрешение "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="70aac-150">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="70aac-151">Настройте запрос к API Graph следующим образом: установите версию в "BETA", тип запроса — в "POST" и URL-адрес в `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="70aac-151">Configure the Graph API request as follows: Set version to “BETA”, request type to “POST” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="70aac-152">Скопируйте и вставьте следующий запрос JSON в поле "Текст запроса".</span><span class="sxs-lookup"><span data-stu-id="70aac-152">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="70aac-153">Измените параметры смарт-блокировки соответствующим образом и используйте случайный идентификатор GUID в качестве `templateId`.</span><span class="sxs-lookup"><span data-stu-id="70aac-153">Change the Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="70aac-154">Нажмите кнопку "Выполнить запрос" для просмотра параметров смарт-блокировки вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="70aac-154">Click "Run Query" to set your tenant's Smart Lockout values.</span></span>

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
><span data-ttu-id="70aac-155">Если вы не используете параметры **BannedPasswordList** и **EnableBannedPasswordCheck**, можно оставить их значения ("") и "false" соответственно без изменений.</span><span class="sxs-lookup"><span data-stu-id="70aac-155">If you are not using them, you can leave the **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="70aac-156">Убедитесь, что параметры смарт-блокировки клиента установлены, выполнив [следующие действия](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="70aac-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="70aac-157">Обновление параметров смарт-блокировки</span><span class="sxs-lookup"><span data-stu-id="70aac-157">Update Smart Lockout values</span></span>

<span data-ttu-id="70aac-158">Для обновления параметров смарт-блокировки клиента (если они были установлены ранее), выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="70aac-158">Follow these steps to update your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="70aac-159">Войдите в Graph Explorer как глобальный администратор клиента.</span><span class="sxs-lookup"><span data-stu-id="70aac-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="70aac-160">При необходимости предоставьте доступ для запрошенных разрешений.</span><span class="sxs-lookup"><span data-stu-id="70aac-160">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="70aac-161">Нажмите кнопку "Изменить разрешения" и выберите разрешение "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="70aac-161">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="70aac-162">[Для считывания параметров смарт-блокировки вашего клиента выполните следующие действия](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="70aac-162">[Follow these steps to read your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="70aac-163">Скопируйте значение `id` (GUID) элемента с отображаемым именем ("displayName") "PasswordRuleSettings".</span><span class="sxs-lookup"><span data-stu-id="70aac-163">Copy the `id` value (a GUID) of the item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="70aac-164">Настройте запрос к API Graph следующим образом: установите версию в "BETA", тип запроса — в "PATCH" и URL-адрес в `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` — в качестве `<id>` используйте значение GUID из шага 3.</span><span class="sxs-lookup"><span data-stu-id="70aac-164">Configure the Graph API request as follows: Set version to “BETA”, request type to “PATCH” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use the GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="70aac-165">Скопируйте и вставьте следующий запрос JSON в поле "Текст запроса".</span><span class="sxs-lookup"><span data-stu-id="70aac-165">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="70aac-166">Измените параметры смарт-блокировки соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="70aac-166">Change the Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="70aac-167">Нажмите кнопку "Выполнить запрос" для обновления параметров смарт-блокировки вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="70aac-167">Click "Run Query" to update your tenant's Smart Lockout values.</span></span>

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

<span data-ttu-id="70aac-168">Убедитесь, что параметры смарт-блокировки клиента были обновлены, выполнив [следующие действия](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="70aac-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70aac-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70aac-169">Next steps</span></span>
- <span data-ttu-id="70aac-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.</span><span class="sxs-lookup"><span data-stu-id="70aac-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
