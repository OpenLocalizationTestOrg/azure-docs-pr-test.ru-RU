---
title: "Выбор типа установки Azure AD Connect | Документация Майкрософт"
description: "В этом разделе описывается способ установки hello tooselect введите toouse для Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a><span data-ttu-id="864e8-103">Выберите тип какие установки toouse для Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="864e8-103">Select which installation type toouse for Azure AD Connect</span></span>
<span data-ttu-id="864e8-104">При новой установке Azure AD Connect есть два типа установки: экспресс и пользовательская.</span><span class="sxs-lookup"><span data-stu-id="864e8-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="864e8-105">Этот раздел поможет toodecide, в котором параметр toouse во время установки.</span><span class="sxs-lookup"><span data-stu-id="864e8-105">This topic helps you toodecide which option toouse during installation.</span></span>

## <a name="express"></a><span data-ttu-id="864e8-106">Express</span><span class="sxs-lookup"><span data-stu-id="864e8-106">Express</span></span>
<span data-ttu-id="864e8-107">Express является наиболее распространенным типом hello и используется 90% всех новых установок.</span><span class="sxs-lookup"><span data-stu-id="864e8-107">Express is hello most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="864e8-108">Было спроектированный tooprovide конфигурацию, которая работает для наиболее распространенных сценариев клиента hello.</span><span class="sxs-lookup"><span data-stu-id="864e8-108">It was designed tooprovide a configuration that works for hello most common customer scenarios.</span></span>

<span data-ttu-id="864e8-109">Предполагается следующее:</span><span class="sxs-lookup"><span data-stu-id="864e8-109">It assumes:</span></span>

- <span data-ttu-id="864e8-110">У вас один локальный лес Active Directory.</span><span class="sxs-lookup"><span data-stu-id="864e8-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="864e8-111">У вас учетной записью администратора предприятия, которые можно использовать для установки hello.</span><span class="sxs-lookup"><span data-stu-id="864e8-111">You have an enterprise administrator account you can use for hello installation.</span></span>
- <span data-ttu-id="864e8-112">У вас не более 100 000 объектов в локальной службе Active Directory.</span><span class="sxs-lookup"><span data-stu-id="864e8-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="864e8-113">Вы получаете следующее:</span><span class="sxs-lookup"><span data-stu-id="864e8-113">You get:</span></span>

- <span data-ttu-id="864e8-114">[Синхронизация паролей](active-directory-aadconnectsync-implement-password-synchronization.md) из tooAzure в локальной среде AD для единого входа.</span><span class="sxs-lookup"><span data-stu-id="864e8-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises tooAzure AD for single sign-on.</span></span>
- <span data-ttu-id="864e8-115">Конфигурация, при которой синхронизируются [пользователи, группы, контакты и компьютеры с ОС Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="864e8-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="864e8-116">Синхронизация всех соответствующих объектов во всех доменах и подразделениях.</span><span class="sxs-lookup"><span data-stu-id="864e8-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="864e8-117">[Автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md) — включена toomake убедиться, что всегда hello последней доступной версии.</span><span class="sxs-lookup"><span data-stu-id="864e8-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled toomake sure you always use hello latest available version.</span></span>

<span data-ttu-id="864e8-118">Когда еще можно использовать экспресс-установку:</span><span class="sxs-lookup"><span data-stu-id="864e8-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="864e8-119">Если вы не хотите toosynchronize всех подразделений, можно по-прежнему использовать Express и на последней странице hello, отмените выделение **запуска процесса синхронизации hello...** *.</span><span class="sxs-lookup"><span data-stu-id="864e8-119">If you do not want toosynchronize all OUs, you can still use Express and on hello last page, unselect **Start hello synchronization process...***.</span></span> <span data-ttu-id="864e8-120">Затем снова запустите мастер установки hello и изменить hello подразделений в [параметры конфигурации](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) и включите запланированной синхронизации.</span><span class="sxs-lookup"><span data-stu-id="864e8-120">Then run hello installation wizard again and change hello OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="864e8-121">Вы хотите tooenable одной из функций hello в Azure AD Premium, такие как обратная запись паролей.</span><span class="sxs-lookup"><span data-stu-id="864e8-121">You want tooenable one of hello features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="864e8-122">Сначала пройти через первоначальной установки express tooget hello завершена.</span><span class="sxs-lookup"><span data-stu-id="864e8-122">First go through express tooget hello initial installation completed.</span></span> <span data-ttu-id="864e8-123">Затем снова запустите мастер установки hello и изменить hello [параметры конфигурации](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="864e8-123">Then run hello installation wizard again and change hello [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="864e8-124">Пользовательская</span><span class="sxs-lookup"><span data-stu-id="864e8-124">Custom</span></span>
<span data-ttu-id="864e8-125">путь настроенного Hello разрешает множество дополнительных возможностей, чем версия express.</span><span class="sxs-lookup"><span data-stu-id="864e8-125">hello customized path allows many more options than express.</span></span> <span data-ttu-id="864e8-126">Он должен использоваться во всех случаях, где описано в предыдущем разделе, для быстрой настройки hello не является репрезентативной для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="864e8-126">It should be used in all cases where hello configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="864e8-127">Используйте в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="864e8-127">Use when:</span></span>

- <span data-ttu-id="864e8-128">У вас учетная запись администратора предприятия tooan доступ в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="864e8-128">You do not have access tooan enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="864e8-129">У вас есть более чем одном лесе или планирование toosynchronize более чем одном лесе в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="864e8-129">You have more than one forest or you plan toosynchronize more than one forest in hello future.</span></span>
- <span data-ttu-id="864e8-130">У вас доменов в лесу, недоступен с сервера hello Connect.</span><span class="sxs-lookup"><span data-stu-id="864e8-130">You have domains in your forest not reachable from hello Connect server.</span></span>
- <span data-ttu-id="864e8-131">При планировании toouse федерации или сквозной проверки подлинности пользователя при входе.</span><span class="sxs-lookup"><span data-stu-id="864e8-131">You plan toouse federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="864e8-132">Содержит более 100 000 объектов и требуют toouse полных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="864e8-132">You have more than 100,000 objects and need toouse a full SQL Server.</span></span>
- <span data-ttu-id="864e8-133">При планировании toouse фильтрации на основе группы и не только домен или фильтрация на основе Подразделения.</span><span class="sxs-lookup"><span data-stu-id="864e8-133">You plan toouse group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="864e8-134">Обновление с DirSync</span><span class="sxs-lookup"><span data-stu-id="864e8-134">Upgrade from DirSync</span></span>
<span data-ttu-id="864e8-135">Если вы используете DirSync, следуйте указаниям hello [обновление от DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade существующую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="864e8-135">If you are currently using DirSync, then follow hello steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade your existing configuration.</span></span> <span data-ttu-id="864e8-136">Есть два различных сценария обновления:</span><span class="sxs-lookup"><span data-stu-id="864e8-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="864e8-137">Подключение tooinstall обновления на месте на hello же сервера.</span><span class="sxs-lookup"><span data-stu-id="864e8-137">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="864e8-138">Параллельные развертывания tooinstall подключить на новом сервере, пока hello существующего сервера DirSync по-прежнему работает.</span><span class="sxs-lookup"><span data-stu-id="864e8-138">Parallel deployment tooinstall Connect on a new server while hello existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="864e8-139">Обновление из Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="864e8-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="864e8-140">Если вы используете Azure AD Sync, то можно выполнить hello [действия](active-directory-aadconnect-upgrade-previous-version.md) как при обновлении одного Connect версии tooa новой.</span><span class="sxs-lookup"><span data-stu-id="864e8-140">If you are currently using Azure AD Sync, then you can follow hello [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version tooa newer.</span></span> <span data-ttu-id="864e8-141">Есть два различных сценария обновления:</span><span class="sxs-lookup"><span data-stu-id="864e8-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="864e8-142">Подключение tooinstall обновления на месте на hello же сервера.</span><span class="sxs-lookup"><span data-stu-id="864e8-142">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="864e8-143">Tooinstall миграции ходу подключить на новом сервере при hello существующего сервера Azure AD Sync по-прежнему работает.</span><span class="sxs-lookup"><span data-stu-id="864e8-143">Swing-migration tooinstall Connect on a new server while hello existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="864e8-144">Миграция с FIM2010 или MIM2016</span><span class="sxs-lookup"><span data-stu-id="864e8-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="864e8-145">Если вы используете Forefront Identity Manager 2010 или Microsoft Identity Manager 2016 с hello соединителя Azure AD, единственным вариантом является миграция.</span><span class="sxs-lookup"><span data-stu-id="864e8-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with hello Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="864e8-146">Следуйте инструкциям hello в [миграции ходу](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="864e8-146">Follow hello steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="864e8-147">В шагах hello замените все упоминания Azure AD Sync FIM2010/MIM2016.</span><span class="sxs-lookup"><span data-stu-id="864e8-147">In hello steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="864e8-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="864e8-148">Next steps</span></span>
<span data-ttu-id="864e8-149">В зависимости от настройки hello выбора toouse, используйте hello таблицы из левой toofind содержимого toohello статью с hello подробные инструкции.</span><span class="sxs-lookup"><span data-stu-id="864e8-149">Depending on hello option you have selected toouse, use hello table of content toohello left toofind your article with hello detailed steps.</span></span>
