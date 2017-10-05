---
title: "Настройка источников развертывания для службы приложений в Azure Stack | Документация Майкрософт"
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
ms.openlocfilehash: be4b032e8f7370f696c47a7b8e82c0a819529f4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-sources"></a>Настройка источников развертывания

Служба приложений в Azure Stack поддерживает развертывание по требованию из систем управления версиями разных поставщиков.  Эта возможность позволяет разработчикам развертывать приложения напрямую из репозиториев систем управления версиями.  Чтобы клиенты могли подключить службу приложений к нужному репозиторию, администраторы должны настроить интеграцию между службой приложений в Azure Stack и поставщиком системы управления версиями.  Поддерживается локальная система Git, а также следующие поставщики систем управления версиями:

* GitHub
* Bitbucket;
* OneDrive
* DropBox

## <a name="view-deployment-sources-in-app-service-administration"></a>Просмотр источников развертывания в средстве администрирования службы приложений

1. Войдите в портал администрирования Azure стека (https://adminportal.local.azurestack.external) от имени администратора службы.
2. Перейдите в раздел **Resource Providers** (Поставщики ресурсов) и выберите элемент **App Service Resource Provider Admin** (Администрирование поставщика ресурсов службы приложений).
    ![Администрирование поставщика ресурсов службы приложений][1]
3. Щелкните **Source control configuration** (Настройка системы управления версиями).  Здесь вы увидите список всех настроенных источников развертывания.
    ![Администрирование поставщика ресурсов службы приложений — Настройка системы управления версиями][2]

## <a name="configure-github"></a>Настройка GitHub

> [!NOTE]
> Для выполнения этой задачи вам потребуется учетная запись GitHub.  Возможно, правильнее будет использовать корпоративную учетную запись, а не личную.

1. Войдите в GitHub и перейдите к https://www.github.com/settings/developers **Регистрация нового приложения** ![GitHub - Регистрация нового приложения][3]
2. Введите имя в поле **Application name** (Имя приложения), например "Служба приложений в Azure Stack".
3. Введите значение в поле **Homepage URL** (URL-адрес домашней страницы).  **URL-адрес домашней страницы должен быть адрес портала Azure стека** например - https://portal.local.azurestack.external
4. Введите текст в поле **Application Description** (Описание приложения).
5. Введите значение в поле **Authorization callback URL** (URL-адрес обратного вызова авторизации).  При развертывании Azure стека по умолчанию URL-адрес имеет https://portal.local.azurestack.external/tokenauthorize формы, если приложение выполняется под другой домен замены домена для azurestack.local ![GitHub - Регистрация нового приложения заполняется значениями][4]
6. Щелкните **Register application** (Зарегистрировать приложение).  Откроется следующая страница, на которой вы увидите значения **Client ID** (Идентификатор клиента) и **Client Secret** (Секрет клиента) для нового приложения.
    ![Приложение зарегистрировано на GitHub][5]
7.  В окне или новую вкладку браузера Войдите на портал администрирования стек Azure (https://adminportal.local.azurestack.external) от имени администратора службы. 
8.  Перейдите в раздел **Resource Providers** (Поставщики ресурсов) и выберите элемент **App Service Resource Provider Admin** (Администрирование поставщика ресурсов службы приложений). 
9. Щелкните **Source control configuration** (Настройка системы управления версиями).
10. Скопируйте и вставьте **идентификатор клиента** и **секрет клиента** для GitHub в соответствующие поля ввода.
11. Щелкните **Сохранить**.
12. Если вы не будете настраивать другие источники развертывания, переходите к [планированию восстановления для ролей управления](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).


## <a name="configure-bitbucket"></a>Настройка Bitbucket

> [!NOTE]
> Для выполнения этой задачи вам потребуется учетная запись Bitbucket.  Возможно, правильнее будет использовать корпоративную учетную запись, а не личную.

1. Войдите в систему BitBucket и перейдите к **интеграции** под учетной записью ![BitBucket панель мониторинга — интеграции][7]
2. Нажмите кнопку **OAuth** в списке управления доступом и **потребителя добавить** ![добавьте потребителя OAuth для BitBucket][8]
3. Введите значение в поле **Name** (Имя потребителя), например "Служба приложений в Azure Stack".
4. Введите текст в поле **Description** (Описание) для приложения.
5. Введите значение в поле **Callback URL** (URL-адрес обратного вызова).  В развертывании Azure стека по умолчанию Url-адрес обратного вызова находится в https://portal.local.azurestack.external/TokenAuthorize формы, если приложение выполняется под другой домен замены домена для azurestack.local.  Чтобы интеграция с Bitbucket прошла успешно, в точности соблюдайте приведенное здесь написание URL-адреса с учетом регистра.
6. Введите **URL-адрес** -этот URL-адрес должен быть Azure стека портала URL-адрес, например https://portal.local.azurestack.external
7. Выберите **разрешений** необходимые **репозиториев**: **чтения** **веб-перехватчиков**: **чтение и запись**
8. Щелкните **Сохранить**.  Вы увидите новое зарегистрированное приложение, а также значения **Key** (Ключ) и **Secret** (Секрет) для него в разделе **OAuth consumers** (Потребители OAuth).
    ![Список приложений в Bitbucket][9]
9.  В окне или новую вкладку браузера Войдите на портал администрирования стек Azure (https://adminportal.local.azurestack.external) от имени администратора службы. 
10.  Перейдите в раздел **Resource Providers** (Поставщики ресурсов) и выберите элемент **App Service Resource Provider Admin** (Администрирование поставщика ресурсов службы приложений). 
11. Щелкните **Source control configuration** (Настройка системы управления версиями).
12. Скопируйте и вставьте **ключ** для Bitbucket в поле ввода **Client Id** (Идентификатор клиента), а **секрет** — в поле **Client Secret** (Секрет клиента).
13. Щелкните **Сохранить**.
14. Если вы не будете настраивать другие источники развертывания, переходите к [планированию восстановления для ролей управления](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="configure-onedrive"></a>Настройка OneDrive

> [!NOTE]
> Учетные записи OneDrive для бизнеса сейчас не поддерживаются.  Для выполнения этой задачи вам потребуется учетная запись Майкрософт, связанная с учетной записью OneDrive.  Возможно, правильнее будет использовать корпоративную учетную запись, а не личную.

1. Откройте страницу https://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm и выполните вход с данными учетной записи Майкрософт.
2. Щелкните **Add an app** (Добавить приложение) в разделе **My applications** (Мои приложения).
![Приложения OneDrive][10]
3. Введите значение в поле **Name** (Имя) в разделе New Application Registration (Регистрация нового приложения), например **Служба приложений Azure Stack** и нажмите кнопку **Create Application** (Создать приложение).
4. На следующем экране вы увидите список свойств нового приложения. Запишите значение **Application Id**(Идентификатор приложения).
![Свойства приложения OneDrive][11]
5. В разделе **Application Secrets** (Секреты приложения) щелкните **Generate New Password** (Создать новый пароль) и запишите полученное значение **New password generated** (Созданный новый пароль) — это будет секрет для вашего приложения.
> [!NOTE]
> Обязательно запишите новый пароль. После того, как вы нажмете кнопку OK на этой странице, пароль невозможно будет получить.
6. В разделе **Platforms** (Платформы) щелкните **Add Platform** (Добавление платформы) и выберите **Web** (Веб).
7. Введите **URI перенаправления**.  В развертывании Azure стека по умолчанию, URI перенаправления возможности https://portal.local.azurestack.external/tokenauthorize формы, если приложение выполняется под другой домен замены домена для azurestack.local ![приложение OneDrive - Добавление Веб-платформы][12]
8. Задайте **Разрешения Microsoft Graph** - **Делегированные разрешения**.
    - **Files.ReadWrite.AppFolder**
    - **User.Read**  
      ![Разрешения Graph для приложения OneDrive][13]
10. Щелкните **Сохранить**.
11.  В окне или новую вкладку браузера Войдите на портал администрирования стек Azure (https://adminportal.local.azurestack.external) от имени администратора службы. 
12.  Перейдите в раздел **Resource Providers** (Поставщики ресурсов) и выберите элемент **App Service Resource Provider Admin** (Администрирование поставщика ресурсов службы приложений). 
13. Щелкните **Source control configuration** (Настройка системы управления версиями).
14. Скопируйте и вставьте **идентификатор приложения** для OneDrive в поле ввода **Client Id** (Идентификатор клиента), а **пароль** — в поле **Client Secret** (Секрет клиента).
15. Щелкните **Сохранить**.
16. Если вы не будете настраивать другие источники развертывания, переходите к [планированию восстановления для ролей управления](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="configure-dropbox"></a>Настройка Dropbox

> [!NOTE]
> Для выполнения этой задачи вам потребуется учетная запись Dropbox.  Возможно, правильнее будет использовать корпоративную учетную запись, а не личную.

1. Откройте страницу https://www.dropbox.com/developers/apps и выполните вход с данными учетной записи Dropbox.
2. Щелкните **Create app**(Создать приложение). 
![Приложения Dropbox][14]
3. Выберите **Dropbox API**.
4. Установите уровень доступа **App Folder** (Папка приложения).
5. Введите значение **Name** (Имя) для приложения.
![Регистрация приложения Dropbox][15]
6. Нажмите кнопку **Create App** (Создать приложение).  Вы увидите страницу со списком параметров для приложения, включая **App key** (Ключ приложения) и **App secret** (Секрет приложения).
7. Убедитесь, что параметр **App folder name** (Имя папки приложения) имеет значение **Служба приложений в Azure Stack**.
8. Задайте значение **OAuth 2 Redirect URI** (URI перенаправления OAuth 2) и щелкните **Add** (Добавить).  В развертывании Azure стека по умолчанию, URI перенаправления возможности https://portal.local.azurestack.external/tokenauthorize формы, если приложение выполняется под другой домен замены домена для azurestack.local ![общего банка данных приложения конфигурации][16]
9.  В окне или новую вкладку браузера Войдите на портал администрирования стек Azure (https://adminportal.local.azurestack.external) от имени администратора службы. 
10.  Перейдите в раздел **Resource Providers** (Поставщики ресурсов) и выберите элемент **App Service Resource Provider Admin** (Администрирование поставщика ресурсов службы приложений). 
11. Щелкните **Source control configuration** (Настройка системы управления версиями).
12. Скопируйте и вставьте **ключ приложения** для Dropbox в поле ввода **Client Id** (Идентификатор клиента), а **секрет приложения** — в поле **Client Secret** (Секрет клиента).
13. Щелкните **Сохранить**.
14. Если вы не будете настраивать другие источники развертывания, переходите к [планированию восстановления для ролей управления](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="schedule-repair-of-management-roles"></a>Планирование восстановления для ролей управления
Чтобы обновленные настройки, выполненные для различных источников развертывания, применялись правильно, необходимо восстановление ролей управления.  Этот процесс гарантирует, что все параметры конфигурации будут применяться корректно и настроенные источники развертывания будут доступны для клиентов.

1. В окне или новую вкладку браузера Войдите на портал администрирования стек Azure (https://adminportal.local.azurestack.external) от имени администратора службы.
2. Перейдите в раздел **Resource Providers** (Поставщики ресурсов) и выберите элемент **App Service Resource Provider Admin** (Администрирование поставщика ресурсов службы приложений).
3. Щелкните **Source control configuration** (Настройка системы управления версиями).
4. Скопируйте и вставьте **идентификатор клиента** и **секрет клиента** для GitHub в соответствующие поля ввода.
5. Нажмите кнопку **Сохранить**
6. Щелкните **Roles** (Роли).
7. Щелкните **Management Server** (Сервер управления).
8. Щелкните **Repair All** (Восстановить все) и выберите вариант **Yes** (Да).  Теперь для всех серверов управления запланировано восстановление. Эта операция завершает процесс интеграции.  Операции восстановления выполняются так, чтобы свести время простоя к минимуму.
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
