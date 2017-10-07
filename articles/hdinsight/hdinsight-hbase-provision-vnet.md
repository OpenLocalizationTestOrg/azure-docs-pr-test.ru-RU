---
title: "aaaCreate HBase кластеров в виртуальной сети - Azure | Документы Microsoft"
description: "Приступите к работе с HBase в Azure HDInsight. Узнайте, как кластеров HDInsight HBase toocreate в виртуальной сети Azure."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>Создание кластеров HBase в HDInsight в виртуальной сети Azure
Узнайте, как toocreate Azure HDInsight HBase кластеров в [виртуальной сети Azure][1].

Благодаря интеграции виртуальной сети, HBase кластеров может быть развернутой toohello виртуальных сетевых как приложения таким образом, приложения могут взаимодействовать с HBase напрямую. Hello имеет следующие преимущества:

* Прямое подключение узлов toohello приложения hello web hello HBase кластера, который обеспечивает взаимодействие через HBase Java удаленной процедуры вызова API (RPC).
* повышение производительности без необходимости организации пропуска трафика через множество шлюзов и подсистемы балансировки нагрузки;
* Hello возможность tooprocess конфиденциальные сведения в более безопасном режиме без предоставления общедоступную конечную точку.

### <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* <seg>
  **Рабочая станция с Azure PowerShell**.</seg> Обратитесь к разделу [Установка и использование Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).

## <a name="create-hbase-cluster-into-virtual-network"></a>Создание кластера HBase в виртуальной сети
В этом разделе создать кластер HBase под управлением Linux с hello зависимых учетной записи хранилища Azure в виртуальной сети Azure с помощью [шаблона Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Для других методов создания кластера и см. в основные сведения о настройке hello, [HDInsight, создания кластеров](hdinsight-hadoop-provision-linux-clusters.md). Дополнительные сведения об использовании шаблона toocreate Hadoop кластеров в HDInsight, см. в разделе [кластеров создать Hadoop в HDInsight с помощью шаблонов диспетчера ресурсов Azure](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> Некоторые свойства жестко запрограммированы в шаблон hello. Например:
>
> * **Расположение**: восточный регион США 2.
> * **Версия кластера**: 3.5.
> * **Число рабочих узлов кластера**: 2.
> * **Учетная запись хранения по умолчанию**: уникальная строка
> * **Имя виртуальной сети**: &lt;имя_кластера>-vnet.
> * **Адресное пространство виртуальной сети**: 10.0.0.0/16.
> * **Имя подсети**: subnet1
> * **Диапазон адресов подсети**: 10.0.0.0/24.
>
> &lt;Имя кластера > заменяется именем кластера hello, указываемые при использовании шаблона hello.
>
>

1. Щелкните hello следующий шаблон hello tooopen изображения в hello портал Azure. Hello шаблон находится в [шаблоны быстрый запуск Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Из hello **развертывания пользовательского** колонке введите hello следующие свойства:

   * **Подписки**: выберите кластер HDInsight подписку Azure, используемую toocreate hello, hello зависимых учетной записи хранилища и hello виртуальной сети Azure.
   * **Группа ресурсов**.Щелкните **Создать** и укажите имя новой группы ресурсов.
   * **Расположение**: выберите расположение для группы ресурсов hello.
   * **Имя_кластера**: Введите имя для hello Hadoop кластера toobe создан.
   * **Имя входа и пароль кластера**: имя для входа по умолчанию hello **администратора**.
   * **SSH имя пользователя и пароль**: имя пользователя по умолчанию hello **sshuser**.  Это имя можно изменить.
   * **Я принимаю условия hello, указанных выше, toohello**: (флажок)
3. Щелкните **Приобрести**. Это занимает около toocreate около 20 минут кластера. После создания кластера hello hello кластера колонки в hello портала tooopen можно щелкнуть его.

После завершения учебника hello, может потребоваться toodelete hello кластера. В случае с HDInsight ваши данные хранятся в службе хранилища Azure, что позволяет безопасно удалить неиспользуемый кластер. Плата за кластеры HDInsight взимается, даже когда они не используются. Поскольку плата hello для кластера hello много раз больше, чем hello плата за хранилище, экономически выгодно toodelete кластеры, когда они не используются. Hello инструкции удаления кластера см. в разделе [кластеров управление Hadoop в HDInsight с помощью hello портал Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

Работа с на новый кластер HBase toobegin можно использовать процедуры hello в [приступить к работе с базой HBase на Hadoop в HDInsight](hdinsight-hbase-tutorial-get-started.md).

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>Подключите кластер HBase toohello, с помощью API-интерфейсов RPC Java HBase
1. Создавать инфраструктуру как услугу (IaaS) виртуальной машины в одной виртуальной сети Azure hello и hello одной подсети. Инструкции по созданию виртуальной машины IaaS см. в статье [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md). При следующие hello в данном пошаговом руководстве, необходимо использовать следующие значения для конфигурации сети hello hello:

   * **Виртуальная сеть**: &lt;имя_кластера>-vnet.
   * **Подсеть**: subnet1

   > [!IMPORTANT]
   > Замените &lt;имя кластера > с именем hello использовалась при создании кластера HDInsight hello в предыдущих шагах.
   >
   >

   При использовании этих значений hello виртуальная машина размещается в hello же виртуальной сети и подсети, что и кластер HDInsight hello. Эта конфигурация позволяет им toodirectly взаимодействовать друг с другом. Нет toocreate способом с пустым граничного узла кластера HDInsight. Hello граничного узла может быть кластера используется toomanage hello.  Подробные сведения см. в статье [Использование пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md).

2. При использовании tooHBase tooconnect приложения Java удаленно, необходимо использовать hello полное доменное имя (FQDN). toodetermine это, необходимо получить hello подключения DNS-суффикс hello HBase кластера. toodo, можно использовать один из следующих методов hello:

   * Используйте Web браузера toomake вызова Ambari:

     Обзор toohttps: / /&lt;Имя_кластера >.azurehdinsight.net/api/v1/clusters/&lt;Имя_кластера > / размещает? minimal_response = true. Он включает файл JSON со hello DNS-суффиксов.
   * Используйте веб-сайт Ambari hello:

     1. Обзор слишком https://&lt;Имя_кластера >. azurehdinsight.net.
     2. Нажмите кнопку **узлов** hello верхнем меню.
   * Используйте вызовы REST перелистывание toomake:

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     В hello вернул данные нотации объектов JavaScript (JSON), найдите запись «host_name» hello. Он содержит hello полное доменное имя для hello узлов в кластере hello. Например:

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     Hello часть hello доменных имен, начинающихся с имени кластера hello является hello DNS-суффикс. Например, mycluster.b1.cloudapp.net.
   * Использование Azure PowerShell

     Используйте hello, следуя hello tooregister скрипт Azure PowerShell **Get ClusterDetail** функции, которая может быть DNS-суффикс используется tooreturn hello:

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     После выполнения скрипта hello Azure PowerShell, используйте hello следующая команда tooreturn hello DNS-суффикс, используя hello **Get ClusterDetail** функции. При использовании этой команды укажите имя кластера HDInsight HBase, имя и пароль администратора.

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     Эта команда возвращает DNS-суффикс hello. Например, **yourclustername.b4.internal.cloudapp.net**.


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

tooverify, hello виртуальной машины могут взаимодействовать с hello кластер HBase, используйте команду hello `ping headnode0.<dns suffix>` hello виртуальной машины. Например, ping headnode0.mycluster.b1.cloudapp.net.

toouse эту информацию в приложении Java, можно выполнить действия hello в [Maven использовать toobuild Java приложений, использующих HBase с HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate приложения. приложение hello toohave подключения удаленного сервера HBase tooa, измените hello **hbase-site.xml** файл в этот примере toouse hello полное доменное имя для Zookeeper. Например:

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> Дополнительные сведения о разрешении имен в виртуальных сетях Azure включая то, как toouse собственного DNS-сервера в разделе [разрешения имен (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
>
>

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, каким образом toocreate кластер HBase. toolearn более, см.:

* [Приступая к работе с HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Использование пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md)
* [Настройка репликации HBase в HDInsight](hdinsight-hbase-replication.md)
* [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Приступая к работе с HBase с Hadoop в HDInsight](hdinsight-hbase-tutorial-get-started.md)
* [Анализ мнений пользователей Twitter с использованием HBase в HDInsight](hdinsight-hbase-analyze-twitter-sentiment.md)
* [Обзор виртуальной сети][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Подробности подготовить новый кластер HBase hello"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Используйте действие скрипта toocustomize кластер HBase"

[azure-preview-portal]: https://portal.azure.com
