---
title: "aaaSign для использования Azure с учетной записью Office 365 | Документы Microsoft"
description: "Узнайте, как toocreate подписки Azure с помощью учетной записи Office 365"
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 129cdf7a-2165-483d-83e4-8f11f0fa7f8b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: cc331bf7222b5b03e740cb40a214bc13ef585f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-azure-subscription-with-your-office-365-account"></a>Регистрация для получения подписки Azure с помощью учетной записи Office 365
При наличии подписки Office 365, можно использовать ваш toocreate учетной записи Office 365 подписки Azure. Войдите в toohello [портал Azure](https://portal.azure.com/) с помощью Office 365 имя пользователя и пароль. Если требуется tooset копирование виртуальных машин или использовать другие службы Azure, необходимо зарегистрироваться для получения подписки Azure. Подписки Azure могут совместно использовать с другими пользователями и [tooyour toomanage доступ для управления доступом на основе ролей подписки Azure и ресурсов](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)

При наличии учетной записи Office 365 и подписки Azure, в разделе [связать tooan клиента Office 365 подписки Azure](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-azure-subscription-using-your-office-365-account"></a>Получение подписки Azure с помощью учетной записи Office 365

Зарегистрировавшись в Azure с помощью имени пользователя и пароля Office 365 вы сэкономьте время и предотвратите увеличение числа учетных записей. 

1. Зарегистрируйтесь на сайте [Azure.com](https://account.azure.com/signup?offer=MS-AZR-0044p&appId=docs). 
2. Войдите, используя имя пользователя и пароль Office 365. используемая учетная запись Hello не требуются права администратора toohave. Если имеется более одной учетной записи Office 365, убедитесь, что вы используете hello учетные данные для учетной записи Office 365 hello требуется tooassociate с подпиской Azure. 

   ![Снимок экрана, показывающий страницу входа hello.](./media/billing-use-existing-office-365-account-azure-subscription/billing-sign-in-with-office-365-account.png)

3. Введите hello необходимые сведения и полный hello процесс регистрации. Некоторые данные можно не указывать, если у вас уже есть учетная запись Office 365.

    ![Снимок экрана, показывающий hello форму регистрации.](./media/billing-use-existing-office-365-account-azure-subscription/billing-azure-sign-up-fill-information.png)

- Если необходимо tooadd другие пользователи в вашей организации toohello подписки Azure, см. раздел [Приступая к управлению доступом в hello портал Azure](../active-directory/role-based-access-control-what-is.md). 

## <a id="more-about-subs">Справочная информация о подписках Azure и Office 365</a>
Office 365 и Azure используйте hello Azure AD toomanage пользователями служб и подписок. Hello Azure directory аналогично контейнера, в котором можно группировать пользователей и подписок. toouse hello одинаковые учетные записи пользователей для подписки Azure и Office 365, вы должны убедиться, что toomake, hello Azure подписки создаются в hello же каталоге, что подписки Office 365 hello. Имейте в виду hello после точки.

* Подписка создается в каталоге.
* Пользователь должен принадлежать toodirectories
* Подписку попадает в каталоге hello hello пользователь, создавший подписку hello. Поэтому подписки Office 365 — связанные toohello учетную запись как подписки Azure.
* Подписки Azure, принадлежащие отдельным пользователям в каталоге hello
* Подписки Office 365 принадлежат самому каталогу hello. Пользователи с соответствующими разрешениями hello в каталоге hello могут управлять эти подписки.

![Снимок экрана, показывающий связь hello hello directory, пользователей и подписок.](./media/billing-use-existing-office-365-account-azure-subscription/19-background-information.png)

Дополнительные сведения см. в статье [Связь между подписками Azure и службой Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему. 
