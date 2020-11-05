# experiment8
experiment homework
//成绩管理系统v4

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define maxlen 40
#define maxnumber 30

/*结构体student
学号 num
姓名 name[maxlen]
各科成绩 score[maxnumber]
个人总分 sum
个人平均分 average
*/
typedef struct student{

    long int num;
    char name[maxlen];
    float score[maxnumber];
    float sum;
    float average;


}STU;

/*
******函数名称：Menu
******输入：无
******输出：无
******功能：打印菜单*/

void Menu(){
 printf ("1. Input record\n2. Calculate total and average score of every course\n3. Calculate total and average score of every student\n4. Sort in descending order by total score of every student\n");
printf("5. Sort in ascending order by total score of every student\n6. Sort in ascending order by number\n7. Sort in dictionary order by name\n8. Search by number\n9. Search by name\n10.Statistic analysis for every course\n11.List record\n0. Exit\n");
printf("Please enter your choice:");}
/*
******函数名称：inputdata
******输入：STU stu[30]（学生数组结构体）,int m（课程数目）,int n（学生数目）,char nameclass[][maxlen]（课程名）
******输出：无
******功能：录入学号，各科成绩*/

void inputdata(STU stu[30],int m,int n,char nameclass[][maxlen]){


        printf("\n请先录入学号再录入成绩并用空格分隔开。\n学号\t 姓名\t");

        for(int j=0;j<m;j++){ printf("  %s\t",nameclass[j]);}

                printf("\n");

for(int i=0;i<n;i++){
        scanf("%ld",&stu[i].num);

        scanf("%s",stu[i].name);
        stu[i].sum=0;
        for(int j =0;j<m;j++){
            scanf("%f",&stu[i].score[j]);
            stu[i].sum +=stu[i].score[j];
        } stu[i].average=(1.0*stu[i].sum)/m;
    }


}
/*
******函数名称：outputdata
******输入：STU stu[30]（结构体学生数组）,int m（课程的数目）,int n（学生的人数）,char nameclass[][maxlen]（课程名）
******输出：无（按着排名，学号，姓名，总成绩的次序打印成绩）
******功能：实现列表的打印*/


void outputdata(STU stu[30],int m,int n,char nameclass[][maxlen]){



        for(int j=0;j<m;j++){ printf("  %s\t",nameclass[j]);}

        printf("\n");

        printf("排名\t    学号\t    姓名\t    总分\t\n");

        printf("********************************************\n");
          for(int i=0;i<n;i++){

             printf("No.%d\t   %5ld\t   %5s\t    %.2f\n",i+1,stu[i].num,stu[i].name,stu[i].sum);
          }
          printf("\n");
}
/*
******函数名称：Student_Average
******输入：STU stu[]（结构体学生数组）, int   m（课程数目）,int  n（学生数目）
******功能：实现计算每个学生的总分和平均分。*/


void Student_Average(STU stu[], int   m,int  n){
int i;
float Average;
float Sum;

            printf("学号\t姓名\t总分\t平均分\t");
            printf("\n*************************\n");
           for( i=0;i<n;i++){

               printf("%ld\t%3s\t  %1.2f\t %1.2f\t\n",stu[i].num,stu[i].name,stu[i].sum,stu[i].average);
           }
           for(i=0;i<n;i++){
            Sum+=stu[i].average;
           }
           Average=Sum/n;
            printf("全班平均分为%1.2f\n",Average);

}/*
******函数名称：Subject_Average
******输入： STU stu[](结构体学生数组), char nameclass[][maxlen]（课程名称）,int   m（课程数目）,int  n（学生的人数）
******输出：无（
******功能：实现计算每门课程的总分和平均分。*/

void Subject_Average(STU stu[], char nameclass[][maxlen],int   m,int  n)
    {int i,j;
     float subjectsum[maxnumber];
     float subjectaverage[maxnumber];
    for(j=0;j<m;j++){

        for(i=0;i<n;i++){subjectsum[j]+=stu[i].score[j];}

                    }


        for(j=0;j<m;j++){subjectaverage[j]=(1.0*subjectsum[j])/n;}

       for(i=0;i<m;i++){ printf("%2s总分\t%2s平均分\t",nameclass[i],nameclass[i]);}
       printf("\n********************************************\n");

       for(j=0;j<m;j++){printf("%1.2f\t%1.2f\t",subjectsum[j],subjectaverage[j]);}
       printf("\n");


/*
******函数名称：sort
******输入： STU stu[]（结构体学生数组）, int m（课程的数目）,int n（学生的数目）, int x（标志变量）,int *compare(int a,int b)（比较函数指针）
******输出：无
******功能：实现成绩或学号的升降序。*/




    }void  Sort(STU stu[], int m,int n, int x,int *compare(int a,int b)) {

    int i, j, k;
    STU temp;

    for (i=0; i<n-1; i++)
    {
        k = i;
        for (j=i+1; j<n; j++){
        switch(x){
        case 1:if ((*compare)(stu[j].sum,stu[k].sum))
            {
                k = j;    /*记录最大数下标位置*/
            }break;
        case 2:if ((*compare)(stu[j].num,stu[k].num))
            {
                k = j;    /*记录最大数下标位置*/
            }break;
                }
                               }
        if (k != i)       /*若最大数不在下标位置i*/
        {   {   temp=stu[k];stu[k]=stu[i];stu[i]=temp;}

        }

    }


}


/*
****** 函数名称：Descending_order（Sort分支函数）
****** 输入：a（可能是score[j] or number[j]）,b(可能是score[k] or number[k])
****** 输出：a>b(两个数的大小关系)
****** 功能：实现对两个数的降序大小比较返回*/
int Descending_order(int a,int b){
return a>b;}

/*
****** 函数名称：Ascending_order（Sort分支函数）
****** 输入：a（可能是score[j] or number[j]）,b(可能是score[k] or number[k])
****** 输出：a<b(两个数的大小关系)
****** 功能：实现对两个数的升序大小比较返回*/
int Ascending_order(int a,int b){
return a<b;}



/*
****** 函数名称：Charsort
****** 输入： STU stu[](学生结构体数组),int n（学生的数目）
****** 输出：无
****** 功能：按字典排序对姓名进行排序*/

void Charsort(STU stu[],int n){
    int i,j;
    STU temp;

    for(i=0;i<n-1;i++){
        for(j=i+1;j<n;j++){
                if(strcmp(stu[i].name,stu[j].name)>0){
                        temp=stu[i];stu[i]=stu[j];stu[j]=temp;

                                             }
                          }
                      }

}
/*
****** 函数名称：Search_by_number
****** 输入：STU stu[]（学生结构体数组）,int m（课程数目）,int n（学生数目）,long searchnumber[](搜索的学号)char nameclass[][maxlen]（课程名）
****** 输出：如果找到输出一系列的信息，如果没有则输出不存在
****** 功能：实现对对应学号的成绩查找和排名查找*/
void   Search_by_number(STU stu[],int m,int n ,long searchnumber,char nameclass[][maxlen]){//顺序查找
    int i,k=-1;

    for(i=0;i<n;i++){
        if(stu[i].num==searchnumber){
                k = i;
                break;             }
                    }

         if(k!=-1) {printf("您要查找到的学号为%d，姓名为%s的排名是%d\n",stu[k].num,stu[k].name,k+1);
                    for(i=0;i<m;i++){printf("%s的成绩是%1.2f\t",nameclass[i],stu[k].score[i]);}
                    printf("\n");

                   }
         else printf("你要查找的%d不存在\n",searchnumber);}
 /*
****** 函数名称：Search_by_name
****** 输入：STU stu[]（学生结构体数组）,int m（课程数目）,int n（学生数目）,char searchname[](搜索的姓名)char nameclass[][maxlen]（课程名）
****** 输出：如果找到输出一系列的信息，如果没有则输出不存在
****** 功能：实现对对应姓名的成绩查找和排名查找*/
void   Search_by_name(STU stu[],int m,int n ,char searchname[],char nameclass[][maxlen]){
    int i;int flag=0;
    int k;
    for(i=0;i<n;i++){
        if(strcmp(stu[i].name,searchname)==0){
        flag=1;
        break;}

                    }
        k=i;
    if(flag==1){printf("您要查找到的学号为%d，姓名为%s的排名是%d\n",stu[k].num,stu[k].name,k+1);
                    for(i=0;i<m;i++){printf("%s的成绩是%1.2f\t",nameclass[i],stu[k].score[i]);}
                printf("\n");

              }
    else printf("您要查找的%s不存在！\n",searchname);

}
/*
****** 函数名称：Statistic_analysis
****** 输入：STU stu[]（学生结构体数组）,int m（课程数目）,int n（学生数目）,char nameclass[][maxlen]（课程名）
****** 输出：无（printf语句输出优秀人数和各比例占比）
****** 功能：输出各科优秀人数和各比例占比*/
void Statistic_analysis(STU stu[],int m,int n,char nameclass[][maxlen]){
    int A,B,C,D,E;
    int i,j;
     float A1,B1,C1,D1,E1;
    for(j=0;j<m;j++){  A=0,B=0,C=0,D=0,E=0;
        for(i=0;i<n;i++){
              if(stu[i].score[j]<60)   E++;
                else if(stu[i].score[j]>=60&&stu[i].score[j]<70)   D++;
                else if(stu[i].score[j]>=70&&stu[i].score[j]<80)   C++;
                else if(stu[i].score[j]>=80&&stu[i].score[j]<90)   B++;

                else A++; }
                 A1=(1.0*A)/n*100,B1=(1.0*B)/n*100,C1=(1.0*C)/n*100,D1=(1.0*D)/n*100,E1=(1.0*E)/n*100;
                    printf("%s",nameclass[j]);
                    printf("优秀的有%d人占比 %.2f%%\n良好的有%d人占比 %.2f%%\n中等的有%d人占比 %.2f%%\n合格的有%d人占比 %.2f%%\n不及格的人数有%d人占比 %.2f%%\n\n\n",A,A1,B,B1,C,C1,D,D1,E,E1);
                     }


}

/*
****** 函数名称：List_record
****** 输入：STU stu[]（学生结构体数组）,int m（课程数目）,int n（学生数目）,char nameclass[][maxlen]（课程名）
****** 输出：无
****** 功能：.输出每个学生的学号、姓名、各科考试成绩、总分、平均分*/
void List_record(STU stu[],int m,int n,char nameclass[][maxlen]){
     int i,j;
     float sum;
     float Average[maxnumber];
       for(i=0;i<n;i++){

            for(j=0;j<m;j++){stu[i].sum+=stu[i].score[j];}

                        }

       for(i=0;i<n;i++){

            sum+=stu[i].sum;

                       }

        for(i=0;i<n;i++){
            Average[i]=(stu[i].sum*1.0)/m;
                        }


            printf("学号\t姓名\t总分\t平均分\t");
            for(i=0;i<m;i++){printf("%s\t",nameclass[i]);}
            printf("\n*************************\n");

           for(i=0;i<n;i++){

               printf("\n%ld\t%3s\t%1.2\t %1.2f\t",stu[i].num,stu[i].name,stu[i].sum,Average[i]);
               for(j=0;j<m;j++){printf("%1.2f\t",stu[i].score[j]);}

           }printf("\n");

}



int main()
{  printf("Number:200111102\n");
    printf("Subject 8 -program 1\n");
    printf("欢迎来到成绩管理系统v4.0\n现在你可以选择以下几个功能：\n");
    Menu();
    STU stu[30];
    float a;
    char nameclass[maxlen][maxlen];
    int x;
    char ch;
    int i,j;
    char searchname[maxlen];
    int n,m;
    long searchnumber;


do{ printf("\n请输入你的选择：");
    scanf("%f",&a);
        while((int)a!=a||a<0||a>11)//安全性防护防止用户输入字母还有浮点数以及选项之外的数
        {
            while ((ch=getchar())!=EOF&&ch!='\n');
            printf("\n请重新输入你的选择：");
            scanf("%f",&a);
        }
    int b=(int)a;
    int i=0,j=0;

    switch (b){//switch case对应不同的功能
    case 1:printf("1．Input record\n");

           printf("\n请先输入你要录入人的个数：");
           scanf("%d",&n);

           printf("\n请输入你要录入的课程门数：");
           scanf("%d",&m);

          printf("并输入这些课程的名称：");
          for(j=0;j<m;j++){

            scanf("%s",nameclass[j]);

                           }
           inputdata( stu, m, n, nameclass);
            Menu();
            break;

   case 2:printf("2. Calculate total and average score of every course\n");
           Subject_Average( stu,nameclass, m , n);
           Menu();
            break;

   case 3:printf("3. Calculate total and average score of every student\n");
           Student_Average(stu, m,n);
           Menu();
           break;

   case 4:printf("4. Sort in descending order by total score of every student\n");
           x=1;
           Sort(stu,  m, n,  x,Descending_order );
           outputdata( stu, m, n, nameclass);
            Menu();
            break;


    case 5:printf("5. Sort in ascending order by total score of every student\n");
           x=1;
           Sort(stu,  m, n,  x,Ascending_order );
           outputdata( stu, m, n, nameclass);
           Menu();
           break;

    case 6:printf("6. Sort in ascending order by number\n");
           x=2;
           Sort(stu,  m, n,  x,Ascending_order );
           outputdata( stu, m, n, nameclass);
           Menu();
           break;

    case 7:printf("7. Sort in dictionary order by name\n");
            Charsort(stu, n);
            outputdata( stu, m, n, nameclass);
            break;

   case 8:printf("8. Search by number\n");
           printf("请输入你要查询的学号：");
            scanf("%ld",&searchnumber);
            x=1;
           Sort(stu,  m, n,  x,Descending_order );
            Search_by_number(stu, m, n , searchnumber, nameclass);
            Menu();
            break;


    case 9:printf("9. Search by name\n");
           printf("请输入你要输入的姓名：");
           x=1;
           Sort(stu,  m, n,  x,Descending_order );
           scanf("%s",searchname);
           Search_by_name(stu, m,n , searchname, nameclass);
           Menu();
           break;


   case 10:printf("10.Statistic analysis for every course\n");
           Statistic_analysis(stu, m,n, nameclass);
           Menu();
           break;

   case 11:printf("11.List record\n");
           List_record(stu, m, n, nameclass);
           Menu();
           break;

   case 0:printf("已退出");
          exit(0);
    }
           }while(a!=0);
}
