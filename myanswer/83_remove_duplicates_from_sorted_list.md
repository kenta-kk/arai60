step1

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

step2

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

step3
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

