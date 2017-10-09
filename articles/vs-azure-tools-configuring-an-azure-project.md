---
title: "aaaConfigure проекта облачной службы Azure с помощью Visual Studio | Документы Microsoft"
description: "Узнайте, как tooconfigure Azure облачной службы в проект в Visual Studio, в зависимости от требований для этого проекта."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="42110-103">Настройка проекта облачной службы в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="42110-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="42110-104">Проект облачной службы Azure можно настроить в соответствии с вашими требованиями к этому проекту.</span><span class="sxs-lookup"><span data-stu-id="42110-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="42110-105">Можно задать свойства проекта hello для hello, следующие категории:</span><span class="sxs-lookup"><span data-stu-id="42110-105">You can set properties for hello project for hello following categories:</span></span>

- <span data-ttu-id="42110-106">**Публикация облачной службы tooAzure** -можно задать свойство toomake, убедиться, что случайного удаления существующей службы, развернутой tooAzure облака.</span><span class="sxs-lookup"><span data-stu-id="42110-106">**Publish a cloud service tooAzure** - You can set a property toomake sure that an existing cloud service deployed tooAzure is not accidentally deleted.</span></span>
- <span data-ttu-id="42110-107">**Запуск и отладка облачной службы на локальном компьютере hello** -можно выбрать toouse конфигурации службы и укажите, хотите ли вы toostart hello эмулятор хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="42110-107">**Run or debug a cloud service on hello local computer** - You can select a service configuration toouse and indicate whether you want toostart hello Azure storage emulator.</span></span>
- <span data-ttu-id="42110-108">**Проверить пакет облачной службы при его создании** -принято tootreat все предупреждения как ошибки, чтобы убедитесь, что пакет облачной службы hello развертывает без проблем.</span><span class="sxs-lookup"><span data-stu-id="42110-108">**Validate a cloud service package when it is created** - You can decide tootreat any warnings as errors so that you can ensure that hello cloud service package deploys without any issues.</span></span> 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a><span data-ttu-id="42110-109">Действия tooconfigure проекта облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="42110-109">Steps tooconfigure an Azure cloud service project</span></span>
1. <span data-ttu-id="42110-110">Открытие или создание проекта облачной службы в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="42110-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="42110-111">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и hello контекстном меню, выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="42110-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="42110-112">На странице свойств проекта hello, выберите hello **разработки** вкладки.</span><span class="sxs-lookup"><span data-stu-id="42110-112">In hello project's properties page, select hello **Development** tab.</span></span>

    ![Меню свойств проекта](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="42110-114">Задать **выдавать запрос перед удалением существующего развертывания** слишком**True**.</span><span class="sxs-lookup"><span data-stu-id="42110-114">Set **Prompt before deleting an existing deployment** too**True**.</span></span> <span data-ttu-id="42110-115">Этот параметр помогает tooensure не случайно удалите существующее развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="42110-115">This setting helps tooensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="42110-116">Выберите hello требуемого **конфигурации службы** tooindicate, какую конфигурацию службы требуется toouse при запуске или отладке облачной службы локально.</span><span class="sxs-lookup"><span data-stu-id="42110-116">Select hello desired **Service configuration** tooindicate which service configuration you want toouse when you run or debug your cloud service locally.</span></span> <span data-ttu-id="42110-117">Дополнительные сведения о том, как. в разделе конфигурации службы для роли, toomodify [как tooconfigure hello роли для Azure облачной службы с помощью Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="42110-117">For more information on how toomodify a service configuration for a role, see [How tooconfigure hello roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="42110-118">Задать **Запуск эмулятора хранилища Azure** слишком**True** toostart hello эмулятор хранилища Azure при запуске или отладке облачной службы локально.</span><span class="sxs-lookup"><span data-stu-id="42110-118">Set **Start Azure storage emulator** too**True** toostart hello Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="42110-119">Задать **обрабатывать предупреждения как ошибки** слишком**True** toomake убедиться, что нельзя публиковать при возникновении ошибки проверки правильности пакета.</span><span class="sxs-lookup"><span data-stu-id="42110-119">Set **Treat warnings as errors** too**True** toomake sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="42110-120">Задать **использовать порты веб-проекта** слишком**True** toomake том, что веб-роль использует hello же порт каждый раз запускается локально в IIS Express.</span><span class="sxs-lookup"><span data-stu-id="42110-120">Set **Use web project ports** too**True** toomake sure that your web role uses hello same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="42110-121">Hello инструментов Visual Studio, выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="42110-121">From hello Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42110-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="42110-122">Next steps</span></span>
- [<span data-ttu-id="42110-123">Настройка проекта Azure с помощью нескольких конфигураций службы</span><span class="sxs-lookup"><span data-stu-id="42110-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

