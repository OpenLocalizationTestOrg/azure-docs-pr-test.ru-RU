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
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>Сборка и развертывание приложения API Java в службе приложений Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

В этом учебнике показано как toocreate приложения Java и развернуть ее tooAzure приложений из службы API приложений с помощью [Git]. Hello инструкциям этого учебника можно выполнять в любой операционной системе, поддерживающий работу Java. кода Hello в этот учебник построен с использованием [Maven]. [JAX RS] hello используется toocreate службы RESTful и создается на основании hello [Swagger] спецификации метаданных с помощью hello [Swagger редактор].

## <a name="prerequisites"></a>Предварительные требования
1. [Java Developer Kit 8] \((или более поздней версии).
2. [Maven] на компьютере, на котором ведется разработка.
3. [Git] на компьютере, на котором ведется разработка.
4. Платной или [бесплатной пробной версии] подписки слишком[Microsoft Azure]
5. Пример HTTP-приложения, например [почтальон]

## <a name="scaffold-hello-api-using-swaggerio"></a>API hello формирования шаблонов, с помощью Swagger.IO
В редакторе hello swagger.io документации можно ввести Swagger JSON или YAML код, представляющий структуру hello API. После получения контактной зоны hello API предназначен можно экспортировать кода для различных платформ и платформ. В следующем разделе hello hello формирования шаблонов код будет макетов tooinclude измененные функциональные возможности. 

Этой демонстрации начнется с текстом Swagger JSON, который можно будет вставить в редактор swagger.io hello, которой будут затем используется toogenerate кода осуществлять использование tooaccess JAX RS конечной точкой API. После этого требуется изменить hello формирования шаблонов код tooreturn фиктивные данные, имитируя API REST, построенных на вершине механизм сохраняемости данных.  

1. Скопируйте следующий буфер tooyour Swagger JSON кода hello:
   
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
2. Перейдите toohello [интерактивном редакторе Swagger]. Один раз, нажмите кнопку hello **файл -> Вставить JSON** элемента меню.
   
    ![Пункт меню "Вставить JSON"][paste-json]
3. Вставьте hello контакты список API Swagger JSON скопированное ранее. 
   
    ![Вставка JSON-кода в Swagger][pasted-swagger]
4. Просмотр страницы документации hello и Сводка по API, отображаемого в редакторе hello. 
   
    ![Просмотр документов, созданных при помощи Swagger][view-swagger-generated-docs]
5. Выберите hello **Server Создать -> JAX RS** меню параметр tooscaffold hello серверный код более поздней версии tooadd макетной реализации требуется изменить. 
   
    ![Пункт меню «Создать код»][generate-code-menu-item]
   
    После создания кода hello, будет предоставляться toodownload файла ZIP. Этот файл содержит код hello формирования шаблонов генератором кода hello Swagger и все связанные с ним создавать скрипты. Распакуйте каталог tooa hello всей библиотеки на рабочей станции разработки. 

## <a name="edit-hello-code-tooadd-api-implementation"></a>Изменение кода hello tooadd реализации API
В этом разделе вы замените hello Swagger кода, созданного на стороне сервера реализации пользовательского кода. новый код Hello вернет сущности ArrayList контакт toohello вызывающего клиента. 

1. Откройте hello *Contact.java* файла модели, который находится в hello *src/gen-java/операции ввода-вывода/swagger/модели* папки, с помощью [кода Visual Studio] или в привычном текстовом редакторе. 
   
    ![Открыть файл модели контактов][open-contact-model-file]
2. Добавьте следующий конструктор в hello hello **контакт** класса. 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. Откройте hello *ContactsApiServiceImpl.java* файл реализации службы, который находится в hello *src/main/java и операции ввода-вывода/swagger/api/impl* папки, с помощью [кода Visual Studio]или в привычном текстовом редакторе.
   
    ![Открыть файл кода службы контактов][open-contact-service-code-file]
4. Замените этот новый tooadd кода код службы toohello макетной реализации hello код в файле hello. 
   
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
5. Откройте командную строку и измените каталог toohello корневую папку приложения.
6. Выполните следующий код hello toobuild команды Maven hello и запустить его локально с помощью hello Jetty сервера приложений. 
   
        mvn package jetty:run
7. Должно появиться окно команд hello отражают, Jetty начала кода на порт 8080. 
   
    ![Открыть файл кода службы контактов][run-jetty-war]
8. Используйте [почтальон] метод toomake API toohello «получить все контакты» запроса в HTTP://localhost: 8080/api/контактов.
   
    ![Вызов hello Contacts API][calling-contacts-api]
9. Используйте [почтальон] метод toomake API «получить определенного контакта» toohello запроса, расположенной на http://localhost: 8080/api/contacts/2.
   
    ![Вызов hello Contacts API][calling-specific-contact-api]
10. Наконец создайте файл hello WAR Java (веб-архив), выполнив следующую команду Maven в консоли hello. 
    
         mvn package war:war
11. После построения hello WAR-файл, он будут помещены в hello **целевой** папки. Перейдите в hello **целевой** папку и переименуйте hello WAR-файла слишком**ROOT.war**. (Убедитесь, что этот формат соответствует hello регистр букв).
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. Наконец, выполните следующие команды из корневой папки hello toocreate вашего приложения hello **развертывание** папки toouse toodeploy hello WAR-файл tooAzure. 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>Публикация tooAzure hello выходных данных приложения службы
В этом разделе вы узнаете, как toocreate новое приложение API hello с помощью портала Azure подготовить приложение API для размещения приложений Java и развертывание hello только что созданный WAR файла tooAzure toorun службы приложений нового приложения API. 

1. Создание нового приложения API в hello [портал Azure], щелкнув hello **New -> Web + Mobile -> приложения API** пункт меню, введя свои данные приложения и выбрав **создать**.
   
    ![Создать приложение API][create-api-app]
2. После создания приложения API откройте ваше приложение **параметры** колонки и нажмите кнопку hello **параметры приложения** элемента меню. Выберите hello последние версии Java из доступных параметров hello, а затем выберите hello последнюю Tomcat из hello **контейнера Web** меню, а затем нажмите **Сохранить**.
   
    ![Настроить Java в колонки API приложения hello][set-up-java]
3. Нажмите кнопку hello **учетные данные развертывания** меню параметров элемент и укажите имя пользователя и пароль, который toouse для публикации файлов tooyour приложения API. 
   
    ![Сброс учетных данных развертывания][deployment-credentials]
4. Нажмите кнопку hello **источник развертывания** параметры пункта меню. Один раз, нажмите кнопку hello **выбрать источник** кнопку, выберите hello **локального репозитория Git** , а затем щелкните **ОК**. В результате будет создан работающий в Azure репозиторий Git, который связан с приложением API. Каждый раз при фиксации кода toohello *master* ветви репозитория Git, код будет опубликован в вашей динамической запущенный экземпляр приложения API. 
   
    ![Настройка локального репозитория Git][select-git-repo]
5. Копировать hello новый репозиторий Git в буфер обмена tooyour URL-адрес. Сохраните его, потому что он понадобится чуть позже. 
   
    ![Настройка нового репозитория Git для приложения][copy-git-repo-url]
6. Принудительная hello WAR файл toohello online репозитории. toodo это, перейдите в hello **развертывание** папку, созданную ранее, чтобы легко можно зафиксировать кода hello toohello хранилища в службе приложений. Один раз в окно консоли hello и к которому необходимо перейти в папку hello, где находится папка веб-приложения hello, выдача hello, следуйте процедуре hello toolaunch команды Git и запускать развертывание. 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    После выдачи hello **принудительной** запроса, у пользователя запрашивается пароль hello создан ранее для учетных данных развертывания hello. Введите свои учетные данные, вы увидите, что была развернута, hello обновления экрана портала.
7. При использовании еще раз почтальон toohit hello вновь развернутые приложения API, запущенные в службе приложений Azure, вы увидите, что hello поведение согласуется и теперь он возвращает контактные данные должным образом, что с помощью простого кода изменения toohello Swagger.io формирования шаблонов код Java. 
   
    ![Использование REST API контактов Java в Azure в реальном времени][postman-calling-azure-contacts]

## <a name="next-steps"></a>Дальнейшие действия
В этой статье были может toostart с Swagger JSON-файла и получить из редактора Swagger.io hello формирования шаблонов код Java. В результате внесения простых изменений и развертывания Git вы получили рабочее приложение API, написанное на Java. Hello Далее учебнике показано, каким образом слишком[использовать приложения API из клиентов JavaScript, с помощью CORS][App Service API CORS]. Более поздней версии учебников по hello отображать ряды как tooimplement проверки подлинности и авторизации.

toobuild об этом образце, Дополнительные сведения о hello [хранилища пакета SDK для Java] toopersist hello JSON BLOB-объектов. Или можно использовать hello [документа DB Java SDK] toosave tooAzure данные вашего контакта DB документа. 

<a name="see-also"></a>

## <a name="see-also"></a>См. также
Дополнительные сведения об использовании Azure с Java можно найти на [странице Azure для разработчиков Java](/java/azure).

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
