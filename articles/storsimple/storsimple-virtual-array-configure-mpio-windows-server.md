---
title: "aaaConfigure MPIO на узле подключен tooStorSimple Virtual Array | Документы Microsoft"
description: "Описывает способ tooconfigure Multipath I/O (MPIO) для массива StorSimple виртуального подключения tooa узла под управлением Windows Server 2012 R2."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a>Настройка многопутевого ввода-вывода на узле Windows Server для hello StorSimple Virtual Array
## <a name="overview"></a>Обзор
В этой статье описывается применять определенные настройки для томов только для StorSimple tooinstall функции Multipath I/O (MPIO) на узле Windows Server и проверьте MPIO для томов StorSimple. процедура Hello предполагается виртуального массива StorSimple 1200 с двумя сетевыми интерфейсами подключенных tooa узла Windows Server с двумя сетевыми интерфейсами. Hello сведения, содержащиеся в этой статье применяется только toohello виртуального массива. Сведения об устройствах серии StorSimple 8000, go слишком[Настройка MPIO для StorSimple узла](storsimple-configure-mpio-windows-server.md). 

функция MPIO Hello в Windows Server помогает построения хранилища высокой доступности, отказоустойчивых конфигурациях. MPIO используются избыточные физические компоненты путей: адаптеры, кабели и коммутаторы — toocreate логические пути между сервером hello и hello запоминающее устройство. В случае сбоя компонента вызывает toofail логический путь логику несколько каналов использует альтернативный путь для ввода-вывода, чтобы приложения по-прежнему иметь доступ к данным. Кроме того в зависимости от вашей конфигурации MPIO можно также повысить производительность, повторно балансировки нагрузки hello для всех путей. Дополнительные сведения см. в статье [Обзор многопутевого ввода-вывода](https://technet.microsoft.com/library/cc725907.aspx "Общие сведения о MPIO и компоненты").

Для hello высокого уровня доступности решения StorSimple настройте MPIO на hello узлов Windows Server для подключенных tooyour StorSimple Virtual Array (модель 1200). серверы узла Hello затем может выдержать связи, сети или интерфейса. 

Вам потребуется toofollow эти действия tooconfigure MPIO: 

* Предварительные требования для настройки
* Шаг 1: Установка MPIO на узле Windows Server hello
* Шаг 2. Настройка MPIO для томов StorSimple
* Шаг 3: Подключение томов StorSimple на узле hello

Каждый из hello выше шаги рассматривается в следующих разделах hello.

## <a name="prerequisites"></a>Предварительные требования
В этом разделе описаны предварительные требования конфигурации hello для узла Windows Server hello и виртуального массива.

### <a name="on-windows-server-host"></a>На узле Windows Server
* Убедитесь, что у узла Windows Server есть 2 активных сетевых интерфейса.

### <a name="on-storsimple-virtual-array"></a>На виртуальном массиве StorSimple
* Hello виртуального массива должны быть настроены как iSCSI-сервера. toolearn более, в разделе [настроить виртуальный массив в качестве сервера iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md). Один или несколько сетевых интерфейсов должен быть включен в массиве hello.   
* Hello сетевые интерфейсы на виртуального массива должен быть доступен hello узле Windows Server.
* В виртуальном массиве StorSimple необходимо создать один или несколько томов. toolearn более, в разделе [добавить том](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) на ваш StorSimple Virtual Array. В этой процедуре мы создали виртуального массива hello 3 тома (1 локально закрепленные и 2 многоуровневого тома, как показано ниже).
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>Конфигурация оборудования для виртуального массива StorSimple
на следующем рисунке Hello показывает hello конфигурация оборудования для обеспечения высокой доступности и балансировки нагрузки несколько каналов для узла Windows Server и StorSimple Virtual Array, используемых в этой процедуре.

![конфигурация оборудования mpio](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

Как показано в предшествующих рисунок hello:

* Виртуальный массив StorSimple, выделенный в Hyper-V, — это активное устройство с одним узлом, настроенное в качестве сервера iSCSI.
* В массиве активировано два виртуальных сетевых интерфейса. В hello локального веб-Интерфейсе виртуального массива, двумя сетевыми интерфейсами проверить, разрешены ли перейдя слишком**параметры сети** как показано ниже:
  
    ![сетевые интерфейсы, включенные в 1200](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    Примечание hello IPv4-адреса hello включена сетевых интерфейсов (Ethernet, Ethernet 2 по умолчанию) и сохранить для последующего использования на узле hello.
* На узле Windows Server активировано два сетевых интерфейса. Если hello подключенных интерфейсы для массива и узла находятся в hello одной подсети, то будут 4 пути. Это был вариант hello в этой процедуре. Однако если каждому сетевому интерфейсу на интерфейсе hello массива и узла в другой подсети IP (и не маршрутизируемый), затем только 2 пути будут доступны.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Шаг 1: Установка MPIO на узле Windows Server hello
MPIO представляет собой дополнительный компонент, который по умолчанию не устанавливается в Windows Server. Его необходимо устанавливать в качестве отдельного компонента через диспетчер сервера. выполнить эту функцию на узле Windows Server, tooinstall Здравствуйте, следуйте инструкциям.

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Шаг 2. Настройка MPIO для томов StorSimple
MPIO должен томов StorSimple tooidentify toobe настроен. тома StorSimple toorecognize tooconfigure MPIO, выполнять hello следующие шаги.

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Шаг 3: Подключение томов StorSimple на узле hello
После настройки MPIO на Windows Server тома, созданные для массива StorSimple hello можно подключить и затем можно использовать преимущества MPIO для обеспечения избыточности. toomount тома, выполните hello следующие шаги.

#### <a name="toomount-volumes-on-hello-host"></a>toomount тома узла hello
1. Откройте hello **свойства инициатора iSCSI** окна на узле Windows Server hello. Go слишком**диспетчера сервера > Панель мониторинга > Сервис > инициатор iSCSI**.
2. В hello **свойства инициатора iSCSI** диалоговое окно, нажмите кнопку **обнаружения**, а затем нажмите кнопку **обнаружить целевой портал**.
3. В hello **обнаружить целевой портал** диалогового окна поле, hello следующие:
   
    1. Введите IP-адрес hello hello первый включена сетевого интерфейса на ваш StorSimple Virtual Array. По умолчанию это **Ethernet**. 
    2. Нажмите кнопку **ОК** tooreturn toohello **свойства инициатора iSCSI** диалоговое окно.
     
    > [!IMPORTANT]
    > При использовании частной сети для подключений iSCSI введите IP-адрес hello порта данных hello подключенных toohello частной сети.
     
4. Повторите шаги 2–3 для второго сетевого интерфейса (например Ethernet 2) в массиве. 
5. Выберите hello **цели** на вкладке hello **свойства инициатора iSCSI** диалоговое окно. Для виртуального массива в разделе **Обнаруженные конечные объекты**каждый том будет отображаться как конечный объект. В этом случае будет обнаруживаются три целевых объектов (соответствующие тома toothree).
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. Нажмите кнопку **Connect** tooestablish сеанс iSCSI с помощью виртуального массива StorSimple. Объект **подключения tooTarget** появится диалоговое окно. Выберите hello **включить поддержку многопутевых накопителей** флажок. Нажмите кнопку **Дополнительно**.
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. В hello **Дополнительные параметры** диалогового окна поле, hello следующие:                                        
   
    1. На hello **локальный адаптер** раскрывающемся списке выберите **инициатора iSCSI (Майкрософт)**.
    2. На hello **IP вызывающая** раскрывающегося списка, выберите hello IP-адрес узла hello.
    3. На hello **целевого портала** IP раскрывающегося списка, выберите hello IP-интерфейса массива.
    4. Нажмите кнопку **ОК** tooreturn toohello **свойства инициатора iSCSI** диалоговое окно.
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. Щелкните **Свойства**. 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. В hello **свойства** диалоговое окно, нажмите кнопку **добавить сеанс**.
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. В hello **подключения tooTarget** диалоговое окно, выберите hello **включить поддержку многопутевых накопителей** флажок. Нажмите кнопку **Дополнительно**.
11. В hello **Дополнительные параметры** диалоговое окно:                                        
    
    1. На hello **локальный адаптер** раскрывающегося списка, выберите инициатор Microsoft iSCSI.

    2. На hello **IP вызывающая** раскрывающегося списка, соответствующий узел toohello выберите hello IP адрес. В этом случае выполняется подключение двух сетевых интерфейсов на один сетевой интерфейс tooa hello массива на узле hello. Таким образом этот интерфейс является hello же как для hello первого сеанса.

    3. На hello **целевой IP-адрес портала** раскрывающегося списка, выберите hello IP-адрес для hello включена в массиве hello второго интерфейса данных.

    4. Нажмите кнопку **ОК** tooreturn toohello iSCSI инициатора свойства. Добавлен второй сеанс toohello целевой объект.
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. После добавления hello требуемого сеансов (путей) в hello **свойства инициатора iSCSI** диалоговое окно, выберите hello целевой и нажмите кнопку **свойства**. На вкладке сеансы hello hello **свойства** диалоговое окно, Примечание hello четыре идентификатора сеансов, соответствующие toohello возможным пермутациям пути. Выберите идентификатор сеанса Далее tooa hello флажок toocancel сеанс и нажмите кнопку **Disconnect**.

    6. tooview устройств, представленных в сеансах, выберите hello **устройств** щелкните вкладку tooconfigure hello политику MPIO для выбранного устройства, **MPIO**.

    7. Hello **сведения** появится диалоговое окно. На hello **MPIO** вкладку, можно выбрать соответствующий hello **политика балансировки нагрузки** параметры. Вы также можете просмотреть hello **Active** или **Standby** тип пути.
12. Повторите шаги 8 – 11 tooadd Дополнительные сеансы (пути) toohello цели. С двумя интерфейсами на узле hello и два источника на hello виртуального массива можно добавить итог четыре сеансов для каждого целевого объекта. 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. Необходимо будет toorepeat эти шаги для каждого тома (поверхности в качестве целевого объекта).
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. Откройте **Управление компьютером** , перейдя по слишком**Диспетчер серверов > Панель мониторинга > Управление компьютером**. Hello левой панели щелкните **хранения > Управление дисками**. Hello томах, созданные на hello StorSimple Virtual Array, являются видимыми toothis узла будет отображаться в разделе **Управление дисками** как новые диски.
15. Инициализация диска hello и создайте новый том. В процессе hello Формат выберите размер единицы размещения (AUS) 64 КБ. Повторите процесс hello для всех доступных томов hello.
    
    ![Управление дисками](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. В разделе **Управление дисками**, щелкните правой кнопкой мыши hello **диска** и выберите **свойства**.
17. В hello **несколькими свойства многопутевого диска** диалоговое окно, нажмите кнопку hello **MPIO** вкладки.
    
    ![Свойства диска](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. В hello **имя DSM** щелкните **сведения** и убедитесь, что параметры hello заданы параметры по умолчанию toohello. используются следующие параметры по умолчанию Hello.
    
    * Период проверки пути = 30.
    * Счетчик попыток = 3.
    * Период удаления PDO = 20.
    * Интервал попытки = 1.
    * Проверка пути включена = флажок снят.
    
    > [!NOTE]
    > **Не изменяйте параметры по умолчанию hello.**
   
## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство виртуального массива StorSimple](storsimple-virtual-array-manager-service-administration.md).

