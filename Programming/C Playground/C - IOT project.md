Here is the complete C code designed to teach you how memory works. I have broken it down line-by-line below.

### The Code: `struct_to_bytes.c`


```C
#include <stdio.h>
#include <stdint.h> // Essential for IoT: Gives us uint32_t, uint8_t, etc.

// 1. Define the Blueprint
typedef struct {
    uint32_t device_id;  // 4 bytes
    float temperature;   // 4 bytes
    uint32_t uptime;     // 4 bytes
} SensorPacket;          // Total = 12 bytes

int main() {
    // 2. Create an instance and fill it with data
    SensorPacket packet;
    packet.device_id = 0xAABBCCDD; // A distinct pattern to see in Hex
    packet.temperature = 25.5;
    packet.uptime = 100;

    // 3. Create a pointer that views memory as raw bytes
    // We take the address of 'packet' (&packet) and cast it to a uint8_t pointer
    uint8_t *byte_ptr = (uint8_t *)&packet;

    printf("Original Data:\n");
    printf("Device ID: %X\n", packet.device_id);
    printf("Temp: %f\n", packet.temperature);
    printf("\nRaw Memory Dump (Hex):\n");

    // 4. Iterate through the memory, byte by byte
    for (int i = 0; i < sizeof(SensorPacket); i++) {
        // Access the byte at (start_address + i)
        printf("%02X ", byte_ptr[i]);
    }
    printf("\n");

    return 0;
}
```

---

### The Breakdown

#### 1. The Headers

C

```
#include <stdint.h>
```

- **Why:** In standard C, an `int` might be 2 bytes on an Arduino but 4 bytes on a Raspberry Pi. This chaos breaks IoT communication.
    
- **The Fix:** `<stdint.h>` gives us **Fixed Width Integers**. `uint32_t` is guaranteed to be **Unsigned** (no negatives), **Integer**, **32-bits** (4 bytes) wide everywhere.
    

#### 2. The Struct Definition

C

```
typedef struct { ... } SensorPacket;
```

- **Struct:** This tells the compiler to group these variables together in a single contiguous block of memory.
    
- **Typedef:** This saves time. Without `typedef`, you would have to write `struct SensorPacket myVar;` every time. With it, you just write `SensorPacket myVar;`.
    

#### 3. The Magic Cast (The Hardest Part)

C

```
uint8_t *byte_ptr = (uint8_t *)&packet;
```

This single line is the essence of C.

- `&packet`: "Give me the memory address where the `packet` struct starts." (Let's say it's address `100`).
    
- `(uint8_t *)`: "Treat this address as if it points to **1-byte chunks** (integers 0-255), not a big 12-byte struct."
    
- **The Result:** `byte_ptr` now points to address `100`.
    
    - `byte_ptr[0]` looks at address `100`.
        
    - `byte_ptr[1]` looks at address `101`.
        
    - `byte_ptr[2]` looks at address `102`.
        
    - You can now walk through the struct one byte at a time, oblivious to the fact that it holds floats or ints.
        

#### 4. The Loop & Print

C

```
printf("%02X ", byte_ptr[i]);
```

- `%X`: Print the number in Hexadecimal (Base 16).
    
- `02`: Force it to print 2 digits (e.g., print `0A` instead of just `A`). This makes the output align neatly like a memory dump.
    

### How to Run This (On your Pi or Mac)

1. Save the file as `struct_to_bytes.c`.
    
2. Open your terminal.
    
3. Compile it: `gcc struct_to_bytes.c -o struct_test`
    
4. Run it: `./struct_test`
    

What to look for in the output:

You set device_id to 0xAABBCCDD.

When you print the raw bytes, do you see AA BB CC DD in that order? Or do you see DD CC BB AA?

- If you see `DD CC BB AA`, your machine is **Little Endian** (it stores the "little" end of the number first).
    
- If you see `AA BB CC DD`, your machine is **Big Endian**.
    

This is the first lesson in Computer Architecture: **How does the CPU actually write numbers to RAM?** Give it a try and tell me which order you see!