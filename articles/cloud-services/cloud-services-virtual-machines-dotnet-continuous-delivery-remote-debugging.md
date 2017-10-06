---
title: "Удаленная отладка при помощи непрерывной поставки aaaEnable | Документы Microsoft"
description: "Узнайте, как tooenable удаленную отладку при использовании непрерывной поставки toodeploy tooAzure"
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a>Включить удаленную отладку при использовании непрерывной поставки toopublish tooAzure
Можно включить удаленную отладку в Azure, для облачных служб или виртуальных машин при использовании [непрерывной поставки](cloud-services-dotnet-continuous-delivery.md) tooAzure toopublish, выполнив следующие действия.

## <a name="enabling-remote-debugging-for-cloud-services"></a>Включение удаленной отладки для облачных служб
1. На агент сборки hello, настройте hello исходную среду для Azure, перечисленные в [построения командной строки для Azure](http://msdn.microsoft.com/library/hh535755.aspx).
2. Поскольку выполнения hello удаленной отладки (msvsmon.exe) является обязательным для hello пакета, установите hello **инструменты удаленной отладки для Visual Studio**.

    * [Инструменты удаленной отладки для Visual Studio 2017](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [Инструменты удаленной отладки для Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [Инструменты удаленной отладки для Visual Studio 2013 с обновлением 5](https://www.microsoft.com/download/details.aspx?id=48156)
    
    В качестве альтернативы можно скопировать двоичные файлы удаленной отладки hello из в системе, где установлено приложение Visual Studio.

3. Создайте сертификат, как описано в разделе [Общие сведения о сертификатах для облачных служб Azure](cloud-services-certs-create.md). Следите за hello .pfx и отпечаток сертификата протокола удаленного рабочего СТОЛА и отправка hello сертификат toohello целевой облачной службы.
4. Используйте hello, удаленных с включенной функцией отладки из следующих параметров в toobuild командной строки MSBuild hello и пакета. (Укажите фактические пути tooyour системы и файлов проекта для элементов, заключенных в угловые скобки hello).
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    `VSX64RemoteDebuggerPath`hello путь toohello папку, содержащую msvsmon.exe в hello инструменты удаленной отладки для Visual Studio.
    `RemoteDebuggerConnectorVersion`— версия пакета Azure SDK hello в облачной службе. Кроме того, он должен соответствовать версии hello вместе с Visual Studio.
5. Публикация toohello целевой облачной службы с помощью hello пакета и cscfg-файл создан в предыдущем шаге hello.
6. Импорт toohello машины hello сертификат (PFX-файл), с Visual Studio с пакетом SDK Azure для установки .NET. Убедитесь, что toohello tooimport `CurrentUser\My` хранилище сертификатов, в противном случае присоединение toohello отладчик Visual Studio не удастся.

## <a name="enabling-remote-debugging-for-virtual-machines"></a>Включение удаленной отладки для виртуальных машин
1. Создайте виртуальную машину Azure. См. статью [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) или [Создание виртуальных машин Windows и управление ими в Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
2. На hello [странице классического портала Azure](http://go.microsoft.com/fwlink/p/?LinkID=269851), просмотреть hello виртуальной машины мониторинга toosee hello виртуальной машины **ОТПЕЧАТОК сертификата RDP**. Это значение используется для hello `ServerThumbprint` значение в конфигурации расширения hello.
3. Создайте сертификат клиента, как описано в [Общие сведения о сертификатах для облачных служб Azure](cloud-services-certs-create.md) (оставьте hello .pfx и отпечаток сертификата протокола удаленного рабочего СТОЛА).
4. Установка Azure Powershell (версии 0.7.4 или более поздней версии), перечисленные в [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
5. Запустите следующий скрипт tooenable hello RemoteDebug расширения hello. Замените пути hello и личные данные собственный, такие как имя службы, имя подписки и отпечаток.
   
   > [!NOTE]
   > Этот сценарий настроен для Visual Studio 2015. Если вы используете Visual Studio 2013 или Visual Studio 2017 г., измените hello `$referenceName` и `$extensionName` следующие назначения слишком`RemoteDebugVS2013` или `RemoteDebugVS2017`.

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. Импорт hello сертификата (.pfx) toohello компьютере с Visual Studio с пакетом SDK Azure для установки .NET.

