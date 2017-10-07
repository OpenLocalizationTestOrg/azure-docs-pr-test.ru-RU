---
title: "aaaHow toouse диагностики Azure в виртуальные машины | Документы Microsoft"
description: "С помощью диагностики Azure toogather данных из виртуальных машин Azure для отладки, измерения производительности, мониторинг, анализ трафика и многое другое."
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Включение диагностики на виртуальных машинах Azure
Основные сведения о системе диагностики Azure см. в [обзоре системы диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics.md).

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a>Как tooEnable диагностики в виртуальной машине
Этот обход через описывается tooremotely установки tooan диагностики виртуальной машины Azure с компьютера разработчика. Вы также узнаете, как приложение, которое выполняется на этой виртуальной машине Azure и передает данные телеметрии с помощью tooimplement hello .NET [класса EventSource][EventSource Class]. Диагностика Azure телеметрия используется toocollect hello и сохранить ее в учетную запись хранилища Azure.

### <a name="pre-requisites"></a>Предварительные требования
Этот проход по предполагается есть подписка Azure и с помощью Visual Studio 2017 г. с hello Azure SDK. Если нет подписки Azure, вы можете зарегистрироваться для hello [бесплатной пробной версии][Free Trial]. Убедитесь, что слишком[Установка и настройка Azure PowerShell версии 0.8.7 или более поздней версии][Install and configure Azure PowerShell version 0.8.7 or later].

### <a name="step-1-create-a-virtual-machine"></a>Шаг 1. Создание виртуальной машины
1. На компьютере разработчика запустите Visual Studio 2017.
2. В Visual Studio hello **обозревателя серверов** разверните **Azure**, щелкните правой кнопкой мыши **виртуальные машины** выберите **создания виртуальной машины**.
3. Выберите подписку Azure в hello **выберите подписку** окна и нажмите кнопку **Далее**.
4. Выберите **Windows Server 2012 R2 Datacenter июня 2017 г** в hello **выберите образ виртуальной машины** окна и нажмите кнопку **Далее**.
5. В hello **основные параметры виртуальной машины**, задайте имя виртуальной машины hello слишком «wadexample». Укажите имя пользователя и пароль администратора и щелкните **Далее**.
6. В hello **параметры облачной службы** диалоговое окно создания новой облачной службы с именем «wadexampleVM». Создайте новую учетную запись хранения с именем wadexample и нажмите кнопку **Далее**.
7. Щелкните **Создать**.

### <a name="step-2-create-your-application"></a>Шаг 2. Создание приложения
1. На компьютере разработчика запустите Visual Studio 2017.
2. Создайте новое приложение консоли Visual C#, предназначенное для платформы .NET Framework 4.5. Имя проекта hello «WadExampleVM».

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Замените содержимое Program.cs hello hello, следующий код. Здравствуйте, класс **SampleEventSourceWriter** реализует четыре методы ведения журнала: **SendEnums**, **MessageMethod**, **SetOther** и  **HighFreq**. Hello toohello первый параметр метода WriteEvent определяет идентификатор hello hello соответствующих событий. Метод Run Hello реализует бесконечный цикл, который вызывает каждую hello методы ведения журнала, реализованный в hello **SampleEventSourceWriter** класса каждые 10 секунд.

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through hello loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. Сохранить файл hello и выберите **построить решение** из hello **построения** меню toobuild кода.

### <a name="step-3-deploy-your-application"></a>Шаг 3. Развертывание приложения
1. Щелкните правой кнопкой мыши на hello **WadExampleVM** проекта в **обозревателе решений** и выберите **открыть папку в проводнике**.
2. Перейдите toohello *bin\Debug* папки и всех hello копирования файлов (WadExampleVM.*)
3. В **обозревателя серверов** щелкните правой кнопкой мыши на виртуальной машине hello и выберите **подключиться с помощью удаленного рабочего стола**.
4. После подключения toohello виртуальной Машины создайте папку с именем WadExampleVM и вставьте файлы приложения в папке hello.
5. Запуск приложения hello WadExampleVM.exe. Должно отобразиться пустое окно консоли.

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a>Шаг 4: Создайте конфигурацию диагностики и установите расширение hello
1. Загрузите открытую конфигурацию hello файла определения схемы tooyour компьютера разработчика, выполнив следующую команду PowerShell hello:

     (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
2. Откройте новый XML-файл в Visual Studio либо в уже открытом проекте, либо в экземпляре Visual Studio без открытых проектов. В Visual Studio выберите **Добавить** -> **Новый элемент...** -> **Элементы Visual C#** -> **Данные** -> **XML-файл**. Имя файла hello «WadExample.xml»
3. Hello WadConfig.xsd свяжите с файлом конфигурации hello. Убедитесь, что окно редактора WadExample.xml hello — активное окно приветствия. Нажмите клавишу **F4** tooopen hello **свойства** окна. Щелкните hello **схемы** свойство в hello **свойства** окна. Нажмите кнопку hello **...** в hello **схемы** свойство. Нажмите кнопку hello **добавить...** кнопки и перейдите toohello расположение, где был сохранен файл XSD hello и выберите hello WadConfig.xsd. Нажмите кнопку **ОК**.
4. Замените содержимое файла конфигурации WadExample.xml hello hello на hello следующий XML-код и сохраните файл hello. Этот файл конфигурации определяет несколько toocollect счетчиков производительности: для загрузки ЦП и использования памяти. Затем конфигурация hello определяет четыре события hello соответствующий toohello методы в классе SampleEventSourceWriter hello.

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a>Шаг 5. Удаленная установка системы диагностики на виртуальной машине Azure
Hello командлеты PowerShell для управления системой диагностики на виртуальной Машине являются: набор AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension и Remove AzureVMDiagnosticsExtension.

1. На компьютере разработчика откройте Azure PowerShell.
2. Выполнение установки tooremotely hello сценария диагностики на виртуальной Машине (Замените `<user>` с вашим именем пользователя каталога. Замените `<StorageAccountKey>` с hello ключ учетной записи хранения для вашей учетной записи wadexamplevm):
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a>Шаг 6. Просмотр данных телеметрии
В Visual Studio hello **обозревателя серверов** учетной записи хранилища wadexample toohello перехода. После hello ВМ работает около 5 минут вы должны увидеть hello таблицы **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** и **WADSetOtherTable**. Дважды щелкните на одном hello телеметрии hello таблиц tooview, которые были собраны.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>Схема файла конфигурации
файл конфигурации диагностики Hello определяет значения, используемые tooinitialize диагностические параметры конфигурации при запуске агента диагностики hello. В разделе hello [последняя ссылка на схему](https://msdn.microsoft.com/library/azure/mt634524.aspx) допустимые значения и примеры.

## <a name="troubleshooting"></a>Устранение неполадок
Дополнительные сведения см. в разделе [Устранение неполадок системы диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md).

## <a name="next-steps"></a>Дальнейшие действия
[См. список виртуальных машин, других связанных статьях диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello данные собираются, устранения неполадок или Дополнительные сведения о диагностике в целом.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
