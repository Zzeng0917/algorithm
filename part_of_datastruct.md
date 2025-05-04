## 前缀和与哈希表

### 1.枚举右，维护左

双变量问题，形如: ai + aj = t 可以转变成: ai = t - aj，转化为在aj左边找到符合条件的ai,过程中可以用哈希表记录。



**1.两数之和:求出  ai + aj = target**

```
hash[target - ai] > 0 : ans++
hash[ai]++
```



**1512.好数对的数目:在nums数组中找到：i < j，且nums[i] == nums[j]的组合个数**

分析：问题也就转化为在nums[j] 左边有多少个相同的数，用哈希表记录左边每个num的个数，同时对当前的数进行判断

```
if hash[num] > 0 : ans += hash[num]
hash[num]++
```

***2001可互换矩形的组数相同** 



二维的哈希表：

**LC1128:等价多米诺骨牌对的数目**

形式上，`dominoes[i] = [a, b]` 与 `dominoes[j] = [c, d]` **等价** 当且仅当 (`a == c` 且 `b == d`) 或者 (`a == d` 且 `b == c`)

分析：每次都将最小放在前，最大放在后，就不用额外考虑转换的问题

二维哈希：

```go
//golang: 
cnt := [10][10]int{}
```

```python
#python:defaultdict 是 Python 中 collections 模块下的一个类，它继承自内置的 dict，并扩展了默认值的功能。当访问不存在的键时，defaultdict 可以自动为这个键生成一个默认值，而不会抛出 KeyError 异常。
cnt = defaultdict(int)
```

```c++
//C++
for (auto& x : dominoes) {
            auto [a,b] = minmax(x[0], x[1]);
            ans += cnt[a][b]++;
        }
```



## 队列

(赶进度，为了快点做一些有关堆的题目)

队列：一种特殊的线性表，只允许在头部删除，尾部插入（先进先出）。

优先队列：不同于先进先出，每次从队列中取出最高优先权的元素。

```go
//Golang:没有内置的队列结构，用切片，链表来实现队列的运行。

//使用切片定义队列类型
type queue []interface{}

//入队操作：
func(q *queue) Enqueue(value interface{}) {
   *q = append(*q, value)
}
//出队操作：
func (q *queue) Dequeue() (interface{}, bool) {
   if q.isempty() {
      return nil, false
   }
   value := (*q)[0] //获取队头元素
   *q = (*q)[1:]    //移除队列头部元素
   return value, true
}
```

```python
python:

class queue:
   #队列初始化
   def __init__(self):
     self.items = []
     
   #判断队列是否为空
   def is_empty(self):
     return self.items == []
    
   #元素入队
   def enter_queue(self, item):
     self.items.inser(0, item)
     
   #队首元素出队
   def go_queue(self):
     return self.items.pop()
     
   #清空队列
   def clear(self):
     self.items.clear()
```

```C++
//C++: (链队列,结构比较复杂，东西比较多)

//队列结点的结构
typedef struct queuenode {
  q_data_type data;
  struct queuenode* next;
}queuenode;

//队列的结构
typedef struct queue {
  queuenode* phead;
  queuenode* ptail;
}queue;

//初始化
void queueinit(queue* pq){
  assert(pq);
  pq->phead = pq->ptail = NULL;
}

//销毁队列
void queuedestroy(queue* pq){
  assert(pq);
  queuenode* pcur = pq->phead;
  while(pcur){
    queuenode* next = pcur->next;
    free(pcur);
    pcur = next;
  }
  pq->phead = pq->tail = NULL;
}

//入队()
void QueuePush(Queue* pq, QDataType x)
{
	assert(pq);
	QueueNode* newnode = (QueueNode*)malloc(sizeof(QueueNode));
	if (newnode == NULL)
	{
		perror("malloc fail!");
		exit(1);
	}
	newnode->data = x;
	newnode->next =NULL;

	//若队列为空
	if (pq->phead == NULL)
	{
		pq->phead = pq->ptail = newnode;
	}
	//队列非空
	else {
		pq->ptail->next = newnode;
		pq->ptail = pq->ptail->next;
	}
	//pq->size++
}

//出队（头部）
void QueuePop(Queue* pq)
{
	assert(!QueueEmpty(pq));
	//只有一个结点，phead和ptail都置为空
	if (pq->phead == pq->ptail)
	{
		free(pq->phead);
		pq->phead = pq->ptail = NULL;

	}
	else
	{
		QueueNode* next = pq->phead->next;
		free(pq->phead);
		pq->phead = next;
	}
	//pq->size--;
}

```





## 栈

先进后出

```python
pyhton(C++类似):
入栈: .append 或者.extend
出栈: .pop
判断空: .empty
extend()函数直接添加列表或字典中的元素，而append()函数则是将列表或字典当作一个元素直接添加。
```



```
golang中
byte表示8位无符号整数，范围是0～255，主要用于处理二进制数。
rune表示32位有符号整数，范围是0～0x10FFFF，用于处理多语言文本、Unicode字符
```





