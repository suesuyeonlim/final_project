# Amazon Product Recommendation, Search, and Reviews
<img width="687" alt="image" src="https://github.com/suesuyeonlim/final_project/assets/19903898/da46889a-4f50-48c1-8572-da45b81cae3d">

## I. Project Overview
Amazon is the world's largest online retailer founded in 1994. Its product managers constantly look for ways to improve user experience. User experience at Amazon consists of the following elements: 1) product recommendations customized for individual users; 2) accurate item search; and 3) reviews useful for their purchase decisions.

To enhance the elements of user experience, I first analyze the current status of each element below.

- Recommendations: Amazon mainly uses memory-based collaborative filtering. It requires calculating every time a prediction is made. Also, it does not handle cold-start problems well.
- Search: Amazon's search results are usually extensive and relevant, but for some keywords, the listings tend to repeat.
- Reviews: Each product page has reviews sections. While there is a summary provided for each product, it tends to be generic and not extremely useful for users.

Below is a new proposed plan to improve the elements.

- Recommendations: Use model-based collaborative filtering which does not require computation every time.
- Search: Automate generating product categories based on the keywords sellers post, and classify products as those categories to expand search.
- Reviews: Extract key featured sentences among all the reviews.

For reference, you can find and play around with the code in Google Colab: https://drive.google.com/file/d/1GXH57NHi1oM4hMAOsGKkajTKnjZnWH41/view?usp=drive_link.

## II. Product Recommendation
In order to build recommendation engine using model-based approaches, I use [Amazon Product Reviews from UCSD](https://cseweb.ucsd.edu/~jmcauley/datasets.html#amazon_reviews) for years 2001-2018. As seen below, most reviews are concentrated in the 2013-2018 period and the average rating is approximately 4 stars.

> Number of Reviews

![image](https://github.com/suesuyeonlim/final_project/assets/19903898/347aa238-a020-43ed-9688-96fa32737498)

> Average Review Ratings

![image](https://github.com/suesuyeonlim/final_project/assets/19903898/797d4c0c-94b4-4c63-be19-f568abf3ab14)

Based on the data, I employ model-based approaches. Broadly speaking, model-based approaches derive an item embedding matrix which contains item deciding factors (e.g., how convenient is an item to use?) and a user embedding matrix which contains sensitivities to such item factors. I use three methods - SVD, ALS, and Neural Networks - and find that SVD and ALS perform better than Neural Networks. These methodologies are summarized below:

- SVD: SVD factorizes a matrix in a form A=UDV<sup>T</sup> where U, D, and V represent a user embedding matrix, strength of each latent factor, and an item embedding matrix.
- ALS: ALS minimizes errors by alternating between holding the user embedding matrix constant and the item embedding matrix constant.
- Neural Networks: Dot products of the user embedding matrix and the item embedding matrix feed into the model and optimized.

I would like to demonstrate an example using ALS. The following is an actual purchase list of a customer and the ratings the person left:

<img width="628" alt="image" src="https://github.com/suesuyeonlim/final_project/assets/19903898/b15f8371-62c9-4977-b713-96b8b5c5c895">

Top 10 products recommended for this customer are the following:

<img width="830" alt="image" src="https://github.com/suesuyeonlim/final_project/assets/19903898/bee6240d-e067-40ae-869c-aaf658d8304f">

## III. Product Search Enhancement
For this task, I use [Amazon Berkeley Objects ("ABO") data](https://amazon-berkeley-objects.s3.amazonaws.com/index.html). I take advantage of the product keywords sellers post along with their products, and use them target labels that a neural network should predict based on product images. As a product can have more than one keyword, I use multi-label classification. I train the data to predict target labels, and the training and test accuracies amount to 99% and 93% respectively.

I would like to demonstrate an example of "formal shoes". There are four labels which contain the keyword "formal": "formal shoes for men black", "formal shoes for mens leather", "leather shoes for men formal branded", and "shoes for men formal". Below are 3 examples with one of the aforementioned labels.

![image](https://github.com/suesuyeonlim/final_project/assets/19903898/2554f9f2-cd33-4d4e-9b5e-9730f2579355)
![image](https://github.com/suesuyeonlim/final_project/assets/19903898/69d6834f-103c-4636-9a64-8ae44f4bcf83)
![image](https://github.com/suesuyeonlim/final_project/assets/19903898/1b5a00bb-2075-4f8b-9639-59ab48484227)

## IV. Featured Product Reviews
![image](https://github.com/suesuyeonlim/final_project/assets/19903898/45f2ddb0-4b89-49d2-8c44-f27a442bd6ce)

In order to build an NLP model, I again use [Amazon Product Reviews from UCSD](https://cseweb.ucsd.edu/~jmcauley/datasets.html#amazon_reviews). 
- I first derive most popular positive keywords from reviews of a product by employing TF-IDF on the positive reviews vs a negative word corpus. I do this to extract negative keywords as well.
- Then, I identify specific sentences containing those keywords from the reviews that are most popular based on the number of votes.

I would like to demonstrate an example "Nylabone Dura Chew Textured Dog Chew, X-Large". For this dog chew, the following are the top 5 positive review sentences:

>“( 2560+ lbs)\nIt's really cute to walk along the aisle and see contented dogs happily holding their chew bones in their paws and gnawing away.”

>“I am so glad I got it and I suspect they are even happier!”

>“My 60 pound boxer pit mix is a fan.”

>“Yummy & Healthy & Fun ...”

>“Wears slowly.”

Below are the top 5 negative review sentences:

>“Like I handed her a brick.”

>“I was told that if we got her something like this, she would not tear up anything, like my Bible, anymore.”

>“Price is very high than local store, you may able to buy it from Marshall or other local store with better price, and my dog evening blooding after play a while with this product, after one time use, I just through it away.”

>“so this is a big fat nope is our book of chew toys.”

>“I bought this when I had 4 dogs in the house (our two, and two puppies we were fostering), out of 4 dogs NONE of them wanted this!”

## V. Conclusions
Recommendations: Explore and introduce model-based collaborative filtering.
Search: Implement the automated process of generating product categories and assignining exising products to them, which can be then used for exapnding the search.
Reviews: Show featured review sentences as a summary of reviews.

## VI. Future Work
Recommendations: Explore hybrid approches of model-based and memory-based models to optimize performance.
Search: Further validate the accuracy of expanded item search.
Reviews: Try different formulas for pulling keywords to see which extract most useful sentences. Produce an evaluation tool to measure the success.

## VII. Location of Data/Analysis
- Data: See "Data" folder.
- Analysis: There are two Jupyter notebooks, "01 Data Preparation.ipnyb" and "02 Main Analyses.ipynb". Unless you are interested in the data processing step, you can directly go to "02 Main Analyses.ipynb". Alternatively, you can also play around with the file [here](https://drive.google.com/file/d/1GXH57NHi1oM4hMAOsGKkajTKnjZnWH41/view?usp=drive_link).
  - "01 Data Preparation.ipynb"
    - This notebook cleans and subsets raw data which are used in the main analyses. In order to run this notebook, unzip the folder "Raw Data.zip" in the "Data" folder, and you need to download three datasets - (reviews for Pet Supplies)[https://datarepo.eng.ucsd.edu/mcauley_group/data/amazon_v2/categoryFiles/Pet_Supplies.json.gz], (product information data)[https://datarepo.eng.ucsd.edu/mcauley_group/data/amazon_v2/metaFiles2/meta_Pet_Supplies.json.gz], and (Shoes images data)[https://amazon-berkeley-objects.s3.amazonaws.com/archives/abo-images-small.tar].
  - "02 Main Analyses.ipynb"
    - This notebook contains the three main analyses in product recommendation, search, and reviews. In order to run this notebook, unzip the folder "Data Used for Analysis.zip" in the "Data" folder.

## VIII. References
- Ups and downs: Modeling the visual evolution of fashion trends with one-class collaborative filtering, R. He, J. McAuley, WWW, 2016
- Image-based recommendations on styles and substitutes, J. McAuley, C. Targett, J. Shi, A. van den Hengel, SIGIR, 2015
- Weight Initialization Techniques in Neural Networks, Saurabh Yadav (https://towardsdatascience.com/weight-initialization-techniques-in-neural-networks-26c649eb3b78)
- Book Recommendation System, Gilbert Tanner (https://www.kaggle.com/code/tannergi/book-recommendation-system)
- Using Neural Networks for Your Recommender System, Benedikt Schifferer, NVIDIA DEVELOPER (https://developer.nvidia.com/blog/using-neural-networks-for-your-recommender-system/)
