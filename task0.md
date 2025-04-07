# Task 0 (23 points)

## Answer the following questions in details:

1. What are the differences between testing and debugging?\
Testing is used to estimate the quality of software and find bugs to check if the software meets the requirements for use. We try to reveal the failures. Testing is periodic or can last throughout the software's lifetime. Every time there is a new update, there will be a new round of testing.\
Debugging is the step after we find some failures. We try to debug to identify the cause and fix it. This can be done by reading logs or setting checkpoints. Debugging is triggered after we find failures through testing. The goal of debugging is to fix the code.

2. How testing and debugging complement each other?\
They complement each other for:
    - Testing will find the failure, and the failure tells you how you are going to debug and fix it. When you are done debugging, you want to do another round of testing to see if the debugging was successful.
    - Testing → Find Failure → Debug and Fix → Testing again.
    - Testing will focus on a broad area of functionalities or boundaries. Then debugging will focus on the deep reason why the bug happens and try to solve it.

3. Is testing necessarily a prerequisite of debugging? Explain.\
In general, you need testing to identify which part of the app is abnormal. Failures are usually discovered through testing. Without testing, you don't know where the bug is. Thus, it is always strongly recommended to perform testing before debugging. However, a developer may find problems without testing and can start debugging directly. For example, if you realize you implemented something in the wrong file, you don't need testing to begin debugging.

4. The original ddmin() algorithm finds only one possible 1-minimal input i.e. an input where removing any single character makes the failure disappear. Sketch an extension of ddmin() algorithm named ddminAll() that finds ALL possible 1-minimal inputs.
    - ddmin(): Based on "dichotomy" and minimizes the size of the input while preserving the failure. It finds one 1-minimal input, then stops without exploring other possibilities.
    - Assume we divide the input into two blocks. Then we test each block to check whether block 1 or block 2 alone can still reproduce the failure.
    - We then continue dividing and iterating.
    - For ddmin(), if we find blocks that can be deleted, we delete them. For ddminAll(), we need to keep trying different combinations to find all possible 1-minimal inputs.
    - Thus, we need to maintain a set of results. In ddminAll(), we don't just delete the block; we create a new branch and keep iterating and dividing to find other 1-minimal inputs. When a block can no longer be removed, we have found a 1-minimal input, which we then add to the result set. We continue searching in other branches.
    - In the end, we obtain the final result of ddminAll().



    - ddmin(): Based on "dichotomy" and minimize the size of input to keep the failures. It find the 1-minimal input, then it will stop reaching for other possibilities. 
    - Assuming we have divide input into 2 blocks. Then we test through all the blocks, in this case we test to check if block 1 or block 2 can keep the failure. 
    - Then we keep divide and iterate. 
    - For ddmin(), If we find some blocks to delete, then delete it. For ddminAll(), we need to keeping trying different combinations to find all the ddmin. 
    - Thus we need to keep a set of result. For ddminAll(), we don't just delete the block. We create a new branch, then keep iterate and divide it to find other ddmin. When the block cannot be removed, we get a ddmin, then we add it to the set of results. Then we keep searching on other branches. 
    - Then we get the final result of ddminAdd().

5. Why throughput is a valuable and important metric when it comes to load testing? Explain clearly with at least two reasons.
    - The definition of throughput is the amount of requests/data a system can handle within a certain period.
    - Reason 1: Throughput represents the system's capacity and efficiency. Higher throughput allows the system to better handle peak hours and manage larger datasets. If throughput decreases drastically, it indicates the system is facing a bottleneck.
    - Reason 2: Throughput is complementary to response time. A common understanding is that throughput and response time are the two most important factors in load testing. Throughput tells you how many requests the system can handle per second, while response time tells you how quickly each request is handled. When the load and throughput are increasing but the response time becomes significantly slower, it suggests that the system is reaching its limit.