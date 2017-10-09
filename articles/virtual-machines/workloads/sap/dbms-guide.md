---
title: "Развертывание виртуальных машин СУБД для SAP NetWeaver aaaAzure | Документы Microsoft"
description: "SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД"
services: virtual-machines-linux,virtual-machines-windows
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5654dac7-4204-4387-b312-3d8b2898eb3a
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 11/08/2016
ms.author: sedusch
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 501f6fbc2baa379b706e95d2bfba377ac129b382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-dbms-deployment-for-sap-netweaver"></a>SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД
[767598 ]:https://launchpad.support.sap.com/#/notes/767598
[773830]:https://launchpad.support.sap.com/#/notes/773830
[826037;]:https://launchpad.support.sap.com/#/notes/826037
[965908]:https://launchpad.support.sap.com/#/notes/965908
[1031096]:https://launchpad.support.sap.com/#/notes/1031096
[1114181]:https://launchpad.support.sap.com/#/notes/1114181
[1139904;]:https://launchpad.support.sap.com/#/notes/1139904
[1173395.]:https://launchpad.support.sap.com/#/notes/1173395
[1245200]:https://launchpad.support.sap.com/#/notes/1245200
[1409604]:https://launchpad.support.sap.com/#/notes/1409604
[1558958;]:https://launchpad.support.sap.com/#/notes/1558958
[1585981.]:https://launchpad.support.sap.com/#/notes/1585981
[1588316]:https://launchpad.support.sap.com/#/notes/1588316
[1590719]:https://launchpad.support.sap.com/#/notes/1590719
[1597355]:https://launchpad.support.sap.com/#/notes/1597355
[1605680;]:https://launchpad.support.sap.com/#/notes/1605680
[1619720]:https://launchpad.support.sap.com/#/notes/1619720
[1619726]:https://launchpad.support.sap.com/#/notes/1619726
[1619967;]:https://launchpad.support.sap.com/#/notes/1619967
[1750510]:https://launchpad.support.sap.com/#/notes/1750510
[1752266]:https://launchpad.support.sap.com/#/notes/1752266
[1757924;]:https://launchpad.support.sap.com/#/notes/1757924
[1757928]:https://launchpad.support.sap.com/#/notes/1757928
[1758182]:https://launchpad.support.sap.com/#/notes/1758182
[1758496;]:https://launchpad.support.sap.com/#/notes/1758496
[1772688]:https://launchpad.support.sap.com/#/notes/1772688
[1814258;]:https://launchpad.support.sap.com/#/notes/1814258
[1882376.]:https://launchpad.support.sap.com/#/notes/1882376
[1909114]:https://launchpad.support.sap.com/#/notes/1909114
[1922555;]:https://launchpad.support.sap.com/#/notes/1922555
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1941500]:https://launchpad.support.sap.com/#/notes/1941500
[1956005.]:https://launchpad.support.sap.com/#/notes/1956005
[1973241]:https://launchpad.support.sap.com/#/notes/1973241
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2002167]:https://launchpad.support.sap.com/#/notes/2002167
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2039619]:https://launchpad.support.sap.com/#/notes/2039619
[2069760]:https://launchpad.support.sap.com/#/notes/2069760
[2121797]:https://launchpad.support.sap.com/#/notes/2121797
[2134316]:https://launchpad.support.sap.com/#/notes/2134316
[2171857]:https://launchpad.support.sap.com/#/notes/2171857
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
[dbms-guide-managed-disks]:dbms-guide.md#f42c6cb5-d563-484d-9667-b07ae51bce29

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
[virtual-machines-azurerm-versus-azuresm]:../../../resource-manager-deployment-model.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:../../virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:../../linux/cli-deploy-templates.md 
[virtual-machines-deploy-rmtemplates-powershell]:../../virtual-machines-windows-ps-manage.md 
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
[virtual-machines-manage-availability-linux]:../../linux/manage-availability.md
[virtual-machines-manage-availability-windows]:../../windows/manage-availability.md
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

В этом руководстве является частью документации hello по реализации и развертыванию программного обеспечения SAP hello в Microsoft Azure. Перед прочтением этого руководства, чтение hello [реализацию руководство по планированию и][planning-guide]. В этом документе рассматривается развертывание hello различных систем управления реляционной базы данных (RDBMS) и связанные продукты в сочетании с SAP на виртуальных машинах Microsoft Azure (ВМ) с помощью hello инфраструктуры Azure как возможности услуги (IaaS).

Hello документ дополняет hello документацию по установке SAP и примечания по SAP, которые представляют Привет основные ресурсы для установки и развертывания программного обеспечения SAP в заданный платформы.

## <a name="general-considerations"></a>Общие рекомендации
В этой главе рассматриваются вопросы запуска связанных с SAP систем СУБД на виртуальных машинах Azure. Существует несколько ссылок СУБД toospecific данной главы. Вместо hello конкретные реляционные СУБД обрабатываются в этом документе после данной главы.

### <a name="definitions-upfront"></a>Определения
В документе hello мы используем hello следующими условиями:

* IaaS: инфраструктура как услуга.
* PaaS: платформа как услуга.
* SaaS: программное обеспечение как услуга.
* Компонент SAP: отдельное приложение SAP, например ECC, BW, Solution Manager или EP.  Компоненты SAP могут основываться на традиционной технологии ABAP или Java или быть приложениями не на основе NetWeaver, например бизнес-объектами.
* Среда SAP: один или несколько компонентов SAP логически сгруппированы tooperform бизнес-функцию, например разработки, QAS, обучение, DR или производства.
* Ландшафт SAP: Ссылается toohello все ресурсы SAP в клиента ИТ-инфраструктуре. Hello ландшафт SAP включает все рабочие и непроизводственных средах.
* Система SAP: hello сочетание уровень СУБД и уровня приложений, например, система разработки SAP ERP, тестовая система SAP BW, производственная система SAP CRM и т. д. В развертываниях Azure, не поддерживаемые toodivide этих двух уровней между локальной средой и Azure. Таким образом, система SAP должна быть развернута полностью в локальной среде или полностью в Azure. Тем не менее можно развернуть hello различных системах ландшафта SAP в Azure или локально. Например вы развертывание hello SAP CRM разработки и тестирования системы в Azure, но hello SAP CRM рабочей системы в локальной среде.
* Развертывание только в облаке: развертывания, где hello подписка Azure не подключен через сайт сайт или ExpressRoute подключения toohello локальной сетевой инфраструктуре. В документации Azure развертывания такого рода традиционно называются полностью облачными. Виртуальные машины, развернутые с помощью этого метода осуществляется через Интернет hello и общедоступные конечные точки Интернет назначены toohello ВМ в Azure. Hello в локальной Active Directory (AD) и DNS не расширена tooAzure в этих типах развертываний. Поэтому виртуальные машины hello не являются частью hello в локальной Active Directory. Примечание. Развертывания только в облаке в этом документе определяются как полные ландшафты SAP, которые работают исключительно в Azure. Для них службы Active Directory и служба разрешения имен не распространяются из локальной сети в общедоступное облако. Только для облака конфигурации не поддерживаются для производственных систем SAP или где SAP STMS или других локальных ресурсов должны toobe обмена данными между систем SAP, размещенных в Azure и ресурсам, расположенным в локальной конфигурации.
* Между организациями: Описан сценарий, где виртуальные машины, развернутой tooan подписке Azure с сайт сайт, несколькими сайтами или подключение ExpressRoute между центрами обработки данных в локальной среде hello и Azure. В документации Azure развертывания такого рода также называются распределенными развертываниями. Hello подключения hello обусловлено tooextend локальную доменах локальной Active Directory и DNS в локальной в Azure. Hello локальной альбомная — расширенные toohello активов Azure hello подписки. При таком расширении hello виртуальных машин может быть частью локального домена hello. Пользователи домена hello локального домена имеют доступ к серверам hello и могут запускать службы на их виртуальных машин (как службы СУБД). Возможно взаимодействие и разрешение имен между виртуальными машинами, развернутыми в локальной сети и Azure. Ожидается, что это toobe hello наиболее типичный сценарий развертывания ресурсов SAP в Azure. Дополнительные сведения см. в [этой][vpn-gateway-cross-premises-options] и [этой][vpn-gateway-site-to-site-create] статьях.

> [!NOTE]
> Для производственных систем SAP поддерживаются распределенные развертывания систем SAP, в которых системы SAP выполняются на виртуальных машинах Azure, являющихся членами локального домена. Распределенная конфигурация предполагает развертывание в Azure полного ландшафта SAP или его частей. Даже выполнение hello завершения ландшафт SAP в Azure, необходимо иметь этих виртуальных машин, не входит в состав домена в локальной среде и РЕКЛАМЫ. Прежние версии документации hello мы говорили о сценариях гибридной ИТ-корневым hello термин «Гибридный» hello факт, что между сетями, между локальными и Azure. В данном случае «Гибридный» также означает, что hello ВМ в Azure, являются частью hello локальной Active Directory.
> 
> 

В некоторой документации Майкрософт сценарии распределенного подключения описываются иначе. В частности, это касается высокодоступных конфигураций СУБД. В случае hello hello документов, связанных с SAP сценарий hello между организациями просто сводится toohaving сайт сайт или private (ExpressRoute) подключения и toohello факт что hello ландшафт SAP распределяется между локальной средой и Azure.

### <a name="resources"></a>Ресурсы
Hello следующих руководствах доступны для раздела hello развертываний SAP в Azure.

* [SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию][deployment-guide]
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД (этот документ)][dbms-guide]

следующие примечания по SAP Hello приведены связанные toohello тема SAP в Azure.

| Номер примечания | Название |
| --- | --- |
| [1928533] |Приложения SAP в Azure: поддерживаемые продукты и типы виртуальных машин Azure |
| [2015553] |SAP в Microsoft Azure: требования |
| [1999351] |Устранение неполадок, связанных с расширенным мониторингом Azure для SAP |
| [2178632] |Ключевые метрики мониторинга для SAP в Microsoft Azure |
| [1409604] |Виртуализация в Windows: расширенный мониторинг |
| [2191498] |SAP на платформе Linux в Azure: расширенный мониторинг |
| [2039619] |Здравствуйте, приложения SAP в Microsoft Azure с использованием базы данных Oracle: поддерживаемые продукты и версии |
| [2233094] |DB6: приложения SAP в Azure с использованием IBM DB2 для Linux, UNIX и Windows — дополнительные сведения |
| [2243692] |Linux на виртуальной машине Microsoft Azure (IaaS): проблемы с лицензированием SAP |
| [1984787] |SUSE LINUX Enterprise Server 12: примечания к установке |
| [2002167] |Red Hat Enterprise Linux 7.x: установка и обновление |
| [2069760] |Установка и обновление Oracle Linux 7.x SAP |
| [1597355] |Рекомендация по области буфера для Linux |
| [2171857] |Oracle Database 12c: поддержка файловой системы в Linux |
| [1114181] |Oracle Database 11g: поддержка файловой системы в Linux |


Также считывать hello [SCN вики-сайте](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) , содержащий все примечания SAP для Linux.

Должен иметь практические знания о hello архитектура Microsoft Azure и как развертываемых и эксплуатируемых виртуальных машинах Microsoft Azure. Дополнительные сведения см. по адресу <https://azure.microsoft.com/documentation/>.

> [!NOTE]
> Мы **не** обсуждения платформа как услуга (PaaS) возможности hello платформе Microsoft Azure. Этот документ посвящен под управлением системы управления базой данных (СУБД) в виртуальных машинах Microsoft Azure (IaaS), так же, как будет выполняться hello СУБД в локальной среде. Возможности и функции базы данных в этих двух предложениях существенно отличаются, и их не следует путать друг с другом. См. также: <https://azure.microsoft.com/services/sql-database/>.
> 
> 

Поскольку мы обсуждаем IaaS, в общем hello Windows, Linux и СУБД установки и настройки по существу hello такой же, как любой виртуальной машине или исходного состояния системы исходного компьютера устанавливается в локальной среде. Но некоторые решения в плане архитектуры и реализации управления системой все же отличаются при использовании IaaS. Hello цель данного документа — tooexplain hello архитектуры и системы управления различия, вы должны быть готовы при использовании IaaS.

В общем случае hello области различий, которое обсуждается в этом документе приведены.

* Планирование hello правильный диск виртуальной Машины и макет tooensure систем SAP имеется hello правильную структуру файлов данных и можно добиться достаточное количество операций ввода-ВЫВОДА для рабочей нагрузки.
* Сетевые аспекты при использовании IaaS.
* Toouse возможности конкретной базы данных в формат базы данных hello toooptimize заказа.
* Вопросы резервного копирования и восстановления в IaaS.
* Использование разных типов образов для развертывания.
* Высокий уровень доступности в Azure IaaS.

## <a name="65fa79d6-a85f-47ee-890b-22e794f51a64"></a>Структура развертывания реляционной СУБД
Чтобы toofollow в этой главе, что необходимые toounderstand что был предоставлен в [это] [ deployment-guide-3] главе hello [руководство по развертыванию] [ deployment-guide]. Знания о hello различных Серия виртуальных Машин и их различия различия Azure Standard и Premium хранилища должны быть понятны и известные перед изучением данной главы.

До марта 2015 г диски, содержащие операционной системы были ограниченный too127 ГБ. Это ограничение было снято в марте 2015 года (дополнительные сведения см. по ссылке <https://azure.microsoft.com/blog/2015/03/25/azure-vm-os-drive-limit-octupled/>). Оттуда на дисках, содержащей hello операционной системы может быть hello того же размера, как и любые другие диска. Тем не менее мы все-таки структуру развертывания, где hello операционной системы, СУБД и окончательной двоичные файлы SAP отделены от hello файлы базы данных. Таким образом предполагается, что системы SAP, работающие на виртуальных машинах Azure имеют hello базовой виртуальной Машины (или диски) установлен с hello операционной системы, исполняемые файлы системы управления базы данных и исполняемые файлы SAP. Hello СУБД данных и файлы журналов хранятся в хранилище Azure (Standard или Premium хранилища) в отдельные диски и подключен как логические диски toohello исходного Azure ВМ образа операционной системы. 

В зависимости от использования Azure Standard или Premium хранилища (например, с помощью hello серии DS или виртуальные машины серии GS) существует являются другие квоты в Azure, описаны [здесь (Linux)] [ virtual-machines-sizes-linux] и [здесь (Windows)][virtual-machines-sizes-windows]. При планировании дискового макет, требуются toofind hello оптимальный баланс между hello квоты для hello следующих элементов:

* число файлов данных Hello.
* Количество дисков, содержащих файлы hello Hello.
* Hello в секунду для одного диска.
* пропускная способность Hello на одном диске.
* Hello количество дополнительных дисков данных каждого размера виртуальной Машины.
* Hello общей пропускной способности хранилища виртуальной Машины можно указать.

Azure обеспечивает квоту на количество операций ввода-вывода для каждого диска данных. Эти квоты различаются для дисков, размещенных в службе хранилища Azure классов Standard и Premium. Задержки ввода-вывода, также очень различаются между двумя типами хранилища hello с хранилищем Premium доставки факторов лучше задержки ввода-вывода. Каждый из типов ВМ hello имеет ограниченное число дисков с данными, которые могут tooattach. Другое ограничение состоит в том, что только некоторые типы виртуальных машин могут использовать службу хранилища Azure класса Premium. Это означает, что решение hello для определенного типа виртуальной Машины может не только управляться hello ЦП и требования к памяти, но также hello операций ввода-ВЫВОДА, задержки и диск пропускной способности, обычно масштабируются с hello количеством дисков или hello тип дисках хранилища Premium. Особенно в хранилище Premium hello размер диска также может определяться hello число операций ввода-ВЫВОДА и пропускная способность, которую требуется toobe достигается путем каждого диска.

Hello факт hello общую скорость операций ввода-ВЫВОДА, hello количество дисков, подключенных и размер ВМ взаимосвязаны, hello hello может привести к Azure конфигурации отличается от его локальное развертывание toobe системы SAP. ограничения Hello операций ввода-ВЫВОДА на каждый LUN обычно настраиваются в локальном развертывании. Тогда как со службой хранилища Azure эти пределы являются фиксированного или как в хранилище Premium в зависимости от типа диска hello. Поэтому с локальных развертываний можно видеть пользовательские конфигурации серверов баз данных, использующие много разных томов для определенных исполняемых файлов, таких как SAP и hello СУБД, или предусмотрены отдельные томa для временных баз данных или табличных пространств. При такой системы в локальной среде перемещенный tooAzure его может привести tooa трата потенциальных пропускная способность операций ввода-ВЫВОДА тратит на диск для баз данных, которые не выполняют все или не много операций ввода-ВЫВОДА или исполняемые файлы. Таким образом в виртуальных машинах Azure рекомендуется по возможности установить на диске hello ОС, исполняемые файлы hello СУБД и SAP.

Hello размещения hello файлы базы данных и файлов журнала и hello тип хранилища Azure используется, должен быть определен путем IOPS, задержки и пропускной способности. В порядке toohave достаточное количество операций ввода-ВЫВОДА для журнала транзакций hello, может быть принудительного tooleverage несколько дисков для журнала транзакций hello файлу или используйте диск на больший хранилище Premium. В этом случае один бы построения программного обеспечения RAID (например, хранилище пула для Windows или MDADM и LVM (диспетчер логических томов) для Linux) с дисками hello, которые содержат hello журнала транзакций.

- - -
> ![Windows][Logo_Windows] Windows
> 
> Диск D:\ на виртуальной Машине Azure — это несохраняемый диск, который реализуется некоторые локальные диски на узле hello вычислений Azure. Так как он является несохраняемым, это означает, любое содержимое toohello изменения, внесенные на диск D:\ hello потеряны при перезагрузке hello виртуальной Машины. Под любыми изменениями подразумевается сохранение файлов, создание каталогов, установка приложений и т. д.
> 
> ![Linux][Logo_Linux] Linux
> 
> Виртуальные машины Linux Azure автоматически присоединения диска является несохраняемый диск, поддерживаемый локальные диски на узле вычислений Azure hello/mnt/Resource. Так как он является несохраняемым, это означает, что toocontent любые изменения, внесенные в/mnt/Resource теряются при перезагрузке hello виртуальной Машины. Под любыми изменениями подразумевается сохранение файлов, создание каталогов, установка приложений и т. д.
> 
> 

- - -
Зависимость от hello Azure Серия виртуальных Машин, hello локальные диски на hello вычислений узел отображать различные производительность, что можно классифицировать как:

* A0–A7: крайне ограниченная производительность. Используется только для файла подкачки Windows.
* A8–A11: очень хорошая производительность на уровне 10 тыс. операций ввода-вывода в секунду и более 1 ГБ/с пропускной способности.
* Серия D: очень хорошая производительность на уровне 10 тыс. операций ввода-вывода в секунду и более 1 ГБ/с пропускной способности.
* Серия DS: очень хорошая производительность на уровне 10 тыс. операций ввода-вывода в секунду и более 1 ГБ/с пропускной способности.
* Серия G: очень хорошая производительность на уровне 10 тыс. операций ввода-вывода в секунду и более 1 ГБ/с пропускной способности.
* Серия GS: очень хорошая производительность на уровне 10 тыс. операций ввода-вывода в секунду и более 1 ГБ/с пропускной способности.

Выше инструкции применяются toohello типов ВМ, сертифицированные с SAP. Hello Серия виртуальных Машин с отличным операций ввода-ВЫВОДА и пропускной способности подлежат использование, некоторые функции СУБД, такие как базы данных tempdb или пространства временной таблицы.

### <a name="c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f"></a>Кэширование для виртуальных машин и дисков данных
При создании дисков данных через портал hello или при подключении tooVMs отправленного дисков, мы можно выбрать, будут ли кэшироваться трафик ввода-вывода hello между hello ВМ и диски, расположенные в хранилище Azure. В службе хранилища Azure классов Standard и Premium для этого типа кэша используются две разные технологии. В обоих случаях сам кэш hello может быть диском на hello же дисков по hello временный диск (D:\ в Windows) или/mnt/Resource в Linux hello виртуальной Машины.

Для стандартных хранилища Azure: hello возможные типы кэша:

* Без кэширования
* Кэширование чтения
* Кэширование чтения и записи

В порядке tooget постоянную и определенную производительность, следует задать кэширование hello в стандартном хранилище Azure для всех дисков, содержащих **файлы данных, связанных с СУБД файлы журналов и табличные пространства too'NONE "**. Hello кэширование hello ВМ можно оставить значения по умолчанию hello.

Для хранилища Azure Premium существуют следующие параметры кэширования hello:

* Без кэширования
* Кэширование чтения

Рекомендуется для хранилища Azure Premium tooleverage **кэширование для файлов данных чтения** базы данных SAP hello и выбрал **кэширование для дисков hello файлов журнала не**.

### <a name="c8e566f9-21b7-4457-9f7f-126036971a91"></a>Программный RAID-массив
Как уже говорилось выше необходимо toobalance hello число операций ввода-ВЫВОДА требуется для файлов базы данных hello нескольких hello дисков можно настроить и hello Максимума ВМ Azure обеспечивает для каждого диска или тип диска хранилища Premium. Самый простой способ toodeal с приветствия нагрузки операций ввода-ВЫВОДА на дисках является toobuild программного RAID на разных дисках hello. Число файлов данных СУБД SAP hello поместите на приветствия номера LUN вырезано из hello программного RAID. Зависит от требований hello tooconsider hello об использовании хранилища Premium также может потребоваться после двух hello три разных дисках хранилища Premium обеспечивают выше квоты операций ввода-ВЫВОДА от дисков, на основе стандартных хранилища. Помимо hello значительно лучше задержки ввода-вывода, предоставляемые хранилища Azure Premium. 

Тоже относится toohello журнала транзакций из различных систем реляционных СУБД hello. С многие из них только добавлять дополнительные файлы журнала отслеживания не помогает, так как hello СУБД запись в один из файлов hello только во время. Если требуются высокоскоростных операций ввода-ВЫВОДА, чем одну стандартную хранилища в соответствии можно доставлять диска, вы можете создать чередующийся через нескольких стандартных дисков или можно использовать тип диск большего размера хранилища Premium, помимо высокоскоростных операций ввода-ВЫВОДА также обеспечивает более низкой задержке факторы для записи hello Операций ввода-вывода в журнал транзакций hello.

При развертывании Azure программный RAID-массив предпочтительно использовать в следующих ситуациях:

* Журнал транзакций или журнал повтора операций требует больше операций ввода-вывода, чем обеспечивает Azure для одного диска. Как упоминалось выше, это можно решить, создав LUN для нескольких дисков с помощью программного RAID-массива.
* Неравномерное ввода-вывода распределения рабочей нагрузки по hello разным файлам данных базы данных SAP hello. В таких случаях один могут возникать попадание квоты hello довольно часто один файл данных. В то время как другие файлы данных еще не получают закрыть toohello квоты операций ввода-ВЫВОДА одного диска. В таких случаях hello простым решением является toobuild один LUN через несколько дисков с помощью программного обеспечения RAID. 
* Вы не знаете, какие hello точное ввода-вывода рабочей нагрузки на файл данных — и только примерно знать, что hello общую рабочую нагрузку операций ввода-ВЫВОДА для hello СУБД в дополнительной —. Простой toodo — toobuild один LUN с hello Справка по RAID. Сумма Hello квот нескольких дисков за это устройство LUN затем необходимо выполнить hello известные IOPS скорость.

- - -
> ![Windows][Logo_Windows] Windows
> 
> Мы рекомендуем использовать дисковые пространства Windows при работе с Windows Server 2012 или более поздней версии, так как это более эффективно, чем функция Windows Striping из более ранних версий Windows. Может потребоваться toocreate приветствия Windows пулы носителей и дисковые пространства с помощью команд PowerShell при использовании в качестве операционной системы Windows Server 2012. Здесь можно найти команды PowerShell Hello <https://technet.microsoft.com/library/jj851254.aspx>
> 
> ![Linux][Logo_Linux] Linux
> 
> Только MDADM и LVM (диспетчер логических томов), поддерживаемых toobuild программного RAID на платформе Linux. Дополнительные сведения см. в статье hello в следующих статьях:
> 
> * [Настройка программного RAID-массива в Linux][virtual-machines-linux-configure-raid] (для MDADM)
> * [Настройка диспетчера логических томов на виртуальной машине Linux в Azure][virtual-machines-linux-configure-lvm]
> 
> 

- - -
Ниже приведены рекомендации по использованию ВМ ряда, обычно являются может toowork со службой хранилища Azure Premium.

* Требования для задержки ввода-вывода, закройте доставки устройства SAN и NAS toowhat.
* Потребность в улучшенной задержке при операциях ввода-вывода, чем обеспечивает служба хранилища Azure класса Standard.
* Больше операций ввода-вывода на виртуальную машину, чем можно достичь с помощью нескольких дисков хранилища класса Standard в отношении определенного типа виртуальной машины.

С момента hello базовое хранилище Azure реплицирует каждого узлов хранения tooat как минимум три диска простой RAID 0, можно использовать чередование. Нет необходимости tooimplement RAID5 или RAID1 не существует.

### <a name="10b041ef-c177-498a-93ed-44b3441ab152"></a>Служба хранилища Microsoft Azure
Хранилище Microsoft Azure хранилищ hello базовой ВМ (с ОС) и дисков или большие двоичные объекты tooat как минимум три отдельных узла хранилища. При создании учетной записи хранения или управляемого диска можно выбрать уровень защиты, как показано ниже:

![Георепликация включена для учетной записи хранения Azure][dbms-guide-figure-100]

Azure Локальная репликация службы хранилища (локальное избыточное) предоставляет уровни защиты от потери данных из-за сбоя tooinfrastructure некоторые пользователи могут позволить себе toodeploy. Как показано выше, что имеются четыре различные параметры с пятый выполняется вариантом hello первых трех. Различия состоят в следующем:

* **Локально избыточное хранилище (LRS) класса Premium.** Хранилище Azure класса Premium обеспечивает поддержку высокопроизводительных дисков с низкой задержкой для виртуальных машин с интенсивной рабочей нагрузкой ввода-вывода. Существует три копии данных hello в hello же центре обработки данных Azure региона Azure. Hello копии находятся в различных доменах отказа и обновление (см. в разделе Основные понятия [это] [ planning-guide-3.2] главе hello [руководство по планированию][planning-guide]). В случае реплики hello данных, поступающих из службы из-за сбоя узла хранения tooa или сбой диска новая реплика будет создан автоматически.
* **Локально избыточное хранилище (LRS)**: В этом случае существует три копии данных hello в hello же центре обработки данных Azure региона Azure. Hello копии находятся в различных доменах отказа и обновление (см. в разделе Основные понятия [это] [ planning-guide-3.2] главе hello [руководство по планированию][planning-guide]). В случае реплики hello данных, поступающих из службы из-за сбоя узла хранения tooa или сбой диска новая реплика будет создан автоматически. 
* **Географически избыточное хранилище (GRS)**: В этом случае является асинхронной репликации, который веб-каналы еще три реплики данных hello в другой области Azure, которая в большинстве случаев hello в одном географическом регионе (например, Северной Европе и Западная Здравствуйте, Европа). В результате получатся три дополнительные реплики, так что всего суммарно реплик будет шесть. В варианте такого подхода является дополнительным которых данных hello в регионе реплицированных Azure географически hello могут использоваться для чтения целей (доступ на чтение географически избыточной).
* **Зоны избыточности хранилища (ZRS)**: В этом случае hello трех реплик hello данные остаются в hello же регионе Azure. Как описано в статье [это] [ planning-guide-3.1] главе hello [руководство по планированию] [ planning-guide] регионом Azure может быть несколько центров обработки данных в непосредственной близости. В случае, когда hello LRS hello реплик будут распространяться через hello разных центрах обработки данных, сделать один регион Azure.

Дополнительные сведения см. [здесь][storage-redundancy].

> [!NOTE]
> Для развертываний СУБД не рекомендуется использование hello Geo Redundant Storage
> 
> Георепликация хранилища Azure является асинхронной. Репликация отдельных дисков подключить tooa одной виртуальной Машины не синхронизируются на этапе блокировки. Следовательно не подходящий tooreplicate файлы СУБД, которые распространяются на разных дисках или развертываемом для программного RAID на основе на нескольких дисках. По СУБД необходима, hello постоянного дискового хранилища Точная синхронизация через различные LUN и базовые диски и физические диски. По СУБД использует различные механизмы toosequence, ввод-ВЫВОД записи действий и СУБД сообщает о повреждении дискового хранилища hello мишенью hello репликации, если они отличаются даже лишь несколько миллисекунд. Поэтому если действительно требуется конфигурация базы данных с распределением по нескольким дискам географически реплицируются, такая репликация должна toobe выполнять с помощью средства базы данных и функциональные возможности. Не следует полагаться на Георепликацию хранилища Azure tooperform этого задания. 
> 
> Hello проблема заключается в простой tooexplain на примере системы. Предположим, что у вас есть отправки в Azure, который имеет восемь дисков, содержащих файлы данных СУБД hello, а также один диск, содержащий файл журнала транзакций hello системы SAP. Каждый из этих дисков девять иметь данные, записанные toothem toohello СУБД, в соответствии с последовательным способом ли данные hello записывается toohello данных файлов журнала транзакций.
> 
> В порядке tooproperly репликации hello данных и поддержания целостного образа базы данных, hello содержимое всех девяти дисков будет иметь toobe географически реплицируются в операциях ввода-вывода hello точный порядок hello были выполняться hello девяти разных дисках. Однако георепликация службы хранилища Azure не позволяет toodeclare зависимости между дисками. Это означает, что географическая репликация хранилища Microsoft Azure не знает о hello тем, что hello содержимое этих девяти разных дисках другие связанные tooeach и что изменения данных hello согласованы только при репликации операций ввода-вывода hello порядок hello произошло на всех дисках девять hello.
> 
> Помимо вероятность скрываться, что образы георепликацией hello в сценарии hello не предоставляют целостного образа базы данных, кроме того, к снижению производительности, который отображается с географически избыточное хранилище, которое может привести к серьезным повлиять на производительность. Иными словами, этот тип избыточности хранилища не следует использовать для рабочих нагрузок типа СУБД.
> 
> 

#### <a name="mapping-vhds-into-azure-virtual-machine-service-storage-accounts"></a>Сопоставление виртуальных жестких дисков с учетными записями хранения службы виртуальных машин Azure
В этой главе применяется только tooAzure учетные записи хранения. Если планируется toouse управляемых дисков hello ограничения, упомянутые в этой главе не применяются. Дополнительные сведения об Управляемых дисках см. в [этом разделе][dbms-guide-managed-disks] данного руководства.

Учетная запись хранения Azure является не только административной конструкцией, но и предметом ограничений. В то время как ограничения hello зависят от того, мы говорим о Стандартная учетная запись хранения Azure или учетная запись хранения Azure Premium. Hello точное возможности и ограничения перечислены [здесь][storage-scalability-targets]

Поэтому для стандартного хранилища Azure очень важным toonote имеется ограничение на hello операций ввода-ВЫВОДА на учетную запись хранения (строки содержащий «Общая частота запросов» в [hello статьи][storage-scalability-targets]). Кроме того, существует изначальное ограничение в 100 учетных записей хранения на одну подписку Azure (начиная с июля 2015 г.). Таким образом рекомендуется toobalance операций ввода-ВЫВОДА для виртуальных машин между несколькими учетными записями хранения при использовании стандартного хранилища Azure. При этом отдельная виртуальная машина в идеале использует по возможности одну учетную запись хранения. Поэтому, если говорить о развертываниях СУБД, где каждый виртуальный жесткий диск, размещенный в службе хранилища Azure класса Standard, может достичь предела квоты, следует развертывать не более 30–40 виртуальных жестких дисков на одну учетную запись службы хранилища Azure класса Standard. В hello другой стороны, если использовать хранилище Azure класса Premium и требуется toostore томов большой базы данных, может оказаться точной с точки зрения операций ввода-ВЫВОДА. Однако учетная запись службы хранилища Azure класса Premium накладывает существенно большие ограничения на объем данных, чем аналогичная учетная запись хранилища класса Standard. В результате ограниченное число VHD в учетной записи хранилища Azure Premium можно развернуть только до обращения ограничение тома данных hello. В конце hello считаете учетную запись хранилища Azure «Виртуальная сеть SAN», имеет ограниченные возможности в операции ввода-ВЫВОДА и емкость. В результате задачу hello остается как в локальных развертываний, макет hello toodefine hello VHD разных систем SAP hello через hello различных «воображаемых устройствах SAN» или учетных записей хранилища Azure.

Для стандартной службы хранилища Azure toopresent хранилища из tooa другое хранилище учетных записей не рекомендуется по возможности одной виртуальной Машины.

При использовании hello доменных служб Active Directory или серии GS виртуальных машин Azure, это возможно toomount виртуальные жесткие диски из стандартных учетных записей хранилища Azure и учетные записи хранения Premium. Варианты использования, как записи резервных копий в стандартном хранилище резервные виртуальные жесткие диски и для данных СУБД и файлы журналов в хранилище класса Premium предоставляются toomind, где может использоваться такие разнородное хранилище. 

На основе клиентские развертывания и тестирования около 30 too40, VHD, содержащих файлы данных базы данных и файлы журналов могут быть подготовлены на одной стандартной учетной записи хранения Azure с приемлемой производительностью. Как упоминалось ранее, учетной записи хранилища Azure Premium hello ограничение заключается в емкости данных hello toobe скорее всего, которые могут содержаться и не операций ввода-ВЫВОДА.

Как с SAN устройств в локальной среде для управления доступом необходимо выполнять определенный мониторинг в порядке tooeventually обнаруживать узкие места в учетной записи хранения Azure. Hello расширения мониторинга Azure для SAP и hello портал Azure — средства, которые можно использовать toodetect занятости учетных записей хранилища Azure, которая могут привести неоптимальной производительности операций ввода-ВЫВОДА.  Если такая ситуация обнаруживается, рекомендуется toomove занят виртуальные машины tooanother учетной записи хранилища Azure. См. toohello [руководство по развертыванию] [ deployment-guide] сведения о как tooactivate hello SAP размещения возможностей наблюдения.

Другую статью со сводкой практических рекомендаций по хранилищу Azure класса Standard и связанным учетным записям см. здесь: <https://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx>.

#### <a name="f42c6cb5-d563-484d-9667-b07ae51bce29"></a>Управляемые диски
Управляемые диски — это ресурс нового типа в Azure Resource Manager, который можно использовать вместо виртуальных жестких дисков, хранимых в учетных записях хранения Azure. Управляемый диски автоматически соответствовать hello, группа доступности hello виртуальной машины, которые могут им присоединенного tooand таким образом увеличение hello доступности виртуальных машин и служб hello, выполняющихся на виртуальной машине hello. hello лучше, ознакомьтесь с toolearn [обзорную статью](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview).

Сейчас SAP поддерживает только управляемые диски уровня "Премиум". Дополнительные сведения см. в примечании к SAP [1928533].

#### <a name="moving-deployed-dbms-vms-from-azure-standard-storage-tooazure-premium-storage"></a>Перемещение развертывания ВМ СУБД из стандартного хранилища Azure tooAzure хранилища Premium
Получаем довольно некоторые сценарии, где клиент место toomove развернутой виртуальной Машины из стандартных хранилища Azure в хранилище Azure класса Premium. Если диски хранятся в учетных записях хранения Azure, это невозможно без физического перемещения данных hello. Существует несколько способов tooachieve hello цели:

* Можно просто скопировать все виртуальные жесткие диски — базовый диск и диски с данными — в новую учетную запись службы хранилища Azure класса Premium. Часто вы выбрали hello количество виртуальных жестких дисков в стандартном хранилище Azure не по причине hello факт, что требуется тома данных hello. Однако требуется столько виртуальные жесткие диски из-за hello операций ввода-ВЫВОДА. Теперь, чтобы переместить tooAzure хранилища Premium можно пройти средством меньшее количество виртуальных жестких дисков tooachieve hello аналогичную пропускную способность операций ввода-ВЫВОДА. Учитывая hello факт, что в стандартном хранилище Azure, вы платите за hello использовать данные и не hello номинальный места на диске, hello количество виртуальных жестких дисков не имеет значения с точки зрения затрат. Однако с помощью хранилища Azure Premium оплачиваться будет hello номинальный места на диске. Таким образом большинство клиентов hello попробуйте tookeep hello количество виртуальных жестких дисков Azure в хранилище Premium в hello номеров необходимые tooachieve hello IOPS пропускной способности необходимости. Таким образом большинство пользователей принято способом hello простого 1:1 копирования.
* Если это еще не сделано, следует подключить один виртуальный жесткий диск, на котором можно разместить резервную копию базы данных SAP. После создания резервной копии hello отключите все виртуальные жесткие диски, включая резервное копирование содержащего hello hello виртуального жесткого диска и hello копии базового VHD и hello VHD с резервной копией hello в учетную запись хранилища Azure Premium. Затем будет развернуть hello виртуальных Машин на основании hello базовый виртуальный жесткий ДИСК и подключения hello VHD с резервной копией hello. Теперь можно создавать дополнительные очистите дисках хранилища Premium hello виртуальной Машины, базы данных hello используется toorestore в. Предполагается, что hello СУБД позволяет toochange пути toohello файлов данных и журналов в рамках процесса восстановления hello.
* Другая возможность — это разновидность hello бывшая процесса, где просто скопируйте резервную копию hello виртуального жесткого диска в хранилище Azure класса Premium и присоединить ее к виртуальной Машины, которая только что развертывании и установке.
* Четвертый вероятность Hello выбирается при работе в, необходимо toochange hello количество файлов данных базы данных. В таком случае следует выполнить копирование однородной системы SAP с помощью экспорта и импорта. PUT те экспортировать файлы в VHD, скопированного в учетную запись хранилища Azure Premium и присоединить ее tooa использовать toorun hello импорта процессов виртуальной Машины. Клиенты использовать эту возможность, главным образом в том случае, если они должны toodecrease hello количество файлов данных.

При использовании управляемых диски, можно перенести tooPremium хранилища по:

1. Освободить виртуальную машину hello
2. При необходимости измените размер виртуальной машины tooa hello, которая поддерживает хранилище Premium (например, DS или GS)
3. Изменение типа учетной записи tooPremium (SSD) для hello управляемого диска
4. Запустить виртуальную машину.

### <a name="deployment-of-vms-for-sap-in-azure"></a>Развертывание виртуальных машин для SAP в Azure
Microsoft Azure предлагает несколько способов toodeploy ВМ и связанные диски. Тем самым — toounderstand важные различия hello, так как действия по подготовке виртуальных машин hello может отличаться в зависимости от способа развертывания hello. Как правило мы рассмотрим hello сценарии, описанные в следующих главах hello.

#### <a name="deploying-a-vm-from-hello-azure-marketplace"></a>Развертывание ВМ из Azure Marketplace hello
Например tootake Microsoft или сторонних производителей предоставляется образом из Azure Marketplace toodeploy hello ВМ. После развертывания ВМ в Azure вы выполните hello же рекомендации и средства tooinstall hello программного обеспечения SAP в ВМ, как это делается в локальной среде. Для установки программного обеспечения SAP hello внутри hello виртуальной Машине Azure, Майкрософт и SAP рекомендуется передачи и сохранить установочный носитель SAP hello в дисков или toocreate ВМ Azure работает как «файловый сервер», который содержит все hello необходимые установочные носители SAP.

#### <a name="deploying-a-vm-with-a-customer-specific-generalized-image"></a>Развертывание виртуальной машины с помощью конкретного универсального пользовательского образа
Из-за toospecific исправление требования, связанные с используемой версией ОС или СУБД образы предоставленный hello в hello Azure Marketplace могут не соответствовать вашим потребностям. Таким образом может потребоваться toocreate ВМ с помощью собственного «private» образа ОС или СУБД виртуальной Машины, который можно разворачивать многократно. tooprepare такой «свой» образ для дублирования приветствия обобщенный ОС на hello локальной виртуальной Машины. См. toohello [руководство по развертыванию] [ deployment-guide] подробные сведения о том, как toogeneralize виртуальной Машины.

Если вы уже установили содержимое SAP в локальной виртуальной Машины (особенно для двухуровневых систем), hello параметры системы SAP можно адаптировать после развертывания hello hello виртуальной Машине Azure через экземпляр hello переименовать процедуру, поддерживаемых hello подготовки программного обеспечения SAP Диспетчер (Примечание SAP [1619720]). В противном случае можно установить по SAP hello позже, после развертывания hello hello виртуальной Машине Azure.

Начиная с hello содержимое базы данных, используемого приложением SAP hello можно либо создать hello содержимое заново с помощью установки SAP, или можно импортировать содержимое в Azure, используя VHD с резервной копией СУБД или возможности СУБД toodirectly hello резервное копирование в хранилище Microsoft Azure. В этом случае может также подготовить VHD с hello СУБД данных и журнала файлов в локальной и затем импортировать их как диски в Azure. Но hello передача данных СУБД, которые загружаются из локальной tooAzure, будет работать на дисках VHD, которые должны toobe подготовлен в локальной среде.

#### <a name="moving-a-vm-from-on-premises-tooazure-with-a-non-generalized-disk"></a>Перемещение ВМ из локальной tooAzure с помощью специализированного диска
При планировании toomove определенную систему SAP из локальной tooAzure (точности прогнозов и shift). Это можно сделать путем отправки hello диск, который содержит hello ОС, двоичные файлы SAP hello и возможные двоичные файлы СУБД, а также hello диски с данными hello и файлы журналов для tooAzure СУБД hello. В обратном tooscenario #2 выше обеспечили hello имя узла, ИД безопасности SAP и учетные записи пользователей SAP в ВМ Azure hello как они были настроены в локальной среде hello. Таким образом обобщение hello образ не является обязательным. Этот случай применяется главным образом для сценариев между организациями, когда часть hello ландшафт SAP запускается локально и частей в Azure.

## <a name="871dfc27-e509-4222-9370-ab1de77021c3"></a>Высокая доступность и аварийное восстановление с использованием виртуальных машин Azure
Azure предлагает следующие функции высокой доступности (HA) и аварийного восстановления (DR), применяемые toodifferent компонентов, которые могут использоваться в развертываниях SAP и СУБД hello

### <a name="vms-deployed-on-azure-nodes"></a>Виртуальные машины, развернутые на узлах Azure
Hello платформы Azure не предлагает функции, такие как динамической миграции для развернутых виртуальных машин. Это означает, если обслуживание необходимые в кластере серверов, на котором развернута виртуальная машина, hello виртуальной Машины должен tooget останавливается и перезапускается. Техническое обслуживание в Azure выполняется с помощью так называемых доменов обновления в кластерах серверов. Одновременно поддерживается обслуживание только одного домена обновления. При таком перезапуске имеется прерывания обслуживания во время завершения работы ВМ приветствия, обслуживание и перезапуск виртуальной Машины. Большинство поставщиков СУБД Однако предоставляют функциональные возможности высокого уровня доступности и аварийного восстановления, который быстро перезапускает службы СУБД hello на другой узел в случае недоступности основного узла hello. Hello платформа Azure предлагает функциональность toodistribute виртуальных машин, хранилища и другими службами Azure через домены обновления tooensure планируемого обслуживание или сбои инфраструктуры оказывали влияние только небольшое подмножество виртуальных машин и служб.  При тщательном планировании это возможных tooachieve доступности уровней сопоставимых tooon локальной инфраструктуры.

Группы доступности Microsoft Azure — это логические группы виртуальных машин или служб, которые обеспечивают виртуальных машин и других служб, распределенных toodifferent сбоя и домены обновления в кластере таким образом, что будет существовать только завершение работы одного узла на любой момент времени ( длячтения[(Linux)] [ virtual-machines-manage-availability-linux] или [(Windows)] [ virtual-machines-manage-availability-windows] Дополнительные сведения).

Он должен toobe настроен по назначению при развертывании виртуальных машин, как показано ниже:

![Определение группы доступности для конфигураций высокой доступности СУБД ][dbms-guide-figure-200]

Если мы хотим toocreate высокодоступные конфигурации развертываний СУБД (независимо от hello отдельных СУБД используемой ИНДИВИДУАЛЬНОЙ функциональности), то ВМ СУБД hello потребуется:

* Добавить toohello hello виртуальных машин одной виртуальной сети Azure (<https://azure.microsoft.com/documentation/services/virtual-network/>)
* виртуальные машины высокой ДОСТУПНОСТИ конфигурации hello Hello также должно быть в hello одной подсети. Разрешение имен между hello разным подсетям не поддерживается в развертываниях только для облака, работает разрешения только IP. Для распределенного развертывания с использованием подключения "сеть — сеть" или ExpressRoute уже будет установлена сеть по крайней мере с одной подсетью. Разрешение имен выполняется toohello в соответствии с локальными политиками AD и сетевой инфраструктуры. 

[comment]: <> (Пользователь MSSedusch: проверить, актуально ли до сих пор в ARM)

#### <a name="ip-addresses"></a>IP-адреса
Настоятельно рекомендуется hello toosetup ВМ для конфигураций высокой ДОСТУПНОСТИ устойчивым способом. Полагаться на партнерами IP адресов tooaddress hello высокого уровня ДОСТУПНОСТИ в конфигурации высокого уровня ДОСТУПНОСТИ hello не является надежной в Azure, если используются статические IP-адреса. В Azure существует два понятия "завершение работы".

* Завершение работы через портал Azure или командлета Azure PowerShell Stop AzureRmVM: В этом случае выполняется завершение работы hello виртуальной машины и освобождена. Учетная запись Azure больше не взимается с этой виртуальной Машины, hello, существенно оплачивают только используемое дисковое пространство hello. Однако если hello частный IP-адрес сетевого интерфейса hello не статические, hello IP-адрес освобождается и не гарантируется, что этот сетевой интерфейс hello получает hello старый IP-адрес еще раз после перезапуска hello виртуальной Машины. Выполняет hello завершение работы с помощью hello портал Azure или путем вызова Stop AzureRmVM автоматически вызывает отмену выделения. Если вы не хотите машина hello toodeallocate использовать Stop AzureRmVM - StayProvisioned 
* При выключении hello виртуальной Машины с ОС уровня hello ВМ возвращает завершить работу и не освобождена. Однако в этом случае учетная запись Azure по-прежнему взимается с hello ВМ, несмотря на то, что это shutdown факт hello. В этом случае назначение hello hello IP адрес tooa остановлена виртуальной Машины остается без изменений. Завершение работы hello ВМ не приводит к автоматической отмене выделения.

Даже для сценариев между организациями по умолчанию завершения работы и Отмена выделения означает отмену назначения IP-адресов hello hello виртуальной Машины, даже если в локальной политики в параметрах DHCP отличаются. 

* Hello исключение если назначения статических IP-адрес tooa сетевой интерфейс как описано [здесь][virtual-networks-reserved-private-ip].
* В этом случае hello IP-адрес остается неизменным до тех пор, пока hello сетевого интерфейса не удаляется.

> [!IMPORTANT]
> В порядке tookeep hello всего развертывания простоту и управляемость ясно, что рекомендуется toosetup hello hello в СУБД высокой ДОСТУПНОСТИ и аварийного восстановления конфигурации в Azure в результате которого есть разрешение имен между hello, участвующих в разных ВМ партнерство ВМ.
> 
> 

## <a name="deployment-of-host-monitoring"></a>Развертывание мониторинга узлов
Для производственного использования приложений SAP в виртуальных машинах Azure SAP необходима hello возможность tooget данных мониторинга узла от физических узлах hello с hello виртуальных машинах Azure. Требуется определенный уровень исправлений SAP HostAgent, включающий эту возможность в SAPOSCOL и SAP HostAgent. Hello точный уровень исправления задокументирован в примечании SAP [1409604].

Hello детали развертывания компонентов, которые предоставляют tooSAPOSCOL данных узла и агента узла SAP и управление жизненным циклом hello этих компонентов, см. в разделе toohello [руководство по развертыванию][deployment-guide]

## <a name="3264829e-075e-4d25-966e-a49dad878737"></a>Особенности tooMicrosoft SQL Server
### <a name="sql-server-iaas"></a>IaaS в SQL Server
Начиная с Microsoft Azure, можно легко перенести существующие приложения SQL Server, построенных на платформе Windows Server tooAzure виртуальных машин. SQL Server на виртуальной машине позволяет вам tooreduce hello совокупную стоимость владения развертывания, управления и обслуживания приложений уровня организации, перенеся эти приложения tooMicrosoft Azure. С SQL Server в виртуальной машине Azure Администраторы и разработчики могут по-прежнему использовать hello тех же средств разработки и администрирования, которые доступны в локальной среде. 

> [!IMPORTANT]
> Мы не касаемся базы данных SQL Microsoft Azure, которой является платформой как предложение службы hello платформе Microsoft Azure. Обсуждение Hello в этом документе рассматривается запуск продукта SQL Server hello, известное для локальных развертываний в виртуальных машинах Azure, путем использования hello инфраструктура как служба функцию Azure. Возможности и функции базы данных в этих двух предложениях различаются, и их не следует путать друг с другом. См. также: <https://azure.microsoft.com/services/sql-database/>.
> 
> 

Настоятельно рекомендуется tooreview [это] [ virtual-machines-sql-server-infrastructure-services] документации, прежде чем продолжить.

Hello следующие разделы части документации hello в списке выше ссылку hello производятся статистические вычисления и упомянутых. Также упоминаются особенности, связанные с SAP. Некоторые основные понятия описаны более подробно. Однако настоятельно рекомендуется toowork через hello документацией перед тем как читать документацию SQL Server hello.

Существуют некоторые специальные сведения об SQL Server в IaaS, которые следует знать перед продолжением:

* **Соглашение об уровне обслуживания для виртуальных машин.** Существует соглашение об уровне обслуживания для виртуальных машин, работающих в Azure, которое можно найти здесь: <https://azure.microsoft.com/support/legal/sla/>.  
* **Поддержка версий SQL.** Для клиентов SAP на виртуальной машине Microsoft Azure поддерживается SQL Server 2008 R2 и более поздних версий. Более ранние выпуски не поддерживаются. Дополнительные сведения см. в этом общем [заявлении о поддержке](https://support.microsoft.com/kb/956893). Обратите внимание, что в целом SQL Server 2008 также поддерживается корпорацией Майкрософт. Однако из-за toosignificant функциональные возможности для SAP, в котором впервые появилась в SQL Server 2008 R2, SQL Server 2008 R2 является hello минимальной поддерживаемой версией для SAP. Имейте в виду, что SQL Server 2012 и 2014 была расширена путем более глубокой интеграции в сценарии IaaS hello (например, резервное копирование непосредственно в службу хранилища Azure). Таким образом мы ограничить этот документ tooSQL Server 2012 и 2014 с последним уровнем исправления для Azure.
* **Поддержка функций SQL.** Большинство функций SQL Server поддерживается на виртуальных машинах Microsoft Azure с некоторыми исключениями. **Создание отказоустойчивых кластеров SQL Server с использованием общих дисков не поддерживается**.  Распределенные технологии, такие как зеркальное отображение базы данных, группы доступности AlwaysOn, репликация, доставка журналов и Service Broker, поддерживаются в пределах одного региона Azure. SQL Server AlwaysOn также поддерживается между разными регионами Azure, как описано здесь: <https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.  Просмотрите hello [заявление о поддержке](https://support.microsoft.com/kb/956893) для получения дополнительных сведений. Пример toodeploy конфигурации AlwaysOn отображением в [это] [ virtual-machines-workload-template-sql-alwayson] статьи. Извлеките hello описаны рекомендации [здесь][virtual-machines-sql-server-infrastructure-services] 
* **Производительность SQL**: мы уверены, что Microsoft Azure, размещенные виртуальные машины работать оптимально в предложениями виртуализации в общедоступном облаке tooother сравнения, но отдельные результаты могут различаться. Ознакомьтесь с [этой][virtual-machines-sql-server-performance-best-practices] статьей.
* **Использование образов из Azure Marketplace**: hello самый быстрый способ toodeploy новой виртуальной Машины Microsoft Azure — toouse изображение из hello Azure Marketplace. Это образы в Azure Marketplace hello, содержащие SQL Server. образы Hello, где уже установлено приложение SQL Server не может использоваться для приложений SAP NetWeaver немедленно. Hello причина — параметры сортировки SQL Server по умолчанию hello устанавливается в рамках этих образов и не параметры сортировки hello, необходимые для систем SAP NetWeaver. В заказ toouse такие образы, проверьте hello действия, описанные в главах [с помощью образа SQL Server из Microsoft Azure Marketplace hello][dbms-guide-5.6]. 
* Дополнительные сведения см. в статье [Сведения о ценах](https://azure.microsoft.com/pricing/). Hello [руководство по лицензированию SQL Server 2012](https://download.microsoft.com/download/7/3/C/73CAD4E0-D0B5-4BE5-AB49-D5B886A5AE00/SQL_Server_2012_Licensing_Reference_Guide.pdf) и [руководство по лицензированию SQL Server 2014](https://download.microsoft.com/download/B/4/E/B4E604D9-9D38-4BBA-A927-56E4C872E41C/SQL_Server_2014_Licensing_Guide.pdf) также являются важный ресурс.

### <a name="sql-server-configuration-guidelines-for-sap-related-sql-server-installations-in-azure-vms"></a>Рекомендации по конфигурации SQL Server для связанных с SAP установок SQL Server на виртуальных машинах Azure
#### <a name="recommendations-on-vmvhd-structure-for-sap-related-sql-server-deployments"></a>Рекомендации по структуре виртуальных машин и виртуальных жестких дисков для связанных с SAP развертываний SQL Server
В соответствии с общее описание hello, исполняемые файлы SQL Server следует найти или установлен в системном диске hello диска ОС ВМ hello (диск C:\).  Как правило большая часть системных баз данных SQL Server hello не используются на высоком уровне рабочей нагрузкой SAP NetWeaver. Поэтому hello системные базы данных SQL Server (master, msdb и model) может оставаться на диске C:\ hello. Исключением может быть tempdb, которое в случае hello некоторые SAP ERP и любых рабочих нагрузок BW может потребоваться больше данных или объем операций ввода-вывода, не может поместиться в hello исходной виртуальной Машины. Для таких систем следует выполнить следующие шаги hello:

* Переместить toohello файлов данных основной базы данных tempdb hello одном логическом диске как hello основные файлы данных базы данных SAP hello.
* Добавьте любые tooeach файлы tempdb дополнительных данных из hello других логических дисков, содержащих файл данных базы данных пользователей SAP hello.
* Добавьте hello tempdb logfile toohello логический диск, содержащий файл журнала базы данных пользователя hello.
* **Только для типов ВМ, использующих локальный SSD** hello вычислительного узла tempdb данных и журнала файлов могут находиться на диск D:\ hello. Тем не менее, возможно, рекомендуется использовать toouse несколько файлов данных tempdb. Учтите, что тома диска D:\ различаются в зависимости от типа ВМ hello.

Эти конфигурации включить tempdb tooconsume больше места, чем hello системный диск — может tooprovide. В порядке toodetermine hello соответствующий размер tempdb можно проверить hello размеры tempdb в существующих системах, которые выполняются локально. Кроме того такая конфигурация позволит секунду в tempdb, который не может быть предоставлен hello системного диска. Еще раз системах, работающих в локальной среде может быть рабочей нагрузки используется toomonitor ввода-вывода для базы данных tempdb, чтобы можно было извлечь числа операций ввода-ВЫВОДА hello ожидать toosee на базе данных tempdb.

Конфигурации виртуальной Машины, которой работает SQL Server с базой данных SAP и где данных tempdb и файла журнала tempdb размещаются на диск D:\ hello выглядит следующим образом:

![Эталонная конфигурация виртуальной машины Azure IaaS для SAP][dbms-guide-figure-300]

Имейте в виду, что этот диск D:\ hello имеет различные размеры, зависящее от типа ВМ hello. Зависимость от hello требования к размеру базы данных tempdb может быть принудительного toopair данных tempdb и файлы журнала с hello SAP базы данных и файлов журнала в случаях, когда диск D:\ слишком мал.

#### <a name="formatting-hello-disks"></a>Форматирование дисков hello
Для SQL Server hello размер блока NTFS для дисков, содержащих данные SQL Server и журнала файлов должно быть 64 КБ. Нет необходимости tooformat hello диск D:\, не существует. Он предварительно отформатирован.

В порядке toomake том, что hello восстановление или создание баз данных не инициализируется hello файлы данных, фокусируясь hello содержимое файлов hello, необходимо убедиться, что служба SQL Server hello контекст пользователя hello работает в имеет определенные разрешения. Обычно эти разрешения имеют пользователи из группы администраторов Windows hello. Если hello службы SQL Server выполняется в контексте пользователя hello Windows неадминистративной пользователя, сначала необходимо tooassign этого пользователя hello право пользователя «Выполнение задач обслуживания тома».  Просмотрите сведения о hello в этой статье базы знаний Майкрософт: <https://support.microsoft.com/kb/2574695>

#### <a name="impact-of-database-compression"></a>Влияние сжатия базы данных
В конфигурациях, где пропускная способность ввода-вывода может стать ограничивающим фактором каждая мера, который сокращает число операций ввода-ВЫВОДА может помочь hello toostretch рабочей нагрузки, которая может выполняться в сценарии IaaS, например Azure. Таким образом Если это еще не сделано, применение сжатия SQL Server PAGE настоятельно рекомендуется SAP и Майкрософт перед отправкой существующих tooAzure базы данных SAP.

Рекомендация Hello tooperform сжатие базы данных перед отправкой tooAzure дается по двум причинам:

* меньше Hello объем данных toobe отправлен.
* Hello продолжительность выполнения сжатия hello короче, предполагая, что можно использовать более мощное оборудование с дополнительные процессоры или более высокой пропускной способности ввода-вывода или меньше операций ввода-вывода задержки в локальной среде.
* Меньшего размера базы данных может привести затрат сборки для выделения места на диске

Сжатие баз данных работает на виртуальных машинах Azure так же, как и в локальной среде. Дополнительные сведения о том, как toocompress существующей базы данных SAP SQL Server, установите флажок: <https://blogs.msdn.com/b/saponsqlserver/archive/2010/10/08/compressing-an-sap-database-using-report-msscompress.aspx>

### <a name="sql-server-2014--storing-database-files-directly-on-azure-blob-storage"></a>SQL Server 2014: хранение файлов базы данных непосредственно в хранилище BLOB-объектов Azure
SQL Server 2014 открывает файлы базы данных toostore hello возможность непосредственно в хранилище больших двоичных объектов Azure без hello «оболочку» вокруг них виртуального жесткого диска. Особенно с использованием стандартного хранилища Azure или более компактные типы ВМ этому сценариях, где можно преодолеть ограничения операций ввода-ВЫВОДА, который будет применен ограниченному числу дисков, которые могут быть более компактные типы ВМ подключенного toosome hello. Это возможно в случае с пользовательскими базами данных, но не с системными базами данных SQL Server. Также это возможно для файлов данных и журналов SQL Server. Если вы хотите toodeploy SAP SQL Server базы данных таким образом, а не «оболочку» ее виртуальные жесткие диски, учитывайте следующие hello:

* toobe потребности Hello используемую учетную запись хранения в hello того региона Azure как hello, используемые toodeploy hello, выполняемых в виртуальной Машине SQL Server.
* Ранее перечисленными hello распределение VHD по разным учетным записям хранения Azure соображения для этого метода также развертываний. Означает hello операций ввода-вывода, учитываются hello ограничения hello учетной записи хранилища Azure.

[comment]: <> (Пользователь MSSedusch: но при этом будет использоваться пропускная способность сети, а не хранилища, не так ли?)

Сведения об этом типе развертывания представлены здесь: <https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure>.

В порядке toostore файлов данных SQL Server непосредственно в хранилище Azure класса Premium, вы должны выпуска исправления toohave минимальное SQL Server 2014, которые здесь описаны: <https://support.microsoft.com/kb/3063054>. Хранение файлов данных SQL Server в стандартном хранилище Azure работать с версией SQL Server 2014 выпущена hello. Однако очень такие же исправления hello содержит еще один ряд исправлений, которые повышения надежности hello прямом использовании хранилища больших двоичных объектов для файлов данных SQL Server и резервных копий. Поэтому мы, в целом, рекомендуем использовать эти исправления.

### <a name="sql-server-2014-buffer-pool-extension"></a>Расширение буферного пула SQL Server 2014
В SQL Server 2014 появилась новая функция, которая называется "Расширение буферного пула". Эти функции расширяют возможности hello буферный пул SQL Server, который сохраняется в памяти с помощью кэша второго уровня, поддерживаемый SSDs локального сервера или виртуальной Машине. Это позволяет tookeep большего рабочего набора данных «в памяти». Сравниваемые tooaccessing доступа hello стандартного хранилища Azure в расширение hello hello буферного пула, который хранится на локальной SSD ВМ Azure выполняется быстрее многих факторов.  Таким образом используя локальный диск D:\ hello hello типов ВМ, имеющих отличный операций ввода-ВЫВОДА и пропускной способности может быть очень другого способа tooreduce hello IOPS загрузки в службу хранилища Azure и значительно уменьшить время отклика запросов. Это применимо особенно в том случае, если хранилище класса Premium не используется. В случае хранения Premium и использовании hello hello кэша чтения Azure Premium на вычислительном узле hello согласно рекомендациям для файлов данных, должны больших различий нет. Причиной является то, что оба кэшей (расширение буферного пула для SQL Server и кэша чтения хранилища Premium) с помощью локальных дисках вычислительных узлов hello hello.
Дополнительные сведения об этих возможностях см. в этой документации: <https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension>. 

### <a name="backuprecovery-considerations-for-sql-server"></a>Рекомендации по резервному копированию и восстановлению для SQL Server
При развертывании SQL Server в Azure методику резервного копирования необходимо пересмотреть. Даже если система hello не продуктивной системы, hello SAP размещенной в SQL Server необходимо резервную копию базы данных периодически. Так как служба хранилища Azure сохраняет три образа, резервное копирование становится менее важным с учетом toocompensating сбоя хранилища. Hello Главная причина поддержки правильную план резервного копирования и восстановления не ограничивается компенсации логических или пользовательских ошибок, предоставляя моменту времени возможности восстановления. Поэтому цель hello tooeither использовать резервные копии toorestore hello базу данных обратно tooa определенных момент времени или toouse hello резервных копий в Azure tooseed другой системы путем копирования существующей базы данных hello. Например, можно перейти от уровня 2 SAP конфигурации tooa трехуровневые системы настройки hello же системы путем восстановления резервной копии.

Существует три способа toobackup SQL Server tooAzure хранилища:

1. SQL Server 2012 CU4 и более поздней версии может изначально резервное копирование баз данных tooa URL. Это подробно описывается в блоге hello [новые функциональные возможности SQL Server 2014 — часть 5 — улучшения резервного копирования и восстановления](https://blogs.msdn.com/b/saponsqlserver/archive/2014/02/15/new-functionality-in-sql-server-2014-part-5-backup-restore-enhancements.aspx). Ознакомьтесь с разделом [SQL Server 2012 с пакетом обновления 1 (SP1) и накопительным пакетом обновления 4 (CU4) и последующие выпуски][dbms-guide-5.5.1].
2. TooSQL предыдущие выпуски SQL Server 2012 CU4 могут использовать tooa toobackup функциональность перенаправления виртуального жесткого диска и по сути перейти поток записи hello к расположения службы хранилища Azure, которая была настроена. Ознакомьтесь с разделом [SQL Server 2012 с пакетом обновления 1 (SP1) и накопительным пакетом обновления 3 (CU3) и предыдущие выпуски][dbms-guide-5.5.2].
3. Последний способ Hello — tooperform обычной команды резервного копирования toodisk SQL Server на дисковое устройство. Это шаблон развертывания идентичные toohello локальной и не описываются подробно в этом документе.

#### <a name="0fef0e79-d3fe-4ae2-85af-73666a6f7268"></a>SQL Server 2012 с пакетом обновления 1 (SP1) и накопительным пакетом обновления 4 (CU4) и последующие выпуски
Эта функция позволяет хранилища больших двоичных ОБЪЕКТОВ резервного копирования tooAzure toodirectly. Этот метод не должен создать резервную копию tooother дисках, которые потребляют диска и производительности операций ввода-ВЫВОДА. Идея Hello это по сути:

 ![С помощью резервного копирования SQL Server 2012 tooMicrosoft BLOB-ОБЪЕКТА хранилища Azure][dbms-guide-figure-400]

в этом случае Hello преимущество заключается в необходимости резервные копии SQL Server toospend дисков toostore на один не. Таким образом вы меньшее количество дисков выделенной и hello вся пропускная способность операций ввода-ВЫВОДА может использоваться для файлов данных и журнала диска. Обратите внимание, что максимальный размер резервной копии hello ограниченного tooa не более 1 ТБ, описанные в разделе hello «Ограничения» в этой статье: <https://docs.microsoft.com/sql/relational-databases/backup-restore/sql-server-backup-to-url#limitations>. Если размер резервной копии hello, несмотря на использование сжатия резервных копий SQL Server будет превышать 1 ТБ, размер, hello функциональные возможности, описанные в главах [SQL Server 2012 SP1 CU3 и более ранних версиях] [ dbms-guide-5.5.2] в этом документе, должен быть использовать toobe.

[Связанные документации](https://docs.microsoft.com/sql/relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure) описанием hello восстановление баз данных из резервных копий в хранилище больших двоичных объектов Azure рекомендуется не toorestore непосредственно из хранилища больших двоичных ОБЪЕКТОВ Azure, если резервная копия hello > 25 ГБ. Рекомендация Hello в этой статье просто основанный на вопросы производительности, а не из-за ограничений toofunctional. Поэтому для разных случаев могут применяться разные условия.

Документацию по настройке и использованию преимуществ этого типа архивации можно найти в [этом](https://docs.microsoft.com/sql/relational-databases/tutorial-use-azure-blob-storage-service-with-sql-server-2016) учебнике.

Пример hello последовательности шагов могут считываться [здесь](https://docs.microsoft.com/sql/relational-databases/backup-restore/sql-server-backup-to-url).

Автоматизация резервного копирования, оно имеет наивысший важность toomake убедиться, что различными именами hello больших двоичных объектов для каждой резервной копии. В противном случае они будут перезаписаны и hello цепочка восстановления будет разорвана.

Порядок не toomix копирование действия между hello три разных типа резервных копий при разных контейнеров рекомендуется toocreate под учетной записи хранилища hello, используемой для резервного копирования. Hello контейнеры можно разделять по ВМ только или по типу ВМ и резервного копирования. Hello схемы может выглядеть так:

 ![С помощью резервного копирования SQL Server 2012 tooMicrosoft BLOB-ОБЪЕКТА хранилища Azure — разные контейнеры в отдельной учетной записи хранения][dbms-guide-figure-500]

В примере hello выше hello, резервные копии не будет выполняться в учетной записи же хранилище, где hello hello развернутых виртуальных машин. Будет специально для резервных копий hello новой учетной записи хранения. В учетных записях хранения hello будет разные контейнеры, созданные с помощью матрицы hello тип резервного копирования и hello имя виртуальной Машины. Такая сегментация облегчает проще tooadministrate hello резервные копии hello разных ВМ.

большие двоичные объекты Hello один непосредственно записи hello резервные копии, не добавляете toohello число дисков данных hello виртуальной машины. Следовательно, можно использовать максимум hello hello конкретной SKU ВМ для данных hello подключенных дисков данных и файл журнала транзакций и по-прежнему выполнять резервное копирование в контейнер хранилища. 

#### <a name="f9071eff-9d72-4f47-9da4-1852d782087b"></a>SQL Server 2012 с пакетом обновления 1 (SP1) и накопительным пакетом обновления 3 (CU3) и предыдущие выпуски
Hello первым шагом в порядке tooachieve необходимо выполнить резервное копирование непосредственно в хранилище Azure будет toodownload hello MSI-файл, который связан слишком[это](https://www.microsoft.com/download/details.aspx?id=40740) KBA статьи.

Загрузите файл установки hello x64 и документации hello. Hello файл устанавливает программу, которая называется: «Microsoft SQL Server Backup tooMicrosoft средства Azure». Внимательно прочтите документацию hello hello продукта.  Программа Hello работает в основном hello следующими способами:

* Из hello стороне SQL Server, определяется местоположение диска для резервного копирования SQL Server hello (не используйте диск D:\ hello для этого).
* Hello программы можно toodefine правила, которые могут быть разных типов используемых toodirect контейнеров хранилища Azure toodifferent резервных копий.
* После правила hello hello средство перенаправляет hello поток записи резервной копии tooone hello объекта toohello VHD/дисков hello место хранения Azure, которая была определена ранее.
* Средство Hello оставляет файл-заглушку небольшого размера несколько КБ hello VHD-диск, который был определен для hello SQL Server резервного копирования. **Этот файл должен оставаться на место хранения hello, так как она является обязательным toorestore снова из хранилища Azure.**
  * Если вы потеряли файл заглушки hello (например, утрачен hello носителя, содержащего файл заглушки hello) и выбора hello возможность резервного копирования tooa учетной записью хранения Microsoft Azure, можно восстановить файл заглушки hello через хранилища Microsoft Azure загрузив его из контейнера хранилища hello, в котором она размещена. Затем следует поместить файл заглушки hello в папку на локальном компьютере hello, где настроенных toohello toodetect и передачи hello средство же контейнер с hello одинаковым паролем шифрования, если используется шифрование с исходное правило hello. 

Это означает, что схемы hello как описано выше для последних версий SQL Server могут быть помещены в месте, а также в версиях SQL Server, в которых не разрешена прямая адресация расположения службы хранилища Azure.

Этот способ не следует использовать с более новыми версиями SQL Server, которые изначально поддерживают резервное копирование в хранилище Azure. Исключениями являются которых ограничения встроенного резервного копирования hello в Azure блокируют выполнение такого резервного копирования в Azure.

#### <a name="other-possibilities-toobackup-sql-server-databases"></a>Другие базы данных SQL Server можно использовать toobackup
Другие возможности toobackup базы данных является tooa дисков tooattach дополнительные данные виртуальной Машины, toostore резервных копий для использования по. В этом случае необходимо убедиться, что диски hello не запущены полного toomake. Если это так hello, потребовалось бы toounmount hello дисков и поэтому toospeak «Архивация» и замените его нового пустого диска. Вы вышли из строя этого пути, следует ли tookeep эти VHD в отдельных учетных записей хранилища Azure из hello те, которые hello виртуальные жесткие диски с файлами базы данных hello.

Вторая возможность — toouse большая ВМ, который может иметь несколько дисков, например D14 с 32VHDs. Используйте это та гибкая среда, где можно создать общие папки, используются затем как целевые объекты резервного копирования для различных серверов СУБД hello toobuild дисковых пространств.

Некоторые практические рекомендации также описаны [здесь](https://blogs.msdn.com/b/sqlcat/archive/2015/02/26/large-sql-server-database-backup-on-an-azure-vm-and-archiving.aspx) . 

#### <a name="performance-considerations-for-backupsrestores"></a>Рекомендации по ускорению резервного копирования и восстановления
Как в исходных развертываниях производительности резервного копирования и восстановления зависит от того, сколько томов может читаться параллельно и могут быть какие hello пропускной способности этих томов. Кроме того hello потребление ресурсов ЦП при сжатии резервной копии может играют важную роль на виртуальных машинах с просто копирование tooeight потоков ЦП. Исходя из сказанного выше, можно сделать следующие выводы.

* Hello меньше hello количество дисков, используемые файлы данных toostore hello, hello меньшего hello общую пропускную способность при чтении.
* Здравствуйте, меньшим числом потоков ЦП в ВМ hello hello, hello более серьезное влияние hello сжатие резервных копий.
* Здравствуйте, чем меньше целевых объектов (BLOB-объектов, виртуальных жестких дисков или дисков) toowrite Здравствуйте резервных копий, hello меньшей пропускной способности hello.
* hello Hello меньший размер виртуальной Машины, hello меньшего размера hello пропускной способности квота хранилища записи и чтения из хранилища Azure. Независимо от ли резервные копии hello сохраняются непосредственно на больших двоичных объектов Azure или они хранятся в виртуальные жесткие диски, еще раз, сохраняются в BLOB-объектов Azure.

При использовании больших двоичных ОБЪЕКТОВ хранилища Microsoft Azure в качестве целевой диск резервного копирования hello в последних версиях, их ограниченные toodesignating только один целевой URL-адрес для каждого конкретного резервного копирования.

Однако при использовании hello «Microsoft SQL Server Backup tooMicrosoft средства Azure» в предыдущих версиях, можно определить более одного целевого файла. С более чем одним целевым объектом hello резервное копирование можно масштабировать и hello пропускная способность резервного копирования hello выше. Это приведет к созданию в нескольких файлах, а также в hello учетной записи хранилища Azure. В нашем тестировании с помощью нескольких файловых назначений определенно можно достичь пропускной способности hello, какой из них можно достичь с помощью расширений резервного копирования hello реализуется в из SQL Server 2012 SP1 CU4 на. Вы также не блокируются hello ограничение 1 ТБ как hello собственного резервного копирования в Azure.

Однако, иметь в виду, hello пропускная способность также зависит от расположения hello hello учетной записи хранилища Azure, использовать для резервного копирования hello. Представление может быть toolocate hello учетной записи хранения в разных регионах hello виртуальные машины запущены в. Например можно запустить конфигурацию виртуальной Машины hello в Западной Европе, а поместить hello учетной записи хранилища, используемая tooback сводится в Северной Европе. Определенно оказывает влияние на пропускную способность резервного копирования hello и вероятность toogenerate 150 МБ/с пропускной способностью как кажется toobe возможна в случаях, где запущен hello целевое хранилище и виртуальные машины hello в hello одного регионального центра обработки данных.

#### <a name="managing-backup-blobs"></a>Управление BLOB-объектами при резервном копировании
Нет резервных копий требование toomanage hello самостоятельно. Поскольку hello ожидается, что путем выполнения резервных копий журналов транзакций часто создаются много BLOB-объектов, администрирование этих BLOB-объектов может легко перегрузить портал Azure hello. Таким образом это рекомендуется tooleverage обозреватель хранилища Azure. Существует несколько хороших доступных обозревателей, которые могут помочь toomanage учетную запись хранилища Azure

* Microsoft Visual Studio с установленным пакетом SDK для Azure (<https://azure.microsoft.com/downloads/>).
* Обозреватель службы хранилища Microsoft Azure (<https://azure.microsoft.com/downloads/>).
* Инструменты сторонних производителей

Более подробные сведения об архивации и SAP в Azure, см. в разделе слишком[hello руководство по SAP резервного копирования](sap-hana-backup-guide.md) для получения дополнительной информации.

### <a name="1b353e38-21b3-4310-aeb6-a77e7c8e81c8"></a>С помощью образа SQL Server из Microsoft Azure Marketplace hello
Корпорация Майкрософт предлагает ВМ в hello Azure Marketplace, уже содержащие версии SQL Server. Для клиентов SAP, которым требуются лицензии на SQL Server и Windows это может быть возможность титульной toobasically hello необходимость лицензий путем развертывания VM с уже установленным SQL Server. В порядке toouse такие образы для SAP, hello следующие вопросы должны toobe внесены.

* Неознакомительные версии SQL Server Hello получить требуют больших затрат, чем просто только для Windows ВМ, развернутой из Azure Marketplace. См. эти цены toocompare статьи: <https://azure.microsoft.com/pricing/details/virtual-machines/windows/> и <https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-enterprise/>. 
* Использовать можно только те выпуски SQL Server, которые поддерживаются SAP, например SQL Server 2012.
* Hello параметры сортировки экземпляра SQL Server hello, который устанавливается на виртуальных машинах hello, предусмотренных в Azure Marketplace hello не параметры сортировки hello SAP NetWeaver требует toorun экземпляр SQL Server hello. Вы можете изменить параметры сортировки hello хотя и с hello указаниям, приведенным в следующем разделе hello.

#### <a name="changing-hello-sql-server-collation-of-a-microsoft-windowssql-server-vm"></a>Изменение параметров сортировки SQL Server виртуальной машины Microsoft Windows или SQL Server hello
Поскольку hello образов SQL Server в Azure Marketplace hello не настроены параметры сортировки toouse hello, необходимый для приложений SAP NetWeaver, ему toobe, изменить его сразу после развертывания hello. SQL Server 2012 это можно сделать с помощью hello следующие действия как можно скорее hello которой развернута виртуальная машина, и администратор может toolog в hello развертывания ВМ:

* Откройте окно командной строки Windows с правами администратора.
* Измените каталог hello tooC:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012.
* Выполните команду hello: Setup.exe/quiet/Action = REBUILDDATABASE/instancename = MSSQLSERVER/sqlsysadminaccounts =`<local_admin_account_name`>/SQLCOLLATION = SQL_Latin1_General_Cp850_BIN2   
  * `<local_admin_account_name`> hello учетная запись, которой был определен как hello учетной записи администратора при развертывании hello виртуальной Машины для hello впервые hello коллекции.

процесс Hello обычно занимает несколько минут. В порядке toomake убедиться, что ли шаг hello завершено с hello правильный результат, выполните hello следующие шаги.

* Откройте среду SQL Server Management Studio.
* Откройте окно запроса.
* Выполните команду sp_helpsort hello в главной базе данных SQL Server hello.

Hello требуемого результат должен выглядеть так:

    Latin1-General, binary code point comparison sort for Unicode Data, SQL Server Sort Order 40 on Code Page 850 for non-Unicode Data

Если это не является результатом hello, ОСТАНОВИТЕ развертывание SAP и выясните, почему hello установки команда не работает должным образом. Развертывание приложений SAP NetWeaver в экземпляре SQL Server с разных кодовых страниц для SQL Server не hello упомянутый выше является **не** поддерживается.

### <a name="sql-server-high-availability-for-sap-in-azure"></a>Высокая доступность SQL Server для SAP в Azure
Как упоминалось выше в этом документе нет возможности toocreate общего места для хранения, который необходим для использования hello hello старые функции высокого уровня доступности SQL Server. Эта функциональность устанавливала не менее двух экземпляров SQL Server в Windows Server отказоустойчивого кластера (WSFC) с помощью общего диска для hello пользовательских баз данных (и, в конечном счете, tempdb). Это стандартная высокого уровня доступности долго hello метод, который также поддерживаемый SAP. Поскольку Azure не поддерживает общее хранилище, невозможно реализовать конфигурации высокого уровня доступности SQL Server с конфигурацией кластера общих дисков. Однако многие другие методы высокого уровня доступности все равно могут иметь и описаны в следующих разделах hello.

#### <a name="sql-server-log-shipping"></a>Доставка журналов SQL Server
Один из методов hello объекта высокого уровня доступности (HA) — доставка журналов SQL Server. Если hello виртуальных машин, участвующих в конфигурации высокого уровня ДОСТУПНОСТИ hello имеют работающее разрешение имен, то проблем не существует и установки hello в Azure не отличается от настройки, в которой выполняется в локальной среде. Не рекомендуется toorely на только разрешение IP-адресов. С toosetting отношении доставки журналов и hello принципах доставки журналов документации:

<https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server>

В порядке tooreally добиться высокой доступности, одно из них должно toodeploy hello виртуальных машин, которые находятся в пределах такой toobe конфигурации доставки журналов в рамках hello одну группу доступности Azure.

#### <a name="database-mirroring"></a>Зеркальное отображение базы данных
Зеркальное отображение базы данных, поддерживаемое SAP (см. Примечание SAP [965908]) опирается на определение резервного участника в строку подключения SAP hello. В случаях hello между организациями, предполагается, что hello две виртуальные машины находятся в hello одного домена и что пользовательский контекст hello hello два SQL Server, экземпляры участников запущены под пользователем домена и иметь соответствующие права в hello двух экземплярах SQL Server. Таким образом hello настройки зеркального отображения базы данных в Azure не отличается от обычной локальной установки и конфигурации.

Как только для облака развертываний, простой способ hello-toohave другой домен установки в Azure toohave этих ВМ СУБД (и в идеале выделенных ВМ SAP) в одном домене.

Если домен не поддерживается, один можно также использовать сертификаты для hello базы данных конечные точки зеркального отображения, как описано здесь: <https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql>

Учебник tooset зеркального отображения базы данных в Azure можно найти здесь: <https://docs.microsoft.com/sql/database-engine/database-mirroring/database-mirroring-sql-server> 

#### <a name="sql-server-always-on"></a>AlwaysOn в SQL Server
Always On поддерживается для SAP локально (см. Примечание SAP [1772688]), это поддерживаемых toobe используется в сочетании с SAP в Azure. Hello фактов, которые не могут toocreate общих дисков в Azure не означает, что нельзя создать конфигурацию с всегда в Windows Server отказоустойчивого кластера (WSFC) между разными ВМ. Только означает, что у вас toouse вероятность hello общий диск как кворума в конфигурации кластера hello. Таким образом можно создать конфигурацию с всегда в WSFC в Azure и просто не выбирать тип кворума hello, использующий общий диск. Hello среды Azure эти виртуальные машины развертываются в должно разрешаться hello виртуальных машин по имени и hello виртуальные машины должны находиться в hello того же домена. Это касается развертываний только в Azure и распределенных развертываний. Существует несколько особых рекомендаций по развертыванию hello прослушивателя группы доступности SQL Server (не toobe путать с hello группе доступности Azure) с момента Azure на данный момент времени не допускает toosimply создать объект AD/DNS, так как локальной. Таким образом некоторые действия установки, необходимые tooovercome hello поведения Azure.

Ниже приведены некоторые рекомендации по использованию прослушивателя группы доступности.

* С помощью прослушивателя группы доступности возможен только в Windows Server 2012 или более поздней версии в качестве гостевой ОС hello виртуальной Машины. Для Windows Server 2012 необходимо убедиться, что это исправление применяется toomake: <https://support.microsoft.com/kb/2854082> 
* Windows Server 2008 R2 это исправление не существует, необходимо всегда на toobe использовались в hello же так, как зеркальное отображение базы данных, указав участника отработки отказа в строке подключения hello (с использованием hello default.pfl параметр SAP баз данных SQL Server/mss/server — см. Примечание SAP [965908]).
* При использовании прослушивателя группы доступности, виртуальные машины базы данных hello необходимость toobe подключен tooa выделенные подсистемы балансировки нагрузки. Имя разрешения в развертываниях только в облаке либо потребует всех ВМ SAP системы (серверы приложений, СУБД сервера и сервера (A) SCS) находятся в одной виртуальной сети hello или потребует от слоя hello SAP приложения обслуживания файла etc\host hello в порядок tooget hello ВМ имена hello разрешить VM SQL Server. В порядке tooavoid назначения Azure новых IP-адресов в случаях, когда обе виртуальные машины случайно завершения работы один следует назначить статические IP-адреса сетевых интерфейсов toohello этих виртуальных машин в hello конфигурации Always On (который определяет статический IP-адрес описан в разделе [это] [ virtual-networks-reserved-private-ip] статье)

[comment]: <> (Старые блоги)
[comment]: <> (<https://blogs.msdn.com/b/alwaysonpro/archive/2014/08/29/recommendations-and-best-practices-when-deploying-sql-server-alwayson-availability-groups-in-windows-azure-iaas.aspx>, <https://blogs.technet.com/b/rmilne/archive/2015/07/27/how-to-set-static-ip-on-azure-vm.aspx>) 
* Особые действия, необходимые при построении конфигурации кластера WSFC hello, где hello кластера требуется специальный IP-адрес назначения, так как Azure в текущей функциональности назначается имя кластера hello hello IP-адресом кластера hello hello узла создается. Это означает, что выполнить ручное действие должно быть выполнено tooassign другого кластера toohello IP адрес.
* Hello прослушивателя группы доступности будет создан в Azure с конечными точками TCP/IP, назначаемые toohello виртуальных машин, запущенных hello первичная и Вторичная реплики группы доступности hello toobe.
* Может возникнуть необходимость toosecure эти конечные точки со списками управления доступом.

[comment]: <> (TODO старый блог)
[comment]: <> (Здравствуйте, подробные инструкции и потребности установки конфигурации AlwaysOn в Azure лучше всего реализовывать при прохождении через hello учебника доступных [here][virtual-machines-windows-classic-ps-sql-alwayson-availability-groups])
[comment]: <> (Предварительно настроенное установки AlwaysOn с помощью коллекции Azure hello < https://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx>)
[comment]: <> (Создание прослушивателя группы доступности лучше всего описано в [этом][virtual-machines-windows-classic-ps-sql-int-listener] руководстве)
[comment]: <> (Защита сетевых конечных точек с помощью списков управления доступом лучше всего объясняется здесь:)
[comment]: <> (*    <https://michaelwasham.com/windows-azure-powershell-reference-guide/network-access-control-list-capability-in-windows-azure-powershell/>)
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/08/31/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-1-of-2.aspx> )
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/01/weekend-scripter-creating-acls-for-windows-azure-endpoints-part-2-of-2.aspx>)  
[comment]: <> (*    <https://blogs.technet.com/b/heyscriptingguy/archive/2013/09/18/creating-acls-for-windows-azure-endpoints.aspx>) 

Возможные toodeploy SQL Server группы доступности AlwaysOn превышает также разных регионах Azure. Эта функция использует подключение hello Azure VNet-Vnet ([подробности][virtual-networks-configure-vnet-to-vnet-connection]).

[comment]: <> (TODO старый блог)
[comment]: <> (Ниже описан Hello Настройка группы доступности AlwaysOn SQL Server в этом случае: < https://blogs.technet.com/b/dataplatforminsider/archive/2014/06/19/sql-server-alwayson-availability-groups-supported-between-microsoft-azure-regions.aspx>.) 

#### <a name="summary-on-sql-server-high-availability-in-azure"></a>Сводка по высокой доступности SQL Server в Azure
Учитывая hello факт, что хранилище Azure обеспечивает защиту содержимого hello, имеется один меньше tooinsist причина в образе горячей замены. Это означает, что ваш сценарий обеспечения высокой доступности требуется tooonly защититься от hello в следующих случаях:

* В целом, из-за toomaintenance в кластере серверов hello в Azure или по другим причинам недоступности hello виртуальной Машины
* Проблемы с программным обеспечением в экземпляре SQL Server hello
* Защита от ошибок пользователей при удалении данных, когда требуется восстановление на определенный момент времени

Просмотр соответствующих технологий, один можно утверждать, что первых двух случаях hello контролирует зеркального отображения базы данных или Always On, а третий вариант hello может быть сопоставлен только доставку журналов.

Требуется toobalance hello более сложные настройки Always On tooDatabase по сравнению с hello преимуществами Always On зеркального отображения. Эти преимущества перечислены ниже.

* Вторичные реплики для чтения.
* Резервные копии из вторичных реплик.
* Улучшенная масштабируемость.
* Несколько вторичных реплик.

### <a name="9053f720-6f3b-4483-904d-15dc54141e30"></a>Общие сведения об SQL Server для SAP в Azure
Это руководство содержит много рекомендаций, и мы советуем прочитать его несколько раз перед планированием развертывания в Azure. В общем случае, быть убедиться, что toofollow hello top десяти основных рекомендаций по СУБД в Azure:

[comment]: <> (В 2,3 раза более высокая пропускная способность, чем что? Чем один виртуальный жесткий диск?)
1. Используйте hello последний выпуск СУБД, такие как SQL Server 2014 с hello наибольшие преимущества в Azure. Для SQL Server — SQL Server 2012 SP1 CU4, включающий функции hello резервного копирования в хранилище Azure. Тем не менее, в сочетании с SAP мы бы рекомендовали по крайней мере последних CU SQL Server 2014 SP1 CU1 или SQL Server 2012 SP2 и hello.
2. Тщательно спланируйте ландшафт системы SAP в структуру файлов данных hello Azure toobalance с ограничениями Azure:
   * Слишком много дисков необязательно, но имеют достаточно tooensure, можно получить доступ к вашей необходимое значение IOPS.
   * Если вы не используете Управляемые диски, помните, что количество операций ввода-вывода также ограничено для каждой учетной записи хранения Azure, а количество учетных записей хранения ограничено для каждой подписки Azure ([подробнее об этом][azure-subscription-service-limits]). 
   * Только используйте чередование дисков, при необходимости tooachieve более высокую пропускную способность.
3. Никогда не устанавливать программное обеспечение или поместите все файлы, которые требуют сохранения на диск D:\ hello, поскольку он является несохраняемым, и все содержимое этого диска теряется при перезапуске Windows.
4. Не используйте кэширование дисков для хранилища Azure класса Standard.
5. Не используйте геореплицированные учетные записи хранилища Azure.  Используйте локальную избыточность для рабочих нагрузок СУБД.
6. Используйте поставщика СУБД HA/DR решения tooreplicate базы данных.
7. Всегда используйте разрешение имен, не полагайтесь на IP-адреса.
8. Используйте hello наибольший возможных сжатие базы данных. Для SQL Server это сжатие страниц.
9. Соблюдайте осторожность при использовании образов SQL Server из hello Azure Marketplace. При использовании hello SQL Server, необходимо изменить параметры сортировки экземпляра hello перед установкой любого системы SAP NetWeaver на нем.
10. Установка и настройка hello, мониторинг узла SAP для Azure, как описано в [руководство по развертыванию][deployment-guide].

## <a name="specifics-toosap-ase-on-windows"></a>Особенности tooSAP ASE в Windows
Начиная с Microsoft Azure, можно легко перенести вашей существующей tooAzure приложений SAP ASE виртуальных машин. SAP ASE на виртуальной машине позволяет вам tooreduce hello совокупную стоимость владения развертывания, управления и обслуживания приложений уровня организации, перенеся эти приложения tooMicrosoft Azure. С SAP ASE на виртуальной машине Azure Администраторы и разработчики могут по-прежнему использовать hello тех же средств разработки и администрирования, которые доступны в локальной среде.

Отсутствует SLA для hello виртуальных машин Azure, которые можно найти здесь: <https://azure.microsoft.com/support/legal/sla/virtual-machines>

Мы уверены, что Microsoft Azure, размещенные виртуальные машины очень хорошо выполняет в предложениями виртуализации в общедоступном облаке tooother сравнения, но отдельные результаты могут различаться. Изменения размера SAPS числа различных SAP сертифицированные SKU ВМ предоставляется в отдельном Примечание SAP hello SAP [1928533].

Инструкции и рекомендации, приведенные в учета toohello использования хранилища Azure, развертывания ВМ SAP или мониторинга SAP применяются toodeployments из SAP ASE вместе с приложениями SAP, как указано на протяжении hello первые четыре главах этого документа.

### <a name="sap-ase-version-support"></a>Поддержка версий SAP ASE
SAP в настоящее время поддерживает версию SAP ASE 16.0 для использования с продуктами SAP Business Suite. Все обновления для сервера SAP ASE или toobe драйверы JDBC и ODBC с SAP Business Suite продукты предоставляются только через hello услугами SAP на: <https://support.sap.com/swdc>.

Как и для установки локально не загружать обновления для сервера SAP ASE hello, или hello JDBC и драйверы ODBC непосредственно из Sybase веб-сайтов. Подробные сведения об исправлениях, которые поддерживаются для использования с SAP Business Suite продуктов локально и в виртуальных машинах Azure см. следующие примечания по SAP hello:

* [1590719]
* [1973241]

Общие сведения о запуске SAP Business Suite в SAP ASE можно найти в hello [SCN](https://www.sap.com/community/topic/ase.html)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Рекомендации по конфигурации SAP ASE для связанных с SAP установок SAP ASE на виртуальных машинах Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Структура hello развертывания SAP ASE
В соответствии с общее описание hello, исполняемые файлы SAP ASE следует найти или установлен в системном диске hello диска ОС ВМ hello (диск c:\). Как правило большинство hello SAP ASE инструменты из системы и баз данных, являются не действительно жесткое оптимизированный за счет использования рабочей нагрузкой SAP NetWeaver. Поэтому hello системы и средств баз данных (master, model, saptools, sybmgmtdb и sybsystemdb) может оставаться на диске C:\ hello также. 

Исключением может быть hello временной базы данных, содержащая все рабочие таблицы и временные таблицы, созданные приложением SAP ASE, который в случае некоторых SAP ERP и любых рабочих нагрузок BW может потребоваться больше данных или объем операций ввода-вывода, не может поместиться в исходной hello Диска ОС ВМ (диск c:\).

В зависимости от hello версия SAPInst/SWPM используется система tooinstall hello, hello база данных может содержать:

* Отдельную базу tempdb SAP ASE, которая создается при установке SAP ASE.
* SAP ASE tempdb, созданные при установке SAP ASE и дополнительных saptempdb, созданные приветствия программы установки в SAP
* SAP ASE tempdb, созданные при установке SAP ASE и дополнительные базы данных tempdb, который был создан вручную (например следующее примечание SAP [1752266]) требования к определенной базе данных tempdb ERP/BW toomeet

В случае определенных ERP или всех рабочих нагрузок BW имеет смысл, в tooperformance учета tookeep hello tempdb устройства hello дополнительно создать tempdb (SWPM или вручную) на диске C:\. Если нет дополнительных tempdb, рекомендуется toocreate одно (Примечание SAP [1752266]).

Для таких систем hello следует выполнить следующие действия для hello дополнительно создать tempdb:

* Переместить hello первой базы данных tempdb toohello первый одноранговой базы данных SAP hello
* Добавление базы данных tempdb tooeach устройств из hello VHD, содержащих устройства базы данных SAP hello

Это tooeither tempdb конфигурации позволяет использовать больше места, чем hello системный диск — может tooprovide. Как ссылку можно проверить размеры устройств hello tempdb в существующих системах, которые выполняются локально. Или такой конфигурации позволит секунду в tempdb, который не может быть предоставлен hello системного диска. Снова системах, работающих в локальной среде может быть рабочей нагрузки используется toomonitor ввода-вывода для базы данных tempdb.

Никогда не помещайте каких-либо устройств SAP ASE на диск D:\ ВМ hello hello. Это также применимо toohello tempdb, даже если hello объекты хранятся в базе данных tempdb hello являются временными.

#### <a name="impact-of-database-compression"></a>Влияние сжатия базы данных
В конфигурациях, где пропускная способность ввода-вывода может стать ограничивающим фактором каждая мера, который сокращает число операций ввода-ВЫВОДА может помочь hello toostretch рабочей нагрузки, которая может выполняться в сценарии IaaS, например Azure. Таким образом настоятельно рекомендуется убедиться, что использование сжатия SAP ASE перед отправкой существующих tooAzure базы данных SAP toomake.

Hello рекомендация tooperform сжатия перед отправкой tooAzure, если не реализовано дается по следующим причинам:

* объем Hello tooAzure toobe отправки данных меньше
* Предположим, что можно использовать более мощное оборудование с дополнительные процессоры или более высокой пропускной способности ввода-вывода или меньше операций ввода-вывода задержки в локальной короче Hello продолжительность выполнения сжатия hello
* Меньшего размера базы данных может привести затрат сборки для выделения места на диске

Сжатие данных и LOB работает на виртуальных машинах Azure так же, как и в локальной среде. Дополнительные сведения о как toocheck Если сжатие уже используется существующей базы данных SAP ASE, проверьте Примечание SAP [1750510].

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>С помощью DBACockpit toomonitor базы данных экземпляров
Для систем SAP, в которых используются SAP ASE платформы баз данных, hello DBACockpit доступен как windows embedded браузера в транзакции DBACockpit или Webdynpro. Однако hello полным набором функций для наблюдения и администрирования hello база данных доступна в реализации Webdynpro hello hello DBACockpit только.

Как с локальной системы, несколько шагов требуется tooenable все функциональные возможности SAP NetWeaver, используется реализация Webdynpro hello hello DBACockpit. Выполните Примечание SAP [1245200] tooenable hello использование webdynpros и создавать hello необходимые объекты. При инструкциям hello hello выше заметки, можно также настроить hello Internet Communication Manager (icm) вместе с toobe hello порты, используемые для подключений http и https. по умолчанию Hello для протокола http, выглядит следующим образом:

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
> 
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
> 
> 

и hello ссылки, созданные в транзакции DBACockpit будет выглядеть аналогично toothis:

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

В зависимости от наличие и способ размещения hello hello виртуальной машине Azure система SAP подключен через сайт сайт, несколькими сайтами или ExpressRoute (развертывание между организациями), необходимо убедиться, что toomake, ICM использует полное имя узла, которые могут быть разрешены на hello компьютер, где вы пытаетесь tooopen hello DBACockpit из. См. Примечание SAP [773830] toounderstand как определяет ICM hello полное доменное имя узла в зависимости от параметров профилей и набор параметров icm/host_name_full явным образом при необходимости.

Если вы развернули hello виртуальной Машины в сценарии только для облака без подключения между организациями в локальной среде и Azure, нужны toodefine общедоступный IP-адрес и domainlabel. Формат Hello hello открытому DNS-имени hello виртуальной Машины выглядит следующим образом:

> `<custom domainlabel`>.`<azure region`>.cloudapp.azure.com
> 
> 

Дополнительные сведения, связанные с DNS-имя toohello можно найти [здесь][virtual-machines-azurerm-versus-azuresm].

Значение параметра hello SAP профиля параметр icm/host_name_full toohello, DNS-имя ссылки hello hello виртуальной Машины Azure может выглядеть:

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

В этом случае необходимо toomake убедитесь, что:

* Добавить правила для входящих подключений toohello сетевой группы безопасности в портал Azure для hello TCP/IP toocommunicate порты, используемые с ICM hello
* Добавление конфигурации брандмауэра Windows toohello правила для входящих подключений для hello toocommunicate порты, используемые TCP/IP с hello ICM

Для автоматических импортированных доступны все изменения, рекомендуется tooperiodically применить hello исправления коллекции Примечание SAP применимо tooyour SAP версии:

* [1558958;]
* [1619967;]
* [1882376.]

Дополнительные сведения о панели администратор базы данных для SAP ASE можно найти в следующих примечаниях SAP hello:

* [1605680;]
* [1757924;]
* [1757928]
* [1758182]
* [1758496;]    
* [1814258;]
* [1922555;]
* [1956005.]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Рекомендации по резервному копированию и восстановлению для SAP ASE
При развертывании SAP ASE в Azure методику резервного копирования необходимо пересмотреть. Даже если система hello не продуктивной системы, hello SAP размещаемую SAP ASE должен резервную копию базы данных периодически. Так как служба хранилища Azure сохраняет три образа, резервное копирование становится менее важным с учетом toocompensating сбоя хранилища. Hello основная причина для обеспечения правильной план резервного копирования и восстановления не ограничивается компенсации логических или пользовательских ошибок, предоставляя моменту времени возможности восстановления. Поэтому цель hello tooeither использовать резервные копии toorestore hello базу данных обратно tooa определенных момент времени или toouse hello резервных копий в Azure tooseed другой системы путем копирования существующей базы данных hello. Например, можно перейти от уровня 2 SAP конфигурации tooa трехуровневые системы настройки hello же системы путем восстановления резервной копии.

Резервное копирование и восстановление базы данных в Azure работает hello таким же способом, как и в локальной среде. Ознакомьтесь с примечаниями к SAP:

* [1588316]
* [1585981.]

В них вы найдете дополнительные сведения о создании конфигураций дампов и планировании резервного копирования. В зависимости от ваших потребностей, которые можно настроить и стратегии базы данных и журнала файлов дампа toodisk на одну из существующих дисков hello или добавить дополнительный диск для резервного копирования hello. Это tooreduce hello опасность потери данных в случае возникновения ошибки, рекомендуется toouse диск, где находится устройство не базы данных.

Помимо сжатия данных и больших объектов система SAP ASE также предлагает сжатие резервных копий. Сбрасывает toooccupy меньше пространства с hello базы данных и журнала, его рекомендуется использовать сжатие резервных копий toouse. Дополнительные сведения см. в примечании SAP [1588316]. Сжатие резервной копии hello также является ключевым tooreduce hello объем toobe данных, передаваемых при планировании резервного копирования toodownload или VHD, содержащих резервного копирования создает дамп hello tooon виртуальной машине Azure в локальной.

Не используйте диск D:\ в качестве назначения дампа базы данных или журнала.

#### <a name="performance-considerations-for-backupsrestores"></a>Рекомендации по ускорению резервного копирования и восстановления
Как в исходных развертываниях производительности резервного копирования и восстановления зависит от того, сколько томов может читаться параллельно и могут быть какие hello пропускной способности этих томов. Кроме того hello потребление ресурсов ЦП при сжатии резервной копии может играют важную роль на виртуальных машинах с просто копирование tooeight потоков ЦП. Исходя из сказанного выше, можно сделать следующие выводы.

* Hello меньшее количество hello toostore дисков, используемых Здравствуйте базы данных устройства, hello меньшего размера hello общую пропускную способность при чтении
* Здравствуйте, меньшим числом потоков ЦП в ВМ hello hello, hello более серьезное влияние hello сжатие резервных копий
* Здравствуйте, меньшее число целевых объектов (Stripe каталоги, диски) toowrite hello резервного копирования, hello меньшей пропускной способности hello

число целевых объектов toowrite toothere hello tooincrease являются двух параметров, которые можно использовать или объединить в зависимости от потребностей:

* Чередование hello целевой диск резервного копирования тома на несколько дисков, подключенных в порядок пропускная способность операций ввода-ВЫВОДА tooimprove hello в этом чередующемся томе
* Создание дампа конфигурации на уровне SAP ASE, который использует более одного целевого каталога toowrite hello дампа

Сведения о распределении тома между несколькими дисками см. выше в этом руководстве. Дополнительные сведения об использовании нескольких каталогов в конфигурацию дампа SAP ASE hello см. в документации toohello на sp_config_dump хранимую процедуру, которая является конфигурацией дампа hello используется toocreate на hello [справочный центр Sybase](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Аварийное восстановление с помощью виртуальных машин Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Репликация данных с помощью сервера репликации SAP Sybase
С hello SAP Sybase сервера репликации SAP ASE здесь горячего резервный решения tootransfer базы данных транзакций tooa отдаленных асинхронно. 

Hello установки и функционирования SRS работает также функционально виртуальных Машин, размещенных в службах виртуальных машин Azure, как и в локальной среде.

Поддержка функций HADR ASE через сервер репликации SAP запланирована в будущем выпуске. Это решение будет протестировано и выпущено для платформ Microsoft Azure, как только оно станет доступно.

## <a name="specifics-toosap-ase-on-linux"></a>Особенности tooSAP ASE в Linux
Начиная с Microsoft Azure, можно легко перенести вашей существующей tooAzure приложений SAP ASE виртуальных машин. SAP ASE на виртуальной машине позволяет вам tooreduce hello совокупную стоимость владения развертывания, управления и обслуживания приложений уровня организации, перенеся эти приложения tooMicrosoft Azure. С SAP ASE на виртуальной машине Azure Администраторы и разработчики могут по-прежнему использовать hello тех же средств разработки и администрирования, которые доступны в локальной среде.

Для развертывания виртуальных машин Azure важно tooknow hello официальный соглашений об уровне обслуживания, которые можно найти здесь: <https://azure.microsoft.com/support/legal/sla>

Сведения о размерах SAP и перечень сертифицированных SAP SKU виртуальных машин предоставлены в примечании к SAP [1928533]. Дополнительные документы о размерах SAP для виртуальных машин Azure можно найти здесь <http://blogs.msdn.com/b/saponsqlserver/archive/2015/06/19/how-to-size-sap-systems-running-on-azure-vms.aspx> и здесь <http://blogs.msdn.com/b/saponsqlserver/archive/2015/12/01/new-white-paper-on-sizing-sap-solutions-on-azure-public-cloud.aspx>.

Инструкции и рекомендации, приведенные в учета toohello использования хранилища Azure, развертывания ВМ SAP или мониторинга SAP применяются toodeployments из SAP ASE вместе с приложениями SAP, как указано на протяжении hello первые четыре главах этого документа.

Hello следующие два примечания по SAP включают общие сведения о ASE на ASE и Linux в облаке hello.

* [2134316]
* [1941500]

### <a name="sap-ase-version-support"></a>Поддержка версий SAP ASE
SAP в настоящее время поддерживает версию SAP ASE 16.0 для использования с продуктами SAP Business Suite. Все обновления для сервера SAP ASE или toobe драйверы JDBC и ODBC с SAP Business Suite продукты предоставляются только через hello услугами SAP на: <https://support.sap.com/swdc>.

Как и для установки локально не загружать обновления для сервера SAP ASE hello, или hello JDBC и драйверы ODBC непосредственно из Sybase веб-сайтов. Подробные сведения об исправлениях, которые поддерживаются для использования с SAP Business Suite продуктов локально и в виртуальных машинах Azure см. следующие примечания по SAP hello:

* [1590719]
* [1973241]

Общие сведения о запуске SAP Business Suite в SAP ASE можно найти в hello [SCN](https://www.sap.com/community/topic/ase.html)

### <a name="sap-ase-configuration-guidelines-for-sap-related-sap-ase-installations-in-azure-vms"></a>Рекомендации по конфигурации SAP ASE для связанных с SAP установок SAP ASE на виртуальных машинах Azure
#### <a name="structure-of-hello-sap-ase-deployment"></a>Структура hello развертывания SAP ASE
В соответствии с hello общее описание исполняемые файлы SAP ASE следует найти или в hello корневой файловой системы hello виртуальной Машины (/sybase) установлен. Как правило большинство hello SAP ASE инструменты из системы и баз данных, являются не действительно жесткое оптимизированный за счет использования рабочей нагрузкой SAP NetWeaver. Поэтому hello системы и средств баз данных (master, model, saptools, sybmgmtdb и sybsystemdb) может оставаться на hello корневой файловой системы также. 

Исключением может быть hello временной базы данных, содержащая все рабочие таблицы и временные таблицы, созданные приложением SAP ASE, который в случае некоторых SAP ERP и любых рабочих нагрузок BW может потребоваться больше данных или операций ввода-вывода, тома, который не может поместиться в исходной hello Диск операционной системы Виртуальной машины.

В зависимости от hello версия SAPInst/SWPM используется система tooinstall hello, hello база данных может содержать:

* Отдельную базу tempdb SAP ASE, которая создается при установке SAP ASE.
* SAP ASE tempdb, созданные при установке SAP ASE и дополнительных saptempdb, созданные приветствия программы установки в SAP
* SAP ASE tempdb, созданные при установке SAP ASE и дополнительные базы данных tempdb, который был создан вручную (например следующее примечание SAP [1752266]) требования к определенной базе данных tempdb ERP/BW toomeet

В случае определенных ERP или всех рабочих нагрузок BW имеет смысл, в tooperformance учета устройств tempdb hello tookeep hello дополнительно создать базы данных tempdb (SWPM или вручную) в отдельном файле системе, которая может быть представлена одного Azure диска с данными или Linux RAID Объединение нескольких дисков данных Azure. Если нет дополнительных tempdb, рекомендуется toocreate одно (Примечание SAP [1752266]).

Для таких систем hello следует выполнить следующие действия для hello дополнительно создать tempdb:

* Переместить hello первой базы данных tempdb каталог toohello первый файловой системы базы данных SAP hello
* Добавление базы данных tempdb каталоги tooeach дисков hello, содержащий filesystem базы данных SAP hello

Это tooeither tempdb конфигурации позволяет использовать больше места, чем hello системный диск — может tooprovide. Как ссылку можно проверить размеры directory hello tempdb в существующих системах, которые выполняются локально. Или такой конфигурации позволит секунду в tempdb, который не может быть предоставлен hello системного диска. Снова системах, работающих в локальной среде может быть рабочей нагрузки используется toomonitor ввода-вывода для базы данных tempdb.

Никогда не помещайте все каталоги SAP ASE на/mnt или/mnt/Resource из hello виртуальной Машины. Это также применимо toohello tempdb, даже если hello объекты хранятся в базе данных tempdb hello только являются временными, так как/mnt или/mnt/Resource пробела временной виртуальной Машине Azure по умолчанию, который не является постоянным. Дополнительные сведения о hello пространства временной виртуальной Машине Azure можно найти в [в данной статье][virtual-machines-linux-how-to-attach-disk]

#### <a name="impact-of-database-compression"></a>Влияние сжатия базы данных
В конфигурациях, где пропускная способность ввода-вывода может стать ограничивающим фактором каждая мера, который сокращает число операций ввода-ВЫВОДА может помочь hello toostretch рабочей нагрузки, которая может выполняться в сценарии IaaS, например Azure. Таким образом настоятельно рекомендуется убедиться, что использование сжатия SAP ASE перед отправкой существующих tooAzure базы данных SAP toomake.

Hello рекомендация tooperform сжатия перед отправкой tooAzure, если не реализовано дается по следующим причинам:

* объем Hello tooAzure toobe отправки данных меньше
* Предположим, что можно использовать более мощное оборудование с дополнительные процессоры или более высокой пропускной способности ввода-вывода или меньше операций ввода-вывода задержки в локальной короче Hello продолжительность выполнения сжатия hello
* Меньшего размера базы данных может привести затрат сборки для выделения места на диске

Сжатие данных и LOB работает на виртуальных машинах Azure так же, как и в локальной среде. Дополнительные сведения о как toocheck Если сжатие уже используется существующей базы данных SAP ASE, проверьте Примечание SAP [1750510]. Дополнительные сведения о сжатии баз данных см. в примечании к SAP [2121797].

#### <a name="using-dbacockpit-toomonitor-database-instances"></a>С помощью DBACockpit toomonitor базы данных экземпляров
Для систем SAP, в которых используются SAP ASE платформы баз данных, hello DBACockpit доступен как windows embedded браузера в транзакции DBACockpit или Webdynpro. Однако hello полным набором функций для наблюдения и администрирования hello база данных доступна в реализации Webdynpro hello hello DBACockpit только.

Как с локальной системы, несколько шагов требуется tooenable все функциональные возможности SAP NetWeaver, используется реализация Webdynpro hello hello DBACockpit. Выполните Примечание SAP [1245200] tooenable hello использование webdynpros и создавать hello необходимые объекты. При инструкциям hello hello выше заметки, можно также настроить hello Internet Communication Manager (icm) вместе с toobe hello порты, используемые для подключений http и https. по умолчанию Hello для протокола http, выглядит следующим образом:

> icm/server_port_0 = PROT=HTTP,PORT=8000,PROCTIMEOUT=600,TIMEOUT=600
> 
> icm/server_port_1 = PROT=HTTPS,PORT=443$$,PROCTIMEOUT=600,TIMEOUT=600
> 
> 

и hello ссылки, созданные в транзакции DBACockpit будет выглядеть аналогично toothis:

> https://`<fullyqualifiedhostname`>:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://`<fullyqualifiedhostname`>:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

В зависимости от наличие и способ размещения hello hello виртуальной машине Azure система SAP подключен через сайт сайт, несколькими сайтами или ExpressRoute (развертывание между организациями), необходимо убедиться, что toomake, ICM использует полное имя узла, которые могут быть разрешены на hello компьютер, где вы пытаетесь tooopen hello DBACockpit из. См. Примечание SAP [773830] toounderstand как определяет ICM hello полное доменное имя узла в зависимости от параметров профилей и набор параметров icm/host_name_full явным образом при необходимости.

Если вы развернули hello виртуальной Машины в сценарии только для облака без подключения между организациями в локальной среде и Azure, нужны toodefine общедоступный IP-адрес и domainlabel. Формат Hello hello открытому DNS-имени hello виртуальной Машины выглядит следующим образом:

> `<custom domainlabel`>.`<azure region`>.cloudapp.azure.com
> 
> 

Дополнительные сведения, связанные с DNS-имя toohello можно найти [здесь][virtual-machines-azurerm-versus-azuresm].

Значение параметра hello SAP профиля параметр icm/host_name_full toohello, DNS-имя ссылки hello hello виртуальной Машины Azure может выглядеть:

> https://mydomainlabel.westeurope.cloudapp.net:44300/sap/bc/webdynpro/sap/dba_cockpit
> 
> http://mydomainlabel.westeurope.cloudapp.net:8000/sap/bc/webdynpro/sap/dba_cockpit
> 
> 

В этом случае необходимо toomake убедитесь, что:

* Добавить правила для входящих подключений toohello сетевой группы безопасности в портал Azure для hello TCP/IP toocommunicate порты, используемые с ICM hello
* Добавление конфигурации брандмауэра Windows toohello правила для входящих подключений для hello toocommunicate порты, используемые TCP/IP с hello ICM

Для автоматических импортированных доступны все изменения, рекомендуется tooperiodically применить hello исправления коллекции Примечание SAP применимо tooyour SAP версии:

* [1558958;]
* [1619967;]
* [1882376.]

Дополнительные сведения о панели администратор базы данных для SAP ASE можно найти в следующих примечаниях SAP hello:

* [1605680;]
* [1757924;]
* [1757928]
* [1758182]
* [1758496;]    
* [1814258;]
* [1922555;]
* [1956005.]

#### <a name="backuprecovery-considerations-for-sap-ase"></a>Рекомендации по резервному копированию и восстановлению для SAP ASE
При развертывании SAP ASE в Azure методику резервного копирования необходимо пересмотреть. Даже если система hello не продуктивной системы, hello SAP размещаемую SAP ASE должен резервную копию базы данных периодически. Так как служба хранилища Azure сохраняет три образа, резервное копирование становится менее важным с учетом toocompensating сбоя хранилища. Hello основная причина для обеспечения правильной план резервного копирования и восстановления не ограничивается компенсации логических или пользовательских ошибок, предоставляя моменту времени возможности восстановления. Поэтому цель hello tooeither использовать резервные копии toorestore hello базу данных обратно tooa определенных момент времени или toouse hello резервных копий в Azure tooseed другой системы путем копирования существующей базы данных hello. Например, можно перейти от уровня 2 SAP конфигурации tooa трехуровневые системы настройки hello же системы путем восстановления резервной копии.

Резервное копирование и восстановление базы данных в Azure работает hello таким же способом, как и в локальной среде. Ознакомьтесь с примечаниями к SAP:

* [1588316]
* [1585981.]

В них вы найдете дополнительные сведения о создании конфигураций дампов и планировании резервного копирования. В зависимости от ваших потребностей, которые можно настроить и стратегии базы данных и журнала файлов дампа toodisk на одну из существующих дисков hello или добавить дополнительный диск для резервного копирования hello. tooreduce hello опасность потери данных в случае возникновения ошибки, это рекомендуемое toouse диска, где находится каталог или файл базы данных.

Помимо сжатия данных и больших объектов система SAP ASE также предлагает сжатие резервных копий. Сбрасывает toooccupy меньше пространства с hello базы данных и журнала, его рекомендуется использовать сжатие резервных копий toouse. Дополнительные сведения см. в примечании SAP [1588316]. Сжатие резервной копии hello также является ключевым tooreduce hello объем toobe данных, передаваемых при планировании резервного копирования toodownload или VHD, содержащих резервного копирования создает дамп hello tooon виртуальной машине Azure в локальной.

Не используйте/mnt временного места на виртуальной Машине Azure hello или/mnt/Resource в качестве назначения дампа базы данных или журнала.

#### <a name="performance-considerations-for-backupsrestores"></a>Рекомендации по ускорению резервного копирования и восстановления
Как в исходных развертываниях производительности резервного копирования и восстановления зависит от того, сколько томов может читаться параллельно и могут быть какие hello пропускной способности этих томов. Кроме того hello потребление ресурсов ЦП при сжатии резервной копии может играют важную роль на виртуальных машинах с просто копирование tooeight потоков ЦП. Исходя из сказанного выше, можно сделать следующие выводы.

* Hello меньшее количество hello toostore дисков, используемых Здравствуйте базы данных устройства, hello меньшего размера hello общую пропускную способность при чтении
* Здравствуйте, меньшим числом потоков ЦП в ВМ hello hello, hello более серьезное влияние hello сжатие резервных копий
* Hello меньшее число целевых объектов (программного обеспечения Linux RAID, диски) toowrite Здравствуйте резервного копирования для, hello меньшей пропускной способности hello

число целевых объектов toowrite toothere hello tooincrease являются двух параметров, которые можно использовать или объединить в зависимости от потребностей:

* Чередование hello целевой диск резервного копирования тома на несколько дисков, подключенных в порядок пропускная способность операций ввода-ВЫВОДА tooimprove hello в этом чередующемся томе
* Создание дампа конфигурации на уровне SAP ASE, который использует более одного целевого каталога toowrite hello дампа

Сведения о распределении тома между несколькими дисками см. выше в этом руководстве. Дополнительные сведения об использовании нескольких каталогов в конфигурацию дампа SAP ASE hello см. в документации toohello на sp_config_dump хранимую процедуру, которая является конфигурацией дампа hello используется toocreate на hello [справочный центр Sybase](http://infocenter.sybase.com/help/index.jsp).

### <a name="disaster-recovery-with-azure-vms"></a>Аварийное восстановление с помощью виртуальных машин Azure
#### <a name="data-replication-with-sap-sybase-replication-server"></a>Репликация данных с помощью сервера репликации SAP Sybase
С hello SAP Sybase сервера репликации SAP ASE здесь горячего резервный решения tootransfer базы данных транзакций tooa отдаленных асинхронно. 

Hello установки и функционирования SRS работает также функционально виртуальных Машин, размещенных в службах виртуальных машин Azure, как и в локальной среде.

Сейчас работа ASE HADR через сервер репликации SAP не поддерживается. Он может тестирование и выпуска для платформ Microsoft Azure в будущем hello.

## <a name="specifics-toooracle-database-on-windows"></a>Особенности tooOracle базы данных в Windows
Программное обеспечение Oracle поддерживает Oracle toorun на Microsoft Windows Hyper-V и Azure. Сведения о поддержке общие hello Windows Hyper-V и Azure, проверьте: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces> 

Следующие общие поддержки hello также поддерживается hello конкретного сценария приложений SAP, используя баз данных Oracle. Сведения были указаны в этой части документа hello.

### <a name="oracle-version-support"></a>Поддерживаемые версии Oracle
Cведения о версиях Oracle и соответствующих версиях ОС, которые поддерживаются для работы SAP в Oracle на виртуальных машинах Azure, см. в примечании к SAP [2039619].

Общие сведения о работе SAP Business Suite в Oracle см. на сайте 1DX: <https://www.sap.com/community/topic/oracle.html>.

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Рекомендации по конфигурации Oracle для установки SAP на виртуальные машины Azure
#### <a name="storage-configuration"></a>Конфигурация хранилища
Поддерживается только один экземпляр Oracle, использующий диски, отформатированные в NTFS. Все файлы базы данных должны храниться на файловой системы NTFS, на основе виртуальных жестких дисков или дисков, управляемых hello. Эти диски toohello подключенных виртуальных Машин Azure и основаны на хранилища больших двоичных ОБЪЕКТОВ страницы (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) или дисков, управляемых (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). Любые сетевые диски и удаленные общие ресурсы, включая файловые службы Azure

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx> 
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

**невозможно** использовать для хранения файлов базы данных Oracle!

С помощью дисков, на основе хранилища больших двоичных ОБЪЕКТОВ страницы или управляемых дисков, hello инструкций, созданных в этом документе в главе [кэширование для ВМ и дисков данных] [ dbms-guide-2.1] и [хранилища Microsoft Azure] [ dbms-guide-2.3] применить toodeployments с hello базы данных Oracle.

Как описано ранее в hello общие часть документа hello, существуют квоты на пропускную способность операций ввода-ВЫВОДА для дисков Azure. Hello точное квоты в зависимости от типа ВМ hello используются. Список типов виртуальных машин с соответствующими квотами приведен [здесь (Linux)][virtual-machines-sizes-linux] и [здесь (Windows)][virtual-machines-sizes-windows].

tooidentify hello поддерживаемые типы ВМ Azure см. Примечание tooSAP [1928533].

До тех пор, пока hello Текущая квота операций ввода-ВЫВОДА на диске отвечает требованиям hello, это возможно toostore все hello файлов базы данных на один одного подключенного диска. 

Если требуются дополнительные операции ввода-ВЫВОДА, настоятельно рекомендуется пулы носителей toouse окна (только в Windows Server 2012 и более поздних версий) или чередование дисков для Windows 2008 R2 toocreate один большой логического устройства на нескольких подключенных дисков Windows (см. также раздел [По RAID] [ dbms-guide-2.2] этого документа). Этот подход упрощает места на диске hello накладные toomanage hello администрирования и позволяет избежать трудозатрат hello toomanually распределить файлы по нескольким подключенные диски.

#### <a name="backup--restore"></a>Резервное копирование и восстановление
Для резервного копирования / восстановления функциональности, hello SAP BR * средства для Oracle поддерживаются в hello таким же, каким образом в стандартной операционной системе Windows Server и Hyper-V. Диспетчер восстановления Oracle (RMAN) также поддерживается для toodisk резервных копий и восстановление с диска.

#### <a name="high-availability"></a>Высокая доступность
Для обеспечения высокой доступности и аварийного восстановления можно использовать Oracle Data Guard. Дополнительные сведения см. в [этой документации][virtual-machines-windows-classic-configure-oracle-data-guard].

#### <a name="other"></a>Другие
Другие общие разделы как группы доступности Azure и SAP отслеживания примените, как описано в hello первых трех главах этого документа для развертывания виртуальных машин с hello базы данных Oracle.

## <a name="specifics-toooracle-database-on-oracle-linux"></a>Особенности tooOracle базы данных в Oracle Linux
Программное обеспечение Oracle поддерживает Oracle toorun на Microsoft Windows Hyper-V и Azure. Сведения о поддержке общие hello Windows Hyper-V и Azure, проверьте: <https://blogs.oracle.com/cloud/entry/oracle_and_microsoft_join_forces> 

Следующие общие поддержки hello также поддерживается hello конкретного сценария приложений SAP, используя баз данных Oracle. Сведения были указаны в этой части документа hello.

### <a name="oracle-version-support"></a>Поддерживаемые версии Oracle
Cведения о версиях Oracle и соответствующих версиях ОС, которые поддерживаются для работы SAP в Oracle на виртуальных машинах Azure, см. в примечании к SAP [2039619].

Общие сведения о работе SAP Business Suite в Oracle см. на сайте 1DX: <https://www.sap.com/community/topic/oracle.html>.

### <a name="oracle-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Рекомендации по конфигурации Oracle для установки SAP на виртуальные машины Azure
#### <a name="storage-configuration"></a>Конфигурация хранилища
Поддерживается только один экземпляр Oracle, использующий диски, отформатированные в EXT3, EXT4 и XFS. Все файлы базы данных должны храниться на виртуальных жестких дисках или Управляемых дисках с этими файловыми системами. Эти диски toohello подключенных виртуальных Машин Azure и основаны на хранилища больших двоичных ОБЪЕКТОВ страницы (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) или дисков, управляемых (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). Любые сетевые диски и удаленные общие ресурсы, включая файловые службы Azure

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx> 
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

**невозможно** использовать для хранения файлов базы данных Oracle!

С помощью дисков, на основе хранилища больших двоичных ОБЪЕКТОВ страницы или управляемых дисков, hello инструкций, созданных в этом документе в главе [кэширование для ВМ и дисков данных] [ dbms-guide-2.1] и [хранилища Microsoft Azure] [ dbms-guide-2.3] применить toodeployments с hello базы данных Oracle.

Как описано ранее в hello общие часть документа hello, существуют квоты на пропускную способность операций ввода-ВЫВОДА для дисков Azure. Hello точное квоты в зависимости от типа ВМ hello используются. Список типов виртуальных машин с соответствующими квотами приведен [здесь (Linux)][virtual-machines-sizes-linux] и [здесь (Windows)][virtual-machines-sizes-windows].

tooidentify hello поддерживаемые типы ВМ Azure см. Примечание tooSAP [1928533]

До тех пор, пока hello Текущая квота операций ввода-ВЫВОДА на диске отвечает требованиям hello, это возможно toostore все hello файлов базы данных на один одного подключенного диска. 

Если требуются дополнительные операции ввода-ВЫВОДА, настоятельно рекомендуется toouse LVM (диспетчер логических томов) или MDADM toocreate один большой логический том на нескольких подключенных дисков. Ознакомьтесь также с разделом [Программный RAID-массив][dbms-guide-2.2] в этом документе. Этот подход упрощает места на диске hello накладные toomanage hello администрирования и позволяет избежать трудозатрат hello toomanually распределить файлы по нескольким подключенные диски.

#### <a name="backup--restore"></a>Резервное копирование и восстановление
Для резервного копирования / восстановления функциональности, hello SAP BR * средства для Oracle поддерживаются в hello таким же образом как для восстановления исходного состояния системы и Hyper-V. Диспетчер восстановления Oracle (RMAN) также поддерживается для toodisk резервных копий и восстановление с диска.

#### <a name="high-availability"></a>Высокая доступность
Для обеспечения высокой доступности и аварийного восстановления можно использовать Oracle Data Guard. Дополнительные сведения см. в [этой документации][virtual-machines-windows-classic-configure-oracle-data-guard].

#### <a name="other"></a>Другие
Другие общие разделы как группы доступности Azure и SAP отслеживания примените, как описано в hello первых трех главах этого документа для развертывания виртуальных машин с hello базы данных Oracle.

## <a name="specifics-for-hello-sap-maxdb-database-on-windows"></a>Подробные сведения для базы данных SAP MaxDB в Windows hello
### <a name="sap-maxdb-version-support"></a>Поддерживаемые версии SAP MaxDB
Сейчас с продуктами на основе SAP NetWeaver в Azure можно использовать SAP MaxDB версии 7.9. Все обновления для сервера SAP MaxDB или toobe драйверы JDBC и ODBC при использовании продуктов на основе SAP NetWeaver, предоставляются исключительно через hello услугами SAP в <https://support.sap.com/swdc>.
Общие сведения о выполнении SAP NetWeaver в SAP MaxDB см. здесь: <https://www.sap.com/community/topic/maxdb.html>.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-maxdb-dbms"></a>Поддерживаемые версии Microsoft Windows и типы виртуальных машин Azure для СУБД SAP MaxDB
версия Microsoft Windows hello поддерживается toofind для MaxDB СУБД SAP в Azure, см.:

* [матрица доступности продуктов SAP;][sap-pam]
* примечание к SAP [1928533]

Настоятельно рекомендуется toouse hello последнюю версию hello операционной системы Microsoft Windows, который является Microsoft Windows 2012 R2.

### <a name="available-sap-maxdb-documentation"></a>Доступная документация по SAP MaxDB
Обновить hello перечень SAP MaxDB документации можно найти в следующее примечание SAP hello [767598 ]

### <a name="sap-maxdb-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Рекомендации по конфигурации SAP MaxDB для установки SAP на виртуальные машины Azure
#### <a name="b48cfe3b-48e9-4f5b-a783-1d29155bd573"></a>Конфигурация хранилища
Рекомендации по SAP MaxDB хранилища Azure выполните hello Общие рекомендации, упомянутые в главе [структура развертывания реляционной СУБД][dbms-guide-2].

> [!IMPORTANT]
> Как и в других базах данных, в SAP MaxDB тоже есть файлы данных и файлы журналов, Тем не менее в терминологии SAP MaxDB hello правильный он «том» (не «файл»). Например, в SAP MaxDB существуют тома данных и тома журналов. Не путайте их с томами жестких дисков. 
> 
> 

Вкратце повторим рекомендации.

* При использовании учетных записей хранилища Azure, задайте учетную запись хранилища Azure hello, содержащий hello SAP MaxDB данных и журналов тома (т. е. файлы) слишком**локального избыточном хранилище (LRS)** , как указано в главе [службыхранилищаMicrosoftAzure] [dbms-guide-2.3].
* Путь hello отдельные операции ввода-ВЫВОДА для томов с данными SAP MaxDB (т. е. файлы) из hello пути ввода-ВЫВОДА для тома журналов (т. е. файлы). Это означает, что тома данных SAP MaxDB (т. е. файлы) имеют toobe установлен на один логический диск, и тома журнала SAP MaxDB (т. е. файлы) имеют toobe установлен на другом логическом диске.
* Набор hello соответствующего кэширования типа для каждого диска, в зависимости от ли вы использовать для SAP MaxDB данных или журнала тома (т. е. файлы) и использование стандартного Azure или хранилище Azure класса Premium, как описано в главе [кэширование для ВМ и дисков данных][dbms-guide-2.1].
* До тех пор, пока hello Текущая квота операций ввода-ВЫВОДА на диске отвечает требованиям hello, является возможные toostore hello томов с данными одного подключенного диска и также хранить все тома журнала базы данных на другой одного подключенного диска.
* Если требуются дополнительные операции ввода-ВЫВОДА и (или) пространство, настоятельно рекомендуется пулы носителей Microsoft окна toouse (только в Microsoft Windows Server 2012 и более поздних версий) или Microsoft Windows чередование дисков для Microsoft Windows 2008 R2 toocreate один большой логического устройства через несколько подключенные диски. Ознакомьтесь также с разделом [Программный RAID-массив][dbms-guide-2.2] в этом документе. Этот подход упрощает места на диске hello накладные toomanage hello администрирования и позволяет избежать трудозатрат hello вручную распределение файлов на нескольких дисках, подключенных.
* Для hello высоким требованиям операций ввода-ВЫВОДА можно использовать хранилище Azure класса Premium, который доступен в серии DS и виртуальные машины серии GS.

![Эталонная конфигурация виртуальной машины Azure IaaS для СУБД SAP MaxDB][dbms-guide-figure-600]

#### <a name="23c78d3b-ca5a-4e72-8a24-645d141a3f5d"></a>Архивация и восстановление
При развертывании SAP MaxDB в Azure методику резервного копирования необходимо пересмотреть. Даже если система hello не продуктивной системы, hello SAP размещаемую SAP MaxDB необходимо резервную копию базы данных периодически. Так как в службе хранилища Azure хранятся три образа, резервное копирование представляется менее важным в контексте защиты системы от сбоев хранилища и более важных эксплуатационных и административных сбоев. Hello основная причина для обеспечения правильной резервной копии и плана восстановления —, чтобы компенсировать логического или вручную ошибок, предоставляя возможности восстановления на момент. Поэтому цель hello tooeither использования резервных копий toorestore hello базы данных tooa определенных точек времени или toouse hello резервных копий в Azure tooseed другой системы путем копирования существующей базы данных hello. Например, можно перейти от уровня 2 SAP конфигурации tooa трехуровневые системы настройки hello же системы путем восстановления резервной копии.

Резервное копирование и восстановление базы данных в hello Azure работает так же, как и для локальных систем, поэтому можно использовать стандартные MaxDB SAP резервного копирования и восстановления средств, которые описаны в одном документов документации SAP MaxDB hello перечисленные в примечании SAP [767598 ]. 

#### <a name="77cd2fbb-307e-4cbf-a65f-745553f72d2c"></a>Рекомендации по ускорению архивации и восстановления
Как в исходных развертываниях производительность резервного копирования и восстановления зависит от того, сколько томов может читаться параллельно и hello пропускной способности этих томов. Кроме того hello потребление ресурсов ЦП при сжатии резервной копии можно играют важную роль на виртуальных машинах с вверх tooeight потоков ЦП. Исходя из сказанного выше, можно сделать следующие выводы.

* Здравствуйте, меньше hello количество дисков, используемых toostore hello базы данных устройства, hello нижней hello общая пропускная способность операций чтения
* Здравствуйте, меньшим числом потоков ЦП в ВМ hello hello, hello более серьезное влияние hello сжатие резервных копий
* Здравствуйте, меньшее число целевых объектов (Stripe каталоги, диски) toowrite hello резервного копирования, hello нижней Здравствуй, пропускная способность

tooincrease hello число обращается toowrite для, можно двумя способами, которые можно использовать, возможно, в сочетании, в зависимости от потребностей:

* Выделить для резервных копий отдельные тома.
* Чередование hello конечный том архивации через несколько подключенных дисков в порядке пропускная способность операций ввода-ВЫВОДА tooimprove hello на этом томе чередующегося диска
* Выделить отдельные логические диски для:
  * томов (т. е. файлов) резервных копий SAP MaxDB;
  * томов (т. е. файлов) данных SAP MaxDB;
  * томов (т. е. файлов) журналов SAP MaxDB.

Сведения о распределении тома между несколькими дисками см. в разделе [Программный RAID-массив][dbms-guide-2.2] этого документа. 

#### <a name="f77c1436-9ad8-44fb-a331-8671342de818"></a>Другое
Все другие основные разделы, таких как мониторинг группы доступности Azure или SAP применимы, как описано в hello первых трех главах этого документа для развертывания виртуальных машин с базой данных SAP MaxDB hello.
Другие параметры, относящиеся MaxDB SAP — это прозрачное tooAzure виртуальные машины и описаны в различных документах, перечисленные в примечании SAP [767598 ] и в этих примечаниях SAP:

* [826037;] 
* [1139904;]
* [1173395.]

## <a name="specifics-for-sap-livecache-on-windows"></a>Особенности SAP liveCache в Windows
### <a name="sap-livecache-version-support"></a>Поддерживаемые версии SAP liveCache
Минимальной поддерживаемой версией SAP liveCache в службе виртуальных машин Azure является **SAP LC/LCAPPS 10.0 SP 25** (включая **liveCache 7.9.08.31** и **LCA-Build 25**), выпущенная для **EhP 2 для SAP SCM 7.0** и более поздних версий.

### <a name="supported-microsoft-windows-versions-and-azure-vm-types-for-sap-livecache-dbms"></a>Поддерживаемые версии Microsoft Windows и типы виртуальных машин Azure для СУБД SAP liveCache
версия Microsoft Windows hello поддерживается toofind для liveCache SAP в Azure, см.:

* [матрица доступности продуктов SAP;][sap-pam]
* примечание к SAP [1928533]

Настоятельно рекомендуется toouse hello последнюю версию hello операционной системы Microsoft Windows Server. 

### <a name="sap-livecache-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Рекомендации по конфигурации SAP liveCache для установки SAP на виртуальные машины Azure
#### <a name="recommended-azure-vm-types"></a>Рекомендуемые типы виртуальных машин Azure
Как приложение, которое выполняет вычисления, повышая SAP liveCache, сумма hello и быстродействии ОЗУ и ЦП имеет основной влияют на производительность liveCache SAP. 

Для типов ВМ Azure hello, поддерживаемых SAP (Примечание SAP [1928533]), все виртуальные ресурсы ЦП выделенной toohello ВМ, поддерживаемых выделенных ресурсов ЦП hello низкоуровневой оболочки. Из-за отсутствия избыточного выделения ресурсов отсутствует конкуренция за ресурсы ЦП.

Аналогично для всех типов экземпляр виртуальной Машины Azure, поддерживаемых SAP, hello памяти виртуальной Машины — 100% сопоставлен toohello физической памяти — избыток (перерасход), например, не используется.

С этой точки зрения настоятельно рекомендуется toouse hello новой серии D или виртуальной Машине Azure серии DS (в сочетании со службой хранилища Azure Premium) типа, они имеют более быстрые процессоры 60%, чем hello серии A. Для hello наибольший объем ОЗУ и ЦП нагрузки, можно использовать серии G и виртуальные машины серии GS (в сочетании со службой хранилища Azure Premium) с новейших процессоров Intel Xeon® семейства E5 v3, имеющих дважды памяти hello и четыре раза hello твердотельный накопитель хранилище (SSD) hello D hello / Серии DS.

#### <a name="storage-configuration"></a>Конфигурация хранилища
Как SAP liveCache основано на технологии SAP MaxDB, все hello хранилища Azure рекомендации упомянутые для SAP MaxDB в главе [конфигурации хранилища] [ dbms-guide-8.4.1] также допустимы для SAP liveCache. 

#### <a name="dedicated-azure-vm-for-livecache"></a>Выделенная виртуальная машина Azure для liveCache
Как SAP liveCache интенсивно использует вычислительной мощностью, для производственного использования настоятельно рекомендуется toodeploy на выделенной виртуальной машине Azure. 

![Виртуальная машина Azure, выделенная для liveCache, для производственных целей][dbms-guide-figure-700]

#### <a name="backup-and-restore"></a>Архивация и восстановление
Резервное копирование и восстановление, включая вопросы производительности уже описаны в hello подходящие главы SAP MaxDB [резервного копирования и восстановления] [ dbms-guide-8.4.2] и [вопросы производительности для резервного копирования и восстановление][dbms-guide-8.4.3]. 

#### <a name="other"></a>Другие
Все основные разделы уже описаны в hello соответствующие SAP MaxDB [это] [ dbms-guide-8.4.4] главы. 

## <a name="specifics-for-hello-sap-content-server-on-windows"></a>Подробные сведения для hello SAP содержимого сервера в Windows
Hello содержимое сервер SAP находится содержимое toostore отдельную, серверных компонентов, например электронных документов в различных форматах. Hello содержимого сервера SAP предоставляется средой разработки технологии и — между приложениями toobe используется для любого приложения SAP. Он устанавливается на отдельной системе. Стандартное содержимое обучающие материалы и документация из базы знаний хранилища или технической рисунки, исходящие от hello mySAP PLM системы управления документами. 

### <a name="sap-content-server-version-support"></a>Поддерживаемые версии сервера содержимого SAP
В настоящее время SAP поддерживает:

* **сервер содержимого SAP** версии **6.50 (и более поздние)**;
* **SAP MaxDB версии 7.9;**
* **службы Microsoft IIS версии 8.0 (и более поздние версии).**

Настоятельно рекомендуется toouse hello последнюю версию содержимого сервер SAP, который во время hello записи этого документа является **6.50 SP4**и hello новейшую версию **Microsoft IIS 8.5**. 

Проверьте hello последние поддерживаемые версии сервера содержимого SAP и Microsoft IIS в hello [матрицы доступности SAP продукта (PAM)][sap-pam].

### <a name="supported-microsoft-windows-and-azure-vm-types-for-sap-content-server"></a>Поддерживаемые версии Microsoft Windows и типы виртуальных машин Azure для сервера содержимого SAP
toofind поддерживаемой версии Windows для сервера содержимого SAP в Azure, см.:

* [матрица доступности продуктов SAP;][sap-pam]
* примечание к SAP [1928533]

Настоятельно рекомендуется toouse hello последнюю версию Microsoft Windows Server.

### <a name="sap-content-server-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Рекомендации по конфигурации сервера содержимого SAP для установки SAP на виртуальные машины Azure
#### <a name="storage-configuration"></a>Конфигурация хранилища
При настройке сервера SAP содержимого toostore файлов в базе данных SAP MaxDB hello все хранилища Azure лучшие рекомендации рекомендаций, упомянутых для SAP MaxDB в главе [конфигурации хранилища] [ dbms-guide-8.4.1] также допустимо для сценария hello содержимого сервер SAP. 

При настройке сервера SAP содержимого toostore файлы в файловой системе hello это рекомендуется toouse выделенного логического диска. С помощью дисковых пространств Windows можно tooalso увеличьте размер логического диска и пропускную способность операций ввода-ВЫВОДА, как описано в главе [по RAID][dbms-guide-2.2]. 

#### <a name="sap-content-server-location"></a>Расположение сервера содержимого SAP
Сервер содержимого SAP имеет toobe, развернутых в hello же регионе Azure и виртуальной сети Azure, где развертывается hello системы SAP. Все бесплатные toodecide ли вы хотите toodeploy компоненты сервера SAP содержимого в выделенной виртуальной Машине Azure или в hello одной виртуальной Машины, где запущен hello системы SAP. 

![Виртуальная машина Azure, выделенная для сервера содержимого SAP][dbms-guide-figure-800]

#### <a name="sap-cache-server-location"></a>Расположение сервера кэширования SAP
Hello кэша сервера SAP является дополнительный компонент серверных tooprovide доступа too(cached) документы локально. Hello кэша сервера SAP кэширует документы hello содержимого сервера SAP. Это действие toooptimize сетевого трафика, если документы toobe извлекаться несколько раз из различных источников. Общее правило Hello — что hello кэша сервера SAP есть toobe toohello физически закрыть клиент, обращающийся к hello кэша сервера SAP. 

В этом случае существует два варианта.

1. **Клиент — это система SAP серверной** при tooaccess настроенный сервер SAP содержимого серверной части системы SAP этой системы SAP является клиентом. Как система SAP и содержимого сервера SAP, развернутых в hello же регионе Azure — в hello же центре обработки данных Azure — это физически закрыть tooeach других. Таким образом нет нет необходимости toohave выделенный кэш сервер SAP. Hello доступ клиентов (SAP GUI или веб-браузер) пользовательского интерфейса SAP системы SAP напрямую, а hello SAP система получает документы из hello содержимого сервер SAP.
2. **Клиент — браузер локальной** hello сервера SAP содержимого может быть настроенный toobe прямого доступа hello веб-браузера. В этом случае выполнение локального веб-браузера является клиентом hello содержимого сервер SAP. На локальном центре обработки данных и обработки данных Azure, помещаются в разных местах (в идеале закрыть tooeach другие). Локальный центр обработки данных — tooAzure, подключенных через VPN Azure сеть-сеть или подключение ExpressRoute. Несмотря на то, что оба параметра обеспечивают безопасное tooAzure соединение сети VPN, сайт сайт сетевое подключение не предлагает сети полосы пропускания и задержки SLA между hello локального центра обработки данных и hello центра обработки данных Azure. toospeed копирование toodocuments доступа вы выполните одно из следующих hello:
   1. Установка сервера кэша SAP в локальной, закройте toohello локального веб-браузера (параметр [это] [ dbms-guide-900-sap-cache-server-on-premises] рисунок)
   2. настроить канал Azure ExpressRoute, который обеспечивает выделенное высокоскоростное сетевое подключение с низкой задержкой между локальным ЦОД и ЦОД Azure.

![Параметр tooinstall кэша сервера SAP локально][dbms-guide-figure-900]
<a name="642f746c-e4d4-489d-bf63-73e80177a0a8"></a>

#### <a name="backup--restore"></a>Резервное копирование и восстановление
При настройке hello содержимого сервера SAP toostore файлов в базе данных SAP MaxDB hello в главе SAP MaxDB уже описываются вопросы процедуры и производительности резервного копирования и восстановления hello [резервного копирования и восстановления] [ dbms-guide-8.4.2] и главе [факторы производительности при резервном копировании и восстановлении][dbms-guide-8.4.3]. 

Если настроить hello содержимого сервера SAP toostore файлы в файловой системе hello, уже tooexecute вручную резервного копирования и восстановления всей файловой структуры hello находятся документы hello. Это аналогично tooSAP MaxDB резервного копирования и восстановления, рекомендуется toohave выделенный дисковый том для целей резервного копирования. 

#### <a name="other"></a>Другие
Другие параметры конкретного сервера SAP содержимого — это прозрачное tooAzure виртуальные машины и описаны в различных документов и примечания по SAP:

* <https://service.sap.com/contentserver> 
* примечание к SAP [1619726]  

## <a name="specifics-tooibm-db2-for-luw-on-windows"></a>Особенности tooIBM DB2 для LUW в Windows
С помощью Microsoft Azure можно легко перенести в существующее приложение SAP, запущенных на IBM DB2 для Linux, UNIX и Windows (LUW) tooAzure виртуальных машин. С SAP на IBM DB2 для LUW Администраторы и разработчики могут по-прежнему использовать hello же средства разработки и администрирования, которые доступны в локальной среде.
Общие сведения о работе SAP Business Suite в IBM DB2 для LUW можно найти в hello сети сообщества SAP (SCN) в <https://www.sap.com/community/topic/db2-for-linux-unix-and-windows.html>.

Дополнительные сведения и новости о SAP в DB2 для LUW в Azure см. в примечании к SAP [2233094]. 

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>Поддерживаемые версии IBM DB2 для Linux, UNIX и Windows
SAP в IBM DB2 для LUW поддерживается в службах виртуальных машин Microsoft Azure начиная с версии DB2 10.5.

Сведения о поддерживаемых продуктах SAP и типах ВМ Azure см. Примечание tooSAP [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Рекомендации по конфигурации IBM DB2 для Linux, UNIX и Windows для установки SAP на виртуальные машины Azure
#### <a name="storage-configuration"></a>Конфигурация хранилища
Все файлы базы данных должны храниться на основании непосредственно подключенных дисков файловой системы NTFS hello. Эти диски toohello подключенных виртуальных Машин Azure и зависимости в хранилища больших двоичных ОБЪЕКТОВ страницы (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) или дисков, управляемых (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). Любые сетевые диски или удаленные общие ресурсы, такие как hello следующие службы файлов Azure, **не** поддерживается для файлов базы данных: 

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

При использовании дисков, на основе хранилища больших двоичных ОБЪЕКТОВ страницы или дисков, управляемых hello инструкций, созданных в этом документе в главе [структура развертывания реляционной СУБД] [ dbms-guide-2] справедливы toodeployments с hello IBM DB2 для LUW базы данных. 

Как описано ранее в hello общие часть документа hello, существуют квоты на пропускную способность операций ввода-ВЫВОДА для дисков. точное квоты Hello зависят hello ВМ типа используется. Список типов виртуальных машин с соответствующими квотами приведен [здесь (Linux)][virtual-machines-sizes-linux] и [здесь (Windows)][virtual-machines-sizes-windows].

При условии, что hello Текущая квота операций ввода-ВЫВОДА на диске недостаточно, это возможно toostore все hello файлы базы данных на один одного подключенного диска. 

Для повышения производительности вопросы также ссылаться toochapter «данных безопасности и производительности рекомендации для базы данных каталогов» в руководствах по установке SAP.

Кроме того, вы можете использовать пулы носителей Windows (только в Windows Server 2012 и более поздних версий) или чередование Windows для Windows 2008 R2, как описано в главе [по RAID] [ dbms-guide-2.2] этого документа toocreate один большой логического устройства на нескольких дисках.
Для дисков hello, содержащих пути к хранилищу hello DB2 для sapdata и saptmp каталогов необходимо указать размер сектора физического диска 512 КБ. При использовании пулов хранения Windows, необходимо создать hello пулы носителей вручную через интерфейс командной строки с помощью параметра hello»-LogicalSectorSizeDefault». Дополнительные сведения см. здесь: <https://technet.microsoft.com/itpro/powershell/windows/storage/new-storagepool>.

#### <a name="backuprestore"></a>Резервное копирование и восстановление
функциональные возможности резервного копирования и восстановления Hello для IBM DB2 для LUW, поддерживаемых в hello таким же, каким образом в стандартной операционной системе Windows Server и Hyper-V.

У вас обязательно должна быть надежная стратегия резервного копирования базы данных. 

Как исходного развертывания, резервного копирования и восстановления производительность зависит от того, сколько томов может читаться параллельно, и какие hello пропускной способности этих томов могут быть. Кроме того hello потребление ресурсов ЦП при сжатии резервной копии может играют важную роль на виртуальных машинах с просто копирование tooeight потоков ЦП. Исходя из сказанного выше, можно сделать следующие выводы.

* Hello меньшее количество hello toostore дисков, используемых Здравствуйте базы данных устройства, hello меньшего размера hello общую пропускную способность при чтении
* Здравствуйте, меньшим числом потоков ЦП в ВМ hello hello, hello более серьезное влияние hello сжатие резервных копий
* Здравствуйте, меньшее число целевых объектов (Stripe каталоги, диски) toowrite hello резервного копирования, hello нижней Здравствуй, пропускная способность

tooincrease количество hello toowrite целевых объектов для, два параметра может быть, использовать и объединены в зависимости от потребностей:

* Чередование hello целевой диск резервного копирования тома на несколько дисков в порядке пропускная способность операций ввода-ВЫВОДА tooimprove hello в этом чередующемся томе
* Более одного целевого каталога toowrite hello Создание резервной копии

#### <a name="high-availability-and-disaster-recovery"></a>Высокая доступность и аварийное восстановление
Microsoft Cluster Server (MSCS) не поддерживается.

Поддерживается аварийное восстановление высокой доступности (HADR) DB2. Если виртуальные машины hello hello высокого уровня ДОСТУПНОСТИ конфигурации имеют работающее разрешение имен, установки hello в Azure не отличается от настройки, в которой выполняется в локальной среде. Не рекомендуется toorely на только разрешение IP-адресов.

Не используйте Георепликации для учетных записей хранения hello, хранящих диски hello базы данных. Дополнительные сведения см. в разделе toochapter [хранилища Microsoft Azure] [ dbms-guide-2.3] и главе [высокий уровень доступности и аварийного восстановления с виртуальными машинами Azure] [ dbms-guide-3].

#### <a name="other"></a>Другие
Другие общие разделы как группы доступности Azure и SAP отслеживания примените, как описано в hello первых трех главах этого документа для развертывания виртуальных машин с IBM DB2 для LUW также. 

См. также toochapter [общие SQL Server для SAP в Azure Сводка][dbms-guide-5.8].

## <a name="specifics-tooibm-db2-for-luw-on-linux"></a>Особенности tooIBM DB2 для LUW в Linux
С помощью Microsoft Azure можно легко перенести в существующее приложение SAP, запущенных на IBM DB2 для Linux, UNIX и Windows (LUW) tooAzure виртуальных машин. С SAP на IBM DB2 для LUW Администраторы и разработчики могут по-прежнему использовать hello же средства разработки и администрирования, которые доступны в локальной среде. Общие сведения о работе SAP Business Suite в IBM DB2 для LUW можно найти в hello сети сообщества SAP (SCN) в <https://www.sap.com/community/topic/db2-for-linux-unix-and-windows.html>.

Дополнительные сведения и новости о SAP в DB2 для LUW в Azure см. в примечании к SAP [2233094].

### <a name="ibm-db2-for-linux-unix-and-windows-version-support"></a>Поддерживаемые версии IBM DB2 для Linux, UNIX и Windows
SAP в IBM DB2 для LUW поддерживается в службах виртуальных машин Microsoft Azure начиная с версии DB2 10.5.

Сведения о поддерживаемых продуктах SAP и типах ВМ Azure см. Примечание tooSAP [1928533].

### <a name="ibm-db2-for-linux-unix-and-windows-configuration-guidelines-for-sap-installations-in-azure-vms"></a>Рекомендации по конфигурации IBM DB2 для Linux, UNIX и Windows для установки SAP на виртуальные машины Azure
#### <a name="storage-configuration"></a>Конфигурация хранилища
Все файлы базы данных должны храниться на подключенных напрямую дисках с файловой системой. Эти диски toohello подключенных виртуальных Машин Azure и зависимости в хранилища больших двоичных ОБЪЕКТОВ страницы (<https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs>) или дисков, управляемых (<https://docs.microsoft.com/azure/storage/storage-managed-disks-overview>). Любые сетевые диски или удаленные общие ресурсы, такие как hello следующие службы файлов Azure, **не** поддерживается для файлов базы данных:

* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx>
* <https://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx>

При использовании дисков, на основе хранилища больших двоичных ОБЪЕКТОВ Azure страница hello инструкций, созданных в этом документе в главе [структура развертывания реляционной СУБД] [ dbms-guide-2] справедливы toodeployments с hello IBM DB2 для LUW базы данных.

Как описано ранее в hello общие часть документа hello, существуют квоты на пропускную способность операций ввода-ВЫВОДА для дисков. точное квоты Hello зависят hello ВМ типа используется. Список типов виртуальных машин с соответствующими квотами приведен [здесь (Linux)][virtual-machines-sizes-linux] и [здесь (Windows)][virtual-machines-sizes-windows].

При условии, что hello Текущая квота операций ввода-ВЫВОДА на диске недостаточно, это возможно toostore все hello файлы базы данных на один отдельный диск.

Для повышения производительности вопросы также ссылаться toochapter «данных безопасности и производительности рекомендации для базы данных каталогов» в руководствах по установке SAP.

Кроме того, можно использовать LVM (диспетчер логических томов) или MDADM, приведенные в главе [по RAID] [ dbms-guide-2.2] этот документ toocreate один большой логического устройства на нескольких дисках.
Для дисков hello, содержащих пути к хранилищу hello DB2 для sapdata и saptmp каталогов необходимо указать размер сектора физического диска 512 КБ.

#### <a name="backuprestore"></a>Резервное копирование и восстановление
функциональные возможности резервного копирования и восстановления Hello для IBM DB2 для LUW, поддерживаемых в hello таким же способом, как и для стандартных Linux установки локальной.

У вас обязательно должна быть надежная стратегия резервного копирования базы данных.

Как исходного развертывания, резервного копирования и восстановления производительность зависит от того, сколько томов может читаться параллельно, и какие hello пропускной способности этих томов могут быть. Кроме того hello потребление ресурсов ЦП при сжатии резервной копии может играют важную роль на виртуальных машинах с просто копирование tooeight потоков ЦП. Исходя из сказанного выше, можно сделать следующие выводы.

* Hello меньшее количество hello toostore дисков, используемых Здравствуйте базы данных устройства, hello меньшего размера hello общую пропускную способность при чтении
* Здравствуйте, меньшим числом потоков ЦП в ВМ hello hello, hello более серьезное влияние hello сжатие резервных копий
* Здравствуйте, меньшее число целевых объектов (Stripe каталоги, диски) toowrite hello резервного копирования, hello нижней Здравствуй, пропускная способность

tooincrease количество hello toowrite целевых объектов для, два параметра может быть, использовать и объединены в зависимости от потребностей:

* Чередование hello целевой диск резервного копирования тома на несколько дисков в порядке пропускная способность операций ввода-ВЫВОДА tooimprove hello в этом чередующемся томе
* Более одного целевого каталога toowrite hello Создание резервной копии

#### <a name="high-availability-and-disaster-recovery"></a>Высокая доступность и аварийное восстановление
Поддерживается аварийное восстановление высокой доступности (HADR) DB2. Если виртуальные машины hello hello высокого уровня ДОСТУПНОСТИ конфигурации имеют работающее разрешение имен, установки hello в Azure не отличается от настройки, в которой выполняется в локальной среде. Не рекомендуется toorely на только разрешение IP-адресов.

Не используйте Георепликации для учетных записей хранения hello, хранящих диски hello базы данных. Дополнительные сведения см. в разделе toochapter [хранилища Microsoft Azure] [ dbms-guide-2.3] и главе [высокий уровень доступности и аварийного восстановления с виртуальными машинами Azure] [ dbms-guide-3].

#### <a name="other"></a>Другие
Другие общие разделы как группы доступности Azure и SAP отслеживания примените, как описано в hello первых трех главах этого документа для развертывания виртуальных машин с IBM DB2 для LUW также.

См. также toochapter [общие SQL Server для SAP в Azure Сводка][dbms-guide-5.8].

