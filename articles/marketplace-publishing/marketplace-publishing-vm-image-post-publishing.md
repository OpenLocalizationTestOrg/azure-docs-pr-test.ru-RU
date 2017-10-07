---
title: "образ виртуальной машины в Azure Marketplace hello aaaManaging | Документы Microsoft"
description: "Подробное руководство о том, как toomanage ваш образ виртуальной машины hello Azure Marketplace после первоначальной публикации"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a>Распространение руководство для виртуальной машины, предлагает в hello Azure Marketplace
В этой статье объясняется, как можно обновить предложение виртуальной машины в Azure Marketplace hello. Оно поможет hello процесс добавления одного или нескольких новых SKU tooan существующее предложение. Он также поможет выполнить hello удаляется из hello Marketplace предложение виртуальной машины или номера SKU.

После предложения и SKU на промежуточное хранение в hello [портал Azure](http://portal.azure.com), невозможно изменить hello следующие текстовые поля:

* **Предложить идентификатор**: В hello публикацию портала, go слишком**виртуальные машины** и выберите ваше предложение. Щелкните **Образы VM** > **Offer Identifier** (Идентификатор предложения).
* **Идентификатор SKU**: В hello публикацию портала, go слишком**виртуальные машины** и выберите ваше предложение. Щелкните **SKUS** (Номера SKU) > **Add a SKU** (Добавить SKU).
* **Пространство имен издателя**: В hello публикацию портала, go слишком**виртуальные машины** > **Пошаговое руководство** > **сообщить нам о вашей компании** (см. в разделе «Шаг 2 регистрации вашей компании») > **пространство имен издателя** > **пространства имен**.

После предложения hello и SKU, перечисленные в hello [Marketplace](http://azure.microsoft.com/marketplace), невозможно изменить hello следующие текстовые поля:

* **Предложить идентификатор**: В hello публикацию портала, go слишком**виртуальные машины** и выберите ваше предложение. Щелкните **Образы VM** > **Offer Identifier** (Идентификатор предложения).
* **Идентификатор SKU**: В hello публикацию портала, go слишком**виртуальные машины** и выберите ваше предложение. Щелкните **SKUS** (Номера SKU) > **Add a SKU** (Добавить SKU).
* **Пространство имен издателя**: В hello публикацию портала, go слишком**виртуальные машины** > **Пошаговое руководство** > **сообщить нам о вашей компании** (см. в разделе «Шаг 2 регистрации») **Пространство имен издателя** > **пространства имен**.
* **Порты**: В hello публикацию портала, go слишком**виртуальные машины** и выберите ваше предложение. Щелкните **Образы VM** > **Open Ports** (Открыть порты).
* **Pricing Change of listed SKU(s)** (Изменение цены указанных SKU).
* **Billing Model Change of listed SKU(s)** (Изменение модели выставления счетов указанных SKU).
* **Removal of billing regions of listed SKU(s)**
* **Число перечисленных SKU(s) диск изменяющихся данных hello**

## <a name="update-hello-technical-details-of-a-sku"></a>Обновить hello технические детали SKU
tooadd новый toohello версии перечисленных SKU и повторно опубликовать вашего предложения, выполните следующие действия:

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).
2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **ОБРАЗОВ виртуальных Машин** вкладки.
4. В hello **SKU** найдите hello, которые должны tooupdate SKU.
5. Добавить новый номер версии для hello SKU и выберите hello  **+**  кнопки. Новая версия Hello должно быть в формате X.Y.Z, где X, Y и Z являются целыми числами. Версии нужно изменять только пошагово в сторону увеличения.
6. В hello **URL-адрес виртуального жесткого диска ОС** введите hello подписанного URL-адреса URI создан для операционной системы hello виртуального жесткого диска и сохранить изменения hello.

   > [!IMPORTANT]
   > Вы не инкремента или декремента hello число дисков данных из перечисленных SKU. В этом случае необходимо toocreate новая Конфигурация. Подробные инструкции см. в разделе toohello [добавьте новая Конфигурация в рамках перечисленных предложения](#add-a-new-sku-under-a-listed-offer).
   >
   >
7. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

    ![Образы виртуальных машин](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a>Обновить сведения нетехнический hello предложение или SKU
Вы можете обновить нетехнический hello (маркетинга, юридической и технической поддержки, категории) сведения о динамической предложение или Конфигурация в hello Marketplace.

### <a name="update-hello-offer-description-and-logos"></a>Обновить описание предложения hello и эмблем
tooupdate hello подробные сведения о предложении и повторно опубликовать вашего предложения, выполните следующие действия:

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).
2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **МАРКЕТИНГА** вкладки.
4. Щелкните **English (US)** (Английский (США)).
5. Нажмите кнопку hello **сведения** вкладки. В hello **описание** раздел, предложение update hello **заголовок**, **Сводка**, и **ДЛИННАЯ Сводка** и сохранить изменения hello.

   > [!NOTE]
   > При обновлении hello подробности номера SKU, следует учитывать эти ограничения. 
   * Не вводите повторяющийся текст hello описание предложения и описание SKU hello.
   * Не вводите повторяющийся текст для заголовка SKU hello и полная Сводка предложение hello. 
   * Не вводите повторяющийся текст hello SKU название и описание предложения hello.
   >
   >

    ![Сведения](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. В hello **ЭМБЛЕМЫ** раздел hello **сведения** измените hello эмблемы. Переходить по эмблемы hello hello [рекомендации Azure Marketplace](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).

   > [!NOTE]
   > Имиджевый логотип необязательный. Вы можете не tooupload значок героя. Однако после отправки значок героя нет не toodelete подготовить его из hello публикацию портала. Выполните hello [рекомендации значок героя](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
   >
   >
7. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

    ![Логотипы](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a>Обновите описание SKU hello
hello tooupdate SKU сведений и повторно опубликуйте вашего предложения, выполните следующие действия.

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).
2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **МАРКЕТИНГА** вкладки.
4. Щелкните **English (US)** (Английский (США)).
5. Нажмите кнопку hello **ПЛАНЫ** вкладки. В hello **SKU** статьи, обновите hello SKU **заголовок**, **Сводка**, и **описание** и сохранить изменения hello.

   > [!NOTE]
   > При обновлении hello подробности номера SKU, следует учитывать эти ограничения. 
   * Не вводите повторяющийся текст hello описание предложения и описание SKU hello. 
   * Не вводите повторяющийся текст для заголовка SKU hello и полная Сводка предложение hello. 
   * Не вводите повторяющийся текст hello SKU название и описание предложения hello.
   >
   >
6. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

    ![Планы](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a>Изменение имеющихся ссылок или добавление новых
существующие ссылки toochange или добавить новые связи, а затем повторно опубликовать ваше предложение, выполните следующие действия:

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).
2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **МАРКЕТИНГА** вкладки.
4. Щелкните **English (US)** (Английский (США)).
5. Нажмите кнопку hello **ссылки** вкладки.
6. tooadd новую ссылку в hello **ссылки** щелкните **+ добавить ССЫЛКУ**. В hello **ссылку Добавить** диалогового окна введите ссылку hello **заголовок** и **URL-адрес** и сохранить изменения hello. Вы можете ввести любую ссылку, содержащую сведения, которые могут помочь клиентам.
7. tooupdate или удалить существующую связь, выберите ссылку hello и щелкните hello **изменить** кнопки или hello **удалить** кнопки.

   > [!NOTE]
   > Проверьте, hello ссылки, введенные в этом разделе работают надлежащим образом, так как эти ссылки, получить проверяются во время процесса запроса на вашей рабочей среде.
   >
   >
8. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

    ![Ссылки](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![Добавление ссылки](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a>Изменение имеющегося примера изображения или добавление нового
toochange существующего образца изображения или добавлять новые образы образец и затем повторно опубликовать вашего предложения, выполните следующие действия:

> [!NOTE]
> Только один образец изображение отображается в hello [портал Azure](https://portal.azure.com).
>
>

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).
2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **МАРКЕТИНГА** вкладки.
4. Щелкните **English (US)** (Английский (США)).
5. Нажмите кнопку hello **ОБРАЗЦОВ ИЗОБРАЖЕНИЙ** вкладки.
6. новый образ образца в hello tooadd **образцов изображений** щелкните **отправить новый образ** и сохранить изменения hello.

   > [!NOTE]
   > Включать примеры изображения необязательно.
   >
7. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

    ![Примеры изображений](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a>Обновление содержимого юридических hello
tooupdate Здравствуйте содержимого и повторно опубликовать вашего предложения, выполните следующие действия:

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).
2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **МАРКЕТИНГА** вкладки.
4. Щелкните **English (US)** (Английский (США)).
5. Нажмите кнопку hello **ЮРИДИЧЕСКИХ** вкладки. В hello **юридических** статьи, обновлять политики и условия использования. Введите или вставьте hello политики и условия в hello **условия использования** и сохраните изменения hello.
6. Hello символ hello юридические условия использования ограничен 1 миллиона символов.
7. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

    ![Юридическая информация](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a>Обновить сведения о поддержке hello
tooupdate hello сведения о поддержке и повторно опубликовать вашего предложения, выполните следующие действия:

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).
2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **поддержки** вкладки.
4. В hello **Engineering обратитесь** статьи hello реконструирования контактные сведения об обновлении. Эти сведения используются для внутренней связи между партнером hello и Microsoft только.
5. В hello **поддержки** статьи, обновите контактные сведения о поддержке hello и hello **URL-адрес поддержки**. Эти сведения используются для внутренней связи между партнером hello и Microsoft только.

   > [!NOTE]
   > Если требуется поддержка по электронной почте только tooprovide введите номер телефона фиктивный в hello **поддержки** раздела. В этом случае вместо него используется hello электронной почты вы указали.
   >
   >
6. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

    ![Поддержка](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a>Обновить категории hello
hello tooupdate категорий, в разделе ваше предложение и повторно опубликовать ваше предложение выполните следующие действия.

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).
2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **категории** вкладки.
4. В hello **категории** щелкните обновление hello категорий для вашего предложения, сохранить изменения hello. Для выбора toofive категорий для галереи hello Azure Marketplace.
5. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
6. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

    ![Категории](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a>Добавление нового SKU во внесенное в список предложение
tooadd новая Конфигурация в режиме реального времени предложение, выполните следующие действия.

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).
2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **номера SKU** вкладки. Затем щелкните **Add a SKU** (Добавить номер SKU). 
4. В диалоговом окне приветствия введите **идентификатор SKU** в нижнем регистре. Выберите hello **предоставляют свои собственные модель выставления счетов лицензии (BYOL)** флажок, если вы хотите toopublish hello новая Конфигурация BYOL модель выставления счетов. В противном случае снимите флажок "hello". Щелкните toocreate знак деления hello новая Конфигурация. Если не выбрать модель выставления счетов BYOL hello, hello выставления счетов автоматически устанавливается модель toohourly. Hello 30-дневную бесплатную пробную версию для hello почасовой модели выставления счетов, установите **один месяц** для **доступна бесплатная пробная версия?** В противном случае выберите **Нет пробной версии**. (**Доступна бесплатная пробная версия?**  отображается только в том случае, если вы не выбрали BYOL во время создания hello новая Конфигурация.)

   > [!IMPORTANT]
   > **Скрыть этот SKU из hello Marketplace, так как он должен всегда купил через шаблон решения** должно быть **Да** *только* Если утверждения для публикации шаблона решения. В противном случае для этого параметра всегда должно быть задано значение **Нет**.
   >
   >
4. В меню hello hello левой части экрана выберите hello **ОБРАЗОВ виртуальных Машин** вкладку, чтобы узнать hello новая Конфигурация, созданный вами.
5. tooset до hello новая Конфигурация см. в разделе [на получение сертификата для образа виртуальной Машины](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) рекомендации.
6. маркетинговые материалы по tooadd hello новая Конфигурация см. в разделе [предоставляют Marketplace маркетинг содержимое](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
7. сведения о ценах на tooadd hello новая Конфигурация см. в разделе [задать цен](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).
8. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

    ![Номера SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![Добавление номера SKU](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a>Изменить количество дисков данных hello перечисленных SKU
Вы не инкремента или декремента hello число дисков данных из перечисленных SKU. В этом случае необходимо toocreate новая Конфигурация. Подробные инструкции см. в разделе toohello [добавьте новая Конфигурация в рамках перечисленных предложения](#add-a-new-sku-under-a-listed-offer).

## <a name="delete-a-listed-offer-from-hello-marketplace"></a>Удаляет предложение перечисленных из hello Marketplace
Различные аспекты должны toobe занимается в случае, когда hello tooremove запрос динамического предложения. руководство tooget из tooremove группы поддержки hello перечисленных предложения от hello Marketplace, выполните следующие действия.

1. Создавать запрос в службу поддержки на hello [создать инцидент](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) страницы.

2. В качестве **типа проблемы** выберите **Managing offers** (Управление предложениями), а в качестве **категории** — **Modifying an offer and/or SKU already in production** (Изменение предложения и/или SKU, которые уже находятся в рабочей среде).
3. Запрос "hello".

Группа поддержки Hello помогает выполнить процесс удаления предложения и SKU hello.

> [!NOTE]
> Всегда можно удалить предложение hello, когда оно находится в состоянии черновика (но не тестовой или производственной). На hello **ЖУРНАЛ** щелкните **ОТМЕНИТЬ черновик**.
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a>Удалить указанные SKU из hello Marketplace
toodelete указанные SKU из hello Marketplace, выполните следующие действия.

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).

2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В области hello hello левой части экрана щелкните hello **номера SKU** вкладки.
4. Выберите hello SKU, toodelete и щелкните hello **удалить** кнопки.
5. Go toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish предложение hello в hello Marketplace.
6. После предложения hello повторной публикации в hello Marketplace, hello SKU удаляется из hello Marketplace и hello портал Azure.

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a>Удаление текущей версии перечисленных SKU hello из hello Marketplace
toodelete hello текущей версии перечисленных SKU из hello Marketplace, выполните следующие действия. 

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).

2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **ОБРАЗОВ виртуальных Машин** вкладки.
4. Выберите hello SKU которого текущей версии toodelete и щелкните hello **удалить** кнопки.
5. Go toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish предложение hello в hello Marketplace.
6. После предложения hello возвращает повторной публикации в hello Marketplace hello текущей версии hello перечисленных SKU будет удалена из hello Marketplace и hello портал Azure. Hello SKU затем откатывается tooits предыдущей версии.

## <a name="revert-hello-listing-price-tooproduction-values"></a>Отменить вывод значения цен tooproduction hello
значения tooproduction цен листинг hello toorevert, выполните следующие действия.

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).
2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **ЦЕНЫ** вкладки.
4. Выберите регион, стоимость использования которой требуется tooreset.

    ![Регионы с ценами](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. Для номера SKU с моделью почасовой оплаты сбросьте hello цен для всех ядер hello в рабочей среде для выбранного региона hello. Для номера SKU с моделью выставления счетов BYOL сделать hello SKU в регионе hello, установив флажок hello SKU hello в hello **EXTERNALLY-LICENSED (BYOL) SKU ДОСТУПНОСТИ** раздела.

    ![Модели ценообразования](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. Щелкните **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES** (Автоматически назначить цены для других рынков на основе цен в США).

   > [!NOTE]
   > Подпись кнопки Hello может отличаться в зависимости от региона hello, выбранный. Так как мы выбрали США, кнопка hello обозначается **AUTOPRICE другие РЫНКИ ОСНОВЕ ON ЦЕН в ПОДРОБНОЙ**.
   >
   >

    ![Автоматическое назначение цен](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. На 1 hello Autoprice мастера, выберите базовый рынка hello и нажмите кнопку hello **стрелка** кнопки.

    ![Базовый рынок](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. На странице 2 выберите планов обслуживания и метрах (ядра) и щелкните hello **стрелка** кнопки.

    ![Планы обслуживания и единицы измерения](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. На странице 3 щелкните **переключить все** tooselect всех регионов. Если необходимо выбрать конкретные регионы, можно установить для них флажки вручную. Нажмите кнопку hello **стрелка** кнопки.

    ![Выбор рынков](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. На странице 4, просмотрите hello обменные курсы и нажмите кнопку **Готово**. Мастер Hello сбрасывает hello цены соответствующим tooyour выбранных элементов.

11. На hello **ЦЕНЫ** щелкните **изменения ПРЕДСТАВЛЕНИЯ СВОДКИ и**.
    В разделе **View Version** (Просмотр версии) выберите **Черновик**, а в **Сравнить с** — **Рабочая среда**. При появлении разницы нет цены, цены hello успешно возвращены значения toohello рабочей.

    ![Просмотр сводки и изменений](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
13. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

## <a name="revert-hello-billing-model-tooproduction-values"></a>Вернуть hello значения tooproduction модели выставления счетов
toorevert hello выставления счетов tooproduction значения модели, выполните следующие действия.

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).

2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **номера SKU** вкладки.
4. Нажмите кнопку hello **изменить** модели выставления счетов hello toorevert кнопки. В открывшемся окне приветствия, установите или снимите hello **выставления счетов и лицензирование извне выполняется из Azure (также называемого перевести собственной лицензии)** флажок.

    ![Изменение выставления счетов](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. Выполните действия hello «Revert вывод значения цен tooproduction hello» в этой статье.
6. Go toohello **публикации** и нажмите кнопку **tooSTAGING ПРИНУДИТЕЛЬНОЙ**. Подробное руководство по тестированию ваше предложение в промежуточной среде hello см. в разделе [протестировать ваше предложение виртуальной Машины для hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. После тестирования ваше предложение в промежуточной, перейдите toohello **публикации** на вкладке hello публикацию портала. Нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a>Отменить параметр видимости hello перечисленных toohello рабочее значение SKU
параметр видимости hello toorevert перечисленных SKU toohello производства значение, выполните следующие действия.

1. Войдите в toohello [публикацию портала](https://publish.windowsazure.com).

2. Go toohello **виртуальные машины** и выберите ваше предложение.
3. В меню hello hello левой части экрана выберите hello **номера SKU** вкладки.
4. Выберите ваш SKU и вернуть параметр видимости hello hello SKU toohello рабочее значение.

    ![Видимость](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. После завершения работы с hello изменения, нажмите кнопку **tooPRODUCTION tooPUSH ЗАПРОСИТЬ УТВЕРЖДЕНИЕ** toorepublish ваше предложение в hello Marketplace.

## <a name="see-also"></a>См. также
* [Get Started: Публикация toohello предложение Azure Marketplace](marketplace-publishing-getting-started.md)
* [Основная информация об отчетах о выплатах Azure Marketplace](marketplace-publishing-report-payout.md)
* [Просмотр и изменение статуса участия в программе поощрения поставщиков облачных решений в Azure Marketplace](marketplace-publishing-csp-incentive.md)
* [Устранение неполадок публикации в Marketplace hello](marketplace-publishing-support-common-issues.md)
* [Поддержка издателей](marketplace-publishing-get-publisher-support.md)
* [Локальная разработка образа виртуальной машины для Azure Marketplace](marketplace-publishing-vm-image-creation-on-premise.md)
* [Создание виртуальной машины под управлением Windows, на портале Azure предварительной версии hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
