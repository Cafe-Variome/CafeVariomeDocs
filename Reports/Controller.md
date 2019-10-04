## Controller

The CVUI_Controller class is the main superclass to generate responses in CafeVariome. It is equipped with properties, functions, and authorization checks to make future development easier. Principles of inheritance, and encapsulation are deployed.

This class extends CodeIgniter Controller classs.

Every new controller that generates an HTML response in the form of a view has to inherit from CVUI_Controller.

Below is a reference to methods and properties used in the class.

---

### _public function_ initController(\CodeIgniter\HTTP\RequestInterface $request, \CodeIgniter\HTTP\ResponseInterface $response, \Psr\Log\LoggerInterface $logger)

This method is the constructor of the class. 

__$request__ : an instance of RequestInterface   
__$response__ : an instance of ResponseInterface  
__$logger__ : an instance of the logger interface

These parameters are instantiated by CodeIgniter and are passed to the superclass constructor.

----

### _protected function_ wrapData(UIData $uidata) : array 

This function converts an instance of _UIData_ class and returns an array of elements to be passed to a view. 

__$uidata__ : an instance of UIData class  

---
### _protected function_ setAuthLevel(bool $protected, bool $isAdmin)

This function takes two inputs of boolean type and sets _isProtected_ and _isAdmin_ properties.

__$protected__ : boolean indicating whether access to the controller requires authentication or not.    
__$isAdmin__ : boolean indicating whether access to the controller requires ___Administrator__ privileges or not.





