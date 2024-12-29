# DSA - Tree
## [101. Symmetric Tree](https://leetcode.cn/problems/symmetric-tree)

breadth-first (stop at null)
```
var isSymmetric = function(root) {
  if(root==null) return true
  let queue1 = [root]
  let queue2 = []
  while(queue1.length>0) {
    // iterate through half of array: i < queue1.length/2
    for(let i=0; i<queue1.length/2; i++) {
      if(queue1[i]==null || queue1[queue1.length-1-i]==null) {
        if(queue1[i]!=null || queue1[queue1.length-1-i]!=null)
          return false
      }
      else if(queue1[i].val!=queue1[queue1.length-1-i].val)
        return false
    }
    while(queue1.length>0) {
      const node = queue1.shift()
      if(node==null) continue
      queue2.push(node.left)
      queue2.push(node.right)
    }
    queue1 = queue2
    queue2 = []
  }
  return true
}
```
depth-first
```
var isSymmetric = function(root) {
  if(root==null) return true
  return compare(root.left, root.right)
}
function compare(node1, node2) {
  if(node1==null || node2==null) {
    if(node1==null && node2==null)
      return true
    else return false
  }
  else {
    if(node1.val==node2.val)
      return compare(node1.left, node2.right) && compare(node1.right, node2.left)
    else return false
  }
}
```

improved breadth-first (stop at null)
in every push 4 nodes are added, impossible to have odd nodes in queue
```
var isSymmetric = function(root) {
  const queue = [root, root]
  while(queue.length>1) {
    const node1 = queue.shift()
    const node2 = queue.shift()
    if(node1==null || node2==null) {
      if(node1!=null || node2!=null)
        return false
    }
    else {
      if(node1.val!=node2.val)
        return false
      queue.push(node1.left, node2.right, node1.right, node2.left)
    }
  }
  return true
}
```
