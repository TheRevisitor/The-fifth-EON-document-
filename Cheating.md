# How to Cheat on EON
This page will also contain reverse engineering done by me and a couple people on EON.

## Setup
You will need to have some sort of coding knowledege.

Eon uses a custom /account/api/oauth/token request from epic games api to the momentum instance they run. For eon it is /v2/account/api/login/token

You will need to get a auth token via that request, then you can start by making a websocket instance and connect to the EON Matchmaker: ws://45.87.172.39:2999

To connect to the eon matchmaker you will need these headers

``      headers: {
        Authorization: "Epic-Signed mms-player account <accountid> <putplaylisthere> <putregionhere> c4c663648a35ada9e078ccdb9e64ccd 96EEAC72CAD7CD00",
        "Sec-WebSocket-Protocol": "ws",
        Pragma: "no-cache",
      }
``

Now you can create a status event .on("message") if the message contains Play in the message.name you can use the message.payload.sessionId to send a request to services.eonfn.dev/fortnite/api/matchmaking/session/:sessionId

with headers 

``
        {
          headers: {
            Authorization: `bearer ${tokenfromearlier}`,
            "X-Epic-Correlation-ID": CONFIG.CORRELATION_ID,
            "User-Agent":
              "Fortnite/++Fortnite+Release-12.41-CL-12905909 Windows/10.0.26100.1.256.64bit",
          },
``

