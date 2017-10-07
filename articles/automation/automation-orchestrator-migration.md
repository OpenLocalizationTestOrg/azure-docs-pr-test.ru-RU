---
title: "aaaMigrating из tooAzure Orchestrator автоматизации | Документы Microsoft"
description: "Описывает, как пакеты toomigrate Runbook и интеграции с System Center Orchestrator tooAzure автоматизации."
services: automation
documentationcenter: 
author: bwren
manager: stevenka
editor: tysonn
ms.assetid: 1a7da58c-7a98-49b5-9d9d-001a9f6e631a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2016
ms.author: bwren
ms.openlocfilehash: 797b50067ef2aa68470760e99d494b89ab7baacf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-from-orchestrator-tooazure-automation-beta"></a>Миграция с Orchestrator tooAzure автоматизации (бета-версия)
Модули Runbook в [System Center Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) основаны на действиях из пакетов интеграции, которые созданы специально для Orchestrator, а модули Runbook службы автоматизации Azure основаны на рабочих процессах Windows PowerShell.  [Графические модули Runbook](automation-runbook-types.md#graphical-runbooks) в службе автоматизации Azure имеют аналогичные runbooks tooOrchestrator внешний вид с их действия, предоставляющий командлеты PowerShell, дочерние модули Runbook и активы.

Hello [средств миграции System Center Orchestrator](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) включает в себя средства tooassist при преобразовании Orchestrator tooAzure автоматизации модулей Runbook.  Кроме того при Runbook hello tooconverting самостоятельно, необходимо преобразовать hello пакеты интеграции с действиями hello, что hello Runbook используют модули toointegration с командлетами Windows PowerShell.  

Ниже приведен базовый процесс hello для преобразования tooAzure Orchestrator модули Runbook автоматизации.  Каждое из этих действий подробно описан в следующих разделах hello.

1. Загрузите hello [средств миграции System Center Orchestrator](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) , содержащее hello средства и модули, описанные в этой статье.
2. Импортируйте [модуль стандартных действий](#standard-activities-module) в службу автоматизации Azure.  В него входят преобразованные версии стандартных действий Orchestrator, которые могут использоваться в преобразованных модулях Runbook.
3. Импортируйте [модули интеграции System Center Orchestrator](#system-center-orchestrator-integration-modules) в службу автоматизации Azure для пакетов интеграции, используемых в модулях Runbook с доступом к System Center.
4. Преобразовать пользовательские и сторонние пакеты интеграции, с помощью hello [преобразователь пакет интеграции](#integration-pack-converter) и импортировать в службы автоматизации Azure.
5. Преобразование с помощью hello модули Runbook в Orchestrator [Runbook преобразователь](#runbook-converter) и установить в службе автоматизации Azure.
6. Вручную создайте необходимые активы Orchestrator в службе автоматизации Azure, так как hello Runbook преобразователь не выполняет преобразование этих ресурсов.
7. Настройка [гибридной рабочей ролью Runbook](#hybrid-runbook-worker) в модулях Runbook toorun преобразовать center локальных данных, будут обращаться к локальным ресурсам.

## <a name="service-management-automation"></a>Автоматизация управления службами
[Service Management Automation](http://technet.microsoft.com/library/dn469260.aspx) (SMA) хранит и запускающей модули Runbook в вашем центре обработки локальных данных, например Orchestrator и использует hello же модули интеграции в автоматизации Azure. Hello [Runbook преобразователь](#runbook-converter) преобразует модули Runbook toographical модулей Runbook в Orchestrator Впрочем, не поддерживаемые в SMA.  Вы можете установить hello [стандартного действия модуля](#standard-activities-module) и [модули интеграции System Center Orchestrator](#system-center-orchestrator-integration-modules) в SMA, но необходимо вручную [перепишите модули Runbook](http://technet.microsoft.com/library/dn469262.aspx).

## <a name="hybrid-runbook-worker"></a>гибридный компонент Runbook Worker
Модули Runbook для Orchestrator сохраняются на сервере базы данных и работают на серверах модулей Runbook, которые оба размещаются в вашем локальном центре обработки данных.  Модули Runbook в автоматизации Azure хранятся в облаке Azure hello и могут выполняться в центре локальных данных с помощью [гибридной рабочей ролью Runbook](automation-hybrid-runbook-worker.md).  Это будет обычно выполнение модулей Runbook, преобразованные из Orchestrator, поскольку они являются спроектированный toorun на локальных серверах.

## <a name="integration-pack-converter"></a>Преобразователь пакета интеграции
Hello преобразователь пакет интеграции преобразует пакетов интеграции, которые были созданы с помощью hello [пакета Orchestrator Integration Toolkit (OIT)](http://technet.microsoft.com/library/hh855853.aspx) toointegration модулей на основании Windows PowerShell, который может быть импортирован в службу автоматизации Azure или Service Management Automation.  

При запуске hello преобразователь пакет интеграции, осуществляется с помощью мастера, который позволит вам tooselect файл интеграции с пакетом обновления (.oip).  приветствия мастера, то список действий hello, включенные в этот пакет интеграции и позволяет tooselect, в которой будут перенесены.  После завершения мастера hello, она создает модуль интеграции, содержащий соответствующий командлет для каждого из действий hello в hello исходного пакета интеграции.

### <a name="parameters"></a>Параметры
Все свойства действия в пакет интеграции hello, преобразованный tooparameters hello соответствующий командлет в модуле интеграции hello.  У командлетов Windows PowerShell есть набор [общих параметров](http://technet.microsoft.com/library/hh847884.aspx) , который может использоваться со всеми командлетами.  Например, hello - параметр Verbose вызывает командлет toooutput подробные сведения о его работе.  Командлет не может иметь параметр с точно такое же имя в качестве общего параметра hello.  Если свойства hello одинаковые имена, как общий параметр заданы действие, hello мастер предложит вы tooprovide другое имя для параметра hello.

### <a name="monitor-activities"></a>Действия Monitor
Мониторинг Runbook в Orchestrator, начинающихся [наблюдения за активностью](http://technet.microsoft.com/library/hh403827.aspx) и выполняться непрерывно toobe ожидания вызывается на определенное событие.  Службы автоматизации Azure не поддерживает runbooks монитора, поэтому все действия монитора в пакете интеграции hello не будут преобразованы.  Вместо этого командлет заполнитель создается в модуле интеграции hello для hello наблюдение за активностью.  Этот командлет не имеет функциональных возможностей, но разрешается toobe установлены все преобразованные runbook, которые его используют.  Этот runbook не будет возможности toorun в службе автоматизации Azure, но его также можно установить, чтобы его можно изменить.

### <a name="integration-packs-that-cannot-be-converted"></a>Пакеты интеграции, которые не могут быть преобразованы
Не удается преобразовать пакеты интеграции, которые не были созданы с помощью пакета OIT с hello преобразователь пакета интеграции. Кроме того, на данный момент оно не может преобразовывать некоторые пакеты интеграции, предоставляемые Майкрософт.  Преобразованные версии этих пакетов интеграции [доступны для загрузки](#system-center-orchestrator-integration-modules) , а значит могут быть установлены в службе автоматизации Azure или в средстве автоматизации управления службами.

## <a name="standard-activities-module"></a>модуль стандартных действий
Orchestrator содержит набор [стандартных действий](http://technet.microsoft.com/library/hh403832.aspx) , не включенных в пакет интеграции, которые, однако, используются во многих модулях Runbook.  модуль Hello стандартных действий — модуль интеграции, который включает в себя командлет эквивалентные каждое из этих действий.  Перед импортом любых преобразованных модулей Runbook, использующих стандартные действия, необходимо установить этот модуль интеграции службы автоматизации Azure.

В дополнение к этому toosupporting преобразовать модули Runbook, hello командлеты в модуле hello стандартных действий может использоваться кем-то знакомы с Orchestrator toobuild новых модулей Runbook в автоматизации Azure.  Хотя функции hello всех hello стандартных действий могут выполняться с помощью командлетов, они могут работать по-разному.  Hello командлеты в стандартных действий hello преобразовать модуль будет работать hello же, как соответствующие действия и используйте hello такими же параметрами.  Это может помочь hello существующих Orchestrator runbook для автора в их tooAzure перехода Runbook автоматизации.

## <a name="system-center-orchestrator-integration-modules"></a>модули интеграции System Center Orchestrator
Корпорация Майкрософт предоставляет [пакеты интеграции](http://technet.microsoft.com/library/hh295851.aspx) для создания компонентов System Center tooautomate модулей Runbook и других продуктов Майкрософт.  Некоторые из этих пакетов интеграции в настоящее время основаны на пакета OIT, но не может быть в данный момент преобразованный toointegration модули из-за проблемы.  [Модули интеграции System Center Orchestrator](https://www.microsoft.com/download/details.aspx?id=49555) включают преобразованные версии этих пакетов интеграции, которые можно импортировать в службу автоматизации Azure и в средство автоматизации управления службами.  

Каждой версии RTM hello этого инструмента обновленные версии пакетов интеграции hello для пакета OIT, который может быть преобразован с приветствия преобразователь пакета интеграции будут опубликованы.  Рекомендации также будет предоставляться в преобразовании модулей Runbook с помощью действий из пакетов интеграции hello не на основе пакета OIT tooassist.

## <a name="runbook-converter"></a>Runbook Converter
Hello Runbook преобразователь преобразует модули Runbook в Orchestrator в [графические модули Runbook](automation-runbook-types.md#graphical-runbooks) , могут быть импортированы в автоматизации Azure.  

Преобразователь Runbook реализуется в виде модуля PowerShell с помощью командлета вызывается **ConvertFrom SCORunbook** , выполняет преобразование hello.  При установке средства hello, он создаст сеанса PowerShell tooa ярлык, который загружает hello командлета.   

Ниже является основной процесс tooconvert hello модуля runbook Orchestrator и импортировать его в службе автоматизации Azure.  Hello следующих разделах предоставляются дополнительные сведения об использовании средства hello и работе с модулями Runbook преобразованный.

1. Экспортируйте один или несколько модулей Runbook в Orchestrator.
2. Получите модули интеграции для всех действий в hello runbook.
3. Преобразуйте Runbook Orchestrator hello в экспортированном файле hello.
4. Просмотрите сведения в журналах toovalidate hello преобразования и toodetermine любые необходимые задачи вручную.
5. Импортируйте преобразованные модули Runbook в службу автоматизации Azure.
6. Создайте все необходимые средства в службе автоматизации Azure.
7. Измените hello runbook в автоматизации Azure toomodify любые необходимые действия.

### <a name="using-runbook-converter"></a>Использование преобразователя модулей Runbook
Здравствуйте, синтаксис **ConvertFrom SCORunbook** выглядит следующим образом:

    ConvertFrom-SCORunbook -RunbookPath <string> -Module <string[]> -OutputFolder <string>

* RunbookPath - путь toohello экспорта файла содержащего tooconvert hello модулей Runbook.
* Модуль — запятыми список интеграции модулей, содержащих действия в модулях Runbook hello.
* OutputFolder - toocreate папки toohello путь преобразовать графические модули Runbook.

Следующая команда преобразует hello Runbook в файл экспорта, который вызывается Hello **MyRunbooks.ois_export**.  Эти модули Runbook используют hello Active Directory и пакеты интеграции Data Protection Manager.

    ConvertFrom-SCORunbook -RunbookPath "c:\runbooks\MyRunbooks.ois_export" -Module c:\ip\SystemCenter_IntegrationModule_ActiveDirectory.zip,c:\ip\SystemCenter_IntegrationModule_DPM.zip -OutputFolder "c:\runbooks"


### <a name="log-files"></a>Файлы журналов
Hello Runbook преобразователь создаст следующие файлы журнала в hello hello местоположения hello преобразовать runbook.  Если hello файлы уже существуют, они будут перезаписаны данными из hello последнее преобразование.

| Файл | Оглавление |
|:--- |:--- |
| Преобразователь модулей Runbook — Progress.log |Подробные шаги hello преобразования, включая сведения для каждого действия успешно преобразованных и предупреждения для каждого действия, не преобразуются. |
| Преобразователь модулей Runbook — Summary.log |Сводка hello последнее преобразование, включая любые предупреждения и дальнейшие задачи, требующие tooperform, таких как создание переменную, необходимую для преобразования hello runbook. |

### <a name="exporting-runbooks-from-orchestrator"></a>Экспорт модулей Runbook из Orchestrator
Hello преобразователь Runbook работает с файлом экспорта из Orchestrator, который содержит один или несколько модулей Runbook.  В файле экспорта hello создаст соответствующий runbook службы автоматизации Azure для каждого модуля runbook Orchestrator.  

tooexport runbook в Orchestrator, щелкните правой кнопкой мыши имя hello hello runbook в Runbook Designer и выберите **Экспорт**.  tooexport всех модулей Runbook в папке, щелкните правой кнопкой мыши имя hello hello папку и выберите пункт **Экспорт**.

### <a name="runbook-activities"></a>Действия Runbook
Hello Runbook преобразователь преобразует каждое действие в hello Orchestrator runbook tooa соответствующему действию в автоматизации Azure.  Для тех действий, которые не могут быть преобразованы действия заполнитель создается в runbook hello с текст предупреждения.  После импорта hello преобразовать runbook в автоматизации Azure, необходимо заменить любой из этих действий допустимые действия, выполняющие hello необходимые функциональные возможности.

Все действия в Orchestrator в hello [стандартного действия модуля](#standard-activities-module) будут преобразованы.  В то же время некоторые стандартные действия Orchestrator не входят в этот модуль и не подвергаются преобразованию.  Например **Отправка события платформы** не имеет службы автоматизации Azure эквивалента поскольку hello событий определенного tooOrchestrator.

[Мониторинг действий](https://technet.microsoft.com/library/hh403827.aspx) не преобразуются, так как она не эквивалентные toothem в службе автоматизации Azure.  Hello исключение — монитор операции [преобразовать пакеты интеграции](#integration-pack-converter) , которые будут преобразованный toohello заполнитель действия.

Все действия из [преобразовать пакет интеграции](#integration-pack-converter) будет преобразован при указании модуля интеграции toohello hello путь с hello **модули** параметра.  Пакеты интеграции System Center, можно использовать hello [модули интеграции System Center Orchestrator](#system-center-orchestrator-integration-modules).

### <a name="orchestrator-resources"></a>Ресурсы Orchestrator
Hello Runbook преобразователь преобразует только модули Runbook, не другие ресурсы Orchestrator, такие как счетчиков, переменных или соединения.  Счетчики в службе автоматизации Azure не поддерживаются.  Переменные и подключения поддерживаются, но должны создаваться вручную.  файлы журналов Hello будет содержат сведения о hello runbook требует таких ресурсов и указать, что соответствующие ресурсы, необходимые toocreate в службе автоматизации Azure для hello правильно преобразовать runbook toooperate.

Например runbook может использовать переменную toopopulate определенное значение в действии.  Hello преобразованный runbook будет преобразовать действие hello и определить переменной активов в службе автоматизации Azure с точно такое же имя как переменную Orchestrator hello hello.  Это будет помещен в hello **Runbook преобразователь - Summary.log** файл, созданный после преобразования hello.  Вам потребуется toomanually создать этого актива переменных службы автоматизации Azure перед использованием hello runbook.

### <a name="input-parameters"></a>Входные параметры
Модули Runbook в Orchestrator принимать входные параметры с hello **инициализация данных** действия.  Если преобразуемый runbook hello включает это действие, а затем [входной параметр](automation-graphical-authoring-intro.md#runbook-input-and-output) в hello Azure Automation runbook создается для каждого параметра в действии hello.  Объект [скрипта рабочего процесса управления](automation-graphical-authoring-intro.md#activities) создается действие в runbook преобразовать hello, которая получает и возвращает значение каждого параметра.  Все действия в hello runbook, использование входного параметра см. toohello выходные данные из этого действия.

Hello эта стратегия используется обусловлено toobest зеркальный hello функциональные возможности hello Orchestrator runbook.  Действия в новых графический Runbook следует обращаться напрямую tooinput параметры, используя в качестве источника входных данных модуля Runbook.

### <a name="invoke-runbook-activity"></a>Действие вызова модуля Runbook
Модули Runbook в Orchestrator запускать другие модули Runbook с hello **вызов Runbook** действия. Если преобразуемый runbook hello включает это действие и hello **ожидания завершения** был установлен, то для него создается действие runbook в runbook преобразовать hello.  Если hello **ожидания завершения** параметр не задан, то создается действие сценария в рабочий процесс, использующий **Start-AzureAutomationRunbook** toostart hello runbook.  После импорта hello преобразовать runbook в автоматизации Azure, необходимо изменить это действие с hello сведений, указанных в действии hello.

## <a name="related-articles"></a>Связанные статьи
* [System Center 2012 — Orchestrator](http://technet.microsoft.com/library/hh237242.aspx)
* [Автоматизация управления службами](https://technet.microsoft.com/library/dn469260.aspx)
* [Гибридный компонент Runbook Worker](automation-hybrid-runbook-worker.md)
* [Стандартные действия Orchestrator](http://technet.microsoft.com/library/hh403832.aspx)
* [Скачивание набора средств для миграции System Center Orchestrator](https://www.microsoft.com/en-us/download/details.aspx?id=47323)
