---
title: Qu’est-ce que Form Recognizer ?
titleSuffix: Azure Cognitive Services
description: Le service Azure Form Recognizer vous permet d’identifier et d’extraire des paires clé/valeur et des données de table de vos formulaires, ainsi que d’extraire des informations importantes des tickets de caisse et des cartes de visite.
author: laujan
manager: nitinme
ms.service: cognitive-services
ms.subservice: forms-recognizer
ms.topic: overview
ms.date: 03/15/2021
ms.author: lajanuar
ms.custom: cog-serv-seo-aug-2020
keywords: traitement de données automatisé, traitement de documents, entrée de données automatisée, traitement des formulaires
ms.openlocfilehash: 680bb612546aaffc167970c1c48a44159ef9af6f
ms.sourcegitcommit: db925ea0af071d2c81b7f0ae89464214f8167505
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2021
ms.locfileid: "107518222"
---
# <a name="what-is-form-recognizer"></a>Qu’est-ce que Form Recognizer ?

[!INCLUDE [TLS 1.2 enforcement](../../../includes/cognitive-services-tls-announcement.md)]

Azure Form Recognizer est un service cognitif qui vous permet de créer des logiciels de traitement de données automatisé à l’aide des technologies du Machine Learning. Identifiez et extrayez du texte, des paires clé/valeur, des marques de sélection, des tableaux et une structure de vos documents : le service produit des données structurées qui incluent les relations dans le fichier d’origine, des rectangles englobants, la confiance, etc. Vous pouvez obtenir des résultats rapidement, avec précision et en adéquation avec votre contenu particulier, sans la nécessité d’une intervention manuelle lourde ou de compétences approfondies en science des données. Utilisez Form Recognizer pour automatiser l’entrée de données dans vos applications et enrichir les fonctionnalités de recherche de vos documents.

Form Recognizer est constitué de modèles de traitement de documents personnalisés, de modèles prédéfinis pour les factures, reçus, ID et cartes de visite, et du modèle de disposition. Vous pouvez appeler les modèles Form Recognizer au moyen d’une API REST ou de SDK de bibliothèque de client, afin d’en réduire la complexité et de l’intégrer à votre workflow ou application.

Cette documentation contient les types d’articles suivants :  

* Les [**Démarrages rapides**](quickstarts/client-library.md) sont des instructions de prise en main qui vous guident dans la formulation de vos requêtes au service.  
* Les [**Guides pratiques**](build-training-data-set.md) contiennent des instructions sur l’utilisation du service de manière plus spécifique ou personnalisée.  
* Les [**Concepts**](concept-layout.md) fournissent des explications approfondies sur les fonctions et fonctionnalités du service.  
* Les [**Tutoriels**](tutorial-bulk-processing.md) sont des guides plus longs qui montrent comment utiliser le service en tant que composant dans des solutions métier élargies.  

## <a name="form-recognizer-features"></a>Fonctionnalités de Form Recognizer

Avec Form Recognizer, vous pouvez facilement extraire et analyser les données de formulaire avec les fonctionnalités suivantes :

* **[API Disposition](#layout-api)**  : extrayez du texte, des marques de sélection et des structures de tableaux ainsi que les coordonnées de leurs rectangles englobants dans des documents.
* **[Modèles personnalisés](#custom-models)**  : extrayez du texte, des paires clé/valeur, des marques de sélection et les données de tableaux dans vos formulaires. Ces modèles étant entraînés avec vos propres données, ils sont adaptés à vos formulaires.

* **[Modèles prédéfinis](#prebuilt-models)**  : extrayez les données de types de documents uniques à l’aide de modèles prédéfinis. Les modèles prédéfinis suivants sont disponibles actuellement :

  * [Factures](./concept-invoices.md)
  * [Reçus](./concept-receipts.md)
  * [Cartes de visite](./concept-business-cards.md)
  * [Cartes d’identité (ID)](./concept-identification-cards.md)


## <a name="get-started"></a>Bien démarrer

Utilisez l’exemple d’outil Form Recognizer qui permet de tester Disposition, les Modèles prédéfinis, et d’effectuer l’entraînement d’un modèle personnalisé pour vos documents. Vous aurez besoin d’un abonnement Azure ([**créez-en un gratuitement**](https://azure.microsoft.com/free/cognitive-services)) ainsi que d’une clé et d’un point de terminaison de [**ressource Form Recognizer**](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesFormRecognizer) pour tester le service Form Recognizer.

### <a name="v21-preview"></a>[v2.1 (préversion)](#tab/v2-1)

> [!div class="nextstepaction"]
> [Essayer Form Recognizer](https://fott-preview.azurewebsites.net/)

### <a name="v20"></a>[v2.0](#tab/v2-0)

> [!div class="nextstepaction"]
> [Essayer Form Recognizer](https://fott.azurewebsites.net/)

---
Suivez le [Guide de démarrage rapide de la bibliothèque de client/API REST](./quickstarts/client-library.md) pour commencer à extraire des données de vos documents. Nous vous recommandons d’utiliser le service gratuit pendant que vous apprenez la technologie. N’oubliez pas que le nombre de pages gratuites est limité à 500 par mois.

Vous pouvez également utiliser les exemples REST (GitHub) pour démarrer. 

* Extraire du texte, des marques de sélection et une structure de tableau à partir de documents
  * [Extraire des données de disposition - Python](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/FormRecognizer/rest/python-layout.md)
* Entraîner des modèles personnalisés et extraire des données de formulaire
  * [Effectuer l’entraînement sans étiquettes - Python](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/FormRecognizer/rest/python-train-extract.md)
  * [Effectuer l’entraînement avec des étiquettes - Python](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/FormRecognizer/rest/python-labeled-data.md)
* Extraire des données dans des factures
  * [Extraire les données de factures - Python](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/FormRecognizer/rest/python-invoices.md)
* Extraire les données des reçus de ventes
  * [Extraire des données de reçu - Python](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/FormRecognizer/rest/python-receipts.md)
* Extraire des données à partir de cartes de visite
  * [Extraire des données de cartes de visite - Python](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/FormRecognizer/rest/python-business-cards.md)

### <a name="review-the-rest-apis"></a>Passer en revue les API REST

Vous allez utiliser les API suivantes pour entraîner des modèles et extraire des données structurées à partir de formulaires.

|Nom |Description |
|---|---|
| **Analyser la disposition** | Analysez un document transmis sous forme de flux pour en extraire du texte, des marques de sélection, des tableaux et la structure |
| **Entraîner un modèle personnalisé**| Entraîner un nouveau modèle pour analyser vos formulaires avec 5 formulaires du même type. Définissez le paramètre _useLabelFile_ sur `true` pour effectuer l’entraînement avec des données étiquetées manuellement. |
| **Analyser le formulaire** |Analysez un formulaire transmis en tant que flux de données pour en extraire du texte, des paires clé/valeur et des tableaux avec votre modèle personnalisé.  |
| **Analyser une facture** | Analysez une facture pour en extraire des informations clés, des tableaux et autre texte.|
| **Analyser le reçu** | Analysez un document de reçu pour en extraire les informations clés et d’autres textes.|
| **Analyser l’ID** | Analysez un document de carte d’identité pour extraire des informations clés et autre texte.|
| **Analyser la carte de visite** | Analysez une carte de visite pour extraire du texte et des informations clés.|

### <a name="v21-preview"></a>[v2.1 (préversion)](#tab/v2-1)

Explorez la [documentation de référence sur l’API REST](https://westus.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-v2-1-preview-3/operations/AnalyzeWithCustomForm) pour en savoir plus. Si vous êtes familiarisé avec une version précédente de l’API, consultez l’article [Nouveautés](./whats-new.md) pour en savoir plus sur les modifications récentes.

### <a name="v20"></a>[v2.0](#tab/v2-0)

Explorez la [documentation de référence sur l’API REST](https://westus.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-v2/operations/AnalyzeLayoutAsync) pour en savoir plus. Si vous êtes familiarisé avec une version précédente de l’API, consultez l’article [Nouveautés](./whats-new.md) pour en savoir plus sur les modifications récentes.

---

## <a name="layout-api"></a>API de disposition

Form Recognizer peut extraire de documents du texte, des marques de sélection et la structure des tableaux (les numéros de ligne et de colonne associés au texte) en utilisant la reconnaissance optique de caractères (OCR) haute définition et un modèle de deep learning amélioré. Pour plus d’informations, consultez le guide conceptuel [Disposition](./concept-layout.md).

:::image type="content" source="./media/tables-example.jpg" alt-text="Exemples de tableaux" lightbox="./media/tables-example.jpg":::

## <a name="custom-models"></a>Modèles personnalisés

Les modèles personnalisés Form Recognizer effectuent l’entraînement avec vos propres données, et il vous suffit de cinq exemples de formulaires d’entrée pour démarrer. Un modèle de traitement de documents entraîné peut restituer des données structurées qui incluent les relations du document de formulaire d’origine. Une fois que le modèle est entraîné, vous pouvez le tester, le réentraîner et l’utiliser ensuite pour extraire de manière fiable des données d’autres formulaires, en fonction de vos besoins.

Quand vous entraînez des modèles personnalisés, vous disposez des options suivantes : entraînement avec des données étiquetées et sans données étiquetées.

### <a name="train-without-labels"></a>Effectuer l’entraînement sans étiquettes

Form Recognizer utilise l’apprentissage non supervisé pour comprendre la disposition et les relations entre les champs et les entrées de vos formulaires. Quand vous soumettez vos formulaires d’entrée, l’algorithme groupe les formulaires par types, découvre les clés et les tableaux présents, et associe les valeurs aux clés et les entrées aux tableaux. L’entraînement sans étiquette ne nécessitant pas d’étiquetage manuel des données ni de programmation et de maintenance intensives, nous vous recommandons d’essayer cette méthode en premier.

Consultez [Créer un jeu de données d’entraînement](./build-training-data-set.md) pour obtenir des conseils sur la collecte de vos documents d’entraînement.

### <a name="train-with-labels"></a>Effectuer l’entraînement avec des étiquettes

Quand vous effectuez l’entraînement avec des données étiquetées, le modèle utilise l’apprentissage supervisé afin d’extraire les valeurs dignes d’intérêt, à l’aide des formulaires étiquetés que vous fournissez. Des données étiquetées aboutissent à des modèles plus performants et peuvent engendrer des modèles qui fonctionnent avec des formulaires complexes ou des formulaires contenant des valeurs sans clés.

Form Recognizer utilise l’[API Layout](#layout-api) pour connaître les tailles et les positions attendues des éléments de texte imprimés et manuscrits et pour extraire des tables. Ensuite, il utilise des étiquettes spécifiées par l’utilisateur pour connaître les associations clé/valeur et les tables dans les documents. Nous vous recommandons d’utiliser cinq formulaires étiquetés manuellement du même type (même structure) pour commencer l’entraînement d’un nouveau modèle et d’ajouter des données étiquetées en fonction des besoins afin d’améliorer la justesse du modèle. Form Recognizer permet d’effectuer l’entraînement d’un modèle pour extraire des paires clé-valeur et des tables à l’aide de fonctionnalités d’apprentissage supervisé. 

[Bien démarrer avec l’entraînement avec des étiquettes](./quickstarts/label-tool.md)

> [!VIDEO https://channel9.msdn.com/Shows/Docs-Azure/Azure-Form-Recognizer/player]

## <a name="prebuilt-models"></a>Modèles prédéfinis

Form Recognizer comprend aussi des modèles prédéfinis pour le traitement de données automatisé des types de formulaires uniques.

### <a name="prebuilt-invoice-model"></a>Modèle de facture prédéfini

Le modèle de facture prédéfini extrait les données des factures dans différents formats, et retourne des données structurées. Ce modèle extrait des informations clés, comme l’ID de facture, les détails du client, les détails du fournisseur, le destinataire de l’envoi, le destinataire de la facture, le total, les taxes, le sous-total, les éléments de ligne, et ainsi de suite. De plus, le modèle de facture prédéfini est entraîné pour analyser et retourner tout le texte et tous les tableaux de la facture. Pour plus d’informations, consultez le guide conceptuel [Factures](./concept-invoices.md).

:::image type="content" source="./media/overview-invoices.jpg" alt-text="Exemple de facture" lightbox="./media/overview-invoices.jpg":::

### <a name="prebuilt-receipt-model"></a>Modèle de ticket de caisse prédéfini

Le modèle Prebuilt Receipt (Ticket de caisse prédéfini) permet de lire les tickets de caisse en anglais émis en Australie, au Canada, en Grande-Bretagne, en Inde et aux États-Unis&mdash;du type utilisé dans les restaurants, les stations-service, les commerces, etc. Ce modèle extrait des informations clés telles que la date et l’heure de la transaction, les détails du commerçant, le montant des taxes, les articles, les totaux, etc. En outre, le modèle de reçu préconstruit est entraîné pour analyser et retourner tout le texte d’un reçu. Pour plus d’informations, consultez le guide conceptuel des [reçus](./concept-receipts.md).

:::image type="content" source="./media/overview-receipt.jpg" alt-text="exemple de ticket de caisse" lightbox="./media/overview-receipt.jpg":::

### <a name="prebuilt-identification-id-cards-model"></a>Modèle prédéfini de cartes d’identité (ID)

Le modèle Cartes d’identité (ID) vous permet d’extraire les informations clés de passeports du monde entier et de permis de conduire des États-Unis. Il extrait des données telles que l’ID de document, la date de naissance, la date d’expiration, le nom, le pays, la région, la zone lisible par machine et plus encore. Pour plus d’informations, consultez le guide conceptuel des [cartes d’identité (ID)](./concept-identification-cards.md).

:::image type="content" source="./media/overview-id.jpg" alt-text="exemple de carte d’identité" lightbox="./media/overview-id.jpg":::

### <a name="prebuilt-business-cards-model"></a>Modèle de cartes de visite prédéfini

Le modèle Business Cards (Cartes de visite) vous permet d’extraire des informations d’une carte de visite rédigée en anglais telles que le nom, la fonction, l’adresse postale, l’adresse e-mail, la société et les numéros de téléphone de la personne. Pour plus d’informations, consultez le guide conceptuel des [cartes de visite](./concept-business-cards.md).

:::image type="content" source="./media/overview-business-card.jpg" alt-text="exemple de carte de visite" lightbox="./media/overview-business-card.jpg":::

## <a name="input-requirements"></a>Critères des entrées

[!INCLUDE [input requirements](./includes/input-requirements.md)]

## <a name="deploy-on-premises-using-docker-containers"></a>Déployer localement en utilisant des conteneurs Docker

[Utilisez des conteneurs Form Recognizer(préversion)](form-recognizer-container-howto.md) pour déployer des fonctionnalités d’API localement. Ce conteneur Docker vous donne la possibilité de rapprocher le service plus près de vos données, ce qui peut être souhaitable pour des raisons de conformité, de sécurité ou opérationnelles.

## <a name="service-availability-and-redundancy"></a>Disponibilité et redondance du service

### <a name="is-form-recognizer-service-zone-resilient"></a>Le service Form Recognizer est-il résilient aux zones ?

Oui. Le service Form Recognizer est résilient aux zones par défaut.

### <a name="how-do-i-configure-the-form-recognizer-service-to-be-zone-resilient"></a>Comment configurer le service Form Recognizer pour le rendre résilient aux zones ?

Aucune configuration client n’est nécessaire pour activer la résilience des zones. La résilience aux zones pour les ressources Form Recognizer est disponible par défaut et gérée par le service lui-même.

## <a name="data-privacy-and-security"></a>Sécurité et confidentialité des données

Comme c’est le cas pour tous les services Cognitive Services, les développeurs utilisant le service Form Recognizer doivent connaître les politiques de Microsoft relatives aux données client. Pour en savoir plus, consultez la [page Cognitive Services](https://www.microsoft.com/trustcenter/cloudservices/cognitiveservices) dans le Centre de gestion de la confidentialité Microsoft.

## <a name="next-steps"></a>Étapes suivantes

Essayez notre outil en ligne et notre guide de démarrage rapide pour en savoir plus sur le service Form Recognizer.

* [**Outil Form Recognizer**](https://fott-preview.azurewebsites.net/)
* [**Démarrage rapide de la bibliothèque de client et de l’API REST**](quickstarts/client-library.md)
