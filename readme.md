# CSCI 2275 – Data Structures - Final Project
Authors: Meena Ropp and Christina Fernandez

This project simulates a file system by storing files and directories into an n-ary tree data type. The files are also stored in a hash table to allow for a more efficient search method. The project also explores how different collision resolution methods influence the number of collisions in the hash table.

The following functions were made for the file system commands all within the master branch.

Touch: This command adds a new file into the current directory. It adds a new node to the hashtable and to the n-ary tree as a child of the current directory. However, the function first checks if there is enough space on the disk to add the 1 byte size file, and if there is no room then the user gets an error.

Mkdir: This command adds a new directory into the current directory. This adds a new node to the n-ary tree as a child of the current directory, or as a new sub-directory. This function also first checks if there is enough space on the disk to add this 1 byte size directory. If there is not room then no node is added and the user gets and error message.

Edit: This function takes in a file path and new string to be written to that file. The file is found through a linear search of the current directory's children and if it exists and is in fact a file then the fileData is overwritten with the new string. The fileSize is also changed to be the length of the new string plus one. Also, the file node's modified time is changed to the current time of when the function was called. However, none of these changes are made if the new fileSize makes the disk memory go over capacity.

Ls: This command prints all of the files and subdirectories within the current directory. If the current directory is empty, then this prints nothing.

Tree: This command prints all of the files and subdirectories within the current directory, including the files and subdirectories within other subdirectories.

Rm: This command removes a file or subdirectory from the current directory. If the user wants to remove a directory they are prompted to ensure that this is what they want and if so the subdirectory and all of its contents are deleted. This function also removes the file node from the hash table if the user chooses to remove a file.

Cd: This command changes the current directory that the user is in. If the new directory does not exist then no changes are made.

Mv: This command either moves a file in the current directory to a different directory or changes the filename of the file. If the user chooses to change the file name then it also changes the location of this file node in the hashtable and re-indexes it with the new file name. 

Pwd: This functions prints the path from the current directory to the root, or it's absolute path.

Stat: This function takes in a filename from a file in the current directory and prints information about the file. This includes filename, filesize, filetype, creation time, modified time, and its parent directory.

Cat: This function takes in a filename and prints the data within the file. 

Search: This function takes in a file or directory name. It then utilizes the hash table to print the absolute path to the found file(s) or directory(s).

The following functions were made to collect data about how the type of collision resoution method affects the number of collisions.

insertItemLinear: This function inserts a file into the hash table using the linear probing method. First, this function finds the index of the hash node you'd like to insert, then probes through the hash table starting at that index. If the index already contains a hash node, the function will then iterate through the hashtable by 1 until there is an empty space in the hash table to insert the new hash node. Within this iteration, the function will count the number of collisions that occur. If the index ever exceeds the current set hash table size, the function will then double the size of the table and rehash the current elements. 

insertItemQuadratic: This function inserts a file in the hash table using the quadratic probing method. First, this function finds the index of the hash node you'd like to insert, then probes through the hash table starting at that index. If the index already contains a hash node, the function will then iterate through the hashtable by the index*a^2 until there is an empty space in the hash table to insert the new hash node. Within this iteration, the function will count the number of collisions that occur. If the index ever exceeds the current set hash table size, the function will then double the size of the table and rehash the current elements. 

insertItemChaining: This function inserts a file in the hash table using the linear probing method. First, this function finds the index of the hash node you'd like to insert, then probes through the hash table starting at that index. If the index already contains a hash node, the function will then add the new hash node to a linked list with the head of the list as the current element at the index. The function will count the number of collisions as the number of elements in the linked lists of each index. The hash table will never need to be resized in this function. 

resizeHashTable: This function resizes the hash table by doubling the limit on the amount of hash nodes that can be inserted in the table. In addition, when the table size is doubled, all of the current elements in the table must be rehashed using the current table type (linear, quadratic, chaining) because the hash function is based on the size of the table. 

resetCollisions: This function sets the number of collsions back to 0. 

getCollisions: This function returns the number of collisions from inserting items in the hash table. 
