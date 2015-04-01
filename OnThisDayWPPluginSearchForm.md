[[OTD](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPlugin) | [Screenshots](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPluginScreenshots) | [Installation and Upgrading](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPluginInstallationAndUpgrading) | [Usage](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPluginUsage) | [Customization](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPluginCustomization) | [Search Form](http://code.google.com/p/llbbsc/wiki/OnThisDayWPPluginSearchForm)]

# Introduction #

You can turn this feature on under option page(it is activated by default). Once you turn it on, there will be a search form appended after the list.

# Usage #

User can select Month, Day of Month and Year in any possible combinations, include the first blank option in each part. The blank option means unspecific month, day of month, or year.

## Search Form Only ##

If you only need search form, that means you don't need OTD list, then you can just call `GetDateSearchForm()` like
```
<?php echo GetDateSearchForm(); ?>
```
to get the search form only.

# Additional Modification for Theme #

If your theme has some code like the following, you may need to do some modifications:
```
<?php /* If this is a category archive */ if (is_category()) { ?>
    <h2 class="pagetitle">Archive for the &#8216;<?php single_cat_title(); ?>&#8217; Category</h2>
<?php /* If this is a daily archive */ } elseif (is_day()) { ?>
    <h2 class="pagetitle">Archive for <?php the_time('F jS, Y'); ?></h2>
<?php /* If this is a monthly archive */ } elseif (is_month()) { ?>
    <h2 class="pagetitle">Archive for <?php the_time('F, Y'); ?></h2>
<?php /* If this is a yearly archive */ } elseif (is_year()) { ?>
    <h2 class="pagetitle">Archive for <?php the_time('Y'); ?></h2>
<?php /* If this is an author archive */ } elseif (is_author()) { ?>
    <h2 class="pagetitle">Author Archive</h2>
<?php /* If this is a paged archive */ } elseif (isset($_GET['paged']) && !empty($_GET['paged'])) { ?>
    <h2 class="pagetitle">Blog Archives</h2>
```
Usually these are in `archive.php` theme template file, like Default Theme 1.6.

You may modify it to be:
```
<?php /* If this is a category archive */ if ( is_category() ) { ?>
    <h2 class="pagetitle">Archive for the &#8216;<?php single_cat_title(); ?>&#8217; Category</h2>
<?php /* If this is a date archive */ } elseif ( is_date() ) { ?>
    <h2 class="pagetitle">Archive for <?php echo dateArchiveTitle(); ?> </h2>
<?php /* If this is an author archive */ } elseif ( is_author() ) { ?>
    <h2 class="pagetitle">Author Archive</h2>
<?php /* If this is a paged archive */ } elseif ( isset($_GET['paged'] ) && !empty($_GET['paged'])) { ?>
    <h2 class="pagetitle">Blog Archives</h2>
<?php } ?>
```
The parts of daily, monthly and yearly archives have been removed, and replaced with a much simpler code:
```
<?php /* If this is a date archive */ } elseif ( is_date() ) { ?>
    <h2 class="pagetitle">Archive for <?php echo dateArchiveTitle(); ?> </h2>
```
`OnThisDay.php` provides a function named `dateArchiveTitle()`, it will decide an appropriate date archive title, e.g.
```
2nd day of July in every year
in 2007
July in every year 
```