## Newspaper
In the shared Box folder, you can find the files containing the downloaded news articles and metadata under /presidency_project/newspaper/ny2/, /presidency_project/newspaper/wp/, and /presidency_project/newspaper/wsj/. You can find the most recently saved R objects under /presidency_project_/newspaper/workspaceR/

* Clean up `readNews.R`: Currently, when I update with another month of news, the code reads in all the months of news again anew. This takes longer than necessary. It should be re-written to load the previously saved RData file, read in only the newest articles and metadata and either (1) transform these, and add them to the tm corpus, and recreate the quanteda corpus completely, or (2) transform these and add them to the prior quanteda corpus (not sure if I need the tm corpus -- maybe, if we want to add additional cleaning steps via tm_map as problems are realized). Probably other bits could be better, too.

  * Aycan
* Run `exploreNews.R` and look for words, phrases that need to be normalized across the three newspapers. For instance, `readNews.R` already makes a few changes like changing F.B.I in the NYT to FBI to match the WSJ, or trying to change the appearance of U.S. in the WSJ to United States to match the NYT. But I suspect the current clean up isn't sufficient either because not everything worked and there are more phrases and abbreviations specific to a news source. We need another set of eyes to start capturing these so we can beef up and correct the reading/cleaning file.

  * Leah
* Create a new version of `complexityNews.R` using sentences as unit (e.g., `complexityNews_sent.R`: this should start with the same data object that `complexityNews.R` uses, but first reshape `qcorpus2` to sentences. It should create a new metadata data frame like `qmeta2` (e.g., `qmeta2_sent <- docvars(qcorpus2_sent`) and add the complexity/readability score to the dataframe.

  * Sofia

* Create version of `sentimentNews.R` using sentences as unit (e.g., `sentimentNews_sent.R`); as above, this should start with the same data object that `sentimentNews.R` uses (ideally, it would start with the saved data object from `complexityNews_sent.R`, but if that's not created yet -- we can sequence them later), but will need to reshape `qcorpus2` to sentences. And this, too, should create a new metadata frame like `qmeta2` and add the various sentiment scores to the dataframe.

  * Sofia

* Update `sentimentNews.R` and `sentimentNews_sent.R` to try the [Lexicoder Sentiment Dictionary](http://www.lexicoder.com/index.html), implemented in `quanteda` in late 2017 ([see here](https://quanteda.io/reference/data_dictionary_LSD2015.html)). Evaluation of sentiment results generated from lexicoder, sentimentr, and bing dictionaries -- e.g., face validity, do sample articles/sentences scored as highly negative or positive read as such? 
	* Aycan

* Generate `policyNews.R` and `policyNews_sent.R` (beginning with output of `sentimentNews.R` and `sentimentNews_sent.R`) to implement policy/issue attention in articles using the Lexicoder Topic Dictionary. Evaluation of results -- e.g., to sample articles/sentences scored highly on major topics appear to be correctly assigned?

* Generate `positionNews.R` and `positionNews_sent.R` to test ideological position of text using Wordfish ([see example here](http://quanteda.io/articles/pkgdown/examples/plotting.html)); and test policy position of text using [Laver and Garry's WordStat dictionary](https://provalisresearch.com/products/content-analysis-software/wordstat-dictionary/laver-garry-dictionary-of-policy-position/), readable into quanteda ([see example here](https://tutorials.quanteda.io/basic-operations/dfm/dfm_lookup/), the laver-garry.cat hyperlink on the example links to the dictionary file). Honestly, I don't expect either of these to work very well -- both have been developed for party platform-style texts, not news (and Laver-Garry dictionary is for UK parties). But evaluation of these results can provide some ideas about how to improve measures in this corpus, and ideological/policy positioning is a key feature in comparison of news treatment (particularly with regard to charges of bias).
  
  * Leah

* Start named entity recognition process (might be better in Python?): in particular, extracting persons, organizations, and geographical or geopolitical entities is key. I'm less clear on how we want to store this -- it won't be as neatly structured as the other attributes extracted from the text so far. But in addition to including this in the larger feature data frame eventually, the entitites also lend themselves to other analytic approaches (e.g., networks).

* To be added: improvements to topic model script

  
## Additional Sources

* Look into possibility of scraping key internet news sites on right and left. First need to identify/justify what are key native digital news sites on right/left; e.g., Politico, Breitbart, or something else, selected by audience size/ideological center. May or may not be able to acquire from January 20, 2017 on, but could we at least set up something going forward?

## Cable News

* To be added: reviewing topictiling, validating initial results (e.g., against Vanderbilt News Archive's story count for Anderson Cooper, other ways?), figure out how to containerize the process (via singularity) to run on the cluster. 

## Presidential Documents

* To begin, need to separate `analyze_presdoc.R` into an exploratory script (the parts just looking at the text in multiple ways) and a feature extraction script (where features are being added to a document dataframe -- complexity, sentiment, policy/issues, topics, etc.). 

* Once an extraction script is started, consider a sentence or paragraph version to mirror the newspapers (should discuss which makes more sense in this case; unlike the newspaper case where paragraphs are usually one sentence, it could make more difference here).

## Tweets

* To be added: ran out of time

