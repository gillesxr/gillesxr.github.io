---
layout: default
title: "Modification du noeud de sortie du navigateur TOR"
lang: fr
date: 2024-10-21
---
## Le noeud du problème ##

Parfois, la ressource web à laquelle vous souhaitez accéder est restreinte à une zone géographique particulière, notamment pour des problèmes de droits, comme ceux que l'on rencontre avec les évènements sportifs.

Pour résoudre ce problème vous pouvez, soit déménager dans le pays en question, ce qui peut être onéreux, soit utiliser le [navigateur TOR](https://www.torproject.org).

Par défaut, le navigateur TOR sélectionne un noeud de sortie (l'ordinateur qui accède à la ressource) dans un pays choisi aléatoirement. Ce noeud de sortie peut être définit en modifiant le fichier de configuration du navigateur nommé *torrc*.

Si vous souhaitez accéder à différentes zones géographiques, il devient pénible de modifier ce fichier à la main. Le script `change_exit_node` vous permet de réaliser ce changement en ligne de commande ou par l'intermédiaire d'une interface graphique.
