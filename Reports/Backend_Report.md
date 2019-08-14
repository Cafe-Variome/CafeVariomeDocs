## Backend Migration Report ##
---
Mehdi Mehtarizadeh  - _August 2019_

The backend migration involved updating the code to PHP 7, adapting it to the new CodeIgniter 4 platform. Moreover, Elasticsearch and Neo4J database have been upgraded. KeyCloak is newly introduced to act as identity broker/provider.

### CodeIgniter 4 ###
----
CodeIgniter (CI) 4 relies on a backend which differs significantly from CI 3 and CI 2. CI 4 promotes the MVC design pattern in a better way. 

A transtion from snake case to camel case is obvious in function names. The new Cafe Variome code uses camel case as well.

Some libraries and helpers, such as the _file helper_, no longer exist in CI 4.

To load a library or model in CI 2 or 3 the following code is used:

    $this->load->model('model_name')
    $this->load->library('library_name')

However, in CI 4, to achieve the above functionality, the model or library is initiated as an object with the _new_ keyword in PHP. If the corresponding class is static, the name of the class with double colons is used to access methods and properties. Proper namespaces must be used in place.
