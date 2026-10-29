# Step 3: Compare a hosted model with the emulator on a fixed request set

## The idea

The emulator answers from your scripts, so every run is the same. A real model answers on its own, and three things change:

- the proposal can differ between two runs of the same request
- the answer can take longer
- the answer can fail to arrive, or fail to fit the contract

The comparison measures exactly those, on a small fixed set of requests, each sent a few times, beside the emulator's answer for the same moment.

Four ideas keep the comparison honest:

- **Judge every answer the way the agent would:** build a proposal from it with your contract. If the contract rejects it, the agent would get a refusal, so record it as malformed. A model can't know how many tokens it used, so that count comes from the response's usage report, not from the model.
- **Well formed isn't the same as allowed:** a tool call can fit the contract and still ask for a next step or reason code outside your authority lists. That's its own outcome. The retrieved procedure even contains an instruction a model might follow.
- **What leaves your machine is redacted:** the request text goes through the same redaction the worker applies, and the key comes through the secret port, never from a file or a command line.
- **Bad results are the finding:** one live run, kept as it came. Running again to make bad rows go away hides the thing you were measuring.

> Covered in **3.6 Evaluating an Agent Run**.

## What's expected

- A fixed request set of three to five named requests. Each has its text and its emulator baseline: the script and the position it stands for.
- An emulator dry run where every row is parsed and matches its baseline.
- One live run, with the command and the time recorded. It writes one row per call:
  - the request name and the run number
  - the source
  - the kind and the reason
  - the tokens from the usage report
  - the latency
  - the outcome: `parsed`, `malformed`, `outside_authority`, `timeout` or `error`
- A summary line with these:
  - the number of runs
  - kind matches against the baseline
  - outside-authority answers
  - malformed answers
  - timeouts and errors
  - the median and maximum latency
- The raw rows sit under the ignored `evidence/` folder.
- If the endpoint can't be reached, the script says so before the set starts and exits without a sample.

## When you're stuck

### You can't pick the moments to compare

<details><summary>Hint 1</summary>

Read the approval script `poe demo` plays. Which proposals matter most to the dispatcher?

</details>

<details><summary>Hint 2</summary>

Each moment needs a baseline: which script and which position stand for it?

</details>

<details><summary>Hint 3</summary>

Pick three to five moments, such as the proposal of the review, the finish, and perhaps a second try from your recovery script, and name each request.

</details>

### Every hosted answer comes back malformed

<details><summary>Hint 1</summary>

Print one raw answer. Is it a single JSON object, or wrapped in other text?

</details>

<details><summary>Hint 2</summary>

Which fields does the contract require? Can a model know every one of them, such as its own token count?

</details>

<details><summary>Hint 3</summary>

Where does the response report usage?

</details>

<details><summary>Hint 4</summary>

The approach: ask the model for the kind, the reason and, for a tool call, its input. Read the token count from the response's usage report and add it before the contract judges the answer.

</details>

### The model proposes things your configuration doesn't allow

<details><summary>Hint 1</summary>

Read the procedure text you sent. Does it contain an instruction the model could follow?

</details>

<details><summary>Hint 2</summary>

Is such an answer malformed, or well formed but asking for something outside your lists?

</details>

<details><summary>Hint 3</summary>

Check a parsed tool call's reason code and next step against your authority configuration, and give those answers their own outcome. Keep them: they're a finding for Step 4.

</details>

### You're not sure how to give the script the key

<details><summary>Hint 1</summary>

Where does the worker's provider key live, and how does the worker read it?

</details>

<details><summary>Hint 2</summary>

Can your key live in the same place under a name you choose?

</details>

<details><summary>Hint 3</summary>

Store the key in the local secret store under your chosen name, read it through the secret port in the script, and keep the name, never the value, for your worksheet.

</details>

### The script can't reach the endpoint

<details><summary>Hint 1</summary>

Did the failure happen before the first call, or in the middle of the set?

</details>

<details><summary>Hint 2</summary>

Check the address and the model name against the lesson.

</details>

<details><summary>Hint 3</summary>

Check that the key you read is the one you stored, by its version, never by printing it.

</details>

<details><summary>Hint 4</summary>

If it still fails before the set starts, keep the message, check it holds no key, and continue with the emulator baseline. An unavailable endpoint is a result, not a failure of the Task.

</details>

### Two answers look the same but tell the dispatcher different things

<details><summary>Hint 1</summary>

Does your row compare only the kinds?

</details>

<details><summary>Hint 2</summary>

Read the reasons and tool inputs of two answers with the same kind. Would a dispatcher act the same way on both?

</details>

<details><summary>Hint 3</summary>

Keep the reason and the tool input in the rows you discuss, so the worksheet can say how answers with the same kind differ.

</details>

### The request sends personal data

<details><summary>Hint 1</summary>

Which function does the worker run on text before it reaches the model?

</details>

<details><summary>Hint 2</summary>

At which points does the worker call it? Read `src/worker/use_cases.py`.

</details>

<details><summary>Hint 3</summary>

Run the same redaction at the same points before your request leaves your machine.

</details>
