# I310D-Assignment2

The goal of this assignment is to explore the concept of bias through querying an existing natural language processing model — specifically, the Perspective API released by Google Jigsaw. For this assignment, I examined a dataset of internet comments and their scores, in addition to formulating my own queries and using the Perspective API client to score the toxicity of each comment.

To explore the scored dataset, I began by comparing the scores to the labels assigned by manual viewers. It can be inferred that high scores equals more 1-point labels from a general glance at the dataset. We can find that the model made mistakes with certain records such as the scores associated with the comment_text. 

To test the Perspective model for bias, I wanted to determine how subjective the labels for each comment_text by checking for inefficiencies in the number of labels being 0 or 1 and comparing it to the scores to see if there is a relationship between them. 

My hypothesis is that the higher the score of a comment_text, the more labels it should have. 

In order to analyze the data I decided to being by identifying all the comment_text’s that have a score of 0 in each label, then compare them to their score to see if there’s some sort of correlation between the 0-labeled comments and the at-least-1-labeled comments. I used the following line of codes and here are their respective results: 

##All Labels = 0

df[(df['toxic']==0) & (df['severe_toxic']==0) & (df['obscene']==0) & (df['threat']==0) & (df['insult']==0) & (df['identity_hate']==0)].sort_values(['score'])

<img width="1117" alt="Screen Shot 2022-04-20 at 12 35 52 AM" src="https://user-images.githubusercontent.com/56270858/164157717-d7e44946-167a-4b1a-afcc-f7acc0a13420.png">

#At Least One Label = 1

df[(df['toxic']==1) | (df['severe_toxic']==1) | (df['obscene']==1) | (df['threat']==1) | (df['insult']==1) | (df['identity_hate']==1)].sort_values(['score'])

<img width="1117" alt="Screen Shot 2022-04-20 at 12 36 52 AM" src="https://user-images.githubusercontent.com/56270858/164157794-7a4fb840-698d-4123-b1eb-f9cabc3c6e14.png">

I found it interesting out of 41,338 rows of records, 37,160 records scored received labels of 0 in every category and only 4,178 records have at least labels of 1. Furthermore, another interesting finding was that despite various comment_text’s having either entirely 0-point labels or at least a 1-point label, their scores did not indicate a strong correlation between the labels and the scores.

Comments in the entirely 0-point labels section had a minimum score range of 0.00004 (comment_text: “Можешь говорить по русски.” == “You can speak Russian.” to 0.000131 (comment_text: “Vals Vienés \n |Rumba \n |Cha Cha Chá(ciclo 7)” == “Viennese Waltz \n |Rumba \n |Cha Cha Chá(cycle 7)”) with comments in a different language at both extremes in the minimum score range.

Comments in the same section had a maximum score range of 0.955174 (comment_text: “jesus is completely fake plz go away fags”) to 0.977703 (comment_text: “fuck y'all all of yall”) with comments that had explicit and offense remarks, but still had a label of 0 throughout.

In other news, comments in the at least 1 point labels section had a minimum score range of 0.054399 (comment_text: “And we have a winner for the douchiest comment...”) to 0.140743 (comment_text: “SMOKE WEED ERRYDAY RIGHT BEFORE CLASS....PROFE...”) and they both have toxic labels of 1. 

Comments in the same section had a maximum score range of 0.997278 (comment_text: “you fucking piece of shit”) to 0.998329 (comment_text: “Fuck you you fucking pig!\n\nYou motherfucking...” where the first comment_text had toxic, severe_toxic, obscene, and insult labels of 1 each and the second comment_text has toxic, obscene, and insult labels of 1 each. I find it interesting because they 

After analyzing the data, it remains difficult whether to accept or reject the hypothesis stated above that: “the higher the score of a comment_text, the more labels it should have.” This is because though different comment_texts have different labels, even those that have 0 labels have scores almost as high as those comments that have at least 1 to 4 labels associated with them.

I feel as though the model could have been created in a fairer manner by studying/finding out how people feel about certain materials to see who finds what more toxic or not. 

In terms of biases that I believe exist, I believe it is fair to say that the reviewed dataset contains very subjective and biased data from the manual reviewers. It cannot be denied that different individuals have different morals and ethics in different contexts,

I theorize that there were varied reviewers to this dataset which greatly skewed the results of my findings and, in general, the overall dataset. I say this because some people may find certain comments more toxic than others based on different factors, experiences, and characteristics.
