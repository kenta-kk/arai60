### 困っていること
step2の「他の人が見やすいようにコードを整える」というのが
どうすれば良いかわからず、step1とstep3をやるだけになっています、
なので、「ここがわかりにくい」などお気軽にコメントください！

### 基本方針
今いるノードを記録しつつ、次のノードに移っていく
前に来たことのあるノードに戻ってきたらサイクルが含まれていると判断
戻らずに端っこのノードにきたらサイクルが含まれていないと判断する

### 解答1

```python
# Definition for singly-linked list.
# class ListNode:
# def __init__(self, x):
# self.val = x
# self.next = None

class Solution:
	def hasCycle(self, head: Optional[ListNode]) -> bool:
		visited_nodes = set()
		current_node = head
		while current_node:
			if current_node in visited_nodes:
				return True
			visited_nodes.add(current_node)
			current_node = current_node.next
		return False
```

### 後から調べたこと
ハッシュ関数には衝突？というものがあるらしい。めっちゃでかい数だと
ハッシュ関数を通して出てくる値が被っちゃうことがあるみたい(それが衝突?)
今回は10^4程度なので多分衝突は起きないものとして考えて良いと思う。

### フロイドの循環検出法
うさぎと亀のアルゴリズムとも言うらしい。早く動くポインタと遅く動くポインタが衝突したらサイクルを含んでいることがわかる。

### 解答2

```python
# Definition for singly-linked list.
# class ListNode:
# def __init__(self, x):
# self.val = x
# self.next = None

class Solution:
	def hasCycle(self, head: Optional[ListNode]) -> bool:
		fast, slow = head, head
		while fast:
			if fast.next:
				fast = fast.next
				if fast.next:
					fast = fast.next
				else:
					break
			else:
				break
			
			if fast is slow:
				return True
			
			slow = slow.next
		return False
```
