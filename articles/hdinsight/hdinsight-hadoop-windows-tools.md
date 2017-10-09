---
title: "aaaUse ПК Windows с Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Сведения об использовании Hadoop в HDInsight на компьютере с Windows, а также о запросе кластеров и управлении ими с помощью PowerShell, Visual Studio и средств Linux. Разработка решений для работы с большими данными на языке .NET."
services: hdinsight
keywords: "hadoop в windows, hadoop для windows"
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a>Незавершенное hello экосистема Hadoop в HDInsight с помощью компьютера Windows

Дополнительные сведения о разработке и параметры управления на Компьютере Windows hello для работы в экосистеме hello Hadoop в HDInsight. 

Служба HDInsight включает в себя компоненты Apache Hadoop и Hadoop, технологии с открытым исходным кодом, разработанные на платформе Linux. HDInsight версии 3.4 и выше hello распространения Ubuntu Linux использует в качестве базовой операционной системы для кластера hello hello. Но с HDInsight можно также работать в клиенте или среде разработки Windows.

## <a name="use-powershell-for-deployment-and-management-tasks"></a>Задачи развертывания и управления с помощью PowerShell
Azure PowerShell — это среда сценариев, можно использовать toocontrol и автоматизации задач развертывания и управления в HDInsight из Windows.

При помощи PowerShell можно выполнять такие задачи:

* [создавать кластеры](hdinsight-hadoop-create-linux-clusters-azure-powershell.md);
* [Выполнение запросов Hive с помощью PowerShell](hdinsight-hadoop-use-hive-powershell.md)
* [управлять кластерами](hdinsight-administer-use-powershell.md).

Выполните действия слишком[Установка и настройка Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooget hello последнюю версию. Если у вас есть сценарии, требующие изменения toobe toouse hello новые командлеты для диспетчера ресурсов Azure, см. раздел [перенести tooAzure средства разработки на основе диспетчера ресурсов для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="utilities-you-can-run-in-a-browser"></a>Браузерные служебные программы
Hello следующие программы имеют веб-интерфейса, который выполняется в браузере.
* **[Azure облачной оболочки (Предварительная версия)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**  является интерактивной командной строки оболочки, который выполняется в браузере и изнутри hello портал Azure.
* **[Веб-Интерфейс Ambari](hdinsight-hadoop-manage-ambari.md)**  управления и мониторинга служебной программы, доступные в hello портал Azure, которое может быть используется toomanage различных типов заданий, таких как:
    * [Использовать Ambari с hello REST API](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [используйте представление Hive в Ambari](hdinsight-hadoop-use-hive-ambari-view.md)
    * [использование представлений Tez в Ambari](hdinsight-debug-ambari-tez-view.md).

## <a name="data-lake-hadoop-tools-for-visual-studio"></a>Средства Data Lake (Hadoop) для Visual Studio
Используйте средства Озера данных для toodeploy Visual Studio и управление ими Storm топологии. Средства Озера данных также устанавливает hello SCP.NET пакета SDK, который позволяет вам toodevelop топологии Storm C# с помощью Visual Studio.

Перед переходом в следующих примерах toohello [установки и повторите Озера Data Tools для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md). 

При помощи средств Data Lake и Visual Studio можно выполнять следующие задачи:
* [Развертывать топологии Storm и управлять ими](hdinsight-storm-deploy-monitor-topology-linux.md).
* [Разрабатывать топологии Storm на языке C#](hdinsight-storm-develop-csharp-visual-studio-topology.md). шаблоны битов Hello пример топологии Storm могут подключаться toodatabases, таких как Azure Cosmos DB и базы данных SQL.

## <a name="visual-studio-and-hello-net-sdk"></a>Visual Studio и .NET SDK hello 

Можно использовать Visual Studio с кластерами toomanage .NET SDK hello и разрабатывать приложения для больших данных. Других интегрированных средах разработки можно использовать для следующих задач hello, но примеры показаны в Visual Studio.

Примеры задач, которые можно выполнить с hello .NET SDK в Visual Studio.
* [создавать кластеры и работать в HDInsight из приложения .NET Framework](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md);
* [Выполнять запросы Hive, с помощью hello .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [использовать определяемые пользователем функции C# при потоковой передаче Hive и Pig в Hadoop](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).

> Совет При запуске решения .NET с кластерами HDInsight под управлением Windows, это подходящий момент tooplan миграции кластеров на основе tooLinux. Дополнительные сведения см. в разделе [решение перенести .NET для HDInsight под управлением Windows на основе tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a>Intellij IDEA и Eclipse IDE для кластеров Spark
Оба [ИДЕЯ Intellij](https://www.jetbrains.com/idea/download) и hello [интегрированной среды разработки Eclipse](https://www.eclipse.org/downloads/) можно использовать для:
* разрабатывать и отправлять приложения Scala Spark в кластер HDInsight Spark;
* получать доступ к ресурсам кластера Spark;
* разрабатывать и запускать приложения Scala Spark в локальной среде.

В этих статьях описывается: 
* IntelliJ ИДЕЯ: [Spark создание приложений, с помощью средств Azure для подключаемый модуль Intellij hello и hello Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)
* Eclipse IDE или Scala интегрированную среду разработки Eclipse: [Spark создания приложений и средств Azure для Eclipse hello](hdinsight-apache-spark-eclipse-tool-plugin.md) 


## <a name="notebooks-on-spark-for-data-scientists"></a>Записные книжки в Spark для специалистов по обработке и анализу данных 
Кластеры Apache Spark в HDInsight включают записные книжки Zeppelin и ядра, которые можно использовать с записными книжками Jupyter. 

* [Узнайте, как toouse ядер на Spark кластеры с приложениями Spark tootest записные книжки Jupyter](hdinsight-apache-spark-zeppelin-notebook.md)
* [Узнайте, как ноутбуки Zeppelin toouse на Spark кластеры toorun Spark заданий](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a>Запуск средств и технологии Linux в Windows

Ситуации, когда необходимо использовать специальное средство или технология, которая доступна только для Linux, рассмотрим следующие варианты hello.

* **Bash (бета-версия) на платформе Windows 10** предоставляет подсистему Linux в Windows. Bash позволяет toodirectly запуска программ Linux без toomaintain выделенной установки Linux. [Установите и запустите hello Bash бета-версии на Windows 10](https://msdn.microsoft.com/commandline/wsl/install_guide)
* **Docker для Windows** предоставляет средства на базе Linux toomany доступ и запускается непосредственно из Windows. Например можно использовать клиент Beeline hello toorun Docker для куста непосредственно из Windows. Можно также использовать Docker toorun локального книжке Jupyter и удаленное подключение tooSpark на HDInsight. [Начните работу с Docker для Windows.](https://docs.docker.com/docker-for-windows/)
* **[MobaXTerm](http://mobaxterm.mobatek.net/)**  разрешает toographically обзора hello кластера файловой системы по SSH-подключения.

## <a name="next-steps"></a>Дальнейшие действия
Если вы новый tooworking в кластеры под управлением Linux, см. раздел hello статей, выполните:
* [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Сведения об использовании HDInsight в Linux](hdinsight-hadoop-linux-information.md)