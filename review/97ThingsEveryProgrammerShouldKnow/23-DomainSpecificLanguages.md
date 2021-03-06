# 领域专用语言

[Domain-Specific Languages](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_23/)

> 译注：我看标题以为本节的内容是说要注重客户/业务方的领域术语，但其实不是，本节所说的领域语言是指：前端、后端、数据库、桌面软件等不同的开发领域，所使用的不同的语言

不论何时你听到任何领域内的专家在讨论，可以是国际象棋选手，幼儿教师，或者保险代理人，你都能发现他们的词汇与日常用语有很大的不同。这是领域专用语言(DSLs)的一部分：一个特定领域内的特殊词汇，用来描述领域内特定的某件事情。

在软件世界里，DSLs是通过一种语言写成的一些可执行表达式，专门用在一个领域中，这种语言具备有限的词汇和语法，可读、可理解，并希望领域专家可以编写。针对开发者和科学家的软件DSLs已经存在很长时间了。例如，可以从配置文件中找到Unix的“小语种”，而通过LISP宏创建的语言就是一些更古老的例子了。

DSLs通常根据内部或外部来分类：

- **内部DSLs**通过一种通用的编程语言编写，使其语法看起来更像是自然语言。相比于其他不用这种方式的语言(如Java)，这可以更方便给语言提供更多语法糖和格式化的可能性(例如Ruby和Scalar)。很多内部DSL打包了现有的API、库、或者业务代码，然后提供一个封装来减少对某些功能的诡异访问。只需要运行(run)它们就可以直接执行(excutable)。根据实现和领域，它们被用于构建数据结构，定义依赖，运行处理或任务，和其他系统通信，或者校验用户输入。内部DSL语法受限于它的宿主语言(**译注：host language应该是指用于编写DSL的基础语言——母语**)。有很多模式——例如，表达式构建器、方法链、以及注解——能够帮你把宿主语言转换为你的DSL。如果宿主语言不需要重新编译，那DSL可以很快被领域专家拿来做开发。
- **外部DSLs**是文本或图形化表达式语言——尽管文本DSLs要比图形化的更常见。文本表达式可能通过如词法/语法分析器、模型转换器、生成器，或者任何后期处理类型的工具链进行处理。外部DSL主要用于读入内部模型，作为进一步处理的基础。它用来定义一个语法很有用(例如EGNF——译注：[扩展巴科斯范式](https://zh.wikipedia.org/wiki/%E6%89%A9%E5%B1%95%E5%B7%B4%E7%A7%91%E6%96%AF%E8%8C%83%E5%BC%8F))。一个语法提供工具链生成部分的起点(例如编辑器、可视化、解析器、生成器)。对于一个简单的DSL来说，手工做的分析器可能足够了——用于创建实例、正则表达式。但如果要求太多，自定义的解析器就会变得很笨，所以查看专为语言语法和DSL工作而设计的工具是有意义的——例如，[openArchitectureWare](https://de.wikipedia.org/wiki/OpenArchitectureWare)、[Antlr](https://www.ibm.com/developerworks/cn/java/j-lo-antlr/index.html)、[SableCC](https://en.wikipedia.org/wiki/SableCC)、[AndroMDA](https://www.andromda.org)。把外部DSLs定义为XML方言也很常见，尽管读起来经常有问题——尤其对没有技术基础的读者而言。

你必须始终考虑你DSL的目标受众。他们是开发者、管理人员、商业消费者、或者终端用户？你不得不去调整语言的技术门槛、可用的工具、语法帮助(如智能感知)、早期校验、可视化、以及代表目标受众。通过隐藏技术细节，DSL可以让用户无需在开发人员的帮助下根据需求自主调整系统。它可以加速开发，因为在初始化语言框架到位后就存在分散工作的可能。现有的表达式和语法也有不同的迁移路径。