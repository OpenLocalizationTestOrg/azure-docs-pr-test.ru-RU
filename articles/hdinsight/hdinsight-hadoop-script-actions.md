---
title: "Разработка действий с помощью HDInsight — Azure aaaScript | Документы Microsoft"
description: "Узнайте, как toocustomize Hadoop кластеры с действие сценария. Действие сценария можно дополнительное программное обеспечение используется tooinstall конфигурации Hadoop кластера или toochange hello приложений, установленных на кластер под управлением."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a>Разработка скриптов c действиями сценария для кластеров HDInsight под управлением Windows
Узнайте, как сценарии toowrite действия скрипта для HDInsight. Дополнительную информацию о скриптах с действиями сценария см. в статье [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster.md). Hello же статьи, написанные для кластеров HDInsight под управлением Linux. в разделе [сценариев разработки действий сценария для HDInsight](hdinsight-hadoop-script-actions-linux.md).



> [!IMPORTANT]
> Hello шагов в работают только этот документ для кластеров HDInsight под управлением Windows. Для версий ниже HDInsight 3.4 кластер HDInsight доступен только в Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement). Сведения об использовании действий скриптов в кластерах на платформе Linux см. в статье, посвященной [разработке действий скриптов с помощью HDInsight в Linux](hdinsight-hadoop-script-actions-linux.md).
>
>



Действие сценария можно дополнительное программное обеспечение используется tooinstall конфигурации Hadoop кластера или toochange hello приложений, установленных на кластер под управлением. Действия сценариев, сценарии, которые выполняются на узлах кластера hello при развертывании кластеров HDInsight и они выполняются после узлов в кластере hello завершить конфигурацию HDInsight. Действие сценария выполняется с правами учетной записи системного администратора и предоставляет права на полный доступ toohello узлов кластера. Могут быть предоставлены каждого кластера со списком toobe действия сценариев выполняются в порядке hello, в котором они указаны.

> [!NOTE]
> При появлении hello следующие сообщение об ошибке:
>
> System.Management.Automation.CommandNotFoundException; ExceptionMessage: hello термин «Сохранить HDIFile» не распознан как имя командлета, функции, файла скрипта или действующей программы hello. Проверьте правильность hello имени hello, или если был указан путь, убедитесь, что задан правильный путь, hello и повторите попытку.
> Это, поскольку не были включены hello вспомогательные методы.  См. раздел [Вспомогательные методы для пользовательских скриптов](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).
>
>

## <a name="sample-scripts"></a>Примеры сценариев
Для создания кластеров HDInsight в операционной системе Windows, hello действие сценария является скрипт Azure PowerShell. Hello следующий сценарий — пример по настройке файлов конфигурации hello сайта:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

сценарий Hello принимает четыре параметра, имя файла конфигурации hello hello свойство toomodify hello значение tooset, а также описание. Например:

    hive-site.xml hive.metastore.client.socket.timeout 90

Эти параметры задает too90 значение hive.metastore.client.socket.timeout hello hello hive-site.xml файла.  значение по умолчанию Hello составляет 60 секунд.

Этот пример сценария также доступен по ссылке [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).

HDInsight содержится несколько скриптов tooinstall дополнительные компоненты в кластерах HDInsight:

| Имя | Скрипт |
| --- | --- |
| **Установка Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. Ознакомьтесь со статьей [Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]. |
| **Установка R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. Ознакомьтесь со статьей [Установка и использование R на кластерах HDInsight Hadoop][hdinsight-r-scripts]. |
| **Установка Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. Ознакомьтесь со статьей [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md). |
| - **Установка Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. Ознакомьтесь со статьей [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md). |

Действие сценария могут быть восстановлены из hello портал Azure, Azure PowerShell или с помощью hello HDInsight .NET SDK.  Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария][hdinsight-cluster-customize].

> [!NOTE]
> Примеры сценариев Hello работать только с кластера HDInsight версии 3.1 или более поздней версии. Дополнительную информацию о версиях кластера HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight](hdinsight-component-versioning.md).
>
>

## <a name="helper-methods-for-custom-scripts"></a>Вспомогательные методы для пользовательских скриптов
Вспомогательные методы действий скриптов представляют собой служебные программы, которые можно использовать при создании пользовательских скриптов. Эти методы определяются в [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1)и могут быть включены в сценарии, используя следующий образец hello:

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

Ниже приведены hello вспомогательные методы, предоставляемые этим сценарием.

| Вспомогательный метод | Описание |
| --- | --- |
| **Save-HDIFile** |Загрузка файла с hello определенное место tooa универсальный код ресурса (URI) на локальном диске hello, связанного с кластером назначенного toohello узла виртуальной Машины Azure hello. |
| **Expand-HDIZippedFile** |Распаковывает ZIP-файл. |
| **Invoke-HDICmdScript** |Запускает сценарий из cmd.exe. |
| **Write-HDILog** |Записывать выходные данные из hello пользовательского скрипта для действия сценария. |
| **Get-Services** |Получите список служб, запущенных на компьютере hello, где hello скрипт будет выполнен. |
| **Get-Service** |Hello определенным именем службы в качестве входного, получить подробные сведения для конкретной службы (имя службы, обработки кода, состояние, т. д.) на компьютере hello, где выполняется сценарий hello. |
| **Get-HDIServices** |Получите список служб HDInsight, запущенного на компьютере hello, где выполняется сценарий hello. |
| **Get-HDIService** |Именем hello конкретных HDInsight службы как входные данные, получить подробные сведения для конкретной службы (имя службы, обработки кода, состояние, т. д.) на компьютере hello, где выполняется сценарий hello. |
| **Get-ServicesRunning** |Получите список служб, запущенных на компьютере hello где hello скрипт будет выполнен. |
| **Get-ServiceRunning** |Проверьте, если определенной службы (по имени) выполняется на компьютере hello где hello скрипт будет выполнен. |
| **Get-HDIServicesRunning** |Получите список служб HDInsight, запущенного на компьютере hello, где выполняется сценарий hello. |
| **Get-HDIServiceRunning** |Проверьте, если определенной службы HDInsight (по имени) выполняется на компьютере hello где hello скрипт будет выполнен. |
| **Get-HDIHadoopVersion** |Получите версию hello Hadoop на компьютере hello, где выполняется сценарий hello. |
| **Test-IsHDIHeadNode** |Проверьте, является ли hello компьютера, где выполняется сценарий hello головного узла. |
| **Test-IsActiveHDIHeadNode** |Проверьте, является ли hello компьютера, где выполняется сценарий hello активного головного узла. |
| **Test-IsHDIDataNode** |Проверьте, является ли hello компьютера, где выполняется сценарий hello узел данных. |
| **Edit-HDIConfigFile** |Измените файлы конфигурации hello hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml или yarn-site.xml. |

## <a name="best-practices-for-script-development"></a>Рекомендации по разработке скриптов
При разработке пользовательского скрипта для кластера HDInsight, существует несколько лучшие методики tookeep помнить:

* Проверка версии Hadoop hello

    Только в HDInsight версии 3.1 (Hadoop 2.4) и выше поддерживается использование пользовательских компонентов tooinstall действие сценария в кластере. В пользовательском скрипте, необходимо использовать hello **Get HDIHadoopVersion** версии вспомогательный метод toocheck hello Hadoop, перед тем как продолжить выполнение других задач в скрипте hello.
* Обеспечить стабильность связывает tooscript ресурсы

    Пользователям следует убедиться, все сценарии hello и другие артефакты, использовать в настройке hello кластера остаются доступными во время существования hello hello кластера и что hello версии этих файлов не изменяет время hello. Эти ресурсы необходимы, если требуется повторное создание образа hello узлов в кластере hello. Рекомендуется Hello является toodownload и архивировать все данные в учетной записи хранения, hello пользовательских элементов управления. Это может быть учетная запись хранения по умолчанию hello или любой hello дополнительных учетных записей хранения, указанного во время развертывания для кластера, настроенного для hello.
    В hello Spark и R настроена образцы кластера предоставляемых в документации hello, например, мы внесли локальную копию hello ресурсы этой учетной записи хранения: https://hdiconfigactions.blob.core.windows.net/.
* Убедитесь, что скрипт настройки кластера hello идемпотентными

    Следует ожидать, что за время существования кластера hello повторном создании hello узлы кластера HDInsight. скрипт настройки кластера Hello выполняется при каждом повторном создании кластера. Этот сценарий должны быть идемпотентными спроектированный toobe в смысле hello, при осуществлении, скрипт hello следует убедиться, что данный кластер hello возвращается toohello же настроить состояние, которое было сразу после hello скрипт был выполнен для hello первый раз, когда изначально был кластер hello создать. Например пользовательский сценарий установки приложения в D:\AppLocation на своего первого запуска, то при каждом последующем запуске при осуществлении, скрипт hello следует проверить, существует ли приложение hello в hello местоположение D:\AppLocation перед продолжением работы с другими в шагах hello скрипта.
* Установка пользовательских компонентов в оптимальное расположение hello

    При повторном создании кластера узлов диск ресурсов C:\ hello и системного диска D:\ может быть переформатированы, приведет к потере hello данных и приложений, которые были установлены на этих дисках. Это также может произойти, если узел виртуальной машины (VM) Azure, являющийся частью кластера hello выходит из строя и заменяется на новый узел. Компоненты можно установить на диск D:\ hello или в месте C:\apps hello в кластере hello. Все расположения на диске C:\ hello зарезервированы. Укажите hello места, где приложений или библиотек toobe, установленные в скрипт настройки кластера hello.
* Обеспечить высокий уровень доступности кластера архитектура hello

    HDInsight имеет активный / пассивный архитектуру для обеспечения высокой доступности, в какие один головной узел находится в активном режиме (где запущены службы HDInsight hello) и другие hello головной узел находится в режиме ожидания (в которой HDInsight не запущены службы). Hello узлов переключить активных и пассивных Если прерываются службы HDInsight. Если действие сценария используется tooinstall на оба головного узла высокий уровень доступности служб, обратите внимание, что этот механизм отработки отказа HDInsight hello не может tooautomatically сбой по эти службы, устанавливаемые пользователем. Таким образом пользователь установил службы на HDInsight головного узла, ожидаемый toobe высокой доступности необходимо иметь собственный механизм отработки отказа в режиме "активный пассивный" или находиться в режиме активный активный.

    Действие HDInsight сценария команды выполняются на оба головного узла роли hello головной узел указан как значение в hello *ClusterRoleCollection* параметра. Поэтому при разработке пользовательского скрипта убедитесь, что в скрипте учтены эти особенности установки. Не следует запускать возникают проблемы, где hello и теми же службами установлена и запущена на обоих hello головного узла, и они в конечном итоге конкурируют друг с другом. Также следует помнить, что данные теряются при осуществлении, поэтому программное обеспечение, установленное с помощью сценария действия имеет toobe устойчивым toosuch событий. Приложения должны быть спроектированный toowork с высокой доступности данных, который распределяется на множество узлов. Обратите внимание, что как 1/5 hello узлов в кластере можно повторно создать образ на hello то же время.
* Настройка хранилища больших двоичных объектов Azure toouse пользовательские компоненты hello

    Возможно, Hello пользовательских компонентов, установленных на узлах кластера hello toouse конфигурации по умолчанию хранилище системы распределенных файла Hadoop (HDFS). Вместо этого следует изменить toouse hello конфигурации хранилища больших двоичных объектов Azure. На повторное создание образа кластера возвращает в формате файловой системы HDFS hello и будут потеряны все данные, хранящиеся в ней. В случае использования хранилища BLOB-объектов Azure эти данные сохраняются.

## <a name="common-usage-patterns"></a>Общие варианты использования
В этом разделе приводятся рекомендации по реализации некоторых hello распространенных шаблонов использования, вы можете столкнуться при написании пользовательского скрипта.

### <a name="configure-environment-variables"></a>Настройка переменных среды
Часто в действие разработки сценариев, вы считаете, что необходимые переменные среды tooset hello. Например наиболее вероятный сценарий при загрузить двоичный файл внешнего узла, установите его на кластере hello и добавить к расположению hello там, где это переменной среды «PATH» установленных tooyour. Hello, следующий фрагмент кода показывает, как переменные среды tooset в hello пользовательского скрипта.

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

Эта инструкция задает переменную среды hello **MDS_RUNNER_CUSTOM_CLUSTER** toohello значение «true», а также задает hello области этой переменной toobe компьютера. В некоторых случаях важно, переменные среды задаются в соответствующей области hello — компьютера или пользователя. Дополнительные сведения о настройке переменных среды см. [здесь][1].

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Доступ к toolocations, где хранятся пользовательские сценарии hello
Скрипты, используемые toocustomize tooeither потребностей кластера находиться в учетной записи хранения по умолчанию hello для кластера hello или в открытый контейнер только для чтения в любой другой учетной записи хранилища. Если сценарий получает доступ к ресурсам, расположенным в другом месте их необходимы toobe в общедоступном (по крайней мере открытый только для чтения). Для экземпляра может tooaccess файл и сохраните его при помощи команды hello SaveFile HDI.

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

В этом примере необходимо убедиться, что этот контейнер hello «somecontainer» в учетной записи хранения «somestorageaccount» является общедоступным. В противном случае hello сценарий создает исключение «Не найдено» и сбой.

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a>Передайте в командлет Add-AzureRmHDInsightScriptAction toohello параметров
toopass командлета toohello AzureRmHDInsightScriptAction добавить несколько параметров, необходимо tooformat hello строковое значение toocontain все параметры для скрипта hello. Например:

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

или

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a>Вызов исключения при сбое развертывания кластера
Если вы хотите tooget точно уведомление факта hello настройки кластера не выполнена должным образом, а является важным toothrow исключение и сбой создания кластера hello. Для экземпляра может потребоваться tooprocess файл, если он существует и обрабатывать такие ошибки hello, где hello файл не существует. Благодаря что завершал скрипт hello и состояние hello hello кластера правильно известно. Hello следующий фрагмент кода приведен пример того, как tooachieve это:

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

В этом фрагменте кода если hello файл не существовал, он приведет tooa состоянии, которое hello скрипт фактически завершал после печати hello сообщение hello кластера достигает рабочее состояние, при условии, что он «успешно» завершения процесса настройки кластера. Если вы хотите toobe точно уведомление факта hello настройки кластера по сути не выполнена должным образом из-за отсутствующего файла, он является более подходящим toothrow исключение и не шаг настройки кластера hello. tooachieve это необходимо использовать вместо этого следующий фрагмент кода hello.

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a>Контрольный список для развертывания действия сценария
Ниже приведены шаги hello, который мы воспользовались при подготовке toodeploy эти скрипты.

1. Поместите файлы hello, содержащие пользовательские скрипты hello в месте, доступном из узлов кластера hello во время развертывания. Это может быть любым по умолчанию hello или дополнительные учетные записи хранения, указанного во время hello развертывания кластера или любой другой контейнер хранилища общего доступа.
2. Добавьте проверку в сценарии toomake убедиться, что они выполняются идемпотентной, так, чтобы hello сценарий может выполняться несколько раз для hello того же узла.
3. Используйте hello **Write-Output** tooSTDOUT tooprint командлет Azure PowerShell, а также STDERR. Не используйте **Write-Host**.
4. Использовать папку временного файла, например $env: TEMP, tookeep hello загруженный файл, используемый в сценарии hello и затем удалить их после выполнения скриптов.
5. Устанавливайте пользовательское программное обеспечения только на диске D:\ или в папке C:\apps. Не следует использовать другие расположения на диске c: hello, как они зарезервированы. Обратите внимание, что установки файлов на диске C: hello вне папки C:\apps hello может привести к сбою установки во время reimages hello узла.
6. В событии hello измененные настройки на уровне операционной системы или файлы конфигурации службы Hadoop вы можете toorestart службы HDInsight, чтобы они не может взять все параметры уровня ОС, например hello переменные среды, заданные в скриптах hello.

## <a name="debug-custom-scripts"></a>Отладка пользовательских сценариев
журналы ошибок сценария Hello хранятся вместе с другие выходные данные в учетной записи хранения hello по умолчанию, указанное для hello кластера при его создании. Hello журналы хранятся в таблице с именем hello *u < \cluster-name-fragment >< \time-stamp > setuplog*. Это статистическое журналы, которые имеют записи из всех узлов hello (головного узла и узлов рабочих ролей), на какие hello скрипт выполняется в кластере hello.
Легко toocheck hello журналов — toouse, средства HDInsight для Visual Studio. Установка средства hello описана в разделе [приступить к работе со средствами Visual Studio Hadoop для HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)

**toocheck hello журнала с помощью Visual Studio**

1. Откройте Visual Studio.
2. Последовательно щелкните **Представление** и **Обозреватель сервера**.
3. Щелкните правой кнопкой мыши «Azure», щелкните "Подключить" слишком**подписки Microsoft Azure**, а затем введите учетные данные.
4. Разверните **хранения**разверните hello учетной записи хранилища Azure используется в качестве файловой системы по умолчанию hello, разверните **таблиц**, а затем дважды щелкните имя таблицы hello.

Можно также удаленный в toosee узлы кластера hello STDOUT и STDERR для пользовательских сценариев. Hello журналы на каждом узле конкретный единственный узел toothat и записываются в **C:\HDInsightLogs\DeploymentAgent.log**. Эти файлы журналов записываются все выходные данные пользовательского скрипта hello. Фрагмент журнала для действия сценария Spark выглядит следующим образом:

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


В этом журнале было ясно, что действие сценария Spark hello был выполнен на Виртуальную машину с именем HEADNODE0 hello и что не были исключения во время выполнения hello.

В событии hello, происходит сбой при выполнении hello выходные данные, описывающие его также содержится в этом файле журнала. Hello сведения, представленные в этих журналах могут помочь при отладке скрипта, которые могут возникнуть.

## <a name="see-also"></a>См. также
* [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария][hdinsight-cluster-customize]
* [Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]
* [Установка и использование R на кластерах HDInsight Hadoop][hdinsight-r-scripts]
* [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md).
* [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
