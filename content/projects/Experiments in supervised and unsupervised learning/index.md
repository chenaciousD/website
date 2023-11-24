---
title: "Experiments in supervised and reinforcement learning"
date: 2023-04-01T02:01:58+05:30
description: "An AI car designed to build a relationship between car and driver"
---

DRAFT COMING

### Why I did this experiments
Bacon ipsum dolor amet pork chop pancetta ball tip, turkey bresaola landjaeger flank sausage. Prosciutto beef ribs pork belly, hamburger ham hock brisket bacon boudin.

{{< figure src="ImageClassifier.png" title="Sample images with one-hot encoding" >}}

### Training my own Neural Network 
I used Google Colab and Jupiter Notebook and used a dataset from Archdaily to train a neural network to predict a building type based on an image. 
I used fast.AI’s library to create datablocks. 
Part of this was to take the categorical data and transform it into numericals - and then associate it with an image. 
I then split the dataset into a training dataset and a validation data set. 
I used Resnet50 which is a convolutional neural network.

{{< highlight python >}}
def train_model():
learn = cnn_learner(train_dls, resnet50, metrics=accuracy)
learn.lr_find()
learn.fit_one_cycle(10, lr_max=1e-3)
{{< /highlight >}}


### Building a Reinforcement Learning Algorithm 
A news reading experience that learns your preferred level of summarization based on content category and context, using Q-learning. 
This Flask web application is a sophisticated news content aggregator and distributor, integrating OpenAI's GPT-3 and NewsAPI for dynamic content handling. It fetches, processes, and serves news articles, optimizing its actions based on user feedback and reinforcement learning. The core mechanism involves fetching news from various categories, extracting content, and storing it with a 'served' status. An 'Agent' then selects actions, like generating headlines or summaries, based on the current state, which considers time, category, and user interactions. This Agent uses an epsilon-greedy policy for decision-making, striking a balance between exploring new actions and exploiting known successful ones. User feedback plays a crucial role in refining the system's learning, as it updates Q-values to enhance future content relevance and effectiveness. This design allows the app to adapt over time, offering a responsive and evolving experience in news content delivery.

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
