# Pootle Instance For KDE

Trying to integrate [KDE translation](https://l10n.kde.org) to Pootle for easy translation.

## Setup

* Install [pootle](http://docs.translatehouse.org/projects/pootle/en/stable-2.8.x/server/installation.html)

  This repo use `pipenv`
* Set the `translations` folder.
  ```
  mkdir translations
  mkdir translations/l10n-kf5
  mkdir translations/l10n-kf5/templates/
  ```


## Running

Get into the virtual environment shell and run `pootle runserver --insecure`

## Adding Project To Pootle

Find the package to add from [here](https://l10n.kde.org/stats/gui/trunk-kf5/package/). Example : `applications`, `kde-workspace`

* Set the package :
  ```
  export REPO_ROOT=$PWD
  export PACKAGE=''
  ```
* Get the `template` files :

  ```
  cd $REPO_ROOT/translations/l10n-kf5/templates
  svn checkout svn://anonsvn.kde.org/home/kde/trunk/l10n-kf5/templates/messages/$PACKAGE $PACKAGE
  ```
* Get the language files :

  ```
  export LANG_CODE='ml'
  mkdir $REPO_ROOT/translations/l10n-kf5/$LANG_CODE && cd $REPO_ROOT/translations/l10n-kf5/$LANG_CODE
  svn checkout svn://anonsvn.kde.org/home/kde/trunk/l10n-kf5/$LANG_CODE/messages/$PACKAGE $PACKAGE
  ```
* Open Pootle admin and [add project](http://docs.translatehouse.org/projects/pootle/en/stable-2.8.x/server/project_setup.html)

  The following project variables need to be changed :

  * File types : `Gettext PO`
  * Path or URL : `{POOTLE_TRANSLATION_DIRECTORY}l10n-kf5`
  * Path mapping preset : `non-GNU style`
  * Template name : `templates`
* [Sync Pootle](http://docs.translatehouse.org/projects/pootle/en/stable-2.8.x/features/using_pootle_fs.html) :
  ```
  pootle fs sync l10n-kf5
  ```