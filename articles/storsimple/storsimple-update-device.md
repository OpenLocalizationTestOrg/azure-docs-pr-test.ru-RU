---
title: "aaaUpdate устройства StorSimple | Документы Microsoft"
description: "Объясняет, как обновить toouse hello StorSimple tooinstall функция регулярных и обновления в режиме обслуживания и исправления."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>Обновление устройства StorSimple серии 8000
## <a name="overview"></a>Обзор
Hello StorSimple обновления предоставляет следующие возможности tooeasily актуальность устройства StorSimple. В зависимости от типа hello обновления можно применить обновления toohello устройства hello классический портал Azure или с помощью интерфейса Windows PowerShell hello. Этот учебник описывает типы обновления hello и как tooinstall каждого из них.

Можно применить два вида обновлений устройств: 

* Обычные обновления.
* Обновления режима обслуживания.

Можно устанавливать регулярные обновления через hello классический портал Azure или Windows PowerShell; Тем не менее необходимо использовать Windows PowerShell tooinstall обновления в режиме обслуживания. 

Каждый тип обновления будет описан отдельно ниже.

### <a name="regular-updates"></a>Обычные обновления
Регулярные обновления, не нарушающие работу обновления, которые можно установить при hello устройство находится в обычном режиме. Эти обновления применяются через контроллера устройства tooeach веб-сайт центра обновления Майкрософт hello. 

> [!IMPORTANT]
> Отработка отказа контроллера может возникнуть во время процесса обновления hello. Однако это не повлияет на доступность системы или операции.
> 
> 

* Дополнительные сведения о способах tooinstall регулярные обновления через hello классического портала Azure см. в разделе [Установка регулярных обновлений через hello классический портал Azure](#install-regular-updates-via-the-azure-classic-portal).
* Обычные обновления можно также установить через Windows PowerShell для StorSimple. Дополнительные сведения см. в статье [Установка обычных обновлений через Windows PowerShell для StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).

### <a name="maintenance-mode-updates"></a>Обновления режима обслуживания.
Обновления режима обслуживания прерывают работу. К ним относятся, например, обновления встроенного ПО дисков. Эти обновления требуют toobe устройства hello перевести в режим обслуживания. Дополнительные сведения см. в разделе [Шаг 2. Вход в режим обслуживания](#step2). Нельзя использовать hello Azure классического портала tooinstall обновления в режиме обслуживания. Вместо этого необходимо использовать Windows PowerShell для StorSimple. 

Дополнительные сведения о способах обновления tooinstall режима обслуживания см. в разделе [обновления в режиме обслуживания, установите через Windows PowerShell для StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Режим обслуживания, обновления, необходимо применять отдельно tooeach контроллера. 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>Установка регулярных обновлений через hello классический портал Azure
Можно использовать устройство StorSimple tooyour обновления Azure классического портала tooapply hello.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>Установка обычных обновлений через Windows PowerShell для StorSimple
Кроме того можно использовать Windows PowerShell для StorSimple tooapply (обычный режим) регулярных обновлений.

> [!IMPORTANT]
> Несмотря на то, что можно устанавливать регулярные обновления, с помощью Windows PowerShell для StorSimple, настоятельно рекомендуется установить регулярные обновления через hello классический портал Azure. Предварительная проверка, начиная с обновлением 1, будет выполнено предыдущих tooinstalling обновлений с портала hello. Эти предварительные проверки устраняют сбои и обеспечивают более стабильную работу. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>Установка обновлений режима обслуживания через Windows PowerShell для StorSimple
Вы используете Windows PowerShell для StorSimple режим обслуживания tooapply обновлений устройства StorSimple tooyour. В этом режиме приостанавливаются все запросы ввода-вывода. Службы, такие как энергонезависимой ОЗУ (NVRAM) или служба кластеров hello также останавливаются. Оба контроллера перезагружаются при входе и выходе из этого режима. При выходе из этого режима все службы hello будет возобновлена и должен быть работоспособное. Это может занять несколько минут.

Если вам требуется tooapply обновления в режиме обслуживания, вы получите оповещение через hello классический портал Azure о наличии обновлений, которые должны быть установлены. Оповещения содержат инструкции по использованию Windows PowerShell для StorSimple tooinstall hello обновлений. После установки устройства используйте hello же процедура toochange hello устройства tooRegular режим. Пошаговые инструкции см. в разделе [Шаг 4. Выход из режима обслуживания](#step4).

> [!IMPORTANT]
> * Перед переходом в режим обслуживания, убедитесь, что оба контроллера устройства находятся в работоспособном состоянии, проверив hello **состояние оборудования** на hello **обслуживания** страницу приветствия классический портал Azure. Если hello контроллер не работает, обратитесь в службу поддержки Майкрософт за дальнейшими действиями hello. Дополнительные сведения см. в tooContact технической поддержки Майкрософт. 
> * При работе в режиме обслуживания необходимо tooapply сначала hello обновления на одном контроллере, и затем на hello другой контроллер.
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>Шаг 1: Подключение toohello последовательной консоли<a name="step1">
Во-первых работать с приложением, такие как PuTTY tooaccess hello последовательной консоли. Hello следующая процедура описывает, как toouse PuTTY tooconnect toohello последовательной консоли.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>Шаг 2. Вход в режим обслуживания <a name="step2">
После подключения консоли toohello проверить наличие обновлений tooinstall и введите tooinstall режим обслуживания их.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>Шаг 3. Установка обновлений <a name="step3">
Затем установите обновления.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>Шаг 4. Выход из режима обслуживания <a name="step4">
В конце выйдите из режима обслуживания.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>Установка исправлений через Windows PowerShell или StorSimple
В отличие от обновлений для Microsoft Azure StorSimple, исправления устанавливаются из общей папки. Как и в случае обновлений, существует два вида исправлений: 

* Обычные исправления. 
* Исправления режима обслуживания.  

Hello следующих процедурах объясняется, как toouse Windows PowerShell для StorSimple tooinstall регулярных и исправлений в режиме обслуживания.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>Что произойдет, tooupdates при выполнении фабрику для сброса устройства hello?
Если устройство является toofactory Сброс параметров, все обновления hello будут потеряны. После регистрации и настройки hello Восстановление заводских настроек устройства необходимо будет устанавливать обновления toomanually через hello классический портал Azure и (или) Windows PowerShell для StorSimple. Дополнительные сведения о Восстановление заводских настроек см. в разделе [сбросить параметры по умолчанию hello устройства toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [устройства StorSimple с помощью Windows PowerShell для StorSimple tooadminister](storsimple-windows-powershell-administration.md).
* Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).

