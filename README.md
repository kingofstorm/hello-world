    常见算法题总结
    
    *******************************
    01背----------------------01bag.cpp
    
    
    
    ##################################
    	
        #include<iostream>
        #include<string>
        #include<vector>
        #include<algorithm>
        using namespace std;
        struct TreeNode {
            int val;
            struct TreeNode *left;
            struct TreeNode *right;
           TreeNode(int x) :
            val(x), left(NULL), right(NULL) {
            }
        };
    	class LongestPath {
	public:
	void find(TreeNode* root,int& max,int& tmp,vector<int>&pret)
        	{
		        if (root == NULL)
			        return;
		        if (pret.back() == root->val)
		    {
			    tmp++;
		    	pret.push_back(root->val);
			    if (tmp > max)
				max = tmp;
	    	}
	    	else
		        {
			        pret.push_back(root->val);
		        	tmp = 1;
	        	}
	        find(root->left, max, tmp, pret);
	    	find(root->right, max, tmp, pret);
	    	pret.pop_back();
    		}
		int findPath(TreeNode* root) {
		if (root == NULL)
			return 0;
		int max = 1;
		int tmp = 1;
		int pre = root->val;
		vector<int> pret;
		pret.push_back(pre);
		find( root->left, max, tmp,pret);
		find(root->right, max, tmp, pret);
		return max;
		// write code here
		}
	  };


	TreeNode* CreateBinaryTree()
	{
		int N;
		cin >> N;
		if (N == -1)
		return NULL;
		TreeNode *root = new TreeNode(N);
		root->left = CreateBinaryTree();
		root->right = CreateBinaryTree();
		return root;
	}

	int main(int argc, char* argv[])
	{
	

		LongestPath path;
		TreeNode* root = CreateBinaryTree();
		int res = path.findPath(root);
		cout << res<<endl;
		return 0;
	}
    
    
    
    
    #################################
    4-19
    
	vector<int> getPartition(const vector<vector<int> >& land, int n, int m) {
	vector<int> pro(n+1, 0);
	pro[0] = 0;
	for (int i = 0; i < n;i++)
		for (int j = 0; j < m; j++)
			pro[i+1] += land[j][i];
	vector<int> record1(n+1, m);
	record1[0] = 0;
	vector<int> record2(n+1, 0);
	vector<int> record(n+1, 0);
	int sum = 0;
	int min =100000;
	int tt = 0;
	for (int k = 0; k <=n; k++)
	{
		int i = 0;
		int j = k+1;
		while (i<=k) 
		{
			sum += pro[i] - record2[i];
			i++;
		}
		while (j<=n)
		{
			sum += record1[j] - pro[j];
			j++;
		}
		if (sum < min)
		{
			min = sum;
			tt = k;
		}
		sum = 0;
	}
	vector<int> res(2, 0);
	res[0] = tt;
	res[1] = tt+ 1;
	return res;

}
    
    
    ******************************
    1：字符串相关算法：
     KMP
    2：整数处理相关算法
    3：动态规划
    4：贪婪算法
    5：排序算法总结
    6：图论相关
     DFS
     BFS
    7：树相关算法
    8：链表相关

    Mysql 数据库：
    基本操作
      create database db_name; 
      show create database db_name'
      use db_name;
      drop database db_name;
    MyISAM和InnoDB存储引擎
      show engines;支持的有8种。从5.5版本开始，默认支持InnoDB。
      
      InnoDB  需要大量Insert delete update时
        InnoDB是事务安全的，如果表主要提供OLTP
        联机事务处理OLTP（on-line transaction processing）
        联机分析处理OLAP（On-Line Analytica Processing）。
        OLTP是传统的关系型数据库的主要应用，主要是基本的、日常的事务处理，例如银行交易。
        OLAP是数据仓库系统的主要应用，支持复杂的分析操作，侧重决策支持，并且提供直观易懂的查询结果      
        支持外键
      MyISAM 不是事务安全的，也不支持外键。需要大量select是使用
    use choose;
    set default_storage_engine=InnoDB;
    create table my_table(
    taday datetime;
    name char(20);)
    
    显示表结构：
      show tables;
      describle table_name;
    
      show create table table_name;查看详细信息   字段名 数据类型 约束条件 存储引擎 默认字符集等
    系统变量
        show global variables;全局系统变量
        show session variables;会话系统变量
        show session varaibles like ' ';
    备份数据库
        flush tables with read lock;
        
        unlock tables;
    
    3.1 Mysql数据类型
        数值类型
            整数：tinyint smallint mediumint int bigint
            小数 精确小数类型 decimal
            浮点类型 float double
        字符串类型
            char(n)   255
            varchar(n) 
            tinytext
            
            text
            mediumtext
            longtext;
        日期类型
            date time year datatime timestamp
            
            
    3.2 创建表
        create table_name(
        字段n 数据类型 [约束条件]，//主键约束primary key，非空约束 检查约束 默认值约束 唯一性约束(通过唯一性索引实现) 外键约束
        )其他选项()
        
    3.3修改表结构 
    修改字段信息
        删除字段
            alter table table_name drop 字段
        添加字段
        修改字段名
            alter table person change person_name name char(20);
            alter table person modify name char(30)
    修改表名
        alter table person rename human;
    3.5索引 类比新华字典
        前缀索引  不能跨表索引 主索引 聚簇索引
        
    5 表记录查询
    select |where| group by| having| order by

