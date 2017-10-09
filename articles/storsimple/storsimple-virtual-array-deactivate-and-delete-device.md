---
title: "aaaDeactivate и удаление виртуального массива Microsoft Azure StorSimple | Документы Microsoft"
description: "Описывает способ tooremove устройство StorSimple из службы, сначала отключить его, а затем удаляет его."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>Отключение и удаление виртуального массива StorSimple

## <a name="overview"></a>Обзор

При отключении StorSimple Virtual Array hello связь между устройством hello и соответствующей службы диспетчера StorSimple устройство hello прерывается. В этом учебнике объясняется, как выполнить такие задачи:

* Отключение устройства 
* Удаление отключенного устройства

Hello информация в этой статье относится только tooStorSimple виртуальных массивов. Сведения о серии 8000 go toohow слишком[деактивировать или удалить устройство](storsimple-deactivate-and-delete-device.md).

## <a name="when-toodeactivate"></a>Когда toodeactivate?

Отключение является НЕОБРАТИМОЙ операцией. Нельзя зарегистрировать деактивированное устройство с hello службы диспетчера StorSimple устройство еще раз. Возможно требуется toodeactivate и удалите StorSimple Virtual Array в hello следующие сценарии:

* **Переход на другой ресурс** : устройство находится в оперативном режиме и планирование toofail отказа устройства. Если вы планируете tooupgrade tooa больше устройств, может потребоваться toofail отказа устройства. После передачи hello право собственности на данные и завершения hello перехода на другой ресурс, hello исходное устройство удаляется автоматически.
* **Незапланированная отработка отказа** : устройство находится в автономном режиме, и требуется toofail по сравнению с устройства hello. Данная ситуация может произойти при аварии, когда происходит сбой в центре обработки данных hello и основного устройства не работает. При планировании toofail устройствами hello устройства tooa получателя. После передачи hello право собственности на данные и завершения hello перехода на другой ресурс, hello исходное устройство удаляется автоматически.
* **Списание** : необходимо toodecommission hello устройством. Для этого необходимо toofirst деактивировать устройство hello, а затем удалите его. После отключения устройства все данные, хранящиеся локально, станут недоступны. Вы можете только доступ и восстановление данных hello, хранящихся в облаке hello. Если планируется hello tookeep данные на устройстве после отключения, следует сделать снимок облачного всех данных перед отключением устройства. Этот моментальный снимок облака позволяет toorecover все hello данных в дальнейшем.

## <a name="deactivate-a-device"></a>Отключение устройства

toodeactivate устройства, выполните следующие шаги hello.

#### <a name="toodeactivate-hello-device"></a>устройство toodeactivate hello

1. В службе, перейдите слишком**управления > устройства**. В hello **устройств** колонка, щелкните и обратиться в toodeactivate устройства выберите hello.
   
    ![Выберите устройство toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. В вашей **панели мониторинга устройства** колонка, щелкните **... Дополнительные** и выберите из списка hello **деактивировать**.
   
    ![Нажмите кнопку "Отключить"](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. В hello **деактивировать** колонки, имя устройства типа hello и нажмите кнопку **деактивировать**. 
   
    ![Подтвердите отключение](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    Hello отключить начинается процесс и занимает несколько минут toocomplete.
   
    ![Отключение выполняется](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. После деактивации обновляет hello список устройств.
   
    ![Отключение завершено](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    Теперь устройство можно удалить.

## <a name="delete-hello-device"></a>Удаление устройства hello

Устройство имеет первый деактивированный toodelete toobe его. При удалении устройства удаляется из списка hello службы toohello подключенных устройств. Hello службы могут больше не сможете управлять hello удалить устройство. Однако Hello данные, связанные с устройством hello остается в облаке hello. За эти данные будет взиматься плата.

toodelete hello устройства, выполните следующие шаги hello.

#### <a name="toodelete-hello-device"></a>устройство toodelete hello

1. В вашей StorSimple диспетчер устройств, перейдите в слишком**управления > устройства**. В hello **устройств** колонке выберите деактивированное устройство, что вы хотите toodelete.
2. В hello **панели мониторинга устройства** колонка, щелкните **... Дополнительные** и нажмите кнопку **удалить**.
   
   ![Выберите устройство toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. В hello **удаление** колонки, имя типа hello удалять hello tooconfirm устройства и нажмите кнопку **удалить**. Идет удаление устройства hello не удаляет hello облачные данные, связанные с устройством hello. 
   
   ![Подтверждение удаления](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. Удаление Hello запускается, занимающий toocomplete несколько минут.
   
   ![Удаление выполняется](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    После удаления устройства hello, можно просмотреть hello обновить список устройств.

## <a name="next-steps"></a>Дальнейшие действия

* Сведения о том, как toofail, перейти слишком[отработки отказа и аварийного восстановления виртуального массива StorSimple](storsimple-virtual-array-failover-dr.md).

* Дополнительные сведения о toolearn как hello toouse службы диспетчера StorSimple устройство go слишком[используйте hello tooadminister службы диспетчера StorSimple устройство виртуального массива StorSimple](storsimple-virtual-array-manager-service-administration.md). 

