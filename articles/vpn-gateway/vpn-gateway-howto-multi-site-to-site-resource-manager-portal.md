---
title: "Добавление нескольких VPN шлюзом для межсайтовых подключений tooa виртуальной сети: портала Azure: диспетчер ресурсов | Документы Microsoft"
description: "Добавление нескольких сайтов S2S подключений tooa VPN-шлюз, имеется существующее подключение"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a>Добавить tooa подключения сайта для сайта виртуальной сети с помощью существующего VPN-подключения шлюза

> [!div class="op_single_selector"]
> * [Портал Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (классическая модель)](vpn-gateway-multi-site.md)
>
> 

В этой статье описывается использование hello Azure портала tooadd-сайтами (S2S) подключений tooa VPN-шлюз, имеется существующее подключение. Этот тип подключения чаще всего ссылка tooas конфигурации «нескольких сайтов». Вы можете добавить tooa подключения S2S виртуальной сети, который уже S2S подключение, подключение точка-сеть или подключение виртуальной сети для виртуальной сети. При добавлении подключения есть некоторые ограничения. Проверьте hello [перед началом](#before) раздела в этой статье tooverify, прежде чем начать настройку. 

Эта статья относится tooVNets, созданных с помощью модели развертывания диспетчера ресурсов hello, шлюз VPN routebased.. Эти действия не относятся существующих конфигураций подключений tooExpressRoute/сайт-сайт. Сведения о параллельно существующих подключениях см. в разделе [Параллельно существующие подключения ExpressRoute и "сеть — сеть"](../expressroute/expressroute-howto-coexist-resource-manager.md).

### <a name="deployment-models-and-methods"></a>Модели и методы развертывания
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Мы обновляем эту таблицу по мере выпуска новых статей и дополнительных инструментов для этой конфигурации. Если статья доступен, непосредственно свяжем tooit из этой таблицы.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>Перед началом работы
Проверьте hello следующих элементов:

* Убедитесь, что не создаете параллельно действующие подключения ExpressRoute и "сеть — сеть".
* У вас есть виртуальная сеть, созданную с помощью модели развертывания диспетчера ресурсов hello использовать существующее подключение.
* Hello шлюз виртуальной сети для виртуальной сети — routebased.. При наличии шлюза PolicyBased VPN, необходимо удалить шлюз виртуальной сети hello и создать новый шлюз VPN как routebased..
* Ни один из диапазонов адресов hello перекрываться для любого hello виртуальных сетей, которая подключается к этой виртуальной сети.
* У вас есть совместимых устройств VPN и тем, кто имеет доступ tooconfigure его. См. статью о [VPN-устройствах](vpn-gateway-about-vpn-devices.md). Если вы не знакомы с конфигурацией своего устройства VPN или не знакомы с hello диапазоны IP-адресов в конфигурации локальной сети, необходимо toocoordinate с тем, кто сможет предоставить эти сведения для вас.
* Имеется внешний общедоступный IP-адрес для VPN-устройства. Этот IP-адрес не может располагаться вне преобразования сетевых адресов (NAT).

## <a name="part1"></a>Часть 1. Настройка подключения
1. В браузере перейдите toohello [портал Azure](http://portal.azure.com) и, при необходимости, выполнить вход с учетной записью Azure.
2. Нажмите кнопку **все ресурсы** и найдите вашей **шлюз виртуальной сети** из списка ресурсов hello и щелкните его.
3. На hello **шлюз виртуальной сети** колонка, щелкните **подключения**.
   
    ![Колонка подключений](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Колонка подключений")<br>
4. На hello **подключений** колонка, щелкните **+ добавить**.
   
    ![Добавить кнопки подключения](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "кнопку Добавить соединения")<br>
5. На hello **добавить подключение** колонки, заполните следующие поля hello:
   
   * **Имя:** hello имя узла toohello toogive вы создаете подключение hello.
   * **Тип подключения.** Выберите **Сеть — сеть (IPSec)**.
     
     ![Добавить подключение колонке](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "добавить подключение колонку")<br>

## <a name="part2"></a>Часть 2. Добавление шлюза локальной сети
1. Щелкните **Шлюз локальной сети**, а затем ***Выберите шлюз локальной сети***. После этого откроется hello **Выбор шлюза локальной сети** колонку.
   
    ![Выбор шлюза локальной сети](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Выбор шлюза локальной сети")<br>
2. Нажмите кнопку **создать новый** tooopen hello **создать шлюз локальной сети** колонку.
   
    ![Создание локальной сети шлюза колонке](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "создать шлюз локальной сети")<br>
3. На hello **создать шлюз локальной сети** колонки, заполните следующие поля hello:
   
   * **Имя:** hello имя ресурса шлюза локальной сети toohello toogive.
   * **IP-адрес:** hello hello VPN-устройства на узел hello tooconnect на общедоступный IP-адрес.
   * **Адресное пространство:** hello адресное пространство, которое следует toobe направлено toohello новый сайт локальной сети.
4. Нажмите кнопку **ОК** на hello **создать шлюз локальной сети** колонке toosave hello изменения.

## <a name="part3"></a>Часть 3 — добавить общий ключ hello и создания подключения hello
1. На hello **добавить подключение** колонке добавить hello общий ключ должен toouse toocreate подключения к. Можно получить общий ключ hello из устройства VPN или сделать здесь и затем настройте ваш hello toouse устройство VPN же общим ключом. важный, что это ключи hello абсолютно Hello hello таким же.
   
    ![Общий ключ](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Общий ключ")<br>
2. Hello нижней части колонки hello, нажмите кнопку **ОК** toocreate hello соединения.

## <a name="part4"></a>Часть 4 - Проверка hello VPN-подключения


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей. Hello виртуальные машины в разделе [обучения](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) для получения дополнительной информации.
