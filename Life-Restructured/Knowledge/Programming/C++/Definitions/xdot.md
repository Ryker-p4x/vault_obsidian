You can use this to see the compiler's internal graph representation of a block of .dot files that can be generated using flags like -fdump-tree-all-graph

**Use cases:**
1. Understanding compiler internals better
2. Can be useful if you're building your own compiler to use this to catch bugs
3. You can see the intermediate representation to see how a compiler interpreted the code and optimized a complex branch, loop or template metaprogram
4. Reverse engineers and security analysts use Control Flow Graph to see how the compiled binary executes stuff which can help in finding bugs or analyzing malware.