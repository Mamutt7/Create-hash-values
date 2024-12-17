# Create-hash-values

Activity overview
As a security analyst, you’ll need to implement security controls to protect organizations against a range of threats.

That’s where hashing comes in. Previously, you learned that a hash function is an algorithm that produces a code that can’t be decrypted. Hash functions are used to uniquely identify the contents of a file so that you can check whether it has been modified. This code provides a unique identifier known as a hash value or digest.

For example, a malicious program may mimic an original program. If one code line is different from the original program, it produces a different hash value. Security teams can then identify the malicious program and work to mitigate the risk.

Many tools are available to compare hashes for various scenarios. But for a security analyst it’s important to know how to manually compare hashes.

In this lab activity, we’ll create hash values for two files and use Linux commands to manually examine the differences.

## Scenario
In this scenario, we need to investigate whether two files are identical or different.

Here’s how you'll do this task: First, you’ll display the contents of two files and create hashes for each file. Next, you’ll examine the hashes and compare them.

Let’s hash some files!

### Task 1. Generate hashes for files
The lab starts in your home directory, `/home/analyst`, as the current working directory. This directory contains two files `file1.txt` and `file2.txt`, which contain same data.

In this task, you need to display the contents of each of these files. You’ll then generate a hash value for each of these files and send the values to new files, which you’ll use to examine the differences in these values later.

1. Use the ls command to list the contents of the directory.
Two files, `file1.txt` and `file2.txt`, are listed.

2. Use the cat command to display the contents of the file1.txt file:
```
cat file1.txt
```

3. Use the cat command to display the contents of the file2.txt file:
```
cat file2.txt
```
4. Review the output of the two file contents:
```
analyst@4fb6d613b6b0:-$ cat file1.txt
X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*
analyst@4fb6d613b6b0:-$ cat file2.txt
X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*
```
![image](https://github.com/user-attachments/assets/f41c8ed3-eb78-417f-8119-699919af8630)


Although the contents of both files appear identical when you use the cat command, you need to generate the hash for each file to determine if the files are actually different.

Use the sha256sum command to generate the hash of the `file1.txt` file:
```
sha256sum file1.txt 
```
You now need to follow the same step for the `file2.txt` file.

Use the sha256sum command to generate the hash of the `file2.txt` file:
```
sha256sum file2.txt
```
Review the generated hashes of the contents of the two files:
```
analyst@4fb6d613b6b0:-$ sha256sum file1.txt
131f95c51cc819465fa1797f6ccacf9d494aaaff46fa3eac73ae63ffbdfd8267  file1.txt
analyst@4fb6d613b6b0:-$ sha256sum file2.txt
2558ba9a4cad1e69804ce03aa2a029526179a91a5e38cb723320e83af9ca017b  file2.txt
```
![image](https://github.com/user-attachments/assets/04a4939f-31e8-43fe-a4ed-754608d16cba)


### Task 2. Compare hashes
In this task, you’ll write the hashes to two separate files and then compare them to find the difference.

1. Use the `sha256sum` command to generate the hash of the `file1.txt` file, and send the output to a new file called `file1hash`:
```
sha256sum file1.txt >> file1hash
```
You now need to complete the same step for the `file2.txt` file.

2. Use the `sha256sum` command to generate the hash of the `file2.txt` file, and send the output to a new file called `file2hash`:
```
sha256sum file2.txt >> file2hash
```

Now, you should have two hashes written to separate files. The first hash was written to the `file1hash` file, and the second hash was written to the `file2hash` file.

You can manually display and compare the differences.

3. Use the `cat` command to display the hash values in the `file1hash` and `file2hash` files.

Inspect the output and note the difference in the hash values.

![image](https://github.com/user-attachments/assets/d2686065-f867-4fa9-b1cb-b954daae833e)


Now, you can use the `cmp` command to compare the two files byte by byte. If a difference is found, the command reports the byte and line number where the first difference is found.

4. Use the `cmp` command to highlight the differences in the `file1hash` and `file2hash` files:
```
cmp file1hash file2hash
```

Review the output, which reports the first difference between the two files:
```
analyst@4fb6d613b6b0:-$ cmp file1hash file2hash
file1hash file2hash differ: char1, line 1
```

![image](https://github.com/user-attachments/assets/04344a3c-a2e1-4186-8c4d-29050bfe35c7)


### Conclusion

You practiced how to

- compute hashes using `sha256sum`,
- display hashes using the `cat` command, and
- compare hashes using the `cmp` command.
These are valuable tools you can use to validate data integrity as you contribute to the control of your organization’s security.

