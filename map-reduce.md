# MapReduce Summary

## Source

[click here](https://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf)

## Summary

### Introduction

The paper introduces an innovative approach to processing and generating large data sets with a distributed algorithm, known as MapReduce. The authors, Jeffrey Dean and Sanjay Ghemawat, outline the framework's capability to simplify data processing across distributed systems.

### Key Concepts

- **MapReduce Framework:** Describes the architecture and operational flow of the MapReduce framework, highlighting its ability to automatically parallelize in different machines and execute processes across a large-scale distributed environment.
- **Map and Reduce Functions:** Details the implementation and functionality of 'Map' and 'Reduce' functions within the framework, including data input, processing, and output stages.
- **Use Cases:** Word Counter, Distributed Grep, Count of URL Access Frequency, Reverse Web-Link Graph, Term-Vector per Host, Inverted Index, Distributed Sort
- **Master and Worker:** The master assign a task(map and reduce) to each worker.
- **Fault Tolerance:** The master pings every worker periodically. Any map task or reduce task in progress on a failed worker is also reset to idle and becomes eligible for rescheduling. If master fails, user is able to retry the MapReduce operation if they desire.
- **Atomic Commits on Map Task:** When a map task is done, the worker sends a note to the the master saying, "I finished this, and here's where I put the work." If the master already has a note for that task, it ignores the new one.
- **Atomic Commits on Reduce Task:** When a reduce task is done, the worker carefully replaces the temporary note on the board with a permanent one. If the same task ends up being done more than once, we only keep one set of work to avoid duplicates, thanks to atomic rename that ensures we only have one final version.
-  **Deterministic:** Most of the time, tasks are deterministic, meaning if you do the same work again with the same information, you'll get the same result. This makes it easy for programmers to predict what their program will do.
-  **Non-Deterministic:** Sometimes, tasks can give different results even with the same input, due to randomness or other factors. In these cases, MapReduce still tries to make sure the work makes sense, but the final outcome might be based on different executions of the tasks.
-  **Locality:** To avoid network issue, the input data and output data of map task store in local disks. However, the final outputs of reduce task store in cloud storage.
-  **Backup Task:** "Straggler" operation, a machine that takes an unusually long time to complete one of the last few map or reduce tasks in the computation, is able to solve by the master schedules backup executions of the remaining in-progress tasks. The task is marked as completed whenever either the primary or the backup execution completes.

### Implementation

The paper provides insights into the practical implementation of the MapReduce framework, including optimizations for performance and scalability. It also presents case studies showcasing the framework's application in various Google projects, demonstrating its effectiveness in real-world scenarios.

-  **Performance:** Demonstrated through a grep example and a sort example, showcasing the system's ability to handle terabytes of data efficiently.
-  **Experience:** MapReduce has been widely adopted within Google for a variety of tasks, including machine learning, data processing for Google News, and large-scale graph computations, demonstrating its flexibility and power.
-  **Large-Scale Indexing :** The use of MapReduce in rewriting Google's production indexing system, noting significant improvements in simplicity, maintainability, and operational ease.

### Conclusion

MapReduce is presented as a powerful tool for data processing, offering significant advantages in terms of scalability, efficiency, and reliability. The authors conclude that the framework meets the growing demands of processing large data sets in distributed environments, making it a valuable asset for developers and organizations.
