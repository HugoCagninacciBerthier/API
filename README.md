# API

# Documentation des API (REST et SOAP)
 
## Introduction
Ce projet implémente deux API permettant de rechercher des entreprises par leur numéro SIREN à partir d'un fichier CSV contenant des données sur l'index d'égalité femmes-hommes.
Les API sont implémentées en Python avec Flask et Flask-RESTx pour l'API REST, et Flask avec Zeep pour l'API SOAP.
 
## Prérequis
- Python 3.x
- Flask
- Flask-RESTx
- pandas
- Zeep
- lxml
 
Vous pouvez installer les dépendances avec la commande :
pip install flask flask-restx pandas zeep lxml

 
## 1. API REST
 
### Fonctionnalité
L'API REST permet d'obtenir des informations sur une entreprise à partir de son numéro SIREN en effectuant une requête HTTP GET.
 
### Code Source
Le fichier principal de l'API REST est basé sur Flask et Flask-RESTx. Il charge les données depuis un fichier CSV et expose un endpoint permettant la recherche d'une entreprise.
 
### Chercher une entreprise par son SIREN
- GET /siren/<siren_id> : Recherche une entreprise par son numéro SIREN.
 
### Paramètres
- **Entrée** : siren_id (string) - Numéro SIREN de l'entreprise recherchée.
- **Sortie** : JSON contenant les informations de l'entreprise ou un message d'erreur si le SIREN n'est pas trouvé.
 
### Exemple d'utilisation
#### Requête
curl -X GET "http://localhost:5000/siren/123456789"

#### Réponse
{
    "Année": "2023",
    "Structure": "Entreprise XYZ",
    "Tranche d'effectifs": "50-99",
    "SIREN": "123456789",
    "Raison Sociale": "XYZ SAS",
    "Région": "Île-de-France",
    "Département": "75",
    "Pays": "France",
    "Code NAF": "6201Z",
    "Note Index": "85"
}

 
### Lancement du serveur
python rest_api.py

Par défaut, l'API sera disponible à l'adresse http://localhost:5000.
 
---
 
## 2. API SOAP
 
### Fonctionnalité
L'API SOAP permet de récupérer les mêmes informations qu'avec l'API REST, mais en utilisant le protocole SOAP.
 
### Code Source
L'API SOAP est construite avec Flask et Zeep, et fournit un WSDL permettant aux clients de générer des requêtes conformes.
 
### Endpoints
- GET /egapro.wsdl : Fournit la description du service WSDL.
- GET /soap : Endpoint SOAP qui traite les requêtes et retourne les données associées à un numéro SIREN.
 
### Paramètres
- **Entrée** : siren (string) - Numéro SIREN de l'entreprise recherchée.
- **Sortie** : XML contenant les informations de l'entreprise ou un message d'erreur si le SIREN n'est pas trouvé.
 
### Exemple d'utilisation
#### Requête SOAP (XML)
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <GetSiren>
            <siren>123456789</siren>
        </GetSiren>
    </soap:Body>
</soap:Envelope>

#### Réponse SOAP (XML)
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <GetSirenResponse>
            <Année>2023</Année>
            <Structure>Entreprise XYZ</Structure>
            <Tranche_deffectifs>50-99</Tranche_deffectifs>
            <SIREN>123456789</SIREN>
            <Raison_Sociale>XYZ SAS</Raison_Sociale>
            <Région>Île-de-France</Région>
            <Département>75</Département>
            <Pays>France</Pays>
            <Code_NAF>6201Z</Code_NAF>
            <Note_Index>85</Note_Index>
        </GetSirenResponse>
    </soap:Body>
</soap:Envelope>

 
### Lancement du serveur
# python soap_api.py
L'API sera disponible à l'adresse http://localhost:8000.
 
## Conclusion
Ces deux API permettent de récupérer des informations sur les entreprises en fonction de leur numéro SIREN. L'API REST est plus moderne et facile à consommer, tandis que l'API SOAP offre une compatibilité avec des systèmes plus anciens utilisant ce protocole.
 
