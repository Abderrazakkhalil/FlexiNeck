.. AdaptiveNeck documentation master file

==================================
AdaptiveNeck: Documentation
==================================

.. image:: https://img.shields.io/badge/PyTorch-Compatible-red
   :target: https://pytorch.org/
   :alt: PyTorch Compatible

.. image:: https://img.shields.io/badge/License-MIT-blue.svg
   :target: https://opensource.org/licenses/MIT
   :alt: License MIT

Introduction
============

AdaptiveNeck est un module de cou (*neck*) hautement configurable et modulaire pour les architectures de vision par ordinateur moderne. Il sert d'intermédiaire entre le backbone (réseau d'extraction de caractéristiques) et les têtes spécialisées (classification, détection, segmentation).

Conçu avec une emphase sur la flexibilité et la performance, AdaptiveNeck fournit:

* Une architecture **modulaire** avec des composants interchangeables
* Un support pour plusieurs types de tâches visuelles
* Des mécanismes d'attention configurables
* Des techniques de fusion adaptatifs
* Des formats de sortie personnalisables

.. toctree::
   :maxdepth: 2
   :caption: Guide Utilisateur

   installation
   quickstart
   configuration
   examples

.. toctree::
   :maxdepth: 2
   :caption: Composants

   architecture
   fpn
   pan
   spp
   attention
   fusion

.. toctree::
   :maxdepth: 2
   :caption: API Reference

   api/adaptive_neck
   api/modules
   api/utils

.. toctree::
   :maxdepth: 1
   :caption: Développement

   contributing
   roadmap
   changelog

Caractéristiques Principales
============================

AdaptiveNeck intègre plusieurs techniques à l'état de l'art pour l'extraction et le traitement des caractéristiques:

Feature Pyramid Network (FPN)
-----------------------------

Le module FPN permet une extraction multi-échelle des caractéristiques avec des connexions top-down pour enrichir les features de basse résolution avec un contexte sémantique.

Path Aggregation Network (PAN)
-----------------------------

Le PAN complète le FPN avec un flux d'information bottom-up, améliorant ainsi la propagation des détails localisés des features de haute résolution.

Spatial Pyramid Pooling (SPP)
-----------------------------

Le module SPP capture des contextes à différentes échelles en utilisant plusieurs niveaux de pooling spatial, élargissant ainsi le champ réceptif effectif.

Mécanismes d'Attention
---------------------

AdaptiveNeck intègre plusieurs types d'attention pour améliorer les représentations de features:

* **Attention sur les Canaux**: Accentue les canaux de caractéristiques importantes
* **Attention Spatiale**: Focalise sur les régions pertinentes spatialement
* **Attention Hybride**: Combine les avantages des deux approches précédentes

Modules de Fusion Adaptative
---------------------------

Différentes stratégies de fusion sont disponibles:

* **Fusion Simple**: Addition directe des caractéristiques
* **Fusion Pondérée**: Combinaison adaptative avec des poids appris
* **Fusion Adaptative**: Utilisation de mécanismes d'attention pour guider la fusion

Installation
===========

Pour installer AdaptiveNeck:

.. code-block:: bash

   pip install adaptive-neck

Ou depuis la source:

.. code-block:: bash

   git clone https://github.com/username/adaptive-neck.git
   cd adaptive-neck
   pip install -e .

Exemple Rapide
=============

Voici un exemple simple d'utilisation d'AdaptiveNeck:

.. code-block:: python

   import torch
   from adaptive_neck import AdaptiveNeck
   
   # Définir les dimensions des features d'un backbone (ex: ResNet)
   in_channels = [256, 512, 1024, 2048]  # C2, C3, C4, C5
   
   # Créer une instance de AdaptiveNeck pour la détection d'objets
   neck = AdaptiveNeck(
       in_channels=in_channels,
       out_channels=256,
       use_fpn=True,
       use_pan=True,
       use_spp=True,
       attention_type="channel",
       fusion_type="adaptive",
       output_format="pyramid"
   )
   
   # Créer des tenseurs aléatoires simulant les features d'un backbone
   batch_size = 2
   features = [
       torch.randn(batch_size, 256, 64, 64),
       torch.randn(batch_size, 512, 32, 32),
       torch.randn(batch_size, 1024, 16, 16),
       torch.randn(batch_size, 2048, 8, 8)
   ]
   
   # Forward pass
   outputs = neck(features)
   
   # Pour le format "pyramid", outputs est un dictionnaire
   for level_name, feature_map in outputs.items():
       print(f"{level_name}: {feature_map.shape}")

Citation
========

Si vous utilisez AdaptiveNeck dans votre recherche, merci de citer:

.. code-block:: text

   @article{author2023adaptativeneck,
     title={AdaptiveNeck: A Modular and Configurable Neck Architecture for Vision Models},
     author={Author, A.},
     journal={arXiv preprint arXiv:2023.xxxxx},
     year={2023}
   }

Licence
=======

Ce projet est sous licence MIT - voir le fichier LICENSE pour plus de détails.

Indices et tables
================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
