void makeSms(char* msgTk, String phoneNum){
  #ifdef DEBUG
  Serial.println("Start Sending");
  Serial.println(String(RxBuff));
  #endif
  //strcpy(RxBuff, "");
  enableSendingChecking = true;
  int sizeOfArray = strlen(msgTk);
  Serial.println("SIZE of CHAR:" + String(sizeOfArray));

  sim800.println("AT+CMGS=\"" + phoneNum + "\"");    
  delay(2000);
  sim800.flush();
  for(int i=0; i<sizeOfArray; i++){
      sim800.print(msgTk[i]);
  }
  sim800.flush();
  sim800.print("\r\n");   
  sim800.println((char)26); 
  //delay(4000);
  //memset(RxBuff, 0, sizeof(RxBuff));
  //strcpy(RxBuff, "");
  lastSendingTime = millis();
  enableSendingChecking = true;
  sendingOk = false; 
  //delay(50); 
  #ifdef DEBUG
  Serial.println(String(RxBuff));
  Serial.println("End Sending");
  #endif  
}


void Gsm_Init()
{    
    delay(15000);
    sim800.println("ATE0"); 
    delay(1000);
    sim800.println("AT+IPR=9600");
    delay(1000);
    sim800.println("AT+CLTS=1");
    delay(1000);
    sim800.println("AT+CMGF=1");
    delay(1000); 
    sim800.println("AT+CMGD=1,4");
    delay(1000); 
    sim800.println("AT+CPMS=\"ME\""); 
    delay(1000); 
    sim800.println("AT+CNMI=2,2");  
    delay(1000);
    sim800.println("AT&W");  
    delay(500);
    sim800.setTimeout(50);
}
