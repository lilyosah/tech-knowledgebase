# 09-27-2021 Title

---

Class: #NLP 
- [Class Notion page]()
- [Description](https://moodle.colgate.edu/mod/page/view.php?id=532477&inpopup=1)
Related notes:
- [[Language Models]]

## TODO
- [x] Compute Log P probability
	- [x] Verify tokenize has the minimum number of tokens for the n-gram. Ex: 3-gram must be >= 3
	- [x] Overwrite log_sentence_prob
- [ ] Extend the algorithm to deal with n-grams where n > 2
- [ ] Report the behavior of the method _generate_sentence_ in a one-page report.
- [ ] Done
- [ ] Submitted


--- 

## Part 2
 hi~my~name
 my~name~is...
 prob of next word given less. The second thing there is a bigram...**Need to calculate n-1 grams**
 P(is|my~name)
 
 my~name
 
 - Bigram
	 - Prob of the next word following the token given all the times the first word (token) appears
	 - correct actual bigram count / first token count
	 - Prob of the sentence: The probabilities of each of the individual bigrams of the given sentence multiplied together 
 - Trigram
	 - prob of the next two words as a bigram given all the times the first word appears
	 - Prob of the sentence: The probabilities of each of the given trigrams of the sentence multiplied together 

Trigram: need to count the occurences of w1w2w3 and divide by occurences of w1w2  
- n_grams: creates n-grams of specified lengths
- self.\_n_grams keeps counters of ngrams. Need to count ngrams of length n and n-1


 


