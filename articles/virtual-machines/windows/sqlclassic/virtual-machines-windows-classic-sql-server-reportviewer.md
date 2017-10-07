---
title: "aaaUse ReportViewer на веб-сайте | Документы Microsoft"
description: "Описывается, как toobuild Azure веб-узел с элементом управления Visual Studio ReportViewer hello, отображение отчета хранятся на виртуальной машине Microsoft Azure."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>Использование ReportViewer для веб-сайта, размещенного в Azure
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

Можно построить на Microsoft Azure сайт с hello управления Visual Studio ReportViewer, который отображает отчет, сохраненный на виртуальной машине Microsoft Azure. Hello элемента управления ReportViewer — веб-приложения сборки с помощью шаблона ASP.NET веб-приложения hello.

> [!IMPORTANT]
> шаблоны веб-приложение ASP.NET MVC Hello не поддерживают элемент управления ReportViewer hello.

tooincorporate ReportViewer на сайт Microsoft Azure Web необходимо hello toocomplete следующие задачи.

* **Добавить** toohello сборки пакета развертывания
* **Настроить** проверку подлинности и авторизацию
* **Публикация** hello tooAzure приложения ASP.NET Web

## <a name="prerequisites"></a>Предварительные требования
Просмотрите раздел «Общие рекомендации и советы и рекомендации» hello в [SQL Server Business Intelligence в виртуальных машинах Azure](../classic/ps-sql-bi.md).

> [!NOTE]
> Элементы управления ReportViewer входят в состав Visual Studio Standard Edition или выше. Если вы используете hello Web Developer Express Edition, необходимо установить hello [MICROSOFT REPORT VIEWER 2012 RUNTIME](https://www.microsoft.com/download/details.aspx?id=35747) функциями времени выполнения ReportViewer toouse hello.
> 
> ReportViewer в режиме локальной обработки не поддерживается в Microsoft Azure.

## <a name="adding-assemblies-toohello-deployment-package"></a>Добавление сборки toohello пакета развертывания
При размещении ASP.NET приложения в локальной hello сборки ReportViewer обычно устанавливаются непосредственно в hello глобальный кэш сборок (GAC) сервера IIS hello во время установки Visual Studio и может обращаться непосредственно приложение hello. Тем не менее при размещается приложение ASP.NET в облаке hello, Microsoft Azure не разрешает все, что toobe установлен в hello в глобальный кэш СБОРОК, поэтому необходимо убедиться, что сборки ReportViewer hello доступны для приложения локально. Можно это сделать, добавив toothem ссылки в проекте и настроить их toobe копируется локально.

В режиме удаленной обработки элемент управления ReportViewer hello использует hello следующие сборки:

* **Microsoft.ReportViewer.WebForms.dll**: содержит код ReportViewer hello, который требуется toouse ReportViewer на странице. Ссылка для этой сборки добавляется в проект tooyour при удалении элемента управления ReportViewer на страницу ASP.NET в проекте.
* **Microsoft.ReportViewer.Common.dll**: содержит классы, используемые в hello элемента управления ReportViewer, во время выполнения. Tooyour проекта не добавляются автоматически.

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>tooadd tooMicrosoft.ReportViewer.Common ссылки
* Правой кнопкой ваш проект **ссылки** , а затем выберите **добавить ссылку**, выберите сборку hello hello вкладке .NET и нажмите кнопку **ОК**.

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>сборки hello toomake локального доступа для приложения ASP.NET
1. В hello **ссылки** папку, щелкните сборку Microsoft.ReportViewer.Common hello, чтобы его свойства отобразятся в панели свойств hello.
2. В области свойств hello задайте **Копировать локально** tooTrue.
3. Повторите шаги 1 и 2 для сборки Microsoft.ReportViewer.WebForms.

### <a name="tooget-reportviewer-language-pack"></a>Языковой пакет ReportViewer tooget
1. Установите hello соответствующие Microsoft Report Viewer 2012 Runtime распространяемый пакет из [центра загрузки Майкрософт](http://go.microsoft.com/fwlink/?LinkId=317386).
2. Hello выберите язык из раскрывающегося списка hello и страница hello получает перенаправленный toohello соответствующую страницу центра загрузки.
3. Нажмите кнопку **загрузки** загрузку hello toostart ReportViewerLP.exe.
4. После загрузки ReportViewerLP.exe нажмите кнопку **запуска** tooinstall немедленно, или нажмите кнопку **Сохранить** toosave его tooyour компьютера. Если щелкнуть **Сохранить**, запоминать hello hello папке, где сохраняется файл hello.
5. Найдите папку hello, где был сохранен файл hello. Щелкните файл ReportViewerLP.exe правой кнопкой мыши, выберите **Запуск от имени администратора**, а затем нажмите кнопку **Да**.
6. После запуска ReportViewerLP.exe, вы увидите hello c:\windows\assembly имеет файлы ресурсов hello **Microsoft.ReportViewer.Webforms.Resources** и **Microsoft.ReportViewer.Common.Resources** .

### <a name="tooconfigure-for-localized-reportviewer-control"></a>tooconfigure для локализованного управления ReportViewer
1. Скачайте и установите распространяемый пакет Microsoft Report Viewer 2012 Runtime hello, следующие hello выше указанной инструкции.
2. Создать <language> папку в проекте и скопируйте hello hello связанные файлы сборок ресурсов. Hello ресурсов сборки файлов toobe копируются являются: **Microsoft.ReportViewer.Webforms.Resources.dll** и **Microsoft.ReportViewer.Common.Resources.dll**. Выберите файлы сборок ресурсов hello и на панели «Свойства» hello установите **скопируйте каталог tooOutput** слишком»**всегда Копировать**».
3. Задать hello Culture и UICulture для веб-проекта hello. Дополнительные сведения о том, как отображается hello tooset язык и региональные параметры и региональные параметры пользовательского интерфейса для веб-страницу ASP.NET, [как: набор hello Culture и Uiculture для глобализации веб-страницы ASP.NET](http://go.microsoft.com/fwlink/?LinkId=237461).

## <a name="configuring-authentication-and-authorization"></a>Настройка проверки подлинности и авторизации
Hello ReportViewer должен toouse tooauthenticate правильные учетные данные с сервера отчетов hello и hello учетные данные должны быть авторизованы по hello server tooaccess hello отчетов нужные. Сведения о проверке подлинности см. в разделе hello Технический документ [серверы отчетов виртуальную машину с использованием Microsoft Azure и элемент управления средства просмотра отчетов служб Reporting Services](https://msdn.microsoft.com/library/azure/dn753698.aspx).

## <a name="publish-hello-aspnet-web-application-tooazure"></a>Публикация hello tooAzure приложения ASP.NET Web
Инструкции по публикации приложения ASP.NET Web tooAzure см. в разделе [как: миграция и публикация tooAzure веб-приложения из Visual Studio](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) и [приступить к работе с веб-приложений и ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md).

> [!IMPORTANT]
> Если hello команду Добавить проект развертывания Azure или добавить проект облачной службы Azure не отображается в контекстном меню hello в обозревателе решений, может понадобиться toochange hello целевой платформы проекта hello too.NET Framework 4.
> 
> Hello две команды предоставляют фактически hello же функциональные возможности. Один или hello другие команды будет отображаться в контекстном меню hello в зависимости от того, какая версия Microsoft Azure SDK hello установки.
> 
> 

## <a name="resources"></a>Ресурсы
[Отчеты Майкрософт](http://go.microsoft.com/fwlink/?LinkId=205399)

[SQL Server Business Intelligence на виртуальных машинах Azure](../classic/ps-sql-bi.md)

[Использовать tooCreate PowerShell Azure ВМ с собственного режима сервера отчетов](../classic/ps-sql-report.md)

