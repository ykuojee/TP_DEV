# TP 02 — Réalisation des 41 étapes

Projet Flask avec templates Jinja et compilation Tailwind CSS 4.
Les étapes Windows sont des alternatives à celles de macOS. Les déplacements
globaux et les modifications du profil shell ont été remplacés par une installation locale.

## Lancer le projet

Depuis ce dossier, lancer Flask dans un premier terminal :

```bash
.tools/bin/poetry run python app.py
```

Ouvrir http://127.0.0.1:5000/.
Pour recompiler automatiquement les styles, ouvrir un deuxième terminal dans ce dossier :

```bash
npm run watch:css
```

Pour une compilation ponctuelle : `npm run build:css`.
Arrêter chaque processus avec Ctrl+C.

## Corrigé et correspondance des 41 étapes

| N° | Réalisation / réponse |
| --- | --- |
| 1 | Les certificats Python ne doivent être réinstallés qu'en cas de problème SSL. La commande du sujet vise Python 3.14 ; ce Mac utilise Python 3.13. Ne pas exécuter un chemin de version inexistant. |
| 2 | Poetry installé dans `.tools` avec `python3 -m venv .tools`, puis `.tools/bin/python -m pip install poetry`. |
| 3 | Utiliser `.tools/bin/poetry` depuis le projet ; aucune modification de `~/.zshrc` nécessaire. Pour une commande abrégée dans le terminal courant : `export PATH="$PWD/.tools/bin:$PATH"`. |
| 4 | Vérifier avec `.tools/bin/poetry --version`. |
| 5 | Tailwind 4 et son CLI sont déclarés dans `package.json`. Installer avec `npm install`. Avec Tailwind 4, le CLI npm est fourni par `@tailwindcss/cli`. |
| 6 | Le binaire autonome constitue une alternative à npm ; cette réalisation utilise npm. |
| 7 | `chmod +x` concerne uniquement le binaire autonome ; inutile avec npm. |
| 8 | Afficher l'aide : `npx tailwindcss --help`. Utiliser deux tirets ASCII. |
| 9 | La version apparaît dans `npx tailwindcss --help`. Le nom de commande est en minuscules. |
| 10 | Le CLI local se trouve dans `node_modules/.bin/`, plutôt que dans `~/.local/bin/`. |
| 11 | Aide locale : `./node_modules/.bin/tailwindcss --help`. |
| 12 | Aucun déplacement avec `sudo` nécessaire : les scripts npm trouvent automatiquement le CLI local. |
| 13 | Dossier `PROJECT-10` créé dans `TP_DEV_IA`. |
| 14 | Projet Poetry initialisé par le fichier `pyproject.toml`, équivalent au résultat de `poetry init`. |
| 15 | Métadonnées : nom `project-10`, auteur `Utilisateur`, version `0.1.0`. Le mode paquet est désactivé pour cette application simple. |
| 16 | `ls` affiche notamment `pyproject.toml` et, après résolution des dépendances, `poetry.lock`. |
| 17 | Lire la configuration : `cat pyproject.toml`. |
| 18 | Flask `2.3.3` déclaré dans les dépendances Poetry. |
| 19 | OpenAI `0.27.10` déclaré conformément à la version du sujet. L'ajout de `openai@latest` est une alternative qui remplace cette version ; ne pas exécuter les deux successivement pour reproduire le TP. Aucun appel API n'est requis ici. |
| 20 | `python-dotenv` `1.0.0` déclaré ; aucune clé API n'est nécessaire pour afficher la page. |
| 21 | Ouvrir ce dossier dans PyCharm via File > Open. Cette manipulation de l'IDE reste à effectuer si vous souhaitez utiliser PyCharm. |
| 22 | Dans les réglages de l'interpréteur PyCharm, sélectionner l'interpréteur existant `.venv/bin/python`. Si l'assistant demande Poetry, fournir le chemin absolu vers `.tools/bin/poetry` dans ce dossier. |
| 23 | `app.py` crée Flask et la route `/`. La première version pédagogique renvoie `Hello World!` ; la version finale renvoie le template, conformément à l'étape 29. Lancement : `.tools/bin/poetry run python app.py`. Le plugin shell est facultatif. |
| 24 | Adresse locale : http://127.0.0.1:5000/. |
| 25 | Dossier `templates` et fichier `index.html` créés. |
| 26 | Structure HTML5 définie avec `<!doctype html>`. |
| 27 | Document HTML avec langue française, UTF-8, viewport, titre et contenu. |
| 28 | Import de `Flask` et `render_template` dans `app.py`. |
| 29 | `home()` renvoie `render_template("index.html")`. |
| 30 | La route sert la page HTML après démarrage de Flask. |
| 31 | Dossier `static/css` créé. |
| 32 | Fichier `static/css/input.css` créé avec `@import "tailwindcss";`. |
| 33 | La compilation intermédiaire vers `output.css` peut se faire avec `npx tailwindcss -i ./static/css/input.css -o ./static/css/output.css --watch`. Le projet utilise directement le chemin final de l'étape 39. |
| 34 | La balise `link` utilise Jinja et `url_for('static', ...)` pour charger le CSS. |
| 35 | Le titre contient `text-3xl font-bold text-blue-600` et le texte Lorem du sujet. |
| 36 | Les anciennes directives `@tailwind base`, `@tailwind components`, `@tailwind utilities` correspondent à Tailwind 3 ; elles ne sont pas ajoutées au projet Tailwind 4. |
| 37 | Import unique Tailwind 4 présent dans `input.css`. |
| 38 | `@source "../../templates";` présent : le chemin part de `static/css/input.css`. |
| 39 | `npm run watch:css` génère `static/dist/css/style.css` et surveille les changements. `npm run build:css` compile une seule fois. |
| 40 | Correction de la coquille du sujet : le lien final est `url_for('static', filename='dist/css/style.css')`, puisque l'étape 39 écrit dans `static/dist/css/style.css`. |
| 41 | Avec le mode watch actif, modifier ou retirer `text-blue-600`, enregistrer puis actualiser le navigateur : le titre change de couleur. Tailwind régénère le CSS ; en mode watch, certaines règles déjà détectées peuvent rester dans le fichier. Une compilation propre permet de vérifier l'élimination des classes inutilisées. |

## Réinstaller les dépendances

```bash
python3 -m venv .tools
.tools/bin/python -m pip install poetry==2.5.1
POETRY_VIRTUALENVS_IN_PROJECT=true .tools/bin/poetry install
npm ci
npm run build:css
```

Les fichiers de verrouillage fixent les versions résolues. Ne pas publier `.env`,
`.tools`, `.venv` ou `node_modules` dans Git.

## Vérifications effectuées

- Poetry 2.5.1 ; dépendances installées dans `.venv` et verrouillées.
- Tailwind 4.3.3 ; compilation CSS réussie.
- Route `/` : HTTP 200 avec le template et le chemin CSS attendus, via le client de test Flask.
- Fichier `/static/dist/css/style.css` : HTTP 200 ; classes `text-3xl`, `font-bold` et `text-blue-600` présentes.
- Les manipulations de PyCharm et la démonstration interactive en mode watch sont expliquées ci-dessus ; elles n'ont pas été exécutées dans l'interface.
