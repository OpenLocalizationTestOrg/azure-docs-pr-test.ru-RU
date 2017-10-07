---
title: "Хранилище ключей Azure, с помощью службы автоматизации Azure aaaManage | Документы Microsoft"
description: "Узнайте, как hello службы автоматизации Azure можно использовать toomanage хранилище ключей Azure."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a>Управление хранилищем ключей Azure с помощью службы автоматизации Azure
В этом руководстве приведены toohello службы автоматизации Azure и как можно использовать toosimplify управление ключи и секретные данные в хранилище ключей Azure.

## <a name="what-is-azure-automation"></a>Что такое служба автоматизации Azure
[Служба автоматизации Azure](../automation/automation-intro.md) — это служба Azure, которая упрощает управление облаком благодаря автоматизации процессов и настройке требуемого состояния. С помощью службы автоматизации Azure, вручную, повторяющиеся, длительные и ошибкам задачи могут быть автоматизированные tooincrease надежность, эффективность и toovalue времени для вашей организации.

Служба автоматизации Azure обеспечивает механизм выполнения рабочих процессов высокую степень, высокой доступности, которая масштабируется toomeet вашим потребностям. В службе автоматизации Azure процессы можно запустить вручную, в сторонних системах или по расписанию, чтобы все задачи выполнялись в нужное время.

Снизить операционные издержки и освободить ИТ и автоматический запуск DevOps toofocus сотрудников на работу, которая добавляет ценность для бизнеса, перемещая toobe задачи управления вашей облачной службой автоматизации Azure.

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>Как служба автоматизации Azure помогает управлять хранилищем ключей Azure?
Хранилище ключей можно управлять в службе автоматизации Azure с помощью hello [командлетам хранилища ключей AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) и [командлеты классический хранилище ключей Azure](https://msdn.microsoft.com/library/azure/dn868052.aspx). Здравствуйте модуль Azure для управления классический хранилище ключей доступны автоматически в службе автоматизации Azure, а также импортировать hello [модуль AzureRM KeyVault](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) в службу автоматизации Azure, что позволяет выполнять многие управления хранилищем ключей задачи в рамках службы hello. Также вы можете обеспечить эти командлеты в службе автоматизации Azure с помощью командлетов hello для других служб Azure, tooautomate сложные задачи служб Azure и систем сторонних разработчиков.

Эти задачи, среди прочего можно выполнять с hello командлетам хранилища ключей Azure: 

* создавать и настраивать хранилище ключей;
* создавать или импортировать ключи;
* создавать или обновлять секреты;
* обновлять атрибуты ключей;
* получать ключи или секреты;
* удалять ключи или секреты.

Ниже приведены несколько примеров использования PowerShell toomanage хранилища ключей.  

* [Azure Key Vault - Step by Step (Хранилище ключей Azure: шаг за шагом)](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [Setting Up and Configuring an Azure Key Vault (Установка и настройка хранилища ключей Azure)](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello автоматизации Azure и как можно использовать toomanage хранилище ключей Azure, выполните следующие дополнительные сведения об автоматизации Azure toolearn ссылки.

* Hello Azure Automation в разделе [учебник по началу работы](../automation/automation-first-runbook-graphical.md).
* В разделе hello [сценариев PowerShell хранилище ключей Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).

