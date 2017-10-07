---
title: "Автоматизация DSC непрерывное развертывание с Chocolatey aaaAzure | Документы Microsoft"
description: "Непрерывное развертывание DevOps с помощью Automation DSC Azure и диспетчера пакетов Chocolatey.  Пример с полным шаблоном ARM в формате JSON и исходным кодом PowerShell."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: c0baa411-eb76-4f91-8d14-68f68b4805b6
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/29/2016
ms.author: golive
ms.openlocfilehash: 60af52af5f834fd48e3a0dc4677919397b53f0f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="usage-example-continuous-deployment-toovirtual-machines-using-automation-dsc-and-chocolatey"></a>Пример использования: TooVirtual непрерывное развертывание компьютеров с помощью DSC службы автоматизации и Chocolatey
В мире DevOps существует множество средств tooassist с различными точками в конвейере hello непрерывной интеграции.  Конфигурация Azure Automation требуемого состояния (DSC) является приветствия параметры toohello новый добавления, можно использовать команды DevOps.  В этой статье показана настройка непрерывного развертывания для компьютера Windows.  Можно легко расширить tooinclude метод hello столько компьютеров Windows, необходимости в роли hello (веб-сайта, например), а также из отсутствует tooadditional также ролей.

![Непрерывное развертывание для виртуальных машин IaaS](./media/automation-dsc-cd-chocolatey/cdforiaasvm.png)

## <a name="at-a-high-level"></a>На высоком уровне
Эта схема включает немало действий, но, к счастью, их можно разбить на два основных процесса: 

* Написание кода и его тестирование, создание и публикация установочные пакеты для основной и вспомогательной версии системы hello. 
* Создание и управление ими виртуальных машин, которые будут устанавливаться и выполнения кода hello в пакеты hello.  

Эти основные процессы выполняются в месте, он после обновления hello короткий шаг tooautomatically пакет, запущенный на любой конкретной виртуальной Машины, как новые версии созданы и развертываются.

## <a name="component-overview"></a>Обзор компонентов
Пакет диспетчеры, такие как [apt get](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool) , довольно хорошо известен в Linux Здравствуй, мир, но не слишком много ресурсов в мире Windows hello.  [Chocolatey](https://chocolatey.org/) такого результата, а также Скотт Хансельман [блог](http://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx) на hello раздел является отличным введение.  По сути Chocolatey позволяет tooinstall пакеты из центрального репозитория пакетов в системе Windows, с помощью командной строки hello.  Вы можете создать собственный репозиторий и управлять им, а Chocolatey будет устанавливать пакеты из любого указанного вами количества репозиториев.

Требуемого состояния (DSC) ([Обзор](https://technet.microsoft.com/library/dn249912.aspx)) — это средство PowerShell, который позволяет вам toodeclare hello необходимую конфигурацию для машины.  Например, вы можете указать, что нужно установить Chocolatey и IIS, открыть порт 80 и установить версию 1.0.0 вашего веб-сайта.  Hello DSC локальный диспетчер конфигураций (LCM) развертывает этой конфигурации. Опрашивающий сервер DSC содержит хранилище конфигураций для компьютеров. Hello LCM на каждом компьютере флажок в периодически toosee его конфигурация соответствует hello хранимой. Он сообщения о состоянии или попытка toobring hello машины обратно в соответствие с сохраненной конфигурации hello. Вы можете изменить hello сохраненной конфигурации на hello опрашивающего сервера toocause компьютер или набор toocome машины в соответствие с hello изменения конфигурации.

Служба автоматизации Azure является управляемой службой в Microsoft Azure, которая позволяет tooautomate различных задач с помощью Runbook, узлы, учетные данные, ресурсы и ресурсы, например расписания и глобальные переменные. Azure Automation DSC расширяет автоматизация средства PowerShell DSC tooinclude возможностей.  Вот прекрасный [обзор](automation-dsc-overview.md)на эту тему.

Ресурс DSC — это модуль кода, который имеет определенные возможности, такие как управление сетевыми подключениями, Active Directory или SQL Server.  Hello Chocolatey ресурса DSC знает, как tooaccess сервера NuGet (среди прочих), загрузить пакеты установки пакетов и т. д.  Существует множество других ресурсов DSC в hello [коллекции PowerShell](http://www.powershellgallery.com/packages?q=dsc+resources&prerelease=&sortOrder=package-title).  Эти модули установлены на опрашивающем сервере Automation DSC Azure (вручную), поэтому их можно использовать в ваших конфигурациях.

Шаблоны Resource Manager предоставляют декларативный способ создания инфраструктуры с помощью сетей, подсетей, сетевой безопасности и маршрутизации, подсистем балансировки нагрузки, сетевых карт, виртуальных машин и т. д.  Вот [статье](../azure-resource-manager/resource-manager-deployment-model.md) , сравнивает hello (декларативной) модели развертывания диспетчера ресурсов с hello управления службами Azure (ASM или Классическая) развертывания модели (принудительные), а также обсуждаются основные ресурсы hello поставщики, вычислений, хранилища и сети.

Одна важная особенность шаблона диспетчера ресурсов является tooinstall его возможности расширения ВМ в hello виртуальной Машины, как он задан.  Расширение VM предоставляет определенные возможности, такие как выполнение пользовательского сценария, установка антивирусного программного обеспечения или выполнение сценария конфигурации DSC.  Существует много других типов расширений VM.

## <a name="quick-trip-around-hello-diagram"></a>Быстрый trip вокруг диаграммы hello
Начиная с верхней hello, писать код, построения и тестирования, а затем создайте пакет установки.  Chocolatey может обрабатывать пакеты установки различных типов, например MSI, MSU и ZIP.  И иметь hello всю мощь PowerShell toodo hello фактической установки, если собственных возможностей Chocolatey не совсем вверх tooit.  Перевести hello пакет в неизвестной точке достижимым — репозитория пакетов.  Он может располагаться где угодно. Например, в этом примере используется общая папка в учетной записи хранилища больших двоичных объектов Azure.  Chocolatey работает непосредственно с серверами NuGet и некоторыми другими серверами в рамках управления метаданными пакета.  [В этой статье](https://github.com/chocolatey/choco/wiki/How-To-Host-Feed) описаны параметры hello.  В этом примере используется NuGet.  Nuspec — это метаданные о пакетах.  Hello Nuspec «компилируются» в его NuPkg и хранящихся на сервере NuGet.  Когда конфигурацию запрашивает пакет по имени, а также ссылается на сервер NuGet, hello Chocolatey ресурса DSC (в настоящее время на hello ВМ) извлекает пакет hello и устанавливает его автоматически.  Можно также запросить определенную версию пакета.

В hello нижней левой части рисунка hello имеется шаблон диспетчера ресурсов Azure (ARM).  В этом примере использования hello расширения виртуальной Машины регистрирует hello виртуальной Машины с hello Azure Automation DSC опрашивающего сервера (то есть опрашивающего сервера) в качестве узла.  Hello конфигурация хранится в hello опрашивающего сервера.  На самом деле это двойное хранение: в виде обычного текста и в виде компиляции в MOF-файле (для тех, кто имеет опыт работы с такими файлами).  В портале hello hello MOF — «конфигурация узла» (как противоположность toosimply «конфигурация»).  Он является hello артефакт, связанный с узлом, узел hello будете знать его конфигурации.  Ниже приведены сведения показывают, как tooassign hello toohello конфигурации каждого узла.

Скорее всего вы выполняете уже бит hello вверху hello или большую его часть.  Создание hello nuspec, компиляции и сохранить их на сервере NuGet — это небольшие вещь.  Кроме того, вы уже управляете виртуальными машинами.  Получение hello следующего шага toocontinuous развертывания требуется настройка опрашивающего сервера hello (один раз), регистрирует узлы (один раз) и создание и хранение hello конфигурации существует (первоначально).  Как пакеты будут обновлены и развернуты репозитория toohello обновите hello конфигурации и конфигурации узлов в hello опрашивающего сервера (повторите при необходимости).

Начинать работу с шаблона ARM не обязательно.  Нет регистрации виртуальных машин в hello опрашивающего сервера и всех остальных hello toohelp командлетов PowerShell. Дополнительные сведения см. в статье [Подключение компьютеров для управления с помощью Azure Automation DSC](automation-dsc-onboarding.md).

## <a name="step-1-setting-up-hello-pull-server-and-automation-account"></a>Шаг 1: Настройка hello опрашивающего сервера и автоматизации учетной записи
Проверкой подлинности командной строки PowerShell (Add-AzureRmAccount): (может занять несколько минут пока Настройка hello опрашивающего сервера)

    New-AzureRmResourceGroup –Name MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES
    New-AzureRmAutomationAccount –ResourceGroupName MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES –Name MY-AUTOMATION-ACCOUNT 

Можно поместить ваша учетная запись автоматизации в любые hello следующих областей (также называемого местоположение): восточная часть США 2, центральных штатах юга США, Вирджиния государственных организаций США, Западная Европа, Юго-Восточная Азия, восток Японии, центральной Индии и Юго-Восточная Австралия, Канады центра Северной Европе.

## <a name="step-2-vm-extension-tweaks-toohello-arm-template"></a>Шаг 2: Расширение ВМ модификации toohello шаблон ARM
Сведения о регистрации виртуальной Машины (с помощью расширения PowerShell DSC VM hello), в [шаблона быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/dsc-extension-azure-automation-pullserver).  Этот шаг регистрирует новый ВМ hello опрашивающий сервер в список hello узлов DSC.  Часть этой регистрации: необходимо указать hello конфигурации применены toobe toohello каждого узла.  Эта конфигурация узла нет tooexist еще в hello опрашивающего сервера, поэтому он действителен шаг 4 — где это делается для hello первый раз.  Однако здесь на этапе 2 необходима toohave решение hello имя узла hello и hello имя конфигурации hello.  В этом примере использования hello узел является «isvbox» и «ISVBoxConfig» hello настроен.  Поэтому имя конфигурации узла hello (указанный в DeploymentTemplate.json toobe) — «ISVBoxConfig.isvbox».  

## <a name="step-3-adding-required-dsc-resources-toohello-pull-server"></a>Шаг 3: Добавление необходимых опрашивающего сервера DSC ресурсы toohello
Hello коллекции PowerShell — инструментированного tooinstall ресурсов DSC в учетную запись службы автоматизации Azure.  Перейдите toohello ресурсов и щелкните кнопку «Развернуть tooAzure автоматизации» hello.

![Пример из коллекции PowerShell](./media/automation-dsc-cd-chocolatey/xNetworking.PNG)

Другим способом все добавленные toohello портал Azure позволяет toopull в новый или существующий модулями обновления. Пролистайте ресурсов учетной записи автоматизации hello, Плитка активы hello и наконец hello модули плитки.  значок обзора коллекции Hello позволяет toosee hello список модулей в галерее hello, перейти к подробным сведениям и в конечном счете импортируйте в вашей учетной записи автоматизации. Это является tookeep хорошим способом модули вверх toodate из tootime времени. И функцию импорта hello проверяет зависимости с другими tooensure модули, ничего не получает синхронизированы.

Или не существует подхода вручную hello.  Структура папок Hello модуля интеграции для компьютеров Windows PowerShell немного отличается от структуры папок hello ожидаемый hello автоматизации Azure.  Некоторые параметры вам придется настроить самостоятельно.  Но это несложно, и выполняется только один раз для каждого ресурса (если не требуется, чтобы tooupgrade его в будущем.)  Дополнительные сведения о разработке модулей интеграции PowerShell см. в статье [Authoring Integration Modules for Azure Automation](https://azure.microsoft.com/blog/authoring-integration-modules-for-azure-automation/) (Разработка модулей интеграции для службы автоматизации Azure).

* Установка модуля hello, необходимое на рабочей станции следующим образом:
  * Установите [Windows Management Framework 5](http://aka.ms/wmf5latest) (не требуется для Windows 10).
  * `Install-Module –Name MODULE-NAME`< — грабс hello модуля из коллекции PowerShell hello 
* Скопировать папку модуля hello из `c:\Program Files\WindowsPowerShell\Modules\MODULE-NAME` tooa временной папке 
* Удалить из главной папки hello примеров и документации 
* ZIP-папки основной hello, точно именования hello ZIP-файл hello же, как папка hello 
* Поместите hello ZIP-файл в достижимым расположении HTTP, например хранилище больших двоичных объектов в учетной записи хранилища Azure.
* Выполните эту команду PowerShell:
  
      New-AzureRmAutomationModule `
          -ResourceGroupName MY-AUTOMATION-RG -AutomationAccountName MY-AUTOMATION-ACCOUNT `
          -Name MODULE-NAME –ContentLink "https://STORAGE-URI/CONTAINERNAME/MODULE-NAME.zip"

пример Hello включены выполняет следующие действия для cChoco и xNetworking. В разделе hello [заметки](#notes) для специальной обработки для cChoco.

## <a name="step-4-adding-hello-node-configuration-toohello-pull-server"></a>Шаг 4: Добавление hello узел toohello опрашивающего сервера
Нет ничего особенного hello первый раз импортировать конфигурацию в hello опрашивающего сервера и компиляции.  Все последующие импорта/компиляции из hello конфигурации выглядят точно hello таким же.  Каждый раз, ваш пакет обновления и требуется его tooproduction выполнением этого действия после того как убедитесь файл конфигурации hello toopush правильность — включая hello новой версии пакета.  Ниже приведен файл конфигурации hello и PowerShell.

ISVBoxConfig.ps1:

    Configuration ISVBoxConfig 
    { 
        Import-DscResource -ModuleName cChoco 
        Import-DscResource -ModuleName xNetworking

        Node "isvbox" {   

            cChocoInstaller installChoco 
            { 
                InstallDir = "C:\choco" 
            }

            WindowsFeature installIIS 
            { 
                Ensure="Present" 
                Name="Web-Server" 
            }

            xFirewall WebFirewallRule 
            { 
                Direction = "Inbound" 
                Name = "Web-Server-TCP-In" 
                DisplayName = "Web Server (TCP-In)" 
                Description = "IIS allow incoming web site traffic." 
                DisplayGroup = "IIS Incoming Traffic" 
                State = "Enabled" 
                Access = "Allow" 
                Protocol = "TCP" 
                LocalPort = "80" 
                Ensure = "Present" 
            }

            cChocoPackageInstaller trivialWeb 
            {            
                Name = "trivialweb" 
                Version = "1.0.0" 
                Source = “MY-NUGET-V2-SERVER-ADDRESS” 
                DependsOn = "[cChocoInstaller]installChoco", 
                "[WindowsFeature]installIIS" 
            } 
        }    
    }

New-ConfigurationScript.ps1:

    Import-AzureRmAutomationDscConfiguration ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -SourcePath C:\temp\AzureAutomationDsc\ISVBoxConfig.ps1 ` 
        -Published –Force

    $jobData = Start-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -ConfigurationName ISVBoxConfig 

    $compilationJobId = $jobData.Id

    Get-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -Id $compilationJobId

Эти действия приводят к новой конфигурации узла с именем «ISVBoxConfig.isvbox», размещенной на hello опрашивающего сервера.  Имя конфигурации узла Hello построен как «configurationName.nodeName».

## <a name="step-5-creating-and-maintaining-package-metadata"></a>Шаг 5. Создание и поддержка метаданных пакета
Для каждого пакета, помещенному в hello репозитория пакетов необходимо nuspec, описывающим его.  Эти метаданные Nuspec следует компилировать и хранить на сервере NuGet. Этот процесс описан [здесь](http://docs.nuget.org/create/creating-and-publishing-a-package).  В качестве сервера NuGet можно использовать сайт MyGet.org.  Это платная служба, но начальные единицы хранения предоставляются бесплатно.  На сайте NuGet.org вы найдете инструкции по установке сервера NuGet для закрытых пакетов.

## <a name="step-6-tying-it-all-together"></a>Шаг 6. Сборка
Каждый раз версии передает QA и утверждена для развертывания, создается пакет hello, nuspec nupkg обновления и развертывания сервера toohello NuGet.  Кроме того hello конфигурации (шаг 4 выше) должен быть обновленные tooagree с hello новый номер версии.  Должно быть отправлено toohello опрашивающего сервера и компиляции.  С этого момента это toohello виртуальных машин, которые зависят от конфигурации toopull hello обновления и установить его.  Каждое такое обновление довольно просто и представляет собой одну-две строки кода PowerShell.  В случае Visual Studio Team Services hello некоторые из них содержатся в задачи сборки, которые можно соединять друг с другом в сборке.  Дополнительные сведения см. в [этой статье](https://www.visualstudio.com/en-us/docs/alm-devops-feature-index#continuous-delivery).  Это [в репозитории GitHub](https://github.com/Microsoft/vso-agent-tasks) Здравствуйте, сведения о различных доступных задач.

## <a name="notes"></a>Примечания
В этом примере использования начинается с виртуальной Машины с помощью универсального образа Windows Server 2012 R2 из коллекции Azure hello.  Можно запустить из любой хранимой образа, а затем настроить оттуда с hello конфигурации DSC.  Однако изменения конфигурации, который является помещенного в изображение будет гораздо сложнее, чем динамическое обновление конфигурации hello, с помощью DSC.

У вас нет toouse шаблон ARM и toouse расширения ВМ hello этот способ с виртуальных машин.  И виртуальные машины, у вас нет toobe на Azure toobe в группе управления компакт-диска.  Все, что необходим, Chocolatey будет установлен, а также hello НОК настроен на hello виртуальной Машины, она знает, где hello опрашивающего сервера.  

Конечно при обновлении пакета на виртуальной Машине, используемой в производственной среде, необходимо tootake эту виртуальную Машину из ротации во время установки обновления hello.  Это можно сделать разными способами.  Например, на виртуальной машине, которая находится под контролем балансировщика нагрузки Azure, можно добавить настраиваемый зонд.  При обновлении hello виртуальной Машины, иметь hello пробы конечную точку вернуть 400.  необходимые toocause Hello оптимизировать это изменение может быть внутри вашей конфигурации, как можно оптимизировать tooswitch обратно tooreturning 200 после завершения обновления hello "hello".

Полный исходный код для этого примера хранится в [этом проекте Visual Studio](https://github.com/sebastus/ARM/tree/master/CDIaaSVM) на сайте GitHub.

## <a name="related-articles"></a>Связанные статьи
* [Обзор DSC службы автоматизации Azure](automation-dsc-overview.md)
* [Командлеты Automation DSC Azure](https://msdn.microsoft.com/library/mt244122.aspx)
* [Подключение компьютеров для управления с помощью Azure Automation DSC](automation-dsc-onboarding.md)

