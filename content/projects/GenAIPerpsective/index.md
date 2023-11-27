+++
title = 'Curiosity is all you need: How GenAI will transform creativity'
date = 2023-11-22T18:54:38-08:00
draft = false
description = "Blah blah blah"
+++

**DRAFT COMING**

# Anyone can create

`GenAI will dramatically reduce the barriers to creativity.` I don't mean creativity in the sense of the creative profession (i.e. designers and artists) although it will have tremendous impact there too. I mean creativity in the sense of the act of creation - the ability to envison and realize an idea - your own idea - independently. 
  
# Curiosity is all you need

For me, GPT has sparked a new enthusiasm and energy for learning and creation. Any topic, any thread, any thought, any idea has the potential to be realized if you are curious enough to see it through. Although I specifically used GPT to help me build software, I also believe that this trend will permeate other industries too.

In high school, I was given a science award for being the most inquisitive. I would often annoy teachers with my questions - some of which were dumb, sometimes repetitive, and perhaps distracting - but they were an essential part of the way I learned. My questions were my brain trying to form and validate my mental model of a concept. GPT is a teacher with limitless energy. It doesn't judge, it comes along with you on your learning journey and it never tires. Here are a few ways I have prompted GPT to help me understand an idea: 
1. Provide an example(s) (a simple tactic that can you can easily continue to modify to simpler and simpler examples)
2. Provide analogies or metaphors (GPT helped me understand the difference between policy driven and reward driven reinforcement learning algorithms through the lens of cooking)
3. Provide the space or framework in which this concept exists. (a tactic that I use frequently when I'm trying to situate and determine the level of the concept)
4. Validate or build on a partially-formed hypothesis (a tactic that I use when the picture is beginning to clear but I need better language to articulate it; sometimes I use the tactic "complete this sentence" where I leave an ellipsis for GPT to fill in)
5. Give more context about yourself (this is an obvious one - which is tell it more about the reason why you're trying to learn and anything relevant about yourself so that it can tailor its response)

# From three weeks to three days

As an example of how different it is for a non-technical person to build something now versus during pre-GenAI era. In 2019, I built my personal website using Gatsby by following a step-by-step tutorial and scrolling through stackoverflow to great frustration. To get to a reasonable stopping point where I felt it was presentable, it probably took me three weeks in total (including content creation etc).

Contrast that experience to this website which I built using Hugo - which took me three days with no tutorial, no instructions, just Github Copilot. I was able to customize an existing [theme](https://themes.gohugo.io/themes/archie/), streamline the deployment process with with Github actions and also add fun little elements like the [Typed.JS](https://mattboldt.com/demos/typed-js/) animation on the homepage. 

Over the last six weeks, I've built eight prototypes starting with basic scripts and culminating in a full stack news summarization app that used reinforcement learning with human feedback, a React front end, python backend, a SQL database and integrations with several external APIs including NewsAPI and OpenAI. See my posts [Three ways I played with OpenAI's APIs]({{< relref "/projects/ThreeWaysLLMs/index.md" >}}) and [Experiments in Supervised and Reinforcement Learning]({{< relref "/projects/LearningExperiments/index.md" >}}). 

My only tools were 1. `curiosity`, 2. `patience` and 3. `healthy skepticism`. I've already written about curiosity above. Patience is required to iterate through a prompt and its generated response until you achieve what you're looking for. The healthy skepticism is required to ensure you don't blindly follow GPT's instructions because it does make mistakes and can lead you astray.

# Treat Prompting like a Game 

This is how I started my conversations with GPT for my website and each of my projects. Each of these steps builds critical context for it to help you move forward into the next step.

- Step 1: Prompt GPT to brainstorm with you. In all of my projects, I would start with a vague idea ("I want to build a X"). During this phase, I will prompt GPT to ask me follow up questions, one at a time to help me flesh out my goals and ideas. Through this process, you are building context for it to provide more recommendations later in the dialogue. 
- Step 2: Create a product spec (or a requirements document) with the help of GPT that articulates the features of the project. GPT can help you brainstorm what are the most important aspects based on the context that is set from Step 1. I often will prompt GPT to help me distill or prioritize which are the most important requirements by giving it more context (like is this a project for personal learning or not etc)
- Step 3: Prompt GPT to help you create a tech spec. As part fo this process, you will need to give it some more context about your technical know-how, time commitment and also whether this app is a proof of concept. During this phase I would often iterate with GPT by asking it to simplify certain aspects of this recommendation by reminding it of my learning goals. Or I might ask it to give me several implemenation options and tell me the pros and cons of each to help me decide which direction. 
- Step 4: Ask it to help you decide where to start and provide a plan of steps. With a tech spec in hand. I would then prompt GPT to help me figure out where is the best place to start. For example with the Reinforcement Learning app, it suggested that we first start learning how Q-learning (a RL algorithm) works with fake data. This was a critical first step for me because it provided a foundational understanding of the model.
- Step 5: For each new step, I would always try to provide the context of the prior one. 

Initially I used Replit (and copy/pasted between GPT for help writing and debugging code). I've since moved to using Visual Studio Code to access Github Copilot directly in the interface.

**A few additional observations**
- GPT rarely gets it right the first time. There is still a significant amount of debugging - but GPT guides you through this process.
- GPT will hallucinate. For example, it once hallucinated about an API endpoint that didn't exist. I didn't realize this until lots of troubleshooting and then finally reading the official documentation. Increasingly, I will paste in documentation from external websites to make sure it provides me valid answers.
- GPT has to be constantly reminded of its context. As my prototypes got more complex involving multiple files and modules, I would have to remind GPT about the existence of these modules. 

 