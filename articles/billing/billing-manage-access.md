---
title: "tooAzure доступа aaaManage выставления счетов с помощью ролей | Документы Microsoft"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>Управление сведениями о toobilling доступ для Azure с помощью управления доступом на основе ролей

Можно предоставить доступ для Azure выставления счетов toomembers сведений рабочей группы путем назначения одной hello следующие подписки tooyour роли пользователя: учетная запись администратора, администратор службы, соадминистратора, владельца, участника, чтения и чтения выставления счетов. Они бы toobilling доступа к данным в hello [портал Azure](https://portal.azure.com/), и они могут использовать hello [выставления счетов API-интерфейсы](billing-usage-rate-card-overview.md) tooprogrammatically получения счета (один раз согласился входящий) и сведения об использовании. Дополнительные сведения о том, кто может назначать роли и какие роли за что отвечают, см. в статье [Роли в Azure RBAC](../active-directory/role-based-access-built-in-roles.md).

## <a name="opt-in"></a>Разрешение дополнительных пользователей tooaccess счетов

Hello администратора учетной записи необходимо явно включить с помощью hello [портал Azure](https://portal.azure.com/) разрешить tooinvoices доступ для других пользователей, а также через API.

1. Здравствуйте, администратор учетной записи, выберите подписку из hello [колонке подписки](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) на портале Azure.

1. Выберите **счета** и затем **доступ к tooinvoices**.

    ![Снимок экрана показано, как toodelegate доступ к tooinvoices](./media/billing-manage-access/AA-optin.png)

1. Включить **на** hello доступа следуют сохранения изменений hello, tooallow пользователей в счет toodownload выделенных ролях подписки.

    ![Снимок экрана показывает tooinvoice доступ включен выключен toodelegate](./media/billing-manage-access/AA-optinAllow.png)

Включения защиты позволяет администратору службы, соадминистратора, владельца, участника, чтения и чтения выставления счетов hello подписки toodownload PDF счета в hello портал Azure. Однако накладные старше декабря 2016 являются toohello доступны только администратор учетной записи сейчас.

Hello администратора учетной записи можно также настроить toohave счета, отправляемых по электронной почте. toolearn более, в разделе [получить ваш счет в сообщении электронной почты](billing-download-azure-invoice-daily-usage-date.md).

## <a name="adding-users-toohello-billing-reader-role"></a>Добавление роли чтения выставления счетов toohello пользователей

Hello выставления счетов чтения роль имеет доступ только для чтения toosubscription данные для выставления счетов на портале Azure, а не tooservices доступа, таких как виртуальные машины и учетные записи хранения. Назначьте toosomeone роль чтения выставления счетов hello, требуется доступ к toohello данные для подписки выставления счетов, но не hello toomanage возможности Azure службы. Эта роль подходит для сотрудников организации, отвечающих за управление финансами и затратами для подписок Azure.

1. Выберите подписку из hello [колонке подписки](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) на портале Azure.

1. Выберите **Управление доступом (IAM)** и нажмите кнопку **Добавить**.

    ![Снимок экрана показывает IAM в колонке подписки hello](./media/billing-manage-access/select-iam.PNG)

1. Выберите **выставления счетов чтения** в hello **выберите роль** страницы.

    ![Снимок экрана показывает чтения выставление счетов в представлении всплывающее окно приветствия](./media/billing-manage-access/select-roles.PNG)

1. Введите hello электронной почты для пользователя hello tooinvite и нажмите щелкните **ОК** toosend hello приглашения.

    ![Снимок экрана, показывающий tooinvite tooenter электронной почты пользователя](./media/billing-manage-access/add-user.PNG)

1. Следуйте инструкциям в toolog hello приглашение по электронной почте, в качестве читателя выставления счетов.

    ![Снимок экрана, показывающий, что hello чтения выставления счетов можно увидеть на портале Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> Функция выставления счетов чтения Hello находится в предварительной версии и пока не поддерживает подписки enterprise (EA) или неглобальной облака.

## <a name="adding-users-tooother-roles"></a>Добавление ролей пользователей tooother

Пользователи с другими ролями, такими как владелец или участник, получают доступ не только к счетам, но и к службам Azure. см. Эти роли toomanage [добавить или изменить роли Администратор Azure, управлять hello подписки или службы](billing-add-change-azure-subscription-administrator.md).

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>Кто имеет доступ к hello [центр учетных записей](https://account.windowsazure.com)?

Toohello центр учетных записей можно выполнить только hello учетной записи администратора. Hello учетная запись администратора является владельцем юридических hello hello подписки. По умолчанию hello пользователя, который зарегистрировал или купил hello подписки Azure — hello учетной записи администратора, если не hello [владельца подписки был передан](billing-subscription-transfer.md) toosomebody else. Hello учетной записи администратора можно создавать подписки, отмены подписки, изменить hello адрес для выставления счетов для подписки и управление политиками доступа для hello подписки.

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.

Если у вас есть дополнительные вопросы, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.
