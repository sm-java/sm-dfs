#Tech Notes - Linux FUSE 

####Issues

There are several common problems that plague programmers new to Fuse. This is a partial list:

####1. Multithreading
  1. By default, Fuse is multithreaded. That's handy for production filesystems, because it lets client (or file access) A proceed even 
  if client B is hung up. But multithreading introduces the possibility of race conditions, and makes debugging harder. Always run with 
  the -s switch to avoid this problem. 
  
  2. getattr - Fuse calls getattr like crazy. Implement it first, or nothing will work.

####2. Truncate
Unless you're writing a read-only filesystem, you need to implement the truncate system call to make writes work correctly.

####3. Working directory
  1. When it starts, Fuse changes its working directory to "/". That will probably break any code that uses relative pathnames. To make 
  matters worse, the chdir is suppressed when you run with the -f switch, so your code might appear to work fine under the debugger. 
  To avoid the problem, either
   - (a) use absolute pathnames, or 
   - (b) record your current working directory by calling get_current_dir_name before you invoke fuse_main, and then convert 
      relative pathnames into corresponding absolute ones. 
      
   Obviously, (b) is the preferred approach.
      
  2. Printf - Your printf/fprintf debugging code will only work if you run with the -f switch. Otherwise, Fuse disconnects stdout and stderr.

####4. Unimplemented functions
It is very tempting to just leave functions undefined if your filesystem doesn't need them, or if you just haven't gotten around to 
writing them yet. Don't. If a function isn't listed in your fuse_operations struct, Fuse will silently generate a failure when it is 
called, and you'll never find out that you need to write it. Instead, write every unimplemented function as a stub that prints a 
message to stderr and returns an error code. When you see the message, you'll know what extra functions you need to write.


####Resources
1. [FUSE Docs](https://www.cs.hmc.edu/~geoff/classes/hmc.cs135.201109/homework/fuse/fuse_doc.html)
2. [FUSE Tutorial](http://engineering.facile.it/blog/eng/write-filesystem-fuse/)
3. [FUSE Tutorial - 2](https://www.cs.nmsu.edu/~pfeiffer/fuse-tutorial/)
4. [BindFS](http://bindfs.org/)
