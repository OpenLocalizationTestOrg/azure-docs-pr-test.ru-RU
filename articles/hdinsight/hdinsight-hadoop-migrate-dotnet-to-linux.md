---
title: "aaaUse .NET с Hadoop MapReduce в HDInsight под управлением Linux — в Azure | Документы Microsoft"
description: "Узнайте, как toouse приложений .NET для потоковой передачи MapReduce в HDInsight под управлением Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a>Перенос решений .NET для HDInsight под управлением Windows на основе tooLinux HDInsight

Используйте кластеры HDInsight под управлением Linux [моно (https://mono-project.com)](https://mono-project.com) toorun приложений .NET. Моно позволяет toouse компоненты .NET, таких как приложения MapReduce с HDInsight под управлением Linux. В этом документе сведения способ создания решения toomigrate .NET для toowork кластеры HDInsight под управлением Windows с моно на HDInsight под управлением Linux.

## <a name="mono-compatibility-with-net"></a>Совместимость Mono с .NET

Mono версии 4.2.1 входит в состав HDInsight версии 3.5. Дополнительные сведения о версии hello Mono, входящий в состав HDInsight см. в разделе [версий компонента HDInsight](hdinsight-component-versioning.md). tooinstall моно, определенную версию в разделе hello [установку или обновление моно](hdinsight-hadoop-install-mono.md) документа.

Подробные сведения о совместимости между моно и .NET см. в разделе hello [моно совместимости (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) документа.

> [!IMPORTANT]
> Hello SCP.NET framework совместим с моно. Дополнительные сведения об использовании SCP.NET моно см. в разделе [топологии toodevelop C# используйте Visual Studio для Apache Storm на HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="automated-portability-analysis"></a>Автоматический анализ переносимости

Hello [анализатор переносимости .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) может быть toogenerate используется отчет о несовместимости между приложением и Mono. Используйте следующие шаги tooconfigure hello анализатора toocheck hello приложения для обеспечения переносимости моно:

1. Установка hello [анализатор переносимости .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer). Во время установки выберите версию Visual Studio toouse hello.

2. В Visual Studio 2015 выберите __анализ__ > __параметры анализатор переносимости__и убедитесь, что __4.5__ возврата hello __моно__  раздел.

    ![Возврат моно раздел параметров анализатора hello 4.5](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    Выберите __ОК__ toosave hello конфигурации.

3. Выберите __Анализ__ > __Analyze Assembly Portability__ (Анализ переносимости сборки). Выберите hello сборку, содержащую решение, а затем выберите __откройте__ toobegin анализа.

4. После завершения анализа выберите __Анализ__ > __View analysis reports__ (Просмотр отчетов об анализе). В __результаты анализа переносимость__выберите __откройте отчет__ tooopen отчета.

    ![Диалоговое окно результатов анализатора переносимости](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> Анализатор Hello нельзя перехватить все проблемы с решением. Например, путь к файлу `c:\temp\file.txt` считается ОК, поскольку моно выполняется в Windows и hello путь является допустимым в этом контексте. Однако hello путь является недопустимым на платформе Linux.

## <a name="manual-portability-analysis"></a>Ручной анализ переносимости

Выполнение аудита вручную с помощью данных hello в hello кода [переносимость приложения (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) документа.

## <a name="modify-and-build"></a>Изменение и выполнение сборки

Продолжайте toobuild toouse Visual Studio .NET решения для HDInsight. Тем не менее необходимо убедиться, что этот проект hello используется настроенный toouse .NET Framework 4.5.

## <a name="deploy-and-test"></a>Развертывание и тестирование

После изменения к решению, используя рекомендации hello из hello анализатор переносимости .NET или вручную анализа, необходимо выполнить тестирование с HDInsight. Тестирование решения hello в кластере HDInsight под управлением Linux может раскрыть небольшие проблемы, требующие toobe исправлено. Мы рекомендуем включить дополнительное ведение журнала в приложении во время тестирования.

Дополнительные сведения о доступе к журналам см. в разделе hello следующие документы:

* [Доступ к журналам приложений YARN в HDInsight под управлением Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a>Дальнейшие действия

* [Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)