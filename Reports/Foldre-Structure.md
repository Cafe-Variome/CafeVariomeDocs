## Folder Structure ##

The programme follows the directory structure in CodeIgniter 4.  

    |--app
        |__Config
        |__Controllers
        |__Database
        |__Filters
        |__Helpers
        |__Language
        |__Libraries
        |__Models
        |__ThirdParty
        |__Views
    |--public
    |--resources
        |__css
        |__images
        |__js
        |__phenotype_lookup_data
    |--system
    |--upload
    |--vendor
    |--writable
        |__cache
        |__debugbar
        |__logs
        |__session
        |__uploads


Folders _vendor_ and _resources_ are added. _vendor_ is used by Composer to store third-party libraries and packages. _resources_ holds images, JavaScript and CSS files. _phenotype_lookup_data_ is used to store phenotype data from the installation and other installations in the same network. __The json files in this folder are essential for the discovery interface to load properly.__