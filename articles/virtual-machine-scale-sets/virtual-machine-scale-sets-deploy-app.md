---
title: "Задает aaaDeploy приложения на масштабирования виртуальных машин"
description: "Наборы масштабирования виртуальных машин Azure используйте toodepoy расширения приложения."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>Развертывание приложения в масштабируемых наборах виртуальных машин

В этой статье описываются различные способы как задать tooinstall программное обеспечение в масштабе hello hello время подготовки.

Вы можете tooreview hello [Обзор разработки установите масштаб](virtual-machine-scale-sets-design-overview.md) статьи, которая описывает некоторые hello ограничения, накладываемые наборы масштабирования виртуальных машин.

## <a name="capture-and-reuse-an-image"></a>Запись и повторное использование образа

Можно использовать виртуальную машину, заданные в Azure tooprepare базового образа для масштаба. Этот процесс создает управляемого диска вашей учетной записи хранилища, который может ссылаться в качестве базового образа hello для набора масштабирования. 

Здравствуйте, следующие действия:

1. Создайте виртуальную машину Azure
   * [Linux][linux-vm-create]
   * [Windows][windows-vm-create]

2. В удаленном hello виртуальной машины и настроить оформлением tooyour hello системы.

   Теперь вы можете установить приложение. Однако следует помнить, что путем установки приложения, вы можете сделать обновление более сложные приложения, так как может потребоваться tooremove его первого. Вместо этого можно использовать этот шаг tooinstall все необходимые компоненты, которые могут потребоваться приложение, например определенных компонентов операционной системы или среды выполнения.

3. Выполните действия из учебника «запись машины» hello либо для [Linux] [ linux-vm-capture] или [Windows][windows-vm-capture].

4. Создание [набора масштабирования виртуальных машин] [ vmss-create] с hello изображения URI, записанный в предыдущем шаге hello.

Дополнительные сведения о дисках см. в статьях [Обзор управляемых дисков](../virtual-machines/windows/managed-disks-overview.md) и [Использование подключенных дисков данных](virtual-machine-scale-sets-attached-disks.md).

## <a name="install-when-hello-scale-set-is-provisioned"></a>Установка при подготовке набор масштабирования hello

Расширения виртуальных машин может быть применен tooa набора масштабирования виртуальных машин. Расширение виртуальной машины позволяет настраивать hello виртуальных машин в качестве всей группы масштабирования. Дополнительные сведения о расширениях см. в статье, посвященной [расширениям виртуальных машин](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Вы можете использовать три основных расширения в зависимости от типа операционной системы: Linux или Windows.

### <a name="windows"></a>Windows

Для операционной системы на основе Windows, используйте либо hello **версии 1.8 пользовательский сценарий** расширения или hello **PowerShell DSC** расширения.

#### <a name="custom-script"></a>Custom Script

Hello расширение пользовательского скрипта запускает сценарий на каждом экземпляре виртуальной машины в наборе масштабирования hello. Файл конфигурации или переменная указывает файлы, загруженные toohello виртуальной машины, а затем выполняет команду. Можно использовать этот установщик toorun, сценария, пакетный файл любых исполняемых файлов, например.

PowerShell использует хэш-таблицу для параметров hello. В этом примере настраивается toorun расширение пользовательского скрипта hello сценарий PowerShell, установка служб IIS.

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Используйте hello `-ProtectedSetting` переключения для любых параметров, которые могут содержать конфиденциальные сведения.

---------


Azure CLI использует файл json для параметров hello. В этом примере настраивается toorun расширение пользовательского скрипта hello сценарий PowerShell, установка служб IIS. Сохранить следующие файл json как hello _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

Затем выполните следующую команду Azure CLI.

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Используйте hello `--protected-settings` переключения для любых параметров, которые могут содержать конфиденциальные сведения.

### <a name="powershell-dsc"></a>PowerShell DSC

Можно использовать PowerShell DSC toocustomize hello шкалы набор экземпляров виртуальных машин. Hello **DSC** опубликованное расширение **Microsoft.Powershell** развертывает и запускает конфигурацию DSC hello указано на каждый экземпляр виртуальной машины. Файл конфигурации или переменной указывает расширение hello где *.zip* пакета, а какие _функции скрипта_ toorun сочетания.

PowerShell использует хэш-таблицу для параметров hello. В этом примере развертывается пакет DSC, который устанавливает службы IIS.

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Используйте hello `-ProtectedSetting` переключения для любых параметров, которые могут содержать конфиденциальные сведения.

-----------

Azure CLI использует json для параметров hello. В этом примере развертывается пакет DSC, который устанавливает службы IIS. Сохранить следующие файл json как hello _settings.json_.

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

Затем выполните следующую команду Azure CLI.

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Используйте hello `--protected-settings` переключения для любых параметров, которые могут содержать конфиденциальные сведения.

### <a name="linux"></a>Linux

Linux можно использовать либо hello **v2.0 пользовательский сценарий** расширения или используйте **облака init** во время создания.

Пользовательский скрипт является простой расширение, которое загружает файлы экземпляров виртуальных машин toohello и выполняет команду.

#### <a name="custom-script"></a>Custom Script

Сохранить следующие файл json как hello _settings.json_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

Используйте этот tooan расширение существующего набора масштабирования виртуальных машин tooadd hello Azure CLI. Каждая виртуальная машина в шкале hello автоматически задать расширение hello запусков.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Используйте hello `--protected-settings` переключения для любых параметров, которые могут содержать конфиденциальные сведения.

#### <a name="cloud-init"></a>Cloud-Init

Init облако используется при создании набора масштабирования hello. Сначала создайте локальный файл с именем _init.txt облака_ и добавьте tooit вашей конфигурации. Например, ознакомьтесь с [этой статьей](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt).

Задать использование hello Azure CLI toocreate шкалу. Hello `--custom-data` hello имя файла скрипта облака init принимает поле.

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a>Как управлять обновлениями приложений?

Если вы развернули приложение через расширение, измените определение расширения hello иным образом. В результате изменения экземпляров виртуальных машин tooall toobe повторного развертывания расширения hello. Что-то **должен** изменить сведения о расширении hello, таких как переименование указанный файл, в противном случае Azure выполняет не. при этом hello расширение изменилось.

Если приложение hello помещенного в свой собственный образ операционной системы, используйте конвейер автоматического развертывания для обновлений приложения. Разработка вашей архитектуры toofacilitate Быстрая замена промежуточные шкалы набор в рабочей среде. Хорошим примером такого подхода является hello [работы драйвера Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).

[Packer](https://www.packer.io/) и [Terraform](https://www.terraform.io/) поддержки диспетчера ресурсов Azure, поэтому можно определить образы «как код» и создавать их в Azure, затем с помощью hello виртуального жесткого диска в наборе масштабирования. Но такой подход не подходит для образов Marketplace, в которых расширения и пользовательские сценарии более важны, так как вы не оперируете данными из Marketplace напрямую.

## <a name="what-happens-when-a-scale-set-scales-out"></a>Что происходит при расширении масштабируемого набора?
При добавлении одного или нескольких виртуальных машин tooa набор масштабирования приложения hello устанавливается автоматически. Для примера, если задать масштаб hello имеет расширения, определенные, выполняются на новую виртуальную машину при каждом его создания. Если набор масштабирования hello основана на пользовательский образ, любой новой виртуальной машины является копией hello источник пользовательского изображения. Если узлы контейнера hello шкалы набор виртуальных машин, может иметь hello tooload контейнеры для запуска кода в настраиваемое расширение скриптов. Кроме того, расширение может устанавливать агент, который регистрируется в оркестраторе кластера, например в службе контейнеров Azure.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>Как можно развернуть обновление ОС в доменах обновления?
Предположим, что нужно tooupdate образа ОС, сохраняя hello масштабирования виртуальных машин установите под управлением. PowerShell и hello Azure CLI можно обновить образы виртуальных машин hello, одной виртуальной машине одновременно. Hello [обновление набора масштабирования виртуальных машин](./virtual-machine-scale-sets-upgrade-scale-set.md) статье также приводятся дополнительные сведения на какие параметры будут доступны tooperform обновления операционной системы в наборе масштабирования виртуальных машин.

## <a name="next-steps"></a>Дальнейшие действия

* [Используйте PowerShell toomanage набора параметров масштабирования.](virtual-machine-scale-sets-windows-manage.md)
* [Создание шаблона масштабируемого набора](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

