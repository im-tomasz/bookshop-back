# 📚 Bookshop Back

## 🚀 Description

Ce projet est le back end d’un bookshop. Je l'ai créé pour m’entraîner à créer une API à partir de la doc d'API Platform, dans le but de la consommer par une application front (par exemple en React).  
L’objectif est d’apprendre à maîtriser la création d’API en PHP, la gestion des routes, et la structuration d’un back utilisé par un front moderne.

---

## 🛠️ Stack technique

- **PHP** : langage principal pour le back end.
- **API Platform** : création rapide de routes d’API REST.
- **PostgreSQL** : pour stockage des données.

---

## 🗂️ Structure & parties importantes

- **src/Controller** : contient les contrôleurs, gère les routes et la logique derrière chaque endpoint de l’API.
- **src/Entity** : définit les objets principaux (par exemple, Livre), leur structure, et leur relation avec la base de données.
- **src/Repository** : permet d’effectuer des recherches, filtrages et accès spécifiques aux données.
- **config/** : fichiers de configuration généraux du projet (routes, services, base de données).
- **public/** : point d’entrée des requêtes (souvent index.php).

---

## 🎯 Compétences mises en application

- Création d’une API en PHP, organisation du code selon le modèle MVC simplifié.
- Définition et manipulation d’entités (objets-métiers).
- Construction de routes et gestion des requêtes REST (GET, POST, etc), via API Platform.
- Structuration d’un projet back utilisé par un front moderne (React).

---

## ✨ Exemples de code pertinents

**1. Exemple de Contrôleur d’API (src/Controller/BookController.php)**

```php name=src/Controller/BookController.php
<?php
namespace App\Controller;

use App\Entity\Book;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\JsonResponse;
use Symfony\Component\Routing\Annotation\Route;

class BookController extends AbstractController
{
    #[Route('/api/books', name: 'api_books')]
    public function index(): JsonResponse
    {
        $books = $this->getDoctrine()->getRepository(Book::class)->findAll();
        return $this->json($books);
    }
}
```
> exposition d'une route `/api/books` qui retourne au format JSON la liste des livres, accessible simplement depuis le front.

---

**2. Définition d’une entité (src/Entity/Book.php)**

```php name=src/Entity/Book.php
<?php
namespace App\Entity;

use Doctrine\ORM\Mapping as ORM;

#[ORM\Entity]
class Book
{
    #[ORM\Id]
    #[ORM\GeneratedValue]
    #[ORM\Column(type: 'integer')]
    private $id;

    #[ORM\Column(type: 'string', length: 255)]
    private $title;

    // ... autres propriétés et getters/setters
}
```
> définition de l’objet métier principal. Permet de lier proprement le code à la base de données, simplifie les échanges de données avec le front.

---

**3. Exemple de réponse JSON envoyée par l’API**

```json name=API response
[
  {
    "id": 1,
    "title": "Clean Code"
  },
  {
    "id": 2,
    "title": "Le Seigneur des Anneaux"
  }
]
```
> Voici comment l’API va répondre à une requête GET, ce qui permettra au front comme React d’afficher dynamiquement la liste des livres.
