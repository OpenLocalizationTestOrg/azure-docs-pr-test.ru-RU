---
title: "Azure доменных служб Active Directory: Присоединиться к управляемому домену tooa виртуальной Машины Windows Server | Документы Microsoft"
description: "Присоединить виртуальную машину с Windows Server tooAzure AD доменных служб"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>К домену Windows Server виртуальной машины tooa управляемого
> [!div class="op_single_selector"]
> * [Классический портал Azure — Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell — Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

В этой статье показано, как toojoin виртуальной машины запущенной Windows Server 2012 R2 tooan доменные службы Azure AD управление домен, с помощью классического портала Azure hello.

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>Шаг 1: Создание виртуальной машины Windows Server hello
Следуйте указаниям в hello hello [создать виртуальную машину под управлением Windows в классический портал Azure hello](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) учебника. Очень важно tooensure, эта созданная виртуальная машина присоединена toohello одной виртуальной сети, в которой включены доменные службы Azure AD. параметр «Быстрое создание» Hello не включает вы toojoin hello виртуальной машины tooa виртуальной сети. Поэтому необходимо toouse hello «Из коллекции» параметр toocreate hello виртуальной машины.

Выполнить hello следующие шаги toocreate виртуальной машины присоединены к домену toohello виртуальную сеть Windows включена доменные службы Azure AD.

1. В классический портал Azure, на панели команд hello hello нижней части окна hello hello щелкните **New**.
2. В разделе **Среда выполнения приложений** щелкните **Виртуальная машина**, а затем выберите **Из коллекции**.
3. на экране приветствия позволяет **Выбор изображения** для виртуальной машины из списка доступных образов hello. Выберите соответствующий образ hello.

    ![Выбор образа](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. второй экран приветствия позволяет выбрать имя компьютера, размер и имя пользователя с правами администратора и пароль. Используйте уровень hello и размер, необходимый toorun приложения или рабочей нагрузки. имя пользователя Hello, выбираемое здесь — пользователя локального администратора на компьютере hello. Не вводите здесь учетные данные пользователя домена.

    ![Настройка виртуальной машины](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. Третье окно приветствия позволяет настраивать ресурсы для сети, хранилища и доступности. Убедитесь, вы выбрали hello виртуальной сети, в которой включены доменные службы Azure AD из hello **регион, территориальная группа или виртуальная сеть** раскрывающегося списка. Укажите **DNS-имя облачной службы** соответствующим образом для hello виртуальной машины.

    ![Выбор виртуальной сети для виртуальной машины](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Обеспечить присоединения виртуальной машины toohello hello одной виртуальной сети, в котором требуется включить доменные службы Azure AD. В результате hello виртуальной машины можно разделе hello домена и выполнения задач, таких как hello к домену. При выборе toocreate hello виртуальной машины в другую виртуальную сеть подключения этой виртуальной сети toohello виртуальной сети включена доменные службы Azure AD.
   >
   >
6. Четвертый экран приветствия позволяет установить агент ВМ hello и настройки некоторых доступных расширений hello.

    ![Готово](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. После создания виртуальной машины hello классический портал hello перечислены hello новой виртуальной машины в группе hello **виртуальные машины** узла. Hello виртуальной машины и облачные службы запускаются автоматически, и их состояние отображается как **под управлением**.

    ![Виртуальная машина настроена и запущена](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>Шаг 2: Подключение с помощью учетной записи локального администратора hello виртуальной машины Windows Server toohello
Теперь мы подключения виртуальной машины Windows Server только что созданный toohello, toojoin его toohello домена. Используйте учетные данные локального администратора hello, указанные при создании виртуальной машины hello, tooconnect tooit.

Выполните следующие шаги tooconnect toohello виртуальной машины hello.

1. Перейдите в слишком**виртуальные машины** узел hello классического портала. Выберите hello виртуальной машины, созданной на шаге 1 и нажмите кнопку **Connect** на панели команд hello hello нижней части окна hello.

    ![Подключение tooWindows виртуальной машины](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. Классический портал Hello предлагает tooopen или сохраните файл с расширением «.rdp», который является используется tooconnect toohello виртуальной машины. Щелкните файл tooopen hello, когда завершена загрузка.
3. В строке приветствия входа введите ваш **учетные данные локального администратора**, указанные при создании виртуальной машины hello. Например, в примере выше это localhost\mahesh.

На этом этапе вы должны войти в toohello вновь создана виртуальная машина Windows, используя учетные данные локального администратора. Hello следующим шагом является виртуальной машины toohello toojoin hello домена.

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>Шаг 3: Присоединение управляемого домена виртуальной машины Windows Server toohello AAD DS hello
Выполните следующие шаги toojoin hello домена Windows Server виртуальной машины toohello AAD DS управляемого hello.

1. Подключите toohello Windows Server, как показано в шаге 2. Hello начальном экране откройте **диспетчера сервера**.
2. Нажмите кнопку **локального сервера** в левой части окна диспетчера серверов hello hello.

    ![Запуск диспетчера серверов на виртуальной машине](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Нажмите кнопку **рабочей группы** под hello **свойства** раздела. В hello **системные свойства** страницу свойств, нажмите кнопку **изменений** toojoin hello домена.

    ![Страница системных свойств](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Укажите имя домена hello управляемого домена доменные службы Azure AD в hello **домена** текстовое поле и нажмите кнопку **ОК**.

    ![Укажите объединить toobe домена hello](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. Вы являются запрашиваемые tooenter toojoin hello учетные данные домена. Убедитесь, которую **указать учетные данные hello toohello принадлежность пользователя администраторов контроллера домена AAD** группы. Только члены этой группы имеют привилегии toojoin машины toohello управляемый домен.

    ![Ввод учетных данных для присоединения к домену](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. Можно указать учетные данные в любом из следующих способов hello:

   * Формат имени участника-пользователя: укажите hello суффикс UPN для учетной записи пользователя hello, настроенной в Azure AD. В этом примере — суффикс UPN пользователя hello «bob» hello "bob@domainservicespreview.onmicrosoft.com".
   * Формат SAMAccountName: hello имя учетной записи можно указать в формате SAMAccountName hello. В этом примере пользователь hello «bob», должны tooenter «CONTOSO100\bob».

     > [!NOTE]
     > **Рекомендуется использовать учетные данные для toospecify формат имени участника-пользователя hello.** Hello SAMAccountName могут создаваться автоматически в случае префикс имени участника-пользователя пользователя слишком долго (например, «joereallylongnameuser»). Если несколько пользователей имеют одинаковый префикс имени участника-пользователя (например, «bob») в клиенте Azure AD, их SAMAccountName формата может быть создан с помощью службы hello приветствия. В этих случаях можно использовать в формате UPN hello надежно toolog в toohello домене.
     >
     >
7. После успешного присоединения к домену, может появиться следующие сообщения с приветствием домена toohello hello. Перезапустите виртуальную машину hello для toocomplete операции присоединения домена hello.

    ![Вас приветствует toohello домена](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Устранение неполадок при присоединении к домену
### <a name="connectivity-issues"></a>Проблемы, связанные с подключением
Если виртуальная машина hello домена не удается toofind hello, см. следующие шаги по устранению неполадок toohello:

* Убедитесь, что на виртуальной машине hello подключенных toohello одной виртуальной сети, что вы включили доменных служб в. В противном случае hello виртуальная машина — не удается tooconnect toohello домен и таким образом не удается toojoin hello домена.
* Если виртуальная машина hello tooanother подключенной виртуальной сети, убедитесь в наличии подключенных toohello виртуальной сети, в котором требуется включить доменных служб в этой виртуальной сети.
* Попробуйте tooping hello домена с помощью имени домена hello hello управляемого домена (например, «ping contoso100.com»). Если вы не удается toodo таким образом, попробуйте tooping hello IP-адресов для домена hello отображаются на странице приветствия, где вы включили доменные службы Azure AD (например, «ping 10.0.0.4»). Если вы могли tooping hello IP-адрес, но не hello домена, DNS-сервер может неправильно настроен. Возможно не настроена hello IP-адреса домена hello как DNS-серверы для hello виртуальной сети.
* Попробуйте списания hello кэш сопоставителя DNS на виртуальной машине hello («ipconfig/flushdns»).

Если вы получаете toohello диалоговым окном, которое запрашивает учетные данные toojoin hello домена, у вас проблемы с подключением.

### <a name="credentials-related-issues"></a>Проблемы, связанные с учетными данными
См. в toohello, выполнив действия, если возникают проблемы с учетными данными домена не удается toojoin hello.

* Попробуйте использовать учетные данные для toospecify формат имени участника-пользователя hello. Hello SAMAccountName для вашей учетной записи может быть создан для автоматически при наличии нескольких пользователей с помощью hello UPN же префикса в клиенте или если префикса имени участника-пользователя является слишком длинные. Таким образом формат SAMAccountName hello для вашей учетной записи может отличаться от ожидается сведения или использовать в вашем домене в локальной среде.
* Попробуйте toouse hello учетные данные учетной записи пользователя, к которому относится toohello «AAD Администраторы контроллера домена» группа toojoin машины toohello управляемый домен.
* Убедитесь, что [включена синхронизация паролей](active-directory-ds-getting-started-password-sync.md) в соответствии с hello шаги, описанные в руководстве по началу работы hello.
* Убедитесь, что используют hello UPN пользователя hello, настроенным в Azure AD (например, "bob@domainservicespreview.onmicrosoft.com") toosign в.
* Убедитесь, что время ожидания для toocomplete синхронизации паролей, как указано в руководство по началу работы hello.

## <a name="related-content"></a>Похожий контент
* [Приступая к работе с доменными службами Azure AD](active-directory-ds-getting-started.md)
* [Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
