# Event Sourcing Pattern

Event sourcing persists the state of a business entity such an Order or a Customer as a sequence of state-changing events. Whenever the state of a business entity changes, a new event is appended to the list of events. Since saving an event is a single operation, it is inherently atomic.

## External References

- [Chris Richardson: Event Sourcing](https://microservices.io/patterns/data/event-sourcing.html)
- [Microsoft: Event Sourcing pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing)
- [Evaluate: Event Sourcing](https://eventuate.io/whyeventsourcing.html)
