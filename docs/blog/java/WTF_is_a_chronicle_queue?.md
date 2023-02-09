09/02/2023

## Baeldung's Overview
Chronicle Queue persists every message using a memory-mapped file. This allows us to share messages between processes.

It stores data directly to **off-heap memory**(what then, is off-heap memory), making it free of GC overhead. 
