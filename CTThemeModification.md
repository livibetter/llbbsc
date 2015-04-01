[[CT](http://code.google.com/p/llbbsc/wiki/CT) | [Installation](http://code.google.com/p/llbbsc/wiki/CTInstall) |
[Upgrading](http://code.google.com/p/llbbsc/wiki/CTUpgrade) |
[Usage](http://code.google.com/p/llbbsc/wiki/CTUsage) | [CSS Customization](http://code.google.com/p/llbbsc/wiki/CTCSSCustomization) | [Testing](http://code.google.com/p/llbbsc/wiki/CTTest) | [Theme Modification](http://code.google.com/p/llbbsc/wiki/CTThemeModification)]

# Introduction #

CT is designed for being used without any modifications. However, there is no guarantee that every theme can work with CT; therefore, you may need to make small modifications to your theme.

If you have to use CT under this situation, you may not able to use all features of CT.

I will show you how to modify default theme.

# Disabling both Single Post Mode and Multi-post Mode #

First, you need to disable both Single Post Mode and Multi-post Mode, since your theme can work with CT by default.

# Knowing what is WordPress Loop #

WordPress Loop is very important thing to WordPress blogging system. Please open `index.php` of default theme in your favorite text editor. It looks like:
```
<?php get_header(); ?>

    <div id="content" class="narrowcolumn">

    <?php if (have_posts()) : ?>

        <?php while (have_posts()) : the_post(); ?>

            <div class="post" id="post-<?php the_ID(); ?>">
                <h2><a href="<?php the_permalink() ?>" rel="bookmark" title="Permanent Link to <?php the_title_attribute(); ?>"><?php the_title(); ?></a></h2>
                <small><?php the_time('F jS, Y') ?> <!-- by <?php the_author() ?> --></small>

                <div class="entry">
                    <?php the_content('Read the rest of this entry &raquo;'); ?>
                </div>

                <p class="postmetadata"><?php the_tags('Tags: ', ', ', '<br />'); ?> Posted in <?php the_category(', ') ?> | <?php edit_post_link('Edit', '', ' | '); ?>  <?php comments_popup_link('No Comments &#187;', '1 Comment &#187;', '% Comments &#187;'); ?></p>
            </div>

        <?php endwhile; ?>
[snip]
```

From fourth nonempty line `<?php while (have_posts()) : the_post(); ?>` till `<?php endwhile; ?>`, that is a WordPress Loop. You can find similar loops in `page.php`, `single.php`, `archive.php`, `search.php`.

# Automatic Method #

I personally prefer to insert citations right after post content, before tags/categories. The modified version of `index.php` would be:
```
<?php get_header(); ?>

    <div id="content" class="narrowcolumn">

    <?php if (have_posts()) : ?>

        <?php while (have_posts()) : the_post(); ?>

            <div class="post" id="post-<?php the_ID(); ?>">
                <h2><a href="<?php the_permalink() ?>" rel="bookmark" title="Permanent Link to <?php the_title_attribute(); ?>"><?php the_title(); ?></a></h2>
                <small><?php the_time('F jS, Y') ?> <!-- by <?php the_author() ?> --></small>

                <div class="entry">
                    <?php the_content('Read the rest of this entry &raquo;'); ?>
                </div>
<?php
if (function_exists('GetCitationsBlockStaticHTML'))
    echo GetCitationsBlockStaticHTML($post, null);
?>
                <p class="postmetadata"><?php the_tags('Tags: ', ', ', '<br />'); ?> Posted in <?php the_category(', ') ?> | <?php edit_post_link('Edit', '', ' | '); ?>  <?php comments_popup_link('No Comments &#187;', '1 Comment &#187;', '% Comments &#187;'); ?></p>
            </div>

        <?php endwhile; ?>
[snip]
```

The code for citations is
```
<?php
if (function_exists('GetCitationsBlockStaticHTML'))
    echo GetCitationsBlockStaticHTML($post, null);
?>
```

It directly prints out all citations to visitors as if you choose Automatic under Multi-post Mode in General Options.

# Manual Method #
Replace the code in previous section with
```
<?php
if (function_exists('GetCitationsBlockNonStaticHTML'))
    echo GetCitationsBlockNonStaticHTML($post, true, true);
?>
```
Parameters:
  * First - Post object, you should no need to change this.
  * Second - Use dynamic method
  * Third - Show a popup option

# Widget #
No matter your theme support WordPress Widget or not, you can always put the following code in `sidebar.php` at appropriate place:
```
<?php
if (function_exists('CTWidget'))
    CTWidget(array('before_widget'=>'<li>', 'after_widget'=>'</li>', 'before_title'=>'<h2>', 'after_title'=>'</h2>'));
?>
```
For default theme:
```
<?php
if (function_exists('CTWidget'))
    CTWidget(array('before_widget'=>'<li>', 'after_widget'=>'</li>', 'before_title'=>'<h2>', 'after_title'=>'</h2>'));
?>
        </ul>
    </div>
<<< LAST LINE OF sidebar.php >>>
```