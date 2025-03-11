# Module 5 

## Introduction 

This project focuses on optimizing the performance of a Spring Boot application, forking https://github.com/muhammad-khadafi/exercise-profiling, by using performance testing with JMeter and profiling with IntelliJ Profiler. The goal was to identify and resolve bottlenecks in the application, improving the CPU time.

## Tutorial and Exercise

### Performance Testing 

#### JMeter Apache GUI

##### /all-student-name

| Listener Name | Result Image | 
| ------------- | -----------  |
| View Results Tree | ![Screenshot 2025-03-11 051807](https://github.com/user-attachments/assets/7408f99a-15f1-4874-a71b-f6d0bbeacecf) | 
| View Results in Table |  ![Screenshot 2025-03-11 051813](https://github.com/user-attachments/assets/5f1947be-cb86-44d9-8779-e07d48fb29c8) | 
| Summary Report | ![Screenshot 2025-03-11 051820](https://github.com/user-attachments/assets/cd8823c6-3a28-4393-b2b6-acb60d184aad) |
| Graph Result |  ![Screenshot 2025-03-11 051828](https://github.com/user-attachments/assets/d9b9edd9-67f2-4a06-be4d-e0238819319e) |

##### /highest-gpa

| Listener Name | Result Image | 
| ------------- | -----------  |
| View Results Tree | ![Screenshot 2025-03-11 051704](https://github.com/user-attachments/assets/47702751-2031-44b7-8f25-368709be2e07) | 
| View Results in Table | ![Screenshot 2025-03-11 051715](https://github.com/user-attachments/assets/4ac4aae4-2458-41ae-a069-1f62e2eb2429) | 
| Summary Report | ![Screenshot 2025-03-11 051724](https://github.com/user-attachments/assets/18c83e58-d859-4490-9812-a243843ab74f) |
| Graph Result | ![Screenshot 2025-03-11 051732](https://github.com/user-attachments/assets/d989e064-c3ec-4b75-8198-095cc3a18997) |

#### Command Line

##### /all-student-name

| Command Line | Log File Results |
| ------------ | ---------------- |
| ![Screenshot 2025-03-11 050959](https://github.com/user-attachments/assets/533e37af-5d5b-465f-9b80-2a82bd6eccdf) | ![Screenshot 2025-03-11 051047](https://github.com/user-attachments/assets/c6cc180c-639f-422e-a67b-07dcbd4e93a7) |

##### /highest-gpa

| Command Line | Log File Results |
| ------------ | ---------------- |
| ![Screenshot 2025-03-11 051208](https://github.com/user-attachments/assets/4ba418b5-4e5c-4294-980f-0b673832b469) | ![Screenshot 2025-03-11 051230](https://github.com/user-attachments/assets/e1d78039-455c-4933-93be-0d5a68c28ce9) | 


### Profiling 

#### Optimizations Implemented 

1. **Optimization of `joinStudentNames()` Method**
    - Issue: The `joinStudentNames()` method took **1453 ms CPU Time** due to the use of string concatenation that could be inefficient by `+=`
    - Solution: Replaced the string concatenation with `String.join()` and `stream().map()`
    - Result: Execution time reduced by 95%, now executes for **71ms CPU Time**
![Screenshot 2025-03-11 061517](https://github.com/user-attachments/assets/a99131b6-d803-4879-9dd5-9cb3ec18d358)

2. **Optimization of `findStudentWithHighestGpa()` Method**
    - Issue: The method retrieved all students and processed them in Java, taking **108ms CPU Time**.
    - Solution: Moved the filtering logic to the database using an optimized query with `ORDER BY gpa DESC LIMIT 1`.
    - Result: Execution time reduced by 78%, now executes for **24ms CPU Time**
![Screenshot 2025-03-11 062407](https://github.com/user-attachments/assets/8be6e5a3-8568-4497-9d6f-4e02af4c7c0e)

#### JMeter Apache Optimization Comparison

##### /all-student-name

| Listener Name | Result Image Before | Result Image After |
| ------------- | ------------------  | ------------------ |
| View Results in Table |  ![Screenshot 2025-03-11 051813](https://github.com/user-attachments/assets/5f1947be-cb86-44d9-8779-e07d48fb29c8) | ![Screenshot 2025-03-11 063028](https://github.com/user-attachments/assets/bc759311-4fac-440f-a8d9-9ad0db622c65) |
| Summary Report | ![Screenshot 2025-03-11 051820](https://github.com/user-attachments/assets/cd8823c6-3a28-4393-b2b6-acb60d184aad) |![Screenshot 2025-03-11 063034](https://github.com/user-attachments/assets/f8277273-5dca-4e78-8518-c94879fa682e) |

##### /highest-gpa

| Listener Name | Result Image Before | Result Image After |
| ------------- | ------------------  | ------------------ |
| View Results in Table | ![Screenshot 2025-03-11 051715](https://github.com/user-attachments/assets/4ac4aae4-2458-41ae-a069-1f62e2eb2429) | ![Screenshot 2025-03-11 063058](https://github.com/user-attachments/assets/be1036a2-ec20-4040-a0f5-86cec234d6b9) |
| Summary Report | ![Screenshot 2025-03-11 051724](https://github.com/user-attachments/assets/18c83e58-d859-4490-9812-a243843ab74f) | ![Screenshot 2025-03-11 063105](https://github.com/user-attachments/assets/4a74f884-e740-41b0-8592-72778c619cab) |

As you can see, by comparing before and after profiling on **/all-student-name** and **/highest-gpa**. We can see that **there is an improvement**. Through profiling and performance testing, the application experienced significant performance gains. By optimizing string operations and database queries, execution time was reduced drastically as seen in the Summary Report Listener, ensuring better efficiency and scalability.

### Reflection

1. **What is the difference between the approach of performance testing with JMeter and profiling with IntelliJ Profiler in the context of optimizing application performance?**
    - JMeter: Simulates multiple concurrent users to measure how the application handles load and overall performance under stress.
    - IntelliJ Profiler: Identifies specific performance bottlenecks at the code level by analyzing CPU usage, memory consumption, and method execution times.
    - Key Difference: JMeter focuses on overall system behavior, while IntelliJ Profiler provides detailed insights into inefficient code execution.

2. **How does the profiling process help you in identifying and understanding the weak points in your application?**
Profiling exposed inefficient string operations in `joinStudentNames()` and unnecessary data fetching in `findStudentWithHighestGpa()`. And by the tutorial, helped on optimizing `getAllStudentWithCourses()`.  Without profiling, these bottlenecks would have been difficult to pinpoint.

3. **Do you think IntelliJ Profiler is effective in assisting you to analyze and identify bottlenecks in your application code?**
**Yes**, it can be concluded that IntelliJ Profile is effective. IntelliJ Profiler proved to be highly effective in:
    - Identifying slow methods with high CPU usage.
    - Visualizing the flame graph to better identify slow methods.
    - Providing stack traces for method execution.
    - Comparing each profile run to ease differentiating between optimized code

4. **What are the main challenges you face when conducting performance testing and profiling, and how do you overcome these challenges?**

     The main challenges that I faced is when doing Performance Test, sometimes the results differ in JMeter as it is in Postman. The time needed to execute the GET request sometimes is higher in JMeter than it is in Postman. To overcome this, I had to cross-validate between those two and check the actual load testing in JMeter. The next challenge is upon executing the Profiler test in IntelliJ Profiler, the time taken to execute `getAllStudentsWithCourses` is not fast. So, to overcome this, I just had to optimize the method right away.

5. **What are the main benefits you gain from using IntelliJ Profiler for profiling your application code?**

     The main benefits that I gain from using IntelliJ Profiler is how easy it is to set up since I have been using IntelliJ IDEA for the whole Advanced Programming Course. I didn't have to download anything, let alone just click one button to run. IntelliJ Profiler is also easy to use without sacrificing any performance whatsoever, it allows for precise method-level analysis but keeping it at a beginner-level. In addition, it can even enable real-time performance tracking as used, paired with Postman, making it easier to optimize code.
   
6. **How do you handle situations where the results from profiling with IntelliJ Profiler are not entirely consistent with findings from performance testing using JMeter?**

    When the results from IntelliJ Profiler and JMeter don’t match, I take the following steps:

    a. Compare CPU time vs. request latency
   
   - IntelliJ Profiler mainly measures CPU execution time, while JMeter evaluates end-to-end response time (which includes network latency).
   - If JMeter shows high latency but IntelliJ Profiler doesn’t indicate a CPU bottleneck, the issue may be I/O delays, garbage collection, or database queries. Analyze method execution times vs. thread contention

    b. Analyze method execution times vs. thread contention

   - IntelliJ Profiler highlights slow methods, but it doesn’t always account for multi-threading issues (e.g., too many concurrent requests causing thread contention).

    c. Run multiple test scenarios to find common performance trends

    - If IntelliJ Profiler and JMeter disagree under heavy load, I consider resource contention, memory pressure, or database connection pool saturation as possible causes.

7. **What strategies do you implement in optimizing application code after analyzing results from performance testing and profiling? How do you ensure the changes you make do not affect the application's functionality?**

    Once bottlenecks are identified, I optimize code systematically while ensuring no unintended side effects:

    a. Optimize one bottleneck at a time and measure the impact

    - Instead of making multiple changes at once, I focus on one optimization, then rerun performance tests.
    - Example: If string concatenation in a loop is slow, I replace it with StringBuilder, then measure if the improvement is significant before moving on.

    b. Write unit tests to ensure functional correctness after optimizations

    - Before making changes, I write unit tests to verify the correctness of existing logic.
    - After optimization, I rerun the tests to confirm no unintended functional changes.

    c. Monitor database queries to avoid overloading the DB after moving logic from Java to SQL

    - Some performance fixes involve pushing logic from Java to SQL queries (e.g., using JOIN instead of multiple queries).
    - I check query execution plans (`EXPLAIN ANALYZE` in PostgreSQL) to ensure changes improve efficiency rather than adding DB overhead.
   
