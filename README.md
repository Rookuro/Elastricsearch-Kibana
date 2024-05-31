
## Elasticsearch & Kibana

### Partie 1: Installation et Configuration du Cluster Elasticsearch

1/ Choix de l'Environnement :

```shell
  Nous avons décidé d'utiliser Docker pour configurer Elasticsearch
```

2/ Créer un réseau Docker pour le cluster

```shell
MacBook-Pro:TP-Elasticsearch-Kibana alexis$ docker network create tp-elasticsearch-kibana_esnet
```

```shell
MacBook-Pro:TP-Elasticsearch-Kibana alexis$ docker network ls
NETWORK ID     NAME                            DRIVER    SCOPE
01a43273406f   bridge                          bridge    local
d6682ab79d4b   host                            host      local
012446e9f14c   none                            null      local
83c76ae88f24   tp-elasticsearch-kibana_esnet   bridge    local
7c5fb1a67276   tp-redis_app_net                bridge    local
MacBook-Pro:TP-Elasticsearch-Kibana alexis$ 
```

3/ Configuration du Cluster

Créer un fichier docker-compose.yml

```shell
docker-compose.yml
```

4/ Démarrage du Cluster

Lancer le docker compose

```shell
docker-compose up -d
```

Vérifier le statut du cluster

curl -X GET "localhost:9200/_cluster/health?pretty"


### Partie 2: Premiers Pas avec le Cluster Elasticsearch

1/ Créer un index nommé test01.

<img width="638" alt="Capture d’écran 2024-05-30 à 09 27 35" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/0d687ad6-82dd-4fa3-92d0-36046c757c54">

2/ Vérifier que cet index est maintenant présent.

<img width="823" alt="Capture d’écran 2024-05-30 à 09 28 29" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/818323ea-fdcd-4a0c-adb8-7929d14fa4a8">

3/ Créer un document dans cet dans l'index test01.

<img width="1413" alt="Capture d’écran 2024-05-30 à 09 43 55" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/b7d37178-b611-4d3d-8de6-f8946b256717">

4/ Afficher ce document.

<img width="638" alt="Capture d’écran 2024-05-30 à 09 44 27" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/337cde16-421c-430b-9ff7-e904b8f98ced">

5/ Afficher quel mapping a été appliquer par défaut. Est-il optimal ?

<img width="768" alt="Capture d’écran 2024-05-30 à 09 47 37" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/2f579b25-92d0-4f21-a4c2-20c79b2f659c">

<img width="611" alt="Capture d’écran 2024-05-30 à 09 47 59" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/a9d56722-8b05-4092-9490-e9639bfe142d">

Le mapping par défaut peut ne pas être optimal, notamment pour le champ date_creation, qui devrait idéalement être de type date avec un format spécifique.

6/ Essayer de modifier le mapping pour le champ date_creation, pour un plus adapté.

<img width="1415" alt="Capture d’écran 2024-05-30 à 09 57 32" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/326082ff-4d80-4be3-a901-6ca9fe3e8908">

Nous rencontrerons une erreur au cours de la modification. Pour modifier le mapping du champ date_creation, vous devez recréer l'index car Elasticsearch ne permet pas de 
modifier le type de champ d'un index existant.

```http
curl -X DELETE "localhost:9200/test01"
```
```http
curl -X PUT "localhost:9200/test01" -H 'Content-Type: application/json' -d '{
  "mappings": {
    "properties": {
      "date_creation": {
        "type": "date",
        "format": "dd-MM-yyyy"
      }
    }
  }
}'
```
7/ Créer un nouvel index test02 et  et 8/ Créer un nouvel index test02.

<img width="962" alt="Capture d’écran 2024-05-30 à 09 59 12" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/d5a7f2c8-0ecd-4991-a3a9-639dc21637f7">

9/ Afficher la manière dont le texte de la description du document a été traité par l'analyzer.

<img width="1417" alt="Capture d’écran 2024-05-30 à 10 21 19" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/10ab6066-1484-4204-9457-c76d414244f4">

10/ Créer un index test03 qui 

<img width="975" alt="Capture d’écran 2024-05-30 à 10 24 16" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/ffbc3d0d-c2ed-4ec1-9f89-13971229874d">

<img width="896" alt="Capture d’écran 2024-05-30 à 10 24 31" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/a7e5107c-c4d8-491b-aff3-d2ab5e1615c2">

<img width="1418" alt="Capture d’écran 2024-05-30 à 10 25 09" src="https://github.com/Rookuro/Elastricsearch-Kibana/assets/91243899/27c0aedb-9dfc-4ceb-803d-b6574dcaf184">

### Partie 3: Intégration de Kibana

























