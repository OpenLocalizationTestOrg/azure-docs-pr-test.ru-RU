---
title: "Синхронизация aaaAzure AD Connect служб компонентов и конфигурации | Документы Microsoft"
description: "Описываются функциональные возможности службы синхронизации Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="f2c87-103">Функции службы синхронизации Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f2c87-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="f2c87-104">функция синхронизации Hello Azure AD Connect состоит из двух компонентов:</span><span class="sxs-lookup"><span data-stu-id="f2c87-104">hello synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="f2c87-105">Hello локальный компонент с именем **синхронизации Azure AD Connect**, который также называется **модуль синхронизации**.</span><span class="sxs-lookup"><span data-stu-id="f2c87-105">hello on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="f2c87-106">Hello службы, размещенные в Azure AD, также известный как **служба синхронизации Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="f2c87-106">hello service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="f2c87-107">В этом разделе объясняется, как hello следующие функции для hello **служба синхронизации Azure AD Connect** работы и как можно настроить их с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2c87-107">This topic explains how hello following features of hello **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="f2c87-108">Эти параметры настраиваются при hello [Azure Active Directory модуля для Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="f2c87-108">These settings are configured by hello [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="f2c87-109">Он загружается и устанавливается отдельно от Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f2c87-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="f2c87-110">Hello командлеты, описанные в этом разделе были представлены в hello [марта 2016 г (сборка 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="f2c87-110">hello cmdlets documented in this topic were introduced in hello [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="f2c87-111">Если у вас hello командлеты, описанные в этом разделе или они не создают hello же привести, а затем убедитесь, что при запуске hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="f2c87-111">If you do not have hello cmdlets documented in this topic or they do not produce hello same result, then make sure you run hello latest version.</span></span>

<span data-ttu-id="f2c87-112">Конфигурация toosee hello в вашем каталоге Azure AD, запустите `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="f2c87-112">toosee hello configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="f2c87-113">![Результат вызова командлета Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="f2c87-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="f2c87-114">Многие из этих параметров могут быть изменены только службой Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f2c87-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="f2c87-115">Hello следующие параметры могут быть настроены с `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="f2c87-115">hello following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="f2c87-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="f2c87-116">DirSyncFeature</span></span> | <span data-ttu-id="f2c87-117">Комментарий</span><span class="sxs-lookup"><span data-stu-id="f2c87-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="f2c87-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="f2c87-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="f2c87-119">Позволяет toojoin объектов userPrincipalName в адресе tooprimary SMTP сложения.</span><span class="sxs-lookup"><span data-stu-id="f2c87-119">Allows objects toojoin on userPrincipalName in addition tooprimary SMTP address.</span></span> |
| [<span data-ttu-id="f2c87-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="f2c87-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="f2c87-121">Позволяет hello hello синхронизации ядра tooupdate атрибут userPrincipalName управляемых лицензированных пользователей (нефедеративных).</span><span class="sxs-lookup"><span data-stu-id="f2c87-121">Allows hello sync engine tooupdate hello userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="f2c87-122">После включения функции отключить ее нельзя.</span><span class="sxs-lookup"><span data-stu-id="f2c87-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="f2c87-123">С 24 августа 2016 года hello функция *повторяющийся атрибут устойчивости* включена по умолчанию для новых Azure каталогов AD.</span><span class="sxs-lookup"><span data-stu-id="f2c87-123">From August 24, 2016 hello feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="f2c87-124">Эта функция будет постепенно активирована и включена для каталогов, созданных до этой даты.</span><span class="sxs-lookup"><span data-stu-id="f2c87-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="f2c87-125">Если каталог имеет о tooget эта функция включена, вы получите уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="f2c87-125">You will receive an email notification when your directory is about tooget this feature enabled.</span></span>
> 
> 

<span data-ttu-id="f2c87-126">Hello следующие параметры настраиваются для Azure AD Connect и не может изменяться функцией `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="f2c87-126">hello following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="f2c87-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="f2c87-127">DirSyncFeature</span></span> | <span data-ttu-id="f2c87-128">Комментарий</span><span class="sxs-lookup"><span data-stu-id="f2c87-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="f2c87-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="f2c87-129">DeviceWriteback</span></span> |[<span data-ttu-id="f2c87-130">Azure AD Connect: включение обратной записи устройств</span><span class="sxs-lookup"><span data-stu-id="f2c87-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="f2c87-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="f2c87-131">DirectoryExtensions</span></span> |[<span data-ttu-id="f2c87-132">Синхронизация Azure AD Connect: расширения каталогов</span><span class="sxs-lookup"><span data-stu-id="f2c87-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="f2c87-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="f2c87-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="f2c87-134">Позволяет toobe атрибут на карантин, если он является копией другого объекта, а не сбой hello весь объект во время экспорта.</span><span class="sxs-lookup"><span data-stu-id="f2c87-134">Allows an attribute toobe quarantined when it is a duplicate of another object rather than failing hello entire object during export.</span></span> |
| <span data-ttu-id="f2c87-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="f2c87-135">PasswordSync</span></span> |[<span data-ttu-id="f2c87-136">Реализация синхронизации паролей с помощью службы Azure AD Connect Sync</span><span class="sxs-lookup"><span data-stu-id="f2c87-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="f2c87-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="f2c87-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="f2c87-138">Предварительная версия. Обратная запись групп</span><span class="sxs-lookup"><span data-stu-id="f2c87-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="f2c87-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="f2c87-139">UserWriteback</span></span> |<span data-ttu-id="f2c87-140">Сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="f2c87-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="f2c87-141">Устойчивость повторяющихся атрибутов</span><span class="sxs-lookup"><span data-stu-id="f2c87-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="f2c87-142">Вместо завершения ошибкой tooprovision объекты с повторяющимися именами участников-пользователей, / proxyAddresses, hello дублирования атрибута «карантин» и назначается временное значение.</span><span class="sxs-lookup"><span data-stu-id="f2c87-142">Instead of failing tooprovision objects with duplicate UPNs / proxyAddresses, hello duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="f2c87-143">После устранения конфликта hello, hello временный элемент представляет имя участника-пользователя автоматически изменен toohello соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="f2c87-143">When hello conflict is resolved, hello temporary UPN is changed toohello proper value automatically.</span></span> <span data-ttu-id="f2c87-144">Дополнительные сведения см. в статье [Синхронизация удостоверений и устойчивость повторяющихся атрибутов](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="f2c87-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="f2c87-145">Мягкое сопоставление атрибута userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="f2c87-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="f2c87-146">Если эта функция включена, soft-match включена для имени участника-пользователя в дополнение toohello [основной SMTP-адрес](https://support.microsoft.com/kb/2641663), который всегда включен.</span><span class="sxs-lookup"><span data-stu-id="f2c87-146">When this feature is enabled, soft-match is enabled for UPN in addition toohello [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="f2c87-147">Soft-match используется toomatch существующих пользователей облака — в Azure AD с помощью локальных пользователей.</span><span class="sxs-lookup"><span data-stu-id="f2c87-147">Soft-match is used toomatch existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="f2c87-148">Если вам требуется toomatch локальных учетных записей AD с существующие учетные записи, созданные в облаке hello и вы не используете Exchange Online, а затем эта возможность полезна.</span><span class="sxs-lookup"><span data-stu-id="f2c87-148">If you need toomatch on-premises AD accounts with existing accounts created in hello cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="f2c87-149">В этом сценарии обычно не нужно атрибут причина hello tooset SMTP в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="f2c87-149">In this scenario, you generally don’t have a reason tooset hello SMTP attribute in hello cloud.</span></span>

<span data-ttu-id="f2c87-150">Эта функция по умолчанию включена для создаваемых каталогов Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2c87-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="f2c87-151">Чтобы увидеть, включена ли эта функция, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f2c87-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="f2c87-152">Если эта функция отключена для вашего каталога Azure AD, ее можно включить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f2c87-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="f2c87-153">Синхронизация обновлений атрибута userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="f2c87-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="f2c87-154">Исторически атрибут UserPrincipalName toohello обновления, с помощью службы синхронизации hello из локальной был заблокирован, если выполняются оба из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="f2c87-154">Historically, updates toohello UserPrincipalName attribute using hello sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="f2c87-155">Hello пользователя управляется (нефедеративных).</span><span class="sxs-lookup"><span data-stu-id="f2c87-155">hello user is managed (non-federated).</span></span>
* <span data-ttu-id="f2c87-156">пользователь Hello не назначена лицензия.</span><span class="sxs-lookup"><span data-stu-id="f2c87-156">hello user has not been assigned a license.</span></span>

<span data-ttu-id="f2c87-157">Дополнительные сведения см. в разделе [пользователя не совпадают имена в Office 365, Azure или Intune hello локального имени участника-пользователя или альтернативному имени пользователя](https://support.microsoft.com/kb/2523192).</span><span class="sxs-lookup"><span data-stu-id="f2c87-157">For more details, see [User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="f2c87-158">Включение этой функции позволяет hello синхронизации ядра tooupdate hello userPrincipalName, измененные в локальной среде и использовать синхронизацию паролей при. Если используется федерация, эта функция не будет работать.</span><span class="sxs-lookup"><span data-stu-id="f2c87-158">Enabling this feature allows hello sync engine tooupdate hello userPrincipalName when it is changed on-premises and you use password sync. If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="f2c87-159">Эта функция по умолчанию включена для создаваемых каталогов Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2c87-159">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="f2c87-160">Чтобы увидеть, включена ли эта функция, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f2c87-160">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="f2c87-161">Если эта функция отключена для вашего каталога Azure AD, ее можно включить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f2c87-161">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="f2c87-162">После включения этой функции существующие значения атрибут userPrincipalName останутся неизменными.</span><span class="sxs-lookup"><span data-stu-id="f2c87-162">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="f2c87-163">При следующей смене hello userPrincipalName атрибут локальных hello обычный разностной синхронизации пользователей обновит hello имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2c87-163">On next change of hello userPrincipalName attribute on-premises, hello normal delta sync on users will update hello UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="f2c87-164">См. также</span><span class="sxs-lookup"><span data-stu-id="f2c87-164">See also</span></span>
* [<span data-ttu-id="f2c87-165">Службы синхронизации Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f2c87-165">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="f2c87-166">[Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="f2c87-166">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

