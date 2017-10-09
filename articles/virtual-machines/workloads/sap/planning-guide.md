---
title: "Виртуальные машины aaaAzure планированию и реализации для SAP NetWeaver | Документы Microsoft"
description: "SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению"
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: d7c59cc1-b2d0-4d90-9126-628f9c7a5538
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d1e9fa13d847e4d8abb3c34fd352d1f4ece3717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-planning-and-implementation-for-sap-netweaver"></a>SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению
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

[azure-cli]:../../../cli-install-nodejs.md
[azure-portal]:https://portal.azure.com
[azure-ps]:/powershell/azureps-cmdlets-docs
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md#subscription-limits

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

[planning-guide]:planning-guide.md  
[planning-guide-1.2]:planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff
[planning-guide-11]:planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058
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
[planning-guide-figure-2500]:media/virtual-machines-shared-sap-planning-guide/planning-monitoring-overview-2502.png
[planning-guide-figure-2600]:media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-2901]:media/virtual-machines-shared-sap-planning-guide/2901-azure-ha-sap-ha-md.png
[planning-guide-figure-300]:media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-3201]:media/virtual-machines-shared-sap-planning-guide/3201-sap-ha-with-sql-md.png
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
[sap-pam]:https://support.sap.com/pam
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
[virtual-machines-linux-capture-image-resource-manager-capture]:../../linux/capture-image.md#step-2-capture-the-vm
[virtual-machines-windows-capture-image-resource-manager]:../../windows/capture-image.md
[virtual-machines-windows-capture-image]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-windows-capture-image-prepare-the-vm-for-image-capture]:../../virtual-machines-windows-generalize-vhd.md
[virtual-machines-linux-configure-raid]:../../linux/configure-raid.md
[virtual-machines-linux-configure-lvm]:../../linux/configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:../../virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:../../linux/suse-create-upload-vhd.md
[virtual-machines-linux-create-upload-vhd-oracle]:../../linux/oracle-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:../../linux/redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:../../linux/add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:../../linux/add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:../../linux/quick-create-cli.md
[virtual-machines-linux-update-agent]:../../linux/update-agent.md
[virtual-machines-manage-availability]:../../linux/manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-create-powershell.md
[virtual-machines-sizes-linux]:../../linux/sizes.md
[virtual-machines-sizes-windows]:../../windows/sizes.md
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
[virtual-networks-multiple-nics-windows]:../../windows/multiple-nics.md
[virtual-networks-multiple-nics-linux]:../../linux/multiple-nics.md
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
[capture-image-linux-step-2-create-vm-image]:../../linux/capture-image.md#step-2-create-vm-image

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Microsoft Azure позволяет компаниям tooacquire вычислительные ресурсы и хранилища в минимальными затратами времени без длительных процессов поставки. Виртуальные машины Azure позволяют компаниям toodeploy Классические приложения, как приложения в Azure на основе SAP NetWeaver и повышать их надежность и доступность, не привлекая дополнительные ресурсы доступны в локальной. Службы виртуальных машин Azure также поддерживает подключения между организациями, какие tooactively компаний позволяет интегрировать виртуальные машины Azure в свои локальные домены их частных облаков и свой ландшафт системы SAP.
В этом техническом документе описываются принципы работы hello из виртуальной машины Microsoft Azure и предоставляет подробно обсуждаются вопросы планирования и реализации для установок SAP NetWeaver в Azure и таким образом должен быть tooread hello документа перед началом фактическим развертываниям SAP NetWeaver в Azure.
Hello документ дополняет hello документацию по установке SAP и примечания по SAP, которые представляют Привет основные ресурсы для установки и развертывания программного обеспечения SAP в заданный платформы.

## <a name="summary"></a>Сводка
Облачные вычисления — это широко используемый термин, который приобретает все большее значение в пределах hello ИТ-индустрии, от малых компаний вверх toolarge транснациональных корпораций.

Microsoft Azure — hello платформа облачных служб Майкрософт, которая предлагает широкий спектр новых возможностей. Теперь клиенты — может toorapidly подготовки и Отмена подготовки приложения как служба в облаке hello так, чтобы они не только tootechnical или бюджетные ограничения. Вместо того чтобы тратить время и бюджет на аппаратную инфраструктуру, компании могут сосредоточить внимание на приложения hello, бизнес-процессов и его преимущества для клиентов и пользователей.

Корпорация Майкрософт предоставляет службы виртуальных машин Microsoft Azure как комплексную платформу «инфраструктура как услуга» (IaaS). Виртуальные машины Azure (IaaS) поддерживают приложения на основе SAP NetWeaver. В этом документе описывается, как tooplan и реализуйте SAP NetWeaver на основе приложений в Microsoft Azure как платформу hello по выбору.

Hello этом документе основное внимание уделяется два основных аспекта:

* Первая часть Hello описывает две модели развертывания для приложений на основе SAP NetWeaver в Azure. Также в ней описываются общие процессы управления Azure и их специфика для развертываний SAP.
* Hello второй части Подробные сведения о реализации hello два разных сценария, описанных в первой части hello.

Дополнительные ресурсы перечислены в этой статье в разделе [Ресурсы][planning-guide-1.2].

### <a name="definitions-upfront"></a>Определения
В документе hello мы используем hello следующими условиями:

* IaaS: инфраструктура как услуга.
* PaaS: платформа как услуга.
* SaaS: программное обеспечение как услуга.
* ARM: Azure Resource Manager.
* Компонент SAP: отдельное приложение SAP, например ECC, BW, Solution Manager или EP.  Компоненты SAP могут основываться на традиционной технологии ABAP или Java или быть приложениями не на основе NetWeaver, например бизнес-объектами.
* Среда SAP: один или несколько компонентов SAP логически сгруппированы tooperform бизнес-функцию, например разработки, QAS, обучение, DR или производства.
* Ландшафт SAP: Ссылается toohello все ресурсы SAP в клиента ИТ-инфраструктуре. Hello ландшафт SAP включает все рабочие и непроизводственных средах.
* Система SAP: hello сочетание уровень СУБД и уровня приложений, например, система разработки SAP ERP, тестовая система SAP BW, производственная система SAP CRM и т. д. В развертываниях Azure, не поддерживаемые toodivide этих двух уровней между локальной средой и Azure. Таким образом, система SAP должна быть развернута полностью в локальной среде или полностью в Azure. Тем не менее можно развернуть hello различных системах ландшафта SAP в Azure или локально. Например вы развертывание hello SAP CRM разработки и тестирования системы в Azure, но hello SAP CRM рабочей системы в локальной среде.
* Развертывание только в облаке: развертывания, где hello подписка Azure не подключен через сайт сайт или ExpressRoute подключения toohello локальной сетевой инфраструктуре. В документации Azure развертывания такого рода традиционно называются полностью облачными. Виртуальные машины, развернутые с помощью этого метода осуществляется через Интернет hello и общедоступный IP-адрес и/или публичного DNS-сервера имя назначенного toohello ВМ в Azure. Для Microsoft Windows hello в локальной среде Active Directory (AD) и DNS не будет продлен tooAzure в этих типах развертываний. Поэтому виртуальные машины hello не являются частью hello в локальной Active Directory. Это же справедливо и для реализаций Linux с использованием OpenLDAP + Kerberos и т. п.

> [!NOTE]
> В этом документе под полностью облачным развертыванием понимается полный ландшафт SAP. Такое развертывание работает только в Azure без распространения службы Active Directory (OpenLDAP) или службы разрешения имен из локальной сети в общедоступное облако. Только для облака конфигурации не поддерживаются для производственных систем SAP или где SAP STMS или других локальных ресурсов должны toobe обмена данными между систем SAP, размещенных в Azure и ресурсам, расположенным в локальной конфигурации.
>
>

* Между организациями: Описан сценарий, где виртуальные машины, развернутой tooan подписке Azure с сайт сайт, несколькими сайтами или подключение ExpressRoute между центрами обработки данных в локальной среде hello и Azure. В документации Azure развертывания такого рода также называются распределенными развертываниями. Hello подключения hello обусловлено tooextend локальным доменам в локальной среде Active Directory или OpenLDAP и локальных DNS в Azure. Hello локальной альбомная — расширенные toohello активов Azure hello подписки. При таком расширении hello виртуальных машин может быть частью локального домена hello. Пользователи домена hello локального домена имеют доступ к серверам hello и могут запускать службы на их виртуальных машин (как службы СУБД). Возможно взаимодействие и разрешение имен между виртуальными машинами, развернутыми в локальной сети и в Azure. Это сценарий hello, предполагается, что большинство toobe активы SAP развернутых в. Дополнительные сведения см. в [этой][vpn-gateway-cross-premises-options] и [этой][vpn-gateway-site-to-site-create] статьях.

> [!NOTE]
> Для рабочих систем SAP поддерживаются распределенные развертывания систем SAP, в которых системы SAP выполняются на виртуальных машинах Azure, являющихся членами локального домена. Распределенная конфигурация предполагает развертывание в Azure полного ландшафта SAP или его частей. Даже выполнение hello завершения ландшафт SAP в Azure, необходимо иметь этих виртуальных машин, не входит в состав локальному домену и РЕКЛАМЫ и OpenLDAP. Прежние версии документации hello мы говорили о сценариях гибридной ИТ-корневым hello термин «Гибридный» hello факт, что между сетями, между локальными и Azure. Кроме того, hello факт, что hello ВМ в Azure являются частью hello в локальной Active Directory или OpenLDAP.
>
>

В некоторой документации Майкрософт сценарии распределенного подключения описываются иначе. В частности, это касается высокодоступных конфигураций СУБД. В случае hello документов, связанных с SAP hello hello межсетевых локальных ресурсах просто сводится toohaving сайт сайт или private (ExpressRoute) подключения и hello факт что hello ландшафт SAP распределяется между локальной средой и Azure.  

### <a name="e55d1e22-c2c8-460b-9897-64622a34fdff"></a>Ресурсы
Hello следующих дополнительных руководствах рассматриваются темы hello развертываний SAP в Azure.

* [SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению (этот документ)][planning-guide]
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию][deployment-guide]
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]

> [!IMPORTANT]
> Везде, где применяется возможные toohello связи, ссылающиеся на руководство по установке SAP (Reference InstGuide-01, в разделе <http://service.sap.com/instguides>). Когда дело доходит toohello предварительные требования и процесс установки, руководства по установке NetWeaver SAP hello следует всегда внимательно читайте, как в этом документе рассматриваются только особые задачи для системы SAP NetWeaver, установленные на виртуальной машине Microsoft Azure.
>
>

следующие примечания по SAP Hello приведены связанные toohello тема SAP в Azure.

| Номер примечания | Название |
| --- | --- |
| [1928533] |Приложения SAP в Azure: поддерживаемые продукты и размеры |
| [2015553] |SAP в Microsoft Azure: требования |
| [1999351] |Устранение неполадок, связанных с расширенным мониторингом Azure для SAP |
| [2178632] |Ключевые метрики мониторинга для SAP в Microsoft Azure |
| [1409604] |Виртуализация в Windows: расширенный мониторинг |
| [2191498] |SAP на платформе Linux в Azure: расширенный мониторинг |
| [2243692] |Linux на виртуальной машине Microsoft Azure (IaaS): проблемы с лицензированием SAP |
| [1984787] |SUSE LINUX Enterprise Server 12: примечания к установке |
| [2002167] |Red Hat Enterprise Linux 7.x: установка и обновление |
| [2069760] |Установка и обновление Oracle Linux 7.x SAP |
| [1597355] |Рекомендация по области буфера для Linux |

Также считывать hello [SCN вики-сайте](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) , содержащий все примечания SAP для Linux.

Общие ограничения по умолчанию и максимальные ограничения для подписок Azure можно найти в [этой статье][azure-subscription-service-limits-subscription].

## <a name="possible-scenarios"></a>Возможные сценарии
SAP часто рассматривается как один из hello критически важных приложений в предприятиях. Архитектура Hello и операции таких приложений чаще всего являются очень сложными и гарантирует, что требования к доступности и производительности важна.

Таким образом, предприятия имеют toothink тщательно о том, какие приложения могут выполняться в среде общедоступного облака, независимо от выбранного hello поставщика облачных.

Ниже перечислены возможные типы систем для развертывания приложений на основе SAP NetWeaver в среде общедоступного облака.

1. Рабочие системы среднего размера.
2. Системы для разработки.
3. Тестовые системы.
4. Системы-прототипы.
5. Обучающие и демонстрационные системы.

В порядке toosuccessfully развертывания систем SAP в Azure IaaS или IaaS в целом, очень важно toounderstand hello значительные различия hello предложения из обычных аутсорсеров или хостеров и предложениями IaaS. В то время как hello обычный хостер или аутсорсер адаптирует рабочей нагрузки toohello (тип сети, хранилища и сервер) инфраструктуры клиенту toohost, вместо этого клиента hello ответственности toochoose hello правильной рабочей нагрузки развертываниях IaaS.

В качестве первого шага клиенты должны hello tooverify следующих элементов:

* Hello SAP поддерживаемые типы ВМ
* Hello SAP продукты или выпуски поддерживается в Azure
* Hello поддерживаемые выпуски ОС и СУБД для конкретных выпусков SAP в Azure приветствия
* пропускная способность SAP, предоставляемая разными SKU Azure.

Hello ответы toothese вопросы можно прочитать в примечании SAP [1928533].

В качестве второго шага Azure ограничения ресурсов и пропускной способности должны потребления ресурсов по сравнению toobe tooactual локальных систем. Таким образом клиенты необходимость toobe представление hello различных возможностях hello Azure типы с поддержкой SAP hello области:

* ресурсы ЦП и памяти для разных типов виртуальных машин;
* пропускная способность операций ввода-вывода для разных типов виртуальных машин;
* сетевые возможности для разных типов виртуальных машин.

Большую часть этих данных можно найти [здесь (Linux)][virtual-machines-sizes-linux] и [здесь (Windows)][virtual-machines-sizes-windows].

Имейте в виду, что hello ограничениями, перечисленными в hello ссылку выше, верхних пределов. Это означает, что hello ограничения для hello ресурсам, например операций ввода-ВЫВОДА могут быть предоставлены ни при каких обстоятельствах. Хотя исключения Hello эти ресурсы ЦП и памяти hello типа выбранной виртуальной Машины. Hello типов ВМ, поддерживаемых SAP ресурсы ЦП и памяти hello: зарезервированные и таким образом, доступные в любой момент времени для потребления в ВМ hello.

Hello платформы Microsoft Azure, как другие платформы IaaS — это платформа для нескольких клиентов. Это означает, что хранилище, сеть и другие ресурсы совместно используются несколькими клиентами. Интеллектуальная регулирование и логика — клиент tooprevent используется один из в квотирования, влияющие на производительность другого клиента (шумный сосед) hello. Хотя логика в Azure пытается tookeep отклонения пропускной маленькие, высокой общей платформы, как правило, toointroduce больших отклонений в доступности ресурсов и пропускной способности, чем многие клиенты являются используется tooin их развертывания в локальной среде. В результате могут наблюдаться разные уровни пропускной способности по сети или ввода-вывода (hello тома а также задержка) хранилища из toominute минуты. Hello вероятность, что система SAP в Azure может испытывать большие отклонения, чем в локальной системе необходимо принимать во внимание toobe.

Последний шаг — tooevaluate требования к доступности. Это может произойти, hello базовой инфраструктуры Azure tooget обновлены и узлы hello выполнение перезагрузки toobe виртуальных машин. В этих случаях виртуальные машины, размещенные на этих узлах, также завершают работу и перезапускаются. Hello времени такое обслуживание выполняется в рабочее время вспомогательные для конкретного региона, но потенциальное окно hello в несколько часов в течение которого происходит перезапуск, довольно велико. Существуют различные технологии в hello платформы Azure, который может быть настроен toomitigate некоторые или все hello влияние таких обновлений. Будущих улучшений hello платформы Azure, СУБД и приложения SAP, разработанные toominimize hello влияние таких перезагрузок.

В порядке toosuccessfully развертывания системы SAP в Azure, hello локальной системы SAP операционной системы базы данных, и приложения SAP должны располагаться на hello Azure SAP может предоставить Матрица поддержки, размерам hello hello ресурсы инфраструктуры Azure и что можно работать с доступности соглашения об уровне обслуживания Microsoft Azure предлагает приветствия. Определения этих систем необходимо toodecide на одном из следующих двух сценариях развертывания hello.

### <a name="1625df66-4cc6-4d60-9202-de8a0b77f803"></a>Только для облака — развертывания виртуальных машин в Azure без зависимостей от hello в локальной сети клиента
![Одна виртуальная машина с демонстрационной версией SAP или обучающим сценарием, развернутая в Azure][planning-guide-figure-100]

Этот сценарий является типичным для обучающих или демонстрационных систем, где все компоненты hello SAP и прочее по устанавливаются в одной виртуальной Машины. В этом сценарии развертывания не поддерживаются производственные системы SAP. Как правило этот сценарий соответствует hello следующие требования:

* виртуальные машины Hello сами доступны по публичной сети hello. Прямое сетевое соединение hello приложения, запущенные в toohello hello виртуальными машинами в локальной сети либо hello компании, которой принадлежит hello демонстрации или обучения содержимого или hello клиента не требуется.
* В случае нескольких виртуальных машин, представляющий сценарий hello обучения или демонстрации сетевого подключения и разрешение имен должен toowork между виртуальными машинами hello. Но обмена данными между hello набор виртуальных машин должны toobe изолированной, чтобы несколько наборов ВМ можно развернуть рядом друг с другом без помех.  
* Подключение к Интернету является обязательным для hello конечного пользователя tooremote входа в toohello, размещенных виртуальных машин в Azure. В зависимости от hello гостевой ОС, используется служб терминалов и RDS или VNC/ssh tooeither ВМ hello tooaccess выполнения задач обучения hello или выполнять демонстрации hello. Если порты SAP, например 3200 3300 & 3600 также hello экземпляр приложения SAP может осуществляться из любого подключенного рабочего Интернета.
* Здравствуйте, системы SAP (и VM(s)) представляют изолированный сценарий в Azure, который только требует открытого подключения к Интернету для доступа к конечным пользователем и не требует tooother подключение виртуальных машин в Azure.
* SAPGUI и браузер устанавливаются и работают непосредственно на hello виртуальной Машины.
* Требуется быстрого сброса ВМ toohello исходное состояние и нового развертывания этого исходного состояния еще раз.
* В случае hello Демонстрация и сценариев обучения, который реализуются в нескольких виртуальных машин, Active Directory / OpenLDAP/или служба DNS является обязательным для каждого набора виртуальных машин.

![Группа виртуальных машин в облачной службе Azure для демонстрационных или обучающих целей][planning-guide-figure-200]

Очень важно tookeep помните, что hello виртуальные машины в каждом hello наборы toobe необходимости разворачивать параллельно, где приветствия имен виртуальных Машин в каждом наборе hello являются одинаковыми hello.

### <a name="f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10"></a>Между организациями - развертывание одной или нескольких ВМ SAP в Azure с требованием hello полной интеграции с локальной сетью hello
![VPN-подключение типа "сеть — сеть" (распределенное подключение)][planning-guide-figure-300]

Этот сценарий является распределенным и допускает множество моделей развертывания. Это может быть просто описано, как при запуске некоторые части hello SAP альбомная локальной и другие части hello ландшафт SAP в Azure. Все аспекты hello факт, что часть компонентов SAP hello работает в Azure должны быть прозрачными для конечных пользователей. Поэтому Здравствуйте SAP транспорта Correction System (STMS), взаимодействие с RFC, печать, безопасность (например SSO), т. д. без проблем работать для hello систем SAP в Azure. Но hello межсетевых локальных ресурсах также описан сценарий, где работает hello завершения ландшафт SAP в Azure с доменом клиента hello и DNS расширяются до Azure.

> [!NOTE]
> Это сценарий развертывания hello, поддерживаемый для производственных систем SAP.
>
>

Чтение [в этой статье] [ vpn-gateway-create-site-to-site-rm-powershell] Дополнительные сведения о том, как tooconnect в локальной сети tooMicrosoft Azure

> [!IMPORTANT]
> Когда мы говорим о сценариях распределенной между Azure и локальных клиентских развертываний, мы ищем hello гранулярность системы SAP в целом. Ниже перечислены сценарии, которые *не поддерживаются* для распределенного развертывания.
>
> * Выполнение различных уровней приложений SAP с помощью различных методов развертывания. Например выполнение hello СУБД слоя в локальной среде, но hello уровня приложения SAP в виртуальных машин, развернутых как ВМ Azure, или наоборот.
> * Размещение некоторых компонентов одного уровня SAP в Azure, а других — в локальной среде. Например, разделение экземпляров уровня приложения hello SAP между локальной и виртуальных машинах Azure.
> * Не поддерживается распределение виртуальных машин, выполняющих экземпляры одной системы SAP, на несколько регионов Azure.
>
> Причиной этих ограничений Hello — требование hello очень низкой задержкой сети высокой производительности в одной системе, особенно между экземплярами приложений hello и hello уровнем СУБД системы SAP.
>
>

### <a name="supported-os-and-database-releases"></a>Поддерживаемые ОС и версии базы данных
* Серверное программное обеспечение Майкрософт, которое поддерживается для служб виртуальных машин Azure, перечислено в этой статье: <http://support.microsoft.com/kb/2721672>.
* Выпуски операционной системы и системы баз данных, которые поддерживаются службами виртуальных машин Azure в сочетании с программным обеспечением SAP, описаны в примечании к SAP [1928533].
* Приложения и выпуски SAP, поддерживаемые службами виртуальных машин Azure, описаны в примечании к SAP [1928533].
* Только 64-разрядные образы, которые являются toorun поддерживаемые гостевые виртуальные машины в Azure для сценариев SAP. Это также означает, что поддерживаются только 64-разрядные приложения SAP и базы данных.

## <a name="microsoft-azure-virtual-machine-services"></a>Службы виртуальных машин Microsoft Azure
Платформа Microsoft Azure Hello — в облаке масштабируемая Интернет-платформа служб размещается и функционирует в Microsoft данные центров. Hello платформа включает службы виртуальных машин Microsoft Azure hello (инфраструктуру как услугу или IaaS) и набор многофункциональную платформу как возможности службы (PaaS).

Hello платформы Azure уменьшает hello потребность в предварительных закупках технологий и инфраструктуры. Оно упрощает обслуживание и эксплуатацию приложений, предоставляя toohost вычислений и хранения по требованию, масштабирование и управление веб-приложения и подключенных приложений. Управление инфраструктурой автоматизировано, и платформа, которая предназначена для обеспечения высокой доступности и динамического масштабирования toomatch с потребностями hello вариант оплаты по мере использования модель ценообразования.

![Позиционирование служб виртуальных машин Microsoft Azure][planning-guide-figure-400]

Службах виртуальной машины Azure Майкрософт позволяет вы tooAzure изображения toodeploy пользовательского сервера как экземпляры IaaS (см. рис. 4). Hello виртуальных машин в Azure основаны на виртуальные жесткие диски Hyper-V (VHD) и не может toorun разных операционных систем в качестве гостевой ОС.

С точки зрения эксплуатации службы виртуальных машин Azure предоставляет аналогичные приветствия возникает как виртуальных машин, развернутых на локальном компьютере. Однако он имеет значительное преимущество hello ненужные tooprocure, администрирования и управления инфраструктурой hello. Разработчики и Администраторы имеют полный контроль над hello образ операционной системы в течение этих виртуальных машин. Администраторы могут войти на удаленный toothose виртуальные машины tooperform обслуживание и устранение неполадок задач, а также задачи по развертыванию программного обеспечения. В toodeployment учета hello ограничиваются только размеры hello и возможности ВМ Azure. Но эти ограничения не всегда можно будет настроить так же точно, как в локальной среде. Есть несколько типов виртуальных машин, каждый из которых имеет определенное сочетание следующих параметров:

* количество виртуальных ЦП;
* память;
* количество подключаемых виртуальных жестких дисков;
* пропускная способность сети и хранилища.

размер Hello и ограничения различных размеров разных виртуальных машин предлагаемых можно увидеть в таблице в [в этой статье (Linux)] [ virtual-machines-sizes-linux] и [в этой статье (Windows)] [ virtual-machines-sizes-windows].

Как вы можете заметить, есть несколько семейств (серий) виртуальных машин. Позволяет отличать hello следующие семейства виртуальных машин:

* Типы виртуальных машин A0–A7: не все из них сертифицированы для использования с SAP. Это первая серия виртуальных машин, представленная при появлении Azure IaaS.
* Типы виртуальных машин A8–A11: высокопроизводительные вычислительные экземпляры. Они выполняются на более мощных вычислительных узлах, чем другие виртуальные машины серии A.
* Типы виртуальных машин серии D/Dv2D: производительность выше, чем у серии A0-A7. Не все типы ВМ hello сертифицированные с SAP.
* Типов ВМ серии DS и серии DSv2: аналогичные tooD/Dv2-series, возникают возможности tooconnect tooAzure хранилище Premium (в главе [хранилища Azure Premium] [ planning-guide-3.3.2] этого документа). Также не все типы сертифицированы для использования с SAP.
* Типы виртуальных машин серии G: это типы виртуальных машин с большим объемом памяти.
* Типов ВМ серии GS: как серия G, но включая toouse параметр hello хранилища Azure Premium (в главе [хранилища Azure Premium] [ planning-guide-3.3.2] этого документа). При использовании виртуальных машин серии GS как серверы баз данных, он является обязательным toouse хранилище Premium для DB данных и файлы журнала транзакций

Может оказаться hello и те же конфигурации ЦП и памяти, в другую серию виртуальных Машин. Тем не менее при поиске производительность и пропускную способность hello этих виртуальных машин из разных рядов hello может существенно отличаются. Здравствуйте, одинаково вне зависимости от конфигурации ЦП и памяти. Причиной является то, что базовое оборудование сервера узла hello во введении hello hello разных типов ВМ имели характеристики разных пропускной способности.  Обычно различие hello, показанный на производительность и пропускную способность также отражаются в цены hello hello разных ВМ.

Не все другую серию виртуальных Машин могут быть предложены в каждом из них hello регионов Azure (для следующей главе регионы Azure см. в разделе). Также не забывайте, что не все виртуальные машины и не все серии виртуальных машин сертифицированы для использования с SAP.

> [!IMPORTANT]
> Для использования hello приложений на основе SAP NetWeaver, только hello подмножество типов виртуальных Машин и конфигураций, перечисленные в примечании SAP [1928533] поддерживаются.
>
>

### <a name="be80d1b9-a463-4845-bd35-f4cebdb5424a"></a>Регионы Azure
Корпорация Майкрософт разрешает toodeploy виртуальных машин в так называемых «регионы Azure». Регион Azure включает один или несколько близко расположенных центров обработки данных. Для большинства hello геополитических регионов в Здравствуй, мир Microsoft имеет по крайней мере двух регионах Azure. К примеру, в Европе есть регионы Azure "Северная Европа" и "Западная Европа". Такие двух регионах Azure в области геополитические разделяются достаточной расстояние, естественных или технических аварий не влияет на обе области Azure в hello геополитические совпадают. Поскольку Microsoft стабильно создает новый Azure областей в разных регионах геополитические глобально, hello числа этих регионов неуклонно растет и на момент декабря 2015 достигнуто hello число 20 регионы Azure с помощью дополнительных областей уже было объявлено. Как клиент можно развернуть систем SAP в этих областях, включая hello двух регионов Azure в Китае. Актуальные сведения о регионах Azure доступны на этом веб-сайте: <https://azure.microsoft.com/regions/>.

### <a name="8d8ad4b8-6093-4b91-ac36-ea56d80dbf77"></a>Hello понятие виртуальной машины Microsoft Azure
Microsoft Azure предлагает инфраструктуры как услуги (IaaS) решения toohost виртуальные машины с той же функциональностью в качестве локального решения виртуализации. Возможности виртуальных машин из toocreate внутри hello портал Azure, PowerShell или интерфейс командной строки, которые также предоставляют возможности управления и развертывания.

Диспетчер ресурсов Azure можно tooprovision приложений с помощью декларативного шаблона. В одном шаблоне можно развернуть несколько служб и их зависимые компоненты. Использовать hello же toorepeatedly шаблона развертывания приложения на каждом этапе жизненного цикла приложения hello.

Дополнительные сведения об использовании шаблонов Resource Manager см. здесь:

* [Развертывание и управление виртуальными машинами с помощью шаблонов диспетчера ресурсов Azure и Azure CLI hello] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Управление виртуальными машинами с помощью Azure Resource Manager и PowerShell][virtual-machines-deploy-rmtemplates-powershell]
* <https://azure.microsoft.com/documentation/templates/>

Другой интересной функцией является hello возможность toocreate образов из виртуальных машин, что позволяет tooprepare определенные репозитории, из которых являются может tooquickly развертывание экземпляров виртуальных машин, которые соответствуют вашим требованиям.

Дополнительные сведения о создании образов виртуальных машин можно найти в [этой][virtual-machines-linux-capture-image-resource-manager] (Linux) или [этой статье][virtual-machines-windows-capture-image-resource-manager] (Windows).

#### <a name="df49dc09-141b-4f34-a4a2-990913b30358"></a>Домены сбоя
Домены сбоя представляют физическую единицу сбоя, очень близкие toohello физической инфраструктурой в центрах обработки данных, и хотя физически блок или плата может считаться доменом сбоя, имеется нет прямого однозначного соответствия между двумя hello.

При развертывании нескольких виртуальных машин в рамках одной системы SAP в службах виртуальных машин Microsoft Azure, вы можете влиять hello Azure Fabric Controller toodeploy приложения в других доменах сбоя, удовлетворяя требованиям hello hello Соглашения об уровне ОБСЛУЖИВАНИЯ Microsoft Azure. Однако hello распределение доменов сбоя по единице масштабирования Azure (коллекция сотни вычислительные узлы или узлы хранилища и сети) или назначение hello tooa ВМ конкретному домену сбоя стоит по которому у вас прямого управления. Контроллер структуры Azure toodeploy набор виртуальных машин по разным доменам сбоя порядок toodirect hello нужен tooassign toohello группе доступности Azure виртуальные машины во время развертывания. Дополнительные сведения о группах доступности Azure содержатся в разделе этого документа о [группах доступности Azure][planning-guide-3.2.3].

#### <a name="fc1ac8b2-e54a-487c-8581-d3cc6625e560"></a>Домены обновления
Домены обновления представляют логическую единицу, помогающую обновление виртуальной Машины в систему SAP, которая состоит из экземпляров SAP, работающих в несколько виртуальных машин, toodetermine. Когда происходит обновление, Microsoft Azure проходит через hello процесс обновления этих доменов последовательно один за другим. Если вы во время развертывания распределите виртуальные машины по разным доменам обновления, это частично защитит систему SAP от потенциального простоя. В заказ tooforce Azure toodeploy hello ВМ системы SAP по разным доменам обновления, необходимо tooset конкретного атрибута во время развертывания каждой виртуальной машины. Аналогичные tooFault домены, в единицу масштабирования Azure состоит из нескольких доменов обновления. Контроллер структуры Azure toodeploy набор виртуальных машин по разным доменам обновления заказа toodirect hello нужен tooassign toohello группе доступности Azure виртуальные машины во время развертывания. Дополнительные сведения о группах доступности Azure содержатся ниже в разделе о [группах доступности Azure][planning-guide-3.2.3].

#### <a name="18810088-f9be-4c97-958a-27996255c665"></a>Группы доступности Azure
Виртуальные машины Azure в одной группе доступности Azure распространяются с hello Azure Fabric Controller по разным сбоя и домены обновления. Hello hello распределения по разным сбоя и домены обновления служит tooprevent всех ВМ системы SAP из процесса завершения работы в случае hello обслуживания инфраструктуры или сбоя в одном домене сбоя. По умолчанию виртуальные машины не входят в группу доступности. Hello участие ВМ в группе доступности определяется во время развертывания или позднее, путем перенастройки и повторного развертывания виртуальной машины.

Концепция hello toounderstand группы доступности Azure и hello, группы доступности связаны tooFault и домены обновления, как прочитать [в данной статье][virtual-machines-manage-availability]

Задает доступность toodefine для ARM через шаблон json см. раздел [hello спецификации rest api](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2015-06-15/swagger/compute.json) и выполните поиск «доступности».

### <a name="a72afa26-4bf4-4a25-8cf7-855d6032157f"></a>Хранилище. Служба хранилища Microsoft Azure и диски данных
Виртуальные машины Microsoft Azure используют хранилища разных типов. При реализации SAP в службах виртуальных машин Azure, очень важно toounderstand hello различия между двумя основными типами хранилища:

* непостоянное (временное) хранилище;
* постоянное хранилище.

хранилище непостоянные Hello непосредственно подключенного toohello работающих виртуальных машин и находится на hello самих вычислительных узлах — хранилище локального экземпляра hello (временные хранилища). размер Hello зависит от размера виртуальной машины, выбранной при запуске развертывания hello hello hello. Этот тип хранилища является временным и поэтому hello диск инициализируется при перезапуске экземпляра виртуальной машины. Как правило файл подкачки hello hello операционной системы находится на этом временном диске.

- - -
> ![Windows][Logo_Windows] Windows
>
> На виртуальных машинах Windows hello временный диск подключается как диск D:\ в развернутой виртуальной Машины.
>
> ![Linux][Logo_Linux] Linux
>
> На виртуальных машинах Linux диск подключается как /mnt/resource или /mnt. Дополнительные сведения см. здесь:
>
> * [Как tooAttach tooa диска данных виртуальной машины Linux][virtual-machines-linux-how-to-attach-disk]
> * <https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux#temporary-disk>
>
>

- - -
Hello фактический диск является энергозависимым, поскольку оно хранится на самом сервере узла hello. Если hello ВМ направляется на повторное развертывание (например из-за toomaintenance на узле hello или выключение и перезагрузка) содержимое hello hello диска теряется. Таким образом, это не параметр toostore всех важных данных на этом диске. Hello используемого носителя для этого типа хранилища отличается от другую серию виртуальных Машин с очень разными характеристиками производительности которых начиная с июня 2015 выглядеть следующим образом:

* A5–A7: крайне ограниченная производительность. Не рекомендуется использовать для любых целей, кроме файла подкачки.
* A8–A11: очень хорошая производительность на уровне 10 тыс. операций ввода-вывода в секунду и более 1 ГБ/с пропускной способности.
* Серия D: очень хорошая производительность на уровне 10 тыс. операций ввода-вывода в секунду и более 1 ГБ/с пропускной способности.
* Серия DS: очень хорошая производительность на уровне 10 тыс. операций ввода-вывода в секунду и более 1 ГБ/с пропускной способности.
* Серия G: очень хорошая производительность на уровне 10 тыс. операций ввода-вывода в секунду и более 1 ГБ/с пропускной способности.
* Серия GS: очень хорошая производительность на уровне 10 тыс. операций ввода-вывода в секунду и более 1 ГБ/с пропускной способности.

Выше инструкции применяются toohello типов ВМ, сертифицированные с SAP. для некоторых компонентов СУБД используйте подлежат Hello Серия виртуальных Машин с отличным операций ввода-ВЫВОДА и пропускной способности. Дополнительные сведения см. в разделе hello [руководство по развертыванию СУБД][dbms-guide].

Хранилище Microsoft Azure предоставляет материализованного хранилища и hello типичные уровни защиты и избыточности видеть в хранилище SAN. Диски, на основе хранилища Azure — это виртуальный жесткий диск (VHD) в службах хранилища Azure hello. Hello локальный диск ОС (Windows C:\, Linux/dev/sda1) хранится на hello хранилища Azure и дополнительные тома/диски, подключенные toohello виртуальная машина получить, тоже хранятся там.

Он возможных tooupload существующий VHD из локальной или создать пустые контейнеры в Azure и присоединения этих toodeployed виртуальных машин.

После создания или отправки виртуального жесткого диска в хранилище Azure, она возможных toomount и присоединить эти tooan существующей виртуальной машины и toocopy существующий VHD (отключены).

Эти виртуальные жесткие диски являются постоянными, то есть данные и изменения на них безопасно сохраняются при повторных загрузке и создании экземпляра виртуальной машины. Даже при удалении экземпляра эти VHD остаются в безопасности и могут быть повторно развернуты в случае диски без операционной системы можно также tooother подключенных виртуальных машин.

В рамках hello настройки сети уровней различных избыточности хранилища Azure:

* Минимальный уровень, который может быть выбран имеет значение «локальный избыточность» это эквивалент toothree реплики данных hello в hello одного центра обработки данных региона Azure (в главе [регионы Azure][planning-guide-3.1]).
* Зоны избыточное хранилище, изображения, hello трех распространяются через разных центрах обработки данных в пределах hello же регионе Azure.
* Уровень избыточности по умолчанию — географическую избыточность, которая асинхронно реплицирует hello содержимое в другой три изображения hello данных в другой регион Azure, которая размещается в hello геополитические совпадают.

См. также hello таблицу поверх относительно hello избыточности различные параметры в этой статье: <https://azure.microsoft.com/pricing/details/storage/>

Дополнительные сведения о службе хранилища Azure:

* <https://azure.microsoft.com/documentation/services/storage/>
* <https://azure.microsoft.com/services/site-recovery>
* <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>
* <https://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview.aspx>

#### <a name="azure-standard-storage"></a>Служба хранилища Azure класса Standard
Стандартная хранилища Azure была hello тип хранилища, доступный во время выпуска Azure IaaS. Для каждого диска применялись квоты на число операций ввода-вывода в секунду. Задержка возникла не hello же класс как SAN и NAS-устройства обычно развертывается для мощных систем SAP размещается локально. Тем не менее, hello оказался достаточно для сотен стандартное хранилище Azure систем SAP, в то же время развертывания в Azure.

Диски, которые хранятся на стандартных учетных записей хранилища Azure взимается основании hello фактические данные, хранящиеся, тома hello транзакции с хранилищем, исходящую передачу данных и избыточности с параметром, выбранным. Много дисков могут быть созданы на hello максимум 1 ТБ, но при условии, что эти оставаться пустым является бесплатной. Если затем вы указываете один виртуальный жесткий ДИСК с 100 ГБ, взимается плата для хранения 100 ГБ, а не для hello номинальный размер приветствия создан VHD с.

#### <a name="ff5ad0f9-f7f4-4022-9102-af07aef3bc92"></a>Хранилище Azure уровня "Премиум"
В апреле 2015 г. корпорация Майкрософт представила службу хранилища Azure класса Premium. Хранилище Premium появилась с целью tooprovide hello:

* снижение задержки при операциях ввода-вывода;
* более высокую пропускную способность;
* меньший разброс значений задержки при операциях ввода-вывода.

Для этой цели ряд изменений какие hello две наиболее значимые являются:

* Использование дисков SSD в узлах службы хранилища Azure hello
* Новый кэша чтения, поддерживаемый hello локальный SSD вычислительный узел Azure

В обратном tooStandard хранилище, где не изменился, возможности зависят от размера hello hello диск (или VHD), хранилище Premium в настоящее время имеет три категории другой диск, которые отображаются в этой статье: <https://azure.microsoft.com/ цены и сведения / / неуправляемого дисков или>

Вы видите, зависят от категории hello размера дисков hello пропускная способность операций ввода-ВЫВОДА или диска и диска или диск

Базовая себестоимость в случае hello хранилища Premium не hello фактические данные тома, хранящегося в таких дисков, но категорию размера hello такого диска, независимо от объема hello hello данные, хранящиеся в пределах hello диска.

Можно также создавать диски хранилища Premium, сопоставление не производится непосредственно на категории размер hello показано. Это может быть случай hello, особенно в том случае, если копирование дисков из стандартного хранилища в хранилище Premium. В таких случаях сопоставления toohello следующего наибольшего хранилище Premium диска параметра выполняется.

Имейте в виду, что только определенные Серия виртуальных Машин можно воспользоваться преимуществами hello хранилища Azure Premium. Начиная с декабря 2015 г. это hello и GS-серии DS. Hello серии DS является по сути hello же, как серии D с исключением hello, что серии DS имеет возможность hello toomount хранилище Premium на основе виртуальных машин Дополнительно toodisks, которые размещаются в стандартном хранилище Azure. Же является допустимым для серии tooGS серии G по сравнению.

Если вы извлекаете hello часть ВМ серии DS hello в [в этой статье (Linux)] [ virtual-machines-sizes-linux] и [в этой статье (Windows)][virtual-machines-sizes-windows], вы поймете, Нет тома ограничения tooPremium хранения диски с данными hello гранулярность hello уровня виртуальной Машины. Разные серии DS или виртуальные машины серии GS также имеют различные ограничения в отношении toohello число дисков данных, которые могут быть подключены. Эти ограничения описаны в статье hello, упомянутых выше, а также. Но по сути это означает, что если, например, подключить 32 tooa x P30 дисков одной виртуальной Машины DS14 можно не получить 32 x hello максимальной пропускной способности диска P30. Вместо этого hello максимальной пропускной способности на уровне ВМ задокументированного hello статьи ограничения пропускной способности.

Дополнительные сведения о хранилище класса Premium можно найти здесь: <http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2>

#### <a name="c55b2c6e-3ca1-4476-be16-16c81927550f"></a>Управляемые диски
Управляемые диски — это ресурс нового типа в Azure Resource Manager, который можно использовать вместо виртуальных жестких дисков, хранимых в учетных записях хранения Azure. Управляемый диски автоматически соответствовать hello, группа доступности hello виртуальной машины, которые могут им присоединенного tooand таким образом увеличение hello доступности виртуальных машин и служб hello, выполняющихся на виртуальной машине hello. Дополнительные сведения см. в статье hello [обзорную статью](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview).

Рекомендуется использовать tooyou диска управляемый, так как они упрощают развертывание hello и управление виртуальными машинами.
Сейчас SAP поддерживает только управляемые диски уровня "Премиум". Дополнительные сведения см. в примечании SAP [1928533].

#### <a name="azure-storage-accounts"></a>Учетные записи службы хранилища Azure
При развертывании служб или виртуальных машин в Azure развертывание виртуальных жестких дисков и образов виртуальных машин можно организовать в группы, которые называются учетными записями службы хранилища Azure. При планировании развертывания Azure, необходимо toocarefully учитывать ограничения hello в Azure. На одной стороне hello имеется ограниченное число учетных записей хранения на подписку Azure. Хотя каждая учетная запись хранилища Azure может содержать большое количество VHD-файлы, есть фиксированное ограничение на hello общее число операций ввода-ВЫВОДА на учетную запись хранения. При развертывании сотен ВМ SAP с системами СУБД, создающими значительное вызовов операций ввода-ВЫВОДА, рекомендуется toodistribute высокой ВМ СУБД операций ввода-ВЫВОДА между несколькими учетными записями хранения Azure. Следует соблюдать осторожность не tooexceed hello текущее ограничение учетных записей хранилища Azure на подписку. Поскольку хранилище является жизненно важной частью развертывания базы данных hello для системы SAP, эта концепция рассматривается более подробно в уже существует ссылка hello [руководство по развертыванию СУБД][dbms-guide].

Дополнительные сведения об учетных записях хранения Azure см. в [этой статье][storage-scalability-targets]. Чтение в этой статье, выясняется, что существуют отличия в ограничения hello стандартных учетных записей хранилища Azure и учетные записи хранения Premium. Основные различия — hello объем данных, которые могут быть сохранены в такой учетной записи хранилища. В стандартном хранилище hello том величиной больше, чем с хранилище Premium. На hello другой стороне hello стандартной учетной записи хранилища важности ограничен операций ввода-ВЫВОДА (см. столбец «Общая частота запросов»), а данное ограничение не имеет учетной записи хранилища Azure Premium hello. Мы рассмотрим сведения и результаты этих различий при обсуждении hello развертывания систем SAP, в особенности это касается серверов СУБД hello.

В учетной записи хранилища у вас hello вероятность toocreate различные контейнеры для hello цели организации и категоризация различных виртуальных жестких дисков. Эти контейнеры используются, например, для разделения виртуальных жестких дисков разных виртуальных машин. Производительность системы не зависит от того, сколько контейнеров находится в учетной записи службы хранилища Azure — один или несколько.

В пределах Azure имени виртуального жесткого диска ниже hello после именования подключение, которое должно tooprovide уникальное имя для hello VHD в Azure:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Как строка hello упомянутых выше должен toouniquely идентификации hello виртуального жесткого диска, который хранится в хранилище Azure.

### <a name="61678387-8868-435d-9f8c-450b2424f5bd"></a>Сеть Microsoft Azure
Microsoft Azure предоставляет сетевую инфраструктуру, позволяющую hello сопоставление всех сценариев, что мы хотим toorealize с программным обеспечением SAP. Ниже приведены возможности Hello.

* Доступ из hello за пределами непосредственно toohello виртуальных машин с помощью служб терминалов Windows или ssh/VNC
* Tooservices доступа и определенные порты, используемые приложениями в пределах hello виртуальные машины
* внутреннее взаимодействие и разрешение имен между группами виртуальных машин, развернутых в Azure;
* Подключения между организациями между локальной сетью клиента и hello сети Azure
* подключения между сайтами Azure в разных регионах Azure или в разных центрах обработки данных.

Дополнительные сведения см. здесь: <https://azure.microsoft.com/documentation/services/virtual-network/>

Существует много разных возможностей tooconfigure имя и разрешение IP-адресов в Azure. В этом документе только для облака сценарии используют по умолчанию hello использовании Azure DNS (в отличие от toodefining создания собственной службы DNS). Есть также возможность использовать новую службу Azure DNS вместо собственного DNS-сервера. Дополнительные сведения см. в [этой статье][virtual-networks-manage-dns-in-vnet] и на [этой странице](https://azure.microsoft.com/services/dns/).

Для сценариев между организациями, мы полагаемся на факт hello, hello локальной OpenLDAP/AD/DNS посредством VPN или частного подключения tooAzure была расширена. В некоторых сценариях, показанных здесь, может быть необходимые toohave реплику AD/OpenLDAP, установленная в Azure.

Поскольку сеть и разрешение имен является жизненно важной частью развертывания базы данных hello для системы SAP, эта концепция рассматривается более подробно в hello [руководство по развертыванию СУБД][dbms-guide].

##### <a name="azure-virtual-networks"></a>Виртуальные сети Azure
При построении виртуальной сети Azure, можно определить диапазон адресов hello частных IP-адресов hello занимаемый функциональные возможности DHCP в Azure. В сценариях между организациями hello определенный диапазон IP-адресов по-прежнему назначается через DHCP в Azure. Однако разрешение доменных имен выполняется в локальной среде (при условии, что виртуальные машины hello являются частью локального домена) и таким образом, можно разрешить адреса за пределами разных облачных службах Azure.

Все виртуальные машины в Azure требованиям toobe подключен tooa виртуальной сети.

Дополнительные сведения см. в [этой статье][resource-groups-networking] и на [этой странице](https://azure.microsoft.com/documentation/services/virtual-network/).

[comment]: <> (MShermannd TODO не удалось найти статьи, включая раздел OpenLDAP hello + ARM;)
[comment]: <> (MSSedusch: <https://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL>)

> [!NOTE]
> По умолчанию после развертывания виртуальной Машины невозможно изменить конфигурацию виртуальной сети hello. параметры TCP/IP Hello должно остаться toohello Azure DHCP-сервера. Поведение по умолчанию — назначение динамических IP-адресов.
>
>

Hello MAC-адрес виртуального сетевого адаптера hello может изменяться, например после изменения размера и hello Windows или Linux гостевой ОС hello новую сетевую карту и автоматически в этом случае использование DHCP tooassign hello адресов IP и DNS.

##### <a name="static-ip-assignment"></a>Назначение статического IP-адреса
Это возможно tooassign фиксированной или зарезервированные IP-адреса tooVMs в виртуальной сети Azure. Работающих виртуальных машин hello в виртуальной сети Azure открывает tooleverage значительные возможности этой функции, если это необходимо или требуется в некоторых сценариях. Назначение IP-адресов Hello остается действительными на протяжении всего существования hello hello ВМ, независимо от работает ли hello виртуальной Машины или завершение работы. В результате необходимо tootake hello общее число ВМ (работающих и остановленных виртуальных МАШИН) в учетную запись, при определении hello диапазон IP-адресов для hello виртуальной сети. Назначение Hello IP-адрес сохраняется, пока hello ВМ и его сетевого интерфейса не будет удален или пока hello IP-адрес его назначение отменяется еще раз. Дополнительные сведения см. в [этой статье][virtual-networks-static-private-ip-arm-pportal].

##### <a name="multiple-nics-per-vm"></a>Несколько сетевых адаптеров на виртуальной машине
Для виртуальной машины Azure вы можете определить несколько виртуальных сетевых адаптеров (vNIC). С возможностью toohave hello несколько vNICs запуском tooset копирование разделение трафика сети where, например, клиентский трафик направляется через один виртуальный сетевой адаптер и серверная часть трафика направляется через второй виртуального сетевого адаптера. В зависимости от типа hello виртуальной машины имеются различные ограничения в считает количество toohello vNICs. Подробные сведения о параметрах, функциональных возможностях и ограничениях см. в следующих статьях:

* [Создание виртуальной машины Windows, использующей несколько сетевых адаптеров, и управление ею][virtual-networks-multiple-nics-windows]
* [Как создать виртуальную машину Linux в Azure с несколькими сетевыми картами][virtual-networks-multiple-nics-linux]
* [Развертывание виртуальных машин с несколькими сетевыми адаптерами с помощью шаблона][virtual-network-deploy-multinic-arm-template]
* [Создание виртуальной машины с несколькими сетевыми интерфейсами с помощью PowerShell][virtual-network-deploy-multinic-arm-ps]
* [Развертывание виртуальных машин multi сетевого Адаптера, с помощью hello Azure CLI][virtual-network-deploy-multinic-arm-cli]

#### <a name="site-to-site-connectivity"></a>Подключение типа "сеть — сеть"
Распределенное развертывание — это виртуальные машины Azure, подключенные к локальной сети с использованием прозрачного и постоянного VPN-подключения. Это ожидаемое toobecome hello наиболее SAP шаблон общего развертывания в Azure. Hello предполагается, что операционные процедуры и процессы с экземплярами SAP в Azure должны работать прозрачно. Это означает, что вы должны быть может tooprint из этих систем, а также использовать hello SAP Transport Management System (TMS) tootransport изменения из системы разработки в Azure tooa тестовой системы развернутых локально. Дополнительную документацию по подключениям типа "сеть — сеть" можно найти в [этой статье][vpn-gateway-create-site-to-site-rm-powershell].

##### <a name="vpn-tunnel-device"></a>Устройство для VPN-туннеля
В заказ toocreate подключения сеть сеть (локального центра tooAzure данных центра обработки данных), необходимо tooeither получить и настроить VPN-устройство или использовать маршрутизации и удаленного доступа (RRAS) которая появилась как программный компонент с Windows Server 2012.

* [Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью PowerShell][vpn-gateway-create-site-to-site-rm-powershell]
* [О VPN-устройствах для подключений VPN-шлюзов типа "сеть — сеть"][vpn-gateway-about-vpn-devices]
* [VPN-шлюз: вопросы и ответы][vpn-gateway-vpn-faq]

![Подключение типа "сеть — сеть" между локальной средой и Azure][planning-guide-figure-600]

Hello выше рисунке показаны две подписки Azure имеют поддиапазоны IP-адресов, зарезервированных для использования в виртуальных сетях в Azure. hello Hello подключения из локального tooAzure сети устанавливается посредством VPN.

#### <a name="point-to-site-vpn"></a>VPN-подключение типа "точка — сеть"
Точка сеть VPN требуется tooconnect машины каждого клиента с помощью свой собственный VPN в Azure. Для сценариев SAP hello, которую мы ищем подключение точка сайт не имеет смысла. Таким образом нет дальнейшие ссылки предоставляют toopoint сеть VPN-подключение.

Дополнительные сведения см. здесь:
* [Настройка tooa подключение точка-сайт виртуальной сети с помощью hello портал Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
* [Настройка tooa подключение точка-сайт виртуальной сети с помощью PowerShell](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

#### <a name="multi-site-vpn"></a>Многосайтовая VPN
Azure предлагает также сегодня подключения VPN с несколькими сайтами toocreate hello вероятность для одной подписки Azure. Ранее одна подписка была ограниченный tooone сеть сеть VPN-подключения. Теперь это ограничение снято — многосайтовые VPN-подключения поддерживаются и для отдельных подписок. В результате возможно tooleverage более одного региона Azure для конкретной подписки посредством конфигурациях между организациями.

Дополнительную документацию можно найти в [этой статье][vpn-gateway-create-site-to-site-rm-powershell].

[comment]: <> (MShermannd: нет ссылки на документацию по ARM)

#### <a name="vnet-toovnet-connection"></a>Виртуальная сеть tooVNet подключения
С помощью VPN с несколькими сайтами, необходимо, чтобы tooconfigure отдельной виртуальной сети Azure, в каждой из областей hello. Тем не менее очень часто имеется требование hello, hello программных компонентов в различных регионах hello должны взаимодействовать друг с другом. В идеальном случае такая связь не должны маршрутизироваться из одного региона Azure tooon организациями и отсутствует toohello другой регион Azure. tooshortcut, Azure предлагает возможность tooconfigure hello подключения из одной виртуальной сети Azure в одной области tooanother виртуальной сети Azure размещено в другом регионе. Такая конфигурация называется подключением типа "виртуальная сеть — виртуальная сеть". Дополнительные сведения об этих функциях см. здесь: <https://azure.microsoft.com/documentation/articles/vpn-gateway-vnet-vnet-rm-ps/>.

#### <a name="private-connection-tooazure--expressroute"></a>TooAzure частного подключения — ExpressRoute
Microsoft Azure ExpressRoute позволяет создавать частные подключения между центрами обработки данных Azure и локальной инфраструктуры либо hello клиента или в среде совместного размещения hello. ExpressRoute предоставляется различными поставщиками MPLS VPN (с пакетной коммутацией) или другими поставщиками сетевых услуг. Подключения ExpressRoute не выходят hello общедоступный Интернет. Подключения ExpressRoute обеспечивают более высокую защищенность, большую надежность через несколько параллельных соединений, высокую скорость и меньшую задержку по сравнению с обычными подключениями через Интернет hello.

Дополнительные сведения об Azure ExpressRoute и доступных предложениях см. здесь:

* <https://azure.microsoft.com/documentation/services/expressroute/>
* <https://azure.microsoft.com/pricing/details/expressroute/>
* <https://azure.microsoft.com/documentation/articles/expressroute-faqs/>

ExpressRoute позволяет подключать несколько подписок Azure через один канал ExpressRoute, как описано здесь:

* <https://azure.microsoft.com/documentation/articles/expressroute-howto-linkvnet-arm/>
* <https://azure.microsoft.com/documentation/articles/expressroute-howto-circuit-arm/>

#### <a name="forced-tunneling-in-case-of-cross-premises"></a>Принудительное туннелирование для распределенного развертывания
Для виртуальных машин, присоединение к доменам локальной через сеть сеть "," точка сеть "или" ExpressRoute необходимо убедиться, что hello параметров Интернет-прокси развернуты для всех пользователей hello в этих виртуальных машин toomake. По умолчанию, программное обеспечение, работающее в этих виртуальных машин или пользователей с помощью обозревателя tooaccess hello Интернета, не будут проходить через прокси-сервер организации hello, а будут подключаться прямо через Azure toohello Интернета. Однако параметры прокси-сервера даже hello не через прокси-сервер организации hello hello трафика toodirect 100% решением, так как отвечает toocheck программного обеспечения и служб для hello прокси-сервера. Если программное обеспечение, работающее в hello виртуальной Машины не выполняется, или если администратор регулирует параметры hello, toohello трафика Интернет быть направлен непосредственно с помощью Azure toohello Интернета.

Порядок tooavoid это, можно настроить Принудительное туннелирование с подключением сайт сайт в локальной среде и Azure. Hello подробное описание функции Принудительное туннелирование hello публикуется здесь <https://azure.microsoft.com/documentation/articles/vpn-gateway-forced-tunneling-rm/>

Объявление маршрута по умолчанию через hello ExpressRoute BGP клиентами включено Принудительное туннелирование с ExpressRoute сеансы пиринга.

#### <a name="summary-of-azure-networking"></a>Обзор сетевых возможностей Azure
В этом разделе собраны ключевые замечания о сетевых возможностях Azure. Здесь приводится сводка основных точек hello.

* Виртуальные сети Azure позволяет tooset hello сети, в соответствии с tooyour собственных нужд
* Виртуальные сети Azure можно использовать tooassign IP адрес диапазоны tooVMs или назначить фиксированный tooVMs IP-адресов
* tooset сеть-сеть или подключение точка-сеть toocreate виртуальной сети Azure необходимо сначала
* После развертывания виртуальной машины она больше не hello toochange можно назначать toohello виртуальной Машины в виртуальной сети

### <a name="quotas-in-azure-virtual-machine-services"></a>Квоты в службах виртуальных машин Microsoft Azure
Мы должны toobe снимите о hello фактов, hello хранилища и сетевой инфраструктуры является общим для виртуальных машин, работающих в инфраструктуре Azure hello различных служб. И, как и центрах обработки данных клиента собственные hello избыточная Подготовка некоторые ресурсы инфраструктуры hello степень tooa месте. Hello платформе Microsoft Azure использует диска, ЦП, сети и другие потребления ресурсов квоты toolimit hello и toopreserve постоянной и определенной производительности.  Hello разных типов ВМ (A5, A6, т. д.) имеют разные квоты hello количество дисков, ЦП, оперативной памяти и сети.

> [!NOTE]
> Ресурсы ЦП и памяти hello типов ВМ, поддерживаемых SAP, предварительно выделяются в узлах hello. Это означает, что после развертывания виртуальной Машины hello hello на узле hello доступных ресурсов в соответствии с определением hello типа ВМ.
>
>

Необходимо учитывать при планировании и определении размеров SAP в решениях Azure hello квоты для размера виртуальной машины. описываются квот для VM Hello [здесь (Linux)] [ virtual-machines-sizes-linux] и [здесь (Windows)][virtual-machines-sizes-windows].

Hello квоты представляют теоретические максимальные значения hello.  Hello ограничение операций ввода-ВЫВОДА на диске могут быть реализованы с небольшими операциями (8 КБ), но возможно не могут быть реализованы с большими операциями (1 МБ).  ограничения IOP Hello обеспечивается при детализации hello одного диска.

Toodecide дерева грубого принятия решений ли система SAP размещается в службах виртуальных машин Azure и ее возможностях или существующей системы должен toobe настроены по-разному в системе hello toodeploy заказа в Azure, дерево принятия решений hello может использоваться как:

![Возможность toodecide toodeploy SAP в Azure для принятия решений дерева][planning-guide-figure-700]

**Шаг 1**: hello наиболее важные сведения toostart с является hello требования SAP для конкретной системы SAP. Hello SAPS требования к необходимости toobe выделены в СУБД hello и части приложения SAP hello, даже если hello система SAP уже развернута локально в двухуровневой конфигурации. Для существующих систем hello, SAPS связанные toohello оборудование часто можно определить или оценка на основании имеющихся измерений производительности SAP. Hello результаты можно найти здесь: <http://global.sap.com/campaigns/benchmark/index.epx>.
Для новых разворачиваемых систем SAP следует проверены задачу определения размеров, которую следует определить требования hello SAP к системе hello.
См. также этот блог и вложенный документ по размерам SAP в Azure: <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>.

**Шаг 2**: для существующих систем hello операций ввода-вывода и операций ввода-вывода в секунду на сервере СУБД hello должна измеряться. Для только планируемых систем hello, изменение размера упражнения для hello новой системы также должна дать общее представление о hello требования ввода-вывода на стороне СУБД hello. Если нет уверенности, рано или поздно tooconduct экспериментальную.

**Шаг 3**: требования SAP hello сравнения для сервера СУБД с hello SAPS hello разные типы ВМ можно предоставить hello. Hello сведения по системам SAP hello разных типах ВМ Azure, задокументированы в примечании SAP [1928533]. Hello необходимо уделить внимание ВМ СУБД hello сначала, так как уровень hello базы данных — hello слоев в системе SAP NetWeaver, который не масштабируется в большинстве развертываний hello. Напротив hello уровня приложения SAP может масштабироваться. Если ни один из hello SAP поддерживается типах ВМ Azure может обеспечить SAPS необходимые hello, hello рабочую нагрузку системы SAP запланированный hello не может выполняться в Azure. Вы должны либо toodeploy hello системы в локальной или требуется объем рабочей нагрузки hello toochange для hello системы.

**Шаг 4**. Как описано [здесь (Linux)][virtual-machines-sizes-linux] и [здесь (Windows)][virtual-machines-sizes-windows], Azure применяет квоту на количество операций ввода-вывода в секунду для каждого диска как в хранилище уровня Standard, так и в хранилище уровня Premium. Зависит от типа ВМ hello, hello количество дисков данных, которые могут быть подключены зависит. В результате можно вычислить максимальное число операций ввода-ВЫВОДА, которую можно достичь с каждым из типов ВМ hello. Зависит от структуры файлов базы данных hello, вы можете создать чередующийся дисков toobecome один том в hello гостевой ОС. Однако если hello текущего операций ввода-ВЫВОДА тома в развернутой системе SAP превышает ограничения hello вычисляется hello крупного типа ВМ в Azure и не toocompensate вероятность с большим объемом памяти, рабочей нагрузки hello hello системы SAP может серьезно повлиять. В таких случаях можно нажать точки, где не следует развертывать hello системы в Azure.

**Шаг 5**: особенно в системах SAP, который локально в двухуровневой конфигурации развертываются, hello скорее всего, что hello системы может потребоваться toobe, настроенный в Azure в трехуровневую конфигурацию. На этом шаге необходимо toocheck есть ли компонент в уровне приложения hello SAP, который нельзя масштабировать и который не может поместиться в hello ЦП и памяти, что ресурсы hello другое предложение типов ВМ Azure. Если на самом деле такой компонент, hello системы SAP и ее рабочей нагрузки нельзя развернуть в Azure. Но если компоненты приложения SAP hello можно масштабировать по нескольким ВМ Azure, hello систему можно развернуть в Azure.

**Шаг 6**: Если hello СУБД и компоненты уровня приложения SAP может работать на виртуальных машинах Azure, hello конфигурации необходимы определенные относится к toobe:

* количество виртуальных машин Azure;
* Типов ВМ для отдельных компонентов hello
* Число VHD в ВМ СУБД tooprovide достаточное количество операций ввода-ВЫВОДА

## <a name="managing-azure-assets"></a>Управление ресурсами Azure
### <a name="azure-portal"></a>Портал Azure
Hello портал Azure является одним из трех развертывания ВМ Azure toomanage интерфейсов. Hello базовые задачи управления, такие как развертывание ВМ из образов, можно сделать с помощью портала Azure hello. Кроме того, hello создания учетных записей хранения, виртуальных сетей, и других компонентах Azure также также может обрабатывать задачи hello портал Azure. Тем не менее функции, как отправка VHD из локальной tooAzure или копирование VHD в Azure — задачи, которые требуют сторонних средств или администрирование с помощью PowerShell или интерфейс командной строки.

![Портал Microsoft Azure, обзор виртуальных машин][planning-guide-figure-800]

[comment]: <> (MSSedusch * <https://azure.microsoft.com/documentation/articles/virtual-networks-create-vnet-arm-pportal/>)
[comment]: <> (MSSedusch * <https://azure.microsoft.com/documentation/articles/virtual-machines-windows-tutorial/>)

Задачи администрирования и конфигурации для экземпляра виртуальной машины hello возможны в пределах hello портал Azure.

Помимо перезапуска и завершения работы виртуальной машины можно также присоединить, отсоединить и создавать диски данных для экземпляра виртуальной машины hello, toocapture hello экземпляр для подготовки образа и настройте размер hello hello экземпляр виртуальной машины.

Hello портал Azure предоставляет базовые функциональные возможности toodeploy и настройка виртуальных машин и многих других служб Azure. Однако не вся доступная функциональность охватывается hello портал Azure. В hello портал Azure нет возможности tooperform задачи, такие как:

* Отправка tooAzure виртуальных жестких дисков
* копирование виртуальных машин.

[comment]: <> (MShermannd, TODO: как насчет службы автоматизации для виртуальных машин SAP? )
[comment]: <> (MSSedusch: пока что можно развернуть виртуальные машины с несколькими ОС)
[comment]: <> (Также MSSedusch автоматизация относительно развертывания не поддерживается с hello портал Azure. Задачи, такие как развертыванию нескольких виртуальных машин не поддерживается через портал Azure hello.)

### <a name="management-via-microsoft-azure-powershell-cmdlets"></a>Управление с помощью командлетов Microsoft Azure PowerShell
Windows PowerShell — это мощная и расширяемая платформа, широко используемая клиентами для большого количества систем, развернутых в Azure. После установки hello командлетов PowerShell на компьютер, ноутбук или выделенную станцию управления командлеты PowerShell hello может выполняться удаленно.

Здравствуйте tooenable процесса локальном компьютере или ноутбуке hello использования командлетов Azure PowerShell и tooconfigure Здравствуйте, для использования с hello Azure подписок — это описано в разделе [в этой статье][powershell-install-configure].

Более подробное описание действий, как tooinstall, обновления и настроить hello командлетов Azure PowerShell можно найти также в [в этой главе hello руководство по развертыванию][deployment-guide-4.1].

Клиент до сих опыту, PowerShell (PS) безусловно является hello более мощные средства toodeploy виртуальных машин и toocreate пользовательские шаги в hello развертывания виртуальных машин. Toosupplement управления командлеты PS задачи, они в hello портал Azure или даже использовали командлеты PS всех клиентов hello работающих экземпляров SAP в Azure используются исключительно toomanage их развертывания в Azure. Так как общий ресурс командлеты Azure конкретных hello hello же соглашение об именовании как hello более 2000 командлетов для Windows, это простая задача для администраторов tooleverage Windows эти командлеты.

См. пример: <http://blogs.technet.com/b/keithmayer/archive/2015/07/07/18-steps-for-end-to-end-iaas-provisioning-in-the-cloud-with-azure-resource-manager-arm-powershell-and-desired-state-configuration-dsc.aspx>

[comment]: <> (MShermannd, TODO: описывайте новые команды интерфейса командной строки при тестировании )
Развертывание расширения мониторинга Azure для SAP hello (в главе [решение мониторинга Azure для SAP] [ planning-guide-9.1] в этом документе) возможен только через PowerShell или интерфейс командной строки. Таким образом работает обязательные tooset и настроить PowerShell или интерфейс командной строки при развертывании или администрировании системы SAP NetWeaver в Azure.  

Как Azure предоставляет дополнительные функциональные возможности, новые командлеты PS реально добавленными toobe, что требует обновления командлетов hello. Таким образом он делает hello toocheck смысле веб-сайте загрузки Azure по крайней мере один раз в месяц hello <https://azure.microsoft.com/downloads/> для новой версии hello командлетов. Hello новая версия устанавливается поверх старой версии hello.

Общий список команд PowerShell, связанных с Azure, см. здесь: <https://docs.microsoft.com/powershell/azure/overview>.

### <a name="management-via-microsoft-azure-cli-commands"></a>Управление с помощью интерфейса командной строки Microsoft Azure
Для клиентов, Linux и данные toomanage Azure Powershell ресурсов может оказаться параметр. Корпорация Майкрософт предлагает в качестве альтернативы интерфейс командной строки Azure.
Hello Azure CLI предоставляет набор с открытым исходным кодом кросс платформенных команды для работы с hello платформы Azure. Hello Azure CLI предоставляет большую часть hello же функциональные возможности, найденные в hello портал Azure.

Сведения об установке, настройке и как toouse CLI команды tooaccomplish Azure задания см.

* [Установка hello Azure CLI][xplat-cli]
* [Развертывание и управление виртуальными машинами с помощью шаблонов диспетчера ресурсов Azure и Azure CLI hello] [.. /.. / linux/create-ssh-secured-vm-from-template.md]
* [Использовать hello Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure][xplat-cli-azure-resource-manager]

Также ознакомьтесь с главой [Azure CLI для виртуальных машин Linux] [ deployment-guide-4.5.2] в hello [руководство по развертыванию] [ planning-guide] на как toodeploy toouse Azure CLI hello мониторинга Azure Расширение для SAP.

## <a name="different-ways-toodeploy-vms-for-sap-in-azure"></a>Различные способы toodeploy ВМ для SAP в Azure
В этой главе сведения различными способами hello toodeploy ВМ в Azure. Также здесь рассматриваются дополнительные процедуры подготовки и процессы управления виртуальными жесткими дисками и виртуальными машинами в Azure.

### <a name="deployment-of-vms-for-sap"></a>Развертывание виртуальных машин для SAP
Microsoft Azure предлагает несколько способов toodeploy ВМ и связанные диски. Таким образом будет различия hello toounderstand очень важен, так как действия по подготовке виртуальных машин hello могут отличаться в зависимости от метода развертывания hello. Как правило мы рассмотрим hello следующие сценарии:

#### <a name="4d175f1b-7353-4137-9d2f-817683c26e53"></a>Перемещение ВМ из локальной tooAzure с помощью специализированного диска
При планировании toomove определенную систему SAP из локальной tooAzure. Это можно сделать путем отправки hello виртуальный жесткий ДИСК, содержащий hello ОС, hello двоичные файлы SAP и двоичные файлы СУБД и hello виртуальные жесткие диски с файлами данных и журналов hello объекта tooAzure СУБД hello. В отличие от слишком[сценария #2 ниже][planning-guide-5.1.2]оставьте имя узла hello, ИД безопасности SAP, а SAP учетные записи пользователей в виртуальной Машине Azure hello как они были настроены в локальной среде hello. Таким образом обобщение hello образ не является обязательным. В разделе главы [подготовки к перемещению ВМ из локальной tooAzure с помощью специализированного диска] [ planning-guide-5.2.1] этого документа в локальной среде действий по подготовке и отправке специализированного tooAzure виртуальных машин или виртуальные жесткие диски. Глава чтения [сценарий 3: перемещение ВМ из локально с помощью специализированного VHD Azure с SAP] [ deployment-guide-3.4] в hello [руководство по развертыванию] [ deployment-guide] Подробные инструкции по развертыванию такого образа в Azure.

#### <a name="e18f7839-c0e2-4385-b1e6-4538453a285c"></a>Развертывание виртуальной машины с помощью пользовательского образа
Из-за требований исправлениям toospecific вашей версии ОС или СУБД образы предоставленный hello в hello Azure Marketplace могут не соответствовать вашим потребностям. Таким образом может потребоваться toocreate ВМ с помощью собственного «private» образа ОС или СУБД виртуальной Машины, который можно разворачивать многократно. tooprepare такой «свой» образ для дублирования hello следующих элементов имеют считается toobe:

- - -
> ![Windows][Logo_Windows] Windows
>
> Здесь Дополнительные сведения см. в разделе: <https://docs.microsoft.com/azure/virtual-machines/windows/upload-generalized-managed> параметры Windows hello (такие как идентификатор безопасности Windows и имя узла) необходимо задать абстрагированные/универсальные на hello локально Виртуальная машина с помощью команды sysprep hello.
>
>
> ![Linux][Logo_Linux] Linux
>
> Выполните hello действия, описанные в следующих статьях для [SUSE][virtual-machines-linux-create-upload-vhd-suse], [Red Hat][virtual-machines-linux-redhat-create-upload-vhd], или [Oracle Linux] [ virtual-machines-linux-create-upload-vhd-oracle], tooprepare toobe виртуальный жесткий ДИСК отправлен tooAzure.
>
>

- - -
Если вы уже установили содержимое SAP в локальной виртуальной Машины (особенно для двухуровневых систем), hello параметры системы SAP можно адаптировать после развертывания hello hello виртуальной Машине Azure через экземпляр hello переименовать процедуру, поддерживаемых hello подготовки программного обеспечения SAP Диспетчер (Примечание SAP [1619720]). В разделе главы [Подготовка развертывания ВМ с определенным пользователем образа для SAP] [ planning-guide-5.2.2] и [Отправка VHD из локальной tooAzure] [ planning-guide-5.3.2]этого документа локальной действия по подготовке и процесса отправки обобщенный tooAzure виртуальной Машины. Глава чтения [сценарий 2: развертывание ВМ с помощью пользовательского образа для SAP] [ deployment-guide-3.3] в hello [руководство по развертыванию] [ deployment-guide] подробное описание шагов развертывания SAP NetWeaver в Azure.

#### <a name="deploying-a-vm-out-of-hello-azure-marketplace"></a>Развертывание ВМ из Azure Marketplace hello
Вы хотели бы toouse корпорации Майкрософт или сторонних указанный образ ВМ из Azure Marketplace toodeploy hello ВМ. После развертывания ВМ в Azure вы выполните hello же рекомендации и средства tooinstall hello программное обеспечение SAP или СУБД как это делается в локальной среде. Более подробные описания развертывания, см. в разделе главы [сценария 1: развертывание ВМ из Azure Marketplace для SAP hello] [ deployment-guide-3.2] в hello [руководство по развертыванию] [ deployment-guide].

### <a name="6ffb9f41-a292-40bf-9e70-8204448559e7"></a>Подготовка виртуальных машин с SAP для Azure
Перед отправкой виртуальных машин в Azure необходимо toomake том, что hello ВМ и VHD выполнить определенные требования. Существуют небольшие различия в зависимости от используемого способа развертывания hello.

#### <a name="1b287330-944b-495d-9ea7-94b83aff73ef"></a>Подготовка к перемещению ВМ из локальной tooAzure с помощью специализированного диска
Распространенный способ развертывания — toomove существующей виртуальной Машины, который запускается из tooAzure в локальной системе SAP. Здравствуйте того же имени узла виртуальной Машины и hello системы SAP в ВМ должны просто запускаться в Azure с помощью hello и скорее hello же ИД безопасности SAP. В этом случае hello гостевой операционной системы виртуальной Машины не быть обобщена для нескольких развертываний. Если hello локальная сеть расширяется до Azure (в главе [между организациями - развертывание одной или нескольких ВМ SAP в Azure с требованием hello полной интеграции с локальной сетью hello] [ planning-guide-2.2] в этом документе), затем даже hello учетные записи домена можно использовать в hello виртуальной Машины, которые использовались до локальной.

Ниже перечислены требования для подготовки собственного диска виртуальной машины Azure.

* Первоначально hello VHD содержащей hello операционной системы может иметь максимальный размер 127 ГБ. Это ограничение получен исключено в конце hello марта 2015 г. Теперь hello виртуальный жесткий ДИСК, содержащий hello операционной системы может быть вверх too1TB в размере, любые другие хранилища Azure также размещенного виртуального жесткого диска.
* Он должен toobe в фиксированный формат VHD hello. Динамические виртуальные жесткие диски и виртуальные жесткие диски в формате VHDx пока не поддерживаются в Azure. Динамические виртуальные жесткие диски будут преобразованный toostatic виртуальных жестких дисков при передаче hello виртуального жесткого диска с командлеты PowerShell или интерфейс командной строки
* Виртуальные жесткие диски, которые toohello подключенных виртуальных Машин и должен устанавливаться в Azure toohello toobe необходимость виртуальной Машины в фиксированном формате VHD также. Сведения об ограничениях размеров дисков данных см. [в этой](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) (Linux) и [этой статье](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows) (Windows). Динамические виртуальные жесткие диски будут преобразованный toostatic виртуальных жестких дисков при передаче hello виртуального жесткого диска с командлеты PowerShell или интерфейс командной строки
* Добавьте другую локальную учетную запись с правами администратора, которые могут использоваться службой поддержки Майкрософт или назначаться в качестве контекста для toorun служб и приложений в до hello, в котором развернута виртуальная машина и более подходящих пользователей можно использовать.
* Hello в случае использования сценария развертывания только для облака (в главе [только для облака — развертывания виртуальных машин в Azure без зависимостей от hello в локальной сети клиента] [ planning-guide-2.1] данного объекта документ) в сочетании с такого метода развертывания домену, учетные записи могут не работать после развертывания диска Azure hello в Azure. Это особенно важно для учетных записей, используемых toorun служб, таких как приложения hello СУБД или SAP. Поэтому требуется tooreplace эти учетные записи домена, локальные учетные записи ВМ и удалить hello локальными учетными записями домена hello виртуальной Машины. Сохранение локальных пользователей домена в образе виртуальной Машины hello не является проблемой при hello ВМ разворачивается в hello межсетевых локальных ресурсах, приведенные в главе [между организациями - развертывание одной или нескольких ВМ SAP в Azure с требованием hello, полностью интегрированы в локальную сеть hello] [ planning-guide-2.2] в настоящем документе.
* Если учетные записи домена использовались в качестве имен входа СУБД или пользователям при выполнении hello системы в локальной среде и эти виртуальные машины должны toobe, развернутых в сценариях только для облака, пользователи домена hello должны toobe удалены. Необходимо убедиться, что что hello локального администратора, а также другого локального пользователя ВМ добавляется в качестве имени входа или пользователя в СУБД как администраторов hello toomake.
* Добавьте другие локальные учетные записи, которые могут потребоваться для hello выбранного варианта развертывания.

- - -
> ![Windows][Logo_Windows] Windows
>
> В этом случае никакая универсализация (sysprep) ВМ hello необходимые tooupload и разверните hello ВМ в Azure.
> Убедитесь, что диск D:\ не используется.
> Настройте автоподключение для подключенных дисков, как описано в разделе этого документа [Настройка автоподключения для подключенных дисков][planning-guide-5.5.3].
>
> ![Linux][Logo_Linux] Linux
>
> В этом случае никакая универсализация (waagent-deprovision) является обязательным tooupload ВМ hello и развертывание hello ВМ в Azure.
> Убедитесь, что /mnt/resource не используется, и что все диски подключены через uuid. Для диска ОС hello убедитесь, что запись hello также отражает подключения на основе uuid hello.
>
>

- - -
#### <a name="57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3"></a>Подготовка виртуальной машины к развертыванию с помощью пользовательского образа для SAP
Файлы на виртуальном жестком диске, содержащие обобщенную ОС, также хранятся в контейнерах учетных записей хранения Azure или как образы управляемых дисков. Можно развернуть новую виртуальную Машину из такого образа с помощью ссылки на hello образа виртуального жесткого диска или дисков, управляемых как источник в файлах шаблона развертывания, как описано в главе [сценарий 2: развертывание ВМ с помощью пользовательского образа для SAP] [ deployment-guide-3.3]из hello [руководство по развертыванию][deployment-guide].

Ниже перечислены требования для подготовки собственного образа виртуальной машины Azure.

* Первоначально hello VHD содержащей hello операционной системы может иметь максимальный размер 127 ГБ. Это ограничение получен исключено в конце hello марта 2015 г. Теперь hello виртуальный жесткий ДИСК, содержащий hello операционной системы может быть вверх too1TB в размере, любые другие хранилища Azure также размещенного виртуального жесткого диска.
* Он должен toobe в фиксированный формат VHD hello. Динамические виртуальные жесткие диски и виртуальные жесткие диски в формате VHDx пока не поддерживаются в Azure. Динамические виртуальные жесткие диски будут преобразованный toostatic виртуальных жестких дисков при передаче hello виртуального жесткого диска с командлеты PowerShell или интерфейс командной строки
* Виртуальные жесткие диски, которые toohello подключенных виртуальных Машин и должен устанавливаться в Azure toohello toobe необходимость виртуальной Машины в фиксированном формате VHD также. Сведения об ограничениях размеров дисков данных см. [в этой](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-linux) (Linux) и [этой статье](https://docs.microsoft.com/azure/storage/storage-about-disks-and-vhds-windows) (Windows). Динамические виртуальные жесткие диски будут преобразованный toostatic виртуальных жестких дисков при передаче hello виртуального жесткого диска с командлеты PowerShell или интерфейс командной строки
* Поскольку все hello пользователей домена, зарегистрированную в качестве пользователей в hello виртуальной Машины не существует в сценарии только для облака (в главе [только для облака — развертывания виртуальных машин в Azure без зависимостей от hello в локальной сети клиента] [ planning-guide-2.1] этого документа), службы, с помощью такого домена, учетные записи могут не работать после развертывания hello образа в Azure. Это особенно важно для учетных записей, используемых toorun служб, таких как СУБД или приложений SAP. Поэтому требуется tooreplace эти учетные записи домена, локальные учетные записи ВМ и удалить hello локальными учетными записями домена hello виртуальной Машины. Сохранение локальных пользователей домена в образе виртуальной Машины hello может не возникнуть проблемы, если ВМ разворачивается в hello hello межсетевых локальных ресурсах, приведенные в главе [между организациями - развертывание одной или нескольких ВМ SAP в Azure с требованием hello полной интеграции с локальной сетью hello] [ planning-guide-2.2] в настоящем документе.
* Добавьте другую локальную учетную запись с правами администратора, которые могут использоваться службой поддержки Майкрософт при исследовании проблем или назначаться в качестве контекста для toorun служб и приложений в до hello, в котором развернута виртуальная машина и более подходящих пользователей можно использовать.
* В развертываний только в облаке и где учетные записи домена использовались в качестве имен входа СУБД или пользователей при запуске hello системы в локальной среде следует удалить пользователей домена hello. Необходимо toomake убедитесь, что имя входа или учетных данных пользователя hello СУБД как администраторов добавлен hello локального администратора, а также другого локального пользователя ВМ.
* Добавьте другие локальные учетные записи, которые могут потребоваться для hello выбранного варианта развертывания.
* Если изображение hello содержит установку SAP NetWeaver и переименование hello имя узла из исходного имени hello точке "hello" hello развертывания Azure, вероятнее всего, это рекомендуемый toocopy hello последние версии DVD Manager hello подготовки программного обеспечения SAP в шаблон Hello. Это позволит вам использовать tooeasily hello SAP предоставляемых переименования функции tooadapt hello изменить имя узла или изменение hello SID hello системы SAP в hello развернут образ виртуальной Машины, сразу после запуска новой копии.

- - -
> ![Windows][Logo_Windows] Windows
>
> Убедитесь, что диск D:\ не используется. Настройте автоподключение для подключенных дисков, как описано в разделе этого документа [Настройка автоподключения для подключенных дисков][planning-guide-5.5.3].
>
> ![Linux][Logo_Linux] Linux
>
> Убедитесь, что /mnt/resource не используется, и что все диски подключены через uuid. Для диска ОС hello убедитесь, что запись hello также отражает подключения на основе uuid hello.
>
>

- - -
* В такой шаблон можно также заранее установить графический интерфейс SAP (для администрирования и настройки).
* Другое программное обеспечение, переименование hello toorun необходимые виртуальные машины успешно в сценариях между организациями, которые могут быть установлены до тех пор, пока это программное обеспечение может работать с hello hello виртуальной Машины.

Если hello ВМ, достаточно подготовленная toobe универсальных и в конечном счете зависит от учетных записей и пользователей не доступно в hello целевые сценарии развертывания Azure, ведется hello последнее действие по универсализации такого образа.

##### <a name="generalizing-a-vm"></a>Обобщение виртуальной машины
- - -
> ![Windows][Logo_Windows] Windows
>
> Последний шаг Hello — toolog в tooa ВМ с учетной записью администратора. Откройте окно командной строки Windows с правами администратора. Go too%windir%\windows\system32\sysprep и запустите программу sysprep.exe.
> Откроется небольшое окно. Это вариант «Generalize» hello важные toocheck (по умолчанию hello он снят) и измените параметр завершения hello со значения по умолчанию «Перезагрузить» too'Shutdown ". Эта процедура предполагает, процесс выполнения sysprep hello выполненного локально в hello гостевой ОС виртуальной машины.
> Процедура hello tooperform виртуальная машина уже запущена в Azure, выполните hello действия, описанные в [в этой статье](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/capture-image-resource).
>
> ![Linux][Logo_Linux] Linux
>
> [Как toocapture toouse виртуальных машин Linux в качестве шаблона диспетчера ресурсов][capture-image-linux-step-2-create-vm-image]
>
>

- - -
### <a name="transferring-vms-and-vhds-between-on-premises-tooazure"></a>Передача ВМ и VHD между локальной tooAzure
Так как отправка tooAzure образы и диски виртуальной Машины не поддерживается через портал Azure hello, необходимы toouse командлетов Azure PowerShell или интерфейс командной строки. Другой вариант — использование hello hello средство «AzCopy». Hello средство можно скопировать VHD между локальной средой и Azure (в обоих направлениях). Также она позволяет копировать виртуальные жесткие диски между регионами Azure. Скачивание и использование AzCopy описывается в [этой документации][storage-use-azcopy].

Третий альтернативный бы toouse различных сторонних средств, ориентированных графического пользовательского интерфейса. Но перед этим убедитесь, что эти средства поддерживают страничные BLOB-объекты Azure. Для наших целей мы должны toouse Azure страничный большой двоичный объект хранения (Здесь описываются различия hello: <https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>). Также hello средств, предоставляемых Azure очень эффективно сжимать ВМ hello и виртуальные жесткие диски, для которых требуется загрузить toobe. Это важно, поскольку эффективное сжатие сокращает время передачи hello (который зависит от все равно hello передачи ссылки toohello целевые Интернет с помещение локальной hello и региона развертывания Azure hello). Это справедливо предположить, что отправка ВМ или VHD из Европейского расположения toohello США Azure данных на основе центры займет больше времени, чем отправка hello же ВМ или VHD toohello европейских центрах обработки данных Azure.

#### <a name="a43e40e6-1acc-4633-9816-8f095d5a7b6a"></a>Отправка VHD из локальной tooAzure
tooupload существующей ВМ или VHD из hello в локальной сети ВМ или VHD должен toomeet hello требования, перечисленные в главе [подготовки к перемещению ВМ из локальной tooAzure с помощью специализированного диска] [ planning-guide-5.2.1] этого документа.

Такую ВМ необходимо обобщить toobe и могут быть отправлены в состоянии hello и форме, имеющиеся в ней после завершения работы на hello локальной стороне. Hello относится к дополнительным VHD, не могут содержать любой операционной системе.

##### <a name="uploading-a-vhd-and-making-it-an-azure-disk"></a>Отправка виртуального жесткого диска и его преобразование в диск Azure
В этом случае мы tooupload виртуального жесткого диска, с указанием или без ОС в нем, а подключить ее tooa виртуальную Машину в качестве диска данных или использовать его в качестве диска ОС. Этот процесс состоит из нескольких этапов.

**PowerShell**

* Войдите в подписке tooyour с *AzureRmAccount входа*
* Задать подписки hello контекста с *набор AzureRmContext* и параметр SubscriptionId или Имя_подписки - статье <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* Отправка hello VHD с *добавить AzureRmVhd* tooan учетной записи хранилища Azure — в разделе <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (Необязательно) Создать диск управляемых из hello виртуального жесткого диска с *New AzureRmDisk* -в разделе <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermdisk>
* Задать hello ОС из нового toohello конфигурации виртуальной Машины виртуальный жесткий ДИСК или диск управляемых с помощью *AzureRmVMOSDisk набор* -в разделе <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>
* Создание новой виртуальной Машины из hello конфигурации виртуальной Машины с *New AzureRmVM* -в разделе <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>
* Добавьте диск данных tooa новой виртуальной Машины с *добавить AzureRmVMDataDisk* -в разделе <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk>

**Azure CLI 2.0**

* Войдите в подписке tooyour с *входа az*
* Выберите подписку с помощью команды *az account set --subscription `<subscription name or id`>*.
* Отправить hello VHD с *az хранилища больших двоичных объектов передачи* -в разделе [hello с помощью Azure CLI со службой хранилища Azure][storage-azure-cli]
* (Необязательно) Создать диск управляемых из hello виртуального жесткого диска с *создать диск az* -https://docs.microsoft.com/cli/azure/disk#create см.
* Создание новой виртуальной Машины указание hello передать виртуальный жесткий ДИСК или диск, управляемых как диска ОС с *создания виртуальной машины az* и параметр *--присоединить os диск*
* Добавьте диск данных tooa новой виртуальной Машины с *присоединить диск виртуальной машины az* и параметр *--new*

**Шаблон**

* Отправить VHD с помощью Powershell или Azure CLI hello
* (Необязательно) Создать диск управляемых из hello виртуального жесткого диска с помощью Powershell, Azure CLI или hello портал Azure
* Развертывание hello виртуальной Машины с помощью шаблона JSON, ссылающиеся на hello виртуального жесткого диска, как показано в [этот пример шаблона JSON](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json) или с помощью управляемых дисков, как показано в [этот пример шаблона JSON](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-disk-md/azuredeploy.json).

#### <a name="deployment-of-a-vm-image"></a>Развертывание образа виртуальной машины
tooupload существующей ВМ или VHD из hello в локальной сети в порядке toouse ее как образ виртуальной Машины Azure ВМ или VHD должны toomeet hello требования, перечисленные в главе [Подготовка развертывания ВМ с определенным пользователем образа для SAP] [ planning-guide-5.2.2] этого документа.

* Используйте *sysprep* в Windows или *waagent-deprovision* на Linux toogeneralize ВМ -. в разделе [технического справочника по Sysprep](https://technet.microsoft.com/library/cc766049.aspx) для Windows или [как toocapture Toouse виртуальных машин Linux в качестве шаблона диспетчера ресурсов] [ capture-image-linux-step-2-create-vm-image] для Linux
* Войдите в подписке tooyour с *AzureRmAccount входа*
* Задать подписки hello контекста с *набор AzureRmContext* и параметр SubscriptionId или Имя_подписки - статье <https://docs.microsoft.com/powershell/module/azurerm.profile/set-azurermcontext>
* Отправка hello VHD с *добавить AzureRmVhd* tooan учетной записи хранилища Azure — в разделе <https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvhd>
* (Необязательно) Создание управляемых образа диска из hello виртуального жесткого диска с *New AzureRmImage* -в разделе <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermimage>
* Диск ОС hello набор новых toothe конфигурации виртуальной Машины
  * виртуальный жесткий диск с помощью командлета *Set-AzureRmVMOSDisk -SourceImageUri -CreateOption fromImage* (дополнительные сведения см. по адресу: <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk>);
  * образ управляемого диска с помощью командлета *Set-AzureRmVMSourceImage* (дополнительные сведения см. по адресу: <https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage>).
* Создание новой виртуальной Машины из hello конфигурации виртуальной Машины с *New AzureRmVM* -в разделе <https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvm>

**Azure CLI 2.0**

* Используйте *sysprep* в Windows или *waagent-deprovision* на Linux toogeneralize ВМ -. в разделе [технического справочника по Sysprep](https://technet.microsoft.com/library/cc766049.aspx) для Windows или [как toocapture Toouse виртуальных машин Linux в качестве шаблона диспетчера ресурсов] [ capture-image-linux-step-2-create-vm-image] для Linux
* Войдите в подписке tooyour с *входа az*
* Выберите подписку с помощью команды *az account set --subscription `<subscription name or id`>*.
* Отправить hello VHD с *az хранилища больших двоичных объектов передачи* -в разделе [hello с помощью Azure CLI со службой хранилища Azure][storage-azure-cli]
* (Необязательно) Создание управляемых образа диска из hello виртуального жесткого диска с *создать образ az* -https://docs.microsoft.com/cli/azure/image#create см.
* Создание новой виртуальной Машины указание hello передать виртуальный жесткий ДИСК или образ диска, управляемых как диска ОС с *создания виртуальной машины az* и параметр *--изображения*

**Шаблон**

* Используйте *sysprep* в Windows или *waagent-deprovision* на Linux toogeneralize ВМ -. в разделе [технического справочника по Sysprep](https://technet.microsoft.com/library/cc766049.aspx) для Windows или [как toocapture Toouse виртуальных машин Linux в качестве шаблона диспетчера ресурсов] [ capture-image-linux-step-2-create-vm-image] для Linux
* Отправить VHD с помощью Powershell или Azure CLI hello
* (Необязательно) Создание управляемых образа диска из hello виртуального жесткого диска с помощью Powershell, Azure CLI или hello портал Azure
* Развертывание hello виртуальной Машины с помощью шаблона JSON, ссылающиеся на hello образа виртуального жесткого диска, как показано в [этот пример шаблона JSON](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sap-2-tier-user-image/azuredeploy.json) или с помощью hello управляемый образ диска, как показано в [этот пример шаблона JSON](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).

#### <a name="downloading-vhds-or-managed-disks-tooon-premises"></a>Загрузка виртуальных жестких дисков или дисков, управляемых tooon организациями
Azure инфраструктура как услуга не является односторонней street того, что только могут tooupload виртуальные жесткие диски и систем SAP. Можно переместить SAP систем из Azure обратно в локальный Привет также.

Во время hello hello hello загрузки виртуальных жестких дисков или дисков, управляемых не может быть активной. Даже при загрузке дисков, подключенных tooVMs, hello toobe потребностей виртуальной Машины завершена и освобождается. Если требуется только базы данных hello toodownload содержимого, которые затем должны быть используется tooset новой системы локально. Если и допустима, время "hello" hello загрузить hello установки новой системы hello, hello системы в Azure можно по-прежнему работать , можно исключить длинное простои, выполняя сжатой базы данных резервной копии в виде диска и просто загрузить этот диск вместо загрузки также hello ВМ на основе ОС.

#### <a name="powershell"></a>PowerShell

  * Загрузка управляемого диска  
  Необходимо сначала toohello доступа tooget базовый большой двоичный объект hello управляемого диска. Затем можно скопировать hello базового большого двоичного объекта tooa новой учетной записи хранения и загрузить hello BLOB-объектов из этой учетной записи хранения.

  ```powershell
  $access = Grant-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name> -Access Read -DurationInSecond 3600
  $key = (Get-AzureRmStorageAccountKey -ResourceGroupName <resource group> -Name <storage account name>)[0].Value
  $destContext = (New-AzureStorageContext -StorageAccountName <storage account name -StorageAccountKey $key)
  Start-AzureStorageBlobCopy -AbsoluteUri $access.AccessSAS -DestContainer <container name> -DestBlob <blob name> -DestContext $destContext
  # Wait for blob copy toofinish
  Get-AzureStorageBlobCopyState -Container <container name> -Blob <blob name> -Context $destContext
  Save-AzureRmVhd -SourceUri <blob in new storage account> -LocalFilePath <local file path> -StorageKey $key
  # Wait for download toofinish
  Revoke-AzureRmDiskAccess -ResourceGroupName <resource group> -DiskName <disk name>
  ```

  * Загрузка виртуального жесткого диска  
  После остановки системы SAP hello и hello виртуальная машина завершает работу, можно использовать командлет PowerShell hello AzureRmVhd сохранить на hello локальной целевые диски VHD hello toodownload обратно toohello локальной системы. В порядке toodo потребуется URL-адрес hello hello виртуальный жесткий ДИСК, который можно найти в разделе «Storage hello объекта hello портал Azure (необходимость toonavigate toohello учетной записи хранилища и hello контейнер хранилища которой hello виртуальный жесткий ДИСК был создан) и вам нужен tooknow, где hello виртуальный жесткий ДИСК должен быть скопировать.

  Затем можно использовать команду hello, просто определяет параметр hello SourceUri как hello URL-адрес виртуального жесткого диска toodownload hello и hello LocalFilePath как физическое расположение hello hello виртуального жесткого диска (включая его имя). Команда Hello может выглядеть так:

  ```powerhell
  Save-AzureRmVhd -ResourceGroupName <resource group name of storage account> -SourceUri http://<storage account name>.blob.core.windows.net/<container name>/sapidedata.vhd -LocalFilePath E:\Azure_downloads\sapidesdata.vhd
  ```

  Дополнительные сведения о командлете Save AzureRmVhd hello см. Здесь <https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvhd>.

#### <a name="cli-20"></a>CLI 2.0
  * Загрузка управляемого диска  
  Необходимо сначала toohello доступа tooget базовый большой двоичный объект hello управляемого диска. Затем можно скопировать hello базового большого двоичного объекта tooa новой учетной записи хранения и загрузить hello BLOB-объектов из этой учетной записи хранения.
  ```
  az disk grant-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --duration-in-seconds 3600
  az storage blob download --sas-token "<sas token>" --account-name <account name> --container-name <container name> --name <blob name> --file <local file>
  az disk revoke-access --ids "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>"
  ```

  * Загрузка виртуального жесткого диска   
  После остановки системы SAP hello hello виртуальная машина завершает работу, можно использовать команду hello Azure CLI _загрузку большого двоичного объекта хранилища azure_ на целевом сервере локальной hello toodownload hello VHD диски world локальной серверной toohello. В порядке toodo потребуется имя hello и контейнером hello hello виртуальный жесткий ДИСК, который можно найти в разделе «Storage hello объекта hello портал Azure (необходимость toonavigate toohello учетной записи хранилища и hello контейнер хранилища которой hello виртуальный жесткий ДИСК был создан) и вы должны tooknow где Hello виртуального жесткого диска должны быть скопированы.

  Затем можно использовать команду hello, просто определяя hello параметров большого двоичного объекта и контейнера hello VHD toodownload и назначения hello как физический целевое расположение hello hello виртуального жесткого диска (включая его имя). Команда Hello может выглядеть так:

  ```
  az storage blob download --name <name of hello VHD toodownload> --container-name <container of hello VHD toodownload> --account-name <storage account name of hello VHD toodownload> --account-key <storage account key> --file <destination of hello VHD toodownload>
  ```

### <a name="transferring-vms-and-disks-within-azure"></a>Передача виртуальных машин и дисков в пределах Azure
#### <a name="copying-sap-systems-within-azure"></a>Копирование систем SAP в пределах Azure
Система SAP или даже выделенный сервер СУБД, поддерживающий уровень приложения SAP, могут состоять из нескольких дисков, которые содержат либо hello ОС с двоичными файлами hello или hello данных и файлы базы данных SAP hello журналов. Здравствуйте, функциональность Azure копирования дисков, ни hello функциональность Azure сохранения дисков tooa локальный диск имеет механизм синхронизации, который бы синхронно снимок несколько дисков. Таким образом, состояние hello hello копировании или при сохранении дисков даже при их подключении к hello одной виртуальной Машины будет отличаться. Это означает, что в hello конкретную ситуацию с различными данными, а также виду в разных дисках hello, hello базы данных в конец hello будет несогласованной.

**Заключение: Порядок toocopy или сохранить диски, которые являются частью конфигурации системы SAP требуется система SAP toostop hello и потребовать tooshut вниз hello развертывания ВМ. Только в том случае, то можно скопировать или загрузить набор hello tooeither дисков создайте копию hello системы SAP в Azure или локально.**

Диски с данными можно сохранить в качестве VHD-файлы в учетную запись хранилища Azure и может быть непосредственно подключенного tooa виртуальной машине или использоваться в качестве изображения. В этом случае hello VHD указывает расположение скопированный tooanother до выполнения вложенного toohello виртуальной машины. Полное имя Hello hello VHD-файл в Azure должно быть уникальным в пределах Azure. Как упоминалось ранее, уже, hello имя имеет вид трехкомпонентным именем, выглядит следующим образом:

    http(s)://<storage account name>.blob.core.windows.net/<container name>/<vhd name>

Для дисков данных также можно использовать управляемые диски. В этом случае hello управляемый диск — используется toocreate новый управляемый диск, прежде чем вложенного toohello виртуальной машины. Имя Hello hello управляемого диска должно быть уникальным в пределах группы ресурсов.

##### <a name="powershell"></a>PowerShell
Можно использовать командлеты Azure PowerShell toocopy виртуального жесткого диска, как показано в [в этой статье][storage-powershell-guide-full-copy-vhd]. toocreate новый диск управляемый код, используйте New AzureRmDiskConfig и создать AzureRmDisk, как показано в следующий пример hello.

```powershell
$config = New-AzureRmDiskConfig -CreateOption Copy -SourceUri "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" -Location <location>
New-AzureRmDisk -ResourceGroupName <resource group name> -DiskName <disk name> -Disk $config
```

##### <a name="cli-20"></a>CLI 2.0
Можно использовать Azure CLI toocopy виртуального жесткого диска, как показано в [в этой статье][storage-azure-cli-copy-blobs]. использовать toocreate на новый диск управляемый *создать диск az* как показано в следующий пример hello.

```
az disk create --source "/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/disks/<disk name>" --name <disk name> --resource-group <resource group name> --location <location>
```

##### <a name="azure-storage-tools"></a>Средства хранилища Azure
* <http://storageexplorer.com/>

Профессиональные выпуски обозревателей службы хранилища Azure можно найти по следующим ссылкам.

* <http://www.cerebrata.com/>
* <http://clumsyleaf.com/products/cloudxplorer>

Hello копия самого VHD в учетной записи хранения является занимает всего несколько секунд (создание моментальных снимков с отложенным копированием или копированием при записи аналогичном оборудовании tooSAN). После того как вы копию hello VHD-файл можно прикрепить tooa виртуальной машины или используйте его как изображение tooattach копирует машин toovirtual hello виртуального жесткого диска.

##### <a name="powershell"></a>PowerShell
```powershell
# attach a vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -VhdUri <path toovhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name newdatadisk -ManagedDiskId <managed disk id> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption attach
$vm | Update-AzureRmVM

# attach a copy of hello vhd tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Name <disk name> -VhdUri <new path of vhd> -SourceImageUri <path tooimage vhd> -Caching <caching option> -DiskSizeInGB $null -Lun <lun, for example 0> -CreateOption fromImage
$vm | Update-AzureRmVM

# attach a copy of hello managed disk tooa vm
$vm = Get-AzureRmVM -ResourceGroupName <resource group name> -Name <vm name>
$diskConfig = New-AzureRmDiskConfig -Location $vm.Location -CreateOption Copy -SourceUri <source managed disk id>
$disk = New-AzureRmDisk -DiskName <disk name> -Disk $diskConfig -ResourceGroupName <resource group name>
$vm = Add-AzureRmVMDataDisk -VM $vm -Caching <caching option> -Lun <lun, for example 0> -CreateOption attach -ManagedDiskId $disk.Id
$vm | Update-AzureRmVM
```
##### <a name="cli-20"></a>CLI 2.0
```

# attach a vhd tooa vm
az vm unmanaged-disk attach --resource-group <resource group name> --vm-name <vm name> --vhd-uri <path toovhd>

# attach a managed disk tooa vm
az vm disk attach --resource-group <resource group name> --vm-name <vm name> --disk <managed disk id>

# attach a copy of hello vhd tooa vm
# this scenario is currently not possible with Azure CLI. A workaround is toomanually copy hello vhd toohello destination.

# attach a copy of a managed disk tooa vm
az disk create --name <new disk name> --resource-group <resource group name> --location <location of target virtual machine> --source <source managed disk id>
az vm disk attach --disk <new disk name or managed disk id> --resource-group <resource group name> --vm-name <vm name> --caching <caching option> --lun <lun, for example 0>
```

#### <a name="9789b076-2011-4afa-b2fe-b07a8aba58a1"></a>Копирование дисков между учетными записями хранения Azure
Эта задача не может выполняться на hello портал Azure. Используйте командлеты Azure PowerShell, интерфейс командной строки Azure или обозреватель хранилища стороннего поставщика. Здравствуйте, командлеты PowerShell или команды CLI можно создавать и управлять больших двоичных объектов, среди которых hello возможность tooasynchronously копирования BLOB-объектов в учетных записях хранения и по регионам в рамках подписки Azure hello.

##### <a name="powershell"></a>PowerShell
Вы также можете копировать виртуальные жесткие диски между подписками. Дополнительные сведения см. в [этой статье][storage-powershell-guide-full-copy-vhd].

базовый поток логики командлета PS hello Hello выглядит следующим образом:

* Создать контекст учетной записи хранилища для hello **источника** учетной записи хранилища с *New AzureStorageContext* -в разделе <https://msdn.microsoft.com/library/dn806380.aspx>
* Создать контекст учетной записи хранилища для hello **целевой** учетной записи хранилища с *New AzureStorageContext* -в разделе <https://msdn.microsoft.com/library/dn806380.aspx>
* Запустить копию hello с

```powershell
Start-AzureStorageBlobCopy -SrcBlob <source blob name> -SrcContainer <source container name> -SrcContext <variable containing context of source storage account> -DestBlob <target blob name> -DestContainer <target container name> -DestContext <variable containing context of target storage account>
```

* Проверить состояние копии hello в цикле с hello

```powershell
Get-AzureStorageBlobCopyState -Blob <target blob name> -Container <target container name> -Context <variable containing context of target storage account>
```

* Подключите hello новый виртуальный жесткий ДИСК tooa виртуальной машине, как описано выше.

Примеры можно найти в [этой статье][storage-powershell-guide-full-copy-vhd].

##### <a name="cli-20"></a>CLI 2.0
* Запустить копию hello с

```
az storage blob copy start --source-blob <source blob name> --source-container <source container name> --source-account-name <source storage account name> --source-account-key <source storage account key> --destination-container <target container name> --destination-blob <target blob name> --account-name <target storage account name> --account-key <target storage account name>
```

* Проверьте состояние hello в том случае, если hello копии в цикле с

```
az storage blob show --name <target blob name> --container <target container name> --account-name <target storage account name> --account-key <target storage account name>
```

* Подключите hello новый виртуальный жесткий ДИСК tooa виртуальной машине, как описано выше.

Примеры можно найти в [этой статье][storage-azure-cli-copy-blobs].

### <a name="disk-handling"></a>Управление дисками
#### <a name="4efec401-91e0-40c0-8e64-f2dceadff646"></a>Структура виртуальной машины и диска для развертываний SAP
В идеале hello Обработка структуры hello виртуальной машины и связанных hello диски должны быть очень простыми. Для локальных установок клиенты разработали много способов структурирования серверной установки.

* Один базовый диск, содержащий hello ОС и все двоичные файлы hello объекта hello СУБД и SAP. С марта 2015 г. Этот диск можно вверх too1TB размер вместо более ранней ограничения, которые ограничены его too127GB.
* Один или несколько дисков, содержащих hello СУБД журнала файла базы данных SAP hello и файлов журналов hello hello временной области хранения СУБД (если hello СУБД это поддерживает). Если требования к операций ввода-ВЫВОДА журнала базы данных hello высоки, toostripe необходимо несколько дисков в порядке tooreach hello операций ввода-ВЫВОДА тома требуется.
* Количество дисков, содержащих один или два файла базы данных из базы данных SAP hello и hello временные файлы данных СУБД также (если hello СУБД это поддерживает).

![Эталонная конфигурация виртуальной машины Azure IaaS для SAP][planning-guide-figure-1300]

[comment]: <> (MShermannd, TODO: опишите структуру Linux )

- - -
> ![Windows][Logo_Windows] Windows
>
> У многих клиентов мы видели конфигурации, where, например, двоичные файлы SAP и СУБД не были установлены на диске c:\ hello, где hello установлена ОС. Обнаружены различные причины, но когда мы вернемся корневой toohello, обычно оказывалось, что hello диски были слишком малы, и обновлениям ОС требовалось дополнительное пространство 10 – 15 лет назад. Оба этих условия в наши дни встречаются редко. Сегодня диск c:\ hello могут быть сопоставлены большого тома дисков или на виртуальных машинах. Это простоту структуры развертываний tookeep заказа, рекомендуется toofollow следующий шаблон развертывания для систем SAP NetWeaver в Azure
>
> файл подкачки операционной системы Windows Hello должен находиться на hello диск D: (временном диске)
>
> ![Linux][Logo_Linux] Linux
>
> Поместите swapfile Linux hello в/mnt/mnt/resource в Linux, как описано в [в этой статье][virtual-machines-linux-agent-user-guide]. файл подкачки Hello можно настроить в файле конфигурации hello hello /etc/waagent.conf агент для Linux. Добавить или изменить hello следующие параметры:
>
>

```
ResourceDisk.EnableSwap=y
ResourceDisk.SwapSizeMB=30720
```

tooactivate hello изменения, необходимо toorestart hello агент Linux с

```
sudo service waagent restart
```

Прочтите Примечание SAP [1597355] для получения дополнительных сведений о hello рекомендуется использовать размер файла подкачки

- - -
Hello количество дисков, используемых для файлов данных СУБД hello и hello тип хранилища Azure, размещенных на этих дисках должно определяться hello IOPS требования и необходимые задержки hello. Точные квоты описаны в [этой][virtual-machines-sizes-linux] (Linux) и [этой статье][virtual-machines-sizes-windows] (Windows).

Взаимодействие с SAP развертываний через hello последние два года при изучении нам некоторых уроках, которые можно описать как:

* Файлы данных toodifferent трафика операций ввода-ВЫВОДА не всегда hello же, поскольку существующие системы клиента может по-разному размера данных файлов, представляющих их баз данных SAP. В результате оказалось лучше использовать конфигурацию RAID через несколько дисков tooplace hello файлов данных, LUN вырезано из тех, toobe. Обнаружены ситуациях, особенно в случае стандартного хранилища Azure, где скорость операций ввода-ВЫВОДА попаданий hello Квота один диск для журнала транзакций СУБД hello. В таких случаях рекомендуется использовать хранилище Premium hello, или в качестве альтернативы статистической обработки нескольких стандартное хранилище дисков с программным RAID.

- - -
> ![Windows][Logo_Windows] Windows
>
> * [Рекомендации по оптимизации производительности SQL Server на виртуальных машинах Azure][virtual-machines-sql-server-performance-best-practices]
>
> ![Linux][Logo_Linux] Linux
>
> * [Настройка программного RAID-массива в Linux][virtual-machines-linux-configure-raid]
> * [Настройка диспетчера логических томов на виртуальной машине Linux в Azure][virtual-machines-linux-configure-lvm]
> * [Секреты хранилища Azure и оптимизация ввода-вывода для Linux](http://blogs.msdn.com/b/igorpag/archive/2014/10/23/azure-storage-secrets-and-linux-i-o-optimizations.aspx)
>
>

- - -
* Хранилище класса Premium демонстрирует значительно более высокую производительность, особенно по критически важному параметру записи журналов транзакций. Для сценариев SAP, произведенным ожидаемый toodeliver как производительности настоятельно рекомендуется toouse Серия виртуальных Машин, которое можно использовать хранилище Azure класса Premium.

Учитывайте этот диск hello, содержащий hello ОС, и как мы рекомендуем hello двоичные файлы SAP и hello базы данных (базовой ВМ), больше не ограниченной too127GB. Он теперь может содержать до too1TB в размере. Это должно быть достаточно места tookeep, все hello, включая необходимый файл, например, журналы пакетных заданий SAP.

Для Дополнительные рекомендации и Дополнительные сведения, особенно для ВМ СУБД, обратитесь к hello [руководство по развертыванию СУБД][dbms-guide]

#### <a name="disk-handling"></a>Управление дисками
В большинстве случаев необходимо toocreate дополнительные диски в базы данных SAP hello toodeploy заказа в hello виртуальной Машины. Мы говорили о вопросах hello на количество дисков в главе [структуры ВМ/диска для развертываний SAP] [ planning-guide-5.5.1] этого документа. Hello Azure портал позволяет tooattach и отключать диски после развертывания базовой ВМ. Hello диски можно подключать и отключать, если hello виртуальная машина работает и запущены, а также при остановке. При подключении диска, hello портал Azure предлагает tooattach пустой диск или существующий диск, который на данный момент времени не присоединен tooanother виртуальной Машины.

**Примечание**: вложенные tooone ВМ диски можно только в любой момент времени.

![Подключение и отключение дисков: служба хранилища Azure класса "Стандартный"][planning-guide-figure-1400]

Во время развертывания hello новой виртуальной машины можно ли вы, чтобы toouse управляемых дисков или разместить на дисках на учетных записях хранения Azure. Если вы хотите toouse хранилище Premium, рекомендуется использовать управляемых дисков.

Далее необходимо toodecide ли при необходимости, tooselect существующий диск, который был отправлен ранее и должен быть подключен toohello ВМ теперь или требуется toocreate новый и пустой диск.

**ВАЖНЫЕ**: вы **не** требуется toouse кэширование узла с помощью стандартного хранилища Azure. Настройки кэша узла hello следует оставить в hello значения по умолчанию. С помощью хранилища Azure Premium следует включить кэширование чтения если характеристик ввода-вывода hello основном чтения как типичные трафик ввода-вывода в файлах данных базы данных. Для файла журнала транзакций базы данных мы рекомендуем не использовать кэширование.

- - -
> ![Windows][Logo_Windows] Windows
>
> [Tooattach данных места на диске в hello портал Azure][virtual-machines-linux-attach-disk-portal]
>
> Если диски подключены, то необходимо toolog в toohello ВМ tooopen hello диспетчера дисков Windows. Если automount не включена, согласно рекомендациям в главе [Установка параметра automount для присоединенных дисков][planning-guide-5.5.3], hello новый подключенный том должен toobe выполнены через Интернет и инициализирована.
>
> ![Linux][Logo_Linux] Linux
>
> Если диски подключены, нужно toolog в toohello ВМ и инициализировать диски hello, как описано в [в данной статье][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]
>
>

- - -
Если новый диск hello пустой диск, потребуется также диск hello tooformat. Для форматирования, особенно для СУБД файлов данных и журналов hello такие же требования для развертывания ОС hello распространяются СУБД.

Как уже упоминалось в главе [hello понятие виртуальной машины Microsoft Azure][planning-guide-3.2], учетная запись хранения Azure не предоставляет неограниченные ресурсы в отношении объем операций ввода-вывода, операций ввода-ВЫВОДА и данных тома. Такие ограничения наиболее критичны для виртуальных машин с СУБД. Может быть лучшим toouse отдельную учетную запись хранилища для каждой виртуальной Машины, если у вас есть несколько высокой toodeploy виртуальных машин для ввода-вывода тома в toostay порядке в пределах "hello" hello тома учетной записи хранилища Azure. В противном случае необходимо toosee как можно сбалансировать эти ВМ между разными учетными записями хранения без прерывания в ограничение hello в каждой отдельной учетной записи хранения. Дополнительные сведения см. в hello [руководство по развертыванию СУБД][dbms-guide]. Эти ограничения должны учитываться и для виртуальных машин, на которых работают только серверы приложения SAP, или других виртуальных машин, для которых позднее могут потребоваться дополнительные виртуальные жесткие диски. Эти ограничения не применяются при использовании управляемого диска. Если планируется toouse хранилище Premium, рекомендуется использовать управляемые диска.

Другой раздел, который используется для учетных записей хранения является ли hello VHD в учетной записи хранилища георепликации. Георепликация включена или отключена на hello уровне учетной записи хранения, а не на hello уровня виртуальной Машины. Если географическая репликация включена, hello VHD в учетной записи хранения будут реплицироваться в другой центр обработки данных Azure в течение приветствия hello одного региона. Прежде чем производить на это, следует подумать о hello следующие ограничения:

Георепликация Azure работает локально в каждый виртуальный жесткий ДИСК на виртуальной машине и не реплицируется IOs hello в хронологическом порядке по нескольким VHD на виртуальной машине. Таким образом hello виртуального жесткого диска, что представляет hello базовой ВМ, а также любые дополнительные VHD, подключенные toohello ВМ, реплицируются независимо друг от друга. Это означает, что синхронизация между изменениями hello в hello не разным VHD. Hello факт, что hello операций ввода-вывода реплицируются независимо от порядка hello, в котором они написаны означает, что георепликация значения для серверов баз данных с базами данных, распределенными по нескольким VHD. В дополнение toohello СУБД также могут существовать другие приложения, где процессы запись или изменение данных в разных VHD, и там, где это порядок hello tookeep важных изменений. Если у вас есть такие приложения, не следует включать георепликацию в Azure. Если в вашей среде нужна георепликация для одного набора виртуальных машин, но не нужна для другого набора, вы можете распределить виртуальные машины и подключенные к ним виртуальные жесткие диски между несколькими учетными записями хранения, для которых георепликация будет включена или отключена.

#### <a name="17e0d543-7e8c-4160-a7da-dd7117a1ad9d"></a>Настройка автоподключения для подключенных дисков
- - -
> ![Windows][Logo_Windows] Windows
>
> Для виртуальных машин, которые создаются из собственных образов или дисков, это необходимые toocheck и возможно установить параметр automount hello. Установка этого параметра позволит hello виртуальной Машины, после перезагрузки или повторного развертывания в Azure toomount hello подключаемые/монтируемые диски автоматически.
> имеет параметр для hello образов, предоставляемых корпорацией Майкрософт в Azure Marketplace hello Hello.
>
> В порядке tooset hello automount Проверьте документацию hello hello командной строки исполняемому diskpart.exe здесь:
>
> * [Параметры командной строки служебной программы DiskPart](https://technet.microsoft.com/library/bb490893.aspx)
> * [Автоподключение](http://technet.microsoft.com/library/cc753703.aspx)
>
> окно командной строки Windows Hello следует открывать от имени администратора.
>
> Если диски подключены, то необходимо toolog в toohello ВМ tooopen hello диспетчера дисков Windows. Если automount не включена, согласно рекомендациям в главе [Установка параметра automount для присоединенных дисков][planning-guide-5.5.3], hello новые подключенные тома > должен toobe выполнены через Интернет и инициализирована.
>
> ![Linux][Logo_Linux] Linux
>
> Необходимо tooinitialize присоединенную пустой диск, как описано в [в этой статье][virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux].
> Необходимо также tooadd новые диски toohello/etc/fstab.
>
>

- - -
### <a name="final-deployment"></a>Окончательное развертывание
Hello окончательного развертывания и точные действия, особенно в отношении toohello развертывания расширенного мониторинга SAP, см. toohello [руководство по развертыванию][deployment-guide].

## <a name="accessing-sap-systems-running-within-azure-vms"></a>Доступ к системам SAP, работающим на виртуальных машинах Azure
При использовании только для облака может потребоваться систем SAP toothose tooconnect через hello общедоступный Интернет с помощью графического интерфейса SAP. В этих случаях hello следующие процедуры должны toobe применения.

Далее в документе hello, мы обсудим hello другие основные сценарии, подключающегося систем tooSAP в конфигурациях между организациями, имеющие подключения сеть сеть (VPN-туннель) или соединение Azure ExpressRoute между локальными hello и системами Azure.

### <a name="remote-access-toosap-systems"></a>Систем tooSAP удаленного доступа
С помощью диспетчера ресурсов Azure по умолчанию конечные точки не больше как в нет hello бывшая классической модели. При соблюдении следующих условий открыты все порты виртуальной машины Azure ARM.

1. Нет группы безопасности сети определяется для hello подсети или сетевого интерфейса hello. TooAzure сетевой трафик виртуальных машин может быть защищен с помощью так называемых «Сетевые группы безопасности». Дополнительные сведения см. в статье [Группа безопасности сети][virtual-networks-nsg].
2. Для сетевого интерфейса hello определен без подсистемы балансировки нагрузки Azure   

Просмотреть hello архитектуры отличаются классической модели и ARM, как описано в [в этой статье][virtual-machines-azure-resource-manager-architecture].

#### <a name="configuration-of-hello-sap-system-and-sap-gui-connectivity-for-cloud-only-scenario"></a>Настройка подключения к системе SAP и графического интерфейса SAP для сценария только для облака hello
См. в этой статье, описывающий сведения о разделе toothis: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/06/24/sap-gui-connection-closed-when-connecting-to-sap-system-in-azure.aspx>

#### <a name="changing-firewall-settings-within-vm"></a>Изменение параметров брандмауэра на виртуальной машине
Может быть необходимости tooconfigure hello брандмауэр на вашей виртуальной машины tooallow внешней системы SAP tooyour трафика.

- - -
> ![Windows][Logo_Windows] Windows
>
> По умолчанию hello брандмауэра Windows в Azure развернутой виртуальной Машины включена. Теперь требуется tooallow hello порта SAP toobe открыт, в противном случае hello SAP GUI не будет возможности tooconnect.
> toodo это:
>
> * Откройте панель управления управления\система и Безопасность\брандмауэр too'Advanced параметры.
> * Щелкните правой кнопкой мыши "Правила для входящих подключений" и выберите "Новое правило".
> * В hello следующие мастера выбрали toocreate нового правила «Порт».
> * Hello следующем шаге мастера hello оставьте параметр hello TCP и введите в нужный номер порта hello tooopen. Наш экземпляр SAP имеет идентификатор 00, поэтому мы выбрали номер порта 3200. Если экземпляр имеет другой номер, должен быть открыт порт hello, заданные ранее зависимости от числа экземпляр hello.
> * В следующей части мастера hello hello необходим tooleave hello элемент «Разрешить подключение» установлен.
> * Hello на следующем шаге мастера hello необходимо toodefine ли hello правило применяется для домена, общедоступной и частной сети. Настройте это необходимые tooyour требуется. Однако подключение с помощью графического интерфейса SAP из hello за пределами через hello общедоступной сети, необходимо toohave hello правило применяется toohello общедоступной сети.
> * В hello последний шаг мастера hello имя правила hello и сохраните изменения, нажав «Готово»
>
> правило Hello вступает в силу немедленно.
>
> ![Определение правила для порта][planning-guide-figure-1600]
>
> ![Linux][Logo_Linux] Linux
>
> Hello изображений Linux в Azure Marketplace hello не включайте hello утилита iptables брандмауэра по умолчанию, которое можно использовать системы SAP tooyour подключения hello. Если включена утилита iptables или другой брандмауэр, см. в документации toohello утилита iptables или hello используется брандмауэр tooallow слишком входящий трафик tcp через порт 32xx (где xx — номер системы hello системы SAP).
>
>

- - -
#### <a name="security-recommendations"></a>Рекомендации по обеспечению безопасности
Hello SAP GUI не подключается сразу tooany экземпляров hello SAP (через порт 32xx), которые выполняются, но сначала он подключается через Привет открыть порт toohello процесса сервера сообщений SAP (порт 36xx). В hello за hello тот же порт использовался сервером сообщений hello для экземпляров приложения toohello hello внутреннего взаимодействия. tooprevent локальные серверы приложений случайно взаимодействие с сервером сообщений в Azure hello внутренние порты связи можно изменить. Настоятельно рекомендуется toochange hello внутренний обмен данными между сервером сообщений SAP hello и его приложения экземпляров tooa другой номер порта в системах, которые были клонированы из локальных систем, таких как клоны системы разработки для тестирования проекта и т. д. Это можно сделать с помощью параметра профиля по умолчанию hello:

> rdisp/msserv_internal
>
>

как описано в документе [параметры безопасности для hello сервером сообщений SAP](https://help.sap.com/saphelp_nwpi71/helpdata/en/47/c56a6938fb2d65e10000000a42189c/content.htm)

## <a name="96a77628-a05e-475d-9df3-fb82217e8f14"></a>Концепция полностью облачного развертывания экземпляров SAP
### <a name="3e9c3690-da67-421a-bc3f-12c520d99a30"></a>Обучающий сценарий с демонстрацией одной виртуальной машины с SAP NetWeaver
![Под управлением одной ВМ SAP демонстрационных систем с hello одинаковыми именами ВМ, изолированных в облачных службах Azure][planning-guide-figure-1700]

В этом сценарии (см главу [только для облака] [ planning-guide-2.1] этого документа) будет реализована типичная обучающая или демонстрационная сценарий системы, где содержится сценарий завершения обучения или демонстрации hello в одной виртуальной Машины. Мы предполагаем, что hello развертывания выполняется с помощью шаблонов образа ВМ. Также предполагается, что несколько развернутых с помощью виртуальных машин с hello hello эти необходимость toobe демонстрационных/обучающих ВМ же имя.

Hello предполагается создан образ виртуальной Машины, как описано в некоторых разделах главе [Подготовка ВМ с SAP для Azure] [ planning-guide-5.2] в настоящем документе.

Hello последовательности событий tooimplement hello сценария выглядит следующим образом:

##### <a name="powershell"></a>PowerShell
* Создайте группу ресурсов для каждого обучающего или демонстрационного ландшафта.

```powershell
$rgName = "SAPERPDemo1"
New-AzureRmResourceGroup -Name $rgName -Location "North Europe"
```
* Создание учетной записи хранилища, если вы не хотите toouse управляемых дисков

```powershell
$suffix = Get-Random -Minimum 100000 -Maximum 999999
$account = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name "saperpdemo$suffix" -SkuName Standard_LRS -Kind "Storage" -Location "North Europe"
```

* Создайте новую виртуальную сеть каждое обучения или демонстрации tooenable альбомная hello использование hello того же имени узла и IP-адреса. Виртуальная сеть Hello защищен сетевой группы безопасности, которая позволяет выполнять только трафик tooport 3389 tooenable удаленного рабочего стола доступа и порт 22 SSH.

```powershell
# Create a new Virtual Network
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGRDP -Protocol * -SourcePortRange * -DestinationPortRange 3389 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 100
$sshRule = New-AzureRmNetworkSecurityRuleConfig -Name SAPERPDemoNSGSSH -Protocol * -SourcePortRange * -DestinationPortRange 22 -Access Allow -Direction Inbound -SourceAddressPrefix * -DestinationAddressPrefix * -Priority 101
$nsg = New-AzureRmNetworkSecurityGroup -Name SAPERPDemoNSG -ResourceGroupName $rgName -Location  "North Europe" -SecurityRules $rdpRule,$sshRule

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix  10.0.1.0/24 -NetworkSecurityGroup $nsg
$vnet = New-AzureRmVirtualNetwork -Name SAPERPDemoVNet -ResourceGroupName $rgName -Location "North Europe"  -AddressPrefix 10.0.1.0/24 -Subnet $subnetConfig
```

* Создать новый общедоступный IP-адрес, который можно использовать tooaccess hello виртуальную машину из hello Интернета

```powershell
# Create a public IP address with a DNS name
$pip = New-AzureRmPublicIpAddress -Name SAPERPDemoPIP -ResourceGroupName $rgName -Location "North Europe" -DomainNameLabel $rgName.ToLower() -AllocationMethod Dynamic
```

* Создание нового сетевого интерфейса для hello виртуальной машины

```powershell
# Create a new Network Interface
$nic = New-AzureRmNetworkInterface -Name SAPERPDemoNIC -ResourceGroupName $rgName -Location "North Europe" -Subnet $vnet.Subnets[0] -PublicIpAddress $pip
```

* Создайте виртуальную машину. Для сценария hello только для облака все ВМ будут иметь hello таким же именем. Hello ИД безопасности SAP hello SAP NetWeaver, экземпляры этих ВМ будут также hello таким же. В рамках hello группы ресурсов Azure, имя hello hello виртуальной Машины требуется уникальный toobe, но в разных группах ресурсов Azure можно запускать ВМ с hello таким же именем. Здравствуйте, «Администратор» по умолчанию учетная запись Windows или 'root' для Linux не допускаются. Таким образом имя пользователя администратора должен toobe определен и пароль. размер Hello hello виртуальной Машины также должен toobe определен.

```powershell
#####
# Create a new virtual machine with an official image from hello Azure Marketplace
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

# select image
$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2012-R2-Datacenter" -Version "latest"
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "SUSE" -Offer "SLES-SAP" -Skus "12-SP1" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "RedHat" -Offer "RHEL" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -PublisherName "Oracle" -Offer "Oracle-Linux" -Skus "7.2" -Version "latest"
# $vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$diskName="osfromimage"
$osDiskUri=$account.PrimaryEndpoints.Blob.ToString() + "vhds/" + $diskName  + ".vhd"

$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Windows
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOSDisk -VM $vmconfig -Name $diskName -VhdUri $osDiskUri -CreateOption fromImage -SourceImageUri <path tooVHD that contains hello OS image> -Linux
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

```powershell
#####
# Create a new virtual machine with a Managed Disk Image
#####
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vmconfig = New-AzureRmVMConfig -VMName SAPERPDemo -VMSize Standard_D11

$vmconfig = Add-AzureRmVMNetworkInterface -VM $vmconfig -Id $nic.Id

$vmconfig = Set-AzureRmVMSourceImage -VM $vmconfig -Id <Id of Managed Disk Image>
$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Windows -ComputerName "SAPERPDemo" -Credential $cred
#$vmconfig = Set-AzureRmVMOperatingSystem -VM $vmconfig -Linux -ComputerName "SAPERPDemo" -Credential $cred

$vmconfig = Set-AzureRmVMBootDiagnostics -Disable -VM $vmconfig
$vm = New-AzureRmVM -ResourceGroupName $rgName -Location "North Europe" -VM $vmconfig
```

* По желанию вы можете добавить дополнительные диски и восстановить необходимое содержимое. Имейте в виду, что все имена больших двоичных объектов (BLOB toohello URL-адреса) должно быть уникальным в пределах Azure.

```powershell
# Optional: Attach additional VHD data disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
$dataDiskUri = $account.PrimaryEndpoints.Blob.ToString() + "vhds/datadisk.vhd"
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -VhdUri $dataDiskUri -DiskSizeInGB 1023 -CreateOption empty | Update-AzureRmVM

# Optional: Attach additional Managed Disks
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name SAPERPDemo
Add-AzureRmVMDataDisk -VM $vm -Name datadisk -DiskSizeInGB 1023 -CreateOption empty -Lun 0 | Update-AzureRmVM
```

##### <a name="cli"></a>Интерфейс командной строки
можно использовать следующий пример кода Hello в Linux. Для Windows, либо используйте PowerShell описанное выше или адаптировать hello пример toouse % rgName % вместо $rgName и задайте переменную среды hello, с помощью команды Windows hello *задать*.

* Создайте группу ресурсов для каждого обучающего или демонстрационного ландшафта.

```
rgName=SAPERPDemo1
rgNameLower=saperpdemo1
az group create --name $rgName --location "North Europe"
```

* Создание новой учетной записи хранения

```
az storage account create --resource-group $rgName --location "North Europe" --kind Storage --sku Standard_LRS --name $rgNameLower
```

* Создайте новую виртуальную сеть каждое обучения или демонстрации tooenable альбомная hello использование hello того же имени узла и IP-адреса. Виртуальная сеть Hello защищен сетевой группы безопасности, которая позволяет выполнять только трафик tooport 3389 tooenable удаленного рабочего стола доступа и порт 22 SSH.

```
az network nsg create --resource-group $rgName --location "North Europe" --name SAPERPDemoNSG
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGRDP --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 3389 --access Allow --priority 100 --direction Inbound
az network nsg rule create --resource-group $rgName --nsg-name SAPERPDemoNSG --name SAPERPDemoNSGSSH --protocol \* --source-address-prefix \* --source-port-range \* --destination-address-prefix \* --destination-port-range 22 --access Allow --priority 101 --direction Inbound

az network vnet create --resource-group $rgName --name SAPERPDemoVNet --location "North Europe" --address-prefixes 10.0.1.0/24
az network vnet subnet create --resource-group $rgName --vnet-name SAPERPDemoVNet --name Subnet1 --address-prefix 10.0.1.0/24 --network-security-group SAPERPDemoNSG
```

* Создать новый общедоступный IP-адрес, который можно использовать tooaccess hello виртуальную машину из hello Интернета

```
az network public-ip create --resource-group $rgName --name SAPERPDemoPIP --location "North Europe" --dns-name $rgNameLower --allocation-method Dynamic
```

* Создание нового сетевого интерфейса для hello виртуальной машины

```
az network nic create --resource-group $rgName --location "North Europe" --name SAPERPDemoNIC --public-ip-address SAPERPDemoPIP --subnet Subnet1 --vnet-name SAPERPDemoVNet
```

* Создайте виртуальную машину. Для сценария hello только для облака все ВМ будут иметь hello таким же именем. Hello ИД безопасности SAP hello SAP NetWeaver, экземпляры этих ВМ будут также hello таким же. В рамках hello группы ресурсов Azure, имя hello hello виртуальной Машины требуется уникальный toobe, но в разных группах ресурсов Azure можно запускать ВМ с hello таким же именем. Здравствуйте, «Администратор» по умолчанию учетная запись Windows или 'root' для Linux не допускаются. Таким образом имя пользователя администратора должен toobe определен и пароль. размер Hello hello виртуальной Машины также должен toobe определен.

```
#####
# Create virtual machines using storage accounts
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --authentication-type password

#####
# Create virtual machines using Managed Disks
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image SUSE:SLES-SAP:12-SP1:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image RedHat:RHEL:7.2:latest --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --image "Oracle:Oracle-Linux:7.2:latest" --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --authentication-type password
```

```
#####
# Create a new virtual machine with a VHD that contains hello private image that you want toouse
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Windows --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --os-type Linux --admin-username <username> --admin-password <password> --size Standard_D11 --use-unmanaged-disk --storage-account $rgNameLower --storage-container-name vhds --os-disk-name os --image <path tooimage vhd> --authentication-type password

#####
# Create a new virtual machine with a Managed Disk Image
#####
az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id>
#az vm create --resource-group $rgName --location "North Europe" --name SAPERPDemo --nics SAPERPDemoNIC --admin-username <username> --admin-password <password> --size Standard_DS11_v2 --os-disk-name os --image <managed disk image id> --authentication-type password
```

* По желанию вы можете добавить дополнительные диски и восстановить необходимое содержимое. Имейте в виду, что все имена больших двоичных объектов (BLOB toohello URL-адреса) должно быть уникальным в пределах Azure.

```
# Optional: Attach additional VHD data disks
az vm unmanaged-disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --vhd-uri https://$rgNameLower.blob.core.windows.net/vhds/data.vhd  --new

# Optional: Attach additional Managed Disks
az vm disk attach --resource-group $rgName --vm-name SAPERPDemo --size-gb 1023 --disk datadisk --new
```

##### <a name="template"></a>Шаблон
Можно использовать шаблоны образец hello на hello azure — начало работы — шаблоны репозитория в github.

* [Простая виртуальная машина Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
* [Простая виртуальная машина Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
* [Виртуальная машина из образа](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)

### <a name="implement-a-set-of-vms-which-need-toocommunicate-within-azure"></a>Реализовать набор виртуальных машин, которым требуется toocommunicate в Azure
Этот сценарий только для облака имеет типичный сценарий для целей обучения или демонстрации, где hello программное обеспечение, представляющее hello обучения или демонстрации сценария распространяется на несколько виртуальных машин. Hello разные компоненты, установленные в разных toocommunicate необходимость виртуальных машин hello друг с другом. В этом сценарии не требуется взаимодействие с локальной сетью или использование распределенного подключения.

Этот сценарий является расширением hello установки, описанные в главах [одной ВМ с SAP NetWeaver обучения или демонстрации сценария] [ planning-guide-7.1] этого документа. В этом случае другие виртуальные машины будут добавлены tooan существующую группу ресурсов. Следующий пример hello обучения альбомная hello состоит из ВМ ASCS/SCS SAP виртуальная машина, работающая СУБД и экземпляр сервера приложений SAP виртуальной Машины.

Перед построением этого сценария необходимо toothink об основных параметров, которые уже были обработаны в сценарии hello до.

#### <a name="resource-group-and-virtual-machine-naming"></a>Имена группы ресурсов и виртуальных машин
Все группы ресурсов должны иметь уникальные имена. Создайте собственную схему именования ресурсов, например `<rg-name`>-суффикс.

имя виртуальной машины Hello имеет toobe уникальным в пределах группы ресурсов hello.

#### <a name="set-up-network-for-communication-between-hello-different-vms"></a>Настройка сети для обмена данными между разными ВМ hello
![Набор виртуальных машин в виртуальной сети Azure][planning-guide-figure-1900]

tooprevent коллизий с клонов из hello же ландшафтов обучения или демонстрации, требуется toocreate виртуальную сеть Azure для каждой альбомной ориентации. Разрешение имен DNS будет предоставлено Azure, или можно настроить собственный DNS-сервер за пределами Azure (не toobe подробнее рассматривается ниже). В нашем сценарии мы не создаем собственную службу DNS. Для всех виртуальных машин в одной виртуальной сети Azure возможно взаимодействие с использованием имен узлов.

Hello причин, по которым ландшафтов обучения или демонстрации tooseparate виртуальных сетей и не только ресурсом группы может быть:

* Hello SAP альбомную в соответствии с потребностями собственный AD/OpenLDAP и сервер домена потребностей toobe часть каждого из ландшафтов hello.  
* Здравствуйте ландшафт SAP, как настроить состоит из компонентов, необходимость toowork с фиксированными IP-адресами.

Дополнительные сведения о виртуальных сетях Azure и как toodefine их можно найти в [в этой статье][virtual-networks-create-vnet-arm-pportal].

## <a name="deploying-sap-vms-with-corporate-network-connectivity-cross-premises"></a>Развертывание виртуальных машин SAP с подключением к корпоративной сети (распределенное развертывание)
Запускается ландшафт SAP и развертывание hello toodivide между ОС для высокопроизводительных серверов СУБД, локальных виртуализированных сред для уровней приложений и небольших двухуровневых настроенных систем SAP и Azure IaaS. Hello базовое предположение заключается в том, что системы SAP в одном ландшафте SAP требуется toocommunicate друг с другом и с многих других компонентов программного обеспечения, развернутые в компании hello, независимо от формы развертывания. Также должно быть различий hello формы развертывания для hello конечного пользователя при соединении с SAP GUI или других интерфейсов. Эти условия можно выполнить только, у нас есть hello в локальной среде Active Directory или OpenLDAP и службы DNS расширенные toohello системы Azure с помощью сайта в узла / /-site подключения или частных соединений, таких как Azure ExpressRoute.

В порядке tooget несколько фоновых hello сведений по реализации SAP в Azure, мы рекомендуем вам главе tooread [понятия только развертывание экземпляров SAP] [ planning-guide-7] этого документа, в котором указано, Некоторые принципов hello конструкции Azure и как их использовать с приложениями SAP в Azure.

### <a name="scenario-of-an-sap-landscape"></a>Сценарий ландшафта SAP
Hello межсетевых локальных ресурсах могут быть примерно описаны как в графики hello ниже:

![Подключение типа "сеть — сеть" между ресурсами в локальной среде и Azure][planning-guide-figure-2100]

Hello сценарий, показанный выше описывает сценарий, где hello в локальной среде AD и OpenLDAP и расширены tooAzure DNS. На стороне локальной hello определенный диапазон IP-адрес зарезервирован на подписку Azure. диапазон IP-адресов Hello будет назначен tooan виртуальной сети Azure на стороне Azure hello.

#### <a name="security-considerations"></a>Вопросы безопасности
Hello минимальные требования составляют hello использование протокола защищенной связи, например SSL/TLS для доступа через браузер или VPN-подключений для системы, получить доступ к toohello Azure службы. Hello предполагается, что компании обрабатывают hello VPN-подключение между своей корпоративной сетью и Azure очень по-разному. Некоторые компании могут полностью открыть все порты hello. Другие компании может потребоваться toobe очень точный какие порты необходимы tooopen и т. д.

В таблице hello ниже типичные SAP перечислены порты связи. По сути это достаточно tooopen hello порт шлюза SAP.

| служба | Имя порта | Пример: `<nn`> = 01 | Диапазон по умолчанию (мин — макс) | Комментарий |
| --- | --- | --- | --- | --- |
| Диспетчер |sapdp`<nn>` см. * |3201 |3200–3299 |Диспетчер SAP, который используется графическим пользовательским интерфейсом SAP для Windows и Java |
| Сервер сообщений |sapms`<sid`> см. ** |3600 |свободный sapms`<anySID`> |sid = идентификатор SAP-System-ID |
| Шлюз |sapgw`<nn`> см. * |3301 |свободный |Шлюз SAP, используемый для взаимодействия CPIC и RFC |
| Маршрутизатор SAP |sapdp99 |3299 |свободный |Только имена CI (Центральный экземпляр) служб могут переназначаться в/etc/Services tooan произвольное значение после установки. |

*) nn = номер экземпляра SAP

**) sid = идентификатор SAP-System-ID

Дополнительные сведения о том, какие порты нужны для различных продуктов и служб SAP, сгруппированные по продуктам SAP, см. здесь: <http://scn.sap.com/docs/DOC-17124>.
В этом документе следует может tooopen выделенной порты в VPN-устройства hello, необходимые для определенных продуктов SAP и сценариев.

Меры безопасности при развертывании виртуальных машин в этом случае может быть toocreate [сетевой группы безопасности] [ virtual-networks-nsg] toodefine правила доступа.

### <a name="dealing-with-different-virtual-machine-series"></a>Работа с виртуальными машинами разных серий
В ходе hello последние 12 месяцев Майкрософт добавила гораздо больше типов ВМ, отличающихся в числа ЦП, памяти или более важными оборудования выполняется на. Не все эти виртуальные машины поддерживаются SAP (поддерживаемые типы виртуальных машин см. в примечании к SAP [1928533]). Некоторые виртуальные машины работают на базовом оборудовании разных поколений. Эти поколения оборудования узла начало развертываются в гранулярности hello объекта Azure единица масштабирования. Означает случаях могут возникнуть где hello вы выбрали не может выполняться на различных размеров виртуальных Машин hello же единице измерения. Группа доступности имеет ограничения по toospan возможность hello, единицы масштабирования на основе оборудования.  Для одной системы SAP или разных систем SAP в разных наборах доступности, например, если вы хотите toorun hello СУБД на виртуальных машинах A5 A11 hello уровня приложения SAP на виртуальных машинах серии G, то вам будет принудительного toodeploy.

#### <a name="printing-on-a-local-network-printer-from-sap-instance-in-azure"></a>Печать на принтере локальной сети из экземпляра SAP в Azure
##### <a name="printing-over-tcpip-in-cross-premises-scenario"></a>Печать по протоколу TCP/IP в распределенном сценарии
Настройка сетевые принтеры на основе TCP/IP в локальной среде на виртуальной Машине Azure является общей hello таким же, как в корпоративной сети, при условии, что имеется туннель VPN-сайтами или установленное соединение ExpressRoute.

- - -
> ![Windows][Logo_Windows] Windows
>
> toodo это:
>
> * Некоторые сетевые принтеры поставляются с мастером настройки, который позволяет легко tooset принтера на виртуальной Машине Azure. Если ни одна из программ мастера были переданы с принтера hello «manual» способ tooset hello принтера является toocreate новый порт принтера TCP/IP.
> * Откройте "Панель управления", затем "Устройства и принтеры" -> "Установка принтера".
> * Выберите "Добавить принтер с использованием TCP/IP-адреса или имени узла".
> * Введите IP-адрес принтера hello hello
> * Стандартный порт принтера — 9100.
> * При необходимости вручную установите hello соответствующий драйвер принтера.
>
> ![Linux][Logo_Linux] Linux
>
> * как и для Windows просто следуйте стандартной процедуре hello tooinstall сетевого принтера
> * просто выполните hello открытый руководства по Linux для [SUSE](https://www.suse.com/documentation/sles-12/book_sle_deployment/data/sec_y2_hw_print.html) или [Red Hat и Oracle Linux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/sec-Printer_Configuration.html) о том, как tooadd принтера.
>
>

- - -
![Сетевая печать][planning-guide-figure-2200]

##### <a name="host-based-printer-over-smb-shared-printer-in-cross-premises-scenario"></a>Доступ по протоколу SMB к принтеру на основе узла (общему принтеру) в распределенном сценарии
Принтеры на основе узла нарочно не являются сетевыми. Но принтер на основе узла могут использоваться совместно компьютеров в сети, пока принтер hello подключенных tooa включении компьютера. Подключитесь к корпоративной сети с помощью подключения "сеть — сеть" или ExpressRoute, и вы сможете совместно использовать локальный принтер. Hello протокол SMB использует NetBIOS вместо DNS в качестве службы имен. Hello NetBIOS-имя узла может отличаться от hello DNS-имя узла. Hello обычно являются идентичными hello NetBIOS-имя узла и имя узла DNS hello. Hello DNS-домена не имеет смысла в пространстве имен NetBIOS hello. Здравствуйте, соответственно, полное имя узла DNS, состоящее из имени узла DNS hello и DNS-домена не должен использоваться в пространстве имен NetBIOS hello.

общий ресурс печати Hello идентифицируется по уникальному имени в сети hello:

* Имя сервера SMB hello (всегда требуется).
* Имя общего ресурса hello (всегда требуется).
* Имя домена hello, если общий принтер не hello домену, в системе SAP.
* Кроме того имя пользователя и пароль может быть обязательным tooaccess общего принтера hello.

Практическое руководство:

- - -
> ![Windows][Logo_Windows] Windows
>
> Включите общий доступ к локальному принтеру.
> В hello виртуальной Машине Azure откройте проводник Windows hello и введите имя общего ресурса hello hello принтера.
> Мастер установки принтера проведет через процесс установки hello.
>
> ![Linux][Logo_Linux] Linux
>
> Ниже приведены некоторые примеры документации, посвященной настройке сетевых принтеров в Linux или содержащей разделы о печати в Linux. Он будет работать hello одинаково на виртуальной Машине Linux Azure, при условии, что hello виртуальная машина является частью виртуальной частной сети:
>
> * SLES <https://en.opensuse.org/SDB:Printing_via_SMB_(Samba)_Share_or_Windows_Share>
> * RHEL или Oracle Linux <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Printer_Configuration.html#s1-printing-smb-printer>
>
>

- - -
##### <a name="usb-printer-printer-forwarding"></a>USB-принтер (переадресация принтеров)
В Azure hello возможность пользователям доступ hello служб удаленных рабочих столов tooprovide hello tootheir локальным устройствам печати в удаленном сеансе не доступна.

- - -
> ![Windows][Logo_Windows] Windows
>
> Дополнительные сведения о печати в Windows можно найти здесь: <http://technet.microsoft.com/library/jj590748.aspx>.
>
>

- - -
#### <a name="integration-of-sap-azure-systems-into-correction-and-transport-system-tms-in-cross-premises"></a>Интеграция систем SAP Azure в систему исправлений и транспортировки (TMS) при распределенном развертывании
Здравствуйте SAP Change and Transport System (TMS) tooexport toobe настроен потребностей и импорта транспортных запросов в системах в альбомной ориентации hello. Мы предполагаем, что hello экземпляры разработки системы SAP (DEV) расположены в Azure, в то время как hello качества (QA) и производственные системы (PRD) являются локальными. Кроме того, мы предполагаем, что существует централизованный транспортный каталог.

##### <a name="configuring-hello-transport-domain"></a>Настройка транспортного домена hello
Настройте транспортный домен в качестве hello контроллера транспортного домена, как описано в системе hello [hello Настройка контроллера домена транспорта](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm). Пользователь системы TMSADM будет создана и hello обязательные назначения RFC будет создан. Можно проверить эти подключения RFC с помощью hello транзакции SM59. Для вашего транспортного домена должно быть включено разрешение имен узлов.

Практическое руководство:

* В нашем сценарии мы решили hello в локальной системе QAS будет контроллера домена CTS hello. Выполните транзакцию STMS. Откроется диалоговое окно TMS Hello. Откроется диалоговое окно "Настройка транспортного домена". (Это диалоговое окно отображается только в том случае, если транспортный домен еще не настроен).
* Убедитесь, что этот пользователь автоматически создается hello TMSADM авторизован (SM59 -> ABAP Connection -> TMSADM@E61.DOMAIN_E61 -> сведения -> Utilities(M) -> Authorization Test). Hello начальный экран транзакции STMS должен показывать, что эта система SAP теперь функционирует hello контроллером домена транспорта hello, как показано ниже:

![Начальный экран транзакции STMS в контроллере домена hello][planning-guide-figure-2300]

#### <a name="including-sap-systems-in-hello-transport-domain"></a>Включение систем SAP в транспортный домен hello
Hello последовательность включения системы SAP в транспортный домен выглядит следующим образом:

* На hello системе DEV в Azure перейдите toohello транспортную систему (клиент 000) и вызовите транзакцию STMS. Выберите другие конфигурацию в диалоговое окно «hello» и продолжите Include System in Domain. Укажите hello контроллера домена в качестве конечного узла ([включая систем SAP в транспортный домен hello](http://help.sap.com/erp2005_ehp_04/helpdata/en/44/b4a0c17acc11d1899e0000e829fbbd/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm)). Hello система больше не включены в транспортный домен hello toobe ожидания.
* По соображениям безопасности имеется tooconfirm контроллера домена назад toohello toogo ваш запрос. Нажмите кнопку Обзор системы и утвердить hello ожидания системы. Затем убедитесь, что будут распространяться настройки строки и hello hello.

Эта система SAP теперь содержит hello необходимых сведений о hello всех прочих системах SAP в транспортный домен hello. В hello же время hello адрес отправки данных новой системы SAP hello tooall hello других систем SAP и ввода hello системы SAP в транспортный профиль программы управления транспортом hello hello. Проверьте, работают ли RFC и доступ к каталогу транспорта toohello hello домена.

Продолжить настройку hello транспортной системы как обычно, как описано в документации hello [Change and Transport System](http://help.sap.com/saphelp_nw70ehp3/helpdata/en/48/c4300fca5d581ce10000000a42189c/content.htm?frameset=/en/44/b4a0b47acc11d1899e0000e829fbbd/frameset.htm).

Практическое руководство:

* Убедитесь, что локальная система STMS настроена правильно.
* Убедитесь, что имя узла hello hello Transport Domain Controller можно решить с виртуальной машиной в Azure и наоборот.
* Call transaction STMS (Вызов транзакции STMS) -> Other Configuration (Другие настройки) -> Include System in Domain (Включить систему в домен).
* Подтверждение соединения hello в hello в локальную систему TMS.
* Настройте транспортные маршруты, группы и уровни как обычно.

В сеть сеть подключенных между организациями сценариев, hello задержки между локальной средой и Azure по-прежнему может быть значительной. Если мы выполните hello последовательность транспортировки объектов tooproduction систем разработки и тестирования или думаем о применении транспорта или поддержки пакетов toohello различных систем, вам следует учесть, что, зависимые от расположения главного транспортного hello hello каталог, некоторые из систем hello столкнутся большое значение задержки чтения или записи данных в главном транспортном каталоге hello. Hello ситуация — конфигурациями альбомная tooSAP, где hello разные системы распределяются по разных центрах обработки данных со значительной расстояние между центрами обработки данных hello.

В порядок toowork вокруг такую задержку и систем hello работать быстро в чтением или записью tooor в транспортном каталоге hello, можно настроить два домена STMS транспорта (для локальных. и с системами hello в доменах транспорта hello Azure и ссылка В следующей документации с объяснением hello принципы этой концепции в SAP TMS hello: <http://help.sap.com/saphelp_me60/helpdata/en/c4/6045377b52253de10000009b38f889/content.htm?frameset=/en/57/ 38dd924eb711d182bf0000e829fbfe/FRAMESET.htm>.

Практическое руководство:

* Настройте транспортный домен в каждом расположении (локально и в Azure) с использованием транзакции STMS <http://help.sap.com/saphelp_nw70ehp3/helpdata/en/44/b4a0b47acc11d1899e0000e829fbbd/content.htm>
* Связать hello домена с помощью связи доменов и подтвердите hello связь между двумя доменами hello.
  <http://help.sap.com/saphelp_nw73ehp1/helpdata/en/a3/139838280c4f18e10000009b38f8cf/content.htm>
* Распространите hello конфигурации связанного toohello систему.

#### <a name="rfc-traffic-between-sap-instances-located-in-azure-and-on-premises-cross-premises"></a>Трафик RFC между экземплярами SAP в Azure и в локальной среде (распределенное развертывание)
Трафик RFC между системами, которые являются локальными, так и в Azure должен toowork. tooset соединение вызовите транзакцию SM59 в исходной системе которых требуется toodefine соединение RFC hello целевой системы. Конфигурация Hello — примерно toohello стандартной установки соединения RFC.

Мы предполагаем, что в сценарии между организациями hello hello виртуальные машины принадлежат какие выполнения систем SAP, которым требуется toocommunicate друг с другом hello того же домена. Поэтому hello установки соединения RFC между системами SAP не отличаются от действий по настройке hello и входных данных в локальных сценариев.

#### <a name="accessing-local-fileshares-from-sap-instances-located-in-azure-or-vice-versa"></a>Доступ к локальным общим папкам из экземпляров SAP, размещенных в Azure, и наоборот
Экземплярам SAP, размещенным в Azure должны tooaccess файловые ресурсы, которые находятся в пределах корпоративной локальной среде hello. Кроме того на локальных экземплярах SAP должны tooaccess общих папок, расположенных в Azure. tooenable hello общие файловые ресурсы необходимо настроить разрешения hello и параметров общего доступа в локальной системе hello. Убедитесь, что порты hello tooopen на hello VPN или подключение ExpressRoute между Azure и центра обработки данных.

## <a name="supportability"></a>Возможности поддержки
### <a name="6f0a47f3-a289-4090-a053-2521618a28c3"></a>Решение мониторинга Azure для SAP
В порядке tooenable hello мониторинг критически важных систем SAP в Azure hello SAP средств мониторинга SAPOSCOL или SAP Host Agent получают данные из hello узла службы виртуальной машины Azure с помощью расширения мониторинга Azure для SAP. Поскольку hello требования по SAP были tooSAP конкретных приложений, корпорация Майкрософт решила не toogenerically реализуйте hello необходимые функциональные возможности в Azure, но оставить его для клиентов toodeploy hello необходимые мониторинга компонентов и конфигураций tootheir Виртуальные машины в Azure. Тем не менее развертывание и управление жизненным циклом компонентов мониторинга hello будет в значительной степени автоматизировано Azure.

#### <a name="solution-design"></a>Архитектура решения
решение Hello разработала tooenable мониторинга SAP основана на архитектуре агента ВМ Azure и инфраструктуры расширений hello. Идея Hello hello агента ВМ Azure и инфраструктуры расширений представляет tooallow установку программного обеспечения приложения hello галереи расширений ВМ Azure в виртуальной Машине. Здравствуйте, принцип идея этой концепции является tooallow (в случаях, таких как hello расширения мониторинга Azure для SAP), hello развертывание специальной функциональности в ВМ и hello конфигурации такого программного обеспечения во время развертывания.

Здравствуйте, «Агента ВМ Azure», позволяющий обработку специальных расширений ВМ Azure в рамках ВМ встраивается в ВМ Windows по умолчанию для создания виртуальной Машины hello портал Azure приветствия. В случае SUSE, Red Hat или Oracle Linux агент виртуальной Машины hello уже образ Azure Marketplace. В случае, если один будет передать виртуальную Машину Linux агента ВМ локально tooAzure hello имеет toobe установлен вручную.

Здравствуйте базовые структурные элементы решения мониторинг hello в Azure для SAP выглядит следующим образом:

![Компоненты расширения Microsoft Azure][planning-guide-figure-2400]

Как показано в hello блок-схема выше одной части hello решение по мониторингу для SAP размещается в hello образа виртуальной Машины Azure и Azure галереи расширений, который является глобально реплицируемым репозиторием, управляемым операциями Azure. Он несет hello hello совместные SAP/MS, занимающейся hello Azure реализацию SAP toowork с операциями Azure toopublish новых версий расширения мониторинга Azure для SAP hello.

При развертывании новой виртуальной Машины Windows hello «Агента ВМ Azure» автоматически добавляется в hello виртуальной Машины. функция Hello этого агента — toocoordinate hello Загрузка и настройка hello расширений Azure для мониторинга систем SAP NetWeaver. Для виртуальных машин Linux hello агента ВМ Azure уже hello образ ОС Azure Marketplace.

Однако имеется шаг, который все еще требуется toobe исполнен hello клиента. Это hello включения и настройки сбора данных о производительности hello. Hello процесс, связанный с toohello «конфигурация» выполняется автоматически CLI команд или сценария PowerShell. Hello сценарий PowerShell можно загрузить в центре скриптов Microsoft Azure hello согласно инструкциям hello [руководство по развертыванию][deployment-guide].

Hello общая архитектура hello Azure решение по мониторингу для SAP выглядит следующим образом.

![Решение мониторинга Azure для SAP NetWeaver][planning-guide-figure-2500]

**Для hello точное как tooand подробное описание процедуры использования этих командлетов PowerShell или интерфейса командной во время развертывания, выполните hello инструкциями, приведенными в hello [руководство по развертыванию][deployment-guide].**

### <a name="integration-of-azure-located-sap-instance-into-saprouter"></a>Интеграция в SAProuter экземпляра SAP, размещенного в Azure
Экземпляры SAP, работающие в Azure должны toobe доступен из SAProuter также.

![Сетевое подключение с помощью SAP-Router][planning-guide-figure-2600]

SAProuter позволяет hello взаимодействие по протоколу TCP/IP между участвующими системами, если отсутствует прямое соединение IP. Это обеспечивает преимущество hello, что на уровне сети нет конца в конец соединения между участниками обмена данными hello не требуется. Hello SAProuter прослушивает порт 3299 по умолчанию.
экземпляры tooconnect SAP через SAProuter требуется hello toogive строка SAProuter и имя узла с любой tooconnect попытки.

## <a name="sap-netweaver-as-java"></a>SAP NetWeaver AS Java
Пока hello фокус hello документ был SAP NetWeaver в целом или hello стек SAP NetWeaver ABAP. В этом небольшом разделе перечислены специальные рекомендации для стека SAP Java hello. Одно из наиболее важные SAP NetWeaver Java исключительно на основе приложения hello — hello корпоративный портал SAP. На основе других SAP NetWeaver приложений, как если бы SAP PI и SAP Solution Manager hello SAP NetWeaver ABAP и Java стеки. Таким образом определенно нет необходимости tooconsider определенные аспекты связанных toohello стеком Java SAP NetWeaver также.

### <a name="sap-enterprise-portal"></a>Корпоративный портал SAP
Hello Установка портала SAP в виртуальных машинах Azure не отличается от на локальные установки при развертывании в сценариях между организациями. С момента приветствия DNS выполняется локально можно сделать hello параметры порта отдельных экземпляров hello как настроенные в локальной среде. Hello рекомендации и ограничения, описанные в этом документе, пока относятся к приложениям как корпоративный портал SAP или hello стека SAP NetWeaver Java в целом.

![Портал SAP][planning-guide-figure-2700]

Сценарий развертывания, некоторые клиенты — hello прямой раскрытия toohello корпоративный портал SAP hello Интернета, а hello узла виртуальной машины — подключенных toohello корпоративной сети через туннель VPN или ExpressRoute сайт сайт. Такой сценарий у вас есть toomake том, что определенные порты, открытые и не заблокирован брандмауэром или сетевой группы безопасности. Hello же механизм необходимо toobe применяется, когда требуется экземпляр SAP Java tooan tooconnect из локального в сценарии только для облака.

Hello исходный URI портала — HTTP (s):`<Portalserver`>: 5XX00/irj, где порт hello сформированное 50000 плюс (Номер_системы × 100). Hello по умолчанию портала URI для системы SAP 00 — `<dns name`>.`<azure region` >.Cloudapp.azure.com:PublicPort/irj. Дополнительные сведения см. здесь: <http://help.sap.com/saphelp_nw70ehp1/helpdata/de/a2/f9d7fed2adc340ab462ae159d19509/frameset.htm>.

![Настройка конечной точки][planning-guide-figure-2800]

Если вы хотите toocustomize hello URL-адрес или порты корпоративного портала SAP, см. в этой документации:

* [Change Portal URL (Изменение URL-адреса портала)](http://wiki.scn.sap.com/wiki/display/EP/Change+Portal+URL)
* [Change Default port numbers, Portal port numbers (Изменение номеров портов по умолчанию и номеров портов портала)](http://wiki.scn.sap.com/wiki/display/NWTech/Change+Default++port+numbers%2C+Portal+port+numbers)

## <a name="high-availability-ha-and-disaster-recovery-dr-for-sap-netweaver-running-on-azure-virtual-machines"></a>Высокая доступность и аварийное восстановление для SAP NetWeaver на виртуальных машинах Azure
### <a name="definition-of-terminologies"></a>Определение терминов
Термин Hello **высокий уровень доступности (HA)** обычно связанные tooa задано технологий, которая сводит к минимуму перерывы в ИТ, предоставляя непрерывности ИТ-услуг через избыточности, отказоустойчивый или отработки отказа защищенные компоненты внутри hello **же** центра обработки данных. (в нашем случае — в одном регионе Azure).

**Аварийное восстановление** также предназначено для минимизации перебоев в работе ИТ-служб и их восстановления, но в **разных** центрах обработки данных, которые обычно находятся за сотни километров друг от друга. В нашем случае обычно от разных регионах Azure в течение hello же геополитические регионе или в соответствии с параметром вас как клиента.

### <a name="overview-of-high-availability"></a>Общие сведения о высокой доступности
Можно разделить hello обсуждение высокого уровня доступности SAP в Azure на две части:

* **Высокая доступность инфраструктуры Azure**, например высокая доступность вычислений (на виртуальных машинах), сети, хранилища и т. д. и ее преимущества для увеличения доступности приложений SAP.
* **Высокая доступность приложений SAP**, например высокая доступность программных компонентов SAP:
  * серверов приложений SAP,
  * экземпляров ASCS/SCS SAP,
  * сервера базы данных,

а также ее совместное использование с высокой доступностью инфраструктуры Azure.

Высокого уровня доступности SAP в Azure есть некоторые различия по сравнению tooSAP высокого уровня доступности, в локальной физической или виртуальной среде. Hello следующие документе SAP описываются стандартные конфигурации высокого уровня доступности SAP в виртуализированных средах Windows: <http://scn.sap.com/docs/DOC-44415>. Конфигурации высокой доступности SAP, интегрированной с SAPinst, для Linux (такой же, как для Windows) не существует. Сведения о высокой доступности SAP в локальной среде Linux см. здесь: <http://scn.sap.com/docs/DOC-8541>.

### <a name="azure-infrastructure-high-availability"></a>Высокая доступность инфраструктуры Azure
В настоящее время предоставляется соглашение SLA для одной ВМ с временем бесперебойной работы на уровне 99,9 %. представление tooget hello доступность одной виртуальной Машины выглядит так, можно просто построить произведение hello hello разные доступные SLA Azure: <https://azure.microsoft.com/support/legal/sla/>.

Hello основа для расчета hello — 30 дней в месяц или 43200 минут. Таким образом, время простоя 0,05% соответствует too21.6 минут. Как обычно доступности hello hello различных служб будет умножить в hello следующими способами:

(Доступность службы 1 / 100) * (доступность службы 2 / 100) * (доступность службы 3 / 100) *…

Например:

(99,95 / 100) * (99,9 / 100) * (99,9 / 100) = 0,9975, или общая доступность 99,75 %.

#### <a name="virtual-machine-vm-high-availability"></a>Высокая доступность виртуальных машин (ВМ)
Существует два типа событий платформы Azure, которые могут повлиять на доступность виртуальных машин hello: планового обслуживания и незапланированных обслуживания.

* События планового обслуживания, периодические обновления, внесенные программой Microsoft toohello базовой платформы Azure tooimprove общую надежность, производительность и безопасность инфраструктуры платформы hello, работать виртуальные машины.
* Происходить случаи внепланового обслуживания при сбое оборудования hello или основной виртуальной машины физической инфраструктуры иным образом. Это могут быть сбои локальной сети или локальных жестких дисков, а также другие ошибки на уровне стойки. При обнаружении такой сбой hello платформы Azure автоматически перенести виртуальную машину из hello неработоспособный физический сервер размещения виртуальной машины tooa работоспособности физического сервера. Такие события происходят редко, но также может привести к tooreboot виртуальной машины.

Дополнительные сведения можно найти в этой документации: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="azure-storage-redundancy"></a>Избыточность хранилища Azure
Hello данных вашей учетной записи хранилища Microsoft Azure всегда является реплицированной tooensure устойчивость и высокого уровня доступности и следовании hello об уровне ОБСЛУЖИВАНИЯ хранилища Azure, даже при временных сбоях оборудования лицо hello.

Так как хранилище Azure сохраняет три изображения hello данных по умолчанию, RAID5 или RAID1 на нескольких дисках Azure не обязательны.

Дополнительные сведения найти в этой документации: <http://azure.microsoft.com/documentation/articles/storage-redundancy/>

#### <a name="utilizing-azure-infrastructure-vm-restart-tooachieve-higher-availability-of-sap-applications"></a>Использование инфраструктуры Azure ВМ перезапускается tooAchieve «высокий» доступности приложений SAP
Если вы решите не toouse функции например Server отказоустойчивой кластеризации Windows (WSFC) или Pacemaker в Linux (в настоящее время поддерживается только для SLES 12 и более поздней версии), перезапустите виртуальную Машину Azure — загруженные tooprotect систему SAP от запланированных и незапланированных простоев hello Инфраструктура Azure физического сервера и общей базовой платформы Azure.

> [!NOTE]
> Это важные toomention, что перезапуск виртуальной Машины Azure в основном защищает виртуальные машины и не приложения. Перезапуск виртуальной машины не гарантирует высокую доступность приложений SAP, но обеспечивает определенный уровень доступности инфраструктуры, а значит — опосредованно — и более высокую доступность систем SAP. Имеется также нет соглашения об уровне ОБСЛУЖИВАНИЯ для hello времени toorestart виртуальной Машины после сбоя узла плановой или незапланированной. Таким образом, этот метод обеспечения высокой доступности не подходит для критически важных компонентов системы SAP, таких как (A)SCS или СУБД.
>
>

Другой элемент инфраструктуры, важный для обеспечения высокой доступности, — хранилище. Например, в соглашении об уровне обслуживания хранилища Azure указана доступность 99,9 %. Если пользователь развернет все виртуальные машины с содержащимися на них дисками в одной учетной записи хранения Azure, потенциальная недоступность хранилища Azure приведет к недоступности всех виртуальных машин, размещенных в этой учетной записи хранения Azure, а также всех компонентов SAP, выполняющихся на этих виртуальных машинах.  

Вместо размещения всех виртуальных машин в одной учетной записи хранения Azure можно также использовать выделенные учетные записи хранения для каждой виртуальной машины и таким образом повысить общую доступность виртуальных машин и приложения SAP с помощью нескольких независимых учетных записей хранения Azure.

Диски Azure управляемых автоматически помещаются в hello домен сбоя hello виртуальной машины, к которым они присоединены. При наличии двух виртуальных машин в группе доступности задать и использовать управляемые диски, hello платформы берет на себя распространение hello управляемых дисков в других доменах сбоя также. Если планируется toouse хранилище Premium, настоятельно рекомендуется использовать Управление дисками также.

Пример архитектуры системы SAP NetWeaver, в которой используется высокая доступность инфраструктуры Azure и учетные записи хранения:

![Использование инфраструктуры Azure «выше» доступности SAP tooachieve приложений высокого уровня ДОСТУПНОСТИ][planning-guide-figure-2900]

Пример архитектуры системы SAP NetWeaver, в которой используется высокая доступность инфраструктуры Azure и управляемые диски:

![Использование инфраструктуры Azure «выше» доступности SAP tooachieve приложений высокого уровня ДОСТУПНОСТИ][planning-guide-figure-2901]

Для важных компонентов SAP добиться hello пока следующие:

* Высокая доступность серверов приложений (AS) SAP

  Экземпляры серверов приложений SAP являются избыточными компонентами. Каждый экземпляр SAP AS развертывается на отдельной виртуальной машине, которая работает в отдельных домене сбоя и домене обновления Azure (см. разделы [Домены сбоя][planning-guide-3.2.1] и [Домены обновления][planning-guide-3.2.2]). Это обеспечивается за счет групп доступности Azure (см. раздел [Группы доступности Azure][planning-guide-3.2.3]). Потенциальная недоступность домена сбоя или обновления Azure (запланированная или незапланированная) приведет к недоступности ограниченного количества виртуальных машин и их экземпляров SAP AS.

  Если каждый экземпляр SAP AS помещается в отдельную учетную запись хранения Azure, потенциальная недоступность одной учетной записи хранения Azure приведет к недоступности только одной виртуальной машины и соответствующего экземпляра SAP AS. Однако учтите, что существует ограничение на число учетных записей хранения Azure в рамках одной подписки Azure. автоматический запуск tooensure (A) SCS экземпляра после перезагрузки hello виртуальной Машины, убедитесь, что tooset Autostart, параметр hello в экземпляре (A) SCS запускаете профиля, описанные в главах [использование автозапуска экземпляров SAP] [ planning-guide-11.5].
  Дополнительные сведения см. в разделе [Высокая доступность серверов приложений SAP][planning-guide-11.4.1].

  Даже при использовании управляемых дисков эти диски также сохраняются в учетной записи хранения Azure и могут быть недоступны в случае сбоя хранилища.

* *Повышение* доступности экземпляра SAP (A)SCS

  Здесь мы используем hello Azure ВМ перезапускается tooprotect виртуальной Машины с помощью установленного экземпляра SAP (A) SCS. В hello случай запланированных и незапланированных простоев Azure серверов, виртуальных машин будет перезапущена на другой доступный сервер. Как упоминалось ранее, в первую очередь перезапуск виртуальной Машины Azure защищает виртуальные машины и не приложений, в данном случае hello (A) SCS экземпляра. Через hello ВМ перезапускается мы свяжемся косвенно «высокий» доступности экземпляра SAP (A) SCS. автоматический запуск tooinsure (A) SCS экземпляра после перезагрузки hello виртуальной Машины, убедитесь, что tooset Autostart, параметр экземпляра (A) SCS запускаете профиля, описанные в главах [использование автозапуска экземпляров SAP][planning-guide-11.5]. Это означает, что hello (A) SCS, работающий как единственная точка отказа (SPOF) в одной виртуальной Машины будет определяющим фактором доступности всего ландшафта SAP hello hello hello.

* *Повышение* доступности сервера СУБД

  Здесь аналогичный экземпляр SAP (A) SCS toohello вариант использования, мы используем перезапуск виртуальной Машины Azure tooprotect hello виртуальной Машины с программным обеспечением СУБД и мы более «высокая доступность» СУБД программного обеспечения посредством перезапуск виртуальной Машины.
  СУБД, работающих в одной виртуальной Машины также SPOF и является определяющим фактором доступности всего ландшафта SAP hello hello hello.

### <a name="sap-application-high-availability-on-azure-iaas"></a>Высокая доступность приложений SAP в Azure IaaS
tooachieve полного SAP системы высокого уровня доступности, мы должны tooprotect все важные компоненты системы SAP для примера избыточных серверов приложений SAP, а уникальные компоненты (например единственная точка отказа), например экземпляра SAP (A) SCS и СУБД.

#### <a name="5d9d36f9-9058-435d-8367-5ad05f00de77"></a>Высокая доступность серверов приложений SAP
Для экземпляров серверов-диалоговое окно приложения hello SAP не требуется toothink о конкретных высокого уровня доступности. Высокая доступность достигается за счет простой избыточности и, как следствие, достаточного количества серверов на разных виртуальных машинах. Они должна быть размещена в одной группе доступности Azure tooavoid, hello виртуальные машины могут обновляться на hello hello одновременно во время планового обслуживания. Hello базовую функциональность, построенная на различные обновления и домены отказоустойчивости в единице масштабирования Azure уже был введен в главе [домены обновления][planning-guide-3.2.2]. Группы доступности Azure были описаны в разделе этого документа [Группы доступности Azure][planning-guide-3.2.3].

Количество доменов сбоя и обновления, которые можно использовать в группе доступности Azure в единице масштабирования Azure, не бесконечно. Это означает, что помещается число виртуальных машин в одной группе доступности, рано или поздно более одной виртуальной Машины в конце hello же сбоя или обновление домена.

Развертывание нескольких сервера приложений SAP экземпляров в их выделенные виртуальные машины, и при условии, что мы получили 5 доменами обновления, hello следующий рисунок появляется в конце hello. Hello фактическое максимальное число доменов сбоя и обновления в наборе доступности может измениться в будущих hello:

![Высокая доступность серверов приложений SAP в Azure][planning-guide-figure-3000]

Дополнительные сведения можно найти в этой документации: <http://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability>

#### <a name="high-availability-for-hello-sap-ascs-instance-on-windows"></a>Высокий уровень доступности для экземпляра SAP (A) SCS hello в Windows
Отказоустойчивого кластера (WSFC) является экземпляром SAP (A) SCS hello tooprotect часто используемых решений. Он также интегрируется в SAPinst в форме "установки с высокой доступностью". На данный момент времени hello инфраструктуры Azure не может tooprovide hello функциональные возможности tooset копирование hello hello необходимые отказоустойчивого кластера Windows Server так же, как это можно сделать локально.

По состоянию на январь 2016 г. hello Azure облачной платформы операционной системы Windows hello не предоставляет возможность использования в общий том кластера на диске, совместно используется двумя виртуальными машинами Azure hello.

Хотя приемлемым решением является hello об использовании программного обеспечения сторонних поставщиков, предоставляющий общего тома репликацией синхронной, так и прозрачный диска, которая может быть интегрирован в WSFC. Этот подход неявно подразумевает, что этой только hello активный узел кластера может tooaccess копирует один диск hello в момент времени. По состоянию на январь 2016 г. Этот высокого уровня ДОСТУПНОСТИ конфигурации является экземпляром SAP (A) SCS hello поддерживается tooprotect на гостевую ОС Windows на виртуальных машинах Azure в сочетании с программным обеспечением сторонних поставщиков SIOS DataKeeper.

Hello SIOS DataKeeper решение предоставляет tooWindows ресурса кластера общего диска отказоустойчивых кластеров, задав:

* Дополнительный виртуальный жесткий ДИСК Azure присоединенного tooeach hello виртуальных машин (ВМ), в конфигурации кластера Windows
* SIOS DataKeeper Cluster Edition работает на обоих узлах виртуальных машин.
* Наличие SIOS DataKeeper Cluster Edition настроен таким образом, она отражает синхронно hello содержимое hello дополнительные VHD, подключенный том с источника tooadditional виртуальных машин подключен виртуальный жесткий ДИСК тома целевой виртуальной Машины.
* SIOS DataKeeper абстрагирования hello исходных и целевых локальных томов и презентация их tooWindows отказоустойчивого кластера как один общий диск.

Можно найти все сведения о том, как tooinstall отказоустойчивого кластера Windows с помощью SIOS DataKeeper и SAP в hello [кластеризация экземпляра SAP ASCS с использованием отказоустойчивых кластеров Windows Server в Azure с помощью sios DataKeeper] [ ha-guide-classic]Технический документ.

#### <a name="high-availability-for-hello-sap-ascs-instance-on-linux"></a>Высокий уровень доступности для экземпляра SAP (A) SCS hello в Linux
Начиная с декабря 2015 также отсутствует диск эквивалентные tooshared WSFC для виртуальных машин Linux в Azure. Альтернативные решения, использующие стороннее программное обеспечение, например SIOS для Windows, для работы с SAP на платформе Linux в Azure еще не проверены.

#### <a name="high-availability-for-hello-sap-database-instance"></a>Высокий уровень доступности для экземпляра базы данных SAP hello
Hello СУБД HA SAP установки Обычная основана на двух ВМ СУБД, где используются функциональные возможности высокого уровня доступности СУБД tooreplicate данные из hello active СУБД экземпляр toohello второй виртуальной Машины в пассивный экземпляр СУБД.

Высокий уровень доступности и аварийного восстановления функциональные возможности для СУБД в СУБД общего, а также определенные описаны в hello [руководство по развертыванию СУБД][dbms-guide].

#### <a name="end-to-end-high-availability-for-hello-complete-sap-system"></a>Здравствуйте, конца в конец высокий уровень доступности для всей системы SAP
Ниже приведены два примера полной высокодоступной архитектуры SAP NetWeaver в Azure: по одному для Windows и Linux.

Неуправляемые только диски: hello основные понятия, описанные ниже может потребоваться toobe скомпрометированы немного при развертывании многие системы SAP и количество виртуальных машин, развернутых в hello превышением hello максимальное количество учетных записей хранения на подписку. В таких случаях виртуальных жестких дисков виртуальных машин должны toobe объединены в одну учетную запись хранения. В таких случаях VHD-диски виртуальных машин нужно объединить в одной учетной записи хранения.  Обычно объединяются VHD-диски виртуальных машин уровня приложений SAP из разных систем SAP. Тем самым учитывая ограничения операций ввода-ВЫВОДА hello учетных записей хранилища Azure (<https://azure.microsoft.com/documentation/articles/storage-scalability-targets>)


##### <a name="windowslogowindows-ha-on-windows"></a>![Windows][Logo_Windows] Высокая доступность в Windows
![Высокодоступная архитектура приложений SAP NetWeaver с сервером SQL Server в Azure IaaS][planning-guide-figure-3200]

для системы SAP NetWeaver hello, toominimize воздействие проблем инфраструктуры и установку обновлений на узлы используются следующие конструкции Azure Hello:

* Hello вся система развернута в Azure (это обязательно — уровень СУБД, (A) SCS экземпляра и toorun требуется полное приложение слоя в hello местоположения).
* Hello вся система работает в одной подписки Azure (обязательно).
* Hello вся система работает в одной виртуальной сети Azure (обязательно).
* разделить Hello hello виртуальные машины из одной системы SAP на три группы доступности возможно даже со всех виртуальных машин hello, принадлежащий toohello одной виртуальной сети.
* Все виртуальные машины с экземплярами СУБД из одной системы SAP находятся в одной группе доступности. Мы предполагаем, что используется несколько ВМ с экземплярами СУБД на систему, так как используются встроенные функции высокой доступности СУБД (например, SQL Server AlwaysOn или Oracle Data Guard).
* Все виртуальные машины с экземплярами СУБД используют собственную учетную запись хранения. Файлы данных и журналов СУБД реплицируются из одной учетной записи tooanother хранилища учетной записи хранилища с помощью функций высокого уровня доступности СУБД, которые синхронизируют данные hello. Недоступность одну учетную запись хранилища приведет к недоступности одного узла кластера SQL Server в Windows, но не hello всей службы SQL Server.
* Все виртуальные машины с экземпляром (A)SCS из одной системы SAP находятся в одной группе доступности. Внутри этих виртуальных машин tooprotect hello (A) SCS экземпляр настраивается отказоустойчивого кластера Windows Server (WSFC).
* Все виртуальные машины с экземплярами (A)SCS используют собственную учетную запись хранения. (A) SCS экземпляр файлы и папки глобальных SAP, реплицируются из одной учетной записи tooanother хранилища учетной записи хранилища с помощью SIOS DataKeeper репликации. Недоступность одну учетную запись хранилища приведет к недоступности одной (A) SCS Windows узле кластера, но не весь hello (A) SCS службы.
* ВСЕ виртуальные машины hello, представляющий уровень сервера приложений SAP hello, третья группа доступности.
* ВСЕ виртуальные машины hello, использующие серверы приложений SAP использовать свои собственные учетную запись. Недоступность одну учетную запись хранилища приведет к недоступности одного сервера приложений SAP, где другие AS SAP продолжить toorun.

Hello следующем рисунке показано приветствия же альбомную с помощью управляемых дисков.

![Высокодоступная архитектура приложений SAP NetWeaver с сервером SQL Server в Azure IaaS][planning-guide-figure-3201]

##### <a name="linuxlogolinux-ha-on-linux"></a>![Linux][Logo_Linux] Высокая доступность в Linux
Архитектура Hello для HA SAP в Linux в Azure, по сути, представляет hello так же, как Windows, как описано выше. Начиная с января 2016 года для Linux в Azure сейчас нет доступных решений для обеспечения высокой доступности SAP (A)SCS.

Как следствие как января 2016 систему SAP Linux Azure не могут быть достигнуты hello же доступности в качестве системы SAP Windows Azure из-за отсутствия высокого уровня ДОСТУПНОСТИ для экземпляра hello (A) SCS и hello базы данных SAP ASE одного экземпляра.

### <a name="4e165b58-74ca-474f-a7f4-5e695a93204f"></a>Использование автозапуска для экземпляров SAP
SAP предлагаемых функции hello экземпляров SAP toostart сразу же после начала hello hello ОС в ВМ hello. конкретные шаги Hello задокументированные в статье базы знаний SAP [1909114]. Однако SAP не рекомендует toouse hello параметру больше так как отсутствует контроль в порядке hello перезапуска экземпляра, при условии, что есть влияют несколько виртуальных Машин или запуска нескольких экземпляров каждой виртуальной Машины. При условии, что типичный сценарий Azure из одного экземпляра сервера приложений SAP в случае одной виртуальной Машины со временем получения перезапуска виртуальной Машины и hello, hello автозапуска является не очень важным, их можно включить путем добавления этого параметра:

    Autostart = 1

В hello запуск профиля hello экземпляра SAP ABAP или Java.

> [!NOTE]
> Hello Autostart, параметр может иметь некоторые также недостатков. Более подробно триггеры параметр hello hello запуска экземпляра SAP ABAP или Java hello связаны, что запущена служба Windows, Linux hello экземпляра. Конечно это hello так при загрузке hello операционной системы. Кроме того, перезапуск служб SAP также обычно происходит при управлении жизненным циклом программного обеспечения SAP (например, SUM или другие обновления). Эти функциональные возможности больше не ожидаются toobe экземпляр автоматически перезагружается вообще. Таким образом hello Autostart, параметр должен быть отключен перед запуском таких задач. Autostart, параметр Hello также следует не использоваться для экземпляров SAP, в кластер, подобно ASCS/SCS/CI.
>
>

Дополнительные сведения об автозапуске экземпляров SAP см. здесь:

* [Start/Stop SAP along with your Unix Server Start/Stop (Запуск и остановка SAP одновременно с запуском и остановкой Unix-сервера).](http://scn.sap.com/community/unix/blog/2012/08/07/startstop-sap-along-with-your-unix-server-startstop)
* [Starting and Stopping SAP NetWeaver Management Agents (Запуск и остановка агентов управления SAP NetWeaver).](https://help.sap.com/saphelp_nwpi711/helpdata/en/49/9a15525b20423ee10000000a421938/content.htm)
* [Как tooenable автоматического запуска из базы данных HANA](http://www.freehanatutorials.com/2012/10/how-to-enable-auto-start-of-hana.html)

### <a name="larger-3-tier-sap-systems"></a>Более крупные трехуровневые системы SAP
Аспекты высокой доступности трехуровневых конфигураций SAP рассмотрены в предыдущих разделах. Что касается системах, где требования к серверу hello СУБД слишком велики toohave, расположенные в Azure, но может развернуть hello уровня приложения SAP в Azure?

#### <a name="location-of-3-tier-sap-configurations"></a>Расположение трехуровневых конфигураций SAP
Это не уровней приложения hello поддерживаемых toosplit сам или приложения hello и СУБД между локальной средой и Azure. Система SAP полностью развертывается либо локально, либо в среде Azure. Это также не поддерживается toohave некоторые из серверов приложений hello запуска в Azure в локальной среде и некоторые другие. Это hello, начальная точка hello-обсуждений. Также не поддерживают toohave hello СУБД компоненты системы SAP и hello уровень сервера приложений SAP, развернутых в двух разных регионах Azure. Например, СУБД в западной части США, а уровень приложений SAP в центральной части США. Не поддерживает такие конфигурации обусловлено чувствительность задержки hello hello архитектура SAP NetWeaver.

Тем не менее продолжался hello данные за прошлый год партнерами разработала совместного расположения tooAzure областей. Эти расположения сопутствующего часто находятся в данных физического Azure toohello очень близости центрах обработки внутри области Azure. короткое расстояние Hello и подключение средств в совместное размещение hello через ExpressRoute в Azure может привести к задержкой, меньше 2 мс. В таких случаях возможна toolocate hello уровня СУБД (включая хранилище SAN и NAS) в выравнивании и hello уровня приложения SAP в Azure. По состоянию на декабрь 2015 г. таких развертываний не было, но многие клиенты, использующие развертывания приложений, отличных от SAP, уже используются такой подход.

### <a name="offline-backup-of-sap-systems"></a>Автономное резервное копирование систем SAP
Зависимость от hello выбранной (2-уровневой или 3-уровневой) существует конфигурации SAP может быть tooback необходимость копирования. содержимое Hello hello самой ВМ, а также toohave резервная копия базы данных hello. резервные копии, связанные с СУБД Hello, ожидаемый toobe выполняться средствами базы данных. Подробное описание hello различных баз данных, можно найти в [руководство по СУБД][dbms-guide]. На Здравствуйте другой стороны, hello данных SAP можно архивировать автономно (включая также содержимое базы данных hello) как описано в этом разделе или оперативно, как описано в следующем разделе hello.

автономное резервное копирование Hello потребуется по сути выключение виртуальной Машины через портал Azure hello hello и копия базового диска ВМ hello, а также все присоединенные диски toohello виртуальной Машины. Это сохранит точка изображения времени hello ВМ и соответствующий диск. Рекомендуется toocopy hello «резервное копирование», в другую учетную запись хранилища Azure. Поэтому hello процедуры, описанные в главах [копирование дисков между учетными записями хранения Azure] [ planning-guide-5.4.2] применит этого документа.
Помимо отключение hello, с помощью hello Azure один портал можно также сделать через Powershell или интерфейс командной строки как описанные здесь: <https://azure.microsoft.com/documentation/articles/virtual-machines-deploy-rmtemplates-powershell/>

Включает восстановление этого состояния удаления hello базовой ВМ также как hello исходных дисков hello базовый виртуальной Машины и подключенные диски, резервное копирование hello сохраненного дисков toohello исходной учетной записи хранилища или группа ресурсов для управляемого дисков и затем повторное развертывание системы hello.
В этой статье приведен пример, в том, как tooscript этот процесс в Powershell: <http://www.westerndevs.com/azure-snapshots/>

Убедитесь, что tooinstall новая лицензия SAP с момента восстановления резервной копии виртуальной Машины, как описано выше создает новый ключ оборудования.

### <a name="online-backup-of-an-sap-system"></a>Оперативное резервное копирование системы SAP
Резервное копирование СУБД выполняется с СУБД специальные методы, как описано в hello hello [руководство по СУБД][dbms-guide].

Другие виртуальные машины в системе SAP hello резервное копирование с помощью функции резервного копирования виртуальной машины Azure. Резервное копирование виртуальной машины в Azure появилась в начале 2015 г. и в то же время является стандартным tooback завершения ВМ в Azure. Служба архивации Azure хранятся резервные копии hello в Azure и позволяет восстановление виртуальной Машины, еще раз.

> [!NOTE]
> Начиная с декабря 2015 г. с помощью резервной копии виртуальной Машины не сохранять ИД виртуальной Машины уникальный hello, который используется для SAP лицензирования. Это означает, что восстановление из резервной копии виртуальной Машины установки SAP лицензионный ключ как hello восстановленная виртуальная машина считается toobe новой виртуальной Машины и не является заменой бывшая один, который был сохранен.
>
> ![Windows][Logo_Windows] Windows
>
> Теоретически, виртуальные машины, которые выполнения может быть резервное копирование баз данных также согласованного Если hello СУБД поддерживает hello Windows VSS (служба теневого копирования томов <https://msdn.microsoft.com/library/windows/desktop/bb968832 (v=vs.85).aspx >) как, например, SQL Server выполняет.
> Но следует помнить, что восстановление состояния базы данных на определенный момент времени невозможно, если резервная копия была создана с помощью функции резервного копирования ВМ Azure. Таким образом рекомендуется tooperform резервные копии баз данных с функциональность СУБД, не полагаясь на резервное копирование виртуальной Машины Azure.
>
> tooget знакомы с резервное копирование виртуальных машин Azure, начните здесь: <https://docs.microsoft.com/azure/backup/backup-azure-vms>.
>
> Другие возможные значения — toouse сочетания Microsoft Data Protection Manager, установленные в виртуальной Машине Azure и Azure Backup для резервного копирования и восстановления баз данных. Дополнительные сведения см. здесь: <https://docs.microsoft.com/azure/backup/backup-azure-dpm-introduction>.  
>
> ![Linux][Logo_Linux] Linux
>
> Нет эквивалент tooWindows VSS в Linux, не существует. Резервное копирование СУБД SAP должно выполняться средствами СУБД. Hello СУБД SAP резервное копирование должно выполняться с помощью функциональность СУБД. Hello файловой системы, которая включает данные, связанные с SAP hello могут сохраняться, например, используя tar, как описано здесь: <http://help.sap.com/saphelp_nw70ehp2/helpdata/en/d3/c0da3ccbb04d35b186041ba6ac301f/content.htm>
>
>

### <a name="azure-as-dr-site-for-production-sap-landscapes"></a>Azure как сайт аварийного восстановления для производственных ландшафтов SAP
С момента Mid 2014 расширений компонентов toovarious вокруг Hyper-V, System Center и Azure включите hello использование Azure в качестве сайта аварийного восстановления для виртуальных машин, работающих в локальной среде на базе Hyper-v.

Блог, с подробными сведениями о том, как toodeploy это решение работает описанным здесь: <http://blogs.msdn.com/b/saponsqlserver/archive/2014/11/19/protecting-sap-solutions-with-azure-site-recovery.aspx>.

## <a name="summary"></a>Сводка
перечисляются ключевые моменты Hello высокого уровня доступности систем SAP в Azure:

* На данный момент времени, hello единая точка отказа SAP не может быть защищена точно hello таким же, как это можно сделать в случае локального развертывания. Hello объясняется, что кластеры общих дисков не еще построить в Azure без использования hello программном обеспечении сторонних производителей.
* Для уровня СУБД hello необходимо toouse функциональность СУБД, которая не зависит от технологии кластера общего диска. Подробные сведения описаны в hello [руководство по СУБД][dbms-guide].
* влияние hello toominimize проблемы в доменах сбоя в hello Azure инфраструктуры или обслуживание узлов, следует использовать группы доступности Azure:
  * Рекомендуется toohave один набор доступности для уровня приложения SAP hello.
  * Рекомендуется toohave набор отдельных доступности для уровня СУБД SAP hello.
  * НЕ рекомендуется приветствия tooapply набор же доступности для ВМ разных систем SAP.
  * Рекомендуется toouse Premium управляемых дисков.
* В целях резервного копирования для уровня СУБД SAP hello проверьте hello [руководство по СУБД][dbms-guide].
* Резервное копирование экземпляров диалога SAP делает не имеет особого значения, так как это обычно происходит быстрее, экземпляры tooredeploy простого диалогового окна.
* Резервное копирование hello ВМ, содержащей глобальный каталог hello hello системы SAP, используя его все профили hello различных экземпляров hello, смысла и должно выполняться с помощью системы архивации данных Windows и, например tar в Linux. Так как существуют различия между Windows Server 2008 (R2) и Windows Server 2012 (R2), что позволяет проще tooback с помощью hello Недавние Windows Server, рекомендуется toorun Windows Server 2012 (R2) операционной системой Windows виртуальной машине.
