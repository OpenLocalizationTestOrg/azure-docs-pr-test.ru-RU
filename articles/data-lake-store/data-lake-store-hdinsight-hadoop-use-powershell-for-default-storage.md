---
title: "aaaCreate HDInsight кластер хранилища Озера данных хранения по умолчанию с помощью PowerShell | Документы Microsoft"
description: "Использовать toocreate Azure PowerShell и использовать кластеров HDInsight в хранилище Озера данных Azure"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>Создание кластеров HDInsight, использующих Data Lake Store, с помощью PowerShell
> [!div class="op_single_selector"]
> * [Использовать hello портал Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Использование PowerShell (для хранилища по умолчанию)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Использование PowerShell (для дополнительного хранилища)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Использование Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

Узнайте, как кластеры tooconfigure toouse Azure PowerShell Azure HDInsight с хранилища Озера данных Azure, как хранилище по умолчанию. Инструкции по созданию кластера HDInsight, использующего Data Lake Store в качестве дополнительного хранилища, см. в статье [Создание кластера HDInsight с Data Lake Store (как дополнительное хранилище) с помощью Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell.md).

Ниже приведены некоторые важные сведения об использовании HDInsight с Data Lake Store.

* кластеры HDInsight toocreate параметр Hello с доступом хранилища Озера tooData хранения по умолчанию доступна для HDInsight версии 3.5 и 3.6.

* кластеры HDInsight с toocreate параметр Hello получить доступ к хранилищу Озера tooData как хранилищем по умолчанию *недоступно* для кластеров HDInsight Premium.

tooconfigure toowork HDInsight в хранилище Озера данных с помощью PowerShell, следуйте инструкциям hello в разделах следующие пять hello.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, убедитесь, что выполнены следующие требования к hello:

* **Подписка Azure**: перейти слишком[получить бесплатная пробная версия](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 или более поздней**: в разделе [как tooinstall и настройте PowerShell](/powershell/azure/overview).
* **Пакет средств разработки программного обеспечения (SDK)**: tooinstall Windows SDK, перейдите в слишком[загружает и средств для Windows 10](https://dev.windows.com/en-us/downloads). Hello SDK — toocreate используется сертификат безопасности.
* **Субъекту-службе Azure Active Directory**: в данном учебнике как toocreate участника службы в Azure Active Directory (Azure AD). Однако toocreate участника службы, необходимо быть администратором Azure AD. Если вы являетесь администратором, можно пропустить это предварительное условие и продолжить работу с учебником hello.

    >[!NOTE]
    >Создать субъект-службу может только администратор Azure AD. Администратор Azure AD должен сначала создать субъект-службу, после чего вы сможете создать кластер HDInsight, использующий Data Lake Store. Hello участника-службы должны создаваться с помощью сертификата, как описано в [создании участника службы с сертификатом](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a>Создание учетной записи хранения озера данных
toocreate учетную запись хранилища Озера данных hello следующие:

1. С рабочего стола откройте окно PowerShell, а затем введите ниже фрагменты hello. Когда вы будете запрашиваемые toosign в знак в качестве одного из администраторов подписки hello или владельцы. 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > Если регистрация поставщика ресурсов хранилища Озера данных hello и получать сообщение об ошибке слишком`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, подписки не может быть входят для хранилища Озера данных. tooenable подписки Azure hello хранилища Озера данных общедоступной предварительной версии, следуйте инструкциям hello [Приступая к работе с хранилища Озера данных Azure с помощью портала Azure hello](data-lake-store-get-started-portal.md).
    >

2. Учетная запись Data Lake Store связывается с группой ресурсов Azure. Для начала создайте группу ресурсов.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Вы должны увидеть подобные выходные данные:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Создайте учетную запись Data Lake Store. Hello учетной записи, имя должно содержать только строчные буквы и цифры.

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

4. Использование хранилища Озера данных хранения по умолчанию требует вы toospecify корневой путь toowhich hello кластера файлы скопированы во время создания кластера. корневой путь, который является toocreate **/кластеры/hdiadlcluster** в фрагменте hello, используйте следующие командлеты hello:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Настройка проверки подлинности на основе ролей доступ к хранилищу Озера tooData
Каждая подписка Azure связана с сущностью Azure AD. Пользователей и служб, доступ к ресурсам подписки с помощью hello портал Azure или hello API диспетчера ресурсов Azure должны сначала пройти проверку подлинности в Azure AD. Доступ предоставляется tooAzure подписками и службами путем назначения им hello соответствующей роли на ресурс Azure. Для служб субъекта-службы идентифицирует службу hello в Azure AD.

В этом разделе показано, как службы toogrant приложения, такие как HDInsight, tooan доступ ресурсов Azure (hello ранее созданной учетной записи хранилища Озера данных). Осуществляется путем создания службы основного приложения hello и назначение ролей tooit через PowerShell.

tooset проверку подлинности Active Directory для Озера данных Azure, выполнять задачи hello в следующих двух разделах hello.

### <a name="create-a-self-signed-certificate"></a>Создание самозаверяющего сертификата
Убедитесь, что у вас есть [пакета Windows SDK](https://dev.windows.com/en-us/downloads) установлен перед продолжением hello шаги в этом разделе. Необходимо также создать каталог, например *C:\mycertdir*, в котором можно создать сертификат hello.

1. Из окна PowerShell hello, go toohello расположение, где установлен пакет SDK для Windows (как правило, *\Windows Kits\10\bin\x86 C:\Program Files (x86)*) и использовать hello [MakeCert] [ makecert] toocreate программа самозаверяющий сертификат и закрытый ключ. Используйте hello, следующие команды:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Появится запрос tooenter hello пароль для закрытого ключа. После успешного выполнения команды hello, вы увидите **CertFile.cer** и **mykey.pvk** в указанный каталог hello сертификата.
2. Используйте hello [Pvk2Pfx] [ pvk2pfx] .pvk hello tooconvert программы или CER-файлы, MakeCert созданный tooa PFX-файл. Выполните следующую команду hello.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Когда вам будет предложено ввести hello пароль закрытого ключа, указанный ранее. значение, указываемое для hello Hello **-po** параметр является hello пароль, связанный с hello PFX-файл. После успешного завершения команды hello, вы также увидите **CertFile.pfx** в указанный каталог hello сертификата.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Создание приложения Azure AD и субъекта-службы
В этом разделе Создание субъекта-службы для приложения Azure AD, назначение роли участника службы toohello и проверять подлинность как у участника-службы hello, предоставляя сертификат. toocreate hello, следующие команды запуска приложения в Azure AD:

1. Вставьте следующие командлеты в окне консоли PowerShell hello hello. Убедитесь, что это значение hello, укажите для hello **- DisplayName** свойство является уникальным. Здравствуйте, значения для **- Домашняя страница** и **- IdentiferUris** значения заполнителя, а не проверяются.

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
3. Предоставьте корневой папки хранилища Озера данных toohello hello службы доступа и папкам hello в hello корневой путь, указанный ранее. Используйте следующие командлеты hello.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>Создание кластера HDInsight Linux с хранилища Озера данных хранения по умолчанию hello

В этом разделе создается кластер HDInsight Hadoop Linux с хранилища Озера данных хранения по умолчанию hello. В этом выпуске hello кластер HDInsight и хранилище Озера данных должна находиться в hello местоположения.

1. Получить идентификатор клиента подписки hello и сохраните ее toouse позже.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Создание кластера HDInsight hello с помощью hello следующие командлеты:

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    После успешного завершения hello командлета вы увидите выход, содержащий сведения о кластере hello.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Запуск тестовых заданий в toouse кластера HDInsight hello хранилища Озера данных
После настройки кластера HDInsight можно запускать задания теста для его tooensure его доступность хранилища Озера данных. Таким образом, toodo запуска toocreate задания Hive образец таблицы, использующей hello образец данных, уже доступный в хранилище Озера данных  *<cluster root>/example/data/sample.log*.

В этом разделе в hello кластера hdinsight под Linux, созданного подключения Secure Shell (SSH) и запустите образец запроса Hive.

* Если вы используете Windows клиент toomake SSH-подключения в кластер hello, см. раздел [использование SSH с Linux-based Hadoop в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* При использовании toomake клиента Linux SSH-подключения в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight в Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

1. После внесения hello соединения, запустите hello Hive командной строки (CLI) с помощью hello следующую команду:

        hive
2. Следующие инструкции toocreate новую таблицу с именем tooenter hello используйте hello CLI **автомобилей** с помощью hello образец данных в хранилище Озера данных:

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Вы увидите выходные данные запроса hello hello SSH консоли.

    >[!NOTE]
    >Hello путь toohello образцов данных в hello предшествующий команда CREATE TABLE является `adl:///example/data/`, где `adl:///` корневой кластер hello. Следующий пример hello корневого кластера hello, указанный в этом учебнике, является команда hello `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. Можно использовать краткого варианта hello или предоставить корневого кластера toohello полный путь hello.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>Доступ к Data Lake Store с помощью команд HDFS
После настройки хранилища Озера данных toouse кластера HDInsight hello, можно использовать системы распределенных файла Hadoop (HDFS) оболочки команды tooaccess hello хранилища.

В этом разделе сделать SSH-подключения в hello кластера hdinsight под Linux, созданного и выполните команды HDFS hello.

* Если вы используете Windows клиент toomake SSH-подключения в кластер hello, см. раздел [использование SSH с Linux-based Hadoop в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* При использовании toomake клиента Linux SSH-подключения в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight в Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

После внесения hello подключения список файлов hello в хранилище Озера данных с помощью hello, следующая команда системы файла HDFS.

    hdfs dfs -ls adl:///

Можно также использовать hello `hdfs dfs -put` команды tooupload хранилища Озера tooData некоторые файлы, а затем используйте `hdfs dfs -ls` tooverify ли hello файлы были успешно отправлены.

## <a name="see-also"></a>См. также
* [Портал Azure: создайте toouse кластера HDInsight хранилища Озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
