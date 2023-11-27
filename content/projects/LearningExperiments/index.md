---
title: "Experiments in supervised and reinforcement learning"
date: 2023-04-01T02:01:58+05:30
description: "An AI car designed to build a relationship between car and driver"
---

## My motivation behind these experiments
After reading the [Alignment Problem](https://brianchristian.org/the-alignment-problem/) and taking a deep learning class from [fast.ai](https://course.fast.ai/). I was interested in learning how some of the learning methods worked in practice. 

## Training my own Neural Net 

My goal was to see an end-to-end machine learning workflow. I used the FastAI library for its ease of use. I found a dataset available from [Harvard](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/IGNELZ). The Annotated Image Database of Architecture is comprised of about 15,000 images that are pre-labeled across various categories including building type and location. The images were sourced originally from [Archdaily](https://www.archdaily.com/), an architecture blog.

- The workflow started with loading and processing image filenames and labels for training, validation, and testing. 
- I created pandas DataFrames to organize the datasets. For model training and evaluation, it sets up DataLoaders with the necessary image transformations. 
- I used a convolutional neural network model, using the ResNet50 architecture, which is then trained, with the learning rate optimized through FastAI's utilities. 
- After training the model, I evaluated the performance on the validation datasets. 

{{< figure src="ImageClassifier.png" title="Sample images with respective categories in numerical form" >}}

I tested the resulting model with some of my own images to see how well it performed, anecdotally. 

| Image | Predicted Class | Model Performance |
|-------|-----------------|----------|
| david_baker_apt.png | Apartments | Correct |
| SFO.png | Mixed Use Architecture | Correct |
| sightglass.png | Restaurants & Bars | Correct |
| sfmoma.png | Apartments | Incorrect |
| seagrambuilding.png | Office buildings | Correct |
| levisstadium.png | Institutional buildings | Incorrect |
| bar_agricole.png | Office buildings | Incorrect|
| Danish_kindergarten.png | Apartments | Incorrect |
| tennis_stadium.png | Schools | Incorrect|
| Art_Gallery.png | Churches | Incorrect|
| Asplund_library.png | Library | Correct |
| Opera_house.png | Cultural Architecture | Correct |
| whiskybar.png | Restaurants & Bars | Correct |
| SFO_interior.png | Schools | Incorrect |
| columbia_school_of_business.png | Office buildings | Incorrect|
| everlane_sf.png | Store | Correct |
| lumina_sf.png | Housing | Correct |
| sfo with plane.png | Public Architecture & Space | Incorrect|
| office interior.png | Offices | Correct |

As you can see in the above table, my model didn't have the greatest accuracy. I wasn't able to achieve more than 50% accuracy based on the validation dataset. A significant takeaway from this exercise was the importance of the quality of training data. MORE TO COME.

## Building a Reinforcement Learning with Human Feedback Algorithm 

RLHF is a type of machine learning where the system learns to make decisions by taking actions and receiving feedback from the user in various situations. The core concepts are:
- `agent/system` the decision maker
- `environment` the interaction space of total possible states that the agent can face
- `actions` the things that the agent can do
- `states` the specific configurations of the environment 
- `rewards` the feedback that the system might receive from taking action in a state 
-`policy` how the system decides which action to take in a given state

I applied these concepts to create an adaptive news summarization system. My idea was that, depending on the time of day and the topic, users might prefer different styles of news reading experiences. For instance, in the morning, users might prefer brief summaries, while in the evening, they might be more inclined to read longer articles. Preferences could also vary based on the topic, with some topics warranting concise summaries and others requiring more in-depth coverage.

In this system, my "agent" determines the appropriate level of news detail to provide based on several factors, including the time of day, the day of the week, and the topic. Users can then offer feedback in the form of positive, negative, or neutral responses. I use this feedback to create a reward function, which the agent employs to update its understanding of the user's preferences. This ensures that the agent can make better decisions the next time it encounters a similar situation. I've implemented the reinforcement learning algorithm known as q-learning to drive this process.

**Here's how it works:**
- The backend periodically fetches new articles from [NewsAPI](https://newsapi.org/docs/endpoints/top-headlines).
- The user requests to read an article via a react front end by hitting my backend's `/get_content` endpoint
- I capture the state (i.e., time of day, day of week, and then also the topic of the next article available for serving)
- The Agent processes the state to determine the best possible summarization action to take on the article (this is done through a q-lookup table)
- Based on the decision, it takes the summarization action on the article 
- THe user receives the article in the front end. The backend marks the article as served in the database to ensure that they don't get served the same article more than once
- The user provides feedback on served content (i.e., was it a good level of detail?) through the `/give_feedback` end point
- The AI agent updates the q-values in the q-table for that particular state for future reference as seen below:

{{< highlight python >}}
def process_feedback_and_update_q_value(self, content_id, state_id):
      # Fetch the latest engagement for the given content
      latest_engagement = UserEngagement.query.filter_by(content_id=content_id).order_by(UserEngagement.timestamp.desc()).first()
    
      # Calculate the reward based on user feedback
      reward = latest_engagement.calculate_reward()
    
      # Find the corresponding StateAction ID
      state_action = StateAction.query.filter_by(state_id=state_id, action_id=latest_engagement.action_id).first()
    
      # Update the Q-value for the corresponding state-action pair
      q_value_record = QValue.query.filter_by(state_action_id=state_action.id).first()
      
      if q_value_record:
        # Basic Q-value update
        alpha = 0.5  # Learning rate, adjust as needed
        reward = latest_engagement.calculate_reward()
    
        q_value_record.value += alpha * (reward - q_value_record.value)
        db.session.commit()
      else:
        print(f"No QValue found for StateAction ID: {state_action.id}")
{{< /highlight >}}

The overall process was quite interesting. As part of the definition of the learning algorithm there were a few key inputs that could have significant impact on how the algorithm behaves and the overall user experience:

1. `The Learning Rate` represents to what degree should the agent incorporate user feedback into the learning model. This can have significnat impact on the user experience. It balances the weight of new information compared to historical knowledge from prior interactions for a particular state-action pair. 
2. `The Exploration Policy` represents how much "exploration" should agent do particularly in the beginning when there is limited user data. The tradeoff between exploration (trying our new random actions just to see the user's interaction) vs exploitation (choosing the action with known rewards due to prior feedback interactions) can have significant imapact on the user experience especially during the initial learning period.
