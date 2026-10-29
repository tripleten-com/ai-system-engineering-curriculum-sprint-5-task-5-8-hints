# Before you submit

The basic checks confirm that your work is there. They don't judge whether it's right. Your instructor reads your pull requests and evidence notes with four questions. Ask them of your own work first.

## Did you meet the Task's requirements?

- Does each case state its script, its decision, the full kinds list, the required events in order, the side effect and, where halted, the halt reason?
- Does the set carry a field named `version`, with a rule for changing it?
- Does `poe eval` run every case on a fresh exception, name the first mismatch and exit non-zero on a failure?
- Did the key reach the comparison only through the secret port, and did the request pass through redaction?
- Does the worksheet have all five sections and exactly one mitigation?

## Did you explain your design choices?

- Does your note say how a case says "no answer" and "no side effect", and why?
- Does it say which moments you compared, how many runs, and why that's enough?
- Does it give the mitigation's cost and what would prove it worked?

## Can your tests fail when the code is wrong?

- Did you make the comparison ignore order, the classifier accept everything and the summary miscount once each, and see tests fail?
- Did you watch each case fail in `poe eval` with one expectation changed?

## Did you state the limits of what your checks show?

- Does your note say what one day's sample can't tell you about the hosted model on another day?
- Did you keep the bad rows rather than rerunning to make them go away?
