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
