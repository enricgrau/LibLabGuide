===============
Italiano v0.0.1
===============

Crea e attiva un ambiente virtuale
----------------------------------

* Crea una cartella di lavoro e cambia directory con ``cd /path/my_folder``
* Con **pip**:
    * ``python -m venv <my_venv>``
    * ``<my_venv>\Scripts\activate``
* Con **conda**:
    * ``conda create --name <my_venv>``
    * ``activate ./<my_env>``


Clona con GIT
-------------

* Crea una cartella di lavoro **<my_library>**
* Apri **cmd** e cambia nella cartella creata con ``cd /path/<my_library>``
* ``git clone https://github.com/user/repository_name.git``


Installa localmente una libreria
---------------------------------

* Scarica la libreria desiderata in una cartella **/path/<my_library>**
* Su **cmd** cambia nella cartella con ``cd /path/<my_library>``
* Per **pip**:
    * Prima disinstalla se installato con ``pip uninstall <my_library>``
    * Installa con ``python setup.py install``
* Per **conda**:
    * ``conda remove <my_library>``
    * ``conda install /path/library-filename.tar.bz2``


Pubblica su conda-forge
-----------------------

* Prima clona il **feedstock** da **conda-forge** su GitHub
* Clonalo sul tuo PC con ``git clone https://github.com/user/repository_name.git``
* Su Anaconda Prompt:
    * ``conda activate demo``
    * ``conda skeleton pypi <my_library>`` (prima scarica questo in una qualsiasi directory)
    * ``conda install conda-build`` (solo se non installato)

* Modifica il file **meta** di conseguenza nella cartella **recipies** in **stage-recipie**
* Carica su Github, segui “Update Github Respository”


Aggiorna conda-forge
--------------------

* Prima, la libreria deve essere pubblicata su **pypi**
* Su Anaconda Prompt, cambia directory nella cartella della libreria con ``cd /path/<my_library>``
* ``conda install conda-build`` (se non installato)
* ``conda activate <venv>`` (se necessario)
* ``conda skeleton pypi <my_library>`` <directory diversa>
* Se conda skeleton non funziona, usa ``grayskull pypi <my_library>`` (recupera anche da pipy), cambia prima in un'altra cartella
* Forka il **<my_library>-feedstock** sul tuo PC/profilo (se non forkato)
* Aggiorna il repo personale o fai un **git pull**. Normalmente se provi a fare **push** prima otterrai un errore
* Cambia il **sha256** e la **versione** nel file **meta.yaml** nella cartella **recipe** con quello creato (scaricato). Questo dovrebbe essere nelle prime 10 righe.
* Cambia la **versione** alla nuova, e reimposta il **numero di build** a **0**
* NON CAMBIARE L'HOST, solo i requisiti sotto **run:** se ci sono cambiamenti
* Se fatto dalla cartella locale, aggiorna il repository GitHub con **git**, deve essere riuscito senza errori (segui “Update GitHub”)
* Richiedi la pull request dell'aggiornamento: **Titolo: Update <my_library>-feedstock to vX.X.X**
* Ricorda di commentare sulla pull request per il rerender come ``@conda-forge-admin, please rerender``
* Una volta che tutti i test sono ok, clicca **Merge pull request**
* Aspetta un po' per l'aggiornamento


Aggiorna libreria con Pip
-------------------------

* ``pip install --upgrade <my_library>``


Riformatta in PEP8
------------------

* ``autopep8 --in-place --aggressive --aggressive <filename>.py``


Aggiorna Repository GitHub
--------------------------

* Tasto destro nella cartella > Git Bash Here 
* ``git branch``
* ``git checkout main`` (o master)
* ``git branch``
* ``git add *``
* ``git status``
* ``git commit -m “update note”``
* ``git push origin main`` (o master)


Carica su PyPi
--------------

* Su **cmd** come Amministratore
* ``cd /path/<my_library>``
* ``pip install –r requirements_dev.txt`` (solo la prima volta o se cambiato)
* ``python setup.py sdist``
* Vai su GitHub > Releases > New Releases e aggiungi un **tag** e un **titolo di rilascio** come **vx.x.x**, una descrizione, e pubblica il rilascio (non caricare il zip).
* ``twine upload .\dist\<package-x.x.x.tar.gz>``
* ``twine upload -u <username> -p <password> - repository-url https://pypi.org/manage/project/<my_library>/dist/<my_library>-x.x.x.tar.gz``
* Inserisci l'utente e la password di **PyPi**


Incrementa la versione
-----------------------

* Su **cmd** come Amministratore
* ``cd /path/<my_library>``
* ``bumpversion patch/minor/major`` (scegliere uno)
* ``git add *``
* ``git commit -m “commit note”``
* ``git push origin main`` (o master)
* ``git push --tags``
* Se questo non funziona, puoi cambiare la versione manualmente nei file **setup.py**, **setup.cfg**, e **__init__.py**.


Documentazione Sphinx
---------------------

* Su **cmd** come Amministratore
* Installa **Sphinx** con ``pip install sphinx``
* Crea una cartella chiamata **sphinx**
* Cambia la directory di lavoro nella cartella **sphinx** con ``cd /path/<my_library>/sphinx``
* Scarica il modello con il comando ``sphinx-quickstart`` e segui le istruzioni di installazione. Configuralo come desideri, in caso di dubbi usa i valori predefiniti.
* Modifica e aggiungi file **.rst** come necessario
* Prima di creare i file HTML, eseguire sempre ``make clean``
* Crea i nuovi file HTML con ``make html``
* Crea una directory chiamata **/path/<my_library>/docs**
* Copia i file da **/path/<my_library>/sphinx/_build/html** nella directory **/path/<my_library>/docs**, sostituisci tutto ma non eliminare nessun file. 
* Aggiorna il repository con **git** 
* Su GitHub vai in **Settings > Pages** e sotto **Branch** seleziona la cartella **docs** dove sono stati spinti i file **html**.
* Se i file html non vengono visualizzati bene, aggiungi un file **.nojekkyll** vuoto nella cartella **docs**.


Ignora i file già committati
-----------------------------

* Aggiorna **.gitignore** se necessario
* ``git rm -r --cached .``
* ``git add .``
* ``git commit –m “commit comment”``
* ``git push origin main``


Coverage
--------

* Installa **coverage** se non installato con ``pip install coverage``
* Cambia directory nella cartella dei test della libreria con ``cd /path/<my_library>/tests``
* Esegui il file di test con ``python –m unittest test_package.py``
* Esegui i test con **coverage** con ``coverage run –m unittest <test_package>.py``
* Genera il rapporto di copertura con ``coverage report``. Per leggerlo includi ``-m`` alla fine. In caso di errore, usa ``-i`` alla fine
* Genera il file **xml** con ``coverage xml``
* Se il comando ``coverage`` non funziona, utilizza ``python -m coverage <test_package>.py``


Conta le righe con cloc
-----------------------

* Scarica **cloc** dal suo repository GitHub
* Su **cmd**, vai alla posizione dell'eseguibile **cloc**
* Per contare le righe, scrivi il nome dell'.exe e poi la posizione/nome della cartella/file
* Esempio: ``cloc-1.96.1.exe <my_file>.py``
