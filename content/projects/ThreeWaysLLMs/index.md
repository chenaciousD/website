---
title: "Three ways I played with OpenAI's APIs"
date: 2023-11-01T02:01:58+05:30
description: "LLM ideas"
image: "Chat.png"
---

## My motiviation behind these experiments
I was curious about the hype around GenAI so I wanted to play with the technology firsthand. Here are a few examples of what I created. Each of these applications was built with the assistance of GPT or Github Copilot. 

## Learn that Law: An Example of Retrieval Augmentation Generation 
My first project was to build a simple [RAG](https://stackoverflow.blog/2023/10/18/retrieval-augmented-generation-keeping-llms-relevant-and-current/) which enable users to query an external data source with natural language. At the time, OpenAI did not have the ability to store "knowledge" as it does now with custom GPTs, so if the text could not fit within OpenAI's context window, one had to use its embeddings API to store it in a external vector database. The external data source I was interested in querying was the law [SB9](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202120220SB9), a recently introduced law that was not present in the training dataset of GPT (at the time)

Here what my simple app does: 
- The external document (in this case SB9) is read, processed, and split into sections. 
- Embeddings for each section are generated using OpenAI's API and stored in [Pinecone](https://www.pinecone.io/), a vector database. 
- When a user queries the system, the closest section embeddings to the query are retrieved, and a combined response from these sections is generated. 
- This response is then sent to GPT-3, which provides a conversational summary. 
- I used a [Gradio](https://www.gradio.app/) interface to allows users to interact with this system in a user-friendly manner.

I got the system to work reasonably well but I discovered that the way the document is chunked for embeddings can have a significant impact on the quality of the retreival process.

{{< figure src="SB9Law.png" title="Example query using Gradio interface" >}}

## To Do or Not to Do: Experimenting with Classification
My second project was inspired by note taking and task lists. Often when I'm away from my computer in a social setting, a thought or a task may come to me that I want to capture and come back to at the end of the day. However, each thought or task might need to be handled in a different way based on priority, objective, topics. My concept was to create a virtual assistant that sifts through messages sent over text and employs GPT to understand, categorize, appropriately respond and take action on the message. Here's how it works:

- A user sends a message, which is stored in an Airtable table. 
- At regular intervals, the application's scheduler triggers the check_for_new_messages function. 
- When a new message is found, the application uses the OpenAI GPT-4 model to classify the message into categories such as PriorityType, TopicType, and ActionType.
- After classifying the message, the application uses GPT-4 again to generate a relevant response based on the user's original message and respective classification type
- The application then formats an email, incorporating the original message, its classification, and the generated response. 
- The application compiles and sends an individual digest of messages and responses to each user. The user receives this formatted email via SendGrid, a cloud-based email delivery service. The email contains the classification details and the AI-generated response.

{{< figure src="Intern.png" title="A request categorized as research and the generated response" >}}

A challenge that I ran into on this project was the unpredictability of the generated response. Sometimes it would generate a response in prose and other times it would generate a response with a bulleted list. This unpredictability caused some issues downstream when I tried to format it into an email. Ultimately, the simplest solution I came up with was to modify the prompt to create a more predictable output. 

## ... A block away: An Example of Personalization, Prompting and Function Calling 
This experiment was inspired by a friend of mine who constantly would text me for recommendations based on very specific locations - real-time. What if you could share your location with an agent to help you find places to discover - real time with natural language?

Most recommendation engines use what's known as collaborative filtering or content-based filtering to determine recommendations. However, they require a lot of data from the user in the form of explicit user preferences. In this experiment, I took a shortcut and used GPT to provide meaningful recommendations by allowing the user to enter a snippet of useful context to help it rank the results returned from the Google Search API. This is how it works: 

- When a user shares their current location (latitude and longitude), specifies the type of place they're interested in, and sets a distance limit, the app processes this information using GPT. For instance, it can understand statements like "I want to find a nearby coffee shop" and determine both the desired place type (e.g., restaurant, cafe) and the preferred search radius (from "walking distance" to a specific number of meters).
- To streamline this information, the app utilizes OpenAI's function calling to create a JSON format containing the identified PlaceType and Radius. This JSON is then used to intelligently call the Google Places Nearby search API.
- The app's backend interacts with the Google Places API to fetch results that match the user's query for nearby locations.
- Subsequently, the app sends an SMS to the user, requesting additional context to refine the search. Users can provide any relevant information they think might be helpful, such as "I'm with my family" or "I'm an architect."
- The backend employs OpenAI's GPT to personalize recommendations based on the user's context. It generates a response with a rationale and sends it back to the user via SMS.

{{< figure src="Place-recommender.jpeg" title="Sample Natural Language Conversations" >}}
