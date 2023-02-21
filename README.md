# rope
# c
첫째 줄에 정수 N이 주어진다. 다음 N개의 줄에는 각 로프가 버틸 수 있는 최대 중량이 주어진다. 각각의 로프는 그 굵기나 길이가 다르기 때문에 들 수 있는 물체의 중량이 서로 다르고 여러 개의 로프를 병렬로 연결하면 각각의 로프에 걸리는 중량을 나눌 수 있다. k개의 로프를 사용하여 중량이 w인 물체를 들어올릴 때, 각각의 로프에는 모두 고르게 w/k 만큼의 중량이 걸리게 된다 이 로프들을 이용하여 들어올릴 수 있는 물체의 최대 중량을 구해내는 프로그램을 작성해보자! (모두사용할필요 없고 골라서 사용가능)

#include <stdio.h>
#include <stdlib.h> //qsort()함수  
#include <string.h>

/*int comp (const void *a,const void * b){ //qsort를 이용하면 이런방식도 가능하다는 점
    return *(int *)b - *(int *)a;}*/


int maxcheck(int x,int y){
	return x>y ? x:y;}
	
	
void main(){
	int i,n,j;
	int weight[100];
	scanf("%d",&n);
	for(i=0;i<n;i++){
		scanf("%d",&weight[i]);}
	for(i=0;i<n;i++){
		for(j=0;j<n-(i+1);j++){ //이거 대신에 qsort도 이용가능!  
			if(weight[j]<weight[j+1]){//내림차순으로 먼저 정렬  
				int tmp;
				tmp=weight[j];
				weight[j]=weight[j+1];
				weight[j+1]=tmp;}}}
	//qsort(weight,n,sizeof(int),comp);
	int max=0; //제일 큰값은 병렬 연결하지 않는다  
	for(i=0;i<n;i++){ //무게중에서 큰값은 1번 작아질수로 작은값에 곱하기 1씨증가시켜야 함--> 병렬연결은 연결하는 제일작은 값보다 크면 줄이 끊어진다! 
		max=maxcheck(max,weight[i]*(i+1));} //예로 10 15가 있다면 10,15,(10+10)이런경우가 나올수 있다 
	printf("로프를 사용해서 가장 둘수 있는 최대무게는: %d\n",max);  } 
