## Elo Customer Loyalty Prediction (Kaggle Comp)

### Overview of the project

Elo, a payment solutions provider was looking to uncover signals in customer loyalty in order to provide customised purchase recommendations to its users. Kagglers were asked to builld a model to predict individual customers' loyalty scores.

The __Evaluation Metric__ used was Root Mean Squared Error (RMSE)

### The Data

The Data broadly consisted of 3 sections; Details about the customer, Transactions of customers, Details about the various merchants the customers shopped at. Further details are as follows:

1. __Details about the customer (The training set):__ 
   - Features: 
       - Card_id: Unique customer identifier
       - First_active_month: Customer's first activity
       - 3 anonymized categorical features
       - Target feature
2. __Transactions:__ Historical transactions made by customers. Around 30 million in total. Most features were anonymized but a few were named.
3. __Merchants:__ Metadata about the several merchants used (2 tables). Some features like average sales etc were named but most were anonymized.
4. __Test Set:__ Identical to the training set

### Brief overview of the process used to solve the problem

Firstly, I worked on properly joining the different tables and then aggregating the transactions & merchants data according to the individual card_ids (the unique customer identifier). Next step was to figure out a good validation set.  And finally, empirical application (fine tuning) of different algorithms to see what worked best. My PC did not have the capacity to process this amount of data so I had to use __AWS EC2__ instances frequently. 

### Step wise walk through

1. __Joins and aggregations:__
    1. Creating a DataFrame with transactions containing only training set card_ids. This was done by doing a left join of training DF & transactions DF on the card_id column. This left rows of the test set with NaNs; on removing these rows, only transactions of training card_ids remained. I have not added the file in which this was done (did'nt seem useful).
    2. Aggregating training set transactions: Please review this file: [Aggregating Transactions](
        Elo-Merchant-Category-Kaggle-Comp-/Aggregating Transactions.ipynb/)

2. __Selecting Validation Set (File Link: ):__ Quickly apply a few different algorithms and then check the scores on validation and test set. Doing this 4 or 5 times and check if the results of Val vs Test form around about a straight line. This generally indicates that the validation set is reflective of the test set and can be used for algo fine tuning.
    - __Results:__ The Val set looked good and was chosen.
