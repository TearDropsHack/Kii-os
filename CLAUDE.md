# Kii-OS — guide du dépôt

## Le projet en une phrase

**Kii-OS** est un système d'exploitation Linux **atomique** et **souverain**, construit
par-dessus **Aurora** (Universal Blue, KDE Plasma) à l'aide de l'outil **BlueBuild**,
puis publié comme image de conteneur sur GHCR.

- Dépôt : `TearDropsHack/Kii-os`
- Image publiée : `ghcr.io/teardropshack/kii-os:latest`
- Base : `ghcr.io/ublue-os/aurora:stable` (Fedora Atomic + KDE Plasma)
- Auteur : HandKii

## Architecture : comment une idée devient un OS

```
recipes/recipe.yml          ← on décrit CE QU'ON VEUT (déclaratif, YAML)
files/  modules/            ← les fichiers et scripts que la recette injecte
        │
        ▼  git push
.github/workflows/build.yml ← GitHub Actions lance blue-build/github-action
        │
        ▼  build + signature cosign
ghcr.io/teardropshack/kii-os:latest   ← image de conteneur OCI publiée
        │
        ▼  bootc / rpm-ostree sur la machine
La VM ou le PC démarre sur cette image (mise à jour = nouvelle image)
```

Point clé pour débutant : **on ne modifie jamais le système à la main**. On modifie la
recette, on pousse, la CI reconstruit l'image, et la machine se met à jour dessus.
Toute retouche manuelle sur la VM sera perdue à la prochaine mise à jour.

### Carte du dépôt

| Chemin | Rôle |
| --- | --- |
| `recipes/recipe.yml` | La recette principale : base, paquets, flatpaks, modules |
| `files/system/` | Arborescence copiée telle quelle dans `/` de l'image |
| `files/scripts/` | Scripts exécutés pendant le build (module `script`) |
| `modules/` | Modules BlueBuild personnalisés (vide pour l'instant) |
| `.github/workflows/build.yml` | La CI qui construit et publie l'image |
| `cosign.pub` | Clé publique de vérification de signature — **NE JAMAIS TOUCHER** |
| `.claude/agents/` | Les sous-agents spécialisés du projet |

Référence des modules BlueBuild : <https://blue-build.org/reference/modules/>

## Règles d'or (non négociables)

1. **Délégation systématique.** Chaque chantier passe par le sous-agent compétent —
   `architecte` (recette / modules / bootc), `designer` (KDE / branding),
   `qa` (builds / logs / vérifications), `scribe` (docs). Puis synthèse.
2. **Un changement = un commit = un build VERT.** On vérifie avec `gh run watch`
   avant d'enchaîner. **Jamais deux chantiers dans un même commit.**
3. **Phase risquée = PLAN court soumis à validation humaine AVANT d'implémenter.**
4. **Interdiction absolue** de créer, modifier, déplacer ou supprimer :
   `cosign.pub`, toute clé privée, tout secret, tout fichier de signature.
   Le module `signing` de la recette reste en place.
5. **Ressources libres uniquement.** Thèmes, icônes, polices, fonds d'écran : licence
   libre et redistribuable vérifiée avant intégration.
6. **Tout passe par la recette.** Zéro bidouille manuelle sur la machine de test.
7. **Fin de phase = « RAPPORT RÉGIE »** copiable : 1) changements, 2) état du build,
   3) problèmes, 4) suite proposée.
8. **Français simple.** L'utilisateur est débutant : explications courtes, pas de jargon
   non expliqué.

## Commandes utiles

```bash
# Suivre le dernier build
gh run watch $(gh run list --limit 1 --json databaseId -q '.[0].databaseId')

# Lister les builds récents
gh run list --limit 5

# Déclencher un build manuellement
# (indispensable si le commit ne touche QUE des fichiers .md :
#  le workflow ignore les *.md en push)
gh workflow run bluebuild

# Voir les logs d'un build en échec
gh run view <ID> --log-failed
```

## Pièges connus

- Le workflow a `paths-ignore: ["**.md"]` : un commit purement documentaire **ne
  déclenche pas** de build. Utiliser `gh workflow run bluebuild`.
- Le nom de l'image dans `recipe.yml` doit être en **minuscules** (registre OCI).
- Sur une image atomique, `/etc` est modifiable mais `/usr` est en lecture seule au
  runtime : les fichiers de personnalisation système vont dans l'image, pas sur la
  machine.
