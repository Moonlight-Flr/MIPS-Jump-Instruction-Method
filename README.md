# MIPS-Jump-Instruction-Method

This repository describes an efficient method for manually calculating the 26 bits required for a jump instruction in MIPS assembler.

Let us consider a situation in which a jump (`j`) instruction targets a function located at memory address `0x040000A9`.

---

## Calculation Steps

1. **Convert to binary**  
   Example:  
   `0x040000A9 → 0000 0100 0000 0000 0000 0000 1010 1001`

2. **Perform a Shift Right Logical (`srl`) by 2 positions**  
   Example:  
   `0000 0100 0000 0000 0000 0000 1010 1001 → 0000 0001 0000 0000 0000 0000 0010 1010`

3. **Remove the 6 most significant bits**  
   Example:  
   `0000 0001 0000 0000 0000 0000 0010 1010 → 01 0000 0000 0000 0000 0010 1010`

4. **Convert back to hexadecimal**  
   Example:  
   `01 0000 0000 0000 0000 0010 1010 → 0x100002A`

---

## Additional Notes:
- This method applies to addresses within the **same 256 MB block**.
- Addresses must also be **word-aligned** (multiples of 4 bytes).

---

## Example Ranges for 256 MB Memory Blocks

In MIPS, memory is divided into blocks of 256 MB. Below are some examples of how these blocks are defined in hexadecimal.

### Memory Block Ranges:
1. **Block `0x0`:**  
   Range: `0x00000000` to `0x0FFFFFFF`.

2. **Block `0x1` (e.g., `0x100002AC`):**  
   Range: `0x10000000` to `0x1FFFFFFF`.

3. **Block `0x4` (e.g., `0x040000A9`):**  
   Range: `0x04000000` to `0x04FFFFFF`.

4. **Block `0x14` (e.g., `0x140004F8`):**  
   Range: `0x14000000` to `0x14FFFFFF`.

5. **Block `0x49` (e.g., `0x04920FA0`):**  
   Range: `0x04900000` to `0x049FFFFF`.

---

## Understanding the Most Significant Bits in MIPS Memory Blocks

This section explains the concept of most significant bits (MSB) in MIPS memory blocks, particularly in the context of hexadecimal addresses and their corresponding binary representations. 

### Key Concept: Most Significant Bits
When working with memory blocks in MIPS, the **first hexadecimal digit** (or **4 bits**) from the left serves as the reference to identify the memory block. This concept can initially be confusing because the representation of most significant bits depends on the context.

### Contexts Explained:
1. **For Complete 32-bit Addresses**:  
   The first hexadecimal digit (or 4 bits) in a complete 32-bit address determines the most significant bits. This is the point of reference for identifying 256 MB memory blocks.  
   **Example:**  
   - Address: `0x04000000`  
   - Binary Representation: `0000 0100 0000 0000 0000 0000 0000 0000`  
   - **Most Significant Bits:** `0100`  
   - Corresponding Block: `0x04` (Range: `0x04000000` to `0x04FFFFFF`)

2. **For Individual Hexadecimal Values**:  
   When considering a standalone hexadecimal value (e.g., `0x05`), the entire value is represented using 8 bits. Here, the most significant bits are determined by the leftmost 4 bits of the binary representation.  
   **Example:**  
   - Hexadecimal Value: `0x05`  
   - Binary Representation: `0000 0101`  
   - **Most Significant Bits:** `0000`  
   - However, in memory context, the reference digit is `0x5` (ignoring the leading zero).  

---

## Detailed Examples of Block Ranges:
1. **Address `0x05000058`:**
   - Binary Representation: `0000 0101 0000 0000 0000 0000 0101 1000`
   - **Most Significant Bits:** The reference digit is `0x5` (corresponds to `0101` in binary).
   - Block Range: `0x05000000` to `0x05FFFFFF`

2. **Address `0x12000125`:**
   - Binary Representation: `0001 0010 0000 0000 0000 0000 0001 0010 0101`
   - **Most Significant Bits:** The reference digit is `0x12` (corresponds to `0001 0010` in binary).
   - Block Range: `0x12000000` to `0x12FFFFFF`

3. **Address `0x58900000`:**
   - Binary Representation: `0101 1001 1000 0000 0000 0000 0000 0000`
   - **Most Significant Bits:** The reference digit is `0x58` (corresponds to `0101 1001` in binary).
   - Block Range: `0x58000000` to `0x58FFFFFF`

---

## Conclusion
In MIPS, the **most significant bits (MSB)** refer to the **leftmost 4 bits** of a 32-bit address or the **reference hexadecimal digit** from the entire address. This is crucial for identifying memory blocks of 256 MB, as the block is strictly determined by the **first hexadecimal digit** (ignoring leading zeros).




