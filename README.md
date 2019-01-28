# Using NLP to play the stock market

In this assignment, we'll use everything we've learned to analyze corporate news and pick stocks. Be aware that in this assignment, we're trying to beat the benchmark of random chance (aka better than 50%).

This assignment will involve building three models:

**1. An RNN based on word inputs**

**2. A CNN based on character inputs**

**3. A neural net architecture that merges the previous two models**

You will apply these models to predicting whether a stock return will be positive or negative in the same day of a news publication.

## Your X - Reuters news data

Reuters is a news outlet that reports on corporations, among many other things. Stored in the `news_reuters.csv` file is news data listed in columns. The corresponding columns are the `ticker`, `name of company`, `date of publication`, `headline`, `first sentence`, and `news category`.

In this assignment it is up to you to decide how to clean this dataset. For instance, many of the first sentences contain a location name showing where the reporting is done. This is largely irrevant information and will probably just make your data noisier. You can also choose to subset on a certain news category, which might enhance your model performance and also limit the size of your data.

## Your Y - Stock information from Yahoo! Finance

Trading data from Yahoo! Finance was collected and then normalized using the [S&P 500](https://en.wikipedia.org/wiki/S%26P_500_Index). This is stored in the `stockReturns.json` file. 

In our dataset, the ticker for the S&P is `^GSPC`. Each ticker is compared the S&P and then judged on whether it is outperforming (positive value) or under-performing (negative value) the S&P. Each value is reported on a daily interval from 2004 to now.

Below is a diagram of the data in the json file. Note there are three types of data: short: 1 day return, mid: 7 day return, long 28 day return.

```
          term (short/mid/long)
         /         |         \
   ticker A   ticker B   ticker C
      /   \      /   \      /   \
  date1 date2 date1 date2 date1 date2
```

You will need to pick a length of time to focus on (day, week, month). You are welcome to train models on each dataset as well.  

Transform the return data such that the outcome will be binary:

```
label[y < 0] = 0
label[y >= 0] = 1
```

Finally, this data needs needs to be joined on the date and ticker - For each date of news publication, we want to join the corresponding corporation's news on its return information. We make the assumption that the day's return will reflect the sentiment of the news, regardless of timing.


# Your models - RNN, CNN, and RNN+CNN

For your RNN model, it needs to be based on word inputs, embedding the word inputs, encoding them with an RNN layer, and finally a decoding step (such as softmax or some other choice).

Your CNN model will be based on characters. For reference on how to do this, look at the CNN class demonstration in the course repository.

Finally you will combine the architecture for both of these models, either [merging](https://github.com/ShadyF/cnn-rnn-classifier) using the [Functional API](https://keras.io/getting-started/functional-api-guide/) or [stacking](http://www.aclweb.org/anthology/S17-2134). See the links for reference.

For each of these models, you will need to:
1. Create a train and test set, retaining the same test set for every model
2. Show the architecture for each model, printing it in your python notebook
2. Report the peformance according to some metric
3. Compare the performance of all of these models in a table (precision and recall)
4. Look at your labeling and print out the underlying data compared to the labels - for each model print out 2-3 examples of a good classification and a bad classification. Make an assertion why your model does well or poorly on those outputs.
5. For each model, calculate the return from the three most probable positive stock returns. Compare it to the actual return. Print this information in a table.

### Good luck!
--------------------------
