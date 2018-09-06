# Spirited-WordCloud

Adding school spirit colours to a wordcloud

## Getting Started

Feeding images into [ColourMind](http://colormind.io/image/) to get colour palette for a wordcloud for Ryerson's Frosh Week

We uploaded this orientation schedule to the neural network 
![Ryerson Orientation Schedule](https://github.com/imjakedaniels/Spirited-WordCloud/blob/master/Project%20and%20Code/Ryerson%20Orientation%20Schedule.jpg?raw=true "Ryerson Orientation Schedule")

These are the colours we used
```
ryePallete <- c('#1C5F9B', '#C1138A', '#2E1D3B', '#FCC210')
```
### Prerequisites
```
library(wordcloud2)
library(rtweet)
library(tidyverse)
library(tidytext) 
```

## Connecting to Twitter API
```
#insert your own tokens
create_token(app = Sys.getenv("TWITTER_APP"),
  consumer_key = Sys.getenv("TWITTER_CONSUMER_KEY"),
  consumer_secret = Sys.getenv("TWITTER_CONSUMER_SECRET"))
```

## Pulling Tweets
```
rtr <- search_tweets("#RoadToRyerson", n = 2000, include_rts = FALSE)

data(stop_words)

rtrTable <- rtr %>%
  unnest_tokens(word, text) %>%  #Unnest the words
  anti_join(stop_words) %>%  #remove stop words
  count(word, sort = T) %>% #do a word count
  filter(!word %in% c('t.co', 'https', 'roadtoryerson', 'amp', 'ryersonu', 'ryerson', 'ryersonsa', 'ryersonfcs', 'student', 1:10))
```

## Visual
```
wordcloud2(rtrTable, size=0.7, color=rep_len( ryePallete, nrow(rtrTable)))
```
![Ryerson Orientation Schedule](https://github.com/imjakedaniels/Spirited-WordCloud/blob/master/Final%20Visual/ryerson_wordcloud.png?raw=true "Ryerson Orientation Schedule")


## Authors

* **Jake Daniels** - *Initial work* - [LinkedIn](https://www.linkedin.com/in/imjakedaniels/)