# ice
/*
 * DS单链表——合并
 */
#include <iostream>

using namespace std;

class Node{
public:
    int data;
    Node *next;
    Node (){next = NULL;}
};
class LinkList{
public:
    Node* head;
    int len;
    LinkList(){ head = new Node(); len = 0;}
    ~LinkList(){
        Node *p, *q;
        p = head;
        while(p){
            q = p;
            p = p->next;
            delete q;
        }
        len = 0;
        head = NULL;
    }
    Node* CreateList(int n){
        Node *p, *tail;
        tail = head;
        len = n;
        int i = 0, data;
        for(; i < n; i++){
            p = new Node();
            cin >> data;
            p->data = data;
            tail->next = p;
            tail = p;
        }
        tail->next = NULL;
        return head;
    }
    void show(){
        Node *p;
        p = head->next;
        while(p){
            cout << p->data << " ";
            p = p->next;
        }
        cout << endl;
    }
};
Node* LL_merge(Node *pa, Node *pb){
    Node *a = pa->next;
    Node *b = pb->next;
    Node *pc = new Node();
    Node *c = pc;
    while(a&&b){
        if(a->data <= b->data){
            c->next = a;
            c = a;
            a = a->next;
        }
        else{
            c->next = b;
            c = b;
            b = b->next;
        }
    }
    c->next = c->next == a? b : a;
    return pc;
}
int main()
{
    LinkList list1, list2;
    int n,m;
    cin >> n;
    list1.CreateList(n);
    cin >> m;
    list2.CreateList(m);
    list1.head = LL_merge(list1.head,list2.head);
    list1.show();
    return 0;
}
