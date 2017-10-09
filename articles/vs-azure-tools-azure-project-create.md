---
title: "aaaCreating проекта облачной службы Azure с помощью Visual Studio | Документы Microsoft"
description: "Узнайте, теперь toocreate проекта облачной службы Azure с помощью Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="40591-103">Создание проекта облачной службы Azure в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="40591-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="40591-104">Hello Azure Tools для Visual Studio предоставляет шаблон проекта, который позволяет создать облачную службу Azure.</span><span class="sxs-lookup"><span data-stu-id="40591-104">hello Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="40591-105">После создания проекта hello Visual Studio позволяет tooconfigure, отладки и развертывания службы tooAzure hello облака.</span><span class="sxs-lookup"><span data-stu-id="40591-105">Once hello project has been created, Visual Studio enables you tooconfigure, debug, and deploy hello cloud service tooAzure.</span></span>

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="40591-106">Действия toocreate проекта облачной службы Azure в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="40591-106">Steps toocreate an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="40591-107">В этом разделе описывается процесс создания проекта облачной службы Azure в Visual Studio с применением одной или нескольких веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="40591-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="40591-108">Запустите Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="40591-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="40591-109">Hello главного меню, выберите **файл** > **New** > **проекта**.</span><span class="sxs-lookup"><span data-stu-id="40591-109">On hello main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="40591-110">Выберите **облака** из hello Visual C# или Visual Basic узлов проектов шаблонов и выберите **облачной службы Azure** из списка шаблонов hello.</span><span class="sxs-lookup"><span data-stu-id="40591-110">Select **Cloud** from hello Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from hello list of templates.</span></span>

    ![Новая облачная служба Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="40591-112">Укажите, какую версию hello нужно toouse toodevelop проект .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="40591-112">Specify which version of hello .NET Framework you want toouse toodevelop your project.</span></span>

1. <span data-ttu-id="40591-113">Введите имя и расположение проекта и имя решения hello.</span><span class="sxs-lookup"><span data-stu-id="40591-113">Enter a name and location for your project and a name for hello solution.</span></span> 

1. <span data-ttu-id="40591-114">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="40591-114">Select **OK**.</span></span>

1. <span data-ttu-id="40591-115">В hello **новой облачной службы Microsoft Azure** диалоговое окно, выберите hello роли, что tooadd и задайте tooadd кнопку со стрелкой вправо hello их tooyour решения.</span><span class="sxs-lookup"><span data-stu-id="40591-115">In hello **New Microsoft Azure Cloud Service** dialog, select hello roles that you want tooadd, and choose hello right arrow button tooadd them tooyour solution.</span></span>

    ![Выбор ролей для новой облачной службы Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="40591-117">роли, вы добавили, при наведении указателя мыши на роль hello в hello toorename **новой облачной службы Microsoft Azure** диалоговое окно и в контекстном меню hello, выберите **Переименовать**.</span><span class="sxs-lookup"><span data-stu-id="40591-117">toorename a role that you've added, hover on hello role in hello **New Microsoft Azure Cloud Service** dialog, and, from hello context menu, select **Rename**.</span></span> <span data-ttu-id="40591-118">Можно также переименовать роль в решении (в hello **обозревателе решений**) после его добавления.</span><span class="sxs-lookup"><span data-stu-id="40591-118">You can also rename a role within your solution (in hello **Solution Explorer**) after it has been added.</span></span>

    ![Переименование роли облачной службы Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="40591-120">Hello проекта Visual Studio Azure содержит связи toohello роли проектов в решении hello.</span><span class="sxs-lookup"><span data-stu-id="40591-120">hello Visual Studio Azure project has associations toohello role projects in hello solution.</span></span> <span data-ttu-id="40591-121">Hello проект также содержит hello *файла определения службы* и *файла конфигурации службы*:</span><span class="sxs-lookup"><span data-stu-id="40591-121">hello project also includes hello *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="40591-122">**Файл определения службы** -определяет hello параметры среды выполнения для приложения, включая какие роли являются обязательными, конечные точки и размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="40591-122">**Service definition file** - Defines hello runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="40591-123">**Файл конфигурации службы** -настраивает, сколько экземпляров роли выполняются и hello значения параметров hello, определенных для роли.</span><span class="sxs-lookup"><span data-stu-id="40591-123">**Service configuration file** - Configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> 

<span data-ttu-id="40591-124">Дополнительные сведения об этих файлах см. в разделе [настроить hello роли для облачной службы Azure с помощью Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="40591-124">For more information about these files, see [Configure hello Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="40591-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40591-125">Next steps</span></span>
- [<span data-ttu-id="40591-126">Управление ролями в проектах облачных служб Azure с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="40591-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
