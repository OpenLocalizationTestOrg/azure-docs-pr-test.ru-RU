---
title: "Диспетчер моментальных снимков StorSimple aaaDeploy | Документы Microsoft"
description: "Узнайте, как toodownload и установите hello диспетчера моментальных снимков StorSimple, оснастки MMC для управления функции защиты и резервного копирования данных StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>Развертывание hello оснастки MMC диспетчера моментальных снимков StorSimple

## <a name="overview"></a>Обзор
оснастку консоли управления (MMC), которая упрощает защиту данных и управления резервным копированием в среде Microsoft Azure StorSimple является Hello диспетчера моментальных снимков StorSimple. Используя диспетчер моментальных снимков StorSimple, вы можете управлять локальным и облачным хранилищами Microsoft Azure StorSimple как полностью интегрированной системой хранения данных. Это в свою очередь позволяет упростить процессы архивации и восстановления, а также сократить затраты. 

В этом учебнике описываются требования к конфигурации, а также процедуры установки, удаления и обновления диспетчера моментальных снимков StorSimple.

> [!NOTE]
> * Нельзя использовать toomanage диспетчера моментальных снимков StorSimple Microsoft Azure StorSimple виртуальных массивов (также известный как StorSimple локального виртуального устройства).
> * Если планируется tooinstall StorSimple с обновлением 2 на устройстве StorSimple, что toodownload hello последняя версия диспетчера моментальных снимков StorSimple и установить его **перед установкой обновления StorSimple 2**. Hello последнюю версию диспетчера моментальных снимков StorSimple имеет обратную совместимость и работает с всех версий Microsoft Azure StorSimple. Если вы используете предыдущую версию hello диспетчера моментальных снимков StorSimple, необходимо будет tooupdate ИТ (необязательно toouninstall hello предыдущей версии перед установкой новой версии hello).


## <a name="storsimple-snapshot-manager-installation"></a>Установка диспетчера моментальных снимков StorSimple
Диспетчер моментальных снимков StorSimple можно установить на компьютерах под управлением операционной системы hello Windows Server 2008 R2 SP1, Windows Server 2012 или Windows Server 2012 R2. На серверах под управлением Windows 2008 R2 необходимо также установить Windows Server 2008 с пакетом обновления 1 (SP1) и Windows Management Framework 3.0.

Перед началом установки или обновления hello диспетчера моментальных снимков StorSimple оснастку для hello консоли управления (MMC), убедитесь, что это устройство Microsoft Azure StorSimple hello и хост-сервере настроены правильно.

## <a name="configure-prerequisites"></a>Настройка необходимых компонентов
Hello ниже представлен общий обзор задач конфигурации, которые необходимо выполнить перед установкой диспетчера моментальных снимков StorSimple hello. Подробные сведения о конфигурации и настройке Microsoft Azure StorSimple, включая информацию о требованиях к системе и пошаговые инструкции, см. в статье [Развертывание локального устройства StorSimple](storsimple-8000-deployment-walkthrough-u2.md).

> [!IMPORTANT]
> Прежде чем начать, просмотрите hello [контрольный список для настройки развертывания](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) и и [необходимые условия для развертывания](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) в [развертывание локального устройства StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>Перед установкой диспетчера моментальных снимков StorSimple
1. Распакуйте, присоедините и подключите устройство Microsoft Azure StorSimple hello, как описано в [установки устройства StorSimple 8100](storsimple-8100-hardware-installation.md) или [установки устройства StorSimple 8600](storsimple-8600-hardware-installation.md).
2. Убедитесь, что ваш компьютер работает под управлением одного из следующих операционных систем hello:
   
   * Windows Server 2008 R2 (на серверах под управлением Windows 2008 R2 также необходимо установить Windows Server 2008 с пакетом обновления 1 (SP1) и Windows Management Framework 3.0)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     Для виртуального устройства StorSimple hello узел должен быть виртуальной машине Microsoft Azure.
3. Убедитесь, что выполнены все требования к конфигурации hello Microsoft Azure StorSimple. Подробные сведения go слишком[необходимые условия для развертывания](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).
4. Подключите узел toohello hello устройство и выполните начальную настройку hello. Подробные сведения go слишком[шагов развертывания](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).
5. Создание тома на устройстве hello, их назначение toohello узла и убедитесь, на которых размещены hello можно подключать и использовать их. Диспетчер моментальных снимков StorSimple поддерживает следующие типы томов hello:
   
   * базовые тома;
   * простые тома;
   * динамические тома;
   * динамические зеркальные тома (RAID 1);
   * общие тома кластера.
     
     Сведения о создании томов на устройстве StorSimple hello или виртуальное устройство StorSimple go слишком[шаг 6: Создание тома](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)в [развертывание локального устройства StorSimple](storsimple-8000-deployment-walkthrough-u2.md).

## <a name="install-a-new-storsimple-snapshot-manager"></a>Установка нового диспетчера моментальных снимков StorSimple
Перед установкой диспетчера моментальных снимков StorSimple, убедитесь, что hello тома, созданные на устройстве StorSimple hello или виртуальное устройство StorSimple подключен, инициализации и форматируются согласно [Настройка необходимых компонентов](#configure-prerequisites).

> [!IMPORTANT]
> * Для виртуального устройства StorSimple hello узел должен быть виртуальной машине Microsoft Azure. 
> * узел Hello, должен работать под управлением Windows 2008 R2, Windows Server 2012 или Windows Server 2012 R2. Если сервер работает под управлением Windows Server 2008 R2, необходимо также установить Windows Server 2008 с пакетом обновления 1 (SP1) и Windows Management Framework 3.0.
> * Перед подключением tooStorSimple hello устройства диспетчера моментальных снимков необходимо настроить подключение iSCSI от устройства StorSimple toohello hello узла.

Выполните эти шаги toocomplete установка диспетчера моментальных снимков StorSimple. При установке обновления перейдите слишком[обновление или переустановка диспетчера моментальных снимков StorSimple](#upgrade-or-reinstall-storsimple-snapshot-manager).

* Шаг 1. Установка диспетчера моментальных снимков StorSimple 
* Шаг 2: Подключите устройство tooa диспетчера моментальных снимков StorSimple 
* Шаг 3: Проверка устройства toohello подключения hello 

### <a name="step-1-install-storsimple-snapshot-manager"></a>Шаг 1. Установка диспетчера моментальных снимков StorSimple
Используйте следующие шаги tooinstall диспетчера моментальных снимков StorSimple hello.

#### <a name="tooinstall-storsimple-snapshot-manager"></a>tooinstall диспетчера моментальных снимков StorSimple
1. Загрузите программное обеспечение диспетчера моментальных снимков StorSimple hello (go слишком[диспетчера моментальных снимков StorSimple](https://www.microsoft.com/download/details.aspx?id=44220) в центре загрузки Майкрософт hello) и сохраните его на узле hello.
2. В проводнике щелкните правой кнопкой мыши hello сжатую папку и нажмите кнопку **извлечь все**.
3. В hello **извлечения сжатых ZIP-папок** окна в hello **выберите конечную папку и извлеките файлы** введите или укажите путь toohello, куда извлечь toobe toofile.
   
    > [!IMPORTANT]
    > Необходимо установить диспетчер моментальных снимков StorSimple на hello диска C:.
    
4. Выберите hello **Показать извлеченные файлы после завершения** флажок и нажмите кнопку **извлечения**.
   
    ![Диалоговое окно "Извлечение файлов"](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. По завершении извлечения hello откроется целевая папка hello. Дважды щелкните значок установки приложения hello, который отображается в папке назначения hello.
6. Здравствуйте, когда **Установка успешно завершена** появится сообщение, нажмите кнопку **закрыть**. На рабочем столе должен появиться значок диспетчера моментальных снимков StorSimple hello.
   
    ![Значок рабочего стола](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>Шаг 2: Подключите устройство tooa диспетчера моментальных снимков StorSimple
Используйте следующие шаги tooconnect устройства диспетчера моментальных снимков StorSimple tooa StorSimple hello.

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>устройства диспетчера моментальных снимков StorSimple tooa tooconnect
1. Щелкните значок диспетчера моментального снимка StorSimple hello на рабочем столе. Откроется окно диспетчера моментальных снимков StorSimple Hello. окно Hello содержит **области** области **результатов** области и **действия** области. 
   
    ![Пользовательский интерфейс диспетчера моментальных снимков StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * Hello **область** область (hello слева) содержит список узлов в древовидной структуры. Можно разворачивать некоторые узлы tooselect представления или узел связанные toothat конкретных данных. Щелкните значок tooexpand hello стрелку или свернуть узел. Щелкните правой кнопкой мыши элемент в hello **область** toosee панели список доступных действий для этого элемента.
   * Hello **результатов** область (hello центральная панель) содержит подробные сведения об узле hello, представление или данные, выбранные в hello **область** области.
   * Hello **действия** области перечислены hello операций, которые можно выполнять на узле hello, представление или данные, выбранные в hello **область** области.
     
     Полное описание пользовательского интерфейса диспетчера моментальных снимков StorSimple hello см. в разделе [пользовательский интерфейс диспетчера моментальных снимков StorSimple](storsimple-use-snapshot-manager.md).
2. В hello **область** панели, щелкните правой кнопкой мыши hello **устройств** , а затем щелкните **Настройка устройства**. Hello **настроить устройство** откроется диалоговое окно.
   
    ![Настройка устройства](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. В hello **устройства** перечислены поля, выберите hello IP-адрес Microsoft Azure StorSimple hello и виртуальное устройство. В hello **пароль** текстовое поле, введите пароль диспетчера моментальных снимков StorSimple hello, созданный для устройства hello в hello портал Azure. Нажмите кнопку **ОК**.
4. Диспетчер моментальных снимков StorSimple ищет устройство hello. При наличии hello устройства диспетчера моментальных снимков StorSimple добавит подключение. Вы можете [проверка устройства toohello подключения hello](#to-verify-the-connection) tooconfirm, hello подключения был успешно добавлен.
   
    Если устройство hello недоступна для какой-либо причине, диспетчера моментальных снимков StorSimple возвращает сообщение об ошибке. Нажмите кнопку **ОК** tooclose hello сообщение об ошибке, а затем нажмите кнопку **отменить** tooclose hello **настроить устройство** диалоговое окно.
5. При подключении устройства tooa, диспетчера моментальных снимков StorSimple импортирует каждой группы томов, настроенные для данного устройства, при условии, что hello группы томов имеют связанные резервные копии. Группы томов, у которых нет связанных резервных копий, не импортируются. Кроме того, не импортируются политики архивации, созданные для группы томов. toosee Здравствуйте импортированные группы, щелкните правой кнопкой мыши самый верхний hello **группы томов** узел в hello **область** панели и нажмите **переключить импортированные группы**.

### <a name="step-3-verify-hello-connection-toohello-device"></a>Шаг 3: Проверка устройства toohello подключения hello
Используйте следующие шаги tooverify, что диспетчер моментальных снимков StorSimple — toohello подключенного устройства StorSimple hello.

#### <a name="tooverify-hello-connection"></a>подключение tooverify hello
1. В hello **область** панели щелкните hello **устройств** узла.
   
    ![Состояние устройства диспетчера моментальных снимков StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. Проверьте hello **результатов** панели: 
   
   * Если появляется зеленый индикатор на значок устройства hello и **доступно** отображается в hello **состояние** столбец, затем hello устройства подключен. 
   * Если красный индикатор на значок устройства hello и недоступно в hello **состояние** столбец, затем hello устройства не подключены. 
   * Если **обновление** отображается в hello **состояние** столбца, а затем диспетчера моментальных снимков StorSimple извлекает группы томов и связанные резервные копии для подключенного устройства.

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>Обновление или переустановка диспетчера моментальных снимков StorSimple
Диспетчер моментальных снимков StorSimple следует полностью удалить перед обновлением или переустановить программное обеспечение hello. 

Перед переустановкой диспетчера моментальных снимков StorSimple, резервное копирование hello существующей базы данных диспетчера моментальных снимков StorSimple на главном компьютере hello. Это экономит hello резервного копирования политик и сведения о конфигурации, чтобы эти данные могут быть легко восстановлены из резервной копии.

При обновлении или переустановке диспетчера моментальных снимков StorSimple выполните следующие действия.

* Шаг 1. Удаление диспетчера моментальных снимков StorSimple 
* Шаг 2: Резервное копирование базы данных диспетчера моментальных снимков StorSimple hello 
* Шаг 3: Переустановка диспетчера моментальных снимков StorSimple и восстановление базы данных hello 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>Шаг 1. Удаление диспетчера моментальных снимков StorSimple
Используйте следующие шаги toouninstall диспетчера моментальных снимков StorSimple hello.

#### <a name="toouninstall-storsimple-snapshot-manager"></a>toouninstall диспетчера моментальных снимков StorSimple
1. На главном компьютере hello, откройте hello **панели управления**, нажмите кнопку **программы**, а затем нажмите кнопку **программы и компоненты**.
2. Hello левой панели щелкните **удаление или изменение программы**.
3. Щелкните правой кнопкой мыши **StorSimple Snapshot Manager**, а затем выберите пункт **Удалить**.
4. Запустится программа установки диспетчера моментальных снимков StorSimple hello. Щелкните **Изменение установки**, а затем нажмите кнопку **Удалить**.
   
   > [!NOTE]
   > Если есть в фоновом режиме hello запущены процессы MMC, например диспетчера моментальных снимков StorSimple или Управление дисками, hello удаления произойдет сбой и вы получите tooclose сообщение все экземпляры MMC, прежде чем попытку toouninstall hello программы. Выберите **автоматически закрывать приложения и выполнить их после установки toorestart**, а затем нажмите кнопку **ОК**.
   > 
   > 
5. При удалении hello завершения **Установка успешно завершена** появится сообщение. Нажмите кнопку **Закрыть**

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>Шаг 2: Резервное копирование базы данных диспетчера моментальных снимков StorSimple hello
Используйте следующие шаги toocreate hello и сохранить копию базы данных диспетчера моментальных снимков StorSimple hello.

#### <a name="tooback-up-hello-database"></a>tooback копирование базы данных hello
1. Остановите hello служба управления Microsoft StorSimple:
   
   1. Запустите диспетчер серверов.
   2. На hello мониторинга диспетчера серверов на hello **средства** последовательно выберите пункты **службы**.
   3. На hello **службы** выберите **служба управления Microsoft StorSimple**.
   4. В hello правой панели в разделе **служба управления Microsoft StorSimple**, нажмите кнопку **остановить службу hello**.
      
        ![Остановка службы диспетчера StorSimple устройство hello](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. Обзор tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData — это скрытая папка.
  
3. Найти XML-файл каталога hello, копирование файла hello и сохранить hello скопировать в безопасном месте или в облаке hello.
   
    ![Файл каталога резервных копий StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. Перезапустите hello служба управления Microsoft StorSimple: 
   
   1. На hello мониторинга диспетчера серверов на hello **средства** последовательно выберите пункты **службы**.
   2. На hello **службы** страницу, выберите hello **службы управления Microsoft StorSimple**e.
   3. В hello правой панели в разделе **служба управления Microsoft StorSimple**, нажмите кнопку **перезапустите службу hello**. 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>Шаг 3: Переустановка диспетчера моментальных снимков StorSimple и восстановление базы данных hello
tooreinstall диспетчера моментальных снимков StorSimple, следуйте указаниям hello [Установка нового диспетчера моментальных снимков StorSimple](#install-a-new-storsimple-snapshot-manager). Затем с помощью hello следующая база данных диспетчера моментальных снимков StorSimple hello toorestore процедуры.

#### <a name="toorestore-hello-database"></a>База данных toorestore hello
1. Остановите hello служба управления Microsoft StorSimple:
   
   1. Запустите диспетчер серверов.
   2. На hello мониторинга диспетчера серверов на hello **средства** последовательно выберите пункты **службы**.
   3. На hello **службы** выберите **служба управления Microsoft StorSimple**.
   4. В hello правой панели в разделе **служба управления Microsoft StorSimple**, нажмите кнопку **остановить службу hello**.
2. Обзор tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   
   > [!NOTE]
   > ProgramData — это скрытая папка.
   > 
   > 
3. Удалите XML-файл каталога hello и замените его ранее сохраненной версией hello.
4. Перезапустите hello служба управления Microsoft StorSimple: 
   
   1. На hello мониторинга диспетчера серверов на hello **средства** последовательно выберите пункты **службы**.
   2. На hello **службы** выберите **служба управления Microsoft StorSimple**.
   3. В hello правой панели в разделе **служба управления Microsoft StorSimple**, нажмите кнопку **перезапустите службу hello**.

## <a name="next-steps"></a>Дальнейшие действия
* toolearn более о диспетчера моментальных снимков StorSimple, перейдите в слишком[диспетчера моментальных снимков StorSimple?](storsimple-what-is-snapshot-manager.md).
* toolearn Дополнительные сведения о пользовательский интерфейс диспетчера моментальных снимков StorSimple hello, go слишком[пользовательский интерфейс диспетчера моментальных снимков StorSimple](storsimple-use-snapshot-manager.md).
* toolearn Подробнее об использовании диспетчера моментальных снимков StorSimple, перейдите в слишком[tooadminister диспетчера моментальных снимков StorSimple используйте решения StorSimple](storsimple-snapshot-manager-admin.md).

