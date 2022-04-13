# ds4400_facial_recognition_final_project


1. download data - download the massive UTK aligned and cropped labelled faces (will refer to it as UTK-CA) https://susanqq.github.io/UTKFace/
2. get random subsample for testing - choose a random sample of that massive dataset and load them in. idk maybe 100 images to practice until we make sure shit runs. how do we store a bunch of images? can we put them in a...dataframe?
3. get target labels for race and gender - extract corresponding labels for images from file names with regexes or something, store race in a vector and gender in a different vector
5. preprocessing - preprocessing was mostly done for us by the wonderful UTK-CA dataset

ABOVE DONE

SKIP BELOW STEP, DO AT END TO SEE HOW ACCURACY CHANGES
7. normalizing - we might want to use "histogram equalization" so that light/dark doesn't change predictions, but unsure of best way to do this
TODO STEP 5


EIGENFACES ARE A GOOD IDEA. TRY WORKING WITH THIS FOR TWO DAYS ON RACE, TRY TO VISUALIZE THEM FOR EACH RACE CLASS. gender would be an easier task, it's binary. 
IF THIS IS TOO HARD, CONSIDER USING PRE-TRAINED MODIFIED CNNs FOR FEATURE EXTRACTION INSTEAD (see tutorials online)
6. extract features from images - extract features from the face images with one of a few possible techniques (eigenfaces/fisherfaces/LBPH (local binary patterns histogram)) goal: construct a low-dimensional linear subspace that best explains the variation/scatter of the face images
  4a. choose a method of feature extraction from {eigenface, fisherface, gaborface, LBPH (local binary patterns histogram)}
  TODO STEP 4A
  4b. resource - tutorials for using opencv's eigenfaces/fisherfaces/LBPH (local binary patterns histogram) https://www.superdatascience.com/blogs/opencv-face-recognition
  
  
5. model selection - select models that we want to train on the extracted features
  5a. consider: multi-class logistic regression FIRST, linear SVM, then random forest, adaboost+eigen should be a good combo but kinda overkill. using a FFNN at the end is how CNNs are constructed that so that would work well
  TODO STEP 5A
  5b. Consider a pre-trained CNN if we're feeling frisky and want to melt some GPUs?
6. practice model training - train models on extracted features using our 100 person subset of UTK-CA. see if it works
7. select unbalanced dataset - Choose a larger random subset of UTK-CA, num records = (TBD TODO - not sure how many is reasonable for this), split train/test, see how it performs. 
8. create balanced dataset - Choose a random subset of UTK-CA the same size as the above subset BUT make sure it's balanced by explicitly finding 8 groups of equal size (8 = races*genders, ex  num black females should be equal to num white males in balanced dataset), split train/test, see how it performs.
9. demonstrate balanced vs. unbalanced - make a graph showing the representations of age and race in the balanced and unbalanced datasets
10. real model training - train models we chose in 5a on unbalanced dataset and on balanced dataset. save as many performance metrics as we can for each model
11. model performance comparison - make a chart where rows are each model type (including whether it was trained on balanced or unbalanced dataset), and columns are predictive accuracy for each class? ideally show that unbalanced dataset did a worse job

side resources:

http://i-rep.emu.edu.tr:8080/xmlui/bitstream/handle/11129/4353/mehriarmin.pdf?sequence=1
- great notes on histogram equalization and methodology with PCA, LDA, LBP, decision trees, random forest

a super accessibly written dissertation with details of feature extraction methods AND classification methods! https://researchrepository.wvu.edu/cgi/viewcontent.cgi?article=4453&context=etd Eigenface, Fisherface, and Gaborface methods for gender feature representation are introduced, in addition to Local Binary Pattern (LBP) descriptor. The classifiers that are used include Adaboost classifier and SVM
LDA is good for when we have limited computational resources (which i guess we do)
random forest is easy and baller if we can get good features from eigenface, fisherface, or gaborface
MLP is also good, they use 20 hidden nodes and 40 training cycles for binary gender (ha) classification task
also very useful for discussion and model comparison sections - lots of great info at an appropriate level for us to read in this paper
