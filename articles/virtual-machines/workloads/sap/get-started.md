---
title: "aaaGetting работы с SAP на виртуальных машинах Azure | Документы Microsoft"
description: "Сведения о работе решений SAP на виртуальных машинах в Microsoft Azure."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: ad8e5c75-0cf6-4564-ae62-ea1246b4e5f2
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ac390f8e1c802505b8f9304a12868364fa60f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-for-hosting-and-running-sap-workload-scenarios"></a>Размещение и выполнение сценариев рабочей нагрузки SAP с помощью Azure
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
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2233094]:https://launchpad.support.sap.com/#/notes/2233094
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription

[dbms-guide]:dbms-guide.md 
[dbms-guide-2.1]:dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f 
[dbms-guide-2.2]:dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 
[dbms-guide-2.3]:dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 
[dbms-guide-2]:dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 
[dbms-guide-3]:dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 
[dbms-guide-5.5.1]:dbms-guide.md#0fef0e79-d3fe-4ae2-85af-73666a6f7268 
[dbms-guide-5.5.2]:dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b
[dbms-guide-5.6]:dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 
[dbms-guide-5.8]:dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 
[dbms-guide-5]:dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 
[dbms-guide-8.4.1]:dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 
[dbms-guide-8.4.2]:dbms-guide.md#23c78d3b-ca5a-4e72-8a24-645d141a3f5d 
[dbms-guide-8.4.3]:dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c 
[dbms-guide-8.4.4]:dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 
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

[deployment-guide]:deployment-guide.md 
[deployment-guide-2.2]:deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 
[deployment-guide-3.1.2]:deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab 
[deployment-guide-3.2]:deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 
[deployment-guide-3.3]:deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 
[deployment-guide-3.4]:deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1
[deployment-guide-3]:deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e 
[deployment-guide-4.1]:deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 
[deployment-guide-4.2]:deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e 
[deployment-guide-4.3]:deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc 
[deployment-guide-4.4.2]:deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 
[deployment-guide-4.4]:deployment-guide.md#c7cbb0dc-52a4-49db-8e03-83e7edc2927d 
[deployment-guide-4.5.1]:deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 
[deployment-guide-4.5.2]:deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f 
[deployment-guide-4.5]:deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca 
[deployment-guide-5.1]:deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2
[deployment-guide-5.2]:deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 
[deployment-guide-5.3]:deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 
[deployment-guide-configure-monitoring-scenario-1]:deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b 
[deployment-guide-configure-proxy]:deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d 
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
[deployment-guide-troubleshooting-chapter]:deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b 
[deploy-template-cli]:../../../resource-group-template-deploy.md
[deploy-template-portal]:../../../resource-group-template-deploy.md
[deploy-template-powershell]:../../../resource-group-template-deploy.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md
[getting-started-dbms]:get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c


[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056
[ha-guide]:sap-high-availability-guide.md

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[planning-guide]:planning-guide.md 
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff 
[planning-guide-11.4.1]:planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 
[planning-guide-11.5]:planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f 
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803 
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 
[planning-guide-3.1]:planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a 
[planning-guide-3.2.1]:planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 
[planning-guide-3.2.2]:planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 
[planning-guide-3.2.3]:planning-guide.md#18810088-f9be-4c97-958a-27996255c665 
[planning-guide-3.2]:planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 
[planning-guide-3.3.2]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 
[planning-guide-5.1.1]:planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 
[planning-guide-5.1.2]:planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c 
[planning-guide-5.2.1]:planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef 
[planning-guide-5.2.2]:planning-guide.md#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 
[planning-guide-5.2]:planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 
[planning-guide-5.3.1]:planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 
[planning-guide-5.3.2]:planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a 
[planning-guide-5.4.2]:planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 
[planning-guide-5.5.1]:planning-guide.md#4efec401-91e0-40c0-8e64-f2dceadff646 
[planning-guide-5.5.3]:planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d 
[planning-guide-7.1]:planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 
[planning-guide-7]:planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 
[planning-guide-9.1]:planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 
[planning-guide-azure-premium-storage]:planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 

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
[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f 

[powershell-install-configure]:https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[resource-group-authoring-templates]:../../../resource-group-authoring-templates.md
[resource-group-overview]:../../../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../../../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
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
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md 
[virtual-machines-linux-agent-user-guide]:../../linux/agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:../../linux/agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:../../linux/capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#capture-the-vm
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
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
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

Выбирая Microsoft Azure в качестве партнеру готовности облака SAP, являются может tooreliably работает на платформе масштабируемой, совместимых и исключительную критически важных рабочих нагрузок SAP и сценариев.  Получение hello масштабируемости, гибкости и экономия Azure. С hello развернут партнерство между корпорацией Майкрософт и SAP и можно запускать приложения SAP в сценариях разработки и тестирования и производства в Azure, полностью поддерживаются. Из SAP NetWeaver tooSAP S4/HANA SAP BI Linux tooWindows, tooSQL SAP HANA, у нас есть вас. 

Помимо размещение сценариев SAP NetWeaver с Здравствуйте различными системами DBMS на Azure, можно разместить в разных другие сценарии рабочая нагрузка SAP, как бизнес-Аналитики SAP в Azure. Документация о развертываниях SAP NetWeaver на виртуальных машинах Azure собственного можно найти в hello раздел «SAP NetWeaver на виртуальных машинах Azure». 

Azure имеет собственный предложения виртуальной машине Azure, постоянно растет в объем ресурсов ЦП и памяти ресурсы toocover SAP рабочей нагрузки, использующий SAP HANA. Дополнительные сведения по этой теме поиска hello документов в разделе "hello" SAP HANA на виртуальных машинах Azure.»

Hello Azure для SAP HANA имеет уникальный предложение, которое задает Azure отдельно от конкурентов. В порядке tooenable размещение больше памяти и ресурсов ЦП ресурсоемких SAP, сценарии, включающие SAP HANA, Azure предлагает hello использование клиента выделенном оборудовании исходного hello с целью выполнения развертывания SAP HANA, которые требуют копирования too20 ТБ (60 ТБ масштабное развертывание) память для S/4HANA или другая нагрузка SAP HANA. Этот уникальный решения Azure для SAP HANA в Azure (большие экземпляры) позволяет toorun SAP HANA на оборудовании исходного выделенного hello с уровня приложения SAP hello или слоя среднего и шпионских рабочей нагрузки, размещенной в машинном коде виртуальных машинах Azure. Это решение, описанное в нескольких документов, в разделе "hello" «SAP HANA в Azure (большие экземпляры)».   

Размещение рабочей нагрузки сценариев SAP в Azure также можно создать требования к интеграции удостоверений и единого входа с помощью компонентов SAP Azure Activity Directory toodifferent и SAP SaaS или предлагает PaaS. Список таких интеграции и сценариях единый вход с Azure Active Directory (AAD) и SAP сущностями описано и описаны в разделе hello» интеграции удостоверений AAD SAP и единый вход.»


## <a name="sap-hana-on-sap-hana-on-azure-large-instances"></a>SAP HANA на сервере SAP HANA в Azure (крупные экземпляры)

### <a name="overview-and-architecture-of-sap-hana-on-azure-large-instances"></a>Обзор и описание архитектуры SAP HANA в Azure (крупные экземпляры)
Заголовок: aaaOverview и архитектура SAP HANA в Azure (большие экземпляры)

Сводка: Этой архитектуры и техническое руководство по развертыванию предоставляет сведения о toohelp развертывания SAP на hello новый HANA SAP в Azure (большие экземпляры) в Azure. Это не предполагаемого toobe полное руководство покрытия определенные настройки решений SAP, но вместо полезную информацию в первоначальное развертывание и текущих операций. Не заменяйте документацию SAP по связанные toohello установки SAP HANA (или hello много примечания о поддержке SAP, охватывающие hello раздела). Он дает возможность просмотра и содержит дополнительные сведения hello установки SAP HANA в Azure (большие экземпляры).

Обновление: июль 2017 г.

[Это руководство можно найти здесь.](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="infrastructure-and-connectivity-toosap-hana-on-azure-large-instances"></a>Инфраструктуры и подключения к tooSAP HANA в Azure (большие экземпляры)
Заголовок: aaaInfrastructure и подключения к tooSAP HANA в Azure (большие экземпляры)

Сводка: После завершения покупки hello SAP HANA в Azure (большие экземпляры) между вами и hello технической поддержки учетных записей Microsoft enterprise, различные конфигурации сети требуются в порядке tooensure правильной связи.  Требуется эта информация hello структуры документа, имеющий toobe совместно с hello следующую информацию. В этом документе перечислены какие сведения toobe собранные и какие сценарии настройки toobe запуска. 

Обновление: июль 2017 г.

[Это руководство можно найти здесь.](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="install-sap-hana-in-sap-hana-on-azure-large-instances"></a>Установка SAP HANA на сервере SAP HANA в Azure (крупные экземпляры)
Заголовок: aaaInstall SAP HANA на HANA SAP в Azure (большие экземпляры)

Сводка: В этом документе описаны процедуры установки hello по установке SAP HANA большого экземпляра Azure. 

Обновление: июль 2017 г.

[Это руководство можно найти здесь.](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-and-disaster-recovery-of-sap-hana-on-azure-large-instances"></a>Высокая доступность и аварийное восстановление SAP HANA в Azure (крупные экземпляры)
Заголовок: aaaHigh доступности и аварийного восстановления из SAP HANA в Azure (большие экземпляры)

Сводка: для работы критически важных серверов SAP HANA в Azure (крупные экземпляры) крайне важно обеспечить высокий уровень доступности и реализовать стратегию аварийного восстановления. Его toowork импорта с SAP, ваш системный интегратор или Microsoft tooproperly архитектора и реализации hello справа стратегии ДОСТУПНОСТИ и аварийное Восстановление для. Важные вопросы, как целевой точки восстановления (RPO) и восстановления время Целевое значение, определенных tooyour среде, необходимо учитывать.  В этом документе рассматриваются варианты для включения предпочтительного уровня высокой доступности и аварийного восстановления.

Последнее обновление: декабрь 2016 г.

[Этот документ можно найти здесь](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="troubleshooting-and-monitoring-of-sap-hana-on-azure-large-instances"></a>Устранение неполадок и мониторинг архитектуры SAP HANA в Azure (крупные экземпляры).
Заголовок: aaaTroubleshooting и мониторинга для SAP HANA в Azure (большие экземпляры)

Сводка: в данном руководстве содержатся сведения, полезные для организации мониторинга среды SAP HANA в Azure, а также дополнительные сведения об устранении неполадок. 

Последнее обновление: декабрь 2016 г.

[Этот документ можно найти здесь](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="sap-hana-on-azure-virtual-machines"></a>SAP HANA на виртуальных машинах Azure

### <a name="getting-started-with-sap-hana-on-azure"></a>Начало работы с SAP HANA в Azure
Заголовок: руководство по aaaQuickstart для ручной установки SAP HANA на виртуальных машинах Azure

Сводка: Этого краткого руководства помогает tooset экземпляра SAP HANA систему на виртуальных машинах Azure ручной установки SAP NetWeaver 7.5 и SAP HANA SP12. руководство по Hello предполагает, что чтения hello знакомы с основами Azure IaaS как hello как toodeploy виртуальных машин или виртуальные сети, либо через портал Azure hello или Powershell или интерфейс командной строки, включая шаблоны json toouse параметр. Более того предполагается, что чтения hello знакомые с SAP HANA, SAP NetWeaver и как tooinstall его локально.

Обновление: июнь 2017 г.

[Это руководство можно найти здесь.](hana-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="s4hana-sap-cal-deployment-on-azure"></a>Развертывание S/4HANA SAP CAL в Azure
Заголовок: aaaDeploy SAP S/4HANA или BW/4HANA в Azure

Сводка: Это руководство поможет развертывания hello toodemonstrate S/4HANA SAP в Azure с помощью SAP облака устройства библиотеки. Устройства библиотеки SAP облака — это служба, SAP, который позволяет приложениям toodeploy SAP в Azure. Hello руководстве описывается развертывание hello шаг за шагом.

Обновление: июнь 2017 г.

[Это руководство можно найти здесь.](cal-s4h.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="high-availability-of-sap-hana-in-azure-virtual-machines"></a>Высокий уровень доступности SAP HANA на виртуальных машинах Azure
Заголовок: aaaHigh доступности из SAP HANA на виртуальных машинах Azure

Сводка: В этом руководстве приводит можно путем настройки высокого уровня доступности hello hello ОС SUSE 12 и SAP HANA tooaccommodate HANA системы репликации с автоматическим переходом на другой. руководство по Hello не является подходящим для SUSE и виртуальных машин Azure. руководства Hello еще применяется к Red Hat или исходного состояния системы или частное облако или других развертываний общедоступное облако Azure не.

Обновление: июнь 2017 г.

[Это руководство можно найти здесь.](sap-hana-high-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-backup-overview-on-azure-vms"></a>Обзор резервного копирования SAP HANA на виртуальных машинах Azure
Заголовок: aaaBackup руководство по SAP HANA на виртуальных машинах Azure

Сводка. Это руководство содержит основные сведения о возможностях резервного копирования SAP HANA на виртуальных машинах Azure.

Обновление: март 2017 г.

[Это руководство можно найти здесь.](sap-hana-backup-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="sap-hana-file-level-backup-on-azure-vms"></a>Резервное копирование SAP HANA на уровне файлов на виртуальных машинах Azure
Заголовок: резервное копирование HANA aaaSAP, основанные на моментальных снимках хранилища

Сводка. Это руководство содержит информацию об использовании резервных копий на основе моментальных снимков на виртуальных машинах Azure при запуске SAP HANA на виртуальных машинах Azure.

Обновление: март 2017 г.

[Это руководство можно найти здесь.](sap-hana-backup-file-level.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="sap-hana-snapshot-based-backups-on-azure-vms"></a>Резервные копии на основе моментальных снимков SAP HANA на виртуальных машинах Azure
Заголовок: aaaSAP HANA резервного копирования Azure на уровне файлов

Сводка. Это руководство содержит сведения об использовании резервного копирования SAP HANA на уровне файлов под управлением SAP HANA на виртуальных машинах Azure.

Обновление: март 2017 г.

[Это руководство можно найти здесь.](sap-hana-backup-storage-snapshots.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="sap-netweaver-deployed-on-azure-virtual-machines"></a>Развертывание SAP NetWeaver на виртуальных машинах Azure

### <a name="deploy-sap-ides-system-on-windows-and-sql-server-through-sap-cal-on-azure"></a>Развертывание системы SAP IDES в Windows и SQL Server c использованием клиентской лицензии SAP в Azure
Заголовок: aaaTesting SAP NetWeaver в ВМ Microsoft Azure SUSE Linux 

Сводка: В этом документе описываются hello развертывания системы SAP интегрированными средами разработки на основе Windows и SQL Server в Azure с помощью устройства библиотеки SAP облака. SAP облачному устройству библиотеки — это служба SAP, которая позволяет развертывать hello продуктов SAP в Azure. В этом документе шаг за шагом проходит через hello развертывания системы SAP интегрированными средами разработки. Hello интегрированными средами разработки системы приведено только для нескольких десятков приложений, развертываемых через облако SAP устройства в Microsoft Azure.

Обновление: июнь 2017 г.

[Это руководство можно найти здесь.](cal-ides-erp6-erp7-sp3-sql.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


### <a name="quickstart-guide-for-netweaver-on-suse-linux-on-azure"></a>Краткое руководство по NetWeaver под управлением SUSE Linux в Azure
Заголовок: aaaTesting SAP NetWeaver в ВМ Microsoft Azure SUSE Linux 

Сводка: Этой статье описываются различные tooconsider действия при работе с SAP NetWeaver на виртуальных машинах Microsoft Azure SUSE Linux (ВМ). SAP NetWeaver официально поддерживается на виртуальных машинах SUSE Linux в Azure. Все сведения о версиях Linux, версиях ядра SAP и другую информацию можно найти в примечании SAP 1928533 "Приложения SAP в Azure: поддерживаемые продукты и типы виртуальных машин Azure".

Последнее обновление: сентябрь 2016 г.

[Это руководство можно найти здесь.](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="3da0389e-708b-4e82-b2a2-e92f132df89c"></a>Планирование и реализация
Заголовок: aaaAzure виртуальных машин планированию и реализации для SAP NetWeaver

Сводка: Данный документ является toostart руководство hello с, если вы собираетесь использовать SAP NetWeaver на виртуальных машинах Azure. Данное руководство по планированию и реализации помогает определить существующие или запланированного на основе SAP NetWeaver система может быть tooan развернутой среды виртуальных машин Azure. Рассматривается несколько сценариев развертывания SAP NetWeaver, а также конфигурации, определенных tooAzure. Бумага Hello перечислены и описаны все hello необходимые данные о конфигурации вам hello toorun стороне SAP и Azure гибридной среды. Также описаны меры, вы сможете tooensure высокого уровня доступности систем SAP NetWeaver в IaaS.

Обновление: июнь 2017 г.

[Это руководство можно найти здесь.][planning-guide]

### <a name="high-availability-configurations-of-sap-netweaver-in-azure-vms"></a>Конфигурации высокой доступности SAP NetWeaver на виртуальных машинах Azure
Заголовок: aaaAzure виртуальных машин высокой доступности для SAP NetWeaver

Сводка: В этом документе мы рассмотрим hello действия, которые можно предпринять toodeploy высокого уровня доступности систем SAP в Azure с помощью модели развертывания диспетчера ресурсов Azure hello. Здесь рассматриваются эти основные задачи. В документе hello описаны компоненты как одной точки сбоя как расширенный бизнеса приложения программирования (ABAP) SAP центра служб (ASC) или центра служб SAP (SCS) и систем управления базами данных (СУБД) и избыточные компоненты, такие как SAP Сервер приложений будет toobe защищенных выполняющейся в виртуальных машинах Azure. В нем показаны пошаговые инструкции по установке и настройке системы SAP с высоким уровнем доступности в отказоустойчивом кластере Windows Server в Azure.

Обновление: июнь 2017 г.

[Это руководство можно найти здесь.](high-availability-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="realizing-multi-sid-deployments-of-sap-netweaver-in-azure-vms"></a>Реализация развертываний с несколькими идентификаторами безопасности SAP NetWeaver на виртуальных машинах Azure
Заголовок: aaaCreate конфигурации SAP NetWeaver multi-SID 

Сводка: Этот документ является документом toohello сложения высокого уровня доступности SAP NetWeaver на виртуальных машинах Azure. Из-за toonew функциональность в Azure, которая появилась в сентябре 2016 года это возможно toodeploy несколько ASCS NetWeaver SAP/SCS экземпляров в паре виртуальных машинах Azure. С такой конфигурации можно снизить hello количество виртуальных машин необходимые toodeploy toorealize высокодоступных конфигураций, SAP NetWeaver. Hello руководстве описаны hello Настройка таких конфигураций multi-SID.

Последнее обновление: декабрь 2016 г.

[Это руководство можно найти здесь.](high-availability-multi-sid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="6aadadd2-76b5-46d8-8713-e8d63630e955"></a>Развертывание SAP NetWeaver на виртуальных машинах Azure
Заголовок: aaaAzure развертывания виртуальных машин для SAP NetWeaver

Сводка: Этот документ содержит инструкции по развертыванию машин toovirtual программного обеспечения SAP NetWeaver в Azure. Данный документ фокусируется на трех сценария развертываниях с акцентом на активации расширений мониторинга hello Azure для SAP, включая рекомендации для hello расширений мониторинга Azure для SAP по устранению неполадок. В этом документе предполагается, что вы прочитали hello планирования и реализации руководства.

Обновление: июнь 2017 г.

[Это руководство можно найти здесь.][deployment-guide]

### <a name="1343ffe1-8021-4ce6-a08d-3a1553a4db82"></a>Руководство по развертыванию СУБД
Заголовок: aaaAzure развертывания виртуальных машин СУБД для SAP NetWeaver

Сводка: В этом документе рассматриваются вопросы планирования и реализации для hello СУБД, которые должны работать вместе с SAP. В первой части hello перечислены и представлены общие рекомендации. Hello следующие части бумаги hello связаны toodeployments различных DBMS в Azure, которые поддерживаются системами SAP. Описаны следующие СУБД: SQL Server, SAP ASE и Oracle. В этих отдельных частей обсуждаются вопросы, у вас есть tooaccount для при использовании систем SAP в Azure в сочетании с этими СУБД. Субъекты, например методы резервного копирования и высокий уровень доступности, поддерживаемые различными системами DBMS на Azure представлены для использования hello вместе с приложениями SAP приветствия.

Обновление: июнь 2017 г.

[Это руководство можно найти здесь.][dbms-guide]

### <a name="using-azure-site-recovery-for-sap-workload"></a>Использование Azure Site Recovery для рабочей нагрузки SAP
Заголовок: aaaSAP NetWeaver: построение решения аварийного восстановления с помощью Azure Site Recovery 

Сводка: В этом документе описывается способ hello, использование служб Azure Site Recovery hello с целью обработки сценариев аварийного восстановления. Варианты использования Azure в качестве расположения для аварийного восстановления для локальных ландшафтов SAP с помощью служб Azure Site Recovery. Еще один сценарий, описанный в документе hello: hello Aure в Azure (A2A) аварийного восстановления вариантов и управление с помощью Azure Site Recovery.  

Дата обновления: август 2017 г.

[Это руководство можно найти здесь.](http://aka.ms/asr-sap)

