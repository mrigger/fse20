# Installation

The artifact consists of two main components:

1. SQLancer, the tool which we created, and in which we implemented NoREC, to find all bugs reported in the paper.
2. A SQLite database with a list of bugs that we reported and additional meta information.

Both components are expected to be usable with minimal effort.

## Video

To help getting started with the artifact, we recorded a video to explain and demonstrate its main functionality. Please consider watching it (see video.mp4).

## SQLancer

SQLancer is a [Java](https://www.java.com/) application built using [Maven](https://maven.apache.org/).

For an up-to-date installation description and source code of SQLancer, please consult the [SQLancer repository](https://github.com/sqlancer/sqlancer/).

As of now, SQLancer requires the following software to be installed:

* [Java 11](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
* [Maven](https://maven.apache.org/install.html)

To download SQLancer, build it, and run NoREC using SQLite, run the following:

```
git clone https://github.com/sqlancer/sqlancer
cd sqlancer
mvn package
cd target
java -jar SQLancer-0.0.1-SNAPSHOT.jar sqlite3 --oracle NoREC
```

It is expected that progress information, similar to the following, is printed:
```
[2020/06/03 22:23:01] Executed 125649 queries (25109 queries/s; 3.20/s dbs, successful statements: 82%). Threads shut down: 0.
[2020/06/03 22:23:06] Executed 318318 queries (38641 queries/s; 0.00/s dbs, successful statements: 82%). Threads shut down: 0.
[2020/06/03 22:23:11] Executed 519601 queries (40264 queries/s; 0.00/s dbs, successful statements: 82%). Threads shut down: 0.
[2020/06/03 22:23:16] Executed 714814 queries (39050 queries/s; 0.00/s dbs, successful statements: 82%). Threads shut down: 0.
```

Using SQLite to evaluate the artifact is most convenient, since SQLite is an embedded DBMS, meaning that the DBMS is included directly within SQLancer using a [JDBC driver](https://docs.oracle.com/javase/tutorial/jdbc/basics/index.html). Note that the latest version of the [SQLite JDBC driver](https://bitbucket.org/xerial/sqlite-jdbc/downloads/) does not include the latest SQLite version, meaning that NoREC could find bugs that have already been fixed on the latest SQLite version.

Besides for SQLite, NoREC is supported also for the following DBMS:
* [CockroachDB](https://github.com/cockroachdb/cockroach)
* [MariaDB](https://github.com/mariadb)
* [PostgreSQL](https://github.com/postgres/postgres/)
* ([DuckDB](https://github.com/cwida/duckdb), where we implemented NoREC after we conducted our initial study. In order to use it, you need to manually build the JDBC driver; the DuckDB developers [are currently working on a Maven artifact](https://github.com/cwida/duckdb/issues/649), which we will include in the camera-ready artifact.)

If you decide to test these, please download and install their latest version, using the instructions on the respective pages.

## SQLite Database

To view the database's content, we recommend using a GUI like [DB Browser for SQLite](https://sqlitebrowser.org/). Alternatively, you can install [SQLite](https://www.sqlite.org/download.html) and use its CLI:

```
sqlite3 bugs.db
sqlite> SELECT COUNT(*) FROM DBMS_BUGS; -- 168
```