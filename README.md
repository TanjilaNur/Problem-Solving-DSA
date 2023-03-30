# Problem-Solving-DSA

##Implementing Tree
- A tree data structure is a hierarchical structure that is used to represent and organize data in a way that is easy to navigate and search. It is a collection of nodes that are connected by edges and has a hierarchical relationship between the nodes.

- This data structure is a specialized method to organize and store data in the computer to be used more effectively. It consists of a central node, structural nodes, and sub-nodes, which are connected via edges. We can also say that tree data structure has roots, branches, and leaves connected with one another. 

1. Using a class:
class TreeNode {
    var value: Int
    var left: TreeNode?
    var right: TreeNode?

    init(_ value: Int) {
        self.value = value
        self.left = nil
        self.right = nil
    }
}

class BinaryTree {
    var root: TreeNode?

    func insert(_ value: Int) {
        let newNode = TreeNode(value)
        if root == nil {
            root = newNode
            return
        }

        var currentNode = root
        while true {
            if value < currentNode!.value {
                if currentNode!.left == nil {
                    currentNode!.left = newNode
                    return
                }
                currentNode = currentNode!.left
            } else {
                if currentNode!.right == nil {
                    currentNode!.right = newNode
                    return
                }
                currentNode = currentNode!.right
            }
        }
    }

    func search(_ value: Int) -> Bool {
        var currentNode = root
        while currentNode != nil {
            if currentNode!.value == value {
                return true
            } else if value < currentNode!.value {
                currentNode = currentNode!.left
            } else {
                currentNode = currentNode!.right
            }
        }
        return false
    }
}


2. Using a struct:

struct TreeNode {
    var value: Int
    var left: TreeNode?
    var right: TreeNode?
}

struct BinaryTree {
    var root: TreeNode?

    mutating func insert(_ value: Int) {
        let newNode = TreeNode(value)
        if root == nil {
            root = newNode
            return
        }

        var currentNode = root
        while true {
            if value < currentNode!.value {
                if currentNode!.left == nil {
                    currentNode!.left = newNode
                    return
                }
                currentNode = currentNode!.left
            } else {
                if currentNode!.right == nil {
                    currentNode!.right = newNode
                    return
                }
                currentNode = currentNode!.right
            }
        }
    }

    func search(_ value: Int) -> Bool {
        var currentNode = root
        while currentNode != nil {
            if currentNode!.value == value {
                return true
            } else if value < currentNode!.value {
                currentNode = currentNode!.left
            } else {
                currentNode = currentNode!.right
            }
        }
        return false
    }
}

3. Using Enum:

enum TreeNode {
    case empty
    indirect case node(Int, left: TreeNode, right: TreeNode)

    init() {
        self = .empty
    }

    mutating func insert(_ value: Int) {
        switch self {
        case .empty:
            self = .node(value, left: .empty, right: .empty)
        case .node(let val, var left, var right):
            if value < val {
                left.insert(value)
            } else {
                right.insert(value)
            }
            self = .node(val, left: left, right: right)
        }
    }

    func search(_ value: Int) -> Bool {
        switch self {
        case .empty:
            return false
        case .node(let val, let left, let right):
            if value == val {
                return true
            } else if value < val {
                return left.search(value)
            } else {
                return right.search(value)
            }
        }
    }
}
