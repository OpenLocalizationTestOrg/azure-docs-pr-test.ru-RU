---
title: "aaaWhat — виртуальная машина анализа данных? | Документация Майкрософт"
description: "Как tooget начал делать основные сценарии аналитики с данных обработки и анализа виртуальными машинами."
keywords: "средства анализа и обработки данных, виртуальная машина для анализа и обработки данных, средства для анализа и обработки данных, анализ и обработка данных Linux"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d4f91270-dbd2-4290-ab2b-b7bfad0b2703
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 18c7a75208671c663f3b6be6ee8d0bf666772e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-cloud-based-data-science-virtual-machine-for-linux-and-windows"></a>Введение toohello облачного виртуальная машина анализа данных для Linux и Windows
Hello виртуальной машины обработки и анализа данных (DSVM) является настроенного образа виртуальной Машины в облаке Azure корпорации Майкрософт, предназначенный для выполнения обработки и анализа данных. Он имеет обработки и анализа многие популярные данных и другие средства предварительно установлен и предварительно настроенных toojump-start построение интеллектуальных приложений для расширенной аналитики. Она доступна на платформах Windows Server и Linux. Версия DSVM для операционных систем Windows работает в Windows Server 2016 и Windows Server 2012. Мы предлагаем выпуск hello DSVM OpenLogic 7.2 CentOS под управлением ОС Linux и Ubuntu 16.04 LTS Linux. 

В этом разделе рассматриваются возможности hello ВМ обработки и анализа данных, описаны некоторые основные сценарии hello hello виртуальной Машины с помощью, конкретизирует hello ключевые функции, доступные на приветствия Windows и версий Linux и описано, как tooget работу с их помощью.

## <a name="what-can-i-do-with-hello-data-science-virtual-machine"></a>Что можно сделать hello виртуальная машина анализа данных
Цель Hello hello виртуальная машина анализа данных — tooprovide специалистов по данным на всех уровнях навыков и ролей в среде обработки и анализа данных без возникновения конфликтов. Эта виртуальная машина позволяет значительно сэкономить время на развертывании собственной среды. Вместо этого вы можете сразу же запустить проект по анализу и обработке данных в новом экземпляре виртуальной машины. 

Hello ВМ обработки и анализа данных разработан и настроить его для работы со сценариями широкое распространение. Масштаб среды можно увеличивать и уменьшать согласно требованиям проекта. Вы являются может toouse задач обработки и анализа данных tooprogram предпочитаемый язык. Можно установить другие средства и настроить систему hello для свои конкретные нужды.

## <a name="key-scenarios"></a>Ключевые сценарии
В этом разделе предлагаются некоторые основные сценарии, для которых hello можно развернуть ВМ обработки и анализа данных.

### <a name="preconfigured-analytics-desktop-in-hello-cloud"></a>Предварительно настроить рабочий стол аналитика в облаке hello
Hello ВМ обработки и анализа данных предоставляет базовой конфигурации для поиска tooreplace их локальных компьютерах с desktop управляемой облачной команд обработки и анализа данных. Базовый уровень гарантирует, что все hello специалистами по анализу данных в команде согласованное установку с какие экспериментах tooverify и совместной. Также снижает затраты за счет снижения нагрузки sysadmin hello и сохранение вовремя hello необходимости tooevaluate, установки и обслуживания hello различных пакетов программного обеспечения требуется toodo расширенной аналитики.  

### <a name="data-science-training-and-education"></a>Обучение обработке и анализу данных
Enterprise инструкторов и преподавателей, в которых классы для обработки и анализа данных обычно предоставляют tooensure образ виртуальной машины, у своих учащихся согласованная Установка и предсказуемое работы образцов hello. Hello ВМ обработки и анализа данных создается среда, по требованию с помощью согласованного программы установки, которая упрощает задачи поддержки и несовместимости hello. Случаи, где эти среды должны toobe часто создана специально для более короткие учебным курсам, существенно выигрывают.

### <a name="on-demand-elastic-capacity-for-large-scale-projects"></a>Эластичность по требованию для проектов большого масштаба
Интенсивная работа и соревнования по обработке и анализу данных, моделирование и изучение данных большого масштаба обычно требуют использования мощного оборудования в течение короткого периода. Hello ВМ обработки и анализа данных может помочь быстро по запросу обработки и анализа данных среды hello реплицировать, на горизонтальным масштабированием серверах, позволяющие экспериментов, требующие мощная toobe вычислительных ресурсов выполните.

### <a name="short-term-experimentation-and-evaluation"></a>Краткосрочные эксперименты и оценка
Hello ВМ обработки и анализа данных может быть используется tooevaluate или узнать средств Microsoft R Server, SQL Server, например, Visual Studio Сервис, Jupyter, глубоко обучения / ML наборы инструментов и новые инструменты широко применяются в hello сообщества с установки с минимальными усилиями. Поскольку hello ВМ обработки и анализа данных может быть быстро настроить, оно может применяться в других краткосрочное использование сценариев, например опубликованных экспериментов, выполнение демонстрационные материалы, в следующих пошаговых руководствах документации сеансов или конференции учебники по репликации.

### <a name="deep-learning"></a>Глубокое обучение
обработки и анализа данных Hello виртуальной Машины можно использовать для обучения модели с помощью алгоритмов углубленного обучения на основе оборудования GPU (единицы обработки графики). Использование виртуальной Машины, масштабирование возможностям облака Azure, DSVM дает возможность использовать GPU на базе оборудования в облаке hello согласно необходимости. Один можно переключить tooa GPU на основе виртуальной Машины при обучении большие модели, или требуется высокая скорость вычислений при сохранении hello того же диска ОС.  выпуск Windows Server 2016 Hello DSVM поставляется предварительно установлены с драйверов GPU, платформы и версии GPU hello глубокой алгоритмы обучения. На hello Linux глубокого изучения на GPU разрешены только на hello [виртуальная машина анализа данных для Linux (Ubuntu) выпуска](http://aka.ms/dsvm/ubuntu). В этом случае все платформы углубленного обучения hello будет режим резервной toohello ЦП можно развернуть выпуск Ubuntu-Windows-2016 hello ВМ обработки и анализа данных toonon GPU на основе виртуальной машины Azure. Ранее мы публиковали [набор инструментов для глубокого изучения](http://aka.ms/dsvm/deeplearning) для Windows Server 2012. Теперь же мы рекомендуем использовать Windows Server 2016 для рабочих нагрузок глубокого обучения на платформе Windows. выпуск на основе CentOS Linux Hello hello DSVM содержит только hello ЦП строит некоторых hello глубокого изучения средства (CNTK, Tensorflow, MXNet), но не предустановлена драйверов GPU hello и платформы. 

## <a name="whats-included-in-hello-data-science-vm"></a>Содержание hello ВМ обработки и анализа данных?
Hello виртуальная машина анализа данных содержит много обработки и анализа данных для популярных и глубокого изучения средств уже установлен и настроен. Он также включает средства, которые позволяют легко toowork различных продуктов Azure данных и аналитики. Вы можете анализировать и построения прогнозных моделей для крупных наборов данных с помощью hello Microsoft R Server или SQL Server 2016. Целый ряд других средств с открытым исходным кодом hello и корпорации Майкрософт, также включены, а также образец кода и портативных компьютеров. Hello следующей таблице перечисляются и сравнивает hello основных компонентов, включенных в приветствия Windows и Linux выпусков hello виртуальная машина анализа данных.


| **Средство**                                                           | **Выпуск для Windows** | **Выпуск для Linux** |
| :------------------------------------------------------------------ |:-------------------:|:------------------:|
| [Microsoft R Open](https://mran.microsoft.com/open/) с предустановленными популярными пакетами   |Да                      | Да             |
| [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) Developer Edition включает в себя: <br />  параллельную платформу &nbsp;&nbsp;&nbsp;&nbsp;* [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started) и распределенную высокопроизводительную платформу R;<br />  &nbsp;&nbsp;&nbsp;&nbsp;* [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) — новые передовые алгоритмы ML от Майкрософт; <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [средства операционализации R](https://msdn.microsoft.com/microsoft-r/operationalize/about).                                            |Да                      | Да <br/> (пакет MicrosoftML пока недоступен)|
| [Microsoft Office](https://products.office.com/en-us/business/office-365-proplus-business-software) Pro Plus с общей активацией — Excel, Word и PowerPoint   |Да                      |Нет              |
| [Anaconda Python](https://www.continuum.io/) 2.7, 3.5 с предустановленными популярными пакетами    |Да                      |Да              |
| [JuliaPro](https://juliacomputing.com/products/juliapro.html) с предварительно установленными популярными пакетами для языка Julia                         |Да                      |Да              |
| Реляционные базы данных                                                            | [SQL Server 2016 SP1](https://www.microsoft.com/sql-server/sql-server-2016) <br/> Developer Edition| [PostgreSQL](https://www.postgresql.org/) |
| Инструменты базы данных                                                       | * SQL Server Management Studio <br/>* SQL Server Integration Services<br/>* [bcp, sqlcmd](https://docs.microsoft.com/sql/tools/command-prompt-utility-reference-database-engine)<br /> * Драйверы ODBC и JDBC| * [SQuirreL SQL](http://squirrel-sql.sourceforge.net/) (инструмент запросов), <br /> * bcp, sqlcmd <br /> * Драйверы ODBC и JDBC|
| Масштабируемое аналитическое решение в базе данных со службами SQL Server R | Да     |Нет              |
| **[Jupyter Notebook Server](http://jupyter.org/) со следующими ядрами**                                  | Да     | Да |
|     &nbsp;&nbsp;&nbsp;&nbsp;* R | Да | Да |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Python 2.7 и 3.5 | Да | Да |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Julia | Да | Да |
|     &nbsp;&nbsp;&nbsp;&nbsp;* PySpark | Нет | Да |
|     &nbsp;&nbsp;&nbsp;&nbsp;* [Sparkmagic](https://github.com/jupyter-incubator/sparkmagic) | Нет | Да (только Ubuntu) |
|     &nbsp;&nbsp;&nbsp;&nbsp;* SparkR     | Нет | Да |
| JupyterHub (многопользовательский сервер блокнотов)| Нет | Да |
| **Инструменты разработки, редакторы кода и интегрированные среды разработки**| | |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio 2017 (Community Edition)](https://www.visualstudio.com/community/) с подключаемым модулем Git, Azure HDInsight (Hadoop), Data Lake, SQL Server Data Tools (SSDT), [Node.js](https://github.com/Microsoft/nodejstools), [Python](http://aka.ms/ptvs) и [инструментами R для Visual Studio (RTVS)](http://microsoft.github.io/RTVS-docs/) | Да | Нет |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio Code](https://code.visualstudio.com/) | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [RStudio Desktop](https://www.rstudio.com/products/rstudio/#Desktop) | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [RStudio Server](https://www.rstudio.com/products/rstudio/#Server) | Нет | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [PyCharm](https://www.jetbrains.com/pycharm/) | Нет | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Atom](https://atom.io/) | Нет | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Juno (интегрированная среда разработки Julia)](http://junolab.org/)| Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* Vim и Emacs | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* Git и GitBash | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* OpenJDK | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* .Net Framework | Да | Нет |
| PowerBI Desktop | Да | Нет |
| Tooaccess пакеты SDK Azure и пакет аналитики Cortana услуг | Да | Да |
| **Инструменты перемещения данных и управления ими** | | |
| &nbsp;&nbsp;&nbsp;&nbsp;* Обозреватель хранилищ Azure | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Интерфейс командной строки Azure](https://docs.microsoft.com/cli/azure/overview) | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure Powershell | Да | Нет |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Azcopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy) | Да | Нет |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Adlcopy (служба хранилища Azure Data Lake)](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob) | Да | Нет |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Инструмент переноса данных DocDB](https://docs.microsoft.com/azure/documentdb/documentdb-import-data) | Да | Нет |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Шлюз управления данными Майкрософт](https://msdn.microsoft.com/library/dn879362.aspx): перемещение данных между локальным хранилищем и облаком | Да | Нет |
| &nbsp;&nbsp;&nbsp;&nbsp;* Служебные программы командной строки Unix/Linux | Да | Да |
| [Apache Drill](http://drill.apache.org) для просмотра данных | Да | Да |
| **Инструменты машинного обучения** |||
| &nbsp;&nbsp;&nbsp;&nbsp;* Средства, интегрирующиеся с [Машинным обучением Azure](https://azure.microsoft.com/services/machine-learning/) (R, Python) | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Xgboost](https://github.com/dmlc/xgboost) | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit) | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Weka](http://www.cs.waikato.ac.nz/ml/weka/) | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Rattle](http://rattle.togaware.com/) | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [LightGBM](https://github.com/Microsoft/LightGBM) | Нет | Да (только Ubuntu) |
| &nbsp;&nbsp;&nbsp;&nbsp;* [H2O](https://www.h2o.ai/h2o/) | Нет | Да (только Ubuntu) |
| **Инструменты глубокого обучения на основе графического процессора** |Версия для Windows Server 2016  |Версия для Ubuntu |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Microsoft Cognitive Toolkit (CNTK)](http://cntk.ai) | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Tensorflow](https://www.tensorflow.org/) | Да | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [MXNet](http://mxnet.io/) | Да | Да|
| &nbsp;&nbsp;&nbsp;&nbsp;* [Caffe и Caffe2](https://github.com/caffe2/caffe2) | Нет | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Torch](http://torch.ch/) | Нет | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Theano](https://github.com/Theano/Theano) | Нет | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Keras](https://keras.io/)| Нет | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [NVidia Digits](https://github.com/NVIDIA/DIGITS) | Нет | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* [CUDA, CUDNN, драйвер Nvidia](https://developer.nvidia.com/cuda-toolkit) | Да | Да |
| **Платформа для больших данных (только Devtest)**|||
| &nbsp;&nbsp;&nbsp;&nbsp;* Локальный изолированный экземпляр [Spark](http://spark.apache.org/) | Нет | Да |
| &nbsp;&nbsp;&nbsp;&nbsp;* Локальный экземпляр [Hadoop](http://hadoop.apache.org/) (HDFS, YARN) | Нет | Да |



## <a name="how-tooget-started-with-hello-windows-data-science-vm"></a>Как tooget работу с виртуальной Машины для обработки и анализа данных Windows hello
* Создайте экземпляр выпуска Windows DSVM hello требуемого, перейдя к
  * [DSVM на платформе Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.windows-data-science-vm)
  
  или 
  * [DSVM на платформе Windows Server 2012](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/). 
* Нажмите кнопку hello **получение ИТ ТЕПЕРЬ** кнопки.
* Войдите в toohello ВМ с удаленного рабочего стола с использованием учетных данных hello, указанных при создании hello виртуальной Машины.
* toodiscover и запустите hello инструментах, щелкните hello **запустить** меню.

## <a name="get-started-with-hello-linux-data-science-vm"></a>Приступая к работе с hello ВМ обработки и анализа данных Linux
* Создать экземпляр требуемого hello выпуск Linux DSVM, перейдя по слишком
  * [DSVM на платформе Ubuntu](http://aka.ms/dsvm/ubuntu)

  или

  * [DSVM на платформе OpenLogic CentOS](http://aka.ms/dsvm/centos).

  
* Нажмите кнопку hello **компания** кнопки.
* Войдите в toohello виртуальной Машины из клиента SSH, например Putty или команды SSH, с использованием учетных данных hello, указанных при создании hello виртуальной Машины.
* Введите в командную строку hello, dsvm больше информации.
* Для графического рабочего стола, загрузите hello X2Go клиента для вашей платформы клиента [здесь](http://wiki.x2go.org/doku.php/doc:installation:x2goclient) и следуйте инструкциям hello в документе обработки и анализа данных виртуальной Машины с Linux hello [подготовки hello виртуальная машина Linux данных анализа](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).

## <a name="next-steps"></a>Дальнейшие действия
### <a name="for-hello-windows-data-science-vm"></a>Для виртуальной Машины для обработки и анализа данных Windows hello
* Дополнительные сведения о как toorun определенных инструментальных средств, доступных в версии Windows hello. в разделе [подготовки hello виртуальная машина анализа данных Microsoft](machine-learning-data-science-provision-vm.md) и
* Дополнительные сведения о tooperform различные задачи, необходимые для обработки и анализа данных проекта на ВМ Windows hello. в статье [десять вы можете делать на hello обработки и анализа данных виртуальной машины](machine-learning-data-science-vm-do-ten-things.md).

### <a name="for-hello-linux-data-science-vm"></a>Для обработки и анализа данных виртуальной Машины с Linux hello
* Дополнительные сведения о как toorun определенных инструментальных средств, доступных в версии Linux hello. в разделе [подготовки hello виртуальная машина анализа данных Linux](machine-learning-data-science-linux-dsvm-intro.md).
* Пошаговое руководство показывает, как tooperform несколько науки общих данных задач с hello виртуальных Машин Linux см. в разделе [обработки и анализа данных на hello виртуальная машина анализа данных Linux](machine-learning-data-science-linux-dsvm-walkthrough.md).

