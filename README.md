

# Data Mining : algorithm for potentially liked pictures

BOUVEAU Augustin

JOBERT–ROLLIN Gabin

03/2023


## Goals :

This project's goal was to learn more about machine learning through a simple recommendation algorithm. We wanted  to get accustomed to python machine learning and data analysis libraries such as panda, sklearn and matplotlib. The recommendation algorithm uses user preferences to decide which image should be presented or not to the user, and then adapts itself according to the user’s choices. The data acquisition, annotation, analysis, and visualization are automated.


## Images :


### Sources and licenses

All our images were taken from wikidata using wikiquery. We only used images licensed under Creative Commons. You can easily change the type of images you want to download and use in the program, just replace the tag and query number at the begining in **lstSources**. The program will adapt by itself to those new images. We chose to use three different sources for now, fruits (Q1364), dogs (Q144) and lakes (Q23397). 

### Data size

We download all the images we get through the various queries in **lstSources**, but we set a limit parameter to download only the amount of pictures you want. Just change **limitPerSources** to whatever you want. The images will then be saved in the **images** folder, and will be named "image" + id, where id is an integer starting from 0 for the first image. Obviously the more images you want to download the larger the data size will be. It is important to know that the algorithm will perform better if the user has seen a lot of images.

### Stored Data

All of our images' data is stored in a json file, called **metaDataJson.json**. We extract the exif data for all images, but we were quite unlucky and couldn't get enough exif data for all our images to actually put it to use. We also got the 3 predominant colors in RGB format for all images, as well as a simple and naive estimation of the overall dominant color. The height, width and mode (RGB, etc) of the image are stored too. Those are used to get the image's orientation as well as size (big, small, etc), which are then used in the recommendation algorithm. The images also get a "main" tag when they are downloaded. This tag is decided based on the query used to get the image, so any image downloaded in this way will have at least one tag.


## Users :


### Create users

The users are stored in **jsonUser.json**, which is created if it doesn't exist when we first call the **createUser** function. This function initializes a json file with the user0 if empty or if it didn't exist before calling the function, otherwise it creates a new user using the given first name, last name, as well as a set of images seen and liked if wanted. If no images are given, two images are chosen randomly, and both a like and a dislike are randomly given. This ensures that the model will be able to work properly.

### User preferences

The user's preferences are calculated through the analysis of his liked images. We get all of his liked images' data and extract his preferences, meaning what most of his liked images share like the orientation, size, dominant color and tag. It is possible to get these informations for each user individually or for all users using the **printUserPref** function. It is also possible to get a more detailed view of the user's liked images' data through bar plots using the **plotPref** function. This function can also be used to display these informations for all the images we downloaded previously.


## Data analysis and machine learning :


### KMeans and MiniBatchKMeans

We wanted to get the dominant colors in each image. We thought of using sklearn's KMeans algorithm but through trials and tests we finally chose to use MiniBatchKMeans because it had better performance and great accuracy. This allowed us to get three colors in RGB format, which are then used to get an idea of the user's favorite color. These colors are then used in our recommendation algorithm.

### Decision Tree Classifier

We settled on using a decision tree classifier for our recommendation algorithm. It was helpful considering the various elements on which the evaluation of the likeability of the image could be established. We used ordinal encoders for our decision tree classifier, namely to avoid issues with some tags that could be presented to the user for the first time, or tags not present in the user's liked images. Our model gets retrained every time the user sees a new image and likes it or dislikes it. This is done through the **analyseGlobale** function, which can be called for a specific user and a specific pictures. We get all the data from the user's already seen images, we compare that to the images he liked. We then get the specific images data as the input for our prediction and we predict whether the user will like that image or not. That prediction is then used to recommend the image to the user, which and then likes or dislikes, which in turn help improving our model and our recommendations.


## Self-evaluation :


We managed to get real results after a bit of practice. We still don't know enough about all the libraries we used to be sure we got the most out of them and chose the best models for the job,, but at least we learned a bit more about how to use them. Our machine learning algorithm could be better, but it still works. We tested the algorithm with a lot of users and images, and even without  a lot of data to learn from, it seemed to perform well.


## How to improve 


### Our project

We can still improve our project a lot. We could always get more precise and make sure every function was safe to use and resistant to user manipulation (input types etc). Most of the improvements we could get are about optimization though. We could improve on execution time and costs, as well as accuracy. It would also be possible to improve our model by getting more data out of our images and exif, adding more tags to the user’s profile, etc. We knew it was possible to use the pickle library and partial fit to avoid rebuilding the model every run. But we had difficulty storing the model, so we had to run it quite often when updating the user’s liked images and such. But for this simple project using few pictures at a time and with the user’s limited amount of seen images for now, it worked good enough for us.

### Classes

We did not have a lot of time to practice what we needed during class, we had to work a lot by ourselves which helped us progress greatly despite the time it took. 


## Conclusion :


We succeeded in making our recommendation algorithm the way we wanted, and we are satisfied with the results and accuracy of our model. Our algorithms are functional but may be improved by choosing more suited sklearn algorithms and using partial fit to increase efficiency.
