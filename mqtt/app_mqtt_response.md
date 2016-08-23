mqtt location messsage body
===

1. 定位 topic

        hanks ap publish => clientId/location/ringSN,
        
        app sub => clientId/location/

2. 手環收到訊息後所回傳的response => json data

3. 定位實際所回傳的 location response:(特例: 手環定位失敗, 也算是回傳成功訊息, 但APP可由status_code and message來判斷相關錯誤.)

     SUCCESS:
   
        {
            "status_code" : "000000",
            "data" : {
                "ring_sn" : "ring_name" 
                "cmd" : 1 
                "cmd_key" : "1qazxsw22"   // 可以讓APP and ring 判別前後收到順序, 等和手環ODM討論過後, 再來決定.
                "longitude" : 25.12312312      // Double
                "latitude" :  26.12312         // Double
                "timestamp" : "2002-10-02T15:00:00Z"    // String (RFC3339 normalize to UTC) => server get timestamp
                "type" : "gps"                 // String(gps/rrc_indoor/rrc_outdoor)
                "ring_response_code" : 0       // 1:true/0:false => 定位失敗, 如手環有回傳訊息, 可是返回APP中, 其中某一環節.
            },
            "message" : "success" 
        }

     FAIL:
     
        {
            "status_code" : "000000",
            "error_message" : {
                  "err_code" : "server statusCode"
                  "err_meaasge" : "xxxxfasdfasd"
            }
        }

4. 設定fence後回傳的response:

    SUCCESS:
   
        {
          "status_code" : "000000",
          "data" : {
              "ring_sn" : 
              "cmd":
              "cmd_key" : "1qazxsw22"   // 可以讓APP and ring 判別前後收到順序, 等和手環ODM討論過後, 再來決定.
              "fence_no" :          
              "timestamp" :     // String (RFC3339 normalize to UTC) => server get timestamp
              "ring_response_code" : 0       // 1:true/0:false => 定位失敗, 如手環有回傳訊息, 可是返回APP中, 其中某一環節.
          }
          "message" : "success" 
        }
  
    FAIL:
    
        {
            "status_code" : "000000",
            "error_message" : {
                "err_code" : "server statusCode"
                "err_meaasge" : "xxxxfasdfasd"
            } 
        }

