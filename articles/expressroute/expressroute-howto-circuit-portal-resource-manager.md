---
title: "Создание и изменение канала ExpressRoute с помощью портала Azure | Документация Майкрософт"
description: "В этой статье описывается, как toocreate, подготовки, проверьте, обновление, удаление и отзыв канал ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a>Создание и изменение канала ExpressRoute
> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Интерфейс командной строки Azure](howto-circuit-cli.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-circuit-classic.md)
>

В этой статье описывается, как toocreate канал Azure ExpressRoute с помощью hello Azure hello и портал Azure модели развертывания диспетчера ресурсов. Hello следующие шаги также показано, как toocheck hello состояние канала hello, обновления или удаления и сделать.


## <a name="before-you-begin"></a>Перед началом работы
* Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.
* Убедитесь, что доступ toohello [портал Azure](https://portal.azure.com).
* Убедитесь, что имеются разрешения toocreate новых сетевых ресурсов. Обратитесь к администратору учетной записи, если нет соответствующих разрешений hello.
* Вы можете [просмотреть видео](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) перед началом в порядке toobetter понять hello действия.

## <a name="create-and-provision-an-expressroute-circuit"></a>Создание и предоставление канала ExpressRoute
### <a name="1-sign-in-toohello-azure-portal"></a>1. Войдите в toohello портал Azure
В браузере перейдите toohello [портал Azure](http://portal.azure.com) и выполните вход с учетной записью Azure.

### <a name="2-create-a-new-expressroute-circuit"></a>2. Создание канала ExpressRoute
> [!IMPORTANT]
> Ваш канал ExpressRoute будет записана с момента hello выдачи ключа службы. Убедитесь, что эта операция при готовности tooprovision hello цепи hello поставщика услуг подключения.
> 
> 

1. Можно создать канал ExpressRoute, выбрав параметр toocreate hello новый ресурс. Нажмите кнопку **New** > **сети** > **ExpressRoute**, как показано в hello после изображения:
   
    ![Создание канала ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. После нажатия кнопки **ExpressRoute**, вы увидите hello **канал ExpressRoute создания** колонку. Если вы заполнение значений hello в этой колонке, убедитесь, что указан правильный уровень номера SKU hello и измерение данных.
   
   * **Уровень** определяет, какого уровня надстройка включена — ExpressRoute "Стандартный" или ExpressRoute "Премиум". Можно указать **Стандартная** tooget hello стандартном номере SKU или **Premium** hello premium надстройки.
   * **Измерение данных** определяет hello выставления счетов с типом. Выберите **С учетом трафика** для тарифного плана с оплатой за трафик или **Не ограничено** для безлимитного тарифного плана. Обратите внимание, что можно изменить hello выставления счетов с типом из **Metered** слишком**неограниченное количество**, но не может изменить тип hello из **неограниченное количество** слишком**Metered**.
     
     ![Настройте уровень номера SKU hello и измерение данных](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> Имейте в виду, что расположение Пиринга hello указывает hello [физическое расположение](expressroute-locations.md) где вы пиринг с корпорацией Майкрософт. Это **не** слишком связанные свойства «Местоположение», которое ссылается toohello geography, где находится hello поставщика сетевых ресурсов Azure. Они не связаны, но это хорошей практикой toochoose расположение Пиринга канала hello территориально закрыть toohello поставщика сетевых ресурсов. 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3. Представление hello цепи и свойства
**Просмотреть все каналы hello**

Можно просмотреть все каналы hello, созданной при выборе **все ресурсы** hello меню слева.

![Просмотр каналов](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**Просмотр свойств hello**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Свойства](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4. Отправка ключа tooyour подключения hello службы поставщика для подготовки
В этой колонке **состояние поставщика** предоставляет сведения о hello текущее состояние подготовки на стороне поставщика услуг hello. **Circuit состояние** предоставляет hello состояния на стороне Microsoft hello. Дополнительные сведения о состояния подготовки схемы см. в разделе hello [рабочих процессов](expressroute-workflows.md#expressroute-circuit-provisioning-states) статьи.

При создании нового канала ExpressRoute hello схемы будут иметь hello следующие состояния:

Состояние поставщика: Не подготовлено<BR>
Состояние канала: Включен

![Инициация процесса подготовки](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

цепь Hello приведет к изменению toohello при поставщика услуг подключения hello находится в процессе hello включить его для вас следующие состояния:

Состояние поставщика: Идет подготовка<BR>
Состояние канала: Включен

Для вас toobe может toouse канал ExpressRoute он должен быть в hello следующие состояния:

Состояние поставщика: Подготовлено<BR>
Состояние канала: Включен

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5. Периодически Проверьте состояние hello и состояние hello ключа канала hello
Можно просмотреть свойства hello hello канала, который вы хотите, выбрав его. Проверьте hello **состояние поставщика** и убедитесь, что его следует переместить слишком**инициализировано** перед продолжением.

![Состояние канала и поставщика](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6. Создание конфигурации маршрутизации
Пошаговые инструкции см. в разделе toohello [expressroute в конфигурацию маршрутизации](expressroute-howto-routing-portal-resource-manager.md) статью toocreate и изменения пиринги в цепи.

> [!IMPORTANT]
> Эти инструкции применяются только toocircuits, созданных с помощью службы поставщиков, предлагающих услуги подключений второго уровня. Если вы работаете с поставщиком, предлагающим услуги третьего уровня (обычно это IPVPN, например MPLS), то ваш поставщик услуг подключения выполнит настройку и управление конфигурацией самостоятельно.
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7. Связывание виртуальной сети tooan канал ExpressRoute
Затем свяжите виртуальной сети tooyour канал ExpressRoute. Используйте hello [связывание виртуальной сети цепи tooExpressRoute](expressroute-howto-linkvnet-arm.md) статьи при работе с моделью развертывания диспетчера ресурсов hello.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Получение состояния hello канал ExpressRoute
Hello состояние канала можно просмотреть, выбрав его. 

![Состояние канала ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>Изменение канала ExpressRoute
Некоторые свойства канала ExpressRoute можно изменить, не повлияв на подключение.

Можно сделать hello без простоев следующие:

* включать и отключать надстройку ExpressRoute "Премиум" для канала ExpressRoute;
* Увеличение hello пропускной способностью вашего канала ExpressRoute при условии, что доступно емкости на порту hello. Обратите внимание, что понижение уровня полосы пропускания канала hello не поддерживается. 
* Изменение плана на основе данных, измеряемые tooUnlimited данных отслеживания использования hello. Обратите внимание, изменяющихся план контроля использования программных продуктов hello из данных tooMetered данных не поддерживается.
* Параметр *Allow Classic Operations*(Разрешить классические операции) можно включать и отключать.

Дополнительные сведения об ограничениях и ограничениях см. в разделе toohello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).

Щелкните hello toomodify канал ExpressRoute **конфигурации** как показано на следующем рисунке hello.

![Изменение канала](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

Можно изменить hello пропускной способности, SKU модели выставления счетов и разрешить классический операции в колонке конфигурации hello.

> [!IMPORTANT]
> Канал ExpressRoute toorecreate hello возможно, если имеется существующий порт hello недостаточной мощности. Обновление схемы hello невозможно, если доступна без дополнительной емкости в этом расположении.
>
> Нельзя уменьшить hello пропускной способности канала ExpressRoute без прерывания. Понижение уровня полосы пропускания необходимо канал ExpressRoute toodeprovision hello и повторной инициализации новый канал ExpressRoute.
> 
> Отключить надстройку premium операция может завершиться неудачно, если вы используете ресурсы, которые больше, чем то, что разрешено для стандартной схемы hello.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Отзыв и удаление канала ExpressRoute
Ваш канал ExpressRoute можно удалить, выбрав hello **удалить** значок. Обратите внимание hello следующие:

* Необходимо удалить связь всех виртуальных сетей с каналом expressroute hello. Если операция завершается неудачно, проверьте, связаны ли виртуальную сеть toohello канала.
* Если состояние подготовки службы поставщика hello ExpressRoute канала **Provisioning** или **инициализировано** необходимо работать с ваш канал hello toodeprovision поставщика службы с их стороны. Она будет продолжать tooreserve ресурсы и выставлять вам счет на поставщика услуг hello завершения списания цепи hello и уведомляет нас.
* Если поставщик услуг hello отозваны hello канала (состояние подготовки поставщика услуг hello задано слишком**не инициализировано**) можно удалить цепь hello. Это приведет к остановке выставления счетов для схемы hello

## <a name="next-steps"></a>Дальнейшие действия
После создания ваш канал, убедитесь, что hello следующие:

* [Создание и изменение маршрутизации для канала ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
* [Связать вашей виртуальной сети tooyour канал ExpressRoute](expressroute-howto-linkvnet-arm.md)

