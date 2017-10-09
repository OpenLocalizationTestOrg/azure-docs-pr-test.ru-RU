---
title: "aaaConnectors в hello пользовательского интерфейса Azure AD Synchronization Service Manager | Документы Microsoft"
description: "Понимать hello Synchronization Service Manager на вкладке hello соединители для Azure AD Connect."
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
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="55930-103">Использование соединителей с hello Azure AD Connect Sync Service Manager</span><span class="sxs-lookup"><span data-stu-id="55930-103">Using connectors with hello Azure AD Connect Sync Service Manager</span></span>

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="55930-105">Вкладка соединители Hello — используется toomanage, которой подключен модуль синхронизации hello всех систем.</span><span class="sxs-lookup"><span data-stu-id="55930-105">hello Connectors tab is used toomanage all systems hello sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="55930-106">Действия соединителя</span><span class="sxs-lookup"><span data-stu-id="55930-106">Connector actions</span></span>
| <span data-ttu-id="55930-107">Действие</span><span class="sxs-lookup"><span data-stu-id="55930-107">Action</span></span> | <span data-ttu-id="55930-108">Комментарий</span><span class="sxs-lookup"><span data-stu-id="55930-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="55930-109">Создание</span><span class="sxs-lookup"><span data-stu-id="55930-109">Create</span></span> |<span data-ttu-id="55930-110">Не используйте.</span><span class="sxs-lookup"><span data-stu-id="55930-110">Do not use.</span></span> <span data-ttu-id="55930-111">Для подключения лесов tooadditional AD, используйте мастер установки hello.</span><span class="sxs-lookup"><span data-stu-id="55930-111">For connecting tooadditional AD forests, use hello installation wizard.</span></span> |
| <span data-ttu-id="55930-112">Свойства</span><span class="sxs-lookup"><span data-stu-id="55930-112">Properties</span></span> |<span data-ttu-id="55930-113">Используется для фильтрации доменов и подразделений.</span><span class="sxs-lookup"><span data-stu-id="55930-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="55930-114">Удалить</span><span class="sxs-lookup"><span data-stu-id="55930-114">Delete</span></span>](#delete) |<span data-ttu-id="55930-115">Используется tooeither удаление данных hello hello соединителя пробел или toodelete подключения tooa леса.</span><span class="sxs-lookup"><span data-stu-id="55930-115">Used tooeither delete hello data in hello connector space or toodelete connection tooa forest.</span></span> |
| [<span data-ttu-id="55930-116">Настройка профилей выполнения</span><span class="sxs-lookup"><span data-stu-id="55930-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="55930-117">За исключением домена, фильтрации, ничего не tooconfigure здесь.</span><span class="sxs-lookup"><span data-stu-id="55930-117">Except for domain filtering, nothing tooconfigure here.</span></span> <span data-ttu-id="55930-118">Это действие можно использовать профили запуска toosee уже настроен.</span><span class="sxs-lookup"><span data-stu-id="55930-118">You can use this action toosee already configured run profiles.</span></span> |
| <span data-ttu-id="55930-119">Выполнить</span><span class="sxs-lookup"><span data-stu-id="55930-119">Run</span></span> |<span data-ttu-id="55930-120">Использовать toostart одного раза запуска профиля.</span><span class="sxs-lookup"><span data-stu-id="55930-120">Used toostart a one-off run of a profile.</span></span> |
| <span data-ttu-id="55930-121">Остановить</span><span class="sxs-lookup"><span data-stu-id="55930-121">Stop</span></span> |<span data-ttu-id="55930-122">Останавливает соединитель, на котором в настоящее время запущен профиль.</span><span class="sxs-lookup"><span data-stu-id="55930-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="55930-123">Экспортировать соединитель</span><span class="sxs-lookup"><span data-stu-id="55930-123">Export Connector</span></span> |<span data-ttu-id="55930-124">Не используйте.</span><span class="sxs-lookup"><span data-stu-id="55930-124">Do not use.</span></span> |
| <span data-ttu-id="55930-125">Импортировать соединитель</span><span class="sxs-lookup"><span data-stu-id="55930-125">Import Connector</span></span> |<span data-ttu-id="55930-126">Не используйте.</span><span class="sxs-lookup"><span data-stu-id="55930-126">Do not use.</span></span> |
| <span data-ttu-id="55930-127">Обновить соединитель</span><span class="sxs-lookup"><span data-stu-id="55930-127">Update Connector</span></span> |<span data-ttu-id="55930-128">Не используйте.</span><span class="sxs-lookup"><span data-stu-id="55930-128">Do not use.</span></span> |
| <span data-ttu-id="55930-129">Обновить схему</span><span class="sxs-lookup"><span data-stu-id="55930-129">Refresh Schema</span></span> |<span data-ttu-id="55930-130">Обновляет кэшированные схемы hello.</span><span class="sxs-lookup"><span data-stu-id="55930-130">Refreshes hello cached schema.</span></span> <span data-ttu-id="55930-131">Это предпочтительный toouse hello вариант в мастере установки hello вместо этого, поскольку также обновлений синхронизировать правила.</span><span class="sxs-lookup"><span data-stu-id="55930-131">It is preferred toouse hello option in hello installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="55930-132">Пространство поиска соединителя</span><span class="sxs-lookup"><span data-stu-id="55930-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="55930-133">Используемых объектов toofind и слишком[выполните объект и его данные через систему hello](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="55930-133">Used toofind objects and too[Follow an object and its data through hello system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="55930-134">Удалить</span><span class="sxs-lookup"><span data-stu-id="55930-134">Delete</span></span>
<span data-ttu-id="55930-135">Действие delete Hello используется для двух разных целей.</span><span class="sxs-lookup"><span data-stu-id="55930-135">hello delete action is used for two different things.</span></span>  
![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="55930-137">Здравствуйте, параметр **удалить только пространство соединителя** удаляет все данные, но оставить hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="55930-137">hello option **Delete connector space only** removes all data, but keep hello configuration.</span></span>

<span data-ttu-id="55930-138">Здравствуйте, параметр **удалить соединители и места** удаляет данные hello и конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="55930-138">hello option **Delete Connector and connector space** removes hello data and hello configuration.</span></span> <span data-ttu-id="55930-139">Этот параметр используется в том случае, если больше не требуется tooconnect tooa леса.</span><span class="sxs-lookup"><span data-stu-id="55930-139">This option is used when you do not want tooconnect tooa forest anymore.</span></span>

<span data-ttu-id="55930-140">Оба варианта синхронизировать все объекты и обновить объекты метавселенной hello.</span><span class="sxs-lookup"><span data-stu-id="55930-140">Both options sync all objects and update hello metaverse objects.</span></span> <span data-ttu-id="55930-141">Это действие является длительной операцией.</span><span class="sxs-lookup"><span data-stu-id="55930-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="55930-142">Настройка профилей выполнения</span><span class="sxs-lookup"><span data-stu-id="55930-142">Configure Run Profiles</span></span>
<span data-ttu-id="55930-143">Этот параметр позволяет hello toosee запуска профилей, настроенных для соединителя.</span><span class="sxs-lookup"><span data-stu-id="55930-143">This option allows you toosee hello run profiles configured for a Connector.</span></span>

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="55930-145">Пространство поиска соединителя</span><span class="sxs-lookup"><span data-stu-id="55930-145">Search Connector Space</span></span>
<span data-ttu-id="55930-146">Действие пространства соединителя Hello поиска является полезным toofind объектов и устранения неполадок данных.</span><span class="sxs-lookup"><span data-stu-id="55930-146">hello search connector space action is useful toofind objects and troubleshoot data issues.</span></span>

![Диспетчер службы синхронизации](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="55930-148">Начните с выбора **пространства**.</span><span class="sxs-lookup"><span data-stu-id="55930-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="55930-149">Можно выполнить поиск на основе данных (RDN различающееся имя, привязка, поддерева) или состояния hello объекта (все другие параметры).</span><span class="sxs-lookup"><span data-stu-id="55930-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of hello object (all other options).</span></span>  
<span data-ttu-id="55930-150">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="55930-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="55930-151">Если, к примеру, выполняется поиск в поддереве, вы получаете все объекты в одном подразделении.</span><span class="sxs-lookup"><span data-stu-id="55930-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="55930-152">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="55930-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="55930-153">В этой сетке можно выбрать объект, выберите **свойства**, и [следовать ей](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) из пространства соединителя источника hello через метавселенной hello и toohello целевого пространства соединителя.</span><span class="sxs-lookup"><span data-stu-id="55930-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from hello source connector space, through hello metaverse, and toohello target connector space.</span></span>

### <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="55930-154">Изменение пароля учетной записи hello AD DS</span><span class="sxs-lookup"><span data-stu-id="55930-154">Changing hello AD DS account password</span></span>
<span data-ttu-id="55930-155">При изменении пароля учетной записи hello hello служба синхронизации не будет tooon локальные изменения могут tooimport или экспорта AD.</span><span class="sxs-lookup"><span data-stu-id="55930-155">If you change hello account password, hello Synchronization Service will no longer be able tooimport/export changes tooon-premises AD.</span></span>   <span data-ttu-id="55930-156">Возможны следующие hello.</span><span class="sxs-lookup"><span data-stu-id="55930-156">You may see hello following:</span></span>

- <span data-ttu-id="55930-157">шаг Hello импорта и экспорта для hello соединителя AD завершится ошибкой «нет-start-учетные данные».</span><span class="sxs-lookup"><span data-stu-id="55930-157">hello import/export step for hello AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="55930-158">В средстве просмотра событий Windows журнал событий приложения hello содержит ошибку с Идентификатором 6000 событий и сообщений «hello toorun управления агента «contoso.com» не удалось, так как hello учетные данные были заданы неверно.»</span><span class="sxs-lookup"><span data-stu-id="55930-158">Under Windows Event Viewer, hello application event log contains an error with Event ID 6000 and message “hello management agent “contoso.com” failed toorun because hello credentials were invalid.”</span></span>

<span data-ttu-id="55930-159">tooresolve hello выполните обновление учетной записи пользователя hello AD DS с помощью следующих hello:</span><span class="sxs-lookup"><span data-stu-id="55930-159">tooresolve hello issue, update hello AD DS user account using hello following:</span></span>


1. <span data-ttu-id="55930-160">Запустите hello Synchronization Service Manager (служба → НАЧАЛА синхронизации).</span><span class="sxs-lookup"><span data-stu-id="55930-160">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="55930-161">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="55930-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="55930-162">Go toohello **соединители** вкладки.</span><span class="sxs-lookup"><span data-stu-id="55930-162">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="55930-163">Выберите hello соединителя AD, являющийся hello настроенных toouse учетной записи службы AD DS.</span><span class="sxs-lookup"><span data-stu-id="55930-163">Select hello AD Connector which is configured toouse hello AD DS account.</span></span>
4. <span data-ttu-id="55930-164">В разделе "Действия" выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="55930-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="55930-165">В всплывающем диалоговом окне приветствия выберите подключение tooActive леса:</span><span class="sxs-lookup"><span data-stu-id="55930-165">In hello pop-up dialog, select Connect tooActive Directory Forest:</span></span>
6. <span data-ttu-id="55930-166">Имя леса Hello указывает hello соответствующего в локальной среде AD.</span><span class="sxs-lookup"><span data-stu-id="55930-166">hello Forest name indicates hello corresponding on-prem AD.</span></span>
7. <span data-ttu-id="55930-167">имя пользователя Hello Указывает учетную запись доменных служб Active Directory hello AD, используемый для синхронизации.</span><span class="sxs-lookup"><span data-stu-id="55930-167">hello User name indicates hello AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="55930-168">Введите в текстовом поле пароля hello hello новый пароль для учетной записи hello AD DS ![Azure AD подключения синхронизации шифрования ключа служебной программы](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="55930-168">Enter hello new password of hello AD DS account in hello Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="55930-169">Нажмите кнопку ОК toosave hello новый пароль и перезапустите hello служба синхронизации tooremove hello старый пароль из кэша памяти.</span><span class="sxs-lookup"><span data-stu-id="55930-169">Click OK toosave hello new password and restart hello Synchronization Service tooremove hello old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="55930-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55930-170">Next steps</span></span>
<span data-ttu-id="55930-171">Дополнительные сведения о hello [синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) конфигурации.</span><span class="sxs-lookup"><span data-stu-id="55930-171">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="55930-172">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="55930-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
