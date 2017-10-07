---
title: "кластеры HDInsight aaaCustomize с помощью действий скрипта - Azure | Документы Microsoft"
description: "Добавьте пользовательские компоненты кластеров на основе tooLinux HDInsight с помощью действий скрипта. Действия сценариев, Bash-скриптов, которые могут быть конфигурации кластера используется toocustomize hello или добавить дополнительные службы и служебные программы, например цветового тона, Solr или R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>Настройка кластеров HDInsight под управлением Linux с помощью действия сценария

HDInsight предоставляет параметр конфигурации **действие сценария** , вызывающий пользовательские скрипты, настроить кластер hello. Эти сценарии, используемые tooinstall дополнительные компоненты и изменения параметров конфигурации. Действия скрипта можно использовать во время или после создания кластера.

> [!IMPORTANT]
> действия сценариев toouse возможность Hello в кластере уже запущенному доступна только для кластеров HDInsight под управлением Linux.
>
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Действия скриптов также может быть опубликованным toohello Azure Marketplace как приложение HDInsight. Некоторые примеры hello в этом документе показывают, как можно установить приложения HDInsight с помощью команд-действий сценарий PowerShell и hello пакета SDK для .NET. Дополнительные сведения о приложениях HDInsight см. в разделе [HDInsight публикации приложения в Azure Marketplace hello](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>Разрешения

При использовании кластера HDInsight, присоединенных к домену, существует два Ambari разрешения, необходимые при использовании действия скриптов с кластером hello.

* **AMBARI. ЗАПУСТИТЕ\_НАСТРАИВАЕМЫЙ\_команда**: роль администратора Ambari hello имеет это разрешение по умолчанию.
* **КЛАСТЕР. ЗАПУСТИТЕ\_НАСТРАИВАЕМЫЙ\_команда**: оба Здравствуйте, администратор кластера HDInsight и администратор Ambari иметь это разрешение по умолчанию.

Дополнительные сведения о работе с разрешениями в присоединенном к домену кластере HDInsight см. в статье [Управление присоединенными к домену кластерами HDInsight (предварительная версия)](hdinsight-domain-joined-manage.md).

## <a name="access-control"></a>управление доступом;

Если вы не hello администратором или владельцем подписки Azure, ваша учетная запись должна быть хотя бы **участника** доступа toohello ресурсов группы, содержащей hello кластера HDInsight.

Кроме того при создании кластера HDInsight, имеющим по крайней мере **участника** toohello доступа к подписке Azure необходимо уже зарегистрированы hello поставщика для HDInsight. Регистрация поставщика происходит, когда пользователь с подпиской toohello доступа участника создает ресурс для hello первый раз на hello подписки. Регистрацию также можно выполнить без создания ресурса [с помощью REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).

Дополнительные сведения о работе с помощью управления доступом см. в разделе hello следующие документы:

* [Приступая к управлению доступом в hello портал Azure](../active-directory/role-based-access-control-what-is.md)
* [Использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>Что такое действия скриптов

Действие скрипта — это просто скрипт Bash, в который вы вводите универсальный код ресурса (URI) и для которого вы указываете параметры. Hello скрипт выполняется на узлах в кластере HDInsight hello. Hello ниже приведены характеристики и возможности выполнения сценариев.

* Должен быть сохранен в URI, который доступен с кластера HDInsight hello. Hello ниже приведены возможные хранилищах.

    * **Хранилища Озера данных Azure** учетной записи, доступном из кластера HDInsight hello. Дополнительные сведения об использовании Azure Data Lake Store с HDInsight см. в статье [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        При использовании сценария, сохраненного в хранилище Озера данных, является формат URI hello `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > tooaccess Hello службы основной HDInsight использует хранилище Озера данных должен иметь доступ на чтение toohello сценария.

    * Большой двоичный объект в **учетной записи хранилища Azure** , является либо учетной записи хранения основной или дополнительный hello для кластера HDInsight hello. Во время создания кластера HDInsight предоставляется доступ tooboth из этих типов учетных записей хранения.

    * Служба совместного доступа к файлам, например хранилище BLOB-объектов Azure, GitHub, OneDrive, Dropbox и т. д.

        Примеры URI, в разделе hello [скрипты действий примера сценария](#example-script-action-scripts) раздела.

        > [!WARNING]
        > HDInsight поддерживает только учетные записи хранения Azure __общего назначения__. Он не поддерживает hello __хранилище больших двоичных объектов__ тип учетной записи.

* Можно ограничить слишком**проведение только определенные типы узлов**, пример головного узла или узлов рабочих ролей.

  > [!NOTE]
  > При использовании с HDInsight Premium, можно задать, использование hello сценария на узле edge hello.

* Действия скрипта могут быть **сохраняемыми** или **специализированными**.

    **Сохранить** сценарии, примененные tooworker узлы добавлены toohello кластера после запуска сценария hello. Например, при масштабировании hello кластера.

    Сохраненный скрипт также может применять изменения tooanother узел типа, например головного узла.

  > [!IMPORTANT]
  > Действия сохраняемых скриптов должны иметь уникальные имена.

    **Специализированные** скрипты не сохраняются. Они не применяются tooworker узлы добавлены toohello кластера после hello сценарий был выполнен. Впоследствии можно распространить нерегламентированных сценариев tooa сохранить скрипт или понизить уровень скрипта нерегламентированных tooan сохраненный скрипт.

  > [!IMPORTANT]
  > Действия скриптов, используемые при создании кластера, автоматически сохраняются.
  >
  > Скрипты, в которых произошла ошибка, не сохраняются, даже если вы отдельно указали, что они должны быть сохранены.

* Может принимать **параметров** , используемых скриптом hello во время выполнения.
* Запустите с **корневой права доступа уровня** на узлах кластера hello.
* Можно использовать через hello **портал Azure**, **Azure PowerShell**, **Azure CLI**, или **HDInsight .NET SDK**

кластер Hello ведет журнал всех сценариев, которые уже были выполнены. Журнал Hello полезно при необходимости идентификатор hello toofind скрипта для операции повышения или понижения роли.

> [!IMPORTANT]
> Нет не tooundo автоматическим способом hello изменений, внесенных в действие сценария. Либо вручную отменить изменения hello, или укажите скрипт, который изменяет их.


### <a name="script-action-in-hello-cluster-creation-process"></a>Действие сценария в процессе создания кластера hello

Действия скриптов, используемые в процессе создания кластера и выполняющиеся в существующем кластере, несколько отличаются:

* скрипт Hello **автоматически сохраненные**.
* Объект **сбоя** в hello сценарий может привести к toofail процесса создания кластера hello.

Hello следующей схеме показана при выполнении сценария действия во время создания hello.

![Настройка кластера HDInsight и этапы создания кластера][img-hdi-cluster-states]

Hello скрипт выполняется при HDInsight настроена. На этом этапе hello сценарий выполняется параллельно на всех hello указанные узлы в кластере hello и запускается с правами корневой на узлах hello.

> [!NOTE]
> Поскольку hello скрипт выполняется на узлах кластера hello корневой уровень прав доступа, можно выполнять такие операции, как остановка и запуск служб, включая службы, связанные с Hadoop. При остановке службы, необходимо убедиться, что служба Ambari hello и других служб, связанных с Hadoop доступны и запущены перед hello сценарий завершает работу. Эти службы необходимы toosuccessfully определить работоспособность hello и состояние кластера hello во время создания.


При создании кластера можно использовать несколько действий скриптов одновременно. Эти сценарии вызываются в порядке hello, в котором они указаны.

> [!IMPORTANT]
> Действия сценария должны быть завершены в течение 60 минут. В противном случае возникнет ошибка времени ожидания. Во время подготовки кластеров, hello скрипт выполняется параллельно с другими процессами, установки и настройки. Соперничество за ресурсы, такие как ЦП или в сети может вызвать скрипт hello tootake больше toofinish не так, как в среде разработки.
>
> toominimize hello время принимает toorun hello скрипт, избежать задач, таких как загрузка и компиляция приложения из источника. Предварительная компиляция приложения и хранения hello двоичного файла в хранилище Azure.


### <a name="script-action-on-a-running-cluster"></a>Действие скрипта в работающем кластере

В отличие от сценария, который используется во время создания кластера, ошибка в скрипте действия были выполнены на уже запущенному кластеру не вызывает автоматического состояние tooa сбой toochange hello кластера. По завершении сценария hello кластера должна возвращать tooa состояние «запущен».

> [!IMPORTANT]
> Даже если hello кластер находится в состоянии «работает», hello невыполненного сценария может нарушили вещей. Например сценарий удалось удалить файлы, необходимый hello кластера.
>
> Действия сценариев выполняются с правами корневой, поэтому необходимо понять назначение сценарий перед ее применением tooyour кластера.

При применении кластера tooa сценария, состояние кластера hello изменяется toofrom **под управлением** слишком**принято**, затем **конфигурацию HDInsight**опять слишком**Под управлением** для успешного скриптов. состояние скрипта Hello заносится в журнал действий скриптов hello и toodetermine этой информации можно использовать ли скрипт hello успешно или неудачно. Например, hello `Get-AzureRmHDInsightScriptActionHistory` командлет PowerShell может быть состояние hello используется tooview сценария. Она возвращает сведения аналогичные toohello следующий текст:

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Если вы изменили пароль пользователя (администратор) hello кластера после создания кластера hello, сценарий, который выполняли действия для этого кластера может завершиться ошибкой. При наличии каких-либо действий сохраненный скрипт рабочих узлов, целевой этих скриптов может возникать, если масштабирование hello кластера.

## <a name="example-script-action-scripts"></a>Пример действий сценария

Сценарий, сценарии, действие применяется с помощью hello следующие программы:

* Портал Azure
* Azure PowerShell
* Инфраструктура CLI Azure
* Пакет SDK для HDInsight .NET

HDInsight предоставляет следующие компоненты в кластерах HDInsight hello tooinstall сценариев:

| Имя | Скрипт |
| --- | --- |
| **Добавление учетной записи хранения Azure** |https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. В разделе [tooan HDInsight добавить дополнительное хранилище кластера](hdinsight-hadoop-add-storage.md). |
| **Установка Hue** |https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. См. статью [Установка и использование Hue на кластерах HDInsight Hadoop](hdinsight-hadoop-hue-linux.md). |
| **Установка Presto** |https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. См. статью [Установка и использование Presto в кластерах HDInsight](hdinsight-hadoop-install-presto.md). |
| **Установка Solr** |https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Ознакомьтесь со статьей [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md). |
| **Установка Giraph** |https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Ознакомьтесь со статьей [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md). |
| **Предварительная загрузка библиотек Hive** |https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. См статью [Добавление библиотек Hive в кластеры HDInsight](hdinsight-hadoop-add-hive-libraries.md). |
| **Установка или обновление Mono** | https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash См. статью [Установка или обновление Mono в HDInsight](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Использование действия скрипта при создании кластера

В этом разделе приведены примеры о различных способах hello действия скриптов можно использовать при создании кластера HDInsight.

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>Используйте действие скрипта, во время создания кластера из hello портал Azure

1. Начните создание кластера, как описано в разделе [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Остановить при достижении hello __Сводка кластера__ раздела.

2. Из hello __Сводка кластера__ раздел, выберите hello __изменить__ связей для __Дополнительные параметры__.

    ![Ссылка "Дополнительные параметры"](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. Из hello __Дополнительные параметры__ выберите __скрипт действия__. Из hello __скрипт действия__ выберите __+ new отправки__

    ![Отправка нового действия скрипта](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Используйте hello __выберите сценарий__ tooselect входа готового скрипта. toouse пользовательского скрипта, выберите __пользовательские__ и укажите hello __имя__ и __Bash универсальный код Ресурса скрипта__ для своего сценария.

    ![Добавить скрипт в виде выберите сценария hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Привет, в следующей таблице описываются элементы hello в форме hello.

    | Свойство | Значение |
    | --- | --- |
    | Выберите скрипт | toouse собственный сценарий, выберите __настраиваемый__. В противном случае выберите один из hello предоставляются скриптов. |
    | Имя |Укажите имя для действия сценария hello. |
    | URI bash-скрипта |Укажите сценарий toohello URI hello, вызванный toocustomize hello кластера. |
    | Головной, рабочий или Zookeeper |Укажите узлы hello (**Head**, **рабочих**, или **ZooKeeper**) на какие hello настройки выполнения скрипта. |
    | Параметры |Укажите параметры hello, если это требуется для сценария hello. |

    Используйте hello __сохранить этот скрипт__ tooensure входа, hello сценарий применяется во время операции масштабирования.

5. Выберите __создать__ toosave hello скрипта. Затем можно использовать __+ отправить новый__ tooadd другой сценарий.

    ![Несколько действий скриптов](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Закончив добавление сценариев использования hello __выберите__ кнопку, а затем hello __Далее__ toohello tooreturn кнопку __Сводка кластера__ раздела.

3. toocreate hello кластера, выберите __создать__ из hello __Сводка кластера__ выделения.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Использование действия сценария на основе шаблонов диспетчера ресурсов Azure

Hello в примерах этого раздела показано, как toouse сценария действий с помощью шаблонов диспетчера ресурсов Azure.

#### <a name="before-you-begin"></a>Перед началом работы

* Сведения о настройке рабочей станции toorun командлеты HDInsight Powershell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).
* Дополнительные сведения о toocreate шаблонов, см. раздел [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Сведения об использовании Azure PowerShell с Resource Manager см. в [этой статье](../azure-resource-manager/powershell-azure-resource-manager.md).

#### <a name="create-clusters-using-script-action"></a>Создание кластеров с помощью действия скрипта

1. Скопируйте hello следующий шаблон tooa расположение на компьютере. Этот шаблон устанавливает Giraph на hello headnodes и рабочих узлов в кластере hello. Можно также проверить допустимость шаблона JSON hello. Вставьте содержимое шаблона в [JSONLint](http://jsonlint.com/) — интерактивное средство проверки JSON.

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. Запуск Azure PowerShell и вход в tooyour учетная запись Azure. После предоставления учетных данных, hello команда возвращает сведения о вашей учетной записи.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Если у вас несколько подписок, укажите идентификатор подписки hello нужно toouse для развертывания.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > Можно использовать `Get-AzureRmSubscription` tooget список всех подписок, связанных с вашей учетной записи, включая идентификатор подписки hello для каждого из них.

4. Создайте группу ресурсов, если у вас нет существующей группы ресурсов. Укажите имя группы ресурсов hello и место, необходимое для решения hello. Возвращается Сводка hello новую группу ресурсов.

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. toocreate развертывания для группы ресурсов, запустите hello **New AzureRmResourceGroupDeployment** команду и укажите необходимые параметры hello. Параметры Hello hello следующие данные:

    * имя развертывания;
    * Hello имя группы ресурсов
    * созданный шаблон toohello URL-адрес или путь Hello.

  Если для вашего шаблона требуются какие-либо параметры, необходимо также передать их. В этом случае tooinstall действие hello сценария R в кластере hello параметры не требуются.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    Используется запрос tooprovide значения для параметров hello, определенные в шаблоне hello.

1. При развертывании группы ресурсов hello отображается сводка hello развертывания.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. Если сбой развертывания, можно использовать следующие командлеты tooget сведения о сбоях hello hello.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Использование действия скрипта при создании кластера с помощью Azure PowerShell

В этом разделе мы используем hello [AzureRmHDInsightScriptAction добавить](https://msdn.microsoft.com/library/mt603527.aspx) сценариев tooinvoke командлет с помощью toocustomize действие сценария кластера. Прежде чем продолжить, убедитесь, что вы установили и настроили Azure PowerShell. Сведения о настройке рабочей станции toorun командлеты HDInsight PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).

Hello следующий сценарий демонстрирует, каким образом tooapply действие скрипта, при создании кластера с помощью PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Он может занять несколько минут, перед созданием кластера hello.

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>Используйте действие скрипта, во время создания кластера из hello HDInsight .NET SDK

Hello HDInsight .NET SDK предоставляет клиентские библиотеки, делает его проще toowork с HDInsight из приложения .NET. Пример кода см. в разделе [под управлением Linux, создание кластеров HDInsight с помощью hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-tooa-running-cluster"></a>Применить действие сценария tooa под управлением кластера

В этом разделе рассказано, как tooapply скрипт действия tooa под управлением кластера.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>Применить действие сценария tooa под управлением кластера из hello портал Azure

1. Из hello [портал Azure](https://portal.azure.com), выберите кластер HDInsight.

2. Обзор кластера HDInsight hello, выберите hello **действия скрипта** плитки.

    ![Элемент "Действия сценариев"](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Можно также выбрать **все параметры** , а затем выберите **действия скрипта** из hello в разделе "Параметры".

3. С помощью hello hello раздел действия скрипта, выберите **отправить новый**.

    ![Добавить скрипт tooa под управлением кластера](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Используйте hello __выберите сценарий__ tooselect входа готового скрипта. toouse пользовательского скрипта, выберите __пользовательские__ и укажите hello __имя__ и __Bash универсальный код Ресурса скрипта__ для своего сценария.

    ![Добавить скрипт в виде выберите сценария hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Привет, в следующей таблице описываются элементы hello в форме hello.

    | Свойство | Значение |
    | --- | --- |
    | Выберите скрипт | toouse собственный сценарий, выберите __пользовательские__. В противном случае выберите предоставленный скрипт. |
    | Имя |Укажите имя для действия сценария hello. |
    | URI bash-скрипта |Укажите сценарий toohello URI hello, вызванный toocustomize hello кластера. |
    | Головной, рабочий или Zookeeper |Укажите узлы hello (**Head**, **рабочих**, или **ZooKeeper**) на какие hello настройки выполнения скрипта. |
    | Параметры |Укажите параметры hello, если это требуется для сценария hello. |

    Используйте hello __сохранить этот скрипт__ убедиться, что скрипт hello запись toomake применяется во время операции масштабирования.

5. Наконец, используйте hello **создать** кнопку tooapply hello сценария toohello кластера.

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>Применить действие сценария tooa под управлением кластера из Azure PowerShell

Прежде чем продолжить, убедитесь, что вы установили и настроили Azure PowerShell. Сведения о настройке рабочей станции toorun командлеты HDInsight PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).

Hello следующем примере показано, как tooapply действие сценария tooa запущенному кластеру:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

После завершения операции hello, появится примерно toohello сведения после текста:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>Применить действие сценария tooa под управлением кластера из hello Azure CLI

Прежде чем продолжить, убедитесь, что был установлен и настроен hello Azure CLI. Дополнительные сведения см. в разделе [Install hello Azure CLI](../cli-install-nodejs.md).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooswitch tooAzure режим диспетчера ресурсов, используйте следующую команду в командной строке hello hello:

        azure config mode arm

2. Используйте hello, следуя tooauthenticate tooyour подписки Azure.

        azure login

3. Используйте следующие команды tooapply tooa действие скрипта под управлением кластера hello

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    Если параметры для этой команды не заданы, вам будет предложено сделать это. Если hello указывается с помощью сценария `-u` принимает параметры, можно указать их с помощью hello `-p` параметра.

    Допустимые типы узлов: `headnode`, `workernode` и `zookeeper`. Если скрипт hello должен быть применен toomultiple типы узлов, задавать типы hello, разделенных «;». Например, `-n headnode;workernode`.

    toopersist Здравствуйте сценария, добавьте hello `--persistOnSuccess`. Также можно сохранить скрипт hello позже с помощью `azure hdinsight script-action persisted set`.

    После завершения задания hello, появится примерно toohello выходных данных после текста:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>Применить действие сценария tooa под управлением кластера с помощью API-интерфейса REST

См. статью [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx) (Выполнение действий скрипта в работающем кластере).

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>Применить действие сценария tooa под управлением кластера из hello HDInsight .NET SDK

Пример использования hello .NET SDK tooapply сценариев tooa кластера см. в разделе [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Просмотр журнала и изменения типа действий скриптов

### <a name="using-hello-azure-portal"></a>С помощью портала Azure hello

1. Из hello [портал Azure](https://portal.azure.com), выберите кластер HDInsight.

2. Обзор кластера HDInsight hello, выберите hello **действия скрипта** плитки.

    ![Элемент "Действия сценариев"](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Можно также выбрать **все параметры** , а затем выберите **действия скрипта** из hello в разделе "Параметры".

4. Журнал скриптов для этого кластера отображается на hello разделе действий скрипта. Эти сведения включают в себя список сохраняемых скриптов. Hello снимке вы увидите, что hello Solr был скрипт запуска в этом кластере. Снимок экрана приветствия не показывает все сохраненные сценарии.

    ![Раздел "Действия скриптов"](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. При выборе сценарий из журнала hello отображаются hello разделе "Свойства" для этого скрипта. С помощью hello в верхней части экрана приветствия можно снова запустить сценарий hello или повысить его уровень.

    ![Раздел "Свойства действий скрипта"](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. Можно также использовать hello **...**  toohello справа от записи в раздел tooperform hello действия скрипта действий.

    ![Использование действий скриптов](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Использование Azure PowerShell

| Используйте следующие hello: | слишком... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Получение сведений о действиях сохраняемого скрипта |
| Get-AzureRmHDInsightScriptActionHistory |Получить журнал сценария действия, применяемые toohello кластера или сведений для конкретных сценариев |
| Set-AzureRmHDInsightPersistedScriptAction |Повышает уровень нерегламентированным tooa действие сценария сохраняются действие сценария |
| Remove-AzureRmHDInsightPersistedScriptAction |Можно понизить уровень сохраненный скрипт действие нерегламентированных action tooan |

> [!IMPORTANT]
> С помощью `Remove-AzureRmHDInsightPersistedScriptAction` не отменяет hello действия, выполняемые с помощью сценария. Этот командлет удаляет только флаг материализованный hello.

Hello следующий пример сценария демонстрирует использование командлетов toopromote hello, а затем понижение уровня скрипта.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>С помощью hello Azure CLI

| Используйте следующие hello: | слишком... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Получение списка сохраняемых действий сценария |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Получение сведений о конкретном сохраняемом действии сценария |
| `azure hdinsight script-action history list <clustername>` |Получить журнал кластера toohello действия, применяемые для сценария |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Получение сведений о конкретном действии сценария |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Повышает уровень нерегламентированным tooa действие сценария сохраняются действие сценария |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Можно понизить уровень сохраненный скрипт действие нерегламентированных action tooan |

> [!IMPORTANT]
> С помощью `azure hdinsight script-action persisted delete` не отменяет hello действия, выполняемые с помощью сценария. Этот командлет удаляет только флаг материализованный hello.

### <a name="using-hello-hdinsight-net-sdk"></a>С помощью hello HDInsight .NET SDK

Пример использования журнал hello .NET SDK tooretrieve скриптов из кластера, повысить или понизить уровень скриптов см. в разделе [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> Этот пример также демонстрирует, как приложение HDInsight с помощью tooinstall hello .NET SDK.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Поддержка программного обеспечения с открытым исходным кодом, используемого в кластере HDInsight

Hello Microsoft Azure HDInsight service использует экосистему технологий открытым исходным кодом, сформированный вокруг Hadoop. Microsoft Azure предоставляет общий уровень поддержки для технологий с открытым исходным кодом. Дополнительные сведения см. в разделе hello **области поддержки** раздел hello [ответы поддержки Azure веб-сайт](https://azure.microsoft.com/support/faq/). Hello службы HDInsight обеспечивает дополнительный уровень поддержки встроенных компонентов.

Существует два типа компонентов открытым исходным кодом, доступных в hello службы HDInsight:

* **Встроенные компоненты** -эти компоненты предустановлен в кластерах HDInsight и предоставляют основные функциональные возможности кластера hello. Например YARN ResourceManager, язык запросов Hive hello (HiveQL) и библиотеку Mahout hello принадлежать toothis категории. Полный список компонентов кластера доступен в [новые возможности, предоставляемые HDInsight версиями кластеров Hadoop hello](hdinsight-component-versioning.md).
* **Пользовательские компоненты** -, как пользователь кластера hello, можно установить или использовать любой компонент, доступные в сообществе hello или созданный вами в рабочей нагрузке.

> [!WARNING]
> Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются. Службу технической поддержки Майкрософт помогает tooisolate и разрешить проблемы toothese связанные компоненты.
>
> Пользовательские компоненты получают toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello. Службу технической поддержки Майкрософт может быть проблемой может tooresolve hello или они может попросить вас tooengage доступных каналов для hello открытых технологий, которых находится глубокие знания для данной технологии. Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).

Служба HDInsight Hello предоставляет несколько способов toouse пользовательские компоненты. Hello же уровнем поддержки применяется независимо от того, как компонент используется, или установлен на кластере hello. Hello следующий список описывает hello наиболее распространенными способами, что пользовательские компоненты можно использовать в кластерах HDInsight:

1. Отправки заданий - Hadoop или других типов заданий, обрабатываемых или использовать пользовательские компоненты может быть отправлено toohello кластера.

2. Настройка кластера - во время создания кластера можно указать дополнительные параметры и пользовательские компоненты, установленные на узлах кластера hello.

3. Примеры — для популярных пользовательские компоненты, корпорация Майкрософт и другие могут предоставлять примеры использования этих компонентов в кластерах HDInsight hello. Эти примеры представляются без поддержки.

## <a name="troubleshooting"></a>Устранение неполадок

Можно использовать tooview Ambari web пользовательского интерфейса информация, зарегистрированная службой действий скрипта. При сбое во время создания кластера скрипт hello hello журналы также доступны в учетной записи хранения по умолчанию hello связанные с кластером hello. Информация о как tooretrieve hello журналов с помощью обоих этих параметров.

### <a name="using-hello-ambari-web-ui"></a>С помощью hello Ambari веб-интерфейса

1. В браузере перейдите toohttps://CLUSTERNAME.azurehdinsight.net. Замените ИМЯ_КЛАСТЕРА hello имя кластера HDInsight.

    При появлении запроса введите имя учетной записи администратора hello (администратор) и пароль для hello кластера. В веб-формы могут содержаться учетных данных администратора tooreenter hello.

2. На панели hello вверху hello страницы приветствия выберите hello **ops** входа. Отображается список текущих и предыдущих операций, выполняемых на hello кластера с помощью Ambari.

    ![Веб-панель Ambari с выбранной записью ops](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. Поиск записей hello, имеющих **запуска\_customscriptaction** в hello **операции** столбца. Эти записи создаются при запуске действия скрипта hello.

    ![Снимок экрана операций](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    tooview hello STDOUT и STDERR выходных данных, выберите элемент run\customscriptaction hello и прокрутите вниз список ссылок hello. Этот выход создается при запуске сценария hello и может содержать полезные сведения.

### <a name="access-logs-from-hello-default-storage-account"></a>Журналы событий из учетной записи хранения по умолчанию hello

Сбой создания кластера hello из-за ошибки действие сценария tooa журналы hello может осуществляться из учетной записи хранилища кластера hello.

* Hello журналы хранения можно найти по адресу `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![Снимок экрана операций](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    В этом каталоге журналы hello организована отдельно для головному узлу, workernode и zookeeper узлов. Ниже приведены некоторые примеры.

    * **Головной узел:** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Рабочий узел** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Узел Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Все потоки stdout и stderr hello соответствующего узла будет отправлен toohello учетной записи хранилища. Для каждого действия скрипта создается файл **output-\*.txt** и файл **errors-\*.txt**. Hello *.txt выходной файл содержит сведения о hello URI hello скрипта, который получен работать на узле hello. Например:

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* Можно повторно создать кластер действие сценария с hello таким же именем. В этом случае можно отличить hello журналы на основе имени папки hello даты. Например hello структуру папок для кластера (mycluster), созданные в разное время выглядит примерно toohello следующие записи журнала:

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* При создании кластера действие сценария с hello одинаковые имена на hello же день, можно использовать hello уникальный префикс tooidentify hello требуемых файлов журнала.

* При создании кластера рядом с 12:00 (полночь), возможно, файлы журнала hello охватывать два дня. В таких случаях вы видите две папки другую дату hello одного кластера.

* Отправка контейнер по умолчанию toohello файлов журнала может занять too5 минут, особенно для больших кластеров. Таким образом Если требуется, чтобы журналы hello tooaccess, не следует удалять немедленно hello кластера при сбое действия сценария.

### <a name="ambari-watchdog"></a>Модуль наблюдения Ambari

> [!WARNING]
> Не меняйте пароль hello для hello контрольного Ambari (hdinsightwatchdog) в кластере HDInsight под управлением Linux. Hello при смене пароля для этой учетной записи прерывается hello возможность toorun новые действия, сценарий на кластер HDInsight hello.

### <a name="cant-import-name-blobservice"></a>Не удается импортировать BlobService имени

__Симптомы__: hello сбоя действия сценария. Аналогичные toohello текст следующая ошибка отображается при просмотре hello операции в Ambari:

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Причина__: Эта ошибка возникает при обновлении клиента hello хранилища Azure Python, который входит в состав кластера HDInsight hello. HDInsight требуется клиент службы хранилища Azure версии 0.20.0.

__Разрешение__: tooresolve эту ошибку, установить соединение вручную tooeach узла кластера с помощью `ssh` и используйте hello следующая версия клиента правильного хранения hello tooreinstall команды:

```
sudo pip install azure-storage==0.20.0
```

Сведения о подключении toohello кластера с помощью SSH. в разделе [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>Журнал не отображает скрипты, используемые во время создания кластера

Если кластер создан до 15 марта 2016 г., в журнале действий скриптов могут отсутствовать записи. Если изменить размер кластера hello после 15 марта 2016 г., hello сценариев во время создания кластера отображаются в журнал как они применяются toonew узлов в кластере hello как часть hello операцию изменения размера.

Есть два исключения.

* Если кластер создан до 1 сентября 2015 г. Это дата добавления действий скриптов. Если кластер был создан раньше, действия скриптов не могли использоваться при его создании.

* Если используется несколько действий скрипта во время создания кластера и использовать hello же имя для нескольких сценариев или hello одинаковые имена, одному URI, но различные параметры для нескольких сценариев. В этих случаях появляется hello следующая ошибка:

    Нет новый скрипт действия может быть выполнена для этого кластера из-за tooconflicting имен сценария в существующих скриптов. Имена скриптов, указанные при создании кластера, должны быть уникальными. Существующие скрипты выполняются при изменении размера.

## <a name="next-steps"></a>Дальнейшие действия

* [Разработка скриптов действия сценария для HDInsight](hdinsight-hadoop-script-actions-linux.md)
* [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Добавление дополнительного хранилища кластера HDInsight tooan](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Этапы создания кластера"
