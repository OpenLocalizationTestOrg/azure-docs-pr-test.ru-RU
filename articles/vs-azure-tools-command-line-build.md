---
title: "построение строки aaaCommand для Azure | Документы Microsoft"
description: "Создание сборки для Azure с помощью командной строки"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a>Построение проектов Azure из командной строки hello
Hello Microsoft Build Engine (MSBuild) позволяет создавать продукты в средах лаборатории построения, где не установлена среда Visual Studio. MSBuild использует для файлов проекта расширяемый формат XML, который полностью поддерживается Майкрософт. С помощью формата файла MSBuild hello, можно описать элементы, которые должны быть построения для одного или нескольких платформ и конфигураций.

Можно также запустить MSBuild hello командной строки, и в этом разделе описывается данный подход. Задавая свойства в командной строке приветствия, можно строить конкретные конфигурации проекта. Аналогичным образом можно также определить hello целевые объекты, MSBuild строит. Дополнительные сведения о параметрах командной строки и MSBuild см. в [справочнике по командной строке MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).

## <a name="msbuild-parameters"></a>Параметры MSBuild
Hello простейший способ toocreate пакета является toorun MSBuild с hello `/t:Publish` параметр. По умолчанию эта команда создает каталог отношения toohello корневой папки для проекта hello, такие как `<ProjectDirectory>\bin\Configuration\app.publish\`. При построении проекта Azure создаются два файла: hello собственно файл пакета и сопутствующий файл конфигурации hello:

* файл пакета (`project.cspkg`);
* файл конфигурации (`ServiceConfiguration.TargetProfile.cscfg`).

По умолчанию каждый проект Azure включает в себя один файл конфигурации службы для локальных сборок (отладка) и один — для облачных (промежуточное хранение или производство). Но файлы конфигурации службы можно добавлять или удалять по необходимости. При построении пакета в среде Visual Studio будет предложено какие tooinclude файла конфигурации службы наряду с hello пакета. При построении пакета с помощью MSBuild hello локального файла конфигурации службы включается по умолчанию. файл tooinclude на другую конфигурацию служб, набор hello `TargetProfile` свойство hello команды MSBuild (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

Если требуется, чтобы toouse альтернативный каталог для hello хранящихся пакетов и файлов конфигурации, путь hello набора с помощью hello `/p:PublishDir=Directory\` параметр, включая hello конечный разделитель обратной косой черты.

## <a name="next-steps"></a>Дальнейшие действия
После построения пакета hello его можно развернуть tooAzure. Учебник, показано, как tooautomate, обработки, в разделе [непрерывная доставка для облачных служб в Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).

