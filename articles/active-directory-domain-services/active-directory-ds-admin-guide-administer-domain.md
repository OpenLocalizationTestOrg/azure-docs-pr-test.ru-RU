---
title: "Доменные службы Azure Active Directory: администрирование управляемого домена | Документация Майкрософт"
description: "Администрирование управляемых доменов доменных служб Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a>Администрирование управляемого домена доменных служб Azure Active Directory
В этой статье показано, как tooadminister доменных служб Azure Active Directory (AD) Управление домена.

## <a name="before-you-begin"></a>Перед началом работы
tooperform hello задачи, перечисленные в этой статье, необходимо:

1. Действующая **подписка Azure**.
2. **Каталог Azure AD** — синхронизированный с локальным каталогом или каталогом только для облака.
3. **Доменные службы Azure AD** должна быть включена для каталога hello Azure AD. Если вы еще не сделали этого, выполните все действия hello hello [руководство по началу работы](active-directory-ds-getting-started.md).
4. Объект **виртуальную машину к домену** из которой администрировать hello управляемого домена доменные службы Azure AD. Если у вас нет такой виртуальной машины, выполните все задачи hello, описанные в статье hello [к домену Windows виртуальной машины tooa управляемых](active-directory-ds-admin-guide-join-windows-vm.md).
5. Требуются учетные данные hello **группы «Администраторы AAD контроллера домена» toohello принадлежность учетной записи пользователей** в вашем каталоге tooadminister управляемого домена.

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a>Административные задачи, которые можно выполнять в управляемом домене
Члены группы «Администраторы контроллера домена AAD» hello, предоставляются права на hello управляемый домен, для выполнения их задач tooperform такие как:

* Присоедините машины toohello управляемый домен.
* Настройка встроенных hello объекта групповой Политики, для контейнеров «AADDC компьютеры» и «Пользователи AADDC» hello в hello управляемый домен.
* Для администрирования DNS на управляемый домен hello.
* Создавать и администрировать пользовательских подразделений (OU) в домене управляемого hello.
* Рост toocomputers административного доступа присоединен toohello управляемый домен.

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a>Административные права, которые не предоставляются в управляемом домене
Hello домена управляется корпорацией Майкрософт, включая действия, такие как исправления, наблюдения и создания резервных копий. Таким образом домен hello заблокирована, и у вас прав tooperform определенные административные задачи в домене hello. Некоторые примеры задач, которые нельзя выполнять, приведены ниже.

* Права администратора домена или администратора предприятия для управляемого домена hello не предоставляются.
* Не удается расширить схему hello hello управляемого домена.
* Не удается подключиться toodomain контроллеры hello управляемых с помощью удаленного рабочего стола.
* Не удается добавить домен управляемого toohello контроллеров домена.

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a>Задача 1. Подготовка виртуальной машины tooremotely присоединенных к домену Windows Server администрирование управляемого домена hello
Управляемые домены Azure AD доменных служб можно управлять с помощью знакомых средств администрирования Active Directory как hello администрирования Active Directory Center (ADAC) или AD PowerShell. Администраторы клиента нет прав tooconnect toodomain контроллеров hello управляемого домена через удаленный рабочий стол. Таким образом члены группы «Администраторы AAD контроллера домена» могут администрировать приветствия управляемые домены, удаленно с помощью средства администрирования AD в Windows Server или клиентский компьютер, — управляемый домен toohello присоединены к домену. Можно установить средства администрирования AD в качестве части необязательный компонент hello средств удаленного администрирования сервера (RSAT) на Windows Server и клиентских компьютерах, присоединенных к toohello управляемого домена.

Hello первым шагом является tooset виртуальную машину Windows Server, соединенных toohello управляемого домена. Инструкции приведены в статье toohello [к домену Windows Server виртуальной машины tooan доменные службы Azure AD управляемых](active-directory-ds-admin-guide-join-windows-vm.md).

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a>Удаленное администрирование управляемого домена hello с клиентского компьютера (например, Windows 10)
Hello инструкциям в этой статье использует hello tooadminister виртуальной машины Windows Server AAD DS управляемого домена. Однако также можно toouse toodo виртуальной машины Windows клиента (например, Windows 10) таким образом.

Вы можете [установить средства удаленного администрирования сервера (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) на виртуальной машине Windows клиента, следуя инструкциям hello на сайте TechNet.

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a>Задача 2 - средства администрирования установки Active Directory на виртуальной машине hello
Выполните следующие шаги tooinstall hello Администрирование Active Directory средств на виртуальную машину к домену hello hello. Для получения дополнительных сведений об [установке и использовании средств удаленного администрирования сервера](https://technet.microsoft.com/library/hh831501.aspx) перейдите на сайт TechNet.

1. Перейдите в слишком**виртуальные машины** узел в hello классический портал Azure. Выберите виртуальную машину hello, созданный в задаче 1 и нажмите кнопку **Connect** на панели команд hello hello нижней части окна hello.

    ![Подключение tooWindows виртуальной машины](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. Классический портал Hello предлагает tooopen или сохраните файл с расширением «.rdp», который является используется tooconnect toohello виртуальной машины. Щелкните файл tooopen hello, когда завершена загрузка.
3. В строке приветствия входа используйте hello учетные данные пользователей, принадлежащих группе «Администраторы контроллера домена AAD» toohello. Например, мы используем "bob@domainservicespreview.onmicrosoft.com" в нашем случае.
4. Hello начальном экране откройте **диспетчера сервера**. Нажмите кнопку **Добавить роли и компоненты** hello центральной панели среды hello окна диспетчера серверов.

    ![Запуск диспетчера серверов на виртуальной машине](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. На hello **перед началом** страница hello **мастера добавления ролей и компонентов**, нажмите кнопку **Далее**.

    ![Страница "Перед началом работы"](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. На hello **тип установки** оставьте hello **Установка ролей или компонентов** включенным и нажмите кнопку **Далее**.

    ![Страница "Тип установки"](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. На hello **Выбор сервера** выберите hello текущей виртуальной машины из пула серверов hello и нажмите кнопку **Далее**.

    ![Страница "Выбор сервера"](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. На hello **ролей сервера** щелкните **Далее**. Мы пропустить эту страницу, так как мы не производится установка любых ролей на сервере hello.
9. На hello **функции** щелкните tooexpand hello **средства удаленного администрирования сервера** узел и нажмите кнопку tooexpand hello **средства администрирования ролей** узла. Выберите **AD DS и AD LDS средства** компонент из списка hello средства администрирования ролей.

    ![Страница "Компоненты"](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. На hello **Подтверждение** щелкните **установить** tooinstall hello AD и средства AD LDS компонента на виртуальной машине hello. После успешного завершения установки компонента щелкните **закрыть** tooexit hello **Добавить роли и компоненты** мастера.

    ![Страница подтверждения](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a>Задача 3 — подключить tooand исследовать hello управляемого домена
Теперь, когда средства администрирования hello AD устанавливаются на hello, присоединенных к домену виртуальной машины, можно использовать эти средства tooexplore и администрирование управляемого домена hello.

> [!NOTE]
> Необходимо toobe членом группы «Администраторы контроллера домена AAD» hello, tooadminister hello управляемого домена.
>
>

1. На начальном экране приветствия, нажмите кнопку **Администрирование**. Вы увидите Администрирование hello AD установлена на виртуальной машине hello.

    ![Средства администрирования, установленные на сервере](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Щелкните **Центр администрирования Active Directory**.

    ![Центр администрирования Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooexplore hello домена, щелкните имя домена hello в левой области hello (например, «contoso100.com»). Обратите внимание на два контейнера, которые называются соответственно "Компьютеры AADDC" и "Пользователи AADDC".

    ![Центр администрирования Active Directory — просмотр домена](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. Щелкните контейнер hello вызывается **AADDC пользователей** toosee всех пользователей и групп, принадлежащих toohello управляемого домена. В этом контейнере должны отобразиться учетные записи и группы пользователей вашего клиента Azure AD. Отметим в данном примере, учетная запись пользователя для hello пользователя с именем «bob» и группу «Администраторы AAD контроллера домена», доступны в этом контейнере.

    ![Центр администрирования Active Directory — пользователи домена](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. Щелкните контейнер hello вызывается **AADDC компьютеры** toosee hello компьютеры присоединены toothis управляемый домен. Должна появиться запись для текущей виртуальной машины hello, — домен toohello присоединены к домену. Учетные записи компьютеров для всех компьютеров, которые будут присоединены toohello доменные службы Azure AD управляемого домена хранятся в этом контейнере «Компьютеры AADDC».

    ![Центр администрирования Active Directory — компьютеры, присоединенные к домену](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a>Похожий контент
* [Приступая к работе с доменными службами Azure AD](active-directory-ds-getting-started.md)
* [К домену Windows Server виртуальной машины tooan доменные службы Azure AD управляемого](active-directory-ds-admin-guide-join-windows-vm.md)
* [Развертывание средств удаленного администрирования сервера](https://technet.microsoft.com/library/hh831501.aspx)
