---
title: "aaaTechnical предварительные условия для создания образа виртуальной машины для hello Azure Marketplace | Документы Microsoft"
description: "Сведения о требованиях hello для создания и развертывания toohello образ виртуальной машины Azure Marketplace для других toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a>Технические предварительные условия для создания образа виртуальной машины для hello Azure Marketplace
Чтение hello процесса тщательно перед началом и понять, где и почему каждого шага выполняются. Настолько, насколько возможно, вы должны подготовить сведения о компании и другие данные, загрузить необходимые средства и перед началом процесса создания предложения hello создать технические компоненты. Все эти компоненты описаны в данной статье.  

## <a name="download-needed-tools--applications"></a>Загрузка необходимых средств и приложений
Должно быть hello следующих элементов готов до начала процесса hello:

* В зависимости от операционной системы в качестве цели, установка hello [командлетов Azure PowerShell](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) или [средство командной строки Linux](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) из hello [загрузки Azure](https://azure.microsoft.com/downloads/) страница.
* установите Azure Storage Explorer из CodePlex;
* Загрузите и установите hello средство тестирования сертификации для Azure Certified.
  * [http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913). Необходимо, чтобы средство сертификации hello toorun компьютер под управлением Windows. Если нет доступных компьютере под управлением Windows, можно запустить средство hello, используя виртуальную Машину под управлением Windows в Azure.

## <a name="platforms-supported"></a>Поддерживаемые платформы
Виртуальные машины Azure можно разрабатывать на базе Windows или Linux. Некоторые элементы hello процесса, таких как создание совместимое Azure виртуального жесткого диска (VHD) — используйте различные средства и шаги в зависимости от операционной системы с помощью публикации:  

* При использовании Linux см. раздел «Создание с совместимостью Azure виртуального жесткого диска (на основе Linux)» toohello hello [руководство по публикации образ виртуальной машины](marketplace-publishing-vm-image-creation.md).
* Если вы используете Windows, см. раздел «Создание с совместимостью Azure виртуального жесткого диска (на основе Windows)» toohello hello [руководство по публикации образ виртуальной машины](marketplace-publishing-vm-image-creation.md).

> [!NOTE]
> Требуется доступ к tooa машину под управлением Windows, чтобы:
> 
> * Запустите средство проверки сертификации hello.
> * Создайте hello общего виртуального жесткого диска подписанный URL для hello сертификации отправки виртуального жесткого диска.
> 
> 

## <a name="develop-your-vhd"></a>Разработка VHD
Можно разрабатывать VHD Azure в облаке hello или в локальной среде:

* Разработка в облаке означает, что все этапы разработки выполняются удаленно на VHD, который находится в Azure.
* Для локальной разработки VHD необходимо загрузить и разработать в локальной инфраструктуре. Такой вариант возможен, но не рекомендуется. Обратите внимание, что разработка для Windows или SQL в локальной требуется вы toohave hello соответствующих локальных лицензионных ключей. Невозможно добавить или установить SQL Server после создания виртуальной машины. Ваше предложение необходимо основать на изображении утвержденных SQL из hello портал Azure. Если вы решите toodevelop в локальной среде, необходимо выполнить некоторые действия не так, как если вы разрабатывали в облаке hello. Соответствующие сведения см. в статье [Локальная разработка образа виртуальной машины для Azure Marketplace](marketplace-publishing-vm-image-creation-on-premise.md).

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
