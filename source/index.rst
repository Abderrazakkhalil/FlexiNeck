FlexiNeck
=====================

.. image:: _static/flexineck_logo.png
   :alt: Logo de FlexiNeck
   :align: center
   :width: 400px

|PyPI version| |License| |Python Version| |Documentation Status|

.. |PyPI version| image:: https://img.shields.io/pypi/v/flexineck.svg
   :target: https://pypi.python.org/pypi/flexineck/
   :alt: Dernière version PyPI

.. |License| image:: https://img.shields.io/github/license/username/flexineck.svg
   :target: https://github.com/username/flexineck/blob/main/LICENSE
   :alt: Licence

.. |Python Version| image:: https://img.shields.io/pypi/pyversions/flexineck.svg
   :target: https://pypi.python.org/pypi/flexineck/
   :alt: Versions Python

.. |Documentation Status| image:: https://readthedocs.io/en/latest/?badge=latest
   :target: https://flexineck.readthedocs.io/en/latest/?badge=latest
   :alt: État de la documentation

**FlexiNeck** est un module *neck* modulaire et entièrement configurable, conçu pour s'intégrer facilement dans diverses architectures de vision par ordinateur.

Fonctionnalités clés
==========================

* **Configuration flexible** : Adaptez les composants du neck à votre tâche spécifique.
* **Polyvalence** : Compatible avec la détection d'objets, la segmentation d'images, la classification, etc.
* **Modules intégrés** :
   * FPN (Feature Pyramid Network)
   * PAN (Path Aggregation Network)
   * SPP (Spatial Pyramid Pooling)
   * Mécanismes d'attention : canal, spatial, ou hybride
   * Méthodes de fusion : simple, pondérée, ou adaptative
* **Formats de sortie variés** : pyramidal, multi-échelle, ou mono-niveau

Installation
==========================

.. code-block:: bash

   pip install flexineck

Exemple rapide d’utilisation
==============================

.. code-block:: python

   import torch
   from flexineck import FlexiNeck

   # Dimensions des sorties du backbone (ex. ResNet)
   in_channels = [256, 512, 1024, 2048]

   # Création d'un module FlexiNeck pour la détection
   neck = FlexiNeck(
       in_channels=in_channels,
       out_channels=256,
       use_fpn=True,
       use_pan=True,
       use_spp=True,
       attention_type="channel",
       fusion_type="adaptive",
       output_format="pyramid"
   )

   # Simulation de features en entrée
   features = [
       torch.randn(2, 256, 64, 64),
       torch.randn(2, 512, 32, 32),
       torch.randn(2, 1024, 16, 16),
       torch.randn(2, 2048, 8, 8)
   ]

   # Passage avant
   outputs = neck(features)  # Exemple : {'p2': tensor, 'p3': tensor, ...}

Navigation dans la documentation
==============================

.. toctree::
   :maxdepth: 2
   :caption: Sommaire

   installation
   guide_utilisateur
   architecture
   api
   configurations
   exemples
   avancé
   faq
   contribution
   changelog

Architecture
-------------------

.. image:: _static/architecture_schema.png
   :alt: Schéma de l'architecture FlexiNeck
   :align: center
   :width: 600px

La structure de **FlexiNeck** repose sur une combinaison hiérarchique de modules spécialisés pour la fusion, l’enrichissement et la normalisation des features issues d’un backbone. Chaque composant est optionnel et interchangeable, ce qui permet une grande flexibilité pour répondre aux besoins de chaque tâche de vision.

.. toctree::
   :maxdepth: 2

   architecture/vue_ensemble
   architecture/fpn
   architecture/pan
   architecture/spp
   architecture/attention
   architecture/fusion

Et ainsi de suite pour les autres sections (API, Configurations, Exemples…).

À propos
==========================

**FlexiNeck** a été conçu pour simplifier l’intégration et l’expérimentation avec des modules *neck* puissants et modernes, tout en maintenant une interface unifiée et intuitive.

Indices et tables
==========================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
