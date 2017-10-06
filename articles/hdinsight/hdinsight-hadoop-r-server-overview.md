---
title: "aaaIntroduction tooR Server на Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse R Server на HDInsight toocreate приложений для анализа больших данных."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6dc21bf5-4429-435f-a0fb-eea856e0ea96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: daf7b70a15748d66510a04da370f39c5f26eb4ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#<a name="introduction-toor-server-and-open-source-r-capabilities-on-hdinsight"></a>Введение tooR сервера и возможности R открытым исходным кодом на HDInsight

Microsoft R Server доступен в качестве варианта развертывания при создании кластеров HDInsight в Azure. Эта новая возможность предоставляет специалистами по анализу данных, статистике и программисты R с tooscalable доступ по запросу распределенных методы анализа в HDInsight.

Может быть кластеров масштабы toohello проектов и задач и затем обрыва, когда они больше не понадобятся. Так как они являются частью Azure HDInsight, эти кластеры поставляются с 24/7 уровня предприятия, соглашение об уровне ОБСЛУЖИВАНИЯ 99,9% времени и hello возможность toointegrate с другими компонентами в hello Azure экосистемы.

R Server на HDInsight предоставляет hello новейшим возможностям для анализа на основе R на наборах данных практически любого размера, загрузить tooeither хранилища больших двоичных объектов Azure или озере данных. Поскольку R Server встроена в R с открытым кодом, hello R-приложений, создаваемые могут использовать любые hello 8000 + пакетов R с открытым кодом. также доступны подпрограммы Hello в ScaleR пакета analytics большие наборы данных корпорации Майкрософт, входящий в состав R Server.

Hello граничного узла кластера обеспечивает удобное место tooconnect toohello кластера и toorun R-сценарии. С граничного узла у вас есть hello функций ScaleR возможность выполнения hello параллелизован распределенных между ядрами hello hello edge узел сервера. Также выполнять их на узлах hello hello кластера с помощью элемента ScaleR Map-Reduce Hadoop или Spark контекстов вычислений.

Hello моделей или прогнозов, которые могут быть загружены в результате анализа для использовать локально. Их также можно использовать в любой службе Azure, в частности в [веб-службе](../machine-learning/machine-learning-publish-a-machine-learning-web-service.md) [Студия машинного обучения Microsoft Azure](http://studio.azureml.net).

## <a name="get-started-with-r-on-hdinsight"></a>Начало работы с R Server в HDInsight
tooinclude R Server в кластер HDInsight, необходимо выбрать hello тип кластера сервера R, при создании кластера HDInsight с помощью портала Azure hello. Hello тип кластера R Server включает в себя R Server hello данные по узлам кластера hello и на граничного узла, который служит в качестве зоны размещения для анализа на основе R Server. В разделе [Приступая к работе с сервером R в HDInsight](hdinsight-hadoop-r-server-get-started.md) Пошаговое руководство по как toocreate hello кластера.

## <a name="learn-about-data-storage-options"></a>Варианты хранилищ данных
Хранилище по умолчанию для файловой системы HDFS hello кластеров HDInsight можно связать с учетной записью хранения Azure или хранилище Озера данных Azure. Эту связь гарантирует, что все данные будут переданы сохраняемым toohello хранения данных кластера во время анализа. Существуют различные инструменты для обработки hello передачи toohello вариант хранения данных, выбрать, включая hello средство передачи на основе портала учетной записи хранения hello и hello [AzCopy](../storage/common/storage-use-azcopy.md) программы.

У вас есть возможность добавить доступ tooadditional больших двоичных объектов и Озера хранилищ данных во время процесса независимо от параметра hello основного хранилища используется подготовки кластера hello hello. В разделе [Приступая к работе с сервером R в HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-get-started) сведения о добавлении учетных записей доступа к tooadditional. В разделе дополнительных hello [параметры хранилища Azure R Server на HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-storage) toolearn статьи о применении нескольких учетных записей хранения.

Можно также использовать [файлов Azure](../storage/files/storage-how-to-use-files-linux.md) качестве хранилища для использования на узле edge hello. Файлы Azure позволяет toomount общую папку, созданную в хранилище Azure toohello Linux файловой системы. Дополнительные сведения об этих вариантах хранения данных для R Server в кластере HDInsight см. в статье [Параметры службы хранилища Azure для R Server в кластерах HDInsight](hdinsight-hadoop-r-server-storage.md).

## <a name="access-r-server-on-hello-cluster"></a>R Server доступа в кластере hello
Можно подключить tooR сервера на hello граничного узла с помощью браузера, мы выбрали tooinclude RStudio сервера во время процесса инициализации hello. Если он не был установлен при подготовке кластера hello, можно добавить его позже. Сведения об установке сервера RStudio Server после создания кластера см. в статье [Установка RStudio с R Server в HDInsight](hdinsight-hadoop-r-server-install-r-studio.md). Toohello R Server можно также подключиться с помощью консоли hello R tooaccess SSH/PuTTY. 

## <a name="develop-and-run-r-scripts"></a>Разработка и выполнение сценариев R
Hello R сценарии создания и запуска можно использовать любой из hello 8000 + пакетов R с открытым кодом в toohello сложения параллельно и распределенных процедур, доступных в библиотеке ScaleR hello. Как правило сценарий, который выполняется с сервером R на hello граничного узла выполняется в интерпретатор hello R на этом узле. Hello исключениями являются шагов, которые требуется toocall функции ScaleR с контекстом вычислений, который имеет значение tooHadoop Map Reduce (RxHadoopMR) или Spark (RxSpark). В этом случае функции hello работало в режиме распределенного этих данных (задача) узлы кластера hello, связанные с данными hello ссылка. Дополнительные сведения о параметрах контекста hello различных вычислений см. в разделе [вычислений параметры контекста R Server на HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).

## <a name="operationalize-a-model"></a>Ввод модели в эксплуатацию
По завершении моделирование данных вы ввода в эксплуатацию hello модели toomake прогнозы новых данных из Azure и локальными. Этот процесс называется оценкой. Оценка может осуществляться в HDInsight, Машинном обучении Azure или локальной среде.

### <a name="score-in-hdinsight"></a>Оценка в HDInsight
tooscore в HDInsight, написать функцию R, вызывающий вашей toomake прогнозов модели к новому файлу данных вы загрузили tooyour учетной записи хранилища. Затем сохраните прогнозы hello задней toohello учетной записи хранилища. Hello сопоставление по запросу можно запускать на hello граничного узла кластера или с помощью запланированных заданий.  

### <a name="score-in-azure-machine-learning-aml"></a>Оценка в Машинном обучении Azure
используя AML веб-службы, используйте hello tooscore открыть исходный пакет Azure Machine Learning R, известный как [AzureML](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toopublish модели как веб-службу Azure. Для удобства этот пакет уже установлены на hello граничного узла. Затем используйте средства hello в машинное обучение toocreate пользовательский интерфейс для hello веб-службы и затем вызвать hello веб-службы, необходимые для оценки.

Если этот параметр выбран, необходимо tooconvert любые объекты ScaleR модели объектов tooequivalent модели с открытым исходным кодом для использования с hello веб-службы. Для этого используйте функции приведения ScaleR, такие как `as.randomForest()`, для моделей на основе ансамблей.

### <a name="score-on-premises"></a>Оценка в локальной среде
tooscore в локальной среде после создания модели можно сериализовать модели hello в R, загрузки, отменить сериализацию, а затем использовать его для оценки новых данных. Можно оценить новые данные с помощью hello подход, описанный ранее в [оценки в HDInsight](#scoring-in-hdinsight) или с помощью [DeployR](https://deployr.revolutionanalytics.com/).

## <a name="maintain-hello-cluster"></a>Обслуживание кластера hello
### <a name="install-and-maintain-r-packages"></a>Установка и обслуживание пакетов R
Большинство пакетов hello R используемых необходимы на hello граничного узла с момента большинство шагов R-сценарии работы с ней. tooinstall дополнительных пакетов R на hello граничного узла, можно использовать обычные hello `install.packages()` метод в R.

Если используется только подпрограммы из библиотеки ScaleR hello в кластере hello, необязательно обычно tooinstall дополнительных пакетов R на узлах данных hello. Тем не менее, может потребоваться использование toosupport hello дополнительные пакеты **rxExec** или **RxDataStep** выполнение на узлах данных hello.

В этих случаях hello дополнительных пакетов можно установить с помощью сценария действия после создания кластера hello. Дополнительные сведения см. в статье [Приступая к работе с R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-get-started.md).   

### <a name="change-hadoop-map-reduce-memory-settings"></a>Изменение параметров памяти Hadoop MapReduce
Кластер может быть измененный toochange hello объем памяти, доступной tooR сервера при выполнении задания Map Reduce. toomodify кластер, используйте hello Ambari Apache пользовательского интерфейса, которая доступна через hello Azure — колонка портала для кластера. Сведения о как tooaccess hello Ambari пользовательского интерфейса для кластера содержатся в разделе [управление кластерами HDInsight с помощью Ambari веб-интерфейса hello](hdinsight-hadoop-manage-ambari.md).

Это также возможно toochange hello объем памяти, доступной tooR сервера с использованием Hadoop параметров в вызове hello слишком**RxHadoopMR** следующим образом:

    hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"  

### <a name="scale-your-cluster"></a>Масштабирование кластера
Существующий кластер может масштабироваться вверх или вниз через портал hello. Путем масштабирования, можно получить дополнительную емкость hello, которые могут потребоваться для более крупных задач обработки, либо можно масштабировать обратно кластера при простое. Инструкции о том, как tooscale кластера, в разделе [кластеры HDInsight управление](hdinsight-administer-use-portal-linux.md).

### <a name="maintain-hello-system"></a>Обслуживание системы hello
Исправлений ОС tooapply обслуживания и другие обновления выполняются на hello базовый виртуальных машин Linux в кластер HDInsight в нерабочие часы. Как правило каждый понедельник и четверг обслуживания выполняется в 3:30 (с учетом hello местное время для hello виртуальной Машины). Обновления выполняются таким образом, что они не влияет на более чем квартала hello кластера одновременно.  

Поскольку избыточны hello головного узла, а не все узлы данных зависят от него, все задания, которые выполняются в течение этого времени может замедлить работу. Они по-прежнему выполняться toocompletion, однако. Обслуживание не затрагивает установленное пользовательское программное обеспечение или локальные данные, если только в системе не возникнет неустранимая ошибка, требующая повторной сборки кластера.

## <a name="learn-about-ide-options-for-r-server-on-an-hdinsight-cluster"></a>Параметры IDE для R Server в кластере HDInsight
Hello Linux граничного узла из кластера HDInsight является целевой зоны для анализа на основе R hello. Последние версии hdinsight, укажите параметр по умолчанию для установки версии сообщества hello [RStudio сервера](https://www.rstudio.com/products/rstudio-server/) на узле edge hello в интегрированной среде разработки на основе браузера. Использование RStudio сервера в качестве интегрированной среды разработки для разработки hello и выполнение сценариев R может быть значительно более производительны, чем просто с помощью консоли hello R. При выборе tooadd RStudio сервера при создании hello кластера, но требуется tooadd его более поздней версии, затем в разделе [установки R Studio Server в кластерах HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-install-r-studio). +

Другой вариант полной интегрированной среды разработки является tooinstall рабочего стола интегрированной среды разработки и использовать его tooaccess hello кластера с использованием удаленного Map Reduce или Spark контекст вычислений. К возможным вариантам относятся [Инструменты R для Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx), RStudio и [StatET](http://www.walware.de/goto/statet) на базе Eclipse от Walware.

Наконец, доступ hello R Server консоли на hello граничного узла, введя **R** hello Linux командной строки после подключения через SSH или PuTY. При использовании интерфейса консоли hello, это удобный toorun текстовый редактор для разработки скриптов R в другом окне Вырезать и вставить части скрипта в консоли hello R, при необходимости.

## <a name="learn-about-pricing"></a>Информация о ценах
Hello сборы, связанные с HDInsight кластер с сервером R, аналогичную структуру toohello сборов за hello Стандартная кластеров HDInsight. Они основаны на hello размера hello базовой ВМ между именем hello, данных и краевым узлам, добавляя hello uplift core час. Дополнительные сведения о цены на HDInsight и доступность hello 30-дневной бесплатной пробной версии см. в разделе [цены на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о как кластеры toouse R Server с HDInsight, в разделе hello следующие вопросы:

* [Приступая к работе с R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-get-started.md)
* [Добавить tooHDInsight RStudio сервера (если не устанавливается во время создания кластера)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Варианты контекста вычислений для R Server в HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)
* [Параметры службы хранилища Azure для R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-storage.md)
