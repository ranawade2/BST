Sameer Test

BST

//Program – Binary Search Tree

#include<iostream>
using namespace std;
class node
{
public:
  int data;
	node *left, *right;
	node()
	{
		left=right=NULL;
	}
	node(int val)
	{
		left=right=NULL;
		data=val;
	}
};

class bst
{
private:
	node *root;
	void insertNode(node *&rootptr, node *pnew);
	void deleteNode(node *&root, int delval);
	int least(node *rootptr);
	int max(node *rootptr);
	void pre(node *rootptr);
	void post(node *rootptr);
	void in(node *rootptr);
	int countinternal(node *rootptr, int &count);
	void printTree(node *p, int level);
	int search(node *rootptr, int data);

public:
	bst();
	void callsearch(int data);
	void insertBST(int datain);
	void deleteBST(int data);
	void displayin();
	void displaypost();
	void displaypre();
	void count();
	void print();
	void leastele();
	void maxele();
};

bst::bst()
{
	root=NULL;
}

void bst::print()
{
	printTree(root, 0);
};

void bst::callsearch(int data)
{
	search(root, data);
}

int bst::search(node *rootptr, int data)
{
	if(rootptr==NULL)
	{
		cout<<"Data not found";
		return 0;
	}	
	else if(rootptr->data==data)
		cout<<"Element found"<<endl;
	else if(data<rootptr->data)
		search(rootptr->left, data);
	else
		search(rootptr->right, data);
}

void bst::count()
{
	int c=0;
	cout<<"The number of internal nodes is: "<<countinternal(root, c)<<endl;
}

int bst::countinternal(node *rootptr,int &count)
{
	if(rootptr!=NULL)
	{
		countinternal(rootptr->left, count);
		if(rootptr->right!=NULL || rootptr->left!=NULL)
			count++;
		countinternal(rootptr->right, count);
		return count;
	}
}
void bst::printTree(node *p, int level)
{
	if(p!=NULL)
	{
		printTree(p->right, level+1);
		for(int i=0;i<level;i++)
			cout<<"   ";
		cout<<level<<":"<<p->data<<endl;
		printTree(p->left, level+1);
	}
};

void bst::insertBST(int datain)
{
	node *p=new node(datain);
	insertNode(root, p);
}

void bst::insertNode(node *&rootptr, node *pnew)
{
	node *curr, *parent;
	if(root==NULL)
		root=pnew;
	else
	{
		curr=root;
		while(curr!=NULL)
		{
			parent=curr;
			if(pnew->data<curr->data)
				curr=curr->left;
			else if(pnew->data==curr->data)
				cout<<"Duplicate value inserted"<<endl;
			else
				curr=curr->right;
		}
		if(pnew->data<parent->data)
			parent->left=pnew;
		else
			parent->right=pnew;
	}
}

void bst::deleteBST(int data)
{
	int p=data;
	deleteNode(root, p);
}

void bst::deleteNode(node *&rootptr, int delval)
{
	node *temp;
	if(root==NULL)
	{
		cout<<"Deletion failed"<<endl;
		return;
	}
	if(delval<rootptr->data)
		deleteNode(rootptr->left, delval);
	else if(delval>rootptr->data)
		deleteNode(rootptr->right, delval);
	else
	{
		if(rootptr->left==NULL)
		{
			temp=rootptr;
			rootptr=rootptr->right;
			delete temp;
			cout<<"Deletion successful";
		}
		else if(rootptr->right==NULL)
		{
			temp=rootptr;
			rootptr=rootptr->left;
			delete temp;
			cout<<"Delete successful";
		}
		else
		{
			temp=rootptr->left;
			while(temp->right!=NULL)
			{
				temp=temp->right;
			}
			rootptr->data=temp->data;
			deleteNode(rootptr->left, temp->data);
		}
	}
}

void bst::displaypre()
{
	pre(root);
}

void bst::displaypost()
{
	post(root);
}

void bst::displayin()
{
	in(root);
}

void bst::leastele()
{
	cout<<"The smallest element is: "<<least(root)<<endl;
}

int bst::least(node *rootptr)
{
	if(rootptr->left==NULL)
		return rootptr->data;
	else
		least(rootptr->left);
}

void bst::maxele()
{
	cout<<"Largest element is: "<<max(root)<<endl;
}

int bst::max(node *rootptr)
{
	if(rootptr->right==NULL)
		return rootptr->data;
	else
		max(rootptr->right);
}

void bst::pre(node *rootptr)
{
	if(rootptr!=NULL)
	{
		cout<<rootptr->data<<endl;
		pre(rootptr->left);
		pre(rootptr->right);
	}
}

void bst::post(node *rootptr)
{
	if(rootptr!=NULL)
	{
		post(rootptr->left);
		post(rootptr->right);
		cout<<rootptr->data<<endl;
	}
}

void bst::in(node *rootptr)
{
	if(rootptr!=NULL)
	{
		in(rootptr->left);
		cout<<rootptr->data<<endl;
		in(rootptr->right);
	}
}


int main()
{
	int c, ele, el;
bst B;
	cout<<"Choose an operation to perform"<<endl;
	cout<<"1 Insert"<<endl;
	cout<<"2 Delete"<<endl;
	cout<<"3 Display"<<endl;
	cout<<"4 Display pre order"<<endl;
	cout<<"5 Display post order"<<endl;
	cout<<"6 Display in order"<<endl;
	cout<<"7 Search"<<endl;
	cout<<"8 Count internal nodes"<<endl;
	cout<<"9 Display Largest element"<<endl;
	cout<<"10 Display Smallest element"<<endl;
	cout<<"11 Quit"<<endl;
	for(;;)
	{
		cout<<"Enter choice: ";
		cin>>c;
		switch(c)
		{
			case 1: cout<<"Enter element to be inserted"<<endl;
				cin>>ele;
				B.insertBST(ele);
				break;
			case 2: cout<<"Enter element to be deleted"<<endl;
				cin>>ele;
				B.deleteBST(ele);
				break;
			case 3: B.print();
				break;
			case 4: B.displaypre();
				break;
			case 5: B.displaypost();
				break;
			case 6: B.displayin();
				break;
			case 7: cout<<"Enter element to search"<<endl;
				cin>>ele;
				B.callsearch(ele);
				break;
			case 8: B.count();
				break;
			case 9: B.maxele();
				break;
			case 10: B.leastele();
				break;
			case 11: return 0;
		}
	}
	return 0;
}
