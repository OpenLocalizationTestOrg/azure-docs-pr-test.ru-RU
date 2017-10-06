---
title: "Доменные службы Azure Active Directory: развертывание прокси приложения Azure Active Directory | Документация Майкрософт"
description: "Использование прокси приложения Azure AD в управляемых доменах доменных служб Azure Active Directory"
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
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a>Развертывание прокси приложения Azure AD в управляемых доменах доменных служб Azure AD
Прокси приложения Azure Active Directory (AD) поможет поддерживать удаленные работники путем публикации toobe локальных приложений, доступны через hello Интернета. Используя доменные службы Azure AD вы можете службами инфраструктуры tooAzure локальных приложений прежних версий теперь точности прогнозов и сдвига. Затем можно опубликовать эти приложения используют hello прокси приложения Azure AD, tooprovide toousers безопасного удаленного доступа в вашей организации.

Если вы toohello новый прокси приложения Azure AD, получить общие сведения об этой функции hello следующей статьей: [как tooprovide безопасный удаленный доступ tooon локальные приложения](../active-directory/active-directory-application-proxy-get-started.md).


## <a name="before-you-begin"></a>Перед началом работы
tooperform hello задачи, перечисленные в этой статье, необходимо:

1. Действующая **подписка Azure**.
2. **Каталог Azure AD** — синхронизированный с локальным каталогом или каталогом только для облака.
3. **Azure AD Basic или Premium лицензирования** является обязательным toouse hello прокси приложения Azure AD.
4. **Доменные службы Azure AD** должна быть включена для каталога hello Azure AD. Если вы еще не сделали этого, выполните все действия hello hello [руководство по началу работы](active-directory-ds-getting-started.md).

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a>Задача 1. Включить прокси приложения Azure AD для каталога Azure AD
Выполните следующие шаги tooenable hello прокси приложения Azure AD для вашего каталога Azure AD hello.

1. Войдите как администратор в hello [портал Azure](http://portal.azure.com).

2. Нажмите кнопку **Azure Active Directory** toobring копирование обзор directory hello. Щелкните **Корпоративные приложения**.

    ![Выбор каталога Azure AD](./media/app-proxy/app-proxy-enable-start.png)
3. Щелкните **Прокси приложения**. Если у вас подписка Azure AD Basic или Azure AD Premium, вы видите параметр tooenable пробную версию. Переключить **включите прокси приложения?** слишком**включить** и нажмите кнопку **Сохранить**.

    ![Использование прокси приложения](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. toodownload Здравствуйте соединитель, нажмите кнопку hello **соединитель** кнопки.

    ![Загрузка соединителя](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. На странице загрузки hello, примите условия лицензии hello и соглашения о конфиденциальности и нажмите кнопку hello **загрузки** кнопки.

    ![Подтверждение загрузки](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a>Задача 2 - Подготовка к домену Windows серверов toodeploy hello Azure AD соединитель прокси приложения
Необходимо, присоединенных к домену Windows Server виртуальных машин на которых можно установить соединитель прокси приложения Azure AD hello. В зависимости от приложения hello опубликован можно выбрать несколько серверов, на которых установлен соединитель hello tooprovision. Этот параметр развертывания обеспечивает более высокую доступность и позволяет обрабатывать более тяжелые нагрузки аутентификации.

Подготовка серверов соединителя hello на hello одной виртуальной сети (или подключенных одноранговыми виртуальной сети), в котором вы включили управляемого домена доменные службы Azure AD. Подобным образом, серверы hello размещение приложений hello публикацию через прокси-сервер приложения hello необходимо toobe установлен на hello одной виртуальной сети Azure.

tooprovision серверов соединителя, выполните задачи hello, описанные в статье hello [к домену Windows виртуальной машины tooa управляемых](active-directory-ds-admin-guide-join-windows-vm.md).


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a>Задача 3. Установка и регистрация hello соединитель прокси приложения Azure AD
Ранее подготовки виртуальной машины Windows Server и присоединения его toohello управляемый домен. В этой задаче будет установить соединитель прокси приложения Azure AD hello на этой виртуальной машине.

1. Скопируйте hello соединителя установки пакета toohello виртуальной Машины на котором устанавливается соединитель прокси приложения Azure AD Web hello.

2. Запустите **AADApplicationProxyConnectorInstaller.exe** на виртуальной машине hello. Примите условия лицензионного соглашения на использование программного обеспечения hello.

    ![Принятие условий установки](./media/app-proxy/app-proxy-install-connector-terms.png)
3. Во время установки, запрашиваемые tooregister hello соединителя с hello прокси приложения из каталога Azure AD.
    * Укажите **учетные данные глобального администратора Azure AD**. Ваш клиент глобального администратора может отличаться от учетных данных Microsoft Azure.
    * Hello администратора учетной записи, используемой tooregister hello соединитель должен принадлежать toohello же каталоге, где вы включили службы прокси приложения hello. К примеру, если hello клиента домена contoso.com, Здравствуйте, администратор должен быть admin@contoso.com или любой допустимый псевдоним для этого домена.
    * Если Конфигурация усиленной безопасности включена для сервера hello где устанавливается соединитель hello, hello экран регистрации может быть заблокирован. доступ tooallow hello инструкции в сообщении об ошибке hello. Убедитесь, что конфигурация усиленной безопасности Internet Explorer отключена.
    * Если не удается зарегистрировать соединитель, см. сведения в статье [Устранение неполадок прокси-сервера приложений](../active-directory/active-directory-application-proxy-troubleshoot.md).

    ![Соединитель установлен](./media/app-proxy/app-proxy-connector-installed.png)
4. Соединитель hello tooensure работает правильно, выполнения hello Azure AD приложения прокси-сервера соединителя средство устранения неполадок. Вы увидите успешно отчета после выполнения hello средство устранения неполадок.

    ![Успешное завершение работы средства устранения неполадок](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. Вы увидите соединитель недавно установленные hello, перечисленные на странице прокси приложения hello в каталоге Azure AD.

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> Вы можете tooinstall соединители на нескольких серверах tooguarantee высокого уровня доступности для проверки подлинности в приложениях, опубликованных через hello прокси приложения Azure AD. Выполните hello же шаги, перечисленные выше соединитель hello tooinstall на другие серверы присоединены к домену tooyour управляемый домен.
>
>

## <a name="next-steps"></a>Дальнейшие действия
Вы настроили hello прокси приложения Azure AD и интегрировать управляемого домена доменные службы Azure AD.

* **Переноса виртуальных машин tooAzure приложений:** точности прогнозов и shift можно из локальных серверов tooAzure виртуальные машины присоединены к домену tooyour управляемого домена приложений. Это позволяет избавиться от инфраструктуры hello затрат на выполнение локальными серверами.

* **Публикация приложений с помощью прокси приложения Azure AD:** публикации приложений, работающих на виртуальных машинах Azure с помощью hello прокси приложения Azure AD. Дополнительные сведения см. в статье [Публикация приложений с помощью прокси приложения Azure AD](../active-directory/application-proxy-publish-azure-portal.md).


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a>Примечание к развертыванию. Публикация приложений интегрированной проверки подлинности Windows с использованием прокси приложения Azure AD
Включить-tooyour приложений с помощью встроенной проверки подлинности Windows (IWA), предоставление разрешения соединителей прокси приложения tooimpersonate пользователей и отправляют и получают от их имени маркеры. Настройка ограниченного делегирования kerberos (KCD) для hello соединитель toogrant hello необходимые разрешения tooaccess ресурсов на управляемый домен hello. Используйте механизм проверки подлинности Kerberos на основе ресурсов hello на управляемых доменов для повышения уровня безопасности.


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a>Включить основанное на ресурсах ограниченное делегирование kerberos для соединитель прокси приложения hello Azure AD
Соединитель прокси приложения Azure Hello должна быть настроена для ограниченного делегирования kerberos (KCD), поэтому он может олицетворять пользователей на управляемый домен hello. В управляемом домене доменных служб Azure AD у вас нет привилегий администратора домена. Таким образом **традиционное ограниченное делегирование Kerberos на уровне учетной записи нельзя настроить в управляемом домене**.

Используйте основанное на ресурсах ограниченное делегирование Kerberos, как описано в этой [статье](active-directory-ds-enable-kcd.md).

> [!NOTE]
> Необходимо toobe членом группы «Администраторы контроллера домена AAD» hello, tooadminister hello управляемого домена командлетах AD PowerShell.
>
>

Язык, hello PowerShell Get-ADComputer командлет tooretrieve hello hello компьютер, на какие hello прокси приложения Azure AD соединителя.
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

После этого используйте tooset командлета Set-ADComputer hello копирование основанное на ресурсах ограниченное делегирование Kerberos для hello ресурсов сервера.
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

При развертывании несколько соединителей прокси приложения на управляемый домен необходимо tooconfigure основанное на ресурсах ограниченное делегирование Kerberos для каждого такого экземпляра соединителя.


## <a name="related-content"></a>Похожий контент
* [Приступая к работе с доменными службами Azure AD](active-directory-ds-getting-started.md)
* [Настройка ограниченного делегирования Kerberos в управляемом домене](active-directory-ds-enable-kcd.md)
* [(Обзор ограниченного делегирования Kerberos)](https://technet.microsoft.com/library/jj553400.aspx)
