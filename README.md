# PHP Study Guide

## What?

Originally PHP Study Guide was a small project that provides step by step guide
on information needed to pass [PHP5.3 ZCE certification][1].

For now it aims to go little bit beyond the Zend Certification and is a good
place to start your experience with PHP5.3 or, if you are already an experienced
web developer, to return to the basics and remember some details.

>For advanced topics and best practices, please, also consider to take a look 
at new, awesome and promissing project [PHP The Right Way][2] by [Josh Lockhart][3] 
with some support of PHP community.

## Where?

At the moment project is placed at [http://php-guide.evercodelab.com/][4] and
hosted on [GitHub.Pages](http://pages.github.com).

## Sources

All content is assembled from different sources and tutorials.

* Zend PHP 5.0 Certification Course by Paul Reinheimer
* Zend PHP 5 Certification Study Guide
* Zend PHP 5.3 Study Guide v1
* [Read The Web Blog][5]
* <http://www.php.net/manual/en/>
* <http://zend-php.appspot.com/>

Original guide was structured in Google Docs and then published as [pdf][6].

## Who?

Mainly project is done by me, [Roma Lapin][7] and supported by [Evercode Lab][8].

## How to contribute

At first all content was assembled to be used for PHP5.3 ZCE certification. So
it aimed to be short and kind of limited. For now feel free to contribute to it.
All suggestions to content and design is appreciated.

In order to contribute, please, do the following.

* [Fork the project][9]
* Clone down your fork
* Create a topic branch to contain your change `git checkout -b my_awesome_feature`
* Add some code
* Push the branch up `git push origin my_awesome_feature`
* [Send a Pull Request][10]

## Project layout and details

On the whole project follows standart [jekyll project layout][11].

Each certification section is presented as page in `pages` directory. Each
subsection is a part of a page.

Pygments is used for code highlighting.

Each page should have following variables in YAML Front Matter:

* title – page title
* layout - usually it is "page"

Menus is stored in `_includes/menu`.

[1]: http://www.zend.com/en/services/certification/php-5-certification/ "PHP5.3 ZCE certification"
[2]: http://www.phptherightway.com/ "PHP The Right Way"
[3]: https://github.com/codeguy
[4]: http://php-guide.evercodelab.com/ "http://php-guide.evercodelab.com/"
[5]: http://readtheweb.info/index.php?s=Zend+PHP+5+Certification+Exam&submit=Go
[6]: http://victimofbabylon.com/zce-php-53-study-guide
[7]: https://github.com/memphys
[8]: http://www.evercodelab.com/
[9]: http://help.github.com/fork-a-repo/
[10]: http://help.github.com/send-pull-requests/
[11]: https://github.com/mojombo/jekyll/wiki/usage

