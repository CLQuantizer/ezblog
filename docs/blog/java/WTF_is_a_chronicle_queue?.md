09/02/2023

## Baeldung's Overview
Chronicle Queue persists every message using a memory-mapped file. This allows us to share messages between processes.

It stores data directly to **off-heap memory**(what then, is off-heap memory), making it free of GC overhead. 

## ChatGPT's babble

One of the key advantages of Chronicle Queue is that **it is lock-free**, which means that multiple threads can write to and read from the queue **simultaneously**.

Chronicle Queue also provides a number of features that make it well suited for storing time-series data, such as support for data expiration, data compaction, and data replication. These features help to ensure that the data remains organized and efficient, even as the size of the queue grows over time.