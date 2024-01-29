==============
English v0.0.1
==============

Clone with GIT
--------------
* Create a working folder **<my_library>**
* Open **cmd** and change to the created folder with ``cd /path/<my_library>``
* ``git clone https://github.com/user/repository_name.git``


Locally install a library
-------------------------
* Download the desired library into a folder `/path/<my_library>`
* On **cmd** and change to the fodler with ``cd /path/<my_library>``
* For **pip**:
    * First uninstall if installed with ``pip uninstall <my_library>``
    * Install with ``python setup.py install``
* For **conda**:
    * ``conda remove <my_library>``
    * ``conda install /path/library-filenmae.tar.bz2``


Publish to conda-forge
----------------------

* First clone the `feedstock` from `conda-forge` on GitHub
* Clone it to your PC with ``git clone https://github.com/user/repository_name.git``
* On Anaconda Prompt:
    * ``conda activate demo``
    * ``conda skeleton pypi <my_library>`` (first download this on any directory)
    * ``conda install conda-build`` (only if not installed)

* Modify the `meta` file accordingly in the folder `recipies` in `stage-recipie`
* Upload to Github, follow “Update Github Respository”


Update conda-forge
------------------
* First, the library need to be published in `pypi`
* On Anaconda Prompt, cd to library folder
* ``conda install conda-build`` (if not installed)
* ``conda activate demo`` (if needed)
* ``conda skeleton pypi <my_library>`` <different directory> 
* If conda skeleton doesn’t work, use ``grayskull pypi <my_library>`` (retrieves from pipy too), cd to a different folder first
* Fork the `<my_library>-feedstock` to your PC/profile (if not forked)
* Update the personal repo or do a “git pull”. Normally if you try to “push” first you’ll get an error… 
* Change the `sha256` and `version` on the `meta.yaml` file on `recipe` folder with the one created (downloaded). This should be within the first 10 lines.
* Change the `version` to the new one, and reset `build number` to `0`
* DON’T CHANGE THE HOST, only requirements under `run:` if any changes
* If done from local folder, update the github repository whith git, must be successful with no errors (follow “Update Github”)
* Pull request the update: Title: Update spectrapepper-feedstock to vX.X.X
* Remember to comment on the pull request for rerender as `@conda-forge-admin, please rerender`
* Once all tests are ok, click “Merge pull request”
* Wait some time for the update


Pip Update
----------

* ``pip install --upgrade <my_library>``


Reformat to PEP8
----------------

* ``autopep8 --in-place --aggressive --aggressive <filename>``


Update GitHub Repository
------------------------

* Right click in forlder -> Git Bash Here 
* ``git branch``
* ``git checkout main`` (or master)
* ``git branch``
* ``git add *``
* ``git status``
* ``git commit -m “update note”``
* ``git push origin main`` (or master)


Upload to PyPi
--------------

* On **cmd** as Administrator
* ``cd /path/<my_library>``
* ``pip install –r requirements_dev.txt`` (only first time or if changed)
* ``python setup.py sdist``
* Go to Github > Releases > New Releases  and add a **tag** and **Release title** as **vx.x.x**, some description, and publish release (don’t upload the zip).
* ``twine upload .\dist\<package-x.x.x.tar.gz>``
* ``twine upload -u <username> -p <password> - repository-url https://pypi.org/manage/user/dist/<my_library>-0.0.10.tar.gz``
* Enter **PyPi** user and pass


Bump version
------------

* On **cmd** as Administrator
* ``cd /path/<my_library>``
* ``bumpversion patch/minor/mayor`` (select one)
* ``git add *``
* ``git commit -m “commit note”``
* ``git push origin main`` (or master)
* ``git push --tags``
* If this does not work, you can change the version manually in the files **setup.py**, **setup.cfg**, and **__init__.py** files.


Sphinx docs
-----------

* On **cmd** as Administrator
* Install **Sphinx** with ``pip install sphinx``
* Create a folder called **sphinx**
* Change work directory to the folder **sphinx** with ``cd /path/<my_library>/sphinx``
* Download the template with the command ``sphinx-quickstart`` and follow the installation instructions. Set it up as you need, if in doubt go with the defaults.
* Change and add **.rst** files as you need
* Before creating the HTML files, always do ``Make clean``
* Create the new HTML files with ``Make html``
* Create a directory called **/path/<my_library>/docs**
* Copy files under **/path/<my_library>/sphinx/_build/html** to the **/path/<my_library>/docs** directory, replace all but don’t delete any files. 
* Update the repository with **git** 
* In **GitHub** got to  **Settings > Pages** and Under **Branch** select the **docs** folder where the **html** where pushed to.
* If the html files do not render well, add and empty **.nojekkyll** file in the **docs** folder.


Ignore already commited files
-----------------------------

* Update **.gitignore** if needed
* ``git rm -r --cached .``
* ``git add .``
* ``git commit –m “commit comment”``
* ``git push origin main``


Coverage
--------

* ``pip install coverage`` (if not installed)
* change directory (cd) to the corresponding folder where the tests are
* ``python –m unittest test_package.py`` (just run the py file)
* ``coverage run –m unittest test_package.py`` (to run the test with coverage)
* ``coverage report`` (generates the report, format not supported. To read include “-m” at the end)
* If error, use ``-i`` at the end
* ``coverage xml`` (supported format!)
* If ``coverage`` does not work, then use ``python -m coverage …``


Count lines with cloc
---------------------

* Download **cloc** from its Github repository
* On **cmd**, cd to the location of the **cloc** executable
* To count lines, write the name of the .exe and then the location/name of the dir/file
* Example: ``cloc-1.96.1.exe my_file.py``
