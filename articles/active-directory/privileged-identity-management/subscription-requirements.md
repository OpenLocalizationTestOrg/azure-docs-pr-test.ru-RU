---
title: "подписки для управления удостоверениями aaaPrivileged - Azure | Документы Microsoft"
description: "Описание подписки hello и требования к лицензиям для использования в клиенте Azure AD Privileged Identity Management и управления им"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a>Требования к подписке для Azure Active Directory Privileged Identity Management

Azure AD Privileged Identity Management доступен как часть hello Premium P2 выпуск Azure AD. Дополнительные сведения о hello см. другие функции, P2 и сравнивает его tooPremium P1, [выпуски Azure Active Directory](../active-directory-editions.md).

>[!NOTE]
Время в предварительной версии управления привилегированными пользователями Azure Active Directory (Azure AD) было без выполнения проверок лицензий для службы клиента tootry hello.  Теперь, при достижении общей доступности Azure AD Privileged Identity Management пробной или платной подписки должны присутствовать для hello toocontinue клиента, с помощью управления привилегированными пользователями после декабря 2016 г.
  

## <a name="confirm-your-trial-or-paid-subscription"></a>Подтверждение пробной или платной подписки

Если точно неизвестно, имеет ли ваша организация пробную версию или приобрести подписку, можно проверить, существует ли подписка в клиенте с помощью команды hello, добавленные в Azure Active Directory модуля для Windows PowerShell версии 1. 
1. Откройте окно PowerShell.
2. Введите `Connect-MsolService` tooauthenticate имени пользователя в клиенте.
3. Укажите `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.

Эта команда возвращает список подписок hello в клиенте. Если нет строк, возвращаемых потребуется tooobtain Azure AD Premium P2 пробной версии, приобретения подписки Azure AD Premium P2 или toouse EMS E5 подписки Azure AD Privileged Identity Management.  tooget пробной версии и приступить к использованию Azure AD Privileged Identity Management, чтение [Приступая к работе с Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

Если эта команда возвращает строку, в какие SkuPartNumber «AAD_PREMIUM_P2» или «EMSPREMIUM» и IsTrial: «True», это указывает на пробную версию Azure AD Premium P2 в клиенте hello.  Если у вас P2 Azure AD Premium или EMS E5 Покупка подписки hello состояние подписки не включен, необходимо приобрести подписки P2 Azure AD Premium или EMS E5 toocontinue подписки, с помощью Azure AD Privileged Identity Management.

Azure AD Premium P2 доступна через [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), hello [откройте программу корпоративного лицензирования](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx)и hello [программы поставщиков облачных решений](https://partner.microsoft.com/en-US/cloud-solution-provider). Подписчики Azure и Office 365 также могут приобрести выпуск Active Directory Premium P2 через Интернет.  Дополнительные сведения о ценах Azure AD Premium и как tooorder сети можно найти в [ценах Azure Active Directory](https://azure.microsoft.com/en-us/pricing/details/active-directory/).

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a>Служба Azure AD Privileged Identity Management недоступна в клиенте

Служба Azure AD Privileged Identity Management будет недоступна в клиенте в следующих случаях:
- если организация использовала Azure AD Privileged Identity Management в режиме предварительного просмотра без приобретения подписки на Azure AD Premium P2 или EMS E5;
- если организация использовала пробную версию служб Azure AD Premium P2 или EMS E5, у которых истек срок действия;
- если организация использовала платную подписку, у которой истек срок действия.

Когда истекает срок действия подписки на Azure AD Premium P2 или EMS E5 или если организация, использовавшая Azure AD Privileged Identity Management в режиме предварительного просмотра, не приобретает подписку на Azure AD Premium P2 или EMS E5, происходит следующее:

- Постоянные роли назначения tooAzure AD ролей не затрагиваются.
- Hello расширения Azure AD Privileged Identity Management в hello портал Azure, а также hello Graph API и интерфейсов PowerShell Azure AD Privileged Identity Management, будет больше не будут доступны для работы в привилегированном режиме tooactivate ролей пользователей, управление привилегированный доступ или выполнять проверки доступа привилегированных ролей.
- Назначения ролей соответствующих ролей Azure AD будут удалены, как пользователи больше не будет роли может tooactivate работы в привилегированном режиме.
- завершаются все действующие проверки доступа для ролей Azure AD и удаляются параметры конфигурации Azure AD Privileged Identity Management;
- Azure AD Privileged Identity Management прекращает отправку сообщений электронной почты об изменении назначений ролей.

## <a name="next-steps"></a>Дальнейшие действия

- [Приступая к работе с управлением привилегированными пользователями Azure AD](../active-directory-privileged-identity-management-getting-started.md)
- [Роли в службе управления привилегированными пользователями Azure AD](../active-directory-privileged-identity-management-roles.md)
