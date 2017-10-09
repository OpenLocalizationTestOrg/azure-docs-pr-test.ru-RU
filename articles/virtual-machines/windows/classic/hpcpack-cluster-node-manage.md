---
title: "кластер HPC Pack aaaManage вычислительных узлов | Документы Microsoft"
description: "Дополнительные сведения о tooadd средства сценария PowerShell, удаление, запуск и остановка узлов вычислительного кластера HPC Pack 2012 R2 в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Управление числом hello и доступностью вычислительных узлов в кластере HPC Pack в Azure
При создании кластера HPC Pack 2012 R2 в виртуальных машинах Azure, может понадобиться способов tooeasily добавления, удаления, запускать (подготавливать) или некоторые остановку (отзыв) виртуальных машин вычислительных узлов в кластере. toodo эти задачи выполняются скрипты Azure PowerShell, которые установлены на ВМ головного узла hello. Эти скрипты помогают контролировать количество hello и доступности ресурсов кластера HPC Pack, благодаря чему можно контролировать затраты.

> [!IMPORTANT] 
> Эта статья относится tooHPC кластеры Pack 2012 R2 в Azure, созданные с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.
> Кроме того в HPC Pack 2016 hello сценариев PowerShell, описанных в этой статье недоступны.

## <a name="prerequisites"></a>Предварительные требования
* **Кластер HPC Pack 2012 R2 в виртуальных машинах Azure**: создать кластер HPC Pack 2012 R2 в hello классической модели развертывания. Например можно автоматизировать развертывание hello, используя образ hello HPC Pack 2012 R2 ВМ в Azure Marketplace hello и скрипт Azure PowerShell. Сведения и необходимые условия см. в разделе [создание кластера HPC с помощью скрипта развертывания IaaS пакета HPC hello](hpcpack-cluster-powershell-script.md).
  
    После развертывания, найти hello сценарии управления узла в hello % CCP\_ДОМАШНЯЯ папка bin % на головном узле hello. Запустите каждый из скриптов hello с правами администратора.
* **Параметры файла или управления сертификата публикации Azure**: требуется одно из следующих hello toodo на головном узле hello:
  
  * **Файл параметров публикации импорта hello Azure**. toodo, выполнения hello следующие командлеты Azure PowerShell на головном узле hello:
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * **Настройка сертификата управления Azure hello на головном узле hello**. Если у вас есть hello CER-файл, импортируйте его в хранилище сертификатов CurrentUser\My hello, а затем запустите hello, выполнив командлет Azure PowerShell для среды Azure (облачной или AzureChinaCloud):
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a>Добавление виртуальных машин вычислительных узлов
Добавление вычислительных узлов с hello **Add-HpcIaaSNode.ps1** сценария.

### <a name="syntax"></a>Синтаксис
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a>Параметры
* **ServiceName**: добавляются имя облачной службы hello, новых виртуальных машин вычислительных узлов.
* **ImageName**: имя образа виртуальной Машины Azure, который можно получить с помощью hello классический портал Azure или командлета Azure PowerShell **Get-AzureVMImage**. изображение Hello должно соответствовать hello следующие требования:
  
  1. Должна быть установлена операционная система Windows.
  2. Необходимо установить пакет HPC в роли вычислительного узла hello.
  3. Hello изображение должно быть частным образом в категории User hello, а не общедоступным образом ВМ Azure.
* **Количество**: количество вычислительных узлов виртуальных машин toobe добавлен.
* **InstanceSize**: hello размер ВМ вычислительных узлов.
* **DomainUserName**: имя пользователя домена, которое является toohello домена используется toojoin hello новые виртуальные машины.
* **DomainUserPassword**: пароль пользователя домена hello.
* **NodeNameSeries** (необязательно): шаблону именования для hello вычислительных узлов. необходимо использовать формат Hello &lt; *корневой\_имя*&gt;&lt;*запустить\_номер*&gt;%. Например MyCN % 10% означает ряд hello расчет имен узлов, начиная с MyCN11. Если не указан, hello скрипт использует hello настроен серия имен узла в кластере HPC hello.

### <a name="example"></a>Пример
Hello следующем примере добавляется 20 узлов большого размера виртуальных машин в облачной службе hello *hpcservice1*, основываясь на образ виртуальной Машины hello *ВМ hpccnimage1*.

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a>Удаление виртуальных машин вычислительных узлов
Удаление вычислительных узлов с hello **Remove-HpcIaaSNode.ps1** сценария.

### <a name="syntax"></a>Синтаксис
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a>Параметры
* **Имя**: удалить имена toobe узлов кластера. Поддерживаются подстановочные знаки. Имя набора параметров Hello — имя. Невозможно указать оба hello **имя** и **узел** параметров.
* **Узел**: объект HpcNode hello для hello узлы toobe удалены, который может быть получен с помощью командлета HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). Имя набора параметров Hello является узлом. Невозможно указать оба hello **имя** и **узел** параметров.
* **DeleteVHD** (необязательно): Установка toodelete hello связанные диски для hello виртуальных машин, которые будут удалены.
* **Force** (необязательно): Установка tooforce узлы HPC в автономный режим перед их удалением.
* **Подтвердите** (необязательно): запрашивать подтверждение перед выполнением команды hello.
* **WhatIf**: параметр toodescribe, что произойдет при выполнении команды hello без фактического выполнения команды hello.

### <a name="example"></a>Пример
Hello следующий пример принудительно устанавливает hello автономные узлы, имена которых начинаются *HPCNode-CN -* и их удаляет узлы hello и связанными дисками.

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a>Запуск виртуальных машин вычислительных узлов
Начало вычислительных узлов с hello **Start-HpcIaaSNode.ps1** сценария.

### <a name="syntax"></a>Синтаксис
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a>Параметры
* **Имя**: имена toobe узлы кластера hello работы. Поддерживаются подстановочные знаки. Имя набора параметров Hello — имя. Невозможно указать оба hello **имя** и **узел** параметров.
* **Узел**-объект HpcNode hello для hello узлы toobe работы, который может быть получен с помощью командлета HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). Имя набора параметров Hello является узлом. Невозможно указать оба hello **имя** и **узел** параметров.

### <a name="example"></a>Пример
Hello следующий пример запускает узлы, имена которых начинаются *HPCNode-CN -*.

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a>Остановка виртуальных машин вычислительных узлов
Остановить вычислительных узлов с hello **Stop-HpcIaaSNode.ps1** сценария.

### <a name="syntax"></a>Синтаксис
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a>Параметры
* **Имя**-имена toobe узлы кластера hello остановлена. Поддерживаются подстановочные знаки. Имя набора параметров Hello — имя. Невозможно указать оба hello **имя** и **узел** параметров.
* **Узел**: объект HpcNode hello для toobe узлов hello остановлена, который может быть получен с помощью командлета HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). Имя набора параметров Hello является узлом. Невозможно указать оба hello **имя** и **узел** параметров.
* **Force** (необязательно): Установка tooforce узлы HPC в автономный режим перед их остановкой.

### <a name="example"></a>Пример
Hello следующий пример принудительно устанавливает узлы, имена которых начинаются *HPCNode-CN -* и затем останавливается hello узлов.

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a>Дальнейшие действия
* tooautomatically увеличения или сжатия hello узлы кластера в соответствии с текущей рабочей нагрузкой заданий и задач в кластере hello hello см. в разделе [автоматически увеличиваться и уменьшаться hello ресурсы кластера HPC Pack в Azure соответствующим toohello рабочая нагрузка кластера](hpcpack-cluster-node-autogrowshrink.md).

