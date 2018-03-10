# Emulsify on the Docksal stack

This is a short "How to" for using [Emulsify](https://github.com/fourkitchens/emulsify) Drupal theme with [Docksal](https://github.com/docksal/docksal) development environment.

## How to:

1. position yourself in the project root directory

`cd [PROJECT_ROOT_DIR]`

2. install Emulsify theme using Docksal's Composer (Composer instance installed and configured in Docksal image)

`fin exec composer require fourkitchens/emulsify`

**NOTE!!!**
I recommend using the _docksal/cli:2.0_ image (e.g. _docksal/cli:2.0-php7.1_).
Docksal now exposes port 3000 for NodeJS apps by default so you can use Browsersync and similar node applications directly from Docksal containers. This means that it is no longer necessary to have node.js, nvm or/and yarn installed on your local OS. 

3. next, enable Emulsify and its dependencies.
Drush 8.x users should use the following command but before that, position yourself in the web root directory ("_web_" or "_docroot_" in most cases) or use your drush aliases:

`cd [WEB_ROOT_DIR]`

`fin exec drush en emulsify components unified_twig_ext -y`

Drush 9.x users should use the following commands:

`cd [WEB_ROOT_DIR]`

`fin exec drush en components unified_twig_ext -y`

`fin exec drush theme:enable emulsify`

- optionaly, create a custom clone of Emulsify with:

`fin exec drush emulsify "YOUR_THEME"`

**NOTE!** At the moment (emulsify 2.2) Emulsify Drush command for cloning works only on Drush 8.x. 

4. next, run the following command from your theme directory (_contrib/emulsify_ or you custom clone _custom/YOUR_THEME_):

`cd contrib/emulsify`

or

`cd custom/[YOUR_THEME_NAME]`

5. if you already don't have your Github auth token globally defined you should do this now with (replace "YOUR_TOKEN" with the [token generated on your Github account](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)):

`fin exec composer config --global github-oauth.github.com YOUR_TOKEN`
 - this step is **necessary**, otherwise, you'll get this error after executing command in the following step: "_Failed to clone the git<span>@</span>github&#46;com:drupal-pattern-lab/patternengine-php-twig.git repository_"

6. then run `fin exec npm install` or `fin exec yarn install` command

7. after a successful instalation you can start your Gulp tasks by runing `fin exec npm start` or `fin exec yarn start`

- there are 2 access URLs and you'll use the second one (external URL)

8. don't forget to set your theme as a default one; If you created a cloned theme, disable the original Emulsify theme `fin exec drush pmu emulsify -y` (works on Drush 8.x) or with
`fin exec drupal theme:uninstall emulsify` then enable and set to default your new theme in Drupal 
(you can do that with the Drupal console command 
`fin exec drupal theme:install [YOUR_THEME_NAME] --set-default` or via the Drupal UI)
