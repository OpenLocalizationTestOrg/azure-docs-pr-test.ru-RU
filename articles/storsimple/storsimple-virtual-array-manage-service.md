---
title: "службе диспетчера StorSimple устройство aaaDeploy | Документы Microsoft"
description: "Объясняет, как toocreate и delete hello службы диспетчера StorSimple устройство в hello портал Azure и описывает, как toomanage hello ключ регистрации службы."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>Развертывание службы диспетчера StorSimple устройство hello для StorSimple Virtual Array
## <a name="overview"></a>Обзор

службе диспетчера StorSimple устройство Hello выполняется в Microsoft Azure и подключается toomultiple устройства StorSimple. После создания службы hello, его можно использовать устройства hello toomanage hello Microsoft Azure портала запуск в браузере. Это позволяет toomonitor всех hello устройствах, подключенных toohello устройства StorSimple службы из централизованного расположения, что сокращает административную нагрузку.

Hello распространенные задачи связанные tooa службы диспетчера StorSimple устройств являются:

* создание службы;
* удаление службы;
* Получить ключ регистрации службы hello
* Повторное создание ключа регистрации службы hello

В данном учебнике как tooperform каждого из hello выше задач. Hello сведения, содержащиеся в этой статье — применимо только tooStorSimple виртуальных массивов. Дополнительные сведения о StorSimple серии 8000 go слишком[развертывание службы диспетчера StorSimple](storsimple-manage-service.md).

## <a name="create-a-service"></a>создание службы;

toocreate службы требуется toohave:

* подписка с соглашением Enterprise;
* активная учетная запись хранения Microsoft Azure;
* Здравствуйте, сведений о выставлении счетов, который используется для управления доступом

Можно также выбрать toogenerate учетной записи хранилища при создании службы hello.

Одна служба может управлять несколькими устройствами. Однако устройство не может охватить несколько служб. Крупные организации могут иметь несколько toowork экземпляров службы с разными подписками, организациями или даже местоположениями развертывания.

> [!NOTE]
> Необходимо, чтобы отдельные экземпляры устройствам серии StorSimple 8000 toomanage службы диспетчера StorSimple устройство и StorSimple виртуальных массивов.


Выполните следующие шаги toocreate службы hello.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>удаление службы;

Перед удалением службы убедитесь в отсутствии подключенных устройств, которые используют ее. Если используется служба hello деактивируйте hello подключенных устройств. Операция отключения Hello sever hello соединения между устройством hello и hello службы, но сохранить данные устройства hello в облаке hello.

> [!IMPORTANT]
> После удаления службы hello операцию невозможно отменить. Любое устройство, использовавшей hello службы потребуется toobe сброса к заводским настройкам прежде, чем он может использоваться с другой службой. В этом случае локальные данные hello на hello устройства, а также конфигурации hello, будут потеряны.
 

Выполните следующие шаги toodelete службы hello.

#### <a name="toodelete-a-service"></a>toodelete службы

1. Go слишком**все ресурсы**. Найдите службу диспетчера устройств StorSimple. Выберите службу hello, что вы хотите toodelete.
   
    ![Выберите службы toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. Go tooyour службы мониторинга tooensure существует нет устройств, подключенных toohello служб. Нет устройств, зарегистрированных с помощью этой службы, также увидите эффект toohello заголовка сообщения. Нажмите кнопку **Delete**(Удалить).
   
    ![Удаление службы](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. При появлении запроса на подтверждение нажмите кнопку **Да** в уведомлении подтверждения hello. 
   
    ![Подтверждение удаления службы](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. Он может занять несколько минут, чтобы удалить toobe службы hello. После hello служба успешно удалена, вы получите уведомление.
   
    ![Успешное удаление службы](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

Список Hello служб будет обновлен.

 ![Обновленный список служб](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>Получить ключ регистрации службы hello
После успешного создания службы необходимо будет tooregister устройства StorSimple со службой hello. tooregister первого устройства StorSimple будет необходимо hello ключ регистрации службы. tooregister дополнительных устройств с существующей службой StorSimple, необходимо будет hello регистрационный ключ и ключ шифрования данных службы hello (который создается на первом устройстве hello во время регистрации). Дополнительные сведения о ключе шифрования данных службы hello см. в разделе [безопасность StorSimple](storsimple-security.md). Hello регистрационный ключ можно получить, обратившись к hello **ключей** колонку для службы.

Выполните следующие шаги tooget hello регистрационный ключ hello.

#### <a name="tooget-hello-service-registration-key"></a>Ключ регистрации службы tooget hello
1. В hello **устройства StorSimple** колонке go слишком**управления &gt;**  **ключей**.
   
   ![Колонка "Ключи"](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. В hello **ключей** колонки, отображается ключ регистрации службы. Скопируйте ключ регистрации hello, используя значок копирования hello. 

Ключ регистрации службы hello храните в безопасном месте. Вам потребуется этот ключ, а также ключ шифрования данных службы hello tooregister дополнительных устройств с этой службой. После получения ключа регистрации службы hello, необходимо будет tooconfigure устройством через hello Windows PowerShell для StorSimple интерфейса.

## <a name="regenerate-hello-service-registration-key"></a>Повторное создание ключа регистрации службы hello
Tooregenerate ключ регистрации службы потребуется tooperform требуется смена ключей или если hello список администраторов службы изменился. При повторном создании ключа hello, hello новый ключ используется только для регистрации последующих устройств. Hello устройств, которые уже были зарегистрированы, не затрагиваются этим процессом.

Выполните следующие tooregenerate действия ключа регистрации службы hello.

#### <a name="tooregenerate-hello-service-registration-key"></a>Ключ регистрации службы tooregenerate hello
1. В hello **устройства StorSimple** колонке go слишком**управления &gt;**  **ключей**.
   
   ![Колонка "Ключи"](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. В hello **ключей** колонка, щелкните **повторно создать**.
   
   ![Кнопка повторного создания](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. В hello **регистрационный ключ службы заново** колонке действие hello проверка требуется, если hello повторно создаются ключи. Все устройства последующие hello, которые зарегистрированы с помощью этой службы будет использовать новый ключ hello. Нажмите кнопку **повторно создать** tooconfirm. Вы получите уведомление после завершения регистрации hello.
   
   ![Подтверждение повторного создания ключа](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. Появится новый ключ регистрации службы.
   
    ![Подтверждение повторного создания ключа](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   Скопируйте этот ключ и сохраните его для регистрации новых устройств в службе.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[начать](storsimple-virtual-array-deploy1-portal-prep.md) с StorSimple Virtual Array.
* Узнайте, каким образом слишком[Администрирование устройства StorSimple](storsimple-ova-web-ui-admin.md).

