# Chrome

## Removing specific site from history

1. Search where your `History` file is located:

   ```bash
   find . -type f -name History
   ```

   and change into that directory.

2. Open the `History` database with `sqlite3`:

   ```bash
   sqlite3 History
   ```

3. Delete the site from history:

   ```sql
   delete from urls where url like '%foo.bar.net%';
   ```

4. Exit sqlite3:

   ```sql
   .exit
   ```
