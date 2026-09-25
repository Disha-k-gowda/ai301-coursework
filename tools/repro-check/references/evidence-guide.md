# Evidence guide: where proof lives in a reproduction package

## Environment

Where it lives: In an eval bundle, look at the repro report's environment record, the issue context, and the repo-facts block. In live mode, look at the student's draft repro comment together with the issue thread and the repository documentation that states setup, dependency, platform, or version requirements.

What good looks like: The environment identifies the software, versions, platform, configuration, or other conditions that materially affect the reproduction. Those conditions should match the issue's target environment, or any relevant difference should be explicitly identified so another person can interpret the result.

## Steps

Where it lives: In an eval bundle, look at the repro report's reproduction steps, including setup actions, commands, inputs, configuration changes, and the transition that triggers the behavior. Use the issue context and repo-facts when they establish a required starting state. In live mode, look at the student's draft repro comment and the repository's setup or usage documentation.

What good looks like: Starting from the recorded environment and starting state, a stranger can perform the actions in the stated order and reach the attempted trigger without inventing a material command, input, configuration, or intermediate action. Details that do not affect reproduction do not need to be recorded.

## Behavior shown

Where it lives: In an eval bundle, look at the repro report's observed output and its supporting artifacts, such as command output, logs, error messages, screenshots, or other captured results. Read those artifacts against the behavior described in the issue context. In live mode, compare the evidence in the student's draft repro comment with the specific behavior reported in the GitHub issue.

What good looks like: The artifacts provide observable evidence about the specific behavior named by the issue. A successful reproduction shows that behavior rather than merely a related failure; a cannot-reproduce result shows what was actually observed when the documented reproduction was attempted.

## Honesty

Where it lives: In an eval bundle, compare the repro report's stated outcome with its steps, observed behavior, and supporting artifacts. In live mode, compare the conclusion in the student's draft repro comment with the evidence included in or referenced by that comment.

What good looks like: The conclusion says no more than the evidence supports. A reproduced result is backed by evidence of the issue's specific behavior, while a cannot-reproduce result accurately reports the attempted conditions and observed result. If the evidence is mixed or limited, the wording reflects that limitation instead of presenting an unsupported conclusion as certain.

## Comms

Where it lives: In an eval bundle, compare the claim comment and repro report with the issue context, repo-facts block, and any repository communication or contribution requirements supplied in the package. In live mode, inspect the GitHub issue thread and applicable repository files or templates, such as CONTRIBUTING, issue or pull-request templates, README guidance, and stated AI-use disclosure policies, then compare them with the student's draft comment.

What good looks like: The claim identifies the specific issue and truthfully states the investigation the student intends to perform without claiming work that has not happened or promising a fix or completion date. The repro communication accurately states what was attempted and observed and follows applicable repository-specific requirements, including any required AI-use disclosure. Generic boilerplate does not substitute for issue-specific information.