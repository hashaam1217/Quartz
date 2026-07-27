# Review List
- Finite State Machine (Is there more to it?)
	- Switch Case Approach 
	- Table Driven Approach
- Grind Big Endian / Little Endian conversions for CAN
- Pointer Arithmetic problems
- Refresh yourself on XOR and other operations on bits
- Using Macros to set bits
- Counting Set bits 
	- Brian Kernighan's algorithm: `n &= (n-1)` clears lowest set bit
	- 1U
- **Circular buffer implementation.** Write a thread-safe ring buffer where ISR writes and main loop reads. Mark head/tail as `volatile`. Use power-of-2 buffer sizes with `& (SIZE-1)` instead of modulo. Handle the full-vs-empty ambiguity by sacrificing one slot.
- Struct Padding and Alignment
- Interpolation, different types of interpolation
- **Linked list reversal.** Write iterative in-place reversal of a singly linked list. [Interview Query](https://www.interviewquery.com/interview-guides/tesla-software-engineer) Also know Floyd's cycle detection algorithm. These are the most commonly asked data structure problems in embedded interviews.
- [[SOC Estimation]]
- Regulatory codes ([[ISO 26262]])

# Tesla Information
US 7,602,145 B2 (2009 US Patent on Cell balancing)


4 Different cell formats [Source](https://evseekers.com/tesla-battery-types/)   
- 18650 
- 4680 Transitioning to this currently Model Y / Cybertruck
- 2170 (Model 3/Y) Panasonic, higher energy density
- LFP prismatic (Standard Range Model 3/Y) (Lithium Iron Phosphate), also safer. Lower energy density and heavier. 

10 mV and 3 degree Celsius 


## Small Questions
Cheatsheet
```C
static
global
macros
1U
volatile
const
bytes of: 
char
int
#pragma packing
++p vs p++
`#define SECONDS_PER_YEAR (365UL * 24UL * 60UL * 60UL)` — unsigned long, no semicolon.




```