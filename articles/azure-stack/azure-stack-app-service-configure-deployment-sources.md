---
title: "aaaConfigure источников развертывания для приложения служб Azure стек | Документы Microsoft"
description: "Действия администратора службы для настройки источников развертывания (Git, GitHub, Bitbucket, Dropbox и OneDrive) для службы приложений в Azure Stack"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 2eaf0a7f4b6e52d64a302000c1dd3c3eb5d6a6ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-sources"></a>Настройка источников развертывания

Служба приложений в Azure Stack поддерживает развертывание по требованию из систем управления версиями разных поставщиков.  Этот компонент позволяет приложения разработчики toobe может toodeploy прямой из их репозиториев системы управления версиями.  В порядок может tooconfigure toobe клиентов службы приложений tooconnect tootheir репозиториев, администраторам необходимо сначала настроить интеграцию hello службы приложений Azure стек и hello поставщик системы управления версиями.  Hello поддерживается поставщики управления версиями, кроме toolocal Git, являются:

* GitHub
* Bitbucket;
* OneDrive
* DropBox

## <a name="view-deployment-sources-in-app-service-administration"></a>Просмотр источников развертывания в средстве администрирования службы приложений

1. Войдите в портал администрирования Azure стека (https://adminportal.local.azurestack.external) toohello под Здравствуйте, администратор службы.
2. Обзор слишком**поставщиков ресурсов** и выберите hello **администратора поставщика ресурсов службы приложения**.  ![Администрирование поставщика ресурсов службы приложений][1]
3. Щелкните **Source control configuration** (Настройка системы управления версиями).  Вы увидите список всех источников развертывания настроен hello.
    ![Администрирование поставщика ресурсов службы приложений — Настройка системы управления версиями][2]

## <a name="configure-github"></a>Настройка GitHub

> [!NOTE]
> Требуется учетная запись GitHub toocomplete этой задачи.  Вы можете toouse учетную запись для вашей организации, а не личную учетную запись.

1. Вход tooGitHub и обзор toohttps://www.github.com/settings/developers **Регистрация нового приложения** ![GitHub - Регистрация нового приложения][3]
2. Введите имя в поле **Application name** (Имя приложения), например "Служба приложений в Azure Stack".
3. Введите hello **URL-адрес домашней страницы**.  **Hello URL-адрес домашней страницы должен быть адрес портала Azure стека hello** например - https://portal.local.azurestack.external
4. Введите текст в поле **Application Description** (Описание приложения).
5. Введите hello **URL-адрес обратного вызова авторизации**.  При развертывании Azure стека по умолчанию hello URL-адрес имеет hello https://portal.local.azurestack.external/tokenauthorize формы, если приложение выполняется под другой домен замены домена для azurestack.local ![GitHub - Регистрация нового приложения с заполняется значениями][4]
6. Щелкните **Register application** (Зарегистрировать приложение).  Можно будет использовать с hello листинг страницы **идентификатор клиента** и **секрет клиента** для приложения hello.
    ![Приложение зарегистрировано на GitHub][5]
7.  В другом браузере вкладку или окно входа toohello портала администратора Azure стека (https://adminportal.local.azurestack.external) от имени администратора службы hello. 
8.  Обзор слишком**поставщиков ресурсов** и выберите hello **администратора поставщика ресурсов службы приложения**. 
9. Щелкните **Source control configuration** (Настройка системы управления версиями).
10. Скопируйте и вставьте hello **идентификатор клиента** и **секрет клиента** в соответствующие поля ввода hello для GitHub.
11. Щелкните **Сохранить**.
12. Если вы не готовы tooconfigure другие источники развертывания, перейдите в слишком[восстановления ролей для управления расписанием](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).


## <a name="configure-bitbucket"></a>Настройка Bitbucket

> [!NOTE]
> Требуется учетная запись BitBucket toocomplete этой задачи.  Вы можете toouse учетную запись для вашей организации, а не личную учетную запись.

1. Войдите в tooBitBucket и обзор слишком**интеграции** под учетной записью ![BitBucket панель мониторинга — интеграции][7]
2. Нажмите кнопку **OAuth** в списке управления доступом и **потребителя добавить** ![добавьте потребителя OAuth для BitBucket][8]
3. Введите **имя** для hello объекта-получателя, например службы приложений Azure стеке
4. Введите **описание** для приложения hello
5. Введите hello **URL-адрес обратного вызова**.  При развертывании Azure стека по умолчанию hello URL-адрес обратного вызова находится в https://portal.local.azurestack.external/TokenAuthorize формы hello, если приложение выполняется под другой домен замены домена для azurestack.local.  URL-адрес Hello необходимо выполнить капитализации hello перечисленные здесь для интеграции toosucceed BitBucket.
6. Введите hello **URL-адрес** -этот URL-адрес должен быть hello Azure стека URL-адрес портала, например https://portal.local.azurestack.external
7. Выберите hello **разрешений** необходимые **репозиториев**: **чтения** **веб-перехватчиков**: **чтение и запись**
8. Щелкните **Сохранить**.  Теперь вы увидите этого новые приложения и hello **ключ** и **секрет** под **потребителей OAuth**.
    ![Список приложений в Bitbucket][9]
9.  В другом браузере вкладку или окно входа toohello портала администратора Azure стека (https://adminportal.local.azurestack.external) от имени администратора службы hello. 
10.  Обзор слишком**поставщиков ресурсов** и выберите hello **администратора поставщика ресурсов службы приложения**. 
11. Щелкните **Source control configuration** (Настройка системы управления версиями).
12. Скопируйте и вставьте hello **ключ** в hello **идентификатор клиента** поля ввода и **секрет** в hello **секрет клиента** поле ввода для BitBucket.
13. Щелкните **Сохранить**.
14. Если вы не готовы tooconfigure другие источники развертывания, перейдите в слишком[восстановления ролей для управления расписанием](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="configure-onedrive"></a>Настройка OneDrive

> [!NOTE]
> Учетные записи OneDrive для бизнеса сейчас не поддерживаются.  Необходимо toohave связанной учетной записи Майкрософт tooa toocomplete учетной записи OneDrive этой задачи.  Вы можете toouse учетную запись для вашей организации, а не личную учетную запись.

1. Обзор toohttps://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm и вход с использованием учетной записи Майкрософт.
2. Щелкните **Add an app** (Добавить приложение) в разделе **My applications** (Мои приложения).
![Приложения OneDrive][10]
3. Введите **имя** hello Регистрация нового приложения, введите **службы приложений Azure стеке**и нажмите кнопку **Создание приложения**
4. Следующий экран приветствия список свойств hello нового приложения. Запись hello **идентификатор приложения**
![OneDrive свойства приложения][11]
5. В разделе **секреты приложения** щелкните **создать новый пароль** и запись hello **новый пароль, созданный** -это ваш секрет приложения.
> [!NOTE]
> Запишите toomake убедиться, что новый пароль hello как его не удается найти после нажатия кнопки ОК на этом этапе.
6. В разделе **Platforms** (Платформы) щелкните **Add Platform** (Добавление платформы) и выберите **Web** (Веб).
7. Введите hello **URI перенаправления**.  В развертывании Azure стека по умолчанию, hello URI перенаправления возможности https://portal.local.azurestack.external/tokenauthorize формы hello, если приложение выполняется под другой домен замены домена для azurestack.local ![приложение OneDrive — Добавить веб-платформы][12]
8. Набор hello **Microsoft Graph разрешения** - **делегированные разрешения**
    - **Files.ReadWrite.AppFolder**
    - **User.Read**  
      ![Разрешения Graph для приложения OneDrive][13]
10. Щелкните **Сохранить**.
11.  В другом браузере вкладку или окно входа toohello портала администратора Azure стека (https://adminportal.local.azurestack.external) от имени администратора службы hello. 
12.  Обзор слишком**поставщиков ресурсов** и выберите hello **администратора поставщика ресурсов службы приложения**. 
13. Щелкните **Source control configuration** (Настройка системы управления версиями).
14. Скопируйте и вставьте hello **идентификатор приложения** в hello **идентификатор клиента** поля ввода и **пароль** в hello **секрет клиента** поле ввода для OneDrive.
15. Щелкните **Сохранить**.
16. Если вы не готовы tooconfigure другие источники развертывания, перейдите в слишком[восстановления ролей для управления расписанием](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="configure-dropbox"></a>Настройка Dropbox

> [!NOTE]
> Необходимо toohave toocomplete учетной записи общего банка данных этой задачи.  Вы можете toouse учетную запись для вашей организации, а не личную учетную запись.

1. Обзор toohttps://www.dropbox.com/developers/apps и вход с использованием учетной записи общего банка данных
2. Щелкните **Create app**(Создать приложение). 
![Приложения Dropbox][14]
3. Выберите **Dropbox API**.
4. Задайте уровень доступа hello слишком**папка приложения**
5. Введите значение **Name** (Имя) для приложения.
![Регистрация приложения Dropbox][15]
6. Нажмите кнопку **Create App** (Создать приложение).  Теперь откроется страница Вывод hello параметров для приложения hello в том числе **ключ приложения** и **секрет приложения**.
7. Проверьте hello **имя папки приложения** задано слишком**службы приложений Azure стеке**
8. Набор hello **URI перенаправления OAuth 2** и нажмите кнопку **добавить**.  В развертывании Azure стека по умолчанию, hello URI перенаправления возможности https://portal.local.azurestack.external/tokenauthorize формы hello, если приложение выполняется под другой домен замены домена для azurestack.local ![общего банка данных приложения конфигурации][16]
9.  В другом браузере вкладку или окно входа toohello портала администратора Azure стека (https://adminportal.local.azurestack.external) от имени администратора службы hello. 
10.  Обзор слишком**поставщиков ресурсов** и выберите hello **администратора поставщика ресурсов службы приложения**. 
11. Щелкните **Source control configuration** (Настройка системы управления версиями).
12. Скопируйте и вставьте hello **ключ приложения** в hello **идентификатор клиента** поля ввода и **секрет приложения** в hello **секрет клиента** поле ввода для Общий банк данных.
13. Щелкните **Сохранить**.
14. Если вы не готовы tooconfigure другие источники развертывания, перейдите в слишком[восстановления ролей для управления расписанием](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="schedule-repair-of-management-roles"></a>Планирование восстановления для ролей управления
Чтобы обновления в конфигурации hello hello настроек hello применения различных toobe источников развертывания toobe исправить необходимости роли управления hello.  Этот процесс гарантирует правильное применение значений конфигурации hello и источники развертывания настроен hello становятся доступны tootenants.

1. В другом браузере вкладку или окно входа toohello портала администратора Azure стека (https://adminportal.local.azurestack.external) от имени администратора службы hello.
2. Обзор слишком**поставщиков ресурсов** и выберите hello **администратора поставщика ресурсов службы приложения**.
3. Щелкните **Source control configuration** (Настройка системы управления версиями).
4. Скопируйте и вставьте hello **идентификатор клиента** и **секрет клиента** в соответствующие поля ввода hello для GitHub.
5. Нажмите кнопку **Сохранить**
6. Щелкните **Roles** (Роли).
7. Щелкните **Management Server** (Сервер управления).
8. Щелкните **Repair All** (Восстановить все) и выберите вариант **Yes** (Да).  Эта операция планирует восстановления на все серверы управления toocomplete hello интеграции.  операции восстановления Hello, управляемых toominimize время простоя.
    ![Администрирование поставщика ресурсов службы приложений — Роли — Восстановить все серверы управления][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin.png
[2]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-source-control-configuration.png
[3]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-developer-applications.png
[4]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-populated.png
[5]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-complete.png
[6]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-roles-management-server-repair-all.png
[7]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-dashboard.png
[8]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer.png
[9]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer-complete.png
[10]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-applications.png
[11]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-registration.png
[12]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-platform.png
[13]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-graph-permissions.png
[14]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-applications.png
[15]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-registration.png
[16]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-configuration.png
