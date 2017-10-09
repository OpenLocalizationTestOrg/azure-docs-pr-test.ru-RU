---
title: "aaaAdd tooAzure приложения Java веб-приложений служб приложений"
description: "Этом учебнике показано, как tooadd приложения или страницы tooyour экземпляр веб-приложениях Azure приложения службы, который уже настроен toouse Java."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a>Добавить tooAzure приложения Java веб-приложений служб приложений
После инициализации веб-приложения Java в [службе приложений Azure] [ Azure App Service] как описано в статье [Создание веб-приложения Java в службе приложений Azure](web-sites-java-get-started.md), можно отправить приложение путем размещения Ваш WAR в hello **веб-приложений** папки.

Здравствуйте, toohello пути навигации **веб-приложений** папки зависит от настройки экземпляра веб-приложений.

* Если настройка веб-приложения с помощью hello Azure Marketplace, hello путь toohello **веб-приложений** папка находится в форме hello **d:\home\site\wwwroot\bin\application\_server\webapps**, где **приложения\_сервера** — hello имя сервера приложения hello в силе для конкретного экземпляра веб-приложений. 
* Если настройка веб-приложения с помощью hello Azure пользовательский Интерфейс конфигурации hello путь toohello **веб-приложений** папка находится в форме hello **d:\home\site\wwwroot\webapps**. 

Обратите внимание что tooupload управления источника можно использовать приложение или веб-страницы, включая [сценариев непрерывной интеграции](app-service-continuous-deployment.md). FTP может также использоваться для загрузки приложения или веб-страниц. Дополнительные сведения о развертывании приложений через FTP см. в разделе [развертывание вашего приложения tooAzure службы приложений].

Примечание для веб-приложений Tomcat: после отправки вашего WAR файл toohello **веб-приложений** папки, сервера приложений Tomcat hello обнаружит добавили его и автоматически загружает его. Обратите внимание, что при копировании файлов (кроме WAR-файлы) toohello КОРНЕВОЙ каталог сервера приложений hello будет toobe перезапуска перед использованием этих файлов. функция Hello автозагрузки (AutoLoad) для веб-приложений Tomcat Java hello, работающих в Azure основана на новый WAR-файл добавляется или новые файлы или каталоги добавляются toohello **веб-приложений** папки. 

<a name="see-also"></a>

## <a name="see-also"></a>См. также
Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure].

[application-insights-app-insights-java-get-started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[развертывание вашего приложения tooAzure службы приложений]: ./web-sites-deploy.md
