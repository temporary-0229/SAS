# 1회차 스터디
`2020. 02. 29`
진행자 김지훈
## Theme
BST 문제들

## Round 1
### Problem - [get BST Height](https://www.hackerrank.com/challenges/30-binary-search-trees/problem)

solver : 찬용님
```javascript
function getheight(root) {
   return iterate(root) - 1;
}

function iterate(node) {
	let l = 0, r = 0;
	if(node.right) l = iterate(node.right);
	if(node.left) r = iterate (node.left);

	return l > r ? l + 1 : r + 1;
}
```

#### 회고 및 코멘트
* 지훈 : 듣는 사람이 마냥 기다리지 않게 개략적인 흐름을 이야기 해주면 좋을 것 같다


## Round 2
### Problem - [BST Level-Order Traversal](https://www.hackerrank.com/challenges/30-binary-trees/problem)

solver : 보곤님
```javascript
this.levelOrder = function(root) {
	return search(root);
}

function search(root) {
	console.log(root.data); // 3
	if (root.left) console.log(search(root.left)): // 2 null
	if (root.right) console.log(search(root.right)); //
}
```
* FIXME : 보곤님 다시 푸셨으면 밑에 코드 다시 적어주세요~

#### 회고 및 코멘트
* 지훈 : 멘탈이 바사삭 한게 보였다. 바사삭한 멘탈은 빨리 수습하고 나오는게 좋음


## Round 3
### Problem - [valid BST](https://www.hackerrank.com/challenges/valid-bst/problem)

solver : Everyone

#### jihoon
#### solve 1
```javascript
const sam1 = [3, 2, 1, 5, 4, 6]
const sam2 = [1, 2, 3]
const sam3 = [1, 3, 4, 2]
const sam4 = [3, 4, 5, 1, 2]

function Node(data) {
    this.data = data;
    this.left = null;
    this.right = null;
}

function BinarySearchTree() {
    this.insert = function(root, data, p_node = null) {
        if (root === null) {
            this.data = new Node(data);
            return this.data;
        }

                if (p_node)
                    console.log(p_node.data, root.data, data)

        if (data <= root.data) {
            if (root.left) {
                this.insert(root.left, data, root);
            } else if (root.right == null) {
                root.left = new Node(data);
            }
        } else {
            if (root.right) {
                this.insert(root.right, data, root);
            } else {
                root.right = new Node(data);
            }
        }

        return this.root;
    };
}

function getSize(root) {
    if (root == null)
        return 0
    return getSize(root.left) + getSize(root.right) + 1
}




function solution(arr) {
    // generate node
    const root = new BinarySearchTree().insert(null, arr.slice(0, 1)[0]);
    arr.slice(1, arr.length).forEach(it => new BinarySearchTree().insert(root, it));

    return getSize(root) == arr.length
}

console.log(`expect\t: true \nactual\t: ` +  solution(sam1))
console.log(`expect\t: true \nactual\t: ` +  solution(sam2))
console.log(`expect\t: false \nactual\t: ` +  solution(sam3))
console.log(`expect\t: false \nactual\t: ` +  solution(sam4))
```
* 뭔가 더 간단한 방법이 있을 것 같은데, 우선 받은 arr를 bst 로 만들고,  만들어진 bst 의 사이즈를 비교했다.
    * Time Complexity : O(n)
    * Space Complexity : O(n)

#### 회고 및 코멘트
* 지훈 : 효율적인 방법이 아닌 것 같다 다시 고민...
