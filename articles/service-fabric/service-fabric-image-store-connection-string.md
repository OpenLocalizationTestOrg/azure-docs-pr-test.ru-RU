---
title: "Строка соединения хранилище Service Fabric изображения aaaAzure | Документы Microsoft"
description: "Понять, строка подключения хранилища hello изображения"
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a>Понимать строка ImageStoreConnectionString приветствия

В некоторых нашей документации мы кратко упомянем без описания, оно означает существование hello параметром «Строка ImageStoreConnectionString». И после через статьи как [развертывание и удаление приложений с помощью PowerShell][10], он выглядит как все это сделать будет значение hello копирования и вставки, как в манифесте кластера hello hello целевого объекта кластер. Поэтому приветствия должен быть можно настроить на кластер, но при создании кластера с помощью hello [портал Azure][11], нет tooconfigure без параметра этот параметр и его всегда «fabric: ImageStore». Что такое назначение hello эта настройка будет?

![Манифест кластера][img_cm]

Service Fabric начал как платформу для внутреннего использования Майкрософт с несколькими различными командами, поэтому некоторые аспекты широкие возможности настройки — «Image Store» hello является один аспект. По существу hello Image Store представляет собой подключаемый репозиторий для хранения пакетов приложений. При развернутом tooa узел в кластере hello приложения этот узел загружает содержимое пакета приложения hello из hello Image Store. Hello строка ImageStoreConnectionString — это параметр, который включает все hello сведения, необходимые для клиентов и узлов toofind hello правильный хранилище образов для данного кластера.

В настоящее время существуют поставщики хранилища образов трех типов. Ниже приведены их строки подключения.

1. Служба хранилища образов: fabric:ImageStore

2. Файловая система: file:[путь_к_файловой_системе]

3. Служба хранилища Azure: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"

Тип поставщика Hello, используемый в производственной среде это hello служба хранилища образов, с отслеживанием состояния сохраненного Системная служба, можно увидеть из Service Fabric Explorer. 

![Служба хранилища образов][img_is]

Размещения hello Image Store в службе system внутри самого кластера hello устраняет внешние зависимости для репозитория пакетов hello и дает больший контроль над hello расположение хранилища. Усовершенствования вокруг hello хранилища образов, поставщик хранилища образов hello tootarget скорее всего, во-первых, в противном случае исключительно. Hello строку подключения для поставщика службы хранилища образов hello не имеет все уникальные данные, так как клиент hello уже подключенных toohello целевого кластера. Hello клиент должен только tooknow использования протоколов, предназначенных для hello системной службы.

Hello файловой системы поставщик используется вместо hello службы хранилища образов для локального кластеров одно поле во время разработки toobootstrap hello кластера немного быстрее. Разница Hello обычно мала, но это полезно оптимизации для большинство людей во время разработки. Здравствуйте, другие хранилища поставщика типов, а также его возможных toodeploy локального ящика один кластер с, но обычно нет причин toodo таким образом, так как процесс разработки и тестирования hello продолжает hello одинаково независимо от поставщика. Кроме такого использования поставщиками файловой системы и хранилища Azure hello существует только для поддержки устаревшего кода.

Поэтому хотя hello строка ImageStoreConnectionString можно настроить, обычно просто используйте параметр по умолчанию hello. При публикации tooAzure через [Visual Studio][12], параметр hello уже автоматически настроен соответствующим образом. Tooclusters программное развертывание, размещенных в Azure строка подключения hello всегда является «fabric: ImageStore». Хотя в случае сомнений, его значение всегда может быть проверено службой Получение манифеста кластера hello, [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), или [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest). Тестирование локально и рабочие кластеры всегда должен быть поставщик службы хранилища образов hello настроенных toouse также.

### <a name="next-steps"></a>Дальнейшие действия
[Развертывание и удаление приложений с помощью PowerShell][10]

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
