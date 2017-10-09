---
title: "aaaUse Azure портала toomanage ресурсы Azure | Документы Microsoft"
description: "Используйте портал Azure и управление ресурсов Azure toomanage ресурсы. Показано, как toowork с ресурсами toomonitor панелей мониторинга."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a>Управление ресурсами Azure через портал
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Интерфейс командной строки Azure](xplat-cli-azure-resource-manager.md)
> * [Портал](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

В этом разделе показано, как toouse hello [портал Azure](https://portal.azure.com) с [диспетчера ресурсов Azure](resource-group-overview.md) toomanage ресурсами Azure. toolearn о развертывании ресурсы с помощью портала hello. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и портал Azure](resource-group-template-deploy-portal.md).

В настоящее время не каждая служба поддерживает hello портала или диспетчер ресурсов. Для этих служб требуется toouse hello [классический портал](https://manage.windowsazure.com). Состояние каждой службы hello см [диаграммы доступности Azure портала](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="manage-resource-groups"></a>Управление группами ресурсов

Группа ресурсов — это контейнер, содержащий связанные ресурсы для решения Azure. Hello группы ресурсов может содержать все hello ресурсы для решения hello и доступны только те ресурсы, которые должны toomanage как группа. Можно выбрать способ tooallocate ресурсы группы tooresource основаны на то, что hello больше смысла для вашей организации. Как правило, добавьте ресурсы, которые совместно используют hello же toohello жизненного цикла, сгруппировать того же ресурса, чтобы легко развертывать, обновлять и удалять их в группу. 

Группа ресурсов Hello хранит метаданные о ресурсах hello. Таким образом при указании расположения для группы ресурсов hello указывается, где хранятся эти метаданные. Для обеспечения соответствия, может потребоваться tooensure, ваши данные сохранены в определенном регионе.

1. Выберите все группы ресурсов hello в вашей подписке toosee **групп ресурсов**.
   
    ![просмотр групп ресурсов](./media/resource-group-portal/browse-groups.png)
2. Выберите toocreate группы пустой ресурсов **добавить**.
   
    ![добавление группы ресурсов](./media/resource-group-portal/add-resource-group.png)
3. Укажите имя и расположение для новой группы ресурсов hello. Нажмите кнопку **Создать**.
   
    ![Создать группу ресурсов](./media/resource-group-portal/create-empty-group.png)
4. Может потребоваться tooselect **обновление** группы ресурсов toosee hello создан недавно.
   
    ![обновление группы ресурсов](./media/resource-group-portal/refresh-resource-groups.png)
5. Выберите toocustomize hello данные, отображаемые для вашей группы ресурсов **столбцы**.
   
    ![настройка столбцов](./media/resource-group-portal/select-columns.png)
6. Выберите столбцы tooadd hello, а затем выберите **обновление**.
   
    ![добавление столбцов](./media/resource-group-portal/add-columns.png)
7. toolearn о развертывании ресурсов tooyour новую группу ресурсов, в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и портал Azure](resource-group-template-deploy-portal.md).
8. Для группы ресурсов tooa быстрого доступа можно закрепить панель tooyour колонке hello.
   
    ![закрепление группы ресурсов](./media/resource-group-portal/pin-group.png)
9. панель мониторинга Hello отображает hello группы ресурсов и его ресурсам. Можно выбрать hello группы ресурсов или любой из его элемент toohello toonavigate ресурсов.
   
    ![закрепление группы ресурсов](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a>Добавление тегов к ресурсам
Можно применить теги tooresource групп и toologically ресурсы организации активов. Сведения о работе с тегами см. в разделе [использование теги tooorganize ресурсам Azure](resource-group-using-tags.md).

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a>Мониторинг ресурсов
При выборе ресурса колонки ресурсов hello предоставляет по умолчанию диаграмм и таблиц для отслеживания типа ресурса.

1. Выберите ресурс и уведомление hello **мониторинг** раздела. Он включает диаграммы, соответствующие toohello типа ресурса. Hello рисунке показаны наблюдение за данными для учетной записи хранения по умолчанию hello.
   
    ![показать мониторинг](./media/resource-group-portal/show-monitoring.png)
2. Вы можете закрепить раздел hello колонке tooyour мониторинга, выбрав hello многоточие (...) над разделом hello. Можно также настроить раздел hello размер hello в колонке hello или полностью удалить. Hello следующем рисунке показано, как toopin, настроить или удалить hello ЦП и памяти раздела.
   
    ![закрепление раздела](./media/resource-group-portal/pin-cpu-section.png)
3. После закрепления панели мониторинга toohello раздел hello, вы увидите hello сводки на панели мониторинга hello. И выбрав его сразу же осуществляется toomore подробные сведения о данных hello.
   
    ![просмотр панели мониторинга](./media/resource-group-portal/view-startboard.png)
4. toocompletely настроить hello данные мониторинга через портал hello, перейдите на панель мониторинга по умолчанию tooyour и выберите **новая панель мониторинга**.
   
    !["Веб-транзакции"](./media/resource-group-portal/dashboard.png)
5. Присвойте имя новой информационной панели и перетащите плитки на панели мониторинга hello. Плитка приветствия фильтруются по различные параметры.
   
    !["Веб-транзакции"](./media/resource-group-portal/create-dashboard.png)
   
     в разделе toolearn о работе с панелями мониторинга, [Создание и совместное использование панели мониторинга на портал Azure hello](../azure-portal/azure-portal-dashboards.md).

## <a name="manage-resources"></a>Управление ресурсами
В колонке hello для ресурса вы видите hello параметры для управления hello ресурсов. портал Hello показывает возможности управления для этого определенного типа ресурсов. Команды управления hello разделе hello верхней части колонки ресурсов hello и левой стороны hello.

![Управление ресурсами](./media/resource-group-portal/manage-resources.png)

Из этих параметров можно выполнять операции, такие как запуск и остановка виртуальной машины или повторной настройки свойств hello hello виртуальной машины.

## <a name="move-resources"></a>Перемещение ресурсов
Группы ресурсов tooanother ресурсов toomove или другая подписка, в статье [переместить группу ресурсов toonew ресурсов или подписку](resource-group-move-resources.md).

## <a name="lock-resources"></a>Блокировка ресурсов
Можно заблокировать подписки, группы ресурсов или ресурсов tooprevent другим пользователям в организации от случайного удаления или изменения критическим ресурсам. Дополнительные сведения см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](resource-group-lock-resources.md).

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a>Просмотр сведений о подписке и затратах
Можно просмотреть сведения о подписке и hello сведенные затраты для всех ресурсов. Выберите **подписки** и вы хотите toosee подписки hello. Может иметь только один tooselect подписки.

![Подписка](./media/resource-group-portal/select-subscription.png)

В колонке подписки hello видеть скорость темпа работ.

![график расходов](./media/resource-group-portal/burn-rate.png)

а также разбивка расходов по типам ресурсов.

![стоимость ресурсов](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a>Экспорт шаблона
После настройки группы ресурсов, вы можете шаблона диспетчера ресурсов hello tooview для группы ресурсов hello. Экспорт шаблона hello имеет два преимущества:

1. Можно легко автоматизировать будущих развертываний hello решения, так как шаблон hello содержит все всей инфраструктурой hello.
2. Ознакомьтесь с синтаксисом шаблона, просмотрев hello JavaScript Object Notation (JSON), представляющий решения.

Пошаговое руководство см. в статье [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md) (Экспорт шаблона Azure Resource Manager из существующих ресурсов).

## <a name="delete-resource-group-or-resources"></a>Удаление ресурсов или группы ресурсов
При удалении группы ресурсов удаляет все hello ресурсы, содержащиеся в нем. Из группы ресурсов можно также удалить отдельные ресурсы. Требуется tooexercise осторожны при удалении группы ресурсов, из-за возможной ресурсы в других групп ресурсов, связанных tooit. Диспетчер ресурсов не приводит к удалению связанных ресурсов, но они могут не работать должным образом без hello ожидается ресурсов.

![удаление группы](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a>Дальнейшие действия
* см. журналы действий tooview, [аудит операций с помощью диспетчера ресурсов](resource-group-audit.md).
* tooview сведения о состоянии развертывания см. [просмотреть операции развертывания](resource-manager-deployment-operations.md).
* ресурсы toodeploy через портал hello см [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и портал Azure](resource-group-template-deploy-portal.md).
* tooresources toomanage доступ, в разделе [использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](../active-directory/role-based-access-control-configure.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

