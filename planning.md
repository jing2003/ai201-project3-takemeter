# TakeMeter — planning.md

---

## Community

**Community:** r/GenshinImpact

I chose r/GenshinImpact as my community because it is active, text-heavy, and centered on a game that has many different types of discussion. Users post about team-building, character builds, artifact farming, pulling decisions, quests, story theories, character interpretation, updates, events, and personal reactions to the game.

This community is a good fit for a classification task because the discourse is varied enough to create meaningful label distinctions. Some posts are practical and advice-focused, some are analytical and story-focused, and others are mostly emotional reactions or unsupported opinions. These differences matter because people visit the community for different reasons: some want help improving their account, some want deeper lore discussion, and others want to share quick reactions or complaints.

---

## Labels

I will use **three labels**:

1. `gameplay_advice`
2. `lore_analysis`
3. `reaction_opinion`

---

### Label 1: `gameplay_advice`

**Definition:** A post or comment that asks for or gives practical advice about gameplay, builds, teams, artifacts, weapons, pulls, quests, exploration, combat, or account progress.

**Example 1:**
"Should I pull for Furina if I already have Yelan and Xingqiu? I mainly use Hu Tao and Hyperbloom teams, so I'm not sure if she would improve my account."

**Example 2:**
"For Nahida, is Elemental Mastery more important than Crit Rate and Crit Damage? I'm trying to build her for a Hyperbloom team with Kuki."

This label is focused on practical decision-making. The post should help the user make a gameplay choice or solve a gameplay-related problem.

---

### Label 2: `lore_analysis`

**Definition:** A post or comment that discusses Genshin's story, characters, worldbuilding, theories, regions, factions, quests, or symbolism using explanation, interpretation, or evidence from the game.

**Example 1:**
"I think Furina's story works because her performance as an Archon reflects the pressure of being forced into a role. Her behavior during the Fontaine Archon Quest makes more sense when you see it as survival rather than arrogance."

**Example 2:**
"The Abyss Order's goal seems connected to the idea that Teyvat's current order is artificial. Several quests suggest that the world's history has been rewritten or hidden from ordinary people."

This label is focused on interpretation and explanation. The post should go beyond simply liking or disliking a story moment and should attempt to explain meaning, motivation, symbolism, or worldbuilding.

---

### Label 3: `reaction_opinion`

**Definition:** A post or comment that mainly expresses a personal reaction, complaint, praise, rant, hot take, or emotional opinion without much supporting explanation.

**Example 1:**
"The new event is boring. I don't understand why they keep making events like this."

**Example 2:**
"This banner is terrible. I'm skipping everything until the next region."

This label is focused on immediate reactions or unsupported opinions. The post may still be meaningful to the community, but it does not provide enough specific advice or analysis to fit the other two labels.

---

## Hard Edge Cases

The hardest edge case will be **character-focused posts**, because a post about the same character could belong to any of the three labels depending on the purpose of the post.

For example, a post about Furina could be:

- `gameplay_advice` if the user asks whether to pull for her, how to build her, or what team to use her in.
- `lore_analysis` if the user discusses her role in the Fontaine Archon Quest, her character development, or what she represents in the story.
- `reaction_opinion` if the user simply says they love her, hate her, think she is overrated, or dislike her banner without much explanation.

### Decision Rule

When I encounter an ambiguous post, I will label it based on the main intent of the post.

If the post is about account decisions, team-building, combat usefulness, builds, artifacts, weapons, or pulling advice, I will label it `gameplay_advice`.

If the post is about story meaning, character development, symbolism, worldbuilding, theories, or quest interpretation, I will label it `lore_analysis`.

If the post mainly expresses a feeling, complaint, praise, rant, or unsupported judgment, I will label it `reaction_opinion`.

### Specific Ambiguous Example

"Is Neuvillette still worth pulling, or is he overrated now?"

This could be either `gameplay_advice` or `reaction_opinion`.

I will label it `gameplay_advice` if the post includes account context, team needs, character goals, Abyss performance, or asks for practical advice. I will label it `reaction_opinion` if the post is mainly a broad opinion about whether the character is overrated without asking for specific help.

Another ambiguous example is:

"Artifact farming is bad because it takes too much resin and the RNG makes progress feel impossible."

This could be `reaction_opinion` or `gameplay_advice`.

I will label it `reaction_opinion` if the post mainly complains about artifact farming. I will label it `gameplay_advice` only if the post asks for or gives specific advice about artifact stats, domains, resin use, builds, or account improvement.

---

## Data Collection Plan

I will manually collect at least **200 public posts or comments** from r/GenshinImpact. I will collect text from posts and comments that contain enough written content to classify. I will avoid collecting usernames or unnecessary personal information. The dataset will focus on the text content and the assigned label.

I plan to collect examples from a mix of:

- Recent posts
- Recent comments
- Search results within the subreddit for gameplay terms
- Search results within the subreddit for lore/story terms
- Search results within the subreddit for opinion/reaction terms

I will not include deleted posts, removed posts, image-only posts, meme-only posts, pure self-promotion, or posts that require an image/video to understand.

### Target Label Distribution

My goal is to collect a roughly balanced dataset:

| Label              | Target Count |
| ------------------ | -----------: |
| `gameplay_advice`  |           67 |
| `lore_analysis`    |           66 |
| `reaction_opinion` |           67 |
| **Total**          |      **200** |

A balanced dataset is important because if one label dominates the dataset, the model may learn to overpredict that label instead of learning the actual differences between discourse types.

### If a Label Is Underrepresented

If one label is underrepresented after the first 200 examples, I will collect more examples targeted toward that label.

For `gameplay_advice`, I can search for terms like "build," "team," "artifact," "weapon," "pull," "worth it," "help," or "quest."

For `lore_analysis`, I can search for terms like "lore," "theory," "Archon Quest," "story," "Celestia," "Abyss," "Khaenri'ah," "character development," or specific character names.

For `reaction_opinion`, I can search for terms like "boring," "best," "worst," "overrated," "underrated," "hate," "love," "event," or "banner."

If a label is still difficult to collect, I will either collect more than 200 total examples to balance the dataset or document the imbalance as a limitation. I will not force unclear examples into a label just to reach the target count.

---

## Data Collection and Annotation Results

I collected and annotated my dataset using public r/GenshinImpact posts and comments. The dataset is saved as one CSV file with the required `text` and `label` columns, plus a `notes` column for short notes about difficult or borderline cases. I did not pre-split the file because the project notebook will handle the train, validation, and test split automatically.

During collection, I filtered out deleted posts, removed posts, image-only posts, meme-only posts, pure self-promotion, and posts that could not be understood without text. I focused on examples that fit my three planned labels: `gameplay_advice`, `lore_analysis`, and `reaction_opinion`.

### Final Label Distribution

| Label              |   Count |
| ------------------ | ------: |
| `gameplay_advice`  |      67 |
| `lore_analysis`    |      67 |
| `reaction_opinion` |      67 |
| **Total**          | **201** |

No single label accounts for more than 70% of the dataset. The dataset is balanced across the three labels, which should help prevent the model from mostly predicting one majority class.

### Difficult Annotation Cases

#### Difficult Case 1

**Text:** “Is Neuvillette still worth pulling, or is he overrated now?”
**Possible labels:** `gameplay_advice` vs. `reaction_opinion`
**Final label:** `gameplay_advice`
**Reason:** The word “overrated” makes it sound like an opinion post, but the main purpose is asking whether the character is worth pulling.

#### Difficult Case 2

**Text:** “Artifact farming is bad because it takes too much resin and the RNG makes progress feel impossible.”
**Possible labels:** `gameplay_advice` vs. `reaction_opinion`
**Final label:** `reaction_opinion`
**Reason:** The post talks about a gameplay system, but it mainly expresses frustration instead of asking for or giving practical build advice.

#### Difficult Case 3

**Text:** “Yeah I agree, Dainsleif and sibling journeyed after. Who knows what the details are, if sibling tried to help save Khaenri'ah or only met Dainsleif after it was destroyed and didn't know about the history until after learning about it and talking to Dainsleif. At which some point they started to hate Dainsleif's attitude or perspectives of Khaneri'ah or Abyss Order and joined the Abyss Order to right the wrongs. Meanwhile Dainsleif has some other opinion or objectives regarding why the Abyss Order is going about it all wrong...”
**Possible labels:** `lore_analysis` vs. `reaction_opinion`
**Final label:** `lore_analysis`
**Reason:** The post includes speculation, but it is mainly explaining story events, character motivations, Khaenri'ah, Dainsleif, and the Abyss Order.

### Annotation Reflection

The hardest examples were usually about characters, banners, artifact farming, or story speculation. These posts sometimes mixed opinion language with gameplay advice or lore interpretation. To stay consistent, I labeled each example based on its main purpose. If the post was mainly asking for practical help, I labeled it `gameplay_advice`. If it was mainly interpreting story, characters, or worldbuilding, I labeled it `lore_analysis`. If it mostly expressed a feeling, complaint, praise, or unsupported opinion, I labeled it `reaction_opinion`.

---

## Evaluation Metrics

Accuracy alone is not enough for this task because the dataset may not be perfectly balanced, and some labels may be easier for the model to predict than others. A model could get decent accuracy by doing well on the most common label while still performing poorly on a less common label like `lore_analysis`.

I will use the following metrics:

### Accuracy

Accuracy will show the overall percentage of correct predictions. This is useful as a general performance measure, but it will not be my only metric.

### Macro F1 Score

Macro F1 is important because it gives equal weight to each label. This matters because I want the model to perform reasonably well on all three discourse types, not just the most common one.

### Per-Class Precision and Recall

I will check precision and recall for each label.

Precision answers: when the model predicts a label, how often is it correct?

Recall answers: out of all true examples of a label, how many did the model successfully find?

This is important because different errors have different meanings. For example, if the model has low recall for `lore_analysis`, it may be missing deeper story discussion and incorrectly labeling it as general opinion. If it has low precision for `gameplay_advice`, it may be calling too many vague opinion posts advice.

### Confusion Matrix

I will use a confusion matrix to see which labels are most often confused with each other. This is especially important for edge cases like character posts that could be gameplay-related, lore-related, or opinion-based.

The confusion matrix will help me answer questions such as:

- Is the model confusing `gameplay_advice` with `reaction_opinion`?
- Is the model failing to recognize `lore_analysis`?
- Are ambiguous character posts causing most of the errors?

---

## Definition of Success

For this project, a successful classifier should do more than get a high overall accuracy. It should separate practical gameplay discussion, lore/story analysis, and reaction/opinion posts well enough that the predictions would be useful for organizing or understanding community discourse.

### Minimum Success Criteria

I will consider the model successful for the class project if it reaches:

- Overall accuracy of at least **75%**
- Macro F1 score of at least **0.70**
- Recall of at least **0.60** for each individual label

These thresholds would show that the model is learning meaningful differences between the labels instead of only predicting the easiest or most common category.

### Good Enough for a Real Community Tool

For real deployment in a community tool, I would want stronger performance:

- Overall accuracy of at least **85%**
- Macro F1 score of at least **0.80**
- Recall of at least **0.75** for each individual label
- No major pattern of harmful or misleading confusion between labels

For example, if the model consistently labels detailed lore analysis as `reaction_opinion`, that would be a serious problem because it would undervalue thoughtful discussion. If it sometimes confuses a vague pull complaint with gameplay advice, that is less serious but still worth improving.

A real community tool should also keep a human review step for uncertain or borderline cases. I would not use this classifier as an automatic moderation system. It would be more appropriate as a tool for organizing posts, analyzing discourse patterns, or helping moderators identify broad trends.

---

## AI Tool Plan

AI tools will be used carefully in this project. They will help with stress-testing labels, optionally assisting annotation, and analyzing model failures, but the final label decisions and evaluation conclusions will be reviewed by me.

### Label Stress-Testing

Before annotating all 200 examples, I will give an AI tool my label definitions and edge case rules. I will ask it to generate 5–10 example posts that sit near the boundary between two labels, such as `gameplay_advice` vs. `reaction_opinion` or `lore_analysis` vs. `reaction_opinion`.

The purpose is to test whether my label definitions are clear enough. If the AI generates examples that I cannot classify consistently, I will revise the definitions and decision rules before labeling the full dataset.

Example prompt I may use:

"Here are my three labels for classifying r/GenshinImpact posts: `gameplay_advice`, `lore_analysis`, and `reaction_opinion`. Generate 10 ambiguous posts that sit between two labels. For each one, explain which two labels it could fit and why."

After receiving the AI-generated examples, I will manually decide how each should be labeled. If I find that my rules are unclear, I will update this planning document.

### Annotation Assistance

I may use an LLM to pre-label some examples before I review them myself. If I do this, I will not treat the AI label as the final label. I will use it only as a first-pass suggestion.

To track this, my dataset will include separate columns such as:

| Column               | Purpose                                  |
| -------------------- | ---------------------------------------- |
| `text`               | The post or comment text                 |
| `ai_suggested_label` | The label suggested by the AI, if used   |
| `human_final_label`  | My final reviewed label                  |
| `notes`              | Any uncertainty or edge case explanation |

If I use AI pre-labeling, I will disclose this in my AI usage section. If I decide not to use AI pre-labeling, I will label everything manually and only use AI for stress-testing and failure analysis.

For Milestone 3, I used an AI tool to help organize the dataset and suggest labels for some examples. I reviewed the labels against my own definitions before using them in the final dataset. I will disclose this in the README AI Usage section because AI assistance was part of the annotation workflow.

### Failure Analysis

After training and evaluating the model, I will collect the wrong predictions and give them to an AI tool to look for patterns. I will ask the AI to identify common failure types, such as:

- The model confuses vague gameplay complaints with gameplay advice.
- The model misses lore analysis when the post also contains emotional language.
- The model relies too much on character names instead of the purpose of the post.
- The model struggles with short posts that lack context.

I will verify these patterns myself by reading the incorrect predictions. I will not assume the AI's failure analysis is correct without checking the examples. The final evaluation write-up will include both the model's metrics and my own interpretation of where the classifier works and where it falls apart.

---

## Stretch Feature Plan

### Stretch Feature 1: Inter-Annotator Reliability

Before training the final model, I may ask another person to independently label at least 30 examples from my dataset using my label definitions. I will not tell them my labels beforehand for those examples. After they label the examples, I will compare their labels with mine.

I will report either simple percentage agreement or Cohen’s kappa. Simple percentage agreement is easier to explain, while Cohen’s kappa is stronger because it accounts for agreement by chance.

I will also analyze disagreements. For example, if we disagree mostly between `gameplay_advice` and `reaction_opinion`, that would show that my boundary between practical advice and opinion language may still be difficult.

### Stretch Feature 2: Confidence Calibration

After evaluating the fine-tuned model, I will check whether the model’s confidence scores are meaningful. I will group predictions by confidence range and compare the confidence level to actual accuracy.

Possible confidence groups:

| Confidence Range | What I Will Check                          |
| ---------------- | ------------------------------------------ |
| 90–100%          | Should usually be correct                  |
| 70–89%           | Should be mostly correct but less reliable |
| 50–69%           | Should contain more mistakes               |
| Below 50%        | Should be treated as uncertain             |

If high-confidence predictions are often wrong, then the model is overconfident. If low-confidence predictions are usually wrong or ambiguous, that means confidence may be useful for identifying examples that need human review.

### Stretch Feature 3: Error Pattern Analysis

Beyond listing individual wrong predictions, I will look for a systematic pattern across the model’s errors. I will group wrong predictions by label pair and post type.

I will look for patterns such as:

- The model misclassifies short gameplay complaints as `gameplay_advice`
- The model misclassifies emotional lore posts as `reaction_opinion`
- The model relies too much on character names instead of the actual purpose of the post
- The model struggles when a post includes both opinion language and practical advice

If I find a repeated pattern, I will describe it in the README with supporting examples from the error set.

### Stretch Feature 4: Deployed Interface

If time allows, I will build a simple interface that accepts a new Genshin-related post or comment as input and displays the predicted label and confidence score.

The interface can be simple. It may be a small Python app, notebook cell, Streamlit app, or web page depending on what is easiest to connect to the trained model.

The interface should allow a user to:

1. Enter or paste a post/comment.
2. Click a button or run a function.
3. See the predicted label.
4. See the confidence score.

If I complete this stretch feature, I will commit the interface code to the repo and document how to run it in the README.
