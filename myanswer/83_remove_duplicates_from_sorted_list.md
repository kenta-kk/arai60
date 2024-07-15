### step1

2つポインタ用意して、比較して同じ値だったらスキップしていくイメージ
メインで進むノードと、先発隊みたいなノードがいて、その2つで比較する


```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head == None:
            return None

        current_node = head
        scan_node = head.next

        while scan_node:
            if current_node.val == scan_node.val:
                scan_node = scan_node.next
                current_node.next = scan_node
            else:
                current_node = scan_node
                scan_node = scan_node.next
        return head
        
```

### step2

scan_nodeとか使って、2個のポインタにしたせいでややこしくなってる気がする
あと、問題141と142の経験から無限ループ使うと書きやすい感じしたので、
ここでもそれ使ってシンプルにできないか考えよう。


```python

class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        while 1:
            if current is None or current.next is None:
                break
            if current.val == current.next.val:
                current.next = current.next.next
            else:
                current = current.next
        return head

```

### step3
(step2と同じコード)

```python

class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        while 1:
            if current is None or current.next is None:
                break
            if current.val == current.next.val:
                current.next = current.next.next
            else:
                current = current.next
        return head

```

### 2024/7/15追記
コメントもらった後のメモ
- 選択肢が見えてない、調べごとしていない、というコメントをもらったがその通りすぎる
- 今のところ、動くコード作るのに結構労力使ってるのが原因ぽい
    - 対策：step2に時間かける。急いで進もうと思うとよくない。
- あと、人のコードをみたときに、自分のコード改善に取り入れるのがうまくできていない
    - 対策：自分の書こうとしてるコードも、読んだ人のコードも一回自然言語で紙に書きだしてみてロジックを整理する
- それでいろんなバリエーション作ってから、一番良いとおもうものをstep2として書く

参考
https://github.com/TORUS0818/leetcode/pull/5/files
`while current:` の方が素直

```python

class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        while current:
            if current.next is None:
                return head
            if current.val == current.next.val:
                current.next = current.next.next
            else:
                current = current.next
        return head

```

あるいは、colorboxさんの指摘どおり、whileにcurrentとcurrent.nextの
Noneの確認をいれることでif文のブロックを減らせる
こっちのがシンプルな記述

```python

class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        while current and current.next:
            if current.val == current.next.val:
                current.next = current.next.next
            else:
                current = current.next
        return head

```

あるいは、whileにifの条件を流用するにしても、こういう書き方もあるんだなぁ
参考
https://discord.com/channels/1084280443945353267/1195700948786491403/1196388760275910747


```python

class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        while current:
            while current.next and current.val == current.next.val:
                current.next = current.next.next
            current = current.next
        return head


```

