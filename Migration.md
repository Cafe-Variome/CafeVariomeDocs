# Migration to Code Igniter 4 and Bootstrap 4 #

**Mehdi Mehtarizadeh**

Migration to CodeIgniter 4 and Bootstrap 4 is necessary at the time of writing. Current CodeIgniter and Bootstrap are obsolete. There are challenges to move the code as the software lacks *technical* and *architecture design documentation*. On the backend side upgrading the code to PHP 7 requires effort. There are major differences in the structure of CodeIgniter 2 and CodeIgniter 4. Moreover, heavy user interfaces currently deployed are dependant on Bootstrap 2. The migration of Bootstrap is expected to bring more unwanted challenges and therefore requires more effort.    
## User Interface Migration ##
---
The user interface benefits from Bootstrap 2.0.2. At the time of writing this report version 4.3.1 is out.

## Back-end Migration ##
---
The core software is written in PHP 5.5. It is expected that some incompatibilities occur as the move to CodeIgniter4 is made.

## Data Migration ##
---
Data migration in its true essence is not needed as MySQL will be deployed as the main database management system for CafeVariome. The installation software in [Cafe Variome V2](https://github.com/CafeVariomeUoL/CafeVariomeV2) creates 64 databases. According to current team developers, less than 20 tables are in actual use. Current developers suggest to make the move with necessary tables (users, pages, menus, preferences, ...) and then move the rest of the tables if necessary.

