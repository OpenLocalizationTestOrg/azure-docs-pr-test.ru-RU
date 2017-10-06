---
title: "Доменные службы Azure Active Directory: руководство по администрированию | Документация Майкрософт"
description: "Создание подразделения в управляемых доменах доменных служб Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a>Создание подразделения в управляемом домене доменных служб Azure AD
Управляемые домены доменных служб Azure AD включают два встроенных контейнера: "Компьютеры AADDC" и "Пользователи AADDC". Hello «AADDC компьютеры», контейнер содержит объекты-компьютеры для всех компьютеров, являющихся присоединены toohello управляемый домен. контейнер «Пользователи AADDC» Hello включает в себя пользователей и групп в клиенте Azure AD hello. В некоторых случаях может быть toocreate необходимых учетных записей служб на рабочих нагрузок toodeploy домена управляемых hello. Для этой цели можно создать пользовательские организационное подразделение (OU) на управляемый домен hello и создание учетных записей службы в этом Подразделении. В этой статье показано, как toocreate Подразделения управляемого домена.

## <a name="before-you-begin"></a>Перед началом работы
tooperform hello задачи, перечисленные в этой статье, необходимо:

1. Действующая **подписка Azure**.
2. **Каталог Azure AD** — синхронизированный с локальным каталогом или каталогом только для облака.
3. **Доменные службы Azure AD** должна быть включена для каталога hello Azure AD. Если вы еще не сделали этого, выполните все действия hello hello [руководство по началу работы](active-directory-ds-getting-started.md).
4. Домену виртуальной машины с которого осуществляется управление доменными службами hello Azure AD управляемого домена. Если у вас нет такой виртуальной машины, выполните все задачи hello, описанные в статье hello [к домену Windows виртуальной машины tooa управляемых](active-directory-ds-admin-guide-join-windows-vm.md).
5. Требуются учетные данные hello **группы «Администраторы AAD контроллера домена» toohello принадлежность учетной записи пользователей** в вашем каталоге toocreate пользовательские Подразделения управляемого домена.

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a>Установка средств администрирования AD на виртуальной машине, присоединенной к домену, для удаленного администрирования
Управляемый доменов доменные службы AD Azure можно управлять удаленно с помощью знакомых средств администрирования Active Directory например hello администрирования Active Directory Center (ADAC) или AD PowerShell. Администраторы клиента нет прав tooconnect toodomain контроллеров hello управляемого домена через удаленный рабочий стол. tooadminister Здравствуйте управляемый домен, установите средства администрирования hello AD на это управляемый домен присоединены к домену toohello виртуальной машины. См. в статье toohello под названием [администрирования Azure AD управляемого домена доменных служб](active-directory-ds-admin-guide-administer-domain.md) инструкции.

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a>Создайте подразделение в домене управляемого hello
Теперь, установлены средства администрирования hello AD на hello, присоединенных к домену виртуальной машины, toocreate эти средства можно использовать подразделения в домене управляемых hello. Выполните следующие шаги hello.

> [!NOTE]
> Только члены группы «Администраторы контроллера домена AAD» hello имеют hello toocreate полномочия, необходимые пользовательскому Подразделению. Убедитесь, что после выполнения действий от пользователя, который принадлежит группе toothis hello.
>
>

1. На начальном экране приветствия, нажмите кнопку **Администрирование**. Вы увидите Администрирование hello AD установлена на виртуальной машине hello.

    ![Средства администрирования, установленные на сервере](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Щелкните **Центр администрирования Active Directory**.

    ![Центр администрирования Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooview hello домена, щелкните имя домена hello в левой области hello (например, «contoso100.com»).

    ![Центр администрирования Active Directory — просмотр домена](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. Hello правой стороны **задачи** области, нажмите кнопку **New** под hello узел с именем домена. В этом примере мы щелкнуть **New** в узле «contoso100(local)» hello hello правой стороны **задачи** области.

    ![Центр администрирования Active Directory — новое подразделение](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. Вы увидите параметр hello toocreate организационную единицу. Нажмите кнопку **подразделение** toolaunch hello **Создание подразделения** диалогового окна.
6. В hello **Создание подразделения** диалогового окна, укажите **имя** для hello нового Подразделения. Укажите краткое описание hello Подразделение. Можно также установить hello **управляется** hello Подразделение в поле. toocreate Здравствуйте пользовательскому Подразделению, нажмите кнопку **ОК**.

    ![Центр администрирования Active Directory — диалоговое окно "Создание подразделения"](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. вновь созданные Подразделение Hello должен появиться в hello Центр администрирования AD (ADAC).

    ![Центр администрирования Active Directory — созданное подразделение](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a>Разрешения и параметры безопасности для созданных подразделений
По умолчанию hello пользователя (член группы администраторов контроллера домена, hello «AAD»), который создал приветствия пользовательскому Подразделению предоставляются права администратора (полный доступ) над hello Подразделение. Hello пользователя можно пойти дальше и предоставить права tooother пользователей или группы «Администраторы контроллера домена AAD» toohello в случае необходимости. Как показано на следующий снимок экрана приветствия, hello пользователя "bob@domainservicespreview.onmicrosoft.com", созданный hello «MyCustomOU» подразделения предоставляется полный контроль над ним.

 ![Центр администрирования Active Directory — безопасность нового подразделения](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a>Заметки об администрировании пользовательских подразделений
После создания пользовательского подразделения в нем можно создать пользователей, группы, компьютеры и учетные записи служб. Не удается переместить пользователей или группы из подразделения toocustom Подразделении «Пользователи AADDC» hello.

> [!WARNING]
> Учетные записи пользователей, группы, учетные записи служб и объекты-компьютеры, созданные в пользовательских подразделениях, недоступны в клиенте Azure AD. Другими словами эти объекты больше не показывать с помощью API Azure AD Graph hello, или в hello пользовательского интерфейса Azure AD. Они доступны только в управляемом домене доменных служб Azure AD.
>
>

## <a name="related-content"></a>Похожий контент
* [Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
* [Администрирование групповой политики в управляемом домене доменных служб Azure AD](active-directory-ds-admin-guide-administer-group-policy.md)
* [Центр администрирования Active Directory: приступая к работе](https://technet.microsoft.com/library/dd560651.aspx)
* [Пошаговое руководство по использованию учетных записей служб](https://technet.microsoft.com/library/dd548356.aspx)
