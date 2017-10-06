---
title: "устройство StorSimple aaaDeploy государственных портала | Документы Microsoft"
description: "Описывает этапы hello и рекомендации для службы на портале Azure для государственных hello и развертывание устройство StorSimple с обновлением 2 hello."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 5277538c-797e-4e8e-b613-31b5c10cf5a9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/16/2016
ms.author: v-sharos
ms.openlocfilehash: 68104988595341a49a87d78c4a9b1d2675759c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal-update-2"></a>Развертывание устройства StorSimple в локальной среде в hello портала государственных организаций (обновление 2)
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>Обзор
Вас приветствует tooMicrosoft развертывания устройства Azure StorSimple. Эти руководства по развертыванию применить toohello StorSimple серии 8000 выполняющегося 2 обновления программного обеспечения в hello государственных портала Azure. В этой серии учебников описывается контрольный список настройки, список предварительных требований к конфигурации и подробное пошаговое руководство по настройке устройства StorSimple.

Hello сведения в этих учебниках предполагается, что проверены hello меры предосторожности и распаковать, racked и подключить кабели устройства StorSimple. Если по-прежнему требуется tooperform тех задач, начните с проверки hello [меры предосторожности](storsimple-safety.md). Следуйте инструкциям для конкретного устройства hello стойку toounpack и подключите к устройству.

* [Распаковка, монтаж в стойку и подключение кабелей к устройству 8100](storsimple-8100-hardware-installation.md)
* [Распаковка, монтаж в стойку и подключение кабелей к устройству 8600](storsimple-8600-hardware-installation.md)

Вам потребуется администратора привилегии toocomplete hello процесса установки и настройки. Рекомендуется просмотреть hello контрольный список для настройки перед началом. Hello развертывания и конфигурации может занять некоторое время toocomplete.

> [!NOTE]
> сведения о развертывании StorSimple Hello опубликованы на веб-сайте Microsoft Azure hello применяется tooStorSimple 8000 ряда только для устройств. Полные сведения об устройствах серии hello 7000 см. в: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Дополнительные сведения о развертывании серии 7000, см hello [StorSimple краткое руководство по системе](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Шаги по развертыванию
Выполните эти действия tooconfigure устройства StorSimple и подключите его tooyour в службе StorSimple Manager. В дополнение к этому toohello обязательные действия, существуют дополнительные шаги и процедуры, что может потребовать toocomplete во время развертывания hello. Hello пошаговые инструкции по развертыванию указывают, когда следует выполнять каждый из этих необязательных действий.

| Шаг | Description (Описание) |
| --- | --- |
| **ПРЕДВАРИТЕЛЬНЫЕ ТРЕБОВАНИЯ** |Они должны toobe завершена при подготовке к развертыванию предстоящих hello. |
| [Контрольный список конфигурации развертывания](#deployment-configuration-checklist) |Используйте этот контрольный список toogather и записи сведения о предыдущих tooand во время развертывания hello. |
| [Предварительные условия для развертывания](#deployment-prerequisites) |Эти проверки, hello среда готова к развертыванию. |
|  | |
| **ПОШАГОВОЕ РАЗВЕРТЫВАНИЕ** |Эти действия являются обязательным toodeploy устройства StorSimple в рабочей среде. |
| [Шаг 1. Создание новой службы](#step-1-create-a-new-service) |Настройте облачное управление и хранение для устройства StorSimple. *При наличии существующей службы для других устройств StorSimple пропустите этот шаг*. |
| [Шаг 2: Получение ключа регистрации службы hello](#step-2-get-the-service-registration-key) |Использование этого ключа tooregister и подключите устройство StorSimple со службой управления hello. |
| [Шаг 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Подключение к сети tooyour устройство hello и зарегистрируйте его в Azure toocomplete hello установки с помощью службы управления hello. |
| [Шаг 4: Выполнение hello минимальной настройки устройства](#step-4-complete-minimum-device-setup) </br>Необязательно: обновление устройства StorSimple. |Используйте программу установки устройства hello toocomplete в службе управления hello и включите ее tooprovide хранилища. |
| [Шаг 5. Создание контейнера томов](#step-5-create-a-volume-container) |Создание контейнера тома tooprovision. Контейнер томов имеет учетную запись хранения, пропускной способности и параметры шифрования для всех томов hello, содержащиеся в нем. |
| [Шаг 6. Создание тома](#step-6-create-a-volume) |Подготовка хранилища томов на устройстве StorSimple hello для серверов. |
| [Шаг 7. Подключение, инициализация и форматирование тома](#step-7-mount-initialize-and-format-a-volume) </br>Необязательно: настройка MPIO. |Подключение устройства hello хранилища iSCSI toohello серверов. При необходимости настройте tooensure MPIO, что серверы может выдержать связи, сети и интерфейс сбоя. |
| [Шаг 8. Создание резервной копии](#step-8-take-a-backup) |Настройка вашего tooprotect политику резервного копирования данных |
|  | |
| **ПРОЧИЕ ПРОЦЕДУРЫ** |При развертывании решения может потребоваться toorefer toothese процедуры. |
| [Настройте новую учетную запись хранилища для службы hello](#configure-a-new-storage-account-for-the-service) | |
| [Использовать PuTTY tooconnect toohello последовательной консоли устройства](#use-putty-to-connect-to-the-device-serial-console) | |
| [Проверка наличия обновлений и их применение](#scan-for-and-apply-updates) | |
| [Получение IQN узла Windows Server hello](#get-the-iqn-of-a-windows-server-host) | |
| [Создание резервной копии вручную](#create-a-manual-backup) | |
| [Настройка MPIO](#configure-mpio) | |

## <a name="deployment-configuration-checklist"></a>Контрольный список конфигурации развертывания
Прежде чем развертывать устройства StorSimple, необходимо будет toocollect tooconfigure сведения hello, программного обеспечения на устройстве. Некоторые из этих сведений заранее подготовка позволит упростить процесс hello hello устройство StorSimple в среде развертывания. Загрузить и использовать сведения о конфигурации toonote hello этот контрольный список при развертывании устройства.  

[Скачать контрольный список настройки развертывания устройства StorSimple](http://www.microsoft.com/download/details.aspx?id=49159)  

## <a name="deployment-prerequisites"></a>Предварительные условия для развертывания
Привет, в следующих разделах объясняется hello предварительные требования конфигурации для службы диспетчера StorSimple и устройства StorSimple.

### <a name="for-hello-storsimple-manager-service"></a>Для hello службы диспетчера StorSimple
Перед тем как начать, убедитесь в следующем.

* Имеется учетная запись Майкрософт и данные для доступа к ней.
* Имеется учетная запись хранения Microsoft Azure и данные для доступа к ней.
* Для hello в службе StorSimple Manager включены подписки Microsoft Azure. Необходимо приобрести подписку по hello [соглашение Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* У вас есть доступ программное обеспечение эмуляции tooterminal например PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Для устройства hello в центре обработки данных hello
Перед настройкой устройства hello, убедитесь, что:

* Устройство должно быть полностью распаковано, установлено в стойку. Кроме того, к нему должны быть подключены все кабели питания, сети и последовательного доступа, как описано в разделах:
  
  * [Распаковка, монтаж в стойку и подключение кабелей к устройству 8100](storsimple-8100-hardware-installation.md)
  * [Распаковка, монтаж в стойку и подключение кабелей к устройству 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Для hello сети в центре обработки данных hello
Перед тем как начать, убедитесь в следующем.

* Hello порты в брандмауэре центра обработки данных, tooallow открыт для трафика iSCSI и облаку описаны в [требования к сети для устройства StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>ПОШАГОВОЕ РАЗВЕРТЫВАНИЕ
Используйте следующие пошаговые инструкции toodeploy hello устройства StorSimple в центре обработки данных hello.

## <a name="step-1-create-a-new-service"></a>Шаг 1. Создание новой службы
Служба Диспетчера StorSimple может управлять несколькими устройствами StorSimple. Выполните следующие шаги toocreate новый экземпляр службы StorSimple Manager hello hello.

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> Если вы не включили hello автоматическое создание учетной записи хранилища в службе, необходимо будет toocreate по крайней мере одну учетную запись хранения после успешного создания службы. Эта учетная запись хранения будет использоваться при создании контейнера томов.
> 
> * Если не была автоматически создана учетная запись хранения, перейдите в слишком[настроить новую учетную запись хранилища для службы hello](#configure-a-new-storage-account-for-the-service) подробные инструкции.
> * Если вы включили hello автоматическое создание учетной записи хранилища, перейдите в слишком[шаг 2: ключ регистрации службы hello Get](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Шаг 2: Получение ключа регистрации службы hello
После hello в службе StorSimple Manager запущен и работает, потребуется ключ регистрации службы tooget hello. Этот ключ используется tooregister и подключения службы toohello устройства StorSimple.

Выполнение шагов в hello портала государственных hello.

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Шаг 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple
Используйте Windows PowerShell для StorSimple toocomplete hello начальной настройки устройства StorSimple, как описывается в hello после процедуры. Вам потребуется toocomplete программное обеспечение эмуляции терминала toouse этот шаг. Дополнительные сведения см. в разделе [последовательной консоли устройства toohello использование PuTTY tooconnect](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Шаг 4. Выполнение минимальной настройки устройства
Для hello минимальную настройку устройства StorSimple вы должны:

* Настройка hello дополнительного DNS-сервера.
* Включите последовательный интерфейс iSCSI хотя бы на одном сетевом интерфейсе.
* Назначьте фиксированные IP-адреса контроллеров tooboth hello.

Выполните следующие шаги в hello портала государственных toocomplete hello минимальной настройки устройства hello.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Шаг 5. Создание контейнера томов
Контейнер томов имеет учетную запись хранения, пропускной способности и параметры шифрования для всех томов hello, содержащиеся в нем. Вам потребуется toocreate контейнер тома, прежде чем приступить к подготовке томов на устройстве StorSimple.

Выполнение шагов в toocreate портала государственных hello контейнер томов hello.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Шаг 6. Создание тома
После создания контейнера тома, можно подготовить том хранилища на устройстве StorSimple hello для серверов. Выполнение шагов в toocreate портала государственных hello тома hello.

> [!IMPORTANT]
> Azure StorSimple может создать только тома с тонкой подготовкой.  В системе Azure StorSimple вы не можете создавать полностью или частично выделяемые тома.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Шаг 7. Подключение, инициализация и форматирование тома
Выполните следующие шаги на вашем узле Windows Server.

> [!IMPORTANT]
> * Hello высокую доступность решения StorSimple рекомендуется настроить MPIO на предыдущий tooconfiguring iSCSI узлов серверов (необязательно). Конфигурации MPIO на серверах узла убедитесь, что серверы hello может выдержать связи, сети или интерфейса.
> * MPIO и iSCSI инструкции по установке и конфигурации на узле Windows Server, перейдите слишком[Настройка MPIO для устройства StorSimple](storsimple-configure-mpio-windows-server.md). Они также будут включать toomount действия hello, инициализация и форматирование томов StorSimple.
> * MPIO и iSCSI инструкции по установке и конфигурации на узле Linux, перейдите слишком[Настройка MPIO для узла StorSimple Linux](storsimple-configure-mpio-on-linux.md)
> 
> 

Если решить tooconfigure MPIO, выполните следующие шаги toomount hello, инициализация и форматирование тома StorSimple на узле Windows Server.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Шаг 8. Создание резервной копии
Резервные копии обеспечивают защиту состояния томов до определенной точки во времени и улучают возможности восстановления, одновременно снижая время восстановления. Устройство StorSimple позволяет создавать резервные копии двух типов: локальные и облачные моментальные снимки. Каждый из этих типов резервных копий может создаваться **по расписанию** или **вручную**.

Выполните следующие шаги в toocreate портала государственных hello архивации по расписанию hello.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

Резервное копирование вручную можно выполнить в любое время. Для процедур go слишком[создать вручную резервную копию](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Настройте новую учетную запись хранилища для службы hello
Это необязательный шаг должны tooperform только в том случае, если вы не включили hello автоматическое создание учетной записи хранилища в службе. Учетную запись хранения Microsoft Azure является обязательным toocreate контейнера томов StorSimple.

При необходимости toocreate учетную запись хранилища Azure в другом регионе. в разделе [об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md) пошаговые инструкции.

Выполните следующие шаги в hello портала государственных на hello hello **в службе StorSimple Manager** страницы.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Использовать PuTTY tooconnect toohello последовательной консоли устройства
tooWindows tooconnect PowerShell для StorSimple, необходимо toouse программное обеспечение эмуляции терминала, например PuTTY. Можно использовать PuTTY при доступе к hello устройства непосредственно через последовательную консоль hello или открыв сеанс telnet с удаленного компьютера.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Проверка наличия обновлений и их применение
Обновление устройства может занять несколько часов. Выполните следующие шаги tooscan для hello и установить обновления на устройстве.

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a>tooupdate устройства
1. На устройстве hello **быстрый запуск** щелкните **устройств**. Выберите hello физическое устройство, нажмите кнопку **обслуживания** и нажмите кнопку **сканирование обновлений**.  
2. Создается задание tooscan наличие доступных обновлений. Если обновления доступны, hello **сканирования обновлений** изменяет слишком**установить обновления**. Нажмите **Установить обновления**.
3. Будет создано задание обновления. Отслеживать состояние обновления hello, перейдя по слишком**задания**.
   
   > [!NOTE]
   > Сразу после запуска задания обновления hello отображает состояние hello как 50 процентов. состояние Hello изменяется значение в процентах too100 только после завершения задания обновления hello. Нет состояния в режиме реального времени для процесса обновления hello.
   > 
   > 
4. После успешного обновления устройства hello включите сетевые интерфейсы Data 2 и 3 данных, если они были отключены.

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Получение IQN узла Windows Server hello
Выполните следующие шаги tooget hello iSCSI hello полное имя (IQN) узла Windows под управлением Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Создание резервной копии вручную
Выполните следующие действия, описанные в ручной архивации hello портала государственных toocreate по требованию для одного тома на устройстве StorSimple hello.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>Настройка MPIO
MPIO представляет собой дополнительный компонент, который по умолчанию отсутствует в Windows Server. Его необходимо устанавливать в качестве отдельного компонента через диспетчер сервера. Инструкции по установке MPIO, см. слишком[Настройка MPIO для устройства StorSimple](storsimple-configure-mpio-windows-server.md).

Инструкции по установке MPIO для устройства StorSimple подключенных tooa узле Linux, см. слишком[Настройка MPIO для узла Linux](storsimple-configure-mpio-on-linux.md).

> [!NOTE]
> MPIO не поддерживается на виртуальном устройстве StorSimple в Azure.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* Настройте [виртуальное устройство](storsimple-virtual-device-u2.md).
* Используйте hello [в службе StorSimple Manager](storsimple-manager-service-administration.md) toomanage устройства StorSimple.

