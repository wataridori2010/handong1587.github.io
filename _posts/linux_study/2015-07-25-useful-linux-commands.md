---
layout: post
category: linux_study
title: Useful Linux Commands
date: 2015-07-25
---

# Pack/Unpack/Compress/Uncompress

|file type    |  Pack/Compress                      | Unpack/Uncompress           |
|:-----------:|:-----------------------------------:|:---------------------------:|
|.tar         |  tar cvf FileName.tar DirName       |  tar xvf FileName.tar       |
|.gz          |  gzip FileName                      |  gunzip FileName.gz         |
|.gz          |  gzip FileName                      |  gzip -d FileName.gz        |
|.tar.gz, .tgz|  tar zcvf FileName.tar.gz DirName   |  tar zxvf FileName.tar.gz   |
|.bz2         |  bzip2 -z FileName                  |  bzip2 -d FileName.bz2      |
|.bz2         |                                     |  bunzip2 FileName.bz2       |
|.tar.bz2     |  tar jcvf FileName.tar.bz2 DirName  |  tar jxvf FileName.tar.bz2  |
|.bz          |                                     |  bzip2 -d FileName.bz       |
|.bz          |                                     |  bunzip2 FileName.bz        |
|.tar.bz      |                                     |  tar jxvf FileName.tar.bz   |
|.Z           |  compress FileName                  |  uncompress FileName.Z      |
|.tar.Z       |  tar Zcvf FileName.tar.Z DirName    |  tar Zxvf FileName.tar.Z    |
|.zip         |  zip FileName.zip DirName           |  unzip FileName.zip         |
|.rar         |  rar a FileName.rar DirName         |  rar x FileName.rar         |
|.lha         |  lha -a FileName.lha FileName       |  lha -e FileName.lha        |
|.rpm         |                                     |  rpm2cpio FileName.rpm \| cpio -div |
|.deb         |                                     |  ar x example.deb           |
|.deb         |                                     |  ar p FileName.deb data.tar.gz \| tar zx |
|.deb         |                                     |  dpkg -x somepackage.deb ~/temp/ |
|.xz          |                                     |  xz -d linux-3.12.tar.xz    |
|.xz          |                                     |  tar -xf linux-3.12.tar     |
|.xz          |                                     |  tar -Jxf linux-3.12.tar.xz |

For compress/uncompress those files:

.tar .tgz .tar.gz .tar.Z .tar.bz .tar.bz2 .zip .cpio .rpm .deb .slp .arj .rar .ace .lha .lzh .lzx .lzs .arc .sda .sfx .lnx .zoo .cab .kar .cpt .pit .sit .sea

```
compress:   sEx a FileName.* FileName
uncompress: sEx x FileName.*
```

# Print info

| task                         | command               |
|:----------------------------:|:---------------------:|
| Print system info            | cat /proc/version     |
| Print software info          | whereis SOFEWARE      |
|                              | which SOFEWARE        |
|                              | locate SOFEWARE       |
| Print CPU info               | cat /proc/cpuinfo     |
|                              | dmesg \| grep -i xeon |
| Print memory info            | cat /proc/meminfo     |
|                              | free -m               |
| Print graphics card version  | nvcc --version        |
| Print graphics card GPU info | nvidia-smi            |
| Print disk free space        | df -h                 |
|                              | df -hl                |
| Print current folder size    | du -sh DIRNAME        |
| Print target folder volume (in MB) | du -sm          |

# Download

Download file:

```
wget "http://domain.com/directory/4?action=AttachFile&do=view&target=file.tgz"
```

Download file to specific directory:

```
wget -O /home/omio/Desktop/ "http://thecanadiantestbox.x10.mx/CC.zip"
```

Download all files from a folder on a website or FTP:

```
wget -r --no-parent --reject "index.html*" http://vision.cs.utexas.edu/voc/
```

# Transfer Files

Remote transfer files, remote -> local:

```
scp account@111.111.111.111:/path/to/remote/file /path/to/local/
```

Remote transfer files, local -> remote:

```
scp /path/to/local/file account@111.111.111.111:/path/to/remote/
```

Print directory structure:

```
ls -l -R
```

Print folder in current directory:

```
ls -lF |grep /
```

```
ls -l |grep '^d'
```


Print history command:

```
history
```

```
history | less
```

# Rename

Perl-based rename commands (-n: test commands; -v: print renamed files):

```
rename -n 's/\.htm$/\.html/' \*.htm
```

```
rename -v 's/\.htm$/\.html/' \*.htm
```

**1. Replace first letter of all files' name with 'q':**

```
for i in `ls`; do mv -f $i `echo $i | sed 's/^./q/'`; done
```

**same with a bash script:**

```
for file in `ls`
do
  newfile =`echo $i | sed 's/^./q/'`
　mv $file $newfile
done
```

**2. Replace first 5 letters with 'abcde'**

```
for i in `ls`; do mv -f $i `echo $i | sed 's/^...../abcde/'`;
```

**3. Replace last 5 letters with 'abcde'**

```
for i in `ls`; do mv -f $i `echo $i | sed 's/.....$/abcde/'`;
```

**4. Add 'abcde' to the front**

```
for i in `ls`; do mv -f $i `echo "abcde"$i`; done
```

**5. Convert all lower case to upper case**

```
for i in `ls`; do mv -f $i `echo $i | tr a-z A-Z`; done
```

# Count

Count lines in a document

```
wc -l /dir/file.txt
```

```
cat /dir/file.txt | wc -l
```

Filter and count only lines with pattern, or with -v to invert match

```
grep -w "pattern" -c file
```

```
grep -w "pattern" -c -v file
``` 

Count files in the current directory:

```
ls -l | grep “^-” | wc -l
```

example: counting all js files in directory "/home/account/" (recursively):

```
ls -lR /home/account | grep js | wc -l
```

```
ls -l "/home/account" | grep "js" | wc -l
```

Count files in the current directory, recursively:

```
ls -lR | grep “^-” | wc -l
```

Count folders in the current directory, recursively:

```
ls -lR | grep “^d” | wc -l
```

# Search

1. Search for a file by its file name. 
The command below will search for the query in the current directory and any subdirectories.
Using -iname instead of -name ignores the case of your query. The -name command is case-sensitive.

```
find -iname "filename"
```

## References

**How to Find a File in Linux**

[http://www.wikihow.com/Find-a-File-in-Linux](http://www.wikihow.com/Find-a-File-in-Linux)

**How to find files in Linux using 'find'**

[http://www.codecoffee.com/tipsforlinux/articles/21.html](http://www.codecoffee.com/tipsforlinux/articles/21.html)

**35 Practical Examples of Linux Find Command**

[http://www.tecmint.com/35-practical-examples-of-linux-find-command/](http://www.tecmint.com/35-practical-examples-of-linux-find-command/)

# GDB

**GDB reference card**

[https://web.stanford.edu/class/cs107/gdb_refcard.pdf](https://web.stanford.edu/class/cs107/gdb_refcard.pdf)

**GDB Tutorial: A Walkthrough with Examples**

- slides: [https://www.cs.umd.edu/~srhuang/teaching/cmsc212/gdb-tutorial-handout.pdf](https://www.cs.umd.edu/~srhuang/teaching/cmsc212/gdb-tutorial-handout.pdf)

**GNU GDB Debugger Command Cheat Sheet**

[http://www.yolinux.com/TUTORIALS/GDB-Commands.html](http://www.yolinux.com/TUTORIALS/GDB-Commands.html)

**Cheat Sheet**:

| shortcut   | command       | explanation      |
|:----------:|:-------------:|:----------------:|
| q          | quit          |                  |
| h          | help          |                  |
| h command  | help command  | print command meaning|
| b          | break         | example: b 5     |
| disable codenum|           |                  |
| enable codenum |           ||
| condition codenum xxx|     | set break condition|
| c          | continue      |                  |
| n          | next          |                  |
| s          | step          |                  |
| w          |               | print code in current execution point|
| j codenum  |               | jump to line j   |
| l          |               | list nearby code |
| p          |               | print var value  |
| a          |               | print current func/var value|
| Enter      |               | repeat last command|

```
gdb --arg python demo.py 2>&1 | tee demo.log
```

# PDB

```
import pdb
pdb.set_trace()
```

# Ctags

| command         | explanation                                       |
|:---------------:|:-------------------------------------------------:|
| ctags –R *      | Generate tags files in source code root directory |
| vim -t func/var | find func/var definition                          |
| :ts             | give a list if func/var has multiple definitions  |
| Ctrl+]          | jump to definition                                |
| Ctrl+T          | jump back                                         |

# Screen

| task                        | command                       |
|:---------------------------:|:-----------------------------:|
| Run program in screen mode  | screen python demo.py --gpu 1 |
| Detach screen               | Ctrl + a, c                   |
| Re-connect screen           | screen -r pid                 |
| Display all screens         | screen -ls                    |
| Delete screen               | kill pid                      |
| Naming a screen             | screen -S sessionName         |

# nohup

```
nohup command-with-options &
```

```
nohup xxx.sh 1 > log.txt 2>&1 &
```

**nohup - get the process ID to kill a nohup process**

```
nohup command-with-options & 
echo $! > save_pid.txt
kill -9 `cat save_pid.txt`
```

# Cscope

| task                              | command                         |
|:---------------------------------:|:-------------------------------:|
| Generate Cscope database          | find . -name "*.c" -o -name "*.cc" -o -name "*.cpp" -o -name "*.cu" -o -name "*.h" -o -name "*.hpp" -o -name "*.py" -o -name "*.proto" > cscope.files |
| Build a Cscope reference database | cscope -q -R -b -i cscope.files |
| Start the Cscope browser          | cscope -d                       |
| Exit a Cscope browser             | Ctrl + d                        |

**Cheat Sheet**

```
-b  Build the cross-reference only.
-C  Ignore letter case when searching.
-c  Use only ASCII characters in the cross-ref file (don’t compress).
-d  Do not update the cross-reference.
-e  Suppress the -e command prompt between files.
-F  symfile Read symbol reference lines from symfile.
-f  reffile Use reffile as cross-ref file name instead of cscope.out.
-h  This help screen.
-I  incdir Look in incdir for any #include files.
-i  namefile Browse through files listed in namefile, instead of cscope.files
-k  Kernel Mode – don’t use /usr/include for #include files.
-L  Do a single search with line-oriented output.
-l  Line-oriented interface.
-num  pattern Go to input field num (counting from 0) and find pattern.
-P  path Prepend path to relative file names in pre-built cross-ref file.
-p  n Display the last n file path components.
-q  Build an inverted index for quick symbol searching.
-R  Recurse directories for files.
-s  dir Look in dir for additional source files.
-T  Use only the first eight characters to match against C symbols.
-U  Check file time stamps.
-u  Unconditionally build the cross-reference file.
-v  Be more verbose in line mode.
-V  Print the version number.
```

# Vim

**Shifting blocks visually**

[http://vim.wikia.com/wiki/Shifting_blocks_visually](http://vim.wikia.com/wiki/Shifting_blocks_visually)

| mode        | task                      | command   |
|:-----------:|:-------------------------:|:-------- :|
| normal mode | indent the current line   | type >>   |
| normal mode | unindent the current line | type <<   |
| insert mode | indent the current line   | Ctrl-T    |
| insert mode | unindent the current line | Ctrl-D    |

For all commands, pressing **.** repeats the operation.

For example, typing **5>>..** shifts five lines to the right, and then repeats
the operation twice so that the five lines are shifted three times.

Insert current file name:

```
:r! echo %
```

# Matlab

Comment multi-lines in Matlab: Ctrl+R, Ctrl+T

Launch Matlab:

```
cd /usr/local/bin/
sudo ln -s /usr/local/MATLAB/R2012a/bin/matlab Matlab
gedit ~/.bashrc
alias matlab="/usr/local/MATLAB/R2012a/bin/matlab"
```

Start MATLAB Without Desktop:

```
matlab -nojvm -nodisplay -nosplash
```

Matlab + nohup:

runGenerareSSProposals.sh:

```
#!/bin/sh
cd /path/to/detection-proposals
matlab -nojvm -nodisplay -nosplash -r "startup; callRunCOCO; exit"
```

runNohup.sh:

```
time=`date +%Y%m%d_%H%M%S`
cd /path/to/detection-proposals
nohup ./runGenerareSSProposals.sh > runGenerareSSProposals_${time}.log 2>&1 &
echo $! > save_runGenerareSSProposals_val_pid.txt
```

# Others

Launch terminal in Ubuntu: Ctrl+Alt+T

Create symbol link:

```
ln -s EXISTING_FILE SYMLINK_FILE
ln -s /path/to/file /path/to/symlink
```

Open image:

```
eog /path/to/image/im.jpg
```

```
display /path/to/image/im.jpg
```

Convert text files with DOS or MAC line breaks to Unix line breaks

```
sudo dos2unix /path/to/file
sudo sed -i -e 's/\r$//' /path/to/file
```

Create new file list:

```
sed 's?^?'`pwd`'/detection_images/?; s?$?.jpg?' trainval.txt > voc.2007trainval.list
```