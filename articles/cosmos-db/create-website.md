---
title: "aaaDeploy веб-приложения с помощью шаблона - Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, как toodeploy учетную запись Azure Cosmos DB, веб-приложениях службы приложений Azure и образец веб-приложения с помощью шаблона диспетчера ресурсов Azure."
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a>Развертывание Azure Cosmos DB и веб-приложений службы приложений Azure с помощью шаблона Azure Resource Manager
В этом учебнике показано как toouse toodeploy шаблона диспетчера ресурсов Azure и интегрировать [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) веб-приложения и примера веб-приложения.

С помощью шаблонов диспетчера ресурсов Azure, можно легко автоматизировать развертывание hello и настройку ресурсам Azure.  В этом учебнике показано как toodeploy веб-приложения и автоматически настроить сведения о соединении учетной записи Azure Cosmos DB.

После завершения этого учебника будет hello может tooanswer следующие вопросы:  

* Как использовать toodeploy шаблона диспетчера ресурсов Azure и интегрировать учетную запись Azure Cosmos DB и веб-приложения в службе приложений Azure?
* Как использовать toodeploy шаблона диспетчера ресурсов Azure и интеграции Azure Cosmos DB учетной записи, веб-приложения в приложение службы веб-приложения и приложения Webdeploy?

<a id="Prerequisites"></a>

## <a name="prerequisites"></a>Предварительные требования
> [!TIP]
> Во время этого учебника, не приобретает опыта работы с шаблоны Azure Resource Manager или JSON, следует нужно toomodify hello ссылки на шаблоны или параметры развертывания, а затем потребуется знания о каждой из этих областей.
> 
> 

Перед выполнением инструкции hello в этом учебнике, убедитесь, что hello следующее:

* Подписка Azure. Azure — это платформа на основе подписок.  Дополнительные сведения о получении подписки см. на страницах [Как приобрести Azure](https://azure.microsoft.com/pricing/purchase-options/), [Предложения для участников](https://azure.microsoft.com/pricing/member-offers/) или [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/).

## <a id="CreateDB"></a>Шаг 1: Загрузите файлы шаблонов hello
Давайте начнем, загрузив hello файлы шаблонов, которые будут использоваться в этом учебнике.

1. Загрузите hello [учетную запись Azure Cosmos DB, веб-приложений, создание и развертывание приложения демонстрационный пример](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) шаблона tooa локальную папку (например C:\Azure Cosmos DBTemplates). В этом примере разворачиваются учетная запись Azure Cosmos DB, веб-приложение службы приложений и веб-приложение.  Она также автоматически настроит hello web приложения tooconnect toohello Azure Cosmos DB учетной записи.
2. Загрузите hello [создать учетную запись Azure Cosmos DB и пример веб-приложений](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) шаблона tooa локальную папку (например C:\Azure Cosmos DBTemplates). Этот шаблон будет развернута учетную запись Azure Cosmos DB, веб-приложение служб приложений и будет изменить hello сайта приложения параметры tooeasily поверхности Azure Cosmos DB сведения о соединении, но не включает веб-приложения.  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a>Шаг 2: Развертывание hello Azure Cosmos DB учетной записи, приложение службы веб-приложения и демонстрационные приложения пример
Теперь давайте развернем первый шаблон.

> [!TIP]
> шаблон Hello не проверки hello веб-приложения и имя учетной записи Azure Cosmos DB введенным ниже) допустимым и (б) доступны.  Настоятельно рекомендуется проверить доступность hello hello именах Планирование развертывания hello предыдущих toosubmitting toosupply.
> 
> 

1. Имя входа toohello [портала Azure](https://portal.azure.com), нажмите кнопку Создать и выполните поиск «Шаблона-развертывания».
    ![Снимок экрана: hello шаблона-развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment1.png)
2. Выберите элемент развертывания hello шаблона и нажмите кнопку **создать** ![экрана приветствия шаблон развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment2.png)
3. Нажмите кнопку **изменить шаблон**, вставьте содержимое файла шаблона DocDBWebsiteTodo.json hello hello и нажмите кнопку **Сохранить**.
   ![Снимок экрана: hello шаблона-развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment3.png)
4. Нажмите кнопку **изменить параметры**, предоставить значения для всех обязательных параметров hello и нажмите кнопку **ОК**.  Ниже приведены параметры Hello.
   
   1. Имя САЙТА: Указывает имя приложения службы веб-приложения hello и используется tooconstruct URL-адрес hello, который будет использоваться tooaccess hello веб-приложения (например если указать «mydemodocdbwebapp», то hello URL-адрес, по которому вы получите доступ к веб-приложения hello будет mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Задает имя hello размещение toocreate плана служб приложений.
   3. РАСПОЛОЖЕНИЕ: Указывает hello расположение Azure, в какие toocreate hello Azure Cosmos DB и веб-ресурсов приложения.
   4. DATABASEACCOUNTNAME: Задает имя hello toocreate учетная запись Azure Cosmos DB hello.   
      
      ![Снимок экрана: hello шаблона-развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment4.png)
5. Выберите существующую группу ресурсов или укажите toomake имя новой группы ресурсов и выберите расположение для группы ресурсов hello.

    ![Снимок экрана: hello шаблона-развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment5.png)
6. Нажмите кнопку **просмотрите условия**, **покупки**, а затем нажмите кнопку **создать** toobegin hello развертывания.  Выберите **toodashboard ПИН-код** , полученный развертывания hello легко отображается на домашней странице портала Azure.
   ![Снимок экрана: hello шаблона-развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment6.png)
7. После завершения развертывания hello колонки группы ресурсов hello будет открыт.
   ![Снимок экрана: колонка группы ресурсов hello](./media/create-website/TemplateDeployment7.png)  
8. toouse Здравствуйте, приложения, просто перейдите toohello URL-адрес приложения (в приведенном выше примере hello, hello URL-адрес будет http://mydemodocdbwebapp.azurewebsites.net).  Вы увидите hello следующие веб-приложения:
   
   ![Пример приложения Todo](./media/create-website/image2.png)
9. Продолжить и создать несколько задач в веб-приложения hello и вернитесь колонки группы ресурсов toohello в hello портал Azure. Выберите hello Azure Cosmos DB учетной записи ресурса в список ресурсов hello и нажмите кнопку **Explorer запроса**.
    ![Снимок экрана: hello Сводка дисторсии с веб-приложения hello выделен](./media/create-website/TemplateDeployment8.png)  
10. Выполните запрос по умолчанию hello, «ВЫБЕРИТЕ * из c» и проверить результаты hello.  Обратите внимание, что этот запрос hello извлеченные hello JSON-представление элементов todo hello, созданный на шаге 7 выше.  При желании вы свободного tooexperiment с запросами; Например, попробуйте запустить SELECT * FROM c WHERE c.isComplete = true tooreturn все элементы todo, которые были помечены как завершенные.
    
    ![Снимок экрана: hello обозреватель запроса и результатов колонок, отображения результатов запроса hello](./media/create-website/image5.png)
11. Чувствовать себя hello свободного tooexplore взаимодействие с порталом Azure Cosmos DB или изменить приложение Todo образец hello.  Когда вы закончите, давайте развернем еще один шаблон.

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a>Шаг 3: Развертывание hello учетной записи документа и пример веб-приложения
Теперь давайте развернем второй шаблон.  Этот шаблон является полезным tooshow как Azure Cosmos DB сведения о соединении, например конечной точки учетной записи и главный ключ может вводить в веб-приложения в качестве параметров приложения или пользовательской строки подключения. Например возможно, свои собственные веб-приложения, что будет, например toodeploy с учетной записью Azure Cosmos DB и сведения о соединении hello автоматически во время развертывания.

> [!TIP]
> шаблон Hello не проверки hello веб-приложения и имя учетной записи Azure Cosmos DB введенным ниже) допустимым и (б) доступны.  Настоятельно рекомендуется проверить доступность hello hello именах Планирование развертывания hello предыдущих toosubmitting toosupply.
> 
> 

1. В hello [портала Azure](https://portal.azure.com), нажмите кнопку Создать и выполните поиск «Шаблона-развертывания».
    ![Снимок экрана: hello шаблона-развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment1.png)
2. Выберите элемент развертывания hello шаблона и нажмите кнопку **создать** ![экрана приветствия шаблон развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment2.png)
3. Нажмите кнопку **изменить шаблон**, вставьте содержимое файла шаблона DocDBWebSite.json hello hello и нажмите кнопку **Сохранить**.
   ![Снимок экрана: hello шаблона-развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment3.png)
4. Нажмите кнопку **изменить параметры**, предоставить значения для всех обязательных параметров hello и нажмите кнопку **ОК**.  Ниже приведены параметры Hello.
   
   1. Имя САЙТА: Указывает имя приложения службы веб-приложения hello и используется tooconstruct URL-адрес hello, который будет использоваться tooaccess hello веб-приложения (например если указать «mydemodocdbwebapp», то hello URL-адрес, по которому вы получите доступ к веб-приложения hello будет mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Задает имя hello размещение toocreate плана служб приложений.
   3. РАСПОЛОЖЕНИЕ: Указывает hello расположение Azure, в какие toocreate hello Azure Cosmos DB и веб-ресурсов приложения.
   4. DATABASEACCOUNTNAME: Задает имя hello toocreate учетная запись Azure Cosmos DB hello.   
      
      ![Снимок экрана: hello шаблона-развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment4.png)
5. Выберите существующую группу ресурсов или укажите toomake имя новой группы ресурсов и выберите расположение для группы ресурсов hello.

    ![Снимок экрана: hello шаблона-развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment5.png)
6. Нажмите кнопку **просмотрите условия**, **покупки**, а затем нажмите кнопку **создать** toobegin hello развертывания.  Выберите **toodashboard ПИН-код** , полученный развертывания hello легко отображается на домашней странице портала Azure.
   ![Снимок экрана: hello шаблона-развертывания пользовательского интерфейса](./media/create-website/TemplateDeployment6.png)
7. После завершения развертывания hello колонки группы ресурсов hello будет открыт.
   ![Снимок экрана: колонка группы ресурсов hello](./media/create-website/TemplateDeployment7.png)  
8. Щелкните ресурс веб-приложения hello hello списка ресурсов, а затем нажмите кнопку **параметры приложения** ![экрана приветствия группы ресурсов](./media/create-website/TemplateDeployment9.png)  
9. Обратите внимание, как параметры приложения для конечной точки Azure Cosmos DB hello и каждой из главных ключей базы данных Azure Cosmos hello.

    ![Снимок экрана с параметрами приложения](./media/create-website/TemplateDeployment10.png)  
10. Чувствовать себя свободного toocontinue изучение hello Azure Portal или выполните один из наших Azure DB Cosmos [образцы](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate приложение Azure Cosmos DB.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Дальнейшие действия
Поздравляем! Мы выполнили развертывание Azure Cosmos DB, веб-приложения службы приложений и примера веб-приложения с использованием шаблонов Azure Resource Manager.

* Щелкните toolearn Дополнительные сведения о базе данных Azure Cosmos, [здесь](http://azure.com/docdb).
* Щелкните toolearn Дополнительные сведения о приложениях веб-службы приложения Azure [здесь](http://go.microsoft.com/fwlink/?LinkId=325362).
* toolearn Дополнительные сведения о шаблоны Azure Resource Manager, нажмите кнопку [здесь](https://msdn.microsoft.com/library/azure/dn790549.aspx).

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)
* Toohello руководства в разделе Изменение hello старого портала toohello новый портал: [ссылки для навигации по hello классический портал Azure](http://go.microsoft.com/fwlink/?LinkId=529715)

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](http://go.microsoft.com/fwlink/?LinkId=523751), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

