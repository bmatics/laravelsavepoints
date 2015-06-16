# laravelsavepoints
Adds support for save points to database connections in Laravel 5

Add `Bmatics\TransactionSavePoints\TransactionSavePointServiceProvider` to your app's service providers.

To enable save points for a connection, simply add `'savepoints' => true` to the connection config.

When enabled on a connection, beginning a new transaction while another transaction is already active will create a save point.  Beginning additional transactions on the same connection will create additional save points.  Commiting or rolling back on the connection will release or rollback to the last created save point. When all save points have been released or rolled back to, commiting or rolling back on the connection will commit or rollback the entire transaction

The Database must support the following SQL statements:
- `SAVEPOINT [savepoint_name]`
- `RELEASE SAVEPOINT [savepoint_name]`
- `ROLLBACK TO SAVEPOINT [savepoint_name]`
