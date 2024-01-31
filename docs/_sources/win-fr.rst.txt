===============
Français v0.0.1
===============

Créer et activer un environnement virtuel
-----------------------------------------

* Créer un dossier de travail et changer de répertoire avec ``cd /path/my_folder``
* Avec **pip** :
    * ``python -m venv <my_venv>``
    * ``<my_venv>\Scripts\activate``
* Avec **conda** :
    * ``conda create --name <my_venv>``
    * ``activate ./<my_env>``


Cloner avec GIT
---------------

* Créer un dossier de travail **<my_library>**
* Ouvrir **cmd** et changer pour le dossier créé avec ``cd /path/<my_library>``
* ``git clone https://github.com/user/repository_name.git``


Installer localement une bibliothèque
--------------------------------------

* Télécharger la bibliothèque souhaitée dans un dossier **/path/<my_library>**
* Sur **cmd** et changer pour le dossier avec ``cd /path/<my_library>``
* Pour **pip** :
    * D'abord désinstaller si installé avec ``pip uninstall <my_library>``
    * Installer avec ``python setup.py install``
* Pour **conda** :
    * ``conda remove <my_library>``
    * ``conda install /path/library-filename.tar.bz2``


Publier sur conda-forge
-----------------------

* D'abord cloner le **feedstock** de **conda-forge** sur GitHub
* Le cloner sur votre PC avec ``git clone https://github.com/user/repository_name.git``
* Sur Anaconda Prompt :
    * ``conda activate demo``
    * ``conda skeleton pypi <my_library>`` (d'abord télécharger ceci dans n'importe quel répertoire)
    * ``conda install conda-build`` (seulement si pas installé)

* Modifier le fichier **meta** en conséquence dans le dossier **recipies** dans **stage-recipie**
* Téléverser sur Github, suivre “Update Github Respository”


Mettre à jour conda-forge
-------------------------

* D'abord, la bibliothèque doit être publiée sur **pypi**
* Sur Anaconda Prompt, changer de répertoire pour le dossier de la bibliothèque avec ``cd /path/<my_library>``
* ``conda install conda-build`` (si pas installé)
* ``conda activate <venv>`` (si nécessaire)
* ``conda skeleton pypi <my_library>`` <répertoire différent>
* Si conda skeleton ne fonctionne pas, utiliser ``grayskull pypi <my_library>`` (récupère aussi depuis pipy), changer pour un autre dossier d'abord
* Fork le **<my_library>-feedstock** sur votre PC/profil (si pas encore forké)
* Mettre à jour le repo personnel ou faire un **git pull**. Normalement si vous essayez de **push** d'abord vous aurez une erreur 
* Changer le **sha256** et la **version** dans le fichier **meta.yaml** dans le dossier **recipe** avec celui créé (téléchargé). Ceci devrait être dans les 10 premières lignes.
* Changer la **version** à la nouvelle, et remettre le **numéro de build** à **0**
* NE PAS CHANGER L'HÔTE, seulement les exigences sous **run:** si des changements
* Si fait à partir du dossier local, mettre à jour le dépôt GitHub avec **git**, doit être réussi sans erreurs (suivre “Update GitHub”)
* Demander la pull request de la mise à jour : **Titre : Update <my_library>-feedstock to vX.X.X**
* N'oubliez pas de commenter sur la pull request pour le rerender comme ``@conda-forge-admin, please rerender``
* Une fois tous les tests ok, cliquer sur **Merge pull request**
* Attendre un peu pour la mise à jour


Mettre à jour la bibliothèque avec Pip
--------------------------------------

* ``pip install --upgrade <my_library>``


Reformater en PEP8
------------------

* ``autopep8 --in-place --aggressive --aggressive <filename>.py``


Mettre à jour le dépôt GitHub
-----------------------------

* Clic droit dans le dossier > Git Bash Here 
* ``git branch``
* ``git checkout main`` (ou master)
* ``git branch``
* ``git add *``
* ``git status``
* ``git commit -m “update note”``
* ``git push origin main`` (ou master)


Téléverser sur PyPi
-------------------

* Sur **cmd** en tant qu'Administrateur
* ``cd /path/<my_library>``
* ``pip install –r requirements_dev.txt`` (seulement la première fois ou si changé)
* ``python setup.py sdist``
* Aller sur GitHub > Releases > New Releases et ajouter un **tag** et un **titre de sortie** comme **vx.x.x**, une description, et publier la sortie (ne pas télécharger le zip).
* ``twine upload .\dist\<package-x.x.x.tar.gz>``
* ``twine upload -u <username> -p <password> - repository-url https://pypi.org/manage/project/<my_library>/dist/<my_library>-x.x.x.tar.gz``
* Entrer l'utilisateur et le mot de passe de **PyPi**


Bump version
------------

* Sur **cmd** en tant qu'Administrateur
* ``cd /path/<my_library>``
* ``bumpversion patch/minor/mayor`` (sélectionner un)
* ``git add *``
* ``git commit -m “commit note”``
* ``git push origin main`` (ou master)
* ``git push --tags``
* Si cela ne fonctionne pas, vous pouvez changer la version manuellement dans les fichiers **setup.py**, **setup.cfg**, et **__init__.py**.


Sphinx docs
-----------

* Sur **cmd** en tant qu'Administrateur
* Installer **Sphinx** avec ``pip install sphinx``
* Créer un dossier appelé **sphinx**
* Changer le répertoire de travail pour le dossier **sphinx** avec ``cd /path/<my_library>/sphinx``
* Télécharger le modèle avec la commande ``sphinx-quickstart`` et suivre les instructions d'installation. Configurez-le comme vous le souhaitez, en cas de doute, optez pour les valeurs par défaut.
* Modifier et ajouter des fichiers **.rst** selon vos besoins
* Avant de créer les fichiers HTML, toujours faire ``make clean``
* Créer les nouveaux fichiers HTML avec ``make html``
* Créer un répertoire appelé **/path/<my_library>/docs**
* Copier les fichiers sous **/path/<my_library>/sphinx/_build/html** dans le répertoire **/path/<my_library>/docs**, remplacer tous mais ne rien supprimer. 
* Mettre à jour le dépôt avec **git** 
* Sur GitHub aller à **Settings > Pages** et sous **Branch** sélectionner le dossier **docs** où les fichiers **html** ont été poussés.
* Si les fichiers html ne se rendent pas bien, ajouter un fichier **.nojekkyll** vide dans le dossier **docs**.


Ignorer les fichiers déjà commités
-----------------------------------

* Mettre à jour **.gitignore** si nécessaire
* ``git rm -r --cached .``
* ``git add .``
* ``git commit –m “commit comment”``
* ``git push origin main``


Coverage
--------

* Installer **coverage** si pas installé avec ``pip install coverage``
* Changer de répertoire pour le dossier de test de la bibliothèque avec ``cd /path/<my_library>/tests``
* Exécuter le fichier de test avec ``python –m unittest test_package.py``
* Exécuter les tests avec **coverage** avec ``coverage run –m unittest <test_package>.py``
* Générer le rapport de couverture avec ``coverage report``. Pour lire inclure ``-m`` à la fin. Si erreur, utiliser ``-i`` à la fin
* Générer le fichier **xml** avec ``coverage xml``
* Si la commande ``coverage`` ne fonctionne pas, alors utiliser ``python -m coverage <test_package>.py``


Compter les lignes avec cloc
-----------------------------

* Télécharger **cloc** depuis son dépôt GitHub
* Sur **cmd**, cd à l'emplacement de l'exécutable **cloc**
* Pour compter les lignes, écrire le nom de l'.exe puis l'emplacement/nom du répertoire/fichier
* Exemple : ``cloc-1.96.1.exe <my_file>.py``
