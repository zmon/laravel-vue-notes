The article [Two Best Laravel Packages to Manage Roles/Permissions](https://laravel-news.com/two-best-roles-permissions-packages) lead me to
the following comparision.

Option | [Laravel-permission](https://github.com/spatie/laravel-permission#using-multiple-guards) | [Bouncer](https://github.com/JosephSilber/bouncer)
----|----|----
Description | This package allows you to manage user permissions and roles in a database. | Bouncer is an elegant, framework-agnostic approach to managing roles and abilities for any app using Eloquent models.
Developer | Spatie is a web design agency in Antwerp, Belgium. | -
**Multiple Gards** | multiple guards they will act like namespaces for your permissions and roles. Meaning every guard has its own set of permissions and roles that can be assigned to their user model.| May be Scope 
Uses default `can` | Yes | Yes
Dependecies | Lumen | 
CLI | Yes | Only to clean unassigned and orphaned abilities
Unit Testing | Helps |
Database Seeding | example |
Extending | Yes |
Cache | Yes | Yes - Auto **NOTE:** fid not file or database cache drivers.
Cache Refreash |  | Yes, and per user 
User can own a model | ? | Yes
Multi-tenancy | See [A full-featured multi-tenant app with Laravel Part 2 — Roles and Permissions](https://medium.com/@ashokgelal/a-full-featured-multi-tenant-app-with-laravel-part-2-roles-and-permissions-d9a5bfe5d525) and issue[Question: Multi Tenant #280](https://github.com/spatie/laravel-permission/issues/280) both work arounds. | Yes - using Scope Middleware
Can change internal table names | no | Yes







