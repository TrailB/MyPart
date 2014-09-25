MyPart
======
/* Function to read profile file and to set environment variables */

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
	} while (word[a] != ':');
	do {
		fscanf(profileFile, "%c", &word[a]);
		message[b++] = word[a];
	} while (word[a] != '\n');
	message[b - 1] = '\0';
	b = 0;
	do {
		fscanf(profileFile, "%c", &word[a]);
	} while (word[a] != ':');
	do {
		fscanf(profileFile, "%c", &word[a]);
		PROMPT[b++] = word[a];
	} while (word[a] != '\n');
	PROMPT[b - 1] = '\0';
	b = 0;
	do {
		fscanf(profileFile, "%c", &word[a]);
	} while (word[a] != ':');
	do {
		fscanf(proFile, "%c", &word[a]);
		PATH[b++] = word[a];
	} while (word[a] != '\n');
	PATH[b - 1] = '\0';
	b = 0;
	do {
		fscanf(profileFile, "%c", &word[a]);
	} while (word[a] != ':');
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
