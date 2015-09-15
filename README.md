# paralelos

#include <mpi.h>
#include <stdio.h>
#include <string.h>
#include <time.h>
//#include <iostream.h>
//#include <dos.h>


//#define BUFSIZE 128
#define TAG 0

int main(int argc, char *argv[])
{
  //char idstr[32];
  //char buff[BUFSIZE];
  int size;
  int rank;
  //int i;
  int num=10;
  MPI_Status stat;

  MPI_Init(&argc,&argv); 
  MPI_Comm_size(MPI_COMM_WORLD,&size); 
  MPI_Comm_rank(MPI_COMM_WORLD,&rank); 
  
  if(rank == 0)
  {
	printf("ingrese %d \n", num);
	//scanf("%d", &num);
  }
  else
  {
	/* Recibe del rank 0: */
	MPI_Recv(&num, 1, MPI_INT, rank-1, TAG, MPI_COMM_WORLD, &stat);
	printf("Recibi %d de %d procesador\n", num, rank);
	
	
  }
  if(size-1>rank)
  {
   	MPI_Send(&num, 1, MPI_INT, rank+1, TAG, MPI_COMM_WORLD);
  }
  
  //cout<<"recibi "<<num<<"de"<<rank<<endl;
  MPI_Finalize(); 
  return 0;
}
