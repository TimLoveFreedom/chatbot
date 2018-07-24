# chatbot
该项目会继续完善，包含kbqa(neo4j)、task-oriented、chatbot、qa；目前kbqa  demo已完成

一、kbqa

效果如图所示：

  ![avatar](/KG/movie/example.png)


主要流程：

数据准备-->问题抽象-->问题分类-->问题扩展-->答案生成

数据准备：
  
  mysql数据库中的genre（电影类型表）、movie（电影表）、movie_to_genre（电影-类型表）、person（演员表）、person_to_movie（演员-电影表）导出csv格式的数据
  通过load csv...  merge命令导入到neo4j图数据库中。
  
问题抽象：

  问题中涉及到专有的电影名称会转化为他的词性 nm。这样做的好处在于能让分类器减轻特征的选取工作量,也可以缩减训练集的规模。如（卧虎藏龙的评分是多少。抽象后的语句：nm的评分是多少）
  
问题分类：
  
  ![avatar](/KG/movie/classifier.png)
  
  通过分类查找对应模板句子和模板索引
  
问题扩展：

  将问题抽象中的实体词性替换成查询的实体内容（如：nm 评分  替换为 卧虎藏龙 评分）
  
答案生成：

  根据模板索引可以获取对应cypher语句
  
  根据实体内容可以填充cypher语句中参数

二、task-oriented（基于任务对话系统）

效果如图所示：

  ![avatar](/Task-Oriented/description.png)
  
  NLU（自然语言理解）：
  
   这个模块的功能是把来自用户的句子映射到机器可读的语义结构上，一般包含实体（entity）抽取，意图（intent）识别，话题（domain）识别等。
  
  DST(对话状态跟踪)：  
   
   在NLU的基础上，状态跟踪需要把多轮对话历史进行总结，理解上下文中的含义。这个模块对于跟踪用户需求有着至关重要的作用，因为很多时候需要通过综合考
   虑用户多轮输入才能真正理解他们的需求。
    
  DP(对话策略)：
  
   在有了对话状态后，对话策略需要决定下一步应该做什么行动（action）。行动包括查询数据库，或者产生下面要说的一句话。相当于对话系统的高层决策者。
    
  NLG(自然语言生成)：
  
   负责把对话策略的行动装换成自然语言
    
  
  
  
  
  
