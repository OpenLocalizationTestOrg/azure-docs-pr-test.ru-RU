---
title: "Как назначить доступ на основе MSI к ресурсу Azure с помощью портала Azure"
description: "Пошаговые инструкции по назначению MSI для одного ресурса и предоставлению доступа другому ресурсу с помощью портала Azure."
services: active-directory
documentationcenter: 
author: BryanLa
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/15/2017
ms.author: bryanla
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: 7d0a50db28ba3d9926f7a83fe224b7a0dbe6ed20
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="assign-a-managed-service-identity-access-to-a-resource-by-using-the-azure-portal"></a>Назначение доступа на основе управляемого удостоверения службы для ресурса с помощью портала Azure

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

После настройки MSI для ресурса Azure можно предоставить доступ на основе удостоверения управляемой службы (MSI) другому ресурсу, как и любому субъекту безопасности. В этой статье показано, как предоставить виртуальной машине Azure доступ на основе MSI к учетной записи хранения Azure с помощью портала Azure.

## <a name="prerequisites"></a>Технические условия

[!INCLUDE [msi-core-prereqs](~/includes/active-directory-msi-core-prereqs-ua.md)]

## <a name="use-rbac-to-assign-the-msi-access-to-another-resource"></a>Использование RBAC для назначения доступа на основе MSI другому ресурсу

После включения MSI для ресурса Azure, [например виртуальной машины Azure](msi-qs-configure-portal-windows-vm.md):

1. Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи, связанной с подпиской Azure, для которой вы настроили MSI.

2. Перейдите к нужному ресурсу, для которого требуется изменить управление доступом. В этом примере мы предоставляем виртуальной машине Azure доступ к учетной записи хранения, поэтому мы переходим к учетной записи хранения.

3. Перейдите на страницу **Управление доступом (IAM)** ресурса, затем нажмите кнопку **+Добавить**. Укажите **роль**, **предоставьте доступ к виртуальной машине** и укажите соответствующие **подписку** и **группу ресурсов** для ресурса. В области критериев поиска отобразится ресурс. Выберите этот ресурс и нажмите кнопку **Сохранить**. 

   ![Снимок экрана "Управление доступом (IAM)"](~/articles/active-directory/media/msi-howto-assign-access-portal/assign-access-control-iam-blade-before.png)  

4. Вы вернетесь на главную страницу **Управление доступом (IAM)**, на которой вы увидите новую запись для MSI ресурса. В этом примере виртуальной машине SimpleWinVM из группы ресурсов Demo был предоставлен доступ с правами **Участник** к учетной записи хранения.

   ![Снимок экрана "Управление доступом (IAM)"](~/articles/active-directory/media/msi-howto-assign-access-portal/assign-access-control-iam-blade-after.png)

## <a name="troubleshooting"></a>Устранение неполадок

Если MSI для ресурса не отображается в списке доступных удостоверений, убедитесь, что вы правильно включили MSI. В нашем случае мы можем вернуться к виртуальной машине Azure, чтобы:

- просмотреть страницу **Конфигурация** и убедиться, что **поддержка MSI** **включена**;
- просмотреть страницу **Расширения** и убедиться, что расширение MSI успешно развернуто.

Если какое-либо из условий не выполнено, может потребоваться повторно развернуть MSI для ресурса или устранить неполадки с развертыванием.

## <a name="related-content"></a>Связанная информация

- Общие сведения об MSI см. в разделе [Управляемое удостоверение службы (MSI) для Azure Active Directory](msi-overview.md).
- О том, как включить MSI для виртуальной машины Azure, можно узнать в разделе [Настройка управляемого удостоверения службы (MSI) на виртуальной машине Azure с помощью портала Azure](msi-qs-configure-portal-windows-vm.md).


