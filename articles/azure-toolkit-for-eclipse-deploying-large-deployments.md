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
# <a name="deploying-large-deployments"></a>Развертывание крупных систем
Если развертывание слишком большой toobe, содержащиеся в папке approot по умолчанию hello, можно использовать ресурс локального хранилища в качестве корневой папки развертывания hello для пакета JDK и сервера приложений.

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a>toouse ресурс локального хранилища, как hello корневой папки развертывания для крупных развертываний
1. Создайте новый локальный ресурс хранилища. Имя Hello hello ресурса не имеет значения. Ресурсы хранилища определяются на уровне роли hello. Hello быстрым способом tooaccess hello локального хранилища конфигурации диалогового окна, из которого можно создать новый ресурс локального хранилища, можно с помощью hello следующие шаги: щелкните правой кнопкой мыши роль hello в hello **обозревателя проектов** представление (разверните вашей Узел проекта Azure, если вы не видите hello роли), нажмите кнопку **Azure**, а затем нажмите кнопку **локального хранилища**. В рамках hello **локального хранилища** диалоговое окно, нажмите кнопку **добавить** toocreate новый ресурс локального хранилища.

2. Набор hello требуемого размера tooat как минимум 2048 МБ (меньшее значение может вызвать hello же проблемы с размером файлов, которые возникли в hello approot).

3. Убедитесь, что **очистить содержимое hello при перезапуске экземпляра роли hello** проверяется; это поможет предотвратить столкнулись конфликтует с уже существующими файлами в ресурсе hello логику запуска развертывания hello при hello роли экземпляр будет перезапущен.

4. Убедитесь, что hello **переменной хранения среды hello путь к каталогу ресурса после развертывания** toohello строка имеет значение **DEPLOYROOT**. Ваше диалоговое окно ресурсов локального хранилища будет выглядеть аналогично toohello следующее.

   ![][ic667943]

Кроме того Если вы используете **DEPLOYROOT** как hello *имя* локального ресурса, и вы не измените имя переменной среды, автоматически создается hello (которого будет установлено слишком **DEPLOYROOT_PATH** в этом случае), который будет работать для вашего приложения, а также.

Дополнительные сведения о создании локального ресурса хранилища вы можете найти в статье [Свойства локального хранилища][Local storage properties].

## <a name="see-also"></a>См. также
[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]

[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
