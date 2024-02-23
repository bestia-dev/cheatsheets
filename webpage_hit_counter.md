# webpage_hit_counter

## psql over SSH

From my computer I can in one single command connect to ssh and execute an SQL statement.

```bash
ssh luciano_bestia@bestia.dev " psql -h localhost -p 5432 -U admin -W -d webpage_hit_counter -c 'select A.webpage, B.count from webpage A join hit_counter B on B.webpage_id=A.id order by B.count desc;' "


```

## psql command

I plan to make a web interface for manipulating data in webpage_hit_counter. But this project takes a lot of time.  
There must be a backend app and a frontend app and something sane in between. Then it must have a good authentication and authorization module.
This takes time to develop and it is not funny and amusing.  
In the mid-time I need to work with the database. I can do all the things in psql easy, but manually.  
Some code for psql:

``` psql
// enter psql
psql -h localhost -p 5432 -U admin -W -d webpage_hit_counter
// and then enter the password.

// First rule: the sql statements must end with a semicolon ;
// strings are delimited by a single quote, never by a double quote

// warning: the `like` clause is case sensitive by default
// to show all tables:
\dt

// list the most visited webpages
select A.webpage, B.count from webpage A join hit_counter B on B.webpage_id=A.id order by B.count desc;

// to finish the scrolling of long lists press just q enter
q

// run this 2 commands together to insert a new webpage:
insert into webpage (id, webpage) values(627386887, 'page_name');
insert into hit_counter (webpage_id,count)
select id,2
from webpage A
where A.id not in (select webpage_id from hit_counter);

// run this 2 commands together to delete a webpage:
delete from hit_counter where webpage_id=674042962;
delete from webpage where id = 674042962;

// exit psql
\q
```

