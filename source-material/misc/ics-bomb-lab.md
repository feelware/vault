## Phase 2

```c
void read_six_numbers(long rdi, long rsi) {
	rsp -= 24;

    rdx = rsi;
    rcx = rsi + 4;
    
    rax = rsi + 20;
    *(rsp + 8) = rax;
    
    rax = rsi + 16;
    *rsp = rax;
    
    r9 = rsi + 12;
    r8 = rsi + 8;
    
    rsi = 0x4025c3;  // %d %d %d %d %d %d
    rax = 0;

    rax = sscanf(
	    rdi,  // points to user input
	    rsi,  // "%d %d %d %d %d %d"
	    rdx,  // caller %rsp
	    rcx,  // caller %rsp + 4
	    r8,   // caller %rsp + 8
	    r9    // caller %rsp + 12
	    // caller %rsp + 16
	    // caller %rsp + 20
	);  // returns total items read
    
    if (rax <= 5)
		explode_bomb();
	    return;
    
    rsp += 24;
}
```

> [!todo]
> understand order criteria for function arguments stored in caller stack frame (`rsi+16` then `rsi+20`, or viceversa?)

| nº  | offset | offset (hex) |
| --- | ------ | ------------ |
| 1   | 0      | 0            |
| 2   | 4      | 4            |
| 3   | 8      | 8            |
| 4   | 12     | c            |
| 5   | 16     | 10           |
| 6   | 20     | 14           |

```c
void phase_2(char *rdi) {
	rsp -= 40;
	
	rsi = rsp;
	read_six_numbers(
		rdi,  // points to user input
		rsi   // top of current stack frame
	);
	
	if (*rsp != 1) {    // *rsp = first number introduced
		explode_bomb();
		return;
	}
	// else jump to +52

	rbx = rsp + 4;   // -> 2nd digit
	rbp = rsp + 24;  // -> after last digit 
	// jump (inconditionally) to +27

L27:
	rax = *(rbx - 4);
	rax *= 2;
	if (*rbx != rax) {
		explode_bomb();
		return;
	}
		// else jump to +41
	rbx += 4;
	if (rbx != rbp) {
		goto L27;
	}
	// else exit
	
	rsp += 40;
}
```

```c
int x[6] = {1, 2, 4, 8, 16, 32};

int *rbx = x + 1; // index pointer (init val: 2)
int *rbp = x + 6; // pointer to end (val: ?)

do {
	int cur = *rbx;
	int prev_double = (*(rbx - 1)) * 2;

	if (cur != prev_double) {
	   printf("%d != 2*%d\n", cur, *(rbx - 1));
	   return 1;
	}

	rbx += 1;
} while (rbx != rbp);

printf("all good!\n");
return 0;
```

> [!note] findings
> - input is 6 numbers
> - first number must be 1
> - each number should be twice the previous

## Phase 3

### Stack frame

```
+24 (prev %rsp)          
---
+20
+16
+12 (%rcx, 2nd)
+8  (%rdx, 1st)
+4
+0  (%rsp)
```

### Code

```c
void phase_3(char* rdi) {
	rsp -= 24;
	
	rcx = rsp + 12;
	rdx = rsp + 8;
	
	rsi = 0x4025cf; // 
	rax = 0;
	
	rax = sscanf(
		rdi,  // user input
		rsi,  // format: %d %d
		rdx,  // 1st
		rcx   // 2nd
	);
	
	if (rax <= 1) {     // if input has less than 2 numbers
		explode_bomb();
		return;
	}
	// else goto +39
39:
	// if ((*(rsp + 8) > 7) && (*(rsp + 8) < 0)) {
	//     explode_bomb(); // goto +106
	//     return;
	// }
	// 
	// since 1st is used as index of jump table
	// this check is made to avoid
	// the index being out of bounds (0-7 range)
	// 
	// this check seems to be the
	// the way the compiler implements
	// the switch's "default" case

	rax = *(rsp + 8) // 1st
	switch (rax) {
		case 0:
			rax = *(rsp + 8) // 1st
			break;
		case 1:
			rax = 0x137;
			break;
		case 2:
			rax = 0x2c3;
			break;
		case 3:
			rax = 0x100;
			break;
		case 4:
			rax = 0x185;
			break;
		case 5:
			rax = 0xce;
			break;
		case 6:
			rax = 0x2aa;
			break;
		case 7:
			rax = 0x147;
			break;
		default:
			explode_bomb(); // goto +106
			return;
	}
	
	if (rax != *(rsp + 12)) {  // if rax != 2nd
		explode_bomb();
		return;
	}
	
	rsp += 24;
}
```

> [!note]
> `jmp *0x402470(,%rax,8)`
> - this instruction looks up a **jump table** located at `0x402470`
> - this table is composed of 8 consecutive addresses (each one 8 bytes long)
> - these addresses point to different sections of `phase_3`
> ```
> position  row content         phase_3
> in table  (jump target)       location
> --------  ------------------  --------
> 0x402470  0x0000000000400f7c  +57
> 0x402478  0x0000000000400fb9  +118
> 0x402480  0x0000000000400f83  +64
> 0x402488  0x0000000000400f8a  +71
> 0x402490  0x0000000000400f91  +78
> 0x402498  0x0000000000400f98  +85
> 0x4024a0  0x0000000000400f9f  +92
> 0x4024a8  0x0000000000400fa6  +99
> ```
> - the instruction uses `%rax` to index the table, jumping to the address pointed by the selected row
> - `%rax` is scaled by 8 precisely because each row is 8-bytes long
> - example: if `%rax` is 3, the instruction will cause a jump to `+71`: `mov $0x100,%eax`
