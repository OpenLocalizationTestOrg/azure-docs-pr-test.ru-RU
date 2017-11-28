---
title: "Функции и конфигурация синхронизации Azure AD Connect | Документация Майкрософт"
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
ms.openlocfilehash: c2873510c280a2683c235cfdce3d2617c3b665cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-features"></a><span data-ttu-id="1cb61-103">Функции службы синхронизации Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="1cb61-103">Azure AD Connect sync service features</span></span>
<span data-ttu-id="1cb61-104">Средство синхронизации Azure AD Connect состоит из двух компонентов.</span><span class="sxs-lookup"><span data-stu-id="1cb61-104">The synchronization feature of Azure AD Connect has two components:</span></span>

* <span data-ttu-id="1cb61-105">Локальный компонент под названием **Синхронизация Azure AD Connect**, который также называется **модулем синхронизации**.</span><span class="sxs-lookup"><span data-stu-id="1cb61-105">The on-premises component named **Azure AD Connect sync**, also called **sync engine**.</span></span>
* <span data-ttu-id="1cb61-106">Размещенная в Azure AD служба, которая также называется **службой синхронизации Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="1cb61-106">The service residing in Azure AD also known as **Azure AD Connect sync service**</span></span>

<span data-ttu-id="1cb61-107">В этом разделе описаны следующие функции **службы синхронизации Azure AD Connect** и их настройка с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1cb61-107">This topic explains how the following features of the **Azure AD Connect sync service** work and how you can configure them using Windows PowerShell.</span></span>

<span data-ttu-id="1cb61-108">Для их настройки нужен [Модуль Azure Active Directory для Windows PowerShell](http://aka.ms/aadposh).</span><span class="sxs-lookup"><span data-stu-id="1cb61-108">These settings are configured by the [Azure Active Directory Module for Windows PowerShell](http://aka.ms/aadposh).</span></span> <span data-ttu-id="1cb61-109">Он загружается и устанавливается отдельно от Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="1cb61-109">Download and install it separately from Azure AD Connect.</span></span> <span data-ttu-id="1cb61-110">Описанные в этом разделе командлеты появились в [версии за март 2016 г. (сборка 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span><span class="sxs-lookup"><span data-stu-id="1cb61-110">The cmdlets documented in this topic were introduced in the [2016 March release (build 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1).</span></span> <span data-ttu-id="1cb61-111">Если у вас нет командлетов, описанных в этом разделе, или они дают другой результат, проверьте, используете ли вы последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="1cb61-111">If you do not have the cmdlets documented in this topic or they do not produce the same result, then make sure you run the latest version.</span></span>

<span data-ttu-id="1cb61-112">Для просмотра конфигурации каталога Azure AD выполните следующую команду: `Get-MsolDirSyncFeatures`.</span><span class="sxs-lookup"><span data-stu-id="1cb61-112">To see the configuration in your Azure AD directory, run `Get-MsolDirSyncFeatures`.</span></span>  
<span data-ttu-id="1cb61-113">![Результат вызова командлета Get-MsolDirSyncFeatures](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span><span class="sxs-lookup"><span data-stu-id="1cb61-113">![Get-MsolDirSyncFeatures result](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)</span></span>

<span data-ttu-id="1cb61-114">Многие из этих параметров могут быть изменены только службой Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="1cb61-114">Many of these settings can only be changed by Azure AD Connect.</span></span>

<span data-ttu-id="1cb61-115">Следующие параметры можно настроить с помощью `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="1cb61-115">The following settings can be configured by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="1cb61-116">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="1cb61-116">DirSyncFeature</span></span> | <span data-ttu-id="1cb61-117">Комментарий</span><span class="sxs-lookup"><span data-stu-id="1cb61-117">Comment</span></span> |
| --- | --- |
| [<span data-ttu-id="1cb61-118">EnableSoftMatchOnUpn</span><span class="sxs-lookup"><span data-stu-id="1cb61-118">EnableSoftMatchOnUpn</span></span>](#userprincipalname-soft-match) |<span data-ttu-id="1cb61-119">Позволяет присоединять объекты по атрибуту userPrincipalName в дополнение к основному адресу SMTP.</span><span class="sxs-lookup"><span data-stu-id="1cb61-119">Allows objects to join on userPrincipalName in addition to primary SMTP address.</span></span> |
| [<span data-ttu-id="1cb61-120">SynchronizeUpnForManagedUsers</span><span class="sxs-lookup"><span data-stu-id="1cb61-120">SynchronizeUpnForManagedUsers</span></span>](#synchronize-userprincipalname-updates) |<span data-ttu-id="1cb61-121">Позволяет модулю синхронизации обновлять атрибут userPrincipalName для управляемых или лицензированных пользователей (не являющихся федеративными).</span><span class="sxs-lookup"><span data-stu-id="1cb61-121">Allows the sync engine to update the userPrincipalName attribute for managed/licensed (non-federated) users.</span></span> |

<span data-ttu-id="1cb61-122">После включения функции отключить ее нельзя.</span><span class="sxs-lookup"><span data-stu-id="1cb61-122">After you have enabled a feature, it cannot be disabled again.</span></span>

> [!NOTE]
> <span data-ttu-id="1cb61-123">Начиная с 24 августа 2016 г. функция *Устойчивость повторяющихся атрибутов* включена по умолчанию для всех новых каталогов Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1cb61-123">From August 24, 2016 the feature *Duplicate attribute resiliency* is enabled by default for new Azure AD directories.</span></span> <span data-ttu-id="1cb61-124">Эта функция будет постепенно активирована и включена для каталогов, созданных до этой даты.</span><span class="sxs-lookup"><span data-stu-id="1cb61-124">This feature will also be rolled out and enabled on directories created before this date.</span></span> <span data-ttu-id="1cb61-125">Вы получите по электронной почте уведомление о включении этой функции для вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="1cb61-125">You will receive an email notification when your directory is about to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="1cb61-126">Следующие параметры настраиваются службой Azure AD Connect и не могут изменяться командлетом `Set-MsolDirSyncFeature`:</span><span class="sxs-lookup"><span data-stu-id="1cb61-126">The following settings are configured by Azure AD Connect and cannot be modified by `Set-MsolDirSyncFeature`:</span></span>

| <span data-ttu-id="1cb61-127">DirSyncFeature</span><span class="sxs-lookup"><span data-stu-id="1cb61-127">DirSyncFeature</span></span> | <span data-ttu-id="1cb61-128">Комментарий</span><span class="sxs-lookup"><span data-stu-id="1cb61-128">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="1cb61-129">DeviceWriteback</span><span class="sxs-lookup"><span data-stu-id="1cb61-129">DeviceWriteback</span></span> |[<span data-ttu-id="1cb61-130">Azure AD Connect: включение обратной записи устройств</span><span class="sxs-lookup"><span data-stu-id="1cb61-130">Azure AD Connect: Enabling device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |
| <span data-ttu-id="1cb61-131">DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="1cb61-131">DirectoryExtensions</span></span> |[<span data-ttu-id="1cb61-132">Синхронизация Azure AD Connect: расширения каталогов</span><span class="sxs-lookup"><span data-stu-id="1cb61-132">Azure AD Connect sync: Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [<span data-ttu-id="1cb61-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span><span class="sxs-lookup"><span data-stu-id="1cb61-133">DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency</span></span>](#duplicate-attribute-resiliency) |<span data-ttu-id="1cb61-134">Позволяет поместить атрибут, являющийся копией другого объекта, на карантин, вместо того чтобы прерывать весь процесс экспорта для этого объекта.</span><span class="sxs-lookup"><span data-stu-id="1cb61-134">Allows an attribute to be quarantined when it is a duplicate of another object rather than failing the entire object during export.</span></span> |
| <span data-ttu-id="1cb61-135">PasswordSync</span><span class="sxs-lookup"><span data-stu-id="1cb61-135">PasswordSync</span></span> |[<span data-ttu-id="1cb61-136">Реализация синхронизации паролей с помощью службы Azure AD Connect Sync</span><span class="sxs-lookup"><span data-stu-id="1cb61-136">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |
| <span data-ttu-id="1cb61-137">UnifiedGroupWriteback</span><span class="sxs-lookup"><span data-stu-id="1cb61-137">UnifiedGroupWriteback</span></span> |[<span data-ttu-id="1cb61-138">Предварительная версия. Обратная запись групп</span><span class="sxs-lookup"><span data-stu-id="1cb61-138">Preview: Group writeback</span></span>](active-directory-aadconnect-feature-preview.md#group-writeback) |
| <span data-ttu-id="1cb61-139">UserWriteback</span><span class="sxs-lookup"><span data-stu-id="1cb61-139">UserWriteback</span></span> |<span data-ttu-id="1cb61-140">Сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="1cb61-140">Not currently supported.</span></span> |

## <a name="duplicate-attribute-resiliency"></a><span data-ttu-id="1cb61-141">Устойчивость повторяющихся атрибутов</span><span class="sxs-lookup"><span data-stu-id="1cb61-141">Duplicate attribute resiliency</span></span>
<span data-ttu-id="1cb61-142">При подготовке объектов с повторяющимися именами участников-пользователей (UPN) или адресами прокси-сервера (proxyAddress) процесс не прерывается ошибкой, а повторяющийся атрибут помещается на карантин, и ему присваивается временное значение.</span><span class="sxs-lookup"><span data-stu-id="1cb61-142">Instead of failing to provision objects with duplicate UPNs / proxyAddresses, the duplicated attribute is “quarantined” and a temporary value is assigned.</span></span> <span data-ttu-id="1cb61-143">После разрешения конфликта временное имя участника-пользователя (UPN) будет автоматически исправлено на соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="1cb61-143">When the conflict is resolved, the temporary UPN is changed to the proper value automatically.</span></span> <span data-ttu-id="1cb61-144">Дополнительные сведения см. в статье [Синхронизация удостоверений и устойчивость повторяющихся атрибутов](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="1cb61-144">For more details, see [Identity synchronization and duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="userprincipalname-soft-match"></a><span data-ttu-id="1cb61-145">Мягкое сопоставление атрибута userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="1cb61-145">UserPrincipalName soft match</span></span>
<span data-ttu-id="1cb61-146">При включении этой функции к имени участника-пользователя, а также к [основному адресу SMTP](https://support.microsoft.com/kb/2641663), который всегда активен, может применяться мягкое сопоставление.</span><span class="sxs-lookup"><span data-stu-id="1cb61-146">When this feature is enabled, soft-match is enabled for UPN in addition to the [primary SMTP address](https://support.microsoft.com/kb/2641663), which is always enabled.</span></span> <span data-ttu-id="1cb61-147">Оно используется для сопоставления существующих облачных пользователей в Azure AD с локальными пользователями.</span><span class="sxs-lookup"><span data-stu-id="1cb61-147">Soft-match is used to match existing cloud users in Azure AD with on-premises users.</span></span>

<span data-ttu-id="1cb61-148">Эта функция удобна для сопоставления локальных учетных записей AD с существующими учетными записями, созданными в облаке, если вы не используете Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="1cb61-148">If you need to match on-premises AD accounts with existing accounts created in the cloud and you are not using Exchange Online, then this feature is useful.</span></span> <span data-ttu-id="1cb61-149">В такой ситуации устанавливать атрибут SMTP для облака обычно не нужно.</span><span class="sxs-lookup"><span data-stu-id="1cb61-149">In this scenario, you generally don’t have a reason to set the SMTP attribute in the cloud.</span></span>

<span data-ttu-id="1cb61-150">Эта функция по умолчанию включена для создаваемых каталогов Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1cb61-150">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="1cb61-151">Чтобы увидеть, включена ли эта функция, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1cb61-151">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

<span data-ttu-id="1cb61-152">Если эта функция отключена для вашего каталога Azure AD, ее можно включить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1cb61-152">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a><span data-ttu-id="1cb61-153">Синхронизация обновлений атрибута userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="1cb61-153">Synchronize userPrincipalName updates</span></span>
<span data-ttu-id="1cb61-154">Обновления атрибута userPrincipalName с помощью службы синхронизации из локальной среды блокируются за исключением тех случаев, когда выполняются два следующих условия:</span><span class="sxs-lookup"><span data-stu-id="1cb61-154">Historically, updates to the UserPrincipalName attribute using the sync service from on-premises has been blocked, unless both of these conditions are true:</span></span>

* <span data-ttu-id="1cb61-155">пользователь является управляемым (нефедеративным);</span><span class="sxs-lookup"><span data-stu-id="1cb61-155">The user is managed (non-federated).</span></span>
* <span data-ttu-id="1cb61-156">пользователю не назначена лицензия.</span><span class="sxs-lookup"><span data-stu-id="1cb61-156">The user has not been assigned a license.</span></span>

<span data-ttu-id="1cb61-157">Дополнительные сведения см. в статье [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192) (Имена пользователей в Office 365, Azure или Intune не совпадают с локальным именем участника-пользователя или альтернативным именем для входа).</span><span class="sxs-lookup"><span data-stu-id="1cb61-157">For more details, see [User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID](https://support.microsoft.com/kb/2523192).</span></span>

<span data-ttu-id="1cb61-158">Включение этой функции позволяет модулю синхронизации обновлять атрибут userPrincipalName при его изменении в локальной среде и при использовании синхронизации паролей.</span><span class="sxs-lookup"><span data-stu-id="1cb61-158">Enabling this feature allows the sync engine to update the userPrincipalName when it is changed on-premises and you use password sync.</span></span> <span data-ttu-id="1cb61-159">Если используется федерация, эта функция не будет работать.</span><span class="sxs-lookup"><span data-stu-id="1cb61-159">If you use federation, this feature is not supported.</span></span>

<span data-ttu-id="1cb61-160">Эта функция по умолчанию включена для создаваемых каталогов Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1cb61-160">This feature is on by default for newly created Azure AD directories.</span></span> <span data-ttu-id="1cb61-161">Чтобы увидеть, включена ли эта функция, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1cb61-161">You can see if this feature is enabled for you by running:</span></span>  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

<span data-ttu-id="1cb61-162">Если эта функция отключена для вашего каталога Azure AD, ее можно включить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1cb61-162">If this feature is not enabled for your Azure AD directory, then you can enable it by running:</span></span>  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

<span data-ttu-id="1cb61-163">После включения этой функции существующие значения атрибут userPrincipalName останутся неизменными.</span><span class="sxs-lookup"><span data-stu-id="1cb61-163">After enabling this feature, existing userPrincipalName values will remain as-is.</span></span> <span data-ttu-id="1cb61-164">Если в дальнейшем атрибут userPrincipalName изменится в локальной среде, то имя участника-пользователя будет обновлено при обычной синхронизации изменений для пользователей.</span><span class="sxs-lookup"><span data-stu-id="1cb61-164">On next change of the userPrincipalName attribute on-premises, the normal delta sync on users will update the UPN.</span></span>  

## <a name="see-also"></a><span data-ttu-id="1cb61-165">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="1cb61-165">See also</span></span>
* [<span data-ttu-id="1cb61-166">Службы синхронизации Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="1cb61-166">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="1cb61-167">[Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="1cb61-167">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

