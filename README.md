# RoR-notes

Just a stop place to take notes in my backend journey on rails

## 1. Helpful rake for DB migration

* display the status (up or down) of each migration
> rails db:migrate:status

* roll back last migration
>  rails db:rollback

* roll back last x number of migrations
> rails db:rollback STEP=x

* roll back all migrations to specific version
> rails db:migrate VERSION=xxxxxxxxxxxxxx

* roll back only one specific version
> rails db:migrate:down VERSION=xxxxxxxxxxxxxx

* migrate only one specific version
> rails db:migrate:up VERSION=xxxxxxxxxxxxxxAs a best practice, you should always test that rails db:rollback works when you create a migration. You can read more about rails migrations in this doc


## 2. Tip for deleting ********* NO FILE ************** migration in Rails

It might happen sometime when switching around development branches and migration files history doesn't match with its schema in pgsql
especially when I run `rails db:migrate` in a branch with a new migration and switch to another one which doesn't have that migration file.

CMD: `rails db:migrate:status`

```
   up     20230731134140  Create user table
   up     20230731136150  ********** NO FILE **********
   up     20230822190421  Add some attributes to user table
   up     20230906211704  Add description to user
   up     20230915162646  ********** NO FILE **********
```

Try this:
```
rails dbconsole
delete from schema_migrations where version='#{version_number}';
```
> e.g: `delete from schema_migrations where version='20230915162646';`
