---
title: "Four ways to use LLMs"
date: 2023-04-01T02:01:58+05:30
description: "An AI car designed to build a relationship between car and driver"
---

DRAFT COMING!

### Retrieval Augmentation Generation 
A system for users to query a document (named 'SB9.txt') and receive summarized answers about its content, leveraging both embeddings and GPT-3. Initially, the document is read, preprocessed, and split into sections. Embeddings for each section are generated using OpenAI's API and stored in Pinecone, a vector database. When a user queries the system, the closest section embeddings to the query are retrieved, and a combined response from these sections is generated. This response is then sent to GPT-3, which provides a conversational summary. Lastly, a Gradio interface allows users to interact with this system in a user-friendly manner.

### Text Classification 
This Flask application acts as a virtual executive assistant for users, diligently sifting through messages stored in Airtable. Once a user submits a message, the application employs the intelligence of OpenAI's GPT-4 model to understand and categorize the message based on its priority, topic, and required action. But the assistant doesn't stop there. It further crafts an insightful response to the message, ensuring the user receives valuable feedback. To keep the user in the loop, the application sends a neatly formatted email, summarizing the message's classification and the generated response. The assistant ensures no message is left unattended by continuously checking for new messages and processing them. So, whether a user is seeking guidance on a work project or needs advice on a personal matter, the assistant is always at the ready, making sure every query is answered promptly and efficiently.

### Recommendation
Uses Google places API provides recommendations by comparing context with the returned search results 
Had issues with a consistent json output; had to really be specific in prompting 
Bacon ipsum dolor amet pork chop pancetta ball tip, turkey bresaola landjaeger flank sausage. Prosciutto beef ribs pork belly, hamburger ham hock brisket bacon boudin.

{{< figure src="Place-recommender.jpeg" title="Sample Natural Language Conversations" >}}

### Function Calling 
The script integrates OpenAI's GPT-3 model with the OpenWeatherMap API to provide weather-based conversational responses. The get_current_weather function fetches the current weather for specified coordinates. In the run_conversation function, an initial conversation with the GPT-3 model is initiated about the weather in Hong Kong. GPT-3 is expected to return the coordinates for Hong Kong, which are then used to fetch the weather data. The weather data, along with the model's response, is passed back to GPT-3 for a final conversational message. When the script runs, it initiates this conversation flow and prints the resulting conversation.