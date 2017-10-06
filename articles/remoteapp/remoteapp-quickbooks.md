---
title: "aaaDeploy QuickBooks в Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooshare QuickBooks с Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>Развертывание QuickBooks в Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Используйте следующие сведения tooshare QuickBooks как приложение в Azure RemoteApp hello.

Предоставить совместный доступ к QuickBooks 2015 Enterprise в Azure RemoteApp можно либо в гибридной, либо в облачной коллекции. Hello компании файл должен находиться на виртуальной Машине, на котором работает сервер базы данных QuickBooks отдельно от серверов hello Azure RemoteApp. Никогда не храните файл hello компании на образ Azure RemoteApp - потери данных происходит в том случае, если это сделать. Только QuickBooks Enterprise поддерживает размещения файла QuickBooks hello на внешнего общего ресурса с сервером базы данных QuickBooks через стандартные сети Windows.   

> [!IMPORTANT]
> Hello QuickBooks сервера базы данных, на котором размещается файл hello компании должны размещаться на отдельных виртуальных Машин в пределах hello же виртуальной сети как hello коллекции Azure RemoteApp.  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a>Действия toodeploy QuickBooks
1. Создание виртуальной Машины Azure и установите QuickBooks QuickBooks сервера базы данных и поместите файл hello компании на виртуальной Машине Azure.  Убедитесь, что tooproperly Настройка правил брандмауэра.
2. Установите на QuickBooks [пользовательского образа](remoteapp-imageoptions.md) и создать [коллекции Azure RemoteApp](remoteapp-collections.md), облачной или гибридной, в пределах hello точного одной виртуальной сети, где размещение виртуальной Машины hello hello QuickBooks сервер базы данных с находится корпоративных файлов. 
3. [Публикация](remoteapp-publish.md) toousers QuickBooks приложения
4. Запустить клиент hello QuickBooks, размещенных в Azure RemoteApp, перейдите с помощью стандартных сетевых toohello ВМ размещения hello QuickBooks сервера базы данных Windows и откройте файл компании hello. 

## <a name="documentation-references"></a>Ссылки на документацию
* [Поддерживаемые конфигурации](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* [Варианты развертывания](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

Также можно проверить презентации Ignite [основы из Microsoft Azure RemoteApp управления и администрирования](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -too1:02:45 tooget toohello QuickBooks часть Перемотка вперед.

## <a name="deployment-architecture"></a>Архитектура развертывания
![Развертывание QuickBooks + Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

