# 🏦 Digital Banking — Spring Boot & Angular

**Application bancaire full-stack : gestion des clients, des comptes et des opérations (débit, crédit, virement).**

![Java](https://img.shields.io/badge/Java-17-ED8B00?logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-4.0-6DB33F?logo=springboot&logoColor=white)
![Angular](https://img.shields.io/badge/Angular-13-DD0031?logo=angular&logoColor=white)
![H2](https://img.shields.io/badge/H2-in--memory-1F6FEB)
![Lombok](https://img.shields.io/badge/Lombok-✓-BC4521)

Projet réalisé dans le cadre de l'examen final du module **Java / Spring** — Génie informatique, Université Mundiapolis.

---

## ✨ Fonctionnalités

- **Clients** : liste, recherche par mot-clé, création, modification, suppression
- **Comptes bancaires** : comptes courants (découvert) et comptes épargne (taux d'intérêt), statut du compte
- **Opérations** : débit, crédit et virement entre comptes, avec contrôle du solde
- **Historique paginé** des opérations d'un compte
- **Front Angular** : navigation clients → comptes d'un client → opérations

## 🏗️ Architecture

```
┌──────────────────────┐    HTTP / JSON    ┌──────────────────────────────────────┐
│  angular-banking-    │ ────────────────▶ │  spring-banking-backend  (:8085)     │
│  frontend  (:4200)   │                   │  web → services → repositories → H2  │
└──────────────────────┘                   └──────────────────────────────────────┘
```

**Backend** (`spring-banking-backend`), organisé en couches :

| Package | Rôle |
|---|---|
| `entities` | `Customer`, `BankAccount` (abstraite) → `CurrentAccount` / `SavingAccount`, `AccountOperation` |
| `dtos` + `mappers` | Objets de transfert pour ne pas exposer les entités JPA |
| `repositories` | Interfaces Spring Data JPA |
| `services` | Logique métier (`BankAccountService`) et exceptions métier |
| `web` | Contrôleurs REST |

L'héritage des comptes utilise la stratégie JPA `SINGLE_TABLE` avec une colonne discriminante `TYPE`.

## 🔌 API REST

| Méthode | Endpoint | Description |
|---|---|---|
| `GET` | `/customers` | Liste des clients |
| `GET` | `/customers/search?keyword=` | Recherche de clients |
| `GET` | `/customers/{id}` | Détail d'un client |
| `POST` | `/customers` | Créer un client |
| `PUT` | `/customers/{id}` | Modifier un client |
| `DELETE` | `/customers/{id}` | Supprimer un client |
| `GET` | `/accounts` | Liste des comptes |
| `GET` | `/accounts/{id}` | Détail d'un compte |
| `GET` | `/accounts/{id}/operations` | Historique complet |
| `GET` | `/accounts/{id}/pageOperations?page=&size=` | Historique paginé |
| `POST` | `/accounts/debit` | Débit |
| `POST` | `/accounts/credit` | Crédit |
| `POST` | `/accounts/transfer` | Virement |

## 🚀 Lancer le projet

**Prérequis :** Java 17, Node.js 16+ et Angular CLI 13.

```bash
# 1. Backend
cd exam-final-java/spring-banking-backend
./mvnw spring-boot:run          # http://localhost:8085  (console H2 : /h2-console)

# 2. Frontend
cd exam-final-java/angular-banking-frontend
npm install
ng serve                         # http://localhost:4200
```

## 📁 Structure

```
exam-final-java/
├── spring-banking-backend/     # API REST Spring Boot
└── angular-banking-frontend/   # Client Angular
```

---

👤 **Saad Sabir Idrissi** — Élève ingénieur Data & IA · [Portfolio](https://saad-sabir-idrissi.vercel.app) · [LinkedIn](https://www.linkedin.com/in/saad-sabir-idrissi)
