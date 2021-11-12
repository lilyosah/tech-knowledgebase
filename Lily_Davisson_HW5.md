```Python
import json
from b4msa.textmodel import TextModel
from sklearn.metrics import pairwise_distances
from EvoMSA.utils import load_model, download

def process_json_file(name):
	lines = []
	with open(name) as q:
		for line in q.readlines():
			lines.append(json.loads(line))
	return lines

def get_closest(queries, dataset, tm):
	data = tm.transform(dataset)
	queries = tm.transform(queries)
	dis = pairwise_distances(data, queries, metric='cosine')
	
 	results = []

	for i in range(queries.shape[0]):
		ranked = dis[:, i].argsort()[:5]
		results.append(str({"query": i, "knn": [d for d in ranked]}).replace("'", '"'))

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