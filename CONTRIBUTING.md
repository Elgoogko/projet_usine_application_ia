# Contribuer à usine-4.0

## Table des matières

- J'ai une question
  - Je veux contribuer
  - Signaler des bugs
  - Suggérer des améliorations
  - Votre première contribution de code
  - Améliorer la documentation
- Guides de style
  - Messages de commit
- Rejoindre l'équipe du projet


## J'ai une question

> Si vous voulez poser une question, nous supposons que vous avez lu la Documentation disponible.

Avant de poser une question, il est préférable de rechercher dans les [Issues](/issues) existantes celles qui pourraient vous aider. Si vous avez trouvé une issue pertinente et avez besoin de précisions, vous pouvez écrire votre question dans cette issue. Il est également conseillé de d'abord chercher des réponses sur internet.

Si malgré tout vous ressentez le besoin de poser une question et d'obtenir des précisions, nous recommandons ce qui suit :

- Ouvrir une [Issue](/issues/new).
- Fournir autant de contexte que possible sur ce que vous rencontrez.
- Indiquer les versions du projet et de la plateforme (Python, uv, PyTorch, etc.), selon ce qui semble pertinent.

Nous nous occuperons de l'issue dès que possible.

<!--
Vous pouvez créer une étiquette d'issue séparée pour les questions et l'inclure dans cette description. Les contributeurs pourront alors étiqueter leurs issues en conséquence.

Selon la taille du projet, vous pouvez externaliser les questions, par exemple vers Stack Overflow ou Gitter. Vous pouvez ajouter des moyens de contact et d'information supplémentaires :
- IRC
- Slack
- Gitter
- Tag Stack Overflow
- Blog
- FAQ
- Roadmap
- Liste de diffusion
- Forum
-->

## Je veux contribuer

> ### Avertissement légal <!-- omit in toc -->
> En contribuant à ce projet, vous acceptez que vous avez rédigé 100 % du contenu, que vous détenez les droits nécessaires sur ce contenu et que le contenu que vous proposez peut être publié sous la licence du projet.

### Signaler des bugs

<!-- omit in toc -->
#### Avant de soumettre un rapport de bug

Un bon rapport de bug ne devrait pas obliger les autres à vous relancer pour obtenir plus d'informations. Par conséquent, nous vous demandons d'investiguer soigneusement, de rassembler les informations et de décrire le problème en détail dans votre rapport. Merci de suivre les étapes suivantes en amont pour nous aider à corriger tout bug potentiel le plus rapidement possible.

- Assurez-vous d'utiliser la dernière version.
- Déterminez s'il s'agit vraiment d'un bug et non d'une erreur de votre part, par exemple l'utilisation de composants/versions d'environnement incompatibles (assurez-vous d'avoir lu la documentation. Si vous cherchez du support, consultez cette section).
- Pour voir si d'autres utilisateurs ont rencontré (et potentiellement déjà résolu) le même problème que vous, vérifiez qu'il n'existe pas déjà un rapport de bug pour votre bug ou erreur dans le [bug tracker](/issues?q=label%3Abug).
- Assurez-vous également de rechercher sur internet (y compris Stack Overflow) pour voir si des utilisateurs en dehors de la communauté GitHub ont discuté du problème.
- Rassemblez les informations sur le bug :
  - Trace d'appels (Traceback)
  - OS, plateforme et version (Windows, Linux, macOS, x86, ARM)
  - Version de l'interpréteur, du compilateur, du SDK, de l'environnement d'exécution, du gestionnaire de paquets, selon ce qui semble pertinent.
  - Éventuellement votre entrée et la sortie obtenue
  - Pouvez-vous reproduire le problème de manière fiable ? Et pouvez-vous également le reproduire avec des versions antérieures ?

<!-- omit in toc -->
#### Comment soumettre un bon rapport de bug ?

> Vous ne devez jamais signaler de problèmes de sécurité, de vulnérabilités ou de bugs incluant des informations sensibles dans le tracker d'issues, ni ailleurs en public. À la place, les bugs sensibles doivent être envoyés par e-mail à <barijoris.boicos@gmail.com>.
<!-- Vous pouvez ajouter une clé PGP pour permettre l'envoi de messages chiffrés. -->

Nous utilisons les issues GitHub pour suivre les bugs et erreurs. Si vous rencontrez un problème avec le projet :

- Ouvrez une [Issue](/issues/new). (Comme nous ne pouvons pas savoir à ce stade s'il s'agit d'un bug ou non, nous vous demandons de ne pas encore parler de bug et de ne pas étiqueter l'issue.)
- Expliquez le comportement attendu et le comportement observé.
- Merci de fournir autant de contexte que possible et de décrire les *étapes de reproduction* qu'une autre personne peut suivre pour recréer le problème de son côté. Cela inclut généralement votre code. Pour de bons rapports de bug, vous devriez isoler le problème et créer un cas de test réduit.
- Fournissez les informations collectées dans la section précédente.

Une fois l'issue créée :

- L'équipe du projet étiquettera l'issue en conséquence.
- Un membre de l'équipe essaiera de reproduire le problème avec les étapes que vous avez fournies. S'il n'y a pas d'étapes de reproduction ou pas de moyen évident de reproduire le problème, l'équipe vous demandera ces étapes et marquera l'issue comme `needs-repro`. Les bugs avec l'étiquette `needs-repro` ne seront pas traités tant qu'ils n'auront pas été reproduits.
- Si l'équipe parvient à reproduire le problème, il sera marqué `needs-fix`, ainsi que éventuellement d'autres étiquettes (comme `critical`), et l'issue sera laissée pour être implémentée par quelqu'un.

<!-- Vous pouvez créer un modèle d'issue pour les bugs et erreurs qui servira de guide et définira la structure des informations à inclure. Si vous le faites, référencez-le ici dans la description. -->


### Suggérer des améliorations

Cette section vous guide dans la soumission d'une suggestion d'amélioration pour usine-4.0, **y compris les fonctionnalités entièrement nouvelles et les améliorations mineures des fonctionnalités existantes**. Suivre ces recommandations aidera les mainteneurs et la communauté à comprendre votre suggestion et à trouver les suggestions liées.

<!-- omit in toc -->
#### Avant de soumettre une amélioration

- Assurez-vous d'utiliser la dernière version.
- Lisez attentivement la documentation et vérifiez si la fonctionnalité est déjà couverte, peut-être par une configuration individuelle.
- Effectuez une [recherche](/issues) pour voir si l'amélioration a déjà été suggérée. Si c'est le cas, ajoutez un commentaire à l'issue existante au lieu d'en ouvrir une nouvelle.
- Déterminez si votre idée correspond au périmètre et aux objectifs du projet. Il vous appartient d'étayer solidement votre dossier pour convaincre les développeurs du projet des mérites de cette fonctionnalité. Gardez à l'esprit que nous voulons des fonctionnalités utiles à la majorité de nos utilisateurs et pas seulement à un petit sous-ensemble. Si vous ciblez uniquement une minorité d'utilisateurs, envisagez d'écrire une bibliothèque complémentaire/plugin.

<!-- omit in toc -->
#### Comment soumettre une bonne suggestion d'amélioration ?

Les suggestions d'amélioration sont suivies sous forme d'[issues GitHub](/issues).

- Utilisez un **titre clair et descriptif** pour l'issue afin d'identifier la suggestion.
- Fournissez une **description étape par étape de l'amélioration suggérée** avec autant de détails que possible.
- **Décrivez le comportement actuel** et **expliquez le comportement que vous attendiez à la place** et pourquoi. À ce stade, vous pouvez aussi indiquer les alternatives qui ne vous conviennent pas.
- Vous pouvez **inclure des captures d'écran ou des enregistrements d'écran** qui vous aident à démontrer les étapes ou à montrer la partie concernée par la suggestion. Vous pouvez utiliser [LICEcap](https://www.cockos.com/licecap/) pour enregistrer des GIF sur macOS et Windows, et l'[enregistreur d'écran intégré à GNOME](https://help.gnome.org/users/gnome-help/stable/screen-shot-record.html.fr) ou [SimpleScreenRecorder](https://github.com/MaartenBaert/ssr) sur Linux. <!-- cette partie ne doit être incluse que si le projet possède une interface graphique -->
- **Expliquez en quoi cette amélioration serait utile** à la plupart des utilisateurs d'usine-4.0. Vous pouvez également mentionner d'autres projets qui l'ont mieux résolu et qui pourraient servir d'inspiration.

<!-- Vous pouvez créer un modèle d'issue pour les suggestions d'amélioration qui servira de guide et définira la structure des informations à inclure. Si vous le faites, référencez-le ici dans la description. -->

### Améliorer la documentation
<!-- TODO
Mise à jour, amélioration et correction de la documentation

-->

## Guides de style
### Messages de commit
<!-- TODO

-->

<!-- omit in toc -->
## Attribution
Ce guide est basé sur le [contributing.md](https://contributing.md/generator) !