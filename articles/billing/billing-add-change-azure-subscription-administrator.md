---
title: "aaaAdd или изменение роли подписки Azure admin | Документы Microsoft"
description: "Описывает способ tooadd или изменить Соадминистратор Azure, администратор службы и учетной записи администратора"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a>Добавление или изменение роли Администратор Azure, управлять hello подписки или службы
Вы можете изменить hello администратор Azure, который управляет подпиской Azure или управляет hello Azure службы, используемые в вашей подписке. tooview Azure сведения о выставлении счетов и управления подписками, необходимо войти в toohello [центр учетных записей](https://account.windowsazure.com/Home/Index) как Здравствуйте, администратор учетной записи. 

## <a name="add-an-admin-for-a-subscription"></a>Добавление администратора подписки
Администратор Azure можно добавить в hello портал Azure или в классический портал Azure hello.

**Портал Azure**

tooadd пользователя-администратора для подписки в hello портал Azure, вы даете им роль владельца hello. роль владельца Hello могут управлять только hello ресурсы в подписке hello, назначенный. Он не имеет подписок tooother прав доступа. Здравствуйте, владельцы, добавленные посредством hello [портал Azure](https://portal.azure.com) не может управлять ресурса в hello [классический портал Azure](https://manage.windowsazure.com).

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Выберите меню концентратора hello **подписки** > *hello подписку, которую нужно hello admin tooaccess*.

    ![Снимок экрана, на котором показана выбранная подписка](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. В колонке подписки hello выберите **(IAM) управления доступом к**.
4. Выберите **Добавить** > **Роль** > **Владелец**. Введите адрес электронной почты hello hello пользователя необходимо tooadd в качестве владельца пользователя выберите hello, а затем выберите **Сохранить**.

    ![Снимок экрана, показывающий hello выбранные роли-владельца](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Если требуется учетная запись владельца hello tooadd как соадминистратора в hello **(IAM) управления доступом к** страницы, щелкните правой кнопкой мыши пользователя hello и выберите **добавить как соадминистратора**. Эта функция в настоящее время доступна в [предварительной версии портала Azure](https://preview.portal.azure.com/). 

     ![Снимок экрана, на котором показаны элементы для добавления соадминистратора](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >Вам потребуется пользователя «Владелец» hello tooadd как соадминистратора Если hello пользователь должен toomanage hello служб Azure в [классический портал Azure](https://manage.windowsazure.com/).

    разрешение совместного администрирования tooremove hello, щелкните правой кнопкой мыши пользователя «соадминистратора» hello, а затем выберите **удалить соадминистратора**.

    ![Снимок экрана, на котором показаны элементы для удаления соадминистратора](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**классическом портале Azure**

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/).
2. В области навигации hello выберите **параметры**> **Администраторы**> **добавить**. </br>

    ![Снимок экрана, показывающий, как добавить кнопку в tooget toohello](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Введите адрес электронной почты hello hello пользователя, которому tooadd как соадминистратора и выберите hello подписки на hello tooaccess соадминистратора.</br>

    ![Снимок экрана, на котором показана выбранная подписка ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

Hello следующий адрес электронной почты могут быть добавлены в качестве Соадминистратора:

* **Учетная запись Майкрософт** (ранее идентификатор Windows Live ID). </br>
  Можно использовать в продуктах корпорации Майкрософт ориентированная на клиентов tooall toosign учетной записи Майкрософт и облачным службам, например Outlook (например, Hotmail), Скайп (MSN), OneDrive, Windows Phone и Xbox LIVE.
* **Organizational account**</br>
  Учетная запись организации — это учетная запись, созданная в каталоге Azure Active Directory. Hello учетная запись организации адрес указан в следующем формате:

    пользователь@&lt;домен&gt;.onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Изменение администратора службы для подписки
Только hello учетной записи администратора можно изменить hello администратора службы для подписки.

1. Войдите в слишком[центр учетных записей Azure](https://account.windowsazure.com/subscriptions) с помощью учетной записи администратора hello.
2. Выберите подписку hello требуется toochange.
3. На правой стороне hello, выберите **изменить подписку** сведения. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. В hello **АДМИНИСТРАТОРА службы** введите адрес электронной почты hello hello новому администратору службы. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a>Изменение учетной записи администратора hello
владение tootransfer hello Azure tooanother учетную запись, в разделе [Передача владения подпиской Azure](billing-subscription-transfer.md).

Настоятельно рекомендуется не удалять или переименовать адрес электронной почты учетной записи администратора hello. Вы можете увидеть неожиданные и нежелательные поведение с hello учетная запись Azure. Не может быть tooAzure возможности входа в систему с этой учетной записью, внести изменения учетной записи toohello или управление ресурсами с помощью этой учетной записи. 

## <a name="check-hello-account-administrator-of-hello-subscription"></a>Проверьте учетную запись администратора подписки hello hello
Если вы точно не знаете, кто является администратором учетной записи hello для вашей подписки, используйте следующие шаги toofind out hello.

  1. Войдите в toohello [портал Azure](https://portal.azure.com).
  2. Выберите меню концентратора hello **подписки**.
  3. Выберите hello подписку, которую вы хотите toocheck, а затем найдите в разделе **параметры**.
  4. Выберите **Свойства**. Здравствуйте, администратор учетной записи подписки hello отображается в hello **администратор учетной записи** поле.  

## <a name="types-of-azure-admin-accounts"></a>Типы учетных записей администратора Azure
 Учетная запись администратора, администратор службы и соадминистратор являются hello три вида ролей администратора в Microsoft Azure. Hello следующей таблице описаны hello различие между эти три роли администратора.

| Роль администратора | Ограничение | Description (Описание) |
| --- | --- | --- |
| Администратор учетной записи |Один на учетную запись Azure |Это является hello, кто зарегистрировал или приобрели подписки Azure и — hello авторизованным tooaccess [центр учетных записей](https://account.windowsazure.com/Home/Index) и выполнять различные задачи управления. Эти: теперь может toocreate подписки, отмены подписки, изменить hello выставления счетов для подписки и изменить hello администратора службы. |
| Администратор службы |Один на подписку Azure |Эта роль является авторизованным toomanage служб в hello [портал Azure](https://portal.azure.com). По умолчанию для новой подписки hello учетная запись администратора также является hello администратора службы. |
| Соадминистратор (ЦС) в hello [классический портал Azure](https://manage.windowsazure.com) |200 на подписку |Эта роль имеет hello же привилегии доступа как hello администратора службы, но нельзя изменить связь hello каталогов tooAzure подписки. |

Azure Active Directory ролевого управления доступом (RBAC) позволяет пользователям toobe добавлены toomultiple ролей. Дополнительные сведения см. в статье [Контроль доступа на основе ролей в Azure Active Directory](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Ограничения для учетных записей администратора
* Каждая подписка связывается с каталогом Azure AD (также известный как hello каталог по умолчанию). hello toofind каталог по умолчанию hello подписки связана, последовательно выберите toohello [классический портал Azure](https://manage.windowsazure.com/)выберите **параметры** > **подписки**. Проверьте hello подписки идентификатор toofind hello каталог по умолчанию.
* Если вы вошли в учетную запись Майкрософт, можно только добавить другие учетные записи Майкрософт или пользователей в каталог по умолчанию hello как Соадминистратора.
* Если вы выполняете вход с использованием учетной записи организации, вы можете добавлять другие учетные записи организации в своей организации в качестве соадминистраторов. Например, abby@contoso.com может добавить bob@contoso.com в качестве администратора службы или соадминистратора, но не может добавить john@notcontoso.com, если john@notcontoso.com не находится в каталоге по умолчанию. Пользователи, вошедшие в систему с учетными записями организации можно продолжить tooadd пользователей учетной записи Майкрософт в качестве администратора службы или Соадминистратором.
* Теперь, когда это возможно toosign в tooAzure с учетной записью организации, ниже приведены изменения hello tooService администратора и требования к учетной записи соадминистратора.

  | Метод входа | Добавить учетную запись Майкрософт или пользователей каталога по умолчанию в качестве соадминистратора или администратора службы? | Добавьте учетную запись организации в hello одной организации, как ЦС или SA? | Добавить учетную запись организации в другой организации в качестве соадминистратора или администратора службы? |
  | --- | --- | --- | --- |
  |  Учетная запись Майкрософт |Да |Нет |Нет |
  |  Учетная запись организации |Да |Да |Нет |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>Дополнительные сведения о контроле доступа к ресурсам и Active Directory
* toolearn Дополнительные сведения о как осуществляется доступ к ресурсам в Microsoft Azure в разделе [основные сведения о доступе к ресурсам в Azure](../active-directory/active-directory-understanding-resource-access.md).
* Дополнительные сведения об Azure Active Directory см. в статьях [Связь между подписками Azure и службой Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) и [Назначение ролей администратора в Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.
