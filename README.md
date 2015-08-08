# wbimb
What's been in my bag?

This is a short script for single-user Wallabag instances, that allows you to create periodic (daily/weekly/etc.) blog posts that report on what articles you've had in your Wallabag instance.

Disclaimer: this is mostly here for my own reference.  I'll gradually be tweaking to add features.  Use at your own risk.

# Features
* Tracks what you've read, even after the document has been deleted from Wallabag (uses a separate db table).
* Allows you to delete single entries or all entries
* Allows you to preview the output.
* Allos for cut-and-paste of raw HTML

# Installation

Below assumes an existing instance of Wallabag, using a SQLite3 database.

1) In the poche.sqlite database file (used by Wallabag), create a table called "bag", via:

   CREATE TABLE bag (id integer primary key, title text, url text, user_id NUMERIC, stamp datetime);

2) Find/edit Database.class.php and add the following as the first few lines in the "add" function:

   $now = date('Y-m-d');
   $sql_action = 'INSERT INTO bag (url, title, user_id, stamp) VALUES (?, ?, ?, ?)';
   $params_action = array($url, $title, $user_id, $now);
   $this->executeQuery($sql_action, $params_action);

3) Create a folder called "wb" (or whatever) in your web server root.  Download index.php and drop into that folder.

4) Edit index.php so that it has the full path to poche.sqlite (the SQLite3 database used by Wallabag).

# Shortcomings
* Doesn't yet differentiate between users
* For now, requires manual cut-and-paste into your blog

# Feature wish list
* Posting directly to a blog via XMLRPC or similar.
