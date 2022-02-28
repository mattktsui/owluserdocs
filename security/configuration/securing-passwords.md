# Securing Passwords

Security is the utmost importance for Collibra DQ and our customers. In order to not send around plain text passwords when owlchecks are executed from the CLI users/admins can encrypt passwords and execute owlchecks using the encrypted passwords instead of plain text.  To encrypt your password execute the command below\


| owlmanage.sh encypt=password |
| ---------------------------- |

The output password will look something like the following\


| Q+Ri1S+ljpG+fDefXLY4/vXtUosspAoL |
| -------------------------------- |

Now you can use this password in any owlcheck from the command line where you would normally place a plain text password.  Example owlcheck with encrypted password in place of plain text password highlighted in bold.\


| ./owlcheck -q "SELECT id, browser->'$.name' browser FROM events" -c "jdbc:mysql://54.212.36.218:2212/test" -u "owl" -p "Q+Ri1S+ljpG+fDefXLY4/vXtUosspAoL" -driver "com.mysql.cj.jdbc.Driver" -lib "/opt/owl/drivers/mysql8" -ds jsonremotemysql -rd "2019-01-28" |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

\
If executing a DQ Job from within the Owl-web the owl-web will automatically encrypt your password for you -- so you do not have to encrypt it. All passwords are masked out of the logs in order not to store plan passwords for security purposes.
