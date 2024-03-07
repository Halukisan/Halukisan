### Hi there 👋
[Chinese](https://github.com/Halukisan/Halukisan/blob/main/README.md)|[English](https://github.com/Halukisan/Halukisan/blob/main/READMEE.md)

**Halukisan/Halukisan** Front-end and back-end development engineer, commonly used MVC and DDD architecture, familiar with SpringBoot and Vue, currently very interested in large models. You can see the homework I wrote for school in Neuproject, First stores all the notes I took while learning programming, and MyBoke stores the source code of the blog.

There have some tips that can help you learn about me:
- 🔭 I’m currently working on xFusion
- 🌱 I’m currently learning LLM
- 🤔 I’m looking for help with LLM
- 📫 How to reach me: 2162408515@qq.com

### **Interest**

I like content related to large models. I have tried calling the ChatGLM large model API to develop a project with front-end and back-end separation. I want to train a large (small) model myself.
[Mistral](https://modelscope.cn/models/TabbyML/Mistral-7B/summary) has very good ratings in all aspects, second only to [ChatGLM3 6B](https://modelscope.cn/models/ZhipuAI/ chatglm3-6b/summary) performance, please refer to the details
[Data Learning] (https://www.datalearner.com/ai-models/llm-evaluation).

For product-type large model development, I personally feel that small models are more suitable. Large-scale data retrieval is carried out within a company or school. In this scenario, what is mainly needed is accurate answers to questions related to the internal products of certain schools or companies rather than an AI with comprehensive knowledge.

To quickly train a model for "hand in work", you can choose Mistral 7B. There are existing online training model websites abroad (I forgot about them), and you can also use the computing power provided in [Magic Tower Community] (https://modelscope.cn/home).
![image](https://github.com/Halukisan/Halukisan/assets/102407304/7808aaae-58c7-458e-a40e-91ce0027648a)
![image](https://github.com/Halukisan/Halukisan/assets/102407304/97c321ba-e697-40d7-831a-30157f937b89)

From the data, we can see that Mistral 7B’s performance is far ahead~
The **FunctionCalling** function helps the model have more "new" answers to user questions, rather than depending on the collection time of the training data. In this regard, you can refer to the function calling of Zhipu Qingyan. For questions that are not in the training set, GLM will call the fustion calling function and initiate an HTTP request to search for data. For the first three pieces of data that are most similar to the question, the model will perform the full text Summary, and finally returned to the user.

Here you need to consider whether the model's answers contain sensitive content. In the secondary development GLM project, all input tokens and output tokens of the model are filtered for sensitive words and replaced with sensitive words. At the same time, a safer model training method should be used for answers that do not require the use of function calling to avoid sensitive answers during the training phase.

**Consideration**
1. **Caching Strategy**: A suitable caching strategy needs to be designed to ensure that the cached data is up to date and can effectively handle cache invalidations and updates.
2. **Safe tool selection**: Ensure that external tools are reliable and safe to avoid introducing potential security risks
3. **Performance Monitoring**: Monitor the performance of the model and cache layer to ensure that the system can run under high load
4. **Data Privacy**: When processing user data, you need to ensure compliance with relevant privacy regulations and policies
5. **Error Handling**: Design a handling mechanism to ensure that when a tool call fails, the system can gracefully degrade or provide an alternative response
6. **Update and Maintenance**: Regularly and maintain the logic of function calling and caching layers

### **New idea**
Consider using function calling and model caching layers (in Star) to improve model performance and efficiency. For prompts, sensitive words are filtered first, and the cache layer is queried. If there is data, it is filtered and returned to the user. If there is similar data in the model training set, it will be answered directly. Otherwise, function calling is called and an HTTP request is initiated to search for the data. For the first three questions and questions For the data with the highest similarity, the model will summarize the full text, filter it again, and then answer the user, store it in the cache layer, and store it in the vector database Milvus.
![image](https://github.com/Halukisan/Halukisan/assets/102407304/d7799d0d-adb6-4895-9b0d-1b439d350585)
![image](https://github.com/Halukisan/Halukisan/assets/102407304/9038584a-e4df-4557-804f-e8732304a96c)

Here, all the data obtained by function calling will be stored in Milvus, which will cause the problem of model hallucination to be more serious. We can store the data according to the timestamp. The user asks similar questions, and the model answers according to the timestamp (scalar) and the embedding value of the prompt. This can ensure the similarity and freshness of the data (consider new data directly overwriting old data (how to determine the relationship between new and old data?))

The architectural design of the model is very important. The commonly used transform architecture is sufficient. For personal training, partition training is more friendly to your wallet.

### Milvus
For prompts and responses, a special model is needed to calculate the embedding value. It is not recommended to use java (vector does not support it) to call it. The design of the vector database is very important. Prompt and embedding and answer and timestamp... set the scalar timestamp to assist search.

#### Work
Currently interning at xFusion, assisting in the implementation of AI. Processed the data, studied and investigated the tool framework model,

Write at 2024/3/7 23:55
