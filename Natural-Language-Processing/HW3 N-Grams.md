# 09-27-2021 Title

---

Class: #NLP 
- [Class Notion page]()
- [Description](https://moodle.colgate.edu/mod/page/view.php?id=532477&inpopup=1)
Related notes:
- [[Language Models and N-grams]]

## TODO
- [ ] Compute Log P probability
	- [ ] Verify tokenize has the minimum number of tokens for the n-gram. Ex: 3-gram must be >= 3
	- [ ] Overwrite log_sentence_prob
- [ ] Extend the algorithm to deal with n-grams where n > 2
- [ ] Report the behavior of the method _generate_sentence_ in a one-page report.
- [ ] Done
- [ ] Submitted


--- 

## 

 # part 2

 # bigrams

 # hi all

 # hi~all

 # p(all|hi)

 # hi all world

 # p(all|hi)p(world|all)

 # hi my name is mario

 # Get the probability of each of the pairs 

 # hi~my

 # hi~name

 # hi~mairo

 # 3grams
 
 hi~my~name
 my~name~is...
 prob of next word given less. The second thing there is a bigram...**Need to calculate n-1 grams**
 P(is|my~name)
 
 my~name
 
 - Bigram
	 - Prob of the next word following the token given all the times the first word appears
	 - bigram count / first token count
	 - Prob of the sentence: The probabilities of each of the individual bigrams multiplied together 
 - Trigram
	 - prob of the next two words as a bigram given all the times the first word appears
 


