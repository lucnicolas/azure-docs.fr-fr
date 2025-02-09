---
title: Préférence de routage dans Azure
description: Découvrez comment vous pouvez choisir le mode d’acheminement de votre trafic entre Azure et Internet avec une préférence de routage.
services: virtual-network
documentationcenter: na
author: KumudD
manager: mtillman
ms.service: virtual-network
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2021
ms.author: mnayak
ms.openlocfilehash: 44edd9273730ff7ba81a3ad5af2408ff6b7b7a5c
ms.sourcegitcommit: 73fb48074c4c91c3511d5bcdffd6e40854fb46e5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106060633"
---
# <a name="what-is-routing-preference"></a>Qu’est-ce qu’une préférence de routage ?

Une préférence de routage Azure vous permet de choisir le mode d’acheminement de votre trafic entre Azure et Internet. Vous pouvez choisir de router le trafic via le réseau Microsoft ou le réseau du fournisseur de services Internet (Internet public). Ces options sont également appelées respectivement *routage de patate froide* et *routage de patate chaude*. Le prix du transfert de données de sortie varie en fonction de la sélection du routage. Vous pouvez choisir l’option de routage lors de la création d’une adresse IP publique. L’adresse IP publique peut être associée à des ressources telles qu’une machine virtuelle, un groupe de machines virtuelles identiques, un équilibreur de charge accessible via Internet, etc. Vous pouvez également définir la préférence de routage pour des ressources de stockage Azure telles que des objets blob, des fichiers, le web et Azure Data Lake. Par défaut, le trafic est acheminé via le réseau Microsoft mondial pour tous les services Azure.

## <a name="routing-via-microsoft-global-network"></a>Routage via le réseau Microsoft mondial

Lorsque vous acheminez votre trafic via le *réseau Microsoft mondial*, le trafic est acheminé sur l’un des réseaux les plus importants du globe, couvrant plus de 250 000 km de fibre avec plus de 165 points de présence en périphérie. Le réseau est correctement approvisionné avec plusieurs chemins en fibre redondants pour garantir une fiabilité et une disponibilité exceptionnellement élevées. L’ingénierie du trafic est gérée par un contrôleur WAN à définition logicielle qui garantit une sélection de chemin à faible latence pour votre trafic, et offre les performances d’un réseau d’exception.

![Routage via le réseau Microsoft mondial](media/routing-preference-overview/route-via-microsoft-global-network.png)

**Trafic d’entrée :** l’annonce du BGP Anycast global garantit que le trafic d’entrée accède au réseau Microsoft le plus proche de l’utilisateur. Par exemple, si un utilisateur à Singapour accède à des ressources Azure hébergées à Chicago, aux États-Unis, le trafic entre dans le réseau Microsoft mondial par le point de présence en périphérie de Singapour et voyage sur le réseau Microsoft jusqu’au service hébergé à Chicago.

**Trafic de sortie :** le trafic de sortie suit le même principe. Il circule essentiellement sur le réseau Microsoft mondial et sort au point le plus proche de l’utilisateur. Par exemple, si du trafic provenant d’Azure à Chicago est destiné à un utilisateur à Singapour, le trafic voyage sur le réseau Microsoft de Chicago à Singapour, et quitte le réseau Microsoft au point de présence en périphérie de Singapour.

Le trafic d’entrée et de sortie voyage en grande partie sur le réseau Microsoft mondial. C’est ce qu’on appelle également le *routage de patate froide*.


## <a name="routing-over-public-internet-isp-network"></a>Routage via l’Internet public (réseau de fournisseur de services Internet)

Le nouveau choix de *routage Internet* minimise le trajet sur le réseau Microsoft mondial et utilise le réseau de transit du fournisseur de services Internet pour acheminer votre trafic. Cette option de routage à coût optimisé offre des performances réseau comparables à celles d’autres fournisseurs de cloud.

![Routage via l’Internet public](media/routing-preference-overview/route-via-isp-network.png)

**Trafic d’entrée :** le chemin d’entrée utilise un *routage de patate chaude*, ce qui signifie que le trafic entre dans le réseau Microsoft le plus proche de la région du service hébergé. Par exemple, si un utilisateur à Singapour accède à des ressources Azure hébergées à Chicago, le trafic voyage sur l’Internet public et entre dans le réseau Microsoft mondial à Chicago.

**Trafic de sortie :** le trafic de sortie suit le même principe. Il quitte le réseau Microsoft dans la région où le service hébergé. Par exemple, si du trafic de votre service Azure à Chicago est destiné à un utilisateur à Singapour, le trafic quitte le réseau Microsoft de Chicago et transite jusqu’à l’utilisateur à Singapour via l’Internet public.

## <a name="supported-services"></a>Services pris en charge

Une adresse IP publique avec choix de préférence de routage « Réseau Microsoft mondial » peut être associée à n’importe quel service Azure. En revanche, une adresse IP publique avec choix de préférence de routage **Internet** peuvent être associée aux ressources Azure suivantes :

* Machine virtuelle
* Jeu de mise à l’échelle de machine virtuelle
* Azure Kubernetes Service (AKS)
* Équilibreur de charge accessible via Internet
* Application Gateway
* Pare-feu Azure

Pour le stockage, les points de terminaison principaux utilisent toujours le **réseau Microsoft mondial**. Vous pouvez activer des points de terminaison secondaires avec **Internet** comme choix pour le routage du trafic. Les services de stockage actuellement pris en charge sont :

* Objets blob
* Fichiers
* Web
* Azure Data Lake

## <a name="pricing"></a>Tarifs
La différence de prix entre les deux options est reflétée dans la tarification du transfert de données de sortie Internet. Le prix du transfert de données via le **réseau Microsoft mondial** est identique au prix de sortie Internet actuel. Pour accéder aux dernières informations sur la tarification, visitez la [page sur les tarifs de bande passante Azure](https://azure.microsoft.com/pricing/details/bandwidth/).

## <a name="limitations"></a>Limites


* La préférence de routage est compatible uniquement avec la référence (SKU) standard redondante interzone d’IP publique. La référence (SKU) de base d’adresse IP publique n’est pas prise en charge.
* La préférence de routage ne prend actuellement en charge que les adresses IP publiques IPv4. Les adresses IP publiques IPv6 ne sont pas prises en charge.


## <a name="next-steps"></a>Étapes suivantes

* [Configurer la préférence de routage pour une machine virtuelle à l’aide d’Azure PowerShell](configure-routing-preference-virtual-machine-powershell.md)
* [Configurer la préférence de routage pour une machine virtuelle à l’aide d’Azure CLI](configure-routing-preference-virtual-machine-cli.md)
