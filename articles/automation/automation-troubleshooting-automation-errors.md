---
title: "Общие службы автоматизации Azure выдает aaaTroubleshooting | Документы Microsoft"
description: "Эта статья содержит сведения о toohelp поиск и устранение распространенных ошибок автоматизации Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: "ошибка службы автоматизации, устранение неполадок, проблема"
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Устранение распространенных проблем службы автоматизации Azure 
В этой статье содержатся сведения об устранении проблем распространенные ошибки, которые могут возникнуть в службе автоматизации Azure и предлагает возможные решения tooresolve их.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Ошибки, связанные с аутентификацией, при работе с модулями Runbook службы автоматизации Azure
### <a name="scenario-sign-in-tooazure-account-failed"></a>Сценарий: Сбой учетной записи входа tooAzure
**Ошибка:** ошибка hello «Unknown_user_type: неизвестный тип пользователя» при работе с помощью командлетов Add-AzureAccount или AzureRmAccount входа hello.

**Причина ошибки hello:** Эта ошибка возникает, если имя актива учетных данных hello является недопустимым или если hello имя пользователя и пароль, использование учетных данных службы toosetup hello автоматизации, являются недопустимыми.

**Советы по устранению неполадок:** в заказ toodetermine проблема, принимают hello следующие шаги:  

1. Убедитесь, что у вас нет специальные символы, включая hello  **@**  знаку в том, что вы используете tooconnect tooAzure активов имя hello автоматизации учетных данных.  
2. Проверьте, что можно использовать hello имя пользователя и пароль, который хранится в учетных данных службы автоматизации Azure hello в редакторе локальной интегрированную среду Сценариев PowerShell. Это можно сделать, выполнив следующие командлеты в интегрированной среде Сценариев PowerShell hello hello:  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. Локальный сбой проверки подлинности означает, что учетные данные Azure Active Directory были указаны неправильно. См. слишком[проверки подлинности с помощью Azure Active Directory tooAzure](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) post tooget hello Azure Active Directory учетной записи блога правильно настроить.  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>Сценарий: Не удается toofind hello подписки Azure
**Ошибка:** возникнет ошибка hello «hello подписке с именем ``<subscription name>`` не найден» при работе с командлетами Select-AzureSubscription или выберите AzureRmSubscription hello.

**Причина ошибки hello:** Эта ошибка возникает, если имя hello подписки является недопустимым или hello Azure Active Directory пользователя, сведения о подписке tooget hello не настроена в качестве администратора подписки hello.

**Советы по устранению неполадок:** в порядке toodetermine Если прошел проверку подлинности tooAzure и имеет доступ toohello подписки вы пытаетесь tooselect, принимают hello следующие шаги:  

1. Убедитесь, что запускается hello **Add-AzureAccount** перед запуском hello **Select-AzureSubscription** командлета.  
2. Если вы по-прежнему видите это сообщение об ошибке, измените код, добавив hello **Get-AzureSubscription** командлет с соблюдением hello **Add-AzureAccount** командлета и выполнить код hello.  Теперь проверьте, если выходные данные Get-AzureSubscription hello содержит сведения о вашей подписке.  

   * Если вы не видите все сведения о подписке в выходных данных hello, это означает hello подписка не инициализирована.  
   * Если отображаются сведения о подписке hello в выходных данных hello, убедитесь, что вы используете hello правильное имя подписки или идентификатор с hello **Select-AzureSubscription** командлета.   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>Сценарий: Проверка подлинности tooAzure сбой, так как многофакторная проверка подлинности включена
**Ошибка:** возникнет ошибка hello «Add-AzureAccount: AADSTS50079: регистрации строгой проверки подлинности (подтверждение до) является обязательным» при проверке подлинности tooAzure с помощью Azure имени пользователя и пароля.

**Причина ошибки hello:** при наличии многофакторной проверки подлинности для учетной записи Azure, нельзя использовать tooAzure tooauthenticate пользователя Azure Active Directory.  Вместо этого необходимо toouse сертификат или tooAzure tooauthenticate участника службы.

**Советы по устранению неполадок:** toouse сертификат с hello командлетов для управления службой Azure, см. слишком[Создание и добавление сертификата toomanage Azure службы.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) toouse участника службы с помощью командлетов диспетчера ресурсов Azure, см. слишком[Создание службы с помощью портала Azure основной](../azure-resource-manager/resource-group-create-service-principal-portal.md) и [проверки подлинности участника службы с помощью диспетчера ресурсов Azure.](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>Распространенные ошибки при работе с модулями Runbook
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>Сценарий: запуск задания runbook hello была предпринята попытка три раза, но он не toostart каждый раз
**Ошибка:** runbook завершается ошибкой hello ««hello задания была предпринята попытка три раза, но его не удалось.»

**Причина ошибки hello:** Эта ошибка может вызываться hello следующих причин:  

1. Предельный объем памяти.  Мы включили ограничения на объем памяти, выделенной tooa "песочницы" [ограничения службы автоматизации](../azure-subscription-service-limits.md#automation-limits) , задания, может произойти ошибка он использует более 400 МБ памяти. 

2. Модуль несовместим.  Данная ситуация может возникать, если зависимости модуля заданы неправильно, в результате чего модуль Runbook, как правило, возвращает сообщение об ошибке "Команда не найдена" или "Не удается привязать параметр". 

**Советы по устранению неполадок:** любой hello следующие решения устранит проблему hello:  

* Рекомендованные методы toowork выходит за пределы памяти hello предназначены для рабочей нагрузки hello toosplit несколькими модулями Runbook, обрабатывает столько данных в памяти, не toowrite ненужные выходных данных из модулей Runbook или рассмотрите возможность записи в вашей PowerShell сколько контрольные точки модули Runbook рабочего процесса.  

* Требуется tooupdate Azure модули, выполнив шаги hello [как tooupdate модули Azure PowerShell в службе автоматизации Azure](automation-update-azure-modules.md).  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>Сценарий: сбой модуля Runbook из-за десериализованного объекта
**Ошибка:** runbook завершается с ошибкой hello «не удается привязать параметр ``<ParameterName>``. Не удается преобразовать hello ``<ParameterType>`` значение типа Deserialized ``<ParameterType>`` tootype ``<ParameterType>``».

**Причина ошибки hello:** Если runbook — это рабочий процесс PowerShell, он содержит сложные объекты в формате десериализованный в порядке toopersist состояния runbook Если hello рабочий процесс приостанавливается.  

**Советы по устранению неполадок:**  
Любой из следующих трех решений hello устранит эту проблему:

1. Если направив сложные объекты от одного командлета tooanother, перенос этих командлетов в InlineScript.  
2. Передача hello имя или значение, необходимое из hello сложный объект, вместо того чтобы передавать весь объект hello.  
3. Используйте модуль Runbook PowerShell, а не модуль Runbook рабочего процесса PowerShell.  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>Сценарий: Задание Runbook сбой, так как превышена квота выделенной hello
**Ошибка:** задания runbook завершается ошибкой hello «hello hello заданий за месяц общее время выполнения исчерпана квота для этой подписки».

**Причина ошибки hello:** Эта ошибка возникает при hello выполнения задания превышает 500-минутного hello свободного квоты для вашей учетной записи. Эта квота применяется типы tooall задания выполнения задач, таких как тестирование задания, запуск задания из портала hello, выполнение задания с помощью веб-перехватчиков и планирование tooexecute задания с помощью либо hello портал Azure или в центре обработки данных. см. Дополнительные сведения о ценах для автоматизации toolearn [цены автоматизации](https://azure.microsoft.com/pricing/details/automation/).

**Советы по устранению неполадок:** следует toouse более 500 минут обработки в месяц, вам потребуется toochange подписке из hello бесплатный уровень toohello базового уровня. Можно обновить toohello базового уровня, принимающий hello следующие шаги:  

1. Войдите в tooyour подписки Azure  
2. Выберите учетную запись автоматизации hello которые вы будете tooupgrade  
3. Щелкните **Параметры** > **Ценовая категория и использование** > **Ценовая категория**.  
4. На hello **выберите ценовую категорию** колонке выберите **Basic**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>Сценарий: не удается распознать командлет при выполнении модуля Runbook
**Ошибка:** runbook задание завершается с ошибкой hello»``<cmdlet name>``: hello термин ``<cmdlet name>`` не распознан как имя командлета, функции, файла скрипта или действующей программы hello.»

**Причина ошибки hello:** Эта ошибка возникает, когда подсистемы PowerShell hello не удается найти hello командлета в модуле runbook.  Возможно, hello модуль, содержащий командлет hello отсутствует учетная запись hello, имеется конфликт имен, имя runbook, или командлет hello также существует в другом модуле и автоматизации не удается разрешить имя hello.

**Советы по устранению неполадок:** любой hello следующие решения устранит проблему hello:  

* Проверьте правильность ввода имени командлета hello.  
* Убедитесь, что командлет hello существует в учетной записи автоматизации и что нет конфликтов. tooverify при его наличии, командлет hello откройте книгу в режиме редактирования и поиска hello командлета требуется toofind в библиотеке hello или запустить **Get-Command ``<CommandName>``** .  После проверки командлета hello доступных toohello учетная запись, и что имеются конфликты имен с другими командлетами или модулей Runbook, добавьте его toohello холст и убедитесь, что используется допустимый параметр, задайте в модуле runbook.  
* Если имеется конфликт имен и hello командлет доступен в двух разных модулях, можно решить эту проблему с помощью полного имени командлета hello hello. Например, можно использовать следующий формат: **имя_модуля\имя_командлета**.  
* Если выполняются hello runbook в локальной среде, в группу гибридных рабочих ролей, а затем убедитесь в том, что hello модуля или командлета устанавливается на hello компьютера, на котором размещена hello гибридной рабочей роли.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>Сценарий: Длительных runbook часто возникает ошибка с исключением hello: «hello задания не может продолжать выполнение, так как оно постоянно исключалось с hello же контрольной точки».
**Причина ошибки hello:** это сделано поведение конструктора из-за toohello «Справедливое» мониторинг процессов в автоматизации Azure, которая автоматически приостанавливает runbook, если он выполняется дольше, чем 3 часа. Однако hello возвращаемое сообщение об ошибке не поддерживает «дальнейшие действия» параметров. Модуль Runbook может быть приостановлен по целому ряду причин. Приостанавливает произойти главным образом из-за tooerrors. Например исключение в книгу, сбой сети или к ошибкам при Здравствуйте Runbook Worker при выполнении модуля runbook hello, все приведут toobe runbook hello приостановлена и начать с последней контрольной точки при возобновлении.

**Советы по устранению неполадок:** hello задокументированы tooavoid решения этой проблемы является toouse контрольные точки в рабочем процессе.  сведения слишком toolearn[рабочих процессов PowerShell обучения](automation-powershell-workflow.md#checkpoints).  Более подробно справедливое распределение процессов и контрольные точки описываются в записи блога [Azure Automation: Reliable, Fault-Tolerant Runbook Execution Using Checkpoints](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/) (Служба автоматизации Azure: надежное и отказоустойчивое выполнение модулей Runbook с помощью контрольных точек).

## <a name="common-errors-when-importing-modules"></a>Распространенные ошибки при импорте модулей
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>Сценарий: Модуль не tooimport или командлеты не может быть выполнена после импорта
**Ошибка:** модуля завершается ошибкой tooimport или импортирует успешно, но не командлеты будут извлечены.

**Причина ошибки hello:** некоторые наиболее распространенные причины, модуль может не импортировать успешно tooAzure Automation являются:  

* Структура Hello не соответствует структуре hello, автоматизации должен его toobe в.  
* модуль Hello зависит от другой модуль, который еще не развернутых tooyour учетной записи автоматизации.  
* модуль Hello отсутствует его зависимости в папке hello.  
* Hello **New AzureRmAutomationModule** командлет которого создается модуль hello tooupload используется и не указаны пути hello полный хранилища или не загружены hello модуль, используя общедоступный URL-адрес.  

**Советы по устранению неполадок:**  
Все следующие решения hello устранит проблему hello:  

* Убедитесь, что этот модуль hello соответствует кодировке hello:  
  ModuleName.Zip **->** имя_модуля или номер версии **->** (имя_модуля.psm1, имя_модуля.psd1).
* Откройте hello psd1-файл и проверить, есть ли модуль hello любые зависимости.  Если Да, отправьте эти модули toohello учетной записи автоматизации.  
* Убедитесь, что любой библиотек, на которую указывает ссылка, присутствуют в папке модуля hello.  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>Распространенные ошибки при настройке требуемого состояния (DSC)
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>Сценарий: узел находится в состоянии сбоя с ошибкой "Не найден"
**Ошибка:** hello узел имеет отчет с **сбой** состояние и ошибкой hello «hello действие hello tooget попытка из сервера https://``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction завершилось ошибкой, так как допустимую конфигурацию ``<guid>`` не найден.»

**Причина ошибки hello:** Эта ошибка обычно возникает при hello узлу присваивается имя tooa конфигурации (например ABC) вместо имени узла конфигурации (например ABC. Веб-сервер).  

**Советы по устранению неполадок:**  

* Убедитесь, что присваиваются hello узла с «имя конфигурации узла» и не hello «configuration name».  
* Можно назначить tooa узла для конфигурации узла с помощью портал Azure или с помощью командлета PowerShell.

  * В заказ tooassign tooa узел для конфигурации узла с помощью портала Azure, откройте hello **узлы DSC** колонки, затем выберите узел и выберите команду **конфигурации узла назначения** кнопки.  
  * В заказ tooassign tooa узел для конфигурации узла с помощью командлета PowerShell, используйте **AzureRmAutomationDscNode набор** командлета

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>Сценарий: при компиляции конфигурации не были созданы файлы конфигурации узла (MOF-файлы).
**Ошибка:** приостанавливает задание компиляции DSC hello. Ошибка: «Компиляция завершена успешно, но были сформированы не .mofs конфигурации узла».

**Причина ошибки hello:** при hello выражения, следующего за hello **узел** слишком оценивает ключевое слово в конфигурации hello DSC $ значение null, то будет произведено не конфигурации узла.    

**Советы по устранению неполадок:**  
Все следующие решения hello устранит проблему hello:  

* Убедитесь, что этот toohello далее выражение hello **узел** ключевое слово в определение конфигурации hello не оценивает слишком $null.  
* Если вы передаете ConfigurationData при компиляции конфигурации hello, убедитесь, что передаете hello ожидаемые значения, которые hello конфигурация требует от [ConfigurationData](automation-dsc-compile.md#configurationdata).

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>Сценарий: hello отчета узла DSC перестает отвечать состоянии «выполняется»
**Ошибка** : агент DSC выводит сообщение "Экземпляр с заданными значениями свойств не найден".

**Причина ошибки hello:** обновления вашей версии WMF и привести к повреждению WMI.  

**Советы по устранению неполадок:** , следуйте инструкциям hello hello [DSC известные проблемы и ограничения](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) toofix hello проблему.

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>Сценарий: Не удается toouse учетных данных в конфигурации DSC
**Ошибка:** с ошибкой hello приостановки задания компиляции DSC: «System.InvalidOperationException ошибка при обработке свойство «Учетные данные» типа ``<some resource name>``: преобразуя и сохраняя зашифрованный пароль в виде обычного текста допустим только в том случае, если PSDscAllowPlainTextPassword устанавливается tootrue».

**Причина ошибки hello:** вы уже использовали учетных данных в конфигурации, но не предоставил правильную **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue для каждого узла Конфигурация.  

**Советы по устранению неполадок:**  

* Убедиться, что toopass становились hello правильную **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue для каждой конфигурации узла, упомянутые в конфигурации hello. Дополнительные сведения см. в разделе слишком[средств в Azure Automation DSC](automation-dsc-compile.md#assets).

## <a name="next-steps"></a>Дальнейшие действия
Если были выполнены hello выше шаги по устранению неполадок и не может найти ответ hello, можно просмотреть hello Дополнительные варианты поддержки ниже.

* Обратитесь за помощью к экспертам Azure. Отправить вашей проблемы toohello [форумы MSDN Azure или переполнения стека.](https://azure.microsoft.com/support/forums/).
* Отправьте запрос в службу поддержки Azure Go toohello [узла Azure поддерживает](https://azure.microsoft.com/support/options/) и нажмите кнопку **получение поддержки** под **технические и выставление счетов поддержки**.
* Опубликуйте запрос на сценарий на странице [Центр скриптов](https://azure.microsoft.com/documentation/scripts/) , если вы ищете модуль интеграции или определенное решение для службы автоматизации Azure, в котором используются модули Runbook.
* Оставьте свой отзыв или запрос на ту или иную функцию для службы автоматизации Azure на [странице отзывов](https://feedback.azure.com/forums/34192--general-feedback).
