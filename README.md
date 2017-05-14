# drools_tic_tac_toe
Tic tac toe implemented as drools rules

* If running on docker 
- Find the session 
docker ps

- Tail the log 
docker logs -f af3399eac0f1 

********************************************
1. Restart the container to reset working memory  (Using the workbench) 
2. use RESTClient to send comand to the KIEserver
in my case:
http://localhost:8180/kie-server/services/rest/server/containers/instances/TicTac

Header Name 	Header Value
Authorization	Basic a2llc2VydmVyOmtpZXNlcnZlcjEh
Content-Type	application/json
X-KIE-ContentType	JSON

Body:
-----------------------------------
{
  "lookup":"defaultKieSession", 
  "commands":[
 {"fire-all-rules":"{}"}
 ]
  }

-The server log should read:
21:49:02,964 INFO  [stdout] (default task-16) - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
21:49:02,965 INFO  [stdout] (default task-16) Game started!  player starts:x
21:49:02,995 INFO  [stdout] (default task-16) AI making move: 5 value2 = 3
21:49:02,997 INFO  [stdout] (default task-16)     set turn to: y


- put your play inserting a player move object

 {
  "lookup":"defaultKieSession", 
  "commands":[
       { "insert":{
          "object": { 
           "demo.Playermove" : { "position":"8" } 
        } }
        },
 {"fire-all-rules":"{}"}
 ]
 }
 
 ---------------------------
 See the result on the console: 
 
22:01:24,847 WARN  [org.kie.remote.common.rest.variant.AcceptHeaders] (default task-17) Ignoring unsupported locale: null
22:01:24,857 INFO  [stdout] (default task-17) Player making move: 8
22:01:24,858 INFO  [stdout] (default task-17)     set turn to: x
22:01:24,861 INFO  [stdout] (default task-17) AI making move: 9 value2 = 2
22:01:24,861 INFO  [stdout] (default task-17)     set turn to: y
22:01:24,864 INFO  [stdout] (default task-17) Angle right matches!! 
22:01:24,864 INFO  [stdout] (default task-17)   move3=1


And so on... 

 
