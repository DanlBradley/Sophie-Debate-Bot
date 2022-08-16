<h1>Sophie – the debate bot</h1>

<h2>Business Problem</h2>

This repo contains the files necessary to build (the beginnings of) a conversational AI that will debate with the user on a specified topic. At a high level, the goal is for the AI to be able to classify what issue the user is discussing, what their stance on that issue is, and then generate a specific response defending the other side of the chosen topic. In addition, metrics should be logged to measure the effectiveness of both the person’s and the computer’s arguments for/against the issue.

Most chat bots, AI, and other automated systems exist to help you or otherwise pick up tasks that you would rather not do yourself. An argumentative bot, however, would challenge you and push you to identify weaknesses in your beliefs. This has the potential to be beneficial in many areas, including education, debate preparation/forecasting of any kind, professional development, and advertisement strategy development to name a few.

Education: One of the most efficient ways to learn about an issue is to have someone show you weaknesses in your own understanding. A conversational AI that attacks these weaknesses is a powerful feedback tool for learning.

Debate preparation/forecasting: It goes without saying that a debate AI could help in the realm of debates. It could be used to help people hone their debate skills by being automatically scored by the program and help forecast how each participant in a debate is doing based on the quality of their points.

Professional development: It is often the case that disagreements do not get resolved in the workplace because emotions can so often get in the way. By allowing people to discuss such ideas with a conversational AI, the emotional component can be reduced.

Advertisement: By understanding and measuring which arguments well against people, an advertisement team may be able to gain insight in which advertisement strategies work best in each field. While A/B testing has been widely implemented in advertisement, there are still few tools to uncover which sales pitches work well in absolute terms.

IBM has been developing [their own](https://research.ibm.com/interactive/project-debater/) automatic debate system for several years, titled Project Debater, and released a paper on the system in Nature [1]. The basic principle is a hierarchy of classification models in addition to a corpus-based topic generation model, using over 400 million articles from the web. My project cannot be at this scale, of course, and I will focus on the hierarchical classification and rebuttal portion of this system to develop a chat bot that can build suitable responses to a person on a select set of issues, that will be trained on using labeled datasets discussed in the next section.

 

<h2>Data Sources</h2>

Sophie will consist of multiple models, each with their own trained output, and therefore will require different datasets to train each model. IBM Debater has already compiled many datasets for this task and will be heavily leveraged in this project. In addition, the ArgKP dataset will be used to train a model on key point analysis. The datasets associated with the different models are listed below:

1.	Domain detection: What topic is the debater discussing? The model must be able to determine this accurately to access the correct class of responses.
a.	The dataset: Argumentative Sentences in Recorded Debates [2]
b.	700 sentences labeled 0 or 1 if it is about the specified topic.
2.	Argument quality: How convincing is the argument? This model will leverage a dataset which compares pairs of evidence for/against a topic and which of the pair is more convincing.
a.	The dataset: Evidence Quality [3]
b.	1,844 pieces of evidence, from which 5,697 pairs were sampled and manually labeled which of the pair was more convincing. From 69 topics.
3.	Argument stance: Is the debater for or against the selected topic? This is important to classify so that Sophie can determine how to argue against the point.
a.	The dataset: Claim Stance [4]
b.	2,394 claims in 55 labeled topics
4.	Debater Analysis: Sophie should be able to comprehend what the debater is saying and use their key points and stance to generate a relevant rebuttal passage.
a.	The dataset: Recorded Debating Dataset (no audio files) [5]
5.	Key point analysis: This model will train on the ArgKP dataset and their associated manually created key points as substrings of the argument. The goal of the model then is to train on 
a.	The dataset: ArgKP 2021 [6]
b.	27,519 argument, key point pairs labeled as matching or not matching on 31 topics. Stance and topic are also labeled.
6.	 Claim generation: Finally, Sophie must be able to take these factors into account and generate argumentative claims.
a.	The dataset: IBM Debater - GPT-2 Claim Generation [7]
b.	2,739 texts by GPT-2 fine-tuned models on 131 topics. Labeled for plausibility and stance.




Bibliography

[1] Slonim, N., Bilu, Y., Alzate, C. et al. An autonomous debating system. Nature 591, 379–384 (2021). https://doi.org/10.1038/s41586-021-03215-w

[2] Unsupervised Expressive Rules Provide Explainability and Assist Human Experts Grasping New Domains, Eyal Shnarch, Leshem Choshen, Guy Moshkowich, Noam Slonim and Ranit Aharonov, Findings of the Association for Computational Linguistics: EMNLP 2020

[3] Will it Blend? Blending Weak and Strong Labeled Data in a Neural Network for Argumentation Mining, Eyal Shnarch, Carlos Alzate, Lena Dankin, Martin Gleize, Yufang Hou, Leshem Choshen, Ranit Aharonov and Noam Slonim. Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics, 2018

[4] A Benchmark Dataset for Automatic Detection of Claims and Evidence in the Context of Controversial Topics, Ehud Aharoni, Anatoly Polnarov, Tamar Lavee, Daniel Hershcovich, Ran Levy, Ruty Rinott, Dan Gutfreund, and Noam Slonim, Proceedings of the First Workshop on Argumentation Mining, ACL, pp. 64-68, Association for Computational Linguistics, 2014

[5] Out of the echo chamber: Detecting countering debate speeches, Matan Orbach, Yonatan Bilu, Assaf Toledo, Dan La- hav, Michal Jacovi, Ranit Aharonov, and Noam Slonim. 2020. Proceedings of the 58th Annual Meeting of the Association for Compu- tational Linguistics, pages 7073–7086, Online. As- sociation for Computational Linguistics. 

[6] Overview of the 2021 Key Point Analysis Shared Task. Roni Friedman, Lena Dankin, Yufang Hou, Ranit Aharonov, Yoav Katz and Noam Slonim. 8th Workshop on Argumentation Mining 2021.

[7] Shai Gretz, Yonatan Bilu, Edo Cohen-Karlik and Noam Slonim, The workweek is the best time to start a family -- A Study of GPT-2 Based Claim Generation, In Proceedings of EMNLP Findings, 2020
