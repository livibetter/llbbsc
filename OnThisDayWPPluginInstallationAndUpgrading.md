[[OTD](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPlugin) | [Screenshots](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPluginScreenshots) | [Installation and Upgrading](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPluginInstallationAndUpgrading) | [Usage](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPluginUsage) | [Customization](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPluginCustomization) | [Search Form](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPluginSearchForm)]

# Installation #

  1. Copy directory `OnThisDay` to `wp-content/plugins`.
  1. Activate "On this day" in plugins page.
  1. Set Options, Add "On this day" widget at sidebar, or add `OTDList()` to sidebar, or main post loop.

# Upgrading #

This secion will tell you, do you need to upgrade and anything you have to pay attention while upgrading.

## 0.2.3 to 0.3 ##
  * Three are two more options `Include pages` and `Exclude current year's posts` in General Options has been added in 0.3, some behaviors may be changed.

## 0.2 to 0.2.1 ##
  * Steps: Deactivate 0.2, remove 0.2, upload 0.2.1, activate 0.2.1.
  * All old options will be removed, such limit, excerpt length, etc.
  * OTDList accepts only $targetPost. You can only customize HTML using settings in Options page.

## 0.1 to 0.1.1 ##
  * Just override
  * If your WP can do date search normally, then you don't have to upgrade.
  * Upgrading to 0.1.1 can ensure including the javascript code only once. In another words, save little bandwidth.

# Uninstalltion #

From version 0.5, OTD allows you to remove all settings for OTD as well as deactivation of OTD.

  * Go to OTD option page.
  * Click "Deactivate Plugin" at "Management" section on right side.