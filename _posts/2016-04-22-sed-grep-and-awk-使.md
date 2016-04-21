##0.RE & wildcard

##1.sed(stream editor)

	sed [-nefri] '[n1[,n2]] [aicdps] [str]'
* n:silent  
* e:more than one command
* f:
* r:extended reguler expression
* i:write the file
***
**[n1[,n2]]**:command adress 
	1. n1,n2 & n($ is the last line)
	2. /regular expression/
	
***
* **a/i +str**: append in the end/insert at the start
* **c +str**: replace
* **s/str_old/str_new/g**: replace(RE available)
* **d**: delete
* **p**: print

##2.grep(global regular expression print)

	grep [-acinv] [-An] [-Bn] 'str' file
* a:binary
* c:count
* i:ignore case
* n:row number
* v:reverse
***
* **str**:RE avaliable

##3.awk

	awk 'option1{command1}option2{command2}'

####3.1 Built-in
* **NF**
* **NR**
* **FS**:seperator
* **$0 $1 $2...**(what's the difference in shell?)

####3.2 BEGIN and END
* **BEGIN**:do before read the file
* **END**:do after read the file

####3.3 command

* print(change line) and printf(don't change line)
* `for while if` in c
* no $ in variables

####3.4 communication with shell