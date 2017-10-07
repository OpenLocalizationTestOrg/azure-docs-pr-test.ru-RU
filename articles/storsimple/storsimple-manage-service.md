---
title: "aaaDeploy hello в службе StorSimple Manager | Документы Microsoft"
description: "Объясняет, как toocreate и delete hello в службе StorSimple Manager в hello классический портал Azure и описывает, как toomanage hello регистрационный ключ службы."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>Развертывание службы диспетчера StorSimple hello в hello классический портал Azure

## <a name="overview"></a>Обзор
Hello в службе StorSimple Manager выполняется в Microsoft Azure и подключается toomultiple устройства StorSimple. После создания службы hello, его можно использовать устройства hello toomanage hello Microsoft Azure классического портала запуск в браузере. Это позволяет toomonitor всех hello устройствах, подключенных toohello StorSimple Manager службы из централизованного расположения, что сокращает административную нагрузку.

Целевая страница Hello диспетчера StorSimple перечислены все службы диспетчера StorSimple hello, можно использовать toomanage запоминающего устройства StorSimple. Каждой службы диспетчера StorSimple представляются hello следующую информацию на странице приветствия StorSimple Manager.

* **Имя** — hello имя, присвоенное службе диспетчера StorSimple tooyour при его создании. **Имя службы Hello нельзя добавить после создания службы hello. Это справедливо для других сущностей, например устройств, тома, контейнеры томов и политик резервного копирования, не может быть переименован в hello классический портал Azure.**
* **Состояние** — hello состояние службы hello, который может быть **Active**, **создание**, или **Online**.
* **Расположение** — hello географического расположения, в которых hello StorSimple устройство будет развертываться.
* **Подписки** — hello выставления счетов за подписку, которая связана с вашей службой.

Ниже перечислены Hello общих задач, которые могут выполняться посредством hello страница диспетчера StorSimple

* создание службы;
* удаление службы;
* Получить ключ регистрации службы hello
* Повторное создание ключа регистрации службы hello

В данном учебнике как tooperform каждого из этих задач.

## <a name="create-a-service"></a>создание службы;
Используйте hello **быстрое создание** вариант toocreate службе StorSimple Manager в том случае, если требуется toodeploy устройства StorSimple. toocreate службы требуется toohave:

* подписка с соглашением Enterprise;
* активная учетная запись хранения Microsoft Azure;
* Здравствуйте, сведений о выставлении счетов, который используется для управления доступом

Можно также выбрать toogenerate учетной записи хранения по умолчанию при создании службы hello.

Одна служба может управлять несколькими устройствами. Однако устройство не может охватить несколько служб. Крупные организации могут иметь несколько toowork экземпляров службы с разными подписками, организациями или даже местоположениями развертывания. Обратите внимание на то, что вам необходимы отдельные экземпляры устройствам серии StorSimple 8000 toomanage службы диспетчера StorSimple и StorSimple виртуальных массивов.

> [!IMPORTANT] 
> Если вы создали неиспользуемые службу (устройство не операций на этот ресурс) предыдущих tooAugust 2016 г., она не может осуществляться с помощью портала Azure или классический портал Azure. Рекомендуется создать новую службу в hello портал Azure.

Выполните следующие шаги toocreate службы hello.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>удаление службы;
Перед удалением службы убедитесь в отсутствии подключенных устройств, которые используют ее. Если используется служба hello деактивируйте hello подключенных устройств. Операция отключения Hello sever hello соединения между устройством hello и hello службы, но сохранить данные устройства hello в облаке hello.

> [!IMPORTANT] 
> После удаления службы hello операцию невозможно отменить. Любое устройство, использовавшей hello службы потребуется toobe сброса к заводским настройкам прежде, чем он может использоваться с другой службой. В этом случае локальные данные hello на hello устройства, а также конфигурации hello, будут потеряны.

Выполните следующие шаги toodelete службы hello.

### <a name="toodelete-a-service"></a>toodelete службы
1. На hello **в службе StorSimple Manager** странице службы выберите hello обратиться в toodelete.
2. Нажмите кнопку **удалить** hello нижней части страницы приветствия.
3. Нажмите кнопку **Да** в уведомлении подтверждения hello. Он может занять несколько минут, чтобы удалить toobe службы hello.

## <a name="get-hello-service-registration-key"></a>Получить ключ регистрации службы hello
После успешного создания службы необходимо будет tooregister устройства StorSimple со службой hello. tooregister первого устройства StorSimple будет необходимо hello ключ регистрации службы. tooregister дополнительных устройств с существующей службой StorSimple, необходимо будет hello регистрационный ключ и ключ шифрования данных службы hello (который создается на первом устройстве hello во время регистрации). Дополнительные сведения о ключе шифрования данных службы hello см. в разделе [безопасность StorSimple](storsimple-security.md). Hello регистрационный ключ можно получить, обратившись к **регистрационный ключ** на hello **служб** страницы.

Выполните следующие шаги tooget hello регистрационный ключ hello.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

Ключ регистрации службы hello храните в безопасном месте. Вам потребуется этот ключ, а также ключ шифрования данных службы hello tooregister дополнительных устройств с этой службой. После получения ключа регистрации службы hello, необходимо будет tooconfigure устройством через hello Windows PowerShell для StorSimple интерфейса.

Дополнительные сведения о том, как toouse этот регистрации ключа, см. в разделе [Step 3: Настройка и регистрация hello устройства через Windows PowerShell для StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Повторное создание ключа регистрации службы hello
Tooregenerate ключ регистрации службы потребуется tooperform требуется смена ключей или если hello список администраторов службы изменился. При повторном создании ключа hello, hello новый ключ используется только для регистрации последующих устройств. Hello устройств, которые уже были зарегистрированы, не затрагиваются этим процессом.

Выполните следующие tooregenerate действия ключа регистрации службы hello.

### <a name="tooregenerate-hello-service-registration-key"></a>Ключ регистрации службы tooregenerate hello
1. На hello **службы диспетчера StorSimple** щелкните **регистрационный ключ**.
2. В hello **регистрационный ключ службы** диалоговое окно, нажмите кнопку **повторно создать**.
3. Появится сообщение подтверждения. Нажмите кнопку **ОК** toocontinue с hello повторного формирования.
4. Появится новый ключ регистрации службы.
5. Скопируйте этот ключ и сохраните его для регистрации новых устройств в службе.
6. Щелкните значок галочки hello ![значок с изображением флажка](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose данным диалоговым окном.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о hello [процесс развертывания StorSimple](storsimple-deployment-walkthrough-u2.md).
* Узнайте больше об [управлении учетной записью хранения StorSimple](storsimple-manage-storage-accounts.md).
* Дополнительные сведения о том, как слишком[используйте hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).
