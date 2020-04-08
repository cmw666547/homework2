#include<iostream>
using namespace std;

int ma(int a[],int n){
int sum,maxs;
int i;
sum=maxs=0;
for(i =0;i<n;i++)
{
sum+=a[i];
if(sum>maxs)
maxs=sum;
else if(sum<0)
sum=0;
}
return maxs;
}
//我们求的是最大字段和，求的是和，要的是结果，一个结果，不必太在意它究竟是哪一段，
//定义一个变量maxs表示这个和，只要这个变量始终能表示最大的一段，最大，就行
//字段全为负的时候为maxs为0，只要有正数在，maxs就有为正的时候，所以说maxs的最小值为0，
//所以maxs初值可以定义为0，字段和比他大就替换，保证maxs始终为最大
//s一直在加和状态，加完变大就给maxs保存，如果加完变小了不给maxs，继续加，静观其变，
//如果变成负数了，再继续加的话，这段负数只会拖后腿导致后面一段和变小的，
//所以，归零即可，相当于继续进行下一段的计算，maxs存的还是上一段的最大值，如果折段的比他大则替换，
//否则不替换，总之maxs为最大，是最大字段和
int main(){
int n;
cin>>n;
int *a=new int [n];
for(int i=0;i<n;i++)
cin>>a[i];
cout<<ma(a,n);
return 0;
}




/*
这个方法不完备，只考虑了相邻两个加完变小就不继续往上加了，生成了一个子段，
但是可能再加一个值还会变大的，这个方法每个元素只对应一个子段形成了n个子段，但是实际上
第一个元素对应n-1个子段，第二个元素对应n-2个子段，而我们用b来存每个子段和，这时候b不再是n个
元素了，而是n的阶乘个元素，虽然也能算出来，但是计算量过于庞大，方法过于笨拙，解决问题有很多种方法，
要学会用简单的方法解决，不要总是想到最笨的方法，另辟蹊径，别有洞天，灵活点
#include <stdio.h>
#include <stdlib.h>

using namespace std;

int main()
{
   int n,i,j,a[10000],b[10000],t,ma,s,k=0,fr;
   scanf("%d",&n);
   for(i=0;i<=n-1;i++)
   {
       scanf("%d",&a[i]);
       if(a[i]<0)
        k++;
   }
   if(k==n)
   {
       printf("0");
       return 0;
   }
   for(i=0;i<=n-1;i++)
   {
       s=0;
       fr=0;
       for(j=i;j<=n-1;j++)
       {
           s+=a[j];
           if(s<fr)
           {
               s=s-a[j];
               b[i]=s;
               break;
           }
           fr=s;
       }
   }
   for(i=0;i<=n-1;i++)
   {
       ma=i;
       for(j=i;j<=n-1;j++)
       {
           if(b[j]>b[ma])
            ma=j;
       }
       t=b[i];
       b[i]=b[ma];
       b[ma]=t;
   }
   printf("%d",b[0]);
}
*/
