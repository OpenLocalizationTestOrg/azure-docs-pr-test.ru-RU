---
title: "Active Directory Identity Protection репертуара aaaAzure | Документы Microsoft"
description: "Узнайте, как Azure AD Identity Protection делает возможность hello toolimit злоумышленник tooexploit скомпрометированных удостоверения или устройство и toosecure удостоверения или устройства, который ранее был toobe подозреваемое или известных скомпрометирован."
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
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="e0990-104">Тренировочное задание по защите идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0990-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="e0990-105">Это тренировочное задание поможет:</span><span class="sxs-lookup"><span data-stu-id="e0990-105">This playbook helps you to:</span></span>

* <span data-ttu-id="e0990-106">Заполнение данных в среде защиты идентификации hello, имитация события рисков и уязвимостей</span><span class="sxs-lookup"><span data-stu-id="e0990-106">Populate data in hello Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="e0990-107">Настройка политики условного доступа на основе рисков и проверка hello влияние этих политик</span><span class="sxs-lookup"><span data-stu-id="e0990-107">Set up risk-based conditional access policies and test hello impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="e0990-108">Моделирование событий риска</span><span class="sxs-lookup"><span data-stu-id="e0990-108">Simulating Risk Events</span></span>
<span data-ttu-id="e0990-109">В этом разделе приводятся шаги для имитации hello следующие типы событий риска:</span><span class="sxs-lookup"><span data-stu-id="e0990-109">This section provides you with steps for simulating hello following risk event types:</span></span>

* <span data-ttu-id="e0990-110">попытки входа с анонимных IP-адресов (простое моделирование);</span><span class="sxs-lookup"><span data-stu-id="e0990-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="e0990-111">попытки входа из неизвестных расположений (моделирование средней сложности);</span><span class="sxs-lookup"><span data-stu-id="e0990-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="e0990-112">Невозможно tooatypical местоположений (сложно)</span><span class="sxs-lookup"><span data-stu-id="e0990-112">Impossible travel tooatypical locations (difficult)</span></span>

<span data-ttu-id="e0990-113">Другие события риска нельзя моделировать без угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="e0990-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="e0990-114">Попытки входа с анонимных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="e0990-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="e0990-115">События риска этого типа означают, что пользователь успешно вошел, используя IP-адрес, определенный как IP-адрес анонимного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="e0990-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="e0990-116">Эти учетные записи-посредники, используемые пользователями, которые хотите toohide IP-адрес своего устройства и могут быть использованы злоумышленниками.</span><span class="sxs-lookup"><span data-stu-id="e0990-116">These proxies are used by people who want toohide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="e0990-117">**toosimulate входа в с анонимных IP-адреса выполнить следующие шаги hello**:</span><span class="sxs-lookup"><span data-stu-id="e0990-117">**toosimulate a sign-in from an anonymous IP, perform hello following steps**:</span></span>

1. <span data-ttu-id="e0990-118">Загрузите hello [Tor браузера](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="e0990-118">Download hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="e0990-119">С помощью обозревателя Tor hello перейдите слишком[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e0990-119">Using hello Tor Browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="e0990-120">Введите учетные данные hello hello счета, tooappear в hello **попытки входа с анонимных IP-адресов** отчета.</span><span class="sxs-lookup"><span data-stu-id="e0990-120">Enter hello credentials of hello account you want tooappear in hello **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="e0990-121">вход Hello будут отображаться на панели мониторинга hello защиту учетных данных в течение 5 минут.</span><span class="sxs-lookup"><span data-stu-id="e0990-121">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="e0990-122">Попытки входа из неизвестных расположений</span><span class="sxs-lookup"><span data-stu-id="e0990-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="e0990-123">Hello риск незнакомых расположений — это в режиме реального времени оценки механизм, считает, что после входа в расположениях (IP, широты и долготы и ASN) toodetermine новый / незнакомых расположений.</span><span class="sxs-lookup"><span data-stu-id="e0990-123">hello unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="e0990-124">Hello система хранит предыдущего IP-адреса, широты и долготы и ASN пользователя и рассматривает эти расположения знакомый toobe.</span><span class="sxs-lookup"><span data-stu-id="e0990-124">hello system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these toobe familiar locations.</span></span> <span data-ttu-id="e0990-125">Местоположения входа считается знакомы, если hello местоположения входа не соответствует ни hello существующие знакомые расположений.</span><span class="sxs-lookup"><span data-stu-id="e0990-125">A sign-in location is considered unfamiliar if hello sign-in location does not match any of hello existing familiar locations.</span></span>

<span data-ttu-id="e0990-126">Защита идентификации Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="e0990-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="e0990-127">предусматривает первоначальный период обучения — 14 дней, в течение которых она не отмечает новые расположения в качестве незнакомых.</span><span class="sxs-lookup"><span data-stu-id="e0990-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="e0990-128">игнорирует входы из знакомых устройства и расположения, территориально закрыть tooan существующий путь.</span><span class="sxs-lookup"><span data-stu-id="e0990-128">ignores sign-ins from familiar devices and locations that are geographically close tooan existing familiar location.</span></span>

<span data-ttu-id="e0990-129">toosimulate незнакомых расположений, у вас toosign в из расположения и устройство, которое hello учетной записи не входил в систему с до.</span><span class="sxs-lookup"><span data-stu-id="e0990-129">toosimulate unfamiliar locations, you have toosign in from a location and device that hello account has not signed in from before.</span></span> 

<span data-ttu-id="e0990-130">**toosimulate вход из незнакомых расположения, выполнить следующие шаги hello**:</span><span class="sxs-lookup"><span data-stu-id="e0990-130">**toosimulate a sign-in from an unfamiliar location, perform hello following steps**:</span></span>

1. <span data-ttu-id="e0990-131">Выберите учетную запись, в журнале которой есть записи по крайней мере за 14 дней.</span><span class="sxs-lookup"><span data-stu-id="e0990-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="e0990-132">Выполните одно из двух:</span><span class="sxs-lookup"><span data-stu-id="e0990-132">Do either:</span></span>
   
   <span data-ttu-id="e0990-133">а.</span><span class="sxs-lookup"><span data-stu-id="e0990-133">a.</span></span> <span data-ttu-id="e0990-134">При использовании виртуальной частной сети, перейдите слишком[https://myapps.microsoft.com](https://myapps.microsoft.com) и введите учетные данные hello hello счета, риск событие toosimulate hello.</span><span class="sxs-lookup"><span data-stu-id="e0990-134">While using a VPN, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com) and enter hello credentials of hello account you want toosimulate hello risk event for.</span></span>
   
   <span data-ttu-id="e0990-135">b.</span><span class="sxs-lookup"><span data-stu-id="e0990-135">b.</span></span> <span data-ttu-id="e0990-136">Попросите коллеге в другое расположение toosign в с использованием учетных данных учетной записи hello (не рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="e0990-136">Ask an associate in a different location toosign in using hello account’s credentials (not recommended).</span></span>

<span data-ttu-id="e0990-137">вход Hello будут отображаться на панели мониторинга hello защиту учетных данных в течение 5 минут.</span><span class="sxs-lookup"><span data-stu-id="e0990-137">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-tooatypical-location"></a><span data-ttu-id="e0990-138">Невозможно переместиться tooatypical расположение</span><span class="sxs-lookup"><span data-stu-id="e0990-138">Impossible travel tooatypical location</span></span>
<span data-ttu-id="e0990-139">Имитация условие невозможно переместиться hello сложно, так как использует алгоритм hello tooweed обучения машины out ложных срабатываний, например невозможно переместиться из знакомых устройств или входа в систему из виртуальных частных сетей, которые используются другими пользователями в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="e0990-139">Simulating hello impossible travel condition is difficult because hello algorithm uses machine learning tooweed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in hello directory.</span></span> <span data-ttu-id="e0990-140">Кроме того hello алгоритму журнал 3 дня too14 входа для пользователя hello перед созданием событий риска.</span><span class="sxs-lookup"><span data-stu-id="e0990-140">Additionally, hello algorithm requires a sign-in history of 3 too14 days for hello user before it begins generating risk events.</span></span>

<span data-ttu-id="e0990-141">**toosimulate размещению tooatypical невозможно переместиться выполнить следующие шаги hello**:</span><span class="sxs-lookup"><span data-stu-id="e0990-141">**toosimulate an impossible travel tooatypical location, perform hello following steps**:</span></span>

1. <span data-ttu-id="e0990-142">С помощью стандартных браузер, перейдите в слишком[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e0990-142">Using your standard browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="e0990-143">Введите учетные данные hello hello учетной записи, которую требуется toogenerate событие невозможно переместиться риск для.</span><span class="sxs-lookup"><span data-stu-id="e0990-143">Enter hello credentials of hello account you want toogenerate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="e0990-144">Измените агент пользователя.</span><span class="sxs-lookup"><span data-stu-id="e0990-144">Change your user agent.</span></span> <span data-ttu-id="e0990-145">Его можно изменить в Internet Explorer с помощью средств разработчика, а также в Firefox или Chrome с помощью надстройки переключателя между агентом и пользователем.</span><span class="sxs-lookup"><span data-stu-id="e0990-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="e0990-146">Измените свой IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e0990-146">Change your IP address.</span></span> <span data-ttu-id="e0990-147">Его можно изменить, используя VPN, надстройку Tor или запустив новый компьютер Azure в другом центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="e0990-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="e0990-148">Вход слишком[https://myapps.microsoft.com](https://myapps.microsoft.com) с помощью hello же учетные данные, как до и в течение нескольких минут после hello предыдущего входа в систему.</span><span class="sxs-lookup"><span data-stu-id="e0990-148">Sign-in too[https://myapps.microsoft.com](https://myapps.microsoft.com) using hello same credentials as before and within a few minutes after hello previous sign-in.</span></span>

<span data-ttu-id="e0990-149">вход Hello будут отображаться в панели мониторинга защиты идентификации hello в 2 – 4 часа.</span><span class="sxs-lookup"><span data-stu-id="e0990-149">hello sign-in will show up in hello Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="e0990-150">Из-за hello сложных моделей машинного обучения участвующих есть вероятность, которые не будут извлекаться вверх.</span><span class="sxs-lookup"><span data-stu-id="e0990-150">Because of hello complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="e0990-151">Может потребоваться tooreplicate следующие действия для нескольких учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0990-151">You might want tooreplicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="e0990-152">Моделирование уязвимостей</span><span class="sxs-lookup"><span data-stu-id="e0990-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="e0990-153">Уязвимости — это слабые стороны среды Azure AD, которыми могут воспользоваться злоумышленники.</span><span class="sxs-lookup"><span data-stu-id="e0990-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="e0990-154">Сейчас защита идентификации Azure AD поддерживает три типа уязвимостей, которые используют другие функции Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0990-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="e0990-155">Эти уязвимости отображается на панели мониторинга защиты идентификации hello автоматически после настройки этих функций.</span><span class="sxs-lookup"><span data-stu-id="e0990-155">These Vulnerabilities will be displayed on hello Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="e0990-156">Azure AD [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e0990-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="e0990-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md);</span><span class="sxs-lookup"><span data-stu-id="e0990-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="e0990-158">[управление привилегированными пользователями](active-directory-privileged-identity-management-configure.md)Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0990-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="e0990-159">Риск компрометации пользователя</span><span class="sxs-lookup"><span data-stu-id="e0990-159">User compromise risk</span></span>
<span data-ttu-id="e0990-160">**tootest риск компрометации пользователя, выполните следующие шаги hello**:</span><span class="sxs-lookup"><span data-stu-id="e0990-160">**tootest User compromise risk, perform hello following steps**:</span></span>

1. <span data-ttu-id="e0990-161">Вход слишком[https://portal.azure.com](https://portal.azure.com) с учетными данными глобального администратора для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="e0990-161">Sign-in too[https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="e0990-162">Перейдите в слишком**защиты идентификации**.</span><span class="sxs-lookup"><span data-stu-id="e0990-162">Navigate too**Identity Protection**.</span></span> 
3. <span data-ttu-id="e0990-163">На главном hello **Azure AD Identity Protection** колонка, щелкните **параметры**.</span><span class="sxs-lookup"><span data-stu-id="e0990-163">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="e0990-164">На hello **Параметры портала** колонки в разделе **правила безопасности**, нажмите кнопку **риск компрометации пользователя**.</span><span class="sxs-lookup"><span data-stu-id="e0990-164">On hello **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="e0990-165">На hello **входа риск** колонке включить **включить правило** off, а затем нажмите кнопку **Сохранить** параметры.</span><span class="sxs-lookup"><span data-stu-id="e0990-165">On hello **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="e0990-166">Смоделируйте событие риска неизвестного расположения или использования анонимного IP-адреса для указанной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e0990-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="e0990-167">Это будет повысить уровень риска hello пользователя для этого пользователя слишком**Средний**.</span><span class="sxs-lookup"><span data-stu-id="e0990-167">This will elevate hello user risk level for that user too**Medium**.</span></span>
7. <span data-ttu-id="e0990-168">Подождите несколько минут и убедитесь, что для пользователя отображается уровень **Средний**.</span><span class="sxs-lookup"><span data-stu-id="e0990-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="e0990-169">Go toohello **Параметры портала** колонку.</span><span class="sxs-lookup"><span data-stu-id="e0990-169">Go toohello **Portal Settings** blade.</span></span>
9. <span data-ttu-id="e0990-170">На hello **риск компрометации пользователя** колонки в разделе **включить правило**выберите **на** .</span><span class="sxs-lookup"><span data-stu-id="e0990-170">On hello **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="e0990-171">Выберите один из следующих вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="e0990-171">Select one of hello following options:</span></span>
    
    <span data-ttu-id="e0990-172">а.</span><span class="sxs-lookup"><span data-stu-id="e0990-172">a.</span></span> <span data-ttu-id="e0990-173">tooblock, выберите **Средний** под **входа блока**.</span><span class="sxs-lookup"><span data-stu-id="e0990-173">tooblock, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="e0990-174">b.</span><span class="sxs-lookup"><span data-stu-id="e0990-174">b.</span></span> <span data-ttu-id="e0990-175">Изменение безопасного пароля tooenforce, выберите **Средний** под **требовать многофакторную проверку подлинности**.</span><span class="sxs-lookup"><span data-stu-id="e0990-175">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="e0990-176">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e0990-176">Click **Save**.</span></span>
12. <span data-ttu-id="e0990-177">Теперь можно протестировать условный доступ на основе рисков. Для этого войдите в учетную запись, используя данные пользователя с уровнем риска, который вы повысили.</span><span class="sxs-lookup"><span data-stu-id="e0990-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="e0990-178">Если риск hello пользователя — средний, в зависимости от конфигурации hello политики, вход в систему либо заблокированы или принудительно toochange пароль.</span><span class="sxs-lookup"><span data-stu-id="e0990-178">If hello user risk is Medium, depending on hello configuration of your policy, your sign-in is be either blocked or you are forced toochange your password.</span></span> 
    <br><br><span data-ttu-id="e0990-179">
    ![Репертуара](./media/active-directory-identityprotection-playbook/201.png "репертуара")
    </span><span class="sxs-lookup"><span data-stu-id="e0990-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="e0990-180">Риск при входе</span><span class="sxs-lookup"><span data-stu-id="e0990-180">Sign-in risk</span></span>
<span data-ttu-id="e0990-181">**tootest входа в риск, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e0990-181">**tootest a sign in risk, perform hello following steps:**</span></span>

1. <span data-ttu-id="e0990-182">Вход слишком[https://portal.azure.com ](https://portal.azure.com) с учетными данными глобального администратора для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="e0990-182">Sign-in too[https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="e0990-183">Перейдите в слишком**защиты идентификации**.</span><span class="sxs-lookup"><span data-stu-id="e0990-183">Navigate too**Identity Protection**.</span></span>
3. <span data-ttu-id="e0990-184">На главном hello **Azure AD Identity Protection** колонка, щелкните **параметры**.</span><span class="sxs-lookup"><span data-stu-id="e0990-184">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="e0990-185">На hello **Параметры портала** колонки в разделе **правила безопасности**, нажмите кнопку **входа риск**.</span><span class="sxs-lookup"><span data-stu-id="e0990-185">On hello **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="e0990-186">На hello ** вход риск ** колонке выберите **на** под **включить правило**.</span><span class="sxs-lookup"><span data-stu-id="e0990-186">On hello **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="e0990-187">Выберите один из следующих вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="e0990-187">Select one of hello following options:</span></span>
   
   <span data-ttu-id="e0990-188">а.</span><span class="sxs-lookup"><span data-stu-id="e0990-188">a.</span></span> <span data-ttu-id="e0990-189">tooblock, выберите **Средний** под **входа блока**</span><span class="sxs-lookup"><span data-stu-id="e0990-189">tooblock, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="e0990-190">b.</span><span class="sxs-lookup"><span data-stu-id="e0990-190">b.</span></span> <span data-ttu-id="e0990-191">Изменение безопасного пароля tooenforce, выберите **Средний** под **требовать многофакторную проверку подлинности**.</span><span class="sxs-lookup"><span data-stu-id="e0990-191">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="e0990-192">tooblock, средний, выберите в области блока войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="e0990-192">tooblock, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="e0990-193">tooenforce многофакторную проверку подлинности, выберите **Средний** под **требовать многофакторную проверку подлинности**.</span><span class="sxs-lookup"><span data-stu-id="e0990-193">tooenforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="e0990-194">Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="e0990-194">Click on **Save**.</span></span>
10. <span data-ttu-id="e0990-195">Теперь можно проверить условного доступа на основе риск путем имитации незнакомых расположений hello, или анонимного IP-адреса угрозу события, поскольку оба **Средний** риск события.</span><span class="sxs-lookup"><span data-stu-id="e0990-195">You can now test risk-based conditional access by simulating hello unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="e0990-196">![Сборник тренировочных заданий](./media/active-directory-identityprotection-playbook/200.png "Сборник тренировочных заданий")</span><span class="sxs-lookup"><span data-stu-id="e0990-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="e0990-197">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="e0990-197">See also</span></span>
* [<span data-ttu-id="e0990-198">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e0990-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

