---
title: "aaaDelete Azure кластера и его ресурсам | Документы Microsoft"
description: "Сведения об использовании delete toocompletely структуры службы кластера либо удаление группы ресурсов hello, содержащий hello кластера или путем выборочного удаления ресурсов."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a>Удаление кластера Service Fabric на Azure и hello ресурсы, используемые в нем
Кластера Service Fabric состоит из многих других ресурсов Azure в дополнение к этому toohello сам ресурс кластера. Поэтому toocompletely Удаление кластера Service Fabric требуется также toodelete Здравствуйте, все ресурсы, которые оно состоит из.
У вас есть два варианта: либо удаление hello группы ресурсов, hello кластера находится в (которая удаляет hello кластерных ресурсов и другие ресурсы в группе ресурсов hello) или специально удалить ресурс кластера hello и связанные с ним ресурсы (но не другие ресурсы в группе ресурсов hello).

> [!NOTE]
> Удаление ресурса кластера hello **не** удаления всех hello другие ресурсы, которые состоят из кластера Service Fabric.
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a>Удалите hello весь ресурс (группа Ресурсов), hello кластера Service Fabric
Это простой способ tooensure hello удалить все ресурсы hello, связанной с кластером, включая группу ресурсов hello. Можно удалить группу ресурсов hello, с помощью PowerShell или с помощью портала Azure hello. Если группы ресурсов содержит ресурсы, которые не являются связанные tooService структуры кластера, можно удалить отдельные ресурсы.

### <a name="delete-hello-resource-group-using-azure-powershell"></a>Удаление группы ресурсов hello, с помощью Azure PowerShell
Можно также удалить группу ресурсов hello, выполнив следующие командлеты Azure PowerShell hello. Убедитесь, что на компьютере установлена среда Azure PowerShell 1.0 или более поздней версии. Если вы не выполнили это перед, выполните hello действия, описанные в [как tooinstall и настройка Azure PowerShell.](/powershell/azure/overview)

Откройте окно PowerShell и выполните следующие командлеты PS hello:

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

Удаление hello prompt tooconfirm будет работать, если вы не использовали hello *-Force* параметр. На подтверждение hello RG и все ресурсы hello, содержащиеся в нем удаляются.

### <a name="delete-a-resource-group-in-hello-azure-portal"></a>Удаление группы ресурсов в hello портал Azure
1. Имя входа toohello [портал Azure](https://portal.azure.com).
2. Переход кластера Service Fabric toohello требуется toodelete.
3. Щелкните имя группы ресурсов на странице essentials кластера hello hello.
4. Откроется окно hello **Essentials группы ресурсов** страницы.
5. Нажмите кнопку **Delete**(Удалить).
6. Следуйте инструкциям hello на этой странице toocomplete hello удаления группы ресурсов hello.

![Удаление группы ресурсов][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a>Удалить ресурс кластера hello и hello ресурсы, используемые в нем, но не другие ресурсы в группе ресурсов hello
Если группы ресурсов содержит только ресурсы, связанные toohello кластера Service Fabric требуется toodelete, а затем проще toodelete hello весь ресурс группа. Если вы собираетесь tooselectively delete hello ресурсы по одному в группе ресурсов, выполните следующие действия.

При развертывании кластера с помощью портала hello, или с помощью одного из шаблонов диспетчера ресурсов структуры службы hello из галереи шаблонов hello ресурсами hello, hello кластера использует помечены hello, следующие два теги. Их можно использовать, какие ресурсы должны toodecide toodelete.

***Тег #1:*** ключ = clusterName, значение = «имя кластера hello»

***Тег 2:*** ключ = resourceName, значение = ServiceFabric.

### <a name="delete-specific-resources-in-hello-azure-portal"></a>Удаление конкретных ресурсов hello портал Azure
1. Имя входа toohello [портал Azure](https://portal.azure.com).
2. Переход кластера Service Fabric toohello требуется toodelete.
3. Go слишком**все параметры** колонке essentials hello.
4. Щелкните **теги** под **управление ресурсами** в колонке параметров hello.
5. Выберите одну из hello **теги** в tooget колонки теги hello список всех ресурсов hello с этим тегом.
   
    ![Теги ресурсов][ResourceTags]
6. Получив hello перечень ресурсов, заключенное в теги, щелкните на каждом из ресурсов hello и удалите их.
   
    ![Ресурсы с тегами][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a>Удаление hello ресурсов с помощью Azure PowerShell
Hello ресурсы по одному можно удалить, выполнив следующие командлеты Azure PowerShell hello. Убедитесь, что на компьютере установлена среда Azure PowerShell 1.0 или более поздней версии. Если вы не выполнили это перед, выполните hello действия, описанные в [как tooinstall и настройка Azure PowerShell.](/powershell/azure/overview)

Откройте окно PowerShell и выполните следующие командлеты PS hello:

```powershell
Login-AzureRmAccount
```
Для каждого ресурса hello нужны toodelete, hello следующей:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

toodelete hello ресурса кластера, запустите следующие hello:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a>Дальнейшие действия
После tooalso hello чтения сведения о обновлением кластера и секционирование службы:

* [Узнайте об обновлениях кластера.](service-fabric-cluster-upgrade.md)
* [Узнайте о секционировании служб с отслеживанием для максимального масштабирования.](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
