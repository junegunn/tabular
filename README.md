tabular.vim
===========

Forked from https://github.com/godlygeek/tabular.

Change #1: Extended format
--------------------------

Extended format so that we can limit the number of cells of each line to be processed.

=== Why
In the following example, the additional colons in the third line should not be
considered as cell-delimiters.

```yaml
mysql:
  driver: com.mysql.jdbc.Driver
  url: jdbc:mysql://localhost/test
  database: test
```

Which means, we want

```yaml
mysql:
  driver:   com.mysql.jdbc.Driver
  url:      jdbc:mysql://localhost/test
  database: test
```

and not,

```yaml
mysql:
  driver:    com.mysql.jdbc.Driver
  url:       jdbc:                  mysql:  //localhost/test
  database:  test
```

=== How

Put this line into your .vimrc

```vim
" Specify the number of cells after the dash
let g:tabular_default_format = "l1-1"
```

Change #2: Better tabularization in visual mode
-----------------------------------------------

=== Why

For the following case, where comments are interleaved,
you might want to tabularize the lines in visual mode.

```yaml
mysql:
  # JDBC driver for MySQL database
  driver: com.mysql.jdbc.Driver
  # JDBC URL for the connection
  url: jdbc:mysql://localhost/test
  database: test
  user: root
  # password: r00t
```

Select all the lines in visual mode then, `:'<,'>Tab /:\zs`
Then, the result should be

```yaml
mysql:
  # JDBC driver for MySQL database
  driver:      com.mysql.jdbc.Driver
  # JDBC URL for the connection
  url:         jdbc:mysql://localhost/test
  database:    test
  user:        root
  # password:  r00t
```

instead of,

```yaml
mysql:
  # JDBC driver for MySQL database
  driver:                           com.mysql.jdbc.Driver
  # JDBC URL for the connection
  url:                              jdbc:mysql://localhost/test
  database:                         test
  user:                             root
  # password:                       r00t
```

