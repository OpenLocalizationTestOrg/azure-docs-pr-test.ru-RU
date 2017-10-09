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
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="2409d-105">Экспорт сертификатов hello Azure Cosmos DB эмулятора для использования с Java, Python и Node.js</span><span class="sxs-lookup"><span data-stu-id="2409d-105">Export hello Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="2409d-106">**Загрузите hello эмулятора**</span><span class="sxs-lookup"><span data-stu-id="2409d-106">**Download hello Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="2409d-107">Hello эмулятор DB Cosmos Azure предоставляет локальную среду, эмулирующую hello Azure Cosmos DB службы для целей разработки, включая его использование SSL-соединений.</span><span class="sxs-lookup"><span data-stu-id="2409d-107">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="2409d-108">Этой записи блога показано, как tooexport hello SSL-сертификатов для использования в языках и сред выполнения, которые не интегрировать hello хранилище сертификатов Windows, таких как Java, который использует свой собственный [хранилище сертификатов](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) и Python, который использует [сокета оболочки](https://docs.python.org/2/library/ssl.html) и Node.js, который использует [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="2409d-108">This post demonstrates how tooexport hello SSL certificates for use in languages and runtimes that do not integrate with hello Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="2409d-109">Вы можете прочитать больше о эмулятор hello в [используйте hello Azure Cosmos DB эмулятор для разработки и тестирования](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="2409d-109">You can read more about hello emulator in [Use hello Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="2409d-110">В этом учебнике hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2409d-110">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2409d-111">ротация сертификатов;</span><span class="sxs-lookup"><span data-stu-id="2409d-111">Rotating certificates</span></span>
> * <span data-ttu-id="2409d-112">экспорт сертификатов SSL;</span><span class="sxs-lookup"><span data-stu-id="2409d-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="2409d-113">Изучение как toouse hello сертификата в Java, Python и Node.js</span><span class="sxs-lookup"><span data-stu-id="2409d-113">Learning how toouse hello certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="2409d-114">Смена сертификатов</span><span class="sxs-lookup"><span data-stu-id="2409d-114">Certification rotation</span></span>

<span data-ttu-id="2409d-115">Сертификаты в hello: локальный эмулятор Azure Cosmos DB создан hello впервые запускается эмулятор hello.</span><span class="sxs-lookup"><span data-stu-id="2409d-115">Certificates in hello Azure Cosmos DB Local Emulator are generated hello first time hello emulator is run.</span></span> <span data-ttu-id="2409d-116">Создается два сертификата:</span><span class="sxs-lookup"><span data-stu-id="2409d-116">There are two certificates.</span></span> <span data-ttu-id="2409d-117">Один используется для соединения toohello локальный эмулятор и один для управления секреты в эмуляторе hello.</span><span class="sxs-lookup"><span data-stu-id="2409d-117">One used for connecting toohello local emulator and one for managing secrets within hello emulator.</span></span> <span data-ttu-id="2409d-118">Hello сертификат необходимо tooexport является hello соединения с понятным именем hello «DocumentDBEmulatorCertificate».</span><span class="sxs-lookup"><span data-stu-id="2409d-118">hello certificate you want tooexport is hello connection certificate with hello friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="2409d-119">Могут быть повторно созданы оба сертификата, нажав кнопку **восстановить данные** показанной ниже из Azure Cosmos DB эмулятор в панели задач Windows hello.</span><span class="sxs-lookup"><span data-stu-id="2409d-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in hello Windows Tray.</span></span> <span data-ttu-id="2409d-120">Если вы повторно создать сертификаты, hello и установили их в хранилище сертификатов Java hello или использовать их в другом месте, вам потребуется tooupdate их, в противном случае приложения не смогут подключиться toohello локальный эмулятор.</span><span class="sxs-lookup"><span data-stu-id="2409d-120">If you regenerate hello certificates and have installed them into hello Java certificate store or used them elsewhere you will need tooupdate them, otherwise your application will no longer connect toohello local emulator.</span></span>

![Сброс данных в локальном эмуляторе Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="2409d-122">Как tooexport hello Azure Cosmos DB SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="2409d-122">How tooexport hello Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="2409d-123">Запустите диспетчер сертификатов Windows hello, выполнив команду certlm.msc и перейдите toohello Personal -> папку сертификатов и открытых hello сертификат с понятным именем hello **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="2409d-123">Start hello Windows Certificate manager by running certlm.msc and navigate toohello Personal->Certificates folder and open hello certificate with hello friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 1)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="2409d-125">Щелкните **Сведения**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2409d-125">Click on **Details** then **OK**.</span></span>

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 2)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="2409d-127">Нажмите кнопку **скопируйте tooFile...** .</span><span class="sxs-lookup"><span data-stu-id="2409d-127">Click **Copy tooFile...**.</span></span>

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 3)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="2409d-129">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2409d-129">Click **Next**.</span></span>

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 4)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="2409d-131">Щелкните **No, do not export private key** (Не экспортировать закрытый ключ), а затем — **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2409d-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 5)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="2409d-133">Щелкните **Файлы X.509 (.CER) в кодировке Base-64**, а затем — **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2409d-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 6)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="2409d-135">Присвойте имя сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="2409d-135">Give hello certificate a name.</span></span> <span data-ttu-id="2409d-136">В этом случае — **documentdbemulatorcert**. Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2409d-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 7)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="2409d-138">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="2409d-138">Click **Finish**.</span></span>

    ![Экспорт данных в локальном эмуляторе Azure Cosmos DB (шаг 8)](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a><span data-ttu-id="2409d-140">Как toouse hello сертификата в Java</span><span class="sxs-lookup"><span data-stu-id="2409d-140">How toouse hello certificate in Java</span></span>

<span data-ttu-id="2409d-141">При запуске приложения Java или MongoDB приложений, использующих hello Java клиента это проще tooinstall hello сертификат в хранилище сертификатов по умолчанию hello Java hello передачи «-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= «<password>» флаги.</span><span class="sxs-lookup"><span data-stu-id="2409d-141">When running Java applications or MongoDB applications that use hello Java client it is easier tooinstall hello certificate into hello Java default certificate store than passing hello "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="2409d-142">Пример hello включены [Java демонстрационное приложение](https://localhost:8081/_explorer/index.html) зависит от хранилища сертификатов по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="2409d-142">For example hello included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on hello default certificate store.</span></span>

<span data-ttu-id="2409d-143">Следуйте инструкциям hello hello [Добавление toohello сертификат, в хранилище сертификатов ЦС Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 сертификата в хранилище сертификатов Java по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="2409d-143">Follow hello instructions in hello [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificate into hello default Java certificate store.</span></span> <span data-ttu-id="2409d-144">Следует учитывать, что, работа выполняется в каталог hello % JAVA_HOME % при выполнении keytool.</span><span class="sxs-lookup"><span data-stu-id="2409d-144">Keep in mind you will be working in hello %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="2409d-145">Один раз Здравствуйте, «CosmosDBEmulatorCertificate» SSL установлен сертификат ваше приложение должно быть tooconnect доступ и использование hello локальный эмулятор DB Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="2409d-145">Once hello "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able tooconnect and use hello local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="2409d-146">Если продолжить toohave проблемы может потребоваться toofollow hello [отладки подключений SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) статьи.</span><span class="sxs-lookup"><span data-stu-id="2409d-146">If you continue toohave trouble you may want toofollow hello [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="2409d-147">Скорее всего hello сертификат не установлен в хранилище %JAVA_HOME%/jre/lib/security/cacerts hello.</span><span class="sxs-lookup"><span data-stu-id="2409d-147">It is very likely hello certificate is not installed into hello %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="2409d-148">Для пример, при наличии нескольких установленных версий приложения Java могут использовать хранилище другой cacerts чем hello, который был обновлен.</span><span class="sxs-lookup"><span data-stu-id="2409d-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than hello one you updated.</span></span>

## <a name="how-toouse-hello-certificate-in-python"></a><span data-ttu-id="2409d-149">Как toouse hello сертификат на Python</span><span class="sxs-lookup"><span data-stu-id="2409d-149">How toouse hello certificate in Python</span></span>

<span data-ttu-id="2409d-150">По умолчанию hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) для hello DocumentDB API не будет попробуйте и используйте hello SSL-сертификат при подключении toohello локальный эмулятор.</span><span class="sxs-lookup"><span data-stu-id="2409d-150">By default hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="2409d-151">Если задать toouse SSL проверку можно выполнить примеры hello в hello [Python сокета оболочки](https://docs.python.org/2/library/ssl.html) документации.</span><span class="sxs-lookup"><span data-stu-id="2409d-151">If however you want toouse SSL validation you can follow hello examples in hello [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-toouse-hello-certificate-in-nodejs"></a><span data-ttu-id="2409d-152">Как toouse hello сертификата в Node.js</span><span class="sxs-lookup"><span data-stu-id="2409d-152">How toouse hello certificate in Node.js</span></span>

<span data-ttu-id="2409d-153">По умолчанию hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) для hello DocumentDB API не будет попробуйте и используйте hello SSL-сертификат при подключении toohello локальный эмулятор.</span><span class="sxs-lookup"><span data-stu-id="2409d-153">By default hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="2409d-154">Если задать toouse SSL проверку можно выполнить примеры hello в hello [документация по Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="2409d-154">If however you want toouse SSL validation you can follow hello examples in hello [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2409d-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2409d-155">Next steps</span></span>

<span data-ttu-id="2409d-156">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="2409d-156">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2409d-157">изменили сертификаты;</span><span class="sxs-lookup"><span data-stu-id="2409d-157">Rotated certificates</span></span>
> * <span data-ttu-id="2409d-158">SSL-сертификат, экспортированный hello</span><span class="sxs-lookup"><span data-stu-id="2409d-158">Exported hello SSL certificate</span></span>
> * <span data-ttu-id="2409d-159">Было рассмотрено, как toouse hello сертификата в Java, Python и Node.js</span><span class="sxs-lookup"><span data-stu-id="2409d-159">Learned how toouse hello certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="2409d-160">Теперь можно перейти toohello основные понятия раздела приведены дополнительные сведения о Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2409d-160">You can now proceed toohello Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2409d-161">Глобальное распределение</span><span class="sxs-lookup"><span data-stu-id="2409d-161">Global distribution</span></span>](distribute-data-globally.md) 
