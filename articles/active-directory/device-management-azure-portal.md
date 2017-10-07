---
title: "портал Azure — hello aaaManaging устройств с помощью предварительного просмотра | Документы Microsoft"
description: "Узнайте, как toouse hello Azure портала toomanage устройств."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a><span data-ttu-id="a4c9b-103">Управление устройствами с помощью hello портал Azure — Предварительный просмотр</span><span class="sxs-lookup"><span data-stu-id="a4c9b-103">Managing devices using hello Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="a4c9b-104">Эта функция сейчас предоставляется в режиме общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-104">This capability currently is in public preview.</span></span> <span data-ttu-id="a4c9b-105">Подготовить toorevert или отмените все изменения.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-105">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="a4c9b-106">функция Hello доступна в подписках Azure Active Directory (Azure AD) предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-106">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="a4c9b-107">Однако при hello функция станет общедоступной, некоторые аспекты hello компонентов может потребоваться подписка Azure Active Directory premium.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-107">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="a4c9b-108">Благодаря управлению устройствами в Azure Active Directory (Azure AD) ваши пользователи получают доступ к ресурсам с устройств, которые соответствуют стандартам безопасности и нормативным требованиям.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="a4c9b-109">В этой статье:</span><span class="sxs-lookup"><span data-stu-id="a4c9b-109">This topic:</span></span>

- <span data-ttu-id="a4c9b-110">Предполагается, что вы знакомы с hello [управления toodevice введение в Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="a4c9b-110">Assumes that you are familiar with hello [introduction toodevice management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="a4c9b-111">Предоставляет вам сведения об управлении устройствами с помощью hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a4c9b-111">Provides you with information about managing your devices using hello Azure portal</span></span>


<span data-ttu-id="a4c9b-112">toomanage устройств в hello портал Azure, необходимо tooclick **устройств** в hello **управление** раздел hello hello **Azure Active Directory** колонку.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-112">toomanage devices in hello Azure portal, you need tooclick **Devices** in hello **Manage** section of hello hello **Azure Active Directory** blade.</span></span>

![Управление устройством Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="a4c9b-114">Настройка параметров устройства</span><span class="sxs-lookup"><span data-stu-id="a4c9b-114">Configure device settings</span></span>

<span data-ttu-id="a4c9b-115">устройства с помощью портала Azure hello, они должны toobe toomanage зарегистрирован или объединить tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-115">toomanage your devices using hello Azure portal, they need toobe either registered or joined tooAzure AD.</span></span> <span data-ttu-id="a4c9b-116">Как администратор можно выполнить тонкую настройку hello процесс регистрации и присоединения устройств, настроив параметры устройства hello.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-116">As an administrator, you can fine-tune hello process of registering and joining devices by configuring hello device settings.</span></span>

![Управление устройством Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="a4c9b-118">Hello колонку параметров устройств обеспечивает tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="a4c9b-118">hello device settings blade enables you tooconfigure:</span></span>

- <span data-ttu-id="a4c9b-119">**Пользователи могут присоединять устройства tooAzure AD** — это параметры позволяет tooselect hello пользователи могут присоединить устройства tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-119">**Users may join devices tooAzure AD** - This settings enables you tooselect hello users who can join devices tooAzure AD.</span></span> <span data-ttu-id="a4c9b-120">по умолчанию Hello — **все**.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-120">hello default is **All**.</span></span>

- <span data-ttu-id="a4c9b-121">**Дополнительные локальные администраторы в Azure AD устройств, присоединенных к** -можно выбирать hello пользователей, которым предоставляются права локального администратора на устройстве.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-121">**Additional local administrators on Azure AD joined devices** - You can select hello users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="a4c9b-122">Пользователей, добавленные здесь будут добавлены toohello *Администраторы устройств* роли в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-122">Users added here are added toohello *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="a4c9b-123">По умолчанию права локального администратора предоставляются глобальным администраторам в Azure AD и владельцам устройств.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="a4c9b-124">Этот параметр является возможностью premium edition доступны через продуктов, таких как Azure AD Premium или Enterprise Mobility Suite (EMS) hello.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-124">This option is a premium edition capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="a4c9b-125">**Пользователи могут регистрировать свои устройства в Azure AD** -требуется tooconfigure toobe устройств tooallow этот параметр, зарегистрированных в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-125">**Users may register their devices with Azure AD** - You need tooconfigure this setting tooallow devices toobe registered with Azure AD.</span></span> <span data-ttu-id="a4c9b-126">При выборе **нет**, tooregister, если они не присоединены Azure AD или гибридной Azure AD объединить устройства не допускаются.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-126">If you select **None**, devices are not allowed tooregister when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="a4c9b-127">Для регистрации в Microsoft Intune или службе управления мобильными устройствами (MDM) для Office 365 требуется регистрация.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="a4c9b-128">Если вы настроили одну из этих служб, то будет выбран пункт **ВСЕ**, а кнопка **НЕТ** будет отключена.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="a4c9b-129">**Требовать многофакторную проверку подлинности устройств toojoin** -для выбора пользователей, требуется tooprovide ли второй проверки подлинности коэффициент toojoin их устройства tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-129">**Require Multi-Factor Auth toojoin devices** - You can choose whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="a4c9b-130">по умолчанию Hello — **нет**.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-130">hello default is **No**.</span></span> <span data-ttu-id="a4c9b-131">Рекомендуется использовать Многофакторную идентификацию при регистрации устройства.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="a4c9b-132">Перед включением многофакторной проверки подлинности для этой службы, необходимо убедиться, что многофакторная проверка подлинности настроена для hello пользователей, которые регистрируют свои устройства.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for hello users that register their devices.</span></span> <span data-ttu-id="a4c9b-133">Дополнительные сведения о различных службах Многофакторной идентификации в Azure см. в статье [Приступая к работе со службой "Многофакторная идентификация Microsoft Azure" в облаке](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a4c9b-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="a4c9b-134">**Максимальное число устройств** -этот параметр включает tooselect hello максимальное число устройств, которые пользователь может располагать в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-134">**Maximum number of devices** - This setting enables you tooselect hello maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="a4c9b-135">Если пользователь достигает этой квоты, они не должны дополнительных устройств может tooadd пока один или несколько существующих устройств hello удаляются.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-135">If a user reaches this quota, they are not be able tooadd additional devices until one or more of hello existing devices are removed.</span></span> <span data-ttu-id="a4c9b-136">Квота Hello устройство будет считаться для всех устройств, которые присоединены Azure AD или Azure AD, зарегистрированных в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-136">hello device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="a4c9b-137">значение по умолчанию Hello — **20**.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-137">hello default value is **20**.</span></span>

- <span data-ttu-id="a4c9b-138">**Пользователи могут выполнять синхронизацию параметров и данных приложений на устройствах** -по умолчанию этого параметра установлено слишком**NONE**.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-138">**Users may sync settings and app data across devices** - By default, this setting is set too**NONE**.</span></span> <span data-ttu-id="a4c9b-139">Выбор конкретных пользователей или групп или все позволяет параметры пользователя hello и toosync данных приложения на своих устройствах Windows 10.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-139">Selecting specific users or groups or ALL allows hello user’s settings and app data toosync across their Windows 10 devices.</span></span> <span data-ttu-id="a4c9b-140">Узнайте больше о том, как работает синхронизация в Windows 10.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="a4c9b-141">Этот параметр является возможностью premium через продуктов, таких как Azure AD Premium или Enterprise Mobility Suite (EMS) hello.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-141">This option is a premium capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span>
 
    ![Управление устройством Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="a4c9b-143">Поиск устройств</span><span class="sxs-lookup"><span data-stu-id="a4c9b-143">Locate devices</span></span>

<span data-ttu-id="a4c9b-144">С правами администратора в hello портал Azure есть два способа toolocate зарегистрирован и устройств, присоединенных к:</span><span class="sxs-lookup"><span data-stu-id="a4c9b-144">As an administrator, in hello Azure portal, you have two options toolocate registered and joined devices:</span></span>

- <span data-ttu-id="a4c9b-145">**Все устройства** в hello **управление** раздел hello **устройств** колонку</span><span class="sxs-lookup"><span data-stu-id="a4c9b-145">**All devices** in hello **Manage** section of hello **Devices** blade</span></span>  

    ![Все устройства](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="a4c9b-147">**Устройства** в hello **управление** раздел **пользователя** колонку</span><span class="sxs-lookup"><span data-stu-id="a4c9b-147">**Devices** in hello **Manage** section of a **User** blade</span></span>
 
    ![Все устройства](./media/device-management-azure-portal/43.png)



<span data-ttu-id="a4c9b-149">С параметрами, и вы можете получить tooa представление:</span><span class="sxs-lookup"><span data-stu-id="a4c9b-149">With both options, you can get tooa view that:</span></span>


- <span data-ttu-id="a4c9b-150">Позволяет toosearch для устройств с помощью hello отображаемое имя в качестве фильтра.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-150">Enables you toosearch for devices using hello display name as filter.</span></span>

- <span data-ttu-id="a4c9b-151">предоставляет подробный обзор зарегистрированных и присоединенных к домену устройств;</span><span class="sxs-lookup"><span data-stu-id="a4c9b-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="a4c9b-152">Позволяет tooperform общие задачи управления устройствами</span><span class="sxs-lookup"><span data-stu-id="a4c9b-152">Enables you tooperform common device management tasks</span></span>
   

![Все устройства](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="a4c9b-154">Задачи управления устройствами</span><span class="sxs-lookup"><span data-stu-id="a4c9b-154">Device management tasks</span></span>

<span data-ttu-id="a4c9b-155">Как администратор, вы можете управлять hello зарегистрирован или устройств, присоединенных к.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-155">As an administrator, you can manage hello registered or joined devices.</span></span> <span data-ttu-id="a4c9b-156">В этом разделе приводятся сведения об общих задачах управления.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="a4c9b-157">**Управление устройством Intune**. Если вы являетесь администратором Intune, то вы можете управлять устройствами, которые помечены как **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="a4c9b-158">Администратор может видеть дополнительное устройство.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-158">An administrator can see additional device</span></span> 

![Управление устройством Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="a4c9b-160">**Включение или отключение устройства Azure AD**</span><span class="sxs-lookup"><span data-stu-id="a4c9b-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="a4c9b-161">tooenable или отключите устройство, необходимо toobe глобального администратора в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-161">tooenable or disable a device, you need toobe a global administrator in Azure  AD.</span></span> <span data-ttu-id="a4c9b-162">Отключение устройства не позволит ему обращаться к вашим ресурсам Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="a4c9b-163">toodisable hello устройства, можно нажать кнопку *...*</span><span class="sxs-lookup"><span data-stu-id="a4c9b-163">toodisable hello device, you can either click *…*</span></span> <span data-ttu-id="a4c9b-164">Выберите устройство hello для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-164">click hello device for additional details.</span></span>

 
![Управление устройством Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="a4c9b-166">Отключение устройства изменяет состояние hello в hello **включено** столбец слишком**нет**.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-166">Disabling a device changes hello state in hello **ENABLED** column too**No**.</span></span>

![Отключение устройства](./media/device-management-azure-portal/32.png)


<span data-ttu-id="a4c9b-168">**Удалить устройство Azure AD** -toodelete устройство, необходимо использовать toobe глобального администратора в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-168">**Delete an Azure AD device** - toodelete a device, you need toobe a global administrator in Azure AD.</span></span>  
<span data-ttu-id="a4c9b-169">Удаление устройства:</span><span class="sxs-lookup"><span data-stu-id="a4c9b-169">Deleting a device:</span></span>
 
- <span data-ttu-id="a4c9b-170">не позволит ему обращаться к вашим ресурсам Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a4c9b-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="a4c9b-171">Удаляет все сведения, которые являются toohello присоединенные устройства, например, ключи BitLocker для устройств Windows</span><span class="sxs-lookup"><span data-stu-id="a4c9b-171">Removes all details that are attached toohello device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="a4c9b-172">является действием без возможности восстановления и не рекомендуется, если только не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="a4c9b-173">Если устройство управляется другой центр управления (например, Microsoft Intune), убедитесь, что это устройство hello очищено, и удалено перед удалением устройства hello в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that hello device has been wiped / retired before deleting hello device in Azure AD.</span></span>

<span data-ttu-id="a4c9b-174">Вы можете щелкнуть "…",</span><span class="sxs-lookup"><span data-stu-id="a4c9b-174">You can either select “…”</span></span> <span data-ttu-id="a4c9b-175">устройство hello toodelete или hello устройства для получения дополнительных сведений щелкните здесь</span><span class="sxs-lookup"><span data-stu-id="a4c9b-175">toodelete hello device or click on hello device for additional details</span></span>
 
![Удалить устройство.](./media/device-management-azure-portal/34.png)


<span data-ttu-id="a4c9b-177">**Просмотр и копирование идентификатор устройства** -идентификатор tooverify hello устройства идентификатор сведения об устройстве можно использовать на устройстве hello или с помощью PowerShell во время устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-177">**View or copy device ID** - You can use a device ID tooverify hello device ID details on hello device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="a4c9b-178">tooaccess hello копирования, нажмите кнопку hello устройства.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-178">tooaccess hello copy option, click hello device.</span></span>

![Просмотр идентификатора устройства](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="a4c9b-180">**Просмотр и копирование ключи BitLocker** -Если вы являетесь администратором, можно просмотреть и копирования hello BitLocker ключей toorecover toohelp пользователей их зашифрованный диск.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy hello BitLocker keys toohelp users toorecover their encrypted drive.</span></span> <span data-ttu-id="a4c9b-181">Эти ключи доступны только для устройств Windows, которые были зашифрованы и ключи которых были сохранены в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="a4c9b-182">При доступе к hello устройств, можно скопировать эти ключи.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-182">You can copy these keys when accessing details of hello device.</span></span>
 
![Просмотр ключей BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="a4c9b-184">Журналы аудита</span><span class="sxs-lookup"><span data-stu-id="a4c9b-184">Audit logs</span></span>


<span data-ttu-id="a4c9b-185">Hello действий устройствами доступны через журналы действий hello.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-185">hello device activities are available through hello activity logs.</span></span> <span data-ttu-id="a4c9b-186">Это включает запуск службой регистрации устройств hello или пользователем hello действий:</span><span class="sxs-lookup"><span data-stu-id="a4c9b-186">This includes activities triggered by hello device registration service or by hello user:</span></span>

- <span data-ttu-id="a4c9b-187">Создания устройства и добавления владельцев или пользователей на устройстве hello</span><span class="sxs-lookup"><span data-stu-id="a4c9b-187">Device creation and adding owners/users on hello device</span></span>

- <span data-ttu-id="a4c9b-188">Изменения параметров toodevice</span><span class="sxs-lookup"><span data-stu-id="a4c9b-188">Changes toodevice settings</span></span>

- <span data-ttu-id="a4c9b-189">операции с устройством, например удаление или обновление устройства.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="a4c9b-190">Является вашей toohello точки входа, аудит данных **журналы аудита** в hello **действия** раздел hello **устройств* колонку.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-190">Your entry point toohello auditing data is **Audit logs** in hello **Activity** section of hello **Devices* blade.</span></span>

![Журналы аудита](./media/device-management-azure-portal/61.png)


<span data-ttu-id="a4c9b-192">Журнал аудита содержит представление списка по умолчанию, в котором отображаются:</span><span class="sxs-lookup"><span data-stu-id="a4c9b-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="a4c9b-193">Hello дату и время вхождения hello</span><span class="sxs-lookup"><span data-stu-id="a4c9b-193">hello date and time of hello occurrence</span></span>

- <span data-ttu-id="a4c9b-194">целевые объекты Hello</span><span class="sxs-lookup"><span data-stu-id="a4c9b-194">hello targets</span></span>

- <span data-ttu-id="a4c9b-195">Здравствуйте, инициатор или субъекта (,) действия</span><span class="sxs-lookup"><span data-stu-id="a4c9b-195">hello initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="a4c9b-196">Действие Hello (что)</span><span class="sxs-lookup"><span data-stu-id="a4c9b-196">hello activity (what)</span></span>

![Журналы аудита](./media/device-management-azure-portal/63.png)

<span data-ttu-id="a4c9b-198">Представление списка hello можно настроить, щелкнув **столбцы** инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-198">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>
 
![Журналы аудита](./media/device-management-azure-portal/64.png)


<span data-ttu-id="a4c9b-200">toonarrow вниз hello сообщила tooa уровень данных, что работает автоматически, можно фильтровать hello данные аудита, используя hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="a4c9b-200">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="a4c9b-201">Категория</span><span class="sxs-lookup"><span data-stu-id="a4c9b-201">Catergory</span></span>
- <span data-ttu-id="a4c9b-202">Тип ресурса действия</span><span class="sxs-lookup"><span data-stu-id="a4c9b-202">Activity resource type</span></span>
- <span data-ttu-id="a4c9b-203">Действие</span><span class="sxs-lookup"><span data-stu-id="a4c9b-203">Activity</span></span>
- <span data-ttu-id="a4c9b-204">диапазон дат;</span><span class="sxs-lookup"><span data-stu-id="a4c9b-204">Date range</span></span>
- <span data-ttu-id="a4c9b-205">Цель</span><span class="sxs-lookup"><span data-stu-id="a4c9b-205">Target</span></span>
- <span data-ttu-id="a4c9b-206">"Кем инициировано (субъект)".</span><span class="sxs-lookup"><span data-stu-id="a4c9b-206">Initiated By (Actor)</span></span>

<span data-ttu-id="a4c9b-207">Кроме того toohello фильтры, можно выполнить поиск конкретных записей.</span><span class="sxs-lookup"><span data-stu-id="a4c9b-207">In addition toohello filters, you can search for specific entries.</span></span>

![Журналы аудита](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="a4c9b-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4c9b-209">Next steps</span></span>

* [<span data-ttu-id="a4c9b-210">Управление toodevice введение в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4c9b-210">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



