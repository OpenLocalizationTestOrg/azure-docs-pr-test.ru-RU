---
title: "toouse aaaHow Azure RemoteApp с учетными записями пользователей Office 365 | Документы Microsoft"
description: "Узнайте, как toouse Azure RemoteApp с мои учетные записи пользователей Office 365"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a>Как toouse Azure RemoteApp с учетными записями пользователей Office 365
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Если у вас есть подписка Office 365, у вас Azure Active Directory, хранит именам пользователей и пароли использовать tooaccess службам Office 365. Например если пользователям активировать Office 365 профессиональный плюс их проверку подлинности toocheck Azure AD для лицензий. Большинство пользователей будет как toouse hello же каталога с Azure RemoteApp.

При развертывании удаленного приложения Azure RemoteApp вы, скорее всего, будете использовать подписку, которая связана с другим каталогом Azure AD. В заказ toouse каталога Office 365, вы должны будете toomove hello подписки Azure в этот каталог.

Сведения о том, как Office 365 toodeploy клиентских приложений, в разделе [как toouse подписки Office 365 в Azure RemoteApp](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>Этап 1. Регистрация бесплатной подписки Azure Active Directory для Office 365
Если вы используете hello классический портал Azure, выполните шаги hello в [зарегистрировать бесплатную подписку Azure Active Directory](https://technet.microsoft.com/library/dn832618.aspx) tooyour tooget административного доступа Azure AD через портал управления Azure hello. В результате hello этого процесса необходимо будет toolog в hello портал Azure и видите свой каталог существует — на этом этапе вы не увидите гораздо более поскольку hello полной Azure подписку, которую вы используете Azure RemoteApp. находится в другом каталоге.

Запомнить hello имя и пароль учетной записи администратора hello, созданный на этом шаге — он понадобится на этапе 2.

При использовании портала Azure hello извлечь [как tooregister и активировать бесплатные Azure Active Directory, с помощью портала Office 365](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a>Этап 2: Изменение hello Azure AD, связанные с подпиской Azure.
Мы будем toochange вашей подписке Azure из текущего каталога в каталог hello Office 365, который мы работали на этапе 1.

Следуйте инструкциям hello, описанным в [изменение клиента Azure Active Directory hello в Azure RemoteApp](remoteapp-changetenant.md). Обратите особое внимание toohello следующие шаги:

* Шаг № 1. Если вы развернули удаленное приложение Azure RemoteApp (ARA) в этой подписке, удалите все учетные записи Azure AD из коллекций ARA перед выполнением дальнейших действий. Также можно удалить все существующие коллекции.
* Шаг № 2. Этот шаг является особенно важным. Требуется toouse учетную запись Майкрософт (например @outlook.com) как администратором службы для подписки hello; это, поскольку мы не может иметь все учетные записи пользователей из hello существующие подписки Azure AD присоединенного toohello — в этом мы не будет возможности toomove его tooa другой Azure AD.
* Шаг #4: При добавлении существующего каталога, hello система выдаст запрос toosign с учетной записью администратора hello для этого каталога. Убедитесь, что учетная запись администратора toouse hello из этапа 1.
* Шаг #5: Изменение hello родительский каталог tooyour Office 365 directory hello подписки. должен быть Hello конечный результат, что параметры -> подписок, подписки перечислены directory hello Office 365. 
  ![Перейдите в каталог родительского hello hello подписки](./media/remoteapp-o365user/settings.png)

На этом этапе подписки Azure RemoteApp связана с Office 365, Azure AD; hello существующих Office 365 учетных записей пользователей можно использовать с Azure RemoteApp!

