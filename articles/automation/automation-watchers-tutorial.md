---
title: Suivre les fichiers mis à jour avec une tâche d’observateur dans Azure Automation
description: Cet article explique comment créer une tâche d’observateur dans le compte Azure Automation afin de surveiller la création de fichiers dans un dossier.
services: automation
ms.subservice: process-automation
ms.topic: conceptual
ms.date: 12/17/2020
ms.openlocfilehash: ca4c4013e0044811a5bac8786996761b8a5c45f1
ms.sourcegitcommit: f28ebb95ae9aaaff3f87d8388a09b41e0b3445b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2021
ms.locfileid: "97682750"
---
# <a name="track-updated-files-with-a-watcher-task"></a>Suivre les fichiers mis à jour avec une tâche d’observateur

Azure Automation utilise une tâche d’observateur pour rechercher les événements et déclencher des actions avec des runbooks PowerShell. La tâche d’observateur se compose de deux éléments : l’observateur et l’action. Un runbook d’observateur s’exécute à un intervalle défini dans la tâche d’observateur et génère des données vers un runbook d’action.

> [!NOTE]
> Les tâches d’observateur ne sont pas prises en charge dans Azure Chine Vianet 21.

> [!IMPORTANT]
> Depuis mai 2020, l’utilisation d’Azure Logic Apps est la méthode recommandée et prise en charge pour surveiller des événements, planifier des tâches récurrentes et déclencher des actions. Consultez [Créer et exécuter des tâches, processus et flux de travail automatisés récurrents avec Azure Logic Apps](../logic-apps/concepts-schedule-automated-recurring-tasks-workflows.md).

Cet article vous guide lors de la création d’une tâche d’observateur pour surveiller l’ajout d’un nouveau fichier à un répertoire. Vous allez apprendre à effectuer les actions suivantes :

* Importer un runbook d’observateur
* Créer une variable Automation
* Créer un runbook d’action
* Créer une tâche d’observateur
* Déclencher un observateur
* Inspecter la sortie

## <a name="prerequisites"></a>Prérequis

Pour suivre les instructions de cet article, vous avez besoin des éléments suivants :

* Abonnement Azure. Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer [un compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
* Un [compte Automation](./index.yml) qui contiendra les runbooks Watcher et d'actions ainsi que la tâche d'observateur.
* Un [Runbook Worker hybride](automation-hybrid-runbook-worker.md) où la tâche d'observateur est exécutée.
* Runbooks PowerShell. Les runbooks PowerShell Workflow ne sont pas pris en charge par les tâches d’observateur.

## <a name="import-a-watcher-runbook"></a>Importer un runbook d’observateur

Cet article utilise un runbook d’observateur appelé **Watch-NewFile** pour rechercher les nouveaux fichiers dans un répertoire. Le runbook d’observateur récupère la dernière heure d’écriture connue pour les fichiers d’un dossier et examine tous les fichiers plus récents que ce filigrane.

Vous pouvez télécharger le runbook à partir de l’[organisation Azure Automation GitHub](https://github.com/azureautomation).

1. Accédez à la page de l’organisation Azure Automation GitHub pour [Watch-NewFile.ps1](https://github.com/azureautomation/watcher-action-that-processes-events-triggerd-by-a-watcher-runbook).
2. Pour télécharger le runbook à partir de GitHub, sélectionnez **Code** sur le côté droit de la page, puis sélectionnez **Télécharger le ZIP** pour télécharger l’intégralité du code dans un fichier zip.
3. Extrayez le contenu et [importez le runbook](manage-runbooks.md#import-a-runbook-from-the-azure-portal).

Vous pouvez également importer ce runbook dans votre compte Automation à partir du portail en suivant les étapes ci-dessous.

1. Ouvrez votre compte Automation, puis cliquez sur la page Runbooks.
2. Cliquez sur **Parcourir la galerie** et, dans la liste déroulante **Source**, sélectionnez **GitHub**.
3. Recherchez **Runbook d’observateur**, sélectionnez **Runbook d’observateur qui recherche les nouveaux fichiers dans un répertoire**, puis cliquez sur **Importer**.
4. Ajoutez un nom et une description pour le runbook, puis cliquez sur **OK** pour importer le runbook dans votre compte Automation.
5. Sélectionnez **Modifier**, puis cliquez sur **Publier**. Lorsque vous y êtes invité, cliquez sur **Oui** pour publier le runbook.

## <a name="create-an-automation-variable"></a>Créer une variable Automation

Une [variable Automation](./shared-resources/variables.md) sert à stocker les timestamps que le runbook précédent lit et stocke à partir de chaque fichier.

1. Sélectionnez **Variables** sous **Ressources partagées**, puis cliquez sur **+ Ajouter une variable**.
1. Entrez le nom **Watch-NewFileTimestamp**.
1. Sélectionnez le type DateTime.
1. Cliquez sur **Créer** pour créer la variable Automation.

## <a name="create-an-action-runbook"></a>Créer un runbook d’action

Dans une tâche d’observateur, un runbook d’action sert à agir sur les données transmises à partir d’un runbook d’observateur. Vous devez importer un runbook d’action prédéfini appelé **Process-NewFile** à partir de l’[organisation Azure Automation GitHub](https://github.com/azureautomation).

Pour créer un runbook d’action :

1. Accédez à la page de l’organisation Azure Automation GitHub pour [Process-NewFile.ps1](https://github.com/azureautomation/watcher-action-that-processes-events-triggerd-by-a-watcher-runbook).
2. Pour télécharger le runbook à partir de GitHub, sélectionnez **Code** sur le côté droit de la page, puis sélectionnez **Télécharger le ZIP** pour télécharger l’intégralité du code dans un fichier zip.
3. Extrayez le contenu et [importez le runbook](manage-runbooks.md#import-a-runbook-from-the-azure-portal).

Vous pouvez également importer ce runbook dans votre compte Automation à partir du portail :

1. Accédez à votre compte Automation et sélectionnez **Runbooks** sous **Automatisation de processus**.
1. Cliquez sur **Parcourir la galerie** et, dans la liste déroulante **Source**, sélectionnez **GitHub**.
1. Recherchez **Action d’observateur**, sélectionnez **Action d’observateur qui traite des événements déclenchés par un runbook d’observateur**, puis cliquez sur **Importer**.
1. Ajoutez un nom et une description pour le runbook, puis cliquez sur **OK** pour importer le runbook dans votre compte Automation.
1. Sélectionnez **Modifier**, puis cliquez sur **Publier**. Lorsque vous y êtes invité, cliquez sur **Oui** pour publier le runbook.

## <a name="create-a-watcher-task"></a>Créer une tâche d’observateur

À cette étape, vous configurez la tâche d’observateur référençant les runbooks d’observateur et d’action définis aux sections précédentes.

1. Accédez à votre compte Automation et sélectionnez **Tâches d’observateur** sous **Automatisation de processus**.
1. Sélectionnez la page des tâches d'observateur, puis cliquez sur **+ Ajouter une tâche d'observateur**.
1. Saisissez le nom **WatchMyFolder**.

1. Sélectionnez **Configurer l'observateur**, puis choisissez le Runbook **Watch-NewFile**.

1. Entrez les valeurs suivantes pour les paramètres :

   * **FOLDERPATH** : dossier du runbook Worker hybride où les fichiers sont créés, par exemple, **d:\fichiersexemples**.
   * **EXTENSION** : extension pour la configuration. Laisser vide pour traiter toutes les extensions de fichier.
   * **RECURSE** : opération récursive. Conservez cette valeur par défaut.
   * **RUN SETTINGS** : paramètre d’exécution du runbook. Sélectionnez le worker hybride.

1. Cliquez sur **OK**, puis sur **Sélectionner** pour revenir à la page de l'observateur.
1. Sélectionnez **Configurer l'action**, puis choisissez le runbook **Process-NewFile**.
1. Entrez les valeurs suivantes pour les paramètres :

   * **EVENTDATA** : données d’événement. Laisser vide. Les données sont transmises à partir du runbook Watcher.
   * **Run Settings** : paramètre d’exécution du runbook. Conservez la valeur Azure car ce runbook s'exécute dans Azure Automation.

1. Cliquez sur **OK**, puis sur **Sélectionner** pour revenir à la page de l'observateur.
1. Cliquez sur **OK** pour créer la tâche d'observateur.

    ![Configurer l'action d'observateur à partir de l'interface utilisateur](media/automation-watchers-tutorial/watchertaskcreation.png)

## <a name="trigger-a-watcher"></a>Déclencher un observateur

Vous devez exécuter un test comme décrit ci-dessous pour vous assurer que la tâche d’observateur fonctionne comme prévu. 

1. Accédez à distance au runbook Worker hybride.
2. Ouvrez **PowerShell** et créez un fichier de test dans le dossier.

```azurepowerShell-interactive
New-Item -Name ExampleFile1.txt
```

L’exemple ci-après illustre la sortie attendue.

```output
    Directory: D:\examplefiles


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       12/11/2017   9:05 PM              0 ExampleFile1.txt
```

## <a name="inspect-the-output"></a>Inspecter la sortie

1. Accédez à votre compte Automation et sélectionnez **Tâches d’observateur** sous **Automatisation de processus**.
1. Cliquez sur la tâche d'observateur **WatchMyFolder**.
1. Cliquez sur **Afficher les flux d'observateurs** sous **Flux** pour voir que l'observateur a trouvé le nouveau fichier et lancé le runbook d'action.
1. Pour voir les tâches du runbook d'action, cliquez sur **Afficher les tâches d'action d'observateur**. Sélectionnez une tâche pour en voir les détails.

   ![Tâches d'action d'observateur à partir de l'interface utilisateur](media/automation-watchers-tutorial/WatcherActionJobs.png)

La sortie attendue lors de la détection du nouveau fichier peut être consultée dans l’exemple suivant :

```output
Message is Process new file...

Passed in data is @{FileName=D:\examplefiles\ExampleFile1.txt; Length=0}
```

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur la création de votre propre runbook, consultez [Créer un runbook PowerShell](learn/automation-tutorial-runbook-textual-powershell.md).
