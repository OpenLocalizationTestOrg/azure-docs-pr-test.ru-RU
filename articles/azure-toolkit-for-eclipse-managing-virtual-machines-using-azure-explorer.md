---
title: "Здравствуйте, aaaManage виртуальных машин с помощью обозревателя Azure для Eclipse | Документы Microsoft"
description: "Узнайте, как toomanage виртуальных машин Azure с помощью hello обозреватель Azure для Eclipse."
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
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a>Управление виртуальными машинами с помощью hello обозреватель Azure для Eclipse

Hello Explorer Azure, который является частью hello средств Azure для Eclipse, предоставляет разработчикам Java с помощью решения для использования в управлении виртуальными машинами свою учетную запись в Azure из внутри hello Eclipse интегрированной среды разработки (IDE).

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Создание виртуальной машины в Eclipse

toocreate виртуальной машины с помощью обозревателя Azure hello hello следующие:

1. Войдите в tooyour учетная запись Azure с использованием hello [входа в инструкции для средств Azure для Eclipse hello].

2. В hello **обозреватель Azure** , разверните узел hello **Azure** узел, щелкните правой кнопкой мыши **виртуальные машины**и нажмите кнопку **создания виртуальной Машины**.

   ![Hello команда создания виртуальной Машины][CR01]  
   Hello **Создание новой виртуальной машины** откроется мастер.

3. В hello **выберите подписку** окно, выберите подписку и нажмите кнопку **Далее**.

   ![Выберите окно подписки Hello][CR02]

4. В hello **выберите образ виртуальной машины** окно, введите hello следующую информацию:

   * **Расположение**: указывает расположение для создания виртуальной машины (например, *Западная часть США*).

   * **Издатель**: указывает hello издателя, создавшего образ hello, используемой toocreate вашей виртуальной машины (например, *Microsoft*).

   * **Предложить**: указывает hello виртуальной машины предложения toouse hello выбранного издателя (например, *JDK*).

   * **SKU**: указывает toouse единица складского учета hello из выбранного предложения hello (например, *JDK_8*).

   * **Версия #**: Указывает, какую версию выбранного hello SKU toouse.

    ![Hello выбора образа виртуальной машины окна][CR03]

5. Щелкните **Далее**.

6. В hello **основные параметры виртуальной машины** окно, введите hello следующую информацию:

   * **Имя виртуальной машины**: Указывает имя hello для новой виртуальной машины, которой должно начинаться с буквы и содержать только буквы, цифры и дефисы.

   * **Размер**: указывает hello количество ядер и памяти tooallocate для виртуальной машины.

   * **Имя пользователя**: указывает hello toocreate учетной записи администратора для управления виртуальной машины.

   * **Пароль** и **Подтверждение**: указывает hello пароль для учетной записи администратора.

    ![окно Hello основные параметры виртуальной машины][CR04]

7. Щелкните **Далее**.

8. В hello **создать новую учетную запись хранения** окно, введите hello следующую информацию:

   * **Группа ресурсов**: указывает hello группу ресурсов для виртуальной машины. Выберите один из следующих вариантов hello.
      * **Создать новый**: Указывает, что toocreate новую группу ресурсов.
      * **Использовать существующие**: Указывает, что tooselect группы ресурсов, который должен быть связан с учетной записью Azure.

      ![диалоговое окно «Создание новой учетной записи хранилища Hello»][CR05]

   * **Учетная запись хранения**: указывает hello toouse учетной записи хранилища для хранения виртуальной машины. Можно использовать существующую учетную запись хранения или создать новую.

   * **Виртуальная сеть** и **подсети**: задает hello виртуальной сети и подсети, в которой будут подключаться к виртуальной машине. Вы можете выбрать имеющуюся сеть и подсеть или создать их. При выборе **создать новый**, отображается следующая диалоговое окно приветствия:

      ![диалоговое окно создания новой виртуальной сети Hello][CR06]

9. В hello **связанные ресурсы** окно, введите hello следующую информацию:

   * **Общедоступный IP-адрес**: указывает внешний IP-адрес для виртуальной машины. Вы можете toocreate новый IP-адрес или, если виртуальная машина не будет иметь общедоступный IP-адрес, можно выбрать **(нет)**.

   * **Группа безопасности сети**: определяет необязательный брандмауэр для виртуальной машины. Вы можете выбрать имеющийся брандмауэр или задать значение **(Нет)**, чтобы не использовать брандмауэр.

   * **Группа доступности**: определяет необязательную группу доступности, в которую может входить виртуальная машина. Можно выбрать существующий набор доступности или создать новую группу доступности или, если виртуальная машина не будет принадлежать tooan набор доступности, можно выбрать **(нет)**.

   ![окно Hello связанные ресурсы][CR07]

9. Нажмите кнопку **Готово**  
  В окне инструментов обозревателя Azure hello отображается на новую виртуальную машину.

   ![Новая виртуальная машина][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a>Перезапуск виртуальной машины в Eclipse

toorestart виртуальной машины с помощью hello обозреватель Azure в Eclipse, hello следующие:

1. В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **перезапустите**.

   ![команды перезапуска виртуальной машины Hello][RE01]

2. В окне подтверждения hello, щелкните **Да**.

   ![окно подтверждения перезапуска Hello][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a>Завершение работы виртуальной машины в Eclipse

tooshut вниз работающей виртуальной машины с помощью hello обозреватель Azure в Eclipse, hello следующие:

1. В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **завершение работы**.

   ![Здравствуйте, команда завершения работы виртуальной машины][SH01]

2. В окне подтверждения hello, щелкните **Да**.

   ![окно подтверждения Hello завершение работы виртуальной машины][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a>Удаление виртуальной машины в Eclipse

toodelete виртуальной машины с помощью hello обозреватель Azure в Eclipse, hello следующие:

1. В hello **обозреватель Azure** просмотра, щелкните правой кнопкой мыши hello виртуальной машины и выберите **удалить**.

   ![команда удаления виртуальной машины Hello][DE01]

2. В окне подтверждения hello, щелкните **Да**.

   ![окно подтверждения удаления виртуальной машины Hello][DE02]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об Azure размеры виртуальных машин и ценах см. в разделе hello следующие ресурсы:

* Размеры виртуальных машин Azure
  * [Размеры виртуальных машин Windows в Azure]
  * [Размеры виртуальных машин Linux в Azure]
* Цены на виртуальные машины Azure
  * [Цены на виртуальные машины Windows]
  * [Цены на виртуальные машины Linux]

Дополнительные сведения о hello наборы инструментов Azure для Java интегрированные среды разработки см. следующие ресурсы hello:

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

[Размеры виртуальных машин Windows в Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Размеры виртуальных машин Linux в Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Цены на виртуальные машины Windows]: /pricing/details/virtual-machines/windows/
[Цены на виртуальные машины Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
