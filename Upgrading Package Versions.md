---
tags:
  - concept
links:
  - https://docs.djangoproject.com/en/5.0/howto/upgrade-version/
---


1. Resolve any deprecation warnings raised by your project while using your current version of the package. 
	- Fixing these warnings before upgrading ensures that you’re informed about areas of the code that need altering.
	- `python -Wa manage.py test`
2. Read the release notes for the version you want to upgrade to
	- If you’re upgrading through more than one feature version (e.g. 2.0 to 2.2), it’s usually easier to upgrade through each feature release incrementally (2.0 to 2.1 to 2.2) rather than to make all the changes for each feature release at once. For each feature release, use the latest patch release (e.g. for 2.1, use 2.1.15)
	- Read the release notes for each final release from the one after your current package version, up to and including the version to which you plan to upgrade
	- ==Pay particular attention to backwards incompatible changes== to get a clear idea of what will be needed for a successful upgrade
4. Resolve any deprecation warnings or breaking code changes with your current version before continuing the upgrade process
5. Install the new package version 
	- If you are using a [[virtual environment]] and it is a major upgrade, you might want to set up a new environment with all the dependencies first
	- `pip install --upgrade -v "Django==2.1.15"`
6. When the new environment is set up, run the full test suite for your application
	- Fix any failures
7. Repeat process from step 1 until you reach the desired package version