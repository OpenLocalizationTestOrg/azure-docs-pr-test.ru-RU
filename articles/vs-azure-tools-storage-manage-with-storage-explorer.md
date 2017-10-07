---
title: "aaaGet работы с обозреватель хранилищ (Предварительная версия) | Документы Microsoft"
description: "Управление ресурсами хранилища Azure с помощью обозревателя хранилищ (предварительная версия)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a>Приступая к работе с обозревателем службы хранилища (предварительная версия)
## <a name="overview"></a>Обзор
Azure Storage Explorer (Предварительная версия) имеет отдельное приложение, позволяющее tooeasily работы с данными хранилища Azure для Windows, macOS и Linux. В этой статье вы узнаете hello различные способы соединения tooand управление учетных записей хранилища Azure.

![Обозреватель службы хранилища Microsoft Azure (предварительная версия)][15]

## <a name="prerequisites"></a>Предварительные требования
* [Скачайте и установите обозреватель службы хранилища (предварительная версия).](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a>Подключите tooa учетной записи хранилища или службы
Обозреватель хранилищ (Предварительная версия) предоставляет несколько способов tooconnect toostorage счетов. Вот что вы можете, к примеру, делать:
* Подключите toostorage учетные записи, связанные с подписками Azure.
* Подключение toostorage учетных записей и служб, которые являются общими из подписок Azure.
* Подключение tooand управление локальным хранилищем с помощью hello эмулятор хранилища Azure. 

Можно также работать с учетными записями хранения в глобальной и национальной среде Azure.

* [Подключение tooan подписки Azure](#connect-to-an-azure-subscription): управлять ресурсами, которые принадлежат tooyour подписки Azure.
* [Работать с локальной разработки хранилища](#work-with-local-development-storage): управление локальным хранилищем с помощью hello эмулятор хранилища Azure.
* [Подключить хранилище tooexternal](#attach-or-detach-an-external-storage-account): управлять ресурсами, которые принадлежат tooanother подписки Azure или, находящиеся в национальной облаков Azure, используя имя учетной записи хранилища hello, ключ и конечных точек.
* [Добавить учетную запись хранилища с помощью SAS](#attach-storage-account-using-sas): управление ресурсами хранилища, которые принадлежат tooanother подписки Azure с помощью подписанного URL-адреса (SAS).
* [Присоединение службы с помощью SAS](#attach-service-using-sas): управление службой носителей (контейнер больших двоичных объектов, очереди или таблицы), к которому относится tooanother подписки Azure с помощью SAS.

## <a name="connect-tooan-azure-subscription"></a>Подключение tooan подписки Azure
> [!NOTE]
> Если у вас нет учетной записи Azure, [зарегистрируйтесь для работы с бесплатной пробной версией](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. В обозревателе хранилищ (предварительная версия) выберите раздел **Параметры учетной записи Azure**.

    ![Параметры учетной записи Azure][0]

2. Hello левая панель содержит все учетные записи Microsoft hello, вы вошли. tooconnect tooanother учетной записи выберите **добавить учетную запись**, а затем следуйте hello toosign инструкции с учетной записью Майкрософт, которая связана с по крайней мере одну подписку Azure.

    >[!NOTE]
    >Подключение toonational Azure (например, Германии Azure, Azure для государственных и Azure China через вход) в настоящее время не поддерживается. Hello. в разделе «присоединение или отключение учетной записи внешнего хранилища» как в разделе учетных записей хранилища Azure toonational tooconnect.

3. После успешной регистрации учетную запись Майкрософт, hello слева, панель заполняется hello Azure подписок, связанных с этой учетной записи. Здравствуйте, выберите подписки Azure, которые вы хотите toowork с, а затем выберите **применить**. (При выборе **все подписки** переключатели, выбрав все или никакие из hello в списке подписок Azure.)

    ![Выбор подписок Azure][3]  
    Hello левая панель отображает связанные с подписками Azure hello выбранные учетные записи хранения hello.

    ![Выбранные подписки Azure][4]

## <a name="connect-tooan-azure-stack-subscription"></a>Подключение подписки tooan стек Azure

Сведения о подключении подписки tooan стека Azure см. в разделе [tooan подключить обозреватель хранилища Azure стека подписки](azure-stack/azure-stack-storage-connect-se.md).

## <a name="work-with-local-development-storage"></a>Работа с локальным хранилищем разработки
Обозреватель хранилищ (Предварительная версия) позволяет работать для локального хранилища с помощью hello эмулятор хранилища Azure. Такой подход позволяет писать код на соответствие и хранения данных тестирования не имея учетной записи хранилища, развернутое в Azure, так как учетная запись хранения hello эмулируется по hello эмулятор хранилища Azure.

> [!NOTE]
> Hello эмулятор хранилища Azure в настоящее время поддерживается только для Windows.
>
>

1. Hello левой панели проводника хранилищ (Предварительная версия), разверните hello **(локальное и присоединенные)** > **учетные записи хранения** > **(разработка)** узла.

    ![Узел локальной разработки][21]

2. Hello эмулятор хранилища Azure еще не установлен, имеется ли запрос toodo так через информационной панели. Если hello информационная панель отображается, выберите **Загрузка последней версии hello**и затем установить эмулятор hello.

    ![Строка эмулятора хранения Azure с предложением скачать последнюю версию][22]

3. После установки эмулятора hello, можно создать и работать с локальной больших двоичных объектов, очередей и таблиц. toolearn как тип toowork с каждой учетной записи хранилища, см. в одном hello следующее:

    * [Управление ресурсами хранилища BLOB-объектов Azure](vs-azure-tools-storage-explorer-blobs.md)
    * Управление ресурсами хранилища файловых ресурсов Azure — *ожидается в ближайшее время*.
    * Управление ресурсами хранилища очередей Azure — *ожидается в ближайшее время*.
    * Управление ресурсами хранилища таблиц Azure — *ожидается в ближайшее время*.

## <a name="attach-or-detach-an-external-storage-account"></a>Присоединение и отсоединение учетной записи внешнего хранилища
С помощью обозревателя хранилища (Предварительная версия) можно присоединить tooexternal учетных записей хранилища, чтобы учетные записи хранения можно было легко совместно. В этом разделе объясняется, как tooattach too(and detach from) учетные записи внешнего хранилища.

### <a name="get-hello-storage-account-credentials"></a>Получить учетные данные хранилища hello
tooshare учетной записи внешнего хранилища hello владельца этой учетной записи необходимо сначала получить hello учетные данные (имя учетной записи и ключ) для учетной записи hello и затем предоставить эти сведения hello, кто хочет учетной записи tooattach toothat (внешнего). Учетные данные хранилища hello через портал Azure hello можно получить, выполнив hello ниже:

1. Войдите в toohello [портал Azure](https://portal.azure.com).

2. Щелкните **Обзор**.

3. Выберите **Учетные записи хранения**.

4. На hello **учетные записи хранения** колонки, выберите hello требуемой учетной записи хранилища.

5. На hello **параметры** колонке hello выбранную учетную запись хранилища, выберите **ключи доступа**.

    ![Варианты ключей доступа][5]

6. На hello **ключи доступа** колонки, hello копирования **имя учетной записи хранения** и **key1** значения для использования при присоединении toohello учетной записи хранилища.

    ![Ключи доступа][6]

### <a name="attach-tooan-external-storage-account"></a>Присоединение tooan учетной записи внешнего хранилища
учетной записи внешнего хранилища tooan tooattach, необходимо имя и ключ учетной записи hello. раздел «Get hello учетные данные хранилища» Hello объясняется, как эти значения из tooobtain hello портал Azure. Однако портал hello hello ключ учетной записи называется **key1**. Поэтому там, где обозреватель хранилищ (Предварительная версия) запрашивает ключ учетной записи, введите hello **key1** значение.

1. В обозревателе хранилищ (Предварительная версия), выберите **подключения хранилища tooAzure**.

    ![Параметр хранения tooAzure подключения][23]

2. В hello **подключения tooAzure хранилища** диалоговом окне укажите ключ учетной записи hello (hello **key1** значение из hello портал Azure) и выберите **Далее**.

    > [!NOTE]
    > Можно вводить строки подключения к хранилищу hello из учетной записи хранения в национальной Azure. Например учетные записи хранения Германия tooAzure tooconnect, введите соединения строки аналогичные toohello следующие данные: 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<storage_account_key>
    >* EndpointSuffix=core.cloudapi.de
    
    >Можно получить строки подключения hello hello Azure портала в hello таким же, как описано в hello раздел «Получить учетные данные хранилища hello».

    ![Подключение хранилища tooAzure-диалоговое окно][24]

3. В hello **присоединить внешнее хранилище** диалогового окна hello **имя учетной записи** введите имя учетной записи хранения hello, укажите нужные параметры и затем выберите **Далее**.

    ![Диалоговое окно присоединения внешнего хранилища][8]

4. В hello **Сводка по соединению** диалогового окна поле, проверьте сведения о hello. Toochange всего, установите **обратно** и снова введите параметры требуемого hello. 

5. Нажмите кнопку **Подключиться**.

6. После успешного подключения учетной записи внешнего хранилища hello отображается с **(внешнего)** добавляется toohello имя учетной записи хранения.

    ![Результат подключения учетной записи внешнего хранилища tooan][9]

### <a name="detach-from-an-external-storage-account"></a>Отсоединение учетной записи внешнего хранилища
1. Щелкните правой кнопкой мыши hello учетной записи внешнего хранилища требуется toodetach, а затем выберите **отсоединения**.

    ![Вариант отсоединения от хранилища][10]

2. Сообщения о подтверждении hello выберите **Да** tooconfirm hello отсоединение от учетной записи внешнего хранилища hello.

## <a name="attach-a-storage-account-by-using-an-sas"></a>Присоединение учетной записи хранения с помощью SAS
[SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) позволяет Здравствуйте, администратор подписки Azure предоставьте учетной записи хранилища tooa временный доступ без необходимости учетные данные tooprovide подписки Azure.

tooillustrate этот сценарий, давайте предположим, пользователь UserA является администратором, подписка Azure, и UserA хочет tooaccess UserB tooallow учетную запись хранилища в течение ограниченного времени с определенными разрешениями:

1. Пользователь UserA приводит к возникновению ошибки SAS (состоящие из hello строку подключения для учетной записи хранения hello) на определенное время период и с hello требуемого разрешения.

2. Общие папки пользователя UserA hello SAS с hello пользователь (в нашем примере UserB), который должен учетной записи хранилища toohello доступа.  

3. Пользователь б использует обозреватель хранилищ (Предварительная версия) tooattach toohello счет принадлежит tooUserA с помощью hello указан SAS.

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a>Получить SAS для hello имени учетной записи которого tooshare
1. В обозревателе хранилищ (Предварительная версия), щелкните правой кнопкой мыши учетную запись хранения hello, нужно совместно использовать, а затем выберите **получить подпись общего доступа**.

    ![Вариант получения SAS в контекстном меню][13]

2. В hello **подписи общего доступа** диалоговом окне укажите hello промежуток времени, а также разрешения для учетной записи hello, а затем выберите **создать**.

    ![Диалоговое окно получения SAS][14]  
    Hello **подписи общего доступа** диалоговое окно открывается и отображает hello SAS.

3. Далее toohello **строка подключения**выберите **копирования** toocopy его toohello буфер обмена и выберите **закрыть**.

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a>Присоединение toohello общей учетной записи с помощью hello SAS
1. В обозревателе хранилищ (Предварительная версия), выберите **подключения хранилища tooAzure**.

    ![Параметр хранения tooAzure подключения][23]

2. В hello **подключения tooAzure хранения** диалоговое окно, укажите строку подключения hello, а затем выберите **Далее**.

    ![Подключение хранилища tooAzure-диалоговое окно][24]

3. В hello **Сводка по соединению** диалогового окна поле, проверьте сведения о hello. Выберите изменения toomake **обратно**и введите параметры hello. 

4. Нажмите кнопку **Подключиться**.

5. После присоединения, hello учетной записи хранилища отображается с **(SAS)** добавляется предоставленное имя учетной записи toohello.

    ![Результат вложенного tooan учетной записи с помощью SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a>Присоединение службы с помощью SAS
раздел «Присоединения» учетной записи хранилища с помощью SAS Hello поясняет, как администратор подписки Azure можно предоставить учетной записи хранилища tooa временный доступ путем создания и совместного использования SAS для учетной записи хранения hello. Аналогичным образом SAS можно создать для конкретной службы (контейнера больших двоичных объектов, очереди или таблицы) в учетной записи хранилища.  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a>Создать SAS для hello службы, которые должны tooshare
В этом контексте служба может быть контейнером больших двоичных объектов, очередью или таблицей. hello toogenerate SAS для перечисленных службы, см.:

* [Получить hello SAS для контейнера больших двоичных объектов](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Получить hello SAS для общей папки: *ожидается в ближайшее время*
* Получить hello SAS для очереди: *ожидается в ближайшее время*
* Получить hello SAS для таблицы: *ожидается в ближайшее время*

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a>Подключите общие toohello учетную запись службы с помощью hello SAS
1. В обозревателе хранилищ (Предварительная версия), выберите **подключения хранилища tooAzure**.

    ![Параметр хранения tooAzure подключения][23]

2. В hello **подключения tooAzure хранения** диалоговое окно, укажите hello универсальный код Ресурса SAS, а затем выберите **Далее**.

    ![Подключение хранилища tooAzure-диалоговое окно][24]

3. В hello **Сводка по соединению** диалогового окна поле, проверьте сведения о hello. Выберите изменения toomake **обратно**и введите параметры hello. 

4. Нажмите кнопку **Подключиться**.

5. После присоединения, hello присоединенную службы отображается под hello **(служба SAS)** узла.

    ![Результат присоединение tooa общие службы с помощью SAS][20]

## <a name="search-for-storage-accounts"></a>Поиск учетных записей хранилищ
При наличии длинный список учетных записей хранения toolocate быстрый способ записи — поле поиска hello toouse hello верхней части левой панели hello.

При вводе в поле поиска hello hello левой области учетных записей хранилища отображает hello, соответствует значению hello поиска введенные вами toothat точку. Например, для поиска для хранения всех учетных записей, имя которого содержит **tarcher** показан на следующий снимок экрана приветствия:

![Поиск учетной записи хранения][11]

## <a name="next-steps"></a>Дальнейшие действия
* [Управление ресурсами хранилища BLOB-объектов Azure с помощью обозревателя хранилищ (предварительная версия)](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
