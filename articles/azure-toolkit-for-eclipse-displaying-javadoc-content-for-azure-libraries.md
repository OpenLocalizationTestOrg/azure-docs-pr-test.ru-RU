---
title: "aaaDisplaying содержимого Javadoc в Eclipse для hello пакета библиотек Azure для Java"
description: "Как toodisplay hello содержимого Javadoc для библиотек Azure hello в Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a><span data-ttu-id="acb6e-103">Отображение в Eclipse содержимого Javadoc для пакета библиотек Azure для Java hello</span><span class="sxs-lookup"><span data-stu-id="acb6e-103">Displaying Javadoc Content in Eclipse for hello Azure Libraries Package for Java</span></span>
<span data-ttu-id="acb6e-104">Hello содержимого Javadoc для библиотек Azure для Java hello можно просмотреть в среде Eclipse, связав toohello содержимого Javadoc hello библиотек Azure для Java.</span><span class="sxs-lookup"><span data-stu-id="acb6e-104">hello Javadoc content for hello Azure Libraries for Java can be viewed within your Eclipse environment by associating hello Javadoc content toohello Azure Libraries for Java.</span></span> <span data-ttu-id="acb6e-105">Hello следующие шаги показывают, как toouse эту возможность в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="acb6e-105">hello following steps show you how toouse this functionality within Eclipse.</span></span>

<span data-ttu-id="acb6e-106">Подразумевается, что вы уже добавили hello библиотеки Azure для Java tooyour построения пути.</span><span class="sxs-lookup"><span data-stu-id="acb6e-106">This procedure assumes you have already added hello Azure Library for Java tooyour build path.</span></span>

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a><span data-ttu-id="acb6e-107">toodisplay содержимого Javadoc в Eclipse для hello библиотек Azure для Java</span><span class="sxs-lookup"><span data-stu-id="acb6e-107">toodisplay Javadoc content in Eclipse for hello Azure Libraries for Java</span></span>
* <span data-ttu-id="acb6e-108">В обозревателе проектов Eclipse в hello **ссылки на библиотеки** Привет открыть контекстное меню для библиотеки Azure для Java JAR hello, раздела проекта.</span><span class="sxs-lookup"><span data-stu-id="acb6e-108">Within Eclipse's Project Explorer, in hello **Referenced Libraries** section of your project, open hello context menu for hello Azure Library for Java JAR.</span></span> <span data-ttu-id="acb6e-109">Например **microsoft windowsazure-api 0.1.0.jar** (номер версии hello могут быть различия, зависящие от версии установки).</span><span class="sxs-lookup"><span data-stu-id="acb6e-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (hello version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="acb6e-110">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="acb6e-110">Click **Properties**.</span></span>

* <span data-ttu-id="acb6e-111">В рамках hello **свойства** диалоговом окне приветствия левой панели, нажмите кнопку **расположение Javadoc**.</span><span class="sxs-lookup"><span data-stu-id="acb6e-111">Within hello **Properties** dialog, in hello left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="acb6e-112">Hello **расположение Javadoc** отображается диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="acb6e-112">hello **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="acb6e-113">Вы можете указать **Javadoc URL** (URL-адрес Javadoc) или **Javadoc in archive** (Javadoc в архиве) в соответствующих полях.</span><span class="sxs-lookup"><span data-stu-id="acb6e-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="acb6e-114">При выборе toospecify **URL-адрес Javadoc**, используйте hello URL-адреса, такие как **http://dl.windowsazure.com/javadoc** или **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="acb6e-114">If you choose toospecify a **Javadoc URL**, use hello URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="acb6e-115">При выборе toouse **Javadoc в архиве**, можно указать внешний файл или файл рабочей области.</span><span class="sxs-lookup"><span data-stu-id="acb6e-115">If you choose toouse **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="acb6e-116">Выберите нужный вариант и при необходимости выполните переход или проверку.</span><span class="sxs-lookup"><span data-stu-id="acb6e-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="acb6e-117">Hello следующий пример связывает hello библиотек Azure для Java с hello, соответствующий JAR-ФАЙЛ Javadoc, был загружен локально tooa папку с именем **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="acb6e-117">hello following example associates hello Azure Libraries for Java with hello corresponding Javadoc JAR that has been downloaded locally tooa folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="acb6e-118">*Необязательно*: щелкните **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="acb6e-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="acb6e-119">Здесь могут отображаться потенциальные проблемы с JAR-ФАЙЛ Javadoc hello.</span><span class="sxs-lookup"><span data-stu-id="acb6e-119">Potential issues with hello Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="acb6e-120">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="acb6e-120">Click **OK**.</span></span>

<span data-ttu-id="acb6e-121">После связывания с библиотекой hello hello содержимое Javadoc должно отображаться в Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="acb6e-121">Once associated with hello library, hello Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="acb6e-122">Например если `blob` определяется типа `CloudBlockBlob` в вашем коде hello ниже приведен пример содержимого Javadoc, которое появляется при вводе `blob.acquireLease` в коде:</span><span class="sxs-lookup"><span data-stu-id="acb6e-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, hello following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="acb6e-123">См. также</span><span class="sxs-lookup"><span data-stu-id="acb6e-123">See Also</span></span>
<span data-ttu-id="acb6e-124">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="acb6e-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="acb6e-125">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="acb6e-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="acb6e-126">[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="acb6e-126">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="acb6e-127">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="acb6e-127">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
