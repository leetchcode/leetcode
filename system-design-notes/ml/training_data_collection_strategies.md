# Strategies to collect training data

## User's interaction with pre-existing system (Online data collection)
For example in a movie recommendation scenario if a user likes/watches a movie recommendation, it will count as a positive training example, but if a user dislikes/ignores a movie recommendation, it will be seen as a negative training example.

## Human labelers (Offline)
Certain scenarios exist where users interacting can't generate data for example image segmentation in a self-driving car. The car will capture images using cameras but the user's interaction doesn't really generate labels i.e objects in the image. This will require offline human labelers.
- Crowdsourcing: simple tasks that don't require specialized training and no privacy concerns. For ex: email spam classification is simple enough but if there are no privacy concerns can                   be used
- Specialized labelers: This is expensive as they need to be trained for example for image segmentation in images captured by self-driving cars. Another option is targeted data generation
                        i.e identify where the model is performing poorly and focus on those scenarios. For instance, you may find that it performs poorly for night time images and where                         multiple pedestrians are present. Therefore, you will focus more on gathering and labeling night time images and those with multiple pedestrians. 
