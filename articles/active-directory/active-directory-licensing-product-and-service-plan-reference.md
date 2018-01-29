---
title: "Названия продуктов и идентификаторы планов служб для лицензирования в Azure Active Directory | Документация Майкрософт"
description: "Сопоставление идентификаторов для управления лицензированием в Azure AD с помощью порталов Azure и Office 365, PowerShell или Microsoft Graph"
services: active-directory
keywords: "Планы службы лицензирования Azure Active Directory"
documentationcenter: 
author: piotrci
manager: mtillman
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 10/26/2017
ms.author: piotrci
ms.openlocfilehash: 421c7472442c0f01a99ac2ae8c49417b26724573
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="product-names-and-service-plan-identifiers-for-licensing"></a>Названия продуктов и идентификаторы планов служб для лицензирования

При управлении лицензиями на порталах [Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) или Office 365 вы видите названия продуктов в таком формате: *Office 365 Enterprise E3*. Когда используются командлеты PowerShell версии 1.0, тот же продукт определяется с помощью определенного, но менее понятного имени *ENTERPRISEPACK*. При использовании командлетов PowerShell версии 2.0 или Microsoft Graph продукт идентифицируется с помощью значения GUID: *6fd2c87f-b296-42f0-b197-1e91e994b900*. В таблице ниже представлен список самых популярных продуктов Microsoft Online Services, а также значения их идентификаторов.

- **Название продукта**. Используется на порталах управления.
- **Идентификатор строки**. Используется командлетами PowerShell версии 1.0 для операций с лицензиями.
- **Идентификатор GUID**. Идентификатор, используемый в Azure AD Graph и Microsoft Graph.
- **Включенные планы службы**. Список планов службы предусмотренных для продукта, которые соответствуют идентификатору строки и GUID.

>[!NOTE]
>Эти сведения достоверные по состоянию на 11 октября 2017 года.

| Название продукта | Идентификатор строки | GUID | Включенные планы службы |
| --- | --- | --- |--- |
| Azure Active Directory Basic  | AAD_BASIC | 2b9c8e7c-319c-43a2-a2a0-48c5c6161de7  | AAD_BASIC (c4da7f8a-5ee2-4c99-a7e1-87d2df57f6fe)
| Azure Active Directory Premium P1 | AAD_PREMIUM   | 078d2b04-f1bd-4111-bbd4-b4b1b354cef4  | AAD_PREMIUM (41781fb2-bc02-4b7c-bd55-b576c07bb09d)<br/>MFA_PREMIUM (8a256a2b-b617-496d-b51b-e76466e88db0)
| Azure Information Protection Plan 1   | RIGHTSMANAGEMENT  | c52ea49f-fe5d-4e95-93ba-1de91d380f89  | RMS_S_ENTERPRISE (bea4c11e-220a-4e6d-8eb8-8ea15d019f90)<br/>RMS_S_PREMIUM (6c57d4b6-3b23-47a5-9bc9-69f17b4947b3)
| Dynamics 365 Customer Engagement Plan Enterprise Edition  | DYN365_ENTERPRISE_PLAN1   | ea126fc5-a19e-42e2-a731-da9d437bffcf  | DYN365_ENTERPRISE_P1 (d56f3deb-50d8-465a-bedb-f079817ccac1)<br/>FLOW_DYN_P2 (b650d915-9886-424b-a08d-633cede56f57)<br/>NBENTERPRISE (03acaee3-9492-4f40-aed4-bcb6b32981b6)<br/>POWERAPPS_DYN_P2 (0b03f40b-c404-40c3-8651-2aceb74365fa)<br/>PROJECT_CLIENT_SUBSCRIPTION (fafd7243-e5c1-4a3a-9e40-495efcb1d3c3)<br/>SHAREPOINT_PROJECT (fe71d6c3-a2ea-4499-9778-da042bf08063)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)
| Dynamics 365 for Financials Business Edition  | DYN365_FINANCIALS_BUSINESS_SKU    | cc13a803-544e-4464-b4e4-6d6169a138fa  | DYN365_FINANCIALS_BUSINESS (920656a2-7dd8-4c83-97b6-a356414dbd36)<br/>FLOW_DYN_APPS (7e6d7d78-73de-46ba-83b1-6d25117334ba)<br/>POWERAPPS_DYN_APPS (874fc546-6efe-4d22-90b8-5c4e7aa59f4b)
| Dynamics 365 for Sales Enterprise Edition | DYN365_ENTERPRISE_SALES   | 1e1a282c-9c54-43a2-9310-98ef728faace  | DYN365_ENTERPRISE_SALES (2da8e897-7791-486b-b08f-cc63c8129df7)<br/>FLOW_DYN_APPS (7e6d7d78-73de-46ba-83b1-6d25117334ba)<br/>NBENTERPRISE (03acaee3-9492-4f40-aed4-bcb6b32981b6)<br/>POWERAPPS_DYN_APPS (874fc546-6efe-4d22-90b8-5c4e7aa59f4b)<br/>PROJECT_ESSENTIALS (1259157c-8581-4875-bca7-2ffb18c51bda)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)
| Dynamics 365 for Team Members Enterprise Edition  | DYN365_ENTERPRISE_TEAM_MEMBERS    | 8e7a3d30-d97d-43ab-837c-d7701cef83dc  | DYN365_Enterprise_Talent_Attract_TeamMember (643d201a-9884-45be-962a-06ba97062e5e)<br/>DYN365_Enterprise_Talent_Onboard_TeamMember (f2f49eef-4b3f-4853-809a-a055c6103fe0)<br/>DYN365_ENTERPRISE_TEAM_MEMBERS (6a54b05e-4fab-40e7-9828-428db3b336fa)<br/>Dynamics_365_for_Operations_Team_members (f5aa7b45-8a36-4cd1-bc37-5d06dea98645)<br/>Dynamics_365_for_Retail_Team_members (c0454a3d-32b5-4740-b090-78c32f48f0ad)<br/>Dynamics_365_for_Talent_Team_members (d5156635-0704-4f66-8803-93258f8b2678)<br/>FLOW_DYN_TEAM (1ec58c70-f69c-486a-8109-4b87ce86e449)<br/>POWERAPPS_DYN_TEAM (52e619e2-2730-439a-b0d3-d09ab7e8b705)<br/>PROJECT_ESSENTIALS (1259157c-8581-4875-bca7-2ffb18c51bda)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)
| Enterprise Mobility + Security E3 | EMS   | efccb6f7-5641-4e0e-bd10-b4976e1bf68e  | AAD_PREMIUM (41781fb2-bc02-4b7c-bd55-b576c07bb09d)<br/>ADALLOM_S_DISCOVERY (932ad362-64a8-4783-9106-97849a1a30b9)<br/>INTUNE_A (c1ec4a95-1f05-45b3-a911-aa3fa01094f5)<br/>MFA_PREMIUM (8a256a2b-b617-496d-b51b-e76466e88db0)<br/>RMS_S_ENTERPRISE (bea4c11e-220a-4e6d-8eb8-8ea15d019f90)<br/>RMS_S_PREMIUM (6c57d4b6-3b23-47a5-9bc9-69f17b4947b3)
| Enterprise Mobility + Security E5 | EMSPREMIUM    | b05e124f-c7cc-45a0-a6aa-8cf78c946968  | AAD_PREMIUM (41781fb2-bc02-4b7c-bd55-b576c07bb09d)<br/>AAD_PREMIUM_P2 (eec0eb4f-6444-4f95-aba0-50c24d67f998)<br/>ADALLOM_S_STANDALONE (2e2ddb96-6af9-4b1d-a3f0-d6ecfd22edb2)<br/>INTUNE_A (c1ec4a95-1f05-45b3-a911-aa3fa01094f5)<br/>MFA_PREMIUM (8a256a2b-b617-496d-b51b-e76466e88db0)<br/>RMS_S_ENTERPRISE (bea4c11e-220a-4e6d-8eb8-8ea15d019f90)<br/>RMS_S_PREMIUM (6c57d4b6-3b23-47a5-9bc9-69f17b4947b3)<br/>RMS_S_PREMIUM2 (5689bec4-755d-4753-8b61-40975025187c)
| Exchange Online (Plan 1)  | EXCHANGESTANDARD  | 4b9405b0-7788-4568-add1-99614e613b69  | EXCHANGE_S_STANDARD (9aaf7827-d63c-4b61-89c3-182f06f82e5c)
| Exchange Online (Plan 2)  | EXCHANGEENTERPRISE    | 19ec0d23-8335-4cbd-94ac-6050e30712fa  | EXCHANGE_S_ENTERPRISE (efb87545-963c-4e0d-99df-69c6916d9eb0)
| Exchange Online Archiving for Exchange Online | EXCHANGEARCHIVE_ADDON | ee02fd1b-340e-4a4b-b355-4a514e4c8943  | EXCHANGE_S_ARCHIVE_ADDON (176a09a6-7ec5-4039-ac02-b2791c6ba793)
| Exchange Online Archiving for Exchange Server | EXCHANGEARCHIVE   | 90b5e015-709a-4b8b-b08e-3200f994494c  | EXCHANGE_S_ARCHIVE (da040e0a-b393-4bea-bb76-928b3fa1cf5a)
| Exchange Online Essentials    | EXCHANGEESSENTIALS    | 7fc0182e-d107-4556-8329-7caaa511197b  | EXCHANGE_S_STANDARD (9aaf7827-d63c-4b61-89c3-182f06f82e5c)
| Exchange Online Essentials    | EXCHANGE_S_ESSENTIALS | e8f81a67-bd96-4074-b108-cf193eb9433b  | EXCHANGE_S_ESSENTIALS (1126bef5-da20-4f07-b45e-ad25d2581aa8)
| Exchange Online Kiosk | EXCHANGEDESKLESS  | 80b2d799-d2ba-4d2a-8842-fb0d0f3a4b82  | EXCHANGE_S_DESKLESS (4a82b400-a79f-41a4-b4e2-e94f5787b113)
| Intune    | INTUNE_A  | 061f9ace-7d42-4136-88ac-31dc755f143f  | INTUNE_A (c1ec4a95-1f05-45b3-a911-aa3fa01094f5)
| Microsoft Dynamics CRM Online Basic   | CRMPLAN2  | 906af65a-2970-46d5-9b58-4e9aa50f0657  | CRMPLAN2 (bf36ca64-95c6-4918-9275-eb9f4ce2c04f)<br/>FLOW_DYN_APPS (7e6d7d78-73de-46ba-83b1-6d25117334ba)<br/>POWERAPPS_DYN_APPS (874fc546-6efe-4d22-90b8-5c4e7aa59f4b)
| Microsoft Dynamics CRM Online Professional    | CRMSTANDARD   | d17b27af-3f49-4822-99f9-56a661538792  | CRMSTANDARD (f9646fb2-e3b2-4309-95de-dc4833737456)<br/>FLOW_DYN_APPS (7e6d7d78-73de-46ba-83b1-6d25117334ba)<br/>MDM_SALES_COLLABORATION (3413916e-ee66-4071-be30-6f94d4adfeda)<br/>NBPROFESSIONALFORCRM (3e58e97c-9abe-ebab-cd5f-d543d1529634)<br/>POWERAPPS_DYN_APPS (874fc546-6efe-4d22-90b8-5c4e7aa59f4b)
| Microsoft Intune A Direct | INTUNE_A  | 061f9ace-7d42-4136-88ac-31dc755f143f  | INTUNE_A (c1ec4a95-1f05-45b3-a911-aa3fa01094f5)
| MS Imagine Academy    | IT_ACADEMY_AD | ba9a34de-4489-469d-879c-0f0f145321cd  | IT_ACADEMY_AD (d736def0-1fde-43f0-a5be-e3f8b2de6e41)
| Office 365 Business   | O365_BUSINESS | cdd28e44-67e3-425e-be4c-737fab2899d3  | FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>OFFICE_BUSINESS (094e7854-93fc-4d55-b2c0-3ab5369ebdc1)<br/>ONEDRIVESTANDARD (13696edf-5a08-49f6-8134-03083ed8ba30)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)
| Office 365 Business   | SMB_BUSINESS  | b214fe43-f5a3-4703-beeb-fa97188220fc  | FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>OFFICE_BUSINESS (094e7854-93fc-4d55-b2c0-3ab5369ebdc1)<br/>ONEDRIVESTANDARD (13696edf-5a08-49f6-8134-03083ed8ba30)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)
| Office 365 Business Essentials    | O365_BUSINESS_ESSENTIALS  | 3b555118-da6a-4418-894f-7df1e2096870  | EXCHANGE_S_STANDARD (9aaf7827-d63c-4b61-89c3-182f06f82e5c)<br/>FLOW_O365_P1 (0f9b09cb-62d1-4ff4-9129-43f4996f83f4)<br/>FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>POWERAPPS_O365_P1 (92f7a6f3-b89b-4bbd-8c30-809e6da5ad1c)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>SHAREPOINTSTANDARD (c7699d2e-19aa-44de-8edf-1736da088ca1)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>YAMMER_ENTERPRISE (7547a3fe-08ee-4ccb-b430-5077c5041653)
| Office 365 Business Essentials    | SMB_BUSINESS_ESSENTIALS   | dab7782a-93b1-4074-8bb1-0e61318bea0b  | EXCHANGE_S_STANDARD (9aaf7827-d63c-4b61-89c3-182f06f82e5c)<br/>FLOW_O365_P1 (0f9b09cb-62d1-4ff4-9129-43f4996f83f4)<br/>FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>POWERAPPS_O365_P1 (92f7a6f3-b89b-4bbd-8c30-809e6da5ad1c)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>SHAREPOINTSTANDARD (c7699d2e-19aa-44de-8edf-1736da088ca1)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>YAMMER_MIDSIZE (41bf139a-4e60-409f-9346-a1361efc6dfb)
| Office 365 Business Premium   | O365_BUSINESS_PREMIUM | f245ecc8-75af-4f8e-b61f-27d8114de5f3  | EXCHANGE_S_STANDARD (9aaf7827-d63c-4b61-89c3-182f06f82e5c)<br/>FLOW_O365_P1 (0f9b09cb-62d1-4ff4-9129-43f4996f83f4)<br/>FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>MICROSOFTBOOKINGS (199a5c09-e0ca-4e37-8f7c-b05d533e1ea2)<br/>O365_SB_Relationship_Management (5bfe124c-bbdc-4494-8835-f1297d457d79)<br/>OFFICE_BUSINESS (094e7854-93fc-4d55-b2c0-3ab5369ebdc1)<br/>POWERAPPS_O365_P1 (92f7a6f3-b89b-4bbd-8c30-809e6da5ad1c)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>SHAREPOINTSTANDARD (c7699d2e-19aa-44de-8edf-1736da088ca1)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>YAMMER_ENTERPRISE (7547a3fe-08ee-4ccb-b430-5077c5041653)
| Office 365 Business Premium   | SMB_BUSINESS_PREMIUM  | ac5cef5d-921b-4f97-9ef3-c99076e5470f  | EXCHANGE_S_STANDARD (9aaf7827-d63c-4b61-89c3-182f06f82e5c)<br/>FLOW_O365_P1 (0f9b09cb-62d1-4ff4-9129-43f4996f83f4)<br/>FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>MICROSOFTBOOKINGS (199a5c09-e0ca-4e37-8f7c-b05d533e1ea2)<br/>O365_SB_Relationship_Management (5bfe124c-bbdc-4494-8835-f1297d457d79)<br/>OFFICE_BUSINESS (094e7854-93fc-4d55-b2c0-3ab5369ebdc1)<br/>POWERAPPS_O365_P1 (92f7a6f3-b89b-4bbd-8c30-809e6da5ad1c)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>SHAREPOINTSTANDARD (c7699d2e-19aa-44de-8edf-1736da088ca1)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>YAMMER_MIDSIZE (41bf139a-4e60-409f-9346-a1361efc6dfb)
| Office 365 Enterprise E1  | STANDARDPACK  | 18181a46-0d4e-45cd-891e-60aabd171b4e  | Deskless (8c7d2df8-86f0-4902-b2ed-a0458298f3b3)<br/>EXCHANGE_S_STANDARD (9aaf7827-d63c-4b61-89c3-182f06f82e5c)<br/>FLOW_O365_P1 (0f9b09cb-62d1-4ff4-9129-43f4996f83f4)<br/>FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>POWERAPPS_O365_P1 (92f7a6f3-b89b-4bbd-8c30-809e6da5ad1c)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>SHAREPOINTSTANDARD (c7699d2e-19aa-44de-8edf-1736da088ca1)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>STREAM_O365_E1 (743dd19e-1ce3-4c62-a3ad-49ba8f63a2f6)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>YAMMER_ENTERPRISE (7547a3fe-08ee-4ccb-b430-5077c5041653)
| Office 365 Enterprise E2  | STANDARDWOFFPACK  | 6634e0ce-1a9f-428c-a498-f84ec7b8aa2e  | Deskless (8c7d2df8-86f0-4902-b2ed-a0458298f3b3)<br/>EXCHANGE_S_STANDARD (9aaf7827-d63c-4b61-89c3-182f06f82e5c)<br/>FLOW_O365_P1 (0f9b09cb-62d1-4ff4-9129-43f4996f83f4)<br/>FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>POWERAPPS_O365_P1 (92f7a6f3-b89b-4bbd-8c30-809e6da5ad1c)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>SHAREPOINTSTANDARD (c7699d2e-19aa-44de-8edf-1736da088ca1)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>STREAM_O365_E1 (743dd19e-1ce3-4c62-a3ad-49ba8f63a2f6)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>YAMMER_ENTERPRISE (7547a3fe-08ee-4ccb-b430-5077c5041653)
| Office 365 Enterprise E3  | ENTERPRISEPACK    | 6fd2c87f-b296-42f0-b197-1e91e994b900  | Deskless (8c7d2df8-86f0-4902-b2ed-a0458298f3b3)<br/>EXCHANGE_S_ENTERPRISE (efb87545-963c-4e0d-99df-69c6916d9eb0)<br/>FLOW_O365_P2 (76846ad7-7776-4c40-a281-a386362dd1b9)<br/>FORMS_PLAN_E3 (2789c901-c14e-48ab-a76a-be334d9d793a)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>OFFICESUBSCRIPTION (43de0ff5-c92c-492b-9116-175376d08c38)<br/>POWERAPPS_O365_P2 (c68f8d98-5534-41c8-bf36-22fa496fa792)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>RMS_S_ENTERPRISE (bea4c11e-220a-4e6d-8eb8-8ea15d019f90)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>STREAM_O365_E3 (9e700747-8b1d-45e5-ab8d-ef187ceec156)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>YAMMER_ENTERPRISE (7547a3fe-08ee-4ccb-b430-5077c5041653)
| Office 365 Enterprise E3 Developer    | DEVELOPERPACK | 189a915c-fe4f-4ffa-bde4-85b9628d07a0  | EXCHANGE_S_ENTERPRISE (efb87545-963c-4e0d-99df-69c6916d9eb0)<br/>FLOW_O365_P2 (76846ad7-7776-4c40-a281-a386362dd1b9)<br/>FORMS_PLAN_E5 (e212cbc7-0961-4c40-9825-01117710dcb1)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>OFFICESUBSCRIPTION (43de0ff5-c92c-492b-9116-175376d08c38)<br/>POWERAPPS_O365_P2 (c68f8d98-5534-41c8-bf36-22fa496fa792)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>SHAREPOINT_S_DEVELOPER (a361d6e2-509e-4e25-a8ad-950060064ef4)<br/>SHAREPOINTWAC_DEVELOPER (527f7cdd-0e86-4c47-b879-f5fd357a3ac6)<br/>STREAM_O365_E5 (6c6042f5-6f01-4d67-b8c1-eb99d36eed3e)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)
| Office 365 Enterprise E4  | ENTERPRISEWITHSCAL    | 1392051d-0cb9-4b7a-88d5-621fee5e8711  | Deskless (8c7d2df8-86f0-4902-b2ed-a0458298f3b3)<br/>EXCHANGE_S_ENTERPRISE (efb87545-963c-4e0d-99df-69c6916d9eb0)<br/>FLOW_O365_P2 (76846ad7-7776-4c40-a281-a386362dd1b9)<br/>FORMS_PLAN_E3 (2789c901-c14e-48ab-a76a-be334d9d793a)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>MCOVOICECONF (27216c54-caf8-4d0d-97e2-517afb5c08f6)<br/>OFFICESUBSCRIPTION (43de0ff5-c92c-492b-9116-175376d08c38)<br/>POWERAPPS_O365_P2 (c68f8d98-5534-41c8-bf36-22fa496fa792)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>RMS_S_ENTERPRISE (bea4c11e-220a-4e6d-8eb8-8ea15d019f90)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>STREAM_O365_E3 (9e700747-8b1d-45e5-ab8d-ef187ceec156)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>YAMMER_ENTERPRISE (7547a3fe-08ee-4ccb-b430-5077c5041653)
| Office 365 Enterprise E5  | ENTERPRISEPREMIUM | c7df2760-2c81-4ef7-b578-5b5392b571df  | ADALLOM_S_O365 (8c098270-9dd4-4350-9b30-ba4703f3b36b)<br/>BI_AZURE_P2 (70d33638-9c74-4d01-bfd3-562de28bd4ba)<br/>Deskless (8c7d2df8-86f0-4902-b2ed-a0458298f3b3)<br/>EQUIVIO_ANALYTICS (4de31727-a228-4ec3-a5bf-8e45b5ca48cc)<br/>EXCHANGE_ANALYTICS (34c0d7a0-a70f-4668-9238-47f9fc208882)<br/>EXCHANGE_S_ENTERPRISE (efb87545-963c-4e0d-99df-69c6916d9eb0)<br/>FLOW_O365_P3 (07699545-9485-468e-95b6-2fca3738be01)<br/>FORMS_PLAN_E5 (e212cbc7-0961-4c40-9825-01117710dcb1)<br/>LOCKBOX_ENTERPRISE (9f431833-0334-42de-a7dc-70aa40db46db)<br/>MCOEV (4828c8ec-dc2e-4779-b502-87ac9ce28ab7)<br/>MCOMEETADV (3e26ee1f-8a5f-4d52-aee2-b81ce45c8f40)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>OFFICESUBSCRIPTION (43de0ff5-c92c-492b-9116-175376d08c38)<br/>POWERAPPS_O365_P3 (9c0dab89-a30c-4117-86e7-97bda240acd2)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>RMS_S_ENTERPRISE (bea4c11e-220a-4e6d-8eb8-8ea15d019f90)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>STREAM_O365_E5 (6c6042f5-6f01-4d67-b8c1-eb99d36eed3e)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>THREAT_INTELLIGENCE (8e0c0a52-6a6c-4d40-8370-dd62790dcd70)<br/>YAMMER_ENTERPRISE (7547a3fe-08ee-4ccb-b430-5077c5041653)
| Office 365 Enterprise E5 Without PSTN Conferencing    | ENTERPRISEPREMIUM_NOPSTNCONF  | 26d45bd9-adf1-46cd-a9e1-51e9a5524128  | ADALLOM_S_O365 (8c098270-9dd4-4350-9b30-ba4703f3b36b)<br/>BI_AZURE_P2 (70d33638-9c74-4d01-bfd3-562de28bd4ba)<br/>Deskless (8c7d2df8-86f0-4902-b2ed-a0458298f3b3)<br/>EQUIVIO_ANALYTICS (4de31727-a228-4ec3-a5bf-8e45b5ca48cc)<br/>EXCHANGE_ANALYTICS (34c0d7a0-a70f-4668-9238-47f9fc208882)<br/>EXCHANGE_S_ENTERPRISE (efb87545-963c-4e0d-99df-69c6916d9eb0)<br/>FLOW_O365_P3 (07699545-9485-468e-95b6-2fca3738be01)<br/>FORMS_PLAN_E5 (e212cbc7-0961-4c40-9825-01117710dcb1)<br/>LOCKBOX_ENTERPRISE (9f431833-0334-42de-a7dc-70aa40db46db)<br/>MCOEV (4828c8ec-dc2e-4779-b502-87ac9ce28ab7)<br/>MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)<br/>OFFICESUBSCRIPTION (43de0ff5-c92c-492b-9116-175376d08c38)<br/>POWERAPPS_O365_P3 (9c0dab89-a30c-4117-86e7-97bda240acd2)<br/>PROJECTWORKMANAGEMENT (b737dad2-2f6c-4c65-90e3-ca563267e8b9)<br/>RMS_S_ENTERPRISE (bea4c11e-220a-4e6d-8eb8-8ea15d019f90)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>STREAM_O365_E5 (6c6042f5-6f01-4d67-b8c1-eb99d36eed3e)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>THREAT_INTELLIGENCE (8e0c0a52-6a6c-4d40-8370-dd62790dcd70)<br/>YAMMER_ENTERPRISE (7547a3fe-08ee-4ccb-b430-5077c5041653)
| Office 365 F1 | DESKLESSPACK  | 4b585984-651b-448a-9e53-3b10f069cf7f  | Deskless (8c7d2df8-86f0-4902-b2ed-a0458298f3b3)<br/>EXCHANGE_S_DESKLESS (4a82b400-a79f-41a4-b4e2-e94f5787b113)<br/>FLOW_O365_S1 (bd91b1a4-9f94-4ecf-b45b-3a65e5c8128a)<br/>FORMS_PLAN_K (f07046bd-2a3c-4b96-b0be-dea79d7cbfb8)<br/>MCOIMP (afc06cb0-b4f4-4473-8286-d644f70d8faf)<br/>POWERAPPS_O365_S1 (e0287f9f-e222-4f98-9a83-f379e249159a)<br/>SHAREPOINTDESKLESS (902b47e5-dcb2-4fdc-858b-c63a90a2bdb9)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>STREAM_O365_K (3ffba0d2-38e5-4d5e-8ec0-98f2b05c09d9)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>TEAMS1 (57ff2da0-773e-42df-b2af-ffb7a2317929)<br/>YAMMER_ENTERPRISE (7547a3fe-08ee-4ccb-b430-5077c5041653)
| Office 365 Midsize Business   | MIDSIZEPACK   | 04a7fb0d-32e0-4241-b4f5-3f7618cd1162  | EXCHANGE_S_STANDARD_MIDMARKET (fc52cc4b-ed7d-472d-bbe7-b081c23ecc56)<br/>MCOSTANDARD_MIDMARKET (b2669e95-76ef-4e7e-a367-002f60a39f3e)<br/>OFFICESUBSCRIPTION (43de0ff5-c92c-492b-9116-175376d08c38)<br/>SHAREPOINTENTERPRISE_MIDMARKET (6b5b6a67-fc72-4a1f-a2b5-beecf05de761)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)<br/>YAMMER_MIDSIZE (41bf139a-4e60-409f-9346-a1361efc6dfb)
| Office 365 Proplus    | OFFICESUBSCRIPTION    | c2273bd0-dff7-4215-9ef5-2c7bcfb06425  | FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>OFFICESUBSCRIPTION (43de0ff5-c92c-492b-9116-175376d08c38)<br/>ONEDRIVESTANDARD (13696edf-5a08-49f6-8134-03083ed8ba30)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)
| Office 365 Small Business | LITEPACK  | bd09678e-b83c-4d3f-aaba-3dad4abd128b  | EXCHANGE_L_STANDARD (d42bdbd6-c335-4231-ab3d-c8f348d5aff5)<br/>MCOLITE (70710b6b-3ab4-4a38-9f6d-9f169461650a)<br/>SHAREPOINTLITE (a1f3d0a8-84c0-4ae0-bae4-685917b8ab48)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)
| Office 365 Small Business Premium | LITEPACK_P2   | fc14ec4a-4169-49a4-a51e-2c852931814b  | EXCHANGE_L_STANDARD (d42bdbd6-c335-4231-ab3d-c8f348d5aff5)<br/>MCOLITE (70710b6b-3ab4-4a38-9f6d-9f169461650a)<br/>OFFICE_PRO_PLUS_SUBSCRIPTION_SMBIZ (8ca59559-e2ca-470b-b7dd-afd8c0dee963)<br/>SHAREPOINTLITE (a1f3d0a8-84c0-4ae0-bae4-685917b8ab48)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)
| Onedrive for Business (Plan 1)    | WACONEDRIVESTANDARD   | e6778190-713e-4e4f-9119-8b8238de25df  | FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>ONEDRIVESTANDARD (13696edf-5a08-49f6-8134-03083ed8ba30)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)
| Onedrive for Business (Plan 2)    | WACONEDRIVEENTERPRISE | ed01faf2-1d88-4947-ae91-45ca18703a96  | ONEDRIVEENTERPRISE (afcafa6a-d966-4462-918c-ec0b4e0fe642)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)
| Power BI for Office 365 Add-On    | POWER_BI_ADDON    | 45bc2c81-6072-436a-9b0b-3b12eefbc402  | BI_AZURE_P1 (2125cfd7-2110-4567-83c4-c1cd5275163d)<br/>SQL_IS_SSIM (fc0a60aa-feee-4746-a0e3-aecfe81a38dd)
| Power BI Pro  | POWER_BI_PRO  | f8a1db68-be16-40ed-86d5-cb42ce701560  | BI_AZURE_P2 (70d33638-9c74-4d01-bfd3-562de28bd4ba)
| Project for Office 365    | PROJECTCLIENT | a10d5e58-74da-4312-95c8-76be4e5b75a0  | PROJECT_CLIENT_SUBSCRIPTION (fafd7243-e5c1-4a3a-9e40-495efcb1d3c3)
| Project Online Essentials | PROJECTESSENTIALS | 776df282-9fc0-4862-99e2-70e561b9909e  | FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>PROJECT_ESSENTIALS (1259157c-8581-4875-bca7-2ffb18c51bda)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)
| Project Online Premium    | PROJECTPREMIUM    | 09015f9f-377f-4538-bbb5-f75ceb09358a  | PROJECT_CLIENT_SUBSCRIPTION (fafd7243-e5c1-4a3a-9e40-495efcb1d3c3)<br/>SHAREPOINT_PROJECT (fe71d6c3-a2ea-4499-9778-da042bf08063)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)
| Project Online Premium without Project Client | PROJECTONLINE_PLAN_1  | 2db84718-652c-47a7-860c-f10d8abbdae3  | FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>SHAREPOINT_PROJECT (fe71d6c3-a2ea-4499-9778-da042bf08063)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)
| Project Online Professional   | PROJECTPROFESSIONAL   | 53818b1b-4a27-454b-8896-0dba576410e6  | PROJECT_CLIENT_SUBSCRIPTION (fafd7243-e5c1-4a3a-9e40-495efcb1d3c3)<br/>SHAREPOINT_PROJECT (fe71d6c3-a2ea-4499-9778-da042bf08063)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)
| Project Online with Project for Office 365    | PROJECTONLINE_PLAN_2  | f82a60b8-1ee3-4cfb-a4fe-1c6a53c2656c  | FORMS_PLAN_E1 (159f4cd6-e380-449f-a816-af1a9ef76344)<br/>PROJECT_CLIENT_SUBSCRIPTION (fafd7243-e5c1-4a3a-9e40-495efcb1d3c3)<br/>SHAREPOINT_PROJECT (fe71d6c3-a2ea-4499-9778-da042bf08063)<br/>SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)<br/>SHAREPOINTWAC (e95bec33-7c88-4a70-8e19-b10bd9d0c014)<br/>SWAY (a23b959c-7ce8-4e57-9140-b90eb88a9e97)
| Sharepoint Online (Plan 1)    | SHAREPOINTSTANDARD    | 1fc08a02-8b3d-43b9-831e-f76859e04e1a  | SHAREPOINTSTANDARD (c7699d2e-19aa-44de-8edf-1736da088ca1)
| Sharepoint Online (Plan 2)    | SHAREPOINTENTERPRISE  | a9732ec9-17d9-494c-a51c-d6b45b384dcb  | SHAREPOINTENTERPRISE (5dbe027f-2339-4123-9542-606e4d348a72)
| Skype for Business Cloud PBX  | MCOEV | e43b5b99-8dfb-405f-9987-dc307f34bcbd  | MCOEV (4828c8ec-dc2e-4779-b502-87ac9ce28ab7)
| Skype for Business Online (Plan 1)    | MCOIMP    | b8b749f8-a4ef-4887-9539-c95b1eaa5db7  | MCOIMP (afc06cb0-b4f4-4473-8286-d644f70d8faf)
| Skype for Business Online (Plan 2)    | MCOSTANDARD   | d42c793f-6c78-4f43-92ca-e8f6a02b035f  | MCOSTANDARD (0feaeb32-d00e-4d66-bd5a-43b5b83db82c)
| Skype for Business PSTN Conferencing  | MCOMEETADV    | 0c266dff-15dd-4b49-8397-2bb16070ed52  | MCOMEETADV (3e26ee1f-8a5f-4d52-aee2-b81ce45c8f40)
| Skype FOR Business PSTN Domestic and International Calling    | MCOPSTN2  | d3b4fe1f-9992-4930-8acb-ca6ec609365e  | MCOPSTN2 (5a10155d-f5c1-411a-a8ec-e99aae125390)
| Skype for Business PSTN Domestic Calling  | MCOPSTN1  | 0dab259f-bf13-4952-b7f8-7db8f131b28d  | MCOPSTN1 (4ed3ff63-69d7-4fb7-b984-5aec7f605ca8)
| Visio Pro for Office 365  | VISIOCLIENT   | c5928f49-12ba-48f7-ada3-0d743a3601d5  | VISIO_CLIENT_SUBSCRIPTION (663a804f-1c30-4ff0-9915-9db84f0d1cea)
| Windows 10 Enterprise E3  | WIN10_PRO_ENT_SUB | cb10e6cd-9da4-4992-867b-67546b1db821  | WIN10_PRO_ENT_SUB (21b439ba-a0ca-424f-a6cc-52f954a5b111)

## <a name="service-plans-that-cannot-be-assigned-at-the-same-time"></a>Планы службы, которые нельзя назначить одновременно

Некоторые продукты содержат планы службы, которые невозможно назначить одному и тому же пользователю в одно и то же время. Например, если у вас есть *Office 365 корпоративный E1* и *Office 365 корпоративный E3* в клиенте и вы попытаетесь назначить обе лицензии одному пользователю, эта операция завершится сбоем. Это обусловлено тем, что продукт E3 содержит следующие планы службы, конфликтующие со своими аналогами E1:

-   SharePoint Online (план 2) конфликтует с SharePoint Online (план 1);
-   Exchange Online (план 2) конфликтует с Exchange Online (план 1).

При использовании лицензирования на основе группы вы столкнетесь с [конфликтующими планами службы](active-directory-licensing-group-problem-resolution-azure-portal.md#conflicting-service-plans). При использовании PowerShell появится ошибка *MutuallyExclusiveViolation*.

В этом разделе перечислены наиболее распространенные планы служб, которые являются взаимоисключающими, сгруппированные по типу службы. Эти сведения можно использовать для планирования развертывания лицензии и избежания ошибок назначения.

### <a name="service-azure-active-directory"></a>Служба: *Azure Active Directory*

>[!NOTE]
>Все планы службы, связанные с Azure Active Directory, теперь можно совместно назначить одному пользователю. Это упрощает определенные сценарии управления лицензиями, например перемещение пользователей из Azure AD Basic в Azure AD Premium P1.

### <a name="service-dynamics-crm"></a>Служба: *Dynamics CRM*

Совместное назначение недоступно для следующих планов службы:

| Имя плана службы | GUID |
| --- | --- |
| CRMIUR    | c42a56bd-9e70-4ace-be17-dc8eeae369d7 |
| CRMPLAN1  | 119cf168-b6cf-41fb-b82e-7fee7bae5814 |
| CRMPLAN2  | bf36ca64-95c6-4918-9275-eb9f4ce2c04f |
| CRMSTANDARD   | f9646fb2-e3b2-4309-95de-dc4833737456 |
| DYN365_ENTERPRISE_P1  | d56f3deb-50d8-465a-bedb-f079817ccac1 |
| DYN365_ENTERPRISE_P1_IW   | 056a5f80-b4e0-4983-a8be-7ad254a113c9 |
| DYN365_ENTERPRISE_SALES   | 2da8e897-7791-486b-b08f-cc63c8129df7 |
| DYN365_ENTERPRISE_TEAM_MEMBERS    | 6a54b05e-4fab-40e7-9828-428db3b336fa |
| EMPLOYEE_SELF_SERVICE | ba5f0cfa-d54a-4ea0-8cf4-a7e1dc4423d8 |

### <a name="service-exchange-online"></a>Служба: *Exchange Online*

Совместное назначение недоступно для следующих планов службы:

| Имя плана службы | GUID |
| --- | --- |
| EXCHANGE_B_STANDARD   | 90927877-dcff-4af6-b346-2332c0b15bb7 |
| EXCHANGE_L_STANDARD   | d42bdbd6-c335-4231-ab3d-c8f348d5aff5 |
| EXCHANGE_S_ARCHIVE    | da040e0a-b393-4bea-bb76-928b3fa1cf5a |
| EXCHANGE_S_DESKLESS   | 4a82b400-a79f-41a4-b4e2-e94f5787b113 |
| EXCHANGE_S_ENTERPRISE | efb87545-963c-4e0d-99df-69c6916d9eb0 |
| EXCHANGE_S_ESSENTIALS | 1126bef5-da20-4f07-b45e-ad25d2581aa8 |
| EXCHANGE_S_STANDARD   | 9aaf7827-d63c-4b61-89c3-182f06f82e5c |
| EXCHANGE_S_STANDARD_MIDMARKET | fc52cc4b-ed7d-472d-bbe7-b081c23ecc56 |

### <a name="service-intune"></a>Служба: *Intune*

Совместное назначение недоступно для следующих планов службы:

| Имя плана службы | GUID |
| --- | --- |
| INTUNE_A  | c1ec4a95-1f05-45b3-a911-aa3fa01094f5 |
| INTUNE_A_VL   | 3e170737-c728-4eae-bbb9-3f3360f7184c |
| INTUNE_B  | 2dc63b8a-df3d-448f-b683-8655877c9360 |

### <a name="service-sharepoint-online"></a>Служба: *SharePoint Online*

Совместное назначение недоступно для следующих планов службы:

| Имя плана службы | GUID |
| --- | --- |
| ONEDRIVEENTERPRISE    | afcafa6a-d966-4462-918c-ec0b4e0fe642 |
| SHAREPOINT_S_DEVELOPER    | a361d6e2-509e-4e25-a8ad-950060064ef4 |
| SHAREPOINTDESKLESS    | 902b47e5-dcb2-4fdc-858b-c63a90a2bdb9 |
| SHAREPOINTENTERPRISE  | 5dbe027f-2339-4123-9542-606e4d348a72 |
| SHAREPOINTENTERPRISE_EDU  | 63038b2c-28d0-45f6-bc36-33062963b498 |
| SHAREPOINTENTERPRISE_MIDMARKET    | 6b5b6a67-fc72-4a1f-a2b5-beecf05de761 |
| SHAREPOINTLITE    | a1f3d0a8-84c0-4ae0-bae4-685917b8ab48 |
| SHAREPOINTSTANDARD    | c7699d2e-19aa-44de-8edf-1736da088ca1 |
| SHAREPOINTSTANDARD_EDU    | 0a4983bb-d3e5-4a09-95d8-b2d0127b3df5 |

### <a name="service-skype-for-business"></a>Служба: *Skype для бизнеса*

Совместное назначение недоступно для следующих планов службы:

| Имя плана службы | GUID |
| --- | --- |
| MCOIMP    | afc06cb0-b4f4-4473-8286-d644f70d8faf |
| MCOSTANDARD_MIDMARKET | b2669e95-76ef-4e7e-a367-002f60a39f3e |
| MCOSTANDARD   | 0feaeb32-d00e-4d66-bd5a-43b5b83db82c |
| MCOLITE   | 70710b6b-3ab4-4a38-9f6d-9f169461650a |

Совместное назначение недоступно для следующих планов службы:

| Имя плана службы | GUID |
| --- | --- |
| MCOPSTN1  | 4ed3ff63-69d7-4fb7-b984-5aec7f605ca8 |
| MCOPSTN2  | 5a10155d-f5c1-411a-a8ec-e99aae125390 |

### <a name="service-yammer"></a>Служба: *Yammer*

Совместное назначение недоступно для следующих планов службы:

| Имя плана службы | GUID |
| --- | --- |
| YAMMER_ENTERPRISE | 7547a3fe-08ee-4ccb-b430-5077c5041653 |
| YAMMER_EDU    | 2078e8df-cff6-4290-98cb-5408261a760a |
| YAMMER_MIDSIZE    | 41bf139a-4e60-409f-9346-a1361efc6dfb |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о наборе функций для управления лицензиями с помощью групп см. по ссылкам ниже.

* [Примеры PowerShell для группового лицензирования в Azure AD](active-directory-licensing-ps-examples.md)
