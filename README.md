# ACME Headless CMS
This read me document describe headless CMS archticture including some digrams explains the target design.
I will describe step by step how I went through the challenge and the output for each step.

## Business Understanding
Before starting any architecture dive, you should understand well the customer needs.
I approache on of my firends which was working before in a service provider for travel agencies, and understand what they are doing who are the stackholder for this business.

## CMS Understanding
Then I went deeper to gain information about CMS as a concept and what should it provide.

## Model Design
#### Relational
- I started to design below ERD to describe whate are the main entities and the relation between them.
- I tried to make it as felixable as possible, but this lead to more complexity and more relations, which is not our target here.

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/ERD.png)
- WOW, I got an Idea What if this structure in <b>JSON</b>, it will be felixable as much as I want, let's forward and we will see if it's good idea or not.

## Content Manager WebApplication
This web application should be responsible of the following:
- Allow User to Model the content Types (Components) with full felixabilty.
- Allow the same User or diffrent User to add the content to the created components.
- Alow User to test what has been done.
- Allow User to instantly publish the content or schedule it.

##### <ins>Very High Level</ins>
This web Application should have FrontEnd & Backend, below is the backend portions.
* Backend will conist of independant decoupled Micro Services.
* I did not consider Micro frontend, as the frontend here is not that huge to divide it into small portions, and take the burrden of manitaince.

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/CMWA.png)
______________________________________________________________________________________________________________________________________________________________
##### <ins>Going Deeper</ins>
- Modeler service responsibility is to handle Content Types creation (Modeling Only).

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/Modeler.png)
______________________________________________________________________________________________________________________________________________________________
- Content Manager Service responsibility to handle contents of the created Models.
- I was planning to separate Testing in a tester service then decide to now overcomplicate things as some how testing is coupled to the contents.

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/ContentManager.png)
______________________________________________________________________________________________________________________________________________________________
- Publisher Service responsibility to publish what has been done either online or offline.
- Here I added BPM workflow to enrich the publisher with approval process, which is mandatory to avoid content corruption by one person.

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/Publisher.png)
______________________________________________________________________________________________________________________________________________________________
## Content Discovery APIs
- Content Discovery is the interface for all channels.
- All of the API returned contents, but in different ways.
- I tried to separate those APIs consedring the behaviour for each which is different and will help us later on in scalling them accordingly and choose the best technology fit with the behabiour.

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/ContentDiscovery2.png)

## Now It's time to decide data format and store !
### Data format
- As mentioned before, I figure out that relational DB will not give us the design felixability we need.
- And the Idea is to use <b>JSON</b>
- Then I started designing the JSON structure for creating a component.
- Applying the model on a sample use case, which is creating offer list component.
- Covering <b>Composition</b> scenario and most of the required elements in any component.
- [Link for offer component model sample in JSON](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/model.json) 

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/componentModel.PNG)

#### How Content Manager will use this Model
- I started to test this model logically, if it will fit with our requirements.
- How content manager will render this model on the screen to fill the data ?
- Let's draw a prototype as we are parsing this model and convert it to GUI components.

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/CMSGUI.png)

#### How Content Manager will save the contents
- It seems fine, now how Conent Manager will save the content after entering the information.
- [Link for offer component content sample](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/content.json)

#### Design some APIs for Service discovery
- Based on the above saved contents I started design couple of APIs to get component by Tag and By ID.
- Below snapshot from Swagger Editor.
- ![Link For Swagger Sample API](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/componentsInquiryAPI.yaml)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/componentsInquirySwagger.PNG)

______________________________________________________________________________________________________________________________________________________________

### Data Store
- I started to dive here, as it consider the most important component in this Use case.
- What I want is to Store data in JSON for <b>felixable structure</b>, and <b>fast data reading</b> to fulfill the high traffic.
- At this point I thought directly towards <b>NOSQL</b> and <b>Mongo DB</b> specifically, but does is the appropriate decission as we have many other options.
- I started to compare between some options like Casssandra, Redis And MongoDB.
- Any archticture decission is a kind of TradeOFF to get the best fit for your use case.
- I found that MongoDB is the most fit here.

#### Why Mongo DB here
- Felixable JSON Structure: We can return the JSON objects directly from DB to the client through our APIs without doing any processing or conversions
- Scalability: Will help us as traffic is increasing.
- High Performance: We should accomodate 1000s of requests per second, which can be reached with some tuning.
- Caching: Support caching data in RAM, which will help us to avoid going to different caching DB to speed up the response time.
- Supports Geo-based search including Polygons and locations.
- Supports Full-Text search as part of Mongo Atlas.

##### Geofences POC
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/importgeo.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/importgeo2.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/importgeo3.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/importgeo4.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/importgeo5.PNG)

##### Peroformance Enhancements through Indexes POC
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance1.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance2.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance3.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance4.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance5.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance6.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance7.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance8.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance9.PNG)



![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/allTogether.png)

