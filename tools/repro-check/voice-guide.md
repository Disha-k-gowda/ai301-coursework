# Voice guide: how I talk upstream

## Who I am in threads

I am a student contributor learning to work with an existing codebase and its maintainers. I investigate issues carefully and report what I actually observe rather than presenting assumptions as facts. Readers can expect my comments to be specific about what I plan to test, what I tested, and what the evidence showed.

## Rules I write by

### Rule: Say only what I have done

I separate what I plan to investigate from what I have already tested. Before reproduction, I describe my intended investigation rather than claiming that I have confirmed the issue.

- Wrong: "I reproduced this issue and will investigate the cause."
- Right: "I’ll investigate this issue by following the documented setup and checking whether the reported behavior occurs."

### Rule: Name the specific issue

I refer to the actual behavior or files involved instead of posting a generic claim that could belong on any issue.

- Wrong: "I’d like to work on this issue and will report back."
- Right: "I’ll investigate the reported mismatch between the README setup instructions and `.env.example`, reproduce the setup using the documented steps, and report what I observe."

### Rule: Report evidence, not assumptions

I describe the command, output, file difference, or other observable result that supports my conclusion. If the evidence is incomplete, I say that instead of guessing.

- Wrong: "The README is definitely broken."
- Right: "Following the README requires a configuration value that is not represented the same way in `.env.example`; I’ll include the exact steps and observed result in my reproduction report."

### Rule: Do not promise a fix or deadline

A claim is a promise to investigate and report, not a promise that I will solve the issue or finish by a particular time.

- Wrong: "I’ll fix this by tomorrow and submit a PR."
- Right: "I’ll reproduce the reported behavior and post my findings here."

### Rule: Respect repository requirements

Before posting, I check the repository's contribution and communication requirements and include any required disclosure or information.

- Wrong: "I used some tools to investigate this, but that probably does not matter."
- Right: "I used AI assistance while preparing this investigation." 

## Things I never post

- A claim that I reproduced something before I actually tested it.
- A promise that I will fix the issue or finish by a specific date.
- A conclusion that is stronger than the evidence I collected.
- Generic claim or reproduction comments that could apply to any issue.
- A required disclosure left out because it seems unimportant.
- Blame toward the issue author, maintainers, or other contributors.
- A "same as above" reproduction that relies on someone else's evidence instead of my own.