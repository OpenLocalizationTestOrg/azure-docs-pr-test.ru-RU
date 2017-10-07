---
title: "aaaUse Azure портала toodeploy ресурсы Azure | Документы Microsoft"
description: "Используйте портал Azure и управление ресурсов Azure toodeploy ресурсы."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Развертывание ресурсов с использованием шаблонов Resource Manager и портала Azure
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Интерфейс командной строки Azure](resource-group-template-deploy-cli.md)
> * [Портал](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

В этом разделе показано, как toouse hello [портал Azure](https://portal.azure.com) с [диспетчера ресурсов Azure](resource-group-overview.md) toodeploy ресурсами Azure. в разделе toolearn об управлении вашими ресурсами, [ресурсы с помощью портала управления Azure](resource-group-portal.md).

В настоящее время не каждая служба поддерживает hello портала или диспетчер ресурсов. Для этих служб требуется toouse hello [классический портал](https://manage.windowsazure.com). Состояние каждой службы hello см [диаграммы доступности Azure портала](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Создать группу ресурсов
1. Выберите toocreate группы пустой ресурсов **New** > **управления** > **группы ресурсов**.
   
    ![создание группы ресурсов](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Укажите имя группы, ее расположение и при необходимости выберите подписку. Tooprovide расположение группы ресурсов hello необходимо потому, что группа ресурсов hello хранит метаданные о ресурсах hello. В целях соответствия требованиям можно toospecify, где хранятся эти метаданные. Обычно мы рекомендуем указывать расположение, в котором будет храниться большинство ресурсов. С помощью hello же расположение можно упростить шаблон.
   
    ![настройка значений группы](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Развертывание ресурсов из Marketplace
После создания группы ресурсов, можно развернуть tooit ресурсы из hello Marketplace. Hello Marketplace предоставляет предопределенные решения для распространенных сценариев.

1. Выберите toostart развертывания, **New** и hello тип ресурса хотелось бы toodeploy. Затем найдите для конкретной версии ресурса hello hello хотелось бы toodeploy.
   
    ![развертывание ресурсов](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Если требуется toodeploy конкретного решения hello не отображается, можно искать hello Marketplace.
   
    ![поиск в Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. В зависимости от типа выбранного ресурса hello есть коллекция tooset соответствующие свойства перед развертыванием. Здесь эти свойства не показаны, так как они варьируются в зависимости от типа ресурса. Для всех типов необходимо выбрать целевую группу ресурсов. Hello следующем рисунке показано, как toocreate веб-приложение и развернуть ее toohello группы ресурсов, вы создали.
   
    ![Создать группу ресурсов](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    Кроме того можно решить toocreate группы ресурсов, при развертывании имеющихся ресурсов. Выберите **создать новый** и присвойте имя группы ресурсов hello.
   
    ![создание новой группы ресурсов](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Начнется развертывание. Hello развертывания может потребоваться несколько минут. После завершения развертывания hello, появится уведомление.
   
    ![просмотр уведомления](./media/resource-group-template-deploy-portal/view-notification.png)
5. После развертывания ресурсов, можно добавить дополнительные группы ресурсов toohello ресурсов с помощью hello **добавить** команду колонки группы ресурсов hello.
   
    ![Добавить ресурсы](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Развертывание ресурсов с помощью настраиваемого шаблона
Если требуется tooexecute развертывания, но использование шаблонов hello в hello Marketplace, можно создать настраиваемый шаблон, определяющий hello инфраструктуры для вашего решения. в разделе toolearn о создании шаблонов, [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).

1. Выберите настроенный шаблон через портал hello toodeploy **New**и начинается поиск **развертывания шаблона** пока можно выбрать его из вариантов hello.
   
    ![поиск развертывания шаблона](./media/resource-group-template-deploy-portal/search-template.png)
2. Выберите **развертывания шаблона** из доступных ресурсов hello.
   
    ![выберите "развертывание шаблона"](./media/resource-group-template-deploy-portal/select-template.png)
3. После запуска развертывания шаблона hello, откройте пустой шаблон hello, доступные для настройки.
   
    ![создание шаблона](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    В редакторе hello добавьте hello синтаксис JSON, который определяет ресурсы hello требуется toodeploy. По завершении нажмите кнопку **Сохранить**. Рекомендации по написанию синтаксис JSON hello. в разделе [Пошаговое руководство диспетчера ресурсов шаблона](resource-manager-template-walkthrough.md).
   
    ![изменение шаблона](./media/resource-group-template-deploy-portal/edit-template.png)
4. Или можно выбрать существующий шаблон из hello [шаблоны Azure краткое руководство](https://azure.microsoft.com/documentation/templates/). Эти шаблоны предоставляются hello сообщества. Они охватывают многих распространенных сценариев и кто-то добавить шаблон, аналогичные toowhat вы пытаетесь toodeploy. Toofind hello шаблоны можно найти что-нибудь, соответствующий вашему сценарию.
   
    ![выбор шаблона быстрого запуска](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    Выбранный шаблон hello можно просмотреть в редакторе hello.
5. После предоставления hello все другие значения, выберите **создать** toodeploy hello шаблона. 
   
    ![развертывание шаблона](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>Развертывание ресурсов на основе шаблона, сохранить tooyour учетной записи
портал Hello включает toosave шаблона tooyour учетная запись Azure и повторно развернуть позже. Дополнительные сведения о работе с шаблонами, сохраненных [приступить к работе с шаблонами закрытого на портал Azure hello](../marketplace-consumer/mytemplates-getstarted.md).

1. Выберите шаблонами сохраненного toofind **Обзор** > **шаблоны**.
   
    ![просмотр шаблонов](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Выберите из списка hello шаблонов сохранены tooyour учетной записи, с которой вы хотите toowork на hello.
   
    ![сохраненные шаблоны](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Выберите **развернуть** tooredeploy сохранен шаблон.
   
    ![развертывание сохраненного шаблона](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Дальнейшие действия
* см. журналы аудита tooview, [аудит операций с помощью диспетчера ресурсов](resource-group-audit.md).
* tootroubleshoot ошибок развертывания, в разделе [просмотреть операции развертывания](resource-manager-deployment-operations.md).
* tooretrieve шаблона из развертывания или группы ресурсов, в разделе [Экспорт шаблона диспетчера ресурсов Azure с существующие ресурсы](resource-manager-export-template.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

