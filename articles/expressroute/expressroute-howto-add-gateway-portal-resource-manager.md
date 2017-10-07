---
title: "Добавление виртуальной сети шлюза tooa виртуальной сети для ExpressRoute: портал: Azure | Документы Microsoft"
description: "В этой статье описывается добавление tooan шлюза виртуальной сети, уже созданы диспетчера ресурсов виртуальной сети для ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>Настройка шлюза виртуальной сети для ExpressRoute с помощью портала Azure hello
> [!div class="op_single_selector"]
> * [Resource Manager — портал Azure](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager — PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Классическая модель: PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

В этой статье поможет tooadd действия hello шлюз виртуальной сети для существующей виртуальной сети. В этой статье рассматриваются действия tooadd hello, масштабировать и удалить шлюз виртуальной сети (VNet) для существующей виртуальной сети. Hello этапах данной конфигурации предназначены специально для виртуальных сетей, которые были созданы с помощью модели развертывания диспетчера ресурсов hello, который будет использоваться в конфигурации ExpressRoute. Дополнительные сведения о шлюзах виртуальных сетей и параметрах конфигурации шлюза для ExpressRoute см. в разделе [Сведения о шлюзах виртуальных сетей ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Подготовка

Hello действия для этой задачи используйте виртуальную сеть на основе hello значений в следующий список ссылок на конфигурации hello. Мы используем этот список для работы с примером. Можно скопировать toouse список hello как ссылка, заменив значения hello собственные.

**Справочный список для конфигурации**

* Имя виртуальной сети: TestVNet.
* Адресное пространство виртуальной сети: 192.168.0.0/16.
* Имя подсети: FrontEnd. 
    * Адресное пространство подсети: 192.168.1.0/24.
* Группа ресурсов — TestRG.
* Расположение: восточная часть США.
* Имя подсети шлюза: GatewaySubnet; подсеть шлюза всегда необходимо называть *GatewaySubnet*.
    * Адресное пространство шлюза подсети: 192.168.200.0/26.
* Имя шлюза: ERGW.
* IP-имя шлюза: MyERGWVIP.
* Тип шлюза: ExpressRoute. Для конфигурации ExpressRoute требуется этот тип.
* Общедоступное IP-имя шлюза: MyERGWVIP.

Можно просмотреть [видео](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) об этих действиях перед началом настройки.

## <a name="create-hello-gateway-subnet"></a>Создать подсеть шлюза hello

1. В hello [портала](http://portal.azure.com), перейдите toohello диспетчера ресурсов виртуальной сети для которого требуется toocreate шлюз виртуальной сети.
2. В hello **параметры** раздел колонка вашей виртуальной сети, нажмите кнопку **подсети** tooexpand hello подсетей колонку.
3. На hello **подсетей** колонка, щелкните **+ подсеть шлюза** tooopen hello **добавить подсеть** колонку. 
   
    ![Добавить подсеть шлюза hello](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "добавить подсеть шлюза hello")


4. Hello **имя** для подсети автоматически заполняется hello значение «GatewaySubnet». Это значение необходимо для подсети Azure toorecognize hello как hello подсеть шлюза. Настройка автоматического заполнения hello **диапазона адресов** значения toomatch требований к конфигурации. Рекомендуется создать подсеть шлюза с блоком адресов /27 или больше (/26, /25 и т. д.). Нажмите кнопку **ОК** toosave hello значения и создать подсеть шлюза hello.

    ![Добавление подсети hello](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "Добавление подсети hello")

## <a name="create-hello-virtual-network-gateway"></a>Создание шлюза виртуальной сети hello

1. На портале hello левой hello, щелкните  **+**  и введите «Шлюз виртуальной сети» в поиске. Найдите **шлюз виртуальной сети** в поиске hello вернуться и щелкните запись hello. На hello **шлюз виртуальной сети** колонка, щелкните **создать** hello нижней части колонки hello. При этом откроется hello **создать шлюз виртуальной сети** колонку.
2. На hello **создать шлюз виртуальной сети** колонки, заполните значения hello шлюз виртуальной сети.

    ![Поля колонки "Создание шлюза виртуальной сети"](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Поля колонки "Создание шлюза виртуальной сети"")
3. **Имя**. Назовите свой шлюз. Это не является hello то же, что для подсети шлюза. Его по имени hello объекта hello шлюза, который вы создаете.
4. **Тип шлюза**. Выберите **ExpressRoute**.
5. **SKU**: номер SKU шлюза hello выберите из раскрывающегося списка hello.
6. **Расположение**: Настройка hello **расположение** поле toopoint toohello расположение виртуальной сети. Если расположение hello не указывает toohello региона, где находится виртуальной сети, hello виртуальной сети не отображается в раскрывающемся списке «Выберите виртуальную сеть» hello.
7. Выберите toowhich hello виртуальной сети требуется tooadd этого шлюза. Нажмите кнопку **виртуальная сеть** tooopen hello **выберите виртуальную сеть** колонку. Выберите hello виртуальной сети. Если вы не видите виртуальной сети, убедитесь, что hello **расположение** поле указывает toohello регион, в котором находится виртуальной сети.
9. Выберите общедоступный IP-адрес. Нажмите кнопку **общедоступный IP-адрес** tooopen hello **выберите общедоступный IP-адрес** колонку. Нажмите кнопку **+ создать** tooopen hello **создать открытый IP адрес колонке**. Введите имя общедоступного IP-адреса. Эта колонка создает открытый toowhich объекта адрес IP, динамически назначен общедоступный IP-адрес. Нажмите кнопку **ОК** toosave к колонке toothis изменения.
10. **Подписки**: Убедитесь, что правильно выбрана подписка hello.
11. **Группа ресурсов**: этот параметр определяется hello виртуальной сети, который выбран.
12. Не изменять hello **расположение** после выбора hello предыдущие параметры.
13. Проверьте параметры hello. Если требуется, чтобы ваш tooappear шлюза на панели мониторинга hello, можно выбрать **toodashboard ПИН-код** hello нижней части колонки hello.
14. Нажмите кнопку **создать** toobegin Создание шлюза hello. Параметры Hello проверяются и развертывает hello шлюза. Создание шлюза виртуальной сети может занять toocomplete too45 минут.

## <a name="next-steps"></a>Дальнейшие действия
После создания шлюза виртуальной сети hello, можно связать вашей виртуальной сети tooan канал ExpressRoute. В разделе [связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md).
