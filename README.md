# Chat Analysis
## Data Format:
JSON

# Data Preparation
## Import Library
os, pandas, numpy, matplotlib.pyplot, json, imp, time, pandas.io.json

## Data Import:
1. Set the directory by ```os.chdir```

2. use ```open()``` to connect the raw data set with spyder
	1. Specific the encoding to ```utf-8-sig``` for Chinese characters
	
3. load the opened data by ```json.load()```

4. normalize the data by ```json_normalize()```

## Data Cleansing
#### Assume that we have a list of internal user ID, but we want to refresh when new raw data come in

### Internal Users
1. Find the internal user ID (useless for analysis) by ```value_counts()``` and ```head(5)```
	- I assume that the top 5 users must be an internal users. Of course, eye-ball checking will do it later
	
2. Use ```.index``` and ```list()``` to create a ```temp_list``` for internal user ID

3. Combine the list with original one with ```extend()```

4. Drop the duplicated ID in list by ```set()```

5. Filter the internal users by ```apply()``` the ```lambda``` function with ```not in temp_list```

#### However, there are some problems in the data set when normalizing the JSON structrual format
#### When chatbot reply 3 messages at the same time, it will count as '3 Chats Appeared', we need to find a way to count it as '1 Chat'
#### Therefore, we will take unique timestamp and user_id as ONE conversation (assume user and chatbot will not reply more than once at same timestamp

### Duplicated / Useless Chat
1. Drop the duplicated chat by ```drop_duplicates()``` for **_timestamp_** and **_user_id_**

2. Filter the useless data at 'message' column('menu', 'GET_STARTED', null data)
	- delete null data by ```notnull()```

3. Drop the useless column by ```drop()``` with ```axis = 1```
	- '_index', '_score', '_source.chatbot_id', 'sort', '_type', '_source.platform', '_source', '_source.morePayload.limit', '_source.morePayload.morekey', '_source.morePayload.type', '_source.quickReplyPayload.moreKey', '_source.quickReplyPayload.morType'












# Explorartory Analysis
