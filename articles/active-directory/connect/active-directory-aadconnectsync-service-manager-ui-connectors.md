---
title: "Соединители в пользовательском интерфейсе Synchronization Service Manager Azure AD Connect | Документация Майкрософт"
description: "Получите общие сведения о вкладке \"Соединители\" в диспетчере службы синхронизации для Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0fae4b1755ca95466eeffb5ce61c1c7855d7381
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="using-connectors-with-the-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="1d042-103">Использование соединителей с Synchronization Service Manager Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="1d042-103">Using connectors with the Azure AD Connect Sync Service Manager</span></span>

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="1d042-105">Вкладка "Соединители" используется для управления всеми системами, к которым подключен модуль синхронизации.</span><span class="sxs-lookup"><span data-stu-id="1d042-105">The Connectors tab is used to manage all systems the sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="1d042-106">Действия соединителя</span><span class="sxs-lookup"><span data-stu-id="1d042-106">Connector actions</span></span>
| <span data-ttu-id="1d042-107">Действие</span><span class="sxs-lookup"><span data-stu-id="1d042-107">Action</span></span> | <span data-ttu-id="1d042-108">Комментарий</span><span class="sxs-lookup"><span data-stu-id="1d042-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="1d042-109">Создание</span><span class="sxs-lookup"><span data-stu-id="1d042-109">Create</span></span> |<span data-ttu-id="1d042-110">Не используйте.</span><span class="sxs-lookup"><span data-stu-id="1d042-110">Do not use.</span></span> <span data-ttu-id="1d042-111">Для подключения к дополнительным лесам AD используйте мастер установки.</span><span class="sxs-lookup"><span data-stu-id="1d042-111">For connecting to additional AD forests, use the installation wizard.</span></span> |
| <span data-ttu-id="1d042-112">Свойства</span><span class="sxs-lookup"><span data-stu-id="1d042-112">Properties</span></span> |<span data-ttu-id="1d042-113">Используется для фильтрации доменов и подразделений.</span><span class="sxs-lookup"><span data-stu-id="1d042-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="1d042-114">Удалить</span><span class="sxs-lookup"><span data-stu-id="1d042-114">Delete</span></span>](#delete) |<span data-ttu-id="1d042-115">Используется для удаления данных в пространстве соединителя или удаления подключения к лесу.</span><span class="sxs-lookup"><span data-stu-id="1d042-115">Used to either delete the data in the connector space or to delete connection to a forest.</span></span> |
| [<span data-ttu-id="1d042-116">Настройка профилей выполнения</span><span class="sxs-lookup"><span data-stu-id="1d042-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="1d042-117">Ничего настраивать не требуется, кроме фильтрации домена.</span><span class="sxs-lookup"><span data-stu-id="1d042-117">Except for domain filtering, nothing to configure here.</span></span> <span data-ttu-id="1d042-118">Это действие можно использовать для просмотра уже настроенных профилей выполнения.</span><span class="sxs-lookup"><span data-stu-id="1d042-118">You can use this action to see already configured run profiles.</span></span> |
| <span data-ttu-id="1d042-119">Выполнить</span><span class="sxs-lookup"><span data-stu-id="1d042-119">Run</span></span> |<span data-ttu-id="1d042-120">Используется для одноразового запуска профиля.</span><span class="sxs-lookup"><span data-stu-id="1d042-120">Used to start a one-off run of a profile.</span></span> |
| <span data-ttu-id="1d042-121">Остановить</span><span class="sxs-lookup"><span data-stu-id="1d042-121">Stop</span></span> |<span data-ttu-id="1d042-122">Останавливает соединитель, на котором в настоящее время запущен профиль.</span><span class="sxs-lookup"><span data-stu-id="1d042-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="1d042-123">Экспортировать соединитель</span><span class="sxs-lookup"><span data-stu-id="1d042-123">Export Connector</span></span> |<span data-ttu-id="1d042-124">Не используйте.</span><span class="sxs-lookup"><span data-stu-id="1d042-124">Do not use.</span></span> |
| <span data-ttu-id="1d042-125">Импортировать соединитель</span><span class="sxs-lookup"><span data-stu-id="1d042-125">Import Connector</span></span> |<span data-ttu-id="1d042-126">Не используйте.</span><span class="sxs-lookup"><span data-stu-id="1d042-126">Do not use.</span></span> |
| <span data-ttu-id="1d042-127">Обновить соединитель</span><span class="sxs-lookup"><span data-stu-id="1d042-127">Update Connector</span></span> |<span data-ttu-id="1d042-128">Не используйте.</span><span class="sxs-lookup"><span data-stu-id="1d042-128">Do not use.</span></span> |
| <span data-ttu-id="1d042-129">Обновить схему</span><span class="sxs-lookup"><span data-stu-id="1d042-129">Refresh Schema</span></span> |<span data-ttu-id="1d042-130">Обновляет кэшированную схему.</span><span class="sxs-lookup"><span data-stu-id="1d042-130">Refreshes the cached schema.</span></span> <span data-ttu-id="1d042-131">Этот параметр рекомендуется использовать в мастере установки, так как он также обновляет правила синхронизации.</span><span class="sxs-lookup"><span data-stu-id="1d042-131">It is preferred to use the option in the installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="1d042-132">Пространство поиска соединителя</span><span class="sxs-lookup"><span data-stu-id="1d042-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="1d042-133">Применяется для поиска объектов и [отслеживания объекта и его данных в системе](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="1d042-133">Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="1d042-134">Удалить</span><span class="sxs-lookup"><span data-stu-id="1d042-134">Delete</span></span>
<span data-ttu-id="1d042-135">Действие удаления используется в двух разных целях.</span><span class="sxs-lookup"><span data-stu-id="1d042-135">The delete action is used for two different things.</span></span>  
![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="1d042-137">Параметр **Delete connector space only** (Удалить только пространство соединителя) позволяет удалить все данные, но оставить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="1d042-137">The option **Delete connector space only** removes all data, but keep the configuration.</span></span>

<span data-ttu-id="1d042-138">Параметр **Delete Connector and connector space** (Удалить соединитель и пространство соединителя) позволяет удалить данные и конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="1d042-138">The option **Delete Connector and connector space** removes the data and the configuration.</span></span> <span data-ttu-id="1d042-139">Этот параметр используется, если подключение к лесу больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="1d042-139">This option is used when you do not want to connect to a forest anymore.</span></span>

<span data-ttu-id="1d042-140">Оба параметра синхронизируют все объекты и обновляют объекты метавселенной.</span><span class="sxs-lookup"><span data-stu-id="1d042-140">Both options sync all objects and update the metaverse objects.</span></span> <span data-ttu-id="1d042-141">Это действие является длительной операцией.</span><span class="sxs-lookup"><span data-stu-id="1d042-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="1d042-142">Настройка профилей выполнения</span><span class="sxs-lookup"><span data-stu-id="1d042-142">Configure Run Profiles</span></span>
<span data-ttu-id="1d042-143">Этот параметр позволяет просматривать профили выполнения, настроенные для соединителя.</span><span class="sxs-lookup"><span data-stu-id="1d042-143">This option allows you to see the run profiles configured for a Connector.</span></span>

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="1d042-145">Пространство поиска соединителя</span><span class="sxs-lookup"><span data-stu-id="1d042-145">Search Connector Space</span></span>
<span data-ttu-id="1d042-146">Действие поиска пространства соединителя полезно для поиска объектов и устранения проблем с данными.</span><span class="sxs-lookup"><span data-stu-id="1d042-146">The search connector space action is useful to find objects and troubleshoot data issues.</span></span>

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="1d042-148">Начните с выбора **пространства**.</span><span class="sxs-lookup"><span data-stu-id="1d042-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="1d042-149">Можно выполнять поиск на основе данных (RDN DN, привязка, поддерево) или состояния объекта (все другие параметры).</span><span class="sxs-lookup"><span data-stu-id="1d042-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).</span></span>  
<span data-ttu-id="1d042-150">![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="1d042-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="1d042-151">Если, к примеру, выполняется поиск в поддереве, вы получаете все объекты в одном подразделении.</span><span class="sxs-lookup"><span data-stu-id="1d042-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="1d042-152">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="1d042-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="1d042-153">Здесь можно выбрать объект и **свойства**, а также [отслеживать объект](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) из исходного пространства соединителя через метавселенную до целевого пространства соединителя.</span><span class="sxs-lookup"><span data-stu-id="1d042-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.</span></span>

### <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="1d042-154">Изменение пароля учетной записи AD DS</span><span class="sxs-lookup"><span data-stu-id="1d042-154">Changing the AD DS account password</span></span>
<span data-ttu-id="1d042-155">В случае изменения пароля учетной записи служба синхронизации больше не сможет импортировать или экспортировать изменения в локальную среду AD.</span><span class="sxs-lookup"><span data-stu-id="1d042-155">If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.</span></span>   <span data-ttu-id="1d042-156">Может отображаться следующее:</span><span class="sxs-lookup"><span data-stu-id="1d042-156">You may see the following:</span></span>

- <span data-ttu-id="1d042-157">Шаг импорта или экспорта для соединителя AD завершается ошибкой "no-start-credentials".</span><span class="sxs-lookup"><span data-stu-id="1d042-157">The import/export step for the AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="1d042-158">В средстве просмотра событий Windows журнал событий приложения содержит ошибку с идентификатором события 6000 и сообщением об ошибке "Не удалось выполнить управляющий агент "contoso.com", так как учетные данные были недопустимыми".</span><span class="sxs-lookup"><span data-stu-id="1d042-158">Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”</span></span>

<span data-ttu-id="1d042-159">Чтобы устранить это проблему, обновите учетную запись пользователя AD DS, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="1d042-159">To resolve the issue, update the AD DS user account using the following:</span></span>


1. <span data-ttu-id="1d042-160">Запустите Synchronization Service Manager ("Запуск" → "Служба синхронизации").</span><span class="sxs-lookup"><span data-stu-id="1d042-160">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="1d042-161">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="1d042-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="1d042-162">Перейдите на вкладку **Соединители**.</span><span class="sxs-lookup"><span data-stu-id="1d042-162">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="1d042-163">Выберите соединитель AD, который настроен на использование учетной записи AD DS.</span><span class="sxs-lookup"><span data-stu-id="1d042-163">Select the AD Connector which is configured to use the AD DS account.</span></span>
4. <span data-ttu-id="1d042-164">В разделе "Действия" выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="1d042-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="1d042-165">Во всплывающем диалоговом окне выберите "Connect to Active Directory Forest" (Подключиться к лесу Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1d042-165">In the pop-up dialog, select Connect to Active Directory Forest:</span></span>
6. <span data-ttu-id="1d042-166">Имя леса указывает соответствующую локальную службу AD.</span><span class="sxs-lookup"><span data-stu-id="1d042-166">The Forest name indicates the corresponding on-prem AD.</span></span>
7. <span data-ttu-id="1d042-167">Имя пользователя указывает учетную запись AD DS, используемую для синхронизации.</span><span class="sxs-lookup"><span data-stu-id="1d042-167">The User name indicates the AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="1d042-168">В текстовом поле "Пароль" введите новый пароль учетной записи AD DS. ![Служебная программа для ключа шифрования в службе синхронизации Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png).</span><span class="sxs-lookup"><span data-stu-id="1d042-168">Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="1d042-169">Нажмите кнопку "ОК" для сохранения нового пароля и перезапустите службу синхронизации, чтобы удалить из кэша памяти старый пароль.</span><span class="sxs-lookup"><span data-stu-id="1d042-169">Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="1d042-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d042-170">Next steps</span></span>
<span data-ttu-id="1d042-171">Узнайте больше о настройке [службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="1d042-171">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="1d042-172">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="1d042-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
