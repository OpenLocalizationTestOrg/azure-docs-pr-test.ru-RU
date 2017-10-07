---
title: "истечение срока действия в Azure Active Directory группы aaaPreview Office 365 | Документы Microsoft"
description: "Сопоставление групп tooset копирование истечения срока действия для Office 365 в Azure Active Directory (Предварительная версия)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a>Настройка срока действия групп Office 365 (предварительная версия)

Теперь вы можете управлять жизненным циклом hello групп Office 365, задав истечение срока действия для выбранных групп Office 365. После установки этот срок действия, владельцы этих групп — запрос toorenew их группы, если они по-прежнему требуются группы hello. Все группы Office 365, которые не будут обновлены, будут удалены. Любой группы Office 365, который был удален, можно восстановить в течение 30 дней владельцев группы hello или администратором hello.  


> [!NOTE]
> Срок действия можно задать только для групп Office 365.
>
> Для этого требуется наличие лицензии Azure AD Premium:
>   - Здравствуйте, администратор, настраивающий параметры истечения срока действия hello для приветствия клиента
>   - Все члены группы hello, выбранные для этого параметра

## <a name="set-office-365-groups-expiration"></a>Настройка срока действия групп Office 365

1. Откройте hello [Центр администрирования Azure AD](https://aad.portal.azure.com) с учетной записью, которая является глобальным администратором в клиенте Azure AD.

2. Откройте страницу Azure AD и щелкните **Пользователи и группы**.

3. Выберите **параметры групповой** , а затем выберите **истечение срока действия** параметры истечения срока действия tooopen hello.
  
  ![Колонка "Срок действия"](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. На hello **истечение срока действия** колонку, вы можете:

  * Задать время существования группы hello в днях. Можно выбрать один из hello предустановленный набор значений или пользовательское значение (должно быть 31 дня или больше). 
  * Укажите адрес электронной почты, где должны отправляться уведомления об окончания срока действия и обновления hello при группы не имеет владельца. 
  * Выбрать, срок действия каких групп Office 365 может истечь. Можно включить истечение срока действия для **все** группы Office 365, можно выбрать один из группы Office 365 hello, или выбрать **нет** отключение истечения срока действия для всех групп.
  * По завершении сохраните параметры, нажав кнопку **Сохранить**.

Инструкции hello как toodownload и установка срока действия tooconfigure модуль Microsoft PowerShell для группы Office 365 с помощью PowerShell см. в разделе [модуля Azure Active Directory V2 PowerShell - общедоступный выпуск предварительной версии 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).

Уведомления по электронной почте, подобные данному, отправляются владельцев группы Office 365 toohello 30 дней, 15 дней и 1 день предыдущего tooexpiration hello группы.

![Уведомление по электронной почте о истечении срока действия](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

Владелец группы Hello можно выбрать **обновления группы** toorenew hello группы Office 365, или можно выбрать **Go toogroup** toosee hello элементы и другие сведения о hello группы.

По истечении срока действия группы hello группа удаляется один день после даты окончания срока действия hello. Уведомление по электронной почте, подобные данному, отправляется владельцев группы toohello Office 365, уведомляющее их о hello истечение срока действия и последующего удаления группы Office 365.

![Уведомление по электронной почте об удалении группы](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

Hello группы можно восстановить, выбрав **восстановления группы** либо используя командлеты PowerShell, как описано в [Группа восстановление удаленных Office 365 в Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-RESTORE-Azure-Portal).
    
Если hello группу, в которую производится восстановление содержит документы, сайтов SharePoint или другие постоянные объекты, он может занять too24 часы toofully восстановления hello группы и ее содержимое.

> [!NOTE]
> * При развертывании настройки срока окончания действия hello, возможно, некоторые группы, которые являются более старыми, чем период истечения срока действия hello. Эти группы не будут удалены немедленно, но являются значение too30 дней до истечения срока действия. Hello первого обновления уведомление по электронной почте отправляется в течение дня. Например, группа A создан 400 дней назад, и задать срок действия hello too180 дней. При применении параметры истечения срока действия группы A имеет 30 дней, прежде чем он будет удален, если владельца hello обновляет его.
> * Если это динамическая группа удаляется и восстановлены, он рассматривается как новую группу и повторно заполненная соответствующим toohello правило. Этот процесс может занять too24 часов.

## <a name="next-steps"></a>Дальнейшие действия
В следующих статьях содержатся дополнительные сведения о группах Azure AD.

* [Просмотр существующих групп](active-directory-groups-view-azure-portal.md)
* [Управление параметрами группы](active-directory-groups-settings-azure-portal.md)
* [Управление участниками группы](active-directory-groups-members-azure-portal.md)
* [Управление членством в группе](active-directory-groups-membership-azure-portal.md)
* [Управление динамическими правилами для пользователей в группе](active-directory-groups-dynamic-membership-azure-portal.md)
