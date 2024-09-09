Thursday, August 29 2024

# Changing the database from postgresql to mysql (mariadb) and finishing up

So the requirement was to use mysql instead of postgresql since all the other infrastucture relied on it, it was unwise to maintain two different databases seperately, therefore i changed the database to mysql.


This was the new database class which fulfilled new requirements:


```cpp

class DatabaseManager {
public:
    // Constructor
    DatabaseManager(const string& host, const string& user, const string& password, const string& dbname);

    // Destructor
    ~DatabaseManager();

    // Method to execute a query
    void executeQuery(const string& query);

private:
    sql::Driver *driver;
    sql::Connection *con;
    string host;
    string user;
    string password;
    string dbname;
};


```



The syntax for initializing the constructor also needed to be changed, which i did and tested. It worked fine.


# Compilation on ARM

ARM64 (also known as aarch64) is quite different from AMD64, however the code i wrote was not architecture specific.

I attempted to cross compile but it was not possible to install aarch64 packages on an X86 system, neither did i had access to a ARM machine, nor it was viable to do on an ARM machine since it would take a lot of time.

The solution? a virtual machine.


I set up an ARM virtual machine and installed debian 12 ARM version on it.

After cloning the repostiroy, i ran into an issue while compilation.

the path for libraries on X86 system is: /usr/lib/x86_64-linux-gnu

and for ARM64 it is: /usr/lib/aarch64-linux-gnu

To improvise, i edited the Makefile to have this:

LIB_DIRS = /usr/lib/*-linux-gnu


It solved my issue and i was finally able to compile on an ARM version. After testing it worked.
