---
title: "Проверка пропускной способности VPN tooa виртуальная сеть Microsoft Azure | Документы Microsoft"
description: "Hello цель данного документа — toohelp пользователя проверить пропускную способность сети hello из их tooan ресурсы локальной виртуальной машине Azure."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>Как toovalidate VPN пропускной способности tooa виртуальной сети

Шлюз VPN-подключение позволяет tooestablish безопасность, подключения между организациями между виртуальной сети в Azure и локальной ИТ-инфраструктуры.

В этой статье показано, как toovalidate пропускную способность сети из hello локальной tooan ресурсы виртуальной машины Azure. Кроме того, в ней приведены рекомендации по устранению неполадок.

>[!NOTE]
>Эта статья посвящена toohelp диагностики и устранения распространенных проблем. Если вы не удается toosolve hello проблема, используя следующую информацию, hello [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
>
>

## <a name="overview"></a>Обзор

Hello шлюза VPN-подключения включает в себя hello следующие компоненты:

- Локальное VPN-устройство (см. список [проверенных VPN-устройств](vpn-gateway-about-vpn-devices.md#devicetable)).
- Общедоступный Интернет
- VPN-шлюз Azure
- Виртуальная машина Azure

Hello, следующая диаграмма показывает hello логические подключения локальной сети tooan виртуальной сети Azure через виртуальную частную сеть.

![TooMSFT логические сети клиента подключения к сети с помощью VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>Вычислить hello максимальный ожидаемый Исходящие и входящие данные

1.  Определите базовые требования приложения к пропускной способности.
2.  Определите предел пропускной способности для VPN-шлюза Azure. Для получения справки, в разделе hello» суммарную пропускную способность, SKU и VPN типа» [планирования и проектирования для шлюза VPN](vpn-gateway-plan-design.md).
3.  Определить hello [виртуальной Машины Azure пропускная способность рекомендации](../virtual-machines/virtual-machines-windows-sizes.md) для размер виртуальной Машины.
4.  Определите пропускную способность поставщика услуг Интернета (ISP).
5.  Вычислите ожидаемую пропускную способность — наименьшая пропускная способность (виртуальной машины, шлюза, поставщика услуг Интернета) * 0,8.

Если вычисляемый пропускная способность не соответствует требованиям приложения базовые пропускной способности, необходимо пропускной способности hello tooincrease hello ресурса, который считается hello узким местом. tooresize шлюз VPN Azure в разделе [изменение номер SKU шлюза](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku). tooresize виртуальной машины в разделе [изменить размер виртуальной Машины](../virtual-machines/virtual-machines-windows-resize-vm.md). Если вы не столкнетесь с ожидаемой пропускной способности Интернета, можно также toocontact поставщика услуг Интернета.

## <a name="validate-network-throughput-by-using-performance-tools"></a>Проверка пропускной способности сети с помощью средств повышения производительности

Эту проверку следует выполнять в часы пониженной нагрузки, так как насыщенность пропускной способности туннеля VPN при тестировании не позволяет получить точные результаты.

Средство Hello, мы используем для этого теста является iPerf, который работает в Windows и Linux и имеет режима сервера и клиента. Это ограниченное too3 Гбит/с для виртуальных машин Windows.

Это средство не выполняет любой toodisk операций чтения и записи. Самостоятельно сформированный трафик TCP от одного конечного toohello других исключительно создается. Статистику на основании экспериментов, что меры hello пропускную способность между клиентом и сервером узлами, оно создано. При тестировании между двумя узлами, один действует как сервер hello и hello других в качестве клиента. После завершения этого теста, рекомендуется, выполняется обратная tootest ролей hello и отправка и загрузка пропускной способности на обоих узлах.

### <a name="download-iperf"></a>Скачивание iPerf
Скачайте [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip). Дополнительные сведения см. в [документации по iPerf](https://iperf.fr/iperf-doc.php).

 >[!NOTE]
 >Hello сторонние продукты, которые описаны в этой статье, созданы компаниями, не зависимыми от Майкрософт. Корпорация Майкрософт не дает никаких гарантий, явных или подразумеваемых гарантий, о hello производительности и надежности этих продуктов.
 >
 >

### <a name="run-iperf-iperf3exe"></a>Запуск iPerf (iperf3.exe)
1. Включите правило NSG и ACL, разрешающее трафик hello (для тестирования на виртуальной Машине Azure общедоступный IP-адрес).

2. На обоих узлах включите исключение брандмауэра для порта 5001.

    **Windows:** выполнения hello следующую команду с правами администратора:

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    правило hello tooremove при тестировании завершена, выполните следующую команду:

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Linux в Azure.** Образы Linux в Azure имеют нестрогие брандмауэры. В случае прослушивание порта приложения hello-трафика через. Для защищенных пользовательских образов может потребоваться явно открыть нужные порты. В число распространенных брандмауэров уровня ОС для Linux входят `iptables`, `ufw` и `firewalld`.

3. На узле сервера hello измените toohello каталог, где извлекается iperf3.exe. Затем запустите iPerf в режиме сервера и сделать его toolisten через порт 5001 hello, следующие команды:

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. На узле клиента hello измените toohello каталог, где средство iperf извлечены и затем выполните следующую команду hello:

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    Hello клиент инициирует трафик через порт 5001 toohello сервера на 30 секунд. Здравствуйте, флаг "-P", указывающее, мы используем 32 узла сервера toohello одновременных подключений.

    Hello следующий экран показывает hello выходные данные в этом примере:

    ![Выходные данные](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. (Необязательно) toopreserve hello тестирование результатов, выполните следующую команду:

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. После выполнения предыдущих шагов hello, выполните hello отменить же действия с ролями hello, таким образом, hello узел сервера теперь будет hello клиента и наоборот.

## <a name="address-slow-file-copy-issues"></a>Решение проблем с низкой скоростью при копировании файлов
При использовании проводника или перетаскивании объектов во время сеанса RDP может наблюдаться снижение скорости копирования файлов. Эта проблема обычно является из-за tooone или оба hello следующие факторы:

- Приложения для копирования файлов, такие как проводник и RDP, не используют несколько потоков при копировании. Для повышения производительности используйте многопоточные копирования файлов, например [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy файлы с помощью потоков 16 или 32. Щелкните номер потока hello toochange для копирования файлов в Richcopy, **действия** > **параметры копирования** > **копирование файла**.<br><br>
![Проблемы с низкой скоростью при копировании файлов](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- Недостаточная скорость чтения и записи виртуальной машины. Дополнительные сведения см. в статье [Устранение неполадок службы хранилища Azure](../storage/common/storage-e2e-troubleshooting.md).

## <a name="on-premises-device-external-facing-interface"></a>Внешний интерфейс для локального устройства
Если hello локального VPN-устройства из Интернета IP-адрес включается в hello [локальной сети](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) определение в Azure, могут возникнуть toobring невозможности hello отключает VPN, случайные или проблем с производительностью.

## <a name="checking-latency"></a>Проверка задержки
Используйте tracert tootrace tooMicrosoft Azure Edge устройства toodetermine при наличии задержки превышает 100 мс между прыжков.

Запустите из локальной сети hello, *tracert* toohello VIP hello шлюза Azure или виртуальной Машины. Как только вы увидите только * возвращен, вы знаете, достигнуто hello Azure edge. При появлении DNS-имена, включающие «MSN» вернул известно, что достигнуто магистрали Microsoft hello.<br><br>
![Проверка задержки](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>Дальнейшие действия
Для получения дополнительных сведений справки ознакомьтесь с hello ссылкам:

- [Оптимизации пропускной способности сети для виртуальной машины Azure](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Служба технической поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
