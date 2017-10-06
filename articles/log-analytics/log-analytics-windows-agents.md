---
title: "tooAzure компьютеры Windows aaaConnect анализа журналов | Документы Microsoft"
description: "В этой статье показано компьютеров Windows hello tooconnect действия hello в вашей локальной инфраструктуры toohello службы анализа журналов с помощью настроенной версии hello агента наблюдения Майкрософт (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>Подключение службы анализа журналов toohello компьютеров Windows в Azure

В этой статье представлены действия hello tooconnect Windows компьютеры в рабочих областях tooOMS локальной инфраструктуры с помощью настроенной версии hello агента наблюдения Майкрософт (MMA). Требуется tooinstall и подключения агентов для всех компьютеров hello требуется tooonboard для них службы анализа журналов toohello toosend данных и tooview и act на этих данных. Каждый агент может передавать toomultiple рабочих областей.

Установить агенты можно с помощью программы установки, командной строки или DSC (настройки требуемого состояния) в службе автоматизации Azure.  

>[!NOTE]
Для виртуальных машин, работающих в Azure, можно упростить установку с помощью hello [расширение виртуальной машины](log-analytics-azure-vm-extension.md).

На компьютерах с подключением к Интернету hello агент использует данные hello подключения toohello Internet toosend tooOMS. Для компьютеров, не подключен к Интернету, можно использовать прокси-сервер или hello [шлюза OMS](log-analytics-oms-gateway.md).

Подключение к tooOMS компьютеров Windows выполняется просто с помощью трех простых шагов:

1. Загрузка файла установки агента hello из портала OMS hello
2. Установка агента hello, с помощью выбранного метода hello
3. Настройка агента hello или добавление дополнительных рабочих областей, при необходимости

Hello следующей схеме показаны hello отношения между компьютерами Windows и OMS после установки и агенты.

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

Если политики безопасности ИТ запретить компьютеры toohello tooconnect вашей сети Интернет, можно настроить вашей toohello tooconnect компьютеров OMS шлюза. Дополнительные сведения и инструкции по tooconfigure вашей toocommunicate серверы через службу OMS toohello шлюза OMS. в статье [подключения tooOMS компьютеров с помощью шлюза OMS hello](log-analytics-oms-gateway.md).

## <a name="system-requirements-and-required-configuration"></a>Системные требования и необходимая конфигурация
Перед началом установки или развертывания агентов, просмотрите следующие сведения о tooensure требованиям hello hello.

- Hello OMS MMA можно установить только на компьютерах под управлением Windows Server 2008 (SP2), 1 или более поздней версии или Windows 7 с пакетом обновления 1 или более поздней версии.
- Вам понадобится подписка Azure.  Дополнительные сведения см. в статье [Начало работы с Log Analytics](log-analytics-get-started.md).
- Каждый компьютер Windows должен быть toohello может tooconnect Интернет с помощью протокола HTTPS или toohello OMS шлюза. Это подключение может быть прямой через прокси-сервер, или hello OMS шлюза.
- Hello OMS MMA можно установить на автономных компьютерах, серверах и виртуальных машин. Если tooOMS tooconnect виртуальных машин, размещенных в Azure, см. [tooLog виртуальных машин подключение Azure Analytics](log-analytics-azure-vm-extension.md).
- Hello агент должен toouse TCP-порт 443 для различных ресурсов.

### <a name="network"></a>Сеть

Windows агентов регистрации tooand tooconnect со службой OMS hello они должны иметь доступ к ресурсам toonetwork, включая номера портов hello и URL-адреса домена.

- Для прокси-серверов необходимо tooensure, hello нужный прокси-сервер, ресурсы настраиваются в параметрах агента.
- Брандмауэры, ограничивающие toohello доступа к Интернету вы или сетевых специалистов должны tooconfigure tooOMS доступа toopermit вашего брандмауэра. Настройка параметров агента не требуется.

Привет, в следующей таблице показаны ресурсы, необходимые для обмена данными.

>[!NOTE]
>Некоторые из hello следующие ресурсы ссылаются оперативной аналитики, который был ранее назывался анализа журналов.

| Ресурс агента | порты; | Обход проверки HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Да |
| *.oms.opinsights.azure.com | 443 | Да |
| *.blob.core.windows.net | 443 | Да |
| *.azure-automation.net | 443 | Да |



## <a name="download-hello-agent-setup-file-from-oms"></a>Загрузите файл установки hello агента с OMS
1. На портале OMS hello, hello **Обзор** щелкните hello **параметры** плитки.  Нажмите кнопку hello **подключенные источники** вкладку вверху hello.  
    ![Вкладка "Подключенные источники"](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. Нажмите кнопку **серверов Windows** и нажмите кнопку **загрузить агент Windows** применимо tooyour тип процессора компьютера toodownload файл установки hello.
3. На hello справа от **идентификатор рабочей области**нажмите значок копирования hello и вставьте идентификатор hello в Блокнот.
4. На hello справа от **первичного ключа**нажмите значок копирования hello и вставьте ключ hello в Блокнот.     

## <a name="install-hello-agent-using-setup"></a>Установка агента hello, с помощью программы установки
1. Запустите программу установки tooinstall hello на компьютере, которые должны toomanage.
2. На начальной странице приветствия нажмите кнопку **Далее**.
3. На странице приветствия условия лицензионного соглашения, прочтите hello лицензии и нажмите кнопку **принимаю**.
4. На странице приветствия конечную папку, изменить или оставьте папку установки по умолчанию hello и нажмите кнопку **Далее**.
5. На странице приветствия параметры установки агента вы можете tooconnect hello tooAzure агента анализа журналов (OMS), Operations Manager, либо hello вариантов можно оставить пустым, если требуется агент tooconfigure hello позже. Щелкните **Далее**.   
    - Если вы выбрали tooconnect tooAzure аналитика журналов (OMS), вставьте hello **идентификатор рабочей области** и **ключ рабочей области (первичный ключ)** , скопированные в Блокнот в предыдущей процедуре hello и нажмите кнопку  **Далее**.  
        ![Вставка идентификатора рабочей области и первичного ключа](./media/log-analytics-windows-agents/connect-workspace.png)
    - Если выбрана tooconnect tooOperations Manager, введите hello **имя группы управления**, **сервера управления** имя, и **порт сервера управления**и нажмите кнопку **Далее**. На странице приветствия учетная запись действия агента выберите hello локальной системной учетной записью или учетной записью локального домена и нажмите кнопку **Далее**.  
        ![конфигурация группы управления](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![учетная запись действия агента](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. На странице готовности tooInstall hello, просмотрите выбранные параметры и нажмите кнопку **установить**.
7. На hello Настройка успешно завершена и щелкните **Готово**.
8. По завершении hello **Microsoft Monitoring Agent** отображается в **панели управления**. Можно просмотреть конфигурацию существует и убедитесь, что этот агент hello подключенных tooOperational Insights (OMS). При подключенном tooOMS hello агента отображается сообщение, указывающее: **hello Microsoft Monitoring Agent успешно подключен toohello службы Microsoft Operations Management Suite.**

## <a name="configure-proxy-settings"></a>Настройка параметров прокси

Можно использовать следующие параметры прокси-сервера tooconfigure процедуры для hello Microsoft Monitoring Agent с помощью панели управления hello. Необходимо toouse эту процедуру для каждого сервера. Если у вас есть много серверов, что вам нужно tooconfigure, может оказаться проще toouse tooautomate сценария этот процесс. Если это так, см. далее процедуре hello [tooconfigure параметры прокси-сервера для Microsoft Monitoring Agent с помощью скрипта hello](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>параметры прокси-сервера tooconfigure для hello Microsoft Monitoring Agent с помощью панели управления
1. Откройте **Панель управления**.
2. Откройте **Microsoft Monitoring Agent**.
3. Нажмите кнопку hello **параметры прокси-сервера** вкладки.  
    ![вкладка параметров прокси-сервера](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. Выберите **использовать прокси-сервер** и введите hello URL-адреса и порта номер, если такой необходимости, аналогичные toohello примере показано. Если прокси-сервер требует проверки подлинности, введите hello имя пользователя и пароль tooaccess hello прокси-сервера.


### <a name="verify-agent-connectivity-toooms"></a>Проверьте подключение tooOMS агента

Можно легко проверить, является ли агенты взаимодействуют с OMS с помощью процедуры hello:

1.  На компьютере с агентом Windows hello hello откройте панель управления.
2.  Откройте "Microsoft Monitoring Agent".
3.  Перейдите на вкладку hello анализа журналов Azure (OMS).
4.  В столбце состояния hello вы увидите этот агент hello успешно подключения службы toohello Operations Management Suite.

![Агент подключен](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>параметры прокси-сервера tooconfigure для hello Microsoft Monitoring Agent с помощью скрипта
Скопируйте hello следующие образцы, обновить его, используя сведения о конкретных tooyour среды, сохраните его с расширением PS1 и запустите скрипт hello на каждом компьютере, который подключается непосредственно toohello службой OMS.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Установка агента hello, с помощью командной строки hello
- Изменения, а затем используйте следующий пример tooinstall hello агента с помощью командной строки hello hello. пример Hello выполняет полностью автоматической установки.

    >[!NOTE]
    Tooupgrade агент, вы должны toouse hello анализа журналов API сценариев. В разделе tooupgrade далее разделе hello агента.

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

Hello агент использует в качестве его самораспаковывающегося IExpress с помощью hello `/c` команды. Вы увидите hello параметры командной строки в [параметры командной строки для IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) и затем обновление hello toosuit примере вашим потребностям.

|Параметры MMA                   |Примечания         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = Настройка hello агента tooreport tooa рабочей области                |
|OPINSIGHTS_WORKSPACE_ID                | Идентификатор рабочей области (guid) для рабочей области tooadd hello                    |
|OPINSIGHTS_WORKSPACE_KEY               | Проверки подлинности рабочей области, ключей используется tooinitially с рабочей областью hello |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | Укажите hello облачной среде, где находится hello рабочей области <br> 0 — коммерческое облако Azure (по умолчанию). <br> 1 — Azure для государственных организаций. |
|OPINSIGHTS_PROXY_URL               | URI для hello toouse прокси-сервера |
|OPINSIGHTS_PROXY_USERNAME               | Имя пользователя tooaccess проверенный прокси-сервер |
|OPINSIGHTS_PROXY_PASSWORD               | Пароль tooaccess проверенный прокси-сервер |

>[!NOTE]
ограничение попадание Длина командной строки hello tooavoid IExpress, установка hello агента с настроена рабочая область, а затем используйте tooset скрипт конфигурации для рабочей области hello.

>[!NOTE]
Если вы получаете `Command line option syntax error.` при использовании hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` параметр, можно использовать следующие инструкции по решению hello:
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>Добавление рабочей области с помощью сценария
Добавление рабочей области с помощью API сценариев агента анализа журналов hello с hello в следующем примере:

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd рабочую область в Azure для правительства США, hello используйте следующий пример сценария:
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
Если использовали hello командной строки или скрипта ранее tooinstall или настройки агента hello `EnableAzureOperationalInsights` была заменена `AddCloudWorkspace`.

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>Установка агента hello, с помощью DSC службы автоматизации Azure

Можно использовать следующий скрипт tooinstall пример hello агента с помощью DSC службы автоматизации Azure hello. пример Hello устанавливает hello 64-разрядный агент, обозначенную hello `URI` значение. Также можно использовать 32-разрядная версия hello, заменив значение URI hello. Ниже приведены Hello идентификаторы URI для обеих версий.

- 64-разрядный агент Windows: https://go.microsoft.com/fwlink/?LinkId=828603
- 32-разрядный агент Windows: https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
В этом примере процедура и сценарий не выполняют обновление существующего агента.

1. Импорт xPSDesiredStateConfiguration hello DSC-модуль из [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) в службу автоматизации Azure.  
2.  Создайте в службе автоматизации Azure ресурсы-контейнеры для переменных *OPSINSIGHTS_WS_ID* и *OPSINSIGHTS_WS_KEY*. Задать *OPSINSIGHTS_WS_ID* tooyour идентификатор рабочей области аналитики журналов OMS и задайте *OPSINSIGHTS_WS_KEY* toohello первичный ключ рабочей области.
3.  Использовать hello следующий скрипт и сохраните его как MMAgent.ps1
4.  Изменения, а затем используйте следующий пример tooinstall hello агента с помощью DSC службы автоматизации Azure hello. Импорт MMAgent.ps1 автоматизации Azure с помощью интерфейса автоматизации Azure hello или командлета.
5.  Назначение toohello конфигурации узла. В течение 15 минут hello узел проверяет свою конфигурацию и hello MMA помещается toohello узла.

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>Получить последнее значение ProductId hello

Hello `ProductId value` в hello MMAgent.ps1 сценария является уникальным tooeach версия агента. При публикации обновленную версию каждого агента, изменяет значение ProductId hello. Таким образом при hello ProductId изменения в будущем hello, можно найти с помощью простого скрипта версия агента hello. После того как вы hello установлен на тестовом сервере последнюю версию агента, можно использовать следующие значения ProductId hello установлен tooget сценария hello. Используя последнее значение ProductId hello, можно обновить значение hello hello MMAgent.ps1 сценария.

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>Настройка агента вручную или добавление дополнительных рабочих областей
При установке агентов, но не настроены или если требуется, чтобы агент tooreport hello toomultiple-рабочие области, можно использовать следующие сведения tooenable агента hello или перенастроить его. После настройки hello агент будет зарегистрирован со службой агента hello и получите необходимые сведения о конфигурации и пакеты управления, содержащие сведения о решении.

1. После установки Microsoft Monitoring Agent Привет открыть **панели управления**.
2. Откройте **Microsoft Monitoring Agent** и нажмите кнопку hello **анализа журналов Azure (OMS)** вкладки.   
3. Нажмите кнопку **добавить** tooopen hello **добавьте рабочей областью аналитики журналов** поле.
4. Вставить hello **идентификатор рабочей области** и **ключ рабочей области (первичный ключ)** скопированные в Блокнот в предыдущей процедуры для hello рабочей tooadd и нажмите кнопку **ОК**.  
    ![Настройка Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)

После сбора данных с компьютеров, отслеживаемых агентом hello hello число компьютеров, которые отслеживает OMS будет отображаться на портале OMS hello hello **подключенные источники** вкладке **параметры** как  **Серверы подключены**.


## <a name="toodisable-an-agent"></a>toodisable агента
1. После установки агента hello откройте **панели управления**.
2. Откройте агент Microsoft Monitoring Agent, а затем нажмите кнопку hello **анализа журналов Azure (OMS)** вкладки.
3. Выберите рабочую область и щелкните **Удалить**. Повторите этот шаг для всех рабочих областей.


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>При необходимости настройте группы управления Operations Manager tooan tooreport агентов

При использовании Operations Manager в ИТ-инфраструктуре hello MMA агента может использоваться как агент Operations Manager.

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>tooconfigure tooreport агенты MMA tooan группы управления Operations Manager
1.  Откройте на компьютере hello, где установлен агент hello **панели управления**.  
2.  Откройте **Microsoft Monitoring Agent** и нажмите кнопку hello **Operations Manager** вкладки.  
    ![Вкладка "Operations Manager в Microsoft Monitoring Agent"](./media/log-analytics-windows-agents/om-mg01.png)
3.  Если серверы Operations Manager интегрированы с Active Directory, установите флажок **Автоматически обновлять назначения групп управления из AD DS**.
4.  Нажмите кнопку **добавить** tooopen hello **добавить группу управления** диалоговое окно.  
    ![Добавление группы управления в Microsoft Monitoring Agent](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  В **имя группы управления** введите hello имя группы управления.
6.  В hello **основного сервера управления** введите имя компьютера hello объекта hello основного сервера управления.
7.  В hello **порт сервера управления** поле номер TCP-порта типа hello.
8.  В разделе **учетная запись действия агента**, выберите hello локальной системной учетной записью или учетной записью локального домена.
9.  Нажмите кнопку **ОК** tooclose hello **добавить группу управления** диалоговое окно и нажмите кнопку **ОК** tooclose hello **свойства Microsoft Monitoring Agent**диалоговое окно.


## <a name="next-steps"></a>Дальнейшие действия

- [Добавление решений анализа журналов из коллекции решений hello](log-analytics-add-solutions.md) tooadd функциональные возможности и сбора данных.
