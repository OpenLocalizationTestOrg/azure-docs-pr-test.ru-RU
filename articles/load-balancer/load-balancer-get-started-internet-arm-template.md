---
title: "Подсистема балансировки нагрузки aaaCreate с выходом в Интернет - шаблон Azure | Документы Microsoft"
description: "Узнайте, как в диспетчере ресурсов с помощью шаблона подсистемы балансировки нагрузки, toocreate из Интернета"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a>Создание балансировщика нагрузки для Интернета с помощью шаблона

> [!div class="op_single_selector"]
> * [Портал](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Шаблон](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello модели развертывания диспетчера ресурсов. Вы также можете [Узнайте, как с помощью классической модели развертывания подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Развертывание с помощью шаблона hello щелкните toodeploy

шаблон Образец Hello доступны в репозитории открытого hello использует параметр файл, содержащий сценарий hello по умолчанию значения, используемые toogenerate hello, описанный выше. toodeploy это с помощью шаблона щелкните toodeploy, выполните [эту ссылку](http://go.microsoft.com/fwlink/?LinkId=544801), нажмите кнопку **развертывание tooAzure**, замените значения параметров по умолчанию hello при необходимости и следуйте инструкциям hello hello портала.

## <a name="deploy-hello-template-by-using-powershell"></a>Развертывание hello шаблона с помощью PowerShell

toodeploy hello шаблона, загруженного с помощью PowerShell, выполните шаги hello.

1. Если ранее не пользовались Azure PowerShell, см. раздел [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) и следуйте инструкциям hello все toohello hello способом завершения toosign в Azure и выберите свою подписку.
2. Запустите hello **New AzureRmResourceGroupDeployment** Здравствуйте, командлет toocreate группы ресурсов с помощью шаблона.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
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

3. В браузере перейдите слишком[hello шаблоном краткого руководства](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), скопируйте содержимое hello hello json-файл и вставьте его в новый файл на своем компьютере. Для этого сценария будет копирование значений hello ниже tooa файл с именем **c:\lb\azuredeploy.parameters.json**.
4. Запустите hello **создайте группу azure развертывания** командлет toodeploy hello новую подсистему балансировки загрузки с помощью шаблона hello и параметр файлы загружаются и изменить выше. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a>Дальнейшие действия

[Приступая к настройке внутренней подсистемы балансировки нагрузки](load-balancer-get-started-ilb-arm-ps.md)

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
