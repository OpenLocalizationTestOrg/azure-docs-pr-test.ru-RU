---
title: "Группа aaaRestore удаленные Office 365 в Azure Active Directory | Документы Microsoft"
description: "Как toorestore удаленные из группы, Просмотр групп могут быть восстановлены и permamnently удаление группы в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>Восстановление удаленной группы Office 365 в Azure Active Directory

При удалении группы Office 365 в Azure Active Directory (Azure AD) hello, hello удалена группа зависимых, но не отображается в течение 30 дней от даты удаления hello. Это, чтобы группа hello и его содержимое можно восстановить при необходимости. Эта функциональность ограничен исключительно tooOffice 365 группы в Azure AD. Она недоступна для групп безопасности или групп рассылки.

> [!NOTE] 
> Не используйте `Remove-MsolGroup` поскольку очищает hello группы без возможности восстановления. Всегда используйте `Remove-AzureADMSGroup` группы toodelete Office 365. 

требуемые разрешения Hello toorestore группы может быть любым из следующих hello:

Роль  | Разрешения 
--------- | ---------
Администратор компании, партнер с поддержкой 2 уровня; администратор службы InTune | Восстановление любой удаленной группы Office 365 
Администратор учетных записей, партнер с поддержкой 1 уровня | Можно восстановить в любой удаленной группы Office 365, за исключением этих назначенного toohello роли администратора компании 
Пользователь | Восстановление любой удаленной группы Office 365, которая принадлежала им 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a>Представление hello удалить группы Office 365, которые будут доступны toorestore
следующие командлеты Hello может быть tooverify группы удалены hello используется tooview, один hello или те, которые вы хотите быть не еще удалены без возможности восстановления. Эти командлеты являются частью hello [модуля Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/). Дополнительные сведения об этом модуле можно найти в hello [Azure Active Directory PowerShell версии 2](/powershell/azure/install-adv2?view=azureadps-2.0) статьи.

1.  Запустите следующий командлет toodisplay удалить группы Office 365 в клиенте, по-прежнему доступны toorestore hello.
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  Кроме того Если вы знаете objectID hello определенной группы (и его можно получить из командлета hello в шаге 1) выполнения hello, выполнив командлет tooverify, Здравствуйте, удаленные из определенной группы не еще был удален без возможности восстановления.
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a>Как toorestore удаленные группы Office 365
После проверки того, что группы hello toorestore по-прежнему доступны, группа удалена hello восстановления с одним hello следующие шаги. Если группа hello содержит документы, SP сайты или другие постоянные объекты, он может занять too24 часы toofully восстановления группы и ее содержимое.

1.  Выполнения hello следующие группы hello toorestore командлет и его содержимое.
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

Кроме того hello следующий командлет может выполняться toopermanently удалить hello удалить группу.
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>Как убедиться, что действие выполнено?
успешно восстановленных группы Office 365, запустите hello tooverify `Get-AzureADGroup –ObjectId <objectId>` командлет toodisplay сведения о группе hello. После восстановления hello завершения запроса:
- Hello группа отображается в левой навигационной панели hello на сервере Exchange
- Планирование Hello hello группы будут отображаться в планировщик
- Станут доступны все сайты Sharepoint и их содержимое.
- Группа Hello может осуществляться из любого из конечных точек обмена hello и других рабочих нагрузок Office 365, поддерживающие группы Office 365


## <a name="next-steps"></a>Дальнейшие действия
В следующих статьях содержатся дополнительные сведения о группах Azure Active Directory.

* [Просмотр существующих групп](active-directory-groups-view-azure-portal.md)
* [Управление параметрами группы](active-directory-groups-settings-azure-portal.md)
* [Управление участниками группы](active-directory-groups-members-azure-portal.md)
* [Управление членством в группе](active-directory-groups-membership-azure-portal.md)
* [Управление динамическими правилами для пользователей в группе](active-directory-groups-dynamic-membership-azure-portal.md)
