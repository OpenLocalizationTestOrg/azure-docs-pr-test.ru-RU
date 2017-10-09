---
title: "aaaDeploying крупных развертываний"
description: "Узнайте, как с помощью крупных развертываний toodeploy hello средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="2fb7b-103">Развертывание крупных систем</span><span class="sxs-lookup"><span data-stu-id="2fb7b-103">Deploying Large Deployments</span></span>
<span data-ttu-id="2fb7b-104">Если развертывание слишком большой toobe, содержащиеся в папке approot по умолчанию hello, можно использовать ресурс локального хранилища в качестве корневой папки развертывания hello для пакета JDK и сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="2fb7b-104">If your deployment is too large toobe contained in hello default approot folder, you can use a local storage resource as hello deployment root folder for your JDK and application server.</span></span>

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="2fb7b-105">toouse ресурс локального хранилища, как hello корневой папки развертывания для крупных развертываний</span><span class="sxs-lookup"><span data-stu-id="2fb7b-105">toouse a local storage resource as hello deployment root folder for large deployments</span></span>
1. <span data-ttu-id="2fb7b-106">Создайте новый локальный ресурс хранилища.</span><span class="sxs-lookup"><span data-stu-id="2fb7b-106">Create a new local storage resource.</span></span> <span data-ttu-id="2fb7b-107">Имя Hello hello ресурса не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="2fb7b-107">hello name of hello resource does not matter.</span></span> <span data-ttu-id="2fb7b-108">Ресурсы хранилища определяются на уровне роли hello.</span><span class="sxs-lookup"><span data-stu-id="2fb7b-108">Storage resources are defined at hello role level.</span></span> <span data-ttu-id="2fb7b-109">Hello быстрым способом tooaccess hello локального хранилища конфигурации диалогового окна, из которого можно создать новый ресурс локального хранилища, можно с помощью hello следующие шаги: щелкните правой кнопкой мыши роль hello в hello **обозревателя проектов** представление (разверните вашей Узел проекта Azure, если вы не видите hello роли), нажмите кнопку **Azure**, а затем нажмите кнопку **локального хранилища**.</span><span class="sxs-lookup"><span data-stu-id="2fb7b-109">hello quickest way tooaccess hello local storage configuration dialog, from which you could create a new local storage resource, is by using hello following steps: Right-click hello role in hello **Project Explorer** view (expand your Azure project node if you don't see hello role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="2fb7b-110">В рамках hello **локального хранилища** диалоговое окно, нажмите кнопку **добавить** toocreate новый ресурс локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="2fb7b-110">Within hello **Local Storage** dialog, click **Add** toocreate a new local storage resource.</span></span>

2. <span data-ttu-id="2fb7b-111">Набор hello требуемого размера tooat как минимум 2048 МБ (меньшее значение может вызвать hello же проблемы с размером файлов, которые возникли в hello approot).</span><span class="sxs-lookup"><span data-stu-id="2fb7b-111">Set hello desired size tooat least 2048 MB (anything less may cause hello same file size problems as you would encounter in hello approot).</span></span>

3. <span data-ttu-id="2fb7b-112">Убедитесь, что **очистить содержимое hello при перезапуске экземпляра роли hello** проверяется; это поможет предотвратить столкнулись конфликтует с уже существующими файлами в ресурсе hello логику запуска развертывания hello при hello роли экземпляр будет перезапущен.</span><span class="sxs-lookup"><span data-stu-id="2fb7b-112">Ensure that **Clean hello contents when hello role instance is recycled** is checked; this will help prevent hello deployment's startup logic from running into conflicts with pre-existing files in hello resource when hello role instance is recycled.</span></span>

4. <span data-ttu-id="2fb7b-113">Убедитесь, что hello **переменной хранения среды hello путь к каталогу ресурса после развертывания** toohello строка имеет значение **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="2fb7b-113">Ensure that hello **Environment variable storing hello resource's directory path after deployment** value is set toohello string **DEPLOYROOT**.</span></span> <span data-ttu-id="2fb7b-114">Ваше диалоговое окно ресурсов локального хранилища будет выглядеть аналогично toohello следующее.</span><span class="sxs-lookup"><span data-stu-id="2fb7b-114">Your local storage resource dialog will look similar toohello following.</span></span>

   ![][ic667943]

<span data-ttu-id="2fb7b-115">Кроме того Если вы используете **DEPLOYROOT** как hello *имя* локального ресурса, и вы не измените имя переменной среды, автоматически создается hello (которого будет установлено слишком **DEPLOYROOT_PATH** в этом случае), который будет работать для вашего приложения, а также.</span><span class="sxs-lookup"><span data-stu-id="2fb7b-115">Alternatively, if you use **DEPLOYROOT** as hello *name* of your local resource and you do not change hello automatically-generated environment variable name (which will be set too**DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="2fb7b-116">Дополнительные сведения о создании локального ресурса хранилища вы можете найти в статье [Свойства локального хранилища][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="2fb7b-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="2fb7b-117">См. также</span><span class="sxs-lookup"><span data-stu-id="2fb7b-117">See Also</span></span>
<span data-ttu-id="2fb7b-118">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2fb7b-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="2fb7b-119">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2fb7b-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="2fb7b-120">[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2fb7b-120">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="2fb7b-121">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="2fb7b-121">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
