---
title: "aaaGetting работы с DSC службы автоматизации Azure | Документы Microsoft"
description: "Описание и примеры использования hello наиболее распространенные задачи в Azure Automation требуемого состояния (DSC)"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a>Приступая к работе с DSC службы автоматизации Azure
В этом разделе объясняется, как toodo hello наиболее распространенные задачи с Azure Automation требуемого состояния (DSC), таких как создание, Импорт и компиляции конфигурации адаптации машин слишком управлять ими и просмотр отчетов. Общие сведения о DSC службы автоматизации Azure см. в [этой статье](automation-dsc-overview.md). Документацию по DSC см. в статье [Общие сведения о службе настройки требуемого состояния Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).

Этот раздел содержит пошаговое руководство по toousing DSC службы автоматизации Azure. Если требуется, чтобы среде образец, в которой уже настроена без hello действий, описанных в этом разделе, можно использовать [hello следующий шаблон ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup). Этот шаблон позволяет настроить полнофункциональную среду DSC службы автоматизации Azure, в том числе виртуальную машину Azure, которой управляет DSC соответствующей службы.

## <a name="prerequisites"></a>Предварительные требования
toocomplete hello примеры в этом разделе, hello требуются следующие сертификаты:

* Учетная запись службы автоматизации Azure. Указания по созданию учетной записи запуска от имени пользователя для службы автоматизации Azure см. в статье [Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени](automation-sec-configure-azure-runas-account.md).
* Виртуальная машина Azure Resource Manager (неклассическая) под управлением Windows Server 2008 R2 или более поздней версии. Инструкции по созданию виртуальной Машины см. в разделе [создания первой виртуальной машине Windows в hello портал Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)

## <a name="creating-a-dsc-configuration"></a>Создание конфигурации DSC
Мы создадим простой [конфигурации DSC](https://msdn.microsoft.com/powershell/dsc/configurations) таким образом hello наличие или отсутствие hello **веб-сервера** Windows функция (IIS), в зависимости от того, как назначить узлы.

1. Запустите Windows PowerShell ISE hello (или любой текстовый редактор).
2. Введите следующий текст hello:
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. Сохраните файл как файл hello `TestConfig.ps1`.

Эта конфигурация вызывает один ресурс в каждом блоке узла hello [ресурс WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), таким образом hello наличие или отсутствие hello **веб-сервера** компонентов.

## <a name="importing-a-configuration-into-azure-automation"></a>Импорт конфигурации в службу автоматизации Azure
Затем мы будем импортируйте конфигурации hello в hello учетной записи автоматизации.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.
3. На hello **учетной записи автоматизации** колонка, щелкните **конфигураций DSC**.
4. На hello **конфигураций DSC** колонка, щелкните **Добавление конфигурации**.
5. На hello **Импорт конфигурации** колонки, обзора toohello `TestConfig.ps1` файл на своем компьютере.
   
    ![Снимок экрана: hello ** импорта конфигурации ** колонку](./media/automation-dsc-getting-started/AddConfig.png)
6. Нажмите кнопку **ОК**.

## <a name="viewing-a-configuration-in-azure-automation"></a>Просмотр конфигурации в службе автоматизации Azure
После импорта конфигурации, его можно просмотреть в hello портал Azure.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.
3. На hello **учетной записи автоматизации** колонка, щелкните **конфигураций DSC**
4. На hello **конфигураций DSC** колонка, щелкните **TestConfig** (это имя hello hello конфигурации, импортированных в предыдущей процедуре hello).
5. На hello **конфигурации TestConfig** колонка, щелкните **источник конфигурации**.
   
    ![Снимок экрана: колонка конфигурации TestConfig hello](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    Объект **источник конфигурации TestConfig** колонке откроется кода hello PowerShell для настройки hello.

## <a name="compiling-a-configuration-in-azure-automation"></a>Компилирование конфигурации в службе автоматизации Azure
Перед установкой требуемого состояния узла tooa конфигурации DSC, определяя, состояние должно быть компилируются в одну или несколько конфигураций узла (MOF-документа) и поместить в hello опрашивающего сервера DSC службы автоматизации. Подробное описание компилирования конфигураций в Azure Automation DSC см. в [этой статье](automation-dsc-compile.md). Дополнительные сведения о компилировании конфигураций см. в статье [Конфигурации DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.
3. На hello **учетной записи автоматизации** колонка, щелкните **конфигураций DSC**
4. На hello **конфигураций DSC** колонка, щелкните **TestConfig** (имя hello hello ранее импортированные конфигурации).
5. На hello **TestConfig конфигурации** колонке нажмите кнопку **компиляции**, а затем нажмите кнопку **Да**. Запустится задание компиляции.
   
    ![Снимок экрана: колонка конфигурации TestConfig hello, выделение кнопки компиляции](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> При компиляции конфигурации в службе автоматизации Azure автоматически разворачивает любой созданный узел toohello MOF-файлы конфигурации опрашивающего сервера.
> 
> 

## <a name="viewing-a-compilation-job"></a>Просмотр задания компиляции
После запуска компиляции, его можно просмотреть в hello **задания компиляции** плитки в hello **конфигурации** колонку. Hello **задания компиляции** плитки показывает выполняющихся, завершен, а также задания со сбоями. При открытии в колонке задания компиляции, он отображает сведения об этом задании, включая любые ошибок или предупреждений, входные параметры в конфигурации hello и компиляция журналы.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.
3. На hello **учетной записи автоматизации** колонка, щелкните **конфигураций DSC**.
4. На hello **конфигураций DSC** колонка, щелкните **TestConfig** (имя hello hello ранее импортированные конфигурации).
5. На hello **задания компиляции** плитки приветствия **TestConfig конфигурации** колонка, щелкните любой hello заданиями. Объект **задание компиляции** запуска открывается колонка, помеченные hello дату hello задание компиляции.
   
    ![Снимок экрана: колонка задание компиляции hello](./media/automation-dsc-getting-started/CompilationJob.png)
6. Щелкните одну из них hello **задание компиляции** дальнейшей toosee колонки сведений о hello задания.

## <a name="viewing-node-configurations"></a>Просмотр конфигураций узлов
При успешном выполнении задания компиляции создается одна или несколько конфигураций узлов. Конфигурация узла является MOF-документ, развернутых toohello опрашивающего сервера и готов toobe извлекать и применить один или несколько узлов. Можно просмотреть конфигурацию узла hello в вашей учетной записи автоматизации в hello **конфигурации узла DSC** колонку. Настройка узла имеет имя, состоящее из формы hello *ConfigurationName*. *NodeName*.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.
3. На hello **учетной записи автоматизации** колонка, щелкните **конфигурации узла DSC**.
   
    ![Снимок экрана: колонка hello конфигурации узла DSC](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a>Подключение виртуальной машины Azure для управления с использованием DSC службы автоматизации Azure
Можно использовать виртуальные машины Azure Automation DSC toomanage Azure (классический и диспетчера ресурсов), виртуальные машины в локальной, машины Linux, виртуальные машины AWS и локальных физических компьютеров. В этом разделе будет рассматриваться как tooonboard только виртуальные машины диспетчера ресурсов Azure. Дополнительные сведения о подключении машин других типов см. в статье [Подключение компьютеров для управления с помощью Azure Automation DSC](automation-dsc-onboarding.md).

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a>tooonboard ВМ Azure Resource Manager для управления с помощью DSC службы автоматизации Azure
1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.
3. На hello **учетной записи автоматизации** колонка, щелкните **узлы DSC**.
4. В hello **узлы DSC** колонка, щелкните **добавить виртуальную Машину Azure**.
   
    ![Снимок экрана: колонка узлы DSC hello выделение hello виртуальной Машине Azure, добавить кнопки](./media/automation-dsc-getting-started/OnboardVM.png)
5. В hello **добавить виртуальные машины Azure** колонка, щелкните **выберите виртуальные машины tooonboard**.
6. В hello **выберите виртуальные машины** колонке выберите hello ВМ tooonboard и нажмите кнопку **ОК**.
   
   > [!IMPORTANT]
   > Это должна быть виртуальная машина Azure Resource Manager под управлением Windows Server 2008 R2 или более поздней версии.
   > 
   > 
7. В hello **добавить виртуальные машины Azure** колонка, щелкните **Настройка регистрационные данные**.
8. В hello **регистрации** колонки, введите имя hello hello узла конфигурации требуется toohello tooapply ВМ в hello **имя конфигурации узла** поле. Имя конфигурации узла в учетной записи автоматизации hello hello должно совпадать. На этом этапе указывать имя необязательно. Можно изменить конфигурации узла назначен hello после адаптации hello узла.
   Установите флажок **Перезагрузить узел при необходимости** и нажмите кнопку **ОК**.
   
    ![Снимок экрана: колонка регистрации hello](./media/automation-dsc-getting-started/RegisterVM.png)
   
    Hello узел конфигурацию, заданную будет применен toohello ВМ с интервалами, указанными с hello **частота обновления режима конфигурации**, и hello виртуальной Машины будет проверять наличие обновлений конфигурации узла toohello с интервалами, указанными с hello  **Частота обновления**. Дополнительные сведения об использовании этих значений см. в разделе [hello Настройка локального диспетчера конфигураций](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).
9. В hello **добавить виртуальные машины Azure** колонка, щелкните **создать**.

Azure будет запускаться hello процесс адаптации hello виртуальной Машины. После завершения hello виртуальной Машины будут отображаться в hello **узлы DSC** колонки в hello учетной записи автоматизации.

## <a name="viewing-hello-list-of-dsc-nodes"></a>Просмотр списка hello узлы DSC
Можно просмотреть список hello всех компьютеров, которые были выставленных для управления в вашей учетной записи автоматизации в hello **узлы DSC** колонку.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.
3. На hello **учетной записи автоматизации** колонка, щелкните **узлы DSC**.

## <a name="viewing-reports-for-dsc-nodes"></a>Просмотр отчетов для узлов DSC
Каждый раз, DSC службы автоматизации Azure выполняет проверку согласованности на управляемом узле, узел hello отправляет состояние отчета задней toohello опрашивающего сервера. Эти отчеты можно просматривать в колонке hello для этого узла.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.
3. На hello **учетной записи автоматизации** колонка, щелкните **узлы DSC**.
4. На hello **отчеты** эскиза, щелкните в любом hello отчеты в списке hello.
   
    ![Снимок экрана: колонка hello отчета](./media/automation-dsc-getting-started/NodeReport.png)

В колонке hello для отдельного отчета можно увидеть следующие сведения о состоянии для соответствующего согласованности hello hello Проверьте:

* Здравствуйте, отчет о состоянии — ли узел hello hello конфигурации «Сбой», «совместимый» или узел hello» не является совместимым» (если hello узел находится в **applyandmonitor** режим и hello машина не находится в состоянии требуемого hello).
* время начала Hello hello проверку согласованности.
* Проверьте Hello общего времени выполнения для обеспечения согласованности hello.
* Проверьте тип Hello согласованности.
* Все ошибки, включая hello ошибка код и сообщение об ошибке. 
* Все ресурсы DSC, в конфигурации hello и hello состояния каждого ресурса (ли hello узел находится в состоянии hello требуемого для этого ресурса), можно щелкнуть на каждый ресурс tooget более подробные сведения для этого ресурса.
* Привет, IP-адрес и режим конфигурации узла hello.

Можно также щелкнуть **просмотра отчета** фактические данные hello toosee, который hello узел отправляет toohello сервера. Дополнительные сведения об использовании этих данных см. в статье [Использование сервера отчетов DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).

Он может занять некоторое время после узла выставленных до первого отчета hello доступен. Может потребоваться toowait копирование too30 минут для первого отчета hello окончании освоить узла.

## <a name="reassigning-a-node-tooa-different-node-configuration"></a>Переназначение другой узел tooa с узлом
Можно назначить toouse узла конфигурации другому узлу не hello, начальным значением.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.
3. На hello **учетной записи автоматизации** колонка, щелкните **узлы DSC**.
4. На hello **узлы DSC** колонке нажмите имя hello hello узла требуется tooreassign.
5. В колонке hello для этого узла, щелкните **узел назначения**.
   
    ![Снимок экрана: колонка узел hello выделение hello назначить узел кнопки](./media/automation-dsc-getting-started/AssignNode.png)
6. На hello **назначить конфигурацию узла** колонки, выберите hello узла конфигурации toowhich tooassign hello узел и нажмите кнопку **ОК**.
   
    ![Снимок экрана: колонка hello конфигурации узла назначения](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a>Отмена регистрации узла
Если вы больше не требуется toobe узла, под управлением Azure Automation DSC, можно отменить его регистрацию.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Hello концентратора меню **все ресурсы** и затем hello имя вашей учетной записи автоматизации.
3. На hello **учетной записи автоматизации** колонка, щелкните **узлы DSC**.
4. На hello **узлы DSC** колонке нажмите имя hello hello узла требуется toounregister.
5. В колонке hello для этого узла, щелкните **Unregister**.
   
    ![Снимок экрана: колонка узел hello выделение кнопки Unregister hello](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a>Связанные статьи
* [Обзор Azure Automation DSC](automation-dsc-overview.md)
* [Подключение компьютеров для управления с помощью Azure Automation DSC](automation-dsc-onboarding.md)
* [Общие сведения о платформе Desired State Configuration Windows PowerShell](https://msdn.microsoft.com/powershell/dsc/overview)
* [Командлеты Automation DSC Azure](/powershell/module/azurerm.automation/#automation)
* [Цены на Automation DSC Azure](https://azure.microsoft.com/pricing/details/automation/)

