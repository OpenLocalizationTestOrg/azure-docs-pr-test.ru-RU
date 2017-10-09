---
title: "Доменные службы Azure Active Directory: администрирование DNS в управляемых доменах | Документация Майкрософт"
description: "Администрирование DNS в управляемых доменах доменных служб Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a>Администрирование DNS в управляемых доменах доменных служб Azure AD
Azure доменных служб Active Directory включает в себя сервер DNS (разрешение доменных имен), предоставляет разрешение DNS для домена управляемого hello. В некоторых случаях может потребоваться tooconfigure DNS в домене управляемых hello. Может потребоваться toocreate записи DNS для машины, которые не присоединены к домену toohello домена, настроить виртуальный IP-адресов для подсистем балансировки нагрузки или установки внешних DNS-серверы пересылки. По этой причине пользователям, которые входят в группу «Администраторы контроллера домена AAD» toohello предоставляются права администрирования DNS на управляемый домен hello.

## <a name="before-you-begin"></a>Перед началом работы
tooperform hello задачи, перечисленные в этой статье, необходимо:

1. Действующая **подписка Azure**.
2. **Каталог Azure AD** — синхронизированный с локальным каталогом или каталогом только для облака.
3. **Доменные службы Azure AD** должна быть включена для каталога hello Azure AD. Если вы еще не сделали этого, выполните все действия hello hello [руководство по началу работы](active-directory-ds-getting-started.md).
4. Объект **виртуальную машину к домену** из которой администрировать hello управляемого домена доменные службы Azure AD. Если у вас нет такой виртуальной машины, выполните все задачи hello, описанные в статье hello [к домену Windows виртуальной машины tooa управляемых](active-directory-ds-admin-guide-join-windows-vm.md).
5. Требуются учетные данные hello **группы «Администраторы AAD контроллера домена» toohello принадлежность учетной записи пользователей** в вашем каталоге tooadminister DNS для управляемого домена.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a>Задача 1. Подготовка tooremotely виртуальную машину к домену администрирование DNS для hello управляемого домена
Управляемый доменов доменные службы AD Azure можно управлять удаленно с помощью знакомых средств администрирования Active Directory например hello администрирования Active Directory Center (ADAC) или AD PowerShell. Аналогичным образом DNS для домена управляемого hello может управляться удаленно с помощью средства администрирования DNS-сервера hello.

В каталоге Azure AD у администраторов нет контроллеров toodomain tooconnect права на hello управляемого домена через удаленный рабочий стол. Члены группы «Администраторы контроллера домена AAD» hello администрирования управляемых доменов удаленно с помощью средства DNS-сервера с компьютера Windows Server или клиентской, соединенных toohello управляемого домена DNS. Средства DNS-сервера можно установить как часть необязательный компонент hello средств удаленного администрирования сервера (RSAT) на Windows Server и клиентские машины присоединены toohello управляемого домена.

Первая задача Hello — tooprovision виртуальной машины Windows Server, управляемый домен toohello присоединены к домену. Инструкции приведены в статье toohello [к домену Windows Server виртуальной машины tooan доменные службы Azure AD управляемых](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a>Задача 2 - средства установки DNS-сервера на виртуальной машине hello
Выполните следующие средства администрирования DNS hello tooinstall действия на виртуальную машину к домену hello hello. Для получения дополнительных сведений об [установке и использовании средств удаленного администрирования сервера](https://technet.microsoft.com/library/hh831501.aspx) перейдите на сайт TechNet.

1. Перейдите в слишком**виртуальные машины** узел в hello классический портал Azure. Выберите виртуальную машину hello, созданный в задаче 1 и нажмите кнопку **Connect** на панели команд hello hello нижней части окна hello.

    ![Подключение tooWindows виртуальной машины](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. Классический портал Hello предлагает tooopen или сохраните файл с расширением «.rdp», который является используется tooconnect toohello виртуальной машины. Щелкните файл hello, когда завершена загрузка.
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
9. На hello **функции** щелкните tooexpand hello **средства удаленного администрирования сервера** узел и нажмите кнопку tooexpand hello **средства администрирования ролей** узла. Выберите **средства DNS-сервера** компонент из списка hello средства администрирования ролей.

    ![Страница "Компоненты"](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. На hello **Подтверждение** щелкните **установить** tooinstall hello DNS-сервер средств на виртуальной машине hello. После успешного завершения установки компонента щелкните **закрыть** tooexit hello **Добавить роли и компоненты** мастера.

    ![Страница подтверждения](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a>Задача 3 — консоль управления tooadminister DNS для запуска hello DNS
Теперь, когда компонент устанавливается на средства DNS-сервера hello hello виртуальной машины к домену, мы используем hello DNS средства tooadminister DNS в домене управляемых hello.

> [!NOTE]
> Необходимо toobe членом группы hello «AAD Администраторы контроллера домена», tooadminister DNS на управляемый домен hello.
>
>

1. На начальном экране приветствия, нажмите кнопку **Администрирование**. Вы увидите hello **DNS** консоли, установленной на виртуальной машине hello.

    ![Администрирование — консоль DNS](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. Нажмите кнопку **DNS** консоли управления DNS toolaunch hello.
3. В hello **подключения tooDNS сервера** диалоговое окно, выберите вариант hello под названием **hello следующий компьютер**и введите имя домена DNS hello hello управляемого домена (например, «contoso100.com»).

    ![Консоль DNS - подключения toodomain](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. Hello консоли DNS подключается toohello управляемый домен.

    ![Консоль DNS — администрирование домена](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. Теперь можно использовать DNS консоли hello tooadd-записи DNS для компьютеров в виртуальной сети hello, в котором требуется включить службы домена AAD.

> [!WARNING]
> Будьте внимательны при администрировании DNS для hello управляемого домена с помощью средства администрирования DNS. Убедитесь, что вы **не удаляйте и не изменять записи DNS встроенных hello, которые используются службами домена в домене hello**. Встроенные записи DNS включают в себя записи DNS домена, записи сервера имен и другие записи, используемые для обнаружения контроллера домена. Если изменить эти записи доменных служб повреждены hello виртуальной сети.
>
>

В разделе hello [средства DNS статья на Technet](https://technet.microsoft.com/library/cc753579.aspx) Дополнительные сведения об управлении DNS.

## <a name="related-content"></a>Похожий контент
* [Приступая к работе с доменными службами Azure AD](active-directory-ds-getting-started.md)
* [К домену Windows Server виртуальной машины tooan доменные службы Azure AD управляемого](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
* [Средства DNS](https://technet.microsoft.com/library/cc753579.aspx)
