#include<stdio.h>
#include<stdlib.h>
#include<math.h>
int randomgen (int a, int b)
{
  return rand () % (b);
}
void main()
{
  float x1[70],x2[70],target[70],y_predicted[50],M1,M2,bias,lr=0.03;
  for(int i=0;i<70;i++)
  {
    x1[i]=randomgen(1,50);
    x2[i]=randomgen(1,50);
  }
  printf("Enter M1 : ");
  scanf("%f",&M1);
  printf("Enter M2 : ");
  scanf("%f",&M2);
  printf("Enter bias : ");
  scanf("%f",&bias);
  for(int i=0;i<70;i++)
  {
    if((M1*x1[i]+M2*x2[i])>=bias)
    target[i]=1;
    else
    target[i]=0;
  }
  float cost=0,summ1,summ2,sumbai,m1=1,m2=2,bai=3;
  int prassy=1500;
while(prassy--)  
{
  cost=0;
  summ1=0;summ2=0;sumbai=0;
  for(int i=0;i<50;i++)
  {
    y_predicted[i]=1/(1+exp(-((m1*x1[i])+(m2*x2[i])+bai)));
  }
  for(int i=0;i<50;i++)
  {
    cost=cost+((-target[i]*log(y_predicted[i]))-(1-target[i])*log(1-y_predicted[i]));
  }
  for(int i=0;i<50;i++)
  {
   summ1+=(y_predicted[i]-target[i])*x1[i];
   summ2+=(y_predicted[i]-target[i])*x2[i];
   sumbai+=(y_predicted[i]-target[i]);
  }
  m1=m1-(lr*summ1)/100;
  m2=m2-(lr*summ2)/100;
  bai=bai-(lr*sumbai)/100;
  printf(" cost : %f \n m1 : %f \n m2 : %f \nbias : %f      \n" ,cost,m1,m2,bias);

} 
for(int i=0;i<50;i++)
printf("%f        %f\n" ,target[i],y_predicted[i]);
printf("\n***************Predictions******************\noriginal     |       predicted\n");
for(int i=51;i<70;i++)
{
  printf("%f     |     %f\n",target[i],1/(1+exp(-((m1*x1[i])+(m2*x2[i])+bai))));
}
printf("\n*********** 100 percent working model***********************");
}


