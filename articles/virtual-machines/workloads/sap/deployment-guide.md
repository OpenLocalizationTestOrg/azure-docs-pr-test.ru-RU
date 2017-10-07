---
title: "Развертывание виртуальных машин для SAP NetWeaver aaaAzure | Документы Microsoft"
description: "Узнайте, как SAP toodeploy программное обеспечение на виртуальных машинах Linux в Azure."
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 1c4f1951-3613-4a5a-a0af-36b85750c84e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.openlocfilehash: 42f1d8a3eff51e113729dbfe2848b67deaf06936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-deployment-for-sap-netweaver"></a>Развертывание виртуальных машин Azure для SAP NetWeaver
[767598]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1139904]:https://launchpad.support.sap.com/#/notes/1139904
[1173395]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958]:https://launchpad.support.sap.com/#/notes/1558958
[1585981]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258]:https://launchpad.support.sap.com/#/notes/1814258
[1882376]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[2367194]:https://launchpad.support.sap.com/#/notes/2367194

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

[dbms-guide]:dbms-guide.md (Azure Virtual Machines DBMS deployment for SAP)
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Caching for VMs and VHDs)
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID)
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure Storage)
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Structure of a RDBMS deployment)
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (High availability and disaster recovery with Azure VMs)
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 (SQL Server 2012 SP1 CU4 and later)
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 and earlier releases)
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (Using a SQL Server image from hello Azure Marketplace)
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (General SQL Server for SAP on Azure summary)
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Specifics tooSQL Server RDBMS)
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Storage configuration)
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Backup and restore)
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Performance considerations for backup and restore)
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (Other)
[dbms-guide-900-sap-cache-server-on-premises]:dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[deployment-guide]:deployment-guide.md (Azure Virtual Machines deployment for SAP)
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP resources)
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab (Deploying a VM by using a custom image)
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 (Scenario 1: Deploying a VM from hello Azure Marketplace for SAP)
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Scenario 2: Deploying a VM with a custom image for SAP)
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1 (Scenario 3: Moving a VM from on-premises using a non-generalized Azure VHD with SAP)
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e (Deployment scenarios of VMs for SAP on Microsoft Azure)
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Deploying Azure PowerShell cmdlets)
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (Download and import SAP-relevant PowerShell cmdlets)
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (Join a VM tooan on-premises domain - Windows only)
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux)
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (Download, install, and enable hello Azure VM Agent)
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell)
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI)
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Configure hello Azure Enhanced Monitoring Extension for SAP)
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness check for Azure Enhanced Monitoring for SAP)
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (Health check for hello Azure monitoring infrastructure)
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (Troubleshooting Azure monitoring for SAP)

[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure monitoring)
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d (Configure hello proxy)
[deployment-guide-figure-100]:media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:deployment-guide.md#figure-11
[deployment-guide-figure-1100]:media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:deployment-guide.md#figure-14
[deployment-guide-figure-1400]:media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:deployment-guide.md#figure-5
[deployment-guide-figure-50]:media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:deployment-guide.md#figure-6
[deployment-guide-figure-600]:media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:deployment-guide.md#figure-7
[deployment-guide-figure-700]:media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b (Checks and troubleshooting for setting up end-to-end monitoring)

[deploy-template-cli]:../../../resource-group-template-deploy-cli.md
[deploy-template-portal]:../../../resource-group-template-deploy-portal.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:../../virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:../../virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:../../virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:../../virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:../../virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:../../virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md (Azure Virtual Machines planning and implementation for SAP)
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Resources)
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High availability and disaster recovery for SAP NetWeaver running on Azure Virtual Machines)
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (High availability for SAP Application Servers)
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (Using Autostart for SAP instances)
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 (Cloud-only - Virtual Machine deployments in Azure without dependencies on hello on-premises customer network)
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross-premises - Deployment of single or multiple SAP VMs in Azure fully integrated with hello on-premises network)
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure regions)
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fault domains)
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Upgrade domains)
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665 (Azure availability sets)
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (Microsoft Azure virtual machines concept)
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Deploying a VM with a customer specific image)
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Preparation for moving a VM from on-premises tooAzure with a non-generalized disk)
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Preparation for deploying a VM with a customer specific image for SAP)
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Preparing VMs with SAP for Azure)
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Difference between an Azure disk and an Azure image)
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (Uploading a VHD from on-premises tooAzure)
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Copying disks between Azure Storage accounts)
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 (VM/VHD structure for SAP deployments)
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Setting automount for attached disks)
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (Single VM with SAP NetWeaver demo/training scenario)
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Concepts of Cloud-Only deployment of SAP instances)
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Monitoring Solution for SAP)
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Storage)
[planning-guide-managed-disks]:planning-guide.md#c55b2c6e-3ca1-4476-be16-16c81927550f (Managed Disks)
[planning-guide-figure-100]:media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and data disks)

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-os-disk-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk-md%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-2-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image-md%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-md%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image-md%2Fazuredeploy.json
[storage-azure-cli]:../../../storage/common/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../../../storage/common/storage-azure-cli.md#copy-blobs
[storage-introduction]:../../../storage/common/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../../../storage/common/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../../../storage/common/storage-premium-storage.md
[storage-redundancy]:../../../storage/common/storage-redundancy.md
[storage-scalability-targets]:../../../storage/common/storage-scalability-targets.md
[storage-use-azcopy]:../../../storage/common/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:../../linux/attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../../../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md (Manage virtual machines by using Azure Resource Manager and PowerShell)
[virtual-machines-windows-agent-user-guide]:../../windows/agent-user-guide.md
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:../../virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:../../linux/sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:./../../windows/sqlclassic/virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:./../../windows/sql/virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:./../../windows/sql/virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:./../../windows/sql/virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:../../virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:../../virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../../../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../../../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../../../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../../../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../../../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../../../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../../../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../../../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../../../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../../../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../../../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../../../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../../../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../../../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../../../cli-install-nodejs.md
[xplat-cli-azure-resource-manager]:../../../xplat-cli-azure-resource-manager.md

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Виртуальные машины Azure является hello решением для организаций, которым требуются вычислительные ресурсы и хранилища, минимальное время и без длительных процессов поставки. Можно использовать виртуальные машины Azure toodeploy Классические приложения, такие как приложений на основе SAP NetWeaver в Azure. и повысить уровень их надежности и доступности, не привлекая дополнительные локальные ресурсы. Виртуальные машины Azure поддерживают распределенные подключения. Это позволяет интегрировать их в локальные домены, частные облака и системный ландшафт SAP вашей организации.

В этой статье мы рассмотрим приложения hello действия toodeploy SAP на виртуальных машинах (ВМ) в Azure, включая параметры альтернативного развертывания и устранения неполадок. Эта статья основана на информации hello в [виртуальных машинах Azure планированию и реализации для SAP NetWeaver][planning-guide]. Она также дополняет документацию по установке SAP и примечания по SAP, которые являются основными ресурсами hello по установке и развертыванию программного обеспечения SAP.

## <a name="prerequisites"></a>Предварительные требования
Настройка виртуальной машины Azure перед развертыванием ПО SAP состоит из нескольких этапов и предполагает наличие определенных ресурсов. Прежде чем начать, убедитесь в соблюдении hello предварительные требования для установки программного обеспечения SAP на виртуальных машинах в Azure.

### <a name="local-computer"></a>Локальный компьютер
toomanage Windows или виртуальных машин Linux, можно использовать сценарий PowerShell и hello портал Azure. В обоих случаях вам потребуется локальный компьютер под управлением Windows 7 или более поздней версии. Если требуется toomanage только виртуальные машины Linux и требуется toouse компьютер Linux для этой задачи можно использовать Azure CLI.

### <a name="internet-connection"></a>Подключение к Интернету
toodownload и выполнения hello средства и сценарии, необходимые для развертывания программного обеспечения SAP, должен быть подключен toohello Интернета. Hello виртуальной Машине Azure, на котором выполняется hello расширение мониторинга Azure для SAP необходимо также toohello доступа к Интернету. Если hello виртуальной Машины Azure входит в состав виртуальной сети Azure или локального домена, убедитесь, что заданы hello соответствующие параметры прокси, как описано в [настройки прокси-сервера hello][deployment-guide-configure-proxy].

### <a name="microsoft-azure-subscription"></a>Подписка на Microsoft Azure
Вам потребуется активная учетная запись Azure.

### <a name="topology-and-networking"></a>Топология и сеть
Необходимые toodefine hello топология и архитектура hello развертывания SAP в Azure.

* Toobe учетных записей хранилища Azure используется
* Место системы SAP hello toodeploy виртуальной сети
* Система SAP hello toodeploy toowhich группы ресурсов
* Регион Azure, место системы SAP toodeploy hello
* конфигурация SAP (двух- или трехуровневая);
* Размеры виртуальных Машин и hello количество дисков toobe дополнительные данные, установленными toohello виртуальные машины
* конфигурация системы исправлений и транспортировки SAP.

Создание и настройка учетных записей хранилища Azure (при необходимости) или виртуальные сети Azure, перед началом процесса развертывания программных продуктов SAP hello. Сведения о том, как toocreate и настроить эти ресурсы см. в разделе [виртуальных машинах Azure планированию и реализации для SAP NetWeaver][planning-guide].

### <a name="sap-sizing"></a>Определение размера системы SAP
Знаете hello следующую информацию для изменения размеров SAP:

* Прогнозировать нагрузка SAP, например, с помощью hello, быстрый SAP размер символов, инструмент и hello SAP приложения производительности Standard (число SAPS.)
* Необходимых ресурсов и памяти ЦП системы SAP hello
* требуемое число операций ввода-вывода в секунду;
* требуемая пропускная способность сети при дальнейшем обмене данными между разными виртуальными машинами в Azure;
* Необходимая пропускная способность сети между локальной средств и hello системы SAP, развернутых в Azure

### <a name="resource-groups"></a>Группы ресурсов
В диспетчере ресурсов Azure можно использовать toomanage группы ресурсов все ресурсы приложения hello в вашей подписке Azure. Дополнительные сведения см. в [обзоре Azure Resource Manager][resource-group-overview].

## <a name="resources"></a>Ресурсы

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Ресурсы SAP
При настройке развертывания программного обеспечения SAP, необходимы следующие ресурсы SAP hello.

* примечание к SAP [1928533], которое содержит:
  * Список размеров виртуальных Машин Azure, которые поддерживаются для развертывания по SAP hello
  * важные сведения о доступных ресурсах для каждого размера виртуальной машины Azure;
  * сведения о поддерживаемом программном обеспечении SAP и сочетаниях операционных систем и баз данных;
  * сведения о требуемой версии ядра SAP для Windows и Linux в Microsoft Azure.

* примечание к SAP [2015553], в котором описываются предварительные требования к SAP при развертывании программного обеспечения SAP в Azure;
* примечание к SAP [2178632], содержащее подробные сведения обо всех доступных метриках мониторинга для SAP в Azure;
* Примечание SAP [1409604] hello требуемое версия агента узла SAP для Windows в Azure.
* Примечание SAP [2191498] имеет hello требуемая версия агента узла SAP для Linux в Azure.
* примечание к SAP [2243692], содержащее сведения о лицензировании SAP в Linux в Azure;
* примечание к SAP [1984787], содержащее общие сведения о SUSE Linux Enterprise Server 12;
* примечание к SAP [2002167], содержащее общие сведения о Red Hat Enterprise Linux 7.x;
* примечание к SAP [2069760], содержащее общие сведения об Oracle Linux 7.x;
* Примечание SAP [1999351] имеет дополнительные диагностические сведения для hello расширение мониторинга Azure для SAP.
* примечание к SAP [1597355], содержащее общие сведения об области буфера для Linux;
* на [странице SCN SAP в Azure](https://wiki.scn.sap.com/wiki/x/Pia7Gg) есть новости и коллекция полезных ресурсов;
* [вики-сайт сообщества SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes), содержащий все необходимые примечания к SAP для Linux;
* командлеты PowerShell для SAP, которые являются частью [Azure PowerShell][azure-ps];
* команды интерфейса командной строки Azure для SAP, который является частью [Azure CLI][azure-cli];

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>Ресурсы Windows
Дополнительные сведения о развертывании SAP в Azure см. в следующих статьях:

* [SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]
* [Развертывание виртуальных машин Azure для SAP NetWeaver (эта статья)][deployment-guide]
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Сценарии развертывания ПО SAP на виртуальных машинах Azure
Виртуальные машины и связанные диски можно развернуть в Azure несколькими способами. Это важные toounderstand hello различия между варианты развертывания, поскольку tooprepare различные действия может занять виртуальных машин для развертывания в зависимости от выбранного типа развертывания hello.

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Сценарий 1: Развертывание ВМ из hello Azure Marketplace для SAP
Можно использовать образа, предоставленного корпорацией Майкрософт или посторонним в Azure Marketplace toodeploy hello ВМ. Hello Marketplace предлагает несколько стандартных образов ОС Windows Server и различные дистрибутивы Linux. Вы также можете развернуть образ, содержащий номера SKU СУБД, например Microsoft SQL Server. Дополнительные сведения об использовании образов с номерами SKU СУБД см. в статье [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide].

Hello приведенной ниже схеме показано hello последовательность SAP определенного действия для развертывания виртуальной Машины из hello Azure Marketplace:

![Блок-схема развертывания ВМ для систем SAP с помощью образа виртуальной Машины из hello Azure Marketplace][deployment-guide-figure-100]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Создание виртуальной машины с помощью портала Azure hello
Hello простым способом toocreate новую виртуальную машину с изображением из hello Azure Marketplace можно с помощью портала Azure hello.

1.  Go слишком<https://portal.azure.com/#create/hub>.  Или в hello Azure меню портала, выберите **+ создать**.
2.  Выберите **вычислений**, а затем выберите тип операционной системы требуется toodeploy hello. Например, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2) или Oracle Linux 7.2. представление списка по умолчанию Hello не показывает, что для всех поддерживаемых операционных систем. Выберите **Показать все**, чтобы просмотреть полный список. Дополнительные сведения о поддерживаемых операционных системах для развертывания ПО SAP см. в примечании к SAP [1928533].
3.  На следующей странице hello просмотрите условия.
4.  В hello **выберите модель развертывания** выберите **диспетчера ресурсов**.
5.  Нажмите кнопку **Создать**.

Hello мастер поможет установить hello необходимые параметры toocreate hello виртуальной машины, кроме tooall необходимые ресурсы, такие как сетевые интерфейсы и учетные записи хранения. Ниже приведены некоторые из этих параметров.

1. **Основные сведения**:
 * **Имя**: hello имя ресурса hello (имя виртуальной машины hello).
 * **Тип диска виртуальной Машины**: выберите тип диска hello hello ОС диска. Если требуется toouse хранилище Premium для дисков данных, рекомендуется использовать хранилище Premium для hello диск ОС, а также.
 * **Имя пользователя и пароль** или **открытый ключ SSH**: Введите hello пользователя и пароль пользователя hello, которая создается во время инициализации hello. Для виртуальной машины Linux можно ввести hello использовать toosign toohello машине открытого ключа Secure Shell (SSH).
 * **Подписки**: выберите подписку hello, что требуется toouse tooprovision hello новой виртуальной машины.
 * **Группа ресурсов**: hello имя группы ресурсов hello hello виртуальной Машины. Можно ввести либо имя hello новое имя группы ресурсов или hello группы ресурсов, который уже существует.
 * **Расположение**: где toodeploy hello новой виртуальной машины. Если вы хотите tooconnect hello виртуальной машины tooyour локальную сеть, убедитесь, что выберите расположение hello hello виртуальной сети, соединяющей Azure tooyour в локальную сеть. Дополнительные сведения см. в разделе [Сеть Microsoft Azure][planning-guide-microsoft-azure-networking] [руководства по планированию и внедрению SAP NetWeaver на виртуальных машинах][planning-guide].
2. **Размер**:

     Список поддерживаемых типов виртуальных машин см. в примечании к SAP [1928533]. Убедитесь, что вы выберите правильный тип виртуальной Машины hello toouse хранилища Azure Premium. Не все типы виртуальных машин поддерживают хранилище класса Premium. Дополнительные сведения см. в разделе [Хранилище. Служба хранилища Microsoft Azure и диски данных][planning-guide-storage-microsoft-azure-storage-and-data-disks] и [Хранилище Azure класса Premium][planning-guide-azure-premium-storage] [руководства по планированию и внедрению SAP NetWeaver на виртуальных машинах][planning-guide].

3. **Параметры**:
  * **Хранилище**
    * **Тип диска**: выберите тип диска hello hello ОС диска. Если требуется toouse хранилище Premium для дисков данных, рекомендуется использовать хранилище Premium для hello диск ОС, а также.
    * **Использование управляемых дисков**: следует toouse управляемых дисков выберите "Да". Дополнительные сведения о дисках управляемых см. в разделе [управляемых дисков] [ planning-guide-managed-disks] в руководстве по планированию hello.
    * **Учетная запись хранения.** Создайте учетную запись хранения или выберите имеющуюся. Запуск приложений SAP поддерживают не все типы хранилищ. Дополнительные сведения о типах хранилищ см. в разделе [Служба хранилища Microsoft Azure][dbms-guide-2.3] в статье [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide].
  * **Сеть**
    * **Виртуальная сеть** и **подсети**: toointegrate hello виртуальную машину с интрасетью, выберите hello виртуальной сети, подключенной tooyour локальной сети.
    * **Общедоступный IP-адрес**: выберите hello общедоступный IP-адрес, должны быть toouse или введите параметры toocreate новый общедоступный IP-адрес. Можно использовать открытые tooaccess адрес IP к виртуальной машине через Интернет hello. Убедитесь, что также создать сетевой безопасности группы toohelp безопасного доступа tooyour виртуальную машину.
    * **Группа безопасности сети.** Дополнительные сведения см. в статье [Управление потоком сетевого трафика с помощью групп безопасности сети][virtual-networks-nsg].
  * **Расширения**: можно установить расширения виртуальной машины, добавив их toohello развертывания. Расширения tooadd на этом шаге не обязательно. Hello расширения, необходимые для поддержки SAP устанавливаются позже. В разделе [hello Настройка расширения улучшенного мониторинга Azure для SAP] [ deployment-guide-4.5] в данном руководстве.
  * **Высокий уровень доступности**: группа доступности выберите или введите параметры hello toocreate наличие новых значение. Дополнительные сведения см. в разделе [Группы доступности Azure][planning-guide-3.2.3].
  * **Мониторинг**
    * **Диагностика загрузки.** Диагностику загрузки можно **отключить**.
    * **Диагностика гостевой ОС.** Диагностику мониторинга можно **отключить**.

4. **Сводка**:

  Просмотрите выбранные параметры и нажмите кнопку **ОК**.

Виртуальная машина развернута в выбранной группы ресурсов hello.

#### <a name="create-a-virtual-machine-by-using-a-template"></a>Создание виртуальной машины с помощью шаблона
Можно создать виртуальную машину с помощью одного из шаблонов hello SAP, опубликованных в hello [репозитории GitHub azure — начало работы — шаблоны][azure-quickstart-templates-github]. Также можно вручную создать виртуальную машину с помощью hello [портал Azure][virtual-machines-windows-tutorial], [PowerShell][virtual-machines-ps-create-preconfigure-windows-resource-manager-vms], или [Azure CLI ][virtual-machines-linux-tutorial].

* [**Шаблон двухуровневой конфигурации (только одна виртуальная машина)** (sap-2-tier-marketplace-image)][sap-templates-2-tier-marketplace-image].

  Этот шаблон используется toocreate двухуровневую систему, используя только одна виртуальная машина.
* [**Шаблон двухуровневой конфигурации (только одна виртуальная машина) с управляемыми дисками** (sap-2-tier-marketplace-image-md)][sap-templates-2-tier-marketplace-image-md].

  toocreate двухуровневую систему с использованием только одной виртуальной машины и диски, управляемые, используйте этот шаблон.
* [**Шаблон трехуровневой конфигурации (несколько виртуальных машин)** (sap-3-tier-marketplace-image)][sap-templates-3-tier-marketplace-image].

  Этот шаблон используется toocreate трехуровневые системы с помощью нескольких виртуальных машин.
* [**Шаблон трехуровневой конфигурации (несколько виртуальных машин) с управляемыми дисками** (sap-3-tier-marketplace-image-md)][sap-templates-3-tier-marketplace-image-md].

  toocreate трехуровневые системы с помощью нескольких виртуальных машин и управляемых дисков, используйте этот шаблон.

Введите следующие параметры для шаблона hello hello в hello портала Azure:

1. **Основные сведения**:
  * **Подписки**: hello подписки toouse toodeploy hello шаблона.
  * **Группа ресурсов**: hello шаблон toodeploy toouse hello ресурсов группы. Можно создать новую группу ресурсов, или можно выбрать существующую группу ресурсов в подписке hello.
  * **Расположение**: где toodeploy hello шаблона. Если вы выбрали существующую группу ресурсов, используется hello расположение группы ресурсов.

2. **Параметры**:
  * **Идентификатор системы SAP**: hello идентификатор системы SAP (SID).
  * **Тип ОС**: hello операционной системы требуется toodeploy, например, Windows Server 2012 R2, SUSE Linux Enterprise Server 12 (SLES 12), Red Hat Enterprise Linux 7.2 (RHEL 7.2) или Oracle Linux 7.2.

    представление списка Hello не отображается, что для всех поддерживаемых операционных систем. Дополнительные сведения о поддерживаемых операционных системах для развертывания ПО SAP см. в примечании к SAP [1928533].
  * **Размер системы SAP**: hello размер hello системы SAP.

    предоставляет Hello число SAPS hello новую систему. Если вы не уверены, сколько SAPS hello система требует, обратитесь к партнеру технологии SAP или системные интеграторы.
  * **Доступность системы** (только шаблон трехуровневого): hello доступность системы.

    Выберите **высокую доступность** в качестве конфигурации, которая подходит для установки высокого уровня доступности. Будут созданы два сервера баз данных и два сервера для ABAP SAP Central Services (ASCS).
  * **Тип хранилища** (только шаблон двухуровневая): hello тип toouse хранилища.

    В системах большого размера мы настоятельно рекомендуем использовать хранилище Azure класса Premium. Дополнительные сведения о типах хранилищ см. в следующих ресурсах:
      * [Использование хранилища SSD класса Premium Azure для экземпляра СУБД SAP][2367194]
      * [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide] (раздел [Служба хранилища Microsoft Azure][dbms-guide-2.3]).
      * [Хранилище класса Premium: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure][storage-premium-storage-preview-portal]
      * [Введение tooMicrosoft хранилища Azure][storage-introduction]
  * **Имя администратора** и **Пароль администратора.** Имя пользователя и пароль.
    Создается новый пользователь, для входа в toohello виртуальной машины.
  * **New or existing subnet** (Новая или имеющаяся подсеть). Определяет, следует ли создать виртуальную сеть и подсеть или использовать имеющуюся подсеть. При наличии виртуальной сети, подключенной tooyour локальную сеть, выберите **существующие**.
  * **Идентификатор подсети**: hello идентификатор hello подсети hello виртуальные машины будут подключаться. Выберите подсеть hello виртуальной частной сети (VPN) или виртуальной сети Azure ExpressRoute toouse tooconnect hello виртуальной машины tooyour локальной сети. Идентификатор Hello обычно выглядит следующим образом: /subscriptions/&lt;идентификатор подписки > /resourceGroups/&lt;имя группы ресурсов > /providers/Microsoft.Network/virtualNetworks/&lt;имя виртуальной сети > /subnets/&lt;имя подсети >

3. **Условия использования:**  
    Просмотрите и примите условия использования hello.

4.  Щелкните **Приобрести**.

Hello агент ВМ разворачивается по умолчанию при использовании образа с hello Azure Marketplace.

#### <a name="configure-proxy-settings"></a>Настройка параметров прокси
В зависимости от конфигурации локальной сети может потребоваться tooset копирование hello прокси-сервера на виртуальной Машине. Если подключенных tooyour локальной сети через VPN или ExpressRoute ВМ, hello виртуальной Машины не может быть hello может tooaccess Интернета и не быть может toodownload hello необходимые расширения или сбора данных мониторинга. Дополнительные сведения см. в разделе [настройки прокси-сервера hello][deployment-guide-configure-proxy].

#### <a name="join-a-domain-windows-only"></a>Присоединение к домену (только для Windows)
Если развертывания Azure подключенных tooan в локальной среде Active Directory или DNS-экземпляр с помощью Azure VPN-подключения сеть сеть или ExpressRoute (это называется *между организациями* в [Планирование виртуальных машинах Azure и реализации для SAP NetWeaver][planning-guide]), предполагается, что hello виртуальной Машины присоединением к домену в локальной. Дополнительные сведения о вопросах для выполнения этой задачи см. в разделе [присоединения к домену tooan локальной виртуальной Машины (только Windows)][deployment-guide-4.3].

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Настройка мониторинга
Убедитесь, что SAP поддерживает среду, Настройка hello расширения мониторинга Azure для SAP, как описано в toobe [hello Настройка расширения улучшенного мониторинга Azure для SAP][deployment-guide-4.5]. Проверьте предварительные условия hello для мониторинга SAP и требуемых минимальных версий ядра SAP и агента узла SAP, в ресурсах hello, перечисленных в [ресурсы SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Проверка мониторинга
Проверьте, работает ли мониторинг, как описано в разделе [Проверки и устранение неполадок при комплексной настройке мониторинга][deployment-guide-troubleshooting-chapter].

#### <a name="post-deployment-steps"></a>Действия, выполняемые после развертывания
После создания развертывается hello виртуальной Машины и hello виртуальной Машины, необходимо, чтобы tooinstall hello необходимые программные компоненты в hello виртуальной Машины. Из-за hello программного развертывания и установки последовательности в этом типе развертывания виртуальной Машины toobe программного обеспечения hello установлен уже должен быть доступен, либо в Azure, на другой виртуальной Машиной, или как диск, который может быть присоединен. Также рассмотрите возможность предоставляется с помощью сценария между организациями, какие подключения toohello локальных ресурсов (Общие папки установки).

После развертывания ВМ в Azure, выполните hello же инструкций и инструментов и tooinstall hello программного обеспечения SAP в ВМ, как вы бы в локальной среде. tooinstall программного обеспечения SAP в ВМ Azure, как Майкрософт и SAP рекомендуют отправить и сохранить установочный носитель SAP hello на Azure виртуальных жестких дисков или дисков, управляемых, так и создания виртуальной Машины Azure, который работает как файловый сервер, имеющий hello все необходимые установочные носители SAP.

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Сценарий 2. Развертывание виртуальной машины для SAP с помощью пользовательского образа
Поскольку разные версии операционной системы или СУБД исправления с разными требованиями, hello изображения, которые можно найти в hello Azure Marketplace могут не удовлетворять вашим потребностям. Вместо этого вы можете toocreate виртуальной Машины с помощью своего собственного образа ОС или СУБД виртуальной Машины, его можно развернуть позже.
Используйте различные шаги toocreate частным образом для Linux чем toocreate, один для Windows.

- - -
> ![Windows][Logo_Windows] Windows
>
> tooprepare образа Windows, который можно использовать toodeploy нескольких виртуальных машин, параметры Windows hello (такие как идентификатор безопасности Windows и имя узла) должен быть абстрагированы или обобщить hello локальной виртуальной Машины. Можно использовать [sysprep](https://msdn.microsoft.com/library/hh825084.aspx) toodo это.
>
> ![Linux][Logo_Linux] Linux
>
> должно быть tooprepare образа можно использовать toodeploy нескольких виртуальных машин Linux, некоторые параметры Linux hello абстрактные или обобщенный на локальной виртуальной Машины. Можно использовать `waagent -deprovision` toodo это. Дополнительные сведения см. в разделе [образа виртуальной машины Linux в Azure] [ virtual-machines-linux-capture-image] и hello [руководство пользователя агента Azure Linux][virtual-machines-linux-agent-user-guide-command-line-options].
>
>

- - -
Можно подготовить и создать пользовательский образ и затем использовать его toocreate несколько новых виртуальных машин. Дополнительные сведения см. в [руководстве по планированию и внедрению SAP NetWeaver на виртуальных машинах][planning-guide]. Настройка базы данных содержимого, либо с помощью диспетчера подготовки программного обеспечения SAP tooinstall новой системы SAP (восстанавливает резервную копию базы данных с диска, присоединенные toohello виртуальная машина) или при помощи восстановления резервной копии базы данных хранилища Azure, напрямую используемой СУБД поддерживает его. Дополнительные сведения см. в [руководстве по развертыванию СУБД][dbms-guide]. Если вы уже установили системы SAP на локальной ВМ (особенно для двухуровневой систем), вы можете адаптировать параметры системы SAP hello после развертывания hello hello ВМ Azure с помощью процедуры переименования системы hello, поддерживаемых SAP подготовки программного обеспечения Диспетчер (Примечание SAP [1619720]). В противном случае можно установить по SAP hello после развертывания виртуальной Машины Azure hello.

Hello приведенной ниже схеме показано hello последовательность SAP определенного действия для развертывания виртуальной Машины с помощью пользовательского образа:

![Блок-схема развертывания виртуальной машины для систем SAP с помощью образа виртуальной машины в частном Marketplace][deployment-guide-figure-300]

#### <a name="create-a-virtual-machine-by-using-hello-azure-portal"></a>Создание виртуальной машины с помощью портала Azure hello
toocreate простым способом Hello новой виртуальной машины из образа диска управляемых — с помощью hello портал Azure. Дополнительные сведения о как toocreate образ диска управление считывать [управляемого образа универсальной ВМ в Azure](https://docs.microsoft.com/azure/virtual-machines/windows/capture-image-resource)

1.  Go слишком<https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2Fimages>. Или в hello Azure меню портала, выберите **изображения**.
2.  Выберите hello управляемый образ toodeploy и щелкните на **создания виртуальной Машины**

Hello мастер поможет установить hello необходимые параметры toocreate hello виртуальной машины, кроме tooall необходимые ресурсы, такие как сетевые интерфейсы и учетные записи хранения. Ниже приведены некоторые из этих параметров.

1. **Основные сведения**:
 * **Имя**: hello имя ресурса hello (имя виртуальной машины hello).
 * **Тип диска виртуальной Машины**: выберите тип диска hello hello ОС диска. Если требуется toouse хранилище Premium для дисков данных, рекомендуется использовать хранилище Premium для hello диск ОС, а также.
 * **Имя пользователя и пароль** или **открытый ключ SSH**: Введите hello пользователя и пароль пользователя hello, которая создается во время инициализации hello. Для виртуальной машины Linux можно ввести hello использовать toosign toohello машине открытого ключа Secure Shell (SSH).
 * **Подписки**: выберите подписку hello, что требуется toouse tooprovision hello новой виртуальной машины.
 * **Группа ресурсов**: hello имя группы ресурсов hello hello виртуальной Машины. Можно ввести либо имя hello новое имя группы ресурсов или hello группы ресурсов, который уже существует.
 * **Расположение**: где toodeploy hello новой виртуальной машины. Если вы хотите tooconnect hello виртуальной машины tooyour локальную сеть, убедитесь, что выберите расположение hello hello виртуальной сети, соединяющей Azure tooyour в локальную сеть. Дополнительные сведения см. в разделе [Сеть Microsoft Azure][planning-guide-microsoft-azure-networking] [руководства по планированию и внедрению SAP NetWeaver на виртуальных машинах][planning-guide].
2. **Размер**:

     Список поддерживаемых типов виртуальных машин см. в примечании к SAP [1928533]. Убедитесь, что вы выберите правильный тип виртуальной Машины hello toouse хранилища Azure Premium. Не все типы виртуальных машин поддерживают хранилище класса Premium. Дополнительные сведения см. в разделе [Хранилище. Служба хранилища Microsoft Azure и диски данных][planning-guide-storage-microsoft-azure-storage-and-data-disks] и [Хранилище Azure класса Premium][planning-guide-azure-premium-storage] [руководства по планированию и внедрению SAP NetWeaver на виртуальных машинах][planning-guide].

3. **Параметры**:
  * **Хранилище**
    * **Тип диска**: выберите тип диска hello hello ОС диска. Если требуется toouse хранилище Premium для дисков данных, рекомендуется использовать хранилище Premium для hello диск ОС, а также.
    * **Использование управляемых дисков**: следует toouse управляемых дисков выберите "Да". Дополнительные сведения о дисках управляемых см. в разделе [управляемых дисков] [ planning-guide-managed-disks] в руководстве по планированию hello.
  * **Сеть**
    * **Виртуальная сеть** и **подсети**: toointegrate hello виртуальную машину с интрасетью, выберите hello виртуальной сети, подключенной tooyour локальной сети.
    * **Общедоступный IP-адрес**: выберите hello общедоступный IP-адрес, должны быть toouse или введите параметры toocreate новый общедоступный IP-адрес. Можно использовать открытые tooaccess адрес IP к виртуальной машине через Интернет hello. Убедитесь, что также создать сетевой безопасности группы toohelp безопасного доступа tooyour виртуальную машину.
    * **Группа безопасности сети.** Дополнительные сведения см. в статье [Управление потоком сетевого трафика с помощью групп безопасности сети][virtual-networks-nsg].
  * **Расширения**: можно установить расширения виртуальной машины, добавив их toohello развертывания. Расширение tooadd в этот шаг не требуется. Hello расширения, необходимые для поддержки SAP устанавливаются позже. В разделе [hello Настройка расширения улучшенного мониторинга Azure для SAP] [ deployment-guide-4.5] в данном руководстве.
  * **Высокий уровень доступности**: группа доступности выберите или введите параметры hello toocreate наличие новых значение. Дополнительные сведения см. в разделе [Группы доступности Azure][planning-guide-3.2.3].
  * **Мониторинг**
    * **Диагностика загрузки.** Диагностику загрузки можно **отключить**.
    * **Диагностика гостевой ОС.** Диагностику мониторинга можно **отключить**.

4. **Сводка**:

  Просмотрите выбранные параметры и нажмите кнопку **ОК**.

Виртуальная машина развернута в выбранной группы ресурсов hello.
#### <a name="create-a-virtual-machine-by-using-a-template"></a>Создание виртуальной машины с помощью шаблона
toocreate развертывания с помощью частный образ ОС из hello портал Azure, используйте один из следующих шаблонов SAP hello. Эти шаблоны, опубликованные в hello [репозитории GitHub azure — начало работы — шаблоны][azure-quickstart-templates-github]. Кроме того, виртуальную машину можно создать вручную с помощью [PowerShell][virtual-machines-upload-image-windows-resource-manager].

* [**Шаблон двухуровневой конфигурации (только одна виртуальная машина)** (sap-2-tier-user-image)][sap-templates-2-tier-user-image].

  Этот шаблон используется toocreate двухуровневую систему, используя только одна виртуальная машина.
* [**Шаблон двухуровневой конфигурации (только одна виртуальная машина) с образом управляемого диска** (sap-2-tier-user-image-md)][sap-templates-2-tier-user-image-md].

  toocreate двухуровневую систему, используя только одну виртуальную машину и образ управляемого диска, используйте этот шаблон.
* [**Шаблон трехуровневой конфигурации (несколько виртуальных машин)** (sap-3-tier-user-image)][sap-templates-3-tier-user-image].

  Этот шаблон используется toocreate трехуровневые системы с помощью нескольких виртуальных машин или собственный образ операционной системы.
* [**Шаблон трехуровневой конфигурации (несколько виртуальных машин) с образом управляемого диска** (sap-3-tier-user-image-md)][sap-templates-3-tier-user-image-md].

  toocreate трехуровневые системы с помощью нескольких виртуальных машин или собственный образ операционной системы и образа управляемого диска, используйте этот шаблон.

Введите следующие параметры для шаблона hello hello в hello портала Azure:

1. **Основные сведения**:
  * **Подписки**: hello подписки toouse toodeploy hello шаблона.
  * **Группа ресурсов**: hello шаблон toodeploy toouse hello ресурсов группы. Можно создать новую группу ресурсов или выберите существующую группу ресурсов в подписке hello.
  * **Расположение**: где toodeploy hello шаблона. Если вы выбрали существующую группу ресурсов, используется hello расположение группы ресурсов.
2. **Параметры**:
  * **Идентификатор системы SAP**: hello идентификатор системы SAP.
  * **Тип ОС**: hello тип операционной системы, который будет toodeploy (Windows или Linux).
  * **Размер системы SAP**: hello размер hello системы SAP.

    предоставляет Hello число SAPS hello новую систему. Если вы не уверены, сколько SAPS hello система требует, обратитесь к партнеру технологии SAP или системные интеграторы.
  * **Доступность системы** (только шаблон трехуровневого): hello доступность системы.

    Выберите **высокую доступность** в качестве конфигурации, которая подходит для установки высокого уровня доступности. Будут созданы два сервера баз данных и два сервера для ASCS.
  * **Тип хранилища** (только шаблон двухуровневая): hello тип toouse хранилища.

    В системах большого размера мы настоятельно рекомендуем использовать хранилище Azure класса Premium. Дополнительные сведения о типах носителей см. в разделе hello следующие ресурсы:
      * [Использование хранилища SSD класса Premium Azure для экземпляра СУБД SAP][2367194]
      * [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide] (раздел [Служба хранилища Microsoft Azure][dbms-guide-2.3]).
      * [Хранилище класса Premium: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure][storage-premium-storage-preview-portal]
      * [Введение tooMicrosoft хранилища Azure][storage-introduction]
  * **Пользовательский образ виртуального жесткого диска URI** (только шаблон образа диска неуправляемый): hello URI hello закрытый образ виртуального жесткого диска, например, https://&lt;имя_учетной_записи >.blob.core.windows.net/vhds/userimage.vhd.
  * **Учетная запись хранилища образов пользователя** (только шаблон образа диска неуправляемый): hello имя учетной записи хранения hello hello частный образ операционной системы хранения, например, &lt;имя_учетной_записи > в https://&lt;имя_учетной_записи >. BLOB.Core.Windows.NET/vhds/userimage.VHD.
  * **userImageId** (только шаблон образ управляемого диска): идентификатор hello управляемых образа необходимо toouse
  * **Имя пользователя администратора** и **пароль администратора**: hello, имя пользователя и пароль.

    Создается новый пользователь, для входа в toohello виртуальной машины.
  * **New or existing subnet** (Новая или имеющаяся подсеть). Определяет, следует ли создать виртуальную сеть и подсеть или использовать имеющуюся подсеть. При наличии виртуальной сети, подключенной tooyour локальную сеть, выберите **существующие**.
  * **Идентификатор подсети**: hello идентификатор hello подсети toowhich hello виртуальные машины будут подключаться. Выберите подсеть hello VPN или ExpressRoute виртуальной сети toouse tooconnect hello виртуальной машины tooyour в локальной сети. Идентификатор Hello обычно выглядит следующим образом:

    /subscriptions/&lt;идентификатор_подписки>/resourceGroups/&lt;имя_группы_ресурсов>/providers/Microsoft.Network/virtualNetworks/&lt;имя_виртуальной_сети>/subnets/&lt;имя_подсети>.

3. **Условия использования:**  
    Просмотрите и примите условия использования hello.

4.  Щелкните **Приобрести**.

#### <a name="install-hello-vm-agent-linux-only"></a>Установка hello агент виртуальной Машины (Linux)
Агент Linux должна быть установлена в hello пользовательский образ или развертывания hello приветствия toouse hello шаблоны, описанные в предшествующих раздел hello, завершится ошибкой. Загрузите и установите hello агент виртуальной Машины в hello пользовательский образ, как описано в [скачать, установить и включить агент виртуальной Машины Azure hello][deployment-guide-4.4]. Если вы не используете шаблоны hello, также можно установить позже hello агент виртуальной Машины.

#### <a name="join-a-domain-windows-only"></a>Присоединение к домену (только для Windows)
Если развертывания Azure подключенных tooan в локальной среде Active Directory или DNS-экземпляр с помощью Azure VPN-подключения сеть сеть или Azure ExpressRoute (это называется *между организациями* в [виртуальных машинах Azure Планирование и реализация для SAP NetWeaver][planning-guide]), предполагается, что hello виртуальной Машины присоединением к домену в локальной. Дополнительные сведения о вопросах для этого шага см. в разделе [присоединения к домену tooan локальной виртуальной Машины (только Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Настройка параметров прокси
В зависимости от конфигурации локальной сети может потребоваться tooset копирование hello прокси-сервера на виртуальной Машине. Если подключенных tooyour локальной сети через VPN или ExpressRoute ВМ, hello виртуальной Машины не может быть hello может tooaccess Интернета и не быть может toodownload hello необходимые расширения или сбора данных мониторинга. Дополнительные сведения см. в разделе [настройки прокси-сервера hello][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Настройка мониторинга
Убедитесь, что SAP поддерживает среду, Настройка hello расширения мониторинга Azure для SAP, как описано в toobe [hello Настройка расширения улучшенного мониторинга Azure для SAP][deployment-guide-4.5]. Проверьте предварительные условия hello для мониторинга SAP и требуемых минимальных версий ядра SAP и агента узла SAP, в ресурсах hello, перечисленных в [ресурсы SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Проверка мониторинга
Проверьте, работает ли мониторинг, как описано в разделе [Проверки и устранение неполадок при комплексной настройке мониторинга][deployment-guide-troubleshooting-chapter].


### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Сценарий 3. Перемещение локальной виртуальной машины с помощью специализированного виртуального жесткого диска Azure с SAP
В этом сценарии предполагается toomove определенную систему SAP из локальной среды tooAzure. Это можно сделать путем передачи hello VHD с ОС, двоичные файлы SAP hello, hello и в конечном итоге hello двоичные файлы СУБД, а также hello виртуальных жестких дисков с данными hello и файлы журналов для hello СУБД tooAzure. В отличие от hello сценарий, описанный в [сценарий 2: развертывание ВМ с помощью пользовательского образа для SAP][deployment-guide-3.3]в этом случае оставьте hello имя узла, ИД безопасности SAP, а SAP учетные записи пользователей в hello ВМ Azure, так как они находились настроить в локальной среде hello. Hello toogeneralize ОС не обязательно. Данная ситуация возникает чаще всего сценарии toocross организациями, где часть hello ландшафт SAP работает локально и выполняется его в Azure.

В этом сценарии hello агент виртуальной Машины — **не** автоматически, установленных во время развертывания. Поскольку hello агент виртуальной Машины и hello расширение мониторинга Azure для SAP требуется toorun SAP NetWeaver в Azure, необходимо toodownload, установить и включить обоих компонентов вручную после создания виртуальной машины hello.

Дополнительные сведения о hello агента ВМ Azure см. следующие ресурсы hello.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Обзор агента виртуальной машины Azure][virtual-machines-windows-agent-user-guide]
>
> ![Linux][Logo_Linux] Linux
>
> [Руководство пользователя агента Linux для Azure][virtual-machines-linux-agent-user-guide]
>
>

- - -

Следующая блок-схема Hello показана последовательность hello шаги по переносу Виртуальной машине локально с помощью специализированного VHD Azure:

![Блок-схема развертывания виртуальной машины для систем SAP с помощью диска виртуальной машины][deployment-guide-figure-400]

Если диск hello уже отправлен и задан в Azure (см. [виртуальных машинах Azure планированию и реализации для SAP NetWeaver][planning-guide]), выполните задачи hello, описанные в hello далее разделах.

#### <a name="create-a-virtual-machine"></a>Создание виртуальной машины
toocreate развертывания с помощью закрытого диска ОС через портал Azure hello использовать шаблон hello SAP, опубликованных в hello [репозитории GitHub azure — начало работы — шаблоны][azure-quickstart-templates-github]. Кроме того, виртуальную машину можно создать вручную с помощью PowerShell.

* [**Шаблон двухуровневой конфигурации (только одна виртуальная машина)** (sap-2-tier-user-disk)][sap-templates-2-tier-os-disk].

  Этот шаблон используется toocreate двухуровневую систему, используя только одна виртуальная машина.
* [**Шаблон двухуровневой конфигурации (только одна виртуальная машина) с управляемым диском** (sap-2-tier-user-disk-md)][sap-templates-2-tier-os-disk-md].

  toocreate двухуровневую систему с использованием только одной виртуальной машины и диска управляемых, используйте этот шаблон.

Введите следующие параметры для шаблона hello hello в hello портала Azure:

1. **Основные сведения**:
  * **Подписки**: hello подписки toouse toodeploy hello шаблона.
  * **Группа ресурсов**: hello шаблон toodeploy toouse hello ресурсов группы. Можно создать новую группу ресурсов или выберите существующую группу ресурсов в подписке hello.
  * **Расположение**: где toodeploy hello шаблона. Если вы выбрали существующую группу ресурсов, используется hello расположение группы ресурсов.
2. **Параметры**:
  * **Идентификатор системы SAP**: hello идентификатор системы SAP.
  * **Тип ОС**: hello тип операционной системы, который будет toodeploy (Windows или Linux).
  * **Размер системы SAP**: hello размер hello системы SAP.

    предоставляет Hello число SAPS hello новую систему. Если вы не уверены, сколько SAPS hello система требует, обратитесь к партнеру технологии SAP или системные интеграторы.
  * **Тип хранилища** (только шаблон двухуровневая): hello тип toouse хранилища.

    В системах большого размера мы настоятельно рекомендуем использовать хранилище Azure класса Premium. Дополнительные сведения о типах носителей см. в разделе hello следующие ресурсы:
      * [Использование хранилища SSD класса Premium Azure для экземпляра СУБД SAP][2367194]
      * [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide] (раздел [Служба хранилища Microsoft Azure][dbms-guide-2.3]).
      * [Хранилище класса Premium: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure][storage-premium-storage-preview-portal]
      * [Введение tooMicrosoft хранилища Azure][storage-introduction]
  * **URI VHD-файла на диске ОС** (только шаблон неуправляемые диска): hello URI hello частных дисков операционной системы, например, https://&lt;имя_учетной_записи >.blob.core.windows.net/vhds/osdisk.vhd.
  * **Управляемый ИД диска на диске ОС** (только шаблон управляемого диска): hello идентификатор hello диск управляемого диска ОС, /subscriptions/92d102f7-81a5-4df7-9877-54987ba97dd9/resourceGroups/group/providers/Microsoft.Compute/disks/WIN
  * **New or existing subnet** (Новая или имеющаяся подсеть). Определяет, следует ли создать виртуальную сеть и подсеть или использовать имеющуюся подсеть. При наличии виртуальной сети, подключенной tooyour локальную сеть, выберите **существующие**.
  * **Идентификатор подсети**: hello идентификатор hello подсети toowhich hello виртуальные машины будут подключаться. Выберите подсеть hello VPN или Azure ExpressRoute виртуальной сети toouse tooconnect hello виртуальной машины tooyour в локальной сети. Идентификатор Hello обычно выглядит следующим образом:

    /subscriptions/&lt;идентификатор_подписки>/resourceGroups/&lt;имя_группы_ресурсов>/providers/Microsoft.Network/virtualNetworks/&lt;имя_виртуальной_сети>/subnets/&lt;имя_подсети>.

3. **Условия использования:**  
    Просмотрите и примите условия использования hello.

4.  Щелкните **Приобрести**.

#### <a name="install-hello-vm-agent"></a>Установить агент ВМ hello
Здравствуйте, hello toouse шаблонов, описанных в предыдущем разделе, hello ВМ агент должен быть установлен на диске hello ОС или hello развертывание завершится ошибкой. Загрузите и установите агент ВМ hello в hello виртуальной Машины, как описано в [скачать, установить и включить агент виртуальной Машины Azure hello][deployment-guide-4.4].

Если вы не используете hello шаблоны, описанные в предшествующих раздел hello, можно также установить hello агент виртуальной Машины после него.

#### <a name="join-a-domain-windows-only"></a>Присоединение к домену (только для Windows)
Если развертывания Azure подключенных tooan в локальной среде Active Directory или DNS-экземпляр с помощью Azure VPN-подключения сеть сеть или ExpressRoute (это называется *между организациями* в [Планирование виртуальных машинах Azure и реализации для SAP NetWeaver][planning-guide]), предполагается, что hello виртуальной Машины присоединением к домену в локальной. Дополнительные сведения о вопросах для выполнения этой задачи см. в разделе [присоединения к домену tooan локальной виртуальной Машины (только Windows)][deployment-guide-4.3].

#### <a name="configure-proxy-settings"></a>Настройка параметров прокси
В зависимости от конфигурации локальной сети может потребоваться tooset копирование hello прокси-сервера на виртуальной Машине. Если подключенных tooyour локальной сети через VPN или ExpressRoute ВМ, hello виртуальной Машины не может быть hello может tooaccess Интернета и не быть может toodownload hello необходимые расширения или сбора данных мониторинга. Дополнительные сведения см. в разделе [настройки прокси-сервера hello][deployment-guide-configure-proxy].

#### <a name="configure-monitoring"></a>Настройка мониторинга
Убедитесь, что SAP поддерживает среду, Настройка hello расширения мониторинга Azure для SAP, как описано в toobe [hello Настройка расширения улучшенного мониторинга Azure для SAP][deployment-guide-4.5]. Проверьте предварительные условия hello для мониторинга SAP и требуемых минимальных версий ядра SAP и агента узла SAP, в ресурсах hello, перечисленных в [ресурсы SAP][deployment-guide-2.2].

#### <a name="monitoring-check"></a>Проверка мониторинга
Проверьте, работает ли мониторинг, как описано в разделе [Проверки и устранение неполадок при комплексной настройке мониторинга][deployment-guide-troubleshooting-chapter].

## <a name="update-hello-monitoring-configuration-for-sap"></a>Обновить hello конфигурации мониторинга для SAP
Обновление конфигурации мониторинга SAP hello в любом hello следующие сценарии:
* Создание группы корпорации Майкрософт и SAP Hello расширяет возможности мониторинга hello и запрашивает большее или меньшее количество счетчиков.
* Корпорация Майкрософт выпустила новую версию hello базовой инфраструктуры Azure, обеспечивающая hello данные мониторинга и hello расширение мониторинга Azure для SAP потребностей toobe адаптировать toothose изменения.
* Подключите tooyour дополнительные данные дисков виртуальной Машины Azure или удалить диск данных. В этом случае обновление hello коллекцию связанных с хранилищем данных. Изменение конфигурации путем добавления или удаления конечных точек или назначение IP-адреса tooa виртуальной Машины не влияет на конфигурацию мониторинга hello.
* Следует изменить размер hello ВМ Azure, например, размер A5 tooany другой размер виртуальной Машины.
* Добавьте новый tooyour интерфейсы сети виртуальной Машины Azure.

Параметры обновления hello мониторинг инфраструктуры, следуя hello мониторинга tooupdate шагов в [hello Настройка расширения улучшенного мониторинга Azure для SAP][deployment-guide-4.5].

## <a name="detailed-tasks-for-sap-software-deployment"></a>Подробное описание развертывания программного обеспечения SAP
В этом разделе приведены подробные инструкции для выполнения определенных задач в процессе конфигурации и развертывания hello.

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Развертывание командлетов Azure PowerShell
1.  Go слишком[центра загрузок Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  В разделе **Программы командной строки** в подразделе **PowerShell** выберите **Установка Windows**.
3.  В поле диалогового окна диспетчера загрузки Майкрософт hello hello загрузки файла (например, WindowsAzurePowershellGet.3f.3f.3fnew.exe), выберите **запуска**.
4.  Выберите toorun установщика веб-платформы Майкрософт (Microsoft Web PI) **Да**.
5.  Откроется следующая страница:

  ![Страница установки командлетов Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Выберите **установить**, а затем примите условия лицензии программного обеспечения корпорации Майкрософт hello.
7.  После этого будет установлен Azure PowerShell. Выберите **Готово** мастер установки tooclose hello.

Регулярно проверять наличие обновлений toohello PowerShell командлетов, которые обычно обновляются раз в месяц. toocheck простым способом Hello для обновлений является toodo hello предыдущих шагах установки, страницу установки toohello, показанном в шаге 5. Hello даты и версии номер выпуска командлетов hello включаются на странице приветствия, показанном в шаге 5. Если не указано иное в примечании SAP [1928533] или примечание SAP [2015553], рекомендуется работать с hello последняя версия командлетов Azure PowerShell.

версия hello toocheck hello командлетов Azure PowerShell, которые установлены на компьютере, выполните следующую команду PowerShell:
```powershell
(Get-Module AzureRm.Compute).Version
```
Hello результат выглядит следующим образом:

![Результат проверки версии командлетов Azure PowerShell][deployment-guide-figure-600]
<a name="figure-6"></a>

На компьютере установлена версия командлетов Azure hello является текущей версии hello, первая страница приветствия мастера установки hello указывает, добавив **(установлен)** toohello название продукта (см. следующий снимок экрана приветствия). Это означает, что установлена последняя версия командлетов Azure. tooclose приветствия мастера установки установите **выхода**.

![Страница установки командлетов Azure PowerShell, указывающее, что hello самую последнюю версию командлетов Azure PowerShell установлены][deployment-guide-figure-700]
<a name="figure-7"></a>

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Развертывание Azure CLI
1.  Go слишком[центра загрузок Microsoft Azure](https://azure.microsoft.com/downloads/).
2.  В разделе **средства командной строки**в разделе **интерфейс командной строки Azure**выберите hello **установить** ссылку для вашей операционной системы.
3.  В поле диалогового окна диспетчера загрузки Майкрософт hello hello загрузки файла (например, WindowsAzureXPlatCLI.3f.3f.3fnew.exe), выберите **запуска**.
4.  Выберите toorun установщика веб-платформы Майкрософт (Microsoft Web PI) **Да**.
5.  Откроется следующая страница:

  ![Страница установки командлетов Azure PowerShell][deployment-guide-figure-500]<a name="figure-5"></a>

6.  Выберите **установить**, а затем примите условия лицензии программного обеспечения корпорации Майкрософт hello.
7.  После этого будет установлен Azure CLI. Выберите **Готово** мастер установки tooclose hello.

Регулярно проверять наличие обновлений tooAzure CLI, который обычно обновляется раз в месяц. toocheck простым способом Hello для обновлений является toodo hello предыдущих шагах установки, страницу установки toohello, показанном в шаге 5.

версия toocheck hello Azure CLI, который установлен на компьютере, выполните следующую команду:
```
azure --version
```

Hello результат выглядит следующим образом:

![Результат проверки версии с помощью интерфейса командой строки Azure][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Присоединить к домену tooan локальной виртуальной Машины (только Windows)
При развертывании ВМ SAP в сценарии между организациями, где расширена локальной Active Directory и DNS в Azure, ожидается, что виртуальные машины hello соединить локальному домену. Здравствуйте, подробное описание действий, которые принимают toojoin домена tooan локальной виртуальной Машины и hello toobe требуется дополнительное программное обеспечение члена домена в локальной среде, зависит от клиента. Обычно toojoin tooan виртуальная машина локальный домен, требуется дополнительное программное обеспечение tooinstall, как и защиты от вредоносных программ и программное обеспечение резервного копирования или мониторинга.

В этом случае необходимо также убедиться, что, если параметры прокси-сервера Интернета, принудительно, если виртуальная машина будет присоединен к домену в вашей среде, имеет учетную запись Local System (S-1-5-18) в hello гостевой виртуальной Машины Windows hello hello одинаковые параметры прокси-сервера toomake. наиболее простой вариант Hello — tooforce hello прокси-сервера с помощью групповой политики, который применяет toosystems в домене hello домена.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Скачать, установить и включить hello агента ВМ Azure
Для виртуальных машин, развернутых из образа ОС, не подготовлен (например, изображение, которое не создаются в средство подготовки системы Windows или средства sysprep, hello) необходимо toomanually загрузку, установку и hello Включение агента ВМ Azure.

При развертывании виртуальной Машины из hello Azure Marketplace, этот шаг не требуется. Образы из hello Azure Marketplace уже имеют hello агента ВМ Azure.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows
1.  Загрузите hello агента ВМ Azure:
  1.  Загрузите hello [пакет установщика агента ВМ Azure](https://go.microsoft.com/fwlink/?LinkId=394789).
  2.  Хранить hello пакет MSI агента ВМ локально на персональном компьютере или сервере.
2.  Установка агента ВМ Azure hello:
  1.  Подключение toohello развертывания ВМ Azure с помощью удаленного рабочего стола (RDP).
  2.  Откройте окно проводника hello виртуальной Машины и выберите hello целевой каталог для hello MSI-файла hello агент виртуальной Машины.
  3.  Перетащите файл MSI установщика агента ВМ Azure hello из вашего локального компьютера или сервера toohello целевой каталог hello агент виртуальной Машины на hello виртуальной Машины.
  4.  Дважды щелкните файл MSI hello на hello виртуальной Машины.
3.  Для виртуальных машин, которые присоединены к домену tooon локальных доменов, убедитесь, что также применяются окончательной параметры прокси-сервера Интернета учетная запись локальной системы Windows toohello (S-1-5-18) в hello виртуальной Машины, как описано в [настройки прокси-сервера hello] [ deployment-guide-configure-proxy]. Hello агент виртуальной Машины выполняется в этом контексте и должен tooAzure может tooconnect toobe.

Взаимодействие с пользователем не требуется tooupdate hello агента ВМ Azure. Здравствуйте агент ВМ автоматически обновляется и не требует перезапуска виртуальной Машины.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
Используйте следующие команды tooinstall hello агент виртуальной Машины для Linux hello.

* **SUSE Linux Enterprise Server (SLES)**

  ```
  sudo zypper install WALinuxAgent
  ```

* **Red Hat Enterprise Linux (RHEL) или Oracle Linux**

  ```
  sudo yum install WALinuxAgent
  ```

Если уже установлен агент hello, tooupdate hello Azure Linux Agent hello действия, описанные в [обновление hello агент Azure Linux на toohello виртуальной Машины, последнюю версию с сайта GitHub][virtual-machines-linux-update-agent].

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Настройка прокси-сервера hello
Hello выполнить действия, tooconfigure hello прокси-сервера в Windows отличаются от способом hello, настройте hello прокси-сервера в Linux.

#### <a name="windows"></a>Windows
Параметры прокси-сервера необходимо настроить правильно для hello локальной системной учетной записью, что tooaccess hello Интернета. Если не заданы параметры прокси-сервера с помощью групповой политики, можно настроить параметры hello hello локальной системной учетной записи.

1. Go слишком**запустить**, введите **gpedit.msc**и выберите **ввод**.
2. Выберите **Конфигурация компьютера** > **Административные шаблоны** > **Компоненты Windows** > **Internet Explorer**. Убедитесь, что приветствия **сделать прокси-сервера, параметры на уровне компьютера (а не на уровне пользователя)** отключена или не настроена.
3. В **панели управления**, перейдите в слишком**сетями и общим доступом** > **обозревателя**.
4. На hello **подключений** вкладке, выберите hello **параметры локальной сети** кнопки.
5. Очистить hello **автоматическое определение параметров** флажок.
6. Выберите hello **использует прокси-сервер для подключений LAN** флажок и введите адрес прокси-сервера hello и порт.
7. Выберите hello **Дополнительно** кнопки.
8. В hello **исключения** введите IP-адрес hello **168.63.129.16**. Нажмите кнопку **ОК**.

#### <a name="linux"></a>Linux
Настройка hello правильный прокси-сервера в файл конфигурации hello hello агента виртуальной машине Microsoft Azure, которая находится в \\и т. д\\waagent.conf.

Набор hello следующие параметры:

1.  **Узел прокси-сервера HTTP**, Например, задайте для него слишком**proxy.corp.local**.
  ```
  HttpProxy.Host=<proxy host>

  ```
2.  **Порт прокси-сервера HTTP**, Например, задайте для него слишком**80**.
  ```
  HttpProxy.Port=<port of hello proxy host>

  ```
3.  Перезапустите агент hello.

  ```
  sudo service waagent restart
  ```

Здравствуйте, параметры прокси-сервера в \\и т. д\\waagent.conf справедливы toohello необходимые расширения виртуальных Машин. Если требуется, чтобы toouse hello Azure репозиториев, убедитесь, что репозиториев toothese трафика hello не проходит через локальной интрасети. При создании определяемых пользователем маршрутов tooenable принудительного туннелирования, убедитесь, что маршрут, который направляет трафик toohello репозиториев напрямую toohello Интернет, а не через сеть сеть VPN-подключение.

* **SLES**

  Необходимо также tooadd маршруты для hello IP-адреса, указанного в \\и т. д\\regionserverclnt.cfg. Hello на этом рисунке показан пример.

  ![Принудительное туннелирование][deployment-guide-figure-50]


* **RHEL**

  Необходимо также tooadd маршруты для IP-адресов hello hello узлов, перечисленных в \\и т. д\\yum.repos.d\\rhui подсистемы балансировки нагрузки. Пример см. в разделе hello предшествующий рис.

* **Oracle Linux**

  Для Oracle Linux в Azure нет репозиториев. Необходима tooconfigure собственные репозиториев для Oracle Linux или использовать hello открытых репозиториев.

Дополнительные сведения о пользовательских маршрутах см. в [этой статье][virtual-networks-udr-overview].

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Настройка hello расширение мониторинга Azure для SAP
Когда подготовленного hello виртуальной Машины как описано в [сценарии развертывания ВМ для SAP в Azure][deployment-guide-3], hello hello виртуальной машине установлен агент ВМ Azure. Hello следующим шагом является toodeploy hello расширение мониторинга Azure для SAP, которое доступно в hello репозиторий расширений Azure в глобальных центрах hello. Дополнительные сведения см. в [руководстве по планированию и внедрению SAP NetWeaver на виртуальных машинах][planning-guide-9.1].

Можно использовать PowerShell или Azure CLI tooinstall и настроить hello расширение мониторинга Azure для SAP. расширение hello tooinstall на виртуальной Машине Linux или группу Windows с помощью компьютером Windows. в разделе [Azure PowerShell][deployment-guide-4.5.1]. tooinstall hello расширения на виртуальной Машине Linux с помощью настольного компьютера Linux, в разделе [Azure CLI][deployment-guide-4.5.2].

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell для виртуальных машин Windows и Linux
hello tooinstall расширение мониторинга Azure для SAP с помощью PowerShell:

1. Убедитесь, что установки hello последняя версия командлетов Azure PowerShell hello. Дополнительные сведения см. в разделе [Развертывание командлетов Azure PowerShell][deployment-guide-4.1].  
2. Запустите следующий командлет PowerShell hello.
    Чтобы просмотреть список доступных сред, выполните командлет `commandlet Get-AzureRmEnvironment`. Toouse глобального Azure в вашей среде это **облачной**. Для Azure в Китае выберите **AzureChinaCloud**.

    ```powershell
    $env = Get-AzureRmEnvironment -Name <name of hello environment>
    Login-AzureRmAccount -Environment $env
    Set-AzureRmContext -SubscriptionName <subscription name>

    Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
    ```

После ввода данные вашей учетной записи и определите hello виртуальной машины Azure, скрипт hello развертывает hello необходимые расширения и hello необходимые возможности. Это может занять несколько минут.
Дополнительные сведения о командлете `Set-AzureRmVMAEMExtension` см. в [этой статье][msdn-set-azurermvmaemextension].

![Экран успешного выполнения командлета Azure Set-AzureRmVMAEMExtension для SAP][deployment-guide-figure-900]

Hello `Set-AzureRmVMAEMExtension` конфигурации все hello действия tooconfigure мониторинга узла для SAP.

выходные данные сценария Hello включает hello следующую информацию:

* Подтверждение, что наблюдение за диск hello операционной системы и все дополнительные диски с данными конфигурации.
* следующие два сообщения Hello подтверждение hello настройки метрик хранилища для конкретной учетной записи хранения.
* Первой строке результата дает hello состояние фактического обновления конфигурации мониторинга hello hello.
* Другая строка выходных данных подтверждает конфигурации hello развернута или обновлена.
* Последняя строка Hello выходных данных носит информационный характер. Он показывает параметры для тестирования конфигурации мониторинга hello.
* Продолжить проверку готовности hello hello расширение мониторинга Azure для SAP, toocheck улучшенного мониторинга Azure все шаги были выполнены успешно, что этот hello инфраструктуры Azure предоставляет необходимые данные hello, как описано в [Проверки готовности для улучшенного мониторинга Azure для SAP][deployment-guide-5.1].
* Подождите 15-30 минут для диагностики Azure toocollect hello важные данные.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Интерфейс командной строки Azure для виртуальных машин Linux
hello tooinstall расширение мониторинга Azure для SAP с помощью Azure CLI:

1. Установите Azure CLI 1.0, как описано в [Install hello Azure CLI 1.0][azure-cli].
2. Войдите в систему, используя учетную запись Azure.

  ```
  azure login
  ```

3. Переключение режима tooAzure диспетчера ресурсов:

  ```
  azure config mode arm
  ```

4. Включите расширенный мониторинг Azure.

  ```
  azure vm enable-aem <resource-group-name> <vm-name>
  ```

5. Убедитесь, что, hello расширение мониторинга Azure не активна на виртуальной Машине Linux Azure hello. Проверка hello ли файл \\var\\lib\\AzureEnhancedMonitor\\PerfCounters существует. Если он существует, в командной строке выполните этой команды toodisplay, собираемых hello монитора Enhanced Azure:
```
cat /var/lib/AzureEnhancedMonitor/PerfCounters
```

Hello вывод выглядит следующим образом:
```
2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
…
…
```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Проверки и устранение неполадок при комплексной настройке мониторинга
После развертывания ВМ Azure и настроить hello соответствующей инфраструктуры мониторинга Azure проверьте, работают ли все компоненты hello hello расширение мониторинга Azure надлежащим образом.

Запустите проверку готовности hello hello расширение мониторинга Azure для SAP, как описано в [проверки готовности для расширения улучшенного мониторинга Azure для SAP hello][deployment-guide-5.1]. Если проверка выполнена успешно и получены все соответствующие счетчики производительности, мониторинг Azure успешно настроен. Можно продолжить установку hello агента узла SAP, как описано в примечаниях SAP hello в [ресурсы SAP][deployment-guide-2.2]. Если проверка готовности hello указывает, что счетчиков отсутствуют, выполнение проверки работоспособности hello hello инфраструктуры мониторинга Azure, как описано в [проверки работоспособности для конфигурации инфраструктуры мониторинга Azure] [ deployment-guide-5.2]. Сведения об устранении неполадок см. в разделе [Устранение неполадок инфраструктуры мониторинга Azure для SAP][deployment-guide-5.3].

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Проверка готовности hello расширение мониторинга Azure для SAP
Эта проверка гарантирует, что все метрики производительности, отображаемых в приложении SAP предоставляемые hello базовой инфраструктуры мониторинга Azure.

#### <a name="run-hello-readiness-check-on-a-windows-vm"></a>Запустить проверку готовности hello виртуальной Машины Windows.

1.  Войдите в toohello виртуальной машины Azure (с помощью учетной записи администратора не обязательна).
2.  Откройте окно командной строки и
3.  В командной строке hello изменить каталог hello toohello папки установки расширения улучшенного мониторинга Azure для SAP hello: C:\\пакетов\\подключаемых модулей\\ Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;версии >\\drop

  Hello *версии* в toohello путь hello расширения мониторинга могут быть различными. Если вы видите папки для нескольких версий hello расширения в папке установки hello, проверьте конфигурацию hello объекта hello службы AzureEnhancedMonitoring Windows, мониторинга и затем коммутатора toohello папки отображается в виде *tooexecutable путь* .

  ![Свойства службы, запущенной hello расширение мониторинга Azure для SAP][deployment-guide-figure-1000]

4.  Hello командной строки, выполнив **azperflib.exe** без параметров.

  > [!NOTE]
  > Azperflib.exe работает в цикле и обновляет собранные hello счетчики каждые 60 секунд. цикл tooend hello, hello закрыть окно командной строки.
  >
  >

Если hello расширение мониторинга Azure не установлен или hello служба AzureEnhancedMonitoring не запущена, расширение hello не был настроен правильно. Подробные сведения о как toodeploy hello расширения см. в разделе [Устранение неполадок hello инфраструктуры мониторинга Azure для SAP][deployment-guide-5.3].

##### <a name="check-hello-output-of-azperflibexe"></a>Проверьте выходные данные hello azperflib.exe
Результат выполнения файла azperflib.exe содержит все заполненные счетчики производительности Azure для SAP. Hello нижней части списка собранных счетчиков hello сводки и состояния индикаторов Показать состояние hello Azure мониторинга.

![Результат проверки работоспособности с использованием файла azperflib.exe, в котором указано, что ошибок нет][deployment-guide-figure-1100]
<a name="figure-11"></a>

Проверьте hello результат, возвращенный для hello **Counters total** выходных данных, который выводятся как пустые, так и для **состояние работоспособности**, показанный в предшествующих рисунок hello.

Полученные значения hello интерпретировать следующим образом:

| Итоговые значения azperflib.exe | Состояние работоспособности мониторинга Azure |
| --- | --- |
| **Вызовы API — недоступны** | Счетчики, которые доступны не может быть любой конфигурации виртуальной машины неприменимо toohello или ошибок. Просмотрите **состояние работоспособности**. |
| **Counters total - empty** (Всего счетчиков: пусто) |Привет, следующие два счетчика хранилища Azure может быть пустым: <ul><li>задержка операций чтения в хранилище на сервере (мс);</li><li>задержка операций чтения в хранилище E2E (мс).</li></ul>Все остальные значения счетчиков должны присутствовать. |
| **Состояние работоспособности** |Отображается только при возврате состояния **ОК**. |
| **Диагностика** |Подробные сведения о состоянии работоспособности. |

Если hello **состояние работоспособности** значение не **ОК**, следуйте инструкциям в разделе hello [проверки работоспособности для конфигурации инфраструктуры мониторинга Azure] [ deployment-guide-5.2].

#### <a name="run-hello-readiness-check-on-a-linux-vm"></a>Запустить проверку готовности hello на виртуальной Машине Linux

1.  Подключение toohello виртуальной машине Azure с помощью SSH.

2.  Проверьте выходные данные hello hello расширение мониторинга Azure.

  а.  Запустите `more /var/lib/AzureEnhancedMonitor/PerfCounters`

   **Ожидаемый результат.** Возвращает список счетчиков производительности. Hello файла не должно быть пустым.

 b. Запустите `cat /var/lib/AzureEnhancedMonitor/PerfCounters | grep Error`

   **Ожидаемый результат**: возвращает одну строку, где ошибка hello **нет**, например **3; конфигурации; Ошибка; 0; 0; Нет; 0; 1456416792; tst servercs;**

  c. Запустите `more /var/lib/AzureEnhancedMonitor/LatestErrorRecord`

    **Ожидаемый результат.** Возвращает пустую строку или строка отсутствует.

Если hello выше проверка не пройдена, выполните следующие дополнительные проверки:

1.  Убедитесь, что waagent hello установлен и включен.

  а.  Запустите `sudo ls -al /var/lib/waagent/`

      **Ожидаемый результат**: Перечисляет hello содержимое каталога waagent hello.

  b.  Запустите `ps -ax | grep waagent`

   **Ожидаемый результат.** Должна отобразиться одна запись, аналогичная следующей: `python /usr/sbin/waagent -daemon`.

3.   Убедитесь, что этот hello расширение мониторинга Azure установлены и запущены.

  а.  Запустите `sudo sh -c 'ls -al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'`

    **Ожидаемый результат**: Перечисляет hello содержимое каталога hello расширение мониторинга Azure.

  b. Запустите `ps -ax | grep AzureEnhanced`

     **Ожидаемый результат.** Должна отобразиться одна запись, аналогичная следующей: `python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py daemon`.

3. Установка агента узла SAP, как описано в примечании SAP [1031096]и проверьте выходные данные hello `saposcol`.

  а.  Запустите `/usr/sap/hostctrl/exe/saposcol -d`

  b.  Запустите `dump ccm`

  c.  Проверка ли hello **Virtualization_Configuration\Enhanced мониторинг доступа** метрика **true**.

Если сервер приложений ABAP SAP NetWeaver уже установлен, откройте транзакцию ST06 и проверьте, включен ли расширенный мониторинг.

Если любой из этих проверок завершиться ошибкой и подробные сведения о как tooredeploy hello расширения см. в разделе [Устранение неполадок hello инфраструктуры мониторинга Azure для SAP][deployment-guide-5.3].

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Проверка работоспособности для hello конфигурации инфраструктуры мониторинга Azure
Если некоторые hello данные мониторинга предоставляются неверно, обозначенный hello тестирования описан [проверки готовности для улучшенного мониторинга Azure для SAP][deployment-guide-5.1], запустите hello `Test-AzureRmVMAEMExtension` toocheck командлета является ли hello мониторинга инфраструктуры и отслеживание расширения для НАСТОЛЬНОЙ hello Azure настроены правильно.

1.  Убедитесь, что установлена hello последняя версия командлетов Azure PowerShell hello, как описано в [командлеты PowerShell Azure развертывание][deployment-guide-4.1].
2.  Запустите следующий командлет PowerShell hello. Список доступных сред выполнения командлета hello `Get-AzureRmEnvironment`. глобальные Azure, выберите toouse hello **облачной** среды. Для Azure в Китае выберите **AzureChinaCloud**.
  ```powershell
  $env = Get-AzureRmEnvironment -Name <name of hello environment>
  Login-AzureRmAccount -Environment $env
  Set-AzureRmContext -SubscriptionName <subscription name>
  Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
  ```

3.  Введите данные учетной записи и определите hello виртуальной машины Azure.

  ![Страница ввода командлета Azure Test-VMConfigForSAP_GUI для SAP][deployment-guide-figure-1200]

4. конфигурации тестов hello Hello скрипт hello виртуальной машины необходимо выбрать.

  ![Результат успешного тестирования hello инфраструктуры мониторинга Azure для SAP][deployment-guide-figure-1300]

Убедитесь, что для каждой проверки установлено состояние **ОК**. Если некоторые проверки не отображаются, **ОК**, запустите командлет для обновления hello, как описано в [hello Настройка расширения улучшенного мониторинга Azure для SAP][deployment-guide-4.5]. Подождите 15 минут и повторите hello проверки, описанных в [проверки готовности для улучшенного мониторинга Azure для SAP] [ deployment-guide-5.1] и [проверки работоспособности для конфигурации инфраструктуры мониторинга Azure] [deployment-guide-5.2]. Если hello проверки по-прежнему указывают на проблему с некоторыми счетчиками, см. раздел [Устранение неполадок hello инфраструктуры мониторинга Azure для SAP][deployment-guide-5.3].

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Устранение неполадок hello инфраструктуры мониторинга Azure для SAP

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] Счетчики производительности Azure вообще не отображаются
Служба AzureEnhancedMonitoring Windows Hello собирает метрики производительности в Azure. Если служба hello не был правильно установлен или не запущена на виртуальной машине, можно собирать метрики производительности.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>каталог установки Hello hello расширение мониторинга Azure пустой

###### <a name="issue"></a>Проблема
каталог установки Hello C:\\пакетов\\подключаемые модули\\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\&lt;версии >\\сброса является пустым.

###### <a name="solution"></a>Решение
Hello расширение не установлено. Определите, связано ли это с неполадками прокси (как описано выше). Может потребоваться машины hello toorestart или повторного запуска hello `Set-AzureRmVMAEMExtension` сценарий настройки.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>Служба для расширенного мониторинга Azure не существует

###### <a name="issue"></a>Проблема
Hello служба AzureEnhancedMonitoring Windows не существует.

В результате выполнения azperlib.exe отображается следующая ошибка:

![Выполнение azperflib.exe показывает, что служба hello hello расширение мониторинга Azure для SAP не запущена][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>Решение
Если служба hello не существует, hello расширение мониторинга Azure для SAP не был установлен правильно. Повторное развертывание hello расширения с помощью hello шаги, описанные для вашего сценария развертывания в [сценарии развертывания ВМ для SAP в Azure][deployment-guide-3].

После развертывания расширения hello через 1 час, проверьте еще раз, предоставляются ли счетчики производительности Azure hello в hello виртуальной Машине Azure.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-toostart"></a>Служба для улучшенного мониторинга Azure существует, но произошел сбой toostart

###### <a name="issue"></a>Проблема
Hello служба AzureEnhancedMonitoring Windows существует и включена, но произошел сбой toostart. Дополнительные сведения Проверьте журнал событий приложения hello.

###### <a name="solution"></a>Решение
Неправильная конфигурация Hello. Перезапустите hello отслеживание расширения для hello виртуальной Машины, как описано в [hello Настройка расширения улучшенного мониторинга Azure для SAP][deployment-guide-4.5].

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] Отсутствуют некоторые счетчики производительности Azure
Служба AzureEnhancedMonitoring Windows Hello собирает метрики производительности в Azure. Hello служба получает данные из нескольких источников. Некоторые данные конфигурации собираются локально, метрики производительности считываются из системы диагностики Azure, Счетчики хранилища используются из журналов на уровне подписки hello хранилища.

Если устранить неполадки с помощью Примечание SAP [1999351] не устранить проблему hello, повторно запустите hello `Set-AzureRmVMAEMExtension` сценарий настройки. Могут быть toowait в час, так как счетчики analytics или диагностики хранилища не могут быть созданы сразу после включения. При повторном возникновении проблемы hello, откройте сообщение о поддержке клиентов SAP на hello компонента BC-OP-NT-AZR для Windows или BC-OP-LNX-AZR для виртуальной машины Linux.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] Счетчики производительности Azure вообще не отображаются
Сбор показателей производительности в Azure выполняет управляющая программа. Если управляющая программа hello не запущена, можно собирать метрики производительности.

##### <a name="hello-installation-directory-of-hello-azure-enhanced-monitoring-extension-is-empty"></a>каталог установки Hello hello расширения улучшенного мониторинга Azure пустой

###### <a name="issue"></a>Проблема
каталог Hello \\var\\lib\\waagent\\ имеет вложенный каталог для hello расширения улучшенного мониторинга Azure.

###### <a name="solution"></a>Решение
Hello расширение не установлено. Определите, связано ли это с неполадками прокси (как описано выше). Может потребоваться toorestart hello компьютера или повторного запуска hello `Set-AzureRmVMAEMExtension` сценарий настройки.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] Отсутствуют некоторые счетчики производительности Azure
Сбор показателей производительности в Azure выполняет управляющая программа, которая получает данные из нескольких источников. Некоторые данные конфигурации собираются локально, метрики производительности считываются из системы диагностики Azure, Счетчики хранилища берутся из журналов hello в вашей подписке хранилища.

Полный и актуальный список известных проблем см. в примечании SAP [1999351]. В нем содержатся дополнительные сведения об устранении неполадок расширенного мониторинга Azure для SAP.

Если устранить неполадки с помощью Примечание SAP [1999351] не устранить проблему hello, повторно запустите hello `Set-AzureRmVMAEMExtension` сценарий конфигурации, как описано в [hello Настройка расширения улучшенного мониторинга Azure для SAP][deployment-guide-4.5]. Могут быть toowait часа, так как счетчики analytics или диагностики хранилища не могут быть созданы сразу после включения. При повторном возникновении проблемы hello, откройте сообщение о поддержке клиентов SAP на hello компонента BC-OP-NT-AZR для Windows или BC-OP-LNX-AZR для виртуальной машины Linux.
