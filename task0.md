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

4. The original ddmin() algorithm finds only one possible 1-minimal input i.e. an input where removing any single character makes the failure disappear. Sketch an extension of ddmin() algorithm named ddminAll() that finds ALL possible 1-minimal inputs.\
    - ddmin(): Based on "dichotomy" and minimize the size of input to keep the failures. It find the 1-minimal input, then it will stop reaching for other possibilities. 
    - 

 

4.2 ddminAll() 算法的思路与伪码示例
这里展示一个简要思路，假设我们处理的输入是线性的、可拆分为片段（字符序列）的形式：

初始设置

设当前的故障输入为 input。

我们将 input 分成若干片段（如 2 块或更多），并测试各个子集是否能保持故障。

递归或迭代搜索

与 ddmin() 相似地尝试去掉部分片段测试故障是否依然可重现。

如果移除某块后依然触发故障，说明这块对故障不是“必要”的，可将其去除；否则说明这块是“必要”的。

在原 ddmin() 中，一旦找到并删除这些块后，就继续向下缩减；但对“所有 1-最小输入”来说，我们需要在已确定“必要”部分的基础上，继续尝试不同组合，以发现其它可能的最小化方案。

维护候选结果的集合

在每次确定一块并非必要时，都产生一个新候选分支，继续在该分支上递归搜索最小输入。

同时，对保留块进行进一步拆分或二分，测试更小粒度的删除可能性。

当没有块可以再被移除时，就得到一个1-最小输入；把它加入结果集中，但不要停止搜索，因为还可能存在其它删除组合。

去重或合并等价结果

对得到的所有1-最小输入，可能需要根据问题定义对重复或等价结果进行合并或排重。

伪码示例 (简化)
python
Copy
Edit
def ddminAll(input):
    results = set()
    # 如果 input 在最小程度上无法再删去任何一个字符而保持失败，即为1-最小
    if is_1_minimal(input):
        results.add(input)
        return results

    # 否则，先分块
    n = 2
    while n <= len(input):
        chunks = split_into_n_chunks(input, n)
        foundNewCase = False
        for chunk in chunks:
            newInput = input - chunk  # 删除该chunk
            if test(newInput) == FAIL:
                # 如果故障依旧
                # 递归继续缩小
                foundNewCase = True
                results.update(ddminAll(newInput))
        if foundNewCase:
            # 如果成功删除了一些块，就不需要进一步增加n，
            # 因为我们是要先尽量减少输入再做进一步搜索
            break
        else:
            n = n * 2
    return results
注意：这是一个极其简化的示意思路，实际实现会更复杂。例如需要考虑不止二分分块、重复检测、分块策略等。



5. Why throughput is a valuable and important metric when it comes to load testing? Explain clearly with at least two reasons.\

为什么吞吐量 (Throughput) 在负载测试 (Load Testing) 中非常重要？
吞吐量通常指单位时间内系统处理的请求数、数据量或事务量，是衡量系统在并发场景下整体处理能力的关键指标。在负载测试中，它的重要性主要体现在：

衡量系统整体容量与效率

吞吐量高意味着系统每秒能够处理更多用户请求或更大数据量，有助于评估系统的可扩展性和峰值应对能力。

如果吞吐量明显下降，说明系统可能存在严重的性能瓶颈，且在高并发环境下容易导致响应时间激增或用户无法正常访问。

与响应时间等指标相辅相成

通常在负载测试时需要同时看响应时间与吞吐量两项指标：吞吐量能告诉你系统在一秒内成功处理多少请求，响应时间则告诉你每个请求被处理的速度。

如果想让更多用户并行访问系统，而又希望单个用户的体验不受过多影响，就需要在吞吐量和响应时间之间进行平衡。

当负载持续增加，吞吐量若保持增长但响应时间飙升，这说明系统已经逼近或超过其容量上限。

业务价值

对需要并发访问（如电商网站、金融交易系统、政府门户等）的业务而言，吞吐量直接决定了系统能否支撑预期的业务规模。

当吞吐量不足时，系统经常出现排队、超时等情况，导致用户体验恶化和潜在经济损失。