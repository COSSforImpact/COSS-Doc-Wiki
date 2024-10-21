---
icon: elementor
---

# Sunbird Design : QUML Player integration with containers design

#### Story Link: [Lazy loading of questions in QUML Player](https://project-sunbird.atlassian.net/browse/SB-22404) <a href="#qumlplayerintegrationwithcontainersdesign-storylink-lazyloadingofquestionsinqumlplayer" id="qumlplayerintegrationwithcontainersdesign-storylink-lazyloadingofquestionsinqumlplayer"></a>

#### Problem statement: <a href="#qumlplayerintegrationwithcontainersdesign-problemstatement" id="qumlplayerintegrationwithcontainersdesign-problemstatement"></a>

QUML player should be capable of playing question sets on its own and since each question set may contain hundreds of question loading all the questions at once and providing them to player from container like mobile or web with low bandwidth will give a bad user experience so questions should be lazy-loaded to make the player user experience smooth.

#### &#x20;Solution: <a href="#qumlplayerintegrationwithcontainersdesign-solution" id="qumlplayerintegrationwithcontainersdesign-solution"></a>

We will define an abstract class with the method declarations which is the contract between QUML player and containers below is the abstract class for the same\
\


```
abstract class QuestionCursor {

  getQuestions(identifiers: string[]) : <question>[] || null || error<Object>;

  getQuestion(identifier: string): question || error<Object>
  
  saveState(metaData: object, questionSetId: string, userId?: string); //
  
  getState(questionSetId: string, userId?: string): metaData; //
}
```

1. Fetch question set length
2. Check if the question set length is below the threshold, the threshold should be the configuration driven
3. If the question set length is below the threshold get all the questions
4. if the question set length higher than the threshold then get the threshold number of questions
5. If it is an exam threshold = 1,
