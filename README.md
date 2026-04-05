# Chapter 12: Chain-of-Thought, Few-Shot, and Meta Language Creation
### Design of Agentic Systems with Case Studies

---

I wrote this chapter to answer one question I could answer without looking anything up:
**what breaks in a Meta Language system, and why does the architecture cause the failure, not the model?**

The answer is format overfitting. That is what this chapter is about.

The scenario is a clinical medication extraction pipeline at a regional hospital. The inputs are messy. The stakes are real. And the failure, a model that fabricates dose values rather than flagging uncertainty, passes every automated validation check. The output validates. The downstream system accepts it. No alarm fires.

That is not a model problem. That is an architecture problem. And one line of code proves it.

---

## What's in This Repo

| File | Description |
|---|---|
| `Chapter12.html` | The full publication-ready chapter |
| `AuthorsReview.html` | Author's Note, design choices, tool usage, and honest self-assessment |
| `chapter_12_med_extraction.ipynb` | Runnable Jupyter notebook, three architectures, three failure modes triggered |
| `index.html` | Landing page linking everything together |
| `README.md` | You are here |

---

## Read, Watch, and Run

**Chapter**
The full chapter walks through three prompt architectures, zero-shot, few-shot with chain-of-thought, and Meta Language DSL, and shows what breaks when each one fails. Every failure mode is triggered in the notebook, not just described.

👉 [Read Chapter 12](https://gagana2572.github.io/chapter-12-Design-of-Agentic-Systems-/Chapter12.html)

---

**Author's Note**
Three pages covering design choices, every Human Decision Node where I caught and corrected an AI architectural claim, and an honest self-assessment scored against the rubric.

👉 [Read the Author's Note](https://gagana2572.github.io/chapter-12-Design-of-Agentic-Systems-/AuthorsReview.html)

---

**Video Walkthrough**
A 10-minute Explain, Show, Try walkthrough. The Show section includes the Human Decision Node on camera, the moment I rejected the AI's proposed VERIFY architecture and explained why.

👉 [Watch the Video](https://drive.google.com/drive/folders/109AcRVL17ABnjMwrO9ODkPFrjdUcPP9Q?usp=sharing)

---

**Notebook**
Run it yourself. You need a free Groq API key from console.groq.com, no credit card needed. Add it to Colab Secrets as `GROQ_API_KEY` and run all cells top to bottom.

👉 [Open in Colab](https://colab.research.google.com/drive/1xG3FFcS-Rsjty6ti3Lx_gK7eQrKVrQiS?usp=sharing)

---

## The Star Failure, Try It Yourself

Go to Cell 18 in the notebook. Find this line:

```python
dose_field = "dose: [numeric+unit | CONFLICTING(source_a, source_b) | UNCONFIRMED | null]"
```

Change it to:

```python
dose_field = "dose: [numeric+unit]"
```

Run the cell. Watch what happens to the lisinopril conflict. It appears in the ANALYZE trace and disappears in FORMAT. The model knew. The schema had no path for uncertainty. So it picked a value.

That is format overfitting. One line caused it. One line fixes it.

---

## The Three Failure Modes

| Failure Mode | Trigger | Why It Is Dangerous |
|---|---|---|
| Format Overfitting | Remove uncertainty tokens from schema | Fabricated values pass validation silently |
| Exemplar Bias | Exemplar set drawn from clean inputs only | Wrong clinical flag applied to ambiguous entry |
| CoT Collapse | Corrupted reasoning step in exemplar | Error visible in ANALYZE, invisible in FORMAT |

---

## The Human Decision Node

During development, the AI proposed that the VERIFY phase should check whether every FORMAT field is populated, a schema compliance check.

I rejected that.

Checking that every field has a value is not the same as checking that every field has a value that came from the text. A schema compliance check passes a record full of fabricated values because fabricated values are syntactically valid.

The check I implemented confirms that every uncertainty flagged in ANALYZE appears in FORMAT. That is a semantic consistency check. Different mechanism. Different failure mode prevention.

This decision is documented in Cell 16 of the notebook and stated on camera in the video.

---

*Gagana · Spring 2026 · Design of Agentic Systems with Case Studies*
