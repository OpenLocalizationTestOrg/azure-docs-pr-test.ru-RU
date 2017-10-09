---
title: "aaaRestrict доступ с помощью подписанных URL - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toorestrict подписей общего доступа toouse HDInsight доступ к toodata хранится в BLOB-объектов хранилища Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a>Использование подписей общего доступа Azure хранилища toorestrict доступа toodata в HDInsight

HDInsight имеет полный доступ toodata в учетных записях хранения Azure hello, связанные с кластером hello. Подписанные URL-адреса можно использовать на toohello hello BLOB-объектов контейнера toorestrict доступа к данным. Например tooprovide данные toohello доступ только для чтения. Подписи общего доступа (SAS) являются возможностью учетных записей хранилища Azure, которая позволяет вам toodata toolimit доступа. Например предоставляя toodata доступ только для чтения.

> [!IMPORTANT]
> Чтобы создать решение на основе Apache Ranger, попробуйте использовать HDInsight, присоединенный к домену. Дополнительные сведения см. в разделе hello [настройки присоединенных к домену HDInsight](hdinsight-domain-joined-configure.md) документа.

> [!WARNING]
> HDInsight должны иметь полный доступ toohello по умолчанию хранилища для кластера hello.

## <a name="requirements"></a>Требования

* Подписка Azure
* C# или Python. Пример кода на C# предоставлен в решении Visual Studio.

  * Требуется Visual Studio версии 2013, 2015 или 2017.
  * Требуется Python версии 2.7 или более новой.

* Кластер HDInsight под управлением Linux или [Azure PowerShell] [ powershell] -при наличии существующего кластера под управлением Linux, можно использовать Ambari tooadd кластера toohello подписи общего доступа. В противном случае можно использовать Azure PowerShell toocreate кластер и добавить подпись общего доступа во время создания кластера.

    > [!IMPORTANT]
    > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Здравствуйте, файлы примеров из [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature). Этот репозиторий содержит hello следующих элементов:

  * Проект Visual Studio, способный создать контейнер хранилища, хранимую политику и SAS для использования с HDInsight.
  * Сценарий Python, способный создать контейнер хранилища, хранимую политику и SAS для использования с HDInsight.
  * Сценарий PowerShell, можно создать HDInsight кластера и настроить его toouse hello SAS.

## <a name="shared-access-signatures"></a>Подписи коллективного доступа

Существуют две формы подписанных URL-адресов:

* Нерегламентированный: hello время начала, время окончания и разрешения для hello SAS указаны на hello универсальный код Ресурса SAS.

* Хранимая политика доступа. Хранимая политика доступа определяется в контейнере ресурсов, например в контейнере больших двоичных объектов. Политики могут быть ограничения используемых toomanage для одного или нескольких подписей общего доступа. При связывании подписанный URL-адрес с хранимой политикой доступа hello SAS наследует ограничения hello - hello время начала, время окончания и разрешения -, определенные для hello хранимые политики доступа.

Hello различия между hello двух форм являются важными для одного ключевого сценария: отзыва. Подписанный URL-адрес является URL-адрес, поэтому любой пользователь получает hello SAS можно использовать, независимо от того, кто запросил toobegin с. Если открыто опубликована SAS, он может использоваться кем Здравствуй, мир!. Распространяемая подпись общего доступа действительна до тех пор, пока не произойдет одно из четырех возможных событий:

1. Hello окончания времени, указанного на hello достижения SAS.

2. Hello срок действия указанного hello хранимой политике доступа, ссылается hello достижения SAS. Hello следующие сценарии вызвать hello срок достигнут toobe:

    * Hello время интервала времени.
    * Hello хранимые политики доступа-измененный toohave время истечения срока действия в прошлом hello. Изменение hello срок — один из способов toorevoke hello SAS.

3. Hello хранимой политики доступа, ссылается hello удаляется SAS, который является другим способом toorevoke hello SAS. При повторном создании hello хранимые политики доступа в hello точно такое же имя, все маркеры SAS для предыдущей политики hello действительны (если не прошел срок hello на hello SAS). Если предполагается toorevoke hello SAS, быть убедиться, что toouse другое имя при повторном создании hello политики доступа в будущем hello срока истечения срока действия.

4. ключ учетной записи Hello, используемые toocreate hello SAS повторно. Идет повторное создание ключа hello в результате все приложения, использующие hello предыдущих toofail ключа, проверки подлинности. Обновите все компоненты toohello новый ключ.

> [!IMPORTANT]
> URI подписи коллективного доступа связан с сигнатурой hello toocreate ключа используется учетная запись hello и hello связанных хранимой политики доступа (если таковые имеются). Если хранимая политика доступа не указан, hello только способом toorevoke подписанный URL-адрес является ключ учетной записи toochange hello.

Рекомендуется всегда использовать хранимые политики доступа. При использовании хранимых политик, можно отменить подписи или расширить hello даты истечения срока действия при необходимости. Hello в данном пошаговом руководстве используется toogenerate политики доступа SAS.

Дополнительные сведения о подписей общего доступа см. в разделе [основные сведения о модели SAS hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="create-a-stored-policy-and-sas-using-c"></a>Создание хранимой политики и SAS с использованием C\#

1. Откройте решение hello в Visual Studio.

2. В обозревателе решений щелкните правой кнопкой мыши на hello **SASToken** проект и выберите **свойства**.

3. Выберите **параметры** и добавьте значения для hello следующие записи:

   * StorageConnectionString: hello строка соединения для hello хранилища учетной записи, которую toocreate хранимых политик и SAS для. Hello формат должен быть `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` где `myaccount` hello имя вашей учетной записи хранилища и `mykey` hello ключ для учетной записи хранения hello.

   * Имя контейнера: hello контейнер в учетной записи хранения hello, которым требуется доступ toorestrict.

   * SASPolicyName: hello toouse имя для hello хранятся toocreate политики.

   * FileToUpload: hello путь tooa файл, отправленный toohello контейнера.

4. Запустите проект hello. После создания hello SAS, отображаются сведения аналогичные toohello после текста:

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Сохраните hello маркера политики SAS, имя учетной записи хранилища и имя контейнера. Эти значения используются при связывании учетной записи хранилища hello с кластером HDInsight.

### <a name="create-a-stored-policy-and-sas-using-python"></a>Создание хранимой политики и SAS с использованием Python

1. Откройте файл SASToken.py hello и измените hello следующие значения:

   * политика\_name: hello toouse имя для hello хранимых toocreate политики.

   * хранилище\_учетной записи\_name: hello имя вашей учетной записи хранилища.

   * хранилище\_учетной записи\_ключ: hello ключ учетной записи хранения hello.

   * хранилище\_контейнера\_name: hello контейнера в учетной записи хранения hello, которым требуется доступ toorestrict.

   * Пример\_файл\_путь: hello путь tooa файл, отправленный toohello контейнера.

2. Запустите сценарий hello. Она отображает hello SAS маркера аналогичные toohello после текста после завершения сценария hello:

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Сохраните hello маркера политики SAS, имя учетной записи хранилища и имя контейнера. Эти значения используются при связывании учетной записи хранилища hello с кластером HDInsight.

## <a name="use-hello-sas-with-hdinsight"></a>Использовать hello SAS с HDInsight

При создании кластера HDInsight необходимо указать основную учетную запись хранения; дополнительные учетные записи хранения указываются по желанию. Оба метода добавления хранилища требуется полный доступ учетных записей хранения toohello и контейнеров, которые используются.

toouse контейнер tooa доступа toolimit подписи общего доступа, добавьте toohello настраиваемой записи **сайта основные** конфигурации для кластера hello.

* Для **на основе Windows** или **под управлением Linux** кластеров HDInsight, вы можете добавить запись hello во время создания кластера с помощью PowerShell.
* Для **под управлением Linux** кластеров HDInsight изменить конфигурацию hello после создания кластера, с помощью Ambari.

### <a name="create-a-cluster-that-uses-hello-sas"></a>Создать кластер, который использует hello SAS

Пример создания кластера HDInsight, hello использует SAS включается в hello `CreateCluster` каталог репозитория hello. toouse, которую он hello используйте следующие шаги:

1. Откройте hello `CreateCluster\HDInsightSAS.ps1` файл в текстовом редакторе и измените следующие значения в начале документа hello hello hello.

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    Например, изменить `'mycluster'` toohello имя кластера hello требуется toocreate. Hello SAS значения должны совпадать значения hello hello предыдущих шагах, при создании учетной записи хранилища и маркер SAS.

    После изменения значения hello сохраните файл hello.

2. Откройте командную строку Azure PowerShell. Если вы не знакомы с модулем Azure PowerShell или он у вас не установлен, см. статью [Установка и настройка служб Azure PowerShell][powershell].

1. В строке приветствия используйте hello, следующая команда tooauthenticate tooyour подписки Azure:

    ```powershell
    Login-AzureRmAccount
    ```

    При появлении соответствующего запроса войдите в систему hello учетной записи для подписки Azure.

    Если ваша учетная запись связана с несколькими подписками Azure, может потребоваться toouse `Select-AzureRmSubscription` tooselect hello подписки нужно toouse.

4. Из строки hello измените каталоги toohello `CreateCluster` каталог, содержащий файл HDInsightSAS.ps1 hello. Затем используйте следующий сценарий hello toorun hello

    ```powershell
    .\HDInsightSAS.ps1
    ```

    Как сценарий выполняется hello она записывает выходные данные командной строки PowerShell toohello при создании ресурса hello группы и хранения учетных записей. Вы являетесь пользователем hello HTTP запрос tooenter для hello кластера HDInsight. Эта учетная запись является кластера toohello доступа используется toosecure HTTP в секунду.

    При создании кластера под управлением Linux запрашивается имя учетной записи пользователя SSH и пароль. Эта учетная запись является журнала используется tooremotely toohello кластера.

   > [!IMPORTANT]
   > Когда появится сообщение hello HTTP/s или SSH имя пользователя и пароль, необходимо указать пароль, отвечающий hello следующие условия:
   >
   > * содержит не меньше 10 символов;
   > * содержит хотя бы одну цифру;
   > * содержит хотя бы один специальный символ;
   > * содержит хотя бы одну букву в верхнем или нижнем регистре.

Это занимает немного времени для этого сценария toocomplete, обычно около 15 минут. По завершении сценария hello без ошибок после создания кластера hello.

### <a name="use-hello-sas-with-an-existing-cluster"></a>Использовать hello SAS с существующего кластера

При наличии существующего кластера под управлением Linux, можно добавить hello SAS toohello **сайта основные** конфигурации с помощью hello следующие шаги:

1. Откройте hello Ambari web пользовательского интерфейса для кластера. Hello адрес для этой страницы является https://YOURCLUSTERNAME.azurehdinsight.net. В ответ на запрос проверки подлинности toohello кластер, использующий имя администратора hello (администратор) и пароль, который используется при создании кластера hello.

2. Hello слева от оператора hello Ambari web пользовательского интерфейса, выберите **HDFS** , а затем выберите hello **Configs** tab в середине hello страницы приветствия.

3. Выберите hello **Дополнительно** вкладку, а затем найдите hello **сайта основные настраиваемый** раздела.

4. Разверните hello **сайта основные настраиваемый** раздела, а затем toohello конец прокрутки и выберите hello **добавить свойство...**  ссылку. Используйте hello следующие значения для hello **ключ** и **значение** поля:

   * **Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net
   * **Значение**: hello SAS, возвращенных hello приложение C# или Python, выполненных ранее

     Замените **CONTAINERNAME** в имени контейнера hello вместе с hello приложение C# или SAS. Замените **STORAGEACCOUNTNAME** вы использовали имя учетной записи хранилища hello.

5. Нажмите кнопку hello **добавить** toosave этот ключ и значение, а затем щелкните hello **Сохранить** кнопку изменения конфигурации toosave hello. При появлении запроса добавьте описание изменения hello («Добавление доступа к хранилищу SAS» например) и нажмите кнопку **Сохранить**.

    Нажмите кнопку **ОК** после завершения изменений hello.

   > [!IMPORTANT]
   > Перед hello изменения вступят в силу, необходимо перезапустить несколько служб.

6. В веб-Ambari hello пользовательского интерфейса, выберите **HDFS** из списка hello hello слева, а затем выберите **перезапустите все** из hello **действий службы** раскрывающемся списке в правом hello. При появлении запроса выберите **Turn on maintenance mode** (Включить режим обслуживания) и щелкните "Conform Restart All" (Подтвердить перезапуск).

    Повторите эту процедуру для MapReduce2 и YARN.

7. После перезапуска службы hello выделить каждую таблицу и отключать режим обслуживания из hello **действий службы** раскрывающийся список.

## <a name="test-restricted-access"></a>Тестирование ограниченного доступа

tooverify, ограничен доступ hello используйте следующие методы:

* Для **на основе Windows** кластеров HDInsight использование удаленного рабочего стола tooconnect toohello кластера. Дополнительные сведения см. в разделе [подключиться с помощью протокола удаленного рабочего СТОЛА tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

    После подключения использовать hello **командной строки Hadoop** значок рабочего стола tooopen hello командную строку.

* Для **под управлением Linux** кластеров HDInsight использование SSH tooconnect toohello кластера. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

После подключения toohello кластера, используйте следующие шаги tooverify можно только чтение и список элементов в учетной записи хранения SAS hello hello:

1. содержимое hello toolist hello контейнера, используйте следующую команду из строки hello hello: 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    Замените **SASCONTAINER** с именем hello hello контейнера, созданные для учетной записи хранения SAS hello. Замените **SASACCOUNTNAME** с именем hello hello учетной записи хранения для hello SAS.

    Список Hello включает файл hello, отправленный при создании hello контейнера и SAS.

2. Используйте следующие команды tooverify, вы можете узнать hello содержимое файла hello hello. Замените hello **SASCONTAINER** и **SASACCOUNTNAME** как в предыдущем шаге hello. Замените **FILENAME** с именем hello файла hello, отображенный в предыдущей команде hello:

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    Эта команда перечисляет hello содержимое файла hello.

3. Используйте hello следующая команда toodownload hello файл toohello локальной файловой системы:

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    Эта команда загрузки hello tooa локальный файл с именем **testfile.txt**.

4. Используйте hello следующая команда tooupload hello локальный файл tooa новый файл с именем **testupload.txt** на hello хранилище SAS:

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    Появится toohello аналогичные сообщения после текста:

        put: java.io.IOException

    Эта ошибка возникает, так как место хранения hello чтения + только список. Используйте следующие команды tooput hello данные в хранилище по умолчанию hello hello кластер, который доступен для записи hello.

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    На этот раз hello операция должна завершиться успешно.

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="a-task-was-canceled"></a>Задача была отменена

**Симптомы**: при создании кластера с помощью сценария PowerShell hello, может появиться сообщение об ошибке после hello:

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

**Причина**: Эта ошибка может возникать, если использовать пароль для пользователя admin/HTTP hello для кластера hello, или (для кластеров под управлением Linux) hello пользователя SSH.

**Разрешение**: использовать пароль, отвечающий hello следующие условия:

* содержит не меньше 10 символов;
* содержит хотя бы одну цифру;
* содержит хотя бы один специальный символ;
* содержит хотя бы одну букву в верхнем или нижнем регистре.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как tooyour tooadd ограниченным доступом хранилища кластера HDInsight, узнайте toowork другие способы, с данными в кластере:

* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с HDInsight](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
