---
title: "aaaDebugging, опубликованных в Azure облачной службы в Visual Studio и IntelliTrace | Документы Microsoft"
description: "Узнайте, как toodebug облачной службы в Visual Studio и IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a>Отладка опубликованной облачной службы Azure с помощью Visual Studio и IntelliTrace
С помощью IntelliTrace можно записывать в журнал расширенные отладочные сведения для экземпляра роли при его запуске в Azure. При необходимости toofind hello причину проблемы, можно использовать toostep журналы IntelliTrace hello по коду из Visual Studio, как если бы оно было запущено в Azure. По сути записей код клавиши выполнения и среде данные IntelliTrace при приложение Azure работает как облачной службы в Azure, а также позволяет воспроизвести hello записанные данные в Visual Studio. 

IntelliTrace можно использовать, если ваше приложение Azure предназначено для .NET Framework 4 или более поздней версии и если у вас установлена среда разработки Visual Studio Enterprise. IntelliTrace собирает сведения для ваших ролей Azure. Hello виртуальных машин для этих ролей всегда запускать 64-разрядных операционных системах.

В качестве альтернативы можно использовать [удаленной отладки](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach непосредственно tooa облачной службе, запущенной в Azure.

> [!IMPORTANT]
> IntelliTrace предназначена только для отладки и не должна использоваться в рабочей среде.
> 

## <a name="configure-an-azure-application-for-intellitrace"></a>Настройка приложения Azure для IntelliTrace
tooenable IntelliTrace для приложения Azure необходимо создать и опубликовать приложение hello из проекта Visual Studio Azure. Перед публикацией tooAzure, необходимо настроить IntelliTrace для приложения Azure. Если опубликовать приложение без настройки IntelliTrace, необходимо toorepublish hello проекта. Дополнительные сведения см. в статье [Публикация облачной службы с помощью инструментов Azure](http://go.microsoft.com/fwlink/p/?LinkId=623012).

1. Когда вы будете готовы toodeploy приложения Azure, убедитесь, что целевых объектов построения задано слишком**отладки**.

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект и hello контекстном меню, выберите **публикации**.
   
1. В hello **публикации приложения Azure** диалоговое окно, выберите hello подписки Azure и выберите **Далее**.

1. В hello **параметры** страницу, выберите hello **Дополнительные параметры** вкладки.

1. Включите hello **включить IntelliTrace** параметр toocollect журналы IntelliTrace для приложения после его публикации в облаке hello.
   
1. toocustomize hello основную конфигурацию IntelliTrace, выберите **параметры** Далее слишком**включить IntelliTrace**.

    ![Ссылка на "Параметры IntelliTrace"](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. В hello **параметры IntelliTrace** диалоговое окно, можно указать какие события toolog, ли toocollect сведений о вызовах, какие toocollect модулей и процессов в журналах и о том, сколько места tooallocate toohello записи. Дополнительные сведения об IntelliTrace см. в разделе [Отладка с помощью IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).
   
    ![Параметры IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

Журнал IntelliTrace Hello представляет собой кольцевой файл журнала hello максимальный размер, указанный в параметрах IntelliTrace hello (размер по умолчанию hello составляет 250 МБ). Журналы IntelliTrace, собранные tooa файл в файловой системе hello hello виртуальной машины. Когда вы запрашиваете журналы hello, моментальный снимок берется на момент времени и загрузить tooyour локального компьютера.

После hello облачной службы Azure опубликованных tooAzure, можно определить, включен ли IntelliTrace из hello Azure узла в **обозревателя серверов**, как показано в hello после изображения:

![Обозреватель сервера: IntelliTrace включен](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a>Скачивание журналов IntelliTrace для экземпляра роли
С помощью Visual Studio можно скачать журналы IntelliTrace для экземпляра роли, выполнив следующие действия:

1. В **обозревателя серверов**, разверните hello **облачные службы** узел и найдите экземпляр роли, журналы которых нужно toodownload. 

1. Щелкните правой кнопкой мыши экземпляр роли hello и hello s контекстном меню, выберите **Просмотр журналов IntelliTrace**. 

    ![Пункт меню "Просмотр журналов IntelliTrace"](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. журналы IntelliTrace Hello являются tooa загруженного файла в каталоге на локальном компьютере. При каждом запросе журналов IntelliTrace hello, создается новый моментальный снимок. Во время загрузки журналов hello, Visual Studio отображает ход выполнения операции hello hello в hello **журнал действий Azure** окна. Как показано на следующий рисунок hello, можно развернуть элемент строку hello для hello операции toosee более подробно.

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

Вы можете продолжить toowork в Visual Studio во время загрузки журналов IntelliTrace hello. После завершения загрузки журнала hello он открывается в Visual Studio.

> [!NOTE]
> Hello журналы IntelliTrace могут содержать исключения, платформа hello создает и обрабатывает позже. Эти исключения формируются внутренним кодом платформы при обычном запуске роли, поэтому на них можно не обращать внимания.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
- [Параметры отладки облачных служб Azure](vs-azure-tools-debugging-cloud-services-overview.md)
- [Публикация облачной службы с помощью инструментов Azure](vs-azure-tools-publishing-a-cloud-service.md)