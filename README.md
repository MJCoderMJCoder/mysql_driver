* # [Accessing data with MySQL](https://spring.io/guides/gs/accessing-data-mysql/)


# Make some security changes

Now when you are on production environment, you may be exposed to SQL injection attacks. A hacker may inject DROP TABLE or any other destructive SQL commands. So as a security practice, make those changes to your database before you expose the application to users.

`mysql> revoke all on db_example.* from 'springuser'@'localhost';`

This revokes ALL the priviliges from the user associated with the Spring application. Now the Spring application cannot do anything in the database. We don’t want that, so

`mysql> grant select, insert, delete, update on db_example.* to 'springuser'@'localhost';`

This gives your Spring application only the privileges necessary to make changes to only the data of the database and not the structure (schema).

When you want to make changes on the database, regrant the permissions, change the spring.jpa.hibernate.ddl-auto to update, then re-run your applications, then repeat. Or, better, use a dedicated migration tool such as Flyway or Liquibase.