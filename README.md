Projet Docker 2 - Cluster Elasticsearch avec Kibana

L'objectif de ce projet est de mettre en place un cluster Elasticsearch composé de trois nœuds et un conteneur Kibana qui a accès au cluster.

Détail des Fichiers et Dossiers

docker-compose.yml
Ce fichier orchestre la configuration du cluster Elasticsearch et du service Kibana via Docker Compose. 
Par exemple :
services:
  es01:
    image: docker.elastic.co/elasticsearch/elasticsearch:${ES_VERSION}
    volumes:
      - esdata01:/usr/share/elasticsearch/data
      - ./es-cluster/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml
Ici, es01 est défini comme un service avec une image Elasticsearch spécifique et des volumes pour la persistance des données et la configuration.

.env
Ce fichier contient des variables d'environnement utilisées dans docker-compose.yml. 
Par exemple :
ES_VERSION=8.11.3
Cette ligne définit la version d'Elasticsearch et Kibana utilisée dans tout le projet.

es-cluster/
Dossier contenant les configurations pour Elasticsearch et Kibana.

es-cluster/elasticsearch.yml
Configuration des nœuds Elasticsearch. 
Par exemple :
cluster.name: "mon-cluster-es"
discovery.seed_hosts: ["es01", "es02", "es03"]
Ces lignes définissent le nom du cluster et les hôtes initiaux pour la découverte du cluster.

es-cluster/kibana.yml
Fichier de configuration pour Kibana. 
Par exemple :
server.host: "0.0.0.0"
elasticsearch.hosts: ["http://es01:9200"]
Ces paramètres spécifient l'adresse d'écoute du serveur Kibana et l'URL du cluster Elasticsearch auquel il se connecte.
