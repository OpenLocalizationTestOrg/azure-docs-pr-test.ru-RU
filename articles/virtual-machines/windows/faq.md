---
title: "aaaFAQ о виртуальных машинах Windows в Azure | Документы Microsoft"
description: "Предоставляет ответы toosome hello часто задаваемых вопросов о виртуальных машинах, созданных с помощью модели hello диспетчера ресурсов."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Часто задаваемые вопросы по виртуальным машинам Windows
В этой статье рассматриваются некоторые распространенные вопросы о виртуальных машинах, созданных в Azure с помощью модели развертывания диспетчера ресурсов hello. Hello Linux версию этого раздела см. в разделе [часто задаваемые вопросы о виртуальных машин Linux](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Что можно запускать на виртуальной машине Azure?
Все подписчики могут запускать на виртуальной машине Azure серверное программное обеспечение. Сведения о политике поддержки hello для выполнения серверного программного обеспечения Майкрософт в Azure см. в разделе [поддержка по Microsoft server для виртуальных машин Azure](https://support.microsoft.com/kb/2721672)

Определенные версии Windows 7, Windows 8.1 и Windows 10, доступные tooMSDN Azure подписчикам, а также подписчикам MSDN Dev и Test Pay-As-You-Go, для задач разработки и тестирования. Дополнительные сведения, включая указания и ограничения, см. в статье [Образы клиента Windows для подписчиков MSDN](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/). 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Какой объем памяти можно использовать с виртуальной машиной?
Каждый диск данных может быть вверх too1 ТБ. Hello количество дисков данных, которые можно использовать зависит от размера hello hello виртуальной машины. Дополнительную информацию см. в статье [Размеры виртуальных машин](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Диски Azure управляемых являются hello новый и рекомендуемые диска предложения по хранению для использования с виртуальными машинами Azure для постоянного хранения данных. Можно использовать несколько управляемых дисков для каждой виртуальной машины. Есть два класса управляемых дисков с разными возможностями хранения: управляемые диски "Премиум" и "Стандартный". Сведения о ценах см. на [странице с расценками на управляемые диски](https://azure.microsoft.com/pricing/details/managed-disks).

Учетные записи хранилища Azure можно также предоставить хранилища для hello диска операционной системы и дисков данных. Каждый из этих дисков представляет собой VHD-файл, хранящийся как страничный BLOB-объект. Информацию о ценах см. в статье [Информация о ценах на хранилища](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Как получить доступ к своей виртуальной машине?
Установите удаленное подключение с использованием протокола удаленного рабочего стола (RDP) к виртуальной машине Windows. Инструкции см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Поддерживаются более двух одновременных подключений, если сервер hello не настроен в качестве узла сеансов служб удаленных рабочих столов.  

Если у вас возникают проблемы с удаленным рабочим столом, см. раздел [tooa подключений удаленного рабочего стола на устранение неполадок виртуальной машины на основе Windows Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Если вы знакомы с Hyper-V, то возможно ищете tooVMConnect аналогичные средства. Azure не предлагает аналогичное средство, так как консоль доступа tooa виртуальной машины не поддерживается.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>Можно использовать данные toostore hello временный диск (hello диск D: по умолчанию)
Не используйте hello временный диск toostore данных. Он обеспечивает лишь временное хранение, поэтому вы рискуете потерять данные, которые невозможно восстановить. Перемещение виртуальной машины hello tooa другой узел, может произойти потеря данных. Изменение размера виртуальной машины, обновление hello узла или сбоя оборудования на узле hello перечислены hello причин, по которым виртуальная машина может перемещаться.

Если у вас есть приложение, которое требуется буква диска D: toouse hello, можно переназначить буквы дисков, чтобы hello временный диск использует нечто, отличное от D:. Инструкции см. в разделе [изменений hello букву временного диска Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Как изменить букву диска hello hello временного диска?
Вы можете изменить букву диска hello путем перемещения файла подкачки hello и повторное назначение буквы диска, но необходимо убедиться, что hello действия в определенном порядке toomake. Инструкции см. в разделе [изменений hello букву временного диска Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>Можно добавить существующую группу доступности виртуальной Машины tooan?
Нет. Следует ли ВМ toobe частью группы доступности необходимо toocreate hello виртуальной Машины в наборе hello. В настоящее время не tooadd способом доступности tooan виртуальной Машины, после его создания.

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>Можно загрузить tooAzure виртуальной машины?
Да. Инструкции см. в разделе [перенос локальных виртуальных машин tooAzure](on-prem-to-azure.md).

## <a name="can-i-resize-hello-os-disk"></a>Можно ли изменить размер диска ОС hello?
Да. Инструкции см. в разделе [как tooexpand hello диска операционной системы виртуальной машины в группу ресурсов Azure](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Можно ли копировать или клонировать существующую виртуальную машину Azure?
Да. Управляемые образы можно создать образ виртуальной машины и затем использовать hello изображения toobuild несколько новых виртуальных машин. Инструкции см. здесь: [Создание пользовательского образа виртуальной машины](tutorial-custom-images.md).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Почему в Azure Resource Manager не отображаются регионы центральной и восточной Канады?

две новые области Hello центра Канады и Восточная Канада автоматически не зарегистрированы для создания виртуальной машины для существующих подписок Azure. Эта регистрация выполняется автоматически при развертывании виртуальной машины с помощью hello Azure портала tooany другой области, с помощью диспетчера ресурсов Azure. После виртуальной машины не развернутой tooany другой регион Azure hello новые области должны быть доступны для последующих виртуальных машин.

## <a name="does-azure-support-linux-vms"></a>Поддерживает ли Azure виртуальные машины Linux?
Да. tooquickly Создание виртуальной Машины с Linux tootry ожидания см. в разделе [Создание виртуальной Машины Linux в Azure, с помощью портала hello](../linux/quick-create-portal.md).

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Можно добавить toomy сетевого Адаптера виртуальной Машины после ее создания?
Да, теперь это возможно. Первый toobe потребностей Hello ВМ остановлена освобождена. Затем можно добавить или удалить сетевой Адаптер (если он не является последней сетевой Адаптер для виртуальной Машины hello hello). 

## <a name="are-there-any-computer-name-requirements"></a>Есть ли какие-либо требования к имени компьютера?
Да. Имя компьютера Hello может быть более 15 символов. Дополнительные сведения об именовании ресурсов см. в [правилах и ограничениях соглашений об именовании](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="are-there-any-resource-group-name-requirements"></a>Есть ли какие-либо требования к имени группы ресурсов?
Да. Имя группы ресурсов Hello может быть более 90 символов в длину. Дополнительные сведения о группах ресурсов см. в [правилах и ограничениях соглашений об именовании](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Каковы требования к имени пользователя hello, при создании виртуальной Машины?

Длина имени пользователя не должна превышать 20 знаков. Также оно не должно заканчиваться точкой ("."). 


Hello следующие имена пользователей не разрешены:
<table>
    <tr>
        <td style="text-align:center">administrator </td><td style="text-align:center"> admin </td><td style="text-align:center"> user </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> a</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> aspnet</td>
    </tr>
    <tr>
        <td style="text-align:center">backup </td><td style="text-align:center"> console </td><td style="text-align:center"> david </td><td style="text-align:center"> guest</td>
    </tr>
    <tr>
        <td style="text-align:center">john </td><td style="text-align:center"> владелец </td><td style="text-align:center"> root </td><td style="text-align:center"> server</td>
    </tr>
    <tr>
        <td style="text-align:center">sql </td><td style="text-align:center"> support </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">test2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> user4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>

## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>Каковы требования к паролю hello при создании виртуальной Машины?
Пароли необходимо 12 123 символов и удовлетворять 3 из следующих 4 требованиям сложности hello:

* используются строчные знаки;
* используются прописные знаки;
* используется цифра;
* используется специальный знак (регулярное выражение [\W_]).

Hello следующие пароли не допускаются:

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Pa$$word </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Password! </td>
        <td>Password1 </td>
        <td>Password22 </td>
        <td>iloveyou! </td>
    </tr>
</table>
