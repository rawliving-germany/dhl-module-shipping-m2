Raw Living Germanys Fork of DHL Shipping Extension
==================================================

The situation is awful, DHL and its partner netresearch are neither developing
transparently, nor were they able to ship a magento2 extension that is beyond
a beta state since more than ... a long time.

What we fixed here:
* hard-coded kg instead of lbs and cm instead of inch as weight/dimensions in label creation.
* removed the COD payment modification - we do not use COD and the code messed up payment method for international orders

DHL Shipping Extension
======================

The DHL Shipping extension for Magento® 2 integrates the DHL business customer
shipping API into the order processing workflow.

Facts
-----
* version: 0.6.0

Description
-----------
This extension enables merchants to request shipping labels for incoming orders
via the [DHL business customer shipping API](https://entwickler.dhl.de/en/)
(DHL Geschäftskundenversand-API).

Requirements
------------
* PHP >= 5.6.5
* PHP >= 7.0.6

Compatibility
-------------
* Magento >= 2.1.4

Installation Instructions
-------------------------
The DHL Shipping module for Magento® 2 is distributed in three formats:
* Drop-In
* [Composer Artifact](https://getcomposer.org/doc/05-repositories.md#artifact)
* [Composer VCS](https://getcomposer.org/doc/05-repositories.md#using-private-repositories)

### Install Source Files ###

The following sections describe how to install the module source files,
depending on the distribution format, to your Magento® 2 instance. 

#### Drop-In ####
If you received a single ZIP file with no `composer.json` file included, extract
its contents to the project root directory. The module sources should then be
available in the following sub-directory:

    app
    └── code
        └── Dhl
            └── Shipping

#### Artifact ####
If you received multiple ZIP files with `composer.json` files included, move
them to a common directory on the server. The directory
`/var/www/share/marketplace/dhl` is used in the following examples. Please
replace this path with the actual artifact directory of choice.

    /var
    └── www
        └── share
            └── marketplace
               └── dhl
                    ├── Dhl_Shipping_Lib-0.6.0.zip
                    └── Dhl_Shipping_Module_M2-0.6.0.zip

Then navigate to the project root directory and run the following commands:

    composer config repositories.dhl-shipping-m2 artifact /var/www/share/marketplace/dhl/
    composer require dhl/module-shipping-m2:0.6.0

#### VCS ####
If you prefer to install the module using [git](https://git-scm.com/), run the
following commands in your project root directory:

    composer config repositories.dhl-module-shipping-m2 vcs https://github.com/netresearch/dhl-module-shipping-m2.git
    composer config repositories.dhl-lib-shipping vcs https://github.com/netresearch/dhl-lib-shipping-mx.git
    composer require dhl/module-shipping-m2:0.6.0

### Enable Module ###
Once the source files are available, make them known to the application:

    ./bin/magento module:enable Dhl_Shipping
    ./bin/magento setup:upgrade

Last but not least, flush cache and compile.

    ./bin/magento cache:flush
    ./bin/magento setup:di:compile

Uninstallation
--------------

The following sections describe how to uninstall the module, depending on the
distribution format, from your Magento® 2 instance. 

#### Composer VCS and Composer Artifact ####

To unregister the shipping module from the application, run the following command:

    ./bin/magento module:uninstall --remove-data Dhl_Shipping
    
This will automatically remove source files and clean up the database.

#### Drop-In ####

To uninstall the module manually, run the following commands in your project
root directory:

    ./bin/magento module:disable Dhl_Shipping
    rm -r app/code/Dhl/Shipping

To clean up the database, run the following commands:

    DROP TABLE `dhlshipping_quote_address`;
    DROP TABLE `dhlshipping_order_address`;
    DELETE FROM `core_config_data` WHERE `path` LIKE 'carriers/dhlshipping/%';
    DELETE FROM `setup_module` WHERE `module` = 'Dhl_Shipping';

Support
-------
In case of questions or problems, please have a look at the
[Support Portal (FAQ)](http://dhl.support.netresearch.de/) first.

If the issue cannot be resolved, you can contact the support team via the
[Support Portal](http://dhl.support.netresearch.de/) or by sending an email
to <dhl.support@netresearch.de>.

Developer
---------
* Christoph Aßmann | [Netresearch GmbH & Co. KG](http://www.netresearch.de/) | [@mam08ixo](https://twitter.com/mam08ixo)
* Sebastian Ertner | [Netresearch GmbH & Co. KG](http://www.netresearch.de/)
* Benjamin Heuer | [Netresearch GmbH & Co. KG](http://www.netresearch.de/)
* Paul Siedler | [Netresearch GmbH & Co. KG](http://www.netresearch.de/)

License
-------
[OSL - Open Software Licence 3.0](http://opensource.org/licenses/osl-3.0.php)

Copyright
---------
(c) 2017 DHL Paket GmbH
