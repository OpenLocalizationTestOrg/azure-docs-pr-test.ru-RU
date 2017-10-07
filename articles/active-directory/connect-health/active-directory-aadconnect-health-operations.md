---
title: "aaaAzure операций Active Directory Connect Health"
description: "В этой статье описаны дополнительные операции, которые можно выполнить после развертывания Azure AD Connect Health."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Операции Azure Active Directory Connect Health
В этом разделе описывается hello различные операции, выполняемые с помощью работоспособности подключения Azure Active Directory (Azure AD).

## <a name="enable-email-notifications"></a>Включение уведомлений по электронной почте
Можно настроить уведомления по электронной почте toosend службы Azure AD Connect Health hello при оповещения указывают, инфраструктуры удостоверений неработоспособен. Они будут отправляться при создании оповещения, а также если оно разрешено.

![Снимок экрана окна настройки уведомлений по электронной почте в Azure AD Connect Health](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> По умолчанию отправка уведомлений по электронной почте включена.
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>уведомления по электронной почте tooenable Azure AD Connect Health
1. Откройте hello **оповещения** колонке hello службы, для которого требуется tooreceive уведомление по электронной почте.
2. На панели действий hello, нажмите кнопку **параметры уведомлений**.
3. На коммутаторе уведомления по электронной почте hello, выберите **ON**.
4. Установите флажок hello, если требуется, чтобы все уведомления по электронной почте tooreceive глобальных администраторов.
5. Уведомления по электронной почте tooreceive в любых адресов электронной почты, укажите их в hello **дополнительных получателей электронной почты** поле. tooremove адрес электронной почты из этого списка, щелкните правой кнопкой мыши запись hello и выберите **удалить**.
6. toofinalize hello изменения, нажмите кнопку **Сохранить**. Изменения вступят в силу только после сохранения.

## <a name="delete-a-server-or-service-instance"></a>Удаление экземпляра службы или сервера

В некоторых случаях может потребоваться tooremove сервер из отслеживаемых. Вот что нужно tooknow tooremove server из службы hello Azure AD Connect Health.

После удаления сервера, помните о следующих hello.

* При выполнении этого действия дальнейший сбор данных с этого сервера прекращается. Этот сервер будет удален из hello, наблюдение за службой. После этого действия не могут tooview новые оповещения, мониторинг или аналитические данные об использовании для этого сервера.
* Это действие не приводит к удалению hello агент работоспособности с сервера. Если вы не удалили агент работоспособности hello перед выполнением этого шага, могут отображаться toohello связанных ошибок агент работоспособности на сервере hello.
* Это действие не удаляет hello данные, собранные с этого сервера. Данные будут удалены в соответствии с hello политики хранения данных Azure.
* После выполнения этого действия, если требуется мониторинг toostart hello же сервере еще раз, необходимо удалить и переустановить hello агент работоспособности на этом сервере.

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>toodelete server из службы hello Azure AD Connect Health
Azure AD Connect Health для службы федерации Active Directory (AD FS) и Azure AD Connect (синхронизация):

1. Откройте hello **сервера** колонку из hello **список серверов** колонки, выбрав имя toobe hello server удалена.
2. На hello **сервера** колонке hello панели действий щелкните **удалить**.
3. Подтвердите, введя имя сервера hello в окне подтверждения hello.
4. Нажмите кнопку **Delete**(Удалить).

Azure AD Connect Health для доменных служб Azure Active Directory:

1. Откройте hello **контроллеры домена** панели мониторинга.
2. Удалить toobe контроллера домена выберите hello.
3. На панели действий hello, нажмите кнопку **удалить выбранные**.
4. Подтвердите сервера hello toodelete действие hello.
5. Нажмите кнопку **Delete**(Удалить).

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>Удаление экземпляра службы из службы Azure AD Connect Health
В некоторых случаях может потребоваться tooremove экземпляра службы. Вот теми, которые требуется экземпляра из службы hello Azure AD Connect Health tooknow tooremove службы.

После удаления экземпляра службы, следует учитывать следующие hello.

* Это действие удаляет текущий экземпляр службы hello из hello, наблюдение за службой.
* Это действие не удалить или удаления hello агент работоспособности из любого hello серверов, которые были отслеживаются как часть данного экземпляра службы. Если вы не удалили агент работоспособности hello перед выполнением этого шага, может видеть toohello связанных ошибок работоспособности агента на серверах hello.
* Все данные в этом экземпляре службы будут удалены в соответствии с hello политики хранения данных Azure.
* После выполнения этого действия toostart наблюдение за службой hello, удалите и переустановите hello агент работоспособности на всех серверах hello. После выполнения этого действия, если требуется мониторинг hello того же сервера еще раз, удалить, повторно установить и зарегистрировать toostart hello агент работоспособности на этом сервере.

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete экземпляр службы из службы hello Azure AD Connect Health
1. Откройте hello **службы** колонку из hello **список служб** колонке путем выбора нужных tooremove идентификатор hello service (имя фермы).
2. На hello **сервера** колонке hello панели действий щелкните **удалить**.
3. Подтвердите, введя имя службы hello в окне подтверждения hello (например: sts.contoso.com).
4. Нажмите кнопку **Delete**(Удалить).
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>Использование управления доступом на основе ролей
[Управления доступом на основе ролей (RBAC)](../role-based-access-control-configure.md) для Azure AD Connect Health обеспечивает доступ toousers и группам помимо глобальных администраторов. RBAC назначает ролей предназначен toohello пользователей и групп, а также предоставляет механизм toolimit hello Глобальные администраторы в каталоге.

### <a name="roles"></a>Роли
Azure AD Connect Health поддерживает следующие встроенные роли hello:

| Роль | Разрешения |
| --- | --- |
| Владелец |Владельцы могут *управление доступом* (например, назначить роли tooa пользователю или группе,) *просматривать все данные* (например, просматривать предупреждения) из портала hello и *изменить параметры* () Например, уведомления по электронной почте) в Azure AD Connect Health. <br>По умолчанию данная роль назначается глобальным администраторам Azure AD и не может быть изменена. |
| Участник |Участники могут *просматривать все данные* (например, просматривать предупреждения) из портала hello и *изменить параметры* (например, уведомления по электронной почте) в Azure AD Connect Health. |
| читатель. |Читатели могут *просматривать все данные* (например, просматривать предупреждения) из портала hello в Azure AD Connect Health. |

Все остальные роли (например, Администраторы доступа пользователя или пользователей DevTest Labs) иметь нет влияния tooaccess в Azure AD Connect Health, даже если hello роли доступны в порталах hello.

### <a name="access-scope"></a>Область доступа
Azure AD Connect Health поддерживает управление доступом на двух уровнях:

* **Все экземпляры службы**: это путь в большинстве случаев рекомендуется hello. Он позволяет управлять доступом для всех экземпляров службы (например, фермы ADFS) во всех типах ролей, отслеживаемых Azure AD Connect Health.
* **Экземпляр службы**: В некоторых случаях может потребоваться toosegregate доступа на основе типов роли или экземпляра службы. В этом случае вы можете управлять доступом на уровне экземпляра службы hello.  

Разрешение предоставляется, если пользователь имеет доступ в каталог hello или службы уровне экземпляра.

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>Разрешить пользователям или группам доступ tooAzure AD Connect Health
Hello следующие шаги показывают, как получить доступ к tooallow.
#### <a name="step-1-select-hello-appropriate-access-scope"></a>Шаг 1: Выберите область доступа hello
доступ пользователей на hello tooallow *все экземпляры службы* уровня в Azure AD Connect Health, откройте hello главной колонке в Azure AD Connect Health.<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>Шаг 2. Добавление пользователей и групп, а также назначение ролей
1. Из hello **Настройка** щелкните **пользователей**.<br>
   ![Снимок экрана главной колонки компонента управления доступом на основе ролей в Azure AD Connect Health с выделенной плиткой "Пользователи"](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. Выберите **Добавить**.
3. В hello **выберите роль** выберите роли (например, **владельца**).<br>
   ![Снимок экрана окна "Пользователи" компонента управления доступом на основе ролей в Azure AD Connect Health](./media/active-directory-aadconnect-health/RBAC_add.png)
4. Имя типа hello или идентификатор hello целевой пользователя или группы. Можно выбрать один или несколько пользователей или групп на hello то же время. Нажмите кнопку **Выбрать**.
   ![Снимок экрана окна "Пользователи" компонента управления доступом на основе ролей в Azure AD Connect Health](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. Нажмите кнопку **ОК**.<br>
6. После назначения роли hello hello пользователей и групп отображаются в списке hello.<br>
   ![Снимок экрана окна "Пользователи" компонента управления доступом на основе ролей в Azure AD Connect Health с выделенными новыми пользователями](./media/active-directory-aadconnect-health/RBAC_user_list.png)

Теперь hello перечислены пользователи и группы имеют доступ, в соответствии с tootheir, которым назначены роли.

> [!NOTE]
> * Глобальные администраторы всегда имеют полный доступ tooall hello операций, но не существуют в hello списка учетных записей глобальных администраторов.
> * функция Hello приглашения пользователей не поддерживается в Azure AD Connect Health.
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>Шаг 3: Hello колонке расположении совместно с пользователями или группами
1. После назначения разрешений пользователь может получить доступ к Azure AD Connect Health, перейдя по [этому адресу](http://aka.ms/aadconnecthealth).
2. В колонке hello hello пользователя можно закрепить колонку hello или разных частей, toohello панели мониторинга. Просто щелкните hello **toodashboard ПИН-код** значок.<br>
   ![Снимок экрана колонки закрепления компонента управления доступом на основе ролей в Azure AD Connect Health с выделенным значком "Закрепить колонку на панели мониторинга"](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> Пользователь с ролью hello чтения не может tooget расширения Azure AD Connect Health hello Azure Marketplace. Hello пользователя не удается выполнить toodo операцию необходимые «создать» hello таким образом. Hello пользователь по-прежнему может получить toohello колонки с переходом toohello предшествующий ссылку. Для последующего использования hello пользователя можно закрепить панель toohello колонке hello.
>
>

### <a name="remove-users-or-groups"></a>Удаление пользователей или групп
Можно удалить пользователя или группу добавлен tooAzure AD RBAC работоспособности подключения. Просто щелкните правой кнопкой мыши hello пользователя или группы и выберите **удалить**.<br>
![Снимок экрана окна "Пользователи" компонента управления доступом на основе ролей в Azure AD Connect Health с выделенной командой "Удалить"](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>Дальнейшие действия
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Установка агента Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Использование Azure AD Connect Health с AD FS](active-directory-aadconnect-health-adfs.md)
* [Использование Azure AD Connect Health для синхронизации](active-directory-aadconnect-health-sync.md)
* [Using Azure AD Connect Health with AD DS (Использование Azure AD Connect Health с AD DS)](active-directory-aadconnect-health-adds.md)
* [Часто задаваемые вопросы об Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health: история выпусков версий](active-directory-aadconnect-health-version-history.md)
