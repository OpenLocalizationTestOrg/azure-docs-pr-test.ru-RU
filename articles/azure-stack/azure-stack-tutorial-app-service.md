---
title: "aaaMake веб, мобильных устройств и пользователей стек Azure доступны tooyour приложения API | Документы Microsoft"
description: "Учебника tooinstall hello поставщик ресурсов службы приложений и создание предложения, обеспечивающие вашей стек Azure пользователи hello возможность toocreate web, мобильных устройств и приложения API."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/03/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 62b86cf6288b8f629bc92dade003c712fe523187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="make-web-mobile-and-api-apps-available-tooyour-azure-stack-users"></a>Сделать веб, мобильных устройств и пользователей стек Azure доступны tooyour приложения API

Как администратор облака Azure стека, можно создать предложения, которые позволяют пользователям (клиентов) создавать приложения Azure функции и web, мобильных устройств и API. Путем предоставления доступа пользователям tooyour toothese по требованию, облачные приложения, их можно сэкономить время и ресурсы. tooset этот показатель будет:

> [!div class="checklist"]
> * Развертывание hello поставщик ресурсов службы приложений
> * Создание предложения
> * Предложение hello теста

## <a name="deploy-hello-app-service-resource-provider"></a>Развертывание hello поставщик ресурсов службы приложений

1. [Подготовка узла Azure стека Development Kit hello](azure-stack-app-service-before-you-get-started.md). Это включает в себя развертывание hello поставщик ресурсов SQL Server, который необходим для создания некоторых приложений.
2. [Загрузите скрипты установки и вспомогательные hello](azure-stack-app-service-deploy.md#download-the-required-components).
3. [Запустите сценарий вспомогательный hello toocreate необходимые сертификаты](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).
4. [Установить поставщик ресурсов службы приложения hello](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (может занять несколько часов tooinstall и для всех hello tooappear рабочих ролей).
5. [Проверка установки hello](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).

## <a name="create-an-offer"></a>Создание предложения

Например можно создать предложение, которое позволяет пользователям создавать DNN веб-системы управления содержимым. Он требует hello службы SQL Server, которая уже включена, установив hello поставщик ресурсов SQL Server.

1.  [Задать квоты](azure-stack-setting-quotas.md) и назовите его *AppServiceQuota*. Выберите **Microsoft.Web** для hello **имен** поля.
2.  [Создание плана](azure-stack-create-plan.md). Назовите его *TestAppServicePlan*выберите hello hello **Microsoft.SQL** службы, и **AppService квоты** квоты.

    > [!NOTE]
    > Пользователи toolet создавать другие приложения, в плане hello могут потребоваться другие службы. Например, функции Azure требует этого плана hello hello **хранилища Майкрософт** обслуживание, когда требуется Wordpress **Microsoft.MySQL**.
    > 
    >

3.  [Создать предложение](azure-stack-create-offer.md), назовите его **TestAppServiceOffer** и выберите hello **TestAppServicePlan** плана.

## <a name="test-hello-offer"></a>Предложение hello теста

Теперь, когда вы развернули hello поставщик ресурсов службы приложений и создать предложение, вы сможете войти как пользователь, подписаться toohello предложение и создать приложение. В этом примере мы создадим платформы DNN системы управления контентом. Сначала необходимо создать базу данных SQL и hello DNN веб-приложения.

### <a name="subscribe-toohello-offer"></a>Подписаться на предложение toohello
1. Войдите в toohello портала Azure стека (https://portal.local.azurestack.external) как клиента.
2. Нажмите кнопку **получить подписку** > тип **TestAppServiceSubscription** под **отображаемое имя** > **выберите предложение**  >  **TestAppServiceOffer** > **создания**.

### <a name="create-a-sql-database"></a>Создание базы данных SQL

1. Нажмите кнопку  **+**   >  **данные + хранилище** > **базы данных SQL**.
2. Оставьте hello значения по умолчанию для полей hello, за исключением того, следующим образом:
    - **Имя базы данных**: DNNdb
    - **Максимальный размер в МБ**: 100
    - **Подписки**: TestAppServiceOffer
    - **Группа ресурсов**: DNN RG
3. Нажмите кнопку **параметры входа**, введите учетные данные для базы данных hello и нажмите кнопку **ОК**. Эти учетные данные будут использоваться позже в следующие действия.
4. Нажмите кнопку **SKU** > выберите hello SKU SQL, созданный для hello сервер размещения SQL > **ОК**.
5. Щелкните **Создать**.

### <a name="create-a-dnn-app"></a>Создание приложения DNN    

1. Нажмите кнопку  **+**   >  **все** > **Предварительная версия платформы DNN** > **создать**.
2. Тип *DNNapp* под **имя приложения** и выберите **TestAppServiceOffer** под **подписки**.
3. Нажмите кнопку **настроить необходимые параметры** > **создать новый** > тип **план служб приложений** имя.
4. Нажмите кнопку **Ценовая категория** > **F1 свободного** > **выберите** > **ОК**.
5. Нажмите кнопку **базы данных** и введите данные hello hello базы данных SQL, созданного ранее.
6. Щелкните **Создать**.

Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * Развертывание hello поставщик ресурсов службы приложений
> * Создание предложения
> * Предложение hello теста

Как переместить следующий учебник toolearn toohello для:

> [!div class="nextstepaction"]
> [Развертывание приложений tooAzure и стек Azure](azure-stack-solution-pipeline.md)
