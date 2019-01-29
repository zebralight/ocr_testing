Notes:
* Lindsay will check w/Ryan on embedding
* Intro needs more. Sections like:
* * Focus some grounding methods in the intro: this is dense but people need a compass. What are they about to hear and why should they pay attention. Blow out the first graph.
* * Testing Method
* *

Scaffolding the viewer
Limit the embeds to the end and capture key takeaways in screenshots/ images.


# Welcome

This repository contains the scripts and outputs from our OCR comparison tests.

We identified a few sample documents to run through OCR systems so we could compare the results. The documents we used in our final write up are these:

+ A receipt -- This receipt from the Riker's commissary was included in States of Incarceration, a collaborative storytelling project and traveling exhibition about incarceration in America.
+ A heavily redacted document -- Carter Page's FISA warrant is a legal filing with a lot of redacted portions, just the kind of exasperating thing reporters deal with all the time.
+ Something historical -- Executive Order 9066 authorized the internment of Japanese Americans in 1942. The scanned image available in the national archives is fairly high quality but it is still an old, typewritten document.
+ A form -- This Texas campaign finance report, from a Texas Tribune story about abuses in the juvenile justice system has very clean text but the formatting is important to understanding the document.
+ Something wrinkled --  in early 2014 a group of divers retrieved hundreds of pages of documents from a lake at Ukrainian President Viktor Yanukovych's vast country estate. The former president or his staff had dumped the records there in the hopes of destroying them, but many pages were still at least somewhat legible. Reporters laid them out to dry and began the process of transcribing the waterlogged papers. We selected a page that is more or less readable to the human eye but definitely warped with water damage.

We also tested the OCR engines against a handful of alternate documents. We've preserved two of those documents here so that you can look them over, too. Both are relatively easy to read and all the OCR engines we tested handled them well.  

The first, `cepr_oversight_order`  is an order giving the Puerto Rico Energy Commission oversight powers over the Puerto Rico Electric Power Authority, after the latter authority's [highly unusual](https://www.reuters.com/article/us-usa-puertorico-power/tiny-montana-firms-puerto-rico-power-deal-draws-scrutiny-idUSKBN1CW1X1) [$300 Million contract](https://www.vox.com/policy-and-politics/2017/11/15/16648924/puerto-rico-whitefish-contract-congress-investigation) with Whitefish Energy came under scrutiny.

The second, `whitefish_energy_vs_commonwealth_puerto_rico` is the full text of a legal filing in the protracted fight over who is responsible for delays in rebuilding Puerto Rico's electric grid. These two articles are a great place to get more context:
* [Puerto Rico moves to cancel contract with Whitefish Energy to repair electric grid](https://www.washingtonpost.com/business/economy/puerto-rico-governor-says-contract-to-whitefish-company-should-be-canceled/2017/10/29/e5336cda-bcb8-11e7-97d9-bdab5a0ab381_story.html?utm_term=.685e693e654d), *The Washington Post*, Oct 29, 2017; and
* [Puerto Rico Grid Contractor Dispute Devolves Into Litigation](https://www.wsj.com/articles/puerto-rico-grid-contractor-dispute-devolves-into-litigation-1511396684), *The Wall Street Journal*, Nov 22, 2017

# Using this Repository

The `/lib/` directory includes the scripts that we used to test each OCR client. Each tool requires some setup, but once you've got a tool installed, you can invoke it with:


`ruby ./lib/ocr.rb [command]`

For example once you have installed Tesseract, `ruby ./lib/ocr.rb tesseract documents` will use Tesseract to OCR all the images in the "documents" directory.

Once you have set up Google Cloud services and stored your credentials, `ruby ./lib/ocr.rb google google_cloud_vision/credentials.json documents/historical-executive_order_9066-japanese_internment.jpg` will use Google Cloud Vision to OCR a single image.

## Installation

### Cloud Services

Once you have set up your accounts on the appropriate cloud service, save your credentials into a `credentials.json` file.

#### Google Cloud Vision

See the example in [`google_cloud_vision/credentials.sample.json`](https://github.com/factful/ocr_testing/blob/master/google_cloud_vision/credentials.sample.json)

#### Azure Computer Vision

See the example in [`azure/credentials.sample.json`](https://github.com/factful/ocr_testing/blob/master/azure/credentials.sample.json)

#### Abbyy

Abbyy provides a python script. 

### Command Line Tools

#### Tesseract

`tesseract` far and away the best maintained and easiest to use of the command line tools we tested.  It is available via most package managers.

On MacOS:

`brew install tesseract --with-all-languages`

Ubuntu/Debian:

`apt install tesseract tesseract-ocr-*`

#### OCRopus

- requires python 2.7
- requires downloading [code from Github](https://github.com/tmbdev/ocropy)
- requires downloading models

```
cd ocropy
pip install -r requirements.txt
python setup.py install
```

`ocropus-rpred` should now be available on the commandline.

#### Calamari

- requires everything OCRopus requires
- also requires python3
- requires tensorflow

```
cd calamari
pip install -r requirements.txt
python setup.py install
```

`calamari-predict` should now be available on the commandline.
