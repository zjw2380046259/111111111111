#include<stdio.h>
#include<string.h>
#include<windows.h>
void welcome ()
{
	printf("+----------------------------+\n");
	printf("|                            |\n");
	printf("|  欢迎使用储蓄综合业务平台  |\n");
	printf("|                            |\n");
	printf("+----------------------------+\n");
	
	int x;
	char a[10]="admin";
	char userName[10];
	char userPWD[10];
	for(x=0;x<3;x++)
	{
		printf("请输入用户名：");
		scanf("%s",userName);
		printf("\n请输入密码:");
		scanf("%s",userPWD);
		if (strcmp(a,userName)==0&&strcmp(a,userPWD)==0)
		{
			printf("\n欢迎使用本系统\n");
			break;
		}
		else
		{
			printf("\n用户名或密码错误\n");
		}
	}
	if(x==3)
	{
		exit(0);
	}
}

	void menu()
{
    printf("+--------------------------------+\n");
	printf("|   存款 请按1      销户 请按5   |\n");	
	printf("|   取款 请按2      信息 请按6   |\n");
	printf("|   查询 请按3      转账 请按7   |\n");
	printf("|   开户 请按4      退出 请按0   |\n");
    printf("+--------------------------------+\n");
}

void funChoose()
{
	printf("请输入要选择的功能\n");
    int b;
    while(1>0)
    {
    	scanf("%d",&b);
    	switch(b)
    	{
    		case 0:
    			printf("这是退出功能的实现\n");
    			exit(0);
    		case 1:
    			printf("这是存款功能的实现\n");
    			menu();
    			break;
    		case 2:
    			printf("这是取款功能的实现\n");
    			menu();
    			break;
    		case 3:
    			printf("这是查询功能的实现\n");
    			menu();
    		    break;
    		case 4:
    			printf("这是开户功能的实现\n");
    			menu();
    			break;
    		case 5:
    			printf("这是销户功能的实现\n");
    			menu();
    			break;
    		case 6:
    			printf("这是信息功能的实现\n");
    			menu();
    			break;
    		case 7:
    			printf("这是转账功能的实现\n");
    			menu();
    			break;	
    	}

    }
}
int main()
{
    welcome();
    menu();
    funChoose();
	return 0;
}
