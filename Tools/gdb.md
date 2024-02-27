# GNU Debugger (GDB)

# Starting gdb
```
> gdb program_to_debug
(gdb) run
(gdb) run parameter_1 parameter_2
```
```
echo "set disassembly-flavor intel" > ~/.gdbinit
echo "# source gef.py" >> ~/.gdbinit
```
# Setting break point
```
Set breakpoint at main function
(gdb) break *main
Set breakpoint at given function
(gdb) break *function_name
Set breakpoint at given location
(gdb) break *0x0000555555400892
Set breakpoint at relative location
(gdb) break *function_name + 15
Show set breakpoints
(gdb) info break
Delete a breakpoint based on previous command
(gdb) delete break 1
```

# Inspecting registers
## Printing registers
```
(gdb) info regisers
(gdb) print $rip
```
## Examining registers
```
Examine instruction at given location
(gdb) x/i $rip
Examine 10 instrucions at givene location
(gdb) x/10i $rip
Examine 4 giant hex at given location
(gdb) x/4gx $rsp
Examine 4 signed numbers at given location
(gdb) x/4d $rsp
Examine 4 unsigned numbers at given location
(gdb) x/4u $rsp
Examine 4 addresses at given location
(gdb) x/4a $rsp
```
```
Example:

(gdb) x/i $rip
=> 0x555555400892 <main+4>:     sub    $0x40,%rsp
(gdb) x/10i $rip
=> 0x555555400892 <main+4>:     sub    $0x40,%rsp
   0x555555400896 <main+8>:     movl   $0x539,-0x4(%rbp)
   0x55555540089d <main+15>:    mov    $0x0,%eax
   0x5555554008a2 <main+20>:    call   0x55555540081a <setup>
   0x5555554008a7 <main+25>:    mov    $0x0,%eax
   0x5555554008ac <main+30>:    call   0x55555540087b <banner>
   0x5555554008b1 <main+35>:    lea    0x208(%rip),%rdi        # 0x555555400ac0
   0x5555554008b8 <main+42>:    call   0x5555554006b0 <puts@plt>
   0x5555554008bd <main+47>:    lea    0x2dc(%rip),%rdi        # 0x555555400ba0
   0x5555554008c4 <main+54>:    call   0x5555554006b0 <puts@plt>
(gdb) x/4gx $rsp
0x7fffffffde00: 0x0000000000000001      0x00007ffff7df26ca
0x7fffffffde10: 0x0000000000000000      0x000055555540088e
(gdb) x/4d $rsp
0x7fffffffde00: 1       140737351984842
0x7fffffffde10: 0       93824990840974
(gdb) x/4u $rsp
0x7fffffffde00: 1       140737351984842
0x7fffffffde10: 0       93824990840974
(gdb) x/4a $rsp
0x7fffffffde00: 0x1     0x7ffff7df26ca <__libc_start_call_main+122>
0x7fffffffde10: 0x0     0x55555540088e <main>
```

## Casting

```
Casting $rsp to a pointer to a long and dereferncing it
(gdb) p/a *(long *) $rsp
Printing saved output (as long hex) from previous command
(gdb) printf "%lx\n", $5
```
```
Example:

(gdb) x/gx $rsp
0x7fffffffddb8: 0x00005555554008a7
(gdb) x/a $rsp
0x7fffffffddb8: 0x5555554008a7 <main+25>
(gdb) x/gx $rsp
0x7fffffffddb8: 0x00005555554008a7
(gdb) p/a *(long *) $rsp
$5 = 0x5555554008a7 <main+25>
(gdb) printf "%lx\n", $5
5555554008a7
```

# Inspecting assembly code
```
(gdb) disassemble *main
(gdb) dissasemble *function_name
```

# Stepping through instructions
```
Display information after a step
(gdb) display/a $rip
(gdb) display/5i $rip
```
```
Step instruction (step into calls)
(gdb) si
Next instruction (step over calls)
(gdb) ni
Continue until breakpoint
(gdb) c
Skip instruction (step out of a call)
(gdb) finish
```
# Variables

## User defined variables
```
Create new variable and assign value to it
(gdb) set $variable_name = $rdi
Print new variable
(gdb) p $variable_name
```

## Modifying registers values
```
Modify given register value
(gdb) set *(long *) $rsp = 0xdead
Modify instruction pointer
(gdb) set $rip = *main + 21
```
```
Example:

(gdb) x/gx $rsp
0x7fffffffddb8: 0x00005555554008a7
(gdb) set *(long *) $rsp = 0xdead
(gdb) x/gx $rsp
0x7fffffffddb8: 0x000000000000dead
```

# Scripting
```
> gdb -x script_name.gdb program_to_debug
```

```
Example: At every breakpoint: be silent, show $rip and continue.

break *main
commands
    silent
    p/a $rip
    continue
end
run parameter_1 parameter_2
q
```

# GDB Enhanced Features (GEF)
## Setup for split screen debugging
```
mkfifo /tmp/challange
```

```
> gdb program_to_debug
(gdb) run > /tmp/challange
```

```
cat /tmp/challange
```