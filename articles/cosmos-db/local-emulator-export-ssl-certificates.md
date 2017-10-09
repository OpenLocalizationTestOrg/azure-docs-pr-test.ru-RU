---
title: "сертификаты DB эмулятор Azure Cosmos hello aaaExport | Документы Microsoft"
description: "При разработке на языках и сред выполнения, которые используют хранилище сертификатов Windows hello может потребоваться tooexport и управлять сертификатами SSL hello. В этой статье приведены пошаговые инструкции."
services: cosmos-db
documentationcenter: 
keywords: "Эмулятор Azure Cosmos DB"
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>Экспорт сертификатов hello Azure Cosmos DB эмулятора для использования с Java, Python и Node.js

[**Загрузите hello эмулятора**](https://aka.ms/cosmosdb-emulator)

Hello эмулятор DB Cosmos Azure предоставляет локальную среду, эмулирующую hello Azure Cosmos DB службы для целей разработки, включая его использование SSL-соединений. Этой записи блога показано, как tooexport hello SSL-сертификатов для использования в языках и сред выполнения, которые не интегрировать hello хранилище сертификатов Windows, таких как Java, который использует свой собственный [хранилище сертификатов](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) и Python, который использует [сокета оболочки](https://docs.python.org/2/library/ssl.html) и Node.js, который использует [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback). Вы можете прочитать больше о эмулятор hello в [используйте hello Azure Cosmos DB эмулятор для разработки и тестирования](./local-emulator.md).

В этом учебнике hello следующие задачи:

> [!div class="checklist"]
> * ротация сертификатов;
> * экспорт сертификатов SSL;
> * Изучение как toouse hello сертификата в Java, Python и Node.js

## <a name="certification-rotation"></a>Смена сертификатов

Сертификаты в hello: локальный эмулятор Azure Cosmos DB создан hello впервые запускается эмулятор hello. Создается два сертификата: Один используется для соединения toohello локальный эмулятор и один для управления секреты в эмуляторе hello. Hello сертификат необходимо tooexport является hello соединения с понятным именем hello «DocumentDBEmulatorCertificate».

Могут быть повторно созданы оба сертификата, нажав кнопку **восстановить данные** показанной ниже из Azure Cosmos DB эмулятор в панели задач Windows hello. Если вы повторно создать сертификаты, hello и установили их в хранилище сертификатов Java hello или использовать их в другом месте, вам потребуется tooupdate их, в противном случае приложения не смогут подключиться toohello локальный эмулятор.

![Сброс данных в локальном эмуляторе Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a>Как tooexport hello Azure Cosmos DB SSL-сертификата

1. Запустите диспетчер сертификатов Windows hello, выполнив команду certlm.msc и перейдите toohello Personal -> папку сертификатов и открытых hello сертификат с понятным именем hello **DocumentDbEmulatorCertificate**.

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 1)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. Щелкните **Сведения**, а затем нажмите кнопку **ОК**.

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 2)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. Нажмите кнопку **скопируйте tooFile...** .

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 3)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. Щелкните **Далее**.

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 4)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. Щелкните **No, do not export private key** (Не экспортировать закрытый ключ), а затем — **Далее**.

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 5)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. Щелкните **Файлы X.509 (.CER) в кодировке Base-64**, а затем — **Далее**.

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 6)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. Присвойте имя сертификата hello. В этом случае — **documentdbemulatorcert**. Щелкните **Далее**.

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 7)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. Нажмите кнопку **Готово**

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 8)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a>Как toouse hello сертификата в Java

При запуске приложения Java или MongoDB приложений, использующих hello Java клиента это проще tooinstall hello сертификат в хранилище сертификатов по умолчанию hello Java hello передачи «-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= «<password>» флаги. Пример hello включены [Java демонстрационное приложение](https://localhost:8081/_explorer/index.html) зависит от хранилища сертификатов по умолчанию hello.

Следуйте инструкциям hello hello [Добавление toohello сертификат, в хранилище сертификатов ЦС Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 сертификата в хранилище сертификатов Java по умолчанию hello. Следует учитывать, что, работа выполняется в каталог hello % JAVA_HOME % при выполнении keytool.

Один раз Здравствуйте, «CosmosDBEmulatorCertificate» SSL установлен сертификат ваше приложение должно быть tooconnect доступ и использование hello локальный эмулятор DB Cosmos Azure. Если продолжить toohave проблемы может потребоваться toofollow hello [отладки подключений SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) статьи. Скорее всего hello сертификат не установлен в хранилище %JAVA_HOME%/jre/lib/security/cacerts hello. Для пример, при наличии нескольких установленных версий приложения Java могут использовать хранилище другой cacerts чем hello, который был обновлен.

## <a name="how-toouse-hello-certificate-in-python"></a>Как toouse hello сертификат на Python

По умолчанию hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) для hello DocumentDB API не будет попробуйте и используйте hello SSL-сертификат при подключении toohello локальный эмулятор. Если задать toouse SSL проверку можно выполнить примеры hello в hello [Python сокета оболочки](https://docs.python.org/2/library/ssl.html) документации.

## <a name="how-toouse-hello-certificate-in-nodejs"></a>Как toouse hello сертификата в Node.js

По умолчанию hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) для hello DocumentDB API не будет попробуйте и используйте hello SSL-сертификат при подключении toohello локальный эмулятор. Если задать toouse SSL проверку можно выполнить примеры hello в hello [документация по Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы сделали hello следующее:

> [!div class="checklist"]
> * изменили сертификаты;
> * SSL-сертификат, экспортированный hello
> * Было рассмотрено, как toouse hello сертификата в Java, Python и Node.js

Теперь можно перейти toohello основные понятия раздела приведены дополнительные сведения о Cosmos DB.

> [!div class="nextstepaction"]
> [Глобальное распределение](distribute-data-globally.md) 
