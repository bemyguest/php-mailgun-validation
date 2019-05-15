
# php-mailgun-validation
This package use newest, v4 Mailgun's API
Validate email address with Mailgun's validation service (Syntax checks, DNS validation, MX validation)  
More about E-mail validation: https://documentation.mailgun.com/en/latest/api-email-validation.html#email-validation
Package require Private API Key from Mailgun's dashboard: https://app.mailgun.com/app/email_validations


Installing using Composer
---------
You can install this package using composer:

    composer require bemyguest/php-mailgun-validation

Example Use Case
---------

    <?php
    require 'vendor\autoload.php';
    use bemyguest\MailgunValidator;
    
    $validator = new MailgunValidator('your-mailgun-private-key');
    
    echo var_dump($validator->validate('test@example.com')); //bool(false)
    echo var_dump($validator->validate('someuser@gmail.com')); //bool(true)
    echo var_dump($validator->validate('someuser@hotmail.com')); //bool(true)
    echo var_dump($validator->validate('someuser@aol.com')); //bool(true)
    echo var_dump($validator->validate('misformed@domain')); //bool(false)
    echo var_dump($validator->validate('invalid@anonexistingdomain.com')); //bool(false)
    
    echo var_dump($validator->validateExtended('someuser@ymail.com'));
    
    ```
    => {#8474
         +"address": "abc@abc.com",
         +"did_you_mean": null,
         +"is_disposable_address": null,
         +"is_role_address": null,
         +"reason": [
           "no_mx",
           "unknown_provider",
         ],
         +"result": "undeliverable",
         +"risk": "high",
       }

    ```
