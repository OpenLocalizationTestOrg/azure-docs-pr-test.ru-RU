---
title: "aaaMake SQL базы данных пользователей стек Azure доступны tooyour | Документы Microsoft"
description: "Учебника tooinstall hello поставщик ресурсов SQL Server и создание предложения, позволяющих пользователям Azure стека создавать базы данных SQL."
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
ms.openlocfilehash: 778513ba982981895afe2d57b3b5dda71ead8886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="make-sql-databases-available-tooyour-azure-stack-users"></a>Сделать доступных tooyour стека Azure пользователи баз данных SQL

Как администратор облака Azure стека, можно создать предложения, предоставив пользователям возможность создания баз данных SQL, которые используются с их собственный облачных приложений, веб-сайты и рабочие нагрузки (клиентами). Предоставляя эти пользовательские, по запросу, tooyour пользователей баз данных на основе облака, их можно сохранить время и ресурсы. tooset этот показатель будет:

> [!div class="checklist"]
> * Разверните hello поставщик ресурсов SQL Server
> * Создание предложения
> * Предложение hello теста

## <a name="deploy-hello-sql-server-resource-provider"></a>Разверните hello поставщик ресурсов SQL Server

процесс развертывания Hello подробно в hello [баз данных SQL используйте статьи стек Azure](azure-stack-sql-resource-provider-deploy.md)и состоит из следующих основных шага hello:

1.  [Развертывание поставщика ресурсов SQL hello]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).
2.  [Проверка развертывания hello]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).
3.  [Предоставляют емкость, подключив tooa, где размещен SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).

## <a name="create-an-offer"></a>Создание предложения

1.  [Задать квоты](azure-stack-setting-quotas.md) и назовите его *SQLServerQuota*. Выберите **Microsoft.SQLAdapter** для hello **имен** поля.
2.  [Создание плана](azure-stack-create-plan.md). Назовите его *TestSQLServerPlan*выберите hello **Microsoft.SQLAdapter** службы, и **SQLServerQuota** квоты.

    > [!NOTE]
    > Пользователи toolet создавать другие приложения, в плане hello могут потребоваться другие службы. Например, функции Azure требует этого плана hello hello **хранилища Майкрософт** обслуживание, когда требуется Wordpress **Microsoft.MySQLAdapter**.
    > 
    >

3.  [Создать предложение](azure-stack-create-offer.md), назовите его **TestSQLServerOffer** и выберите hello **TestSQLServerPlan** плана.

## <a name="test-hello-offer"></a>Предложение hello теста

Теперь, когда вы развернули hello поставщик ресурсов SQL Server и создать предложение, вы сможете войти как пользователь, подписаться toohello предложение и создать базу данных.

### <a name="subscribe-toohello-offer"></a>Подписаться на предложение toohello
1. Войдите в toohello портала Azure стека (https://portal.local.azurestack.external) как клиента.
2. Нажмите кнопку **получить подписку** , а затем введите **TestSQLServerSubscription** под **отображаемое имя**.
3. Нажмите кнопку **выберите предложение** > **TestSQLServerOffer** > **создать**.
4. Нажмите кнопку **дополнительные службы** > **подписки** > **TestSQLServerSubscription** > **ресурсов Поставщики**.
5. Нажмите кнопку **зарегистрировать** Далее toohello **Microsoft.SQLAdapter** поставщика.

### <a name="create-a-sql-database"></a>Создание базы данных SQL

1. Нажмите кнопку  **+**   >  **данные + хранилище** > **базы данных SQL**.
2. Значения по умолчанию hello оставьте поля hello, или можно использовать эти примеры:
    - **Имя базы данных**: SQLdb
    - **Максимальный размер в МБ**: 100
    - **Подписки**: TestSQLOffer
    - **Группа ресурсов**: SQL RG
3. Нажмите кнопку **параметры входа**, введите учетные данные для базы данных hello и нажмите кнопку **ОК**.
4. Нажмите кнопку **SKU** > выберите hello SKU SQL, созданный для hello сервер размещения SQL > **ОК**.
5. Щелкните **Создать**.

Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * Разверните hello поставщик ресурсов SQL Server
> * Создание предложения
> * Предложение hello теста

Как переместить следующий учебник toolearn toohello для:

> [!div class="nextstepaction"]
> [Сделать web, мобильных устройств и пользователей доступны tooyour приложения API]( azure-stack-tutorial-app-service.md)

