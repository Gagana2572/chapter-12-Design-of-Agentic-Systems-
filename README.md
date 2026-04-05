# Chapter 12: Chain-of-Thought, Few-Shot, and Meta Language Creation
### Design of Agentic Systems with Case Studies

---

I wrote this chapter to answer one question I could answer without looking anything up:
**what breaks in a Meta Language system, and why does the architecture cause the failure, not the model?**

The answer is format overfitting. One line of code proves it.

---

## Links

 [Read Chapter 12](https://gagana2572.github.io/chapter-12-Design-of-Agentic-Systems-/Chapter12/Chapter12.html)

 [Author's Note](https://gagana2572.github.io/chapter-12-Design-of-Agentic-Systems-/AuthorsNote/AuthorsReview.html)

 [Watch the Video](https://drive.google.com/file/d/1FTh0QNF6SSMB5XBSNUyIyQBrtFh9xE1f/view)

 [Open Notebook in Colab](https://colab.research.google.com/drive/1xG3FFcS-Rsjty6ti3Lx_gK7eQrKVrQiS?usp=sharing)

---

## What's in This Repo

| Folder / File | Description |
|---|---|
| `Chapter12/Chapter12.html` | Full publication-ready chapter |
| `AuthorsNote/AuthorsReview.html` | Design choices, tool usage, self-assessment |
| `Collab Notebook/chapter_12_med_extraction.ipynb` | Runnable notebook, three architectures, three failure modes |
| `index.html` | Landing page |
| `README.md` | You are here |

---

## The Star Failure — Try It Yourself

Go to Cell 18 in the notebook. Change one line:

```python
# Before
dose_field = "dose: [numeric+unit | CONFLICTING(source_a, source_b) | UNCONFIRMED | null]"

# After
dose_field = "dose: [numeric+unit]"
```

Run the cell. The lisinopril conflict appears in the ANALYZE trace and disappears in FORMAT. The model knew. The schema had no path for uncertainty. So it fabricated a value. That is format overfitting.

---

## The Human Decision Node

During development, the AI proposed that the VERIFY phase should check whether every FORMAT field is populated, a schema compliance check. I rejected that.

Checking that every field has a value is not the same as checking that every field has a value that came from the text. I implemented a semantic consistency check instead, confirming that every uncertainty flagged in ANALYZE appears in FORMAT. This decision is documented in Cell 16 of the notebook and stated on camera in the video.

---

*Gagana · Spring 2026 · Design of Agentic Systems with Case Studies*
