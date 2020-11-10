Databases

- **Redis** - This is stored in memory and is ridiculously fast. However, it is only for measured data (you know exactly how much is going to be stored). If you put to much in, you could run out of memory. Note that "too much" is probably going to be unfeasible for most people. If you're into PHP, it can replace Memcached.

- **MySQL** - PHP developers love this. End of story. It is short of new features and doesn't have much else to say. It is almost entirely SQL compliant to the spec. It doesn't have many new and cool data types or management features. This has a paid version that is usually required in production.

- **MariaDB** - A new DB built off of MySQL. It is said to be faster. I would suggest trying it first instead of MySQL instead of MySQL first. It also has better support/help available.

- **MongoDB** - It is the most JavaScript friendly because it use JSON for storage. However, it is much slower than the others. I had trouble setting it up on my 32-bit computer while enabling all features. I still don't understand that limitation. A shared opinion is that it is "bloated." It really is.

- **PostgreSQL** - It is slowly emerging again. It is a champion of data integrity and has been trusted for a very long time. People got away from it when they found MySQL to be faster. However, it really isn't much slower. MySQL is more of "plug and play" for configuration. If you want Postgre to run fast, you have to set it up correctly. Don't worry though, a developer environment shouldn't need the complicated configs. I really favor Postgre for a standard database (tables). It's got some awesome new data types! JSON was mentioned below, it has the best number support, data integrity, CPU allocation, and MUCH more. Just Google it. Don't be put off that SQL helpers and such in NodeJS don't have support for it! It uses mostly standard SQL commands, so any app that sends SQL to MySQL should be able to use it. The main differences are in the connection, database groups, users/groups, and permissions.

- **SQLite** - This is just a database in a file. It is very limited at functions, but is great for very small things with small capacity (i.e. Raspberry Pi). IT can really only handle one connection at a time. There is no server. The permissions on the file are its security.

- **CouchDB** - It is JavaScript friendly like Mongo. It uses JSON for storage, HTTP for requests, and JavaScript for tasks. It's cool, but it I'm not sure about performance when compared to PostgreSQL, MySQL, and MariaDB. It has a versioning feature, so lots of data change will use up disk space fast!

- **Cassandra** - It's built in Java and is best at storing extremely large things. I have never used it and have no opinion on it. I haven't ever had a need for it.

- **JSON File** - How much do you really need to store? How fast do you need it? How many applications will use it? If it isn't too too much data, this is a better option than SQLite. I'm sure there are some NPM libraries that handle it for you. I usualy just use fs-extra, async, and my own functions. It is extremely easy.

Databases that I've looked into but plan to test in the future: Riak, Couchbase, VoltDB, HBase, and ElasticSearch. Riak is know for ultimate security, Couchbase is the old Membase, and ElasticSearch and HBase are normally for search engine type stuff.
