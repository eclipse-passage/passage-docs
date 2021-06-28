<!--
tags: licensing, floating
stories: floating-licensing:1
actors: app-dev, lic-operator, app-user, agent
-->
How floating licensing works
===

As opposed to personal licensing, where a user of a product-under-licensing gets one's own license pack and hosts it close to the product for single use,
floating licensing delegates actual license packs hosting and executing to a dedicated agent - Floating License Server. 

This allows number of users to exploit their installations of our product simultaneously in the scope of one floating license pack. 
  
Floating License Server
---
The Server, that is installed somewhere in the reach, 
 - hosts all floating license packs and 
 - respond to 'give me permission to use this feature' requests from our product's users via http.

Communication with the Server
---
The product 
 - asks the Server for a grant on a particular feature and, 
 - if succeed, proceeds with the feature and then, 
 - when it's over, releases the grant. 

The Server can lease several grants for the same feature at the same time, as hosted floating licence packs permit.

Full floating licensing workflow
--- 
There are four actors in the floating licensing workflow:
- _product development and management_, where
   - management [defines feature set and product release plan]() and
   - development
      - [declares licensing requirements]() in the product codebase,
      - [covers feature usages with licensing protection](),
      - [configures product to use Floating License Server]();
- _operator_, who [issues](issue-floating-license-pack.md) a [floating license pack](floating-license-pack.md), and delivers it to client
- _agent_, who [installs](floating-server-install.md) and [runs](floating-server-run.md) a Floating License Server,
- _client_ as a representative of a set of the product _users_, who [deploys floating license pack](floating-license-pack.md).

