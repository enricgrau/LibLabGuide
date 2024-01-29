==============
English v0.0.1
==============

Clone with GIT
--------------
-	git clone https://github.com/user/repository.git


Locally install a library
^^^^^^^^^^^^^^^^^^^^^^^^^

-	On command prompt/terminal (Admin) cd to the folder of the library
-	First uninstall if installed with pip uninstall ‘library’
-	Install with python setup.py install


Publish to conda-forge
^^^^^^^^^^^^^^^^^^^^^^

-	First clone the “feedstock” from conda-forge on GitHub
-	Clone it to your PC: Git clone <fork url>
-	On Anaconda Prompt:
-	conda activate demo
-	conda skeleton pypi <package> (first download this on any directory)
-	conda install conda-build (only if not installed)
-	Modify the “meta” file accordingly in the folder “recipies” in “stage-recipie”
-	Upload to Github, follow “Update Github”


Update conda-forge
^^^^^^^^^^^^^^^^^^

-	On Anaconda Prompt, cd to library folder
-	conda install conda-build (if not installed)
-	conda activate demo (if needed)
-	conda skeleton pypi spectrapepper <different directory> 
-	If conda skeleton doesn’t work, use grayskull pypi <library name> (retrieves from pipy!), cd to a different folder first
-	Fork the spectrapepper-feedstock to your PC/profile (if not forked)
-	Update the personal repo or do a “git pull”. Normally if you try to “push” first you’ll get an error… 
-	Change the sha256 and version on the “meta.yaml” file on “recipe” folder with the one created (downloaded). This should be the first 10 lines.
-	Change the “version” to the new one, and reset “build number” to 0
-	DON’T CHANGE THE HOST, only requirements under “run:” if any changes
-	If done from local folder, update the github repository whit git, must be successful with no errors (follow “Update Github”)
-	Pull request the update: Title: Update spectrapepper-feedstock to vX.X.X
-	Remember to comment on the pull request for rerender as “@conda-forge-admin, please rerender”
-	Once all tests are ok, click “Merge pull request”
-	Wait some time for the update


Pip Update
^^^^^^^^^^

-	Pip install --upgrade <package>

Reformat to PEP8
^^^^^^^^^^^^^^^^

-	autopep8 --in-place --aggressive --aggressive <filename>


Update GitHub
^^^^^^^^^^^^^^

-	Right click in forlder -> Git Bash Here 
-	git branch
-	git checkout main (or master)
-	git branch
-	git add *
-	git status
-	git commit -m “update note”
-	git push origin main (or master)


Upload to PyPi
^^^^^^^^^^^^^^

-	On Windows Terminal (Admin)
-	cd c:\...\...\library folder
-	pip install –r requirements_dev.txt (only first time or if changed)
-	python setup.py sdist
-	Github -> Releases -> New Realse -> tag and name vx.x.x, some description, and publish release (don’t upload the zip).
-	twine upload .\dist\<package-x.x.x.tar.gz>
-	twine upload -u GrauJack -p afw89= - repository-url https://pypi.org/manage/project/spectrapepper/ dist/spectrapepper-0.0.10.tar.gz
-	Enter PyPi user and pass


Bump version
^^^^^^^^^^^^

-	On Windows Terminal
-	cd c:\...\...\current folder
-	bumpversion patch/minor/mayor (select one)
-	git add \*, add ., commit, push
-	git push --tags


Sphinx docs
^^^^^^^^^^^

-	On Windows Terminal
-	Install library with pip install sphinx
-	Create a folder called “sphinx” 
-	Cd to folder “sphinx”
-	Download the template with the command sphinx-quickstart and follow the installation instructions. Set it up as you need, if in doubt go with the defaults.
-	Change and add `.rst` files as you need
-	Before creating the HTML files, always do `Make clean`
-	Create the new HTML files with `Make html`
-	Copy files under “_build/html” to “docs”, replace all but don’t delete any files. ‘.nojekkyll’ is essential and not made by sphinx.


Ignore already commited files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-	Update .gitignore
-	Git rm -r --cached .
-	Git add .
-	Git commit –m “…”
-	Git push origin main


Coverage
^^^^^^^^

-	Remember first to change the imports (import my_functions…)
-	pip install coverage (if not installed)
-	change directory (cd) to the corresponding folder where the tests are
-	python –m unittest test_spectrapepper.py (just run the py file)
-	coverage run –m unittest test_spectrapepper.py (to run the test with coverage)
-	coverage report (generates the report, format not supported. To read include “-m” at the end)
-	If error, use “-i” at the end
-	coverage xml (supported format!)
-	If “coverage …” does not work, then use “python -m coverage …”


Count lines with cloc
^^^^^^^^^^^^^^^^^^^^^

-	Download cloc from its Github repository
-	On Windows Terminal, cd to the location of the cloc executable
-	To count lines, write the name of the .exe and then the location/name of the dir/file
-	Example: cloc-1.96.1.exe my_file.py 
