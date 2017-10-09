---
title: "aaaDeploy устройства серии StorSimple 8000 в портал Azure | Документы Microsoft"
description: "Описывает шаги hello и рекомендации по развертыванию устройства серии StorSimple 8000 hello под управлением обновления 3 и более поздней версии и службой диспетчера устройств StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 28d32d6c0d37169902d9db91701deee4fd99dc4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-3-and-later"></a>Развертывание локального устройства StorSimple (с обновлением 3 и более поздней версии)

## <a name="overview"></a>Обзор
Вас приветствует tooMicrosoft развертывания устройства Azure StorSimple. Эти руководства по развертыванию применить tooStorSimple серии 8000 обновления 3 или более поздней версии. В этой серии учебников описывается контрольный список настройки, предварительные требования к конфигурации и подробное пошаговое руководство по настройке устройства StorSimple.

Hello сведения в этих учебниках предполагается, что проверены hello меры предосторожности и распаковать, racked и подключить кабели устройства StorSimple. Если по-прежнему требуется tooperform тех задач, начните с проверки hello [меры предосторожности](storsimple-8000-safety.md). Следуйте инструкциям для конкретного устройства hello стойку toounpack и подключите к устройству.

* [Распаковка, монтаж в стойку и подключение кабелей к устройству 8100](storsimple-8100-hardware-installation.md)
* [Распаковка, монтаж в стойку и подключение кабелей к устройству 8600](storsimple-8600-hardware-installation.md)

Необходимо, чтобы администратор права toocomplete hello процесса установки и настройки. Рекомендуется просмотреть hello контрольный список для настройки перед началом. Hello развертывания и конфигурации может занять некоторое время toocomplete.

> [!NOTE]
> сведения о развертывании StorSimple Hello опубликованы на веб-сайте Microsoft Azure hello применяется tooStorSimple 8000 ряда только для устройств. Полные сведения об устройствах серии hello 7000 см. в: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Дополнительные сведения о развертывании серии 7000, см hello [StorSimple краткое руководство по системе](http://onlinehelp.storsimple.com/111_Appliance/). 


## <a name="deployment-steps"></a>Шаги по развертыванию
Выполните эти действия tooconfigure устройства StorSimple и подключите его службе диспетчера StorSimple устройство tooyour. В дополнение к этому toohello обязательные действия, существуют дополнительные шаги и процедурах, которые могут потребоваться при развертывании hello. Hello пошаговые инструкции по развертыванию указывают, когда следует выполнять каждый из этих необязательных действий.

| Шаг | Description (Описание) |
| --- | --- |
| **ПРЕДВАРИТЕЛЬНЫЕ ТРЕБОВАНИЯ** |Они должны выполняться в процессе подготовки к развертыванию предстоящих hello. |
| [Контрольный список конфигурации развертывания](#deployment-configuration-checklist) |Используйте этот контрольный список toogather и записи информации до и во время развертывания hello. |
| [Предварительные условия для развертывания](#deployment-prerequisites) |Эти проверки hello среда готова к развертыванию. |
|  | |
| **ПОШАГОВОЕ РАЗВЕРТЫВАНИЕ** |Эти действия являются обязательным toodeploy устройства StorSimple в рабочей среде. |
| [Шаг 1. Создание новой службы](#step-1-create-a-new-service) |Настройте облачное управление и хранение для устройства StorSimple. *При наличии существующей службы для других устройств StorSimple пропустите этот шаг*. |
| [Шаг 2: Получение ключа регистрации службы hello](#step-2-get-the-service-registration-key) |Использование этого ключа tooregister & подключение со службой управления hello устройства StorSimple. |
| [Шаг 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |toocomplete hello установки с помощью службы управления hello, подключение к сети tooyour устройство hello и зарегистрируйте его в Azure. |
| [Шаг 4. Выполнение минимальной настройки устройства](#step-4-complete-minimum-device-setup)</br>[Необязательно: обновление устройства StorSimple](#scan-for-and-apply-updates) |Используйте программу установки устройства hello toocomplete в службе управления hello и включите ее tooprovide хранилища. |
| [Шаг 5. Создание контейнера томов](#step-5-create-a-volume-container) |Создание контейнера тома tooprovision. Контейнер томов имеет учетную запись хранения, пропускной способности и параметры шифрования для всех томов hello, содержащиеся в нем. |
| [Шаг 6. Создание тома](#step-6-create-a-volume) |Подготовить тома хранилища на устройстве StorSimple hello для серверов. |
| [Шаг 7. Подключение, инициализация и форматирование тома](#step-7-mount-initialize-and-format-a-volume)</br>[Необязательно: настройка MPIO](storsimple-8000-configure-mpio-windows-server.md) |Подключение устройства hello хранилища iSCSI toohello серверов. При необходимости настройте tooensure MPIO, что серверы может выдержать связи, сети и интерфейс сбоя. |
| [Шаг 8. Создание резервной копии](#step-8-take-a-backup) |Настройка вашего tooprotect политику резервного копирования данных |
|  | |
| **ПРОЧИЕ ПРОЦЕДУРЫ** |При развертывании решения может потребоваться toorefer toothese процедуры. |
| [Настройте новую учетную запись хранилища для службы hello](#configure-a-new-storage-account-for-the-service) | |
| [Использовать PuTTY tooconnect toohello последовательной консоли устройства](#use-putty-to-connect-to-the-device-serial-console) | |
| [Получение IQN узла Windows Server hello](#get-the-iqn-of-a-windows-server-host) | |
| [Создание резервной копии вручную](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a>Контрольный список конфигурации развертывания
Перед развертыванием устройства требуется toocollect tooconfigure сведения hello, программное обеспечение на устройстве StorSimple. Подготовка некоторые из этих сведений опережает время помогает оптимизировать hello процесс развертывания устройства StorSimple hello в вашей среде. Загрузите и используйте этот контрольный список toonote вниз hello сведения о конфигурации при развертывании устройства.

* [Скачать контрольный список настройки развертывания устройства StorSimple](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a>Предварительные условия для развертывания
Привет, в следующих разделах объясняется hello предварительные требования конфигурации для службы диспетчера StorSimple устройства и устройства StorSimple.

### <a name="for-hello-storsimple-device-manager-service"></a>Для hello службой диспетчера устройств StorSimple
Перед тем как начать, убедитесь в следующем.

* Имеется учетная запись Майкрософт и данные для доступа к ней.
* Имеется учетная запись хранения Microsoft Azure и данные для доступа к ней.
* Для службы диспетчера StorSimple устройство hello включены подписки Microsoft Azure. Необходимо приобрести подписку по hello [соглашение Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* У вас есть доступ программное обеспечение эмуляции tooterminal например PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Для устройства hello в центре обработки данных hello
Перед настройкой устройства hello, убедитесь, что устройство полностью распаковать, монтируется на стойки и полностью подключить кабели питания, сети и для последовательного доступа, как описано в:

* [Распаковка, монтаж в стойку и подключение кабелей к устройству 8100](storsimple-8100-hardware-installation.md)
* [Распаковка, монтаж в стойку и подключение кабелей к устройству 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Для hello сети в центре обработки данных hello
Перед тем как начать, убедитесь в следующем.

* Hello порты в брандмауэре центра обработки данных, tooallow открыт для трафика iSCSI и облаку описаны в [требования к сети для устройства StorSimple](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>ПОШАГОВОЕ РАЗВЕРТЫВАНИЕ
Используйте следующие пошаговые инструкции toodeploy hello устройства StorSimple в центре обработки данных hello.

## <a name="step-1-create-a-new-service"></a>Шаг 1. Создание новой службы
Служба диспетчера устройств StorSimple может управлять несколькими устройствами StorSimple. Выполните следующие шаги toocreate экземпляр службы диспетчера StorSimple устройство hello hello.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]

> [!IMPORTANT]
> Если вы не включили hello автоматическое создание учетной записи хранилища в службе, необходимо будет toocreate по крайней мере одну учетную запись хранения после успешного создания службы. Эта учетная запись хранения будет использоваться при создании контейнера томов.
>
> * Если не была автоматически создана учетная запись хранения, перейдите в слишком[настроить новую учетную запись хранилища для службы hello](#configure-a-new-storage-account-for-the-service) подробные инструкции.
> * Если вы включили hello автоматическое создание учетной записи хранилища, перейдите в слишком[шаг 2: ключ регистрации службы hello Get](#step-2-get-the-service-registration-key).


## <a name="step-2-get-hello-service-registration-key"></a>Шаг 2: Получение ключа регистрации службы hello
После hello службы диспетчера StorSimple устройство работает, потребуется ключ регистрации службы tooget hello. Этот ключ используется tooregister и подключите устройство StorSimple со службой hello.

Выполнение шагов в hello портал Azure hello.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Шаг 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple
Используйте Windows PowerShell для StorSimple toocomplete hello начальной настройки устройства StorSimple, как описывается в hello после процедуры. Необходимо toocomplete программное обеспечение эмуляции терминала toouse этот шаг. Дополнительные сведения см. в разделе [последовательной консоли устройства toohello использование PuTTY tooconnect](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-8000-configure-and-register-device-u2](../../includes/storsimple-8000-configure-and-register-device-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Шаг 4. Выполнение минимальной настройки устройства
Для hello минимальную настройку устройства StorSimple вы должны: 

* Укажите понятное имя для устройства.
* Задайте часовой пояс устройства hello.
* Назначьте фиксированные IP-адреса контроллеров tooboth hello.

Выполните следующие шаги в hello Azure портала toocomplete hello минимальной настройки устройства hello.

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a>Шаг 5. Создание контейнера томов
Контейнер томов имеет учетную запись хранения, пропускной способности и параметры шифрования для всех томов hello, содержащиеся в нем. Вам потребуется toocreate контейнер тома, прежде чем приступить к подготовке томов на устройстве StorSimple.

Выполнение шагов в hello Azure портала toocreate контейнер томов hello.

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Шаг 6. Создание тома
После создания контейнера тома, можно подготовить том хранилища на устройстве StorSimple hello для серверов. Выполните следующие шаги в hello Azure портала toocreate тома hello.

> [!IMPORTANT]
> Диспетчер устройств StorSimple может создавать тома с тонкой и полной подготовкой. Однако тома с частичной подготовкой создать нельзя.


[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Шаг 7. Подключение, инициализация и форматирование тома
Привет, следующие шаги выполняются на узле Windows Server.

> [!IMPORTANT]
> * Hello высокую доступность решения StorSimple рекомендуется настроить MPIO на предыдущий tooconfiguring iSCSI узлов серверов (необязательно). Конфигурации MPIO на серверах узла убедитесь, что серверы hello может выдержать связи, сети или интерфейса.
> * MPIO и iSCSI инструкции по установке и конфигурации на узле Windows Server, перейдите слишком[Настройка MPIO для устройства StorSimple](storsimple-8000-configure-mpio-windows-server.md). К ним также относятся toomount действия hello, инициализация и форматирование томов StorSimple.
> * MPIO и iSCSI инструкции по установке и конфигурации на узле Linux, перейдите слишком[Настройка MPIO для узла StorSimple Linux](storsimple-configure-mpio-on-linux.md)

Если решить tooconfigure MPIO, выполните следующие шаги toomount hello, инициализация и форматирование тома StorSimple на узле Windows Server.

[!INCLUDE [storsimple-8000-mount-initialize-format-volume](../../includes/storsimple-8000-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Шаг 8. Создание резервной копии
Резервные копии обеспечивают защиту состояния томов до определенной точки во времени и улучают возможности восстановления, одновременно снижая время восстановления. Устройство StorSimple позволяет создавать резервные копии двух типов: локальные и облачные моментальные снимки. Каждый из этих типов резервных копий может создаваться **по расписанию** или **вручную**.

Выполнение шагов в hello Azure портала toocreate архивации по расписанию hello.

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

Резервное копирование вручную можно выполнить в любое время. Для процедур go слишком[создать вручную резервную копию](#create-a-manual-backup).

Вы завершили hello конфигурации устройства.

## <a name="configure-a-new-storage-account-for-hello-service"></a>Настройте новую учетную запись хранилища для службы hello
Это необязательный шаг должны tooperform только в том случае, если вы не включили hello автоматическое создание учетной записи хранилища в службе. Учетную запись хранения Microsoft Azure является обязательным toocreate контейнера томов StorSimple.

При необходимости toocreate учетную запись хранилища Azure в другом регионе. в разделе [об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md) пошаговые инструкции.

Выполнение шагов в hello в hello портала Azure hello **службы диспетчера StorSimple устройство** страницы.

[!INCLUDE [storsimple-8000-configure-new-storage-account-u2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Использовать PuTTY tooconnect toohello последовательной консоли устройства
tooWindows tooconnect PowerShell для StorSimple, необходимо toouse программное обеспечение эмуляции терминала, например PuTTY. Можно использовать PuTTY при доступе к hello устройства непосредственно через последовательную консоль hello или открыв сеанс telnet с удаленного компьютера.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Проверка наличия обновлений и их применение
Обновление устройства может занять несколько часов. Подробные инструкции по как tooinstall hello последнее обновление, перейдите в слишком[установите обновление 4](storsimple-8000-install-update-4.md).


## <a name="get-hello-iqn-of-a-windows-server-host"></a>Получение IQN узла Windows Server hello
Выполните следующие шаги tooget hello iSCSI hello полное имя (IQN) узла Windows под управлением Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Создание резервной копии вручную
Выполните следующие действия, описанные в ручной архивации hello Azure toocreate портала по запросу для одного тома на устройстве StorSimple hello.

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Дальнейшие действия
* [Deploy and manage a StorSimple Cloud Appliance in Azure (Update 3 and later)](storsimple-8000-cloud-appliance-u2.md) (Развертывание и администрирование облачного устройства StorSimple в Azure (обновление 3 и более поздней версии)).
* [Используйте hello toomanage службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).

