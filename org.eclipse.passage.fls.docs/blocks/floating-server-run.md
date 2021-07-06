<!--
tags: licensing, floating
stories: floating-licensing:20
actors: agent
-->
Run Floating License Server
===

Prerequisites
---
 - Java version: 11 (developed and tested on AdoptOpenJDK 11.0.8.10)

Cli Options
---
  -server.port=8090
  [lic residence folder]
  
Cli commands 
---
Lifecycle commands (scope `fls`): 
 - start 
 - stop 
 - restart
 - state
 
Administration commands (scope `fls`):
 - upload
 
FLS licensing commands (scope `self`): 
 - licstatus 
 - licrequest


