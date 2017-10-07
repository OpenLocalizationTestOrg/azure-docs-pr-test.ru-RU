---
title: "aaaCreate контейнер облачной службы с помощью PowerShell | Документы Microsoft"
description: "В этой статье объясняется, как toocreate облачной службы контейнера с помощью PowerShell. контейнер Hello находится рабочих и веб-ролей."
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a>Использование Azure PowerShell команды toocreate контейнер пустой облачной службы
В этой статье объясняется, как tooquickly создать контейнер облачные службы с помощью командлетов Azure PowerShell. Выполните следующие действия hello:

1. Установка командлетов Microsoft Azure PowerShell hello из hello [Azure PowerShell загружает](http://aka.ms/webpi-azps) страницы.
2. Откройте командную строку PowerShell hello.
3. Используйте hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign в.

   > [!NOTE]
   > Дополнительные инструкции по установке командлет Azure PowerShell hello и подключении tooyour подписки Azure см. в разделе слишком[как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
   >
   >
4. Используйте hello **New-AzureService** toocreate командлет контейнер пустой Azure облачной службы.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. Выполните этот командлет пример tooinvoke hello.

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

Дополнительные сведения о создании hello облачной службы Azure выполните следующую команду:

```
Get-help New-AzureService
```

### <a name="next-steps"></a>Дальнейшие действия
* toomanage hello развертывание облачной службы см. в toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), и [AzureService набора](https://msdn.microsoft.com/library/azure/dn495242.aspx) команды. Можно также указать слишком[как tooconfigure облачные службы](cloud-services-how-to-configure.md) для получения дополнительных сведений.
* toopublish облачной службы проекта tooAzure см. в toohello **PublishCloudService.ps1** образец кода из [непрерывная доставка для облачной службы в Azure](cloud-services-dotnet-continuous-delivery.md).
