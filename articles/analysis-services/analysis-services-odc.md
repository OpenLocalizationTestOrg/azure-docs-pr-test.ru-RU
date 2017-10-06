---
title: "aaaCreate .odc файл tooconnect tooan Azure сервер служб Analysis Services | Документы Microsoft"
description: "Узнайте, как toocreate tooand tooconnect файла подключения к данным Office получить данные с сервера служб Analysis Services в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/23/2017
ms.author: owend
ms.openlocfilehash: 9c8c8df23b17f19905d7ec51af4eb63eb995045e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-office-data-connection-file"></a><span data-ttu-id="3addf-103">Создание файла подключения к данным Office</span><span class="sxs-lookup"><span data-stu-id="3addf-103">Create an Office Data Connection file</span></span>

<span data-ttu-id="3addf-104">Сведения в этой статье описывается, как создать подключение к данным Office файл tooconnect tooan Azure сервер служб Analysis Services из Excel 2016 номер версии 16.0.7369.2117 или более ранней версии, или Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="3addf-104">Information in this article describes how you can create an Office Data Connection file tooconnect tooan Azure Analysis Services server from Excel 2016 version number 16.0.7369.2117 or earlier, or Excel 2013.</span></span> <span data-ttu-id="3addf-105">Обновленный [поставщик MSOLAP.7](analysis-services-data-providers.md) также является обязательным.</span><span class="sxs-lookup"><span data-stu-id="3addf-105">An updated [MSOLAP.7 provider](analysis-services-data-providers.md) is also required.</span></span>


1. <span data-ttu-id="3addf-106">Скопируйте hello подключения ниже образец файла и вставить в текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="3addf-106">Copy hello sample connection file below and paste into a text editor.</span></span> 

2. <span data-ttu-id="3addf-107">В `odc:ConnectionString`, измените hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="3addf-107">In `odc:ConnectionString`, change hello following properties:</span></span>

    *   <span data-ttu-id="3addf-108">В `Data Source=asazure://<region>.asazure.windows.net/<servername>;` изменить `<region>` toohello области сервера служб Analysis Services и `<servername>` toohello имя вашего сервера.</span><span class="sxs-lookup"><span data-stu-id="3addf-108">In `Data Source=asazure://<region>.asazure.windows.net/<servername>;` change `<region>` toohello region of your Analysis Services server and `<servername>` toohello name of your  server.</span></span>

    *   <span data-ttu-id="3addf-109">В `Initial Catalog=<database>;` изменить `<database>` toohello имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="3addf-109">In `Initial Catalog=<database>;` change `<database>` toohello name of your database.</span></span>

3. <span data-ttu-id="3addf-110">В `<odc:CommandText>Model</odc:CommandText>` изменить `Model` toohello имя модели или перспективы.</span><span class="sxs-lookup"><span data-stu-id="3addf-110">In `<odc:CommandText>Model</odc:CommandText>` change `Model` toohello name of your model or perspective.</span></span> 

4. <span data-ttu-id="3addf-111">Сохраните файл hello с `.odc` toohello расширения C:\Users\\*username*папку \Documents\My источники данных.</span><span class="sxs-lookup"><span data-stu-id="3addf-111">Save hello file with an `.odc` extension toohello C:\Users\\*username*\Documents\My Data Sources folder.</span></span>

5. <span data-ttu-id="3addf-112">Щелкните правой кнопкой мыши файл hello и нажмите кнопку **открыть в Excel**.</span><span class="sxs-lookup"><span data-stu-id="3addf-112">Right-click hello file, and then click **Open in Excel**.</span></span> <span data-ttu-id="3addf-113">Или в Excel в hello **данные** ленты, нажмите кнопку **существующие подключения**, выберите файл и нажмите кнопку **откройте**.</span><span class="sxs-lookup"><span data-stu-id="3addf-113">Or in Excel, on hello **Data** ribbon, click **Existing Connections**, select your file, and then click **Open**.</span></span>



<span data-ttu-id="3addf-114">**Образец файла подключения**</span><span class="sxs-lookup"><span data-stu-id="3addf-114">**Sample connection file**</span></span>
```
<html xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns="http://www.w3.org/TR/REC-html40">

<head>
<meta http-equiv=Content-Type content="text/x-ms-odc; charset=utf-8">
<meta name=ProgId content=ODC.Cube>
<meta name=SourceType content=OLEDB>
<meta name=Catalog content="Database">
<meta name=Table content=Model>
<title>AzureAnalysisServicesConnection</title>
<xml id=docprops><o:DocumentProperties
  xmlns:o="urn:schemas-microsoft-com:office:office"
  xmlns="http://www.w3.org/TR/REC-html40">
  <o:Name>SampleAzureAnalysisServices</o:Name>
 </o:DocumentProperties>
</xml><xml id=msodc><odc:OfficeDataConnection
  xmlns:odc="urn:schemas-microsoft-com:office:odc"
  xmlns="http://www.w3.org/TR/REC-html40">
  <odc:Connection odc:Type="OLEDB">
   <odc:ConnectionString>Provider=MSOLAP.7;Data Source=asazure://<region>.asazure.windows.net/<servername>;Initial Catalog=<database>;</odc:ConnectionString>
   <odc:CommandType>Cube</odc:CommandType>
   <odc:CommandText>Model</odc:CommandText>
  </odc:Connection>
 </odc:OfficeDataConnection>
</xml>
<style>
<!--
    .ODCDataSource
    {
    behavior: url(dataconn.htc);
    }
-->
</style>
 
</head>

<body onload='init()' scroll=no leftmargin=0 topmargin=0 rightmargin=0 style='border: 0px'>
<table style='border: solid 1px threedface; height: 100%; width: 100%' cellpadding=0 cellspacing=0 width='100%'> 
  <tr> 
    <td id=tdName style='font-family:arial; font-size:medium; padding: 3px; background-color: threedface'> 
      &nbsp; 
    </td> 
     <td id=tdTableDropdown style='padding: 3px; background-color: threedface; vertical-align: top; padding-bottom: 3px'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td id=tdDesc colspan='2' style='border-bottom: 1px threedshadow solid; font-family: Arial; font-size: 1pt; padding: 2px; background-color: threedface'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td colspan='2' style='height: 100%; padding-bottom: 4px; border-top: 1px threedhighlight solid;'> 
      <div id='pt' style='height: 100%' class='ODCDataSource'></div> 
    </td> 
  </tr> 
</table> 

  
<script language='javascript'> 

function init() { 
  var sName, sDescription; 
  var i, j; 
  
  try { 
    sName = unescape(location.href) 
  
    i = sName.lastIndexOf(".") 
    if (i>=0) { sName = sName.substring(1, i); } 
  
    i = sName.lastIndexOf("/") 
    if (i>=0) { sName = sName.substring(i+1, sName.length); } 

    document.title = sName; 
    document.getElementById("tdName").innerText = sName; 

    sDescription = document.getElementById("docprops").innerHTML; 
  
    i = sDescription.indexOf("escription>") 
    if (i>=0) { j = sDescription.indexOf("escription>", i + 11); } 

    if (i>=0 && j >= 0) { 
      j = sDescription.lastIndexOf("</", j); 

      if (j>=0) { 
          sDescription = sDescription.substring(i+11, j); 
        if (sDescription != "") { 
            document.getElementById("tdDesc").style.fontSize="x-small"; 
          document.getElementById("tdDesc").innerHTML = sDescription; 
          } 
        } 
      } 
    } 
  catch(e) { 

    } 
  } 
</script> 

</body> 
 
</html>

```



