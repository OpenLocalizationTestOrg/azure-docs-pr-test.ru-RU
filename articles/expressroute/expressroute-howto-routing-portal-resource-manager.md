---
title: "Как tooconfigure маршрутизации (пиринг) для канала ExpressRoute: диспетчера ресурсов: Azure | Документы Microsoft"
description: "В этой статье содержится описание этапов hello для создания и подготовки hello private, public и Microsoft пиринг канал ExpressRoute. В этой статье также рассказывается, как состояние toocheck hello, обновления или удаления пиринги для своего канала."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a>Создание и изменение пиринга для канала ExpressRoute

Эта статья поможет вам создавать и управлять ими конфигурации маршрутизации для канала ExpressRoute в hello портал Azure с помощью модели развертывания диспетчера ресурсов hello. Можно также проверить состояние hello, update или delete и отзыв пиринги за канал ExpressRoute. Если вы хотите toouse toowork другой метод с ваш канал, выберите статью из hello после списка:


## <a name="configuration-prerequisites"></a>Предварительные требования для настройки

* Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md) страницы hello [требования к маршрутизации](expressroute-routing.md) страницы и hello [рабочих процессов](expressroute-workflows.md) страницы перед началом настройки.
* Вам потребуется активный канал ExpressRoute. Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить. Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен для вас toobe может toorun hello командлеты в следующих разделах hello.
* Если планируется toouse общего ключа/MD5-хэш быть toouse убедиться, что это на обеих сторонах hello туннеля и ограничение hello число символов tooa максимум 25.

Эти инструкции применяются только toocircuits, созданных с помощью предложения службы связи уровня 2 поставщиков услуг. Если ваш поставщик услуг подключения предлагает услуги третьего уровня (обычно это IPVPN, например MPLS), он выполнит настройку маршрутизации и управление ею. 

> [!IMPORTANT]
> Мы сейчас не объявляет пиринги настроен поставщиками услуг через портал управления службами hello. Такая возможность будет предоставлена позже. Перед настройкой пирингов BGP уточните информацию у поставщика услуг.
> 
> 

Для каждого канала ExpressRoute можно настроить один, два или три пиринга (частный пиринг Azure, общедоступный пиринг Azure и пиринг Microsoft). Пиринги можно настраивать в любом порядке, Тем не менее необходимо выполнить настройку hello из каждого из них пиринга одновременно.

## <a name="azure-private-peering"></a>Частный пиринг Azure

Этот раздел поможет вам создать, получить, обновление и удаление hello Azure закрытая конфигурация пиринга канал ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate открытого пиринга Azure

1. Настройте канал ExpressRoute hello. Убедитесь, что цепь hello полностью подготовлена с поставщиком услуг подключения hello перед продолжением.

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Настройка открытого пиринга Azure для hello схемы. Убедитесь, что hello следующих элементов, прежде чем продолжить hello следующие шаги:

  * / 30 подсеть для основной ссылки hello. подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.
  * / 30 подсеть для дополнительной ссылки hello. подсеть Hello не должна быть частью любого адресного пространства, зарезервированного для виртуальных сетей.
  * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
  * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS. Для этого пиринга можно использовать частный номер AS. Не используйте номер 65515.
  * **Необязательно —** хэш MD5 при выборе toouse один.
3. Выберите hello Azure закрытого пиринга строки, как показано в следующий пример hello:

  ![Частный пиринг](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. Настройте частный пиринг. Следующие изображения Hello показан пример конфигурации:

  ![Настройка частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. Сохранение конфигурации hello, после того как заданы все параметры. После успешного принятия конфигурации hello, вы видите что-нибудь подобное toohello следующий пример:

  ![Сохранение частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a>tooview Azure закрытого пиринга подробные сведения

Можно просмотреть свойства hello открытого пиринга Azure, выбрав пиринг hello.

![Просмотр частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate конфигурации закрытого пиринга Azure

Можно выбрать строку hello для пиринга и изменить свойства пиринга hello.

![Обновление частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a>toodelete открытого пиринга Azure

Удалите конфигурацию пиринга, выбрав значок удаления hello, можно, как показано в hello после изображения:

![Удаление частного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a>Общедоступный пиринг Azure

Этот раздел поможет вам создать, получить, обновление и удаление hello Azure открытая конфигурация пиринга канал ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate частного пиринга Azure

1. Настройте канал ExpressRoute. Убедитесь, что цепь hello полностью подготовлена с поставщиком услуг подключения hello перед продолжением дальнейшей.

  ![Отображение общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Настройка открытого пиринга Azure для hello схемы. Убедитесь, что hello следующих элементов, прежде чем продолжить hello следующие шаги:

  * / 30 подсеть для основной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4.
  * / 30 подсеть для дополнительной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4.
  * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
  * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS.
  * **Необязательно —** хэш MD5 при выборе toouse один.
3. Выберите hello Azure открытого пиринга строки, как показано в hello после изображения:

  ![Выбор строки общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. Настройте общедоступный пиринг. Следующие изображения Hello показан пример конфигурации:

  ![Настройка общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. Сохранение конфигурации hello, после того как заданы все параметры. После успешного принятия конфигурации hello, вы видите что-нибудь подобное toohello следующий пример:

  ![Сохранение настройки общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a>tooview открытый пиринг сведения о Azure

Можно просмотреть свойства hello открытого пиринга Azure, выбрав пиринг hello.

![Просмотр свойств общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate конфигурации открытого пиринга Azure

Можно выбрать строку hello для пиринга и изменить свойства пиринга hello.

![Выбор строки общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a>toodelete частного пиринга Azure

Пиринга конфигурации можно удалить, выбрав значок удаления hello, как показано в следующий пример hello:

![Удаление общедоступного пиринга](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a>Пиринг Майкрософт

Этот раздел поможет вам создать, получить, обновление и удаление пиринга конфигурации Microsoft hello за канал ExpressRoute.

> [!IMPORTANT]
> Microsoft пиринг ExpressRoute каналов, которые были настроены предыдущих tooAugust 1, 2017 г. будет иметь все службы префиксов, объявленных через пиринг Майкрософт hello, даже если не определены фильтры маршрутов. Пиринг каналы ExpressRoute, настроенных в течение или после 1 августа 2017 г. Корпорация Майкрософт не будет иметь префиксы объявленных пока фильтр не будет подключено toohello канала. Дополнительные сведения см. в руководстве по [настройке фильтра маршрута для пиринга Майкрософт](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate пиринг Майкрософт

1. Настройте канал ExpressRoute. Убедитесь, что цепь hello полностью подготовлена с поставщиком услуг подключения hello перед продолжением дальнейшей.

  ![Отображение пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Настройка Microsoft пиринг для цепи hello. Убедитесь, что hello следующую информацию, прежде чем продолжить.

  * / 30 подсеть для основной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.
  * / 30 подсеть для дополнительной ссылки hello. Это должен быть допустимый префикс общедоступного адреса IPv4, принадлежащего вам и зарегистрированного в RIR/IRR.
  * Допустимый идентификатор виртуальной локальной сети tooestablish этот пиринг. Убедитесь, что другие пиринги в цепи hello использует hello таким же идентификатором виртуальной локальной сети.
  * Номер AS для пиринга. Можно использовать 2-байтовые и 4-байтовые номера AS.
  * Объявленные префиксы: необходимо предоставить список всех префиксов планирование tooadvertise сеансом BGP hello. Допускаются только общедоступные префиксы IP-адресов. Если планируется toosend набор префиксов, вы можете отправить список с разделителями запятыми. Эти префиксы должны быть tooyou, зарегистрированные в RIR / IRR.
  * **Необязательно —** клиента ASN: если префиксы рекламы, не зарегистрированный toohello пиринг как число, можно указать hello в качестве номера toowhich они зарегистрированы.
  * Имя реестра маршрутизации: Можно указать hello RIR / IRR, для какой hello, а число и префиксы зарегистрирована.
  * **Необязательно —** хэш MD5 при выборе toouse один.
3. Можно выбрать hello пиринг нужно tooconfigure, как показано в следующих hello пример. Выберите строку пиринг Microsoft hello.

  ![Выбор строки пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. Настройте пиринг Майкрософт. Следующие изображения Hello показан пример конфигурации:

  ![Настройка пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. Сохранение конфигурации hello, после того как заданы все параметры.

  Если ваш канал возвращает tooa «Проверка необходимости» состояние (как показано на рисунке hello), необходимо открыть поддержки билет tooshow, подтверждения владения группы поддержки tooour префиксы hello.

  ![Сохранение настройки пиринга Майкрософт](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  Непосредственно из портала hello, можно открыть запрос в службу поддержки, как показано в следующий пример hello:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. После конфигурации hello успешно принято, вы видите что-нибудь подобное toohello после изображения:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a>данные пиринга tooview Microsoft

Можно просмотреть свойства hello открытого пиринга Azure, выбрав пиринг hello.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a>Конфигурация пиринга Майкрософт tooupdate

Можно выбрать строку hello для пиринга и изменить свойства пиринга hello.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a>toodelete пиринг Майкрософт

Удалите конфигурацию пиринга, выбрав значок удаления hello, можно, как показано в hello после изображения:

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a>Дальнейшие действия

Следующий шаг [связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md)
* Дополнительную информацию о рабочих процессах ExpressRoute см. в статье [Процедуры ExpressRoute для подготовки каналов и состояний каналов](expressroute-workflows.md).
* Дополнительную информацию о пиринге канала см. в статье [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).
* Подробнее о работе с виртуальными сетями см. в статье [Обзор виртуальных сетей](../virtual-network/virtual-networks-overview.md).
