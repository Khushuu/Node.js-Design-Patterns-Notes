# Blocking I/O vs Non-blocking I/O

## Blocking I/O

In blocking I/O, a function waits until the operation finishes before continuing.

Example:
```
data = socket.read()
print(data)
```

A server using blocking I/O cannot handle multiple connections on the same thread. Each I/O operation blocks the thread.

Traditional solutions use one thread per connection. This avoids blocking other connections, but threads consume memory and CPU time.

Using many threads can waste resources because most of the time threads wait for I/O.

## Non-blocking I/O

Non-blocking I/O returns immediately even if the data is not ready.

If no data is available, the call returns a special value like `NO_DATA_AVAILABLE`.

A simple non-blocking loop looks like this:
```
resources = [socketA, socketB, fileA]
while (!resources.isEmpty()) {
  for (resource of resources) {
    data = resource.read()
    if (data === NO_DATA_AVAILABLE) {
      continue
    }
    if (data === RESOURCE_CLOSED) {
      resources.remove(i)
    } else {
      consumeData(data)
    }
  }
}
```

This works, but it wastes CPU time by repeatedly checking resources that are not ready.

A better method is to use the operating systems event notification interface.
