# Assessing the Difficulty of Trivia Questions
![people playing trivia](images/Transit_Trivia_Night_(12240726723).jpeg)
*photo courtesy of Wikimedia Commons*
## Goal
Build a regression model to predict the level of difficulty of trivia questions using Jeopardy! clues.  

## Business Objective
Trivia events have grown in popularity in recent years. Odds are you can find a bar or restaurant nearby that hosts trivia nights most days of the week. These events bring in diners and drinkers to establishments on nights that are otherwise slow. In return, the hosting facility typically pays a fee to a trivia company to put on the event.

Trivia events have become big busines in recent years, with a number of companies providing trivia services [locally and nationally](https://triviabliss.com/trivia-night-companies-us/). The pandemic initially put a damper on these events, but they were soon adapted to online platforms such as Zoom. Even Netflix has gotten in on the trivia trend, with a daily interactive trivia game being launched on their streaming service in [April 2022](https://www.nytimes.com/2022/03/03/crosswords/history-trivia-netflix.html).

There's an art to crafting a successful trivia event. The questions can't be too easy, or people will become bored. They also can't be too difficult, or people will disengage. There needs to be a mixture of easy, medium, and hard questions in order for participants to experience both successes and stumbles. This can be hard to achieve since the perceived difficulty of questions can be highly subjective.

That's why I created a model using natural language processing to assess the level of difficulty of trivia questions. This will help ensure that your trivia events hit the sweet spot where players are appropriately challenged, stay engaged, and have a good time.

## Data Source
I used question from Jeopardy to train my models. The data set is a .tsv file that can be found on [Github](https://github.com/jwolle1/jeopardy_clue_dataset), contributed by a source who chooses to remain anonymous. 

The data set includes 389,445 questions from Jeopardy! shows that aired between 1984-2021. In addition to question and answers, the variables include the round in which the question appeared (Jeopardy! or Double Jeopardy!), the dollar value of the question, if the question was a Daily Double, the question’s category, any comments the host made about the question, the air date, and any special notes about the question (ie., if the show was a special tournament). There are 47,752 unique categories to which the questions are assigned.

### Data Cleaning
In 2001, all clue values were doubled for both the Jeopardy! and Double Jeopardy! rounds. This meant that questions that were valued at $100 became $200, $200 questions became $400 questions, etc. In order to normalize the data, I converted all pre-2001 clue values to their 2001 equivalencies, so that all questions were valued at $200, $400, $600, $800, and $1000 for the first-round questions and $400, $800, $1200, $1600, and $2000 for the second-round ones. To do this, the ‘air date’ column had to first be converted from an object to a date-time type variable.

I also removed questions that were Daily Doubles, since the contestants determined their own wagers for those questions. I also removed Final Jeopardy! questions for the same reason. This left 363,765 questions to use for modeling.

### Natural Language Processing Cleaning and Feature Engineering
To prepare the data for machine learning, punctuation was removed and the text of the questions and answers were made lowercase. Numerals were also removed. The text from the questions and answers were combined into a new category in order to increase the data that the model could use. This ‘q_and_a’ category was tokenized and lemmatized.

##  Modeling and Evaluation
This project could be approached as a classification problem, assigning questions to easy, medium, and difficult categories. I decided to tackle it as a regression problem since the outcome variable represented real values.

There are $400 and $800 clue value amounts that appear in both the first and second rounds of game play. The relative difficulty of the question assigned to these values shifts between rounds. For example, in Round 1 an $800 dollar question is one of the harder questions, whereas in Round 2 an $800 question is considered to be an easier type of question. Unsure how this would affect my models, I decided to run them on data where all the questions are together, regardless of round, and also run them on data where the Round 1 and Round 2 questions are separated. 

To do so, I first converted the text to a matrix using a vectorizer. I chose first to use the Tfidf Vectorizer to determine the relevance different words have to the questions’ level of difficulty. I created 9 different Tfidf Vectorizers with different parameters and tested each on a untuned models to see which performed the best in regards to error rate and computation time. This varied based on type of model. For example, the linear regression model worked best when stop words were removed and uni-, bi-, and trigrams were included. This, however, created over 3 million features, which wouldn’t be efficient for tree-based models. For those, I added a parameter that limited maximum features to 150,000 or fewer.

Doc2Vec was also used to see if taking documents (the words in questions and answers) as a single unit would improve model performance more than examining words individually (or bigrams/trigrams). Stanford’s Global Vectors for Word Representation (GloVe) (LINK for  https://nlp.stanford.edu/projects/glove/) was utilized to train semantic relationships.

I ran the following models on the data set:
-	Linear Regression
-	Ridge Regression
-	Random Forest Regressor
-	Linear Support Vector Regression
-	Gradient Boosting
-	Neural Network
-	Linear Support Vector Regression using Doc2Vec

For each of these models, the data was tested with the questions all together and with the questions divided by round. In cases where hyperparameter tuning was needed, I used the Halving Random Search Cross Validation, which provided significantly better computation times than Randomized Search.

The models were evaluated using mean absolute percentage error (mape), which gives the average difference between the predicted value and the actual value of the Jeopardy questions. Because it's an error in percentage, it's not relative to the size of the numbers in the data, which allows comparison between the smaller values in the Jeopardy! round to the larger values in the Double Jeopardy! round.

In all cases, the models performed best when the rounds were separated. This lends support to the hypothesis that overlapping values between the rounds makes it more difficult for models to predict the question value. The best model was the neural network:
1.	For both rounds together:
    -	 The validation set had a mape of 51%; the test set had a mape of 51.3%
2.	With rounds separated:
    -	For Round 1, the validation set had a mape of 50%; the test set had a mape of 50.8%
    -	For Round 2, the validation set had a mape of 50.1%; the test set had a mape of 53.1%

## Conclusion and Next Steps
With the best model having a 50.4% average difference between predicted and actual question values, there remains room for improvement. Language is incredibly nuanced, and word choice is likely just one of many factors that affect the level of difficulty of trivia. Focusing on word count and word relations appear to have some predictive influence on category value, but other variables remain uncaptured by the models presented here.

Going forward, there are a few different options to try to improve the model's performance:
-	Take into account questions that were missed by contestants and use that as a metric of difficulty (such as the so-called triple stumpers, where no contestants answered correctly)
-	Use topic modeling to see if question difficulty is tied to domain
-	Compare and contrast trivia questions with other type of questions that require more than memory recall, such as analyzing and evaluating information

#### For more information
Please contact: 
[Sally Heinzel](mailto:seheinzel@gmail.com) 

Check out the full [Jupyter notebook](NEW LINK https://github.com/snakeeyes021/flu-shot-learning/blob/main/Combined%20Notebook.ipynb) and the [presentation](NEW LINK https://github.com/snakeeyes021/flu-shot-learning/raw/main/Boosting%20Vaccination%20Rates%20Presentation.pdf).

Reproduction instructions (or a link to them)

**Repository Structure:**
```
├── data                                   <- Sourced externally
├── images                                 <- Both sourced externally and generated from code 
├── .gitignore                             <- gitignore      
├── README.md                              <- The top-level README for reviewers of this project
├── Presentation.pdf                       <- PDF version of project presentation
├── app.py                                 <- ViaGoGo streamlit application back-end
└── index.ipynb                            <- Narrative documentation of analysis and modeling

```
