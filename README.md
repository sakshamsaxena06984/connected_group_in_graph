# connected_group_in_graph

#include<bits/stdc++.h>
#include<vector>
#include<unordered_set>
using namespace std;
void dfs(vector<int> *edge,bool* &visited,int start,unordered_set<int>* component)
{
	visited[start]=true;
	component->insert(start);
	for(int i=0;i<edge[start].size();i++)
	{
		int next=edge[start][i];
		if(visited[next]==false)
		{
			visited[next]=true;
			dfs(edge,visited,next,component);
		}
	}
}
unordered_set<unordered_set<int>*>* helper(vector<int> *edge,int n)
{
	bool *visited=new bool[n];
	for(int i=0;i<n;i++)
	{
		visited[i]=false;
	}

	unordered_set<unordered_set<int>*>* output=new 	unordered_set<unordered_set<int>*>();

	for(int i=0;i<n;i++)
	{
		if(visited[i]==false)
		{
			unordered_set<int> *component=new unordered_set<int>();
			dfs(edge,visited,i,component);
			output->insert(component);

		}
	}



	return output;
}
int main()
{
	int n;
	cout<<"ENTER THE NUMBER OF NODE"<<endl;
	cin>>n;
	vector<int> *edge=new vector<int>[n];
	int m;
	cin>>m;
	cout<<"enter the number connection"<<endl;
	for(int i=0;i<m;i++)
	{
		int j,k;
		cin>>j>>k;
		edge[j-1].push_back(k-1);
		edge[k-1].push_back(j-1);
	}


	unordered_set<unordered_set<int>*>* output=helper(edge,n);
	unordered_set<unordered_set<int>*>::iterator it=output->begin();
	while(it!=output->end())
	{
		unordered_set<int>* element_output=*it;
		unordered_set<int>::iterator it1=element_output->begin();
		
		while(it1!=element_output->end())
		{
			cout<<*it1+1<<" ";
			it1++;
		}
		delete element_output;
		it++;
	}
	delete output;
	delete edge;
	
	
}
