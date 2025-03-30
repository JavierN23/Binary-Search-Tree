Imagine you were to take an empty binary search tree and insert the following sequence of numbers in this order: [1, 5, 9, 2, 4, 10, 6, 3, 8]. Draw a diagram showing what the binary search tree would look like. Remember, the numbers are being inserted in the order presented here. (2 points)
![Binary Search Tree drawio](https://github.com/user-attachments/assets/70d0f4a9-c57b-47ef-ac57-8740abeb748c)

If a well-balanced binary search tree contains 1,000 values, what is the maximum number of steps it would take to search for a value within it? (1 point)
We can solve this by using the log base 2 of N formula and if we use this we will get Log_2(1000) = 9.97 --> 10

Write an algorithm that finds the greatest value within a binary search tree. (2 points)

    #include <iostream>

    using namespace std;
    
    struct TreeNode {    
    int value;
    
    TreeNode* left;
    
    TreeNode* right;
    
    TreeNode(int val) : value(val), left(nullptr), right(nullptr) {}
    };
    int findMaxValue(TreeNode* root) {
    if (!root) {
        throw invalid_argument("Tree is empty!");
    }
    
    TreeNode* current = root;
    while (current->right) {
        current = current->right; 
    }
    
    return current->value; 
    }
    int main() {
    // Constructing a sample BST
    TreeNode* root = new TreeNode(5);
    root->right = new TreeNode(9);
    root->right->right = new TreeNode(12);
    root->right->left = new TreeNode(7);

    cout << "Greatest value in BST: " << findMaxValue(root) << endl; // Output: 12
    delete root->right->right;
    delete root->right->left;
    delete root->right;
    delete root;

    return 0;
    }
Write a code in C++ using the same array mentioned in #1 and implement a binary search tree. Only insertion operation is required.

    #include <iostream>

    using namespace std;
    struct TreeNode {
    int value;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val) : value(val), left(nullptr), right(nullptr) {}
    };
    TreeNode* insert(TreeNode* root, int val) {
    if (!root) return new TreeNode(val); // Create a new node if tree is empty
    
    if (val < root->value)
        root->left = insert(root->left, val); // Insert into left subtree
    else
        root->right = insert(root->right, val); // Insert into right subtree

    return root; // Return unchanged root node 
    }
    void inorderTraversal(TreeNode* root) {
    if (!root) return;
    
    inorderTraversal(root->left);  // Visit left subtree
    cout << root->value << " ";    // Print current node
    inorderTraversal(root->right); // Visit right subtree
    }

    int main() {
    int arr[] = {1, 5, 9, 2, 4, 10, 6, 3, 8};
    int n = sizeof(arr) / sizeof(arr[0]);

    TreeNode* root = nullptr; // Initialize BST root

    // Insert elements into the BST
    for (int i = 0; i < n; i++) {
        root = insert(root, arr[i]);
    }

    // Print the BST in sorted order (in-order traversal)
    cout << "In-order Traversal of BST: ";
    inorderTraversal(root);
    cout << endl;

    return 0;
    }

