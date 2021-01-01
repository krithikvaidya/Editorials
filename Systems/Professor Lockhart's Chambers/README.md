# Professor Lockhart's Chambers

## Problem Statement

Professor Lockhart claims that his chamber has the best security measures in place, and constantly brags about it to Professor Flitwick. Flitwick, getting annoyed with this, decides to use his intellect and put the chamber's defenses to the test. He begins looking for security vulnerabilities in his chamber. Pretty soon, he discovers that there is a flaw in the screening mechanism of the chamber, and it does not correctly screen all the people trying to enter (i.e., it does not sanitize SQL inputs, which means it is prone to SQL injection attacks).

The chamber entry door works very similarly to a website that contains a login form. On entering the username + password details, the user gains access to the chambers. The chamber's code for obtaining the user details (which is used for verification), based on information entered in the login form is the following:

```user_details = "SELECT * FROM users WHERE username='" + uname + "' AND password='" + passwd + "'"```

where _uname_ is the username entered in the login form, and _passwd_ is the corresponding password.

The above is prone to SQL injection attacks, as we can set the _passwd_ field to something like:

```password' OR 1=1```

As a result, the database server runs the following SQL query:

```SELECT * FROM users WHERE username='username' AND password='password' OR 1=1'```

Leading to the second part of the AND clause being always evaluated as True, even if the password is wrong since 1=1 always. This enables anyone to get past the screening mechanism, without even knowing the right password.

Using the above login form, what will be the input to the password field form so that Professor Flitwick can delete Professor Lockhart's own record from the database, thereby barring him from entering his own chambers?

(Hint: Use the SQL _DELETE_ statement)

Note: Each - in the code snippet below denotes a blank of 1 character. Fill in the blanks. Use standard SQL syntax (single quotes for strings, etc). Assume Professor Lockhart's username is 'Lockhart' (without the quotes). Do not use backticks (`) anywhere.

## [Editorial Solution](Algorithms/template/answer-template.md)

The problem is a straightforward [SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection) problem. The following input to the _passwd_ field would cause an SQL injection attack, deleting Professor Lockhart's row from the database.

```'; DELETE FROM users WHERE username='Lockhart';```

The BASH code expected to be filled was:

```echo "'; DELETE FROM users WHERE username='Lockhart';"```