---
title: "aaaManage формулы в toocreate Azure DevTest Labs виртуальные машины | Документы Microsoft"
description: "Узнайте, как tooupdate и удаление формулы Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a>Управление формулами Azure DevTest Labs

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

В этой статье показано, как toocreate формулы из базового (пользовательского образа, образа Marketplace или другие формулы) или существующей виртуальной Машины. В этой статье также объясняется, как управлять существующими формулами.

## <a name="create-a-formula"></a>Создание формулы
Любой пользователь с DevTest Labs *пользователей* разрешений является могут toocreate виртуальные машины с помощью формулы в качестве базы. Существует два способа toocreate формулы: 

* У базового - используйте toodefine все характеристики hello hello формулы.
* Из существующего лаборатории виртуальной Машины — используйте оператор toocreate формулы, основанные на параметрах hello существующей виртуальной Машины.

Дополнительные сведения о добавлении пользователей и разрешений см. в статье [Добавление владельцев и пользователей в Azure DevTest Labs](./devtest-lab-add-devtest-user.md).

### <a name="create-a-formula-from-a-base"></a>Создание формулы из базового образа
Hello следующие шаги описывают hello процесс создания формулы из образа, образа Marketplace или другие формулы.

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

2. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.

3. Выберите из списка hello лабораториям hello требуемой лаборатории.  

4. В колонке hello лаборатории выберите **формулы (многократно используемых базовых классов)**.
   
    ![Меню формулы](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. На hello **формулы** колонке выберите **+ добавить**.
   
    ![Добавление формулы](./media/devtest-lab-create-formulas/add-formula.png)

6. На hello **выберите базовый** колонке базы выберите hello (пользовательского образа, образа Marketplace или формулу) из которого нужно toocreate hello формулы.
   
    ![Список базовых образов](./media/devtest-lab-create-formulas/base-list.png)

7. На hello **создать формулу** колонке укажите hello следующие значения:
   
    * **Имя формулы** — введите имя формулы. Это значение отображается в списке hello базовые образы при создании виртуальной Машины. Имя Hello проверку введите его, и если не является допустимым, сообщение указывает hello требования к именам.
    * **Описание** — введите содержательное описание формулы. Это значение доступно из контекстного меню hello формулу, при создании виртуальной Машины.
    * **Имя пользователя** — введите имя пользователя, которому будут предоставлены права администратора.
    * **Пароль** : Введите - или выберите из раскрывающегося списка hello - значение, связанный с hello секрет (пароль), чтобы получить toouse hello указанного пользователя. Дополнительные сведения о секреты hello. в разделе [Azure DevTest Labs: личное хранилище секретный](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).
    * **Тип диска виртуальной машины** — укажите либо жесткого диска (жестком диске) или в хранилище на диске тип tooindicate SSD (твердотельного накопителя) допустим для hello виртуальных машин, подготовленных с помощью этого базового образа.
    * ** Виртуальной машины размера ** — выберите один из элементов hello предопределенные hello процессорных ядер, объем оперативной памяти и размер жесткого диска hello toocreate hello виртуальной Машины. 
    * **Артефакты** -hello выберите tooopen **добавить артефакты** колонки, выберите и настройте hello артефакты, что требуется tooadd toohello базового образа. Дополнительные сведения об артефактах см. в статье [Управление артефактами виртуальной машины в Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).
    * **Дополнительные параметры** -hello выберите tooopen **Дополнительно** колонки, в которой выполняется настройка hello следующие параметры:
        * **Виртуальная сеть** -указать hello нужно виртуальной сети.
        * **Подсети** -указать подсеть требуемого hello.    
        * **Конфигурация IP-адреса** -указать, следует hello Public, Private или общим IP-адреса. Дополнительные сведения см. в статье [Общие IP-адреса в Azure DevTest Labs](./devtest-lab-shared-ip.md).
        * **Сделать эту машину claimable** -внесения «claimable» на машине означает, что он не будет назначено владения во время создания hello. Вместо этого пользователи лаборатории будет машины hello может tootake владения («утверждения») в колонке hello лаборатории.     
    * **Изображение** -это поле отображает имя hello базового образа, выбранного на предыдущей колонке hello. 
     
       ![Создание формулы](./media/devtest-lab-create-formulas/create-formula.png)

8. Выберите **создать** toocreate hello формулы.

9. При создании формулы hello отображается в списке hello на hello **формулы** колонку.

### <a name="create-a-formula-from-a-vm"></a>Создание формулы на основе виртуальной машины
Hello следующие шаги описывают hello процесс создания формула, основанная на существующей виртуальной Машины. 

> [!NOTE]
> toocreate формулы из виртуальной Машины hello виртуальная машина должна быть создана после 30 марта 2016 г. 
> 
> 

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
3. Выберите из списка hello лабораториям hello требуемой лаборатории.  
4. В лаборатории hello **Обзор** колонке виртуальной Машины выберите hello, с которой вы будете toocreate hello формулы.
   
    ![Лабораторные виртуальные машины](./media/devtest-lab-create-formulas/my-vms.png)
5. В колонке hello виртуальной Машины выберите **Создание формулы (многократно используемых base)**.
   
    ![Создание формулы](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. На hello **создать формулу** колонке введите **имя** и **описание** для вашей новую формулу.
   
    ![Колонка "Create formula" (Создание формулы)](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. Выберите **ОК** toocreate hello формулы.

## <a name="modify-a-formula"></a>Изменение формулы
toomodify формулу, выполните следующие действия.

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
3. Выберите из списка hello лабораториям hello требуемой лаборатории.  
4. В колонке hello лаборатории выберите **формулы (многократно используемых базовых классов)**.
   
    ![Меню формулы](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. На hello **формулы лаборатории** колонку, вы хотите toomodify формулы выберите hello.
6. На hello **обновить формулу** , отредактируйте требуемого hello и, при необходимости выберите **обновление**.

## <a name="delete-a-formula"></a>Удаление формулы
toodelete формулу, выполните следующие действия.

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.
3. Выберите из списка hello лабораториям hello требуемой лаборатории.  
4. В лаборатории hello **параметры** колонке выберите **формулы**.
   
    ![Меню формулы](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. На hello **формулы лаборатории** колонки, toohello hello выберите кнопку с многоточием справа от формулы hello нужно toodelete.
   
    ![Меню формулы](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. Формула hello контекстном меню выберите **удалить**.
   
    ![Контекстное меню формулы](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. Выберите **Да** toohello диалоговое окно подтверждения удаления.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Связанные записи в блогах
* [Custom images or formulas? (Пользовательские изображения или формулы?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Дальнейшие действия
После создания формулы, используемой при создании виртуальной Машины, hello следующим шагом является слишком[добавления виртуальных Машин лаборатории tooyour](devtest-lab-add-vm-with-artifacts.md).

