---
title: 'Démarrage rapide : Bien démarrer avec la création d’un espace de travail Synapse'
description: Dans ce tutoriel, vous allez voir comment créer un espace de travail Synapse, un pool SQL dédié et un pool Apache Spark serverless.
services: synapse-analytics
author: saveenr
ms.author: saveenr
manager: julieMSFT
ms.reviewer: jrasnick
ms.service: synapse-analytics
ms.subservice: workspace
ms.topic: tutorial
ms.date: 03/17/2021
ms.openlocfilehash: b22954edf4f3a5a935c470326aa43bd24ee2d708
ms.sourcegitcommit: dddd1596fa368f68861856849fbbbb9ea55cb4c7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107366060"
---
# <a name="creating-a-synapse-workspace"></a>Création d’un espace de travail Synapse

Dans ce tutoriel, vous allez voir comment créer un espace de travail Synapse, un pool SQL dédié et un pool Apache Spark serverless. 

## <a name="prerequisites"></a>Prérequis

Pour effectuer les étapes de ce tutoriel, vous devez avoir accès à un groupe de ressources pour lequel vous disposez du rôle **Propriétaire**. Créez l’espace de travail Synapse dans ce groupe de ressources.

## <a name="create-a-synapse-workspace-in-the-azure-portal"></a>Créer un espace de travail Synapse dans le portail Azure

### <a name="start-the-process"></a>Démarrer le processus
1. Ouvrez le [portail Azure](https://portal.azure.com). Dans la barre de recherche, entrez **Synapse** sans appuyer sur la touche Entrée.
1. Dans les résultats de la recherche, sous **Services**, sélectionnez **Azure Synapse Analytics**.
1. Sélectionnez **Ajouter** pour créer un espace de travail.

## <a name="basics-tab--project-details"></a>Onglet Général > Détails du projet
Remplissez les champs suivants :

1. **Abonnement** : Choisissez un abonnement.
1. **Groupe de ressources** : Utilisez n’importe quel groupe de ressources.
1. **Groupe de ressources managé** : Laissez ce champ vide.

## <a name="basics-tab--workspace-details"></a>Onglet Général > Détails de l’espace de travail
Remplissez les champs suivants :

1. **Nom de l’espace de travail** : Choisissez un nom unique au monde. Dans ce tutoriel, nous utiliserons **myworkspace**.
1. **Région** : Choisissez n’importe quelle région.

Sous **Sélectionner Data Lake Storage Gen2** :

1. À côté de **Nom du compte**, sélectionnez **Créer**, puis nommez le nouveau compte de stockage **contosolake**, ou utilisez un nom similaire, car celui-ci doit être unique.
1. À côté de **Nom du système de fichiers**, sélectionnez **Créer**, puis nommez-le **users**. Cette opération crée un conteneur de stockage appelé **users**. L’espace de travail utilise ce compte de stockage comme compte de stockage « principal » pour les tables Spark et les journaux des applications Spark.
1. Cochez la case « Attribuez-moi le rôle Contributeur aux données blob du stockage sur le compte Data Lake Storage Gen2 ». 

## <a name="completing-the-process"></a>Fin du processus
Sélectionnez **Vérifier + créer** > **Créer**. Votre espace de travail est prêt en quelques minutes.

> [!NOTE]
> Pour activer les fonctionnalités de l’espace de travail à partir d’un pool SQL dédié (anciennement SQL DW) existant, reportez-vous au [Guide pratique pour activer un espace de travail pour votre pool SQL dédié (anciennement SQL DW)](./sql-data-warehouse/workspace-connected-create.md).


## <a name="open-synapse-studio"></a>Ouvrir Synapse Studio

Après avoir créé votre espace de travail Azure Synapse, vous pouvez ouvrir Synapse Studio de deux manières :

* Ouvrez votre espace de travail Synapse dans le [portail Azure](https://portal.azure.com). Dans la section **Vue d’ensemble** de l’espace de travail Synapse, sélectionnez **Ouvrir** dans la zone Ouvrir Synapse Studio.
* Accédez à `https://web.azuresynapse.net` et connectez-vous à votre espace de travail.

## <a name="place-sample-data-into-the-primary-storage-account"></a>Placer les exemples de données dans le compte de stockage principal
Nous allons utiliser un petit jeu de données de 100 000 lignes provenant des données de NYX Taxi Cab des nombreux exemples de ce guide de démarrage. Nous commençons par le placer dans le compte de stockage principal que vous avez créé pour l’espace de travail.

* Téléchargez ce fichier sur votre ordinateur : https://azuresynapsestorage.blob.core.windows.net/sampledata/NYCTaxiSmall/NYCTripSmall.parquet 
* Dans Synapse Studio, accédez au hub de données. 
* Sélectionnez **Lié**.
* Sous la catégorie **Azure Data Lake Storage Gen2**, vous verrez un élément avec un nom qui ressemble à **myworkspace (Principal - contosolake)** .
* Sélectionnez le conteneur nommé **users (Principal)** .
* Sélectionnez **Charger**, puis sélectionnez le fichier `NYCTripSmall.parquet` que vous avez téléchargé.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Analyser en utilisant un pool SQL serverless](get-started-analyze-sql-on-demand.md)
