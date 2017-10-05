---
title: "Использование ScaleR и SparkR с Azure HDInsight | Документация Майкрософт"
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
ms.openlocfilehash: 29733f6f6b725dd4735219ed221431805558a5e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="c30db-103">Совместное использование ScaleR и SparkR в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c30db-103">Combine ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="c30db-104">В этой статье показано, как прогнозировать задержки прибытия авиарейсов с помощью модели логистической регрессии **ScaleR** на основе данных по задержкам авиарейсов и погодных данных, объединенных с помощью **SparkR**.</span><span class="sxs-lookup"><span data-stu-id="c30db-104">This article shows how to predict flight arrival delays using a **ScaleR** logistic regression model from data on flight delays and weather joined with **SparkR**.</span></span> <span data-ttu-id="c30db-105">В этом сценарии демонстрируются возможности ScaleR для работы с данными в Spark и Microsoft R Server для выполнения задач аналитики.</span><span class="sxs-lookup"><span data-stu-id="c30db-105">This scenario demonstrates the capabilities of ScaleR for data manipulation on Spark used with Microsoft R Server for analytics.</span></span> <span data-ttu-id="c30db-106">Сочетание этих технологий позволяет применять новейшие возможности распределенной обработки.</span><span class="sxs-lookup"><span data-stu-id="c30db-106">The combination of these technologies enables you to apply the latest capabilities in distributed processing.</span></span>

<span data-ttu-id="c30db-107">Хотя оба пакета работают поверх механизма выполнения Spark Hadoop, совместное использование данных в памяти для них заблокировано, так как для каждого из них требуются отдельные сеансы Spark.</span><span class="sxs-lookup"><span data-stu-id="c30db-107">Although both packages run on Hadoop’s Spark execution engine, they are blocked from in-memory data sharing as they each require their own respective Spark sessions.</span></span> <span data-ttu-id="c30db-108">Это будет исправлено в последующих версиях R Server, а пока временным решением является поддержание не перекрывающихся сеансов Spark и обмен данными с помощью промежуточных файлов.</span><span class="sxs-lookup"><span data-stu-id="c30db-108">Until this issue is addressed in an upcoming version of R Server, the workaround is to maintain non-overlapping Spark sessions, and to exchange data through intermediate files.</span></span> <span data-ttu-id="c30db-109">В приведенных в этой статье инструкциях показано, что обеспечить выполнение этих требований достаточно просто.</span><span class="sxs-lookup"><span data-stu-id="c30db-109">The instructions here show that these requirements are straightforward to achieve.</span></span>

<span data-ttu-id="c30db-110">Мы будем использовать пример, изначально озвученный в докладе Марио Инчиоза (Mario Inchiosa) и Рони Берда (Roni Burd) на конференции Strata 2016, который доступен в виде вебинара [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio) (Создание масштабируемой платформы анализа и обработки данных на основе R). В примере SparkR используется для объединения набора данных по задержкам прибытия рейсов известных авиакомпаний с погодными данными в аэропортах отправления и прибытия.</span><span class="sxs-lookup"><span data-stu-id="c30db-110">We use an example here initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd that is also available through the webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). The example uses SparkR to join the well-known airlines arrival delay data set with weather data at departure and arrival airports.</span></span> <span data-ttu-id="c30db-111">Объединенные данные затем используются в качестве входных для модели логистической регрессии ScaleR, которая служит для прогнозирования задержки прибытия.</span><span class="sxs-lookup"><span data-stu-id="c30db-111">The data joined is then used as input to a ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="c30db-112">Код, который будет использоваться в этом руководстве, первоначально был написан для R Server под управлением Spark в кластере HDInsight в Azure.</span><span class="sxs-lookup"><span data-stu-id="c30db-112">The code we walkthrough was originally written for R Server running on Spark in an HDInsight cluster on Azure.</span></span> <span data-ttu-id="c30db-113">Однако понятие совместного использования SparkR и ScaleR в одном скрипте в равной степени применимо к локальным средам.</span><span class="sxs-lookup"><span data-stu-id="c30db-113">But the concept of mixing the use of SparkR and ScaleR in one script is also valid in the context of on-premises environments.</span></span> <span data-ttu-id="c30db-114">Здесь предполагается средний уровень знания языка R и библиотеки [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) сервера R Server.</span><span class="sxs-lookup"><span data-stu-id="c30db-114">In the following, we presume an intermediate level of knowledge of R and R the [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library of R Server.</span></span> <span data-ttu-id="c30db-115">В процессе рассмотрения сценария также приводятся общие сведения об использовании [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html).</span><span class="sxs-lookup"><span data-stu-id="c30db-115">We also introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) while walking through this scenario.</span></span>

## <a name="the-airline-and-weather-datasets"></a><span data-ttu-id="c30db-116">Наборы данных об авиакомпаниях и погоде</span><span class="sxs-lookup"><span data-stu-id="c30db-116">The airline and weather datasets</span></span>

<span data-ttu-id="c30db-117">Открытый набор данных об авиакомпаниях **AirOnTime08to12CSV** содержит сведения о прибытии и отправлении всех коммерческих авиарейсов в США с октября 1987 г. по декабрь 2012 г.</span><span class="sxs-lookup"><span data-stu-id="c30db-117">The **AirOnTime08to12CSV** airlines public dataset contains information on flight arrival and departure details for all commercial flights within the USA, from October 1987 to December 2012.</span></span> <span data-ttu-id="c30db-118">Это большой набор данных, содержащий около 150 миллионов записей.</span><span class="sxs-lookup"><span data-stu-id="c30db-118">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="c30db-119">Примерный размер составляет 4 ГБ в не распакованном виде.</span><span class="sxs-lookup"><span data-stu-id="c30db-119">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="c30db-120">Он доступен в [архиве правительства США](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span><span class="sxs-lookup"><span data-stu-id="c30db-120">It is available from the [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span></span> <span data-ttu-id="c30db-121">Кроме того, он доступен в виде ZIP-файла (AirOnTimeCSV.zip), содержащего набор из 303 отдельных ежемесячных CSV-файлов из [репозитория Revolution Analytics](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/).</span><span class="sxs-lookup"><span data-stu-id="c30db-121">More conveniently, it is available as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from the [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="c30db-122">Чтобы увидеть влияние погоды на задержки авиарейсов, также требуются данные по погоде в каждом из аэропортов.</span><span class="sxs-lookup"><span data-stu-id="c30db-122">To see the effects of weather on flight delays, we also need the weather data at each of the airports.</span></span> <span data-ttu-id="c30db-123">Их можно скачать как ZIP-файлы в необработанном виде по месяцам из [репозитория Национального управления океанических и атмосферных исследований](http://www.ncdc.noaa.gov/orders/qclcd/).</span><span class="sxs-lookup"><span data-stu-id="c30db-123">This data can be downloaded as zip files in raw form, by month, from the [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="c30db-124">Для этого примера мы возьмем данные по погоде за период с мая 2007 г. по декабрь 2012 г. и воспользуемся почасовыми файлами данных каждого из 68 ежемесячных ZIP-архивов.</span><span class="sxs-lookup"><span data-stu-id="c30db-124">For the purposes of this example, we pull weather data from May 2007 – December 2012 and used the hourly data files within each of the 68 monthly zips.</span></span> <span data-ttu-id="c30db-125">Ежемесячные ZIP-файлы также содержат сопоставления (YYYYMMstation.txt) между идентификатором метеостанции (WBAN), связанным с ней аэропортом (CallSign) и отклонением часового пояса аэропорта от времени UTC (часовой пояс).</span><span class="sxs-lookup"><span data-stu-id="c30db-125">The monthly zip files also contain a mapping (YYYYMMstation.txt) between the weather station ID (WBAN), the airport that it is associated with (CallSign), and the airport’s time zone offset from UTC (TimeZone).</span></span> <span data-ttu-id="c30db-126">Все они потребуются при объединении с данными авиакомпаний по задержке рейсов.</span><span class="sxs-lookup"><span data-stu-id="c30db-126">All of this information is needed when joining with the airline delay and weather data.</span></span>

## <a name="setting-up-the-spark-environment"></a><span data-ttu-id="c30db-127">Настройка среды Spark</span><span class="sxs-lookup"><span data-stu-id="c30db-127">Setting up the Spark environment</span></span>

<span data-ttu-id="c30db-128">Сначала необходимо настроить среду Spark.</span><span class="sxs-lookup"><span data-stu-id="c30db-128">The first step is to set up the Spark environment.</span></span> <span data-ttu-id="c30db-129">Начнем с указания каталога, содержащего каталоги входных данных, и создания контекста вычислений Spark и функции ведения журнала в консоли:</span><span class="sxs-lookup"><span data-stu-id="c30db-129">We begin by pointing to the directory that contains our input data directories, creating a Spark compute context, and creating a logging function for informational logging to the console:</span></span>

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session to reduce startup times 
#   (remember to stop it later!)
 
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

<span data-ttu-id="c30db-130">Далее мы добавим "Spark_Home" в путь поиска для пакетов R, чтобы использовать SparkR, и инициализируем сеанс SparkR.</span><span class="sxs-lookup"><span data-stu-id="c30db-130">Next we add “Spark_Home” to the search path for R packages so that we can use SparkR, and initialize a SparkR session:</span></span>

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

## <a name="preparing-the-weather-data"></a><span data-ttu-id="c30db-131">Подготовка данных о погоде</span><span class="sxs-lookup"><span data-stu-id="c30db-131">Preparing the weather data</span></span>

<span data-ttu-id="c30db-132">Чтобы подготовить данные по погоде, подставим их в столбцы, необходимые для моделирования:</span><span class="sxs-lookup"><span data-stu-id="c30db-132">To prepare the weather data, we subset it to the columns needed for modeling:</span></span> 

- <span data-ttu-id="c30db-133">"Visibility"</span><span class="sxs-lookup"><span data-stu-id="c30db-133">"Visibility"</span></span>
- <span data-ttu-id="c30db-134">"DryBulbCelsius"</span><span class="sxs-lookup"><span data-stu-id="c30db-134">"DryBulbCelsius"</span></span>
- <span data-ttu-id="c30db-135">"DewPointCelsius"</span><span class="sxs-lookup"><span data-stu-id="c30db-135">"DewPointCelsius"</span></span>
- <span data-ttu-id="c30db-136">"RelativeHumidity"</span><span class="sxs-lookup"><span data-stu-id="c30db-136">"RelativeHumidity"</span></span>
- <span data-ttu-id="c30db-137">"WindSpeed"</span><span class="sxs-lookup"><span data-stu-id="c30db-137">"WindSpeed"</span></span>
- <span data-ttu-id="c30db-138">"Altimeter"</span><span class="sxs-lookup"><span data-stu-id="c30db-138">"Altimeter"</span></span>

<span data-ttu-id="c30db-139">Затем добавим код аэропорта, связанного с метеостанцией, и преобразуем значения местного времени в формат UTC.</span><span class="sxs-lookup"><span data-stu-id="c30db-139">Then we add an airport code associated with the weather station and convert the measurements from local time to UTC.</span></span>

<span data-ttu-id="c30db-140">Начнем с создания файла для сопоставления сведений о метеостанции (WBAN) с кодом аэропорта.</span><span class="sxs-lookup"><span data-stu-id="c30db-140">We begin by creating a file to map the weather station (WBAN) info to an airport code.</span></span> <span data-ttu-id="c30db-141">Их можно получить из файла сопоставления, который содержится в данных по погоде,</span><span class="sxs-lookup"><span data-stu-id="c30db-141">We could get this correlation from the mapping file included with the weather data.</span></span> <span data-ttu-id="c30db-142">сопоставив поле *CallSign* (например, LAX) в файле данных по погоде с *источником* в данных по авиакомпаниям.</span><span class="sxs-lookup"><span data-stu-id="c30db-142">By mapping the *CallSign* (for example, LAX) field in the weather data file to *Origin* in the airline data.</span></span> <span data-ttu-id="c30db-143">Также мы получаем сопоставление *WBAN* с *идентификатором аэропорта* (например, 12892 для LAX), включающее сведения о *часовом поясе* и сохраненные в CSV-файле с именем wban-to-airport-id-tz.CSV, который мы можем использовать.</span><span class="sxs-lookup"><span data-stu-id="c30db-143">However, we just happened to have another mapping on hand that maps *WBAN* to *AirportID* (for example, 12892 for LAX) and includes *TimeZone* that has been saved to a CSV file called “wban-to-airport-id-tz.CSV” that we can use.</span></span> <span data-ttu-id="c30db-144">Например:</span><span class="sxs-lookup"><span data-stu-id="c30db-144">For example:</span></span>

| <span data-ttu-id="c30db-145">AirportID</span><span class="sxs-lookup"><span data-stu-id="c30db-145">AirportID</span></span> | <span data-ttu-id="c30db-146">WBAN</span><span class="sxs-lookup"><span data-stu-id="c30db-146">WBAN</span></span> | <span data-ttu-id="c30db-147">TimeZone</span><span class="sxs-lookup"><span data-stu-id="c30db-147">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="c30db-148">10685</span><span class="sxs-lookup"><span data-stu-id="c30db-148">10685</span></span> | <span data-ttu-id="c30db-149">54831</span><span class="sxs-lookup"><span data-stu-id="c30db-149">54831</span></span> | <span data-ttu-id="c30db-150">-6</span><span class="sxs-lookup"><span data-stu-id="c30db-150">-6</span></span>
| <span data-ttu-id="c30db-151">14871</span><span class="sxs-lookup"><span data-stu-id="c30db-151">14871</span></span> | <span data-ttu-id="c30db-152">24232</span><span class="sxs-lookup"><span data-stu-id="c30db-152">24232</span></span> | <span data-ttu-id="c30db-153">–8</span><span class="sxs-lookup"><span data-stu-id="c30db-153">-8</span></span>
| <span data-ttu-id="c30db-154">..</span><span class="sxs-lookup"><span data-stu-id="c30db-154">..</span></span> | <span data-ttu-id="c30db-155">..</span><span class="sxs-lookup"><span data-stu-id="c30db-155">..</span></span> | <span data-ttu-id="c30db-156">..</span><span class="sxs-lookup"><span data-stu-id="c30db-156">..</span></span>

<span data-ttu-id="c30db-157">Следующий код считывает каждый почасовой необработанный файл данных по погоде, выполняет подстановку в необходимые столбцы, объединяет файл сопоставления метеостанции, преобразует дату и время измерений в формат UTC, а затем записывает новую версию файла:</span><span class="sxs-lookup"><span data-stu-id="c30db-157">The following code reads each of the hourly raw weather data files, subsets to the columns we need, merges the weather station mapping file, adjusts the date times of measurements to UTC, and then writes out a new version of the file:</span></span>

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

## <a name="importing-the-airline-and-weather-data-to-spark-dataframes"></a><span data-ttu-id="c30db-158">Импорт данных авиакомпаний и погодных данных в таблицы данных Spark</span><span class="sxs-lookup"><span data-stu-id="c30db-158">Importing the airline and weather data to Spark DataFrames</span></span>

<span data-ttu-id="c30db-159">Теперь мы используем функцию SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) для импорта данных по погоде и авиакомпаниям в кадры данных Spark.</span><span class="sxs-lookup"><span data-stu-id="c30db-159">Now we use the SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function to import the weather and airline data to Spark DataFrames.</span></span> <span data-ttu-id="c30db-160">Это функция отложенного выполнения, как и многие другие методы Spark. Это означает, что они находятся в очереди на выполнение, но выполняются только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="c30db-160">This function, like many other Spark methods, are executed lazily, meaning that they are queued for execution but not executed until required.</span></span>

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for the airline data

logmsg('create a SparkR DataFrame for the airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for the weather data

logmsg('create a SparkR DataFrame for the weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="c30db-161">Фильтрация и преобразование данных</span><span class="sxs-lookup"><span data-stu-id="c30db-161">Data cleansing and transformation</span></span>

<span data-ttu-id="c30db-162">Далее выполним очистку импортированных данных по авиакомпаниям, чтобы переименовать столбцы.</span><span class="sxs-lookup"><span data-stu-id="c30db-162">Next we do some cleanup on the airline data we’ve imported to rename columns.</span></span> <span data-ttu-id="c30db-163">Мы оставим только необходимые переменные и округлим время запланированного отправления до ближайшего часа, чтобы объединить с последними данными по погоде перед вылетом.</span><span class="sxs-lookup"><span data-stu-id="c30db-163">We only keep the variables needed, and round scheduled departure times down to the nearest hour to enable merging with the latest weather data at departure:</span></span>

```
logmsg('clean the airline data') 
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

# Select desired columns from the flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time to full hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

<span data-ttu-id="c30db-164">Теперь выполним аналогичные операции с данными по погоде:</span><span class="sxs-lookup"><span data-stu-id="c30db-164">Now we perform similar operations on the weather data:</span></span>

```
# Average weather readings by hour
logmsg('clean the weather data') 
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

## <a name="joining-the-weather-and-airline-data"></a><span data-ttu-id="c30db-165">Объединение данных о погоде с данными об авиакомпаниях</span><span class="sxs-lookup"><span data-stu-id="c30db-165">Joining the weather and airline data</span></span>

<span data-ttu-id="c30db-166">Теперь воспользуемся функцией SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html), чтобы выполнить левое внешнее соединение данных по погоде с данными по авиакомпаниям на основе идентификатора аэропорта отправления (AirportID) и значения даты и времени (datetime).</span><span class="sxs-lookup"><span data-stu-id="c30db-166">We now use the SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function to do a left outer join of the airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="c30db-167">Внешнее объединение позволяет сохранить все записи данных об авиакомпаниях, даже если они не коррелируют с погодными данными.</span><span class="sxs-lookup"><span data-stu-id="c30db-167">The outer join allows us to retain all the airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="c30db-168">После соединения удалим некоторые избыточные столбцы и переименуем оставшиеся, чтобы удалить входящий префикс кадра данных, возникший при соединении.</span><span class="sxs-lookup"><span data-stu-id="c30db-168">Following the join, we remove some redundant columns, and rename the kept columns to remove the incoming DataFrame prefix introduced by the join.</span></span>

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

<span data-ttu-id="c30db-169">Аналогичным образом объединим данные по погоде и авиакомпаниям на основе идентификатора аэропорта прибытия (AirportID) и значения даты и времени (datetime).</span><span class="sxs-lookup"><span data-stu-id="c30db-169">In a similar fashion, we join the weather and airline data based on arrival AirportID and datetime:</span></span>

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

## <a name="save-results-to-csv-for-exchange-with-scaler"></a><span data-ttu-id="c30db-170">Сохранение результатов в CSV-файл для обмена со ScaleR</span><span class="sxs-lookup"><span data-stu-id="c30db-170">Save results to CSV for exchange with ScaleR</span></span>

<span data-ttu-id="c30db-171">На этом операции соединения с помощью SparkR завершены.</span><span class="sxs-lookup"><span data-stu-id="c30db-171">That completes the joins we need to do with SparkR.</span></span> <span data-ttu-id="c30db-172">Сохраним данные из окончательного кадра данных Spark joinedDF5 в CSV-файл в качестве входных данных для SparkR и завершим сеанс SparkR.</span><span class="sxs-lookup"><span data-stu-id="c30db-172">We save the data from the final Spark DataFrame “joinedDF5” to a CSV for input to ScaleR and then close out the SparkR session.</span></span> <span data-ttu-id="c30db-173">Мы явно указываем SparkR сохранить итоговый CSV-файл в 80 отдельных секциях, чтобы обеспечить достаточный параллелизм при обработке в ScaleR.</span><span class="sxs-lookup"><span data-stu-id="c30db-173">We explicitly tell SparkR to save the resultant CSV in 80 separate partitions to enable sufficient parallelism in ScaleR processing:</span></span>

```
logmsg('output the joined data from Spark to CSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result to directory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down the SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-to-xdf-for-use-by-scaler"></a><span data-ttu-id="c30db-174">Импорт в XDF для использования в ScaleR</span><span class="sxs-lookup"><span data-stu-id="c30db-174">Import to XDF for use by ScaleR</span></span>

<span data-ttu-id="c30db-175">Мы могли бы использовать CSV-файл с объединенными данными по авиакомпаниям и погоде "как есть", чтобы создать модель с помощью текстового источника данных ScaleR.</span><span class="sxs-lookup"><span data-stu-id="c30db-175">We could use the CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source.</span></span> <span data-ttu-id="c30db-176">Однако вместо этого мы сначала импортируем его в формат XDF, так как он более эффективен при выполнении нескольких операций с набором данных.</span><span class="sxs-lookup"><span data-stu-id="c30db-176">But we import it to XDF first, since it is more efficient when running multiple operations on the dataset:</span></span>

```
logmsg('Import the CSV to compressed, binary XDF format') 

# set the Spark compute context for R Server 
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

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="c30db-177">Разделение данных на наборы для обучения и тестирования</span><span class="sxs-lookup"><span data-stu-id="c30db-177">Splitting data for training and test</span></span>

<span data-ttu-id="c30db-178">Воспользуемся rxDataStep для отделения данных за 2012 год в целях тестирования, оставив остальные данные для обучения.</span><span class="sxs-lookup"><span data-stu-id="c30db-178">We use rxDataStep to split out the 2012 data for testing and keep the rest for training:</span></span>

```
# split out the training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out the testing data

logmsg('split out the test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="c30db-179">Обучение и тестирование модели логистической регрессии</span><span class="sxs-lookup"><span data-stu-id="c30db-179">Train and test a logistic regression model</span></span>

<span data-ttu-id="c30db-180">Все готово для создания модели.</span><span class="sxs-lookup"><span data-stu-id="c30db-180">Now we are ready to build a model.</span></span> <span data-ttu-id="c30db-181">Чтобы увидеть влияние данных по погоде на задержку времени прибытия, мы используем подпрограмму логистической регрессии ScaleR.</span><span class="sxs-lookup"><span data-stu-id="c30db-181">To see the influence of weather data on delay in the arrival time, we use ScaleR’s logistic regression routine.</span></span> <span data-ttu-id="c30db-182">С ее помощью мы смоделируем, зависит ли задержка прибытия более чем на 15 минут от погоды в аэропортах отправления и прибытия.</span><span class="sxs-lookup"><span data-stu-id="c30db-182">We use it to model whether an arrival delay of greater than 15 minutes is influenced by the weather at the departure and arrival airports:</span></span>

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use the scalable rxLogit() function but set max iterations to 3 for the purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

<span data-ttu-id="c30db-183">Теперь давайте посмотрим, как это работает с данными для тестирования, сделав некоторые прогнозы и оценив ROC и AUC.</span><span class="sxs-lookup"><span data-stu-id="c30db-183">Now let’s see how it does on the test data by making some predictions and looking at ROC and AUC.</span></span>

```
# Predict over test data (Logistic Regression).

logmsg('predict over the test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use the scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under the Curve (AUC).

logmsg('calculate the roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a><span data-ttu-id="c30db-184">Альтернативное применение модели</span><span class="sxs-lookup"><span data-stu-id="c30db-184">Scoring elsewhere</span></span>

<span data-ttu-id="c30db-185">Эту модель можно также использовать для оценки данных на другой платформе</span><span class="sxs-lookup"><span data-stu-id="c30db-185">We can also use the model for scoring data on another platform.</span></span> <span data-ttu-id="c30db-186">путем ее сохранения в файл RDS с последующей передачей и импортом в конечную среду оценки, например в службы SQL Server R.</span><span class="sxs-lookup"><span data-stu-id="c30db-186">By saving it to an RDS file and then transferring and importing that RDS into a destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="c30db-187">Важно убедиться в том, что уровни фактора данных для оценки соответствуют уровням, на которых основана модель.</span><span class="sxs-lookup"><span data-stu-id="c30db-187">It is important to ensure that the factor levels of the data to be scored match those on which the model was built.</span></span> <span data-ttu-id="c30db-188">Этого можно добиться, если извлечь и сохранить сведения столбцов, связанные с данными для моделирования, с помощью функции ScaleR `rxCreateColInfo()`, а затем применить эти сведения к источнику входных данных для прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="c30db-188">That match can be achieved by extracting and saving the column infomation associated with the modeling data via ScaleR’s `rxCreateColInfo()` function and then applying that column information to the input data source for prediction.</span></span> <span data-ttu-id="c30db-189">В следующем примере мы сохраним несколько строк из тестового набора данных, а затем извлечем и используем сведения о столбцах из этого примера в скрипте прогнозирования:</span><span class="sxs-lookup"><span data-stu-id="c30db-189">In the following we save a few rows of the test dataset and extract and use the column information from this sample in the prediction script:</span></span>

```
# save the model and a sample of the test dataset 

logmsg('save serialized version of the model and a sample of the test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop the spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a><span data-ttu-id="c30db-190">Сводка</span><span class="sxs-lookup"><span data-stu-id="c30db-190">Summary</span></span>

<span data-ttu-id="c30db-191">В этой статье показано, как можно использовать SparkR для работы с данными в сочетании со ScaleR для разработки модели в Hadoop Spark.</span><span class="sxs-lookup"><span data-stu-id="c30db-191">In this article, we’ve shown how it’s possible to combine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark.</span></span> <span data-ttu-id="c30db-192">Этот сценарий требует создания нескольких сеансов Spark, использования одновременно только одного сеанса и обмена данными посредством CSV-файлов.</span><span class="sxs-lookup"><span data-stu-id="c30db-192">This scenario requires that you maintain separate Spark sessions, only running one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="c30db-193">При всей своей простоте этот процесс станет еще проще в предстоящем выпуске R Server, в котором SparkR и ScaleR смогут совместно использовать сеансы и кадры данных Spark.</span><span class="sxs-lookup"><span data-stu-id="c30db-193">Although straightforward, this process should be even easier in an upcoming R Server release, when SparkR and ScaleR can share a Spark session and so share Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="c30db-194">Дальнейшие действия и дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="c30db-194">Next steps and more information</span></span>

- <span data-ttu-id="c30db-195">Дополнительные сведения об использовании R Server в Spark см. в [руководстве по началу работы в библиотеке MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c30db-195">For more information on use of R Server on Spark, see the [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="c30db-196">Общие сведения об R Server см. в статье [Начало работы с Microsoft R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node).</span><span class="sxs-lookup"><span data-stu-id="c30db-196">For general information on R Server, see the [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="c30db-197">Сведения об R Server в HDInsight см. в статьях [Основные сведения об R Server и возможностях открытого кода R в HDInsight](hdinsight-hadoop-r-server-overview.md) и [Приступая к работе с R Server в HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c30db-197">For information on R Server on HDInsight, see [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) and [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span>

<span data-ttu-id="c30db-198">Дополнительные сведения об использовании SparkR см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c30db-198">For more information on use of SparkR, see:</span></span>

- <span data-ttu-id="c30db-199">[SparkR (R on Spark)](https://spark.apache.org/docs/2.1.0/sparkr.html) (SparkR (язык R в Spark))</span><span class="sxs-lookup"><span data-stu-id="c30db-199">[Apache SparkR document](https://spark.apache.org/docs/2.1.0/sparkr.html)</span></span>

- <span data-ttu-id="c30db-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) (Общие сведения о SparkR) на сайте Databricks</span><span class="sxs-lookup"><span data-stu-id="c30db-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
