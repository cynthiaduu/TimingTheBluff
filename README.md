# TimingTheBluff

### Project Overview
Poker is a game of skill, strategy, and deception. One of the most critical aspects of the game is the ability to bluff - convincing opponents that a weak hand is strong or vice versa. But, would it be possible to use data and machine learning to detect when a player is bluffing? This project explores whether or not it is possible to detect if a player is bluffing based on various in-game factors, such as decision time, player position, and bet sizing, with a primary focus on whether the time it takes to bet can uncover deception. The ability to identify bluffs in poker has significant implications not only for poker strategy, but also for broader fields like behavioral economics, game theory, and artificial intelligence.

In this study, we collected hand histories from private, real-money cash games hosted on the PokerNow.club platform. These games featured blinds ranging from $0.25/$0.50 up to $2/$5 ($50 to $500 buy-in). After each session, we exported the detailed game logs—encompassing actions such as posting blinds, betting, raising, folding, and showdown results—into CSV files.

We then processed and cleaned these logs, filtering out administrative lines and any incomplete or irrelevant records. The resulting dataset retained all pertinent gameplay actions, including each player’s decisions (e.g., bets, calls, raises, folds) and timing information. This allowed us to label each hand as a bluff or value scenario and engineer various features (such as bet size ratios, decision times, and positional context) for subsequent analyses.

Given the abundance in data values, we decided to discard any anomalies from standard Texas Hold’em 2 hand poker. From these data values, we extracted hands that went to showdown for verification of our dependent variable bluff/value.We also extracted information of community/hand cards pertaining to the round, engineering variables such as winning_hand and board_evaluation. The variable board_evaluation was then used to engineer variables analyzing the current state of the community cards. Any variables that was directly related to the outcome were only used to verify the validity of the dependent variable.

### Models Used
#### Logistic Regression

Logistic regression is a simpler, linear model that is often used for binary classification problems, such as predicting whether a hand is a bluff or not. While it may not capture complex relationships as well as more advanced models, it serves as a useful baseline due to its interpretability and allows us to understand the weight of each feature.

#### Random Forest

Random Forest is a method that builds multiple decision trees and merges them to improve the model’s accuracy and reduce overfitting. This model works well in cases with complex data and non-linear relationships, which is likely in our dataset where player behavior is influenced by multiple factors like position, hand strength, betting history, and opponents’ actions. We wanted to try this model because it can handle both numerical and categorical features and provide insight into feature importance.

#### XGBoost

XGBoost is a powerful gradient boosting model that builds a series of decision trees iteratively, each one focusing on correcting the mistakes made by the previous tree. XGBoost is able to handle large datasets and capture complex patterns in data. Thus, it is a great fit for predicting bluffing behavior, where interactions between features like bet timing, hand strength, and player position are important.

#### SVM

Support Vector Machines are supervised learning models that are effective for classification tasks, especially in cases where the data is not linearly separable. SVM tries to find the hyperplane that best divides the two classes (bluff vs value) with the maximum margin. This is useful if you believe that there are clear, but complex boundaries between bluffing and non-bluffing hands, even though they may not be easy to capture with simpler models. SVM can also be adapted with kernel functions to handle non-linear decision boundaries, making it versatile for this type of analysis.

#### MLP

MLP consists of multiple layers of neurons that process features like bet sizes, action sequences, and player positions to detect bluffing patterns. Unlike LSTM, it does not retain past information explicitly, but it can still learn complex interactions between features. MLP serves as a middle ground between simpler models like logistic regression and deep learning approaches like LSTM, making it a strong candidate for identifying bluffing tendencies based on structured game data.

#### LSTM

LSTM is a type of recurrent neural network (RNN) that’s particularly effective for sequential data, like time-series or game logs where the order of actions matters. In poker, the decisions players make depend on the context of previous moves, so using LSTM allows the model to capture these temporal dependencies. For example, a player’s betting pattern across multiple rounds can give clues about whether they are bluffing or playing a value hand. LSTM can also handle varying-length sequences, making it ideal for processing poker hands of different lengths.

### Conclusion
Overall, the Long Short Term Memory model has proven highly effective at predicting bluffing where other models failed. Across multiple models, decision time has proven useful in predicting whether of not a player is bluffing. These results should prove useful both in justifying the inclusion of decision time in future statistical models, and poker simulations.
