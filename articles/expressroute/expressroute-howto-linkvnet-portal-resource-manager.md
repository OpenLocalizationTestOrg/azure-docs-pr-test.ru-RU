---
title: "Связывание виртуальной сети tooan канал ExpressRoute: портал Azure | Документы Microsoft"
description: "Этот документ содержит общие сведения о том, как toolink виртуальных сетей (Vnet) tooExpressRoute цепи."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Подключение виртуальной сети tooan канал ExpressRoute
> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Интерфейс командной строки Azure](howto-linkvnet-cli.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-linkvnet-classic.md)
> 

Эта статья поможет вам связать каналы ExpressRoute tooAzure виртуальных сетей (Vnet) с помощью модели развертывания диспетчера ресурсов hello и hello портал Azure. Виртуальные сети могут быть в hello той же подписке, или они могут быть частью другую подписку.

## <a name="before-you-begin"></a>Перед началом работы
* Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.
* Вам потребуется активный канал ExpressRoute.
  
  * Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и иметь цепи hello, предоставляемой поставщиком соединения.
  * Убедитесь, что для вашего канала настроен частный пиринг Azure. В разделе hello [Настройка маршрутизации](expressroute-howto-routing-portal-resource-manager.md) маршрутизации инструкции.
  * Убедитесь, что настроен открытого пиринга Azure и hello пиринга BGP между вашей сетью и Майкрософт работает так, чтобы можно было включить подключение начала до конца.
  * Вам необходимо создать и полностью подготовить виртуальную сеть и шлюз виртуальной сети. Следуйте инструкциям hello слишком[создать шлюз виртуальной сети для ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Шлюз виртуальной сети для ExpressRoute использует hello «ExpressRoute», тип шлюза не VPN.

* Объедините too10 виртуальных сетей tooa стандартные каналом expressroute. Все виртуальные сети должны быть в hello геополитические совпадают при использовании стандартных канал ExpressRoute. 
* Связывание виртуальной сети за пределами области геополитические hello объекта hello канал ExpressRoute или подключения большее количество виртуальных сетей tooyour канал ExpressRoute, если вы включили hello ExpressRoute премиальное дополнение. Проверьте hello [часто задаваемые вопросы о](expressroute-faqs.md) Дополнительные сведения о премиальное дополнение hello.
* Вы можете [просмотреть видео](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) до начала toobetter понять hello действия.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Подключить виртуальную сеть в Привет одному каналу tooa подписки

### <a name="toocreate-a-connection"></a>toocreate соединение

> [!NOTE]
> Сведения о конфигурации BGP не будет отображаться при hello уровня 3 поставщик настроен на пиринги. Если ваш канал находится в состоянии, подготовленных, должен быть toocreate возможности подключения.
>

1. Убедитесь, что канал ExpressRoute и частный пиринг Azure настроены. Следуйте инструкциям в разделе hello [создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и [Настройка маршрутизации](expressroute-howto-routing-arm.md). Ваш канал ExpressRoute должна выглядеть hello после изображения:

    ![Снимок экрана канала ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. Теперь вы можете запустить подготовку toolink подключения вашей виртуальной сети шлюза tooyour канал ExpressRoute. Нажмите кнопку **подключения** > **добавить** tooopen hello **добавить подключение** колонке и затем настройте значения hello.

    ![Снимок экрана добавления подключения](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. После успешной настройки подключения к объект подключения будет показана информация hello hello подключения.

     ![Снимок экрана объекта подключения](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a>toodelete соединение
Подключение можно удалить, выбрав hello **удалить** значок колонке hello для соединения.

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Подключить виртуальную сеть в цепи tooa другой подписке
Канал ExpressRoute может совместно использоваться несколькими подписками. на следующем рисунке Hello показана простая схема способ управления доступом подходит для каналов ExpressRoute в нескольких подписках.

![Подключение между подписками](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- Каждый из hello маленькие облака в облако hello является используется toorepresent подписках, которые принадлежат toodifferent отделам в организации.
- Каждый из отделов hello hello организации можно использовать собственную подписку для развертывания своих служб, но они могут совместно использовать одной ExpressRoute цепи tooconnect tooyour назад в локальной сети.
- Одному отделу (в этом примере: ИТ) может быть владельцем hello канал ExpressRoute. Другие подписки в hello организации можно использовать канал ExpressRoute hello.

    > [!NOTE]
    > Плата за подключение и пропускную способность для hello выделенного канала будет применен toohello владельца канала ExpressRoute. Все виртуальные сети совместно использовать hello же пропускной способности.
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>Администрирование: владельцы канала и его пользователи

Hello «владелец схемы» зарегистрирован как авторизованный пользователь питания, для hello ресурсов цепь ExpressRoute. Владелец канала Hello можно создать авторизацию, может быть активирован с «канала пользователи». Пользователи канала являются владельцами виртуальной сети hello шлюзов, которые не находятся в одной подписке, как hello канал ExpressRoute. Пользователи канала могут активировать разрешения (по одному разрешению для каждой виртуальной сети).

Владелец канала Hello имеет авторизаций toomodify и revoke power hello в любое время. Отмена авторизации приведет все подключения ссылку, удаляемый из подписки hello, доступ к которым был отозван.

### <a name="circuit-owner-operations"></a>Действия владельца канала

**toocreate авторизации подключения**

Владелец канала Hello создает авторизации. Это приведет к создание hello ключ авторизации, которое может быть используемые схемы пользователя tooconnect их toohello шлюзы виртуальной сети канал ExpressRoute. Разрешение действительно только для одного подключения.

1. В колонке hello ExpressRoute выберите **авторизаций** , а затем введите **имя** для авторизации hello и нажмите кнопку **Сохранить**.

    ![Authorizations](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. После сохранения конфигурации hello скопируйте hello **идентификатор ресурса** и hello **ключ авторизации**.

    ![Ключ авторизации](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**toodelete авторизации подключения**

Подключение можно удалить, выбрав hello **удалить** значок колонке hello для соединения.

### <a name="circuit-user-operations"></a>Действия пользователя канала

Hello канала пользователю требуется идентификатор ресурса hello и ключ авторизации от владельца канала hello. 

**tooredeem авторизации подключения**

1.  Нажмите кнопку hello **+ создать** кнопки.

    ![Нажмите кнопку "Создать"](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  Поиск **«Соединения»** в hello Marketplace, выберите его и нажмите кнопку **создать**.

    ![Поиск подключений](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  Убедитесь, что hello **тип подключения** задано слишком «ExpressRoute».


4.  Введите сведения о hello, а затем нажмите кнопку **ОК** в колонке основы hello.

    ![Колонка «Основные»](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  В hello **параметры** колонки, выберите hello **шлюз виртуальной сети** и проверьте hello **активировать авторизации** флажок.

6.  Введите hello **ключ авторизации** и hello **однорангового узла схемы URI** и присвойте имя подключения hello. Нажмите кнопку **ОК**.

    ![Колонка "Настройки"](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. Просмотрите сведения о hello в hello **Сводка** колонку и нажмите кнопку **ОК**.


**toorelease авторизации подключения**

Авторизации можно освободить путем удаления соединений hello, связывающий hello цепь ExpressRoute toohello виртуальной сети.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).
