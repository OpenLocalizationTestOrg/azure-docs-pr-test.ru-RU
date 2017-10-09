---
title: "шаблоны aaaDeploy вместе с Visual Studio в стек Azure | Документы Microsoft"
description: "Узнайте, как шаблоны toodeploy вместе с Visual Studio в Azure стека."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: aea917b585a30ef4fbe7263db66f0659b56b21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a><span data-ttu-id="8e110-103">Развертывание шаблонов в Azure Stack с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8e110-103">Deploy templates in Azure Stack using Visual Studio</span></span>

<span data-ttu-id="8e110-104">Используйте Visual Studio toodeploy диспетчера ресурсов Azure шаблоны toohello стека Azure пакет средств разработки.</span><span class="sxs-lookup"><span data-stu-id="8e110-104">Use Visual Studio toodeploy Azure Resource Manager templates toohello Azure Stack development kit.</span></span>

1. <span data-ttu-id="8e110-105">[Установка и подключение](azure-stack-install-visual-studio.md) tooAzure стека с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e110-105">[Install and connect](azure-stack-install-visual-studio.md) tooAzure Stack with Visual Studio.</span></span>
2. <span data-ttu-id="8e110-106">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e110-106">Open Visual Studio.</span></span>
3. <span data-ttu-id="8e110-107">Нажмите кнопку **файл**, нажмите кнопку **New**и в hello **новый проект** диалоговом окне **группы ресурсов Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e110-107">Click **File**, click **New**, and in hello **New Project** dialog box click **Azure Resource Group**.</span></span>
4. <span data-ttu-id="8e110-108">Введите **имя** для hello новых проектов, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8e110-108">Enter a **Name** for hello new project, and then click **OK**.</span></span>
5. <span data-ttu-id="8e110-109">В hello **выберите шаблон Azure** диалоговое окно, изменение hello *Показать шаблоны из этого расположения* раскрывающемся слишком**краткое руководство стек Azure**</span><span class="sxs-lookup"><span data-stu-id="8e110-109">In hello **Select Azure Template** dialog box, change hello *Show templates from this location* drop-down too**Azure Stack Quickstart**</span></span>
6. <span data-ttu-id="8e110-110">Нажмите кнопку **101-создать storage-account**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8e110-110">Click **101-create-storage-account**, and then click **OK**.</span></span>  
7. <span data-ttu-id="8e110-111">В новый проект, вы увидите список доступных шаблонов hello, развернув hello **шаблоны** узел в hello **обозревателе решений** области.</span><span class="sxs-lookup"><span data-stu-id="8e110-111">In your new project, you can see a list of hello templates available by expanding hello **Templates** node in hello **Solution Explorer** pane.</span></span>
8. <span data-ttu-id="8e110-112">В hello **обозревателе решений** hello щелкните правой кнопкой мыши имя проекта, выберите пункт **развернуть**, нажмите кнопку **новое развертывание**.</span><span class="sxs-lookup"><span data-stu-id="8e110-112">In hello **Solution Explorer** pane, right-click hello name of your project, click **Deploy**, then click **New Deployment**.</span></span>
9. <span data-ttu-id="8e110-113">В hello **развернуть группу tooResource** диалогового окна hello **подписки** раскрывающийся список, выберите подписку Microsoft Azure стека.</span><span class="sxs-lookup"><span data-stu-id="8e110-113">In hello **Deploy tooResource Group** dialog box, in hello **Subscription** drop-down, select your Microsoft Azure Stack subscription.</span></span>
10. <span data-ttu-id="8e110-114">В hello **группы ресурсов** выберите существующую группу ресурсов или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="8e110-114">In hello **Resource Group** list, choose an existing resource group or create a new one.</span></span>
11. <span data-ttu-id="8e110-115">В hello **расположение группы ресурсов** список, выберите расположение и нажмите кнопку **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="8e110-115">In hello **Resource group location** list, choose a location, and then click **Deploy**.</span></span>
12. <span data-ttu-id="8e110-116">В hello **изменение параметров** диалогового окна введите значения для параметров hello (которые зависят от шаблона), а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8e110-116">In hello **Edit Parameters** dialog box, enter values for hello parameters (which vary by template), and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e110-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8e110-117">Next steps</span></span>
[<span data-ttu-id="8e110-118">Развертывание шаблонов с hello командной строки</span><span class="sxs-lookup"><span data-stu-id="8e110-118">Deploy templates with hello command line</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="8e110-119">Разработка шаблонов для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8e110-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)

