# TP5 – Réponses

Run complet et vert (lint, build → test) : https://github.com/belgasmeriem/python-fastapi-app/actions/runs/42283067078

**Q0.** Le code est dans `app/`, les tests dans `tests/`, les dépendances de dev dans `requirements-dev.txt`, et oui il existe un dossier `.github`.

**Q1.** `branches: [main, 'feature/**']`, `paths: ['app/**', 'tests/**']`, `types: [opened, synchronize]` (voir `01-filtres.yml`).

**Q2.** Modifier seulement le README ne lance pas Filtres : aucun fichier modifié ne correspond à `paths`. Modifier un fichier de `app/` lance Filtres.

**Q3.** ET entre `branches` et `paths` (les deux filtres doivent correspondre). OU entre les valeurs d'une même liste, donc entre deux types d'activité. Sans `paths` sous `pull_request`, Filtres se lance pour toute PR.

**Q4.** `tag.yml` se déclenche uniquement avec `tags: ['v*']`. Le tag `v1.0.0` a lancé le workflow Tag.

**Q5.** `uses: actions/checkout@v4`, `uses: actions/setup-python@v5` avec `python-version: '3.13'`, `run: pip install -r requirements.txt -r requirements-dev.txt`, et `needs: [lint, build]` pour le job test.

**Q6.** Sans `needs`, les trois jobs démarrent en parallèle et la durée totale est plus courte. Avec `needs`, test attend lint et build. Avec une erreur de lint (`import os` inutilisé), lint échoue et test est ignoré (skipped).

**Q7.** Chaque job s'exécute sur un runner neuf et isolé, sans le code ni Python : il faut refaire checkout et setup-python.

**Q8.** Nom de l'app : `env.APP_NAME` ; acteur : `github.actor` ; événement : `github.event_name` ; branche : `github.ref_name` ; SHA : `github.sha` ; OS du runner : `runner.os`. J'ai limité `APP_NAME` au step d'affichage : définie au niveau du workflow, elle écrasait la valeur par défaut de `Settings` et faisait échouer `test_settings_default_values`.

**Q9.** Sur un push : `event_name` = `push`, `head_ref` et `base_ref` sont vides, `ref_name` = `feature/tp-ci`. Sur une PR : `event_name` = `pull_request`, `head_ref` = `feature/tp-ci`, `base_ref` = `main`, `ref_name` = `1/merge`.

**Q10.** Dans `toJson(github)` lors d'un push, le message est dans `event.head_commit.message` ("ci: ajoute pull_request"). Sur un `pull_request`, `head_commit` ne contient pas de message : seul le titre de la PR est fourni.