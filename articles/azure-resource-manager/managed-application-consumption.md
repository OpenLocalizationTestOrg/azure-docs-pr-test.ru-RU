---
title: "приложения с управляемым aaaConsume Azure | Документы Microsoft"
description: "В этой статье описывается, как создавать управляемое приложение Azure с помощью опубликованных файлов."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>Использование внутреннего управляемого приложения

Можно использовать [управляемые приложения](managed-application-overview.md) Azure, предназначенные для членов вашей организации. Например, можно выбрать управляемые приложения отдела ИТ, которые обеспечивают соответствие стандартам организации. Эти управляемые приложения доступны через hello каталога услуг, hello Azure Marketplace.

Прежде чем продолжить эту статью, необходимо иметь управляемого приложения, доступные в каталог услуг hello для вашей подписки. Если кто-либо в вашей организации еще не создал управляемое приложение, ознакомьтесь с разделом [Создание и публикация управляемого приложения Azure](managed-application-publishing.md).

В настоящее время можно использовать Azure CLI или hello Azure портала tooconsume управляемого приложения.

## <a name="create-hello-managed-application-by-using-hello-portal"></a>Создание приложения hello управляемых с помощью портала hello

toodeploy управляемого приложения через портал hello, выполните следующие действия.

1. Go toohello портал Azure. Найдите **управляемое приложение из каталога услуг**.

   ![Управляемое приложение каталога услуг](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. Выберите hello управляемого приложения, нужно toocreate из списка доступных решений hello. Нажмите кнопку **Создать**.

   ![Выбор управляемого приложения](./media/managed-application-consumption/select-offer.png)

1. Укажите значения для параметра hello, которые требуется tooprovision hello ресурсы. Выберите расположение **Западно-центральная часть США**. Нажмите кнопку **ОК**.

   ![Параметры управляемого приложения](./media/managed-application-consumption/input-parameters.png)

1. шаблон Hello проверяет заданных значений hello. Если проверка прошла успешно, выберите **ОК** toostart hello развертывания.

   ![Проверка управляемого приложения](./media/managed-application-consumption/validation.png)

После завершения развертывания hello в группе hello управляемых ресурсов, предоставленные подготавливаются hello соответствующие ресурсы, определенные в шаблоне hello.

## <a name="create-hello-managed-application-by-using-azure-cli"></a>Создание приложения hello управляемых с помощью Azure CLI

Существует два способа toocreate управляемого приложения с помощью Azure CLI.

* Команда hello для создания управляемых приложений.
* Команда hello обычным шаблоном развертывания.

### <a name="use-hello-template-deployment-command"></a>Команда hello шаблон развертывания

Развертывание файла applianceMainTemplate.json hello, hello поставщик создан.

Создайте две группы ресурсов: Hello первая группа ресурсов находится где hello ресурсов управляемого приложения создается: Microsoft.Solutions/appliances. Hello вторая группа ресурсов содержит все ресурсы hello, определенные в mainTemplate.json. Эта группа ресурсов находится под управлением hello независимого поставщика программных Продуктов.

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> Используйте `westcentralus` как hello расположение группы ресурсов hello.
>

applianceMainTemplate.json toodeploy в mainResourceGroup hello используйте следующую команду:

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

После hello предыдущих запусков шаблона он запрашивает hello значения параметров "hello", определенные в шаблоне hello. В дополнение к этому toohello параметры, которые требуется tooprovision ресурсы в шаблоне, требуется два значения параметра ключа:

- **managedResourceGroupId**: hello идентификатор hello ресурсов группы содержащего hello ресурсы, определенные в applianceMainTemplate.json. Идентификатор Hello имеет вид hello `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`. В предыдущих пример hello, его идентификатор базы данных hello объекта `managedResourceGroup`.
- **applianceDefinitionId**: hello идентификатор hello управляемых определение ресурсов приложения. Это значение предоставляется hello независимого поставщика программных Продуктов.

> [!NOTE]
> Hello издателя необходимо предоставить доступ toohello ресурсов группы, содержащей определение приложения hello управляемых. Определение ресурсов Hello создается в hello издателя подписки. Таким образом пользователя, группы пользователей или приложения в клиенте hello должен ресурсов toothis доступ для чтения.

После успешного завершения развертывания hello вы видите hello управляемого приложения создается в mainResourceGroup. Hello storageAccount ресурс создается в managedResourceGroup.

### <a name="use-hello-create-command"></a>Hello используется команда «Создать»

Можно использовать hello `az managedapp create` команда toocreate управляемое приложение из hello управляемое определение приложения.

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **Идентификатор для определения устройства**: идентификатор ресурса hello hello управляемые определения приложения, созданные в предыдущих шага hello. tooobtain этот идентификатор запуска hello следующую команду:

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  Эта команда возвращает определение hello управляемого приложения. Необходимо получить значение hello hello идентификатор свойства.

* **управляемые rg-id**: hello имя hello ресурсов группы содержащего hello ресурсы, определенные в applianceMainTemplate.json. Эта группа ресурсов находится группа hello управляемых ресурсов. Он управляет hello издателя. Если эта группа не существует, она создается автоматически.
* **Группа ресурсов**: hello группа ресурсов, где hello управляемого ресурса приложения создается. Hello ресурсов Microsoft.Solutions/appliance живет в этой группе ресурсов.
* **Параметры**: hello параметры, необходимые для hello ресурсы, определенные в applianceMainTemplate.json.

## <a name="known-issues"></a>Известные проблемы

Эта предварительная версия включает hello следующих ситуаций:

* 500 Внутренняя ошибка сервера отображается во время создания hello hello управляемого приложения. При возникновении этой проблемы, это скорее всего toobe временными. Повторите операцию hello.
* Для группы управляемых ресурсов hello требуется новую группу ресурсов. Если используется существующая группа ресурсов, происходит сбой развертывания hello.
* Hello группы ресурсов, содержащей hello Microsoft.Solutions/appliances ресурсов должны быть созданы в hello **westcentralus** расположение.

## <a name="next-steps"></a>Дальнейшие действия

* Введение toomanaged приложений, в разделе [Обзор управляемого приложения](managed-application-overview.md).
* Сведения о публикации управляемых приложений в каталоге услуг см. в разделе [Создание и публикация управляемого приложения Azure](managed-application-publishing.md).
* Сведения о публикации toohello управляемые приложения Azure Marketplace см. в разделе [Azure управляемого приложения в hello Marketplace](managed-application-author-marketplace.md).
* Сведения о использование управляемого приложения из hello Marketplace в разделе [использовать Azure управляемого приложения в hello Marketplace](managed-application-consume-marketplace.md).
