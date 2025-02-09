---
title: Nouveautés de Windows Virtual Desktop - Azure
description: Nouvelles fonctionnalités et mises à jour de produit pour Windows Virtual Desktop.
author: Heidilohr
ms.topic: overview
ms.date: 04/08/2021
ms.author: helohr
ms.reviewer: thhickli; darank
manager: femila
ms.custom: references_regions
ms.openlocfilehash: 710f33ada7a64248f0371a3e8c39e085d3f0834c
ms.sourcegitcommit: 5f482220a6d994c33c7920f4e4d67d2a450f7f08
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2021
ms.locfileid: "107107055"
---
# <a name="whats-new-in-windows-virtual-desktop"></a>Nouveautés de Windows Virtual Desktop

Windows Virtual Desktop est mis à jour régulièrement. Vous trouverez dans cet article des informations sur :

- Les dernières mises à jour.
- Nouvelles fonctionnalités
- Les améliorations apportées aux fonctionnalités existantes.
- Résolution des bogues

Cet article est mis à jour tous les mois. Pensez à consulter cette page régulièrement pour être tenu informé des nouvelles mises à jour.

## <a name="client-updates"></a>Mises à jour de client

Consultez ces articles pour en savoir plus sur les mises à jour de nos clients pour Windows Virtual Desktop et Windows Virtual Desktop :

- [Windows](/windows-server/remote/remote-desktop-services/clients/windowsdesktop-whatsnew)
- [macOS](/windows-server/remote/remote-desktop-services/clients/mac-whatsnew)
- [iOS](/windows-server/remote/remote-desktop-services/clients/ios-whatsnew)
- [Android](/windows-server/remote/remote-desktop-services/clients/android-whatsnew)
- [Web](/windows-server/remote/remote-desktop-services/clients/web-client-whatsnew)

## <a name="windows-virtual-desktop-agent-updates"></a>Mises à jour de l’agent Windows Virtual Desktop

L’agent Windows Virtual Desktop se met à jour au moins une fois par mois.

Voici les modifications apportées à l'agent Windows Virtual Desktop :

- Version 1.0.2866.1500 : cette mise à jour publiée le 26 mars 2021 corrige un problème lié à la vérification de l'intégrité de la pile.
- Version 1.0.2800.2802 : cette mise à jour publiée le 10 mars 2021 comporte des améliorations générales et des correctifs de bogues.
- Version 1.0.2800.2800 : cette mise à jour publiée le 2 mars 2021 corrige un problème de connexion inversée.
- Version 1.0.2800.2700 : cette mise à jour publiée le 10 février 2021 comporte des améliorations générales et des correctifs de bogues.
- Version 1.0.2800.2700 : cette mise à jour publiée le 4 février 2021 corrige un problème d'accès refusé.

## <a name="fslogix-updates"></a>Mises à jour FSLogix

Vous êtes curieux de découvrir les dernières mises à jour de FSLogix ? Consultez [Nouveautés de FSLogix](/fslogix/whats-new).

## <a name="march-2021"></a>Mars 2021

Voici ce qui a changé en mars 2021.

### <a name="updates-to-the-azure-portal-ui-for-windows-virtual-desktop"></a>Mises à jour de l’interface utilisateur du portail Azure pour Windows Virtual Desktop

Nous avons apporté les mises à jour suivantes à Windows Virtual Desktop pour le portail Azure :

- Nous avons activé les nouvelles options de disponibilité (zones et groupe à haute disponibilité) pour les workflows, afin de créer des pools d’hôtes et d’ajouter des machines virtuelles.
- Nous avons résolu un problème dans lequel un hôte avec l’état « A besoin d’aide » apparaissait comme indisponible. À présent, une icône d’avertissement s’affiche en regard de l’hôte.
- Nous avons activé le tri pour les sessions actives.
- Vous pouvez désormais envoyer des messages à des utilisateurs spécifiques, ou les déconnecter sous l’onglet Détails de hôte.
- Nous avons modifié le champ de la durée maximale de session.
- Nous avons ajouté un chemin de validation UO au workflow pour créer un pool d’hôtes.
- Vous pouvez désormais utiliser la toute dernière version de l’image Windows 10 lorsque vous créez un pool d’hôtes personnels.

### <a name="generation-2-images-and-trusted-launch"></a>Images Génération 2 et lancement fiable

La Place de marché Azure dispose à présent d’images de 2e génération pour Windows 10 Entreprise et Windows 10 Entreprise multisession. Ces images vous permettent d’utiliser des machines virtuelles à lancement fiable. Pour plus d’informations sur les machines virtuelles de Génération 2, consultez [Dois-je créer une machine virtuelle de génération 1 ou 2](../virtual-machines/generation-2.md). Pour savoir comment provisionner des machines virtuelles Windows Virtual Desktop à lancement fiable, consultez [notre billet sur TechCommunity](https://techcommunity.microsoft.com/t5/windows-virtual-desktop/windows-virtual-desktop-support-for-trusted-launch/m-p/2206170).

### <a name="fslogix-is-now-preinstalled-on-windows-10-enterprise-multi-session-images"></a>FSLogix est maintenant préinstallé sur les images Windows 10 Entreprise multisession

Pour faire suite aux commentaires des clients, nous avons configuré une nouvelle version de l’image Windows 10 Entreprise multisession qui comporte une version non configurée de FSLogix déjà installée. Nous espérons que votre déploiement de Windows Virtual Desktop s’en trouvera facilité.

### <a name="azure-monitor-for-windows-virtual-desktop-is-now-in-general-availability"></a>Azure Monitor pour Windows Virtual Desktop est maintenant en disponibilité générale

Azure Monitor pour Windows Virtual Desktop est maintenant en disponibilité générale. Cette fonctionnalité est un service automatique qui supervise vos déploiements et vous permet d’afficher les événements, l’intégrité et les suggestions de dépannage à un seul endroit. Pour plus d’informations, reportez-vous à [notre documentation](azure-monitor.md) ou consultez [notre billet sur TechCommunity](https://techcommunity.microsoft.com/t5/windows-virtual-desktop/azure-monitor-for-windows-virtual-desktop-is-generally-available/m-p/2242861).

### <a name="march-2021-updates-for-teams-on-windows-virtual-desktop"></a>Mises à jour de mars 2021 pour Teams sur Windows Virtual Desktop

Nous avons effectué les mises à jour suivantes pour Teams sur Windows Virtual Desktop :

- Nous avons amélioré les performances en termes de qualité vidéo sur les appels et le mode 2x2.
- Nous avons réduit l’utilisation du processeur de 5 à 10 % (selon la génération du processeur) en utilisant le déchargement matériel du traitement vidéo (XVP).
- Les machines plus anciennes peuvent désormais utiliser le décodage matériel et XVP pour afficher davantage de flux vidéo entrants de manière fluide en mode 2x2.
- Nous avons mis à jour la pile WebRTC en passant de M74 à M88 pour améliorer les performances de la synchronisation AV et réduire les problèmes temporaires.
- Nous avons remplacé notre encodeur logiciel H264 par OpenH264 (logiciel Open Source utilisé dans Teams sur le web), ce qui a amélioré la qualité vidéo de la caméra sortante.
- Nous avons activé le mode 2x2 pour Team Server, il sera accessible au grand public le 30 mars. Le mode 2x2 affiche jusqu’à quatre flux vidéo entrants en même temps.

### <a name="start-vm-on-connect-public-preview"></a>Démarrer une machine virtuelle à la connexion (préversion publique)

Le nouveau paramètre de pool d’hôtes, Démarrer une machine virtuelle à la connexion, est désormais disponible en préversion publique. Ce paramètre vous permet d’activer vos machines virtuelles dès que vous en avez besoin. Si vous souhaitez réduire les coûts, vous devrez libérer vos machines virtuelles en configurant vos paramètres Azure Compute. Pour plus d’informations, consultez notre [billet de blog](https://aka.ms/wvdstartvmonconnect) et [notre documentation](start-virtual-machine-connect.md).

### <a name="windows-virtual-desktop-specialty-certification"></a>Certification de spécialité de Windows Virtual Desktop

Nous avons publié une version bêta de l’examen AZ-140 qui vous permettra de prouver votre maîtrise de Windows Virtual Desktop dans Azure. Pour plus d’informations, consultez [notre billet sur TechCommunity](https://techcommunity.microsoft.com/t5/microsoft-learn-blog/beta-exam-prove-your-expertise-in-windows-virtual-desktop-on/ba-p/2147107).

## <a name="february-2021"></a>Février 2021

Voici ce qui a changé en février 2021.

### <a name="portal-experience"></a>Utilisation du portail

Nous avons amélioré l’expérience du portail Azure comme suit :

- Mode de drainage en bloc sur les hôtes sous l’onglet de la grille des hôtes de session. 
- L’attachement d’application MSIX est maintenant disponible en préversion publique.
- Informations de vue d’ensemble du pool d’hôtes corrigé pour le mode sombre.

### <a name="eu-metadata-storage-now-in-public-preview"></a>Stockage des métadonnées de l’UE maintenant en préversion publique

Nous hébergeons maintenant une préversion publique de la région géographique Europe (UE) comme option de stockage pour les métadonnées de service dans Windows Virtual Desktop. Les clients peuvent choisir entre Europe Ouest et Europe Nord quand ils créent leurs objets de service. Les objets et les métadonnées de service pour les pools d’hôtes seront stockés dans la région géographique Azure associée à chaque région. Pour plus d’informations, consultez [notre billet de blog annonçant la préversion publique](https://techcommunity.microsoft.com/t5/windows-virtual-desktop/announcing-public-preview-of-windows-virtual-desktop-service/m-p/2143939).

### <a name="teams-on-windows-virtual-desktop-plugin-updates"></a>Mises à jour de Teams sur le plug-in Windows Virtual Desktop

Nous avons amélioré la qualité des appels vidéo sur le plug-in Windows Virtual Desktop en résolvant les problèmes les plus couramment signalés, par exemple quand l’écran devenait soudainement foncé, ou quand la vidéo et le son se désynchronisaient. Ces améliorations doivent accroître les performances de la vue monovidéo avec la commutation de l’orateur actif. Nous avons également résolu un problème où les appareils matériels avec des caractères spéciaux n’étaient pas disponibles dans Teams.

## <a name="january-2021"></a>Janvier 2021

Voici ce qui a changé en janvier 2021 :

### <a name="new-windows-virtual-desktop-offer"></a>Nouvelle offre Windows Virtual Desktop

Les nouveaux clients réalisent une économie de 30 % sur les coûts de calcul Windows Virtual Desktop pour les machines virtuelles des séries D et Bs sur une durée maximale de 90 jours dans le cadre d’une utilisation de la solution Microsoft native. Vous pouvez faire valoir cette offre sur le portail Azure avant le 31 mars 2021. Pour en savoir plus, consultez la [page de l’offre Windows Virtual Desktop](https://azure.microsoft.com/services/virtual-desktop/offer/).

### <a name="networksecuritygrouprules-value-change"></a>Modification de la valeur de networkSecurityGroupRules 

Dans le modèle imbriqué Azure Resource Manager, nous avons modifié la valeur par défaut de networkSecurityGroupRules, passant d’un objet à un tableau. Si vous utilisez managedDisks-customimagevm.json sans spécifier de valeur pour networkSecurityGroupRules, cela vous évitera des erreurs. Cette modification n’est pas un changement cassant et assure une compatibilité descendante.

### <a name="fslogix-hotfix-update"></a>Mise à jour corrective FSLogix

Nous avons lancé FSLogix version 2009 HF_01 (2.9.7654.46150) pour résoudre les problèmes de la version précédente (2.9.7621.30127). Nous vous recommandons de cesser d’utiliser la version précédente et de mettre à jour FSLogix dès que possible.

Pour plus d’informations, consultez les notes de publication dans [Nouveautés de FSLogix](/fslogix/whats-new#fslogix-apps-2009-hf_01-29765446150).

### <a name="azure-portal-experience-improvements"></a>Améliorations de l’expérience du portail Azure

Voici les améliorations que nous avons apportées à l’expérience du portail Azure :

- Vous pouvez maintenant ajouter directement des informations d’identification d’administrateur de machines virtuelles locales au lieu d’ajouter un compte local créé avec des informations d’identification de compte de jonction de domaine Active Directory.
- Les utilisateurs peuvent désormais lister les affectations individuelles et de groupe dans des onglets distincts pour les utilisateurs individuels et les groupes.
- Le numéro de version de l’agent Windows Virtual Desktop est désormais visible dans la vue d’ensemble Machine virtuelle des pools d’hôtes.
- Ajout de la suppression en bloc pour les pools d’hôtes et les groupes d’applications.
- Vous pouvez maintenant activer ou désactiver le mode maintenance pour plusieurs hôtes de session appartenant à un pool d’hôtes.
- Suppression du champ d’adresse IP publique de la page d’information sur la machine virtuelle.

### <a name="windows-virtual-desktop-agent-troubleshooting"></a>Résolution des problèmes de l’agent Windows Virtual Desktop

Nous avons récemment créé le [guide de résolution des problèmes de l’agent Windows Virtual Desktop](troubleshoot-agent.md) pour aider les clients qui ont rencontré des problèmes courants.

### <a name="microsoft-defender-for-endpoint-integration"></a>Intégration de Microsoft Defender for Endpoint

L’intégration de Microsoft Defender pour point de terminaison est désormais en disponibilité générale. Cette fonctionnalité dote les machines virtuelles Windows Virtual Desktop de la même expérience d’investigation qu’un ordinateur Windows 10 local. Si vous utilisez Windows 10 Entreprise multisession, Microsoft Defender pour point de terminaison prend en charge jusqu’à 50 connexions utilisateur simultanées, ce qui vous fait bénéficier des économies de Windows 10 Entreprise multisession et de la confiance de Microsoft Defender pour point de terminaison. Pour plus d’informations, consultez notre [billet de blog](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/windows-virtual-desktop-support-is-now-generally-available/ba-p/2103712).

### <a name="azure-security-baseline-for-windows-virtual-desktop"></a>Ligne de base de sécurité Azure pour Windows Virtual Desktop

Nous avons récemment publié un [article sur la ligne de base de sécurité Azure](security-baseline.md) pour Windows Virtual Desktop sur lequel nous voudrions attirer votre attention. Parmi ces recommandations figurent des informations sur l’application du benchmark de sécurité Azure version 2.0 à Windows Virtual Desktop. Le benchmark de sécurité Azure décrit les paramètres et les pratiques que nous vous recommandons d’utiliser pour sécuriser vos solutions cloud sur Azure.

## <a name="december-2020"></a>Décembre 2020

Voici ce qui a changé en décembre 2020 : 

### <a name="azure-monitor-for-windows-virtual-desktop"></a>Azure Monitor pour Windows Virtual Desktop

La préversion publique d’Azure Monitor pour Windows Virtual Desktop est désormais disponible. Cette nouvelle fonctionnalité comprend un tableau de bord robuste basé sur Azure Monitor Workbooks pour aider les professionnels de l’informatique à comprendre leurs environnements Windows Virtual Desktop. Pour plus de détails, consultez l’[annonce sur notre blog](https://techcommunity.microsoft.com/t5/windows-virtual-desktop/azure-monitor-for-windows-virtual-desktop-public-preview/m-p/1946587). 

### <a name="azure-resource-manager-template-change"></a>Changement apporté au modèle Azure Resource Manager 

Dans la dernière mise à jour, nous avons supprimé tous les paramètres d’adresse IP publique du modèle Azure Resource Manager pour la création er le provisionnement de pools d’hôtes. Nous vous recommandons vivement de ne pas utiliser d’IP publiques pour Windows Virtual Desktop afin de sécuriser votre déploiement. Si votre déploiement reposait sur des IP publiques, vous devrez le reconfigurer pour utiliser des IP privées à la place ; sinon, votre déploiement ne fonctionnera pas correctement.

### <a name="msix-app-attach-public-preview"></a>Préversion publique de MSIX app attach 

MSIX app attach est un autre service proposé en préversion publique ce mois-ci. MSIX app attach est un service qui présente de manière dynamique des applications MSIX aux machines virtuelles hôtes de votre session Windows Virtual Desktop. Pour plus de détails, consultez l’[annonce sur notre blog](https://techcommunity.microsoft.com/t5/windows-virtual-desktop/msix-app-attach-azure-portal-integration-public-preview/m-p/1986231). 

### <a name="screen-capture-protection"></a>Protection contre la capture d’écran 

Ce mois-ci marque également le lancement en préversion publique de la protection contre la capture d’écran. Vous pouvez utiliser cette fonctionnalité pour empêcher la capture d’informations sensibles sur les points de terminaison clients. Pour essayer la protection contre la capture d’écran, accédez à [cette page](https://aka.ms/WVDScreenCaptureProtection).  

### <a name="built-in-roles"></a>Rôles intégrés

Nous avons ajouté de nouveaux rôles intégrés à Windows Virtual Desktop pour l’affectation d’autorisations aux administrateurs. Pour plus d’informations, consultez [Rôles intégrés pour Windows Virtual Desktop](rbac.md). 

### <a name="application-group-limit-increase"></a>Augmentation du nombre limite de groupes d’applications

Nous avons augmenté le nombre limite de groupes d’applications par locataire Azure Active Directory à 200 groupes.

### <a name="client-updates-for-december-2020"></a>Mises à jour des clients en décembre 2020

Nous avons publié de nouvelles versions des clients suivants : 

- Android
- macOS
- Windows

Pour plus d’informations sur les mises à jour des clients, consultez [Mises à jour des clients](whats-new.md#client-updates).

## <a name="november-2020"></a>Novembre 2020

### <a name="azure-portal-experience"></a>Utilisation du portail Azure

Nous avons résolu deux bogues dans l’expérience utilisateur du portail Azure :

- Le nom convivial de l’application de bureau n’est plus remplacé dans le workflow « Ajouter une machine virtuelle ».
- L’onglet de l’hôte de session se chargera désormais si les hôtes de session font partie de groupes identiques.

### <a name="fslogix-client-version-2009"></a>Client FSLogix, version 2009 

Nous avons publié une nouvelle version du client FSLogix avec de nombreux correctifs et améliorations. Pour en savoir plus, consultez [notre billet de blog](https://social.msdn.microsoft.com/Forums/en-US/defe5828-fba4-4715-a68c-0e4d83eefa6b/release-notes-for-fslogix-apps-release-2009-29762130127?forum=FSLogix).

### <a name="rdp-shortpath-public-preview"></a>Préversion publique de RDP Shortpath

RDP Shortpath introduit une connectivité directe à votre hôte de session Windows Virtual Desktop en utilisant ExpressRoute et des VPN de point à site et de site à site. Il présente également le protocole de transport URCP. RDP Shortpath est conçu pour réduire la latence et les sauts de réseau, afin d’améliorer l’expérience utilisateur. Pour en savoir plus, consultez [RDP Shortpath de Windows Virtual Desktop](shortpath.md).

### <a name="azdesktopvirtualization-version-201"></a>Az.DesktopVirtualization, version 2.0.1

Nous avons publié la version 2.0.1 des applets de commande Windows Virtual Desktop. Cette mise à jour comprend des applets de commande qui vous permettent de gérer l’attachement d’application MSIX. Vous pouvez télécharger la nouvelle version depuis [ PowerShell Gallery](https://www.powershellgallery.com/packages/Az.DesktopVirtualization/2.0.1).

### <a name="azure-advisor-updates"></a>Mises à jour d’Azure Advisor

Azure Advisor comporte désormais une nouvelle recommandation en matière de conseils de proximité dans Windows Virtual Desktop et une nouvelle recommandation pour optimiser les performances dans les pools d’hôtes à charge équilibrée en profondeur d’abord. Pour plus d’informations, consultez le [site web Azure](https://azure.microsoft.com/updates/new-recommendations-from-azure-advisor/).

## <a name="october-2020"></a>Octobre 2020

Voici ce qui a changé en octobre 2020 :

### <a name="improved-performance"></a>performances améliorées

- Nous avons optimisé les performances en réduisant la latence des connexions dans les zones géographiques Azure suivantes :
    - Suisse
    - Canada

Vous pouvez maintenant utiliser l’[Outil d’estimation de l’expérience](https://azure.microsoft.com/services/virtual-desktop/assessment/) pour estimer la qualité de l’expérience utilisateur dans ces zones.

### <a name="azure-government-cloud-availability"></a>Disponibilité du cloud Azure Government

Le cloud Azure Government est désormais en disponibilité générale. Pour en savoir plus, consultez [notre billet de blog](https://azure.microsoft.com/updates/windows-virtual-desktop-is-now-generally-available-in-the-azure-government-cloud/).

### <a name="windows-virtual-desktop-azure-portal-updates"></a>Mises à jour du portail Azure Windows Virtual Desktop

Nous avons apporté des mises à jour au portail Azure Windows Virtual Desktop :

- Correction d’une erreur resourceID qui empêchait les utilisateurs d’ouvrir l’onglet « Sessions ».
- Rationalisation de l’interface utilisateur sous l’onglet « Hôtes de session ».
- Correction des paramètres « Valeurs par défaut », « Facilité d’utilisation » et « Restaurer les valeurs par défaut » sous les propriétés RDP.
- Harmonisation des fonctions de suppression sous tous les onglets.
- Le portail valide désormais les noms d’application dans le workflow « Ajouter une application ».
- Correction d’un problème en raison duquel les données d’exportation de l’hôte de session n’étaient pas alignées dans les colonnes.
- Correction d’un problème en raison duquel le portail ne pouvait pas récupérer les sessions utilisateur.
- Correction d’un problème lors de la récupération de l’hôte de session, qui se produisait quand la machine virtuelle était créée dans un groupe de ressources différent.
- Mise à jour de l’onglet « Hôte de session » pour lister les sessions actives et déconnectées.
- L’onglet « Applications » contient désormais des pages.
- Correction d’un problème en raison duquel le texte « requiert une ligne de commande » ne s’affichait pas correctement sous l’onglet « Liste des applications ».
- Correction d’un problème en raison duquel le portail ne pouvait pas déployer des pools d’hôtes ou des machines virtuelles lors de l’utilisation de la version en allemand de la Galerie d’images partagées.

### <a name="client-updates-for-october-2020"></a>Mises à jour des clients en octobre 2020

Nous avons publié de nouvelles versions des clients. Pour en savoir plus, consultez les articles suivants :

- [Windows](/windows-server/remote/remote-desktop-services/clients/windowsdesktop-whatsnew)
- [iOS](/windows-server/remote/remote-desktop-services/clients/ios-whatsnew)

Pour plus d’informations sur les autres clients, consultez [Mises à jour des clients](#client-updates).

## <a name="september-2020"></a>Septembre 2020

Voici ce qui a changé en septembre 2020 :

- Nous avons optimisé les performances en réduisant la latence des connexions dans les zones géographiques Azure suivantes :
    - Allemagne
    - Afrique du Sud (pour les environnements de validation uniquement)

Vous pouvez maintenant utiliser l’[Outil d’estimation de l’expérience](https://azure.microsoft.com/services/virtual-desktop/assessment/) pour estimer la qualité de l’expérience utilisateur dans ces zones.

- Nous avons publié la version 1.2.1364 du client Windows Desktop pour Windows Virtual Desktop. Dans cette mise à jour, nous avons apporté les modifications suivantes :
    - Correction d’un problème empêchant le bon fonctionnement de l’authentification unique (SSO) sur Windows 7.
    - Correction d’un problème qui provoquait la déconnexion du client quand un utilisateur ayant activé l’optimisation des médias pour Teams tentait d’appeler ou de rejoindre une réunion Teams alors qu’une autre application avait un flux audio ouvert en mode exclusif.
    - Résolution d’un problème où Teams ne listait pas les périphériques audio ou vidéo quand l’optimisation des médias pour Teams était activée.
    - Ajout d’un lien « Besoin d’aide avec les paramètres ? » à la page des paramètres de bureau.
    - Correction d’un problème lié au bouton « S’abonner » lors de l’utilisation de thèmes sombres à contraste élevé.
    
- Grâce à l’aide exceptionnelle de nos utilisateurs, nous avons résolu deux problèmes critiques pour le client Microsoft Store Bureau à distance. Nous continuerons à consulter les commentaires et à résoudre les problèmes au fur et à mesure que nous ouvrons notre publication progressive du client à d’autres utilisateurs dans le monde entier.
    
- Nous avons ajouté une nouvelle fonctionnalité qui vous permet de changer l’emplacement, l’image, le groupe de ressources, le nom du préfixe et la configuration réseau d’une machine virtuelle dans le cadre du workflow pour ajouter une machine virtuelle à votre déploiement dans le portail Azure.

- Les professionnels de l’informatique peuvent désormais gérer des machines virtuelles Windows 10 Entreprise hybrides jointes à Azure Active Directory en utilisant Microsoft Endpoint Manager. Pour plus d’informations, consultez [notre billet de blog](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/microsoft-endpoint-manager-announces-support-for-windows-virtual/ba-p/1681048).

## <a name="august-2020"></a>Août 2020

Voici ce qui a changé en août 2020 :

- Nous avons amélioré les performances pour réduire la latence des connexions dans les régions Azure suivantes : 

    - Royaume-Uni
    - France
    - Norvège
    - Corée du Sud

   Vous pouvez utiliser l’[Estimateur d’expérience](https://azure.microsoft.com/services/virtual-desktop/assessment/) pour avoir une idée générale de la façon dont ces modifications affecteront vos utilisateurs.

- Le client Bureau à distance Microsoft Store (v10.2.1522+) est maintenant en disponibilité générale ! Cette version du client Bureau à distance Microsoft Store est compatible avec Windows Virtual Desktop. Nous avons également introduit des flux d’interface utilisateur actualisés pour améliorer l’expérience utilisateur. Cette mise à jour comprend Fluent Design, les modes Light et Dark ainsi que de nombreuses autres modifications intéressantes. Nous avons également réécrit le client pour qu’il utilise le même moteur RDP (Remote Desktop Protocol) sous-jacent que les clients iOS, macOS et Android. Cela nous permet de fournir de nouvelles fonctionnalités plus rapidement sur toutes les plateformes. [Téléchargez le client](https://www.microsoft.com/p/microsoft-remote-desktop/9wzdncrfj3ps?rtc=1&activetab=pivot:overviewtab) et essayez-le !

- Nous avons corrigé un problème dans le client Teams Desktop (version 1.3.00.21759) où le client montrait seulement le fuseau horaire UTC dans le chat, les canaux et le calendrier. Le client mis à jour montre maintenant le fuseau horaire de la session à distance.

- Azure Advisor fait désormais partie de Windows Virtual Desktop. Quand vous accédez à Windows Virtual Desktop via le portail Azure, vous pouvez voir des recommandations pour optimiser votre environnement Windows Virtual Desktop. Découvrez plus d’informations sur [Azure Advisor](azure-advisor.md).

- Azure CLI prend désormais en charge Windows Virtual Desktop (`az desktopvirtualization`) pour vous aider à automatiser vos déploiements Windows Virtual Desktop. Pour obtenir la liste des commandes de l’extension, consultez [desktopvirtualization](/cli/azure/ext/desktopvirtualization/).

- Nous avons mis à jour nos modèles de déploiement pour les rendre entièrement compatibles avec les interfaces Azure Resource Manager de Windows Virtual Desktop. Vous trouverez les modèles sur [GitHub](https://github.com/Azure/RDS-Templates/tree/master/ARM-wvd-templates).

- Le portail US Gov de Windows Virtual Desktop est maintenant en préversion publique. Pour plus d’informations, consultez [notre annonce](https://azure.microsoft.com/updates/windows-virtual-desktop-is-now-available-in-the-azure-government-cloud-in-preview/).

## <a name="july-2020"></a>Juillet 2020  

En juillet, l’intégration de Windows Virtual Desktop avec Gestion des ressources Azure est devenue généralement disponible.

Voici ce qui a changé avec cette nouvelle mise en production : 

- La « mise en production de l’automne 2019 » est désormais appelée « Windows Virtual Desktop (classique) », tandis que la « mise en production du printemps 2020 » s’appelle désormais simplement « Windows Virtual Desktop ». Pour plus d’informations, consultez [ce billet de blog](https://azure.microsoft.com/blog/new-windows-virtual-desktop-capabilities-now-generally-available/). 

Pour en savoir plus sur les nouvelles fonctionnalités, consultez [ce billet de blog](https://techcommunity.microsoft.com/t5/itops-talk-blog/windows-virtual-desktop-spring-update-enters-public-preview/ba-p/1340245). 

### <a name="autoscaling-tool-update"></a>Mise à jour de l’outil de mise à l’échelle automatique

La dernière version de l’outil de mise à l’échelle automatique qui était en préversion est désormais généralement disponible. Cet outil se sert d’un compte Azure Automation et de l’application logique Azure pour arrêter et redémarrer automatiquement les machines virtuelles de l’hôte de la session dans un pool d’hôtes, ce qui réduit les coûts d’infrastructure. Pour en savoir plus, consultez [Procéder à la mise à l’échelle des hôtes de session à l’aide d’Azure Automation](set-up-scaling-script.md).

### <a name="azure-portal"></a>Portail Azure

Vous pouvez désormais effectuer les opérations suivantes avec le portail Azure dans Windows Virtual Desktop : 

- affecter directement des utilisateurs à des hôtes de session de bureau personnel ;  
- modifier le paramètre d’environnement de validation pour les pools d’hôtes. 

### <a name="diagnostics"></a>Diagnostics

Nous avons mis en production de nouvelles requêtes prédéfinies pour l’espace de travail Log Analytics. Pour accéder aux requêtes, accédez à **Journaux**, puis, sous **Catégorie**, sélectionnez **Windows Virtual Desktop**. Pour en savoir plus, consultez [Utiliser Log Analytics pour la fonctionnalité de diagnostic](diagnostics-log-analytics.md).

### <a name="update-for-remote-desktop-client-for-android"></a>Mise à jour du client Bureau à distance pour Android

Le [client Bureau à distance pour Android](https://play.google.com/store/apps/details?id=com.microsoft.rdc.androidx) prend à présent en charge les connexions Windows Virtual Desktop. Depuis la version 10.0.7, le client Android offre une nouvelle interface utilisateur pour une expérience utilisateur améliorée. Le client s’intègre également avec Microsoft Authenticator sur les appareils Android pour activer l’accès conditionnel lors de l’abonnement à des espaces de travail Windows Virtual Desktop.  

La version précédente du client Bureau à distance s’appelle désormais « Bureau à distance 8 ». Toutes les connexions existantes dans la version antérieure du client seront transférées sans problème vers le nouveau client. Le nouveau client a été réécrit dans le même moteur central de protocole RDP (Remote Desktop Protocol) sous-jacent que les clients iOS et macOS, ce qui accélère la mise en production de nouvelles fonctionnalités sur toutes les plateformes. 

### <a name="teams-update"></a>Mise à jour de Microsoft Teams

Nous avons apporté des améliorations à Microsoft Teams pour Windows Virtual Desktop. Plus important encore, Windows Virtual Desktop prend désormais en charge l’optimisation audio et vidéo pour le client Windows Desktop. La redirection améliore la latence en créant des chemins directs entre utilisateurs quand ceux-ci utilise l’audio ou la vidéo dans le cadre d’appels et de réunions. Une distance moins élevée signifie moins de tronçons, ce qui améliore la fluidité sonore et visuelle des appels. Pour plus d’informations, consultez [Utiliser Microsoft Teams sur Windows Virtual Desktop](teams-on-wvd.md).

## <a name="june-2020"></a>Juin 2020

Le mois dernier, nous avons introduit l’intégration de Windows Virtual Desktop avec Azure Resource Manager en préversion. Cette mise à jour comprend de nombreuses nouvelles fonctionnalités passionnantes que nous souhaiterions vous présenter. Voici les nouveautés de cette version de Windows Virtual Desktop.

### <a name="windows-virtual-desktop-is-now-integrated-with-azure-resource-manager"></a>Windows Virtual Desktop est désormais intégré avec Azure Resource Manager

Windows Virtual Desktop est maintenant intégré à Azure Resource Manager. Dans la dernière mise à jour, tous les objets Windows Virtual Desktop sont désormais des ressources Azure Resource Manager. Cette mise à jour est également intégrée avec le contrôle d’accès en fonction du rôle (RBAC) Azure. Pour en savoir plus, consultez [Qu’est-ce qu’Azure Resource Manager ?](../azure-resource-manager/management/overview.md).

Les conséquences de ce changement sont les suivantes :

- Windows Virtual Desktop est désormais intégré au portail Azure. Cela signifie que vous pouvez gérer tout directement dans le portail, sans avoir besoin de PowerShell, d’applications web ou d’outils tiers. Pour bien démarrer, consultez notre tutoriel intitulé [Créer un pool d’hôtes avec le portail Azure](create-host-pools-azure-marketplace.md).

- Avant cette mise à jour, vous pouviez uniquement publier des RemoteApps et des Desktops sur des utilisateurs individuels. Avec Azure Resource Manager, vous pouvez désormais publier des ressources sur des groupes Azure Active Directory.

- La version précédente de Windows Virtual Desktop avait quatre rôles d’administrateur intégrés que vous pouviez attribuer à un locataire ou un pool d’hôtes. Ces rôles sont désormais dans le [contrôle d’accès en fonction du rôle (RBAC) Azure](../role-based-access-control/overview.md). Vous pouvez appliquer ces rôles à chaque objet Azure Resource Manager Windows Virtual Desktop, ce qui vous permet d’avoir un modèle de délégation complet et riche.

- Dans cette mise à jour, vous n’avez plus besoin d’exécuter la Place de marché Azure ou le modèle GitHub de manière répétée pour étendre un pool d’hôtes. Il vous suffit d’accéder à votre pool d’hôtes dans le portail Azure et de sélectionner **+ Ajouter** pour déployer des hôtes de session supplémentaires.

- Le déploiement de pool d’hôtes est maintenant entièrement intégré à [Azure Shared Image Gallery](../virtual-machines/shared-image-galleries.md). Shared Image Gallery est un service Azure distinct qui stocke des définitions d’images de machine virtuelle, notamment la gestion de versions d’images. Vous pouvez également utiliser la réplication globale pour copier et envoyer vos images vers d’autres régions Azure en vue d’un déploiement local.

- Les fonctions de supervision qui étaient auparavant effectuées à l’aide de PowerShell ou de l’application web Service de diagnostics ont été déplacées vers Log Analytics dans le portail Azure. Vous disposez désormais aussi de deux options pour visualiser vos rapports. Vous pouvez exécuter des requêtes Kusto et utiliser des classeurs pour créer des rapports visuels.

- Vous n’avez plus besoin de finaliser le consentement Azure Active Directory (Azure AD) pour utiliser Windows Virtual Desktop. Dans cette mise à jour, le locataire Azure AD sur votre abonnement Azure authentifie vos utilisateurs et fournit des contrôles Azure AD pour vos administrateurs.

### <a name="powershell-support"></a>Prise en charge de PowerShell

Nous avons ajouté de nouvelles applets de commande AzWvd au module Az Azure PowerShell avec cette mise à jour. Ce nouveau module est pris en charge dans PowerShell Core, qui s’exécute sur .NET Core.

Pour installer le module, suivez les instructions fournies dans [Configurer le module PowerShell pour Windows Virtual Desktop](powershell-module.md).

Vous pouvez également consulter la liste des commandes disponibles dans la [référence PowerShell AzWvd](/powershell/module/az.desktopvirtualization/#desktopvirtualization).

Pour plus d’informations sur les nouvelles fonctionnalités, consultez [notre billet de blog](https://techcommunity.microsoft.com/t5/itops-talk-blog/windows-virtual-desktop-spring-update-enters-public-preview/ba-p/1340245).

### <a name="additional-gateways"></a>Passerelles supplémentaires

Nous avons ajouté un nouveau cluster de passerelle en Afrique du Sud pour réduire la latence de connexion.

### <a name="microsoft-teams-on-windows-virtual-desktop-preview"></a>Microsoft Teams sur Windows Virtual Desktop (Préversion)

Nous avons apporté des améliorations à Microsoft Teams pour Windows Virtual Desktop. Plus important encore, Windows Virtual Desktop prend désormais en charge la redirection audio et vidéo pour les appels. La redirection améliore la latence en créant des chemins directs entre les utilisateurs quand ils effectuent des appels audio ou vidéo. Une distance moins élevée signifie moins de tronçons, ce qui améliore la fluidité sonore et visuelle des appels.

Pour plus d’informations, consultez [notre billet de blog](https://azure.microsoft.com/updates/windows-virtual-desktop-media-optimization-for-microsoft-teams-is-now-available-in-public-preview/).

## <a name="next-steps"></a>Étapes suivantes

Apprenez-en davantage sur ce qui est prévu à l’avenir en consultant la [feuille de route Microsoft 365 Windows Virtual Desktop](https://www.microsoft.com/microsoft-365/roadmap?filters=Windows%20Virtual%20Desktop).
