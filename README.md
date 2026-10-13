# Projet IaC & DevSecOps - TD2 : Déploiement automatisé de NovaShop

Ce dépôt contient l'ensemble du code d'Infrastructure as Code (IaC) réalisé dans le cadre du TD2. L'objectif de ce projet est de provisionner, configurer et déployer de bout en bout l'application 3-tiers "NovaShop" sur un cluster Kubernetes (K3s) hébergé sur OpenStack.

## Technologies utilisées

L'approche de ce projet est entièrement déclarative et repose sur trois piliers :
* **Terraform** (Provisionnement) : Création des ressources sur OpenStack (Machine Virtuelle, IP flottante, Règles de sécurité, Réseau) via des *data sources* et *resources*.
* **Ansible** (Configuration) : Préparation de la VM, installation automatique du cluster K3s, récupération du `kubeconfig` et ouverture d'un tunnel SSH sécurisé.
* **Helm & Kubernetes** (Déploiement applicatif) : Packaging et déploiement de l'application NovaShop dans le namespace `td2` (Ingress, Services, Deployments, StatefulSet pour la persistance des données).

## Architecture du dépôt

```text
.
├── terraform/       # Fichiers HCL (provider, variables, outputs, resources, data)
├── ansible/         # Playbook et rôles Ansible (k3s-prereq, k3s, kubeconfig)
├── helm/            # Charts Helm de l'application NovaShop
│   ├── postgres/    # Base de données (StatefulSet, PVC)
│   ├── backend/     # API Python (Déploiement multi-réplicas, ConfigMap)
│   └── frontend/    # Serveur Web Nginx (Ingress Traefik, Load-Balancing)
└── README.md
