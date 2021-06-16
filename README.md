# CafeVariomeDocs

This repository contains software documentation for [Cafe Variome](https://github.com/CafeVariomeUoL/CafeVariomeCI4). 

These documents mainly include technical documentation and UML diagrams and explain the various sections of cafevariome based on existence functionalities. The current installation of cafevariome can be done both manually via command line or automatically via ansible which is idempotent and less error prone. For more information regarding the installation please refer to the main github page of cafevariome as stated above. As mentioned earlier, this document explains the functionalities of cafevariome to help cafevariome users to be familiarized from the begining like authentication up to the end such as uploading thier data and creating queries based on the data for data discovery purpose. Thereby, the authentication is the 1st phase that needs to be explained as follows. The rest of finctionalities will be explained accordingly.

## Authentication

After installing the cafevariome, the authentication must be accomplished in order to access to the dashboard. However, the authentication can be done locally or through keycloak which is an open source Red Hat software product to allow single sign-on with Identity and Access Management aimed at modern applications and services. The keycloak can be integrated with ELIXIR AAI to federate identities from ELIXIR to access resources that are provided by cafe variome for data discovery. For distinguishing between various authentication modes, the AuthAdapter.php is used as follows:

*
class AuthAdapter extends \CodeIgniter\Config\BaseConfig
{

    /**
     * Valid values:
     *  1. KeyCloakFirst : If keycloak URI is configured properly and an endpoint exists,
     *  Keycloak is used as authentication engine. Otherwise, IonAuth is used.
     *  2. KeyCloakOnly
     *  3. IonAuthOnly
     *  4. OAuth
     */
    public $authRoutine = 'IonAuthOnly';
}
*