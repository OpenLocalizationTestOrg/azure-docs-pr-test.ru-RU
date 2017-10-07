---
title: "hello aaaUsing Visual Studio Azure мастер публикации приложений | Документы Microsoft"
description: "Узнайте, как tooconfigure hello различные параметры в мастер публикации Visual Studio Azure приложения hello"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>Используя мастер публикации Visual Studio Azure приложения hello
После разработки веб-приложения в Visual Studio, tooan приложения облачной службы Azure можно опубликовать с помощью hello **публикации приложения Azure** мастера. 

> [!NOTE]
> Этот раздел посвящен развертывание служб toocloud, не tooweb сайтов. Сведения о развертывании tooweb сайтов см. в разделе [как tooDeploy веб-сайта Azure](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>Доступ к приветствия мастера публикации приложений Azure

Можно открыть мастер публикации приложений Azure hello двумя способами, в зависимости от типа проекта Visual Studio, в которой имеется hello.

**Если у вас проект облачной службы Azure:**

1. Создайте или откройте проект облачной службы Azure в среде Visual Studio.

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и hello контекстном меню, выберите **публикации**.

**Если у вас проект веб-приложения, который не является проектом Azure:**

1. Создайте или откройте проект облачной службы Azure в среде Visual Studio.

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и hello контекстном меню, выберите **преобразовать** > **преобразовать проект облачной службы tooAzure**. 

1. В **обозревателе решений**, щелкните правой кнопкой мыши только что созданный hello проекта Azure и hello контекстном меню, выберите **публикации**.

## <a name="sign-in-page"></a>Страница входа

![Страница входа](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Учетная запись** — выберите учетную запись или **добавить учетную запись** в раскрывающемся списке hello учетной записи.

**Выберите подписку** -выберите hello toouse подписки для развертывания.
   
## <a name="settings-page---common-settings-tab"></a>Страница "Параметры": вкладка "Общие параметры"   

![Общие параметры](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**Облачная служба** -с помощью раскрывающегося списка hello, либо выберите существующее облако службы или выберите  **&lt;Создать >**и создать облачную службу. Hello центра обработки данных отображаются в круглых скобках для каждой облачной службы. Рекомендуется, hello местоположение центра обработки данных для hello облачной службы быть hello же, как hello местоположение центра обработки данных для учетной записи хранения hello (Дополнительные параметры).  

**Среда**: выберите **Рабочая среда** или **Промежуточная среда**. Выберите приложение hello в промежуточной среде, если требуется, чтобы toodeploy в тестовой среде. 

**Конфигурация сборки**: выберите **Отладка** или **Выпуск**.

**Конфигурация службы**: выберите **Облако** или **Локально**.
   
**Включить удаленный рабочий стол для всех ролей** -Проверьте этот параметр, если требуется, чтобы могли tooremotely toobe подключение toohello службы. Этот параметр в основном используется для устранения неполадок. Если флажок установлен, hello **конфигурация удаленного рабочего стола** откроется диалоговое окно. Выберите hello **параметры** конфигурации hello toochange ссылку.
   
**Включить веб-развертывание для всех веб-ролей** -Проверьте этот параметр, tooenable веб-развертывания для службы hello. Необходимо выбрать hello **включить удаленный рабочий стол для всех ролей** параметр toouse эту функцию. Дополнительные сведения см. в статье [[Публикация облачной службы с помощью инструментов Azure](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx). 

## <a name="settings-page---advanced-settings-tab"></a>Страница "Параметры": вкладка "Дополнительные параметры"

![Дополнительные параметры](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Метка развертывания** -примите имя по умолчанию hello, или введите имя по своему выбору. tooappend hello даты toohello метка развертывания, оставьте hello флажком. 
   
**Учетная запись хранения** — выберите hello toouse учетной записи хранилища для этого развертывания **&lt;создать новый > toocreate учетной записи хранилища. Hello центра обработки данных отображаются в круглых скобках для каждой учетной записи хранилища. Рекомендуется, hello местоположение центра обработки данных для hello учетной записи хранилища быть hello таким же как hello местоположение центра обработки данных для hello облачной службы (Общие параметры).  
   
Hello учетной записи хранилища Azure сохраняет hello пакета для развертывания приложения hello. После развертывания приложения hello hello пакет удаляется из учетной записи хранения hello.

**Удалить развертывание при сбое** -выберите этот параметр toohave hello развертывание удалены все ошибки, возникающие во время публикации. Это должен быть установлен, если требуется toomaintain постоянного виртуального IP-адреса для облачной службы.

**Обновление развертывания** -выберите этот параметр, если требуется toodeploy только обновленные компоненты. Этот тип развертывания выполняется быстрее, чем полное развертывание. Если требуется toomaintain постоянного виртуального IP-адреса для облачной службы, он должен быть установлен. 

**Параметры обновления развертывания -** -это диалоговое окно используется toofurther укажите, каким образом обновить toobe ролей hello. При выборе **добавочное обновление**, каждый экземпляр приложения настолько обновленные один за другим, это приложение hello доступна всегда. При выборе **одновременное обновление**, все экземпляры приложения обновляются в hello то же время. Одновременное обновление выполняется быстрее, но службы могут быть недоступны во время процесса обновления hello. 

![Параметры развертывания](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**Включить IntelliTrace** -укажите, следует ли tooenable IntelliTrace. С помощью IntelliTrace можно записывать в журнал расширенные отладочные сведения для экземпляра роли при его запуске в Azure. При необходимости toofind hello причину проблемы, можно использовать toostep журналы IntelliTrace hello по коду из Visual Studio, как если бы оно было запущено в Azure. Дополнительные сведения об использовании IntelliTrace см. в статье [Отладка опубликованной облачной службы Azure с помощью Visual Studio и IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md). 

**Включить профилирование** -укажите, следует ли tooenable профилирование производительности. Hello профилировщик Visual Studio позволяет tooget глубокий анализ вычислительных аспектов hello как облачная служба выполняется. Дополнительные сведения об использовании hello профилировщик Visual Studio см. в разделе [тестирование производительности облачной службы Azure для hello](./vs-azure-tools-performance-profiling-cloud-services.md).

**Включить удаленный отладчик для всех ролей** -укажите, следует ли tooenable удаленную отладку. Дополнительные сведения об отладке облачных служб с помощью Visual Studio см. в статье [Отладка облачной службы или виртуальной машины Azure в Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Страница "Параметры диагностики"

![Параметры диагностики](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

Диагностика позволяет tootroubleshoot облачной службы Azure (или виртуальная машина Azure). Дополнительные сведения о системе диагностики см. в статье [Настройка системы диагностики для облачных служб и виртуальных машин Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Дополнительные сведения о службе Application Insights см. в статье [Что такое Azure Application Insights?](./application-insights/app-insights-overview.md)

## <a name="summary-page"></a>Страница "Сводка"

![Сводка](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Использовать профиль** -toocreate можно выбрать профиль публикации из hello параметры, которые вы выбрали. Например, можно создать один профиль для тестовой среды, а другой — для рабочей. toosave этот профиль, выберите hello **Сохранить** значок. Hello мастер создает профиль hello и сохраняет его в проект Visual Studio hello. Имя профиля hello toomodify, откройте hello **использовать профиль** , а затем выберите **< Управление >**.
   
   > [!NOTE]
   > Hello профиль публикации отображается в обозревателе решений в Visual Studio, а параметры профиля hello записываются tooa файл с расширением azurepubxml. Параметры сохраняются как атрибуты XML-тегов.
   > 
   > 

## <a name="publishing-your-application"></a>Публикация приложения

После настройки всех параметров hello для развертывания проекта выберите **публикации** внизу hello диалогового окна "hello". Можно отслеживать состояние процесса hello в hello **выходной** в Visual Studio.

## <a name="next-steps"></a>Дальнейшие действия
- [Миграция и публикация веб-приложения tooan облачной службы Azure из Visual Studio](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [Узнайте, как Visual Studio toouse toopublish Azure облачной службы](./vs-azure-tools-publishing-a-cloud-service.md)
- [Отладка опубликованной облачной службы Azure с помощью Visual Studio и IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [Тестирование производительности облачной службы Azure для hello](./vs-azure-tools-performance-profiling-cloud-services.md)
- [Настройка системы диагностики для облачных служб и виртуальных машин Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) 
- [Что такое Azure Application Insights?](./application-insights/app-insights-overview.md)