# Using LDA and Jensen-Shannon Distance (JSD) to group similar newspaper articles

Many researchers have the problem that their data sets or automated set annotations contain articles that are irrelevant to their research question. For example, if the goal is to find newspaper articles or "news items" on return migration, researchers have to deal with some ambiguous search terms. The German words "Heimkehr" (returning home) or "Rückkehr" (returning back) lead to many articles that are relevant to the research question, but also to articles that are not relevant (e.g. return from a mountain tour, work, etc.). By using topic models and document similarity measurements, this notebook allows me to exclude these articles without combining the word "Heimkehr" with other search terms. Furthermore, the same code can also be used to remove or prefer a certain genre, e.g. advertising, sports news, etc.

To give another example: If I want to create a collection of articles about the disease cancer, one of the important German words for cancer is "Krebs". But "Krebs" in German is also a common surname, an animal (crab) or a sign of the zodiac.
The main purpose of this notebook is to take into account the context of articles in order to automatically refine a search query. This means that even ambiguous words can be used for the search without having to combine them with other words, making the search less influenced by the researcher's prior knowledge and avoiding a too narrow tunnel vision.

So how is this working?

Given a manually annotated collection of articles containing relevant as well as non relevant articles, this program will get the topic distribution of each document using LDA (gensim library). These topic distributions serve as a comparison for other, unseen articles, in order to automatically distinguish between relevant and non-relevant articles. The annotations are used for evaluation and counting the relevance probability for an unseen article.

For the comparison, the Jensen-Shannon distance method is used to measure the similarity between the topic distribution of an unseen article and the topic distribution of the training corpus. Therefore, the topic distribution of each new article will be compared to the topic distribution of the articles in the trained corpus. Then, for each unseen article, the 10 most similar articles from the training corpus are being extracted. These articles carry the information about the manually assigned relevancy. If 60 precent of the automatically found similar articles were annotated as relevant, the new article will be marked as relevant. Otherwise it will be marked as irrelevant. Using two different datasets (one about cancer and one about return migration), the average score of correct selected articles is between 80 and 90 percent.
