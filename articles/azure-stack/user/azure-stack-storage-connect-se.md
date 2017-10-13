---
title: "Подключаться к подписке Azure стека обозреватель хранилищ"
description: "Узнайте, как подключаться к подписке Azure стека Exporer хранилища"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: c7e6d70148d39fd74f6409a0a239833f8e9f7614
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="connect-storage-explorer-to-an-azure-stack-subscription"></a>Подключаться к подписке Azure стека обозреватель хранилищ

*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*

Azure Storage Explorer (Предварительная версия) имеет отдельное приложение, предназначенное для упрощения работы с данными стека хранилища Azure в Windows, macOS и Linux. Существует несколько средств доступными для перемещения данных в и из стека хранилища Azure. Дополнительные сведения см. в разделе [средств для хранилища Azure стек передачи данных](azure-stack-storage-transfer.md).

В этой статье вы узнаете, как соединиться с учетных записей хранилища Azure стека с помощью обозревателя хранилищ. 

Если вы не установили обозреватель хранилищ, [загрузки](http://www.storageexplorer.com/) и и установить его.

После подключения к подписке Azure стека можно использовать [обозреватель хранилищ Azure статьи](../../vs-azure-tools-storage-manage-with-storage-explorer.md) для работы с данными Azure стека. 

## <a name="prepare-an-azure-stack-subscription"></a>Подготовка подписки Azure стека

Вам нужен доступ к рабочему столу стек Azure хост-компьютера или VPN-подключения для обозревателя хранилищ, доступ к подписке Azure стека. Дополнительные сведения о настройке VPN-подключения в Azure Stack см. в разделе [Подключение c VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).

Пакет средств разработки стек Azure необходимо экспортировать корневой сертификат центра Azure стека.

### <a name="to-export-and-then-import-the-azure-stack-certificate"></a>Чтобы экспортировать и импортировать сертификат стек Azure

1. Откройте `mmc.exe` на машине узла Azure стека или локальный компьютер через VPN-подключения в стек Azure. 

2. В **файл**выберите **добавить или удалить оснастку**, а затем добавьте **сертификаты** для управления **моей учетной записи пользователя**.



3. В разделе **\Trusted Root Certification Authorities\Certificates Root\Certificated консоли (локальный компьютер)** найти **AzureStackSelfSignedRootCert**.

    ![Загрузка корневого сертификата Azure Stack с помощью mmc.exe][25]

4. Щелкните правой кнопкой мыши сертификат, выберите **все задачи** > **Экспорт**, а затем следуйте инструкциям, чтобы экспортировать сертификат с **X.509 в кодировке Base-64 (. (CER)**.  

    Экспортированный сертификат будет использоваться на следующем шаге.
5. Запустите проводник хранилища (Предварительная версия), и если вы видите **подключение к хранилищу Azure** диалогового окна поле, отмените его.

6. На **изменить** последовательно выберите пункты **SSL-сертификаты**, а затем нажмите кнопку **импорта сертификатов**. Используйте диалоговое окно выбора файла, чтобы найти и открыть сертификат, изученный на предыдущем шаге.

    После импорта вам будет предложено перезапустить обозреватель хранилищ.

    ![Импорт сертификата в обозреватель хранилищ (предварительная версия)][27]

Теперь вы готовы подключаться к подписке Azure стека обозреватель хранилищ.

### <a name="to-connect-an-azure-stack-subscription"></a>Для подключения подписки на стек Azure


1. После перезапуска обозревателя хранилищ (предварительная версия) откройте меню **Изменить** и убедитесь, что **Target Azure Stack** (Целевой объект Azure Stack) выбран. В противном случае выберите его и перезапустите обозреватель хранилищ, чтобы изменения вступили в силу. Эта настройка необходима для совместимости со средой Azure Stack.

    ![Проверка установки флажка Target Azure Stack (Целевой объект Azure Stack)][28]

7. На панели слева щелкните **Управление учетными записями**.  
    Отобразятся все учетные записи Майкрософт, в которые вы вошли.

8. Чтобы подключиться к учетной записи Azure Stack, выберите **Добавить учетную запись**.

    ![Добавление учетной записи Azure Stack][29]

9. В **подключение к хранилищу Azure** диалогового **среды Azure**выберите **среду стека Azure используйте**и нажмите кнопку **Далее**.

10. Чтобы войти в учетную запись стек Azure, который связан с по крайней мере одну подписку Azure стека, заполните **войти в среду Azure стека** диалоговое окно.  

    Ниже приведены подробные сведения о каждом поле диалогового окна.

    * **Имя среды.** Это поле может настраивать пользователь.
    * **ARM resource endpoint** (Конечная точка ресурса ARM). Примеры конечной точки ресурсов ARM:

        * Для оператора облака:<br> https://adminmanagement.local.azurestack.external   
        * Для клиента:<br> https://Management.local.azurestack.external
 
    * **Идентификатор клиента**: необязательно. Значение задается, только если необходимо указать каталог.

12. Выполнив вход с помощью учетной записи Azure Stack, на панели слева вы увидите подписки Azure Stack, связанные с этой учетной записью. Выберите подписки Azure Stack, с которыми вы собираетесь работать, а затем щелкните **Применить**. (Чтобы выбрать или очистить все подписки Azure Stack, установите флажок **Все подписки**. Чтобы отменить выбор, снимите флажок.)

    ![Выбор подписок Azure Stack после заполнения диалогового окна Custom Cloud Environment (Пользовательская облачная среда)][30]  
    На панели слева отобразятся все учетные записи хранения, связанные с выбранными подписками Azure Stack.

    ![Список учетных записей хранения, включая учетные записи подписки Azure Stack][31]

## <a name="next-steps"></a>Дальнейшие действия
* [Приступая к работе с обозреватель хранилищ (Предварительная версия)](../../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [Хранилища Azure стека: различия и рекомендации](azure-stack-acs-differences.md)


* Дополнительные сведения о хранилище Azure см. в разделе [ознакомление с хранилищем Microsoft Azure](../../storage/common/storage-introduction.md)

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
