---
title: "aaaCreate внутренний балансировщик нагрузки - шаблон Azure | Документы Microsoft"
description: "Узнайте, как в диспетчере ресурсов с помощью шаблона подсистемы балансировки нагрузки, toocreate во внутренний"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a>Создайте внутренний балансировщик нагрузки с помощью шаблона

> [!div class="op_single_selector"]
> * [портале Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Шаблон](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).  В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Развертывание с помощью шаблона hello щелкните toodeploy

шаблон Образец Hello доступны в репозитории открытого hello использует параметр файл, содержащий сценарий hello по умолчанию значения, используемые toogenerate hello, описанный выше. toodeploy это с помощью шаблона щелкните toodeploy, выполните [эту ссылку](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello при необходимости и следуйте инструкциям hello hello портала.

## <a name="deploy-hello-template-by-using-powershell"></a>Развертывание hello шаблона с помощью PowerShell

toodeploy hello шаблона, загруженного с помощью PowerShell, выполните шаги hello.

1. Если ранее не пользовались Azure PowerShell, см. раздел [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) и следуйте инструкциям hello все toohello hello способом завершения toosign в Azure и выберите свою подписку.
2. Загрузите локальном диске файл параметров tooyour hello.
3. Измените файл hello и сохраните его.
4. Запустите hello **New AzureRmResourceGroupDeployment** Здравствуйте, командлет toocreate группы ресурсов с помощью шаблона.

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Развертывание hello шаблона с помощью hello Azure CLI

toodeploy hello шаблона с использованием hello Azure CLI, выполните шаги hello.

1. Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello **azure конфигурации режима** tooswitch tooResource Manager режим команд, как показано ниже.

    ```azurecli
    azure config mode arm
    ```

    Вот hello ожидается выходных данных для приведенных выше команд hello.

        info:    New mode is arm

3. Откройте файл параметров hello, выберите его содержимое и сохраните файл tooa на своем компьютере. В этом примере мы сохранить файл параметров hello слишком*parameters.json*.
4. Запустите hello **создайте группу azure развертывания** toodeploy hello новый внутренней подсистемы балансировки нагрузки с помощью шаблонов hello и параметров команды файлы вы загрузили и изменить выше. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a>Дальнейшие действия

[Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)

