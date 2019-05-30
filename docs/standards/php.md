!!! summary "PHP conventions - order of priority."
    There are various sources of authority for PHP conventions, but they should be followed in the following order:

    1. PHP-FIG [PSR-2] standards
    2. This documentation 
    3. Where the answer isn't clear in this documentation then refer to the existing code in the file then the repository for clarity
    4. If no clear standard is found then this **must** be raised with a senior developer for the standards to be set in the documentation

!!! success "We use the latest version of PHP for new applications."

!!! fail "We don't make new applications on old versions of PHP."

!!! warning "We currently have older applications on PHP 5.6."

!!! danger "We have legacy applications on unsupported versions of PHP."

## Function return

??? success "Do not assign a value to a variable to immediately return it."

    ```php
    //Bad
    return $result = $this->getResult();
    
    //Bad
    $result = $this->getResult();
    return $result;
    
    //Best
    return $this->getResult();
    ```

    Unless the variable is being used or manipulated further in the function, it must not be assigned to a variable.
    Instead the result should be returned directly.

[PSR-2]: http://www.php-fig.org/psr/psr-2/
