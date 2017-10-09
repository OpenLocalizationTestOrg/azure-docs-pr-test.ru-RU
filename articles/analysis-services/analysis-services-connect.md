---
title: "aaaConnect tooAzure служб Analysis Services | Документы Microsoft"
description: "Узнайте, как tooconnect tooand получить данные с сервера служб Analysis Services в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a>Подключение сервера tooan Azure Analysis Services

В этой статье описан подключающегося tooa сервера с помощью моделирования данных и управления приложениями, например SQL Server Management Studio (SSMS) или SQL Server Data Tools (SSDT). Для этого также можно использовать клиентские приложения создания отчетов, такие как Microsoft Excel, Power BI Desktop или пользовательские приложения. Службы Analysis Services tooAzure подключений использования протокола HTTPS.

## <a name="client-libraries"></a>Клиентские библиотеки
[Получить последние клиентские библиотеки hello](analysis-services-data-providers.md)

Все server tooa подключений, независимо от типа требуются обновленные объекты AMO, ADOMD.NET и OLEDB библиотеки tooconnect tooand интерфейс клиента с сервером служб Analysis Services. Для SSMS, SSDT, Excel 2016 и Power BI последние клиентские библиотеки hello установлены или обновляется ежемесячные выпуски. Однако в некоторых случаях возможна приложения не имеют последние hello. Например, при обновлении политики задержки или обновления Office 365 находятся на hello отложенный канала.

## <a name="server-name"></a>имя сервера;

При создании сервера служб Analysis Services в Azure, необходимо указать уникальное имя и hello региона, где будет создан toobe сервер hello. При указании имени сервера hello в соединении, является схема именования hello server:

```
<protocol>://<region>/<servername>
```
 Где протокола — строка **asazure**, регион — hello Uri, где был создан сервер hello (например, westus.asazure.windows.net) и имя_сервера — hello имя вашего сервера, уникальный в пределах области hello.

### <a name="get-hello-server-name"></a>Получить имя сервера hello
В **портал Azure** > сервера > **Обзор** > **имя сервера**, копировать hello всего сервера имя. Если другим пользователям в организации слишком подключении toothis сервера, можно предоставить это имя сервера с ними. При указании имени сервера, необходимо использовать весь путь hello.

![Получение имени сервера в Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>Строка подключения

При подключении tooAzure Analysis Services с помощью hello табличной объектной модели, используйте hello следующие форматы строк подключения:

###### <a name="integrated-azure-active-directory-authentication"></a>Встроенная проверка подлинности Azure Active Directory
Встроенная проверка подлинности продолжается hello кэш учетных данных Azure Active Directory, если он доступен. В противном случае отображается окно входа Azure hello.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>Проверка подлинности Azure Active Directory с использованием имени пользователя и пароля

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Проверка подлинности Windows (встроенный механизм безопасности)
Используйте учетную запись Windows hello работают hello текущего процесса.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>Подключение с помощью ODC-файла
Более старые версии Excel позволяет пользователям подключаться tooan сервера Azure Analysis Services с помощью файла подключения к данным Office (ODC). toolearn более, в разделе [создайте файл подключения к данным Office (ODC)](analysis-services-odc.md).


## <a name="next-steps"></a>Дальнейшие действия
[Подключение с помощью Excel](analysis-services-connect-excel.md)    
[Подключение с помощью Power BI](analysis-services-connect-pbi.md)   
[Управление службами Analysis Services](analysis-services-manage.md)   

