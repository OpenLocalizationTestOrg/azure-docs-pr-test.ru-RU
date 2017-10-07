---
title: "aaaHow toouse диагностики Azure (.NET) с облачными службами | Документы Microsoft"
description: "С помощью диагностики Azure toogather данных из Azure облачных служб для отладки, измерения производительности, мониторинг, анализ трафика и многое другое."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a>Включение системы диагностики Azure в облачных службах Azure
Основные сведения о системе диагностики Azure см. в [обзоре системы диагностики Azure](../azure-diagnostics.md).

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a>Как tooEnable диагностики в рабочей роли
В этом пошаговом руководстве описывается, как tooimplement рабочей роли Azure, создающего данные телеметрии с помощью hello класс .NET EventSource. Система диагностики Azure данные телеметрии используется toocollect hello и сохранить ее в учетную запись хранилища Azure. При создании рабочей роли, Visual Studio автоматически включает 1.0 диагностики как часть решения hello в пакеты SDK Azure для .NET 2.4 и более ранних версий. Hello следующие инструкции описывают процесс hello создания hello рабочей роли, отключение 1.0 диагностики из решения hello и развертывание Diagnostics версии 1.2 или 1.3 tooyour рабочей роли.

### <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается есть подписка Azure и с помощью Visual Studio с hello Azure SDK. Если нет подписки Azure, вы можете зарегистрироваться для hello [бесплатной пробной версии][Free Trial]. Убедитесь, что слишком[Установка и настройка Azure PowerShell версии 0.8.7 или более поздней версии][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-worker-role"></a>Шаг 1. Создание рабочей роли
1. Запустите **Visual Studio**.
2. Создание **облачной службы Azure** проект из hello **облака** шаблона, ориентированном на .NET Framework 4.5.  Назовите проект hello «WadExample» и нажмите кнопку ОК.
3. Выберите **рабочую роль** и нажмите кнопку «ОК». будет создан проект Hello.
4. В **обозревателе решений**, дважды щелкните hello **WorkerRole1** файла свойств.
5. В hello **конфигурации** вкладки, отмените **включить диагностику** toodisable диагностики 1.0 (Azure SDK 2.4 и более ранних версий).
6. Построение tooverify вашего решения, у вас нет ошибок.

### <a name="step-2-instrument-your-code"></a>Шаг 2. Инструментирование кода
Замените содержимое hello WorkerRole.cs hello, следующий код. Здравствуйте, класс SampleEventSourceWriter, наследником hello [класса EventSource][EventSource Class], реализует четыре методы ведения журнала: **SendEnums**, **MessageMethod** , **SetOther** и **HighFreq**. Здравствуйте, первый параметр toohello **WriteEvent** метод определяет идентификатор hello hello соответствующих событий. Метод Run Hello реализует бесконечный цикл, который вызывает каждую hello методы ведения журнала, реализованный в hello **SampleEventSourceWriter** класса каждые 10 секунд.

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a>Шаг 3. Развертывание рабочей роли

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. Развертывание tooAzure рабочих ролей из среды Visual Studio, выбрав hello **WadExample** hello обозревателе решений выберите проект **публикации** из hello **построения** меню.
2. Выберите свою подписку.
3. В hello **параметры публикации Microsoft Azure** диалогового окна выберите **создать...** .
4. В hello **создать облачную службу и учетную запись хранения** диалоговое окно, введите **имя** (например, «WadExample») и выберите регион или территориальная группа.
5. Набор hello **среды** слишком**промежуточной**.
6. Измените любые другие **Параметры** по необходимости и щелкните **Опубликовать**.
7. После завершения развертывания, убедитесь в hello портал Azure, облачная служба **под управлением** состояния.

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a>Шаг 4: Создание файла конфигурации диагностики и Установка расширения hello
1. Загрузите определение схемы файл открытой конфигурации hello, выполнив следующую команду PowerShell hello:

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. Добавьте файл XML tooyour **WorkerRole1** проект, щелкнув hello **WorkerRole1** проект и выберите **добавить** -> **новый элемент...** -> **Элементы Visual C#** -> **Данные** -> **XML-файл**. Имя файла hello «WadExample.xml».

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. Hello WadConfig.xsd свяжите с файлом конфигурации hello. Убедитесь, что окно редактора WadExample.xml hello — активное окно приветствия. Нажмите клавишу **F4** tooopen hello **свойства** окна. Нажмите кнопку hello **схемы** свойство в hello **свойства** окна. Нажмите кнопку hello **...** в hello **схемы** свойство. Нажмите кнопку hello **добавить...** кнопки и перейдите toohello расположение, где был сохранен файл XSD hello и выберите hello WadConfig.xsd. Нажмите кнопку **ОК**.

4. Замените содержимое файла конфигурации WadExample.xml hello hello на hello следующий XML-код и сохраните файл hello. Этот файл конфигурации определяет несколько toocollect счетчиков производительности: для загрузки ЦП и использования памяти. Затем конфигурация hello определяет четыре события hello соответствующий toohello методы в классе SampleEventSourceWriter hello.

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a>Шаг 5. Установка системы диагностики в рабочей роли
Hello командлеты PowerShell для управления системой диагностики для рабочих и веб-роли являются: набор AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension и Remove AzureServiceDiagnosticsExtension.

1. Откройте Azure PowerShell.
2. Выполните сценарий hello tooinstall диагностики в рабочей роли (Замените *StorageAccountKey* с hello ключ учетной записи хранения для вашей учетной записи wadexample и *config_path* с путем hello toohello *WadExample.xml* файла):

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a>Шаг 6. Просмотр данных телеметрии
В Visual Studio hello **обозревателя серверов**, учетной записи хранилища wadexample toohello перехода. После около пяти минут выполнения hello облачной службы, вы увидите таблицы hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** и **WADSetOtherTable**. Дважды щелкните одну из hello hello таблиц tooview телеметрии, собранных.

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a>Схема файла конфигурации
файл конфигурации диагностики Hello определяет значения, используемые tooinitialize диагностические параметры конфигурации при запуске агента диагностики hello. В разделе hello [последняя ссылка на схему](https://msdn.microsoft.com/library/azure/mt634524.aspx) допустимые значения и примеры.

## <a name="troubleshooting"></a>Устранение неполадок
Если возникли проблемы, см. сведения в статье [Устранение неполадок с помощью системы диагностики Azure](../azure-diagnostics-troubleshooting.md). Это поможет вам устранить распространенные проблемы.

## <a name="next-steps"></a>Дальнейшие действия
[Просмотреть список Azure виртуальной машины диагностики статей](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello данные собираются, устранения неполадок или Дополнительные сведения о диагностике в целом.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
