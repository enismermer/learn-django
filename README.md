# Projet Django : Gestion des Employés

Ce projet est une application web développée avec le framework Django. Elle permet de gérer les employés d'une organisation, en fournissant des fonctionnalités telles que l'ajout, la modification, la suppression et l'affichage des employés.

## Architecture du Projet

Le projet est structuré selon les conventions de Django, avec les principaux répertoires et fichiers suivants :

```
learn-django/
├── db.sqlite3                # Base de données SQLite utilisée pour le développement
├── manage.py                 # Commande principale pour interagir avec Django
├── employe/                  # Application principale
│   ├── __init__.py           # Indique que ce répertoire est un module Python
│   ├── admin.py              # Configuration de l'administration Django
│   ├── apps.py               # Configuration de l'application
│   ├── forms.py              # Définition des formulaires
│   ├── models.py             # Définition des modèles de données
│   ├── tests.py              # Tests unitaires pour l'application
│   ├── urls.py               # Définition des routes spécifiques à l'application
│   ├── views.py              # Logique métier et gestion des requêtes
│   ├── migrations/           # Fichiers de migration pour la base de données
│   │   ├── __init__.py       # Indique que ce répertoire est un module Python
│   ├── templates/            # Fichiers HTML pour les interfaces utilisateur
│       ├── employe/          # Templates spécifiques à l'application employe
│           ├── base.html     # Template de base pour l'héritage
│           ├── confirmer_suppression.html # Page de confirmation de suppression
│           ├── formulaire.html # Formulaire pour ajouter/modifier un employé
│           ├── list.html     # Liste des employés
├── employe_project/          # Répertoire du projet Django
│   ├── __init__.py           # Indique que ce répertoire est un module Python
│   ├── asgi.py               # Point d'entrée pour les serveurs ASGI
│   ├── settings.py           # Configuration globale du projet
│   ├── urls.py               # Routes principales du projet
│   ├── wsgi.py               # Point d'entrée pour les serveurs WSGI
├── env/                      # Environnement virtuel Python
```

## Templates

Les templates sont utilisés pour générer les pages HTML dynamiques. Ils se trouvent dans le répertoire `employe/templates/employe/` et incluent :

- **base.html** : Template de base contenant la structure HTML commune (header, footer, etc.).
- **list.html** : Affiche la liste des employés.
- **formulaire.html** : Formulaire pour ajouter ou modifier un employé.
- **confirmer_suppression.html** : Page de confirmation avant de supprimer un employé.

## Modèle (Model)

Le fichier `models.py` contient les définitions des modèles de données. Par exemple, un modèle `Employe` pourrait ressembler à ceci :

```python
from django.db import models

class Employe(models.Model):
    nom = models.CharField(max_length=100)
    poste = models.CharField(max_length=100)
    date_embauche = models.DateField()

    def __str__(self):
        return self.nom
```

## Vue (View)

Les vues dans `views.py` contiennent la logique métier. Par exemple, une vue pour afficher la liste des employés :

```python
from django.shortcuts import render
from .models import Employe

def liste_employes(request):
    employes = Employe.objects.all()
    return render(request, 'employe/list.html', {'employes': employes})
```

## Routes (URLs)

Les routes sont définies dans `urls.py`. Par exemple :

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.liste_employes, name='liste_employes'),
    path('ajouter/', views.ajouter_employe, name='ajouter_employe'),
    path('modifier/<int:id>/', views.modifier_employe, name='modifier_employe'),
    path('supprimer/<int:id>/', views.supprimer_employe, name='supprimer_employe'),
]
```

## Environnement Virtuel

Le projet utilise un environnement virtuel Python pour gérer les dépendances. L'environnement est situé dans le répertoire `env/`. Pour l'activer :

```bash
source env/bin/activate
```

## Commandes Utiles

- **Lancer le serveur de développement** :

```bash
python manage.py runserver
```

- **Appliquer les migrations** :

```bash
python manage.py migrate
```

- **Créer un superutilisateur** :

```bash
python manage.py createsuperuser
```

## Auteur

Ce projet a été réalisé par Enis. Il s'agit d'un exemple d'application Django pour apprendre et pratiquer le développement web avec ce framework.