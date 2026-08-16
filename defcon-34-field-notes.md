# Defcon 34 Field Notes

These are field notes from attending my first DefCon in Las Vegas on Aug 6-9, 2026. I’d kind of written off conferences since attending a couple in the last few years. People tend to generically say they are useful for networking but I usually left feeling a bit disappointed by the depth and relevance of the content. DefCon was a nice surprise. For one, it was an area of personal interest and relevant to my work. Without being a security professional, you could find the right level of depth for your background.

A few sessions I particularly enjoyed and takeaways:


## Minimize Harm, Maximize Defense: How Anthropic Navigates the Offense-Defense Divide 
*Speaker: Curt Barnard*

- Frontier models themselves are difficult to use for security testing out of the box, as they’re specifically trained to follow certain safety behaviors, in both pre and post training, causing it to refuse security testing use cases.
  
- The gap between open weight models and frontier models is the headroom for frontier model security teams, as open weight can be manipulated and fine tuned away from its original alignment, by anyone, this becomes the baseline of what’s possible for misuse. Anthropic compares the frontier model defensive performance with what the open weight models can do and works to prevent that gap from closing.
  
- A lot of the work in using models to investigate cybersecurity issues is two-fold.
  
  - One is maximizing token usage efficiency for the right complexity of work in the investigation. You don’t want to burn through tokens for simple tasks, and at the same time the better model is not always best for all tasks. For example, frontier models exercise more reasoning autonomy, so they may choose to run off of the task and take more creativity, which can be not useful in a case where you need deterministic classification of an output. Small-scale model for simple classification tasks, frontier model for deep code investigation as a starting principle. I think this principle is applicable to more use cases than just safety.
  - Second, reviewing the validity of the AI’s output - is the issue the AI found actually real and important? In my own work, I continuously see this overlooked - actually looking at the data behind the output and validating it; everyone wants the metric, but few want to open the data behind it. It’s very easy to say AI hallucinates, yes the output is not good, but it’s a bit harder to pinpoint patterns and actionable next steps to improve it, and people often seem to lose interest at this step of the work where the findings become real.
  
- Generally, Anthropic over does the safety guardrails, for good reason, they’re on the frontier, their market differentiator is largely their investment into safety just as much as model capability, but that same value can block real safety work. This is an area Anthropic is actively partnering with safety professionals on through Project Glasswing - a coalition where partners get to access Mythos for defensive security work. The speaker recommended [this blogpost from Mozilla](https://blog.mozilla.org/en/privacy-security/ai-security-zero-day-vulnerabilities/), one of the involved partners.
  
- [Another read](https://www.anthropic.com/news/claude-fable-5-mythos-5) recommended by the speaker, explains how Anthropic’s cybersecurity constitution is applied as a classifier in the safety pipeline. They maintain and constantly iterate on this constitution which defines model safety principles and behavior, similar to their better known general Claude constitution.

- How do you detect bad actors from the people just investigating, learning? Identity verification is used as a proxy for bad intent, since intent isn’t observable.
  
- Lastly, token budget is also a real limitation of AI weaponization. You need tokens to make models do bad things. :)


## AI Pentesting is not a Vibe Check
*Speaker: Ads Dawson*

- AI system vulnerabilities are often in the application and embedding layer - not in the model itself. Or at least that’s where it’s frequently overlooked today.

- To isolate failure points of AI systems, you try to inject instructions in the model's context that gets it to do something it's not supposed to do.

- A very simple version of this is adding instructions to the query in white text - not visible to the user.

- Vulnerability surface area to inject bad context increases with agents, because there’s a ton of context agents pull and reference in its work, which remains invisible to the user.

- MCPs are currently an overlooked area for these vulnerabilities. Protections tend to stop at guarding against server-side request hacking, which leaves a lot of room for bad actors to work in. Tools calls are another.

## HALctf

This was my first ctf and I didn’t get to complete all the challenges, partially due to server constraints and largely due to user skill, but I learned a lot about how CTFs operate, especially by talking to the hosts and participants. At 1am, the night before the CTF was closing, there were still 50 agent runs in queue at a time.

<img width="1500" height="148" alt="defcon-halctf-screenshot" src="https://github.com/user-attachments/assets/846009bb-c2ef-4ac1-8d59-b6feaa124476" />
Screenshot is borrowed from the HALctf Discord, but this is an accurate depiction of what a lot of my participation time looked like. The off peak time was really during dinner hours which in hindsight I didn’t capitalize enough on. I’m looking forward to participating again next year.

## Takeaways across sessions - Safety Frameworks vs General AI Frameworks

While the talks focused on AI security, a lot of the points made seem to apply to any AI system work.

- Safety failure modes often exist above the model level, and the same is true of AI product quality problems. Agent orchestration and harnesses are critical to output quality in agentic products, just as much as the underlying model.

- A bigger model is not always better. For open ended tasks like finding a security vulnerability, bigger models that take more reasoning autonomy can be a liability. Where consistency and reliability are essential, like in LLM-as-a-judge pipelines, using a smaller model can ensure more consistency.

- You can’t evaluate what you can’t see. Agents use large contexts the user will never see (at least currently), which is a safety vulnerability. That’s also a core quality and user friction problem in agents; you need to see trajectory data, the full context agents operate on, to understand root causes and gaps for improvement. The output itself is only one part of the picture.

- Validation is a step frequently skipped, and often the most important. The Anthropic team spends a lot of time validating the security investigation work of the model at every step of a rigorous pipeline. This isn’t solved by hiring a huge rater team alone. It’s managed by overseeing every step of the validation pipeline reliably and consistently.
  

## In closing

I picked up a lock picking kit for fun on the way home. Overall, it was genuinely an enjoyable conference. I’d recommend it for anyone who has the budget and wants curated exposure into the side of tech most non-security roles don’t think too much about.
