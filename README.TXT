1. About the module Shoputils.Payeer 2.0.x-2.1.x-2.2.x - v2.3 (Payment module "Payment system PAYEER")

  The "Payeer" payment module allows you to accept payments through the system
  Payeer - http://payeer.com/.

  Module features:
  - Deferred (deferred) payment;
  - Order status when confirming, paying and canceling the order;
  - Setting the minimum and maximum order amount at which the module will be enabled;
  - Manage templates of e-mail notifications about the results of payment for buyers and administrators of the online store;
  - Arbitrary name of the payment method on the checkout page;
  - Display of payment instructions on the order confirmation page;
  - Keeping a log of requests from the server "PAYEER";
  - Selection (installation) of the PAYEER currency;
  - Information on configuring Payeer parameters on the "Information" tab;
  - Compatible with the module "Order and Registration Simple"
  
  You can see how the module works and is configured at:
  http://opencart.shoputils.ru/demo/20
  http://opencart.shoputils.ru/demo/20/admin/ (Login: demo, Password: demo)
   
2. Installing the module

   2.1 Unpack the archive, copy the contents of the upload directory to the folder with installed Opencart 2.0.x and click
     "Activate" in "Admin Panel" - "Add-ons" - "Payment" - "Payment system PAYEER, v2.1"

   2.2 For the deferred payment to work correctly, you need to install the OCMOD extension of the module.
     In the "Admin Panel" - "Modules" - "Install Extensions" click the "Download" button
     and select the file ocmod / your_opencart_version / ocmod_shoputils_payeer_laterpay.ocmod.xml from the distribution.
     After the message "The module has been successfully installed!" need to go to
     "Admin Panel" - "Modules" - "Modifiers" and click the "Update" button
     (see fig. http://opencart.shoputils.ru/image/data/install/rk_install_oc2.0_1.png)
     
   2.3 In the "Admin Panel" - "Add-ons" - "Payment" - "Payment system PAYEER, v2.0" Click "Edit"
     and configure the payment module to accept payments through "PAYEER" (see item 3).
     
   2.4 The module has a display of payment icons. To show them when choosing payment methods on the store pages,
     you need to fix the following file (you can skip the edit if it already exists if you are using the ocStore engine version 2.1.0.2.1
     and higher or if the "Simple - simplified registration and ordering" module is used):
     
        For versions 2.0 - 2.2 - catalog / view / theme / {your_theme} /template/checkout/payment_method.tpl
          
          Right after the block:

        <? php foreach ($ payment_methods as $ payment_method) {?>
        <div class = "radio">
          <label>
            <? php if ($ payment_method ['code'] == $ code ||! $ code) {?>
            <? php $ code = $ payment_method ['code']; ?>
            <input type = "radio" name = "payment_method" value = "<? php echo $ payment_method ['code'];?>" checked = "checked" />
            <? php} else {?>
            <input type = "radio" name = "payment_method" value = "<? php echo $ payment_method ['code'];?>" />
            <? php}?>
            <? php echo $ payment_method ['title']; ?>
            <? php if ($ payment_method ['terms']) {?>
            (<? php echo $ payment_method ['terms'];?>)
            <? php}?>

          Add the following lines:

        <? php // Shoputils Payment Modules Begin?>
        <? php if (isset ($ payment_method ['description'])) {?>
        <br /> <small> <? php echo $ payment_method ['description']; ?> </small>
        <? php}?>
        <? php // Shoputils Payment Modules End?>


3. Module configuration

  - Status

  - Display the module only for logged in administrators
    If the option is enabled, the module will be available at checkout only to the administrator if he is logged in
    in the admin panel. This is useful if you need not to show the module to customers during testing and configuration.

- Order status after payment
    After successful payment of the order, the selected status will be set to the order.
	
	- Статус заказа после подтверждения
	  При нажатии на кнопку "Подтвердить" на последнем этапе оформления заказа, заказу будет установлен выбранный статус
   
  - Order status after unsuccessful payment.
    If Payeer returns the buyer after an unsuccessful payment, the order will be set to the selected status.
    
  - Order status for deferred payment.
    After checking the order, the store manager will set this status, the buyer will be notified by e-mail and will be able to pay for the order.
    Also, a link to payment will appear in the buyer's personal account in the "My orders" section.
    BE CAREFUL!
    If this status matches the "order status after confirmation" - the deferred payment mode will be disabled and customers
    will be redirected to the "United Checkout" website for payment immediately after clicking on the "Checkout" button.
    
  - Deferred payment mode.
    When the delayed (deferred) payment mode is enabled, the buyer will be able to pay for the order only after the order is checked by the store manager.
    If you need the buyer to be able to make payment immediately after placing the order without confirmation by the manager -
    do not enable this option.

  - Title.
    The name of the payment method on the checkout page.
    ATTENTION!!! There is a limitation for Opencart / ocStore v1.5.1.3 and below: do not rename the name of the payment method if deferred
    payment and there are unpaid deferred orders in the system. Otherwise, customers who fail to pay for deferred orders will
    will never be able to pay them.
    
  - Payment instructions.
    Payment instructions are displayed upon order confirmation. If the field is not filled in, payment instructions will not be displayed.

  - Display the "Pay for order" icon in the buyer's personal account if the payment for the order is interrupted.
    How it works? The buyer went to the website of the payment system and did not pay for the order (changed his mind, did not have enough money,
    turned off the electricity in the house or office, etc.). Then an icon "$" will appear in his Personal Account (LC) in the order history list,
    by clicking on which the buyer can again try to pay for his order. The icon will only appear if the current status is
    Buyer's order matches the order status specified in the "Order status after confirmation" and "Order status after unsuccessful payment" fields.
    
  - The text of the button is button_confirm ("Confirm order").
    The button is displayed at the last stage of ordering. When you click on it, the order will be finalized and the buyer will be sent
    for payment to the website of the payment system (if the deferred payment mode is disabled).
    
  - Your template for a letter to the buyer about successful payment.
    If enabled - after successful payment, the buyer will receive an e-mail, the template of which can be customized below.
    If disabled, a standard Opencart order change letter will be sent.
    FastTemplate variables are supported.

  - Your own template for a letter to the buyer about an unsuccessful payment.
    If enabled - in case of unsuccessful payment, the buyer will receive an e-mail, the template of which can be customized below.
    If disabled, a standard Opencart order change letter will be sent.
    FastTemplate variables are supported. 

- Send an e-mail notification to the administrator about successful payment.
    If enabled, the administrator and IM managers will be notified by e-mail about successful payment by the client. Additional
    You can add e-mail addresses for notifications in "System-> Settings-> Edit-> Mail" tab.
    FastTemplate variables are supported.

  - Send an e-mail notification about unsuccessful payment to the administrator.
    If enabled, the administrator and IM managers will receive a notification by e-mail about unsuccessful payment by the client.
    You can add additional e-mail addresses for notifications in "System-> Settings-> Change-> Mail" tab
    FastTemplate is supported.

    List of possible FastTemplate values:
    Order number - {order_id}
    Store name - {store_name}
    Shop logo - {logo}
    List of purchased products - {products}
    Total - {total}
    Name Patronymic of the customer - {customer_firstname}
    Customer surname - {customer_lastname}
    Customer group - {customer_group}
    customer e-mail - {customer_email}
    Customer phone - {customer_telephone}
    Order status - {order_status}
    Buyer's comment to the order - {comment}
    Buyer's IP address - {ip}
    Order adding date - {date_added}
    Order modification date - {date_modified}

  - Shop ID (ID)
    The identifier of the store registered in the PAYEER system.
    You can find it out in your Payeer account: "Account -> Store -> Settings".
    Example: 3111827

  - The secret key
    The secret key for notifying about the execution of the payment, which is used to verify the 
    integrity of the information received and to uniquely identify the sender
    Must match the secret key specified in your Payeer account: "Account -> Store -> Settings".
    Example: iUqJPrkQkdbECTH5.

  - Store currency
    The currency in which the merchant transfers the payment amount to the payment
    gateway "Payeer"

  - Magazine:
  - The request log from Payeer is saved in the file: system / logs / shoputils_payeer.log
  
    In your Payeer account ("Account -> Store -> Settings"), you must specify the following URLs:
    Successful payment URL;
    Unsuccessful payment URL;
    Handler URL;
    Their values ​​are specified in the module settings 
    (Administrative panel -> Add-ons -> Payment -> Payeer payment system -> "Information" tab).
    BE CAREFUL!!! When "copy-pasting" in the browser, make sure that there are no extra spaces at the beginning or end of URLs!
          
(c) Shoputils (http://opencart.shoputils.ru) 2010 - 2016
