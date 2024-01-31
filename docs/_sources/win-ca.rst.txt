=============
Català v0.0.1
=============

Crea i activa un entorn virtual
-------------------------------

* Crea una carpeta de treball i canvia de directori amb ``cd /path/my_folder``
* Amb **pip**:
    * ``python -m venv <my_venv>``
    * ``<my_venv>\Scripts\activate``
* Amb **conda**:
    * ``conda create --name <my_venv>``
    * ``activate ./<my_env>``


Clona amb GIT
-------------

* Crea una carpeta de treball **<my_library>**
* Obre **cmd** i canvia a la carpeta creada amb ``cd /path/<my_library>``
* ``git clone https://github.com/user/repository_name.git``


Instal·la localment una biblioteca
----------------------------------

* Descarrega la biblioteca desitjada en una carpeta **/path/<my_library>**
* A **cmd** canvia a la carpeta amb ``cd /path/<my_library>``
* Per a **pip**:
    * Primer desinstal·la si està instal·lat amb ``pip uninstall <my_library>``
    * Instal·la amb ``python setup.py install``
* Per a **conda**:
    * ``conda remove <my_library>``
    * ``conda install /path/library-filename.tar.bz2``


Publica a conda-forge
---------------------

* Primer clona el **feedstock** de **conda-forge** a GitHub
* Clona'l al teu PC amb ``git clone https://github.com/user/repository_name.git``
* A Anaconda Prompt:
    * ``conda activate demo``
    * ``conda skeleton pypi <my_library>`` (primer descarrega això en qualsevol directori)
    * ``conda install conda-build`` (només si no està instal·lat)

* Modifica l'arxiu **meta** segons correspongui a la carpeta **recipies** a **stage-recipie**
* Puja a Github, segueix “Update Github Respository”


Actualitza conda-forge
----------------------

* Primer, la biblioteca ha d'estar publicada a **pypi**
* A Anaconda Prompt, canvia de directori a la carpeta de la biblioteca amb ``cd /path/<my_library>``
* ``conda install conda-build`` (si no està instal·lat)
* ``conda activate <venv>`` (si cal)
* ``conda skeleton pypi <my_library>`` <directori diferent>
* Si conda skeleton no funciona, utilitza ``grayskull pypi <my_library>`` (recupera també des de pipy), canvia primer a una altra carpeta
* Forka el **<my_library>-feedstock** al teu PC/perfil (si no està forkat)
* Actualitza el repositori personal o fes un **git pull**. Normalment si intentes fer **push** primer obtindràs un error
* Canvia el **sha256** i la **versió** a l'arxiu **meta.yaml** a la carpeta **recipe** amb el creat (descarregat). Això hauria d'estar a les primeres 10 línies.
* Canvia la **versió** a la nova, i restableix el **número de construcció** a **0**
* NO CANVIS L'AMFITRIÓ, només els requisits sota **run:** si hi ha canvis
* Si es fa des de la carpeta local, actualitza el repositori GitHub amb **git**, ha de ser reeixit sense errors (segueix “Update GitHub”)
* Sol·licita la pull request de l'actualització: **Títol: Update <my_library>-feedstock to vX.X.X**
* Recorda comentar a la pull request per al rerender com ``@conda-forge-admin, please rerender``
* Un cop tots els tests estan bé, fes clic a **Merge pull request**
* Espera una estona per a l'actualització


Actualitza la biblioteca amb Pip
--------------------------------

* ``pip install --upgrade <my_library>``


Reformat a PEP8
---------------

* ``autopep8 --in-place --aggressive --aggressive <filename>.py``


Actualitza el Repositori GitHub
-------------------------------

* Feu clic dret a la carpeta > Git Bash Here 
* ``git branch``
* ``git checkout main`` (o master)
* ``git branch``
* ``git add *``
* ``git status``
* ``git commit -m “update note"``
* ``git push origin main`` (o master)


Puja a PyPi
-----------

* A **cmd** com a Administrador
* ``cd /path/<my_library>``
* ``pip install –r requirements_dev.txt`` (només la primera vegada o si ha canviat)
* ``python setup.py sdist``
* Ves a GitHub > Releases > New Releases i afegeix un **tag** i un **títol de llançament** com **vx.x.x**, una descripció, i publica el llançament (no pujar el zip).
* ``twine upload .\dist\<package-x.x.x.tar.gz>``
* ``twine upload -u <username> -p <password> - repository-url https://pypi.org/manage/project/<my_library>/dist/<my_library>-x.x.x.tar.gz``
* Introdueix l'usuari i la contrasenya de **PyPi**


Augmenta la versió
-------------------

* A **cmd** com a Administrador
* ``cd /path/<my_library>``
* ``bumpversion patch/minor/major`` (selecciona un)
* ``git add *``
* ``git commit -m “commit note”``
* ``git push origin main`` (o master)
* ``git push --tags``
* Si això no funciona, pots canviar la versió manualment en els arxius **setup.py**, **setup.cfg**, i **__init__.py**.


Documentació Sphinx
-------------------

* A **cmd** com a Administrador
* Instal·la **Sphinx** amb ``pip install sphinx``
* Crea una carpeta anomenada **sphinx**
* Canvia el directori de treball a la carpeta **sphinx** amb ``cd /path/<my_library>/sphinx``
* Descarrega la plantilla amb la comanda ``sphinx-quickstart`` i segueix les instruccions d'instal·lació. Configura-la com vulguis, en cas de dubte opta pels valors predeterminats.
* Modifica i afegeix fitxers **.rst** segons necessitis
* Abans de crear els fitxers HTML, sempre fes ``make clean``
* Crea els nous fitxers HTML amb ``make html``
* Crea un directori anomenat **/path/<my_library>/docs**
* Copia els fitxers de **/path/<my_library>/sphinx/_build/html** al directori **/path/<my_library>/docs**, substitueix tot però no elimines cap fitxer. 
* Actualitza el repositori amb **git** 
* A GitHub ves a **Settings > Pages** i sota **Branch** selecciona la carpeta **docs** on s'han empès els fitxers **html**.
* Si els fitxers html no es visualitzen bé, afegeix un fitxer **.nojekkyll** buit a la carpeta **docs**.


Ignora els fitxers ja committats
---------------------------------

* Actualitza **.gitignore** si cal
* ``git rm -r --cached .``
* ``git add .``
* ``git commit –m “commit comment”``
* ``git push origin main``


Coverage
--------

* Instal·la **coverage** si no està instal·lat amb ``pip install coverage``
* Canvia de directori a la carpeta de tests de la biblioteca amb ``cd /path/<my_library>/tests``
* Executa el fitxer de test amb ``python –m unittest test_package.py``
* Executa els tests amb **coverage** amb ``coverage run –m unittest <test_package>.py``
* Genera l'informe de cobertura amb ``coverage report``. Per llegir-lo inclou ``-m`` al final. En cas d'error, utilitza ``-i`` al final
* Genera el fitxer **xml** amb ``coverage xml``
* Si la comanda ``coverage`` no funciona, utilitza ``python -m coverage <test_package>.py``


Compta línies amb cloc
-----------------------

* Descarrega **cloc** des del seu repositori GitHub
* A **cmd**, ves a la ubicació de l'executable **cloc**
* Per comptar línies, escriu el nom de l'.exe i després la ubicació/nom del directori/fitxer
* Exemple: ``cloc-1.96.1.exe <my_file>.py``
