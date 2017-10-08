---
title: "aaaSetting копирование присоединения Azure AD для пользователей | Документы Microsoft"
description: "В этой статье объясняется, как администраторы могут настроить присоединение к Azure AD для регистрации локальных каталогов и устройств."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a>Настройка присоединения к Azure AD в организации
Перед настройкой присоединения Azure Active Directory (Azure AD соединения), вам требуется синхронизировать tooeither вверх вашего локального каталога пользователей toohello облака или вручную создать управляемых учетных записей в Azure AD.

Подробные инструкции для синхронизации вашей tooAzure пользователей в локальной среде AD рассматривается в [интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

toomanually Создание и управление пользователями в Azure AD см. в слишком[Управление пользователями в Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).

## <a name="set-up-device-registration"></a>Настройка регистрации устройств
1. Войдите на toohello портал Azure с правами администратора.
2. Выберите на левой панели hello **Active Directory**.
3. На hello **каталога** вкладке, выберите свой каталог.
4. Выберите hello **Настройка** вкладки.
5. Go toohello **устройств** раздела.
6. На hello **устройств** установите hello следующее:  
   * **МАКСИМАЛЬНОЕ число устройств на пользователя**: выберите hello максимальное число устройств, которые пользователь может располагать в Azure AD.  Если пользователь достигает этой квоты, он не будет дополнительных устройств может tooadd только после удаления одного или нескольких существующих устройств из.
   * **ТРЕБОВАНИЯ МНОГОФАКТОРНОЙ проверки Подлинности tooJOIN устройств**: пользователи могут быть обязательным tooprovide второй проверки подлинности коэффициент toojoin их устройства tooAzure AD. Дополнительные сведения о многофакторной проверке подлинности Azure см. в разделе [Приступая к работе с многофакторной проверкой подлинности в Azure в облаке hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).
   * **Пользователи могут устройств присоединения AZURE AD**: выберите hello пользователей и групп, которые допускаются tooAzure устройств toojoin AD.
   * **Дополнительные АДМИНИСТРАТОРЫ ON AZURE AD к УСТРОЙСТВАМ, ПРИСОЕДИНЕННЫМ**: С Azure AD Premium или hello Enterprise Mobility Suite (EMS), можно выбрать пользователей, которым предоставляются права локального администратора toohello устройства. По умолчанию права локального администратора предоставляются глобальным администраторам и владельцам устройств.

<center>![Настройка регистрации устройств](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center>

После настройки присоединения Azure AD для пользователей, они могут подключаться tooAzure AD через их корпоративных и личных устройств.

Ниже приведены три сценария hello tooenable можно использовать ваш tooset пользователей копирование присоединения Azure AD.

* Пользователю о необходимости присоединиться устройства, принадлежащие компании непосредственно tooAzure AD.
* Пользователей присоединения к домену принадлежащие компании устройства toohello локальной Active Directory и затем расширить tooAzure устройства hello AD.
* Добавление пользователей работы или учебную учетные записи tooWindows на личных устройствах

## <a name="additional-information"></a>Дополнительная информация
* [Windows 10 для предприятия hello: способов toouse устройств для работы](active-directory-azureadjoin-windows10-devices-overview.md)
* [Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Сценарии использования для присоединения к Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Подключитесь к домену устройства tooAzure AD для Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Настройка присоединения к Azure AD](active-directory-azureadjoin-setup.md)

