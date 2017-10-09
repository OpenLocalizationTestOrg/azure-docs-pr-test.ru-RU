---
title: "aaaDownload hello шаблона виртуальной машины Azure | Документы Microsoft"
description: "Загрузите hello процессадля toohelp виртуальной Машины с помощью автоматизации развертываний в модели развертывания диспетчера ресурсов hello"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a>Загрузите шаблон hello для виртуальной Машины
При создании виртуальной Машины в Azure с помощью портала hello или PowerShell диспетчера ресурсов шаблона создается автоматически для вас. Можно использовать этот шаблон tooquickly дубликат развертывания. шаблон Hello содержит сведения обо всех hello ресурсов в группе ресурсов. Для виртуальной машины это означает, что шаблон hello содержит все элементы, созданные для поддержки hello виртуальной Машины в этой группе ресурсов, включая hello сетевых ресурсов.

## <a name="download-hello-template-using-hello-portal"></a>Загрузите шаблон hello, с помощью портала hello
1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Один hello концентратора последовательно выберите пункты **виртуальные машины**.
3. Выберите виртуальную машину hello из списка hello.
4. Выберите элемент **Сценарий автоматизации**.
5. Выберите **загрузки** и сохранить на локальном компьютере файл .zip tooyour hello.
6. Откройте hello ZIP-файл и извлеките папки tooa файлов hello. Hello ZIP-файл будет содержать:
   
   * deploy.ps1;
   * deploy.sh; 
   * deployer.rb;
   * DeploymentHelper.cs;
   * parameters.json;
   * template.json.

файл template.json Hello — шаблон hello.

## <a name="download-hello-template-using-powershell"></a>Загрузите шаблон hello, с помощью PowerShell
Можно также загрузить файл шаблона .json hello, с помощью hello [AzureRMResourceGroup экспорта](https://msdn.microsoft.com/library/mt715427.aspx) командлета. Можно использовать hello `-path` параметр tooprovide hello, имя файла и путь для hello JSON-файл. В этом примере показано, как с именем шаблона hello toodownload для группы ресурсов hello **myResourceGroup** toohello **C:\users\public\downloads** папку на локальном компьютере.

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о развертывании ресурсов с помощью шаблонов, в разделе [Пошаговое руководство диспетчера ресурсов шаблона](../../azure-resource-manager/resource-manager-template-walkthrough.md).

