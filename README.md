YELP REVIEW SENTIMENT ANALYSIS
======

IN PROGRESS Project for UC Berkeley Data Science 205 Class Storing and Retrieving Data. Based on the Yelp Dataset Challenge.

Setup
------
Make sure you already have git configured locally, install `virtualenv` and download this directory:

    pip install virtualenv
    virtualenv venv
    cd venv
    git clone https://github.com/sialan/yelp-review-sentiment-analysis.git

Create a clean virtual environment and install dependencies:
    
    source bin/activate
    pip install -r requirements.txt

Download the Yelp dataset from https://www.yelp.com/dataset_challenge/dataset. Extract the json files from the zipped package and save them in the `data/input` folder.
    
For running scripts remotely on AWS EMR via MrJob, you will need to first configure account settings in the settings.json file.

	{
	    "aws":{
	        "aws_access_key_id": "YOUR_ACCESS_KEY",
    		"aws_secret_access_key": "YOUR_SECRET_KEY"
	    },
	    "s3":{
	        "input_bucket": "s3://mybucket/input/",
    		"output_bucket": "s3://mybucket/output/"
	    }
	}

Create the specified s3 bucket if it does not already exist and upload the json data files to s3. Make sure you already have the AWS command-line tool installed and configured.
    
    aws s3 cp data/input/yelp_dataset_challenge_reviews.json s3://mybucket/input/
    aws s3 cp data/input/yelp_dataset_challenge_reviews.json s3://mybucket/input/

Run Locally
------
To perform the sentiment analysis by keyphrase locally, run the main.py file with the `--local` and `--keyphrase` flag. Output will be stored in the `data/output/` folder.

	python main.py --local --keyphrase

To perform the sentiment analysis by topic locally, run the main.py file with the `--local` and `--topic` flag. Output will be stored in the `data/output/` folder.

	python main.py --local --topic

Run Remotely
------
To perform the sentiment analysis by keyphrase remotely on AWS EMR, run the main.py file with the `--remote` and `--keyphrase` flag. Output will be stored in the `output_bucket` specified in settions.json. 

	python main.py --remote --keyphrase

To perform the sentiment analysis by keyphrase remotely on AWS EMR, run the main.py file with the `--remote` and `--topic` flag. Output will be stored in the `output_bucket` specified in settions.json. 

	python main.py --remote --topic

Run Demo
------
To run the developed d3.js visualization for sentiment analysis, change to the demo folder and spin up a local python server. Demo can be accessed http://localhost:8888. Alternatively, a live version of the keyword sentiment analysis is being hosted at http://ucb-205-keyword-demo.s3-website-us-west-2.amazonaws.com/.
	
	cd demo
	python -m SimpleHTTPServer 8888
