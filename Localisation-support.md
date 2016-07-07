# Localisation Configuration

Localisation was added in [issue 458](https://github.com/jekkos/opensourcepos/issues/458) and will require the `php5-intl` extension. To make everything work correctly make sure that this is installed first. 

## php5-intl extension installation
`php5-intl` can be installed as follows

* On a debian based system by hitting `sudo apt-get install php5-intl` or by manually enabling the intl extension in your cpanel (if using shared hosting).
* On a wamp install by following the instructions [in this post](http://stackoverflow.com/questions/23431788/how-to-install-intl-php-extension-with-wamp-server)

## Finding a suitable locale

Next a suitable locale code should be chosen. [A full list of language codes](https://github.com/jekkos/opensourcepos/blob/master/application/language/Language%20code%20definition) can be found directly in our repository. This language code will at first determine the currency symbol and position, decimal and thousands separator. Currency symbol can then be overridden aside from the selected locale

