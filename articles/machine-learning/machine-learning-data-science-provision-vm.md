---
title: "hello aaaProvision виртуальная машина анализа данных Microsoft | Документы Microsoft"
description: "Настройка и создание виртуальной машины в Azure для обработки и анализа данных и машинного обучения."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 907a3bdc7e480d05e8e245f5e50d632900fcf471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-microsoft-data-science-virtual-machine"></a>Подготовить hello виртуальная машина анализа данных Microsoft
Виртуальная машина анализа данных Microsoft Hello является образ виртуальной машины (ВМ) Windows Azure предварительно установлен и настроен с ряд популярных средств, которые обычно используются для анализа данных и машинного обучения. Hello инструментах являются:

* Microsoft R Server Developer Edition
* дистрибутив Anaconda Python;
* Записная книжка Jupyter (с ядрами R и Python).
* выпуск Visual Studio Community;
* Power BI Desktop;
* SQL Server 2016 Developer Edition.
* Инструменты машинного обучения и анализа данных
  * [Computational Network Toolkit (CNTK)](https://github.com/Microsoft/CNTK): набор программных средств для глубокого обучения от Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): система быстрого машинного обучения, поддерживающая такие методы, как онлайн-обучение, хэширование, общее сокращение, сокращение, обучение поиску, активное и интерактивное обучение.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): инструмент, предоставляющий быструю и точную реализацию повышенного дерева.
  * [Диска](http://rattle.togaware.com/) (hello аналитические средства R tooLearn легко): это средство, которое делает Приступая к работе с анализа данных и машинного обучения в R, легко анализировать данные на основе графического интерфейса пользователя и моделирование с автоматического генерирования кода R.
  * [mxnet](https://github.com/dmlc/mxnet): платформа глубокого обучения, предназначенная для обеспечения эффективности и гибкости.
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/): программное обеспечение для визуального интеллектуального анализа данных и машинного обучения, написанное на языке Java.
  * [Apache Drill](https://drill.apache.org/): обработчик SQL-запросов без схемы для Hadoop, NoSQL и облачного хранилища.  Поддерживает ODBC и JDBC запрос NoSQL и файлы из стандартных средств бизнес-Аналитики, например PowerBI, Excel, Tableau tooenable интерфейсов.
* Библиотеки R и Python для машинного обучения Azure и других служб Azure
* Git, включая toowork Git Bash с репозитории исходного кода, включая GitHub, Visual Studio Team Services
* Порты Windows для нескольких популярных служебных программ командной строки Linux (включая awk, sed, perl, grep, find, wget, curl и др.), доступные в командной строке. 

Анализ данных включает выполнение следующих задач:

1. поиск, загрузка и предварительная обработка данных;
2. построение и тестирование моделей;
3. Развертывание моделей hello для потребления в интеллектуальных приложений

Специалисты по анализу данных использовать разнообразные средства toocomplete этих задач. Его можно довольно много времени toofind hello соответствующих версий программного обеспечения hello и затем загрузить и установить их. Hello виртуальная машина анализа данных Майкрософт может облегчить эту нагрузку, предоставляя готовые к использованию образ, который можно подготовить в Azure с помощью любых несколько популярных средств предварительно установлен и настроен. 

Виртуальная машина анализа данных Microsoft Hello быстрее заняться analytics проекта. Благодаря этому можно toowork по задачам на различных языках, включая R, Python, SQL и C#. Visual Studio предоставляет toodevelop интегрированной среды разработки и тестирования кода, легко toouse. Hello Azure SDK, включенных в hello ВМ можно toobuild приложений с помощью различных служб на облачная платформа корпорации Майкрософт. 

Плата за программное обеспечение для этого образа виртуальной машины не взимается. Вы платите только за оплаты использования Azure hello какие в зависимости от размера hello hello виртуальной машины, которым вы предоставили. Дополнительные сведения о hello вычислений сборы можно найти в разделе цены на hello hello [виртуальная машина анализа данных](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) страницы. 

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Другие версии hello виртуальная машина анализа данных
Объект [CentOS](machine-learning-data-science-linux-dsvm-intro.md) образ также доступен, со многими hello же средства, как образ Windows hello. Доступен и образ [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md), содержащий множество аналогичных инструментов, а также платформы глубокого обучения.

## <a name="prerequisites"></a>Предварительные требования
Перед созданием виртуальная машина анализа данных Майкрософт, необходимо иметь следующие hello.

* **Подписка Azure**: один, см. в разделе tooobtain [получить бесплатная пробная версия](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Учетная запись хранилища Azure**: один, см. в разделе toocreate [создать учетную запись хранилища Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account). Кроме того учетной записи хранилища hello могут создаваться в рамках процесса hello создания hello виртуальной Машины, если не требуется toouse существующую учетную запись.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Создание виртуальной машины Майкрософт для обработки и анализа данных
Ниже приведены шаги toocreate hello экземпляр hello виртуальная машина анализа данных Microsoft.

1. Перейдите toohello виртуальной машины со списком на [портал Azure](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).
2. Выберите hello **создать** toobe нижней hello уделить мастер, расположенную.![ настроить данные-обработки и анализа vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Hello используются мастером toocreate hello виртуальная машина анализа данных Microsoft требует **входов** для каждого hello **пять шагов** перечислителей hello справа от на рисунке. Ниже приведены hello необходимые входные данные tooconfigure каждого из следующих действий.
   
   1. **Основы**
      
      1. **Имя**— имя создаваемого сервера для обработки и анализа данных.
      2. **Имя пользователя**— идентификатор учетной записи администратора.
      3. **Пароль**— пароль учетной записи администратора.
      4. **Подписки**: при наличии нескольких подписок выберите hello один на какие hello компьютер — toobe создан и включен в счет.
      5. **Группа ресурсов**— вы можете создать новую группу или использовать существующую.
      6. **Расположение**: hello выберите центр обработки данных, наиболее подходящим. Обычно это hello центра обработки данных, большая часть данных, или ближайшее физическое расположение tooyour быстрый доступ к сети.
   2. **Размер**: выберите один из типов сервера hello, соответствует требованиям вашей работы и ограничениями расходов. Дополнительные варианты размера виртуальной машины можно увидеть, щелкнув "Просмотреть все".
   3. **Параметры**:
      
      1. **Тип диска**. Выберите "Премиум", если требуется твердотельный накопитель (SSD), в противном случае выберите "Стандартный".
      2. **Учетная запись хранения**: можно создать новую учетную запись хранилища Azure в подписке или используйте существующую в hello же *расположение* , выбранную на hello **основы** шаг мастера hello.
      3. **Другие параметры**: обычно просто используйте значения по умолчанию hello. В случае, если требуется использование hello tooconsider значения по умолчанию, можно навести hello информационная ссылка для получения справки по определенным полям hello.
   4. **Сводка**. Проверьте, все ли сведения введены правильно.
   5. **Приобретение**: щелкните **купить** toostart hello подготовки. Ссылка предоставляется условия toohello hello транзакции. Hello виртуальной Машины не поддерживает все дополнительная плата за пределами hello вычислений для hello размер сервера, выбранного в hello **размер** шаг. 

> [!NOTE]
> Подготовка Hello займет около 10-20 минут. состояние подготовки hello Hello отображается на hello портал Azure.
> 
> 

## <a name="how-tooaccess-hello-microsoft-data-science-virtual-machine"></a>Как tooaccess hello виртуальная машина анализа данных Microsoft
Один раз hello создания ВМ, вы можете удаленного рабочего стола в нее с помощью hello учетных данных администратора, настроенные в предыдущем hello **основы** раздела. 

После создания и подготовки ВМ, вы являетесь готов toostart, с помощью средств hello, которые устанавливаются и настраиваются на нем. Существуют плиток меню Пуск и значки рабочего стола для многих средств hello. 

## <a name="how-toocreate-a-strong-password-for-jupyter-and-start-hello-notebook-server"></a>Как надежный пароль для Jupyter и начала toocreate hello server записной книжки
По умолчанию блокнота jupyter hello предварительно настроен, но отключена на hello виртуальной Машины, пока не будет задан пароль Jupyter. вызывается для выполнения hello следующую команду в командной строке данных обработки и анализа виртуальной машины или дважды щелкните ярлык на рабочем столе hello мы предоставили hello toocreate надежный пароль для сервера записной книжки Jupyter hello, установленного на компьютере hello  **Задать пароль Jupyter & запуск** из локальной учетной записи администратора виртуальной Машины.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

Следуйте сообщений hello и выбрать надежный пароль при появлении запроса.

Hello предыдущий сценарий создает хэш пароля и в файле конфигурации Jupyter hello, расположенные в хранилище: **C:\ProgramData\jupyter\jupyter_notebook_config.py** под именем параметра hello ***c. NotebookApp.password***.

Hello также включает и выполнении сценария сервера Jupyter hello в фоновом режиме hello. Сервер Jupyter создается при вызове задачи windows в планировщик заданий WIndows hello **Start_IPython_Notebook**.  Вы можете иметь toowait на несколько секунд после установки пароля hello перед открытием записной книжки hello в браузере. В разделе hello ниже раздел **книжке Jupyter** на как tooaccess hello блокнота jupyter. 


## <a name="tools-installed-on-hello-microsoft-data-science-virtual-machine"></a>Средства, которые установлены на hello виртуальная машина анализа данных Microsoft

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Developer Edition
Если вы хотите toouse R для аналитики, hello виртуальной Машины имеет установленного выпуска Microsoft R Server Developer. Microsoft R Server — это широко развертываемая платформа аналитики корпоративного класса на основе R, которая поддерживается, масштабируется и является безопасной. Для поддержки различных статистики большие наборы данных, прогнозирующее моделирование и машинное обучение возможности, R Server поддерживает полный спектр hello аналитики: исследование, анализ, визуализации и моделирования. С помощью и расширение R с открытым кодом, Microsoft R Server полностью совместима со скриптами R, функциями и пакетами CRAN, tooanalyze данные на корпоративном уровне. Оно также устраняет ограничения в памяти hello откройте источник R, добавив параллельной и фрагментированной обработки данных. Это позволяет toorun анализ данных намного больше, чем помещается в оперативной памяти.  Visual Studio Community Edition на hello, виртуальная машина содержит hello средства R для расширения Visual Studio, которая предоставляет полный интегрированной среды разработки для работы с R. Можно также загрузить и использовать других интегрированных средах разработки, например также [RStudio](http://www.rstudio.com). 

### <a name="python"></a>Python
Для разработки на языке Python установлен дистрибутив Anaconda Python версий 2.7 и 3.5. Это распределение содержит hello базовый Python вместе с примерно 300 hello наиболее популярные математические, проектирование и данные пакетов аналитики. Можно использовать средства Python для Visual Studio (PTVS), установленной в Visual Studio 2015 Community edition hello или один из интегрированных средах разработки входит в состав Anaconda как IDLE или Spyder приветствия. Можно запустить одним из них путем поиска на панели поиска hello (**Win** + **S** ключа).

> [!NOTE]
> toopoint hello средства Python для Visual Studio на Anaconda Python 2.7 и 3.5, необходимо toocreate пользовательских средах для каждой версии. Перейдите в Visual Studio 2015 Community Edition hello эти пути в среде tooset слишком**средства** -> **средства Python** -> **среды Python** и нажмите кнопку **+ настраиваемый**. 
> 
> 

Anaconda Python 2.7 устанавливается в папку C:\Anaconda, а Anaconda Python 3.5 — в папку С:\Anaconda\envs\py35. Подробные указания см. в [документации по PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it). 

### <a name="jupyter-notebook"></a>Портативный компьютер Jupyter
Дистрибутив anaconda также имеет записной книжке Jupyter, код tooshare среды и анализа. В сервере Jupyter Notebook предварительно настроены ядра Python 2.7, Python 3.4, Python 3.5 и R. Нет значка на рабочем столе с именем «hello браузера книжке Jupyter toolaunch tooaccess hello записной книжки сервера. Если вы находитесь на hello виртуальной Машине через удаленный рабочий стол, вы можете посетить [https://localhost:9999 /](https://localhost:9999/) tooaccess hello блокнота jupyter при входе в toohello виртуальной Машины.

> [!NOTE]
> При появлении любых предупреждений о сертификатах нажмите кнопку "Продолжить". 
> 
> 

Мы упакованные некоторые примеры записных книжек Python и в среде R. hello Показать записные книжки Jupyter как toowork с Microsoft R Server, SQL Server 2016 R Services (аналитика в базе данных), Python, Microsoft Когнитивных ToolKit (CNTK) для углубленного обучения и другие Azure технологии, когда вы войдете в tooJupyter. После проверки подлинности с использованием пароля hello, созданный на предыдущем шаге книжке Jupyter toohello можно увидеть образцы toohello hello ссылку на домашней странице записной книжки hello. 

### <a name="visual-studio-2015-community-edition"></a>Выпуск Visual Studio Community 2015 
Visual Studio Community edition, установлены на hello виртуальной Машины. Это бесплатная версия hello популярных интегрированной среды разработки Майкрософт, которые можно использовать для оценки, а также для небольших команд. Можно извлечь приветствия, условия лицензирования [здесь](https://www.visualstudio.com/support/legal/mt171547).  Откройте Visual Studio, дважды щелкнув значок рабочего стола hello или hello **запустить** меню. Кроме того, вы можете выполнить поиск программ следующим образом: нажмите клавиши **WIN** + **S** и введите запрос "Visual Studio". Выполнив вход, вы сможете создавать проекты, используя такие языки, как C#, Python, R и node.js. Подключаемые модули также будут установлены, благодаря которым она удобный toowork со службами Azure как каталог данных Azure, Azure HDInsight (Hadoop, Spark) и Озера данных Azure. 

> [!NOTE]
> Может появиться сообщение о том, что период ознакомления истек. Введите учетные данные учетной записи Майкрософт или создайте новый доступ toohello бесплатную учетную запись tooget Visual Studio Community Edition. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>SQL Server 2016 Developer Edition.
Разработчик версии SQL Server 2016 с помощью анализа в базе данных служб R toorun обеспечивается hello виртуальной Машины. Службы R предоставляют платформу для разработки и развертывания аналитических приложений. Можно использовать hello функциональный и эффективный язык R и hello многие пакеты из hello сообщества toocreate моделей и формировать прогнозы для данных SQL Server. Позволяет исключить закрыть toohello аналитические данные, поскольку службы R (в базе данных) интегрировать hello R языка SQL Server. Это позволяет исключить hello затрат и рисков, связанных с перемещением данных.

> [!NOTE]
> выпуск developer Привет SQL Server 2016 может использоваться только для разработки и тестирования в целях. Требуется toorun лицензии его в рабочей среде. 
> 
> 

Доступ к hello SQL server, запустив **SQL Server Management Studio**. Имя виртуальной Машины заполняется значением hello имя сервера. Используйте проверку подлинности Windows, когда в системе как hello администрирования в Windows. Выполнив вход в SQL Server Management Studio, вы можете создавать других пользователей и базы данных, импортировать данные и выполнять запросы SQL. 

Анализ tooenable в базе данных, с помощью Microsoft R, запустите следующую команду в качестве одного hello однократно в среде SQL Server management studio после входа в систему как администратор сервера hello. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace hello %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Таблицы Azure
Несколько средств Azure устанавливаются на hello виртуальной Машины:

* Нет документации по пакету SDK Azure hello tooaccess ярлык на рабочем столе. 
* **AzCopy**: использовать toomove данных из вашей учетной записи хранилища Microsoft Azure. Использование toosee, тип **Azcopy** об использовании командной строки toosee hello. 
* **Обозреватель хранилищ Microsoft Azure**: использовать toobrowse через hello объекты, которые были сохранены в вашей учетной записи хранилища Azure и передача данных tooand из хранилища Azure. Можно ввести **обозреватель хранилищ** в поиск, или найти его на hello tooaccess меню Пуск этого средства. 
* **Adlcopy**: использовать Озера данных tooAzure toomove данных. Использование toosee, тип **adlcopy** из командной строки. 
* **dtui**: использовать toomove tooand данных из Azure Cosmos DB NoSQL базы данных в облаке hello. Введите **dtui** в командной строке. 
* **Шлюз управления данными Майкрософт** позволяет перемещать данные между локальными источниками данных и облаком. Он используется в таких инструментах, как фабрика данных Azure. 
* **Microsoft Azure Powershell**: это средство используется tooadminister ресурсам Azure в hello на ВМ также установлен язык сценариев Powershell. 

### <a name="power-bi"></a>Power BI
toohelp создания панелей мониторинга и значительные визуализации hello **Power BI Desktop** установлен. Использовать эти средства toopull данные из различных источников, tooauthor вашей панели мониторинга и отчеты и toopublish их toohello облака. Сведения см. в разделе hello [Power BI](http://powerbi.microsoft.com) сайта. Power BI desktop можно найти в меню Пуск hello. 

> [!NOTE]
> Необходимо tooaccess учетной записи Office 365 Power BI. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>Дополнительные средства разработки Майкрософт
Hello [ **Microsoft Web Platform Installer** ](https://www.microsoft.com/web/downloads/platform.aspx) можно использовать toodiscover и загрузить другие средства разработки Майкрософт. Имеется также имеется средство toohello ярлык на рабочем столе hello виртуальная машина анализа данных Microsoft.  

## <a name="important-directories-on-hello-vm"></a>Важные каталогов на hello виртуальной Машины
| Элемент | Каталог |
| --- | --- |
| Конфигурации сервера записной книжки Jupyter |C:\ProgramData\jupyter |
| Корневой каталог примеров записных книжек Jupyter |c:\dsvm\notebooks |
| Другие примеры |c:\dsvm\samples |
| Anaconda (по умолчанию: Python 2.7) |c:\Anaconda |
| Среда Anaconda Python 3.5 |c:\Anaconda\envs\py35 |
| Каталог экземпляров R Server (изолированный) (экземпляр R по умолчанию на основе R3.2.2) |C:\Program Files\Microsoft SQL Server\130\R_SERVER |
| Каталог экземпляров R Server (в базе данных) (R3.2.2) |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES |
| Каталог экземпляров Microsoft R Open (R3.3.1) |C:\Program Files\Microsoft\MRO-3.3.1 |
| Прочие инструменты |c:\dsvm\tools |

> [!NOTE]
> Экземпляры hello создана виртуальная машина анализа данных Майкрософт перед 1.5.0 (до 3 сентября 2016 г.) используется структура каталогов немного отличается от указанного в предшествующей таблице hello. 
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Ниже приведены некоторые далее шаги toocontinue обучения и исследования. 

* Изучите hello различные инструменты обработки и анализа данных на hello обработки и анализа данных виртуальной Машины, нажав кнопку hello «Пуск» и извлечение hello средств, перечисленных в меню "hello".
* Перейдите в слишком**C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** для примеров с помощью библиотеки RevoScaleR hello в R, поддерживающий анализа данных в масштабе предприятия.  
* Прочитать статью hello: [10 вещей, которые можно выполнять на hello обработки и анализа данных виртуальной машины](http://aka.ms/dsvmtenthings)
* Узнайте, как toobuild tooend аналитические решения систематически с помощью hello [процесс обработки и анализа данных для команды](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).
* Посетите hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com) для analytics обучения и данные машина образцы hello, используйте набор аналитики Cortana. Мы также предоставлен значка в hello **запустить** меню и на рабочем столе hello галереи toothis hello виртуальной машины.

