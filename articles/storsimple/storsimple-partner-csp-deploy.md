---
title: "aaaMicrosoft Azure StorSimple и обзор программы поставщика облачных решений | Документы Microsoft"
description: "Общие сведения о hello StorSimple и CSP для партнеров StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a>Развертывание виртуального массива StorSimple для программы поставщика облачных решений

## <a name="overview"></a>Обзор

Можно развернуть StorSimple Virtual Array hello партнеры поставщика облачных решений (CSP) для своих клиентов. Партнер CSP может создать службу диспетчера устройств StorSimple. Эту службу можно использовать toodeploy и управление StorSimple Virtual Array и hello связанных общих папок, томов и резервных копий.

В этой статье описывается, как можно добавить клиента или нового клиента существующие подписки tooan CSP партнера, а затем создать toodeploy службы StorSimple Virtual Array в CSP.

## <a name="prerequisites"></a>Предварительные требования

Перед началом работы убедитесь, что выполнены следующие условия:

- Вы зарегистрированы в рамках программы hello CSP.
- У вас есть допустимые учетные данные для входа в [Центр партнеров](http://partnercenter.microsoft.com/). Hello учетные данные позволяют toosign toohello партнера портала tooadd клиентов, искать клиентов или перейдите tooa учетной записи клиента из hello мониторинга для партнеров. Hello CSP могут функционировать как администратор StorSimple от имени клиента hello в hello портал Azure.
                             
## <a name="add-a-customer"></a>Добавление клиента

При добавлении клиента автоматически создается подписка. tooadd клиента (и автоматически создавать подписки), выполните следующие действия на портале партнера hello hello.

1. Go toohello [партнерском центре](http://partnercenter.microsoft.com/) и войдите с использованием учетных данных поставщика служб Шифрования. Нажмите на кнопку **Панель мониторинга**.

     ![Панель мониторинга в Центре партнеров](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. В hello левой панели щелкните **клиентов**. В hello на правой панели щелкните **добавить клиентов**. Введите сведения о hello hello клиента. Нажмите кнопку **далее: подписки** toocreate подписки клиента.

    ![Добавление клиента](./media/storsimple-partner-csp-deploy/image2.png)

3.  Выберите предложение **Microsoft Azure**. Scroll toohello нижней части страницы приветствия и нажмите кнопку **проверки**.

    ![Просмотр сведений о подписке](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. Просмотрите сведения hello и нажмите кнопку **отправить**.

    ![Отправка подписки](./media/storsimple-partner-csp-deploy/image4.png)

5. Сохраните сведения о подтверждении hello для дальнейшего использования.

    ![Сохранение подтверждения](./media/storsimple-partner-csp-deploy/image5.png)

6. Найдите или перейдите toohello клиента, для которого был только что добавлен. Нажмите кнопку hello **название компании** toodrill работу в детали hello.

    ![Поиск приветствия клиента](./media/storsimple-partner-csp-deploy/image6.png)  

7. В hello левой панели выберите **управление службой**. В hello на правой панели в разделе **администрировать службы**, нажмите кнопку **Microsoft Azure Management Portal** toosign в Azure администратору клиента.

    ![Войдите в портал tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. Щелкните toocreate диспетчера устройств StorSimple, **+ создать** и поиска или перехода слишком**серией виртуальных устройств StorSimple**. Дополнительные сведения см. слишком[развертывание службы диспетчера StorSimple устройство](storsimple-virtual-array-manage-service.md).

    ![Создание службы диспетчера устройств StorSimple](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a>Добавление подписки

В некоторых случаях может быть существующим клиентом, и требуется, чтобы tooadd подписки. tooadd tooan существующий клиент подписки, выполнить следующие шаги на портале партнера hello hello.

1. Go toohello [партнерском центре](http://partnercenter.microsoft.com/) и войдите с использованием учетных данных поставщика служб Шифрования. Нажмите на кнопку **Панель мониторинга**.

     ![Панель мониторинга в Центре партнеров](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. В hello левой панели щелкните **клиентов**. Найдите или перейдите toohello клиента, для которого требуется задать подписку на tooadd. Нажмите кнопку hello ![значок проверки развертывания](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) строку hello tooexpand значок для hello название компании для вашего клиента. В сведениях о hello, нажмите кнопку **добавить подписки**.

    ![Клиенты](./media/storsimple-partner-csp-deploy/image10.png)

3. Проверьте **Microsoft Azure** для hello **предложения Top** в hello подписки и нажмите кнопку **отправить**. После этого будет создана подписка.

    ![Добавление новой подписки](./media/storsimple-partner-csp-deploy/image11.png)

6. После создания новой подписки щелкните **<--клиентов** в левой области tooreturn toohello hello **клиентов** страницы. Поиск hello клиента, для которого вы только что создали подписки. Нажмите кнопку hello **название компании** toodrill работу в детали hello.

    ![Поиск приветствия клиента](./media/storsimple-partner-csp-deploy/image6.png)  

7. В hello левой панели выберите **управление службой**. В hello на правой панели в разделе **администрировать службы**, нажмите кнопку **Microsoft Azure Management Portal** toosign в Azure администратору клиента.

    ![Войдите в портал tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. Щелкните toocreate диспетчера устройств StorSimple, **+ создать** и поиска или перехода слишком**серией виртуальных устройств StorSimple**. Дополнительные сведения см. слишком[развертывание службы диспетчера StorSimple устройство](storsimple-virtual-array-manage-service.md).

    ![Создание службы диспетчера устройств StorSimple](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a>Дальнейшие действия

- Если у вас есть дополнительные вопросы о hello StorSimple CSP, перейдите в слишком[StorSimple в CSP: часто задаваемые вопросы](storsimple-partner-csp-faq.md).
- В случае готовности toodeploy StorSimple, go слишком[развертывания StorSimple в CSP](storsimple-partner-csp-deploy.md).
