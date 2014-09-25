MyPart
======
#define _SVID_SOURCE
#include <stdio.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <string.h>
#include <signal.h>
#include <setjmp.h>
#include <stdlib.h>
#include <fcntl.h>
#include <ctype.h>
#include <unistd.h>
#define MAX_CHAR 1024 // Max characters for Input and array sizes

char PROMPT[MAX_CHAR];
char PATH[MAX_CHAR];
char HOME[MAX_CHAR];
char last_dir[MAX_CHAR];
char message[MAX_CHAR];
char alias_for_cd[MAX_CHAR];
int cd_has_alias = 0;

//Structure for alias

typedef struct {
	char *akey;
	char *val;
} alias;

int num_of_alias;
alias **aliases;

jmp_buf (getinput); //Saving environment for setjmp and longjmp

// Setting home directory for new shell

int setHomeDirectory(char home[]) {
	int chk;
	chk = chdir(home);
	//Exception handling of home directory not set successfully
	if (chk != 0) {
		printf("\nError Setting home directory\n");
		return 0;
	}
	return 1;
}

//Function to read profile file and to set environment variables 

void setEnvVar() {

  	char line[MAX_CHAR];
	char word[MAX_CHAR];
	FILE *profileFile;           // Declaring the file pointer
	int a = 0;
	int b = 0;
	
	// opening the profile file in reading mode
	
	profileFile = fopen("profile.txt", "r");  
	
	// Exception handling when profile file is not successfully opened
	
	if (profileFile == NULL)
	{
	    perror("An error occured while opening the profile file. \n");
	    exit(-1);
	 }
	
	//
	do {
		fscanf(profileFile, "%c", &word[a]);
	} while (word[a] != '#');
	do {
		fscanf(profileFile, "%c", &word[a]);
		message[b++] = word[a];
	} while (word[a] != '\n');
	message[b - 1] = '\0';
	b = 0;
	do {
		fscanf(profileFile, "%c", &word[a]);
	} while (word[a] != '#');
	do {
		fscanf(profileFile, "%c", &word[a]);
		PROMPT[b++] = word[a];
	} while (word[a] != '\n');
	PROMPT[b - 1] = '\0';
	b = 0;
	do {
		fscanf(profileFile, "%c", &word[a]);
	} while (word[a] != '#');
	do {
		fscanf(proFile, "%c", &word[a]);
		PATH[b++] = word[a];
	} while (word[a] != '\n');
	PATH[b - 1] = '\0';
	b = 0;
	do {
		fscanf(profileFile, "%c", &word[a]);
	} while (word[a] != '#');
	do {
		fscanf(profileFile, "%c", &word[a]);
		HOME[b++] = word[a];
	} while (word[a] != '\n');
	HOME[b - 1] = '\0';

	int x=setHomeDirectory(HOME);
	
	\\Exception handling 
	if (x != 1) {
		printf("\nError Setting home directory\n");
	}
}
