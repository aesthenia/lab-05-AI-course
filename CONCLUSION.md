# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

(write here)
Layer 1 changed the most. 
Bare: 16 correct, 4 wrong, 4 no answer.
After layer 1: 18 correct, 6 wrong, 0 no answer. It changed what the agent can
do: tool errors go back to the model, so it can try again. q23 and q24 became
correct, but q21 and q22 became wrong. 
Layer 2 changed nothing. 
Layer 3 kept 18 correct and only changed what the agent admits: q18 and q22 went from wrong to no answer.

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

(write here)
q11: which region had the lowest retail trade in 2021. The tool call was
correct, it only went wrong at the reading step: the list is sorted highest first,
so the lowest is the last row, but the model answered "Almaty Region". The
harness only asked for the ANSWER line. Grounding checks only numbers, and a
region name has no numbers, so it passed obviously. I would add a code check that
compares the answer with the last row, it will cost one or two extra model calls,
more tokens and time, and the check itself can make a mistake as well.

## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

(write here)
I would ship the fixed workflow. On the 15 fixed-shape questions it got 13
correct, 0 wrong, 2 no answer, with 15 model calls, 3852 tokens and 16.0
seconds. The bare agent got 9 correct, 2 wrong, 4 no answer, with 26 calls,
19835 tokens and 47.9 seconds. So the workflow is more accurate, about 5 times
cheaper in tokens and 3 times faster. The agent also got both "lowest"
questions (q08, q11) wrong. I would choose the agent for a question with an
unknown shape, like a growth question that needs several tool calls and a
calculation.

---

I wrote this file myself, without any AI tool.
