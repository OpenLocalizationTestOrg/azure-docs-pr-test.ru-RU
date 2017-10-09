---
title: "Источник aaaOpen технологии часто задаваемые вопросы про Azure веб-приложений | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о технологиях открытым исходным кодом в веб-приложения hello функция службы приложений Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a>Часто задаваемые вопросы о технологиях с открытым кодом в веб-приложениях Azure

Данная статья содержит ответы toofrequently, задаваемые вопросы (FAQ) о проблемах, связанных с открытым исходным кодом технологии для hello [веб-приложений функции службы приложений Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a>База данных ClearDB не работает. Как решить эту проблему?

По вопросам, связанным с базами данных, обращайтесь в [службу поддержки ClearDB](https://www.cleardb.com/developers/help/support). 

Ответы toocommon ответы на вопросы о ClearDB см [ClearDB часто задаваемые вопросы о](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a>Почему Моя база данных ClearDB отсутствует в портале hello

Если создать базу данных ClearDB в hello [портал Azure](http://portal.azure.com/), hello базы данных не отображается в hello [классический портал Azure](http://manage.windowsazure.com/). toowork этой может вручную связать веб-приложения toohello базы данных.

Аналогично Если создать базу данных ClearDB в hello [классический портал Azure](http://manage.windowsazure.com/), вы не увидите базу данных в hello [портал Azure](http://portal.azure.com/). Для этой ситуации нет решения. 

Дополнительные сведения см. в статье [Часто задаваемые вопросы о базах данных ClearDB MySql в службе приложений Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a>Почему не удалось перенести базу данных ClearDB при переносе подписки?

При переносе ресурсов из одной подписки в другую действуют некоторые ограничения. База данных ClearDB MySQL — это сторонняя служба, и она не перемещается при переносе подписки Azure.

Если вы не управляете hello миграции базы данных MySQL, прежде чем переносить ресурсы Azure, базу данных ClearDB MySQL могут быть недоступны. tooavoid этого, во-первых, вручную перенести базу данных ClearDB, а затем перенести hello подписки Azure для веб-приложения.

Дополнительные сведения см. в статье [Часто задаваемые вопросы о базах данных ClearDB MySql в службе приложений Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a>Как включить ведение журнала tootroubleshoot PHP проблемы PHP?

tooturn PHP ведения журнала:

1. Войдите в tooyour [Kudu веб-сайт](https://*yourwebsitename*.scm.azurewebsites.net).
2. В верхнем меню hello, выберите **консоли отладки** > **CMD**.
3. Выберите hello **сайта** папки.
4. Выберите hello **wwwroot** папки.
5. Выберите hello  **+**  значок, а затем выберите **новый файл**.
6. Задайте имя файла hello слишком**. user.ini**.
7. Выберите значок карандаша hello Далее слишком**. user.ini**.
8. Добавьте следующий код в файл hello:`log_errors=on`
9. Щелкните **Сохранить**.
10. Выберите значок карандаша hello Далее слишком**wp-config.php**.
11. Изменить toohello текста hello, следующий код:
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. В hello портал Azure, в меню приложения веб-hello перезапустите веб-приложения.

Дополнительные сведения см. в записи блога [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Включение журналов ошибок WordPress).

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a>Как включить ведение журнала ошибок в приложениях Python, размещенных в службе приложений?

ошибки приложения Python toocapture:

1. В hello портал Azure, в веб-приложения выберите **параметры**.
2. На hello **параметры** выберите **параметры приложения**.
3. В разделе **параметры приложения**, введите hello следующая пара ключ значение:
    * Ключ: WSGI_LOG.
    * Значение: D:\home\site\wwwroot\logs.txt (введите собственное имя файла).

Теперь вы увидите ошибки в файле logs.txt hello в папке wwwroot hello.

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a>Как изменить версию hello hello Node.js приложений, размещенных в службе приложений?

версии hello toochange hello Node.js приложения, можно использовать один из следующих вариантов hello:

*   В hello портал Azure, используйте **параметры приложения**.
    1. В hello портал Azure перейдите tooyour веб-приложения.
    2. На hello **параметры** колонке выберите **параметры приложения**.
    3. В **параметры приложения**, можно включить WEBSITE_NODE_DEFAULT_VERSION как ключ hello и hello версии Node.js необходимо в качестве значения hello.
    4. Go tooyour [Kudu консоли](https://*yourwebsitename*.scm.azurewebsites.net).
    5. toocheck Здравствуйте Node.js версии, введите следующую команду hello:  
   ```
   node -v
   ```
*   Измените файл iisnode.yml hello. Изменение версии hello Node.js в файле iisnode.yml hello только задает hello среды выполнения, iisnode использует. Ваш Kudu cmd, а другие — по-прежнему использовать hello Node.js версии, который задан в **параметры приложения** в hello портал Azure.

    tooset hello iisnode.yml вручную, создайте файл iisnode.yml в корневой папке приложения. В файле hello включите hello, следующей строкой:
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   Задать hello iisnode.yml файла с помощью package.json во время развертывания исходного элемента управления.
    Hello процесс развертывания управления Azure источника включает в себя hello следующие шаги:
    1. Перемещение содержимого toohello веб-приложение Azure.
    2. Создает скрипт развертывания по умолчанию, если его нет (deploy.cmd, .deployment файлы) в hello веб-приложения корневой папке.
    3. Запускает скрипт развертывания, в котором создается файл iisnode.yml Если упоминается hello Node.js версии в файле package.json hello > ядра`"engines": {"node": "5.9.1","npm": "3.7.3"}`
    4. файл iisnode.yml Hello имеет hello, следующей строкой кода:
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a>Я вижу приветственное сообщение «Ошибка при установке подключения к базе данных» в моем приложении WordPress, размещенного в службе приложений. Как устранить эту проблему?

Если вы видите эту ошибку в Azure WordPress приложения, tooenable php_errors.log и debug.log, полный hello шаги подробно описаны в [WordPress, включить журналы ошибок](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

При включении журналы hello воспроизвести ошибки hello и проверьте hello журналы toosee при запуске из подключений:
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

При появлении этой ошибки в файлах debug.log или php_errors.log приложения превышает hello число подключений. Если вы размещаете на ClearDB, проверьте hello число подключений, доступных в вашей [план обслуживания](https://www.cleardb.com/pricing.view).

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a>Как отлаживать приложение Node.js, размещенное в службе приложений?

1.  Go tooyour [Kudu консоли](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).
2.  Папка logs приложения перейдите tooyour (D:\home\LogFiles\Application).
3.  В файле logging_errors.txt hello проверьте содержимое.

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a>Как установить собственные модули Python в веб-приложении службы приложений или приложении API?

Некоторые пакеты невозможно установить с помощью pip в Azure. Hello пакета могут быть недоступны на hello индекс пакета Python или компилятор может потребоваться (компилятора недоступен на компьютере hello, на котором выполняется веб-приложение hello в службе приложений). Сведения об установке собственных модулей в веб-приложениях службы приложений или приложениях API см. в [этой записи блога](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a>Развертывание Django приложение tooApp службы с помощью Git и hello новой версии Python

Сведения об установке Django см. в разделе [развертывание Django приложение tooApp службы](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).

## <a name="where-are-hello-tomcat-log-files-located"></a>Где находятся файлы журналов Tomcat hello, расположенные?

Для развертываний Microsoft Azure Marketplace и пользовательских развертываний:

* Расположение папки: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs.
* Необходимые файлы:
    * catalina.*ГГГГ-ММ-ДД*.log
    * host-manager.*ГГГГ-ММ-ДД*.log
    * localhost.*ГГГГ-ММ-ДД*.log
    * manager.*ГГГГ-ММ-ДД*.log
    * site_access_log.*ГГГГ-ММ-ДД*.log


Для развертываний из меню **Параметры приложения** портала:

* Расположение папки: D:\home\LogFiles.
* Необходимые файлы:
    * catalina.*ГГГГ-ММ-ДД*.log
    * host-manager.*ГГГГ-ММ-ДД*.log
    * localhost.*ГГГГ-ММ-ДД*.log
    * manager.*ГГГГ-ММ-ДД*.log
    * site_access_log.*ГГГГ-ММ-ДД*.log

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a>Как устранить ошибки подключения драйвера JDBC Driver?

Может появиться следующие сообщения в журналах Tomcat hello:

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

Ошибка hello tooresolve:

1. Удалите файл sqljdbc*.jar hello из папки приложения/lib.
2. Если вы используете hello пользовательского Tomcat или Azure Marketplace Tomcat веб-сервера, скопируйте эту папку lib файл toohello .jar Tomcat.
3. При включении Java из hello портал Azure (выберите **Java 1.8** > **сервера Tomcat**), копия sqljdbc.* hello jar-файл в папке hello, tooyour параллельные приложения. Затем добавьте следующие файл web.config toohello параметр classpath hello:

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a>Почему возникают ошибки при попытке toocopy файлы журнала в режиме реального времени?

При попытке toocopy динамической журнала файлов для приложения Java (например, Tomcat), может отображаться следующая ошибка FTP:

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

сообщение об ошибке Hello может зависеть от клиента hello FTP.

Все приложения Java имеют эту проблему. Только Kudu поддерживает загрузку этого файла во время выполнения приложение hello.

Остановка приложение hello позволяет доступа по FTP toothese файлов.

Другое решение — toowrite веб-задания, который выполняется по расписанию и копирует эти файлы tooa другой каталог. Пример проекта, в разделе hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) проекта.

## <a name="where-do-i-find-hello-log-files-for-jetty"></a>Расположение файлов журнала hello для Jetty

Marketplace и развертывание пользовательских hello файл журнала находится в папке D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs hello. Обратите внимание, что расположение папки hello зависит от версии hello Jetty, вы используете. Например путь hello предназначена для Jetty 9.1.2. Найдите файл jetty_*ГГГГ_ММ_ДД*.stderrout.log.

Для развертываний портала параметр приложения hello файл журнала находится в D:\home\LogFiles. Найдите файл jetty_*ГГГГ_ММ_ДД*.stderrout.log.

## <a name="can-i-send-email-from-my-azure-web-app"></a>Можно ли отправлять электронные сообщения из веб-приложения Azure?

Служба приложений не имеет встроенной функции отправки электронных сообщений. Альтернативные варианты отправки электронных сообщений из приложения см. в [этом обсуждении Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a>Почему моего сайта WordPress перенаправления tooanother URL-адрес?

Если вы недавно перенесли tooAzure WordPress может перенаправить toohello старые URL-адрес домена. Это вызвано параметр базы данных MySQL hello.

WordPress контактному лицу + — это расширение узла Azure, можно использовать URL-адрес перенаправления hello tooupdate непосредственно в базе данных hello. Дополнительные сведения об использовании WordPress Buddy+ см. в записи блога [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Средства WordPress и перенос базы данных MySQL с помощью WordPress Buddy+).

Кроме того, при желании URL-адреса перенаправления hello toomanually обновления с помощью SQL-запросы или PHPMyAdmin см [WordPress: перенаправление URL-адрес toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a>Как изменить пароль для входа в WordPress?

Если вы забыли пароль входа в WordPress, можно использовать WordPress контактному лицу + tooupdate его. ваш пароль, hello установки WordPress контактному лицу + Azure расширение сайта последующем выполнении hello шаги описаны в tooreset [WordPress средства и миграции MySQL WordPress контактному лицу +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a>Не удается выполнить вход tooWordPress Как решить эту проблему?

Если вы не можете войти в WordPress после установки подключаемого модуля, возможно, вы установили не тот модуль. WordPress Buddy+ — это расширение сайта Azure, с помощью которого можно отключить подключаемые модули в WordPress. Дополнительные сведения см. в записи блога [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Средства WordPress и перенос базы данных MySQL с помощью WordPress Buddy+).

## <a name="how-do-i-migrate-my-wordpress-database"></a>Как перенести базу данных WordPress?

У вас есть несколько вариантов для миграции базы данных MySQL hello, веб-сайт WordPress подключенных tooyour:

* Разработчики: Используйте hello [командной строки или PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)
* с помощью [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (остальные пользователи).

## <a name="how-do-i-help-make-wordpress-more-secure"></a>Как повысить уровень защиты WordPress?

toolearn о рекомендациях по безопасности для WordPress, в разделе [советы и рекомендации по обеспечению безопасности WordPress Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a>Удается toouse PHPMyAdmin и hello сообщение «Доступ запрещен». Как решить эту проблему?

Данная проблема возникает, если в приложении функции hello MySQL еще не запущена в данном экземпляре службы приложений. tooresolve hello проблему, попробуйте tooaccess веб-сайта. При этом запустится hello необходимых процессов, включая процесс hello MySQL в приложении. tooverify с MySQL, выполняется в приложении в обозреватель процессов, убедитесь, что mysqld.exe указывается в процессах hello.

Убедившись, что MySQL в приложении работает, попробуйте toouse PHPMyAdmin.

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a>Произошла ошибка HTTP 403 при экспорте базы данных MySQL в приложении с помощью PHPMyadmin или повторите tooimport. Как решить эту проблему?

Это известная ошибка в старой версии браузера Chrome. проблема tooresolve hello, новая версия обновления tooa Chrome. Также попробуйте использовать другой браузер, например Internet Explorer или Edge, где hello проблема не возникает.
