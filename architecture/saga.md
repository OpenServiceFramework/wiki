# Saga Pattern

A saga is a sequence of local transactions. Each local transaction updates the database and triggers the next local transaction. If a local transaction fails, the saga executes a series of compensating transactions that undo the changes that were made by the preceding local transactions.

## External References

- [Chris Richardson: Sagas](https://microservices.io/patterns/data/saga.html)
- [Google Cloud: Implementing the saga pattern in Workflows](https://cloud.google.com/blog/topics/developers-practitioners/implementing-saga-pattern-workflows)
