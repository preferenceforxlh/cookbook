# CAMEL
## 项目结构
- CAMEL
    - agents目录：存放各种Agent实现
        - ChatAgent：最重要的基类模型，初始化流程如下：
            1. 创建model_manager管理模型，使用model_manager提供的统一run接口来调用模型，必要时会使用model_factory创建模型
            2. 创建AgentMemory(如果不提供Memory，默认使用ChatHistoryMemory的in-memory形式)
            3. 使用BaseMessage创建SystemMessage，并且必要时扩充SystemMessage，添加指定输出为xx语言的prompt
            4. 初始化memory，将SystemMessage写入AgentMemory
            5. 初始化internel tools，将提供的tools转换成FunctionTool
            6. 初始化externel_tools, 获取外部tools的openai_tool_schema
            Agent最重要的step方法：
            1. 
    - configs目录：配置每个平台使用OpenaiAPI进行请求时可以使用的参数
        - xxconfig
    - models目录：存放每个平台模型的实现，以及model_factory模型工厂
        - xxx_model.py: 每个平台的模型实现
        - model_factory：模型的创建工厂
        - model_manager: 模型管理工具，包装模型，提供模型运行的统一接口，内部指定到底运行哪个模型
    - memory目录：存放Agent对话过程中使用的memory模块
        - ChatHistoryMemory： User-Agent对话历史，可以in-memory存储，也可以存数据库
        - VectorDBMemory： 存放向量化的记忆
    - storage目录：存放memory的低层存储方式
        - key-value形式
            - in-memory
            - redis数据库
        - vector形式
            - 各种向量数据库
        - ..
    