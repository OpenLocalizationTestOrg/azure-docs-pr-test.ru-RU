---
title: "aaaManaging роли в Azure облачными службами с помощью Visual Studio | Документы Microsoft"
description: "Дополнительные сведения об tooadd и удаление ролей в Azure облачных служб с помощью Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Управление ролями в облачных службах Azure с помощью Visual Studio
После создания облачной службы Azure, можно добавить новый tooit роли или удалить из него существующие роли. Также можно импортировать существующий проект и преобразовать его tooa роли. Например, можно импортировать веб-приложение ASP.NET и использовать его в качестве веб-роли.

## <a name="adding-a-role-tooan-azure-cloud-service"></a>Добавление роли tooan облачной службы Azure
Привет, выполнив действия позволят вам добавить веб- или рабочей роли tooan проекта облачной службы Azure в Visual Studio.

1. Создайте или откройте проект облачной службы Azure в среде Visual Studio.

1. В **обозревателе решений**, разверните узел проекта hello

1. Щелкните правой кнопкой мыши hello **ролей** контекстное меню узла toodisplay hello. Hello контекстном меню, выберите **добавить**, выберите существующий веб-роли или рабочей роли из текущего решения hello, или создайте проект веб- или рабочей роли. Вы также можете выбрать соответствующий проект, например проект веб-приложения ASP.NET, и связать его с проектом роли.

    ![Параметры меню tooadd роли tooan проекта облачной службы Azure](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Удаление роли из облачной службы Azure
Hello следующие шаги описывают удаление рабочих и веб-роли из проекта облачной службы Azure в Visual Studio.

1. Создайте или откройте проект облачной службы Azure в среде Visual Studio.

1. В **обозревателе решений**, разверните узел проекта hello

1. Разверните hello **ролей** узла.

1. Щелкните правой кнопкой мыши узел hello tooremove и, hello контекстном меню, выберите **удалить**. 

    ![Параметры меню tooadd tooan роли облачной службы Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a>Повторное добавление роли tooan проекта облачной службы Azure
Если удалить роль из проекта облачной службы, но позднее tooadd hello роль обратно toohello проект, только декларация роли hello и основные атрибуты, такие как конечные точки и диагностические сведения, будут добавлены. Дополнительные ресурсы или ссылки не будут добавлены toohello `ServiceDefinition.csdef` файл или toohello `ServiceConfiguration.cscfg` файл. Если вы хотите tooadd эти сведения, необходимые toomanually добавьте его обратно в эти файлы.

Например можно удалить роль веб-службы и позднее tooadd эту роль обратно в ваше решение. Если это сделать, то произойдет ошибка. tooprevent эту ошибку, у вас есть tooadd hello `<LocalResources>` элемент, показанный в следующие hello XML обратно в hello `ServiceDefinition.csdef` файла. Используйте имя hello hello веб-службы роли, который вы добавили обратно в проект hello как часть атрибута имени hello hello  **<LocalStorage>**  элемента. В этом примере hello hello веб-служба роли называется **WCFServiceWebRole1**.

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>Дальнейшие действия
- [Настройка ролей hello для облачной службы Azure с помощью Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md)
