# ACME Headless CMS
This read me document describe headless CMS archticture including some digrams explains the target design.
I will describe step by step how I went through the challenge and the output for each step.

### Business Understanding
Before starting any architecture dive, you should understand well the customer needs.
I approache on of my firends which was working before in a service provider for travel agencies, and understand what they are doing who are the stackholder for this business.

### CMS Understanding
Then I went deeper to gain information about CMS as a concept and what should it provide.

### Model Design
- I started to design below ERD to describe whate are the main entities and the relation between them.
- I tried to make it as felixable as possible, but this lead to more complexity and more relations, which is not our target here.
- WOW, I got an Idea What if this structure in <b>JSON</b>, it will be felixable as much as I want.
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/ERD.png)

- Then I started designing the JSON object.
- Applying the model on a sample use case, which is creating offer list component.
- Covering below Composition scenario and mostof the required elements in any component.

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/componentModel.PNG)

![alt offer component model sample](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/model.json)

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/CMWA.png)

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/Modeler.png)

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/ContentManager.png)

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/Publisher.png)

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/CMSGUI.png)

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/componentsInquirySwagger.PNG)
![alt Swagger Sample API](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/componentsInquiryAPI.yaml)



![alt offer component content sample](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/content.json)

![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/allTogether.png)

### Why Mongo DB
##### Geofences POC
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/importgeo.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/importgeo2.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/importgeo3.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/importgeo4.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/importgeo5.PNG)

# Peroformance Enhancements through Indexes POC
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance1.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance2.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance3.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance4.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance5.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance6.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance7.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance8.PNG)
![alt text](https://github.com/ramyhasaan/architecture-challenge/blob/main/artifacts/mongodb/componentsPefromance9.PNG)

