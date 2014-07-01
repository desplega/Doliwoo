#**Doliwoo**
* Contributors: Cédric Salvador
* Tags: Dolibarr, WooCommerce, Doliwoo
* Requires at least: 3.7.1
* Tested up to: 3.7.1
* Stable tag: 1.0
* License: GPLv3
* License URI: http://www.gnu.org/licenses/gpl-3.0.html

A Wordpress plugin acting as an interface between WooCommerce and Dolibarr.

##**Description**

* Allows Woocommerce to pull user, thirdparty and product datas from Dolibarr.
* Can create orders and thirdparties in Dolibarr via its webservices, using WooCommerce purchase data.

##**Installation**

* Extract the zip file.
* Drop the contents in the wp-content/plugins/ directory of your WordPress installation.
* Copy conf.php-sample, modify it to fit your installation, then save it as conf.php.
* Activate the Plugin from Plugins page.

##**Detailed instructions**

Prerequisites
* Wordpress + Woocommerce installed, in i.e. http://localhost/wordpress/
* Dolibarr installed, i.e. http://localhost/dolibarr/htdocs/
* Ensure products and order modules are enabled in Dolibarr.
* Enable WebServices module and definde a 'dolibarrkey' (long string composed of numbers and letters, i.e. '0123456789qwertyuiop'.
* Define a product category in Dolibarr, i.e. 'WEB'. In case this is the first category you define the id will be '1'. If you already defined product categories you can get the id from the 'llx_categorie' table in Dolibarr database.
* Define new products in Dolibarr and assign them this category. Only products in this category will be exported to Woocommerce.
* Create a user to be used as web service link. Call the user 'webservice' for example.
* Assign rights to this user to view, create and modify any kind of document or product (orders in special). A password is required to use this user. Get the user id from 'Ref' field in the User Card.

Doliwoo installation
- Unzip doliwoo.zip in wordpress plugin folder, i.e. wordpress/wp-content/plugins/doliwoo
- Create conf.php file with user and product category info:
  <?php
    $webservs_url = 'http://localhost/dolibarr/htdocs/webservices/'; // If not a page, should end with /
    $ns = 'http://www.dolibarr.org/ns/';
    $authentication = array(
      'dolibarrkey'=> '0123456789qwertyuiop',
      'sourceapplication'=>'Doliwoo',
      'login'=>'webservice',
      'password'=> '12345',
      'entity'=>'1');
    $category_id = '1'; // Category ID (get the created product category id from llx_categorie)
    $generic_id = '2'; // Web service user id (get the Ref. from User card)

Functionality
- Once products are created in Dolibarr using the 'WEB' category you can activate Doliwoo plugin in Wordpress. At the moment of activation the products are imported to Woocommerce. After that, a cron job will import the new products (daily).
- Also VAT tax definitions will be imported to Woocommerce.
- Create an Order in Woocommerce. The order will be exported to Dolibarr.
- Users from Woocommerce will be exported to Dolibarr at the time of order exporting. For testing, you should first create the user account, log in and afterwards create the order and proceed with the checkout.
