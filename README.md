The quantum circuit is constructed using qiskit and compares any two given integers (positive or negative).
The logic of the quantum circuit is as follows: <br>
QUBIT_SIZE = 3 <br>
This logic uses the classical states and works for any numbers in the range [-2^(QUBIT_SIZE-1), 2^(QUBIT_SIZE-1)-1]. <br>
Consider two integers (positive or negative) num1 and num2. <br>
To illustrate with an example, say num1 = 3 and num2 = -2. <br>
2’s complement of 3 in 3-bit representation is 011. It is stored in int1 quantum register. <br>
2’s complement of -2 in 3-bit representation is 110. It is stored in int2 quantum register. <br>
1. Flip the most significant bit (i.e. sign bit) of both integers. <br>
int1 = |111> <br>
int2 = |010> <br>
2. Copy the int2 bits in int2_copy quantum register. <br>
int2_copy = |010> <br>
3. Find the position of the first differing bit in int1 and int2, say k. Set only the bit in that position to 1 and rest bits are set to 0. Store it in diff1bit quantum register. 
diff1bit = |100> <br>
If all bits are same, then diff1bit = |000> <br>
4. Perform bitwise AND of diff1bit and int1 bits, and store it in int1_AND_diff1bit register. <br>
int1_AND_diff1bit = |111> bitwise AND |100> = |100> <br>
5. Perform bitwise AND of diff1bit and int2_copy bits, and store it in int2_AND_diff1bit register. <br>
int2_AND_diff1bit = |010> bitwise AND |100> = |000> <br>
Notice that int1_AND_diff1bit in kth position will have the kth bit value, say b_1, of int1 and 0 in the other positions. Similarly, int2_AND_diff1bit in kth position will have the kth bit value, say b_2, of int2_copy and 0 in the other positions. Since, b_1 and b_2 are unequal, one of them is 1 and the other is 0. If b_1 is 1, then num1 is larger and if b_2 is 1, then num_2 is larger. If two numbers are equal, then b_1 = b_2 = 0. <br>
6. Compute OR of the bits of int1_AND_diff1bit and store it in OR_int1bits register. Similarly, compute OR of the bits of int2_AND_diff1bit and store it in OR_int2bits register. <br>
OR_int1bits = 1 <br>
OR_int2bits = 0 <br>
7. Measure OR_int1bits and store the classical value in meas_OR_int1bits classical register and measure OR_int1bits and store the classical value in meas_OR_int2bits classical register. <br>
meas_OR_int1bits = 1 <br>
meas_OR_int2bits = 0 <br>
8. Since qiskit is little-endian, if the measured value is ‘1 0’, then it means that OR_int2bits = 1 and OR_int1bits = 0. So, it means num1 is higher. <br>
If the measured value is ‘0 1’, then it means that OR_int1bits = 1 and OR_int2bits = 0 and hence, num2 is higher. <br>
If the measured value is ‘0 0’, then it means that both numbers are equal. <br>
Therefore, for our case, num1 (i.e. 3) is higher. <br>







