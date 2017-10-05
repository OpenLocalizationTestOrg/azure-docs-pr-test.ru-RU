---
title: "Развертывание шаблонов в Azure Stack с помощью Visual Studio | Документация Майкрософт"
description: "Узнайте, как развертывать шаблоны в Azure Stack с помощью Visual Studio."
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
ms.openlocfilehash: e9b467f47f166198d9790f19dbdd3d1d0fd79947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a><span data-ttu-id="98ffa-103">Развертывание шаблонов в Azure Stack с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98ffa-103">Deploy templates in Azure Stack using Visual Studio</span></span>

<span data-ttu-id="98ffa-104">Visual Studio можно используйте для развертывания пакета средств разработки Azure стека шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="98ffa-104">Use Visual Studio to deploy Azure Resource Manager templates to the Azure Stack development kit.</span></span>

1. <span data-ttu-id="98ffa-105">[Выполните установку и подключение](azure-stack-install-visual-studio.md) к Azure Stack с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98ffa-105">[Install and connect](azure-stack-install-visual-studio.md) to Azure Stack with Visual Studio.</span></span>
2. <span data-ttu-id="98ffa-106">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98ffa-106">Open Visual Studio.</span></span>
3. <span data-ttu-id="98ffa-107">Щелкните **Файл**, выберите **Создать** и в диалоговом окне **Новый проект** щелкните **Группа ресурсов Azure**.</span><span class="sxs-lookup"><span data-stu-id="98ffa-107">Click **File**, click **New**, and in the **New Project** dialog box click **Azure Resource Group**.</span></span>
4. <span data-ttu-id="98ffa-108">Введите **имя** нового проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="98ffa-108">Enter a **Name** for the new project, and then click **OK**.</span></span>
5. <span data-ttu-id="98ffa-109">В диалоговом окне **Выберите шаблон Azure** измените значение раскрывающегося списка *Показывать шаблоны из этого расположения* на **Azure Stack Quickstart** (Быстрый запуск Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="98ffa-109">In the **Select Azure Template** dialog box, change the *Show templates from this location* drop-down to **Azure Stack Quickstart**</span></span>
6. <span data-ttu-id="98ffa-110">Нажмите кнопку **101-создать storage-account**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="98ffa-110">Click **101-create-storage-account**, and then click **OK**.</span></span>  
7. <span data-ttu-id="98ffa-111">Вы можете просмотреть список шаблонов, доступных в новом проекте, развернув узел **Шаблоны** в области **обозревателя решений**.</span><span class="sxs-lookup"><span data-stu-id="98ffa-111">In your new project, you can see a list of the templates available by expanding the **Templates** node in the **Solution Explorer** pane.</span></span>
8. <span data-ttu-id="98ffa-112">В области **обозревателя решений** щелкните правой кнопкой мыши имя проекта, щелкните **Развернуть**, а затем щелкните **Новое развертывание**.</span><span class="sxs-lookup"><span data-stu-id="98ffa-112">In the **Solution Explorer** pane, right-click the name of your project, click **Deploy**, then click **New Deployment**.</span></span>
9. <span data-ttu-id="98ffa-113">В диалоговом окне **Развернуть в группе ресурсов** из раскрывающегося списка **Подписки** выберите свою подписку Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="98ffa-113">In the **Deploy to Resource Group** dialog box, in the **Subscription** drop-down, select your Microsoft Azure Stack subscription.</span></span>
10. <span data-ttu-id="98ffa-114">Выберите существующую группу ресурсов из раскрывающегося списка **Группа ресурсов** или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="98ffa-114">In the **Resource Group** list, choose an existing resource group or create a new one.</span></span>
11. <span data-ttu-id="98ffa-115">Из списка **Расположение группы ресурсов** выберите расположение, затем нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="98ffa-115">In the **Resource group location** list, choose a location, and then click **Deploy**.</span></span>
12. <span data-ttu-id="98ffa-116">В диалоговом окне **Изменить параметры** введите значения параметров (которые зависят от шаблона), а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="98ffa-116">In the **Edit Parameters** dialog box, enter values for the parameters (which vary by template), and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98ffa-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98ffa-117">Next steps</span></span>
[<span data-ttu-id="98ffa-118">Развертывание шаблонов с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="98ffa-118">Deploy templates with the command line</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="98ffa-119">Разработка шаблонов для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="98ffa-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)

