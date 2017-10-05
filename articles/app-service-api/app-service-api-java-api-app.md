---
title: "Сборка и развертывание приложения API Java в службе приложений Azure"
description: "Узнайте, как создать пакет приложения API Java и развернуть его в службе приложений Azure."
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: e38c540071cb49b0177e79178566d72ecb5f8886
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="5447d-103">Сборка и развертывание приложения API Java в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="5447d-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="5447d-104">В этом учебнике показано, как создать приложение Java и развернуть его в приложения API службы приложений Azure, используя [Git].</span><span class="sxs-lookup"><span data-stu-id="5447d-104">This tutorial shows how to create a Java application and deploy it to Azure App Service API Apps using [Git].</span></span> <span data-ttu-id="5447d-105">Указания, приведенные в этом учебнике, применимы в любой операционной системе, на которой может работать Java.</span><span class="sxs-lookup"><span data-stu-id="5447d-105">The instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="5447d-106">Код в этом руководстве создан с помощью [Maven].</span><span class="sxs-lookup"><span data-stu-id="5447d-106">The code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="5447d-107">[Jax-RS] используется для создания службы RESTful и формируется на основе спецификации метаданных [Swagger] с помощью [редактора Swagger].</span><span class="sxs-lookup"><span data-stu-id="5447d-107">[Jax-RS] is used to create the RESTful Service, and is generated based on the [Swagger] metadata specification using the [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5447d-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5447d-108">Prerequisites</span></span>
1. <span data-ttu-id="5447d-109">[Java Developer Kit 8] \((или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="5447d-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="5447d-110">[Maven] на компьютере, на котором ведется разработка.</span><span class="sxs-lookup"><span data-stu-id="5447d-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="5447d-111">[Git] на компьютере, на котором ведется разработка.</span><span class="sxs-lookup"><span data-stu-id="5447d-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="5447d-112">Платная или [бесплатная пробная версия] подписки [Microsoft Azure].</span><span class="sxs-lookup"><span data-stu-id="5447d-112">A paid or [free trial] subscription to [Microsoft Azure]</span></span>
5. <span data-ttu-id="5447d-113">Пример HTTP-приложения, например [Postman]</span><span class="sxs-lookup"><span data-stu-id="5447d-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-the-api-using-swaggerio"></a><span data-ttu-id="5447d-114">Формирование API на основе скаффолдинга при помощи Swagger.io</span><span class="sxs-lookup"><span data-stu-id="5447d-114">Scaffold the API using Swagger.IO</span></span>
<span data-ttu-id="5447d-115">В онлайн-редакторе Swagger.io можно ввести код Swagger в формате JSON или YAML, представляющий структуру API.</span><span class="sxs-lookup"><span data-stu-id="5447d-115">Using the swagger.io online editor, you can enter Swagger JSON or YAML code representing the structure of your API.</span></span> <span data-ttu-id="5447d-116">После завершения разработки контактной зоны API можно экспортировать код в различные платформы и структуры.</span><span class="sxs-lookup"><span data-stu-id="5447d-116">Once you have the API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="5447d-117">В следующем разделе в код, сформированный на основе скаффолдинга, будет добавлена возможность использования макетов.</span><span class="sxs-lookup"><span data-stu-id="5447d-117">In the next section, the scaffolded code will be modified to include mock functionality.</span></span> 

<span data-ttu-id="5447d-118">Мы начнем со вставки текста JSON-кода Swagger в редактор swagger.io, который затем будет использован для создания кода с применением JAX-RS для доступа к конечной точке REST API.</span><span class="sxs-lookup"><span data-stu-id="5447d-118">This demonstration will begin with a Swagger JSON body that you will paste into the swagger.io editor, which will then be used to generate code making use of JAX-RS to access a REST API endpoint.</span></span> <span data-ttu-id="5447d-119">Затем вы измените код, созданный на основе скаффолдинга, для возврата данных макетов, при этом REST API будет смоделирован поверх механизма обеспечения постоянного хранения данных.</span><span class="sxs-lookup"><span data-stu-id="5447d-119">Then, you'll edit the scaffolded code to return mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="5447d-120">Скопируйте приведенный ниже JSON-код Swagger в буфер обмена:</span><span class="sxs-lookup"><span data-stu-id="5447d-120">Copy the following Swagger JSON code to your clipboard:</span></span>
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="5447d-121">Перейдите в [онлайн-редактор Swagger].</span><span class="sxs-lookup"><span data-stu-id="5447d-121">Navigate to the [Online Swagger Editor].</span></span> <span data-ttu-id="5447d-122">В редакторе щелкните в меню **Файл -> Paste JSON** (Вставить JSON).</span><span class="sxs-lookup"><span data-stu-id="5447d-122">Once there, click the **File -> Paste JSON** menu item.</span></span>
   
    ![Пункт меню "Вставить JSON"][paste-json]
3. <span data-ttu-id="5447d-124">Вставьте JSON-код Swagger API списка контактов, который был скопирован ранее.</span><span class="sxs-lookup"><span data-stu-id="5447d-124">Paste in the Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Вставка JSON-кода в Swagger][pasted-swagger]
4. <span data-ttu-id="5447d-126">Просмотрите страницы документации и сводные данные API, отображаемые в редакторе.</span><span class="sxs-lookup"><span data-stu-id="5447d-126">View the documentation pages and API summary rendered in the editor.</span></span> 
   
    ![Просмотр документов, созданных при помощи Swagger][view-swagger-generated-docs]
5. <span data-ttu-id="5447d-128">В меню выберите **Generate Server -> JAX-RS** (Создать сервер -> JAX RS), чтобы создать серверный код на основе скаффолдинга, который позже будет изменен для добавления возможности реализации макетов.</span><span class="sxs-lookup"><span data-stu-id="5447d-128">Select the **Generate Server -> JAX-RS** menu option to scaffold the server-side code you'll edit later to add mock implementation.</span></span> 
   
    ![Пункт меню «Создать код»][generate-code-menu-item]
   
    <span data-ttu-id="5447d-130">После создания кода появится ZIP-файл для скачивания.</span><span class="sxs-lookup"><span data-stu-id="5447d-130">Once the code is generated, you'll be provided a ZIP file to download.</span></span> <span data-ttu-id="5447d-131">Этот файл содержит код, сформированный генератором кода Swagger на основе скаффолдинга, а также все связанные сценарии сборки.</span><span class="sxs-lookup"><span data-stu-id="5447d-131">This file contains the code scaffolded by the Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="5447d-132">Распакуйте всю библиотеку в каталог на рабочей станции, где ведется разработка.</span><span class="sxs-lookup"><span data-stu-id="5447d-132">Unzip the entire library to a directory on your development workstation.</span></span> 

## <a name="edit-the-code-to-add-api-implementation"></a><span data-ttu-id="5447d-133">Измените код для добавления возможности реализации API.</span><span class="sxs-lookup"><span data-stu-id="5447d-133">Edit the Code to add API Implementation</span></span>
<span data-ttu-id="5447d-134">В этом разделе вы замените серверную реализацию созданного с помощью Swagger кода на пользовательский код.</span><span class="sxs-lookup"><span data-stu-id="5447d-134">In this section, you'll replace the Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="5447d-135">Новый код вернет ArrayList сущностей Contact вызывающему клиенту.</span><span class="sxs-lookup"><span data-stu-id="5447d-135">The new code will return an ArrayList of Contact entities to the calling client.</span></span> 

1. <span data-ttu-id="5447d-136">Откройте файл модели *Contact.java*, расположенный в папке *src/gen/java/io/swagger/model*, с помощью [Visual Studio Code] или текстового редактора на ваш выбор.</span><span class="sxs-lookup"><span data-stu-id="5447d-136">Open the *Contact.java* model file, which is located in the *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Открыть файл модели контактов][open-contact-model-file]
2. <span data-ttu-id="5447d-138">Добавьте следующий конструктор в класс **Contact**.</span><span class="sxs-lookup"><span data-stu-id="5447d-138">Add the following constructor within the **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="5447d-139">Откройте файл реализации службы *ContactsApiServiceImpl.java*, расположенный в папке *src/main/java/io/swagger/api/impl*, с помощью [Visual Studio Code] или текстового редактора на ваш выбор.</span><span class="sxs-lookup"><span data-stu-id="5447d-139">Open the *ContactsApiServiceImpl.java* service implementation file, which is located in the *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Открыть файл кода службы контактов][open-contact-service-code-file]
4. <span data-ttu-id="5447d-141">Перезапишите код в файле на новый, чтобы добавить возможность реализации макетов в код службы.</span><span class="sxs-lookup"><span data-stu-id="5447d-141">Overwrite the code in the file with this new code to add a mock implementation to the service code.</span></span> 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. <span data-ttu-id="5447d-142">Откройте окно командной строки и измените каталог на корневую папку приложения.</span><span class="sxs-lookup"><span data-stu-id="5447d-142">Open a command prompt and change directory to the root folder of your application.</span></span>
6. <span data-ttu-id="5447d-143">Выполните следующую команду Maven для создания кода и его локального запуска при помощи сервера приложений Jetty.</span><span class="sxs-lookup"><span data-stu-id="5447d-143">Execute the following Maven command to build the code and run it using the Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="5447d-144">В командном окне должно быть видно, что Jetty запустил код на порте 8080.</span><span class="sxs-lookup"><span data-stu-id="5447d-144">You should see the command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Открыть файл кода службы контактов][run-jetty-war]
8. <span data-ttu-id="5447d-146">Используйте [Postman] для запроса метода API, позволяющего получить все контакты, который расположен по адресу http://localhost:8080/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="5447d-146">Use [Postman] to make a request to the "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Вызвать API контактов][calling-contacts-api]
9. <span data-ttu-id="5447d-148">Используйте [Postman] для запроса метода API, позволяющего получить определенный контакт, который расположен по адресу http://localhost:8080/api/contacts/2.</span><span class="sxs-lookup"><span data-stu-id="5447d-148">Use [Postman] to make a request to the "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Вызвать API контактов][calling-specific-contact-api]
10. <span data-ttu-id="5447d-150">Наконец, создайте WAR-файл Java (веб-архив), выполнив следующую команду Maven в консоли.</span><span class="sxs-lookup"><span data-stu-id="5447d-150">Finally, build the Java WAR (Web ARchive) file by executing the following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="5447d-151">После создания WAR-файл будет помещен в папку **target** .</span><span class="sxs-lookup"><span data-stu-id="5447d-151">Once the WAR file is built, it will be placed into the **target** folder.</span></span> <span data-ttu-id="5447d-152">Перейдите в **целевую** папку и переименуйте WAR-файл на **ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="5447d-152">Navigate into the **target** folder and rename the WAR file to **ROOT.war**.</span></span> <span data-ttu-id="5447d-153">(Обязательно учитывайте регистр.)</span><span class="sxs-lookup"><span data-stu-id="5447d-153">(Make sure the capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="5447d-154">Наконец, выполните следующие команды из корневой папки приложения, чтобы создать папку **deploy** , предназначенную для развертывания WAR-файла в Azure.</span><span class="sxs-lookup"><span data-stu-id="5447d-154">Finally, execute the following commands from the root folder of your application to create a **deploy** folder to use to deploy the WAR file to Azure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-the-output-to-azure-app-service"></a><span data-ttu-id="5447d-155">Публикация выходных данных в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="5447d-155">Publish the output to Azure App Service</span></span>
<span data-ttu-id="5447d-156">В этом разделе вы узнаете, как создать приложение API при помощи портала Azure, подготовить это приложение API для размещения приложений Java и развернуть новый WAR-файл в службе приложений Azure, чтобы запустить новое приложение API.</span><span class="sxs-lookup"><span data-stu-id="5447d-156">In this section you'll learn how to create a new API App using the Azure Portal, prepare that API App for hosting Java applications, and deploy the newly-created WAR file to Azure App Service to run your new API App.</span></span> 

1. <span data-ttu-id="5447d-157">Создайте приложение API на [портале Azure]. Для этого выберите в меню **Создать -> Интернет + мобильные устройства -> Приложение API**, введите сведения о приложении и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5447d-157">Create a new API app in the [Azure portal], by clicking the **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Создать приложение API][create-api-app]
2. <span data-ttu-id="5447d-159">После создания приложения API откройте в нем колонку **Параметры** и щелкните пункт меню **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="5447d-159">Once your API app has been created, open your app's **Settings** blade, and then click the **Application settings** menu item.</span></span> <span data-ttu-id="5447d-160">Выберите последние версии Java из доступных вариантов и последнюю версию Tomcat в меню **веб-контейнера**, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5447d-160">Select the latest Java versions from the available options, then select the latest Tomcat from the **Web container** menu, and then click **Save**.</span></span>
   
    ![Настройка Java в колонке приложения API][set-up-java]
3. <span data-ttu-id="5447d-162">В меню параметров щелкните пункт **Учетные данные развертывания** и укажите имя пользователя и пароль, которые вы хотите использовать для публикации файлов в приложении API.</span><span class="sxs-lookup"><span data-stu-id="5447d-162">Click the **Deployment credentials** settings menu item, and provide a username and password you wish to use for publishing files to your API App.</span></span> 
   
    ![Сброс учетных данных развертывания][deployment-credentials]
4. <span data-ttu-id="5447d-164">Щелкните пункт меню параметров **Источник развертывания**.</span><span class="sxs-lookup"><span data-stu-id="5447d-164">Click the **Deployment source** settings menu item.</span></span> <span data-ttu-id="5447d-165">Затем нажмите кнопку **Выбор источника** и выберите вариант **Локальный репозиторий Git**. После этого нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5447d-165">Once there, click the **Choose source** button, select the **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="5447d-166">В результате будет создан работающий в Azure репозиторий Git, который связан с приложением API.</span><span class="sxs-lookup"><span data-stu-id="5447d-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="5447d-167">Каждый раз при фиксации кода в *главной* ветви репозитория Git код будет публиковаться в запущенном в данный момент экземпляре приложения API.</span><span class="sxs-lookup"><span data-stu-id="5447d-167">Each time you commit code to the *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Настройка локального репозитория Git][select-git-repo]
5. <span data-ttu-id="5447d-169">Скопируйте URL-адрес нового репозитория Git в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="5447d-169">Copy the new Git repository's URL to your clipboard.</span></span> <span data-ttu-id="5447d-170">Сохраните его, потому что он понадобится чуть позже.</span><span class="sxs-lookup"><span data-stu-id="5447d-170">Save this as it will be important in a moment.</span></span> 
   
    ![Настройка нового репозитория Git для приложения][copy-git-repo-url]
6. <span data-ttu-id="5447d-172">Отправьте WAR-файл в онлайн-репозиторий при помощи Git.</span><span class="sxs-lookup"><span data-stu-id="5447d-172">Git push the WAR file to the online repository.</span></span> <span data-ttu-id="5447d-173">Для этого перейдите в созданную ранее папку **deploy** , из которой можно с легкостью зафиксировать код в репозитории, работающем в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="5447d-173">To do this, navigate into the **deploy** folder you created earlier so that you can easily commit the code up to the repository running in your App Service.</span></span> <span data-ttu-id="5447d-174">Открыв окно консоли и перейдя в папку, в которой находится папка с веб-приложениями, запустите следующие команды Git, чтобы запустить процесс и начать развертывание.</span><span class="sxs-lookup"><span data-stu-id="5447d-174">Once you're in the console window and navigated into the folder where the webapps folder is located, issue the following Git commands to launch the process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="5447d-175">После отправки запроса на **передачу** потребуется ввести пароль, созданный ранее для учетных данных развертывания.</span><span class="sxs-lookup"><span data-stu-id="5447d-175">Once you issue the **push** request, you'll be asked for the password you created for the deployment credential earlier.</span></span> <span data-ttu-id="5447d-176">После ввода учетных данных на портале вы увидите, что обновление развернуто.</span><span class="sxs-lookup"><span data-stu-id="5447d-176">After you enter your credentials, you should see your portal display that the update was deployed.</span></span>
7. <span data-ttu-id="5447d-177">При повторном использовании Postman для выполнения недавно развернутого приложения API, работающего в службе приложений Azure, станет видно, что поведение приложения согласовано и что теперь оно возвращает данные контактов должным образом, а также использует изменения простого кода по отношению к сформированному на основе скаффолдинга Java-коду Swagger.io.</span><span class="sxs-lookup"><span data-stu-id="5447d-177">If you once again use Postman to hit the newly-deployed API App running in Azure App Service, you'll see that the behavior is consistent and that now it is returning contact data as expected, and using simple code changes to the Swagger.io scaffolded Java code.</span></span> 
   
    ![Использование REST API контактов Java в Azure в реальном времени][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="5447d-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5447d-179">Next steps</span></span>
<span data-ttu-id="5447d-180">Следуя инструкциям в этой статье, вы смогли выполнить требуемые задачи с JSON-файлом Swagger и определенным Java-кодом, сформированным на основе скаффолдинга и полученным при помощи редактора Swagger.io.</span><span class="sxs-lookup"><span data-stu-id="5447d-180">In this article, you were able to start with a Swagger JSON file and some scaffolded Java code obtained from the Swagger.io editor.</span></span> <span data-ttu-id="5447d-181">В результате внесения простых изменений и развертывания Git вы получили рабочее приложение API, написанное на Java.</span><span class="sxs-lookup"><span data-stu-id="5447d-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="5447d-182">Из следующего руководства вы узнаете, как [использовать приложения API в клиентах JavaScript с помощью CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="5447d-182">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="5447d-183">В последующих учебниках серии демонстрируется, как реализовать проверку подлинности и авторизацию.</span><span class="sxs-lookup"><span data-stu-id="5447d-183">Later tutorials in the series show how to implement authentication and authorization.</span></span>

<span data-ttu-id="5447d-184">Далее рекомендуем вам ознакомиться с дополнительными сведениями о [пакете SDK для Java для службы хранилища]. С помощью этого пакета вы сможете сохранять большие двоичные объекты JSON.</span><span class="sxs-lookup"><span data-stu-id="5447d-184">To build on this sample, you can learn more about the [Storage SDK for Java] to persist the JSON blobs.</span></span> <span data-ttu-id="5447d-185">Кроме того, вы можете использовать [пакет SDK для Java для Document DB]. Он позволяет сохранять данные контактов в Azure Document DB.</span><span class="sxs-lookup"><span data-stu-id="5447d-185">Or, you could use the [Document DB Java SDK] to save your Contact data to Azure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="5447d-186">См. также</span><span class="sxs-lookup"><span data-stu-id="5447d-186">See Also</span></span>
<span data-ttu-id="5447d-187">Дополнительные сведения об использовании Azure с Java можно найти на [странице Azure для разработчиков Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="5447d-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[портале Azure]: https://portal.azure.com/
[пакет SDK для Java для Document DB]: ../documentdb/documentdb-java-application.md
[бесплатная пробная версия]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Developer Kit 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax-RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[онлайн-редактор Swagger]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[пакете SDK для Java для службы хранилища]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[редактора Swagger]: http://editor.swagger.io/
[Visual Studio Code]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
