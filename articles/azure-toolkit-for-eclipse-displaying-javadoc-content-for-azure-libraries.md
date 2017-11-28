---
title: "Отображение в Eclipse содержимого Javadoc для пакета библиотек Azure для Java"
description: "Узнайте, как отобразить содержимое Javadoc для библиотек Azure в Eclipse."
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
ms.openlocfilehash: b44deb773b2159cba1d5d957455409f10fc49334
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="669f1-103">Отображение в Eclipse содержимого Javadoc для пакета библиотек Azure для Java</span><span class="sxs-lookup"><span data-stu-id="669f1-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>
<span data-ttu-id="669f1-104">Содержимое Javadoc для библиотек Azure для Java можно просмотреть в среде Eclipse, сопоставив его с библиотеками Azure для Java.</span><span class="sxs-lookup"><span data-stu-id="669f1-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="669f1-105">Ниже показано, как использовать эту функциональность в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="669f1-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="669f1-106">В данной процедуре подразумевается, что вы уже добавили библиотеку Azure для Java в путь сборки.</span><span class="sxs-lookup"><span data-stu-id="669f1-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="669f1-107">Порядок отображения в Eclipse содержимого Javadoc для библиотек Azure для Java</span><span class="sxs-lookup"><span data-stu-id="669f1-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>
* <span data-ttu-id="669f1-108">В разделе проекта **Referenced Libraries** (Ссылки на библиотеки) обозревателя проектов Eclipse откройте контекстное меню для JAR-файла библиотеки Azure для Java.</span><span class="sxs-lookup"><span data-stu-id="669f1-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="669f1-109">Например, **microsoft windowsazure-api 0.1.0.jar** (номер версии может отличаться в зависимости от установленной версии).</span><span class="sxs-lookup"><span data-stu-id="669f1-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="669f1-110">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="669f1-110">Click **Properties**.</span></span>

* <span data-ttu-id="669f1-111">В левой области диалогового окна **Свойства** щелкните **Javadoc Location** (Расположение Javadoc).</span><span class="sxs-lookup"><span data-stu-id="669f1-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="669f1-112">Отображается диалоговое окно **Javadoc Location** (Расположение Javadoc).</span><span class="sxs-lookup"><span data-stu-id="669f1-112">The **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="669f1-113">Вы можете указать **Javadoc URL** (URL-адрес Javadoc) или **Javadoc in archive** (Javadoc в архиве) в соответствующих полях.</span><span class="sxs-lookup"><span data-stu-id="669f1-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="669f1-114">Если вы решите указать URL-адрес Javadoc в поле **Javadoc URL** (URL-адрес Javadoc), используйте такие URL-адреса, как **http://dl.windowsazure.com/javadoc** или **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="669f1-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="669f1-115">Если вы решите использовать **Javadoc in archive**(Javadoc в архиве), можете указать внешний файл или файл рабочей области.</span><span class="sxs-lookup"><span data-stu-id="669f1-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="669f1-116">Выберите нужный вариант и при необходимости выполните переход или проверку.</span><span class="sxs-lookup"><span data-stu-id="669f1-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="669f1-117">В следующем примере библиотеки Azure для Java сопоставляются с соответствующим JAR-файлом Javadoc, скачанным в локальную папку с именем **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="669f1-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="669f1-118">*Необязательно*: щелкните **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="669f1-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="669f1-119">При этом могут отображаться потенциальные проблемы с JAR-файлом Javadoc.</span><span class="sxs-lookup"><span data-stu-id="669f1-119">Potential issues with the Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="669f1-120">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="669f1-120">Click **OK**.</span></span>

<span data-ttu-id="669f1-121">После сопоставления с библиотекой содержимое Javadoc должно отображаться в Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="669f1-121">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="669f1-122">Например, если `blob` определен в коде с типом `CloudBlockBlob`, ниже приведен пример содержимого Javadoc, которое появляется при вводе `blob.acquireLease` в коде:</span><span class="sxs-lookup"><span data-stu-id="669f1-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="669f1-123">См. также</span><span class="sxs-lookup"><span data-stu-id="669f1-123">See Also</span></span>
<span data-ttu-id="669f1-124">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="669f1-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="669f1-125">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="669f1-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="669f1-126">[Установка набора средств Azure для Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="669f1-126">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="669f1-127">Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="669f1-127">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
