# BASH SHELL SCRIPTING

Check MD5 checksum recursesively down directory tree.  This command might take a long time, so you may want to wrap it with `nohup` and `&`
```sh

# recursively look inside /parent-dir/dir1

find dir1 -type f -name "*.md5"  | xargs -I {} sh -c 'date; echo {}; cd `dirname {}`; md5sum -c `basename {}`; cd /parent-dir; echo' > results.txt 

```
