Annexe - Documentation technique 
================================

:Type: Documentation technique
:Organisateur: ABI
:Auteur: CDS
:Objectif: Documenter le fonctionnement logiciel des sas de sécurité

Ce document présente l'installation et le fonctionnement des drivers des sas de sécurité

#. DRIVERS DES SAS
#. Les sas sont fournis avec des drivers dont l'API est composée des opérations essentielles suivantes
#. -- lancer(port entier, numSérie entier, refContrôleur Contrôleur). Lance une instance du driver avec
#. - port : le numéro du port de connexion au panneau de brassage du sas
#. - numSérie : le numéro de série du sas
#. - refContrôleur la référence (un oid) du contrôleur de sas qui va le commander
#. -- allumerLedLecteur(f face, c couleur, t entier). Allume la LED du lecteur de QRCode sur la face f avec la couleur c pendant t secondes. Les valeurs de couleur possibles sont vert, orange, rouge. Quand t=0 la LED est allumée jusqu'à la prochaine commande de changement. Quand c=éteint, éteint la led.
#. -- clignoterLedLecteur(f face, c couleur, t entier). Fait clignoter la LED du lecteur de QRCode sur la face f avec la couleur c pendant t secondes. Les valeurs de couleur possibles sont vert, orange, rouge. Quand t=0 la LED clignote jusqu'à la prochaine commande de changement. 
#. -- ouvrirPorte(face:caractère, entrée:booléen) : chaîne. Ouvre la porte de la face du sas passée en paramètre
#. si entrée est vrai, renvoie KO en cas d'échec (impossible d'ouvrir la porte complètement), Full quand une personne est détectée présente, METAL quand quand une personne est détectée présente avec du métal, Piggybacking quand plus d'une personne est détectée présente et VOID quand personne n'est détecté au bout de 5 secondes
#. si entrée est faux renvoie KO en cas d'échec (impossible d'ouvrir la porte complètement), VOID quand personne n'est détecté et Full quand une personne est détectée présente au bout de 5 secondes 
#. -- fermerPorte(face:caractère) : chaîne. Ferme la porte de la face du sas passée en paramètre et renvoie KO en cas d'échec (impossible de fermer la porte complètement), OK sinon
#. -- diffuserMessageAudio(m:audio). Diffuse le message audio m sur le haut-parleur à l'intérieur du sas
#. #########
#. OPERATION SPECIFIQUE AUX SAS XTRA
#. -- scannerEmpreinte(face) : digitCode. Lance le scan d'une empreinte digitale sur le lecteur interne de la face passée en paramètre
#. ######
#. INSTALLATION DES SAS
#. L'installation d'un sas s'effectue de la façon suivante
#. -- sur le serveur applicatif : création d'un contrôleur de sas et d'une instance de la classe sas en leur donnant le numéro de série du sas. On récupère leurs oids.
#. -- Connexion physique du sas au panneau de brassage du serveur de contrôle 
#. -- Installation du code des drivers de sas sur le serveur de contrôle
#. -- Lancement sur le serveur de contrôle d'une instance du driver de sas, en lui donnant en paramètre le numéro du port de connexion au panneau de brassage, le numéro de série du sas et l'oid du contrôleur de sas qui va le commander
#. -- Appel par cette instance de driver de l'opération lierASas(oid) du contrôleur de sas. Elle indique au contrôleur de sas la référence objet (oid) du sas qu'il va commander
#. -- Une fois lancée l'instance du driver de sas est en attente du passage d'un badge sur un de ses lecteur
#. ######
#. FONCTIONNEMENT EN CONTINU
#. A la lecture d'un badge sur une de ses faces, le driver de sas appelle l'opération contrôlersas(face,qrcCode) où face est la face (A ou B) sur laquelle la lecture a été faite et qrCode est la valeur du QRCode lu. La méthode de cette opération va gérer le passage dans le sas.

