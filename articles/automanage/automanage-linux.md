---
title: Azure Automanage pour Linux
description: Découvrez les bonnes pratiques Azure Automanage relatives aux machines virtuelles pour les services automatiquement intégrés et configurés sur les machines Linux.
author: deanwe
ms.service: virtual-machines
ms.subservice: automanage
ms.collection: linux
ms.workload: infrastructure
ms.topic: conceptual
ms.date: 02/22/2021
ms.author: deanwe
ms.openlocfilehash: 24b72afb7f685e50ac9452889b404fa8bda29644
ms.sourcegitcommit: 02bc06155692213ef031f049f5dcf4c418e9f509
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/03/2021
ms.locfileid: "106278318"
---
# <a name="azure-automanage-for-virtual-machines-best-practices---linux"></a>Bonnes pratiques Azure Automanage pour les machines virtuelles - Linux

Ces services Azure sont automatiquement intégrés quand vous utilisez Automanage pour les machines virtuelles sur une machine virtuelle Linux. Ils sont essentiels pour notre livre blanc sur les meilleures pratiques, que vous pouvez trouver dans notre [Cloud Adoption Framework](/azure/cloud-adoption-framework/manage/azure-server-management).

Nous allons intégrer et configurer automatiquement tous ces services, superviser leur fonctionnement et apporter les corrections nécessaires en cas de dérive. Pour en savoir plus sur ce processus, consultez [Azure Automanage pour machines virtuelles](automanage-virtual-machines.md).

## <a name="supported-linux-distributions-and-versions"></a>Distributions et versions Linux prises en charge

Automanage prend en charge les distributions et versions Linux suivantes :

- CentOS 7.3+
- RHEL 7.4+
- Ubuntu 16.04 et 18.04
- SLES 12 (SP3-SP5 uniquement)

## <a name="participating-services"></a>Services participant

>[!NOTE]
> Microsoft Antimalware n’est pas pris en charge sur les machines virtuelles Linux pour le moment.

|Service    |Description    |Environnements pris en charge<sup>1</sup>    |Préférences prises en charge<sup>1</sup>    |
|-----------|---------------|----------------------|-------------------------|
|[Surveillance des insights de machine virtuelle](https://docs.microsoft.com/azure/azure-monitor/vm/vminsights-overview)    |Azure Monitor pour machines virtuelles surveille les performances et l’intégrité de vos machines virtuelles, y compris de leurs processus en cours d’exécution et de leurs dépendances vis-à-vis d’autres ressources. En savoir [plus](../azure-monitor/vm/vminsights-overview.md).    |Production    |Non    |
|[Sauvegarde](https://docs.microsoft.com/azure/backup/backup-overview)   |Le service Sauvegarde Azure propose des sauvegardes indépendantes et isolées pour éviter une destruction involontaire des données de vos machines virtuelles. En savoir [plus](../backup/backup-azure-vms-introduction.md). Les frais sont calculés en fonction du nombre et de la taille des machines virtuelles protégées. En savoir [plus](https://azure.microsoft.com/pricing/details/backup/).    |Production    |Oui    |
|[Centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-introduction)    |Azure Security Center est un système de gestion de la sécurité de l’infrastructure unifié qui renforce la posture de sécurité de vos centres de données et fournit une protection avancée contre les menaces pour vos charges de travail hybrides dans le cloud. En savoir [plus](../security-center/security-center-introduction.md).  Automanage configure l’abonnement dans lequel votre machine virtuelle réside en offre de niveau gratuit d’Azure Security Center. Si votre abonnement est déjà intégré avec Azure Security Center, Automanage ne le reconfigure pas.    |Production, Dev/Test    |Non    |
|[Gestion des mises à jour](https://docs.microsoft.com/azure/automation/update-management/overview)    |Vous pouvez utiliser la solution Update Management d’Azure Automation pour gérer les mises à jour du système d’exploitation de vos machines virtuelles. Vous pouvez rapidement évaluer l’état des mises à jour disponibles sur toutes les machines d’agent et gérer le processus d’installation des mises à jour nécessaires pour les serveurs. En savoir [plus](../automation/update-management/overview.md).    |Production, Dev/Test    |Non    |
|[Suivi des modifications et inventaire](https://docs.microsoft.com/azure/automation/change-tracking/overview) |La fonctionnalité Suivi des modifications et inventaire combine les fonctions de suivi des modifications et d’inventaire pour vous permettre d’effectuer le suivi des modifications apportées à l’infrastructure des machines virtuelles et des serveurs. Le service prend en charge le suivi des modifications sur les services, les démons, les logiciels, le registre et les fichiers de votre environnement pour vous aider à diagnostiquer les changements indésirables et à déclencher des alertes. La prise en charge de l’inventaire vous permet d’interroger les ressources intégrées pour voir les applications installées et d’autres éléments de configuration.  En savoir [plus](../automation/change-tracking/overview.md).    |Production, Dev/Test    |Non    |
|[Configuration d’invité Azure](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration)  | La stratégie Guest Configuration est utilisée pour superviser la configuration et signaler la conformité de la machine. Le service Automanage installe la base de référence Azure pour Linux à l’aide de l’extension Guest Configuration. Pour les machines Linux, le service Guest Configuration installe la base de référence en mode d’audit uniquement. Vous pouvez voir à quel niveau votre machine virtuelle n’est pas conforme à la base de référence. Toutefois, la non-conformité n’est pas automatiquement corrigée. En savoir [plus](../governance/policy/concepts/guest-configuration.md).    |Production, Dev/Test    |Non    |
|[Diagnostics de démarrage](https://docs.microsoft.com/azure/virtual-machines/boot-diagnostics)  | Les diagnostics de démarrage sont une fonctionnalité de débogage pour les machines virtuelles Azure qui permet de diagnostiquer les échecs de démarrage de machine virtuelle. Les diagnostics de démarrage permettent à un utilisateur d’observer l’état de la machine virtuelle lors de son démarrage en collectant des informations de journal série et des captures d’écran. |Production, Dev/Test    |Non    |
|[Compte Azure Automation](https://docs.microsoft.com/azure/automation/automation-create-standalone-account)    |Azure Automation prend en charge la gestion tout au long du cycle de vie de votre infrastructure et des applications. En savoir [plus](../automation/automation-intro.md).    |Production, Dev/Test    |Non    |
|[Espace de travail Log Analytics](https://docs.microsoft.com/azure/azure-monitor/logs/log-analytics-overview) |Azure Monitor stocke des données de journal dans un espace de travail Log Analytics, qui est une ressource Azure et un conteneur où les données sont collectées, agrégées, et qui sert de limite d’administration. En savoir [plus](../azure-monitor/logs/design-logs-deployment.md).    |Production, Dev/Test    |Non    |


<sup>1</sup> La sélection de l’environnement est disponible quand vous activez Automanage. En savoir [plus](automanage-virtual-machines.md#environment-configuration). Vous pouvez également modifier les paramètres par défaut de l’environnement, et définir vos propres préférences dans le respect des bonnes pratiques.


## <a name="next-steps"></a>Étapes suivantes

Essayez d’activer le service Automanage pour machines virtuelles dans le portail Azure.

> [!div class="nextstepaction"]
> [Activer le service Automanage pour machines virtuelles dans le portail Azure](quick-create-virtual-machines-portal.md)