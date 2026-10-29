# Step 4: Complete the worksheet and decide one mitigation

## The idea

The rows from Step 3 aren't an answer for the dispatcher yet. They don't need a report on the model. They need to know what Coldline will do when the model is slow, wrong or silent. The worksheet turns numbers into that one decision.

A mitigation is one change that reduces the harm of a failure you actually observed, with a cost you can state. It acts on what comes back from the model call, not on a particular model, so it still holds when the model changes. The lesson offers four:

- **Keep the refusal:** accept that some runs end with nothing for the dispatcher.
- **Ask once more:** retry once when an answer can't be read.
- **Limit each call's time:** treat a slow answer as missing.
- **Narrow the question:** say in the request exactly what's allowed at that moment.

Each option fits a different problem. Each one also costs something different: the dispatcher's manual work, an extra call's time and tokens, a correct answer lost to a slow model, or longer requests.

You pick exactly one, the one that matches the behavior that would hurt the dispatcher first, and you show the numbers that chose it. A reader who wasn't there should reach the same option from your rows. Then say what evidence would prove the mitigation worked, or that it wasn't needed. You decide here; you don't build it in this Task.

> Covered in **Retries, Backoff, and the Billed Retry Storm**, in **Partial-Failure Patterns**, and in **Architecture Decision Records**.

## What's expected

- The worksheet has five sections:
  - the sample and run record
  - response variance
  - latency
  - failure behavior
  - the mitigation decision
- The record names the commands, the times, whether the endpoint was available, and the secret's name, never its value.
- Variance is per request: the distinct kinds across runs beside the emulator's one kind, how the reasons differed, and malformed and missing answers counted separately.
- Failure behavior says what your agent would do with each bad row, taken from your handlers and the wrapper's rules, not from a run.
- The decision names exactly one option, the numbers that selected it, its cost, and the evidence that would prove it.

## When you're stuck

### You're not sure what goes in each section

<details><summary>Move 1</summary>

Start with the record: what did you run, when, and was the endpoint up? A reader needs that before any number.

</details>

<details><summary>Move 2</summary>

For variance and latency, read straight from your rows and summary line. Group the rows per request.

</details>

<details><summary>Move 3</summary>

Keep interpretation for the last two sections. The first three state what you observed.

</details>

### None of the four options fits what you saw

<details><summary>Move 1</summary>

Which behavior would bother the dispatcher first: a run that ends with nothing, a long wait, a proposal that changes between runs, or one that asks for something outside the rules?

</details>

<details><summary>Move 2</summary>

Read the description of each option again, including the cases the lesson says it fits.

</details>

<details><summary>Move 3</summary>

Tool calls that follow text in the retrieved procedure are expected, and the tool's checks already turn them down. Which option does the lesson match to that case?

</details>

### You can't say what the agent would do with a bad answer

<details><summary>Move 1</summary>

The comparison never ran the graph. Which code decides what happens to an answer that doesn't fit the contract?

</details>

<details><summary>Move 2</summary>

Which code decides what happens to a slow or missing answer?

</details>

<details><summary>Move 3</summary>

For each bad row, follow the answer through those two places and write the outcome: a named refusal, or a retry and then an error.

</details>

### Your decision has no numbers behind it

<details><summary>Move 1</summary>

Could a reader reach the same option from your rows alone?

</details>

<details><summary>Move 2</summary>

Which counts and which latency did you actually use?

</details>

<details><summary>Move 3</summary>

Name them in the decision, beside the option, its cost, and the evidence that would prove it.

</details>

### The endpoint was unavailable

<details><summary>Move 1</summary>

What failure did you see, and what message did you keep?

</details>

<details><summary>Move 2</summary>

An unreachable model is a failure in its own right. Which of the options exist for exactly that case?

</details>

<details><summary>Move 3</summary>

Decide from the emulator baseline and the failure you saw, and say so in the record.

</details>
