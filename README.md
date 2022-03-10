# Capstone Proposals
## Data Set Ideas
**1.) Cornea Donor Study**
https://public.jaeb.org/cds/view/home

This is a really cool study about people who had cornea transplants and their donors. It follows up with the patients at 5 and 10 years to see if they had any complications or graft failures. There's a lot of interesting information about the donor (age, gender, tissue quality, cause of death, hours from death to preservation, etc.). I could look at different donor variables to see what best predicts transplant outcome. BUT I don't know how I could incorporate material from Phase 4. This seems more like a linear regression problem and may not be suitable for a capstone.

**1.5) Along those same lines....Organ Procurement and Transplantation Network** 
https://optn.transplant.hrsa.gov/data/view-data-reports/national-data/

This site has a lot of interesting data about different kinds of organ transplant donors/recipients nationwide. I found this at the beginning of the bootcamp and saved it as my go-to capstone data set. However, once I looked at it more, I think it's more like data reports than a database. I could maybe(?) scrape enough data to make a useful data set out of it, but I think I'd be in the same position as I am with data set #1--not sure what ML I can do with it.

**2.) 200,000+ Jeopardy! Questions** https://www.reddit.com/r/datasets/comments/1uyd0t/200000_jeopardy_questions_in_a_json_file/

Randomly came across this data set and found it intriguing. It'd be fun to work with it as if I'm helping someone who's going to be on Jeopardy prepare for the most common topics/questions/etc. But once again, I'm not sure this is capstone-worthy.

**3.) Game of Thrones Season 8–Twitter** https://www.kaggle.com/monogenea/game-of-thrones-twitter

This is a dataset of tweets during the final season of Game of Thrones (April-May 2019). I could do sentiment analysis on it to see how fans reacted to the season as it unfolded episode by episode, as well as possibly look at sentiment analysis at the character-level.



Data from here: https://github.com/jwolle1/jeopardy_clue_dataset 
This dataset contains Jeopardy! clues from Season 1 through Season 37 (August 2021). It does not contain every clue that has appeared on the show. The data source prefers not to be credited.

There are 389,445 clues in total. They can be found in combined_season1-37.tsv.

There are also individual files for each season (located in the seasons folder). These files are small enough that you should be able to open them with Microsoft Excel or Google Sheets.

Seasons 1-12 average 5,076 clues each.
Seasons 13-37 average 13,141 clues each.
There is a kids_teen.tsv file which contains only clues that appeared in Kids and Teen Tournament matches.

There is a separate goat_tournament_jan2020.tsv file which covers the Jennings-Holzhauer-Rutter event.

Note that combined_season1-37.tsv is zipped. When uncompressed it is approx. 58 MB.

I've done my best to clean the data and filter out clues that depend on images, video, or audio.

Column Information:

Label	Description
round	1 for Single Jeopardy, 2 for Double Jeopardy, or 3 for Final Jeopardy
value	The clue's value on the board. If the clue was a Daily Double, this column will be the wagered amount.
daily_double	yes or no.
category	
comments	The host's comments about a category.
answer	
question	
air_date	The calendar date on which the episode first aired.
notes	Indicates whether a clue appeared in a special match.
All data is property of Jeopardy Productions, Inc. and protected under law. I am not affiliated with the show. Please don't use the data to make a public-facing web site, app, or any other product.
#### For more information
Please contact: 
[Sally Heinzel](mailto:seheinzel@gmail.com) 

Check out the full [Jupyter notebook](NEW LINK https://github.com/snakeeyes021/flu-shot-learning/blob/main/Combined%20Notebook.ipynb) and the [presentation](NEW LINK https://github.com/snakeeyes021/flu-shot-learning/raw/main/Boosting%20Vaccination%20Rates%20Presentation.pdf).

**Repository Structure:**
```
├── data                                   <- Both sourced externally and generated from code 
├── images                                 <- Both sourced externally and generated from code 
├── .gitignore                             <- gitignore      
├── README.md                              <- The top-level README for reviewers of this project
├── ViaGoGo_presentation.pdf               <- PDF version of project presentation
├── app.py                                 <- ViaGoGo streamlit application back-end
└── index.ipynb                            <- Narrative documentation of analysis and modeling

```
