# 小心分享
那是我到公司的第一个项目。我刚毕业一心想要证明自己，每天都调代码到很晚。当我每get到一个新特性时，都很认真地把学到的东西——尽可能注释、日志、推送到代码共享库中，就这样工作着。但对我认为很OK的代码审查却让我醍醐灌顶——重用得不好。

为什么会这样？整个大学的复用被认为是高质量软件工程的缩影。我读了所有的条款，书籍，接受过非常有经验的软件专家的教育。这些全是错的？

事实证明我确实错过了一些关键事情。

**上下文**

系统中两处有复用接口的地方实际执行相同逻辑情况比我想象中少。就算我把代码从库里再拉取一遍，这些部分也没有其他依赖。彼此独立推进，独立修改逻辑以适应系统业务需求的改变。有四行相似的代码出问题了——时间异常、耦合。直到我继续深究。

我创建的这个代码共享库就像把鞋带相互绑在每只脚上。创建一个业务领域之前必须先与另一个进行同步。这样独立的功能维护成本可以忽略不计，但公共库则需要巨量的测试。

当我想要减少一定数量的代码行数时，我却要增加同等数量的依赖。这些依赖对上下文必须非常严谨——确保被分配过，有正确合理的赋值。当这些依赖得不到检查时，即便代码看上去没问题，整个系统也会被它们绕死。

这些错误就潜伏在那，当然从核心来看貌似是不错的想法。当调用它们的上下文正确时，这些技术会很有价值。但当上下文本身不好时，它们给系统带来的负担已经超过其价值。当入库的代码存在大量不懂技术的复用时，我都会在最近几天非常留意这次分享。

小心分享。检查你的上下文。确保OK，再继续。