# Make Me Laugh

A tiny web app that tries to make you laugh about anything you describe. You type in a situation, pick the kind of humor you want, and it fires back five short jokes that pop onto the screen one by one and dissolve away. Every joke runs on an AI model living on your own laptop through Ollama. No internet, no accounts, no API keys.

This document is the starting point for the build. It describes the app, its features, and how it leans on a local model. The code comes later.

---

## The idea in one paragraph

Most people have seen an AI tell a flat, lifeless joke. This app turns that weakness into the whole point. You give it something real to work with, "my Monday," "airport wifi," "my cat ignoring me," and it riffs on that exact thing. It does not give you one safe answer. It gives you five, each coming at the topic from a different angle, and it lets you steer the flavor of the humor before it tries. When one lands, you laugh out loud, and that laugh is the result. You cannot fake it and you cannot get it from a model that prints a paragraph and stops.

## What the app actually does

1. You describe something in a text box. Anything. A feeling, a person, a situation, a pet peeve.
2. You pick a few options that shape the humor (style, length, how clean or spicy).
3. You hit the button.
4. The app sends your description plus your chosen options to the local model running in Ollama.
5. The model returns five short, genuinely different jokes.
6. The jokes pop onto the screen one at a time and gently dissolve, like a small performance rather than a wall of text.

That is the entire loop. Simple on the surface, with a surprising amount going on underneath.

## Powered by Ollama, running locally

This is the part worth saying out loud, because it changes how the app feels.

Everything happens on the laptop. The model that writes the jokes is downloaded and running through Ollama on the same machine the app runs on. You can turn the wifi off and it keeps working exactly the same. Nothing you type ever leaves your computer.

Concretely:

- Ollama runs a small local server at `http://localhost:11434`.
- The app sends each request to that address. There is no cloud call anywhere.
- The default model is `qwen3.5:4b`, the same one in the setup guide. Anyone running `qwen3.5:2b` or `gemma4:e2b` can use those instead by changing one line.
- Humor is personal and sometimes a little private. Because the model is local, you can describe anything without it being sent off to a company server. That privacy is real, not a marketing line.

A request to the model looks roughly like this:

```
POST http://localhost:11434/api/chat
{
  "model": "qwen3.5:4b",
  "messages": [
    { "role": "system", "content": "<the humor instructions, built from the user's options>" },
    { "role": "user", "content": "<what the user described>" }
  ],
  "stream": false,
  "format": "json"
}
```

The `format: "json"` part asks the model to return clean, structured data so the app can reliably pull out the five jokes. More on that below.

## Core features

**One simple input.** A single text box where the user describes the thing they want jokes about. Empty input should be handled gently, either a nudge to type something or a "surprise me" fallback.

**Variety options the user selects.** A small set of controls that change the request before it is sent. This is what keeps it fresh and what makes every person's result different. Detailed in the next section.

**Five jokes, on purpose.** The app always asks for five, and it asks for five that are different from each other. One flat pun repeated five ways is a failure. Range is the requirement.

**Pop and dissolve.** Jokes appear one at a time and fade out, so it feels performed rather than printed. Kept deliberately simple so it never slows the build down.

**Fully offline.** Works with wifi off. The app should make this obvious, maybe a small "running locally" badge, because it is the most surprising thing about it.

## The variety options

These are the controls the user picks from before generating. Each one quietly rewrites part of the instruction sent to the model. They are the heart of why the app stays interesting after the first try.

**Comedy style.** The main control. The user can pick one or combine a few.

- Observational, the everyday "why is it like this" humor
- Absurd, surreal and unexpected
- Wordplay and puns
- Sarcastic
- Deadpan, dry and flat on purpose
- Dad jokes
- Wholesome, gentle and warm
- Dark, for the brave

**Length.** How long each joke runs.

- One-liners
- Short, a setup and a punchline
- Mini-story, a few sentences that build

**Edge level.** How far it is allowed to go.

- Keep it clean, safe for any room
- A little spicy, sharper and bolder

**Angle (optional).** What the jokes point at.

- About the topic, the default
- Roast me, turn it on the user
- Cheer me up, kinder, lift the mood

Sensible defaults matter. If the user picks nothing, the app should still work: default to Observational, Short, Keep it clean, About the topic. That way a first-timer gets a good result with zero effort, and the options reward anyone who explores.

## How the options become an instruction

Every option the user selects gets folded into the system prompt, the plain-language instruction the model reads before it writes anything. A template version:

```
You are a sharp, quick comedian. The user will describe something.
Your job is to make them laugh about it.

Write exactly 5 jokes. Each joke must take a clearly different angle
from the others. Do not reuse setups or punchlines.

Comedy style: {selected styles}
Length: {selected length}
Tone: {clean or spicy}
Point the jokes at: {the topic / the user / lifting their mood}

Return only JSON, no extra text, in this exact shape:
{ "jokes": ["...", "...", "...", "...", "..."] }
```

The user's actual description goes in as the user message. Change one line of this prompt and the whole personality of the app changes, which is the single most useful thing a beginner can learn about working with models.

## The five-jokes problem, and why it is the real lesson

Small models love to give you five versions of the same joke. Left alone, the app will produce five near-identical puns and the bit dies. Fixing that is the most valuable moment in the whole build.

The fix lives in the instruction: demand that each joke take a different angle, name the angles if needed (one observational, one absurd, one wordplay, and so on), and tell the model plainly not to repeat itself. Watching the output go from "five flat clones" to "five that actually differ" by editing one sentence is the clearest possible demonstration of prompt quality. It teaches range, not just answers.

There is a second common snag worth planning for: the model sometimes wraps its JSON in extra chatter, which breaks the app. The fix is to tighten the prompt ("return only raw JSON, no markdown, no preamble") and to have the app fail softly if parsing does not work. That failure-then-fix loop is honest and useful.

## The pop and dissolve

Keep this light. When the five jokes come back, show them one at a time with a short delay between each, and let each one fade after a moment. The goal is to make the app feel like it is performing for you rather than dumping text. It should never become the hard part of the build or steal time from the model work. A simple timed fade is plenty.

## Suggested build arc

For a follow-along session, the app is built in clear stages, each one producing something visible.

1. **Scaffold.** A one-page app: a text box, a button, and an area for results. The UI appears.
2. **Connect.** On click, send the text to the local model at `localhost:11434` and show the raw reply. The app is now talking to AI, offline. First real "whoa."
3. **Steer.** Turn the reply into jokes by adding the comedian instruction and asking for five in JSON. Now it is actually funny, or at least trying.
4. **Add the options.** Drop in the style, length, edge, and angle controls and wire them into the prompt. The same app suddenly has range, and everyone's screen does something different.
5. **Make it perform.** Add the pop and dissolve so the jokes feel alive.

## Stretch ideas, if there is time

- A "surprise me" button that fills the input with a random everyday topic.
- A laugh-o-meter where the user marks which joke landed, just for fun.
- Let the user pick the model in the UI and compare how `qwen3.5:2b` and `qwen3.5:4b` differ at the same joke.
- A second round that builds on the first, asking the model to top its best joke.

## Technical notes

- **Runtime:** Ollama, already installed and running, serving at `http://localhost:11434`.
- **Default model:** `qwen3.5:4b`. Swappable to `qwen3.5:2b` or `gemma4:e2b`.
- **App stack:** a minimal Node.js web app, one page.
- **Endpoint:** `POST /api/chat` with a system message and a user message.
- **Structured output:** request JSON with `format: "json"` and a fixed shape so the five jokes are easy to read out reliably.
- **Offline:** no third-party calls of any kind. The app should work with networking disabled.
