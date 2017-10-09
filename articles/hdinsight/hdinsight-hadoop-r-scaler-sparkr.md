---
title: "aaaUse ScaleR и SparkR с Azure HDInsight | Документы Microsoft"
description: "Использование ScaleR и SparkR с R Server и HDInsight"
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="0e467-103">Совместное использование ScaleR и SparkR в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0e467-103">Combine ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="0e467-104">В этой статье показано, как toopredict "черный" прибытия задержки с помощью **ScaleR** модель логистической регрессии на основе данных на задержки рейсов и погоды соединить с **SparkR**.</span><span class="sxs-lookup"><span data-stu-id="0e467-104">This article shows how toopredict flight arrival delays using a **ScaleR** logistic regression model from data on flight delays and weather joined with **SparkR**.</span></span> <span data-ttu-id="0e467-105">Этот сценарий показывает возможности hello ScaleR для работы с данными на Spark, используемых с Microsoft R Server для аналитики.</span><span class="sxs-lookup"><span data-stu-id="0e467-105">This scenario demonstrates hello capabilities of ScaleR for data manipulation on Spark used with Microsoft R Server for analytics.</span></span> <span data-ttu-id="0e467-106">Hello сочетание этих технологий позволяет новейшим возможностям tooapply hello в распределенной обработки.</span><span class="sxs-lookup"><span data-stu-id="0e467-106">hello combination of these technologies enables you tooapply hello latest capabilities in distributed processing.</span></span>

<span data-ttu-id="0e467-107">Хотя оба пакета работают поверх механизма выполнения Spark Hadoop, совместное использование данных в памяти для них заблокировано, так как для каждого из них требуются отдельные сеансы Spark.</span><span class="sxs-lookup"><span data-stu-id="0e467-107">Although both packages run on Hadoop’s Spark execution engine, they are blocked from in-memory data sharing as they each require their own respective Spark sessions.</span></span> <span data-ttu-id="0e467-108">Пока эта проблема решена в последующих версиях сервера R, hello достаточно toomaintain неперекрывающиеся Spark сеансы и tooexchange данных с помощью промежуточных файлов.</span><span class="sxs-lookup"><span data-stu-id="0e467-108">Until this issue is addressed in an upcoming version of R Server, hello workaround is toomaintain non-overlapping Spark sessions, and tooexchange data through intermediate files.</span></span> <span data-ttu-id="0e467-109">Эти инструкции Hello показывают, что эти требования являются просто tooachieve.</span><span class="sxs-lookup"><span data-stu-id="0e467-109">hello instructions here show that these requirements are straightforward tooachieve.</span></span>

<span data-ttu-id="0e467-110">Мы используем пример здесь изначально совместно в поговорим в 2016 Стратификации Inchiosa Марио и Roni Burd, также доступна через веб-семинар hello [построение масштабируемой платформе обработки и анализа данных с помощью R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). пример hello использует SparkR toojoin hello хорошо известных авиакомпании прибытия задержки набор данных с данных о погоде в аэропортах отправления и прибытия.</span><span class="sxs-lookup"><span data-stu-id="0e467-110">We use an example here initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd that is also available through hello webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). hello example uses SparkR toojoin hello well-known airlines arrival delay data set with weather data at departure and arrival airports.</span></span> <span data-ttu-id="0e467-111">объединить данные Hello затем используется в качестве входного tooa ScaleR логистической регрессии модели для прогнозирования задержки авиарейсов прибытия.</span><span class="sxs-lookup"><span data-stu-id="0e467-111">hello data joined is then used as input tooa ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="0e467-112">Hello мы пошаговое описание кода изначально был записан для сервера R, работающего на Spark в кластер HDInsight в Azure.</span><span class="sxs-lookup"><span data-stu-id="0e467-112">hello code we walkthrough was originally written for R Server running on Spark in an HDInsight cluster on Azure.</span></span> <span data-ttu-id="0e467-113">Но понятие hello смешивание hello использование SparkR и ScaleR в одном скрипте также допускается в контексте hello локальных сред.</span><span class="sxs-lookup"><span data-stu-id="0e467-113">But hello concept of mixing hello use of SparkR and ScaleR in one script is also valid in hello context of on-premises environments.</span></span> <span data-ttu-id="0e467-114">В следующих hello мы предположить промежуточный уровень знаний об hello и удалите [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) библиотеки R Server.</span><span class="sxs-lookup"><span data-stu-id="0e467-114">In hello following, we presume an intermediate level of knowledge of R and R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library of R Server.</span></span> <span data-ttu-id="0e467-115">В процессе рассмотрения сценария также приводятся общие сведения об использовании [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html).</span><span class="sxs-lookup"><span data-stu-id="0e467-115">We also introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) while walking through this scenario.</span></span>

## <a name="hello-airline-and-weather-datasets"></a><span data-ttu-id="0e467-116">наборы данных авиакомпании и погоды Hello</span><span class="sxs-lookup"><span data-stu-id="0e467-116">hello airline and weather datasets</span></span>

<span data-ttu-id="0e467-117">Hello **AirOnTime08to12CSV** авиакомпании открытый набор данных содержит сведения о полете прибытия и отправления сведения для всех коммерческих рейсов в США, hello из tooDecember 1987 октября 2012 г.</span><span class="sxs-lookup"><span data-stu-id="0e467-117">hello **AirOnTime08to12CSV** airlines public dataset contains information on flight arrival and departure details for all commercial flights within hello USA, from October 1987 tooDecember 2012.</span></span> <span data-ttu-id="0e467-118">Это большой набор данных, содержащий около 150 миллионов записей.</span><span class="sxs-lookup"><span data-stu-id="0e467-118">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="0e467-119">Примерный размер составляет 4 ГБ в не распакованном виде.</span><span class="sxs-lookup"><span data-stu-id="0e467-119">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="0e467-120">Он доступен из hello [архивы правительство США](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span><span class="sxs-lookup"><span data-stu-id="0e467-120">It is available from hello [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span></span> <span data-ttu-id="0e467-121">Более простым способом может быть указан как ZIP-файл (AirOnTimeCSV.zip), содержащий набор 303 отдельные ежемесячные CSV-файлы из hello [Revolution Analytics набора данных репозитория](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span><span class="sxs-lookup"><span data-stu-id="0e467-121">More conveniently, it is available as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from hello [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="0e467-122">toosee hello влияние погоды на задержки рейсов, заключаются в данных о погоде hello на каждом аэропортах hello.</span><span class="sxs-lookup"><span data-stu-id="0e467-122">toosee hello effects of weather on flight delays, we also need hello weather data at each of hello airports.</span></span> <span data-ttu-id="0e467-123">Эти данные можно загрузить в виде ZIP-файлов в исходном виде по месяцам, начиная от hello [репозиторий National Oceanic и атмосферные администрирования](http://www.ncdc.noaa.gov/orders/qclcd/).</span><span class="sxs-lookup"><span data-stu-id="0e467-123">This data can be downloaded as zip files in raw form, by month, from hello [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="0e467-124">Hello целях в этом примере по запросу данных о погоде из мая 2007 г. — декабрь 2012 г. и использовать hello почасовой файлы данных внутри каждого 68 ежемесячные zips hello.</span><span class="sxs-lookup"><span data-stu-id="0e467-124">For hello purposes of this example, we pull weather data from May 2007 – December 2012 and used hello hourly data files within each of hello 68 monthly zips.</span></span> <span data-ttu-id="0e467-125">Hello ежемесячные ZIP-файлы также содержат сопоставления (YYYYMMstation.txt) между станции погоды hello ID (WBAN), аэропорт hello, что он связан с (CallSign) и hello аэропорта смещение часового пояса от времени UTC (часовой пояс).</span><span class="sxs-lookup"><span data-stu-id="0e467-125">hello monthly zip files also contain a mapping (YYYYMMstation.txt) between hello weather station ID (WBAN), hello airport that it is associated with (CallSign), and hello airport’s time zone offset from UTC (TimeZone).</span></span> <span data-ttu-id="0e467-126">Все эти сведения необходимо при соединении с данными задержки и погоды авиакомпании hello.</span><span class="sxs-lookup"><span data-stu-id="0e467-126">All of this information is needed when joining with hello airline delay and weather data.</span></span>

## <a name="setting-up-hello-spark-environment"></a><span data-ttu-id="0e467-127">Настройка среды Spark hello</span><span class="sxs-lookup"><span data-stu-id="0e467-127">Setting up hello Spark environment</span></span>

<span data-ttu-id="0e467-128">Hello первым шагом является tooset hello Spark среды.</span><span class="sxs-lookup"><span data-stu-id="0e467-128">hello first step is tooset up hello Spark environment.</span></span> <span data-ttu-id="0e467-129">Начнем с указывающим toohello каталог, содержащий каталоги нашей входных данных, контекст вычислений Spark и создания функции ведения журнала консоли toohello информационное ведения журнала:</span><span class="sxs-lookup"><span data-stu-id="0e467-129">We begin by pointing toohello directory that contains our input data directories, creating a Spark compute context, and creating a logging function for informational logging toohello console:</span></span>

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

<span data-ttu-id="0e467-130">Далее добавим путь поиска «Spark_Home» toohello R-пакетов, чтобы мы могли использовать SparkR и инициализации сеанса SparkR:</span><span class="sxs-lookup"><span data-stu-id="0e467-130">Next we add “Spark_Home” toohello search path for R packages so that we can use SparkR, and initialize a SparkR session:</span></span>

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a><span data-ttu-id="0e467-131">Подготовка данных о погоде hello</span><span class="sxs-lookup"><span data-stu-id="0e467-131">Preparing hello weather data</span></span>

<span data-ttu-id="0e467-132">tooprepare hello погоды мы подмножества его toohello столбцы, необходимые для моделирования:</span><span class="sxs-lookup"><span data-stu-id="0e467-132">tooprepare hello weather data, we subset it toohello columns needed for modeling:</span></span> 

- <span data-ttu-id="0e467-133">"Visibility"</span><span class="sxs-lookup"><span data-stu-id="0e467-133">"Visibility"</span></span>
- <span data-ttu-id="0e467-134">"DryBulbCelsius"</span><span class="sxs-lookup"><span data-stu-id="0e467-134">"DryBulbCelsius"</span></span>
- <span data-ttu-id="0e467-135">"DewPointCelsius"</span><span class="sxs-lookup"><span data-stu-id="0e467-135">"DewPointCelsius"</span></span>
- <span data-ttu-id="0e467-136">"RelativeHumidity"</span><span class="sxs-lookup"><span data-stu-id="0e467-136">"RelativeHumidity"</span></span>
- <span data-ttu-id="0e467-137">"WindSpeed"</span><span class="sxs-lookup"><span data-stu-id="0e467-137">"WindSpeed"</span></span>
- <span data-ttu-id="0e467-138">"Altimeter"</span><span class="sxs-lookup"><span data-stu-id="0e467-138">"Altimeter"</span></span>

<span data-ttu-id="0e467-139">Затем мы добавьте код аэропорта, связанный с станции погоды hello и преобразуйте hello измерений из tooUTC местное время.</span><span class="sxs-lookup"><span data-stu-id="0e467-139">Then we add an airport code associated with hello weather station and convert hello measurements from local time tooUTC.</span></span>

<span data-ttu-id="0e467-140">Мы начнем с создания файла toomap hello погоды станции (WBAN) сведения о tooan аэропорт кода.</span><span class="sxs-lookup"><span data-stu-id="0e467-140">We begin by creating a file toomap hello weather station (WBAN) info tooan airport code.</span></span> <span data-ttu-id="0e467-141">Эта связь удалось получить из файла сопоставления hello, входящий в состав данных о погоде hello.</span><span class="sxs-lookup"><span data-stu-id="0e467-141">We could get this correlation from hello mapping file included with hello weather data.</span></span> <span data-ttu-id="0e467-142">Путем сопоставления hello *CallSign* (например, LAX) поля в файле данных погоды hello слишком*источника* данных авиакомпании hello.</span><span class="sxs-lookup"><span data-stu-id="0e467-142">By mapping hello *CallSign* (for example, LAX) field in hello weather data file too*Origin* in hello airline data.</span></span> <span data-ttu-id="0e467-143">Тем не менее, мы произошедшего toohave другое сопоставление с стороны, сопоставляющий *WBAN* слишком*AirportID* (например, 12892 LAX) и включает *часовой пояс* , были сохранены tooa CSV-файл с именем «wban к аэропорт идентификатор tz. CSV», можно использовать.</span><span class="sxs-lookup"><span data-stu-id="0e467-143">However, we just happened toohave another mapping on hand that maps *WBAN* too*AirportID* (for example, 12892 for LAX) and includes *TimeZone* that has been saved tooa CSV file called “wban-to-airport-id-tz.CSV” that we can use.</span></span> <span data-ttu-id="0e467-144">Например:</span><span class="sxs-lookup"><span data-stu-id="0e467-144">For example:</span></span>

| <span data-ttu-id="0e467-145">AirportID</span><span class="sxs-lookup"><span data-stu-id="0e467-145">AirportID</span></span> | <span data-ttu-id="0e467-146">WBAN</span><span class="sxs-lookup"><span data-stu-id="0e467-146">WBAN</span></span> | <span data-ttu-id="0e467-147">TimeZone</span><span class="sxs-lookup"><span data-stu-id="0e467-147">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="0e467-148">10685</span><span class="sxs-lookup"><span data-stu-id="0e467-148">10685</span></span> | <span data-ttu-id="0e467-149">54831</span><span class="sxs-lookup"><span data-stu-id="0e467-149">54831</span></span> | <span data-ttu-id="0e467-150">-6</span><span class="sxs-lookup"><span data-stu-id="0e467-150">-6</span></span>
| <span data-ttu-id="0e467-151">14871</span><span class="sxs-lookup"><span data-stu-id="0e467-151">14871</span></span> | <span data-ttu-id="0e467-152">24232</span><span class="sxs-lookup"><span data-stu-id="0e467-152">24232</span></span> | <span data-ttu-id="0e467-153">–8</span><span class="sxs-lookup"><span data-stu-id="0e467-153">-8</span></span>
| <span data-ttu-id="0e467-154">..</span><span class="sxs-lookup"><span data-stu-id="0e467-154">..</span></span> | <span data-ttu-id="0e467-155">..</span><span class="sxs-lookup"><span data-stu-id="0e467-155">..</span></span> | <span data-ttu-id="0e467-156">..</span><span class="sxs-lookup"><span data-stu-id="0e467-156">..</span></span>

<span data-ttu-id="0e467-157">Следующий код считывает каждый hello почасовой погоды необработанных данных Hello файлам подмножеств toohello столбцы, объединяет файл сопоставления станции погоды hello, настраивает hello время tooUTC измерения даты и затем записывает новую версию файла hello:</span><span class="sxs-lookup"><span data-stu-id="0e467-157">hello following code reads each of hello hourly raw weather data files, subsets toohello columns we need, merges hello weather station mapping file, adjusts hello date times of measurements tooUTC, and then writes out a new version of hello file:</span></span>

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a><span data-ttu-id="0e467-158">Импорт hello авиакомпании и погоды данных tooSpark блоки данных</span><span class="sxs-lookup"><span data-stu-id="0e467-158">Importing hello airline and weather data tooSpark DataFrames</span></span>

<span data-ttu-id="0e467-159">Теперь мы используем hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) функции hello tooimport погоды и авиакомпании tooSpark данных блоки данных.</span><span class="sxs-lookup"><span data-stu-id="0e467-159">Now we use hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function tooimport hello weather and airline data tooSpark DataFrames.</span></span> <span data-ttu-id="0e467-160">Это функция отложенного выполнения, как и многие другие методы Spark. Это означает, что они находятся в очереди на выполнение, но выполняются только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="0e467-160">This function, like many other Spark methods, are executed lazily, meaning that they are queued for execution but not executed until required.</span></span>

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="0e467-161">Фильтрация и преобразование данных</span><span class="sxs-lookup"><span data-stu-id="0e467-161">Data cleansing and transformation</span></span>

<span data-ttu-id="0e467-162">Теперь нам нужно Очистка некоторых данных авиакомпании hello импортированные toorename столбцов.</span><span class="sxs-lookup"><span data-stu-id="0e467-162">Next we do some cleanup on hello airline data we’ve imported toorename columns.</span></span> <span data-ttu-id="0e467-163">Мы только хранить необходимые переменные hello и округление время запланированного отправления вниз toohello ближайшего tooenable час, объединение с последней погоды hello в отличие:</span><span class="sxs-lookup"><span data-stu-id="0e467-163">We only keep hello variables needed, and round scheduled departure times down toohello nearest hour tooenable merging with hello latest weather data at departure:</span></span>

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

<span data-ttu-id="0e467-164">Теперь мы выполнения схожих операций в данных о погоде hello:</span><span class="sxs-lookup"><span data-stu-id="0e467-164">Now we perform similar operations on hello weather data:</span></span>

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a><span data-ttu-id="0e467-165">Соединение данных погоды и авиакомпании hello</span><span class="sxs-lookup"><span data-stu-id="0e467-165">Joining hello weather and airline data</span></span>

<span data-ttu-id="0e467-166">Теперь мы используем hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) функции toodo левое внешнее соединение hello авиакомпании и погоды данных с выхода AirportID и datetime.</span><span class="sxs-lookup"><span data-stu-id="0e467-166">We now use hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function toodo a left outer join of hello airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="0e467-167">внешнее соединение Hello позволяет нам tooretain записи всех данных авиакомпании hello, даже если нет соответствия данных погоды.</span><span class="sxs-lookup"><span data-stu-id="0e467-167">hello outer join allows us tooretain all hello airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="0e467-168">Соединения hello мы удалить некоторые избыточные столбцы и переименовать hello сохраняются tooremove hello входящих кадр данных префикс столбцов представленные hello соединения.</span><span class="sxs-lookup"><span data-stu-id="0e467-168">Following hello join, we remove some redundant columns, and rename hello kept columns tooremove hello incoming DataFrame prefix introduced by hello join.</span></span>

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

<span data-ttu-id="0e467-169">Аналогичным образом мы соединения hello погоды и авиакомпании данные на основании прибытия AirportID и даты-времени:</span><span class="sxs-lookup"><span data-stu-id="0e467-169">In a similar fashion, we join hello weather and airline data based on arrival AirportID and datetime:</span></span>

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a><span data-ttu-id="0e467-170">Сохранить результаты tooCSV для обмена с ScaleR</span><span class="sxs-lookup"><span data-stu-id="0e467-170">Save results tooCSV for exchange with ScaleR</span></span>

<span data-ttu-id="0e467-171">Мы должны toodo с SparkR соединения hello, которая завершается.</span><span class="sxs-lookup"><span data-stu-id="0e467-171">That completes hello joins we need toodo with SparkR.</span></span> <span data-ttu-id="0e467-172">Мы сохранять данные hello hello последний кадр данных Spark «joinedDF5» tooa CSV для ввода tooScaleR и закрыть сеанс SparkR hello.</span><span class="sxs-lookup"><span data-stu-id="0e467-172">We save hello data from hello final Spark DataFrame “joinedDF5” tooa CSV for input tooScaleR and then close out hello SparkR session.</span></span> <span data-ttu-id="0e467-173">Нам явно установить SparkR toosave hello результирующих CSV в 80 разные разделы tooenable достаточно параллелизма во время обработки ScaleR:</span><span class="sxs-lookup"><span data-stu-id="0e467-173">We explicitly tell SparkR toosave hello resultant CSV in 80 separate partitions tooenable sufficient parallelism in ScaleR processing:</span></span>

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a><span data-ttu-id="0e467-174">Импорт tooXDF для использования ScaleR</span><span class="sxs-lookup"><span data-stu-id="0e467-174">Import tooXDF for use by ScaleR</span></span>

<span data-ttu-id="0e467-175">Мы могли бы использовать hello CSV-файл авиакомпании присоединены к домену и данных о погоде как-для моделирования из источника данных ScaleR текста.</span><span class="sxs-lookup"><span data-stu-id="0e467-175">We could use hello CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source.</span></span> <span data-ttu-id="0e467-176">Но мы его tooXDF сначала импортировать, так как она является более эффективным, при выполнении нескольких операций в наборе данных hello:</span><span class="sxs-lookup"><span data-stu-id="0e467-176">But we import it tooXDF first, since it is more efficient when running multiple operations on hello dataset:</span></span>

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="0e467-177">Разделение данных на наборы для обучения и тестирования</span><span class="sxs-lookup"><span data-stu-id="0e467-177">Splitting data for training and test</span></span>

<span data-ttu-id="0e467-178">Мы используем toosplit rxDataStep hello 2012 данных для тестирования и сохранить hello rest для обучения:</span><span class="sxs-lookup"><span data-stu-id="0e467-178">We use rxDataStep toosplit out hello 2012 data for testing and keep hello rest for training:</span></span>

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="0e467-179">Обучение и тестирование модели логистической регрессии</span><span class="sxs-lookup"><span data-stu-id="0e467-179">Train and test a logistic regression model</span></span>

<span data-ttu-id="0e467-180">Теперь мы все готово toobuild модели.</span><span class="sxs-lookup"><span data-stu-id="0e467-180">Now we are ready toobuild a model.</span></span> <span data-ttu-id="0e467-181">toosee hello влияние данных о погоде на задержку времени прибытия hello, мы используем подпрограммы ScaleR логистической регрессии.</span><span class="sxs-lookup"><span data-stu-id="0e467-181">toosee hello influence of weather data on delay in hello arrival time, we use ScaleR’s logistic regression routine.</span></span> <span data-ttu-id="0e467-182">Мы используем его toomodel ли погоды hello в аэропортах отправления и прибытия hello влияют прибытия задержкой более 15 минут:</span><span class="sxs-lookup"><span data-stu-id="0e467-182">We use it toomodel whether an arrival delay of greater than 15 minutes is influenced by hello weather at hello departure and arrival airports:</span></span>

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

<span data-ttu-id="0e467-183">Теперь давайте посмотрим, как она на hello тестовые данные, некоторые прогнозы и оценив ROC и AUC.</span><span class="sxs-lookup"><span data-stu-id="0e467-183">Now let’s see how it does on hello test data by making some predictions and looking at ROC and AUC.</span></span>

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a><span data-ttu-id="0e467-184">Альтернативное применение модели</span><span class="sxs-lookup"><span data-stu-id="0e467-184">Scoring elsewhere</span></span>

<span data-ttu-id="0e467-185">Hello модели также можно использовать для оценки данных на другой платформе.</span><span class="sxs-lookup"><span data-stu-id="0e467-185">We can also use hello model for scoring data on another platform.</span></span> <span data-ttu-id="0e467-186">Путем его сохранения файла tooan служб удаленных рабочих СТОЛОВ и передаче и импорте назначения оценки среду, такую как SQL Server R Services, служб удаленных рабочих СТОЛОВ.</span><span class="sxs-lookup"><span data-stu-id="0e467-186">By saving it tooan RDS file and then transferring and importing that RDS into a destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="0e467-187">Это важные tooensure, уровни коэффициент hello toobe данных hello оцененных соответствуют на какие hello модели был создан.</span><span class="sxs-lookup"><span data-stu-id="0e467-187">It is important tooensure that hello factor levels of hello data toobe scored match those on which hello model was built.</span></span> <span data-ttu-id="0e467-188">Что соответствия может осуществляться путем извлечения, и сохранения информации о столбце hello, связанные с hello моделирование данных с помощью элемента ScaleR `rxCreateColInfo()` функции, а затем применяет этот источник столбца сведения toohello входных данных для прогноза.</span><span class="sxs-lookup"><span data-stu-id="0e467-188">That match can be achieved by extracting and saving hello column infomation associated with hello modeling data via ScaleR’s `rxCreateColInfo()` function and then applying that column information toohello input data source for prediction.</span></span> <span data-ttu-id="0e467-189">В следующих hello мы сохранить несколько строк из набора тестов hello извлечения и использовать сведения о столбце hello из этого примера в сценарии прогнозирования hello:</span><span class="sxs-lookup"><span data-stu-id="0e467-189">In hello following we save a few rows of hello test dataset and extract and use hello column information from this sample in hello prediction script:</span></span>

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a><span data-ttu-id="0e467-190">Сводка</span><span class="sxs-lookup"><span data-stu-id="0e467-190">Summary</span></span>

<span data-ttu-id="0e467-191">В этой статье было показано, как и при возможности toocombine использование SparkR для работы с данными с ScaleR по разработке модели в Hadoop Spark.</span><span class="sxs-lookup"><span data-stu-id="0e467-191">In this article, we’ve shown how it’s possible toocombine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark.</span></span> <span data-ttu-id="0e467-192">Этот сценарий требует создания нескольких сеансов Spark, использования одновременно только одного сеанса и обмена данными посредством CSV-файлов.</span><span class="sxs-lookup"><span data-stu-id="0e467-192">This scenario requires that you maintain separate Spark sessions, only running one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="0e467-193">При всей своей простоте этот процесс станет еще проще в предстоящем выпуске R Server, в котором SparkR и ScaleR смогут совместно использовать сеансы и кадры данных Spark.</span><span class="sxs-lookup"><span data-stu-id="0e467-193">Although straightforward, this process should be even easier in an upcoming R Server release, when SparkR and ScaleR can share a Spark session and so share Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="0e467-194">Дальнейшие действия и дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="0e467-194">Next steps and more information</span></span>

- <span data-ttu-id="0e467-195">Дополнительные сведения об использовании сервера R в Spark. в разделе hello [руководство Приступая к работе в сети MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span><span class="sxs-lookup"><span data-stu-id="0e467-195">For more information on use of R Server on Spark, see hello [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="0e467-196">Общие сведения о сервере R см. в разделе hello [Приступая к работе с R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) статьи.</span><span class="sxs-lookup"><span data-stu-id="0e467-196">For general information on R Server, see hello [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="0e467-197">Сведения об R Server в HDInsight см. в статьях [Основные сведения об R Server и возможностях открытого кода R в HDInsight](hdinsight-hadoop-r-server-overview.md) и [Приступая к работе с R Server в HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0e467-197">For information on R Server on HDInsight, see [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) and [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span>

<span data-ttu-id="0e467-198">Дополнительные сведения об использовании SparkR см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="0e467-198">For more information on use of SparkR, see:</span></span>

- <span data-ttu-id="0e467-199">[SparkR (R on Spark)](https://spark.apache.org/docs/2.1.0/sparkr.html) (SparkR (язык R в Spark))</span><span class="sxs-lookup"><span data-stu-id="0e467-199">[Apache SparkR document](https://spark.apache.org/docs/2.1.0/sparkr.html)</span></span>

- <span data-ttu-id="0e467-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) (Общие сведения о SparkR) на сайте Databricks</span><span class="sxs-lookup"><span data-stu-id="0e467-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
