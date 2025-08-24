# **Sequence Models**

Sequence models are used when the **order** of the input plays an important role in predicting the output.  
Some common applications include:

- Speech recognition  
- Time series prediction  
- Music generation  
- Sentiment analysis  
- And more…

---

## **Basic Notation**

Let's understand the notation we'll use for sequence models.

### **Example Sequence**

> “My name is Manish Jyani”

- Inputs: x<sup>&lt;1&gt;</sup>, x<sup>&lt;2&gt;</sup>, x<sup>&lt;3&gt;</sup>, x<sup>&lt;4&gt;</sup>  
- Total input length: **T<sub>x</sub> = 4**  
- **x** represents the **input sequence**.  
- Similarly, **y** will represent the **output sequence**.  
- **T<sub>y</sub>** will represent the length of the output.

---

### **Generalized Representation**

For the *i*-th training example:  

x<sup>&lt;t&gt;</sup><sub>i</sub> → the **t-th element** in the **i-th training example**.

- Here, **t** stands for **temporal index** (position in the sequence).
- Example:  
  x<sup>&lt;3&gt;</sup><sub>2</sub> → the **3rd word** of the **2nd training example**.

---

### **Important Insight**

In sequence inputs, when we talk about the **previous time step**, it simply refers to the **previous word** in the sequence (on the **left side**).  
There’s **no actual time** involved here.

Example:  
x<sup>&lt;t-1&gt;</sup> lies **to the left** of x<sup>&lt;t&gt;</sup>.


# Gated Recurrent Unit (GRU)

The **Gated Recurrent Unit (GRU)** is a type of Recurrent Neural Network (RNN) architecture designed to handle **long-term dependencies** more effectively than vanilla RNNs.  
It introduces **gating mechanisms** to control how information flows through the network, making it efficient and less prone to the **vanishing gradient problem**.

---

## **1. Why GRU?**
Vanilla RNNs struggle with:
- **Vanishing/Exploding Gradients** → Training becomes unstable.
- **Short Memory** → They fail to capture dependencies over long sequences.
  
GRUs solve this by **selectively updating or resetting the hidden state** using gates, which helps the network decide **what to keep** and **what to forget**.

---

## **2. Core Idea**
GRU manages information using a **single hidden state** `h<t>` (no separate cell state like LSTM).  
The gates decide:
- Whether to **update** the hidden state with new information.
- Whether to **reset** the past memory.

This makes GRUs computationally lighter and easier to train compared to LSTMs.

---

## **3. GRU Architecture**

At each time step `t`, the GRU takes:
- **Input vector**: `x<t>`
- **Previous hidden state**: `h<t-1>`
- Produces:
    - **New hidden state**: `h<t>`

---

## **4. GRU Equations**

### **Step 1 — Update Gate (`z<t>`)**
Controls **how much past information** to carry forward.

\[
z^{<t>} = \sigma \left( W_z \cdot [h^{<t-1>}, x^{<t>}] + b_z \right)
\]

- If `z<t>` → **close to 1** → keep previous hidden state.
- If `z<t>` → **close to 0** → overwrite with new information.

---

### **Step 2 — Reset Gate (`r<t>`)**
Decides **how much past information** to ignore.

\[
r^{<t>} = \sigma \left( W_r \cdot [h^{<t-1>}, x^{<t>}] + b_r \right)
\]

- If `r<t>` → **close to 0** → forget past memory.
- If `r<t>` → **close to 1** → use previous memory fully.

---

### **Step 3 — Candidate Hidden State (`\tilde{h}<t>`)**
The **new memory** created at this time step.

\[
\tilde{h}^{<t>} = \tanh \left( W_h \cdot [r^{<t>} \odot h^{<t-1>}, x^{<t>}] + b_h \right)
\]

- If `r<t>` is small, past memory is largely ignored.

---

### **Step 4 — Final Hidden State (`h<t>`)**
Blend old and new information.

\[
h^{<t>} = (1 - z^{<t>}) \odot h^{<t-1>} + z^{<t>} \odot \tilde{h}^{<t>}
\]

- When `z<t>` ≈ **1** → focus on new information.
- When `z<t>` ≈ **0** → preserve old memory.

---

## **5. Key Advantages of GRU**
- Simpler than LSTM — fewer gates → **faster training**.
- Handles **vanishing gradients** better than vanilla RNNs.
- Requires **fewer parameters** than LSTMs, making it computationally efficient.
- Performs well when training data is limited.

---

## **6. Summary Table**

| **Aspect**      | **RNN**         | **GRU**         |
|-----------------|------------------|------------------|
| Vanishing Gradients | High problem | Reduced problem |
| Gates           | None            | Update, Reset   |
| Memory Handling | Single hidden state | Controlled by gates |
| Training Speed  | Fast, but unstable | Fast & stable |
| Parameters      | Fewer           | Moderate        |

---

## **7. Intuition**
Think of GRU as a **smart filter**:
- **Reset gate**: Decides *“How much past memory to forget?”*
- **Update gate**: Decides *“How much new info to add?”*
- Final hidden state `h<t>`: A **weighted mix** of past memory and new candidate memory.

---
