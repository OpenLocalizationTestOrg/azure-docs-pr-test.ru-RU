---
title: "Вопросы и ответы об автоматической регистрации устройств в Azure Active Directory | Документация Майкрософт"
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
ms.openlocfilehash: 29751239ae2a26cd7b07ddd0d8a8e706d4056b68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="851c0-103">Вопросы и ответы об автоматической регистрации устройств в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="851c0-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="851c0-104">**Вопрос. Мной недавно было зарегистрировано устройство. Почему оно отсутствует в моих сведениях о пользователе на портале Azure?**</span><span class="sxs-lookup"><span data-stu-id="851c0-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="851c0-105">**Ответ.** Устройства Windows 10, присоединенных к домену с автоматической регистрацией устройств, не отображаются в области сведений о пользователе.</span><span class="sxs-lookup"><span data-stu-id="851c0-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span></span>
<span data-ttu-id="851c0-106">Чтобы увидеть все устройства, нужно использовать PowerShell.</span><span class="sxs-lookup"><span data-stu-id="851c0-106">You need to use PowerShell to see all devices.</span></span> 

<span data-ttu-id="851c0-107">В области сведений о пользователе перечислены только следующие устройства:</span><span class="sxs-lookup"><span data-stu-id="851c0-107">Only the following devices are listed under the USER info:</span></span>

- <span data-ttu-id="851c0-108">Все личные устройства, не присоединенные к сети предприятия.</span><span class="sxs-lookup"><span data-stu-id="851c0-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="851c0-109">Все устройства не на платформе Windows 10 или Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="851c0-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="851c0-110">Все устройства не на платформе Windows.</span><span class="sxs-lookup"><span data-stu-id="851c0-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="851c0-111">**Вопрос. Почему я не вижу на портале Azure все устройства, зарегистрированные в Azure Active Directory?**</span><span class="sxs-lookup"><span data-stu-id="851c0-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span></span> 

<span data-ttu-id="851c0-112">**Ответ.** В данный момент нет возможности просмотреть все зарегистрированные устройства на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="851c0-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span></span> <span data-ttu-id="851c0-113">Для поиска всех устройств можно использовать Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="851c0-113">You can use Azure PowerShell to find all devices.</span></span> <span data-ttu-id="851c0-114">Дополнительные сведения см. в описании командлета [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="851c0-114">For more details, see the [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="851c0-115">**Вопрос. Как узнать состояние регистрации устройства клиента?**</span><span class="sxs-lookup"><span data-stu-id="851c0-115">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="851c0-116">**Ответ.** Состояние регистрации устройства зависит от:</span><span class="sxs-lookup"><span data-stu-id="851c0-116">**A:** The device registration state depends on:</span></span>

- <span data-ttu-id="851c0-117">типа устройства;</span><span class="sxs-lookup"><span data-stu-id="851c0-117">What the device is</span></span>
- <span data-ttu-id="851c0-118">способа его регистрации;</span><span class="sxs-lookup"><span data-stu-id="851c0-118">How it was registered</span></span> 
- <span data-ttu-id="851c0-119">любых относящихся к нему данных.</span><span class="sxs-lookup"><span data-stu-id="851c0-119">Any details related to it.</span></span> 
 

---

<span data-ttu-id="851c0-120">**Вопрос. Почему устройство, удаленное мной на портале Azure или с помощью Windows PowerShell, по-прежнему указано как зарегистрированное?**</span><span class="sxs-lookup"><span data-stu-id="851c0-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="851c0-121">**Ответ.** Это сделано намеренно.</span><span class="sxs-lookup"><span data-stu-id="851c0-121">**A:** This is by design.</span></span> <span data-ttu-id="851c0-122">У устройства не будет доступа к ресурсам в облаке.</span><span class="sxs-lookup"><span data-stu-id="851c0-122">The device will not have access to resources in the cloud.</span></span> <span data-ttu-id="851c0-123">Если вы захотите удалить устройство и повторно зарегистрировать его, то на нем нужно будет выполнить действие вручную.</span><span class="sxs-lookup"><span data-stu-id="851c0-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="851c0-124">Для компьютеров Windows 10 и Windows Server 2016, присоединенных к локальному домену AD, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="851c0-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="851c0-125">Запустите командную строку от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="851c0-125">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="851c0-126">Введите `dsregcmd.exe /debug /leave`.</span><span class="sxs-lookup"><span data-stu-id="851c0-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="851c0-127">Выполните выход и вход, чтобы запустить запланированную задачу, которая повторно регистрирует устройство.</span><span class="sxs-lookup"><span data-stu-id="851c0-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span></span> 

<span data-ttu-id="851c0-128">Для компьютеров на других платформах Windows, присоединенных к локальному домену AD, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="851c0-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="851c0-129">Запустите командную строку от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="851c0-129">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="851c0-130">Введите `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="851c0-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="851c0-131">Введите `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="851c0-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="851c0-132">**Вопрос. Почему на портале Azure отображаются повторяющиеся записи устройств?**</span><span class="sxs-lookup"><span data-stu-id="851c0-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="851c0-133">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="851c0-133">**A:**</span></span>

-   <span data-ttu-id="851c0-134">Несколько попыток отсоединить, а затем присоединить одно и то же устройство Windows 10 или Windows Server 2016 могут привести к появлению повторяющихся записей.</span><span class="sxs-lookup"><span data-stu-id="851c0-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="851c0-135">Если вы использовали кнопку "Добавить рабочую или учебную учетную запись", то имейте ввиду, что каждый пользователь Windows, нажавший эту кнопку, создает новую запись устройства с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="851c0-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="851c0-136">На других платформах Windows, присоединенных к локальному домену AD с помощью автоматической регистрации, для каждого пользователя домена, который входит в устройство, создается новая запись устройства с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="851c0-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="851c0-137">Компьютер, присоединенный к AAD, который был очищен, подвержен повторной установке и повторно присоединен с тем же именем, будет отображен как еще одна запись с тем же именем устройства.</span><span class="sxs-lookup"><span data-stu-id="851c0-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="851c0-138">**Вопрос. Почему пользователь все еще имеет доступ к ресурсам с устройства, которое было отключено на портале Azure?**</span><span class="sxs-lookup"><span data-stu-id="851c0-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="851c0-139">**Ответ.** На применение отмены может потребоваться около часа.</span><span class="sxs-lookup"><span data-stu-id="851c0-139">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="851c0-140">В случае потери устройства рекомендуется очистить его, чтобы пользователи не смогли получить к нему доступ.</span><span class="sxs-lookup"><span data-stu-id="851c0-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span></span> <span data-ttu-id="851c0-141">Дополнительные сведения см. в разделе [Регистрация устройств для управления в Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="851c0-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="851c0-142">**Вопрос. Почему мои пользователи видят сообщение "You can’t get there from here" (Нет доступа)?**</span><span class="sxs-lookup"><span data-stu-id="851c0-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="851c0-143">**Ответ.** Если вы настроили определенные правила условного доступа, чтобы требовать определенное состояние устройства, и устройство им не соответствует, то пользователи заблокируются и видят данное сообщение.</span><span class="sxs-lookup"><span data-stu-id="851c0-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="851c0-144">Оцените эти правила и убедитесь, что устройство может удовлетворять их критериям, чтобы избежать появления этого сообщения.</span><span class="sxs-lookup"><span data-stu-id="851c0-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---


<span data-ttu-id="851c0-145">**Вопрос. В области сведений о пользователе на портале Azure отображается запись устройства и указывается, что оно зарегистрировано в клиенте. Правильно ли оно настроено для применения условного доступа?**</span><span class="sxs-lookup"><span data-stu-id="851c0-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="851c0-146">**Ответ.** Запись устройства (deviceID) и его состояние на портале Azure должны соответствовать клиенту и удовлетворять всем критериям оценки для условного доступа.</span><span class="sxs-lookup"><span data-stu-id="851c0-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="851c0-147">Дополнительные сведения см. в разделе [Знакомство с регистрацией устройств в Azure Active Directory](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="851c0-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="851c0-148">**Вопрос. Почему я получаю сообщение "Неверное имя пользователя или пароль" для устройства, которые было только что присоединено к Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="851c0-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="851c0-149">**Ответ.** Ниже перечислены распространенные причины появления такого сообщения:</span><span class="sxs-lookup"><span data-stu-id="851c0-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="851c0-150">Ваши учетные данные недействительны.</span><span class="sxs-lookup"><span data-stu-id="851c0-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="851c0-151">Вашему компьютеру не удалось связаться с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="851c0-151">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="851c0-152">Наличие проблем с сетевым подключением.</span><span class="sxs-lookup"><span data-stu-id="851c0-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="851c0-153">Не были выполнены предварительные требования присоединения к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="851c0-153">The Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="851c0-154">Убедитесь, что вы следовали указаниям в статье [Использование возможностей облачных служб на устройствах с Windows 10 с помощью присоединения к Azure Active Directory](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="851c0-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="851c0-155">Для использования федеративных имен для входа требуется, чтобы сервер федерации поддерживал активную конечную точку WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="851c0-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="851c0-156">**Вопрос. Почему я вижу диалоговое окно "Oops… an error occurred!" (Произошла ошибка) при попытке присоединить свой компьютер?**</span><span class="sxs-lookup"><span data-stu-id="851c0-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="851c0-157">**Ответ.** Причина этого в настройке регистрации Azure Active Directory с помощью Intune.</span><span class="sxs-lookup"><span data-stu-id="851c0-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="851c0-158">Дополнительные сведения см. в разделе [Настройка управления устройствами Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="851c0-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="851c0-159">**Вопрос. Почему мне не удается присоединить компьютер, хотя никакие сообщения об ошибке не отображаются?**</span><span class="sxs-lookup"><span data-stu-id="851c0-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="851c0-160">**Ответ.** Наиболее вероятная причина — пользователь вошел на устройство с помощью встроенной учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="851c0-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span></span> <span data-ttu-id="851c0-161">Создайте другую локальную учетную запись, прежде чем использовать присоединение к Azure Active Directory, чтобы завершить настройку.</span><span class="sxs-lookup"><span data-stu-id="851c0-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 

---

<span data-ttu-id="851c0-162">**Вопрос. Где можно найти инструкции для настройки автоматической регистрации устройств?**</span><span class="sxs-lookup"><span data-stu-id="851c0-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span></span>

<span data-ttu-id="851c0-163">**Ответ.** Подробные инструкции см. в статье [Настройка автоматической регистрации присоединенных к домену устройств Windows в Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="851c0-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="851c0-164">**Вопрос. Где можно найти сведения об устранении неполадок автоматической регистрации устройств?**</span><span class="sxs-lookup"><span data-stu-id="851c0-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="851c0-165">**Ответ.** Сведения об устранении неполадок можно найти в этих разделах:</span><span class="sxs-lookup"><span data-stu-id="851c0-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="851c0-166">Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров для Windows 10 и Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="851c0-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="851c0-167">Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров для клиентов Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="851c0-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

