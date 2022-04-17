# Wallbox

# Problem

A function that given a path of the file system finds the first file that meets the
following requirements
a. The file owner is admin
b. The file is executable
c. The file has a size lower than 14*2^20


# Approach

Open a Directory and iterate through all files.
    File path must be generic because when the test runs on different OS it shouldnt fail because of the absolute path (in windows double backslash and Linux   forward slash)

Without opening the file check the size of the file is 14 MB below (AND) check whether the file owner has admin permission as well the file is executable.
    Used Stat() function, which return information about a file, in the buffer pointed to by statbuf.  No permissions are required on the file
itself, but—in the case of stat(), fstatat(), and lstat()—execute (search) permission is required on all of the directories in pathname that lead to the file.

Iterate through each file and check whether it size is below 14 MB, if yes then
then check for admin permission and the file is executable (rwx --x --x). To achieve this use ST_MODE flag which will return the file permission in octal.
Take the last 3 octet as thats what we need it to compare with our given condition, hence mask all the other octet.
Now, compare the masked ST_MODE with the already predefined permission and see if it's a match, if yes then
toggle the found flag
print the filename and break the loop as we need only the firstFilename that matches our condition.


