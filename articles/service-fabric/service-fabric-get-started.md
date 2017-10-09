---
title: "aaaSet среду разработки для Azure микрослужбами | Документы Microsoft"
description: "Установка среды выполнения hello, пакета SDK и средств и создайте кластер локальной разработки. После завершения этой установки, будет готов toobuild приложений."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a>Подготовка среды разработки
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 toobuild и запустите [приложения Azure Service Fabric] [ 1] на компьютере разработки установите hello среды выполнения, пакет SDK и средства. Необходимо также tooenable выполнение сценариев Windows PowerShell hello, включенных в пакет SDK для hello.

## <a name="prerequisites"></a>Предварительные требования
### <a name="supported-operating-system-versions"></a>Поддерживаемые версии операционных систем
для разработки поддерживаются Hello следующих версий операционной системы:

* Windows 7
* Windows 8 и Windows 8.1;
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> Windows 7 по умолчанию поставляется с Windows PowerShell версии 2.0. Для выполнения командлетов PowerShell для Service Fabric требуется PowerShell начиная с версии 3.0. Вы можете [загрузить Windows PowerShell 5.0] [ powershell5-download] из центра загрузки Майкрософт hello.
> 
> 

## <a name="install-hello-sdk-and-tools"></a>Установка пакета SDK для hello и средств
### <a name="toouse-visual-studio-2017"></a>toouse Visual Studio 2017 г.
Средства Service Fabric являются частью рабочей нагрузки Azure разработки и управления hello в Visual Studio 2017 г. Эту рабочую нагрузку необходимо включить при установке Visual Studio.
Кроме того необходимо tooinstall hello Microsoft Azure Service Fabric SDK, с помощью установщика веб-платформы.

* [Установить пакет Microsoft Azure Service Fabric SDK hello][core-sdk]

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>toouse Visual Studio 2015 (требуется Visual Studio 2015 с обновлением 2 или более поздней версии)
Для Visual Studio 2015 средств Service Fabric устанавливаются вместе с hello SDK, с помощью установщика веб-платформы hello:

* [Установить пакет Microsoft Azure Service Fabric SDK hello и средства][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>Только установка пакета SDK
Если требуется только hello SDK, можно установить этот пакет:
* [Установить пакет Microsoft Azure Service Fabric SDK hello][core-sdk]

Ниже перечислены текущие версии Hello
* Пакет SDK для Service Fabric 2.7.198
* Среда выполнения Service Fabric 5.7.198
* Средства Service Fabric для Visual Studio 2015 1.7.50721
* Visual Studio 2017 с обновлением 2 включает средства Service Fabric для Visual Studio 1.6.20170504
* Visual Studio 2017 с обновлением 3 (предварительная версия 7) (15.3.0, предварительная версия 7.0) включает средства Service Fabric для Visual Studio 1.7.20170721

Список поддерживаемых версий см. в статье [Azure Service Fabric support options](service-fabric-support.md) (Варианты поддержки Azure Service Fabric).

## <a name="enable-powershell-script-execution"></a>Включение сценариев PowerShell
Для создания локального кластера разработки и развертывания приложений из Visual Studio в Service Fabric используются сценарии Windows PowerShell. По умолчанию ОС Windows блокирует выполнение этих сценариев. tooenable их, необходимо изменить политику выполнения PowerShell. Откройте PowerShell с правами администратора и введите hello следующую команду:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Дальнейшие действия
Среда разработки настроена, и вы готовы к созданию и запуску собственных приложений.

* [Создание первого приложения Service Fabric в Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
* [Узнайте, как toodeploy приложений в локальном кластере и управление ими](service-fabric-get-started-with-a-local-cluster.md)
* [Дополнительные сведения о модели программирования hello: надежные службы и службы Reliable Actor](service-fabric-choose-framework.md)
* [Извлечение hello Service Fabric примеры кода на GitHub](https://aka.ms/servicefabricsamples)
* [Визуализация кластера с помощью обозревателя Service Fabric](service-fabric-visualizing-your-cluster.md)
* [Выполните hello обучения tooget путь платформы toohello начальные сведения о Service Fabric](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* [Сведения о вариантах поддержки Service Fabric](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Страница кампании Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Ссылка на WebPI VS 2015"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Ссылка на WebPI Dev15"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Ссылка на WebPI Core SDK"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
