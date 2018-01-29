---
title: "Создание масштабируемого набора виртуальных машин Linux с помощью шаблона Azure | Документация Майкрософт"
description: "Узнайте, как быстро создать масштабируемый набор виртуальных машин Linux с помощью шаблона Azure Resource Manager, который позволяет развернуть пример приложения и настроить правила автоматического масштабирования."
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/19/2017
ms.author: iainfou
ms.openlocfilehash: b07bdd0739dabb05ef7012051b7ac28af3aaddaf
ms.sourcegitcommit: 901a3ad293669093e3964ed3e717227946f0af96
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="create-a-linux-virtual-machine-scale-set-with-an-azure-template"></a>Создание масштабируемого набора виртуальных машин Linux с помощью шаблона Azure
Масштабируемый набор виртуальных машин обеспечивает развертывание и администрирование набора идентичных автомасштабируемых виртуальных машин. Вы можете вручную изменить число виртуальных машин в масштабируемом наборе или определить правила для автоматического масштабирования на основе использования ЦП, объема памяти или сетевого трафика. Следуя инструкциям этого руководства, вы создадите масштабируемый набор виртуальных машин Linux с помощью шаблона Azure Resource Manager. Вы также можете создать масштабируемый набор с помощью [Azure CLI 2.0](virtual-machine-scale-sets-create-cli.md), [Azure PowerShell](virtual-machine-scale-sets-create-powershell.md) или [портала Azure](virtual-machine-scale-sets-create-portal.md).

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если вы решили установить и использовать интерфейс командной строки локально, то для работы с этим руководством вам понадобится Azure CLI 2.0.20 или более поздней версии. Чтобы узнать версию, выполните команду `az --version`. Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="define-a-scale-set-in-a-template"></a>Определение масштабируемого набора в шаблоне
Шаблоны Azure Resource Manager позволяют развернуть группы связанных ресурсов. Шаблоны написаны в формате JSON (нотация объектов JavaScript) и определяют всю среду инфраструктуры Azure для приложения. С помощью одного шаблона можно создать масштабируемый набор виртуальных машин, установить приложения и настроить правила автоматического масштабирования. Вы можете повторно использовать этот шаблон, применив переменные и параметры, чтобы обновить существующие или создать дополнительные масштабируемые наборы. Шаблоны можно развернуть с помощью портала Azure, Azure CLI 2.0 или Azure PowerShell либо же на основе конвейеров непрерывной интеграции и непрерывной поставки (CI/CD).

Дополнительные сведения о шаблонах см. в [обзоре Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment).

Чтобы создать масштабируемый набор с помощью шаблона, определите необходимые ресурсы. Ниже перечислены основные элементы и типы ресурсов для масштабируемого набора виртуальных машин.

| Свойство                     | Описание свойства                                  | Пример значения в шаблоне                    |
|------------------------------|----------------------------------------------------------|-------------------------------------------|
| Тип                         | Создаваемый тип ресурса Azure                            | Microsoft.Compute/virtualMachineScaleSets; |
| name                         | Имя масштабируемого набора                                       | myScaleSet                                |
| location                     | Расположение для создания масштабируемого набора                     | Восток США                                   |
| sku.name                     | Размер виртуальной машины для каждого экземпляра в масштабируемом наборе                  | Standard_A1                               |
| sku.capacity                 | Количество экземпляров виртуальных машин, которое требуется изначально создать           | 2                                         |
| upgradePolicy.mode           | Режим обновления экземпляра виртуальной машины при внесении изменений              | Автоматический                                 |
| imageReference               | Платформа или пользовательский образ, используемые для экземпляров виртуальных машин | Сервер Canonical Ubuntu 16.04-LTS         |
| osProfile.computerNamePrefix | Префикс имени для каждого экземпляра виртуальной машины                     | myvmss                                    |
| osProfile.adminUsername      | Имя пользователя для каждого экземпляра виртуальной машины                        | azureuser                                 |
| osProfile.adminPassword      | Пароль для каждого экземпляра виртуальной машины                        | P@ssw0rd!                                 |

 В примере ниже показано определение основных ресурсов для масштабируемого набора. Вы можете персонализировать этот шаблон масштабируемого набора, например изменить размер виртуальной машины или начальную емкость, а также использовать другую платформу или пользовательский образ.

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "myScaleSet",
  "location": "East US",
  "apiVersion": "2017-12-01",
  "sku": {
    "name": "Standard_A1",
    "capacity": "2"
  },
  "properties": {
    "upgradePolicy": {
      "mode": "Automatic"
    },
    "virtualMachineProfile": {
      "storageProfile": {
        "osDisk": {
          "caching": "ReadWrite",
          "createOption": "FromImage"
        },
        "imageReference":  {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "16.04-LTS",
          "version": "latest"
        }
      },
      "osProfile": {
        "computerNamePrefix": "myvmss",
        "adminUsername": "azureuser",
        "adminPassword": "P@ssw0rd!"
      }
    }
  }
}
```

 Для краткости в этом примере не показана конфигурация адаптера виртуальной сети. Также не показаны дополнительные компоненты, такие как подсистема балансировки нагрузки. Полный шаблон масштабируемого набора приведен [в конце этой статьи](#deploy-the-template).


## <a name="install-an-application"></a>Установка приложения
Когда развертывается масштабируемый набор, расширения виртуальных машин позволяют создать задачи автоматизации и настройки после развертывания, например для установки приложения. Сценарии можно скачать из службы хранилища Azure или GitHub или передать на портал Azure во время выполнения расширения. Чтобы применить расширение к масштабируемому набору, добавьте раздел *extensionProfile* в предыдущий пример ресурса. Как правило, профиль расширения определяет следующие свойства:

- тип расширения;
- издатель расширения;
- версия расширения;
- расположение скриптов настройки или установки;
- команды для выполнения на экземплярах виртуальных машин.

Шаблон [HTTP-сервера Python под управлением Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) использует настраиваемое расширение скриптов для установки [Bottle](http://bottlepy.org/docs/dev/), веб-платформы Python и простого HTTP-сервера. 

Два скрипта определены в файлах **fileUris** - *installserver.sh* и *workserver.py*. Эти файлы загружаются из GitHub, затем *commandToExecute* выполняет `bash installserver.sh` для установки и настройки приложения:

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "AppInstall",
      "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "fileUris": [
            "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
            "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
          ],
          "commandToExecute": "bash installserver.sh"
        }
      }
    }
  ]
}
```


## <a name="deploy-the-template"></a>Развертывание шаблона
Шаблон [HTTP-сервера Python под управлением Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) можно развернуть с помощью кнопки **Deploy to Azure** (Развернуть в Azure). После ее нажатия откроется портал Azure, загрузится весь шаблон и появится диалог для ввода параметров, таких как имя масштабируемого набора, число экземпляров и учетные данные администратора.

[![Развертывание шаблона в Azure](media/virtual-machine-scale-sets-create-template/deploy-button.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-vmss-bottle-autoscale%2Fazuredeploy.json)

Вы можете также использовать Azure CLI 2.0 для установки HTTP-сервера Python под управлением Linux с помощью команды [az group deployment create](/cli/azure/group/deployment#create), как показано ниже.

```azurecli-interactive
# Create a resource group
az group create --name myResourceGroup --location EastUS

# Deploy template into resource group
az group deployment create \
    --resource-group myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/azuredeploy.json
```

В ответ на запросы предоставьте имя масштабируемого набора, число экземпляров и учетные данные администратора для экземпляров виртуальных машин. Создание масштабируемого набора и вспомогательных ресурсов занимает несколько минут.


## <a name="test-your-sample-application"></a>Проверка примера приложения
Чтобы просмотреть, как работает приложение, получите общедоступный IP-адрес подсистемы балансировки нагрузки с помощью команды [az network public-ip list](/cli/azure/network/public-ip#show):

```azurecli-interactive
az network public-ip list \
    --resource-group myResourceGroup \
    --query [*].ipAddress -o tsv
```

Введите в браузер общедоступный IP-адрес своей подсистемы балансировки нагрузки в формате *http://общедоступный_IP_адрес:9000/имя_приложения*. Подсистема балансировки нагрузки передаст запрос на один из экземпляров виртуальной машины, как показано в следующем примере:

![Веб-страница NGINX по умолчанию](media/virtual-machine-scale-sets-create-template/running-python-app.png)


## <a name="clean-up-resources"></a>Очистка ресурсов
Вы можете удалить ненужную группу ресурсов, масштабируемый набор и все связанные ресурсы с помощью команды [az group delete](/cli/azure/group#delete), как показано ниже.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Дополнительная информация
В этом руководстве вы создали масштабируемый набор Linux с помощью шаблона Azure и применили расширение пользовательского скрипта, чтобы установить базовый веб-сервер NGINX на экземплярах виртуальной машины. Следующие руководства помогут вам расширить возможности масштабируемого набора, чтобы улучшить масштабируемость и автоматизацию.

- [Развертывание приложения в масштабируемых наборах виртуальных машин](virtual-machine-scale-sets-deploy-app.md)
- Автоматическое масштабирование масштабируемых наборов виртуальных машин с помощью [Azure CLI](virtual-machine-scale-sets-autoscale-cli.md), [Azure PowerShell](virtual-machine-scale-sets-autoscale-powershell.md) или [портала Azure](virtual-machine-scale-sets-autoscale-portal.md)
- [Автоматические обновления ОС масштабируемого набора виртуальных машин Azure](virtual-machine-scale-sets-automatic-upgrade.md)
