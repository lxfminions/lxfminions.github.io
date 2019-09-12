---
layout: post
title: JDBC Notes
categories: [it]
tags: [Java, JDBC]
date: 2018-12-08
---
{% include toc.html %}
## Overview
JDBC (Java Database Connectivity) and API provided by Oracle that 
<span style="background-color: yellow" >allows programmers to handle 
defferent databases from Java applications</span>: it allows
developers to establish connection to databases, defines how a specific client
can access a given database, provides mechanisms for reading, updating and deleting entries of data in a database and takes care of transactions composed
of different SQL statements.


## Step by step 
Following below steps, you can make a simple program operate `MySQL` database.
<div class="thi-step">
<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
To load a spicific database driver and get a connection between java code and data source (here is a database).
{% highlight ruby %}
Class.forName("com.mysql.Driver");
Connection conn = DriverManager.getConnection("jdbc:mysql://localhost/countries?" + "user=root&password=root");
{% endhighlight %}
</div>
</div>

<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
Getted a connection
{% highlight ruby %}
Statement stmt = conn.createStatement();
{% endhighlight ruby %}
</div>
</div>

<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
Execute a SQL statement.
{% highlight ruby %}
String sql = "SELECT * FROM TABLE-NAME";
ResultSet rs = stmt.executeQuery(sql);
{% endhighlight ruby %}
</div>
</div>

<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
Deal with the return result 
{% highlight ruby %}
while (rs.next()) {
  rs.getInt();
  rs.getString();
  rs.getDate();
}
{% endhighlight ruby %}
</div>
</div>

<div class="step">
<div class="step-number"></div>
<div class="step-content" markdown="1">
Close the statement session and the connection.
{% highlight ruby %}
stmt.close();
conn.close();
{% endhighlight ruby %}
{% include warning.html content="Must remember to close the connection or session" %}
</div>
</div>
</div>


## Detailed for relative class

### Interface
- `Connection`: A connection (session) with a specific database. SQL statements
 are executed and results are returned within  the context of a connection.
- `PreparedStatement`: An object that represents a precompiled SQL statement.
- `ResultSet`: A table of data representing a database result set.
- `Statement`: The object used for executing a static SQL statement.

### Class
- `DriverManager`: The basic service for managing a set of JDBC drivers.
{% include tip.html content="[More Detail Inforamtion With Oracle.](https://docs.oracle.com/javase/8/docs/api/java/sql/package-summary.html)" %}
## Source Code
Here is the whole JDBC example. 
<ul class="collapsible" data-collapsible="accordion">
<li>
<div class ="collapsible-header" markdown="1"><i class="material-icons">face</i>
Source Code
</div>
<div class="collapsible-body" markdown="1">
{% highlight ruby %}
class SqlTest {
  public static void main(String[] args) throws ClassNotFoundException, SQLException {
    /* Load the mysql driver */
    Class.forName("com.mysql.Driver");
    /* To get connection by calling DriverManager's method */
    Connection conn = DriverManager.getConnection();
    /* To create a Statement to execute sql statement. */
    Statement stmt = conn.createStatement();
    String sql = "SELECT * FROM TABLE";
    /* Executed result stores ResultSets class */ 
    ResultSet rs = stmt.executeQuery(sql);
    while(rs.next()) {
      System.out.println(rs.getInt("id") + " "
        + rs.getString("name") + " "
        + rs.getString("class") + " "
        + rs.getDate("date"));
    }

    /* Close database connection. */
    stmt.close();
    conn.close();
  }
}
{% endhighlight ruby %}
