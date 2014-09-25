MyPart
======
/* Function to read profile file and to set environment variables */

void setEnvVar() {

  char line[MAX_CHAR];
	char word[MAX_CHAR];
	int i = 0;
	int j = 0;
	FILE *profileFile; 
	
	profileFile = fopen("profile.txt", "r");  // opening file in read mode
	
	if (profileFile == NULL)
	{
	    perror("An error occured while opening the file. \n");
	    exit(EXIT_FAILURE);
	 }

	do {
		fscanf(infile, "%c", &word[i]);
	} while (word[i] != ':');
	do {
		fscanf(infile, "%c", &word[i]);
		message[j++] = word[i];
	} while (word[i] != '\n');
	message[j - 1] = '\0';
	j = 0;
	do {
		fscanf(infile, "%c", &word[i]);
	} while (word[i] != ':');
	do {
		fscanf(infile, "%c", &word[i]);
		PROMPT[j++] = word[i];
	} while (word[i] != '\n');
	PROMPT[j - 1] = '\0';
	j = 0;
	do {
		fscanf(infile, "%c", &word[i]);
	} while (word[i] != ':');
	do {
		fscanf(infile, "%c", &word[i]);
		PATH[j++] = word[i];
	} while (word[i] != '\n');
	PATH[j - 1] = '\0';
	j = 0;
	do {
		fscanf(infile, "%c", &word[i]);
	} while (word[i] != ':');
	do {
		fscanf(infile, "%c", &word[i]);
		HOME[j++] = word[i];
	} while (word[i] != '\n');
	HOME[j - 1] = '\0';

	int x=setHomeDirectory(HOME);
	if (x != 1) {
		printf("\nError Setting home directory\n");
	}
}
