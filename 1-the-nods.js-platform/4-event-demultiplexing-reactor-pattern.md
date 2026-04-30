# Event Demultiplexing and the Reactor Pattern

## Event Demultiplexing

Modern operating systems provide a way to wait for many resources at once. This mechanism is called an **event demultiplexer**.

It watches multiple resources and returns events when they are ready.

This is more efficient than busy-waiting because the system blocks until new events arrive.

Example pseudocode:
```
watchList.add(socketA, FOR_READ)
watchList.add(fileB, FOR_READ)
while (events = demultiplexer.watch(watchList)) {
  for (event of events) {
    data = event.resource.read()
    if (data === RESOURCE_CLOSED) {
      demultiplexer.unwatch(event.resource)
    } else {
      consumeData(data)
    }
  }
}
```

This pattern lets one thread handle multiple I/O operations by waiting for events.

## Reactor Pattern

The reactor pattern is the version of this idea used by Node.js.

A handler (callback) is attached to each I/O request. When the event loop sees the event, it calls the handler.

What happens:
1. The application submits an I/O request to the Event Demultiplexer and provides a handler.
2. The non-blocking request returns immediately.
3. When the I/O completes, the Event Demultiplexer adds an event to the Event Queue.
4. The Event Loop processes events from the queue.
5. The handler runs and returns control to the Event Loop.
6. When the queue is empty, the Event Loop blocks again waiting for new events.

This makes asynchronous behavior clear: the app starts an operation now and handles the result later.

A Node.js application exits when there are no pending events or active handles left.

The reactor pattern is different from the proactor pattern. In the reactor pattern, the application reacts when I/O is ready. In the proactor pattern, the system handles the I/O and notifies the app only after it completes.
