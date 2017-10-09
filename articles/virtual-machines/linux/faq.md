---
title: "вопросы и ответы для виртуальных машин Linux в Azure aaaFrequently | Документы Microsoft"
description: "Предоставляет ответы toosome hello часто задаваемых вопросов о виртуальных машинах Linux, созданных с помощью модели hello диспетчера ресурсов."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a>Часто задаваемые вопросы по виртуальным машинам Linux
В этой статье рассматриваются некоторые распространенные вопросы о виртуальных машин Linux, созданных в Azure с помощью модели развертывания диспетчера ресурсов hello. Версию Windows hello в этом разделе см. в разделе [часто задаваемые вопросы о виртуальных машинах](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Что можно запускать на виртуальной машине Azure?
Все подписчики могут запускать на виртуальной машине Azure серверное программное обеспечение. Дополнительные сведения см. в статье [Linux в Azure — рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Какой объем памяти можно использовать с виртуальной машиной?
Каждый диск данных может быть вверх too1 ТБ. Hello количество дисков данных, которые можно использовать зависит от размера hello hello виртуальной машины. Дополнительную информацию см. в статье [Размеры виртуальных машин](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Учетная запись хранилища Azure предоставляет хранилище для диска операционной системы hello и диски с данными. Каждый из этих дисков представляет собой VHD-файл, хранящийся как страничный BLOB-объект. Информацию о ценах см. в статье [Информация о ценах на хранилища](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Как получить доступ к своей виртуальной машине?
Установите подключение к удаленному toolog на toohello виртуальную машину, используя Secure Shell (SSH). В разделе hello инструкции о том, как tooconnect [из Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [из Mac и Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). По умолчанию SSH поддерживает не более 10 параллельных подключений. Это число можно увеличить, изменив файл конфигурации hello.

Если возникают проблемы, ознакомьтесь со статьей об [устранении неполадок с подключением Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a>Можно использовать (/ dev/sdb1) toostore hello временный диск данных?
Не следует использовать (/ dev/sdb1) toostore hello временный диск данных. Он обеспечивает лишь временное хранение. Вы рискуете потерять данные, которые невозможно будет восстановить.

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Можно ли копировать или клонировать существующую виртуальную машину Azure?
Да. Инструкции см. в разделе [как toocreate копию виртуальной машины Linux в hello модели развертывания диспетчера ресурсов](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Почему в Azure Resource Manager не отображаются регионы центральной и восточной Канады?
две новые области Hello центра Канады и Восточная Канада автоматически не зарегистрированы для создания виртуальной машины для существующих подписок Azure. Эта регистрация выполняется автоматически при развертывании виртуальной машины с помощью hello Azure портала tooany другой области, с помощью диспетчера ресурсов Azure. После виртуальной машины не развернутой tooany другой регион Azure hello новые области должны быть доступны для последующих виртуальных машин.

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Можно добавить toomy сетевого Адаптера виртуальной Машины после ее создания?
Да, теперь это возможно. Первый toobe потребностей Hello ВМ остановлена освобождена. Затем можно добавить или удалить сетевой Адаптер (если он не является последней сетевой Адаптер для виртуальной Машины hello hello). 

## <a name="are-there-any-computer-name-requirements"></a>Есть ли какие-либо требования к имени компьютера?
Да. Имя компьютера Hello может быть более 64 символов. Дополнительные сведения об именовании ресурсов см. в [правилах и ограничениях соглашений об именовании](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="are-there-any-resource-group-name-requirements"></a>Есть ли какие-либо требования к имени группы ресурсов?
Да. Имя группы ресурсов Hello может быть более 90 символов в длину. Дополнительные сведения о группах ресурсов см. в [правилах и ограничениях соглашений об именовании](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Каковы требования к имени пользователя hello, при создании виртуальной Машины?
Длина имени пользователя должно быть от 1 до 64 знаков.

Hello следующие имена пользователей не разрешены:

<table>
    <tr>
        <td style="text-align:center">administrator </td><td style="text-align:center"> admin </td><td style="text-align:center"> user </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>
    <tr>
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
Пароли необходимо 6 72 символов и удовлетворять 3 из следующих 4 требованиям сложности hello:

* используются строчные знаки;
* используются прописные знаки;
* используется цифра;
* используется специальный знак (регулярное выражение [\W_]).

Hello следующие пароли не допускаются:

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center">P@$$w0rd</td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center">Pa$$word</td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center">Password!</td>
        <td style="text-align:center">Password1</td>
        <td style="text-align:center">Password22</td>
        <td style="text-align:center">iloveyou!</td>
    </tr>
</table>
