---
title: "Диагностика aaaBoot для виртуальных машин Linux в Azure | Документ Microsoft"
description: "Обзор возможностей отладки два hello для виртуальных машин Linux в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a>Как toouse загрузки виртуальных машин Linux tootroubleshoot диагностики в Azure

Теперь Azure поддерживает две функции отладки. Виртуальные машины Azure, созданные на основе модели развертывания с помощью Resource Manager, поддерживают выходные данные и снимки экрана консоли. 

При повторном подключении tooAzure собственного образа или даже загрузки одного из образов платформы hello, может быть несколько причин, почему Возвращает виртуальную машину в состояние не является загрузочным. Эти функции позволяют вам tooeasily Диагностика и восстановление сбоев загрузки виртуальных машин.

Для виртуальных машин Linux можно легко просмотреть hello выходные данные журналов консоли из hello портала:

![Портал Azure](./media/boot-diagnostics/screenshot1.png)
 
Тем не менее для Windows и Linux виртуальных машин Azure также позволяет toosee снимок экрана приветствия виртуальных Машин из низкоуровневой оболочки hello:

![Ошибка](./media/boot-diagnostics/screenshot2.png)

Обе эти функции доступны на виртуальных машинах Azure во всех регионах. Обратите внимание, снимки экрана и выходных данных может занять tooappear минут too10 вашей учетной записи хранилища.

## <a name="common-boot-errors"></a>Распространенные ошибки загрузки

- [Проблемы с файловой системой](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [Проблемы с ядром](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [Ошибки FSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Включение диагностики на новой виртуальной машине
1. При создании новой виртуальной машины из hello предварительной версии портала выберите hello **диспетчера ресурсов Azure** из раскрывающегося списка модели развертывания hello:
 
    ![Диспетчер ресурсов](./media/boot-diagnostics/screenshot3.jpg)

2. Настройте hello мониторинг параметр tooselect hello учетной записи хранилища куда tooplace эти файлы диагностики.
 
    ![Создание виртуальной машины](./media/boot-diagnostics/screenshot4.jpg)

3. При развертывании на основе шаблона Azure Resource Manager перейдите tooyour ресурса виртуальной машины и добавить профиль раздел hello диагностики. Не забывайте заголовок версии API «2015-06-15» hello toouse.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. Hello диагностического профиля позволяет учетной записи хранилища hello tooselect место tooput эти журналы.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a>Обновление имеющейся виртуальной машины

Диагностика загрузки tooenable через портал hello, можно также обновить существующую виртуальную машину через портал hello. Выберите hello Диагностика загрузки и сохранить. Перезапустите эффект tootake hello виртуальной Машины.

![Обновление имеющейся виртуальной машины](./media/boot-diagnostics/screenshot5.png)