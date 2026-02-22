---
date: '2025-10-07'
feed: show
tags:
- genai/prompt
title: Prompt Enhancement Tips
---

# Nudge Phrases
Used to push the auto model selections to try and use better or thinking models where appropriate
1. Think hard about this
2. Think deeply about this
3. Think carefully

# Verbosity
Affect the level of output/response you receive
- Low - give me the bottom line in 100 words or less
- Medium - aim for concise 3 to five paragraph explanation
- High - provide a comprehensive and detailed breakdown 600 to 800 words

# Prompt Optimizer Meta Prompt
Optimization prompt to help improve or adjust your prompt to be better
```
You are an expert prompt engineer specializing in creating prompts for AI language models, particularly `[model]`

Your task is to take my prompt and transform it into a well-crafted and effective prompt that will elicit optimal responses.

Format your output prompt within a code block for clarity and easy copy-pasting.

## Here’s my initial prompt:
```

# Prompt Multiplier
I'm trying to get good results using the following prompt:
`[insert prompt]`
Your task is to write a better prompt that is more optimal for `[text model]` and would produce better results.
Give me 3 variations.

# Evaluating/Improving a Prompt
Evaluate the quality of the following prompt and provide feedback on what I did well and did not do well. Then, refine my prompt and return it.

# Prompt Better
Provide a prompt that would get me the final results we got here from the first request

# XML Tags
Sandwich pertinent sections in between XML tags to help it discern what is what
`<Task> </Task>`
`<Tone> </tone>`

# Perfection Loop
Have the system continue looping through it's own work until it creates a 10/10 
```
Before you respond, create an internal rubric for what defines a 'world-class' answer to my request. Then internally iterate on your work until it scores 10/10 against that rubric, and show me only the final, perfect output.
```

# Output Guardrails
Produce the draft with inline citations, highlight low-confidence areas, and add a final ‘What could be wrong here?’ checklist.

# Optionality
Options in prompt templates to ask me which way to complete - 3 tones, 3 options for length, etc - simplifies or condenses a few different prompt options into a singular prompt.