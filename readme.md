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

The **Gated Recurrent Unit (GRU)** is a recurrent architecture that handles **long-term dependencies** better than a vanilla RNN by using **gates** to control information flow, which helps mitigate the **vanishing gradient** problem.

---

## 1) Why GRU?
- Vanilla RNNs struggle to remember information over long sequences (gradients vanish/explode).
- GRUs add **gating** so the model can **keep** important past info or **update** it when needed.
- Simpler than LSTMs (fewer gates), typically **faster to train** while still strong on many tasks.

---

## 2) Notation & Setup
At time step **t**:
- Input: **x**<sup>&lt;t&gt;</sup>  
- Previous hidden state: **h**<sup>&lt;t−1&gt;</sup>  
- New hidden state: **h**<sup>&lt;t&gt;</sup>  

(We’ll use parentheses in equations, e.g., \(h^{(t)}\), for clarity.)

---


## 3) GRU Equations

**Update gate**  
![z_t](https://latex.codecogs.com/png.latex?z^{(t)}%20=%20\sigma(W_z%5B%20h^{(t-1)},x^{(t)}%20%5D%20+%20b_z))

**Reset gate**  
![r_t](https://latex.codecogs.com/png.latex?r^{(t)}%20=%20\sigma(W_r%5B%20h^{(t-1)},x^{(t)}%20%5D%20+%20b_r))

**Candidate hidden state**  
![h_tilde](https://latex.codecogs.com/png.latex?\tilde{h}^{(t)}%20=%20\tanh(W_h%5B%20r^{(t)}%20\odot%20h^{(t-1)},%20x^{(t)}%20%5D%20+%20b_h))

**Final hidden state**  
![h_t](https://latex.codecogs.com/png.latex?h^{(t)}%20=%20(1-z^{(t)})%20\odot%20h^{(t-1)}%20+%20z^{(t)}%20\odot%20\tilde{h}^{(t)})


## 4) Advantages (at a glance)
- **Better long-range memory** than vanilla RNNs.
- **Fewer parameters** and **faster** than LSTMs in many setups.
- Works well for **NLP, speech, and time-series** tasks.

---

## 5) Quick Comparison

| Aspect                | Vanilla RNN                 | GRU                                  |
|----------------------|-----------------------------|--------------------------------------|
| Gates                | —                           | Update \(z\), Reset \(r\)            |
| Handles long memory  | Weak                        | Stronger (reduced vanishing)         |
| Parameters           | Few                         | Moderate (less than LSTM)            |
| Training stability   | Can be unstable             | More stable                          |


Think of GRU as a **smart filter**:
- **Reset gate**: Decides *“How much past memory to forget?”*
- **Update gate**: Decides *“How much new info to add?”*
- Final hidden state `h<t>`: A **weighted mix** of past memory and new candidate memory.

---