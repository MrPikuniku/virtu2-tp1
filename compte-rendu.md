# TP 1 - Découverte de Kubernetes
### R5.09 - Virtualisation avancée

# 1. Manipulation de pods

### 1.1 Combien de pods sont présents dans le système ?
Il n'en a pas            
**Commande :**
```sh
k get pods
```

### 1.2 Créez un pod avec les spécifications suivantes
- nom `nginx`
- image `nginx:alpine`

```sh
k run nginx --image nginx:alpine
```

## 1.3 Affichez l’état de votre pod en listant les pods du système
Le pod est en execution
```sh
k describe pods
```

### 1.4 Sur quel Node sont exécutés vos pods

sur minikube
```sh
k get pods -o wide  
```

### 1.5 Supprimez le Pod que vous venez de créer
```sh
k delete pod nginx 
```

### 1.6 Créez un nouveau Pod avec les spécifications suivantes
```sh
k run redis --image redis123
```

### 1.7 Consultez l’état de votre Pod, il devrait y avoir une erreur. Savez-vous qu’elle en est la cause ? 
L'image redis123 n'existe pas

### 1.8 Éditez la configuration de votre Pod pour réparer le problème

modifier le champ image
```sh
k edit redis
```

### 1.9 Supprimez votre pod
```sh
k delete pod redis
```

# 2. Déploiements

### 2.1 Créer un Deployment avec les spécifications suivantes
- nom `hello-deploy`
- image [`gcr.io/google-samples/hello-app:1.0`](http://gcr.io/google-samples/hello-app:1.0)
- 3 répliques
  
```sh
 k create deployment --image=gcr.io/google-samples/hello-app:1.0 hello-deploy --replicas=3
```

### 2.2 Listez le nombre de Pods dans le système, que remarquez-vous dans le nom des Pods ?
Leur nom coommence par hello-deploy  

### 2.3 Inspectez un des Pods hello, par qui sont-ils contrôlés ?
```sh
hello-deploy-64f6c6995
```
__COMMENT_ON_SAIT_QU'ILS_SONT_CONTROLES__
```sh 
ControlledBy: ReplicaSet/hello-deploy-64f6c6995
```

### 2.4 Tentez de supprimer l’un des pods `hello`, puis listez les pods du système, combien de pods y a-t-il ? Pourquoi ?
Il y en a trois car le déploiement est reglé a trois replicatas   

### 2.5 Modifiez votre Deployment pour qu’il gère maintenant 5 répliques, vérifiez que la modification est effective en listant les Deployments présents sur le système, puis confirmez en listant les Pods .
Il faut modifier les champs dans lesquels il y a écrit 'replica';  

```sh
k get deploy

k get pods
```

### 2.6 Réduisez à présent le nombre de répliques à 2, vérifiez que la modification a été prise en compte.
k get deploy
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
hello-deploy   2/2     2            2

### 2.7 Supprimez votre déploiement, combien de pods sont désormais présents dans le système ?
k delete deployment/he 

# 3. Syntaxe déclaratve 

### 3.1 Via l'approche `impérative`, créez le Pod suivant :
- nom `redis-imp`
- image `redis`
```sh
__COMMANDE__
```

### 3.2 Récupérez la configuration de votre Pod `redis-imp` au format YAML pour pouvoir la sauvegarder dans un fichier `redis-imp.yaml`
```sh
__COMMANDE__
```

### 3.3 Utilisez l’approche déclarative pour créer un Pod :
- nom : `nginx`
- image : `nginx:alpine`
```sh
__COMMANDE__
```

### 3.4 Supprimez-le ensuite via la syntaxe déclarative
```sh
__COMMANDE__
```

### 3.5 Via la syntaxe déclarative, créez un déploiement avec les spécifications suivantes
- nom `hello-deploy`
- nombre de répliques 3
- image `gcr.io/google-samples/hello-app:1.0`
```sh
__COMMANDE__
```

### 3.6 Via l’approche impérative, passez le nombre de répliques de 3 à 5. Supprimez ensuite votre déploiement puis recréez-le, combien y a-t-il de répliques ? Qu’en déduisez-vous ?
```sh 
__COMMANDE__
```
__REPONSE__

### 3.7 Effectuez la même manœuvre via l'approche déclarative cette fois
```sh
__COMMANDE__
```

# 4. Configuration des Pods

### 4.1 Via l’approche déclarative, créez un fichier configuration pour un Pod puis créez-le :
- fichier `color.pod.yaml`
- nom `color-deploy`
- image `arthureudeline/color-env:1.0.0`
- Modifiez votre fichier pour paramétrer l’environnement des pods pour y ajouter la variable `COLOR` avec la valeur `red`.
- Créez ensuite ce pod.
```sh
__COMMANDE__
```
Modifications du fichier du pod

```yaml
__MODIFS__
```

### 4.2 Modifiez ensuite votre fichier pour passer la variable `COLOR` à `blue`. Tentez de mettre à jour votre pod, que se passe-t-il ? Pourquoi ?
__REPONSE__

### 4.3 Générez un fichier de configuration pour une ConfigMap puis créez-la.
- Nom `color-config`
- fichier color.config.yaml
- Définissez-y la variable `COLOR` à `green`
```sh
__COMMANDE
```

### 4.4 Modifiez votre fichier color.pod.yaml pour y utiliser la ConfigMap que vous venez de créer. Forcez la mise à jour si besoin. 
```yaml
__MODIFICATIONS__
```