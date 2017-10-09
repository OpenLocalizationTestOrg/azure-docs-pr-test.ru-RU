---
title: "toocreate aaaUse шаблоны Azure HDInsight и хранилище Озера данных | Документы Microsoft"
description: "Использовать toocreate шаблонов диспетчера ресурсов Azure и использовать кластеров HDInsight в хранилище Озера данных Azure"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a>Создание кластера HDInsight с Data Lake Store с помощью шаблона Azure Resource Manager
> [!div class="op_single_selector"]
> * [Использование портала](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Использование PowerShell (для хранилища по умолчанию)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Использование PowerShell (для дополнительного хранилища)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Использование Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Узнайте, как tooconfigure toouse Azure PowerShell HDInsight кластер с хранилища Озера данных Azure, **как дополнительное хранилище**.

В поддерживаемых типах кластеров Data Lake Store можно использовать в качестве хранилища по умолчанию или дополнительной учетной записи хранения. При использовании хранилища Озера данных как дополнительное хранилище hello учетной записи хранения по умолчанию для кластеров hello по-прежнему будут хранилища больших двоичных объектов Azure (WASB) и hello кластера файлов (например, журналы, т. д.) по-прежнему записываются toohello хранилища по умолчанию, при hello данных, которые необходимо tooprocess могут храниться в учетной записи хранилища Озера данных. С помощью хранилища Озера данных от имени учетной записи дополнительное хранилище не влияет на производительность и работу хранилища toohello hello возможность tooread и записи из кластера hello.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Использование Data Lake Store в качестве хранилища кластера HDInsight

Ниже приведены некоторые важные сведения об использовании HDInsight с Data Lake Store.

* Кластеры HDInsight toocreate параметр с доступом хранилища Озера tooData хранения по умолчанию доступна для HDInsight версии 3.5 и 3.6.

* Кластеры HDInsight toocreate параметр с доступом хранилища Озера tooData как дополнительное хранилище доступно для HDInsight версии 3.2, 3.4, 3.5 и 3.6.

В этой статье мы подготовим кластер Hadoop, в котором хранилище озера данных будет дополнительным хранилищем. Инструкции как toocreate Hadoop кластер с хранилища Озера данных в качестве хранилища по умолчанию см. в разделе [создать кластер HDInsight в хранилище Озера данных с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь следующие hello.

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 или более поздней версии**. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
* **Субъект-служба Azure Active Directory**. В этом учебнике приведены инструкции о том, как toocreate участника службы в Azure AD. Тем не менее необходимо быть toocreate toobe может субъекта-службы администрирования Azure AD. Если вы являетесь администратором Azure AD, можно пропустить это предварительное условие и продолжить работу с учебником hello.

    **Если вы не являетесь администратором Azure AD**, не будет возможности tooperform hello действия требуется toocreate участника службы. В этом случае администратор Azure AD должен сначала создать субъект-службу, после чего вы сможете создать кластер HDInsight с Data Lake Store. Кроме того, hello участника-службы должны создаваться с помощью сертификата, как описано в разделе [создании участника службы с сертификатом](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a>Создание кластера HDInsight с помощью Azure Data Lake Store
Hello шаблона диспетчера ресурсов и hello предварительные требования для использования шаблона hello, можно найти на github на сайте [развертывания кластера HDInsight Linux с помощью нового хранилища Озера данных](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage). Выполните hello инструкций, приведенных в этой связи toocreate кластер HDInsight с хранилища Озера данных Azure как дополнительное хранилище hello.

Hello инструкциям по ссылке hello вышеупомянутых требуются PowerShell. Прежде чем начать с этих инструкций, убедитесь, что вход tooyour учетная запись Azure. С рабочего стола откройте новое окно Azure PowerShell и введите следующие фрагменты кода hello. При toolog запрос, убедитесь, что войти в систему один hello admininistrators/владелец подписки:

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a>Отправка хранилища Озера данных Azure toohello образца данных
шаблон диспетчера ресурсов Hello создает новую учетную запись хранилища Озера данных и связывает его с кластером HDInsight hello. Теперь необходимо отправить некоторые toohello данных образец хранилища Озера данных. Вам потребуется позже в заданий учебника toorun hello из кластера HDInsight, доступа к данным в хранилище Озера данных hello эти данные. Дополнительные сведения о данных tooupload см. [отправить файл tooyour хранилища Озера данных](data-lake-store-get-started-portal.md#uploaddata). Если вы ищете некоторые tooupload образец данных, вы можете получить hello **скорая помощь данных** папку из hello [репозитории Озера данных Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).

## <a name="set-relevant-acls-on-hello-sample-data"></a>Установите соответствующие разрешения на hello образец данных
toomake убедиться, что данные образца hello, загруженными доступен с кластера HDInsight hello, необходимо убедиться, приложение hello Azure AD, удостоверения используемый tooestablish между кластером HDInsight hello и хранилище Озера данных имеет доступ toohello файла или папки, которые Этот tooaccess. toodo это, выполните следующие шаги hello.

1. Найти имя hello hello приложения Azure AD, которая связана с кластером HDInsight и hello хранилища Озера данных. Одним из способов toolook имени hello tooopen hello HDInsight кластера колонки, созданные с помощью шаблона диспетчера ресурсов hello, нажмите кнопку hello **удостоверение кластера AAD** и найдите значение hello **участника-службы Отображаемое имя**.
2. Теперь предоставляют доступ toothis приложения Azure AD в hello файл или папку, которые должны tooaccess из кластера HDInsight hello. право hello tooset списки управления доступом на hello файл или папку в хранилище Озера данных, см. [защиты данных в хранилище Озера данных](data-lake-store-secure-data.md#filepermissions).

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Запуск тестовых заданий в hello HDInsight кластера toouse hello хранилища Озера данных
После настройки кластера HDInsight можно запускать тестовые задания на tootest кластера hello, hello HDInsight кластера можно получить доступ к хранилищу Озера данных. toodo таким образом, будет выполняться задание куста образец, создающий таблицу, используя данные образца hello, отправленный хранилища Озера данных более ранних tooyour.

В этом разделе вы будете SSH в кластере HDInsight Linux и выполнения hello образец запроса Hive. Если вы работаете с клиентом Windows, рекомендуется использовать **PuTTY**, который можно скачать по адресу: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Дополнительные сведения об использовании PuTTY см. в разделе [Использование SSH с Hadoop на основе Linux в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

1. После установления соединения, запустите hello Hive CLI с помощью hello следующую команду:

   ```
   hive
   ```
2. С помощью hello (CLI), введите следующие инструкции toocreate новую таблицу с именем hello **автомобилей** , используя данные образца hello hello хранилища Озера данных:

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   Вы должны увидеть следующие выходные данные как toohello.

   ```
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
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a>Доступ к хранилищу озера данных с помощью команд HDFS
После настройки хранилища Озера данных toouse кластера HDInsight hello hello HDFS оболочки команды tooaccess hello хранилища можно использовать.

В этом разделе вы будете SSH в кластере HDInsight Linux и выполнения hello команды HDFS. Если вы работаете с клиентом Windows, рекомендуется использовать **PuTTY**, который можно скачать по адресу: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Дополнительные сведения об использовании PuTTY см. в разделе [Использование SSH с Hadoop на основе Linux в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

После подключения, используйте следующие файлы hello toolist команды файловой системы HDFS в хранилище Озера данных hello hello.

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

Должен быть выведен список hello файл, отправленный хранилища Озера данных более ранних toohello.

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

Можно также использовать hello `hdfs dfs -put` команды tooupload toohello некоторые файлы хранилища Озера данных, а затем используйте `hdfs dfs -ls` tooverify ли hello файлы были успешно отправлены.


## <a name="next-steps"></a>Дальнейшие действия
* [Копирование данных из хранилища Озера tooData больших двоичных объектов хранилища Azure](data-lake-store-copy-data-wasb-distcp.md)
