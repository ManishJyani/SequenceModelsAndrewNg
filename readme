# Sequence Models git 

Sequence models are used when the **order of the input** plays an important role in predicting the output.  
Examples include:
- Speech recognition
- Time series prediction
- Music generation
- Sentiment analysis

---

## Notation

Let's consider an example for **name identification** where we provide a sequence of words as input.

**Example Sequence**:  
"My name is Manish Jyani"

- Input sequence representation:  
  \( x^{<1>}, x^{<2>}, x^{<3>}, x^{<4>} \)
- Total input length: \( T_x = 4 \)
- \( x \) → represents the **input** at each time step  
- \( y \) → represents the **output** at each time step  
- \( T_y \) → total length of the **output sequence**

---

## Generalized Representation

For the \( i^{th} \) training example:

\[
x^{(i)<t>} \quad \text{= the } t^{th} \text{ element in the } i^{th} \text{ training example}
\]

- Here, \( t \) stands for **temporal step**.
- The same notation applies for outputs:  
  \( y^{(i)<t>} \) → output at time step \( t \) for training example \( i \).

---

## Gotcha Moment 🚀

In sequence inputs, when we say **"previous time step"**, it simply refers to the **previous element in the sequence** (not actual clock time).

For example:  
- \( x^{<t-1>} \) lies **to the left** of \( x^{<t>} \) in the sequence.
- There is **no actual notion of time** here — it only represents the **order of elements**.

