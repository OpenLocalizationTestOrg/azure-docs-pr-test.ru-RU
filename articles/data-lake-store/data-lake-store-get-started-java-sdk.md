---
title: "aaaUse hello Java SDK toodevelop приложения в хранилище Озера данных Azure | Документы Microsoft"
description: "Использовать хранилище Озера данных Azure, Java SDK toocreate учетной записи хранилища Озера данных и выполнения основных операций в hello хранилища Озера данных"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a>Начало работы с хранилищем озера данных Azure с помощью Java
> [!div class="op_single_selector"]
> * [Портал](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Пакет SDK для .NET](data-lake-store-get-started-net-sdk.md)
> * [Пакет SDK для Java](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Узнайте, как основных операций SDK для Java хранилища Озера данных Azure hello tooperform toouse такие как создание папками, отправка и загрузка файлов данных и т. д. Дополнительные сведения об Azure Data Lake Store см. в [этой статье](data-lake-store-overview.md).

Можно открыть документы hello API пакета SDK для Java для хранилища Озера данных Azure в [API Java хранилища Озера данных Azure docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).

## <a name="prerequisites"></a>Предварительные требования
* Комплект разработчика Java (JDK 7 или более поздней версии с использованием Java версии 1.7 или более поздней).
* Учетная запись Azure Data Lake Store. Следуйте инструкциям hello в [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](data-lake-store-get-started-portal.md).
* [Maven](https://maven.apache.org/install.html). В этом руководстве это средство используется для создания зависимостей проекта. Несмотря на возможные toobuild без использования системы построения как Maven или Gradle, убедитесь, этих систем является гораздо проще toomanage зависимости.
* Интегрированная среда разработки, например [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) или аналогичная (необязательно).

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Как выполнить аутентификацию с помощью Azure Active Directory?
В этом учебнике мы используем tooretrieve клиента секрет маркера Azure Active Directory (проверка подлинности service to service) приложения Azure AD. Мы используем этот токен toocreate файл хранилища Озера данных tooperform объекта клиента операций и операций с каталогами. Инструкции по как tooauthenticate с помощью хранилища Озера данных Azure hello секрет клиента мы выполните следующие общие действия hello.

1. Создать веб-приложение Azure AD.
2. Получить идентификатор клиента hello, секрет клиента и конечная точка маркера для hello веб-приложения Azure AD.
3. Настройка доступа для веб-приложения hello Azure AD в хранилище Озера данных файла или папки, будет tooaccess из приложения Java, который вы создаете hello hello.

Инструкции по tooperform следующие действия. в статье [создать приложение Active Directory](data-lake-store-authenticate-using-active-directory.md).

Azure Active Directory предоставляет другие параметры также tooretrieve маркер. Можно выбрать из ряд toosuit механизмов проверки подлинности, отличный сценария, например, приложение, работающее в браузере, распространяемых в виде классического приложения приложение или серверное приложение выполняется локально или в Azure виртуальные компьютер. Доступны также различные типы учетных данных, например пароли, сертификаты, метод двухфакторной проверки подлинности и т. д. Кроме того, Azure Active Directory позволяет toosynchronize локальных пользователей Active Directory с облаком hello. Дополнительные сведения см. в статье [Сценарии аутентификации в Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md). 

## <a name="create-a-java-application"></a>Создание приложения Java
Образец кода Hello доступных [на GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) пошагово рассматривается процесс hello Создание файлов в хранилище hello, объединения файлов, загрузку файла, и удалить некоторые файлы в хранилище hello. В этом разделе статьи hello пошаговыми руководствами по hello основной части кода hello.

1. Создайте проект Maven с помощью [архетипа mvn](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) hello из командной строки или с помощью интегрированной среды разработки. Инструкции как проект с помощью IntelliJ toocreate Java см. в разделе [здесь](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html). Дополнительные сведения о разделе toocreate проект с помощью Eclipse, [здесь](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm). 
2. Добавьте следующие зависимости tooyour Maven hello **pom.xml** файла. Добавьте следующий фрагмент текста между hello hello  **\</Version >** тег и hello  **\</project >** тег:
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    Первая зависимость Hello — toouse hello SDK хранилища Озера данных (`azure-data-lake-store-sdk`) из репозитория maven hello. Здравствуйте, вторая зависимость (`slf4j-nop`) является toospecify toouse framework какие ведения журнала для этого приложения. Hello SDK хранилища Озера данных использует [slf4j](http://www.slf4j.org/) фасадной ведения журнала, которая позволяет выбирать из нескольких популярных ведения журнала платформы, такие как log4j, ведение журнала, logback, т. д., Java или без регистрации. В этом примере мы будет отключить ведение журнала, поэтому мы используем hello **slf4j nop** привязки. toouse см. другие параметры ведения журнала в вашем приложении [здесь](http://www.slf4j.org/manual.html#projectDep).

### <a name="add-hello-application-code"></a>Добавьте код приложения hello
Существует три основные части toohello кода.

1. Получить маркер hello Azure Active Directory
2. С помощью маркера toocreate hello клиента хранилища Озера данных.
3. Использование клиента tooperform hello хранилища Озера данных операций.

#### <a name="step-1-obtain-an-azure-active-directory-token"></a>Шаг 1. Получение маркера Azure Active Directory
Hello SDK хранилища Озера данных предоставляет удобные методы, позволяющие управлять hello маркеров безопасности требуется tootalk toohello хранилища Озера данных. Однако hello SDK не требует использования только эти методы. Можно использовать другие средства получения токена, например использование hello [пакет SDK Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java), или пользовательский код.

hello toouse токен tooobtain SDK хранилища Озера данных для приложения hello Active Directory Web, созданного ранее, используйте один из подклассов hello `AccessTokenProvider` (hello приведенном ниже примере используется `ClientCredsTokenProvider`). Поставщик маркеров кэши Hello hello-учетные данные используется токен tooobtain hello в памяти и автоматически обновляет токен hello, если он стал примерно tooexpire. Это возможно toocreate собственные подклассы `AccessTokenProvider` токены извлекаются в коде клиента, но сейчас Давайте просто hello использования одного, предоставляемых в hello SDK.

Замените **ЗАПОЛНЕНИЯ здесь** hello фактическими значениями для hello Azure Active Directory, веб-приложения.

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a>Шаг 2. Создание клиентского объекта Azure Data Lake Store (ADLStoreClient)
Создание [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) объект требует toospecify hello хранилища Озера данных учетной записи имя и hello поставщик маркеров был создан в последнем шаге hello. Обратите внимание, что hello хранилища Озера данных учетной записи, имя должно toobe полное доменное имя. Например, замените часть **FILL-IN-HERE** примерно таким значением: **mydatalakestore.azuredatalakestore.net**.

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a>Шаг 3: Используйте hello ADLStoreClient tooperform файлов и каталогов операции
Приведенный ниже код Hello содержит фрагменты примеров некоторых распространенных операций. Вы можете просмотреть полный hello [docs API пакета SDK для Java хранилища Озера данных](https://azure.github.io/azure-data-lake-store-java/javadoc/) из hello **ADLStoreClient** объекта toosee других операций.

Обратите внимание, что чтение файлов и запись в них осуществляется с помощью стандартных потоков Java. Это означает, что слоя любого из потоков Java по hello поверх hello хранилища Озера данных потоки toobenefit из стандартных функциональных возможностей Java (например, печать потоков для Форматированные выходные данные или any hello сжатия или шифрования потоков для дополнительных возможностей сверху, и т. д.).

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a>Шаг 4: Построение и запуск приложения hello
1. toorun из в IDE, найдите и нажмите клавишу hello **запуска** кнопки. toorun из Maven, используйте [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).
2. автономный JAR-файл, который можно запустить из jar hello построения из командной строки с включен, все зависимости с помощью hello tooproduce [подключаемого модуля сборки Maven](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html). Здравствуйте, pom.xml в hello [примере исходный код на github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) приводится пример того, как toodo это.

## <a name="next-steps"></a>Дальнейшие действия
* [Просмотр JavaDoc для пакета Java SDK hello](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)

