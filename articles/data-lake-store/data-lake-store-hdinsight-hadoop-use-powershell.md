---
Заголовок: aaa "PowerShell: кластера Azure HDInsight с помощью хранилища Озера данных в виде дополнительное хранилище | Документы Microsoft» служб:-хранилищу Озера данных — hdinsight documentationcenter: '' Автор: диспетчер nitinme: jhubbard редактор: cgronlun

MS.AssetId: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: ms.devlang хранилища Озера данных: н/д ms.topic: статья ms.tgt_pltfrm: ms.workload н/д: ms.date большие наборы данных: ms.author 06/08/2017 г.: nitinme

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>Использовать Azure PowerShell toocreate кластер HDInsight с хранилища Озера данных (в качестве дополнительного хранилища)
> [!div class="op_single_selector"]
> * [Использование портала](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Использование PowerShell (для хранилища по умолчанию)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Использование PowerShell (для дополнительного хранилища)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Использование Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Узнайте, как tooconfigure toouse Azure PowerShell HDInsight кластер с хранилища Озера данных Azure, **как дополнительное хранилище**. Инструкции как toocreate HDInsight кластер с хранилища Озера данных Azure, как хранилище по умолчанию см. в разделе [создать кластер HDInsight с помощью хранилища Озера данных в качестве хранилища по умолчанию](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).

> [!NOTE]
> Если вы собираетесь хранилища Озера данных Azure toouse как дополнительное хранилище для кластера HDInsight, настоятельно рекомендуется это сделать, при создании кластера hello, как описано в этой статье. Добавление хранилища Озера данных Azure в качестве дополнительного хранилища tooan существующий кластер HDInsight является сложным процессом и ошибкам tooerrors.
>

В поддерживаемых типах кластеров Data Lake Store можно использовать в качестве хранилища по умолчанию или дополнительной учетной записи хранения. При использовании хранилища Озера данных как дополнительное хранилище hello учетной записи хранения по умолчанию для кластеров hello по-прежнему будут хранилища больших двоичных объектов Azure (WASB) и hello кластера файлов (например, журналы, т. д.) по-прежнему записываются toohello хранилища по умолчанию, при hello данных, которые необходимо tooprocess могут храниться в учетной записи хранилища Озера данных. С помощью хранилища Озера данных от имени учетной записи дополнительное хранилище не влияет на производительность и работу хранилища toohello hello возможность tooread и записи из кластера hello.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Использование Data Lake Store в качестве хранилища кластера HDInsight

Ниже приведены некоторые важные сведения об использовании HDInsight с Data Lake Store.

* Кластеры HDInsight toocreate параметр с доступом хранилища Озера tooData как дополнительное хранилище доступно для HDInsight версии 3.2, 3.4, 3.5 и 3.6.

Настройка HDInsight toowork с хранилища Озера данных с помощью PowerShell включает следующие шаги hello.

* Создание хранилища озера данных Azure
* Настройка проверки подлинности на основе ролей доступ к хранилищу Озера tooData
* Создание кластера HDInsight с хранилища Озера tooData проверки подлинности
* Запустите задание тестов на кластере hello

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь следующие hello.

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 или более поздней версии**. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
* **Пакет SDK Windows**. Его можно установить [отсюда](https://dev.windows.com/en-us/downloads). Использовать этот toocreate сертификат безопасности.
* **Субъект-служба Azure Active Directory**. В этом учебнике приведены инструкции о том, как toocreate участника службы в Azure AD. Тем не менее необходимо быть toocreate toobe может субъекта-службы администрирования Azure AD. Если вы являетесь администратором Azure AD, можно пропустить это предварительное условие и продолжить работу с учебником hello.

    **Если вы не являетесь администратором Azure AD**, не будет возможности tooperform hello действия требуется toocreate участника службы. В этом случае администратор Azure AD должен сначала создать субъект-службу, после чего вы сможете создать кластер HDInsight с Data Lake Store. Кроме того, hello участника-службы должны создаваться с помощью сертификата, как описано в разделе [создании участника службы с сертификатом](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-azure-data-lake-store"></a>Создание хранилища озера данных Azure
Выполните эти шаги toocreate хранилища Озера данных.

1. С рабочего стола откройте новое окно Azure PowerShell и введите следующий фрагмент кода hello. Когда запрос toolog, убедитесь, что войти в систему один администратор или владелец подписки hello:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > Если появится сообщение об ошибке слишком`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` при регистрации поставщика ресурсов хранилища Озера данных hello, это возможно, что ваша подписка не входят для хранилища Озера данных Azure. Убедитесь, что подписка Azure для общедоступной предварительной версии Data Lake Store включена, выполнив указанные [инструкции](data-lake-store-get-started-portal.md).
   >
   >
2. Учетная запись хранения озера данных Azure связывается с группой ресурсов Azure. Для начала создайте группу ресурсов Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Вы должны увидеть подобные выходные данные:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Создайте учетную запись хранения озера данных Azure. Hello учетная запись, что имя должно содержать только строчные буквы и цифры.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    Вы должны увидеть результаты hello следующим образом:

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. Отправьте некоторые образец данных tooAzure Озера данных. Мы будем использовать далее в этой статье tooverify, что hello данных доступен с кластера HDInsight. Если вы ищете некоторые tooupload образец данных, вы можете получить hello **скорая помощь данных** папку из hello [репозитории Озера данных Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Настройка проверки подлинности на основе ролей доступ к хранилищу Озера tooData
Каждая подписка Azure связана со службой Azure Active Directory. Пользователей и служб, которые обращаются к ресурсам hello подписки с помощью hello классический портал Azure или API диспетчера ресурсов Azure должны сначала пройти проверку подлинности с помощью Azure Active Directory. Доступ предоставляется tooAzure подписками и службами путем назначения им hello соответствующей роли на ресурс Azure.  Для служб субъекта-службы идентифицирует службу hello в hello Azure Active Directory (AAD). В этом разделе показано, как службы toogrant приложения, как HDInsight tooan доступа ресурсов Azure (hello созданную ранее учетную запись хранилища Озера данных Azure) путем создания участника службы для приложения hello и назначение ролей toothat через Azure PowerShell.

tooset проверку подлинности Active Directory для Озера данных Azure, необходимо выполнить следующие задачи hello.

* Создание самозаверяющего сертификата
* создать приложение в Azure Active Directory и субъект-службу.

### <a name="create-a-self-signed-certificate"></a>Создание самозаверяющего сертификата
Убедитесь, что у вас есть [пакета Windows SDK](https://dev.windows.com/en-us/downloads) установлен перед продолжением hello шаги в этом разделе. Необходимо также создать каталог, например **C:\mycertdir**, где будет создан сертификат hello.

1. В окне PowerShell hello перейдите toohello расположение, где установлен пакет SDK для Windows (как правило, `C:\Program Files (x86)\Windows Kits\10\bin\x86` и использовать hello [MakeCert] [ makecert] toocreate программа самозаверяющий сертификат и закрытый ключ. Используйте следующие команды hello.

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Появится запрос tooenter hello пароль для закрытого ключа. После hello команда выполнена успешно, вы увидите **CertFile.cer** и **mykey.pvk** в указанный каталог сертификат hello.
2. Используйте hello [Pvk2Pfx] [ pvk2pfx] .pvk hello tooconvert программы или CER-файлы, MakeCert созданный tooa PFX-файл. Выполните следующую команду hello.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    При появлении запроса введите hello пароль закрытого ключа, указанной вами ранее. значение, указываемое для hello Hello **-po** параметр является hello пароль, связанный с hello PFX-файл. После успешного завершения команды hello вы также увидите CertFile.pfx в каталог hello сертификата.

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>Создание приложения в Azure Active Directory и субъекта-службы
В этом разделе выполните шаги hello toocreate участника службы для приложения Azure Active Directory, назначение роли участника службы toohello и проверять подлинность как у участника-службы hello, предоставляя сертификат. Запустите следующие команды toocreate hello приложения в Azure Active Directory.

1. Вставьте следующие командлеты в окне консоли PowerShell hello hello. Убедитесь, что значение hello укажите для hello **- DisplayName** свойство является уникальным. Кроме того, hello значения для **- Домашняя страница** и **- IdentiferUris** значения заполнителя, а не проверяются.

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. Создание участника службы с помощью идентификатора приложения hello.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Предоставьте hello службы доступа toohello хранилища Озера данных папки и файла hello, вы получите доступ к кластеру HDInsight hello. в приведенном ниже фрагменте Hello предоставляет доступ toohello корень hello хранилища Озера данных учетной записи (который вы скопировали hello образец файла данных) и сам файл hello.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>Создание кластера HDInsight на платформе Linux с Data Lake Store в качестве дополнительного хранилища

В этом разделе показано, как создать кластер HDInsight Hadoop на платформе Linux с Data Lake Store в качестве дополнительного хранилища. В этом выпуске кластера HDInsight hello и hello хранилища Озера данных должны находиться в hello местоположения.

1. Начать с получения идентификатора hello подписки клиента. Позже он вам понадобится.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. Для этого выпуска кластер Hadoop, хранилище Озера данных может использоваться только как дополнительное хранилище для кластера hello. хранилище по умолчанию Hello по-прежнему будут hello Azure хранилища больших двоичных объектов (WASB). Таким образом сначала создадим hello учетной записи и хранилища контейнеров хранилища для кластера hello.

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. Создание кластера HDInsight hello. Используйте следующие командлеты hello.

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    После успешного завершения командлет hello должны появиться сведения кластера hello списка выходных данных.


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Запуск тестовых заданий в hello HDInsight кластера toouse hello хранилища Озера данных
После настройки кластера HDInsight можно запускать тестовые задания на tootest кластера hello, hello HDInsight кластера можно получить доступ к хранилищу Озера данных. toodo таким образом, будет выполняться задание куста образец, создающий таблицу, используя данные образца hello, отправленный хранилища Озера данных более ранних tooyour.

В этом разделе будет SSH в HDInsight Linux кластер был создан и выполнения запроса Hive образец hello hello.

* При использовании клиента Windows tooSSH в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* При использовании tooSSH клиента Linux в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight в Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. После установления соединения, запустите hello Hive CLI с помощью hello следующую команду:

        hive
2. С помощью hello (CLI), введите следующие инструкции toocreate новую таблицу с именем hello **автомобилей** , используя данные образца hello hello хранилища Озера данных:

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    Вы должны увидеть следующие выходные данные как toohello.

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a>Доступ к хранилищу озера данных с помощью команд HDFS
После настройки хранилища Озера данных toouse кластера HDInsight hello hello HDFS оболочки команды tooaccess hello хранилища можно использовать.

В этом разделе будет SSH в HDInsight Linux кластер был создан и выполнения команд HDFS hello hello.

* При использовании клиента Windows tooSSH в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* При использовании tooSSH клиента Linux в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight в Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

После подключения, используйте следующие файлы hello toolist команды файловой системы HDFS в хранилище Озера данных hello hello.

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

Должен быть выведен список hello файл, отправленный хранилища Озера данных более ранних toohello.

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

Можно также использовать hello `hdfs dfs -put` команды tooupload toohello некоторые файлы хранилища Озера данных, а затем используйте `hdfs dfs -ls` tooverify ли hello файлы были успешно отправлены.

## <a name="see-also"></a>См. также
* [Портал: Создание toouse кластера HDInsight хранилища Озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
