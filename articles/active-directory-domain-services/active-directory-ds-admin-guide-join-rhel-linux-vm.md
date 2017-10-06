---
title: "Azure доменных служб Active Directory: Присоединиться к управляемому домену tooa ВМ RHEL | Документы Microsoft"
description: "Присоединить виртуальную машину с Red Hat Enterprise Linux tooAzure AD доменных служб"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a>Присоединить к виртуальной машине Red Hat Enterprise Linux 7 tooa управляемого домену
В этой статье показано, как toojoin tooan виртуальной машины Red Hat Enterprise Linux (RHEL) 7 доменные службы Azure AD управление домена.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Подготовка виртуальной машины Red Hat Enterprise Linux
Выполните следующие шаги tooprovision RHEL 7 виртуальной машины с помощью портала Azure hello hello.

1. Войдите в toohello [портал Azure](https://portal.azure.com).

    ![Панель мониторинга портала Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Нажмите кнопку **New** на hello оставить область и тип **Red Hat** в hello панель поиска, как показано на следующий снимок экрана приветствия. В результатах поиска hello отображаются записи для Red Hat Enterprise Linux. Щелкните **Red Hat Enterprise Linux 7.2**.

    ![Выбор RHEL в результатах](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. Результаты поиска Hello в hello **все** области должны быть перечислены hello Red Hat Enterprise Linux 7.2 изображения. Нажмите кнопку **Red Hat Enterprise Linux 7.2** tooview Дополнительные сведения о hello образ виртуальной машины.

    ![Выбор RHEL в результатах](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. В hello **Red Hat Enterprise Linux 7.2** области, вы увидите Дополнительные сведения о hello образ виртуальной машины. В hello **выберите модель развертывания** раскрывающийся список, выберите **классический**. Нажмите кнопку hello **создать** кнопки.

    ![Просмотр сведений об образе](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. В hello **основы** страница hello **создать виртуальную машину** мастера введите hello **имя узла** для hello новой виртуальной машины. Также укажите имя пользователя локального администратора в hello **имя пользователя** поля и **пароль**. Вы также можете toouse пользователя локального администратора hello tooauthenticate ключа SSH. Кроме того, выбрать **ценовую категорию** для hello виртуальной машины.

    ![Мастер создания виртуальной машины: страница основных сведений](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. В hello **размер** страница hello **создать виртуальную машину** приветствия мастера, выберите размер виртуальной машины hello.

    ![Мастер создания виртуальной машины: выбор размера](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. В hello **параметры** страница hello **создать виртуальную машину** приветствия мастера, выберите учетную запись хранения для виртуальной машины hello. Нажмите кнопку **виртуальной сети** следует развернуть ВМ Linux toowhich hello tooselect hello виртуальной сети. В hello **виртуальной сети** колонки, выберите hello виртуальной сети, в которой доступно доменные службы Azure AD. В этом примере мы выберите виртуальную сеть «MyPreviewVNet» hello.

    ![Создание виртуальной машины — выбор виртуальной сети](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. На hello **Сводка** страница hello **создать виртуальную машину** приветствия мастера просмотрите и нажмите кнопку **ОК** кнопки.

    ![Создание виртуальной машины — виртуальная сеть выбрана](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. Следует запустить развертывание hello новой виртуальной машины на основе образа hello RHEL 7.2.

    ![Создание виртуальной машины — развертывание начато](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Через несколько минут hello виртуальная машина должна была успешно развернута и готова к использованию.

    ![Создание виртуальной машины — развернута](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a>Удаленное подключение к виртуальной машине Linux toohello обслуживаемого
подготовлено Hello RHEL 7.2 виртуальной машины в Azure. Следующая задача Hello-tooconnect удаленно toohello виртуальной машины.

**Подключите виртуальную машину toohello RHEL 7.2** , следуйте инструкциям статьи hello в hello [как toolog на tooa виртуальной машине под управлением Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello остальные шаги hello предполагается, что используется hello PuTTY SSH клиентской tooconnect toohello RHEL виртуальной машины. Дополнительные сведения см. в разделе hello [странице загрузки PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Откройте hello PuTTY программы.
2. Введите hello **имя узла** для только что создана виртуальная машина RHEL hello. В этом примере наши виртуальная машина имеет hello имя узла «contoso rhel.cloudapp .net». Если вы не уверены в правильности имени узла hello вашей виртуальной машины, см. toohello мониторинга виртуальных Машин на hello портал Azure.

    ![Подключение PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Войдите в систему виртуальной машины toohello, используя учетные данные локального администратора hello, которое было указано при создании hello виртуальной машины. В этом примере мы использовали учетной записи локального администратора hello «mahesh».

    ![Окно входа PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a>Установить необходимые пакеты на виртуальной машине Linux hello
После подключения виртуальной машины toohello hello следующей задачей является tooinstall пакеты, необходимые для присоединения к домену на виртуальной машине hello. Выполните следующие шаги hello.

1. **Установить realmd:** hello realmd пакет используется для присоединения к домену. В терминале PuTTY введите hello следующую команду:

    sudo yum install realmd

    ![Установка realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Через несколько минут hello realmd пакет должен получить установлен на виртуальной машине hello.

    ![realmd установлен](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Установить sssd:** hello realmd пакета зависит от операций соединения sssd tooperform домена. В терминале PuTTY введите hello следующую команду:

    sudo yum install sssd

    ![Установка sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Через несколько минут hello sssd пакет должен получить установлен на виртуальной машине hello.

    ![realmd установлен](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Установка kerberos:** в терминале PuTTY введите hello следующую команду:

    sudo yum install krb5-workstation krb5-libs

    ![Установка kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Через несколько минут hello realmd пакет должен получить установлен на виртуальной машине hello.

    ![Kerberos установлен](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a>Присоединение управляемого домена виртуальной машины Linux toohello hello
Теперь, когда требуется hello пакеты устанавливаются на виртуальной машине Linux hello, следующая задача hello-toojoin hello виртуальной машины toohello управляемый домен.

1. Обнаружение управляемого домена доменных служб AAD hello. В терминале PuTTY введите hello следующую команду:

    sudo realm discover CONTOSO100.COM

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Если **область обнаружения** — не удается toofind ваш управляемый домен, убедитесь, этот домен hello доступен из виртуальной машины hello (try ping). Обеспечьте наличие этой виртуальной машине hello действительно был развернутой toohello одной виртуальной сети, в какие hello управляемый домен недоступен.
2. Инициализируйте kerberos. В терминале PuTTY введите следующую команду hello. Убедитесь, что пользователь, принадлежащий группы администраторов контроллера домена, toohello «AAD». Только эти пользователи могут присоединен к домену управляемых компьютеров toohello.

    kinit bob@CONTOSO100.COM

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Убедитесь, что указано имя домена hello заглавными буквами, else kinit завершается ошибкой.
3. Присоединен к домену toohello машины hello. В терминале PuTTY введите следующую команду hello. Укажите hello того же пользователя, указанных в предшествующих шаг (kinit) hello.

    sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'

    ![Присоединение к realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

Должно появиться сообщение («Регистрация выполнена успешно машина в сфере») при hello машина успешно присоединена toohello управляемый домен.

## <a name="verify-domain-join"></a>Проверка присоединения к домену
Можно быстро узнать, была ли успешно присоединена toohello управляемый домен компьютера hello. Подключение toohello вновь RHEL виртуальной Машины с помощью SSH и учетная запись пользователя домена и затем toosee проверку, если правильно разрешить учетной записи пользователя hello присоединенных к домену.

1. В терминалов, PuTTY типа hello, следующая команда tooconnect toohello вновь домену RHEL виртуальной машины с помощью SSH. Использовать учетную запись домена, к которому относится toohello управляемого домена (например, "bob@CONTOSO100.COM" в этом случае.)

    ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net
2. В PuTTY терминала введите следующие команды toosee Если hello домашний каталог был правильно инициализирован hello.

    pwd
3. Введите подписку toosee команду, если членство в группах hello устраняются правильно hello в терминале PuTTY.

    id

Ниже приведен пример выходных данных этих команд:

![Проверка присоединения к домену](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Устранение неполадок при присоединении к домену
См. toohello [Устранение неполадок присоединения к домену](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) статьи.

## <a name="related-content"></a>Похожий контент
* [Приступая к работе с доменными службами Azure AD](active-directory-ds-getting-started.md)
* [К домену Windows Server виртуальной машины tooan доменные службы Azure AD управляемого](active-directory-ds-admin-guide-join-windows-vm.md)
* [Как toolog на tooa виртуальной машине под управлением Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Installing Kerberos (Установка Kerberos)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7: Windows Integration Guide (Red Hat Enterprise Linux 7: руководство по интеграции Windows)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
