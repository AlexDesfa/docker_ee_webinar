
# La plateforme Docker Enterprise Edition
[Webinar](https://goto.docker.com/Webinaire-Series-On-Demand.html?aliId=262683773 "Tout ce que vous devez savoir sur la plateforme Docker Enterprise")

Docker Enterprise Edition est une solution de conteneurisation destinée aux entreprises, elle dispose de fonctionnalités étendues par rapport au - bien connu - Docker Engine et déploie une plate-forme de conteneurisation.
Son but est d'accompagner les organisations afin de moderniser leurs infrastructures applicatives en intégrant des fonctionnalités critiques pour les entreprises telle que notamment la sécurité et à la gouvernance.

### Respect de 3 piliers :
  - __choix__ : liberté opérationnelle des outils (CLI/Web UI), des orchestrateurs (Swarm/Kubernetes), des images (OS, applications), du type de cloud
  - __sécurité__ : authentification, rôles, encryption, sécurité des images via des signatures et des scans de vulnérabilités
  - __agilité__ : interopérabilité, automatisation, accélération des déploiements d’applications et de leur mise à jour dans un cycle continu

### Tarification :
Facturation au nombre de nœuds du cluster
3 versions :
 - basique
 - standard
 - advanced

2 niveaux de support :
 - en jours ouvrés
 - en 24/24h

### Certification :
- formations gratuites en ligne: [playwithdocker](https://training.play-with-docker.com/), [playwithkubernetes](https://training.play-with-kubernetes.com/)
- formations en classe orientées production
- certifications diplômantes en ligne

---

## Épisode 1 : Vue d’ensemble de la plateforme Docker Enterprise

### Container :
 Dans Docker Enterprise, il est bien de revenir sur la définition du container qui n'est pas une grosse brique logicielle difficile à manipuler (image des containers sur les cargos) mais plutôt un paquet portable, léger et flexible. En anglais : `a lightweight portable package that isolate software component`

### Les différentes versions de Docker :
  - moby project : framework opensource pour les contributeurs
  - docker desktop & engine : outil gratuit de distribution de containers pour les développeurs.
  - docker enterprise : plateforme d’exécution et de production de containers pour les entreprises.

### Fonctionnalités spécifiques :
Docker Enterprise est une plateforme adaptée à la production et au déploiement de containers en clusters, pour cela des fonctionnalités spécifiques au domaine des opérations ont été ajoutées:
  - __sécurité__ : contrôle de la qualité, contrôle des vulnérabilité des images, encryptions, certificats, 3rd parties contrôlées
  - __gouvernance__ : règles et droits d'accès et d'administration, responsabilités limitées sur les clusters de production, ...
  - __automatisation__ : orchestration, intégration avec le reste de la production, automatisation des logs, ...
  - __support et certification__ : support d'entreprise dédié, plug-ins et infrastructures certifiés

### Les 4 piliers de mise en production de Docker Enterprise :
  - __gouvernance__ : bonnes pratiques d'organisation autour de la mise en production, formation des développeurs, des opérateurs aux outils de conteneurisation
  - __plateforme__ : architecture des applications conteneurisées
  - __pipeline__ : méthodologie DevOps, optimisation des chaînes d'intégrations et de déploiements continus
  - __applications__

### Docker Enterprise architecture
![Docker Enterprise architecture](docker_ee_arch.png)
2 outils complémentaires pour gérer la plateforme et les orchestrateurs:
  - __Universal Control Plane (UCP)__: manager de clusters docker qui s'exécute sur Swarm ou sur Kubernetes en apportant d'autres fonctionnalités que n'ont pas ces outils opensource :
    - une installation facilitée
    - une console d'administration
    - de la sécurité
    - du contrôle d'accès basé sur des rôles
    - l'isolation physique des applications
    - l'intégration avec des annuaires LDAP/ActiveDirectory
    - l'intégration avec le Data Center : logs, utilisateurs, etc ...

  ![Screenshot Dashboard](docker_ee_dashboard.png)

  - __Docker Trusted Registry (DTR)__ : cycle de vie des images Docker, DockerHub privatif sécurisé
    - interface graphique d'administration
    - redondance des images
    - sécurité des images : scanner de vulnérabilité, protection des images de production
    - règles de promotion des images : nombre de vulnérabilités critiques
    - usage du repository:
      ```bash
      docker login dtr.xxx.docker-ee.com
      docker tag nginx dtr.xxx.docker-ee.com/dev/portal:dev
      docker push dtr.xxx.docker-ee.com/dev/portal:dev
       ```

  ![Screenshot WebDTR](docker_ee_dtr.png)

### Sécurité de la chaîne de déploiement
3 catégories de sécurisation :
  - secure platform : certificats électroniques, encryption
  - secure content : qualité des images (scanner de vulnérabilité, signature des images)
  - secure access : authentification et sécurisation de la connection des administrateurs

---
## Épisode 2 : le __choix__
Adapter une solution à ses méthode de travail

### Docker Certified Infrastructures :
Docker EE supporte différents Cloud Providers :
  - VMWare
  - AWS
  - MS Azure
  - Google Cloud (soon)
  - IBM Cloud (soon)

Docker EE supporte différents OS :
  - Windows Server
  - Ubuntu / CentOS / RedHat / Suse / Oracle Linux (pas de Debian, ou de Fedora)

Grâce à des scripts de déploiement pre-cooked :
  - Terraform : creation des machines
  - Ansible : installation de Docker Enterprise

### Federated Application Management :
Interface graphique commune pour gérer les multiples plateformes de Cloud Containers et de VM Services qui permet de gérer les clusters Swarm et/ou Kubernetes, de déplacer/reconfigurer les applications.

![Screenshot multiple platforms Infra](docker_ee_mult_platforms.png)


Scénarios :
  * Utilisation de AKS,EKS,GKE pour déployer des applications, puis les rapatrier en local
  * Création de cluster Swarm, Kubernetes ou Mixte
  * Création de services

Docker EE apporte une interface graphique mais supporte aussi les commandes en ligne natives de docker et de kubectl via un __Client Bundle__ (certificats d'administration et shell scripts dans un .zip)

  ```shell
  # unzip du client bundle
  unzip file.zip

  # chargement de l'environnement Docker EE
  source env.sh

  # interrogation du démon docker déployé via Docker EE
  docker ps
  # déploiement de pods via le service kubernetes de Docker EE
  kubectl apply -f pod-jenkins.yml
  # verification des services
  kubectl get all
  ```
Résultats sur l'interface de Docker EE :

![Screenshot Web Interface](docker_ee_web_mixed_kube_swarm.png)

### Monitoring et logging d'applications
L'outil intégré dans EE est basé sur Prometheus Engine mais d'autres solutions peuvent être intégrées (MS OMS, SysDig, Splunk, ...)
Logging EFK & ELK

### Environnements de développement et de déploiement
Git Enterprise, GitLabs, Jenkins, Selenium, Visual Studio, Eclipse, TFS, etc
