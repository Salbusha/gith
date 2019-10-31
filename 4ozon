#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
#include <time.h>
#include <sys/wait.h>
#include <sys/types.h>
int main(void){
    int fd[2], i;
    time_t t;
    pipe(fd);
    struct tm *st;
    if(!fork()){
        if(!fork()){
            if(!fork()){
                t = time(NULL);
                for(i = 0; i < 3; i++){
                    write(fd[1], &t, sizeof(t));
                }
                close(fd[0]);
                close(fd[1]);
                exit(0);
            }else{
                close(fd[1]);
                read(fd[0], &t, sizeof(t));
                close(fd[0]);
                wait(NULL);
                st = localtime(&t);
                printf("D:%d\n", st->tm_mday);
                fflush(stdout);
            }
            exit(0);
        }else{
            close(fd[1]);
            read(fd[0], &t, sizeof(t));
            close(fd[0]);
            wait(NULL);
            st = localtime(&t);
            printf("M:%d\n", st->tm_mon + 1);
            fflush(stdout);
        }
        exit(0);
    }else{
        close(fd[1]);
        read(fd[0], &t, sizeof(t));
        close(fd[0]);
        wait(NULL);
        st = localtime(&t);
        printf("Y:%d\n", st->tm_year + 1900);
        fflush(stdout);
        exit(0);
    }
}
