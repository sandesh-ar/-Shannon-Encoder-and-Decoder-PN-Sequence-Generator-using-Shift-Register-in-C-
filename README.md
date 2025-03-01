# 🔄 Shannon Encoder and Decoder & PN Sequence Generator using Shift Register in C  

## 📌 Overview  
This repository contains **C programs** for:  
1. **Shannon Encoder and Decoder:** Implements Shannon's entropy-based coding technique to efficiently compress and decompress messages.  
2. **PN (Pseudo-Noise) Sequence Generator:** Uses a **Linear Feedback Shift Register (LFSR)** to generate pseudo-random sequences for **spread-spectrum communication** and **cryptography**.  

**Shannon coding** is a foundational technique in **information theory**, while **PN sequences** are essential for **signal encoding and error detection** in communication systems.  

---

## 🎯 Objectives  
- ✅ **Implement Shannon's encoder and decoder** in C for efficient data compression.  
- ✅ **Generate PN sequences** using shift registers for **spread-spectrum applications**.  
- ✅ **Validate simulation outputs** against **manual calculations** for accuracy.  
- ✅ **Analyze the efficiency and applications** of Shannon coding and PN sequences.  

---

## 📚 Introduction  

### 🔹 **Shannon Coding**  
- **Named after:** Claude Shannon, the father of **information theory**.  
- **Purpose:** Reduce message length by assigning **shorter codes to frequent symbols** and **longer codes to rare symbols**.  
- **Applications:**  
  - **Data Compression:** ZIP, MP3, MPEG.  
  - **Communication Systems:** Efficient transmission with minimal redundancy.  

### 🔹 **PN (Pseudo-Noise) Sequence**  
- **What is it:** A **binary sequence** that mimics random noise, generated deterministically using shift registers.  
- **Key Properties:**  
  - **Pseudo-randomness:** Resembles white noise.  
  - **Low cross-correlation:** Ensures distinct signals in spread-spectrum systems.  
- **Applications:**  
  - **Direct Sequence Spread Spectrum (DSSS)**.  
  - **Frequency Hopping Spread Spectrum (FHSS)**.  
  - **Cryptography and Error Detection**.  

---

## 🛠️ **C Programs Overview**  

### 📌 **1. Shannon Encoder and Decoder in C++**  
- **Language:** C++  
- **Key Functions:**  
  - **Cumulative Probability Calculation:** Determines code length.  
  - **Binary Conversion:** Converts cumulative probability to binary codes.  
  - **Encoding:** Converts symbols to binary codes.  
  - **Decoding:** Reconstructs original message from binary codes.  

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to calculate cumulative probabilities
vector<double> calculateCumulativeProbabilities(vector<double> probabilities) {
    vector<double> cumulative_probabilities(probabilities.size(), 0);
    cumulative_probabilities[0] = 0;
    for (size_t i = 1; i < probabilities.size(); i++) {
        cumulative_probabilities[i] = cumulative_probabilities[i - 1] + probabilities[i - 1];
    }
    return cumulative_probabilities;
}

// Function to convert cumulative probability to binary
string convertToBinary(double cumulative_prob, int code_length) {
    string binary_code = "";
    double frac = cumulative_prob;
    for (int i = 0; i < code_length; i++) {
        frac *= 2;
        binary_code += (frac >= 1) ? '1' : '0';
        if (frac >= 1) frac -= 1;
    }
    return binary_code;
}
```


## 📌 2. PN Sequence Generator using Shift Register in C  

### 🔹 **Language:** C  
### 🔹 **Key Features:**  
- Uses **Linear Feedback Shift Register (LFSR)** with **4 stages**.  
- Generates a **maximal-length sequence** (2^n - 1).  
- Demonstrates **pseudo-randomness, balance, and periodicity**.  

---

### 📜 **C Code for PN Sequence Generator**  
```c
#include <stdio.h>

int main() {
    int n = 4;
    int L = (1 << n) - 1;
    int shift_register[4] = {1, 0, 0, 0};
    int pn_sequence[L];
    int feedback_taps[4] = {0, 0, 1, 1};

    printf("Generated 4-bit PN sequence:\n");
    for (int i = 0; i < L; i++) {
        pn_sequence[i] = shift_register[3];
        printf("%d ", pn_sequence[i]);
        
        int feedback = 0;
        for (int j = 0; j < n; j++) {
            feedback ^= (shift_register[j] * feedback_taps[j]);
        }
        
        for (int j = n - 1; j > 0; j--) {
            shift_register[j] = shift_register[j - 1];
        }
        
        shift_register[0] = feedback;
    }
    printf("\n");
    return 0;
}

```

## 📈 **Simulation Results**  

### 🔹 **Shannon Encoder Output**  
```yaml
Symbol: 1, Code: 00  
Symbol: 2, Code: 01  
Symbol: 3, Code: 101  
Symbol: 4, Code: 1100  
Symbol: 5, Code: 1110  
Encoded Message: 000110111001110  
Decoded Message: 1 2 3 4 5 1 3 2  

### 🔹 **PN Sequence Output**  
```plaintext
Generated 4-bit PN sequence: 0 0 0 1 0 0 1 1 0 1 0 1 1 1 1 

```

## ✅ **Advantages**  

| **Aspect**         | **Shannon Coding**                                        | **PN Sequence**                                           |
|--------------------|-----------------------------------------------------------|------------------------------------------------------------|
| **Efficiency**     | Minimizes message length                                   | Ensures secure and interference-free communication         |
| **Application**    | Data compression, storage, communication systems           | DSSS, FHSS, Cryptography, Error Detection                   |
| **Robustness**     | Accurate decoding with prefix-free codes                   | High noise immunity and low cross-correlation               |

---

## 🚀 **Applications**  
- **Shannon Coding:** Data compression, cryptography, communication systems.  
- **PN Sequence:** Spread spectrum, error detection, cryptography.  

---

## 🏁 **Conclusion**  
The **Shannon encoder and decoder** implemented in C demonstrates the efficiency of **entropy-based compression** by reducing redundancy without information loss.  
The **PN sequence generator** showcases the practical application of **LFSR** in generating deterministic yet **pseudo-random sequences** for secure and robust communication systems.  

---


