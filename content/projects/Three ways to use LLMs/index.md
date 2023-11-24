---
title: "Four ways to use LLMs"
date: 2023-04-01T02:01:58+05:30
description: "An AI car designed to build a relationship between car and driver"
---

Over a period of a few weeks, I play with OpenAI's APIs to prototype various applications. Here are a few examples of what I created. Each of these applications were built with the assistance of GPT. Note I have no engineering expertise. See my other post.

### Learn that Law: An Example of Retrieval Augmentation Generation 
My first project was to build a simple [RAG](https://stackoverflow.blog/2023/10/18/retrieval-augmented-generation-keeping-llms-relevant-and-current/) which is the basis of many LLM use cases that promise users to be able to query an external data source with natural language. At the time, OpenAI did not have the ability to store "knowledge" as it does now with custom GPTs, so if the text could not fit within OpenAI's context window, one had to use its embeddings API to store in a vector database. The external data source I was interested in querying was the law [SB9](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202120220SB9), a recently introduced law that was not present in the training dataset of GPT (at the time)

Here what my extremely simple app does: 
- The external document (in this case SB9) is read, preprocessed, and split into sections. 
- Embeddings for each section are generated using OpenAI's API and stored in [Pinecone](https://www.pinecone.io/), a vector database. 
- When a user queries the system, the closest section embeddings to the query are retrieved, and a combined response from these sections is generated. 
- This response is then sent to GPT-3, which provides a conversational summary. 
- I used a [Gradio](https://www.gradio.app/) interface to allows users to interact with this system in a user-friendly manner.

{{< figure src="SB9Law.png" title="Example query using Gradio interface" >}}

### To Do or Not to Do: Experimenting with Classification
Often when I'm away from my computer - in a social setting, a thought or a task may come to me that I want to capture and come back to at the end of the day. However, each thought or task might need to be handled in a different way based on priority, objective etc. So the concept here was to create a virtual assistant, sifting through messages sent over text and employing GPT to understand, categorize, appropriately respond and then one day (take action) the message. Here's how it works:

- User Submits a Message: A user sends a message, which is stored in the Airtable 'Messages' table. 
- Scheduled Message Check: At regular intervals, the application's scheduler triggers the check_for_new_messages function. 
- Message Classification: When a new message is found, the application uses the OpenAI GPT-4 model to classify the message into categories such as PriorityType, TopicType, and ActionType.
- Generating a Response: After classifying the message, the application uses GPT-4 again to generate a relevant response based on the user's original message and the classification type
- Formatting the Email: The application then formats an email, incorporating the original message, its classification, and the generated response. 
- Sending the Email Digest: The application compiles and send an individual digest of messages and responses to each userThe user receives this formatted email via SendGrid, a cloud-based email delivery service. The email contains the classification details and the AI-generated response.

{{< figure src="Intern.png" title="A request categorized as research and the 'Intern's generated response" >}}

### ...Block Away: An Example of Contextualized Recommendation
This experiment was inspired by a friend of mine who constantly would text me for recommendations based on very specific locations - real-time. So the concept was what if you could share your location with an agent to help you find places to go to and discover - real time. 

How could LLMs  be used to provide personalized recommendations based on very limited user input? Most recommendation engines use what's known as collaborative filtering or content-based filtering to determine recommendations. However, they alot of data from the user in the form of explicit user preferences. In this experiment, I took a shortcut and use GPT to provide meaningful recommendations by allowing the user to enter a snippet of useful context to help it rank the results returned from the Google Search API. This is how it works: 
- Sends/Receives SMS: Integrates Twilio API for SMS communication.
- Fetches Place Recommendations: Uses Google Places API to retrieve nearby location suggestions.
- Processes User SMSs with GPT-3: Uses OpenAI's GPT-3 to extract entities. Interprets natural language input like "I want a coffee shop a few blocks away". GPT-3 analyzes this text to identify the type of place the user is interested in (like a restaurant, cafe, etc.) and the preferred search radius (like "walking distance" or a specific number of meters) to form a query to Google Places Nearby search API
- Sends return SMS to user asking for more context: To help provide context to GPT, the user can enter anything they think might be useful in helping refine the search results (i.e., "I'm with my family; I'm an architect" etc)
- Ranks Recommendations: Employs OpenAI's GPT-3 for personalizing recommendations based on user profiles.
- Manages User States: Tracks and updates the progression of user interactions.

{{< figure src="Place-recommender.jpeg" title="Sample Natural Language Conversations" >}}

### Function Calling 
The script integrates OpenAI's GPT-3 model with the OpenWeatherMap API to provide weather-based conversational responses. The get_current_weather function fetches the current weather for specified coordinates. In the run_conversation function, an initial conversation with the GPT-3 model is initiated about the weather in Hong Kong. GPT-3 is expected to return the coordinates for Hong Kong, which are then used to fetch the weather data. The weather data, along with the model's response, is passed back to GPT-3 for a final conversational message. When the script runs, it initiates this conversation flow and prints the resulting conversation.