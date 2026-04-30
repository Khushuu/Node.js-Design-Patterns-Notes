# How Node.js Works

This section explains how Node.js works inside. It introduces the **reactor pattern**, the **single-threaded event loop**, and **non-blocking I/O**.

## Single Thread and Background Work

Node.js is often called **single-threaded** because the event loop runs on one thread. But Node.js can still use background threads for some operations.

The event loop handles asynchronous tasks on one thread. When CPU-heavy work is needed, Node.js can use separate threads so the event loop stays responsive.

## I/O Is the Bottleneck

I/O means input/output. It is usually the slowest part of a computer program.

- RAM access is very fast, in nanoseconds.
- Disk and network access are much slower, in milliseconds.

I/O is not expensive for the CPU, but it adds a delay between starting a request and finishing it.

Human input, like mouse clicks, can be much slower than disk or network I/O.

Node.js handles I/O efficiently with a **non-blocking, event-driven** design. This keeps the system responsive while waiting for I/O operations.
