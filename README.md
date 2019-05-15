### Based on overint/php-mailgun-validation

# php-mailgun-validation
Validate email address with Mailgun's validation service (Syntax checks, DNS validation, MX validation)  
You can view Mailgun's blog post about the service here: http://blog.mailgun.com/free-email-validation-api-for-web-forms/  
An API key is required to use this library, it can be obtained from mailgun's site after signup:  
https://mailgun.com/app/account/security

~~The service is free, however fair usage limits do apply (detailed in the post linked above)~~.  
Mailgun no longer offers this service for free, however this library works fine with the new paid service. 

Installing using Composer
---------
You can install this package using composer:

    composer require bemyguest/php-mailgun-validation

Example Use Case
---------

    <?php
    require 'vendor\autoload.php';
    use bemyguest\MailgunValidator;
    
    $validator = new MailgunValidator('your-mailgun-public-key');
    
    echo var_dump($validator->validate('test@example.com')); //bool(false)
    echo var_dump($validator->validate('someuser@gmail.com')); //bool(true)
    echo var_dump($validator->validate('someuser@hotmail.com')); //bool(true)
    echo var_dump($validator->validate('someuser@aol.com')); //bool(true)
    echo var_dump($validator->validate('misformed@domain')); //bool(false)
    echo var_dump($validator->validate('invalid@anonexistingdomain.com')); //bool(false)
    
    echo var_dump($validator->validateExtended('someuser@ymail.com'));
    
     object(stdClass)#207 (8) { 
        ["address"]=> string(18) "someuser@ymail.com" 
        ["did_you_mean"]=> NULL 
        ["is_disposable_address"]=> bool(false) 
        ["is_role_address"]=> bool(false) 
        ["is_valid"]=> bool(true) 
        ["mailbox_verification"]=> string(4) "true" 
        ["parts"]=> object(stdClass)#208 (3) { 
            ["display_name"]=> NULL 
            ["domain"]=> string(9) "ymail.com" 
            ["local_part"]=> string(8) "someuser" 
        } 
        ["reason"]=> NULL 
    }
