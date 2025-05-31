4.2	Refonte du module de procédure 
4.2.1	Définition de la mission

4.2.1.1	Contexte général 

L’entreprise Hutchinson est un groupe d’industriel Filiale de TotalEnergies et spécialisé dans la fabrication de solutions multi-matériaux. Leader mondial dans la transformation d’élastomères ils fournissent des secteurs comme l’automobile, l’aéronautique ou l’énergie . Leurs produits incluent des systèmes antivibratoire, des solutions d’étanchéité et des systèmes de gestion des fluides . 
Dans la continuité de leurs stratégie d’amélioration continue, Hutchinson cherche à harmoniser ses processus internes. Leur objectif est donc de crée un référentiel de procédures standardisées tout en permettant des adaptations spécifiques dans les sites de productions. 
PICC étant en discussion avec l’entreprise Hutchinson pour lui vendre notre solution, cette dernière souhaite développer certaines partie du logiciel pour réponde à ses besoins. Ainsi, le module de gestion des procédures sera remanié pour qu’il soit à la fois standardisé et adaptable. Cela permettra de facilité la diffusion et l’application des meilleurs pratiques au sein du groupe. Les enjeux de cette mission seront donc : 

-	D’Assurer la cohérence des procédure au niveau du group tout en respectant les particularités locales 
-	Permette une exécution collaborative des procédures avec une traçabilité et un suivie en temps réel
-	Facilité la mise à jour et l’évolution des procédures en fonctions des retour d’expérience 

4.2.1.2	Objectifs de la mission 


Après avoir analyse le besoin de notre future client Hutchinson nous avons définie une suite d’objectif pour répondre à ces attentes. Bien que le module de procédures soit déjà fonctionnel il incombe d’apporter les modifications suivante : 

-	Permettre de crée un référentiel commun à l’ensemble des site de production 
-	Crée un mécanisme d’héritage au sein des procédures permettant la modification des procédure locale et la mise à jour par rapport au procédure globales 
-	Amélioré la gestion des procédures en offrant une vue d’ensemble de toutes celles exécuté dans un contexte données 
-	Ajouter un mécanisme de synchronisation en temps réel 
-	Permettre de visualiser en un coup d’œil l’avancement les blocages 
-	Ajouter un system pour définir le rôle et la responsabilité de chacun vis-à-vis de chaque étapes d’une procédure
-	Permettre l’exécution partagé des procédures 
-	Ajouter un mécanisme de validation contrôlant les moments critique de l’exécution 

Ces modifications nous permettrons d’apporter clarté et uniformisation dans l’exécution des procédures non seulement pour l’entreprise Hutchinson mais aussi pour tout nos clients qui bénéficierons ce ces nouvelles fonctionnalités 

4.2.1.3	Organisation du projet 

Pour réaliser ce projet nous avons privilégié le cadre Agile qui nous permettais de rester au plus proche de l’attente de nos future client. Par le biais de Constant qui tenais le rôle de Product Owner nous avions la capacité d’ajuster le développement des fonctionnalités au fur et à mesure du projet.  La définition de nos rôle n’était pas canon face au cadre Agile : 

-	Constant Product Owner : donne la vision globale du projet ; est en contact direct avec le client ; réalise des tests de mise en situation réel ; propose des critiques sur le coté fonctionnel

-	Simon Scrum Master et Manager Opérationnel : Définit la liste des tâches, traduit les besoin en fonctionnalités, valide les choix technique ; aide le développer en cas de blocage.

-	Etienne Développer et Manager Opérationnel : Définit la liste des tâches, traduit le besoins en fonctionnalités, propose des solutions innovante. 

Les outils ainsi que la méthodologie de pilotage utilisé est définie dans la partie Organisation Interne de la présentation de l’entreprise (3.2.1 & 3.2.2). 

	


4.2.2	Choix techniques et justifications
4.2.2.1	Intégration de la matrice RASCI


Nous avons ajouté la matrice RASCI dans la définition de chaque étapes d’une procédure pour affiner la gestion des rôles attribué. Son objectif est de : 

-	Clarifier la responsabilité au plus petit niveau 
-	Garantir qu’une personne soit désigné comme responsable de chaque étape 
-	Permettre une exécution partagé mais contrôlé des procédures

La matrice est appliquée à chaque étape de la procédure, une étapes ne peut être complété que par un utilisateur désigné comme responsable. Les autres rôle sont moins exploité mais pourront à l’avenir avoir des droits spécifiques. 

Le rôles disponibles dans cette matrices sont : 

-	R – Responsible : Exécution de l’étape  
-	A – Accountable : validateur final ou garant du résultat
-	S – Support : Fournie des informations ou ressource 
-	C – Consulted : expert à consulté avant l’action 
-	I – Informed : reçoit des notification liées à l’étape 

En intégrant un outils du Leen management au cœur de notre module nous nous attendons à réduire les ambiguïté dans la gestions des connaissances pratique et a aligné les standards de qualité et de conformité de chaque site. C’est aussi un moyen efficace de d’encadrer un workflow qui peut être complexe une fois que l’exécution des procédure est autorisé. 


4.2.2.2	Utilisation de socket


A l’origine l’actualisation des états des procédures se faisait via une requête envoyé au server avec un intervalle régulier. Ce mécanisme nous a causé certains problème notamment en test avec les clients qui ne voyait pas apparaître immédiatement une procédure à laquelle il devrait pourtant avoir accès. Avec un besoin croissant dans ce module d’interconnectivité nous avons envisagé actualiser l’exécution des procédures via la socket client. Son objectif est de : 

-	Emmètre des évènements pour notifier les changements d’état des étapes de procédures 
-	Diffuser des mises à jour à tous les clients pour s’assurer que l’information affiché est cohérente 


Cette technologie permet d’améliorer l’expérience utilisateur grâce à des mise à jour instantané sans rafraichir la page ou attendre la fin de l’intervalle entre deux requêtes. C’est aussi une réduction de la charge pour le server qui subissait des requêtes répétitive de la part de tous les utilisateurs, même lorsqu’aucun avancement n’avait été fait dans l’exécution d’une procédure. Enfin, cela facilite la collaboration entre utilisateur puisque cette fonctionnalité nous a permit d’intégrer une vue dédié à l’avancement de toutes les procédures en cours. 

4.2.3	Méthodologie mise en œuvre 
4.2.4.1 Procédure désordonné et mécanisme de validation

Avant la refonte, les procédures s’exécutaient toujours de manière séquentiel. L’utilisateur devais compléter chaque étapes dans l’ordre de la première à la dernière sans pouvoir en laisser une seul pour plus tard. L’idée était d’apporté plus de souplesse dans l’exécution des procédures en permettant de compléter chaque étape dans n’importe quel ordre. 
	La modélisation des procédures se fait déjà sous forme de graphique orienté où chaque nœud est une étape et chaque arc la transition possible vers un autre nœud. Cette modélisation permet de générer des procédures complexes avec plusieurs embronchement et incluant des branches conditionnel. La validation est alors simple puisqu’il suffit d’avoir un chemin reliant la première étape à la dernier. De plus cette validation n’a pas lieu d’être codé explicitement puisque les contraintes d’une procédure exécuté séquentiellement, ne pas pouvoir faire de saut entre les étapes et être obligé de valider une étape pour passer à la suivante, permettent à elles seul d’être sûr de la validité d’une procédure une fois arrivé sur l’étape de fin. 

	L’ajout des procédures désordonné complique cette logique puisqu’il est possible de compléter l’étape de fin à n’importe quel moment de l’exécution. Il est aussi possible de valider une étapes dans une branche conditionnel avant d’avoir passé le nœud représentant la condition. 
	Nous avons donc utilisé l’algorithme de Parcours en Profondeur pour trouver tout les chemins possible entre le point de départ et le point d’arrivé. Nous aussi avons modifié cet algorithme pour qu’il exclue d’office tous les chemins ne comprenant pas l’étape courante, ce qui nous permet de réduire nos recherche au fur et à mesure de l’avancement de l’exécution. 
 
EXEMPLE D’EXECUTION D’UNE PROCEDURE 

Une fois la liste de chemin possible trouvé il nous faut chercher le chemin le plus court comprenant un maximum d’étapes valide. En cherchant le chemin le plus court, nous nous s’assurons que le chemin prédéfinie se rapproche le plus de celui que l’utilisateur empreinte actuellement. Si l’étape courante n’est plus dans liste des chemins possible, c’est que l’utilisateur a changé d’embronchement, il faut alors recalculer les chemins possible. 
Ce Mécanisme permet à chaque étapes de la procédure désordonne de définir un chemin allant de la première à la dernière étapes. Il est alors possible valider une procédure une fois que toutes les étapes de ce chemin sont validées. Cela permet également d’ajouter de nouvelles fonctionnalité comme un file d’Arianne, une liste des étapes et un pourcentage de complétion. Ces fonctionnalités sont fortement liées au chemin qu’emprunt l’utilisateur et sont amener à être modifié au fil de l’exécution de la procédure. En effet, en choisissant un chemin conditionnel le pourcentage de complétion diminue et la liste des étapes s’allonge. 


4.2.4.2 Amélioration des outils de gestions des procédures 

Avant la refonte, les procédures en cours d’exécution étaient affichées dans le panneau descriptif de l’entité procédure ainsi que dans la page d’accueil de l’utilisateur. Ce mécanisme ne permettait pas une gestion des exécutions par projet et pouvait même entrainer des surcharges d’éléments dans l’interface. 
Pour palier à ce problèmes nous avons crée une nouvelle entité dédiée à la gestion des procédures. Celle-ci permet d’affilié une liste de procédure pour ainsi suivre l’exécutions de toutes les procédures lancé depuis cette entité. 
 	 
GESTION DES INSTANTES DE PROCEDURES AVEC ET SANS GESTIONNAIRE DE PROCEDURE

Le gestionnaire de procédures permet de segmenter les différentes instances des chaque procédures. En effet, dans les procédures en cours, toutes les instances de cette procédures qui sont lancé simultanément sont affiché. Bien que chaque instance dispose d’un nom, il devient vite compliqué de s’y retrouver. En revanche dans les processus associé, seul les instances crée depuis cette interface apparaissent. 
De plus, la mise à jour par socket permet de synchroniser l’état des procédures en temps réel assurant la cohérence des informations et une vue d’ensemble plus sécurisé. 
Enfin des statuts ont été ajouté, ils permettent d’identifier en un coup d’œil les éventuel blocage sur une étape. Couplé à bar de progression de la procédure cette vue permet aux managers d’être plus réactif vis-à-vis de leurs équipes. 


4.2.4.3	Intégration de l’héritage dans les procédures

La mise en place d’héritage dans les procédures permet leurs standardisation et leurs adaptation. L’entreprise peut définir des procédures modèles et autorisé leur adaptation dans un contexte locales. C’est aussi un moyen de diminuer le nombre de doublon facilitant ainsi la maintenance de ces procédés standardisé. 

En pratique une procédure modèle ne diffère en rien d’une procédure classique. L’utilisateur devra crée une suite d’étape et de liens pour les relier. La relations parents enfant se crée lorsque cette procédure est copiée à partir d’un modèle. L’entité qui sera créé à la suite de cette évènement sera légèrement différents puisqu’elle bénéficie : 

-	D’élément graphique rappelant la provenance de chaque étape, local ou modèle
-	D’affichage fantomatique de la procédure modèle lorsque des étapes sont supprimé 
-	De bouton supplémentaire permettant le retour à la version d’origine 


 


En ce qui concerne la propagation modifications, elles se font sans actions de l’utilisateur lorsqu’une étape n’est pas modifié. De même lorsqu’une étape est ajoutée dans la procédure modèle, elle sera ajoutée automatiquement si la procédure local n’a pas modifié les étapes qui l’entoure. En revanche si ces étapes ont été modifié, la nouvelle étape apparaîtra de manière fantomatique dans la procédure locale. Enfin lorsqu’une étape est modifiée dans la procédure locale et modèle, alors l’utilisateur peut choisir d’intégrer la nouvelle version de l’étape. 

	Cette gestion augmente la flexibilité dans la mesure où les sites de productions peuvent apporter leurs modification sans compromettre la standardisation globales. Le coup en maintenance est aussi moindre puisque les mise à jour sont, autant que possible, propagé automatiquement. 

4.2.4.4	Problème rencontré 

Nous avons dû faire face à une complexité dans la gestion des types de procédures. En effet, nous utilisons 4 types de procédures ayant chacun des règles spécifique d’enchainement et de validation d’étape. L’organisation initial du code ne permettait pas la gestion de cette diversité ce qui entrainait des incohérences dans la l’exécution et la validation. Les 4 type de procédures utilisé sont : 

-	Ordonné sans statut 
-	Ordonnée avec statut 
-	Désordonné sans statut 
-	Désordonné sans statut

Les étapes ont alors fait face à des problèmes de validation. Les mécanismes de navigation et de validation était tout d’abord partagé et s’adaptaient mal au différents types de procédures. Les sauvegardes et les statuts ne s’appliquaient pas au même moment, en fonction du type de procédure ces mécanismes sont parfois automatiques. Ainsi, chaque ajout demandait une attention trop particulière pour ne par enrayer le mécanisme d’un autre type de procédure. 

Le projet a donc souffert de l’apparition de nombreux bugs dû à l’incohérence dans la gestions des différents type de procédures, affectant la fiabilité du système.  Occasionnant des retards dû à la complexité de développement et à la résolution de bug, cela a aussi impacter la satisfaction et la productivité des utilisateurs finaux en phase de test. Pour répondre à ce problème, nous avons revu l’architecture du module de procédure en apportant plus de segmentation entre les différents type de procédures. Le mécanisme de validation d’une étape a lui aussi été revu pour être en harmonie avec le gestion des statuts. Enfin, nous avons mit l’accent sur la formation des utilisateurs en internet qui devais maintenant interagir avec une system bien plus complexe et l’expliquer au client. 
