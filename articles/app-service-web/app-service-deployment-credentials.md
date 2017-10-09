---
title: "учетные данные развертывания службы приложения aaaAzure | Документы Microsoft"
description: "Узнайте, как toouse hello учетные данные развертывания службы приложений Azure."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a>Настройка учетных данных развертывания службы приложений Azure
[Служба приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) поддерживает два типа учетных данных для [развертывания локальной системы Git](app-service-deploy-local-git.md) и [развертывания FTP(S)](app-service-deploy-ftp.md). Они не являются hello то же, что учетные данные Azure Active Directory.

* **Учетные данные уровня пользователя**: один набор учетных данных для учетной записи Azure всей hello. Для любого приложения, в любую из своих подписок, hello Azure учетная запись имеет разрешение tooaccess может быть tooApp используется toodeploy службы. Это набор учетных данных по умолчанию hello, настройте в **службы приложений** > **&lt;имя_приложения >** > **учетные данные развертывания**. Это также является hello набор по умолчанию, которая будет отображена в портале hello графического интерфейса пользователя (например hello **Обзор** и **свойства** вашего приложения [колонки ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources)).

    > [!NOTE]
    > При делегировании доступа к ресурсам tooAzure посредством управления на основе доступа ролей (RBAC) или соадминистратором разрешения каждого Azure пользователя, который получает доступ tooan приложения можно использовать своих личных учетных данных уровня пользователя, пока не отменяется доступ. Эти учетные данные развертывания не следует использовать совместно с другими пользователями Azure.
    >
    >

* **Учетные данные на уровне приложения**. Это единый набор учетных данных для каждого приложения. Это может быть только используемые toodeploy toothat приложения. Hello учетные данные для каждого приложения создается автоматически при создании приложения, а также находится в приложение hello профиль публикации. Нельзя вручную настроить учетные данные hello, но вы можете сбросить их для приложения в любое время.

    > [!NOTE]
    > В порядке toogive кто-то toothese учетные данные для доступа через доступа на основе элемента управления (РОЛЕЙ), вы должны toomake их участника или более поздней версии на веб-приложения hello. Средства чтения не разрешены toopublish и недоступен, поэтому эти учетные данные.
    >
    >

## <a name="userscope"></a>Установка и сброс учетных данных на уровне пользователя

Учетные данные на уровне пользователя можно настроить в [колонке ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources) любого приложения. Независимо от на какие приложения вам следует настроить эти учетные данные, он применяет tooall приложений и для всех подписок в Azure учетная запись. 

tooconfigure учетные данные уровня пользователя:

1. В hello [портал Azure](https://portal.azure.com), щелкните службы приложений >  **&lt;any_app >** > **учетные данные развертывания**.

    > [!NOTE]
    > На портале hello необходимо иметь хотя бы одно приложение перед обращением к колонке учетные данные развертывания hello. Однако при наличии hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), можно настроить учетные данные уровня пользователя без существующего приложения.

2. Настройте hello имя пользователя и пароль и нажмите кнопку **Сохранить**.

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

После задания учетных данных развертывания можно найти hello *Git* развертывания имени пользователя в вашем приложении **Обзор**,

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

а имя пользователя для развертывания *FTP* — в разделе **Свойства** для приложения.

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> Azure не отображает пароль развертывания на уровне пользователя. Если вы забудете пароль hello, его нельзя восстановить. Тем не менее можно сбросить учетные данные с помощью инструкции hello в этом разделе.
>
>  

## <a name="appscope"></a>Установка и сброс учетных данных на уровне приложений
Для каждого приложения в службе приложений свои учетные данные уровня приложения хранятся в hello XML профиля публикации.

учетные данные уровня приложения hello tooget:

1. В hello [портал Azure](https://portal.azure.com), щелкните службы приложений >  **&lt;any_app >** > **Обзор**.

2. Щелкните **Дополнительно** > **Получить профиль публикации**. Начнется загрузка файла с расширением .PublishSettings.

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. Откройте hello. Файл параметров публикации и найти hello `<publishProfile>` тег с атрибутом hello `publishMethod="FTP"`. Получите из него атрибуты `userName` и `password`.
Это учетные данные уровня приложения hello.

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    Подобных учетных данных toohello уровня пользователя имя пользователя hello FTP развертывания имеет формат hello `<app_name>\<username>`, и имя пользователя развертывания Git hello является просто `<username>` без hello выше `<app_name>\`.

учетные данные уровня приложения hello tooreset:

1. В hello [портал Azure](https://portal.azure.com), щелкните службы приложений >  **&lt;any_app >** > **Обзор**.

2. Щелкните **Дополнительно** > **Сбросить профиль публикации**. Нажмите кнопку **Да** Сброс tooconfirm hello.

    Действие reset Hello делает недействительными все загруженные ранее. Файлы параметров публикации.

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как toouse toodeploy эти учетные данные приложения из [local Git](app-service-deploy-local-git.md) или с помощью [FTP/S](app-service-deploy-ftp.md).
