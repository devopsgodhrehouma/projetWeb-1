### Tutoriel : Déployer un Projet **Docusaurus** avec CI/CD sur AWS Amplify (Pour Débutants)

Ce tutoriel vous guidera, étape par étape, pour déployer un site **Docusaurus** existant avec **AWS Amplify** et mettre en place une plateforme CI/CD. **Idéal pour débutants**, tout est expliqué pour que vous puissiez copier-coller facilement.

---

## **Prérequis**

1. **Un projet Docusaurus existant** :  
   Assurez-vous que votre projet Docusaurus contient déjà :
   - Un fichier `package.json` avec les scripts nécessaires (`npm install`, `npm run build`).
   - Un dossier de code source (`src`) et un fichier `docusaurus.config.js`.

2. **Compte AWS** :  
   Créez un compte gratuit sur [AWS](https://aws.amazon.com/free/).

3. **Compte GitHub/GitLab** :  
   Hébergez le projet Docusaurus sur GitHub ou GitLab.

4. **Node.js installé** :  
   Installez Node.js sur votre machine en suivant [ce lien](https://nodejs.org/).

---

## **Étape 1 : Préparer le projet Docusaurus**

1. **Cloner le projet existant** (si nécessaire) :
   ```bash
   git clone <URL_DU_DÉPÔT>
   cd <NOM_DU_PROJET>
   ```

2. **Installer les dépendances** :
   ```bash
   npm install
   ```

3. **Tester localement** (optionnel mais recommandé) :
   Lancer un serveur local pour vérifier que le projet fonctionne :
   ```bash
   npm run start
   ```
   Ouvrez [http://localhost:3000](http://localhost:3000) pour vérifier.

4. **Construire le site statique** :
   Construisez le site statique qui sera déployé sur Amplify :
   ```bash
   npm run build
   ```
   Cela génère un dossier `build/` contenant les fichiers prêts à être déployés.

---

## **Étape 2 : Configurer AWS Amplify**

1. **Accéder à AWS Amplify** :  
   Connectez-vous à votre compte AWS et accédez à la console **Amplify** :  
   [AWS Amplify Console](https://console.aws.amazon.com/amplify/).

2. **Créer une nouvelle application Amplify** :
   - Cliquez sur **Get Started** dans la section "Host your web app".
   - Sélectionnez **Connect a repository** pour lier votre projet Docusaurus hébergé sur GitHub ou GitLab.

3. **Lier votre dépôt** :
   - Autorisez AWS Amplify à accéder à votre compte GitHub/GitLab.
   - Sélectionnez le **dépôt** et la **branche** contenant votre projet Docusaurus.

4. **Configurer les étapes CI/CD** :  
   Une fois votre dépôt connecté, AWS Amplify détectera automatiquement un fichier `package.json` et configurera les commandes de build et déploiement.

   Si besoin, modifiez les commandes dans la configuration Amplify :
   - **Commandes pour l'installation des dépendances** :
     ```bash
     npm install
     ```
   - **Commandes pour le build** :
     ```bash
     npm run build
     ```
   - **Répertoire de sortie** :
     ```
     build
     ```

5. **Lancer le déploiement** :  
   Cliquez sur **Save and Deploy** pour démarrer le processus CI/CD. Amplify :
   - Installe les dépendances.
   - Construit le projet.
   - Déploie automatiquement le site.

6. **Accéder à l'URL** :  
   Une fois le déploiement terminé, Amplify fournit une URL comme :  
   ```
   https://<randomstring>.amplifyapp.com
   ```
   Votre site est maintenant en ligne !

---

## **Étape 3 : Configurer CI/CD pour chaque mise à jour**

AWS Amplify configure automatiquement le CI/CD : chaque fois que vous poussez une modification sur la branche associée (ex. `main`), Amplify :
1. Récupère le nouveau code.
2. Reconstruit le site.
3. Met à jour automatiquement le site en ligne.

Pour tester :
1. Faites une modification dans votre projet local.
2. Poussez vos modifications :
   ```bash
   git add .
   git commit -m "Mise à jour du contenu"
   git push origin main
   ```
3. Amplify déclenche automatiquement le pipeline CI/CD.

---

## **Étape 4 : Optimisation SEO avec AWS Amplify**

Pour un site optimisé SEO :
1. **Activer les redirections** :  
   Créez un fichier `amplify.yml` à la racine pour gérer les redirections :
   ```yaml
   redirects:
     - source: </:path*> # Pour les routes Docusaurus
       target: /index.html
       status: 200
   ```

2. **Configurer un domaine personnalisé (optionnel)** :  
   - Si vous possédez un domaine, connectez-le à Amplify via l'onglet **Domain management**.
   - Amplify génère automatiquement des certificats SSL pour sécuriser le site (HTTPS).

---

## **Étape 5 : Publicité avec Google AdSense**

1. **Créer un compte Google AdSense** :  
   Rendez-vous sur [AdSense](https://www.google.com/adsense/) et suivez les étapes pour configurer votre site.

2. **Ajouter le script AdSense dans Docusaurus** :
   Modifiez le fichier `docusaurus.config.js` pour ajouter le script AdSense dans `<head>` :
   ```javascript
   module.exports = {
     themeConfig: {
       ...
     },
     scripts: [
       {
         src: 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js',
         async: true,
       },
     ],
   };
   ```

3. **Intégrer les annonces AdSense** :  
   Ajoutez des blocs d'annonces où nécessaire dans vos pages :
   ```html
   <ins class="adsbygoogle"
        style="display:block"
        data-ad-client="ca-pub-xxxxxxxxxxxxxxxx"
        data-ad-slot="1234567890"
        data-ad-format="auto"
        data-full-width-responsive="true"></ins>
   <script>
     (adsbygoogle = window.adsbygoogle || []).push({});
   </script>
   ```

---

## **Étape 6 : Résolution des problèmes courants**

1. **Erreur de build sur Amplify** :  
   Si Amplify échoue à construire votre projet, vérifiez les versions de Node.js. Ajoutez un fichier `.nvmrc` dans la racine de votre projet :
   ```
   18
   ```

2. **Erreur 404 pour des pages spécifiques** :  
   Assurez-vous que le fichier `amplify.yml` contient des redirections comme décrit précédemment.

---

## **Étape 7 : Points Bonus**

- **Utiliser l’environnement staging** :  
   AWS Amplify permet de créer des environnements multiples (staging, production) pour tester vos modifications avant de les publier.

- **Surveiller les performances** :  
   Utilisez les outils intégrés Amplify pour suivre les performances et optimiser le temps de chargement.

---

## **Résumé**

- **AWS Amplify** est idéal pour héberger un site **Docusaurus** avec CI/CD.
- Chaque modification poussée dans votre dépôt est automatiquement mise en production.
- Avec un tutoriel pas à pas, les débutants peuvent facilement suivre et déployer leur projet.

----------



## Prérequis

Avant de commencer, assurez-vous d'avoir :

1. Un compte AWS
2. Un projet Docusaurus existant sur un dépôt Git (GitHub, GitLab, etc.)
3. Git installé sur votre machine locale
4. Node.js installé sur votre machine locale

## Étape 1 : Connexion à la console AWS

1. Ouvrez votre navigateur et allez sur la page de connexion AWS.
2. Cliquez sur "Utilisateur IAM" (il est recommandé de ne pas utiliser le compte racine).
3. Saisissez l'ID ou l'alias de votre compte, puis cliquez sur "Suivant".
4. Entrez votre nom d'utilisateur IAM et votre mot de passe.
5. Cliquez sur "Connexion"[2].

## Étape 2 : Accéder à AWS Amplify

1. Une fois connecté à la console AWS, cherchez "Amplify" dans la barre de recherche.
2. Cliquez sur "AWS Amplify" dans les résultats de recherche[2].

## Étape 3 : Démarrer avec AWS Amplify

1. Sur la page d'accueil d'AWS Amplify, cliquez sur "Get started" sous "Host your web app"[2].

## Étape 4 : Connecter votre dépôt Git

1. Choisissez votre fournisseur Git (GitHub, GitLab, etc.).
2. Cliquez sur "Continue".
3. Si c'est la première fois que vous connectez ce fournisseur Git à AWS Amplify, vous devrez autoriser l'accès. Suivez les instructions à l'écran pour vous connecter à votre compte Git et autoriser AWS Amplify[2].

## Étape 5 : Configurer le projet

1. Sélectionnez le dépôt contenant votre projet Docusaurus.
2. Choisissez la branche que vous souhaitez déployer (généralement "main" ou "master").
3. Cliquez sur "Next"[2].

## Étape 6 : Configurer les paramètres de build

1. AWS Amplify tentera de détecter automatiquement les paramètres de build. Vérifiez-les attentivement.
2. Assurez-vous que le "baseDirectory" est défini sur "/build" pour Docusaurus.
3. Voici un exemple de configuration `amplify.yml` pour Docusaurus :

```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - yarn install
    build:
      commands:
        - yarn build
  artifacts:
    baseDirectory: build
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*
```

4. Cliquez sur "Next"[1][3].

## Étape 7 : Vérifier et déployer

1. Vérifiez tous les paramètres une dernière fois.
2. Cliquez sur "Save and deploy"[2].

## Étape 8 : Suivre le déploiement

1. AWS Amplify va maintenant lancer le pipeline CI/CD avec trois étapes :
   - Provisionnement de l'environnement de build
   - Build de l'application
   - Déploiement
2. Vous pouvez suivre la progression de ces étapes dans la console AWS Amplify[2].

## Étape 9 : Accéder à votre site déployé

1. Une fois le déploiement terminé, AWS Amplify fournira un URL pour votre site.
2. Cliquez sur cet URL pour voir votre site Docusaurus en direct[3].

## Étape 10 : Configurer un domaine personnalisé (optionnel)

1. Dans la console AWS Amplify, allez dans "Domain Management".
2. Suivez les instructions pour ajouter et vérifier la propriété de votre domaine.
3. AWS Amplify fournira également un certificat SSL pour votre domaine[3].

## Utilisation continue

Désormais, chaque fois que vous pousserez des modifications sur la branche configurée de votre dépôt Git, AWS Amplify déclenchera automatiquement un nouveau build et déploiement de votre site Docusaurus.

Ce tutoriel vous permet de mettre en place une plateforme CI/CD robuste pour votre projet Docusaurus existant en utilisant AWS Amplify. N'hésitez pas à explorer les options supplémentaires offertes par AWS Amplify pour personnaliser davantage votre workflow de déploiement.

