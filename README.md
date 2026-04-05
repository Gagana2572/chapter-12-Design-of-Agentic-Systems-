# Chapter 12: Chain-of-Thought, Few-Shot, and Meta Language Creation
### Design of Agentic Systems with Case Studies

---

I wrote this chapter to answer one question I could answer without looking anything up:
**what breaks in a Meta Language system, and why does the architecture cause the failure, not the model?**

The answer is format overfitting. One line of code proves it.

---

## Links of What's in This Repo

 [Read Chapter 12](https://gagana2572.github.io/chapter-12-Design-of-Agentic-Systems-/Chapter12/Chapter12.html)

 [Author's Note](https://gagana2572.github.io/chapter-12-Design-of-Agentic-Systems-/AuthorsNote/AuthorsReview.html)

 [Watch the Video](https://drive.google.com/file/d/1FTh0QNF6SSMB5XBSNUyIyQBrtFh9xE1f/view?usp=sharing)

 [Open Notebook in Colab](https://colab.research.google.com/drive/1xG3FFcS-Rsjty6ti3Lx_gK7eQrKVrQiS?usp=sharing)

---


## The Human Decision Node

During development, the AI proposed that the VERIFY phase should check whether every FORMAT field is populated, a schema compliance check. I rejected that.

Checking that every field has a value is not the same as checking that every field has a value that came from the text. I implemented a semantic consistency check instead, confirming that every uncertainty flagged in ANALYZE appears in FORMAT. This decision is documented in Cell 16 of the notebook and stated on camera in the video.

---

*Gagana · Spring 2026 · Design of Agentic Systems with Case Studies*
