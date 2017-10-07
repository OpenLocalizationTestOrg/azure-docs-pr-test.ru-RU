---
title: "aaaProvision StorSimple Virtual Array в VMware | Документы Microsoft"
description: "Это второе руководство из серии, посвященной развертыванию виртуального массива StorSimple, в котором описывается подготовка виртуального устройства в VMware."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a>Развертывание виртуального массива StorSimple — подготовка в VMware
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a>Обзор
В данном учебнике как tooprovision и подключите tooa StorSimple Virtual Array в системе узла, под управлением VMware ESXi 5.5 и более поздних версий. Эта статья относится развертывания toohello StorSimple виртуальных массивов в портале Azure и hello государственных облако Microsoft Azure.

Требуется tooprovision правами администратора и подключитесь tooa виртуального устройства. Hello подготовки и базовая установка может занять около 10 минут toocomplete.

## <a name="provisioning-prerequisites"></a>Предварительные требования к подготовке
Здравствуйте, tooprovision необходимые компоненты виртуального устройства в системе узла, под управлением VMware ESXi 5.5 и выше, приведены ниже.

### <a name="for-hello-storsimple-device-manager-service"></a>Для hello службой диспетчера устройств StorSimple
Перед тем как начать, убедитесь в следующем.

* Выполнены все действия hello в [портал hello подготовки для StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).
* Загруженный hello образа виртуального устройства для VMware с hello портал Azure. Дополнительные сведения см. в разделе **шаг 3: загрузка образа виртуального устройства hello** из [подготовки портала hello руководство StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).

### <a name="for-hello-storsimple-virtual-device"></a>Для виртуального устройства StorSimple hello
Перед развертыванием виртуального устройства нужно выполнить указанные ниже условия.

* У вас есть доступ tooa компьютерной системе под управлением Hyper-V (2008 R2 или более поздней версии), могут быть используется tooa подготавливать устройства.
* Hello система узла — может toodedicate hello следующие ресурсы tooprovision виртуального устройства:

  * Не менее 4 ядер.
  * Не менее 8 ГБ ОЗУ. Если планируется tooconfigure hello виртуального массива как файловый сервер, 8 ГБ поддерживает менее 2 миллионов файлов. Необходимо 2-4 миллиона toosupport файла по 16 ГБ ОЗУ.
  * Один сетевой интерфейс.
  * Виртуальный диск размером 500 ГБ для системных данных.

### <a name="for-hello-network-in-datacenter"></a>Для hello сети в центре обработки данных
Перед тем как начать, убедитесь в следующем.

* После знакомства с hello сетевые требования toodeploy виртуальное устройство StorSimple и настроенный hello сети центра обработки данных согласно требованиям hello. 

## <a name="step-by-step-provisioning"></a>Пошаговая подготовка
tooprovision и подключение виртуального устройства tooa, требуется hello tooperform следующие шаги:

1. Убедитесь, что система hello узла имеет достаточно ресурсов toomeet hello минимальным требованиям к виртуальному устройству.
2. Подготовьте виртуальное устройство в низкоуровневой оболочке.
3. Запуск виртуального устройства hello и получение hello IP-адрес.

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a>Шаг 1. Обеспечение соответствия главной системы минимальным требованиям к виртуальному устройству
toocreate виртуальное устройство, необходимы следующие компоненты:

* Доступ tooa компьютерной системе под управлением VMware ESXi Server 5.5 и более поздних версий.
* Клиент vSphere VMware на узле ESXi hello toomanage системы.

  * Не менее 4 ядер.
  * Не менее 8 ГБ ОЗУ. Если планируется tooconfigure hello виртуального массива как файловый сервер, 8 ГБ поддерживает менее 2 миллионов файлов. Необходимо 2-4 миллиона toosupport файла по 16 ГБ ОЗУ.
  * Один сетевой интерфейс подключен toohello сеть, позволяющей tooInternet маршрутизации трафика. Hello минимальной пропускной способности Интернета должно быть 5 tooallow Мбит/с для оптимальной работы устройства hello.
  * Виртуальный диск данных размером 500 ГБ.

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a>Шаг 2. Подготовка виртуального устройства в низкоуровневой оболочке
Выполните следующие шаги tooprovision виртуального устройства в вашей низкоуровневой оболочки hello.

1. Копировать изображение hello виртуального устройства в системе. Вы загрузили этот виртуальный образ через портал Azure hello.

   1. Убедитесь, что вы скачали hello последнего файла образа. Если ранее загруженный образ hello загрузите его снова tooensure, у вас есть образ последнюю hello. Hello последний образ имеет два файла (а не одной).
   2. Запишите расположение hello, где сохранен hello изображения с помощью этого образа позже в процедуре hello.

2. Войдите в систему toohello сервер ESXi, с помощью клиента vSphere hello. Необходимо toocreate привилегии администратора toohave виртуальной машины.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. В клиенте vSphere hello в разделе инвентаризации hello hello левой панели выберите hello ESXi сервера.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. Отправьте hello VMDK toohello ESXi сервера. Перейдите toohello **конфигурации** hello правой панели. В списке **Hardware** (Оборудование) выберите пункт **Storage** (Хранилище).

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. В hello правой панели в разделе **хранилища данных**, выберите hello место tooupload hello VMDK хранилища данных. хранилище данных Hello должен иметь достаточно свободного места для hello ОС и дисков данных.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. Щелкните правой кнопкой мыши и выберите пункт **Browse Datastore** (Обзор хранилища данных).

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. Отобразится окно **Datastore Browser** (Браузер хранилища данных).

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. На панели инструментов hello, нажмите кнопку ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) toocreate значок новую папку. Укажите имя папки hello и запомните или запишите его. Это имя будет использоваться позднее при создании виртуальной машины (рекомендуется). Нажмите кнопку **ОК**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. в левой области hello hello появится новая папка Hello **обозревателя хранилища данных**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. Щелкните значок передачи hello ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) и выберите **передать файл**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. Найдите и выберите toohello VMDK-файлы, загруженные. Вы увидите два файла. Выберите tooupload файл.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. Щелкните **Открыть**. Отправка Hello toohello файл VMDK hello указанное хранилище данных запускает. Он может занять несколько минут для файла tooupload hello.
13. После завершения передачи hello появиться hello файла в хранилище данных hello в созданную папку hello.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    Теперь отправить hello второй VMDK файл toohello же хранилище данных.
14. Возвращает окно клиента toohello vSphere. Выбрав сервер ESXi, щелкните правой кнопкой мыши и выберите пункт **New Virtual Machine**(Создать виртуальную машину).

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. Отобразится окно **Create New Virtual Machine** (Создание виртуальной машины). На hello **конфигурации** страницу, выберите hello **настраиваемый** параметр. Щелкните **Далее**.
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. На hello **имя и расположение** укажите hello имя виртуальной машины. Это имя должно соответствовать имени папки hello (рекомендуется), указанную ранее в шаге 8.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. На hello **хранения** выберите хранилище данных, требуется toouse tooprovision ВМ.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. На hello **версия виртуальной машины** выберите **версия виртуальной машины: 8**. Too11 версии 8 для всех поддерживаемых.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. На hello **гостевой операционной системы** страницу, выберите hello **гостевой операционной системы** как **Windows**. Для **версии**, в раскрывающемся списке «hello» выберите **Microsoft Windows Server 2012 (64-разрядная версия)**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. На hello **процессоров** настройте hello **число виртуальных процессоров** и **число ядрами на сокет виртуального** , который hello **общее число ядер**— 4 (или более). Щелкните **Далее**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. На hello **памяти** укажите 8 ГБ (или более) ОЗУ. Щелкните **Далее**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. На hello **сети** укажите hello количество hello сетевых интерфейсов. Hello минимальные требования составляют один сетевой интерфейс.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. На hello **SCSI-контроллер** примите по умолчанию hello **контроллеров LSI SAS логику**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. На hello **выберите диск** выберите **использовать существующий виртуальный диск**. Щелкните **Далее**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. На hello **выберите существующий диск** в разделе **путь к файлу диска**, нажмите кнопку **Обзор**. Откроется диалоговое окно **Browse Datastores** (Обзор хранилищ данных). Перейдите в расположение toohello, где вы отправили hello VMDK. Вы увидите только один файл в хранилище данных hello как hello двух файлов, изначально загруженные были объединены. Выберите файл hello и нажмите кнопку **ОК**. Щелкните **Далее**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. На hello **Дополнительные параметры** , примите значение по умолчанию hello и нажмите кнопку **Далее**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. На hello **готовности tooComplete** просмотрите все параметры hello hello новой виртуальной машины. Проверьте **изменить параметры виртуальной машины hello до завершения**. Нажмите кнопку **Продолжить**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. На hello **свойства виртуальных машин** страницы в hello **оборудования** найдите hello оборудования устройства. Выберите пункт **New Hard Disk**(Новый жесткий диск). Щелкните **Добавить**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. Откроется окно **Add Hardware** (Установка оборудования). На hello **тип устройства** в разделе **hello выберите тип устройства, нужно tooadd**выберите **жесткого диска**и нажмите кнопку **Далее**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. На hello **выберите диск** выберите **создать новый виртуальный диск**. Щелкните **Далее**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. На hello **создать диск** измените hello **размер диска** too500 ГБ (или более). Хотя 500 ГБ hello минимальным требованиям, всегда можно подготовить диск большего размера. Обратите внимание, что вы не может увеличивать и уменьшать один раз подготовленного диска hello. Дополнительные сведения о hello размер диска tooprovision, можно узнать в разделе размера hello в hello [обеспечению](storsimple-ova-best-practices.md). В разделе **Disk Provisioning** (Подготовка диска) выберите пункт **Thin Provision** (Тонкая подготовка). Щелкните **Далее**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. На hello **Дополнительно** примите по умолчанию hello.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. На hello **готовности tooComplete** просмотрите параметры диска hello. Нажмите кнопку **Готово**

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. Возвращает toohello страницы свойств виртуальной машины. Новый жесткий диск будет добавлен tooyour виртуальной машины. Нажмите кнопку **Готово**

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. На виртуальной машине, выбранного в правой области hello перейдите toohello **Сводка** вкладки. Просмотрите параметры hello для виртуальной машины.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

Теперь виртуальная машина подготовлена. Hello следующим шагом является toopower на этом компьютере и получить hello IP-адрес.

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a>Шаг 3: Запустите hello виртуальное устройство и получение IP-адреса hello
Выполните следующие шаги toostart hello виртуального устройства и подключения tooit.

#### <a name="toostart-hello-virtual-device"></a>toostart hello виртуального устройства
1. Запуск виртуального устройства hello. В vSphere hello Configuration Manager в левой области hello выберите устройство и щелкните правой кнопкой мыши toobring hello контекстного меню. Выберите **Power** (Питание), а затем — **Power on** (Включить). Виртуальная машина включится. Можно просмотреть состояние hello в нижней hello **последние задачи** области клиента vSphere hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. задачи настройки Hello займет несколько минут toocomplete. После запуска устройства hello перейдите toohello **консоли** вкладки. Отправьте сочетание клавиш Ctrl + Alt + Delete toolog toohello устройства. Кроме того можно точки курсора hello в окне консоли hello и нажмите клавиши Ctrl + Alt + Insert. пользователь по умолчанию Hello *StorSimpleAdmin* и пароль по умолчанию hello *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. В целях безопасности пароль администратора устройства hello истечения срока действия при первом входе hello. Все запрашиваемые toochange hello пароль.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. Введите пароль длиной не менее 8 символов. Hello пароль должен содержать 3 из 4 следующих требований: верхнем регистре, нижнем регистре, цифры и специальные символы. Повторно введите пароль tooconfirm hello его. Вы получите уведомление, изменился пароль hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. После успешного изменения пароль hello hello виртуальное устройство может быть перезагружен. Ожидание перезагрузки toocomplete hello. консоль Windows PowerShell Hello hello устройства могут отображаться вместе с индикатор хода выполнения.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. Шаги 6–8 применяются только при загрузке в среде без DHCP. Если вы работаете в среде DHCP, пропустите следующие шаги и перейдите toostep 9. Если загрузил устройства в среде не DHCP появится следующий экран приветствия.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   Настройте сети hello.
7. Используйте hello `Get-HcsIpAddress` команды toolist hello сетевых интерфейсов на виртуальное устройство. Если устройство имеет один сетевой интерфейс включен, hello интерфейсом по умолчанию имя, назначенное toothis является `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. Используйте hello `Set-HcsIpAddress` командлет tooconfigure hello сети. Пример приведен ниже.

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. После завершения начальной настройки hello и загрузки операционной системы устройства hello копирование появится текст баннера hello устройства. Запишите IP-адрес hello и hello URL-адрес в hello баннер текст toomanage hello устройства. Будет использовать этот IP адрес tooconnect toohello веб-интерфейса виртуального устройства, а полный hello локальную настройку и регистрацию.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. (Необязательно) Выполните этот шаг только в том случае, если вы развертываете устройства в hello государственных облака. Теперь будет включена hello США федеральным сведения обработки Standard (FIPS) режим на устройстве. стандарт Hello FIPS 140 определяет утвержденные для использования системами нам федеральным правительством компьютера для защиты конфиденциальных данных hello алгоритмов шифрования.

    1. tooenable hello режиме FIPS, запустите следующий командлет hello:

        `Enable-HcsFIPSMode`
    2. Перезагрузите устройство, после включения режима FIPS hello, чтобы проверки шифрования hello вступили в силу.

       > [!NOTE]
       > Можно включить или отключить режим FIPS на устройстве. Чередующиеся hello устройство между режимом FIPS и не FIPS не поддерживается.
       >
       >

Если устройство не соответствует hello минимальные требования к конфигурации, вы увидите ошибку в текст баннера hello (см. ниже). Необходимо будет конфигурации устройства toomodify hello, чтобы он имеет достаточно ресурсов toomeet hello минимальным требованиям. Затем можно перезапустить и подключить устройство toohello. Ссылки toohello минимальным требованиям к конфигурации в [шаг 1: Убедитесь, что hello основной системы минимальным требованиям виртуального устройства](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

Если во время начальной настройки hello hello локального пользовательского веб-интерфейса с помощью сталкиваются любая другая ошибка, см. следующие рабочие процессы toohello:

* Запустите диагностические тесты слишком[Устранение неполадок при настройке пользовательского интерфейса web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Создайте пакет журнала и просмотрите файлы журнала](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Дальнейшие действия
* [Deploy StorSimple Virtual Array - Set up as file server (Preview) (Развертывание виртуального массива StorSimple — настройка в качестве файлового сервера (предварительная версия))](storsimple-virtual-array-deploy3-fs-setup.md)
* [Deploy StorSimple Virtual Array – Set up your virtual device as an iSCSI server (preview) (Развертывание виртуального массива StorSimple — настройка в качестве сервера iSCSI (предварительная версия))](storsimple-virtual-array-deploy3-iscsi-setup.md)
