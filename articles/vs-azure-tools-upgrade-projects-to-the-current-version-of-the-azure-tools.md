---
title: "Здравствуйте, aaaHow tooupgrade проекты toohello текущей версии инструментов Azure | Документы Microsoft"
description: "Узнайте, как tooupgrade Azure проекта в Visual Studio toohello hello в текущей версии инструментов Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: c89ba43af0f2fd9db46ce0c90f0da3d70dc1510b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupgrade-projects-toohello-current-version-of-hello-azure-tools-for-visual-studio"></a>Как tooupgrade проектов toohello текущей версии hello Azure Tools для Visual Studio
## <a name="overview"></a>Обзор
После установки текущего выпуска инструментов Azure hello (или предыдущего выпуска новее 1.6) hello, все проекты, созданные с помощью средств Azure, выпущенных до версии 1.6 (ноябрь 2011 г.), будут автоматически обновлены сразу же после их открытия. Если вы создали проекты с помощью Здравствуйте 1.6 (ноябрь 2011 г.) версии этих средств и при этом у вас установлен, можно открыть эти проекты в старой версии hello и впоследствии ли tooupgrade их.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>Изменение проекта при его обновлении
Если проект обновляется автоматически, или указать, что требуется tooupgrade она проекта изменению toowork с текущими версиями определенных сборок, и некоторые свойства, также изменяются, как описано в этом разделе. Если проект требует других изменений toobe совместим с более новая версия инструментов hello hello, эти изменения необходимо вносить вручную.

* Hello файл web.config для веб-ролей и рабочих ролей файл app.config hello, обновленные tooreference hello более новую версию Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll.
* сборки Microsoft.WindowsAzure.StorageClient.dll, Microsoft.WindowsAzure.Diagnostics.dll и Microsoft.WindowsAzure.ServiceRuntime.dll Hello являются обновленные toohello новых версий.
* Профили публикации, которые были сохранены в файле проекта Azure hello (.ccproj), перемещенный tooa-отдельный файл с расширением azurepubxml hello в hello **публикации** подкаталог.
* Некоторые свойства в hello профиль публикации, обновленные toosupport новых и измененных функций. Свойство **AllowUpgrade** заменяется свойством **DeploymentReplacementMethod**, так как развернутую облачную службу можно обновлять одновременно или поступательно.
* Здравствуйте, свойство **UseIISExpressByDefault** добавляется и набор toofalse таким образом, чтобы hello веб-сервер, который используется для отладки не изменялся автоматически из tooIIS Internet Information Services (IIS), экспресс-выпуск. IIS Express — hello стандартного веб-сервера для проектов, созданных с помощью более поздние выпуски средств hello hello.
* Если Azure Caching размещается в одном или нескольких ролях проекта, при обновлении проекта некоторые свойства в конфигурации службы hello (файл cscfg) и определения службы (файл csdef) изменяются. Если проект hello использует пакет NuGet для кэша Azure hello, проект hello — обновленных toohello самую последнюю версию пакета hello. Следует открыть файл web.config hello и убедитесь, что этого hello конфигурация клиента была правильно сохранена во время обновления hello. Если вы добавили hello ссылки tooAzure кэширование клиентских сборок без использования пакета NuGet hello, эти сборки не будут обновлены; необходимо вручную обновить эти ссылки на новые версии toohello.

> [!IMPORTANT]
> Для проектов F # необходимо вручную обновить ссылки на сборки tooAzure, чтобы они ссылались hello новых версий этих сборок.
> 
> 

### <a name="how-tooupgrade-an-azure-project-toohello-current-release"></a>Как tooupgrade Azure проекта toohello текущего выпуска
1. Установка hello текущего hello инструментов Azure в hello установки Visual Studio требуется toouse для hello обновить версию проекта и последовательно откройте hello проекта, которые должны tooupgrade. Если hello проект был создан с помощью инструментов Azure, выпущенных до версии 1.6 (ноябрь 2011 г.), проект hello — автоматически обновленные toohello текущей версии. Если hello проект был создан с hello выпуске, ноябрь 2011 г., по-прежнему установленной версии hello проект откроется в этом выпуске.
2. В обозревателе решений откройте hello контекстное меню для узла проекта hello, выберите **свойства**, а затем выберите hello **приложения** диалогового окна «hello», появившемся.
   
    Hello **приложения** вкладке отображается версия инструментов hello, связанной с проектом hello. В открывшемся hello текущей версии средств Azure hello проект уже был обновлен. Если установлена более новая версия средства hello, чем показано, какие вкладки hello, **обновление** появится кнопка.
3. Выберите hello **обновление** tooupgrade кнопка средств hello текущей версии toohello проекта.
4. Построение проекта hello и затем исправьте все ошибки, возникающие в результате изменения в API. Сведения о как toomodify кода для hello новой версии, в документации hello hello конкретного API.

