---
title: "aaaRelease заметки для Application Insights | Документы Microsoft"
description: "Добавление развертывания или построения маркеры диаграммы обозревателя метрик tooyour в Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Заметки к диаграммам метрик в Application Insights
Заметки к диаграммам [обозревателя метрик](app-insights-metrics-explorer.md) показывают, где развернута новая сборка, а также отображают другие важные события. Они позволяют легко toosee ли изменения имели никакого воздействия на производительность приложения. Они могут создаваться автоматически с hello [системы сборки Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs). Можно также создать заметки tooflag любого события, например по [создание их на основе PowerShell](#create-annotations-from-powershell).

![Пример заметок с видимой корреляцией с временем ответа сервера](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>Заметки о выпуске сборки VSTS

Выпуск заметки являются компонентом облачной сборки hello и выпуска службы из Visual Studio Team Services. 

### <a name="install-hello-annotations-extension-one-time"></a>Установка расширения заметок hello (один раз)
заметки выпуска может toocreate toobe, вам потребуется tooinstall один из hello многие службы Team расширения, доступные в hello Visual Studio Marketplace.

1. Войдите в tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) проекта.
2. В Visual Studio Marketplace [расширение заметок выпуска hello](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)и добавить его учетную запись Team Services tooyour.

![В верхнем правом углу веб-страницы Team Services откройте "Магазин". Выберите Visual Team Services и нажмите кнопку "Дополнительно" в разделе "Сборка и выпуск".](./media/app-insights-annotations/10.png)

Требуется только toodo этом один раз для учетной записи Visual Studio Team Services. Теперь можно настроить заметки к выпуску для любого проекта в вашей учетной записи. 

### <a name="configure-release-annotations"></a>Настройка заметок к выпуску

Для каждого шаблона выпуска VSTS необходим ключ tooget отдельный API.

1. Войдите в toohello [портал Microsoft Azure](https://portal.azure.com) и открыть ресурс Application Insights hello, осуществляющее мониторинг приложения. (Или [создайте новый](app-insights-overview.md), если вы этого еще не сделали.)
2. Откройте **Доступ через API** и выберите **Идентификатор Application Insights**.
   
    ![На сайте portal.azure.com откройте ресурс Application Insights и выберите "Параметры". Откройте "Доступ к API". Скопируйте идентификатор приложения hello](./media/app-insights-annotations/20.png)

4. В отдельном окне браузера откройте (или создайте) hello шаблон выпуска, который управляет развертываний из Visual Studio Team Services. 
   
    Добавьте задачу и выберите задачу заметки выпуска аналитики приложения hello меню "hello".
   
    Вставить hello **идентификатор приложения** , скопированный из hello колонке доступа к API.
   
    ![В Visual Studio Team Services откройте "Выпуск", выберите определение выпуска и нажмите кнопку "Изменить". Щелкните "Добавьте задачу" и выберите "Заметки к выпуску Application Insights". Вставьте hello идентификатор аналитики приложений.](./media/app-insights-annotations/30.png)
4. Набор hello **APIKey** переменной tooa поля `$(ApiKey)`.

5. Обратно в hello Azure окна создайте новый ключ API и сделайте его копию.
   
    ![В hello колонке доступа к API в Azure окно приветствия нажмите кнопку Создать ключ API. Введите комментарий, щелкните "Написать заметки" и нажмите кнопку "Создать ключ". Скопируйте новый ключ hello.](./media/app-insights-annotations/40.png)

6. Перейдите на вкладку конфигурации hello hello шаблона выпуска.
   
    Создайте определение переменной для `ApiKey`.
   
    Вставьте определение переменной ApiKey ключа toohello ваш API.
   
    ![В окне Team Services hello перейдите на вкладку конфигурации hello и нажмите кнопку Добавить переменную. Задайте имя tooApiKey hello в hello значение ключа hello только что созданный и нажмите кнопку hello значок блокировки.](./media/app-insights-annotations/50.png)
7. Наконец **Сохранить** hello определения выпуска.


## <a name="view-annotations"></a>Просмотр заметок
Теперь при использовании toodeploy шаблона выпуска hello нового выпуска заметки будут отправляться tooApplication аналитики. Hello заметки будут отображаться на диаграммах в обозревателе метрик.

Щелкните любой заметки маркер tooopen подробности hello выпуска, включая запрашивающей стороны, ветвь системы управления версиями, определение выпуска, среды и многое другое.

![Щелкните любой маркер заметки о выпуске.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>Создание настраиваемых заметок в PowerShell
Вы можете создать аннотации из любого процесса на свой выбор (без использования Visual Studio Team System). 


1. Создать локальную копию hello [сценарий Powershell из GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).

2. Получить идентификатор приложения hello и создайте ключ API из hello колонке доступа к API.

3. Вызов скрипта hello следующим образом:

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

Это легко toomodify hello скрипт, например toocreate заметок для прошлых hello.

## <a name="next-steps"></a>Дальнейшие действия

* [Создание рабочих элементов](app-insights-diagnostic-search.md#create-work-item)
* [Автоматизация с помощью PowerShell](app-insights-powershell.md)
