# Library Laboratory Guide

Over the years, while developing Python libraries with Git and GitHub, I've often needed to carry out various procedures. Some of these tasks are rare, perhaps done only once in the lifetime of a library, like publishing to PyPI or Conda-forge. Because of this, remembering these infrequent steps can be challenging. To address this, I've been gathering all these procedures and compiling them into one central document for quick reference. I've found this collection immensely helpful, and it struck me that it might be beneficial to others as well. So, I'm sharing it here for anyone who might find it useful. And es, this si essentially a cheat sheet.

Access the documentation here: https://enricgrau.github.io/LibLabGuide/

# How to use

The guide is organized by Operating System (OS) and language. Each OS has its own folder, within which you'll find documents for different languages. These documents are in HyperText Markup Language (HTML) format, created using a Sphinx template. This makes them easily accessible through any preferred web browser. You can quickly find what you need using the search function or the index navigation.

All instructions and procedures are compiled into one comprehensive file, without being split into further categories. They are arranged sequentially, so if you're starting a library from scratch, you can follow the steps in order from beginning to end (or close to it).

You may download the corresponding HTML file for your preferred OS and language, and open it locally, though some aesthetics may be lost.


# Available guides

- Windows
    - English (en) [v0.0.1]
    - Español (es) [v0.0.1]
 

# List of procedures and commands

- Crerate and activate virtual environment
- Update libraries with `pip`
- Clone repository with `git`
- Update GitHub repositiry
- Bump repositories version
- Locally install a library
- Publish/Update to `PyPi`
- Publish to ``Conda-forge``
- Update ``Conda-forge``
- Create documentation with ``Sphinx``
- Update documentation with ``Sphinx``
- Ignore commited files in ``git``
- Code coverage with ``codecov``
- Count code lines with `cloc`
- Reformat to ``PEP8``


# Disclaimer

- I'm dedicated to regularly updating and enhancing this list. If you're interested in contributing, I would be delighted to have your support!
- Please use these procedures cautiously. While I try to keep them up to date, changes in technology can sometimes outpace my updates.
- I cannot be held accountable for any issues or inconveniences that might arise from following these instructions.


# Credits

Finally, I kindly ask that if you find this list useful, consider citing or reference it as:

        @misc{Grau-Luque2024LLG,
        author = {E. Grau-Luque},
        title = {{LibLabGuide: A list of useful commands and procdeures for developing Github repositories and Python libraries}},
        year = {2024},
        publisher = {GitHub},
        journal = {GitHub repository},
        doi = {}
        url = {https://github.com/enricgrau/LibLabGuide},
        }

If you cannot make a reference otr citation, please consider contributing. Everything helps!