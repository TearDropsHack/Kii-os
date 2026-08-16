Une mise à jour a cassé quelque chose ? Reviens à la version précédente avec `bootc rollback`
`ujust changelogs` résume les changements de paquets depuis la dernière mise à jour
`ujust update` met à jour le système, les Flatpaks et Homebrew en une seule commande
`brew search` puis `brew install` pour les outils en ligne de commande — Kii-OS gère les mises à jour tout seul
`ujust bbrew` propose des sélections d'outils prêtes à l'emploi (dev, terminal, bureau)
`Ctrl`-`Alt`-`T` ouvre un terminal instantanément
`ujust --choose` affiche chaque raccourci avec le script qu'il exécute
`ujust -n nom_de_recette` permet de prévisualiser une recette avant de la lancer
`tldr ls` donne l'essentiel d'une commande en 10 secondes (`brew install tealdeer` pour l'installer)
Sauvegarde tes paquets Homebrew et tes Flatpaks avec `brew bundle dump`
Streaming et jeu à distance : `ujust setup-sunshine` installe et configure l'hôte Sunshine
Tablette graphique ? `ujust install-opentabletdriver` installe un pilote libre et configurable
`ujust install-fonts` installe des polices de qualité, dont les Nerd Fonts pour ton terminal
Un Flatpak s'est cassé ? Warehouse permet de revenir à une version antérieure de l'application
Ajuste finement les permissions de tes Flatpaks avec Flatseal plutôt qu'en désactivant le bac à sable
Le système est immuable : installe tes outils de développement dans un conteneur avec `distrobox create`
Tes conteneurs de développement sont portables — ils fonctionnent à l'identique ailleurs
`ujust rebase-helper` permet de revenir à une image précise ou de changer de canal
`ujust check-local-overrides` repère les modifications locales qui pourraient gêner une mise à jour
`ujust toggle-updates` active ou désactive les mises à jour automatiques en arrière-plan
Carte Nvidia et Secure Boot activé ? `ujust enroll-secure-boot-key` enrôle la clé de signature des pilotes
`ujust toggle-tpm2` déverrouille automatiquement ton disque chiffré via le TPM
`ujust toggle-tailscale` monte un réseau privé entre tes machines en quelques secondes
`ujust benchmark` lance un test système d'une minute, `ujust device-info` récapitule ta configuration
`ujust clean-system` fait le ménage dans les images, caches et paquets inutilisés
Change de shell dans les réglages du terminal plutôt que globalement — le système reste sain
KDE Plasma fait tourner ton bureau, pense à [soutenir le projet](https://kde.org/donate)
Une idée, un bug, une question ? Tout se passe sur [le dépôt Kii-OS](https://github.com/TearDropsHack/Kii-os)
