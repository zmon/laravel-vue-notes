The article [Two Best Laravel Packages to Manage Roles/Permissions](https://laravel-news.com/two-best-roles-permissions-packages) lead me to
the following comparision.

Option | [Laravel-permission](https://github.com/spatie/laravel-permission#using-multiple-guards) | [Bouncer](https://github.com/JosephSilber/bouncer)
----|----|----
Description | This package allows you to manage user permissions and roles in a database. | Bouncer is an elegant, framework-agnostic approach to managing roles and abilities for any app using Eloquent models.
Developer | Spatie is a web design agency in Antwerp, Belgium. | -
**Multiple Gards** multiple guards they will act like namespaces for your permissions and roles. Meaning every guard has its own set of permissions and roles that can be assigned to their user model.| Yes |
Uses default `can` | Yes | 
Dependecies | Lumen | 
CLI | Yes |
Unit Testing | Helps |
Database Seeding | example |
Extending | Yes |
Cache | Yes |





