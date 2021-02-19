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
   
  - Статус заказа после неудачной оплаты.
    Если Payeer вернет покупателя после неудачного платежа, заказу будет установлен выбранный статус.
    
  - Статус заказа для отсроченной оплаты.
    После проверки заказа менеджер магазина выставит данный статус, покупатель будет уведомлен по e-mail и сможет оплатить заказ.
    Также, ссылка на оплату появится в личном кабинете покупателя в разделе "Мои заказы".
    БУДЬТЕ ВНИМАТЕЛЬНЫ!
    Если данный статус будет совпадать со "статус заказа после подтверждения" - режим отсроченной оплаты будет отключен и покупатели
    будут перенаправляться на сайт "Единой Кассы" для оплаты сразу после нажатия на кнопку "Оформить заказ".
    
  - Режим отсроченной оплаты.
    При включенном режиме отсроченной (отложенной) оплаты покупатель сможет оплатить заказ только после проверки заказа менеджером магазина.
    Если Вам необходимо, чтобы у покупателя была возможность произвести оплату сразу после оформления заказа без подтверждения менеджером -
    не включайте эту опцию.

  - Название.
    Название метода оплаты на странице оформления заказа.
    ВНИМАНИЕ!!! Для Opencart/ocStore v1.5.1.3 и ниже есть ограничение: не переименовывайте название метода оплаты, если включена отсроченная
    оплата и в системе присутствуют не оплаченные отсроченные заказы. В противном случае, покупатели, не успевшие оплатить отсроченные заказы,
    никогда не смогут их оплатить.
    
  - Инструкция по оплате.
    Инструкция по оплате выводится при подтверждении заказа. Если поле не заполнено - инструкция по оплате выводиться не будет.

  - Отображать иконку "Оплатить заказ" в ЛК покупателя, если оплата заказа прервана.
    Как это работает? Покупатель перешел на сайт платежной системы и не стал оплачивать заказ (передумал, не хватило денег,
    отключили электричество в доме или офисе и пр.). Тогда в его Личном Кабинете (ЛК) в списке истории заказов появится иконка "$",
    нажав на которую покупатель сможет снова попробовать оплатить свой заказ. Иконка появится только в том случае, если текущий статус
    заказа покупателя совпадает со статусом заказа, указанных в полях "Статус заказа после подтверждения" и "Статус заказа после неудачной оплаты".
    
  - Текст кнопки button_confirm ("Потвердить заказ").
    Кнопка выводится на последнем этапе оформления заказа. При нажатии на нее заказ будет сформирован окончательно и покупатель будет отправлен
    для оплаты на сайт платежной системы (если режим отсроченной оплаты отключен).
    
  - Свой шаблон письма покупателю об успешной оплате.
    Если включено - после успешной оплаты покупателю на e-mail придет письмо, шаблон которого можно настроить ниже.
    Если выключено - будет отправляться стандартное в Opencart письмо об изменении заказа.
    Поддерживаются переменные FastTemplate.

  - Свой шаблон письма покупателю о неудачной оплате.
    Если включено - при неудачной оплате покупателю на e-mail придет письмо, шаблон которого можно настроить ниже.
    Если выключено - будет отправляться стандартное в Opencart письмо об изменении заказа.
    Поддерживается переменные FastTemplate.


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
