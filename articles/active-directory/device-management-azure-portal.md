---
title: "Управление устройствами с помощью портала Azure (предварительная версия) | Документация Майкрософт"
description: "Узнайте, как использовать портал Azure для управления устройствами."
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
ms.openlocfilehash: 4b46e1627a229b0649d9ccd2550cd28fda9849f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="managing-devices-using-the-azure-portal---preview"></a><span data-ttu-id="f872c-103">Управление устройствами с помощью портала Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="f872c-103">Managing devices using the Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="f872c-104">Эта функция сейчас предоставляется в режиме общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="f872c-104">This capability currently is in public preview.</span></span> <span data-ttu-id="f872c-105">Вы должны быть готовы отменить или удалить все изменения.</span><span class="sxs-lookup"><span data-stu-id="f872c-105">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="f872c-106">На этапе общедоступной предварительной версии эта функция доступна во всех подписках Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f872c-106">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="f872c-107">Однако, когда функция станет общедоступной, для некоторых аспектов компонента может потребоваться подписка Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="f872c-107">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="f872c-108">Благодаря управлению устройствами в Azure Active Directory (Azure AD) ваши пользователи получают доступ к ресурсам с устройств, которые соответствуют стандартам безопасности и нормативным требованиям.</span><span class="sxs-lookup"><span data-stu-id="f872c-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="f872c-109">В этой статье:</span><span class="sxs-lookup"><span data-stu-id="f872c-109">This topic:</span></span>

- <span data-ttu-id="f872c-110">Предполагается, что вы ознакомлены с [общими сведениями об управлении устройствами в Azure Active Directory](device-management-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f872c-110">Assumes that you are familiar with the [introduction to device management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="f872c-111">приводятся сведения об управлении устройствами с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="f872c-111">Provides you with information about managing your devices using the Azure portal</span></span>


<span data-ttu-id="f872c-112">Для управления устройствами на портале Azure нужно щелкнуть **Устройства** в разделе **Управление**, расположенном в колонке **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f872c-112">To manage devices in the Azure portal, you need to click **Devices** in the **Manage** section of the the **Azure Active Directory** blade.</span></span>

![Управление устройством Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="f872c-114">Настройка параметров устройства</span><span class="sxs-lookup"><span data-stu-id="f872c-114">Configure device settings</span></span>

<span data-ttu-id="f872c-115">Чтобы иметь возможность управлять устройствами с помощью портала Azure, их нужно зарегистрировать в Azure AD или присоединить к каталогу Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872c-115">To manage your devices using the Azure portal, they need to be either registered or joined to Azure AD.</span></span> <span data-ttu-id="f872c-116">Администратор может точно настроить процесс регистрации и присоединения устройств, задав параметры устройства.</span><span class="sxs-lookup"><span data-stu-id="f872c-116">As an administrator, you can fine-tune the process of registering and joining devices by configuring the device settings.</span></span>

![Управление устройством Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="f872c-118">В колонке параметров устройства можно настроить следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="f872c-118">The device settings blade enables you to configure:</span></span>

- <span data-ttu-id="f872c-119">**Пользователи могут присоединять устройства к Azure AD**. Этот параметр позволяет выбрать пользователей, которые могут присоединять устройства к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872c-119">**Users may join devices to Azure AD** - This settings enables you to select the users who can join devices to Azure AD.</span></span> <span data-ttu-id="f872c-120">Значение этого параметра по умолчанию — **Все**.</span><span class="sxs-lookup"><span data-stu-id="f872c-120">The default is **All**.</span></span>

- <span data-ttu-id="f872c-121">**Дополнительные локальные администраторы на устройствах, присоединенных к Azure AD**. Этот параметр позволяет выбрать пользователей, которым предоставляются права локального администратора на устройстве.</span><span class="sxs-lookup"><span data-stu-id="f872c-121">**Additional local administrators on Azure AD joined devices** - You can select the users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="f872c-122">Добавленные здесь пользователи добавляются в роль *Администраторы устройств* в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872c-122">Users added here are added to the *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="f872c-123">По умолчанию права локального администратора предоставляются глобальным администраторам в Azure AD и владельцам устройств.</span><span class="sxs-lookup"><span data-stu-id="f872c-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="f872c-124">Этот параметр относится к возможностям выпуска Premium и доступен в таких продуктах, как Azure AD Premium или Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="f872c-124">This option is a premium edition capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="f872c-125">**Пользователи могут регистрировать устройства в Azure AD**. Этот параметр необходимо настроить, чтобы разрешить регистрацию устройств в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872c-125">**Users may register their devices with Azure AD** - You need to configure this setting to allow devices to be registered with Azure AD.</span></span> <span data-ttu-id="f872c-126">Если выбрать значение **Нет**, то регистрация устройств, не присоединенных к Azure AD или гибридной среде Azure AD, будет запрещена.</span><span class="sxs-lookup"><span data-stu-id="f872c-126">If you select **None**, devices are not allowed to register when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="f872c-127">Для регистрации в Microsoft Intune или службе управления мобильными устройствами (MDM) для Office 365 требуется регистрация.</span><span class="sxs-lookup"><span data-stu-id="f872c-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="f872c-128">Если вы настроили одну из этих служб, то будет выбран пункт **ВСЕ**, а кнопка **НЕТ** будет отключена.</span><span class="sxs-lookup"><span data-stu-id="f872c-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="f872c-129">**Чтобы присоединить устройства, требуется многофакторная идентификация**. Укажите, следует ли пользователям предоставлять второй фактор аутентификации для присоединения устройства к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872c-129">**Require Multi-Factor Auth to join devices** - You can choose whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="f872c-130">По умолчанию используется значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="f872c-130">The default is **No**.</span></span> <span data-ttu-id="f872c-131">Рекомендуется использовать Многофакторную идентификацию при регистрации устройства.</span><span class="sxs-lookup"><span data-stu-id="f872c-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="f872c-132">Перед включением Многофакторной идентификации для этой службы необходимо убедиться, что Многофакторная идентификация настроена для пользователей, которые регистрируют свои устройства.</span><span class="sxs-lookup"><span data-stu-id="f872c-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for the users that register their devices.</span></span> <span data-ttu-id="f872c-133">Дополнительные сведения о различных службах Многофакторной идентификации в Azure см. в статье [Приступая к работе со службой "Многофакторная идентификация Microsoft Azure" в облаке](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f872c-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="f872c-134">**Максимальное число устройств на пользователя**. Этот параметр позволяет выбрать максимальное количество устройств, которое пользователь может иметь в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872c-134">**Maximum number of devices** - This setting enables you to select the maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="f872c-135">По достижении этой квоты пользователь больше не сможет добавлять дополнительные устройства до тех пор, пока не будет удалены одно или несколько существующих устройств.</span><span class="sxs-lookup"><span data-stu-id="f872c-135">If a user reaches this quota, they are not be able to add additional devices until one or more of the existing devices are removed.</span></span> <span data-ttu-id="f872c-136">Квота устройств считается для всех устройств, которые присоединены к Azure AD или зарегистрированы в Azure AD на данный момент.</span><span class="sxs-lookup"><span data-stu-id="f872c-136">The device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="f872c-137">По умолчанию используется значение **20**.</span><span class="sxs-lookup"><span data-stu-id="f872c-137">The default value is **20**.</span></span>

- <span data-ttu-id="f872c-138">**Пользователи могут выполнять синхронизацию параметров и данных разных устройств**. По умолчанию этот параметр имеет значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="f872c-138">**Users may sync settings and app data across devices** - By default, this setting is set to **NONE**.</span></span> <span data-ttu-id="f872c-139">Выбор конкретных пользователей, групп или значения "Все" позволяет синхронизировать параметры и данные приложений пользователя на его устройствах Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f872c-139">Selecting specific users or groups or ALL allows the user’s settings and app data to sync across their Windows 10 devices.</span></span> <span data-ttu-id="f872c-140">Узнайте больше о том, как работает синхронизация в Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f872c-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="f872c-141">Этот параметр относится к возможностям Premium и доступен в таких продуктах, как Azure AD Premium или Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="f872c-141">This option is a premium capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span>
 
    ![Управление устройством Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="f872c-143">Поиск устройств</span><span class="sxs-lookup"><span data-stu-id="f872c-143">Locate devices</span></span>

<span data-ttu-id="f872c-144">Войдя на портал Azure как администратор, вы сможете воспользоваться двумя средствами обнаружения зарегистрированных и присоединенных к домену устройств:</span><span class="sxs-lookup"><span data-stu-id="f872c-144">As an administrator, in the Azure portal, you have two options to locate registered and joined devices:</span></span>

- <span data-ttu-id="f872c-145">**Все устройства** в разделе **Управление** колонки **Устройства**;</span><span class="sxs-lookup"><span data-stu-id="f872c-145">**All devices** in the **Manage** section of the **Devices** blade</span></span>  

    ![Все устройства](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="f872c-147">**Устройства** в разделе **Управление** колонки **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="f872c-147">**Devices** in the **Manage** section of a **User** blade</span></span>
 
    ![Все устройства](./media/device-management-azure-portal/43.png)



<span data-ttu-id="f872c-149">С помощью любого из этих средств можно получить представление, которое:</span><span class="sxs-lookup"><span data-stu-id="f872c-149">With both options, you can get to a view that:</span></span>


- <span data-ttu-id="f872c-150">позволяет искать устройства с помощью отображаемого имени в качестве фильтра;</span><span class="sxs-lookup"><span data-stu-id="f872c-150">Enables you to search for devices using the display name as filter.</span></span>

- <span data-ttu-id="f872c-151">предоставляет подробный обзор зарегистрированных и присоединенных к домену устройств;</span><span class="sxs-lookup"><span data-stu-id="f872c-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="f872c-152">позволяет выполнять общие задачи управления устройствами.</span><span class="sxs-lookup"><span data-stu-id="f872c-152">Enables you to perform common device management tasks</span></span>
   

![Все устройства](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="f872c-154">Задачи управления устройствами</span><span class="sxs-lookup"><span data-stu-id="f872c-154">Device management tasks</span></span>

<span data-ttu-id="f872c-155">Администратор может управлять зарегистрированными или присоединенными к домену устройствами.</span><span class="sxs-lookup"><span data-stu-id="f872c-155">As an administrator, you can manage the registered or joined devices.</span></span> <span data-ttu-id="f872c-156">В этом разделе приводятся сведения об общих задачах управления.</span><span class="sxs-lookup"><span data-stu-id="f872c-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="f872c-157">**Управление устройством Intune**. Если вы являетесь администратором Intune, то вы можете управлять устройствами, которые помечены как **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="f872c-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="f872c-158">Администратор может видеть дополнительное устройство.</span><span class="sxs-lookup"><span data-stu-id="f872c-158">An administrator can see additional device</span></span> 

![Управление устройством Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="f872c-160">**Включение или отключение устройства Azure AD**</span><span class="sxs-lookup"><span data-stu-id="f872c-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="f872c-161">Чтобы включить или отключить устройство, необходимы права глобального администратора в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872c-161">To enable or disable a device, you need to be a global administrator in Azure  AD.</span></span> <span data-ttu-id="f872c-162">Отключение устройства не позволит ему обращаться к вашим ресурсам Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872c-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="f872c-163">Чтобы отключить устройство, можно щелкнуть *…*</span><span class="sxs-lookup"><span data-stu-id="f872c-163">To disable the device, you can either click *…*</span></span> <span data-ttu-id="f872c-164">и выбрать устройство для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="f872c-164">click the device for additional details.</span></span>

 
![Управление устройством Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="f872c-166">После отключения устройства состояние в столбце **Включено** меняется на **Нет**.</span><span class="sxs-lookup"><span data-stu-id="f872c-166">Disabling a device changes the state in the **ENABLED** column to **No**.</span></span>

![Отключение устройства](./media/device-management-azure-portal/32.png)


<span data-ttu-id="f872c-168">**Удаление устройства Azure AD**. Чтобы включить или отключить устройство, необходимы права глобального администратора в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872c-168">**Delete an Azure AD device** - To delete a device, you need to be a global administrator in Azure AD.</span></span>  
<span data-ttu-id="f872c-169">Удаление устройства:</span><span class="sxs-lookup"><span data-stu-id="f872c-169">Deleting a device:</span></span>
 
- <span data-ttu-id="f872c-170">не позволит ему обращаться к вашим ресурсам Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f872c-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="f872c-171">приведет к удалению всех данных, связанных с устройством, например ключей BitLocker для устройств Windows;</span><span class="sxs-lookup"><span data-stu-id="f872c-171">Removes all details that are attached to the device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="f872c-172">является действием без возможности восстановления и не рекомендуется, если только не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="f872c-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="f872c-173">Если устройством управляет другой центр управления (например, Microsoft Intune), то перед удалением устройства в Azure AD убедитесь, что оно было очищено или снято с учета.</span><span class="sxs-lookup"><span data-stu-id="f872c-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that the device has been wiped / retired before deleting the device in Azure AD.</span></span>

<span data-ttu-id="f872c-174">Вы можете щелкнуть "…",</span><span class="sxs-lookup"><span data-stu-id="f872c-174">You can either select “…”</span></span> <span data-ttu-id="f872c-175">чтобы удалить устройство, или щелкнуть устройство, чтобы получить дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="f872c-175">to delete the device or click on the device for additional details</span></span>
 
![Удалить устройство.](./media/device-management-azure-portal/34.png)


<span data-ttu-id="f872c-177">**Просмотр и копирование идентификатора устройства**. С помощью идентификатора устройства можно проверить соответствующие сведения об устройстве или устранять неполадки, используя PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f872c-177">**View or copy device ID** - You can use a device ID to verify the device ID details on the device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="f872c-178">Чтобы перейти к функции копирования, щелкните устройство.</span><span class="sxs-lookup"><span data-stu-id="f872c-178">To access the copy option, click the device.</span></span>

![Просмотр идентификатора устройства](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="f872c-180">**Просмотр и копирование ключей BitLocker**. Если вы являетесь администратором, то можете просмотреть и скопировать ключи BitLocker, чтобы помочь пользователям восстановить свои зашифрованные диски.</span><span class="sxs-lookup"><span data-stu-id="f872c-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy the BitLocker keys to help users to recover their encrypted drive.</span></span> <span data-ttu-id="f872c-181">Эти ключи доступны только для устройств Windows, которые были зашифрованы и ключи которых были сохранены в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f872c-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="f872c-182">Эти ключи можно скопировать, отобразив сведения об устройстве.</span><span class="sxs-lookup"><span data-stu-id="f872c-182">You can copy these keys when accessing details of the device.</span></span>
 
![Просмотр ключей BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="f872c-184">Журналы аудита</span><span class="sxs-lookup"><span data-stu-id="f872c-184">Audit logs</span></span>


<span data-ttu-id="f872c-185">Действия устройств можно просмотреть в журналах действий.</span><span class="sxs-lookup"><span data-stu-id="f872c-185">The device activities are available through the activity logs.</span></span> <span data-ttu-id="f872c-186">Сюда входят действия, активированные службой регистрации устройств или пользователем:</span><span class="sxs-lookup"><span data-stu-id="f872c-186">This includes activities triggered by the device registration service or by the user:</span></span>

- <span data-ttu-id="f872c-187">создание устройства и добавление владельцев или пользователей устройства;</span><span class="sxs-lookup"><span data-stu-id="f872c-187">Device creation and adding owners/users on the device</span></span>

- <span data-ttu-id="f872c-188">изменение параметров устройства;</span><span class="sxs-lookup"><span data-stu-id="f872c-188">Changes to device settings</span></span>

- <span data-ttu-id="f872c-189">операции с устройством, например удаление или обновление устройства.</span><span class="sxs-lookup"><span data-stu-id="f872c-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="f872c-190">Знакомство с данными аудита следует начать с **журналов аудита** в разделе **Действие** колонки **Устройства*.</span><span class="sxs-lookup"><span data-stu-id="f872c-190">Your entry point to the auditing data is **Audit logs** in the **Activity** section of the **Devices* blade.</span></span>

![Журналы аудита](./media/device-management-azure-portal/61.png)


<span data-ttu-id="f872c-192">Журнал аудита содержит представление списка по умолчанию, в котором отображаются:</span><span class="sxs-lookup"><span data-stu-id="f872c-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="f872c-193">дата и время выполнения действия;</span><span class="sxs-lookup"><span data-stu-id="f872c-193">the date and time of the occurrence</span></span>

- <span data-ttu-id="f872c-194">целевые объекты;</span><span class="sxs-lookup"><span data-stu-id="f872c-194">the targets</span></span>

- <span data-ttu-id="f872c-195">инициатор или субъект (кто?) действия;</span><span class="sxs-lookup"><span data-stu-id="f872c-195">the initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="f872c-196">действие (что?).</span><span class="sxs-lookup"><span data-stu-id="f872c-196">the activity (what)</span></span>

![Журналы аудита](./media/device-management-azure-portal/63.png)

<span data-ttu-id="f872c-198">Представление списка можно настроить, щелкнув **Столбцы** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="f872c-198">You can customize the list view by clicking **Columns** in the toolbar.</span></span>
 
![Журналы аудита](./media/device-management-azure-portal/64.png)


<span data-ttu-id="f872c-200">Для сужения результатов до подходящего уровня вы можете отфильтровать данные аудита, используя следующие поля:</span><span class="sxs-lookup"><span data-stu-id="f872c-200">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="f872c-201">Категория</span><span class="sxs-lookup"><span data-stu-id="f872c-201">Catergory</span></span>
- <span data-ttu-id="f872c-202">Тип ресурса действия</span><span class="sxs-lookup"><span data-stu-id="f872c-202">Activity resource type</span></span>
- <span data-ttu-id="f872c-203">Действие</span><span class="sxs-lookup"><span data-stu-id="f872c-203">Activity</span></span>
- <span data-ttu-id="f872c-204">диапазон дат;</span><span class="sxs-lookup"><span data-stu-id="f872c-204">Date range</span></span>
- <span data-ttu-id="f872c-205">Цель</span><span class="sxs-lookup"><span data-stu-id="f872c-205">Target</span></span>
- <span data-ttu-id="f872c-206">"Кем инициировано (субъект)".</span><span class="sxs-lookup"><span data-stu-id="f872c-206">Initiated By (Actor)</span></span>

<span data-ttu-id="f872c-207">Помимо применения фильтров можно выполнить поиск конкретных записей.</span><span class="sxs-lookup"><span data-stu-id="f872c-207">In addition to the filters, you can search for specific entries.</span></span>

![Журналы аудита](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="f872c-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f872c-209">Next steps</span></span>

* [<span data-ttu-id="f872c-210">Общие сведения об управлении устройствами в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f872c-210">Introduction to device management in Azure Active Directory</span></span>](device-management-introduction.md)



