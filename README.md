#include<stdio.h>
#include<string.h>
#include<stdlib.h>

void welcome();
void funChoose();
void openAccount();
void deposit();
void AccountCancellation();
void query();
void withdrawMoney();
void information();
void transferAccounts();

int h=0;//数组的下标
struct userinFormation
{
    int accountNumber;//账号
    double amountOfMoney;//金额
    char userName[10];//用户名
    char password[10];//密码
    char state[5];//状态
}account[100];

void welcome()//登陆系统
{
    printf("+--------------------------------+\n");
    printf("|                                |\n");
    printf("|       欢迎使用银行储蓄系统        |\n");
    printf("|                                |\n");
    printf("+--------------------------------+\n");
    char a[20];
    char b[20];
    int c=0;
    while(1)
    {
        printf("请输入用户名:");
        scanf("%s",a);
        printf("\n");
        printf("请输入密码：");
        scanf("%s",b);
        printf("\n");
        if(strcmp(a,"admin")==0&&strcmp(b,"admin")==0)
        {
            printf("欢迎使用本系统！！！\n");
            return ;
        }
        else
        {
            c++;
            printf("用户名或密码输入错误，请重新输入\n");
        }
        if(c==3)
        {
            exit(0);
        }
    }
}

void funChoose ()//功能菜单
{
    int put;
    while(1)
    {
        printf("+-----------------------------------+\n");
        printf("|   存款 1             取款 2        ｜\n");
        printf("|   查询 3             开户 4        |\n");
        printf("|   销户 5             信息 6        |\n");
        printf("|   转账 7             退出 0        |\n");
        printf("+-----------------------------------+\n");
        printf("请输入需要使用功能后的数字:");
        scanf("%d",&put);
        if(put<=8&&put>=0)
        {
            switch(put)
            {
                case 1:
                deposit();
                break;
                case 2:
                withdrawMoney();
                break;
                case 3:
                query();
                break;
                case 4:
                openAccount();
                break;
                case 5:
                AccountCancellation();
                break;
                case 6:
                information();
                break;
                case 7:
                transferAccounts();
                break;
                case 0:
                return ;
            }
        }
        else
        {
            printf("输入错误，请重新输入！！\n");
        }
        
    }
}

void openAccount ()//开户
{
    int a=1;
    int c;
    long n;
    while(1)
    {
        if(a==1)
        {
            printf("请输入用户名：");
            scanf("%s",account[h].userName);
            if(strlen(account[h].userName)<6)
            {
                a++;
                continue;
            }
            else 
            {
                printf("\n用户长度不正确！！请重新输入用户名！！\n");
            }
        }
        if(a==2)
        {
            printf("请输入六位的密码：");
            scanf("%s",account[h].password);
            if(strlen(account[h].password)==6)
            {
                a++;
                continue;
            }
            else
            {
                printf("密码的长度不正确！！请重新输入密码！！\n");
            }
        }
        if(a==3)
        {
            printf("请输入存入金额：");
            scanf("%lf",&account[h].amountOfMoney);
            n=account[h].amountOfMoney;
            for(c=0;n>0;c++)
            {
                n=n/10;
            }
            if(c<=12)
            {
                strcpy(account[h].state,"正常");
                account[h].accountNumber=10001+h;
                printf("+-------------------------------------------+\n");
                printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
                printf("|—------------------------------------------|\n");
                printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[h].accountNumber,account[h].userName,account[h].password,account[h].amountOfMoney,account[h].state);
                printf("|-------------------------------------------+\n");
                h++;
                break;
            }
            else if (c>12)
            {
                printf("\n超过存入最大金额！请重新输入！！\n");
                continue;
            }


        }
    }
}

void deposit()//存款
{
    int b,c;
    double d;
    printf("请输入需要存入的账户：");
    scanf("%d",&c);
    for(b=0;b<=99;b++)
    {
        if(c==b+10001)
        {
            if(strcmp(account[b].state,"正常")==0)
            {
                printf("请输入存入的金额:");
                scanf("%lf",&d);
                if(d>0)
                {
                    account[b].amountOfMoney+=d;
                    printf("+-------------------------------------------+\n");
                    printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
                    printf("|—------------------------------------------|\n");
                    printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[b].accountNumber,account[b].userName,account[b].password,account[b].amountOfMoney,account[b].state);
                    printf("|-------------------------------------------+\n");
                    break;
                }
                else
                {
                    printf("输入错误！！");

                }
            }
            else
            {
                printf("该账户已经注销！！\n");
                return ;
            }
        }
    }

    if(b==100)
    {
        printf("查无此帐！！");
    }
    
}

void AccountCancellation()//销户
{
    int x,b,c=0;
    printf("请输入需要销户的账号：");
    scanf("%d",&x);
    for(b=0;b<100;b++)
    {
        if(x==account[b].accountNumber)
        {
            printf("+-------------------------------------------+\n");
            printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
            printf("|—------------------------------------------|\n");
            printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[b].accountNumber,account[b].userName,account[b].password,account[b].amountOfMoney,account[b].state);
            printf("|-------------------------------------------+\n");
            printf("确认销号请按1，或按其他键返回菜单！\n");
            scanf("%d",&c);
            if(c==1)
            {
                account[b].amountOfMoney=0;
                strcpy(account[b].state,"销户");
                printf("+-------------------------------------------+\n");
                printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
                printf("|—------------------------------------------|\n");
                printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[b].accountNumber,account[b].userName,account[b].password,account[b].amountOfMoney,account[b].state);
                printf("|-------------------------------------------+\n");

            }
            else
            {
                printf("\n已取消销户！\n");
            }

        }
    }
    if(b==100&&c==0)
    {
        printf("查无此帐！！\n");
    }
}

void query()//查询
{
    int a,b;
    printf("请输入需要查询的账号：");
    scanf("%d",&a);
    for(b=0;b<100;b++)
    {
        if(account[b].accountNumber==a)
        {
            printf("+-------------------------------------------+\n");
            printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
            printf("|—------------------------------------------|\n");
            printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[b].accountNumber,account[b].userName,account[b].password,account[b].amountOfMoney,account[b].state);
            printf("|-------------------------------------------+\n");
            break;

        }
    }
    if(b==100)
    {
        printf("查无此帐！！\n");
    }
}

void withdrawMoney ()//取款
{
    int a,b;
    double d;
    char c[10];
    printf("请输入需要取款的账户：");
    scanf("%d",&a);
    for(b=0;b<100;b++)
    {
        if(account[b].accountNumber==a)
        {
            if(strcmp(account[b].state,"销户")==0)
            {
                printf("该账号已销户！！\n");
                break;
            }
            else
            {
                printf("请输入密码：");
                scanf("%s",c);
                if(strcmp(c,account[b].password)==0)
                {
                    printf("请输入取款金额");
                    scanf("%lf",&d);
                    if(d>0)
                    {
                        account[b].amountOfMoney-=d;
                        printf("+-------------------------------------------+\n");
                        printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
                        printf("|—------------------------------------------|\n");
                        printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[b].accountNumber,account[b].userName,account[b].password,account[b].amountOfMoney,account[b].state);
                        printf("|-------------------------------------------+\n");
                        break;

                    }
                    if(d<0)
                    {
                        printf("金额输入错误！！\n");
                        return ;
                    }
                }
                else
                {
                    printf("密码输入错误！！\n");
                    return ;
                }
            }

        }
    }
    if(b==100)
    {
        printf("查无此帐！！\n");
    }
}

void information()//信息
{
    int b;
    for(b=0;b<h;b++)
    {
        printf("+-------------------------------------------+\n");
        printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
        printf("|—------------------------------------------|\n");
        printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[b].accountNumber,account[b].userName,account[b].password,account[b].amountOfMoney,account[b].state);
        printf("|-------------------------------------------+\n");

    }
}

void transferAccounts()//转账
{
    int a,b,d,e;
    double f;
    char c[10];
    printf("请输入账号：");
    scanf("%d",&a);
    for(b=0;b<100;b++)
    {
        if(a==account[b].accountNumber)
        {
            if(strcmp(account[b].state,"销户")!=0)
            {
                printf("请输入密码：");
                scanf("%s",c);
                if(strcmp(c,account[b].password)==0)
                {
                    printf("+-------------------------------------------+\n");
                    printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
                    printf("|—------------------------------------------|\n");
                    printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[b].accountNumber,account[b].userName,account[b].password,account[b].amountOfMoney,account[b].state);
                    printf("|-------------------------------------------+\n");
                    break;
                }
                else
                {
                    printf("密码输入错误！！\n");
                    return ;
                }
            }
            else
            {
                printf("该账户已经注销！！\n");
                return ;
            }
        }
    }
    if(b==100)
    {
        printf("查无此帐！！\n");
        return ;
    }
    printf("请输入接受款项的账号：");
    scanf("%d",&d);
    for(e=0;e<100;e++)
    {
        if(d==account[e].accountNumber)
        {
            printf("+-------------------------------------------+\n");
            printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
            printf("|—------------------------------------------|\n");
            printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[e].accountNumber,account[e].userName,account[e].password,account[e].amountOfMoney,account[e].state);
            printf("|-------------------------------------------+\n");
            if(strcmp(account[e].state,"销户")!=0)
            {
                printf("请输入转账金额：");
                scanf("%lf",&f);
                if(f>0)
                {
                    account[b].amountOfMoney-=f;
                    account[e].amountOfMoney+=f;
                    printf("+-------------------------------------------+\n");
                    printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
                    printf("|—------------------------------------------|\n");
                    printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[b].accountNumber,account[b].userName,account[b].password,account[b].amountOfMoney,account[b].state);
                    printf("|-------------------------------------------+\n");
                    printf("+-------------------------------------------+\n");
                    printf("|  账号  |  用户名  |  密码  |  金额  |状态 |\n");
                    printf("|—------------------------------------------|\n");
                    printf("|%-8d|%-10s|%-8s|%-8.2f|%-5s |\n",account[e].accountNumber,account[e].userName,account[e].password,account[e].amountOfMoney,account[e].state);
                    printf("|-------------------------------------------+\n");
                    printf("转账成功！！！\n");
                    break;
                }
                else
                {
                    printf("输入错误！！\n");
                    return ;
                }
            }
            else
            {
                printf("该账户已经注销！！\n");
                return ;
            }
        }
    }
    if(e==100)
    {
        printf("查无此帐！！\n");
        return ;
    }

}
int main ()//主函数
{
    welcome();
    funChoose();
    return 0;
}

