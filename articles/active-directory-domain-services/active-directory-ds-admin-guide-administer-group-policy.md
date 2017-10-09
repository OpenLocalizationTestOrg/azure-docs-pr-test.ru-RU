---
title: "Доменные службы Azure Active Directory: администрирование групповой политики в управляемых доменах | Документация Майкрософт"
description: "Администрирование групповой политики в управляемых доменах доменных служб Azure Active Directory"
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
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a>Администрирование групповой политики в управляемом домене доменных служб Azure AD
Azure доменных служб Active Directory включает в себя встроенные объекты групповой политики (GPO) для контейнеров «Пользователи AADDC» и «Компьютеры AADDC» hello. Вы можете настроить эти встроенные объекты групповой политики tooconfigure групповой политики на управляемый домен hello. Кроме того члены группы «Администраторы контроллера домена AAD» hello можно создать собственные настраиваемые подразделений в управляемый домен hello. Также создать пользовательские объекты групповой политики и связать их toothese настраиваемый подразделений. Пользователи, принадлежащие группе «Администраторы контроллера домена AAD» toohello предоставляются права администрирования групповой политики в домене управляемого hello.

## <a name="before-you-begin"></a>Перед началом работы
tooperform hello задачи, перечисленные в этой статье, необходимо:

1. Действующая **подписка Azure**.
2. **Каталог Azure AD** — синхронизированный с локальным каталогом или каталогом только для облака.
3. **Доменные службы Azure AD** должна быть включена для каталога hello Azure AD. Если вы еще не сделали этого, выполните все действия hello hello [руководство по началу работы](active-directory-ds-getting-started.md).
4. Объект **виртуальную машину к домену** из которой администрировать hello управляемого домена доменные службы Azure AD. Если у вас нет такой виртуальной машины, выполните все задачи hello, описанные в статье hello [к домену Windows виртуальной машины tooa управляемых](active-directory-ds-admin-guide-join-windows-vm.md).
5. Требуются учетные данные hello **группы «Администраторы AAD контроллера домена» toohello принадлежность учетной записи пользователей** в вашем каталоге tooadminister групповой политики для управляемого домена.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a>Задача 1. Подготовка tooremotely виртуальную машину к домену администрирования групповой политики для домена управляемого hello
Управляемый доменов доменные службы AD Azure можно управлять удаленно с помощью знакомых средств администрирования Active Directory например hello администрирования Active Directory Center (ADAC) или AD PowerShell. Аналогичным образом групповую политику для hello управляемого домена может управляться удаленно с помощью средств администрирования групповой политики hello.

В каталоге Azure AD у администраторов нет контроллеров toodomain tooconnect права на hello управляемого домена через удаленный рабочий стол. Члены группы «Администраторы контроллера домена AAD» hello можно удаленно администрировать групповой политики для управляемых доменов. Они могут использовать средства групповой политики на Windows Server или клиентской домена управляемого компьютера toohello присоединены к домену. Средства групповой политики можно установить в качестве части необязательный компонент управления групповыми политиками hello на Windows Server и клиентских компьютерах, присоединенных к toohello управляемый домен.

Первая задача Hello — tooprovision виртуальной машины Windows Server, управляемый домен toohello присоединены к домену. Инструкции приведены в статье toohello [к домену Windows Server виртуальной машины tooan доменные службы Azure AD управляемых](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a>Задача 2 - средства установки групповой политики на виртуальной машине hello
Выполните следующие средства администрирования групповой политики hello tooinstall действия на виртуальную машину к домену hello hello.

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
9. На hello **функции** страницу, выберите hello **Управление групповой политикой** компонентов.

    ![Страница "Компоненты"](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. На hello **Подтверждение** щелкните **установить** компонентом управления групповыми политиками hello tooinstall на виртуальной машине hello. После успешного завершения установки компонента щелкните **закрыть** tooexit hello **Добавить роли и компоненты** мастера.

    ![Страница подтверждения](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a>Задача 3. запуск hello групповой политики консоль управления tooadminister групповой политики
Можно использовать консоль управления групповыми политиками hello на виртуальную машину к домену hello tooadminister групповой политики на управляемый домен hello.

> [!NOTE]
> Необходимо toobe членом группы hello «AAD Администраторы контроллера домена», tooadminister групповой политики на управляемый домен hello.
>
>

1. На начальном экране приветствия, нажмите кнопку **Администрирование**. Вы увидите hello **Управление групповой политикой** консоли, установленной на виртуальной машине hello.

    ![Запуск управления групповыми политиками](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. Нажмите кнопку **Управление групповой политикой** консоли управления групповыми политиками toolaunch hello.

    ![Консоль управления групповой политикой](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a>Задача 4. Настройка встроенных объектов групповой политики
Существуют две встроенные объекты групповой политики (GPO) — по одной для контейнеров «AADDC компьютеры» и «Пользователи AADDC» hello управляемого домена. Вы можете настроить эти объекты групповой политики tooconfigure групповой политики на управляемый домен hello.

1. В hello **Управление групповой политикой** щелкните tooexpand hello **лес: contoso100.com** и **домены** узлы toosee hello групповых политик для управляемого домена.

    ![Встроенные объекты групповой политики](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. Эти встроенные объекты групповой политики tooconfigure групповых политик можно настроить на управляемый домен. Щелкните правой кнопкой мыши hello объекта групповой Политики и нажмите кнопку **изменить...**  toocustomize, встроенные hello объекта групповой Политики. Hello редактор групповой политики конфигурации позволяет вам toocustomize hello объекта групповой Политики.

    ![Редактирование встроенного объекта групповой политики](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. Теперь вы можете использовать hello **редактор управления групповыми политиками** консоли tooedit, встроенные hello объекта групповой Политики. Для экземпляра hello следующий снимок экрана показано, как toocustomize hello встроенного объекта групповой Политики «AADDC компьютеры».

    ![Настройка объекта групповой политики](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a>Шаг 5. Создание пользовательского объекта групповой политики
Можно создать или импортировать собственные пользовательские объекты групповой политики. Можно также связать настраиваемый tooa пользовательские объекты групповой политики Подразделения, вы создали в управляемый домен. Дополнительные сведения о создании пользовательских подразделений см. в статье [Создание подразделения в управляемом домене доменных служб Azure AD](active-directory-ds-admin-guide-create-ou.md).

> [!NOTE]
> Необходимо toobe членом группы hello «AAD Администраторы контроллера домена», tooadminister групповой политики на управляемый домен hello.
>
>

1. В hello **Управление групповой политикой** щелкните tooselect пользовательские организационное подразделение (OU). Щелкните правой кнопкой мыши Подразделение hello и нажмите кнопку **создать объект GPO в этом домене и связать его...** .

    ![Создание пользовательского объекта групповой политики](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. Укажите имя для нового hello объекта групповой Политики и нажмите кнопку **ОК**.

    ![Указание имени объекта групповой политики](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. Новый объект групповой Политики создается и связанный настраиваемый tooyour Подразделения. Щелкните правой кнопкой мыши hello объекта групповой Политики и нажмите кнопку **изменить...**  меню "hello".

    ![Созданный объект групповой политики](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. Вы можете настроить hello только что созданный объект групповой Политики, с помощью hello **редактор управления групповыми политиками**.

    ![Настройка нового объекта групповой политики](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


Дополнительные сведения об использовании [консоли управления групповой политикой](https://technet.microsoft.com/library/cc753298.aspx) можно найти в библиотеке Technet.

## <a name="related-content"></a>Похожий контент
* [Приступая к работе с доменными службами Azure AD](active-directory-ds-getting-started.md)
* [К домену Windows Server виртуальной машины tooan доменные службы Azure AD управляемого](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
* [Консоль управления групповой политикой](https://technet.microsoft.com/library/cc753298.aspx)
