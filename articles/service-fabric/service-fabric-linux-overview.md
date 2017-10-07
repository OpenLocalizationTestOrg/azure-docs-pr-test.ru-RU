---
title: "aaaAzure Service Fabric для Linux | Документы Microsoft"
description: "Кластеров Service Fabric поддерживает Linux и Java, это означает, что вы сможете может toodeploy и ведущие приложения Service Fabric на языке Java и C# в Linux."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a>Service Fabric в Azure
Предварительный просмотр Hello Service Fabric в Linux включает toobuild, развертывания и управления высокой надежности, высокомасштабируемых приложений на платформе Linux так же, как и в Windows. платформы Service Fabric Hello (надежные службы и службы Reliable Actor) доступны на языке Java в Linux в дополнение tooC # (.NET Core).  Также можно создавать [гостевые исполняемые службы](service-fabric-deploy-existing-app.md) , используя любой язык или платформу. Кроме того Предварительная версия hello также поддерживает оркестрация контейнеры Docker. Контейнеры docker можно запускать исполняемые файлы гостевого или собственного Service Fabric служб, которые используют платформы Service Fabric hello.

Service Fabric в Linux — по существу эквивалентные tooService структуры в Windows (за исключением особенностей операционной системы и поддержку языка программирования). Таким образом, большая часть наших [существующей документации](http://aka.ms/servicefabricdocs) применяется в помочь ознакомиться с технологией hello.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>Поддерживаемые операционные системы и языки программирования
Предварительный просмотр Hello ограниченный поддерживает создание hello разработки одно поле кластеры Кроме toomulti машины в Azure под управлением Ubuntu Server 16.04. поддерживает просмотр Hello hello службы Reliable actor и hello платформы надежной службы без сохранения состояния в Java и C# в исполняемых файлах tooguest сложения и управляя операциями контейнеры Docker.  

> [!NOTE]
> Платформа Reliable Collections пока не поддерживается в Linux. Не поддерживаются только кластеры автономном либо - только одно поле, так и кластеры несколькими компьютерами Azure Linux поддерживаются в режиме предварительного просмотра hello.
>
>


## <a name="supported-tooling"></a>Поддерживаемые средства
Предварительный просмотр Hello поддерживает взаимодействие с hello кластера с помощью службы структуры CLI. Для разработчиков Java интеграция с Eclipse и Yeoman доступна при помощи среды Eclipse, поддерживаемой в Linux и OS X. Hello OSX интеграции использует кулисами hello через vagrant виртуальной Машины Linux. Для разработчиков C# интеграция с Yeoman предоставляется toogenerate шаблоны приложений.

## <a name="next-steps"></a>Дальнейшие действия

* Познакомьтесь с hello [службы Reliable Actor](service-fabric-reliable-actors-introduction.md) и [надежного обмена](service-fabric-reliable-services-introduction.md) платформами программирования
* [Подготовка среды разработки в Linux](service-fabric-get-started-linux.md)
* [Настройка среды разработки для Mac OS X](service-fabric-get-started-mac.md)
* [Создание первого приложения Azure Service Fabric](service-fabric-create-your-first-linux-application-with-java.md)
* [Настройка непрерывных интеграции и развертывания с помощью Jenkins и GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [Различия между Service Fabric для Linux (предварительная версия) и Windows (общедоступная версия)](service-fabric-linux-windows-differences.md)
