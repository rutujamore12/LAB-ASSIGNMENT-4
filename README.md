 #include<iostream>
#include<stack>
using namespace std;

struct Node{
int data;
Node * left;
Node  * right;
Node(int value){
data = value;
left = 0;
right = 0;

}
};
bool isOperator(char c) {
    return c == '+' || c == '-' || c == '*' || c == '/';
}


Node* constructPostfixTree(const string& postfix)
{
    stack<Node*> s;
    for (int i = 0; i<1; i++)
{
char c =postfix[i];
        if (isOperator(c)) {
            Node* node = new Node(c);
            node->right = s.top(); s.pop();
            node->left = s.top(); s.pop();
            s.push(node);
        } else {
            s.push(new Node(c));
        }
    }
    return s.top();
}

// Construct an expression tree from a prefix expression
Node* constructPrefixTree(const string& prefix) {
    stack<Node*> s;
    for (int i = prefix.size() - 1; i >= 0; --i) {
        char c = prefix[i];
        if (isOperator(c)) {
            Node* node = new Node(c);
            node->left = s.top(); s.pop();
            node->right = s.top(); s.pop();
            s.push(node);
        } else {
            s.push(new Node(c));
        }
    }
    return s.top();
}

Node * insertNode(Node * root,int value){
if(root==0)
{
return new Node(value);
}
if(value<root->data){
root->left=
insertNode(root->left,value);
}
else{
root->right=
insertNode(root->right,value);
}

return root;
}
void inOrderRecursive(Node*root)
{
if(root==0)
{
return ;
}
cout<<root->data<<" ";
inOrderRecursive(root->left);
inOrderRecursive(root->right);

}


void inOrderNonrecursive(Node * root)
{
    Node* tmp = root;
    stack<Node*> S;

    while (true) {
       
        while (tmp != 0)
{
            S.push(tmp);
            tmp = tmp->left;
        }
       
       
        if (S.empty())
{
            return;
        }

        tmp = S.top();
        S.pop();
        cout << tmp->data << " ";
        tmp = tmp->right;
    }
}


void preOrderRecursive(Node * root)
{
if(root==0)
{
return ;
}
cout<<root->data<<" ";
preOrderRecursive(root->left);
preOrderRecursive(root->right);


}
void preOrderNonrecursive(Node * root)
{
Node* tmp = root;
    stack<Node*> S;

    while (true) {
       
        while (tmp != 0)
{
            S.push(tmp);
            cout<< tmp->data<<" ";
            tmp = tmp->left;
      }
       
       
        if (S.empty())
{
            return;
        }
        tmp = S.top();
        S.pop();
          tmp = tmp->right;
}
}
void postOrderRecursive(Node * root)
{
if(root==0)
{
return ;

}
postOrderRecursive(root->left);
postOrderRecursive(root->right);
cout<<root->data<<" ";

}
 
void postOrderNonrecursive(Node* root) {
    if (root == 0)
{
return;
}

    stack<Node*> S;
    Node* prev = 0 ;

    S.push(root);
    while (!S.empty()) {
        Node* tmp = S.top();
       
        if (!prev || prev->left == tmp|| prev->right == tmp) {
            if (tmp->left) {
                S.push(tmp->left);
            } else if (tmp->right) {
                S.push(tmp->right);
            }
        }
       
        else if (tmp->left == prev) {
            if (tmp->right) {
                S.push(tmp->right);
            }
        }
       
        else {
            cout << tmp->data << " ";
            S.pop();
        }
        prev = tmp;
    }
}

int main(){
string expression;
    int choice;
    char op;

    do {
        cout << "1. Construct Tree from Postfix Expression" << endl;
        cout << "2. Construct Tree from Prefix Expression" << endl;
        cout << "Enter choice: ";
        cin >> choice;

        Node* root = 0;

        switch (choice) {
            case 1:
                cout << "Enter Postfix Expression: ";
                cin >> expression;
                root = constructPostfixTree(expression);
                break;
            case 2:
                cout << "Enter Prefix Expression: ";
                cin >> expression;
                root = constructPrefixTree(expression);
                break;
            default:
                cout << "Invalid choice" << endl;
                continue;
        }
        do {
            cout << endl;
            cout << "1. Inorder Recursive" << endl;
            cout << "2. Inorder Nonrecursive" << endl;
            cout << "3. Preorder Recursive" << endl;
            cout << "4. Preorder Nonrecursive" << endl;
            cout << "5. Postorder Recursive" << endl;
            cout << "6. Postorder Nonrecursive" << endl;
            cout << "Enter choice: ";
            cin >> choice;

            switch (choice) {
                case 1:
                    cout << "Inorder Recursive: ";
                    inOrderRecursive(root);
                    cout << endl;
                    break;
                case 2:
                    cout << "Inorder Nonrecursive: ";
                    inOrderNonrecursive(root);
                    cout << endl;
                    break;
                case 3:
                    cout << "Preorder Recursive: ";
                    preOrderRecursive(root);
                    cout << endl;
                    break;
                case 4:
                    cout << "Preorder Nonrecursive: ";
                    preOrderNonrecursive(root);
                    cout << endl;
                    break;
                case 5:
                    cout << "Postorder Recursive: ";
                    postOrderRecursive(root);
                    cout << endl;
                    break;
                case 6:
                    cout << "Postorder Nonrecursive: ";
                    postOrderNonrecursive(root);
                    cout << endl;
                    break;
                default:
                    cout << "Invalid choice" << endl;
                    break;
            }

            cout << "Do you want to continue with traversals (y/n)? ";
            cin >> op;
        } while (op == 'y' || op == 'Y');

        cout << "Do you want to construct another tree (y/n)? ";
        cin >> op;

    } while (op == 'y' || op == 'Y');

    return 0;
} 

 
