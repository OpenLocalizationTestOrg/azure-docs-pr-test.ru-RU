---
title: "Emulator Express toorun aaaUsing и отладки Azure облачной службы на локальном компьютере | Документы Microsoft"
description: "С помощью Emulator Express toorun и отладки облачной службы на локальном компьютере"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="ddec6-103">С помощью Emulator Express toorun и отладки Azure облачной службы на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="ddec6-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="ddec6-104">Emulator Express позволяет протестировать и отладить облачную службу, не запуская Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="ddec6-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="ddec6-105">Можно задать параметры вашего проекта toouse либо Emulator Express или hello полного эмулятора в зависимости от требований hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ddec6-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="ddec6-106">Дополнительные сведения о hello полного эмулятора в разделе [запуск приложения Azure в эмуляторе вычислений hello](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="ddec6-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="ddec6-107">Использование Emulator Express в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ddec6-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="ddec6-108">При создании проекта Azure в пакете Azure SDK 2.3 или более поздней версии Emulator Express используется автоматически.</span><span class="sxs-lookup"><span data-stu-id="ddec6-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="ddec6-109">Для существующих проектов, которые были созданы в более ранней версии hello Azure SDK используйте следующие шаги tooselect Emulator Express hello:</span><span class="sxs-lookup"><span data-stu-id="ddec6-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="ddec6-110">Создайте или откройте проект облачной службы Azure в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddec6-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="ddec6-111">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и hello контекстном меню, выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="ddec6-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="ddec6-112">На страницах свойств проектов hello выберите hello **Web** вкладки.</span><span class="sxs-lookup"><span data-stu-id="ddec6-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Свойства проекта облачной службы Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="ddec6-114">В разделе **Локальный сервер Development Server** выберите **Использовать IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="ddec6-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="ddec6-115">В разделе **Эмулятор** выберите **Использовать Emulator Express**.</span><span class="sxs-lookup"><span data-stu-id="ddec6-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="ddec6-116">toolaunch hello Emulator Express, запустите следующую команду в командной строке hello:</span><span class="sxs-lookup"><span data-stu-id="ddec6-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="ddec6-117">Ограничения Emulator Express</span><span class="sxs-lookup"><span data-stu-id="ddec6-117">Emulator Express limitations</span></span>
<span data-ttu-id="ddec6-118">следующие проблемы Hello перечислены известные ограничения Emulator Express.</span><span class="sxs-lookup"><span data-stu-id="ddec6-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="ddec6-119">Emulator Express несовместим с веб-сервером IIS.</span><span class="sxs-lookup"><span data-stu-id="ddec6-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="ddec6-120">Облачная служба может содержать несколько ролей, но каждая роль является ограниченной tooone экземпляра.</span><span class="sxs-lookup"><span data-stu-id="ddec6-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="ddec6-121">Невозможен доступ к портам с номерами меньше 1000.</span><span class="sxs-lookup"><span data-stu-id="ddec6-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="ddec6-122">Если используется поставщик проверки подлинности, обычно использующий порт ниже 1000, может потребоваться toochange этот значение tooa номер порта выше 1000.</span><span class="sxs-lookup"><span data-stu-id="ddec6-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="ddec6-123">Все ограничения, которые применяются toohello эмулятор вычислений Azure также применить tooEmulator Express.</span><span class="sxs-lookup"><span data-stu-id="ddec6-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="ddec6-124">Например, число экземпляров роли в развернутой службе не может быть больше 50.</span><span class="sxs-lookup"><span data-stu-id="ddec6-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="ddec6-125">Дополнительные сведения о hello эмулятор вычислений Azure см. в разделе [запуск приложения Azure в эмуляторе вычислений hello](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="ddec6-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddec6-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ddec6-126">Next steps</span></span>
[<span data-ttu-id="ddec6-127">Отладка облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="ddec6-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
