# 🔄 Test du Load Balancing - TicketFlow

## ✅ Configuration Actuelle

### Services Démarrés

| Service | Port | Status | Description |
|---------|------|--------|-------------|
| **Eureka Server** | 8761 | ✅ UP | Service de découverte |
| **API Gateway** | 8080 | ✅ UP | Point d'entrée unique |
| **Customer Service - Instance 1** | 8081 | ✅ UP | Service métier (1ère instance) |
| **Customer Service - Instance 2** | 8082 | ✅ UP | Service métier (2ème instance) |

---

## 📊 Architecture Load Balancing

```
                      Client HTTP
                          │
                          ▼
                  ┌───────────────┐
                  │  API Gateway  │
                  │   Port 8080   │
                  └───────┬───────┘
                          │
              ┌───────────┴───────────┐
              │   Load Balancer       │
              │  (Spring Cloud LB)    │
              └───────────┬───────────┘
                          │
          ┌───────────────┴───────────────┐
          │                               │
          ▼                               ▼
    ┌─────────────┐               ┌─────────────┐
    │  Customer   │               │  Customer   │
    │  Service    │               │  Service    │
    │  Port 8081  │               │  Port 8082  │
    └─────────────┘               └─────────────┘
```

---

## 🚀 Comment les Instances ont été Démarrées

### Instance 1 (Port 8081) - Démarrage Normal
```powershell
./mvnw -pl services/customer-service spring-boot:run
```

### Instance 2 (Port 8082) - Avec Variable d'Environnement
```powershell
$env:SERVER_PORT='8082'; ./mvnw -pl services/customer-service spring-boot:run
```

> **Note :** Chaque instance utilise sa propre base de données H2 in-memory, donc les données ne sont PAS partagées entre les instances.

---

## 🧪 Tests du Load Balancing

### 1. Vérifier les Instances dans Eureka

**Dashboard Eureka :**
```
http://localhost:8761
```

**API Eureka (XML) :**
```powershell
curl.exe http://localhost:8761/eureka/apps/CUSTOMER-SERVICE
```

**Résultat Attendu :** Vous devez voir 2 instances :
- `customer-service:8081:xxxxx`
- `customer-service:8082:xxxxx`

---

### 2. Test via l'API Gateway

L'API Gateway distribue automatiquement les requêtes entre les 2 instances.

```powershell
# Test simple - Liste des clients
curl.exe http://192.168.137.1:8080/api/customers

# Test avec un client spécifique
curl.exe http://192.168.137.1:8080/api/customers/1
```

---

### 3. Test de Load Balancing avec Boucle

```powershell
# Envoyer 10 requêtes pour voir la distribution
for ($i = 1; $i -le 10; $i++) {
    Write-Output "Requête $i"
    curl.exe http://192.168.137.1:8080/api/customers/1
    Start-Sleep -Milliseconds 500
}
```

**Vérification :** Consultez les logs des deux terminaux :
- Terminal avec port 8081
- Terminal avec port 8082

Vous verrez les requêtes HTTP arriver alternativement sur chaque instance.

---

### 4. Test Direct des Instances (Sans Load Balancing)

Pour tester directement chaque instance :

```powershell
# Instance 1 (Port 8081)
curl.exe http://192.168.137.1:8081/api/customers

# Instance 2 (Port 8082)
curl.exe http://192.168.137.1:8082/api/customers
```

> **Important :** Comme chaque instance a sa propre BDD H2, elles retournent des données différentes !

---

## 📝 Observations

### Points Importants

1. **Load Balancing Automatique**
   - Spring Cloud LoadBalancer est intégré dans l'API Gateway
   - Pas de configuration supplémentaire nécessaire
   - Distribution round-robin par défaut

2. **Service Discovery**
   - Les instances s'enregistrent automatiquement dans Eureka
   - L'API Gateway découvre les instances dynamiquement
   - Si une instance tombe, elle est automatiquement retirée après 90 secondes

3. **Base de Données**
   - ⚠️ Chaque instance a sa propre BDD H2 in-memory
   - Les données ne sont PAS synchronisées
   - En production, utilisez une base de données partagée

4. **Identifiants Uniques**
   - Chaque instance a un ID unique (UUID)
   - Format : `customer-service:PORT:UUID`

---

## 🔧 Commandes Utiles

### Lister Tous les Processus
```powershell
# Voir tous les services en cours d'exécution
Get-Process -Name java
```

### Arrêter une Instance
```powershell
# Trouve le processus Java sur le port 8082
netstat -ano | Select-String ":8082"

# Arrête le processus (remplace PID par le numéro trouvé)
Stop-Process -Id PID
```

### Vérifier les Ports Utilisés
```powershell
# Vérifie les ports occupés
Test-NetConnection -ComputerName localhost -Port 8761
Test-NetConnection -ComputerName localhost -Port 8080
Test-NetConnection -ComputerName localhost -Port 8081
Test-NetConnection -ComputerName localhost -Port 8082
```

---

## 🎯 Prochaines Étapes

Pour améliorer le Load Balancing :

1. **Ajouter une 3ème instance** (Port 8083)
   ```powershell
   $env:SERVER_PORT='8083'; ./mvnw -pl services/customer-service spring-boot:run
   ```

2. **Configurer une Base de Données Partagée**
   - Remplacer H2 par PostgreSQL ou MySQL
   - Partager les données entre toutes les instances

3. **Ajouter des Métriques**
   - Spring Boot Actuator
   - Micrometer + Prometheus
   - Grafana pour visualisation

4. **Implémenter Circuit Breaker**
   - Resilience4J
   - Gestion des pannes d'instances

---

## 📚 Ressources

- [Spring Cloud Gateway](https://spring.io/projects/spring-cloud-gateway)
- [Spring Cloud LoadBalancer](https://spring.io/guides/gs/spring-cloud-loadbalancer/)
- [Netflix Eureka](https://spring.io/projects/spring-cloud-netflix)

---

**Auteur :** AHAIDOUS Khadija  
**Projet :** TicketFlow - Plateforme de réservation de tickets  
**Date :** 20 Octobre 2026
