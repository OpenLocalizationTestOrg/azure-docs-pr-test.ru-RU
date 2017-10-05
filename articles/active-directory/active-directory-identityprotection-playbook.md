---
title: "Тренировочное задание по защите идентификации Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как защита идентификации Azure AD позволяет помешать злоумышленникам воспользоваться скомпрометированными удостоверениями и устройствами, а также защитить удостоверение или устройство, которое ранее предположительно или фактически скомпрометировано."
services: active-directory
keywords: "защита удостоверений Azure Active Directory, Cloud App Discovery, управление приложениями, безопасность, риск, уровень риска, уязвимость, политика безопасности"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 2ecd07faed785fa6aa179ac1cca35a70d965e1dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="839a1-104">Тренировочное задание по защите идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="839a1-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="839a1-105">Это тренировочное задание поможет:</span><span class="sxs-lookup"><span data-stu-id="839a1-105">This playbook helps you to:</span></span>

* <span data-ttu-id="839a1-106">заполнить данными среду защиты идентификации, моделируя события рисков и уязвимости;</span><span class="sxs-lookup"><span data-stu-id="839a1-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="839a1-107">настроить политики условного доступа на основе рисков и проверить воздействие этих политик.</span><span class="sxs-lookup"><span data-stu-id="839a1-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="839a1-108">Моделирование событий риска</span><span class="sxs-lookup"><span data-stu-id="839a1-108">Simulating Risk Events</span></span>
<span data-ttu-id="839a1-109">В этом разделе поэтапно описано моделирование событий риска следующих типов:</span><span class="sxs-lookup"><span data-stu-id="839a1-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="839a1-110">попытки входа с анонимных IP-адресов (простое моделирование);</span><span class="sxs-lookup"><span data-stu-id="839a1-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="839a1-111">попытки входа из неизвестных расположений (моделирование средней сложности);</span><span class="sxs-lookup"><span data-stu-id="839a1-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="839a1-112">невозможно переместиться в нетипичные расположения (сложное моделирование).</span><span class="sxs-lookup"><span data-stu-id="839a1-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="839a1-113">Другие события риска нельзя моделировать без угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="839a1-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="839a1-114">Попытки входа с анонимных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="839a1-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="839a1-115">События риска этого типа означают, что пользователь успешно вошел, используя IP-адрес, определенный как IP-адрес анонимного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="839a1-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="839a1-116">Эти прокси-серверы используют пользователи, желающие скрыть IP-адреса своих устройств. Иногда их используют злоумышленники.</span><span class="sxs-lookup"><span data-stu-id="839a1-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="839a1-117">**Чтобы смоделировать вход с использованием анонимного IP-адреса, выполните следующее**.</span><span class="sxs-lookup"><span data-stu-id="839a1-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="839a1-118">Скачайте [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="839a1-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="839a1-119">В браузере Tor Browser перейдите по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="839a1-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="839a1-120">Введите учетные данные учетной записи, которую нужно использовать в отчете **Попытки входа с анонимных IP-адресов** .</span><span class="sxs-lookup"><span data-stu-id="839a1-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="839a1-121">Информация о входе появится на панели мониторинга защиты идентификации в течение 5 минут.</span><span class="sxs-lookup"><span data-stu-id="839a1-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="839a1-122">Попытки входа из неизвестных расположений</span><span class="sxs-lookup"><span data-stu-id="839a1-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="839a1-123">Для определения риска входа из неизвестных расположений используется механизм оценки данных входа в реальном времени. Он сравнивает расположение с предыдущими расположениями (IP-адресом, широтой, долготой и ASN), чтобы выявлять новые или незнакомые расположения.</span><span class="sxs-lookup"><span data-stu-id="839a1-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="839a1-124">Система хранит предыдущие IP-адреса, сведения о широте, долготе и ASN, а также учитывает их в качестве сведений о знакомых расположениях.</span><span class="sxs-lookup"><span data-stu-id="839a1-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span></span> <span data-ttu-id="839a1-125">Расположения входа считаются незнакомыми, если они не соответствуют существующим знакомым расположениям.</span><span class="sxs-lookup"><span data-stu-id="839a1-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span></span>

<span data-ttu-id="839a1-126">Защита идентификации Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="839a1-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="839a1-127">предусматривает первоначальный период обучения — 14 дней, в течение которых она не отмечает новые расположения в качестве незнакомых.</span><span class="sxs-lookup"><span data-stu-id="839a1-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="839a1-128">игнорирует вход с помощью знакомых устройств и из расположений, географически близких к знакомому.</span><span class="sxs-lookup"><span data-stu-id="839a1-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span></span>

<span data-ttu-id="839a1-129">Чтобы смоделировать вход из незнакомого расположения, нужно использовать расположение и устройство, которые ранее не использовались для входа с учетной записью.</span><span class="sxs-lookup"><span data-stu-id="839a1-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span></span> 

<span data-ttu-id="839a1-130">**Чтобы смоделировать вход из незнакомого расположения, выполните следующее**.</span><span class="sxs-lookup"><span data-stu-id="839a1-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="839a1-131">Выберите учетную запись, в журнале которой есть записи по крайней мере за 14 дней.</span><span class="sxs-lookup"><span data-stu-id="839a1-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="839a1-132">Выполните одно из двух:</span><span class="sxs-lookup"><span data-stu-id="839a1-132">Do either:</span></span>
   
   <span data-ttu-id="839a1-133">а.</span><span class="sxs-lookup"><span data-stu-id="839a1-133">a.</span></span> <span data-ttu-id="839a1-134">Если вы используете VPN, перейдите по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com) и введите данные учетной записи, для которой необходимо смоделировать событие риска.</span><span class="sxs-lookup"><span data-stu-id="839a1-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span></span>
   
   <span data-ttu-id="839a1-135">b.</span><span class="sxs-lookup"><span data-stu-id="839a1-135">b.</span></span> <span data-ttu-id="839a1-136">Попросите пользователя в другом расположении использовать соответствующие данные для входа в учетную запись (не рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="839a1-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span></span>

<span data-ttu-id="839a1-137">Информация о входе появится на панели мониторинга защиты идентификации в течение 5 минут.</span><span class="sxs-lookup"><span data-stu-id="839a1-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="839a1-138">Невозможно переместиться в нетипичное расположение</span><span class="sxs-lookup"><span data-stu-id="839a1-138">Impossible travel to atypical location</span></span>
<span data-ttu-id="839a1-139">Моделирование условия невозможности перемещения — достаточно сложная задача, так как соответствующий алгоритм использует машинное обучение, чтобы отсеять ложные срабатывания, например, когда невозможно переместиться и используется знакомое устройство или вход выполнен из VPN, которую используют другие пользователи в каталоге.</span><span class="sxs-lookup"><span data-stu-id="839a1-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="839a1-140">Кроме того, для работы алгоритма требуется, чтобы у пользователя была история входов за период 3–14 дней. Это позволит начать создавать события риска.</span><span class="sxs-lookup"><span data-stu-id="839a1-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span></span>

<span data-ttu-id="839a1-141">**Чтобы смоделировать невозможность перемещения в типичное расположение, выполните следующее**.</span><span class="sxs-lookup"><span data-stu-id="839a1-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="839a1-142">В стандартном браузере перейдите по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="839a1-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="839a1-143">Введите данные учетной записи, для которой вы хотите создать событие риска невозможности перемещения.</span><span class="sxs-lookup"><span data-stu-id="839a1-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="839a1-144">Измените агент пользователя.</span><span class="sxs-lookup"><span data-stu-id="839a1-144">Change your user agent.</span></span> <span data-ttu-id="839a1-145">Его можно изменить в Internet Explorer с помощью средств разработчика, а также в Firefox или Chrome с помощью надстройки переключателя между агентом и пользователем.</span><span class="sxs-lookup"><span data-stu-id="839a1-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="839a1-146">Измените свой IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="839a1-146">Change your IP address.</span></span> <span data-ttu-id="839a1-147">Его можно изменить, используя VPN, надстройку Tor или запустив новый компьютер Azure в другом центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="839a1-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="839a1-148">Перейдите по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com) , введите те же учетные данные, что и при предыдущем входе, а затем, спустя несколько минут с последнего, входа войдите в учетную запись.</span><span class="sxs-lookup"><span data-stu-id="839a1-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="839a1-149">Информация о входе появится на панели мониторинга защиты идентификации в течение 2–4 часов.</span><span class="sxs-lookup"><span data-stu-id="839a1-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="839a1-150">Из-за использования сложных моделей машинного обучения существует вероятность того, что она не отобразится.</span><span class="sxs-lookup"><span data-stu-id="839a1-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="839a1-151">Возможно, вам потребуется выполнить эти шаги для нескольких учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="839a1-151">You might want to replicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="839a1-152">Моделирование уязвимостей</span><span class="sxs-lookup"><span data-stu-id="839a1-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="839a1-153">Уязвимости — это слабые стороны среды Azure AD, которыми могут воспользоваться злоумышленники.</span><span class="sxs-lookup"><span data-stu-id="839a1-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="839a1-154">Сейчас защита идентификации Azure AD поддерживает три типа уязвимостей, которые используют другие функции Azure AD.</span><span class="sxs-lookup"><span data-stu-id="839a1-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="839a1-155">Эти уязвимости будут автоматически отображаться на панели мониторинга защиты идентификации после настройки данных функций:</span><span class="sxs-lookup"><span data-stu-id="839a1-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="839a1-156">Azure AD [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="839a1-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="839a1-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md);</span><span class="sxs-lookup"><span data-stu-id="839a1-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="839a1-158">[управление привилегированными пользователями](active-directory-privileged-identity-management-configure.md)Azure AD.</span><span class="sxs-lookup"><span data-stu-id="839a1-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="839a1-159">Риск компрометации пользователя</span><span class="sxs-lookup"><span data-stu-id="839a1-159">User compromise risk</span></span>
<span data-ttu-id="839a1-160">**Чтобы тестировать риск компрометации пользователя, выполните следующее**.</span><span class="sxs-lookup"><span data-stu-id="839a1-160">**To test User compromise risk, perform the following steps**:</span></span>

1. <span data-ttu-id="839a1-161">Войдите на портал по адресу [https://portal.azure.com](https://portal.azure.com) , используя учетные данные глобального администратора для клиента.</span><span class="sxs-lookup"><span data-stu-id="839a1-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="839a1-162">Перейдите к **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="839a1-162">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="839a1-163">В главной колонке **Azure AD Identity Protection** щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="839a1-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="839a1-164">В колонке **Параметры портала** в разделе **Правила безопасности** щелкните **User compromise risk** (Риск компрометации пользователя).</span><span class="sxs-lookup"><span data-stu-id="839a1-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="839a1-165">В колонке **Риск при входе** установите переключатель **Включить правило** в выключенное положение и нажмите кнопку **Сохранить**, чтобы сохранить параметры.</span><span class="sxs-lookup"><span data-stu-id="839a1-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="839a1-166">Смоделируйте событие риска неизвестного расположения или использования анонимного IP-адреса для указанной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="839a1-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="839a1-167">Это повысит риск для заданного пользователя до уровня **Средний**.</span><span class="sxs-lookup"><span data-stu-id="839a1-167">This will elevate the user risk level for that user to **Medium**.</span></span>
7. <span data-ttu-id="839a1-168">Подождите несколько минут и убедитесь, что для пользователя отображается уровень **Средний**.</span><span class="sxs-lookup"><span data-stu-id="839a1-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="839a1-169">Перейдите к колонке **Параметры портала** .</span><span class="sxs-lookup"><span data-stu-id="839a1-169">Go to the **Portal Settings** blade.</span></span>
9. <span data-ttu-id="839a1-170">В колонке **User Compromise Risk** (Риск компрометации пользователя) установите переключатель **Включить правило** в положение **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="839a1-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="839a1-171">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="839a1-171">Select one of the following options:</span></span>
    
    <span data-ttu-id="839a1-172">а.</span><span class="sxs-lookup"><span data-stu-id="839a1-172">a.</span></span> <span data-ttu-id="839a1-173">Чтобы заблокировать вход, установите переключатель **Заблокировать вход** в положение **Средний**.</span><span class="sxs-lookup"><span data-stu-id="839a1-173">To block, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="839a1-174">b.</span><span class="sxs-lookup"><span data-stu-id="839a1-174">b.</span></span> <span data-ttu-id="839a1-175">Чтобы принудительно применять изменение пароля, установите переключатель **Требовать многофакторную проверку подлинности** в положение **Средний**.</span><span class="sxs-lookup"><span data-stu-id="839a1-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="839a1-176">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="839a1-176">Click **Save**.</span></span>
12. <span data-ttu-id="839a1-177">Теперь можно протестировать условный доступ на основе рисков. Для этого войдите в учетную запись, используя данные пользователя с уровнем риска, который вы повысили.</span><span class="sxs-lookup"><span data-stu-id="839a1-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="839a1-178">Если у пользователя уровень риска "Средний", то, в зависимости от настроенной политики, вход будет заблокирован или пароль будет принудительно изменен.</span><span class="sxs-lookup"><span data-stu-id="839a1-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span></span> 
    <br><br><span data-ttu-id="839a1-179">
    ![Репертуара](./media/active-directory-identityprotection-playbook/201.png "репертуара")
    </span><span class="sxs-lookup"><span data-stu-id="839a1-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="839a1-180">Риск при входе</span><span class="sxs-lookup"><span data-stu-id="839a1-180">Sign-in risk</span></span>
<span data-ttu-id="839a1-181">**Чтобы протестировать риск при входе, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="839a1-181">**To test a sign in risk, perform the following steps:**</span></span>

1. <span data-ttu-id="839a1-182">Войдите на портал по адресу [https://portal.azure.com ](https://portal.azure.com) , используя учетные данные глобального администратора для клиента.</span><span class="sxs-lookup"><span data-stu-id="839a1-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="839a1-183">Перейдите к **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="839a1-183">Navigate to **Identity Protection**.</span></span>
3. <span data-ttu-id="839a1-184">В главной колонке **Azure AD Identity Protection** щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="839a1-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="839a1-185">В колонке **Параметры портала** в разделе **Правила безопасности** щелкните **Риск при входе**.</span><span class="sxs-lookup"><span data-stu-id="839a1-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="839a1-186">На ** вход риск ** колонке выберите **на** под **включить правило**.</span><span class="sxs-lookup"><span data-stu-id="839a1-186">On the **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="839a1-187">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="839a1-187">Select one of the following options:</span></span>
   
   <span data-ttu-id="839a1-188">а.</span><span class="sxs-lookup"><span data-stu-id="839a1-188">a.</span></span> <span data-ttu-id="839a1-189">Чтобы заблокировать вход, установите переключатель **Заблокировать вход** в положение **Средний**.</span><span class="sxs-lookup"><span data-stu-id="839a1-189">To block, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="839a1-190">b.</span><span class="sxs-lookup"><span data-stu-id="839a1-190">b.</span></span> <span data-ttu-id="839a1-191">Чтобы принудительно применять изменение пароля, установите переключатель **Требовать многофакторную проверку подлинности** в положение **Средний**.</span><span class="sxs-lookup"><span data-stu-id="839a1-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="839a1-192">Чтобы заблокировать вход, установите положение "Средний" для переключателя "Блокировать вход".</span><span class="sxs-lookup"><span data-stu-id="839a1-192">To block, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="839a1-193">Чтобы принудительно применять Многофакторную идентификацию, установите переключатель **Требовать многофакторную проверку подлинности** в положение **Средний**.</span><span class="sxs-lookup"><span data-stu-id="839a1-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="839a1-194">Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="839a1-194">Click on **Save**.</span></span>
10. <span data-ttu-id="839a1-195">Теперь можно протестировать условный доступ на основе рисков. Для этого смоделируйте событие риска незнакомого расположения или использования анонимного IP-адреса, так как они считаются событиями с уровнем риска **Средний**.</span><span class="sxs-lookup"><span data-stu-id="839a1-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="839a1-196">![Сборник тренировочных заданий](./media/active-directory-identityprotection-playbook/200.png "Сборник тренировочных заданий")</span><span class="sxs-lookup"><span data-stu-id="839a1-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="839a1-197">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="839a1-197">See also</span></span>
* [<span data-ttu-id="839a1-198">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="839a1-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

