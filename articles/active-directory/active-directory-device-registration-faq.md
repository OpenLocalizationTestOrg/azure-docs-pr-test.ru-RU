---
title: "aaaAzure Active Directory автоматической регистрации устройств часто задаваемые вопросы | Документы Microsoft"
description: "Часто задаваемые вопросы об автоматической регистрации устройств в Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: ba7f113fd3bc310def001a1f44d938b0be71dba8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="c0a41-103">Вопросы и ответы об автоматической регистрации устройств в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0a41-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="c0a41-104">**Вопрос. я недавно регистрации устройства hello. Почему отсутствует hello устройства в группе Мои сведения о пользователе в hello портал Azure**</span><span class="sxs-lookup"><span data-stu-id="c0a41-104">**Q: I registered hello device recently. Why can’t I see hello device under my user info in hello Azure portal?**</span></span>

<span data-ttu-id="c0a41-105">**Ответ** устройств Windows 10, присоединенных к домену с автоматической регистрации устройств, не отображаются в списке сведения о ПОЛЬЗОВАТЕЛЕ hello.</span><span class="sxs-lookup"><span data-stu-id="c0a41-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under hello USER info.</span></span>
<span data-ttu-id="c0a41-106">Требуется toouse PowerShell toosee все устройства.</span><span class="sxs-lookup"><span data-stu-id="c0a41-106">You need toouse PowerShell toosee all devices.</span></span> 

<span data-ttu-id="c0a41-107">Только hello следующие устройства отображаются в сведения о ПОЛЬЗОВАТЕЛЕ hello:</span><span class="sxs-lookup"><span data-stu-id="c0a41-107">Only hello following devices are listed under hello USER info:</span></span>

- <span data-ttu-id="c0a41-108">Все личные устройства, не присоединенные к сети предприятия.</span><span class="sxs-lookup"><span data-stu-id="c0a41-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="c0a41-109">Все устройства не на платформе Windows 10 или Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c0a41-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="c0a41-110">Все устройства не на платформе Windows.</span><span class="sxs-lookup"><span data-stu-id="c0a41-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="c0a41-111">**Вопрос. Почему не отображаются все устройства hello, зарегистрированные в Azure Active Directory в hello портал Azure?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-111">**Q: Why can I not see all hello devices registered in Azure Active Directory in hello Azure portal?**</span></span> 

<span data-ttu-id="c0a41-112">**Ответ** в настоящее время нет способа toosee все зарегистрированные устройства в имеется hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a41-112">**A:** Currently, there is no way toosee all registered devices in hello Azure portal.</span></span> <span data-ttu-id="c0a41-113">Все устройства можно использовать toofind Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c0a41-113">You can use Azure PowerShell toofind all devices.</span></span> <span data-ttu-id="c0a41-114">Дополнительные сведения см. в разделе hello [Get MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) командлета.</span><span class="sxs-lookup"><span data-stu-id="c0a41-114">For more details, see hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="c0a41-115">**Как определить, какие hello состояния регистрации устройства клиента hello вопрос. есть?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-115">**Q: How do I know what hello device registration state of hello client is?**</span></span>

<span data-ttu-id="c0a41-116">**Ответ** зависит от состояния регистрации устройства hello:</span><span class="sxs-lookup"><span data-stu-id="c0a41-116">**A:** hello device registration state depends on:</span></span>

- <span data-ttu-id="c0a41-117">Какие устройства hello</span><span class="sxs-lookup"><span data-stu-id="c0a41-117">What hello device is</span></span>
- <span data-ttu-id="c0a41-118">способа его регистрации;</span><span class="sxs-lookup"><span data-stu-id="c0a41-118">How it was registered</span></span> 
- <span data-ttu-id="c0a41-119">Любые данные, связанные с tooit.</span><span class="sxs-lookup"><span data-stu-id="c0a41-119">Any details related tooit.</span></span> 
 

---

<span data-ttu-id="c0a41-120">**Вопрос. Почему это устройство, удаленный в hello Azure портала или с помощью Windows PowerShell по-прежнему перечислены зарегистрированный?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-120">**Q: Why is a device I have deleted in hello Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="c0a41-121">**Ответ.** Это сделано намеренно.</span><span class="sxs-lookup"><span data-stu-id="c0a41-121">**A:** This is by design.</span></span> <span data-ttu-id="c0a41-122">Hello устройство не будет tooresources доступа в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="c0a41-122">hello device will not have access tooresources in hello cloud.</span></span> <span data-ttu-id="c0a41-123">Если tooremove hello устройства и повторите регистрацию, выполняемое вручную действие должно быть toobe, которое выполняется на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="c0a41-123">If you want tooremove hello device and register again, a manual action must be toobe taken on hello device.</span></span> 

<span data-ttu-id="c0a41-124">Для компьютеров Windows 10 и Windows Server 2016, присоединенных к локальному домену AD, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="c0a41-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="c0a41-125">Откройте командную строку hello с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="c0a41-125">Open hello command prompt as an administrator.</span></span>

2.  <span data-ttu-id="c0a41-126">Введите `dsregcmd.exe /debug /leave`.</span><span class="sxs-lookup"><span data-stu-id="c0a41-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="c0a41-127">Выйдите из системы и войдите в tootrigger hello задание, которое регистрирует hello устройство еще раз.</span><span class="sxs-lookup"><span data-stu-id="c0a41-127">Sign out and sign in tootrigger hello scheduled task that registers hello device again.</span></span> 

<span data-ttu-id="c0a41-128">Для компьютеров на других платформах Windows, присоединенных к локальному домену AD, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="c0a41-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="c0a41-129">Откройте командную строку hello с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="c0a41-129">Open hello command prompt as an administrator.</span></span>
2.  <span data-ttu-id="c0a41-130">Введите `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="c0a41-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="c0a41-131">Введите `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="c0a41-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="c0a41-132">**Вопрос. Почему на портале Azure отображаются повторяющиеся записи устройств?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="c0a41-133">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="c0a41-133">**A:**</span></span>

-   <span data-ttu-id="c0a41-134">Для Windows 10 и Windows Server 2016, если они являются toounjoin повторных попыток и подключите его к hello одном устройстве, могут существовать повторяющиеся записи.</span><span class="sxs-lookup"><span data-stu-id="c0a41-134">For Windows 10 and Windows Server 2016, if they are repeated attempts toounjoin and re-join hello same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="c0a41-135">При использовании добавить рабочую или учебную учетную запись каждого пользователя windows, использующего добавить рабочую или учебную учетную запись будет создать новую запись устройства с hello одинаковое имя устройства.</span><span class="sxs-lookup"><span data-stu-id="c0a41-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with hello same device name.</span></span>

-   <span data-ttu-id="c0a41-136">Другие платформы Windows, которые являются локальными AD, присоединенных к домену с помощью автоматической регистрации будет создать новую запись устройства с hello одинаковое имя устройства, для каждого пользователя домена, работающему в устройство hello.</span><span class="sxs-lookup"><span data-stu-id="c0a41-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with hello same device name for each domain user who logs into hello device.</span></span> 

-   <span data-ttu-id="c0a41-137">Машине AADJ, было очищено, повторно установить и повторно присоединить с hello же имя, будет показываться как другая запись с hello одинаковое имя устройства.</span><span class="sxs-lookup"><span data-stu-id="c0a41-137">An AADJ machine that has been wiped, re-installed and re-joined with hello same name, will show up as another record with hello same device name.</span></span>

---

<span data-ttu-id="c0a41-138">**Вопрос. Почему пользователь по-прежнему доступны ресурсы с устройства, которые отключена в hello портал Azure?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-138">**Q: Why can a user still access resources from a device I have disabled in hello Azure portal?**</span></span>

<span data-ttu-id="c0a41-139">**Ответ** может занять час tooan revoke toobe применения.</span><span class="sxs-lookup"><span data-stu-id="c0a41-139">**A:** It can take up tooan hour for a revoke toobe applied.</span></span>

>[!Note] 
><span data-ttu-id="c0a41-140">Для утерянных устройств рекомендуется Очистка hello tooensure устройства, что пользователи не могут открывать hello устройства.</span><span class="sxs-lookup"><span data-stu-id="c0a41-140">For lost devices, we recommend wiping hello device tooensure that users cannot access hello device.</span></span> <span data-ttu-id="c0a41-141">Дополнительные сведения см. в разделе [Регистрация устройств для управления в Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="c0a41-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="c0a41-142">**Вопрос. Почему мои пользователи видят сообщение "You can’t get there from here" (Нет доступа)?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="c0a41-143">**Ответ** hello устройство не соответствует требованиям hello настройки определенных toorequire правила условного доступа состояние определенного устройства, пользователи заблокированы и данное сообщение.</span><span class="sxs-lookup"><span data-stu-id="c0a41-143">**A:** If you have configured certain conditional access rules toorequire a specific device state and hello device does not meet hello criteria, users are blocked and see this message.</span></span> <span data-ttu-id="c0a41-144">Проверьте оценка правил hello и убедитесь, это устройство hello является tooavoid критерии hello может toomeet это сообщение.</span><span class="sxs-lookup"><span data-stu-id="c0a41-144">Please evaluate hello rules and ensure that hello device is able toomeet hello criteria tooavoid this message.</span></span>

---


<span data-ttu-id="c0a41-145">**Вопрос. я см. запись hello устройства в группе сведения о ПОЛЬЗОВАТЕЛЕ hello в hello портал Azure и проверки состояния hello, зарегистрированного на приветствия клиента. Правильно ли оно настроено для применения условного доступа?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-145">**Q: I see hello device record under hello USER info in hello Azure portal and can see hello state as registered on hello client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="c0a41-146">**Ответ** записью hello устройства (идентификатор устройства) и состояние на портал Azure hello соответствует клиента hello и соответствуют критериям оценки условного доступа.</span><span class="sxs-lookup"><span data-stu-id="c0a41-146">**A:** hello device record (deviceID) and state on hello Azure portal must match hello client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="c0a41-147">Дополнительные сведения см. в разделе [Знакомство с регистрацией устройств в Azure Active Directory](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="c0a41-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="c0a41-148">**Вопрос. Почему я получаю сообщение «имя пользователя или пароль неправильный» для устройства я только что присоединились к tooAzure AD?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined tooAzure AD?**</span></span>

<span data-ttu-id="c0a41-149">**Ответ.** Ниже перечислены распространенные причины появления такого сообщения:</span><span class="sxs-lookup"><span data-stu-id="c0a41-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="c0a41-150">Ваши учетные данные недействительны.</span><span class="sxs-lookup"><span data-stu-id="c0a41-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="c0a41-151">Компьютер будет невозможно toocommunicate с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c0a41-151">Your computer is unable toocommunicate with Azure Active Directory.</span></span> <span data-ttu-id="c0a41-152">Наличие проблем с сетевым подключением.</span><span class="sxs-lookup"><span data-stu-id="c0a41-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="c0a41-153">Hello присоединения Azure AD предварительных требований не выполнены.</span><span class="sxs-lookup"><span data-stu-id="c0a41-153">hello Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="c0a41-154">Убедитесь, что были выполнены шаги hello [расширение возможностей tooWindows 10 устройствами с помощью присоединения Azure Active Directory облака](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0a41-154">Please ensure that you have followed hello steps for [Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="c0a41-155">Федеративных входов требует вашего toosupport сервер федерации к активной конечной точке WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="c0a41-155">Federated logins requires your federation server toosupport a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="c0a41-156">**Вопрос. Почему я вижу hello»... Ошибка произошла ошибка!» диалогового окна, при попытке присоединить ПК?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-156">**Q: Why do I see hello “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="c0a41-157">**Ответ.** Причина этого в настройке регистрации Azure Active Directory с помощью Intune.</span><span class="sxs-lookup"><span data-stu-id="c0a41-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="c0a41-158">Дополнительные сведения см. в разделе [Настройка управления устройствами Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="c0a41-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="c0a41-159">**Вопрос. Почему ли мои toojoin попытки ПК ошибкой, несмотря на то, что не удалось получить информацию об ошибках?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-159">**Q: Why did my attempt toojoin a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="c0a41-160">**Ответ** вероятной причиной является которого hello пользователь вошел в toohello устройства, с помощью hello встроенной учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="c0a41-160">**A:** A likely cause is that hello user is logged in toohello device using hello built-in administrator account.</span></span> <span data-ttu-id="c0a41-161">Создайте другую учетную запись локального перед использованием программы установки hello toocomplete присоединения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c0a41-161">Please create a different local account before using Azure Active Directory Join toocomplete hello setup.</span></span> 

---

<span data-ttu-id="c0a41-162">**Вопрос. где можно найти инструкции для установки hello автоматической регистрации устройств?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-162">**Q: Where can I find instructions for hello setup of automatic device registration?**</span></span>

<span data-ttu-id="c0a41-163">**Ответ** подробные инструкции см. в разделе [как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="c0a41-163">**A:** For detailed instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="c0a41-164">**Вопрос. где можно найти Устранение неполадок сведения о hello автоматической регистрации устройств?**</span><span class="sxs-lookup"><span data-stu-id="c0a41-164">**Q: Where can I find troubleshooting information about hello automatic device registration?**</span></span>

<span data-ttu-id="c0a41-165">**Ответ.** Сведения об устранении неполадок можно найти в этих разделах:</span><span class="sxs-lookup"><span data-stu-id="c0a41-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="c0a41-166">Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD – Windows 10 и Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c0a41-166">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="c0a41-167">Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD для клиентов нижнего уровня Windows</span><span class="sxs-lookup"><span data-stu-id="c0a41-167">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

