# 浮点数不是实数

[Floating-point Numbers Aren't Real](https://97-things-every-x-should-know.gitbooks.io/97-things-every-programmer-should-know/content/en/thing_33/)

在数学科学种，浮点数不是“实数(real)”，尽管他们在很多编程语言中被称为`real`，比如Pascal和Fortran。实数是无限精度并连续无损的；浮点数被限制了精度，所以它们是有限的，类似于“表现不好”的整数，因为它们在整个范围没有均匀间隔。

举个例子，把2147483647(32位int的最大值)分配给一个32位float变量(名为x)，然后打印。你会得到2147483648。现在打印`x - 64`，仍然是2147483648。现在打印`x - 65`你将得到2147483520！为什么？因为这两个浮点数之间的间隔是128，浮点运算会舍入到最近的浮点数。

(译注：类似于分辨率，128是浮点类型在内存中能表现的最小单位——间隔)

IEEE浮点数是基于基数为2的科学记数法的固定精度数：1.d1d2…d(p-1)x2^e，p代表精度(float是24，double是53)。两个连续的数之间的间隔应为2^(1-p+e)，可以安全近似于ε|x|，ε表示机器的epsilon(2^(1-p))。

知道相邻浮点数的间隔可以帮你避免数字类型的错误。比如，你要处理迭代计算，例如搜索方程的根，要求找出比超过系统能表达精度更高的数字是没有意义的。确保你要求得的差值没回比间隔更小，否则会进入死循环。

自从浮点数成了实数的近似值以来，就存在不可避免的错误。这种错误被称作*四舍五入*，会导致意外的结果。当你去减一个近似值时，例如高位数相互抵消，所以在浮点运算的结果，低位的有效数字(被四舍五入的那部分)被提升到了高位，本质上污染了进一步的相关计算(被称作涂抹)。你需要细致地观察你的算法，以阻止这种灾难性的消除。为了说明，考虑用二次公式求解方程x²-100000x+1=0。由于表达式-b+sqrt(b²-4)中的操作数近似相等，你可以先计算出r1=-b+sqrt(b²-4)，再求得r2=1/r1，因此任何二次方程，ax2+bx+c=0，这个结果满足r1r2=c/a。

涂抹可以以更精妙的方式运行。假设一个库通过1+x+x²/2+x³/3!+…的公式计算e^x，这只适用于x是正数，但想想当x为一个很大的负数时会发生什么。偶数次方结果是大的正数，减去奇数次方的幅度甚至不会影响结果。这里的问题是，正项在数字中的地位要比真实答案影响更大。结果就是趋向于无穷大！这里的解决方案也很简单：给一个负x，计算e^x=1/e^|x|。

不言而喻，你不应该将浮点数用于金融类应用——就是像python和C#语言中的十进制类。浮点数用于高效的科学计算。但失去了精度，性能就毫无价值，所以请记住舍入错误的来源及相应的代码。