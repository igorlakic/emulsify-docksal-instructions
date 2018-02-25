# Emulsify on the Docksal stack

This is a short "How to" for using [Emulsify](https://github.com/fourkitchens/emulsify) Drupal theme with [Docksal](https://github.com/docksal/docksal) development environment.

## How to:

- position yourself in the project root directory

`cd [PROJECT_ROOT_DIR]`

- install Emulsify theme using Docksal's Composer (Composer instance installed and configured in Docksal image)

`fin exec composer require fourkitchens/emulsify`

**NOTE!!!**
I recommend using the _docksal/cli:2.0_ image (e.g. _docksal/cli:2.0-php7.1_).
Docksal now exposes port 3000 for NodeJS apps by default so you can use Browsersync and similar node applications directly from Docksal containers. This means that it is no longer necessary to have node.js, nvm or/and yarn installed on your local OS. 

- next, enable Emulsify and its dependencies
Drush 8.x users should use the following command:

`fin exec drush en emulsify components unified_twig_ext -y`

Drush 9.x users should use the following commands:

`fin exec drush en components unified_twig_ext -y`

`fin exec drush theme:enable emulsify`

- optionaly, create a custom clone of Emulsify with:

`fin exec drush emulsify "YOUR_THEME"`

**NOTE!** At the moment (emulsify 2.2) Emulsify Drush command for cloning works only on Drush 8.x. 

- next, run the following command from your theme directory (_contrib/emulsify_ or you custom clone _custom/YOUR_THEME_):

`cd contrib/emulsify`

or

`cd custom/[YOUR_THEME]`

- then run `fin exec npm install` or `fin exec yarn install` command

- near the end, it will break ("Failed to clone the _git@github.com:drupal-pattern-lab/patternengine-php-twig.git_ repository") and you will have to edit _scripts/pattern_lab.sh_ - change line 8 to:

`composer create-project drupal-pattern-lab/edition-twig-standard pattern-lab`

- this change removes the flag "_-n_" for a non-interactive clone. 

- afterwards, run again `fin exec npm install` or `fin exec yarn install` command; Then, you'll have to provide your Github credentials, make a Github token and then copy it to your terminal to continue with the installation process.

- after a successful instalation you can start your Gulp tasks by runing `fin exec npm start` or `fin exec yarn start`

- there are 2 access URLs and you'll use the second one (external URL)

- don't forget to set your theme as a default one; If you created a cloned theme, disable the original Emulsify theme `fin exec drush pmu emulsify -y` (works on Drush 8.x) or with
`fin exec drupal theme:uninstall emulsify` and enable and set to default your new theme in Drupal 
(you can do that with the Drupal console command 
`fin exec drupal theme:install emulsify --set-default` or via the Drupal UI)
