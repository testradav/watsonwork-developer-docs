# Focus


<a name="overview"></a>
## Overview
The Focus API provides a mechanism for our Cognitive service to analyze your text to see if there are any potential areas of focus.

You can send the Focus API a text string that contains one or more sentences, and the service will analyze each sentence.  It will view the text through several different lenses.  A lens is a particular way of looking at the text.  A focus is a result of that lens applied to the given text where the lens has found something interesting. If the lens is "action" or "question", then a particular action or question identified by the lens is a "focus".  The API returns a list of focuses found during the analysis.  That list can be empty (no focuses found), or it might contain one or more focuses.  A confidence level for each focus prediction is included in the response.


### Version information
*Version* : 1.0.0


### URI scheme
*Host* : api.watsonwork.ibm.com  
*Schemes* : HTTPS




<a name="paths"></a>
## Paths

<a name="v1-focus-post"></a>
### Analyze the provided text, and return any focuses.
```
POST /v1/focus
```


#### Description
Analyze the provided text through several different lenses, returning any focuses found.


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Authorization header, in form of `Bearer {access_token}`<br><br>The `access_token` is issued as result of an oauth flow by Watson Work Services.|string||
|**Header**|**Content-Type**  <br>*required*|has to be `application/json`|string||
|**Body**|**RequestEntity**  <br>*required*|Representation of the text to be analyzed.|[RequestEntity](#requestentity)||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Text was analyzed successfully.|[FocusResponse](#focusresponse)|
|**400**|Bad Request: one ore more input values is/are invalid.|No Content|
|**403**|Forbidden: caller is not authenticated|No Content|
|**500**|Internal server error.|No Content|


#### Consumes

* `application/json`


#### Produces

* `application/json`




<a name="definitions"></a>
## Definitions

<a name="focus"></a>
### Focus
Entity that represents a single focus found for the analyzed text


|Name|Description|Schema|
|---|---|---|
|**applicationId**  <br>*optional*|ID of the registered application with which the custom lens is associated.|string|
|**category**  <br>*optional*|The particular type of focus that was identified by the lens.  This field may not exist for some lens types.|enum (Add, Create, Delete, Modify, Schedule, Share, View)|
|**confidence**  <br>*optional*|The level of confidence for this focus, on a scale from 0 to 1.|number|
|**end**  <br>*optional*|In the provided text, the index after the last character of this phrase.|integer|
|**focusVersion**  <br>*optional*|The version of the Focus object.|number|
|**lens**  <br>*optional*|The symbolic name of the lens that produced this focus.|enum (ActionRequest, Commitment, Question)|
|**lensId**  <br>*optional*|The auto-generated ID of the registered Watson Conversation instance.|string|
|**phrase**  <br>*optional*|The phrase in the provided text which matched this focus.|string|
|**start**  <br>*optional*|In the provided text, the index of the starting character of this phrase.|integer|


<a name="focusresponse"></a>
### FocusResponse
Results of cognitive analysis


|Name|Description|Schema|
|---|---|---|
|**focuses**  <br>*optional*||< [Focus](#focus) > array|
|**requestId**  <br>*optional*|Identifier of this cognitive request, automatically generated by the service.  <br>**Maximal length** : `64`|string|


<a name="requestentity"></a>
### RequestEntity
Entity that represents the text to be analyzed


|Name|Description|Schema|
|---|---|---|
|**text**  <br>*optional*|The text to be analyzed.  May contain multiple sentences.  <br>**Maximal length** : `10000`|string|




