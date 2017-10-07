---
title: "aaaDeploy устройства StorSimple (обновление 2) | Документы Microsoft"
description: "Описывает этапы hello и рекомендации по развертыванию устройства StorSimple с обновлением 2 hello и службы."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7dff0612-617b-4fc8-a3fe-994c24bc7c51
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: alkohli
ms.openlocfilehash: 5906cc3c41f03c426905ef91be37852608ae9393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-2"></a>Развертывание локального устройства StorSimple (с обновлением 2)
> [!div class="op_single_selector"]
> * [Обновление 2 и более поздних версий ](storsimple-deployment-walkthrough-u2.md)
> * [Обновление 1](storsimple-deployment-walkthrough-u1.md)
> * [Выпуск общедоступной версии](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a>Обзор
Вас приветствует tooMicrosoft развертывания устройства Azure StorSimple. Эти руководства по развертыванию применить tooStorSimple 8000 с обновлением 2 ряда. В этой серии учебников описывается контрольный список настройки, предварительные требования к конфигурации и подробное пошаговое руководство по настройке устройства StorSimple.

Hello сведения в этих учебниках предполагается, что проверены hello меры предосторожности и распаковать, racked и подключить кабели устройства StorSimple. Если по-прежнему требуется tooperform тех задач, начните с проверки hello [меры предосторожности](storsimple-safety.md). Инструкции hello устройства конкретного стойку toounpack и подключите к устройству.

* [Распаковка, монтаж в стойку и подключение кабелей к устройству 8100](storsimple-8100-hardware-installation.md)
* [Распаковка, монтаж в стойку и подключение кабелей к устройству 8600](storsimple-8600-hardware-installation.md)

Вам потребуется администратора привилегии toocomplete hello процесса установки и настройки. Рекомендуется просмотреть hello контрольный список для настройки перед началом. Hello развертывания и конфигурации может занять некоторое время toocomplete.

> [!NOTE]
> сведения о развертывании StorSimple Hello опубликованы на веб-сайте Microsoft Azure hello применяется tooStorSimple 8000 ряда только для устройств. Полные сведения об устройствах серии hello 7000 см. в: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Дополнительные сведения о развертывании серии 7000, см hello [StorSimple краткое руководство по системе](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Шаги по развертыванию
Выполните эти действия tooconfigure устройства StorSimple и подключите его tooyour в службе StorSimple Manager. В дополнение к этому toohello обязательные действия, существуют дополнительные шаги и процедурах, которые могут потребоваться при развертывании hello. Hello пошаговые инструкции по развертыванию указывают, когда следует выполнять каждый из этих необязательных действий.

| Шаг | Description (Описание) |
| --- | --- |
| **ПРЕДВАРИТЕЛЬНЫЕ ТРЕБОВАНИЯ** |Они должны toobe завершена при подготовке к развертыванию предстоящих hello. |
| [Контрольный список конфигурации развертывания](#deployment-configuration-checklist) |Используйте этот контрольный список toogather и записи сведения о предыдущих tooand во время развертывания hello. |
| [Предварительные условия для развертывания](#deployment-prerequisites) |Эти проверки hello среда готова к развертыванию. |
|  | |
| **ПОШАГОВОЕ РАЗВЕРТЫВАНИЕ** |Эти действия являются обязательным toodeploy устройства StorSimple в рабочей среде. |
| [Шаг 1. Создание новой службы](#step-1-create-a-new-service) |Настройте облачное управление и хранение для устройства StorSimple. *При наличии существующей службы для других устройств StorSimple пропустите этот шаг*. |
| [Шаг 2: Получение ключа регистрации службы hello](#step-2-get-the-service-registration-key) |Использование этого ключа tooregister & подключение со службой управления hello устройства StorSimple. |
| [Шаг 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Подключение к сети tooyour устройство hello и зарегистрируйте его в Azure toocomplete hello установки с помощью службы управления hello. |
| [Шаг 4. Выполнение минимальной настройки устройства](#step-4-complete-minimum-device-setup)</br>[Необязательно: обновление устройства StorSimple](#scan-for-and-apply-updates) |Используйте программу установки устройства hello toocomplete в службе управления hello и включите ее tooprovide хранилища. |
| [Шаг 5. Создание контейнера томов](#step-5-create-a-volume-container) |Создание контейнера тома tooprovision. Контейнер томов имеет учетную запись хранения, пропускной способности и параметры шифрования для всех томов hello, содержащиеся в нем. |
| [Шаг 6. Создание тома](#step-6-create-a-volume) |Подготовка хранилища томов на устройстве StorSimple hello для серверов. |
| [Шаг 7. Подключение, инициализация и форматирование тома](#step-7-mount-initialize-and-format-a-volume)</br>[Необязательно: настройка MPIO](storsimple-configure-mpio-windows-server.md) |Подключение устройства hello хранилища iSCSI toohello серверов. При необходимости настройте tooensure MPIO, что серверы может допускать сбой связи, сети и интерфейс. |
| [Шаг 8. Создание резервной копии](#step-8-take-a-backup) |Настройка вашего tooprotect политику резервного копирования данных |
|  | |
| **ПРОЧИЕ ПРОЦЕДУРЫ** |При развертывании решения может потребоваться toorefer toothese процедуры. |
| [Настройте новую учетную запись хранилища для службы hello](#configure-a-new-storage-account-for-the-service) | |
| [Использовать PuTTY tooconnect toohello последовательной консоли устройства](#use-putty-to-connect-to-the-device-serial-console) | |
| [Получение IQN узла Windows Server hello](#get-the-iqn-of-a-windows-server-host) | |
| [Создание резервной копии вручную](#create-a-manual-backup) | |

## <a name="deployment-configuration-checklist"></a>Контрольный список конфигурации развертывания
Прежде чем развертывать устройства, необходимо будет toocollect tooconfigure сведения hello, программного обеспечения на устройстве StorSimple. Некоторые из этих сведений заранее подготовка позволит упростить процесс hello hello устройство StorSimple в среде развертывания. Загрузите и используйте этот контрольный список toonote вниз hello сведения о конфигурации при развертывании устройства.

* [Скачать контрольный список настройки развертывания устройства StorSimple](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a>Предварительные условия для развертывания
Привет, в следующих разделах объясняется hello предварительные требования конфигурации для службы диспетчера StorSimple и устройства StorSimple.

### <a name="for-hello-storsimple-manager-service"></a>Для hello службы диспетчера StorSimple
Перед тем как начать, убедитесь в следующем.

* Имеется учетная запись Майкрософт и данные для доступа к ней.
* Имеется учетная запись хранения Microsoft Azure и данные для доступа к ней.
* Для hello в службе StorSimple Manager включены подписки Microsoft Azure. Необходимо приобрести подписку по hello [соглашение Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* У вас есть доступ программное обеспечение эмуляции tooterminal например PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Для устройства hello в центре обработки данных hello
Перед настройкой устройства hello, убедитесь, что устройство полностью распаковать, монтируется на стойки и полностью подключить кабели питания, сети и для последовательного доступа, как описано в:

* [Распаковка, монтаж в стойку и подключение кабелей к устройству 8100](storsimple-8100-hardware-installation.md)
* [Распаковка, монтаж в стойку и подключение кабелей к устройству 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Для hello сети в центре обработки данных hello
Перед тем как начать, убедитесь в следующем.

* Hello порты в брандмауэре центра обработки данных, tooallow открыт для трафика iSCSI и облаку описаны в [требования к сети для устройства StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>ПОШАГОВОЕ РАЗВЕРТЫВАНИЕ
Используйте следующие пошаговые инструкции toodeploy hello устройства StorSimple в центре обработки данных hello.

## <a name="step-1-create-a-new-service"></a>Шаг 1. Создание новой службы
Служба Диспетчера StorSimple может управлять несколькими устройствами StorSimple. Выполните следующие шаги toocreate новый экземпляр службы StorSimple Manager hello hello.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> Если вы не включили hello автоматическое создание учетной записи хранилища в службе, необходимо будет toocreate по крайней мере одну учетную запись хранения после успешного создания службы. Эта учетная запись хранения будет использоваться при создании контейнера томов. 
> 
> * Если не была автоматически создана учетная запись хранения, перейдите в слишком[настроить новую учетную запись хранилища для службы hello](#configure-a-new-storage-account-for-the-service) подробные инструкции. 
> * Если вы включили hello автоматическое создание учетной записи хранилища, перейдите в слишком[шаг 2: ключ регистрации службы hello Get](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Шаг 2: Получение ключа регистрации службы hello
После hello в службе StorSimple Manager запущен и работает, потребуется ключ регистрации службы tooget hello. Этот ключ используется tooregister и подключите устройство StorSimple со службой hello.

Выполнение шагов в портал управления hello hello.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Шаг 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple
Используйте Windows PowerShell для StorSimple toocomplete hello начальной настройки устройства StorSimple, как описывается в hello после процедуры. Вам потребуется toocomplete программное обеспечение эмуляции терминала toouse этот шаг. Дополнительные сведения см. в разделе [последовательной консоли устройства toohello использование PuTTY tooconnect](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-u1](../../includes/storsimple-configure-and-register-device-u1.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Шаг 4. Выполнение минимальной настройки устройства
Для hello минимальную настройку устройства StorSimple вы должны: 

* Настройка hello дополнительного DNS-сервера.
* Включите последовательный интерфейс iSCSI хотя бы на одном сетевом интерфейсе.
* Назначьте фиксированные IP-адреса контроллеров tooboth hello.

Выполните следующие шаги в hello портала управления toocomplete hello минимальной настройки устройства hello.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Шаг 5. Создание контейнера томов
Контейнер томов имеет учетную запись хранения, пропускной способности и параметры шифрования для всех томов hello, содержащиеся в нем. Вам потребуется toocreate контейнер тома, прежде чем приступить к подготовке томов на устройстве StorSimple. 

Выполнение шагов в портал управления hello toocreate контейнер томов hello.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Шаг 6. Создание тома
После создания контейнера тома, можно подготовить том хранилища на устройстве StorSimple hello для серверов. Выполните следующие шаги в портал управления hello toocreate тома hello.

> [!IMPORTANT]
> StorSimple Manager может создавать тома с тонкой и полной подготовкой. Однако тома с частичной подготовкой создать нельзя. 
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Шаг 7. Подключение, инициализация и форматирование тома
Привет, следующие шаги выполняются на узле Windows Server. 

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

Выполнение шагов в портал управления hello toocreate архивации по расписанию hello.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

Резервное копирование вручную можно выполнить в любое время. Для процедур go слишком[создать вручную резервную копию](#create-a-manual-backup). 

## <a name="configure-a-new-storage-account-for-hello-service"></a>Настройте новую учетную запись хранилища для службы hello
Это необязательный шаг должны tooperform только в том случае, если вы не включили hello автоматическое создание учетной записи хранилища в службе. Учетную запись хранения Microsoft Azure является обязательным toocreate контейнера томов StorSimple.

При необходимости toocreate учетную запись хранилища Azure в другом регионе. в разделе [об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md) пошаговые инструкции.

Выполните следующие шаги в hello портала управления на hello hello **в службе StorSimple Manager** страницы.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Использовать PuTTY tooconnect toohello последовательной консоли устройства
tooWindows tooconnect PowerShell для StorSimple, необходимо toouse программное обеспечение эмуляции терминала, например PuTTY. Можно использовать PuTTY при доступе к hello устройства непосредственно через последовательную консоль hello или открыв сеанс telnet с удаленного компьютера.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Проверка наличия обновлений и их применение
Обновление устройства может занять несколько часов. Выполните следующие шаги tooscan для hello и установить обновления на устройстве.
<!--can take 1-4 hours--> 

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

<!-- In step 2, you may be requested toodisable Data 2 and Data 3 prior tooinstalling hello updates. You must disable these network interfaces or hello updates may fail.-->

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Получение IQN узла Windows Server hello
Выполните следующие шаги tooget hello iSCSI hello полное имя (IQN) узла Windows под управлением Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Создание резервной копии вручную
Выполните следующие действия, описанные в ручной архивации hello портала управления toocreate по требованию для одного тома на устройстве StorSimple hello.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="next-steps"></a>Дальнейшие действия
* Настройте [виртуальное устройство](storsimple-virtual-device-u2.md).
* Используйте hello [в службе StorSimple Manager](storsimple-manager-service-administration.md) toomanage устройства StorSimple.

