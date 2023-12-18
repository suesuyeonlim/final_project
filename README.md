# Amazon Product Recommendation, Search, and Reviews
![image](https://github.com/suesuyeonlim/final_project/assets/19903898/8ec8c7ec-139e-454d-ad7a-e08bae6a81a0)

## I. Project Overview
In this project, I aim to show how to build recommendation engine for products, enhance search experience, and capture essence of product reviews that would be useful to customers. Specifically,
- <ins>Product Recommendation:</ins> I build recommendation engine using three model-based methodologies - Singular Vector Dceomposition ("SVD"), Alternating Least Squares ("ALS"), and neural networks.
- <ins>Product Search Enhancement:</ins> I show how product search can be enhanced by identifying similar groups of products by using sellers' product keywords through multi-label classifcation neural networks.
- <ins>Featured Product Reviews:</ins> I extracted featured review sentences that capture common themes of reviews for a product through Term Frequency - Inverse Document Frequency ("TF-IDF").

## II. Product Recommendation
In order to build recommendation engine using model-based approaches, I use [Amazon Product Reviews from UCSD](https://cseweb.ucsd.edu/~jmcauley/datasets.html#amazon_reviews) for years 2001-2018. As seen below, most reviews are concentrated in the 2013-2018 period and the average rating is approximately 4 stars.

> Number of Reviews

![image](https://github.com/suesuyeonlim/final_project/assets/19903898/98dee324-3a34-46d5-b2cf-305e7369fc4f)

> Average Review Ratings

![image](https://github.com/suesuyeonlim/final_project/assets/19903898/692d6188-c241-4c59-a2c7-23fc4ae72017)

Based on the data, I employ model-based approaches. Broadly speaking, model-based approaches derive an item embedding matrix which contains item deciding factors (e.g., how convenient is an item to use?) and a user embedding matrix which contains sensitivities to such item factors. I use three methods - SVD, ALS, and Neural Networks - and find that SVD and ALS perform better than Neural Networks. These methodologies are summarized below:

- SVD: SVD factorizes a matrix in a form A=UDV<sup>T</sup> where U, D, and V represent a user embedding matrix, strength of each latent factor, and an item embedding matrix.
- ALS: ALS minimizes errors by alternating between holding the user embedding matrix constant and the item embedding matrix constant.
- Neural Networks: Dot products of the user embedding matrix and the item embedding matrix feed into the model and optimized.

I would like to demonstrate an example using ALS. The following is an actual purchase list of a customer and the ratings the person left:
<img width="890" alt="image" src="https://github.com/suesuyeonlim/final_project/assets/19903898/17fe1b29-9e0f-4b41-8a07-52b6c9ff8f1f">

Top 10 products recommended for this customer are the following:
![image](https://github.com/suesuyeonlim/final_project/assets/19903898/3ebc1270-cb7e-4d78-b746-8c570306dbe3)

## III. Product Search Enhancement
For this task, I use [Amazon Berkeley Objects ("ABO") data](https://amazon-berkeley-objects.s3.amazonaws.com/index.html). I take advantage of the product keywords sellers post along with their products, and use them target labels that a neural network should predict based on product images. As a product can have more than one keyword, I use multi-label classification. I train the data to predict target labels, and the training and test accuracies amount to 99% and 93% respectively.

I would like to demonstrate an example of "formal shoes". There are four labels which contain the keyword "formal": "formal shoes for men black", "formal shoes for mens leather", "leather shoes for men formal branded", and "shoes for men formal". Below are 5 example shows with one of the aforementioned labels.

![image](https://github.com/suesuyeonlim/final_project/assets/19903898/2efadae0-ba3a-452d-9c6d-b5f92bcfe627)
![image](https://github.com/suesuyeonlim/final_project/assets/19903898/f604f2ff-43e4-451b-92d4-0a4efc9d1502)
![image](https://github.com/suesuyeonlim/final_project/assets/19903898/d99db19d-cda8-4bf2-90d5-2769bd470ac5)
![image](https://github.com/suesuyeonlim/final_project/assets/19903898/fff05aff-b671-4248-a332-b787838a8eed)
![image](https://github.com/suesuyeonlim/final_project/assets/19903898/cd191756-b57f-4868-9c2a-56690ac01e38)

## IV. Featured Product Reviews
![image](https://github.com/suesuyeonlim/final_project/assets/19903898/ca6ebb6c-712d-488d-8428-9b34a956c68a)

In order to build an NLP model, I again use [Amazon Product Reviews from UCSD](https://cseweb.ucsd.edu/~jmcauley/datasets.html#amazon_reviews). 
- I first derive most popular positive keywords from reviews of a product by employing TF-IDF on the positive reviews vs a negative word corpus. I do this to extract negative keywords as well.
- Then, I identify specific sentences containing those keywords from the reviews that are most popular based on the number of votes.

I would like to demonstrate an example "LitterMaid LM500 Automated Litter Box". For this cat litter box, the following are the top 5 positive review sentences:

> with 4 cats, i clean the entire unit about once every two weeks.

> after years of digging and scratching around in litter\nboxes myself, it's a joy to own something that brings the process into the 21st Century.

> i use a lot less litter, and spend almost no time dealing with the waste itself.

> (I have my unit in a carpet covered wood box because I have a dog who likes litter boxes...especially when there's a cat in it, and I keep a plastic runner at the opening of the box...it works great and I just vaccuum or sweep the runner when nec.)

> I originally bought this product to help elevate this issue but it has proven to be a blessing from the litter box gods.

Below are the top 5 negative review sentences:

> Therefore in conclusion, I do hope the next unit will be great since the cat seems to like it when it is "On Duty" and working, but when she is on Strike, it burns us all up and our pocketbooks from mailing them all the parts back they require and now burning our tempers that they now want to charge shipping fees for their "FREE" warranties that mean nothing really when they will only give u a problem when u point out there is no charges except the word "Free" regarding their Warranty and replacements on the Warranty information provided with the unit and on their site.

> But the list of shortcomings is a long one, the most endearing of which was flinging urineladen clods of litter against the wall.

> We used 3 types of premium clumping litter, yet end up cleaning the pan by hand frequently each day.

> Second, less than 2 months again this time the unit starts having a huge crack from the outside of the motor assembly and along the outside of the unit all down the side of the connection where the ac dc unit is plugged in.
Name: assembly, dtype: object 

> Finally, the little box at the end that is supposed to receive the litter is undersized for a multiple cat household, and are expen$ive to buy, so we started emptying the box and reusing it.

## V. Location of Data/Analysis
- Data: See "Data" folder.
- Analysis: There are two Jupyter notebooks, "01 Data Preparation.ipnyb" and "02 Main Analyses.ipynb". Unless you are interested in the data processing step, you can directly go to "02 Main Analyses.ipynb".
  - "01 Data Preparation.ipynb": This notebook cleans and subsets raw data which are used in the main analyses. In order to run this notebook, unzip the folder "Raw Data.zip" in the "Data" folder, and you need to download three datasets - (reviews for Pet Supplies)[https://datarepo.eng.ucsd.edu/mcauley_group/data/amazon_v2/categoryFiles/Pet_Supplies.json.gz], (product information data)[https://datarepo.eng.ucsd.edu/mcauley_group/data/amazon_v2/metaFiles2/meta_Pet_Supplies.json.gz], and (Shoes images data)[https://amazon-berkeley-objects.s3.amazonaws.com/archives/abo-images-small.tar].
  - "02 Main Analyses.ipynb": This notebook contains the three main analyses in product recommendation, search, and reviews. In order to run this notebook, unzip the folder "Data Used for Analysis.zip" in the "Data" folder.

## VI. References
- Ups and downs: Modeling the visual evolution of fashion trends with one-class collaborative filtering, R. He, J. McAuley, WWW, 2016
- Image-based recommendations on styles and substitutes, J. McAuley, C. Targett, J. Shi, A. van den Hengel, SIGIR, 2015
- Weight Initialization Techniques in Neural Networks, Saurabh Yadav (https://towardsdatascience.com/weight-initialization-techniques-in-neural-networks-26c649eb3b78)
