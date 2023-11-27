+++
title = 'Curiosity is all you need: How GenAI will transform creativity'
date = 2023-11-22T18:54:38-08:00
draft = false
description = "Blah blah blah"
+++

# Anyone can create

`GenAI will dramatically reduce the barriers to creativity.` I'm not referring solely to creativity within professional fields like design and art, although it will undoubtedly have a substantial impact there as well. What I mean is creativity in its broadest sense—the act of envisioning and bringing an idea to life, your own idea, independently. 
  
# Curiosity is all you need

For me, GPT has sparked a new enthusiasm and energy for learning and creation. Any topic, any thread, any thought, any idea has the potential to be realized if you are curious enough to see it through. Although I specifically used GPT to help me build software, I also believe that this trend will permeate other industries too.

In high school, I was given a science award for being the most inquisitive. I would often annoy teachers with my questions - some of which were dumb, sometimes repetitive, and perhaps distracting - but they were an essential part of the way I learned. My questions were my brain trying to form and validate my mental model of a concept. GPT is a teacher with limitless energy. It doesn't judge, it comes along with you on your learning journey and it never tires. Here are a few ways I have prompted GPT to help me understand an idea: 
1. Ask it to provide an example(s) (a simple tactic that can you can easily continue to modify to simpler and simpler examples)
2. Ask it to create an analogy or metaphor (GPT helped me understand the difference between policy driven and reward driven reinforcement learning algorithms through the lens of cooking)
3. Ask it to explain the context or framework in which this concept is situated. (a strategy I often use when I'm trying to assess the scope and depth of the concept)
4. Ask it to validate or build on a partially-formed hypothesis (a tactic that I use when the picture is beginning to clear but I need better language to articulate it; sometimes I use the tactic "complete this sentence" where I leave an ellipsis for GPT to fill in)
5. Give more context about yourself (this one's self-explanatory — tell GPT more about why you're learning and any relevant information about yourself, so it can tailor its response).

# From three weeks to three days

As an example of how different it is for a non-technical person to create something now compared to the pre-GenAI era: In 2019, I built my personal website using Gatsby, following a step-by-step tutorial and browsing Stack Overflow, which was often frustrating. It took me approximately three weeks to reach a point where I felt it was presentable, including content creation.

Contrast that experience to this website which I built using Hugo - which took me three days with no tutorial, no instructions, just Github Copilot. I customized an existing [theme](https://themes.gohugo.io/themes/archie/), streamlined the deployment process with with Github actions and also added fun little elements like the [Typed.JS](https://mattboldt.com/demos/typed-js/) animation on the homepage. 

Over the past six weeks, I've developed eight prototypes, starting with basic scripts and culminating in a full-stack news summarization app that utilized reinforcement learning with human feedback, a React frontend, a Python backend, an SQL database, and integrations with several external APIs, including NewsAPI and OpenAI. See my posts [Three ways I played with OpenAI's APIs]({{< relref "/projects/ThreeWaysLLMs/index.md" >}}) and [Experiments in Supervised and Reinforcement Learning]({{< relref "/projects/LearningExperiments/index.md" >}}). 

My tools were `curiosity`, `patience` and `healthy skepticism`. I've already written about curiosity above. Patience is required to iterate through a prompt and its generated response until you achieve what you're looking for. The healthy skepticism is required to ensure you don't blindly follow GPT's instructions because it does make mistakes and can lead you astray.

# Prompting a Process

For each of my projects, I took a similar process. Each of these steps builds critical context for it to help you move forward into the next step.

- Brainstorm: Begin by generating a basic idea for your project, such as "I want to create X." During this phase, engage with GPT to ask you follow-up questions one at a time to help you develop your project goals and ideas. This process establishes the context necessary for GPT to offer more relevant recommendations in subsequent discussions.
- Define: Collaborate with GPT to create a product specification or a requirements document that outlines the project's features. GPT can assist you in distilling the most critical aspects based on the context established in Step 1. You can also prompt GPT to help you prioritize these requirements by providing additional context.
- Spec: Use GPT to assist you in generating a technical specification. In this phase, provide GPT with information about your technical expertise, time commitment, and whether the project serves as a proof of concept or needs to be more scalable. During this step, you may iterate with GPT by asking it to simplify certain aspects of its recommendations, reminding it of your learning goals, or requesting multiple implementation options with their respective pros and cons to aid in your decision-making.
- Plan: Seek GPT's guidance in determining where to begin and formulating a plan. For example, when I was working on my Reinforcement Learning app, GPT  suggested starting by learning the basics of Q-learning (a reinforcement learning algorithm) with dummy data. This initial step was essential for me to learn the foundations. 
- Implement: Through purely natural language prompting, you can start to build you app by copying and pasting the code that GPT generates into your IDE. Initially I used Replit (and copy/pasted between GPT for help writing and debugging code). I've since moved to using Visual Studio Code to access Github Copilot directly in the interface.
- Continuously provide context from the previous steps as you proceed to each new step in your project. This ensures that GPT remains informed and can offer relevant assistance at each stage.


**A few additional observations**
- GPT rarely gets it right the first time. There is still a significant amount of debugging, but GPT guides you through this process.
- GPT will hallucinate. For example, it once hallucinated about an API endpoint that didn't exist. I didn't realize this until lots of troubleshooting. Increasingly, I will pass documentation from external websites to make sure it provides me valid answers.
- GPT has to be constantly reminded of its context. As my prototypes got more complex involving multiple files and modules, I would have to remind GPT about the existence of these components. 

 