#unix #bash_history #unix_programming
2024-08-07 21:12

# What is Unix ?
*Time sharing OS Kernel* 

Lets users
1. run their programs,
2. controls the peripheral devices
3. provides file system for data storage.

---
## Control Sequences :

`RETURN` key is used to signify end of input and the system shall interpret the command line, as a response, the `RETURN` is echoed by *moving the cursor to start of new line* by system.


It is like a special control character, other control characters need to be typed by pressing `CNTROL` key, 

```
RETURN == CTRL + m
```

Common control characters :

| Control + char | Control Sequence                                                |
| -------------- | --------------------------------------------------------------- |
| $d$            | tells the program that there is no more input                   |
| $g$            | to ring a bell on terminal                                      |
| $h$            | backspace                                                       |
| $i$            | tab - advances the cursor to next tab stop*                     |
| $c$            | stops a program immediately, without waiting for it to finish** |
More control sequences at *[console_codes(4) Linux Manual page](https://man7.org/linux/man-pages/man4/console_codes.4.html)*

\*tab stops are 8-spaces apart in on UNIX

\*\*`DELETE` and `BREAK` used to serve the same purpose.

---
**NOTE :**  *A lot of shit mentioned such as `backspce using <- or #` doesn't work in `zsh`, so take the text with a grain of salt, it was written where there were dial-up connections required*.

---
