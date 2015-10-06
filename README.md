# captcha1
program

+// Program to implement Pulse Code Modulation.
// Input : amplitude , frequency , time , no of bits for quatization.
// Output: Pulse code modulated bits of stream
//
#include<math.h>
#include <iostream.h>
#include <fstream.h>
#include<math.h>


int main() {
	int x[512],z[512],A;
	cout<<"Enter Amplitude:";cin>>A;

	float f;
	cout<<"Enter frequency:";cin>>f;
	f=1.0/f;
	int t=0,T;
	cout<<"Enter time:";cin>>T;

	// Compute the sine wave by using frequency and time value
	for(t=0;t<=T;t++)
	{
		x[t] = A * sin(2 * 22.0/7 * f * t); //sine wave input in sine1.txt
		cout<<x[t]<<"  ";
	}

	cout<<"\n\n";
	int b,size,m;

	// decid ethe levels of quantization
	// if bits = 2 , no of levels = 4

	cout<<"Enter No of bits for Quantisation code:";cin>>b;
	m=pow(2,b-1);
	size=A/pow(2,b-1);

	int p,n,k;

	// scan complete time periode
	for(t=0;t<=T;t++)
	{
					if(x[t]>=0)
					{
					   p=0;n=size;
					   for(k=0;k<m;k++)
					   {
						 if(x[t]>=p&&x[t]<=n)
						 {
						  z[t]=k+m;
						  // generate code depending upon level
						  break;
						 }
						 p=n;
						 n=n+size;
					   }

					}
					else
					{
						p=-1;n=-size;
						for(k=0;k<m;k++)
						{
						  if(x[t]<=p&&x[t]>=n)
						  {  // generate code depending upon level
							 z[t]=m-k-1;
							 break;
						  }
						  p=n;
						  n=n-size;
						}

					}

	// generate code for each pulse
	cout<<" "<<z[t];//<<" "<<p<<" "<<n;

	}// end of for


	cout<<"\n\n";
	long i,rem,j=0,sum=0;

	// encode the data in the form of bits.
	for(j=0;j<=T;j++)
	{
		i=1;    sum=0;
		do
		{   // convert the number to binary.
			rem=z[j]%2;
			sum=sum + (i*rem);
			z[j]=z[j]/2;
			i=i*10;
		}while(z[j]>0);
		cout<<" "<<sum;
	}
	cin.get();
	return 0;

}

/*
Output:

Enter Amplitude:20
Enter frequency:10
Enter time:20
0  11  19  19  11  0  -11  -19  -19  -11  0  11  19  19  11  0  -11  -19  -18  -
11  0

Enter No of bits for Quantisation code:3
 4 6 7 7 6 4 1 0 0 1 4 6 7 7 6 4 1 0 0 1 4

PCM signal:  100 110 111 111 110 100 1 0 0 1 100 110 111 111 110 100 1 0 0 1 100

*/











