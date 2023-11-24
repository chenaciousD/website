---
title: "Experiments in supervised and reinforcement learning"
date: 2023-04-01T02:01:58+05:30
description: "An AI car designed to build a relationship between car and driver"
---

# Why I did this experiments
After reading the [Alignment Problem](https://brianchristian.org/the-alignment-problem/) and taking a deep learning class from [fast.ai](https://course.fast.ai/). I was inspired to get some exposure to some of the various methods of supervised learning and reinforcement learning. 

## Training my own Neural Net 

The goal for me was to see an end-to-end machine learning workflow. I used the FastAI library for its ease of use. I found a dataset available from [Harvard](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/IGNELZ). The Annotated Image Database of Architecture is comprised of about 15,000 images that are pre-labeled across various categories including building type and location. The images were sourced originally from [Archdaily](https://www.archdaily.com/), an architecture blog.

- The workflow started with loading and processing image filenames and labels for training, validation, and testing. 
- I created pandas DataFrames to organize the datasets. For model training and evaluation, it sets up DataLoaders with the necessary image transformations. 
- I used a a convolutional neural network model, using the ResNet50 architecture, is then initialized and trained, with the learning rate optimized through FastAI's utilities. 
- After training the model, I evaluated the performance on the validation datasets. 

{{< figure src="ImageClassifier.png" title="Sample images with respective categories in numerical form" >}}

I test the resulting model with some of my own images to see how well it performed, anecdotally. 

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

## Building a Reinforcement Learning Algorithm 
MORE TO COME - DRAFT CONTENT

A news reading experience that learns your preferred level of summarization based on content category and context, using Q-learning. This Flask web application is a sophisticated news content aggregator and distributor, integrating OpenAI's GPT-3 and NewsAPI for dynamic content handling. It fetches, processes, and serves news articles, optimizing its actions based on user feedback and reinforcement learning. The core mechanism involves fetching news from various categories, extracting content, and storing it with a 'served' status. An 'Agent' then selects actions, like generating headlines or summaries, based on the current state, which considers time, category, and user interactions. This Agent uses an epsilon-greedy policy for decision-making, striking a balance between exploring new actions and exploiting known successful ones. User feedback plays a crucial role in refining the system's learning, as it updates Q-values to enhance future content relevance and effectiveness. This design allows the app to adapt over time, offering a responsive and evolving experience in news content delivery.

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
