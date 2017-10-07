---
title: "aaaBuild и развертывание приложения Java API в службе приложений Azure"
description: "Узнайте, как toocreate приложения Java API упаковать и развернуть его tooAzure службы приложений."
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
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="cffd1-103">Сборка и развертывание приложения API Java в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="cffd1-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="cffd1-104">В этом учебнике показано как toocreate приложения Java и развернуть ее tooAzure приложений из службы API приложений с помощью [Git].</span><span class="sxs-lookup"><span data-stu-id="cffd1-104">This tutorial shows how toocreate a Java application and deploy it tooAzure App Service API Apps using [Git].</span></span> <span data-ttu-id="cffd1-105">Hello инструкциям этого учебника можно выполнять в любой операционной системе, поддерживающий работу Java.</span><span class="sxs-lookup"><span data-stu-id="cffd1-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="cffd1-106">кода Hello в этот учебник построен с использованием [Maven].</span><span class="sxs-lookup"><span data-stu-id="cffd1-106">hello code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="cffd1-107">[JAX RS] hello используется toocreate службы RESTful и создается на основании hello [Swagger] спецификации метаданных с помощью hello [Swagger редактор].</span><span class="sxs-lookup"><span data-stu-id="cffd1-107">[Jax-RS] is used toocreate hello RESTful Service, and is generated based on hello [Swagger] metadata specification using hello [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cffd1-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cffd1-108">Prerequisites</span></span>
1. <span data-ttu-id="cffd1-109">[Java Developer Kit 8] \((или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="cffd1-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="cffd1-110">[Maven] на компьютере, на котором ведется разработка.</span><span class="sxs-lookup"><span data-stu-id="cffd1-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="cffd1-111">[Git] на компьютере, на котором ведется разработка.</span><span class="sxs-lookup"><span data-stu-id="cffd1-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="cffd1-112">Платной или [бесплатной пробной версии] подписки слишком[Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="cffd1-112">A paid or [free trial] subscription too[Microsoft Azure]</span></span>
5. <span data-ttu-id="cffd1-113">Пример HTTP-приложения, например [почтальон]</span><span class="sxs-lookup"><span data-stu-id="cffd1-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-hello-api-using-swaggerio"></a><span data-ttu-id="cffd1-114">API hello формирования шаблонов, с помощью Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="cffd1-114">Scaffold hello API using Swagger.IO</span></span>
<span data-ttu-id="cffd1-115">В редакторе hello swagger.io документации можно ввести Swagger JSON или YAML код, представляющий структуру hello API.</span><span class="sxs-lookup"><span data-stu-id="cffd1-115">Using hello swagger.io online editor, you can enter Swagger JSON or YAML code representing hello structure of your API.</span></span> <span data-ttu-id="cffd1-116">После получения контактной зоны hello API предназначен можно экспортировать кода для различных платформ и платформ.</span><span class="sxs-lookup"><span data-stu-id="cffd1-116">Once you have hello API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="cffd1-117">В следующем разделе hello hello формирования шаблонов код будет макетов tooinclude измененные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="cffd1-117">In hello next section, hello scaffolded code will be modified tooinclude mock functionality.</span></span> 

<span data-ttu-id="cffd1-118">Этой демонстрации начнется с текстом Swagger JSON, который можно будет вставить в редактор swagger.io hello, которой будут затем используется toogenerate кода осуществлять использование tooaccess JAX RS конечной точкой API.</span><span class="sxs-lookup"><span data-stu-id="cffd1-118">This demonstration will begin with a Swagger JSON body that you will paste into hello swagger.io editor, which will then be used toogenerate code making use of JAX-RS tooaccess a REST API endpoint.</span></span> <span data-ttu-id="cffd1-119">После этого требуется изменить hello формирования шаблонов код tooreturn фиктивные данные, имитируя API REST, построенных на вершине механизм сохраняемости данных.</span><span class="sxs-lookup"><span data-stu-id="cffd1-119">Then, you'll edit hello scaffolded code tooreturn mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="cffd1-120">Скопируйте следующий буфер tooyour Swagger JSON кода hello:</span><span class="sxs-lookup"><span data-stu-id="cffd1-120">Copy hello following Swagger JSON code tooyour clipboard:</span></span>
   
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
2. <span data-ttu-id="cffd1-121">Перейдите toohello [интерактивном редакторе Swagger].</span><span class="sxs-lookup"><span data-stu-id="cffd1-121">Navigate toohello [Online Swagger Editor].</span></span> <span data-ttu-id="cffd1-122">Один раз, нажмите кнопку hello **файл -> Вставить JSON** элемента меню.</span><span class="sxs-lookup"><span data-stu-id="cffd1-122">Once there, click hello **File -> Paste JSON** menu item.</span></span>
   
    ![Пункт меню "Вставить JSON"][paste-json]
3. <span data-ttu-id="cffd1-124">Вставьте hello контакты список API Swagger JSON скопированное ранее.</span><span class="sxs-lookup"><span data-stu-id="cffd1-124">Paste in hello Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Вставка JSON-кода в Swagger][pasted-swagger]
4. <span data-ttu-id="cffd1-126">Просмотр страницы документации hello и Сводка по API, отображаемого в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="cffd1-126">View hello documentation pages and API summary rendered in hello editor.</span></span> 
   
    ![Просмотр документов, созданных при помощи Swagger][view-swagger-generated-docs]
5. <span data-ttu-id="cffd1-128">Выберите hello **Server Создать -> JAX RS** меню параметр tooscaffold hello серверный код более поздней версии tooadd макетной реализации требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="cffd1-128">Select hello **Generate Server -> JAX-RS** menu option tooscaffold hello server-side code you'll edit later tooadd mock implementation.</span></span> 
   
    ![Пункт меню «Создать код»][generate-code-menu-item]
   
    <span data-ttu-id="cffd1-130">После создания кода hello, будет предоставляться toodownload файла ZIP.</span><span class="sxs-lookup"><span data-stu-id="cffd1-130">Once hello code is generated, you'll be provided a ZIP file toodownload.</span></span> <span data-ttu-id="cffd1-131">Этот файл содержит код hello формирования шаблонов генератором кода hello Swagger и все связанные с ним создавать скрипты.</span><span class="sxs-lookup"><span data-stu-id="cffd1-131">This file contains hello code scaffolded by hello Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="cffd1-132">Распакуйте каталог tooa hello всей библиотеки на рабочей станции разработки.</span><span class="sxs-lookup"><span data-stu-id="cffd1-132">Unzip hello entire library tooa directory on your development workstation.</span></span> 

## <a name="edit-hello-code-tooadd-api-implementation"></a><span data-ttu-id="cffd1-133">Изменение кода hello tooadd реализации API</span><span class="sxs-lookup"><span data-stu-id="cffd1-133">Edit hello Code tooadd API Implementation</span></span>
<span data-ttu-id="cffd1-134">В этом разделе вы замените hello Swagger кода, созданного на стороне сервера реализации пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="cffd1-134">In this section, you'll replace hello Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="cffd1-135">новый код Hello вернет сущности ArrayList контакт toohello вызывающего клиента.</span><span class="sxs-lookup"><span data-stu-id="cffd1-135">hello new code will return an ArrayList of Contact entities toohello calling client.</span></span> 

1. <span data-ttu-id="cffd1-136">Откройте hello *Contact.java* файла модели, который находится в hello *src/gen-java/операции ввода-вывода/swagger/модели* папки, с помощью [кода Visual Studio] или в привычном текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="cffd1-136">Open hello *Contact.java* model file, which is located in hello *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Открыть файл модели контактов][open-contact-model-file]
2. <span data-ttu-id="cffd1-138">Добавьте следующий конструктор в hello hello **контакт** класса.</span><span class="sxs-lookup"><span data-stu-id="cffd1-138">Add hello following constructor within hello **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="cffd1-139">Откройте hello *ContactsApiServiceImpl.java* файл реализации службы, который находится в hello *src/main/java и операции ввода-вывода/swagger/api/impl* папки, с помощью [кода Visual Studio]или в привычном текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="cffd1-139">Open hello *ContactsApiServiceImpl.java* service implementation file, which is located in hello *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Открыть файл кода службы контактов][open-contact-service-code-file]
4. <span data-ttu-id="cffd1-141">Замените этот новый tooadd кода код службы toohello макетной реализации hello код в файле hello.</span><span class="sxs-lookup"><span data-stu-id="cffd1-141">Overwrite hello code in hello file with this new code tooadd a mock implementation toohello service code.</span></span> 
   
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
5. <span data-ttu-id="cffd1-142">Откройте командную строку и измените каталог toohello корневую папку приложения.</span><span class="sxs-lookup"><span data-stu-id="cffd1-142">Open a command prompt and change directory toohello root folder of your application.</span></span>
6. <span data-ttu-id="cffd1-143">Выполните следующий код hello toobuild команды Maven hello и запустить его локально с помощью hello Jetty сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="cffd1-143">Execute hello following Maven command toobuild hello code and run it using hello Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="cffd1-144">Должно появиться окно команд hello отражают, Jetty начала кода на порт 8080.</span><span class="sxs-lookup"><span data-stu-id="cffd1-144">You should see hello command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Открыть файл кода службы контактов][run-jetty-war]
8. <span data-ttu-id="cffd1-146">Используйте [почтальон] метод toomake API toohello «получить все контакты» запроса в HTTP://localhost: 8080/api/контактов.</span><span class="sxs-lookup"><span data-stu-id="cffd1-146">Use [Postman] toomake a request toohello "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Вызов hello Contacts API][calling-contacts-api]
9. <span data-ttu-id="cffd1-148">Используйте [почтальон] метод toomake API «получить определенного контакта» toohello запроса, расположенной на http://localhost: 8080/api/contacts/2.</span><span class="sxs-lookup"><span data-stu-id="cffd1-148">Use [Postman] toomake a request toohello "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Вызов hello Contacts API][calling-specific-contact-api]
10. <span data-ttu-id="cffd1-150">Наконец создайте файл hello WAR Java (веб-архив), выполнив следующую команду Maven в консоли hello.</span><span class="sxs-lookup"><span data-stu-id="cffd1-150">Finally, build hello Java WAR (Web ARchive) file by executing hello following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="cffd1-151">После построения hello WAR-файл, он будут помещены в hello **целевой** папки.</span><span class="sxs-lookup"><span data-stu-id="cffd1-151">Once hello WAR file is built, it will be placed into hello **target** folder.</span></span> <span data-ttu-id="cffd1-152">Перейдите в hello **целевой** папку и переименуйте hello WAR-файла слишком**ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="cffd1-152">Navigate into hello **target** folder and rename hello WAR file too**ROOT.war**.</span></span> <span data-ttu-id="cffd1-153">(Убедитесь, что этот формат соответствует hello регистр букв).</span><span class="sxs-lookup"><span data-stu-id="cffd1-153">(Make sure hello capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="cffd1-154">Наконец, выполните следующие команды из корневой папки hello toocreate вашего приложения hello **развертывание** папки toouse toodeploy hello WAR-файл tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cffd1-154">Finally, execute hello following commands from hello root folder of your application toocreate a **deploy** folder toouse toodeploy hello WAR file tooAzure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a><span data-ttu-id="cffd1-155">Публикация tooAzure hello выходных данных приложения службы</span><span class="sxs-lookup"><span data-stu-id="cffd1-155">Publish hello output tooAzure App Service</span></span>
<span data-ttu-id="cffd1-156">В этом разделе вы узнаете, как toocreate новое приложение API hello с помощью портала Azure подготовить приложение API для размещения приложений Java и развертывание hello только что созданный WAR файла tooAzure toorun службы приложений нового приложения API.</span><span class="sxs-lookup"><span data-stu-id="cffd1-156">In this section you'll learn how toocreate a new API App using hello Azure Portal, prepare that API App for hosting Java applications, and deploy hello newly-created WAR file tooAzure App Service toorun your new API App.</span></span> 

1. <span data-ttu-id="cffd1-157">Создание нового приложения API в hello [портал Azure], щелкнув hello **New -> Web + Mobile -> приложения API** пункт меню, введя свои данные приложения и выбрав **создать**.</span><span class="sxs-lookup"><span data-stu-id="cffd1-157">Create a new API app in hello [Azure portal], by clicking hello **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Создать приложение API][create-api-app]
2. <span data-ttu-id="cffd1-159">После создания приложения API откройте ваше приложение **параметры** колонки и нажмите кнопку hello **параметры приложения** элемента меню.</span><span class="sxs-lookup"><span data-stu-id="cffd1-159">Once your API app has been created, open your app's **Settings** blade, and then click hello **Application settings** menu item.</span></span> <span data-ttu-id="cffd1-160">Выберите hello последние версии Java из доступных параметров hello, а затем выберите hello последнюю Tomcat из hello **контейнера Web** меню, а затем нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cffd1-160">Select hello latest Java versions from hello available options, then select hello latest Tomcat from hello **Web container** menu, and then click **Save**.</span></span>
   
    ![Настроить Java в колонки API приложения hello][set-up-java]
3. <span data-ttu-id="cffd1-162">Нажмите кнопку hello **учетные данные развертывания** меню параметров элемент и укажите имя пользователя и пароль, который toouse для публикации файлов tooyour приложения API.</span><span class="sxs-lookup"><span data-stu-id="cffd1-162">Click hello **Deployment credentials** settings menu item, and provide a username and password you wish toouse for publishing files tooyour API App.</span></span> 
   
    ![Сброс учетных данных развертывания][deployment-credentials]
4. <span data-ttu-id="cffd1-164">Нажмите кнопку hello **источник развертывания** параметры пункта меню.</span><span class="sxs-lookup"><span data-stu-id="cffd1-164">Click hello **Deployment source** settings menu item.</span></span> <span data-ttu-id="cffd1-165">Один раз, нажмите кнопку hello **выбрать источник** кнопку, выберите hello **локального репозитория Git** , а затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cffd1-165">Once there, click hello **Choose source** button, select hello **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="cffd1-166">В результате будет создан работающий в Azure репозиторий Git, который связан с приложением API.</span><span class="sxs-lookup"><span data-stu-id="cffd1-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="cffd1-167">Каждый раз при фиксации кода toohello *master* ветви репозитория Git, код будет опубликован в вашей динамической запущенный экземпляр приложения API.</span><span class="sxs-lookup"><span data-stu-id="cffd1-167">Each time you commit code toohello *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Настройка локального репозитория Git][select-git-repo]
5. <span data-ttu-id="cffd1-169">Копировать hello новый репозиторий Git в буфер обмена tooyour URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="cffd1-169">Copy hello new Git repository's URL tooyour clipboard.</span></span> <span data-ttu-id="cffd1-170">Сохраните его, потому что он понадобится чуть позже.</span><span class="sxs-lookup"><span data-stu-id="cffd1-170">Save this as it will be important in a moment.</span></span> 
   
    ![Настройка нового репозитория Git для приложения][copy-git-repo-url]
6. <span data-ttu-id="cffd1-172">Принудительная hello WAR файл toohello online репозитории.</span><span class="sxs-lookup"><span data-stu-id="cffd1-172">Git push hello WAR file toohello online repository.</span></span> <span data-ttu-id="cffd1-173">toodo это, перейдите в hello **развертывание** папку, созданную ранее, чтобы легко можно зафиксировать кода hello toohello хранилища в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="cffd1-173">toodo this, navigate into hello **deploy** folder you created earlier so that you can easily commit hello code up toohello repository running in your App Service.</span></span> <span data-ttu-id="cffd1-174">Один раз в окно консоли hello и к которому необходимо перейти в папку hello, где находится папка веб-приложения hello, выдача hello, следуйте процедуре hello toolaunch команды Git и запускать развертывание.</span><span class="sxs-lookup"><span data-stu-id="cffd1-174">Once you're in hello console window and navigated into hello folder where hello webapps folder is located, issue hello following Git commands toolaunch hello process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="cffd1-175">После выдачи hello **принудительной** запроса, у пользователя запрашивается пароль hello создан ранее для учетных данных развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="cffd1-175">Once you issue hello **push** request, you'll be asked for hello password you created for hello deployment credential earlier.</span></span> <span data-ttu-id="cffd1-176">Введите свои учетные данные, вы увидите, что была развернута, hello обновления экрана портала.</span><span class="sxs-lookup"><span data-stu-id="cffd1-176">After you enter your credentials, you should see your portal display that hello update was deployed.</span></span>
7. <span data-ttu-id="cffd1-177">При использовании еще раз почтальон toohit hello вновь развернутые приложения API, запущенные в службе приложений Azure, вы увидите, что hello поведение согласуется и теперь он возвращает контактные данные должным образом, что с помощью простого кода изменения toohello Swagger.io формирования шаблонов код Java.</span><span class="sxs-lookup"><span data-stu-id="cffd1-177">If you once again use Postman toohit hello newly-deployed API App running in Azure App Service, you'll see that hello behavior is consistent and that now it is returning contact data as expected, and using simple code changes toohello Swagger.io scaffolded Java code.</span></span> 
   
    ![Использование REST API контактов Java в Azure в реальном времени][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="cffd1-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cffd1-179">Next steps</span></span>
<span data-ttu-id="cffd1-180">В этой статье были может toostart с Swagger JSON-файла и получить из редактора Swagger.io hello формирования шаблонов код Java.</span><span class="sxs-lookup"><span data-stu-id="cffd1-180">In this article, you were able toostart with a Swagger JSON file and some scaffolded Java code obtained from hello Swagger.io editor.</span></span> <span data-ttu-id="cffd1-181">В результате внесения простых изменений и развертывания Git вы получили рабочее приложение API, написанное на Java.</span><span class="sxs-lookup"><span data-stu-id="cffd1-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="cffd1-182">Hello Далее учебнике показано, каким образом слишком[использовать приложения API из клиентов JavaScript, с помощью CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="cffd1-182">hello next tutorial shows how too[consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="cffd1-183">Более поздней версии учебников по hello отображать ряды как tooimplement проверки подлинности и авторизации.</span><span class="sxs-lookup"><span data-stu-id="cffd1-183">Later tutorials in hello series show how tooimplement authentication and authorization.</span></span>

<span data-ttu-id="cffd1-184">toobuild об этом образце, Дополнительные сведения о hello [хранилища пакета SDK для Java] toopersist hello JSON BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="cffd1-184">toobuild on this sample, you can learn more about hello [Storage SDK for Java] toopersist hello JSON blobs.</span></span> <span data-ttu-id="cffd1-185">Или можно использовать hello [документа DB Java SDK] toosave tooAzure данные вашего контакта DB документа.</span><span class="sxs-lookup"><span data-stu-id="cffd1-185">Or, you could use hello [Document DB Java SDK] toosave your Contact data tooAzure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="cffd1-186">См. также</span><span class="sxs-lookup"><span data-stu-id="cffd1-186">See Also</span></span>
<span data-ttu-id="cffd1-187">Дополнительные сведения об использовании Azure с Java можно найти на [странице Azure для разработчиков Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="cffd1-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[портал Azure]: https://portal.azure.com/
[документа DB Java SDK]: ../documentdb/documentdb-java-application.md
[бесплатной пробной версии]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Developer Kit 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[JAX RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[интерактивном редакторе Swagger]: http://editor2.swagger.io/
[почтальон]: https://www.getpostman.com/
[хранилища пакета SDK для Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Swagger редактор]: http://editor.swagger.io/
[кода Visual Studio]: https://code.visualstudio.com

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
