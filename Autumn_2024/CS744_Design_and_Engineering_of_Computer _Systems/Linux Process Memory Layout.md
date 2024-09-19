
Reference : [Linux process address space layout](https://www.kernel.org/doc/Documentation/x86/x86_64/mm.txt)

- Process's Virtual Memory == User Space Virt Mem $\bigcup$ Kernel Space Virt Mem.  
- Kernel is shared among the processes and is at higher addresses.

The schematics below are from Higher to lower address i.e. top ==  high, low == bottom (using this convention to validate "*stack grows downwards*")

```plaintext
========================================================================================================================
    Start addr    |   Offset   |     End addr     |  Size   | VM area description
========================================================================================================================
Kernel-space virtual memory, shared between all processes:
________________________________________________________________________________________________________________________
 ffffffffffe00000 |   -2    MB | ffffffffffffffff |    2 MB | ... unused hole
 ffffffffff600000 |  -10    MB | ffffffffff600fff |    4 kB | legacy vsyscall ABI
    FIXADDR_START | ~-11    MB | ffffffffff5fffff | ~0.5 MB | kernel-internal fixmap range, variable size and offset
 ffffffffff000000 |  -16    MB |                  |         |
 ffffffffa0000000 |-1536    MB | fffffffffeffffff | 1520 MB | module mapping space
 ffffffff80000000 |-2048    MB |                  |         |
 ffffffff00000000 |   -4    GB | ffffffff7fffffff |    2 GB | ... unused hole
 ffffffef00000000 |  -68    GB | fffffffeffffffff |   64 GB | EFI region mapping space
 ffffff8000000000 | -512    GB | ffffffeeffffffff |  444 GB | ... unused hole
 ffffff0000000000 |   -1    TB | ffffff7fffffffff |  0.5 TB | %esp fixup stacks
 fffffe8000000000 |   -1.5  TB | fffffeffffffffff |  0.5 TB | ... unused hole
 fffffe0000000000 |   -2    TB | fffffe7fffffffff |  0.5 TB | cpu_entry_area mapping
 fffffc0000000000 |   -4    TB | fffffdffffffffff |    2 TB | ... unused hole
 ffffec0000000000 |  -20    TB | fffffbffffffffff |   16 TB | KASAN shadow memory
 ffffeb0000000000 |  -21    TB | ffffebffffffffff |    1 TB | ... unused hole
 ffffea0000000000 |  -22    TB | ffffeaffffffffff |    1 TB | virtual memory map (vmemmap_base)
 ffffe90000000000 |  -23    TB | ffffe9ffffffffff |    1 TB | ... unused hole
 ffffc90000000000 |  -55    TB | ffffe8ffffffffff |   32 TB | vmalloc/ioremap space (vmalloc_base)
 ffffc88000000000 |  -55.5  TB | ffffc87fffffffff |   64 TB | direct mapping of all physical memory (page_offset_base)
 ffff888000000000 | -119.5  TB | ffffc87fffffffff |   64 TB | direct mapping of all physical memory (page_offset_base)
 ffff880000000000 | -120    TB | ffff887fffffffff |  0.5 TB | LDT remap for PTI
 ffff800000000000 | -128    TB | ffff87ffffffffff |    8 TB | ... guard hole, also reserved for hypervisor
__________________|____________|__________________|_________|___________________________________________________________

________________________________________________________________________________________________________________________
                  |            |                  |         |
 0000800000000000 | +128    TB | ffff7fffffffffff | ~16M TB | ... huge, almost 64 bits wide hole of non-canonical
                  |            |                  |         |     virtual memory addresses up to the -128 TB
                  |            |                  |         |     starting offset of kernel mappings.
__________________|____________|__________________|_________|___________________________________________________________

________________________________________________________________________________________________________________________
                  |            |                  |         |
 0000000000000000 |    0       | 00007fffffffffff |  128 TB | user-space virtual memory, different per mm
__________________|____________|__________________|_________|___________________________________________________________

```

- User-Space Virtual Memory is at lower addresses - the `text`, `data`, and `bss` are loaded from `ELF` during `exec` sys call by the OS. 
```plaintext
			  Higher Mem┌──────────────────┐                       
						│   argv, environ  │                       
						├──────────────────┤                       
						│                  │                       
						│      STACK       │                       
						│                  │                       
						│                  │                       
				  esp──►└────────┬─────────┘                       
								 │(grows downwards)                
								 ▼                                 
																   
							 UNALLOCATED                           
																   
								 ▲                                 
								 │(grows upwards)                  
						┌────────┴─────────┐                       
						│                  │                       
						│      HEAP        │                       
						│                  │                       
						│                  │                       
						┼──────────────────┼                       
						│      .bss        │(Uninitialized data)   
						┼──────────────────┼                       
						│      .data       │(Initialized data)     
						┼──────────────────┼                       
						│      .text       │(Program Code)         
			  Lower Mem └──────────────────┘                       
```



