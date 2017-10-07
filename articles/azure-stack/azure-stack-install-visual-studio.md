---
title: "aaaInstall Visual Studio и подключитесь tooAzure стек | Документы Microsoft"
description: "Узнайте hello действия требуются tooinstall Visual Studio и подключитесь tooAzure стека"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: aa63f9eaf5cd72a0b2f31256c2df99fb41ca11fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-connect-tooazure-stack"></a>Установка Visual Studio и подключение tooAzure стека

Использование Visual Studio tooauthor и развертывания диспетчера ресурсов Azure [шаблоны](azure-stack-arm-templates.md) стека Azure. Можно использовать hello действия, описанные в этой статье tooinstall Visual Studio, либо из [пакет средств разработки Azure стека](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows при подключении через [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn). Эти шаги выполнить новую установку Visual Studio 2015 Community Edition. Дополнительные сведения о [сосуществования](https://msdn.microsoft.com/library/ms246609.aspx) других версий Visual Studio.

## <a name="install-visual-studio"></a>Установка Visual Studio
1. Загрузите и запустите hello [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).             
2. Поиск **Visual Studio Community 2015 с Microsoft Azure SDK - 2.9.6**, нажмите кнопку **добавить**, и **установить**.

    ![Снимок экрана WebPI шаги установки](./media/azure-stack-install-visual-studio/image1.png) 

3. Удаление hello **Microsoft Azure PowerShell** , установленной в составе hello Azure SDK.

    ![Снимок экрана: Добавление и удаление программ интерфейс для Azure PowerShell](./media/azure-stack-install-visual-studio/image2.png) 

4. [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Установка PowerShell для Azure Stack)

5. После завершения установки hello, перезапустите hello операционной системы.

## <a name="connect-tooazure-stack"></a>Подключение tooAzure стека

1. Запустите Visual Studio.

2. Из hello **представление** последовательно выберите пункты **Cloud Explorer**.

3. В новой области hello выберите **добавить учетную запись** и выполните вход с помощью учетных данных Azure Active Directory.  
    ![Снимок экрана Cloud Explorer после входа в систему и подключен tooAzure стека](./media/azure-stack-install-visual-studio/image6.png)

После входа вы можете [развертывания шаблонов](azure-stack-deploy-template-visual-studio.md) или обзор доступных типов ресурсов и группы ресурсов, toocreate собственных шаблонов.  

## <a name="next-steps"></a>Дальнейшие действия

 - [Разработка шаблонов для Azure Stack](azure-stack-develop-templates.md)
