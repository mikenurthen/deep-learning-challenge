# deep-learning-challenge
## Module 21 Challenge

## Analysis
The purpose of this analysis was to create a deep learning neural network that could help identify which applicants for funding would have the great change of success. I used the features provided in the sample dataset to create a binary classifier that can predict whether applicants will be successful if funded by the fictitious company Alphabet Soup.

From Alphabet Soup’s business team, you have received a CSV containing more than 34,000 organizations that have received funding from Alphabet Soup over the years. Within this dataset are a number of columns that capture metadata about each organization, such as:

- EIN and NAME - Identification columns
- APPLICATION_TYPE - Alphabet Soup application type
- AFFILIATION - Affiliated sector of industry
- CLASSIFICATION - Government organization classification
- USE_CASE - Use case for funding
- ORGANIZATION - Organization type
- STATUS - Active status
- INCOME_AMT - Income classification
- SPECIAL_CONSIDERATIONS - Special considerations for application
- ASK_AMT - Funding amount requested
- IS_SUCCESSFUL - Was the money used effectively

### Data Preprocessing
  - What variable(s) are the target(s) for the model?
    - y = application_df["IS_SUCCESSFUL"].values
  - What variable(s) are the features for the model?
    - The features for the model are all columns minus "IS SUCCESSFUL" column.
  - What variable(s) should be removed from the input data because they are neither targets nor features?
    - Column "EIN" should be removed as it provides no insight into predicatability of a successful funding venture.

### Compiling, Training, and Evaluating the Model
- How many neurons, layers, and activation functions were selected for your neural network model, and why?
  - I first selected 2 hidden layers, but could not get the model to achieve an accuracy higher than 72%:
  ![image](https://github.com/mikenurthen/deep-learning-challenge/assets/125414655/c831bb2d-cf12-4851-9866-4ae636da1357)
  ![image](https://github.com/mikenurthen/deep-learning-challenge/assets/125414655/c46ce0db-8d34-4626-ada4-197cd23ced7c)

  - I then added a 3rd hidden layer, while increasing the number of neurons in each layer.
 
- Were you able to achieve the target model performance?
  - Yes, I was able to achieve 75% target accuracy and brought that up to 79%:
  ![image](https://github.com/mikenurthen/deep-learning-challenge/assets/125414655/f719b0e0-49a6-41ee-827b-c6468ff347a2)

- What steps did you take in your attempts to increase model performance?
  - Critical to achieveing a model accuracy above 75% was reintroducing the "NAME" column that was originally dropped form the DataFrame. Then, similar to "APPLICATION_TYPE" and "CLASSIFICATION", I collapsed infrequent values into a single category called "OTHER." These infrequent values turned out to be organization names which appeared less than 6 times in total, which turned out to be 19,214 organizations:
  ![image](https://github.com/mikenurthen/deep-learning-challenge/assets/125414655/f281e3e5-8ea5-4398-ade8-d159a9b7f4bb)<br>
  - "NAME" turned out to be a critical feature to retain for the model to learn that the number of times an organization appeared to apply for funding played a contributing factor into whether or not they were successful. as the model had more information in which to place greater weight upon that particular feature than it could when the feature had been omitted.
With this model carrying 398 input features, it generally found best to use 2-3 times as many neurons as there are input features, I added 800 neurons to my first layer, with less neurons for subsequent layers.
First, I emplored 800, 400, 400 respectively for the first, second, and third hidden layer. This model achieved 78.79% accuracy:
  ![image](https://github.com/mikenurthen/deep-learning-challenge/assets/125414655/dfdc26df-0182-4f08-9e50-75bcb658b947)

  - I then significantly reduced the number of neurons in the second and third hidden layers, and the model improved, albeit nominally, to 79.04%:    
  ![image](https://github.com/mikenurthen/deep-learning-challenge/assets/125414655/5b614e95-889a-441d-a542-f20c835787fa)
  ![image](https://github.com/mikenurthen/deep-learning-challenge/assets/125414655/336748b4-d23b-4dae-8fc8-0fada9993110)

  - What I found most important was for the first layer to include a greater number of neurons, with subsequent layers being less important. The majority of weight calculations seemed to take place in the first layer.
