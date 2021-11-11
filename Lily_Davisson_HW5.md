```Python
import json
from b4msa.textmodel import TextModel
from sklearn.metrics import pairwise_distances
from EvoMSA.utils import load_model, download

def process_json_file(name):
	with open(name) as q:
 	lines = q.readlines()
 	return lines

def get_closest(queries, dataset, tm):
	data = tm.transform(dataset)
 	results = []
 	for query in queries:
		q_parsed = json.loads(query)
		q_text = q_parsed['text']
		q_transformed = tm.transform(q_text)
		dis = pairwise_distances(data, q_transformed, metric='cosine')

 		results.append(str({"query": q_parsed['query'], "knn": dis[:, 0].argsort()[:5].tolist()}))

	return results

  
queries = process_json_file('query.json')
dataset = process_json_file('dataset.json')

emo_tm = load_model(download("emo_En.tm"))
tm = TextModel(lang="english").fit(dataset)

tf = get_closest(queries, dataset, tm)
emo = get_closest(queries, dataset, emo_tm)

with open('tfidf.json', "w") as f:
	f.write("\n".join(tf))

with open('emoji.json', "w") as f:
	f.write("\n".join(emo))
```