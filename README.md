### Hi there 👋


**Halukisan/Halukisan** 前后端开发工程师，常用MVC和DDD架构，熟悉SpringBoot和Vue，目前对大模型很感兴趣。你可以在Neuproject中看到我敷衍学校所写的作业，First中存放着所有学习编程的过程中所记下的笔记，MyBoke中存放着博客的源码。

There have some tips that can help you learn about me: 
- 🔭 I’m currently working on xFusion
- 🌱 I’m currently learning LLM
- 🤔 I’m looking for help with LLM
- 📫 How to reach me: 2162408515@qq.com

### **Interest**

喜欢大模型相关的内容，尝试过调用ChatGLM大模型API来开发前后端分离的项目，想要自己训练一个大（小）模型。
[Mistral](https://modelscope.cn/models/TabbyML/Mistral-7B/summary)在各方面的评分非常好，仅次于[ChatGLM3 6B](https://modelscope.cn/models/ZhipuAI/chatglm3-6b/summary)的表现,详细请参考(数据学习)[https://www.datalearner.com/ai-models/llm-evaluation]。

而对于产品型的大模型开发，个人觉得选取小模型更加适合。公司或者学校内部进行数据大规模的检索，这种场景下，主要需要的是某些学校或者公司内部产品相关问题的精确回答而不是需要一个知识全面的AI。

快速训练一个用于“交作业”的模型，可以选择Mistral 7B。国外有现有的在线训练模型的网站（忘记了），也可以使用[魔塔社区](https://modelscope.cn/home)里面提供的算力。
![image](https://github.com/Halukisan/Halukisan/assets/102407304/7808aaae-58c7-458e-a40e-91ce0027648a)
![image](https://github.com/Halukisan/Halukisan/assets/102407304/97c321ba-e697-40d7-831a-30157f937b89)

通过数据可以看到Mistral 7B的表现遥遥领先~

**FunctionCalling**功能有助于模型对于用户提问有更加“新”的回答，而不是取决于训练数据的收录时间。这个方面可以参考智谱清言的function calling，对于没有在训练集中的问题，GLM会调用fustion calling功能，发起Http请求去搜索数据，对于前三条与问题相似度最高的数据，模型将对全文进行总结，最后返回给用户。

这里需要考虑模型的回答是否有敏感内容，在二次开发GLM项目中，对模型所有的输入token和输出token都进行敏感词过滤，替换敏感词。同时，对于不需要使用function calling功能的回答要使用一种更加安全的模型训练方法，在训练阶段就避免敏感出现回答。

**Consideration**
1. **缓存策略**：需要设计合适的缓存策略，以确保缓存的数据是最新的，并且能够有效的处理缓存失效和更新
2. **工具安全的选择**：确保外部工具是可靠和安全的，避免引入潜在的安全风险
3. **性能监控**：监控模型和缓存层的性能，确保系统可以在高负载下也能运行
4. **数据隐私**：处理用户数据时，需要确保遵守相关的隐私法规和政策
5. **错误处理**：设计处理机制，以确保在工具调用失败时，系统可以优雅地降级或提供替代响应
6. **更新和维护**：定期和维护function calling和缓存层的逻辑

### **New idea**
可以考虑使用function calling和模型缓存层（Star中）来提高模型的性能和效率。对于prompt先进行敏感词过滤，查询缓存层，有数据就过滤后返回给用户，如果模型训练集中有相似数据，就直接回答，否则调用function calling，发起Http请求去搜索数据，对于前三条与问题相似度最高的数据，模型将对全文进行总结，再次过滤，然后回答用户，存入缓存层中，存入向量数据库Milvus中。
![image](https://github.com/Halukisan/Halukisan/assets/102407304/d7799d0d-adb6-4895-9b0d-1b439d350585)
![image](https://github.com/Halukisan/Halukisan/assets/102407304/9038584a-e4df-4557-804f-e8732304a96c)

这里对于function calling获取到的数据，一概存入Milvus中会导致模型幻觉问题更加严重，我们可以根据时间戳存储数据，用户询问相似的问题，模型根据时间戳（标量）和prompt的embedding值回答，这样可以保证数据的相似度和新鲜度（考虑新数据直接覆盖老数据（如何确定新老数据的关系呢？））

模型的架构设计非常重要，常用的transform架构即可，对于个人训练来说，分区训练对你的钱包更加友好。


### Milvus
对于prompt和应答，需要有一个专门的模型去计算embedding值，不建议使用java（vector不支持）去调用。向量数据库的设计非常重要，prompt和embedding和answer和timestamp......设置标量timestamp辅助搜索。




#### 工作
目前在xFusion实习，辅助AI落地。处理了数据，学习调研了工具框架模型，

Write at 2024/3/7 23:55
