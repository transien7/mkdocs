# Reverse Engineering Cheat Sheet
## Compilation Tools  
### GCC (GNU Compiler Collection)  

#### Compile source code  
`gcc <source_code_file> -o <executable_name> -fno-stack-protector -w`  
`gcc -g -z execstack -fno-stack-protector <source_code_file> -o abp -w`  

## Static Analysis Tools  
### Radare2  

#### r2 syntax  
```
r2 -                                # Launch r2
	?vi 0x0000001                   # Decimal number from hex
	? 1                             # Number in various bases
	? 1 + 1 - 3 * 2                 # Same as above but with arithmetic
	d ./ <binary_file>              # Debug view
r2 ./<binary_file>                  # Reads an executable to memory
	V                               # Visual mode (hex of binary in memory)
	p                               # Change views
	f                               # List functions
	s <function>                    # Step into the specified function
	pdf                             # Print disassembled function
	:                               # Allows input
		aaa                         # Analyse the file
		afl                         # Analyse function list
		s <function>                # Step into the specified function
		e stack.size=<n>            # Sets stack display to n bytes
		dr rip = <0x[address]>      # Sets the instruction pointer to a memory address
	[F7]                            # Step into a function
	[F8]                            # Step over a function
```

### objdump  

#### Disassemble binary file  
`objdump -S --disassemble <binary_file> > <output_filename>.dump`  
#### View .dump output file  
`less <output_filename>.dump`  

### ltrace  

#### Dynamically analyse function calls for a binary file  
`ltrace ./<binary_file>`

### GDP (GNU Debugger)
#### Debug a binary file
`gdb ./abp`

#### GDP uses
```
info address <function>      # returns the memory address of the function
set $rip=<address>           # sets the instruction pointer to the memory address
continue                     # runs the program from the current instruction
```

### peres
Provides some useful information for portable executable (PE) files  

### pescan
Provides some useful information for portable executable (PE) files  

### pestr
Dumps strings from a portable executable (PE) file. Useful for creating YARA rules
```
sudo apt install -y pev
pestr <path_to_binary_file>
```

### Detect-it-Easy
A GUI that loads binary files, returning interesting information such as whether the binary has been packed

### upx
Can be used to unpack binaries that have been packed using UPX


## Turn off Address Space Layout Randomisation (ASLR)  

This is particularly useful for reverse engineering as it will ensure instructions are assigned to the same memory addresses each time you run a program  
```
sudo su                                           # go root
echo 0 > /proc/sys/kernel/randomize_va_space      # disable ASLR in current session
```


## Creating YARA rules
  
1. Create the file `rules.yara`
```
touch rules.yara
```
  
2. Edit the file
```
vim rules.yara
```
  
3. Enter rules (the below template could be used to search a binary for 1 of 2 strings)
``` YARA
rule signature_name {
	meta:
		description = ""
		md5 = ""
		sha1 = ""
		filename = ""
		author = ""
	
	strings:
		$stringa = ""
		$stringb = ""

	condition:
		($stringa or $stringb)
}
```
  
4. Compare the binary file to the YARA rules
```
yara -s rules.yara <binary_file>
```