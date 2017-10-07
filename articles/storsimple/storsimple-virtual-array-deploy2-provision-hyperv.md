---
title: "aaaProvision StorSimple Virtual Array в Hyper-V | Документы Microsoft"
description: "Второе руководство по развертыванию виртуального массива StorSimple посвящено подготовке виртуального массива в Hyper-V."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a>Развертывание виртуального массива StorSimple — подготовка в Hyper-V
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a>Обзор
В данном учебнике как tooprovision StorSimple Virtual Array в системе узла, под управлением Hyper-V Windows Server 2012 R2, Windows Server 2012 или Windows Server 2008 R2. Эта статья относится развертывания toohello StorSimple виртуальных массивов в портале Azure и государственных облако Microsoft Azure.

Требуется tooprovision правами администратора и настройка виртуального массива. Hello подготовки и базовая установка может занять около 10 минут toocomplete.

## <a name="provisioning-prerequisites"></a>Предварительные требования к подготовке
Здесь вы найдете tooprovision hello необходимые компоненты виртуального массива в системе узла, под управлением Hyper-V Windows Server 2012 R2, Windows Server 2012 или Windows Server 2008 R2.

### <a name="for-hello-storsimple-device-manager-service"></a>Для hello службой диспетчера устройств StorSimple
Перед тем как начать, убедитесь в следующем.

* Выполнены все действия hello в [портал hello подготовки для StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).
* Загруженный образ виртуального массива hello для Hyper-V с hello портал Azure. Дополнительные сведения см. в разделе **Step 3: образ виртуального массива hello загрузки** из [подготовки портала hello руководство StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).

  > [!IMPORTANT]
  > Hello программного обеспечения hello StorSimple Virtual Array может использоваться только с hello службы диспетчера StorSimple устройство.
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a>Для hello StorSimple Virtual Array
Перед развертыванием виртуального массива выполните указанные ниже условия.

* У вас есть доступ tooa компьютерной системе под управлением Hyper-V в Windows Server 2008 R2 или более поздней версии, могут быть используется tooa подготавливать устройства.
* Hello система узла — может toodedicate hello следующие ресурсы tooprovision виртуального массива:

  * Не менее 4 ядер.
  * Не менее 8 ГБ ОЗУ. Если планируется tooconfigure hello виртуального массива как файловый сервер, 8 ГБ поддерживает менее 2 миллионов файлов. Необходимо 2-4 миллиона toosupport файла по 16 ГБ ОЗУ.
  * Один сетевой интерфейс.
  * Виртуальный диск данных размером 500 ГБ.

### <a name="for-hello-network-in-hello-datacenter"></a>Для hello сети в центре обработки данных hello
Прежде чем начать, проверьте сетевые требования toodeploy StorSimple Virtual Array hello и соответствующим образом настроить hello сети центра обработки данных. Дополнительные сведения см. в разделе [Требования к сети](storsimple-ova-system-requirements.md#networking-requirements).

## <a name="step-by-step-provisioning"></a>Пошаговая подготовка
tooprovision и подключения tooa виртуального массива, необходимо hello tooperform следующие шаги:

1. Убедитесь в наличии достаточных ресурсов toomeet hello минимальное виртуального массива требования к hello компьютерной системе.
2. Подготовьте виртуальный массив в низкоуровневой оболочке.
3. Запуск виртуального массива hello и получение hello IP-адрес.

Каждое из этих действий описан в следующих разделах hello.

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a>Шаг 1: Убедитесь, что hello главной системы требованиям минимальное виртуального массива
toocreate виртуального массива, необходимо:

* роль Hyper-V Hello установлен на Windows Server 2012 R2, Windows Server 2012 или Windows Server 2008 R2 SP1.
* Microsoft Hyper-V Manager на клиенте Microsoft Windows подключенного toohello узла.

Убедитесь, что этот hello базового оборудования (системы узла), на котором создается виртуальный массив hello — может toodedicate hello, следующие ресурсы tooyour виртуального массива:

* Не менее 4 ядер.
* Не менее 8 ГБ ОЗУ. Если планируется tooconfigure hello виртуального массива как файловый сервер, 8 ГБ поддерживает менее 2 миллионов файлов. Необходимо 2-4 миллиона toosupport файла по 16 ГБ ОЗУ.
* Один сетевой интерфейс.
* Виртуальный диск размером 500 ГБ для системных данных.

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a>Шаг 2. Подготовка виртуального массива в низкоуровневой оболочке
Выполните следующие шаги tooprovision устройство в вашей низкоуровневой оболочки hello.

#### <a name="tooprovision-a-virtual-array"></a>tooprovision виртуальных массивов
1. На узле Windows Server скопируйте hello образ виртуального массива tooa локального диска. Загрузить этот образ (VHD или VHDX) через портал Azure hello. Запишите расположение hello, где сохранен hello изображения с помощью этого образа позже в процедуре hello.
2. Откройте **диспетчер сервера**. В hello правом верхнем углу щелкните **средства** и выберите **диспетчера Hyper-V**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   Если вы используете Windows Server 2008 R2, откройте hello диспетчера Hyper-V. В диспетчере сервера щелкните **Роли > Hyper-V > Диспетчер Hyper-V**.
3. В **диспетчера Hyper-V**в панель "область" hello, щелкните правой кнопкой мыши в контекстное меню hello tooopen системы узла и нажмите кнопку **New** > **виртуальной машины**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. На hello **перед началом** страница приветствия мастера создания виртуальной машины, нажмите кнопку **Далее**.
5. На hello **укажите имя и расположение** укажите **имя** виртуального массива. Щелкните **Далее**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. На hello **укажите поколение** страницы, выберите тип образа устройства hello и нажмите кнопку **Далее**. Эта страница не отобразится, если вы используете Windows Server 2008 R2.

   * Выберите **Поколение 2** , если в скачали VHDX-файл образа для Windows Server 2012 или более поздней версии.
   * Выберите **Поколение 1** , если в скачали VHD-файл образа для Windows Server 2008 R2 или более поздней версии.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. На hello **выделить память** укажите **память при запуске** из по крайней мере **8192 МБ**, не Включение динамической памяти, а затем выберите **Далее**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. На hello **Настройка сети** , укажите hello виртуальный коммутатор, подключенный toohello Интернета и выберите **Далее**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. На hello **подключить виртуальный жесткий диск** выберите **использовать существующий виртуальный жесткий диск**, укажите расположение hello образа виртуального массива hello (vhdx или VHD) и нажмите кнопку **Далее**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. Просмотрите hello **Сводка** и нажмите кнопку **Готово** toocreate hello виртуальной машины.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. минимальные требования hello toomeet необходимо 4 ядра. tooadd 4 виртуальных процессоров, выберите системе узла в hello **диспетчера Hyper-V** окна. В правой области hello hello списке **виртуальные машины**, найдите hello виртуальной машины вы только что создали. Выберите и щелкните правой кнопкой мыши имя компьютера hello и выберите **параметры**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. На hello **параметры** hello левой панели нажмите **процессора**. В hello на правой панели установите **число виртуальных процессоров** too4 (или более). Нажмите кнопку **Применить**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. toomeet hello минимальным требованиям, необходимо также tooadd 500 ГБ виртуальный диск данных. В hello **параметры** страницы:

    1. Выберите в левой области hello **SCSI-контроллер**.
    2. Выберите в правой области hello **жесткий диск,** и нажмите кнопку **добавить**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. На hello **жесткий диск** страницу, выберите hello **виртуальный жесткий диск** и нажмите кнопку **New**. Hello **мастера создания виртуального жесткого диска** запускает.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. На hello **перед началом** страница приветствия мастера создания виртуального жесткого диска, нажмите кнопку **Далее**.
16. На hello **страницы Выбор формата диска**, оставьте вариант по умолчанию hello **VHDX** формат. Щелкните **Далее**. Если вы используете Windows Server 2008 R2, то этот экран не отображается.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. На hello **страницы выберите тип диска**, задайте тип виртуального жесткого диска как **динамически расширяемые** (рекомендуется). **Фиксированный размер** диск будет работать, но toowait может потребоваться длительное время. Рекомендуется не использовать hello **Differencing** параметр. Щелкните **Далее**. В Windows Server 2012 R2 и Windows Server 2012 **динамически расширяемые** — параметр по умолчанию hello, а в Windows Server 2008 R2 — по умолчанию hello **фиксированный размер**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. На hello **укажите имя и расположение** укажите **имя** и **расположение** (можно просмотреть tooone) для диска данных hello. Щелкните **Далее**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. На hello **Настройка диска** страницы приветствия выберите параметр **создать пустой виртуальный жесткий диск** и укажите размер hello как **500 ГБ** (или более). Хотя 500 ГБ hello минимальным требованиям, всегда можно подготовить диск большего размера. Обратите внимание, что вы не может увеличивать и уменьшать один раз подготовленного диска hello. Дополнительные сведения о hello размер диска tooprovision, можно узнать в разделе размера hello в hello [обеспечению](storsimple-ova-best-practices.md). Щелкните **Далее**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. На hello **Сводка** , просмотрите сведения об hello данных виртуального диска и, если условие удовлетворено, нажмите кнопку **Готово** toocreate hello диска. Закрывает мастер Hello и виртуальный жесткий диск добавляется tooyour машины.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. Вернуть toohello **параметры** страницы. Нажмите кнопку **ОК** tooclose hello **параметры** страницы и возврата окно диспетчера tooHyper-V.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a>Шаг 3: Запуск виртуальных массивов hello и получение IP-адреса hello
Выполните следующие шаги toostart hello виртуального массива и подключения tooit.

#### <a name="toostart-hello-virtual-array"></a>виртуальный массив toostart hello
1. Запуск виртуального массива hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. После запуска hello устройства, выберите устройство hello, щелкните правой кнопкой мыши и выберите **Connect**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. Вы можете иметь toowait 5 – 10 минут для hello устройства toobe готовности. Сообщение о состоянии отображаются в tooindicate hello hello консоли выполняется. После устройств hello перейти слишком**действия**. Нажмите клавишу `Ctrl + Alt + Delete` toolog toohello виртуального массива. пользователь по умолчанию Hello *StorSimpleAdmin* и пароль по умолчанию hello *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. В целях безопасности пароль администратора устройства hello истечения срока действия при первом входе hello. Все запрашиваемые toochange hello пароль.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   Введите пароль длиной не менее 8 символов. Hello пароль должен соответствовать по крайней мере 3 из следующих требований 4 hello: верхнем регистре, нижнем регистре, цифры и специальные символы. Повторно введите пароль tooconfirm hello его. Вы будете оповещены, изменился пароль hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. Если hello пароль успешно изменен, hello виртуального массива может перезагрузиться. Дождитесь hello toostart устройства.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    консоль Windows PowerShell Hello hello устройства отображается вместе с индикатор хода выполнения.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. Шаги 6–8 применяются только при загрузке в среде без DHCP. Если вы работаете в среде DHCP, пропустите следующие шаги и перейдите toostep 9. Если загрузил устройства в среде не DHCP появится следующий экран приветствия.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    Настройте сети hello.
7. Используйте hello `Get-HcsIpAddress` команды toolist hello сетевых интерфейсов на виртуальных массива. Если устройство имеет один сетевой интерфейс включен, hello интерфейсом по умолчанию имя, назначенное toothis является `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. Используйте hello `Set-HcsIpAddress` командлет tooconfigure hello сети. См. следующий пример hello.

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. После завершения начальной настройки hello и загрузки операционной системы устройства hello копирование появится текст баннера hello устройства. Запишите IP-адрес hello и hello URL-адрес в hello баннер текст toomanage hello устройства. Используйте этот IP адрес tooconnect toohello веб-Интерфейсе виртуального массива, а полный hello локальную настройку и регистрацию.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. (Необязательно) Выполните этот шаг только в том случае, если вы развертываете устройства в hello государственных облака. Теперь будет включена hello США федеральным сведения обработки Standard (FIPS) режим на устройстве. стандарт Hello FIPS 140 определяет утвержденные для использования системами нам федеральным правительством компьютера для защиты конфиденциальных данных hello алгоритмов шифрования.

    1. tooenable hello режиме FIPS, запустите следующий командлет hello:

        `Enable-HcsFIPSMode`
    2. Перезагрузите устройство, после включения режима FIPS hello, чтобы проверки шифрования hello вступили в силу.

       > [!NOTE]
       > Можно включить или отключить режим FIPS на устройстве. Чередующиеся hello устройство между режимом FIPS и не FIPS не поддерживается.
       >
       >

Если устройство не соответствует hello минимальные требования к конфигурации, можно увидеть hello следующая ошибка в текст баннера hello (см. ниже). Измените конфигурацию устройства hello, hello компьютер имеет достаточно ресурсов toomeet hello минимальным требованиям. Затем можно перезапустить и подключить устройство toohello. Ссылки toohello минимальным требованиям к конфигурации в [шаг 1:, hello компьютерной системе требованиям минимальное виртуального массива](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

Если во время начальной настройки hello hello локального пользовательского веб-интерфейса с помощью сталкиваются любая другая ошибка, см. следующие рабочие процессы toohello:

* Запустите диагностические тесты слишком[Устранение неполадок при настройке пользовательского интерфейса web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Создайте пакет журнала и просмотрите файлы журнала](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Дальнейшие действия
* [Deploy StorSimple Virtual Array - Set up as file server (Preview) (Развертывание виртуального массива StorSimple — настройка в качестве файлового сервера (предварительная версия))](storsimple-virtual-array-deploy3-fs-setup.md)
* [Deploy StorSimple Virtual Array – Set up your virtual device as an iSCSI server (preview) (Развертывание виртуального массива StorSimple — настройка в качестве сервера iSCSI (предварительная версия))](storsimple-virtual-array-deploy3-iscsi-setup.md)
