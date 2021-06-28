<!--
tags: licensing, floating
stories: floating-licensing:20
actors: lic-operator, app-user, agent
-->
What is in a Floating License Pack
===

Pack
---

When operator issues a floating license pack, it resides in a folder named after the pack identifier like `d2b83215-b65d-4031-a8c8-a10421d56260`.
Name of each file in the folder starts with this identifier as well. 

Files
---
There are in the folder
 - **license files**, which should be passed under control of Floating License Server and contain information of any user eligible for the license and any feature can be used by it
 - optionally, **floating access files**, one per user, which are to be passed to each of them and keep connection and authentication credentials of the Server

Each piece of content is filed both in open text and encrypted forms. General rule here is to use open text files for statistics, analysis or other internal aims, and share only encrypted versions. 

Here is a typical file structure of a floating license pack:

|file|role|action|
|:---|:---|:---|
|`pack-id`.flic|Open text of the license|Keep it for history, analytics, billing. Do not share.|
|`pack-id`.flicen|Encrypted license|Pass to agent to be deployed under Floating License Server.|
|`pack-id`_`user-id`.fla|Floating Server access file|Keep it. Do not share.|
|`pack-id`_`user-id`.flaen|Encrypted floating access file|Pass to the mentioned user to be stored close to one's installation of our product.|

Content
---
#### A license file (_*.flic_, _*.flicen_) 
hosts
   - **Floating License Server authentication** information, as each floating license is to be released for a particular residence. A license is not intended to be functional in case it is deployed on a server, that cannot be authenticated with these credentials.
   - Enlistment of all **users allowed to exploit the product** - their identifiers, authentication conditions, other info.
   - List of product features that can be used associated with amount of available grants (simultaneous usages). 
  
A product, running on a _user_'s installation, _acquires a grant_ for a _feature_, which is valid for short period (_vivid_ for 60 minutes by default). 
Since a grant is acquired, it's not accessible until it is released. 

After the _feature_'s work is over, the product _releases the grant_ and thus it becomes available for acquisition again.

##### feature grant capacity
Several product installations (users) can acquire different grants for the same feature for overlapping time slots. 
Feature grant's _capacity_ field defines this amount.
If there are no more available grants, the acquisition fails, and the product blocks the feature utilization. 

##### feature grant vivid 
A feature grant, been leased for a user, should not last long. 
Thus, a feature grant information contain instruction on how _vivid_ is the grant. 
Measured in minutes, it defines how long will the grant be valid after leased (limited by the whole license pack validity period).
After this relatively short vivid period the grant is not active, but still acquired until is explicitly released.

##### feature grant validity period
A feature grant can define its own validity period. Even if it is declared to be wider than the owning license pack validity period, at runtime it is still limited by it.
Use the ability if you want to narrow validity period for a particular feature in the pack.
 
#### A floating access file (_*.fla_, _*.flaen_)
A product installation needs to be told how to access a Floating License Server. 

Floating access file delivers this information. It contains:
  - user identifier,
  - the Server connection url components: ip address and port,
  - the Server authentication condition.
  
Each user enlisted in the license file should get such an access file.
  
Destination
---
License files are to be [hosted](floating-server-deploy-license.md) under control of the Floating License Server for which this license pack has been issued.

Precise location for floating access files should be provided by the product development, but by default it should reside on the same machine where the product is installed in `~/.passage/<product-id>/<product-version>` directory. 
