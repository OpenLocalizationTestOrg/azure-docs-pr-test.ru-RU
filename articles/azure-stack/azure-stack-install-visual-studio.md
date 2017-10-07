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
# <a name="install-visual-studio-and-connect-tooazure-stack"></a><span data-ttu-id="f9566-103">Установка Visual Studio и подключение tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="f9566-103">Install Visual Studio and connect tooAzure Stack</span></span>

<span data-ttu-id="f9566-104">Использование Visual Studio tooauthor и развертывания диспетчера ресурсов Azure [шаблоны](azure-stack-arm-templates.md) стека Azure.</span><span class="sxs-lookup"><span data-stu-id="f9566-104">Use Visual Studio tooauthor and deploy Azure Resource Manager [templates](azure-stack-arm-templates.md) in Azure Stack.</span></span> <span data-ttu-id="f9566-105">Можно использовать hello действия, описанные в этой статье tooinstall Visual Studio, либо из [пакет средств разработки Azure стека](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows при подключении через [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="f9566-105">You can use hello steps described in this article tooinstall Visual Studio either from [Azure Stack Development Kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are connected through [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span> <span data-ttu-id="f9566-106">Эти шаги выполнить новую установку Visual Studio 2015 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="f9566-106">These steps perform a new installation of Visual Studio 2015 Community Edition.</span></span> <span data-ttu-id="f9566-107">Дополнительные сведения о [сосуществования](https://msdn.microsoft.com/library/ms246609.aspx) других версий Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9566-107">Read more about [coexistence](https://msdn.microsoft.com/library/ms246609.aspx) between other Visual Studio versions.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="f9566-108">Установка Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f9566-108">Install Visual Studio</span></span>
1. <span data-ttu-id="f9566-109">Загрузите и запустите hello [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9566-109">Download and run hello [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>             
2. <span data-ttu-id="f9566-110">Поиск **Visual Studio Community 2015 с Microsoft Azure SDK - 2.9.6**, нажмите кнопку **добавить**, и **установить**.</span><span class="sxs-lookup"><span data-stu-id="f9566-110">Search for **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**, click **Add**, and **Install**.</span></span>

    ![Снимок экрана WebPI шаги установки](./media/azure-stack-install-visual-studio/image1.png) 

3. <span data-ttu-id="f9566-112">Удаление hello **Microsoft Azure PowerShell** , установленной в составе hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="f9566-112">Uninstall hello **Microsoft Azure PowerShell** that is installed as part of hello Azure SDK.</span></span>

    ![Снимок экрана: Добавление и удаление программ интерфейс для Azure PowerShell](./media/azure-stack-install-visual-studio/image2.png) 

4. <span data-ttu-id="f9566-114">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Установка PowerShell для Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="f9566-114">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md)</span></span>

5. <span data-ttu-id="f9566-115">После завершения установки hello, перезапустите hello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="f9566-115">Restart hello operating system after hello installation completes.</span></span>

## <a name="connect-tooazure-stack"></a><span data-ttu-id="f9566-116">Подключение tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="f9566-116">Connect tooAzure Stack</span></span>

1. <span data-ttu-id="f9566-117">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9566-117">Launch Visual Studio.</span></span>

2. <span data-ttu-id="f9566-118">Из hello **представление** последовательно выберите пункты **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f9566-118">From hello **View** menu, select **Cloud Explorer**.</span></span>

3. <span data-ttu-id="f9566-119">В новой области hello выберите **добавить учетную запись** и выполните вход с помощью учетных данных Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f9566-119">In hello new pane, select **Add Account** and sign in with your Azure Active Directory credentials.</span></span>  
    <span data-ttu-id="f9566-120">![Снимок экрана Cloud Explorer после входа в систему и подключен tooAzure стека](./media/azure-stack-install-visual-studio/image6.png)</span><span class="sxs-lookup"><span data-stu-id="f9566-120">![Screenshot of Cloud Explorer once logged in and connected tooAzure Stack](./media/azure-stack-install-visual-studio/image6.png)</span></span>

<span data-ttu-id="f9566-121">После входа вы можете [развертывания шаблонов](azure-stack-deploy-template-visual-studio.md) или обзор доступных типов ресурсов и группы ресурсов, toocreate собственных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="f9566-121">Once logged in, you can [deploy templates](azure-stack-deploy-template-visual-studio.md) or browse available resource types and resource groups toocreate your own templates.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f9566-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f9566-122">Next Steps</span></span>

 - [<span data-ttu-id="f9566-123">Разработка шаблонов для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f9566-123">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
