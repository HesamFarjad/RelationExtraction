# RelationExtraction
The primary NLP job of inferring semantic relationships between items from text is known as relation extraction (RE). In order to anticipate the link between tokens that make up entity spans, most supervised RE approaches use training modules to tag the tokens.



In code block one, we define a file called read map data to read the relation file, and the output of the relation file is a JSON file, and we read it, and its output is a dictionary.  We make output the dictionary as order dic. In order dic related to map data, there are a series of classes that we are supposed to predict. There is a number on that side indicates that the class is being predicted. The number of our classes becomes len relation when it will be the output of our relation file.

Another function is defined as (df)prepare, in which we define a tokenizer, it is of the BERT tokenizer type, and we put it as uncased so that it is not case-sensitive. Now the output of the JSON file that we got in train_df is a dictionary whose keys are subject, object, and relation. First, we read the subject and extract the parts we need. The subject becomes subject_start__idx. This is a dictionary in which there is a list in which we read the objected key related to the subject, and its output is stert_idx, end_idx, entity type, and text. When we put all these in that main data frame, it becomes subject_start_idx, subject_end_idx, entity type, and subject text, ...
 
Again, we do the same thing for the object, there is a relation, and we put this relation in it, and there is a label, which is the relation file that we read about Jason (like the one related to funders, the place of birth is equal to 2). Based on that, we assign the desired number to it, which can be labeled as a tokenizer for the text part, and we convert it to token to string, where we paste those tokens that are not useful in this code at the moment, which will be used later to change the code. It is likely to be used. After that, there is train_df, which can be prepared_train_df, and the test_df part can also be prepared_test_df, which we apply the prepare funkin that we defined above. For each of the data related to test_df or train_df, we count the number of tokens related to it. Then we report its maximum. So, the maximum number of test_df data tokens is the maximum number of train_df data tokens. (This became the maximum length).
Again, here is the tokenizer. Now use the BERT tokenizer as before, then we define the dataset class here. It is the same as the previous structure (it has initialized, len).

In the get_item part, we got a token, a label, ss (subject start), se (subject end), and os (object start), and so on. Here we define two labels, and want to define two loss functions, and optimize them simultaneously.
 
This lbl1=[0]*len(tkn)+(mx_len-len(tkn))*[100] comes to the size of len token. For instance, if there were 20, it will put 20 0 numbers (assuming that our maximum len is also 100 ) the rest sets it to 80 to 100 so that we know that it is our hundreds of padding. For example, from these first twenty arrays 4 to 6 are related to ss, se, which we set equal to one. And Array 10 to 12 is related to os, oe. (We set the start index and end index equal to one).

Label one-to-one np. We convert the array. We set the subject end, start subject to one, and the values of (os) to (oe) also set to one. Then we convert label-one to torch tensor. We have another label which is the output of the data set-label. It can be the output of the relation file (from 0 to 24).
 
We convert the obtained tokens into IDs that turn into a number. Here the length of the TOKEN is 20. To apply padding, we add zero to the rest of 80. Then we convert the token into a tensor file and execute all of them.
 
There is one relation model class that we have defined here in the initialize section, the bert model, FC One FC To, drop out, (fclh1), (fclh2). These are the tokens that are turned into IDs in our input. We enter them into the BERT model as input. Our model provides us with two outputs. The last hidden state is the first output, while the pooler output is the second.
The output becomes zero, the last hidden state and the output becomes one, pooler output. So, put these in the engine to get two outputs from it. The first model is on (clh), then we define a drop-out layer on it, then apply fully connected clh1 on it, then clh2, and finally permute. What happens is that initially, the output of BERT is 168 in 256. The pooler output has two differences from the (clh) output. The first output is two-dimensional, and the second output is three-dimensional. For example, if our batch size equals 32, our bert output will be 768.
 
In code block 5, we define the dataset. After that, we determine the data loader. Our model becomes a relation model. So, give it the number of classes as an input. And we define the criterion, which is cross entropy. There are three train data loader outputs, text, label, and label 1. which returns from the data function we defined above. The output of our model  is two pred, and Pred is 1. Here pred is pooler output, and pred 1 is (clh) output.
![image](https://github.com/HesamFarjad/RelationExtraction/assets/81914229/4c45c657-f016-4d75-8539-b3633d5cdfcc)
