---
title: "Здравствуйте, aaaManage учетные записи хранения с помощью обозревателя Azure для Eclipse | Документы Microsoft"
description: "Узнайте, как toomanage службе хранилища Azure учетных записей с помощью hello обозреватель Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: b7ec53e77e3c96d87754b9a658d31e6182121b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-eclipse"></a>Управление учетными записями хранилища с помощью hello обозреватель Azure для Eclipse

Hello Explorer Azure, который является частью hello средств Azure для Eclipse, предоставляет разработчикам решения для использования в Java для управления учетными записями хранения в учетную запись Azure с внутри hello Eclipse интегрированной среды разработки (IDE).

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a>Создание учетной записи хранения в Eclipse

toocreate учетной записи хранилища с помощью обозревателя Azure hello hello следующие:

1. Войдите в tooyour учетная запись Azure с использованием hello [входа в инструкции для средств Azure для Eclipse hello].

2. В hello **обозреватель Azure** , разверните узел hello **Azure** узел, щелкните правой кнопкой мыши **учетные записи хранения**и нажмите кнопку **создать учетную запись хранилища**.

   ![Команда "Создать учетную запись хранения"][CS01]

3. В hello **создать учетную запись хранилища** диалоговом окне укажите hello следующие параметры:

   ![Диалоговое окно "Создание учетной записи хранения"][CS02]

   * **Имя**: Указывает имя новой учетной записи хранения hello hello.

   * **Подписки**: указывает hello подписки Azure, чтобы получить toouse hello новой учетной записи хранения.

   * **Группа ресурсов**: указывает hello группу ресурсов для виртуальной машины. Выберите один из следующих вариантов hello.
      * **Создать новое**: Указывает, что toocreate новую группу ресурсов.
      * **Использовать существующий**: указывает, что вы выберете группу ресурсов, связанную с учетной записью Azure.

   * **Область**: указывает hello место для создания учетной записи хранения (например, «West US»).

   * **Учетная запись kind**: Определяет тип hello toocreate учетной записи хранилища (например, «больших двоичных объектов хранилища»). Дополнительные сведения см. в статье [Об учетных записях хранения Azure].

   * **Производительность**: Указывает, какую учетную запись хранения, предложения toouse hello выбранного издателя (например, «Premium»). Дополнительные сведения см. в статье [Целевые показатели масштабируемости и производительности службы хранилища Azure].

   * **Репликация**: указывает hello репликации для учетной записи хранения hello (например, «избыточное в пределах зоны»). Дополнительные сведения см. в статье [Репликация службы хранилища Azure].

4. При указании hello предыдущих параметров щелкните **создать**.

## <a name="create-a-storage-container-in-eclipse"></a>Создание контейнера хранилища в Eclipse

Контейнер хранилища с помощью обозревателя Azure hello toocreate hello следующие:

1. В hello **обозреватель Azure** просмотра щелкните правой кнопкой мыши учетную запись хранения hello где вы toocreate контейнера и нажмите кнопку **создать контейнер больших двоичных объектов**.

   ![Команда "Создать контейнер BLOB-объектов"][CC01]

2. В hello **создать контейнер больших двоичных объектов** диалоговое окно, укажите имя hello для контейнера и нажмите кнопку **ОК**. Дополнительные сведения об именовании контейнеров хранилища см. в статье [Naming and Referencing Containers, Blobs, and Metadata] (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них).

   ![Диалоговое окно "Создание контейнера BLOB-объектов"][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a>Удаление контейнера хранилища в Eclipse

Контейнер хранилища с помощью обозревателя Azure hello toodelete hello следующие:

1. В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши контейнер хранилища hello и нажмите кнопку **удалить**.

   ![Команда "Удалить контейнер хранилища"][DC01]

2. В окне подтверждения hello, щелкните **ОК**.

   ![Окно подтверждения удаления контейнера хранилища][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a>Удаление учетной записи хранения в Eclipse

toodelete учетной записи хранилища с помощью обозревателя Azure hello hello следующие:

1. В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши учетную запись хранения hello и нажмите кнопку **удалить**.

   ![Команда "Удалить учетную запись хранения"][DS01]

2. В окне подтверждения hello, щелкните **ОК**.

   ![Окно подтверждения удаления учетной записи хранения][DS02]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об учетных записях хранения Azure размеров и цен, см. следующие ресурсы hello:

* [Введение tooMicrosoft хранилища Azure]
* [Об учетных записях хранения Azure]
* Размеры учетных записей хранения Azure
  * [Размеры учетных записей хранения Windows в Azure]
  * [Размеры учетных записей хранения Linux в Azure]
* Цены на учетные записи хранения Azure
  * [Windows storage-account pricing] (Цены на учетные записи хранения Windows)
  * [Linux storage-account pricing] (Цены на учетные записи хранения Linux)

Дополнительные сведения о наборы инструментов Azure для Java интегрированные среды разработки см. следующие ресурсы hello:

* [Набор средств Azure для Eclipse]
  * [Новые возможности средств Azure для Eclipse hello]
  * [Установка средств Azure для Eclipse hello]
  * [входа в инструкции для средств Azure для Eclipse hello]
  * [Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]
* [Набор средств Azure для IntelliJ]
  * [Новые возможности средств Azure для IntelliJ hello]
  * [Установка hello Azure Toolkit для IntelliJ]
  * [Вход инструкции для hello Azure Toolkit для IntelliJ]
  * [Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]

Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [средств Java для Visual Studio Team Services].

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[входа в инструкции для средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Вход инструкции для hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[средств Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

[Введение tooMicrosoft хранилища Azure]: /azure/storage/storage-introduction
[Об учетных записях хранения Azure]: /azure/storage/storage-create-storage-account
[Репликация службы хранилища Azure]: /azure/storage/storage-redundancy
[Целевые показатели масштабируемости и производительности службы хранилища Azure]: /azure/storage/storage-scalability-targets
[Naming and Referencing Containers, Blobs, and Metadata]: http://go.microsoft.com/fwlink/?LinkId=255555 (Именование контейнеров, больших двоичных объектов и метаданных и ссылка на них)

[Размеры учетных записей хранения Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры учетных записей хранения Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/ (Цены на учетные записи хранения Windows)
[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/ (Цены на учетные записи хранения Linux)

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
