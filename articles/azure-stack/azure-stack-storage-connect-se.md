---
title: "Обозреватель хранилищ aaaConnect tooan подписки стек Azure"
description: "Узнайте, как tooan tooconnect Exporer хранилища Azure стека подписки"
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
ms.date: 7/24/2017
ms.author: xiaofmao
ms.openlocfilehash: 8508fcf41a114ff58f57582b4a6021d8050aabe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-storage-explorer-tooan-azure-stack-subscription"></a>Подключение подписки Azure стека tooan обозреватель хранилищ

Azure Storage Explorer (Предварительная версия) имеет отдельное приложение, позволяющее tooeasily работы с данными стека хранилища Azure для Windows, macOS и Linux. Существует несколько tooand средства доступными toomove данные из стека хранилища Azure. Дополнительные сведения см. в разделе [средств для хранилища Azure стек передачи данных](azure-stack-storage-transfer.md).

В этой статье вы узнаете, как tooconnect tooyour хранилища Azure стека учетных записей с помощью обозревателя хранилищ. 

Если вы не установили обозреватель хранилищ, [загрузки](http://www.storageexplorer.com/) и и установить его.

После подключения подписки tooyour стека Azure можно использовать hello [обозреватель хранилищ Azure статьи](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork с данными Azure стека. 

## <a name="prepare-an-azure-stack-subscription"></a>Подготовка подписки Azure стека

Требуется доступ к рабочего стола toohello стека Azure хост-компьютера или VPN-подключения для hello стек Azure Storage Explorer tooaccess подписки. tooset копирование tooAzure подключения VPN стека, в статье toolearn [подключения tooAzure стека с помощью VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).

Hello Azure стека Development Kit требуется сертификат корневого центра Azure стека hello tooexport.

### <a name="tooexport-and-then-import-hello-azure-stack-certificate"></a>tooexport, а затем импортировать сертификат Azure стека hello

1. Откройте `mmc.exe` на машине узла Azure стека или локальный компьютер с tooAzure подключения VPN стека. 

2. В **файл**выберите **добавить или удалить оснастку**и затем добавьте **сертификаты** toomanage **учетная запись компьютера** из **локального Компьютер**.



3. В разделе **\Trusted Root Certification Authorities\Certificates Root\Certificated консоли (локальный компьютер)** найти **AzureStackSelfSignedRootCert**.

    ![Загрузить hello Azure стека корневого сертификата через mmc.exe][25]

4. Сертификат hello щелкните правой кнопкой мыши, выберите **все задачи** > **Экспорт**и следуйте hello инструкции tooexport hello сертификат с **Base64-кодировке X.509 (. (CER)**.  

    Hello экспортированный сертификат будет использоваться в следующем шаге hello.
5. Запустите проводник хранилища (Предварительная версия), и если вы видите hello **подключения tooAzure хранения** диалогового окна поле, отмените его.

6. На hello **изменить** меню выберите пункт слишком**SSL-сертификаты**и нажмите кнопку **импорта сертификатов**. Используйте hello файл выбора диалогового окна поле toofind и откройте hello сертификата, экспортированного в предыдущем шаге hello.

    После импорта, запрашиваемые toorestart обозреватель хранилищ.

    ![Импортируйте сертификат hello в обозреватель хранилищ (Предварительная версия)][27]

Теперь все готово tooconnect подписки Azure стека tooan обозреватель хранилищ.

### <a name="tooconnect-an-azure-stack-subscription"></a>tooconnect подписка стек Azure


1. После перезапуска обозревателя хранилищ (Предварительная версия) выберите hello **изменить** меню и убедитесь, что **стека Azure целевой** выбран. Если не выбран, выберите его и перезапустите обозреватель хранилищ для hello изменение tootake эффекта. Эта настройка необходима для совместимости со средой Azure Stack.

    ![Проверка установки флажка Target Azure Stack (Целевой объект Azure Stack)][28]

7. Выберите в левой области hello **управление учетными записями**.  
    Что вы вошли в tooare отображаются все клиенты Microsoft hello.

8. Выберите tooconnect toohello учетная запись Azure стека, **добавить учетную запись**.

    ![Добавление учетной записи Azure Stack][29]

9. В hello **подключения tooAzure хранения** диалогового **среды Azure**выберите **среду стека Azure используйте**и нажмите кнопку **Далее**.

10. toosign вход с помощью hello Azure стека учетной записи, связанной с по крайней мере одну подписку Azure стека, заполните hello **входа в среду стека tooAzure** диалоговое окно.  

    Ниже приведены сведения о Hello для каждого поля:

    * **Имя среды**: hello поле может настраиваться пользователем.
    * **Конечная точка ресурса ARM**: hello образцы конечных точек ресурсов диспетчера ресурсов Azure:

        * Для оператора облака:<br> https://adminmanagement.local.azurestack.external   
        * Для клиента:<br> https://Management.local.azurestack.external
 
    * **Идентификатор клиента**: необязательно. Получает значение Hello только в том случае, если необходимо указать каталог hello.

12. После успешного входа с учетной записью Azure стека hello левой заполняется hello Azure стека подписок, связанных с этой учетной записи. Выберите подписки Azure стека hello, toowork с и затем выберите **применить**. (Установив или сняв hello **все подписки** переключает флажок, если выбрать все или ни один из hello в списке подписок Azure стека.)

    ![Выберите подписки Azure стека hello после заполнения диалогового окна пользовательского облачной среде hello][30]  
    Hello левая панель содержит учетные записи хранения hello, связанные с подписками Azure стека hello выбран.

    ![Список учетных записей хранения, включая учетные записи подписки Azure Stack][31]

## <a name="next-steps"></a>Дальнейшие действия
* [Приступая к работе с обозреватель хранилищ (Предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md)
* [Хранилища Azure стека: различия и рекомендации](azure-stack-acs-differences.md)


* toolearn Дополнительные сведения о хранилище Azure в разделе [tooMicrosoft введение хранилища Azure](../storage/common/storage-introduction.md)

[25]: ./media/azure-stack-storage-connect-se/add-certificate-azure-stack.png
[26]: ./media/azure-stack-storage-connect-se/export-root-cert-azure-stack.png
[27]: ./media/azure-stack-storage-connect-se/import-azure-stack-cert-storage-explorer.png
[28]: ./media/azure-stack-storage-connect-se/select-target-azure-stack.png
[29]: ./media/azure-stack-storage-connect-se/add-azure-stack-account.png
[30]: ./media/azure-stack-storage-connect-se/select-accounts-azure-stack.png
[31]: ./media/azure-stack-storage-connect-se/azure-stack-storage-account-list.png
