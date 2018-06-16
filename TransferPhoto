/**
 * @author Hakeem King
 *
 */
#include <stdio.h>
#include <sys/types.h>
#include <dirent.h> 
#include <stdlib.h>
#include <string.h>
#include <pthread.h>
#define NUM_THREADS 10

void *myThreadFun(void *vargp)
{
    DIR *d;
    struct dirent *dir;

    d = opendir(vargp);
    //buffer for the download command
    char comm[100];
    //buffer for the delete command
    char comm2[100];

    if (d)
    {
        while ((dir = readdir(d)) != NULL){
            sprintf(comm, "-f \"%s\"/ gphoto2 --get-all-files", vargp);
            sprintf(comm, "-f \"%s\"/ gphoto2 --delete-file 1-20", vargp);
            system(comm);
            printf("%s\n",dir->d_name );
        }

    }
    return NULL;
}

int main(void){
    DIR *d;
    ///store_00010001/DCIM/0042
    struct dirent *dir;
    // files 
    char str[100];
    //command
    char comm[100];
    d = opendir("./store_00010001/DCIM/");
    int i = 0;
    if (d)
    {
        while(true){
            pthread_t threads[NUM_THREADS];
            
            while ((dir = readdir(d)) != NULL)
            {
                if(i > 1){
                    sprintf(comm,"./store_00010001/DCIM/%s", dir->d_name);
                    pthread_create(threads + i, NULL, myThreadFun, comm);
                }
                i++;
                sleep(1);
            }
            pthread_exit(NULL);
            d = opendir("./store_00010001/DCIM/");
        }
        closedir(d);
    }
    exit(0);
}
