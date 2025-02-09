---
title: Configurer une appliance Azure Migrate pour Hyper-V
description: Découvrez comment configurer une appliance Azure Migrate pour évaluer et migrer des serveurs sur Hyper-V.
author: vineetvikram
ms.author: vivikram
ms.manager: abhemraj
ms.topic: how-to
ms.date: 03/13/2021
ms.openlocfilehash: 8f0e7ec2566928897d2b84357b599506520e8d95
ms.sourcegitcommit: 32e0fedb80b5a5ed0d2336cea18c3ec3b5015ca1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/30/2021
ms.locfileid: "105612022"
---
# <a name="set-up-an-appliance-for-servers-on-hyper-v"></a>Configurer une appliance pour les serveurs sur Hyper-V

Suivez cet article pour configurer l’appliance Azure Migrate pour la découverte et l’évaluation des serveurs Hyper-V à l’aide de l’outil [Azure Migrate : Discovery and Assessment](migrate-services-overview.md#azure-migrate-discovery-and-assessment-tool).

L'[appliance Azure Migrate](migrate-appliance.md) est une appliance légère utilisée par Azure Migrate : découverte et évaluation/Migration pour découvrir les serveurs localement et envoyer les métadonnées/données de performances des serveurs à Azure.

Vous pouvez déployer l’appliance à l’aide de deux méthodes :

- Configuration sur un serveur Hyper-V au moyen d’un disque dur virtuel téléchargé. Il s’agit de la méthode décrite dans cet article.
- Configurez-la sur un serveur Hyper-V ou serveur physique avec un script d’installation PowerShell. [Cette méthode](deploy-appliance-script.md) doit être utilisée si vous ne pouvez pas configurer un serveur à l’aide d’un disque dur virtuel, ou si vous êtes dans Azure Government.

Après avoir créé l’appliance, vérifiez qu’elle peut se connecter à Azure Migrate: Discovery and assessment, configurez-la pour la première fois, puis inscrivez-la auprès du projet.

## <a name="appliance-deployment-vhd"></a>Déploiement d'appliance (VHD)

Pour configurer l'appliance à l'aide d'un modèle VHD :

- Fournissez un nom d’appliance et générez une clé de projet sur le portail.
- Téléchargez un disque dur virtuel Hyper-V compressé à partir du portail Azure.
- Créez l’appliance et vérifiez qu’elle peut se connecter à Azure Migrate : découverte et évaluation.
- Configurez l’appliance pour la première fois, puis inscrivez-la auprès du projet en utilisant la clé de projet.

### <a name="generate-the-project-key"></a>Générer la clé de projet

1. Dans **Objectifs de migration** > **Serveurs** > **Azure Migrate : découverte et évaluation**, sélectionnez **Découvrir**.
2. Dans **Découvrir les serveurs** > **Vos serveurs sont-ils virtualisés ?** , sélectionnez **Oui, avec Hyper-V**.
3. Dans **1 : Générer une clé de projet**, affectez un nom à l’appliance Azure Migrate que vous allez configurer pour la découverte des serveurs sur Hyper-V. Le nom doit être alphanumérique et comporter 14 caractères au maximum.
1. Cliquez sur **Générer une clé** pour lancer la création des ressources Azure nécessaires. Ne fermez pas la page Découvrir des serveurs pendant la création de ressources.
1. Une fois les ressources Azure créées, une **clé de projet** est générée.
1. Copiez la clé car vous en aurez besoin pour terminer l'inscription de l'appliance lors de sa configuration.

### <a name="download-the-vhd"></a>Télécharger le disque dur virtuel

Dans **2 : Télécharger l'appliance Azure Migrate**, sélectionnez le fichier .VHD et cliquez sur **Télécharger**.

   ![Sélections pour la découverte de serveurs](./media/tutorial-assess-hyper-v/servers-discover.png)


   ![Sélections pour la génération d’une clé](./media/tutorial-assess-hyper-v/generate-key-hyperv.png)

### <a name="verify-security"></a>Vérifier la sécurité

Vérifiez que le fichier compressé est sécurisé avant de le déployer.

1. Sur le serveur où vous avez téléchargé le fichier, ouvrez une fenêtre de commande d’administrateur.
2. Exécutez la commande suivante pour générer le code de hachage du disque dur virtuel
    - ```C:\>CertUtil -HashFile <file_location> [Hashing Algorithm]```
    - Exemple d’utilisation : ```C:\>Get-FileHash -Path ./AzureMigrateAppliance_v3.20.09.25.zip -Algorithm SHA256```

Vérifiez la dernière valeur du code de hachage en comparant le résultat de la commande ci-dessus à la valeur documentée [ici](https://docs.microsoft.com/azure/migrate/tutorial-discover-hyper-v#verify-security)

## <a name="create-the-appliance"></a>Créer l’appliance

Importez le fichier téléchargé, puis créez une appliance.

1. Extrayez le fichier de disque dur virtuel compressé dans un dossier sur l’hôte Hyper-V qui hébergera l’appliance. Trois dossiers sont extraits.
2. Ouvrez le Gestionnaire Hyper-V. Dans **Actions**, cliquez sur **Importer la machine virtuelle**.

    ![Déployer le disque dur virtuel](./media/how-to-set-up-appliance-hyper-v/deploy-vhd.png)

2. Dans l’Assistant Importation de machine virtuelle > **Avant de commencer**, cliquez sur **Suivant**.
3. Dans **Localiser le dossier**, spécifiez le dossier contenant le disque dur virtuel extrait. Cliquez ensuite sur **Suivant**.
1. Dans **Sélectionner une machine virtuelle**, cliquez sur **Suivant**.
2. Dans **Choisir le type d’importation**, cliquez sur **Copier la machine virtuelle (créer un identifiant unique)** . Cliquez ensuite sur **Suivant**.
3. Dans **Choisir la destination**, laissez la valeur par défaut. Cliquez sur **Suivant**.
4. Dans **Dossiers de stockage**, laissez la valeur par défaut. Cliquez sur **Suivant**.
5. Dans **Choisir un réseau**, spécifiez le commutateur virtuel qui sera utilisé par le serveur. Le commutateur nécessite une connexion à Internet pour envoyer des données à Azure.
6. Dans **Récapitulatif**, passez en revue les paramètres. Puis, cliquez sur **Terminer**.
7. Dans Gestionnaire Hyper-V > **Machines virtuelles**, démarrez la machine virtuelle.

### <a name="verify-appliance-access-to-azure"></a>Vérifier l’accès de l’appliance à Azure

Vérifiez que l’appliance peut se connecter aux URL Azure pour les clouds [publics](migrate-appliance.md#public-cloud-urls) et du [secteur public](migrate-appliance.md#government-cloud-urls).

### <a name="configure-the-appliance"></a>Configurer l’appliance

Configurez l’appliance pour la première fois.

> [!NOTE]
> Si vous configurez l’appliance à l’aide d’un [script PowerShell](deploy-appliance-script.md) au lieu du disque dur virtuel téléchargé, ne tenez pas compte des deux premières étapes de cette procédure.

1. Dans Gestionnaire Hyper-V> **Machines virtuelles**, cliquez avec le bouton droit de la souris sur le serveur > **Se connecter**.
2. Spécifiez la langue, le fuseau horaire et le mot de passe pour l’appliance.
3. Ouvrez un navigateur sur un serveur qui peut se connecter à l’appliance, puis ouvrez l’URL de l’application web de l’appliance : **https://*nom ou adresse IP de l’appliance* : 44368**.

   Vous pouvez aussi ouvrir l’application à partir du Bureau de l’appliance en cliquant sur le raccourci de l’application.
1. Acceptez les **termes du contrat de licence** et lisez les informations relatives aux tiers.
1. Dans l’application web > **Configurer les prérequis**, procédez comme suit :
    - **Connectivité** : L’application vérifie que le serveur a accès à Internet. Si le serveur utilise un proxy :
      - Cliquez sur **Configurer le proxy**, puis spécifiez l’adresse du proxy (sous la forme http://ProxyIPAddress ou http://ProxyFQDN) et le port d’écoute.
      - Spécifiez les informations d’identification si le proxy nécessite une authentification.
      - Seuls les proxys HTTP sont pris en charge.
      - Si vous avez ajouté des détails de proxy ou désactivé le proxy et/ou l’authentification, cliquez sur **Enregistrer** pour relancer la vérification de la connectivité.
    - **Synchronisation de l’heure** : L’heure est vérifiée. L’heure de l’appliance doit être synchronisée avec l’heure Internet pour que la découverte de serveur fonctionne correctement.
    - **Installer les mises à jour** : Azure Migrate: Discovery and assessment vérifie que les dernières mises à jour sont installées sur l’appliance. Une fois la vérification terminée, vous pouvez cliquer sur **Afficher les services de l’appliance** pour voir l’état et les versions des composants s’exécutant sur l’appliance.

### <a name="register-the-appliance-with-azure-migrate"></a>Inscrire l’appliance auprès d’Azure Migrate

1. Collez la **clé de projet** copiée à partir du portail. Si vous n’avez pas la clé, accédez à **Azure Migrate : Discovery and Assessment > Découvrir > Gérer les appliances existantes**, sélectionnez le nom d’appliance que vous avez indiqué au moment de générer la clé, puis copiez la clé correspondante.
1. Vous aurez besoin d’un code d’appareil pour vous authentifier auprès d’Azure. Le fait de cliquer sur **Connexion** ouvre une boîte de dialogue modale comprenant le code de l’appareil, comme celle affichée ci-dessous.

    ![Boîte de dialogue modale indiquant le code de l’appareil](./media/tutorial-discover-vmware/device-code.png)

1. Cliquez sur **Copier le code et se connecter** pour copier le code de l’appareil et ouvrir une invite de connexion Azure dans un nouvel onglet de navigateur. S’il n’apparaît pas, vérifiez que vous avez désactivé le bloqueur de fenêtres publicitaires dans le navigateur.
1. Sous le nouvel onglet, collez le code de l’appareil, puis connectez-vous avec votre nom d’utilisateur et votre mot de passe Azure.
   
   La connexion avec un code PIN n’est pas prise en charge.
3. Si vous avez fermé accidentellement l’onglet Connexion avant de vous être connecté, vous devrez actualiser l’onglet Appliance Configuration Manager pour réactiver le bouton de connexion.
1. Une fois connecté, revenez à l’onglet précédent, c’est-à-dire, l’onglet Appliance Configuration Manager.
4. Si le compte d’utilisateur Azure utilisé pour la connexion dispose des [autorisations](./tutorial-discover-hyper-v.md#prepare-an-azure-user-account) adéquates sur les ressources Azure créées au moment de la génération de la clé, l’inscription de l’appliance est lancée.
1. Une fois l'appliance inscrite, vous pouvez consulter les détails de l'inscription en cliquant sur **Afficher les détails**.

### <a name="delegate-credentials-for-smb-vhds"></a>Déléguer des informations d’identification pour les disques durs virtuels sur SMB

Si vous utilisez des disques durs virtuels sur des SMB, vous devez activer la délégation des informations d’identification de l’appliance aux hôtes Hyper-V. Pour effectuer cette opération à partir de l’appliance :

1. Sur l’appliance, exécutez cette commande. HyperVHost1/HyperVHost2 sont des exemples de noms d’hôte.

    ```
    Enable-WSManCredSSP -Role Client -DelegateComputer HyperVHost1.contoso.com, HyperVHost2.contoso.com, HyperVHost1, HyperVHost2 -Force
    ```

2. Vous pouvez également effectuer cette opération dans l’éditeur d’objets de stratégie de groupe sur l’appliance :
    - Dans **Stratégie de l’ordinateur local** > **Configuration de l’ordinateur**, cliquez sur **Modèles d’administration** > **Système** > **Délégation d’informations d’identification**.
    - Double-cliquez sur **Autoriser la délégation de nouvelles informations d’identification**, puis sélectionnez **Activé**.
    - Dans **Options**, cliquez sur **Afficher**, puis ajoutez chaque hôte Hyper-V que vous voulez découvrir à la liste, avec **wsman/** comme préfixe.
    - Dans **Délégation d’informations d’identification**, double-cliquez sur **Autoriser la délégation de nouvelles informations d’identification avec l’authentification de serveur NTLM uniquement**. À nouveau, ajoutez chaque hôte Hyper-V que vous voulez découvrir à la liste, avec **wsman/** comme préfixe.

## <a name="start-continuous-discovery"></a>Démarrer la découverte en continu

Connectez-vous de l’appliance à des hôtes ou des clusters Hyper-V, et démarrez la découverte.

1. À l’**Étape 1 : Fournir les informations d’identification de l’hôte Hyper-V**, cliquez sur **Ajouter les informations d’identification** afin de spécifier un nom convivial pour les informations d’identification, puis ajoutez un **Nom d’utilisateur** et un **Mot de passe** pour l’hôte/le cluster Hyper-V que l’appliance utilisera afin de découvrir les serveurs. Cliquez sur **Enregistrer**.
1. Si vous souhaitez ajouter plusieurs informations d’identification à la fois, cliquez sur **Ajouter** pour enregistrer et ajouter d’autres informations d'identification. Plusieurs informations d’identification sont prises en charge pour la découverte de serveurs sur Hyper-V.
1. À l’**Étape 2 : Fournir les détails de l'hôte/du cluster Hyper-V**, cliquez sur **Ajouter une source de détection** afin de spécifier l'**adresse IP/nom de domaine complet** de l'hôte/du cluster Hyper-V ainsi que le nom convivial des informations d'identification à utiliser pour la connexion à l'hôte/au cluster.
1. Vous pouvez soit **Ajouter un seul élément**  à la fois, soit **Ajouter plusieurs éléments**  en une seule fois. Une option permet également de connaître les détails de l'hôte/du cluster Hyper-V via **Importer CSV**.

    ![Sélections relatives à l'ajout d'une source de détection](./media/tutorial-assess-hyper-v/add-discovery-source-hyperv.png)

    - Si vous choisissez **Ajouter un seul élément**, vous devez spécifier un nom convivial pour les informations d'identification ainsi que l'**adresse IP/nom de domaine complet** de l'hôte/du cluster Hyper-V, puis cliquer sur **Enregistrer**.
    - Si vous choisissez **Ajouter plusieurs éléments** _(sélectionné par défaut)_ , vous pouvez ajouter plusieurs enregistrements à la fois en spécifiant l’**adresse IP/nom de domaine complet** de l’hôte/du cluster Hyper-V avec le nom convivial des informations d’identification dans la zone de texte. Vérifiez les enregistrements ajoutés, puis cliquez sur **Enregistrer**.
    - Si vous choisissez **Importer CSV**, vous pouvez télécharger un fichier de modèle CSV, puis renseigner le fichier avec l'**adresse IP/nom de domaine complet** de l'hôte/du cluster Hyper-V ainsi qu'un nom convivial pour les informations d'identification. Importez ensuite le fichier dans l'appliance, **vérifiez** les enregistrements dans le fichier, puis cliquez sur **Enregistrer**.

1. Dès que vous cliquerez sur Enregistrer, l'appliance essaiera de valider la connexion aux hôtes/clusters Hyper-V ajoutés et affichera l'**État de validation** dans le tableau pour chaque hôte/cluster.
    - Pour les hôtes/clusters validés avec succès, vous pouvez afficher plus de détails en cliquant sur leur adresse IP/nom de domaine complet.
    - Si la validation d'un hôte échoue, examinez l'erreur en cliquant sur **Échec de validation** dans la colonne État du tableau. Réglez le problème et recommencez la validation.
    - Pour supprimer des hôtes ou des clusters, cliquez sur **Supprimer**.
    - Vous ne pouvez pas supprimer un hôte spécifique d’un cluster. Vous pouvez supprimer seulement la totalité du cluster.
    - Vous pouvez ajouter un cluster, même s’il existe des problèmes avec des hôtes spécifiques dans le cluster.
1. Vous pouvez **revalider** la connectivité aux hôtes/clusters à tout moment avant de lancer la découverte.
1. Cliquez sur **Démarrer la découverte** pour lancer la découverte des serveurs à partir des hôtes/clusters validés. Une fois la détection lancée, vous pouvez vérifier son état pour chaque hôte/cluster du tableau.

Ceci démarre la découverte. Il faut environ 2 minutes par hôte pour que les métadonnées des serveurs détectés apparaissent sur le portail Azure.

## <a name="verify-servers-in-the-portal"></a>Vérifier les serveurs dans le portail

Une fois la découverte terminée, vous pouvez vérifier que les serveurs apparaissent dans le portail.

1. Ouvrez le tableau de bord Azure Migrate.
2. Dans la page **Azure Migrate - Windows, Linux et serveurs SQL** > **Azure Migrate : Discovery and assessment**, cliquez sur l’icône qui affiche le nombre de **Serveurs découverts**.

## <a name="next-steps"></a>Étapes suivantes

Essayez l’[évaluation d’Hyper-V](tutorial-assess-hyper-v.md) avec Azure Migrate Discovery and assessment.