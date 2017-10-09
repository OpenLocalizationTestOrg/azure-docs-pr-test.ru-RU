---
title: "Шлюз приложений Azure — шаблоны aaaCreate | Документы Microsoft"
description: "Эта страница содержит toocreate инструкции шлюза приложения Azure с помощью шаблона Azure Resource Manager hello"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a>Создание шлюза приложения с помощью шаблона Azure Resource Manager hello

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-gateway-arm.md)
> * [Классическая модель — Azure PowerShell](application-gateway-create-gateway.md)
> * [Шаблон диспетчера ресурсов Azure](application-gateway-create-gateway-arm-template.md)
> * [Интерфейс командной строки Azure](application-gateway-create-gateway-cli.md)

Шлюз приложений — это балансировщик нагрузки уровня 7. Он предоставляет отработки отказа и маршрутизации производительности HTTP-запросов между различными серверами, являются ли они на hello облачной или локальной. Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку SSL, выполнение пользовательской проверки работоспособности, поддержку нескольких сайтов и т. д. Полный список поддерживаемых функций toofind посетите [Обзор шлюза приложения](application-gateway-introduction.md)

В этой статье описывается загрузка и изменение существующего шаблона диспетчера ресурсов Azure из GitHub и развертывания шаблона hello из GitHub, PowerShell и hello Azure CLI.

При развертывании просто hello шаблона диспетчера ресурсов Azure непосредственно из GitHub без изменений, пропустите toodeploy шаблона в GitHub.

## <a name="scenario"></a>Сценарий

Из этой статьи вы узнаете:

* как создать шлюз приложений с брандмауэром веб-приложения;
* как создать виртуальную сеть с именем VirtualNetwork1 и зарезервированным блоком CIDR (10.0.0.0/16);
* как создать подсеть с именем Appgatewaysubnet и блоком CIDR (10.0.0.0/28);
* Требуется настроить два ранее настроенный серверной части IP-адреса для веб-серверов hello tooload Балансировка трафика hello. В этом примере шаблон hello серверной части IP-адреса являются 10.0.1.10 и 10.0.1.11.

> [!NOTE]
> Эти параметры являются параметрами hello для этого шаблона. toocustomize hello шаблона, можно изменить правила, прослушиватель hello, SSL и другие параметры в файле azuredeploy.json hello.

![Сценарий](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Загрузите и понять hello шаблона диспетчера ресурсов Azure

Можно загрузить шаблон toocreate hello существующего диспетчера ресурсов Azure виртуальной сети и две подсети из GitHub, внесите изменения можно будет и использовать его. Таким образом, toodo используйте hello следующие шаги:

1. Перейдите в слишком[создать шлюз приложения при включенном брандмауэре приложения web](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).
1. Щелкните **azuredeploy.json** и нажмите кнопку **RAW**.
1. Сохранение hello файл tooa локальную папку на компьютере.
1. Если вы знакомы с шаблоны Azure Resource Manager, пропустите toostep 7.
1. Откройте сохраненный файл hello и просмотрите содержимое hello в **параметры** в строке
1. В параметрах шаблона ARM есть заполнитель для значений, которые могут подставляться во время развертывания.

  | Параметр | Описание |
  | --- | --- |
  | **subnetPrefix** |Блок CIDR для подсети шлюза приложения hello. |
  | **applicationGatewaySize** | Размер шлюза приложения hello.  WAF позволяет только средний и крупный. |
  | **backendIpaddress1** |IP-адрес hello первого веб-сервера. |
  | **backendIpaddress2** |IP-адрес hello второй веб-сервер. |
  | **wafEnabled** | Параметр toodetermine, если включен WAF.|
  | **wafMode** | Режим hello брандмауэр веб-приложения.  Доступные варианты: **Предотвращение** или **Защита**.|
  | **wafRuleSetType** | Тип набора правил для WAF.  В настоящее время OWASP — hello поддерживается только параметр. |
  | **wafRuleSetVersion** |Версия набора правил. CRS OWASP 2.2.9 и 3.0 в настоящий момент параметры hello поддерживается. |

1. Проверьте содержимое hello в **ресурсов** и уведомление hello следующие свойства:

   * **type**. Тип ресурса, создаваемого шаблоном hello. В этом случае тип hello — `Microsoft.Network/applicationGateways`, который представляет шлюз приложений.
   * **name**. Имя ресурса hello. Использование уведомления hello `[parameters('applicationGatewayName')]`, что означает это имя hello предоставляется как вход пользователем или файл параметров во время развертывания.
   * **properties**. Список свойств для ресурса hello. Этот шаблон использует hello виртуальную сеть и общедоступный IP-адрес во время создания шлюза приложения.

   > [!NOTE]
   > Дополнительные сведения о шаблонах Resource Manager см. [здесь](/templates/).

1. Переход назад слишком[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).
1. Щелкните **azuredeploy-parameters.json** и нажмите кнопку **RAW**.
1. Сохранение hello файл tooa локальную папку на компьютере.
1. Откройте сохраненный файл hello и отредактируйте hello значения для параметров hello. Используйте следующие значения toodeploy hello приложения шлюза, описанной в нашем сценарии hello.

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. Сохраните файл hello. Можно проверить hello JSON и параметра шаблона с помощью документации средства проверки JSON, как [JSlint.com](http://www.jslint.com/).

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a>Развертывание шаблона hello диспетчера ресурсов Azure с помощью PowerShell

Если ранее не пользовались Azure PowerShell, посетите: [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) и следуйте инструкциям toosign hello в Azure и выберите свою подписку.

1. TooPowerShell входа

    ```powershell
    Login-AzureRmAccount
    ```

1. Проверьте hello подписки для учетной записи hello.

    ```powershell
    Get-AzureRmSubscription
    ```

    С помощью учетных данных, запрашиваемых tooauthenticate.

1. Выберите, какие toouse вашей подписки Azure.

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. При необходимости создайте группу ресурсов с помощью hello **New AzureResourceGroup** командлета. В следующем примере hello создать группу ресурсов под названием AppgatewayRG в расположении, восток США.

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. Запустите hello **New AzureRmResourceGroupDeployment** командлет toodeploy hello новую виртуальную сеть с помощью hello предшествующий файлы шаблонов и параметров загрузки и изменения.
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a>Развертывание с помощью Azure CLI hello hello шаблона диспетчера ресурсов Azure

toodeploy hello Azure Resource Manager загруженный шаблон с помощью Azure CLI, выполните следующие шаги hello.

1. Если ранее не пользовались Azure CLI, см. раздел [установить и настроить hello Azure CLI](/cli/azure/install-azure-cli) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.

1. При необходимости выполнения hello `az group create` команда toocreate группы ресурсов, как показано в следующий фрагмент кода hello. Обратите внимание, hello выходные данные команды hello. Список Hello отображаться после вывода hello объясняется hello параметров, используемых. Дополнительные сведения о группах ресурсов см. в статье [Общие сведения о диспетчере ресурсов Azure](../azure-resource-manager/resource-group-overview.md).

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (или --name)**. Имя для новой группы ресурсов hello. В нашем примере это *appgatewayRG*.
    
    **-l (или --location)**. Регион Azure, где создается новая группа ресурсов hello. В нашем примере это *westus*.

1. Запустите hello `az group deployment create` командлет toodeploy hello новую виртуальную сеть с помощью шаблона hello и параметр файлы загружены и изменен в предшествующих шаг hello. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a>Развертывание шаблона hello Azure Resource Manager с помощью щелкните развертывание

Нажмите кнопку развертывания является другим способом toouse шаблоны Azure Resource Manager. Это легко toouse шаблонов hello портал Azure.

1. Go слишком[создать шлюз приложений с брандмауэр веб-приложения](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).

1. Нажмите кнопку **развертывание tooAzure**.

    ![Развертывание tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Заполните параметры hello hello шаблон развертывания на портале hello и нажмите кнопку **ОК**.

    ![Параметры](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. Выберите **я принимаю условия, указанных выше, toohello** и нажмите кнопку **покупки**.

1. В колонке развертывания пользовательского hello, нажмите кнопку **создать**.

## <a name="providing-certificate-data-tooresource-manager-templates"></a>Предоставление сертификата tooResource данных диспетчер шаблонов

При использовании SSL с помощью шаблона, hello сертификат должен toobe в строку base64, вместо загружена. Строка base64 tooa PFX или CER tooconvert используйте одну из hello, следующие команды. Hello ниже команды преобразуют hello сертификат tooa base64 строку, которая может быть указано toohello шаблона. Hello тесты на ожидаемые выходные данные — это строка, хранится в переменной и вставить в шаблоне hello.

### <a name="macos"></a>macOS
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a>Windows
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a>Удаление всех ресурсов

toodelete все ресурсы, которые созданы в этой статье, выполнение одного из hello следующие шаги:

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>Инфраструктура CLI Azure

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>Дальнейшие действия

Если вы хотите tooconfigure разгрузки SSL, посетите: [настройки шлюза приложения для разгрузки SSL](application-gateway-ssl.md).

Если вы хотите tooconfigure toouse шлюза приложения с внутренней подсистемы балансировки нагрузки, посетите: [создать шлюз приложений с внутренней подсистемы балансировки нагрузки (ILB)](application-gateway-ilb.md).

Дополнительные сведения о параметрах балансировки нагрузки в целом см. в статьях:

* [Подсистема балансировщика нагрузки Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

