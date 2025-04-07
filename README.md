from sklearn.feature_extraction.text import TfidfVectorizer
import pandas as pd
document_Speech_1 = "The car is driven on the road"
document_Speech_2 = "The truck is driven on the highway"

corpus = [document_Speech_1, document_Speech_2]
vectorizer = TfidfVectorizer(stop_words='english')
X = vectorizer.fit_transform(corpus)
feature_names = vectorizer.get_feature_names_out()
df = pd.DataFrame.sparse.from_spmatrix(X, columns=feature_names)    
#Display First F+ew Columns and Last Few Columns
print(df.head())
