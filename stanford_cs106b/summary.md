# Programming Abstractions in C++,

## Lecture_01: Intorduction

* \Win 2018 by Marty Stepp
* Handout: http://cs106b.stanford.edu



## Lecture_04: ADT

* ADT(Abstaract Data Type)：一组相关联的数据集，以及可以作用在数据集上的操作。操作就是增删改查和遍历。
* Data Structure：数据结构是一种组织、管理和存储数据的方式，目的是为了高效的存取数据。更具体来说就是ADT的定义。
* Vector、List、Stack、Queue、Deque、PriorityQueue、Set、Map，当我们讲到上述的ADT或数据结构时，我们只讲它们的特性，不涉及具体实现。

### stack

只允许在一端进行操作的一组数据，符合LIFO的特性，操作包含：push、pop、peek

stack的使用场景：

* 编程语言和编译器
  * 函数调用栈
  * 编译器使用Stack来计算表达式的值
* 成对匹配
  * 回文串判定
  * 括号匹配
  * 将中缀表达式转化为 前缀/后缀 表达式
* 复杂的算法
  * 回溯算法
  * undo stack 用来撤销操作

```
// 括号匹配问题
public boolean isMatch(String str) {
	if (str == null || str.length() == 0) {
		return true;
	}
	
	// 构造matchMap，简化后续重复代码
	Map<Character, Character> matchMap = new HashMap<>(4);
	matchMap.put('(', ')');
	matchMap.put('[', ']');
	matchMap.put('{', '}');
	
	// java中将Deque作为Stack使用, Deque的实现类就是LinkedList
	Deque<Character> stack = new LinkedList<>();
  for (int i = 0, j = str.length(); i < j; i++) {
    char c = str.charAt(i);
  	if (c == '(' || c == '[' || c == '{') {
  		stack.push(c);
  	} else if (c == ')' || c == ']' || c == '}'){
  		if (stack.isEmpty() || stack.pop().equals(matchMap.get(c))) {
  			return false;
  		}
  	} 
  }
  // 最后判断stack是否为空
  return stack.isEmpty();
}
```



## Lecture_06: Recursion

要想掌握Recursion，你必须首先掌握Recursion。

一个问题的定义中包含他自己（self-similar）。一个问题的解决往往需要先解决一个规模更小的类似问题。

一个递归算法都包含至少2个case：

* base case：简单的场景，可以直接给出答案。
* recursive case：复杂的场景，无法直接给出答案，但是可以通过自身做一小部分工作，将剩余工作转化为一个更小规模的类似问题来解决。

递归解法的核心就是找到一个好的base case（规模足够小的场景）以及如何将复杂问题转为为一个规模更小的问题。

### Towers of Hanoi

```
int steps = 0;

// 汉诺塔问题，如果不用递归，很难想象到其他解法
// 如果使用了递归，你只要抽象出缩减问题规模的步骤，它就work了，太神奇了，就跟动态规划一样，it just works.
// 思考：如何将x个碟子从第1根柱子移到第3根？
// 可以分为如下3步：
//    将前x-1个碟子从第1根柱子移到第2根
//    将最后一个碟子从第1根柱子移到第3根
//		将前x-1个碟子从第2根柱子移到第3根（规模更小的相同问题）
public void hanoi(int discs, int from, int to) {
	// base case, 没有碟子的时候，结束
	if (discs == 0) {
		return;
	}
	steps++;
	// recursive case, 将问题转化为  一个规模更小的问题 + a little job by me
	int aux = auxPillar(from, to);
	hanoi(discs - 1, from, aux);
	// 将最底部的盘子从 from 移动到 to
	System.out.println(String.format("move no.%d disc from %d to %d", discs, from, to));
	hanoi(discs - 1, aux, to);
}

// 假设柱子编号为1 2 3
public int auxPillar(int from, int to) {
	return 6 - from - to;
}
```



### Evalute the Expression





## Lecture_09: Exhaustive Search and Backtracking



