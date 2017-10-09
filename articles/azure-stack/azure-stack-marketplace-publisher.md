---
title: "aaaUse hello Marketplace toolkit toocreate и публиковать элементы marketplace | Документы Microsoft"
description: "Узнайте, как создать элементы marketplace tooquickly hello публикации Toolkit"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: ByronR
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/14/2017
ms.author: helaw
ms.openlocfilehash: c1cf9ad1da44787901297eec12faf2a3dea82a6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a>Добавить элементы marketplace, с помощью средства публикации
Добавление к содержимого toohello [Azure Marketplace стека](azure-stack-marketplace.md) делает доступными tooyou вашего решения и клиенты для развертывания.  Hello Marketplace Toolkit создает файлы пакетов Azure Marketplace (.azpkg), исходя из расширения виртуальных Машин или шаблонов диспетчера ресурсов Azure IaaS.  Можно также использовать файлы .azpkg toopublish Marketplace Toolkit hello, либо созданных с помощью средства hello или с помощью [вручную](azure-stack-create-and-publish-marketplace-item.md) действия.  В этом разделе поможет загрузке программы hello, создание marketplace элемента на основе шаблона виртуальной Машины и затем публикации toohello этого элемента стек Azure Marketplace.     


## <a name="prerequisites"></a>Предварительные требования
 - Необходимо работать на узле hello Azure стека, набор средств hello или [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) подключения hello машине, где выполняется средство hello.

 - Загрузите hello [быстрый запуск Azure стека шаблоны](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) и извлечения.

 - Загрузите hello [средство упаковки коллекции Azure](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe). 

 - Публикация toohello marketplace требуется значков и эскизов файла.  Можно использовать собственные или сохранить hello [пример](azure-stack-marketplace-publisher.md#support-files) файлы локально в этом примере.

## <a name="download-hello-tool"></a>Загрузите средство hello
Hello Marketplace набор средств может быть [загрузить из репозитория hello Azure Tools стека](azure-stack-powershell-download.md).


##  <a name="create-marketplace-items"></a>Создание элементов marketplace
В этом разделе используется toocreate Marketplace Toolkit hello marketplace элементов пакета в формате .azpkg.  

### <a name="provide-marketplace-information-with-wizard"></a>Укажите сведения о marketplace с помощью мастера
1. Запустите hello Marketplace Toolkit из сеанса PowerShell:
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. Нажмите кнопку hello **решения** вкладки.  Этот экран принимает сведения об элементе marketplace. Введите сведения об элементе, как он tooappear рынке hello.  Можно также указать [файл параметров](azure-stack-marketplace-publisher.md#use-a-parameters-file) tooprepopulate hello формы.  
    
    ![Снимок экрана: первый экран Marketplace Toolkit](./media/azure-stack-marketplace-publisher/image7.png)
3. Нажмите кнопку **Обзор** и выберите файл изображения для каждого поля, значок и экрана.  Можно использовать собственные значки или hello значков образец hello [файлы поддержки](azure-stack-marketplace-publisher.md#support-files) раздела.
4. После заполнения всех полей, выберите «Предварительная версия решения» для решения hello в рамках hello Marketplace для предварительного просмотра.  Проверьте и измените текст hello, изображения и экрана перед нажатием кнопки **Далее**.  

### <a name="import-template-and-create-package"></a>Импорт шаблона и создания пакета
В этом разделе Импорт шаблона hello и работать с входными данными для вашего решения.

1.  Нажмите кнопку **Обзор** и выберите hello *azuredeploy.json* из папки 101-Simple-Windows-VM hello hello загружены шаблоны.

    ![Снимок экрана второй экран Marketplace Toolkit](./media/azure-stack-marketplace-publisher/image8.png)
2.  Hello мастер развертывания не будет заполнен *основные* шаг и входных данных элементов для каждого параметра, указанной в шаблоне hello.  Можно добавить дополнительные шаги и перемещение между шагами входных данных.  В качестве примера можно привести действия «Конфигурация интерфейсный» и «Конфигурация серверной части» для вашего решения.
3.  Укажите путь tooAzureGalleryPackager.exe hello.  
4.  Нажмите кнопку **создать** и hello Marketplace Toolkit упаковывает решение в файл .azpkg.  После завершения мастера hello отображает tooyour решения hello путь к файлу и предоставьте hello toocontinue параметр, публикацию вашего пакета tooAzure стека.


## <a name="publish-marketplace-items"></a>Публикация элементов marketplace
В этом разделе публикации tooyour элемент marketplace hello Azure Marketplace стека.

![Снимок экрана: первый экран Marketplace Toolkit](./media/azure-stack-marketplace-publisher/image9.png)

1.  Hello мастеру toopublish сведения о решении:
    
    |Поле|Описание|
    |-----|-----|
    | Имя администратора службы | Учетная запись администратора службы.  Пример:ServiceAdmin@mydomain.onmicrosoft.com |
    | Пароль | Пароль для учетной записи администратора службы. |
    | Конечная точка API | Конечная точка Azure стека диспетчера ресурсов Azure.  Пример: management.local.azurestack.external |
2.  Нажмите кнопку **публикации** и публикации журнал hello отображается.
3.  Вы — теперь может toodeploy вашей опубликованные элементы через портал Azure стека hello.


## <a name="use-a-parameters-file"></a>Использовать файл параметров
Также можно использовать параметры файла toocomplete hello marketplace сведения об элементе.  

Hello Marketplace набор средств включает *solution.parameters.ps1* toocreate можно использовать свой собственный файл параметров.


## <a name="support-files"></a>Файлы поддержки
| Описание | Образец |
| ----- | ----- |
| значок .png 40 x 40 | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| значок .png 90 x 90 | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| значок .png 115 x 115 | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| значок .png 255 x 115 | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| эскиз .png 533 х 324 | ![](./media/azure-stack-marketplace-publisher/image5.png) |


